---
title: "Tutorial: integração do Azure Active Directory com a Área Restrita do Salesforce | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e a área restrita do Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bab73fda-6754-411d-9288-f73ecdaa486d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 06ff50050845383a602b0edd6fca953ddd37cebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-sandbox-for-automatic-user-provisioning"></a>Tutorial: configurar a Área Restrita Salesforce para provisionamento automático de usuário

Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform em área restrita do Salesforce e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooSalesforce área restrita.

## <a name="prerequisites"></a>Pré-requisitos

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

*   Um locatário do Azure Active Directory.
*   É preciso ter um locatário válido para a Área Restrita Salesforce for Work ou Área Restrita Salesforce for Education. Você pode usar uma conta de avaliação gratuita para qualquer serviço.
*   Uma conta de usuário na Área Restrita Salesforce com permissões de Administrador de Equipe.

## <a name="assigning-users-toosalesforce-sandbox"></a>Atribuir usuários tooSalesforce área restrita

Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos. No contexto de saudação do provisionamento de conta de usuário automático, são sincronizados apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure.

Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure que representam usuários Olá que precisam acessar tooyour aplicativo de área restrita do Salesforce. Depois de decidir, você pode atribuir tooyour esses usuários aplicativos de área restrita do Salesforce, seguindo as instruções de saudação aqui:

[Atribuir um aplicativo de enterprise tooan usuário ou grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce-sandbox"></a>Dicas importantes para atribuir usuários tooSalesforce área restrita

* É recomendável que um único usuário do AD do Azure é atribuído a saudação de tootest de área restrita tooSalesforce configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.

* Ao atribuir um usuário tooSalesforce área restrita, você deve selecionar uma função de usuário válido. função de "Acesso padrão" Hello não funciona para o provisionamento.

> [!NOTE]
> Este aplicativo importa funções personalizadas de área restrita do Salesforce como parte da saudação qual cliente Olá seja tooselect durante a atribuição de usuários no processo de provisionamento.

## <a name="enable-automated-user-provisioning"></a>Habilitar o Provisionamento Automatizado de Usuários

Esta seção orienta você conectar-se a API de provisionamento de conta de usuário de seu AD do Azure tooSalesforce da área restrita e configurando Olá toocreate do serviço de provisionamento, atualizar e desativar contas em área restrita do Salesforce com base em usuários e grupos de usuário atribuído atribuição no AD do Azure.

>[!Tip]
>Você também pode escolher tooenabled baseado no SAML SSO para a área restrita do Salesforce, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com). O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>provisionamento de conta de usuário automático de tooconfigure:

Olá o objetivo desta seção é toooutline como tooenable o provisionamento de usuário do usuário do Active Directory contas tooSalesforce área restrita.

1. Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.

2. Se você já tiver configurado a área restrita do Salesforce para o logon único, pesquisa de sua instância de área restrita do Salesforce usando o campo de pesquisa de saudação. Caso contrário, selecione **adicionar** e procure **área restrita do Salesforce** na Galeria de aplicativo hello. Selecione a área restrita do Salesforce Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.

3. Selecione a instância de área restrita do Salesforce, selecione Olá **provisionamento** guia.

4. Saudação de conjunto **modo de provisionamento** muito**automática**. 
    ![provisionamento](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)

5. Em Olá **credenciais de administrador** seção, forneça Olá definições de configuração a seguir:
   
    a. Em Olá **nome de usuário administrador** caixa de texto, tipo de uma área restrita do Salesforce nome de conta que tem Olá **administrador do sistema** perfil em Salesforce.com atribuído.
   
    b. Em Olá **senha do administrador** caixa de texto, digite a senha Olá para esta conta.

6. tooget seu token de segurança da área restrita do Salesforce, abra uma nova guia e entrar Olá mesma conta de administrador da área restrita do Salesforce. No hello canto superior direito da página de saudação, clique no nome e, em seguida, clique em **minhas configurações**.

     ![Habilitar o provisionamento automático de usuário](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "Habilitar o provisionamento de usuário automático")
7. No painel de navegação esquerdo hello, clique em **pessoal** tooexpand Olá seção relacionada e, em seguida, clique em **redefinir meu Token de segurança**.
  
    ![Habilitar o provisionamento automático de usuário](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "Habilitar o provisionamento de usuário automático")
8. Em Olá **redefinir meu Token de segurança** , clique em Olá **redefinir Token de segurança** botão.

    ![Habilitar o provisionamento automático de usuário](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "Habilitar o provisionamento de usuário automático")
9. Verifique a caixa de entrada de email de Olá associada a essa conta de administrador. Procure um email de Sandbox.com da equipe de vendas que contém o novo token de segurança hello.
10. Copiar Olá token, vá tooyour janela do AD do Azure e cole-a saudação **soquete Token** campo.

11. No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour aplicativo de área restrita do Salesforce.

12. Em Olá **Email de notificação** , digite o endereço de email de saudação de uma pessoa ou grupo que deve receber notificações de erros de provisionamento e marque caixa de seleção de saudação.

13. Clique em **Salvar.**  
    
14.  Em Olá mapeamentos, selecione **sincronizar do Azure Active Directory Users tooSalesforce área restrita.**

15. Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do AD do Azure tooSalesforce área restrita. Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usada na área restrita do Salesforce para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.

16. tooenable Olá serviço de provisionamento do AD do Azure para a área restrita do Salesforce, alteração Olá **Status de provisionamento** muito**em** na seção configurações da saudação

17. Clique em **Salvar.**


Iniciar a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooSalesforce na seção Olá de usuários e grupos de proteção. a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado. Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionamento do serviço de aplicativo de área restrita do Salesforce.

Agora você pode criar uma conta de teste. Aguarde a minutos too20 tooverify Olá conta foi sincronizada toosalesforce.

## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Logon Único](active-directory-saas-salesforcesandbox-tutorial.md)