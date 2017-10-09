---
title: "falhas de alocação de VM do Windows aaaTroubleshooting | Microsoft Docs"
description: "Solucionar problemas de falhas de alocação ao criar, reiniciar ou redimensionar uma VM do Windows no Azure"
services: virtual-machines-windows, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resource-manager,azure-service-management
ms.assetid: bb939e23-77fc-4948-96f7-5037761c30e8
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: cjiang
ms.openlocfilehash: d0cc75ac60d952d8e4310cebc37654dc4f80857f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-windows-vms-in-azure"></a><span data-ttu-id="fd89f-103">Solucionar problemas de falhas de alocação ao criar, reiniciar ou redimensionar VMs do Windows no Azure</span><span class="sxs-lookup"><span data-stu-id="fd89f-103">Troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure</span></span>
<span data-ttu-id="fd89f-104">Quando você cria uma VM, reiniciar paradas VMs (desalocadas) ou redimensiona uma VM, o Microsoft Azure aloca recursos de computação tooyour assinatura.</span><span class="sxs-lookup"><span data-stu-id="fd89f-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources tooyour subscription.</span></span> <span data-ttu-id="fd89f-105">Ocasionalmente, você poderá receber erros ao executar essas operações – mesmo antes de atingir Olá limites de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="fd89f-105">You may occasionally receive errors when performing these operations -- even before you reach hello Azure subscription limits.</span></span> <span data-ttu-id="fd89f-106">Este artigo explica as causas de saudação de alguns Olá comuns de falhas de alocação e sugere possíveis correções.</span><span class="sxs-lookup"><span data-stu-id="fd89f-106">This article explains hello causes of some of hello common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="fd89f-107">informações de saudação também podem ser útil ao planejar a implantação Olá dos seus serviços.</span><span class="sxs-lookup"><span data-stu-id="fd89f-107">hello information may also be useful when you plan hello deployment of your services.</span></span> <span data-ttu-id="fd89f-108">Também é possível [solucionar problemas de falhas de alocação ao criar, reiniciar ou redimensionar VMs do Linux no Azure](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fd89f-108">You can also [troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure](../linux/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

