---
title: "Limitações de colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "Limitações atuais à colaboração B2B do Azure Active Directory"
services: active-directory
documentationcenter: 
author: sasubram
manager: femila
editor: 
tags: 
ms.assetid: 
ms.service: active-directory
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: identity
ms.date: 05/23/2017
ms.author: sasubram
ms.openlocfilehash: 581e5d1fb5fb08d0dc89ed2c85edcb5f0005650b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="42c4d-103">Limitações da colaboração B2B do Azure AD</span><span class="sxs-lookup"><span data-stu-id="42c4d-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="42c4d-104">A colaboração B2B do Azure Active Directory (Azure AD) está sujeita, atualmente, às limitações descritas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="42c4d-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject to the limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="42c4d-105">Possível autenticação multifator dupla</span><span class="sxs-lookup"><span data-stu-id="42c4d-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="42c4d-106">Com B2B do Azure AD é possível impor a autenticação multifator na organização do recurso (a organização emissora do convite).</span><span class="sxs-lookup"><span data-stu-id="42c4d-106">With Azure AD B2B, you can enforce multi-factor authentication at the resource organization (the inviting organization).</span></span> <span data-ttu-id="42c4d-107">Os motivos para essa abordagem são detalhados em [Acesso condicional para usuários de colaboração B2B](active-directory-b2b-mfa-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="42c4d-107">The reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="42c4d-108">Se um parceiro já tiver uma autenticação multifator configurada e aplicada, é possível que os usuários do parceiro tenham que executar a autenticação uma vez na organização inicial e novamente na sua.</span><span class="sxs-lookup"><span data-stu-id="42c4d-108">If a partner already has multi-factor authentication set up and enforced, their users might have to perform the authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="42c4d-109">Instant-on</span><span class="sxs-lookup"><span data-stu-id="42c4d-109">Instant-on</span></span>
<span data-ttu-id="42c4d-110">Nos fluxos de colaboração B2B, adicionamos usuários ao diretório e os atualizamos dinamicamente durante o resgate do convite, atribuição do aplicativo e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="42c4d-110">In the B2B collaboration flows, we add users to the directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="42c4d-111">As atualizações e as gravações em geral ocorrem em uma instância do diretório e devem ser replicadas em todas as instâncias.</span><span class="sxs-lookup"><span data-stu-id="42c4d-111">The updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="42c4d-112">A replicação estará concluída quando todas as instâncias estiverem atualizadas.</span><span class="sxs-lookup"><span data-stu-id="42c4d-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="42c4d-113">Às vezes, quando o objeto é gravado ou atualizado em uma instância e a chamada para recuperar esse objeto for para outra instância, poderão ocorrer latências de replicação.</span><span class="sxs-lookup"><span data-stu-id="42c4d-113">Sometimes when the object is written or updated in one instance and the call to retrieve this object is to another instance, replication latencies can occur.</span></span> <span data-ttu-id="42c4d-114">Se isso acontecer, atualize ou tente novamente.</span><span class="sxs-lookup"><span data-stu-id="42c4d-114">If that happens, refresh or retry to help.</span></span> <span data-ttu-id="42c4d-115">Se você estiver gravando um aplicativo utilizando nossa API, então, tentativas com algumas retiradas é uma boa prática defensiva para aliviar esse problema.</span><span class="sxs-lookup"><span data-stu-id="42c4d-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice to alleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42c4d-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="42c4d-116">Next steps</span></span>

<span data-ttu-id="42c4d-117">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="42c4d-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="42c4d-118">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="42c4d-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="42c4d-119">Propriedades de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="42c4d-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="42c4d-120">Adicionar um usuário de colaboração B2B a uma função</span><span class="sxs-lookup"><span data-stu-id="42c4d-120">Adding a B2B collaboration user to a role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="42c4d-121">Delegar convites de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="42c4d-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="42c4d-122">Grupos dinâmicos e colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="42c4d-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="42c4d-123">Código de colaboração B2B e exemplos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="42c4d-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="42c4d-124">Configurar aplicativos SaaS para colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="42c4d-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="42c4d-125">Tokens de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="42c4d-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="42c4d-126">Mapeamento de declarações de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="42c4d-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="42c4d-127">Compartilhamento externo do Office 365</span><span class="sxs-lookup"><span data-stu-id="42c4d-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
