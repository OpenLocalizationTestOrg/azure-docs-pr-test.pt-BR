---
title: "portal inscrição do serviço aaaSelf para colaboração B2B do Azure Active Directory | Microsoft Docs"
description: "As relações entre empresas dá suporte à colaboração B2B do Active Directory do Azure, permitindo que os aplicativos corporativos tooselectively de parceiros de negócios acesso"
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
ms.date: 05/24/2017
ms.author: sasubram
ms.openlocfilehash: c78920ecf812f7efc06a8b54b1fff834c32904f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-portal-for-azure-ad-b2b-collaboration-sign-up"></a><span data-ttu-id="66208-103">Portal de autoatendimento para inscrição na colaboração B2B do Azure AD</span><span class="sxs-lookup"><span data-stu-id="66208-103">Self-service portal for Azure AD B2B collaboration sign-up</span></span>

<span data-ttu-id="66208-104">Os clientes podem fazer muito com recursos internos de saudação que são expostos por meio de nosso administrador de TI [portal do Azure](https://portal.azure.com) e nossa [painel de acesso do aplicativo](https://myapps.microsoft.com) para os usuários finais.</span><span class="sxs-lookup"><span data-stu-id="66208-104">Customers can do a lot with hello built-in features that are exposed through our IT admin [Azure portal](https://portal.azure.com) and our [Application Access Panel](https://myapps.microsoft.com) for end users.</span></span> <span data-ttu-id="66208-105">Mas também estamos cientes de que as empresas precisam de fluxo de trabalho de integração de saudação toocustomize para B2B usuários toofit as necessidades da sua organização.</span><span class="sxs-lookup"><span data-stu-id="66208-105">But we are also aware that businesses need toocustomize hello onboarding workflow for B2B users toofit their organization’s needs.</span></span> <span data-ttu-id="66208-106">Eles podem fazer isso com a [nossa API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span><span class="sxs-lookup"><span data-stu-id="66208-106">They can do that with [our API](https://developer.microsoft.com/graph/docs/api-reference/v1.0/resources/invitation).</span></span>

<span data-ttu-id="66208-107">Ao discutir isso com nossos clientes, vimos uma necessidade comum se destacar das outras.</span><span class="sxs-lookup"><span data-stu-id="66208-107">In discussions with our customers, we see one common need rise up above all others.</span></span> <span data-ttu-id="66208-108">Olá convidar organização pode não saber antecipadamente que Olá parceiros externos individuais são que precisam acessar os recursos de tootheir.</span><span class="sxs-lookup"><span data-stu-id="66208-108">hello inviting organization may not know ahead of time who hello individual external collaborators are who need access tootheir resources.</span></span> <span data-ttu-id="66208-109">Quisessem uma maneira para os usuários de empresas parceiras muito inscrever-se com um conjunto de políticas que Olá convidar controles da organização.</span><span class="sxs-lookup"><span data-stu-id="66208-109">They wanted a way for users from partner companies too sign themselves up with a set of policies that hello inviting organization controls.</span></span> <span data-ttu-id="66208-110">Esse cenário é possível por meio de nossas APIs, portanto, publicamos um projeto no Github que fez exatamente isso: [exemplo de projeto no Github](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span><span class="sxs-lookup"><span data-stu-id="66208-110">This scenario is possible through our APIs,  so we published a project on Github that did just that: [sample Github project](https://github.com/Azure/active-directory-dotnet-graphapi-b2bportal-web).</span></span>

<span data-ttu-id="66208-111">Nosso projeto Github demonstra como as organizações podem usar nossas APIs e fornecem um recurso de inscrição de autoatendimento, baseado em políticas para seus parceiros confiáveis, com as regras que determinam a saudação aplicativos que eles possam acessar.</span><span class="sxs-lookup"><span data-stu-id="66208-111">Our Github project demonstrates how organizations can use our APIs, and provide a policy-based, self-service sign-up capability for their trusted partners, with rules that determine hello apps they can access.</span></span> <span data-ttu-id="66208-112">Os usuários do parceiro podem obter acesso tooresources quando necessário, com segurança, sem a necessidade de saudação convidar organização toomanually integrá-los.</span><span class="sxs-lookup"><span data-stu-id="66208-112">Partner users can get access tooresources when they need them, securely, without requiring hello inviting organization toomanually onboard them.</span></span> <span data-ttu-id="66208-113">Você pode facilmente implantar projeto Olá em uma assinatura do Azure de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="66208-113">You can easily deploy hello project into an Azure subscription of your choice.</span></span>

## <a name="as-is-code"></a><span data-ttu-id="66208-114">Código no estado em que se encontra</span><span class="sxs-lookup"><span data-stu-id="66208-114">As-is code</span></span>

<span data-ttu-id="66208-115">Lembre-se de que esse código é disponibilizado como um exemplo de uso toodemonstrate de convite de saudação do Azure Active Directory B2B API.</span><span class="sxs-lookup"><span data-stu-id="66208-115">Remember that this code is made available as a sample toodemonstrate usage of hello Azure Active Directory B2B invitation API.</span></span> <span data-ttu-id="66208-116">Ele deve ser personalizado pela sua equipe de desenvolvimento ou por um parceiro e deve ser revisado antes de ser implantado em um cenário de produção.</span><span class="sxs-lookup"><span data-stu-id="66208-116">It should be customized by your dev team or a partner, and should be reviewed before being deployed in a production scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66208-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="66208-117">Next steps</span></span>

<span data-ttu-id="66208-118">Procure nossos outros artigos sobre a colaboração B2B do AD do Azure:</span><span class="sxs-lookup"><span data-stu-id="66208-118">Browse our other articles on Azure AD B2B collaboration:</span></span>
* [<span data-ttu-id="66208-119">O que é a colaboração B2B do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="66208-119">What is Azure AD B2B collaboration?</span></span>](active-directory-b2b-what-is-azure-ad-b2b.md)
* [<span data-ttu-id="66208-120">Como os administradores do Azure Active Directory adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="66208-120">How do Azure Active Directory admins add B2B collaboration users?</span></span>](active-directory-b2b-admin-add-users.md)
* [<span data-ttu-id="66208-121">Como os operadores de informação adicionam usuários de colaboração B2B?</span><span class="sxs-lookup"><span data-stu-id="66208-121">How do information workers add B2B collaboration users?</span></span>](active-directory-b2b-iw-add-users.md)
* [<span data-ttu-id="66208-122">elementos de saudação do hello email de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="66208-122">hello elements of hello B2B collaboration invitation email</span></span>](active-directory-b2b-invitation-email.md)
* [<span data-ttu-id="66208-123">Resgate de convite de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="66208-123">B2B collaboration invitation redemption</span></span>](active-directory-b2b-redemption-experience.md)
* [<span data-ttu-id="66208-124">Licenciamento da colaboração B2B do Azure AD</span><span class="sxs-lookup"><span data-stu-id="66208-124">Azure AD B2B collaboration licensing</span></span>](active-directory-b2b-licensing.md)
* [<span data-ttu-id="66208-125">Solução de problemas de colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66208-125">Troubleshooting Azure Active Directory B2B collaboration</span></span>](active-directory-b2b-troubleshooting.md)
* [<span data-ttu-id="66208-126">Perguntas frequentes sobre a colaboração B2B do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="66208-126">Azure Active Directory B2B collaboration frequently asked questions (FAQ)</span></span>](active-directory-b2b-faq.md)
* [<span data-ttu-id="66208-127">Autenticação multifator para usuários de colaboração B2B</span><span class="sxs-lookup"><span data-stu-id="66208-127">Multi-factor authentication for B2B collaboration users</span></span>](active-directory-b2b-mfa-instructions.md)
* [<span data-ttu-id="66208-128">Adicionar usuários de colaboração B2B sem um convite</span><span class="sxs-lookup"><span data-stu-id="66208-128">Add B2B collaboration users without an invitation</span></span>](active-directory-b2b-add-user-without-invite.md)
* [<span data-ttu-id="66208-129">Índice de artigos para Gerenciamento de Aplicativos no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="66208-129">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)