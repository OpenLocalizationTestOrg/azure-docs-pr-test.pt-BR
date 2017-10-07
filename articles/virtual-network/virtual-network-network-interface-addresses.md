---
title: "aaaConfigure endereços IP de uma interface de rede do Azure | Microsoft Docs"
description: "Saiba como tooadd, alterar e remover endereços públicos e privados para uma interface de rede."
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
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 1e5ea6c65d93be9b1fda5d807500a0823c94c89c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-remove-ip-addresses-for-an-azure-network-interface"></a>Adicionar, alterar ou remover endereços IP para um adaptador de rede do Azure

Saiba como tooadd, alterar e remover endereços públicos e privados para uma interface de rede. Endereços IP privados atribuídos a interface de rede tooa habilitar toocommunicate uma máquina virtual com outros recursos em uma rede virtual do Azure e redes conectadas. Um endereço IP privado também permite toohello de comunicação de saída à Internet usando um endereço IP imprevisível. Um [endereço IP público](virtual-network-public-ip-address.md) atribuído tooa interface de rede permite comunicação de entrada tooa máquina de virtual de saudação à Internet. endereço de saudação também permite que a comunicação de saída de máquina virtual de saudação toohello Internet usando um endereço IP previsível. Para obter detalhes, confira [Entender as conexões de saída no Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Se você precisar toocreate, alterar ou excluir uma interface de rede, leia Olá [gerenciar uma interface de rede](virtual-network-network-interface.md) artigo. Se você precisar de interfaces de rede de tooadd tooor remover interfaces de rede de uma máquina virtual, leia Olá [adicionar ou remover interfaces de rede](virtual-network-network-interface-vm.md) artigo. 


## <a name="before-you-begin"></a>Antes de começar

Olá concluir tarefas a seguir antes de concluir qualquer etapas em qualquer seção deste artigo:

- Saudação de revisão [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn artigo sobre os limites de endereços IP públicos e privados.
- Faça logon no toohello Azure [portal](https://portal.azure.com), interface de linha de comando (CLI) do Azure, ou o PowerShell do Azure com uma conta do Azure. Caso ainda não tenha uma conta do Azure, inscreva-se para obter uma [conta de avaliação gratuita](https://azure.microsoft.com/free).
- Se usar o PowerShell comandos toocomplete tarefas neste artigo, [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que você tem a versão mais recente de saudação do hello commandlets do PowerShell do Azure instalados. tooget ajuda para comandos do PowerShell, com exemplos, digite `get-help <command> -full`.
- Se usar a interface de linha de comando (CLI) do Azure comandos toocomplete tarefas neste artigo, [instalar e configurar Olá CLI do Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que você tem a versão mais recente de saudação do hello CLI do Azure instalado. tooget ajuda para comandos CLI, digite `az <command> --help`. Em vez de instalar Olá CLI e seus pré-requisitos, você pode usar o hello Shell de nuvem do Azure. Olá Shell de nuvem do Azure é um shell Bash livre que podem ser executados diretamente no hello portal do Azure. Ele tem Olá CLI do Azure pré-instalado e configurado toouse com sua conta. Olá toouse Shell de nuvem, clique em Olá nuvem Shell **> _** botão na parte superior de saudação do hello [portal](https://portal.azure.com).

## <a name="add-ip-addresses"></a>Adicionar endereços IP

Você pode adicionar quantas [privada](#private) e [pública](#public) [IPv4](#ipv4) endereços como interface de rede necessário tooa, dentro dos limites de saudação listados no hello [limites do Azure ](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artigo. Você não pode usar o hello portal tooadd uma interface de rede IPv6 endereço tooan (embora quando você criar a interface de rede hello, você pode usar Olá portal tooadd uma interface de rede privada tooa de endereço IPv6). Você pode usar o PowerShell ou Olá CLI tooadd um IPv6 privada endereço tooone [configuração de IP secundária](#secondary) (contanto que não há nenhuma configuração de IP secundária existente), para uma rede existente interface que não está anexado tooa virtual máquina. Não é possível usar qualquer ferramenta tooadd uma interface de rede pública tooa de endereço IPv6. Confira [IPv6](#ipv6) para obter detalhes sobre como usar endereços IPv6. 

1. Faça logon no toohello [portal do Azure](https://portal.azure.com) com uma conta que é atribuídas (no mínimo) permissões para a função de Colaborador de rede Olá para sua assinatura. Saudação de leitura [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artigo toolearn mais sobre como atribuir funções e permissões tooaccounts.
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *interfaces de rede*. Quando **interfaces de rede** aparece nos resultados da pesquisa hello, clique nele.
3. Em Olá **interfaces de rede** folha que aparece, clique em interface de rede Olá endereço tooadd um IPv4 para.
4. Clique em **as configurações de IP** em Olá **configurações** seção da folha de Olá Olá interface de rede selecionado.
5. Clique em **+ adicionar** na folha de saudação que é aberta para as configurações de IP.
6. Especifique Olá seguinte e clique em **Okey** tooclose Olá **configuração Adicionar IP** folha:

    |Configuração|Obrigatório?|Detalhes|
    |---|---|---|
    |Nome|Sim|Deve ser exclusivo para a interface de rede Olá|
    |Tipo|Sim|Uma vez que você está adicionando uma interface de rede IP configuration tooan e cada interface de rede deve ter uma [primário](#primary) configuração IP, sua única opção é **secundário**.|
    |Método de atribuição de endereço IP privado|Sim|[**Dinâmico** ](#dynamic) endereços podem mudar de máquina virtual de saudação for reiniciado depois de ter sido Olá interrompido (desalocado) estado. Azure atribui um endereço disponível de espaço de endereço Olá Olá sub-rede Olá da interface de rede está conectado ao. [**Estático** ](#static) endereços não são liberados até que a interface de rede de saudação é excluído. Especifique um endereço IP do intervalo espaço de endereços de sub-rede de saudação que não está em uso por outra configuração de IP.|
    |Endereço IP público|Não|**Desabilitado:** nenhum recurso de endereço IP público é a configuração de IP toohello atualmente associados. **Habilitado:** selecione um endereço IP público IPv4 existente ou crie um novo. toolearn como toocreate um endereço IP público, ler Olá [endereços IP públicos](virtual-network-public-ip-address.md#create-a-public-ip-address) artigo.|
7. Adicionar manualmente secundário particular IP endereços toohello sistema operacional máquina virtual executando instruções Olá Olá [atribuir vários endereços IP de sistemas de operacionais de computador toovirtual](virtual-network-multiple-ip-addresses-portal.md#os-config) artigo. Consulte [privada](#private) endereços IP para considerações especiais antes de adicionar manualmente o sistema de operacional da máquina virtual de tooa de endereços IP. Não adicione qualquer público IP endereços toohello operacional sistema da máquina virtual.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI|[az network nic ip-config create](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Add-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/add-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-ip-address-settings"></a>Alterar configurações de endereço IP

Método de atribuição de hello toochange de um endereço IPv4, alteração Olá um endereço IPv4 estático, talvez seja necessário ou alterar Olá endereço IP público atribuído tooa interface de rede. Se você estiver alterando o endereço IPv4 privado de saudação de uma configuração de IP secundária associada a uma interface de rede secundário em uma máquina virtual (Saiba mais sobre [interfaces de rede primária e secundária](virtual-network-network-interface-vm.md#about)), local Olá virtual máquina em Olá parada estado (desalocado) antes de concluir Olá etapas a seguir: 

1. Faça logon no toohello [portal do Azure](https://portal.azure.com) com uma conta que é atribuídas (no mínimo) permissões para a função de Colaborador de rede Olá para sua assinatura. Saudação de leitura [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artigo toolearn mais sobre como atribuir funções e permissões tooaccounts.
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *interfaces de rede*. Quando **interfaces de rede** aparece nos resultados da pesquisa hello, clique nele.
3. Em Olá **interfaces de rede** folha que aparece, clique em interface de rede Olá desejado tooview ou alterar as configurações de endereço IP para.
4. Clique em **as configurações de IP** em Olá **configurações** seção da folha de Olá Olá interface de rede selecionado.
5. Clique em configuração de IP hello que deseja toomodify da lista de saudação na folha de saudação que é aberta para as configurações de IP.
6. Alterar Olá configurações, conforme desejado, usando Olá informações sobre configurações de saudação na etapa 6 de saudação [adicionar uma configuração de IP](#create-ip-config) deste artigo. Clique em **salvar** tooclose folha de Olá Olá configuração de IP é alterado.

>[!NOTE]
>Se a interface de rede primária Olá tem várias configurações de IP e você alterar o endereço IP privado de Olá Olá primário da configuração de IP, você deve reatribuir manualmente Olá primário e secundário IP endereços toohello interface de rede do Windows (não necessário para Linux). toomanually atribuir a interface de rede de tooa de endereços IP dentro de um sistema operacional, ler Olá [atribuir vários endereços IP máquinas toovirtual](virtual-network-multiple-ip-addresses-portal.md#os-config) artigo. Consulte [privada](#private) endereços IP para considerações especiais antes de adicionar manualmente o sistema de operacional da máquina virtual de tooa de endereços IP. Não adicione qualquer público IP endereços toohello operacional sistema da máquina virtual.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI|[az network nic ip-config update](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRMNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="remove-ip-addresses"></a>Remover endereços IP

Você pode remover [privada](#private) e [pública](#public) endereços IP de uma interface de rede, mas uma interface de rede sempre deve ter pelo menos um tooit de endereço atribuído IPv4 privado.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com) com uma conta que é atribuídas (no mínimo) permissões para a função de Colaborador de rede Olá para sua assinatura. Saudação de leitura [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artigo toolearn mais sobre como atribuir funções e permissões tooaccounts.
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *interfaces de rede*. Quando **interfaces de rede** aparece nos resultados da pesquisa hello, clique nele.
3. Em Olá **interfaces de rede** folha que aparece, clique em tooremove endereços de IP de interface de rede do hello.
4. Clique em **as configurações de IP** em Olá **configurações** seção da folha de Olá Olá interface de rede selecionado.
5. Com o botão direito um [secundário](#secondary) configuração de IP (não é possível excluir o hello [primário](#primary) configuração) deseja toodelete, clique em **excluir**, em seguida, clique em **Sim**  tooconfirm exclusão de saudação. Se a configuração de saudação teve um recurso de endereço IP público associados tooit, recurso Olá é dissociado da configuração de IP hello, mas Olá recurso não será excluído.
6. Olá fechar **as configurações de IP** folha.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI|[az network nic ip-config delete](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/remove-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="ip-configurations"></a>Configurações de IP

[Privada](#private) e (opcionalmente) [pública](#public) endereços IP são atribuídos tooone ou mais configurações de IP atribuída tooa interface de rede. Há dois tipos de configurações de IP:

### <a name="primary"></a>Primário

Cada adaptador de rede recebe uma configuração de IP primário. Uma configuração de IP primário:

- Tem um [privada](#private) [IPv4](#ipv4) tooit endereço atribuído. Você não pode atribuir uma particular [IPv6](#ipv6) configuração de IP primário do endereço tooa.
- Também pode ter um [pública](#public) tooit de endereço atribuído de IPv4. Não é possível atribuir uma público tooa primária ou secundária IP configuração de endereço IPv6. Você pode, no entanto, atribua um público IPv6 endereço balanceador de carga do Azure tooan, que pode carregar saldo IPv6 endereço da máquina virtual tooa tráfego. Para saber mais, confira [detalhes e limitações do IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations).

### <a name="secondary"></a>Secundário

Além disso tooa configuração de IP primário, uma interface de rede pode ter zero ou mais configurações secundárias IP atribuídas tooit. Uma configuração de IP secundário:

- Deve ter um tooit de endereço atribuído privado IPv4 ou IPv6. Se o endereço de saudação for IPv6, interface de rede Olá só pode ter uma configuração de IP secundária. Se o endereço de saudação for IPv4, interface de rede Olá pode ter várias configurações de IP secundárias atribuídas tooit. toolearn mais sobre como número de endereços IPv4 público e privado pode ser atribuído a interface de rede tooa, consulte Olá [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artigo.  
- Também pode ter um tooit de endereço atribuído IPv4 público, se o endereço IP privado de saudação é IPv4. Se o endereço IP privado de saudação for IPv6, você não pode atribuir um público IPv4 ou IPv6 endereço toohello configuração de IP. Atribuir várias interface de rede IP endereços tooa é útil em cenários como:
    - Hospede vários sites ou serviços com diferentes endereços IP e os certificados SSL em um único servidor.
    - Uma máquina virtual usada como dispositivo de rede virtual, como um firewall ou balanceador de carga.
    - qualquer Olá endereços IPv4 privados de qualquer pool de tooan back-end do balanceador de carga do Azure de interfaces de rede Olá Olá tooadd de capacidade. Olá anterior, apenas Olá primário endereço IPv4 para a interface de rede primária Olá pôde ser adicionado tooa pool de back-end. toolearn mais informações sobre como tooload equilibrar várias configurações de IPv4, consulte Olá [várias configurações de IP de balanceamento de carga](../load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo. 
    - Olá capacidade tooload saldo um IPv6 endereço atribuído tooa interface de rede. toolearn mais informações sobre como tooload equilibrar tooa privado endereço de IPv6, consulte Olá [endereços IPv6 de balanceamento de carga](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.


## <a name="address-types"></a>Tipos de endereço

Você pode atribuir Olá seguintes tipos de tooan de endereços IP [configuração IP](#ip-configurations):

### <a name="private"></a>Privado

Privada [IPv4](#ipv4) endereços habilitar toocommunicate uma máquina virtual com outros recursos em uma rede virtual ou outras redes conectadas. Uma máquina virtual não pode ser comunicada como entrada para, nem pode máquina virtual de saudação comunicar saída com uma particular [IPv6](#ipv6) endereço, com uma exceção. Uma máquina virtual pode se comunicar com o balanceador de carga do Azure hello usando um endereço IPv6. Para saber mais, confira [detalhes e limitações do IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations). 

Por padrão, servidores de DHCP do Azure Olá atribuem endereço IPv4 privado de saudação para Olá [configuração de IP primário](#primary) de saudação interface toohello interface de rede no sistema de operacional de máquina virtual de saudação. A menos que necessário, você deve nunca definir manualmente Olá endereço IP de uma interface de rede no sistema operacional da máquina de virtual hello. 

> [!WARNING]
> Se o endereço IPv4 de saudação definido como endereço IP primário de saudação de uma interface de rede no sistema operacional de uma máquina virtual é nunca diferente do endereço IPv4 privado Olá atribuído a configuração de IP primário toohello Olá principal da interface de rede anexada tooa a máquina virtual no Azure, você perderá a conectividade toohello VM.

Há cenários em que é necessário toomanually definir Olá o endereço IP de uma interface de rede no sistema operacional da máquina de virtual hello. Por exemplo, você deve definir manualmente endereços IP primário e secundário de saudação de um sistema operacional Windows ao adicionar vários tooan de endereços IP máquina virtual do Azure. Para uma máquina virtual Linux, talvez seja necessário apenas endereços IP para secundários do toomanually conjunto hello. Consulte [tooa sistema de operacional VM de endereços de IP adicionar](virtual-network-multiple-ip-addresses-portal.md#os-config) para obter detalhes. Quando você definir o endereço IP de saudação no sistema de operacional Olá manualmente, é recomendável que você atribua sempre uma configuração de IP do hello endereços toohello para uma interface de rede usando Olá atribuição estática (em vez de dinâmicas) método. Atribuição de endereço hello usando o método estático Olá garante que o endereço de saudação não seja alterado no Azure. Se você alguma vez precisar endereço de saudação toochange tooan configuração de IP atribuído, é recomendável que você:

1. tooensure Olá VM está recebendo um endereço de servidores de DHCP do Azure hello, altere a atribuição de saudação do hello IP endereço back tooDHCP de máquina de virtual de saudação de reinicialização e sistema de operacional de saudação.
2. Parar (desalocar) máquina virtual de saudação.
3. Alterar o endereço IP de Olá Olá configuração de IP no Azure.
4. Inicie a máquina virtual de saudação.
5. [Configurar manualmente](virtual-network-multiple-ip-addresses-portal.md#os-config) Olá secundário toomatch de endereços de saudação e sistema operacional (também endereço IP primário do hello dentro do Windows) de IP que você definir no Azure.
 
Seguindo as etapas anteriores hello, Olá privada IP endereço atribuído toohello interface de rede no Azure e no sistema operacional de uma máquina virtual, permanecem Olá mesmo. rastrear tookeep que máquinas virtuais dentro de sua assinatura que você configurou manualmente endereços IP dentro de um sistema operacional, considere a adição de um Azure [marca](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags) toohello VMs. Você pode usar "Atribuição de endereço IP: estático", por exemplo. Dessa forma, você pode localizar facilmente máquinas virtuais de saudação dentro de sua assinatura que você definiu Olá endereço IP no sistema de operacional Olá manualmente.

Além disso, tooenabling toocommunicate uma máquina virtual com outros recursos em Olá conectados ou mesmo redes virtuais, um IP privado de endereços também permite que uma máquina virtual toocommunicate saída toohello da Internet. Conexões de saída são convertido pelo Azure tooan imprevisível endereço IP público de endereço de rede de origem. toolearn mais sobre Azure saída conectividade com a Internet, ler Olá [conectividade de Internet de saída do Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo. Você não pode se comunicar de endereço IP privado de entrada tooa máquina virtual de saudação à Internet.

### <a name="public"></a>Público

Endereços IP públicos habilitar a conectividade de entrada tooa máquina de virtual de saudação à Internet. Conexões de saída toohello Internet usar um endereço IP previsível. Para obter detalhes, confira [Entender as conexões de saída no Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Você pode atribuir uma configuração de IP pública tooan de endereço IP, mas não é necessário. Se você não atribuir uma máquina de virtual do tooa de endereço IP pública, ele ainda possa se comunicar toohello saída à Internet usando seu endereço IP privado. toolearn mais informações sobre endereços IP públicos, ler Olá [endereço IP público](virtual-network-public-ip-address.md) artigo.

Há limites de número toohello privada e endereços IP públicos que você pode atribuir tooa interface de rede. Para obter detalhes, leia Olá [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artigo.

> [!NOTE]
> Azure converte privada IP endereço tooa endereço IP público uma máquina virtual. Como resultado, sistema operacional de saudação desconhece endereços IP públicos atribuídos tooit, portanto não há nenhuma necessidade tooever manualmente atribuir um endereço IP público no sistema operacional de saudação.

## <a name="assignment-methods"></a>Métodos de atribuição

Os endereços IP públicos e privados recebem usando Olá métodos de atribuição a seguir:

### <a name="dynamic"></a>Dinâmico

Endereços IPv4 e (opcionalmente) IPv6 privados dinâmicos são atribuídos por padrão. Endereços dinâmicos podem ser alterados se a máquina virtual de saudação é colocada em hello (desalocado) estado de parado e iniciado. Se você não quiser toochange de endereços IPv4 para a vida útil de saudação da máquina virtual de saudação, atribua endereços de saudação usando o método estático hello. Você só pode atribuir um endereço IPv6 privado usando o método de atribuição dinâmica hello. Não é possível atribuir uma público tooan IP configuração de endereço IPv6 usando um método.

### <a name="static"></a>estático

Não alteram endereços atribuídos usando o método estático Olá até que uma máquina virtual é excluída. Atribuir manualmente privada IPv4 endereço tooan IP estático de espaço de endereço Olá para interface de rede de Olá Olá sub-rede está em. (Opcionalmente), você pode atribuir uma pública ou privada IPv4 endereço tooan configuração de IP estático. Não é possível atribuir uma pública ou privada IPv6 endereço tooan configuração de IP estático. toolearn mais sobre como o Azure atribui endereços IPv4 públicos estáticos, consulte Olá [endereço IP público](virtual-network-public-ip-address.md) artigo.

## <a name="ip-address-versions"></a>Versões de endereço IP

Você pode especificar Olá versões a seguir durante a atribuição de endereços:

### <a name="ipv4"></a>IPv4

Cada adaptador de rede deve ter uma configuração de IP [primário](#primary) com um endereço [IPv4](#ipv4) [privado](#private) atribuído. Você pode adicionar uma ou mais configurações de IP [secundário](#secondary) que possuem um endereço IPv4 privado e (opcionalmente) um IPv4 [público](#public).

### <a name="ipv6"></a>IPv6

Você pode atribuir privada zero ou um [IPv6](#ipv6) endereço tooone secundária configuração de IP de uma interface de rede. interface de rede de saudação não pode ter quaisquer configurações de IP secundárias existentes. Você não pode adicionar uma configuração de IP com um endereço IPv6 usando o portal de saudação. Use o PowerShell ou hello CLI tooadd uma configuração de IP com uma IPv6 endereço tooan existente rede interface privada. interface de rede de saudação não pode ser anexado tooan existente de VM.

> [!NOTE]
> Embora você possa criar uma interface de rede com um endereço IPv6 usando o portal de hello, não é possível adicionar uma rede interface tooa novo ou existente máquina virtual existente, usando o portal de saudação. Usar o PowerShell ou hello Azure CLI 2.0 toocreate uma interface de rede com um endereço IPv6 privado e anexar a interface de rede de saudação ao criar uma máquina virtual. Você não pode anexar a uma interface de rede com um endereço privado de IPv6 atribuído a máquina virtual existente de tooan tooit. Não é possível adicionar uma IPv6 endereço tooan IP configuração privada para qualquer máquina virtual, rede interface anexado tooa usando quaisquer ferramentas (portal, CLI ou o PowerShell).

Não é possível atribuir uma público tooa primária ou secundária IP configuração de endereço IPv6.

## <a name="next-steps"></a>Próximas etapas
toocreate uma máquina virtual com diferentes configurações de IP, ler Olá artigos a seguir:

|Tarefa|Ferramenta|
|---|---|
|Criar uma VM com diversos NICs|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Criar uma VM com um NIC com vários endereços IPv4|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Criar uma VM com um NIC com um endereço IPv6 privado (atrás de um Azure Load Balancer)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [modelo do Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
