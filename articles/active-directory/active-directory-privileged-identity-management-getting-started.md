---
title: "Introdução ao Azure AD Privileged Identity Management | Microsoft Docs"
description: Saiba como gerenciar identidades privilegiadas com o aplicativo Azure Active Directory Privileged Identity Management no portal do Azure.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2299db7d-bee7-40d0-b3c6-8d628ac61071
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/27/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: 17cdff033cc3dbb199d11c3b8ac1acbc92499877
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="start-using-azure-ad-privileged-identity-management"></a><span data-ttu-id="e2123-103">Começar a usar o Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="e2123-103">Start using Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="e2123-104">Com o Privileged Identity Management do Azure Active Directory (AD), você pode gerenciar, controlar e monitorar o acesso em sua organização.</span><span class="sxs-lookup"><span data-stu-id="e2123-104">With Azure Active Directory (AD) Privileged Identity Management, you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="e2123-105">Esse escopo inclui o acesso a recursos no Azure AD e outros serviços online da Microsoft, como o Office 365 ou o Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="e2123-105">This scope includes access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="e2123-106">Este artigo lhe mostra como adicionar o aplicativo do Azure AD PIM o painel do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2123-106">This article tells you how to add the Azure AD PIM app to your Azure portal dashboard.</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="e2123-107">Adicionar o aplicativo Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="e2123-107">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="e2123-108">Antes de usar o Azure AD Privileged Identity Management, você precisa adicionar o aplicativo ao painel do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2123-108">Before you use Azure AD Privileged Identity Management, you need to add the application to your Azure portal dashboard.</span></span>

