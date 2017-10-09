---
title: aaaConnect tooa VM do Windows Server | Microsoft Docs
description: "Saiba como tooconnect e fazer logon usando o tooa VM do Windows hello modelo de implantação do Azure de Gerenciador de recursos de portal e hello."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: dc397f435ef165ae5af09f1d037ad3d520bb7ac3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconnect-and-log-on-tooan-azure-virtual-machine-running-windows"></a><span data-ttu-id="72c29-103">Como tooconnect e logon tooan virtuais do Azure do computador que executa o Windows</span><span class="sxs-lookup"><span data-stu-id="72c29-103">How tooconnect and log on tooan Azure virtual machine running Windows</span></span>
<span data-ttu-id="72c29-104">Você usará Olá **conectar** botão Olá toostart portal do Azure uma sessão de área de trabalho remota (RDP) de uma área de trabalho do Windows.</span><span class="sxs-lookup"><span data-stu-id="72c29-104">You'll use hello **Connect** button in hello Azure portal toostart a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="72c29-105">Primeiro você se conectar a máquina virtual de toohello e você fizer logon.</span><span class="sxs-lookup"><span data-stu-id="72c29-105">First you connect toohello virtual machine, then you log on.</span></span>

<span data-ttu-id="72c29-106">Se você estiver tentando tooconnect tooa VM do Windows de um Mac, você precisa tooinstall como um cliente RDP para Mac [a área de trabalho remota Microsoft](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="72c29-106">If you are trying tooconnect tooa Windows VM from a Mac, you need tooinstall an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="72c29-107">Conecte-se a máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="72c29-107">Connect toohello virtual machine</span></span>
1. <span data-ttu-id="72c29-108">Se você ainda não fez isso, entre no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="72c29-108">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="72c29-109">No menu de Hub hello, clique em **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="72c29-109">On hello Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="72c29-110">Selecione máquina virtual de Olá Olá lista.</span><span class="sxs-lookup"><span data-stu-id="72c29-110">Select hello virtual machine from hello list.</span></span>
4. <span data-ttu-id="72c29-111">Na folha de saudação para a máquina virtual de saudação, clique em **conectar**.</span><span class="sxs-lookup"><span data-stu-id="72c29-111">On hello blade for hello virtual machine, click **Connect**.</span></span>
   
    ![Captura de tela da saudação mostrando portal do Azure como tooconnect tooyour VM.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="72c29-113">Se hello **conectar** botão no portal de saudação está desativada e não tooAzure conectado por meio de um [rota expressa](../../expressroute/expressroute-introduction.md) ou [VPN Site a Site](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) conexão, você precisa toocreate e Atribua a VM um endereço IP público antes de usar o RDP.</span><span class="sxs-lookup"><span data-stu-id="72c29-113">If hello **Connect** button in hello portal is greyed out and you are not connected tooAzure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need toocreate and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="72c29-114">Leia mais sobre [endereços IP públicos no Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="72c29-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-toohello-virtual-machine"></a><span data-ttu-id="72c29-115">Faça logon na máquina virtual de toohello</span><span class="sxs-lookup"><span data-stu-id="72c29-115">Log on toohello virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="72c29-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="72c29-116">Next steps</span></span>
<span data-ttu-id="72c29-117">Se você tiver problemas ao tentar tooconnect, consulte [conexões de área de trabalho remota solucionar](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72c29-117">If you run into trouble when you try tooconnect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="72c29-118">Este artigo orienta você no diagnóstico e na solução de problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="72c29-118">This article walks you through diagnosing and resolving common problems.</span></span>

