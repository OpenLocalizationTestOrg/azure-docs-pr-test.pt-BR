---
title: "Atribuir licenças para o Azure MFA | Microsoft Docs"
description: "Saiba como atribuir as licenças do usuário para a Microsoft Azure Multi-Factor Authentication"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 514ef423-8ee6-4987-8a4e-80d5dc394cf9
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ROBOTS: NOINDEX
ms.openlocfilehash: 45522bf526c4aeab1d6ccc8891a55a0436ff9320
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="assigning-an-azure-mfa-azure-ad-premium-or-enterprise-mobility-license-to-users"></a><span data-ttu-id="27357-103">Atribuindo uma licença do Azure MFA, do Azure AD Premium ou do Enterprise Mobility aos usuários</span><span class="sxs-lookup"><span data-stu-id="27357-103">Assigning an Azure MFA, Azure AD Premium, or Enterprise Mobility license to users</span></span>
<span data-ttu-id="27357-104">Se você tiver comprado licenças do Azure MFA, do Azure AD Premium ou do Enterprise Mobility Suite, não precisará criar um provedor Multi-Factor Auth.</span><span class="sxs-lookup"><span data-stu-id="27357-104">If you have purchased Azure MFA, Azure AD Premium, or Enterprise Mobility Suite licenses, you do not need to create a Multi-Factor Auth provider.</span></span> <span data-ttu-id="27357-105">Depois de atribuir as licenças para seus usuários, você poderá começar a ativá-los para a MFA.</span><span class="sxs-lookup"><span data-stu-id="27357-105">Once you assign the licenses to your users, you can begin enabling them for MFA.</span></span>

## <a name="to-assign-a-license"></a><span data-ttu-id="27357-106">Para atribuir uma licença</span><span class="sxs-lookup"><span data-stu-id="27357-106">To assign a license</span></span>
1. <span data-ttu-id="27357-107">Entre no [portal clássico do Azure](https://manage.windowsazure.com) como um administrador.</span><span class="sxs-lookup"><span data-stu-id="27357-107">Sign in to the [Azure classic portal](https://manage.windowsazure.com) as an administrator.</span></span>
2. <span data-ttu-id="27357-108">Selecione **Active Directory**à esquerda.</span><span class="sxs-lookup"><span data-stu-id="27357-108">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="27357-109">Na página do Active Directory, clique duas vezes no diretório que tenha os usuários que você deseja habilitar.</span><span class="sxs-lookup"><span data-stu-id="27357-109">On the Active Directory page, double-click the directory that has the users you wish to enable.</span></span>
4. <span data-ttu-id="27357-110">Na parte superior da página do diretório, selecione **Licenças**.</span><span class="sxs-lookup"><span data-stu-id="27357-110">At the top of the directory page, select **Licenses**.</span></span>
   <span data-ttu-id="27357-111">![Atribuir licenças](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span><span class="sxs-lookup"><span data-stu-id="27357-111">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)</span></span>
5. <span data-ttu-id="27357-112">Na página de licenças, selecione **Autenticação Multifator do Azure**, **Active Directory Premium** ou **Enterprise Mobility Suite**.</span><span class="sxs-lookup"><span data-stu-id="27357-112">On the Licenses page, select **Azure Multi-Factor Authentication**, **Active Directory Premium**, or **Enterprise Mobility Suite**.</span></span>  <span data-ttu-id="27357-113">Se você tiver apenas uma, então, ela deverá ser selecionada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="27357-113">If you only have one, then it should be selected automatically.</span></span>
6. <span data-ttu-id="27357-114">Na parte inferior da página, clique em **Atribuir**.</span><span class="sxs-lookup"><span data-stu-id="27357-114">At the bottom of the page, click **Assign**.</span></span>
   <span data-ttu-id="27357-115">![Atribuir licenças](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span><span class="sxs-lookup"><span data-stu-id="27357-115">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)</span></span>
7. <span data-ttu-id="27357-116">Na caixa que aparece, clique ao lado dos usuários ou grupos aos quais você deseja atribuir licenças.</span><span class="sxs-lookup"><span data-stu-id="27357-116">In the box that comes up, click next to the users or groups you want to assign licenses to.</span></span>  <span data-ttu-id="27357-117">Você deverá ver uma marca de seleção verde aparecer.</span><span class="sxs-lookup"><span data-stu-id="27357-117">You should see a green check mark appear.</span></span>
8. <span data-ttu-id="27357-118">Clique no ícone da marca de seleção para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="27357-118">Click the check mark icon to save the changes.</span></span>
   <span data-ttu-id="27357-119">![Atribuir licenças](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span><span class="sxs-lookup"><span data-stu-id="27357-119">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)</span></span>
9. <span data-ttu-id="27357-120">Você deverá ver uma mensagem informando quantas licenças foram atribuídas e quantas podem ter falhado.</span><span class="sxs-lookup"><span data-stu-id="27357-120">You should see a message saying how many licenses were assigned and how many may have failed.</span></span>  <span data-ttu-id="27357-121">Clique em **Ok**.</span><span class="sxs-lookup"><span data-stu-id="27357-121">Click **Ok**.</span></span>
   <span data-ttu-id="27357-122">![Atribuir licenças](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span><span class="sxs-lookup"><span data-stu-id="27357-122">![Assign Licenses](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="27357-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="27357-123">Next steps</span></span>

- <span data-ttu-id="27357-124">Para saber mais, veja [O que é o licenciamento do Microsoft Azure Active Directory?](../active-directory/active-directory-licensing-what-is.md)</span><span class="sxs-lookup"><span data-stu-id="27357-124">For more information, see [What is Microsoft Azure Active Directory licensing?](../active-directory/active-directory-licensing-what-is.md)</span></span>
