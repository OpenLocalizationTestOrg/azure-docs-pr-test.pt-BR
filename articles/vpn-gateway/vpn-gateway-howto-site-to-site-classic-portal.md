---
title: "Conecte-se a sua rede de local tooan rede virtual do Azure: VPN Site a Site (clássico): Portal | Microsoft Docs"
description: "Etapas toocreate uma conexão IPsec de seu local de rede tooan rede virtual do Azure sobre Olá Internet pública. Essas etapas ajudará você a criar uma conexão de Gateway VPN Site a Site entre locais usando o portal de saudação."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/010/2017
ms.author: cherylmc
ms.openlocfilehash: b260bdf610b264458660b278bd32bf0fc5b519ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-using-hello-azure-portal-classic"></a>Criar uma conexão Site a Site usando Olá portal do Azure (clássico)

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Este artigo mostra como toouse Olá toocreate portal do Azure uma conexão de gateway VPN Site a Site de sua toohello de rede local VNet. Olá etapas neste artigo se aplicam a toohello modelo de implantação clássico. Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Uma conexão de gateway VPN Site a Site é usado tooconnect seu local de rede tooan rede virtual do Azure por um túnel VPN IPsec/IKE (IKEv1 ou IKEv2). Esse tipo de conexão exige um VPN de dispositivos localizado localmente que tenha uma tooit de endereço atribuído de IP público externamente. Para saber mais sobre os gateways de VPN, veja [Sobre o gateway de VPN](vpn-gateway-about-vpngateways.md).

![Diagrama de conexão Site a Site de Gateway de VPN entre locais](./media/vpn-gateway-howto-site-to-site-classic-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Antes de começar

Verifique se você atendeu a saudação critérios a seguir antes de iniciar a configuração:

* Verifique se que você deseja toowork no modelo de implantação clássico hello. Se você quiser toowork no modelo de implantação do Gerenciador de recursos de hello, consulte [criar uma conexão Site a Site (Gerenciador de recursos)](vpn-gateway-howto-site-to-site-resource-manager-portal.md). Quando possível, é recomendável que você use o modelo de implantação do Gerenciador de recursos de saudação.
* Verifique se você tem um dispositivo VPN compatível e alguém que é capaz de tooconfigure-lo. Para obter mais informações sobre dispositivos VPN compatíveis e a configuração de dispositivo, confira [Sobre dispositivos VPN](vpn-gateway-about-vpn-devices.md).
* Verifique se você possui um endereço IPv4 público voltado para o exterior para seu dispositivo VPN. Esse endereço IP não pode estar localizado atrás de um NAT.
* Se você não estiver familiarizado com intervalos de endereços IP de saudação localizados na configuração de rede local, é necessário toocoordinate com alguém que possa fornecer os detalhes para você. Quando você criar essa configuração, você deve especificar os prefixos de intervalo endereço IP hello Azure encaminhe tooyour no local. Nenhuma das sub-redes Olá da sua rede local pode ser sobre colo com sub-redes de rede virtual Olá que você deseja tooconnect para.
* Atualmente, PowerShell é chave compartilhada de saudação toospecify necessárias e criar conexão de gateway VPN hello. Instale a versão mais recente Olá de saudação cmdlets do PowerShell de gerenciamento de serviço do Azure (SM). Para obter mais informações, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview). Ao trabalhar com o PowerShell para essa configuração, verifique se você está executando como administrador. 

### <a name="values"></a>Exemplo de valores de configuração para este exercício

Olá exemplos neste artigo usam Olá valores a seguir. Você pode usar esses valores toocreate um ambiente de teste, ou consulte toothem toobetter entender exemplos Olá neste artigo.

* **Nome da rede virtual:** TestVNet1
* **Espaço de endereço:** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (opcional para este exercício)
* **Sub-redes:**
  * FrontEnd: 10.11.0.0/24
  * BackEnd: 10.12.0.0/24 (opcional para este exercício)
