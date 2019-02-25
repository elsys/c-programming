---
title: Лекция 07 - Структури
category: новини
tags:
  - лекции
---

[Линк към презентацията](https://docs.google.com/presentation/d/1HR6gxPx_eadOBan7gWBmcB0DGX6IjUPhOpWeSP2Vf9Y/edit?usp=sharing)
{% include presentation id="2PACX-1vTjpZH89d63cAQPO-mbtvwmSMwwXnxTETK9RaeH_kKjnxklvaFhkhb44JgCm1pioUqXpLxAPUiUnPuM" %}

## Решения на задачите за структури

## Б клас
```c
#include <stdio.h>

struct point_t {
  float y;
  float x;
};

// (a,b) (m,n) (x,y)
// (1,1) (2,2) (3,3)
// float a = point1.x;
// float b = point1.y;
// a(n−y)+m(y−b)+x(b−n) == 0
// 1(2-3) + 2(3-1) + 3(1-2) = -1 + 4 + -3 = 0

int are_on_line(struct point_t p1, struct point_t p2, struct point_t p3) {
  return (p1.x * (p2.y - p3.y) +
          p2.x * (p3.y - p1.y) +
          p3.x * (p1.y - p2.y)) == 0;
}

struct point_t add_points(struct point_t p1, struct point_t p2) {
  struct point_t result;

  result.x = p1.x + p2.x;
  result.y = p1.y + p2.y;

  return result;
}

int main() {
  struct point_t point1;
  point1.x = 1;
  point1.y = 1;
  struct point_t point2 = {2, 2};
  struct point_t point3 = {3,4};

  printf("%d\n", are_on_line(point1, point2, point3));

  struct point_t point4 = add_points(point1, point2);

  printf("point4=(%f,%f)\n", point4.x, point4.y);

  return 0;
}
```

## Г клас
```c
#include <stdio.h>

struct point_t {
  float y;
  float x;
};

// (1,1) (2,2) (3,3)
// (a,b) (m,n) (x,y)
// a(n−y)+m(y−b)+x(b−n)=0
int on_the_line(struct point_t point1, struct point_t point2, struct point_t point3){
  float a = point1.x;
  float b = point1.y;
  float m = point2.x;
  float n = point2.y;
  float x = point3.x;
  float y = point3.y;
  if(a*(n−y)+m*(y−b)+x*(b−n)=0){
      return 1;
  }
  else{
    return 0;
  }
}

int main() {
  struct point_t point1;
  point1.x = 5;
  point1.y = 13;
  struct point_t point2 = {10, 20};

  return 0;
}
```
