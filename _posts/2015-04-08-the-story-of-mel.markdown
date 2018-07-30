---
title: "The 'Story of Mel' Explained"
layout: post
date: 2015-04-08 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag:
- programming
star: false
category: blog
author: James Seibel
description: What it took to be an elite programmer in the early days of computing
---


<a href="http://www.catb.org/jargon/html/story-of-mel.html" target="_blank">The Story of Mel</a> is a story about a ‘Real Programmer’ that came out in the early 1980′s on Usenet. As described on its <a href="http://en.wikipedia.org/wiki/The_Story_of_Mel" target="_blank">Wikipedia page</a>:

> **The Story of Mel** is an archetypical piece of computer programming folklore. Its subject, Mel Kaye, is the canonical Real Programmer.

This is a very popular piece of programming lore, which is often reposted. Many people have read this story without fully understanding it, which is a shame, because it really gives you a taste for what it took to be an elite programmer in the early days of computing (late 1950′s / early 1960′s).

What follows is the complete story, with the technical bits explained as needed. If I make a mistake or you think something should be improved, please comment below.

## The Story of Mel
```
A recent article devoted to the macho side of programming
made the bald and unvarnished statement:

Real Programmers write in FORTRAN.

Maybe they do now,
in this decadent era of
Lite beer, hand calculators, and “user-friendly” software
but back in the Good Old Days,
when the term “software” sounded funny
and Real Computers were made out of drums and vacuum tubes,
Real Programmers wrote in machine code.
Not FORTRAN. Not RATFOR. Not, even, assembly language.
Machine Code.
Raw, unadorned, inscrutable hexadecimal numbers.
Directly.
```

Machine code is binary (1′s and 0′s). <a href="http://en.wikipedia.org/wiki/Hexadecimal#Binary_conversion" target="_blank">Hexadecimal</a> is a representation of Base 16 (0-9, A-F), so it is easy to represent 4 binary numbers in one hexadecimal character. Writing ‘A’ rather than 1010 is easier for humans to read. So Mel is a machine programmer, who wrote his binary in hexadecimal format. He didn’t use any fancy assembly language, (Add, Sub, etc.) to make coding easier- he wrote in binary code directly.

```
Lest a whole new generation of programmers
grow up in ignorance of this glorious past,
I feel duty-bound to describe,
as best I can through the generation gap,
how a Real Programmer wrote code.
I’ll call him Mel,
because that was his name.

I first met Mel when I went to work for Royal McBee Computer Corp.,
a now-defunct subsidiary of the typewriter company.
The firm manufactured the LGP-30,
a small, cheap (by the standards of the day)
drum-memory computer,
and had just started to manufacture
the RPC-4000, a much-improved,
bigger, better, faster — drum-memory computer.
Cores cost too much,
and weren’t here to stay, anyway.
(That’s why you haven’t heard of the company,
or the computer.)
```

<a href="http://en.wikipedia.org/wiki/Magnetic-core_memory" target="_blank">Core Memory</a> was a form of random access memory that used magnetic fields to store information. It was hand-manufactured by skilled factory workers, which made it expensive. Eventually it came down in cost, from $1 per bit to 1 cent per bit, but during Mel’s time it was quite expensive. Therefore, the engineers at Royal McBee, trying to target the lower-end of the computer market (an <a href="http://en.wikipedia.org/wiki/LGP-30" target="_blank">LGP-30</a> would cost about $400,000 in 2015 – however, quite cheap for computers in the 1950′s!) decided to use Drum Memory which is simpler to manufacturer and therefore cheaper. <a href="http://en.wikipedia.org/wiki/Drum_memory" target="_blank">Drum Memory</a> is much slower than Core Memory, which made the new RPC-4000 still seem less-than-ideal to a programmer despite improvements in other areas of the machine.

```
I had been hired to write a FORTRAN compiler
for this new marvel and Mel was my guide to its wonders.
Mel didn’t approve of compilers.

“If a program can’t rewrite its own code”,
he asked, “what good is it?”
```

