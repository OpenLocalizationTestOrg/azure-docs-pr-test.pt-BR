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
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="c825c-104">Introdução ao Azure Active Directory Identity Protection e ao Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="c825c-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="c825c-105">Microsoft Graph é hello Microsoft unified ponto de extremidade de API e saudação inicial de [do Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span><span class="sxs-lookup"><span data-stu-id="c825c-105">Microsoft Graph is hello Microsoft unified API endpoint and hello home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="c825c-106">Olá primeira API, **identityRiskEvents**, permite que você tooquery Microsoft Graph para obter uma lista de [eventos de risco](active-directory-identityprotection-risk-events-types.md) e informações associadas.</span><span class="sxs-lookup"><span data-stu-id="c825c-106">hello first API, **identityRiskEvents**, allows you tooquery Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="c825c-107">Este artigo mostra como começar a consultar essa API.</span><span class="sxs-lookup"><span data-stu-id="c825c-107">This article gets you started querying this API.</span></span> <span data-ttu-id="c825c-108">Para uma introdução detalhada, a documentação completa e acesso toohello Gerenciador de gráficos, consulte Olá [site Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="c825c-108">For an in-depth introduction, full documentation, and access toohello Graph Explorer, see hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c825c-109">A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c825c-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="c825c-110">Há três etapas tooaccessing identidade proteção de dados por meio do Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="c825c-110">There are three steps tooaccessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="c825c-111">Adicione um aplicativo com um segredo do cliente.</span><span class="sxs-lookup"><span data-stu-id="c825c-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="c825c-112">Use esse segredo e algumas outras partes de informações tooauthenticate tooMicrosoft gráfico, onde você recebe um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="c825c-112">Use this secret and a few other pieces of information tooauthenticate tooMicrosoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="c825c-113">Use esse ponto de extremidade do token toomake solicitações toohello API e obter dados de proteção de identidade.</span><span class="sxs-lookup"><span data-stu-id="c825c-113">Use this token toomake requests toohello API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="c825c-114">Antes de começar, será necessário:</span><span class="sxs-lookup"><span data-stu-id="c825c-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="c825c-115">Aplicativo de saudação de toocreate de privilégios de administrador no AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c825c-115">Administrator privileges toocreate hello application in Azure AD</span></span>
* <span data-ttu-id="c825c-116">nome de saudação do domínio do locatário (por exemplo, contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="c825c-116">hello name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="c825c-117">Adicionar um aplicativo com um segredo do cliente</span><span class="sxs-lookup"><span data-stu-id="c825c-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="c825c-118">[Entrar](https://manage.windowsazure.com) tooyour portal clássico do Azure como administrador.</span><span class="sxs-lookup"><span data-stu-id="c825c-118">[Sign in](https://manage.windowsazure.com) tooyour Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="c825c-119">No painel de navegação esquerdo hello, clique em **do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c825c-119">On on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="c825c-121">De saudação **diretório** lista, pasta de Olá select para o qual você deseja tooenable integração de diretório.</span><span class="sxs-lookup"><span data-stu-id="c825c-121">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
4. <span data-ttu-id="c825c-122">No menu de saudação na parte superior de saudação, clique em **aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c825c-122">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="c825c-124">Clique em **adicionar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="c825c-124">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="c825c-126">Em Olá **o que fazer você deseja toodo** caixa de diálogo, clique em **adicionar um aplicativo que minha organização esteja desenvolvendo**.</span><span class="sxs-lookup"><span data-stu-id="c825c-126">On hello **What do you want toodo** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="c825c-128">Em Olá **Conte-nos sobre seu aplicativo** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c825c-128">On hello **Tell us about your application** dialog, perform hello following steps:</span></span>
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="c825c-130">a.</span><span class="sxs-lookup"><span data-stu-id="c825c-130">a.</span></span> <span data-ttu-id="c825c-131">Em Olá **nome** caixa de texto, digite um nome para seu aplicativo (por exemplo: AADIP aplicativo de API de eventos de risco).</span><span class="sxs-lookup"><span data-stu-id="c825c-131">In hello **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="c825c-132">b.</span><span class="sxs-lookup"><span data-stu-id="c825c-132">b.</span></span> <span data-ttu-id="c825c-133">Como **Tipo**, selecione **Aplicativo Web E/Ou API Web**.</span><span class="sxs-lookup"><span data-stu-id="c825c-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="c825c-134">c.</span><span class="sxs-lookup"><span data-stu-id="c825c-134">c.</span></span> <span data-ttu-id="c825c-135">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="c825c-135">Click **Next**.</span></span>
8. <span data-ttu-id="c825c-136">Em Olá **propriedades do aplicativo** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c825c-136">On hello **App properties** dialog, perform hello following steps:</span></span>
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="c825c-138">a.</span><span class="sxs-lookup"><span data-stu-id="c825c-138">a.</span></span> <span data-ttu-id="c825c-139">Em Olá **URL de logon** caixa de texto, tipo `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="c825c-139">In hello **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="c825c-140">b.</span><span class="sxs-lookup"><span data-stu-id="c825c-140">b.</span></span> <span data-ttu-id="c825c-141">Em Olá **URI da ID do aplicativo** caixa de texto, tipo `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="c825c-141">In hello **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="c825c-142">c.</span><span class="sxs-lookup"><span data-stu-id="c825c-142">c.</span></span> <span data-ttu-id="c825c-143">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="c825c-143">Click **Complete**.</span></span>

<span data-ttu-id="c825c-144">Agora você pode configurar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c825c-144">Your can now configure your application.</span></span>

![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="c825c-146">Conceder a saudação de toouse de permissão do aplicativo API</span><span class="sxs-lookup"><span data-stu-id="c825c-146">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="c825c-147">Na página do seu aplicativo, no menu de saudação na parte superior da saudação, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="c825c-147">On your application's page, in hello menu on hello top, click **Configure**.</span></span> 
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="c825c-149">Em Olá **permissões tooother aplicativos** seção, clique em **Adicionar aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="c825c-149">In hello **permissions tooother applications** section, click **Add application**.</span></span>
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="c825c-151">Em Olá **permissões tooother aplicativos** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c825c-151">On hello **permissions tooother applications** dialog, perform hello following steps:</span></span>
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="c825c-153">a.</span><span class="sxs-lookup"><span data-stu-id="c825c-153">a.</span></span> <span data-ttu-id="c825c-154">Selecione **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="c825c-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="c825c-155">b.</span><span class="sxs-lookup"><span data-stu-id="c825c-155">b.</span></span> <span data-ttu-id="c825c-156">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="c825c-156">Click **Complete**.</span></span>
4. <span data-ttu-id="c825c-157">Clique em **Permissões do Aplicativo: 0**, em seguida, selecione **Ler todas as informações de evento de risco da identidade**.</span><span class="sxs-lookup"><span data-stu-id="c825c-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="c825c-159">Clique em **salvar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="c825c-159">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="c825c-161">Obter uma chave de acesso</span><span class="sxs-lookup"><span data-stu-id="c825c-161">Get an access key</span></span>
1. <span data-ttu-id="c825c-162">Na página do seu aplicativo hello **chaves** seção, selecione 1 ano como duração.</span><span class="sxs-lookup"><span data-stu-id="c825c-162">On your application's page, in hello **keys** section, select 1 year as duration.</span></span>
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="c825c-164">Clique em **salvar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="c825c-164">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="c825c-166">na seção de chaves hello, copie Olá valor da chave recém-criada e, em seguida, cole-o em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="c825c-166">in hello keys section, copy hello value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![Criação de um aplicativo](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="c825c-168">Se você perder esta chave, será necessário tooreturn toothis seção e crie uma nova chave.</span><span class="sxs-lookup"><span data-stu-id="c825c-168">If you lose this key, you will have tooreturn toothis section and create a new key.</span></span> <span data-ttu-id="c825c-169">Mantenha essa chave em segredo: qualquer pessoa que a tenha poderá acessar seus dados.</span><span class="sxs-lookup"><span data-stu-id="c825c-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="c825c-170">Em Olá **propriedades** seção, Olá cópia **ID do cliente**e, em seguida, cole-o em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="c825c-170">In hello **properties** section, copy hello **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a><span data-ttu-id="c825c-171">Autenticar tooMicrosoft gráfico e Olá consulta API de eventos de risco de identidade</span><span class="sxs-lookup"><span data-stu-id="c825c-171">Authenticate tooMicrosoft Graph and query hello Identity Risk Events API</span></span>
<span data-ttu-id="c825c-172">Neste ponto, você deve ter:</span><span class="sxs-lookup"><span data-stu-id="c825c-172">At this point, you should have:</span></span>

* <span data-ttu-id="c825c-173">ID do cliente Olá copiados acima</span><span class="sxs-lookup"><span data-stu-id="c825c-173">hello client ID you copied above</span></span>
* <span data-ttu-id="c825c-174">chave de saudação copiados acima</span><span class="sxs-lookup"><span data-stu-id="c825c-174">hello key you copied above</span></span>
* <span data-ttu-id="c825c-175">nome de saudação do domínio do locatário</span><span class="sxs-lookup"><span data-stu-id="c825c-175">hello name of your tenant's domain</span></span>

<span data-ttu-id="c825c-176">tooauthenticate, enviar uma postagem de solicitação muito`https://login.microsoft.com` com hello parâmetros no corpo de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="c825c-176">tooauthenticate, send a post request too`https://login.microsoft.com` with hello following parameters in hello body:</span></span>

* <span data-ttu-id="c825c-177">grant_type: “**client_credentials**”</span><span class="sxs-lookup"><span data-stu-id="c825c-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="c825c-178">resource: “**https://graph.microsoft.com**”</span><span class="sxs-lookup"><span data-stu-id="c825c-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="c825c-179">client_id: <your client ID></span><span class="sxs-lookup"><span data-stu-id="c825c-179">client_id: <your client ID></span></span>
* <span data-ttu-id="c825c-180">client_secret: <your key></span><span class="sxs-lookup"><span data-stu-id="c825c-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="c825c-181">Você precisa tooprovide valores para Olá **client_id** e hello **client_secret** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="c825c-181">You need tooprovide values for hello **client_id** and hello **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="c825c-182">Se for bem-sucedido, será retornado um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="c825c-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="c825c-183">Olá toocall API, crie um cabeçalho com hello parâmetro a seguir:</span><span class="sxs-lookup"><span data-stu-id="c825c-183">toocall hello API, create a header with hello following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="c825c-184">Durante a autenticação, você pode encontrar o tipo de token hello e token de acesso no hello retornada um token.</span><span class="sxs-lookup"><span data-stu-id="c825c-184">When authenticating, you can find hello token type and access token in hello returned token.</span></span>

<span data-ttu-id="c825c-185">Envie esse cabeçalho como uma toohello de solicitação URL da API a seguir:`https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="c825c-185">Send this header as a request toohello following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="c825c-186">resposta de Hello, se for bem-sucedido, é uma coleção de identidade eventos de risco e dados em Olá formato OData JSON, que pode ser analisado e manipulado como melhor associados.</span><span class="sxs-lookup"><span data-stu-id="c825c-186">hello response, if successful, is a collection of identity risk events and associated data in hello OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="c825c-187">Aqui está o código de exemplo para autenticar e chamar a API de saudação usando o Powershell.</span><span class="sxs-lookup"><span data-stu-id="c825c-187">Here’s sample code for authenticating and calling hello API using Powershell.</span></span>  
<span data-ttu-id="c825c-188">Basta adicionar sua ID do cliente, a chave e o domínio do locatário.</span><span class="sxs-lookup"><span data-stu-id="c825c-188">Just add your client ID, key, and tenant domain.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="c825c-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c825c-189">Next steps</span></span>
<span data-ttu-id="c825c-190">Parabéns, você acabou de criar seu primeiro tooMicrosoft de chamadas gráfico!</span><span class="sxs-lookup"><span data-stu-id="c825c-190">Congratulations, you just made your first call tooMicrosoft Graph!</span></span>  
<span data-ttu-id="c825c-191">Agora você pode consultar os eventos de risco de identidade e usar dados saudação como quiser.</span><span class="sxs-lookup"><span data-stu-id="c825c-191">Now you can query identity risk events and use hello data however you see fit.</span></span>

<span data-ttu-id="c825c-192">toolearn mais sobre o Microsoft Graph e como os aplicativos toobuild usando Olá Graph API, confira Olá [documentação](https://graph.microsoft.io/docs) e muito mais no hello [site Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="c825c-192">toolearn more about Microsoft Graph and how toobuild applications using hello Graph API, check out hello [documentation](https://graph.microsoft.io/docs) and much more on hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="c825c-193">Além disso, verifique se Olá de toobookmark [API do Azure AD Identity Protection](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) página que lista todos os Olá APIs de proteção de identidade disponível no gráfico.</span><span class="sxs-lookup"><span data-stu-id="c825c-193">Also, make sure toobookmark hello [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of hello Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="c825c-194">Como podemos adicionar novo toowork maneiras com proteção de identidade por meio da API, você poderá vê-los na página.</span><span class="sxs-lookup"><span data-stu-id="c825c-194">As we add new ways toowork with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c825c-195">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c825c-195">Additional resources</span></span>
* [<span data-ttu-id="c825c-196">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="c825c-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="c825c-197">Tipos de eventos de risco detectados pelo Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="c825c-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="c825c-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="c825c-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="c825c-199">Visão geral do Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="c825c-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="c825c-200">Raiz do Serviço Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="c825c-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

