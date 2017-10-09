---
title: "aaaTroubleshooting VM Linux falhas de alocação | Microsoft Docs"
description: "Solucionar problemas de falhas de alocação ao criar, reiniciar ou redimensionar uma VM do Linux no Azure"
services: virtual-machines-linux, azure-resource-manager
documentationcenter: 
author: JiangChen79
manager: felixwu
editor: 
tags: top-support-issue,azure-resourece-manager,azure-service-management
ms.assetid: 1ef41144-6dd6-4a56-b180-9d8b3d05eae7
ms.service: virtual-machines-linux
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cjiang
ms.openlocfilehash: 502fbb406b0b4acf086c2586795f69a44cc1a004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-allocation-failures-when-you-create-restart-or-resize-linux-vms-in-azure"></a><span data-ttu-id="8f345-103">Solucionar problemas de falhas de alocação ao criar, reiniciar ou redimensionar VMs do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="8f345-103">Troubleshoot allocation failures when you create, restart, or resize Linux VMs in Azure</span></span>
<span data-ttu-id="8f345-104">Quando você cria uma VM, reiniciar paradas VMs (desalocadas) ou redimensiona uma VM, o Microsoft Azure aloca recursos de computação tooyour assinatura.</span><span class="sxs-lookup"><span data-stu-id="8f345-104">When you create a VM, restart stopped (deallocated) VMs, or resize a VM, Microsoft Azure allocates compute resources tooyour subscription.</span></span> <span data-ttu-id="8f345-105">Ocasionalmente, você poderá receber erros ao executar essas operações – mesmo antes de atingir Olá limites de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f345-105">You may occasionally receive errors when performing these operations -- even before you reach hello Azure subscription limits.</span></span> <span data-ttu-id="8f345-106">Este artigo explica as causas de saudação de alguns Olá comuns de falhas de alocação e sugere possíveis correções.</span><span class="sxs-lookup"><span data-stu-id="8f345-106">This article explains hello causes of some of hello common allocation failures and suggests possible remediation.</span></span> <span data-ttu-id="8f345-107">informações de saudação também podem ser útil ao planejar a implantação Olá dos seus serviços.</span><span class="sxs-lookup"><span data-stu-id="8f345-107">hello information may also be useful when you plan hello deployment of your services.</span></span> <span data-ttu-id="8f345-108">Também é possível [solucionar problemas de falhas de alocação ao criar, reiniciar ou redimensionar VMs do Windows no Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f345-108">You can also [troubleshoot allocation failures when you create, restart, or resize Windows VMs in Azure](../windows/allocation-failure.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-allocation-failure](../../../includes/virtual-machines-common-allocation-failure.md)]