As will be explained later, Mel used a variety of tricks that exploited quirks of the processor and drum memory that allowed him to squeeze every bit of power from the machine. These tricks were so specific to the LGP-30′s processor that no compiler could automatically generate machine code that was as fast and optimized as Mel’s. Therefore, Mel didn’t like compilers, because he’s a Real Programmer, who wants the most power possible.

About a “program <a href="http://en.wikipedia.org/wiki/Self-modifying_code" target="_blank">rewriting its own code</a>“, by modifying the region of memory that contained the program instructions, Mel could (very, very carefully) have the program modify its own instructions while it was running, effectively changing its own source code. Modern high-level languages like Python and JavaScript allow creating new code dynamically, but not mutating existing code. Compilers will not generate self-modifying code, as it’s too dangerous and not likely to be performant. However, a Real Programmer like Mel would find this an attractive feature when programming.

```
Mel had written,
in hexadecimal,
the most popular computer program the company owned.
It ran on the LGP-30
and played blackjack with potential customers
at computer shows.
Its effect was always dramatic.
The LGP-30 booth was packed at every show,
and the IBM salesmen stood around
talking to each other.
Whether or not this actually sold computers
was a question we never discussed.
```

This is mind blowing that something so complex and excellent was written directly in machine code, especially to the author who was fluent in high level languages (<a href="http://en.wikipedia.org/wiki/Fortran" target="_blank">FORTRAN</a>).

```
Mel’s job was to re-write
the blackjack program for the RPC-4000.
(Port? What does that mean?)
```

Typically porting a program to another OS or processor architecture means targeting the new OS / architecture and recompiling the source code. However, when you program directly in machine code (like Mel), you need to completely rewrite the entire program if the new processor has a different set of instructions it supports (which is expensive and time consuming). This is one reason why high level programming languages were created – portability – so that the same source code can run on different operating systems and processors.

```
The new computer had a one-plus-one
addressing scheme,
in which each machine instruction,
in addition to the operation code
and the address of the needed operand,
had a second address that indicated where, on the revolving drum,
the next instruction was located.

In modern parlance,
every single instruction was followed by a GO TO!
Put *that* in Pascal’s pipe and smoke it.
```

Machine language is a series of 1′s and 0′s. In a hypothetical 16 bit instruction scheme, the first 4 bits could be the operation code (allowing 16 maximum operations), the next 4 bits the storage register, the next 4 bits an operand register, and the next 4 bits another operand register. Therefore, if 0001 is the opcode for ‘Add’, and we want to store the result of adding register 1 and 2 into register 3, a potential binary instruction could be 0001 0011 0001 0010 (in decimal: 1 3 1 2).

In the RPC-4000 computer, the instruction of the next address was determined by an operand inside the current instruction. Normally, a program is loaded into memory sequentially. The first instruction is at address 0, the next at 1, the next at 2, and so on, and the program counter (which keeps track of the current instruction) increments each time an instruction is executed (unless a ‘jump’ causes the counter to change to something else).

However, because of the nature of drum memory, it isn’t performant to have the program counter increment sequentially between commands. Understanding this requires a brief digression into drum memory. It is critical that you understand this in order to understand the rest of The Story of Mel.

<a href="http://en.wikipedia.org/wiki/Drum_memory" target="_blank">Drum Memory</a> looks like it sounds – a rotating cylinder that is covered in a magnetic material that can be be switched between two different states (1 and 0) using electricity. State is modified using read-write ‘heads’ that are located along the drum. The drum rotates at a fixed rate, while the heads don’t move, so a head must wait for the drum to rotate into a specific position in order to read or write a certain address.

For instance, imagine a hypothetical drum with 4 ‘tracks’. Each track has its own read-write ‘head’. Each track contains 256 bits, for 1024 bits total. If you want to read the bit at address 900, the drum will send a response once bit 124 (remember, each track has 256 bits, so bit 900 is the 124th bit of the 4th track) rotated beneath the 4th head.

