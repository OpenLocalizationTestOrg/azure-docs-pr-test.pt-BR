---
title: "Criar e gerenciar uma Máquina Virtual do Azure usando o C# | Microsoft Docs"
description: "Use o C# e o Azure Resource Manager para implantar uma máquina virtual e todos os seus recursos de suporte."
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
ms.openlocfilehash: 5d9021c2f65b70e36d5ea82992c9fb9d2d6d394a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a><span data-ttu-id="5a75e-103">Criar e gerenciar VMs Windows no Azure usando C#</span><span class="sxs-lookup"><span data-stu-id="5a75e-103">Create and manage Windows VMs in Azure using C#</span></span> #

<span data-ttu-id="5a75e-104">Uma [VM (Máquina Virtual) do Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) precisa de vários recursos do Azure de suporte.</span><span class="sxs-lookup"><span data-stu-id="5a75e-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="5a75e-105">Este artigo aborda a criação, o gerenciamento e a exclusão de recursos de VM utilizando C#.</span><span class="sxs-lookup"><span data-stu-id="5a75e-105">This article covers creating, managing, and deleting VM resources using C#.</span></span> <span data-ttu-id="5a75e-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="5a75e-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5a75e-107">Criar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a75e-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="5a75e-108">Instalar o pacote</span><span class="sxs-lookup"><span data-stu-id="5a75e-108">Install the package</span></span>
> * <span data-ttu-id="5a75e-109">Criar credenciais</span><span class="sxs-lookup"><span data-stu-id="5a75e-109">Create credentials</span></span>
> * <span data-ttu-id="5a75e-110">Criar recursos</span><span class="sxs-lookup"><span data-stu-id="5a75e-110">Create resources</span></span>
> * <span data-ttu-id="5a75e-111">Executar tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="5a75e-111">Perform management tasks</span></span>
> * <span data-ttu-id="5a75e-112">Excluir recursos</span><span class="sxs-lookup"><span data-stu-id="5a75e-112">Delete resources</span></span>
> * <span data-ttu-id="5a75e-113">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="5a75e-113">Run the application</span></span>

