---
title: Лекция 19 - Решения на задачи от контролно
category: новини
tags:
  - лекции
---


## Б клас

```c
#include <stdio.h>
#include <string.h>

int is_letter(char c) {
  if((c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z')) return 1;
  return 0;
}

int main () {
  char str[250];
//  gets(str);
  fgets(str, 250, stdin);

  int counter = 0, longest = 0;

  //for(int i=0; i < strlen(str); i++) {
  //int length = strlen(str);
  //for(int i=0; i < length; i++) {
  for(int i=0; str[i] != '\0'; i++) {
    if(str[i] >= 'A' && str[i] <= 'Z') {
      counter = 0;
      /*for(;is_letter(str[i++]);) {
        counter++;
      }
      i--;
      */
      int j = i;
      for(; is_letter(str[j]); j++) {
        counter++;
      }
      i = j;
      if(longest < counter) longest = counter;
    }
  }
  printf("Longest is %d\n", longest);
  return 0;
}

```
```c
#include <stdio.h>
#include <string.h>

int is_letter(char c) {
  if((c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z')) return 1;
  return 0;
}

int main () {
  char str[250];
  fgets(str, 250, stdin);

  int counter = 0, longest = 0;
  int is_in_word = 0;

  for(int i=0; str[i] != '\0'; i++) {
    if(str[i] >= 'A' && str[i] <= 'Z') {
      is_in_word = 1;
    }

    if(is_in_word && is_letter(str[i])) {
      counter++;
    } else {
      is_in_word = 0;
      if(longest < counter) longest = counter;
      counter = 0;
    }
  }
  printf("Longest is %d\n", longest);
  return 0;
}

```
```c
#include <stdio.h>

struct drone_t {
  char model[100];
  int capacity;
  int curr_load;
};

void load_drones(struct drone_t *main, struct drone_t *backup, int load) {
  if(main->capacity < main->curr_load + load) {
    int overload = main->curr_load + load - main-> capacity;
    if(backup->capacity < backup->curr_load + overload) {
      printf("Cannot load %d\n", backup->curr_load + overload - backup->capacity);
      backup->curr_load = backup->capacity;
    } else {
      backup->curr_load += overload;
    }
    main->curr_load = main->capacity;
  } else {
    main->curr_load += load;
  }
}

int main() {
  struct drone_t drones[6];

  for(int i=0; i < 6; i++) {
    drones[i].capacity = i * 10;
    drones[i].curr_load = 0;
  }

  for(int i=0; i < 5; i++) {
    load_drones(&drones[i], drones + i + 1, (i+1)*20);
  }

  for(int i=0; i < 6; i++) {
    printf("Drone %d is loaded with %d(%d)\n", i, drones[i].curr_load, drones[i].capacity);
  }
  return 0;
}

```
```c
#include <stdio.h>
#include <stdlib.h>

struct particle_t {
  float x;
  float w;
  char type;
};

void move_particles(struct particle_t *first, struct particle_t *second) {
  float r = first->x - second->x;
  float F = (first->w * second->w) / (r*r);

  first->x += (r > 0 ? -1 : 1) * (F/first->w);

  if(r < 0) {
    second->x += F/second->w;
  } else {
    second->x -= F/second->w;
  }
  printf("Moved first to %.2f, second to %.2f\n", first->x, second->x);
}

int main(int argc, char** argv) {
  int P = atoi(argv[1]);
  int T = atoi(argv[2]);

  struct particle_t *particles = (struct particle_t*)malloc(sizeof(struct particle_t) * P);

  for(int i = 0; i < P; i++) {
    particles[i].x = (i+1)*3;
    particles[i].w = (i+1)*17;
  }

  for(int i=0; i < T; i++) {
    for(int j=0; j < P - 1; j++) {
      for(int k = j+1; k < P; k++) {
        move_particles(particles+j, particles+k);
      }
    }
  }
  return 0;
}

```

## Г клас

