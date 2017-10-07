---
title: "Tutorial: integração do Azure Active Directory ao Citrix GoToMeeting | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a>Tutorial: Configurar o Citrix GoToMeeting para provisionamento automático de usuário

Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no Citrix GoToMeeting e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooCitrix GoToMeeting.

## <a name="prerequisites"></a>Pré-requisitos

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

*   Um locatário do Azure Active Directory.
*   Uma assinatura do Citrix GoToMeeting habilitada para logon único.
*   Uma conta de usuário no Citrix GoToMeeting com permissões de Administrador de Equipe.

## <a name="assigning-users-toocitrix-gotomeeting"></a>Atribuir usuários tooCitrix GoToMeeting

Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos. No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.

Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure que representam usuários Olá que precisam acessar tooyour aplicativo Citrix GoToMeeting. Depois de decidir, você pode atribuir essas tooyour usuários Citrix GoToMeeting aplicativo seguindo as instruções de saudação aqui:

[Atribuir um aplicativo de enterprise tooan usuário ou grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a>Dicas importantes para atribuir usuários tooCitrix GoToMeeting

*   É recomendável que um único usuário do AD do Azure é atribuído tooCitrix GoToMeeting tootest Olá configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir um usuário tooCitrix GoToMeeting, você deve selecionar uma função de usuário válido. função de "Acesso padrão" Hello não funciona para o provisionamento.

## <a name="enable-automated-user-provisioning"></a>Habilitar o Provisionamento Automatizado de Usuários

Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do GoToMeeting tooCitrix seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas no Citrix GoToMeeting com base em usuários e grupos de usuário atribuído atribuição no AD do Azure.

> [!TIP]
> Você também pode escolher tooenabled baseado no SAML SSO para Citrix GoToMeeting, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com). O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>provisionamento de conta de usuário automático de tooconfigure:

1. Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.

2. Se você já tiver configurado o Citrix GoToMeeting para logon único, procure sua instância do usando o campo de pesquisa de saudação do Citrix GoToMeeting. Caso contrário, selecione **adicionar** e procure **Citrix GoToMeeting** na Galeria de aplicativo hello. Selecione o Citrix GoToMeeting Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.

3. Selecione sua instância do Citrix GoToMeeting, em seguida Olá **provisionamento** guia.

4. Saudação de conjunto **provisionamento** modo muito**automática**. 

    ![provisionamento](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. Na seção de credenciais de administrador do hello, execute Olá etapas a seguir:
   
    a. Em Olá **nome de usuário de administrador do Citrix GoToMeeting** caixa de texto, nome de usuário de saudação do tipo de um administrador.

    b. Em Olá **senha do administrador do Citrix GoToMeeting** texto, a senha do administrador do hello.

6. No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour aplicativo Citrix GoToMeeting. Se a conexão de saudação falhar, certifique-se de que sua conta do Citrix GoToMeeting tem permissões de administrador de equipe e tente Olá **"Credenciais de administrador"** etapa novamente.

7. Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a caixa de seleção de saudação.

8. Clique em **Salvar.**

9. Em Olá mapeamentos, selecione **sincronizar do Azure Active Directory Users tooCitrix GoToMeeting.**

10. Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do AD do Azure tooCitrix GoToMeeting. Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no Citrix GoToMeeting para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.

11. tooenable Olá serviço de provisionamento do AD do Azure para Citrix GoToMeeting, alteração Olá **Status de provisionamento** muito**em** na seção configurações da saudação

12. Clique em **Salvar.**

Iniciar a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooCitrix GoToMeeting na seção usuários e grupos de saudação. a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado. Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo da Citrix GoToMeeting.

## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Logon Único](active-directory-saas-citrix-gotomeeting-tutorial.md)


