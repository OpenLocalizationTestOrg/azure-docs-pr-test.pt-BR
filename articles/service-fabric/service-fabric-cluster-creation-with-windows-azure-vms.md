---
title: "Criar um cluster autônomo com VMs do Azure executando o Windows | Microsoft Docs"
description: "Saiba como criar e gerenciar um cluster do Azure Service Fabric nas máquinas virtuais do Azure executando o Windows Server."
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
ms.openlocfilehash: f8a0305a22c00f9bdbdb1bdb06dc299cccee23dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a><span data-ttu-id="e4dfb-103">Criar um cluster do Service Fabric autônomo com três nós e com máquinas virtuais do Azure executando o Windows Server</span><span class="sxs-lookup"><span data-stu-id="e4dfb-103">Create a three node standalone Service Fabric cluster with Azure virtual machines running Windows Server</span></span>
<span data-ttu-id="e4dfb-104">Este artigo descreve como criar um cluster nas máquinas virtuais (VMs) do Azure baseadas no Windows usando o instalador autônomo do Service Fabric para o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-104">This article describes how to create a cluster on Windows-based Azure virtual machines (VMs), using the standalone Service Fabric installer for Windows Server.</span></span> <span data-ttu-id="e4dfb-105">O cenário é um caso especial de [Criar e gerenciar um cluster em execução no Windows Server](service-fabric-cluster-creation-for-windows-server.md) em que as VMs são [VMs do Azure executando o Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), no entanto, você não está criando [um cluster do Service Fabric baseado em nuvem do Azure](service-fabric-cluster-creation-via-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e4dfb-105">The scenario is a special case of [Create and manage a cluster running on Windows Server](service-fabric-cluster-creation-for-windows-server.md) where the VMs are [Azure VMs running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), however you are not creating [an Azure cloud-based Service Fabric cluster](service-fabric-cluster-creation-via-portal.md).</span></span> <span data-ttu-id="e4dfb-106">A diferença em seguir este padrão é que o cluster do Service Fabric autônomo criado pelas seguintes etapas é totalmente gerenciado por você, enquanto que os clusters do Service Fabric baseados em nuvem do Azure são gerenciados e atualizados pelo provedor de recursos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-106">The distinction in following this pattern is that the standalone Service Fabric cluster created by the following steps is entirely managed by you, whereas the Azure cloud-based Service Fabric clusters are managed and upgraded by the Service Fabric resource provider.</span></span>

