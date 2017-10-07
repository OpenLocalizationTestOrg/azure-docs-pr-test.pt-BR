---
title: "Remover aaaAdd tooor de interfaces de rede de máquinas virtuais do Azure | Microsoft Docs"
description: "Saiba como o tooor de interfaces de rede tooadd remover interfaces de rede de máquinas virtuais."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2017
ms.author: jdial
ms.openlocfilehash: eb564b94932b9242f29bc23234b08b0c76ac23a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-network-interfaces-tooor-remove-from-virtual-machines"></a>Adicione a interfaces de rede tooor remover das máquinas virtuais

Saiba como tooadd uma rede existente ao criar uma VM da interface ou adicionar ou remover interfaces de rede de uma VM existente em Olá parado (desalocado) estado. Uma interface de rede permite toocommunicate uma máquina Virtual (VM) do Azure com a Internet, Azure e recursos locais. Uma VM pode ter um ou mais adaptadores de rede. 

Se você precisar tooadd, alterar ou remover endereços IP para uma interface de rede, leia Olá [gerenciar endereços IP de interface de rede](virtual-network-network-interface-addresses.md) artigo. Se você precisar toocreate, alterar ou excluir as interfaces de rede, leia Olá [gerenciar interfaces de rede](virtual-network-network-interface.md) artigo.

## <a name="before"></a>Antes de começar

Olá concluir tarefas a seguir antes de concluir qualquer etapas em qualquer seção deste artigo:

