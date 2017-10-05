---
title: "Remover uma atribuição de usuário ou grupo de um aplicativo empresarial no Azure Active Directory | Microsoft Docs"
description: "Como remover a atribuição de acesso de um usuário ou grupo de um aplicativo empresarial no Azure Active Directory"
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
ms.openlocfilehash: 02f122acfb53c2107e2b0af66c6195aa127a2c77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a><span data-ttu-id="12a76-103">Remover a atribuição de um usuário ou grupo de um aplicativo empresarial no Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12a76-103">Remove a user or group assignment from an enterprise app in Azure Active Directory</span></span>
<span data-ttu-id="12a76-104">É fácil impedir que um usuário ou grupo receba acesso a um de seus aplicativos empresariais no Azure AD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="12a76-104">It's easy to remove a user or a group from being assigned access to one of your enterprise applications in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="12a76-105">Você deve ter as permissões apropriadas para gerenciar o aplicativo empresarial, além de ser um administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="12a76-105">You must have the appropriate permissions to manage the enterprise app, and you must be global admin for the directory.</span></span>

## <a name="how-do-i-remove-a-user-or-group-assignment"></a><span data-ttu-id="12a76-106">Como removo a atribuição de um usuário ou grupo?</span><span class="sxs-lookup"><span data-stu-id="12a76-106">How do I remove a user or group assignment?</span></span>
1. <span data-ttu-id="12a76-107">Entre no [Portal do Azure](https://portal.azure.com) com uma conta que seja um administrador global do diretório.</span><span class="sxs-lookup"><span data-stu-id="12a76-107">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="12a76-108">Escolha **Mais serviços**, insira **Azure Active Directory** na caixa de texto e selecione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="12a76-108">Select **More services**, enter **Azure Active Directory** in the text box, and then select **Enter**.</span></span>
3. <span data-ttu-id="12a76-109">Na folha **Azure Active Directory – *nomedodiretório*** (ou seja, a folha do Azure AD para o diretório que você está gerenciando), escolha **Aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="12a76-109">On the **Azure Active Directory - *directoryname*** blade (that is, the Azure AD blade for the directory you are managing), select **Enterprise applications**.</span></span>

    ![Abrir aplicativos empresariais](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. <span data-ttu-id="12a76-111">Na folha **Aplicativos empresariais**, escolha **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="12a76-111">On the **Enterprise applications** blade, select **All applications**.</span></span> <span data-ttu-id="12a76-112">Você verá uma lista dos aplicativos que pode gerenciar.</span><span class="sxs-lookup"><span data-stu-id="12a76-112">You'll see a list of the apps you can manage.</span></span>
5. <span data-ttu-id="12a76-113">Na folha **Aplicativos empresariais – Todos os aplicativos** , escolha um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="12a76-113">On the **Enterprise applications - All applications** blade, select an app.</span></span>
6. <span data-ttu-id="12a76-114">Na folha ***appname*** (ou seja, a folha com o nome do aplicativo selecionado no título), selecione **Usuários e Grupos**.</span><span class="sxs-lookup"><span data-stu-id="12a76-114">On the ***appname*** blade (that is, the blade with the name of the selected app in the title), select **Users & Groups**.</span></span>

    ![Seleção de usuários ou de grupos](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. <span data-ttu-id="12a76-116">Na folha ***appname*** **- Atribuição de Usuário e Grupo**, selecione um dos usuários ou grupos, em seguida, selecione o comando **Remover**.</span><span class="sxs-lookup"><span data-stu-id="12a76-116">On the ***appname*** **- User & Group Assignment** blade, select one of more users or groups and then select the **Remove** command.</span></span> <span data-ttu-id="12a76-117">Confirme sua decisão na solicitação.</span><span class="sxs-lookup"><span data-stu-id="12a76-117">Confirm your decision at the prompt.</span></span>

    ![Seleção do comando Remover](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a><span data-ttu-id="12a76-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="12a76-119">Next steps</span></span>
* [<span data-ttu-id="12a76-120">Ver todos os meus grupos</span><span class="sxs-lookup"><span data-stu-id="12a76-120">See all of my groups</span></span>](active-directory-groups-view-azure-portal.md)
* [<span data-ttu-id="12a76-121">Atribuir um usuário ou um grupo a um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="12a76-121">Assign a user or group to an enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)
* [<span data-ttu-id="12a76-122">Desabilitar as entradas de usuário em um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="12a76-122">Disable user sign-ins for an enterprise app</span></span>](active-directory-coreapps-disable-app-azure-portal.md)
* [<span data-ttu-id="12a76-123">Alterar o nome ou logotipo de um aplicativo empresarial</span><span class="sxs-lookup"><span data-stu-id="12a76-123">Change the name or logo of an enterprise app</span></span>](active-directory-coreapps-change-app-logo-user-azure-portal.md)
