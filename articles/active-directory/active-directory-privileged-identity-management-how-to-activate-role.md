---
title: "aaaHow tooactivate ou desativar uma função | Microsoft Docs"
description: "Saiba como tooactivate funções privilegiadas identidades de aplicativo do Azure Privileged Identity Management hello."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1ce9e2e7-452b-4f66-9588-0d9cd2539e45
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 8c68ad69e4b006263bbb8a1cfc7ed3dba974e1db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooactivate-or-deactivate-roles-in-azure-ad-privileged-identity-management"></a>Como tooactivate ou desativar funções no Azure AD Privileged Identity Management
Active Directory (AD) Privileged Identity Management do Azure simplifica como as empresas gerenciam o acesso privilegiado tooresources no AD do Azure e outros Microsoft online services como Office 365 ou Microsoft Intune.  

Se você tiver sido feito qualificado para uma função administrativa, isso significa que você pode ativar essa função quando precisar de ações tooperform privilegiado. Por exemplo, se você ocasionalmente gerencia recursos do Office 365, administradores de função com privilégios de sua organização podem não o tornar um Administrador Global permanente, pois essa função também afeta outros serviços. Em vez disso, eles o tornam qualificado para funções do Azure AD, como Administrador do Exchange Online. Você pode solicitar tooactivate essa função quando você precisa de seus privilégios e, em seguida, você terá controle administrativo para um período de tempo predeterminado.

Este artigo é para que os administradores que precisam de tooactivate sua função no Azure AD Privileged Identity Management (PIM). Ele orienta Olá etapas tooactivate uma função quando você precisa de permissões de saudação e desativar a função hello quando terminar. Além disso, os administradores com privilégios de função podem exigir aprovação tooactivate uma função (visualização). Saiba mais sobre os [Fluxos de trabalho de aprovação de PIM](./privileged-identity-management/azure-ad-pim-approval-workflow.md) aqui.

## <a name="add-hello-privileged-identity-management-application"></a>Adicionar aplicativo do hello Privileged Identity Management
Usar o aplicativo do Privileged Identity Management de saudação do AD do Azure no hello [portal do Azure](https://portal.azure.com/) toorequest uma ativação de função, mesmo se você vai toooperate em outro portal ou o PowerShell. Se você não tiver o aplicativo do Azure AD Privileged Identity Management hello em seu portal do Azure, siga essas tooget etapas iniciado.

1. Entrar toohello [portal do Azure](https://portal.azure.com/).
2. Selecione seu nome de usuário no canto superior direito de saudação do hello portal do Azure e diretório hello selecione onde você irá operar.
3. Selecione **mais serviços** e usar Olá toosearch de caixa de texto de filtro para **do Azure AD Privileged Identity Management**.
4. Verificar **Pin toodashboard** e, em seguida, clique em **criar**. Olá aplicativo Privileged Identity Management é aberto.

## <a name="activate-a-role"></a>Ativar uma função
Quando você precisar tootake em uma função, você pode solicitar a ativação selecionando Olá **funções Meus** opção de navegação no aplicativo do hello Azure AD Privileged Identity Management da coluna de navegação esquerda.

1. Entrar toohello [portal do Azure](https://portal.azure.com/) e selecione hello Azure AD Privileged Identity Management bloco.
2. Selecione **Minhas Funções**. Uma lista de suas funções qualificadas atribuídas aparecem na saudação de agrupamento na parte superior de saudação da página de saudação.
3. Selecione uma função tooactivate.
4. Selecione **Ativar**. Olá **solicitar a ativação de função** folha é exibida.
5. Algumas funções exigem a autenticação multifator (MFA) antes de ativar a função hello. Você só pode ter tooauthenticate uma vez por sessão.
   
    ![Verifique com o MFA antes da ativação de função - captura de tela][2]
6. Insira o motivo de saudação para solicitação de ativação Olá no campo de texto de saudação.  Algumas funções exigem toosupply um número de tíquete de problema.
7. Selecione **OK**.  Se a função hello não exigirem a aprovação, agora ele está ativado e função hello aparece na lista de saudação das funções ativas (diretamente abaixo lista Olá de atribuições de função qualificado). Se hello [função requer aprovação](./privileged-identity-management/azure-ad-pim-approval-workflow.md) tooactivate, uma notificação do sistema brevemente aparecerá no canto superior direito de saudação do navegador informando solicitação hello está com aprovação pendente.

    ![Notificação de solicitação pendente – captura de tela][3]

## <a name="deactivate-a-role"></a>Desativar uma função
Após uma função ter sido ativada, ela será desativada automaticamente quando limite de tempo (duração qualificada) for atingido.

Se você concluir suas tarefas de administração no início, você também pode desativar uma função manualmente no aplicativo do Azure AD Privileged Identity Management do hello.  Selecione **funções Meus**, escolha a função hello terminar usando de saudação **atribuições de função Active** agrupamento e selecione **desativar**.  

## <a name="cancel-a-pending-request"></a>Cancelar uma solicitação pendente
No evento de saudação não requerem ativação de uma função que requer aprovação, você pode cancelar uma solicitação pendente a qualquer momento. Simplesmente selecione Olá **funções Meus** opção de navegação no aplicativo do hello Azure AD Privileged Identity Management da coluna de navegação esquerda.

1. Entrar toohello [portal do Azure](https://portal.azure.com/) e selecione hello Azure AD Privileged Identity Management bloco.
2. Selecione **Minhas Funções**. Uma lista de suas funções qualificadas atribuídas aparecem na saudação de agrupamento na parte superior de saudação da página de saudação.
3. Selecione uma função.
4. Selecione Olá **ativação está com aprovação pendente** faixa na folha de detalhes de ativação de função hello.
5. Selecione **Cancelar** na parte superior de saudação do hello **com aprovação pendente** folha.

   ![Cancelar solicitação pendente – captura de tela][4]

## <a name="next-steps"></a>Próximas etapas
Se você estiver interessado em aprender mais sobre o Azure AD Privileged Identity Management, hello links a seguir têm mais informações.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_activation_MFA.png
[3]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Toast2.png
[4]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Banner_Cancel.png
