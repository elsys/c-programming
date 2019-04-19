---
title: Лекция 20 - Двусвързан списък
category: новини
tags:
  - лекции
---

## A клас

```c
#include <stdio.h>
#include <stdlib.h>

struct node_t {
  int value;
  struct node_t* next;
  struct node_t* prev;
};

struct list_t {
  struct node_t* head;
  unsigned int size;
};

struct list_t init_list() {
  struct list_t list;

  list.head = NULL;
  list.size = 0;

  return list;
}

void insert(struct list_t* list, int value) {
  // list->head = new node
  // new node->next = head
  // head->prev = new node

  // new node->prev = NULL
  struct node_t* new_node = malloc(sizeof(struct node_t));
  new_node->value = value;
  new_node->prev = NULL;

  /*struct node_t* old_head = list->head;
  list->head = new_node;
  new_node->next = old_head;
  old_head->prev = new_node;*/

  new_node->next = list->head;
  if(list->head != NULL)
    list->head->prev = new_node;
  list->head = new_node;

  list->size++;
}

void remove_first(struct list_t* list) {
  // head->next->prev = NULL
  // head = head->next
  // free head
  // size--

  struct node_t* old_head = list->head;
  list->head = list->head->next;
  if(list->head != NULL)
    list->head->prev = NULL;

  /*if(list->head->next != NULL)
    list->head->next->prev = NULL;
  list->head = list->head->next;*/

  free(old_head);
  list->size--;
}

int main() {
  struct list_t my_list = init_list();

  insert(&my_list, 15);
  remove_first(&my_list);
  printf("%d\n", my_list.size);
  return 0;
}
```

## Б клас
```c
// Author: Mario Benov
// License: GPL

#include <stdio.h>
#include <stdlib.h>

struct node_t {
  int value;
  struct node_t* next;
  struct node_t* prev;
};
#define node_t struct node_t

struct list_t {
  node_t* head;
  node_t* tail;
  unsigned int size;
};
#define list_t struct list_t

list_t* init_list() {
  list_t* new_list = (list_t*)malloc(sizeof(list_t));

  new_list->head = NULL;
  new_list->tail = NULL;
  new_list->size = 0;

  return new_list;
}

void insert(list_t* list, int val) {
  node_t* new_node = (node_t*)malloc(sizeof(node_t));
  new_node->value = val;

  new_node->next = list->head;
  if(list->head != NULL) {
    list->head->prev = new_node;
  } else {
    list->tail = new_node;
  }
  list->head = new_node;
  //new_node->next->prev = new_node;

  list->size++;
}

void remove_first(list_t* list) {
  node_t* tmp = list->head;
  list->head = list->head->next;
  if(tmp->next != NULL) {
    tmp->next->prev = NULL;
  } else {
    list->tail = NULL;
  }
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

  for(node_t* node = list->head; node != NULL; node = node->next) {
    printf("%d\n", node->value);
  }
  /*node_t* node = list->head;
  for(int i=0; i< list->size; i++, node = node->next) {
    printf("%d - %d\n", i, node->value);
  }*/

  for(node_t* node = list->tail; node != NULL; node = node->prev) {
    printf("%d\n", node->value);
  }

  while(list->head != NULL) {
    remove_first(list);
  }
  free(list);

  /*insert(my_list, 15);
  printf("%d\n", my_list->size);

  remove_first(my_list);
  printf("%d\n", my_list->size);*/
  //free(my_list);
  return 0;
}
```
