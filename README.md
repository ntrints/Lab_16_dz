# Lab_16_dz
Домашняя работа к лабораторной работе №16

# Условия задачи
Массив d0, d1, d2, ..., dh из элементов массивов а0, а1, а2, ..., an, b0, b1, b2 ..., bn, с0, с1,с2, ..., сn расположенные до последнего отрицательного элемента, в обратном порядке.

# Блоксхема
<img width="608" height="1891" alt="image" src="https://github.com/user-attachments/assets/299cd931-e5dc-48be-b95d-ec921167ac68" />

# Реализация программы
```
#define _CRT_SECURE_NO_WARNINGS
#define _USE_MATH_DEFINES
#include <locale.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h> 
#include <conio.h>
#include <math.h>
  
double* full_elements(double* ptr_array, int n) {
    for (int i = 0; i < n; i++) {
        double r = (double)rand() / RAND_MAX;
        ptr_array[i] = r * 2.0 - 1.0;
    }
    return ptr_array;
}
int put_elements(double* ptr_array, int size) {
    for (int i = 0; i < size; i++) {
        printf("%.6lf ", ptr_array[i]);
    }
    printf("\n");
    return 0;
}
double* build_d(double* a, int size_a, double* b, int size_b, double* c, int size_c, int* size_d) {
    int last_neg_index_a = -1, last_neg_index_b = -1, last_neg_index_c = -1;
    for (int i = 0; i < size_a; i++) if (a[i] < 0) last_neg_index_a = i;
    for (int i = 0; i < size_b; i++) if (b[i] < 0) last_neg_index_b = i;
    for (int i = 0; i < size_c; i++) if (c[i] < 0) last_neg_index_c = i;
    if (last_neg_index_a == -1) last_neg_index_a = size_a - 1;
    if (last_neg_index_b == -1) last_neg_index_b = size_b - 1;
    if (last_neg_index_c == -1) last_neg_index_c = size_c - 1;

    *size_d = (last_neg_index_a + 1) + (last_neg_index_b + 1) + (last_neg_index_c + 1);
    double* d = (double*)malloc((*size_d) * sizeof(double));
    if (!d) return NULL;

    int idx = 0;
    for (int i = last_neg_index_a; i >= 0; i--) d[idx++] = a[i];
    for (int i = last_neg_index_b; i >= 0; i--) d[idx++] = b[i];
    for (int i = last_neg_index_c; i >= 0; i--) d[idx++] = c[i];
    return d;
}
int main() {
    setlocale(LC_ALL, "RUS");
    srand(time(NULL));
    int size_a = rand() % 41 + 10;
    int size_b = rand() % 41 + 10;
    int size_c = rand() % 41 + 10;
    double* a = (double*)malloc(size_a * sizeof(double));
    double* b = (double*)malloc(size_b * sizeof(double));
    double* c = (double*)malloc(size_c * sizeof(double));
    if (!a || !b || !c) {
        puts("Ошибка выделения памяти");
        return -1;
    }
    full_elements(a, size_a);
    full_elements(b, size_b);
    full_elements(c, size_c);
    printf("Массив A (size=%d):\n", size_a);
    put_elements(a, size_a);
    printf("\nМассив B (size=%d):\n", size_b);
    put_elements(b, size_b);
    printf("\nМассив C (size=%d):\n", size_c);
    put_elements(c, size_c);
    int size_d;
    double* d = build_d(a, size_a, b, size_b, c, size_c, &size_d);
    if (!d) {
        free(a); free(b); free(c);
        puts("Ошибка выделения памяти для массива D");
        return -1;
    }
    printf("\nМассив D (до последнего отрицательного элемента всех массивов, в обратном порядке):\n");
    put_elements(d, size_d);

    free(a);
    free(b);
    free(c);
    free(d);

    return 0;
}
```
<img width="1033" height="329" alt="image" src="https://github.com/user-attachments/assets/9d72ceab-11f0-468d-811a-176f7e67b481" />
