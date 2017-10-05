---
title: "Conjuntos de disponibilidade para as VMs clássicas do Linux | Microsoft Docs"
description: "Configure um conjunto de disponibilidade para uma máquina virtual do Linux nova ou existente no modelo de implantação clássico usando o Portal do Azure e o Azure PowerShell."
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
ms.openlocfilehash: 41d427862150d17e1ad726afc51114d6f62f5a8e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-configure-an-availability-set-for-linux-virtual-machines-in-the-classic-deployment-model"></a><span data-ttu-id="f4fc1-103">Como configurar um conjunto de disponibilidade para máquinas virtuais do Linux no modelo de implantação clássico</span><span class="sxs-lookup"><span data-stu-id="f4fc1-103">How to configure an availability set for Linux virtual machines in the classic deployment model</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="f4fc1-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f4fc1-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f4fc1-105">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="f4fc1-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="f4fc1-106">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="f4fc1-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="f4fc1-107">Você também pode [configurar os conjuntos de disponibilidades](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) nas implantações do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="f4fc1-107">You can also [configure availability sets](../../azure-cli-arm-commands.md#azure-availset-commands-to-manage-your-availability-sets) in Resource Manager deployments.</span></span>

[!INCLUDE [virtual-machines-common-classic-configure-availability](../../../../includes/virtual-machines-common-classic-configure-availability.md)]