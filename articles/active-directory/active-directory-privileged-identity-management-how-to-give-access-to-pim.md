---
title: aaaHow toogive acesso tooPrivileged Identity Management - Azure | Microsoft Docs
description: "Saiba como tooadd funções toousers com hello extensão do Azure Active Directory Privileged Identity Management para que eles possam PIM."
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
ms.openlocfilehash: 5d99589af4af766e430d7cecd743ace752f63768
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="giving-access-toomanage-azure-ad-privileged-identity-management"></a><span data-ttu-id="33d8f-103">Fornecendo acesso toomanage Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="33d8f-103">Giving access toomanage Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="33d8f-104">administrador global Hello, que permite que o Azure AD Privileged Identity Management (PIM) para uma organização automaticamente obter atribuições de função e acesso tooPIM.</span><span class="sxs-lookup"><span data-stu-id="33d8f-104">hello global administrator who enables Azure AD Privileged Identity Management (PIM) for an organization automatically get role assignments and access tooPIM.</span></span> <span data-ttu-id="33d8f-105">Entretanto, ninguém mais obtém acesso de gravação por padrão, incluindo outros administradores globais.</span><span class="sxs-lookup"><span data-stu-id="33d8f-105">No one else gets write access by default, though, including other global administrators.</span></span> <span data-ttu-id="33d8f-106">Outros administradores globais, administradores de segurança e leitores de segurança têm acesso somente leitura tooAzure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="33d8f-106">Other global adminstrators, security administrators, and security readers have read-only access tooAzure AD PIM.</span></span> <span data-ttu-id="33d8f-107">toogive tooPIM de acesso, o usuário primeiro Olá pode atribuir outros toohello **administrador com privilégios de função** função.</span><span class="sxs-lookup"><span data-stu-id="33d8f-107">toogive access tooPIM, hello first user can assign others toohello **Privileged role administrator** role.</span></span> <span data-ttu-id="33d8f-108">Essa atribuição deve ser feita no próprio PIM e não pode ser alterada por meio do PowerShell ou outros portais.</span><span class="sxs-lookup"><span data-stu-id="33d8f-108">This assignment must be done from within PIM itself, and cannot be changed via PowerShell or other portals.</span></span>

> [!NOTE]
> <span data-ttu-id="33d8f-109">O gerenciamento do Azure AD PIM requer o Azure MFA.</span><span class="sxs-lookup"><span data-stu-id="33d8f-109">Managing Azure AD PIM requires Azure MFA.</span></span> <span data-ttu-id="33d8f-110">Como as contas da Microsoft não podem se registrar para o Azure MFA, um usuário que entra com uma conta da Microsoft não pode acessar o Azure AD PIM.</span><span class="sxs-lookup"><span data-stu-id="33d8f-110">Since Microsoft accounts cannot register for Azure MFA, a user who signs in with a Microsoft account cannot access Azure AD PIM.</span></span>
> 
> 

<span data-ttu-id="33d8f-111">Certifique-se de que haja sempre pelo menos dois usuários em uma função de administrador de função com privilégios, no caso de um usuário estar bloqueado ou sua conta ser excluída.</span><span class="sxs-lookup"><span data-stu-id="33d8f-111">Make sure there are always at least two users in a privileged role administrator role, in case one user is locked out or their account is deleted.</span></span>

