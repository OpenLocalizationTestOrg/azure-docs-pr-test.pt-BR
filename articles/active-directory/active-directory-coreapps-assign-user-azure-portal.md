---
title: "aaaAssign um aplicativo de enterprise tooan usuário ou grupo no Active Directory do Azure | Microsoft Docs"
description: "Como tooselect um aplicativo de enterprise tooassign um tooit de usuário ou grupo no Active Directory do Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5817ad48-d916-492b-a8d0-2ade8c50a224
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 86c11f19892b9c947a5331677c17759178ed2806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-user-or-group-tooan-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="5bd36-103">Atribuir um aplicativo de enterprise tooan usuário ou grupo no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5bd36-103">Assign a user or group tooan enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="5bd36-104">É fácil tooassign um usuário ou um aplicativo do grupo tooyour enterprise no Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="5bd36-104">It's easy tooassign a user or a group tooyour enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="5bd36-105">Você deve ter Olá permissões apropriadas toomanage Olá enterprise aplicativo e deve ser o administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bd36-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-assign-user-access-tooan-enterprise-app"></a><span data-ttu-id="5bd36-106">Como atribuir acesso de usuário tooan enterprise aplicativo?</span><span class="sxs-lookup"><span data-stu-id="5bd36-106">How do I assign user access tooan enterprise app?</span></span>
1. <span data-ttu-id="5bd36-107">Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bd36-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="5bd36-108">Selecione **mais serviços**, insira o Active Directory do Azure na caixa de texto de saudação e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="5bd36-108">Select **More services**, enter Azure Active Directory in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="5bd36-109">Em Olá **do Active Directory do Azure - *directoryname***  folha (ou seja, Olá AD do Azure folha para diretório de saudação que você está gerenciando), selecione **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5bd36-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Abrir aplicativos empresariais](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="5bd36-111">Em Olá **aplicativos empresariais** folha, selecione **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5bd36-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="5bd36-112">Você verá uma lista de aplicativos de saudação, que você pode gerenciar.</span><span class="sxs-lookup"><span data-stu-id="5bd36-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="5bd36-113">Em Olá **aplicativos corporativos - todos os aplicativos** folha, selecione um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5bd36-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="5bd36-114">Em Olá ***appname*** folha (ou seja, Olá folha com nome Olá Olá o aplicativo selecionado no título de saudação), selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5bd36-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![Selecionando Olá comando de todos os aplicativos](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="5bd36-116">Em Olá ***appname*** **-atribuição de grupo de & usuário** folha, selecione Olá **adicionar** comando.</span><span class="sxs-lookup"><span data-stu-id="5bd36-116">On hello ***appname*** **- User & Group Assignment** blade, select hello **Add** command.</span></span>
8. <span data-ttu-id="5bd36-117">Em Olá **Adicionar atribuição** folha, selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5bd36-117">On hello **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Atribuir um aplicativo de usuário ou grupo toohello](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="5bd36-119">Em Olá **usuários e grupos** folha, selecione um ou mais usuários ou grupos de saudação e, em seguida, selecione Olá **selecione** botão na parte inferior da saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bd36-119">On hello **Users and groups** blade, select one or more users or groups from hello list and then select hello **Select** button at hello bottom of hello blade.</span></span>
10. <span data-ttu-id="5bd36-120">Em Olá **Adicionar atribuição** folha, selecione **função**.</span><span class="sxs-lookup"><span data-stu-id="5bd36-120">On hello **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="5bd36-121">Em seguida, na Olá **Selecionar função** folha, selecione um toohello de tooapply função usuários ou grupos selecionados e, em seguida, selecione Olá **Okey** botão na parte inferior da saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bd36-121">Then, on hello **Select Role** blade, select a role tooapply toohello selected users or groups, and then select hello **OK** button at hello bottom of hello blade.</span></span>
11. <span data-ttu-id="5bd36-122">Em Olá **Adicionar atribuição** folha, selecione Olá **atribuir** botão na parte inferior da saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="5bd36-122">On hello **Add Assignment** blade, select hello **Assign** button at hello bottom of hello blade.</span></span> <span data-ttu-id="5bd36-123">Olá atribuída a usuários ou grupos terão permissões de saudação definidas pela função selecionada de saudação para esse aplicativo corporativo.</span><span class="sxs-lookup"><span data-stu-id="5bd36-123">hello assigned users or groups will have hello permissions defined by hello selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bd36-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5bd36-124">Next steps</span></span>
* [<span data-ttu-id="5bd36-125">Ver todos os meus grupos</span><span class="sxs-lookup"><span data-stu-id="5bd36-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="5bd36-126">Remover uma atribuição de usuário ou de grupo de um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="5bd36-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="5bd36-127">Desabilitar as entradas de usuário em um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="5bd36-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="5bd36-128">Alterar nome de saudação ou logotipo de um aplicativo corporativo</span><span class="sxs-lookup"><span data-stu-id="5bd36-128">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