1. <span data-ttu-id="e2123-109">Entre no [portal do Azure](https://portal.azure.com/) como um administrador global do seu diretório.</span><span class="sxs-lookup"><span data-stu-id="e2123-109">Sign in to the [Azure portal](https://portal.azure.com/) as a global administrator of your directory.</span></span>
2. <span data-ttu-id="e2123-110">Se sua organização tiver mais de um diretório, selecione seu nome de usuário no canto superior direito do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2123-110">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span></span> <span data-ttu-id="e2123-111">Selecione o diretório onde você deseja usar o PIM.</span><span class="sxs-lookup"><span data-stu-id="e2123-111">Select the directory where you want to use PIM.</span></span>
3. <span data-ttu-id="e2123-112">Selecione **Mais serviços** e use a caixa de texto Filtrar para procurar **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="e2123-112">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="e2123-113">Marque **Fixar no painel** e então clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e2123-113">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="e2123-114">O aplicativo Privileged Identity Management é aberto.</span><span class="sxs-lookup"><span data-stu-id="e2123-114">The Privileged Identity Management application opens.</span></span>

<span data-ttu-id="e2123-115">Se você for a primeira pessoa a usar o Azure AD Privileged Identity Management em seu diretório, receberá automaticamente as funções **Administrador de segurança** e **Administrador com privilégios de função** no diretório.</span><span class="sxs-lookup"><span data-stu-id="e2123-115">If you're the first person to use Azure AD Privileged Identity Management in your directory, you are automatically assigned the **Security administrator** and **Privileged role administrator** roles in the directory.</span></span> <span data-ttu-id="e2123-116">Somente os administradores com privilégios de função podem gerenciar atribuições de função de usuários.</span><span class="sxs-lookup"><span data-stu-id="e2123-116">Only privileged role administrators can manage role assignments of users.</span></span> <span data-ttu-id="e2123-117">Além disso, você pode optar por executar o [assistente de segurança.](active-directory-privileged-identity-management-security-wizard.md)</span><span class="sxs-lookup"><span data-stu-id="e2123-117">In addition, you may choose to run the [security wizard.](active-directory-privileged-identity-management-security-wizard.md)</span></span> <span data-ttu-id="e2123-118">que orienta você durante a experiência inicial de detecção e atribuição.</span><span class="sxs-lookup"><span data-stu-id="e2123-118">that walks you through the initial discovery and assignment experience.</span></span>

## <a name="navigate-to-your-tasks"></a><span data-ttu-id="e2123-119">Navegue até as tarefas</span><span class="sxs-lookup"><span data-stu-id="e2123-119">Navigate to your tasks</span></span>
<span data-ttu-id="e2123-120">Depois que o Azure AD Privileged Identity Management estiver configurado, você verá a folha de navegação sempre que abrir o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e2123-120">Once Azure AD Privileged Identity Management is set up, you see the navigation blade whenever you open the application.</span></span> <span data-ttu-id="e2123-121">Use essa folha para realizar suas tarefas de gerenciamento de identidade.</span><span class="sxs-lookup"><span data-stu-id="e2123-121">Use this blade to accomplish your identity management tasks.</span></span>

![Tarefas de nível superior para o PIM - captura de tela](./media/active-directory-privileged-identity-management-getting-started/PIM_Tasks_New.png)

* <span data-ttu-id="e2123-123">**Minhas Funções** leva à lista de funções atribuídas a você.</span><span class="sxs-lookup"><span data-stu-id="e2123-123">**My Roles** takes you to a list of roles that are assigned to you.</span></span> <span data-ttu-id="e2123-124">Essa seção é onde você ativará as funções para as quais está qualificado.</span><span class="sxs-lookup"><span data-stu-id="e2123-124">This section is where you activate any roles that you are eligible for.</span></span>
* <span data-ttu-id="e2123-125">**Aprovar Solicitações (Versão prévia)** exibe uma lista de solicitações de ativação de usuários pendentes no seu diretório.</span><span class="sxs-lookup"><span data-stu-id="e2123-125">**Approve Requests (Preview)** displays a list of pending activation requests from users in your directory.</span></span> [<span data-ttu-id="e2123-126">Saiba mais.</span><span class="sxs-lookup"><span data-stu-id="e2123-126">Learn more.</span></span>](./privileged-identity-management/azure-ad-pim-approval-workflow.md)
* <span data-ttu-id="e2123-127">**Solicitações Pendentes (Versão prévia)** exibe todas as solicitações atuais feitas a serem ativadas.</span><span class="sxs-lookup"><span data-stu-id="e2123-127">**Pending Requests (Preview)** displays any current requests to have made to activate.</span></span>
* <span data-ttu-id="e2123-128">**Examinar Acesso** leva você a qualquer revisão de acesso pendente que tenha de ser concluída, esteja você examinando o acesso para si mesmo ou para outra pessoa.</span><span class="sxs-lookup"><span data-stu-id="e2123-128">**Review Access** takes you to any pending access reviews that you need to complete, whether you're reviewing access for yourself or someone else.</span></span>
* <span data-ttu-id="e2123-129">As **Funções de Diretório do Azure AD** localizadas na seção ‘Gerenciar’ é o painel onde os administradores de função com privilégios gerenciam atribuições de função, alteram configurações de ativação de função, iniciam revisões de acesso e muito mais.</span><span class="sxs-lookup"><span data-stu-id="e2123-129">**Azure AD Directory Roles** located under the 'Manage' section is the dashboard for privileged role admins to manage role assignments, change role activation settings, start access reviews, and more.</span></span> <span data-ttu-id="e2123-130">As opções desse painel estão desabilitadas para todos que não forem administradores de função com privilégios.</span><span class="sxs-lookup"><span data-stu-id="e2123-130">The options in this dashboard are disabled for anyone who isn't a privileged role administrator.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2123-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2123-131">Next steps</span></span>
<span data-ttu-id="e2123-132">A [visão geral do Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md) inclui mais detalhes sobre como você pode gerenciar o acesso administrativo em sua organização.</span><span class="sxs-lookup"><span data-stu-id="e2123-132">The [Azure AD Privileged Identity Management overview](active-directory-privileged-identity-management-configure.md) includes more details on how you can manage administrative access in your organization.</span></span>

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
