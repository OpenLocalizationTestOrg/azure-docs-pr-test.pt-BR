---
title: "Tutorial: configurar o LinkedIn Sales Navigator para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como as contas de usuário de provisionar e provisionar eliminação de tooautomatically de Active Directory do Azure do tooconfigure tooLinkedIn navegador de vendas."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 322c5271535994c13a9fafadbf74f356cdfe865d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-sales-navigator-for-automatic-user-provisioning"></a>Tutorial: configurar o LinkedIn Sales Navigator para provisionamento automático de usuário


Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no LinkedIn vendas navegador e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooLinkedIn navegador de vendas. 

## <a name="prerequisites"></a>Pré-requisitos

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

*   Um locatário do Azure Active Directory
*   Um locatário do LinkedIn Sales Navigator 
*   Uma conta de administrador no navegador de vendas do LinkedIn com acesso toohello LinkedIn Centro de contas

> [!NOTE]
> Active Directory do Azure integra-se ao navegador de vendas LinkedIn usando Olá [SCIM](http://www.simplecloud.info/) protocolo.

## <a name="assigning-users-toolinkedin-sales-navigator"></a>Atribuir usuários tooLinkedIn navegador de vendas

Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos. No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no Azure AD serão sincronizados. 

Antes de configurar e habilitar Olá provisionar um serviço, você precisará toodecide quais usuários e/ou grupos no AD do Azure que representam usuários Olá que precisam acessar tooLinkedIn navegador de vendas. Depois de decidir, você pode atribuir tooLinkedIn esses usuários vendas navegador seguindo as instruções de saudação aqui:

[Atribuir um aplicativo de enterprise tooan usuário ou grupo](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-sales-navigator"></a>Dicas importantes para atribuir usuários tooLinkedIn navegador de vendas

*   É recomendável que um único usuário do AD do Azure ser atribuído a saudação de tootest do navegador de vendas tooLinkedIn configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir um tooLinkedIn vendas navegador do usuário, você deve selecionar Olá **usuário** função na caixa de diálogo de atribuição de saudação. função de "Acesso padrão" Hello não funciona para o provisionamento.


## <a name="configuring-user-provisioning-toolinkedin-sales-navigator"></a>Configurando tooLinkedIn navegador de vendas de provisionamento do usuário

Esta seção orienta você conectar-se a conta de usuário SCIM do navegador seu AD do Azure tooLinkedIn vendas API de provisionamento e configuração Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no navegador de vendas do LinkedIn com base no usuário e atribuição de grupo no AD do Azure.

> [!TIP]
> Você também pode escolher tooenabled baseado no SAML SSO para LinkedIn vendas Navigator, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com). O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-sales-navigator-in-azure-ad"></a>conta de usuário automático tooconfigure provisionamento tooLinkedIn navegador de vendas no AD do Azure:


primeira etapa de saudação é tooretrieve seu token de acesso do LinkedIn. Se você for um administrador corporativo, você poderá provisionar um token de acesso automaticamente. No Centro de sua conta, vá muito**configurações &gt; configurações globais** e abra hello **SCIM instalação** painel.

> [!NOTE]
> Se você estiver acessando o Centro de contas Olá diretamente em vez de através de um link, você pode acessar usando Olá etapas a seguir.

1)  Entrar no Centro de tooAccount.

2)  Selecione **Administrador &gt; Configurações de Administrador**.

3)  Clique em **avançado integrações** na lateral esquerda da saudação. Você é direcionado toohello Centro de contas.

4)  Clique em **+ adicionar a nova configuração de SCIM** e siga o procedimento Olá preenchendo cada campo.

> Quando a atribuição automática de licenças não está habilitada, isso significa que somente os dados de usuário estão sincronizados.

![Provisionamento do LinkedIn Sales Navigator](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_1.PNG)

> Quando a atribuição de autolicense estiver habilitada, você precisa toonote a instância do aplicativo e o tipo de licença. Licenças são atribuídas para entrega, primeiro atender base até que todas as licenças de saudação são feitas.

![Provisionamento do LinkedIn Sales Navigator](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_2.PNG)

5)  Clique em **Gerar token**. Você deve ver o vídeo de token de acesso em Olá **token de acesso** campo.

6)  Salve a área de transferência de tooyour de token de acesso ou o computador antes de sair da página hello.

7) Em seguida, entrar toohello [portal do Azure](https://portal.azure.com)e procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.

8) Se você já tiver configurado o navegador de vendas LinkedIn para logon único, pesquisa de sua instância do navegador de vendas LinkedIn usando o campo de pesquisa de saudação. Caso contrário, selecione **adicionar** e procure **LinkedIn vendas navegador** na Galeria de aplicativo hello. Selecione navegador de vendas LinkedIn Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.

9)  Selecione a instância do navegador de vendas LinkedIn, selecione Olá **provisionamento** guia.

10) Saudação de conjunto **modo de provisionamento** muito**automática**.

![Provisionamento do LinkedIn Sales Navigator](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_3.PNG)

11)  Preencha Olá seguintes campos em **credenciais de administrador** :

* Em Olá **URL do locatário** , digite https://api.linkedin.com.

* Em Olá **segredo do Token** campo, insira o token de acesso de saudação gerado na etapa 1 e clique em **Conexão de teste** .

* Você verá uma notificação de êxito no lado de superiordireito de saudação do seu portal.

12) Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a saudação de caixa de seleção abaixo.

13) Clique em **Salvar**. 

14) Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário e grupo Olá que serão sincronizados do AD do Azure tooLinkedIn navegador de vendas. Observe que Olá atributos selecionados como **correspondência** propriedades serão usados toomatch Olá as contas de usuário e grupos no navegador de vendas LinkedIn para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.

![Provisionamento do LinkedIn Sales Navigator](./media/active-directory-saas-linkedinsalesnavigator-provisioning-tutorial/linkedin_4.PNG)

15) tooenable Olá serviço de provisionamento do AD do Azure para LinkedIn vendas Navigator, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção

16) Clique em **Salvar**. 

Isso iniciará a sincronização inicial de usuários e/ou grupos atribuídos tooLinkedIn navegador de vendas na seção usuários e grupos de Olá Olá. Observe que a sincronização inicial Olá levará mais tooperform que sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado. Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo de navegador de vendas do LinkedIn.


## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-enterprise-apps-manage-provisioning.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
