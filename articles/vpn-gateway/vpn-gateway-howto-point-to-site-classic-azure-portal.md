---
title: "Conectar uma rede virtual de computador tooa usando a autenticação de certificado e de ponto para Site: clássico do Portal do Azure | Microsoft Docs"
description: "Conectar com segurança tooyour clássico rede Virtual do Azure, criando uma conexão de gateway VPN ponto a Site usando Olá portal do Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 65e14579-86cf-4d29-a6ac-547ccbd743bd
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 9b53ba43ee4dfb61defeec458905fb1f1b18c3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-classic-azure-portal"></a>Configurar uma conexão de ponto para Site tooa VNet usando a autenticação de certificado (clássico): o portal do Azure

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Este artigo mostra como toocreate uma rede virtual com uma conexão ponto a Site no modelo de implantação clássico hello usando Olá portal do Azure. Essa configuração usa Olá tooauthenticate de certificados conexão cliente. Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>

Um gateway VPN ponto a Site (P2S) permite criar uma rede virtual de tooyour de conexão segura de um computador cliente individual. Conexões VPN Site a ponto são úteis quando você deseja tooconnect tooyour VNet de um local remoto, como quando você está comunicando em casa ou em uma conferência. Uma VPN de P2S também é toouse uma solução útil em vez de uma VPN Site a Site quando você tiver apenas alguns clientes que precisam de tooconnect tooa VNet. 

Usa P2S Olá SSTP Secure Socket Tunneling Protocol (), que é um protocolo VPN baseada em SSL. Uma conexão VPN de P2S é estabelecido pela iniciá-lo do computador do cliente de saudação.


![Diagrama ponto a site](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/point-to-site-connection-diagram.png)


Conexões de autenticação de certificado de ponto a Site requerem a seguir hello:

* Um gateway de VPN dinâmico.
* Olá chave pública (arquivo. cer) para um certificado raiz, que é carregado tooAzure. Isso é considerado um certificado confiável e é usado para autenticação.
* Um certificado de cliente gerado a partir do certificado de raiz hello e instalado em cada computador cliente que se conectam. Esse certificado é usado para autenticação do cliente.
* Um pacote de configuração de cliente VPN deve ser gerado e instalado em cada computador cliente que se conecta. pacote de configuração de cliente Olá configura o cliente VPN nativo Olá que já está no sistema operacional de saudação com hello informações necessárias tooconnect toohello VNet.

As conexões Ponto a Site não exigem um dispositivo VPN ou um endereço IP voltado para o público local. Olá conexão VPN é criado por protocolo SSTP (Secure Socket Tunneling Protocol). No lado do servidor de saudação, há suporte para as versões 1.0, 1.1 e 1.2 do SSTP. cliente Olá decide qual toouse de versão. Por padrão, para Windows 8.1 e posterior, o SSTP usa 1.2. 

Para obter mais informações sobre conexões ponto a Site, consulte Olá [ponto a Site perguntas frequentes sobre](#faq) final Olá deste artigo.

### <a name="example-settings"></a>Configurações de exemplo

Você pode usar o hello valores toocreate um ambiente de teste a seguir, ou consulte valores toothese toobetter entender exemplos Olá neste artigo:

* **Nome: VNet1**
* **Espaço de endereço: 192.168.0.0/16**<br>Neste exemplo, usamos apenas um espaço de endereço. Você pode ter mais de um espaço de endereço para sua rede virtual.
* **Nome da sub-rede: FrontEnd**
* **Intervalo de endereços da sub-rede: 192.168.1.0/24**
* **Assinatura:** se você tiver mais de uma assinatura, verifique se você estiver usando Olá correto.
* **Grupo de Recursos: TestRG**
* **Local: Leste dos EUA**
* **Tipo de conexão: ponto a site**
* **Espaço de Endereço de Cliente: 172.16.201.0/24**. Clientes VPN que se conectam toohello VNet usando esta conexão ponto a Site recebe um endereço IP de Olá pool especificado.
* **GatewaySubnet: 192.168.200.0/24**. sub-rede de Gateway Olá deve usar o nome de saudação 'GatewaySubnet'.
* **Tamanho:** gateway Olá selecione SKU que você deseja toouse.
* **Tipo de Roteamento: Dinâmico**

## <a name="vnetvpn"></a>1. Criar uma rede virtual e um gateway de VPN

Antes de começar, verifique se você tem uma assinatura do Azure. Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial).

