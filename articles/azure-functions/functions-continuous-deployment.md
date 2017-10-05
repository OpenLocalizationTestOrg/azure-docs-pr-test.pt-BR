---
title: "Implantação contínua do Azure Functions | Microsoft Docs"
description: "Use recursos de implantação contínua do Serviço de Aplicativo do Azure para publicar seu Azure Functions."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 3756f1a039730bfd99b0375ce9bfeaf27178f2e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="66dc7-103">Implantação contínua para Azure Functions</span><span class="sxs-lookup"><span data-stu-id="66dc7-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="66dc7-104">As Funções do Azure facilitam a implantação do seu aplicativo de função utilizando a integração contínua do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="66dc7-104">Azure Functions makes it easy to deploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="66dc7-105">Funções integram BitBucket, Dropbox, GitHub e Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="66dc7-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="66dc7-106">Isso permite que um fluxo de trabalho em que atualizações de código de função feitas utilizando um desses serviços integrados acione a implantação ao Azure.</span><span class="sxs-lookup"><span data-stu-id="66dc7-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment to Azure.</span></span> <span data-ttu-id="66dc7-107">Se você for iniciante no Azure Functions, comece pela [Visão geral do Azure Functions](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66dc7-107">If you are new to Azure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="66dc7-108">A implantação contínua é uma ótima opção para projetos nos quais várias contribuições frequentes são integradas.</span><span class="sxs-lookup"><span data-stu-id="66dc7-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="66dc7-109">Ele também permite manter o controle do código-fonte no código de funções.</span><span class="sxs-lookup"><span data-stu-id="66dc7-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="66dc7-110">As seguintes fontes de implantação têm suporte atualmente:</span><span class="sxs-lookup"><span data-stu-id="66dc7-110">The following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="66dc7-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="66dc7-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="66dc7-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="66dc7-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="66dc7-113">Repositório externo (Git ou Mercurial)</span><span class="sxs-lookup"><span data-stu-id="66dc7-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="66dc7-114">Repositório local Git</span><span class="sxs-lookup"><span data-stu-id="66dc7-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="66dc7-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="66dc7-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="66dc7-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="66dc7-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="66dc7-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="66dc7-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="66dc7-118">As implantações são configuradas para cada aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="66dc7-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="66dc7-119">Após a implantação contínua ser habilitada, o acesso ao código de função no portal é definido como *somente leitura*.</span><span class="sxs-lookup"><span data-stu-id="66dc7-119">After continuous deployment is enabled, access to function code in the portal is set to *read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="66dc7-120">Requisitos de implantação contínua</span><span class="sxs-lookup"><span data-stu-id="66dc7-120">Continuous deployment requirements</span></span>

