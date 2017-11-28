---
title: "Criar e gerenciar uma Máquina Virtual do Azure usando o Java | Microsoft Docs"
description: "Use o Java e o Azure Resource Manager para implantar uma máquina virtual e todos os seus recursos de suporte."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: davidmu
ms.openlocfilehash: b9e739a07c5863577285fb3a221b372b385c6762
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a><span data-ttu-id="c3969-103">Criar e gerenciar VMs Windows no Azure usando o Java</span><span class="sxs-lookup"><span data-stu-id="c3969-103">Create and manage Windows VMs in Azure using Java</span></span>

<span data-ttu-id="c3969-104">Uma [VM (Máquina Virtual) do Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) precisa de vários recursos do Azure suporte.</span><span class="sxs-lookup"><span data-stu-id="c3969-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="c3969-105">Este artigo aborda a criação, o gerenciamento e a exclusão de recursos de VM usando o Java.</span><span class="sxs-lookup"><span data-stu-id="c3969-105">This article covers creating, managing, and deleting VM resources using Java.</span></span> <span data-ttu-id="c3969-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="c3969-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c3969-107">Criar um projeto Maven</span><span class="sxs-lookup"><span data-stu-id="c3969-107">Create a Maven project</span></span>
> * <span data-ttu-id="c3969-108">Adicionar dependências</span><span class="sxs-lookup"><span data-stu-id="c3969-108">Add dependencies</span></span>
> * <span data-ttu-id="c3969-109">Criar credenciais</span><span class="sxs-lookup"><span data-stu-id="c3969-109">Create credentials</span></span>
> * <span data-ttu-id="c3969-110">Criar recursos</span><span class="sxs-lookup"><span data-stu-id="c3969-110">Create resources</span></span>
> * <span data-ttu-id="c3969-111">Executar tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="c3969-111">Perform management tasks</span></span>
> * <span data-ttu-id="c3969-112">Excluir recursos</span><span class="sxs-lookup"><span data-stu-id="c3969-112">Delete resources</span></span>
> * <span data-ttu-id="c3969-113">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="c3969-113">Run the application</span></span>

<span data-ttu-id="c3969-114">São necessários cerca de 20 minutos para a conclusão destas etapas.</span><span class="sxs-lookup"><span data-stu-id="c3969-114">It takes about 20 minutes to do these steps.</span></span>

## <a name="create-a-maven-project"></a><span data-ttu-id="c3969-115">Criar um projeto Maven</span><span class="sxs-lookup"><span data-stu-id="c3969-115">Create a Maven project</span></span>

