---
layout: post
title: LeetCode - 884. Uncommon Words from Two Sentences
date: 2024-09-16 23:20:00
categories: [programming, algorithms, rust, python]
---



## Introdução

O problema "884. Uncommon Words from Two Sentences" aborda um desafio de programação que exige o manuseio de strings e a detecçăo de palavras incomuns entre duas frases.

Sabida duas frases `A` e `B`, nosso propósito é selecionar todas as palavras que aparecem exatamente uma vez em uma das frases e não aparecem na outra. 

Para resolver este problema, necessitamos de:
1. Dividir cada sentença em palavras individuais, ou seja, transformar a sentença em um vetor.
2. Contar a frequência de cada palavra em ambas as sentenças.
3. Identificar as palavras que aparecem exatamente uma vez em uma das sentenças e não aparecem na outra.

Este problema testa a habilidade de trabalhar com strings, utilizar estruturas de dados como dicionários para contagem de frequências e aplicar lógica para filtrar os resultados desejados.

### Exemplo

Considere as sentenças:
- A: "this apple is sweet"
- B: "this apple is sour"

As palavras incomuns seriam ["sweet", "sour"] porque "sweet" aparece apenas na sentença A e "sour" aparece apenas na sentença B.

Este problema é uma excelente oportunidade para praticar manipulação de strings e uso de dicionários em Python.


Neste caso, iremos iniciar com uma função simples `uncommonFromSetences` que recebe como argumento duas strings e retorna um vetor de strings.
Usaremos Python para resolver esse problema de forma simplificada, vamos por etapas:

1. Dividir a string em uma lista de palavras.

`uncommon_words.py`
```py
from typing import List

def uncommonFromSetences(s1: str, s2: str) -> List[str]:
    s1 = s1.split()
    s2 = s2.split()
```
nesta etapa usamos os argumentos `s1`e `s2` e dividimos as strings em uma lista de palavras.

2. Criar um dicionário para armazenar a contagem das palvras.

```py
d = {}
```

3. Iterar sobre cada palavra em cada uma de nossas listas `s1` e `s2`, verificando se a palavra já existir em nosso dicionário, iremos incrementar a contagem, caso não, adicionaremos a palavra com a contagem 1:

```py

for word in s1:
  if word in d:
    d[word] += 1
  else:
    d[word] = 1
```

Devemos repetir o mesmo processo para a `s2` e por fim retornar o vetor com as palavras que não são comuns.
4. Retornar o vetor de palavras incomuns.

```py

return [word for word in d if d[word] == 1]
```

Com isso finalizamos nosso código que soluciona o problema proposto.
Segue abaixo o código completo:

```py
from typing import List

def uncommonFromSetences(s1: str, s2: str) -> List[str]:
    s1 = s1.split()
    s2 = s2.split()
    d = {}
    for word in s1:
        if word in d:
            d[word] += 1
        else:
            d[word] = 1
    for word in s2:
        if word in d:
            d[word] += 1
        else:
            d[word] = 1
    return [word for word in d if d[word] == 1]
```

Com isso nosso problema está solucionado!

Aqui vai também a versão de rust do nosso problema, onde seguimos a mesma lógica de usar um hashmap:

```rs
fn uncommon_from_setences(s1: String, s2: String) -> Vec<String> {
    use std::collections::HashMap;
    let mut map = HashMap::new();
    for word in s1.split_whitespace() {
        *map.entry(word).or_insert(0) += 1;
    }
    for word in s2.split_whitespace() {
        *map.entry(word).or_insert(0) += 1;
    }
    map.into_iter().filter(|&(_, word)| word == 1).map(|(word, _)| word.to_string()).collect()
}
```

A base de explicação, fazemos a mesma coisa que no código python, porém usamos mecanismos para desreferenciar os valores mutáveis, assim obtendo o valor em si, permitindo que possamos incrementar diretamente o valor.

```rs
// desreferencia valores retornados pelo o metodo entry do hashmap.
*map.entry(word).or_insert(0) += 1; // entry retorna uma referência mutável &mut V
```

No final retornamos nosso vetor com as palavras que dão match no valor 1.

Por hoje é só, obrigado pessoal! :)

[Home](/)