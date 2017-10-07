---
title: aaaMonitor um cluster Azure DC/OS - ELK pilha | Microsoft Docs
description: "Monitore um cluster de SO/DC no cluster do serviço de contêiner do Azure com ELK (Elasticsearch, Logstash e Kibana)."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Contêineres, CD/OS, Azure, monitoramento, elk"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a>Monitorar um cluster do Serviço de Contêiner do Azure com ELK
Neste artigo, demonstraremos como toodeploy Olá ELK (Elasticsearch, Logstash, Kibana) de pilha em um cluster de SO/controlador de domínio no serviço de contêiner do Azure. 

## <a name="prerequisites"></a>Pré-requisitos
[Implantar](container-service-deployment.md) e [conectar](../container-service-connect.md) um cluster DC/OS configurado pelo Serviço de Contêiner do Azure. Explorar o painel de DC/OS hello e serviços maratona [aqui](container-service-mesos-marathon-ui.md). Também instalar Olá [balanceador de carga maratona](container-service-load-balancing.md).


## <a name="elk-elasticsearch-logstash-kibana"></a>ELK (Elasticsearch, Logstash, Kibana)
Pilha ELK é uma combinação de Elasticsearch, Logstash, e Kibana que fornece uma pilha de tooend final que pode ser usado toomonitor e analise logs em seu cluster.

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a>Configurar a pilha ELK Olá em um cluster de DC/OS
Interface de usuário do controlador de domínio/OS por meio de acesso [http://localhost:80 /](http://localhost:80/) uma vez no hello navegue de interface do usuário do controlador de domínio/OS muito**universo**. Pesquisar e instalar Elasticsearch, Logstash e Kibana da saudação universo de DC/OS e na ordem específica. Você pode aprender mais sobre a configuração se você for toohello **instalação avançada** link.

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

Uma vez Olá contêineres ELK e estão em funcionamento, você precisa tooenable Kibana toobe acessado por meio de balanceamento de carga maratona. Navegue muito **serviços** > **kibana**e clique em **editar** conforme mostrado abaixo.

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


Alternar muito**modo JSON** e role para baixo toohello seção de rótulos.
Você precisa tooadd um `"HAPROXY_GROUP": "external"` entrada aqui conforme mostrado abaixo.
Depois que você clicar em **Implantar alterações**, seu contêiner será reinicializado.

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


Se você quiser tooverify que Kibana está registrado como um serviço no painel HAPROXY hello, você precisa tooopen porta 9090 no cluster de agente hello como HAPROXY é executado na porta 9090.
Por padrão, é abrir as portas 80, 8080 e 443 em Olá cluster do agente de controlador de domínio/OS.
Instruções tooopen uma porta e fornecer público avaliar são fornecidos [aqui](container-service-enable-public-access.md).

tooaccess Olá painel HAPROXY, interface do administrador abrir Olá maratona LB em: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.
Quando você navegar toohello URL, você deve ver o painel HAPROXY Olá conforme mostrado abaixo e você deverá ver uma entrada de serviço para Kibana.

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


Painel de Kibana de saudação tooaccess, que é implantado na porta 5601, é necessário tooopen porta 5601. Siga as instruções [aqui](container-service-enable-public-access.md). Em seguida, abra o painel de Kibana de saudação em: `http://localhost:5601`.

## <a name="next-steps"></a>Próximas etapas

* Para configuração e encaminhamento de log de aplicativo e sistema, confira [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/) (Gerenciamento de Log no DC/SO com ELK).

* toofilter logs, consulte [filtragem de Logs com ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/). 

 

