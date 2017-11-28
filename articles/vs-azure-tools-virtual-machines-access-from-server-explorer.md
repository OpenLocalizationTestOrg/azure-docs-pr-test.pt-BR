---
title: "Acessando Máquinas Virtuais do Azure do Gerenciador de Servidores | Microsoft Docs"
description: "Obtenha uma visão geral de como exibir e gerenciar máquinas virtuais (VMs) do Azure no Gerenciador de Servidores no Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: fcbb00cc2f00691e25ea84333e8c418b08210a67
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a><span data-ttu-id="8087c-103">Acessando máquinas virtuais do Azure por meio do Gerenciador de Servidores</span><span class="sxs-lookup"><span data-stu-id="8087c-103">Accessing Azure Virtual Machines from Server Explorer</span></span>
<span data-ttu-id="8087c-104">Usando o Gerenciador de Servidores no Visual Studio, você pode exibir informações sobre as máquinas virtuais hospedadas pelo Azure.</span><span class="sxs-lookup"><span data-stu-id="8087c-104">By using Server Explorer in Visual Studio, you can display information about your virtual machines hosted by Azure.</span></span>

## <a name="accessing-virtual-machines-in-server-explorer"></a><span data-ttu-id="8087c-105">Acessando máquinas virtuais no Gerenciador de Servidores</span><span class="sxs-lookup"><span data-stu-id="8087c-105">Accessing virtual machines in Server Explorer</span></span>
<span data-ttu-id="8087c-106">Se tiver máquinas virtuais hospedadas pelo Azure, você pode acessá-las no Gerenciador de Servidores.</span><span class="sxs-lookup"><span data-stu-id="8087c-106">If you have virtual machines hosted by Azure, you can access them in Server Explorer.</span></span> <span data-ttu-id="8087c-107">Você primeiro deve entrar sua assinatura do Azure para exibir os serviços móveis.</span><span class="sxs-lookup"><span data-stu-id="8087c-107">You must first sign in to your Azure subscription to view your mobile services.</span></span> <span data-ttu-id="8087c-108">Por exemplo, no Gerenciador de Servidores, você pode abrir o menu de atalho do nó do Azure e escolher **Conectar ao Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="8087c-108">To sign in, open the shortcut menu for the Azure node in Server Explorer, and choose **Connect to Microsoft Azure**.</span></span>

