---
title: "Modificar prefixos de endereço IP do gateway de rede local hello e endereço de IP do Gateway de VPN Olá | Azure | Portal | Microsoft Docs"
description: "Este artigo orienta a alteração prefixos de endereço IP do seu gateway de rede local usando Olá portal do Azure."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 001df7b748ccc234d87aab3501a4f0e4ddfe60f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a>Modificar as configurações de gateway de rede local usando Olá portal do Azure

Às vezes, alteram configurações de saudação do seu gateway de rede local AddressPrefix ou GatewayIPAddress. Este artigo mostra como toomodify suas configurações de gateway de rede local. Você também pode modificar essas configurações usando um método diferente, selecionando uma opção diferente de saudação lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [CLI do Azure](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <a name="ipaddprefix"></a>Modificar os prefixos de endereço IP

Quando você modifica os prefixos de endereço IP, etapas de saudação que seguir dependem se o gateway de rede local tem uma conexão.

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <a name="gwip"></a>Modificar o endereço IP do gateway Olá

Se o dispositivo VPN Olá que você deseja tooconnect toohas alterado seu endereço IP público, você precisa toomodify Olá local de rede gateway tooreflect que alteram. Quando você altera o endereço IP público de hello, etapas de saudação que seguir dependem se o gateway de rede local tem uma conexão.

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a>Próximas etapas

Você pode verificar a conexão de gateway. Confira [Verificar uma conexão de gateway](vpn-gateway-verify-connection-resource-manager.md).