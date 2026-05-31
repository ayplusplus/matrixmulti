# Multithreaded Matrix Multiplication in C

A multithreaded matrix multiplication program written in C using POSIX pthreads. Each cell of the resulting matrix is computed in parallel by its own thread, demonstrating concurrent programming concepts including thread lifecycle management, dynamic memory allocation, and shared output writing.

---

## ✨ Features

- **Multithreaded Computation** — Spawns one thread per output cell, computing all values in parallel
- **Dynamic Thread Management** — Threads are created, joined, and cleaned up properly using `pthread_create` and `pthread_join`
- **File-Based Input** — Reads two matrices from a text file, supporting up to 10x10 matrices
- **Input Validation** — Checks that matrix dimensions are compatible before multiplying (columns of A must equal rows of B)
- **Formatted Output** — Prints Matrix A, Matrix B, and the result Matrix C with aligned columns
- **Memory Safety** — Each thread receives its own dynamically allocated instruction struct, freed after use

---

## 🗂️ File Structure

```
Matrix-Multiplication/
│
├── matrix.c        # Main C source file
├── small.txt       # Example input: 2x3 and 3x2 matrices
└── large.txt       # Example input: two 10x10 matrices
```

---

## 🔧 Tech Stack

| Component | Technology |
|-----------|------------|
| Language | C |
| Threading | POSIX pthreads (`-pthread`) |
| Math | `math.h` (`-lm`) |
| Compiler | GCC |

---

## 🚀 How to Run

**1. Compile**
```bash
gcc -pthread -lm matrix.c -o matrix
```

**2. Run with an input file**
```bash
./matrix large.txt
```

---

## 📄 Input File Format

The input file contains two matrices written back to back. Each matrix starts with its dimensions followed by its values row by row.

```
<rows> <cols>
<values...>
<rows> <cols>
<values...>
```

**Example (small.txt) — 2x3 multiplied by 3x2:**
```
2 3
1 2 3
4 5 6
3 2
7 8
9 10
11 12
```

**Example output:**
```
A [2x3]:
   1 2 3
   4 5 6

B [3x2]:
    7  8
    9 10
   11 12

A x B = C [2x2]:
    58  64
   139 154
```

---

## ⚙️ How It Works

1. Two matrices are read from the input file into global arrays `matrix_a` and `matrix_b`
2. The program validates that the inner dimensions match (`col_a == row_b`)
3. One thread is spawned per cell in the output matrix (`row_a * col_b` threads total)
4. Each thread receives an `instruction` struct containing its target row, column, and inner dimension
5. The thread computes the dot product for its cell and writes the result to `matrix_c`
6. The main thread joins all worker threads before printing the final result

---

## 🧑‍💻 Author

**Sean Austin**
B.S. Applied Computing — Arizona State University
[LinkedIn](https://www.linkedin.com/in/sean-austin-7b3678283/) • [GitHub](https://github.com/ayplusplus)
