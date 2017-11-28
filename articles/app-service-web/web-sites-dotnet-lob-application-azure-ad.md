---
title: "aaaCreate um aplicativo de linha de negócios do Azure com a autenticação do Active Directory do Azure | Microsoft Docs"
description: "Saiba como o aplicativo toocreate uma ASP.NET MVC linha de negócios no serviço de aplicativo do Azure que autentica com o Active Directory do Azure"
services: app-service\web, active-directory
documentationcenter: .net
author: cephalin
manager: erikre
editor: 
ms.assetid: ad947bdb-4463-43ff-a5e3-91d9b2169b60
ms.service: app-service-web
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 09/01/2016
ms.author: cephalin
ms.openlocfilehash: 3bcafad78ac0151889b3e336784cc561009f244f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="a5e5e-103">Criar um aplicativo de linha de negócios do Azure com a autenticação do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5e5e-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="a5e5e-104">Este artigo mostra como aplicativo toocreate uma .NET linha de negócios em [aplicativos de Web do serviço de aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) usando Olá [autenticação / autorização](../app-service/app-service-authentication-overview.md) recurso.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-104">This article shows you how toocreate a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using hello [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="a5e5e-105">Ele também mostra como Olá toouse [API do Graph do Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery dados do diretório de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-105">It also shows how toouse hello [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) tooquery directory data in hello application.</span></span>

<span data-ttu-id="a5e5e-106">locatário do Active Directory do Azure Olá que você usar pode ser um diretório somente no Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-106">hello Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="a5e5e-107">Ou, pode ser [sincronizado com o Active Directory no local](../active-directory/active-directory-aadconnect.md) toocreate uma experiência de logon único para os funcionários que estão em locais e remotos.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) toocreate a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="a5e5e-108">Este artigo usa o diretório padrão de saudação para sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-108">This article uses hello default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="a5e5e-109">O que você compilará</span><span class="sxs-lookup"><span data-stu-id="a5e5e-109">What you will build</span></span>
<span data-ttu-id="a5e5e-110">Você criará um aplicativo simples de criar-leitura-atualização-exclusão (CRUD) de linha de negócios em aplicativos de Web do serviço de aplicativo que rastreia itens de trabalho com hello recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a5e5e-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with hello following features:</span></span>

