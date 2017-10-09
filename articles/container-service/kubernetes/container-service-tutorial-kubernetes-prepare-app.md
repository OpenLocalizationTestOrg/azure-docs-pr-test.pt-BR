---
title: "tutorial de serviço de contêiner aaaAzure - preparar o aplicativo | Microsoft Docs"
description: "Tutorial do Serviço de Contêiner do Azure – preparar o aplicativo"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Kubernetes, DC/SO, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b537ecc9ff50358fb65b128bfe6eb894dd088cc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-images-toobe-used-with-azure-container-service"></a>Criar contêiner imagens toobe usado com o serviço de contêiner do Azure

Neste tutorial, parte um de sete, um aplicativo de vários contêineres é preparado para uso em Kubernetes. As etapas concluídas incluem:  

> [!div class="checklist"]
> * Clonando a fonte do aplicativo do GitHub  
> * Criando uma imagem de contêiner de fonte de saudação do aplicativo
> * Testando o aplicativo hello em um ambiente de Docker local

Depois de concluído, Olá aplicativo a seguir é acessível em seu ambiente de desenvolvimento local.

![Imagem do cluster Kubernetes no Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

Em tutoriais subsequentes, imagem de contêiner de saudação é carregado tooan registro de contêiner do Azure e, em seguida, executar em um Azure hospedado Kubernetes cluster.

## <a name="before-you-begin"></a>Antes de começar

Este tutorial assume uma compreensão básica dos conceitos fundamentais do Docker como contêineres, imagens de contêiner e comandos básicos do docker. Se necessário, consulte [Get started with Docker]( https://docs.docker.com/get-started/) (Introdução ao Docker) para conhecer os conceitos básicos de contêiner. 

toocomplete neste tutorial, você precisa de um ambiente de desenvolvimento do Docker. O Docker fornece pacotes que configuram facilmente o Docker em qualquer sistema [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) ou [Linux](https://docs.docker.com/engine/installation/#supported-platforms).

## <a name="get-application-code"></a>Obter o código de aplicativo

aplicativo de exemplo Hello usado neste tutorial é um aplicativo de votação básico. aplicativo Hello consiste em um componente web front-end e uma instância do Redis de back-end. componente de web Hello é empacotado em uma imagem de contêiner personalizado. instância do Redis Olá usa uma imagem sem modificações do Hub do Docker.  

Use git toodownload uma cópia do ambiente de desenvolvimento de tooyour de aplicativo hello.

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Interna Olá clonado diretório é o código-fonte aplicativo hello, um Docker pré-criados compõem o arquivo e um arquivo de manifesto Kubernetes. Esses arquivos são ativos toocreate usados em todo o conjunto de tutorial hello. 

## <a name="create-container-images"></a>Criar imagens de contêiner

[Composição de docker](https://docs.docker.com/compose/) pode ser usado tooautomate Olá compilação fora de imagens de contêiner e a implantação de saudação do contêiner de vários aplicativos.

Executar a imagem de contêiner de Olá Olá docker compose.yml arquivo toocreate, download Olá Redis imagem e iniciar o aplicativo hello.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

Quando concluído, use Olá [imagens do docker](https://docs.docker.com/engine/reference/commandline/images/) comando toosee imagens de saudação criada.

```bash
docker images
```

Observe que três imagens foram baixadas ou criadas. Olá *front do azure-voto* imagem contém o aplicativo hello. Ela foi derivada de saudação *nginx bulbo* imagem. imagem de Redis Olá foi baixada do Hub do Docker.

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

Executar Olá [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) saudação do comando toosee contêineres em execução.

```bash
docker ps
```

Saída:

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a>Testar o aplicativo localmente

Procure toohttp://localhost:8080 toosee Olá executando o aplicativo.

![Imagem do cluster Kubernetes no Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a>Limpar recursos

Agora que a funcionalidade do aplicativo foi validada, Olá contêineres em execução pode ser interrompido e removido. Não exclua imagens de contêiner de saudação. Olá *front do azure-voto* imagem é instância de registro de contêiner do Azure carregados tooan tutorial Avançar hello.

Execute Olá Olá toostop contêineres em execução a seguir.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

Exclua os contêineres de saudação interrompido com hello comando a seguir.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

Ao concluir, você tem uma imagem de contêiner que contém o aplicativo do Azure voto hello.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, um aplicativo foi testado e imagens de contêiner é criado para o aplicativo hello. Olá, as etapas a seguir foram concluída:

> [!div class="checklist"]
> * Fonte do aplicativo hello clonagem do GitHub  
> * Criando uma imagem de contêiner a partir da origem do aplicativo
> * Aplicativo hello testado em um ambiente de Docker local

Avançar toohello toolearn próximo de tutorial sobre como armazenar imagens de contêiner em um registro de contêiner do Azure.

> [!div class="nextstepaction"]
> [Imagens de push tooAzure registro de contêiner](./container-service-tutorial-kubernetes-prepare-acr.md)
