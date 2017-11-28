---
title: "Modificar os prefixos de endereço IP do gateway de rede local e o endereço IP do Gateway de VPN | Azure | CLI | Microsoft Docs"
description: "Este artigo mostra o passo a passo da alteração dos prefixos de endereço IP do seu gateway de rede local usando a CLI do Azure."
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
ms.openlocfilehash: 7db1ad970ebb93d46d5a861f9a9b27bf121531a3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="modify-local-network-gateway-settings-using-the-azure-cli"></a><span data-ttu-id="4c808-103">Modificar as configurações de gateway de rede local usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="4c808-103">Modify local network gateway settings using the Azure CLI</span></span>

<span data-ttu-id="4c808-104">Às vezes, as configurações do seu gateway de rede local AddressPrefix ou GatewayIPAddress mudam.</span><span class="sxs-lookup"><span data-stu-id="4c808-104">Sometimes the settings for your local network gateway Address Prefix or Gateway IP Address change.</span></span> <span data-ttu-id="4c808-105">Este artigo mostra como modificar as configurações de gateway de rede local.</span><span class="sxs-lookup"><span data-stu-id="4c808-105">This article shows you how to modify your local network gateway settings.</span></span> <span data-ttu-id="4c808-106">Também é possível modificar essas configurações usando um método diferente, selecionando uma opção diferente da lista a seguir:</span><span class="sxs-lookup"><span data-stu-id="4c808-106">You can also modify these settings using a different method by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4c808-107">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4c808-107">Azure portal</span></span>](vpn-gateway-modify-local-network-gateway-portal.md)
> * [<span data-ttu-id="4c808-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c808-108">PowerShell</span></span>](vpn-gateway-modify-local-network-gateway.md)
> * [<span data-ttu-id="4c808-109">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="4c808-109">Azure CLI</span></span>](vpn-gateway-modify-local-network-gateway-cli.md)
>
>

## <span data-ttu-id="4c808-110"><a name="before"></a>Antes de começar</span><span class="sxs-lookup"><span data-stu-id="4c808-110"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="4c808-111">Instale a versão mais recente dos comandos da CLI (2.0 ou posterior).</span><span class="sxs-lookup"><span data-stu-id="4c808-111">Install the latest version of the CLI commands (2.0 or later).</span></span> <span data-ttu-id="4c808-112">Para saber mais sobre como instalar os comandos do CLI, veja [Instalar a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4c808-112">For information about installing the CLI commands, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [CLI-login](../../includes/vpn-gateway-cli-login-include.md)]

## <span data-ttu-id="4c808-113"><a name="ipaddprefix"></a>Modificar os prefixos de endereço IP</span><span class="sxs-lookup"><span data-stu-id="4c808-113"><a name="ipaddprefix"></a>Modify IP address prefixes</span></span>

[!INCLUDE [modify-prefix](../../includes/vpn-gateway-modify-ip-prefix-cli-include.md)]

## <span data-ttu-id="4c808-114"><a name="gwip"></a>Modificar o endereço IP do gateway</span><span class="sxs-lookup"><span data-stu-id="4c808-114"><a name="gwip"></a>Modify the gateway IP address</span></span>

[!INCLUDE [modify-gateway-IP](../../includes/vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

## <a name="next-steps"></a><span data-ttu-id="4c808-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4c808-115">Next steps</span></span>

<span data-ttu-id="4c808-116">Você pode verificar a conexão de gateway.</span><span class="sxs-lookup"><span data-stu-id="4c808-116">You can verify your gateway connection.</span></span> <span data-ttu-id="4c808-117">Confira [Verificar uma conexão de gateway](vpn-gateway-verify-connection-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="4c808-117">See [Verify a gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>

