---
title: "Tutorial: integração do Azure Active Directory com o Box | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e caixa."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e92baabb174642c22c99e2a30bc9c71845b3b75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a>Tutorial: Configurar o Box para provisionamento automático de usuário

Olá objetivo deste tutorial é tooshow Olá etapas tooperform na caixa e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooBox.

## <a name="prerequisites"></a>Pré-requisitos

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

*   Um locatário do Azure Active Directory.
*   Uma assinatura do Box habilitada para logon único.
*   Uma conta de usuário do Box com permissões de Administrador de Equipe.

## <a name="assigning-users-toobox"></a>Atribuir usuários tooBox 

Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos. No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.

Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure representam Olá usuários precisam acessar tooyour caixa aplicativo. Depois de decidir, você pode atribuir esses usuários tooyour o aplicativo do Box, seguindo as instruções de saudação aqui:

[Atribuir um aplicativo de enterprise tooan usuário ou grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a>Atribuir usuários e grupos
Olá **caixa > usuários e grupos** guia Olá portal do Azure permite que você toospecify quais usuários e grupos deve receber acesso tooBox. Atribuição de um usuário ou grupo faz com que Olá toooccur coisas a seguir:

* AD do Azure permite Olá atribuído tooBox de tooauthenticate de usuário (seja por atribuição direta ou associação de grupo). Se não for atribuído a um usuário, o AD do Azure não permite que eles toosign em tooBox e retorna um erro na página de entrada do AD do Azure de saudação.
* Um bloco de aplicativo para a caixa é adicionado do usuário toohello [iniciador do aplicativo](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).
* Se o provisionamento automático estiver habilitado, usuários Olá atribuído e/ou grupos serão adicionados toohello provisionamento toobe fila provisionado automaticamente.
  
  * Se apenas objetos de usuário foram configurado toobe provisionado, em seguida, todos os usuários diretamente atribuídos são colocados na fila de provisionamento de saudação e todos os usuários que são membros de grupos atribuídos são colocados em Olá provisionamento de fila. 
  * Se os objetos de grupo configurado toobe provisionado, todos os objetos de grupo atribuído são tooBox provisionado e todos os usuários que são membros desses grupos. associações de grupo e usuário Olá são preservadas ao que está sendo gravada tooBox.

Você pode usar o hello **atributos > Single Sign-On** guia tooconfigure quais atributos de usuário (ou declarações) é apresentado tooBox durante a autenticação baseada em SAML e hello **atributos > provisionamento** guia tooconfigure como atributos de usuário e grupo de fluam do AD do Azure tooBox durante o provisionamento de operações.

### <a name="important-tips-for-assigning-users-toobox"></a>Dicas importantes para atribuir usuários tooBox 

*   É recomendável que um único AD do Azure atribuídos pelo usuário tooBox tootest Olá configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir um usuário toobox, você deve selecionar uma função de usuário válido. função de "Acesso padrão" Hello não funciona para o provisionamento.

## <a name="enable-automated-user-provisioning"></a>Habilitar o Provisionamento Automatizado de Usuários

Esta seção orienta conectar-se a API de provisionamento de conta de usuário do tooBox seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído na caixa com base na atribuição de usuário e grupo no AD do Azure.

Se o provisionamento automático estiver habilitado, usuários Olá atribuído e/ou grupos serão adicionados toohello provisionamento toobe fila provisionado automaticamente.
    
 * Se apenas objetos de usuário são toobe configurado provisionado, em seguida, os usuários atribuídos diretamente são colocados na fila de provisionamento de saudação e todos os usuários que são membros de grupos atribuídos são colocados em Olá provisionamento de fila. 
    
 * Se os objetos de grupo configurado toobe provisionado, todos os objetos de grupo atribuído são tooBox provisionado e todos os usuários que são membros desses grupos. associações de grupo e usuário Olá são preservadas ao que está sendo gravada tooBox.

> [!TIP] 
> Você também pode escolher tooenabled baseado no SAML SSO para caixa, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com). O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>provisionamento de conta de usuário automático de tooconfigure:

Olá o objetivo desta seção é toooutline como tooenable provisionamento de usuário do Active Directory contas tooBox.

1. Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.

2. Se você já tiver configurado a caixa para logon único, procure a instância da caixa usando o campo de pesquisa de saudação. Caso contrário, selecione **adicionar** e procure **caixa** na Galeria de aplicativo hello. Marque a caixa de saudação dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.

3. Selecione a instância da caixa e selecione Olá **provisionamento** guia.

4. Saudação de conjunto **modo de provisionamento** muito**automática**. 

    ![provisionamento](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. Em Olá **credenciais de administrador** seção, clique em **autorizar** tooopen uma caixa de diálogo de logon em uma nova janela do navegador.

6. Em Olá **Login toogrant acesso tooBox** página, forneça credenciais Olá necessárias e, em seguida, clique em **autorizar**. 
   
    ![Habilitar o provisionamento automático de usuário](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Habilitar o provisionamento de usuário automático")

7. Clique em **conceder acesso tooBox** tooauthorize toohello essa operação e tooreturn portal do Azure. 
   
    ![Habilitar o provisionamento automático de usuário](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Habilitar o provisionamento de usuário automático")

8. No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour caixa aplicativo. Se a conexão de saudação falhar, certifique-se de que sua conta do Box tem permissões de administrador de equipe e tente Olá **"Autorizar"** etapa novamente.

9. Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a caixa de seleção de saudação.

10. Clique em **Salvar.**

11. Em Olá mapeamentos, selecione **tooBox sincronizar Azure usuários do Active Directory.**

12. Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do tooBox do AD do Azure. Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado na caixa para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.

13. tooenable Olá serviço provisionamento do AD do Azure para caixa, alteração Olá **Status de provisionamento** muito**em** na seção configurações da saudação

14. Clique em **Salvar.**

Que inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooBox em Olá usuários e a seção de grupos. a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado. Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo de caixa.

Agora você pode criar uma conta de teste. Aguarde a minutos too20 tooverify Olá conta foi sincronizada toobox.

No seu locatário do Box, os usuários sincronizados estão listados em **usuários gerenciados** em Olá **Console de administração**.

![Status da integração](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "Status da integração")


## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Logon Único](active-directory-saas-box-tutorial.md)