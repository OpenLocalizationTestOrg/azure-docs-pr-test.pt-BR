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
ms.openlocfilehash: 4bb7ec6ec67d3368a0e36c098f290f582510714a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a><span data-ttu-id="df61f-103">Problemas e resoluções para criar um Azure Active Directory ou um locatário do Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="df61f-103">Troubleshoot creating an Azure Active Directory or Azure Active Directory B2C tenant</span></span> 

## <a name="create-an-azure-ad-tenant"></a><span data-ttu-id="df61f-104">Criar um locatário do Azure AD</span><span class="sxs-lookup"><span data-stu-id="df61f-104">Create an Azure AD tenant</span></span>
<span data-ttu-id="df61f-105">Se você não pode criar um locatário do Azure Active Directory (AD do Azure) na primeira tentativa de hello, tente novamente.</span><span class="sxs-lookup"><span data-stu-id="df61f-105">If you can't create an Azure Active Directory (Azure AD) tenant on hello first attempt, try again.</span></span> <span data-ttu-id="df61f-106">Se Olá problema persistir, entre em contato com o suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="df61f-106">If hello problem persists, contact Azure Support.</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="df61f-107">Criar um locatário do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="df61f-107">Create an Azure AD B2C tenant</span></span>
<span data-ttu-id="df61f-108">Se você encontrar problemas quando você [criar um B2C do Azure Active Directory (Azure AD B2C) locatário](active-directory-b2c-get-started.md), tente Olá as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="df61f-108">If you encounter issues when you [create an Azure Active Directory B2C (Azure AD B2C) tenant](active-directory-b2c-get-started.md), try hello following options:</span></span>

* <span data-ttu-id="df61f-109">Se o locatário de saudação do Azure AD B2C não aparecer na lista de locatários, tente novamente toocreate locatário de saudação.</span><span class="sxs-lookup"><span data-stu-id="df61f-109">If hello Azure AD B2C tenant doesn't show up in your list of tenants, try again toocreate hello tenant.</span></span>
* <span data-ttu-id="df61f-110">Se o locatário hello Azure AD B2C aparecerão na lista de locatários e consulte Olá a seguinte mensagem de erro, exclua locatário hello e criá-la novamente:</span><span class="sxs-lookup"><span data-stu-id="df61f-110">If hello Azure AD B2C tenant does show up in your list of tenants and you see hello following  error message, delete hello tenant and create it again:</span></span>

    <span data-ttu-id="df61f-111">"Não foi possível concluir a criação de saudação do locatário de B2C Olá 'contosob2c'.</span><span class="sxs-lookup"><span data-stu-id="df61f-111">"Could not complete hello creation of hello B2C tenant 'contosob2c'.</span></span> <span data-ttu-id="df61f-112">Acesse este [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) para obter mais diretrizes".</span><span class="sxs-lookup"><span data-stu-id="df61f-112">Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance."</span></span>
* <span data-ttu-id="df61f-113">Há são problemas conhecidos quando você excluir um existente B2C de AD do Azure locatário e recriá-la usando Olá mesmo nome de domínio.</span><span class="sxs-lookup"><span data-stu-id="df61f-113">There are known issues when you delete an existing Azure AD B2C tenant and re-create it by using hello same domain name.</span></span> <span data-ttu-id="df61f-114">Quando você criar um novo locatário do Azure AD B2C, você deverá usar um nome de domínio diferente.</span><span class="sxs-lookup"><span data-stu-id="df61f-114">When you create a new Azure AD B2C tenant, you must use a different domain name.</span></span>
* <span data-ttu-id="df61f-115">Se essas resoluções não funcionarem, entre em contato com o Suporte do Azure.</span><span class="sxs-lookup"><span data-stu-id="df61f-115">If these resolutions don't work, contact Azure Support.</span></span> <span data-ttu-id="df61f-116">Para obter mais informações, consulte [Arquivar solicitações de suporte para o Azure AD B2C](active-directory-b2c-support.md).</span><span class="sxs-lookup"><span data-stu-id="df61f-116">For more information, see [File support requests for Azure AD B2C](active-directory-b2c-support.md).</span></span>

