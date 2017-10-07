---
title: aaaCheck conectividade com o observador de rede do Azure - portal do Azure | Microsoft Docs
description: "Esta página explica como toouse conectividade para verificar com o observador de rede usando Olá portal do Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="91d32-103">Verifique a conectividade com o observador de rede do Azure usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="91d32-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="91d32-104">Portal</span><span class="sxs-lookup"><span data-stu-id="91d32-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="91d32-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="91d32-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="91d32-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="91d32-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="91d32-107">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="91d32-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="91d32-108">Saiba como toouse tooverify de conectividade se uma conexão TCP direto de tooa uma máquina virtual que recebe o ponto de extremidade pode ser estabelecida.</span><span class="sxs-lookup"><span data-stu-id="91d32-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="91d32-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="91d32-109">Before you begin</span></span>

<span data-ttu-id="91d32-110">Este artigo pressupõe que você tenha Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="91d32-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="91d32-111">Uma instância do observador de rede na região Olá deseja toocheck conectividade.</span><span class="sxs-lookup"><span data-stu-id="91d32-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="91d32-112">Conectividade de toocheck de máquinas virtuais com.</span><span class="sxs-lookup"><span data-stu-id="91d32-112">Virtual machines toocheck connectivity with.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91d32-113">A verificação de conectividade requer uma extensão de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="91d32-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="91d32-114">Para instalar a extensão de saudação em uma VM do Windows, visite [extensão de máquina virtual do agente do Inspetor de rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para a visita de VM do Linux [extensão de máquina virtual do agente do Inspetor de rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="91d32-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="91d32-115">Verifique a conectividade tooa virtual machine</span><span class="sxs-lookup"><span data-stu-id="91d32-115">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="91d32-116">Este exemplo verifica a máquina de virtual de destino conectividade tooa pela porta 80.</span><span class="sxs-lookup"><span data-stu-id="91d32-116">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

<span data-ttu-id="91d32-117">Navegue tooyour observador de rede e clique em **verificação de conectividade (visualização)**.</span><span class="sxs-lookup"><span data-stu-id="91d32-117">Navigate tooyour Network Watcher and click **Connectivity check (Preview)**.</span></span> <span data-ttu-id="91d32-118">Selecione a conectividade de toocheck de máquina virtual de saudação do.</span><span class="sxs-lookup"><span data-stu-id="91d32-118">Select hello virtual machine toocheck connectivity from.</span></span> <span data-ttu-id="91d32-119">Em Olá **destino** seção escolher **selecione uma máquina virtual** e escolha a máquina virtual correta de saudação e porta tootest.</span><span class="sxs-lookup"><span data-stu-id="91d32-119">In hello **Destination** section choose **Select a virtual machine** and choose hello correct virtual machine and port tootest.</span></span>

<span data-ttu-id="91d32-120">Depois de clicar em **verificar**, conectividade de saudação entre máquinas virtuais Olá Olá porta especificada são verificadas.</span><span class="sxs-lookup"><span data-stu-id="91d32-120">Once you click **Check**, hello connectivity between hello virtual machines on hello port specified are checked.</span></span> <span data-ttu-id="91d32-121">No exemplo hello, destino Olá VM está inacessível, uma lista de saltos serão mostrados.</span><span class="sxs-lookup"><span data-stu-id="91d32-121">In hello example, hello destination VM is unreachable, a listing of hops are shown.</span></span>

![Verificar os resultados de conectividade para uma máquina virtual][1]

## <a name="check-remote-endpoint-connectivity"></a><span data-ttu-id="91d32-123">Verificar a conectividade de ponto de extremidade remoto</span><span class="sxs-lookup"><span data-stu-id="91d32-123">Check remote endpoint connectivity</span></span>

<span data-ttu-id="91d32-124">conectividade de saudação toocheck e latência tooa ponto de extremidade remoto, escolha Olá **especificar manualmente** botão de opção na Olá **destino** seção, Olá url e a porta de saudação de entrada e clique em **verificar** .</span><span class="sxs-lookup"><span data-stu-id="91d32-124">toocheck hello connectivity and latency tooa remote endpoint, choose hello **Specify manually** radio button in hello **Destination** section, input hello url and hello port and click **Check**.</span></span>  <span data-ttu-id="91d32-125">Isso é usado para pontos de extremidade remotos como pontos de extremidade de sites e de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="91d32-125">This is used for remote endpoints like websites and storage endpoints.</span></span>

![Resultados da verificação de conectividade para um site Web][2]

## <a name="next-steps"></a><span data-ttu-id="91d32-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="91d32-127">Next steps</span></span>

<span data-ttu-id="91d32-128">Saiba como o pacote tooautomate captura com alertas de máquina Virtual por meio da exibição [criar uma captura de pacote de disparo de alerta](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="91d32-128">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="91d32-129">Localize se determinado tráfego é permitido dentro ou fora de sua VM visitando [Verificar o fluxo do IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="91d32-129">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
