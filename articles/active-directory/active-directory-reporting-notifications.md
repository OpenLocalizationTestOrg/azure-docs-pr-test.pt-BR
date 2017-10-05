---
title: "Notificações de Relatórios do Active Directory do Azure"
description: "Como usar as notificações de relatórios do Active Directory do Azure para entradas suspeitas."
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
ms.openlocfilehash: f4632bd2af802b10c8c64972e8c605d7ad7c0eaf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="8a223-103">Notificações de Relatórios do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="8a223-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="8a223-104">Quais relatórios geram notificações por email</span><span class="sxs-lookup"><span data-stu-id="8a223-104">What reports generate email notifications</span></span>
<span data-ttu-id="8a223-105">Neste momento, apenas o relatório de atividade de entrada irregular dispara as notificações por email.</span><span class="sxs-lookup"><span data-stu-id="8a223-105">At this time, only the Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="8a223-106">O que é uma "Entrada irregular"?</span><span class="sxs-lookup"><span data-stu-id="8a223-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="8a223-107">Entradas irregulares são aquelas que foram identificadas por nossos algoritmos de aprendizado de máquina, com base em uma condição de “viagem impossível” combinada a um dispositivo e um local de entrada anômalos.</span><span class="sxs-lookup"><span data-stu-id="8a223-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on the basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="8a223-108">Isso pode indicar que um hacker tentou entrar usando essa conta.</span><span class="sxs-lookup"><span data-stu-id="8a223-108">This may indicate that a hacker has been trying to sign in using this account.</span></span>

## <a name="who-receives-the-email-notifications"></a><span data-ttu-id="8a223-109">Quem recebe as notificações por email?</span><span class="sxs-lookup"><span data-stu-id="8a223-109">Who receives the email notifications?</span></span>
<span data-ttu-id="8a223-110">O email é enviado para todos os administradores globais as quais foi atribuída uma licença do Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="8a223-110">The email is sent to all global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="8a223-111">Para garantir que ele seja entregue, podemos enviá-lo também ao endereço de Email alternativo dos administradores.</span><span class="sxs-lookup"><span data-stu-id="8a223-111">To ensure it is delivered, we send it to the admins Alternate Email Address as well.</span></span> <span data-ttu-id="8a223-112">Os administradores devem incluir aad-alerts-noreply@mail.windowsazure.com em suas listas de remetentes seguros, para que eles não deixem de ver o email.</span><span class="sxs-lookup"><span data-stu-id="8a223-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss the email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="8a223-113">Com que frequência esses emails são enviados?</span><span class="sxs-lookup"><span data-stu-id="8a223-113">How often are these emails sent?</span></span>
<span data-ttu-id="8a223-114">O email será enviado se 10 novas atividades de entrada irregular ocorrerem nos últimos 30 dias, ou contando a partir da data em que o último email foi enviado, o período que for mais curto.</span><span class="sxs-lookup"><span data-stu-id="8a223-114">The email is sent if 10 new irregular sign-in activities occur in the last 30 days, or since the last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-the-report-mentioned-in-the-email"></a><span data-ttu-id="8a223-115">Como acessar o relatório mencionado no email?</span><span class="sxs-lookup"><span data-stu-id="8a223-115">How do I access the report mentioned in the email?</span></span>
<span data-ttu-id="8a223-116">Ao clicar no link, você será redirecionado à página do relatório no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="8a223-116">When you click on the link, you will be redirected to the report page within the Azure classic portal.</span></span> <span data-ttu-id="8a223-117">Para acessar o relatório, você precisa ser ambos:</span><span class="sxs-lookup"><span data-stu-id="8a223-117">In order to access the report, you need to be both:</span></span>

* <span data-ttu-id="8a223-118">Um administrador ou coadministrador de sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="8a223-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="8a223-119">Um administrador global no diretório e ter uma licença do Active Directory Premium atribuída a você.</span><span class="sxs-lookup"><span data-stu-id="8a223-119">A global administrator in the directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="8a223-120">Para obter mais informações, consulte [Edições do Active Directory do Azure](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="8a223-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="8a223-121">Posso desativar esses emails?</span><span class="sxs-lookup"><span data-stu-id="8a223-121">Can I turn off these emails?</span></span>
<span data-ttu-id="8a223-122">Sim. Para desligar as notificações relacionadas a entradas anômalas no Portal clássico do Azure, clique em **Configurar** e selecione **Desabilitado** na seção **Notificações**.</span><span class="sxs-lookup"><span data-stu-id="8a223-122">Yes, to turn off notifications related to anomalous sign-ins within the Azure classic portal, click **Configure**, and then select **Disabled** under the **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="8a223-123">O que vem a seguir</span><span class="sxs-lookup"><span data-stu-id="8a223-123">What's next</span></span>
* <span data-ttu-id="8a223-124">Curioso sobre que relatórios de segurança, auditoria e atividade estão disponíveis?</span><span class="sxs-lookup"><span data-stu-id="8a223-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="8a223-125">Verifique [Relatórios de segurança, auditoria e atividade do AD do Azure](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="8a223-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="8a223-126">Introdução ao Azure Active Directory Premium</span><span class="sxs-lookup"><span data-stu-id="8a223-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="8a223-127">Adicionar identidade visual da empresa às páginas de Entrada e do Painel de acesso</span><span class="sxs-lookup"><span data-stu-id="8a223-127">Add company branding to your Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

