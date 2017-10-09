---
title: "Define aaaAvailability para VMs do Linux clássica | Microsoft Docs"
description: "Configure uma conjunto de disponibilidade para uma máquina virtual nova ou existente Linux modelo de implantação clássico hello usando hello portal do Azure e o Azure PowerShell."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b8624315-beca-4ec7-8441-2e98b166b548
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2016
ms.author: cynthn
ms.openlocfilehash: 8d8d041e3540e42a1921f5665469a2fdcaa30a29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-availability-set-for-linux-virtual-machines-in-hello-classic-deployment-model"></a><span data-ttu-id="0cf77-103">Como tooconfigure uma conjunto de disponibilidade para máquinas virtuais Linux no modelo de implantação clássico Olá</span><span class="sxs-lookup"><span data-stu-id="0cf77-103">How tooconfigure an availability set for Linux virtual machines in hello classic deployment model</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="0cf77-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0cf77-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0cf77-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="0cf77-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="0cf77-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0cf77-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="0cf77-107">Você também pode [configurar os conjuntos de disponibilidades](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) nas implantações do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="0cf77-107">You can also [configure availability sets](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) in Resource Manager deployments.</span></span>

[!INCLUDE [virtual-machines-common-classic-configure-availability](../../../../includes/virtual-machines-common-classic-configure-availability.md)]