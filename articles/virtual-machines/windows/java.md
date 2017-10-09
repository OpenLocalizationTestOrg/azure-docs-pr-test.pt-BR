---
title: "aaaCreate e gerenciar um Azure Máquina Virtual usando o Java | Microsoft Docs"
description: "Use o Java e o Azure Resource Manager toodeploy uma máquina virtual e todos os seus recursos de suporte."
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
ms.openlocfilehash: 31ac8d59f92ecff887e64906940933dd6fd50815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-java"></a>Criar e gerenciar VMs Windows no Azure usando o Java

Uma [VM (Máquina Virtual) do Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) precisa de vários recursos do Azure suporte. Este artigo aborda a criação, o gerenciamento e a exclusão de recursos de VM usando o Java. Você aprenderá como:

> [!div class="checklist"]
> * Criar um projeto Maven
> * Adicionar dependências
> * Criar credenciais
> * Criar recursos
> * Executar tarefas de gerenciamento
> * Excluir recursos
> * Executar o aplicativo hello

Demora cerca de 20 minutos toodo essas etapas.

## <a name="create-a-maven-project"></a>Criar um projeto Maven

1. Se você ainda não fez isso, instale o [Java](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
2. Instale o [Maven](http://maven.apache.org/download.cgi).
3. Crie um novo projeto de pasta e hello:
    
    ```
    mkdir java-azure-test
    cd java-azure-test
    
    mvn archetype:generate -DgroupId=com.fabrikam -DartifactId=testAzureApp -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
    ```

## <a name="add-dependencies"></a>Adicionar dependências

1. Em Olá `testAzureApp` pasta, abra Olá `pom.xml` de arquivo e adicione uma configuração de compilação de saudação muito&lt;projeto&gt; tooenable construção de saudação do seu aplicativo:

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

2. Adicione dependências Olá Olá tooaccess necessário SDK de Java do Azure.

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

3. Salve o arquivo hello.

## <a name="create-credentials"></a>Criar credenciais

Antes de iniciar esta etapa, certifique-se de que você tenha acesso tooan [entidade de serviço do Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Você também deve registrar a ID do aplicativo hello, chave de autenticação hello e ID de locatário Olá que você precisa em uma etapa posterior.

### <a name="create-hello-authorization-file"></a>Criar arquivo de autorização Olá

1. Crie um arquivo chamado `azureauth.properties` e adicione tooit essas propriedades:

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

2. Salve o arquivo hello.
3. Defina uma variável de ambiente denominada AZURE_AUTH_LOCATION no shell com o arquivo de autenticação de toohello Olá caminho completo.

### <a name="create-hello-management-client"></a>Crie saudação do cliente de gerenciamento

1. Olá abrir `App.java` arquivo sob `src\main\java\com\fabrikam` e verifique se essa instrução de pacote está na parte superior da saudação:

    ```java
    package com.fabrikam.testAzureApp;
    ```

2. Na instrução de pacote hello, adicione estas instruções de importação:
   
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

2. credenciais do Active Directory Olá toocreate que você precisa de solicitações de toomake, adicione esse código toohello principal método hello classe App:
   
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

## <a name="create-resources"></a>Criar recursos

### <a name="create-hello-resource-group"></a>Criar grupo de recursos de saudação

Todos os recursos devem estar contidos em um [Grupo de recursos](../../azure-resource-manager/resource-group-overview.md).

toospecify valores hello aplicativo e criar grupo de recursos de saudação, adicione este bloco de try toohello código no método main hello:

```java
System.out.println("Creating resource group...");
ResourceGroup resourceGroup = azure.resourceGroups()
    .define("myResourceGroup")
    .withRegion(Region.US_EAST)
    .create();
```

### <a name="create-hello-availability-set"></a>Criar conjunto de disponibilidade Olá

[Conjuntos de disponibilidade](tutorial-availability-sets.md) tornar mais fácil para você toomaintain Olá VMs usados pelo seu aplicativo.

disponibilidade de saudação toocreate definido, adicione este bloco de try toohello código no método main hello:

```java
System.out.println("Creating availability set...");
AvailabilitySet availabilitySet = azure.availabilitySets()
    .define("myAvailabilitySet")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withSku(AvailabilitySetSkuTypes.MANAGED)
    .create();
```
### <a name="create-hello-public-ip-address"></a>Criar endereço IP público de saudação

Um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) é necessário toocommunicate com a máquina virtual de saudação.

toocreate Olá endereço IP público para a máquina virtual de Olá, adicione este bloco de try toohello código no método main hello:

```java
System.out.println("Creating public IP address...");
PublicIPAddress publicIPAddress = azure.publicIPAddresses()
    .define("myPublicIP")
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("myResourceGroup")
    .withDynamicIP()
    .create();
```

### <a name="create-hello-virtual-network"></a>Criar rede virtual Olá

Uma máquina virtual precisa estar em uma sub-rede de uma [Rede virtual](../../virtual-network/virtual-networks-overview.md).

toocreate uma sub-rede e uma rede virtual, adicione este bloco de try toohello código no método main hello:

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

### <a name="create-hello-network-interface"></a>Criar a interface de rede Olá

Uma máquina virtual precisa de um toocommunicate de interface de rede na rede virtual hello.

toocreate uma interface de rede, adicione este bloco de try toohello código no método main hello:

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

### <a name="create-hello-virtual-machine"></a>Criar a máquina virtual de saudação

Agora que você criou Olá todos os recursos de suporte, você pode criar uma máquina virtual.

toocreate Olá a máquina virtual, adicione este bloco de try toohello código no método main hello:

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
System.out.println("Press enter tooget information about hello VM...");
input.nextLine();
```

> [!NOTE]
> Este tutorial cria uma máquina virtual executando uma versão do sistema de operacional de servidor do Windows hello. toolearn mais sobre como selecionar outras imagens, consulte [navegue e selecione as imagens de máquina virtual do Azure com o Windows PowerShell e hello CLI do Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
>

Se você quiser toouse um disco existente em vez de uma imagem do marketplace, use este código: 

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

## <a name="perform-management-tasks"></a>Executar outras tarefas de gerenciamento

Durante a saudação do ciclo de vida de uma máquina virtual, talvez você queira toorun tarefas de gerenciamento como iniciar, parar ou excluir uma máquina virtual. Além disso, talvez você queira toocreate código tooautomate repetitivas ou complexas tarefas.

Quando você precisar toodo nada com hello VM, você precisa tooget uma instância dele. Adicione este bloco de tente toohello código do método principal hello:

```java
VirtualMachine vm = azure.virtualMachines().getByResourceGroup("myResourceGroup", "myVM");
```

### <a name="get-information-about-hello-vm"></a>Obter informações sobre Olá VM

tooget informações sobre a máquina virtual de Olá, adicione este bloco de try toohello código no método main hello:

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
System.out.println("Press enter toocontinue...");
input.nextLine();   
```

### <a name="stop-hello-vm"></a>Parar Olá VM

Você pode parar uma máquina virtual e mantenha todas as suas configurações, mas continuar toobe cobrado por ele, ou você pode parar uma máquina virtual e desalocar a ele. Quando uma máquina virtual é desalocada, todos os recursos associados a ela também são desalocadas e a cobrança para eles termina.

toostop Olá VM sem desalocá-lo, adicionar esse bloco de try toohello código no método main hello:

```java
System.out.println("Stopping vm...");
vm.powerOff();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

Se você quiser toodeallocate Olá virtual machine, altere o código do hello desligado chamada toothis:

```java
vm.deallocate();
```

### <a name="start-hello-vm"></a>Olá iniciar VM

toostart Olá a máquina virtual, adicione este bloco de try toohello código no método main hello:

```java
System.out.println("Starting vm...");
vm.start();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="resize-hello-vm"></a>Redimensionar Olá VM

Muitos aspectos da implantação devem ser considerados ao decidir sobre um tamanho para sua máquina virtual. Para obter mais informações, consulte [Tamanhos de VM](sizes.md).  

toochange tamanho da máquina virtual de Olá, adicione este bloco de try toohello código no método main hello:

```java
System.out.println("Resizing vm...");
vm.update()
    .withSize(VirtualMachineSizeTypes.STANDARD_DS2)
    .apply();
System.out.println("Press enter toocontinue...");
input.nextLine();
```

### <a name="add-a-data-disk-toohello-vm"></a>Adicionar um disco de dados toohello VM

tooadd uma máquina de virtual de toohello disco de dados que é 2 GB de tamanho, tem um LUN de 0 e um tipo de cache de ReadWrite, adicione este bloco de try toohello código no método main hello:

```java
System.out.println("Adding data disk...");
vm.update()
    .withNewDataDisk(2, 0, CachingTypes.READ_WRITE)
    .apply();
System.out.println("Press enter toodelete resources...");
input.nextLine();
```

## <a name="delete-resources"></a>Excluir recursos

Como você é cobrado pelos recursos usados no Azure, é sempre recursos toodelete de práticas recomendadas que não são mais necessários. Se você quiser toodelete Olá VMs e Olá todos os recursos de suporte, você tem toodo é Olá exclusão do grupo de recursos.

1. recurso de saudação toodelete grupo, adicione este bloco de try toohello código no método main hello:
   
```java
System.out.println("Deleting resources...");
azure.resourceGroups().deleteByName("myResourceGroup");
```

2. Salve o arquivo de App.java hello.

## <a name="run-hello-application"></a>Executar o aplicativo hello

Ele deve levar cerca de cinco minutos para este toorun do aplicativo de console completamente do início toofinish.

1. toorun Olá aplicativo, use este comando Maven:

    ```
    mvn compile exec:java
    ```

2. Antes de pressionar **Enter** toostart recursos de exclusão, você pode levar alguns minutos criação de saudação do tooverify de recursos de saudação em Olá portal do Azure. Clique em Olá implantação status toosee informações sobre a implantação de saudação.


## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre como usar o hello [bibliotecas do Azure para Java](https://docs.microsoft.com/en-us/java/azure/java-sdk-azure-overview).

