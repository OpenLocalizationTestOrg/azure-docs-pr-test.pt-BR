---
title: "Modificar os prefixos de endereço IP do gateway de rede local e o endereço IP do Gateway de VPN | Azure | Portal | Microsoft Docs"
description: "Este artigo mostra o passo a passo da alteração dos prefixos de endereço IP do seu gateway de rede local usando o portal do Azure"
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
ms.openlocfilehash: bdd6f90fe97408bd45a72adf58bfdc190207de46
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-the-azure-portal"></a><span data-ttu-id="60fdd-103">Modificar as configurações de gateway de rede local usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="60fdd-103">Modify local network gateway settings using the Azure portal</span></span>

<span data-ttu-id="60fdd-104">Às vezes, as configurações do seu gateway de rede local AddressPrefix ou GatewayIPAddress mudam.</span><span class="sxs-lookup"><span data-stu-id="60fdd-104">Sometimes the settings for your local network gateway AddressPrefix or GatewayIPAddress change.</span></span> <span data-ttu-id="60fdd-105">Este artigo mostra como modificar as configurações de gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="60fdd-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="60fdd-106">Também é possível modificar essas configurações usando um método diferente, selecionando uma opção diferente da lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="60fdd-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="60fdd-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="60fdd-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="60fdd-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="60fdd-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="60fdd-109">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="60fdd-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>


## <span data-ttu-id="60fdd-110"><a name="ipaddprefix"></a>Modificar os prefixos de endereço IP</span><span class="sxs-lookup"><span data-stu-id="60fdd-110"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

<span data-ttu-id="60fdd-111">Quando você modifica os prefixos de endereço IP, as etapas a que seguir dependem se o gateway de rede local tem uma conexão.</span><span class="sxs-lookup"><span data-stu-id="60fdd-111">When you modify IP address prefixes, the steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify prefix](../../includes/vpn-gateway-modify-ip-prefix-portal-include.md)]

## <span data-ttu-id="60fdd-112"><a name="gwip"></a>Modificar o endereço IP do gateway</span><span class="sxs-lookup"><span data-stu-id="60fdd-112"><a name="gwip"></a>Modify the gateway IP address</span></span>

<span data-ttu-id="60fdd-113">Se o dispositivo VPN ao qual você deseja se conectar mudou seu endereço IP público, você precisará modificar o gateway de rede local para refletir essa alteração.</span><span class="sxs-lookup"><span data-stu-id="60fdd-113">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="60fdd-114">Quando você altera o endereço IP público, as etapas a seguir dependem se o gateway de rede local possui uma conexão.</span><span class="sxs-lookup"><span data-stu-id="60fdd-114">When you change the public IP address, the steps you follow depend on whether your local network gateway has a connection.</span></span>

[!INCLUDE [modify gateway IP](../../includes/vpn-gateway-modify-lng-gateway-ip-portal-include.md)]

## <a name="next-steps"></a><span data-ttu-id="60fdd-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="60fdd-115">Next steps</span></span>

<span data-ttu-id="60fdd-116">Você pode verificar a conexão de gateway.</span><span class="sxs-lookup"><span data-stu-id="60fdd-116">You can verify your gateway connection.</span></span> <span data-ttu-id="60fdd-117">Confira [Verificar uma conexão de gateway](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="60fdd-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>