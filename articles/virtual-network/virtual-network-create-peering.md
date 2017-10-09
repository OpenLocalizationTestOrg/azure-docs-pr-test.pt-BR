---
title: aaaCreate um emparelhamento de rede virtual do Azure - Gerenciador de recursos - mesma assinatura | Microsoft Docs
description: Saiba como toocreate um emparelhamento de rede virtual entre redes virtuais criadas por meio de Gerenciador de recursos que existem no hello mesmo assinatura do Azure.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a>Criar um emparelhamento de rede virtual – Resource Manager, mesma assinatura

Neste tutorial, você aprenderá toocreate uma emparelhamento entre redes virtuais criadas por meio do Gerenciador de recursos de rede virtual. Ambas as redes virtuais existirem no hello mesmo assinatura. Emparelhamento duas redes virtuais habilita recursos toocommunicate redes virtuais diferentes entre si com hello mesma largura de banda e latência, como se foram recursos Olá no hello mesma rede virtual. Saiba mais sobre [Emparelhamento de rede virtual](virtual-network-peering-overview.md). 

Olá etapas toocreate um emparelhamento de rede virtual são diferentes, dependendo se as redes virtuais Olá estão em Olá igual ou diferente, assinaturas e qual [modelo de implantação do Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Olá as redes virtuais são criadas a. Saiba como toocreate um virtual rede emparelhamento em outros cenários, clicando em cenário de saudação do hello a tabela a seguir:

|Modelo de implantação do Azure  | Assinatura do Azure  |
|--------- |---------|
|[Ambos Resource Manager](create-peering-different-subscriptions.md) |Diferente|
|[Um Resource Manager, um clássico](create-peering-different-deployment-models.md) |Idêntico|
|[Um Resource Manager, um clássico](create-peering-different-deployment-models-subscriptions.md) |Diferente|

Não é possível criar um emparelhamento de rede virtual entre duas redes virtuais implantadas por meio do modelo de implantação clássico hello. Um emparelhamento de rede virtual só pode ser criado entre duas redes virtuais que existem no hello mesma região do Azure. Se você precisar tooconnect as redes virtuais que foram criados por meio do modelo de implantação clássico hello, ou que existe em diferentes regiões do Azure, você pode usar um Azure [Gateway VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect Olá redes virtuais. 

Você pode usar o hello [portal do Azure](#portal), hello Azure [interface de linha de comando](#cli) (CLI), Azure [PowerShell](#powershell), ou um [modelo do Azure Resource Manager](#template) toocreate um emparelhamento de rede virtual. Clique em qualquer Olá anterior ferramenta links toogo diretamente toohello as etapas para criar uma rede virtual emparelhamento usando sua ferramenta de escolha.

## <a name="portal"></a>Criar emparelhamento – portal do Azure

1. Faça logon no toohello [portal do Azure](https://portal.azure.com). conta Olá com que log deve ter Olá permissões necessárias toocreate um emparelhamento de rede virtual. Consulte Olá [permissões](#permissions) deste artigo para obter detalhes.
2. Clique em **+ Novo**, em **Rede** e, em seguida, em **Rede virtual**.
3. Em Olá **criar rede virtual** folha, inserir, ou selecione os valores para Olá configurações a seguir e clique em **criar**:
    - **Nome**: *myVnet1*
    - **Espaço de endereço**: *10.0.0.0/16*
    - **Nome da sub-rede**: *padrão*
    - **Intervalo de endereços da sub-rede**: *10.0.0.0/24*
    - **Assinatura**: selecione sua assinatura
    - **Grupo de recursos**: selecione **Criar novo** e insira *myResourceGroup*
    - **Localização**: *Leste dos EUA*
4. Conclua as etapas 2-3 novamente especificando Olá valores na etapa 3 a seguir:
    - **Nome**: *myVnet2*
    - **Espaço de endereço**: *10.1.0.0/16*
    - **Nome da sub-rede**: *padrão*
    - **Intervalo de endereços da sub-rede**: *10.1.0.0/24*
    - **Assinatura**: selecione sua assinatura
    - **Grupo de recursos**: selecione **Usar existente** e selecione *myResourceGroup*
    - **Localização**: *Leste dos EUA*
5. Em Olá **pesquisar recursos** caixa na parte superior de saudação do portal hello, tipo *myResourceGroup*. Clique em **myResourceGroup** quando ele aparece nos resultados da pesquisa hello. Uma folha é exibido para Olá **myresourcegroup** grupo de recursos. grupo de recursos de saudação contém Olá duas redes virtuais criadas nas etapas anteriores.
6. Clique em **myVNet1**.
7. Em Olá **myVnet1** folha que aparece, clique em **emparelhamentos** da lista de vertical Olá opções Olá lado esquerdo da folha de saudação.
8. Em Olá **myVnet1 - emparelhamentos** folha que aparecer, clique em **+ adicionar**
9. Em Olá **adicionar emparelhamento** folha que aparece, digite, ou selecione Olá as opções a seguir e clique em **Okey**:
     - **Nome**: *myVnet1ToMyVnet2*
     - **Modelo de implantação de rede virtual**: selecione **Resource Manager**. 
     - **Assinatura**: selecione sua assinatura
     - **Rede virtual**: clique em **Escolher uma rede virtual** e, em seguida, clique em **myVnet2**.
     - **Permitir acesso à rede virtual:** verifique se a opção **Habilitado** está selecionada.
    Nenhuma outra configuração é usada neste tutorial. ler toolearn sobre todas as configurações de emparelhamento, [gerenciar emparelhamentos de rede virtual](virtual-network-manage-peering.md#create-a-peering).
10. Depois de clicar em **Okey** na etapa anterior de saudação, Olá **adicionar emparelhamento** folha fecha e consulte Olá **myVnet1 - emparelhamentos** folha novamente. Depois de alguns segundos, Olá emparelhamento que você criou aparece na folha de saudação. **Iniciada** está listado no hello **STATUS EMPARELHAMENTO** coluna Olá **myVnet1ToMyVnet2** emparelhamento é criado. Você emparelhadas tooVnet2 Vnet1, mas agora myVnet2 toomyVnet1 deve ser par. Olá emparelhamento deve ser criado em ambas as direções tooenable recursos Olá toocommunicate de redes virtuais entre si.
11. Conclua as etapas 5 a 10 novamente para a myVnet2.  Nome hello emparelhamento *myVnet2ToMyVnet1*.
12. Alguns segundos depois de clicar em **Okey** toocreate Olá emparelhamento para MyVnet2, hello **myVnet2ToMyVnet1** emparelhamento você acabou de criar está listado com **conectado** em Olá  **STATUS de EMPARELHAMENTO** coluna.
13. Conclua as etapas 5 a 7 novamente para a MyVnet1. Olá **STATUS EMPARELHAMENTO** para Olá **myVnet1ToVNet2** emparelhamento agora também está **conectado**. Olá emparelhamento é estabelecida com êxito depois de ver **conectado** em Olá **STATUS EMPARELHAMENTO** coluna para ambas as redes virtuais no emparelhamento via protocolo hello.
14. **Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.
15. **Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em Olá [excluir recursos](#delete-portal) deste artigo.

Todos os recursos do Azure que criar a rede virtual agora estão capaz de toocommunicate entre si por meio de seus endereços IP. Se você estiver usando a resolução de nomes do Azure padrão para redes virtuais hello, Olá recursos em redes virtuais Olá não estão tooresolve capaz de nomes entre redes virtuais hello. Se você quiser tooresolve nomes entre redes virtuais em um emparelhamento, você deve criar seu próprio servidor DNS. Saiba como tooset backup [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="cli"></a>Criar emparelhamento – CLI do Azure

saudação de script a seguir:

- Requer Olá CLI do Azure versão 2.0.4 ou posterior. versão de hello toofind, execute Olá `az --version` comando. Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Funciona em um shell do Bash. Para obter opções sobre a execução de scripts de CLI do Azure no cliente do Windows, consulte [em execução Olá CLI do Azure no Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Em vez de instalar hello CLI e suas dependências, você pode usar o hello Shell de nuvem do Azure. Olá Shell de nuvem do Azure é um shell Bash livre que podem ser executados diretamente no hello portal do Azure. Ele tem Olá CLI do Azure pré-instalado e configurado toouse com sua conta. Clique em Olá **Experimente** botão no script hello que segue, que invoca um Shell de nuvem que registra que você pode fazer logon no tooyour conta do Azure com. tooexecute Olá script, clique em Olá **cópia** botão e cole o conteúdo de saudação em seu Shell de nuvem.

1. Crie um grupo de recursos e duas redes virtuais.

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. Crie uma rede virtual emparelhamento entre duas redes virtuais de saudação.
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. Após a execução do script hello, examine emparelhamentos Olá para cada rede virtual. 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Executar comando anterior Olá novamente, substituindo *myVnet1* com *myVnet2*. saída de Hello dos dois comandos mostra **conectado** em Olá **PeeringState** coluna.

     Todos os recursos do Azure que criar a rede virtual agora estão capaz de toocommunicate entre si por meio de seus endereços IP. Se você estiver usando a resolução de nomes do Azure padrão para redes virtuais hello, Olá recursos em redes virtuais Olá não estão tooresolve capaz de nomes entre redes virtuais hello. Se você quiser tooresolve nomes entre redes virtuais em um emparelhamento, você deve criar seu próprio servidor DNS. Saiba como tooset backup [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

4. **Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.
5. **Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em [excluir recursos](#delete-cli) neste artigo.


## <a name="powershell"></a>Criar emparelhamento – PowerShell

1. Instale a versão mais recente Olá de saudação do PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Se você for novo tooAzure PowerShell, consulte [visão geral do Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. toostart uma sessão do PowerShell, ir muito**iniciar**, digite **powershell**e, em seguida, clique em **PowerShell**.
3. No PowerShell, faça logon no tooAzure digitando Olá `login-azurermaccount` comando. conta Olá com que log deve ter Olá permissões necessárias toocreate um emparelhamento de rede virtual. Consulte Olá [permissões](#permissions) deste artigo para obter detalhes.
4. Crie um grupo de recursos e duas redes virtuais. script de saudação tooexecute, cópia Olá seguinte script, cole-o no PowerShell e pressione `Enter` após a última linha de saudação aparece na tela hello:

    ```powershell
    # Variables for common values used throughout hello script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. Crie uma rede virtual emparelhamento entre duas redes virtuais de saudação. A seguir Olá cópia script, cole em tooPowerShell e, em seguida, pressione `Enter` após a última linha de saudação aparece na tela hello:
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. subredes tooreview Olá para rede virtual Olá, cópia Olá seguinte comando, cole em tooPowerShell e, em seguida, pressione `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Executar comando anterior Olá novamente, substituindo *myVnet1* com *myVnet2*. saída de Hello dos dois comandos mostra **conectado** em Olá **PeeringState** coluna.
7. **Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.
8. **Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em [excluir recursos](#delete-powershell) neste artigo.

Todos os recursos do Azure que criar a rede virtual agora estão capaz de toocommunicate entre si por meio de seus endereços IP. Se você estiver usando a resolução de nomes do Azure padrão para redes virtuais hello, Olá recursos em redes virtuais Olá não estão tooresolve capaz de nomes entre redes virtuais hello. Se você quiser tooresolve nomes entre redes virtuais em um emparelhamento, você deve criar seu próprio servidor DNS. Saiba como tooset backup [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="template"></a>Criar emparelhamento – modelo do Resource Manager

1. Consulte [Criar um emparelhamento de rede virtual](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) usando um modelo do Resource Manager. As instruções são fornecidas com o modelo de saudação para implantar o modelo de saudação usando Olá Olá CLI do Azure, o PowerShell ou o portal do Azure. Log na ferramenta toowhichever escolher toodeploy Olá modelo usando uma conta que tenha Olá permissões necessárias toocreate um emparelhamento de rede virtual. Consulte Olá [permissões](#permissions) deste artigo para obter detalhes.
2. **Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.
3. **Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em Olá [excluir recursos](#delete) deste artigo, usando Olá Olá CLI do Azure, o PowerShell ou o portal do Azure.

## <a name="permissions"></a>Permissões

contas de saudação que usar toocreate um emparelhamento de rede virtual devem ter função necessário hello ou as permissões. Por exemplo, se foram emparelhamento duas redes virtuais, VNet1 e VNet2 de chamada, sua conta deverá ser atribuída Olá função mínimo ou as permissões para cada rede virtual a seguir:
    
|Rede virtual|Função|Permissões|
|---|---|---|
|VNet1|[Colaborador de rede](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|VNet2|[Colaborador de rede](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

Saiba mais sobre [funções internas](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) e atribuindo permissões específicas muito[funções personalizadas](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (somente no Gerenciador de recursos).

## <a name="delete"></a>Excluir recursos
Quando concluir este tutorial, você pode desejar que recursos de saudação toodelete criado no tutorial hello, portanto você não incorrer em encargos de uso. Excluir um grupo de recursos também exclui todos os recursos que estão no grupo de recursos de saudação.

### <a name="delete-portal"></a>Portal do Azure

1. Na caixa de pesquisa do portal hello, insira **myResourceGroup**. Nos resultados da pesquisa de saudação, clique em **myResourceGroup**.
2. Em Olá **myResourceGroup** folha, clique em Olá **excluir** ícone.
3. tooconfirm Olá exclusão, Olá **Olá tipo nome do grupo de recursos** , digite **myResourceGroup**e, em seguida, clique em **excluir**.

### <a name="delete-cli"></a>Azure CLI

Digite hello comando a seguir:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>PowerShell

Digite hello comando a seguir:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a>Próximas etapas

- Familiarize por completo com [comportamentos e restrições importantes do emparelhamento de rede virtual](virtual-network-manage-peering.md#requirements-and-constraints) antes de criar um emparelhamento de rede virtual para uso em produção.
- Saiba mais sobre todas as [configurações de emparelhamento de rede virtual](virtual-network-manage-peering.md#create-a-peering).
- Saiba como muito[criar um hub e spoke de topologia de rede](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) com o emparelhamento de rede virtual.
