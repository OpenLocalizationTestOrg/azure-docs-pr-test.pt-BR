---
title: "aaaCreate uma VM com várias NICs - modelo do Gerenciador de recursos do Azure | Microsoft Docs"
description: Criar uma VM com diversas NICs usando um modelo do Azure Resource Manager.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a>Criar uma VM com diversas NICs usando um modelo
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).  Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez da saudação [modelo de implantação clássico](virtual-network-deploy-multinic-classic-ps.md).
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Olá, etapas a seguir usam um grupo de recursos denominado *IaaSStory* para servidores WEB hello e um grupo de recursos denominado *back-end IaaSStory* para servidores de saudação banco de dados.

## <a name="prerequisites"></a>Pré-requisitos
Antes de criar hello servidores de banco de dados, você precisa Olá toocreate *IaaSStory* grupo de recursos com todos os recursos necessários de saudação para esse cenário. concluir a esses recursos, toocreate Olá seguintes etapas:

1. Navegue muito[página de modelo Olá](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. Na página de modelo hello, toohello à direita do **o grupo de recursos pai**, clique em **implantar tooAzure**.
3. Se necessário, altere os valores de parâmetro hello, siga as etapas de Olá no grupo de recursos de saudação do hello visualização do Azure toodeploy portal.

> [!IMPORTANT]
> Verifique se os nomes da conta de armazenamento são exclusivos. Você não pode ter nomes de conta de armazenamento duplicados no Azure.
> 

## <a name="understand-hello-deployment-template"></a>Entender o modelo de implantação de saudação
Antes de implantar o modelo de saudação fornecido com esta documentação, certifique-se de que entender o que ele faz. Olá, as etapas a seguir fornece uma boa visão geral do modelo de saudação:

1. Navegue muito[página de modelo Olá](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. Clique em **azuredeploy.json** tooopen arquivo de modelo de saudação.
3. Saudação de aviso *osType* parâmetro listado abaixo. Esse parâmetro é usado tooselect configurações relacionadas a quais toouse da imagem VM para o servidor de banco de dados hello, juntamente com vários sistemas operacionais.

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. Role para baixo na lista de toohello de variáveis e verifique a definição Olá Olá **dbVMSetting** variáveis, listados abaixo. Ele recebe um dos elementos da matriz Olá contidos em Olá **dbVMSettings** variável. Se você estiver familiarizado com a terminologia de desenvolvimento de software, você pode exibir hello **dbVMSettings** variável como um dicionário ou uma tabela de hash.

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. Suponha que você decidir toodeploy VMs do Windows que executa o SQL Olá back-end. Olá, em seguida, o valor para **osType** seria *Windows*e hello **dbVMSetting** variável contém o elemento Olá listado abaixo, que representa o primeiro valor Olá Olá **dbVMSettings** variável.

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. Saudação de aviso **vmSize** contém valor Olá *Standard_DS3*. Apenas determinados tamanhos VM permitem uso de saudação de várias NICs. Você pode verificar quais tamanhos de VM oferecem suporte a várias NICs lendo Olá [tamanhos de VM do Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) e [tamanhos de VM do Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artigos.

7. Role para baixo demais**recursos** e observe Olá primeiro elemento. Ele descreve uma conta de armazenamento. Esta conta de armazenamento será usado toomaintain discos de dados de Olá usados por cada VM do banco de dados. Nesse cenário, cada VM do banco de dados tem um disco do sistema operacional em armazenamento regular e dois discos de dados em armazenamento SSD (premium).

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. Role para baixo de toohello próximo recurso, como listado abaixo. Esse recurso representa Olá que NIC usada para acesso de banco de dados em cada VM do banco de dados. Aviso uso Olá Olá **cópia** função nesse recurso. Olá modelo permite que você toodeploy como muitas máquinas virtuais que você desejar, com base em hello **dbCount** parâmetro. Portanto, você precisa toocreate Olá a mesma quantidade de NICs para acesso de banco de dados, uma para cada VM.

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. Role para baixo de toohello próximo recurso, como listado abaixo. Esse recurso representa Olá que NIC usada para o gerenciamento em cada VM do banco de dados. Mais uma vez, você precisará de uma dessas NICs para cada VM do banco de dados. Saudação de aviso **networkSecurityGroup** elemento, vinculando um NSG que permite acesso tooRDP/SSH toothis NIC somente.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. Role para baixo de toohello próximo recurso, como listado abaixo. Esse recurso representará um toobe de conjunto de disponibilidade compartilhado por todas as VMs de banco de dados. Dessa forma, você garante que sempre haja uma VM em Olá definido em execução durante a manutenção.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. Role para baixo toohello próximo recurso. Esse recurso representa o banco de dados de saudação VMs, como visto no hello primeiro algumas linhas listadas abaixo. Aviso uso Olá Olá **cópia** funcionar novamente, garantir que várias VMs são criadas com base em Olá **dbCount** parâmetro. Também observe Olá **dependsOn** coleção. Ela lista duas NICs, sendo necessário toobe criado antes de saudação que VM é implantada, juntamente com o conjunto de disponibilidade hello e conta de armazenamento hello.

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. Role para baixo na Olá VM recurso toohello **networkProfile** elemento, como listado abaixo. Observe que há duas NICs como referência para cada VM. Quando você criar várias NICs de uma VM, você deve definir Olá **primário** propriedade de uma saudação NICs muito*true*, e Olá rest muito*false*.

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a>Implantar o modelo do ARM hello usando clique toodeploy

> [!IMPORTANT]
> Certifique-se de seguir Olá [pré-requisitos](#Pre-requisites) etapas antes de seguir as instruções de saudação abaixo.
> 

Olá modelo de exemplo disponível no repositório público Olá usa um arquivo de parâmetro que contém cenário saudação padrão valores usados toogenerate Olá descrito acima. toodeploy usando esse modelo clique toodeploy, execute [este link](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello à direita do **(consulte a documentação) de grupo de recursos de back-end** clique **implantar tooAzure**, substitua Olá valores de parâmetro padrão se necessário e siga as instruções de saudação no portal de saudação.

Olá figura a seguir mostra o conteúdo de saudação do novo grupo de recursos Olá, após a implantação.

![Grupo de recursos Back-end](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a>Implante o modelo de saudação usando o PowerShell
modelo de saudação toodeploy baixados usando o PowerShell, instalar e configurar o PowerShell executando etapas Olá Olá [instalar e configurar o PowerShell](/powershell/azure/overview) artigo e, em seguida, concluir Olá etapas a seguir:

Executar Olá  **`New-AzureRmResourceGroup`**  toocreate cmdlet um grupo de recursos usando Olá modelo.

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

Saída esperada:

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Implantar o modelo hello usando Olá CLI do Azure
modelo de saudação toodeploy usando Olá CLI do Azure, siga as etapas de saudação abaixo.

1. Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.
2. Executar Olá  **`azure config mode`**  modo do Gerenciador de tooResource do comando tooswitch, conforme mostrado abaixo.

    ```azurecli
    azure config mode arm
    ```

    Olá esperado saída segue:

        info:    New mode is arm

3. Olá abrir [arquivo de parâmetro](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), selecione o seu conteúdo e salve-o arquivo tooa no seu computador. Neste exemplo, nós salvamos o arquivo de parâmetros Olá muito*parameters.json*.
4. Executar Olá  **`azure group deployment create`**  cmdlet toodeploy Olá nova rede virtual usando o modelo de saudação e parâmetro arquivos que você baixou e modificado acima. lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    Saída esperada:
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

