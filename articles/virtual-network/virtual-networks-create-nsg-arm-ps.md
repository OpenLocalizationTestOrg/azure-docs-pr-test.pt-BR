---
title: "Criar grupos de segurança de rede – Azure PowerShell | Microsoft Docs"
description: "Aprenda a criar e implantar grupos de segurança de rede usando o PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9cef62b8-d889-4d16-b4d0-58639539a418
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 26fe67b43d63c6685d8ae7644dd7df6931a4d2a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-powershell"></a><span data-ttu-id="9fb01-103">Criar grupos de segurança usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fb01-103">Create network security groups using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

<span data-ttu-id="9fb01-104">O Azure tem dois modelos de implantação: Azure Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="9fb01-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="9fb01-105">A Microsoft recomenda criar recursos por meio do modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="9fb01-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="9fb01-106">Para saber mais sobre as diferenças entre os dois modelos, leia o artigo [Entender os modelos de implantação do Azure](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9fb01-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="9fb01-107">Este artigo aborda o modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="9fb01-107">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="9fb01-108">Você também pode [criar NSGs no modelo de implantação clássica](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9fb01-108">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="9fb01-109">O exemplo de comando PowerShell abaixo espera um ambiente simples já criado com base no cenário acima.</span><span class="sxs-lookup"><span data-stu-id="9fb01-109">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="9fb01-110">Se você quiser executar os comandos conforme eles são exibidos neste documento, primeiro crie o ambiente de teste ao implantar [esse modelo](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), clique em **Implantar no Azure**, substitua os valores de parâmetro padrão, se necessário, e siga as instruções no portal.</span><span class="sxs-lookup"><span data-stu-id="9fb01-110">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="9fb01-111">Como criar o NSG para a sub-rede front-end</span><span class="sxs-lookup"><span data-stu-id="9fb01-111">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="9fb01-112">Para criar um NSG chamado *NSG-FrontEnd* com base no cenário acima, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9fb01-112">To create an NSG named *NSG-FrontEnd* based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="9fb01-113">Se você nunca usou o Azure PowerShell, consulte [Como Instalar e Configurar o Azure PowerShell](/powershell/azure/overview) e siga as instruções até o fim para entrar no Azure e selecionar sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="9fb01-113">If you have never used Azure PowerShell, see [How to Install and Configure Azure PowerShell](/powershell/azure/overview) and follow the instructions all the way to the end to sign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="9fb01-114">Crie uma regra de segurança permitindo acesso da Internet à porta 3389.</span><span class="sxs-lookup"><span data-stu-id="9fb01-114">Create a security rule allowing access from the Internet to port 3389.</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name rdp-rule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
    ```

3. <span data-ttu-id="9fb01-115">Crie uma regra de segurança permitindo acesso da Internet à porta 80.</span><span class="sxs-lookup"><span data-stu-id="9fb01-115">Create a security rule allowing access from the Internet to port 80.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule -Description "Allow HTTP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 101 `
    -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80
    ```

4. <span data-ttu-id="9fb01-116">Adicione as regras criadas acima a um novo NSG chamado **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="9fb01-116">Add the rules created above to a new NSG named **NSG-FrontEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG -Location westus `
    -Name "NSG-FrontEnd" -SecurityRules $rule1,$rule2
    ```

5. <span data-ttu-id="9fb01-117">Verifique as regras criadas no NSG digitando o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9fb01-117">Check the rules created in the NSG by typing the following:</span></span>

    ```powershell
    $nsg
    ```
   
    <span data-ttu-id="9fb01-118">Saída mostrando apenas as regras de segurança:</span><span class="sxs-lookup"><span data-stu-id="9fb01-118">Output showing just the security rules:</span></span>
   
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
                                   "Description": "Allow RDP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "3389",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 100,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 },
                                 {
                                   "Name": "web-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
                                   "Description": "Allow HTTP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "80",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 101,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
6. <span data-ttu-id="9fb01-119">Associe o NSG criado acima à sub-rede *FrontEnd* .</span><span class="sxs-lookup"><span data-stu-id="9fb01-119">Associate the NSG created above to the *FrontEnd* subnet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="9fb01-120">Saída mostrando apenas as configurações da sub-rede *FrontEnd* ; observe o valor da propriedade **NetworkSecurityGroup** :</span><span class="sxs-lookup"><span data-stu-id="9fb01-120">Output showing only the *FrontEnd* subnet settings, notice the value for the **NetworkSecurityGroup** property:</span></span>
   
                    Subnets           : [
                                          {
                                            "Name": "FrontEnd",
                                            "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                            "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                            "AddressPrefix": "192.168.1.0/24",
                                            "IpConfigurations": [
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                              },
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                              }
                                            ],
                                            "NetworkSecurityGroup": {
                                              "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                            },
                                            "RouteTable": null,
                                            "ProvisioningState": "Succeeded"
                                          }
   
   > [!WARNING]
   > <span data-ttu-id="9fb01-121">A saída do comando acima mostra o conteúdo do objeto de configuração da rede virtual, que existe apenas no computador no qual você está executando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9fb01-121">The output for the command above shows the content for the virtual network configuration object, which only exists on the computer where you are running PowerShell.</span></span> <span data-ttu-id="9fb01-122">Você precisa executar o cmdlet `Set-AzureRmVirtualNetwork` para salvar essas configurações no Azure.</span><span class="sxs-lookup"><span data-stu-id="9fb01-122">You need to run the `Set-AzureRmVirtualNetwork` cmdlet to save these settings to Azure.</span></span>
   > 
   > 
7. <span data-ttu-id="9fb01-123">Salve as novas configurações da VNet no Azure.</span><span class="sxs-lookup"><span data-stu-id="9fb01-123">Save the new VNet settings to Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="9fb01-124">Saída mostrando apenas a parte do NSG:</span><span class="sxs-lookup"><span data-stu-id="9fb01-124">Output showing just the NSG portion:</span></span>
   
        "NetworkSecurityGroup": {
          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
        }

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="9fb01-125">Como criar o NSG para a sub-rede back-end</span><span class="sxs-lookup"><span data-stu-id="9fb01-125">How to create the NSG for the back-end subnet</span></span>
<span data-ttu-id="9fb01-126">Para criar um NSG chamado *NSG-BackEnd* com base no cenário acima, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9fb01-126">To create an NSG named *NSG-BackEnd* based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="9fb01-127">Crie uma regra de segurança, permitindo o acesso na sub-rede front-end à porta 1433 (porta padrão usada pelo SQL Server).</span><span class="sxs-lookup"><span data-stu-id="9fb01-127">Create a security rule allowing access from the front-end subnet to port 1433 (default port used by SQL Server).</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name frontend-rule `
    -Description "Allow FE subnet" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix 192.168.1.0/24 -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 1433
    ```

2. <span data-ttu-id="9fb01-128">Crie uma regra de segurança impedindo o acesso à Internet.</span><span class="sxs-lookup"><span data-stu-id="9fb01-128">Create a security rule blocking access to the Internet.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule `
    -Description "Block Internet" `
    -Access Deny -Protocol * -Direction Outbound -Priority 200 `
    -SourceAddressPrefix * -SourcePortRange * `
    -DestinationAddressPrefix Internet -DestinationPortRange *
    ```

3. <span data-ttu-id="9fb01-129">Adicione as regras criadas acima ao novo NSG chamado **NSG-BackEnd**.</span><span class="sxs-lookup"><span data-stu-id="9fb01-129">Add the rules created above to a new NSG named **NSG-BackEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG `
    -Location westus -Name "NSG-BackEnd" `
    -SecurityRules $rule1,$rule2
    ```

4. <span data-ttu-id="9fb01-130">Associe o NSG criado acima à sub-rede *BackEnd* .</span><span class="sxs-lookup"><span data-stu-id="9fb01-130">Associate the NSG created above to the *BackEnd* subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd ` 
    -AddressPrefix 192.168.2.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="9fb01-131">Saída mostrando apenas as configurações da sub-rede *BackEnd* ; observe o valor da propriedade **NetworkSecurityGroup** :</span><span class="sxs-lookup"><span data-stu-id="9fb01-131">Output showing only the *BackEnd* subnet settings, notice the value for the **NetworkSecurityGroup** property:</span></span>
   
        Subnets           : [
                      {
                        "Name": "BackEnd",
                        "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                        "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                        "AddressPrefix": "192.168.2.0/24",
                        "IpConfigurations": [...],
                        "NetworkSecurityGroup": {
                          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "RouteTable": null,
                        "ProvisioningState": "Succeeded"
                      }
5. <span data-ttu-id="9fb01-132">Salve as novas configurações da VNet no Azure.</span><span class="sxs-lookup"><span data-stu-id="9fb01-132">Save the new VNet settings to Azure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

## <a name="how-to-remove-an-nsg"></a><span data-ttu-id="9fb01-133">Como remover um NSG</span><span class="sxs-lookup"><span data-stu-id="9fb01-133">How to remove an NSG</span></span>
<span data-ttu-id="9fb01-134">Para excluir um NSG existente, chamado *NSG-Frontend* neste caso, siga a etapa abaixo:</span><span class="sxs-lookup"><span data-stu-id="9fb01-134">To delete an existing NSG, called *NSG-Frontend* in this case, follow the step below:</span></span>

<span data-ttu-id="9fb01-135">Execute o comando **Remove-AzureRmNetworkSecurityGroup** mostrado abaixo e inclua o grupo de recursos em que o NSG está.</span><span class="sxs-lookup"><span data-stu-id="9fb01-135">Run the **Remove-AzureRmNetworkSecurityGroup** shown below and be sure to include the resource group the NSG is in.</span></span>

```powershell
Remove-AzureRmNetworkSecurityGroup -Name "NSG-FrontEnd" -ResourceGroupName "TestRG"
```

