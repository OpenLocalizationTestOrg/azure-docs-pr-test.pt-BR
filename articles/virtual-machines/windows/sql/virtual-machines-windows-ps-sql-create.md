---
title: "aaaCreate uma máquina Virtual do SQL Server no Azure PowerShell (Gerenciador de recursos) | Microsoft Docs"
description: "Fornece etapas e scripts do PowerShell para criar uma VM do Azure com imagens da galeria de máquinas virtuais do SQL Server."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="2a9e0-103">Provisionar uma máquina virtual SQL Server usando o Azure PowerShell (Gerenciador de Recursos)</span><span class="sxs-lookup"><span data-stu-id="2a9e0-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2a9e0-104">Portal</span><span class="sxs-lookup"><span data-stu-id="2a9e0-104">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="2a9e0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a9e0-105">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="2a9e0-106">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2a9e0-106">Overview</span></span>
<span data-ttu-id="2a9e0-107">Este tutorial mostra como toocreate uma única máquina virtual do Azure usando Olá **do Azure Resource Manager** modelo de implantação usando cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-107">This tutorial shows you how toocreate a single Azure virtual machine using hello **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="2a9e0-108">Neste tutorial, vamos criar uma única máquina virtual usando uma única unidade de disco de uma imagem em Olá Galeria de SQL.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in hello SQL Gallery.</span></span> <span data-ttu-id="2a9e0-109">Vamos criar novos provedores de saudação armazenamento, rede e recursos de computação que serão usados pela máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-109">We will create new providers for hello storage, network, and compute resources that will be used by hello virtual machine.</span></span> <span data-ttu-id="2a9e0-110">Se você tiver provedores existentes para qualquer um desses recursos, poderá usar tais provedores.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="2a9e0-111">Se você precisa hello versão clássica deste tópico, consulte [provisionar uma máquina virtual do SQL Server usando o Azure PowerShell clássico](../classic/ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="2a9e0-111">If you need hello classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a9e0-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2a9e0-112">Prerequisites</span></span>
<span data-ttu-id="2a9e0-113">Para este tutorial, será necessário:</span><span class="sxs-lookup"><span data-stu-id="2a9e0-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="2a9e0-114">Uma conta do Azure e uma assinatura antes de começar.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="2a9e0-115">Se não tiver uma, inscreva-se em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2a9e0-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2a9e0-116">[Azure PowerShell](/powershell/azure/overview), versão mínima do 1.4.0 ou posterior (este tutorial foi escrito usando a versão 1.5.0).</span><span class="sxs-lookup"><span data-stu-id="2a9e0-116">[Azure PowerShell)](/powershell/azure/overview), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="2a9e0-117">tooretrieve sua versão, o tipo **Azure Get-Module - ListAvailable**.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-117">tooretrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="2a9e0-118">Configurar sua assinatura</span><span class="sxs-lookup"><span data-stu-id="2a9e0-118">Configure your subscription</span></span>
<span data-ttu-id="2a9e0-119">Abra o Windows PowerShell e estabelecer acesso tooyour conta do Azure executando Olá cmdlet a seguir.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-119">Open Windows PowerShell and establish access tooyour Azure account by running hello following cmdlet.</span></span> <span data-ttu-id="2a9e0-120">Você verá uma tela tooenter entrar suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-120">You will be presented with a sign in screen tooenter your credentials.</span></span> <span data-ttu-id="2a9e0-121">Use Olá mesmo email e a senha que você use toosign em toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-121">Use hello same email and password that you use toosign in toohello Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="2a9e0-122">Depois de entrar com êxito, você verá algumas informações na tela que inclui SubscriptionId Olá com a qual você entrou.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-122">After successfully signing in you will see some information on screen that includes hello SubscriptionId with which you signed in.</span></span> <span data-ttu-id="2a9e0-123">Isso é assinatura Olá no qual serão criados recursos Olá para este tutorial, a menos que você alterar assinatura diferente tooa.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-123">This is hello subscription in which hello resources for this tutorial will be created unless you change tooa different subscription.</span></span> <span data-ttu-id="2a9e0-124">Se você tiver vários SubscriptionIds, execute Olá tooreturn cmdlet a seguir uma lista de todos os seus SubscriptionIds:</span><span class="sxs-lookup"><span data-stu-id="2a9e0-124">If you have multiple SubscriptionIds, run hello following cmdlet tooreturn a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="2a9e0-125">tooanother toochange SubscriptionID, executar Olá cmdlet com o SubscriptionId desejado a seguir.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-125">toochange tooanother SubscriptionID, run hello following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="2a9e0-126">Definir variáveis de imagem</span><span class="sxs-lookup"><span data-stu-id="2a9e0-126">Define image variables</span></span>
<span data-ttu-id="2a9e0-127">toosimplify usabilidade e compreensão de script hello concluído deste tutorial, vamos começar com a definição de um número de variáveis.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-127">toosimplify usability and understanding of hello completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="2a9e0-128">Alterar valores de parâmetro hello como achar mais conveniente, mas lembre-se de nomenclatura comprimentos de tooname relacionados restrições e caracteres especiais ao modificar valores hello fornecidos.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-128">Change hello parameter values as you see fit, but beware of naming restrictions related tooname lengths and special characters when modifying hello values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="2a9e0-129">Local e Grupo de Recursos</span><span class="sxs-lookup"><span data-stu-id="2a9e0-129">Location and Resource Group</span></span>
<span data-ttu-id="2a9e0-130">Use duas variáveis toodefine Olá dados região e hello grupo de recursos no qual você irá criar hello outros recursos para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-130">Use two variables toodefine hello data region and hello resource group into which you will create hello other resources for hello virtual machine.</span></span>

