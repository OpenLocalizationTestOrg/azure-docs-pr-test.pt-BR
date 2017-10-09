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
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a>Criar uma rede virtual usando um modelo do Azure Resource Manager

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

O Azure tem dois modelos de implantação: Azure Resource Manager e clássico. A Microsoft recomenda a criação de recursos por meio do modelo de implantação do Gerenciador de recursos de saudação. mais sobre toolearn Olá diferenças entre modelos de saudação dois ler Olá [modelos de implantação do Azure entender](../azure-resource-manager/resource-manager-deployment-model.md) artigo.
 
Este artigo explica como toocreate uma rede virtual por meio da implantação do Gerenciador de recursos de saudação do modelo usando um modelo do Gerenciador de recursos do Azure. Você também pode criar uma rede virtual por meio de Gerenciador de recursos usando outras ferramentas ou criar uma rede virtual por meio do modelo de implantação clássico Olá selecionando uma opção diferente de saudação lista a seguir:

> [!div class="op_single_selector"]
- [Portal](virtual-networks-create-vnet-arm-pportal.md)
- [PowerShell](virtual-networks-create-vnet-arm-ps.md)
- [CLI](virtual-networks-create-vnet-arm-cli.md)
- [Modelo](virtual-networks-create-vnet-arm-template-click.md)
- [Portal (clássico)](virtual-networks-create-vnet-classic-pportal.md)
- [PowerShell (Clássico)](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [CLI (Clássica)](virtual-networks-create-vnet-classic-cli.md)

Você aprenderá como toodownload e modificar existentes de modelo do ARM do GitHub e implante o modelo de saudação do GitHub, PowerShell e Olá CLI do Azure.

Se você estiver implantando o modelo do ARM Olá diretamente do GitHub, sem qualquer alteração, simplesmente ignorar muito[implantar um modelo do github](#deploy-the-arm-template-by-using-click-to-deploy).

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>Baixe e entender o modelo do Azure Resource Manager Olá
Você pode baixar Olá o modelo existente para criar uma rede virtual e duas sub-redes do GitHub, faça as alterações que você pode desejar e reutilizá-la. toodo então, conclua Olá etapas a seguir:

1. Navegue muito[página de modelo de exemplo hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
2. Clique em **azuredeploy.json** e em **RAW**.
3. Salve Olá arquivo tooa uma pasta local no computador.
4. Se você estiver familiarizado com modelos, ignore toostep 7.
5. Abrir arquivo hello salvo e examine o conteúdo de saudação em **parâmetros** na linha 5. Os parâmetros do modelo ARM fornecem um espaço reservado para valores que podem ser preenchidos durante a implantação.
   
   | Parâmetro | Descrição |
   | --- | --- |
   | **local** |Região do Azure onde Olá rede virtual será criado |
   | **vnetName** |Nome para Olá nova rede virtual |
   | **addressPrefix** |Espaço de endereço para Olá VNet, no formato CIDR |
   | **subnet1Name** |Nome para Olá primeiro VNet |
   | **subnet1Prefix** |Bloco CIDR para sub-rede primeiro Olá |
   | **subnet2Name** |Nome para Olá segunda rede virtual |
   | **subnet2Prefix** |Bloco CIDR para sub-rede segundo Olá |
   
   > [!IMPORTANT]
   > Os modelos do Gerenciador de Recursos do Azure mantidos no GitHub podem mudar ao longo do tempo. Verifique o modelo de saudação antes de usá-lo.
   > 
   > 
6. Verifique o conteúdo Olá **recursos** e observe o seguinte hello:
   
   * **type**. Tipo de recurso que está sendo criado pelo modelo de saudação. Nesse caso, **Microsoft.Network/virtualNetworks**, que representa uma rede virtual.
   * **name**. Nome de recurso de saudação. Uso de saudação de aviso de **[parameters('vnetName')]**, que significa Olá será nome fornecido como entrada pelo usuário hello ou um arquivo de parâmetro durante a implantação.
   * **properties**. Lista de propriedades para o recurso de saudação. Este modelo usa as propriedades de espaço e sub-redes de endereço Olá durante a criação de rede virtual.
7. Navegue de volta muito[página de modelo de exemplo hello](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
8. Clique em **azuredeploy-paremeters.json** e em **RAW**.
9. Salve Olá arquivo tooa uma pasta local no computador.
10. Abrir arquivo hello salvo e editar Olá valores para parâmetros de saudação. Use Olá valores abaixo Olá toodeploy VNet descrito no cenário de saudação a seguir:

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

11. Salve o arquivo hello.


## <a name="deploy-hello-template-using-powershell"></a>Implante o modelo hello usando o PowerShell

Concluir Olá modelo de saudação toodeploy etapas baixados usando o PowerShell a seguir:

1. Instalar e configurar o Azure PowerShell completando as etapas de saudação do hello [como tooInstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.
2. Execute um novo grupo de recursos de Olá toocreate de comando a seguir:

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    comando Olá cria um grupo de recursos denominado *TestRG* em Olá *centro dos EUA* região do azure. Para saber mais sobre grupos de recursos, visite [Visão geral do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-overview.md).

    Saída esperada:

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. Execute Olá toodeploy Olá nova rede virtual usando Olá arquivos de modelo e o parâmetro baixado e modificado acima de comando a seguir:

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    Saída esperada:
   
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
4. Comando a seguir de execução Olá tooview propriedades Olá Olá nova rede virtual:

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    Saída esperada:

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

## <a name="deploy-hello-template-using-click-to-deploy"></a>Implante o modelo hello usando clique para implantar

Você pode reutilizar predefinidos do Azure Resource Manager modelos carregados tooa repositório do GitHub mantido pela Microsoft e da comunidade toohello aberto. Esses modelos podem ser implantados diretamente fora do GitHub, ou baixado e modificadas toofit suas necessidades. toodeploy um modelo que cria uma rede virtual com duas sub-redes, Olá concluir as etapas a seguir:

1. Em um navegador, navegue muito[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
2. Role para baixo na lista de saudação de modelos e clique em **101-vnet duas sub-redes**. Verificar Olá **README.md** de arquivos, conforme mostrado abaixo.

    ![Arquivo READEME.md no github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. Clique em **implantar tooAzure**. Se necessário, insira suas credenciais de logon do Azure. 
4. Em Olá **parâmetros** folha, insira valores hello você deseja toouse toocreate sua nova rede virtual e, em seguida, clique em **Okey**. Olá figura a seguir mostra valores Olá para o cenário de saudação:
   
    ![Parâmetros de modelo ARM](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. Clique em **grupo de recursos** e selecione Olá VNet para um tooadd do grupo de recursos, ou clique em **criar novo** tooadd Olá VNet tooa novo grupo de recursos. Olá figura a seguir mostra os recursos de saudação configurações de grupo para um novo grupo de recursos chamado **TestRG**:

    ![Grupo de recursos](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. Se necessário, altere Olá **assinatura** e **local** configurações para sua rede virtual.
7. Se não desejar Olá toosee VNet como um bloco em Olá **quadro inicial**, desabilitar **tooStartboard Pin**.
8. Clique em **termos legais**, leia os termos de saudação e clique em **comprar** tooagree. 
9. Clique em **criar** toocreate Olá VNet.
   
    ![Enviando bloco de implantação no portal de visualização](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. Após a conclusão da implantação hello, no hello Azure portal clique em **mais serviços**, tipo *redes virtuais* na caixa de filtro de saudação que aparece, clique em folha de redes virtuais redes toosee Olá Virtual. Na folha de saudação, clique em *TestVNet*. Em Olá *TestVNet* folha, clique em **sub-redes** sub-redes de saudação criada toosee, conforme mostrado na figura abaixo de saudação:
    
     ![Criar rede virtual no portal de visualização](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a>Próximas etapas

Saiba como tooconnect:

- Uma máquina virtual (VM) tooa rede virtual lendo Olá [criar uma VM do Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) ou [criar uma VM do Linux](../virtual-machines/linux/quick-create-portal.md) artigos. Em vez de criar uma rede virtual e a sub-rede nas etapas de saudação de artigos hello, você pode selecionar uma rede virtual existente e a sub-rede tooconnect uma VM.
- Olá redes virtuais de tooother de rede virtual lendo Olá [VNets conectar](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artigo.
- Olá rede virtual tooan na rede local usando uma rede privada virtual (VPN) site a site ou um circuito de rota expressa. Saiba como lendo Olá [conectar uma rede de local de tooan de rede virtual usando uma VPN site a site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) e [vincular um circuito de rota expressa do tooan de VNet](../expressroute/expressroute-howto-linkvnet-arm.md) artigos.
