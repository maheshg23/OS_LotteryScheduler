# Operating System (OS-6233) NYU Spring 2020 Lab 3 

## Lottery Scheduling 

In this assignment, you will implement and test lottery scheduling, a randomized algorithm that
allows processes to receive a proportional share of the CPU without explicitly tracking how long
each process has been run.

1. Each `struct proc` has an additional field, `tickets`,that tracks how many tickets it has.  
2. New processes are assigned 20 lottery tickets when they are created.  
3. When the scheduler runs, it picks a random number between 0 and the total number of
tickets. It then uses the algorithm described in class to loop over runnable processes and
pick the one with the winning ticket.  
4. User processes have a new system call, `settickets`, that allows a process to specify how
many lottery tickets it wants. Normally this would be a bad idea, since it would let a
process hog the CPU by specifying an arbitrary number of tickets – but xv6 has no
security anyway, so this is not that big a deal.  


Once you have implemented this, you will want to test that the scheduler works. Aside from
basic tests that the system is still functioning, you should verify that allocating more tickets to a
process does increase its share of the CPU allotted by the scheduler.  

Included in the source distribution is a new program, `lotterytest`, which forks two children, sets
their priorities, and runs a CPU-intensive task in each, timing the results. The test assigns 80
tickets to one and 20 to the other, so the first should be scheduled 4 times as often as the second
(an 80% / 20% split).  

To build `lotterytest`, just add it to the `UPROGS` list in the `Makefile` (taking care to use a tab
character for indentation rather than 4 spaces). Note that it will not compile until you have added
the `settickets` system call.  

By running lotterytest a few times, you should be able to verify that the process with 80
tickets finishes sooner than the process with only 20.  
