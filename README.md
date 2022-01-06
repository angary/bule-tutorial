# Bule Tutorial

## What is Bule?

Bule is a tool used to create CNF (conjunctive normal form) encodings for SAT solving.

- SAT (Boolean Satisfiability) is the problem of determining if there exists an assignment of True or False to the variables of a boolean formula.
- A formula consists of 
  - **Variables**: Variables that can either be true or false
  - **Parentheses**: Things in parentheses are evaluated first
  - **Conjunction**: AND operator (`||`)
  - **Disjunction**: OR operator (`&&`)
  - **Negation**: NOT operator (`!`)
- A formula is in CNF if:
  - It is a conjunction of clause(s), where a clause is a disjunction of literals
  - English form: Everything inside the brackets are "OR"ed together, and all the brackets are "AND"ed together
  - Example: `(x1 OR NOT x2) AND (NOT x1 OR x2 OR x3) AND NOT x1` from [Wikipedia](https://en.wikipedia.org/wiki/Boolean_satisfiability_problem#:~:text=clause.%20The%20formula-,(x1%20%E2%88%A8%20%C2%ACx2)%20%E2%88%A7%20(%C2%ACx1%20%E2%88%A8%20x2%20%E2%88%A8%20x3)%20%E2%88%A7%20%C2%ACx1,-is%20in%20conjunctive)

Bule helps you "encode" or "represent" these boolean formulas cleanly.
You can then use a SAT solver to solve these formulas (find an assignment of True or False to the variables s.t. the formula evaluates to True).

It also does more things.

## Formula Representation

Representation of `(x1 OR NOT x2) AND (NOT x1 OR x2 OR x3) AND NOT x1` in Bule: 

```
 x1 | ~x2.
~x1 |  x2 | x3.
~x1.
```
[Bule File](basic.bul)

**Note:**
- Each clause is on a different line, OR is done through `|` and NOT is done through `~`.
- A line ends with a `.` (a bit like a semicolon in most programming languages).
- Formula variables have to be declared with `#exists[0]`

> How many different assignments of Trues and Falses will evaluate to True for this formula (solve manually)?

To solve an formula:
```
bule2 --solve basic.bul
```

To show all models (all assignments that can be True):
```
bule2 --solve --models 0 basic.bul
```

## Encoding Problems

If we can represent a problem in CNF form, then we can use SAT solvers to solve for it.

Graph Colouring is a problem where given a graph, find an assignment of colours to each vertex such that adjacent vertices (vertices that are one edge apart) are not the same colour.

Example:

![graph](graph.png)

> To represent this in CNF, what would the variables represent?

We want to find an assignment of colours.
Because we are only working with boolean variables, we can only represent if something is something, or is not something.
As a result, we need a variable for each colour-vertex pair).

> To represent this in CNF, what would the clauses be?

We have to determine the rules:

1. Every vertex has to be given a colour.
2. Adjacent vertices cannot be the same colour.

> How can we code this up?

## Grounding

This process gets quite intensive if we were to add more colours, vertices, and edges.
Currently there is a lot of copy and pasting, but using bule we can perform grounding, which is a process of taking a higher level language or representation and then converting it to basic CNF.

> Show disjunction and conjunction

We can also ground multiple files.

For example, it may be ideal to have the encoding of vertex colouring in one file and then the encoding of a graph in another.

