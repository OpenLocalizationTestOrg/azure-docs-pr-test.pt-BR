---
title: aaaRoles no Azure AD Privileged Identity Management | Microsoft Docs
description: "Saiba quais funções são usadas para identidades com privilégios com hello extensão Privileged Identity Management do Azure."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ac812ccc-cf4e-4ac2-b981-69598056c9ed
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/31/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017;oldportal;it-pro;
ms.openlocfilehash: dc58d005489e3b51b3b3dbea4bf35bd795dbdfb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="different-administrative-role-in-azure-active-directory-pim"></a>Função administrativa diferente no PIM do Azure Active Directory
<!-- **PLACEHOLDER: Need description of how this works. Azure PIM uses roles from MSODS objects.**-->

Você pode atribuir o usuários em sua organização funções administrativas toodifferent no AD do Azure. Essas atribuições de função controlam quais tarefas, como adicionar ou remover usuários ou alterar configurações de serviço, Olá os usuários estiverem tooperform capaz de AD do Azure, Office 365 e outros serviços Online da Microsoft e aplicativos conectados.  

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo.

Um administrador global pode atualizar os usuários que devem **permanentemente** atribuído tooroles no AD do Azure, usando os cmdlets do PowerShell como `Add-MsolRoleMember` e `Remove-MsolRoleMember`, ou por meio do portal clássico Olá conforme descrito em [ atribuindo funções de administrador no Azure Active Directory](active-directory-assign-admin-roles.md).

O Azure AD PIM (Privileged Identity Management) gerencia políticas para o acesso privilegiado para usuários no Azure AD. PIM atribui usuários tooone ou mais funções no AD do Azure, e você pode atribuir alguém toobe permanentemente em uma função de saudação ou qualificados para a função hello. Quando um usuário é atribuído permanentemente a função tooa ou ativa uma atribuição de função qualificado, em seguida, que podem gerenciar o Active Directory do Azure, Office 365 e outros aplicativos com permissões Olá tootheir funções atribuídas.

Não há nenhuma diferença no acesso de saudação fornecido toosomeone com uma permanente em vez de uma atribuição de função qualificado. Olá única diferença é que algumas pessoas não é necessário que o acesso a todo o tempo de saudação. Eles estarão qualificados para a função hello e podem ativá-la e off sempre que eles precisam.

## <a name="roles-managed-in-pim"></a>Funções gerenciadas no PIM
Privileged Identity Management permite que você atribua funções de administrador toocommon usuários, incluindo:

* **Administrador global** (também conhecida como administrador da empresa) tem recursos administrativos do acesso tooall. Você pode ter mais de um administrador global na sua organização. Olá pessoa que se inscreve automaticamente o toopurchase Office 365 torna-se um administrador global.
* **Administrador com função com privilégios** gerencia o Azure AD PIM e atualiza as atribuições de função para outros usuários.  
* **Administrador de cobrança** faz compras, gerencia as assinaturas, gerencia tíquetes de suporte e monitora a integridade do serviço.
* **Administrador de senhas** redefine as senhas, gerencia as solicitações de serviço e monitora a integridade do serviço. Administradores de senha são limitados tooresetting senhas de usuários.
* **Administrador de serviços** gerencia as solicitações de serviço e monitora a integridade do serviço.
  
  > [!NOTE]
  > Se você estiver usando o Office 365, antes de atribuir o usuário de tooa função do administrador de serviço hello, primeiro atribua permissões administrativas do usuário Olá tooa serviço, como o Exchange Online.
  > 
  > 
* **Administrador de gerenciamento de usuários** redefine as senhas, monitora a integridade do serviço e gerencia contas de usuário, grupos de usuários e solicitações de serviço. Olá administrador de gerenciamento de usuário não pode excluir um administrador global, criar outras funções de administrador ou redefinir senhas para cobrança, globais e administradores de serviço.
* **Administrador do Exchange** tem acesso administrativo tooExchange Online por meio do Centro de administração do Exchange hello (EAT) e pode executar quase todas as tarefas no Exchange Online.
* **Administrador do SharePoint** tem acesso administrativo tooSharePoint Online por meio do Centro de administração do SharePoint Online hello e pode executar quase todas as tarefas no SharePoint Online.
* **Skype para o administrador da empresa** tem acesso administrativo tooSkype para negócios por meio de hello Skype para centro de administração de negócios e pode executar quase todas as tarefas no Skype for Business Online.

