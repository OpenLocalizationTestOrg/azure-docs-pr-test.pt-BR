---
title: firewall do aplicativo web aaaConfigure - Gateway de aplicativo do Azure | Microsoft Docs
description: "Este artigo fornece orientação sobre como usar toostart web firewall do aplicativo em um gateway de aplicativo novo ou existente."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: gwallace
ms.openlocfilehash: d5354984760ceab12ed49efa9e18836e9f1d3c96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway-with-azure-cli"></a>Configurar o firewall do aplicativo Web em um Gateway de Aplicativo novo ou existente com a CLI do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-web-application-firewall-portal.md)
> * [PowerShell](application-gateway-web-application-firewall-powershell.md)
> * [CLI do Azure](application-gateway-web-application-firewall-cli.md)

Saiba como toocreate um firewall do aplicativo web habilitado gateway de aplicativo ou adicionar web aplicativo firewall tooan aplicativo gateway existente.

firewall do aplicativo web Hello (WAF) no Gateway de aplicativo do Azure protege os aplicativos da web comuns ataques baseados na web como injeção de SQL, ataques de script entre sites e sequestros de sessão.

O Gateway de Aplicativo do Azure é um balanceador de carga de camada 7. Ele fornece failover, o roteamento de desempenho de solicitações HTTP entre diferentes servidores, independentemente de estarem em nuvem hello ou local. O Gateway de Aplicativo fornece muitos recursos do ADC (controlador de entrega de aplicativos), incluindo o balanceamento de carga de HTTP, a afinidade de sessão baseada em cookies, o descarregamento de protocolo SSL, as sondas de integridade personalizadas, suporte para vários sites e muitos outros. toofind uma lista completa de recursos com suporte, visite: [visão geral do Application Gateway](application-gateway-introduction.md).

Olá artigo a seguir mostra como muito[adicionar web aplicativo firewall tooan aplicativo gateway existente](#add-web-application-firewall-to-an-existing-application-gateway) e [criar um gateway de aplicativo que usa o firewall do aplicativo web](#create-an-application-gateway-with-web-application-firewall).

![imagem de cenário][scenario]

## <a name="prerequisite-install-hello-azure-cli-20"></a>Pré-requisito: Instale Olá 2.0 do CLI do Azure

Olá tooperform as etapas neste artigo, é necessário muito[instalar Olá Interface de linha de comando do Azure para Mac, Linux e Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="waf-configuration-differences"></a>Diferenças de configuração do WAF

Se você leu [criar um Gateway de aplicativo com a CLI do Azure](application-gateway-create-gateway-cli.md), entender Olá SKU configurações tooconfigure durante a criação de um application gateway. WAF fornece configurações adicionais toodefine ao configurar um application gateway Olá SKU. Não há nenhuma outra alteração que você fizer no próprio gateway de aplicativo hello.

| **Configuração** | **Detalhes**
|---|---|
|**SKU** |Um gateway de aplicativo normal sem WAF dá suporte aos tamanhos **Standard\_Small**, **Standard\_Medium** e **Standard\_Large**. Com a introdução de saudação do WAF, há duas SKUs adicionais, **WAF\_médio** e **WAF\_grande**. Não há suporte para WAF em gateways de aplicativo pequenos.|
|**Modo** | Essa configuração é o modo de saudação do WAF. Os valores permitidos são **detecção** e **prevenção**. Quando WAF estiver configurado no modo de detecção, todas as ameaças são armazenadas em um arquivo de log. No modo de prevenção, eventos ainda estão conectados, mas invasor Olá recebe uma resposta de não autorizado 403 do gateway de aplicativo hello.|

## <a name="add-web-application-firewall-tooan-existing-application-gateway"></a>Adicionar web aplicativo firewall tooan aplicativo gateway existente

Olá siga alterações de comando de um gateway de aplicativo habilitado do tooa WAF de gateway padrão de aplicativo existente.

```azurecli-interactive
#!/bin/bash

az network application-gateway waf-config set \
  --enabled true \
  --firewall-mode Prevention \
  --gateway-name "AdatumAppGateway" \
  --resource-group "AdatumAppGatewayRG"
```

Esse comando atualiza o gateway de aplicativo hello com o firewall do aplicativo web. Visite [Application Gateway Diagnostics](application-gateway-diagnostics.md) toounderstand como tooview logs para o gateway de aplicativo. Devido a natureza de segurança toohello de WAF, logs necessidade toobe revisado regularmente toounderstand postura de segurança de saudação de seus aplicativos web.

## <a name="create-an-application-gateway-with-web-application-firewall"></a>Criar um Gateway de Aplicativo com o firewall do aplicativo Web

saudação de comando a seguir cria um Application Gateway com o firewall do aplicativo web.

```azurecli-interactive
#!/bin/bash

az network application-gateway create \
  --name "AdatumAppGateway2" \
  --location "eastus" \
  --resource-group "AdatumAppGatewayRG" \
  --vnet-name "AdatumAppGatewayVNET2" \
  --vnet-address-prefix "10.0.0.0/16" \
  --subnet "Appgatewaysubnet2" \
  --subnet-address-prefix "10.0.0.0/28" \
 --servers "10.0.0.5 10.0.0.4" \
  --capacity 2 
  --sku "WAF_Medium" \
  --http-settings-cookie-based-affinity "Enabled" \
  --http-settings-protocol "Http" \
  --frontend-port "80" \
  --routing-rule-type "Basic" \
  --http-settings-port "80" \
  --public-ip-address "pip2" \
  --public-ip-address-allocation "dynamic" \
  --tags "cli[2] owner[administrator]"
```

> [!NOTE]
> Gateways de aplicativo criados com a configuração de firewall de aplicativo Olá web básico são configurados com CRS 3.0 para proteção.

## <a name="get-application-gateway-dns-name"></a>Obter um nome DNS de Gateway de Aplicativo

Depois de criar o gateway hello, Olá próxima etapa é tooconfigure Olá front-end para comunicação. Ao usar um IP público, o gateway de aplicativo requer um nome DNS atribuído dinamicamente, o que não é amigável. os usuários finais de tooensure pode pressionar o gateway de aplicativo hello, um registro CNAME pode ser usado toopoint toohello ponto de extremidade público do gateway de aplicativo hello. [Configurando um nome de domínio personalizado no Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure um registro CNAME, recuperar detalhes do gateway de aplicativo hello e seu nome de IP/DNS associado usando Olá PublicIPAddress elemento toohello anexado application gateway. nome DNS do gateway do aplicativo Hello deve ser usado toocreate um registro CNAME, qual nome DNS pontos Olá duas web aplicativos toothis. uso de saudação de registros de um não é recomendável porque Olá VIP pode ser alterado na reinicialização do application gateway.

```azurecli-interactive
#!/bin/bash

az network public-ip show \
  --name pip2 \
  --resource-group "AdatumAppGatewayRG"
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

## <a name="next-steps"></a>Próximas etapas

Saiba como as regras de toocustomize WAF visitando: [personalizar regras de firewall do aplicativo web por meio de hello Azure CLI 2.0](application-gateway-customize-waf-rules-cli.md).

[scenario]: ./media/application-gateway-web-application-firewall-cli/scenario.png
