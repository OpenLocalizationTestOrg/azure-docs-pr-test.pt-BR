---
title: "aaaIntroduction tooAzure serviço de contêiner para Kubernetes | Microsoft Docs"
description: "Serviço de contêiner do Azure para Kubernetes torna toodeploy simple e gerenciar aplicativos de contêiner no Azure."
services: container-service
documentationcenter: 
author: gabrtv
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kubernetes, Docker, Contêineres, microsserviços, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/21/2017
ms.author: gamonroy
ms.custom: mvc
ms.openlocfilehash: bfc85a180bdf4a405c9047eb882d3eed01640dd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-container-service-for-kubernetes"></a>Introdução tooAzure serviço de contêiner para Kubernetes
Serviço de contêiner do Azure para Kubernetes torna toocreate simple, configurar e gerenciar um cluster de máquinas virtuais que são pré-configurados toorun em contêineres de aplicativos. Isso permite que você toouse suas habilidades existentes, ou exploram um corpo grande e crescente de experiência da comunidade, toodeploy e gerenciar aplicativos de contêiner no Microsoft Azure.

Usando o serviço de contêiner do Azure, você pode tirar proveito da saudação recursos empresariais do Azure, enquanto mantém a portabilidade de aplicativo por meio de Kubernetes e Olá formato de imagem do Docker.

## <a name="using-azure-container-service-for-kubernetes"></a>Usando o Serviço de Contêiner do Azure para Kubernetes
Nosso objetivo com o serviço de contêiner do Azure é tooprovide um ambiente de hospedagem de contêiner usando ferramentas de código-fonte aberto e tecnologias que são comuns entre os clientes hoje. toothis final, expomos saudação padrão Kubernetes API os pontos de extremidade. Ao usar esses pontos de extremidade padrão, você pode utilizar qualquer software que é capaz de se comunicando tooa Kubernetes cluster. Por exemplo, você pode escolher [kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/), [helm](https://helm.sh/), ou [draft](https://github.com/Azure/draft).

## <a name="creating-a-kubernetes-cluster-using-azure-container-service"></a>Criando um Cluster Kubernetes usando o Serviço de Contêiner do Azure
toobegin usando o serviço de contêiner do Azure, implantar um cluster do serviço de contêiner do Azure com hello [2.0 do CLI do Azure](container-service-kubernetes-walkthrough.md) ou por meio do portal hello (Olá pesquisa Marketplace para **serviço de contêiner do Azure**). Se você for um usuário avançado que precisa de mais controle sobre modelos do hello Azure Resource Manager, você pode usar o código-fonte aberto Olá [acs mecanismo](https://github.com/Azure/acs-engine) toobuild projeto seus próprios Kubernetes personalizados do cluster e implantá-lo por meio de saudação `az` CLI.

### <a name="using-kubernetes"></a>Como usar Kubernetes
O Kubernetes automatiza a implantação, o dimensionamento e o gerenciamento de aplicativos em contêineres. Ele tem um conjunto avançado de recursos, incluindo:
* Binpacking automático
* Autorrecuperação
* Dimensionamento em escala horizontal
* Descoberta de serviço e balanceamento de carga
* Reversões e distribuições automatizadas
* Segredos e gerenciamento de configuração
* Orquestração de armazenamento
* Execução do Lote

Diagrama da arquitetura de Kubernetes implantado por meio do Serviço de Contêiner do Azure:

![Serviço de contêiner do Azure configurado toouse Kubernetes.](media/acs-intro/kubernetes.png)

## <a name="videos"></a>Vídeos

Suporte a Kubernetes nos Serviços de Contêiner do Azure (Azure Friday, janeiro de 2017):

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Kubernetes-Support-in-Azure-Container-Services/player]
>
>

Ferramentas para desenvolver e implantar aplicativos no Kubernetes (Azure OpenDev, junho de 2017):

> [!VIDEO https://channel9.msdn.com/Events/AzureOpenDev/June2017/Tools-for-Developing-and-Deploying-Applications-on-Kubernetes/player]
>
>

## <a name="next-steps"></a>Próximas etapas

Explorar Olá [Kubernetes Quickstart](container-service-kubernetes-walkthrough.md) toobegin Explorando o serviço de contêiner do Azure hoje.
