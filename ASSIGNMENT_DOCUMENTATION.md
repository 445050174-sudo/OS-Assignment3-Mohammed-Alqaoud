# Assignment 3 - Complete Documentation

**Student Name**: [Mohammed Nasser Alqaoud ]  
**Student ID**: [445050174]  
**Date Submitted**: [5/1/2026]

---

## 🎥 VIDEO DEMONSTRATION LINK (REQUIRED)

> **⚠️ IMPORTANT: This section is REQUIRED for grading!**
> 
> Upload your 3-5 minute video to your **PERSONAL Gmail Google Drive** (NOT university email).
> Set sharing to "Anyone with the link can view".
> Test the link in incognito/private mode before submitting.

**Video Link**: [Paste your personal Gmail Google Drive link here]

**Video filename**: `[YourStudentID]_Assignment3_Synchronization.mp4`

**Verification**:
- [ ] Link is accessible (tested in incognito mode)
- [ ] Video is 3-5 minutes long
- [ ] Video shows code walkthrough and commits
- [ ] Video has clear audio
- [ ] Uploaded to PERSONAL Gmail (not @std.psau.edu.sa)

---

## Part 1: Development Log (1 mark)

Document your development process with **minimum 3 entries** showing progression:

    Forked the repo and set my student ID . 

    Added ReentrantLock to protect shared countres . 

    Protected execution log using ReentrantLock. 
    
    Implement Semaphore to control CPU access and tested the program . 


### Entry 1 - [5/1/2026,2]
**What I implemented**: 
Forked the repository , cloned the project, and updated my student ID .

**Challenges encountered**: 
    Understanding how to use GitHub and clone the repository correctly. 

**How I solved it**: 
    Used Visual Studio Code terminal and Git commands step by step.

**Testing approach**: 
    Checked if the projec opened and compiled correctly.

**Time spent**: 
 20 minutes 

---

### Entry 2 - [5/1/2026, 2:40 ]
**What I implemented**: 
    Added ReentrantLock to protect shared counters

**Challenges encountered**: 
    Understanding where crittcal sections should be protected . 

**How I solved it**: 
    Placed lock and unlock statemats inside try-finally blocks.

**Testing approach**: 
Ran the program several times and checked counter valuse .

**Time spent**: 
    35 minutes 

### Entry 3 - [5/1/2026, 3:20 ]
**What I implemented**: 
Protected executionLog ArrayList using ReentrantLock. 

**Challenges encountered**: 
    preventing concurrent modification issues. 


**How I solved it**: 
    Used a separate lock for the execution log .

**Testing approach**: 
Executed the program multiple times and verified no exceptions 
occurred .

**Time spent**: 
25 minutes 

---

### Entry 4 - [5/1/2026, 4:00 ] 
**What I implemented**: 
    Implemented Semaphore to control CPU access.

**Challenges encountered**: 
    Understanding when to acquire and release the semaphore.

**How I solved it**: 
    Used acquire() before esecution and release() inside finally block.

**Testing approach**: 
Verfied that  processes executed correctly without synchronization problems.

**Time spent**: 
40 minutes 

---

### Entry 5 - [5/1/2026, 5:00 ]
**What I implemented**: 
Completed testing, reviewed the code, and prepared documentation.

**Challenges encountered**: 
    Making shre all synchronization mechanisms worked correctly. 

**How I solved it**: 
    Repeated testing and checked program output consistency.

**Testing approach**: 
Ran the application multiple times and reviwed execution logs. 

**Time spent**: 
30 minutes 

---

## Part 2: Technical Questions (1 mark)

### Question 1: Race Conditions
**Q**: Identify and explain TWO race conditions in the original code. For each:
- What shared resource is affected?
- Why is concurrent access a problem?
- What incorrect behavior could occur?

**Your Answer**:

