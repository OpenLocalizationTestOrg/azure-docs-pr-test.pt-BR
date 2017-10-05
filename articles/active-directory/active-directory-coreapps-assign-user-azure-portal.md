---
title: "Atribuir um usuário ou grupo a um aplicativo empresarial no Azure Active Directory | Microsoft Docs"
description: "Como selecionar um aplicativo empresarial par atribuir um usuário ou um grupo a ele no Azure Active Directory"
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
ms.openlocfilehash: ee784704ada9238b5cd048f99aaa4cb192ec7d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-a-user-or-group-to-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="f3d66-103">Atribuir um usuário ou um grupo a um aplicativo empresarial no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f3d66-103">Assign a user or group to an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="f3d66-104">É fácil atribuir um usuário ou um grupo aos aplicativos empresariais no Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="f3d66-104">It's easy to assign a user or a group to your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f3d66-105">Você deve ter as permissões apropriadas para gerenciar o aplicativo empresarial, além de ser um administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="f3d66-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-assign-user-access-to-an-enterprise-app"></a><span data-ttu-id="f3d66-106">Como atribuir acesso de usuário a um aplicativo empresarial?</span><span class="sxs-lookup"><span data-stu-id="f3d66-106">How do I assign user access to an enterprise app?</span></span>
1. <span data-ttu-id="f3d66-107">Entre no [Portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="f3d66-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="f3d66-108">Selecione **Mais serviços**, insira Azure Active Directory na caixa de texto, em seguida, selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="f3d66-108">Select **More services**, enter Azure Active Directory in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="f3d66-109">Na folha **Azure Active Directory – *nomedodiretório*** (ou seja, a folha do Azure AD para o diretório que você está gerenciando), escolha **Aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="f3d66-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Abrir aplicativos empresariais](./media/active-directory-coreapps-assign-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="f3d66-111">Na folha **Aplicativos empresariais**, escolha **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="f3d66-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="f3d66-112">Você verá uma lista dos aplicativos que pode gerenciar.</span><span class="sxs-lookup"><span data-stu-id="f3d66-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="f3d66-113">Na folha **Aplicativos empresariais – Todos os aplicativos** , escolha um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f3d66-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="f3d66-114">Na folha ***appname*** (ou seja, a folha com o nome do aplicativo selecionado no título), selecione **Usuários e Grupos**.</span><span class="sxs-lookup"><span data-stu-id="f3d66-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Seleção do comando todos os aplicativos](./media/active-directory-coreapps-assign-user-azure-portal/select-app-users.png)
7. <span data-ttu-id="f3d66-116">Na folha ***appname*** **- Usuário e Atribuição de Grupos**, selecione o comando **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f3d66-116">On the ***appname*** **- User & Group Assignment** blade, select the **Add** command.</span></span>
8. <span data-ttu-id="f3d66-117">Na folha **Adicionar Atribuição**, selecione **Usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="f3d66-117">On the **Add Assignment** blade, select **Users and groups**.</span></span>

    ![Atribuir um usuário ou um grupo ao aplicativo](./media/active-directory-coreapps-assign-user-azure-portal/assign-users.png)
9. <span data-ttu-id="f3d66-119">Na folha **Usuários e grupos**, selecione um ou mais usuários ou grupos na lista, em seguida, pressione o botão **Selecionar** na parte inferior da folha.</span><span class="sxs-lookup"><span data-stu-id="f3d66-119">On the **Users and groups** blade, select one or more users or groups from the list and then select the **Select** button at the bottom of the blade.</span></span>
10. <span data-ttu-id="f3d66-120">Na folha **Adicionar Atribuição**, selecione **Função**.</span><span class="sxs-lookup"><span data-stu-id="f3d66-120">On the **Add Assignment** blade, select **Role**.</span></span> <span data-ttu-id="f3d66-121">Então, na folha **Selecionar Função**, escolha uma função para aplicar nos usuários ou grupos selecionados, em seguida, selecione o botão **OK** na parte inferior da folha.</span><span class="sxs-lookup"><span data-stu-id="f3d66-121">Then, on the **Select Role** blade, select a role to apply to the selected users or groups, and then select the **OK** button at the bottom of the blade.</span></span>
11. <span data-ttu-id="f3d66-122">Na folha **Adicionar Atribuição**, selecione o botão **Atribuir** na parte inferior da folha.</span><span class="sxs-lookup"><span data-stu-id="f3d66-122">On the **Add Assignment** blade, select the **Assign** button at the bottom of the blade.</span></span> <span data-ttu-id="f3d66-123">Os usuários ou os grupos atribuídos terão as permissões definidas pela função selecionada para esse aplicativo empresarial.</span><span class="sxs-lookup"><span data-stu-id="f3d66-123">The assigned users or groups will have the permissions defined by the selected role for this enterprise app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3d66-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f3d66-124">Next steps</span></span>
* [<span data-ttu-id="f3d66-125">Ver todos os meus grupos</span><span class="sxs-lookup"><span data-stu-id="f3d66-125">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="f3d66-126">Remover uma atribuição de usuário ou de grupo de um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="f3d66-126">Remove a user or group assignment from an enterprise app</span></span>](active-directory-coreapps-remove-assignment-azure-portal.md)
* [<span data-ttu-id="f3d66-127">Desabilitar as entradas de usuário em um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="f3d66-127">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="f3d66-128">Alterar o nome ou logotipo de um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="f3d66-128">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