## <a name="give-another-user-access-toomanage-pim"></a><span data-ttu-id="33d8f-112">Dê toomanage acesso de outro usuário PIM</span><span class="sxs-lookup"><span data-stu-id="33d8f-112">Give another user access toomanage PIM</span></span>
1. <span data-ttu-id="33d8f-113">Entrar toohello [portal do Azure](https://portal.azure.com/) e selecione hello **do Azure AD Privileged Identity Management** aplicativo no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="33d8f-113">Sign in toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** app on hello dashboard.</span></span>
2. <span data-ttu-id="33d8f-114">Selecione **Gerenciar funções com privilégios** > **Administrador com função com privilégios** > **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="33d8f-114">Select **Manage privileged roles** > **Privileged role administrator** > **Add**.</span></span>
   
    ![Adicionar administradores com função com privilégios – captura de tela][1]
3. <span data-ttu-id="33d8f-116">Na folha de usuários gerenciados adicionar Olá, etapa 1 já está concluída.</span><span class="sxs-lookup"><span data-stu-id="33d8f-116">On hello Add managed users blade, step 1 is already complete.</span></span> <span data-ttu-id="33d8f-117">A etapa 2, selecione **Selecione usuários** e pesquisa para o usuário Olá você deseja tooadd.</span><span class="sxs-lookup"><span data-stu-id="33d8f-117">Select step 2, **Select users** and search for hello user you want tooadd.</span></span>
   
    ![Selecionar usuários – captura de tela][2]
4. <span data-ttu-id="33d8f-119">Selecione o usuário Olá Olá dos resultados da pesquisa e, em seguida, clique em **feito**.</span><span class="sxs-lookup"><span data-stu-id="33d8f-119">Select hello user from hello search results, and click **Done**.</span></span>
5. <span data-ttu-id="33d8f-120">Clique em **Okey** toosave sua seleção.</span><span class="sxs-lookup"><span data-stu-id="33d8f-120">Click **OK** toosave your selection.</span></span> <span data-ttu-id="33d8f-121">usuário Olá selecionado será exibido na lista de saudação de administradores com privilégios de função.</span><span class="sxs-lookup"><span data-stu-id="33d8f-121">hello user you have selected will appear in hello list of Privileged role administrators.</span></span>
   
   * <span data-ttu-id="33d8f-122">Sempre que você atribui um novo toosomeone de função, eles são automaticamente configurados como função de saudação tooactivate qualificados.</span><span class="sxs-lookup"><span data-stu-id="33d8f-122">Whenever you assign a new role toosomeone, they are automatically set up as eligible tooactivate hello role.</span></span> <span data-ttu-id="33d8f-123">Se você quiser toomake permanente na função hello, clique em usuário Olá na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="33d8f-123">If you want toomake them permanent in hello role, click hello user in hello list.</span></span> <span data-ttu-id="33d8f-124">Selecione **fazer perm** no menu de informações de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="33d8f-124">Select **make perm** in hello user information menu.</span></span>
6. <span data-ttu-id="33d8f-125">Enviar link ao usuário Olá muito[guia de Introdução ao Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="33d8f-125">Send hello user a link too[Getting started with Azure AD Privileged Identity Management](active-directory-privileged-identity-management-getting-started.md).</span></span>

## <a name="remove-another-users-access-rights-for-managing-pim"></a><span data-ttu-id="33d8f-126">Remover direitos de acesso de outro usuário para o gerenciamento de PIM</span><span class="sxs-lookup"><span data-stu-id="33d8f-126">Remove another user's access rights for managing PIM</span></span>
<span data-ttu-id="33d8f-127">Antes de você remove da função de administrador com privilégios de função hello, sempre Certifique-se de haver dois usuários atribuídos tooit.</span><span class="sxs-lookup"><span data-stu-id="33d8f-127">Before you remove someone from hello privileged role administrator role, always make sure there will still be two users assigned tooit.</span></span>

1. <span data-ttu-id="33d8f-128">No painel PIM hello, clique na função hello **administrador com privilégios de função**.</span><span class="sxs-lookup"><span data-stu-id="33d8f-128">In hello PIM dashboard, click on hello role **Privileged role administrator**.</span></span>  <span data-ttu-id="33d8f-129">saudação de lista de usuários atualmente na função será exibida.</span><span class="sxs-lookup"><span data-stu-id="33d8f-129">hello list of users currently in that role will be displayed.</span></span>
2. <span data-ttu-id="33d8f-130">Clique no usuário Olá na lista de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="33d8f-130">Click on hello user in hello user list.</span></span>
3. <span data-ttu-id="33d8f-131">Clique em **Remover**.</span><span class="sxs-lookup"><span data-stu-id="33d8f-131">Click on **Remove**.</span></span>  <span data-ttu-id="33d8f-132">Será exibida uma mensagem de confirmação.</span><span class="sxs-lookup"><span data-stu-id="33d8f-132">You are presented with a confirmation message.</span></span>
4. <span data-ttu-id="33d8f-133">Clique em **Sim** tooremove usuário Olá função hello.</span><span class="sxs-lookup"><span data-stu-id="33d8f-133">Click **Yes** tooremove hello user from hello role.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="33d8f-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="33d8f-134">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_add_PRA.png
[2]: ./media/active-directory-privileged-identity-management-how-to-give-access-to-pim/PIM_select_users.png