<span data-ttu-id="66dc7-121">Você deve ter a fonte de implantação configurada e o código de funções na fonte de implantação antes de configurar a implantação contínua.</span><span class="sxs-lookup"><span data-stu-id="66dc7-121">You must have your deployment source configured and your functions code in the deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="66dc7-122">Em uma implantação de aplicativo de funções específica, cada função reside em um subdiretório nomeado, em que o nome do diretório é o nome da função.</span><span class="sxs-lookup"><span data-stu-id="66dc7-122">In a given function app deployment, each function lives in a named subdirectory, where the directory name is the name of the function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="66dc7-123">Configurar a implantação contínua</span><span class="sxs-lookup"><span data-stu-id="66dc7-123">Set up continuous deployment</span></span>
<span data-ttu-id="66dc7-124">Utilize o procedimento a seguir para configurar a implantação contínua para um aplicativo de função existente.</span><span class="sxs-lookup"><span data-stu-id="66dc7-124">Use this procedure to configure continuous deployment for an existing function app.</span></span> <span data-ttu-id="66dc7-125">Essas etapas demonstram a integração com um repositório GitHub, porém etapas semelhantes se aplicam para serviços do Visual Studio Team Services ou outros serviços de implantação.</span><span class="sxs-lookup"><span data-stu-id="66dc7-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="66dc7-126">Em seu aplicativo de função no [portal do Azure](https://portal.azure.com), clique em **Recursos da plataforma** e **Opções de implantação**.</span><span class="sxs-lookup"><span data-stu-id="66dc7-126">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Configurar a implantação contínua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="66dc7-128">Em seguida, na folha **Implantações**, clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="66dc7-128">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Configurar a implantação contínua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="66dc7-130">Na folha **Origem da implantação**, clique em **Escolher fonte**, preencha as informações da origem de implantação escolhida e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="66dc7-130">In the **Deployment source** blade, click **Choose source**, then fill in the information for your chosen deployment source and click **OK**.</span></span>
   
    ![Escolher a fonte de implantação](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="66dc7-132">Após a implantação contínua ser configurada, todas as alterações de arquivos na fonte de implantação são copiadas para o aplicativo de função e uma implantação completa do site é disparada.</span><span class="sxs-lookup"><span data-stu-id="66dc7-132">After continuous deployment is configured, all file changes in your deployment source are copied to the function app and a full site deployment is triggered.</span></span> <span data-ttu-id="66dc7-133">O site é reimplantado quando os arquivos da origem são atualizados.</span><span class="sxs-lookup"><span data-stu-id="66dc7-133">The site is redeployed when files in the source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="66dc7-134">Opções de implantação</span><span class="sxs-lookup"><span data-stu-id="66dc7-134">Deployment options</span></span>

<span data-ttu-id="66dc7-135">A seguir estão alguns cenários comuns de implantação:</span><span class="sxs-lookup"><span data-stu-id="66dc7-135">The following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="66dc7-136">Criar uma implantação de preparo</span><span class="sxs-lookup"><span data-stu-id="66dc7-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="66dc7-137">Mover as funções existentes para implantação contínua</span><span class="sxs-lookup"><span data-stu-id="66dc7-137">Move existing functions to continuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="66dc7-138">Criar uma implantação de preparo</span><span class="sxs-lookup"><span data-stu-id="66dc7-138">Create a staging deployment</span></span>

<span data-ttu-id="66dc7-139">Aplicativos de Função ainda não dão suporte a slots de implantação.</span><span class="sxs-lookup"><span data-stu-id="66dc7-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="66dc7-140">No entanto, você ainda pode gerenciar implantações de produção e preparo separadas usando a integração contínua.</span><span class="sxs-lookup"><span data-stu-id="66dc7-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="66dc7-141">O processo para configurar e trabalhar com uma implantação de preparo geralmente tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="66dc7-141">The process to configure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="66dc7-142">Crie dois aplicativos de função em sua assinatura, um para o código de produção e outro para preparo.</span><span class="sxs-lookup"><span data-stu-id="66dc7-142">Create two function apps in your subscription, one for the production code and one for staging.</span></span> 

2. <span data-ttu-id="66dc7-143">Crie uma fonte de implantação, se você ainda não tiver uma.</span><span class="sxs-lookup"><span data-stu-id="66dc7-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="66dc7-144">Este exemplo usa [GitHub].</span><span class="sxs-lookup"><span data-stu-id="66dc7-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="66dc7-145">Para o aplicativo de funções de produção, conclua as etapas acima em **Configurar a implantação contínua** e defina a ramificação de implantação para a ramificação mestra do repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="66dc7-145">For your production function app, complete the preceding steps in **Set up continuous deployment** and set the deployment branch to the master branch of your GitHub repository.</span></span>
   
    ![Escolher a ramificação de implantação](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="66dc7-147">Repita essa etapa para o aplicativo de funções de preparo, mas escolha a ramificação de preparo em vez do repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="66dc7-147">Repeat this step for the staging function app, but choose the staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="66dc7-148">Se sua fonte de implantação não der suporte à ramificação, use uma pasta diferente.</span><span class="sxs-lookup"><span data-stu-id="66dc7-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="66dc7-149">Faça atualizações no código na ramificação de preparo ou na pasta e verifique se as alterações são refletidas na implantação de preparo.</span><span class="sxs-lookup"><span data-stu-id="66dc7-149">Make updates to your code in the staging branch or folder, then verify that those changes are reflected in the staging deployment.</span></span>

6. <span data-ttu-id="66dc7-150">Depois de testar, mescle alterações da ramificação de preparo na ramificação mestre.</span><span class="sxs-lookup"><span data-stu-id="66dc7-150">After testing, merge changes from the staging branch into the master branch.</span></span> <span data-ttu-id="66dc7-151">Essa mesclagem disparará a implantação para o aplicativo de função de produção.</span><span class="sxs-lookup"><span data-stu-id="66dc7-151">This merge triggers deployment to the production function app.</span></span> <span data-ttu-id="66dc7-152">Se sua fonte de implantação não der suporte a ramificações, substitua os arquivos na pasta de produção pelos arquivos da pasta de preparo.</span><span class="sxs-lookup"><span data-stu-id="66dc7-152">If your deployment source doesn't support branches, overwrite the files in the production folder with the files from the staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-to-continuous-deployment"></a><span data-ttu-id="66dc7-153">Mover as funções existentes para implantação contínua</span><span class="sxs-lookup"><span data-stu-id="66dc7-153">Move existing functions to continuous deployment</span></span>
<span data-ttu-id="66dc7-154">Quando houver funções existentes que você criou e manteve no portal, será preciso baixar os arquivos de código de função existentes usando o FTP ou o repositório Git local para poder configurar a implantação contínua conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="66dc7-154">When you have existing functions that you have created and maintained in the portal, you need to download your existing function code files using FTP or the local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="66dc7-155">Você pode fazer isso nas configurações do Serviço de Aplicativo para seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="66dc7-155">You can do this in the App Service settings for your function app.</span></span> <span data-ttu-id="66dc7-156">Depois que os arquivos forem baixados, você poderá carregá-los na fonte de implantação contínua escolhida.</span><span class="sxs-lookup"><span data-stu-id="66dc7-156">After your files are downloaded, you can upload them to your chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="66dc7-157">Depois de configurar a integração contínua, você não poderá mais editar os arquivos de origem no portal de Funções.</span><span class="sxs-lookup"><span data-stu-id="66dc7-157">After you configure continuous integration, you will no longer be able to edit your source files in the Functions portal.</span></span>

- [<span data-ttu-id="66dc7-158">Como configurar credenciais de implantação</span><span class="sxs-lookup"><span data-stu-id="66dc7-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="66dc7-159">Como baixar arquivos usando FTP</span><span class="sxs-lookup"><span data-stu-id="66dc7-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="66dc7-160">Como: baixar arquivos usando o repositório Git local</span><span class="sxs-lookup"><span data-stu-id="66dc7-160">How to: Download files using the local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="66dc7-161">Como: configurar credenciais de implantação</span><span class="sxs-lookup"><span data-stu-id="66dc7-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="66dc7-162">Antes de baixar arquivos do aplicativo de funções com o FTP ou repositório Git local, você deve configurar suas credenciais para acessar o site.</span><span class="sxs-lookup"><span data-stu-id="66dc7-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials to access the site.</span></span> <span data-ttu-id="66dc7-163">As credenciais são definidas no nível do aplicativo de Função.</span><span class="sxs-lookup"><span data-stu-id="66dc7-163">Credentials are set at the Function app level.</span></span> <span data-ttu-id="66dc7-164">Utilize as etapas a seguir para definir as credenciais de implantação no portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="66dc7-164">Use the following steps to set deployment credentials in the Azure portal:</span></span>

1. <span data-ttu-id="66dc7-165">Em seu aplicativo de função no [portal do Azure](https://portal.azure.com), clique em **Recursos da plataforma** e **Credenciais de implantação**.</span><span class="sxs-lookup"><span data-stu-id="66dc7-165">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Definir credenciais de implantação local](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="66dc7-167">Digite um nome de usuário e senha e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="66dc7-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="66dc7-168">Agora você pode usar essas credenciais para acessar seu aplicativo de função do FTP ou do repositório Git interno.</span><span class="sxs-lookup"><span data-stu-id="66dc7-168">You can now use these credentials to access your function app from FTP or the built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="66dc7-169">Como: baixar arquivos usando FTP</span><span class="sxs-lookup"><span data-stu-id="66dc7-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="66dc7-170">No aplicativo de função do [Portal do Azure](https://portal.azure.com), clique em **recursos de Plataforma**e **Propriedades**, e copie os valores para **Usuário de FTP/Implantação**,**Nome do Host FTP** e**Nome de Host FTPS**.</span><span class="sxs-lookup"><span data-stu-id="66dc7-170">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy the values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="66dc7-171">O **Usuário de FTP/Implantação** deve ser inserido conforme exibido no portal, incluindo o nome do aplicativo, a fim de fornecer o contexto adequado para o servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="66dc7-171">**FTP/Deployment User** must be entered as displayed in the portal, including the app name, to provide proper context for the FTP server.</span></span>
   
    ![Obter as informações de implantação](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="66dc7-173">No cliente de FTP, use as informações de conexão coletadas para se conectar ao aplicativo e baixar os arquivos de origem para suas funções.</span><span class="sxs-lookup"><span data-stu-id="66dc7-173">From your FTP client, use the connection information you gathered to connect to your app and download the source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="66dc7-174">Como: baixar arquivos usando o repositório Git local</span><span class="sxs-lookup"><span data-stu-id="66dc7-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="66dc7-175">Em seu aplicativo de função no [portal do Azure](https://portal.azure.com), clique em **Recursos da plataforma** e **Opções de implantação**.</span><span class="sxs-lookup"><span data-stu-id="66dc7-175">In your function app in the [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Configurar a implantação contínua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="66dc7-177">Em seguida, na folha **Implantações**, clique em **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="66dc7-177">Then in the **Deployments** blade click **Setup**.</span></span>
 
    ![Configurar a implantação contínua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="66dc7-179">Na folha **Fonte de implantações**, clique em**Repositório Git Local** e em seguida clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="66dc7-179">In the **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="66dc7-180">Em **Recursos da plataforma**, clique em **Propriedades** e observe o valor da URL de Git.</span><span class="sxs-lookup"><span data-stu-id="66dc7-180">In **Platform features**, click **Properties** and note the value of Git URL.</span></span> 
   
    ![Configurar a implantação contínua](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="66dc7-182">Faça uma cópia do repositório em seu computador local usando uma linha de comando com reconhecimento do Git ou sua ferramenta de Git favorita.</span><span class="sxs-lookup"><span data-stu-id="66dc7-182">Clone the repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="66dc7-183">O comando Git clone é semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="66dc7-183">The Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="66dc7-184">Busque arquivos de seu aplicativo de função para o clone no computador local, como no seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="66dc7-184">Fetch files from your function app to the clone on your local computer, as in the following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="66dc7-185">Se solicitado, forneça as [credenciais de implantação configuradas](#credentials).</span><span class="sxs-lookup"><span data-stu-id="66dc7-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

<span data-ttu-id="66dc7-186">[GitHub]: https://github.com/</span><span class="sxs-lookup"><span data-stu-id="66dc7-186">[GitHub]: https://github.com/</span></span>
