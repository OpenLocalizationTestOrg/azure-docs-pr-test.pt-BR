---
title: Como conceder acesso ao Privileged Identity Management - Azure | Microsoft Docs
description: "Saiba como adicionar funções a usuários com a extensão Azure Active Directory Privileged Identity Management para que possam gerenciar o PIM."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: d4c53b53-2b37-41e6-813c-96ec08a1c897
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: aeaefb484b29da6e89c2c3c650a79a881b3fa5b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="giving-access-to-manage-azure-ad-privileged-identity-management"></a><span data-ttu-id="7f5ec-103">Conceder acesso para gerenciamento do Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="7f5ec-103">Giving access to manage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="7f5ec-104">O administrador global que habilita o Azure AD PIM (Privileged Identity Management) para uma organização automaticamente obtém atribuições de função e acesso ao PIM.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-104">The global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access to PIM.</span></span> <span data-ttu-id="7f5ec-105">Entretanto, ninguém mais obtém acesso de gravação por padrão, incluindo outros administradores globais.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="7f5ec-106">Outros administradores globais, os administradores de segurança e leitores de segurança têm acesso somente leitura ao Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-106">Other global adminstrators, security administrators, and security readers have read-only access to Azure AD PIM.</span></span> <span data-ttu-id="7f5ec-107">Para fornecer acesso ao PIM, o primeiro usuário pode atribuir a outros usuários a função **Administrador com função com privilégios** .</span><span class="sxs-lookup"><span data-stu-id="7f5ec-107">To give access to PIM, the first user can assign others to the **Privileged role administrator** role.</span></span> <span data-ttu-id="7f5ec-108">Essa atribuição deve ser feita no próprio PIM e não pode ser alterada por meio do PowerShell ou outros portais.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="7f5ec-109">O gerenciamento do Azure AD PIM requer o Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="7f5ec-110">Como as contas da Microsoft não podem se registrar para o Azure MFA, um usuário que entra com uma conta da Microsoft não pode acessar o Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="7f5ec-111">Certifique-se de que haja sempre pelo menos dois usuários em uma função de administrador de função com privilégios, no caso de um usuário estar bloqueado ou sua conta ser excluída.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-to-manage-pim"></a><span data-ttu-id="7f5ec-112">Fornecer a outro usuário o acesso para gerenciar o PIM</span><span class="sxs-lookup"><span data-stu-id="7f5ec-112">Give another user access to manage PIM</span></span>
1. <span data-ttu-id="7f5ec-113">Entre no [Portal do Azure](https://portal.azure.com/) e selecione o aplicativo **Azure AD Privileged Identity Management** no painel.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-113">Sign in to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** app on the dashboard.</span></span>
2. <span data-ttu-id="7f5ec-114">Selecione **Gerenciar funções com privilégios** > **Administrador com função com privilégios** > **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Adicionar administradores com função com privilégios – captura de tela][1]
3. <span data-ttu-id="7f5ec-116">Na folha Adicionar usuários gerenciados, a etapa 1 já foi concluída.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-116">On the Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="7f5ec-117">Selecione a etapa 2, **Selecionar usuários** e pesquise o usuário que você deseja adicionar.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-117">Select step 2, **Select users** and search for the user you want to add.</span></span>
   
    ![Selecionar usuários – captura de tela][2]
4. <span data-ttu-id="7f5ec-119">Selecione o usuário nos resultados da pesquisa e clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-119">Select the user from the search results, and click **Done**.</span></span>
5. <span data-ttu-id="7f5ec-120">Clique em **OK** para salvar sua seleção.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-120">Click **OK** to save your selection.</span></span> <span data-ttu-id="7f5ec-121">O usuário que você selecionou aparecerá na lista de Administradores com função com privilégios.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-121">The user you have selected will appear in the list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="7f5ec-122">Sempre que você atribuir uma nova função a alguém, essa pessoa é automaticamente configurada como qualificada para ativar a função.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-122">Whenever you assign a new role to someone, they are automatically set up as eligible to activate the role.</span></span> <span data-ttu-id="7f5ec-123">Se você desejar torná-los permanentes na função, clique no usuário na lista.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-123">If you want to make them permanent in the role, click the user in the list.</span></span> <span data-ttu-id="7f5ec-124">Selecione **tornar perm.** no menu de informações do usuário.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-124">Select **make perm** in the user information menu.</span></span>
6. <span data-ttu-id="7f5ec-125">Enviar ao usuário um link para a [Introdução ao Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="7f5ec-125">Send the user a link to [Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="7f5ec-126">Remover direitos de acesso de outro usuário para o gerenciamento de PIM</span><span class="sxs-lookup"><span data-stu-id="7f5ec-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="7f5ec-127">Antes de remover alguém da função de administrador de função com privilégios, certifique-se de que ainda haverá dois usuários atribuídos a ela.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-127">Before you remove someone from the privileged role administrator role, always make sure there will still be two users assigned to it.</span></span>

1. <span data-ttu-id="7f5ec-128">No painel PIM, clique na função **Administrador com função com privilégios**.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-128">In the PIM dashboard, click on the role **Privileged role administrator**.</span></span>  <span data-ttu-id="7f5ec-129">A lista de usuários atualmente naquela função será exibida.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-129">The list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="7f5ec-130">Clique no usuário na lista de usuários.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-130">Click on the user in the user list.</span></span>
3. <span data-ttu-id="7f5ec-131">Clique em **Remover**.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-131">Click on **Remove**.</span></span>  <span data-ttu-id="7f5ec-132">Será exibida uma mensagem de confirmação.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="7f5ec-133">Clique em **Sim** para remover o usuário da função.</span><span class="sxs-lookup"><span data-stu-id="7f5ec-133">Click **Yes** to remove the user from the role.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="7f5ec-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7f5ec-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