<span data-ttu-id="2a9e0-131">Modifique conforme desejado e, em seguida, execute Olá tooinitialize cmdlets a seguir essas variáveis.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-131">Modify as desired and then execute hello following cmdlets tooinitialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="2a9e0-132">Propriedades de armazenamento</span><span class="sxs-lookup"><span data-stu-id="2a9e0-132">Storage properties</span></span>
<span data-ttu-id="2a9e0-133">Use Olá variáveis toodefine Olá conta e hello tipo de armazenamento do toobe de armazenamento usada pela máquina virtual de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-133">Use hello following variables toodefine hello storage account and hello type of storage toobe used by hello virtual machine.</span></span>

<span data-ttu-id="2a9e0-134">Modifique conforme desejado e, em seguida, execute Olá tooinitialize cmdlet a seguir essas variáveis.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-134">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span> <span data-ttu-id="2a9e0-135">Observe que, neste exemplo estamos usando o [Armazenamento Premium](../../../storage/common/storage-premium-storage.md), que é recomendado para cargas de trabalho de produção.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-135">Note that in this example, we are using [Premium Storage](../../../storage/common/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="2a9e0-136">Para obter detalhes sobre essas diretrizes e outras recomendações, confira [Melhores práticas para o SQL Server em Máquinas Virtuais do Azure](virtual-machines-windows-sql-performance.md).</span><span class="sxs-lookup"><span data-stu-id="2a9e0-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="2a9e0-137">Propriedades da rede</span><span class="sxs-lookup"><span data-stu-id="2a9e0-137">Network properties</span></span>
<span data-ttu-id="2a9e0-138">Use Olá seguindo a interface de rede variáveis toodefine hello, método de alocação de TCP/IP hello, nome de rede virtual Olá, nome de sub-rede virtual hello, Olá intervalo de endereços IP para rede virtual hello, Olá intervalo de endereços IP de sub-rede hello e hello rótulo de nome de domínio público toobe usada pela rede Olá na máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-138">Use hello following variables toodefine hello network interface, hello TCP/IP allocation method, hello virtual network name, hello virtual subnet name, hello range of IP addresses for hello virtual network, hello range of IP addresses for hello subnet, and hello public domain name label toobe used by hello network in hello virtual machine.</span></span>

<span data-ttu-id="2a9e0-139">Modifique conforme desejado e, em seguida, execute Olá tooinitialize cmdlet a seguir essas variáveis.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-139">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="2a9e0-140">Propriedades de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="2a9e0-140">Virtual machine properties</span></span>
<span data-ttu-id="2a9e0-141">Saudação de uso após o nome da máquina virtual variáveis toodefine Olá, nome do computador hello, tamanho da máquina virtual hello e nome de disco do sistema operacional Olá para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-141">Use hello following variables toodefine hello virtual machine name, hello computer name, hello virtual machine size, and hello operating system disk name for hello virtual machine.</span></span>

<span data-ttu-id="2a9e0-142">Modifique conforme desejado e, em seguida, execute Olá tooinitialize cmdlet a seguir essas variáveis.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-142">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="2a9e0-143">Propriedades da imagem</span><span class="sxs-lookup"><span data-stu-id="2a9e0-143">Image properties</span></span>
<span data-ttu-id="2a9e0-144">Use Olá variáveis toodefine Olá imagem toouse para a máquina virtual de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-144">Use hello following variables toodefine hello image toouse for hello virtual machine.</span></span> <span data-ttu-id="2a9e0-145">Neste exemplo, a imagem do SQL Server 2016 Enterprise Olá é usada.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-145">In this example, hello SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="2a9e0-146">Modifique conforme desejado e, em seguida, execute Olá tooinitialize cmdlet a seguir essas variáveis.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-146">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="2a9e0-147">Observe que você pode obter uma lista completa de ofertas de imagem do SQL Server com o comando Get-AzureRmVMImageOffer de saudação:</span><span class="sxs-lookup"><span data-stu-id="2a9e0-147">Note that you can get a full list of SQL Server image offerings with hello Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="2a9e0-148">E você pode ver Olá Skus disponíveis para uma oferta com o comando Get-AzureRmVMImageSku de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-148">And you can see hello Skus available for an offering with hello Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="2a9e0-149">Olá, comando a seguir mostra todos os Skus disponíveis para Olá **SQL2014SP1 WS2012R2** oferecem.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-149">hello following command shows all Skus available for hello **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="2a9e0-150">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2a9e0-150">Create a resource group</span></span>
<span data-ttu-id="2a9e0-151">Com o modelo de implantação do Gerenciador de recursos de hello, o primeiro objeto do hello que você cria é grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-151">With hello Resource Manager deployment model, hello first object that you create is hello resource group.</span></span> <span data-ttu-id="2a9e0-152">Usaremos Olá [AzureRmResourceGroup novo](/powershell/module/azurerm.resources/new-azurermresourcegroup) toocreate cmdlet de um grupo de recursos do Azure e seus recursos com recursos de saudação grupo nome e local definido pelas variáveis de saudação inicializado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-152">We will use hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate an Azure resource group and its resources with hello resource group name and location defined by hello variables that you previously initialized.</span></span>

<span data-ttu-id="2a9e0-153">Execute Olá toocreate cmdlet a seguir em seu novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-153">Execute hello following cmdlet toocreate your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="2a9e0-154">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="2a9e0-154">Create a storage account</span></span>
<span data-ttu-id="2a9e0-155">máquina virtual de saudação requer recursos de armazenamento de disco do sistema operacional hello e hello dados do SQL Server e os arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-155">hello virtual machine requires storage resources for hello operating system disk and for hello SQL Server data and log files.</span></span> <span data-ttu-id="2a9e0-156">Para simplificar, criaremos um único disco para ambos.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="2a9e0-157">Você pode anexar discos adicionais posteriormente usando Olá [Azure adicionar disco](/powershell/module/azure/add-azuredisk) cmdlet na ordem tooplace os dados do SQL Server e arquivos de log em discos dedicados.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-157">You can attach additional disks later using hello [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet in order tooplace your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="2a9e0-158">Usaremos Olá [AzureRmStorageAccount novo](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate um armazenamento padrão da conta no seu novo grupo de recursos e com o nome de conta de armazenamento Olá, nome do Sku de armazenamento e local definido usando variáveis de saudação que você inicializado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-158">We will use hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate a standard storage account in your new resource group and with hello storage account name, storage Sku name, and location defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="2a9e0-159">Execute Olá toocreate cmdlet a seguir em sua nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-159">Execute hello following cmdlet toocreate your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="2a9e0-160">Criar recursos da rede</span><span class="sxs-lookup"><span data-stu-id="2a9e0-160">Create network resources</span></span>
<span data-ttu-id="2a9e0-161">máquina virtual de saudação requer um número de recursos de rede para conectividade de rede.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-161">hello virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="2a9e0-162">Cada máquina virtual exige um rede virtual.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="2a9e0-163">Uma rede virtual deve ter pelo menos uma sub-rede definida.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="2a9e0-164">Uma interface de rede deve ser definida com um público ou um endereço IP privado.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="2a9e0-165">Criar uma configuração de sub-rede da rede virtual</span><span class="sxs-lookup"><span data-stu-id="2a9e0-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="2a9e0-166">Vamos começar criando uma configuração de sub-rede para nossa rede virtual.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="2a9e0-167">Para nosso tutorial, vamos criar uma sub-rede padrão usando Olá [AzureRmVirtualNetworkSubnetConfig novo](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-167">For our tutorial, we will create a default subnet using hello [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span></span> <span data-ttu-id="2a9e0-168">Vamos criar nossa configuração de sub-rede da rede virtual com produtos de prefixo de nome e endereço de sub-rede Olá definido usando variáveis de saudação inicializado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-168">We will create our virtual network subnet configuration with hello subnet name and address prefix defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="2a9e0-169">Você pode definir propriedades adicionais de configuração de sub-rede da rede virtual de saudação usando esse cmdlet, mas que está além do escopo deste tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-169">You can define additional properties of hello virtual network subnet configuration using this cmdlet, but that is beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="2a9e0-170">Execute Olá toocreate cmdlet a seguir em sua configuração de sub-rede virtual.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-170">Execute hello following cmdlet toocreate your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="2a9e0-171">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="2a9e0-171">Create a virtual network</span></span>
<span data-ttu-id="2a9e0-172">Em seguida, vamos criar rede virtual usando Olá [AzureRmVirtualNetwork novo](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-172">Next, we will create our virtual network using hello [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span></span> <span data-ttu-id="2a9e0-173">Vamos criar rede virtual em seu novo grupo de recursos, com o nome hello, o local e o prefixo de endereço definido usando variáveis de saudação inicializado anteriormente e usando a configuração de sub-rede Olá definida na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-173">We will create our virtual network in your new resource group, with hello name, location, and address prefix defined using hello variables that you previously initialized, and using hello subnet configuration that you defined in hello previous step.</span></span>

<span data-ttu-id="2a9e0-174">Execute Olá toocreate cmdlet a seguir em sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-174">Execute hello following cmdlet toocreate your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="2a9e0-175">Criar endereço IP público de saudação</span><span class="sxs-lookup"><span data-stu-id="2a9e0-175">Create hello public IP address</span></span>
<span data-ttu-id="2a9e0-176">Agora que temos de rede virtual definido, é preciso tooconfigure um endereço IP da máquina de virtual toohello conectividade.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-176">Now that we have our virtual network defined, we need tooconfigure an IP address for connectivity toohello virtual machine.</span></span> <span data-ttu-id="2a9e0-177">Para este tutorial, vamos criar um endereço IP público usando toosupport conectividade com a Internet de endereçamento de IP dinâmico.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-177">For this tutorial, we will create a public IP address using dynamic IP addressing toosupport Internet connectivity.</span></span> <span data-ttu-id="2a9e0-178">Usaremos Olá [AzureRmPublicIpAddress novo](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate Olá endereço IP público no hello recurso grupo criado prevously e com o nome hello, local, método de alocação e rótulo de nome de domínio DNS definido usando Olá variáveis que inicializado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-178">We will use hello [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello public IP address in hello resource group created prevously and with hello name, location, allocation method, and DNS domain name label defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="2a9e0-179">Você pode definir propriedades adicionais do endereço IP público hello usando esse cmdlet, mas que está além do escopo Olá deste tutorial inicial.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-179">You can define additional properties of hello public IP address using this cmdlet, but that is beyond hello scope of this initial tutorial.</span></span> <span data-ttu-id="2a9e0-180">Você também pode criar um endereço privado ou um endereço com um endereço estático, mas que também está além do escopo deste tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-180">You could also create a private address or an address with a static address, but that is also beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="2a9e0-181">Execute Olá toocreate cmdlet a seguir em seu endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-181">Execute hello following cmdlet toocreate your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a><span data-ttu-id="2a9e0-182">Criar a interface de rede Olá</span><span class="sxs-lookup"><span data-stu-id="2a9e0-182">Create hello network interface</span></span>
<span data-ttu-id="2a9e0-183">Agora estamos interface de rede do hello toocreate pronto nossa máquina virtual será usado.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-183">We are now ready toocreate hello network interface that our virtual machine will use.</span></span> <span data-ttu-id="2a9e0-184">Usaremos Olá [AzureRmNetworkInterface novo](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate nossa interface de rede no grupo de recursos de saudação criado anteriormente e com o nome hello, local, sub-rede e o endereço IP público definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-184">We will use hello [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate our network interface in hello resource group created earlier and with hello name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="2a9e0-185">Execute Olá toocreate cmdlet a seguir em sua interface de rede.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-185">Execute hello following cmdlet toocreate your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="2a9e0-186">Configurar um objeto da VM</span><span class="sxs-lookup"><span data-stu-id="2a9e0-186">Configure a VM object</span></span>
<span data-ttu-id="2a9e0-187">Agora que temos os recursos de armazenamento e rede definidos, estamos prontos toodefine recursos de computação para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-187">Now that we have storage and network resources defined, we are ready toodefine compute resources for hello virtual machine.</span></span> <span data-ttu-id="2a9e0-188">Para nosso tutorial, nós será especificar o tamanho da máquina virtual hello e várias propriedades de sistema operacional, especifique a interface de rede de saudação que criamos anteriormente, definir armazenamento de blob e, em seguida, especifique o disco do sistema operacional Olá.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-188">For our tutorial, we will specify hello virtual machine size and various operating system properties, specify hello network interface that we previously created, define blob storage, and then specify hello operating system disk.</span></span>

### <a name="create-hello-vm-object"></a><span data-ttu-id="2a9e0-189">Criar objeto VM Olá</span><span class="sxs-lookup"><span data-stu-id="2a9e0-189">Create hello VM object</span></span>
<span data-ttu-id="2a9e0-190">Vamos começar com a especificação de tamanho da máquina virtual hello.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-190">We will start by specifying hello virtual machine size.</span></span> <span data-ttu-id="2a9e0-191">Para este tutorial, estamos especificando um DS13.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="2a9e0-192">Usaremos Olá [AzureRmVMConfig novo](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate um objeto de máquina de virtual configuráveis com nome hello e o tamanho definido usando variáveis de saudação inicializado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-192">We will use hello [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate a configurable virtual machine object with hello name and size defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="2a9e0-193">Execute Olá após o objeto de máquina virtual do cmdlet toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-193">Execute hello following cmdlet toocreate hello virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a><span data-ttu-id="2a9e0-194">Criar um nome da credencial objeto toohold hello e uma senha para credenciais de administrador local Olá</span><span class="sxs-lookup"><span data-stu-id="2a9e0-194">Create a credential object toohold hello name and password for hello local administrator credentials</span></span>
<span data-ttu-id="2a9e0-195">Antes que podemos definir propriedades do sistema operacional Olá para a máquina virtual de hello, precisamos de toosupply Olá credenciais Olá conta de administrador local como uma cadeia de caracteres segura.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-195">Before we can set hello operating system properties for hello virtual machine, we need toosupply hello credentials for hello local administrator account as a secure string.</span></span> <span data-ttu-id="2a9e0-196">tooaccomplish isso, usaremos Olá [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-196">tooaccomplish this, we will use hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="2a9e0-197">Execute Olá cmdlet a seguir e, na janela de solicitação de credencial do hello Windows PowerShell, digite toouse de nome e senha Olá Olá conta de administrador local na máquina de virtual do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-197">Execute hello following cmdlet and, in hello Windows PowerShell credential request window, type hello name and password toouse for hello local administrator account in hello Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a><span data-ttu-id="2a9e0-198">Definir as propriedades de sistema operacional Olá para a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="2a9e0-198">Set hello operating system properties for hello virtual machine</span></span>
<span data-ttu-id="2a9e0-199">Agora, estamos propriedades do sistema operacional da máquina de virtual Olá tooset pronto.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-199">Now we are ready tooset hello virtual machine's operating system properties.</span></span> <span data-ttu-id="2a9e0-200">Usaremos Olá [conjunto AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset Olá tipo de sistema operacional como janelas, exigem Olá [agente da máquina virtual](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe instalado, especifique que Olá habilita automaticamente atualizar e defina o nome da máquina virtual Olá, nome de computador hello e credencial hello usando variáveis de saudação inicializado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-200">We will use hello [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset hello type of operating system as Windows, require hello [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe installed, specify that hello cmdlet enables auto update and set hello virtual machine name, hello computer name, and hello credential using hello variables that you previously initialized.</span></span>

<span data-ttu-id="2a9e0-201">Execute Olá seguintes propriedades de sistema operacional do cmdlet tooset Olá para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-201">Execute hello following cmdlet tooset hello operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a><span data-ttu-id="2a9e0-202">Adicionar a máquina virtual do hello rede interface toohello</span><span class="sxs-lookup"><span data-stu-id="2a9e0-202">Add hello network interface toohello virtual machine</span></span>
<span data-ttu-id="2a9e0-203">Em seguida, adicionaremos a interface de rede de saudação que criamos anteriormente toohello VM.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-203">Next, we will add hello network interface that we created previously toohello virtual machine.</span></span> <span data-ttu-id="2a9e0-204">Usaremos Olá [AzureRmVMNetworkInterface adicionar](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) interface de rede do cmdlet tooadd hello usando a variável de interface de rede Olá definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-204">We will use hello [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd hello network interface using hello network interface variable that you defined earlier.</span></span>

<span data-ttu-id="2a9e0-205">Execute Olá interface de rede do cmdlet tooset Olá para sua máquina virtual a seguir.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-205">Execute hello following cmdlet tooset hello network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a><span data-ttu-id="2a9e0-206">Defina o local de armazenamento de blob Olá para Olá disco toobe usada pela máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="2a9e0-206">Set hello blob storage location for hello disk toobe used by hello virtual machine</span></span>
<span data-ttu-id="2a9e0-207">Em seguida, vamos definir local de armazenamento de blob Olá para Olá disco toobe usada pela máquina virtual de saudação usando variáveis de saudação definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-207">Next, we will set hello blob storage location for hello disk toobe used by hello virtual machine using hello variables that you defined earlier.</span></span>

<span data-ttu-id="2a9e0-208">Execute Olá local de armazenamento de blob do cmdlet tooset Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-208">Execute hello following cmdlet tooset hello blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a><span data-ttu-id="2a9e0-209">Definir propriedades de disco da máquina virtual de saudação de sistema de operacional de saudação</span><span class="sxs-lookup"><span data-stu-id="2a9e0-209">Set hello operating system disk properties for hello virtual machine</span></span>
<span data-ttu-id="2a9e0-210">Em seguida, vamos definir sistema de operacional Olá propriedades do disco da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-210">Next, we will set hello operating system disk properties for hello virtual machine.</span></span> <span data-ttu-id="2a9e0-211">Usaremos Olá [AzureRmVMOSDisk conjunto](/powershell/module/azurerm.compute/set-azurermvmosdisk) toospecify cmdlet que Olá o sistema operacional da máquina virtual de saudação será proveniente de uma imagem, tooset tooread apenas de cache (porque o SQL Server está sendo instalado na Olá mesmo disco) e definir nome da máquina virtual Hello e o disco do sistema operacional Olá definido usando variáveis de saudação que definimos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-211">We will use hello [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet toospecify that hello operating system for hello virtual machine will come from an image, tooset caching tooread only (because SQL Server is being installed on hello same disk) and define hello virtual machine name and hello operating system disk defined using hello variables that we defined earlier.</span></span>

<span data-ttu-id="2a9e0-212">Execute Olá seguintes propriedades de disco do sistema operacional do cmdlet tooset Olá para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-212">Execute hello following cmdlet tooset hello operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a><span data-ttu-id="2a9e0-213">Especifique a imagem da plataforma Olá para a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="2a9e0-213">Specify hello platform image for hello virtual machine</span></span>
<span data-ttu-id="2a9e0-214">Nossa última etapa de configuração é a imagem da plataforma toospecify Olá para nossa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-214">Our last configuration step is toospecify hello platform image for our virtual machine.</span></span> <span data-ttu-id="2a9e0-215">Para nosso tutorial, estamos usando imagem do SQL Server 2016 CTP mais recente hello.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-215">For our tutorial, we are using hello latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="2a9e0-216">Usaremos Olá [AzureRmVMSourceImage conjunto](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse essa imagem conforme definido pelas variáveis Olá definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-216">We will use hello [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse this image as defined by hello variables that you defined earlier.</span></span>

<span data-ttu-id="2a9e0-217">Execute Olá imagem da plataforma do cmdlet toospecify Olá para sua máquina virtual a seguir.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-217">Execute hello following cmdlet toospecify hello platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a><span data-ttu-id="2a9e0-218">Criar hello VM do SQL</span><span class="sxs-lookup"><span data-stu-id="2a9e0-218">Create hello SQL VM</span></span>
<span data-ttu-id="2a9e0-219">Agora que você concluiu as etapas de configuração hello, você está pronto toocreate Olá VM.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-219">Now that you have finished hello configuration steps, you are ready toocreate hello virtual machine.</span></span> <span data-ttu-id="2a9e0-220">Usaremos Olá [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate Olá VM usando variáveis de saudação que definimos.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-220">We will use hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate hello virtual machine using hello variables that we have defined.</span></span>

<span data-ttu-id="2a9e0-221">Execute Olá toocreate cmdlet a seguir em sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-221">Execute hello following cmdlet toocreate your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="2a9e0-222">máquina virtual de saudação é criada.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-222">hello virtual machine is created.</span></span> <span data-ttu-id="2a9e0-223">Observe que uma conta de armazenamento padrão é criada para o diagnóstico de inicialização porque Olá especificado a conta de armazenamento para Olá disco de máquina virtual é uma conta de armazenamento premium.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-223">Notice that a standard storage account is created for boot diagnostics because hello specified storage account for hello virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="2a9e0-224">Agora você pode exibir esta máquina no hello Azure Portal toosee [seu endereço IP público e seu nome de domínio totalmente qualificado](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="2a9e0-224">You can now view this machine in hello Azure Portal toosee [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="2a9e0-225">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="2a9e0-225">Example script</span></span>
<span data-ttu-id="2a9e0-226">Olá script a seguir contém Olá completa script do PowerShell para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-226">hello following script contains hello complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="2a9e0-227">Ele pressupõe que você já tenha instalação Olá assinatura do Azure toouse com hello **adicionar AzureRmAccount** e **AzureRmSubscription selecione** comandos.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-227">It assumes that you have already setup hello Azure subscription toouse with hello **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a><span data-ttu-id="2a9e0-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2a9e0-228">Next steps</span></span>
<span data-ttu-id="2a9e0-229">Após a criação de máquina virtual de saudação, você está pronto tooconnect toohello VM usando o RDP e configuração de conectividade.</span><span class="sxs-lookup"><span data-stu-id="2a9e0-229">After hello virtual machine is created, you are ready tooconnect toohello virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="2a9e0-230">Para obter mais informações, consulte [conectar tooa Máquina Virtual do SQL Server no Azure (Gerenciador de recursos)](virtual-machines-windows-sql-connect.md).</span><span class="sxs-lookup"><span data-stu-id="2a9e0-230">For more information, see [Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

