---
title: "Tutorial: integração do Azure Active Directory do ao Dropbox for Business | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Dropbox for Business."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f3a42e4-6897-4234-af84-b47c148ec3e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0fb01eab4f7c6c4516eac64a4343e46ea221f98d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-dropbox-for-business-for-automatic-user-provisioning"></a>Tutorial: Configurando o Dropbox for Business para o provisionamento automático de usuário

Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no Dropbox para negócios e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooDropbox para empresas.

## <a name="prerequisites"></a>Pré-requisitos

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

*   Um locatário do Azure Active Directory.
*   Uma assinatura habilitada para logon único do Dropbox for Business.
*   Uma conta de usuário no Dropbox for Business com permissões de Administrador de Equipe.

## <a name="assigning-users-toodropbox-for-business"></a>Atribuir usuários tooDropbox para empresas

Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos. No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.

Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure que representam usuários Olá que precisam acessar tooyour Dropbox para o aplicativo de negócios. Depois de decidir, você pode atribuir essas tooyour usuários Dropbox para o aplicativo de negócios seguindo as instruções de saudação aqui:

[Atribuir um aplicativo de enterprise tooan usuário ou grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodropbox-for-business"></a>Dicas importantes para atribuir usuários tooDropbox de negócios

*   É recomendável que um único usuário do AD do Azure é atribuído tooDropbox de saudação do negócio tootest configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir um usuário tooDropbox para empresas, você deve selecionar uma função de usuário válido. função de "Acesso padrão" Hello não funciona para o provisionamento.

## <a name="enable-automated-user-provisioning"></a>Habilitar o Provisionamento Automatizado de Usuários

Esta seção orienta você conectar seu tooDropbox do AD do Azure para a API de provisionamento de conta de usuário da empresa e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído em Dropbox for Business com base no usuário e grupo atribuição no AD do Azure.

>[!Tip]
>Você também pode escolher tooenabled baseado no SAML logon único para Dropbox for Business, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com). O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>provisionamento de conta de usuário automático de tooconfigure:

1. Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.

2. Se você já tiver configurado o Dropbox for Business para logon único, procure sua instância do Dropbox for Business usando o campo de pesquisa de saudação. Caso contrário, selecione **adicionar** e procure **Dropbox for Business** na Galeria de aplicativo hello. Selecione Dropbox for Business dos resultados da pesquisa hello e adicioná-lo tooyour lista de aplicativos.

3. Selecione sua instância do Dropbox for Business e selecione Olá **provisionamento** guia.

4. Saudação de conjunto **modo de provisionamento** muito**automática**. 

    ![provisionamento](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/provisioning.png)

5. Em Olá **credenciais de administrador** seção, clique em **autorizar**. Ela abre uma caixa de diálogo de logon do Dropbox for Business em uma nova janela do navegador.

6. Em Olá **entrar tooDropbox toolink com o Azure AD** caixa de diálogo, tooyour Dropbox para o locatário de negócios de entrada.

     ![Provisionamento do usuário](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769518.png "Provisionamento do usuário")

7. Confirme que deseja toogive Active Directory do Azure permissão toomake alterações tooyour Dropbox para o locatário de negócios. Clique em **Permitir**.
    
      ![Provisionamento do usuário](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/ic769519.png "Provisionamento do usuário")

8. No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour Dropbox para o aplicativo de negócios. Se a conexão de saudação falhar, verifique seu Dropbox para conta de negócios tem permissões de administrador de equipe e tente Olá **"Autorizar"** etapa novamente.

9. Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a caixa de seleção de saudação.

10. Clique em **Salvar.**

11. Em Olá mapeamentos, selecione **tooDropbox sincronizar Azure usuários do Active Directory para a empresa.**

12. Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do AD do Azure tooDropbox para empresas. Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no Dropbox for Business para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.

13. tooenable Olá serviço de provisionamento do AD do Azure para Dropbox for Business, alteração Olá **Status de provisionamento** muito**em** na seção configurações da saudação

14. Clique em **Salvar.**

Ele inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooDropbox para empresas no hello usuários e a seção de grupos. a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado. Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionamento de serviço no seu Dropbox para o aplicativo de negócios.

Agora você pode criar uma conta de teste. Aguarde a minutos too20 tooverify Olá conta foi sincronizada tooDropbox para empresas.

Um ciclo de provisionamento de usuário concluído com êxito é indicado por um status relacionado.

![Atribuir usuários](./media/active-directory-saas-dropboxforbusiness-provisioning-tutorial/IC769523.png "Atribuir usuários")


## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Logon Único](active-directory-saas-dropboxforbusiness-tutorial.md)