### <a name="createvnet"></a>Parte 1: criar uma rede virtual

Se você ainda não tiver uma rede virtual, crie uma. Capturas de tela são fornecidas como exemplos. Ser valores de saudação tooreplace-se com seus próprios. uma rede virtual por meio de toocreate Olá portal do Azure, Olá use as etapas a seguir:

1. Em um navegador, navegue toohello [portal do Azure](http://portal.azure.com) e, se necessário, entre com sua conta do Azure.
2. Clique em **Novo**. Em Olá **marketplace de saudação pesquisa** , digite 'Rede Virtual'. Localize **rede Virtual** de saudação retornada lista e clique em Olá tooopen **rede Virtual** página.

  ![Pesquisar a página da rede virtual](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvnetportal700.png)
3. Inferior Olá da página de rede Virtual de saudação da saudação **selecionar um modelo de implantação** , selecione **clássico**e, em seguida, clique em **criar**.

  ![Selecionar o modelo de implantação](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/selectmodel.png)
4. Em Olá **criar rede virtual** página, defina as configurações de rede virtual hello. Nessa página, você adiciona o primeiro espaço de endereço e um único intervalo de endereços da sub-rede. Depois de terminar de criar hello VNet, você pode voltar e adicionar espaços de endereço e sub-redes adicionais.

  ![Criar página da rede virtual](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/vnet125.png)
5. Verifique se esse Olá **assinatura** é hello correto. Você pode alterar as assinaturas usando Olá lista suspensa.
6. Clique em **Grupo de recursos** e selecione um grupo de recursos existente ou crie um novo digitando um nome para seu novo grupo de recursos. Se você estiver criando um novo grupo de recursos, grupo de recursos de saudação de nome de acordo com o tooyour planejada valores de configuração. Para saber mais sobre grupos de recursos, visite [Visão geral do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-overview.md#resource-groups).
7. Em seguida, selecione Olá **local** configurações para sua rede virtual. local de saudação determina onde recursos Olá que você implante toothis VNet residirá.
8. Selecione **Pin toodashboard** se desejar toofind capaz de toobe sua VNet facilmente no painel de saudação e, em seguida, clique em **criar**.

  ![PIN toodashboard](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/pintodashboard150.png)
9. Depois de clicar em criar, um bloco é exibido no painel que refletirá o progresso de saudação da sua rede virtual. as alterações bloco Olá Olá rede virtual está sendo criado.

  ![Criar bloco de rede virtual](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png)
10. Quando sua rede virtual tiver sido criada, você ver **criado** listado em **Status** na página redes Olá Olá portal clássico do Azure.
11. Adicionar um servidor DNS (opcional). Depois de criar sua rede virtual, você pode adicionar endereços IP de saudação de um servidor DNS para resolução de nome. Olá endereço IP do servidor DNS que você especificar deve ser o endereço de saudação do servidor DNS que pode resolver nomes Olá para recursos de saudação em sua rede virtual.<br>tooadd um servidor DNS, abra as configurações de saudação para sua rede virtual, clique em servidores DNS e adicionar endereço IP de saudação do servidor DNS Olá que você deseja toouse.

### <a name="gateway"></a>Parte 2: criar um gateway de roteamento dinâmico e de sub-rede de gateway

Nesta etapa, você cria uma sub-rede de gateway e um gateway de roteamento Dinâmico. No hello portal do Azure para o modelo de implantação clássico hello, criação de sub-rede de gateway hello e gateway Olá pode ser feito por meio de saudação mesmo páginas de configuração.

1. No portal de hello, navegue para o qual você deseja toocreate um gateway de rede virtual do toohello.
2. Na página de saudação para sua rede virtual, em Olá **visão geral** página, na seção de conexões de VPN hello, clique em **Gateway**.

  ![Clique em toocreate um gateway](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/beforegw125.png)
3. Em Olá **nova Conexão de VPN** página, selecione **ponto para site**.

  ![Tipo de conexão Ponto a Site](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvpnconnect.png)
4. Para **espaço de endereço de cliente**, adicione o intervalo de endereços IP hello. Este é o intervalo de saudação do qual os clientes VPN Olá recebem um endereço IP ao se conectar. Use um intervalo de endereços IP particular que não coincida com hello no local que você se conectará de, ou com hello VNet que você deseja tooconnect para. Você pode excluir o intervalo de preenchimento automático de saudação e adicionar Olá privado intervalo de endereços IP que você deseja toouse.

  ![Espaço de endereço de cliente](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientaddress.png)
5. Selecione Olá **criar gateway imediatamente** caixa de seleção.

  ![Criar gateway imediatamente](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/creategwimm.png)
6. Clique em **configuração de gateway opcional** tooopen Olá **configuração de Gateway** página.

  ![Clique em configuração de gateway opcional](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/optsubnet125.png)
7. Clique em **sub-rede configurar as configurações necessárias** tooadd Olá **sub-rede de gateway**. Embora seja possível toocreate tão pequenas quanto /29 uma sub-rede do gateway, é recomendável que você crie uma sub-rede maior que inclui mais endereços selecionando pelo menos /28 ou /27. Isso permitirá suficiente endereços tooaccommodate possíveis configurações adicionais que você pode em Olá futuras. Ao trabalhar com as sub-redes de gateway, evite associando uma sub-rede do gateway de toohello do grupo (NSG) de segurança de rede. Associando a uma sub-rede toothis de grupo de segurança de rede pode causar sua toostop de gateway VPN está funcionando conforme o esperado.

  ![Adicionar GatewaySubnet](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsubnet125.png)
8. Gateway Olá selecione **tamanho**. tamanho de saudação é SKU do gateway de saudação do seu gateway de rede virtual. No portal de Olá Olá SKU padrão é **básica**. Para obter informações sobre os SKUs de gateway, confira [Sobre configurações de Gateway de VPN](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

  ![Tamanho de gateway](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsize125.png)
9. Selecione Olá **tipo de roteamento** do seu gateway. Configurações de P2S requerem um tipo de roteamento **Dinâmico**. Clique em **OK** quando terminar de configurar esta página.

  ![Configurar o tipo de roteamento](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/routingtype125.png)
10. Em Olá **nova Conexão de VPN** , clique em **Okey** final Olá Olá página toobegin criando seu gateway de rede virtual. Um gateway de VPN pode demorar até too45 toocomplete de minutos, dependendo da saudação sku de gateway que você selecionar.

## <a name="generatecerts"></a>2. Criar certificados

Certificados são usados por clientes VPN do Azure tooauthenticate para VPNs ponto a Site. Você carregar as informações de chave pública do hello de saudação tooAzure de certificado de raiz. chave pública Olá é considerado 'confiável'. Certificados de cliente devem ser gerados a partir do certificado de raiz confiável do hello e, em seguida, em cada computador cliente no repositório de certificados de usuário/pessoal de certificados atual hello. certificado de saudação é cliente de saudação tooauthenticate usado quando ele inicia uma conexão toohello VNet. 

Se você usa certificados autoassinados, eles devem ser criados usando parâmetros específicos. Você pode criar um certificado autoassinado usando instruções Olá para [PowerShell e Windows 10](vpn-gateway-certificates-point-to-site.md), ou [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). É importante seguir as etapas de saudação nestas instruções ao trabalhar com os certificados raiz autoassinados e gerar os certificados de cliente de Olá certificado raiz autoassinado. Caso contrário, os certificados de saudação criados não serão compatíveis com P2S conexões e você receberá um erro de conexão.

### <a name="cer"></a>Parte 1: Obter chave pública da saudação (. cer) para o certificado de raiz de saudação

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="genclientcert"></a>Parte 2: gerar um certificado de cliente

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>3. Carregar arquivo. cer do certificado de raiz de saudação

Depois de saudação gateway foi criado, você pode carregar o arquivo. cer de hello (que contém as informações de chave pública Olá) para um tooAzure de certificado raiz confiável. Você não carregar a chave privada Olá para Olá tooAzure de certificado de raiz. Uma vez carregado o arquivo a.cer, Azure pode usá-lo tooauthenticate clientes que instalaram um certificado de cliente gerado a partir do certificado de raiz confiável do hello. Você pode carregar arquivos de certificado raiz confiável adicionais - tooa total de 20 - posteriormente, se necessário.  

1. Em Olá **conexões VPN** seção da página de saudação para sua rede virtual, clique em Olá **clientes** tooopen gráfico Olá **ponto a site VPN conexão** página.

  ![Clientes](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. Em Olá **conexãopontoasite** , clique em **gerenciar certificados** tooopen Olá **certificados** página.<br>

  ![Página Certificados](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. Em Olá **certificados** , clique em **carregar** tooopen Olá **Upload do certificado** página.<br>

    ![Carregar a página de certificados](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/uploadcerts.png)<br>
4. Clique em Olá pasta gráfico toobrowse para o arquivo. cer de saudação. Selecione o arquivo hello, clique **Okey**. Atualização Olá página toosee Olá carregado certificado Olá **certificados** página.

  ![Carregar um certificado](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/upload.png)<br>

## <a name="vpnclientconfig"></a>4. Configurar cliente Olá

tooconnect tooa VNet usando uma VPN ponto a Site, cada cliente deve instalar um cliente VPN do Windows nativo pacote tooconfigure hello. pacote de configuração de saudação configura native cliente de VPN do Windows hello com a rede virtual do toohello Olá configurações tooconnect necessário.

Você pode usar o hello a mesma configuração de cliente VPN do pacote em cada computador cliente, como versão Olá corresponde a arquitetura de saudação para cliente hello. Para lista de saudação dos sistemas operacionais cliente com suporte, consulte Olá [conexõespontoaSiteperguntas frequentes sobre](#faq) final Olá deste artigo.

### <a name="generateconfigpackage"></a>Parte 1: Gerar e instalar o pacote de configuração de cliente VPN Olá

1. Em Olá portal do Azure, na Olá **visão geral** página para a sua rede virtual, **conexões VPN**, clique Olá Olá de gráfico tooopen cliente **ponto a site VPN conexão** página.
2. Na parte superior de saudação do hello **ponto a site VPN conexão** , clique em pacote de download de saudação que corresponde a toohello sistema operacional do cliente no qual ele será instalado:

  * Para clientes de 64 bits, selecione **Cliente VPN (64 bits)**.
  * Para clientes de 32 bits, selecione **Cliente VPN (32 bits)**.

  ![Baixe o pacote de configuração de cliente VPN](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/dlclient.png)<br>
3. Quando gera Olá empacotado, baixe e instale-o no computador cliente. Se vir um pop-up do SmartScreen, clique em **Mais informações** e em **Executar mesmo assim**. Você também pode salvar Olá pacote tooinstall em outros computadores cliente.

### <a name="installclientcert"></a>Parte 2: Instalar certificado de cliente Olá

Se você quiser toocreate um P2S conexão de um computador cliente que não sejam Olá você usado certificados de cliente toogenerate Olá, é necessário tooinstall um certificado de cliente. Ao instalar um certificado de cliente, é necessário senha Olá que foi criada quando o certificado de cliente Olá foi exportado. Normalmente, isso é apenas uma questão de duas vezes em Olá certificado e instalá-lo. Para saber mais informações consulte, [Instalar um certificado de cliente exportado](vpn-gateway-certificates-point-to-site.md#install).

## <a name="connect"></a>5. Conecte-se tooAzure

### <a name="connect-tooyour-vnet"></a>Conecte-se tooyour VNet

1. tooconnect tooyour VNet, no computador do cliente hello, navegar tooVPN conexões e localize a conexão de VPN Olá que você criou. Ele é chamado hello mesmo nome de sua rede virtual. Clique em **Conectar**. Pode aparecer uma mensagem pop-up que refere-se o certificado de saudação toousing. Se isso acontecer, clique em **continuar** privilégios elevados do toouse.
2. Em Olá **Conexão** página de status, clique em **conectar** toostart conexão de saudação. Se você vir um **Selecionar certificado** tela, verifique se mostrando de certificado de cliente Olá Olá um que você deseja toouse tooconnect. Se não for, use Olá seta suspensa tooselect Olá correto certificado e, em seguida, clique em **Okey**.

  ![Conexão de cliente VPN](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientconnect.png)
3. A conexão é estabelecida.

  ![Conexão estabelecida](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Solucionar problemas de conexões P2S

[!INCLUDE [verify-client-certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

### <a name="verifyvpnconnect"></a>Verifique se a conexão de VPN Olá

1. tooverify que a conexão VPN estiver ativa, abra um prompt de comando com privilégios elevados e execute *ipconfig/all*.
2. Exibir resultados de saudação. Observe que o endereço IP hello recebido é um dos endereços hello dentro do intervalo de endereços de conectividade ponto a Site Olá que você especificou quando criou sua rede virtual. resultados de saudação devem ser exemplo toothis semelhante:

  ```
    PPP adapter VNet1:
        Connection-specific DNS Suffix .:
        Description.....................: VNet1
        Physical Address................:
        DHCP Enabled....................: No
        Autoconfiguration Enabled.......: Yes
        IPv4 Address....................: 192.168.130.2(Preferred)
        Subnet Mask.....................: 255.255.255.255
        Default Gateway.................:
        NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Conecte-se a máquina virtual de tooa

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-classic-include.md)]

## <a name="add"></a>Adicionar ou remover certificados raiz confiáveis

Você pode adicionar e remover um certificado raiz do Azure. Quando você remove um certificado raiz, os clientes que têm um certificado gerado a partir dessa raiz não serão capaz de tooauthenticate e, portanto, não será capaz de tooconnect. Se você quiser um tooauthenticate de cliente e se conectar, você precisa tooinstall um novo certificado de cliente gerado a partir de um certificado raiz confiável tooAzure (carregado).

### <a name="addtrustedroot"></a>tooadd um certificado raiz confiável

Você pode somar too20 confiáveis raiz certificado. cer arquivos tooAzure. Para obter instruções, consulte [seção 3 - arquivo. cer do certificado raiz de saudação do carregamento](#upload).

### <a name="removetrustedroot"></a>tooremove um certificado raiz confiável

1. Em Olá **conexões VPN** seção da página de saudação para sua rede virtual, clique em Olá **clientes** tooopen gráfico Olá **ponto a site VPN conexão** página.

  ![Clientes](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. Em Olá **conexãopontoasite** , clique em **gerenciar certificados** tooopen Olá **certificados** página.<br>

  ![Página Certificados](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. Em Olá **certificados** , clique em Olá reticências próximo toohello certificado que você deseja tooremove e clique em **excluir**.

  ![Excluir o certificado raiz](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deleteroot.png)<br>

## <a name="revokeclient"></a>Revogar um certificado de cliente

É possível revogar certificados de cliente. certificado Olá lista de revogação permite que você tooselectively negar conectividade ponto a Site com base em certificados de cliente individuais. Isso é diferente da remoção de um certificado raiz confiável. Se você remover um certificado de raiz confiável. cer do Azure, ela revoga o acesso de Olá para todos os certificados de cliente gerado/assinado pelo certificado de raiz revogado hello. Revogar um certificado de cliente, em vez de certificado de raiz hello, permite Olá outros certificados que foram gerados a partir do certificado de raiz de Olá toocontinue toobe usado para autenticação de conexão de ponto para Site hello.

uma prática comum Olá é o acesso de toomanage de certificado toouse Olá raiz nos níveis de equipe ou organização, durante o uso de certificados do cliente revogados para controle de acesso refinado sobre usuários individuais.

### <a name="revokeclientcert"></a>toorevoke um certificado de cliente

Você pode revogar um certificado de cliente, adicionando a lista de revogação de toohello Olá impressão digital.

1. Recupere a impressão digital do certificado de cliente hello. Para obter mais informações, consulte [como: recuperar Olá impressão digital de um certificado](https://msdn.microsoft.com/library/ms734695.aspx).
2. Copie o editor de texto Olá informações tooa e remover todos os espaços para que seja uma cadeia de caracteres contínua.
3. Navegue toohello **'nome de rede virtual clássico' > conexão VPN ponto a site > certificados** página e, em seguida, clique em **lista de revogação** tooopen página de lista de revogação de saudação. 
4. Em Olá **lista de revogação** , clique em **+ Adicionar certificado** tooopen Olá **Adicionar lista de toorevocation certificado** página.
5. Em Olá **Adicionar lista de toorevocation certificado** página, cole a impressão digital do certificado hello como uma linha contínua de texto, sem espaços. Clique em **Okey** final Olá Olá página.
6. Após a conclusão da atualização, o certificado de saudação não pode mais ser tooconnect usado. Os clientes que tentam tooconnect usando este certificado recebem uma mensagem dizendo que Olá certificado não é mais válido.

## <a name="faq"></a>Perguntas frequentes sobre Ponto a site

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Próximas etapas
Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais. Para saber mais, veja [Máquinas virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). toounderstand mais sobre redes e máquinas virtuais, consulte [visão geral de rede do Azure e a VM do Linux](../virtual-machines/linux/azure-vm-network-overview.md).
