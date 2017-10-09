---
title: aaaManage Kubernetes Azure cluster com a interface da web | Microsoft Docs
description: "Usando Olá Kubernetes web da interface do usuário no serviço de contêiner do Azure"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a>Usando Olá Kubernetes web da interface do usuário com o serviço de contêiner do Azure

## <a name="prerequisites"></a>Pré-requisitos
Este passo a passo presume que você tenha [criado um cluster Kubernetes usando o Serviço de contêiner do Azure](container-service-kubernetes-walkthrough.md).


Ele também pressupõe que você tenha Olá 2.0 do CLI do Azure e `kubectl` ferramentas instaladas.

Você pode testar se você tiver Olá `az` ferramenta instalada executando:

```console
$ az --version
```

Se você não tiver Olá `az` ferramenta instalada, há instruções [aqui](https://github.com/azure/azure-cli#installation).

Você pode testar se você tiver Olá `kubectl` ferramenta instalada executando:

```console
$ kubectl version
```

Se não tem `kubectl` instalado, você pode executar:

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a>Visão geral

### <a name="connect-toohello-web-ui"></a>Conecte-se a interface da web toohello
Você pode iniciar a interface da web Kubernetes Olá executando:

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

Isso deve abrir um navegador configurado tootalk tooa segura proxy web conectar seu computador local toohello Kubernetes interface da web.

### <a name="create-and-expose-a-service"></a>Criar e expor um serviço
1. No hello Kubernetes interface da web, clique em **criar** botão na janela direita superior do hello.

    ![Criar interface do usuário Kubernetes](./media/container-service-kubernetes-ui/create.png)

    Isso abrirá uma caixa de diálogo em que você poderá começar a criar o aplicativo.

2. Olá nome `hello-nginx`. Saudação de uso [ `nginx` contêiner do Docker](https://hub.docker.com/_/nginx/) e implantar três réplicas do serviço web.

    ![Caixa de diálogo Criar Pod Kubernetes](./media/container-service-kubernetes-ui/nginx.png)

3. Em **Serviço**, selecione **Externo** e insira a porta 80.

    Essa configuração de balanceamento de carga três réplicas de toohello de tráfego.

    ![Caixa de diálogo Criar serviço Kubernetes](./media/container-service-kubernetes-ui/service.png)

4. Clique em **implantar** toodeploy esses contêineres e serviços.

    ![Implantar Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a>Exibir seus contêineres
Depois de clicar em **implantar**, Olá da interface do usuário mostra uma exibição do serviço que implanta:

![Status do Kubernetes](./media/container-service-kubernetes-ui/status.png)

Você pode ver o status de saudação de cada objeto Kubernetes no círculo Olá no lado esquerdo de saudação da interface do usuário, em **compartimentos**. Se for um círculo completo parcialmente, objeto Olá ainda está implantando. Quando um objeto é totalmente implantado, ele exibe uma marca de seleção verde:

![Kubernetes implantado](./media/container-service-kubernetes-ui/deployed.png)

Quando tudo estiver em execução, clique em um dos seus detalhes de toosee compartimentos sobre Olá executando o serviço web.

![Pods Kubernetes](./media/container-service-kubernetes-ui/pods.png)

Em Olá **compartimentos** modo de exibição, você pode ver informações sobre contêineres Olá pod hello, bem como recursos de CPU e memória de saudação usados por esses contêineres:

![Recursos do Kubernetes](./media/container-service-kubernetes-ui/resources.png)

Se você não vir recursos hello, talvez seja necessário toowait alguns minutos para Olá toopropagate de dados de monitoramento.

toosee Olá logs para o contêiner, clique em **exibir logs**.

![Logs do Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a>Exibindo o serviço
Adição toorunning seus contêineres, Olá Kubernetes UI criou externo `Service` que provisiona uma carga balanceador toobring tráfego toohello dos contêineres no cluster.

No painel de navegação esquerdo hello, clique em **serviços** tooview todos os serviços (deve haver apenas um).

![Serviços Kubernetes](./media/container-service-kubernetes-ui/service-deployed.png)

No modo de exibição, você verá um ponto de extremidade externo (endereço IP) que foi alocado tooyour serviço.
Se clicar no endereço IP, você deverá ver o contêiner nginx em execução por trás do balanceador de carga.

![nginx view](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a>Redimensionar o serviço
Em adição tooviewing seus objetos no hello da interface do usuário, você pode editar e atualizar objetos de API Kubernetes hello.

Primeiro, clique em **implantações** de saudação à esquerda de implantação de Olá de toosee de painel de navegação para seu serviço.

Quando estiver no modo de exibição, clique no conjunto de réplicas hello e, em seguida, clique em **editar** na barra de navegação superior hello:

![Editar Kubernetes](./media/container-service-kubernetes-ui/edit.png)

Editar saudação `spec.replicas` campo toobe `2`e clique em **atualização**.

Isso faz com que número de saudação de réplicas toodrop tootwo excluindo um de seus compartimentos.

 

