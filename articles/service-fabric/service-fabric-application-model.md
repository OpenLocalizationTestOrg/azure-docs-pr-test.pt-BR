---
title: Modelo de aplicativo do Azure Service Fabric | Microsoft Docs
description: "Como modelar e descrever aplicativos e serviços no Service Fabric."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 17a99380-5ed8-4ed9-b884-e9b827431b02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/07/2017
ms.author: ryanwi
ms.openlocfilehash: d5f6fbb9d9c0bc0d9762f8d6b4b4eb3b02d29adc
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2017
---
# <a name="model-an-application-in-service-fabric"></a>Modelar um aplicativo no Malha do Serviço
Este artigo fornece uma visão geral do modelo de aplicativo do Azure Service Fabric e descreve como definir um aplicativo e um serviço por meio de arquivos de manifesto.

## <a name="understand-the-application-model"></a>Entenda o modelo de aplicativo
Um aplicativo é uma coleção de serviços membros que executam determinadas funções. Um serviço executa uma função completa e autônoma e pode iniciar e executar independentemente de outros serviços.  Um serviço é composto de código, configuração e dados. Para cada serviço, o código consiste em binários executáveis, a configuração consiste em configurações do serviço que podem ser carregadas no tempo de execução e os dados consistem em dados estáticos arbitrários a serem consumidos pelo serviço. Cada componente nesse modelo hierárquico de aplicativo pode ser atualizado e transformado em outra versão independentemente.

![O modelo de aplicativo Service Fabric][appmodel-diagram]

Um tipo de aplicativo é uma categorização de um aplicativo e consiste em um pacote de tipos de serviço. Um tipo de serviço é uma categorização de um serviço. A categorização pode ter diferentes definições e configurações, mas a funcionalidade núcleo permanece a mesma. As instâncias de um serviço são as diferentes variações de configuração de serviço de um mesmo tipo de serviço.  

Classes (ou "tipos") de aplicativos e serviços são descritas por meio de arquivos XML (manifestos de aplicativo e manifestos do serviço).  Os manifestos descrevem aplicativos e serviços, e são os modelos de aplicativos que poderão ser instanciados a partir do repositório de imagens do cluster.  Manifestos são abordados detalhadamente em [Manifestos de aplicativos e serviços](service-fabric-application-and-service-manifests.md). A definição de esquema dos arquivos ServiceManifest.xml e ApplicationManifest.xml é instalada com o SDK e as ferramentas do Service Fabric em *C:\Arquivos de Programas\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*. O esquema XML é documentado em [documentação do esquema ServiceFabricServiceModel.xsd](service-fabric-service-model-schema.md).

O código para instâncias do aplicativo diferentes será executado como processos separados, mesmo quando hospedadas pelo mesmo nó do Service Fabric. Além disso, o ciclo de vida de cada instância do aplicativo pode ser gerenciado (por exemplo, atualizado) independentemente. O diagrama a seguir mostra como os tipos de aplicativo são compostos de tipos de serviço, que, por sua vez, são compostos de código, configuração e pacotes de dados. Para simplificar o diagrama, somente os pacotes de código/configuração/dados de `ServiceType4` são mostrados, embora cada tipo de serviço inclua alguns ou todos os tipos de pacote.

![Tipos de aplicativos do Service Fabric e tipos de serviço][cluster-imagestore-apptypes]

Pode haver uma ou mais instâncias de um tipo de serviço ativo no cluster. Por exemplo, instâncias de serviço com estado, ou réplicas, alcançam alta confiabilidade replicando o estado entre as réplicas localizadas em diferentes nós do cluster. Essencialmente a replicação fornece redundância para que o serviço esteja disponível mesmo se um nó em um cluster falhar. Um [serviço particionado](service-fabric-concepts-partitioning.md) divide ainda mais seu estado (e padrões de acesso a esse estado) pelos nós do cluster.

O diagrama a seguir mostra a relação entre aplicativos e instâncias de serviço, partições e réplicas.

![Partições e réplicas dentro de um serviço][cluster-application-instances]

> [!TIP]
> É possível exibir o layout de aplicativos em um cluster usando a ferramenta Service Fabric Explorer disponível em http://&lt;yourclusteraddress&gt;:19080/Explorer. Para obter mais informações, consulte [Visualizando o cluster com o Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
> 
> 


## <a name="next-steps"></a>Próximas etapas
- Saiba mais sobre [escalabilidade de aplicativo](service-fabric-concepts-scalability.md).
- Saiba mais sobre [estado](service-fabric-concepts-state.md), [particionamento](service-fabric-concepts-partitioning.md) e [disponibilidade](service-fabric-availability-services.md) de serviços.
- Leia sobre como os aplicativos e serviços são definidos em [Manifestos de aplicativos e serviços](service-fabric-application-and-service-manifests.md).
- Os [modelos de hospedagem de aplicativo](service-fabric-hosting-model.md) descrevem a relação entre réplicas (ou instâncias) de um serviço implantado e o processo de host do serviço.

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png