### <a name="to-get-information-about-your-virtual-machines"></a><span data-ttu-id="8087c-109">Para obter informações sobre suas máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="8087c-109">To get information about your virtual machines</span></span>
1. <span data-ttu-id="8087c-110">No Gerenciador de Servidores, escolha uma máquina virtual e pressione a tecla F4 para mostrar a janela de propriedades.</span><span class="sxs-lookup"><span data-stu-id="8087c-110">In Server Explorer, choose a virtual machine, and then choose the F4 key to show its properties window.</span></span>
   
    <span data-ttu-id="8087c-111">A tabela a seguir mostra quais propriedades estão disponíveis, mas elas são somente leitura.</span><span class="sxs-lookup"><span data-stu-id="8087c-111">The following table shows what properties are available, but they are all read-only.</span></span> <span data-ttu-id="8087c-112">Para alterá-las, use o [Portal Clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="8087c-112">To change them, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>
   
   | <span data-ttu-id="8087c-113">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8087c-113">Property</span></span> | <span data-ttu-id="8087c-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="8087c-114">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="8087c-115">Nome DNS</span><span class="sxs-lookup"><span data-stu-id="8087c-115">DNS Name</span></span> |<span data-ttu-id="8087c-116">A URL com o endereço de Internet da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8087c-116">The URL with the Internet address of the virtual machine.</span></span> |
   | <span data-ttu-id="8087c-117">Ambiente</span><span class="sxs-lookup"><span data-stu-id="8087c-117">Environment</span></span> |<span data-ttu-id="8087c-118">Para uma máquina virtual, o valor dessa propriedade é sempre produção.</span><span class="sxs-lookup"><span data-stu-id="8087c-118">For a virtual machine, the value of this property is always Production.</span></span> |
   | <span data-ttu-id="8087c-119">Nome</span><span class="sxs-lookup"><span data-stu-id="8087c-119">Name</span></span> |<span data-ttu-id="8087c-120">O nome da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8087c-120">The name of the virtual machine.</span></span> |
   | <span data-ttu-id="8087c-121">Tamanho</span><span class="sxs-lookup"><span data-stu-id="8087c-121">Size</span></span> |<span data-ttu-id="8087c-122">O tamanho da máquina virtual, que reflete a quantidade de memória e espaço em disco disponível.</span><span class="sxs-lookup"><span data-stu-id="8087c-122">The size of the virtual machine, which reflects the amount of memory and disk space that’s available.</span></span> <span data-ttu-id="8087c-123">Para obter mais informações, consulte Como configurar os tamanhos de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8087c-123">For more information, see How To: Configure Virtual Machine Sizes.</span></span> |
   | <span data-ttu-id="8087c-124">Status</span><span class="sxs-lookup"><span data-stu-id="8087c-124">Status</span></span> |<span data-ttu-id="8087c-125">Os valores incluem Inicial, Iniciado, Parando, Parado e Recuperando Status.</span><span class="sxs-lookup"><span data-stu-id="8087c-125">Values include Starting, Started, Stopping, Stopped, and Retrieving Status.</span></span> <span data-ttu-id="8087c-126">Se Recuperando Status aparecer, o status atual é desconhecido.</span><span class="sxs-lookup"><span data-stu-id="8087c-126">If Retrieving Status appears, the current status is unknown.</span></span> <span data-ttu-id="8087c-127">Os valores para essa propriedade diferem dos valores que são usados no [Portal Clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="8087c-127">The values for this property differ from the values that are used on the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> |
   | <span data-ttu-id="8087c-128">SubscriptionID</span><span class="sxs-lookup"><span data-stu-id="8087c-128">SubscriptionID</span></span> |<span data-ttu-id="8087c-129">A ID de assinatura para sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="8087c-129">The subscription ID for your Azure account.</span></span> <span data-ttu-id="8087c-130">Você pode mostrar essas informações no [Portal Clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885) exibindo as propriedades de uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="8087c-130">You can show this information on the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) by viewing the properties for a subscription.</span></span> |
2. <span data-ttu-id="8087c-131">Escolha um nó do ponto de extremidade e exiba a janela **Propriedades** .</span><span class="sxs-lookup"><span data-stu-id="8087c-131">Choose an endpoint node, and then view the **Properties** window.</span></span>
3. <span data-ttu-id="8087c-132">A tabela a seguir descreve as propriedades de pontos de extremidade disponíveis, mas eles são somente leitura.</span><span class="sxs-lookup"><span data-stu-id="8087c-132">The following table describes the available properties of endpoints, but they are read-only.</span></span> <span data-ttu-id="8087c-133">Para adicionar ou editar os pontos de extremidade para uma máquina virtual, use o [Portal Clássico do Azure](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="8087c-133">To add or edit the endpoints for a virtual machine, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> 
   
   | <span data-ttu-id="8087c-134">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8087c-134">Property</span></span> | <span data-ttu-id="8087c-135">Descrição</span><span class="sxs-lookup"><span data-stu-id="8087c-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="8087c-136">Nome</span><span class="sxs-lookup"><span data-stu-id="8087c-136">Name</span></span> |<span data-ttu-id="8087c-137">Um identificador para o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="8087c-137">An identifier for the endpoint.</span></span> |
   | <span data-ttu-id="8087c-138">Porta privada</span><span class="sxs-lookup"><span data-stu-id="8087c-138">Private Port</span></span> |<span data-ttu-id="8087c-139">A porta para acesso à rede interna para o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8087c-139">The port for network access internal to your application.</span></span> |
   | <span data-ttu-id="8087c-140">Protocolo</span><span class="sxs-lookup"><span data-stu-id="8087c-140">Protocol</span></span> |<span data-ttu-id="8087c-141">O protocolo de camada de transporte que este ponto de extremidade usa: TCP ou UDP.</span><span class="sxs-lookup"><span data-stu-id="8087c-141">The protocol that the transport layer for this endpoint uses, either TCP or UDP.</span></span> |
   | <span data-ttu-id="8087c-142">Porta pública</span><span class="sxs-lookup"><span data-stu-id="8087c-142">Public Port</span></span> |<span data-ttu-id="8087c-143">A porta usada para acesso público ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8087c-143">The port that’s used for public access to your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8087c-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8087c-144">Next steps</span></span>
<span data-ttu-id="8087c-145">Para saber mais sobre como usar funções do Azure no Visual Studio, consulte [usando a área de trabalho remota com funções do Azure](vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="8087c-145">To learn more about using Azure roles in Visual Studio, see [Using Remote Desktop with Azure Roles](vs-azure-tools-remote-desktop-roles.md).</span></span>

