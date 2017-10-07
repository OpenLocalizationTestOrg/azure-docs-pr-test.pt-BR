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
# <a name="create-and-manage-windows-vms-in-azure-using-c"></a>Criar e gerenciar VMs Windows no Azure usando C# #

Uma [VM (Máquina Virtual) do Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) precisa de vários recursos do Azure de suporte. Este artigo aborda a criação, o gerenciamento e a exclusão de recursos de VM utilizando C#. Você aprenderá como:

> [!div class="checklist"]
> * Criar um projeto do Visual Studio
> * Instalar o pacote de saudação
> * Criar credenciais
> * Criar recursos
> * Executar tarefas de gerenciamento
> * Excluir recursos
> * Executar o aplicativo hello

Demora cerca de 20 minutos toodo essas etapas.

## <a name="create-a-visual-studio-project"></a>Criar um projeto do Visual Studio

1. Se você ainda não fez isso, instale o [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Selecione **desenvolvimento de área de trabalho do .NET** Olá página cargas de trabalho e, em seguida, clique em **instalar**. Olá resumo, você verá que **ferramentas de desenvolvimento do .NET Framework 4 4.6** é selecionado automaticamente para você. Se você já tiver instalado o Visual Studio, você pode adicionar carga de trabalho do .NET hello usando Olá iniciador do Visual Studio.
2. No Visual Studio, clique em **Arquivo** > **Novo** > **Projeto**.
3. Em **modelos** > **Visual C#**, selecione **aplicativo de Console (.NET Framework)**, digite *myDotnetProject* para nome de saudação do Olá projeto local selecione Olá Olá do projeto do e, em seguida, clique em **Okey**.

## <a name="install-hello-package"></a>Instalar o pacote de saudação

Pacotes do NuGet são Olá mais fácil maneira tooinstall Olá bibliotecas que você precisa toofinish essas etapas. bibliotecas de saudação tooget que você precisa no Visual Studio, siga estas etapas:

1. Clique em **Ferramentas** > **Gerenciador de Pacotes Nuget** e em **Console do Gerenciador de Pacotes**.
2. Digite este comando no console de saudação:

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    ```

## <a name="create-credentials"></a>Criar credenciais

Antes de iniciar esta etapa, certifique-se de que você tenha acesso tooan [entidade de serviço do Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Você também deve registrar a ID do aplicativo hello, chave de autenticação hello e ID de locatário Olá que você precisa em uma etapa posterior.

### <a name="create-hello-authorization-file"></a>Criar arquivo de autorização Olá

1. No Gerenciador de Soluções, clique com o botão direito do mouse em *myDotnetProject* > **Adicionar** > **Novo Item** e, em seguida, selecione **Arquivo de Texto** em *Itens do Visual C#*. Arquivo de saudação do nome *azureauth.properties*e, em seguida, clique em **adicionar**.
2. Adicione estas propriedades de autorização:

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

    Substituir  **&lt;id da assinatura&gt;**  com o identificador de assinatura,  **&lt;id do aplicativo&gt;**  com hello aplicativo do Active Directory identificador,  **&lt;chave de autenticação&gt;**  com chave de aplicativo hello, e  **&lt;id de locatário&gt;**  com locatário Olá identificador.

3. Salve o arquivo de azureauth.properties hello. 
4. Defina uma variável de ambiente no Windows chamado AZURE_AUTH_LOCATION com arquivo hello de tooauthorization de caminho completo que você criou. Por exemplo, a saudação comando PowerShell a seguir pode ser usada:

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```

### <a name="create-hello-management-client"></a>Crie saudação do cliente de gerenciamento

1. Abra o arquivo Program.cs Olá projeto Olá que você criou e, em seguida, adicioná-las usando toohello existente instruções na parte superior do arquivo hello:

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    ```

2. cliente de gerenciamento de saudação toocreate, adicione este código toohello método Main:

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-resources"></a>Criar recursos

### <a name="create-hello-resource-group"></a>Criar grupo de recursos de saudação

Todos os recursos devem estar contidos em um [Grupo de recursos](../../azure-resource-manager/resource-group-overview.md).

toospecify valores hello aplicativo e criar grupo de recursos de saudação, adicione este código toohello método Main:

```
var groupName = "myResourceGroup";
var vmName = "myVM";
var location = Region.USWest;
    
Console.WriteLine("Creating resource group...");
var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

### <a name="create-hello-availability-set"></a>Criar conjunto de disponibilidade Olá

[Conjuntos de disponibilidade](tutorial-availability-sets.md) tornar mais fácil para você toomaintain Olá VMs usados pelo seu aplicativo.

disponibilidade de saudação toocreate definido, adicione este código toohello método Main:

```
Console.WriteLine("Creating availability set...");
var availabilitySet = azure.AvailabilitySets.Define("myAVSet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithSku(AvailabilitySetSkuTypes.Managed)
    .Create();
```

### <a name="create-hello-public-ip-address"></a>Criar endereço IP público de saudação

Um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) é necessário toocommunicate com a máquina virtual de saudação.

toocreate Olá endereço IP público para a máquina virtual de Olá, adicione este código toohello método Main:
   
```
Console.WriteLine("Creating public IP address...");
var publicIPAddress = azure.PublicIPAddresses.Define("myPublicIP")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithDynamicIP()
    .Create();
```

