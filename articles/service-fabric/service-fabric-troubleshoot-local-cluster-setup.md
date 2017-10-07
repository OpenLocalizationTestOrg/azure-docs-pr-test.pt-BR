---
title: "aaaTroubleshoot sua instalação local do cluster do Service Fabric | Microsoft Docs"
description: "Este artigo aborda um conjunto de sugestões para a solução de problemas do cluster de desenvolvimento local"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a>Solucionar problemas de configuração do cluster de desenvolvimento local
Se você encontrar um problema ao interagir com o cluster de desenvolvimento local do Azure Service Fabric, examine Olá sugestões para possíveis soluções a seguir.

## <a name="cluster-setup-failures"></a>Falhas de configuração do cluster
### <a name="cannot-clean-up-service-fabric-logs"></a>Não é possível limpar os logs da Malha do Serviço
#### <a name="problem"></a>Problema
Ao executar o script de DevClusterSetup hello, você vir um erro como este:

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a>Solução
Feche Olá janela atual do PowerShell e abra uma nova janela do PowerShell como administrador. Agora você deve ser capaz de toosuccessfully executar script hello.

## <a name="cluster-connection-failures"></a>Falhas de conexão do cluster
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a>Cmdlets do PowerShell do Service Fabric não são reconhecidos no Azure PowerShell
#### <a name="problem"></a>Problema
Se você tentar toorun qualquer Olá cmdlets do PowerShell de malha do serviço, como `Connect-ServiceFabricCluster` em uma janela do PowerShell do Azure, ele falhar, indicando que esse cmdlet Olá não é reconhecido. motivo Olá para isso é que PowerShell do Azure usa a versão de 32 bits de saudação do Windows PowerShell (mesmo em versões de sistema operacional de 64 bits), enquanto Olá cmdlets do Service Fabric só funcionam em ambientes de 64 bits.

#### <a name="solution"></a>Solução
Sempre execute os cmdlets do Service Fabric diretamente do Windows PowerShell.

> [!NOTE]
> versão mais recente de saudação do PowerShell do Azure não cria um atalho especial, para que isso não deve ocorrer.
> 
> 

### <a name="type-initialization-exception"></a>Exceção de Inicialização de Tipo
#### <a name="problem"></a>Problema
Quando você se conectar a cluster toohello no PowerShell, você verá o erro Olá TypeInitializationException para System.Fabric.Common.AppTrace.

#### <a name="solution"></a>Solução
A variável do caminho não foi definida corretamente durante a instalação. Saia do Windows e entre novamente. Isso atualiza o caminho.

### <a name="cluster-connection-fails-with-object-is-closed"></a>Falha de conexão do cluster com “O objeto está fechado”
#### <a name="problem"></a>Problema
Uma chamada tooConnect-ServiceFabricCluster falhará com um erro como este:

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a>Solução
Feche Olá janela atual do PowerShell e abra uma nova janela do PowerShell como administrador. Agora você deve ser capaz de conectar-se toosuccessfully.

### <a name="fabric-connection-denied-exception"></a>Exceção de Conexão ao Fabric Negada
#### <a name="problem"></a>Problema
Ao depurar no Visual Studio, você obtém um erro FabricConnectionDeniedException.

#### <a name="solution"></a>Solução
Esse erro normalmente ocorre quando você tentar toostart um processo de host de serviço manualmente, em vez de permitir toostart de tempo de execução do Service Fabric Olá para você.

Verifique se você não possui um projeto de serviço definido como projeto de inicialização na sua solução. Somente projetos de aplicativo da Malha do Serviço devem ser definidos como projetos de inicialização.

> [!TIP]
> Se, após a instalação, o cluster local começa toobehave anormal, você poderá redefini-lo usando o aplicativo de bandeja de sistema do hello cluster local manager. Isso remove Olá cluster existente e configure um novo. Observe que todos os aplicativos implantados e os dados associados são removidos.
> 
> 

## <a name="next-steps"></a>Próximas etapas
* [Entender e solucionar problemas de cluster com relatórios de integridade do sistema](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [Visualizando o cluster com o Explorador do Service Fabric](service-fabric-visualizing-your-cluster.md)

