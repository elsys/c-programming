---
title: Лекция 16 - Упражнение върху динамична памет
category: новини
tags:
  - лекции
---


## Вектор

## В клас
```c
#include <stdio.h>
#include <stdlib.h>

#define INIT_CAPACITY 5

struct vector_t {
	int capacity;
	int size;
	int *data;
};

struct vector_t init();
void destroy(struct vector_t*);
void add(struct vector_t*, int);
void resize(struct vector_t*);
int get(struct vector_t, int);
void add_front(struct vector_t*, int);
void add_at(struct vector_t*, int, int);

int main() {

	struct vector_t v = init();

	add(&v, 1);
	add(&v, 2);
	add(&v, 3);
	add(&v, 4);
	add(&v, 5);
	add(&v, 6);
	add(&v, 7);

	printf("%d\n", get(v, 6));
	add(&v, 8);
	printf("%d\n", get(v, 7));
	add_front(&v, 10);
	printf("%d %d\n", get(v, 0), v.size);
	add_at(&v, 100, 11);
	printf("%d\n", v.size);
	add_at(&v, 0, 11);
	printf("%d %d\n", get(v, 0), v.size);

	destroy(&v);

	return 0;
}

struct vector_t init() {
	struct vector_t vector;
	vector.capacity = INIT_CAPACITY;
	vector.data = malloc(INIT_CAPACITY * sizeof(int));
	vector.size = 0;

	return vector;
}

void add(struct vector_t *vector, int elem) {
	add_at(vector, vector->size, elem);
}

void add_front(struct vector_t *vector, int elem) {
	add_at(vector, 0, elem);
}

void add_at(struct vector_t *vector, int position, int elem) {
	if (vector->data == NULL) {
		return;
	}

	if (vector->capacity == vector->size) {
		resize(vector);
	}

	if (position < 0 || position > vector->size) {
		return;
	}

	// this was wrong -> for (int i = position; i > 0; i--) {
	for (int i = vector->size; i > position; i--) {
		vector->data[i] = vector->data[i - 1];
	}

	vector->data[position] = elem;
	vector->size++;

}

int get(struct vector_t vector, int index) {
	if (index > vector.size || index < 0) {
		return -1;
	}

	return vector.data[index];
}

void resize(struct vector_t *vector) {
	int *tmp = vector->data;

	vector->capacity *= 2;
	vector->data = malloc(vector->capacity * sizeof(int));

	for (int i = 0; i < vector->size; i++) {
		vector->data[i] = tmp[i];
	}

	free(tmp);
}

void destroy(struct vector_t *vector) {
	free(vector->data);
	vector->data = NULL;

	vector->capacity = 0;
	vector->size = 0;
}
```

## Б клас

```c
#include <stdio.h>
#include <stdlib.h>

int POINT_COUNT = 100;

struct point_t {
  float x;
  float y;
  char c;
};

int main() {
  struct point_t *my_point =
(struct point_t*)malloc(sizeof(struct point_t) * POINT_COUNT);

  //printf("%d\n", sizeof(struct point_t));
  printf("(%.2f,%.2f)\n", my_point->x, my_point->y);
//  printf("(%.2f,%.2f)\n", my_point[1].x, my_point[1].y);

  for(int i=0; i < POINT_COUNT; i++) {
    printf("(%.2f,%.2f)\n", my_point[i].x, my_point[i].y);
 //printf("(%.2f,%.2f)\n", (my_point + i)->x, (my_point + i)->y);
  }

  return 0;
}
```
```c
#include <stdio.h>
#include <stdlib.h>

struct vector_t {
  int count;
  int *items;
};

void init(struct vector_t *vec) {
  printf("Init vector\n");
  vec->count = 0;
  vec->items = (int*)malloc(sizeof(int));
}

void resize(struct vector_t *vec, int new_size) {
  printf("Resize vector to %d\n", new_size);
vec->items = (int*)realloc(vec->items, new_size * sizeof(int));
}

void push(struct vector_t *vec, int item) {
  printf("Push item %d\n", item);
  resize(vec, vec->count + 1);
  vec->items[vec->count] = item;
  vec->count++;
}

int pop(struct vector_t *vec, int *item) {
  if(vec->count <= 0) {
    return 0;
  }

  *item = vec->items[--vec->count];
  resize(vec, vec->count);
  return 1;
}


int main() {
  struct vector_t my_vec;
  init(&my_vec);

  for(int i=0; i < 10; i++) {
    push(&my_vec, i*3);
  }

  int res;
  for(int i=0; i < 7; i++) {
    if(pop(&my_vec, &res)) {
      printf("Popped %d\n", res);
    } else {
      printf("Out of items!\n\n");
    }
  }

  /*printf("Popped %d\n", pop(&my_vec));
  printf("Popped %d\n", pop(&my_vec));
  printf("Popped %d\n", pop(&my_vec));
  printf("Popped %d\n", pop(&my_vec));*/

  return 0;
}
```