<span data-ttu-id="5a75e-114">São necessários cerca de 20 minutos para a conclusão destas etapas.</span><span class="sxs-lookup"><span data-stu-id="5a75e-114">It takes about 20 minutes to do these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="5a75e-115">Criar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a75e-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="5a75e-116">Se você ainda não fez isso, instale o [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="5a75e-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="5a75e-117">Selecione **Desenvolvimento para desktop com o .NET** na página Cargas de trabalho e, em seguida, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="5a75e-117">Select **.NET desktop development** on the Workloads page, and then click **Install**.</span></span> <span data-ttu-id="5a75e-118">No resumo, é possível verificar que as **ferramentas de desenvolvimento do .NET Framework 4 - 4.6** são automaticamente selecionadas.</span><span class="sxs-lookup"><span data-stu-id="5a75e-118">In the summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="5a75e-119">Se o Visual Studio já estiver instalado, você poderá adicionar a carga de trabalho .NET utilizando o Iniciador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a75e-119">If you have already installed Visual Studio, you can add the .NET workload using the Visual Studio Launcher.</span></span>
2. <span data-ttu-id="5a75e-120">No Visual Studio, clique em **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="5a75e-120">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="5a75e-121">Em **Modelos** > **Visual C#**, selecione **Aplicativo de Console (.NET Framework)**, digite *myDotnetProject* para o nome do projeto, selecione o local do projeto e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5a75e-121">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for the name of the project, select the location of the project, and then click **OK**.</span></span>

## <a name="install-the-package"></a><span data-ttu-id="5a75e-122">Instalar o pacote</span><span class="sxs-lookup"><span data-stu-id="5a75e-122">Install the package</span></span>

<span data-ttu-id="5a75e-123">Os pacotes NuGet são a maneira mais fácil de instalar as bibliotecas de que você precisa para concluir estas etapas.</span><span class="sxs-lookup"><span data-stu-id="5a75e-123">NuGet packages are the easiest way to install the libraries that you need to finish these steps.</span></span> <span data-ttu-id="5a75e-124">Para obter as bibliotecas que você precisa no Visual Studio, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="5a75e-124">To get the libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="5a75e-125">Clique em **Ferramentas** > **Gerenciador de Pacotes Nuget** e em **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="5a75e-125">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="5a75e-126">Digite este comando no console:</span><span class="sxs-lookup"><span data-stu-id="5a75e-126">Type this command in the console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a><span data-ttu-id="5a75e-127">Criar credenciais</span><span class="sxs-lookup"><span data-stu-id="5a75e-127">Create credentials</span></span>

<span data-ttu-id="5a75e-128">Antes de começar essa etapa, verifique se você tem acesso a uma [entidade de serviço do Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5a75e-128">Before you start this step, make sure that you have access to an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="5a75e-129">Além disso, registre o ID do aplicativo, a chave de autenticação e o ID do locatário que serão necessários em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="5a75e-129">You should also record the application ID, the authentication key, and the tenant ID that you need in a later step.</span></span>

### <a name="create-the-authorization-file"></a><span data-ttu-id="5a75e-130">Criar o arquivo de autorização</span><span class="sxs-lookup"><span data-stu-id="5a75e-130">Create the authorization file</span></span>

1. <span data-ttu-id="5a75e-131">No Gerenciador de Soluções, clique com o botão direito do mouse em *myDotnetProject* > **Adicionar** > **Novo Item** e, em seguida, selecione **Arquivo de Texto** em *Itens do Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="5a75e-131">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="5a75e-132">Nomeie o arquivo *azureauth.properties* e, em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5a75e-132">Name the file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="5a75e-133">Adicione estas propriedades de autorização:</span><span class="sxs-lookup"><span data-stu-id="5a75e-133">Add these authorization properties:</span></span>

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

    <span data-ttu-id="5a75e-134">Substitua **&lt;subscription-id&gt;** pelo identificador da assinatura, **&lt;application-id&gt;** pelo identificador de aplicativo do Active Directory, **&lt;authentication-key&gt;** pela chave do aplicativo e **&lt;tenant-id&gt;** pelo identificador do locatário.</span><span class="sxs-lookup"><span data-stu-id="5a75e-134">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with the Active Directory application identifier, **&lt;authentication-key&gt;** with the application key, and **&lt;tenant-id&gt;** with the tenant identifier.</span></span>

3. <span data-ttu-id="5a75e-135">Salve o arquivo azureauth.properties.</span><span class="sxs-lookup"><span data-stu-id="5a75e-135">Save the azureauth.properties file.</span></span> 
4. <span data-ttu-id="5a75e-136">Defina uma variável de ambiente no Windows chamada AZURE_AUTH_LOCATION com o caminho completo para o arquivo de autorização que você criou.</span><span class="sxs-lookup"><span data-stu-id="5a75e-136">Set an environment variable in Windows named AZURE_AUTH_LOCATION with the full path to authorization file that you created.</span></span> <span data-ttu-id="5a75e-137">Por exemplo, o seguinte comando do PowerShell pode ser usado:</span><span class="sxs-lookup"><span data-stu-id="5a75e-137">For example, the following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-the-management-client"></a><span data-ttu-id="5a75e-138">Criar o cliente de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="5a75e-138">Create the management client</span></span>

1. <span data-ttu-id="5a75e-139">Abra o arquivo Program.cs para o projeto que você criou e, em seguida, adicione o seguinte usando instruções para as instruções existentes na parte superior do arquivo:</span><span class="sxs-lookup"><span data-stu-id="5a75e-139">Open the Program.cs file for the project that you created, and then add these using statements to the existing statements at top of the file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. <span data-ttu-id="5a75e-140">Para criar o cliente de gerenciamento, adicione este código ao método Main:</span><span class="sxs-lookup"><span data-stu-id="5a75e-140">To create the management client, add this code to the Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a><span data-ttu-id="5a75e-141">Criar recursos</span><span class="sxs-lookup"><span data-stu-id="5a75e-141">Create resources</span></span>

### <a name="create-the-resource-group"></a><span data-ttu-id="5a75e-142">Criar o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="5a75e-142">Create the resource group</span></span>

<span data-ttu-id="5a75e-143">Todos os recursos devem estar contidos em um [Grupo de recursos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a75e-143">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="5a75e-144">Para especificar valores para o aplicativo e criar o grupo de recursos, adicione este código ao método Main:</span><span class="sxs-lookup"><span data-stu-id="5a75e-144">To specify values for the application and create the resource group, add this code to the Main method:</span></span>

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-the-availability-set"></a><span data-ttu-id="5a75e-145">Criar o conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="5a75e-145">Create the availability set</span></span>

<span data-ttu-id="5a75e-146">Os [Conjuntos de disponibilidade](tutorial-availability-sets.md) facilitam a manutenção das máquinas virtuais usadas por seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5a75e-146">[Availability sets](tutorial-availability-sets.md) make it easier for you to maintain the virtual machines used by your application.</span></span>

<span data-ttu-id="5a75e-147">Para criar o conjunto de disponibilidade, adicione este código ao método Main:</span><span class="sxs-lookup"><span data-stu-id="5a75e-147">To create the availability set, add this code to the Main method:</span></span>

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-the-public-ip-address"></a><span data-ttu-id="5a75e-148">Criar um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="5a75e-148">Create the public IP address</span></span>

<span data-ttu-id="5a75e-149">Um [Endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) é necessário para se comunicar com a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5a75e-149">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed to communicate with the virtual machine.</span></span>

<span data-ttu-id="5a75e-150">Para criar o endereço IP público para a máquina virtual, adicione este código ao método Main:</span><span class="sxs-lookup"><span data-stu-id="5a75e-150">To create the public IP address for the virtual machine, add this code to the Main method:</span></span>
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-the-virtual-network"></a><span data-ttu-id="5a75e-151">Criar a rede virtual</span><span class="sxs-lookup"><span data-stu-id="5a75e-151">Create the virtual network</span></span>

<span data-ttu-id="5a75e-152">Uma máquina virtual precisa estar em uma sub-rede de uma [Rede virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5a75e-152">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="5a75e-153">Para criar uma sub-rede e uma rede virtual, adicione este código ao método Main:</span><span class="sxs-lookup"><span data-stu-id="5a75e-153">To create a subnet and a virtual network, add this code to the Main method:</span></span>

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-the-network-interface"></a><span data-ttu-id="5a75e-154">Criar a interface de rede</span><span class="sxs-lookup"><span data-stu-id="5a75e-154">Create the network interface</span></span>

<span data-ttu-id="5a75e-155">Uma máquina virtual precisa de uma interface de rede para se comunicar na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="5a75e-155">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

<span data-ttu-id="5a75e-156">Para criar um adaptador de rede, adicione este código ao método Main:</span><span class="sxs-lookup"><span data-stu-id="5a75e-156">To create a network interface, add this code to the Main method:</span></span>

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

### <a name="create-the-virtual-machine"></a><span data-ttu-id="5a75e-157">Criar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="5a75e-157">Create the virtual machine</span></span>

<span data-ttu-id="5a75e-158">Agora que você criou todos os recursos de suporte, você pode criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5a75e-158">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="5a75e-159">Para criar a máquina virtual, adicione este código ao método Main:</span><span class="sxs-lookup"><span data-stu-id="5a75e-159">To create the virtual machine, add this code to the Main method:</span></span>

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
> <span data-ttu-id="5a75e-160">Este tutorial cria uma máquina virtual executando uma versão do sistema operacional do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="5a75e-160">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="5a75e-161">Para saber mais sobre a seleção de outras imagens, veja [Navegar e selecionar imagens de máquina virtual do Azure com o Windows PowerShell e a CLI do Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5a75e-161">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="5a75e-162">Se você quiser usar um disco existente em vez de uma imagem do marketplace, use este código:</span><span class="sxs-lookup"><span data-stu-id="5a75e-162">If you want to use an existing disk instead of a marketplace image, use this code:</span></span>

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

## <a name="perform-management-tasks"></a><span data-ttu-id="5a75e-163">Executar tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="5a75e-163">Perform management tasks</span></span>

<span data-ttu-id="5a75e-164">Durante o ciclo de vida de uma máquina virtual, é possível que você queira executar tarefas de gerenciamento, como inicialização, interrupção ou exclusão de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5a75e-164">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="5a75e-165">Além disso, é possível que você queira criar um código para automatizar tarefas complexas ou repetitivas.</span><span class="sxs-lookup"><span data-stu-id="5a75e-165">Additionally, you may want to create code to automate repetitive or complex tasks.</span></span>

<span data-ttu-id="5a75e-166">Quando você precisa fazer alguma coisa com a VM, você precisa obter uma instância dela:</span><span class="sxs-lookup"><span data-stu-id="5a75e-166">When you need to do anything with the VM, you need to get an instance of it:</span></span>

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-the-vm"></a><span data-ttu-id="5a75e-167">Obter informações sobre a VM</span><span class="sxs-lookup"><span data-stu-id="5a75e-167">Get information about the VM</span></span>

<span data-ttu-id="5a75e-168">Para obter informações sobre a máquina virtual, adicione este código ao método Main:</span><span class="sxs-lookup"><span data-stu-id="5a75e-168">To get information about the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Getting information about the virtual machine...");
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
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="stop-the-vm"></a><span data-ttu-id="5a75e-169">Pare a VM.</span><span class="sxs-lookup"><span data-stu-id="5a75e-169">Stop the VM</span></span>

<span data-ttu-id="5a75e-170">Você pode parar uma máquina virtual e manter todas as suas configurações, mas continuará a ser cobrado por ela, ou pode parar uma máquina virtual e desalocá-la.</span><span class="sxs-lookup"><span data-stu-id="5a75e-170">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="5a75e-171">Quando uma máquina virtual é desalocada, todos os recursos associados a ela também são desalocadas e a cobrança para eles termina.</span><span class="sxs-lookup"><span data-stu-id="5a75e-171">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="5a75e-172">Para interromper a máquina virtual sem desalocá-la, adicione este código ao método Main:</span><span class="sxs-lookup"><span data-stu-id="5a75e-172">To stop the virtual machine without deallocating it, add this code to the Main method:</span></span>

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

<span data-ttu-id="5a75e-173">Se você desejar desalocar a máquina virtual, altere a chamada PowerOff para este código:</span><span class="sxs-lookup"><span data-stu-id="5a75e-173">If you want to deallocate the virtual machine, change the PowerOff call to this code:</span></span>

```
vm.Deallocate();
```

### <a name="start-the-vm"></a><span data-ttu-id="5a75e-174">Iniciar a VM</span><span class="sxs-lookup"><span data-stu-id="5a75e-174">Start the VM</span></span>

<span data-ttu-id="5a75e-175">Para iniciar a máquina virtual, adicione este código ao método Main:</span><span class="sxs-lookup"><span data-stu-id="5a75e-175">To start the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="resize-the-vm"></a><span data-ttu-id="5a75e-176">Redimensionar a VM</span><span class="sxs-lookup"><span data-stu-id="5a75e-176">Resize the VM</span></span>

<span data-ttu-id="5a75e-177">Muitos aspectos da implantação devem ser considerados ao decidir sobre um tamanho para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5a75e-177">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="5a75e-178">Para obter mais informações, consulte[Tamanhos de VM](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="5a75e-178">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="5a75e-179">Para alterar o tamanho da máquina virtual, adicione este código ao método Main:</span><span class="sxs-lookup"><span data-stu-id="5a75e-179">To change size of the virtual machine, add this code to the Main method:</span></span>

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter to continue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="5a75e-180">Adicionar um disco de dados à VM</span><span class="sxs-lookup"><span data-stu-id="5a75e-180">Add a data disk to the VM</span></span>

<span data-ttu-id="5a75e-181">Para adicionar um disco de dados à máquina virtual, adicione este código ao método Main para adicionar um disco de dados que tem tamanho de 2 GB, tem um LUN de 0 e um tipo de cache de ReadWrite:</span><span class="sxs-lookup"><span data-stu-id="5a75e-181">To add a data disk to the virtual machine, add this code to the Main method to add a data disk that is 2 GB in size, han a LUN of 0 and a caching type of ReadWrite:</span></span>

```
Console.WriteLine("Adding data disk to vm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter to delete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a><span data-ttu-id="5a75e-182">Excluir recursos</span><span class="sxs-lookup"><span data-stu-id="5a75e-182">Delete resources</span></span>

<span data-ttu-id="5a75e-183">Como você é cobrado pelos recursos utilizados no Azure, sempre é uma boa prática excluir os recursos que não são mais necessários.</span><span class="sxs-lookup"><span data-stu-id="5a75e-183">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="5a75e-184">Se você quiser excluir as máquinas virtuais e todos os recursos de suporte, tudo o que precisa fazer é excluir o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="5a75e-184">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

<span data-ttu-id="5a75e-185">Para excluir o grupo de recursos, adicione este código ao método Main:</span><span class="sxs-lookup"><span data-stu-id="5a75e-185">To delete the resource group, add this code to the Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-the-application"></a><span data-ttu-id="5a75e-186">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="5a75e-186">Run the application</span></span>

<span data-ttu-id="5a75e-187">Devem ser necessários cerca de cinco minutos para o aplicativo de console executar completamente do início ao fim.</span><span class="sxs-lookup"><span data-stu-id="5a75e-187">It should take about five minutes for this console application to run completely from start to finish.</span></span> 

1. <span data-ttu-id="5a75e-188">Para executar o aplicativo de console, clique em **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="5a75e-188">To run the console application, click **Start**.</span></span>

2. <span data-ttu-id="5a75e-189">Antes de pressionar **Enter** para iniciar a exclusão de recursos, reserve alguns minutos para verificar a criação dos recursos no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5a75e-189">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="5a75e-190">Clique no status de implantação para ver informações sobre a implantação.</span><span class="sxs-lookup"><span data-stu-id="5a75e-190">Click the deployment status to see information about the deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a75e-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a75e-191">Next steps</span></span>
* <span data-ttu-id="5a75e-192">Aproveite o uso de um modelo para criar uma máquina virtual usando as informações em [Implantar uma Máquina Virtual do Azure usando C# e um modelo do Resource Manager](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5a75e-192">Take advantage of using a template to create a virtual machine by using the information in [Deploy an Azure Virtual Machine using C# and a Resource Manager template](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="5a75e-193">Saiba mais sobre o uso das [Bibliotecas do Azure para .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="5a75e-193">Learn more about using the [Azure libraries for .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).</span></span>

