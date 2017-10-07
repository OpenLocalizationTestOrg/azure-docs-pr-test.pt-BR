---
title: "aaaTroubleshooting instâncias de contêiner do Azure"
description: "Saiba como tootroubleshoot problemas com instâncias de contêiner do Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/03/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: dfec636a0a174c74a6f2e9d9c4da6e871f8d2fda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a>Solucionar problemas de implantação com as Instâncias de Contêiner do Azure

Este artigo mostra como tootroubleshoot problemas ao implantar contêineres tooAzure instâncias de contêiner. Ele também descreve alguns dos problemas comuns hello, que você pode encontrar.

## <a name="getting-diagnostic-events"></a>Obtendo eventos de diagnóstico

logs de tooview do seu código de aplicativo em um contêiner, você pode usar o hello [az contêiner logs](/cli/azure/container#logs) comando. Mas se o contêiner não implantar com êxito, você precisa de informações de diagnóstico de saudação do tooreview fornecidas pelo provedor de recursos de instâncias de contêiner do Azure hello. eventos de saudação tooview para seu contêiner, execute Olá comando a seguir:

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

saída de Hello inclui propriedades básicas de saudação do seu contêiner, juntamente com eventos de implantação:

```bash
{
  "containers": [
    {
      "command": null,
      "environmentVariables": [],
      "image": "microsoft/aci-helloworld",
      ...

      "events": [
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:52+00:00",
        "lastTimestamp": "2017-08-03T22:12:52+00:00",
        "message": "Pulling: pulling image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Pulled: Successfully pulled image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Created: Created container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Started: Started container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      }
    ],
    "name": "helloworld",
      "ports": [
        {
          "port": 80
        }
      ],
    ...
  ]
}
```

## <a name="common-deployment-issues"></a>Tarefas de implantação comuns

Há alguns problemas comuns responsáveis pela maioria dos erros na implantação.

### <a name="unable-toopull-image"></a>Não é possível toopull imagem

Se instâncias de contêiner do Azure é não é possível toopull sua imagem inicialmente, ele tenta novamente por um período antes da falha eventualmente. Se a imagem de saudação não pode ser extraída, eventos como Olá a seguir são mostrados:

```bash
"events": [
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:31+00:00",
    "lastTimestamp": "2017-08-03T22:19:31+00:00",
    "message": "Pulling: pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:32+00:00",
    "lastTimestamp": "2017-08-03T22:19:32+00:00",
    "message": "Failed: Failed toopull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:33+00:00",
    "lastTimestamp": "2017-08-03T22:19:33+00:00",
    "message": "BackOff: Back-off pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  }
]
```

tooresolve, excluir o contêiner de saudação e repita a sua implantação, pagante atenção se você digitou o nome de imagem Olá corretamente.

### <a name="container-continually-exits-and-restarts"></a>Contêiner sai e reinicia continuamente

Atualmente, o Instâncias de Contêiner do Azure dá suporte apenas a serviços de execução longa. Se o contêiner executa toocompletion e fecha, ele automaticamente reinicia e executa novamente. Se isso acontecer, eventos como os mostrados a seguir serão mostrados. Observe o contêiner Olá for iniciada com êxito, em seguida, reinicia rapidamente. Olá API de instâncias de contêiner inclui um `retryCount` reiniciou propriedade que mostra quantas vezes um contêiner específico.

```bash
"events": [
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:55+00:00",
    "lastTimestamp": "2017-08-03T22:23:22+00:00",
    "message": "Pulling: pulling image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:23:23+00:00",
    "message": "Pulled: Successfully pulled image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Created: Created container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Started: Started container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Created: Created container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Started: Started container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 13,
    "firstTimestamp": "2017-08-03T22:21:59+00:00",
    "lastTimestamp": "2017-08-03T22:24:36+00:00",
    "message": "BackOff: Back-off restarting failed container",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:22:13+00:00",
    "lastTimestamp": "2017-08-03T22:22:13+00:00",
    "message": "Created: Created container with id 72e347e891290e238135e4a6b3078748ca25a1275dbbff30d8d214f026d89220",
    "type": "Normal"
  },
  ...
```

> [!NOTE]
> A maioria das imagens de contêiner para as distribuições de Linux definido um shell, como bash, como o comando de padrão de saudação. Já que um shell por si só não é um serviço de execução longa, esses contêineres saem imediatamente e entram em um loop de reinicialização.

### <a name="container-takes-a-long-time-toostart"></a>Contêiner leva um tempo longo toostart

Se o contêiner usa toostart um longo tempo, mas eventualmente tiver êxito, inicie examinando o tamanho de saudação da sua imagem de contêiner. Como instâncias de contêiner do Azure recebe sua imagem de contêiner sob demanda, terá de tempo de inicialização de saudação é tooits está diretamente relacionado tamanho.

Você pode exibir o tamanho de saudação da sua imagem de contêiner usando Olá CLI do Docker:

```bash
docker images
```

Saída:

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

tamanhos de imagem tookeeping chave Olá pequenos é garantir que sua imagem final não contém tudo o que não é necessário em tempo de execução. Uma maneira toodo com [compilações de vários estágios](https://docs.docker.com/engine/userguide/eng-image/multistage-build/). Compilações de vários estágios tornam fácil tooensure que imagem final Olá contém somente artefatos de saudação é necessário para seu aplicativo e não os Olá extra de conteúdo que foi necessária no momento da compilação.

Hello, outros impacto maneira tooreduce Olá Olá pull de imagem em tempo de inicialização do contêiner é toohost imagem de contêiner de saudação usando Olá registro de contêiner do Azure no hello mesma região em que você pretende toouse instâncias de contêiner do Azure. Isso reduz o caminho de rede Olá Olá tootravel de necessidades de imagem de contêiner, reduzindo significativamente o tempo de download de saudação.
