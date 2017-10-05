---
title: "Como executar uma revisão de acesso | Microsoft Docs"
description: "Saiba como executar uma revisão com o aplicativo Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: a98ed60221eeba1d9c92df846aeae2deafb8ae60
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-perform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="32ac6-103">Como executar uma análise de acesso no Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="32ac6-103">How to perform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="32ac6-104">O Azure Active Directory (AD) Privileged Identity Management simplifica a forma como as empresas gerenciam o acesso privilegiado a recursos no Azure AD e em outros Microsoft Online Services, como o Office 365 ou o Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="32ac6-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="32ac6-105">Se você for atribuído a uma função administrativa, o administrador de função com privilégios de sua organização poderá solicitar que você confirme regularmente que ainda precisa da função para seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="32ac6-105">If you are assigned to an administrative role, your organization's privileged role administrator may ask you to regularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="32ac6-106">Você pode receber um email que inclui um link ou pode acessar diretamente o [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="32ac6-106">You might get an email that includes a link, or you can go straight to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="32ac6-107">Siga as etapas neste artigo para executar a autorrevisão das suas funções atribuídas.</span><span class="sxs-lookup"><span data-stu-id="32ac6-107">Follow the steps in this article to perform a self-review of your assigned roles.</span></span>

<span data-ttu-id="32ac6-108">Se você for um administrador com privilégios de função interessado em revisões de acesso, obtenha mais detalhes em [Como iniciar uma revisão de acesso](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="32ac6-108">If you're a privileged role administrator interested in access reviews, get more details at [How to start an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="32ac6-109">Adicionar o aplicativo Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="32ac6-109">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="32ac6-110">Você pode usar o aplicativo Azure AD PIM (Privileged Identity Management) no [portal do Azure](https://portal.azure.com/) para executar a revisão.</span><span class="sxs-lookup"><span data-stu-id="32ac6-110">You can use the Azure AD Privileged Identity Management (PIM) application in the [Azure portal](https://portal.azure.com/) to perform your review.</span></span>  <span data-ttu-id="32ac6-111">Se você não tiver o aplicativo Azure AD Privileged Identity Management em seu portal, siga estas etapas para começar.</span><span class="sxs-lookup"><span data-stu-id="32ac6-111">If you don't have the Azure AD Privileged Identity Management application on your portal, follow these steps to get started.</span></span>

1. <span data-ttu-id="32ac6-112">Entre no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="32ac6-112">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="32ac6-113">Selecione seu nome de usuário no canto superior direito do portal do Azure e selecione o diretório em que você vai operar.</span><span class="sxs-lookup"><span data-stu-id="32ac6-113">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span></span>
3. <span data-ttu-id="32ac6-114">Selecione **Mais serviços** e use a caixa de texto Filtrar para procurar **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="32ac6-114">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="32ac6-115">Marque **Fixar no painel** e então clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="32ac6-115">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="32ac6-116">O aplicativo Privileged Identity Management será aberto.</span><span class="sxs-lookup"><span data-stu-id="32ac6-116">The Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="32ac6-117">Aprovar ou negar acesso</span><span class="sxs-lookup"><span data-stu-id="32ac6-117">Approve or deny access</span></span>
<span data-ttu-id="32ac6-118">Ao aprovar ou negar o acesso, você está apenas dizendo ao revisor se ainda usa essa função ou não.</span><span class="sxs-lookup"><span data-stu-id="32ac6-118">When you approve or deny access, you're just telling the reviewer whether you still use this role or not.</span></span> <span data-ttu-id="32ac6-119">Escolha **Aprovar** se você quiser manter a função ou **Negar** se não precisar mais do acesso.</span><span class="sxs-lookup"><span data-stu-id="32ac6-119">Choose **Approve** if you want to stay in the role, or **Deny** if you don't need the access anymore.</span></span> <span data-ttu-id="32ac6-120">Seu status não mudará imediatamente até que o revisor aplique os resultados.</span><span class="sxs-lookup"><span data-stu-id="32ac6-120">Your status won't change right away, until the reviewer applies the results.</span></span>
<span data-ttu-id="32ac6-121">Siga estas etapas para localizar e concluir a análise de acesso:</span><span class="sxs-lookup"><span data-stu-id="32ac6-121">Follow these steps to find and complete the access review:</span></span>

1. <span data-ttu-id="32ac6-122">No aplicativo PIM, selecione **Examinar o acesso com privilégios**.</span><span class="sxs-lookup"><span data-stu-id="32ac6-122">In the PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="32ac6-123">Se você tiver quaisquer análises de acesso pendentes, elas aparecerão na folha de análises do Acesso do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32ac6-123">If you have any pending access reviews, they appear in the Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="32ac6-124">Selecione a análise que deseja concluir.</span><span class="sxs-lookup"><span data-stu-id="32ac6-124">Select the review you want to complete.</span></span>
3. <span data-ttu-id="32ac6-125">A menos que tenha criado a análise, você aparece como o único usuário na análise.</span><span class="sxs-lookup"><span data-stu-id="32ac6-125">Unless you created the review, you appear as the only user in the review.</span></span> <span data-ttu-id="32ac6-126">Selecione a marca de seleção ao lado de seu nome.</span><span class="sxs-lookup"><span data-stu-id="32ac6-126">Select the check mark next to your name.</span></span>
4. <span data-ttu-id="32ac6-127">Escolha **Aprovar** ou **Negar**.</span><span class="sxs-lookup"><span data-stu-id="32ac6-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="32ac6-128">Talvez seja necessário incluir um motivo para a sua decisão na caixa de texto **Fornecer um motivo** .</span><span class="sxs-lookup"><span data-stu-id="32ac6-128">You may need to include a reason for your decision in the **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="32ac6-129">Feche a folha **Funções de análise do AD do Azure** .</span><span class="sxs-lookup"><span data-stu-id="32ac6-129">Close the **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="32ac6-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="32ac6-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
