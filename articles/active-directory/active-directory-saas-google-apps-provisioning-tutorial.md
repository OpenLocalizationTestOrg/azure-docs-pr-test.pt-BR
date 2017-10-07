---
title: "Tutorial: Configurando o Google Apps para o provisionamento automático de usuário no Azure | Microsoft Docs"
description: "Saiba como contas de usuário de provisionar e provisionar eliminação de tooautomatically do AD do Azure tooGoogle aplicativos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6dbd50b5-589f-4132-b9eb-a53a318a64e5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: d1fa8449bd6013d1627b3552aaa19db1c0f4f46f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-google-apps-for-automatic-user-provisioning"></a>Tutorial: Configurando o Google Apps para o provisionamento automático de usuário

Olá objetivo deste tutorial é tooshow que Olá etapas necessárias tooperform no Google Apps e o Azure AD provisão de tooautomatically e desprovisionar contas de usuário do AD do Azure tooGoogle aplicativos.

## <a name="prerequisites"></a>Pré-requisitos

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

*   Um locatário do Azure Active Directory.
*   É necessário ter um locatário válido do Google Apps for Work ou do Google Apps for Education. Você pode usar uma conta de avaliação gratuita para qualquer serviço.
*   Uma conta de usuário no Google Apps com permissões de Administrador de Equipe.

## <a name="assigning-users-toogoogle-apps"></a>Atribuir usuários tooGoogle aplicativos

Active Directory do Azure usa um conceito chamado "atribuições" toodetermine quais usuários devem receber acesso tooselected aplicativos. No contexto de saudação do provisionamento de conta de usuário automático, apenas Olá usuários e grupos que foram "atribuídos" tooan aplicativo no AD do Azure está sincronizado.