* **GatewaySubnet:** 10.11.255.0/27
* **Grupo de recursos:** TestRG1
* **Local:** Leste dos EUA
* **Servidor DNS:** 10.11.0.3 (opcional para este exercício)
* **Nome do site local:** Site2
* **Espaço de endereço de cliente:** Olá espaço de endereço que está localizado no site local.

## <a name="CreatVNet"></a>1. Criar uma rede virtual

Quando você cria um toouse de rede virtual para uma conexão de S2S, você precisa toomake-se de que os espaços de endereço Olá que você especificar não se sobrepõem com qualquer um dos espaços de endereço de cliente Olá para sites locais de saudação que você deseja tooconnect para. Se você tiver uma sobreposição de sub-redes, a conexão não funcionará corretamente.

* Se você já tiver uma rede virtual, verifique se as configurações de saudação compatíveis com seu design de gateway VPN. Preste muita atenção tooany sub-redes que podem se sobrepor a outras redes. 

* Se você ainda não tiver uma rede virtual, crie uma. Capturas de tela são fornecidas como exemplos. Ser valores de saudação tooreplace-se com seus próprios.

### <a name="toocreate-a-virtual-network"></a>toocreate uma rede virtual

1. Em um navegador, navegue toohello [portal do Azure](http://portal.azure.com) e, se necessário, entre com sua conta do Azure.
2. Clique em **+**. Em Olá **marketplace de saudação pesquisa** , digite 'Rede Virtual'. Localize **rede Virtual** de saudação retornada lista e clique em Olá tooopen **rede Virtual** página.

  ![Pesquisar a página da rede virtual](./media/vpn-gateway-howto-site-to-site-classic-portal/newvnetportal700.png)
3. Inferior Olá da página de rede Virtual de saudação da saudação **selecionar um modelo de implantação** lista suspensa, selecione **clássico**e, em seguida, clique em **criar**.

  ![Selecionar o modelo de implantação](./media/vpn-gateway-howto-site-to-site-classic-portal/selectmodel.png)
4. Em Olá **criar network(classic) virtual** página, defina as configurações de rede virtual hello. Nessa página, você adiciona o primeiro espaço de endereço e um único intervalo de endereços da sub-rede. Depois de terminar de criar hello VNet, você pode voltar e adicionar espaços de endereço e sub-redes adicionais.

  ![Página Criar rede virtual](./media/vpn-gateway-howto-site-to-site-classic-portal/createvnet.png "Página Criar rede virtual")
5. Verifique se esse Olá **assinatura** é hello correto. Você pode alterar as assinaturas usando Olá lista suspensa.
6. Clique em **Grupo de recursos** e selecione um grupo de recursos existente ou crie um novo digitando um nome. Para saber mais sobre grupos de recursos, visite [Visão geral do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Em seguida, selecione Olá **local** configurações para sua rede virtual. local de saudação determina onde recursos Olá que você implante toothis VNet residirá.
8. Se você desejar toofind capaz de toobe sua VNet facilmente no painel de saudação, selecione **toodashboard Pin**. Clique em **criar** toocreate sua VNet.

  ![PIN toodashboard](./media/vpn-gateway-howto-site-to-site-classic-portal/pintodashboard150.png "toodashboard de Pin")
9. Depois de clicar em 'Criar', um bloco é exibido no painel de saudação que reflete o progresso de saudação da sua rede virtual. as alterações bloco Olá Olá rede virtual está sendo criado.

  ![Bloco Criando rede virtual](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png "Criando rede virtual")

Depois de criar sua rede virtual, você ver **criado** listado em **Status** na página redes Olá Olá portal clássico do Azure.

## <a name="additionaladdress"></a>2. Adicionar espaço de endereço adicional

Depois de criar sua rede virtual, adicione o outro espaço de endereço. Adicionar espaço de endereço adicional não é uma parte necessária de uma configuração de S2S, mas se você precisar vários espaços de endereço, use Olá etapas a seguir:

1. Localize as redes virtuais Olá no portal de saudação.
2. Na página de saudação para sua rede virtual, em Olá **configurações** seção, clique em **espaço de endereço**.
3. Na página de espaço de endereço hello, clique em **+ adicionar** e digite o espaço de endereço adicional.

## <a name="dns"></a>3. Especificar um servidor DNS

As configurações de DNS não são uma parte obrigatória de uma configuração de S2S, mas o DNS é necessário se você quiser resolução de nomes. A especificação de um valor não cria um novo servidor DNS. Olá endereço IP do servidor DNS que você especificar deve ser um servidor DNS que pode resolver nomes Olá para recursos de saudação que você está se conectando. Para as configurações de exemplo hello, usamos um endereço IP privado. endereço IP Hello que usamos provavelmente não é endereço IP de saudação do servidor DNS. Ser toouse-se de que seus próprios valores.

Depois de criar sua rede virtual, você pode adicionar endereços IP de saudação de uma resolução de nome DNS server toohandle. Abra as configurações de saudação para sua rede virtual, clique em servidores DNS e adicionar endereço IP de saudação do servidor DNS Olá que você deseja toouse para resolução de nome.

1. Localize as redes virtuais Olá no portal de saudação.
2. Na página de saudação para sua rede virtual, em Olá **configurações** seção, clique em **servidores DNS**.
3. Adicionar um servidor DNS.
4. toosave suas configurações, clique em **salvar** na parte superior de saudação da página de saudação.

## <a name="localsite"></a>4. Configurar site local Olá

Normalmente, o site local Olá refere-se tooyour no local. Ele contém o endereço IP de saudação do hello toowhich de dispositivo VPN que você criará uma conexão e intervalos de endereços IP de saudação que serão encaminhados através do dispositivo de VPN toohello do gateway VPN hello.

1. No portal de hello, navegue para o qual você deseja toocreate um gateway de rede virtual do toohello.
2. Na página de saudação para sua rede virtual, em Olá **visão geral** página, na seção de conexões de VPN hello, clique em **Gateway** tooopen Olá **nova Conexão de VPN** página.

  ![Clique em configurações de gateway tooconfigure](./media/vpn-gateway-howto-site-to-site-classic-portal/beforegw125.png "clique em configurações de gateway tooconfigure")
3. Em Olá **nova Conexão de VPN** página, selecione **Site a site**.
4. Clique em **Local do site - definir configurações obrigatórias** tooopen Olá **site Local** página. Definir configurações de saudação e, em seguida, clique em **Okey** toosave configurações de saudação.
  - **Nome:** criar um nome para seu site local toomake fácil para você tooidentify.
  - **Endereço IP do gateway VPN:** este é o endereço IP público de saudação do dispositivo VPN Olá para sua rede local. dispositivo VPN Olá requer um endereço IP IPv4 público. Especifique um endereço IP público válido para Olá toowhich de dispositivo VPN, você deseja tooconnect. Ele não pode estar atrás de NAT e tem toobe acessível pelo Azure. Se você não souber endereço IP de saudação do seu dispositivo VPN, você pode sempre colocado em um valor de espaço reservado (desde que ela está no formato de saudação de um endereço IP público válido) e, em seguida, alterá-la posteriormente.
  - **Espaço de endereço de cliente:** lista Olá intervalos de endereços IP que você deseja roteado toohello rede de local no local por meio deste gateway. Você pode adicionar vários intervalos de espaço de endereço. Certifique-se de que os intervalos de saudação especificado aqui não se sobrepõem com intervalos de outras redes que sua rede virtual se conecta a ou intervalos de endereços de saudação do hello própria rede virtual.

  ![Site local](./media/vpn-gateway-howto-site-to-site-classic-portal/localnetworksite.png "Configurar site local")

## <a name="gatewaysubnet"></a>5. Configurar a sub-rede de gateway Olá

Você deve criar uma sub-rede de gateway para seu gateway de VPN. sub-rede de gateway Olá contém endereços IP de saudação que usam serviços de gateway VPN hello.

1. Em Olá **nova Conexão de VPN** página, a caixa de seleção select Olá **criar gateway imediatamente**. página Olá 'configuração de gateway opcional' é exibida. Se você não selecionar a caixa de seleção hello, você não verá a sub-rede de gateway Olá página tooconfigure hello.

  ![Configuração de gateway - Sub-rede, tamanho, tipo de roteamento](./media/vpn-gateway-howto-site-to-site-classic-portal/optional.png "Configuração de gateway - Sub-rede, tamanho, tipo de roteamento")
2. Olá tooopen **configuração de Gateway** , clique em **configuração de gateway opcional - subrede, tamanho e tipo de roteamento**.
3. Em Olá **configuração de Gateway** , clique em **Subnet - definir configurações obrigatórias** tooopen Olá **Adicionar sub-rede** página.

  ![Configuração de gateway - Sub-rede de gateway](./media/vpn-gateway-howto-site-to-site-classic-portal/subnetrequired.png "Configuração de gateway - Sub-rede de gateway")
4. Em Olá **Adicionar sub-rede** página, adicionar sub-rede de gateway hello. tamanho de saudação da sub-rede de gateway de saudação que você especificar depende da configuração de gateway VPN Olá que você deseja toocreate. Embora seja possível toocreate tão pequenas quanto /29 uma sub-rede do gateway, é recomendável que você use /27 ou /28. Isso cria uma sub-rede maior que inclui mais endereços. Usar uma sub-rede do gateway maior permite suficiente IP endereços tooaccommodate futuras configurações possíveis.

  ![Adicionar sub-rede de gateway](./media/vpn-gateway-howto-site-to-site-classic-portal/addgwsubnet.png "Adicionar sub-rede de gateway")

## <a name="sku"></a>6. Especificar tipo VPN e Olá SKU

1. Gateway Olá selecione **tamanho**. Este é o gateway de saudação SKU que você use toocreate seu gateway de rede virtual. No portal de Olá Olá 'SKU padrão' = **básica**. Gateways VPN clássicos usam o gateway (herdado) antigo Olá SKUs. Para obter mais informações sobre o gateway herdados de saudação SKUs, consulte [trabalhando com o gateway de rede virtual SKUs (antigos SKUs)](vpn-gateway-about-skus-legacy.md).

  ![Selecionar tipo de SKUL e VPN](./media/vpn-gateway-howto-site-to-site-classic-portal/sku.png "Selecionar tipo de SKUL e VPN")
2. Selecione Olá **tipo de roteamento** do seu gateway. Isso também é conhecido como tipo VPN hello. É do tipo de gateway correto Olá tooselect importante porque não é possível converter o gateway de saudação do tooanother de um tipo. Seu dispositivo VPN deve ser compatível com o tipo de roteamento Olá que você selecionar. Para saber mais sobre o tipo de VPN, confira [Sobre as Configurações de Gateway de VPN](vpn-gateway-about-vpn-gateway-settings.md#vpntype). Você pode ver artigos que faz referência too'RouteBased' e 'PolicyBased' VPN tipos. ' Dinâmico 'corresponde too'RouteBased', e 'Static' corresponde a 'PolicyBased'.
3. Clique em **Okey** toosave configurações de saudação.
4. Em Olá **nova Conexão de VPN** , clique em **Okey** final Olá Olá página toobegin criando seu gateway de rede virtual. Dependendo da saudação SKU que você selecionar, pode demorar até too45 minutos toocreate um gateway de rede virtual.

## <a name="vpndevice"></a>7. Configurar o dispositivo de VPN

Rede de local de tooan conexões site a Site requer um dispositivo VPN. Nesta etapa, você deve configurar seu dispositivo VPN. Ao configurar seu dispositivo VPN, você precisa seguir hello:

- Uma chave compartilhada. Isso é Olá mesmo chave que você especificar ao criar sua conexão VPN Site a Site. Em nossos exemplos, usamos uma chave compartilhada básica. É recomendável que você gerar um toouse chave mais complexa.
- Olá endereço IP público do seu gateway de rede virtual. Você pode exibir o endereço IP público de saudação usando Olá portal do Azure, PowerShell ou CLI.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>8. Criar conexão Olá
Nesta etapa, você define chave compartilhada hello e criar conexão hello. chave Olá definir deve estar Olá mesma chave que foi usada na sua configuração de dispositivo VPN.

> [!NOTE]
> No momento, esta etapa não está disponível no portal do Azure de saudação. Você deve usar a versão de gerenciamento de serviço (SM) de saudação do hello cmdlets do PowerShell do Azure.
>

### <a name="step-1-connect-tooyour-azure-account"></a>Etapa 1. Conecte-se tooyour conta do Azure

1. Abra o console do PowerShell com direitos elevados e conecte-se a conta de tooyour. Use Olá toohelp de exemplo que você se conectar a seguir:

  ```powershell
  Add-AzureAccount
  ```
2. Verificar as assinaturas de saudação para conta de saudação.

  ```powershell
  Get-AzureSubscription
  ```
3. Se você tiver mais de uma assinatura, selecione a assinatura de saudação que você deseja toouse.

  ```powershell
  Select-AzureSubscription -SubscriptionId "Replace_with_your_subscription_ID"
  ```

### <a name="step-2-set-hello-shared-key-and-create-hello-connection"></a>Etapa 2. Definir chave compartilhada hello e criar conexão Olá

Ao trabalhar com o modelo de implantação clássico do PowerShell e hello, às vezes, Olá nomes de recursos no portal de saudação não são Olá nomes hello Azure espera toosee ao usar o PowerShell. Hello etapas a seguir ajudarão a exportar Olá rede arquivo tooobtain Olá exata valores de configuração de nomes de saudação.

1. Crie um diretório no seu computador e, em seguida, exportar diretório toohello de arquivo de configuração do hello rede. Neste exemplo, o arquivo de configuração de rede Olá é tooC:\AzureNet exportado.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. Abra o arquivo de configuração de rede de saudação com um editor de xml e verificar valores de saudação para 'LocalNetworkSite name' e 'VirtualNetworkSite name'. Modificar Olá exemplo tooreflect Olá valores que você precisa. Ao especificar um nome que contém espaços, use aspas ao redor do valor de saudação.

3. Definir chave compartilhada hello e criar conexão hello. Olá '-SharedKey' é um valor que você gera e especificar. Exemplo hello, usamos 'abc123', mas você pode gerar (e deve) usar algo mais complexas. Olá importante é esse valor de saudação que você especificar aqui deve ser Olá que mesmo valor que você especificou ao configurar seu dispositivo VPN.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group TestRG1 TestVNet1' `
  -LocalNetworkSiteName 'D1BFC9CB_Site2' -SharedKey abc123
  ```
Quando a conexão de saudação é criado, o resultado de saudação é: **Status: bem-sucedida**.

## <a name="verify"></a>9. Verificar a conexão

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

Se você estiver tendo problemas para se conectar, consulte Olá **solucionar** seção da tabela de saudação do conteúdo no painel esquerdo da saudação.

## <a name="reset"></a>Como tooreset um gateway de VPN

Redefinir um gateway de VPN do Azure é útil se você perde a conectividade VPN entre locais em um ou mais túneis de VPN site a site. Nessa situação, os seus dispositivos VPN local são todos funcionando corretamente, mas são tooestablish não é possível túneis IPsec com gateways de VPN do Azure hello. Para obter as etapas, consulte [Redefinir um gateway de VPN](vpn-gateway-resetgw-classic.md).

## <a name="changesku"></a>Como toochange um SKU de gateway

Para as etapas de saudação toochange um SKU de gateway, consulte [redimensionar um SKU de gateway](vpn-gateway-about-SKUS-legacy.md).

## <a name="next-steps"></a>Próximas etapas

* Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais. Para saber mais, veja [Máquinas virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Para saber mais sobre Túneis Forçados, confira [Sobre o Túnel Forçado](vpn-gateway-about-forced-tunneling.md).