---
title: "TryHackMe - Corridor"
author: Kaio Gerhardt
description: ""
date: 2022-02-20 10:00:00 +0000
categories : [Write-Ups, TryHackMe]
tags: [tryhackme, idor, web, ctf]
---

<div align="center"> <script src="https://tryhackme.com/badge/3335350"></script> </div>

## Descrição da Maquina

Você se encontrou em um corredor estranho. Você consegue encontrar o caminho de volta para onde veio?

Neste desafio, você explorará potenciais vulnerabilidades de IDOR . Examine os endpoints de URL que você acessa enquanto navega no site e observe os valores hexadecimais que você encontrar (eles se parecem muito com um hash , não é?). Isso pode ajudar você a descobrir locais de sites que você não deveria acessar.

## Solução

Ao estartar a maquina e acessarmos ela pelo navegador, vemos uma pagina web igual a essa.

![page](/assets/img/write-ups/tryhackme/corridor/corridor-page.png)

Ao clicar em qualquer uma das portas, é possivel ver que será redirecionado para uma URL que contem uma string, muito semelhante com um Hash.

![hash](/assets/img/write-ups/tryhackme/corridor/corridor-hash.png)

Se pegarmos a hash que aparece no navegador e colocarmos no [crackstation](https://crackstation.net/), percebemos que a hash nada mais é do que um numero em MD5. Portanto, se pressupoe que todas as outras portas são apenas um numero sequencial encodade em MD5 tambem.

![crackstation](/assets/img/write-ups/tryhackme/corridor/corridor-crackstation.png)

Com isso, podemos realizar um Fuzzing sequencial, encodando em MD5, podemos fazer isso diretamente com o Burp. Ao rodar percebemos que a requisição com o numero 0 retorna um status code 200, com um tamanho de pagina diferente, dando a entender que algo de diferente tem naquele diretorio.

![burp](/assets/img/write-ups/tryhackme/corridor/corridor-burp.png)

Portanto, ao encodar o numero 0 em MD5 em qualquer site web temos a hash `cfcd208495d565ef66e7dff9f98764da`. E ao coloca-la na url, somos redirecionados para uma pagina onde contem a flag do ctf.

![flag](/assets/img/write-ups/tryhackme/corridor/corridor-flag.png)