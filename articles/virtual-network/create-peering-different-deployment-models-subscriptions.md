---
title: "aaaCreate um emparelhamento de rede virtual do Azure - implantação de diferente modelos - diferentes assinaturas | Microsoft Docs"
description: "Saiba como toocreate uma rede virtual emparelhamento entre redes virtuais criadas por meio de modelos diferentes de implantação do Azure que existem em diferentes assinaturas do Azure."
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
ms.openlocfilehash: 865bdabb5b87523ba943d7b5dcbdc2475b78bdb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-and-subscriptions"></a>Criar um emparelhamento de rede virtual – modelos de implantação e assinaturas diferentes

Neste tutorial, você aprenderá toocreate uma emparelhamento entre redes virtuais criadas por meio de diferentes modelos de implantação de rede virtual. redes virtuais Olá existem em assinaturas diferentes. Emparelhamento duas redes virtuais habilita recursos toocommunicate redes virtuais diferentes entre si com hello mesma largura de banda e latência, como se foram recursos Olá no hello mesma rede virtual. Saiba mais sobre [Emparelhamento de rede virtual](virtual-network-peering-overview.md). 

Olá etapas toocreate um emparelhamento de rede virtual são diferentes, dependendo se as redes virtuais Olá estão em Olá igual ou diferente, assinaturas e qual [modelo de implantação do Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Olá as redes virtuais são criadas a. Saiba como toocreate um virtual rede emparelhamento em outros cenários, clicando em cenário de saudação do hello a tabela a seguir:

|Modelo de implantação do Azure  | Assinatura do Azure  |
|--------- |---------|
|[Ambos Resource Manager](virtual-network-create-peering.md) |Idêntico|
|[Ambos Resource Manager](create-peering-different-subscriptions.md) |Diferente|
|[Um Resource Manager, um clássico](create-peering-different-deployment-models.md) |Idêntico|

Não é possível criar um emparelhamento de rede virtual entre duas redes virtuais implantadas por meio do modelo de implantação clássico hello. Um emparelhamento de rede virtual só pode ser criado entre duas redes virtuais que existem no hello mesma região do Azure. Ao criar uma rede virtual emparelhamento entre redes virtuais que existem em assinaturas diferentes, Olá assinaturas devem ser associados toohello mesmo Active Directory do Azure locatário. Se você ainda não tem um locatário do Azure Active Directory, você pode [criar um](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch) rapidamente. Se você precisar tooconnect virtual redes que foram criadas por meio do modelo de implantação clássico hello, ou que existem em diferentes regiões do Azure ou que existe nas assinaturas associadas toodifferent locatários de Active Directory do Azure, você pode usar um Azure [Gateway VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect Olá redes virtuais. 

> [!WARNING]
> A criação de um emparelhamento de rede virtual entre redes virtuais criadas com modelos de implantação do Azure diferentes que existem em assinaturas diferentes está atualmente em versão prévia. Emparelhamentos de rede virtual criados nesse cenário podem não ter Olá mesmo nível de disponibilidade e confiabilidade como criar uma rede virtual emparelhamento em cenários de versão de disponibilidade em geral. Emparelhamentos de rede virtual criados nesse cenário não têm suporte, podem ter recursos restringidos e podem não estar disponíveis em todas as regiões do Azure. Para notificações mais recentes de Olá em disponibilidade e o status desse recurso, verifique Olá [atualizações de rede Virtual do Azure](https://azure.microsoft.com/updates/?product=virtual-network) página.

Você pode usar o hello [portal do Azure](#portal), hello Azure [interface de linha de comando](#cli) (CLI), ou o Azure [PowerShell](#powershell) toocreate um emparelhamento de rede virtual. Clique em qualquer Olá anterior ferramenta links toogo diretamente toohello as etapas para criar uma rede virtual emparelhamento usando sua ferramenta de escolha.

## <a name="register"></a>Registre-se para visualização de saudação

tooregister para visualização hello, etapas Olá completa que seguem para ambas as assinaturas que contêm as redes virtuais Olá deseja toopeer. Olá, somente a ferramenta você pode usar tooregister para visualização de saudação é PowerShell.

1. Instale a versão mais recente Olá de saudação do PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Se você for novo tooAzure PowerShell, consulte [visão geral do Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Iniciar uma sessão do PowerShell e de log em tooAzure usando Olá `login-azurermaccount` comando.
3. Registre sua assinatura para a visualização de saudação inserindo Olá comandos a seguir:

    ```powershell
    Register-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    
    Register-AzureRmResourceProvider `
      -ProviderNamespace Microsoft.Network
    ```
    Não concluir etapas Olá nas seções de saudação do PowerShell, CLI do Azure ou Portal deste artigo até Olá **RegistrationState** saída é exibida após a inserção Olá comando a seguir é **registrado** para ambas as assinaturas:

    ```powershell    
    Get-AzureRmProviderFeature `
      -FeatureName AllowClassicCrossSubscriptionPeering `
      -ProviderNamespace Microsoft.Network
    ```

## <a name="portal"></a>Criar emparelhamento – portal do Azure

Este tutorial usa contas diferentes para cada assinatura. Se você estiver usando uma conta que tenha permissões tooboth assinaturas, você pode usar o hello mesmo conta para todas as etapas, ignore as etapas de saudação para fazer logoff do portal de saudação e ignore as etapas de saudação para atribuição de redes virtuais do toohello permissões de outro usuário. Antes de concluir qualquer Olá etapas a seguir, você deve registrar para visualização de saudação. tooregister, Olá concluir as etapas em Olá [registrar para visualização Olá](#register) deste artigo. Não continue com hello restantes etapas até que ambas as assinaturas são registradas para visualização de saudação.
 
1. Faça logon no toohello [portal do Azure](https://portal.azure.com) como UserA. conta Olá com que log deve ter Olá permissões necessárias toocreate um emparelhamento de rede virtual. Consulte Olá [permissões](#permissions) deste artigo para obter detalhes.
2. Clique em **+ Novo**, em **Rede** e, em seguida, em **Rede virtual**.
3. Em Olá **criar rede virtual** folha, inserir, ou selecione os valores para Olá configurações a seguir e clique em **criar**:
    - **Nome**: *myVnetA*
    - **Espaço de endereço**: *10.0.0.0/16*
    - **Nome da sub-rede**: *padrão*
    - **Intervalo de endereços da sub-rede**: *10.0.0.0/24*
    - **Assinatura:** selecione a assinatura A.
    - **Grupo de recursos**: selecione **Criar novo** e insira *myResourceGroupA*
    - **Localização**: *Leste dos EUA*
4. Em Olá **pesquisar recursos** caixa na parte superior de saudação do portal hello, tipo *myVnetA*. Clique em **myVnetA** quando ele aparece nos resultados da pesquisa hello. Uma folha é exibido para Olá **myVnetA** rede virtual.
5. Em Olá **myVnetA** folha que aparece, clique em **(IAM) do controle de acesso** da lista de vertical Olá opções Olá lado esquerdo da folha de saudação.
6. Em Olá **myVnetA - controle de acesso (IAM)** folha que aparece, clique em **+ adicionar**.
7. Em Olá **adicionar permissões** folha que aparece, selecione **Colaborador rede** em Olá **função** caixa.
8. Em Olá **selecione** caixa, selecione UserB ou digite toosearch de endereço de email do UserB para ele. Olá lista de usuários mostrado é de saudação mesmo locatário do Active Directory do Azure como rede virtual Olá estiver configurando Olá emparelhamento para. Clique em UserB quando ele aparece na lista de saudação.
9. Clique em **Salvar**.
10. Faça logoff do portal de saudação como UserA e faça logon como UserB.
11. Clique em **+ novo**, tipo *rede Virtual* em Olá **Olá pesquisa Marketplace** caixa e, em seguida, clique em **rede Virtual** nos resultados da pesquisa Olá .
12. Em Olá **rede Virtual** folha que aparece, selecione **clássico** em Olá **selecionar um modelo de implantação** caixa e, em seguida, clique em **criar**.
13.   Olá criar rede virtual (clássica) caixa que aparece, digite Olá valores a seguir:

    - **Nome**: *myVnetB*
    - **Espaço de endereço**: *10.1.0.0/16*
    - **Nome da sub-rede**: *padrão*
    - **Intervalo de endereços da sub-rede**: *10.1.0.0/24*
    - **Assinatura:** selecione a assinatura B.
    - **Grupo de recursos**: selecione **Criar novo** e insira *myResourceGroupB*
    - **Localização**: *Leste dos EUA*

14. Em Olá **pesquisar recursos** caixa na parte superior de saudação do portal hello, tipo *myVnetB*. Clique em **myVnetB** quando ele aparece nos resultados da pesquisa hello. Uma folha é exibido para Olá **myVnetB** rede virtual.
15. Em Olá **myVnetB** folha que aparece, clique em **propriedades** da lista de vertical Olá opções Olá lado esquerdo da folha de saudação. Saudação de cópia **ID de recurso**, que é usado em uma etapa posterior. ID do recurso Olá é semelhante toohello exemplo a seguir: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
16. Conclua as etapas 5 a 9 para myVnetB, inserindo **UserA** na etapa 8.
17. Faça logoff do portal de saudação como UserB e faça logon como UserA.
18. Em Olá **pesquisar recursos** caixa na parte superior de saudação do portal hello, tipo *myVnetA*. Clique em **myVnetA** quando ele aparece nos resultados da pesquisa hello. Uma folha é exibido para Olá **myVnet** rede virtual.
19. Clique em **myVnetA**.
20. Em Olá **myVnetA** folha que aparece, clique em **emparelhamentos** da lista de vertical Olá opções Olá lado esquerdo da folha de saudação.
21. Em Olá **myVnetA - emparelhamentos** folha que aparecer, clique em **+ adicionar**
22. Em Olá **adicionar emparelhamento** folha que aparece, digite, ou selecione Olá as opções a seguir e clique em **Okey**:
     - **Nome**: *myVnetAToMyVnetB*
     - **Modelo de implantação de rede virtual**: selecione **Clássico**.
     - **Sei minha ID do recurso**: marque essa caixa.
     - **ID do recurso**: insira a ID de recurso de saudação do myVnetB da etapa 15.
     - **Permitir acesso à rede virtual:** verifique se a opção **Habilitado** está selecionada.
    Nenhuma outra configuração é usada neste tutorial. ler toolearn sobre todas as configurações de emparelhamento, [gerenciar emparelhamentos de rede virtual](virtual-network-manage-peering.md#create-a-peering).
23. Depois de clicar em **Okey** na etapa anterior de saudação, Olá **adicionar emparelhamento** folha fecha e consulte Olá **myVnetA - emparelhamentos** folha novamente. Depois de alguns segundos, Olá emparelhamento que você criou aparece na folha de saudação. **Conectado** está listado no hello **STATUS EMPARELHAMENTO** coluna Olá **myVnetAToMyVnetB** emparelhamento é criado. Olá emparelhamento agora está estabelecido. Não há nenhuma necessidade toopeer Olá rede virtual (clássica) toohello rede virtual (Gerenciador de recursos).

    Todos os recursos do Azure que criar a rede virtual agora estão capaz de toocommunicate entre si por meio de seus endereços IP. Se você estiver usando a resolução de nomes do Azure padrão para redes virtuais hello, Olá recursos em redes virtuais Olá não estão tooresolve capaz de nomes entre redes virtuais hello. Se você quiser tooresolve nomes entre redes virtuais em um emparelhamento, você deve criar seu próprio servidor DNS. Saiba como tooset backup [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

24. **Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.
25. **Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em Olá [excluir recursos](#delete-portal) deste artigo.

## <a name="cli"></a>Criar emparelhamento – CLI do Azure

Este tutorial usa contas diferentes para cada assinatura. Se você estiver usando uma conta que tenha permissões tooboth assinaturas, você pode usar o hello a mesma conta para todas as etapas, ignore as etapas de saudação para registro em log fora do Azure e remove linhas de saudação do script que crie atribuições de função de usuário. Substituir UserA@azure.com e UserB@azure.com em todos os Olá scripts com nomes de usuário de saudação que você está usando para UserA e UserB a seguir. 

Antes de concluir qualquer Olá etapas a seguir, você deve registrar para visualização de saudação. tooregister, Olá concluir as etapas em Olá [registrar para visualização Olá](#register) deste artigo. Não continue com hello restantes etapas até que ambas as assinaturas são registradas para visualização de saudação.

1. [Instalar](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) rede virtual de Olá toocreate da saudação 1.0 da CLI do Azure (clássica).
2. Abra uma sessão CLI e faça logon tooAzure como UserB usando Olá `azure login` comando.
3. Execute Olá CLI no modo de gerenciamento de serviço digitando o hello `azure config mode asm` comando.
4. Digite hello toocreate Olá rede virtual (clássica) de comando a seguir:
 
    ```azurecli
    azure network vnet create --vnet myVnetB --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```
5. Olá restantes etapas deve ser concluída com um shell bash Olá CLI do Azure 2.0.4 ou posterior [instalado](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json), ou usando Olá Shell de nuvem do Azure. Olá Shell de nuvem do Azure é um shell Bash livre que podem ser executados diretamente no hello portal do Azure. Ele tem Olá CLI do Azure pré-instalado e configurado toouse com sua conta. Clique em Olá **Experimente** botão Olá scripts que abre um Shell de nuvem que registra você tooyour conta do Azure. Para opções de execução bash scripts da CLI em um cliente Windows, consulte [em execução Olá CLI do Azure no Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 
6. Copie Olá editor de texto de tooa de script a seguir em seu computador. Substitua `<SubscriptionB-Id>` por sua ID da assinatura. Se você não souber a Id da assinatura, digite Olá `az account show` comando. Olá valor **id** Olá saída é sua ID de assinatura Copie o script hello modificado, cole-o na sessão tooyour 2.0 do CLI e pressione `Enter`. 

    ```azurecli-interactive
    az role assignment create \
      --assignee UserA@azure.com \
      --role "Classic Network Contributor" \
      --scope /subscriptions/<SubscriptionB-Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

    Quando você criou a rede virtual da saudação (clássico) na etapa 4, o Azure criado rede virtual Olá no hello *padrão rede* grupo de recursos.
7. Log UserB fora do Azure e fazer logon como UserA no hello 2.0 do CLI.
8. Crie um grupo de recursos e uma rede virtual (Resource Manager). A seguir Olá cópia do script, cole-o na sessão CLI tooyour e pressione `Enter`. 

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroupA"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network A (Resource Manager).
    az network vnet create \
      --name myVnetA \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Get hello id for myVnetA.
    vNetAId=$(az network vnet show \
      --resource-group $rgName \
      --name myVnetA \
      --query id --out tsv)

    # Assign UserB permissions toomyVnetA.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope $vNetAId
    ```

9. Crie uma rede virtual emparelhamento entre Olá duas redes virtuais criadas por meio de saudação diferentes modelos de implantação. Copie Olá editor de texto de tooa de script a seguir em seu computador. Substitua `<SubscriptionB-id>` por sua ID da assinatura. Se você não souber a Id da assinatura, digite Olá `az account show` comando. Olá valor **id** Olá saída é sua ID de assinatura Azure criada Olá VPN (clássico) criado na etapa 4 em um grupo de recursos denominada *rede padrão*. Cole o script hello modificado em sua sessão CLI e, em seguida, pressione `Enter`.

    ```azurecli-interactive
    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnetAToMyVnetB \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --remote-vnet-id  /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB \
      --allow-vnet-access
    ```

10. Após a execução do script hello, examine Olá emparelhamento para rede virtual da saudação (Gerenciador de recursos). Copie Olá script a seguir e, em seguida, cole-o em sua sessão CLI:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group $rgName \
      --vnet-name myVnetA \
      --output table
    ```
    Olá saída mostra **conectado** em Olá **PeeringState** coluna.

    Todos os recursos do Azure que criar a rede virtual agora estão capaz de toocommunicate entre si por meio de seus endereços IP. Se você estiver usando a resolução de nomes do Azure padrão para redes virtuais hello, Olá recursos em redes virtuais Olá não estão tooresolve capaz de nomes entre redes virtuais hello. Se você quiser tooresolve nomes entre redes virtuais em um emparelhamento, você deve criar seu próprio servidor DNS. Saiba como tooset backup [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

11. **Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.
12. **Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em [excluir recursos](#delete-cli) neste artigo.

## <a name="powershell"></a>Criar emparelhamento – PowerShell

Este tutorial usa contas diferentes para cada assinatura. Se você estiver usando uma conta que tenha permissões tooboth assinaturas, você pode usar o hello a mesma conta para todas as etapas, ignore as etapas de saudação para registro em log fora do Azure e remove linhas de saudação do script que crie atribuições de função de usuário. Substituir UserA@azure.com e UserB@azure.com em todos os Olá scripts com nomes de usuário de saudação que você está usando para UserA e UserB a seguir. 

Antes de concluir qualquer Olá etapas a seguir, você deve registrar para visualização de saudação. tooregister, Olá concluir as etapas em Olá [registrar para visualização Olá](#register) deste artigo. Não continue com hello restantes etapas até que ambas as assinaturas são registradas para visualização de saudação.

1. Instale a versão mais recente Olá de saudação do PowerShell [Azure](https://www.powershellgallery.com/packages/Azure) e [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulos. Se você for novo tooAzure PowerShell, consulte [visão geral do Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Inicie uma sessão do PowerShell.
3. No PowerShell, faça logon na assinatura do tooUserB UserB digitando Olá `Add-AzureAccount` comando.
4. toocreate uma rede virtual (clássica) com o PowerShell, você deve criar um novo ou modificar um existente, o arquivo de configuração de rede. Saiba como muito[exportar, atualizar e importar arquivos de configuração de rede](virtual-networks-using-network-configuration-file.md). Olá arquivo deve incluir a seguir Olá **VirtualNetworkSite** elemento para a rede virtual de saudação usado neste tutorial:

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
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

5. Faça logon na assinatura do tooUserB comandos do Gerenciador de recursos do UserB toouse inserindo Olá `login-azurermaccount` comando.
6. Rede atribuir UserA permissões toovirtual a seguir Olá B. Copiar script tooa editor de texto em seu computador e substituir `<SubscriptionB-id>` com hello ID de assinatura B. Se você não souber a Id de assinatura hello, digite Olá `Get-AzureRmSubscription` comando tooview-lo. Olá valor **Id** em Olá retornados a saída é a ID da assinatura. Azure criada Olá VPN (clássico) criado na etapa 4 em um grupo de recursos denominada *rede padrão*. script de saudação tooexecute, Olá cópia modificado script, cole-o em tooPowerShell e pressione `Enter`.
    
    ```powershell 
    New-AzureRmRoleAssignment `
      -SignInName UserA@azure.com `
      -RoleDefinitionName "Classic Network Contributor" `
      -Scope /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

7. Faça logoff do Azure como UserB e de log na assinatura do tooUserA UserA inserindo Olá `login-azurermaccount` comando. conta Olá com que log deve ter Olá permissões necessárias toocreate um emparelhamento de rede virtual. Consulte Olá [permissões](#permissions) deste artigo para obter detalhes.
8. Criar rede virtual da saudação (Gerenciador de recursos) copiando Olá script, colá-lo em tooPowerShell e, em seguida, pressionando a seguir `Enter`:

    ```powershell
    # Variables for common values
      $rgName='MyResourceGroupA'
      $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network A.
    $vnetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location
    ```

9. Atribua UserB permissões toomyVnetA. A seguir Olá cópia script tooa editor de texto em seu computador e substituir `<SubscriptionA-Id>` com hello ID de assinatura A. Se você não souber a Id de assinatura hello, digite Olá `Get-AzureRmSubscription` comando tooview-lo. Olá valor **Id** em Olá retornados a saída é a ID da assinatura. Cole Olá a versão modificada do script hello no PowerShell e pressione `Enter` tooexecute-lo.

    ```powershell
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

10. Cópia Olá seguinte script tooa editor de texto em seu computador e substituir `<SubscriptionB-id>` com hello o ID da assinatura B. toopeer myVnetA toomyVNetB, copie o script hello modificado, cole-o em tooPowerShell e pressione `Enter`.

    ```powershell
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vnetA `
      -RemoteVirtualNetworkId /subscriptions/<SubscriptionB-id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB
    ```

11. Exibir o estado de emparelhamento de saudação do myVnetA copiando Olá a seguir de script, colando-os em PowerShell e pressionando `Enter`.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName $rgName `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    estado de saudação é **conectado**. Ele muda muito**conectado** depois de configurar o toomyVnetA emparelhamento de saudação do myVnetB.

    Todos os recursos do Azure que criar a rede virtual agora estão capaz de toocommunicate entre si por meio de seus endereços IP. Se você estiver usando a resolução de nomes do Azure padrão para redes virtuais hello, Olá recursos em redes virtuais Olá não estão tooresolve capaz de nomes entre redes virtuais hello. Se você quiser tooresolve nomes entre redes virtuais em um emparelhamento, você deve criar seu próprio servidor DNS. Saiba como tooset backup [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

12. **Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.
13. **Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em [excluir recursos](#delete-powershell) neste artigo.

## <a name="permissions"></a>Permissões

contas de saudação que usar toocreate um emparelhamento de rede virtual devem ter função necessário hello ou as permissões. Por exemplo, se foram emparelhamento duas redes virtuais chamadas myVnetA e myVnetB, sua conta deve ser atribuída Olá função mínimo ou as permissões para cada rede virtual a seguir:
    
|Rede virtual|Modelo de implantação|Função|Permissões|
|---|---|---|---|
|myVnetA|Gerenciador de Recursos|[Colaborador de rede](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Clássico|[Colaborador de rede clássica](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/D|
|myVnetB|Gerenciador de Recursos|[Colaborador de rede](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Clássico|[Colaborador de rede clássica](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Saiba mais sobre [funções internas](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) e atribuindo permissões específicas muito[funções personalizadas](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (somente no Gerenciador de recursos).

## <a name="delete"></a>Excluir recursos
Quando concluir este tutorial, você pode desejar que recursos de saudação toodelete criado no tutorial hello, portanto você não incorrer em encargos de uso. Excluir um grupo de recursos também exclui todos os recursos que estão no grupo de recursos de saudação.

### <a name="delete-portal"></a>Portal do Azure

1. Na caixa de pesquisa do portal hello, insira **myResourceGroupA**. Nos resultados da pesquisa de saudação, clique em **myResourceGroupA**.
2. Em Olá **myResourceGroupA** folha, clique em Olá **excluir** ícone.
3. tooconfirm Olá exclusão, Olá **Olá tipo nome do grupo de recursos** , digite **myResourceGroupA**e, em seguida, clique em **excluir**.
4. Em Olá **pesquisar recursos** caixa na parte superior de saudação do portal hello, tipo *myVnetB*. Clique em **myVnetB** quando ele aparece nos resultados da pesquisa hello. Uma folha é exibido para Olá **myVnetB** rede virtual.
5. Em Olá **myVnetB** folha, clique em **excluir**.
6. exclusão de saudação tooconfirm, clique em **Sim** em Olá **rede virtual Delete** caixa.

### <a name="delete-cli"></a>Azure CLI

1. Faça logon em tooAzure usando Olá rede virtual de saudação toodelete da CLI 2.0 (Gerenciador de recursos) com hello comando a seguir:

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```

2. Faça logon no tooAzure usando hello Azure CLI 1.0 toodelete Olá VPN (clássico) com hello comandos a seguir:

    ```azurecli
    azure config mode asm 

    azure network vnet delete --vnet myVnetB --quiet
    ```

### <a name="delete-powershell"></a>PowerShell

1. No prompt de comando do PowerShell hello, digite Olá toodelete hello (Gerenciador de recursos) de rede virtual de comando a seguir:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -Force
    ```

2. toodelete Olá rede virtual (clássica) com o PowerShell, você deve modificar um arquivo de configuração de rede existente. Saiba como muito[exportar, atualizar e importar arquivos de configuração de rede](virtual-networks-using-network-configuration-file.md). Remova Olá elemento VirtualNetworkSite para rede virtual de saudação usado neste tutorial a seguir:

    ```xml
    <VirtualNetworkSite name="myVnetB" Location="East US">
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
