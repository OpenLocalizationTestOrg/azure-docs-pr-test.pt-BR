---
title: aaaCreate uma identidade ou de estudante no AAD para Linux | Microsoft Docs
description: "Saiba como toocreate uma identidade ou de estudante no Active Directory do Azure toouse com máquinas virtuais Linux."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: b0f86d77-c669-4aa1-a095-c2aa4d9105fe
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: 54c3d0b0e89fe1b2d6a9b58a46776fe446ed72b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-linux-vms"></a><span data-ttu-id="3324a-103">Criando uma identidade de empresa ou escola no Active Directory do Azure toouse com VMs do Linux</span><span class="sxs-lookup"><span data-stu-id="3324a-103">Creating a Work or School identity in Azure Active Directory toouse with Linux VMs</span></span>
<span data-ttu-id="3324a-104">Se você criou uma conta do Azure pessoal ou ter uma assinatura do MSDN pessoal e criado Olá conta do Azure tootake aproveitar créditos do Azure MSDN hello – você usou uma *conta da Microsoft* identidade toocreate-lo.</span><span class="sxs-lookup"><span data-stu-id="3324a-104">If you created a personal Azure account or have a personal MSDN subscription and created hello Azure account tootake advantage of hello MSDN Azure credits -- you used a *Microsoft account* identity toocreate it.</span></span> <span data-ttu-id="3324a-105">Muitos recursos excelentes do Azure – [modelos de grupo de recursos](../../azure-resource-manager/resource-group-overview.md) é um exemplo – requerem uma conta corporativa ou de Estudante (uma identidade gerenciada pelo Active Directory do Azure) toowork.</span><span class="sxs-lookup"><span data-stu-id="3324a-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) toowork.</span></span> <span data-ttu-id="3324a-106">Você pode seguir as instruções de saudação abaixo toocreate que um novo trabalho ou escola conta porque Felizmente, uma das melhores coisas Olá sobre sua conta do Azure pessoal é que ela vem com um domínio do Active Directory do Azure padrão que você pode usar toocreate um novo trabalho ou escola conta que você pode usar com os recursos do Azure que a exigem.</span><span class="sxs-lookup"><span data-stu-id="3324a-106">You can follow hello instructions below toocreate a new work or school account because fortunately, one of hello best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use toocreate a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="3324a-107">No entanto, alterações recentes torná-lo toomanage possíveis sua assinatura com qualquer tipo de conta do Azure usando Olá `azure login` método de logon interativo descrito [aqui](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="3324a-107">However, recent changes make it possible toomanage your subscription with any type of Azure account using hello `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="3324a-108">Você pode usar esse mecanismo, ou você pode seguir as instruções de saudação que seguem.</span><span class="sxs-lookup"><span data-stu-id="3324a-108">You can either use that mechanism, or you can follow hello instructions that follow.</span></span> <span data-ttu-id="3324a-109">Você também pode [criar uma identidade ou de estudante no Active Directory do Azure toouse com VMs do Windows](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3324a-109">You can also [create a work or school identity in Azure Active Directory toouse with Windows VMs](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

