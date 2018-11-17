---
title: Лекция 06 - Решаване на задачите от контролното
category: новини
tags:
  - лекции
---

### Решения и насоки за задачите от контролното

## A клас
```c
#include <stdio.h>

int find_biggest_digit_score(unsigned int);

int main(){

	printf("%d", find_biggest_digit_score(538624263));

	return 0;
}

int find_biggest_digit_score(unsigned int number) {
	int max = number % 10;
	
	while(number > 0) {
		int digit = number % 10;
		
		if (digit > max) {
			max = digit;
		}
		
		number = number / 10;
	}
	
	return max;
}
```

```c
#include <stdio.h>

int find_smallest_diff(int[]);
int abs_diff(int, int);

int main() {

	int arr[] = { 5, 7, 3, 4, 1, 6, 8, 10, 2, 9 };
	
	printf("%d\n", find_smallest_diff(arr));

	return 0;
}


int find_smallest_diff(int arr[10]) {
	int min = abs_diff(arr[0], arr[1]);
	
	for (int i = 0; i < 10; i++) {
		for (int j = 0; j < 10; j++) {
			if (i == j) continue;
			//if (i != j) {
				
			//}

			int diff = abs_diff(arr[i], arr[j]);
			
			if (diff < min) {
				min = diff;
			}
			
		}
	}

	return min;
}

int abs_diff(int a, int b) {
	if (b > a) {
		return b - a;
	}
	
	return a - b;
}
```
```c
#include <stdio.h>

void convert_to_mocking_case(char *);

int main(int argc, char **argv) {

	for (int i = 1; i < argc; i++) {
		convert_to_mocking_case(argv[i]);	
	}

	return 0;
}

void convert_to_mocking_case(char *str) {
		
}
```
## В клас
```c
#include <stdio.h>

int find_even_digit(unsigned long);

int main() {
	
	printf("%d\n", find_even_digit(1573775));
	printf("%d\n", find_even_digit(0));
	printf("%d\n", find_even_digit(12213538));
	
	return 0;
}

int find_even_digit(unsigned long number) {
	
	while (number != 0) {
		int digit = number % 10;
		
		if (digit % 2 == 0) {
			return 1;
		}
		
		number = number / 10;
	}
	
	return 0;

}
```

```c
#include <stdio.h>

int multiply_by_biggest(int[]);

int main() {

	int arr[] = { 5, 7, 3, 4, 1, 5, 8, 10, 2, 9 };
	
	printf("\n%d\n", multiply_by_biggest(arr));

	return 0;
}

int multiply_by_biggest(int arr[10]) {
	int max = arr[0];
	
	for (int i = 0; i < 10; i++) {
		if (arr[i] > max) {
			max = arr[i];
		}
	}
	
	for (int i = 0; i < 10; i++) {
		printf("%d ", arr[i] * max);
	}

	return max;
}


```
```c
#include <stdio.h>

int count_vowels(char*);
int count_consonants(char*);

int main(int argc, char **argv) {

	printf("%d\n", count_vowels(argv[1]));
	printf("%d\n", count_consonants(argv[1]));
	return 0;
}

int count_vowels(char *str) {
	int count = 0;
	for (int i = 0; str[i] != '\0'; i++) {
		if (str[i] == 'a' ||
			str[i] == 'o' ||
			str[i] == 'i' ||
			str[i] == 'u' ||
			str[i] == 'e') {
			count++;
		}
		
		if (str[i] == 'A' ||
			str[i] == 'O' ||
			str[i] == 'I' ||
			str[i] == 'U' ||
			str[i] == 'E') {
			count++;
		}
	}
	
	return count;
}

int count_consonants(char *str) {
	
}
```
