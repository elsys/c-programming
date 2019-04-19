---
title: Лекция 17 - Упражнение върху динамична памет, Стек
category: новини
tags:
  - лекции
---


## Б клас

```c
#include <stdio.h>
#include <stdlib.h>

//#define _DEBUG_

struct stack_t {
  int *items;
  int count;
};

void init(struct stack_t *the_stack);
void push(struct stack_t *the_stack, int item);
int pop(struct stack_t *the_stack, int *popped_item);
void destroy_stack(struct stack_t *the_stack);

void init(struct stack_t *the_stack) {
  #ifdef _DEBUG_
  printf("Init the stack!\n");
  #endif
  the_stack->count = 0;
  the_stack->items = NULL;
}

void push(struct stack_t *the_stack, int item) {
  #ifdef _DEBUG_
  printf("Push %d in the stack\n", item);
  #endif
  the_stack->items = (int*)realloc(the_stack->items,
    sizeof(int)*(++the_stack->count));
  the_stack->items[the_stack->count - 1] = item;
}

int pop(struct stack_t *the_stack, int *popped_item) {
  if(the_stack->count <= 0) {
    // return (int)NULL;
    return 0;
  }

  // int popped_item = the_stack->items[--the_stack->count];
  *popped_item = the_stack->items[--the_stack->count];
  the_stack->items = (int*)realloc(the_stack->items,
    sizeof(int)*(the_stack->count));

  #ifdef _DEBUG_
  printf("Pop %d from the stack\n", popped_item);
  #endif

  // return popped_item;
  return 1;
}

void destroy_stack(struct stack_t *the_stack) {
  #ifdef _DEBUG_
  printf("DESTROY THE STACK(not really)\n");
  #endif
  free(the_stack->items);
  // do not free the stack
  //free(the_stack);
}

int main() {
  struct stack_t steck;
  init(&steck);

  push(&steck, 15);
  push(&steck, 645);
  push(&steck, -1);

  int count = steck.count;
  int popped_item;
  for(int i = 0; i < 10 && pop(&steck, &popped_item); i++) {
    //int popped_item;
    //pop(&steck, &popped_item);
    //printf("%d (count=%d i=%d)\n", pop(&steck), steck.count, i);
    printf("%d (count=%d i=%d)\n", popped_item, steck.count, i);
  }

  destroy_stack(&steck);

  return 0;
}
```
