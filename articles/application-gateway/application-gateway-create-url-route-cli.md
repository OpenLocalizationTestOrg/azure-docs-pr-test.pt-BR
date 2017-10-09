---
title: aaaCreate um application gateway usando a URL de roteamento regras - 2.0 do CLI do Azure | Microsoft Docs
description: "Esta página fornece instruções toocreate, configure um gateway de aplicativo do Azure usando regras de roteamento de URL"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: gwallace
ms.openlocfilehash: 335b52be258945e1172eb0252b732e0e6ecb2ef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing-with-azure-cli-20"></a>Criar um Gateway de Aplicativo usando roteamento com base em caminho com a CLI do Azure 2.0

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-create-url-route-portal.md)
> * [PowerShell do Azure Resource Manager](application-gateway-create-url-route-arm-ps.md)
> * [CLI 2.0 do Azure](application-gateway-create-url-route-cli.md)

Roteamento baseado no caminho de URL permite que você tooassociate rotas com base no caminho de URL de saudação de uma solicitação Http. Ele verifica se há um pool de back-end de tooa rota configurado para URL Olá apresentado em Olá Application Gateway e envia Olá toohello de tráfego de rede definida pelo pool de back-end. Um uso comum para roteamento baseado em URL é equilibrar solicitações de tooload para pools de toodifferent de diferentes tipos de conteúdo do servidor de back-end.

Roteamento baseado em URL apresenta um novo gateway de tooapplication do tipo de regra. O gateway de aplicativo tem dois tipos de regra: básica e PathBasedRouting. Tipo de regra básica fornece serviço de round-robin para Olá back-end pools ao PathBasedRouting distribuição de rodízio tooround Além disso, também leva padrão de caminho da URL de solicitação de saudação em consideração ao escolher o pool de back-end de saudação.

## <a name="scenario"></a>Cenário

Em Olá exemplo a seguir, o Application Gateway está servindo tráfego para contoso.com com dois grupos de servidor back-end: um pool de servidor padrão e um pool de servidores de imagem.

As solicitações para http://contoso.com/image * são roteadas pool de servidores tooimage (imagesBackendPool), se hello não correspondência de padrão de caminho, um pool de servidores padrão (appGatewayBackendPool) está selecionado.

![roteamento de url](./media/application-gateway-create-url-route-cli/scenario.png)

## <a name="log-in-tooazure"></a>Faça logon no tooAzure

Olá abrir **Prompt de comando do Microsoft Azure**e faça logon. 

```azurecli
az login -u "username"
```

> [!NOTE]
> Você também pode usar `az login` sem comutador hello para logon de dispositivo que requer a inserção de um código em aka.ms/devicelogin.

Depois que você digitar Olá anterior de exemplo, um código é fornecido. Navegue toohttps://aka.ms/devicelogin em um processo de logon do navegador toocontinue hello.

![cmd mostrando logon de dispositivo][1]

No navegador de hello, insira o código Olá recebido. Você é redirecionado tooa na página de entrada.

![código de tooenter do navegador][2]

Depois que o código de saudação foi inserido você entrou, Olá fechar navegador toocontinue com cenário de saudação.

![conectado com êxito][3]

## <a name="add-a-path-based-rule-tooan-existing-application-gateway"></a>Adicionar um gateway de aplicativos existentes baseados no caminho de regra tooan

Criar um Gateway de Aplicativo com uma regra com base em caminho definida

### <a name="create-a-new-back-end-pool"></a>Criar um novo pool de back-end

Definir configuração de gateway do aplicativo **imagesBackendPool** Olá com balanceamento de carga de tráfego de rede no pool de back-end de saudação. Neste exemplo, você deve configurar as configurações de pool de back-end diferente para o novo pool de back-end hello. Cada pool de back-end pode ter sua própria configuração de pool de back-end.  Configurações de HTTP de back-end são usadas por membros do pool regras tooroute tráfego toohello correto de back-end. Isso determina o protocolo de saudação e a porta que é usada ao enviar tráfego toohello membros do pool de back-end. Sessões baseada em cookie também são determinadas pelas configurações de HTTP de back-end de saudação.  Se habilitada, a afinidade de sessão baseada em cookie envia tráfego toohello mesmo back-end como solicitações anteriores para cada pacote.

