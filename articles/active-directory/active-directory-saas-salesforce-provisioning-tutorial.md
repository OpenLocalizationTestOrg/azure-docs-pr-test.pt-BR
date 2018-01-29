---
title: "Tutorial: Integração do Azure Active Directory com o Salesforce | Microsoft Docs"
description: "Saiba como configurar o logon único entre o Azure Active Directory e o Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/15/2017
ms.author: jeedes
ms.openlocfilehash: 1c7d029515f27610e5d24c56ec1c60d6830e9e45
ms.sourcegitcommit: 6f33adc568931edf91bfa96abbccf3719aa32041
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a>Tutorial: configurando o Salesforce para provisionamento automático de usuário

O objetivo deste tutorial é mostrar as etapas que precisam ser executadas no Salesforce e no Azure AD para provisionar e desprovisionar automaticamente as contas de usuário do Azure AD para o Salesforce.

## <a name="prerequisites"></a>pré-requisitos

O cenário descrito neste tutorial pressupõe que você já tem os seguintes itens:

*   Um locatário do Azure Active Directory.
*   É preciso ter um locatário válido para o Salesforce for Work ou Salesforce for Education. Você pode usar uma conta de avaliação gratuita para qualquer serviço.
*   Uma conta de usuário no Salesforce com permissões de Administrador de Equipe.

## <a name="assigning-users-to-salesforce"></a>Como atribuir usuários ao Salesforce

O Azure Active Directory usa um conceito chamado "atribuições" para determinar quais usuários devem receber acesso aos aplicativos selecionados. No contexto do provisionamento automático de conta de usuário, somente os usuários e os grupos que foram "atribuídos" a um aplicativo no Azure AD serão sincronizados.

Antes de configurar e habilitar o serviço de provisionamento, você precisa decidir quais usuários ou grupos no Azure AD precisam de acesso ao aplicativo Salesforce. Depois de decidir, você pode atribuir esses usuários ao aplicativo Salesforce seguindo as instruções em [Atribuir um usuário ou grupo a um aplicativo empresarial](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-to-salesforce"></a>Dicas importantes para atribuir usuários ao Salesforce

*   Recomendamos a atribuição de um único usuário do Azure AD ao Salesforce para testar a configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.

*  Ao atribuir um usuário ao Salesforce, você deve selecionar uma função de usuário válida. A função de "Acesso Padrão" não funciona para provisionamento

    > [!NOTE]
    > Este aplicativo importa funções personalizadas do Salesforce como parte do processo de provisionamento, que o cliente deve desejar selecionar durante a atribuição de usuários

## <a name="enable-automated-user-provisioning"></a>Habilitar o provisionamento automatizado de usuários

Esta seção orienta você pela conexão do Azure AD com a API de provisionamento de conta de usuário do Salesforce e pela configuração do serviço de provisionamento, a fim de criar, atualizar e desabilitar contas de usuário atribuídas no Salesforce com base na atribuição de usuário e de grupo do Azure AD.

>[!Tip]
>Você também pode optar por habilitar o Logon Único baseado em SAML para o Salesforce, seguindo as instruções fornecidas no [Portal do Azure](https://portal.azure.com). O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.

### <a name="configure-automatic-user-account-provisioning"></a>configurar o provisionamento automático de conta de usuário

O objetivo desta seção é descrever como habilitar o provisionamento de contas de usuário do Active Directory no Salesforce.

1. No [Portal do Azure](https://portal.azure.com), navegue até a seção **Azure Active Directory > Aplicativos Empresariais > Todos os aplicativos**.

2. Se você já tiver configurado o Salesforce para logon único, pesquise sua instância do Salesforce usando o campo de pesquisa. Caso contrário, selecione **Adicionar** e pesquise **Salesforce** na galeria de aplicativos. Selecione o Salesforce nos resultados da pesquisa e adicione-o à lista de aplicativos.

3. Selecione sua instância do Salesforce e selecione a guia **Provisionamento**.

4. Defina o **Modo de Provisionamento** como **Automático**.

    ![provisionamento](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)

5. Na seção **Credenciais de Administrador**, forneça as seguintes definições de configuração:
   
    a. Na caixa de texto **Nome de Usuário Administrador**, digite o nome da conta do Salesforce com o perfil **Administrador do Sistema** no Salesforce.com atribuído.
   
    b. Na caixa de texto **Senha do Administrador**, digite a senha desta conta.

6. Para obter o token de segurança do Salesforce, abra uma nova guia e entre na mesma conta de administrador do Salesforce. No canto superior direito da página, clique em seu nome e em **Configurações**.

     ![Habilitar o provisionamento automático de usuário](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Habilitar o provisionamento de usuário automático")

7. No painel de navegação esquerdo, clique em **Minhas Informações Pessoais** para expandir a seção correspondente e clique em **Redefinir Meu Token de Segurança**.
  
    ![Habilitar o provisionamento automático de usuário](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Habilitar o provisionamento de usuário automático")

8. Na página **Redefinir Token de Segurança**, clique no botão **Redefinir Token de Segurança**.

    ![Habilitar o provisionamento automático de usuário](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Habilitar o provisionamento de usuário automático")

9. Marque a caixa de entrada de email associada a essa conta de administrador. Procure um email do Salesforce.com que contenha o novo token de segurança.

10. Copie o token, vá até a janela do Azure AD e cole-o no campo **Token Secreto**.

11. A **URL do locatário** deve ser inserida se a instância do Salesforce está na Salesforce Government Cloud. Caso contrário, ela é opcional. Insira a URL do locatário usando o formato https://sua-instância.my.salesforce.com, substituindo a instância pelo nome da sua instância do Salesforce.

12. No Portal do Azure, clique em **Testar Conexão** para garantir que o Azure AD possa se conectar ao seu aplicativo Salesforce.

13. Insira o endereço de email de uma pessoa ou grupo que deve receber notificações de erro de provisionamento no campo **Email de Notificação** e marque a caixa de seleção abaixo.

14. Clique em **Salvar.**  
    
15.  Na seção Mapeamentos, selecione **Sincronizar Usuários do Azure Active Directory com o Salesforce.**

16. Na seção **Mapeamentos de Atributo**, revise os atributos de usuário que serão sincronizados do Azure AD para o Salesforce. Observe que os atributos selecionados como propriedades **Correspondentes** serão usados para corresponder as contas de usuário no Salesforce para operações de atualização. Selecione o botão Salvar para confirmar as alterações.

17. Para habilitar o serviço de provisionamento do Azure AD para o Salesforce, altere o **Status de Provisionamento** para **Ativado** na seção Configurações

18. Clique em **Salvar.**

Isso iniciará a sincronização inicial de todos os usuários e/ou grupos atribuídos ao Salesforce na seção Usuários e Grupos. Observe que a sincronização inicial levará mais tempo do que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos, desde que o serviço esteja em execução. Use a seção **Detalhes de Sincronização** para monitorar o progresso e siga os links para os relatórios de atividade de provisionamento, que descrevem todas as ações executadas pelo serviço de provisionamento em seu aplicativo Salesforce.

Agora você pode criar uma conta de teste. Aguarde 20 minutos para verificar se a conta foi sincronizada com o Salesforce.

## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Logon Único](https://docs.microsoft.com/azure/active-directory/active-directory-saas-salesforce-tutorial)
