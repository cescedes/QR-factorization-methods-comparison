# Gram-Schmidt vs. modified Gram-Schmidt vs. Householder-based QR factorization vs. Givens-based QR factorization
## Summary
The code implements and tests four QR factorization methods: Classical GramSchmidt, Modified Gram-Schmidt, Householder, and Givens rotations which can
be executed and reproduced within the Jupyter Notebook. For each method, the
program measures runtime and orthogonality accuracy using random matrices
of two sets:
- Set A: Matrices of varying row count m with a fixed column count of 100.
- Set B: Matrices with a fixed row count of 3000 and varying column count n.
  
For each matrix size in Sets A and B, the algorithm tests each QR method, skipping any method that previously exceeded the 45-second runtime limit or encountered errors. For each tested size, the runtime and orthogonality error
are displayed.

## Visualization for Set A
<img src="https://github.com/user-attachments/assets/c15e4e7d-e8e6-47a1-8de0-948bd6c16691" width="600"> 

## Visualization for Set B
<img src="https://github.com/user-attachments/assets/e4788cff-83fc-4e01-89f3-779b19e89537" width="600">

### Accuracy
Accuracy is computed with the orthogonality metric $||Q^T Q - I_n||_1$ for each algorithm, which evaluates how close Q is to being orthogonal.

### Performance
Classical and Modified Gram-Schmidt perform significantly faster than Householder and Givens for smaller matrix dimensions. However, their speed advantage diminishes as matrix dimensions grow, with both methods eventually facing time limits. 
Givens rotations method is the most computationally intensive and begin to exceed time limits as matrix size increases, particularly for Set B (wider matrices). 
Givens' application is thus limited for large-scale problems.

### Efficency
The hardware runs on the processor 12th Gen Intel(R) Core(TM) i7-1260P (2.10 GHz). Assuming 4 FLOPS per cycle for double-precision operations and using base clock frequency; the theoretical performance is calculated as: 

$P_{theoretical} = Number of Cores \times Clock Speed (GHz) \times FLOPs per Cycle$

$P_{theoretical} = 12cores \times 2.10GHz \times 4FLOPS per cycle = 100.8 GFLOPS$

## Conclusion

- **Classical and Modified Gram-Schmidt:** Suitable for small to medium-sized matrices where computational speed is prioritized over orthogonal precision. Their large orthogonality errors make them less reliable for precision-sensitive applications.
- **Householder Transformations:** Ideal for cases needing high orthogonality with moderate matrix sizes. It provides the best trade-off between accuracy and efficiency.
- **Givens Rotations:** Recommended for very high-precision requirements in small matrices. Due to its poor scalability, Givens rotations method is unsuitable for large matrices but is excellent in precision-critical scenarios on smaller scales.

