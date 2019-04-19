---
title: Лекция 18 - Свързан списък
category: новини
tags:
  - лекции
---

[Линк към презентацията](https://www.youtube.com/watch?v=dQw4w9WgXcQ)
{% include presentation id="2PACX-1vQZ4C_qftOEKGfuVzN3Yca1YFl8MJniDb-Ydi6VY6EFQDUrno_4v_2wh-St9AXZPhgvulmhPrBEBaEB" %}

## A клас

```c
#include <stdio.h>
#include <stdlib.h>

struct node_t {
	int data;
	struct node_t *next;
};

struct list_t {
	struct node_t *head;
};

struct list_t init_list();
void destroy_list(struct list_t*);
int size(struct list_t);
int empty(struct list_t);
void insert(struct list_t *, int);

int main () {
	struct list_t list = init_list();

	printf("empty = %d\n", empty(list));
	printf("size = %d\n", size(list));
	insert(&list, 5);
	insert(&list, 7);

	printf("size = %d\n", size(list));
	insert(&list, 12);


	printf("%d %d %d\n", list.head->data,
						 list.head->next->data,
						 list.head->next->next->data);

	printf("size = %d\n", size(list));
	printf("empty = %d\n", empty(list));

	destroy_list(&list);

	printf("size = %d\n", size(list));
	printf("empty = %d\n", empty(list));
	return 0;
}

struct list_t init_list()  {
	struct list_t result;

	result.head = NULL;

	return result;
}

void insert(struct list_t *l, int value) {
	struct node_t *tmp = l->head;

	struct node_t *new_node = malloc(sizeof(struct node_t));

	new_node->data = value;
	new_node->next = NULL;

	if (!empty(*l)) {
		while(tmp->next != NULL) {
			tmp = tmp->next;
		}

		tmp->next = new_node;
	} else {
		l->head = new_node;
	}


}

int size(struct list_t l) {
	int result = 0;

	for(struct node_t *node = l.head;
		node != NULL;
		result++, node = node->next);

	return result;
}

int empty(struct list_t l) {
	return l.head == NULL;
}

void destroy_list(struct list_t *l) {
	struct node_t *tmp = l->head;

	while(tmp != NULL) {
		struct node_t *free_node = tmp;
		tmp = tmp->next;

		free(free_node);
	}

	l->head = NULL;
}
```

## Б клас
```c
#include <stdio.h>
#include <stdlib.h>

struct node_t {
  int value;
  struct node_t* next;
};
#define node_t struct node_t

struct list_t {
  node_t* head;
  unsigned int size;
};
#define list_t struct list_t

list_t* init_list() {
  list_t* new_list = (list_t*)malloc(sizeof(list_t));

  new_list->head = NULL;
  new_list->size = 0;

  return new_list;
}

void insert(list_t* list, int val) {
  node_t* new_node = (node_t*)malloc(sizeof(node_t));
  new_node->value = val;

  new_node->next = list->head;
  list->head = new_node;

  list->size++;
}

void remove_first(list_t* list) {
  node_t* tmp = list->head;
  list->head = list->head->next;
  free(tmp);
  list->size--;

  /*node_t* tmp = list->head->next;
  free(list->head);
  list->head = tmp;
  list->size--;*/
}


int main() {
  list_t* list = init_list();

  for(int i=1; i <= 5; i++) {
    insert(list, i);
  }

  remove_first(list);

  /*for(int i=0; i < list->size; i++) {
    printf("%s\n", list[i]);
  }*/

  for(node_t* node = list->head; node != NULL; node = node->next) {
    printf("%d\n", node->value);
  }

  return 0;
}
```

## В клас

```c
#include <stdio.h>
#include <stdlib.h>

struct node_t {
	int data;
	struct node_t *next;
};

struct list_t {
	struct node_t *head;
};

struct list_t init_list();
void destroy_list(struct list_t*);
void destroy_list_r(struct node_t*);
void insert(struct list_t*, int);

int main() {
	struct list_t l = init_list();

	insert(&l, 5);
	insert(&l, 7);
	insert(&l, 12);

	destroy_list_r(l.head);

	return 0;
}

struct list_t init_list() {
	struct list_t result;

	result.head = NULL;

	return result;
}

void insert(struct list_t *l, int value) {
	struct node_t *new_node = malloc(sizeof(struct node_t));
	new_node->data = value;
	new_node->next = NULL;

	struct node_t *tmp = l->head;
	if (tmp == NULL) {
		l->head = new_node;
		return;
	}

	while(tmp->next != NULL) {
		tmp = tmp->next;
	}

	tmp->next = new_node;
}

void destroy_list(struct list_t *list) {
	struct node_t *tmp = list->head;

	while (tmp != NULL) {
		struct node_t *node = tmp;

		tmp = tmp->next;
		free(node);		
	}

	// WE FORGOT
	list->head = NULL;
}

void destroy_list_r(struct list_t *l) {
	destroy_nodes_r(l->head);

	l->head = NULL;
}
void destroy_nodes_r(struct node_t *node) {
	if (node == NULL) {
		return;
	}
	printf("BEFORE %d\n", node->data);
	destroy_nodes_r(node->next);
	printf("AFTER %d\n", node->data);
	free(node);
}
```

## Г клас
```c
#include <stdio.h>
#include <string.h>

void swap(int *a, int *b) {
  int tmp = *a;
  *a = *b;
  *b = tmp;
}
/*
void swap(int a, int b) {
  int tmp = a;
  a = b;
  b = tmp;
}

void swap(int *a, int *b) {
  int *tmp = a;
  a = b;
  b = tmp;
}
*/
int main() {
  /*int val = 13;
  int val2 = 26;
  int *p_val;
//  int *p_val = &val;

  p_val = &val;
  *p_val = 17;
  val = 23;

  p_val = &val2;

  printf("%d %d\n", val, *p_val);

  swap(&val, &val2);
  printf("%d %d\n", val, val2);


  int arr[10];
  int *p_arr = arr;

  printf("%p %p %d %p %p %p %p %p\n", arr, &arr, arr[0], &arr[0], &arr[1], arr + 1, p_arr, p_arr + 1);

  for(int i=0; i< 10; i++) {
    int *p = arr + i;
    printf("%d %p %d %p %d\n", arr[i], (arr+i), *(arr+i), p, *p);
  }


  char str[200];
  fgets(str, 200, stdin);
  char word[10];
  char *str2 = str;
  while(strlen(str2) > 0) {
    if(str2[0] == ' ') {
      str2++;
    } else {
      int i=0;
      while(str2[i] != ' ' && str2[i] != '\0') {
        word[i] = str2[i];
        i++;
      }
      str2 = str2 + i;
      word[i] = '\0';
      printf("%s\n", word);
    }
    printf("str2: %s\n", str2);
  }*/

  long long int a = 1528752;
  int b = (int)a;
  int c = *((int*)(&a) + 1);

  printf("%p %p %p %p\n", &a, (char*)(&a), (&a) + 1, (char*)(&a) + 1);
  printf("%d %d %d\n", a, b, c);



  return 0;
}
```