## <a name="steps-to-create-the-standalone-cluster"></a><span data-ttu-id="e4dfb-107">Etapas para criar o cluster autônomo</span><span class="sxs-lookup"><span data-stu-id="e4dfb-107">Steps to create the standalone cluster</span></span>
1. <span data-ttu-id="e4dfb-108">Entre no Portal do Azure e crie uma nova VM do Windows Server 2012 R2 Datacenter ou do Windows Server 2016 Datacenter em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-108">Sign in to the Azure portal and create a new Windows Server 2012 R2 Datacenter or Windows Server 2016 Datacenter VM in a resource group.</span></span> <span data-ttu-id="e4dfb-109">Leia o artigo [Criar uma VM do Windows no Portal do Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-109">Read the article [Create a Windows VM in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for more details.</span></span>
2. <span data-ttu-id="e4dfb-110">Adicione mais algumas VMs ao mesmo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-110">Add a couple more VMs to the same resource group.</span></span> <span data-ttu-id="e4dfb-111">Verifique se cada uma das VMs tem o mesmo nome de usuário e senha do administrador quando criadas.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-111">Ensure that each of the VMs has the same administrator user name and password when created.</span></span> <span data-ttu-id="e4dfb-112">Uma vez criadas, você deve ver as três VMs na mesma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-112">Once created you should see all three VMs in the same virtual network.</span></span>
3. <span data-ttu-id="e4dfb-113">Conecte cada uma das VMs e desative o Firewall do Windows usando o [painel Gerenciador de Servidores, Servidor Local](https://technet.microsoft.com/library/jj134147.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4dfb-113">Connect to each of the VMs and turn off the Windows Firewall using the [Server Manager, Local Server dashboard](https://technet.microsoft.com/library/jj134147.aspx).</span></span> <span data-ttu-id="e4dfb-114">Isso faz com que o tráfego de rede possa comunicar-se entre os computadores.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-114">This ensures that the network traffic can communicate between the machines.</span></span> <span data-ttu-id="e4dfb-115">Ainda conectado a cada máquina, obtenha o endereço IP abrindo um prompt de comando e digitando `ipconfig`.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-115">While connected to each machine, get the IP address by opening a command prompt and typing `ipconfig`.</span></span> <span data-ttu-id="e4dfb-116">Como alternativa, você pode ver o endereço IP de cada computador no portal selecionando o recurso de rede virtual do grupo de recursos e verificando os adaptadores de rede criados para cada um desses computadores.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-116">Alternatively you can see the IP address of each machine on the portal, by selecting the virtual network resource for the resource group and checking the network interfaces created for each of these machines.</span></span>
4. <span data-ttu-id="e4dfb-117">Conecte uma das VMs e teste se você pode executar o ping nas duas outras VMs com êxito.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-117">Connect to one of the VMs and test that you can ping the other two VMs successfully.</span></span>
5. <span data-ttu-id="e4dfb-118">Conecte uma das VMs, [baixe o pacote do Service Fabric autônomo para Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) em uma nova pasta no computador e extrair o pacote.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-118">Connect to one of the VMs and [download the standalone Service Fabric package for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) into a new folder on the machine and extract the package.</span></span>
6. <span data-ttu-id="e4dfb-119">Abra o arquivo *ClusterConfig.Unsecure.MultiMachine.json* no Bloco de Notas e edite cada nó com os três endereços IP das máquinas.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-119">Open the *ClusterConfig.Unsecure.MultiMachine.json* file in Notepad and edit each node with the three IP addresses of the machines.</span></span> <span data-ttu-id="e4dfb-120">Mude o nome do cluster na parte superior e salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-120">Change the cluster name at the top and save the file.</span></span>  <span data-ttu-id="e4dfb-121">Um exemplo parcial do manifesto do cluster é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-121">A partial example of the cluster manifest is shown below.</span></span>
   
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
7. <span data-ttu-id="e4dfb-122">Se você pretende que isso seja um cluster seguro, decida a medida de segurança que você gostaria de usar e execute as etapas no link associado: [Certificado X509](service-fabric-windows-cluster-x509-security.md) ou [Segurança do Windows](service-fabric-windows-cluster-windows-security.md).</span><span class="sxs-lookup"><span data-stu-id="e4dfb-122">If you intend this to be a secure cluster, decide the security measure you would like to use and follow the steps at the associated link: [X509 Certificate](service-fabric-windows-cluster-x509-security.md) or [Windows Security](service-fabric-windows-cluster-windows-security.md).</span></span> <span data-ttu-id="e4dfb-123">Se estiver configurando o cluster usando a Segurança do Windows, será necessário configurar um controlador de domínio para gerenciar o Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-123">If setting up the cluster using Windows Security, you will need to set up a domain controller to manage Active Directory.</span></span> <span data-ttu-id="e4dfb-124">Observe que não há suporte para o uso de um computador controlador de domínio como um nó do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-124">Note that using a domain controller machine as a Service Fabric node is not supported.</span></span>
8. <span data-ttu-id="e4dfb-125">Abra uma [janela do ISE do PowerShell](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span><span class="sxs-lookup"><span data-stu-id="e4dfb-125">Open a [PowerShell ISE window](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).</span></span> <span data-ttu-id="e4dfb-126">Navegue até a pasta onde você extraiu o pacote do instalador autônomo baixado e salvou o arquivo de configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-126">Navigate to the folder where you extracted the downloaded standalone installer package and saved the cluster configuration file.</span></span> <span data-ttu-id="e4dfb-127">Execute o comando PowerShell a seguir para implantar o cluster:</span><span class="sxs-lookup"><span data-stu-id="e4dfb-127">Run the following PowerShell command to deploy the cluster:</span></span>
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

<span data-ttu-id="e4dfb-128">O script configurará remotamente o cluster do Service Fabric e deverá informar o andamento à medida que implantação ocorre.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-128">The script will remotely configure the Service Fabric cluster and should report progress as deployment rolls through.</span></span>

9. <span data-ttu-id="e4dfb-129">Após um minuto, você poderá verificar se o cluster está operando conectando-se ao Service Fabric Explorer usando um dos endereços IP da máquina, por exemplo, usando `http://10.1.0.5:19080/Explorer/index.html`.</span><span class="sxs-lookup"><span data-stu-id="e4dfb-129">After about a minute, you can check if the cluster is operational by connecting to the Service Fabric Explorer using one of the machine's IP addresses, for example by using `http://10.1.0.5:19080/Explorer/index.html`.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e4dfb-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e4dfb-130">Next steps</span></span>
* [<span data-ttu-id="e4dfb-131">Criar clusters autônomos do Service Fabric no Windows Server ou Linux</span><span class="sxs-lookup"><span data-stu-id="e4dfb-131">Create standalone Service Fabric clusters on Windows Server or Linux</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="e4dfb-132">Adicionar ou remover nós de um cluster do Service Fabric autônomo</span><span class="sxs-lookup"><span data-stu-id="e4dfb-132">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="e4dfb-133">Definições de configuração para o cluster autônomo no Windows</span><span class="sxs-lookup"><span data-stu-id="e4dfb-133">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="e4dfb-134">Proteger um cluster autônomo no Windows usando a segurança</span><span class="sxs-lookup"><span data-stu-id="e4dfb-134">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="e4dfb-135">Proteger um cluster autônomo no Windows usando os certificados X509</span><span class="sxs-lookup"><span data-stu-id="e4dfb-135">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

