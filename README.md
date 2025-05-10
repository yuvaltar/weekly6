https://github.com/yuvaltar/weekly6.git
# weekly6
yuval tarnopolsky 322982810
### part 3:
We created two threads that each increment bar 10,000 times.
Since bar++ is not atomic, both threads often override with each other and 
ruin the expected result wich is 2000. usuly we get between 1000-2000
This happens because:
- The operation bar++ is not synchronized.
- Both threads may read `bar` at the same time, increment it
- and write back the same value — losing one increment.
### part 4:
synchronized on an instance method makes that only one thread at a time
can run that method on a specific instance.
so no increments are overriten and lost.
### part 5:
synchronized(this) locks the same monitor as synchronized on the method.
This still ensures mutual exclusion for the critical section bar++, just with more control over what is locked.
getBar() is no longer synchronized, but that’s okay in this simple case, since it only reads.
### Task 6:
We created 10 threads, each incrementing bar 10 million times. This should result in bar = 100000000.
but we got 40959970 86
This shows that race conditions are a major issue in multithreaded code without synchronization.
### Task 7:
synchronized(this) makes the increment operation thread-safe.

Same test as Task 6, but now we use:
public void baz() {
    synchronized(this) {
        bar++;
    }
}
However, threads must wait for the lock so
this time it was much much slower but did print 10000000
