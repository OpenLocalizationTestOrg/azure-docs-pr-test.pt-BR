---
title: "Conectar uma rede virtual de computador tooa usando a autenticação de certificado e de ponto para Site: Portal do Azure | Microsoft Docs"
description: "Conecte com segurança um tooyour computador rede Virtual do Azure, criando uma conexão de gateway VPN ponto a Site usando a autenticação de certificado. Este artigo se aplica o modelo de implantação do Gerenciador de recursos de toohello e usa Olá portal do Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a15ad327-e236-461f-a18e-6dbedbf74943
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: 1419d6b4c160140b62d656b25bd02f6af7fd6655
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-azure-portal"></a>Configurar uma conexão de ponto para Site tooa VNet usando a autenticação de certificado: portal do Azure

Este artigo mostra como toocreate uma rede virtual com uma conexão ponto a Site no modelo de implantação de Gerenciador de recursos de hello usando Olá portal do Azure. Essa configuração usa Olá tooauthenticate de certificados conexão cliente. Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Um gateway VPN ponto a Site (P2S) permite criar uma rede virtual de tooyour de conexão segura de um computador cliente individual. Conexões VPN Site a ponto são úteis quando você deseja tooconnect tooyour VNet de um local remoto, como quando você está comunicando em casa ou em uma conferência. Uma VPN de P2S também é toouse uma solução útil em vez de uma VPN Site a Site quando você tiver apenas alguns clientes que precisam de tooconnect tooa VNet. 

Usa P2S Olá SSTP Secure Socket Tunneling Protocol (), que é um protocolo VPN baseada em SSL. Uma conexão VPN de P2S é estabelecido pela iniciá-lo do computador do cliente de saudação.

![Diagrama ponto a site](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/point-to-site-connection-diagram.png)

Conexões de autenticação de certificado de ponto a Site requerem a seguir hello:

* Gateway de VPN RouteBased.
* Olá chave pública (arquivo. cer) para um certificado raiz, que é carregado tooAzure. Depois que o certificado Olá é carregado, ele é considerado um certificado confiável e é usado para autenticação.
* Um certificado de cliente que é gerado a partir do certificado de raiz de saudação e instalado em cada computador cliente que se conectam toohello VNet. Esse certificado é usado para autenticação do cliente.
* Um pacote de configuração de cliente VPN. pacote de configuração de cliente VPN Olá contém informações necessárias Olá Olá cliente tooconnect toohello VNet. pacote de saudação configura o cliente VPN existente Olá que é nativa toohello sistema operacional Windows. Cada cliente que se conecta deve ser configurado usando o pacote de configuração de saudação.

As conexões Ponto a Site não exigem um dispositivo VPN ou um endereço IP voltado para o público local. Olá conexão VPN é criado por protocolo SSTP (Secure Socket Tunneling Protocol). No lado do servidor de saudação, há suporte para as versões 1.0, 1.1 e 1.2 do SSTP. cliente Olá decide qual toouse de versão. Por padrão, para Windows 8.1 e posterior, o SSTP usa 1.2.

Para obter mais informações sobre conexões ponto a Site, consulte Olá [ponto a Site perguntas frequentes sobre](#faq) final Olá deste artigo.

#### <a name="example"></a>Valores de exemplo

Você pode usar o hello valores toocreate um ambiente de teste a seguir, ou consulte valores toothese toobetter entender exemplos Olá neste artigo:

* **Nome da VNet:** VNet1
* **Espaço de endereço:** 192.168.0.0/16<br>Neste exemplo, usamos apenas um espaço de endereço. Você pode ter mais de um espaço de endereço para sua rede virtual.
* **Nome da sub-rede:** FrontEnd
* **Intervalo de endereços da sub-rede:** 192.168.1.0/24
* **Assinatura:** se você tiver mais de uma assinatura, verifique se você estiver usando Olá correto.
* **Grupo de Recursos:** TestRG
* **Local:** Leste dos EUA
* **GatewaySubnet:** 192.168.200.0/24<br>
* **Servidor DNS:** (opcional) endereço IP do servidor DNS de saudação que você deseja toouse para resolução de nome.
* **Nome do gateway de rede virtual:** VNet1GW
* **Tipo de gateway:** VPN
* **Tipo de VPN:** baseada em rota
* **Endereço IP público:** VNet1GWpip
* **Tipo de conexão:** ponto a site
* **Pool de endereços do cliente:** 172.16.201.0/24<br>Os clientes VPN que se conectam toohello VNet usando esta conexão ponto a Site recebem um endereço IP do pool de endereços de cliente hello.

## <a name="createvnet"></a>1. Criar uma rede virtual

Antes de começar, verifique se você tem uma assinatura do Azure. Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial).

