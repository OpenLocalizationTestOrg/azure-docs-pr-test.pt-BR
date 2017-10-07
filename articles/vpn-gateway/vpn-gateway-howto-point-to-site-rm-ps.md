---
title: "Conecte-se a uma rede virtual do Azure usando o Site de ponto de tooan do computador e autenticação de certificado: PowerShell | Microsoft Docs"
description: "Conecte uma rede virtual do computador tooyour com segurança por meio da criação de uma conexão de gateway VPN ponto a Site usando a autenticação de certificado. Este artigo se aplica o modelo de implantação do Gerenciador de recursos de toohello e usa o PowerShell."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a>Configurar uma conexão de ponto para Site tooa VNet usando a autenticação de certificado: PowerShell

Este artigo mostra como uma rede virtual com uma conexão ponto a Site na implantação do Gerenciador de recursos de saudação do toocreate modelo usando o PowerShell. Essa configuração usa Olá tooauthenticate de certificados conexão cliente. Você também pode criar essa configuração usando uma ferramenta de implantação diferente ou um modelo de implantação, selecionando uma opção diferente de saudação lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Portal do Azure (clássico)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Um gateway VPN ponto a Site (P2S) permite criar uma rede virtual de tooyour de conexão segura de um computador cliente individual. Conexões VPN Site a ponto são úteis quando você deseja tooconnect tooyour VNet de um local remoto, como quando você está comunicando em casa ou em uma conferência. Uma VPN de P2S também é toouse uma solução útil em vez de uma VPN Site a Site quando você tiver apenas alguns clientes que precisam de tooconnect tooa VNet.

Usa P2S Olá SSTP Secure Socket Tunneling Protocol (), que é um protocolo VPN baseada em SSL. Uma conexão VPN de P2S é estabelecido pela iniciá-lo do computador do cliente de saudação.

