---
title: "aaaCreate e gerenciar um Azure Máquina Virtual usando o c# | Microsoft Docs"
description: "Use o c# e o Azure Resource Manager toodeploy uma máquina virtual e todos os seus recursos de suporte."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 87524373-5f52-4f4b-94af-50bf7b65c277
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: 8beeabde731bbaa25e68d2b9c5abbf71acbe377f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a><span data-ttu-id="4751a-103">Criar e gerenciar VMs Windows no Azure usando C#</span><span class="sxs-lookup"><span data-stu-id="4751a-103">Create and manage Windows VMs in Azure using C#</span></span> #

<span data-ttu-id="4751a-104">Uma [VM (Máquina Virtual) do Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) precisa de vários recursos do Azure de suporte.</span><span class="sxs-lookup"><span data-stu-id="4751a-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="4751a-105">Este artigo aborda a criação, o gerenciamento e a exclusão de recursos de VM utilizando C#.</span><span class="sxs-lookup"><span data-stu-id="4751a-105">This article covers creating, managing, and deleting VM resources using C#.</span></span> <span data-ttu-id="4751a-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="4751a-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4751a-107">Criar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4751a-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="4751a-108">Instalar o pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="4751a-108">Install hello package</span></span>
> * <span data-ttu-id="4751a-109">Criar credenciais</span><span class="sxs-lookup"><span data-stu-id="4751a-109">Create credentials</span></span>
> * <span data-ttu-id="4751a-110">Criar recursos</span><span class="sxs-lookup"><span data-stu-id="4751a-110">Create resources</span></span>
> * <span data-ttu-id="4751a-111">Executar tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="4751a-111">Perform management tasks</span></span>
> * <span data-ttu-id="4751a-112">Excluir recursos</span><span class="sxs-lookup"><span data-stu-id="4751a-112">Delete resources</span></span>
> * <span data-ttu-id="4751a-113">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="4751a-113">Run hello application</span></span>

<span data-ttu-id="4751a-114">Demora cerca de 20 minutos toodo essas etapas.</span><span class="sxs-lookup"><span data-stu-id="4751a-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="4751a-115">Criar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4751a-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="4751a-116">Se você ainda não fez isso, instale o [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="4751a-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="4751a-117">Selecione **desenvolvimento de área de trabalho do .NET** Olá página cargas de trabalho e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="4751a-117">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="4751a-118">Olá resumo, você verá que **ferramentas de desenvolvimento do .NET Framework 4 4.6** é selecionado automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="4751a-118">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="4751a-119">Se você já tiver instalado o Visual Studio, você pode adicionar carga de trabalho do .NET hello usando Olá iniciador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4751a-119">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="4751a-120">No Visual Studio, clique em **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="4751a-120">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="4751a-121">Em **modelos** > **Visual C#**, selecione **aplicativo de Console (.NET Framework)**, digite *myDotnetProject* para nome de saudação do Olá projeto local selecione Olá Olá do projeto do e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="4751a-121">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-package"></a><span data-ttu-id="4751a-122">Instalar o pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="4751a-122">Install hello package</span></span>

<span data-ttu-id="4751a-123">Pacotes do NuGet são Olá mais fácil maneira tooinstall Olá bibliotecas que você precisa toofinish essas etapas.</span><span class="sxs-lookup"><span data-stu-id="4751a-123">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="4751a-124">bibliotecas de saudação tooget que você precisa no Visual Studio, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="4751a-124">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="4751a-125">Clique em **Ferramentas** > **Gerenciador de Pacotes Nuget** e em **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="4751a-125">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="4751a-126">Digite este comando no console de saudação:</span><span class="sxs-lookup"><span data-stu-id="4751a-126">Type this command in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a><span data-ttu-id="4751a-127">Criar credenciais</span><span class="sxs-lookup"><span data-stu-id="4751a-127">Create credentials</span></span>