[!INCLUDE [Basic Point-to-Site VNet](../../includes/vpn-gateway-basic-p2s-vnet-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>2. Adicionar uma sub-rede de gateway

Antes de conectar o gateway de rede virtual tooa, você primeiro precisa de sub-rede de gateway toocreate Olá Olá toowhich de rede virtual você deseja tooconnect. Serviços de gateway Olá usam endereços IP de saudação especificados na sub-rede do gateway hello. Se possível, crie uma sub-rede do gateway usando um bloco CIDR de /28 ou /27 tooprovide suficiente IP endereços tooaccommodate requisitos de configuração futura adicional.

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-p2s-rm-portal-include.md)]

## <a name="dns"></a>3. Especificar um servidor DNS (opcional)

Depois de criar sua rede virtual, você pode adicionar endereços IP de saudação de uma resolução de nome DNS server toohandle. servidor DNS Olá é opcional para essa configuração, mas necessárias se você quiser que a resolução de nomes. A especificação de um valor não cria um novo servidor DNS. Olá endereço IP do servidor DNS que você especificar deve ser um servidor DNS que pode resolver nomes Olá para recursos de saudação que você está se conectando. Neste exemplo, usamos um endereço IP privado, mas é provável que isso não é Olá endereço IP do servidor DNS. Ser toouse-se de que seus próprios valores.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="creategw"></a>4. Criar um gateway de rede virtual

[!INCLUDE [create-gateway](../../includes/vpn-gateway-add-gw-p2s-rm-portal-include.md)]

## <a name="generatecert"></a>5. Gerar certificados

