Just finished reading the report ["Reactive Microservices Architecture"](https://www.lightbend.com/blog/reactive-microservices-architecture-free-oreilly-report-by-lightbend-cto-jonas-boner).

Very informative and comprehensive in its scope. Highly recommended to anyone building or 
tending modern distributed systems.

Amongst the highlights that stuck with me:
> This is the Unix philosophy: Write programs that do one thing and do it well. Write programs to work together.—Doug McIlroy

It is my humble opinion that a huge portion of what is to be said of good system design has already been said in the way Unix was designed and a lot of what is bubbling up now and then as silver bullets are in fact bits and pieces of that early philosophy taken out of its grander context. That very quote about doing one thing well for instance was then brought into Object Oriented world as Single Responsibility Principle and, along with other similar maxims, were burrying more basic tenets under overengineered/unmaintainable designs that they were supposed to alleviate. See next quote for an indication of what might have gone wrong there. Microservices as a trend were initially going against complexity -I am a proponent of the line of thinking stating that a Microservice should be minimal- but in practice I see a lot of them degenerating to a "micro"monoliths.

> Smalltalk  is  not  only  NOT  its  syntax  or  the  class  library,  it  is  not even  about  classes.  I’m  sorry  that  I  long  ago  coined  the  term“objects”  for  this  topic  because  it  gets  many  people  to  focus  on  the lesser idea. The big idea is ‘messaging’.—Alan Kay

That, together with immutability, is probably the best tools against complexity. I'm very happy to see newer tooling such as Golang, investing in this idea. (Erlang has been doing so for decades now with extraordinary results in terms of stable and scalable designs).

> one Microservice  is  no  Microservice — they  come  in  systems.  Like  humans they act autonomously and therefore need to communicate and col‐laborate with others to solve problems—and as with humans, it is in collaboration that both the most interesting opportunities and chal‐lenging problems arise.

Ignore this and you're set for chatty, inefficient microservices that won't be able to scale.

> You  have  to  start  by  looking  at  the  data  and  work  with  a  domainexpert to understand its relationships, guarantees and integrity con‐straints from a business perspective, exploiting reality.This  often  includes  denormalizing  the  data.  Continue  by  definingthe  consistency  (transactional)  boundaries  in  the  system,  within which you can rely on strong consistency. Then you should let theseboundaries drive the design and scoping of the Microservices. If youdesign  your  services  with  data  dependencies  and  relationships  inmind  it  is  possible  to  reduce,  and  sometimes  completely  eliminate,the coupling of data

Data is more often than not the elephant in the room. Get the data model and sharing wrong and you might bring down the most scalable architectures.
