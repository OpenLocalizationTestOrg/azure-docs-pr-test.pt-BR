---
title: "aaaGet iniciado com a proteção de identidade do Azure Active Directory e o Microsoft Graph | Microsoft Docs"
description: "Fornece uma introdução tooquery Microsoft Graph para obter uma lista de eventos de risco e as informações associadas do Azure Active Directory."
services: active-directory
keywords: "azure active directory identity protection, evento de risco, vulnerabilidade, política de segurança, Microsoft Graph"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a>Introdução ao Azure Active Directory Identity Protection e ao Microsoft Graph
Microsoft Graph é hello Microsoft unified ponto de extremidade de API e saudação inicial de [do Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs. Olá primeira API, **identityRiskEvents**, permite que você tooquery Microsoft Graph para obter uma lista de [eventos de risco](active-directory-identityprotection-risk-events-types.md) e informações associadas. Este artigo mostra como começar a consultar essa API. Para uma introdução detalhada, a documentação completa e acesso toohello Gerenciador de gráficos, consulte Olá [site Microsoft Graph](https://graph.microsoft.io/).

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo.

Há três etapas tooaccessing identidade proteção de dados por meio do Microsoft Graph:

1. Adicione um aplicativo com um segredo do cliente. 
2. Use esse segredo e algumas outras partes de informações tooauthenticate tooMicrosoft gráfico, onde você recebe um token de autenticação. 
3. Use esse ponto de extremidade do token toomake solicitações toohello API e obter dados de proteção de identidade.

Antes de começar, será necessário:

* Aplicativo de saudação de toocreate de privilégios de administrador no AD do Azure
* nome de saudação do domínio do locatário (por exemplo, contoso.onmicrosoft.com)

## <a name="add-an-application-with-a-client-secret"></a>Adicionar um aplicativo com um segredo do cliente
1. [Entrar](https://manage.windowsazure.com) tooyour portal clássico do Azure como administrador. 
2. No painel de navegação esquerdo hello, clique em **do Active Directory**. 
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.
4. No menu de saudação na parte superior de saudação, clique em **aplicativos**.
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. Clique em **adicionar** final Olá Olá página.
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo que minha organização esteja desenvolvendo**.
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. Em Olá **Conte-nos sobre seu aplicativo** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    a. Em Olá **nome** caixa de texto, digite um nome para seu aplicativo (por exemplo: AADIP aplicativo de API de eventos de risco).
   
    b. Como **Tipo**, selecione **Aplicativo Web E/Ou API Web**.
   
    c. Clique em **Avançar**.
8. Em Olá **propriedades do aplicativo** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    a. Em Olá **URL de logon** caixa de texto, tipo `http://localhost`.
   
    b. Em Olá **URI da ID do aplicativo** caixa de texto, tipo `http://localhost`.
   
    c. Clique em **Concluído**.

Agora você pode configurar seu aplicativo.

![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a>Conceder a saudação de toouse de permissão do aplicativo API
1. Na página do seu aplicativo, no menu de saudação na parte superior da saudação, clique em **configurar**. 
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. Em Olá **permissões tooother aplicativos** seção, clique em **Adicionar aplicativo**.
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. Em Olá **permissões tooother aplicativos** caixa de diálogo, executar Olá etapas a seguir:
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    a. Selecione **Microsoft Graph**.
   
    b. Clique em **Concluído**.
4. Clique em **Permissões do Aplicativo: 0**, em seguida, selecione **Ler todas as informações de evento de risco da identidade**.
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. Clique em **salvar** final Olá Olá página.
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a>Obter uma chave de acesso
1. Na página do seu aplicativo hello **chaves** seção, selecione 1 ano como duração.
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. Clique em **salvar** final Olá Olá página.
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. na seção de chaves hello, copie Olá valor da chave recém-criada e, em seguida, cole-o em um local seguro.
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > Se você perder esta chave, será necessário tooreturn toothis seção e crie uma nova chave. Mantenha essa chave em segredo: qualquer pessoa que a tenha poderá acessar seus dados.
   > 
   > 
4. Em Olá **propriedades** seção, Olá cópia **ID do cliente**e, em seguida, cole-o em um local seguro. 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a>Autenticar tooMicrosoft gráfico e Olá consulta API de eventos de risco de identidade
Neste ponto, você deve ter:

* ID do cliente Olá copiados acima
* chave de saudação copiados acima
* nome de saudação do domínio do locatário

tooauthenticate, enviar uma postagem de solicitação muito`https://login.microsoft.com` com hello parâmetros no corpo de saudação a seguir:

* grant_type: “**client_credentials**”
* resource: “**https://graph.microsoft.com**”
* client_id: <your client ID>
* client_secret: <your key>

> [!NOTE]
> Você precisa tooprovide valores para Olá **client_id** e hello **client_secret** parâmetro.
> 
> 

Se for bem-sucedido, será retornado um token de autenticação.  
Olá toocall API, crie um cabeçalho com hello parâmetro a seguir:

    `Authorization`=”<token_type> <access_token>"


Durante a autenticação, você pode encontrar o tipo de token hello e token de acesso no hello retornada um token.

Envie esse cabeçalho como uma toohello de solicitação URL da API a seguir:`https://graph.microsoft.com/beta/identityRiskEvents`

resposta de Hello, se for bem-sucedido, é uma coleção de identidade eventos de risco e dados em Olá formato OData JSON, que pode ser analisado e manipulado como melhor associados.

Aqui está o código de exemplo para autenticar e chamar a API de saudação usando o Powershell.  
Basta adicionar sua ID do cliente, a chave e o domínio do locatário.

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a>Próximas etapas
Parabéns, você acabou de criar seu primeiro tooMicrosoft de chamadas gráfico!  
Agora você pode consultar os eventos de risco de identidade e usar dados saudação como quiser.

toolearn mais sobre o Microsoft Graph e como os aplicativos toobuild usando Olá Graph API, confira Olá [documentação](https://graph.microsoft.io/docs) e muito mais no hello [site Microsoft Graph](https://graph.microsoft.io/). Além disso, verifique se Olá de toobookmark [API do Azure AD Identity Protection](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) página que lista todos os Olá APIs de proteção de identidade disponível no gráfico. Como podemos adicionar novo toowork maneiras com proteção de identidade por meio da API, você poderá vê-los na página.

## <a name="additional-resources"></a>Recursos adicionais
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)
* [Tipos de eventos de risco detectados pelo Azure Active Directory Identity Protection](active-directory-identityprotection-risk-events-types.md)
* [Microsoft Graph](https://graph.microsoft.io/)
* [Visão geral do Microsoft Graph](https://graph.microsoft.io/docs)
* [Raiz do Serviço Azure AD Identity Protection](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

