---
title: "Criar uma conexão entre redes virtuais: clássico: portal do Azure | Microsoft Docs"
description: "Como tooconnect virtuais do Azure redes juntos usando o PowerShell e Olá portal clássico do Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: f29c3c091d049ff96cf59f4c28ab86a100bcb5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-connection-classic"></a>Configurar uma conexão entre redes virtuais (clássico)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Este artigo mostra como toocreate uma conexão de gateway VPN entre redes virtuais. Olá redes virtuais podem ser Olá mesmas ou em diferentes regiões e de Olá mesmo ou em assinaturas diferentes. Olá etapas neste artigo se aplicam a toohello modelo de implantação clássico e hello portal do Azure. Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [CLI do Azure](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Conectar modelos de implantação diferentes – portal do Azure](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Conectar modelos de implantação diferentes - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![Rede virtual tooVNet diagrama de conectividade](./media/vpn-gateway-howto-vnet-vnet-portal-classic/v2vclassic.png)

## <a name="about-vnet-to-vnet-connections"></a>Sobre conexões de rede virtual a rede virtual

Conectar-se a uma rede virtual tooanother VPN (rede virtual a rede) no modelo de implantação clássico hello usando um gateway VPN é semelhante tooconnecting uma rede virtual tooan no site local. Ambos os tipos de conectividade usam um gateway VPN tooprovide um túnel seguro usando IPsec/IKE.

Olá VNets que você conecta pode estar em diferentes assinaturas e regiões diferentes. Você pode combinar a comunicação VNet tooVNet com configurações de vários locais. Isso permite estabelecer topologias de rede que combinam conectividade entre instalações a conectividade de rede intervirtual.

![Rede virtual tooVNet conexões](./media/vpn-gateway-howto-vnet-vnet-portal-classic/aboutconnections.png)

### <a name="why"></a>Por que conectar redes virtuais?

Você talvez queira redes virtuais tooconnect para Olá motivos a seguir:

* **Redundância geográfica entre regiões e presença geográfica**

  * Você pode configurar sua própria sincronização ou replicação geográfica com conectividade segura sem passar por pontos de extremidade voltados para a Internet.
  * Com o Azure Load Balancer e a tecnologia de clustering da Microsoft ou de terceiros, você pode configurar uma carga de trabalho altamente disponível com redundância geográfica entre várias regiões do Azure. Um exemplo importante é tooset backup SQL Always On com grupos de disponibilidade espalhados por várias regiões do Azure.
* **Aplicativos multicamadas regionais com limite de isolamento forte**

  * Olá na mesma região, você pode configurar aplicações multicamadas com múltiplas VNets conectado com isolamento forte e comunicação entre camadas segura.
* **Comunicação entre organizações e assinaturas no Azure**

  * Se você tem várias assinaturas do Azure, agora é possível se conectar a cargas de trabalho de assinaturas diferentes com segurança entre redes virtuais.
  * Para empresas ou provedores de serviço, é possível habilitar a comunicação entre organizações usando a tecnologia VPN segura no Azure.

Para obter mais informações sobre conexões de rede virtual a rede, consulte [VNet para VNet considerações](#faq) final Olá deste artigo.

### <a name="before-you-begin"></a>Antes de começar

Antes de iniciar este exercício, baixe e instale a versão mais recente de saudação do hello cmdlets do PowerShell de gerenciamento de serviço do Azure (SM). Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). Podemos usar o portal de saudação para a maioria das etapas de saudação, mas é necessário usar PowerShell toocreate Olá conexões entre hello VNets. Não é possível criar conexões hello usando Olá portal do Azure.

## <a name="plan"></a>Etapa 1 – Planejar os intervalos de endereços IP

É importante toodecide intervalos de saudação que você usará tooconfigure suas redes virtuais. Para essa configuração, você deve garantir que nenhum dos intervalos de rede virtual se sobreponham entre si ou com qualquer uma das redes de local de saudação que se conectam ao.

Olá, tabela a seguir mostra um exemplo de como toodefine seus VNets. Use os intervalos de saudação apenas como uma diretriz. Anote os intervalos de saudação para suas redes virtuais. Você precisa dessas informações para etapas posteriores.

**Exemplo**

| Rede Virtual | Espaço de endereço | Região | Conecta-se o site de rede toolocal |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |Leste dos EUA |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |Oeste dos EUA |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

## <a name="vnetvalues"></a>Etapa 2: criar hello redes virtuais

Criar duas redes virtuais no hello [portal do Azure](https://portal.azure.com). Para redes virtuais clássicas do toocreate as etapas hello, consulte [criar uma rede virtual clássica](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). 

Ao usar o hello portal toocreate uma rede virtual clássica, você deve navegar toohello folha de rede virtual usando Olá seguir etapas, caso contrário, Olá opção toocreate uma rede virtual clássica não aparece:

1. Clique em Olá folha de 'New' de saudação tooopen '+'.
2. No campo de 'Marketplace de saudação de pesquisa' hello, digite 'Rede Virtual'. Se você selecionar em vez disso, a rede -> Rede Virtual, você não obterá Olá opção toocreate uma rede virtual clássica.
3. Localize 'Rede Virtual' de saudação retornada da lista e clique em folha de rede Virtual Olá tooopen. 
4. Na folha de rede virtual hello, selecione uma rede virtual clássica de toocreate 'Clássico'. 

Se você estiver usando este artigo como um exercício, você pode usar o hello valores de exemplo a seguir:

**Valores para TestVNet1**

Nome: TestVNet1<br>
Espaço de endereço: 10.11.0.0/16, 10.12.0.0/16 (opcional)<br>
Nome da sub-rede: padrão<br>
Intervalo de endereços da sub-rede: 10.11.0.1/24<br>
Grupo de recursos: ClassicRG<br>
Local: Leste dos EUA<br>
GatewaySubnet: 10.11.1.0/27

**Valores para TestVNet4**

Nome: TestVNet4<br>
Espaço de endereço: 10.41.0.0/16, 10.42.0.0/16 (opcional)<br>
Nome da sub-rede: padrão<br>
Intervalo de endereços da sub-rede: 10.41.0.1/24<br>
Grupo de recursos: ClassicRG<br>
Local: Oeste dos EUA<br>
GatewaySubnet: 10.41.1.0/27

**Ao criar seus VNets, lembre-Olá se as configurações a seguir:**

* **Espaços de endereço de rede virtual** – na página de espaços de endereço de rede Virtual hello, especifique Olá intervalo de endereços que você deseja toouse para sua rede virtual. Esses são os endereços IP dinâmicos Olá que serão atribuídos toohello VMs e outras instâncias de função que você implantar a rede virtual toothis.<br>endereço de saudação espaços que você selecionar não podem se sobrepor com espaços de endereço Olá para qualquer um dos Olá outros locais VNets locais ou na qual esta rede será conectado.

* **Local** – ao criar uma rede virtual, você a associa a um local do Azure (região). Por exemplo, se você quiser que suas VMs que são implantados toobe de rede virtual tooyour fisicamente localizado no Oeste dos EUA, selecione esse local. Você não pode alterar o local de saudação associado à sua rede virtual depois de criá-lo.

**Depois de criar seus VNets, você pode adicionar Olá configurações a seguir:**

* **Espaço de endereço** – o espaço de endereço adicional não é necessário para essa configuração, mas você pode adicionar espaço de endereço adicionais depois de criar hello VNet.

* **Subredes** – subredes adicionais não são necessários para essa configuração, mas talvez você queira toohave suas VMs em uma sub-rede separada de outras instâncias de função.

* **Servidores DNS** – insira o nome do servidor DNS hello e endereço IP. Essa configuração não cria um servidor DNS. Ele permite que os servidores toospecify Olá DNS que você deseja toouse para resolução de nome para essa rede virtual.

Nesta seção, você configurar o tipo de conexão hello, site local do hello e criar gateway hello.

## <a name="localsite"></a>Etapa 3 – configurar o site local Olá

Configurações do Azure usa Olá especificado em cada toodetermine do site de rede local como tooroute tráfego entre hello VNets. Cada rede virtual deve apontar toohello respectiva rede local que você deseja que o tráfego de tooroute. Determinar o nome hello você deseja que o site de rede local toouse toorefer tooeach. É melhor toouse algo descritivo.

Por exemplo, TestVNet1 conecta tooa site de rede local que você criar chamado 'VNet4Local'. configurações de saudação para VNet4Local contêm prefixos de endereço Olá para TestVNet4.

Olá local do site para cada rede virtual é Olá outras redes. Olá valores de exemplo a seguir é usada para a configuração:

| Rede Virtual | Espaço de endereço | Região | Conecta-se o site de rede toolocal |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |Leste dos EUA |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |Oeste dos EUA |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

1. Localize TestVNet1 no hello portal do Azure. Em Olá **conexões VPN** seção da folha de saudação, clique em **Gateway**.

    ![Sem gateway](./media/vpn-gateway-howto-vnet-vnet-portal-classic/nogateway.png)
2. Em Olá **nova Conexão de VPN** página, selecione **Site a Site**.
3. Clique em **site Local** tooopen Olá página do site Local e definir configurações de saudação.
4. Em Olá **site Local** de página, o nome do seu site local. Em nosso exemplo, podemos nomear site local Olá 'VNet4Local'.
5. Para **Endereço IP do gateway de VPN**, você pode usar qualquer endereço IP desejado, desde que ele esteja em um formato válido. Normalmente, você usaria real endereço IP externo Olá para um dispositivo VPN. Mas, para uma configuração de VNet para VNet clássica, você usar o endereço IP público Olá atribuído toohello gateway para sua rede virtual. Considerando que você ainda não criou gateway de rede virtual hello, você especificar qualquer endereço IP público válido como um espaço reservado.<br>Não deixe em branco. Não é opcional para essa configuração. Em uma etapa posterior, volte para essas configurações e configurá-los com endereços IP de gateway de rede virtual correspondentes de saudação depois que o Azure gerá-los.
6. Para **espaço de endereço de cliente**, usar o espaço de endereço de saudação do hello outras redes. Consulte tooyour planejamento de exemplo. Clique em **Okey** toosave suas configurações e retorno toohello back **nova Conexão de VPN** folha.

    ![site local](./media/vpn-gateway-howto-vnet-vnet-portal-classic/localsite.png)

## <a name="gw"></a>Etapa 4 - criar o gateway de rede virtual Olá

Cada rede virtual deve ter um gateway de rede virtual. Olá rotas de gateway de rede virtual e criptografa o tráfego.

1. Em Olá **nova Conexão de VPN** folha, a caixa de seleção select Olá **criar gateway imediatamente**.
2. Clique em **Sub-rede, tamanho e tipo de roteamento**. Em Olá **configuração de Gateway** folha, clique em **sub-rede**.
3. nome de sub-rede de gateway Olá é preenchido automaticamente com nome necessário de saudação 'GatewaySubnet'. Olá **um intervalo de endereços** contém endereços IP hello alocados toohello serviços de gateway VPN. Algumas configurações permitem uma sub-rede do gateway de /29, mas é melhor toouse um /28 ou /27 tooaccommodate configurações futuras que podem exigir mais endereços IP para os serviços de gateway de saudação. Em nossas configurações de exemplo, usamos 10.11.1.0/27. Ajustar o espaço de endereço de saudação, clique em **Okey**.
4. Configurar Olá **tamanho Gateway**. Essa configuração se refere a toohello [SKU de Gateway](vpn-gateway-about-vpn-gateway-settings.md#gwsku).
5. Configurar Olá **tipo de roteamento**. Olá tipo de roteamento para essa configuração deve ser **dinâmico**. Você não pode alterar o tipo de roteamento hello mais tarde, a menos que você subdividir gateway hello e cria um novo.
6. Clique em **OK**.
7. Em Olá **nova Conexão de VPN** folha, clique em **Okey** toobegin criando Olá gateway de rede virtual. Criar um gateway pode levar até 45 minutos ou mais, dependendo da SKU do gateway Olá selecionado.

## <a name="vnet4settings"></a>Etapa 5 – Definir as configurações de TestVNet4

Repita as etapas de saudação muito[criar um site local](#localsite) e [criar gateway de rede virtual Olá](#gw) tooconfigure TestVNet4, substituindo valores hello quando necessário. Se você estiver fazendo isso como um exercício, use Olá [valores de exemplo](#vnetvalues).

## <a name="updatelocal"></a>Etapa 6 - sites locais de saudação de atualização

Depois que seus gateways de rede virtual foram criadas para ambos os VNets, você deve ajustar sites locais Olá **endereço IP do gateway VPN** valores.

|Nome da VNet|Site conectado|Endereço IP do gateway|
|:--- |:--- |:--- |
|TestVNet1|VNet4Local|Endereço IP do gateway de VPN para TestVNet4|
|TestVNet4|VNet1Local|Endereço IP do gateway de VPN para TestVNet1|

### <a name="part-1---get-hello-virtual-network-gateway-public-ip-address"></a>Parte 1 - Get hello rede virtual público endereço IP do gateway

1. Localize sua rede virtual no hello portal do Azure.
2. Clique em Olá tooopen VNet **visão geral** folha. Na folha de saudação em **conexões VPN**, você pode exibir o endereço IP de saudação do seu gateway de rede virtual.

  ![IP público](./media/vpn-gateway-howto-vnet-vnet-portal-classic/publicIP.png)
3. Copie o endereço IP hello. Você o usará na próxima seção, Olá.
4. Repita essas etapas para TestVNet4

### <a name="part-2---modify-hello-local-sites"></a>Parte 2 - modificar sites locais Olá

1. Localize sua rede virtual no hello portal do Azure.
2. Em redes de saudação **visão geral** folha, clique em site local hello.

  ![Site local criado](./media/vpn-gateway-howto-vnet-vnet-portal-classic/local.png)
3. Em Olá **conexões VPN Site a Site** folha, clique em nome de saudação do site local do hello que você deseja toomodify.

  ![Abrir site local](./media/vpn-gateway-howto-vnet-vnet-portal-classic/openlocal.png)
4. Clique em Olá **site Local** que você deseja toomodify.

  ![modificar site](./media/vpn-gateway-howto-vnet-vnet-portal-classic/connections.png)
5. Saudação de atualização **endereço IP do gateway VPN** e clique em **Okey** toosave configurações de saudação.

  ![IP do gateway](./media/vpn-gateway-howto-vnet-vnet-portal-classic/gwupdate.png)
6. Olá feche outros folhas.
7. Repita essas etapas para TestVNet4.

## <a name="getvalues"></a>Etapa 7 - recuperar os valores do arquivo de configuração de rede Olá

Quando você cria VNets clássico no hello portal do Azure, nome de saudação que você exibir não é nome completo de saudação que você usa para o PowerShell. Por exemplo, uma rede virtual que aparece toobe chamado **TestVNet1** no portal de hello, pode ter um nome muito mais no arquivo de configuração de rede hello. Olá nome pode ter esta aparência: **grupo ClassicRG TestVNet1**. Quando você cria suas conexões, é valores de saudação toouse importante que você vê no arquivo de configuração de rede hello.

No hello etapas a seguir, você se conectará tooyour conta do Azure e baixar e exibir valores de Olá Olá de tooobtain de arquivo de configuração de rede que são necessários para as conexões.

1. Baixe e instale a versão mais recente de saudação do hello cmdlets do PowerShell de gerenciamento de serviço do Azure (SM). Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

2. Abra o console do PowerShell com direitos elevados e conecte-se a conta de tooyour. Use Olá toohelp de exemplo que você se conectar a seguir:

  ```powershell
  Login-AzureRmAccount
  ```

  Verificar as assinaturas de saudação para conta de saudação.

  ```powershell
  Get-AzureRmSubscription
  ```

  Se você tiver mais de uma assinatura, selecione a assinatura de saudação que você deseja toouse.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

  Em seguida, use Olá tooadd cmdlet a seguir tooPowerShell sua assinatura do Azure para o modelo de implantação clássico hello.

  ```powershell
  Add-AzureAccount
  ```
3. Exportar e exibir o arquivo de configuração de rede hello. Crie um diretório no seu computador e, em seguida, exportar diretório toohello de arquivo de configuração do hello rede. Neste exemplo, o arquivo de configuração de rede Olá é exportado muito**C:\AzureNet**.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
4. Abra o arquivo de saudação com um editor e exibição Olá nomes de texto para seus sites e VNets. Esses serão nome hello usado quando você cria suas conexões.<br>Os nomes de VNet são listados como **VirtualNetworkSite name =**<br>Os nomes de site são listados como **LocalNetworkSiteRef name =**

## <a name="createconnections"></a>Etapa 8 — criar hello conexões de gateway VPN

Quando todas as etapas anteriores de saudação tiverem sido concluídas, você pode definir chaves pré-compartilhadas de IPsec/IKE hello e criar conexão hello. Esse conjunto de etapas usa o PowerShell. Não podem ser configuradas conexões VNet para VNet para o modelo de implantação clássico Olá Olá portal do Azure.

Exemplos de hello, observe que Olá chave compartilhada é exatamente Olá mesmo. chave compartilhada Olá deve sempre corresponder. Ser tooreplace se valores hello nesses exemplos com nomes exatos de saudação para seus VNets e Sites de rede Local.

1. Crie conexão de tooTestVNet4 TestVNet1 hello.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet1' `
  -LocalNetworkSiteName '17BE5E2C_VNet4Local' -SharedKey A1b2C3D4
  ```
2. Crie conexão de tooTestVNet1 TestVNet4 hello.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet4' `
  -LocalNetworkSiteName 'F7F7BFC7_VNet1Local' -SharedKey A1b2C3D4
  ```
3. Aguarde Olá conexões tooinitialize. Depois de saudação gateway for inicializado, Olá Status é 'Êxito'.

  ```
  Error          :
  HttpStatusCode : OK
  Id             :
  Status         : Successful
  RequestId      :
  StatusCode     : OK
  ```

## <a name="faq"></a>Considerações de VNet a VNet para VNets clássicas
* redes virtuais Olá podem estar em Olá iguais ou diferentes assinaturas.
* redes virtuais Olá podem estar em Olá mesmas ou em diferentes regiões do Azure (locais).
* Um serviço de nuvem ou um ponto de extremidade de balanceamento de carga não pode abranger redes virtuais, mesmo que elas estejam conectadas entre si.
* A conexão de várias redes virtuais entre si não exige nenhum dispositivo VPN.
* O recurso VNet a VNet dá suporte à conexão de Redes Virtuais do Azure. Não dá suporte a conexão de máquinas virtuais ou serviços de nuvem que não são implantados rede virtual tooa.
* VNet a VNet requer gateways de roteamento dinâmico. Não há suporte para gateways de roteamento estático do Azure.
* A conectividade de rede virtual pode ser usada simultaneamente com VPNs de multissite. Há um máximo de 10 túneis VPN para um gateway VPN de rede virtual conectando tooeither outras redes virtuais ou sites locais.
* Olá espaços de endereço de redes virtuais hello e sites de rede local não devem se sobrepor ao local. Espaços de endereço sobrepostos causarão Olá na criação de redes virtuais ou carregar toofail de arquivos de configuração netcfg.
* Não há suporte a túneis redundantes entre um par de redes virtuais.
* Todos os túneis de VPN para Olá VNet, incluindo VPNs P2S, compartilham a largura de banda disponível para o gateway VPN Olá Olá e Olá mesmo SLA de tempo de atividade de gateway VPN no Azure.
* Tráfego de rede virtual a rede percorrem Olá backbone do Azure.

## <a name="next-steps"></a>Próximas etapas
Verifique as conexões. Confira [Verificar uma conexão de Gateway de VPN](vpn-gateway-verify-connection-resource-manager.md).
