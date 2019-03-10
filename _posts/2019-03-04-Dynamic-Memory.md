---
title: Лекция 15 - Динамична Памет
category: новини
tags:
  - лекции
---

[Линк към презентацията](https://docs.google.com/presentation/d/1VvRguN_czTS_mBs0-HyGxz9eMlAbL8YXepNy-fPmNhk/edit?usp=sharing)
{% include presentation id="2PACX-1vQtuvB_LPMTq9z5Ja_hYs3yS024HMyNbEkn9gw6XTYRWwQN3M55oMyPYEhLPBuDgc69eGzR7JjazJBI" %}

## Б клас
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
  int *int_arr = (int*)malloc(sizeof(int)*10);

  for(int i=0; i < 10; i++) {
    int_arr[i] = i + 1;
  }
  for(int i=0; i < 10; i++) {
    printf("%d\n", int_arr[i]);
  }

  //free(int_arr);
  return 0;
}
```

## Г клас
```c
#include <stdio.h>

void swap(int *left, int *right) {
  /*int tmp = arr[i];
  arr[i] = arr[j];
  arr[j] = tmp;
  */
  int tmp = *left;
  *left = *right;
  *right = tmp;
}

void sort_arr(int *arr, int count) {
  for(int i=0; i < count-1; i++) {
    for(int j=i+1; j < count; j++) {
      if(arr[i] > arr[j]) {
        swap(arr+i, arr+j);
      }
    }
  }
}

int main() {
  int arr[] = {5, 4, 8, 3, 9, 4, 6, 4, 7, 0};
  sort_arr(arr, 10);

  for(int i=0; i< 10; i++) {
    printf("%d ", arr[i]);
  }
  printf("\n");
  return 0;
}
```

```c
#include <stdio.h>
#include <string.h>

struct spell_t {
  char name[20];
  float casting_time;
  char description[200];
  int level;
};

struct spell_book_t {
  struct spell_t spells[10];
  int spell_count;
};

void print_spell(struct spell_t the_spell) {
  printf("Name: %s\n", the_spell.name);
  printf("Time: %f seconds\n", the_spell.casting_time);
  printf("Description: %s\n", the_spell.description);
  printf("Level: %d\n", the_spell.level);
}

void print_spell_list(struct spell_t spell_list[], int spell_count) {
  for(int i=0; i < spell_count; i++) {
    printf("Spell %d:\n", i+1);
    print_spell(spell_list[i]);
  }
}

void print_spell_book(struct spell_book_t book) {
  print_spell_list(book.spells, book.spell_count);
}

struct spell_t create_spell() {
  struct spell_t new_spell = {"Musaka", 1.5 * 60 * 60, "Ima kaima i kartofi. Vkusna e.", 10};

  return new_spell;
}

void change_cast_time(struct spell_t *the_spell) {
  the_spell->casting_time /= 2;
}

void add_spell_to_book(struct spell_book_t *book, struct spell_t spell) {
  book->spells[book->spell_count++] = spell;
}

int main() {
  /*struct spell_t first_spell;

  strcpy(first_spell.name, "Musaka");
  first_spell.casting_time = 1.5 * 60 * 60;
  strcpy(first_spell.description, "Ima kaima i kartofi. Vkusna e.");
  first_spell.level = 10;*/

   //spell_list[0] = first_spell;
  //spell_list[1] = create_spell();

  //  print_spell(first_spell);
//  print_spell(spell_list[0]);

  /*struct spell_t spell_list[5];
  for(int i=0; i < 5; i++) {
    spell_list[i] = create_spell();
  }
  change_cast_time(&spell_list[2]);
  print_spell_list(spell_list, 5);*/

  struct spell_book_t book;
  book.spell_count = 0;

  for(int i = 0; i < 5; i++) {
    add_spell_to_book(&book, create_spell());
  }

  change_cast_time(&(book.spells[2]));
  print_spell_book(book);

  return 0;
}
```
