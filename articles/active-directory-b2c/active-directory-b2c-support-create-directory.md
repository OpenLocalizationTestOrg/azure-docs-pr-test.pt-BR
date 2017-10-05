---
title: "Azure Active Directory B2C: solucionar problemas criando locatários | Microsoft Docs"
description: "Problemas e resoluções para criar um Azure Active Directory ou um locatário do Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 7ba4c6b2-161b-45b5-b3bd-ccb662f5d7a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 81af4536fc223319369aff262d42149cfbf1a1e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="77ad5-103">Problemas e resoluções para criar um Azure Active Directory ou um locatário do Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="77ad5-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="77ad5-104">Criar um locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="77ad5-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="77ad5-105">Caso não consiga criar um locatário do Azure Active Directory (Azure AD) na primeira tentativa, tente novamente.</span><span class="sxs-lookup"><span data-stu-id="77ad5-105">If you can't create an Azure Active Directory (Azure AD) tenant on the first attempt, try again.</span></span> <span data-ttu-id="77ad5-106">Se o problema persistir, contate o Suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="77ad5-106">If the problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="77ad5-107">Criar um locatário do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="77ad5-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="77ad5-108">Se você encontrar problemas ao [criar um locatário do Azure Active Directory B2C (Azure AD B2C)](active-directory-b2c-get-started.md), tente as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="77ad5-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try the following options:</span></span>

* <span data-ttu-id="77ad5-109">Se o locatário do Azure AD B2C não aparecer na lista de locatários, tente criá-lo novamente.</span><span class="sxs-lookup"><span data-stu-id="77ad5-109">If the Azure AD B2C tenant doesn't show up in your list of tenants, try again to create the tenant.</span></span>
* <span data-ttu-id="77ad5-110">Se o locatário do Azure AD B2C aparecer na sua lista de locatários e você vir a seguinte mensagem de erro, exclua o locatário e crie-o novamente:</span><span class="sxs-lookup"><span data-stu-id="77ad5-110">If the Azure AD B2C tenant does show up in your list of tenants and you see the following  error message, delete the tenant and create it again:</span></span>

    <span data-ttu-id="77ad5-111">"Não foi possível concluir a criação do locatário B2C 'contosob2c'.</span><span class="sxs-lookup"><span data-stu-id="77ad5-111">"Could not complete the creation of the B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="77ad5-112">Acesse este [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) para obter mais diretrizes".</span><span class="sxs-lookup"><span data-stu-id="77ad5-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="77ad5-113">Há problemas conhecidos quando você exclui um locatário do Azure AD B2C existente e o recria com o mesmo nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="77ad5-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using the same domain name.</span></span> <span data-ttu-id="77ad5-114">Quando você criar um novo locatário do Azure AD B2C, você deverá usar um nome de domínio diferente.</span><span class="sxs-lookup"><span data-stu-id="77ad5-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="77ad5-115">Se essas resoluções não funcionarem, entre em contato com o Suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="77ad5-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="77ad5-116">Para obter mais informações, consulte [Arquivar solicitações de suporte para o Azure AD B2C](active-directory-b2c-support.md).</span><span class="sxs-lookup"><span data-stu-id="77ad5-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>

