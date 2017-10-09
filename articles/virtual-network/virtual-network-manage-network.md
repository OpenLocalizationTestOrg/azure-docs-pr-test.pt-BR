---
title: aaaCreate, alterar ou excluir uma rede virtual do Azure | Microsoft Docs
description: Saiba como toocreate, alterar ou excluir uma rede virtual no Azure.
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
ms.openlocfilehash: 7dfe6632753182eae2a13bb0327f03f75e03d057
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network"></a>Criar, alterar ou excluir uma rede virtual

Saiba como toocreate e excluir um configurações de alteração e de rede virtual, como servidores DNS e endereço IP espaços, para uma rede virtual existente.

Uma rede virtual é uma representação de sua própria rede na nuvem hello. Uma rede virtual é uma isolamento lógico de saudação nuvem do Azure que é dedicado tooyour assinatura do Azure. Para cada rede virtual que você cria, você pode:
- Escolha um tooassign de espaço de endereço. Um espaço de endereços consiste em um ou mais intervalos de endereços que são definidos usando a notação de roteamento entre domínios (CIDR), como 10.0.0.0/16.
- Escolha servidor de DNS fornecida pelo Azure toouse hello, ou usar seu próprio servidor DNS. Todos os recursos de rede virtual conectado toohello recebem esse nomes de tooresolve de servidores DNS na rede virtual hello.
- Segmento Olá rede virtual em sub-redes, cada qual com seu próprio intervalo de endereços, no espaço de endereço de saudação da rede virtual hello. toolearn como toocreate, alterar e excluir sub-redes, consulte [adicionar, alterar ou excluir sub-redes](virtual-network-manage-subnet.md).

Este artigo explica como toocreate, alterar e excluir redes virtuais usando o modelo de implantação do Azure Resource Manager hello.

## <a name="before"></a>Antes de começar

Antes de iniciar tarefas Olá descritos neste artigo, conclua Olá pré-requisitos a seguir:

