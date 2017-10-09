---
title: "cluster aaaMonitor um serviço de contêiner do Azure com Sysdig | Microsoft Docs"
description: "Monitore um cluster do Serviço de Contêiner do Azure com Sysdig."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Contêineres, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a>Monitorar um cluster do Serviço de Contêiner do Azure com Sysdig
Neste artigo, vamos implantará nós de agente de saudação Sysdig agentes tooall em seu cluster de serviço de contêiner do Azure. Você precisa de uma conta com Sysdig para essa configuração. 

## <a name="prerequisites"></a>Pré-requisitos
[Implantar](container-service-deployment.md) e [conectar](../container-service-connect.md) um cluster configurado pelo Serviço de Contêiner do Azure. Explorar Olá [maratona UI](container-service-mesos-marathon-ui.md). Vá muito[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset uma conta de nuvem Sysdig. 

## <a name="sysdig"></a>Sysdig
Sysdig é um serviço de monitoramento que permite que você toomonitor seus contêineres dentro de seu cluster. Sysdig é conhecido toohelp na solução de problemas, mas ele também tem suas métricas de monitoramentos básico de rede, CPU, memória e e/s. Sysdig torna fácil toosee quais contêineres estão funcionando hello usando o máximo proveito das ou essencialmente hello mais memória e CPU. Essa exibição está em Olá seção de "Visão geral", que está atualmente em beta. 

![Interface do usuário de Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a>Configurar uma implantação de Sysdig com Marathon
Estas etapas mostrarão como tooconfigure e implantar Sysdig aplicativos tooyour cluster com maratona. 

Interface de usuário do controlador de domínio/OS por meio de acesso [http://localhost:80 /](http://localhost:80/) uma vez no hello DC/sistema operacional da interface do usuário navegue toohello "Universo", que está no hello inferior esquerda e, em seguida, procure "Sysdig".

![Sysdig no universo de DC/OS](./media/container-service-monitoring-sysdig/sysdig1.png)

Agora toocomplete Olá configuração são necessários um Sysdig nuvem conta ou uma conta de avaliação gratuita. Depois de entrar no site de nuvem Sysdig toohello, clique em seu nome de usuário e na página hello, você verá sua "chave de acesso". 

![Chave de API d Sysdig](./media/container-service-monitoring-sysdig/sysdig2.png) 

Em seguida, digite sua chave de acesso em configuração Sysdig Olá Olá universo de DC/OS. 

![Configuração de Sysdig no hello universo de DC/OS](./media/container-service-monitoring-sysdig/sysdig3.png)

Agora defina Olá instâncias too10000000 para que sempre que for adicionado um novo nó de cluster toohello Sysdig implantará automaticamente um agente toothat novo nó. Este é um toomake solução temporária se que sysdig implantará tooall novos agentes em cluster hello. 

![Configuração de Sysdig no hello universo de SO/DC-instâncias](./media/container-service-monitoring-sysdig/sysdig4.png)

Depois de instalar o pacote de saudação navegue back toohello Sysdig UI e você será tooexplore capaz de métricas de uso diferentes Olá para contêineres Olá no cluster. 

Você também pode instalar painéis específicos do Mesos e do Marathon por meio do [assistente de novo painel](https://app.sysdigcloud.com/#/dashboards/new).
