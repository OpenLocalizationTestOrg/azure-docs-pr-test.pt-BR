---
title: "<span data-ttu-id=\"b4351-101\">Agente e extensões de VM do Linux no Azure | Microsoft Docs</span><span class=\"sxs-lookup\"><span data-stu-id=\"b4351-101\">Linux VM agent and extensions in Azure | Microsoft Docs</span></span>"
description: "<span data-ttu-id=\"b4351-102\">Fornece uma visão geral do agente e das extensões e de como instalar o agente usando o modelo de implantação clássico em uma VM Linux.</span><span class=\"sxs-lookup\"><span data-stu-id=\"b4351-102\">Gives an overview of the agent and extensions, and how to install the agent, using the classic deployment model on a Linux VM.</span></span>"
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b41e3b21-9132-4d8d-804d-34920b2d0942
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: rasquill
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 06b802c408ea5d1b2b40d05321e1a0014e99ca8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="about-the-virtual-machine-agent-and-extensions-for-linux"></a><span data-ttu-id="b4351-103">Sobre o agente e as extensões da máquina virtual para Linux</span><span class="sxs-lookup"><span data-stu-id="b4351-103">About the virtual machine agent and extensions for Linux</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b4351-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b4351-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="b4351-105">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="b4351-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="b4351-106">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="b4351-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="b4351-107">Para obter informações sobre agentes e extensões de VM usando o Resource Manager, veja [aqui](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b4351-107">For information about VM agents and extensions using Resource Manager, see [here](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-agents-and-extensions](../../../../includes/virtual-machines-common-classic-agents-and-extensions.md)]
