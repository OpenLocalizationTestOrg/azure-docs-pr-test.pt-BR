---
title: "Modificar prefixos de endereço IP do gateway de rede local hello e endereço de IP do Gateway de VPN Olá | Azure | PowerShell | Microsoft Docs"
description: "Este artigo mostra o passo a passo da alteração dos prefixos de endereço IP do seu gateway de rede local usando o PowerShell"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8c7db48f-d09a-44e7-836f-1fb6930389df
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: cherylmc
ms.openlocfilehash: 1353598b39a97fae9bdb424505a5ae2560482654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-local-network-gateway-settings-using-powershell"></a>Modificar as configurações de gateway de rede local usando o PowerShell

Às vezes, alteram configurações de saudação do seu gateway de rede local AddressPrefix ou GatewayIPAddress. Este artigo mostra como toomodify suas configurações de gateway de rede local. Você também pode modificar essas configurações usando um método diferente, selecionando uma opção diferente de saudação lista a seguir:

> [!div class="op_single_selector"]
> * [Portal do Azure](vpn-gateway-modify-local-network-gateway-portal.md)
> * [PowerShell](vpn-gateway-modify-local-network-gateway.md)
> * [CLI do Azure](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <a name="before"></a>Antes de começar

Instale a versão mais recente Olá de saudação cmdlets do PowerShell do Gerenciador de recursos do Azure. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) para obter mais informações sobre como instalar os cmdlets do PowerShell hello.

## <a name="ipaddprefix"></a>Modificar os prefixos de endereço IP

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="gwip"></a>Modificar o endereço IP do gateway Olá

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Próximas etapas

Você pode verificar a conexão de gateway. Confira [Verificar uma conexão de gateway](vpn-gateway-verify-connection-resource-manager.md).