---
title: "Tutorial: integração do Azure Active Directory ao Concur | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: df47f55f-a894-4e01-a82e-0dbf55fc8af1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 13ba364af26a5ce0f1d2b51aaa0f84a4c353b107
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-concur-for-user-provisioning"></a>Tutorial: configurar o Concur para provisionamento de usuário

Olá objetivo deste tutorial é tooshow Olá etapas precisam tooperform no Concur e o Azure AD tooautomatically provisionar e provisionamento de contas de usuário do AD do Azure tooConcur.

## <a name="prerequisites"></a>Pré-requisitos

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

*   Um locatário do Azure Active Directory.
*   Uma assinatura habilitada para logon único do Concur.
*   Uma conta de usuário no Concur com permissões de Administrador de Equipe.

## <a name="assigning-users-tooconcur"></a>Atribuir usuários tooConcur

Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos. No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.

Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure representam Olá usuários precisam acessar tooyour Concur aplicativo. Depois de decidir, você pode atribuir esses aplicativos de Concur tooyour usuários, seguindo as instruções de saudação aqui:

[Atribuir um aplicativo de enterprise tooan usuário ou grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooconcur"></a>Dicas importantes para atribuir usuários tooConcur

*   É recomendável que um único usuário do AD do Azure receberá tooConcur tootest Olá configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.

*   Ao atribuir um usuário tooConcur, você deve selecionar uma função de usuário válido. função de "Acesso padrão" Hello não funciona para o provisionamento.

## <a name="enable-user-provisioning"></a>Permitir provisionamento do usuário

Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do tooConcur seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no Concur com base na atribuição de usuário e grupo no AD do Azure.

> [!Tip] 
> Você também pode escolher tooenabled baseado no SAML SSO para Concur, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com). O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.

### <a name="tooconfigure-user-account-provisioning"></a>provisionamento de conta de usuário de tooconfigure:

Olá o objetivo desta seção é toooutline como tooenable provisionamento de usuário do Active Directory contas tooConcur.

aplicativos tooenable Olá serviço de despesas, é toobe configuração e uso apropriados de um perfil de administrador de serviço da Web. Não adicione Olá administrador WS função tooyour perfil de administrador existente que você usa para funções administrativas T & E.

Os consultores concur ou administrador de saudação do cliente deve criar um perfil de administrador de serviços Web distinto e administrador de saudação do cliente deve usar esse perfil para as funções de administrador de serviços Web da saudação (por exemplo, a habilitação de aplicativos). Esses perfis devem ser mantidos separados de diário T & E perfil de administrador do administrador do cliente Olá (Olá T & perfil de administrador E não devem ter função de administrador de serviços Web hello atribuída).

Ao criar Olá perfil toobe usado para habilitar o aplicativo hello, insira o nome do administrador do cliente de saudação em campos de perfil de usuário de saudação. Isso atribuirá o perfil de toohello de propriedade. Depois de criar um ou mais perfis, cliente Olá deve fazer logon com essa Olá tooclick de perfil "*habilitar*" botão para um aplicativo parceiro no menu de serviços Web hello.

Para Olá motivos a seguir, essa ação não deve ser feita com perfil Olá usam para administração T & E normal.

* Olá cliente tiver toobe Olá que clica em "*Sim*" na janela de caixa de diálogo de saudação é exibida depois que um aplicativo está habilitado. Esse clique confirma que o cliente Olá é disposto para Olá parceiro aplicativo tooaccess seus dados, para que você ou hello parceiro não é possível clicar botão Sim.

* Se um administrador do cliente que habilitou um aplicativo usando Olá T & perfil de administrador E deixa a empresa hello (resultando em perfil hello está sendo desativado), quaisquer aplicativos habilitados usando o perfil não funcionará até que o aplicativo hello está habilitado com outro administrador WS active perfil. É por isso devem toocreate distintos perfis de administrador de serviços Web.

* Se um administrador deixa a empresa Olá, nome de saudação associada toohello perfil de administrador de serviços Web pode ser o administrador de substituição de toohello alterados se desejar sem afetar a saudação habilitada aplicativo desativado porque não é necessário que esse perfil.

**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**

1. Faça logon no tooyour **Concur** locatário.

2. De saudação **administração** menu, selecione **serviços Web**.
   
    ![Locatário do Concur](./media/active-directory-saas-concur-provisioning-tutorial/IC721729.png "Locatário do Concur")

3. Em Olá deixados de lado, da saudação **serviços Web** painel, selecione **habilitar aplicativo parceiro**.
   
    ![Habilitar Aplicativo do Parceiro](./media/active-directory-saas-concur-provisioning-tutorial/ic721730.png "Habilitar Aplicativo do Parceiro")

4. De saudação **habilitar aplicativo** lista, selecione **Active Directory do Azure**e, em seguida, clique em **habilitar**.
   
    ![Microsoft Azure Active Directory](./media/active-directory-saas-concur-provisioning-tutorial/ic721731.png "Microsoft Azure Active Directory")

5. Clique em **Sim** tooclose Olá **Confirmar ação** caixa de diálogo.
   
    ![Confirmar Ação](./media/active-directory-saas-concur-provisioning-tutorial/ic721732.png "Confirmar Ação")

6. Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.

7. Se você já tiver configurado o Concur para SSO, procure sua instância do Concur usando o campo de pesquisa de saudação. Caso contrário, selecione **adicionar** e procure **Concur** na Galeria de aplicativo hello. Selecione Concur Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.

8. Selecione sua instância do Concur e selecione Olá **provisionamento** guia.

9. Saudação de conjunto **modo de provisionamento** muito**automática**. 
 
    ![provisionamento](./media/active-directory-saas-concur-provisioning-tutorial/provisioning.png)

10. Em Olá **credenciais de administrador** seção, digite Olá **nome de usuário** e hello **senha** do administrador do Concur.

11. No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a tooyour Concur aplicativo. Se a conexão de saudação falhar, certifique-se de que sua conta Concur tem permissões de administrador de equipe.

12. Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a caixa de seleção de saudação.

13. Clique em **Salvar.**

14. Em Olá mapeamentos, selecione **tooConcur sincronizar Azure usuários do Active Directory.**

15. Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do tooConcur do AD do Azure. Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no Concur para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.

16. tooenable Olá serviço de provisionamento do AD do Azure para Concur, alteração Olá **Status de provisionamento** muito**na** em Olá **configurações** seção

17. Clique em **Salvar.**

Agora você pode criar uma conta de teste. Aguarde a minutos too20 tooverify Olá conta foi sincronizada tooConcur.

## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Logon Único](active-directory-saas-concur-tutorial.md)

