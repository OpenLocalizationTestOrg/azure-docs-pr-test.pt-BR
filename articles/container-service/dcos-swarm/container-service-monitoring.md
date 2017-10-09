---
title: cluster do Azure DC/OS aaaMonitor - Datadog | Microsoft Docs
description: "Monitore um cluster do Serviço de Contêiner do Azure com o Datadog. Use Olá DC/sistema operacional da web da interface do usuário toodeploy Olá Datadog agentes tooyour cluster."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Contêineres, DC/OS, Docker Swarm, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a>Monitorar um cluster DC/OS do Serviço de Contêiner do Azure com Datadog
Este artigo é implantará nós de agente de saudação Datadog agentes tooall em seu cluster de serviço de contêiner do Azure. Você precisará de uma conta no Datadog para fazer esta configuração. 

## <a name="prerequisites"></a>Pré-requisitos
[Implantar](container-service-deployment.md) e [conectar](../container-service-connect.md) um cluster configurado pelo Serviço de Contêiner do Azure. Explorar Olá [maratona UI](container-service-mesos-marathon-ui.md). Vá muito[http://datadoghq.com](http://datadoghq.com) tooset uma conta Datadog. 

## <a name="datadog"></a>Datadog
O Datadog é um serviço de monitoramento que reúne dados de monitoramento de seus contêineres em seu cluster do Serviço de Contêiner do Azure. O Datadog tem um Painel de Integração do Docker, onde você pode ver as métricas específicas em seus contêineres. As métricas obtidas de seus contêineres são organizadas por CPU, Memória, Rede e E/S. O Datadog divide as métricas em contêineres e em imagens. Um exemplo de quais Olá UI parece CPU uso está abaixo.

![Interface do usuário do Datadog](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a>Configurar uma implantação do Datadog com Marathon
Estas etapas mostrarão como tooconfigure e implantar Datadog aplicativos tooyour cluster com maratona. 

Acesse a interface do usuário do DC/OS via [http://localhost:80/](http://localhost:80/). Uma vez no hello navegue de interface do usuário do controlador de domínio/OS toohello "Universo", que está no hello inferior esquerda e, em seguida, procure "Datadog" e clique em "Instalar".

![Pacote de Datadog dentro Olá universo de DC/OS](./media/container-service-monitoring/datadog1.png)

Agora toocomplete Olá configuração você precisará de uma conta de Datadog ou uma conta de avaliação gratuita. Depois de entrar no site de Datadog toohello pesquisar toohello esquerda e vá tooIntegrations ->, em seguida, [APIs](https://app.datadoghq.com/account/settings#api). 

![Chave de API do Datadog](./media/container-service-monitoring/datadog2.png)

Em seguida, digite sua chave de API em configuração Datadog Olá Olá universo de DC/OS. 

![Configuração de Datadog no hello universo de DC/OS](./media/container-service-monitoring/datadog3.png) 

Em Olá acima configuração instâncias são definidas too10000000 para que sempre que for adicionado um novo nó de cluster toohello Datadog implantará automaticamente um nó de toothat do agente. Essa é uma solução temporária. Depois de instalar o pacote de saudação, você deve navegar toohello back Datadog site e localizar "[painéis](https://app.datadoghq.com/dash/list)." A partir daí, você verá os painéis Custom e Integration. Olá [painel Docker](https://app.datadoghq.com/screen/integration/docker) terá todas as métricas de contêiner de saudação é necessário para o monitoramento do seu cluster. 

