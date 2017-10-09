---
title: "tutorial de serviço de contêiner aaaAzure - implantar aplicativos | Microsoft Docs"
description: "Tutorial do Serviço de Contêiner do Azure – implantar aplicativo"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Kubernetes, DC/SO, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a>Executar aplicativos no Kubernetes

Neste tutorial, parte quatro de sete, um aplicativo de exemplo é implantado em um cluster Kubernetes. As etapas concluídas incluem:

> [!div class="checklist"]
> * Baixar arquivos de manifesto Kubernetes
> * Executar um aplicativo no Kubernetes
> * Testar o aplicativo hello

Em tutoriais subsequentes, este aplicativo é expandido, atualizado, e Operations Management Suite configurado o cluster de Kubernetes toomonitor hello.

Este tutorial assume uma compreensão básica dos conceitos de Kubernetes, para obter informações detalhadas sobre Kubernetes consulte Olá [Kubernetes documentação](https://kubernetes.io/docs/home/).

## <a name="before-you-begin"></a>Antes de começar

Nos tutoriais anteriores, um aplicativo foi empacotado em uma imagem de contêiner, esta imagem foi carregada tooAzure registro de contêiner e um cluster Kubernetes foi criado. Se você ainda não tiver feito essas etapas e deseja toofollow ao longo, retornar muito[Tutorial 1 – criar imagens de contêiner](./container-service-tutorial-kubernetes-prepare-app.md). 

No mínimo, este tutorial requer um cluster Kubernetes.

## <a name="get-manifest-file"></a>Obter arquivo de manifesto

Para este tutorial, [objetos Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) dão implantados utilizando um manifesto Kubernetes. Um manifesto Kubernetes é um arquivo formatado YAML ou JSON que contém instruções de implantação e configuração de objetos Kubernetes.

arquivo de manifesto de aplicativo Hello para este tutorial está disponível no repositório de aplicativo do hello Azure voto, foi clonado em um tutorial anterior. Se você ainda não tiver feito isso, clone o repositório de saudação com hello comando a seguir: 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

arquivo de manifesto Olá encontra-se em Olá seguindo o diretório de repositório de saudação clonado.

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a>Atualizar arquivo de manifesto

Se usar imagens de contêiner do registro de contêiner do Azure toostore hello, Olá toobe necessidades de manifesto atualizado com o nome de loginServer Olá ACR.

Obter o nome de servidor de logon do hello ACR com hello [lista de acr az](/cli/azure/acr#list) comando.

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Olá exemplo manifesto foi previamente criado com um nome de repositório de *microsoft*. Abra o arquivo hello com qualquer editor de texto e substitua Olá *microsoft* valor com o nome do servidor de logon de saudação da sua instância ACR.

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a>Implantar um aplicativo

Saudação de uso [kubectl criar](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) aplicativo hello de toorun de comando. Saudação de analisa esse comando arquivo de manifesto e criar objetos de Kubernetes de saudação definido.

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

Saída:

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a>Testar aplicativo

Um [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) é criado que expõe Olá aplicativo toohello internet. Esse processo pode levar alguns minutos. 

toomonitor andamento, use Olá [kubectl obter serviço](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) com hello `--watch` argumento.

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

Inicialmente, hello **IP externo** para Olá *front do azure-voto* serviço aparece como *pendente*. Depois que o endereço IP externo de saudação foi alterado de *pendente* tooan *endereço IP*, use `CTRL-C` processo de inspeção de kubectl toostop hello.

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

aplicativo de hello toosee, endereço IP externo de toohello procurar.

![Imagem do cluster Kubernetes no Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, Olá aplicativo voto do Azure foi implantado tooan Kubernetes de serviço de contêiner do Azure cluster. As tarefas concluídas incluem:  

> [!div class="checklist"]
> * Baixar arquivos de manifesto Kubernetes
> * Executar o aplicativo hello em Kubernetes
> * Aplicativo hello testado

Avançar toohello toolearn próximo de tutorial sobre como dimensionar um aplicativo Kubernetes e Olá Kubernetes infra-estrutura subjacente. 

> [!div class="nextstepaction"]
> [Dimensionar um aplicativo do Kubernetes e sua infraestrutura](./container-service-tutorial-kubernetes-scale.md)