# Matrix Multiplication Using MapReduce

## What is Matrix Multiplication?

When you multiply two matrices (let's call them \(A\) and \(B\)), you get a new matrix \(C\). Each number in \(C\) is found by multiplying and adding numbers from \(A\) and \(B\).

## What is MapReduce?

MapReduce is like a recipe for doing big tasks by breaking them into smaller steps. It has two main steps: "Map" and "Reduce".

## Steps to Multiply Matrices Using MapReduce

### Preprocessing

1. We start with two matrices \(A\) and \(B\).
2. Each number in \(A\) and \(B\) is turned into a pair of data (like a name tag).

### Map Step

1. Think of this as making copies of the data in a way that gets them ready for adding together.
2. For each number in \(A\), we make several pairs with it.
3. For each number in \(B\), we do the same.

### Shuffle Step

This step groups the data pairs so that all pairs needed to calculate a single number in matrix \(C\) are together.

### Reduce Step

In this step, we take each group of pairs and do the actual multiplication and adding to get each number in matrix \(C\).

## Example with Small Matrices

Let's say we have:

Matrix \(A\):
\[ A = \begin{pmatrix} 1 & 2 \\ 3 & 4 \end{pmatrix} \]

Matrix \(B\):
\[ B = \begin{pmatrix} 5 & 6 \\ 7 & 8 \end{pmatrix} \]

We want to find matrix \(C\).

### Preprocessing

We make pairs:

- From \(A\): 
  - \((A, 1, 1, 1)\)
  - \((A, 1, 2, 2)\)
  - \((A, 2, 1, 3)\)
  - \((A, 2, 2, 4)\)
  
- From \(B\): 
  - \((B, 1, 1, 5)\)
  - \((B, 1, 2, 6)\)
  - \((B, 2, 1, 7)\)
  - \((B, 2, 2, 8)\)

### Map Step

For each number in \(A\) and \(B\), we create pairs:

- For \((A, 1, 1, 1)\): create \((1, 1, 1)\), \((1, 2, 1)\)
- For \((A, 1, 2, 2)\): create \((1, 1, 2)\), \((1, 2, 2)\)
- And similar for other numbers.

### Shuffle Step

Group pairs:

- All pairs needed for calculating \(C_{11}\) together.
- All pairs needed for calculating \(C_{12}\) together.
- And so on.

### Reduce Step

Calculate each number in \(C\) by multiplying and adding:

- For \(C_{11}\): \((1 \times 5) + (2 \times 7) = 5 + 14 = 19\)
- For \(C_{12}\): \((1 \times 6) + (2 \times 8) = 6 + 16 = 22\)
- And so on.

Final matrix \(C\):
\[ C = \begin{pmatrix} 19 & 22 \\ 43 & 50 \end{pmatrix} \]

## Summary

1. **Preprocessing**: Turn numbers into pairs.
2. **Map**: Prepare pairs for adding.
3. **Shuffle**: Group pairs needed for each number in the result.
4. **Reduce**: Multiply and add to get the final result.

## Python Implementation Using `mrjob`

Here's how you can implement this using Python and the `mrjob` library.

1. **Install the `mrjob` library** (if not already installed):
   ```bash
   pip install mrjob
