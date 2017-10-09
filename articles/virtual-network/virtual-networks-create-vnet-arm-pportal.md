---
title: "uma rede virtual do Azure com várias sub-redes do aaaCreate | Microsoft Docs"
description: "Saiba como toocreate uma rede virtual com várias sub-redes no Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ad679a4-a959-4e48-a317-d9f5655a442b
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 0f56fa6ac24537d33b8e217f5b03f387826ab487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-multiple-subnets"></a>Criar uma rede virtual com várias sub-redes

Neste tutorial, saiba como toocreate uma rede virtual do Azure básico que tenha separada subredes públicas e privadas. Você pode criar recursos do Azure, como máquinas virtuais, ambientes de Serviço de Aplicativo, conjuntos de dimensionamento de máquina virtual, Azure HDInsight e serviços de nuvem em uma sub-rede. Recursos em redes virtuais podem se comunicar entre si e com recursos em outra rede virtual de tooa conectado de redes.

Olá, seções a seguir incluem etapas que você pode colocar toocreate uma rede virtual usando Olá [portal do Azure](#portal), Olá interface de linha de comando do Azure ([CLI do Azure](#azure-cli)), [PowerShell do Azure ](#powershell)e um [modelo do Azure Resource Manager](#resource-manager-template). resultado de saudação é Olá mesmo, independentemente de qual ferramenta você usar rede virtual do toocreate hello. Clique em uma seção de toothat ferramenta link toogo tutorial hello. Saiba mais sobre todas as configurações de [rede virtual](virtual-network-manage-network.md) e [sub-rede](virtual-network-manage-subnet.md).

Este artigo fornece etapas toocreate uma rede virtual por meio do modelo de implantação do Gerenciador de recursos hello, que é o modelo de implantação de Olá, que é recomendável usar ao criar novas redes virtuais. Se você precisar toocreate uma rede virtual (clássica), consulte [criar uma rede virtual (clássica)](create-virtual-network-classic.md). Se você não estiver familiarizado com os modelos de implantação do Azure, confira [Entender os modelos de implantação do Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

## <a name="portal"></a>Portal do Azure

1. Em um navegador da Internet, vá toohello [portal do Azure](https://portal.azure.com). Faça logon usando sua [conta do Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se não tiver uma conta do Azure, você poderá assinar uma versão de [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
2. No portal de saudação, clique em **+ novo** > **rede** > **rede Virtual**.
3. Em Olá **criar rede virtual** folha, digite Olá valores a seguir e, em seguida, clique em **criar**:

    |Configuração|Valor|
    |---|---|
    |Nome|myVnet|
    |Espaço de endereço|10.0.0.0/16|
    |Nome da sub-rede|Público|
    |Intervalo de endereços da sub-rede|10.0.0.0/24|
    |Grupo de recursos|Deixe **Criar novo** selecionado e digite **myResourceGroup**.|
    |Assinatura e localização|Selecione sua assinatura e localização.

    Se você for novo tooAzure, saiba mais sobre [grupos de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [assinaturas](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), e [locais](https://azure.microsoft.com/regions) (também chamado tooas *regiões*).
4. No portal de saudação, você pode criar apenas uma sub-rede quando você criar uma rede virtual. Neste tutorial, você criará uma segunda sub-rede depois que você criar rede virtual hello. Você pode criar mais tarde recursos acessíveis pela Internet Olá **pública** sub-rede. Você também pode criar recursos que não estão acessíveis da saudação da Internet no hello **privada** sub-rede. toocreate Olá segunda sub-rede, Olá **pesquisar recursos** na parte superior de saudação da página hello, digite **myVnet**. Nos resultados da pesquisa de saudação, clique em **myVnet**. Se você tiver várias redes virtuais com hello o mesmo nome em sua assinatura, verifique os grupos de recursos de saudação são listados em cada rede virtual. Certifique-se de que você clicar em Olá **myVnet** pesquisa resultados que tem o grupo de recursos de saudação **myResourceGroup**.
5. Em Olá **myVnet** folha, em **configurações**, clique em **sub-redes**.
6. Em Olá **myVnet - sub-redes** folha, clique em **+ sub-rede**.
7. Em Olá **Adicionar sub-rede** folha, para **nome**, digite **particular**. Para **Intervalo de endereços**, digite **10.0.1.0/24**.  Clique em **OK**.
8. Em Olá **myVnet - sub-redes** folha, examine Olá sub-redes. Você pode ver Olá **pública** e **privada** sub-redes que você criou.
9. **Opcional:** toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em [excluir recursos](#delete-portal) neste artigo.

## <a name="azure-cli"></a>CLI do Azure

Comandos da CLI do Azure são Olá mesmo, se você executar os comandos de saudação do Windows, Linux ou macOS. No entanto, há diferenças de script entre shells de sistema operacional. executa script Olá Olá seguindo as etapas em um shell Bash. 

1. [Instalar e configurar Olá CLI do Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que você tem a versão mais recente de saudação do hello CLI do Azure instalado. tooget ajuda para comandos CLI, digite `az <command> --help`. Em vez de instalar Olá CLI e seus pré-requisitos, você pode usar o hello Shell de nuvem do Azure. Olá Shell de nuvem do Azure é um shell Bash livre que podem ser executados diretamente no hello portal do Azure. Olá Shell de nuvem tem Olá CLI do Azure pré-instalado e configurado toouse com sua conta. Olá toouse Shell de nuvem, clique em Olá nuvem Shell (**> _**) botão na parte superior de saudação do hello [portal](https://portal.azure.com) ou simplesmente clicar Olá *Experimente* botão nas etapas Olá seguir. 
2. Se executado localmente Olá CLI, faça logon tooAzure com hello `az login` comando. Se usar Olá Shell de nuvem, você já está conectado.
3. Saudação de revisão script e seus comentários a seguir. No navegador, copie o script hello e cole-o em sua sessão CLI:

    ```azurecli-interactive
    #!/bin/bash
    
    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus
    
    # Create a virtual network with one subnet named Public.
    az network vnet create \
      --name myVnet \
      --resource-group myResourceGroup \
      --subnet-name Public
    
    # Create an additional subnet named Private in hello virtual network.
    az network vnet subnet create \
      --name Private \
      --address-prefix 10.0.1.0/24 \
      --vnet-name myVnet \
      --resource-group myResourceGroup
    ```
    
4. Quando o script hello for concluída em execução, examine as sub-redes Olá para rede virtual hello. Copie Olá comando a seguir e, em seguida, cole-o em sua sessão CLI:

    ```azurecli
    az network vnet subnet list --resource-group myResourceGroup --vnet-name myVnet --output table
    ```

5. **Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em [excluir recursos](#delete-cli) neste artigo.

## <a name="powershell"></a>PowerShell

1. Instale a versão mais recente Olá de saudação do PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Se você for novo tooAzure PowerShell, consulte [visão geral do Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Em uma sessão do PowerShell, faça logon no tooAzure com seus [conta do Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) usando Olá `login-azurermaccount` comando.

3. Saudação de revisão script e seus comentários a seguir. No navegador, copie o script hello e colá-lo em sua sessão do PowerShell:

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name myResourceGroup `
      -Location eastus
    
    # Create hello public and private subnets.
    $Subnet1 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Public `
      -AddressPrefix 10.0.0.0/24
    $Subnet2 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Private `
      -AddressPrefix 10.0.1.0/24
    
    # Create a virtual network.
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Location eastus `
      -Name myVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet1,$Subnet2
    ```

4. sub-redes de saudação tooreview para rede virtual do hello, copie Olá comando a seguir e, em seguida, cole-o em sua sessão do PowerShell:

    ```powershell
    $Vnet.subnets | Format-Table Name, AddressPrefix
    ```

5. **Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em [excluir recursos](#delete-powershell) neste artigo.

## <a name="resource-manager-template"></a>Modelo do Resource Manager

Você pode implantar uma rede virtual usando um modelo do Azure Resource Manager. toolearn mais sobre modelos, consulte [o que é o Gerenciador de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment). modelo de saudação tooaccess e toolearn sobre seus parâmetros, consulte Olá [criar uma rede virtual com duas sub-redes](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) modelo. Você pode implantar o modelo de saudação usando Olá [portal](#template-portal), [CLI do Azure](#template-cli), ou [PowerShell](#template-powershell).

**Opcional:** toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em qualquer subseções [excluir recursos](#delete) neste artigo.

### <a name="template-portal"></a>Portal do Azure

1. No navegador, abra Olá [página modelo](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets).
2. Clique em Olá **implantar tooAzure** botão. Se você ainda não estiver logado tooAzure, entrar na tela de logon do portal do Azure Olá que aparece.
3. Entre no portal de toohello usando seu [conta do Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Se não tiver uma conta do Azure, você poderá assinar uma versão de [avaliação gratuita](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Digite hello valores hello parâmetros a seguir:

    |Parâmetro|Valor|
    |---|---|
    |Assinatura|Selecione sua assinatura|
    |Grupo de recursos|myResourceGroup|
    |Local|Selecione um local|
    |Nome da VNet|myVnet|
    |Prefixo de Endereço da VNet|10.0.0.0/16|
    |Subnet1Prefix|10.0.0.0/24|
    |Subnet1Name|Público|
    |Subnet2Prefix|10.0.1.0/24|
    |Subnet2Name|Privado|

5. Aceite toohello termos e condições e, em seguida, clique em **compra** rede virtual do toodeploy hello.

### <a name="template-cli"></a>Azure CLI

1. [Instalar e configurar Olá CLI do Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que você tem a versão mais recente de saudação do hello CLI do Azure instalado. tooget ajuda para comandos CLI, digite `az <command> --help`. Em vez de instalar Olá CLI e seus pré-requisitos, você pode usar o hello Shell de nuvem do Azure. Olá Shell de nuvem do Azure é um shell Bash livre que podem ser executados diretamente no hello portal do Azure. Olá Shell de nuvem tem Olá CLI do Azure pré-instalado e configurado toouse com sua conta. Olá toouse Shell de nuvem, clique em Olá nuvem Shell **> _** botão na parte superior de saudação do hello [portal](https://portal.azure.com), ou simplesmente clicar Olá **Experimente** botão nas etapas Olá seguir. 
2. Se executado localmente Olá CLI, faça logon tooAzure com hello `az login` comando. Se usar Olá Shell de nuvem, você já está conectado.
3. toocreate um grupo de recursos de rede virtual Olá, seguinte de saudação de cópia de comando e cole-o em sua sessão CLI:

    ```azurecli-interactive
    az group create --name myResourceGroup --location eastus
    ```
    
4. Você pode implantar o modelo de saudação usando uma saudação as opções de parâmetros a seguir:
    - **Valores do parâmetro padrão**. Digite hello comando a seguir:
    
        ```azurecli-interactive
        az group deployment create --resource-group myResourceGroup --name VnetTutorial --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json`
        ```
    - **Valores do parâmetro personalizado**. Baixe e modificar o modelo de saudação antes de implantar o modelo de saudação. Também pode implantar modelo hello usando parâmetros na linha de comando hello, ou implantar o modelo de saudação com um arquivo de parâmetros separados. toodownload Olá modelo e parâmetros de arquivos, clique em Olá **procurar no GitHub** botão Olá [criar uma rede virtual com duas sub-redes](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) página de modelo. No GitHub, clique em Olá **azuredeploy.parameters.json** ou **azuredeploy.json** arquivo. Em seguida, clique em Olá **Raw** arquivo de saudação do botão toodisplay. No navegador, copie o conteúdo de saudação do arquivo hello. Salve o arquivo de tooa de conteúdo de saudação em seu computador. Você pode modificar os valores de parâmetro hello no modelo de saudação ou implantar o modelo de saudação com um arquivo de parâmetros separados.  

    Saiba mais sobre toolearn como toodeploy modelos usando esses métodos, digite `az group deployment create --help`.

### <a name="template-powershell"></a>PowerShell

1. Instale a versão mais recente Olá de saudação do PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Se você for novo tooAzure PowerShell, consulte [visão geral do Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Em uma sessão do PowerShell, toosign com seus [conta do Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account), digite `login-azurermaccount`.
3. toocreate um grupo de recursos de rede virtual do hello, digite Olá comando a seguir:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
    ```
    
4. Você pode implantar o modelo de saudação usando uma saudação as opções de parâmetros a seguir:
    - **Valores do parâmetro padrão**. Digite hello comando a seguir:
    
        ```powershell
        New-AzureRmResourceGroupDeployment -Name VnetTutorial -ResourceGroupName myResourceGroup -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json
        ```
        
    - **Valores do parâmetro personalizado**. Baixe e modificar o modelo de saudação antes de implantá-lo. Também pode implantar modelo hello usando parâmetros na linha de comando hello, ou implantar o modelo de saudação com um arquivo de parâmetros separados. toodownload Olá modelo e parâmetros de arquivos, clique em Olá **procurar no GitHub** botão Olá [criar uma rede virtual com duas sub-redes](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) página de modelo. No GitHub, clique em Olá **azuredeploy.parameters.json** ou **azuredeploy.json** arquivo. Em seguida, clique em Olá **Raw** arquivo de saudação do botão toodisplay. No navegador, copie o conteúdo de saudação do arquivo hello. Salve o arquivo de tooa de conteúdo de saudação em seu computador. Você pode modificar os valores de parâmetro hello no modelo de saudação ou implantar o modelo de saudação com um arquivo de parâmetros separados.  

    Saiba mais sobre toolearn como toodeploy modelos usando esses métodos, digite `Get-Help New-AzureRmResourceGroupDeployment`. 

## <a name="delete"></a>Excluir recursos

Quando você concluir este tutorial, você pode desejar que recursos de saudação toodelete que você criou, para que você não incorrer em encargos de uso. Excluir um grupo de recursos também exclui todos os recursos que estão no grupo de recursos de saudação.

### <a name="delete-portal"></a>Portal do Azure

1. Na caixa de pesquisa do portal hello, insira **myResourceGroup**. Nos resultados da pesquisa de saudação, clique em **myResourceGroup**.
2. Em Olá **myResourceGroup** folha, clique em Olá **excluir** ícone.
3. tooconfirm Olá exclusão, Olá **Olá tipo nome do grupo de recursos** , digite **myResourceGroup**e, em seguida, clique em **excluir**.

### <a name="delete-cli"></a>Azure CLI

Em uma sessão CLI, digite Olá comando a seguir:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

Em uma sessão do PowerShell, digite Olá comando a seguir:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a>Próximas etapas

- Consulte toolearn sobre todas as configurações de sub-rede e rede virtual [gerenciar redes virtuais](virtual-network-manage-network.md#view-vnet) e [gerenciar sub-redes de rede virtual](virtual-network-manage-subnet.md#create-subnet). Você tem várias opções para o uso de redes virtuais e sub-redes em uma produção toomeet diferente dos requisitos do ambiente.
- toofilter entrada e saída de tráfego de sub-rede, criar e aplicar [grupos de segurança de rede](virtual-networks-nsg.md) toosubnets.
- Criar um [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou um [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) máquina virtual e, em seguida, conecte-o rede virtual existente do tooan.
- redes virtuais tooconnect dois em Olá mesmo local do Azure, crie um [emparelhamento de rede virtual](virtual-network-peering-overview.md) entre redes virtuais hello.
- Conectar-se a rede de local de tooan Olá rede virtual usando um [Gateway VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [rota expressa do Azure](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) circuito.
