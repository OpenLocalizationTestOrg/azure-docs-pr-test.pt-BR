---
title: "repositórios de registro de contêiner aaaAzure | Microsoft Docs"
description: "Como repositórios de registro de contêiner do Azure toouse para imagens do Docker"
services: container-registry
documentationcenter: 
author: cristy
manager: balans
editor: dlepow
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: cristyg
ms.openlocfilehash: 06172a63465838a78a607f268da116d8158789ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-registry-repositories"></a>Repositórios de Registro de contêiner do Azure

Os Registros de Contêiner do Azure são compatíveis com uma variedade de serviços e orquestradores. toomake-serviços de fonte de saudação tootrack mais fácil e agentes do qual ACR é usado, começamos usando o campo de cabeçalho de Docker Olá Olá Docker.config arquivo.



## <a name="viewing-repositories-in-hello-portal"></a>Exibir os repositórios em Olá Portal

cabeçalhos ACR Olá seguem o formato de saudação:
```
X-Meta-Source-Client: <cloud>/<service>/<optionalservicename>
```

* Nuvem: Azure, Azure Stack ou outras nuvens do Azure específicas do país ou do governo. Embora no momento não haja suporte para o Azure Stack e nuvens do governo, este parâmetro habilita suporte futuro.
* Serviço: o nome do serviço de saudação.
* Optionalservicename: o parâmetro opcional para serviços com subserviços ou toospecify um SKU (ex: aplicativos web correspondem com aplicativos do Azure/app-service/web).

Orchestrators e serviços de parceiro são incentivados toouse cabeçalho específico valores toohelp com nosso telemetria. Os usuários também podem modificar o valor Olá passado toohello cabeçalho se desejarem.

valores Hello desejamos ACR parceiros toouse toopopulate hello "X-Meta-origem-cliente" campo são os seguintes:

| Nome do Serviço              | Cabeçalho                                |
| ------------------------- | ------------------------------------- |
| Serviço de Contêiner do Azure   | azure/compute/azure-container-service |
| Serviço de Aplicativo – Aplicativos Web    | azure/app-service/web-apps            |
| Serviço de Aplicativo – Aplicativos Lógicos  | azure/app-service/logic-apps          |
| Batch                     | azure/compute/batch                   |
| Console de nuvem             | azure/cloud-console                   |
| Funções                 | azure/compute/functions               |
| Internet das Coisas – Hub  | hub/de iot do Azure                         |
| HDInsight                 | hdinsight/de dados do Azure                  |
| Jenkins                   | Azure/jenkins                         |
| Machine Learning          | azure/data/machine-learning           |
| Service Fabric            | Azure/computação/serviço-malha          |
| VSTS                      | azure/vsts                            |


## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre registros e Olá suporte para serviços e orchestrators](container-registry-intro.md)
