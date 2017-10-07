---
title: "Tutorial: configurar o ThousandEyes para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como as contas de usuário de provisionar e provisionar eliminação de tooautomatically de Active Directory do Azure do tooconfigure tooThousandEyes."
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
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: f31883ab685d0ffcd9a830aa4a7d43c056f5f4cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a>Tutorial: configurar o ThousandEyes para provisionamento automático de usuário


Olá objetivo deste tutorial é tooshow que Olá etapas necessárias tooperform no provisionamento de tooautomatically ThousandEyes e o Azure AD e desprovisionar contas de usuário do AD do Azure tooThousandEyes. 

## <a name="prerequisites"></a>Pré-requisitos

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

*   Um locatário do Azure Active Directory
*   Um locatário ThousandEyes com hello [plano padrão](https://www.thousandeyes.com/pricing) ou melhor habilitado 
*   Uma conta de usuário no ThousandEyes com permissões de administrador 

> [!NOTE]
> Olá provisionamento integração do AD do Azure depende de saudação [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), que é equipes tooThousandEyes disponíveis no plano de saudação padrão ou superior.

## <a name="assigning-users-toothousandeyes"></a>Atribuir usuários tooThousandEyes

Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos. No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado. 

Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure representam Olá usuários precisam acessar tooyour ThousandEyes aplicativo. Depois de decidir, você pode atribuir esses aplicativos de ThousandEyes tooyour usuários, seguindo as instruções de saudação aqui:

[Atribuir um aplicativo de enterprise tooan usuário ou grupo](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toothousandeyes"></a>Dicas importantes para atribuir usuários tooThousandEyes

*   É recomendável que um único usuário do AD do Azure é atribuído tooThousandEyes tootest Olá configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir um usuário tooThousandEyes, você deve selecionar o hello **usuário** função ou outra válida específicas do aplicativo função (se disponível) na caixa de diálogo de atribuição de saudação. Olá **acesso padrão** função não funciona para o provisionamento, e esses usuários são ignorados.


## <a name="configuring-user-provisioning-toothousandeyes"></a>Configurando tooThousandEyes de provisionamento do usuário 

Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do tooThousandEyes seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no ThousandEyes com base na atribuição de usuário e grupo no AD do Azure.

> [!TIP]
> Você também pode escolher tooenabled baseado no SAML SSO para ThousandEyes, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com). O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.


### <a name="configure-automatic-user-account-provisioning-toothousandeyes-in-azure-ad"></a>Configurar conta de usuário automático provisionamento tooThousandEyes no AD do Azure


1. Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.

2. Se você já tiver configurado ThousandEyes para logon único, procure sua instância do ThousandEyes usando o campo de pesquisa de saudação. Caso contrário, selecione **adicionar** e procure **ThousandEyes** na Galeria de aplicativo hello. Selecione ThousandEyes Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.

3. Selecione sua instância do ThousandEyes, em seguida Olá **provisionamento** guia.

4. Saudação de conjunto **modo de provisionamento** muito**automática**.

    ![Provisionamento do ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. Em Olá **credenciais de administrador** seção, Olá entrada **segredo do Token** gerado pela conta do ThousandEyes (token Olá pode ser encontrado em sua conta ThousandEyes: **segurança & Autenticação**). 

    ![Provisionamento do ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour ThousandEyes aplicativo. Se a conexão de saudação falhar, certifique-se de que sua conta ThousandEyes tem permissões de administrador e repita a etapa 5.

7. Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e a caixa de seleção de saudação de seleção "enviam uma notificação por email quando ocorre uma falha."

8. Clique em **Salvar**. 

9. Em Olá mapeamentos, selecione **tooThousandEyes sincronizar do Azure Active Directory Users**.

10. Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do tooThousandEyes do AD do Azure. Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no ThousandEyes para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.

11. tooenable Olá serviço de provisionamento do AD do Azure para ThousandEyes, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção

12. Clique em **Salvar**. 

Essa operação inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooThousandEyes em Olá usuários e a seção de grupos. a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado. Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionamento de serviço.

Para obter mais informações sobre como o provisionamento de saudação do AD do Azure tooread registra, consulte [relatórios sobre o provisionamento de conta de usuário automático](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-enterprise-apps-manage-provisioning.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Próximas etapas

* [Saiba como tooreview registra e obtenha relatórios sobre a atividade de provisionamento](active-directory-saas-provisioning-reporting.md)
