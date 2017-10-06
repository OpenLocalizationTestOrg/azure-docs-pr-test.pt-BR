---
title: "Tutorial: integração do Azure Active Directory ao Benefitsolver | Microsoft Docs"
description: "Saiba como toouse Benefitsolver com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a>Tutorial: Integração do Active Directory do Azure ao Benefitsolver
Olá objetivo deste tutorial é a integração do Azure e Benefitsolver Olá tooshow.  

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

* Uma assinatura válida do Azure
* Uma assinatura habilitada para logon único (SSO) do Benefitsolver

Após concluir este tutorial, os usuários de saudação do Azure AD atribuídos tooBenefitsolver será toosingle capaz de usar o logon no aplicativo hello usando Olá [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:

1. Habilitando a integração de aplicativos de saudação para Benefitsolver
2. Configuração do SSO (logon único)
3. Configurando o provisionamento de usuários
4. Atribuindo usuários

![Cenário](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Cenário")

## <a name="enabling-hello-application-integration-for-benefitsolver"></a>Habilitando a integração de aplicativos de saudação para Benefitsolver
Olá objetivo desta seção é toooutline como integração de aplicativos de saudação tooenable para Benefitsolver.

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a>integração de aplicativos de saudação tooenable para Benefitsolver, execute Olá etapas a seguir:
1. No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
   ![Aplicativos](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Aplicativos")
4. Clique em **adicionar** final Olá Olá página.
   
   ![Adicionar aplicativo](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Adicionar aplicativo")
5. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo da Galeria Olá**.
   
   ![Adicionar um aplicativo da galeria](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Adicionar um aplicativo da galeria")
6. Em Olá **caixa de pesquisa**, tipo **Benefitsolver**.
   
   ![Galeria de Aplicativos](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Galeria de Aplicativos")
7. No painel de resultados de saudação, selecione **Benefitsolver**e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
   ![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")
   
## <a name="configure-single-sign-on"></a>Configurar o logon único

Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooBenefitsolver com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.  

Seu aplicativo de Benefitsolver espera asserções SAML de saudação em um formato específico, o que exige que você tooyour de mapeamentos de atributo personalizado tooadd **atributos de tokens saml** configuração. 

Olá captura de tela a seguir mostra um exemplo.

![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Atributos")

**tooconfigure o logon único, execute Olá etapas a seguir:**

1. Em Olá portal clássico do Azure, em Olá **Benefitsolver** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.
   
   ![Configurar Logon Único](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configurar Logon Único")
2. Em Olá **como você gostaria usuários toosign em tooBenefitsolver** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.
   
   ![Configurar Logon Único](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configurar Logon Único")
3. Em Olá **definir configurações de aplicativo** página, execute Olá etapas a seguir:
   
   ![Definir Configurações de Aplicativo](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Definir Configurações de Aplicativo")
   
   1. Em Olá **URL de logon** caixa de texto, tipo **http://azure.benefitsolver.com**.
   2. Em Olá **URL de resposta** caixa de texto, tipo **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.  
   3. Clique em **Avançar**.
4. Em Olá **configurar logon único no Benefitsolver** página, toodownload seus metadados, clique em **baixar metadados**e, em seguida, salve o arquivo de metadados de saudação localmente no seu computador.
   
   ![Configurar Logon Único](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configurar Logon Único")
5. Envie a equipe de suporte do hello baixado metadados arquivo tooyour Benefitsolver.
   
   >[!NOTE]
   >Sua equipe de suporte Benefitsolver tem toodo Olá configuração real do SSO. Você receberá uma notificação quando o SSO tiver sido habilitado para sua assinatura.
   >

6. Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.
   
   ![Configurar Logon Único](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configurar Logon Único")
7. No menu de saudação na parte superior de saudação, clique em **atributos** tooopen Olá **atributos de tokens SAML** caixa de diálogo.
   
   ![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Atributos")
8. mapeamentos de atributo do tooadd Olá necessária, execute Olá etapas a seguir:
   
   ![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Atributos")
   
   | Nome do atributo | Valor do atributo |
   | --- | --- |
   | ClientID |É necessário tooget esse valor de sua equipe de suporte de Benefitsolver. |
   | ClientKey |É necessário tooget esse valor de sua equipe de suporte de Benefitsolver. |
   | LogoutURL |É necessário tooget esse valor de sua equipe de suporte de Benefitsolver. |
   | EmployeeID |É necessário tooget esse valor de sua equipe de suporte de Benefitsolver. |
   
   1. Para cada linha de dados na tabela de saudação acima, clique em **Adicionar atributo de usuário**.
   2. Em Olá **nome do atributo** caixa de texto, nome de atributo do tipo hello mostrado para aquela linha.
   3. Em Olá **o valor do atributo** texto, o valor do atributo select Olá mostrado para aquela linha.
   4. Clique em **Concluído**.
9. Clique em **Aplicar alterações**.

## <a name="configure-user-provisioning"></a>Configurar provisionamento do usuário
Em ordem tooenable AD do Azure usuários toolog em Benefitsolver, eles devem ser provisionados no Benefitsolver.  

No caso de saudação de Benefitsolver, dados de funcionário estão em seu aplicativo preenchido por meio de um arquivo de censo do seu sistema HRIS (geralmente à noite).  

>[!NOTE]
>Você pode usar qualquer ferramenta de criação outros Benefitsolver usuário conta ou APIs fornecidas pelo Benefitsolver tooprovision contas de usuário do AAD. 
> 

## <a name="assigning-users"></a>Atribuindo usuários
tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a>tooassign usuários tooBenefitsolver, executar Olá etapas a seguir:
1. No hello portal clássico do Azure, crie uma conta de teste.
2. Em hello * * Benefitsolver * * página de integração de aplicativos, clique em **atribuir usuários**.
   
   ![Atribuir Usuários](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Atribuir Usuários")
3. Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.
   
   ![Sim](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Sim")

Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso. Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).

