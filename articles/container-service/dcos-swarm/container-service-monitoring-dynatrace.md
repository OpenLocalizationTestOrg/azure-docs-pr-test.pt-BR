---
title: cluster do Azure DC/OS aaaMonitor - Dynatrace | Microsoft Docs
description: "Monitorar um cluster DC/OS do Serviço de Contêiner do Azure com Dynatrace. Implante Olá Dynatrace OneAgent usando Olá DC/OS painel."
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: "Contêineres, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a>Monitorar um cluster de DC/sistema operacional do Serviço de Contêiner do Azure com Dynatrace SaaS/gerenciado
Neste artigo, mostramos como Olá toodeploy [Dynatrace](https://www.dynatrace.com/) Olá de OneAgent toomonitor todos os nós do agente em seu cluster de serviço de contêiner do Azure. Você precisa de uma conta com o Dynatrace SaaS/gerenciado para essa configuração. 

## <a name="dynatrace-saasmanaged"></a>Dynatrace SaaS/gerenciado
O Dynatrace é uma solução de monitoramento nativa da nuvem para ambientes de cluster e contêiner altamente dinâmicos. Ele permite que você toobetter otimizar suas implantações de contêiner e as alocações de memória usando dados de uso em tempo real. Ele é capaz de identificar automaticamente problemas de infraestrutura e aplicativo, fornecendo linha de base, correlação de problemas e detecção de causa-raiz automatizadas.

a seguir Olá figura mostra Olá Dynatrace UI:

![Interface do usuário do Dynatrace](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a>Pré-requisitos 
[Implantar](container-service-deployment.md) e [conectar](./../container-service-connect.md) tooa cluster configurado pelo serviço de contêiner do Azure. Explorar Olá [maratona UI](container-service-mesos-marathon-ui.md). Vá muito[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset uma conta Dynatrace SaaS.  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a>Configurar uma implantação do Dynatrace com o Marathon
Estas etapas mostram como tooconfigure e implantar Dynatrace aplicativos tooyour cluster com maratona.

1. Acesse a interface do usuário do DC/OS via [http://localhost:80/](http://localhost:80/). Uma vez no hello DC/sistema operacional da interface do usuário, navegue toohello **universo** guia e, em seguida, procure **Dynatrace**.

    ![Dynatrace no universo de DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. configuração de saudação toocomplete, é necessário uma conta Dynatrace SaaS ou uma conta de avaliação gratuita. Quando você faz logon no painel de Dynatrace hello, selecione **implantar Dynatrace**.

    ![Configurar integração de PaaS do Dynatrace](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. Na página de saudação, selecione **configurar a integração de PaaS**. 

    ![Token da API do Dynatrace](./media/container-service-monitoring-dynatrace/api-token.png) 

4. Insira seu token de API em Olá Dynatrace OneAgent configuração Olá universo de DC/OS. 

    ![Configuração de dynaTrace OneAgent no hello universo de DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. Definir instâncias Olá toohello número de nós que você pretende toorun. Definir um número mais alto também funciona, mas o controlador de domínio/OS continuará tentando toofind novas instâncias até que esse número, na verdade, seja atingido. Se preferir, você também pode definir este valor tooa como 1000000. Nesse caso, sempre que um novo nó for adicionado toohello cluster, Dynatrace implanta automaticamente um agente toothat novo nó, preço de saudação do controlador de domínio/sistema operacional tentar constantemente instâncias adicionais do toodeploy.

    ![Configuração de dynaTrace no hello universo de SO/DC-instâncias](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a>Próximas etapas

Depois de instalar pacote hello, navegue toohello back Dynatrace painel. Você pode explorar as métricas de uso diferente de saudação para contêineres de saudação no cluster. 
