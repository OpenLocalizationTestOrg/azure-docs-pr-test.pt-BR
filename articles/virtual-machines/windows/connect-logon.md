---
title: Conectar uma VM do Windows Server | Microsoft Docs
description: "Saiba como se conectar e fazer logon em uma VM do Windows usando o portal do Azure e o modelo de implantação do Gerenciador de Recursos."
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
ms.openlocfilehash: 88431377a36d5bc36220c630f0c8d4a46ab4a434
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-connect-and-log-on-to-an-azure-virtual-machine-running-windows"></a><span data-ttu-id="716dd-103">Como se conectar e fazer logon em uma máquina virtual do Azure executando o Windows</span><span class="sxs-lookup"><span data-stu-id="716dd-103">How to connect and log on to an Azure virtual machine running Windows</span></span>
<span data-ttu-id="716dd-104">Você usará o botão **Conectar** no portal do Azure para iniciar uma sessão da Área de Trabalho Remota (RDP) a partir de uma área de trabalho do Windows.</span><span class="sxs-lookup"><span data-stu-id="716dd-104">You'll use the **Connect** button in the Azure portal to start a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="716dd-105">Primeiro, conecte-se à máquina virtual, em seguida, faça logon.</span><span class="sxs-lookup"><span data-stu-id="716dd-105">First you connect to the virtual machine, then you log on.</span></span>

<span data-ttu-id="716dd-106">Se você estiver tentando se conectar a uma VM do Windows a partir de um Mac, será necessário instalar um cliente do RDP para Mac como a [Área de Trabalho Remota da Microsoft](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="716dd-106">If you are trying to connect to a Windows VM from a Mac, you need to install an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="716dd-107">Conectar-se à máquina virtual</span><span class="sxs-lookup"><span data-stu-id="716dd-107">Connect to the virtual machine</span></span>
1. <span data-ttu-id="716dd-108">Se ainda não tiver feito isso, entre no [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="716dd-108">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="716dd-109">No menu Hub, clique em **Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="716dd-109">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="716dd-110">Selecione a máquina virtual na lista.</span><span class="sxs-lookup"><span data-stu-id="716dd-110">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="716dd-111">Na folha da máquina virtual, clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="716dd-111">On the blade for the virtual machine, click **Connect**.</span></span>
   
    ![Captura de tela do portal do Azure mostrando como conectar sua VM.](./media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="716dd-113">Se o botão **Conectar** no portal estiver esmaecido e você não estiver conectado ao Azure por meio de uma [ExpressRoute](../../expressroute/expressroute-introduction.md) ou de uma conexão [VPN Site a Site](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md), será necessário criar e atribuir à VM um endereço IP público antes de usar o RDP.</span><span class="sxs-lookup"><span data-stu-id="716dd-113">If the **Connect** button in the portal is greyed out and you are not connected to Azure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need to create and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="716dd-114">Leia mais sobre [endereços IP públicos no Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="716dd-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="716dd-115">Faça logon na máquina virtual</span><span class="sxs-lookup"><span data-stu-id="716dd-115">Log on to the virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="716dd-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="716dd-116">Next steps</span></span>
<span data-ttu-id="716dd-117">Se você tiver problemas ao tentar se conectar, consulte [Solucionar Problemas de conexões da Área de Trabalho Remota](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="716dd-117">If you run into trouble when you try to connect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="716dd-118">Este artigo orienta você no diagnóstico e na solução de problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="716dd-118">This article walks you through diagnosing and resolving common problems.</span></span>

