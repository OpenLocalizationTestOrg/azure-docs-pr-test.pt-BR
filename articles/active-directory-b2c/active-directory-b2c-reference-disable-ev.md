---
title: "Azure Active Directory B2C: Desabilitar a verificação de email durante a inscrição do consumidor | Microsoft Docs"
description: "Um tópico demonstra como toodisable email verificação durante a inscrição no Azure Active Directory B2C do consumidor"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="621c6-103">Azure Active Directory B2C: Desabilitar a verificação de email durante a inscrição do consumidor</span><span class="sxs-lookup"><span data-stu-id="621c6-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="621c6-104">Quando habilitada, B2C do Azure Active Directory (AD do Azure) fornece um consumidor Olá toosign de capacidade para aplicativos fornecendo um endereço de email e criar uma conta local.</span><span class="sxs-lookup"><span data-stu-id="621c6-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer hello ability toosign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="621c6-105">B2C do AD do Azure garante endereços de email válidos exigindo que os consumidores tooverify-los durante o processo de inscrição hello.</span><span class="sxs-lookup"><span data-stu-id="621c6-105">Azure AD B2C ensures valid email addresses by requiring consumers tooverify them during hello sign-up process.</span></span> <span data-ttu-id="621c6-106">Ele também impede que um processo automatizado mal-intencionado gerar falsas contas para aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="621c6-106">It also prevents a malicious automated process from generating fake accounts for hello applications.</span></span>

<span data-ttu-id="621c6-107">Alguns desenvolvedores de aplicativo preferem tooskip verificação de email durante o processo de inscrição hello e em vez disso, tem consumidores verificar o endereço de email hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="621c6-107">Some application developers prefer tooskip email verification during hello sign-up process and instead have consumers verify hello email address later.</span></span> <span data-ttu-id="621c6-108">toosupport, B2C do Azure AD pode ser configurado toodisable de verificação do email.</span><span class="sxs-lookup"><span data-stu-id="621c6-108">toosupport this, Azure AD B2C can be configured toodisable email verification.</span></span> <span data-ttu-id="621c6-109">Isso cria um processo de inscrição mais suave e oferece aos desenvolvedores Olá flexibilidade toodifferentiate Olá os consumidores que verificaram seu endereço de email de que esses clientes que não tenham.</span><span class="sxs-lookup"><span data-stu-id="621c6-109">Doing so creates a smoother sign-up process and gives developers hello flexibility toodifferentiate hello consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="621c6-110">Por padrão, as políticas de inscrição têm a verificação de email ativada.</span><span class="sxs-lookup"><span data-stu-id="621c6-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="621c6-111">Use Olá seguindo as etapas tooturn-desativar:</span><span class="sxs-lookup"><span data-stu-id="621c6-111">Use hello following steps tooturn it off:</span></span>

1. <span data-ttu-id="621c6-112">[Siga essas folha de recursos etapas toonavigate toohello B2C Olá portal do Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="621c6-112">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="621c6-113">Clique em **Políticas de inscrição** ou em **Políticas de inscrição ou entrada** dependendo do que você configurou para inscrição.</span><span class="sxs-lookup"><span data-stu-id="621c6-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="621c6-114">Clique em sua política (por exemplo, "B2C_1_SiUp") tooopen-lo.</span><span class="sxs-lookup"><span data-stu-id="621c6-114">Click your policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="621c6-115">Clique em **editar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="621c6-115">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="621c6-116">Clique em **Personalização da interface do usuário da página**.</span><span class="sxs-lookup"><span data-stu-id="621c6-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="621c6-117">Clique em **Página de inscrição da conta local**.</span><span class="sxs-lookup"><span data-stu-id="621c6-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="621c6-118">Clique em **endereço de Email** em Olá **nome** coluna sob Olá **inscrição atributos** seção.</span><span class="sxs-lookup"><span data-stu-id="621c6-118">Click **Email Address** in hello **Name** column under hello **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="621c6-119">Saudação de alternância **Exigir verificação** opção muito**não**.</span><span class="sxs-lookup"><span data-stu-id="621c6-119">Toggle hello **Require verification** option too**No**.</span></span>
8. <span data-ttu-id="621c6-120">Clique em **Okey** na parte inferior da saudação até chegar Olá **Editar política** folha.</span><span class="sxs-lookup"><span data-stu-id="621c6-120">Click **OK** at hello bottom until you reach hello **Edit policy** blade.</span></span>
9. <span data-ttu-id="621c6-121">Clique em **salvar** na parte superior de saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="621c6-121">Click **Save** at hello top of hello blade.</span></span> <span data-ttu-id="621c6-122">Pronto!</span><span class="sxs-lookup"><span data-stu-id="621c6-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="621c6-123">Desabilitar a verificação de email no processo de inscrição Olá pode levar toospam.</span><span class="sxs-lookup"><span data-stu-id="621c6-123">Disabling email verification in hello sign-up process may lead toospam.</span></span> <span data-ttu-id="621c6-124">Se você desabilitar o saudação padrão, é recomendável adicionar seu próprio sistema de verificação.</span><span class="sxs-lookup"><span data-stu-id="621c6-124">If you disable hello default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="621c6-125">Estamos sempre abrir toofeedback e sugestões!</span><span class="sxs-lookup"><span data-stu-id="621c6-125">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="621c6-126">Se você tiver dificuldade com este tópico ou ter recomendações para melhorar este conteúdo, Apreciamos seus comentários na parte inferior da saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="621c6-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="621c6-127">Para solicitações de recurso, adicioná-los muito[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="621c6-127">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
