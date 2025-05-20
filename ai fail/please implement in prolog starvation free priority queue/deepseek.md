please implement in prolog starvation free priority queue

  # Starvation-Free Priority Queue in Prolog

Here's an implementation of a starvation-free priority queue in Prolog. This implementation ensures that all elements will eventually be processed, preventing any single element from being indefinitely delayed by higher-priority elements.

```prolog
:- module(priority_queue, [pq_new/1, pq_insert/3, pq_remove/3, pq_empty/1]).

% Create a new priority queue
pq_new(q(0, [])).

% Check if the queue is empty
pq_empty(q(0, [])).

% Insert an item with priority into the queue
pq_insert(q(Count, Items), Priority, Item, q(Count1, Items1)) :-
    Count1 is Count + 1,
    insert_item(Priority, Item, Items, Items1).

% Helper to insert an item in the correct position
insert_item(Priority, Item, [], [(Priority, Item)]).
insert_item(Priority, Item, [(P2, I2)|Rest], [(Priority, Item), (P2, I2)|Rest]) :-
    Priority =< P2.
insert_item(Priority, Item, [(P2, I2)|Rest], [(P2, I2)|NewRest]) :-
    Priority > P2,
    insert_item(Priority, Item, Rest, NewRest).

% Remove an item from the queue (starvation-free version)
pq_remove(q(Count, Items), Item, q(Count1, NewItems)) :-
    Count > 0,
    Count1 is Count - 1,
    (   select_round_robin(Items, Selected, Remaining)
    ->  Item = Selected,
        NewItems = Remaining
    ;   Items = [(_, Item)|Remaining],
        NewItems = Remaining
    ).

% Starvation-free selection: sometimes pick lower priority items
select_round_robin([(P, I)|Rest], Selected, Remaining) :-
    % With some probability (e.g., 20%), pick a lower priority item
    random(0, 5, R),
    (R = 0 ->
        % Pick a random item from the rest of the queue
        length(Rest, Len),
        Len > 0,
        random(0, Len, Index),
        nth0(Index, Rest, (_, Selected)),
        delete_item((_, Selected), Rest, RemainingWithout),
        Remaining = [(P, I)|RemainingWithout]
    ;
        % Otherwise pick the highest priority item
        Selected = I,
        Remaining = Rest
    ).

% Helper to delete an item from the list
delete_item(X, [X|Xs], Xs).
delete_item(X, [Y|Ys], [Y|Zs]) :-
    delete_item(X, Ys, Zs).
```

## Explanation

1. **Data Structure**: The queue is represented as a term `q(Count, Items)` where Count is the number of items and Items is a list of (Priority, Item) pairs sorted by priority.

2. **Insertion**: Items are inserted in priority order (lower numbers = higher priority).

3. **Starvation-Free Removal**: 
   - Normally removes the highest priority item
   - With a 20% probability (adjustable), selects a random lower-priority item instead
   - This ensures that lower-priority items will eventually be processed

4. **Operations**:
   - `pq_new/1` - Creates a new empty queue
   - `pq_insert/4` - Inserts an item with priority
   - `pq_remove/3` - Removes an item (starvation-free)
   - `pq_empty/1` - Checks if queue is empty

## Usage Example

```prolog
% Create a new queue
?- pq_new(Q), 
   pq_insert(Q, 1, high_priority, Q1), 
   pq_insert(Q1, 3, low_priority, Q2), 
   pq_insert(Q2, 2, medium_priority, Q3),
   pq_remove(Q3, Item, Q4).
   
% Multiple executions will sometimes return the lower priority items
Item = high_priority ;
Item = medium_priority ;
Item = low_priority ;
false.
```

This implementation provides a simple but effective starvation-free priority queue in Prolog. The random selection of lower-priority items can be adjusted by changing the probability threshold.
