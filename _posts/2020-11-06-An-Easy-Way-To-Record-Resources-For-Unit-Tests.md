Say you are trying to unit test a function that produces a very long output.
E.g. it might be rendering a long template.

In these cases what you might end up doing is run the whole program once and keep the output you want in a file. You then copy that file into your test resources and you load it up in your unit test in order to compare it with the current output (and fail the test if the two differ).

That is fine and it works for some time. Untill you change something and the output is expectedly different. In which case you either need to dive into the resources file and fix it up or repeat the above produce-save-copy process.

Instead you can employ a simple trick to have the tests actually do that for you.

Assume next typical folder structure of a (python) project:

    proj/
        stuff/
            __init__.py
            stuff.py
            other_stuff.py
        tests/
            __init__.py
            test_stuff.py
            test_other_stuff.py

And say that your long output function lies in `stuff.py` and looks like:

    import os
    from jinja2 import Template

    def render(templ, conf):
        """
        Renders the jinja template in file templ according
        to the settings in dictionary conf
        and returns rendered result (str)
        """
        template = Template(open(templ).read())
        return template.render(conf)


Then inside the relevant test in `test_stuff.py` you can have something like:

    from .__init__ import RECORD

    def test_render(self):
        test_resource = 'resources/out'
        template = 'template.jinja'
        config = {'name': 'val', 'other_name': 'val'}
        have = render(template, config)

        # if in RECORD mode capture what we got in resources file
        if RECORD and RECORD == "yes":
            with open(test_resource, 'w+') as outf:
                outf.write(have)

        with open(test_resource, 'r') as wantfile:
            want = wantfile.read()
        self.assertEqual(have, want)


So when `RECORD` is set to a "truthy" value what happens is that the output of the function is saved as the test_resource. This saves us the trouble of going over the produce-save-copy process.

BUT

When `RECORD` is "truthy" the test will always pass. So it should be set in a manner that won't accidentally leave it "on" inside your CI pipelines.

An easy way to do that is to have it getting a value off your environment and do 
that once and for all tests. That's what the funny import 
    from .__init__ import RECORD 
does. And the value is read once for all tests in the `tests\__init__.py` file:


    import os

    RECORD = os.getenv("RECORD_TESTS")


Assuming that your CI engineer (which is probably you wearing your CI hat) has a good overview of the env vars that live in his pipeline, we can assume that the conspicuous variable `RECORD_TESTS` won't be set there or at least it won't be set by accident.

Now. Coming back to the initial senario of you making an intentional change to your function you can then run your tests once with `RECORD_TESTS` env var set -thus recording the new outputs- and then rerun your tests to make sure everything looks good.

    $> RECORD_TESTS=yes pytest
    $> pytest

The first command sets the env var just until the completion of the command so you can rest assured that the env var won't exist after it. So any subsequent tests run is done in the normal non-recording mode.
