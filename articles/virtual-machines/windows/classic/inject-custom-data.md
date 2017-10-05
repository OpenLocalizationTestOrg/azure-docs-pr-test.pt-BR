---
title: Injetar dados em VMs do Windows no Azure | Microsoft Docs
description: "Este tópico descreve como injetar dados personalizados em uma máquina virtual do Azure quando a instância é criada e como localizar os dados personalizados no Windows ou Linux."
services: virtual-machines-windows
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 48759f76-eaa0-4202-ada0-706d3f9a9467
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 7836577f16940b618a2912012ba8a8e7160980e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="injecting-custom-data-into-an-azure-virtual-machine"></a><span data-ttu-id="fcf47-103">Injetando dados personalizados em uma máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="fcf47-103">Injecting custom data into an Azure virtual machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="fcf47-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fcf47-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fcf47-105">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="fcf47-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="fcf47-106">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="fcf47-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="fcf47-107">Para obter informações sobre como usar a Extensão de Script personalizado com o modelo do Resource Manager, veja [aqui](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fcf47-107">For information about using the Custom Script Extension with the Resource Manager model, see [here](../extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-classic-inject-custom-data](../../../../includes/virtual-machines-common-classic-inject-custom-data.md)]

