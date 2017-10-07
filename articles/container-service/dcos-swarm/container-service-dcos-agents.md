---
title: "pools de agente aaaDC/OS para o serviço de contêiner do Azure | Microsoft Docs"
description: "Como os pools de agente públicas e privadas de saudação funcionam com um cluster do serviço de contêiner do Azure DC/OS"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, Contêineres, Microsserviços, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c7d3889db07cb9908e8b68b668bd8a14ef3c2552
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-agent-pools-for-azure-container-service"></a>Pools de agentes DC/OS para Serviço de Contêiner do Azure
Os clusters DC/OS no Serviço de Contêiner do Azure contêm nós de agente em dois pools, um público e um privado. Um aplicativo pode ser implantado tooeither pool, que afetam a acessibilidade entre computadores em seu serviço de contêiner. Hello máquinas podem ser toohello exposto à internet (público) ou mantidos interno (privado). Este artigo fornece uma visão geral sobre o motivo da existência de pools público e privado.


* **Agentes privados**: nós de agente privado são executados por meio de uma rede não roteável. Essa rede é acessível apenas da zona do Olá administrador ou por meio do roteador de borda de zona pública hello. Por padrão, o DC/SO inicia aplicativos em nós de agente privada. 

* **Agentes públicos**: nós de agente público executam aplicativos e serviços DC/OS por meio de uma rede acessível publicamente. 

Para obter mais informações sobre segurança de rede do controlador de domínio/sistema operacional, consulte Olá [documentação do controlador de domínio/OS](https://dcos.io/docs/1.7/administration/securing-your-cluster/).

## <a name="deploy-agent-pools"></a>Implantar pools de agentes

Olá DC/OS agente pools no serviço de contêiner do Azure são criados da seguinte maneira:

* Olá **privada pool** contém Olá número de nós de agente que você especifique quando você [implantar Olá DC/OS cluster](container-service-deployment.md). 

* Olá **pública pool** inicialmente contém um número predeterminado de nós de agente. Esse pool é adicionado automaticamente quando Olá DC/OS cluster for provisionado.

Olá privada e Olá públicos são conjuntos de escala de máquina virtual do Azure. Você pode redimensionar esses pools após a implantação.

## <a name="use-agent-pools"></a>Usar pools de agentes
Por padrão, **maratona** implanta qualquer toohello aplicativo novo *privada* nós do agente. Ter tooexplicitly implantar Olá aplicativo toohello *pública* nós durante a criação de saudação do aplicativo hello. Selecione Olá **opcional** guia e digite **slave_public** para Olá **funções de recurso aceitos** valor. Esse processo está documentado [aqui](container-service-mesos-marathon-ui.md#deploy-a-docker-formatted-container) e em Olá [DC/OS](https://dcos.io/docs/1.7/administration/installing/custom/create-public-agent/) documentação.

## <a name="next-steps"></a>Próximas etapas
* Leia mais sobre [como gerenciar seus contêineres DC/OS](container-service-mesos-marathon-ui.md).

* Saiba como muito[abrir o firewall do hello](container-service-enable-public-access.md) fornecido pelos contêineres do Azure tooallow acesso público tooyour DC/OS.

