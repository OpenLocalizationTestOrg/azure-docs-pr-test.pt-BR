---
title: aaaManage Web App no Linux usando o Azure CLI 2.0 | Microsoft Docs
description: Gerenciar o aplicativo Web no Linux usando a CLI do Azure.
keywords: "serviço de aplicativo do azure, aplicativo web, cli, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a>Gerenciar o aplicativo Web no Linux usando a CLI do Azure

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

Usando os comandos de saudação neste artigo são toocreate capaz e gerenciar um aplicativo Web no Linux usando 2.0 do CLI do Azure.
Você pode começar a usar a nova versão Olá de saudação CLI de duas maneiras:

* [Instalando a CLI do Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) em seu computador.
* Usando o [Azure Cloud Shell (versão prévia)](../cloud-shell/overview.md)


## <a name="create-a-linux-app-service-plan"></a>Criar um Plano do Serviço de Aplicativo do Linux

toocreate um plano de serviço de aplicativo do Linux, você pode usar o hello comando a seguir:

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a>Criar um aplicativo Web de contêiner do Docker personalizado

toocreate um aplicativo web e configurá-lo toorun um contêiner do Docker personalizado, você pode usar o hello comando a seguir:

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a>Ativar o log de contêiner do Docker Olá

tooactivate Olá log do contêiner Docker, você pode usar o comando a seguir de saudação:

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a>Alterar o contêiner de Docker Olá personalizado para um aplicativo Web existente no Linux App

toochange um aplicativo criado anteriormente, de saudação atual Docker imagem tooa nova imagem, você pode usar o hello comando a seguir:

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a>Usando imagens do Docker de um registro particular

Você pode configurar suas imagens de toouse do aplicativo de um registro particular. Você precisa tooprovide Olá url para o registro, o nome de usuário e a senha. Isso pode ser obtido usando Olá comando a seguir:

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a>Habilitar implantações contínuas para imagens personalizadas do Docker

Com o comando a seguir de saudação habilitar a funcionalidade de CD hello e obter a url do webhook hello. Essa url pode ser usado tooconfigure você DockerHub ou registro de contêiner do Azure repositórios.

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a>Criar um aplicativo Web no aplicativo Linux usando uma de nossas estruturas de tempo de execução internas

toocreate um aplicativo de Web PHP 5.6 na App Linux que, você pode usar o hello comando a seguir.

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a>Alterar a versão da estrutura de um aplicativo Web existente no aplicativo Linux

toochange um aplicativo criado anteriormente, de saudação atual do framework versão tooNode.js 6.11, você pode usar o hello comando a seguir:

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a>Configurar implantações do Git para seu aplicativo Web

tooset as implantações do Git para seu aplicativo, você pode usar o hello comando a seguir:

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a>Próximas etapas
* [O que é um Aplicativo Web do Azure no Linux?](app-service-linux-intro.md)
* [Instalar a CLI 2.0 do Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [Azure Cloud Shell (versão prévia)](../cloud-shell/overview.md)
* [Configurar ambientes de preparo no Serviço de Aplicativo do Azure](./web-sites-staged-publishing.md)
* [Implantação contínua com o Aplicativo Web do Azure no Linux](./app-service-linux-ci-cd.md)
