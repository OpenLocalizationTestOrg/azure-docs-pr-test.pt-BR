---
title: aaaCreate independente do cluster com VMs do Azure que executam o Windows | Microsoft Docs
description: "Saiba como toocreate e gerenciar um cluster do Azure Service Fabric em máquinas virtuais do Azure executando o Windows Server."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a>Criar um cluster do Service Fabric autônomo com três nós e com máquinas virtuais do Azure executando o Windows Server
Este artigo descreve como toocreate um cluster baseado no Windows Azure (máquinas virtuais), usando Olá instalador autônomo do Service Fabric para Windows Server. cenário de saudação é um caso especial de [criar e gerenciar um cluster executando o Windows Server](service-fabric-cluster-creation-for-windows-server.md) onde Olá VMs são [VMs do Azure executando o Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), no entanto, você está criando não [um Azure cluster de malha do serviço baseado em nuvem](service-fabric-cluster-creation-via-portal.md). distinção de saudação seguir esse padrão é esse cluster de malha do serviço de autônomo Olá criado pelo Olá etapas a seguir é totalmente gerenciada por você, enquanto Olá clusters de malha de serviço baseado em nuvem do Azure são gerenciadas e atualizada pelo Olá Service Fabric provedor de recursos.

## <a name="steps-toocreate-hello-standalone-cluster"></a>Cluster do etapas toocreate Olá autônomo
1. Entre em toohello portal do Azure e criar um novo Windows Server 2012 R2 Datacenter ou VM de Datacenter do Windows Server 2016 em um grupo de recursos. Leia o artigo Olá [criar uma VM do Windows no portal do Azure de saudação](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter mais detalhes.
2. Adicionar duas mais toohello de VMs mesmo grupo de recursos. Certifique-se de que cada uma das VMs de saudação tem Olá mesmo nome de usuário administrador e senha quando criado. Uma vez criado, você deve ver todas as três VMs em hello mesma rede virtual.
3. Conecte-se tooeach de saudação VMs e desativar o Firewall do Windows usando Olá Olá [Gerenciador do servidor, o painel do servidor Local](https://technet.microsoft.com/library/jj134147.aspx). Isso garante que o tráfego de rede Olá pode se comunicar entre as máquinas de saudação. Enquanto conectado tooeach máquina, obter o endereço IP de saudação abrindo um prompt de comando e digitando `ipconfig`. Como alternativa, você pode ver Olá IP endereço de cada máquina no portal de hello, selecionando o recurso de rede virtual Olá Olá para grupo de recursos e verificando as interfaces de rede Olá criados para cada uma dessas máquinas.
4. Conecte-se tooone de saudação VMs e teste que você pode executar ping Olá outras duas VMs com êxito.
5. Conectar-se tooone de saudação VMs e [baixar o pacote de malha do serviço de autônomo de saudação para o Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) para uma nova pasta no hello máquina e extraia o pacote de saudação.
6. Olá abrir *ClusterConfig.Unsecure.MultiMachine.json* arquivo no bloco de notas e editar cada nó com endereços IP hello três máquinas hello. Alterar nome de cluster Olá na parte superior do hello e salve o arquivo hello.  Um exemplo parcial saudação do manifesto de cluster é mostrado abaixo.
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. Se você pretende este toobe um cluster seguro, decidir medidas de segurança Olá deseja toouse e siga as etapas de saudação em hello associados link: [certificado X509](service-fabric-windows-cluster-x509-security.md) ou [a segurança do Windows](service-fabric-windows-cluster-windows-security.md). Se a configuração de cluster hello usando a segurança do Windows, você precisará tooset a um toomanage de controlador de domínio do Active Directory. Observe que não há suporte para o uso de um computador controlador de domínio como um nó do Service Fabric.
8. Abra uma [janela do ISE do PowerShell](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise). Navegue toohello pasta onde você extraiu o pacote do instalador autônomo baixado hello e salva o arquivo de configuração de cluster de saudação. Execute Olá cluster de saudação de toodeploy de comando do PowerShell a seguir:
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

script Hello remotamente irá configurar o cluster do Service Fabric hello e deve relatar o andamento como implantação passa por.

9. Depois de cerca de um minuto, você pode verificar se o cluster de saudação está operacional por meio da conexão toohello usando um IP da máquina de saudação do Service Fabric Explorer endereços, por exemplo, usando `http://10.1.0.5:19080/Explorer/index.html`. 

## <a name="next-steps"></a>Próximas etapas
* [Criar clusters autônomos do Service Fabric no Windows Server ou Linux](service-fabric-deploy-anywhere.md)
* [Adicionar ou remover nós tooa autônomo do Service Fabric cluster](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Definições de configuração para o cluster autônomo no Windows](service-fabric-cluster-manifest.md)
* [Proteger um cluster autônomo no Windows usando a segurança](service-fabric-windows-cluster-windows-security.md)
* [Proteger um cluster autônomo no Windows usando os certificados X509](service-fabric-windows-cluster-x509-security.md)

