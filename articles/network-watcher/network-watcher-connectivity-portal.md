---
title: "Verificar a conectividade com o Observador de Rede do Azure – portal do Azure | Microsoft Docs"
description: "Esta página explica como usar a verificação de conectividade com o Observador de Rede usando o portal do Azure"
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
ms.openlocfilehash: 84774d0f40e06a819ca6de6cf0be68e17ba474e4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-the-azure-portal"></a><span data-ttu-id="f0c54-103">Verificar a conectividade com o Observador de Rede do Azure usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f0c54-103">Check connectivity with Azure Network Watcher using the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="f0c54-104">Portal</span><span class="sxs-lookup"><span data-stu-id="f0c54-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="f0c54-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0c54-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="f0c54-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f0c54-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="f0c54-107">API REST do Azure</span><span class="sxs-lookup"><span data-stu-id="f0c54-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="f0c54-108">Saiba como usar a conectividade para verificar se uma conexão TCP direta de uma máquina virtual para um determinado ponto de extremidade pode ser estabelecida.</span><span class="sxs-lookup"><span data-stu-id="f0c54-108">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f0c54-109">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f0c54-109">Before you begin</span></span>

<span data-ttu-id="f0c54-110">Este artigo pressupõe que você tenha os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="f0c54-110">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="f0c54-111">Uma instância do Observador de Rede na região em que você deseja verificar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="f0c54-111">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="f0c54-112">Máquinas virtuais com as quais verificar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="f0c54-112">Virtual machines to check connectivity with.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f0c54-113">A verificação de conectividade requer uma extensão de máquina virtual `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="f0c54-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="f0c54-114">Para instalar a extensão em uma VM do Windows, visite [Extensão da máquina virtual do Agente do Observador de Rede do Azure para Windows](../virtual-machines/windows/extensions-nwa.md) e para a VM do Linux, visite [Extensão da máquina virtual do Agente do Observador de Rede do Azure para Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="f0c54-114">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="f0c54-115">Verificar a conectividade com uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="f0c54-115">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="f0c54-116">Este exemplo verifica a conectividade a uma máquina virtual de destino pela porta 80.</span><span class="sxs-lookup"><span data-stu-id="f0c54-116">This example checks connectivity to a destination virtual machine over port 80.</span></span>

<span data-ttu-id="f0c54-117">Navegue até o observador de rede e clique em **Verificação de conectividade (versão prévia)**.</span><span class="sxs-lookup"><span data-stu-id="f0c54-117">Navigate to your Network Watcher and click **Connectivity check (Preview)**.</span></span> <span data-ttu-id="f0c54-118">Selecione a máquina virtual para verificar a conectividade.</span><span class="sxs-lookup"><span data-stu-id="f0c54-118">Select the virtual machine to check connectivity from.</span></span> <span data-ttu-id="f0c54-119">No **destino** seção escolher **selecione uma máquina virtual** e escolha a máquina virtual correta e a porta para testar.</span><span class="sxs-lookup"><span data-stu-id="f0c54-119">In the **Destination** section choose **Select a virtual machine** and choose the correct virtual machine and port to test.</span></span>

<span data-ttu-id="f0c54-120">Depois de clicar em **verificar**, a conectividade entre as máquinas virtuais na porta especificada está marcada.</span><span class="sxs-lookup"><span data-stu-id="f0c54-120">Once you click **Check**, the connectivity between the virtual machines on the port specified are checked.</span></span> <span data-ttu-id="f0c54-121">No exemplo, o VM de destino está inacessível, uma lista de saltos serão mostrados.</span><span class="sxs-lookup"><span data-stu-id="f0c54-121">In the example, the destination VM is unreachable, a listing of hops are shown.</span></span>

![Verificar os resultados de conectividade para uma máquina virtual][1]

## <a name="check-remote-endpoint-connectivity"></a><span data-ttu-id="f0c54-123">Verificar a conectividade de ponto de extremidade remoto</span><span class="sxs-lookup"><span data-stu-id="f0c54-123">Check remote endpoint connectivity</span></span>

<span data-ttu-id="f0c54-124">Para verificar a conectividade e a latência para um ponto de extremidade, escolha o **especificar manualmente** botão de opção no **destino** seção, a url e a porta de entrada e clique em **verificar**.</span><span class="sxs-lookup"><span data-stu-id="f0c54-124">To check the connectivity and latency to a remote endpoint, choose the **Specify manually** radio button in the **Destination** section, input the url and the port and click **Check**.</span></span>  <span data-ttu-id="f0c54-125">Isso é usado para pontos de extremidade remotos como pontos de extremidade de sites e de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f0c54-125">This is used for remote endpoints like websites and storage endpoints.</span></span>

![Resultados da verificação de conectividade para um site Web][2]

## <a name="next-steps"></a><span data-ttu-id="f0c54-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f0c54-127">Next steps</span></span>

<span data-ttu-id="f0c54-128">Saiba como automatizar as capturas de pacotes com alertas da Máquina Virtual exibindo [Criar uma captura de pacotes disparada por alertas](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="f0c54-128">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="f0c54-129">Localize se determinado tráfego é permitido dentro ou fora de sua VM visitando [Verificar o fluxo do IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f0c54-129">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