A side effect of this is drastically inconsistent memory response times. In modern semi-conductor based memory, access speed is typically the same no matter which RAM bank the data is in. In Drum Memory, the response time is extremely quick if the requested address is just after the current location of the head, or extremely slow if the head just missed it.

```
Mel loved the RPC-4000
because he could optimize his code:
that is, locate instructions on the drum
so that just as one finished its job,
the next would be just arriving at the “read head”
and available for immediate execution.
There was a program to do that job,
an “optimizing assembler”,
but Mel refused to use it.

“You never know where it’s going to put things”,
he explained, “so you’d have to use separate constants”.

It was a long time before I understood that remark.
Since Mel knew the numerical value
of every operation code,
and assigned his own drum addresses,
every instruction he wrote could also be considered
a numerical constant.
He could pick up an earlier “add” instruction, say,
and multiply by it,
if it had the right numeric value.
His code was not easy for someone else to modify.
```

Continuing our discussion about the drum’s read-write heads, it becomes clear that merely having each instruction sequentially written to the drum would be inefficient. This is because by the time an instruction is executed, the head would no longer be over the very next instruction. This is because the clock rate (instructions executed per second) of the processor and the drum memory are not perfectly synchronized (which is desirable, because you don’t want to bottleneck either the processor or the drum by forcing them to operate at an exactly synchronized rate).

Therefore, an ‘optimizing assembler’ was written that would take assembly code and arrange the instructions in memory locations that lined up with the drum rotation.

This would allow the programmer to write their code in sequential order, without worrying about the next-instruction operand:

```
Add R1, R2, R3, GOTO 2
Subtract R4, R2, R1, GOTO 3
Multiply R1, R2, GOTO 4
…
```

And the optimizing assembler would take the same code, and rearrange the instructions in an order that was optimized for the drum memory, automatically changing the next-instruction address operand. Our optimized code would now look like:

```
1. Add R1, R2, R3, GOTO 112
2. …
55. Multiply R1, R2, GOTO 398
56. …
112. Subtract R4, R2, R1, GOTO 55
113. …
```

Obviously, having to program your commands completely out of order using GOTO’s on each line to jump to a new instruction would be unbelievably difficult. So an optimizing assembler would do this automatically, taking the burden off of the programmer, and output reasonably efficient machine code. The next instruction would be reasonably close to the current location of the track head, minimizing seek time.

Mel never used the optimizing assembler, because Mel is a Real Programmer. He found a trick that was beyond the capabilities of the optimizing assembler that gave him more computation power, and because the optimizing assembler could not give him the same power, he hated using it.

The “constants” Mel used require some explanation.

As described before, a 16 bit processor would have instructions that looked like this:

`1001 0101 1010 1111`

If a hypothetical instruction set used the first 4 bits for the opcode, then you have 16 potential opcodes (2 ^ 4 = 16). Let’s say that the final 4 bits of the instruction were the address of the next instruction (the GOTO statements in the assembly code). Obviously, this is an example, because this system would allow only 16 instructions per program. If you had a command that looked like this:

`And R1, R2, GOTO 5`

The machine code could look like this:

`0001 0001 0010 0101`

*Which evaluates to 4389 in decimal !!!*

Therefore, using extremely careful ordering of the instructions, and by analyzing the existing locations of instructions, Mel could look at all of his instructions and treat them simultaneously as numerical constants.

If he needed to multiply a value, he could examine the location of each track head during the current instruction, see if any instruction had a ‘constant’ value that could be used, or even wait briefly for the drum to rotate a tad further, to give him a range of potential constants.

Mel saw his entire program as a living, intricate machine. The program’s source code was malleable – as the program executed, the instructions of the program could rewrite themselves. So looking at Mel’s source code didn’t show you the whole thing. When executing the program, the instructions themselves would change, so instruction 927 could start as an Add, and then switch to a Multiply.

