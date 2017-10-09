---
title: "aaaAzure pacote autônomo do Service Fabric para o Windows Server | Microsoft Docs"
description: "Descrição e o conteúdo do pacote do Azure Service Fabric autônomo Olá para o Windows Server."
services: service-fabric
documentationcenter: .net
author: maburlik
manager: timlt
editor: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik
ms.openlocfilehash: e4c6cb9128d659144e559fcad06bb78c9969dd60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="contents-of-service-fabric-standalone-package-for-windows-server"></a>Conteúdo do pacote Autônomo do Service Fabric para Windows Server
Em Olá [baixado](http://go.microsoft.com/fwlink/?LinkId=730690) pacote autônomo de malha do serviço, você encontrará Olá seguintes arquivos:

| **Nome do arquivo** | **Descrição breve** |
| --- | --- |
| CreateServiceFabricCluster.ps1 |Um script do PowerShell que cria o cluster de hello usando configurações de saudação em Clusterconfig. |
| RemoveServiceFabricCluster.ps1 |Um script do PowerShell que remove um cluster usando as configurações de saudação em Clusterconfig. |
| AddNode.ps1 |Um script do PowerShell para adicionar um existente do nó tooan implantado cluster na máquina atual hello. |
| RemoveNode.ps1 |Um script do PowerShell para remover um nó de um existente implantado cluster do computador atual hello. |
| CleanFabric.ps1 |Um script do PowerShell para limpeza de uma instalação do Service Fabric máquina atual Olá autônoma. As instalações anteriores do MSI devem ser removidas usando seus próprios desinstaladores associados. |
| TestConfiguration.ps1 |Um script do PowerShell para analisar infraestrutura Olá conforme especificado no hello Cluster.json. |
| DownloadServiceFabricRuntimePackage.ps1 |Um script do PowerShell usado para baixar o pacote de tempo de execução mais recente Olá fora da banda, para cenários onde Olá implantando a máquina não está conectado toohello internet. |
| DeploymentComponentsAutoextractor.exe |Arquivo que contém os componentes de implantação de extração automática usada pelo Olá scripts do pacote autônomo. |
| EULA_ENU.txt |usam termos de licença de saudação de saudação do pacote do Microsoft Azure Service Fabric autônomo do Windows Server. Você pode [baixar uma cópia do EULA da saudação](http://go.microsoft.com/fwlink/?LinkID=733084) agora. |
| Readme. txt |Um link toohello notas de versão e instruções básicas de instalação. É um subconjunto de instruções Olá neste documento. |
| ThirdPartyNotice.rtf |Aviso de software de terceiros que está no pacote de saudação. |
| Tools\Microsoft.Azure.ServiceFabric.WindowsServer.SupportPackage.zip |StandaloneLogCollector.exe que é executado em um rastreamento de demanda toocollect e carregar logs tooMicrosoft para finalidade de suporte. |
| Tools\ServiceFabricUpdateService.zip |Uma ferramenta usada a atualização automática código tooenable para clusters que não têm acesso à internet. Encontre mais detalhes [aqui](service-fabric-cluster-upgrade-windows-server.md)|

**Modelos** 
| **Nome do arquivo** | **Descrição breve** |
| --- | --- |
| ClusterConfig.Unsecure.DevCluster.json |Um arquivo de exemplo de configuração de cluster que contém as configurações de saudação para um não segura, três nós, computador único (ou máquina virtual) cluster de desenvolvimento, incluindo informações de saudação para cada nó no cluster hello. |
| ClusterConfig.Unsecure.MultiMachine.json |Um arquivo de exemplo de configuração de cluster que contém as configurações de saudação para um cluster não segura, com vários computadores (ou máquina virtual), incluindo informações de saudação para cada máquina no cluster hello. |
| ClusterConfig.Windows.DevCluster.json |Um arquivo de exemplo de configuração de cluster que contém todos os cluster de desenvolvimento configurações de um computador único seguro e três nós (ou máquina virtual) hello, incluindo informações de saudação para cada nó no cluster hello. cluster de saudação é protegida usando [identidades do Windows](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.Windows.MultiMachine.json |Um arquivo de exemplo de configuração de cluster que contém todas as configurações de saudação para um cluster de vários computadores (ou máquina virtual) segura, usando a segurança do Windows, incluindo informações de saudação para cada máquina que estiver em cluster seguro hello. cluster de saudação é protegida usando [identidades do Windows](https://msdn.microsoft.com/library/ff649396.aspx). |
| ClusterConfig.x509.DevCluster.json |Um arquivo de exemplo de configuração de cluster que contém todas as configurações de saudação para um seguro, três nós, computador único (ou máquina virtual) cluster de desenvolvimento, incluindo informações de saudação para cada nó no cluster hello. Olá cluster é protegido usando x509 certificados. |
| ClusterConfig.x509.MultiMachine.json |Proteger um arquivo de exemplo de configuração de cluster que contém todas as configurações de saudação do hello, cluster com vários computadores (ou máquina virtual), incluindo informações de saudação para cada nó no cluster seguro hello. Olá cluster é protegido usando x509 certificados. |
| ClusterConfig.gMSA.Windows.MultiMachine.json |Proteger um arquivo de exemplo de configuração de cluster que contém todas as configurações de saudação do hello, cluster com vários computadores (ou máquina virtual), incluindo informações de saudação para cada nó no cluster seguro hello. Olá cluster é protegido usando [contas de serviço gerenciado do grupo](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11).aspx). |

## <a name="cluster-configuration-samples"></a>Exemplos da configuração do cluster
Versões mais recentes dos modelos de configuração de cluster podem ser encontradas na página do GitHub de saudação: [autônomo exemplos de configuração de Cluster](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).

## <a name="independent-runtime-package"></a>Pacote de Tempo de Execução Independente
pacote de tempo de execução mais recente da saudação é baixado automaticamente durante a implantação de cluster de [o Link de Download - tempo de execução do serviço de malha - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).

## <a name="related"></a>Relacionados
* [Criar um cluster autônomo do Azure Service Fabric](service-fabric-cluster-creation-for-windows-server.md)
* [Cenários de segurança do cluster do Service Fabric](service-fabric-windows-cluster-windows-security.md)
