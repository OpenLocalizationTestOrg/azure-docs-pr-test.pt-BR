---
title: "Tutorial: configurar o LinkedIn Elevate para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como as contas de usuário de provisionar e provisionar eliminação de tooautomatically de Active Directory do Azure do tooconfigure tooLinkedIn elevar."
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
ms.openlocfilehash: 08201c078ece0054e75ec0c004840e5186e0e704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-elevate-for-automatic-user-provisioning"></a>Tutorial: configurar o LinkedIn Elevate para provisionamento automático de usuário


Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no LinkedIn elevar e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooLinkedIn elevar. 

## <a name="prerequisites"></a>Pré-requisitos

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

*   Um locatário do Azure Active Directory
*   Um locatário no LinkedIn Elevate 
*   Uma conta de administrador no LinkedIn elevar acesso toohello LinkedIn Centro de contas

> [!NOTE]
> Active Directory do Azure integra LinkedIn elevar usando Olá [SCIM](http://www.simplecloud.info/) protocolo.

## <a name="assigning-users-toolinkedin-elevate"></a>Atribuir usuários tooLinkedIn elevar

Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos. No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no Azure AD serão sincronizados. 

Antes de configurar e habilitar Olá provisionar um serviço, você precisará toodecide quais usuários e/ou grupos no AD do Azure que representam usuários Olá que precisam acessar tooLinkedIn elevar. Depois de decidir, você pode atribuir essas tooLinkedIn usuários elevar seguindo as instruções de saudação aqui:

[Atribuir um aplicativo de enterprise tooan usuário ou grupo](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-elevate"></a>Dicas importantes para atribuir usuários tooLinkedIn elevar

*   É recomendável que um único usuário do AD do Azure receberá tooLinkedIn elevar tootest Olá configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir uma elevação de tooLinkedIn do usuário, você deve selecionar Olá **usuário** função na caixa de diálogo de atribuição de saudação. função de "Acesso padrão" Hello não funciona para o provisionamento.


## <a name="configuring-user-provisioning-toolinkedin-elevate"></a>Configurando tooLinkedIn elevar o provisionamento de usuário

Esta seção orienta você conectar-se a conta de usuário SCIM do elevar tooLinkedIn seu AD do Azure API de provisionamento e configuração Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no LinkedIn elevar com base no usuário e grupo atribuição no AD do Azure.

**Dica:** você também pode escolher tooenabled baseado no SAML SSO para elevar LinkedIn, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com). O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-elevate-in-azure-ad"></a>conta de usuário automático tooconfigure provisionamento tooLinkedIn elevar no AD do Azure:


primeira etapa de saudação é tooretrieve seu token de acesso do LinkedIn. Se você for um administrador corporativo, você poderá provisionar um token de acesso automaticamente. No Centro de sua conta, vá muito**configurações &gt; configurações globais** e abra hello **SCIM instalação** painel.

> [!NOTE]
> Se você estiver acessando o Centro de contas Olá diretamente em vez de através de um link, você pode acessar usando Olá etapas a seguir.

1)  Entrar no Centro de tooAccount.

2)  Selecione **Administrador &gt; Configurações de Administrador**.

3)  Clique em **avançado integrações** na lateral esquerda da saudação. Você é direcionado toohello Centro de contas.

4)  Clique em **+ adicionar a nova configuração de SCIM** e siga o procedimento Olá preenchendo cada campo.

> Quando a atribuição automática de licenças não está habilitada, isso significa que somente os dados de usuário estão sincronizados.

![Provisionamento do LinkedIn Elevate](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate1.PNG)

> Quando a atribuição de autolicense estiver habilitada, você precisa toonote a instância do aplicativo e o tipo de licença. Licenças são atribuídas para entrega, primeiro atender base até que todas as licenças de saudação são feitas.

![Provisionamento do LinkedIn Elevate](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate2.PNG)

5)  Clique em **Gerar token**. Você deve ver o vídeo de token de acesso em Olá **token de acesso** campo.

6)  Salve a área de transferência de tooyour de token de acesso ou o computador antes de sair da página hello.

7) Em seguida, entrar toohello [portal do Azure](https://portal.azure.com)e procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.

8) Se você já tiver configurado o LinkedIn elevar para o logon único, procure sua instância do LinkedIn elevar usando o campo de pesquisa de saudação. Caso contrário, selecione **adicionar** e procure **LinkedIn elevar** na Galeria de aplicativo hello. Selecione LinkedIn elevar Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.

9)  Selecione sua instância do LinkedIn elevar e selecione Olá **provisionamento** guia.

10) Saudação de conjunto **modo de provisionamento** muito**automática**.

![Provisionamento do LinkedIn Elevate](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate3.PNG)

11)  Preencha Olá seguintes campos em **credenciais de administrador** :

* Em Olá **URL do locatário** , digite https://api.linkedin.com.

* Em Olá **segredo do Token** campo, insira o token de acesso de saudação gerado na etapa 1 e clique em **Conexão de teste** .

* Você verá uma notificação de êxito no lado de superiordireito de saudação do seu portal.

12) Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a saudação de caixa de seleção abaixo.

13) Clique em **Salvar**. 

14) Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário e grupo Olá que serão sincronizados do AD do Azure tooLinkedIn elevar. Observe que Olá atributos selecionados como **correspondência** propriedades serão usados toomatch Olá as contas de usuário e grupos no LinkedIn elevar para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.

![Provisionamento do LinkedIn Elevate](./media/active-directory-saas-linkedin-elevate-provisioning-tutorial/linkedin_elevate4.PNG)

15) tooenable Olá serviço de provisionamento do AD do Azure para elevar os LinkedIn, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção

16) Clique em **Salvar**. 

Isso iniciará a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooLinkedIn elevar na seção usuários e grupos de saudação. Observe que a sincronização inicial Olá levará mais tooperform que sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado. Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo LinkedIn elevar.


## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-enterprise-apps-manage-provisioning.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