```azurecli-interactive
az network application-gateway address-pool create \
--gateway-name AdatumAppGateway \
--name imagesBackendPool  \
--resource-group myresourcegroup \
--servers 10.0.0.6 10.0.0.7
```

### <a name="create-a-new-front-end-port"></a>Criar uma nova porta de front-end

Configure portas de front-end Olá para o application gateway. objeto de configuração de porta de front-end de saudação é usado por um ouvinte toodefine qual porta Olá Application Gateway escuta para o tráfego no ouvinte Olá.

```azurecli-interactive
az network application-gateway frontend-port create --port 82 --gateway-name AdatumAppGateway --resource-group myresourcegroup --name port82
```

### <a name="create-a-new-listener"></a>Criar um novo ouvinte

Configure o ouvinte de saudação. Esta etapa configura um ouvinte de Olá para o endereço IP público de saudação e a porta usada tooreceive tráfego de rede. saudação de exemplo a seguir usa a configuração de IP de front-end de Olá configurado anteriormente, a configuração de porta de front-end e um protocolo (http ou https) e configura o ouvinte hello. Neste exemplo, o ouvinte de saudação escuta tooHTTP tráfego na porta 82 no endereço IP público Olá criado anteriormente.

```azurecli-interactive
az network application-gateway http-listener create --name imageListener --frontend-ip appGatewayFrontendIP  --frontend-port port82 --resource-group myresourcegroup --gateway-name AdatumAppGateway
```

### <a name="create-hello-url-path-map"></a>Criar um mapa de caminho de Url Olá

Configure caminhos de regra de URL para pools de back-end de saudação. Esta etapa configura o caminho relativo do hello usado pelo mapeamento de saudação do aplicativo gateway toodefine entre o caminho da URL e qual pool de back-end recebe o tráfego de entrada hello toohandle.

> [!IMPORTANT]
> Cada caminho deve começar com / e coloque-Olá somente um "\*" é permitido, está na extremidade hello. Exemplos válidos são /xyz, /xyz* ou /xyz/*. Olá alimentada correspondente do caminho toohello de cadeia de caracteres não inclui qualquer texto após Olá primeiro "?" ou "#" e os caracteres não são permitidos. 

Olá, exemplo a seguir cria uma regra para "imagens / *" caminho de roteamento de tráfego tooback-end "imagesBackendPool". Essa regra garante que o tráfego para cada conjunto de urls é roteado toohello back-end. Por exemplo, http://adatum.com/images/figure1.jpg fica muito "imagesBackendPool". Se o caminho Olá não corresponde a qualquer uma das regras de caminho predefinido Olá, configuração de mapa de caminho de regra Olá também configura um pool de endereços de back-end do padrão. Por exemplo, http://adatum.com/shoppingcart/test.html irá toopool1 conforme ele é definido como o pool padrão de saudação para tráfego não correspondente.

```azurecli-interactive
az network application-gateway url-path-map create \
--gateway-name AdatumAppGateway \
--name imagespathmap \
--paths /images/* \
--resource-group myresourcegroup2 \
--address-pool imagesBackendPool \
--default-address-pool appGatewayBackendPool \
--default-http-settings appGatewayBackendHttpSettings \
--http-settings appGatewayBackendHttpSettings \
--rule-name images
```

## <a name="next-steps"></a>Próximas etapas

Se você quiser toolearn sobre descarregamento de Secure Sockets Layer (SSL), consulte [Configure um gateway de aplicativo para descarregamento SSL](application-gateway-ssl-cli.md).


[scenario]: ./media/application-gateway-create-url-route-cli/scenario.png
[1]: ./media/application-gateway-create-url-route-cli/figure1.png
[2]: ./media/application-gateway-create-url-route-cli/figure2.png
[3]: ./media/application-gateway-create-url-route-cli/figure3.png
