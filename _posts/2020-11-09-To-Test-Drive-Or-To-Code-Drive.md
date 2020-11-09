Test Driven Design (TDD) is a programming methodology that has had quite a few vocal supporters at least up untill a few years ago.
In recent years though it seems like it's going out of favor and I think I understand why.

TDD is basically programming _by_ unit tests. Say you want to write a method XXX with inputs A, B and 
result C. Instead of going ahead and implement the method you first write a unit test that is testing the method: 

    def Test_X(self):
        # this fails without the correct XXX implementation
        self.assertEqual(wanted_output, XXX(a, b))

Now, with XXX actually missing, that test will fail untill you implement XXX and you implement it correct at least 
as far as the unit test is concerned.

It is an appealing idea as it gets the unit tests at the central place in the whole process. This combined 
with the wide adoption of agile methodologies during the past decade or so explains the hype about it.

But if there is one silver bullet in engineering is that there is no silver bullet in engineering.

TDD's main, albeit somewhat hidden, assumption is that _you know beforehand which method(s) you need and what their signatures will be_.
That, though, is quite rare in practice as Software is in a constant state of change especially in an agile environment where TDD is 
supposed to fit in best.

This is even more true in the begining stages of Software creation where one does not know exactly how he'll go about to solve a problem. 
Various hindrances along  the way might, and often do, require big changes in code path, data models and methods. Doing TDD along 
these stages means a lot of wasted effort as you refactor your code base again and again. And wasted effort is frustrating and unproductive. 
I think it's way more productive and better developer experience if at least during the early stages you went straight to implementation 
and you only invested in unit tests after the code base has started to be a bit less of a moving target, which usually happens after a few iterations. 
Once you get there you could switch to TDD if that's your cup of tea and maybe you should as it makes it more difficult to forget unit testing new code.

Above hybrid methodology is what I've seen in practice and I think it strikes a very good balance between productivity and tests coverage. 
I don't know if it goes by any name so lets just call it Tests After Code (TAC).


Note: There's another catch with TDD, namely a false sense of coverage. You see if you TDD you usually write one test to cover the 
yet non-existent method. There's nothing stopping you for writing more but given the hassle we just described we can assume that under 
pressure most code authors would stick to one test. You then write the method and it passes the test and that's that. Only it isn't. 
You see your method might be correct in one way but might err in many other ways. Which is why usually people write more than one tests 
for each method. Yet since the weight in TDD is in passing that initial gatekeeper test I wouldn't be surprised if that'd also be 
the only test covering your method.
