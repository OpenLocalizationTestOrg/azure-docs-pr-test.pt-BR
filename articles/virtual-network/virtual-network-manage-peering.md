---
title: aaaCreate, alterar ou excluir um emparelhamento de rede virtual do Azure | Microsoft Docs
description: Saiba como toocreate, alterar ou excluir um emparelhamento de rede virtual.
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
ms.date: 07/26/2017
ms.author: jdial
ms.openlocfilehash: 70f85364ab23e23533ad276aeec0156cebe89be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network-peering"></a>Criar, alterar ou excluir um emparelhamento da rede virtual

Saiba como toocreate, alterar ou excluir um emparelhamento de rede virtual. Emparelhamento de rede virtual permite você tooconnect duas redes virtuais no mesmo local do Azure por meio de Olá Olá rede backbone do Azure. Depois de emparelhadas, duas redes virtuais de saudação ainda são gerenciadas como recursos separados. Recursos em qualquer rede virtual se comunicar com hello mesmo latência e a largura de banda que recursos Olá no hello mesma rede virtual. Se você não estiver familiarizado com o emparelhamento de rede virtual, é recomendável ler Olá [visão geral emparelhamento de rede Virtual](virtual-network-peering-overview.md) e Concluindo Olá [criar um tutorial de emparelhamento de rede virtual](virtual-network-create-peering.md), antes da conclusão tarefas de saudação neste artigo.

## <a name="before-you-begin"></a>Antes de começar

Olá concluir tarefas a seguir antes de concluir as etapas em qualquer seção deste artigo:

- Saudação de revisão [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn artigo sobre os limites de emparelhamento.
- Faça logon em toohello portal do Azure, interface de linha de comando (CLI) do Azure ou do PowerShell do Azure com uma conta do Azure. Caso ainda não tenha uma conta do Azure, inscreva-se para obter uma [conta de avaliação gratuita](https://azure.microsoft.com/free).
- Se usar o PowerShell comandos toocomplete tarefas neste artigo, [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que você tem a versão mais recente Olá dos cmdlets do PowerShell do Azure Olá instalados. tooget ajuda para comandos do PowerShell, com exemplos, digite `get-help <command> -full`.
- Se usar a interface de linha de comando (CLI) do Azure comandos toocomplete tarefas neste artigo, [instalar e configurar Olá CLI do Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que você tem a versão mais recente de saudação do hello CLI do Azure instalado. tooget ajuda para comandos CLI, digite `az <command> --help`. Em vez de instalar Olá CLI e seus pré-requisitos, você pode usar o hello Shell de nuvem do Azure. Olá Shell de nuvem do Azure é um shell Bash livre que podem ser executados diretamente no hello portal do Azure. Olá Shell de nuvem tem Olá CLI do Azure pré-instalado e configurado toouse com sua conta. Olá toouse Shell de nuvem, clique em Olá nuvem Shell **> _** botão na parte superior de saudação do hello [portal](https://portal.azure.com). 

## <a name="create-a-peering"></a>Criar um emparelhamento

>[!NOTE]
>Existem vários requisitos, restrições e considerações toosuccessfully criar um emparelhamento de rede virtual. Antes de criar um emparelhamento, certifique-se de que você Familiarize-se com hello [requisitos e restrições](#requirements-and-constraints) e [as permissões necessárias](#permissions).
>

1. Faça logon no toohello [portal](https://portal.azure.com) com uma conta que é atribuída a saudação necessário [função ou as permissões](#permissions).
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *redes virtuais*. Quando **redes virtuais** aparece nos resultados da pesquisa hello, clique nele. Não selecione **redes virtuais (clássico)** se ele aparece na lista de hello, pois não é possível criar um emparelhamento de uma rede virtual implantada por meio do modelo de implantação clássico hello.
3. Em Olá **redes virtuais** folha que aparece, clique em rede virtual hello, você deseja toocreate um emparelhamento para.
4. No painel de saudação que aparece para a rede virtual de saudação selecionado, clique em **emparelhamentos** em Olá **configurações** seção.
5. Clique em **+ Adicionar**. 
6. <a name="add-peering"></a>Em Olá **adicionar emparelhamento** folha, insira ou selecione valores para Olá configurações a seguir:
    - **Nome:** nome Olá Olá emparelhamento deve ser exclusivo na rede virtual hello.
    - **Modelo de implantação de rede virtual:** selecione quais saudação do modelo de implantação virtual rede que você deseja toopeer com foi implantado por meio de.
    - **Sei minha ID de recurso:** se você tem acesso de leitura toohello rede virtual você deseja toopeer com, deixe essa caixa de seleção desmarcada. Se você não tiver acesso de leitura toohello a rede virtual ou assinatura que você deseja toopeer com, essa caixa de seleção. Insira a ID de recurso completo de saudação da rede virtual hello, você deseja toopeer com em Olá **ID de recurso** caixa exibida quando você tiver marcado a caixa de saudação. recurso Olá ID que você digitar deve ser para uma rede virtual existe no hello Azure mesmo [local](https://azure.microsoft.com/regions) como essa rede virtual. ID de recurso completo Olá parece semelhantesmuito/assinaturas/<Id>/providers/Microsoft.Network/virtualNetworks/ /resourceGroups/ < resource-group-name > <--nome de rede virtual >. Você pode obter a ID de recurso Olá para uma rede virtual exibindo as propriedades de saudação para uma rede virtual. toolearn como propriedades de saudação tooview para uma rede virtual, consulte [gerenciar redes virtuais](virtual-network-manage-network.md#view-vnet).
    - **Assinatura:** Olá selecione [assinatura](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) da rede virtual Olá deseja toopeer com. Uma ou mais assinaturas estão listadas, dependendo de quantas assinaturas sua conta tem acesso de leitura. Se você tiver marcado a saudação **ID de recurso** caixa de seleção, essa configuração não está disponível. Você pode emparelhar redes virtuais em assinaturas diferentes, desde que as duas redes virtuais tenham sido criadas por meio do Resource Manager. Olá capacidade toopeer em assinaturas criadas por meio de diferentes modelos de implantação está em versão de visualização. Registrar para visualização de saudação antes de criar um emparelhamento entre redes virtuais implantadas por meio de diferentes modelos de implantação que existem em assinaturas diferentes. Saiba mais sobre como tooregister para visualização hello e [redes virtuais criadas por meio de modelos de implantação diferentes em diferentes assinaturas ponto a ponto](create-peering-different-deployment-models-subscriptions.md).
    - **Rede virtual:** selecione Olá rede virtual que você deseja toopeer com. Você pode selecionar uma rede virtual criada por meio de um modelo de implantação do Azure, mas a rede virtual Olá deve estar no hello mesmo local Olá rede virtual está iniciando Olá emparelhamento do. Você deve ter leitura acesso toohello a rede virtual para que ele toobe visível na lista de saudação. Se uma rede virtual estiver listada, mas esmaecidas, pode ser porque o espaço de endereço de saudação para rede virtual Olá se sobrepõe ao espaço de endereço de saudação para essa rede virtual. Se os espaços de endereço de rede virtual se sobrepõem, eles não podem ser emparelhados. Se você tiver marcado a saudação **ID de recurso** caixa de seleção, essa configuração não está disponível.
    - **Permitir acesso à rede virtual:** selecione **habilitado** (padrão), se você quiser tooenable comunicação entre redes virtuais Olá dois. Habilitar a comunicação entre redes virtuais permite que os recursos conectados tooeither toocommunicate de rede virtual entre si com hello mesma largura de banda e latência, como se estivesse conectado toohello mesma rede virtual. Todas as comunicações entre os recursos em duas redes virtuais de saudação é Olá rede privada do Azure. Olá **VirtualNetwork** marca padrão para grupos de segurança de rede abrange a rede virtual hello e emparelhada rede virtual. marcas de padrão do grupo de segurança, de rede mais sobre toolearn ler Olá [visão geral de grupos de segurança de rede](virtual-networks-nsg.md#default-tags) artigo.  Selecione **desabilitado** se não quiser que o tráfego tooflow toohello emparelhadas rede virtual. Você pode selecionar **desabilitado** se você tiver emparelhadas uma rede virtual com outra rede virtual, mas deseja ocasionalmente toodisable o fluxo do tráfego entre redes virtuais Olá dois. Você pode achar que a habilitação e desabilitação é mais conveniente que excluir e recriar emparelhamentos. Quando essa configuração estiver desabilitada, o tráfego não flua entre Olá emparelhadas redes virtuais.
    - **Permitir tráfego encaminhado:** verificar este toohello de tráfego encaminhado tooallow caixa emparelhadas rede virtual (tráfego não de origem na rede virtual emparelhadas Olá) rede virtual do tooflow toothis. Encaminhamento de tráfego é comum quando você implantou um dispositivo de rede virtual na rede virtual de saudação estiver emparelhamento com e criado rotas definidas pelo usuário tooforward tráfego por meio da solução de virtualização de rede hello. Se você deixar essa caixa desmarcada (padrão), o tráfego encaminhado de rede virtual emparelhadas Olá não é possível fluir rede virtual toothis. Ao habilitar esse recurso permite o tráfego de saudação encaminhado por meio do emparelhamento hello, ele não cria todas as rotas definidas pelo usuário ou soluções de virtualização de rede. Rotas definidas pelo usuário e dispositivos de rede virtual são criados separadamente. Saiba mais sobre [rotas definidas pelo usuário](virtual-networks-udr-overview.md).
    - **Permitir tráfego de gateway:** essa caixa de seleção se você tiver uma rede virtual do toothis anexado de gateway de rede virtual e deseja tooallow tráfego da saudação emparelhadas tooflow de rede virtual por meio do gateway de saudação. Por exemplo, esta rede virtual pode ser anexado tooan rede de local por meio de um gateway de rede virtual. Verificando a que esta caixa permite o tráfego de saudação emparelhadas tooflow de rede virtual por meio da rede virtual do hello gateway toothis anexado. Se você marcar essa caixa, a rede virtual emparelhadas Olá não pode ter um gateway configurado. rede virtual emparelhadas Olá deve ter Olá **usar gateway remoto** caixa de seleção marcada quando configurar o emparelhamento de saudação do hello outra rede virtual de toothis de rede virtual. Se você deixar essa caixa desmarcada (padrão), o tráfego de rede virtual emparelhadas Olá ainda fluxos de rede virtual toothis, mas não é possível fluir através de uma rede virtual do toothis anexado de gateway de rede virtual. Saiba mais sobre [gateways de rede virtual](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#s2smulti). 
    
    Você não pode habilitar essa opção se você estiver emparelhando uma rede virtual (Resource Manager) com uma rede virtual (clássica). Embora o tráfego Olá flui entre as duas redes virtuais Olá, hello (clássico) tráfego de rede virtual não é possível fluir com uma rede virtual de rede gateway toohello anexado (Gerenciador de recursos).
    - **Usar gateways remotos:** verificar esse tráfego de tooallow da caixa de tooflow essa rede virtual por meio de uma rede virtual gateway toohello anexado rede virtual que está emparelhamento com. Por exemplo, Olá rede virtual que você está emparelhamento com possui um gateway VPN anexado que habilita comunicação tooan local na rede.  Marcar essa caixa permite o tráfego de tooflow essa rede virtual por meio de saudação VPN gateway toohello anexado emparelhada rede virtual. Se você marcar esta caixa, rede virtual emparelhadas Olá deve ter um tooit anexado de gateway de rede virtual e deve ter Olá **permitir tráfego de gateway** caixa de seleção marcada. Se você deixar essa caixa desmarcada (padrão), o tráfego de rede virtual emparelhadas Olá ainda possa fluir toothis virtual de rede, mas não é possível fluir através de uma rede virtual do toothis anexado de gateway de rede virtual. 
    
    Você não pode habilitar essa opção se você estiver emparelhando uma rede virtual (Resource Manager) com uma rede virtual (clássica). Embora tráfego Olá flui entre as duas redes virtuais Olá, tráfego de rede virtual (Gerenciador de recursos) de saudação não é possível fluir através de uma rede gateway toohello anexado rede virtual (clássica).
7. Clique em Olá **Okey** botão tooadd Olá sub-rede toohello rede virtual selecionada.

### <a name="commands"></a>Comandos

|Ferramenta|Command|
|---|---|
|CLI|[criar emparelhamento de VNET de rede virtual az](/cli/azure/network/vnet/peering#create?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Add-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|


### <a name="scenarios"></a>Cenários

Um emparelhamento de rede virtual é criado entre redes virtuais criadas por meio de saudação iguais ou diferentes modelos de implantação que existem no hello iguais ou diferentes assinaturas. Conclua um tutorial passo a passo para uma saudação os seguintes cenários:
 
|Modelo de implantação do Azure  | Assinatura  |
|---------|---------|
|Ambos Resource Manager |[Idêntica](virtual-network-create-peering.md)|
| |[Diferente](create-peering-different-subscriptions.md)|
|Um Resource Manager, um clássico     |[Idêntica](create-peering-different-deployment-models.md)|
| |[Diferente](create-peering-different-deployment-models-subscriptions.md)|

## <a name="view-or-change-peering-settings"></a>Exibir ou alterar as configurações de emparelhamento

1. Faça logon no toohello [portal](https://portal.azure.com) com uma conta que é atribuída a saudação necessário [função ou as permissões](#permissions).
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *redes virtuais*. Quando **redes virtuais** aparece nos resultados da pesquisa hello, clique nele.
3. Em Olá **redes virtuais** folha que aparece, clique em rede virtual hello, você deseja toocreate um emparelhamento para.
4. No painel de saudação que aparece para a rede virtual de saudação selecionado, clique em **emparelhamentos** em Olá **configurações** seção.
5. Clique em Olá emparelhamento deseja tooview ou alterar as configurações.
6. Alterar a configuração apropriada hello. Leia sobre as opções para cada configuração no hello [etapa 6](#add-peering) de saudação criar uma seção emparelhamento deste artigo. 

    >[!NOTE]
    >Existem vários requisitos, restrições e considerações toosuccessfully criar um emparelhamento de rede virtual. Antes de criar um emparelhamento, certifique-se de que você Familiarize-se com hello [requisitos e restrições](#requirements-and-constraints) e [as permissões necessárias](#permissions).
    >

7. Clique em **Salvar**.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI|[lista de emparelhamento AZ rede rede virtual](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#list) toolist emparelhamentos de uma rede virtual, [az rede Mostrar emparelhamento vnet](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooshow configurações para um emparelhamento específico, e [az rede atualização de emparelhamento vnet](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#update) configurações de emparelhamento toochange.|
|PowerShell|[Get-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/get-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve exibir as configurações de emparelhamento e [AzureRmVirtualNetworkPeering conjunto](/powershell/module/azurerm.network/set-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json) toochange configurações.|

## <a name="delete-a-peering"></a>Excluir um emparelhamento
Quando um emparelhamento é excluído, o tráfego de uma rede virtual não é mais fluxos de rede virtual emparelhadas toohello. Quando implantadas por meio do Gerenciador de recursos de redes virtuais estão pareadas, cada rede virtual tem um emparelhamento toohello outra rede virtual. Embora excluir Olá emparelhamento de uma rede virtual desabilita a comunicação entre redes virtuais Olá Olá, ele não exclui Olá emparelhamento de saudação outra rede virtual. Olá status de emparelhamento para Olá emparelhamento que existe no hello outra rede virtual é **Disconnected**. Você não pode recriar Olá emparelhamento até que você recrie o emparelhamento de saudação na primeira rede virtual de saudação e status de emparelhamento Olá para virtual redes alterações muito*conectado*. 

Se você quiser toocommunicate redes virtuais às vezes, mas não sempre, em vez de excluir um emparelhamento, você pode definir Olá **permitir acesso à rede virtual** configuração muito**desabilitado** em vez disso. toolearn como, leia a etapa 6 de saudação [criar um emparelhamento](#create-peering) deste artigo. Você pode achar que desabilitar e habilitar o acesso à rede é mais fácil do que excluir e recriar emparelhamentos.

1. Faça logon no toohello [portal](https://portal.azure.com) com uma conta que é atribuída a saudação necessário [função ou as permissões](#permissions).
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *redes virtuais*. Quando **redes virtuais** aparece nos resultados da pesquisa hello, clique nele.
3. Em Olá **redes virtuais** folha que aparece, clique em rede virtual hello, você deseja toodelete um emparelhamento de.
4. Olá folha que aparece para a rede virtual de saudação selecionado, clique em **emparelhamentos** em **configurações**.
5. Na lista de saudação de emparelhamentos que aparece na folha de emparelhamentos hello, com o botão direito Olá emparelhamento você deseja toodelete, clique em **excluir**, em seguida, **Sim** toodelete Olá emparelhamento da primeira rede virtual de saudação.
6. Olá completo anterior etapas toodelete Olá emparelhamento de Olá outra rede virtual no emparelhamento via protocolo hello.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI|[excluir emparelhamento de rede virtual az](/cli/azure/network/vnet/peering?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetworkPeering](/powershell/module/azurerm.network/remove-azurermvirtualnetworkpeering?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="requirements-and-constraints"></a>Requisitos e restrições 

- as redes virtuais Olá que você ponto devem ter espaços de endereço IP sem sobreposição.
- Você não pode adicionar espaços de endereços, ou excluir espaços de endereços de uma rede virtual depois que ela é emparelhada com outra rede virtual. tooadd ou remover espaços de endereço, Olá delete emparelhamento, adicionam ou remover os espaços de endereço hello e recrie o emparelhamento de saudação. saudação de leitura tooadd espaços de endereço, ou remover espaços de endereço de redes virtuais, [criar, alterar ou excluir as redes virtuais](virtual-network-manage-network.md#add-address-spaces) artigo. 
- Você pode emparelhar duas redes virtuais implantadas por meio do Gerenciador de recursos ou uma rede virtual implantado por meio do Gerenciador de recursos com uma rede virtual implantada por meio do modelo de implantação clássico hello. Não é possível emparelhar duas redes virtuais criadas por meio do modelo de implantação clássico hello. Se você não estiver familiarizado com modelos de implantação do Azure, leia Olá [modelos de implantação do Azure entender](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo. Você pode usar um [Gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect dois as redes virtuais criadas por meio do modelo de implantação clássico hello.
- Quando o emparelhamento duas redes virtuais criadas por meio do Gerenciador de recursos, um emparelhamento deve ser configurado para cada rede virtual no emparelhamento via protocolo hello. Quando você cria Olá emparelhamento toohello segunda rede virtual da rede virtual do primeiro hello, status de emparelhamento Olá é *iniciada*.  Quando você cria o emparelhamento Olá Olá rede virtual segundo toohello primeira rede virtual, seu status de emparelhamento é *conectado*. Se você exibir o status de emparelhamento Olá para rede virtual do primeiro Olá, você verá seu status alterado de *iniciada* muito*conectado*. Olá emparelhamento não é estabelecida com êxito até que o status de emparelhamento Olá para ambos os emparelhamentos de rede virtual é *conectado*. 
- Quando o emparelhamento de uma rede virtual criada por meio do Gerenciador de recursos com uma rede virtual criada por meio do modelo de implantação clássico Olá, só é configurar um emparelhamento para rede virtual de saudação implantado por meio do Gerenciador de recursos. Você não pode configurar o emparelhamento de uma rede virtual (clássica) ou entre duas redes virtuais implantadas por meio do modelo de implantação clássico hello. Quando você cria Olá emparelhamento de rede virtual de toohello (Gerenciador de recursos) de rede virtual da saudação (clássico), status de emparelhamento Olá é *atualização*, logo altera muito*conectado*.   
- Um emparelhamento é estabelecido entre duas redes virtuais. Os emparelhamentos não são provisórios. Se você criar emparelhamentos entre:
    - VirtualNetwork1 e VirtualNetwork2
    - VirtualNetwork2 e VirtualNetwork3

  Não há nenhum emparelhamento entre VirtualNetwork1 e VirtualNetwork3 por meio de VirtualNetwork2. Se você quiser toocreate uma rede virtual emparelhamento entre VirtualNetwork1 e VirtualNetwork3, você tem toocreate um emparelhamento entre VirtualNetwork1 e VirtualNetwork3.
- Você não pode resolver nomes em redes virtuais emparelhadas usando a resolução de nomes do Azure padrão. nomes de tooresolve em outras redes virtuais, você deve usar um servidor DNS personalizado. toolearn como tooset o seu próprio servidor DNS, ler Olá [resolução de nome usando seu próprio servidor DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) artigo.
- Recursos em ambas as redes virtuais no emparelhamento Olá possam se comunicar entre si com hello mesmo largura de banda e latência como se estivesse em Olá a mesma rede virtual. No entanto, o tamanho de cada máquina virtual tem sua própria largura de banda de rede máxima. toolearn mais sobre a largura de banda de rede máxima para tamanhos de máquina virtual diferente, ler Olá [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigos de tamanhos de máquina virtual.
- Você pode emparelhar redes virtuais implantadas por meio do Gerenciador de recursos que estão em Olá iguais, ou assinaturas diferentes.
- Você pode emparelhar redes virtuais implantadas por meio de diferentes modelos de implantação que estão em Olá iguais, ou assinaturas diferentes (visualização). 
- Olá assinaturas em ambas as redes virtuais devem ser associado toohello mesmo locatário do Active Directory do Azure. Se você ainda não tiver um locatário do AD, [crie um](../active-directory/develop/active-directory-howto-tenant.md?toc=%2fazure%2fvirtual-network%2ftoc.json#start-from-scratch) rapidamente. Você pode usar um [Gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#V2V) tooconnect duas redes virtuais que existem em diferentes assinaturas associadas locatários do toodifferent do Active Directory.
- Uma rede virtual pode ser emparelhadas tooanother VPN e também ser tooanother conectados a rede virtual com um gateway de rede virtual do Azure. Quando as redes virtuais são conectadas por meio do emparelhamento e um gateway, fluxos de tráfego entre redes virtuais Olá por meio da configuração de emparelhamento hello, em vez de gateway de saudação.
- Há um custo nominal para tráfego de entrada e saída que utiliza um emparelhamento de rede virtual. Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/virtual-network).


## <a name="permissions"></a>Permissões

contas de saudação que usar toocreate um emparelhamento de rede virtual devem ter função necessário hello ou as permissões. Por exemplo, se foram emparelhamento duas redes virtuais chamadas myVnetA e myVnetB, sua conta deve ser atribuída Olá função mínimo ou as permissões para cada rede virtual a seguir:
    
|Rede virtual|Modelo de implantação|Função|Permissões|
|---|---|---|---|
|myVnetA|Gerenciador de Recursos|[Colaborador de rede](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Clássico|[Colaborador de rede clássica](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|N/D|
|myVnetB|Gerenciador de Recursos|[Colaborador de rede](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Clássico|[Colaborador de rede clássica](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Saiba mais sobre [funções internas](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) e atribuindo permissões específicas muito[funções personalizadas](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (somente no Gerenciador de recursos).

## <a name="next-steps"></a>Próximas etapas

Saiba como toocreate uma [topologia de rede de hub e spoke](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) 