[Your answer here - 4-6 sentences with code examples]
The first race condition was in the shared counters such as contextSwitchCount and completedProcessCount. Multiple threads could update these variables at the same time, causing incorrect values.

The second race condition was in executionLog because ArrayList is not thread-safe. If multiple threads tried to add data simultaneously, the program could produce inconsistent logs or throw ConcurrentModificationException.

Using synchronization prevented incorrect updates and protected shared resources from concurrent access.

---

### Question 2: Locks vs Semaphores
**Q**: Explain the difference between ReentrantLock and Semaphore. Where did you use each in your code and why?

**Your Answer**:
ReentrantLock is used for mutual exclusion to protect critical sections and shared variables. I used it for shared counters and executionLog to make sure only one thread accesses them at a time.

Semaphore controls the number of threads allowed to access a resource simultaneously. I used Semaphore to limit CPU access and allow only one process to execute at a time.

[Your answer here - explain your implementation choices]

---

### Question 3: Deadlock Prevention
**Q**: What is deadlock? Explain TWO prevention techniques and what you did to prevent deadlocks in your code.

**Your Answer**:

Deadlock happens when threads wait for each other forever and none of them can continue execution.

The first prevention technique used was try-finally blocks to guarantee that locks and semaphores are always released.

The second technique was using simple lock management without nested locks, which reduced the possibility of circular waiting between threads.
[Your answer here - reference try-finally blocks, lock ordering, etc.]

---

### Question 4: Lock Granularity Design Decision 
**Q**: For Task 1 (protecting the three counters), explain your lock design choice:
- Did you use ONE lock for all three counters (coarse-grained) OR separate locks for each counter (fine-grained)?
- Explain WHY you made this choice
- What are the trade-offs between the two approaches?
- Given that the three counters are independent, which approach provides better concurrency and why?

**Your Answer**:

I used one lock for all shared counters because the implementation was simpler and easier to manage. Using a single lock reduced complexity and made synchronization easier to understand.

The trade-off is that coarse-grained locking reduces concurrency because only one thread can access all counters at a time. Fine-grained locking would allow better concurrency by using separate locks for each counter.

Since the counters are independent, separate locks could improve performance because different threads could update different counters simultaneously. However, for this assignment, using one lock was enough and made the code cleaner and safer.

[Your answer here - explain coarse-grained vs fine-grained locking, independence of counters, concurrency implications. Show understanding of when to use each approach. 5-8 sentences expected.]

---

## Part 3: Synchronization Analysis (1 mark)

### Critical Section #1: Counter Variables

**Which variables**: 
contextSwitchCount, completedProcessCount, totalWaitingTime

**Why they need protection**: 
Multiple threads update these variables simultaneously which may cause inconsistent values.

**Synchronization mechanism used**: 
ReentrantLock

**Code snippet**:
```java
counterLock.lock();
try { contextSwitchCount++;

 }finally { counterLock.unlock(); }
 

// Paste your implementation here
```

**Justification**: 

The lock guarantees mutual exclusion and prevents race conditions during updates.

---

### Critical Section #2: Execution Log

**What resource**: 
executionLog ArrayList

**Why it needs protection**: 
ArrayList is not thread-safe and concurrent modifications may cause exceptions.

**Synchronization mechanism used**: 

ReentrantLock

**Code snippet**:
```java
logLock.lock(); 

try { executionLog.add(message);

 } finally { logLock.unlock(); }
// Paste your implementation here
```

**Justification**: 
The lock protects the execution log from concurrent access and ensures safe updates.

---

### Critical Section #3: CPU Semaphore

**Purpose of semaphore**: 
To control CPU access and limit concurrent execution.

**Number of permits and why**: 
1 permit because only one process should execute at a time.

**Where implemented**: 
Inside run() and runToCompletion() methods.

**Code snippet**:
```java
SharedResources.cpuSemaphore.acquire();

 try {  process execution 
 
 } finally { SharedResources.cpuSemaphore.release(); }
// Paste your implementation here
```

