---
title: "Tutorial: Configurar o Slack para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como as contas de usuário de provisionar e provisionar eliminação de tooautomatically de Active Directory do Azure do tooconfigure tooSlack."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a>Tutorial: Configurar o Slack para provisionamento automático de usuário


Olá, o objetivo deste tutorial é tooshow Olá etapas precisam tooperform na margem de atraso e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooSlack. 

## <a name="prerequisites"></a>Pré-requisitos

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

*   Um locatário de diretório do Azure Active Directory
*   Margem de atraso de locatário com hello [Plus plano](https://aadsyncfabric.slack.com/pricing) ou melhor habilitado 
*   Uma conta de usuário no Slack com permissões de Administrador de Equipe 

Observação: Olá provisionamento integração do AD do Azure depende de saudação [Slack SCIM API](https://api.slack.com/scim) que é equipes tooSlack disponível em hello mais plano ou melhor.

## <a name="assigning-users-tooslack"></a>Atribuir usuários tooSlack

Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos. No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no Azure AD serão sincronizados. 

Antes de configurar e habilitar Olá provisionar um serviço, você precisará toodecide quais usuários e/ou grupos no AD do Azure representam Olá usuários precisam acessar o aplicativo de margem de atraso de tooyour. Depois de decidir, você pode atribuir esses aplicativos de margem de atraso de tooyour usuários, seguindo as instruções de saudação aqui:

[Atribuir um aplicativo de enterprise tooan usuário ou grupo](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a>Dicas importantes para atribuir usuários tooSlack

*   É recomendável que um único usuário do AD do Azure receberá tooSlack tootest Olá configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir um usuário tooSlack, você deve selecionar Olá **usuário** ou uma função de "Grupo" na caixa de diálogo de atribuição de saudação. função de "Acesso padrão" Hello não funciona para o provisionamento.


## <a name="configuring-user-provisioning-tooslack"></a>Configurando tooSlack de provisionamento do usuário 

Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do tooSlack seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído em atraso com base na atribuição de usuário e grupo no AD do Azure.

**Dica:** você também pode escolher tooenabled baseado no SAML SSO para o Slack, seguindo instruções Olá fornecidas no (portal do Azure) [https://portal.azure.com]. O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a>conta de usuário automático tooconfigure provisionamento tooSlack no AD do Azure:


1)  Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.

2) Se você já tiver configurado a margem de atraso para o logon único, pesquisa de sua instância de atraso usando o campo de pesquisa de saudação. Caso contrário, selecione **adicionar** e procure **Slack** na Galeria de aplicativo hello. Selecione a margem de atraso Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.

3)  Selecione a instância de atraso, em seguida Olá **provisionamento** guia.

4)  Saudação de conjunto **modo de provisionamento** muito**automática**.

![Provisionamento do Slack](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  Em Olá **credenciais de administrador** seção, clique em **autorizar**. Isso abre uma caixa de diálogo de autorização do Slack em uma nova janela do navegador. 

6) Na nova janela de Olá, entre usando sua conta de administrador de equipe de margem de atraso. no diálogo de autorização resultante hello, selecione Olá atraso equipe que você deseja tooenable provisionamento para e, em seguida, selecione **autorizar**. Saudação de toocomplete portal do Azure depois de concluído, retorne toohello configuração de provisionamento.

![Caixa de diálogo Autorização](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode conectar o aplicativo de margem de atraso de tooyour. Se a conexão de saudação falhar, certifique-se de que sua conta do Slack tem permissões de administrador de equipe e tente hello "Autorizar" etapa novamente.

8) Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a saudação de caixa de seleção abaixo.

9) Clique em **Salvar**. 

10) Em Olá mapeamentos, selecione **tooSlack sincronizar do Azure Active Directory Users**.

11) Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação serão sincronizados do AD do Azure tooSlack. Observe que Olá atributos selecionados como **correspondência** propriedades serão contas de usuário de saudação toomatch usada na margem de atraso para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.

12) tooenable Olá serviço de provisionamento do AD do Azure para o Slack, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção

13) Clique em **Salvar**. 

Isso iniciará a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooSlack em Olá usuários e a seção de grupos. Observe que a sincronização inicial Olá levará mais tooperform que sincronizações subsequentes, que ocorrem aproximadamente a cada 10 minutos, desde que o serviço hello está sendo executado. Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo a margem de atraso.

## <a name="optional-configuring-group-object-provisioning-tooslack"></a>[Opcional] Configurar provisionamento tooSlack do objeto de grupo 

Opcionalmente, você pode habilitar o provisionamento Olá dos objetos de grupo do AD do Azure tooSlack. Isso é diferente de "atribuir grupos de usuários", no objeto do grupo real Olá além tooits membros serão replicados do tooSlack do AD do Azure. Por exemplo, se você tiver um grupo chamado "Meu Grupo" no Azure AD, um grupo de idêntico chamado "Meu Grupos" será criado dentro do Slack.

### <a name="tooenable-provisioning-of-group-objects"></a>tooenable provisionamento dos objetos de grupo:

1) Em Olá mapeamentos, selecione **tooSlack sincronizar Azure grupos do Active Directory**.

2) Na folha de mapeamento de atributo hello, defina tooYes habilitado.

3) Em Olá **mapeamentos de atributo** seção, revise os atributos de grupo de saudação serão sincronizados do AD do Azure tooSlack. Observe que Olá atributos selecionados como **correspondência** propriedades serão grupos de saudação do toomatch usada na margem de atraso para operações de atualização. 

4) Clique em **Salvar**.

Esse resultado em qualquer tooSlack de objetos atribuídos do grupo no hello **usuários e grupos** seção totalmente sendo sincronizado tooSlack do AD do Azure. Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo a margem de atraso.


## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-enterprise-apps-manage-provisioning.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
