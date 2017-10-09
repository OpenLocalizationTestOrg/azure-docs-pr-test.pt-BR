---
title: "aaaCreate virtual do Azure rede emparelhamento - diferentes modelos de implantação - mesma assinatura | Microsoft Docs"
description: "Saiba como toocreate um emparelhamento de rede virtual entre redes virtuais criadas por meio de modelos diferentes de implantação do Azure que existem no hello mesma assinatura do Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: 365156d651c9042ed52baeb15bf629fcc5329af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a>Criar um emparelhamento de rede virtual – modelos de implantação diferentes e na mesma assinatura 

Neste tutorial, você aprenderá toocreate uma emparelhamento entre redes virtuais criadas por meio de diferentes modelos de implantação de rede virtual. Ambas as redes virtuais existirem no hello mesmo assinatura. Emparelhamento duas redes virtuais habilita recursos toocommunicate redes virtuais diferentes entre si com hello mesma largura de banda e latência, como se foram recursos Olá no hello mesma rede virtual. Saiba mais sobre [Emparelhamento de rede virtual](virtual-network-peering-overview.md). 

Olá etapas toocreate um emparelhamento de rede virtual são diferentes, dependendo se as redes virtuais Olá estão em Olá igual ou diferente, assinaturas e qual [modelo de implantação do Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Olá as redes virtuais são criadas a. Saiba como toocreate um virtual rede emparelhamento em outros cenários, clicando em cenário de saudação do hello a tabela a seguir:

|Modelo de implantação do Azure  | Assinatura do Azure  |
|--------- |---------|
|[Ambos Resource Manager](virtual-network-create-peering.md) |Idêntico|
|[Ambos Resource Manager](create-peering-different-subscriptions.md) |Diferente|
|[Um Resource Manager, um clássico](create-peering-different-deployment-models-subscriptions.md) |Diferente|

Não é possível criar um emparelhamento de rede virtual entre duas redes virtuais implantadas por meio do modelo de implantação clássico hello. Um emparelhamento de rede virtual só pode ser criado entre duas redes virtuais que existem no hello mesma região do Azure. Se você precisar tooconnect as redes virtuais que foram criados por meio do modelo de implantação clássico hello, ou que existe em diferentes regiões do Azure, você pode usar um Azure [Gateway VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect Olá redes virtuais. 

Você pode usar o hello [portal do Azure](#portal), hello Azure [interface de linha de comando](#cli) (CLI), ou o Azure [PowerShell](#powershell) toocreate um emparelhamento de rede virtual. Clique em qualquer Olá anterior ferramenta links toogo diretamente toohello as etapas para criar uma rede virtual emparelhamento usando sua ferramenta de escolha.

## <a name="cli"></a>Criar emparelhamento – Portal

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
4. Clique em **+ Novo**. Em Olá **Olá pesquisa Marketplace** , digite *rede Virtual*. Clique em **rede Virtual** quando ele aparece nos resultados da pesquisa hello. 
5. Em Olá **rede Virtual** folha, selecione **clássico** em Olá **selecionar um modelo de implantação** caixa e, em seguida, clique em **criar**.
6. Em Olá **criar rede virtual** folha, inserir, ou selecione os valores para Olá configurações a seguir e clique em **criar**:
    - **Nome**: *myVnet2*
    - **Espaço de endereço**: *10.1.0.0/16*
    - **Nome da sub-rede**: *padrão*
    - **Intervalo de endereços da sub-rede**: *10.1.0.0/24*
    - **Assinatura**: selecione sua assinatura
    - **Grupo de recursos**: selecione **Usar existente** e selecione *myResourceGroup*
    - **Localização**: *Leste dos EUA*
7. Em Olá **pesquisar recursos** caixa na parte superior de saudação do portal hello, tipo *myResourceGroup*. Clique em **myResourceGroup** quando ele aparece nos resultados da pesquisa hello. Uma folha é exibido para Olá **myresourcegroup** grupo de recursos. grupo de recursos de saudação contém Olá duas redes virtuais criadas nas etapas anteriores.
8. Clique em **myVNet1**.
9. Em Olá **myVnet1** folha que aparece, clique em **emparelhamentos** da lista de vertical Olá opções Olá lado esquerdo da folha de saudação.
10. Em Olá **myVnet1 - emparelhamentos** folha que aparecer, clique em **+ adicionar**
11. Em Olá **adicionar emparelhamento** folha que aparece, digite, ou selecione Olá as opções a seguir e clique em **Okey**:
     - **Nome**: *myVnet1ToMyVnet2*
     - **Modelo de implantação de rede virtual**: selecione **Clássico**. 
     - **Assinatura**: selecione sua assinatura
     - **Rede virtual**: clique em **Escolher uma rede virtual** e, em seguida, clique em **myVnet2**.
     - **Permitir acesso à rede virtual:** verifique se a opção **Habilitado** está selecionada.
    Nenhuma outra configuração é usada neste tutorial. ler toolearn sobre todas as configurações de emparelhamento, [gerenciar emparelhamentos de rede virtual](virtual-network-manage-peering.md#create-a-peering).
12. Depois de clicar em **Okey** na etapa anterior de saudação, Olá **adicionar emparelhamento** folha fecha e consulte Olá **myVnet1 - emparelhamentos** folha novamente. Depois de alguns segundos, Olá emparelhamento que você criou aparece na folha de saudação. **Conectado** está listado no hello **STATUS EMPARELHAMENTO** coluna Olá **myVnet1ToMyVnet2** emparelhamento é criado.

    Olá emparelhamento agora está estabelecido. Todos os recursos do Azure que criar a rede virtual agora estão capaz de toocommunicate entre si por meio de seus endereços IP. Se você estiver usando a resolução de nomes do Azure padrão para redes virtuais hello, Olá recursos em redes virtuais Olá não estão tooresolve capaz de nomes entre redes virtuais hello. Se você quiser tooresolve nomes entre redes virtuais em um emparelhamento, você deve criar seu próprio servidor DNS. Saiba como tooset backup [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
13. **Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.
14. **Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em Olá [excluir recursos](#delete-portal) deste artigo.

## <a name="cli"></a>Criar emparelhamento – CLI do Azure

1. [Instalar](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) rede virtual de Olá toocreate da saudação 1.0 da CLI do Azure (clássica).
2. Abra uma sessão de comando e de log em tooAzure usando Olá `azure login` comando.
3. Execute Olá CLI no modo de gerenciamento de serviço digitando o hello `azure config mode asm` comando.
4. Digite hello toocreate Olá rede virtual (clássica) de comando a seguir:
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. Crie um grupo de recursos e uma rede virtual (Resource Manager). Você pode usar o hello CLI 1.0 ou 2.0 ([instalar](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)). Neste tutorial, Olá 2.0 do CLI é a rede virtual do toocreate usado hello (Gerenciador de recursos), como 2.0 deve ser usado toocreate Olá emparelhamento. Execute Olá seguinte bash script CLI em sua máquina local com hello CLI 2.0.4 ou posterior instalado. Para opções de execução bash scripts da CLI no cliente Windows, consulte [em execução Olá CLI do Azure no Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Você também pode executar o script hello usando Olá Shell de nuvem do Azure. Olá Shell de nuvem do Azure é um shell Bash livre que podem ser executados diretamente no hello portal do Azure. Ele tem Olá CLI do Azure pré-instalado e configurado toouse com sua conta. Clique em Olá **Experimente** botão no script hello que segue, que invoca um Shell de nuvem que registra que você pode fazer logon no tooyour conta do Azure com. tooexecute Olá script, clique em Olá **cópia** botão e colar, conteúdo Olá para o Shell de nuvem, em seguida, pressione `Enter`.

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create hello virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. Crie uma rede virtual emparelhamento entre Olá duas redes virtuais criadas por meio de saudação diferentes modelos de implantação. Copie Olá editor de texto de tooa de script a seguir em seu computador. Substitua `<subscription id>` por sua ID da assinatura. Se você não souber a Id da assinatura, digite Olá `az account show` comando. Olá valor **id** Olá saída é sua ID de assinatura Cole o script hello modificado na sessão CLI tooyour e, em seguida, pressione `Enter`.

    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. Após a execução do script hello, examine Olá emparelhamento para rede virtual da saudação (Gerenciador de recursos). A seguir Olá cópia de comando, cole-o em sua sessão CLI e pressione `Enter`:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Olá saída mostra **conectado** em Olá **PeeringState** coluna. 

    Todos os recursos do Azure que criar a rede virtual agora estão capaz de toocommunicate entre si por meio de seus endereços IP. Se você estiver usando a resolução de nomes do Azure padrão para redes virtuais hello, Olá recursos em redes virtuais Olá não estão tooresolve capaz de nomes entre redes virtuais hello. Se você quiser tooresolve nomes entre redes virtuais em um emparelhamento, você deve criar seu próprio servidor DNS. Saiba como tooset backup [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
8. **Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.
9. **Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em [excluir recursos](#delete-cli) neste artigo.

## <a name="powershell"></a>Criar emparelhamento – PowerShell

1. Instale a versão mais recente Olá de saudação do PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) e [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulos. Se você for novo tooAzure PowerShell, consulte [visão geral do Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Inicie uma sessão do PowerShell.
3. No PowerShell, faça logon no tooAzure digitando Olá `Add-AzureAccount` comando.
4. toocreate uma rede virtual (clássica) com o PowerShell, você deve criar um novo ou modificar um existente, o arquivo de configuração de rede. Saiba como muito[exportar, atualizar e importar arquivos de configuração de rede](virtual-networks-using-network-configuration-file.md). Olá arquivo deve incluir a seguir Olá **VirtualNetworkSite** elemento para a rede virtual de saudação usado neste tutorial:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Importar um arquivo de configuração de rede alterada pode causar alterações tooexisting de redes virtuais (clássico) na sua assinatura. Verifique se você adicionar apenas a rede virtual anterior de saudação e você não alterar ou remover todas as redes virtuais existentes da sua assinatura. 
5. Faça logon na rede virtual de saudação toocreate do tooAzure (Gerenciador de recursos) inserindo Olá `login-azurermaccount` comando. conta Olá com que log deve ter Olá permissões necessárias toocreate um emparelhamento de rede virtual. Consulte Olá [permissões](#permissions) deste artigo para obter detalhes.
6. Crie um grupo de recursos e uma rede virtual (Resource Manager). Copie o script hello, cole-o no PowerShell e pressione `Enter`.

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create hello virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. Crie uma rede virtual emparelhamento entre Olá duas redes virtuais criadas por meio de saudação diferentes modelos de implantação. Copie Olá editor de texto de tooa de script a seguir em seu computador. Substitua `<subscription id>` por sua ID da assinatura. Se você não souber a Id da assinatura, digite Olá `Get-AzureRmSubscription` comando tooview-lo. Olá valor **Id** em Olá retornados a saída é a ID da assinatura. script de saudação tooexecute, Olá cópia modificado script a partir do editor de texto, em seguida, clique em sua sessão do PowerShell e pressione `Enter`.

    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. Após a execução do script hello, examine Olá emparelhamento para rede virtual da saudação (Gerenciador de recursos). A seguir Olá cópia de comando, cole-o na sua sessão do PowerShell e pressione `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Olá saída mostra **conectado** em Olá **PeeringState** coluna.

    Todos os recursos do Azure que criar a rede virtual agora estão capaz de toocommunicate entre si por meio de seus endereços IP. Se você estiver usando a resolução de nomes do Azure padrão para redes virtuais hello, Olá recursos em redes virtuais Olá não estão tooresolve capaz de nomes entre redes virtuais hello. Se você quiser tooresolve nomes entre redes virtuais em um emparelhamento, você deve criar seu próprio servidor DNS. Saiba como tooset backup [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

9. **Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.
10. **Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em [excluir recursos](#delete-powershell) neste artigo.
 
## <a name="permissions"></a>Permissões

contas de saudação que usar toocreate um emparelhamento de rede virtual devem ter função necessário hello ou as permissões. Por exemplo, se foram emparelhamento duas redes virtuais chamadas myVnet1 e myVnet2, sua conta deve ser atribuída Olá função mínimo ou as permissões para cada rede virtual a seguir:
    
|Rede virtual|Modelo de implantação|Função|Permissões|
|---|---|---|---|
|myVnet1|Gerenciador de Recursos|[Colaborador de rede](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Clássico|[Colaborador de rede clássica](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/D|
|myVnet2|Gerenciador de Recursos|[Colaborador de rede](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Clássico|[Colaborador de rede clássica](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Saiba mais sobre [funções internas](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) e atribuindo permissões específicas muito[funções personalizadas](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (somente no Gerenciador de recursos).

## <a name="delete"></a>Excluir recursos
Quando concluir este tutorial, você pode desejar que recursos de saudação toodelete criado no tutorial hello, portanto você não incorrer em encargos de uso. Excluir um grupo de recursos também exclui todos os recursos que estão no grupo de recursos de saudação.

### <a name="delete-portal"></a>Portal do Azure

1. Na caixa de pesquisa do portal hello, insira **myResourceGroup**. Nos resultados da pesquisa de saudação, clique em **myResourceGroup**.
2. Em Olá **myResourceGroup** folha, clique em Olá **excluir** ícone.
3. tooconfirm Olá exclusão, Olá **Olá tipo nome do grupo de recursos** , digite **myResourceGroup**e, em seguida, clique em **excluir**.

### <a name="delete-cli"></a>Azure CLI

1. Use a rede virtual de saudação toodelete da saudação 2.0 do CLI do Azure (Gerenciador de recursos) com hello comando a seguir:

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. Use a rede virtual de saudação toodelete da saudação 1.0 da CLI do Azure (clássico) com hello comandos a seguir:

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. Digite hello toodelete hello (Gerenciador de recursos) de rede virtual de comando a seguir:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. toodelete Olá rede virtual (clássica) com o PowerShell, você deve modificar um arquivo de configuração de rede existente. Saiba como muito[exportar, atualizar e importar arquivos de configuração de rede](virtual-networks-using-network-configuration-file.md). Remova Olá elemento VirtualNetworkSite para rede virtual de saudação usado neste tutorial a seguir:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Importar um arquivo de configuração de rede alterada pode causar alterações tooexisting de redes virtuais (clássico) na sua assinatura. Verifique se você remover apenas a rede virtual anterior de saudação e você não alterar ou remover quaisquer outras redes virtuais existentes da sua assinatura. 

## <a name="next-steps"></a>Próximas etapas

- Familiarize por completo com [comportamentos e restrições importantes do emparelhamento de rede virtual](virtual-network-manage-peering.md#requirements-and-constraints) antes de criar um emparelhamento de rede virtual para uso em produção.
- Saiba mais sobre todas as [configurações de emparelhamento de rede virtual](virtual-network-manage-peering.md#create-a-peering).
- Saiba como muito[criar um hub e spoke de topologia de rede](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) com o emparelhamento de rede virtual.
