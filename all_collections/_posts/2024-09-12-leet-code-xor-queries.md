---
layout: post
title: LeetCode - 1310. XOR Queries of a Subarray
date: 2024-09-12 23:20:00
categories: [programming, algorithms, rust]
---

Dado o problema proposto é necessário entendermos o que é um **XOR** também conhecido como **ou exclusivo**
para que possamos atuar no problema.

o **XOR** é uma operação lógica sobre dois ou mais valores lógicos e que retorna um valor booleano como saída.
Um pouco do funcionamento do **XOR**:

| A     | B     | A XOR B |
| ----- | ----- | ------- |
| TRUE  | TRUE  | FALSE   |
| TRUE  | FALSE | TRUE    |
| FALSE | TRUE  | TRUE    |
| FALSE | FALSE | FALSE   |

E nesse problema em especifico iremos trabalhar com a manipulação de bits, então é de importância a utilização do mesmo.

### **O problema**

Dado dois `arr` onde um será um `arr` de inteiros positivos e o outro um `arr` de queries (consultas) onde as `queries[𝑖] = [left*𝑖*, right**𝑖**]`

Para cada query `𝑖` calcule o **XOR** dos elementos de `left𝑖` para `right𝑖`, isso é, `arr[left𝑖] XOR arr[left𝑖 + 1] XOR ... XOR arr[right𝑖]`;

retorne um array `resposta` onde `resposta[i]` é a resposta da `i-ésima` query;

*Exemplo:*
```rs
input = arr = [1,3,4,8], queries = [[0,1],[1,2],[0,3],[3,3]]
Output: [2, 7, 14, 8]
```

Explicação: A representação de elementos binários no array são:
1 = 0001
3 = 0011
4 = 0100
8 = 1000

O valor **XOR** para as queries são:
```rs
[0, 1] = 1 x 3 = 2
[1, 2] = 3 x 4 = 7
[0, 3] = 1 x 3 x 4 x 8 = 14
[3, 3] = 8
```
### A resolução

O código irá implementar uma função **(xor_queries)** onde ela irá receber como argumentos os nossos dois **arrays** e retornar um **array** de inteiros;

para isso precisamos primeiro fazer um pré-processamento do array `arr`, onde podemos utilizar a estratégia de um vetor auxiliar:
```rs
let mut xor = vec![0; arr.len() + 1];
```

Determinamos a criação de um vetor que será inicializado com o valor 0, o `arr.len() + 1` determina o tamanho do vetor e cria um vetor com um tamanho que é um a mais do que o tamanho do vetor original.

agora devemos seguir para as proximas etapas:

1. Pré-processamento do vetor:

Aqui temos um loop que itera sobre o intervalo de valores de 0 até o último elemento do array ou seja `arr.len() - 1`. percorrendo assim todos os indices do vetor.
```rs
for i in 0..arr.len() {
  xor[i + 1] = xor[i] ^ arr[i];
}
```
Dentro do loop, estamos acessando e modificando o vetor auxiliar `xor` onde `xor[i + 1]` é o próximo elemento no array `xor`;

Já considerando o outro lado da expressão, o `xor[i]` é o elemento atual no vetor `xor` que esta sendo acessado naquela iteração.

por fim `arr[i]` é o elemento atual no array `arr`, onde o operador `^` que é o nosso **XOR** compara os bits dos dois operandos e retorna 1 se os bits forem diferentes e 0 se forem iguais.

2. Processamento das queries:

Para cada query  calculamos o **XOR** do subarray correspondente usando o vetor `xor` já pré-processado na etapa anterior

```rs
let mut res = vec![];
for q in queries {
  res.push(xor[q[0] as usize] ^ xor[q[1] as usize + 1]);
}
```
Por fim temos um vetor auxiliar `res` que foi criado para que possamos inserir os nossos resultados das comparações **XOR** executadas entre os subarrays e necessitamos apenas retornar o array `res` e nossa solução está pronta.

### Conclusão

A função **xor_queries** tem uma complexidade de tempo O(n + m) e uma complexidade de espaço O(n), onde n é o tamanho do vetor arr e m é o número de queries.

Aqui vai nossa solução completa do problema:

```rs
struct Solution;

impl Solution {
  #[doc = "XOR Queries of a Subarray"]
  fn xor_queries(arr: Vec<i32>, queries: Vec<Vec<i32>>) -> Vec<i32> {
    let mut xor = vec![0; arr.len() + 1];
    for i in 0..arr.len() {
      xor[i + 1] = xor[i] ^ arr[i];
    }
    let mut res = vec![];
    for q in queries {
      res.push(xor[q[0] as usize] ^ xor[q[1] as usize + 1]);
    }
    res
  }
}
```

Obrigado!

[Home](/)


