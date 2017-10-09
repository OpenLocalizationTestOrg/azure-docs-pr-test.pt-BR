---
title: "aaaAdd ou remover nós tooa autônomo serviço cluster do Fabric | Microsoft Docs"
description: "Saiba como tooadd ou remover nós tooan Azure Service Fabric do cluster em um computador físico ou virtual executando o Windows Server, que pode ser local ou em qualquer nuvem."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a>Adicionar ou remover nós tooa autônomo do Service Fabric cluster em execução no Windows Server
Depois de ter [criado o cluster do Service Fabric independentes em máquinas do Windows Server](service-fabric-cluster-creation-for-windows-server.md), suas necessidades de negócios podem ser alterados e, talvez você precise tooadd ou remover nós tooyour cluster. Este artigo fornece etapas detalhadas tooachieve isso. Observe que não há suporte para a funcionalidade de adicionar/remover nó em clusters de desenvolvimento local.

## <a name="add-nodes-tooyour-cluster"></a>Adicionar nós tooyour cluster
1. Preparar Olá VM/máquina que deseja tooadd tooyour cluster seguindo as etapas Olá mencionadas Olá [Olá preparar máquinas pré-requisitos do toomeet Olá para implantação de cluster](service-fabric-cluster-creation-for-windows-server.md) seção
2. Identificar qual domínio de falha e o domínio de atualização que você está indo tooadd dessa VM/máquina para
3. Área de trabalho remota (RDP) Olá VM/máquina que você deseja que o cluster de toohello tooadd
4. Copiar ou [baixar pacote autônomo de saudação de malha do serviço para o Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/máquina e descompacte o pacote de saudação
5. Execute o Powershell com privilégios elevados e navegue toohello local do pacote de saudação descompactado
6. Executar Olá *AddNode.ps1* script com os parâmetros de saudação descrevendo Olá novo nó tooadd. Olá exemplo a seguir adiciona um novo nó denominado VM5, com tipo NodeType0 e endereço IP 182.17.34.52, UD1 e fd: / dc1/r0. Olá *ExistingClusterConnectionEndPoint* já está um ponto de extremidade de conexão para um nó no cluster existente do hello, que pode ser um endereço IP de saudação do *qualquer* nó no cluster hello.

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    Depois que o script hello concluir a execução, você pode verificar se o novo nó de saudação foi adicionado executando Olá [ServiceFabricNode Get](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.

7. consistência de tooensure em diferentes nós de cluster hello, você deve iniciar uma atualização de configuração. Executar [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget Olá último arquivo de configuração e adicione Olá recém-adicionado nó muito seção "Nós". Também é recomendável tooalways ter Olá última configuração de cluster disponível no caso de Olá que você precisa tooredploy um cluster com hello mesma configuração.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. Executar [início ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin atualização de saudação.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    Você pode monitorar o progresso de saudação da atualização Olá no Gerenciador do Service Fabric. Como alternativa, você pode executar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a>Adicionar nós tooclusters configurado com a segurança do Windows usando a gMSA
Para clusters configurados com a Conta de Serviço Gerenciado de Grupo (gMSA) (https://technet.microsoft.com/library/hh831782.aspx), um novo nó pode ser adicionado usando uma atualização de configuração:
1. Executar [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) em qualquer um de nós existentes Olá tooget Olá último arquivo de configuração e adicionar detalhes sobre o novo nó de saudação você deseja tooadd na seção de nós"Olá". Verifique se o nó novo Olá faz parte da saudação mesma conta gerenciada de grupo. Essa conta deve ser um Administrador em todos os computadores.

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. Executar [início ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin atualização de saudação.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    Você pode monitorar o progresso de saudação da atualização Olá no Gerenciador do Service Fabric. Como alternativa, você pode executar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

### <a name="add-node-types-tooyour-cluster"></a>Adicionar nó tipos tooyour cluster
Ordenar tooadd um novo tipo de nó, modificar sua configuração tooinclude Olá novo tipo de nó na seção de "NodeTypes" em "Propriedades" e começar a uma configuração de atualização usando [ServiceFabricClusterConfigurationUpgrade início](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps). Depois de concluir a atualização Olá, você pode adicionar o novo cluster tooyour de nós com esse tipo de nó.

## <a name="remove-nodes-from-your-cluster"></a>Remover nós do cluster
Um nó pode ser removido de um cluster usando uma atualização de configuração, no hello maneira a seguir:

1. Executar [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) arquivo de configuração mais recente do tooget hello e *remover* nó Olá da seção "Nós".
Adicionar hello "NodesToBeRemoved" parâmetro muito "configurar" seção na seção "FabricSettings". Olá "valor" deve ser uma lista separada por vírgulas de nomes de nó de nós que precisam toobe removido.

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. Executar [início ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin atualização de saudação.

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    Você pode monitorar o progresso de saudação da atualização Olá no Gerenciador do Service Fabric. Como alternativa, você pode executar [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)

> [!NOTE]
> A remoção de nós pode iniciar várias atualizações. Alguns nós são marcados com `IsSeedNode=”true”` marca e podem ser identificados consultando cluster Olá manifesto usando `Get-ServiceFabricClusterManifest`. Remoção de tais nós pode levar mais tempo do que outros, como nós de propagação Olá terá toobe movido nesses cenários. cluster Olá deve manter um mínimo de 3 nós de tipo de nó primário.
> 
> 

### <a name="remove-node-types-from-your-cluster"></a>Remover tipos de nó do cluster
Antes de remover um tipo de nó, verifique se há quaisquer nós fazendo referência ao tipo de nó de saudação. Remova esses nós antes de remover o tipo de nó correspondente hello. Depois que todos os nós correspondentes são removidos, você pode remover o Olá NodeType de configuração de cluster de saudação e começar a uma configuração de atualização usando [ServiceFabricClusterConfigurationUpgrade início](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).


### <a name="replace-primary-nodes-of-your-cluster"></a>Substituir nós primários de seu cluster
substituição de saudação de nós primários deve ser executada de um nó após o outro, em vez de remover e, em seguida, adicionar em lotes.


## <a name="next-steps"></a>Próximas etapas
* [Definições de configuração para o cluster autônomo no Windows](service-fabric-cluster-manifest.md)
* [Proteger um cluster autônomo no Windows usando os certificados X509](service-fabric-windows-cluster-x509-security.md)
* [Criar um cluster do Service Fabric autônomo com VMs do Azure executando o Windows](service-fabric-cluster-creation-with-windows-azure-vms.md)

