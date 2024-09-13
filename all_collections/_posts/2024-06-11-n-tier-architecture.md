---
layout: post
title: System Design 101 - N-tier Architecture
date: 2024-06-05 10:18:00
categories: [architecture, system design]
---

[Home](/)

Antes mesmo de pensarmos em começar a desenvolver aplicações ou governanças para provisionar e gerenciar ambientes com foco em agilidade e com foco no negócio, arquitetos de solução acabam trabalhando em inúmeras opções para desenvolver architecture designs que atendam as necessidades de negócio.

Existem muitos meios de desenvolver uma solução, onde devemos sempre conseguir as informações certas baseadas em necessidades (requisitos) de usuários (clientes), considerando custos, performance, escalabilidade e disponibilidade da soluções disponibilizadas.

Aqui vamos entender sobre as vantagens de várias arquiteturas diferentes e também olhar para algumas demonstrações de quando utiliza-las.

A primeira arquitetura que iremos nos aprofundar é a **Arquitetura multicamada** que também pode ser chamada de n-tier layered architecutre. Essa abordagem em camadas apoia o desenvolvimento incremental de sistemas, onde, a medida que uma camada é desenvolvida, alguns dos serviços fornecidos por ela podem ser disponibilizados aos usuários ou desenvolvedores.

Nesse tipo de arquitetura é importante utilizarmos princípios de design loosely coupled¹ e também devemos nos atentar a atributos de escalabilidade² e elasticidade³. Uma arquitetura multicamada provê flexibilidade para adicionar novas funcionalidades em cada camada sem perturbar as outras camadas.
Em termos de segurança, nós podemos deixar cada camada isolada das outras, ou seja, caso uma camada for comprometida as outras camadas não serão impactadas. Isso acaba nos trazendo benefícios, onde podemos fazer troubleshootings e gerenciamentos de incidentes de uma forma mais rápida, identificando assim os problemas e de qual camada eles vem.

A arquitetura mais comum em multicamadas é a three-tier architecture (Arquitetura de três camadas) onde são divididas em:

- **Camada de apresentação (Presentation layer):** onde é responsável pela a interface do usuário ou uma camada de apresentação genérica.
- **Camada de aplicação (Logic Layer):** onde normalmente os dados são processados e implementa as regras de negócio da aplicação.
- **Camada de dados (Data layer):** no qual os dados são armazenados e gerenciados, fornecendo à camada de lógica os dados necessários para execução de processos.

O diagrama abaixo, mostra um exemplo básico de como podemos implementar uma arquitetura multicamadas para uma aplicação web que performa funções, como por exemplo, assistir um filme ou até mesmo fazer alguma compra:

![alt text](/assets/images/n-tier-diagram.png)

Podemos constatar as três camadas:

1. **Web layer** (Front-end):
2. **Application-layer** (Back-end): Nossa camada de aplicação
3. **Database-layer** (Banco de Dados): Nossa camada de dados

## A camada de apresentação

A camada web, também conhecida como camada de apresentação, provê as interfaces onde o usuário vai interagir com a aplicação. A camada web é a sua visualização da aplicação, por exemplo, um site ou até mesmo um e-commerce onde você faz compras.
Normalmente desenvolvedores criam essa camada de apresentação usando tecnologias como HTML, CSS, JavaScript e seus frameworks (React, Angular, Vue e etc.). Essa camada coleta as informações do usuário e passa para a camada de aplicação, por exemplo, um formulário de cadastro.

## A camada de aplicação

A camada de aplicação, pode ser resumida em uma camada onde a lógica do negócio acontece, é onde o core do produto fica. A camada de apresentação coleta os dados e informações dos usuários e passa esses dados para que sejam processados pela a camada de aplicação, para termos algum resultado esperado. Por exemplo, um site de compras como o da Amazon, os usuários pode filtrar produtos por ele ser prime ou não e ordenar em ordem crescente ou decrescente. Em retorno a camada de aplicação retorna os dados que foram capturados e passam para a camada de aplicação para que a mesma possa performar as regras de negócio.
Geralmente numa arquitetura de três camadas, todos os algoritmos e lógicas ficam na camada de aplicação.
A camada de aplicação é o centro do negócio que performa as regras de negócio nos dados que estão armazenados na camada de dados.

## A camada de dados

A camada de dados ou também conhecida como Database Layer ou Data tier é responsável por armazenar todas as informações relacionadas aos usuários e suas transações. Essencialmente ela contem qualquer dado que necessite ser persistido na camada de dados. Essa informação pode ser reenviada para a camada de aplicação para o processamento de alguma regra de negócio e eventualmente é renderizada para o usuário final na camada de apresentação.

## Conclusão

Falamos aqui de como a arquitetura de multicamadas pode ser utilizada e demos um exemplo de uma arquitetura de três camadas para uma aplicação web.
Toda a jornada através dessa arquitetura nos apresentou benefícios e uma visão abrangente de suas camadas e responsabilidades. É importante ressaltar que ao estruturar um sistema com camadas bem definidas, com responsabilidades claras e interfaces bem documentadas, os benefícios acabam se estendendo desde a agilidade no desenvolvimento até mesmo a confiabilidade e resiliência de seu sistema a longo prazo.

Lembre-se que, como qualquer outra ferramenta, a efetividade da arquitetura depende de sua implementação adequada. Por isso é importante passar por conceitos da engenharia de requisitos contendo os requisitos funcionais e não funcionais de seu negócio.


<hr>
¹ É uma abordagem para o desacoplamento de componentes em um sistema, onde esses componentes dependem uns dos outros o mínimo possível.

² Capacidade de um sistema lidar com o aumento da demanda sem perder desempenho.

³ Sistemas elásticos se ajustam à demanda, crescendo ou diminuindo sem afetar o desempenho.


[Home](/).