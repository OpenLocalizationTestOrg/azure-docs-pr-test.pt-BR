---
title: "Tutorial: integração do Azure Active Directory com a Área Restrita do Salesforce | Microsoft Docs"
description: "Saiba como toouse área restrita do Salesforce com o Active Directory do Azure tooenable única de logon, o provisionamento automatizado e muito mais!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: ee54c39e-ce20-42a4-8531-da7b5f40f57c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: deccd6a07b57c8ba56b7e1c3f3ab311813ca017b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce-sandbox"></a>Tutorial: Integração do Active Directory do Azure com a Área Restrita Salesforce

Olá objetivo deste tutorial é tooshow integração de saudação do Azure e a área restrita do Salesforce.  

>[!TIP]
>Comentários, consulte Olá [página de suporte do Azure](http://go.microsoft.com/fwlink/?LinkId=521878). 
> 

Forneça as áreas restritas Olá capacidade toocreate várias cópias de sua organização em ambientes separados para uma variedade de propósitos, como desenvolvimento, teste e treinamento, sem comprometer Olá dados e aplicativos em sua equipe de vendas de produção organização.  

Para obter mais detalhes, confira [Visão geral da área restrita](https://help.salesforce.com/HTViewHelpDoc?id=create_test_instance.htm&language=en_US)

cenário de saudação descrito neste tutorial presume que você já tenha Olá itens a seguir:

* Uma assinatura válida do Azure
* Uma área restrita no Salesforce.com

Se você ainda não tem uma área restrita válida no Salesforce.com, será necessário toocontact Salesforce.

cenário de saudação descrito neste tutorial consiste em Olá blocos de construção a seguir:

1. Habilitando Olá integração de aplicativos de área restrita do Salesforce
2. Configuração do SSO (logon único)
3. Habilitando seu domínio
4. Configurando o provisionamento de usuários
5. Atribuindo usuários

![Cenário](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769571.png "Cenário")

## <a name="enable-hello-application-integration-for-salesforce-sandbox"></a>Habilitar a integração de área restrita do Salesforce aplicativos Olá
Olá objetivo desta seção é toooutline como tooenable Olá integração de área restrita do Salesforce.

**tooenable Olá integração de área restrita do Salesforce, execute Olá etapas a seguir:**

1. No hello portal clássico do Azure, no painel de navegação esquerdo hello, clique em **do Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700993.png "Active Directory")
2. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
3. Clique em exibição de aplicativos tooopen hello, no modo de exibição de diretório Olá, **aplicativos** no menu superior hello.
   
   ![Aplicativos](./media/active-directory-saas-salesforce-sandbox-tutorial/IC700994.png "Aplicativos")
4. Olá tooopen **Galeria de aplicativos**, clique em **adicionar um aplicativo**e, em seguida, clique em **adicionar um aplicativo para minha organização toouse**.
   
   ![O que fazer você deseja toodo? ] (./media/active-directory-saas-salesforce-sandbox-tutorial/IC700995.png "o que fazer você deseja toodo?")
5. Em Olá **caixa de pesquisa**, tipo **área restrita do Salesforce**.
   
   ![Galeria de Aplicativos](./media/active-directory-saas-salesforce-sandbox-tutorial/IC710978.png "Galeria de Aplicativos")
6. No painel de resultados de saudação, selecione **área restrita do Salesforce**e, em seguida, clique em **concluir** aplicativo hello de tooadd.
   
   ![Área restrita do SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746474.png "Área restrita do Salesforce")
   
## <a name="configur-single-sign-on-sso"></a>Configurar o SSO (logon único)

Olá objetivo desta seção é toooutline como tooenable usuários tooauthenticate tooSalesforce com suas contas no AD do Azure usando federação com base no protocolo SAML de saudação.

**tooconfigure o logon único, execute Olá etapas a seguir:**

1. Em Olá portal clássico do Azure, em Olá **área restrita do Salesforce** página de integração de aplicativos, clique em **configurar logon único** tooopen Olá **configurar logon único** caixa de diálogo.
   
   ![Configurar logon único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC749323.png "Configurar logon único")
2. Em Olá **como você gostaria toosign usuários em área restrita do tooSalesforce** página, selecione **AD do Microsoft Azure Single Sign-On**e, em seguida, clique em **próximo**.
   
   ![Área restrita do SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746479.png "Área restrita do Salesforce")
3. Em Olá **configurar URL do aplicativo** página Olá **URL de logon** caixa de texto, digite sua URL usando o saudação padrão a seguir `http://company.my.salesforce.com`e, em seguida, clique em **próximo**.
   
   ![Configurar URL do Aplicativo](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781022.png "Configurar URL do Aplicativo")
4. Se você já tiver configurado logon único para outra instância de área restrita do Salesforce em seu diretório, você também deve configurar Olá **identificador** toohave Olá mesmo valor Olá **URL de entrada**. 
 * Olá **identificador** campo pode ser encontrado verificando Olá **Mostrar configurações avançadas** caixa de seleção na Olá **configurar URL do aplicativo** página da caixa de diálogo de saudação.
5. Em Olá **configurar logon único no Salesforce Sandbox** , clique em **Download certificado**e, em seguida, salve o arquivo de certificado de saudação em seu computador.
   
   ![Configurar Logon Único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781023.png "Configurar Logon Único")
6. Em outra janela do navegador da Web, faça logon em sua área restrita Salesforce como um administrador.
7. No menu de saudação na parte superior de saudação, clique em **instalação**.
   
   ![Configuração](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781024.png "Configuração")
8. No painel de navegação Olá Olá esquerda, clique em **controles de segurança**e, em seguida, clique em **configurações de logon único**.
   
   ![Configurações de Logon Único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781025.png "Configurações de Logon Único")
9. Na seção configurações de logon único do hello, execute Olá etapas a seguir:
   
   ![Configurações de Logon Único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781026.png "Configurações de Logon Único")  
 1.  Selecione **SAML Habilitado**. 
 2.  Clique em **Novo**.
10. Na seção configurações de logon único SAML do hello, execute Olá etapas a seguir:
    
    ![Configurações de Logon Único do SAML](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781027.png "Configurações de Logon Único do SAML")  
 1. Na caixa de texto de nome hello, digite o nome de saudação da configuração de saudação (por exemplo: *SPSSOWAAD\_teste*). 
 2. Em Olá portal clássico do Azure, em Olá **configurar logon único no Salesforce Sandbox** página da caixa de diálogo, Olá cópia **URL do emissor** valor e, em seguida, cole-o em Olá **emissor**caixa de texto.
 3. Em Olá **Id da entidade** caixa de texto, tipo **https://test.salesforce.com** se Olá primeira instância de área restrita do Salesforce que você está adicionando tooyour directory. Se você já tiver adicionado uma instância de área restrita do Salesforce, em seguida, para Olá **ID da entidade** tipo no hello **URL de logon**, que deveriam estar neste formato:`http://company.my.salesforce.com`   
 4. Clique em **procurar** Olá tooupload baixado o certificado.  
 5. Como **tipo de identidade SAML**, selecione **asserção contém Olá ID de Federação do objeto de usuário Olá**. 
 6. Como **local da identidade do SAML**, selecione **identidade está no elemento NameIdentifier Olá Olá declaração assunto**.
 7. Em Olá portal clássico do Azure, em Olá **configurar logon único no Salesforce Sandbox** página da caixa de diálogo, Olá cópia **URL de logon remoto** valor e, em seguida, cole-o em Olá **provedor de identidade URL de logon** caixa de texto. 
 8. O SFDC não dá suporte a logout SAML.  Como alternativa, cole 'https://login.microsoftonline.com/common/wsfederation?wa=wsignout1.0'-o na Olá **URL de Logout do provedor de identidade** caixa de texto.
 9. Para **Associação de Solicitação Iniciada pelo Provedor de Serviços**, selecione **HTTP Post**. 
 10. Clique em **Salvar**.
11. Em Olá portal clássico do Azure, selecione a confirmação de configuração de logon único do hello e, em seguida, clique em **concluir** tooclose Olá **configurar logon único** caixa de diálogo.
    
    ![Configurar Logon Único](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781028.png "Configurar Logon Único")

## <a name="enable-your-domain"></a>Habilitar seu domínio
Esta seção pressupõe que você já tenha criado um domínio.  Para obter mais detalhes, confira [Definindo seu nome de domínio](https://help.salesforce.com/HTViewHelpDoc?id=domain_name_define.htm&language=en_US).

**tooenable seu domínio, executar Olá etapas a seguir:**

1. No painel de navegação esquerdo hello, clique em **gerenciamento de domínio**e, em seguida, clique em **meu domínio.**
   
   ![Meu Domínio](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781029.png "Meu Domínio")
   
   >[!NOTE]
   >Verifique se o domínio foi configurado corretamente. 
   > 
2. Em Olá **configurações de página de logon** seção, clique em **editar**, em seguida, como **serviço de autenticação**, selecione nome de saudação do hello configuração de logon único SAML de saudação anterior seção e, finalmente, clique em **salvar**.
   
   ![Meu Domínio](./media/active-directory-saas-salesforce-sandbox-tutorial/IC781030.png "Meu Domínio")

Assim que você tiver um domínio configurado, seus usuários devem usar a área restrita do Salesforce Olá domínio URL toologin toohello.  

valor tooget Olá Olá URL, clique em perfil Olá SSO que você criou na seção anterior hello.

## <a name="configure-user-provisioning"></a>Configurar provisionamento do usuário
Olá o objetivo desta seção é toooutline como tooenable o provisionamento de usuário do usuário do Active Directory contas tooSalesforce área restrita.

**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**

1. No portal do Salesforce hello, na barra de navegação superior hello, selecione seu nome tooexpand seu menu de usuário:
   
   ![Minhas configurações](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698773.png "Minhas configurações")
2. No seu menu de usuário, selecione **minhas configurações** tooopen sua **minhas configurações** página.
3. No painel esquerdo do hello, clique em **pessoal** tooexpand Olá seção pessoal e, em seguida, clique em **redefinir meu Token de segurança**:
   
   ![Minhas configurações](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698774.png "Minhas configurações")
4. Em Olá **redefinir meu Token de segurança** , clique em **redefinir Token de segurança** toorequest um email que contém o token de segurança do Salesforce.com.
   
   ![Novo Token](./media/active-directory-saas-salesforce-sandbox-tutorial/IC698776.png "Novo token")
5. Marque a caixa de entrada de um email do Salesforce.com usando "**confirmação de segurança de salesforce.com.com**" como o assunto.
6. Revise este valor de token de segurança cópia e de email, para o hello.
7. Em Olá portal clássico do Azure, em Olá **área restrita do salesforce** página de integração de aplicativos, clique em **configurar provisionamento de usuário** tooopen Olá **configurar provisionamento do usuário**caixa de diálogo.
   
   ![Configurar provisionamento do usuário](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769573.png "configurar provisionamento do usuário")
8. Em Olá **Insira sua área restrita do Salesforce credenciais tooenable provisionamento automático de usuário** , forneça Olá definições de configuração a seguir:
   
   ![Área restrita do SalesForce](./media/active-directory-saas-salesforce-sandbox-tutorial/IC746476.png "Área restrita do Salesforce")   
 1. Em Olá **nome de usuário de administrador de área restrita do Salesforce** caixa de texto, tipo de uma área restrita do Salesforce nome de conta que tem Olá **administrador do sistema** perfil em Salesforce.com atribuído.
 2. Em Olá **senha do administrador do Salesforce Sandbox** caixa de texto, digite a senha Olá para esta conta.
 3. Em Olá **o Token de segurança do usuário** texto, o valor do token de segurança do hello colar.
 4. Clique em **validar** tooverify sua configuração.
 5. Clique em Olá **próximo** saudação do botão tooopen **confirmação** página.
9. Em Olá **confirmação** , clique em **concluir** toosave sua configuração.
   
## <a name="assigning-users"></a>Atribuindo usuários

tootest sua configuração, você precisa toogrant usuários de saudação do AD do Azure que você deseja tooallow usando seu tooit de acesso do aplicativo, atribuindo a eles.

**tooassign usuários tooSalesforce área restrita, execute Olá etapas a seguir:**

1. No hello portal clássico do Azure, crie uma conta de teste.
2. Em hello * * área restrita do Salesforce * * página de integração de aplicativos, clique em **atribuir usuários**.
   
   ![Atribuir usuários](./media/active-directory-saas-salesforce-sandbox-tutorial/IC769574.png "Atribuir usuários")
3. Selecione seu usuário de teste, clique em **atribuir**e, em seguida, clique em **Sim** tooconfirm sua atribuição.
   
   ![Sim](./media/active-directory-saas-salesforce-sandbox-tutorial/IC767830.png "Sim")

Agora você deve aguardar 10 minutos e verificar se a conta Olá foi sincronizada tooSalesforce área restrita.

Se você quiser tootest suas configurações de SSO, abra Olá painel de acesso. Para obter mais detalhes sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](https://msdn.microsoft.com/library/dn308586).