```
I compared Mel’s hand-optimized programs
with the same code massaged by the optimizing assembler program,
and Mel’s always ran faster.
That was because the “top-down” method of program design
hadn’t been invented yet,
and Mel wouldn’t have used it anyway.
He wrote the innermost parts of his program loops first,
so they would get first choice
of the optimum address locations on the drum.
The optimizing assembler wasn’t smart enough to do it that way.
```

Rather than writing his programs by architecting a high-level design and then building out each piece, as is typically done today, Mel would first implement the loops he needed, and assign them the most efficient locations on the drum for maximum speed. So the code that ran most often (loops) would be guaranteed to run as fast as possible.

```
Mel never wrote time-delay loops, either,
even when the balky Flexowriter
required a delay between output characters to work right.
He just located instructions on the drum
so each successive one was just past the read head
when it was needed;
the drum had to execute another complete revolution
to find the next instruction.
He coined an unforgettable term for this procedure.
Although “optimum” is an absolute term,
like “unique”, it became common verbal practice
to make it relative:
“not quite optimum” or “less optimum”
or “not very optimum”.
Mel called the maximum time-delay locations
the “most pessimum”.
```

Time delay loops were needed to ensure that when using a <a href="http://en.wikipedia.org/wiki/Friden_Flexowriter#Console_terminals" target="_blank">Flexowriter</a> as output, the computer didn’t send commands too fast for it to handle. Time delay loops are bad in a computer that doesn’t have an operating system. If you write a program that uses a sleep() command in Python or Java, the operating system can swap your program out of the processor and execute other programs until you have finished sleeping.

However, in the LGP-30 there was no operating system, just a single program executing. So while your program slept, the computer was doing nothing useful.

So rather than write wasteful time delay loops, Mel would pick the worst possible location for the next instruction, which would delay the maximum amount of time, without needing to write a do-nothing loop.

```
After he finished the blackjack program
and got it to run
(“Even the initializer is optimized”,
he said proudly),
he got a Change Request from the sales department.
The program used an elegant (optimized)
random number generator
to shuffle the “cards” and deal from the “deck”,
and some of the salesmen felt it was too fair,
since sometimes the customers lost.
They wanted Mel to modify the program
so, at the setting of a sense switch on the console,
they could change the odds and let the customer win.

Mel balked.
He felt this was patently dishonest,
which it was,
and that it impinged on his personal integrity as a programmer,
which it did,
so he refused to do it.
The Head Salesman talked to Mel,
as did the Big Boss and, at the boss’s urging,
a few Fellow Programmers.
Mel finally gave in and wrote the code,
but he got the test backwards,
and, when the sense switch was turned on,
the program would cheat, winning every time.
Mel was delighted with this,
claiming his subconscious was uncontrollably ethical,
and adamantly refused to fix it.

After Mel had left the company for greener pa$ture$,
the Big Boss asked me to look at the code
and see if I could find the test and reverse it.
Somewhat reluctantly, I agreed to look.
Tracking Mel’s code was a real adventure.

I have often felt that programming is an art form,
whose real value can only be appreciated
by another versed in the same arcane art;
there are lovely gems and brilliant coups
hidden from human view and admiration, sometimes forever,
by the very nature of the process.
You can learn a lot about an individual
just by reading through his code,
even in hexadecimal.
Mel was, I think, an unsung genius.

Perhaps my greatest shock came
when I found an innocent loop that had no test in it.
No test. None.
Common sense said it had to be a closed loop,
where the program would circle, forever, endlessly.
Program control passed right through it, however,
and safely out the other side.
It took me two weeks to figure it out.
```

Every non-infinite loop has a condition that eventually exits the loop. Even if you have an infinite loop, you can still break out of it. However, the loop Mel wrote had no test or condition that allowed exiting. Yet, somehow, it still exited the loop cleanly…

