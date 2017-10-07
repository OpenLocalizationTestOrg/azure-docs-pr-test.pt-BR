---
title: "aaaCreate uma VM com um endereço IP público estático - modelo do Gerenciador de recursos do Azure | Microsoft Docs"
description: "Saiba como toocreate uma VM com um endereço IP público estático endereço usando um modelo do Gerenciador de recursos do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a>Criar uma VM com um endereço IP público estático usando um modelo do Azure Resource Manager

> [!div class="op_single_selector"]
> * [Portal do Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [CLI do Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Modelo](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (Clássico)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez do modelo de implantação clássico hello.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a>Recursos de endereço IP público em um arquivo de modelo
Você pode exibir e baixar Olá [modelo](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).

Olá, seção a seguir mostra a definição de saudação do recurso IP público de hello, com base no cenário de saudação acima:

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

Saudação de aviso **publicIPAllocationMethod** propriedade, que está definida muito*estático*. Essa propriedade pode ser *Dinâmica* (valor padrão) ou *Estática*. Definindo-toostatic garante que o endereço IP público Olá atribuído nunca será alterado.

Olá, seção a seguir mostra a associação de saudação do endereço IP público de saudação com uma interface de rede:

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

Saudação de aviso **publicIPAddress** propriedade apontando toohello **Id** de um recurso chamado **variables('webVMSetting').pipName**. Esse é o nome de saudação do recurso IP público Olá mostrado acima.

Por fim, acima da interface de rede de saudação está listada no hello **networkProfile** propriedade Olá VM que está sendo criado.

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Implantar o modelo de saudação usando clique toodeploy

Olá modelo de exemplo disponível no repositório público Olá usa um arquivo de parâmetro que contém cenário saudação padrão valores usados toogenerate Olá descrito acima. toodeploy usando esse modelo clique toodeploy, clique em **implantar tooAzure** no arquivo Readme.md Olá Olá [VM com PIP estático](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) modelo. Substituir valores de parâmetro padrão hello, se desejado e insira valores para parâmetros de saudação em branco.  Siga as instruções de Olá Olá portal toocreate uma máquina virtual com um endereço IP público estático.

## <a name="deploy-hello-template-by-using-powershell"></a>Implante o modelo de saudação usando o PowerShell

modelo de saudação toodeploy baixados usando o PowerShell, execute as etapas de saudação abaixo.

1. Se você nunca usou o Azure PowerShell, Olá concluir etapas no hello [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.
2. Em um console do PowerShell, execute Olá `New-AzureRmResourceGroup` cmdlet toocreate um novo grupo de recursos, se necessário. Se você já tiver criado um grupo de recursos, vá toostep 3.

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    Saída esperada:
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. Em um console do PowerShell, execute Olá `New-AzureRmResourceGroupDeployment` modelo do cmdlet toodeploy hello.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    Saída esperada:
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Implantar o modelo hello usando Olá CLI do Azure
modelo de saudação toodeploy usando Olá CLI do Azure, Olá concluir as etapas a seguir:

1. Se você nunca tiver usado a CLI do Azure, siga as etapas de Olá Olá [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) artigo tooinstall e configurá-lo.
2. Executar Olá `azure config mode` modo do Gerenciador de tooResource do comando tooswitch, conforme mostrado abaixo.

    ```azurecli
    azure config mode arm
    ```

    Olá esperado saída Olá comando acima:

        info:    New mode is arm

3. Olá abrir [arquivo de parâmetro](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), selecione o seu conteúdo e salve-o arquivo tooa no seu computador. Neste exemplo, os parâmetros de saudação são salvos arquivo tooa chamado *parameters.json*. Alterar valores de parâmetro de saudação do arquivo hello, se desejado, mas, no mínimo, é recomendável que você altere o valor Olá Olá adminPassword parâmetro tooa complexo senha exclusiva.
4. Executar Olá `azure group deployment create` cmd toodeploy Olá nova rede virtual usando o modelo de saudação e parâmetro arquivos que você baixou e modificado acima. O comando Olá abaixo, substitua <path> com caminho de saudação você salvou o arquivo hello. 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    Saída esperada (lista os valores de parâmetro usados):

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

