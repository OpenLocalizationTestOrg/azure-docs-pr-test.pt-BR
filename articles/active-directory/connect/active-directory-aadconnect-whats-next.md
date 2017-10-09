---
title: "Azure AD Connect: Próximas etapas e como toomanage do Azure AD Connect | Microsoft Docs"
description: "Saiba como tooextend Olá tarefas operacionais e configuração padrão para o Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a>Próximas etapas e como toomanage do Azure AD Connect
Use procedimentos operacionais Olá toomeet de conectar do Azure Active Directory (AD do Azure) de toocustomize este artigo necessidades e requisitos de sua organização.  

## <a name="add-additional-sync-admins"></a>Adicionar administradores de sincronização adicionais
Por padrão, o único usuário a saudação Olá administradores locais e instalação são toomanage capaz de mecanismo de sincronização de saudação instalado. Para outras pessoas toobe capaz de tooaccess e gerenciar o mecanismo de sincronização Olá, localize Olá grupo denominado ADSyncAdmins no servidor de local de saudação e adicioná-los toothis grupo.

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a>Atribuir licenças tooAzure os usuários do AD Premium e Enterprise Mobility Suite
Agora que os usuários tenham sido sincronizadas toohello nuvem, você precisa tooassign-los uma licença para eles podem começar a usar aplicativos de nuvem como o Office 365.

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a>tooassign um Azure AD Premium ou Enterprise Mobility Suite licença

1. Entrar toohello portal do Azure como um administrador.
2. Olá esquerda, selecione **do Active Directory**.
3. Em Olá **do Active Directory** página, clique duas vezes no diretório Olá com usuários Olá desejar tooset.
4. Na parte superior de saudação da página de diretório Olá, selecione **licenças**.
5. Em Olá **licenças** página, selecione **Active Directory Premium** ou **Enterprise Mobility Suite**e, em seguida, clique em **atribuir**.
6. Na caixa de diálogo Olá, selecione os usuários de saudação que deseja tooassign licenças para e, em seguida, clique em Olá marca de seleção ícone toosave Olá alterações.

## <a name="verify-hello-scheduled-synchronization-task"></a>Verifique se a tarefa de sincronização agendada Olá
Use o status de saudação do hello toocheck portal do Azure de uma sincronização.

### <a name="tooverify-hello-scheduled-synchronization-task"></a>tarefa de sincronização agendada Olá tooverify
1. Entrar toohello portal do Azure como um administrador.
2. Olá esquerda, selecione **do Active Directory**.
3. Em Olá **do Active Directory** página, clique duas vezes no diretório Olá com usuários Olá desejar tooset.
4. Na parte superior de saudação da página de diretório Olá, selecione **integração de diretórios**.
5. Em **integração com o active directory local**, Olá Observação hora da última sincronização.

<center>![Horário de sincronização de diretórios](./media/active-directory-aadconnect-whats-next/verify.png)</center>

## <a name="start-a-scheduled-synchronization-task"></a>Iniciar uma tarefa de sincronização agendada
Se você precisar toorun uma tarefa de sincronização, você pode fazer isso executando o Assistente de conexão do AD do Azure Olá novamente.  É necessário tooprovide suas credenciais do AD do Azure.  No Assistente de saudação, selecione Olá **personalizar opções de sincronização** de tarefas e, em seguida, clique em **próximo** toomove por meio do Assistente de saudação. No final da saudação, certifique-se de que Olá **iniciar o processo de sincronização de saudação assim que concluir a configuração inicial Olá** está selecionada.

<center>![Iniciar a sincronização](./media/active-directory-aadconnect-whats-next/startsynch.png)</center>

Para obter mais informações sobre a sincronização do hello Azure AD Connect Agendador, consulte [o Agendador de conectar-se de AD do Azure](active-directory-aadconnectsync-feature-scheduler.md).

## <a name="additional-tasks-available-in-azure-ad-connect"></a>Tarefas adicionais disponíveis no Azure AD Connect
Após a instalação inicial do Azure AD Connect, você pode sempre iniciar assistente Olá novamente de saudação do Azure AD Connect iniciar página ou área de trabalho um atalho.  Você observará que entrar novamente por meio do Assistente de saudação fornece algumas novas opções na forma de saudação de tarefas adicionais.  

Olá tabela a seguir fornece um resumo dessas tarefas e uma breve descrição de cada tarefa.

![Lista de tarefas adicionais](./media/active-directory-aadconnect-whats-next/addtasks.png)

| Tarefa adicional | Descrição |
| --- | --- |
| **Cenário do modo de exibição Olá selecionado** |Exiba sua solução atual do Azure AD Connect.  Isso inclui configurações gerais, diretórios sincronizados e configurações de sincronização. |
| **Personalizar opções de sincronização** |Alterar a configuração atual hello como adicionar configuração adicional de toohello de florestas do Active Directory ou habilitar as opções de sincronização, como usuário, grupo, dispositivo ou write-back de senha. |
| **Habilitar o modo de preparo** |Informações de estágio que não estão sincronizadas imediatamente e não é exportado tooAzure AD ou do Active Directory local.  Com esse recurso, você pode visualizar as sincronizações Olá antes que eles ocorram. |

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [como integrar suas identidades locais ao Azure Active Directory](active-directory-aadconnect.md).
