---
title: aaaCreate Azure Service Fabric clusters no Windows Server e Linux | Microsoft Docs
description: "Clusters de malha do serviço executados no Windows Server e Linux, o que significa que você será capaz de aplicativos de malha do serviço de host e toodeploy em qualquer lugar, você pode executar o Windows Server ou Linux."
services: service-fabric
documentationcenter: .net
author: Chackdan
manager: timlt
editor: 
ms.assetid: 19ca51e8-69b9-4952-b4b5-4bf04cded217
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/08/2017
ms.author: chackdan
ms.openlocfilehash: 46d5f3d019339c57a0024f5a9d47d9018cca01a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-fabric-clusters-on-windows-server-or-linux"></a>Criar clusters do Service Fabric no Windows Server ou no Linux
Um cluster do Azure Service Fabric é um conjunto de máquinas físicas ou virtuais conectadas em rede, no qual os microsserviços são implantados e gerenciados. Um computador ou VM que faz parte de um cluster é chamado de nó de cluster. Podem ser dimensionado toothousands de nós de clusters. Se você adicionar um novo cluster de toohello de nós, Service Fabric redistribui réplicas de partição de serviço hello e instâncias em Olá aumentado o número de nós. Geral melhora o desempenho do aplicativo e reduz a contenção de toomemory de acesso. Se nós Olá cluster Olá não estão sendo usados com eficiência, você pode diminuir o número de saudação de nós no cluster de saudação. Serviço de malha novamente redistribui réplicas da partição hello e instâncias em número de saudação reduzido de nós toomake melhor o uso de hardware de saudação em cada nó.

Malha do serviço permite a criação de saudação de clusters de malha do serviço em quaisquer máquinas virtuais ou computadores que executam o Windows Server ou Linux. Isso significa que você é capaz de toodeploy e executar aplicativos de malha do serviço em qualquer ambiente em que você tem um conjunto de computadores Windows Server ou Linux que estão interconectados, seja local, Microsoft Azure ou com qualquer provedor de nuvem.

## <a name="create-service-fabric-clusters-on-azure"></a>Criar clusters do Service Fabric no Azure
Criar um cluster no Azure é feito através de um modelo de recurso ou Olá portal do Azure. Leitura [criar um cluster do Service Fabric usando um modelo do Gerenciador de recursos](service-fabric-cluster-creation-via-arm.md) ou [criar um cluster do Service Fabric do hello portal do Azure](service-fabric-cluster-creation-via-portal.md) para obter mais informações.

## <a name="supported-operating-systems-for-clusters-on-azure"></a>Sistemas operacionais com suporte para clusters no Azure
Você é capaz de toocreate clusters em VMs que executam esses sistemas operacionais:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux Ubuntu 16.04 (em preview pública) 

## <a name="create-service-fabric-standalone-clusters-on-premises-or-with-any-cloud-provider"></a>Crie clusters autônomos do Service Fabric localmente ou com qualquer provedor de nuvem
Serviço de malha fornece um pacote de instalação para você toocreate autônomo do Service Fabric clusters no local ou em qualquer provedor de nuvem

Para obter mais informações sobre como configurar os clusters autônomos do Service Fabric no Windows Server, leia [Service Fabric cluster creation for Windows Server](service-fabric-cluster-creation-for-windows-server.md)

### <a name="any-cloud-deployments-vs-on-premises-deployments"></a>Qualquer implantação na nuvem vs. implantações locais
Olá para a criação de um cluster do Service Fabric local é semelhante processo toohello de criação de um cluster em qualquer nuvem de sua escolha, com um conjunto de máquinas virtuais. Olá etapas iniciais tooprovision Olá VMs são administradas pelo provedor de nuvem hello ou ambiente local que você está usando. Depois que você tenha um conjunto de VMs com habilitado entre elas, a conectividade de rede, em seguida, Olá etapas tooset pacote do Service Fabric hello, editar configurações de cluster hello e executar a criação do cluster hello e scripts de gerenciamento são idênticas. Isso garante que seus dados de conhecimento e experiência de operação e gerenciamento de clusters de malha do serviço é transferível quando você escolhe tootarget novos ambientes de hospedagem.

### <a name="benefits-of-creating-standalone-service-fabric-clusters"></a>Benefícios de criar clusters autônomos do Service Fabric
* Você está livre toochoose qualquer nuvem provedor toohost seu cluster.
* Aplicativos do Service Fabric, gravados uma vez, podem ser executados em vários ambientes de hospedagem com alterações mínimas toono.
* Conhecimento da criação de aplicativos do Service Fabric traz de um tooanother de ambiente de hospedagem.
* Experiência operacional de execução e gerenciamento do Service Fabric clusters realiza failover de um ambiente tooanother.
* Amplo alcance de clientes, sem limitação de restrições de ambiente de hospedagem.
* Uma camada extra de proteção contra falhas generalizadas e confiabilidade existe porque você pode mover serviços Olá sobre o ambiente de implantação tooanother se um data center ou provedor de nuvem tem um blecaute.

## <a name="supported-operating-systems-for-standalone-clusters"></a>Sistemas operacionais com suporte para clusters autônomos
Você é capaz de toocreate clusters em máquinas virtuais ou computadores que executam esses sistemas operacionais:

* Windows Server 2012 R2
* Windows Server 2016 
* Linux (em breve)

## <a name="advantages-of-service-fabric-clusters-on-azure-over-standalone-service-fabric-clusters-created-on-premises"></a>Vantagens dos clusters do Service Fabric no Azure sobre os clusters autônomos do Service Fabric criados no local
Executar clusters de malha do serviço no Azure oferece vantagens em relação à opção de local de Olá, portanto, se você não tiver necessidades específicas de onde você executa os clusters, sugerimos que você execute no Azure. No Azure, fornecemos integração com outros serviços, o que torna as operações e o gerenciamento de cluster hello mais fácil e mais confiável e recursos do Azure.

* **Portal do Azure:** portal do Azure torna fácil toocreate e gerenciar clusters.
* **Gerenciador de recursos do Azure:** uso do Gerenciador de recursos do Azure permite o fácil gerenciamento de todos os recursos usados pelo cluster hello como uma unidade e simplifica o controle de custo e de cobrança.
* **Cluster do Service Fabric como um Recurso do Azure** : um cluster do Service Fabric é um recurso do ARM, portanto, você pode modelá-lo como faz com outros recursos do ARM no Azure.
* **Integração com a infraestrutura do Azure** Service Fabric coordena com hello subjacente a infraestrutura do Azure para o sistema operacional, rede e outros upgrades tooimprove disponibilidade e confiabilidade de seus aplicativos.  
* **Diagnóstico** : no Azure, fornecemos a integração no diagnóstico do Azure e no Log Analytics.
* **O dimensionamento automático:** para clusters no Azure, fornece a funcionalidade interna de dimensionamento automático devido a conjuntos de escala de máquinas de tooVirtual. No local e outros ambientes de nuvem, você tem toobuild seu próprio recurso ou escala manualmente usando Olá APIs que expõe Service Fabric para clusters de dimensionamento de dimensionamento automático.

## <a name="next-steps"></a>Próximas etapas

* Crie um cluster em VMs ou em computadores que estejam executando o Windows Server: [Criação de um cluster do Service Fabric para o Windows Server](service-fabric-cluster-creation-for-windows-server.md)
* Crie um cluster em VMs ou em computadores que estejam executando o Linux: [Service Fabric no Linux](service-fabric-linux-overview.md)
* Saiba mais sobre as [opções de suporte do Service Fabric](service-fabric-support.md)

