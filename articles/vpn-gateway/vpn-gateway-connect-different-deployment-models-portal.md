---
title: "Conectar redes virtuais clássicas a VNets do Azure Resource Manager: Portal | Microsoft Docs"
description: "Saiba como criar uma conexão VPN entre Rede Virtuais clássicas e Rede Virtuais do Resource Manager usando o Gateway de VPN e o portal"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 5a90498c-4520-4bd3-a833-ad85924ecaf9
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/27/2017
ms.author: cherylmc
ms.openlocfilehash: 8fd058d74d00ecc980d295ee6bd9680ff832f891
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-the-portal"></a>Conectar redes virtuais de diferentes modelos de implantação usando o portal

Este artigo mostra como conectar redes virtuais clássicas para VNets do Gerenciador de recursos para permitir que os recursos localizados nos modelos de implantação separado para se comunicar entre si. As etapas neste artigo usam o PowerShell, mas você também pode criar essa configuração usando o portal do Azure, selecionando o artigo desta lista.

> [!div class="op_single_selector"]
> * [Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

Conectar uma rede virtual clássica a outra rede virtual do Resource Manager é semelhante a conectar uma rede virtual a um site local. Os dois tipos de conectividade usam um gateway de VPN para fornecer um túnel seguro usando IPsec/IKE. Você pode criar uma conexão entre redes virtuais em assinaturas e regiões diferentes. Você também pode conectar redes virtuais que já têm conexões com redes locais, desde que o gateway com o qual foram configuradas seja dinâmico ou baseado em rota. Para saber mais sobre conexões de Rede Virtual a Rede Virtual, consulte as [Perguntas frequentes sobre Rede Virtual para Rede Virtual](#faq) no final deste artigo. 

Se suas redes virtuais estiverem na mesma região, convém considerar conectá-las usando o emparelhamento de redes virtuais. O emparelhamento Vnet não usa um gateway de VPN. Para obter mais informações, consulte [Emparelhamento da VNet](../virtual-network/virtual-network-peering-overview.md). 

### <a name="before"></a>Antes de começar

* Estas etapas pressupõem que ambas as redes virtuais já tenham sido criadas. Se estiver usando este artigo como um exercício e você não possui VNets, há links nas etapas que ajudam a criá-las.
* Verifique se os intervalos de endereços das VNets não se sobrepõem, nem sobrepõem qualquer um dos intervalos para outras conexões às quais os gateways podem estar conectados.
* Instale os cmdlets mais recentes do PowerShell para o Resource Manager e o Gerenciamento de Serviços (clássico). Neste artigo, usamos o portal do Azure e o PowerShell. O PowerShell é necessário para criar a conexão da VNet clássica com a VNet do Resource Manager. Para saber mais, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview): 

### <a name="values"></a>Configurações de exemplo

Você pode usar esses valores para criar um ambiente de teste ou consultá-los para compreender melhor os exemplos neste artigo.

**VNet Clássica**

Nome da VNet = ClassicVNet <br>
Espaço de endereço = 10.0.0.0/24 <br>
Nome da sub-rede = Subnet-1 <br>
Intervalo de endereços da sub-rede: 10.0.0.0/27 <br>
Assinatura = a assinatura que você quer usar <br>
Grupo de Recursos = ClassicRG <br>
Local = Oeste dos EUA <br>
GatewaySubnet = 10.0.0.32/28 <br>
Site local = RMVNetLocal <br>

**VNet do Resource Manager**

Nome da VNet = RMVNet <br>
Espaço de endereço = 192.168.0.0/16 <br>
Grupo de recursos = RG1 <br>
Local = Leste dos EUA <br>
Nome da sub-rede = Subnet-1 <br>
Intervalo de endereços = 192.168.1.0/24 <br>
GatewaySubnet = 192.168.0.0/26 <br>
Nome do gateway de rede virtual = RMGateway <br>
Tipo de gateway = VPN <br>
Tipo de VPN = baseada em rota <br>
SKU = VpnGw1 <br>
Local = Leste dos EUA <br>
Rede virtual = RMVNet <br> (associar o gateway de VPN a essa rede virtual) Configuração do primeiro IP = rmgwpip <br> (endereço IP público do gateway) Gateway de rede local = ClassicVNetLocal <br>
Nome da conexão = RMtoClassic

### <a name="connectoverview"></a>Visão geral da conexão

Para essa configuração, você cria uma conexão de gateway de VPN por um túnel VPN IPsec/IKE entre as redes virtuais. Certifique-se de que os intervalos de VNet não se sobreponham, nem sobreponham nenhuma das redes locais às quais eles se conectam.

A seguinte tabela mostra um exemplo de como as VNets e os sites locais de exemplo são definidos:

| Rede Virtual | Espaço de endereço | Região | Conecta ao site de rede local |
|:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |Oeste dos EUA | RMVNetLocal (192.168.0.0/16) |
| RMVNet | (192.168.0.0/16) |Leste dos EUA |ClassicVNetLocal (10.0.0.0/24) |

## <a name="classicvnet"></a>Seção 1 – Definir as configurações da VNet clássica

Nesta seção, você cria a VNet clássica, a rede local (site local) e o gateway de rede virtual. Capturas de tela são fornecidas como exemplos. Não se esqueça de substituir os valores pelos seus próprios valores ou use os valores de [Exemplo](#values).

### 1. <a name="classicvnet"></a>Criar uma VNet clássica

Caso não tenha uma VNet clássica e esteja executando estas etapas como um exercício, você pode criar uma VNet usando [este artigo](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) e os valores de configurações de [Exemplo](#values) acima.

Caso já tenha uma VNet com um gateway de VPN, verifique se o gateway é Dinâmico. Se ele for Estático, primeiro você deve excluir o gateway de VPN antes de prosseguir para [Configurar o site local](#local).

1. Abra o [portal do Azure](https://ms.portal.azure.com) e entre com sua conta do Azure.
2. Clique em **+ Criar um recurso** para abrir a página 'Novo'.
3. No campo “Pesquisar no Marketplace”, digite “Rede Virtual”. Se você selecionar, em vez disso, Rede -> Rede Virtual, você não terá a opção de criar uma VNet clássica.
4. Localize “Rede Virtual” na lista retornada e clique nela para abrir a página Rede Virtual. 
5. Na página da rede virtual, selecione “Clássica” para criar uma VNet clássica. Se você usar o padrão aqui, acabará com uma rede virtual do Resource Manager.

### 2. <a name="local"></a>Configurar o site local

1. Navegue até **Todos os recursos** e localize **ClassicVNet** na lista.
2. Na página **Visão geral**, na seção **Conexões VPN**, clique em **Gateway** para criar um gateway.
  ![Configurar um gateway de VPN](./media/vpn-gateway-connect-different-deployment-models-portal/gatewaygraphic.png "Configurar um gateway de VPN")
3. Na página **Nova Conexão VPN**, para **Tipo de conexão**, selecione **Site para site**.
4. Em **Site local**, clique em **Definir configurações obrigatórias**. Isso abre a página **Site local**.
5. Na página **Site local**, crie um nome para se referir à VNet do Resource Manager. Por exemplo, "RMVNetLocal".
6. Se o gateway de VPN para a VNet do Resource Manager já tiver um endereço IP público, use o valor do campo **Endereço IP do gateway de VPN**. Se estiver seguindo estas etapas como um exercício ou se ainda não tiver uma gateway de rede virtual para sua VNet do Resource Manager, você poderá criar um endereço IP de espaço reservado. Certifique-se de que o endereço IP de espaço reservado usa um formato válido. Posteriormente, substitua o endereço IP de espaço reservado pelo endereço IP público do gateway de rede virtual do Resource Manager.
7. Para **espaço de endereço de cliente**, use os [valores](#connectoverview) para os espaços de endereço IP de rede virtual para o VNet do Resource Manager. Essa configuração é usada para especificar os espaços de endereço para roteamento até a rede virtual do Resource Manager. No exemplo, usamos 192.168.0.0/16, o intervalo de endereços para a RMVNet.
8. Clique em **OK** para salvar os valores e retornar para a página **Nova conexão VPN**.

### <a name="classicgw"></a>3. Criar o gateway de rede virtual

1. Na página **Nova Conexão VPN**, marque a caixa de seleção **Criar gateway imediatamente**.
2. Clique em **Configuração do gateway opcional** para abrir a página **Configuração do gateway**.

  ![Abrir a página de configuração do gateway](./media/vpn-gateway-connect-different-deployment-models-portal/optionalgatewayconfiguration.png "Abrir a página de configuração de gateway")
3. Clique em **Sub-rede – Configurar as configurações necessárias** para abrir a página **Adicionar sub-rede**. O **Nome** já está configurado com o valor necessário: **GatewaySubnet**.
4. O **intervalo de endereços** refere-se ao intervalo para a sub-rede de gateway. Embora você possa criar uma sub-rede de gateway com um intervalo de endereço /29 (três endereços), aconselhamos a criação de uma sub-rede de gateway que contenha mais endereços IP. Isso acomodará futuras configurações que podem exigir mais endereços IP disponíveis. Se possível, use/27 ou /28. Se estiver usando estas etapas como um exercício, você poderá consultar os [Valores de exemplo](#values). Para este exemplo, vamos usar '10.0.0.32/28'. Clique em **OK** para criar a sub-rede de gateway.
5. Na página **Configuração de Gateway**, **Tamanho** refere-se à SKU de gateway. Selecione o SKU de gateway do seu gateway de VPN.
6. Verifique se o **Tipo de roteamento** é **Dinâmico**, em seguida, clique em **OK** para retornar à página **Nova conexão VPN**.
7. Na página **Nova conexão VPN**, clique em **OK** para começar a criar seu gateway de VPN. A criação de um gateway de VPN pode demorar até 45 minutos para ser concluída.

### <a name="ip"></a>4. Copiar o endereço IP público do gateway de rede virtual

Após a criação do gateway de rede virtual, você pode exibir o endereço IP do gateway. 

1. Navegue até sua rede virtual clássica e clique em **visão geral**.
2. Clique em **Conexões VPN** para abrir a página de conexões VPN. Na página de conexões VPN, você pode exibir o endereço IP público. Esse é o endereço IP público atribuído ao seu gateway de rede virtual. Anote o endereço IP. Você o usará em etapas posteriores quando trabalhar com as definições de configuração do gateway de rede local do Resource Manager. 
3. Você pode exibir o status das conexões do gateway. Observe que o site da rede local criado é listado como 'Conexão'. O status será alterado depois de ter criado as conexões. Você pode fechar esta página quando tiver terminado de exibir o status.

## <a name="rmvnet"></a>Seção 2 – Definir as configurações de VNet do Resource Manager

Nesta seção, você cria o gateway de rede virtual e o gateway de rede local para a VNet do Resource Manager. Capturas de tela são fornecidas como exemplos. Não se esqueça de substituir os valores pelos seus próprios valores ou use os valores de [Exemplo](#values).

### <a name="1-create-a-virtual-network"></a>1. Criar uma rede virtual

**Valores de exemplo:**

* Nome da VNet = RMVNet <br>
* Espaço de endereço = 192.168.0.0/16 <br>
* Grupo de recursos = RG1 <br>
* Local = Leste dos EUA <br>
* Nome da sub-rede = Subnet-1 <br>
* Intervalo de endereços = 192.168.1.0/24 <br>


Caso não tenha uma VNet do Resource Manager e esteja executando estas etapas como um exercício, você poderá criar uma VNet usando [este artigo](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) e os valores do Exemplo.

### <a name="2-create-a-gateway-subnet"></a>2. Criar uma sub-rede de gateway

**Valor de exemplo:** GatewaySubnet = 192.168.0.0/26

Antes de criar um gateway de rede virtual, você precisa primeiro criar a sub-rede de gateway. Criar uma sub-rede de gateway com a contagem CIDR de /28 ou maior (/ 27, / 26 etc.). Se você estiver criando isso como parte de um exercício, poderá usar os Valores de exemplo.

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

### <a name="creategw"></a>3. Criar um gateway de rede virtual

**Valores de exemplo:**

* Nome do gateway de rede virtual = RMGateway <br>
* Tipo de gateway = VPN <br>
* Tipo de VPN = baseada em rota <br>
* SKU = VpnGw1 <br>
* Local = Leste dos EUA <br>
* Rede virtual = RMVNet <br>
* Configuração do primeiro IP = rmgwpip <br>

[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

### <a name="createlng"></a>4. Criar um gateway de rede local

**Valores de exemplo:** Gateway de rede local = ClassicVNetLocal

| Rede Virtual | Espaço de endereço | Região | Conecta ao site de rede local |Endereço IP público do gateway|
|:--- |:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |Oeste dos EUA | RMVNetLocal (192.168.0.0/16) |O endereço IP público que é atribuído ao gateway ClassicVNet|
| RMVNet | (192.168.0.0/16) |Leste dos EUA |ClassicVNetLocal (10.0.0.0/24) |O endereço IP público que é atribuído ao gateway RMVNet.|

O gateway de rede local especifica o intervalo de endereços e o endereço IP público associado à VNet clássica e seu gateway de rede virtual. Se estiver seguindo estas etapas como um exercício, consulte os Valores de exemplo.

[!INCLUDE [vpn-gateway-add-lng-rm-portal](../../includes/vpn-gateway-add-lng-rm-portal-include.md)]

## <a name="modifylng"></a>Seção 3 – Modificar as configurações de site local de VNet clássicas

Nesta seção, você substitui o endereço IP de espaço reservado que usou ao especificar as configurações do site local pelo endereço IP do gateway de VPN do Resource Manager. Esta seção usa os cmdlets do PowerShell (SM) clássicos.

1. No portal do Azure, navegue até a rede virtual clássica.
2. Na página de sua rede virtual, clique em **Visão geral**.
3. No **conexões VPN** seção, clique no nome do seu site local no gráfico.

    ![Conexões VPN](./media/vpn-gateway-connect-different-deployment-models-portal/vpnconnections.png "conexões VPN")
4. Na página **Conexões VPN Site a site**, clique no nome do site.

    ![Nome do site](./media/vpn-gateway-connect-different-deployment-models-portal/sitetosite3.png "nome do site Local")
5. Na página de conexão para seu site local, clique no nome do site local para abrir a página do **Site local**.

    ![Abrir local-site](./media/vpn-gateway-connect-different-deployment-models-portal/openlocal.png "Abrir site local")
6. Na página **Site local**, substitua o **endereço IP do gateway de VPN** pelo endereço IP do gateway do Resource Manager.

    ![Endereço de ip do gateway](./media/vpn-gateway-connect-different-deployment-models-portal/gwipaddress.png "endereço IP do Gateway")
7. Clique em **OK** para atualizar o endereço IP.

## <a name="RMtoclassic"></a>Seção 4 – Criar a conexão do Resource Manager com o clássico

Nestas etapas, você configura a conexão da VNet do Resource Manager com a VNet clássica usando o portal do Azure.

1. Em **Todos os recursos**, localize o gateway de rede local. Em nosso exemplo, o gateway de rede local é **ClassicVNetLocal**.
2. Clique em **Configuração** e verifique se o valor do endereço IP é o gateway de VPN para a VNet clássica. Atualize, se necessário, e clique em **Salvar**. Feche a página.
3. Em **Todos os recursos**, clique no gateway de rede local.
4. Clique em **Conexões** para abrir a página Conexões.
5. Na página **Conexões**, clique em **+** para adicionar uma conexão.
6. Na página **Adicionar conexão**, dê um nome para a conexão. Por exemplo, "RMtoClassic".
7. A opção **Site a Site** já está selecionada nessa página.
8. Selecione o gateway de rede virtual que deseja associar a esse site.
9. Crie uma **chave compartilhada**. Essa chave também é usada na conexão que você cria da VNet clássica com a VNet do Resource Manager. Você pode gerar a chave ou criar uma. Em nosso exemplo, usamos "abc123", mas você pode (e deve) usar algo mais complexo.
10. Clique em **OK** para criar a conexão.

##<a name="classictoRM"></a>Seção 5 – Criar a conexão do clássico com o Resource Manager

Nestas etapas, você configura a conexão da VNet clássica com a VNet do Resource Manager. Essas etapas exigem o PowerShell. Não é possível criar essa conexão no portal. Baixe e instale os cmdlets do PowerShell clássicos (SM) e do Resource Manager (RM).

### <a name="1-connect-to-your-azure-account"></a>1. Conectar-se à sua conta do Azure

Abra o console do PowerShell com direitos elevados e faça logon em sua conta do Azure. O cmdlet a seguir solicita as credenciais de logon para sua conta do Azure. Depois de entrar, as configurações da conta são baixadas para que estejam disponíveis para o Azure PowerShell.

```powershell
Login-AzureRmAccount
```
   
Obtenha uma lista de suas assinaturas do Azure, se você tiver mais de uma assinatura.

```powershell
Get-AzureRmSubscription
```

Especifique a assinatura que você quer usar. 

```powershell
Select-AzureRmSubscription -SubscriptionName "Name of subscription"
```

Adicione sua Conta do Azure para usar os cmdlets do PowerShell clássicos. Para fazer isso, use o seguinte comando:

```powershell
Add-AzureAccount
```

### <a name="2-view-the-network-configuration-file-values"></a>2. Exibir os valores do arquivo de configuração de rede

Quando você cria uma rede virtual no portal do Azure, o nome completo que o Azure usa não fica visível no portal do Azure. Por exemplo, uma VNet que pareça se chamar "ClassicVNet" no portal do Azure pode ter um nome muito mais longo no arquivo de configuração de rede. O nome pode ser algo parecido com "Grupo ClassicRG ClassicVNet". Nestas etapas, você baixa o arquivo de configuração de rede e exibe os valores.

Crie um diretório em seu computador e exporte o arquivo de configuração de rede para o diretório. Neste exemplo, o arquivo de configuração de rede é exportado para C:\AzureNet.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

Abra o arquivo com um editor de texto e exiba o nome da rede virtual clássica. Use os nomes no arquivo de configuração de rede ao executar os cmdlets do PowerShell.

- Os nomes de VNet são listados como **VirtualNetworkSite name =**
- Os nomes de Site são listados como **LocalNetworkSite name =**

### <a name="3-create-the-connection"></a>3. Criar a conexão

Defina a chave compartilhada e crie a conexão da VNet clássica com a VNet do Resource Manager. Não é possível definir a chave compartilhada usando o portal. Certifique-se de que executar essas etapas enquanto estiver conectado usando a versão clássica dos cmdlets do PowerShell. Para fazer isso, use **Add-AzureAccount**. Caso contrário, você não poderá definir o '-AzureVNetGatewayKey'.

- Neste exemplo, **-VNetName** é o nome da VNet clássica como encontrado no arquivo de configuração de rede. 
- O **-LocalNetworkSiteName** é o nome que você especificou para o site local, como encontrado no arquivo de configuração de rede.
- O **-SharedKey** é um valor que você gera e especifica. Neste exemplo, usamos *abc123*, mas você pode gerar algo mais complexo. O importante é que o valor que você especifica aqui deve ser o mesmo valor que especificou ao criar a conexão do Resource Manager com o clássico.

```powershell
Set-AzureVNetGatewayKey -VNetName "Group ClassicRG ClassicVNet" `
-LocalNetworkSiteName "172B9E16_RMVNetLocal" -SharedKey abc123
```

##<a name="verify"></a>Seção 6 – Verificar suas conexões

Você pode verificar a conexão usando o portal do Azure ou o PowerShell. Ao verificar, talvez seja necessário aguardar um minuto ou dois como a conexão está sendo criado. Quando uma conexão é bem-sucedida, o estado da conectividade muda de "Conectando" para "Conectado".

### <a name="to-verify-the-connection-from-your-classic-vnet-to-your-resource-manager-vnet"></a>Para verificar a conexão de sua VNET clássica para sua VNET do Resource Manager

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

###<a name="to-verify-the-connection-from-your-resource-manager-vnet-to-your-classic-vnet"></a>Para verificar a conexão de seu VNET do Resource Manager para sua rede virtual clássica

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>Perguntas frequentes sobre Rede Virtual para Rede Virtual

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-faq-vnet-vnet-include.md)]
