---
title: Criar uma identidade corporativa ou de estudante no AAD para Linux | Microsoft Docs
description: "Saiba como criar uma identidade corporativa ou de estudante no Azure Active Directory para usar com suas máquinas virtuais Linux."
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
ms.openlocfilehash: 4fdb72e3eec41d66f8561baf1755aa425ac278af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-to-use-with-linux-vms"></a><span data-ttu-id="712ac-103">Criando uma identidade Corporativa ou de Estudante no Azure Active Directory para usar com VMs Linux</span><span class="sxs-lookup"><span data-stu-id="712ac-103">Creating a Work or School identity in Azure Active Directory to use with Linux VMs</span></span>
<span data-ttu-id="712ac-104">Se você tiver criado uma conta pessoal do Azure ou tiver uma assinatura pessoal do MSDN e criou a conta do Azure para aproveitar os créditos Azure no MSDN, você usou uma identidade da *conta da Microsoft* para criá-la.</span><span class="sxs-lookup"><span data-stu-id="712ac-104">If you created a personal Azure account or have a personal MSDN subscription and created the Azure account to take advantage of the MSDN Azure credits -- you used a *Microsoft account* identity to create it.</span></span> <span data-ttu-id="712ac-105">Para que muitos recursos excelentes do Azure (como os [modelos de grupo de recursos](../../azure-resource-manager/resource-group-overview.md)) funcionem, é necessário ter uma conta corporativa ou de estudante (uma identidade gerenciada pelo Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="712ac-105">Many great features of Azure -- [resource group templates](../../azure-resource-manager/resource-group-overview.md) is one example -- require a work or school account (an identity managed by Azure Active Directory) to work.</span></span> <span data-ttu-id="712ac-106">Você pode seguir as instruções abaixo para criar uma nova conta corporativa ou de estudante, porque, felizmente, uma das melhores coisas sobre sua conta pessoal do Azure pessoal é que ela vem com um domínio do Active Directory do Azure padrão, que você pode usar para criar uma nova corporativa ou de estudante, que pode usar com os recursos do Azure que necessitam dela.</span><span class="sxs-lookup"><span data-stu-id="712ac-106">You can follow the instructions below to create a new work or school account because fortunately, one of the best things about your personal Azure account is that it comes with a default Azure Active Directory domain that you can use to create a new work or school account that you can use with Azure features that require it.</span></span>

<span data-ttu-id="712ac-107">No entanto, alterações recentes possibilitam gerenciar sua assinatura com qualquer tipo de conta do Azure usando o `azure login` método de logon interativo descrito [aqui](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="712ac-107">However, recent changes make it possible to manage your subscription with any type of Azure account using the `azure login` interactive login method described [here](../../xplat-cli-connect.md).</span></span> <span data-ttu-id="712ac-108">Você pode usar esse mecanismo, ou seguir as instruções abaixo.</span><span class="sxs-lookup"><span data-stu-id="712ac-108">You can either use that mechanism, or you can follow the instructions that follow.</span></span> <span data-ttu-id="712ac-109">Você também pode [criar uma identidade Corporativa ou de Estudante no Azure Active Directory para usar com VMs do Windows](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="712ac-109">You can also [create a work or school identity in Azure Active Directory to use with Windows VMs](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