```c
#include <stdio.h>
#include <string.h>

int is_letter(char c) {
  if((c >= 'A' && c <= 'Z') || (c >= 'a' && c <= 'z')) return 1;
  return 0;
}

int main() {
  char str[250];
  //gets(str);
  fgets(str, 250, stdin);

  int counter = 0, longest = 0;
  int str_length = strlen(str);

  for(int i=0; i < str_length; i++) {
    if(str[i] >= 'A' && str[i] <= 'Z') {
      int j = i;
      for(;is_letter(str[j]);j++) {
        counter++;
      }
      //i += counter;
      i = j;
      if(counter > longest) longest = counter;
      counter = 0;
    }
  }
  printf("Longest was %d\n", longest);
  return 0;
}

```
```c
#include <stdio.h>
#include <string.h>

int is_letter(char c) {
  if((c >= 'A' && c <= 'Z') || (c >= 'a' && c <= 'z')) return 1;
  return 0;
}

int main() {
  char str[250];
  fgets(str, 250, stdin);

  int counter = 0, longest = 0;
  int str_length = strlen(str);
  int is_in_word = 0;

  for(int i=0; i < str_length; i++) {
    if(str[i] >= 'A' && str[i] <= 'Z') {
      is_in_word = 1;
    }

    if(is_in_word && is_letter(str[i])) {
      counter++;
    } else {
      if(counter > longest) longest = counter;
      counter = 0;
      is_in_word = 0;
    }
  }
  printf("Longest was %d\n", longest);
  return 0;
}

```
```c
#include <stdio.h>
#include <string.h>

struct flower_t {
  int age;
  int is_pollinated;
  char species[100];
};

int main() {
  struct flower_t flowers[10];
  for(int i=0; i< 10; i++) {
    flowers[i].is_pollinated = i % 2 == 0;
    strcpy(flowers[i].species, "f1");
    /*switch(i%3) {
      case 0: strcpy(flowers[i].species, "f1"); break;
      case 1: strcpy(flowers[i].species, "f2"); break;
      case 2: strcpy(flowers[i].species, "f3"); break;
    }*/
  }

  for(int i=0; i< 10; i++)  {
    printf("%d: %s, %d\n", i, flowers[i].species, flowers[i].is_pollinated);
  }

  for(int i = 0; i < 5; i++) {
    struct flower_t left = flowers[i];
    struct flower_t mid = flowers[i+1];
    struct flower_t right = flowers[i+2];

    if(!left.is_pollinated && strcmp(left.species, mid.species) == 0) {
      flowers[i].is_pollinated = 1;
    }

    if(!right.is_pollinated && strcmp(right.species, mid.species) == 0) {
      flowers[i+2].is_pollinated = 1;
    }
  }

  for(int i=0; i< 10; i++)  {
    printf("%d: %s, %d\n", i, flowers[i].species, flowers[i].is_pollinated);
  }

  return 0;
}

```
```c
#include <stdio.h>

struct drone_t {
  char model[20];
  unsigned int capacity;
  unsigned int load;
};

void load_drones(struct drone_t *main, struct drone_t *backup, int load) {
  int overload = (load+main->load) -main->capacity;
  if(overload > 0) {
    main->load = main->capacity;
    int overload2 = (overload + backup->load) - backup->capacity;
    if(overload2 > 0) {
      backup->load = backup->capacity;
      printf("%d could not be loaded\n", overload2);
    } else {
      backup->load += overload;
    }
  } else {
    main->load += load;
  }
}

int main() {
  struct drone_t drones[10];
  for(int i=0; i< 10; i++) {
    drones[i].capacity = (i+1) * 10;
    drones[i].load = 0;
  }

  for(int i=0; i< 5; i++) {
    load_drones(&drones[i], drones + i + 1, 50);
  }

  for(int i=0; i< 10; i++) {
    printf("%d: %d/%d\n", i, drones[i].load, drones[i].capacity);
  }
  return 0;
}

```
