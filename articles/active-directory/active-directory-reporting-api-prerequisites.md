---
title: "Olá AD do Azure aaaPrerequisites tooaccess reporting API. | Microsoft Docs"
description: "Saiba sobre a API de relatório do hello pré-requisitos tooaccess Olá AD do Azure"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>API de relatório pré-requisitos tooaccess Olá AD do Azure
Olá [reporting APIs do AD do Azure](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) fornece acesso programático toohello dados por meio de um conjunto de APIs com base em REST. Você pode chamar essas APIs de várias ferramentas e linguagens de programação.

Olá reporting API usa [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) APIs da web do toohello tooauthorize acesso. 

tooprepare seu toohello acesso API de relatório, você deve:

1. Crie um aplicativo em seu locatário do Azure AD 
2. Grant Olá aplicativo as permissões apropriadas tooaccess Olá dados do Azure AD
3. Reúna as definições de configuração de seu diretório

Para dúvidas, problemas ou comentários, entre em contato com a [Ajuda de relatório do AAD](mailto:aadreportinghelp@microsoft.com).

## <a name="create-an-azure-ad-application"></a>Criar um aplicativo Azure AD
tooconfigure seu diretório tooaccess Olá AD do Azure reporting API, você deve entrar no toohello portal clássico do Azure com uma conta de administrador de assinatura do Azure que também é um membro da função de diretório Olá Administrador Global em seu locatário do AD do Azure.

> [!IMPORTANT]
> Aplicativos em execução sob as credenciais com privilégios de "admin" como isso podem ser muito poderosos, portanto as credenciais de ID/segredo do aplicativo de saudação de tookeep-se de que seja seguro.
> 
> 

1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/01.png) 
2. De saudação **do active directory** , selecione seu diretório.
3. No menu de saudação na parte superior de saudação, clique em **aplicativos**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Na barra inferior de saudação, clique em **adicionar**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/03.png) 
5. Em Olá **o que fazer você deseja toodo?** caixa de diálogo, clique em **adicionar um aplicativo que minha organização esteja desenvolvendo**. 
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/04.png) 
6. Em Olá **Conte-nos sobre seu aplicativo** caixa de diálogo, executar Olá etapas a seguir: 
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    a. Em Olá **nome** caixa de texto, digite um nome (por exemplo: aplicativo de API de relatório).
   
    b. Selecione **Aplicativo Web e/ou API Web**.
   
    c. Clique em **Avançar**.
7. Em Olá **propriedades do aplicativo** caixa de diálogo, executar Olá etapas a seguir: 
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    a. Em Olá **URL de logon** caixa de texto, tipo `https://localhost`.
   
    b. Em Olá **URI da ID do aplicativo** caixa de texto, tipo ```https://localhost/ReportingApiApp```.
   
    c. Clique em **Concluído**.

## <a name="grant-your-application-permission-toouse-hello-api"></a>Conceder a saudação de toouse de permissão do aplicativo API
1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com/), em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/01.png) 
2. De saudação **do active directory** , selecione seu diretório.
3. No menu de saudação na parte superior de saudação, clique em **aplicativos**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/02.png)
4. Na lista de aplicativos hello, selecione seu aplicativo recém-criado.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/07.png)
5. No menu de saudação na parte superior de saudação, clique em **configurar**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/08.png)
6. Em hello **permissões tooother aplicativos** seção para hello **Active Directory do Azure** recursos, clique em hello **permissões de aplicativo** lista suspensa e, em seguida, Selecione **ler dados do diretório**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/09.png)
7. Na barra inferior de saudação, clique em **salvar**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a>Reúna as definições de configuração de seu diretório
Esta seção mostra como Olá tooget seguir as configurações de seu diretório:

* Nome de domínio
* ID do cliente
* Segredo do cliente

Você precisa esses valores quando configurar chamadas toohello reporting API. 

### <a name="get-your-domain-name"></a>Obter seu nome de domínio
1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/01.png) 
2. De saudação **do active directory** , selecione seu diretório.
3. No menu de saudação na parte superior de saudação, clique em **domínios**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/11.png) 
4. Em Olá **nome de domínio** coluna, copie o seu nome de domínio.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a>Obter ID do cliente do aplicativo hello
1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/01.png) 
2. De saudação **do active directory** , selecione seu diretório.
3. No menu de saudação na parte superior de saudação, clique em **aplicativos**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Na lista de aplicativos hello, selecione seu aplicativo recém-criado.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/07.png)
5. No menu de saudação na parte superior de saudação, clique em **configurar**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/08.png)
6. Copie a **ID do Cliente**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a>Obter o segredo do cliente do aplicativo hello
tooget cliente do aplicativo segredo, você precisa toocreate uma nova chave e salve seu valor ao salvar a nova chave de saudação porque ele não é possível tooretrieve este valor posteriormente mais.

1. Em Olá [portal clássico do Azure](https://manage.windowsazure.com), em Olá painel de navegação esquerdo, clique em **do Active Directory**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/01.png) 
2. De saudação **do active directory** , selecione seu diretório.
3. No menu de saudação na parte superior de saudação, clique em **aplicativos**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Na lista de aplicativos hello, selecione seu aplicativo recém-criado.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/07.png)
5. No menu de saudação na parte superior de saudação, clique em **configurar**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/08.png)
6. Em Olá **chaves** , execute Olá etapas a seguir: 
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/14.png)
   
    a. Na lista de duração hello, selecione uma duração
   
    b. Na barra inferior de saudação, clique em **salvar**.
   
    ![Registrar aplicativo](./media/active-directory-reporting-api-prerequisites/10.png)
   
    c. Copie o valor da chave hello.

## <a name="next-steps"></a>Próximas etapas
* Seria você como tooaccess Olá dados de saudação do AD do Azure API de relatório de modo programático? Check-out [Introdução à saudação do Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).
* Se você quiser toofind mais informações sobre os relatórios do Active Directory do Azure, consulte Olá [do Azure Active Directory Reporting guia](active-directory-reporting-guide.md).  