1. <span data-ttu-id="c3969-116">Se você ainda não fez isso, instale o [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="c3969-116">If you haven't already done so, install [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
2. <span data-ttu-id="c3969-117">Instale o [Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="c3969-117">Install [Maven](http://maven.apache.org/download.cgi).</span></span>
3. <span data-ttu-id="c3969-118">Crie uma nova pasta e o projeto:</span><span class="sxs-lookup"><span data-stu-id="c3969-118">Create a new folder and the project:</span></span>
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a><span data-ttu-id="c3969-119">Adicionar dependências</span><span class="sxs-lookup"><span data-stu-id="c3969-119">Add dependencies</span></span>

1. <span data-ttu-id="c3969-120">Na pasta `testAzureApp`, abra o arquivo `pom.xml` e adicione a configuração de build ao &lt;projeto&gt; para habilitar a criação do aplicativo:</span><span class="sxs-lookup"><span data-stu-id="c3969-120">Under the `testAzureApp` folder, open the `pom.xml` file and add the build configuration to &lt;project&gt; to enable the building of your application:</span></span>

    ```xml
    <build>
      <plugins>
        <plugin>
            <groupId>org.codehaus.mojo</groupId>
            <artifactId>exec-maven-plugin</artifactId>
            <configuration>
                <mainClass>com.fabrikam.testAzureApp.App</mainClass>
            </configuration>
        </plugin>
      </plugins>
    </build>
    ```

2. <span data-ttu-id="c3969-121">Adicione as dependências necessárias para acessar o SDK do Java do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3969-121">Add the dependencies that are needed to access the Azure Java SDK.</span></span>

    ```xml
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-compute</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-resources</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-mgmt-network</artifactId>
      <version>1.1.0</version>
    </dependency>
    <dependency>
      <groupId>com.squareup.okio</groupId>
      <artifactId>okio</artifactId>
      <version>1.13.0</version>
    </dependency>
    <dependency> 
      <groupId>com.nimbusds</groupId>
      <artifactId>nimbus-jose-jwt</artifactId>
      <version>3.6</version>
    </dependency>
    <dependency>
      <groupId>net.minidev</groupId>
      <artifactId>json-smart</artifactId>
      <version>1.0.6.3</version>
    </dependency>
    <dependency>
      <groupId>javax.mail</groupId>
      <artifactId>mail</artifactId>
      <version>1.4.5</version>
    </dependency>
    ```

3. <span data-ttu-id="c3969-122">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="c3969-122">Save the file.</span></span>

## <a name="create-credentials"></a><span data-ttu-id="c3969-123">Criar credenciais</span><span class="sxs-lookup"><span data-stu-id="c3969-123">Create credentials</span></span>

<span data-ttu-id="c3969-124">Antes de começar essa etapa, verifique se você tem acesso a uma [entidade de serviço do Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c3969-124">Before you start this step, make sure that you have access to an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="c3969-125">Além disso, registre o ID do aplicativo, a chave de autenticação e o ID do locatário que serão necessários em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="c3969-125">You should also record the application ID, the authentication key, and the tenant ID that you need in a later step.</span></span>

### <a name="create-the-authorization-file"></a><span data-ttu-id="c3969-126">Criar o arquivo de autorização</span><span class="sxs-lookup"><span data-stu-id="c3969-126">Create the authorization file</span></span>

1. <span data-ttu-id="c3969-127">Crie um arquivo chamado `azureauth.properties` e adicione estas propriedades a ele:</span><span class="sxs-lookup"><span data-stu-id="c3969-127">Create a file named `azureauth.properties` and add these properties to it:</span></span>

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

    <span data-ttu-id="c3969-128">Substitua **&lt;subscription-id&gt;** pelo identificador da assinatura, **&lt;application-id&gt;** pelo identificador de aplicativo do Active Directory, **&lt;authentication-key&gt;** pela chave do aplicativo e **&lt;tenant-id&gt;** pelo identificador do locatário.</span><span class="sxs-lookup"><span data-stu-id="c3969-128">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with the Active Directory application identifier, **&lt;authentication-key&gt;** with the application key, and **&lt;tenant-id&gt;** with the tenant identifier.</span></span>

2. <span data-ttu-id="c3969-129">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="c3969-129">Save the file.</span></span>
3. <span data-ttu-id="c3969-130">Defina uma variável de ambiente chamada AZURE_AUTH_LOCATION no shell com o caminho completo para o arquivo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="c3969-130">Set an environment variable named AZURE_AUTH_LOCATION in your shell with the full path to the authentication file.</span></span>

### <a name="create-the-management-client"></a><span data-ttu-id="c3969-131">Criar o cliente de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="c3969-131">Create the management client</span></span>

1. <span data-ttu-id="c3969-132">Abra o arquivo `App.java` em `src\main\java\com\fabrikam` e verifique se esta declaração de pacote está na parte superior:</span><span class="sxs-lookup"><span data-stu-id="c3969-132">Open the `App.java` file under `src\main\java\com\fabrikam` and make sure this package statement is at the top:</span></span>

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. <span data-ttu-id="c3969-133">Abaixo da declaração de pacote, adicione estas instruções de importação:</span><span class="sxs-lookup"><span data-stu-id="c3969-133">Under the package statement, add these import statements:</span></span>
   
    ```java
    import com.microsoft.azure.management.Azure;
    import com.microsoft.azure.management.compute.AvailabilitySet;
    import com.microsoft.azure.management.compute.AvailabilitySetSkuTypes;
    import com.microsoft.azure.management.compute.CachingTypes;
    import com.microsoft.azure.management.compute.InstanceViewStatus;
    import com.microsoft.azure.management.compute.DiskInstanceView;
    import com.microsoft.azure.management.compute.VirtualMachine;
    import com.microsoft.azure.management.compute.VirtualMachineSizeTypes;
    import com.microsoft.azure.management.network.PublicIPAddress;
    import com.microsoft.azure.management.network.Network;
    import com.microsoft.azure.management.network.NetworkInterface;
    import com.microsoft.azure.management.resources.ResourceGroup;
    import com.microsoft.azure.management.resources.fluentcore.arm.Region;
    import com.microsoft.azure.management.resources.fluentcore.model.Creatable;
    import com.microsoft.rest.LogLevel;
    import java.io.File;
    import java.util.Scanner;
    ```

2. <span data-ttu-id="c3969-134">Para criar as credenciais do Active Directory necessárias para fazer solicitações, adicione este código ao método principal da classe App:</span><span class="sxs-lookup"><span data-stu-id="c3969-134">To create the Active Directory credentials that you need to make requests, add this code to the main method of the App class:</span></span>
   
    ```java
    try {    
        final File credFile = new File(System.getenv("AZURE_AUTH_LOCATION"));
        Azure azure = Azure.configure()
            .withLogLevel(LogLevel.BASIC)
            .authenticate(credFile)
            .withDefaultSubscription();
    } catch (Exception e) {
        System.out.println(e.getMessage());
        e.printStackTrace();
    }

    ```

## <a name="create-resources"></a><span data-ttu-id="c3969-135">Criar recursos</span><span class="sxs-lookup"><span data-stu-id="c3969-135">Create resources</span></span>

### <a name="create-the-resource-group"></a><span data-ttu-id="c3969-136">Criar o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c3969-136">Create the resource group</span></span>

<span data-ttu-id="c3969-137">Todos os recursos devem estar contidos em um [Grupo de recursos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3969-137">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="c3969-138">Para especificar valores para o aplicativo e criar o grupo de recursos, adicione este código ao bloco try no método principal:</span><span class="sxs-lookup"><span data-stu-id="c3969-138">To specify values for the application and create the resource group, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-the-availability-set"></a><span data-ttu-id="c3969-139">Criar o conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="c3969-139">Create the availability set</span></span>

<span data-ttu-id="c3969-140">Os [conjuntos de disponibilidade](tutorial-availability-sets.md) facilitam a manutenção das máquinas virtuais usadas por seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c3969-140">[Availability sets](tutorial-availability-sets.md) make it easier for you to maintain the virtual machines used by your application.</span></span>

<span data-ttu-id="c3969-141">Para criar o conjunto de disponibilidade, adicione este código ao bloco try no método principal:</span><span class="sxs-lookup"><span data-stu-id="c3969-141">To create the availability set, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-the-public-ip-address"></a><span data-ttu-id="c3969-142">Criar um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="c3969-142">Create the public IP address</span></span>

<span data-ttu-id="c3969-143">Um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) é necessário para se comunicar com a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c3969-143">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed to communicate with the virtual machine.</span></span>

<span data-ttu-id="c3969-144">Para criar o endereço IP público para a máquina virtual, adicione este código ao bloco try no método principal:</span><span class="sxs-lookup"><span data-stu-id="c3969-144">To create the public IP address for the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-the-virtual-network"></a><span data-ttu-id="c3969-145">Criar a rede virtual</span><span class="sxs-lookup"><span data-stu-id="c3969-145">Create the virtual network</span></span>

<span data-ttu-id="c3969-146">Uma máquina virtual precisa estar em uma sub-rede de uma [Rede virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3969-146">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

<span data-ttu-id="c3969-147">Para criar uma sub-rede e uma rede virtual, adicione este código ao bloco try no método principal:</span><span class="sxs-lookup"><span data-stu-id="c3969-147">To create a subnet and a virtual network, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating virtual network...");
Network network = azure.networks()
    .define("myVN")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withAddressSpace("10.0.0.0/16")
    .withSubnet("mySubnet","10.0.0.0/24")
    .create();
```

### <a name="create-the-network-interface"></a><span data-ttu-id="c3969-148">Criar a interface de rede</span><span class="sxs-lookup"><span data-stu-id="c3969-148">Create the network interface</span></span>

<span data-ttu-id="c3969-149">Uma máquina virtual precisa de uma interface de rede para se comunicar na rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c3969-149">A virtual machine needs a network interface to communicate on the virtual network.</span></span>

<span data-ttu-id="c3969-150">Para criar um adaptador de rede, adicione este código ao bloco try no método principal:</span><span class="sxs-lookup"><span data-stu-id="c3969-150">To create a network interface, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating network interface...");
NetworkInterface networkInterface = azure.networkInterfaces()
    .define("myNIC")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetwork(network)
    .withSubnet("mySubnet")
    .withPrimaryPrivateIPAddressDynamic()
    .withExistingPrimaryPublicIPAddress(publicIPAddress)
    .create();
```

### <a name="create-the-virtual-machine"></a><span data-ttu-id="c3969-151">Criar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="c3969-151">Create the virtual machine</span></span>

<span data-ttu-id="c3969-152">Agora que você criou todos os recursos de suporte, você pode criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c3969-152">Now that you created all the supporting resources, you can create a virtual machine.</span></span>

<span data-ttu-id="c3969-153">Para criar a máquina virtual, adicione este código ao bloco try no método principal:</span><span class="sxs-lookup"><span data-stu-id="c3969-153">To create the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Creating virtual machine...");
VirtualMachine virtualMachine = azure.virtualMachines()
    .define("myVM")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("azureuser")
    .withAdminPassword("Azure12345678")
    .withComputerName("myVM")
    .withExistingAvailabilitySet(availabilitySet)
    .withSize("Standard_DS1")
    .create();
Scanner input = new Scanner(System.in);
System.out.println("Press enter to get information about the VM...");
input.nextLine();
```

> [!NOTE]
> <span data-ttu-id="c3969-154">Este tutorial cria uma máquina virtual executando uma versão do sistema operacional do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="c3969-154">This tutorial creates a virtual machine running a version of the Windows Server operating system.</span></span> <span data-ttu-id="c3969-155">Para saber mais sobre a seleção de outras imagens, veja [Navegar e selecionar imagens de máquina virtual do Azure com o Windows PowerShell e a CLI do Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c3969-155">To learn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and the Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
>

<span data-ttu-id="c3969-156">Se você quiser usar um disco existente em vez de uma imagem do marketplace, use este código:</span><span class="sxs-lookup"><span data-stu-id="c3969-156">If you want to use an existing disk instead of a marketplace image, use this code:</span></span> 

```java
ManagedDisk managedDisk = azure.disks.define("myosdisk") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withWindowsFromVhd("https://mystorage.blob.core.windows.net/vhds/myosdisk.vhd") 
    .withSizeInGB(128) 
    .withSku(DiskSkuTypes.PremiumLRS) 
    .create(); 

azure.virtualMachines.define("myVM") 
    .withRegion(Region.US_EAST) 
    .withExistingResourceGroup("myResourceGroup") 
    .withExistingPrimaryNetworkInterface(networkInterface) 
    .withSpecializedOSDisk(managedDisk, OperatingSystemTypes.Windows) 
    .withExistingAvailabilitySet(availabilitySet) 
    .withSize(VirtualMachineSizeTypes.StandardDS1) 
    .create(); 
``` 

## <a name="perform-management-tasks"></a><span data-ttu-id="c3969-157">Executar tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="c3969-157">Perform management tasks</span></span>

<span data-ttu-id="c3969-158">Durante o ciclo de vida de uma máquina virtual, é possível que você queira executar tarefas de gerenciamento, como inicialização, interrupção ou exclusão de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c3969-158">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="c3969-159">Além disso, é possível que você queira criar um código para automatizar tarefas complexas ou repetitivas.</span><span class="sxs-lookup"><span data-stu-id="c3969-159">Additionally, you may want to create code to automate repetitive or complex tasks.</span></span>

<span data-ttu-id="c3969-160">Quando você precisar fazer alguma coisa com a VM, precisará obter uma instância dela.</span><span class="sxs-lookup"><span data-stu-id="c3969-160">When you need to do anything with the VM, you need to get an instance of it.</span></span> <span data-ttu-id="c3969-161">Adicione este código ao bloco try do método principal:</span><span class="sxs-lookup"><span data-stu-id="c3969-161">Add this code to the try block of the main method:</span></span>

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-the-vm"></a><span data-ttu-id="c3969-162">Obter informações sobre a VM</span><span class="sxs-lookup"><span data-stu-id="c3969-162">Get information about the VM</span></span>

<span data-ttu-id="c3969-163">Para obter informações sobre a máquina virtual, adicione este código ao bloco try no método principal:</span><span class="sxs-lookup"><span data-stu-id="c3969-163">To get information about the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("hardwareProfile");
System.out.println("    vmSize: " + vm.size());
System.out.println("storageProfile");
System.out.println("  imageReference");
System.out.println("    publisher: " + vm.storageProfile().imageReference().publisher());
System.out.println("    offer: " + vm.storageProfile().imageReference().offer());
System.out.println("    sku: " + vm.storageProfile().imageReference().sku());
System.out.println("    version: " + vm.storageProfile().imageReference().version());
System.out.println("  osDisk");
System.out.println("    osType: " + vm.storageProfile().osDisk().osType());
System.out.println("    name: " + vm.storageProfile().osDisk().name());
System.out.println("    createOption: " + vm.storageProfile().osDisk().createOption());
System.out.println("    caching: " + vm.storageProfile().osDisk().caching());
System.out.println("osProfile");
System.out.println("    computerName: " + vm.osProfile().computerName());
System.out.println("    adminUserName: " + vm.osProfile().adminUsername());
System.out.println("    provisionVMAgent: " + vm.osProfile().windowsConfiguration().provisionVMAgent());
System.out.println("    enableAutomaticUpdates: " + vm.osProfile().windowsConfiguration().enableAutomaticUpdates());
System.out.println("networkProfile");
System.out.println("    networkInterface: " + vm.primaryNetworkInterfaceId());
System.out.println("vmAgent");
System.out.println("  vmAgentVersion: " + vm.instanceView().vmAgent().vmAgentVersion());
System.out.println("    statuses");
for(InstanceViewStatus status : vm.instanceView().vmAgent().statuses()) {
    System.out.println("    code: " + status.code());
    System.out.println("    displayStatus: " + status.displayStatus());
    System.out.println("    message: " + status.message());
    System.out.println("    time: " + status.time());
}
System.out.println("disks");
for(DiskInstanceView disk : vm.instanceView().disks()) {
    System.out.println("  name: " + disk.name());
    System.out.println("  statuses");
    for(InstanceViewStatus status : disk.statuses()) {
        System.out.println("    code: " + status.code());
        System.out.println("    displayStatus: " + status.displayStatus());
        System.out.println("    time: " + status.time());
    }
}
System.out.println("VM general status");
System.out.println("  provisioningStatus: " + vm.provisioningState());
System.out.println("  id: " + vm.id());
System.out.println("  name: " + vm.name());
System.out.println("  type: " + vm.type());
System.out.println("VM instance status");
for(InstanceViewStatus status : vm.instanceView().statuses()) {
    System.out.println("  code: " + status.code());
    System.out.println("  displayStatus: " + status.displayStatus());
}
System.out.println("Press enter to continue...");
input.nextLine();   
```

### <a name="stop-the-vm"></a><span data-ttu-id="c3969-164">Pare a VM.</span><span class="sxs-lookup"><span data-stu-id="c3969-164">Stop the VM</span></span>

<span data-ttu-id="c3969-165">Você pode parar uma máquina virtual e manter todas as suas configurações, mas continuará a ser cobrado por ela, ou pode parar uma máquina virtual e desalocá-la.</span><span class="sxs-lookup"><span data-stu-id="c3969-165">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="c3969-166">Quando uma máquina virtual é desalocada, todos os recursos associados a ela também são desalocadas e a cobrança para eles termina.</span><span class="sxs-lookup"><span data-stu-id="c3969-166">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

<span data-ttu-id="c3969-167">Para interromper a máquina virtual sem desalocá-la, adicione este código ao bloco try no método principal:</span><span class="sxs-lookup"><span data-stu-id="c3969-167">To stop the virtual machine without deallocating it, add this code to the try block in the main method:</span></span>

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter to continue...");
input.nextLine();
```

<span data-ttu-id="c3969-168">Se você desejar desalocar a máquina virtual, altere a chamada PowerOff para este código:</span><span class="sxs-lookup"><span data-stu-id="c3969-168">If you want to deallocate the virtual machine, change the PowerOff call to this code:</span></span>

```java
vm.deallocate();
```

### <a name="start-the-vm"></a><span data-ttu-id="c3969-169">Iniciar a VM</span><span class="sxs-lookup"><span data-stu-id="c3969-169">Start the VM</span></span>

<span data-ttu-id="c3969-170">Para iniciar a máquina virtual, adicione este código ao bloco try no método principal:</span><span class="sxs-lookup"><span data-stu-id="c3969-170">To start the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter to continue...");
input.nextLine();
```

### <a name="resize-the-vm"></a><span data-ttu-id="c3969-171">Redimensionar a VM</span><span class="sxs-lookup"><span data-stu-id="c3969-171">Resize the VM</span></span>

<span data-ttu-id="c3969-172">Muitos aspectos da implantação devem ser considerados ao decidir sobre um tamanho para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c3969-172">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="c3969-173">Para obter mais informações, consulte [Tamanhos de VM](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="c3969-173">For more information, see [VM sizes](sizes.md).</span></span>  

<span data-ttu-id="c3969-174">Para alterar o tamanho da máquina virtual, adicione este código ao bloco try no método principal:</span><span class="sxs-lookup"><span data-stu-id="c3969-174">To change size of the virtual machine, add this code to the try block in the main method:</span></span>

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter to continue...");
input.nextLine();
```

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="c3969-175">Adicionar um disco de dados à VM</span><span class="sxs-lookup"><span data-stu-id="c3969-175">Add a data disk to the VM</span></span>

<span data-ttu-id="c3969-176">Para adicionar um disco de dados à máquina virtual que tem 2 GB de tamanho, um LUN igual a 0 e um tipo de cache ReadWrite, adicione este código ao bloco try no método principal:</span><span class="sxs-lookup"><span data-stu-id="c3969-176">To add a data disk to the virtual machine that is 2 GB in size, has a LUN of 0, and a caching type of ReadWrite, add this code to the try block in the main method:</span></span>

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter to delete resources...");
input.nextLine();
```

## <a name="delete-resources"></a><span data-ttu-id="c3969-177">Excluir recursos</span><span class="sxs-lookup"><span data-stu-id="c3969-177">Delete resources</span></span>

<span data-ttu-id="c3969-178">Como você é cobrado pelos recursos utilizados no Azure, sempre é uma boa prática excluir os recursos que não são mais necessários.</span><span class="sxs-lookup"><span data-stu-id="c3969-178">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="c3969-179">Se você quiser excluir as máquinas virtuais e todos os recursos de suporte, tudo o que precisa fazer é excluir o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c3969-179">If you want to delete the virtual machines and all the supporting resources, all you have to do is delete the resource group.</span></span>

1. <span data-ttu-id="c3969-180">Para excluir o grupo de recursos, adicione este código ao bloco try no método principal:</span><span class="sxs-lookup"><span data-stu-id="c3969-180">To delete the resource group, add this code to the try block in the main method:</span></span>
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. <span data-ttu-id="c3969-181">Salve o arquivo App.java.</span><span class="sxs-lookup"><span data-stu-id="c3969-181">Save the App.java file.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="c3969-182">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="c3969-182">Run the application</span></span>

<span data-ttu-id="c3969-183">Devem ser necessários cerca de cinco minutos para o aplicativo de console executar completamente do início ao fim.</span><span class="sxs-lookup"><span data-stu-id="c3969-183">It should take about five minutes for this console application to run completely from start to finish.</span></span>

1. <span data-ttu-id="c3969-184">Para executar o aplicativo, use este comando do Maven:</span><span class="sxs-lookup"><span data-stu-id="c3969-184">To run the application, use this Maven command:</span></span>

    ```
    mvn compile exec:java
    ```

2. <span data-ttu-id="c3969-185">Antes de pressionar **Enter** para iniciar a exclusão de recursos, reserve alguns minutos para verificar a criação dos recursos no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3969-185">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="c3969-186">Clique no status de implantação para ver informações sobre a implantação.</span><span class="sxs-lookup"><span data-stu-id="c3969-186">Click the deployment status to see information about the deployment.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c3969-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c3969-187">Next steps</span></span>
* <span data-ttu-id="c3969-188">Saiba mais sobre como usar as [bibliotecas do Azure para Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span><span class="sxs-lookup"><span data-stu-id="c3969-188">Learn more about using the [Azure libraries for Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).</span></span>