<span data-ttu-id="4751a-128">Antes de iniciar esta etapa, certifique-se de que você tenha acesso tooan [entidade de serviço do Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4751a-128">Before you start this step, make sure that you have access tooan [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="4751a-129">Você também deve registrar a ID do aplicativo hello, chave de autenticação hello e ID de locatário Olá que você precisa em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="4751a-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="4751a-130">Criar arquivo de autorização Olá</span><span class="sxs-lookup"><span data-stu-id="4751a-130">Create hello authorization file</span></span>

1. <span data-ttu-id="4751a-131">No Gerenciador de Soluções, clique com o botão direito do mouse em *myDotnetProject* > **Adicionar** > **Novo Item** e, em seguida, selecione **Arquivo de Texto** em *Itens do Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="4751a-131">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="4751a-132">Arquivo de saudação do nome *azureauth.properties*e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4751a-132">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="4751a-133">Adicione estas propriedades de autorização:</span><span class="sxs-lookup"><span data-stu-id="4751a-133">Add these authorization properties:</span></span>

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    <span data-ttu-id="4751a-134">Substituir  **&lt;id da assinatura&gt;**  com o identificador de assinatura,  **&lt;id do aplicativo&gt;**  com hello aplicativo do Active Directory identificador,  **&lt;chave de autenticação&gt;**  com chave de aplicativo hello, e  **&lt;id de locatário&gt;**  com locatário Olá identificador.</span><span class="sxs-lookup"><span data-stu-id="4751a-134">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="4751a-135">Salve o arquivo de azureauth.properties hello.</span><span class="sxs-lookup"><span data-stu-id="4751a-135">Save hello azureauth.properties file.</span></span> 
4. <span data-ttu-id="4751a-136">Defina uma variável de ambiente no Windows chamado AZURE_AUTH_LOCATION com arquivo hello de tooauthorization de caminho completo que você criou.</span><span class="sxs-lookup"><span data-stu-id="4751a-136">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created.</span></span> <span data-ttu-id="4751a-137">Por exemplo, a saudação comando PowerShell a seguir pode ser usada:</span><span class="sxs-lookup"><span data-stu-id="4751a-137">For example, hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a><span data-ttu-id="4751a-138">Crie saudação do cliente de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="4751a-138">Create hello management client</span></span>

1. <span data-ttu-id="4751a-139">Abra o arquivo Program.cs Olá projeto Olá que você criou e, em seguida, adicioná-las usando toohello existente instruções na parte superior do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="4751a-139">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. <span data-ttu-id="4751a-140">cliente de gerenciamento de saudação toocreate, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="4751a-140">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a><span data-ttu-id="4751a-141">Criar recursos</span><span class="sxs-lookup"><span data-stu-id="4751a-141">Create resources</span></span>

### <a name="create-hello-resource-group"></a><span data-ttu-id="4751a-142">Criar grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="4751a-142">Create hello resource group</span></span>

<span data-ttu-id="4751a-143">Todos os recursos devem estar contidos em um [Grupo de recursos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4751a-143">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="4751a-144">toospecify valores hello aplicativo e criar grupo de recursos de saudação, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="4751a-144">toospecify values for hello application and create hello resource group, add this code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a><span data-ttu-id="4751a-145">Criar conjunto de disponibilidade Olá</span><span class="sxs-lookup"><span data-stu-id="4751a-145">Create hello availability set</span></span>

<span data-ttu-id="4751a-146">[Conjuntos de disponibilidade](tutorial-availability-sets.md) tornar mais fácil para você toomaintain Olá VMs usados pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4751a-146">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

<span data-ttu-id="4751a-147">disponibilidade de saudação toocreate definido, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="4751a-147">toocreate hello availability set, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="4751a-148">Criar endereço IP público de saudação</span><span class="sxs-lookup"><span data-stu-id="4751a-148">Create hello public IP address</span></span>

<span data-ttu-id="4751a-149">Um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) é necessário toocommunicate com a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="4751a-149">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

<span data-ttu-id="4751a-150">toocreate Olá endereço IP público para a máquina virtual de Olá, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="4751a-150">toocreate hello public IP address for hello virtual machine, add this code toohello Main method:</span></span>
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a><span data-ttu-id="4751a-151">Criar rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="4751a-151">Create hello virtual network</span></span>

<span data-ttu-id="4751a-152">Uma máquina virtual precisa estar em uma sub-rede de uma [Rede virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4751a-152">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="4751a-153">toocreate uma sub-rede e uma rede virtual, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="4751a-153">toocreate a subnet and a virtual network, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a><span data-ttu-id="4751a-154">Criar a interface de rede Olá</span><span class="sxs-lookup"><span data-stu-id="4751a-154">Create hello network interface</span></span>

<span data-ttu-id="4751a-155">Uma máquina virtual precisa de um toocommunicate de interface de rede na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="4751a-155">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

<span data-ttu-id="4751a-156">toocreate uma interface de rede, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="4751a-156">toocreate a network interface, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating network interface...");
var networkInterface = azure.NetworkInterfaces.Define("myNIC")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetwork(network)
    .WithSubnet("mySubnet")
    .WithPrimaryPrivateIPAddressDynamic()
    .WithExistingPrimaryPublicIPAddress(publicIPAddress)
    .Create();
 ```

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="4751a-157">Criar a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="4751a-157">Create hello virtual machine</span></span>

<span data-ttu-id="4751a-158">Agora que você criou Olá todos os recursos de suporte, você pode criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4751a-158">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="4751a-159">toocreate Olá a máquina virtual, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="4751a-159">toocreate hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Creating virtual machine...");
azure.VirtualMachines.Define(vmName)
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("azureuser")
    .WithAdminPassword("Azure12345678")
    .WithComputerName(vmName)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

> [!NOTE]
> <span data-ttu-id="4751a-160">Este tutorial cria uma máquina virtual executando uma versão do sistema de operacional de servidor do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="4751a-160">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="4751a-161">toolearn mais sobre como selecionar outras imagens, consulte [navegue e selecione as imagens de máquina virtual do Azure com o Windows PowerShell e hello CLI do Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4751a-161">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="4751a-162">Se você quiser toouse um disco existente em vez de uma imagem do marketplace, use este código:</span><span class="sxs-lookup"><span data-stu-id="4751a-162">If you want toouse an existing disk instead of a marketplace image, use this code:</span></span>

```
var managedDisk = azure.Disks.Define("myosdisk")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd")
    .WithSizeInGB(128)
    .WithSku(DiskSkuTypes.PremiumLRS)
    .Create();

azure.VirtualMachines.Define("myVM")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows)
    .WithExistingAvailabilitySet(availabilitySet)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

## <a name="perform-management-tasks"></a><span data-ttu-id="4751a-163">Executar outras tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="4751a-163">Perform management tasks</span></span>

<span data-ttu-id="4751a-164">Durante a saudação do ciclo de vida de uma máquina virtual, talvez você queira toorun tarefas de gerenciamento como iniciar, parar ou excluir uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4751a-164">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="4751a-165">Além disso, talvez você queira toocreate código tooautomate repetitivas ou complexas tarefas.</span><span class="sxs-lookup"><span data-stu-id="4751a-165">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

<span data-ttu-id="4751a-166">Quando você precisar toodo nada com hello VM, você precisa tooget uma instância dele:</span><span class="sxs-lookup"><span data-stu-id="4751a-166">When you need toodo anything with hello VM, you need tooget an instance of it:</span></span>

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="4751a-167">Obter informações sobre Olá VM</span><span class="sxs-lookup"><span data-stu-id="4751a-167">Get information about hello VM</span></span>

<span data-ttu-id="4751a-168">tooget informações sobre a máquina virtual de hello, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="4751a-168">tooget information about hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Getting information about hello virtual machine...");
Console.WriteLine("hardwareProfile");
Console.WriteLine("   vmSize: " + vm.Size);
Console.WriteLine("storageProfile");
Console.WriteLine("  imageReference");
Console.WriteLine("    publisher: " + vm.StorageProfile.ImageReference.Publisher);
Console.WriteLine("    offer: " + vm.StorageProfile.ImageReference.Offer);
Console.WriteLine("    sku: " + vm.StorageProfile.ImageReference.Sku);
Console.WriteLine("    version: " + vm.StorageProfile.ImageReference.Version);
Console.WriteLine("  osDisk");
Console.WriteLine("    osType: " + vm.StorageProfile.OsDisk.OsType);
Console.WriteLine("    name: " + vm.StorageProfile.OsDisk.Name);
Console.WriteLine("    createOption: " + vm.StorageProfile.OsDisk.CreateOption);
Console.WriteLine("    caching: " + vm.StorageProfile.OsDisk.Caching);
Console.WriteLine("osProfile");
Console.WriteLine("  computerName: " + vm.OSProfile.ComputerName);
Console.WriteLine("  adminUsername: " + vm.OSProfile.AdminUsername);
Console.WriteLine("  provisionVMAgent: " + vm.OSProfile.WindowsConfiguration.ProvisionVMAgent.Value);
Console.WriteLine("  enableAutomaticUpdates: " + vm.OSProfile.WindowsConfiguration.EnableAutomaticUpdates.Value);
Console.WriteLine("networkProfile");
foreach (string nicId in vm.NetworkInterfaceIds)
{
    Console.WriteLine("  networkInterface id: " + nicId);
}
Console.WriteLine("vmAgent");
Console.WriteLine("  vmAgentVersion" + vm.InstanceView.VmAgent.VmAgentVersion);
Console.WriteLine("    statuses");
foreach (InstanceViewStatus stat in vm.InstanceView.VmAgent.Statuses)
{
    Console.WriteLine("    code: " + stat.Code);
    Console.WriteLine("    level: " + stat.Level);
    Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
    Console.WriteLine("    message: " + stat.Message);
    Console.WriteLine("    time: " + stat.Time);
}
Console.WriteLine("disks");
foreach (DiskInstanceView disk in vm.InstanceView.Disks)
{
    Console.WriteLine("  name: " + disk.Name);
    Console.WriteLine("  statuses");
    foreach (InstanceViewStatus stat in disk.Statuses)
    {
        Console.WriteLine("    code: " + stat.Code);
        Console.WriteLine("    level: " + stat.Level);
        Console.WriteLine("    displayStatus: " + stat.DisplayStatus);
        Console.WriteLine("    time: " + stat.Time);
    }
}
Console.WriteLine("VM general status");
Console.WriteLine("  provisioningStatus: " + vm.ProvisioningState);
Console.WriteLine("  id: " + vm.Id);
Console.WriteLine("  name: " + vm.Name);
Console.WriteLine("  type: " + vm.Type);
Console.WriteLine("  location: " + vm.Region);
Console.WriteLine("VM instance status");
foreach (InstanceViewStatus stat in vm.InstanceView.Statuses)
{
    Console.WriteLine("  code: " + stat.Code);
    Console.WriteLine("  level: " + stat.Level);
    Console.WriteLine("  displayStatus: " + stat.DisplayStatus);
}
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="stop-hello-vm"></a><span data-ttu-id="4751a-169">Parar Olá VM</span><span class="sxs-lookup"><span data-stu-id="4751a-169">Stop hello VM</span></span>

<span data-ttu-id="4751a-170">Você pode parar uma máquina virtual e mantenha todas as suas configurações, mas continuar toobe cobrado por ele, ou você pode parar uma máquina virtual e desalocar a ele.</span><span class="sxs-lookup"><span data-stu-id="4751a-170">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="4751a-171">Quando uma máquina virtual é desalocada, todos os recursos associados a ela também são desalocadas e a cobrança para eles termina.</span><span class="sxs-lookup"><span data-stu-id="4751a-171">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="4751a-172">máquina de virtual toostop Olá sem desalocá-lo, adicione toohello esse código método Main:</span><span class="sxs-lookup"><span data-stu-id="4751a-172">toostop hello virtual machine without deallocating it, add this code toohello Main method:</span></span>

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

<span data-ttu-id="4751a-173">Se você quiser toodeallocate Olá virtual machine, altere o código do hello desligado chamada toothis:</span><span class="sxs-lookup"><span data-stu-id="4751a-173">If you want toodeallocate hello virtual machine, change hello PowerOff call toothis code:</span></span>

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a><span data-ttu-id="4751a-174">Olá iniciar VM</span><span class="sxs-lookup"><span data-stu-id="4751a-174">Start hello VM</span></span>

<span data-ttu-id="4751a-175">toostart Olá a máquina virtual, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="4751a-175">toostart hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a><span data-ttu-id="4751a-176">Redimensionar Olá VM</span><span class="sxs-lookup"><span data-stu-id="4751a-176">Resize hello VM</span></span>

<span data-ttu-id="4751a-177">Muitos aspectos da implantação devem ser considerados ao decidir sobre um tamanho para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4751a-177">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="4751a-178">Para obter mais informações, consulte [Tamanhos de VM](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="4751a-178">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="4751a-179">toochange tamanho da máquina virtual de Olá, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="4751a-179">toochange size of hello virtual machine, add this code toohello Main method:</span></span>

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="4751a-180">Adicionar um disco de dados toohello VM</span><span class="sxs-lookup"><span data-stu-id="4751a-180">Add a data disk toohello VM</span></span>

<span data-ttu-id="4751a-181">tooadd uma máquina de virtual de toohello de disco de dados, adicione este código toohello principal método tooadd um disco de dados que é 2 GB de tamanho, han um LUN de 0 e um tipo de cache de ReadWrite:</span><span class="sxs-lookup"><span data-stu-id="4751a-181">tooadd a data disk toohello virtual machine, add this code toohello Main method tooadd a data disk that is 2 GB in size, han a LUN of 0 and a caching type of ReadWrite:</span></span>

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a><span data-ttu-id="4751a-182">Excluir recursos</span><span class="sxs-lookup"><span data-stu-id="4751a-182">Delete resources</span></span>

<span data-ttu-id="4751a-183">Como você é cobrado pelos recursos usados no Azure, é sempre recursos toodelete de práticas recomendadas que não são mais necessários.</span><span class="sxs-lookup"><span data-stu-id="4751a-183">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="4751a-184">Se você quiser toodelete Olá VMs e Olá todos os recursos de suporte, você tem toodo é Olá exclusão do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4751a-184">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

<span data-ttu-id="4751a-185">recurso de saudação toodelete grupo, adicione este código toohello método Main:</span><span class="sxs-lookup"><span data-stu-id="4751a-185">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="4751a-186">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="4751a-186">Run hello application</span></span>

<span data-ttu-id="4751a-187">Ele deve levar cerca de cinco minutos para este toorun do aplicativo de console completamente do início toofinish.</span><span class="sxs-lookup"><span data-stu-id="4751a-187">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="4751a-188">aplicativo de console hello toorun, clique em **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="4751a-188">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="4751a-189">Antes de pressionar **Enter** toostart recursos de exclusão, você pode levar alguns minutos criação de saudação do tooverify de recursos de saudação em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4751a-189">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="4751a-190">Clique em Olá implantação status toosee informações sobre a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="4751a-190">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4751a-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4751a-191">Next steps</span></span>
* <span data-ttu-id="4751a-192">Tirar proveito do uso de um modelo toocreate uma máquina virtual usando as informações de saudação em [implantar uma máquina Virtual do Azure usando o c# e um modelo do Gerenciador de recursos](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4751a-192">Take advantage of using a template toocreate a virtual machine by using hello information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="4751a-193">Saiba mais sobre como usar o hello [bibliotecas do Azure para .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="4751a-193">Learn more about using hello [Azure libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span></span>

