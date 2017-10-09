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
# <a name="modify-local-network-gateway-settings-using-powershell"></a><span data-ttu-id="7c6a2-103">Modificar as configurações de gateway de rede local usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c6a2-103">Modify local network gateway settings using PowerShell</span></span>

<span data-ttu-id="7c6a2-104">Às vezes, alteram configurações de saudação do seu gateway de rede local AddressPrefix ou GatewayIPAddress.</span><span class="sxs-lookup"><span data-stu-id="7c6a2-104">Sometimes hello settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="7c6a2-105">Este artigo mostra como toomodify suas configurações de gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="7c6a2-105">This article shows you how toomodify your local network gateway settings.</span></span> <span data-ttu-id="7c6a2-106">Você também pode modificar essas configurações usando um método diferente, selecionando uma opção diferente de saudação lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c6a2-106">You can also modify these settings using a different method by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7c6a2-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7c6a2-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="7c6a2-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c6a2-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="7c6a2-109">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7c6a2-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="7c6a2-110"><a name="before"></a>Antes de começar</span><span class="sxs-lookup"><span data-stu-id="7c6a2-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="7c6a2-111">Instale a versão mais recente Olá de saudação cmdlets do PowerShell do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c6a2-111">Install hello latest version of hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="7c6a2-112">Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) para obter mais informações sobre como instalar os cmdlets do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="7c6a2-112">See [How tooinstall and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing hello PowerShell cmdlets.</span></span>

## <span data-ttu-id="7c6a2-113"><a name="ipaddprefix"></a>Modificar os prefixos de endereço IP</span><span class="sxs-lookup"><span data-stu-id="7c6a2-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <span data-ttu-id="7c6a2-114"><a name="gwip"></a>Modificar o endereço IP do gateway Olá</span><span class="sxs-lookup"><span data-stu-id="7c6a2-114"><a name="gwip"></a>Modify hello gateway IP address</span></span>

[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="7c6a2-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7c6a2-115">Next steps</span></span>

<span data-ttu-id="7c6a2-116">Você pode verificar a conexão de gateway.</span><span class="sxs-lookup"><span data-stu-id="7c6a2-116">You can verify your gateway connection.</span></span> <span data-ttu-id="7c6a2-117">Confira [Verificar uma conexão de gateway](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7c6a2-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>