- Saber sobre as interfaces de rede quantas cada tamanho de VM de Windows e Linux suporte para revisando Olá [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigos de tamanhos de VM.
- Faça logon no toohello Azure [portal](https://portal.azure.com), interface de linha de comando (CLI) do Azure, ou o PowerShell do Azure com uma conta do Azure. Caso ainda não tenha uma conta do Azure, inscreva-se para obter uma [conta de avaliação gratuita](https://azure.microsoft.com/free).
- Se usar o PowerShell comandos toocomplete tarefas neste artigo, [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que você tem a versão mais recente de saudação do hello commandlets do PowerShell do Azure instalados. tooget ajuda para comandos do PowerShell, com exemplos, digite `get-help <command> -full`.
- Se usar a interface de linha de comando (CLI) do Azure comandos toocomplete tarefas neste artigo, [instalar e configurar Olá CLI do Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que você tem a versão mais recente de saudação do hello CLI do Azure instalado. tooget ajuda para comandos CLI, digite `az <command> --help`. Em vez de instalar Olá CLI e seus pré-requisitos, você pode usar o hello Shell de nuvem do Azure. Olá Shell de nuvem do Azure é um shell Bash livre que podem ser executados diretamente no hello portal do Azure. Ele tem Olá CLI do Azure pré-instalado e configurado toouse com sua conta. Olá toouse Shell de nuvem, clique em Olá nuvem Shell **> _** botão na parte superior de saudação do hello [portal](https://portal.azure.com).

## <a name="about"></a>Sobre adaptadores de rede e VMs

Você pode adicionar (anexar) um existente tooa de interface de rede VM ao criar hello VM, desde a interface de rede de saudação não está atualmente anexado tooanother VM. Você pode adicionar uma interface de rede para, ou remova (desconectar) uma interface de rede de toofrom uma VM existente, desde Olá VM está em Olá estado de parado (desalocado). Se você criar uma VM usando Olá portal do Azure, o portal de saudação cria uma interface de rede para você com as configurações padrão. portal de saudação não permite a você:

- Especifique um tooadd de interface de rede existentes ao criar hello VM
- Criar uma VM com várias interfaces de rede
- Especifique um nome para a interface de rede da saudação (portal Olá cria interface de rede Olá com um nome padrão)

Você pode usar o Azure PowerShell ou CLI de saudação toocreate uma interface de rede ou VM com todos os atributos de saudação anterior que você não pode usar o portal de saudação do. Antes de concluir tarefas Olá Olá seções a seguir, considere o seguinte Olá restrições e comportamentos:

- Todos os tamanhos VM dão suporte a pelo menos dois adaptadores de rede, mas alguns tamanhos de VM dão suporte a mais de dois adaptadores de rede. Olá após alguns VM tamanhos suporte uma interface de rede. toolearn quantas interfaces de rede oferece suporte a cada tamanho VM, ler Olá [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigos de tamanhos de VM. 
- No hello anterior, interfaces de rede só podem ser tooVMs adicionado suporte para várias interfaces de rede e foram criados com pelo menos duas interfaces de rede. Você não pôde adicionar um tooa de interface de rede VM que foi criado com uma interface de rede, mesmo se Olá tamanho da VM com suporte a várias interfaces de rede. Por outro lado, você pode remover apenas interfaces de rede de uma VM com pelo menos três interfaces de rede, como máquinas virtuais criadas pelo menos duas interfaces de rede sempre tinham toohave pelo menos duas interfaces de rede. Nenhuma dessas restrições se aplicam mais. Agora você pode criar uma VM com qualquer número de interfaces de rede (o número de toohello com suporte pelo tamanho da VM de saudação) e adicionar ou remover qualquer número de interfaces de rede (a partir do estado de VMs em Olá parado (desalocados)), como Olá VM sempre tem pelo menos uma interface de rede.
- Por padrão, a primeira interface de rede Olá em uma VM é definido como Olá *primário* interface de rede. Todas as outras interfaces de rede Olá VM são *secundário* interfaces de rede.
- Interfaces de rede principal são atribuídos a um gateway padrão pelos servidores de DHCP do Azure hello, mas as interfaces de rede secundárias não são. Uma vez que os adaptadores de rede secundários não são atribuídos a um gateway padrão, eles não conseguem se comunicar com recursos fora da sub-rede por padrão. interfaces de rede secundárias tooenable no toocommunicate máquina virtual do Windows com recursos de fora da sua sub-rede, adicionar sistema operacional que rotas toohello usando Olá `route add` comando de uma linha de comando do Windows. Para VMs do Linux, como o comportamento padrão de saudação usa host fraco roteamento, é recomendável restringir o tráfego de rede secundária interfaces tooa única sub-rede. Se você precisar conectividade fora da sub-rede Olá para interfaces de rede secundárias e habilitar roteamento tooensure que entram com base na política e o tráfego de saída usa Olá interface mesmo de rede.
- Por padrão, todo o tráfego de saída de saudação enviada VM de endereço IP de saudação atribuído a configuração de IP primário toohello Olá principal da interface de rede. Você controla qual endereço IP é usado para tráfego de saída no sistema operacional da VM hello, mas por padrão, é por meio da interface de rede primária hello.
- Olá após todas as VMs em hello mesmo conjunto de disponibilidade eram necessário toohave interfaces de rede de uma único ou vários. VMs com qualquer número de rede interfaces agora podem existir em Olá mesmo conjunto de disponibilidade, toohello número suportado pelo Olá tamanho da VM. Você só pode adicionar uma disponibilidade de tooan VM definida quando ele é criado embora. toolearn mais informações sobre conjuntos de disponibilidade, ler Olá [gerenciar a disponibilidade de saudação de VMs no Azure](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-network%2ftoc.json#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy) artigo.
- Enquanto as interfaces de rede em hello mesma VM pode ser conectado toodifferent sub-redes dentro de uma rede virtual, todas as interfaces de rede Olá devem ser conectado toohello mesma rede virtual.
- Você pode adicionar qualquer endereço IP para qualquer configuração de IP de qualquer pool de tooan back-end do balanceador de carga do Azure de interface de rede primária ou secundária. Olá anterior, apenas Olá endereço IP primário para a interface de rede primária Olá pôde ser adicionado tooa pool de back-end. toolearn mais informações sobre endereços IP e configurações, ler Olá [adicionar, alterar ou remover endereços IP](virtual-network-network-interface-addresses.md) artigo.
- Excluir uma máquina virtual não exclui as interfaces de rede de saudação que estão anexado tooit. Quando uma máquina virtual é excluída, as interfaces de rede de saudação são desanexadas do hello VM. Você pode adicionar toodifferent de interfaces de rede Olá máquinas virtuais ou excluí-los.
- Se uma interface de rede tiver um tooit de endereço atribuído IPv6 privada, você pode anexá-lo tooa VM ao criar hello VM. Você não pode anexar a uma interface de rede com um tooa de endereço de IPv6 atribuído VM depois Olá VM é criada. Se você anexar uma interface de rede com um endereço IPv6 privada atribuído durante a criação de uma máquina virtual, você apenas pode anexar rede interface toohello máquina virtual, independentemente de quantas interfaces de rede oferece suporte ao tamanho da VM hello. Consulte [endereços IP da interface de rede](virtual-network-network-interface-addresses.md) toolearn mais sobre a atribuição de IP endereços toonetwork interfaces.

## <a name="vm-create"></a>Adicionar tooa de interfaces de rede existente nova VM

Quando você cria uma máquina virtual por meio do portal hello, portal Olá cria uma interface de rede com as configurações padrão e anexa toohello VM para você. Não é possível adicionar tooa de interfaces de rede existente nova VM, ou crie uma VM com várias interfaces de rede usando Olá portal do Azure. Você pode usar ambas usando Olá CLI ou o PowerShell. Você pode adicionar como muitas interfaces tooa VM de rede como Olá criar dá suporte ao tamanho da VM. toolearn mais sobre a rede quantas interfaces cada suporta de tamanho VM, ler Olá [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigos de tamanhos de VM. interfaces de rede Olá adicionar tooa VM atualmente não podem ser anexado tooanother VM. mais sobre a criação de interfaces de rede, leia a saudação de toolearn [gerenciar interfaces de rede](virtual-network-network-interface.md#create-a-network-interface) artigo.

> [!WARNING]
> Se uma interface de rede tem um endereço IPv6 privado atribuído tooit, máquina virtual do hello rede interface toohello só pode adicionar ao criar a máquina virtual de saudação. Você pode anexar mais de uma máquina virtual interface toohello de rede quando você criar a máquina virtual de saudação ou após Olá a máquina virtual é criada, como um endereço IPv6 é atribuído a máquina virtual do tooa rede interface anexado tooa. Consulte [endereços IP da interface de rede](virtual-network-network-interface-addresses.md) toolearn mais sobre a atribuição de IP endereços toonetwork interfaces.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI|[az vm create](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-add-nic"></a>Adicionar um existente tooan de interface de rede existente de VM

Você pode adicionar muitas rede interfaces tooa VM como Olá tamanho da VM está adicionando toosupports de interfaces de rede. toolearn quantas interfaces de rede oferece suporte a cada tamanho VM, ler Olá [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigos de tamanhos de VM. Olá VM que você deseja tooadd um toomust de interface de rede oferecem suporte a número de saudação das interfaces de rede, você deseja tooadd e deve estar no hello interrompido (desalocado) estado. interfaces de rede Olá deseja tooadd atualmente não podem ser anexado tooanother VM. Não é possível adicionar tooan de interfaces de rede existente a VM usando Olá portal do Azure. interfaces de rede de tooadd tooan existente VM, você deve usar o hello CLI ou o PowerShell. 

> [!WARNING]
> Se uma interface de rede tem um endereço IPv6 privado atribuído tooit, ele não pode ser adicionado tooan máquina de virtual existente. Você só pode adicionar uma interface de rede com uma atribuído privada IPv6 endereço tooa máquina virtual quando você cria uma máquina virtual. Consulte [endereços IP da interface de rede](virtual-network-network-interface-addresses.md) toolearn mais sobre a atribuição de IP endereços toonetwork interfaces.

|Ferramenta|Command|
|---|---|
|CLI|[az vm nic add](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#add) (referência) ou [etapas detalhadas](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-a-vm)|
|PowerShell|[Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (referência) ou [etapas detalhadas](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-an-existing-vm)|

## <a name="vm-view-nic"></a> Exibir adaptadores de rede para uma VM

Você pode exibir uma saudação rede interfaces tooa atualmente anexadas VM toolearn sobre a configuração de cada interface de rede e endereços IP hello atribuído tooeach interface de rede. 

1. Faça logon no toohello [portal do Azure](https://portal.azure.com) com uma conta que é atribuída a função de proprietário, colaborador ou colaborador da rede Olá para sua assinatura. toolearn mais sobre como atribuir funções tooaccounts, consulte [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *máquinas virtuais*. Quando **máquinas virtuais** aparece nos resultados da pesquisa hello, clique nele.
3. Em Olá **máquinas virtuais** folha que aparece, clique o nome de saudação do hello VM que você deseja tooview interfaces de rede para.
4. Em Olá **configurações** seção da folha de máquina virtual de saudação que aparece para Olá VM que você selecionou, clique em **interfaces de rede**. toolearn sobre configurações de interface de rede e como toochange-los, leia hello [gerenciar interfaces de rede](virtual-network-network-interface.md) artigo. toolearn sobre como adicionar, alterar ou remover endereços IP atribuídos tooa interface de rede, consulte [endereços IP gerenciar](virtual-network-network-interface-addresses.md).

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI|[az vm show](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-remove-nic"></a> Remover um adaptador de rede de uma VM

Olá VM que você deseja tooremove (ou desconectar) uma interface de rede do deve estar no hello (desalocado) de estado parado e devem ter interfaces de rede pelo menos dois está conectado no momento tooit. Você pode remover qualquer interface de rede, mas Olá VM sempre deve ter pelo menos um tooit anexado de interface de rede. Se você remover uma interface de rede principal, o Azure atribui Olá atributo primário toohello interface de rede que tenha sido anexado toohello Olá VM mais longo. 

1. Faça logon no toohello [portal do Azure](https://portal.azure.com) com uma conta que é atribuída a função de proprietário, colaborador ou colaborador da rede Olá para sua assinatura. toolearn mais sobre como atribuir funções tooaccounts, consulte [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *máquinas virtuais*. Quando **máquinas virtuais** aparece nos resultados da pesquisa hello, clique nele.
3. Em Olá **máquinas virtuais** folha que aparece, clique o nome de saudação do hello VM que você deseja tooremove uma interface de rede para.
4. Em Olá **configurações** seção da folha de máquina virtual de saudação que aparece para Olá VM que você selecionou, clique em **interfaces de rede**. toolearn sobre configurações de interface de rede e como toochange-los, leia hello [gerenciar interfaces de rede](virtual-network-network-interface.md) artigo. toolearn sobre como adicionar, alterar ou remover endereços IP atribuídos tooa interface de rede, consulte [endereços IP gerenciar](virtual-network-network-interface-addresses.md).
5. Na saudação folha de interfaces de rede que aparece, clique em Olá **...**  toohello direito Olá da interface de rede que você deseja toodetach.
6. Clique em **Desanexar**. Se houver apenas uma máquina de virtual network interface anexado toohello, Olá **desanexar** opção não está disponível. Clique em **Sim** na caixa de confirmação de saudação que aparece.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI|[az vm nic remove](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#remove) (referência) ou [etapas detalhadas](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-a-vm)|
|PowerShell|[Remove-AzureRMVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (referência) ou [etapas detalhadas](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-an-existing-vm)|

## <a name="next-steps"></a>Próximas etapas
toocreate uma VM com várias interfaces de rede ou endereços IP, leia Olá artigos a seguir:

**Comandos**

|Tarefa|Ferramenta|
|---|---|
|Criar uma VM com diversos NICs|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Criar uma VM com um NIC com vários endereços IPv4|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Criar uma VM com um NIC com um endereço IPv6 privado (atrás de um Azure Load Balancer)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [modelo do Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
