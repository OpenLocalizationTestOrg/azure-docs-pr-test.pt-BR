---
title: "Conectar redes virtuais clássicas tooAzure VNets Gerenciador de recursos: Portal | Microsoft Docs"
description: "Saiba como toocreate uma conexão VPN entre clássico VNets e VNets Gerenciador de recursos usando o Gateway de VPN e o portal de saudação"
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
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: bef63b4e829335b2e1a9434a35ebfe33b4fd7373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-hello-portal"></a>Conectar redes virtuais de diferentes modelos de implantação usando o portal de saudação

Este artigo mostra como tooconnect de clássico VNets tooResource tooallow Manager VNets Olá recursos localizados em toocommunicate de modelos de implantação separado Olá entre si. etapas Olá neste artigo usam principalmente Olá portal do Azure, mas você também pode criar essa configuração usando Olá PowerShell selecionando artigo Olá desta lista.

> [!div class="op_single_selector"]
> * [Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

Conectar um tooa de rede virtual clássica VNet Gerenciador de recursos é semelhante tooconnecting uma VNet tooan no site local. Ambos os tipos de conectividade usam um gateway VPN tooprovide um túnel seguro usando IPsec/IKE. Você pode criar uma conexão entre redes virtuais em assinaturas e regiões diferentes. Você também pode conectar VNets que já têm redes de tooon locais de conexões, como gateway Olá que eles foram configurados com é dinâmica ou baseadas em rota. Para obter mais informações sobre conexões de rede virtual a rede, consulte Olá [perguntas Frequentes de VNet para VNet](#faq) final Olá deste artigo. 

Se seus VNets estão em Olá mesma região, talvez você queira tooinstead considere conectá-los usando o emparelhamento de rede virtual. O emparelhamento Vnet não usa um gateway de VPN. Para obter mais informações, consulte [Emparelhamento da VNet](../virtual-network/virtual-network-peering-overview.md). 

### <a name="prerequisites"></a>Pré-requisitos

* Estas etapas pressupõem que ambas as redes virtuais já tenham sido criadas. Se você estiver usando este artigo como um exercício e não tem VNets, há links no hello etapas toohelp criá-los.
* Verifique se a intervalos de endereços de saudação para Olá que vnets não se sobrepõem uns com os outros, ou intervalos de sobreposição com qualquer Olá para outras conexões que Olá gateways podem estar conectados ao.
* Instale cmdlets do PowerShell mais recente Olá para o Gerenciador de recursos e o gerenciamento de serviço (clássico). Neste artigo, usamos Olá portal do Azure e o PowerShell. O PowerShell é necessário toocreate Olá conexão de toohello de rede virtual clássica Olá VNet Gerenciador de recursos. Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). 

### <a name="values"></a>Configurações de exemplo

Você pode usar esses valores toocreate um ambiente de teste, ou consulte toothem toobetter entender exemplos Olá neste artigo.

**VNet Clássica**

Nome da VNet = ClassicVNet <br>
Espaço de endereço = 10.0.0.0/24 <br>
Subnet-1 = 10.0.0.0/27 <br>
Grupo de Recursos = ClassicRG <br>
Local = Oeste dos EUA <br>
GatewaySubnet = 10.0.0.32/28 <br>
Site local = RMVNetLocal <br>

**VNet do Resource Manager**

Nome da VNet = RMVNet <br>
Espaço de endereço = 192.168.0.0/16 <br>
Subnet-1 = 192.168.1.0/24 <br>
GatewaySubnet = 192.168.0.0/26 <br>
Grupo de recursos = RG1 <br>
Local = Leste dos EUA <br>
Nome do gateway de rede virtual = RMGateway <br>
Tipo de gateway = VPN <br>
Tipo de VPN = baseada em rota <br>
Nome do endereço IP público do gateway = rmgwpip <br>
Gateway de rede local = ClassicVNetLocal <br>
Nome da conexão = RMtoClassic

### <a name="connection-overview"></a>Visão geral da conexão

Para essa configuração, você pode criar uma conexão de gateway VPN por um túnel VPN IPsec/IKE entre redes virtuais hello. Certifique-se de que nenhum dos intervalos de rede virtual se sobreponham entre si ou com qualquer uma das redes de local de saudação que se conectam ao.

Olá tabela a seguir mostra um exemplo de como o exemplo hello VNets e sites locais são definidos:

| Rede Virtual | Espaço de endereço | Região | Conecta-se o site de rede toolocal |
|:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |Oeste dos EUA | RMVNetLocal (192.168.0.0/16) |
| RMVNet | (192.168.0.0/16) |Leste dos EUA |ClassicVNetLocal (10.0.0.0/24) |

## <a name="classicvnet"></a>1. Definir configurações de rede virtual clássicas Olá

Nesta seção, você cria Olá local (site local) da rede e o gateway de rede virtual Olá para a sua rede virtual clássica. Se você não tiver uma rede virtual clássica e estiver executando essas etapas como um exercício, você pode criar uma rede virtual usando [neste artigo](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) e hello [exemplo](#values) valores de configurações acima.

Ao usar o hello portal toocreate uma rede virtual clássica, você deve navegar toohello folha de rede virtual usando Olá seguir etapas, caso contrário, Olá opção toocreate uma rede virtual clássica não aparece:

1. Clique em Olá folha de 'New' de saudação tooopen '+'.
2. No campo de 'Marketplace de saudação de pesquisa' hello, digite 'Rede Virtual'. Se você selecionar em vez disso, a rede -> Rede Virtual, você não obterá Olá opção toocreate uma rede virtual clássica.
3. Localize 'Rede Virtual' de saudação retornada da lista e clique em folha de rede Virtual Olá tooopen. 
4. Na folha de rede virtual hello, selecione uma rede virtual clássica de toocreate 'Clássico'. 

Se você já tiver uma rede virtual com um gateway VPN, verifique se o que gateway Olá é dinâmico. Se ele for estático, primeiro deve excluir o gateway VPN hello e continuar.

Capturas de tela são fornecidas como exemplos. Ser tooreplace-se de que os valores hello com seu próprio ou usar Olá [exemplo](#values) valores.

### <a name="part-1---configure-hello-local-site"></a>Parte 1 - Configure o site local Olá

Olá abrir [portal do Azure](https://ms.portal.azure.com) e entre com sua conta do Azure.

1. Navegue muito**todos os recursos** e localize Olá **ClassicVNet** na lista de saudação.
2. Em Olá **visão geral** folha em Olá **conexões VPN** seção, clique em Olá **Gateway** toocreate gráfico um gateway.

    ![Configurar um gateway de VPN](./media/vpn-gateway-connect-different-deployment-models-portal/gatewaygraphic.png "Configurar um gateway de VPN")
3. Em Olá **nova Conexão de VPN** folha, para **o tipo de Conexão**, selecione **Site a site**.
4. Em **Site local**, clique em **Definir configurações obrigatórias**. Isso abre o hello **site Local** folha.
5. Em Olá **site Local** folha, criar um toohello de toorefer nome VNet Gerenciador de recursos. Por exemplo, "RMVNetLocal".
6. Se o gateway VPN Olá para Olá VNet Gerenciador de recursos já tem um endereço IP público, use o valor de saudação para Olá **endereço IP do gateway VPN** campo. Se estiver seguindo estas etapas como um exercício ou se ainda não tiver uma gateway de rede virtual para sua VNet do Resource Manager, você poderá criar um endereço IP de espaço reservado. Certifique-se de que o endereço IP de espaço reservado Olá usa um formato válido. Posteriormente, você substituir o endereço IP de espaço reservado de saudação com endereço IP público do gateway de rede virtual do Gerenciador de recursos de saudação do hello.
7. Para **espaço de endereço de cliente**, use valores de saudação para espaços de endereço IP de rede virtual de saudação para Olá VNet Gerenciador de recursos. Essa configuração é toospecify usado Olá endereço espaços tooroute toohello Gerenciador de recursos rede virtual.
8. Clique em **Okey** toosave Olá valores e retornar toohello **nova Conexão de VPN** folha.

### <a name="part-2---create-hello-virtual-network-gateway"></a>Parte 2 - criar o gateway de rede virtual Olá

1. Em Olá **nova Conexão de VPN** folha, selecione Olá **criar gateway imediatamente** caixa de seleção e clique em **configuração de gateway opcional** tooopen Olá  **Configuração de gateway** folha. 

    ![Folha de configuração do gateway abra](./media/vpn-gateway-connect-different-deployment-models-portal/optionalgatewayconfiguration.png "folha de configuração de gateway aberto")
2. Clique em **Subnet - definir configurações obrigatórias** tooopen Olá **Adicionar sub-rede** folha. Olá **nome** já está configurado com o valor de saudação necessária **GatewaySubnet**.
3. Olá **um intervalo de endereços** refere-se toohello intervalo para a sub-rede de gateway hello. Embora você possa criar uma sub-rede de gateway com um intervalo de endereço /29 (três endereços), aconselhamos a criação de uma sub-rede de gateway que contenha mais endereços IP. Isso acomodará futuras configurações que podem exigir mais endereços IP disponíveis. Se possível, use/27 ou /28. Se você estiver usando estas etapas como um exercício, você pode consultar toohello [exemplo](#values) valores. Clique em **Okey** toocreate Olá gateway de sub-rede.
4. Em Olá **configuração de Gateway** folha, **tamanho** refere-se toohello SKU do gateway. Selecione o SKU do gateway de saudação do seu gateway VPN.
5. Verificar Olá **tipo de roteamento** é **dinâmico**, em seguida, clique em **Okey** tooreturn toohello **nova Conexão de VPN** folha.
6. Em Olá **nova Conexão de VPN** folha, clique em **Okey** toobegin criando seu gateway de VPN. Criar um gateway VPN pode demorar até too45 toocomplete de minutos.

### <a name="ip"></a>Parte 3 - gateway de rede virtual cópia Olá endereço IP público

Depois que o gateway de rede virtual Olá tiver sido criado, você pode exibir o endereço IP do gateway de saudação. 

1. Navegue tooyour clássico VNet e clique em **visão geral**.
2. Clique em **conexões VPN** tooopen folha de conexões de VPN de saudação. Na folha de conexões de VPN hello, você pode exibir o endereço IP público de saudação. Este é o endereço IP público de saudação atribuído tooyour gateway de rede virtual. 
3. Anote ou copie o endereço IP hello. Você o usará em etapas posteriores quando trabalhar com as definições de configuração do gateway de rede local do Resource Manager. Você também pode exibir o status de saudação de suas conexões de gateway. Site da rede local Olá aviso criado é listado como 'Conexão'. status de saudação será alterado depois que você criou suas conexões.
4. Feche a folha de saudação depois de copiar o endereço IP do gateway de saudação.

## <a name="rmvnet"></a>2. Definir configurações de redes do Gerenciador de recursos de saudação

Nesta seção, você cria o gateway de rede virtual hello e gateway de rede local Olá para VNet do Gerenciador de recursos. Se você não tem um Gerenciador de recursos de VNet e estiver executando essas etapas como um exercício, você pode criar uma rede virtual usando [neste artigo](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) e hello [exemplo](#values) valores de configurações acima.

Capturas de tela são fornecidas como exemplos. Ser tooreplace-se de que os valores hello com seu próprio ou usar Olá [exemplo](#values) valores.

### <a name="part-1---create-a-gateway-subnet"></a>Parte 1 - Criar uma sub-rede de gateway

Antes de criar um gateway de rede virtual, é necessário primeiro toocreate Olá gateway de sub-rede. Criar uma sub-rede de gateway com a contagem CIDR de /28 ou maior. (/ 27, / 26, etc.)

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

### <a name="part-2---create-a-virtual-network-gateway"></a>Parte 2 - Criar um gateway de Rede Virtual

[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

### <a name="createlng"></a>Parte 3 - Criar um gateway de rede local

gateway de rede local Olá Especifica o intervalo de endereços de saudação e o endereço IP público de saudação associado à sua VNet clássico e o gateway de rede virtual.

Se você estiver fazendo o seguinte como um exercício, consulte as configurações de toothese:

| Rede Virtual | Espaço de endereço | Região | Conecta-se o site de rede toolocal |Endereço IP público do gateway|
|:--- |:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |Oeste dos EUA | RMVNetLocal (192.168.0.0/16) |Olá endereço IP público atribuído toohello ClassicVNet gateway|
| RMVNet | (192.168.0.0/16) |Leste dos EUA |ClassicVNetLocal (10.0.0.0/24) |Olá endereço IP público atribuído toohello RMVNet gateway.|

[!INCLUDE [vpn-gateway-add-lng-rm-portal](../../includes/vpn-gateway-add-lng-rm-portal-include.md)]

## <a name="modifylng"></a>3. Modificar configurações de site local de rede virtual clássicas Olá

Nesta seção, você substituir o endereço IP do espaço reservado Olá usado ao especificar as configurações do site local hello, com hello endereço IP de gateway de VPN do Gerenciador de recursos. Esta seção usa cmdlets do PowerShell (SM) clássico hello.

1. No portal do Azure de Olá, navegue rede virtual clássica de toohello.
2. Na folha de saudação para sua rede virtual, clique em **visão geral**.
3. Em Olá **conexões VPN** seção, clique em nome de saudação do seu site local no gráfico de saudação.

    ![Conexões VPN](./media/vpn-gateway-connect-different-deployment-models-portal/vpnconnections.png "conexões VPN")
4. Em Olá **conexões VPN Site a site** folha, clique em nome de saudação do site de saudação.

    ![Nome do site](./media/vpn-gateway-connect-different-deployment-models-portal/sitetosite3.png "nome do site Local")
5. Na folha de conexão de saudação para seu site local, clique nome hello de saudação do hello site local tooopen **site Local** folha.

    ![Abrir local-site](./media/vpn-gateway-connect-different-deployment-models-portal/openlocal.png "Abrir site local")
6. Em Olá **site Local** folha, substituir Olá **endereço IP do gateway VPN** com o endereço IP de saudação do gateway do Gerenciador de recursos de saudação.

    ![Endereço de ip do gateway](./media/vpn-gateway-connect-different-deployment-models-portal/gwipaddress.png "endereço IP do Gateway")
7. Clique em **Okey** tooupdate endereço IP de saudação.

## <a name="RMtoclassic"></a>4. Criar conexão tooclassic do Gerenciador de recursos

Essas etapas, você configura conexão de saudação do hello Gerenciador de recursos de VNet toohello clássico VNet usando Olá portal do Azure.

1. Em **todos os recursos**, localize o gateway de rede local hello. Em nosso exemplo, o gateway de rede local Olá é **ClassicVNetLocal**.
2. Clique em **configuração** e verificar se o valor do endereço IP hello está gateway VPN Olá Olá VNet clássico. Atualize, se necessário, e clique em **Salvar**. Folha de saudação fechar.
3. Em **todos os recursos**, clique em Olá gateway de rede local.
4. Clique em **conexões** tooopen folha de conexões de saudação.
5. Em Olá **conexões** folha, clique em  **+**  tooadd uma conexão.
6. Em Olá **Adicionar conexão** folha, a conexão de saudação do nome. Por exemplo, "RMtoClassic".
7. A opção **Site a Site** já está selecionada nessa folha.
8. Selecione Olá gateway de rede virtual que você deseja tooassociate com este site.
9. Crie uma **chave compartilhada**. Essa chave também é usada na conexão Olá criados a partir toohello de rede virtual clássica Olá VNet Gerenciador de recursos. Você pode gerar chave hello ou criar um. Em nosso exemplo, usamos "abc123", mas você pode (e deve) usar algo mais complexo.
10. Clique em **Okey** toocreate conexão de saudação.

##<a name="classictoRM"></a>5. Criar a conexão do Gerenciador de tooResource clássico

Essas etapas, você pode configurar conexão de saudação do toohello de rede virtual clássica Olá VNet Gerenciador de recursos. Essas etapas exigem o PowerShell. Você não pode criar essa conexão no portal de saudação. Verifique se você baixou e instalou Olá clássico (SM) e cmdlets do PowerShell do Gerenciador de recursos (RM).

### <a name="1-connect-tooyour-azure-account"></a>1. Conecte-se tooyour conta do Azure

Abra o console do PowerShell Olá com direitos elevados e faça logon tooyour conta do Azure. Olá cmdlet a seguir solicita credenciais de logon Olá para sua conta do Azure. Após o logon, as configurações de conta são baixadas para que fiquem disponível tooAzure PowerShell.

```powershell
Login-AzureRmAccount
```
   
Obtenha uma lista de suas assinaturas do Azure, se você tiver mais de uma assinatura.

```powershell
Get-AzureRmSubscription
```

Especifique que você deseja toouse de assinatura de saudação. 

```powershell
Select-AzureRmSubscription -SubscriptionName "Name of subscription"
```

Adicione sua conta do Azure toouse Olá clássico PowerShell cmdlets (SM). toodo assim, você pode usar o hello comando a seguir:

```powershell
Add-AzureAccount
```

### <a name="2-view-hello-network-configuration-file-values"></a>2. Exibir os valores do arquivo de configuração de rede de saudação

Quando você cria uma rede virtual no portal do Azure de saudação, nome completo de saudação que usa o Azure não é visível no portal do Azure de saudação. Por exemplo, uma rede virtual que aparece toobe nomeado 'ClassicVNet' no hello portal do Azure pode ter um nome muito mais no arquivo de configuração de rede hello. Olá nome pode ter esta aparência: 'Grupo ClassicRG ClassicVNet'. Nestas etapas, você deve baixar Olá rede arquivo e exibir hello valores de configuração.

Crie um diretório no seu computador e, em seguida, exportar diretório toohello de arquivo de configuração do hello rede. Neste exemplo, o arquivo de configuração de rede Olá é tooC:\AzureNet exportado.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

Abra o arquivo hello com um editor e exibição Olá nome para sua rede virtual clássica. Use nomes de saudação no arquivo de configuração de rede hello quando executar o cmdlets do PowerShell.

- Os nomes de VNet são listados como **VirtualNetworkSite name =**
- Os nomes de Site são listados como **LocalNetworkSite name =**

### <a name="3-create-hello-connection"></a>3. Criar conexão Olá

Definir chave compartilhada hello e criar conexão de saudação de toohello de rede virtual clássica Olá VNet Gerenciador de recursos. Não é possível definir chave compartilhada hello, usando o portal de saudação. Certifique-se de que executar essas etapas enquanto estiver conectado usando a versão clássica de saudação do hello cmdlets do PowerShell. Assim, use toodo **Add-AzureAccount**. Caso contrário, não será capaz de tooset Olá '-AzureVNetGatewayKey'.

- Neste exemplo, **- VNetName** é o nome de saudação do hello clássico VNet como encontrado no arquivo de configuração de rede. 
- Olá **- LocalNetworkSiteName** nome hello especificado para o site local do hello, como se encontra no arquivo de configuração de rede.
- Olá **- SharedKey** é um valor que você gera e especificar. Neste exemplo, usamos *abc123*, mas você pode gerar algo mais complexo. Olá importante é esse valor de saudação que você especificar aqui deve ser Olá que mesmo valor que você especificou ao criar sua conexão tooclassic do Gerenciador de recursos.

```powershell
Set-AzureVNetGatewayKey -VNetName "Group ClassicRG ClassicVNet" `
-LocalNetworkSiteName "172B9E16_RMVNetLocal" -SharedKey abc123
```

##<a name="verify"></a>6. Verificar as conexões

Você pode verificar que as conexões usando Olá portal do Azure ou o PowerShell. Ao verificar, talvez seja necessário toowait um ou dois minutos como conexão hello está sendo criado. Quando uma conexão for bem-sucedida, o estado de conectividade de saudação muda de 'Conexão' too'Connected'.

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>conexão de saudação tooverify de seu tooyour de rede virtual clássica VNet Gerenciador de recursos

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

###<a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>conexão de saudação tooverify de tooyour sua VNet Gerenciador de recursos de rede virtual clássica

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>Perguntas frequentes sobre Rede Virtual para Rede Virtual

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]
