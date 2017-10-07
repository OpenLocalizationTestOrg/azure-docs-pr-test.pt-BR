---
title: "aaaAzure notificações de relatório do Active Directory"
description: "Como toouse Olá notificações de relatório do Active Directory do Azure para logon suspeitos ins."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="f65d2-103">Notificações de Relatórios do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="f65d2-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="f65d2-104">Quais relatórios geram notificações por email</span><span class="sxs-lookup"><span data-stu-id="f65d2-104">What reports generate email notifications</span></span>
<span data-ttu-id="f65d2-105">Neste momento, as notificações por email somente Olá entradas irregulares em gatilhos de relatório de atividade.</span><span class="sxs-lookup"><span data-stu-id="f65d2-105">At this time, only hello Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="f65d2-106">O que é uma "Entrada irregular"?</span><span class="sxs-lookup"><span data-stu-id="f65d2-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="f65d2-107">Entradas irregulares são aquelas que foram identificados pelos nossos algoritmos com base Olá uma condição "viagem impossível" combinada com um local de entrada anormal e o dispositivo de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="f65d2-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on hello basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="f65d2-108">Isso pode indicar que um hacker tem tentado toosign usando essa conta.</span><span class="sxs-lookup"><span data-stu-id="f65d2-108">This may indicate that a hacker has been trying toosign in using this account.</span></span>

## <a name="who-receives-hello-email-notifications"></a><span data-ttu-id="f65d2-109">Quem recebe notificações de email Olá?</span><span class="sxs-lookup"><span data-stu-id="f65d2-109">Who receives hello email notifications?</span></span>
<span data-ttu-id="f65d2-110">email de saudação é enviado tooall administradores globais que tem sido atribuídos uma licença do Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="f65d2-110">hello email is sent tooall global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="f65d2-111">tooensure é entregue, podemos enviar-toohello admins. do endereço de Email alternativo também.</span><span class="sxs-lookup"><span data-stu-id="f65d2-111">tooensure it is delivered, we send it toohello admins Alternate Email Address as well.</span></span> <span data-ttu-id="f65d2-112">Os administradores devem incluir aad-alerts-noreply@mail.windowsazure.com em suas listas de remetentes confiáveis para que eles não perderem o email de saudação.</span><span class="sxs-lookup"><span data-stu-id="f65d2-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss hello email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="f65d2-113">Com que frequência esses emails são enviados?</span><span class="sxs-lookup"><span data-stu-id="f65d2-113">How often are these emails sent?</span></span>
<span data-ttu-id="f65d2-114">email de saudação é enviado se 10 novas irregulares entrar atividades ocorrem em Olá últimos 30 dias, ou desde o envio de email última hello, o que for menor.</span><span class="sxs-lookup"><span data-stu-id="f65d2-114">hello email is sent if 10 new irregular sign-in activities occur in hello last 30 days, or since hello last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a><span data-ttu-id="f65d2-115">Como acessar o relatório Olá mencionado no email Olá?</span><span class="sxs-lookup"><span data-stu-id="f65d2-115">How do I access hello report mentioned in hello email?</span></span>
<span data-ttu-id="f65d2-116">Quando você clica no link Olá, você será redirecionado toohello página de relatório em Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="f65d2-116">When you click on hello link, you will be redirected toohello report page within hello Azure classic portal.</span></span> <span data-ttu-id="f65d2-117">Em ordem tooaccess Olá relatório, é necessário toobe ambos:</span><span class="sxs-lookup"><span data-stu-id="f65d2-117">In order tooaccess hello report, you need toobe both:</span></span>

* <span data-ttu-id="f65d2-118">Um administrador ou coadministrador de sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="f65d2-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="f65d2-119">Um administrador global no diretório de saudação e atribuída uma licença do Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="f65d2-119">A global administrator in hello directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="f65d2-120">Para obter mais informações, consulte [Edições do Active Directory do Azure](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="f65d2-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="f65d2-121">Posso desativar esses emails?</span><span class="sxs-lookup"><span data-stu-id="f65d2-121">Can I turn off these emails?</span></span>
<span data-ttu-id="f65d2-122">Sim, tooturn desativar as notificações relacionadas tooanomalous entradas em Olá portal clássico do Azure, clique em **configurar**e, em seguida, selecione **desabilitado** em Olá **notificações**seção.</span><span class="sxs-lookup"><span data-stu-id="f65d2-122">Yes, tooturn off notifications related tooanomalous sign-ins within hello Azure classic portal, click **Configure**, and then select **Disabled** under hello **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="f65d2-123">O que vem a seguir</span><span class="sxs-lookup"><span data-stu-id="f65d2-123">What's next</span></span>
* <span data-ttu-id="f65d2-124">Curioso sobre que relatórios de segurança, auditoria e atividade estão disponíveis?</span><span class="sxs-lookup"><span data-stu-id="f65d2-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="f65d2-125">Verifique [Relatórios de segurança, auditoria e atividade do AD do Azure](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="f65d2-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="f65d2-126">Introdução ao Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="f65d2-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="f65d2-127">Adicionar identidade visual tooyour páginas entrar e painel de acesso da empresa</span><span class="sxs-lookup"><span data-stu-id="f65d2-127">Add company branding tooyour Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