**Effect on program behavior**: 
The semaphore ensured controlled execution and prevented simultaneous CPU access by multiple processes.

---

## Part 4: Testing and Verification (2 marks)

### Test 1: Consistency Check
**What I tested**: Running program multiple times to verify consistent results

**Testing procedure**: 
```bash
javac SchedulerSimulationSync.java 
java SchedulerSimulationSync
# Commands used (run the program at least 5 times)
```

**Results**: 
(Show that running multiple times produces consistent, correct results)
The program executed correctly each time and produced stable counter values.

**Why synchronization is necessary**: 
(Explain what race conditions COULD occur without synchronization, even if you didn't observe them. Explain which shared resources need protection and why.)
Without synchronization, multiple threads could update shared variables at the same time, causing incorrect counter values and inconsistent execution logs.

**Conclusion**: 
    Synchronization successfully protected shared resources and improved program stability.
---

### Test 2: Exception Testing
**What I tested**: Checking for ConcurrentModificationException

**Testing procedure**: 
Executed the program repeatedly while multiple threads updated executionLog.

**Results**: 
No exceptions occurred after adding synchronization.

**What this proves**: 
The execution log was safely protected from concurrent modifications.

---

### Test 3: Correctness Verification
**What I tested**: Verifying correct final values (total burst time, context switches, etc.)

**Expected values**: 
All processes should complete successfully and counters should remain consistent.

**Actual values**: 
The results matched expected behavior during all tests.

**Analysis**: 
Synchronization mechanisms maintained correct execution and data consistency.

---

### Test 4: Different Scenarios
**Scenario tested**: [e.g., different time quantum, more processes, etc.]

**Purpose**: 
To verify synchronization under different execution conditions.

**Results**: 
The program remained stable and synchronized correctly.

**What I learned**: 
Synchronization mechanisms work correctly even with different scheduling scenarios.

---

## Part 5: Reflection and Learning

### What I learned about synchronization:

[6-8 sentences about key concepts, challenges, insights]

I learned how synchronization is important in multithreaded applications. Shared resources can produce incorrect results when accessed by multiple threads simultaneously. ReentrantLock protects critical sections and ensures mutual exclusion. Semaphore controls access to limited resources such as CPU execution. I also learned the importance of try-finally blocks to prevent deadlocks and guarantee resource release. Testing synchronization multiple times helped verify program stability and correctness. This assignment improved my understanding of thread safety and concurrent programming.

---

### Real-world applications:

Give TWO examples where synchronization is critical:

**Example 1**: 
Banking systems where multiple users access and update account balances simultaneously.

**Example 2**: 
Operating systems that manage CPU scheduling and process synchronization.

---

### How I would explain synchronization to others:

[Explain to someone who just finished Assignment 1 - use simple terms and analogies]
Synchronization is a way to organize how threads access shared resources safely. Without synchronization, threads may modify the same data at the same time and produce incorrect results. Locks allow only one thread to access critical sections, while semaphores control how many threads can access a resource simultaneously. It is similar to controlling access to a room using a key so only authorized people enter safely.

---

## Part 6: GitHub Repository Information

**Repository URL**: 
https://github.com/yourusername/OS-Assignment3-Mohammed-Alqaoud

**Number of commits**: 
    4
**Commit messages**: 
1. Set student ID
2. part 1 - Added ReentrantLock for shared counters
3. part 2 - Protected execution log using lock
4. part 3 - Implemented semaphore synchronization

---

## Summary

**Total time spent on assignment**: 
    4 hours  
**Key takeaways**: 
1. Understanding race conditions
2. Using ReentrantLock and Semaphore correctly
3. Protecting shared resources in multithreaded programs

**Most challenging aspect**: 
Understanding synchronization and identifying critical sections.

**What I'm most proud of**: 
Successfully implementing synchronization and achieving stable program execution.

---

**End of Documentation**
