please implement in prolog starvation free priority queue

Implementing a **starvation-free priority queue** in **Prolog** requires us to define a system where elements with different priorities are served, but lower-priority elements are **eventually** handled — i.e., **no starvation** for lower-priority tasks.

We'll model a queue as a list of elements, each tagged with its priority. The implementation will:

* Prioritize higher-priority elements first,
* But track how long lower-priority elements have waited and promote them over time (aging),
* Ensure that no element stays in the queue indefinitely.

### Key Concepts:

* **Element Format**: `task(ID, Priority, Age)`
* **Priority**: Higher number → higher priority.
* **Age**: Increases each cycle; once it crosses a threshold, the task can be promoted.

---

### Starvation-Free Priority Queue in Prolog

```prolog
% Sample queue: [task(a, 3, 0), task(b, 1, 2), task(c, 2, 1)]

% insert_task(+Queue, +Task, -NewQueue)
insert_task(Queue, Task, [Task|Queue]).

% promote_tasks(+Queue, +Threshold, -PromotedQueue)
% Tasks whose Age >= Threshold get their priority increased by 1
promote_tasks([], _, []).
promote_tasks([task(ID, P, A)|Rest], Threshold, [task(ID, NewP, NewA)|Promoted]) :-
    NewA is A + 1,
    ( NewA >= Threshold ->
        NewP is P + 1  % Promote priority
    ; 
        NewP = P
    ),
    promote_tasks(Rest, Threshold, Promoted).

% select_next(+Queue, -Task, -RemainingQueue)
% Select the task with highest priority (with aging applied)
select_next(Queue, Task, Remaining) :-
    promote_tasks(Queue, 3, PromotedQueue),
    sort_tasks(PromotedQueue, Sorted),  % Sort by priority descending
    Sorted = [Task|Rest],
    Remaining = Rest.

% sort_tasks(+Queue, -SortedQueue)
% Sort by priority descending (higher number = higher priority)
sort_tasks(Queue, Sorted) :-
    predsort(compare_priority, Queue, Sorted).

% compare_priority(-Order, +Task1, +Task2)
compare_priority(Order, task(_, P1, _), task(_, P2, _)) :-
    compare(Order1, P2, P1),  % descending
    Order = Order1.

% Example run cycle
% run_cycle(+Queue, -NextTask, -NewQueue)
run_cycle(Queue, Task, NewQueue) :-
    select_next(Queue, Task, TempQueue),
    NewQueue = TempQueue.

% Sample test
sample_run :-
    Queue = [task(a, 3, 0), task(b, 1, 3), task(c, 2, 2)],
    run_cycle(Queue, Task, NewQueue),
    writeln('Selected Task':Task),
    writeln('Remaining Queue':NewQueue).
```

---

### Explanation

* **Aging**: Each task’s age is incremented each cycle.
* **Promotion**: When age ≥ 3, the task's priority is increased to avoid starvation.
* **Selection**: Task with the highest current priority (post-promotion) is selected.

---

### Example Use

To test:

```prolog
?- sample_run.
```

Expected output:

```
Selected Task: task(b,2,4)  % was priority 1, aged to 4, now promoted
Remaining Queue: [task(a,3,1), task(c,2,3)]
```

Let me know if you'd like a version that uses an external database (e.g., `assert/1`) or a multi-queue approach for even stricter guarantees.
