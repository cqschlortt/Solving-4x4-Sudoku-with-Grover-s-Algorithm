# Solving-4x4-Sudoku-with-Grover-s-Algorithm
Using qiskit, we solve a 4x4 sudoku puzzle by implementing Grover's Algorithm.  The code includes the creation of a diffuser and two oracles, one which solves a true sudoku (but requires too much computing power for hard puzzles) and one which actually solves Latin Squares puzzles, but allows for more empty cells.  The code requires that the input already be a valid puzzle with only one solution and does not test that these conditions are satisfied.

Both oracles require a circuit with a quantum register of size 2*(number of empty cells), since the numbers 0-3 must be represented by two bits in binary and a solution just needs to fill the empty cells.  They also will have an ancilla register of size 1 which marks when a solution has been found, as well as some other ancilla registers for condition checking and computations.

Oracle 1 solves a sudoku puzzle by testing constraints given by ordered pairs, ensuring that any two cells in each row, column, and block are not the same.  Thus it requires a list of these conditions and a circuit with an ancilla register of size len(conditions list).  The oracle works by determining if a given state satisfies all of the conditions, and if it does, marks that state as the correct state (by flipping the sign of |1>).

Oracle 2 solves a latin squares puzzle by creating lists of possible cell value permutations for each row and column, then checking if a given state is one of these permutations for each row and column.  Thus is requires an ancilla register of size 8.  The oracle works by determining if a given state fits a permutation for all rows and columns, and it does, it marks that state.

The diffuser is the same for both oracles as it only is appended to the part of the circuit which represents the empty cells in the puzzle.  

The algorithm which computes and returns the solution is also very similar for both oracles, altered slightly since oracle 1 and oracle 2 require different circuits.

The code uses a single puzzle with two empty cells, but the puzzle can be adapted to test solutions for other puzzles as long as the number of empty cells for the first oracle is less than approximatly 4 (to make sure code can actually run with standard memory) and the number of empty cells for the second oracle is less than 8 (to make sure code can run with standard memory),
