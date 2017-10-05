---
title: "Criar um aplicativo de linha de negócios do Azure com a autenticação do Azure Active Directory | Microsoft Docs"
description: "Saiba como criar um aplicativo de linha de negócios ASP.NET MVC no Serviço de Aplicativo do Azure que realiza a autenticação com o Azure Active Directory"
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
ms.openlocfilehash: 6eadf0a521a32c5bc580908e4e4b7f4305e2bf7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-line-of-business-azure-app-with-azure-active-directory-authentication"></a><span data-ttu-id="99f2e-103">Criar um aplicativo de linha de negócios do Azure com a autenticação do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99f2e-103">Create a line-of-business Azure app with Azure Active Directory authentication</span></span>
<span data-ttu-id="99f2e-104">Este artigo mostra como criar um aplicativo de linha de negócios do .NET nos [Aplicativos Web do Serviço de Aplicativo do Azure](http://go.microsoft.com/fwlink/?LinkId=529714) usando o recurso [Autenticação/Autorização](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99f2e-104">This article shows you how to create a .NET line-of-business app in [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714) using the [Authentication / Authorization](../app-service/app-service-authentication-overview.md) feature.</span></span> <span data-ttu-id="99f2e-105">Também mostra como usar a [API do Graph do Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) para consultar dados de diretório no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99f2e-105">It also shows how to use the [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to query directory data in the application.</span></span>

<span data-ttu-id="99f2e-106">O locatário do Azure Active Directory que você usa pode ser um diretório somente do Azure.</span><span class="sxs-lookup"><span data-stu-id="99f2e-106">The Azure Active Directory tenant that you use can be an Azure-only directory.</span></span> <span data-ttu-id="99f2e-107">Ou pode ser [sincronizado com seu Active Directory local](../active-directory/active-directory-aadconnect.md) para criar uma experiência de logon único para trabalhadores locais e remotos.</span><span class="sxs-lookup"><span data-stu-id="99f2e-107">Or, it can be [synced with your on-premises Active Directory](../active-directory/active-directory-aadconnect.md) to create a single sign-on experience for workers that are on-premises and remote.</span></span> <span data-ttu-id="99f2e-108">Este artigo usa o diretório padrão para sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="99f2e-108">This article uses the default directory for your Azure account.</span></span>

<a name="bkmk_build"></a>

## <a name="what-you-will-build"></a><span data-ttu-id="99f2e-109">O que você compilará</span><span class="sxs-lookup"><span data-stu-id="99f2e-109">What you will build</span></span>
<span data-ttu-id="99f2e-110">Você compilará um aplicativo simples de linha de negócios CRUD (Create-Read-Update-Delete) nos Aplicativos Web do Serviço de Aplicativo que acompanha itens de trabalho com os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="99f2e-110">You will build a simple line-of-business Create-Read-Update-Delete (CRUD) application in App Service Web Apps that tracks work items with the following features:</span></span>

* <span data-ttu-id="99f2e-111">Autentica usuários no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="99f2e-111">Authenticates users against Azure Active Directory</span></span>
* <span data-ttu-id="99f2e-112">Consulta usuários de diretório e grupos usando a [API do Graph do Azure Active Directory](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span><span class="sxs-lookup"><span data-stu-id="99f2e-112">Queries directory users and groups using [Azure Active Directory Graph API](http://msdn.microsoft.com/library/azure/hh974476.aspx)</span></span>
* <span data-ttu-id="99f2e-113">Usar o modelo *Sem Autenticação* do ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="99f2e-113">Use the ASP.NET MVC *No Authentication* template</span></span>

<span data-ttu-id="99f2e-114">Se você precisar de controle de acesso baseado em função (RBAC) para seu aplicativo de linha de negócios no Azure, confira a [Próxima etapa](#next).</span><span class="sxs-lookup"><span data-stu-id="99f2e-114">If you need role-based access control (RBAC) for your line-of-business app in Azure, see [Next Step](#next).</span></span>

<a name="bkmk_need"></a>

## <a name="what-you-need"></a><span data-ttu-id="99f2e-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="99f2e-115">What you need</span></span>
[!INCLUDE [free-trial-note](../../includes/free-trial-note.md)]

<span data-ttu-id="99f2e-116">É necessário o seguinte para concluir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="99f2e-116">You need the following to complete this tutorial:</span></span>

* <span data-ttu-id="99f2e-117">Um locatário do Active Directory do Azure com usuários em vários grupos</span><span class="sxs-lookup"><span data-stu-id="99f2e-117">An Azure Active Directory tenant with users in various groups</span></span>
* <span data-ttu-id="99f2e-118">Permissões para criar aplicativos no locatário do Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="99f2e-118">Permissions to create applications on the Azure Active Directory tenant</span></span>
* <span data-ttu-id="99f2e-119">Visual Studio 2013 Atualização 4 ou posterior</span><span class="sxs-lookup"><span data-stu-id="99f2e-119">Visual Studio 2013 Update 4 or later</span></span>
* [<span data-ttu-id="99f2e-120">SDK 2.8.1 do Azure ou posterior</span><span class="sxs-lookup"><span data-stu-id="99f2e-120">Azure SDK 2.8.1 or later</span></span>](https://azure.microsoft.com/downloads/)

<a name="bkmk_deploy"></a>

## <a name="create-and-deploy-a-web-app-to-azure"></a><span data-ttu-id="99f2e-121">Crie e implante um aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="99f2e-121">Create and deploy a web app to Azure</span></span>
1. <span data-ttu-id="99f2e-122">No Visual Studio, clique em **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-122">From Visual Studio, click **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="99f2e-123">Selecione **Aplicativo Web ASP.NET**, nomeie seu projeto e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-123">Select **ASP.NET Web Application**, name your project, and click **OK**.</span></span>
3. <span data-ttu-id="99f2e-124">Escolha o modelo **MVC** e altere a autenticação para **Sem Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-124">Select the **MVC** template, then change the authentication to **No Authentication**.</span></span> <span data-ttu-id="99f2e-125">Certifique-se de que a opção **Hospedar na Nuvem** esteja selecionada e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-125">Make sure **Host in the Cloud** is selected and click **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/1-create-mvc-no-authentication.png)
4. <span data-ttu-id="99f2e-126">Na caixa de diálogo **Criar Serviço de Aplicativo**, clique em **Adicionar uma conta** (e, depois, **Adicionar uma conta** na lista suspensa) para fazer logon em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="99f2e-126">In the **Create App Service** dialog, click **Add an account** (and then **Add an account** in the dropdown) to log in to your Azure account.</span></span>
5. <span data-ttu-id="99f2e-127">Depois de conectado, configure seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="99f2e-127">Once logged in configure your web app.</span></span> <span data-ttu-id="99f2e-128">Crie um grupo de recursos e um novo Plano do Serviço de Aplicativo clicando no respectivo botão **Novo** .</span><span class="sxs-lookup"><span data-stu-id="99f2e-128">Create a resource group and a new App Service plan by clicking the respective **New** button.</span></span> <span data-ttu-id="99f2e-129">Clique em **Explorar serviços adicionais do Azure** para continuar.</span><span class="sxs-lookup"><span data-stu-id="99f2e-129">Click **Explore additional Azure services** to continue.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/2-create-app-service.png)
6. <span data-ttu-id="99f2e-130">Na guia **Serviços**, clique em **+** para adicionar um Banco de Dados SQL para seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99f2e-130">In the **Services** tab, click **+** to add a SQL Database for your app.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/3-add-sql-database.png)
7. <span data-ttu-id="99f2e-131">Em **Configurar Banco de Dados SQL**, clique em **Novo** para criar uma instância do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="99f2e-131">In **Configure SQL Database**, click **New** to create a SQL Server instance.</span></span>
8. <span data-ttu-id="99f2e-132">Em **Configurar SQL Server**, configure sua instância do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="99f2e-132">In **Configure SQL Server**, configure your SQL Server instance.</span></span> <span data-ttu-id="99f2e-133">Em seguida, clique em **OK**, **OK** e em **Criar** para iniciar a criação do aplicativo no Azure.</span><span class="sxs-lookup"><span data-stu-id="99f2e-133">Then, click **OK**, **OK**, and **Create** to kick off the app creation in Azure.</span></span>
9. <span data-ttu-id="99f2e-134">Em **Atividade do Serviço de Aplicativo do Azure**, você pode ver quando a criação do aplicativo terminar.</span><span class="sxs-lookup"><span data-stu-id="99f2e-134">In **Azure App Service Activity**, you can see when the app creation is finished.</span></span> <span data-ttu-id="99f2e-135">Clique em **Publicar&lt;*nome_do_aplicativo*>para esse Aplicativo Web agora** e, em seguida, clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-135">Click **Publish &lt;*appname*> to this Web App now**, then click **Publish**.</span></span> 
   
    <span data-ttu-id="99f2e-136">Após a conclusão do Visual Studio, ele abrirá o aplicativo de publicação no navegador.</span><span class="sxs-lookup"><span data-stu-id="99f2e-136">Once Visual Studio finishes, it opens the publish app in the browser.</span></span> 
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/4-published-shown-in-browser.png)

<a name="bkmk_auth"></a>

## <a name="configure-authentication-and-directory-access"></a><span data-ttu-id="99f2e-137">Configurar a autenticação e acesso ao diretório</span><span class="sxs-lookup"><span data-stu-id="99f2e-137">Configure authentication and directory access</span></span>
1. <span data-ttu-id="99f2e-138">Faça logon no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="99f2e-138">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="99f2e-139">No meu à esquerda, clique em **Serviços de Aplicativos** > **&lt;*nome_do_aplicativo*>** > **Autenticação/Autorização**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-139">From the left menu, click **App Services** > **&lt;*appname*>** > **Authentication / Authorization**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/5-app-service-authentication.png)
3. <span data-ttu-id="99f2e-140">Ative a autenticação do Azure Active Directory clicando em **Ativar** > **Azure Active Directory** > **Expresso** > **OK**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-140">Turn on Azure Active Directory authentication by clicking **On** > **Azure Active Directory** > **Express** > **OK**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/6-authentication-express.png)
4. <span data-ttu-id="99f2e-141">Clique em **Salvar** na barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="99f2e-141">Click **Save** in the command bar.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/7-authentication-save.png)
   
    <span data-ttu-id="99f2e-142">Após a gravação das configurações de autenticação, tente navegar até seu aplicativo novamente no navegador.</span><span class="sxs-lookup"><span data-stu-id="99f2e-142">Once the authentication settings are saved successfully, try navigating to your app again in the browser.</span></span> <span data-ttu-id="99f2e-143">As configurações padrão impõem a autenticação em todo o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99f2e-143">Your default settings enforce authentication on the whole app.</span></span> <span data-ttu-id="99f2e-144">Se você ainda não estiver conectado, será redirecionado para uma tela de logon.</span><span class="sxs-lookup"><span data-stu-id="99f2e-144">If you aren't already logged in, you are redirected to a login screen.</span></span> <span data-ttu-id="99f2e-145">Depois de conectado, você verá seu aplicativo protegido por HTTPS.</span><span class="sxs-lookup"><span data-stu-id="99f2e-145">Once logged in, you see your app secured by HTTPS.</span></span> <span data-ttu-id="99f2e-146">Em seguida, será necessário habilitar o acesso aos dados do diretório.</span><span class="sxs-lookup"><span data-stu-id="99f2e-146">Next, you need to enable access to directory data.</span></span> 
5. <span data-ttu-id="99f2e-147">Navegue até o [Portal Clássico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="99f2e-147">Navigate to the [classic portal](https://manage.windowsazure.com).</span></span>
6. <span data-ttu-id="99f2e-148">No menu à esquerda, clique em **Active Directory** > **Diretório Padrão** > **Aplicativos** > **&lt;*nome_do_aplicativo*>**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-148">From the left menu, click **Active Directory** > **Default Directory** > **Applications** > **&lt;*appname*>**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/8-find-aad-application.png)
   
    <span data-ttu-id="99f2e-149">Este é o aplicativo do Azure Active Directory criado pelo Serviço de Aplicativo para você a fim de habilitar o recurso de Autorização/Autenticação.</span><span class="sxs-lookup"><span data-stu-id="99f2e-149">This is the Azure Active Directory application that App Service created for you to enable the Authorization / Authentication feature.</span></span>
7. <span data-ttu-id="99f2e-150">Clique em **Usuários** e **Grupos** para se certificar de que haja alguns usuários e grupos no diretório.</span><span class="sxs-lookup"><span data-stu-id="99f2e-150">Click **Users** and **Groups** to make sure that you have some users and groups in the directory.</span></span> <span data-ttu-id="99f2e-151">Caso contrário, crie alguns usuários e grupos de teste.</span><span class="sxs-lookup"><span data-stu-id="99f2e-151">If not, create a few test users and groups.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/9-create-users-groups.png)
8. <span data-ttu-id="99f2e-152">Clique em **Configurar** para configurar esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99f2e-152">Click **Configure** to configure this application.</span></span>
9. <span data-ttu-id="99f2e-153">Role para baixo até a seção **Chaves** e adicione uma chave selecionando uma duração.</span><span class="sxs-lookup"><span data-stu-id="99f2e-153">Scroll down to the **Keys** section and add a key by selecting a duration.</span></span> <span data-ttu-id="99f2e-154">Em seguida, clique em **Permissões Delegadas** e selecione **Ler dados do diretório**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-154">Then, click **Delegated Permissions** and select **Read directory data**.</span></span> 
   <span data-ttu-id="99f2e-155">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-155">Click **Save**.</span></span>
   
    ![](./media/web-sites-dotnet-lob-application-azure-ad/10-configure-aad-application.png)
10. <span data-ttu-id="99f2e-156">Depois que as configurações forem salvas, role para cima até a seção **Chaves** e clique no botão **Copiar** para copiar a chave do cliente.</span><span class="sxs-lookup"><span data-stu-id="99f2e-156">Once your settings are saved, scroll back up to the **Keys** section and click the **Copy** button to copy the client key.</span></span> 
    
     ![](./media/web-sites-dotnet-lob-application-azure-ad/11-get-app-key.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="99f2e-157">Se você sair desta página agora, não poderá acessar essa chave de cliente novamente.</span><span class="sxs-lookup"><span data-stu-id="99f2e-157">If you navigate away from this page now, you won't be able to access this client key ever again.</span></span>
    > 
    > 
11. <span data-ttu-id="99f2e-158">Em seguida, você precisará configurar seu aplicativo Web com essa chave.</span><span class="sxs-lookup"><span data-stu-id="99f2e-158">Next, you need to configure your web app with this key.</span></span> <span data-ttu-id="99f2e-159">Faça logon no [Azure Resource Manager](https://resources.azure.com) com sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="99f2e-159">Log in to the [Azure Resource Explorer](https://resources.azure.com) with your Azure account.</span></span>
12. <span data-ttu-id="99f2e-160">Na parte superior da página, clique em **Leitura/Gravação** para fazer alterações no Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="99f2e-160">At the top of the page, click **Read/Write** to make changes in the Azure Resource Explorer.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/12-resource-manager-writable.png)
13. <span data-ttu-id="99f2e-161">Encontre as configurações de autenticação de seu aplicativo, localizadas em assinaturas > **&lt;*nome_da_assinatura*>** > **resourceGroups** > **&lt;*nome_do_grupo_de_recursos*>** > **provedores** > **Microsoft.Web** > **sites** > **&lt;*nome_do_aplicativo*>** > **config** > **authsettings**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-161">Find the authentication settings for your app, located at subscriptions > **&lt;*subscriptionname*>** > **resourceGroups** > **&lt;*resourcegroupname*>** > **providers** > **Microsoft.Web** > **sites** > **&lt;*appname*>** > **config** > **authsettings**.</span></span>
14. <span data-ttu-id="99f2e-162">Clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-162">Click **Edit**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/13-edit-authsettings.png)
15. <span data-ttu-id="99f2e-163">No painel de edição, defina as propriedades `clientSecret` e `additionalLoginParams` da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="99f2e-163">In the editing pane, set the `clientSecret` and `additionalLoginParams` properties as follows.</span></span>
    
        ...
        "clientSecret": "<client key from the Azure Active Directory application>",
        ...
        "additionalLoginParams": ["response_type=code id_token", "resource=https://graph.windows.net"],
        ...
16. <span data-ttu-id="99f2e-164">Clique em **Inserir** na parte superior para enviar suas alterações.</span><span class="sxs-lookup"><span data-stu-id="99f2e-164">Click **Put** at the top to submit your changes.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/14-edit-parameters.png)
17. <span data-ttu-id="99f2e-165">Agora, para testar se você tem o token de autorização para acessar a API do Graph do Azure Active Directory, basta navegar até **https://&lt;*nome_do_aplicativo*>.azurewebsites.net/.auth/me** no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="99f2e-165">Now, to test if you have the authorization token to access the Azure Active Directory Graph API, just navigate to **https://&lt;*appname*>.azurewebsites.net/.auth/me** in your browser.</span></span> <span data-ttu-id="99f2e-166">Se você configurou tudo corretamente, veja a propriedade `access_token` na resposta JSON.</span><span class="sxs-lookup"><span data-stu-id="99f2e-166">If you configured everything correctly, you should see the `access_token` property in the JSON response.</span></span>
    
    <span data-ttu-id="99f2e-167">O caminho da URL de `~/.auth/me` é gerenciado pela Autenticação/Autorização do Serviço de Aplicativo para fornecer todas as informações relacionadas à sua sessão autenticada.</span><span class="sxs-lookup"><span data-stu-id="99f2e-167">The `~/.auth/me` URL path is managed by App Service Authentication / Authorization to give you all the information related to your authenticated session.</span></span> <span data-ttu-id="99f2e-168">Para saber mais, confira [Autenticação e autorização no Serviço de Aplicativo do Azure](../app-service/app-service-authentication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="99f2e-168">For more information, see [Authentication and authorization in Azure App Service](../app-service/app-service-authentication-overview.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="99f2e-169">O caminho da URL de `access_token` tem um período de expiração.</span><span class="sxs-lookup"><span data-stu-id="99f2e-169">The `access_token` has an expiration period.</span></span> <span data-ttu-id="99f2e-170">No entanto, a Autenticação/Autorização do Serviço de Aplicativo fornece a funcionalidade de atualização do token com `~/.auth/refresh`.</span><span class="sxs-lookup"><span data-stu-id="99f2e-170">However, App Service Authentication / Authorization provides token refresh functionality with `~/.auth/refresh`.</span></span> <span data-ttu-id="99f2e-171">Para saber mais sobre como usá-la, consulte [Repositório de Token do Serviço de Aplicativo](https://cgillum.tech/2016/03/07/app-service-token-store/).</span><span class="sxs-lookup"><span data-stu-id="99f2e-171">For more information on how to use it, see [App Service Token Store](https://cgillum.tech/2016/03/07/app-service-token-store/).</span></span>
    > 
    > 

<span data-ttu-id="99f2e-172">Em seguida, você fará algo útil com os dados do diretório.</span><span class="sxs-lookup"><span data-stu-id="99f2e-172">Next, you will do something useful with directory data.</span></span>

<a name="bkmk_crud"></a>

## <a name="add-line-of-business-functionality-to-your-app"></a><span data-ttu-id="99f2e-173">Adicionar uma funcionalidade de linha de negócios ao seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="99f2e-173">Add line-of-business functionality to your app</span></span>
<span data-ttu-id="99f2e-174">Agora, crie um rastreador de itens de trabalho CRUD simples.</span><span class="sxs-lookup"><span data-stu-id="99f2e-174">Now, you create a simple CRUD work items tracker.</span></span>  

1. <span data-ttu-id="99f2e-175">Na pasta ~\Modelos, crie um arquivo de classe chamado WorkItem.cs e substitua `public class WorkItem {...}`pelo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="99f2e-175">In the ~\Models folder, create a class file called WorkItem.cs, and replace `public class WorkItem {...}` with the following code:</span></span>
   
     <span data-ttu-id="99f2e-176">using System.ComponentModel.DataAnnotations;</span><span class="sxs-lookup"><span data-stu-id="99f2e-176">using System.ComponentModel.DataAnnotations;</span></span>
   
     <span data-ttu-id="99f2e-177">public class WorkItem   {</span><span class="sxs-lookup"><span data-stu-id="99f2e-177">public class WorkItem   {</span></span>
   
         [Key]
         public int ItemID { get; set; }
         public string AssignedToID { get; set; }
         public string AssignedToName { get; set; }
         public string Description { get; set; }
         public WorkItemStatus Status { get; set; }
     <span data-ttu-id="99f2e-178">}</span><span class="sxs-lookup"><span data-stu-id="99f2e-178">}</span></span>
   
     <span data-ttu-id="99f2e-179">public enum WorkItemStatus   {</span><span class="sxs-lookup"><span data-stu-id="99f2e-179">public enum WorkItemStatus   {</span></span>
   
         Open,
         Investigating,
         Resolved,
         Closed
     <span data-ttu-id="99f2e-180">}</span><span class="sxs-lookup"><span data-stu-id="99f2e-180">}</span></span>
2. <span data-ttu-id="99f2e-181">Compile o projeto para disponibilizar o novo modelo para a lógica de scaffolding no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="99f2e-181">Build the project to make your new model accessible to the scaffolding logic in Visual Studio.</span></span>
3. <span data-ttu-id="99f2e-182">Adicione um novo item com scaffold `WorkItemsController` à pasta ~\Controllers (clique com o botão direito do mouse em **Controladores**, aponte para **Adicionar** e selecione **Novo item com scaffold**).</span><span class="sxs-lookup"><span data-stu-id="99f2e-182">Add a new scaffolded item `WorkItemsController` to the ~\Controllers folder (right-click **Controllers**, point to **Add**, and select **New scaffolded item**).</span></span> 
4. <span data-ttu-id="99f2e-183">Selecione **Controlador MVC 5 com modos de exibição usando o Entity Framework** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-183">Select **MVC 5 Controller with views, using Entity Framework** and click **Add**.</span></span>
5. <span data-ttu-id="99f2e-184">Escolha o modelo que você criou e clique em **+** e em **Adicionar** para adicionar um contexto de dados. Em seguida, clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-184">Select the model that you created, then click **+** and then **Add** to add a data context, and then click **Add**.</span></span>
   
   ![](./media/web-sites-dotnet-lob-application-azure-ad/16-add-scaffolded-controller.png)
6. <span data-ttu-id="99f2e-185">Em ~\Views\WorkItems\Create.cshtml (um item automaticamente submetido a scaffolding), localize o método auxiliar `Html.BeginForm` e faça as seguintes alterações destacadas:</span><span class="sxs-lookup"><span data-stu-id="99f2e-185">In ~\Views\WorkItems\Create.cshtml (an automatically scaffolded item), find the `Html.BeginForm` helper method and make the following highlighted changes:</span></span>  
   
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
    @Html.ActionLink(&quot;Back to List&quot;, &quot;Index&quot;)
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
   
        // Submit the selected user/group to be asssigned.
        $(&quot;#submit-button&quot;).click({ picker: picker }, function () {
            if (!picker.Selected())
                return;
            $(&quot;#main-form&quot;).get()[0].elements[&quot;AssignedToID&quot;].value = picker.Selected().objectId;
        });
    &lt;/script&gt;</mark>
   }
   </pre>
   
   <span data-ttu-id="99f2e-186">Observe que `token` e `tenant` são usados pelo objeto `AadPicker` para fazer chamadas da API do Graph do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="99f2e-186">Note that `token` and `tenant` are used by the `AadPicker` object to make Azure Active Directory Graph API calls.</span></span> <span data-ttu-id="99f2e-187">Você adicionará `AadPicker` mais tarde.</span><span class="sxs-lookup"><span data-stu-id="99f2e-187">You'll add `AadPicker` later.</span></span>     
   
   > [!NOTE]
   > <span data-ttu-id="99f2e-188">Você também pode obter `token` e `tenant` do lado do cliente com `~/.auth/me`, mas isso seria uma chamada de servidor adicional.</span><span class="sxs-lookup"><span data-stu-id="99f2e-188">You can just as well get `token` and `tenant` from the client side with `~/.auth/me`, but that would be an additional server call.</span></span> <span data-ttu-id="99f2e-189">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="99f2e-189">For example:</span></span>
   > 
   > <span data-ttu-id="99f2e-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span><span class="sxs-lookup"><span data-stu-id="99f2e-190">$.ajax({ dataType: "json", url: "/.auth/me", success: function (data) { var token = data[0].access_token; var tenant = data[0].user_claims .find(c => c.typ === 'http://schemas.microsoft.com/identity/claims/tenantid') .val; } });</span></span>
   > 
   > 
7. <span data-ttu-id="99f2e-191">Faça as mesmas alterações com ~\Views\WorkItems\Edit.cshtml.</span><span class="sxs-lookup"><span data-stu-id="99f2e-191">Make the same changes with ~\Views\WorkItems\Edit.cshtml.</span></span>
8. <span data-ttu-id="99f2e-192">O objeto `AadPicker` é definido em um script ao qual você precisa adicionar ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="99f2e-192">The `AadPicker` object is defined in a script that you need to add to your project.</span></span> <span data-ttu-id="99f2e-193">Clique com o botão direito do mouse na pasta ~\Scripts, aponte para **Adicionar** e clique em **arquivo JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-193">Right-click the ~\Scripts folder, point to **Add**, and click **JavaScript file**.</span></span> <span data-ttu-id="99f2e-194">Digite `AadPickerLibrary` para o nome de arquivo e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-194">Type `AadPickerLibrary` for the filename and click **OK**.</span></span>
9. <span data-ttu-id="99f2e-195">Copie o conteúdo deste [local](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) em ~\Scripts\AadPickerLibrary.js.</span><span class="sxs-lookup"><span data-stu-id="99f2e-195">Copy the content from [here](https://raw.githubusercontent.com/cephalin/active-directory-dotnet-webapp-roleclaims/master/WebApp-RoleClaims-DotNet/Scripts/AadPickerLibrary.js) into ~\Scripts\AadPickerLibrary.js.</span></span>
   
   <span data-ttu-id="99f2e-196">No script, o objeto `AadPicker` chama a [API do Graph do Azure Active Directory](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) para pesquisar usuários e grupos que correspondam à entrada.</span><span class="sxs-lookup"><span data-stu-id="99f2e-196">In the script, the `AadPicker` object calls [Azure Active Directory Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) to search for users and groups that match the input.</span></span>  
10. <span data-ttu-id="99f2e-197">~\Scripts\AadPickerLibrary.js também usa o [widget Autocomplete do jQuery UI](https://jqueryui.com/autocomplete/).</span><span class="sxs-lookup"><span data-stu-id="99f2e-197">~\Scripts\AadPickerLibrary.js also uses the [jQuery UI Autocomplete widget](https://jqueryui.com/autocomplete/).</span></span> <span data-ttu-id="99f2e-198">Portanto, você precisa adicionar o jQuery UI ao seu projeto.</span><span class="sxs-lookup"><span data-stu-id="99f2e-198">So you need to add jQuery UI to your project.</span></span> <span data-ttu-id="99f2e-199">Clique com o botão direito do mouse em seu projeto e clique em **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-199">Right-click your project in and click **Manage NuGet Packages**.</span></span>
11. <span data-ttu-id="99f2e-200">No Gerenciador de Pacotes NuGet, clique em Procurar, digite **jquery-ui** na barra de pesquisa e clique em **jQuery.UI.Combined**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-200">In the NuGet Package Manager, click Browse, type **jquery-ui** in the search bar, and click **jQuery.UI.Combined**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/17-add-jquery-ui-nuget.png)
12. <span data-ttu-id="99f2e-201">No painel à direita, clique em **Instalar** e em **OK** para continuar.</span><span class="sxs-lookup"><span data-stu-id="99f2e-201">In the right pane, click **Install**, then click **OK** to proceed.</span></span>
13. <span data-ttu-id="99f2e-202">Abra ~\App_Start\BundleConfig.cs e faça as seguintes alterações realçadas:</span><span class="sxs-lookup"><span data-stu-id="99f2e-202">Open ~\App_Start\BundleConfig.cs and make the following highlighted changes:</span></span>  
    
    <pre class="prettyprint">
    public static void RegisterBundles(BundleCollection bundles)
    {
        bundles.Add(new ScriptBundle(&quot;~/bundles/jquery&quot;).Include(
                    &quot;~/Scripts/jquery-{version}.js&quot;<mark>,
                    &quot;~/Scripts/jquery-ui-{version}.js&quot;,
                    &quot;~/Scripts/AadPickerLibrary.js&quot;</mark>));
    
        bundles.Add(new ScriptBundle(&quot;~/bundles/jqueryval&quot;).Include(
                    &quot;~/Scripts/jquery.validate*&quot;));
    
        // Use the development version of Modernizr to develop with and learn from. Then, when you&#39;re
        // ready for production, use the build tool at http://modernizr.com to pick only the tests you need.
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
    
    <span data-ttu-id="99f2e-203">Há outras maneiras de alto desempenho para gerenciar arquivos JavaScript e CSS em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99f2e-203">There are more performant ways to manage JavaScript and CSS files in your app.</span></span> <span data-ttu-id="99f2e-204">No entanto, para manter a simplicidade, apenas acumule os pacotes carregados com cada exibição.</span><span class="sxs-lookup"><span data-stu-id="99f2e-204">However, for simplicity you're just going to piggyback on the bundles that are loaded with every view.</span></span>
14. <span data-ttu-id="99f2e-205">Por fim, em ~\Global.asax, adicione a linha de código a seguir ao método `Application_Start()`.</span><span class="sxs-lookup"><span data-stu-id="99f2e-205">Finally, in ~\Global.asax, add the following line of code in the `Application_Start()` method.</span></span> <span data-ttu-id="99f2e-206">`Ctrl`+`.` em cada erro de resolução de nomes para corrigi-lo.</span><span class="sxs-lookup"><span data-stu-id="99f2e-206">`Ctrl`+`.` on each naming resolution error to fix it.</span></span>
    
        AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.NameIdentifier;
    
    > [!NOTE]
    > <span data-ttu-id="99f2e-207">Você precisa dessa linha de código porque o modelo padrão de MVC usa a decoração <code>[ValidateAntiForgeryToken]</code> em algumas das ações.</span><span class="sxs-lookup"><span data-stu-id="99f2e-207">You need this line of code because the default MVC template uses <code>[ValidateAntiForgeryToken]</code> decoration on some of the actions.</span></span> <span data-ttu-id="99f2e-208">Devido ao comportamento descrito por [Brock Allen](https://twitter.com/BrockLAllen) em [MVC 4, AntiForgeryToken e declarações](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/), seu HTTP POST poderá falhar na validação do token antifalsificação pelos seguintes motivos:</span><span class="sxs-lookup"><span data-stu-id="99f2e-208">Due to the behavior described by [Brock Allen](https://twitter.com/BrockLAllen) at [MVC 4, AntiForgeryToken and Claims](http://brockallen.com/2012/07/08/mvc-4-antiforgerytoken-and-claims/) your HTTP POST may fail anti-forgery token validation because:</span></span>
    > 
    > * <span data-ttu-id="99f2e-209">O Azure Active Directory não envia http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, que é exigido por padrão pelo token antifalsificação.</span><span class="sxs-lookup"><span data-stu-id="99f2e-209">Azure Active Directory does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, which is required by default by the anti-forgery token.</span></span>
    > * <span data-ttu-id="99f2e-210">Se o Azure Active Directory for um diretório sincronizado com o AD FS, a relação de confiança do AD FS por padrão não envia a declaração http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider, embora você possa configurar manualmente o AD FS para enviá-la.</span><span class="sxs-lookup"><span data-stu-id="99f2e-210">If Azure Active Directory is directory synced with AD FS, the AD FS trust by default does not send the http://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider claim either, although you can manually configure AD FS to send this claim.</span></span>
    > 
    > <span data-ttu-id="99f2e-211">`ClaimTypes.NameIdentifies` especifica a declaração `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, que o Active Directory do Azure fornece.</span><span class="sxs-lookup"><span data-stu-id="99f2e-211">`ClaimTypes.NameIdentifies` specifies the claim `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier`, which Azure Active Directory does supply.</span></span>  
    > 
    > 
15. <span data-ttu-id="99f2e-212">Agora, publique suas alterações.</span><span class="sxs-lookup"><span data-stu-id="99f2e-212">Now, publish your changes.</span></span> <span data-ttu-id="99f2e-213">Clique com o botão direito do mouse em seu projeto e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-213">Right-click your project and click **Publish**.</span></span>
16. <span data-ttu-id="99f2e-214">Clique em **Configurações**, verifique se há uma cadeia de conexão com seu Banco de Dados SQL, escolha **Atualizar Banco de Dados** para fazer as alterações de esquema no modelo e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-214">Click **Settings**, make sure there is a connection string to your SQL Database, select **Update Database** to make the schema changes for your model, and click **Publish**.</span></span>
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/18-publish-crud-changes.png)
17. <span data-ttu-id="99f2e-215">No navegador, navegue até https://&lt;*nome_do_aplicativo*>.azurewebsites.net/workitems e clique em **Criar Novo**.</span><span class="sxs-lookup"><span data-stu-id="99f2e-215">In the browser, navigate to https://&lt;*appname*>.azurewebsites.net/workitems and click **Create New**.</span></span>
18. <span data-ttu-id="99f2e-216">Clique na caixa **AssignedToName** .</span><span class="sxs-lookup"><span data-stu-id="99f2e-216">Click in the **AssignedToName** box.</span></span> <span data-ttu-id="99f2e-217">Agora você verá os usuários e grupos do seu locatário do Azure Active Directory em uma lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="99f2e-217">You should now see users and groups from your Azure Active Directory tenant in a dropdown.</span></span> <span data-ttu-id="99f2e-218">Você pode digitar para filtrar ou usar a tecla `Up` ou `Down` ou clicar para selecionar o usuário ou grupo.</span><span class="sxs-lookup"><span data-stu-id="99f2e-218">You can type to filter, or use the `Up` or `Down` key or click to select the user or group.</span></span> 
    
    ![](./media/web-sites-dotnet-lob-application-azure-ad/19-use-aadpicker.png)
19. <span data-ttu-id="99f2e-219">Clique em **Criar** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="99f2e-219">Click **Create** to save the changes.</span></span> <span data-ttu-id="99f2e-220">Em seguida, clique em **Editar** no item de trabalho criado para observar o mesmo comportamento.</span><span class="sxs-lookup"><span data-stu-id="99f2e-220">Then, click **Edit** on the created work item to observe the same behavior.</span></span>

<span data-ttu-id="99f2e-221">Parabéns, você está executando um aplicativo de linha de negócios no Azure com acesso ao diretório!</span><span class="sxs-lookup"><span data-stu-id="99f2e-221">Congrats, you are now running a line-of-business app in Azure with directory access!</span></span> <span data-ttu-id="99f2e-222">Você pode fazer muito mais com a API do Graph.</span><span class="sxs-lookup"><span data-stu-id="99f2e-222">There's a lot more you can do with the Graph API.</span></span> <span data-ttu-id="99f2e-223">Consulte a [referência da API do Graph do Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span><span class="sxs-lookup"><span data-stu-id="99f2e-223">See [Azure AD Graph API reference](https://msdn.microsoft.com/library/azure/ad/graph/api/api-catalog).</span></span>

<a name="next"></a>

## <a name="next-step"></a><span data-ttu-id="99f2e-224">Próxima etapa</span><span class="sxs-lookup"><span data-stu-id="99f2e-224">Next Step</span></span>
<span data-ttu-id="99f2e-225">Se você precisar de controle de acesso baseado em função (RBAC) para o aplicativo de linha de negócios no Azure, confira [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) para obter um exemplo da equipe do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="99f2e-225">If you need role-based access control (RBAC) for your line-of-business app in azure, see [WebApp-RoleClaims-DotNet](https://github.com/Azure-Samples/active-directory-dotnet-webapp-roleclaims) for a sample from the Azure Active Directory team.</span></span> <span data-ttu-id="99f2e-226">Ele mostra como habilitar funções para seu aplicativo do Azure Active Directory e, em seguida, autorizar usuários com a decoração `[Authorize]` .</span><span class="sxs-lookup"><span data-stu-id="99f2e-226">It shows you how to enable roles for your Azure Active Directory application, and then authorize users with the `[Authorize]` decoration.</span></span>

<span data-ttu-id="99f2e-227">Se o seu aplicativo de linha de negócios precisar acessar dados locais, confira [Acesso a recursos locais usando conexões híbridas no Serviço de Aplicativo do Azure](web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="99f2e-227">If your line-of-business app needs access to on-premises data, see [Access on-premises resources using hybrid connections in Azure App Service](web-sites-hybrid-connection-get-started.md).</span></span>

<a name="bkmk_resources"></a>

## <a name="further-resources"></a><span data-ttu-id="99f2e-228">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="99f2e-228">Further resources</span></span>
* [<span data-ttu-id="99f2e-229">Autenticação e autorização no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="99f2e-229">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)
* [<span data-ttu-id="99f2e-230">Autenticar com o Active Directory local em seu aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="99f2e-230">Authenticate with on-premises Active Directory in your Azure app</span></span>](web-sites-authentication-authorization.md)
* [<span data-ttu-id="99f2e-231">Criar um aplicativo de linha de negócios no Azure com autenticação do AD FS</span><span class="sxs-lookup"><span data-stu-id="99f2e-231">Create a line-of-business app in Azure with AD FS authentication</span></span>](web-sites-dotnet-lob-application-adfs.md)
* [<span data-ttu-id="99f2e-232">Autenticação do Serviço de Aplicativo e a API do Graph do Azure AD</span><span class="sxs-lookup"><span data-stu-id="99f2e-232">App Service Auth and the Azure AD Graph API</span></span>](https://cgillum.tech/2016/03/25/app-service-auth-aad-graph-api/)
* [<span data-ttu-id="99f2e-233">Exemplos e documentação do Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="99f2e-233">Microsoft Azure Active Directory Samples and Documentation</span></span>](https://github.com/AzureADSamples)
* [<span data-ttu-id="99f2e-234">Tipos de declaração e token com suporte no Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="99f2e-234">Azure Active Directory Supported Token and Claim Types</span></span>](http://msdn.microsoft.com/library/azure/dn195587.aspx)
