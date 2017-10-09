---
title: aaaCreate uma rede virtual | Modelo do Gerenciador de recursos do Azure | Microsoft Docs
description: Saiba como toocreate um virtual de rede usando um modelo do Gerenciador de recursos do Azure.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b9c289433ff2a84bec19eac25fa28ab40d131c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="6357a-103">Criar uma rede virtual usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6357a-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="6357a-104">O Azure tem dois modelos de implantação: Azure Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="6357a-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="6357a-105">A Microsoft recomenda a criação de recursos por meio do modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="6357a-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="6357a-106">mais sobre toolearn Olá diferenças entre modelos de saudação dois ler Olá [modelos de implantação do Azure entender](../azure-resource-manager/resource-manager-deployment-model.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="6357a-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="6357a-107">Este artigo explica como toocreate uma rede virtual por meio da implantação do Gerenciador de recursos de saudação do modelo usando um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6357a-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="6357a-108">Você também pode criar uma rede virtual por meio de Gerenciador de recursos usando outras ferramentas ou criar uma rede virtual por meio do modelo de implantação clássico Olá selecionando uma opção diferente de saudação lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="6357a-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="6357a-109">Portal</span><span class="sxs-lookup"><span data-stu-id="6357a-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="6357a-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6357a-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="6357a-111">CLI</span><span class="sxs-lookup"><span data-stu-id="6357a-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="6357a-112">Modelo</span><span class="sxs-lookup"><span data-stu-id="6357a-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="6357a-113">Portal (clássico)</span><span class="sxs-lookup"><span data-stu-id="6357a-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="6357a-114">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="6357a-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="6357a-115">CLI (Clássica)</span><span class="sxs-lookup"><span data-stu-id="6357a-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="6357a-116">Você aprenderá como toodownload e modificar existentes de modelo do ARM do GitHub e implante o modelo de saudação do GitHub, PowerShell e Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="6357a-116">You will learn how toodownload and modify and existing ARM template from GitHub, and deploy hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="6357a-117">Se você estiver implantando o modelo do ARM Olá diretamente do GitHub, sem qualquer alteração, simplesmente ignorar muito[implantar um modelo do github](#deploy-the-arm-template-by-using-click-to-deploy).</span><span class="sxs-lookup"><span data-stu-id="6357a-117">If you are simply deploying hello ARM template directly from GitHub, without any changes, skip too[deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="6357a-118">Baixe e entender o modelo do Azure Resource Manager Olá</span><span class="sxs-lookup"><span data-stu-id="6357a-118">Download and understand hello Azure Resource Manager template</span></span>
<span data-ttu-id="6357a-119">Você pode baixar Olá o modelo existente para criar uma rede virtual e duas sub-redes do GitHub, faça as alterações que você pode desejar e reutilizá-la.</span><span class="sxs-lookup"><span data-stu-id="6357a-119">You can download hello existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="6357a-120">toodo então, conclua Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6357a-120">toodo so, complete hello following steps:</span></span>

1. <span data-ttu-id="6357a-121">Navegue muito[página de modelo de exemplo hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="6357a-121">Navigate too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="6357a-122">Clique em **azuredeploy.json** e em **RAW**.</span><span class="sxs-lookup"><span data-stu-id="6357a-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="6357a-123">Salve Olá arquivo tooa uma pasta local no computador.</span><span class="sxs-lookup"><span data-stu-id="6357a-123">Save hello file tooa a local folder on your computer.</span></span>
4. <span data-ttu-id="6357a-124">Se você estiver familiarizado com modelos, ignore toostep 7.</span><span class="sxs-lookup"><span data-stu-id="6357a-124">If you are familiar with templates, skip toostep 7.</span></span>
5. <span data-ttu-id="6357a-125">Abrir arquivo hello salvo e examine o conteúdo de saudação em **parâmetros** na linha 5.</span><span class="sxs-lookup"><span data-stu-id="6357a-125">Open hello file you just saved and look at hello contents under **parameters** in line 5.</span></span> <span data-ttu-id="6357a-126">Os parâmetros do modelo ARM fornecem um espaço reservado para valores que podem ser preenchidos durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="6357a-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="6357a-127">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="6357a-127">Parameter</span></span> | <span data-ttu-id="6357a-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="6357a-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="6357a-129">**local**</span><span class="sxs-lookup"><span data-stu-id="6357a-129">**location**</span></span> |<span data-ttu-id="6357a-130">Região do Azure onde Olá rede virtual será criado</span><span class="sxs-lookup"><span data-stu-id="6357a-130">Azure region where hello VNet will be created</span></span> |
   | <span data-ttu-id="6357a-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="6357a-131">**vnetName**</span></span> |<span data-ttu-id="6357a-132">Nome para Olá nova rede virtual</span><span class="sxs-lookup"><span data-stu-id="6357a-132">Name for hello new VNet</span></span> |
   | <span data-ttu-id="6357a-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="6357a-133">**addressPrefix**</span></span> |<span data-ttu-id="6357a-134">Espaço de endereço para Olá VNet, no formato CIDR</span><span class="sxs-lookup"><span data-stu-id="6357a-134">Address space for hello VNet, in CIDR format</span></span> |
   | <span data-ttu-id="6357a-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="6357a-135">**subnet1Name**</span></span> |<span data-ttu-id="6357a-136">Nome para Olá primeiro VNet</span><span class="sxs-lookup"><span data-stu-id="6357a-136">Name for hello first VNet</span></span> |
   | <span data-ttu-id="6357a-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="6357a-137">**subnet1Prefix**</span></span> |<span data-ttu-id="6357a-138">Bloco CIDR para sub-rede primeiro Olá</span><span class="sxs-lookup"><span data-stu-id="6357a-138">CIDR block for hello first subnet</span></span> |
   | <span data-ttu-id="6357a-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="6357a-139">**subnet2Name**</span></span> |<span data-ttu-id="6357a-140">Nome para Olá segunda rede virtual</span><span class="sxs-lookup"><span data-stu-id="6357a-140">Name for hello second VNet</span></span> |
   | <span data-ttu-id="6357a-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="6357a-141">**subnet2Prefix**</span></span> |<span data-ttu-id="6357a-142">Bloco CIDR para sub-rede segundo Olá</span><span class="sxs-lookup"><span data-stu-id="6357a-142">CIDR block for hello second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="6357a-143">Os modelos do Gerenciador de Recursos do Azure mantidos no GitHub podem mudar ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="6357a-143">Azure Resource Manager templates maintained in GitHub can change over time.</span></span> <span data-ttu-id="6357a-144">Verifique o modelo de saudação antes de usá-lo.</span><span class="sxs-lookup"><span data-stu-id="6357a-144">Make sure you check hello template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="6357a-145">Verifique o conteúdo Olá **recursos** e observe o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="6357a-145">Check hello content under **resources** and notice hello following:</span></span>
   
   * <span data-ttu-id="6357a-146">**type**.</span><span class="sxs-lookup"><span data-stu-id="6357a-146">**type**.</span></span> <span data-ttu-id="6357a-147">Tipo de recurso que está sendo criado pelo modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6357a-147">Type of resource being created by hello template.</span></span> <span data-ttu-id="6357a-148">Nesse caso, **Microsoft.Network/virtualNetworks**, que representa uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="6357a-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="6357a-149">**name**.</span><span class="sxs-lookup"><span data-stu-id="6357a-149">**name**.</span></span> <span data-ttu-id="6357a-150">Nome de recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="6357a-150">Name for hello resource.</span></span> <span data-ttu-id="6357a-151">Uso de saudação de aviso de **[parameters('vnetName')]**, que significa Olá será nome fornecido como entrada pelo usuário hello ou um arquivo de parâmetro durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="6357a-151">Notice hello use of **[parameters('vnetName')]**, which means hello name will provided as input by hello user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="6357a-152">**properties**.</span><span class="sxs-lookup"><span data-stu-id="6357a-152">**properties**.</span></span> <span data-ttu-id="6357a-153">Lista de propriedades para o recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="6357a-153">List of properties for hello resource.</span></span> <span data-ttu-id="6357a-154">Este modelo usa as propriedades de espaço e sub-redes de endereço Olá durante a criação de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="6357a-154">This template uses hello address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="6357a-155">Navegue de volta muito[página de modelo de exemplo hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="6357a-155">Navigate back too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="6357a-156">Clique em **azuredeploy-paremeters.json** e em **RAW**.</span><span class="sxs-lookup"><span data-stu-id="6357a-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="6357a-157">Salve Olá arquivo tooa uma pasta local no computador.</span><span class="sxs-lookup"><span data-stu-id="6357a-157">Save hello file tooa a local folder on your computer.</span></span>
10. <span data-ttu-id="6357a-158">Abrir arquivo hello salvo e editar Olá valores para parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="6357a-158">Open hello file you just saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="6357a-159">Use Olá valores abaixo Olá toodeploy VNet descrito no cenário de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="6357a-159">Use hello following values below toodeploy hello VNet described in hello scenario:</span></span>

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. <span data-ttu-id="6357a-160">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="6357a-160">Save hello file.</span></span>


## <a name="deploy-hello-template-using-powershell"></a><span data-ttu-id="6357a-161">Implante o modelo hello usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="6357a-161">Deploy hello template using PowerShell</span></span>

<span data-ttu-id="6357a-162">Concluir Olá modelo de saudação toodeploy etapas baixados usando o PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="6357a-162">Complete hello following steps toodeploy hello template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="6357a-163">Instalar e configurar o Azure PowerShell completando as etapas de saudação do hello [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.</span><span class="sxs-lookup"><span data-stu-id="6357a-163">Install and configure Azure PowerShell by completing hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="6357a-164">Execute um novo grupo de recursos de Olá toocreate de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="6357a-164">Run hello following command toocreate a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="6357a-165">comando Olá cria um grupo de recursos denominado *TestRG* em Olá *centro dos EUA* região do azure.</span><span class="sxs-lookup"><span data-stu-id="6357a-165">hello command creates a resource group named *TestRG* in hello *Central US* azure region.</span></span> <span data-ttu-id="6357a-166">Para saber mais sobre grupos de recursos, visite [Visão geral do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6357a-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="6357a-167">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="6357a-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="6357a-168">Execute Olá toodeploy Olá nova rede virtual usando Olá arquivos de modelo e o parâmetro baixado e modificado acima de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="6357a-168">Run hello following command toodeploy hello new VNet using hello template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="6357a-169">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="6357a-169">Expected output:</span></span>
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. <span data-ttu-id="6357a-170">Comando a seguir de execução Olá tooview propriedades Olá Olá nova rede virtual:</span><span class="sxs-lookup"><span data-stu-id="6357a-170">Run hello following command tooview hello properties of hello new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="6357a-171">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="6357a-171">Expected output:</span></span>

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-hello-template-using-click-to-deploy"></a><span data-ttu-id="6357a-172">Implante o modelo hello usando clique para implantar</span><span class="sxs-lookup"><span data-stu-id="6357a-172">Deploy hello template using click-to-deploy</span></span>

<span data-ttu-id="6357a-173">Você pode reutilizar predefinidos do Azure Resource Manager modelos carregados tooa repositório do GitHub mantido pela Microsoft e da comunidade toohello aberto.</span><span class="sxs-lookup"><span data-stu-id="6357a-173">You can reuse pre-defined Azure Resource Manager templates uploaded tooa GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="6357a-174">Esses modelos podem ser implantados diretamente fora do GitHub, ou baixado e modificadas toofit suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="6357a-174">These templates can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> <span data-ttu-id="6357a-175">toodeploy um modelo que cria uma rede virtual com duas sub-redes, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="6357a-175">toodeploy a template that creates a VNet with two subnets, complete hello following steps:</span></span>

1. <span data-ttu-id="6357a-176">Em um navegador, navegue muito[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="6357a-176">From a browser, navigate too[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="6357a-177">Role para baixo na lista de saudação de modelos e clique em **101-vnet duas sub-redes**.</span><span class="sxs-lookup"><span data-stu-id="6357a-177">Scroll down hello list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="6357a-178">Verificar Olá **README.md** de arquivos, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="6357a-178">Check hello **README.md** file, as shown below.</span></span>

    ![Arquivo READEME.md no github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="6357a-180">Clique em **implantar tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="6357a-180">Click **Deploy tooAzure**.</span></span> <span data-ttu-id="6357a-181">Se necessário, insira suas credenciais de logon do Azure.</span><span class="sxs-lookup"><span data-stu-id="6357a-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="6357a-182">Em Olá **parâmetros** folha, insira valores hello você deseja toouse toocreate sua nova rede virtual e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="6357a-182">In hello **Parameters** blade, enter hello values you want toouse toocreate your new VNet, and then click **OK**.</span></span> <span data-ttu-id="6357a-183">Olá figura a seguir mostra valores Olá para o cenário de saudação:</span><span class="sxs-lookup"><span data-stu-id="6357a-183">hello following figure shows hello values for hello scenario:</span></span>
   
    ![Parâmetros de modelo ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="6357a-185">Clique em **grupo de recursos** e selecione Olá VNet para um tooadd do grupo de recursos, ou clique em **criar novo** tooadd Olá VNet tooa novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6357a-185">Click **Resource group** and select a resource group tooadd hello VNet to, or click **Create new** tooadd hello VNet tooa new resource group.</span></span> <span data-ttu-id="6357a-186">Olá figura a seguir mostra os recursos de saudação configurações de grupo para um novo grupo de recursos chamado **TestRG**:</span><span class="sxs-lookup"><span data-stu-id="6357a-186">hello following figure shows hello resource group settings for a new resource group called **TestRG**:</span></span>

    ![Grupo de recursos](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="6357a-188">Se necessário, altere Olá **assinatura** e **local** configurações para sua rede virtual.</span><span class="sxs-lookup"><span data-stu-id="6357a-188">If necessary, change hello **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="6357a-189">Se não desejar Olá toosee VNet como um bloco em Olá **quadro inicial**, desabilitar **tooStartboard Pin**.</span><span class="sxs-lookup"><span data-stu-id="6357a-189">If you do not want toosee hello VNet as a tile in hello **Startboard**, disable **Pin tooStartboard**.</span></span>
8. <span data-ttu-id="6357a-190">Clique em **termos legais**, leia os termos de saudação e clique em **comprar** tooagree.</span><span class="sxs-lookup"><span data-stu-id="6357a-190">Click **Legal terms**, read hello terms, and click **Buy** tooagree.</span></span> 
9. <span data-ttu-id="6357a-191">Clique em **criar** toocreate Olá VNet.</span><span class="sxs-lookup"><span data-stu-id="6357a-191">Click **Create** toocreate hello VNet.</span></span>
   
    ![Enviando bloco de implantação no portal de visualização](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="6357a-193">Após a conclusão da implantação hello, no hello Azure portal clique em **mais serviços**, tipo *redes virtuais* na caixa de filtro de saudação que aparece, clique em folha de redes virtuais redes toosee Olá Virtual.</span><span class="sxs-lookup"><span data-stu-id="6357a-193">Once hello deployment is complete, in hello Azure portal click **More services**, type *virtual networks* in hello filter box that appears, then click Virtual networks toosee hello Virtual networks blade.</span></span> <span data-ttu-id="6357a-194">Na folha de saudação, clique em *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="6357a-194">In hello blade, click *TestVNet*.</span></span> <span data-ttu-id="6357a-195">Em Olá *TestVNet* folha, clique em **sub-redes** sub-redes de saudação criada toosee, conforme mostrado na figura abaixo de saudação:</span><span class="sxs-lookup"><span data-stu-id="6357a-195">In hello *TestVNet* blade, click **Subnets** toosee hello created subnets, as shown in hello following picture:</span></span>
    
     ![Criar rede virtual no portal de visualização](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="6357a-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6357a-197">Next steps</span></span>

<span data-ttu-id="6357a-198">Saiba como tooconnect:</span><span class="sxs-lookup"><span data-stu-id="6357a-198">Learn how tooconnect:</span></span>

- <span data-ttu-id="6357a-199">Uma máquina virtual (VM) tooa rede virtual lendo Olá [criar uma VM do Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) ou [criar uma VM do Linux](../virtual-machines/linux/quick-create-portal.md) artigos.</span><span class="sxs-lookup"><span data-stu-id="6357a-199">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="6357a-200">Em vez de criar uma rede virtual e a sub-rede nas etapas de saudação de artigos hello, você pode selecionar uma rede virtual existente e a sub-rede tooconnect uma VM.</span><span class="sxs-lookup"><span data-stu-id="6357a-200">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="6357a-201">Olá redes virtuais de tooother de rede virtual lendo Olá [VNets conectar](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="6357a-201">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="6357a-202">Olá rede virtual tooan na rede local usando uma rede privada virtual (VPN) site a site ou um circuito de rota expressa.</span><span class="sxs-lookup"><span data-stu-id="6357a-202">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="6357a-203">Saiba como lendo Olá [conectar uma rede de local de tooan de rede virtual usando uma VPN site a site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [vincular um circuito de rota expressa do tooan de VNet](../expressroute/expressroute-howto-linkvnet-arm.md) artigos.</span><span class="sxs-lookup"><span data-stu-id="6357a-203">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