- Se você for novo tooworking com redes virtuais, recomendamos que você examine Olá exercício [criar sua primeira rede virtual do Azure](virtual-network-get-started-vnet-subnet.md). Esse exercício pode ajudá-lo a se familiarizar melhor com as redes virtuais.
- toolearn sobre os limites de redes virtuais, examine [limites do Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).
- Entre em toohello portal do Azure, hello Azure ferramenta de linha de comando (CLI do Azure) ou o PowerShell do Azure usando sua conta do Azure. Caso você não tenha uma conta do Azure, inscreva-se para obter uma [conta de avaliação gratuita](https://azure.microsoft.com/free).
- Se você planejar toouse comandos do PowerShell tarefas de saudação toocomplete descritas neste artigo, você deve primeiro [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que você tenha a versão mais recente de saudação do hello cmdlets do PowerShell do Azure instalado. tooget ajuda para comandos do PowerShell nos exemplos hello, digite `get-help <command> -full`.
- Se você planejar toouse CLI do Azure comandos tarefas de saudação toocomplete descritas neste artigo, você deve primeiro [instalar e configurar a CLI do Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que você tenha a versão mais recente de saudação da CLI do Azure instalado. tooget ajuda com comandos de CLI do Azure, digite `az <command> --help`.


## <a name="create-vnet"></a>Criar uma rede virtual

toocreate uma rede virtual:

1. Entrar toohello [portal](https://portal.azure.com) com uma conta que recebe permissões para a função de Colaborador de rede hello (no mínimo) para sua assinatura. toolearn mais sobre como atribuir tooaccounts funções e permissões, consulte [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Clique em **Nova** > **Rede** > **Rede Virtual**.
3. Em Olá **rede Virtual** folha em Olá **selecionar um modelo de implantação** caixa, deixe **Gerenciador de recursos de** selecionado e, em seguida, clique em **criar**.
4. Em Olá **criar rede virtual** folha, digite ou selecione os valores para Olá configurações a seguir e clique em **criar**:
    - **Nome**: nome hello deve ser exclusivo no hello [grupo de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) que você selecione a rede virtual do toocreate Olá no. Você não pode alterar o nome de saudação após a criação da rede virtual hello. Você pode criar várias redes virtuais ao longo do tempo. Para sugestões de nomenclaturas, consulte [Convenções de nomenclatura](/azure/architecture/best-practices/naming-conventions.md?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions). Uma convenção de nomenclatura a seguir pode ajudar a tornar mais fácil toomanage várias redes virtuais.
    - **Espaço de endereço**: especifique o espaço de endereço de saudação na notação CIDR. espaço de endereço Olá que definir pode ser público ou privado (RFC 1918). Se você definir o espaço de endereço hello como público ou privado, o espaço de endereço de saudação é só pode ser acessado na rede virtual hello, de redes virtuais interconectadas e de quaisquer redes locais que você se conectou a rede virtual toohello. Não é possível adicionar Olá espaços de endereço a seguir:
        - 224.0.0.0/4 (Multicast)
        - 255.255.255.255/32 (Broadcast)
        - 127.0.0.0/8 (Loopback)
        - 169.254.0.0/16 (Link-local)
        - 168.63.129.16/32 (DNS interno)

      Embora seja possível definir apenas um espaço de endereço quando você criar rede virtual hello, você pode adicionar mais espaços de endereço após a criação da rede virtual hello. toolearn como um endereço de tooadd espaço tooan de rede virtual existente, consulte [adicionar ou remover um espaço de endereço](#add-address-spaces) neste artigo.

      >[!WARNING]
      >Se uma rede virtual tiver espaços de endereço sobrepõem a outra rede local ou de rede virtual, redes Olá dois não podem ser conectados. Antes de definir um espaço de endereço, considere se convém tooconnect Olá rede virtual tooother as redes virtuais ou redes locais no hello futuras.
      >
      >

    - **Nome da sub-rede**: nome da sub-rede Olá deve ser exclusivo dentro da rede virtual hello. Você não pode alterar o nome da sub-rede Olá depois Olá sub-rede é criada. portal de saudação requer que você defina uma sub-rede quando você criar uma rede virtual, mesmo que uma rede virtual não é necessário toohave todas as sub-redes. No portal de saudação, você pode definir somente uma sub-rede quando você criar uma rede virtual. Você pode adicionar mais rede virtual toohello de sub-redes mais tarde, após a criação da rede virtual hello. tooadd uma rede virtual do tooa de sub-rede, consulte [criar uma sub-rede](virtual-network-manage-subnet.md#create-subnet) na [criar, alterar ou excluir sub-redes](virtual-network-manage-subnet.md). Você pode criar uma rede virtual que tem várias sub-redes usando a CLI do Azure ou o PowerShell.

      >[!TIP]
      >Às vezes, administradores criam sub-redes toofilter ou controle de tráfego roteamento entre sub-redes hello. Antes de definir sub-redes, considere como você pode desejar toofilter e rotear o tráfego entre suas sub-redes. toolearn mais sobre como filtrar o tráfego entre sub-redes, consulte [grupos de segurança de rede](virtual-networks-nsg.md). O Azure faz o roteamento de tráfego entre as sub-redes automaticamente, mas você pode substituir as rotas padrão do Azure. toolearn como toooverride do Azure padrão de roteamento de tráfego de sub-rede, consulte [rotas definidas pelo usuário](virtual-networks-udr-overview.md).
      >

    - **Intervalo de endereços de sub-rede**: intervalo de saudação deve estar no espaço de endereço Olá inserido para a rede virtual hello. intervalo menor Hello, que você pode especificar é/de 29, que fornece oito endereços IP para a sub-rede de saudação. Reserva do Azure Olá primeiro e último endereço em cada sub-rede para conformidade de protocolo. Três endereços adicionais são reservados para uso pelo serviço do Azure. Como resultado, uma rede virtual com um intervalo de endereços de sub-rede de /29 tem apenas três endereços IP utilizáveis. Se você planejar tooconnect um gateway VPN de tooa de rede virtual, você deve criar uma sub-rede do gateway. Saiba mais sobre [considerações de intervalo de endereços específico para sub-redes de gateway](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Você pode alterar o intervalo de endereços Olá depois sub-rede Olá é criado, sob condições específicas. toolearn como toochange um intervalo de endereços de sub-rede, consulte [alterar as configurações de sub-rede](#change-subnet) na [adicionar, alterar ou excluir sub-redes](virtual-network-manage-subnet.md).
    - **Assinatura:** Selecione uma [assinatura](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription). Você não pode usar o hello mesma rede virtual em mais de uma assinatura do Azure. No entanto, você pode conectar uma rede virtual em uma assinatura toovirtual redes outras assinaturas. tooconnect de redes virtuais em assinaturas diferentes, use o Gateway de VPN do Azure ou o emparelhamento de rede virtual. Qualquer recurso do Azure que você se conectar a rede virtual toohello deve estar no hello mesma assinatura que a rede virtual hello.
    - **Grupo de recursos**: Selecione um [grupo de recursos](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups) existente ou crie um novo. Um recurso do Azure que você se conectar a rede virtual toohello pode estar em Olá mesmo grupo de recursos, como rede virtual hello ou em outro grupo de recursos.
    - **Local:** Selecione um [local](https://azure.microsoft.com/regions/) do Azure, também conhecido como região. Uma rede virtual pode estar em um só local do Azure. No entanto, você pode conectar uma rede virtual em uma localização tooa rede virtual em outro local usando um gateway VPN. Qualquer recurso do Azure que você se conectar a rede virtual toohello deve estar no hello mesmo local da rede virtual hello.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI do Azure|[az network vnet create](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name = "view-vnet"></a>Exibir configurações e redes virtuais

redes virtuais tooview e configurações:

1. Entrar toohello [portal](https://portal.azure.com) com uma conta que recebe permissões para a função de Colaborador de rede hello (no mínimo) para sua assinatura. toolearn mais sobre como atribuir tooaccounts funções e permissões, consulte [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Na caixa de pesquisa do portal hello, insira **redes virtuais**. Nos resultados da pesquisa de saudação, clique em **redes virtuais**.
3. Em Olá **redes virtuais** folha, clique em Olá a rede virtual que você deseja que as configurações de tooview para.
4. Olá configurações a seguir são listadas na folha de saudação para rede virtual de saudação selecionado:
    - **Visão geral**: fornece informações sobre a rede virtual do hello, incluindo o espaço de endereço e servidores DNS. Olá, seguinte captura de tela mostra as configurações de visão geral de saudação para uma rede virtual denominado **MyVNet**:

        ![Visão geral da interface de rede](./media/virtual-network-manage-network/vnet-overview.png)

      Em Olá **visão geral** folha, você pode mover um rede virtual tooa diferente assinatura ou grupo de recursos. toolearn como toomove uma rede virtual, consulte [mover recursos tooa outro grupo de recursos ou assinatura](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json). artigo Olá lista os pré-requisitos e como os recursos de toomove usando Olá portal do Azure, o PowerShell e a CLI do Azure. Movem todos os recursos de rede virtual conectado toohello com a rede virtual hello.
    - **Espaço de endereço**: espaços de endereço de saudação que são atribuídos a rede virtual toohello são listados. toolearn como tooadd e remover um espaço de endereço, concluir Olá etapas [adicionar ou remover um espaço de endereço](#address-spaces) neste artigo.
    - **Dispositivos conectados**: todos os recursos que são de rede virtual conectado toohello são listados. Em Olá anterior a captura de tela, três interfaces de rede e um balanceador de carga são rede virtual toohello conectado. Os novos recursos que você cria e conectar-se a rede virtual toohello são listados. Se você excluir um recurso que foi a rede virtual toohello conectado, não aparece mais na lista de saudação.
    - **Subredes**: é mostrada uma lista de sub-redes que existem na rede virtual hello. toolearn como tooadd e remover uma sub-rede, consulte [criar uma sub-rede](virtual-network-manage-subnet.md#create-subnet) e [excluir uma sub-rede](virtual-network-manage-subnet.md#delete-subnet) na [adicionar, alterar ou excluir sub-redes](virtual-network-manage-subnet.md).
    - **Servidores DNS**: você pode especificar se hello Azure interno do servidor DNS ou um servidor DNS personalizado fornece resolução de nomes de dispositivos de rede virtual toohello conectado. Quando você cria uma rede virtual usando Olá portal do Azure, os servidores DNS do Azure são usados para resolução de nomes em uma rede virtual, por padrão. toomodify servidores DNS Olá, Olá concluir as etapas em [adicionar, alterar ou remover um servidor DNS](#dns-servers) neste artigo.
    - **Emparelhamentos**: se houver emparelhamentos existentes na assinatura hello, eles estão listados aqui. Você pode exibir configurações para emparelhamentos existentes, ou criar, alterar ou excluir emparelhamentos. toolearn mais sobre emparelhamentos, consulte [emparelhamento de rede Virtual](virtual-network-peering-overview.md).
    - **Propriedades**: exibe as configurações de sobre Olá rede virtual, incluindo a ID do recurso da rede virtual hello e Olá assinatura do Azure é no.
    - **Diagrama de**: diagrama Olá fornece uma representação visual de todos os dispositivos de rede virtual toohello conectado. diagrama de saudação tem algumas informações importantes sobre dispositivos de saudação. toomanage um dispositivo nesta exibição, no diagrama de saudação, clique em dispositivo hello.
    - **Configurações comuns do Azure**: toolearn mais sobre configurações comuns do Azure, consulte Olá informações a seguir:
        *   [Log de atividade](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs)
        *   [Controle de acesso (IAM)](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control)
        *   [Marcas](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags)
        *   [Bloqueios](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
        *   [Script de automação](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group)

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI do Azure|[az network vnet show](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork/?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="add-address-spaces"></a>Adicionar ou remover um espaço de endereço

Você pode adicionar e remover espaços de endereço para uma rede virtual. Um espaço de endereço deve ser especificado na notação CIDR e não pode sobrepor com outros espaços de endereço em Olá mesma rede virtual. espaços de endereço Olá que definir podem ser público ou privado (RFC 1918). Se você definir o espaço de endereço hello como público ou privado, o espaço de endereço de saudação é só pode ser acessado na rede virtual hello, de redes virtuais interconectadas e de quaisquer redes locais que você se conectou a rede virtual toohello. Não é possível adicionar Olá espaços de endereço a seguir:

- 224.0.0.0/4 (Multicast)
- 255.255.255.255/32 (Broadcast)
- 127.0.0.0/8 (Loopback)
- 169.254.0.0/16 (Link-local)
- 168.63.129.16/32 (DNS interno)

tooadd ou remover um espaço de endereço:

1. Entrar toohello [portal](https://portal.azure.com) com uma conta que recebe permissões para a função de Colaborador de rede hello (no mínimo) para sua assinatura. toolearn mais sobre como atribuir tooaccounts funções e permissões, consulte [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Na caixa de pesquisa do portal hello, insira **redes virtuais**. Nos resultados da pesquisa hello, selecione **redes virtuais**.
3. Em Olá **redes virtuais** folha, clique em Olá a rede virtual para o qual você deseja tooadd ou remover um espaço de endereço.
4. Em Olá virtual de rede folha, em **configurações**, clique em **espaço de endereço**.
5. Na folha de Olá Olá espaço de endereço, siga um destes Olá as opções a seguir:
    - **Adicionar um espaço de endereço**: insira o novo espaço de endereço hello. espaço de endereço de saudação não pode sobrepor um espaço de endereço existente que está definido para a rede virtual hello.
    - **Remover um espaço de endereço:** Clique com o botão direito em um espaço de endereço, em seguida clique em **Remover**. Se existir uma sub-rede no espaço de endereço Olá, você não pode remover o espaço de endereço de saudação. tooremove um espaço de endereço, você deve primeiro excluir todas as sub-redes (e todos os recursos que são conectados toohello sub-redes) que existe no espaço de endereço de saudação.
6. Clique em **Salvar**.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI do Azure|Somente Resource Manager|[az network vnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="dns-servers"></a>Adicionar, alterar ou remover um servidor DNS

Registram todas as VMs que são a rede virtual conectado toohello com servidores DNS Olá que você especificar para a rede virtual hello. Eles também usam Olá especificado o servidor DNS para resolução de nome. Cada NIC (interface de rede) em uma VM pode ter suas próprias configurações do servidor DNS. Se uma NIC tem suas próprias configurações de servidor DNS, elas substituirão as configurações do servidor DNS Olá para rede virtual hello. toolearn mais sobre as configurações de NIC DNS, consulte [interface tarefas e configurações de rede](virtual-network-network-interface.md#change-dns-servers). toolearn mais informações sobre resolução de nomes para VMs e instâncias de função nos serviços de nuvem do Azure, consulte [resolução de nomes para VMs e instâncias de função](virtual-networks-name-resolution-for-vms-and-role-instances.md). tooadd, alterar ou remover um servidor DNS:

1. Entrar toohello [portal](https://portal.azure.com) com uma conta que recebe permissões para a função de Colaborador de rede hello (no mínimo) para sua assinatura. toolearn mais sobre como atribuir tooaccounts funções e permissões, consulte [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Na caixa de pesquisa do portal hello, digite **redes virtuais**. Nos resultados da pesquisa hello, selecione **redes virtuais**.
3. Em Olá **redes virtuais** folha, clique em Olá desejar toochange as configurações de DNS para a rede virtual.
4. Em Olá virtual de rede folha, em **configurações**, clique em **servidores DNS**.
5. Selecione uma saudação opções na folha de saudação que lista os servidores DNS a seguir:
    - **Padrão (fornecida pelo Azure)**: todos os nomes de recurso e endereços IP privados são automaticamente registrados toohello servidores de DNS do Azure. Você pode resolver nomes entre todos os recursos que são conectado toohello mesma rede virtual. Você não pode usar nomes de tooresolve essa opção entre redes virtuais. nomes de tooresolve entre redes virtuais, você deve usar um servidor DNS personalizado.
    - **Personalizar**: você pode adicionar um ou mais servidores, backup toohello Azure limite para uma rede virtual. toolearn mais sobre os limites do servidor DNS, consulte [limites do Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#virtual-networking-limits-classic). Você tem Olá as opções a seguir:
        - **Adicionar um endereço**: adiciona a lista de servidores DNS Olá server tooyour rede virtual. Essa opção também registra o servidor DNS Olá com o Azure. Se você já tiver registrado um servidor DNS com o Azure, você pode selecionar o servidor DNS na lista de saudação.
        - **Remover um endereço**: clique em próximo servidor toohello que você deseja tooremove, **X**. Excluindo servidor de saudação remove server Olá apenas essa lista de rede virtual. servidor DNS Olá permanece registrado no Azure para seu outros toouse redes virtuais.
        - **Reordenar os endereços de servidor DNS**: é importante tooverify que lista os servidores DNS em Olá corrigir ordem para seu ambiente. Listas de servidores DNS são usadas na ordem de saudação que foram especificados. Eles não funcionam como uma configuração de round-robin. Se o primeiro servidor DNS Olá na lista de saudação pode ser alcançado, o cliente de Olá usa esse servidor DNS, independentemente se o servidor DNS hello está funcionando corretamente. Remova todos os servidores DNS Olá listados e, em seguida, adicioná-los na ordem de saudação que você deseja.
        - **Alterar um endereço**: servidor DNS Olá na lista de saudação de realce e, em seguida, digite Olá novo nome.
6. Clique em **Salvar**.
7. Reinicie Olá VMs que estão conectados toohello rede virtual, para que eles recebem novas configurações de servidor DNS hello. VMs continuam toouse suas configurações de DNS atuais até que sejam reiniciados.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI do Azure|[az network vnet update](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="delete-vnet"></a>Excluir uma rede virtual

Você pode excluir uma rede virtual somente se não houver nenhum tooit conectado de recursos. Se houver recursos tooany conectado sub-rede na rede virtual hello, exclua primeiro recursos Olá sub-redes tooall conectado em rede virtual hello. etapas de saudação levar toodelete um recurso variam dependendo recurso hello. toolearn como ler recursos toodelete toosubnets conectado, Olá documentação para cada tipo de recurso que você deseja toodelete. toodelete uma rede virtual:

1. Entrar toohello [portal](https://portal.azure.com) com uma conta que é atribuídas (no mínimo) permissões para a função de Colaborador de rede Olá para sua assinatura. toolearn mais sobre como atribuir tooaccounts funções e permissões, consulte [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Na caixa de pesquisa do portal hello, insira **redes virtuais**. Nos resultados da pesquisa de saudação, clique em **redes virtuais**.
3. Em Olá **redes virtuais** folha, você deseja toodelete de rede virtual do hello select.
4. Na folha de rede virtual hello, tooconfirm que não há nenhum dispositivo conectado toohello de rede virtual, em **configurações**, clique em **dispositivos conectados**. Se não houver dispositivos conectados, você deve excluí-los antes de excluir a rede virtual hello. Se não houver dispositivos conectados, clique em **Visão geral**.
5. Na parte superior de saudação da folha de saudação, clique em Olá **excluir** ícone.
6. exclusão de saudação tooconfirm da rede virtual de saudação, clique em **Sim**.


**Comandos**

|Ferramenta|Command|
|---|---|
|CLI do Azure|[azure network vnet delete](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetwork](/powershell/module/azurerm.network/remove-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="next-steps"></a>Próximas etapas

- toocreate uma máquina virtual e, em seguida, conecte-a rede virtual tooa, consulte [criar uma rede virtual e se conectar a máquinas virtuais](virtual-network-get-started-vnet-subnet.md#create-vms).
- toofilter o tráfego de rede entre as sub-redes em uma rede virtual, consulte [criar grupos de segurança de rede](virtual-networks-create-nsg-arm-pportal.md).
- toopeer uma rede virtual do tooanother de rede virtual, consulte [criar uma rede virtual emparelhamento](virtual-network-create-peering.md#portal).
- toolearn sobre opções de conexão de rede de local de tooan uma rede virtual, consulte [sobre o Gateway de VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams).