Antes de configurar e habilitar Olá provisionar um serviço, é necessário toodecide quais usuários e/ou grupos no AD do Azure que representam usuários Olá que precisam acessar o aplicativo do Google Apps tooyour. Depois de decidir, você pode atribuir esses aplicativos do usuários tooyour Google Apps, seguindo as instruções de saudação aqui: [atribuir um aplicativo de enterprise tooan usuário ou grupo](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

> [!IMPORTANT]
>*   É recomendável que um único usuário do AD do Azure ser atribuído a saudação de tootest aplicativos de tooGoogle configuração de provisionamento. Outros usuários e/ou grupos podem ser atribuídos mais tarde.
>*   Ao atribuir um usuário tooGoogle aplicativos, você deve selecionar Olá usuário ou função de "Grupo" na caixa de diálogo de atribuição de saudação. função de "Acesso padrão" Hello não funciona para o provisionamento.

## <a name="enable-automated-user-provisioning"></a>Habilitar o provisionamento automatizado de usuários

Esta seção orienta você conectar-se a API de provisionamento de conta de usuário do aplicativos tooGoogle seu AD do Azure e configurar Olá toocreate do serviço de provisionamento, atualizar e desativar contas de usuário atribuído no Google Apps com base na atribuição de usuário e grupo no AD do Azure .

>[!Tip]
>Você também pode escolher tooenabled baseado no SAML SSO para o Google Apps, seguindo instruções Olá fornecidas no [portal do Azure](https://portal.azure.com). O logon único pode ser configurado independentemente do provisionamento automático, embora esses dois recursos sejam complementares.

### <a name="configure-automatic-user-account-provisioning"></a>Configurar o provisionamento automático de conta de usuário

> [!NOTE]
> Outra opção viável para automatizar o provisionamento de tooGoogle aplicativos de usuário é toouse [sincronização de diretório de aplicativos da Google (GADS)](https://support.google.com/a/answer/106368?hl=en) que provisiona seu tooGoogle de identidades do Active Directory local aplicativos. Por outro lado, a solução Olá neste tutorial provisiona usuários do Active Directory do Azure (nuvem) e grupos habilitados para email tooGoogle aplicativos. 

1. O logon no hello [Console de administração do Google Apps](http://admin.google.com/) usando sua conta de administrador e, em seguida, clique em **segurança**. Se você não vir o link hello, podem estar ocultos em Olá **mais controles** menu na parte inferior de saudação da tela hello.
   
    ![Clique em Segurança.][10]

2. Em Olá **segurança** , clique em **referência da API**.
   
    ![Clique em Referência de API.][15]

3. Selecione **Habilitar o acesso à API**.
   
    ![Clique em Referência de API.][16]

    > [!IMPORTANT]
    > Para cada usuário que você pretende tooprovision tooGoogle aplicativos, seu nome de usuário no Active Directory do Azure *deve* ser domínio personalizado tooa associado. Por exemplo, nomes de usuários parecidos com bob@contoso.onmicrosoft.com não são aceitos pelo Google Apps, enquanto bob@contoso.com é aceito. É possível alterar o domínio de um usuário existente editando as propriedades dele no AD do Azure. Instruções de como tooset um domínio personalizado para o Active Directory do Azure e o Google Apps inclusos nos seguintes etapas.
      
4. Se você ainda não adicionou um nome de domínio personalizado tooyour Active Directory do Azure, siga Olá etapas a seguir:
  
    a. Em Olá [portal do Azure](https://portal.azure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**. Na lista de diretório hello, selecione seu diretório. 

    b. Clique em **nome dos domínios** Olá painel de navegação esquerdo e, em seguida, clique em **adicionar**.
     
     ![domínio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_1.png)

     ![adição de domínio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_2.png)

    c. Digite seu nome de domínio em Olá **nome de domínio** campo. Esse nome de domínio deve ser Olá mesmo nome de domínio que você pretende toouse Google Apps. Quando estiver pronto, clique em Olá **Adicionar domínio** botão.
     
     ![nome de domínio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_3.png)

    d. Clique em **próximo** toogo página de verificação de toohello. tooverify que você possui este domínio, você deve editar registros DNS do domínio de saudação de acordo com os valores de toohello fornecidos nessa página. Você pode escolher tooverify usando **registros MX** ou **registros TXT**, dependendo do que você selecionar Olá **tipo de registro** opção. Para obter instruções mais abrangentes sobre como nome de domínio de tooverify com o AD do Azure, consulte [adicionar seu próprio nome de domínio tooAzure AD](https://go.microsoft.com/fwLink/?LinkID=278919&clcid=0x409).
     
     ![domínio](./media/active-directory-saas-google-apps-provisioning-tutorial/domain_4.png)

    e. Repita Olá etapas para todos os domínios de saudação que você pretende tooadd tooyour directory anteriores.

5. Agora que você confirmou todos os domínios com o Azure AD, agora deve confirmá-los novamente com o Google Apps. Para cada domínio que já não está registrado com o Google Apps, execute Olá etapas a seguir:
   
    a. Em Olá [Console de administração do Google Apps](http://admin.google.com/), clique em **domínios**.
     
     ![Clique em Domínios][20]

    b. Clique em **Adicionar um domínio ou um alias de domínio**.
     
     ![Adicione um novo domínio][21]

    c. Selecione **adicionar outro domínio**e digite o nome de saudação do domínio Olá que deseja tooadd.
     
     ![Digite o nome de domínio][22]

    d. Clique em **Continuar e confirmar a propriedade do domínio**. Siga Olá tooverify de etapas que você possui o nome de domínio de saudação. Para obter instruções abrangentes sobre como tooverify seu domínio com o Google Apps, consulte. [Confirmar a propriedade do site com o Google Apps](https://support.google.com/webmasters/answer/35179).

    e. Repita Olá etapas para todos os domínios adicionais que você pretende tooadd tooGoogle aplicativos anteriores.
     
     > [!WARNING]
     > Se você alterar domínio primário Olá para seu locatário do Google Apps, e se você já tiver configurado o logon único com o Azure AD, você tem toorepeat etapa #3 em [etapa 2: Habilitar logon único](#step-two-enable-single-sign-on).
       
6. Em Olá [Console de administração do Google Apps](http://admin.google.com/), clique em **funções de administrador**.
   
     ![Clique em Google Apps][26]

7. Determine qual administrador de conta que você deseja que o provisionamento de usuário toomanage toouse. Para Olá **função admin** dessa conta, editar Olá **privilégios** para essa função. Verifique se ele tem todos os Olá **privilégios de API de administração** habilitado para que essa conta pode ser usada para provisionamento.
   
     ![Clique em Google Apps][27]
   
    > [!NOTE]
    > Se você estiver configurando um ambiente de produção, Olá melhor prática é toocreate uma conta de administrador no Google Apps especificamente para essa etapa. Essas contas devem ter associada a ele uma função de administrador que tem os privilégios necessários API hello.
     
8. Em Olá [portal do Azure](https://portal.azure.com), procurar toohello **Active Directory do Azure > aplicativos da empresa > todos os aplicativos** seção.

9. Se você já tiver configurado o Google Apps para o logon único, procure sua instância do usando o campo de pesquisa de saudação do Google Apps. Caso contrário, selecione **adicionar** e procure **Google Apps** na Galeria de aplicativo hello. Selecione o Google Apps Olá dos resultados da pesquisa e adicioná-lo tooyour lista de aplicativos.

10. Selecione sua instância do Google Apps e selecione Olá **provisionamento** guia.

11. Saudação de conjunto **modo de provisionamento** muito**automática**. 

     ![provisionamento](./media/active-directory-saas-google-apps-provisioning-tutorial/provisioning.png)

12. Em Olá **credenciais de administrador** seção, clique em **autorizar**. Isso abre uma caixa de diálogo de autorização do Google Apps em uma nova janela do navegador.

13. Confirme que deseja toogive Active Directory do Azure toomake as alterações de permissão de locatário tooyour Google Apps. Clique em **Aceitar**.
    
     ![Confirme permissões.][28]

14. No portal do Azure de Olá, clique em **Conexão de teste** tooensure AD do Azure pode se conectar a aplicativos do Google Apps tooyour. Se a conexão de saudação falhar, certifique-se de que sua conta do Google Apps tem permissões de administrador de equipe e tente Olá **"Autorizar"** etapa novamente.

15. Digite hello endereço de email de uma pessoa ou grupo que deve receber notificações de erros de provisionamento no hello **Email de notificação** campo e verificar a caixa de seleção de saudação.

16. Clique em **Salvar.**

17. Em Olá mapeamentos, selecione **sincronizar do Azure Active Directory Users tooGoogle aplicativos.**

18. Em Olá **mapeamentos de atributo** seção, revise os atributos de usuário de saudação que são sincronizados do AD do Azure tooGoogle aplicativos. Olá atributos selecionados como **correspondência** propriedades são contas de usuário de saudação toomatch usado no Google Apps para operações de atualização. Selecione Olá toocommit de botão de salvar as alterações.

19. tooenable Olá serviço de provisionamento do AD do Azure para Google Apps, alteração Olá **Status de provisionamento** muito**em** na seção configurações da saudação

20. Clique em **Salvar.**

Iniciar a sincronização inicial de saudação de todos os usuários e/ou grupos atribuídos aplicativos tooGoogle na seção usuários e grupos de saudação. a sincronização inicial Olá leva tooperform mais que as sincronizações subsequentes, que ocorrem aproximadamente a cada 20 minutos desde que o serviço hello está sendo executado. Você pode usar o hello **detalhes de sincronização** seção toomonitor progresso e execute os relatórios de atividade tooprovisioning links, que descrevem todas as ações executadas pelo Olá provisionar um serviço em seu aplicativo do Google Apps.

## <a name="additional-resources"></a>Recursos adicionais

* [Gerenciamento do provisionamento de conta de usuário para Aplicativos Empresariais](active-directory-saas-tutorial-list.md)
* [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Configurar Logon Único](active-directory-saas-google-apps-tutorial.md)



<!--Image references-->

[10]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-security.png
[15]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-api-enabled.png
[20]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-add-another.png
[24]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-provisioning-tutorial/gapps-auth.png