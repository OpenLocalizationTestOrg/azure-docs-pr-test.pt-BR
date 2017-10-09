---
title: "aaaCreate, alterar ou excluir um endereço IP público do Azure | Microsoft Docs"
description: "Saiba como toocreate, alterar ou excluir um endereço IP público."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bb71abaf-b2d9-4147-b607-38067a10caf6
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 0f2578e8661c8f33419b896debcfa0ba1b41fc5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-public-ip-address"></a>Criar, alterar ou excluir um endereço IP público

Saiba mais sobre um IP público de endereços e como toocreate, alterar e excluir um. Um endereço IP público é um recurso com suas próprias definições configuráveis. Permite que um tooother de endereço IP público a atribuição de recursos do Azure:
- Entrada tooresources de conectividade de Internet, como máquinas virtuais (VM) do Azure, conjuntos de escala de máquina Virtual do Azure, Gateway de VPN do Azure, os gateways de aplicativos e balanceadores de carga do Azure para a Internet. Recursos do Azure não é possível receber comunicação de entrada de saudação à Internet sem um endereço IP público atribuído. Enquanto alguns recursos do Azure são inerentemente acessíveis por meio de endereços IP públicos, outros recursos devem ter endereços IP públicos atribuídos toothem toobe acessível de saudação à Internet.
- Conectividade de saída toohello Internet usando um endereço IP previsível. Por exemplo, uma máquina virtual pode se comunicar toohello saída à Internet sem um tooit de endereço atribuído de IP público, mas seu endereço é o endereço de rede convertido pelo endereço público do imprevisível tooan do Azure. Atribuição de um recurso de tooa de endereço IP público habilita tooknow qual endereço IP é usado para conexão de saída de hello. Embora previsível, endereço Olá pode mudar, dependendo do método de atribuição de saudação escolhido. Para saber mais, confira [Criar um endereço IP público](#create-a-public-ip-address). toolearn mais sobre conexões de saída de recursos do Azure, leia Olá [entender as conexões de saída](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo.

## <a name="before-you-begin"></a>Antes de começar

Olá concluir tarefas a seguir antes de concluir qualquer etapas em qualquer seção deste artigo:

- Saudação de revisão [Azure limita](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn artigo sobre os limites de endereços IP públicos.
- Faça logon no toohello Azure [portal](https://portal.azure.com), interface de linha de comando (CLI) do Azure, ou o PowerShell do Azure com uma conta do Azure. Caso ainda não tenha uma conta do Azure, inscreva-se para obter uma [conta de avaliação gratuita](https://azure.microsoft.com/free).
- Se usar o PowerShell comandos toocomplete tarefas neste artigo, [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que você tem a versão mais recente de saudação do hello commandlets do PowerShell do Azure instalados. tooget ajuda para comandos do PowerShell, com exemplos, digite `get-help <command> -full`.
- Se usar a interface de linha de comando (CLI) do Azure comandos toocomplete tarefas neste artigo, [instalar e configurar Olá CLI do Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Certifique-se de que você tem a versão mais recente de saudação do hello CLI do Azure instalado. tooget ajuda para comandos CLI, digite `az <command> --help`. Em vez de instalar Olá CLI e seus pré-requisitos, você pode usar o hello Shell de nuvem do Azure. Olá Shell de nuvem do Azure é um shell Bash livre que podem ser executados diretamente no hello portal do Azure. Ele tem Olá CLI do Azure pré-instalado e configurado toouse com sua conta. Olá toouse Shell de nuvem, clique em Olá nuvem Shell **> _** botão na parte superior de saudação do hello [portal](https://portal.azure.com).

Os endereços IP públicos têm um encargo nominal. tooview Olá preços, ler Olá [preço do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página. 

## <a name="create-a-public-ip-address"></a>Criar um endereço IP público

1. Faça logon no toohello [portal do Azure](https://portal.azure.com) com uma conta que é atribuídas (no mínimo) permissões para a função de Colaborador de rede Olá para sua assinatura. Saudação de leitura [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artigo toolearn mais sobre como atribuir funções e permissões tooaccounts.
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *endereço ip público*. Quando **endereços IP públicos** aparece nos resultados da pesquisa hello, clique nele.
3. Clique em **+ adicionar** em Olá **endereço IP público** folha que aparece.
4. Insira ou selecione valores para Olá Olá configurações a seguir **criar endereço IP público** folha que aparece, clique **criar**:

    |Configuração|Obrigatório?|Detalhes|
    |---|---|---|
    |Nome|Sim|Olá nome deve ser exclusivo dentro do grupo de recursos de saudação que você selecionar.|
    |Versão IP|Sim| Selecione IPv4 ou IPv6. Enquanto IPv4 público endereços podem ser atribuídas tooseveral recursos do Azure, um endereço IP público do IPv6 somente pode ser atribuído balanceador de carga tooan voltado para a Internet. o balanceador de carga Olá pode balancear cargas de IPv6 tráfego tooAzure virtual máquinas. Saiba mais sobre [máquinas de toovirtual tráfego IPv6 de balanceamento de carga](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
    |Atribuição de endereço IP|Sim|**Dinâmico:** endereços dinâmicos são atribuídos somente depois que o endereço IP público de hello está associado tooa NIC anexado tooa VM e hello VM é iniciada para Olá primeira vez. Os endereços dinâmicos podem alterar se Olá Olá VM NIC é anexado toois parado (desalocado). Olá endereço permanece Olá mesmo se hello VM é reinicializada ou interrompida (mas não desalocada). **Estático:** endereços estáticos são atribuídos ao endereço IP público de saudação é criado. Endereços estáticos do estado de alteração mesmo que se hello VM é colocada em Olá parado (desalocado) não. endereço de saudação somente é liberado quando Olá NIC é excluído. Você pode alterar o método de atribuição de hello depois Olá NIC é criado. Se você selecionar IPv6 para Olá **versão IP**, Olá atribuição disponível somente método é **dinâmico**.|
    |Tempo limite de ociosidade (minutos)|Não|Quantos minutos tookeep abrir uma conexão TCP ou HTTP sem depender de mensagens keep-alive de toosend de clientes. Se você selecionar IPv6 para a **versão IP**, esse valor não poderá ser alterado. |
    |Rótulo do nome DNS|Não|Deve ser exclusivo dentro de saudação do Azure local que você cria o nome da saudação em (em todas as assinaturas e todos os clientes). Olá serviço DNS público do Azure registra automaticamente Olá nome e endereço IP para recursos tooa possa se conectar com o nome da saudação. Azure acrescenta *location.cloudapp.azure.com* (onde o local é o local de saudação você selecionar) o nome de toohello você fornecer toocreate Olá totalmente qualificado nome DNS. Se você escolher toocreate ambas as versões de endereço, hello mesmo nome DNS é atribuído tooboth Olá IPv4 e IPv6. Olá serviço DNS do Azure contém um IPv4 e IPv6 AAAA registros de nome e responde com ambos os registros quando o nome DNS de saudação é pesquisado. Olá cliente pode escolher quais toocommunicate de endereço (IPv4 ou IPv6) com.|
    |Criar um endereço IPv6 (ou IPv4)|Não| O que é exibido, IPv4 ou IPv6, depende do que você seleciona para a **versão IP**. Por exemplo, se você selecionar **IPv4** para a **versão IP**, **IPv6** será exibido aqui.
    |Nome (visível somente se você tiver marcado a saudação **criar um endereço IPv6 (ou IPv4)** caixa de seleção)|Sim, se você selecionar Olá **criar um IPv6** (ou IPv4) caixa de seleção.|Olá nome deve ser diferente do nome de saudação insira para Olá primeiro **nome** nesta lista. Se você escolher toocreate um IPv4 e um endereço IPv6, o portal de saudação cria dois separado públicos recursos de endereço IP, com cada versão do endereço IP atribuído tooit.|
    |Atribuição de endereço IP (visível somente se você tiver marcado a saudação **criar um endereço IPv6 (ou IPv4)** caixa de seleção)|Sim, se você selecionar Olá **criar um IPv6** (ou IPv4) caixa de seleção.|Se a caixa de seleção Olá diz **criar um endereço IPv4**, você pode selecionar um método de atribuição. Se a caixa de seleção Olá diz **criar um endereço IPv6**, não é possível selecionar um método de atribuição, como ele deve ser **dinâmico**.|
    |Assinatura|Sim|Deve existir no hello mesmo [assinatura](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) como recurso Olá deseja tooassociate Olá endereço IP público para.|
    |Grupo de recursos|Sim|Podem existir em Olá igual ou diferente, [grupo de recursos](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) como recurso Olá deseja tooassociate Olá endereço IP público para.|
    |Local|Sim|Deve existir no hello mesmo [local](https://azure.microsoft.com/regions), também chamado tooas região, como recurso Olá deseja tooassociate Olá endereço IP público para.|

**Comandos**

Embora o portal de saudação fornece Olá opção toocreate dois públicos recursos de endereço IP (um IPv4 e um IPv6), Olá comandos CLI e PowerShell a seguir cria um recurso com um endereço para uma versão IP ou hello outros. Se você quiser dois públicos recursos de endereço IP, uma para cada versão IP, você deve executar comando Olá duas vezes, especificando nomes diferentes e versões de recursos de endereço IP públicos hello. 

|Ferramenta|Command|
|---|---|
|CLI|[az network public-ip create](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)|

## <a name="view-change-settings-for-or-delete-a-public-ip-address"></a>Exibir, alterar as configurações ou excluir um endereço IP público

1. Faça logon no toohello [portal do Azure](https://portal.azure.com) com uma conta que é atribuídas (no mínimo) permissões para a função de Colaborador de rede Olá para sua assinatura. Saudação de leitura [funções internas para controle de acesso baseado em função do Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) artigo toolearn mais sobre como atribuir funções e permissões tooaccounts.
2. Na caixa de saudação que contém o texto de saudação *pesquisar recursos* na parte superior de saudação do hello portal do Azure, digite *endereço ip público*. Quando **endereços IP públicos** aparece nos resultados da pesquisa hello, clique nele.
3. Em Olá **endereços IP públicos** folha que aparece, clique em nome de saudação do endereço IP público Olá deseja tooview, alterar configurações ou excluir.
4. Na folha de saudação que aparece para o endereço IP público Olá, complete um dos Olá dependendo se você deseja tooview, as opções a seguir, excluir ou alterar o endereço IP público de saudação.
    - **Exibição**: Olá **visão geral** seção da folha de saudação mostra as configurações de chave para o endereço IP público de Olá, como a interface de rede Olá associado muito (se endereço Olá associado tooa interface de rede). portal Olá não exibir a versão de saudação do endereço da saudação (IPv4 ou IPv6). informações de versão tooview hello, Olá use PowerShell ou CLI comando tooview Olá endereço IP público. Se a versão do endereço IP hello for IPv6, Olá endereço atribuído não é exibida pelo portal hello, PowerShell ou Olá CLI. 
    - **Excluir**: endereço IP público Olá de toodelete, clique em **excluir** em Olá **visão geral** seção da folha de saudação. Se o endereço de saudação configuração de IP tooan atualmente associados, ele não pode ser excluído. Se o endereço de saudação está associado a uma configuração, clique em **desassocie** toodissociate endereço de saudação da configuração de IP hello.
    - **Alterar**: clique em **Configuração**. Alterar as configurações usando as informações de saudação na etapa 4 do hello [criar um endereço IP público](#create-a-public-ip-address) deste artigo. atribuição de saudação toochange para um endereço IPv4 estático toodynamic, primeiro você deve desassociar endereço IPv4 público de saudação da configuração de IP hello que está associada. Você pode alterar Olá atribuição método toodynamic e clique em **associar** tooassociate Olá IP endereço toohello mesmo IP configuração, uma configuração diferente ou você pode deixá-lo dissociada. toodissociate um endereço IP público, no hello **visão geral** seção, clique em **desassocie**.

>[!WARNING]
>Quando você altera o método de atribuição de saudação do toodynamic estático, você perderá o endereço IP de saudação que foi atribuído o endereço IP público de toohello. Enquanto hello Azure servidores DNS públicos mantêm um mapeamento entre endereços estáticos ou dinâmicos e qualquer rótulo de nome DNS (se você definiu um), um endereço IP dinâmico pode alterar quando Olá VM é iniciada no hello parada (desalocado) estado. endereço de saudação tooprevent alterem, atribua um endereço IP estático.

**Comandos**

|Ferramenta|Command|
|---|---|
|CLI|[lista de ip público de rede AZ](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#list) os endereços IP públicos toolist, [az rede public-ip-Mostrar](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooshow configurações; [atualização de ip público de rede az](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#update) tooupdate; [public-ip de rede az excluir](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#delete) toodelete|
|PowerShell|[Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve um IP público endereço objeto e exibir suas configurações, [AzureRmPublicIpAddress conjunto](/powershell/resourcemanager/azurerm.network/set-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooupdate configurações; [AzureRmPublicIpAddress remover](/powershell/module/azurerm.network/remove-azurermpublicipaddress) toodelete|

## <a name="next-steps"></a>Próximas etapas
Atribua endereços IP públicos ao criar hello Azure recursos a seguir:

- Máquinas virtuais [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) ou [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Azure Load Balancer voltado para a Internet](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Application Gateway do Azure](../application-gateway/application-gateway-create-gateway-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Conexão site a site usando um Gateway de VPN do Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Conjunto de Dimensionamento de Máquinas Virtuais do Azure](../virtual-machine-scale-sets/virtual-machine-scale-sets-portal-create.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
