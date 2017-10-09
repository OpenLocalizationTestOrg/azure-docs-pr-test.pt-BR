
* [Criar rapidamente uma máquina virtual no Azure](#quick-create-a-vm-in-azure)
* [Implantar uma máquina virtual no Azure com base em um modelo](#deploy-a-vm-in-azure-from-a-template)
* [Criar uma máquina virtual com base em uma imagem personalizada](#create-a-custom-vm-image)
* [Implantar uma máquina virtual que usa uma rede virtual e um balanceador de carga](#deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer)
* [Remover um grupo de recursos](#remove-a-resource-group)
* [Mostrar log Olá para uma implantação de grupo de recursos](#show-the-log-for-a-resource-group-deployment)
* [Exibir informações sobre uma máquina virtual](#display-information-about-a-virtual-machine)
* [Conecte-se a máquina virtual baseados em Linux de tooa](#log-on-to-a-linux-based-virtual-machine)
* [Parar uma máquina virtual](#stop-a-virtual-machine)
* [Iniciar uma máquina virtual](#start-a-virtual-machine)
* [Anexar um disco de dados](#attach-a-data-disk)

## <a name="getting-ready"></a>Preparando-se
Antes de usar Olá CLI do Azure com grupos de recursos do Azure, você precisará versão toohave Olá de direito CLI do Azure e uma conta do Azure. Se você não tiver Olá CLI do Azure, [instalá-lo](../articles/cli-install-nodejs.md).

### <a name="update-your-azure-cli-version-too090-or-later"></a>Atualizar seu too0.9.0 de versão da CLI do Azure ou posterior
Tipo `azure --version` toosee se você já tiver instalado a versão 0.9.0 ou posterior.

```azurecli
azure --version
0.9.0 (node: 0.10.25)
```

Se sua versão não é 0.9.0 ou posterior, você precisa tooupdate-lo usando um dos Olá instaladores nativo ou por meio **npm** digitando `npm update -g azure-cli`.

Você também pode executar CLI do Azure como um contêiner do Docker usando o seguinte Olá [imagem Docker](https://registry.hub.docker.com/u/microsoft/azure-cli/). Em um host Docker, execute Olá comando a seguir:

```bash
docker run -it microsoft/azure-cli
```

### <a name="set-your-azure-account-and-subscription"></a>Definir sua conta e assinatura do Azure
Se ainda não tiver uma assinatura do Azure, mas tiver uma assinatura do MSDN, você poderá ativar seus [benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). Ou então, você poderá se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).

Agora [login tooyour conta do Azure interativamente](../articles/xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login) digitando `azure login` e seguir Olá solicitará uma experiência de logon interativo tooyour conta do Azure. 

> [!NOTE]
> Se você tem um trabalho ou de estudante ID e você sabe que você não tenha habilitada de autenticação de dois fatores, você pode **também** usar `azure login -u` juntamente com hello ou de estudante toolog ID em *sem* uma sessão interativa. Se você não tem um trabalho ou de estudante ID, você pode [criar uma id de trabalho ou da escola de sua conta pessoal da Microsoft](../articles/virtual-machines/windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toolog em Olá mesma maneira.
>
>

Sua conta pode ter mais de uma assinatura. Você pode listar suas assinaturas digitando `azure account list`, que pode ser semelhante a:

```azurecli
azure account list
info:    Executing command account list
data:    Name                              Id                                    Tenant Id                            Current
data:    --------------------------------  ------------------------------------  ------------------------------------  -------
data:    Contoso Admin                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  true
data:    Fabrikam dev                      xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Fabrikam test                     xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
data:    Contoso production                xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx  false  
```

Você pode definir a assinatura do Azure Olá digitando o seguinte hello. Use Olá nome ou hello ID de assinatura que tem recursos de saudação deseja toomanage.

```azurecli
azure account set <subscription name or ID> true
```

### <a name="switch-toohello-azure-cli-resource-group-mode"></a>Alternar o modo de grupo de recursos toohello CLI do Azure
Por padrão, a saudação CLI do Azure inicia no modo de gerenciamento de serviço de saudação (**asm** modo). Digite hello modo de grupo de tooresource tooswitch a seguir.

```azurecli
azure config mode arm
```

## <a name="understanding-azure-resource-templates-and-resource-groups"></a>Noções básicas sobre grupos de recursos e modelos de recursos do Azure
A maioria dos aplicativos é criada a partir de uma combinação de diferentes tipos de recursos (como uma ou mais VMs e contas de Armazenamento, um banco de dados SQL, uma Rede Virtual ou uma rede de transmissão de conteúdo). Olá API de gerenciamento de serviço do Azure padrão e hello portal clássico do Azure representado esses itens usando uma abordagem pelo serviço. Essa abordagem requer que você toodeploy e gerenciar serviços individuais Olá individualmente (ou localizar outras ferramentas que fazem-lo) e não como uma única unidade lógica de implantação.

*Modelos do Gerenciador de recursos do Azure*, no entanto, possibilitam que você toodeploy e gerenciar esses recursos diferentes, como uma unidade lógica de implantação de forma declarativa. Em vez de imperativa informando do Azure que toodeploy um comando após o outro, você descreve sua implantação completa em um arquivo JSON – todos os recursos de saudação e configurações associadas e parâmetros de implantação – e informar o Azure toodeploy esses recursos como um grupo.

Você pode gerenciar Olá ciclo de vida geral de recursos do grupo hello usando comandos de gerenciamento de recursos de CLI do Azure para:

* Parar, iniciar ou excluir todos os recursos de saudação dentro do grupo de saudação de uma vez.
* Aplique toolock de regras de controle de acesso baseado em função (RBAC) permissões de segurança-los.
* Auditar operações.
* Marcar recursos com metadados extras para ter melhor acompanhamento.

Você pode aprender muito mais sobre grupos de recursos do Azure e o que eles podem fazer para você no hello [visão geral do Gerenciador de recursos do Azure](../articles/azure-resource-manager/resource-group-overview.md). Se você estiver interessado na criação de modelos, confira [Criando modelos do Gerenciador de Recursos do Azure](../articles/resource-group-authoring-templates.md).

## <a id="quick-create-a-vm-in-azure"></a>Tarefa: Criar rapidamente uma VM no Azure
Às vezes, você sabe quais imagem que você precisa, e você precisa de uma VM da imagem agora e não se preocupar muito infraestrutura Olá - talvez você tenha tootest algo em uma VM limpa. Ou seja, quando você deseja Olá toouse `azure vm quick-create` de comando e passe Olá argumentos necessários toocreate uma máquina virtual e sua infraestrutura.

Em primeiro lugar, crie o grupo de recursos.

```azurecli
azure group create coreos-quick westus
info:    Executing command group create
+ Getting resource group coreos-quick
+ Creating resource group coreos-quick
info:    Created resource group coreos-quick
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick
data:    Name:                coreos-quick
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

Em segundo lugar, você precisará de uma imagem. toofind uma imagem com hello CLI do Azure, consulte [Navegando e selecionando imagens de máquina virtual do Azure com o PowerShell e Olá CLI do Azure](../articles/virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Porém, para este artigo, aqui está uma pequena lista de imagens populares. Vamos usar a imagem estável do CoreOS para esta criação rápida.

> [!NOTE]
> Para ComputeImageVersion, você pode simplesmente fornecer 'último' como Olá parâmetro em ambas as linguagem de modelo Olá em Olá CLI do Azure. Isso permitirá que você tooalways usar hello mais recente e corrigida versão da imagem de saudação sem ter que toomodify seus scripts ou modelos. Isso é mostrado abaixo.
>
>

| PublisherName | Oferta | Sku | Versão |
|:--- |:--- |:--- |:--- |
| OpenLogic |CentOS |7 |7.0.201503 |
| OpenLogic |CentOS |7.1 |7.1.201504 |
| CoreOS |CoreOS |Beta |647.0.0 |
| CoreOS |CoreOS |Estável |633.1.0 |
| MicrosoftDynamicsNAV |DynamicsNAV |2015 |8.0.40459 |
| MicrosoftSharePoint |MicrosoftSharePointServer |2013 |1.0.0 |
| msopentech |Oracle-Database-12c-Weblogic-Server-12c |Standard |1.0.0 |
| msopentech |Oracle-Database-12c-Weblogic-Server-12c |Enterprise |1.0.0 |
| MicrosoftSQLServer |SQL2014-WS2012R2 |Enterprise-Optimized-for-DW |12.0.2430 |
| MicrosoftSQLServer |SQL2014-WS2012R2 |Enterprise-Optimized-for-OLTP |12.0.2430 |
| Canônico |UbuntuServer |12.04.5-LTS |12.04.201504230 |
| Canônico |UbuntuServer |14.04.2-LTS |14.04.201503090 |
| MicrosoftWindowsServer |WindowsServer |2012-Datacenter |3.0.201503 |
| MicrosoftWindowsServer |WindowsServer |2012-R2-Datacenter |4.0.201503 |
| MicrosoftWindowsServer |WindowsServer |Windows-Server-Technical-Preview |5.0.201504 |
| MicrosoftWindowsServerEssentials |WindowsServerEssentials |WindowsServerEssentials |1.0.141204 |
| MicrosoftWindowsServerHPCPack |WindowsServerHPCPack |2012R2 |4.3.4665 |

Crie sua VM inserindo Olá `azure vm quick-create` comando e a se preparar para Olá prompts. O resultado deve ser semelhante a esse:

```azurecli
azure vm quick-create
info:    Executing command vm quick-create
Resource group name: coreos-quick
Virtual machine name: coreos
Location name: westus
Operating system Type [Windows, Linux]: linux
ImageURN (format: "publisherName:offer:skus:version"): coreos:coreos:stable:latest
User name: ops
Password: *********
Confirm password: *********
+ Looking up hello VM "coreos"
info:    Using hello VM Size "Standard_A1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Retrieving storage accounts
info:    Could not find any storage accounts in hello region "westus", trying toocreate new one
+ Creating storage account "cli9fd3fce49e9a9b3d14302" in "westus"
+ Looking up hello storage account cli9fd3fce49e9a9b3d14302
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
info:    An nic with given name "coreo-westu-1430261891570-nic" not found, creating a new one
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
info:    Preparing toocreate new virtual network and subnet
/ Creating a new virtual network "coreo-westu-1430261891570-vnet" [address prefix: "10.0.0.0/16"] with subnet "coreo-westu-1430261891570-sne+" [address prefix: "10.0.1.0/24"]
+ Looking up hello virtual network "coreo-westu-1430261891570-vnet"
+ Looking up hello subnet "coreo-westu-1430261891570-snet" under hello virtual network "coreo-westu-1430261891570-vnet"
info:    Found public ip parameters, trying toosetup PublicIP profile
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
info:    PublicIP with given name "coreo-westu-1430261891570-pip" not found, creating a new one
+ Creating public ip "coreo-westu-1430261891570-pip"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
+ Creating NIC "coreo-westu-1430261891570-nic"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Creating VM "coreos"
+ Looking up hello VM "coreos"
+ Looking up hello NIC "coreo-westu-1430261891570-nic"
+ Looking up hello public ip "coreo-westu-1430261891570-pip"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Compute/virtualMachines/coreos
data:    ProvisioningState               :Succeeded
data:    Name                            :coreos
data:    Location                        :westus
data:    FQDN                            :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :coreos
data:        Offer                       :coreos
data:        Sku                         :stable
data:        Version                     :633.1.0
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :cli9fd3fce49e9a9b3d-os-1430261892283
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://cli9fd3fce49e9a9b3d14302.blob.core.windows.net/vhds/cli9fd3fce49e9a9b3d-os-1430261892283.vhd
data:
data:    OS Profile:
data:      Computer Name                 :coreos
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :false
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/coreos-quick/providers/Microsoft.Network/networkInterfaces/coreo-westu-1430261891570-nic
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-30-72-E3
data:          Provisioning State        :Succeeded
data:          Name                      :coreo-westu-1430261891570-nic
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.1.4
data:            Public IP address       :104.40.24.124
data:            FQDN                    :coreo-westu-1430261891570-pip.westus.cloudapp.azure.com
info:    vm quick-create command OK
```

E, assim, você obtém sua nova VM.

## <a id="deploy-a-vm-in-azure-from-a-template"></a>Tarefa: implantar uma VM no Azure a partir de um modelo
Use as instruções de saudação toodeploy essas seções uma nova VM do Azure usando um modelo com hello CLI do Azure. Este modelo cria uma única máquina virtual em uma nova rede virtual com uma única sub-rede e, diferentemente do `azure vm quick-create`, permite que você toodescribe o que você deseja com precisão e repeti-la sem erros. Aqui está o que o modelo cria:

![](./media/virtual-machines-common-cli-deploy-templates/new-vm.png)

### <a name="step-1-examine-hello-json-file-for-hello-template-parameters"></a>Etapa 1: Examine o arquivo JSON de Olá Olá para parâmetros de modelo
Aqui estão Olá conteúdo do hello JSON arquivo de modelo de saudação. (modelo de saudação também está localizado em [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json).)

Modelos são flexíveis, para que designer Olá tenha escolhido toogive muita parâmetros ou escolhido toooffer apenas alguns ao criar um modelo que mais é fixo. Em informações de pedidos toocollect Olá é necessário o modelo de saudação toopass como parâmetros, abrir o arquivo de modelo de saudação (Este tópico tem um modelo embutido, abaixo) e examine Olá **parâmetros** valores.

Nesse caso, o modelo de saudação abaixo pedirá para:

* Um nome de conta de armazenamento exclusivo.
* Um nome de usuário de administrador para Olá VM.
* Uma senha.
* Um nome de domínio para Olá fora toouse do mundo.
* Um número de versão do Servidor do Ubuntu, mas apenas um de uma lista será aceito.

Veja mais sobre os [requisitos de nome de usuário e senha](../articles/virtual-machines/linux/faq.md#what-are-the-username-requirements-when-creating-a-vm).

Depois que você decidir sobre esses valores, você está pronto toocreate um grupo e implanta este modelo em sua assinatura do Azure.

```json
{
"$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
    "newStorageAccountName": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello storage account where hello virtual machine's disks will be placed."
    }
    },
    "adminUsername": {
    "type": "string",
    "metadata": {
        "description": "User name for hello virtual machine."
    }
    },
    "adminPassword": {
    "type": "securestring",
    "metadata": {
        "description": "Password for hello virtual machine."
    }
    },
    "dnsNameForPublicIP": {
    "type": "string",
    "metadata": {
        "description": "Unique DNS name for hello public IP used tooaccess hello virtual machine."
    }
    },
    "ubuntuOSVersion": {
    "type": "string",
    "defaultValue": "14.04.2-LTS",
    "allowedValues": [
        "12.04.5-LTS",
        "14.04.2-LTS",
        "15.04"
    ],
    "metadata": {
        "description": "hello Ubuntu version for hello VM. This will pick a fully patched image of this given Ubuntu version. Allowed values: 12.04.5-LTS, 14.04.2-LTS, 15.04."
    }
    }
},
"variables": {
    "location": "West US",
    "imagePublisher": "Canonical",
    "imageOffer": "UbuntuServer",
    "OSDiskName": "osdiskforlinuxsimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyUbuntuVM",
    "vmSize": "Standard_D1",
    "virtualNetworkName": "MyVNET",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
},
"resources": [
    {
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[parameters('newStorageAccountName')]",
    "apiVersion": "2015-05-01-preview",
    "location": "[variables('location')]",
    "properties": {
        "accountType": "[variables('storageAccountType')]"
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/publicIPAddresses",
    "name": "[variables('publicIPAddressName')]",
    "location": "[variables('location')]",
    "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
        "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
        }
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[variables('virtualNetworkName')]",
    "location": "[variables('location')]",
    "properties": {
        "addressSpace": {
        "addressPrefixes": [
            "[variables('addressPrefix')]"
        ]
        },
        "subnets": [
        {
            "name": "[variables('subnetName')]",
            "properties": {
            "addressPrefix": "[variables('subnetPrefix')]"
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('nicName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
    ],
    "properties": {
        "ipConfigurations": [
        {
            "name": "ipconfig1",
            "properties": {
            "privateIPAllocationMethod": "Dynamic",
            "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
            },
            "subnet": {
                "id": "[variables('subnetRef')]"
            }
            }
        }
        ]
    }
    },
    {
    "apiVersion": "2015-05-01-preview",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[variables('vmName')]",
    "location": "[variables('location')]",
    "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', parameters('newStorageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
    ],
    "properties": {
        "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
        "computername": "[variables('vmName')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
        "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('ubuntuOSVersion')]",
            "version": "latest"
        },
        "osDisk": {
            "name": "osdisk",
            "vhd": {
            "uri": "[concat('http://',parameters('newStorageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
        }
        },
        "networkProfile": {
        "networkInterfaces": [
            {
            "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
        ]
        }
    }
    }
]
}
```

### <a name="step-2-create-hello-virtual-machine-by-using-hello-template"></a>Etapa 2: Criar a máquina virtual de saudação usando o modelo de saudação
Uma vez que os valores de parâmetro prontos, você deve criar um grupo de recursos para sua implantação de modelo e, em seguida, implante o modelo de saudação.

grupo de recursos toocreate hello, tipo `azure group create <group name> <location>` com o nome de saudação do grupo de saudação desejado e localização do datacenter Olá no qual você deseja toodeploy. Isso acontece rapidamente:

```azurecli
azure group create myResourceGroup westus
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

Implantação de saudação toocreate agora, chamada `azure group deployment create` e passar:

* arquivo de modelo de saudação (se você salvou Olá acima arquivo local do JSON modelo tooa).
* Um modelo de URI (se você deseja toopoint no arquivo hello no GitHub ou algum outro endereço da web).
* grupo de recursos Olá no qual você deseja toodeploy.
* E um nome de implantação opcional.

Será solicitada toosupply Olá valores de parâmetros na seção "parâmetros" hello arquivo JSON de saudação. Quando você tiver especificado a todos os valores de parâmetro hello, sua implantação começará.

Aqui está um exemplo:

```azurecli
azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-simple-linux/azuredeploy.json myResourceGroup firstDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
newStorageAccountName: storageaccount
adminUsername: ops
adminPassword: password
dnsNameForPublicIP: newdomainname
```

Olá, tipo de informações a seguir será exibida:

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "firstDeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
data:    DeploymentName     : firstDeployment
data:    ResourceGroupName  : myResourceGroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T07:53:55.1828878Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  -------------
data:    newStorageAccountName  String        storageaccount
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameForPublicIP     String        newdomainname
data:    ubuntuOSVersion        String        14.10
info:    group deployment create command OK
```


## <a id="create-a-custom-vm-image"></a>Tarefa: Criar uma imagem de VM personalizada
Você viu o uso básico de saudação de modelos acima, portanto, agora podemos usar toocreate semelhante de instruções uma VM personalizada de um arquivo. vhd específico no Azure usando um modelo por meio de Olá CLI do Azure. diferença de saudação aqui é que este modelo cria uma única máquina virtual de um disco rígido virtual (VHD) especificado.

### <a name="step-1-examine-hello-json-file-for-hello-template"></a>Etapa 1: Examine Olá JSON no arquivo de modelo de saudação
Aqui estão Olá conteúdo do hello JSON arquivo de modelo de saudação que esta seção usa como exemplo. (modelo de saudação também está localizado em [GitHub](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json).)

Novamente, você precisará de valores de saudação toofind você deseja tooenter para parâmetros de saudação que não têm valores padrão. Quando você executa Olá `azure group deployment create` comando, Olá CLI do Azure solicitará que você tooenter esses valores.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters" : {
        "userImageStorageAccountName": {
            "type": "string",
            "defaultValue" : "userImageStorageAccountName"
        },
        "userImageStorageContainerName" : {
            "type" : "string",
            "defaultValue" : "userImageStorageContainerName"
        },
        "userImageVhdName" : {
            "type" : "string",
            "defaultValue" : "userImageVhdName"
        },
        "dnsNameForPublicIP" : {
            "type" : "string",
            "defaultValue": "uniqueDnsNameForPublicIP"
        },
        "adminUserName": {
            "type": "string"
        },
        "adminPassword": {
            "type": "securestring"
        },
        "osType" : {
            "type" : "string",
            "allowedValues" : [
                "windows",
                "linux"
            ]
        },
        "subscriptionId":{
            "type" : "string"
        },
        "location": {
            "type": "String",
            "defaultValue" : "West US"
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A2"
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue" : "myPublicIP"
        },
        "vmName": {
            "type": "string",
            "defaultValue" : "myVM"
        },
        "virtualNetworkName":{
            "type" : "string",
            "defaultValue" : "myVNET"
        },
        "nicName":{
            "type" : "string",
            "defaultValue":"myNIC"
        }
    },
    "variables": {
        "addressPrefix":"10.0.0.0/16",
        "subnet1Name": "Subnet-1",
        "subnet2Name": "Subnet-2",
        "subnet1Prefix" : "10.0.0.0/24",
        "subnet2Prefix" : "10.0.1.0/24",
        "publicIPAddressType" : "Dynamic",
        "vnetID":"[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",
        "subnet1Ref" : "[concat(variables('vnetID'),'/subnets/',variables('subnet1Name'))]",
        "userImageName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('userImageVhdName'))]",
        "osDiskVhdName" : "[concat('http://',parameters('userImageStorageAccountName'),'.blob.core.windows.net/',parameters('userImageStorageContainerName'),'/',parameters('vmName'),'osDisk.vhd')]"
    },
    "resources": [
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[parameters('publicIPAddressName')]",
        "location": "[parameters('location')]",
        "properties": {
            "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsNameForPublicIP')]"
            }
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/virtualNetworks",
        "name": "[parameters('virtualNetworkName')]",
        "location": "[parameters('location')]",
        "properties": {
        "addressSpace": {
            "addressPrefixes": [
            "[variables('addressPrefix')]"
            ]
        },
        "subnets": [
            {
            "name": "[variables('subnet1Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet1Prefix')]"
            }
            },
            {
            "name": "[variables('subnet2Name')]",
            "properties" : {
                "addressPrefix": "[variables('subnet2Prefix')]"
            }
            }
        ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Network/networkInterfaces",
        "name": "[parameters('nicName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]",
            "[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]"
        ],
        "properties": {
            "ipConfigurations": [
            {
                "name": "ipconfig1",
                "properties": {
                    "privateIPAllocationMethod": "Dynamic",
                    "publicIPAddress": {
                        "id": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]"
                    },
                    "subnet": {
                        "id": "[variables('subnet1Ref')]"
                    }
                }
            }
            ]
        }
    },
    {
        "apiVersion": "2014-12-01-preview",
        "type": "Microsoft.Compute/virtualMachines",
        "name": "[parameters('vmName')]",
        "location": "[parameters('location')]",
        "dependsOn": [
            "[concat('Microsoft.Network/networkInterfaces/', parameters('nicName'))]"
        ],
        "properties": {
            "hardwareProfile": {
                "vmSize": "[parameters('vmSize')]"
            },
            "osProfile": {
                "computername": "[parameters('vmName')]",
                "adminUsername": "[parameters('adminUsername')]",
                "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
                "osDisk" : {
                    "name" : "[concat(parameters('vmName'),'-osDisk')]",
                    "osType" : "[parameters('osType')]",
                    "caching" : "ReadWrite",
                    "image" : {
                        "uri" : "[variables('userImageName')]"
                    },
                    "vhd" : {
                        "uri" : "[variables('osDiskVhdName')]"
                    }
                }
            },
            "networkProfile": {
                "networkInterfaces" : [
                {
                    "id": "[resourceId('Microsoft.Network/networkInterfaces',parameters('nicName'))]"
                }
                ]
            }
        }
    }
    ]
}
```

### <a name="step-2-obtain-hello-vhd"></a>Etapa 2: Obter Olá VHD
Obviamente, você precisará de um .vhd para isso. Você pode usar um que já tenha no Azure ou pode carregar um.

Para uma máquina virtual com base em Windows, consulte [criar e carregar um VHD do Windows Server tooAzure](../articles/virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Para uma máquina virtual com base em Linux, consulte [criando e carregando um disco rígido virtual que contém o sistema de operacional Linux Olá](../articles/virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

### <a name="step-3-create-hello-virtual-machine-by-using-hello-template"></a>Etapa 3: Criar a máquina virtual de saudação usando o modelo de saudação
Agora você está pronto toocreate uma nova máquina virtual com base em. vhd de saudação. Criar um toodeploy de grupo, usando `azure group create <location>`:

```azurecli
azure group create myResourceGroupUser eastus
info:    Executing command group create
+ Getting resource group myResourceGroupUser
+ Creating resource group myResourceGroupUser
info:    Created resource group myResourceGroupUser
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupUser
data:    Name:                myResourceGroupUser
data:    Location:            eastus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

Criar implantação hello usando Olá `--template-uri` toocall opção no modelo de saudação diretamente (ou você pode usar o hello `--template-file` opção toouse um arquivo que você salvou localmente). Observe que, como modelo Olá tem padrões especificados, você será solicitado para apenas algumas coisas. Se você implantar o modelo de saudação em locais diferentes, você pode achar que alguns colisões de nomenclatura ocorrerem com valores padrão de saudação (particularmente Olá nome DNS criar).

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json \
> myResourceGroup \
> customVhdDeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
adminUserName: ops
adminPassword: password
osType: linux
subscriptionId: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

Saída parecida com hello a seguir:

```azurecli
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "customVhdDeployment"
+ Registering providers
info:    Registering provider microsoft.network
info:    Registering provider microsoft.compute
+ Waiting for deployment toocomplete
error:   Deployment provisioning state was not successful
data:    DeploymentName     : customVhdDeployment
data:    ResourceGroupName  : myResourceGroupUser
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T14:55:48.0963829Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-from-user-image/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                           Type          Value
data:    -----------------------------  ------------  ------------------------------------
data:    userImageStorageAccountName    String        userImageStorageAccountName
data:    userImageStorageContainerName  String        userImageStorageContainerName
data:    userImageVhdName               String        userImageVhdName
data:    dnsNameForPublicIP             String        uniqueDnsNameForPublicIP
data:    adminUserName                  String        ops
data:    adminPassword                  SecureString  undefined
data:    osType                         String        linux
data:    subscriptionId                 String        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
data:    location                       String        West US
data:    vmSize                         String        Standard_A2
data:    publicIPAddressName            String        myPublicIP
data:    vmName                         String        myVM
data:    virtualNetworkName             String        myVNET
data:    nicName                        String        myNIC
info:    group deployment create command OK
```

## <a id="deploy-a-multi-vm-application-that-uses-a-virtual-network-and-an-external-load-balancer"></a>Tarefa: implantar um aplicativo com várias VMs que usa uma rede virtual e um balanceador externo de carga
Este modelo permite que você toocreate duas máquinas virtuais em um balanceador de carga e configurar uma regra de balanceamento de carga na porta 80. Esse modelo também implanta uma Conta de Armazenamento, Rede Virtual, Endereço IP Público, Conjunto de Disponibilidade e Interfaces de Rede.

![](./media/virtual-machines-common-cli-deploy-templates/multivmextlb.png)

Siga essas etapas toodeploy um aplicativo de várias VMs que usa uma rede virtual e um balanceador de carga usando um modelo de Gerenciador de recursos no repositório de modelos do GitHub Olá através de comandos do PowerShell do Azure.

### <a name="step-1-examine-hello-json-file-for-hello-template"></a>Etapa 1: Examine Olá JSON no arquivo de modelo de saudação
Aqui estão Olá conteúdo do hello JSON arquivo de modelo de saudação. Se desejar que a versão mais recente do hello, ele localizou [no repositório do GitHub Olá para modelos de](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json). Este tópico usa Olá `--template-uri` toocall de comutador no modelo hello, mas você também pode usar o hello `--template-file` alternar toopass uma versão local.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "location": {
            "type": "string",
            "metadata": {
                "description": "Location of resources"
            }
        },
        "storageAccountName": {
            "type": "string",
            "metadata": {
                "description": "Name of storage account"
            }
        },
        "adminUsername": {
            "type": "string",
            "metadata": {
                "description": "Admin user name"
            }
        },
        "adminPassword": {
            "type": "securestring",
            "metadata": {
                "description": "Admin password"
            }
        },
        "dnsNameforLBIP": {
            "type": "string",
            "metadata": {
                "description": "DNS for load balancer IP"
            }
        },
        "backendPort": {
            "type": "int",
            "defaultValue": 3389,
            "metadata": {
                "description": "Back-end port"
            }
        },
        "vmNamePrefix": {
            "type": "string",
            "defaultValue": "myVM",
            "metadata": {
                "description": "Prefix toouse for VM names"
            }
        },
        "vmSourceImageName": {
            "type": "string",
            "defaultValue": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201412.01-en.us-127GB.vhd"
        },
        "lbName": {
            "type": "string",
            "defaultValue": "myLB",
            "metadata": {
                "description": "Load balancer name"
            }
        },
        "nicNamePrefix": {
            "type": "string",
            "defaultValue": "nic",
            "metadata": {
                "description": "Network interface name prefix"
            }
        },
        "publicIPAddressName": {
            "type": "string",
            "defaultValue": "myPublicIP",
            "metadata": {
                "description": "Public IP name"
            }
        },
        "vnetName": {
            "type": "string",
            "defaultValue": "myVNET",
            "metadata": {
                "description": "Virtual network name"
            }
        },
        "vmSize": {
            "type": "string",
            "defaultValue": "Standard_A1",
            "metadata": {
                "description": "Size of hello VM"
            }
        }
    },
    "variables": {
        "storageAccountType": "Standard_LRS",
        "vmStorageAccountContainerName": "vhds",
        "availabilitySetName": "myAvSet",
        "addressPrefix": "10.0.0.0/16",
        "subnetName": "Subnet-1",
        "subnetPrefix": "10.0.0.0/24",
        "publicIPAddressType": "Dynamic",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('vnetName'))]",
        "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables ('subnetName'))]",
        "publicIPAddressID": "[resourceId('Microsoft.Network/publicIPAddresses',parameters('publicIPAddressName'))]",
        "lbID": "[resourceId('Microsoft.Network/loadBalancers',parameters('lbName'))]",
        "numberOfInstances": 2,
        "nicId1": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 0))]",
        "nicId2": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'), 1))]",
        "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/LBFE')]",
        "backEndIPConfigID1": "[concat(variables('nicId1'),'/ipConfigurations/ipconfig1')]",
        "backEndIPConfigID2": "[concat(variables('nicId2'),'/ipConfigurations/ipconfig1')]",
        "sourceImageName": "[concat('/', subscription().subscriptionId,'/services/images/',parameters('vmSourceImageName'))]",
        "lbPoolID": "[concat(variables('lbID'),'/backendAddressPools/LBBE')]",
        "lbProbeID": "[concat(variables('lbID'),'/probes/tcpProbe')]"
    },
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('storageAccountName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": {
                "accountType": "[variables('storageAccountType')]"
            }
        },
        {
            "type": "Microsoft.Compute/availabilitySets",
            "name": "[variables('availabilitySetName')]",
            "apiVersion": "2015-05-01-preview",
            "location": "[parameters('location')]",
            "properties": { }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/publicIPAddresses",
            "name": "[parameters('publicIPAddressName')]",
            "location": "[parameters('location')]",
            "properties": {
                "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
                "dnsSettings": {
                    "domainNameLabel": "[parameters('dnsNameforLBIP')]"
                }
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/virtualNetworks",
            "name": "[parameters('vnetName')]",
            "location": "[parameters('location')]",
            "properties": {
                "addressSpace": {
                    "addressPrefixes": [
                        "[variables('addressPrefix')]"
                    ]
                },
                "subnets": [
                    {
                        "name": "[variables('subnetName')]",
                        "properties": {
                            "addressPrefix": "[variables('subnetPrefix')]"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Network/networkInterfaces",
            "name": "[concat(parameters('nicNamePrefix'), copyindex())]",
            "location": "[parameters('location')]",
            "copy": {
                "name": "nicLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "dependsOn": [
                "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
            ],
            "properties": {
                "ipConfigurations": [
                    {
                        "name": "ipconfig1",
                        "properties": {
                            "privateIPAllocationMethod": "Dynamic",
                            "subnet": {
                                "id": "[variables('subnetRef')]"
                            }
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/backendAddressPools/LBBE')]"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "[concat('Microsoft.Network/loadBalancers/',parameters('lbName'),'/inboundNatRule/RDP-VM', copyindex())]"
                            }
                        ]


                    }
                ]

            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "name": "[parameters('lbName')]",
            "type": "Microsoft.Network/loadBalancers",
            "location": "[parameters('location')]",
            "dependsOn": [
                "nicLoop",
                "[concat('Microsoft.Network/publicIPAddresses/', parameters('publicIPAddressName'))]"
            ],
            "properties": {
                "frontendIPConfigurations": [
                    {
                        "name": "LBFE",
                        "properties": {
                            "publicIPAddress": {
                                "id": "[variables('publicIPAddressID')]"
                            }
                        }
                    }
                ],
                "backendAddressPools": [
                    {
                        "name": "LBBE"

                    }
                ],
                "inboundNatRules": [
                    {
                        "name": "RDP-VM1",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50001,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    },
                    {
                        "name": "RDP-VM2",
                        "properties": {
                            "frontendIPConfiguration":
                                {
                                    "id": "[variables('frontEndIPConfigID')]"
                                },
                            "protocol": "tcp",
                            "frontendPort": 50002,
                            "backendPort": 3389,
                            "enableFloatingIP": false
                        }
                    }
                ],
                "loadBalancingRules": [
                    {
                        "name": "LBRule",
                        "properties": {
                            "frontendIPConfiguration": {
                                "id": "[variables('frontEndIPConfigID')]"
                            },
                            "backendAddressPool": {
                                "id": "[variables('lbPoolID')]"
                            },
                            "protocol": "tcp",
                            "frontendPort": 80,
                            "backendPort": 80,
                            "enableFloatingIP": false,
                            "idleTimeoutInMinutes": 5,
                            "probe": {
                                "id": "[variables('lbProbeID')]"
                            }
                        }
                    }
                ],
                "probes": [
                    {
                        "name": "tcpProbe",
                        "properties": {
                            "protocol": "tcp",
                            "port": 80,
                            "intervalInSeconds": "5",
                            "numberOfProbes": "2"
                        }
                    }
                ]
            }
        },
        {
            "apiVersion": "2015-05-01-preview",
            "type": "Microsoft.Compute/virtualMachines",
            "name": "[concat(parameters('vmNamePrefix'), copyindex())]",
            "copy": {
                "name": "virtualMachineLoop",
                "count": "[variables('numberOfInstances')]"
            },
            "location": "[parameters('location')]",
            "dependsOn": [
                "[concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName'))]",
                "[concat('Microsoft.Network/networkInterfaces/', parameters('nicNamePrefix'), copyindex())]",
                "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]"
            ],
            "properties": {
                "availabilitySet": {
                    "id": "[resourceId('Microsoft.Compute/availabilitySets',variables('availabilitySetName'))]"
                },
                "hardwareProfile": {
                    "vmSize": "[parameters('vmSize')]"
                },
                "osProfile": {
                    "computername": "[concat(parameters('vmNamePrefix'), copyIndex())]",
                    "adminUsername": "[parameters('adminUsername')]",
                    "adminPassword": "[parameters('adminPassword')]"
                },
                "storageProfile": {
                    "sourceImage": {
                        "id": "[variables('sourceImageName')]"
                    },
                    "destinationVhdsContainer": "[concat('http://',parameters('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/')]"
                },
                "networkProfile": {
                    "networkInterfaces": [
                        {
                            "id": "[resourceId('Microsoft.Network/networkInterfaces',concat(parameters('nicNamePrefix'),copyindex()))]"
                        }
                    ]
                }
            }
        }
    ]
}
```

### <a name="step-2-create-hello-deployment-by-using-hello-template"></a>Etapa 2: Criar a implantação de saudação usando o modelo de saudação
Criar um grupo de recursos para o modelo de saudação usando `azure group create <location>`. Em seguida, crie uma implantação para esse grupo de recursos usando `azure group deployment create` e passando o grupo de recursos hello, passando um nome de implantação e responder a prompts Olá para parâmetros de modelo de saudação que não possuem valores padrão.

```azurecli
azure group create lbgroup westus
info:    Executing command group create
+ Getting resource group lbgroup
+ Creating resource group lbgroup
info:    Created resource group lbgroup
data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/lbgroup
data:    Name:                lbgroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags:
data:
info:    group create command OK
```

Agora use Olá `azure group deployment create` comando e hello `--template-uri` modelo de saudação toodeploy opção. Esteja pronto para fornecer os valores de parâmetros quando eles forem solicitados, conforme mostrado a seguir.

```azurecli
azure group deployment create \
> --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json \
> lbgroup \
> newdeployment
info:    Executing command group deployment create
info:    Supply values for hello following parameters
location: westus
newStorageAccountName: storagename
adminUsername: ops
adminPassword: password
dnsNameforLBIP: lbdomainname
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "newdeployment"
+ Registering providers
info:    Registering provider microsoft.storage
info:    Registering provider microsoft.compute
info:    Registering provider microsoft.network
+ Waiting for deployment toocomplete
data:    DeploymentName     : newdeployment
data:    ResourceGroupName  : lbgroup
data:    ProvisioningState  : Succeeded
data:    Timestamp          : 2015-04-28T20:58:40.1678876Z
data:    Mode               : Incremental
data:    TemplateLink       : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-2-vms-loadbalancer-lbrules/azuredeploy.json
data:    ContentVersion     : 1.0.0.0
data:    Name                   Type          Value
data:    ---------------------  ------------  ----------------------
data:    location               String        westus
data:    newStorageAccountName  String        storagename
data:    adminUsername          String        ops
data:    adminPassword          SecureString  undefined
data:    dnsNameforLBIP         String        lbdomainname
data:    backendPort            Int           3389
data:    vmNamePrefix           String        myVM
data:    imagePublisher         String        MicrosoftWindowsServer
data:    imageOffer             String        WindowsServer
data:    imageSKU               String        2012-R2-Datacenter
data:    lbName                 String        myLB
data:    nicNamePrefix          String        nic
data:    publicIPAddressName    String        myPublicIP
data:    vnetName               String        myVNET
data:    vmSize                 String        Standard_A1
info:    group deployment create command OK
```

Observe que esse modelo implanta uma imagem do Windows Server. No entanto, ela poderia ser facilmente substituída por qualquer imagem do Linux. Deseja toocreate um cluster do Docker com vários gerenciadores de por nuvem? [Você consegue](https://azure.microsoft.com/documentation/templates/docker-swarm-cluster/).

## <a id="remove-a-resource-group"></a>Tarefa: Remover um grupo de recursos
Lembre-se de que você pode reutilizar o grupo de recursos de tooa, mas se você tiver terminado com um, você poderá excluí-la usando `azure group delete <group name>`.

```azurecli
azure group delete myResourceGroup
info:    Executing command group delete
Delete resource group myResourceGroup? [y/n] y
+ Deleting resource group myResourceGroup
info:    group delete command OK
```

## <a id="show-the-log-for-a-resource-group-deployment"></a>Tarefa: Mostrar log Olá para uma implantação de grupo de recursos
Essa é uma tarefa comum ao se criar ou usar modelos. implantação de Olá Olá chamada toodisplay logs para um grupo é `azure group log show <groupname>`, que exibe uma grande quantidade de informações que são úteis para entender por que algo aconteceu – ou não. (Para obter mais informações sobre como solucionar problemas em suas implantações, bem como outras informações sobre problemas, confira [Solução de problemas comuns de implantação do Azure com o Azure Resource Manager](../articles/azure-resource-manager/resource-manager-common-deployment-errors.md)).

falhas de tootarget específico, por exemplo, você pode usar ferramentas como **jq** tooquery coisas um pouco mais precisamente, como quais falhas individuais, você precisa toocorrect. Olá exemplo a seguir usa **jq** tooparse de log para uma implantação **lbgroup**, procura a falhas.

```azurecli
azure group log show lbgroup -l --json | jq '.[] | select(.status.value == "Failed") | .properties'
```
Você pode descobrir rapidamente qual foi o problema, corrigi-lo e tentar novamente. Olá caso a seguir, modelo Olá tinha foi criando duas VMs em Olá mesmo tempo, que é criado um bloqueio em. vhd de saudação. (Depois que modificamos modelo hello, Olá implantação bem-sucedida rapidamente.)

```json
{
    "statusCode": "Conflict",
    "statusMessage": "{\"status\":\"Failed\",\"error\":{\"code\":\"ResourceDeploymentFailure\",\"message\":\"hello resource operation completed with terminal provisioning state 'Failed'.\",\"details\":[{\"code\":\"AcquireDiskLeaseFailed\",\"message\":\"Failed tooacquire lease while creating disk 'osdisk' using blob with URI http://storage.blob.core.windows.net/vhds/osdisk.vhd.\"}]}}"
}
```

## <a id="display-information-about-a-virtual-machine"></a>Tarefa: Exibir informações sobre uma máquina virtual
Você pode ver informações sobre máquinas virtuais específicas no seu grupo de recursos usando Olá `azure vm show <groupname> <vmname>` comando. Se você tiver mais de uma máquina virtual em seu grupo, talvez seja necessário primeiro Olá toolist VMs em um grupo usando `azure vm list <groupname>`.

```azurecli
azure vm list zoo
info:    Executing command vm list
+ Getting virtual machines
data:    Name   ProvisioningState  Location  Size
data:    -----  -----------------  --------  -----------
data:    myVM0  Succeeded          westus    Standard_A1
data:    myVM1  Failed             westus    Standard_A1
```

E, em seguida, procurar por myVM1:

```azurecli
azure vm show zoo myVM1
info:    Executing command vm show
+ Looking up hello VM "myVM1"
+ Looking up hello NIC "nic1"
data:    Id                              :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Failed
data:    Name                            :myVM1
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_A1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :MicrosoftWindowsServer
data:        Offer                       :WindowsServer
data:        Sku                         :2012-R2-Datacenter
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Windows
data:        Name                        :osdisk
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :http://zoostorageralph.blob.core.windows.net/vhds/osdisk.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Windows Configuration:
data:        Provision VM Agent          :true
data:        Enable automatic updates    :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Id                        :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Network/networkInterfaces/nic1
data:          Primary                   :false
data:          Provisioning State        :Succeeded
data:          Name                      :nic1
data:          Location                  :westus
data:            Private IP alloc-method :Dynamic
data:            Private IP address      :10.0.0.5
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/zoo/providers/Microsoft.Compute/availabilitySets/MYAVSET
info:    vm show command OK
```

> [!NOTE]
> Se você quiser tooprogrammatically repositório e manipular a saída de hello dos seus comandos de console, convém toouse uma análise JSON ferramenta como  **[jq](https://github.com/stedolan/jq)**  ou  **[jsawk](https://github.com/micha/jsawk)** , ou bibliotecas de idioma que são bons para tarefas de saudação.
>
>

## <a id="log-on-to-a-linux-based-virtual-machine"></a>Tarefa: Faça logon na máquina virtual baseados em Linux de tooa
Normalmente máquinas Linux são conectado toothrough SSH. Para obter mais informações, consulte [como toouse SSH com Linux no Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a id="stop-a-virtual-machine"></a>Tarefa: Parar uma VM
Execute este comando:

```azurecli
azure vm stop <group name> <virtual machine name>
```

> [!IMPORTANT]
> Use este parâmetro tookeep Olá IP virtual (VIP) de rede virtual de saudação caso ela seja Olá última VM nessa rede virtual. <br><br> Se você usar o hello `StayProvisioned` parâmetro, você ainda será cobrado por Olá VM.
>
>

## <a id="start-a-virtual-machine"></a>Tarefa: iniciar uma VM
Execute este comando:

```azurecli
azure vm start <group name> <virtual machine name>
```

## <a id="attach-a-data-disk"></a>Tarefa: Anexar um disco de dados
Você também precisará toodecide se tooattach um novo disco ou uma que contém dados. Para um novo disco, o comando de saudação cria o arquivo. vhd de saudação e anexa-o no hello mesmo comando.

tooattach um novo disco, execute este comando:

```azurecli
    azure vm disk attach-new <resource-group> <vm-name> <size-in-gb>
```

tooattach um disco de dados existente, execute este comando:

```azurecli
azure vm disk attach <resource-group> <vm-name> [vhd-url]
```

Em seguida, você precisará toomount disco de Olá, como faria normalmente no Linux.

## <a name="next-steps"></a>Próximas etapas
Para obter mais exemplos de uso da CLI do Azure com hello **arm** modo, consulte [hello usando a CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](../articles/xplat-cli-azure-resource-manager.md). toolearn mais sobre os recursos do Azure e seus conceitos, consulte [visão geral do Gerenciador de recursos do Azure](../articles/azure-resource-manager/resource-group-overview.md).

Para obter mais modelos que você pode usar, confira [Modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/) e [Estruturas de aplicativos usando modelos](../articles/virtual-machines/linux/app-frameworks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
