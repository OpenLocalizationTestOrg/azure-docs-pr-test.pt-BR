---
title: "implantação de aaaContinuous para funções do Azure | Microsoft Docs"
description: "Use recursos de implantação contínua do serviço de aplicativo do Azure toopublish funções do Azure."
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
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a><span data-ttu-id="c4cdb-103">Implantação contínua para Azure Functions</span><span class="sxs-lookup"><span data-stu-id="c4cdb-103">Continuous deployment for Azure Functions</span></span>
<span data-ttu-id="c4cdb-104">As funções do Azure torna fácil toodeploy seu aplicativo de função usando a integração contínua do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-104">Azure Functions makes it easy toodeploy your function app using App Service continuous integration.</span></span> <span data-ttu-id="c4cdb-105">Funções integram BitBucket, Dropbox, GitHub e Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="c4cdb-105">Functions integrates with BitBucket, Dropbox, GitHub, and Visual Studio Team Services (VSTS).</span></span> <span data-ttu-id="c4cdb-106">Isso permite que um fluxo de trabalho em que o código de função atualizações feito usando um tooAzure de implantação de disparador esses serviços integrados.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-106">This enables a workflow where function code updates made by using one of these integrated services trigger deployment tooAzure.</span></span> <span data-ttu-id="c4cdb-107">Se você estiver novas funções tooAzure, começar com [visão geral de funções do Azure](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4cdb-107">If you are new tooAzure Functions, start with [Azure Functions Overview](functions-overview.md).</span></span>

<span data-ttu-id="c4cdb-108">A implantação contínua é uma ótima opção para projetos nos quais várias contribuições frequentes são integradas.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-108">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span> <span data-ttu-id="c4cdb-109">Ele também permite manter o controle do código-fonte no código de funções.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-109">It also lets you maintain source control on your functions code.</span></span> <span data-ttu-id="c4cdb-110">Olá origens de implantação a seguir é atualmente suportado:</span><span class="sxs-lookup"><span data-stu-id="c4cdb-110">hello following deployment sources are currently supported:</span></span>

* [<span data-ttu-id="c4cdb-111">Bitbucket</span><span class="sxs-lookup"><span data-stu-id="c4cdb-111">Bitbucket</span></span>](https://bitbucket.org/)
* [<span data-ttu-id="c4cdb-112">Dropbox</span><span class="sxs-lookup"><span data-stu-id="c4cdb-112">Dropbox</span></span>](https://www.dropbox.com/)
* <span data-ttu-id="c4cdb-113">Repositório externo (Git ou Mercurial)</span><span class="sxs-lookup"><span data-stu-id="c4cdb-113">External repository (Git or Mercurial)</span></span>
* [<span data-ttu-id="c4cdb-114">Repositório local Git</span><span class="sxs-lookup"><span data-stu-id="c4cdb-114">Git local repository</span></span>](../app-service-web/app-service-deploy-local-git.md)
* [<span data-ttu-id="c4cdb-115">GitHub</span><span class="sxs-lookup"><span data-stu-id="c4cdb-115">GitHub</span></span>](https://github.com)
* [<span data-ttu-id="c4cdb-116">OneDrive</span><span class="sxs-lookup"><span data-stu-id="c4cdb-116">OneDrive</span></span>](https://onedrive.live.com/)
* [<span data-ttu-id="c4cdb-117">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="c4cdb-117">Visual Studio Team Services</span></span>](https://www.visualstudio.com/team-services/)

<span data-ttu-id="c4cdb-118">As implantações são configuradas para cada aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-118">Deployments are configured on a per-function app basis.</span></span> <span data-ttu-id="c4cdb-119">Após a implantação contínua está habilitada, o código de toofunction de acesso no portal de saudação está definido muito*somente leitura*.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-119">After continuous deployment is enabled, access toofunction code in hello portal is set too*read-only*.</span></span>

## <a name="continuous-deployment-requirements"></a><span data-ttu-id="c4cdb-120">Requisitos de implantação contínua</span><span class="sxs-lookup"><span data-stu-id="c4cdb-120">Continuous deployment requirements</span></span>

<span data-ttu-id="c4cdb-121">Você deve ter sua origem de implantação configurada e seu código de funções na origem de implantação de saudação antes de configurar a implantação contínua.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-121">You must have your deployment source configured and your functions code in hello deployment source before you set up continuous deployment.</span></span> <span data-ttu-id="c4cdb-122">Em uma implantação de aplicativo de determinada função, cada função reside em um subdiretório nomeado, onde o nome do diretório Olá é o nome de saudação do função hello.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-122">In a given function app deployment, each function lives in a named subdirectory, where hello directory name is hello name of hello function.</span></span>  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a><span data-ttu-id="c4cdb-123">Configurar a implantação contínua</span><span class="sxs-lookup"><span data-stu-id="c4cdb-123">Set up continuous deployment</span></span>
<span data-ttu-id="c4cdb-124">Use esta implantação contínua do procedimento tooconfigure para um aplicativo de função existente.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-124">Use this procedure tooconfigure continuous deployment for an existing function app.</span></span> <span data-ttu-id="c4cdb-125">Essas etapas demonstram a integração com um repositório GitHub, porém etapas semelhantes se aplicam para serviços do Visual Studio Team Services ou outros serviços de implantação.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-125">These steps demonstrate integration with a GitHub repository, but similar steps apply for Visual Studio Team Services or other deployment services.</span></span>

1. <span data-ttu-id="c4cdb-126">Em seu aplicativo de função no hello [portal do Azure](https://portal.azure.com), clique em **recursos de plataforma** e **opções de implantação**.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-126">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Configurar a implantação contínua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="c4cdb-128">Em seguida, em Olá **implantações** folha clique **instalação**.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-128">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![Configurar a implantação contínua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="c4cdb-130">Em Olá **origem de implantação** folha, clique em **Escolher fonte**, preencha as informações de saudação para sua fonte de implantação escolhida e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-130">In hello **Deployment source** blade, click **Choose source**, then fill in hello information for your chosen deployment source and click **OK**.</span></span>
   
    ![Escolher a fonte de implantação](./media/functions-continuous-deployment/choose-deployment-source.png)

<span data-ttu-id="c4cdb-132">Após a configuração de implantação contínua, todas as alterações de arquivo na fonte de implantação são copiados toohello função aplicativo e uma implantação completa do site é acionada.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-132">After continuous deployment is configured, all file changes in your deployment source are copied toohello function app and a full site deployment is triggered.</span></span> <span data-ttu-id="c4cdb-133">site de saudação for reimplantado quando os arquivos na fonte de saudação são atualizados.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-133">hello site is redeployed when files in hello source are updated.</span></span>

## <a name="deployment-options"></a><span data-ttu-id="c4cdb-134">Opções de implantação</span><span class="sxs-lookup"><span data-stu-id="c4cdb-134">Deployment options</span></span>

<span data-ttu-id="c4cdb-135">Olá seguem alguns cenários comuns de implantação:</span><span class="sxs-lookup"><span data-stu-id="c4cdb-135">hello following are some typical deployment scenarios:</span></span>

- [<span data-ttu-id="c4cdb-136">Criar uma implantação de preparo</span><span class="sxs-lookup"><span data-stu-id="c4cdb-136">Create a staging deployment</span></span>](#staging)
- [<span data-ttu-id="c4cdb-137">Mover a implantação de toocontinuous funções existentes</span><span class="sxs-lookup"><span data-stu-id="c4cdb-137">Move existing functions toocontinuous deployment</span></span>](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a><span data-ttu-id="c4cdb-138">Criar uma implantação de preparo</span><span class="sxs-lookup"><span data-stu-id="c4cdb-138">Create a staging deployment</span></span>

<span data-ttu-id="c4cdb-139">Aplicativos de Função ainda não dão suporte a slots de implantação.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-139">Function Apps doesn't yet support deployment slots.</span></span> <span data-ttu-id="c4cdb-140">No entanto, você ainda pode gerenciar implantações de produção e preparo separadas usando a integração contínua.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-140">However, you can still manage separate staging and production deployments by using continuous integration.</span></span>

<span data-ttu-id="c4cdb-141">Olá tooconfigure de processo e trabalhar com uma implantação de preparo geralmente tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="c4cdb-141">hello process tooconfigure and work with a staging deployment looks generally like this:</span></span>

1. <span data-ttu-id="c4cdb-142">Crie dois aplicativos de função em sua assinatura, uma para o código de produção de hello e outra para preparação.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-142">Create two function apps in your subscription, one for hello production code and one for staging.</span></span> 

2. <span data-ttu-id="c4cdb-143">Crie uma fonte de implantação, se você ainda não tiver uma.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-143">Create a deployment source, if you don't already have one.</span></span> <span data-ttu-id="c4cdb-144">Este exemplo usa [GitHub].</span><span class="sxs-lookup"><span data-stu-id="c4cdb-144">This example uses [GitHub].</span></span>

3. <span data-ttu-id="c4cdb-145">Para seu aplicativo de função de produção, Olá completo anterior etapas **configurar implantação contínua** e conjunto Olá implantação ramificação toohello mestre ramificação do repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-145">For your production function app, complete hello preceding steps in **Set up continuous deployment** and set hello deployment branch toohello master branch of your GitHub repository.</span></span>
   
    ![Escolher a ramificação de implantação](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. <span data-ttu-id="c4cdb-147">Repita essa etapa para Olá função de aplicativo de teste, mas escolha Olá Preparando ramificação em vez disso, no seu repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-147">Repeat this step for hello staging function app, but choose hello staging branch instead in your GitHub repo.</span></span> <span data-ttu-id="c4cdb-148">Se sua fonte de implantação não der suporte à ramificação, use uma pasta diferente.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-148">If your deployment source doesn't support branching, use a different folder.</span></span>
    
5. <span data-ttu-id="c4cdb-149">Faça atualizações tooyour código em Olá branch ou pasta de preparo e verificar se essas alterações são refletidas na implantação de preparo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-149">Make updates tooyour code in hello staging branch or folder, then verify that those changes are reflected in hello staging deployment.</span></span>

6. <span data-ttu-id="c4cdb-150">Depois de testes, mesclar alterações do branch de preparo Olá no branch mestre hello.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-150">After testing, merge changes from hello staging branch into hello master branch.</span></span> <span data-ttu-id="c4cdb-151">Essa mesclagem gatilhos implantação toohello função aplicativo de produção.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-151">This merge triggers deployment toohello production function app.</span></span> <span data-ttu-id="c4cdb-152">Se sua fonte de implantação não oferece suporte a ramificações, substitua arquivos de saudação na pasta de produção de hello com arquivos Olá Olá pasta temporária.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-152">If your deployment source doesn't support branches, overwrite hello files in hello production folder with hello files from hello staging folder.</span></span>

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a><span data-ttu-id="c4cdb-153">Mover a implantação de toocontinuous funções existentes</span><span class="sxs-lookup"><span data-stu-id="c4cdb-153">Move existing functions toocontinuous deployment</span></span>
<span data-ttu-id="c4cdb-154">Quando você tem funções existentes que você tenha criado e mantido no portal de saudação, você precisa toodownload existente função arquivos de código usando FTP ou hello repositório Git local antes de configurar a implantação contínua conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-154">When you have existing functions that you have created and maintained in hello portal, you need toodownload your existing function code files using FTP or hello local Git repository before you can set up continuous deployment as described above.</span></span> <span data-ttu-id="c4cdb-155">Você pode fazer isso no hello configurações de serviço de aplicativo para seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-155">You can do this in hello App Service settings for your function app.</span></span> <span data-ttu-id="c4cdb-156">Depois que os arquivos são baixados, você poderá carregá-los origem de implantação contínua tooyour escolhido.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-156">After your files are downloaded, you can upload them tooyour chosen continuous deployment source.</span></span>

> [!NOTE]
> <span data-ttu-id="c4cdb-157">Depois de configurar a integração contínua, não será capaz de tooedit sua fonte de arquivos no portal de funções hello.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-157">After you configure continuous integration, you will no longer be able tooedit your source files in hello Functions portal.</span></span>

- [<span data-ttu-id="c4cdb-158">Como configurar credenciais de implantação</span><span class="sxs-lookup"><span data-stu-id="c4cdb-158">How to: Configure deployment credentials</span></span>](#credentials)
- [<span data-ttu-id="c4cdb-159">Como baixar arquivos usando FTP</span><span class="sxs-lookup"><span data-stu-id="c4cdb-159">How to: Download files using FTP</span></span>](#downftp)
- [<span data-ttu-id="c4cdb-160">Como: baixar os arquivos usando o repositório do Git local Olá</span><span class="sxs-lookup"><span data-stu-id="c4cdb-160">How to: Download files using hello local Git repository</span></span>](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a><span data-ttu-id="c4cdb-161">Como: configurar credenciais de implantação</span><span class="sxs-lookup"><span data-stu-id="c4cdb-161">How to: Configure deployment credentials</span></span>
<span data-ttu-id="c4cdb-162">Antes de baixar arquivos de seu aplicativo de função com FTP ou repositório Git local, você deve configurar seu site de saudação tooaccess credenciais.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-162">Before you can download files from your function app with FTP or local Git repository, you must configure your credentials tooaccess hello site.</span></span> <span data-ttu-id="c4cdb-163">As credenciais são definidas no nível de aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-163">Credentials are set at hello Function app level.</span></span> <span data-ttu-id="c4cdb-164">As etapas a seguir de saudação do uso tooset credenciais de implantação no portal do Azure de saudação:</span><span class="sxs-lookup"><span data-stu-id="c4cdb-164">Use hello following steps tooset deployment credentials in hello Azure portal:</span></span>

1. <span data-ttu-id="c4cdb-165">Em seu aplicativo de função no hello [portal do Azure](https://portal.azure.com), clique em **recursos de plataforma** e **credenciais de implantação**.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-165">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment credentials**.</span></span>
   
    ![Definir credenciais de implantação local](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. <span data-ttu-id="c4cdb-167">Digite um nome de usuário e senha e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-167">Type in a username and password, then click **Save**.</span></span> <span data-ttu-id="c4cdb-168">Agora você pode usar essas credenciais tooaccess seu aplicativo de função do FTP ou hello repositório Git interno.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-168">You can now use these credentials tooaccess your function app from FTP or hello built-in Git repo.</span></span>

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a><span data-ttu-id="c4cdb-169">Como: baixar arquivos usando FTP</span><span class="sxs-lookup"><span data-stu-id="c4cdb-169">How to: Download files using FTP</span></span>

1. <span data-ttu-id="c4cdb-170">Em seu aplicativo de função no hello [portal do Azure](https://portal.azure.com), clique em **recursos de plataforma** e **propriedades**, em seguida, copie os valores hello para **dousuáriodeFTP/implantação**, **Nome do Host do FTP**, e **nome de Host FTPS**.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-170">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Properties**, then copy hello values for **FTP/Deployment User**, **FTP Host Name**, and **FTPS Host Name**.</span></span>  

    <span data-ttu-id="c4cdb-171">**Usuário de FTP/implantação** deve ser inserido como exibido no portal de hello, incluindo o nome do aplicativo hello, tooprovide o contexto apropriado para o servidor de saudação FTP.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-171">**FTP/Deployment User** must be entered as displayed in hello portal, including hello app name, tooprovide proper context for hello FTP server.</span></span>
   
    ![Obter as informações de implantação](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. <span data-ttu-id="c4cdb-173">De seu cliente FTP, use informações de conexão Olá coletadas tooconnect tooyour aplicativo e baixar arquivos de origem Olá para suas funções.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-173">From your FTP client, use hello connection information you gathered tooconnect tooyour app and download hello source files for your functions.</span></span>

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a><span data-ttu-id="c4cdb-174">Como: baixar arquivos usando o repositório Git local</span><span class="sxs-lookup"><span data-stu-id="c4cdb-174">How to: Download files using a local Git repository</span></span>

1. <span data-ttu-id="c4cdb-175">Em seu aplicativo de função no hello [portal do Azure](https://portal.azure.com), clique em **recursos de plataforma** e **opções de implantação**.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-175">In your function app in hello [Azure portal](https://portal.azure.com), click **Platform features** and **Deployment options**.</span></span> 
   
    ![Configurar a implantação contínua](./media/functions-continuous-deployment/setup-deployment.png)
 
2. <span data-ttu-id="c4cdb-177">Em seguida, em Olá **implantações** folha clique **instalação**.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-177">Then in hello **Deployments** blade click **Setup**.</span></span>
 
    ![Configurar a implantação contínua](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. <span data-ttu-id="c4cdb-179">Em Olá **origem de implantação** folha, clique em **repositório Git Local** e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-179">In hello **Deployment source** blade, click **Local Git repository** and then click **OK**.</span></span>

3. <span data-ttu-id="c4cdb-180">Em **recursos de plataforma**, clique em **propriedades** e observe o valor de saudação da URL de Git.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-180">In **Platform features**, click **Properties** and note hello value of Git URL.</span></span> 
   
    ![Configurar a implantação contínua](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. <span data-ttu-id="c4cdb-182">Repositório de saudação do clone em seu computador local usando um prompt de comando com reconhecimento de Git ou sua ferramenta favorita do Git.</span><span class="sxs-lookup"><span data-stu-id="c4cdb-182">Clone hello repository on your local machine using a Git-aware command prompt or your favorite Git tool.</span></span> <span data-ttu-id="c4cdb-183">Olá comando de clone de Git tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="c4cdb-183">hello Git clone command looks like this:</span></span>
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. <span data-ttu-id="c4cdb-184">Obter arquivos do seu clone de toohello do aplicativo de função no computador local, como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="c4cdb-184">Fetch files from your function app toohello clone on your local computer, as in hello following example:</span></span>
   
        git pull origin master
   
    <span data-ttu-id="c4cdb-185">Se solicitado, forneça as [credenciais de implantação configuradas](#credentials).</span><span class="sxs-lookup"><span data-stu-id="c4cdb-185">If requested, supply your [configured deployment credentials](#credentials).</span></span>  

[GitHub]: https://github.com/
