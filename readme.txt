This program takes a series of natural numbers (excl. 0) separated by newlines,
and returns "1\t2\t...\t(n^2)\n" to standard in - reusable!
Timings for the input tokens are output to standard error.

Threads are managed by a fixed thread pool executor, using t threads.

You may notice that there exist "DoubleMinusOne" and "Square" actors:
They are composite actors, ie: they create their child actors, place them on the execution queue, then exit.

There are two channel types available: Queue channels and stream channels

Queue channels are used for inter-actor message passing.
To process an input, actors place a consumer object on the channel's wait queue.
When new values are made available, the sending actor will invoke the next consumer in the queue on the thread executor.

Stream channels are used to read from standard in and write to standard out.
Yes, it's not a "pure" actor but the functionality is pretty much identical.

As seen from the flow chart PDF, we have a recursive definition for n^2.
Quite simply, SquareActor will spawn another SquareActor that will take n-1 as its token.