```
The RPC-4000 computer had a really modern facility
called an index register.
It allowed the programmer to write a program loop
that used an indexed instruction inside;
each time through,
the number in the index register
was added to the address of that instruction,
so it would refer
to the next datum in a series.
He had only to increment the index register
each time through.
Mel never used it.
```

An index register is used to efficiently iterate through an array of data, by incrementing it for each element and then adding the current register value to the base address of the array.

```
Instead, he would pull the instruction into a machine register,
add one to its address,
and store it back.
He would then execute the modified instruction
right from the register.
The loop was written so this additional execution time
was taken into account —
just as this instruction finished,
the next one was right under the drum’s read head,
ready to go.
But the loop had no test in it.
```

This is a clever trick to increase speed without using the index register. Rather than incrementing the index register, he would increment the instruction itself (modifying the source code of the program), store it back, and execute it. The additional overhead of modifying the instruction and storing it back was just enough time for the drum to rotate into position to execute the next instruction, without an additional clock cycle to manipulate the index register.

```
The vital clue came when I noticed
the index register bit,
the bit that lay between the address
and the operation code in the instruction word,
was turned on —
yet Mel never used the index register,
leaving it zero all the time.
When the light went on it nearly blinded me.
```

In order to use the index register, there was an ‘index register bit’ which was located between the instruction address and opcode of an instruction. Mel would turn it on, which is perplexing, because Mel never used the index register…

```
He had located the data he was working on
near the top of memory —
the largest locations the instructions could address —
so, after the last datum was handled,
incrementing the instruction address
would make it overflow.
The carry would add one to the
operation code, changing it to the next one in the instruction set:
a jump instruction.
Sure enough, the next program instruction was
in address location zero,
and the program went happily on its way.
```

Operation codes (opcodes) tell the processor which operation to execute for given operands. The opcode Mel used was 1 less than the opcode for JUMP, which ‘jumps’ to another instruction rather than executing the next one sequentially.

When the final element in the array was accessed, at the very top of memory, setting the index register to 1 caused an overflow. The overflow carried over to the opcode, which would be incremented, thus changing the operation to a JUMP because the current opcode was 1 less than JUMP. The JUMP would cause the program to execute the instruction at location 0, the very bottom of memory, which is indeed where Mel placed the next instruction.

To summarize, Mel enabled the index register bit (despite not using the index register) to cause an integer overflow, and because the instruction was at the very top of memory, it had the side-effect of also incrementing the instruction’s opcode, modifying the instruction to change into a JUMP command, in order to exit an infinite loop.

This is a totally insane optimization, which is why it took the author weeks to understand it. Clearly, Mel knew the inner workings of drum memory and the processor so well that he amassed a collection of tricks to squeeze maximum performance from the computer. He would use all of them in his programs, which would always beat the compiler and optimizing assembler. Mel was a Real Programmer.

```
I haven’t kept in touch with Mel,
so I don’t know if he ever gave in to the flood of
change that has washed over programming techniques
since those long-gone days.
I like to think he didn’t.
In any event,
I was impressed enough that I quit looking for the
offending test,
telling the Big Boss I couldn’t find it.
He didn’t seem surprised.

When I left the company,
the blackjack program would still cheat
if you turned on the right sense switch,
and I think that’s how it should be.
I didn’t feel comfortable
hacking up the code of a Real Programmer.
```

## Addendum
For those of you who made it this far, congratulations. I hope you have learned something about the fine art of computer programming, and what it took to be an elite programmer of ancient computers.

Hacker News and other Internet communities routinely argue over what languages constitute ‘real programming’. PHP and JavaScript seem to be the current whipping boys, while C/C++ are what the True Programmers use.

The bottom line is, the argument is irrelevant. None of us are Real Programmers. We are abstracted away so far from what is really happening in the metal, that arguing about languages is a pointless endeavor.

I suggest being content that modern technology doesn’t require us to hack up machine code in order to keep our software running :-)