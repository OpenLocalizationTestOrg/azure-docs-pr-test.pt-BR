---
title: "Tutorial: Integração do Azure Active Directory com o Salesforce | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a916be8dbf0b4c6173cda873936a53cd1f3ff12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a>Tutorial: configurar o Salesforce para provisionamento automático de usuário

Olá objetivo deste tutorial é tooshow Olá etapas necessárias tooperform na equipe de vendas e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooSalesforce.

## <a name="prerequisites"></a>Pré-requisitos

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

*   Um locatário do Azure Active Directory.
*   É preciso ter um locatário válido para o Salesforce for Work ou Salesforce for Education. Você pode usar uma conta de avaliação gratuita para qualquer serviço.
*   Uma conta de usuário no Salesforce com permissões de Administrador de Equipe.

## <a name="assigning-users-toosalesforce"></a>Atribuir usuários tooSalesforce

Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos. No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.

Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure representam Olá usuários precisam acessar o aplicativo do Salesforce tooyour. Depois de decidir, você pode atribuir esses usuários tooyour o aplicativo do Salesforce, seguindo as instruções de saudação aqui:

[Atribuir um aplicativo de enterprise tooan usuário ou grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce"></a>Dicas importantes para atribuir usuários tooSalesforce

*   É recomendável que um único usuário do AD do Azure é atribuído tooSalesforce tootest Olá configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.

*  Ao atribuir um usuário tooSalesforce, você deve selecionar uma função de usuário válido. função de "Acesso padrão" Hello não funciona para provisionamento

    > [!NOTE]
    > Este aplicativo importa funções personalizadas do Salesforce como parte da saudação qual cliente Olá seja tooselect durante a atribuição de usuários no processo de provisionamento

## <a name="enable-automated-user-provisioning"></a>Habilitar o Provisionamento Automatizado de Usuários

Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do tooSalesforce seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no Salesforce com base na atribuição de usuário e grupo no AD do Azure .

>[!Tip]
>Você também pode escolher tooenabled baseado no SAML SSO para Salesforce, seguindo as instruções de saudação fornecidas no [portal do Azure](https://portal.azure.com). O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>provisionamento de conta de usuário automático de tooconfigure:

Olá o objetivo desta seção é toooutline como tooenable o provisionamento de usuário do usuário do Active Directory contas tooSalesforce.

1. Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.

2. Se você já tiver configurado a equipe de vendas para o logon único, procure sua instância do Salesforce usando o campo de pesquisa de saudação. Caso contrário, selecione **adicionar** e procure **Salesforce** na Galeria de aplicativo hello. Selecione a equipe de vendas dos resultados da pesquisa hello e adicioná-lo tooyour lista de aplicativos.

3. Selecione sua instância do Salesforce, em seguida Olá **provisionamento** guia.

4. Saudação de conjunto **modo de provisionamento** muito**automática**. 
![provisionamento](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)

5. Em Olá **credenciais de administrador** seção, forneça Olá definições de configuração a seguir:
   
    a. Em Olá **nome de usuário administrador** caixa de texto, digite nome que tem Olá de conta do Salesforce **administrador do sistema** perfil em Salesforce.com atribuído.
   
    b. Em Olá **senha do administrador** caixa de texto, digite a senha Olá para esta conta.

6. tooget seu token de segurança do Salesforce, abra uma nova guia e entrar Olá mesma conta de administrador do Salesforce. No hello canto superior direito da página de saudação, clique no nome e, em seguida, clique em **minhas configurações**.

     ![Habilitar o provisionamento automático de usuário](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Habilitar o provisionamento de usuário automático")
7. No painel de navegação esquerdo hello, clique em **pessoal** tooexpand Olá seção relacionada e, em seguida, clique em **redefinir meu Token de segurança**.
  
    ![Habilitar o provisionamento automático de usuário](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Habilitar o provisionamento de usuário automático")
8. Em Olá **redefinir meu Token de segurança** , clique em **redefinir Token de segurança** botão.

    ![Habilitar o provisionamento automático de usuário](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Habilitar o provisionamento de usuário automático")
9. Verifique a caixa de entrada de email de Olá associada a essa conta de administrador. Procure um email do Salesforce.com que contém o novo token de segurança hello.
10. Copiar Olá token, vá tooyour janela do AD do Azure e cole-a saudação **soquete Token** campo.

11. No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar o aplicativo do Salesforce tooyour.

12. Em Olá **Email de notificação** , digite o endereço de email de saudação de uma pessoa ou grupo que deve receber as notificações de erro de provisionamento e marque Olá caixa de seleção abaixo.

13. Clique em **Salvar.**  
    
14.  Em Olá mapeamentos, selecione **tooSalesforce sincronizar Azure usuários do Active Directory.**

15. Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do tooSalesforce do AD do Azure. Observe que Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado na equipe de vendas para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.

16. tooenable Olá serviço de provisionamento do AD do Azure para Salesforce, alteração Olá **Status de provisionamento** muito**em** na seção configurações da saudação

17. Clique em **Salvar.**

Isso inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooSalesforce em Olá usuários e a seção de grupos. Observe que a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado. Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo com a equipe de vendas.

Agora você pode criar uma conta de teste. Aguarde a minutos too20 tooverify Olá conta foi sincronizada tooSalesforce.

## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Logon Único](active-directory-saas-salesforce-tutorial.md)