* <span data-ttu-id="a5e5e-111">Autentica usuários no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a5e5e-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="a5e5e-112">Consulta usuários de diretório e grupos usando a [API do Graph do Azure Active Directory](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="a5e5e-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="a5e5e-113">Use Olá ASP.NET MVC *sem autenticação* modelo</span><span class="sxs-lookup"><span data-stu-id="a5e5e-113">Use hello ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="a5e5e-114">Se você precisar de controle de acesso baseado em função (RBAC) para seu aplicativo de linha de negócios no Azure, confira a [Próxima etapa](#next).</span><span class="sxs-lookup"><span data-stu-id="a5e5e-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="a5e5e-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="a5e5e-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="a5e5e-116">Você precisa Olá toocomplete a seguir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="a5e5e-116">You need hello following toocomplete this tutorial:</span></span>

* <span data-ttu-id="a5e5e-117">Um locatário do Active Directory do Azure com usuários em vários grupos</span><span class="sxs-lookup"><span data-stu-id="a5e5e-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="a5e5e-118">Permissões toocreate aplicativos no locatário do Active Directory do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="a5e5e-118">Permissions toocreate applications on hello Azure Active Directory tenant</span></span>
* <span data-ttu-id="a5e5e-119">Visual Studio 2013 Atualização 4 ou posterior</span><span class="sxs-lookup"><span data-stu-id="a5e5e-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="a5e5e-120">SDK 2.8.1 do Azure ou posterior</span><span class="sxs-lookup"><span data-stu-id="a5e5e-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-tooazure"></a><span data-ttu-id="a5e5e-121">Criar e implantar um tooAzure de aplicativo web</span><span class="sxs-lookup"><span data-stu-id="a5e5e-121">Create and deploy a web app tooAzure</span></span>
1. <span data-ttu-id="a5e5e-122">No Visual Studio, clique em **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="a5e5e-123">Selecione **Aplicativo Web ASP.NET**, nomeie seu projeto e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="a5e5e-124">Selecione Olá **MVC** modelo, altere a autenticação de saudação muito**sem autenticação**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-124">Select hello **MVC** template, then change hello authentication too**No Authentication**.</span></span> <span data-ttu-id="a5e5e-125">Certifique-se de **Host na nuvem de saudação** está selecionado e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-125">Make sure **Host in hello Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="a5e5e-126">Em Olá **criar serviço de aplicativo** caixa de diálogo, clique em **adicionar uma conta** (e, em seguida, **adicionar uma conta** na lista suspensa de saudação) toolog em tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-126">In hello **Create App Service** dialog, click **Add an account** (and then **Add an account** in hello dropdown) toolog in tooyour Azure account.</span></span>
5. <span data-ttu-id="a5e5e-127">Depois de conectado, configure seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-127">Once logged in configure your web app.</span></span> <span data-ttu-id="a5e5e-128">Criar um grupo de recursos e um novo plano de serviço de aplicativo clicando Olá respectivo **novo** botão.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-128">Create a resource group and a new App Service plan by clicking hello respective **New** button.</span></span> <span data-ttu-id="a5e5e-129">Clique em **explorar serviços adicionais do Azure** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-129">Click **Explore additional Azure services** toocontinue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="a5e5e-130">Em Olá **serviços** , clique em  **+**  tooadd um banco de dados SQL para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-130">In hello **Services** tab, click **+** tooadd a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="a5e5e-131">Em **configurar banco de dados SQL**, clique em **novo** toocreate uma instância do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-131">In **Configure SQL Database**, click **New** toocreate a SQL Server instance.</span></span>
8. <span data-ttu-id="a5e5e-132">Em **Configurar SQL Server**, configure sua instância do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="a5e5e-133">Em seguida, clique em **Okey**, **Okey**, e **criar** tookick desativar a criação de saudação de aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-133">Then, click **OK**, **OK**, and **Create** tookick off hello app creation in Azure.</span></span>
9. <span data-ttu-id="a5e5e-134">Em **atividade de serviço de aplicativo do Azure**, você pode ver quando da criação do aplicativo hello for concluída.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-134">In **Azure App Service Activity**, you can see when hello app creation is finished.</span></span> <span data-ttu-id="a5e5e-135">Clique em  **publicar &lt;* appname*> toothis aplicativo Web agora * *, em seguida, clique em **publicar**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-135">Click **Publish &lt;*appname*> toothis Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="a5e5e-136">Depois que o Visual Studio for concluído, ele abre Olá publicar o aplicativo no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-136">Once Visual Studio finishes, it opens hello publish app in hello browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="a5e5e-137">Configurar a autenticação e acesso ao diretório</span><span class="sxs-lookup"><span data-stu-id="a5e5e-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="a5e5e-138">Faça logon no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5e5e-138">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="a5e5e-139">No menu à esquerda do hello, clique em **serviços de aplicativos** > **&lt;*appname*> * * > **autenticação / autorização**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-139">From hello left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="a5e5e-140">Ative a autenticação do Azure Active Directory clicando em **Ativar** > **Azure Active Directory** > **Expresso** > **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="a5e5e-141">Clique em **salvar** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-141">Click **Save** in hello command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="a5e5e-142">Depois que as configurações de autenticação Olá foram salvas com êxito, tente navegar tooyour aplicativo novamente no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-142">Once hello authentication settings are saved successfully, try navigating tooyour app again in hello browser.</span></span> <span data-ttu-id="a5e5e-143">As configurações padrão impõem a autenticação no aplicativo inteiro hello.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-143">Your default settings enforce authentication on hello whole app.</span></span> <span data-ttu-id="a5e5e-144">Se você já não estiver conectado, você é redirecionado tooa a tela de login.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-144">If you aren't already logged in, you are redirected tooa login screen.</span></span> <span data-ttu-id="a5e5e-145">Depois de conectado, você verá seu aplicativo protegido por HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="a5e5e-146">Em seguida, você precisa toodirectory tooenable acessar os dados.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-146">Next, you need tooenable access toodirectory data.</span></span> 
5. <span data-ttu-id="a5e5e-147">Navegue toohello [portal clássico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="a5e5e-147">Navigate toohello [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="a5e5e-148">No menu à esquerda do hello, clique em **do Active Directory** > **diretório padrão** > **aplicativos**  >   **&lt;* appname*> * *.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-148">From hello left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="a5e5e-149">Este é o aplicativo do Active Directory do Azure hello que o serviço de aplicativo criado para você tooenable Olá autorização / recurso de autenticação.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-149">This is hello Azure Active Directory application that App Service created for you tooenable hello Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="a5e5e-150">Clique em **usuários** e **grupos** toomake-se de que há alguns usuários e grupos no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-150">Click **Users** and **Groups** toomake sure that you have some users and groups in hello directory.</span></span> <span data-ttu-id="a5e5e-151">Caso contrário, crie alguns usuários e grupos de teste.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="a5e5e-152">Clique em **configurar** tooconfigure este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-152">Click **Configure** tooconfigure this application.</span></span>
9. <span data-ttu-id="a5e5e-153">Role para baixo toohello **chaves** seção e adicione uma chave, selecionando uma duração.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-153">Scroll down toohello **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="a5e5e-154">Em seguida, clique em **Permissões Delegadas** e selecione **Ler dados do diretório**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="a5e5e-155">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="a5e5e-156">Depois que as configurações são salvas, role para cima toohello **chaves** seção e clique em Olá **cópia** chave botão toocopy de saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-156">Once your settings are saved, scroll back up toohello **Keys** section and click hello **Copy** button toocopy hello client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="a5e5e-157">Se você sair desta página agora, não será capaz de tooaccess esse cliente nunca novamente da chave.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-157">If you navigate away from this page now, you won't be able tooaccess this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="a5e5e-158">Em seguida, você precisa tooconfigure seu aplicativo web com essa chave.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-158">Next, you need tooconfigure your web app with this key.</span></span> <span data-ttu-id="a5e5e-159">Faça logon no toohello [Gerenciador de recursos do Azure](https://resources.azure.com) com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-159">Log in toohello [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="a5e5e-160">Na parte superior de saudação da página de saudação, clique em **leitura/gravação** toomake alterações Olá Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-160">At hello top of hello page, click **Read/Write** toomake changes in hello Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="a5e5e-161">Localizar as configurações de autenticação para seu aplicativo, localizado em assinaturas de hello >  **&lt;* subscriptionname*> * * > **resourceGroups**  >   **&lt;* resourcegroupname*> * * > **provedores** > **Microsoft**  >  **sites** > **&lt;*appname*> * * > **config**  >  **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-161">Find hello authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="a5e5e-162">Clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="a5e5e-163">Olá painel de edição, definido Olá `clientSecret` e `additionalLoginParams` propriedades da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-163">In hello editing pane, set hello `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from hello Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="a5e5e-164">Clique em **colocar** em Olá toosubmit superior suas alterações.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-164">Click **Put** at hello top toosubmit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="a5e5e-165">Tootest agora, se você tiver autorização Olá token Olá tooaccess API do Graph do Azure Active Directory, basta navegar até  **https://&lt;*appname*>.azurewebsites.net/.auth/me** no seu Navegador.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-165">Now, tootest if you have hello authorization token tooaccess hello Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="a5e5e-166">Se você configurou tudo corretamente, você deverá ver Olá `access_token` propriedade Olá resposta JSON.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-166">If you configured everything correctly, you should see hello `access_token` property in hello JSON response.</span></span>
    
    <span data-ttu-id="a5e5e-167">Olá `~/.auth/me` caminho da URL é gerenciado pelo aplicativo serviço de autenticação / autorização toogive você todas as informações de saudação relacionados sessão tooyour autenticado.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-167">hello `~/.auth/me` URL path is managed by App Service Authentication / Authorization toogive you all hello information related tooyour authenticated session.</span></span> <span data-ttu-id="a5e5e-168">Para saber mais, confira [Autenticação e autorização no Serviço de Aplicativo do Azure](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a5e5e-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="a5e5e-169">Olá `access_token` tem um período de expiração.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-169">hello `access_token` has an expiration period.</span></span> <span data-ttu-id="a5e5e-170">No entanto, a Autenticação/Autorização do Serviço de Aplicativo fornece a funcionalidade de atualização do token com `~/.auth/refresh`.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="a5e5e-171">Para obter mais informações sobre como toouse, consulte [armazenamento de Token do serviço de aplicativo](https://cgillum.tech/2016/03/07/app-service-token-store/).</span><span class="sxs-lookup"><span data-stu-id="a5e5e-171">For more information on how toouse it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="a5e5e-172">Em seguida, você fará algo útil com os dados do diretório.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-tooyour-app"></a><span data-ttu-id="a5e5e-173">Adicionar a funcionalidade de linha de negócios tooyour aplicativo</span><span class="sxs-lookup"><span data-stu-id="a5e5e-173">Add line-of-business functionality tooyour app</span></span>
<span data-ttu-id="a5e5e-174">Agora, crie um rastreador de itens de trabalho CRUD simples.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="a5e5e-175">Na pasta de ~\Models hello, crie um arquivo de classe chamado WorkItem.cs e substitua `public class WorkItem {...}` com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="a5e5e-175">In hello ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with hello following code:</span></span>
   
     <span data-ttu-id="a5e5e-176">using System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="a5e5e-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="a5e5e-177">public class WorkItem   {</span><span class="sxs-lookup"><span data-stu-id="a5e5e-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="a5e5e-178">}</span><span class="sxs-lookup"><span data-stu-id="a5e5e-178">}</span></span>
   
     <span data-ttu-id="a5e5e-179">public enum WorkItemStatus   {</span><span class="sxs-lookup"><span data-stu-id="a5e5e-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="a5e5e-180">}</span><span class="sxs-lookup"><span data-stu-id="a5e5e-180">}</span></span>
2. <span data-ttu-id="a5e5e-181">Crie hello projeto toomake sua nova lógica de scaffolding toohello acessível do modelo no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-181">Build hello project toomake your new model accessible toohello scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="a5e5e-182">Adicionar um novo item de scaffolding `WorkItemsController` toohello ~\Controllers pasta (clique **controladores**, ponto muito**adicionar**e selecione **novo item de scaffolding**).</span><span class="sxs-lookup"><span data-stu-id="a5e5e-182">Add a new scaffolded item `WorkItemsController` toohello ~\Controllers folder (right-click **Controllers**, point too**Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="a5e5e-183">Selecione **Controlador MVC 5 com modos de exibição usando o Entity Framework** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="a5e5e-184">Modelo de saudação selecione que você criou, clique  **+**  e, em seguida, **adicionar** tooadd um contexto de dados e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-184">Select hello model that you created, then click **+** and then **Add** tooadd a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="a5e5e-185">No ~\Views\WorkItems\Create.cshtml (um item de scaffolding automaticamente), localize Olá `Html.BeginForm` método auxiliar e fazer Olá realçadas alterações a seguir:</span><span class="sxs-lookup"><span data-stu-id="a5e5e-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find hello `Html.BeginForm` helper method and make hello following highlighted changes:</span></span>  
   
   <pre class="prettyprint">
   @model WebApplication1.Models.WorkItem
   
   @{
    ViewBag.Title = &quot;Create&quot;;
   }
   
   &lt;h2&gt;Create&lt;/h2&gt;
   
   @using (Html.BeginForm(<mark>&quot;Create&quot;, &quot;WorkItems&quot;, FormMethod.Post, new { id = &quot;main-form&quot; }</mark>)) 
   {
    @Html.AntiForgeryToken()
   
    &lt;div class=&quot;form-horizontal&quot;&gt;
        &lt;h4&gt;WorkItem&lt;/h4&gt;
        &lt;hr /&gt;
        @Html.ValidationSummary(true, &quot;&quot;, new { @class = &quot;text-danger&quot; })
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToID, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToID, new { htmlAttributes = new { @class = &quot;form-control&quot;<mark>, @type = &quot;hidden&quot;</mark> } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToID, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.AssignedToName, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.AssignedToName, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.AssignedToName, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Description, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EditorFor(model =&gt; model.Description, new { htmlAttributes = new { @class = &quot;form-control&quot; } })
                @Html.ValidationMessageFor(model =&gt; model.Description, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            @Html.LabelFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;control-label col-md-2&quot; })
            &lt;div class=&quot;col-md-10&quot;&gt;
                @Html.EnumDropDownListFor(model =&gt; model.Status, htmlAttributes: new { @class = &quot;form-control&quot; })
                @Html.ValidationMessageFor(model =&gt; model.Status, &quot;&quot;, new { @class = &quot;text-danger&quot; })
            &lt;/div&gt;
        &lt;/div&gt;
   
        &lt;div class=&quot;form-group&quot;&gt;
            &lt;div class=&quot;col-md-offset-2 col-md-10&quot;&gt;
                &lt;input type=&quot;submit&quot; value=&quot;Create&quot; class=&quot;btn btn-default&quot;<mark> id=&quot;submit-button&quot;</mark> /&gt;
            &lt;/div&gt;
        &lt;/div&gt;
    &lt;/div&gt;
   }
   
   &lt;div&gt;
    @Html.ActionLink(&quot;Back tooList&quot;, &quot;Index&quot;)
   &lt;/div&gt;
   
   @section Scripts {
    @Scripts.Render(&quot;~/bundles/jqueryval&quot;)
    <mark>&lt;script&gt;
        // People/Group Picker Code
        var maxResultsPerPage = 14;
        var input = document.getElementById(&quot;AssignedToName&quot;);
   
        // Access token from request header, and tenantID from claims identity
        var token = &quot;@Request.Headers[&quot;X-MS-TOKEN-AAD-ACCESS-TOKEN&quot;]&quot;;
        var tenant =&quot;@(System.Security.Claims.ClaimsPrincipal.Current.Claims
                        .Where(c => c.Type == &quot;http://schemas.microsoft.com/identity/claims/tenantid&quot;)
                        .Select(c => c.Value).SingleOrDefault())&quot;;
   
        var picker = new AadPicker(maxResultsPerPage, input, token, tenant);
   
        // Submit hello selected user/group toobe asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="a5e5e-186">Observe que `token` e `tenant` são usados por Olá `AadPicker` toomake objeto chamadas de API do Graph do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-186">Note that `token` and `tenant` are used by hello `AadPicker` object toomake Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="a5e5e-187">Você adicionará `AadPicker` mais tarde.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="a5e5e-188">Você também pode obter `token` e `tenant` do lado do cliente Olá com `~/.auth/me`, mas que deve ser uma chamada de servidor adicional.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-188">You can just as well get `token` and `tenant` from hello client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="a5e5e-189">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="a5e5e-189">For example:</span></span>
   > 
   > <span data-ttu-id="a5e5e-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span><span class="sxs-lookup"><span data-stu-id="a5e5e-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="a5e5e-191">Alterar Olá mesmo com ~ \Views\WorkItems\Edit.cshtml.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-191">Make hello same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="a5e5e-192">Olá `AadPicker` objeto é definido em um script que você precisa tooadd tooyour projeto.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-192">hello `AadPicker` object is defined in a script that you need tooadd tooyour project.</span></span> <span data-ttu-id="a5e5e-193">Clique Olá ~\Scripts pasta, aponte muito**adicionar**e clique em **arquivo JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-193">Right-click hello ~\Scripts folder, point too**Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="a5e5e-194">Tipo `AadPickerLibrary` para o nome de arquivo hello e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-194">Type `AadPickerLibrary` for hello filename and click **OK**.</span></span>
9. <span data-ttu-id="a5e5e-195">Copiar o conteúdo de saudação do [aqui](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) em ~ \Scripts\AadPickerLibrary.js.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-195">Copy hello content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="a5e5e-196">No script hello, Olá `AadPicker` objeto chamadas [API do Graph do Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch para usuários e grupos que corresponder à entrada hello.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-196">In hello script, hello `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) toosearch for users and groups that match hello input.</span></span>  
10. <span data-ttu-id="a5e5e-197">~\Scripts\AadPickerLibrary.js também usa Olá [jQuery UI AutoCompletar widget](https://jqueryui.com/autocomplete/).</span><span class="sxs-lookup"><span data-stu-id="a5e5e-197">~\Scripts\AadPickerLibrary.js also uses hello [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="a5e5e-198">Assim, é necessário o projeto de tooyour tooadd jQuery UI.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-198">So you need tooadd jQuery UI tooyour project.</span></span> <span data-ttu-id="a5e5e-199">Clique com o botão direito do mouse em seu projeto e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="a5e5e-200">Em Olá NuGet Package Manager, clique em Procurar, tipo **jquery ui** Olá barra de pesquisa e clique em **jQuery.UI.Combined**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-200">In hello NuGet Package Manager, click Browse, type **jquery-ui** in hello search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="a5e5e-201">No painel direito da saudação, clique em **instalar**, em seguida, clique em **Okey** tooproceed.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-201">In hello right pane, click **Install**, then click **OK** tooproceed.</span></span>
13. <span data-ttu-id="a5e5e-202">Abra ~\App_Start\BundleConfig.cs e verifique Olá realçadas alterações a seguir:</span><span class="sxs-lookup"><span data-stu-id="a5e5e-202">Open ~\App_Start\BundleConfig.cs and make hello following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use hello development version of Modernizr toodevelop with and learn from. Then, when you&#39;re
        // ready for production, use hello build tool at http://modernizr.com toopick only hello tests you need.
        bundles.Add(new ScriptBundle(&quot;~/bundles/modernizr&quot;).Include(
                    &quot;~/Scripts/modernizr-*&quot;));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/bootstrap&quot;).Include(
                    &quot;~/Scripts/bootstrap.js&quot;,
                    &quot;~/Scripts/respond.js&quot;));
    
        bundles.Add(new StyleBundle(&quot;~/Content/css&quot;).Include(
                    &quot;~/Content/bootstrap.css&quot;,
                    &quot;~/Content/site.css&quot;<mark>,
                    &quot;~/Content/themes/base/jquery-ui.css&quot;</mark>));
    }
    </pre>
    
    <span data-ttu-id="a5e5e-203">Há toomanage de maneiras mais eficazes JavaScript e arquivos CSS em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-203">There are more performant ways toomanage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="a5e5e-204">No entanto, para manter a simplicidade você apenas vai toopiggyback em pacotes de saudação que serão carregados com cada exibição.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-204">However, for simplicity you're just going toopiggyback on hello bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="a5e5e-205">Por fim, em ~ \Global.asax, adicionar Olá a seguinte linha de código no hello `Application_Start()` método.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-205">Finally, in ~\Global.asax, add hello following line of code in hello `Application_Start()` method.</span></span> <span data-ttu-id="a5e5e-206">`Ctrl`+`.`em cada erro de resolução de nomes muito corrigi-lo.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-206">`Ctrl`+`.` on each naming resolution error too fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="a5e5e-207">Esta linha de código é necessário porque o modelo saudação padrão MVC usa <code>[ValidateAntiForgeryToken]</code> decoração em algumas das ações de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-207">You need this line of code because hello default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of hello actions.</span></span> <span data-ttu-id="a5e5e-208">Devido a toohello comportamento descrito por [Brock Allen](https://twitter.com/BrockLAllen) em [MVC 4, AntiForgeryToken e declarações](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) sua POSTAGEM HTTP pode falhar a validação de token antifalsificação porque:</span><span class="sxs-lookup"><span data-stu-id="a5e5e-208">Due toohello behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="a5e5e-209">Active Directory do Azure não envia http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider hello, que é requerido por padrão pelo token antifalsificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-209">Azure Active Directory does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by hello anti-forgery token.</span></span>
    > * <span data-ttu-id="a5e5e-210">Se o Active Directory do Azure é sincronizado com o AD FS de diretório, relação de confiança de saudação do AD FS por padrão não enviar Olá http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider declaração, embora você possa configurar manualmente o AD FS toosend Esta declaração.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-210">If Azure Active Directory is directory synced with AD FS, hello AD FS trust by default does not send hello http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS toosend this claim.</span></span>
    > 
    > <span data-ttu-id="a5e5e-211">`ClaimTypes.NameIdentifies`Especifica a declaração de saudação `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, que forneça Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-211">`ClaimTypes.NameIdentifies` specifies hello claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="a5e5e-212">Agora, publique suas alterações.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-212">Now, publish your changes.</span></span> <span data-ttu-id="a5e5e-213">Clique com o botão direito do mouse em seu projeto e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="a5e5e-214">Clique em **configurações**, verifique se há uma cadeia de caracteres de conexão tooyour banco de dados SQL, selecione **Atualizar banco de dados** toomake Olá alterações de esquema para o seu modelo e clique em **publicar** .</span><span class="sxs-lookup"><span data-stu-id="a5e5e-214">Click **Settings**, make sure there is a connection string tooyour SQL Database, select **Update Database** toomake hello schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="a5e5e-215">No navegador de hello, navegue toohttps: / /&lt;*appname*>.azurewebsites.net/workitems e clique em **criar novo**.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-215">In hello browser, navigate toohttps://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="a5e5e-216">Clique em Olá **AssignedToName** caixa.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-216">Click in hello **AssignedToName** box.</span></span> <span data-ttu-id="a5e5e-217">Agora você verá os usuários e grupos do seu locatário do Azure Active Directory em uma lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="a5e5e-218">Você pode digitar toofilter, ou usar Olá `Up` ou `Down` de chave ou clique tooselect Olá usuário ou grupo.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-218">You can type toofilter, or use hello `Up` or `Down` key or click tooselect hello user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="a5e5e-219">Clique em **criar** toosave alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-219">Click **Create** toosave hello changes.</span></span> <span data-ttu-id="a5e5e-220">Em seguida, clique em **editar** trabalho Olá criado item tooobserve Olá mesmo comportamento.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-220">Then, click **Edit** on hello created work item tooobserve hello same behavior.</span></span>

<span data-ttu-id="a5e5e-221">Parabéns, você está executando um aplicativo de linha de negócios no Azure com acesso ao diretório!</span><span class="sxs-lookup"><span data-stu-id="a5e5e-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="a5e5e-222">Há muito mais que você pode fazer com hello API do Graph.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-222">There's a lot more you can do with hello Graph API.</span></span> <span data-ttu-id="a5e5e-223">Consulte a [referência da API do Graph do Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="a5e5e-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="a5e5e-224">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="a5e5e-224">Next Step</span></span>
<span data-ttu-id="a5e5e-225">Se você precisar de controle de acesso baseado em função (RBAC) para seu aplicativo de linha de negócios no azure, consulte [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) para obter um exemplo da equipe do Active Directory do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from hello Azure Active Directory team.</span></span> <span data-ttu-id="a5e5e-226">Ele mostra como funções de tooenable para seu aplicativo do Active Directory do Azure e, em seguida, autorizar usuários com hello `[Authorize]` decoração.</span><span class="sxs-lookup"><span data-stu-id="a5e5e-226">It shows you how tooenable roles for your Azure Active Directory application, and then authorize users with hello `[Authorize]` decoration.</span></span>

<span data-ttu-id="a5e5e-227">Se seu aplicativo de linha de negócios precisa acessar dados tooon locais, consulte [acessar recursos usando conexões híbridas no serviço de aplicativo do Azure locais](web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a5e5e-227">If your line-of-business app needs access tooon-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="a5e5e-228">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="a5e5e-228">Further resources</span></span>
* [<span data-ttu-id="a5e5e-229">Autenticação e autorização no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="a5e5e-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="a5e5e-230">Autenticar com o Active Directory local em seu aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="a5e5e-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="a5e5e-231">Criar um aplicativo de linha de negócios no Azure com autenticação do AD FS</span><span class="sxs-lookup"><span data-stu-id="a5e5e-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="a5e5e-232">Autenticação do serviço de aplicativo e hello Azure AD Graph API</span><span class="sxs-lookup"><span data-stu-id="a5e5e-232">App Service Auth and hello Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="a5e5e-233">Exemplos e documentação do Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a5e5e-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="a5e5e-234">Tipos de declaração e token com suporte no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a5e5e-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)