### <a name="create-hello-virtual-network"></a>Criar rede virtual Olá

Uma máquina virtual precisa estar em uma sub-rede de uma [Rede virtual](../../virtual-network/virtual-networks-overview.md).

toocreate uma sub-rede e uma rede virtual, adicione este código toohello método Main:

```
Console.WriteLine("Creating virtual network...");
var network = azure.Networks.Define("myVNet")
    .WithRegion(location)
    .WithExistingResourceGroup(groupName)
    .WithAddressSpace("10.0.0.0/16")
    .WithSubnet("mySubnet", "10.0.0.0/24")
    .Create();
```

### <a name="create-hello-network-interface"></a>Criar a interface de rede Olá

Uma máquina virtual precisa de um toocommunicate de interface de rede na rede virtual hello.

toocreate uma interface de rede, adicione este código toohello método Main:

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

### <a name="create-hello-virtual-machine"></a>Criar a máquina virtual de saudação

Agora que você criou Olá todos os recursos de suporte, você pode criar uma máquina virtual.

toocreate Olá a máquina virtual, adicione este código toohello método Main:

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
> Este tutorial cria uma máquina virtual executando uma versão do sistema de operacional de servidor do Windows hello. toolearn mais sobre como selecionar outras imagens, consulte [navegue e selecione as imagens de máquina virtual do Azure com o Windows PowerShell e hello CLI do Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Se você quiser toouse um disco existente em vez de uma imagem do marketplace, use este código:

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

## <a name="perform-management-tasks"></a>Executar outras tarefas de gerenciamento

Durante a saudação do ciclo de vida de uma máquina virtual, talvez você queira toorun tarefas de gerenciamento como iniciar, parar ou excluir uma máquina virtual. Além disso, talvez você queira toocreate código tooautomate repetitivas ou complexas tarefas.

Quando você precisar toodo nada com hello VM, você precisa tooget uma instância dele:

```
var vm = azure.VirtualMachines.GetByResourceGroup(groupName, vmName);
```

### <a name="get-information-about-hello-vm"></a>Obter informações sobre Olá VM

tooget informações sobre a máquina virtual de hello, adicione este código toohello método Main:

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

### <a name="stop-hello-vm"></a>Parar Olá VM

Você pode parar uma máquina virtual e mantenha todas as suas configurações, mas continuar toobe cobrado por ele, ou você pode parar uma máquina virtual e desalocar a ele. Quando uma máquina virtual é desalocada, todos os recursos associados a ela também são desalocadas e a cobrança para eles termina.

máquina de virtual toostop Olá sem desalocá-lo, adicione toohello esse código método Main:

```
Console.WriteLine("Stopping vm...");
vm.PowerOff();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

Se você quiser toodeallocate Olá virtual machine, altere o código do hello desligado chamada toothis:

```
vm.Deallocate();
```

### <a name="start-hello-vm"></a>Olá iniciar VM

toostart Olá a máquina virtual, adicione este código toohello método Main:

```
Console.WriteLine("Starting vm...");
vm.Start();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="resize-hello-vm"></a>Redimensionar Olá VM

Muitos aspectos da implantação devem ser considerados ao decidir sobre um tamanho para sua máquina virtual. Para obter mais informações, consulte [Tamanhos de VM](sizes.md).  

toochange tamanho da máquina virtual de Olá, adicione este código toohello método Main:

```
Console.WriteLine("Resizing vm...");
vm.Update()
    .WithSize(VirtualMachineSizeTypes.StandardDS2) 
    .Apply();
Console.WriteLine("Press enter toocontinue...");
Console.ReadLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>Adicionar um disco de dados toohello VM

tooadd uma máquina de virtual de toohello de disco de dados, adicione este código toohello principal método tooadd um disco de dados que é 2 GB de tamanho, han um LUN de 0 e um tipo de cache de ReadWrite:

```
Console.WriteLine("Adding data disk toovm...");
vm.Update()
    .WithNewDataDisk(2, 0, CachingTypes.ReadWrite) 
    .Apply();
Console.WriteLine("Press enter toodelete resources...");
Console.ReadLine();
```

## <a name="delete-resources"></a>Excluir recursos

Como você é cobrado pelos recursos usados no Azure, é sempre recursos toodelete de práticas recomendadas que não são mais necessários. Se você quiser toodelete Olá VMs e Olá todos os recursos de suporte, você tem toodo é Olá exclusão do grupo de recursos.

recurso de saudação toodelete grupo, adicione este código toohello método Main:

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a>Executar o aplicativo hello

Ele deve levar cerca de cinco minutos para este toorun do aplicativo de console completamente do início toofinish. 

1. aplicativo de console hello toorun, clique em **iniciar**.

2. Antes de pressionar **Enter** toostart recursos de exclusão, você pode levar alguns minutos criação de saudação do tooverify de recursos de saudação em Olá portal do Azure. Clique em Olá implantação status toosee informações sobre a implantação de saudação.

## <a name="next-steps"></a>Próximas etapas
* Tirar proveito do uso de um modelo toocreate uma máquina virtual usando as informações de saudação em [implantar uma máquina Virtual do Azure usando o c# e um modelo do Gerenciador de recursos](csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Saiba mais sobre como usar o hello [bibliotecas do Azure para .NET](https://docs.microsoft.com/dotnet/azure/?view=azure-dotnet).

