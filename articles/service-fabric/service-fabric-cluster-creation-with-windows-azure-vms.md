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
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="747a5-103">Criar um cluster do Service Fabric autônomo com três nós e com máquinas virtuais do Azure executando o Windows Server</span><span class="sxs-lookup"><span data-stu-id="747a5-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="747a5-104">Este artigo descreve como toocreate um cluster baseado no Windows Azure (máquinas virtuais), usando Olá instalador autônomo do Service Fabric para Windows Server.</span><span class="sxs-lookup"><span data-stu-id="747a5-104">This article describes how toocreate a cluster on Windows-based Azure virtual machines (VMs), using hello standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="747a5-105">cenário de saudação é um caso especial de [criar e gerenciar um cluster executando o Windows Server](service-fabric-cluster-creation-for-windows-server.md) onde Olá VMs são [VMs do Azure executando o Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), no entanto, você está criando não [um Azure cluster de malha do serviço baseado em nuvem](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="747a5-105">hello scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where hello VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="747a5-106">distinção de saudação seguir esse padrão é esse cluster de malha do serviço de autônomo Olá criado pelo Olá etapas a seguir é totalmente gerenciada por você, enquanto Olá clusters de malha de serviço baseado em nuvem do Azure são gerenciadas e atualizada pelo Olá Service Fabric provedor de recursos.</span><span class="sxs-lookup"><span data-stu-id="747a5-106">hello distinction in following this pattern is that hello standalone Service Fabric cluster created by hello following steps is entirely managed by you, whereas hello Azure cloud-based Service Fabric clusters are managed and upgraded by hello Service Fabric resource provider.</span></span>

