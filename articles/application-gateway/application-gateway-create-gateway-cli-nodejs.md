---
title: aaaCreate um Gateway de aplicativo do Azure - 1.0 da CLI do Azure | Microsoft Docs
description: "Saiba como toocreate um Application Gateway usando Olá 1.0 de CLI do Azure no Gerenciador de recursos"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c2f6516e-3805-49ac-826e-776b909a9104
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3c0d2d96b6be404d0372d00f0deb2a32959ca419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-by-using-hello-azure-cli"></a>Criar um gateway de aplicativo usando Olá CLI do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](application-gateway-create-gateway-portal.md)
> * [PowerShell do Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Modelo do Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [CLI 1.0 do Azure](application-gateway-create-gateway-cli.md)
> * [CLI 2.0 do Azure](application-gateway-create-gateway-cli.md)
> 
> 

O Gateway de Aplicativo do Azure é um balanceador de carga de camada 7. Ele fornece failover, o roteamento de desempenho de solicitações HTTP entre diferentes servidores, independentemente de estarem em nuvem hello ou local. Gateway de aplicativo tem Olá recursos de entrega de aplicativos a seguir: HTTP carregar testes de integridade personalizado de balanceamento, afinidade de sessão baseada em cookie e descarregamento de Secure Sockets Layer (SSL) e suporte para vários locais.

## <a name="prerequisite-install-hello-azure-cli"></a>Pré-requisito: Instale Olá CLI do Azure

Olá tooperform as etapas neste artigo, é necessário muito[instalar Olá Interface de linha de comando do Azure para Mac, Linux e Windows (Azure CLI)](../xplat-cli-install.md) e você precisa de muito[logon tooAzure](../xplat-cli-connect.md). 

> [!NOTE]
> Se você não tiver uma conta do Azure, crie uma. Inscreva-se em uma [avaliação gratuita aqui](../active-directory/sign-up-organization.md).

## <a name="scenario"></a>Cenário

Nesse cenário, você aprenderá como toocreate um gateway de aplicativo usando Olá portal do Azure.

Este cenário:

* Criará um Gateway de Aplicativo com duas instâncias.
* Criar uma rede virtual chamada ContosoVNET com um bloco CIDR 10.0.0.0/16 reservado.
* Crie uma sub-rede chamada subnet01 que use 10.0.0.0/28 como bloco CIDR.

> [!NOTE]
> Testes de configuração adicionais do gateway de aplicativo hello, incluindo integridade personalizado, endereços do pool de back-end e regras adicionais são configuradas após a configuração do gateway de aplicativo hello e não durante a implantação inicial.

## <a name="before-you-begin"></a>Antes de começar

O Gateway de Aplicativo do Azure requer sua própria sub-rede. Ao criar uma rede virtual, certifique-se de que você deixe suficiente toohave de espaço de endereço várias sub-redes. Depois de implantar um aplicativo gateway tooa de sub-rede, os gateways de aplicativos adicionais só são toobe capaz de adicionar sub-rede toohello.

## <a name="log-in-tooazure"></a>Faça logon no tooAzure

Olá abrir **Prompt de comando do Microsoft Azure**e faça logon. 

```azurecli-interactive
azure login
```

Depois que você digitar Olá anterior de exemplo, um código é fornecido. Navegue toohttps://aka.ms/devicelogin em um processo de logon do navegador toocontinue hello.

![cmd mostrando logon de dispositivo][1]

No navegador de hello, insira o código Olá recebido. Você é redirecionado tooa na página de entrada.

![código de tooenter do navegador][2]

Depois que o código de saudação foi inserido você entrou, Olá fechar navegador toocontinue com cenário de saudação.

![conectado com êxito][3]

## <a name="switch-tooresource-manager-mode"></a>Alternar tooResource modo Manager

```azurecli-interactive
azure config mode arm
```

## <a name="create-hello-resource-group"></a>Criar grupo de recursos de saudação

Antes de criar o gateway de aplicativo hello, um grupo de recursos é criado o gateway de aplicativo hello toocontain. Veja a seguir de Olá comando hello.

```azurecli-interactive
azure group create \
--name ContosoRG \
--location eastus
```

## <a name="create-a-virtual-network"></a>Criar uma rede virtual

Depois de criar o grupo de recursos hello, uma rede virtual é criada para o gateway de aplicativo hello.  Olá exemplo a seguir, o espaço de endereço Olá foi como 10.0.0.0/16 conforme definido na saudação anterior anotações de cenário.

```azurecli-interactive
azure network vnet create \
--name ContosoVNET \
--address-prefixes 10.0.0.0/16 \
--resource-group ContosoRG \
--location eastus
```

## <a name="create-a-subnet"></a>Criar uma sub-rede

Após a criação de rede virtual hello, uma sub-rede é adicionada para o gateway de aplicativo hello.  Se você planejar toouse gateway de aplicativo com um aplicativo web hospedado no hello mesmo virtual de rede como gateway de aplicativo hello, ser tooleave se espaço suficiente para outra sub-rede.

```azurecli-interactive
azure network vnet subnet create \
--resource-group ContosoRG \
--name subnet01 \
--vnet-name ContosoVNET \
--address-prefix 10.0.0.0/28 
```

## <a name="create-hello-application-gateway"></a>Criar hello application gateway

Após a criação de sub-rede e a rede virtual hello, Olá os pré-requisitos para o gateway de aplicativo hello forem concluídos. Além de uma senha de certificado e hello. pfx exportado anteriormente para o certificado de saudação são necessários para Olá etapa a seguir: endereços IP de saudação usados para Olá back-end são endereços IP de saudação do servidor back-end. Esses valores podem ser qualquer IPs privados na rede virtual hello, ips públicos ou nomes de domínio totalmente qualificado para seus servidores de back-end.

```azurecli-interactive
azure network application-gateway create \
--name AdatumAppGateway \
--location eastus \
--resource-group ContosoRG \
--vnet-name ContosoVNET \
--subnet-name subnet01 \
--servers 134.170.185.46,134.170.188.221,134.170.185.50 \
--capacity 2 \
--sku-tier Standard \
--routing-rule-type Basic \
--frontend-port 80 \
--http-settings-cookie-based-affinity Enabled \
--http-settings-port 80 \
--http-settings-protocol http \
--frontend-port http \
--sku-name Standard_Medium
```

> [!NOTE]
> Para obter uma lista de parâmetros que podem ser fornecidas durante a criação da execução Olá comando a seguir: **criar gateway de aplicativo de rede do azure – ajuda**.

Este exemplo cria um application gateway básico com configurações padrão para o ouvinte hello, pool de back-end, configurações de http de back-end e regras. Você pode modificar essas configurações toosuit sua implantação quando Olá provisionamento é bem-sucedido.
Se você já tiver o aplicativo da web definido com o pool de back-end de saudação em Olá anterior etapas, uma vez criadas, balanceamento de carga começa.

## <a name="next-steps"></a>Próximas etapas

Saiba como sondas de integridade personalizado toocreate visitando [criar um teste de integridade personalizado](application-gateway-create-probe-portal.md)

Saiba como tooconfigure descarregamento de SSL e take Olá cara SSL descriptografia desativada, os servidores web visitando [configurar descarregamento de SSL](application-gateway-ssl-arm.md)

<!--Image references-->

[scenario]: ./media/application-gateway-create-gateway-cli-nodejs/scenario.png
[1]: ./media/application-gateway-create-gateway-cli-nodejs/figure1.png
[2]: ./media/application-gateway-create-gateway-cli-nodejs/figure2.png
[3]: ./media/application-gateway-create-gateway-cli-nodejs/figure3.png
