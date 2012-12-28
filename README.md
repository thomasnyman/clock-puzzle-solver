Clock Puzzle Solver
===================

Clock Puzzle Solver is a Python script for solving the "clock puzzle" mini-games
present in the Final Fantasy XIII-2 role-playing game released by Square Enix in
2012.

The clock puzzles consist of N integers from 1 to ⌊N/2⌋ arranged in a circle.
The puzzle is solved by initially picking any of the N positions in the circle.
Let the integer in the chosen position be M. Now one has to choose either the
number at position M positions clockwise, counter-clockwise from the previously
chosen integer. The solution to the puzzle is a sequence of choices such that
each integer in the circle is chosen exactly once.

Solving the clock puzzle is equivalent to finding a directed Hamiltonian path in
a directed graph with N vertices, where the directed edges describe the valid
moves around the circle. More precisely if the integer at position N is M, then
there are directed edges to the vertices M positions clockwise, or
counter-clockwise from position N.

For example in the figure below picture a) shows an example puzzle with N=6
positions labeled **a-f**. Starting at positions **a** the available moves 2
positions clockwise and counter-clockwise are to positions **c** or **e**
respectively. Picture b) shows the equivalent graph with all edges corresponding
to valid moves. One possible solution is the Hamiltonian path shown in c),
consisting of the moves **a → c → d → e → b → f**.

![Example puzzle](https://raw.github.com/thomasnyman/clock-puzzle-solver/master/doc/example.png "Figure 1. Example puzzle")

Finding a directed Hamiltonian path in a general directed graph is NP-hard. The
graphs corresponding to the clock puzzles are special cases due to their
structure where the outdegree of each vertex is 2 and the edges have a certain
symmetry due to the clockwise/counter-clockwise movement rules. Finding a
Hamiltonian path in a graph with a limited outdegree is still NP-hard, but it is
unclear if the symmetricity would allow a devising a fast algorithm for solving
these puzzles. In the puzzles present in the game N ranges from 5 to 13 which is
sufficiently small to allow those puzzles to be easily solved by brute force.

Synopsis
--------
    clock_puzzle_solver VALUES

Description
-----------

The `clock_puzzle_solver` script takes a list of values corresponding to
integers of the puzzle circle. Each value is assigned a consecutive letter
indicating its position in the ring starting with **a** for the first value.

The script outputs a sequence of positions corresponding to a solution to the
puzzle.

Examples
--------
    clock_puzzle_solver 2 2 1 1 3 2
    a → c → d → e → b → f

    clock_puzzle_solver 2 2 2 4 2 2 3 3 6 4 5 3
    a → k → f → h → e → g → j → b → d → l → i → c
