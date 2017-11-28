---
title: "aaaHow tooperform uma revisão de acesso | Microsoft Docs"
description: "Saiba como tooperform uma revisão com hello aplicativo Privileged Identity Management do Azure."
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
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="9dcf3-103">Como tooperform um acesso examinar no Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="9dcf3-103">How tooperform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="9dcf3-104">Active Directory (AD) Privileged Identity Management do Azure simplifica como as empresas gerenciam o acesso privilegiado tooresources no AD do Azure e outros Microsoft online services como Office 365 ou Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access tooresources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="9dcf3-105">Se você receber a função administrativa tooan, com privilégios de função administrador de sua organização pode solicitar que você tooregularly confirmar que você ainda precisa essa função para seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-105">If you are assigned tooan administrative role, your organization's privileged role administrator may ask you tooregularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="9dcf3-106">Você poderá receber um email que inclui um link ou vá reta toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9dcf3-106">You might get an email that includes a link, or you can go straight toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9dcf3-107">Siga as etapas de saudação este tooperform artigo automaticamente examine atribuídas funções de.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-107">Follow hello steps in this article tooperform a self-review of your assigned roles.</span></span>

<span data-ttu-id="9dcf3-108">Se você for um administrador com privilégios de função interessado em análises de acesso, obtenha mais detalhes em [como toostart um acesso examine](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="9dcf3-108">If you're a privileged role administrator interested in access reviews, get more details at [How toostart an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-hello-privileged-identity-management-application"></a><span data-ttu-id="9dcf3-109">Adicionar aplicativo do hello Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="9dcf3-109">Add hello Privileged Identity Management application</span></span>
<span data-ttu-id="9dcf3-110">Você pode usar o aplicativo de gerenciamento de identidade com privilégios (PIM) de saudação do AD do Azure no hello [portal do Azure](https://portal.azure.com/) tooperform sua análise.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-110">You can use hello Azure AD Privileged Identity Management (PIM) application in hello [Azure portal](https://portal.azure.com/) tooperform your review.</span></span>  <span data-ttu-id="9dcf3-111">Se você não tiver o aplicativo do Azure AD Privileged Identity Management hello em seu portal, siga essas tooget etapas iniciado.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-111">If you don't have hello Azure AD Privileged Identity Management application on your portal, follow these steps tooget started.</span></span>

1. <span data-ttu-id="9dcf3-112">Entrar toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9dcf3-112">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="9dcf3-113">Selecione seu nome de usuário no canto superior direito de saudação do hello portal do Azure e diretório hello selecione onde você irá operar.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-113">Select your username in hello upper right-hand corner of hello Azure portal, and select hello directory where you will you be operating.</span></span>
3. <span data-ttu-id="9dcf3-114">Selecione **mais serviços** e usar Olá toosearch de caixa de texto de filtro para **do Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-114">Select **More services** and use hello Filter textbox toosearch for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="9dcf3-115">Verificar **Pin toodashboard** e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-115">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="9dcf3-116">Olá aplicativo Privileged Identity Management será aberto.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-116">hello Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="9dcf3-117">Aprovar ou negar acesso</span><span class="sxs-lookup"><span data-stu-id="9dcf3-117">Approve or deny access</span></span>
<span data-ttu-id="9dcf3-118">Quando você aprova ou nega o acesso, você está apenas dizendo revisor Olá se você usar essa função ou não.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-118">When you approve or deny access, you're just telling hello reviewer whether you still use this role or not.</span></span> <span data-ttu-id="9dcf3-119">Escolha **aprovar** se você quiser toostay na função hello, ou **Deny** se você não precisa Olá a acesso mais.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-119">Choose **Approve** if you want toostay in hello role, or **Deny** if you don't need hello access anymore.</span></span> <span data-ttu-id="9dcf3-120">Seu status não será alterado imediatamente, até que o revisor Olá aplica resultados hello.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-120">Your status won't change right away, until hello reviewer applies hello results.</span></span>
<span data-ttu-id="9dcf3-121">Siga essas etapas toofind e concluir a avaliação do acesso hello:</span><span class="sxs-lookup"><span data-stu-id="9dcf3-121">Follow these steps toofind and complete hello access review:</span></span>

1. <span data-ttu-id="9dcf3-122">No aplicativo PIM do hello, selecione **acesso privilegiado de revisão**.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-122">In hello PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="9dcf3-123">Se você tiver quaisquer revisões acesso pendente, eles aparecem no hello que acesso do AD do Azure analisa folha.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-123">If you have any pending access reviews, they appear in hello Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="9dcf3-124">Selecione a revisão Olá deseja toocomplete.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-124">Select hello review you want toocomplete.</span></span>
3. <span data-ttu-id="9dcf3-125">A menos que você criou revisão Olá, aparecem como Olá apenas usuário revisão hello.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-125">Unless you created hello review, you appear as hello only user in hello review.</span></span> <span data-ttu-id="9dcf3-126">Selecione nome do próximo tooyour Olá marca de seleção.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-126">Select hello check mark next tooyour name.</span></span>
4. <span data-ttu-id="9dcf3-127">Escolha **Aprovar** ou **Negar**.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="9dcf3-128">Talvez seja necessário um motivo para a sua decisão de saudação do tooinclude **fornecer um motivo** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-128">You may need tooinclude a reason for your decision in hello **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="9dcf3-129">Olá fechar **funções de análise do Azure AD** folha.</span><span class="sxs-lookup"><span data-stu-id="9dcf3-129">Close hello **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="9dcf3-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9dcf3-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
