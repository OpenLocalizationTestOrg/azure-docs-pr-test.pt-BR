---
title: aaaAdd, alterar ou excluir uma sub-rede de rede virtual do Azure | Microsoft Docs
description: Saiba como tooadd, alterar ou excluir uma sub-rede de rede virtual no Azure.
services: virtual-network
documentationcenter: na
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
ms.date: 05/10/2017
ms.author: jdial
ms.openlocfilehash: 0d6d813b7e2fc52a00a87f6c6714ab5b7ca589ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-delete-a-virtual-network-subnet"></a>Adicionar, alterar ou excluir uma sub-rede da rede virtual

Saiba como tooadd, alterar ou excluir uma sub-rede de rede virtual. 

Se você não estiver familiarizado com as redes virtuais, antes de adicionar, alterar ou excluir uma sub-rede recomendamos que você leia [Visão geral da rede virtual do Azure](virtual-networks-overview.md) e [Criar, alterar ou excluir uma rede virtual](virtual-network-manage-network.md). Todos os recursos do Azure implantados em uma rede virtual são implantados em uma sub-rede dentro de uma rede virtual. Normalmente, várias sub-redes são criadas dentro de uma rede virtual para:
- **Filtra o tráfego entre sub-redes**. Você pode aplicar rede segurança grupos toosubnets toofilter de entrada e saída tráfego de rede para todos os recursos (como máquinas virtuais) que estão na rede virtual hello. Saiba mais sobre toolearn como toocreate um grupo de segurança de rede, consulte [criar grupos de segurança de rede](virtual-networks-create-nsg-arm-pportal.md).
- **Controlar o roteamento entre sub-redes**. O Azure cria rotas padrão para que o tráfego seja roteado automaticamente entre sub-redes. Você pode substituir as rotas padrão do Azure, criando rotas definidas pelo usuário. toolearn mais informações sobre rotas definidas pelo usuário, consulte [criar rotas definidas pelo usuário](virtual-network-create-udr-arm-ps.md). 

Este artigo explica como tooadd, alterar e excluir uma sub-rede para redes virtuais que foram criados usando o modelo de implantação do Azure Resource Manager hello.
 
## <a name="before"></a>Antes de começar

Antes de iniciar tarefas Olá descritos neste artigo, conclua Olá pré-requisitos a seguir:

- Se você for novo tooworking com redes virtuais, recomendamos que você examine Olá exercício [criar sua primeira rede virtual do Azure](virtual-network-get-started-vnet-subnet.md). Esse exercício pode ajudá-lo a se familiarizar melhor com as redes virtuais.
- toolearn sobre os limites de redes virtuais, examine [limites do Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).
- Entre em toohello portal do Azure, hello Azure ferramenta de linha de comando (CLI do Azure) ou o PowerShell do Azure usando sua conta do Azure. Caso você não tenha uma conta do Azure, inscreva-se para obter uma [conta de avaliação gratuita](https://azure.microsoft.com/free).
- Se você planejar toouse comandos do PowerShell tarefas de saudação toocomplete descritas neste artigo, você deve primeiro [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que você tenha a versão mais recente de saudação do hello cmdlets do PowerShell do Azure instalado. tooget ajuda para comandos do PowerShell nos exemplos hello, digite `get-help <command> -full`.
- Se você planejar toouse que CLI do Azure comandos tarefas de saudação toocomplete descritas neste artigo, você deve:
    - [Instalar e configurar Olá CLI do Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que você tenha a versão mais recente de saudação da CLI do Azure instalado.
    - Use Olá Shell de nuvem do Azure. Em vez de instalar hello CLI e suas dependências, você pode usar o hello Shell de nuvem do Azure. Olá Shell de nuvem do Azure é um shell Bash livre que podem ser executados diretamente no hello portal do Azure. Ele tem Olá CLI do Azure pré-instalado e configurado toouse com sua conta. Olá toouse Shell de nuvem, clique em Olá nuvem Shell (**> _**) ícone na parte superior de saudação do hello portal do Azure. 

  tooget ajuda com comandos de CLI do Azure, digite `az <command> --help`.

## <a name="create-subnet"></a>Adicionar uma sub-rede

tooadd uma sub-rede:

1. Entrar toohello [portal](https://portal.azure.com) com uma conta que recebe permissões para a função de Colaborador de rede hello (no mínimo) para sua assinatura. toolearn mais sobre como atribuir tooaccounts funções e permissões, consulte [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Na caixa de pesquisa do portal hello, insira **redes virtuais**. Nos resultados da pesquisa de saudação, clique em **redes virtuais**.
3. Em Olá **redes virtuais** folha, clique em Olá deseja tooadd uma sub-rede para a rede virtual.
4. Na folha de rede virtual hello, clique em **sub-redes**.
5. Clique em **+Sub-rede**.
6. Em Olá **Adicionar sub-rede** folha, insira valores para Olá parâmetros a seguir:
    - **Nome**: nome de saudação deve ser exclusivo dentro da rede virtual hello.
    - **Intervalo de endereços**: intervalo de saudação deve ser exclusivo no espaço de endereço Olá para rede virtual hello. intervalo de saudação não pode sobrepor outros intervalos de endereços de sub-rede na rede virtual hello. espaço de endereço Olá deve ser especificado usando a notação de roteamento entre domínios (CIDR). Por exemplo, em uma rede virtual com espaço de endereçamento 10.0.0.0/16, você pode definir um espaço de endereçamento de sub-rede de 10.0.0.0/24. intervalo menor Hello, que você pode especificar é/de 29, que fornece oito endereços IP para a sub-rede de saudação. Reserva do Azure Olá primeiro e último endereço em cada sub-rede para conformidade de protocolo. Três endereços adicionais são reservados para uso pelo serviço do Azure. Como resultado, definindo uma sub-rede/29 resultados de intervalo em três endereços IP utilizáveis na sub-rede Olá de endereço. Se você planejar tooconnect um gateway VPN de tooa de rede virtual, você deve criar uma sub-rede do gateway. Saiba mais sobre [considerações de intervalo de endereços específico para sub-redes de gateway](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Você pode alterar o intervalo de endereços Olá depois sub-rede Olá é adicionado, sob condições específicas. toolearn como toochange um intervalo de endereços de sub-rede, consulte [alterar as configurações de sub-rede](#change-subnet) neste artigo.
    - **Grupo de segurança de rede**: opcionalmente, você pode associar um grupo de segurança de rede existente Olá sub-rede toocontrol tráfego de rede de entrada e saída filtragem para a sub-rede de saudação. Hello grupo de segurança de rede deve existir no hello mesma assinatura e local de rede virtual hello. Ela também deve ser criada usando o modelo de implantação do Gerenciador de recursos de saudação. Saiba mais sobre toolearn como toocreate um grupo de segurança de rede, consulte [grupos de segurança de rede](virtual-networks-create-nsg-arm-pportal.md).
    - **Tabela de rotas**: opcionalmente, você pode associar uma tabela de rota existente com tráfego de rede Olá sub-rede toocontrol tooother redes de roteamento. Hello tabela de rota deve existir no hello mesma assinatura e local de rede virtual hello. Ela também deve ser criada usando o modelo de implantação do Gerenciador de recursos de saudação. toolearn mais sobre como tabelas de rotas toocreate, consulte [rotas definidas pelo usuário](virtual-network-create-udr-arm-ps.md).
    - **Os usuários**: você pode controlar o acesso toohello sub-rede usando funções internas ou suas próprias funções personalizadas. toolearn mais sobre como atribuir funções e usuários tooaccess Olá subrede, consulte [usar função atribuição toomanage acesso tooyour Azure recursos](../active-directory/role-based-access-control-configure.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-access).
7. tooadd Olá sub-rede toohello rede virtual que você selecionou, clique em **Okey**.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI do Azure|[az network vnet subnet create](/cli/azure/network/vnet/subnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json), [Add-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet"></a>Alterar as configurações de sub-rede

Você pode alterar a sub-rede de tooa de acesso do usuário, tabelas de rotas e os grupos de segurança de rede por meio do gerenciamento de recursos que estão em uma sub-rede. toolearn sobre essas configurações, em [adicionar uma sub-rede](#create-subnet), consulte a etapa 6. Se desejar que o espaço de endereço de saudação toochange de uma sub-rede, primeiro você deve excluir todos os recursos que estão na sub-rede hello. etapas de saudação levar toodelete um recurso variam dependendo recurso hello. toolearn como toodelete recursos que estão em sub-redes, documentação de saudação de leitura para cada recurso de tipo que você deseja toodelete. intervalo de endereços toochange Olá para uma sub-rede:

1. Entrar toohello [portal](https://portal.azure.com) com uma conta que recebe permissões para a função de Colaborador de rede hello (no mínimo) para sua assinatura. toolearn mais sobre como atribuir tooaccounts funções e permissões, consulte [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Na caixa de pesquisa do portal hello, insira **redes virtuais**. Nos resultados da pesquisa de saudação, clique em **redes virtuais**.
3. Em Olá **redes virtuais** folha, clique em rede virtual de saudação do qual você deseja toochange um intervalo de endereços de sub-rede.
4. Clique em sub-rede de saudação do qual você deseja que o intervalo de endereços do toochange hello.
5. Na folha de sub-rede hello, em Olá **um intervalo de endereços** , digite o novo intervalo de endereços hello. intervalo de saudação deve ser exclusivo no espaço de endereço Olá para rede virtual hello. intervalo de saudação não pode sobrepor outros intervalos de endereços de sub-rede na rede virtual hello. espaço de endereço Olá deve ser especificado usando a notação CIDR. Por exemplo, em uma rede virtual com espaço de endereçamento 10.0.0.0/16, você pode definir um espaço de endereçamento de sub-rede de 10.0.0.0/24. intervalo menor Hello, que você pode especificar é/de 29, que fornece oito endereços IP para a sub-rede de saudação. Reserva do Azure Olá primeiro e último endereço em cada sub-rede para conformidade de protocolo. Três endereços adicionais são reservados para uso pelo serviço do Azure. Como resultado, uma sub-rede com um intervalo de endereços /29 tem três endereços IP utilizáveis. Se você planejar tooconnect um gateway VPN de tooa de rede virtual, você deve criar uma sub-rede do gateway. Saiba mais sobre [considerações de intervalo de endereços específico para sub-redes de gateway](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Você pode alterar o intervalo de endereços Olá depois sub-rede Olá é criado, sob condições específicas. toolearn como toochange um intervalo de endereços de sub-rede, consulte [alterar as configurações de sub-rede](#change-subnet) neste artigo.
6. Clique em **Salvar**.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI do Azure|[az network vnet subnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-subnet"></a>Excluir uma sub-rede

Você pode excluir uma sub-rede somente se não houver nenhum recurso na sub-rede hello. Se houver recursos na sub-rede hello, você deve excluir recursos Olá que estão na sub-rede Olá antes de excluir sub-rede hello. etapas de saudação levar toodelete um recurso variam dependendo recurso hello. toolearn como toodelete recursos que estão em sub-redes, documentação de saudação de leitura para cada recurso de tipo que você deseja toodelete. toodelete uma sub-rede:

1. Entrar toohello [portal](https://portal.azure.com) com uma conta que recebe permissões para a função de Colaborador de rede hello (no mínimo) para sua assinatura. toolearn mais sobre como atribuir tooaccounts funções e permissões, consulte [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Na caixa de pesquisa do portal hello, insira **redes virtuais**. Nos resultados da pesquisa de saudação, clique em **redes virtuais**.
3. Em Olá **redes virtuais** folha, clique em rede virtual hello, você deseja toodelete uma sub-rede do.
4. Em Olá virtual de rede folha, em **configurações**, clique em **sub-redes**.
5. Na lista de Olá de sub-redes que aparece na folha de sub-redes hello, sub-rede de saudação do botão direito do mouse que você deseja toodelete, clique em **excluir**e, em seguida, clique em **Sim** subrede toodelete hello.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI do Azure|[az network vnet delete](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/remove-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>Próximas etapas

toocreate uma máquina virtual em uma sub-rede, consulte [criar uma rede virtual e implantar VMs na sub-rede Olá](virtual-network-get-started-vnet-subnet.md#create-vms).
