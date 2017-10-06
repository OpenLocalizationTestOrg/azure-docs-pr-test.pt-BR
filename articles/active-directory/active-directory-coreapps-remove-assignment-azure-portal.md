---
title: "aaaRemove uma atribuição de usuário ou grupo de um aplicativo de empresa no Active Directory do Azure | Microsoft Docs"
description: "Como tooremove Olá acessar atribuição de um usuário ou grupo de um aplicativo de empresa no Active Directory do Azure"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="265e9-103">Remover a atribuição de um usuário ou grupo de um aplicativo empresarial no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="265e9-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="265e9-104">É fácil tooremove um usuário ou um grupo sejam atribuídos acesso tooone de seus aplicativos de empresa no Active Directory do Azure (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="265e9-104">It's easy tooremove a user or a group from being assigned access tooone of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="265e9-105">Você deve ter Olá permissões apropriadas toomanage Olá enterprise aplicativo e deve ser o administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="265e9-105">You must have hello appropriate permissions toomanage hello enterprise app, and you must be global admin for hello directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="265e9-106">Como removo a atribuição de um usuário ou grupo?</span><span class="sxs-lookup"><span data-stu-id="265e9-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="265e9-107">Entrar toohello [portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global para o diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="265e9-107">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="265e9-108">Selecione **mais serviços**, digite **Active Directory do Azure** Olá caixa de texto e, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="265e9-108">Select **More services**, enter **Azure Active Directory** in hello text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="265e9-109">Em Olá **do Active Directory do Azure - *directoryname***  folha (ou seja, Olá AD do Azure folha para diretório de saudação que você está gerenciando), selecione **aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="265e9-109">On hello **Azure Active Directory - *directoryname*** blade (that is, hello Azure AD blade for hello directory you are managing), select **Enterprise applications**.</span></span>

    ![Abrir aplicativos empresariais](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="265e9-111">Em Olá **aplicativos empresariais** folha, selecione **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="265e9-111">On hello **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="265e9-112">Você verá uma lista de aplicativos de saudação, que você pode gerenciar.</span><span class="sxs-lookup"><span data-stu-id="265e9-112">You'll see a list of hello apps you can manage.</span></span>
5. <span data-ttu-id="265e9-113">Em Olá **aplicativos corporativos - todos os aplicativos** folha, selecione um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="265e9-113">On hello **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="265e9-114">Em Olá ***appname*** folha (ou seja, Olá folha com nome Olá Olá o aplicativo selecionado no título de saudação), selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="265e9-114">On hello ***appname*** blade (that is, hello blade with hello name of hello selected app in hello title), select **Users & Groups**.</span></span>

    ![Seleção de usuários ou de grupos](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="265e9-116">Em Olá ***appname*** **-atribuição de grupo de & usuário** folha, selecione uma das mais usuários ou grupos e, em seguida, selecione Olá **remover** comando.</span><span class="sxs-lookup"><span data-stu-id="265e9-116">On hello ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select hello **Remove** command.</span></span> <span data-ttu-id="265e9-117">Confirme sua decisão no prompt de saudação.</span><span class="sxs-lookup"><span data-stu-id="265e9-117">Confirm your decision at hello prompt.</span></span>

    ![Selecionando o comando de Remove Olá](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="265e9-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="265e9-119">Next steps</span></span>
* [<span data-ttu-id="265e9-120">Ver todos os meus grupos</span><span class="sxs-lookup"><span data-stu-id="265e9-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="265e9-121">Atribuir um aplicativo de enterprise tooan usuário ou grupo</span><span class="sxs-lookup"><span data-stu-id="265e9-121">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="265e9-122">Desabilitar as entradas de usuário em um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="265e9-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="265e9-123">Alterar nome de saudação ou logotipo de um aplicativo corporativo</span><span class="sxs-lookup"><span data-stu-id="265e9-123">Change hello name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
