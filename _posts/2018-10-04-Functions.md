---
title: Лекция 01 - Функции, масиви и рекурсия
date: 2018-10-04 09:30:00 +0300
category: новини
tags:
  - лекции
---

Качена е презентацията от лекцията за функции, масиви и рекурсия.

[Линк към презентацията](https://docs.google.com/presentation/d/1XofqAuzWZO5kdnfjE7UvkAWmT0GkgEIaKmbxrw4Ze7Q/edit?usp=sharing)

{% include presentation id="2PACX-1vR8nkuqli7Y2W0SXzvVtQN7fufO7evvkdeHNvHV6lzHXGOYLEGFNUtNNZCDfleNXQ2rtQ_d91EZLCow" %}

## Решения на задачите за функции

```c
#include <stdio.h>

// 1
int is_number_even_v1(int number) {
    printf("Called is_number_even_v1(%d)\n", number);
    if(number % 2 == 0) {
        return 1;
    } else {
        return 0;
    }
}

int is_number_even_v2(int number) {
    printf("Called is_number_even_v2(%d)\n", number);
    if(number % 2 == 0) {
        return 1;
    }

    return 0;
}

int is_number_even_v3(int number) {
    printf("Called is_number_even_v3(%d)\n", number);
    return number % 2 == 0;
}

// 2
int add_numbers(int n1, int n2) {
    printf("Called add_numbers(%d, %d)\n", n1, n2);
    return n1 + n2;
}

// 3
int multiply_numbers(int n1, int n2) {
    printf("Called multiply_numbers(%d, %d)\n", n1, n2);
    int result = 0;
    for(int i = 0; i < n2; i++) {
        result = add_numbers(result, n1);
    }
    return result;
}

// 4
int power_number(int number, int power) {
    printf("Called power_number(%d, %d)\n", number, power);
    int result = 1;
    for(int i = 0; i < power; i++) {
        result = multiply_numbers(result, number);
    }
    return result;
}

// 5
int square_number(int number) {
    printf("Called square_number(%d)\n", number);
    return power_number(number, 2);
}

// 6
int is_number_prime(int number) {
    printf("Called is_number_prime(%d)\n", number);
    for(int i = 2; i < number; i++) {
        if(number % i == 0) {
            return 0;
        }
    }
    return 1;
}

// 7
int fibonacci(int n) {
    printf("Called fibonacci(%d)\n", n);
    if(n <= 0) return 0;
    if(n == 1) return 1;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    printf("%d\n", is_number_even_v3(22)); // expected - 1
    printf("%d\n", is_number_even_v3(11)); // expected - 0

    printf("%d\n", add_numbers(5, 7)); // expected - 12
    printf("%d\n", add_numbers(7, 5)); // expected - 12

    printf("%d\n", multiply_numbers(5, 7)); // expected - 35
    printf("%d\n", multiply_numbers(7, 5)); // expected - 35

    printf("%d\n", power_number(5, 7)); // expected - 78125
    printf("%d\n", power_number(7, 5)); // expected - 16807

    printf("%d\n", square_number(5)); // expected - 25
    printf("%d\n", square_number(7)); // expected - 49

    printf("%d\n", is_number_prime(5)); // expected - 1
    printf("%d\n", is_number_prime(8)); // expected - 0

    printf("%d\n", fibonacci(0)); // expected - 0
    printf("%d\n", fibonacci(1)); // expected - 1
    printf("%d\n", fibonacci(2)); // expected - 1
    printf("%d\n", fibonacci(3)); // expected - 2
    printf("%d\n", fibonacci(4)); // expected - 3
    printf("%d\n", fibonacci(5)); // expected - 5
    printf("%d\n", fibonacci(6)); // expected - 8
    printf("%d\n", fibonacci(7)); // expected - 13

    return 0;
}
```
