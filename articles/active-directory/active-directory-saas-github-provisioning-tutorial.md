---
title: "Tutorial: Configurando o GitHub para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como as contas de usuário de provisionar e provisionar eliminação de tooautomatically de Active Directory do Azure do tooconfigure tooGitHub."
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
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a>Tutorial: Configurando o GitHub para o provisionamento automático de usuário


Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no GitHub e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooGitHub. 

## <a name="prerequisites"></a>Pré-requisitos

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

*   Um locatário do Azure Active Directory
*   Um locatário Github com hello [plano de negócios](https://help.github.com/articles/organization-billing-plans/#business-plan) ou melhor habilitado 
*   Uma conta de usuário no GitHub com permissões de Administrador 

> [!NOTE]
> Olá provisionamento integração do AD do Azure depende de saudação [GitHub SCIM API](https://developer.github.com/v3/scim/), que é equipes tooGithub disponíveis no plano de negócios hello ou superior.

## <a name="assigning-users-toogithub"></a>Atribuir usuários tooGitHub

Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos. No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado. 

Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure representam Olá usuários precisam acessar o aplicativo do GitHub tooyour. Depois de decidir, você pode atribuir esses aplicativos de GitHub tooyour usuários, seguindo as instruções de saudação aqui:

[Atribuir um aplicativo de enterprise tooan usuário ou grupo](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a>Dicas importantes para atribuir usuários tooGitHub

*   É recomendável que um único usuário do AD do Azure é atribuído tooGitHub tootest Olá configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir um usuário tooGitHub, você deve selecionar o hello **usuário** função ou outra válida específicas do aplicativo função (se disponível) na caixa de diálogo de atribuição de saudação. Olá **acesso padrão** função não funciona para o provisionamento, e esses usuários são ignorados.


## <a name="configuring-user-provisioning-toogithub"></a>Configurando tooGitHub de provisionamento do usuário 

Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do tooGitHub seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no GitHub com base na atribuição de usuário e grupo no AD do Azure.

> [!TIP]
> Você também pode escolher tooenabled baseado no SAML SSO para o GitHub, seguir Olá instruções fornecidas na [portal do Azure](https://portal.azure.com). O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a>Configurar conta de usuário automático provisionamento tooGitHub no AD do Azure


1. Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.

2. Se você já tiver configurado o GitHub para logon único, procure sua instância do usando o campo de pesquisa de saudação do GitHub. Caso contrário, selecione **adicionar** e procure **GitHub** na Galeria de aplicativo hello. Selecione GitHub Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.

3. Selecione sua instância do GitHub, em seguida Olá **provisionamento** guia.

4. Saudação de conjunto **modo de provisionamento** muito**automática**.

    ![Provisionamento do GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. Em Olá **credenciais de administrador** seção, clique em **autorizar**. Essa operação abre uma caixa de diálogo de autorização do GitHub em uma nova janela do navegador. 

6. Na nova janela de hello, entre no GitHub usando sua conta de administrador. No diálogo de autorização resultante hello, selecione o agrupamento de GitHub de saudação que você deseja tooenable provisionamento para e, em seguida, selecione **autorizar**. Saudação de toocomplete portal do Azure depois de concluído, retorne toohello configuração de provisionamento.

    ![Caixa de diálogo Autorização](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. No portal do Azure de Olá, entrada **URL do locatário** e clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour GitHub aplicativo. Se a conexão de saudação falhar, certifique-se de sua conta do GitHub tem permissões de administrador e **URl do locatário** for inserido corretamente e tente hello "Autorizar" etapa novamente (podem provocar **URL do locatário** pela regra: "https : //api.github.com/scim/v2/organizations/ + < Organizations_name > ", você pode encontrar as organizações em sua conta do GitHub: **configurações** > **organizações**).

    ![Caixa de diálogo Autorização](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e a caixa de seleção de saudação de seleção "enviam uma notificação por email quando ocorre uma falha."

9. Clique em **Salvar**. 

10. Em Olá mapeamentos, selecione **tooGitHub sincronizar do Azure Active Directory Users**.

11. Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do tooGitHub do AD do Azure. Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no GitHub para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.

12. tooenable Olá serviço de provisionamento do AD do Azure para o GitHub, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção

13. Clique em **Salvar**. 

Essa operação inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooGitHub em Olá usuários e a seção de grupos. a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado. Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionamento de serviço.

Para obter mais informações sobre como o provisionamento de saudação do AD do Azure tooread registra, consulte [relatórios sobre o provisionamento de conta de usuário automático](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-enterprise-apps-manage-provisioning.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Próximas etapas

* [Saiba como tooreview registra e obtenha relatórios sobre a atividade de provisionamento](active-directory-saas-provisioning-reporting.md)
