# abductive-logic
Given a partial program and a set of goals, abductive reasoning allows us to come up with  other predicates of the program that would make the goal(s) true

Both the programs were compiled and tested using XSB v3.5.0 on Linux.
The costs and integrity constraints are defined as additional facts in the input program,
which is loaded at runtime.

1. abduction.P
----------------

This program consists of the getAbduction/2 predicate which will return the set of all 
abducibles in a list.
Upon backtracking , it returns the alternate abducibles.
The program P is loaded dynamically, the query Q is given as an input parameter to the 
above predicate and list L is returned with the set of abducibles.

SAMPLE OUTPUT
----------------
 
sowmy@Dalek:~/Course/Assignment/Prolog/Assgn 3$ xsb

| ?- [abduction].
| ?- load_dyn(input).
| ?- getAbduction(citizen(john), L).

L = [t_not(bornInUSA(john)),t_resident(john),naturalized(john)];
L = [t_not(bornInUSA(john)),t_not(bornInUSA(mary)),t_resident(mary),naturalized(mary),registered(mary)];
L = [bornInUSA(john)];
L = [citizen(john)];
no
| ?- 

                                ======== x ================ x ================ x ========
                                
2. minCost.P
---------------

This program consists of 2 predicates:
i) findAllCost/3 - that returns the associated cost of each abducible returned 
by the above getAbduction/2.                                

ii) findMinCost/3 - that returns the least costing abducible among all alternates
 and the corresponding cost.
                            
SAMPLE OUTPUT
---------------
                                
sowmy@Dalek:~/Course/Assignment/Prolog/Assgn 3$ xsb

| ?- load_dyn(input).
| ?- findAllCost(citizen(john), L, C).

L = [t_not(bornInUSA(john)),t_resident(john),naturalized(john)]
C = 1.2000;

L = [t_not(bornInUSA(john)),t_not(bornInUSA(mary)),t_resident(mary),naturalized(mary),registered(mary)]
C = 2.3000;

L = [bornInUSA(john)]
C = 0.5000;

no
| ?- findMinCost(citizen(john), L, C).

L = [bornInUSA(john)]
C = 0.5000;

no
| ?-                         
