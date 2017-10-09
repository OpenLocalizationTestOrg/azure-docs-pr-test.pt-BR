---
title: "aaaSet um cluster do Azure Service Fabric autônomo | Microsoft Docs"
description: "Criar um cluster de autônomo de desenvolvimento com três nós em execução no hello mesmo computador. Depois de concluir esta instalação, você será toocreate pronto um cluster com vários computador."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: e4d0ea9fc3b8475160bd8ed19fd3716463791cc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a>Criar seu primeiro cluster autônomo do Service Fabric
Você pode criar um cluster do Service Fabric independentes em quaisquer máquinas virtuais ou computadores que executam o Windows Server 2012 R2 ou Windows Server 2016, local ou na nuvem hello. Este guia de início rápido ajuda toocreate um cluster de desenvolvimento autônomo em apenas alguns minutos.  Quando terminar, você terá um cluster de três nós em execução em um único computador no qual poderá implantar aplicativos.

## <a name="before-you-begin"></a>Antes de começar
Malha do serviço fornece uma configuração de pacote toocreate Service Fabric autônomo clusters.  [Baixar o pacote de instalação Olá](http://go.microsoft.com/fwlink/?LinkId=730690).  Descompacte Olá pacote tooa pasta de instalação no computador de saudação ou máquina virtual em que você estiver configurando o cluster de desenvolvimento de saudação.  conteúdo Olá Olá do pacote de instalação é descrito em detalhes [aqui](service-fabric-cluster-standalone-package-contents.md).

administrador de cluster Olá implantar e configurar o cluster Olá deve ter privilégios de administrador no computador de saudação. Você não pode instalar o Service Fabric em um controlador de domínio.

## <a name="validate-hello-environment"></a>Validar o ambiente de saudação
Olá *TestConfiguration.ps1* script no pacote autônomo de saudação é usado como um toovalidate de analisador de práticas recomendada, se um cluster pode ser implantado em um ambiente específico. [Preparação de implantação](service-fabric-cluster-standalone-deployment-preparation.md) listas Olá pré-requisitos e requisitos do ambiente. Execute Olá script tooverify se você pode criar o cluster de desenvolvimento hello:

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-hello-cluster"></a>Criar cluster Olá
Vários arquivos de configuração de cluster de exemplo são instalados com o pacote de instalação hello. *ClusterConfig.Unsecure.DevCluster.json* é a configuração mais simples de cluster Olá: um cluster não seguro, três nós em execução em um único computador.  Outros arquivos de configuração descrevem clusters únicos ou vários computadores protegidos com certificados x. 509 ou com a segurança do Windows.  Desnecessários toomodify qualquer uma das definições de configuração saudação padrão para este tutorial, mas examine o arquivo de configuração de saudação e se familiarizar com as configurações de saudação.  Olá **nós** seção descreve três nós de cluster Olá Olá: nome, endereço IP, [tipo de nó, o domínio de falha e o domínio de atualização](service-fabric-cluster-manifest.md#nodes-on-the-cluster).  Olá **propriedades** seção define Olá [segurança, nível de confiabilidade, coleta de diagnósticos e tipos de nós](service-fabric-cluster-manifest.md#cluster-properties) para cluster hello.

Esse cluster não é seguro.  Qualquer pessoa pode conectar-se anonimamente e realizar operações de gerenciamento, portanto, os clusters de produção sempre devem ser protegidos usando os certificados x.509 ou a segurança do Windows.  Segurança somente é configurada no momento da criação de cluster e não é possível tooenable segurança depois Olá cluster é criado.  Leitura [proteger um cluster](service-fabric-cluster-security.md) toolearn mais sobre a segurança de cluster do Service Fabric.  

cluster de desenvolvimento de três nós Olá toocreate, execute Olá *CreateServiceFabricCluster.ps1* script a partir de uma sessão do PowerShell de administrador:

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

pacote de tempo de execução do Service Fabric Olá automaticamente é baixado e instalado no momento da criação do cluster.

## <a name="connect-toohello-cluster"></a>Conecte-se o cluster toohello
O cluster de desenvolvimento de três nós agora está em execução. Olá módulo ServiceFabric do PowerShell é instalado com o tempo de execução de saudação.  Você pode verificar esse cluster hello está em execução de saudação mesmo computador ou em um computador remoto com o tempo de execução do hello Service Fabric.  Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet estabelece um cluster de toohello de conexão.   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
Consulte [conectar tooa segura cluster](service-fabric-connect-to-secure-cluster.md) para obter outros exemplos de cluster de tooa conexão. Depois de cluster toohello conexão, use Olá [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) toodisplay cmdlet uma lista de nós no hello cluster e informações de status para cada nó. **HealthState** deve ser *OK* para cada nó.

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-hello-cluster-using-service-fabric-explorer"></a>Visualizar cluster hello usando o Gerenciador do Service Fabric
O [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) é uma boa ferramenta para visualizar o cluster e gerenciar os aplicativos.  Gerenciador do Service Fabric é um serviço que é executado no cluster hello, que você acessa usando um navegador, navegando muito[http://localhost:19080/Explorer](http://localhost:19080/Explorer). 

painel do cluster Olá fornece uma visão geral do cluster, incluindo um resumo do aplicativo e a integridade do nó. exibição do nó de saudação mostra o layout físico de saudação do cluster hello. Para um nó específico, você pode inspecionar quais aplicativos têm código implantado naquele nó.

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-hello-cluster"></a>Remover cluster Olá
tooremove um cluster, execute Olá *RemoveServiceFabricCluster.ps1* script do PowerShell na pasta de pacote de saudação e passe o arquivo de configuração do hello caminho toohello JSON. Opcionalmente, você pode especificar um local para o log de saudação de exclusão de saudação.

```powershell
# Removes Service Fabric cluster nodes from each computer in hello configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

Olá tooremove Service Fabric tempo de execução do computador de hello, execute o script do PowerShell a seguir saudação da pasta do pacote de saudação.

```powershell
# Removes Service Fabric from hello current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a>Próximas etapas
Agora que você configurou um cluster de desenvolvimento autônomo, tente Olá artigos a seguir:
* [Configurar um cluster de vários computadores autônomos](service-fabric-cluster-creation-for-windows-server.md) e habilitar a segurança.
* [Implantar aplicativos usando o PowerShell](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