Certificados são usados pelos clientes do Azure tooauthenticate tooa VNet sobre uma conexão VPN Site a ponto de conexão. Depois que você obtiver um certificado raiz, você [carregar](#uploadfile) Olá tooAzure de informações de chave pública. certificado de raiz de saudação é considerado 'confiável' pelo Azure para conexão pela rede virtual do P2S toohello. Você também gerar certificados de cliente de certificado de raiz confiável do hello e instalá-las em cada computador cliente. certificado de cliente de saudação é cliente de saudação tooauthenticate usada quando ele inicia uma conexão toohello VNet. 

### <a name="getcer"></a>1. Obter arquivo hello. cer certificado de raiz de saudação

[!INCLUDE [root-certificate](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="generateclientcert"></a>2. Gerar um certificado de cliente

[!INCLUDE [generate-client-cert](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="addresspool"></a>6. Adicionar pool de endereços de cliente Olá

pool de endereços de cliente Olá é um intervalo de endereços IP que você especificar. clientes de saudação que se conectam através de uma VPN ponto a Site recebem um endereço IP nesse intervalo. Use um intervalo de endereços IP particular que não coincida com hello no local que você se conectar de ou Olá VNet que você deseja tooconnect para.

1. Depois que o gateway de rede virtual Olá tiver sido criado, navegar toohello **configurações** seção da página de saudação do gateway de rede virtual. Em Olá **configurações** seção, clique em **configuraçãopontoasite** tooopen Olá **-para-Site-configuração do ponto de** página.

  ![Página ponto a site](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/gatewayblade.png)
2. Em Olá **-para-Site-configuração do ponto de** página, você pode excluir o intervalo de preenchimento automático de saudação e adicionar Olá privado intervalo de endereços IP que você deseja toouse. Clique em **salvar** toovalidate e salvar a configuração de saudação.

  ![Pool de endereços do cliente](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/ipaddresspool.png)

## <a name="uploadfile"></a>7. Carregar dados de certificado pública do certificado de raiz Olá

Depois de saudação gateway foi criado, você carregar Olá informações de chave pública Olá tooAzure de certificado de raiz. Uma vez carregados, dados de certificado público de saudação Azure pode usá-lo tooauthenticate clientes que instalaram um certificado de cliente gerado a partir do certificado de raiz confiável do hello. Você pode carregar um total de tooa o certificados de raiz confiável de 20.

1. Os certificados são adicionados no hello **configuraçãopontoasite** página Olá **certificado raiz** seção.  
2. Certifique-se de que você exportou o certificado de raiz hello como o arquivo de x. 509 (. cer) codificado em Base 64. Certificado de saudação tooexport neste formato serão necessárias para que você pode abrir o certificado de saudação com o editor de texto.
3. Abra o certificado de saudação com um editor de texto, como o bloco de notas. Ao copiar dados do certificado hello, certifique-se de que você copiar o texto de saudação como uma linha contínua sem retornos de carro ou alimentações de linha. Talvez seja necessário toomodify exibição em too'Show de editor de texto de saudação símbolo/Mostrar toosee Olá de carro todos os caracteres retorna e alimentação de linha. Copie somente Olá seção como uma linha contínua a seguir:

  ![Dados do certificado](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/copycert.png)
4. Colar dados do certificado Olá Olá **dados de certificado público** campo. **Nome** Olá certificado e, em seguida, clique em **salvar**. Você pode adicionar certificados de raiz confiável de too20.

  ![Carregamento do certificado](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/rootcertupload.png)

## <a name="clientconfig"></a>8. Gerar e instalar o pacote de configuração de cliente VPN Olá

tooconnect tooa VNet usando uma VPN ponto a Site, cada cliente deve instalar um pacote de configuração de cliente que configura o cliente VPN nativo de saudação com configurações de saudação e arquivos de rede virtual do toohello tooconnect necessário. pacote de configuração de cliente VPN Olá configura native cliente de VPN do Windows hello, não instala um cliente VPN novo ou diferente.

Você pode usar o hello a mesma configuração de cliente VPN do pacote em cada computador cliente, como versão Olá corresponde a arquitetura de saudação para cliente hello. Para lista de saudação dos sistemas operacionais cliente com suporte, consulte Olá [conexõespontoaSiteperguntas frequentes sobre](#faq) final Olá deste artigo.

### <a name="step-1---generate-and-download-hello-client-configuration-package"></a>Etapa 1: gerar e baixar o pacote de configuração de cliente Olá

1. Em Olá **configuraçãopontoasite** , clique em **cliente VPN baixar** tooopen Olá **cliente VPN baixar** página. Ele usa um ou dois minutos para Olá toogenerate de pacote.

  ![Download do cliente VPN 1](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/downloadvpnclient1.png)
2. Selecionar pacote correto Olá para o cliente e, em seguida, clique em **baixar**. Salve o arquivo de pacote de configuração de saudação. Instale o pacote de configuração de cliente VPN de saudação em cada computador cliente que se conecta a rede virtual toohello.

  ![Download do cliente VPN 2](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/vpnclient.png)

### <a name="step-2---install-hello-client-configuration-package"></a>Etapa 2 - Instalar pacote de configuração de cliente de saudação

1. Copiar arquivo de configuração de saudação localmente computador toohello que deseja que a rede virtual do tooconnect tooyour. 
2. Clique duas vezes no pacote de Olá Olá .exe arquivos tooinstall no computador do cliente de saudação. Como você criou o pacote de configuração hello, ele não está assinado e você verá um aviso. Se você receber um pop-up do Windows SmartScreen, clique em **obter mais informações** (em saudação à esquerda), em seguida, **executar assim mesmo** tooinstall pacote de saudação.
3. Instale o pacote de saudação no computador do cliente de saudação. Se você receber um pop-up do Windows SmartScreen, clique em **obter mais informações** (em saudação à esquerda), em seguida, **executar assim mesmo** tooinstall pacote de saudação.
4. No computador do cliente hello, navegue muito**as configurações de rede** e clique em **VPN**. Olá conexão VPN mostra o nome de saudação da rede virtual de saudação que ele se conecta ao.

## <a name="installclientcert"></a>9. Instalar um certificado do cliente exportado

Se você quiser toocreate um P2S conexão de um computador cliente que não sejam Olá você usado certificados de cliente toogenerate Olá, é necessário tooinstall um certificado de cliente. Ao instalar um certificado de cliente, é necessário senha Olá que foi criada quando o certificado de cliente Olá foi exportado. Normalmente, ele é apenas uma questão de duas vezes em Olá certificado e instalá-lo.

Verifique se o certificado de cliente hello exportado como um. pfx juntamente com a cadeia de certificado inteiro hello (que é o padrão de saudação). Caso contrário, informações de certificado raiz Olá não está presentes no computador do cliente hello e cliente Olá não será capaz de tooauthenticate corretamente. Para saber mais informações consulte, [Instalar um certificado de cliente exportado](vpn-gateway-certificates-point-to-site.md#install).

## <a name="connect"></a>10. Conecte-se tooAzure

1. tooconnect tooyour VNet, no computador do cliente hello, navegar tooVPN conexões e localize a conexão de VPN Olá que você criou. Ele é chamado hello mesmo nome de sua rede virtual. Clique em **Conectar**. Pode aparecer uma mensagem pop-up que refere-se o certificado de saudação toousing. Clique em **continuar** privilégios elevados do toouse.

2. Em Olá **Conexão** página de status, clique em **conectar** toostart conexão de saudação. Se você vir um **Selecionar certificado** tela, verifique se mostrando de certificado de cliente Olá Olá um que você deseja toouse tooconnect. Se não for, use Olá seta suspensa tooselect Olá correto certificado e, em seguida, clique em **Okey**.

  ![Cliente VPN conecta tooAzure](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/clientconnect.png)
3. A conexão é estabelecida.

  ![Conexão estabelecida](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Solucionar problemas de conexões P2S

[!INCLUDE [verifies client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>11. Verificar a conexão

1. tooverify que a conexão VPN estiver ativa, abra um prompt de comando com privilégios elevados e execute *ipconfig/all*.
2. Exibir resultados de saudação. Observe que o endereço IP hello recebido é um dos endereços de saudação em Olá ponto a Site VPN cliente Pool de endereços que você especificou na sua configuração. resultados de saudação são exemplo toothis semelhante:

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Conecte-se a máquina virtual de tooa

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <a name="add"></a>Adicionar ou remover certificados raiz confiáveis

Você pode adicionar e remover um certificado raiz do Azure. Quando você remove um certificado raiz, os clientes que têm um certificado gerado a partir dessa raiz não serão capaz de tooauthenticate e, portanto, não será capaz de tooconnect. Se você quiser um tooauthenticate de cliente e se conectar, você precisa tooinstall um novo certificado de cliente gerado a partir de um certificado raiz confiável tooAzure (carregado).

### <a name="tooadd-a-trusted-root-certificate"></a>tooadd um certificado raiz confiável

Você pode somar too20 confiáveis raiz certificado. cer arquivos tooAzure. Para obter instruções, consulte a seção de saudação [carregar um certificado raiz confiável](#uploadfile) neste artigo.

### <a name="tooremove-a-trusted-root-certificate"></a>tooremove um certificado raiz confiável

1. tooremove um certificado raiz confiável, navegar toohello **configuraçãopontoasite** página do seu gateway de rede virtual.
2. Em Olá **certificado raiz** seção da página hello, localize o certificado de saudação que você deseja tooremove.
3. Clique em Olá reticências próximo toohello certificado e, em seguida, clique em 'Remover'.

## <a name="revokeclient"></a>Revogar um certificado de cliente

É possível revogar certificados de cliente. certificado Olá lista de revogação permite que você tooselectively negar conectividade ponto a Site com base em certificados de cliente individuais. Isso é diferente da remoção de um certificado raiz confiável. Se você remover um certificado de raiz confiável. cer do Azure, ela revoga o acesso de Olá para todos os certificados de cliente gerado/assinado pelo certificado de raiz revogado hello. Revogar um certificado de cliente, em vez de certificado de raiz hello, permite Olá outros certificados que foram gerados a partir do certificado de raiz de saudação toocontinue toobe usado para autenticação.

uma prática comum Olá é o acesso de toomanage de certificado toouse Olá raiz nos níveis de equipe ou organização, durante o uso de certificados do cliente revogados para controle de acesso refinado sobre usuários individuais.

### <a name="toorevoke-a-client-certificate"></a>toorevoke um certificado de cliente

Você pode revogar um certificado de cliente, adicionando a lista de revogação de toohello Olá impressão digital.

1. Recupere a impressão digital do certificado de cliente hello. Para obter mais informações, consulte [como tooretrieve Olá impressão digital de um certificado](https://msdn.microsoft.com/library/ms734695.aspx).
2. Copie o editor de texto Olá informações tooa e remover todos os espaços para que seja uma cadeia de caracteres contínua.
3. Navegue de gateway de rede virtual toohello **-para-site-configuração do ponto de** página. Isso é hello na mesma página que você usou muito[carregar um certificado raiz confiável](#uploadfile).
4. Em Olá **certificados revogados** seção, insira um nome amigável de certificado hello (não tem o CN do certificado Olá toobe).
5. Copie e cole toohello de cadeia de caracteres de impressão digital Olá **impressão digital** campo.
6. impressão digital de saudação valida e é adicionado automaticamente a lista de revogação toohello. Uma mensagem é exibida na tela hello que Olá lista está atualizando. 
7. Após a conclusão da atualização, o certificado de saudação não pode mais ser tooconnect usado. Os clientes que tentam tooconnect usando este certificado recebem uma mensagem dizendo que Olá certificado não é mais válido.

## <a name="faq"></a>Perguntas frequentes sobre Ponto a site

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Próximas etapas
Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais. Para saber mais, veja [Máquinas virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). toounderstand mais sobre redes e máquinas virtuais, consulte [visão geral de rede do Azure e a VM do Linux](../virtual-machines/linux/azure-vm-network-overview.md).
