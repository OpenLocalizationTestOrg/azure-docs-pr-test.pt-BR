---
title: "aaaAzure tutorial de instâncias de contêiner - preparar seu aplicativo | Documentos do Azure"
description: "Preparar um aplicativo para implantação tooAzure instâncias de contêiner"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a>Criar contêiner para implantação tooAzure instâncias de contêiner

As Instâncias de Contêiner do Azure permitem a implantação de contêineres do Docker na infraestrutura do Azure sem o provisionamento de máquinas virtuais ou a adoção de serviço de nível superior. Neste tutorial, você criará um aplicativo Web simples no Node.js e o empacotará em um contêiner que pode ser executado usando as Instâncias de Contêiner do Azure. Abordaremos:

> [!div class="checklist"]
> * Clonando a fonte do aplicativo do GitHub  
> * Criando imagens de contêiner da fonte do aplicativo
> * Imagens de saudação de teste em um ambiente de Docker local

Tutoriais subsequentes, você carregar sua imagem tooan registro de contêiner do Azure e, em seguida, implantá-los tooAzure instâncias de contêiner.

## <a name="before-you-begin"></a>Antes de começar

Este tutorial assume uma compreensão básica dos conceitos fundamentais do Docker como contêineres, imagens de contêiner e comandos básicos do docker. Se necessário, consulte [Get started with Docker]( https://docs.docker.com/get-started/) (Introdução ao Docker) para conhecer os conceitos básicos de contêiner. 

toocomplete neste tutorial, você precisa de um ambiente de desenvolvimento do Docker. O Docker fornece pacotes que configuram facilmente o Docker em qualquer sistema [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) ou [Linux](https://docs.docker.com/engine/installation/#supported-platforms).

## <a name="get-application-code"></a>Obter o código de aplicativo

exemplo Hello neste tutorial inclui um aplicativo da web simples criado no [Node.js](http://nodejs.org). aplicativo Hello serve a uma página HTML estática e tem esta aparência:

![Aplicativo de tutorial mostrado no navegador][aci-tutorial-app]

Use git toodownload Olá exemplo:

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a>Criar imagem de contêiner Olá

Olá Dockerfile fornecida no repositório de exemplo hello mostra como o contêiner de saudação é criado. Ele começa em um [imagem oficial do Node. js] [ dockerhub-nodeimage] com base em [Linux Alpine](https://alpinelinux.org/), uma distribuição pequena que é adequado toouse com contêineres. Em seguida, copia os arquivos de aplicativo hello contêiner hello, dependências usando Olá Node Package Manager é instalado e finalmente inicia o aplicativo hello.

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

Saudação de uso `docker build` imagem de contêiner do comando toocreate hello, marcando-o como *aci de tutorial de aplicativo*:

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

Saudação de uso `docker images` toosee imagem de saudação criada:

```bash
docker images
```

Saída:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a>Executar o contêiner de saudação localmente

Antes de tentar implantar Olá contêiner tooAzure instâncias de contêiner, executá-lo localmente tooconfirm funciona. Olá `-d` switch permite que o contêiner Olá executadas em segundo plano hello, enquanto `-p` permite que você toomap uma porta arbitrária no seu tooport computação 80 no contêiner de saudação.

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

Olá abrir navegador toohttp://localhost:8080 tooconfirm que Olá contêiner está em execução.

![Aplicativo hello em execução localmente no navegador Olá][aci-tutorial-app-local]

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você criou uma imagem de contêiner pode ser implantado tooAzure instâncias de contêiner. Olá, as etapas a seguir foram concluída:

> [!div class="checklist"]
> * Fonte do aplicativo hello clonagem do GitHub  
> * Criando imagens de contêiner da fonte do aplicativo
> * Teste o contêiner de saudação localmente

Avançar toohello toolearn próximo de tutorial sobre como armazenar imagens de contêiner em um registro de contêiner do Azure.

> [!div class="nextstepaction"]
> [Imagens de push tooAzure registro de contêiner](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png