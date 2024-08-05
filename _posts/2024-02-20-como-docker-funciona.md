---
title: "Como o Docker funciona por baixo dos panos"
author: Kaio Gerhardt
description: ""
date: 2022-02-20 10:00:00 +0000
categories : [Artigo]
tags: [docker, linux, DevOps, containers]
---

A maioria, se não todos, já devem ter ouvido falar sobre o famoso Docker. No entanto, nem todos sabem o que de fato ele é, como ele funciona e o que faz por baixo de todos aqueles comandos. Assim, tentarei explicar de forma breve e simples como funciona um contêiner e um Container Engine, o Docker, neste caso.

Um contêiner, nada mais é do que um processo isolado que roda usando recursos do seu Host. No qual podemos configurar e executar aplicações isoladas. Sendo assim, é possível executar diversas aplicações distintas em uma mesma máquina sem ter nenhum tipo de conflito.

# Mas afinal, como funciona e consegue garantir essa camada de isolamento?

Para esclarecer, o contêiner e qualquer Container Engine foi feito para funcionar no linux. Qualquer coisa que a faça executar fora deste sistema operacional é apenas uma adaptação.

Dessa forma, o Docker utiliza [Linux Primitives](https://livebook.manning.com/book/core-kubernetes/chapter-3/v-2/1), que são funções nativas do kernel linux, que estabelece todo o necessário para a construção do contêiner. São utilizadas duas coisas principais do linux para isolar os processos no host e manter os ambientes de execução consistentes.

- **cgroups (Control Groups)** são utilizados principalmente para controlar e limitar os recursos que um contêiner pode usar, como CPU, memória e I/O. Isso garante que cada contêiner criado tenha os recursos configurados, evitando assim que ele consuma todos os recursos do host.

- **namespaces:** os namespaces são utilizados para o isolamento de recursos, como processos, redes, sistemas de arquivos, entre outros. Cada contêiner é executado dentro de um namespace próprio, o que cria a ilusão para o contêiner que é o único dentro do host.

![docker](/assets/img/artigos/como-docker-funciona/docker.png)

O isolamento fica bem simples de compreender ao visualizar a imagem acima. No qual o cgroups atua diretamente no kernel, limitando os recursos que devem ser disponibilizados pelo mesmo. E os namespaces, que atuam na separação dos processos diretamente no host.

De forma bastante simplificada, é assim que o Contêiner Engine, consegue executar e manter todo o isolamento dos contêineres dentro do host.