---
title: emparelhamento - Gerenciador de recursos - diferentes assinaturas de rede aaaCreate virtual do Azure | Microsoft Docs
description: Saiba como toocreate uma rede virtual emparelhamento entre redes virtuais criadas pelo Gerenciador de recursos que existem em diferentes assinaturas do Azure.
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
ms.openlocfilehash: c7983a86031e061c1155144e5c493ee9578fa583
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-different-subscriptions"></a>Criar um emparelhamento de rede virtual – Resource Manager, assinaturas diferentes 

Neste tutorial, você aprenderá toocreate uma emparelhamento entre redes virtuais criadas por meio do Gerenciador de recursos de rede virtual. redes virtuais Olá existem em assinaturas diferentes. Emparelhamento duas redes virtuais habilita recursos toocommunicate redes virtuais diferentes entre si com hello mesma largura de banda e latência, como se foram recursos Olá no hello mesma rede virtual. Saiba mais sobre [Emparelhamento de rede virtual](virtual-network-peering-overview.md). 

Olá etapas toocreate um emparelhamento de rede virtual são diferentes, dependendo se as redes virtuais Olá estão em Olá igual ou diferente, assinaturas e qual [modelo de implantação do Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Olá as redes virtuais são criadas a. Saiba como toocreate um virtual rede emparelhamento em outros cenários, clicando em cenário de saudação do hello a tabela a seguir:

|Modelo de implantação do Azure  | Assinatura do Azure  |
|--------- |---------|
|[Ambos Resource Manager](virtual-network-create-peering.md) |Idêntico|
|[Um Resource Manager, um clássico](create-peering-different-deployment-models.md) |Idêntico|
|[Um Resource Manager, um clássico](create-peering-different-deployment-models-subscriptions.md) |Diferente|

Não é possível criar um emparelhamento de rede virtual entre duas redes virtuais implantadas por meio do modelo de implantação clássico hello. Um emparelhamento de rede virtual só pode ser criado entre duas redes virtuais que existem no hello mesma região do Azure. Ao criar uma rede virtual emparelhamento entre redes virtuais que existem em assinaturas diferentes, Olá assinaturas devem ser associados toohello mesmo Active Directory do Azure locatário. Se você ainda não tem um locatário do Azure Active Directory, você pode [criar um](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch) rapidamente. Se você precisar tooconnect virtual redes que foram criadas por meio do modelo de implantação clássico hello, ou que existem em diferentes regiões do Azure ou que existe nas assinaturas associadas toodifferent locatários de Active Directory do Azure, você pode usar um Azure [Gateway VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect Olá redes virtuais. 

Você pode usar o hello [portal do Azure](#portal), hello Azure [interface de linha de comando](#cli) (CLI), ou o Azure [PowerShell](#powershell) toocreate um emparelhamento de rede virtual. Clique em qualquer Olá anterior ferramenta links toogo diretamente toohello as etapas para criar uma rede virtual emparelhamento usando sua ferramenta de escolha.

## <a name="portal"></a>Criar emparelhamento – portal do Azure

Este tutorial usa contas diferentes para cada assinatura. Se você estiver usando uma conta que tenha permissões tooboth assinaturas, você pode usar o hello mesmo conta para todas as etapas, ignore as etapas de saudação para fazer logoff do portal de saudação e ignore as etapas de saudação para atribuição de redes virtuais do toohello permissões de outro usuário.

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
8. Em Olá **selecione** caixa, selecione um UserB ou digite toosearch de endereço de email do UserB para ele. Olá lista de usuários mostrado é de saudação mesmo locatário do Active Directory do Azure como rede virtual Olá estiver configurando Olá emparelhamento para.
9. Clique em **Salvar**.
10. Em Olá **myVnetA - controle de acesso (IAM)** folha, clique em **propriedades** da lista de vertical Olá opções Olá lado esquerdo da folha de saudação. Saudação de cópia **ID de recurso**, que é usado em uma etapa posterior. ID do recurso Olá é semelhante toohello exemplo a seguir: /subscriptions/<Subscription Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/virtualNetworks/myVnetA.
11. Faça logoff do portal de saudação como UserA e faça logon como UserB.
12. Conclua as etapas 2 e 3, digitar ou selecionar Olá valores na etapa 3 a seguir:

    - **Nome**: *myVnetB*
    - **Espaço de endereço**: *10.1.0.0/16*
    - **Nome da sub-rede**: *padrão*
    - **Intervalo de endereços da sub-rede**: *10.1.0.0/24*
    - **Assinatura:** selecione a assinatura B.
    - **Grupo de recursos**: selecione **Criar novo** e insira *myResourceGroupB*
    - **Localização**: *Leste dos EUA*

13. Em Olá **pesquisar recursos** caixa na parte superior de saudação do portal hello, tipo *myVnetB*. Clique em **myVnetB** quando ele aparece nos resultados da pesquisa hello. Uma folha é exibido para Olá **myVnetB** rede virtual.
14. Em Olá **myVnetB** folha que aparece, clique em **propriedades** da lista de vertical Olá opções Olá lado esquerdo da folha de saudação. Saudação de cópia **ID de recurso**, que é usado em uma etapa posterior. ID do recurso Olá é semelhante toohello exemplo a seguir: /subscriptions/<Susbscription ID>/resourceGroups/myResoureGroupB/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnetB.
15. Clique em **(IAM) do controle de acesso** em Olá **myVnetB** folha e conclua as etapas de 5 a 10 para myVnetB, inserindo **UserA** na etapa 8.
16. Faça logoff do portal de saudação como UserB e faça logon como UserA.
17. Em Olá **pesquisar recursos** caixa na parte superior de saudação do portal hello, tipo *myVnetA*. Clique em **myVnetA** quando ele aparece nos resultados da pesquisa hello. Uma folha é exibido para Olá **myVnet** rede virtual.
18. Clique em **myVnetA**.
19. Em Olá **myVnetA** folha que aparece, clique em **emparelhamentos** da lista de vertical Olá opções Olá lado esquerdo da folha de saudação.
20. Em Olá **myVnetA - emparelhamentos** folha que aparecer, clique em **+ adicionar**
21. Em Olá **adicionar emparelhamento** folha que aparece, digite, ou selecione Olá as opções a seguir e clique em **Okey**:
     - **Nome**: *myVnetAToMyVnetB*
     - **Modelo de implantação de rede virtual**: selecione **Resource Manager**.
     - **Sei minha ID do recurso**: marque essa caixa.
     - **ID do recurso**: insira a ID de recurso de saudação da etapa 14.
     - **Permitir acesso à rede virtual:** verifique se a opção **Habilitado** está selecionada.
    Nenhuma outra configuração é usada neste tutorial. ler toolearn sobre todas as configurações de emparelhamento, [gerenciar emparelhamentos de rede virtual](virtual-network-manage-peering.md#create-a-peering).
22. Depois de clicar em **Okey** na etapa anterior de saudação, Olá **adicionar emparelhamento** folha fecha e consulte Olá **myVnetA - emparelhamentos** folha novamente. Depois de alguns segundos, Olá emparelhamento que você criou aparece na folha de saudação. **Iniciada** está listado no hello **STATUS EMPARELHAMENTO** coluna Olá **myVnetAToMyVnetB** emparelhamento é criado. Você emparelhadas myVnetA toomyVnetB, mas agora myVnetB toomyVnetA deve ser par. Olá emparelhamento deve ser criado em ambas as direções tooenable recursos Olá toocommunicate de redes virtuais entre si.
23. Faça logoff do portal de saudação como UserA e faça logon como UserB.
24. Conclua as etapas 17 a 21 novamente para myVnetB. Na etapa 21, nome hello emparelhamento *myVnetBToMyVnetA*, selecione *myVnetA* para **rede Virtual**e insira a ID de saudação na etapa 10 da saudação **IDderecurso** caixa.
25. Alguns segundos depois de clicar em **Okey** toocreate Olá emparelhamento para myVnetB, hello **myVnetBToMyVnetA** emparelhamento você acabou de criar está listado com **conectado** em Olá  **STATUS de EMPARELHAMENTO** coluna.
26. Faça logoff do portal de saudação como UserB e faça logon como UserA.
27. Conclua as etapas 17 a 19 novamente. Olá **STATUS EMPARELHAMENTO** para Olá **myVnetAToVNetB** emparelhamento agora também está **conectado**. Olá emparelhamento é estabelecida com êxito depois de ver **conectado** em Olá **STATUS EMPARELHAMENTO** coluna para ambas as redes virtuais no emparelhamento via protocolo hello. Todos os recursos do Azure que criar a rede virtual agora estão capaz de toocommunicate entre si por meio de seus endereços IP. Se você estiver usando a resolução de nomes do Azure padrão para redes virtuais hello, Olá recursos em redes virtuais Olá não estão tooresolve capaz de nomes entre redes virtuais hello. Se você quiser tooresolve nomes entre redes virtuais em um emparelhamento, você deve criar seu próprio servidor DNS. Saiba como tooset backup [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
28. **Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.
29. **Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em Olá [excluir recursos](#delete-portal) deste artigo.

## <a name="cli"></a>Criar emparelhamento – CLI do Azure

Este tutorial usa contas diferentes para cada assinatura. Se você estiver usando uma conta que tenha permissões tooboth assinaturas, você pode usar o hello a mesma conta para todas as etapas, ignore as etapas de saudação para registro em log fora do Azure e remove linhas de saudação do script que crie atribuições de função de usuário. Substituir UserA@azure.com e UserB@azure.com em todos os Olá scripts com nomes de usuário de saudação que você está usando para UserA e UserB a seguir.

saudação de script a seguir:

- Requer Olá CLI do Azure versão 2.0.4 ou posterior. versão de hello toofind, execute `az --version`. Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Funciona em um shell do Bash. Para obter opções sobre a execução de scripts de CLI do Azure no cliente do Windows, consulte [em execução Olá CLI do Azure no Windows](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Em vez de instalar hello CLI e suas dependências, você pode usar o hello Shell de nuvem do Azure. Olá Shell de nuvem do Azure é um shell Bash livre que podem ser executados diretamente no hello portal do Azure. Ele tem Olá CLI do Azure pré-instalado e configurado toouse com sua conta. Clique em Olá **Experimente** botão no script hello segue, que invoca um Shell de nuvem que você pode fazer logon no tooyour conta do Azure com. 

1. Abra uma sessão CLI e faça logon tooAzure como UserA usando Olá `azure login` comando. conta Olá com que log deve ter Olá permissões necessárias toocreate um emparelhamento de rede virtual. Consulte Olá [permissões](#permissions) deste artigo para obter detalhes.
2. Copiar Olá editor de texto de tooa de script a seguir em seu computador, substitua `<SubscriptionA-Id>` com hello ID de assinaturaA, em seguida, Olá cópia modificado script, cole-o na sua sessão CLI e pressione `Enter`. Se você não souber a Id da assinatura, insira o comando de 'Mostrar de conta az' hello. Olá valor **id** Olá saída é sua ID de assinatura

    ```azurecli-interactive
    # Create a resource group.
    az group create \
      --name myResourceGroupA \
      --location eastus

    # Create virtual network A.
    az network vnet create \
      --name myVnetA \
      --resource-group myResourceGroupA \
      --location eastus \
      --address-prefix 10.0.0.0/16

    # Assign UserB permissions toovirtual network A.
    az role assignment create \
      --assignee UserB@azure.com \
      --role "Network Contributor" \
      --scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```
    
     atribuição de permissão Olá para UserB não é um requisito. Emparelhamento pode ser estabelecida mesmo se os usuários individualmente geram solicitações de emparelhamento para seus respectivos redes virtuais, como Olá solicitações de correspondência. Adicionar um usuário com privilégios de myVNetB como um colaborador de rede na rede virtual local de saudação torna mais fácil instalação de saudação toodo.
3. Faça logoff do Azure como UserA usando Olá `az logout` de comando, em seguida, faça logon no tooAzure como UserB. conta Olá com que log deve ter Olá permissões necessárias toocreate um emparelhamento de rede virtual. Consulte Olá [permissões](#permissions) deste artigo para obter detalhes.
4. Crie myVnetB. Copie o conteúdo do script hello no editor de texto etapa tooa 2 em seu computador. Substituir `<SubscriptionA-Id>` com ID de Assinaturab de saudação. Altere 10.0.0.0/16 too10.1.0.0/16, alterar como tooB e todos os tooA de Bs. Copie o script hello modificado, cole-o na sessão CLI tooyour e pressione `Enter`. 
5. Faça logoff do Azure como UserB e faça logon tooAzure como UserA.
6. Crie uma rede virtual emparelhamento de myVnetA toomyVnetB. Copie Olá editor de texto de tooa de conteúdo de script a seguir em seu computador. Substituir `<SubscriptionB-Id>` com ID de Assinaturab de saudação. script de saudação tooexecute, copie o script hello modificado, cole-o em sua sessão CLI e pressione Enter.
 
    ```azurecli-interactive
        # Get hello id for myVnetA.
        vnetAId=$(az network vnet show \
          --resource-group myResourceGroupA \
          --name myVnetA \
          --query id --out tsv)
    
        # Peer myVNetA toomyVNetB.
        az network vnet peering create \
          --name myVnetAToMyVnetB \
          --resource-group myResourceGroupA \
          --vnet-name myVnetA \
          --remote-vnet-id /subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/VirtualNetworks/myVnetB \
          --allow-vnet-access
    ```

7. Exibir o estado de emparelhamento de saudação do myVnetA.

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroupA \
      --vnet-name myVnetA \
      --output table
    ```

    estado de saudação é **iniciada**. Ele muda muito**conectado** depois de criar toomyVnetA emparelhamento de saudação do myVnetB.

8. Faça logoff UserA do Azure e faça logon no tooAzure como UserB.
9. Crie hello emparelhamento de myVnetB toomyVnetA. Copie o conteúdo do script hello no editor de texto etapa 6 tooa em seu computador. Substituir `<SubscriptionB-Id>` com ID de saudação do assinaturaA e alteração como tooB e todos os tooA de Bs. Depois que você fez alterações hello, Olá cópia modificado script, cole-o em sua sessão CLI e pressione `Enter`.
10. Exibir o estado de emparelhamento de saudação do myVnetB. Copie o conteúdo do script hello no editor de texto etapa 7 tooa em seu computador. Alterar um tooB para o grupo de recursos de saudação e nomes de rede virtual, copie o script hello, cole o script hello modificado na sessão CLI tooyour e, em seguida, pressione `Enter`. Olá estado emparelhamento é **conectado**. Olá emparelhamento estado das alterações myVnetA muito**conectado** depois que você criou o emparelhamento de saudação do myVnetB toomyVnetA. Você pode registrar UserA no tooAzure e concluir a etapa 7 novamente tooverify Olá emparelhamento estado da myVnetA. 

    > [!NOTE]
    > Olá emparelhamento não for estabelecida até que o estado de emparelhamento Olá é **conectado** para ambas as redes virtuais.

11. **Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.
12. **Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em [excluir recursos](#delete-cli) neste artigo.

Todos os recursos do Azure que criar a rede virtual agora estão capaz de toocommunicate entre si por meio de seus endereços IP. Se você estiver usando a resolução de nomes do Azure padrão para redes virtuais hello, Olá recursos em redes virtuais Olá não estão tooresolve capaz de nomes entre redes virtuais hello. Se você quiser tooresolve nomes entre redes virtuais em um emparelhamento, você deve criar seu próprio servidor DNS. Saiba como tooset backup [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
 
## <a name="powershell"></a>Criar emparelhamento – PowerShell

Este tutorial usa contas diferentes para cada assinatura. Se você estiver usando uma conta que tenha permissões tooboth assinaturas, você pode usar o hello a mesma conta para todas as etapas, ignore as etapas de saudação para registro em log fora do Azure e remove linhas de saudação do script que crie atribuições de função de usuário. Substituir UserA@azure.com e UserB@azure.com em todos os Olá scripts com nomes de usuário de saudação que você está usando para UserA e UserB a seguir.

1. Instale a versão mais recente Olá de saudação do PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) módulo. Se você for novo tooAzure PowerShell, consulte [visão geral do Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Inicie uma sessão do PowerShell.
3. No PowerShell, faça logon tooAzure como UserA inserindo Olá `login-azurermaccount` comando. conta Olá com que log deve ter Olá permissões necessárias toocreate um emparelhamento de rede virtual. Consulte Olá [permissões](#permissions) deste artigo para obter detalhes.
4. Crie um grupo de recursos e a rede virtual cópia de r. Olá depois do texto do script tooa editor em seu computador. Substituir `<SubscriptionA-Id>` com hello ID da assinaturaA. Se você não souber a Id da assinatura, digite Olá `Get-AzureRmSubscription` comando tooview-lo. Olá valor **Id** em Olá retornados a saída é a ID da assinatura. script de saudação tooexecute, Olá cópia modificado script, cole-o em tooPowerShell e pressione `Enter`.

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name MyResourceGroupA `
      -Location eastus

    # Create virtual network A.
    $vNetA = New-AzureRmVirtualNetwork `
      -ResourceGroupName MyResourceGroupA `
      -Name 'myVnetA' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus

    # Assign UserB permissions toomyVnetA.
    New-AzureRmRoleAssignment `
      -SignInName UserB@azure.com `
      -RoleDefinitionName "Network Contributor" `
      -Scope /subscriptions/<SubscriptionA-Id>/resourceGroups/myResourceGroupA/providers/Microsoft.Network/VirtualNetworks/myVnetA
    ```

    atribuição de permissão Olá para UserB não é um requisito. Emparelhamento pode ser estabelecida mesmo se os usuários individualmente geram solicitações de emparelhamento para seus respectivos redes virtuais, como Olá solicitações de correspondência. Adicionar um usuário com privilégios de saudação outra rede virtual como um usuário na rede virtual local de saudação torna mais fácil instalação de saudação toodo.
5. Faça logoff do Azure como UserA e faça logon como UserB. conta Olá com que log deve ter Olá permissões necessárias toocreate um emparelhamento de rede virtual. Consulte Olá [permissões](#permissions) deste artigo para obter detalhes.
6. Copie o conteúdo do script hello no editor de texto etapa 4 tooa em seu computador. Substituir `<SubscriptionA-Id>` com a ID de saudação para alteração de B. 10.0.0.0/16 too10.1.0.0/16 da assinatura. Alterar como tooB e todos os tooA de Bs. script de saudação tooexecute, Olá cópia modificado script, cole o PowerShell e pressione `Enter`.
7. Faça logoff do Azure como UserB e faça logon como UserA.
8. Crie hello emparelhamento de myVnetA toomyVnetB. Copie Olá editor de texto de tooa de script a seguir em seu computador. Substituir `<SubscriptionB-Id>` com hello ID de assinatura de script de saudação tooexecute b., copie o script hello modificado, cole tooPowerShell e pressione `Enter`.
 
    ```powershell
    # Peer myVnetA toomyVnetB.
    $vNetA=Get-AzureRmVirtualNetwork -Name myVnetA -ResourceGroupName myResourceGroupA
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnetAToMyVnetB' `
      -VirtualNetwork $vNetA `
      -RemoteVirtualNetworkId "/subscriptions/<SubscriptionB-Id>/resourceGroups/myResourceGroupB/providers/Microsoft.Network/virtualNetworks/myVnetB"
    ```

9. Exibir o estado de emparelhamento de saudação do myVnetA.

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroupA `
      -VirtualNetworkName myVnetA `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    estado de saudação é **iniciada**. Ele muda muito**conectado** depois de configurar o toomyVnetA emparelhamento de saudação do myVnetB.

10. Faça logoff do Azure como UserA e faça logon como UserB.
11. Crie hello emparelhamento de myVnetB toomyVnetA. Copie o conteúdo do script hello no editor de texto de 8 tooa etapa no seu PC. Substituir `<SubscriptionB-Id>` com hello ID de assinatura de um e alterar tooB r e tooA de todos os B. script de saudação tooexecute, Olá cópia modificado script, cole-o em tooPowerShell e pressione `Enter`.
12. Exibir o estado de emparelhamento de saudação do myVnetB. Copie o conteúdo do script hello no editor de texto etapa 9 tooa em seu computador. Altere um tooB para o grupo de recursos de saudação e nomes de rede virtual. script de saudação tooexecute, cole o script hello modificado no PowerShell e pressione `Enter`. estado de saudação é **conectado**. Olá estado emparelhamento de **myVnetA** muda muito**conectado** depois que você criou o emparelhamento de saudação do **myVnetB** muito**myVnetA**. Você pode registrar UserA no tooAzure e concluir a etapa 9 novamente tooverify Olá emparelhamento estado da myVnetA. 

    > [!NOTE]
    > Olá emparelhamento não for estabelecida até que o estado de emparelhamento Olá é **conectado** para ambas as redes virtuais.

    Todos os recursos do Azure que criar a rede virtual agora estão capaz de toocommunicate entre si por meio de seus endereços IP. Se você estiver usando a resolução de nomes do Azure padrão para redes virtuais hello, Olá recursos em redes virtuais Olá não estão tooresolve capaz de nomes entre redes virtuais hello. Se você quiser tooresolve nomes entre redes virtuais em um emparelhamento, você deve criar seu próprio servidor DNS. Saiba como tooset backup [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

13. **Opcional**: Embora a criação de máquinas virtuais não é abordada neste tutorial, você pode criar uma máquina virtual em cada rede virtual e conectar-se de uma máquina virtual toohello outras toovalidate conectividade.
14. **Opcional**: toodelete recursos Olá criados por você neste tutorial, Olá concluir as etapas em [excluir recursos](#delete-powershell) neste artigo.

## <a name="permissions"></a>Permissões

contas de saudação que usar toocreate um emparelhamento de rede virtual devem ter função necessário hello ou as permissões. Por exemplo, se foram emparelhamento duas redes virtuais denominadas **myVnetA** e **myVnetB**, sua conta deve ser atribuída Olá função mínimo ou as permissões para cada rede virtual a seguir:
    
|Rede virtual|Função|Permissões|
|---|---|---|
|myVnetA|[Colaborador de rede](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|myVnetB|[Colaborador de rede](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

Saiba mais sobre [funções internas](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) e atribuindo permissões específicas muito[funções personalizadas](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (somente no Gerenciador de recursos).

## <a name="delete"></a>Excluir recursos
Quando concluir este tutorial, você pode desejar que recursos de saudação toodelete criado no tutorial hello, portanto você não incorrer em encargos de uso. Excluir um grupo de recursos também exclui todos os recursos que estão no grupo de recursos de saudação.

### <a name="delete-portal"></a>Portal do Azure

1. Faça logon em toohello portal do Azure como UserA.
2. Na caixa de pesquisa do portal hello, insira **myResourceGroupA**. Nos resultados da pesquisa de saudação, clique em **myResourceGroupA**.
3. Em Olá **myResourceGroupA** folha, clique em Olá **excluir** ícone.
4. tooconfirm Olá exclusão, Olá **Olá tipo nome do grupo de recursos** , digite **myResourceGroupA**e, em seguida, clique em **excluir**.
5. Faça logoff do portal de saudação como UserA e faça logon como UserB.
6. Conclua as etapas 2 a 4 para myResourceGroupB.

### <a name="delete-cli"></a>Azure CLI

1. Faça logon no tooAzure como UserA e execute Olá comando a seguir:

    ```azurecli-interactive
    az group delete --name myResourceGroupA --yes
    ```
2. Faça logoff do Azure como UserA e faça logon como UserB.
3. Execute Olá comando a seguir:

    ```azurecli-interactive
    az group delete --name myResourceGroupB --yes
    ```

### <a name="delete-powershell"></a>PowerShell

1. Faça logon no tooAzure como UserA e execute Olá comando a seguir:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupA -force
    ```

2. Faça logoff do Azure como UserA e faça logon como UserB.
3. Execute Olá comando a seguir:

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroupB -force
    ```

## <a name="next-steps"></a>Próximas etapas

- Familiarize por completo com [comportamentos e restrições importantes do emparelhamento de rede virtual](virtual-network-manage-peering.md#requirements-and-constraints) antes de criar um emparelhamento de rede virtual para uso em produção.
- Saiba mais sobre todas as [configurações de emparelhamento de rede virtual](virtual-network-manage-peering.md#create-a-peering).
- Saiba como muito[criar um hub e spoke de topologia de rede](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) com o emparelhamento de rede virtual.
