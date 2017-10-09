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
# <a name="modify-local-network-gateway-settings-using-hello-azure-portal"></a><span data-ttu-id="07137-103">Modificar as configurações de gateway de rede local usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="07137-103">Modify local network gateway settings using hello Azure portal</span></span>

<span data-ttu-id="07137-104">Às vezes, alteram configurações de saudação do seu gateway de rede local AddressPrefix ou GatewayIPAddress.</span><span class="sxs-lookup"><span data-stu-id="07137-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="07137-105">Este artigo mostra como toomodify suas configurações de gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="07137-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="07137-106">Você também pode modificar essas configurações usando um método diferente, selecionando uma opção diferente de saudação lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="07137-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="07137-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="07137-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="07137-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="07137-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="07137-109">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="07137-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="07137-110"><a name="ipaddprefix"></a>Modificar os prefixos de endereço IP</span><span class="sxs-lookup"><span data-stu-id="07137-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="07137-111">Quando você modifica os prefixos de endereço IP, etapas de saudação que seguir dependem se o gateway de rede local tem uma conexão.</span><span class="sxs-lookup"><span data-stu-id="07137-111">When you modify IP address prefixes, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="07137-112"><a name="gwip"></a>Modificar o endereço IP do gateway Olá</span><span class="sxs-lookup"><span data-stu-id="07137-112"><a name="gwip"></a>Modify hello gateway IP address</span></span>

<span data-ttu-id="07137-113">Se o dispositivo VPN Olá que você deseja tooconnect toohas alterado seu endereço IP público, você precisa toomodify Olá local de rede gateway tooreflect que alteram.</span><span class="sxs-lookup"><span data-stu-id="07137-113">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="07137-114">Quando você altera o endereço IP público de hello, etapas de saudação que seguir dependem se o gateway de rede local tem uma conexão.</span><span class="sxs-lookup"><span data-stu-id="07137-114">When you change hello public IP address, hello steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="07137-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="07137-115">Next steps</span></span>

<span data-ttu-id="07137-116">Você pode verificar a conexão de gateway.</span><span class="sxs-lookup"><span data-stu-id="07137-116">You can verify your gateway connection.</span></span> <span data-ttu-id="07137-117">Confira [Verificar uma conexão de gateway](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="07137-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>