![Conectar uma rede virtual do Azure - diagrama de conexão de ponto para Site de tooan do computador](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

Conexões de autenticação de certificado de ponto a Site requerem a seguir hello:

* Gateway de VPN RouteBased.
* Olá chave pública (arquivo. cer) para um certificado raiz, que é carregado tooAzure. Depois que o certificado Olá é carregado, ele é considerado um certificado confiável e é usado para autenticação.
* Um certificado de cliente que é gerado a partir do certificado de raiz de saudação e instalado em cada computador cliente que se conectam toohello VNet. Esse certificado é usado para autenticação do cliente.
* Um pacote de configuração de cliente VPN. pacote de configuração de cliente VPN Olá contém informações necessárias Olá Olá cliente tooconnect toohello VNet. pacote de saudação configura o cliente VPN existente Olá que é nativa toohello sistema operacional Windows. Cada cliente que se conecta deve ser configurado usando o pacote de configuração de saudação.

As conexões Ponto a Site não exigem um dispositivo VPN ou um endereço IP voltado para o público local. Olá conexão VPN é criado por protocolo SSTP (Secure Socket Tunneling Protocol). No lado do servidor de saudação, há suporte para as versões 1.0, 1.1 e 1.2 do SSTP. cliente Olá decide qual toouse de versão. Por padrão, para Windows 8.1 e posterior, o SSTP usa 1.2. 

Para obter mais informações sobre conexões ponto a Site, consulte Olá [ponto a Site perguntas frequentes sobre](#faq) final Olá deste artigo.

## <a name="before-beginning"></a>Antes de começar

* Verifique se você tem uma assinatura do Azure. Se ainda não tiver uma assinatura do Azure, você poderá ativar os [Benefícios do assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) ou inscrever-se para obter uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial).
* Instale a versão mais recente Olá de saudação cmdlets do PowerShell do Gerenciador de recursos do Azure. Para obter mais informações sobre como instalar os cmdlets do PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

### <a name="example"></a>Valores de exemplo

Você pode usar toocreate valores de exemplo hello um ambiente de teste, ou consulte valores toothese toobetter entender exemplos Olá neste artigo. Vamos definir variáveis de saudação na seção [1](#declare) artigo hello. Você pode usar etapas hello como uma passo a passo e usar valores de saudação sem alterá-los ou alterá-los tooreflect seu ambiente. 

* **Nome: VNet1**
* **Espaço de endereço: 192.168.0.0/16** e **10.254.0.0/16**<br>Neste exemplo, podemos usar mais de um tooillustrate de espaço de endereço que essa configuração funciona com vários espaços de endereço. No entanto, vários espaços de endereço não são necessários para esta configuração.
* **Nome da sub-rede: FrontEnd**
  * **Intervalo de endereços da sub-rede: 192.168.1.0/24**
* **Nome da sub-rede: BackEnd**
  * **Intervalo de endereços da sub-rede: 10.254.1.0/24**
* **Nome da sub-rede: GatewaySubnet**<br>nome da sub-rede Olá *GatewaySubnet* é obrigatório para Olá toowork de gateway VPN.
  * **Intervalo de endereços da GatewaySubnet: 192.168.200.0/24** 
* **Pool de endereços do cliente VPN: 172.16.201.0/24**<br>Clientes VPN que se conectam toohello usando esta conexão ponto a Site de rede virtual recebem um endereço IP hello pool de endereços de cliente VPN.
* **Assinatura:** se você tiver mais de uma assinatura, verifique se você estiver usando Olá correto.
* **Grupo de Recursos: TestRG**
* **Local: Leste dos EUA**
* **Servidor DNS: Endereço IP** do servidor DNS Olá que você deseja toouse para resolução de nome.
* **Nome de GW: Vnet1GW**
* **Nome do IP público: VNet1GWPIP**
* **VpnType: RouteBased** 

## <a name="declare"></a>1. Fazer logon e definir variáveis

Nesta seção, faça logon e declarar Olá valores usados para essa configuração. Olá declarado valores são usados em scripts de exemplo hello. Altere Olá valores tooreflect seu próprio ambiente. Ou, você pode usar Olá declarado valores e percorrer as etapas de saudação como um exercício.

1. Abra o console do PowerShell com privilégios elevados e faça logon no tooyour conta do Azure. Esse cmdlet solicita credenciais de logon de saudação. Após o logon, ele baixa as configurações de conta para que fiquem disponível tooAzure PowerShell.

  ```powershell
  Login-AzureRmAccount
  ```
2. Obtenha uma lista das assinaturas do Azure.

  ```powershell
  Get-AzureRmSubscription
  ```
3. Especifique que você deseja toouse de assinatura de saudação.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. Declare variáveis Olá que você deseja toouse. Use Olá exemplo a seguir, substituindo valores de saudação para seu próprio quando necessário.

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <a name="ConfigureVNet"></a>2. Configurar uma rede virtual

1. Crie um grupos de recursos.

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. Criar configurações de sub-rede da rede virtual do hello, nomeá-los de saudação *front-end*, *back-end*, e *GatewaySubnet*. Esses prefixos devem fazer parte da saudação espaço de endereço de rede virtual que é declarada.

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. Crie rede virtual hello.

  Neste exemplo, o servidor DNS de saudação é opcional. A especificação de um valor não cria um novo servidor DNS. Olá endereço IP do servidor DNS que você especificar deve ser um servidor DNS que pode resolver nomes Olá para recursos de saudação que você está se conectando. Neste exemplo, usamos um endereço IP privado, mas é provável que isso não é Olá endereço IP do servidor DNS. Ser toouse-se de que seus próprios valores.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. Especifica variáveis de saudação para rede virtual hello, que você criou.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. Um gateway de VPN deve ter um endereço IP público. Você primeiro solicitar o recurso de endereço IP hello e, em seguida, consulte tooit ao criar o gateway de rede virtual. endereço IP de saudação é atribuído dinamicamente recursos toohello ao gateway de VPN Olá é criado. O gateway de VPN atualmente suporta apenas alocação de endereços IP público *Dinâmico*. Você não pode solicitar uma atribuição de endereço IP Público Estático. No entanto, isso não significa que o endereço IP de saudação alterado depois que ele foi atribuído tooyour gateway VPN. somente tempo de saudação alterações de endereço IP público hello quando é Olá gateway é excluído e criado novamente. Isso não altera o redimensionamento, a redefinição ou outras manutenções/atualizações internas do seu gateway de VPN.

  Solicite um endereço IP público atribuído dinamicamente.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <a name="creategateway"></a>3. Criar gateway VPN Olá

Configurar e criar o gateway de rede virtual Olá para sua rede virtual.

* Olá *- GatewayType* devem ser **Vpn** e hello *- VpnType* devem ser **RouteBased**.
* Um gateway de VPN pode levar até too45 toocomplete de minutos, dependendo da saudação [sku de gateway](vpn-gateway-about-vpn-gateway-settings.md) você selecionar.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <a name="addresspool"></a>4. Adicionar pool de endereços de cliente VPN Olá

Depois que o gateway de VPN Olá termina de criar, você pode adicionar pool de endereços de cliente VPN hello. Olá pool de endereços de cliente VPN é o intervalo de saudação do qual os clientes VPN Olá recebem um endereço IP ao se conectar. Use um intervalo de endereços IP particular que não coincida com hello no local que você se conectar de, ou com hello VNet que você deseja tooconnect para. Neste exemplo, Olá pool de endereços de cliente VPN está declarado como um [variável](#declare) na etapa 1.

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <a name="Certificates"></a>5. Gerar certificados

Certificados são usados por clientes VPN do Azure tooauthenticate para VPNs ponto a Site. Você carregar as informações de chave pública do hello de saudação tooAzure de certificado de raiz. chave pública Olá é considerado 'confiável'. Certificados de cliente devem ser gerados a partir do certificado de raiz confiável do hello e, em seguida, em cada computador cliente no repositório de certificados de usuário/pessoal de certificados atual hello. certificado de saudação é cliente de saudação tooauthenticate usado quando ele inicia uma conexão toohello VNet. 

Se você usa certificados autoassinados, eles devem ser criados usando parâmetros específicos. Você pode criar um certificado autoassinado usando instruções Olá para [PowerShell e Windows 10](vpn-gateway-certificates-point-to-site.md), ou, se você não tiver o Windows 10, você pode usar [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). É importante que você siga as etapas de saudação nas instruções de saudação ao gerar os certificados raiz autoassinados e certificados de cliente. Caso contrário, certificados Olá que gerar não será compatíveis com conexões de P2S, e você receberá um erro de conexão.

### <a name="cer"></a>1. Obter arquivo hello. cer certificado de raiz de saudação

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <a name="generate"></a>2. Gerar um certificado de cliente

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>6. Carregar Olá raiz certificado informações de chave pública

Verifique se a criação do gateway de VPN foi concluída. Depois de concluído, você pode carregar o arquivo. cer de saudação (que contém as informações de chave pública Olá) para um tooAzure de certificado raiz confiável. Uma vez carregado o arquivo a.cer, Azure pode usá-lo tooauthenticate clientes que instalaram um certificado de cliente gerado a partir do certificado de raiz confiável do hello. Você pode carregar arquivos de certificado raiz confiável adicionais - tooa total de 20 - posteriormente, se necessário.

1. Declare a variável de saudação para seu nome de certificado, substituindo o valor de saudação com seus próprios.

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. Substitua o caminho do arquivo hello com seus próprios e execute Olá cmdlets.

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. Carregar Olá tooAzure de informações de chave pública. Depois que as informações de certificado de saudação são carregadas, o Azure considera esse toobe um certificado raiz confiável.

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <a name="clientconfig"></a>7. Baixe o pacote de configuração de cliente VPN Olá

tooconnect tooa VNet usando uma VPN ponto a Site, cada cliente deve instalar um pacote de configuração de cliente que configura o cliente VPN nativo de saudação com configurações de saudação e arquivos de rede virtual do toohello tooconnect necessário. pacote de configuração de cliente VPN Olá configura native cliente de VPN do Windows hello, não instala um cliente VPN novo ou diferente. 

Você pode usar o hello a mesma configuração de cliente VPN do pacote em cada computador cliente, como versão Olá corresponde a arquitetura de saudação para cliente hello. Para lista de saudação dos sistemas operacionais cliente com suporte, consulte Olá [conexõespontoaSiteperguntas frequentes sobre](#faq) final Olá deste artigo.

1. Depois de saudação gateway foi criado, você pode gerar e baixar o pacote de configuração de cliente de saudação. Este exemplo baixa o pacote de saudação para clientes de 64 bits. Se desejar que o cliente de 32 bits do toodownload hello, substitua 'Amd64' 'x86'. Você também pode baixar o cliente VPN hello usando Olá portal do Azure.

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. Copie e cole o link Olá retornado pacote tooa web navegador toodownload hello, tomando cuidado aspas de saudação tooremove ao redor de link de saudação. 
3. Baixe e instale o pacote de saudação no computador do cliente de saudação. Se vir um pop-up do SmartScreen, clique em **Mais informações** e em **Executar mesmo assim**. Você também pode salvar Olá pacote tooinstall em outros computadores cliente.
4. No computador do cliente hello, navegue muito**as configurações de rede** e clique em **VPN**. Olá conexão VPN mostra o nome de saudação da rede virtual de saudação que ele se conecta ao.

## <a name="clientcertificate"></a>8. Instalar um certificado do cliente exportado

Se você quiser toocreate um P2S conexão de um computador cliente que não sejam Olá você usado certificados de cliente toogenerate Olá, é necessário tooinstall um certificado de cliente. Ao instalar um certificado de cliente, é necessário senha Olá que foi criada quando o certificado de cliente Olá foi exportado. Normalmente, ele é apenas uma questão de duas vezes em Olá certificado e instalá-lo.

Verifique se o certificado de cliente hello exportado como um. pfx juntamente com a cadeia de certificado inteiro hello (que é o padrão de saudação). Caso contrário, informações de certificado raiz Olá não está presentes no computador do cliente hello e cliente Olá não será capaz de tooauthenticate corretamente. Para saber mais informações consulte, [Instalar um certificado de cliente exportado](vpn-gateway-certificates-point-to-site.md#install). 

## <a name="connect"></a>9. Conecte-se tooAzure

1. tooconnect tooyour VNet, no computador do cliente hello, navegar tooVPN conexões e localize a conexão de VPN Olá que você criou. Ele é chamado hello mesmo nome de sua rede virtual. Clique em **Conectar**. Pode aparecer uma mensagem pop-up que refere-se o certificado de saudação toousing. Clique em **continuar** privilégios elevados do toouse. 
2. Em Olá **Conexão** página de status, clique em **conectar** toostart conexão de saudação. Se você vir um **Selecionar certificado** tela, verifique se mostrando de certificado de cliente Olá Olá um que você deseja toouse tooconnect. Se não for, use Olá seta suspensa tooselect Olá correto certificado e, em seguida, clique em **Okey**.

  ![Cliente VPN conecta tooAzure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. A conexão é estabelecida.

  ![Conexão estabelecida](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Solucionar problemas de conexões P2S

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>10. Verificar a conexão

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

## <a name="addremovecert"></a>Adicionar ou remover um certificado raiz

Você pode adicionar e remover um certificado raiz do Azure. Quando você remove um certificado raiz, os clientes que têm um certificado gerado do certificado de raiz de saudação não podem autenticar e não serão capaz de tooconnect. Se você quiser um tooauthenticate de cliente e se conectar, você precisa tooinstall um novo certificado de cliente gerado a partir de um certificado raiz confiável tooAzure (carregado).

### <a name="addtrustedroot"></a>tooadd um certificado raiz confiável

Você pode somar too20 raiz certificado. cer arquivos tooAzure. as etapas a seguir de saudação ajuda a adicionar um certificado raiz:

#### <a name="certmethod1"></a>Método 1

Isso é tooupload de método mais eficiente de saudação um certificado raiz.

1. Prepare tooupload de arquivo. cer hello:

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. Carregar arquivo hello. Você só pode carregar um arquivo por vez.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. tooverify que Olá carregado do arquivo de certificado:

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <a name="certmethod2"></a>Método 2

Esse método é tem mais etapas que o método 1, mas tem Olá mesmo resultado. Ele está incluído no caso de você precisar tooview Olá certificado dados.

1. Criar e preparar Olá nova raiz certificado tooadd tooAzure. Exportar a chave pública do hello como x. 509 codificado de Base 64 (. CER) e abra-o com um editor de texto. Copie os valores hello, conforme mostrado no exemplo a seguir de saudação:

  ![certificado](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > Ao copiar dados do certificado hello, certifique-se de que você copiar o texto de saudação como uma linha contínua sem retornos de carro ou alimentações de linha. Talvez seja necessário toomodify exibição em too'Show de editor de texto de saudação símbolo/Mostrar toosee Olá de carro todos os caracteres retorna e alimentação de linha.
  >
  >

2. Especifique o nome do certificado hello e informações de chave como uma variável. Substitua as informações de saudação com seu próprio, conforme mostrado no hello exemplo a seguir:

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. Adicione novo certificado raiz do hello. Você pode adicionar apenas um certificado por vez.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. Você pode verificar o que novo certificado Olá foi adicionado corretamente usando Olá exemplo a seguir:

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <a name="removerootcert"></a>tooremove um certificado raiz

1. Declare variáveis hello.

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. Remova certificado hello.

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. Saudação de uso tooverify de exemplo que Olá certificado a seguir foi removida com êxito.

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <a name="revoke"></a>Revogar um certificado de cliente

É possível revogar certificados de cliente. certificado Olá lista de revogação permite que você tooselectively negar conectividade ponto a Site com base em certificados de cliente individuais. Isso é diferente da remoção de um certificado raiz confiável. Se você remover um certificado de raiz confiável. cer do Azure, ela revoga o acesso de Olá para todos os certificados de cliente gerado/assinado pelo certificado de raiz revogado hello. Revogar um certificado de cliente, em vez de certificado de raiz hello, permite Olá outros certificados que foram gerados a partir do certificado de raiz de saudação toocontinue toobe usado para autenticação.

uma prática comum Olá é o acesso de toomanage de certificado toouse Olá raiz nos níveis de equipe ou organização, durante o uso de certificados do cliente revogados para controle de acesso refinado sobre usuários individuais.

### <a name="revokeclientcert"></a>toorevoke um certificado de cliente

1. Recupere a impressão digital do certificado de cliente hello. Para obter mais informações, consulte [como tooretrieve Olá impressão digital de um certificado](https://msdn.microsoft.com/library/ms734695.aspx).
2. Copie o editor de texto Olá informações tooa e remover todos os espaços para que seja uma cadeia de caracteres contínua. Essa cadeia de caracteres é declarada como uma variável na próxima etapa do hello.
3. Declare variáveis hello. Verifique se toodeclare Olá impressão digital recuperado na etapa anterior hello.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. Adicione Olá impressão digital toohello lista de certificados revogados. Consulte o "Êxito" quando a impressão digital de saudação foi adicionado.

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. Verifique se que essa impressão digital de saudação foi adicionado toohello lista de revogação de certificado.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. Depois que tiver sido adicionado a impressão digital do hello, certificado Olá não pode mais ser usado tooconnect. Os clientes que tentam tooconnect usando este certificado recebem uma mensagem dizendo que Olá certificado não é mais válido.

### <a name="reinstateclientcert"></a>tooreinstate um certificado de cliente

Você pode restabelecer um certificado de cliente, removendo a impressão digital de saudação da lista de saudação de certificados de cliente revogados.

1. Declare variáveis hello. Verifique se que você declarar Olá correto impressão digital Olá certificado que você deseja tooreinstate.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. Remova a impressão digital do certificado Olá da lista de revogação de certificado Olá.

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. Verifique se a impressão digital de saudação é removido da saudação revogado lista.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <a name="faq"></a>Perguntas frequentes sobre Ponto a site

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Próximas etapas
Quando a conexão for concluída, você pode adicionar máquinas virtuais tooyour as redes virtuais. Para saber mais, veja [Máquinas virtuais](https://docs.microsoft.com/azure/#pivot=services&panel=Compute). toounderstand mais sobre redes e máquinas virtuais, consulte [visão geral de rede do Azure e a VM do Linux](../virtual-machines/linux/azure-vm-network-overview.md).
