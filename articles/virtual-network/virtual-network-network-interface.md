---
title: aaaCreate, alterar ou excluir uma interface de rede do Azure | Microsoft Docs
description: "Saiba o que é uma interface de rede e como alterar as configurações para toocreate e excluir um."
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
ms.openlocfilehash: dcb6cdbd73bc0d0ca4efb9d972d370cf2d54abb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-network-interface"></a>Criar, alterar ou excluir um adaptador de rede

Saiba como alterar as configurações para toocreate e excluir uma interface de rede. Uma interface de rede permite toocommunicate uma máquina Virtual do Azure com a Internet, Azure e recursos locais. Ao criar uma máquina virtual usando Olá portal do Azure, o portal de saudação cria uma interface de rede com configurações padrão para você. Em vez disso, você pode escolher toocreate interfaces de rede com configurações personalizadas e adicionar um ou mais interfaces de rede tooa máquina virtual ao criá-lo. Talvez você também queira toochange configurações de interface de rede padrão para uma interface de rede existente. Este artigo explica como toocreate uma interface de rede com configurações personalizadas, altere as configurações existentes, como a atribuição de (grupo de segurança de rede) de filtro de rede, atribuição de subrede, configurações do servidor DNS e encaminhamento de IP e excluir uma interface de rede.

Se você precisar tooadd, alterar ou remover endereços IP para uma interface de rede, leia Olá [endereços IP gerenciar](virtual-network-network-interface-addresses.md) artigo. Se você precisa de interfaces de rede tooadd ou remove interfaces de rede de máquinas virtuais, leia Olá [adicionar ou remover interfaces de rede](virtual-network-network-interface-vm.md) artigo.


## <a name="before-you-begin"></a>Antes de começar

Olá concluir tarefas a seguir antes de concluir qualquer etapas em qualquer seção deste artigo:

