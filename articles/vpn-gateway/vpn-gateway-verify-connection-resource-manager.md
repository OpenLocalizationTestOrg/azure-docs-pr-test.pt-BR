---
title: "uma conexão de Gateway VPN de aaaVerify | Microsoft Docs"
description: "Este artigo mostra como tooverify um virtual conexão de Gateway VPN de rede."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 7e3d1043-caa9-4472-96d3-832f4e2c91ee
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2017
ms.author: cherylmc
ms.openlocfilehash: 0d3da94a76b36251d629f82b1575328c7ac10b26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="verify-a-vpn-gateway-connection"></a><span data-ttu-id="73212-103">Verificar uma conexão de Gateway de VPN</span><span class="sxs-lookup"><span data-stu-id="73212-103">Verify a VPN Gateway connection</span></span>

<span data-ttu-id="73212-104">Este artigo mostra como tooverify uma conexão de gateway VPN para Olá clássico e modelos de implantação do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="73212-104">This article shows you how tooverify a VPN gateway connection for both hello classic and Resource Manager deployment models.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="73212-105">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="73212-105">Azure portal</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="powershell"></a><span data-ttu-id="73212-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="73212-106">PowerShell</span></span>

<span data-ttu-id="73212-107">tooverify uma conexão de gateway VPN para implantação do Gerenciador de recursos de saudação modelo usando o PowerShell, instale a versão mais recente de saudação do hello [cmdlets do PowerShell do Gerenciador de recursos do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="73212-107">tooverify a VPN gateway connection for hello Resource Manager deployment model using PowerShell, install hello latest version of hello [Azure Resource Manager PowerShell cmdlets](/powershell/azure/overview).</span></span>

[!INCLUDE [PowerShell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="azure-cli"></a><span data-ttu-id="73212-108">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="73212-108">Azure CLI</span></span>

<span data-ttu-id="73212-109">tooverify uma conexão de gateway VPN para implantação do Gerenciador de recursos de saudação modelo usando a CLI do Azure, instale a versão mais recente de saudação do hello [comandos CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 ou posterior).</span><span class="sxs-lookup"><span data-stu-id="73212-109">tooverify a VPN gateway connection for hello Resource Manager deployment model using Azure CLI, install hello latest version of hello [CLI commands](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0 or later).</span></span>

[!INCLUDE [CLI](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]


## <a name="azure-portal-classic"></a><span data-ttu-id="73212-110">Portal do Azure (clássico)</span><span class="sxs-lookup"><span data-stu-id="73212-110">Azure portal (classic)</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

## <a name="powershell-classic"></a><span data-ttu-id="73212-111">PowerShell (clássico)</span><span class="sxs-lookup"><span data-stu-id="73212-111">PowerShell (classic)</span></span>

<span data-ttu-id="73212-112">tooverify sua conexão de gateway VPN para implantação clássica de saudação do modelo usando o PowerShell, instalar versões mais recentes Olá Olá cmdlets do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="73212-112">tooverify your VPN gateway connection for hello classic deployment model using PowerShell, install hello latest versions of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="73212-113">Se Olá toodownload e instalação de ser [gerenciamento de serviço](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) módulo.</span><span class="sxs-lookup"><span data-stu-id="73212-113">Be sure toodownload and install hello [Service Management](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0) module.</span></span> <span data-ttu-id="73212-114">Use 'Add-AzureAccount' toolog no modelo de implantação clássico toohello.</span><span class="sxs-lookup"><span data-stu-id="73212-114">Use 'Add-AzureAccount' toolog in toohello classic deployment model.</span></span>

[!INCLUDE [Classic PowerShell](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

## <a name="next-steps"></a><span data-ttu-id="73212-115">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="73212-115">Next steps</span></span>

* <span data-ttu-id="73212-116">Você pode adicionar máquinas virtuais tooyour as redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="73212-116">You can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="73212-117">Veja [Criar uma máquina virtual](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para obter as etapas.</span><span class="sxs-lookup"><span data-stu-id="73212-117">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