## <a name="steps-toocreate-hello-standalone-cluster"></a><span data-ttu-id="747a5-107">Cluster do etapas toocreate Olá autônomo</span><span class="sxs-lookup"><span data-stu-id="747a5-107">Steps toocreate hello standalone cluster</span></span>
1. <span data-ttu-id="747a5-108">Entre em toohello portal do Azure e criar um novo Windows Server 2012 R2 Datacenter ou VM de Datacenter do Windows Server 2016 em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="747a5-108">Sign in toohello Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="747a5-109">Leia o artigo Olá [criar uma VM do Windows no portal do Azure de saudação](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="747a5-109">Read hello article [Create a Windows VM in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="747a5-110">Adicionar duas mais toohello de VMs mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="747a5-110">Add a couple more VMs toohello same resource group.</span></span> <span data-ttu-id="747a5-111">Certifique-se de que cada uma das VMs de saudação tem Olá mesmo nome de usuário administrador e senha quando criado.</span><span class="sxs-lookup"><span data-stu-id="747a5-111">Ensure that each of hello VMs has hello same administrator user name and password when created.</span></span> <span data-ttu-id="747a5-112">Uma vez criado, você deve ver todas as três VMs em hello mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="747a5-112">Once created you should see all three VMs in hello same virtual network.</span></span>
3. <span data-ttu-id="747a5-113">Conecte-se tooeach de saudação VMs e desativar o Firewall do Windows usando Olá Olá [Gerenciador do servidor, o painel do servidor Local](https://technet.microsoft.com/library/jj134147.aspx).</span><span class="sxs-lookup"><span data-stu-id="747a5-113">Connect tooeach of hello VMs and turn off hello Windows Firewall using hello [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="747a5-114">Isso garante que o tráfego de rede Olá pode se comunicar entre as máquinas de saudação.</span><span class="sxs-lookup"><span data-stu-id="747a5-114">This ensures that hello network traffic can communicate between hello machines.</span></span> <span data-ttu-id="747a5-115">Enquanto conectado tooeach máquina, obter o endereço IP de saudação abrindo um prompt de comando e digitando `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="747a5-115">While connected tooeach machine, get hello IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="747a5-116">Como alternativa, você pode ver Olá IP endereço de cada máquina no portal de hello, selecionando o recurso de rede virtual Olá Olá para grupo de recursos e verificando as interfaces de rede Olá criados para cada uma dessas máquinas.</span><span class="sxs-lookup"><span data-stu-id="747a5-116">Alternatively you can see hello IP address of each machine on hello portal, by selecting hello virtual network resource for hello resource group and checking hello network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="747a5-117">Conecte-se tooone de saudação VMs e teste que você pode executar ping Olá outras duas VMs com êxito.</span><span class="sxs-lookup"><span data-stu-id="747a5-117">Connect tooone of hello VMs and test that you can ping hello other two VMs successfully.</span></span>
5. <span data-ttu-id="747a5-118">Conectar-se tooone de saudação VMs e [baixar o pacote de malha do serviço de autônomo de saudação para o Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) para uma nova pasta no hello máquina e extraia o pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="747a5-118">Connect tooone of hello VMs and [download hello standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on hello machine and extract hello package.</span></span>
6. <span data-ttu-id="747a5-119">Olá abrir *ClusterConfig.Unsecure.MultiMachine.json* arquivo no bloco de notas e editar cada nó com endereços IP hello três máquinas hello.</span><span class="sxs-lookup"><span data-stu-id="747a5-119">Open hello *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with hello three IP addresses of hello machines.</span></span> <span data-ttu-id="747a5-120">Alterar nome de cluster Olá na parte superior do hello e salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="747a5-120">Change hello cluster name at hello top and save hello file.</span></span>  <span data-ttu-id="747a5-121">Um exemplo parcial saudação do manifesto de cluster é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="747a5-121">A partial example of hello cluster manifest is shown below.</span></span>
   
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
7. <span data-ttu-id="747a5-122">Se você pretende este toobe um cluster seguro, decidir medidas de segurança Olá deseja toouse e siga as etapas de saudação em hello associados link: [certificado X509](service-fabric-windows-cluster-x509-security.md) ou [a segurança do Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="747a5-122">If you intend this toobe a secure cluster, decide hello security measure you would like toouse and follow hello steps at hello associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="747a5-123">Se a configuração de cluster hello usando a segurança do Windows, você precisará tooset a um toomanage de controlador de domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="747a5-123">If setting up hello cluster using Windows Security, you will need tooset up a domain controller toomanage Active Directory.</span></span> <span data-ttu-id="747a5-124">Observe que não há suporte para o uso de um computador controlador de domínio como um nó do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="747a5-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="747a5-125">Abra uma [janela do ISE do PowerShell](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span><span class="sxs-lookup"><span data-stu-id="747a5-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="747a5-126">Navegue toohello pasta onde você extraiu o pacote do instalador autônomo baixado hello e salva o arquivo de configuração de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="747a5-126">Navigate toohello folder where you extracted hello downloaded standalone installer package and saved hello cluster configuration file.</span></span> <span data-ttu-id="747a5-127">Execute Olá cluster de saudação de toodeploy de comando do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="747a5-127">Run hello following PowerShell command toodeploy hello cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="747a5-128">script Hello remotamente irá configurar o cluster do Service Fabric hello e deve relatar o andamento como implantação passa por.</span><span class="sxs-lookup"><span data-stu-id="747a5-128">hello script will remotely configure hello Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="747a5-129">Depois de cerca de um minuto, você pode verificar se o cluster de saudação está operacional por meio da conexão toohello usando um IP da máquina de saudação do Service Fabric Explorer endereços, por exemplo, usando `http://10.1.0.5:19080/Explorer/index.html`.</span><span class="sxs-lookup"><span data-stu-id="747a5-129">After about a minute, you can check if hello cluster is operational by connecting toohello Service Fabric Explorer using one of hello machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="747a5-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="747a5-130">Next steps</span></span>
* [<span data-ttu-id="747a5-131">Criar clusters autônomos do Service Fabric no Windows Server ou Linux</span><span class="sxs-lookup"><span data-stu-id="747a5-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="747a5-132">Adicionar ou remover nós tooa autônomo do Service Fabric cluster</span><span class="sxs-lookup"><span data-stu-id="747a5-132">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="747a5-133">Definições de configuração para o cluster autônomo no Windows</span><span class="sxs-lookup"><span data-stu-id="747a5-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="747a5-134">Proteger um cluster autônomo no Windows usando a segurança</span><span class="sxs-lookup"><span data-stu-id="747a5-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="747a5-135">Proteger um cluster autônomo no Windows usando os certificados X509</span><span class="sxs-lookup"><span data-stu-id="747a5-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

