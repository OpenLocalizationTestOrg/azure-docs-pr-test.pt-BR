---
title: "Tutorial: Configurar o Cerner Central para o provisionamento automático de usuário com o Azure Active Directory | Microsoft Docs"
description: "Saiba como tooautomatically do Active Directory do Azure tooconfigure provisionar a lista de tooa de usuários em Cerner Central."
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
ms.date: 05/26/2017
ms.author: asmalser-msft
ms.openlocfilehash: e96da98e783d24e7f34ae924824f909eead75f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-cerner-central-for-automatic-user-provisioning"></a>Tutorial: Configurar o Cerner Central para provisionamento automático de usuário

Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform em Cerner Central e o Azure AD tooautomatically provisão de provisionar contas de usuário e da lista de usuário do AD do Azure tooa no Cerner Central. 


## <a name="prerequisites"></a>Pré-requisitos

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

*   Um locatário do Azure Active Directory
*   Um locatário do Cerner Central 

> [!NOTE]
> Active Directory do Azure se integra ao centro Cerner usando Olá [SCIM](http://www.simplecloud.info/) protocolo.

## <a name="assigning-users-toocerner-central"></a>Atribuir usuários tooCerner Central

Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos. No contexto de saudação do provisionamento de conta de usuário automático, são sincronizados apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure. 

Antes de configurar e habilitar Olá provisionar um serviço, você deve decidir quais usuários e/ou grupos no AD do Azure representam usuários Olá que precisam acessar tooCerner Central. Depois de decidir, você pode atribuir essas tooCerner usuários Central seguindo as instruções de saudação aqui:

[Atribuir um aplicativo de enterprise tooan usuário ou grupo](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toocerner-central"></a>Dicas importantes para atribuir usuários tooCerner Central

*   É recomendável que um único usuário do AD do Azure receberá tooCerner tootest Central Olá configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.

* Depois que o teste inicial for concluída para um único usuário, centro Cerner recomenda atribuir toda a lista de usuários devem tooaccess Olá lista de usuário de qualquer toobe provisionado tooCerner Cerner solução (não apenas Cerner Central).  Outras soluções Cerner aproveitam essa lista de usuários na lista de usuário hello.

*   Ao atribuir um usuário tooCerner Central, você deve selecionar Olá **usuário** função na caixa de diálogo de atribuição de saudação. Os usuários com função de "Acesso padrão" hello são excluídos do provisionamento.


## <a name="configuring-user-provisioning-toocerner-central"></a>Configurando tooCerner Central de provisionamento do usuário

Esta seção orienta você conectar-se a lista de usuários do AD do Azure tooCerner Central com conta de usuário SCIM da Cerner API de provisionamento e configuração Olá toocreate do serviço de provisionamento, atualizar e desabilitar o usuário atribuído com base em contas em Cerner Central atribuição de usuário e grupo no AD do Azure.

> [!TIP]
> Você também pode escolher tooenabled baseado no SAML SSO Cerner centrais, seguindo instruções Olá fornecidas no [portal do Azure (https://portal.azure.com). O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares. Para obter mais informações, consulte Olá [tutorial do logon único centro Cerner](active-directory-saas-cernercentral-tutorial.md).


### <a name="tooconfigure-automatic-user-account-provisioning-toocerner-central-in-azure-ad"></a>conta de usuário automático tooconfigure provisionamento tooCerner Central no AD do Azure:


Em ordem tooprovision usuário contas tooCerner Central, será necessário toorequest uma conta do sistema Cerner Central de Cerner e gerar um token de portador OAuth que o AD do Azure pode usar o ponto de extremidade do tooconnect tooCerner SCIM. Também é recomendável que a integração Olá executada em um ambiente de área restrita Cerner antes de implantar tooproduction.

1.  Olá primeira etapa é tooensure pessoas de saudação Gerenciando Olá Cerner e integração do AD do Azure tem uma conta de CernerCare, que é necessário tooaccess Olá documentação toocomplete necessário Olá instruções. Se necessário, use Olá URLs abaixo toocreate CernerCare contas em cada ambiente aplicável.

   * Área restrita: https://sandboxcernercare.com/accounts/create

   * Produção:  https://cernercare.com/accounts/create  

2.  Em seguida, será necessário criar uma conta do sistema para o Azure AD. Use as instruções de saudação abaixo toorequest uma conta do sistema para seus ambientes de produção e de área restrita.

   * Instruções:  https://wiki.ucern.com/display/CernerCentral/Requesting+A+System+Account

   * Área restrita: https://sandboxcernercentral.com/system-accounts/

   * Produção:  https://cernercentral.com/system-accounts/

3.  Em seguida, gere um token de portador OAuth para cada uma de suas contas do sistema. toodo isso, siga Olá as instruções abaixo.

   * Instruções: https://wiki.ucern.com/display/public/reference/Accessing+Cerner%27s+Web+Services+Using+A+System+Account+Bearer+Token

   * Área restrita: https://sandboxcernercentral.com/system-accounts/

   * Produção:  https://cernercentral.com/system-accounts/

4. Finalmente, você precisa tooacquire usuário lista Realm IDs para ambos os ambientes de área restrita e de produção de hello na configuração de saudação do Cerner toocomplete. Para obter informações sobre como tooacquire isso, consulte: https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+SCIM. 

5. Agora você pode configurar tooCerner de contas de usuário do AD do Azure tooprovision. Entrar toohello [portal do Azure](https://portal.azure.com)e procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.

6. Se você já tiver configurado Cerner Central para o logon único, pesquisa de sua instância do Cerner Central usando o campo de pesquisa de saudação. Caso contrário, selecione **adicionar** e procure **Cerner Central** na Galeria de aplicativo hello. Selecione Cerner Central Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.

7.  Selecione a instância do Cerner Central, selecione Olá **provisionamento** guia.

8.  Saudação de conjunto **modo de provisionamento** muito**automática**.

   ![Provisionamento do Cerner Central](./media/active-directory-saas-cernercentral-provisioning-tutorial/Cerner.PNG)

9.  Preencha Olá seguintes campos em **credenciais de administrador**:

   * Em Olá **URL do locatário** campo, digite uma URL no formato Olá abaixo, substituindo "Lista-Realm-ID de usuário" com a ID do território Olá você copiou na etapa &#4;.

> Área restrita: https://user-roster-api.sandboxcernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

> Produção: https://user-roster-api.cernercentral.com/scim/v1/Realms/User-Roster-Realm-ID/ 

   * Em Olá **segredo do Token** campo, insira o token de portador OAuth Olá gerado na etapa &#3; e clique em **Conexão de teste**.

   * Você verá uma notificação de êxito no lado de superiordireito de saudação do seu portal.

10. Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a saudação de caixa de seleção abaixo.

11. Clique em **Salvar**. 

12. Em Olá **mapeamentos de atributo** seção, examine o usuário hello e toobe de atributos de grupo sincronizado do AD do Azure tooCerner Central. Olá atributos selecionados como **correspondência** propriedades são usados toomatch Olá as contas de usuário e grupos no Centro de Cerner para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.

13. tooenable Olá serviço de provisionamento do AD do Azure Cerner centrais, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção

14. Clique em **Salvar**. 

Isso inicia a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos tooCerner Central, na seção usuários e grupos de saudação. a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde Olá serviço de provisionamento do AD do Azure está em execução. Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo Cerner Central.

Para obter mais informações sobre como o provisionamento de saudação do AD do Azure tooread registra, consulte [relatórios sobre o provisionamento de conta de usuário automático](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).

## <a name="additional-resources"></a>Recursos adicionais

* [Cerner Central: Publicação de dados de identidade usando o Azure AD](https://wiki.ucern.com/display/public/reference/Publishing+Identity+Data+Using+Azure+AD)
* [Tutorial: Configurar o Cerner Central para logon único com o Azure Active Directory](active-directory-saas-cernercentral-tutorial.md)
* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-enterprise-apps-manage-provisioning.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Próximas etapas
* [Saiba como tooreview registra e obter relatórios sobre a atividade de provisionamento](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).
