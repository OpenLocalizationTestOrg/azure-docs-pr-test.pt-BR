---
title: aaaCreate um Gateway de aplicativo do Azure - 2.0 do CLI do Azure | Microsoft Docs
description: "Saiba como toocreate um Application Gateway usando Olá 2.0 de CLI do Azure no Gerenciador de recursos"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 952065586cd87d253882438bb779b768d9fd59fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli-20"></a>Criar um gateway de aplicativo usando Olá 2.0 do CLI do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell do Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Modelo do Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [CLI 1.0 do Azure](application-gateway-create-gateway-cli.md)
> * [CLI 2.0 do Azure](application-gateway-create-gateway-cli.md)

O Gateway de Aplicativo é uma solução de virtualização dedicada que fornece o ADC (controlador de entrega de aplicativos) como serviço, oferecendo várias funcionalidades de balanceamento de carga de camada 7 para o aplicativo.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete

Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

* [1.0 de CLI do Azure](application-gateway-create-gateway-cli-nodejs.md) -nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de hello.
* [2.0 do CLI do Azure](application-gateway-create-gateway-cli.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação

## <a name="prerequisite-install-hello-azure-cli-20"></a>Pré-requisito: Instale Olá 2.0 do CLI do Azure

Olá tooperform as etapas neste artigo, é necessário muito[instalar Olá Interface de linha de comando do Azure para Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

> [!NOTE]
> Se você não tiver uma conta do Azure, crie uma. Inscreva-se em uma [avaliação gratuita aqui](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Cenário

Nesse cenário, você aprenderá como toocreate um gateway de aplicativo usando Olá portal do Azure.

Este cenário:

* Criará um Gateway de Aplicativo com duas instâncias.
* Criará uma rede virtual chamada AdatumAppGatewayVNET, com um bloco CIDR 10.0.0.0/16 reservado.
* Criará uma sub-rede chamada Appgatewaysubnet que usa 10.0.0.0/28 como seu bloco CIDR.

> [!NOTE]
> Testes de configuração adicionais do gateway de aplicativo hello, incluindo integridade personalizado, endereços do pool de back-end e regras adicionais são configuradas após a configuração do gateway de aplicativo hello e não durante a implantação inicial.

## <a name="before-you-begin"></a>Antes de começar

O Gateway de Aplicativo do Azure requer sua própria sub-rede. Ao criar uma rede virtual, certifique-se de que você deixe suficiente toohave de espaço de endereço várias sub-redes. Depois de implantar um aplicativo gateway tooa de sub-rede, os gateways de aplicativos adicionais somente podem ser adicionados a sub-rede toohello.

## <a name="log-in-tooazure"></a>Faça logon no tooAzure

Olá abrir **Prompt de comando do Microsoft Azure**e faça logon. 

```azurecli-interactive
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

## <a name="create-hello-resource-group"></a>Criar grupo de recursos de saudação

Antes de criar o gateway de aplicativo hello, um grupo de recursos é criado o gateway de aplicativo hello toocontain. Veja a seguir de Olá comando hello.

```azurecli-interactive
az group create --name myresourcegroup --location "eastus"
```

## <a name="create-hello-application-gateway"></a>Criar hello application gateway

endereços IP de saudação usados para Olá back-end são endereços IP de saudação do servidor back-end. Esses valores podem ser qualquer IPs privados na rede virtual hello, ips públicos ou nomes de domínio totalmente qualificado para seus servidores de back-end. Olá exemplo a seguir cria um application gateway com definições de configuração adicionais para as configurações de http, portas e regras.

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet" \
--subnet-address-prefix "10.0.0.0/28" \
--servers 10.0.0.4 10.0.0.5 \
--capacity 2 \
--sku Standard_Small \
--http-settings-cookie-based-affinity Enabled \
--http-settings-protocol Http \
--frontend-port 80 \
--routing-rule-type Basic \
--http-settings-port 80 \
--public-ip-address "pip2" \
--public-ip-address-allocation "dynamic" \

```

Olá, exemplo anterior mostra várias propriedades que não são necessárias durante a criação de saudação de um application gateway. Olá exemplo de código a seguir cria um application gateway com informações de saudação necessária.

```azurecli-interactive
az network application-gateway create \
--name "AdatumAppGateway" \
--location "eastus" \
--resource-group "myresourcegroup" \
--vnet-name "AdatumAppGatewayVNET" \
--vnet-address-prefix "10.0.0.0/16" \
--subnet "Appgatewaysubnet \
--subnet-address-prefix "10.0.0.0/28" \
--servers "10.0.0.5"  \
--public-ip-address pip
```
 
> [!NOTE]
> Para obter uma lista de parâmetros que podem ser fornecidas durante a saudação criação executar comando a seguir: `az network application-gateway create --help`.

Este exemplo cria um application gateway básico com configurações padrão para o ouvinte hello, pool de back-end, configurações de http de back-end e regras. Você pode modificar essas configurações toosuit sua implantação quando Olá provisionamento é bem-sucedido.
Se você já tiver o aplicativo da web definido com o pool de back-end de saudação em Olá anterior etapas, uma vez criadas, balanceamento de carga começa.

## <a name="get-application-gateway-dns-name"></a>Obter um nome DNS de Gateway de Aplicativo

Depois de criar o gateway hello, Olá próxima etapa é tooconfigure Olá front-end para comunicação. Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável. os usuários finais de tooensure pode pressionar o gateway de aplicativo hello, um registro CNAME pode ser usado toopoint toohello ponto de extremidade público do gateway de aplicativo hello. [Configurando um nome de domínio personalizado no Azure](../dns/dns-custom-domain.md). tooconfigure um alias, recuperar detalhes do gateway de aplicativo hello e seu nome de IP/DNS associado usando Olá PublicIPAddress elemento toohello anexado application gateway. nome DNS do gateway do aplicativo Hello deve ser usado toocreate um registro CNAME, qual nome DNS pontos Olá duas web aplicativos toothis. uso de saudação de registros de um não é recomendável porque Olá VIP pode ser alterado na reinicialização do application gateway.


```azurecli-interactive
az network public-ip show --name "pip" --resource-group "AdatumAppGatewayRG"
```

```
{
  "dnsSettings": {
    "domainNameLabel": null,
    "fqdn": "8c786058-96d4-4f3e-bb41-660860ceae4c.cloudapp.net",
    "reverseFqdn": null
  },
  "etag": "W/\"3b0ac031-01f0-4860-b572-e3c25e0c57ad\"",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/publicIPAddresses/pip2",
  "idleTimeoutInMinutes": 4,
  "ipAddress": "40.121.167.250",
  "ipConfiguration": {
    "etag": null,
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/AdatumAppGatewayRG/providers/Microsoft.Network/applicationGateways/AdatumAppGateway2/frontendIPConfigurations/appGatewayFrontendIP",
    "name": null,
    "privateIpAddress": null,
    "privateIpAllocationMethod": null,
    "provisioningState": null,
    "publicIpAddress": null,
    "resourceGroup": "AdatumAppGatewayRG",
    "subnet": null
  },
  "location": "eastus",
  "name": "pip2",
  "provisioningState": "Succeeded",
  "publicIpAddressVersion": "IPv4",
  "publicIpAllocationMethod": "Dynamic",
  "resourceGroup": "AdatumAppGatewayRG",
  "resourceGuid": "3c30d310-c543-4e9d-9c72-bbacd7fe9b05",
  "tags": {
    "cli[2] owner[administrator]": ""
  },
  "type": "Microsoft.Network/publicIPAddresses"
}
```

## <a name="delete-all-resources"></a>Excluir todos os recursos

toodelete todos os recursos criados neste artigo, Olá concluir as etapas a seguir:

```azurecli-interactive
az group delete --name AdatumAppGatewayRG
```
 
## <a name="next-steps"></a>Próximas etapas

Saiba como sondas de integridade personalizado toocreate visitando [criar um teste de integridade personalizado](application-gateway-create-probe-portal.md)

Saiba como tooconfigure descarregamento de SSL e take Olá cara SSL descriptografia desativada, os servidores web visitando [configurar descarregamento de SSL](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli/scenario.png
[1]: ./media/application-gateway-create-gateway-cli/figure1.png
[2]: ./media/application-gateway-create-gateway-cli/figure2.png
[3]: ./media/application-gateway-create-gateway-cli/figure3.png