Leia estes artigos para obter mais detalhes sobre como [atribuir funções de administrador no Azure AD](active-directory-assign-admin-roles.md) e [atribuir funções de administrador no Office 365](https://support.office.com/article/Assigning-admin-roles-in-Office-365-eac4d046-1afd-4f1a-85fc-8219c79e1504).

<!--**PLACEHOLDER: hello above article may not be hello one we want since PIM gets roles from places other that Office 365**-->


Do PIM, você pode [atribuir o usuário de tooa essas funções](active-directory-privileged-identity-management-how-to-add-role-to-user.md) para que hello usuário possa [ativar a função hello quando necessário](active-directory-privileged-identity-management-how-to-activate-role.md).

Se você quiser que outra toomanage de acesso de usuário no PIM em si, funções de saudação que requer o PIM Olá usuário toohave são descritos mais detalhadamente em toogive [como toogive acessar tooPIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).

<!-- ## hello PIM Security Administrator Role **PLACEHOLDER: Need description of hello Security Administrator role.**-->

## <a name="roles-not-managed-in-pim"></a>Funções não gerenciadas no PIM
Funções no Exchange Online ou SharePoint Online, exceto por aquelas mencionadas acima, não são representadas no Azure AD e, portanto, não são visíveis no PIM. Para obter mais informações sobre como alterar as atribuições de função refinadas nesses serviços do Office 365, consulte [Permissões no Office 365](https://support.office.com/article/Permissions-in-Office-365-da585eea-f576-4f55-a1e0-87090b6aaa9d).

As assinaturas e grupos de recursos do Azure também não são representados no Azure AD. toomanage Azure assinaturas, consulte [como tooadd ou alterar funções de administrador do Azure](../billing/billing-add-change-azure-subscription-administrator.md) e para obter mais informações sobre, consulte o RBAC do Azure [o controle de acesso](role-based-access-control-configure.md).

<!--**hello above links might be replaced by ones that are from within this documentation repository **-->


## <a name="user-roles-and-signing-in"></a>Funções de usuário e entrada
Para alguns aplicativos e serviços Microsoft, atribuir uma função de usuário tooa pode não ser suficiente tooenable toobe esse usuário um administrador.

Acesso toohello portal clássico do Azure requer Olá usuário ser um administrador de serviço ou coadministrador em uma assinatura do Azure, mesmo se o usuário Olá não precisa toomanage Olá assinaturas do Azure.  Por exemplo, toomanage definições de configuração do AD do Azure no portal clássico do hello, um usuário devem ser um administrador global no AD do Azure e um coadministrador da assinatura em uma assinatura do Azure.  toolearn como tooadd assinaturas de tooAzure de usuários, consulte [como tooadd ou alterar funções de administrador do Azure](../billing/billing-add-change-azure-subscription-administrator.md).

Acesso tooMicrosoft serviços on-line pode exigir Olá também ser atribuída uma licença ao usuário antes de abrir o portal do serviço de saudação ou executar tarefas administrativas.

## <a name="assign-a-license-tooa-user-in-azure-ad"></a>Atribuir um usuário de tooa de licença no AD do Azure
1. Entrar toohello [portal clássico do Azure](http://manage.windowsazure.com) com uma conta de administrador global ou um coadministrador.
2. Selecione **todos os itens** no menu principal da saudação.
3. Selecione o diretório de saudação que deseja toowork com e que tem licenças associado a ele.
4. Selecione **Licenças**. será exibida a lista de saudação de licenças disponíveis.
5. Selecione o plano de licença Olá que contém Olá licenças que você deseja toodistribute.
6. Selecione **Atribuir Usuários**.
7. Usuário Olá selecione que você deseja tooassign uma licença para.
8. Clique em Olá **atribuir** botão.  Olá usuário agora pode entrar tooAzure.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

