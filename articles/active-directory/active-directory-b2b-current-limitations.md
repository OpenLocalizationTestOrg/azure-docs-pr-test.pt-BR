---
title: "aaaLimitations de colaboração B2B do Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: 322081f32fbacfe67ee1300993c7df1870e498bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-ad-b2b-collaboration"></a><span data-ttu-id="dc5f5-103">Limitações da colaboração B2B do Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc5f5-103">Limitations of Azure AD B2B collaboration</span></span>
<span data-ttu-id="dc5f5-104">Colaboração B2B do Active Directory (AD do Azure) do Azure está atualmente limitações do assunto toohello descritas neste artigo.</span><span class="sxs-lookup"><span data-stu-id="dc5f5-104">Azure Active Directory (Azure AD) B2B collaboration is currently subject toohello limitations described in this article.</span></span>

## <a name="possible-double-multi-factor-authentication"></a><span data-ttu-id="dc5f5-105">Possível autenticação multifator dupla</span><span class="sxs-lookup"><span data-stu-id="dc5f5-105">Possible double multi-factor authentication</span></span>
<span data-ttu-id="dc5f5-106">Com o Azure AD B2B, você pode impor autenticação multifator na organização do recurso hello (Olá convidar organização).</span><span class="sxs-lookup"><span data-stu-id="dc5f5-106">With Azure AD B2B, you can enforce multi-factor authentication at hello resource organization (hello inviting organization).</span></span> <span data-ttu-id="dc5f5-107">motivos Olá para essa abordagem são detalhados no [acesso condicional para usuários de colaboração B2B](active-directory-b2b-mfa-instructions.md).</span><span class="sxs-lookup"><span data-stu-id="dc5f5-107">hello reasons for this approach are detailed in [Conditional access for B2B collaboration users](active-directory-b2b-mfa-instructions.md).</span></span> <span data-ttu-id="dc5f5-108">Se um parceiro já tiver configurado e aplicadas a autenticação multifator, seus usuários podem ter autenticação de saudação tooperform uma vez em sua organização inicial e, em seguida, novamente no seu.</span><span class="sxs-lookup"><span data-stu-id="dc5f5-108">If a partner already has multi-factor authentication set up and enforced, their users might have tooperform hello authentication once in their home organization and then again in yours.</span></span>

## <a name="instant-on"></a><span data-ttu-id="dc5f5-109">Instant-on</span><span class="sxs-lookup"><span data-stu-id="dc5f5-109">Instant-on</span></span>
<span data-ttu-id="dc5f5-110">Em fluxos de colaboração B2B do hello, vamos adicionar usuários toohello diretório e dinamicamente atualizá-los durante o resgate de convite, atribuição de aplicativo e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="dc5f5-110">In hello B2B collaboration flows, we add users toohello directory and dynamically update them during invitation redemption, app assignment, and so on.</span></span> <span data-ttu-id="dc5f5-111">Olá atualizações e gravações normalmente acontecem na instância de um diretório e devem ser replicadas em todas as instâncias.</span><span class="sxs-lookup"><span data-stu-id="dc5f5-111">hello updates and writes ordinarily happen in one directory instance and must be replicated across all instances.</span></span> <span data-ttu-id="dc5f5-112">A replicação estará concluída quando todas as instâncias estiverem atualizadas.</span><span class="sxs-lookup"><span data-stu-id="dc5f5-112">Replication is completed once all instances are updated.</span></span> <span data-ttu-id="dc5f5-113">Às vezes, quando objeto Olá é gravado ou atualizado em uma instância e Olá chamar tooretrieve esse objeto é instância tooanother, latências de replicação podem ocorrer.</span><span class="sxs-lookup"><span data-stu-id="dc5f5-113">Sometimes when hello object is written or updated in one instance and hello call tooretrieve this object is tooanother instance, replication latencies can occur.</span></span> <span data-ttu-id="dc5f5-114">Se isso acontecer, atualize ou tente novamente toohelp.</span><span class="sxs-lookup"><span data-stu-id="dc5f5-114">If that happens, refresh or retry toohelp.</span></span> <span data-ttu-id="dc5f5-115">Se você estiver escrevendo um aplicativo usando nossa API, novas tentativas com alguns retirada é uma boa prática defesa tooalleviate esse problema.</span><span class="sxs-lookup"><span data-stu-id="dc5f5-115">If you are writing an app using our API, then retries with some back-off is a good, defensive practice tooalleviate this issue.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc5f5-116">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dc5f5-116">Next steps</span></span>

<span data-ttu-id="dc5f5-117">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="dc5f5-117">Browse our other articles on Azure AD B2B collaboration:</span></span>

* [<span data-ttu-id="dc5f5-118">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="dc5f5-118">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="dc5f5-119">Propriedades de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="dc5f5-119">B2B collaboration user properties</span></span>](active-directory-b2b-user-properties.md)
* [<span data-ttu-id="dc5f5-120">Adicionando uma função de tooa de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="dc5f5-120">Adding a B2B collaboration user tooa role</span></span>](active-directory-b2b-add-guest-to-role.md)
* [<span data-ttu-id="dc5f5-121">Delegar convites de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="dc5f5-121">Delegate B2bB collaboration invitations</span></span>](active-directory-b2b-delegate-invitations.md)
* [<span data-ttu-id="dc5f5-122">Grupos dinâmicos e colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="dc5f5-122">Dynamic groups and B2B collaboration</span></span>](active-directory-b2b-dynamic-groups.md)
* [<span data-ttu-id="dc5f5-123">Código de colaboração B2B e exemplos do PowerShell</span><span class="sxs-lookup"><span data-stu-id="dc5f5-123">B2B collaboration code and PowerShell samples</span></span>](active-directory-b2b-code-samples.md)
* [<span data-ttu-id="dc5f5-124">Configurar aplicativos SaaS para colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="dc5f5-124">Configure SaaS apps for B2B collaboration</span></span>](active-directory-b2b-configure-saas-apps.md)
* [<span data-ttu-id="dc5f5-125">Tokens de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="dc5f5-125">B2B collaboration user tokens</span></span>](active-directory-b2b-user-token.md)
* [<span data-ttu-id="dc5f5-126">Mapeamento de declarações de usuário de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="dc5f5-126">B2B collaboration user claims mapping</span></span>](active-directory-b2b-claims-mapping.md)
* [<span data-ttu-id="dc5f5-127">Compartilhamento externo do Office 365</span><span class="sxs-lookup"><span data-stu-id="dc5f5-127">Office 365 external sharing</span></span>](active-directory-b2b-o365-external-user.md)
