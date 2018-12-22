---
title: Лекция 11 - Побитови Операции
category: новини
tags:
  - лекции
---

[Линк към презентацията](https://docs.google.com/presentation/d/1ij1HkFU2_bQ27GWmjIPhqjcpW1ncPwpKWun95uhi4dE/edit?usp=sharing)
{% include presentation id="2PACX-1vTaGIE_hbQwQCFjb85eKiZSCmMw-Hz3Sc-94z-MU1VEgkeVnxJh9rJa8TYVzrg5YK-ZMTIZ04nQSdZw" %}


## Решения на задачите за побитови операции

## Б клас
```c
#include <stdio.h>

void print_bits(int n) {
  if(n > 0){
    print_bits(n >> 1);
    printf("%d", n % 2);
  }
}

int main() {
  print_bits(13);
  return 0;
}

```

## Г клас
```c
#include <stdio.h>

void print_bits(int n) {
  int res = 0;
  while(n > 0) {
    //res += n % 2;
    res = res + (n % 2);
    n = n >> 1;
    //n = n / 2;
    if(n > 0) {
      res *= 10;
    }
  }
  while(res > 0) {
    printf("%d", res % 10);
    res /= 10;
  }
  printf("\n");
}


int main() {
  print_bits(13); // 1101
  return 0;
}

```