- Saudação de revisão [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn artigo sobre os limites de interfaces de rede.
- Faça logon no toohello Azure [portal](https://portal.azure.com), interface de linha de comando (CLI) do Azure, ou o PowerShell do Azure com uma conta do Azure. Caso ainda não tenha uma conta do Azure, inscreva-se para obter uma [conta de avaliação gratuita](https://azure.microsoft.com/free).
- Se usar o PowerShell comandos toocomplete tarefas neste artigo, [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que você tem a versão mais recente de saudação do hello commandlets do PowerShell do Azure instalados. tooget ajuda para comandos do PowerShell, com exemplos, digite `get-help <command> -full`.
- Se usar a interface de linha de comando (CLI) do Azure comandos toocomplete tarefas neste artigo, [instalar e configurar Olá CLI do Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que você tem a versão mais recente de saudação do hello CLI do Azure instalado. tooget ajuda para comandos CLI, digite `az <command> --help`. Em vez de instalar Olá CLI e seus pré-requisitos, você pode usar o hello Shell de nuvem do Azure. Olá Shell de nuvem do Azure é um shell Bash livre que podem ser executados diretamente no hello portal do Azure. Ele tem Olá CLI do Azure pré-instalado e configurado toouse com sua conta. Olá toouse Shell de nuvem, clique em Olá nuvem Shell **> _** botão na parte superior de saudação do hello [portal](https://portal.azure.com).

## <a name="create-a-network-interface"></a>Criar um adaptador de rede

Ao criar uma máquina virtual usando Olá portal do Azure, o portal de saudação cria uma interface de rede com configurações padrão para você. Se você preferir especificar todas as suas configurações de interface de rede, você pode criar uma interface de rede com configurações personalizadas e anexar a máquina virtual do hello rede interface tooa ao criar a máquina virtual de saudação (usando o PowerShell ou Olá CLI do Azure). Você também pode criar uma interface de rede e adicioná-lo a máquina virtual existente tooan (usando o PowerShell ou Olá CLI do Azure). toolearn como toocreate uma máquina virtual com uma existente tooadd para ou interface de rede, ou remover interfaces de rede de máquinas virtuais existentes, ler Olá [adicionar ou remover interfaces de rede](virtual-network-network-interface-vm.md) artigo. Antes de criar uma interface de rede, você deve ter um existente [rede virtual](virtual-networks-create-vnet-arm-pportal.md) em Olá mesmo local e assinatura você criar uma interface de rede no.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com) com uma conta que é atribuídas (no mínimo) permissões para a função de Colaborador de rede Olá para sua assinatura. Saudação de leitura [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artigo toolearn mais sobre como atribuir funções e permissões tooaccounts.
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *interfaces de rede*. Quando **interfaces de rede** aparece nos resultados da pesquisa hello, clique nele.
3. Em Olá **interfaces de rede** folha que aparece, clique em **+ adicionar**.
4. Em Olá **criar interface de rede** folha que aparece, digite, ou selecionar valores para Olá configurações a seguir e clique em **criar**:

    |Configuração|Obrigatório?|Detalhes|
    |---|---|---|
    |Nome|Sim|Olá nome deve ser exclusivo dentro do grupo de recursos de saudação que você selecionar. Ao longo do tempo, você provavelmente terá vários adaptadores de rede em sua assinatura do Azure. Saudação de leitura [convenções de nomenclatura](/azure/architecture/best-practices/naming-conventions?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions) artigo sugestões ao criar um toomake de convenção de nomenclatura gerenciar várias interfaces mais fácil de rede. nome da saudação não pode ser alterado depois de interface de rede de saudação é criado.|
    |Rede virtual|Sim|Selecione a rede virtual Olá Olá interface de rede. Você só pode atribuir uma rede interface tooa rede virtual existente no hello mesmo assinatura e local como a interface de rede de saudação. Depois de criar uma interface de rede, você não pode alterar a rede virtual hello, a que ele é atribuído. Olá máquina virtual que você adiciona Olá toomust de interface de rede também existem no hello mesmo local e assinatura como interface de rede de saudação.|
    |Sub-rede|Sim|Selecione uma sub-rede na rede virtual de saudação selecionado. Você pode alterar a sub-rede Olá interface de rede Olá recebe tooafter é criado.|
    |Atribuição de endereço IP privado|Sim| Nessa configuração, você escolhe o método de atribuição de saudação para Olá endereço IPv4. Escolher Olá métodos de atribuição a seguir: **dinâmico:** ao selecionar esta opção, Azure atribui automaticamente um endereço disponível saudação do espaço de endereços de sub-rede de saudação selecionado. Azure pode atribuir uma interface de rede do endereço diferente tooa quando Olá máquina de virtual está em é iniciada depois de ter sido Olá interrompido (desalocado) estado. Olá endereço permanece Olá mesmo se a máquina virtual de saudação é reiniciada sem ter sido Olá interrompido (desalocado) estado. **Estático:** ao selecionar esta opção, você deve atribuir manualmente um endereço IP disponível no espaço de endereço de saudação da sub-rede de saudação selecionado. Endereços estáticos não alteram até você alterá-los ou interface de rede de saudação é excluído. Você pode alterar o método de atribuição de hello após a criação da interface de rede de saudação. servidor do DHCP do Azure Olá atribui essa interface de rede do endereço toohello no sistema de operacional de saudação da máquina virtual de saudação.|
    |Grupo de segurança de rede|Não| Deixe definido muito**nenhum**, selecione uma existente [grupo de segurança de rede](virtual-networks-nsg.md), ou [criar um grupo de segurança de rede](virtual-networks-create-nsg-arm-pportal.md). Grupos de segurança de rede permitem o tráfego de rede toofilter dentro e fora de uma interface de rede. Você pode aplicar zero ou uma segurança grupo tooa interface de rede. Zero ou um grupo de segurança de rede também pode ser aplicado toohello interface de rede de saudação de sub-rede é atribuído a. Quando um grupo de segurança de rede é aplicado tooa interface de rede e interface de rede de Olá Olá sub-rede está atribuído, resultados inesperados, às vezes, ocorrerem. interfaces toonetwork aplicados e sub-redes, os grupos de segurança de rede de tootroubleshoot ler Olá [solucionar problemas de grupos de segurança de rede](virtual-network-nsg-troubleshoot-portal.md#nsg) artigo.|
    |Assinatura|Sim|Selecione uma das suas [assinaturas](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) do Azure. máquina virtual de saudação anexar uma rede interface tooand Olá rede virtual você conectá-lo toomust existe no hello mesma assinatura.|
    |Endereço IP privado (IPv6)|Não| Se você selecionar essa caixa de seleção, um endereço IPv6 é atribuído toohello interface de rede, além de toohello endereço IPv4 atribuído toohello interface de rede. Consulte Olá [IPv6](#IPv6) deste artigo para obter informações importantes sobre o uso de IPv6 com interfaces de rede. Não é possível selecionar um método de atribuição de endereço IPv6 de saudação. Se você escolher tooassign um endereço IPv6, ele é atribuído com o método dinâmico Olá.
    |Nome do IPv6 (aparece apenas quando hello **endereço IP privado (IPv6)** caixa de seleção estiver marcada) |Sim, se hello **endereço IP privado (IPv6)** caixa de seleção é marcada.| Esse nome é atribuído a configuração de IP secundária tooa Olá interface de rede. Saiba mais sobre as configurações de IP no hello [exibir configurações de interface de rede](#view-network-interface-settings) deste artigo.|
    |Grupo de recursos|Sim|Selecione um [grupo de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) existente ou crie um. Uma interface de rede pode existir em Olá mesmo, ou outro grupo de recursos, que a máquina virtual de saudação anexá-lo, ou hello virtual de rede você se conectar a ele.|
    |Local|Sim|máquina virtual de saudação anexar uma rede interface tooand Olá rede virtual você conectá-lo toomust existe no hello mesmo [local](https://azure.microsoft.com/regions), também chamado tooas uma região.|

portal de saudação não fornece Olá opção tooassign uma interface de rede pública toohello de endereço IP ao criá-lo, embora o portal Olá criar um endereço IP público e atribuí-la tooa interface de rede quando você cria uma máquina virtual usando o portal de saudação. toolearn como tooadd uma rede pública de toohello de endereço IP de interface depois de criar, ler Olá [endereços IP gerenciar](virtual-network-network-interface-addresses.md) artigo. Se você quiser toocreate uma interface de rede com um endereço IP público, você deve usar o hello CLI ou o PowerShell toocreate Olá interface de rede.

>[!Note]
> Atribui do Azure é uma interface de rede do MAC endereço toohello somente após a interface de rede Olá máquina de virtual tooa anexado e máquina virtual de saudação iniciou Olá pela primeira vez. Não é possível especificar o endereço de MAC hello Azure atribui toohello interface de rede. Olá permanece atribuído de endereço MAC interface de rede toohello até que a interface de rede de saudação é excluído ou endereço IP privado Olá atribuído a configuração de IP primário toohello Olá principal da interface de rede é alterado. toolearn mais informações sobre endereços IP e as configurações de IP, ler Olá [endereços IP gerenciar](virtual-network-network-interface-addresses.md) artigo.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI|[az network nic create](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|

## <a name="view-network-interface-settings"></a>Ver as configurações de adaptador de rede

Você pode exibir e alterar a maioria das configurações de um adaptador de rede após sua criação.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com) com uma conta que é atribuídas (no mínimo) permissões para a função de Colaborador de rede Olá para sua assinatura. Saudação de leitura [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artigo toolearn mais sobre como atribuir funções e permissões tooaccounts.
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *interfaces de rede*. Quando **interfaces de rede** aparece nos resultados da pesquisa hello, clique nele.
3. Em Olá **interfaces de rede** folha que aparece, clique em interface de rede Olá desejado tooview ou alterar as configurações para.
4. Hello configurações a seguir são listadas na folha de saudação que aparece para interface de rede de saudação selecionado:
    - **Visão geral:** fornece informações sobre a interface de rede Olá, como endereços IP hello atribuído tooit, interface de rede de Olá Olá sub-rede virtual é atribuído ao e interface de rede de Olá Olá máquina virtual está anexado muito (se ele é anexado tooone). Olá, imagem a seguir mostra as configurações de visão geral de saudação para uma interface de rede denominado **mywebserver256**: ![visão geral de interface de rede](./media/virtual-network-network-interface/nic-overview.png) você pode mover um grupo de recursos diferentes de tooa de interface de rede ou assinatura clicando (**alterar**) próximo toohello **grupo de recursos** ou **nome da assinatura**. Se você mover a interface de rede hello, você deve mover todas as interfaces de rede toohello relacionados recursos com ele. Se interface de rede de saudação é máquina virtual de tooa anexado, por exemplo, você deve também mover máquina virtual de saudação e outros recursos relacionados à máquina virtual. toomove uma interface de rede, leia Olá [mover recursos tooa novo grupo de recursos ou assinatura](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json#use-portal) artigo. artigo Olá lista os pré-requisitos e como recursos toomove usando Olá do portal do Azure, PowerShell e Olá CLI do Azure.
    - **As configurações de IP:** endereços públicos e privados IPv4 e IPv6 atribuídos tooIP configurações estão listados aqui. Se um endereço IPv6 é atribuído a configuração de IP tooan, endereço de saudação não será exibido. Saiba mais sobre as configurações de IP e como os endereços de IP de tooadd e remover no hello [endereços IP configurar para uma interface de rede do Azure](virtual-network-network-interface-addresses.md) artigo. Encaminhamento de IP e a atribuição de sub-rede também são configurados nesta seção. toolearn mais sobre essas configurações, ler Olá [habilitar ou desabilitar o encaminhamento de IP](#enable-or-disable-ip-forwarding) e [alterar a atribuição de subrede](#change-subnet-assignment) seções deste artigo.
    - **Servidores DNS:** você pode especificar qual servidor DNS uma interface de rede é atribuída pelo Olá servidores DHCP do Azure. Olá rede interface pode herdar a configuração de saudação do hello interface de rede virtual Olá é atribuído a ou ter uma configuração personalizada que substitui a configuração de saudação para rede virtual hello, ele é atribuído a. toomodify o que é exibido, Olá concluir as etapas em Olá [servidores DNS de alteração](#change-dns-servers) deste artigo.
    - **O grupo de segurança de rede (NSG):** Exibe qual NSG está associado a interface de rede toohello (se houver). Um NSG contém regras de entrada e saída o tráfego de rede de toofilter Olá interface de rede. Se um NSG está associado toohello interface de rede, nome de saudação do hello que NSG associado é exibido. toomodify o que é exibido, Olá concluir as etapas em Olá [gerenciar associações de grupo de segurança de rede](virtual-network-manage-nsg-arm-portal.md#manage-associations) artigo.
    - **Propriedades:** exibe configurações de interface de rede hello, incluindo seu endereço MAC (espaço em branco se a interface de rede de saudação não estiver anexado tooa virtual machine) e o hello assinatura existir no.
    - **Regras de segurança efetivo:** as regras de segurança são listadas se a interface de rede de saudação é anexado tooa máquina virtual em execução, e um NSG está associado toohello interface de rede, sub-rede Olá é atribuído a ou ambos. toolearn mais sobre o que é exibido, leia Olá [solucionar problemas de grupos de segurança de rede](virtual-network-nsg-troubleshoot-portal.md#nsg) artigo. toolearn mais sobre os NSGs, ler Olá [grupos de segurança de rede](virtual-networks-nsg.md) artigo.
    - **Rotas efetivas:** rotas são listadas se a interface de rede de saudação é anexado tooa máquina virtual em execução. rotas de saudação são uma combinação de rotas do hello Azure padrão, todas as rotas definidas pelo usuário (UDR) e todas as rotas BGP que podem existir para a interface de rede de Olá Olá sub-rede é atribuído a. toolearn mais sobre o que é exibido, leia Olá [solucionar rotas](virtual-network-routes-troubleshoot-portal.md#view-effective-routes-for-a-network-interface) artigo. toolearn mais sobre o padrão do Azure e UDRs, ler Olá [rotas definidas pelo usuário](virtual-networks-udr-overview.md) artigo.
    - **Configurações comuns do Azure Resource Manager:** toolearn mais sobre configurações comuns do Gerenciador de recursos do Azure, leia Olá [log de atividades](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs), [(IAM) do controle de acesso](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control), [marcas ](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags), [Bloqueia](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json), e [script de automação](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group) artigos.

**Comandos**

Se um endereço IPv6 for atribuído a interface de rede tooa, Olá PowerShell saída retorna fatos Olá que Olá endereço é atribuído, mas ele não retorna o endereço Olá atribuído. Da mesma forma, Olá CLI retorna o fato de Olá Olá endereço é atribuído, mas retorna *nulo* em sua saída para o endereço de saudação.

|Ferramenta|Command|
|---|---|
|CLI|[lista de nic de rede AZ](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#list) tooview interfaces de rede na assinatura Olá; [Mostrar de nic de rede az](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooview configurações para uma interface de rede|
|PowerShell|[Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) tooview interfaces de rede nas configurações de assinatura ou exibição Olá para uma interface de rede|

## <a name="change-dns-servers"></a>Alterar os servidores DNS

servidor DNS Olá é atribuído pela interface de rede de toohello hello Azure DHCP server no sistema de operacional de máquina virtual de saudação. servidor DNS Olá atribuído é qualquer configuração de servidor DNS Olá é uma interface de rede. toolearn mais sobre as configurações de resolução de nome de uma interface de rede, consulte [resolução de nomes para máquinas virtuais](virtual-networks-name-resolution-for-vms-and-role-instances.md). interface de rede de Olá pode herdar as configurações de saudação da rede virtual hello, ou usar suas próprias configurações exclusivas que substituem a configuração de saudação para rede virtual hello.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com) com uma conta que é atribuídas (no mínimo) permissões para a função de Colaborador de rede Olá para sua assinatura. Saudação de leitura [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artigo toolearn mais sobre como atribuir funções e permissões tooaccounts.
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *interfaces de rede*. Quando **interfaces de rede** aparece nos resultados da pesquisa hello, clique nele.
3. Em Olá **interfaces de rede** folha que aparece, clique em interface de rede Olá desejado tooview ou alterar as configurações para.
4. Na folha de Olá Olá interface de rede selecionado, clique em **servidores DNS** em **configurações**.
5. Clique em:
    - **Herdar de rede virtual (padrão)**: Escolha esta opção tooinherit Olá configuração de servidor DNS definida para a interface de Olá Olá rede virtual é atribuído a. No nível de rede virtual hello, um servidor DNS personalizado ou um servidor DNS fornecida pelo Azure Olá é definido. Olá fornecida pelo Azure servidor DNS pode resolver nomes de host para recursos atribuídos toohello mesma rede virtual. FQDN deve ser usado tooresolve para recursos atribuídos toodifferent as redes virtuais.
    - **Personalizar**: você pode configurar seus próprios nomes de tooresolve de servidor DNS em várias redes virtuais. Insira o endereço IP de saudação do servidor de saudação deseja toouse como um servidor DNS. endereço do servidor DNS Olá que você especificar é atribuído somente toothis interface de rede e substitui a que qualquer configuração de DNS para interface de rede de Olá Olá rede virtual é atribuída.
6. Clique em **Salvar**.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI|[az network nic update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="enable-or-disable-ip-forwarding"></a>Habilitar ou desabilitar o encaminhamento de IP

Encaminhamento de IP permite que a máquina virtual de saudação a que uma interface de rede está conectada:
- Receba o tráfego de rede não está destinado a um dos endereços IP hello atribuídos tooany Olá de configurações de IP atribuída toohello interface de rede.
- Envie o tráfego de rede com um endereço IP de origem diferente do hello tooone de atribuído uma das configurações de IP da interface de rede.

configuração de saudação deve ser habilitada para cada interface de rede que é a máquina virtual toohello anexado que recebe o tráfego que Olá tooforward de necessidades de máquina virtual. Uma máquina virtual pode encaminhar tráfego se ele tem várias interfaces de rede ou um tooit anexado de interface de rede única. Enquanto o encaminhamento de IP é uma configuração do Azure, Olá VM também deve executar o tráfego de saudação tooforward capaz de um aplicativo, como firewall, otimização de WAN e aplicativos de balanceamento de carga. Quando uma máquina virtual está em execução para aplicativos de rede, Olá é geralmente chamado tooas um dispositivo de rede virtual. Você pode exibir uma lista de dispositivos de rede virtual toodeploy pronto em Olá [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances). O encaminhamento de IP normalmente é usado com rotas definidas pelo usuário. toolearn mais sobre as rotas definidas pelo usuário, ler Olá [rotas definidas pelo usuário](virtual-networks-udr-overview.md) artigo.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com) com uma conta que é atribuídas (no mínimo) permissões para a função de Colaborador de rede Olá para sua assinatura. Saudação de leitura [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artigo toolearn mais sobre como atribuir funções e permissões tooaccounts.
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *interfaces de rede*. Quando **interfaces de rede** aparece nos resultados da pesquisa hello, clique nele.
3. Em Olá **interfaces de rede** folha que aparece, clique em interface de rede Olá deseja tooenable ou desabilitar o encaminhamento IP para.
4. Na folha de Olá Olá interface de rede selecionado, clique em **as configurações de IP** em Olá **configurações** seção.
5. Clique em **habilitado** ou **desabilitado** configuração de saudação toochange (configuração padrão).
6. Clique em **Salvar**.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI|[az network nic update](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet-assignment"></a>Alterar atribuição de sub-rede

Você pode alterar a sub-rede hello, mas não Olá rede virtual, atribuído a uma interface de rede.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com) com uma conta que é atribuídas (no mínimo) permissões para a função de Colaborador de rede Olá para sua assinatura. Saudação de leitura [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artigo toolearn mais sobre como atribuir funções e permissões tooaccounts.
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *interfaces de rede*. Quando **interfaces de rede** aparece nos resultados da pesquisa hello, clique nele.
3. Em Olá **interfaces de rede** folha que aparece, clique em interface de rede Olá desejado tooview ou alterar as configurações para.
4. Clique em **as configurações de IP** em **configurações** na folha Olá Olá interface de rede selecionado. Se os endereços IP particulares para todas as configurações de IP listado **(estático)** toothem próxima, você deve alterar Olá IP endereço atribuição método toodynamic completando as etapas de saudação que seguem. Todos os endereços IP privados devem ser atribuídos com hello atribuição dinâmica método toochange Olá sub-rede atribuição Olá interface de rede. Se Olá endereços são atribuídos com o método dinâmico Olá, continue toostep cinco. Se os endereços IPv4 são atribuídos com o método de atribuição estática de hello, conclua Olá etapas toochange Olá atribuição método toodynamic a seguir:
    - Clique em configuração de IP hello deseja toochange Olá método de atribuição de endereço IPv4 para lista de saudação de configurações de IP.
    - Olá folha que aparece para a configuração de IP hello, clique em **dinâmico** para Olá **atribuição** método. Você não pode atribuir um endereço IPv6 com o método de atribuição estática hello.
    - Clique em **Salvar**.
5. Selecione subrede Olá deseja tooconnect Olá Olá de toofrom de interface de rede **sub-rede** lista suspensa.
6. Clique em **Salvar**. Novos endereços dinâmicos são atribuídos em intervalo de endereços de sub-rede Olá para nova subrede hello. Depois de atribuir Olá interface tooa nova sub-rede, você pode atribuir um endereço IPv4 estático do novo intervalo de endereços de sub-rede hello, se você escolher. mais sobre como adicionar, alterar e remover endereços IP para uma interface de rede, leia a saudação de toolearn [endereços IP gerenciar](virtual-network-network-interface-addresses.md) artigo.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI|[az network nic ip-config update](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-a-network-interface"></a>Excluir um adaptador de rede

Você pode excluir uma interface de rede, desde que ele tooa anexado máquina virtual não é. Se ele estiver anexado tooa VM, você deve primeiro estado de máquina virtual em Olá parado (desalocado) Olá local, desanexar a interface de rede de saudação da máquina virtual de Olá, antes de excluir a interface de rede de saudação. toodetach uma interface de rede de uma máquina virtual, Olá concluir as etapas em Olá [desanexar uma interface de rede de uma máquina virtual](virtual-network-network-interface-vm.md#vm-remove-nic) seção Olá [adicionar ou remover interfaces de rede](virtual-network-network-interface-vm.md) artigo. Excluir uma máquina virtual Desconecta todas as tooit anexado interfaces de rede, mas não exclui as interfaces de rede de saudação.

1. Faça logon no toohello [portal do Azure](https://portal.azure.com) com uma conta que é atribuídas (no mínimo) permissões para a função de Colaborador de rede Olá para sua assinatura. Saudação de leitura [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artigo toolearn mais sobre como atribuir funções e permissões tooaccounts.
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *interfaces de rede*. Quando **interfaces de rede** aparece nos resultados da pesquisa hello, clique nele.
3. Interface de rede de saudação com o botão direito que deseja toodelete e clique **excluir**.
4. Clique em **Sim** tooconfirm exclusão Olá da interface de rede.

Quando você exclui uma interface de rede, qualquer MAC ou endereços IP atribuídos tooit são liberados.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI|[az network nic delete](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmNetworkInterface](/powershell/module/azurerm.network/remove-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>Próximas etapas
endereços de uma máquina virtual com várias interfaces de rede IP toocreate, leia Olá artigos a seguir:

**Comandos**

|Tarefa|Ferramenta|
|---|---|
|Criar uma VM com diversos NICs|[CLI](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Criar uma VM com um NIC com vários endereços IPv4|[CLI](virtual-network-multiple-ip-addresses-cli.md), [PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Criar uma VM com um NIC com um endereço IPv6 privado (atrás de um Azure Load Balancer)|[CLI](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [modelo do Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
