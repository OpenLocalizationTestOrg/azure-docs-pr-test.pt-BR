---
title: "aaaLocal tooAzure de implantação do Git do serviço de aplicativo"
description: "Saiba como tooenable local Git implantação tooAzure do serviço de aplicativo."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: ac50a623-c4b8-4dfd-96b2-a09420770063
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 1905e0b7acd58d8dd6496a14f6e4f38f9f8c0212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="local-git-deployment-tooazure-app-service"></a><span data-ttu-id="e685c-103">TooAzure local de implantação do Git do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="e685c-103">Local Git Deployment tooAzure App Service</span></span>
<span data-ttu-id="e685c-104">Este tutorial mostra como toodeploy seu aplicativo muito[do serviço de aplicativo do Azure] de um repositório Git no computador local.</span><span class="sxs-lookup"><span data-stu-id="e685c-104">This tutorial shows you how toodeploy your app too[Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="e685c-105">Serviço de aplicativo oferece suporte a essa abordagem com hello **Git Local** opção de implantação no hello [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="e685c-105">App Service supports this approach with hello **Local Git** deployment option in hello [Azure Portal].</span></span>  
<span data-ttu-id="e685c-106">Muitos dos comandos do Git Olá descritos neste artigo são executados automaticamente durante a criação de um aplicativo de serviço de aplicativo usando Olá [Interface de linha de comando do Azure] conforme descrito [aqui](app-service-web-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e685c-106">Many of hello Git commands described in this article are performed automatically when creating an App Service app using hello [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e685c-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e685c-107">Prerequisites</span></span>
<span data-ttu-id="e685c-108">toocomplete neste tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="e685c-108">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="e685c-109">Git.</span><span class="sxs-lookup"><span data-stu-id="e685c-109">Git.</span></span> <span data-ttu-id="e685c-110">Você pode fazer o download de binários de instalação Olá [aqui](http://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="e685c-110">You can download hello installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="e685c-111">Conhecimento básico do Git.</span><span class="sxs-lookup"><span data-stu-id="e685c-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="e685c-112">Uma conta do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e685c-112">A Microsoft Azure account.</span></span> <span data-ttu-id="e685c-113">Se não tiver uma conta, você poderá [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial) ou [ativar seus benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span><span class="sxs-lookup"><span data-stu-id="e685c-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="e685c-114">Se você quiser tooget iniciado com o serviço de aplicativo do Azure antes de se inscrever para uma conta do Azure, vá muito[tente do serviço de aplicativo](https://azure.microsoft.com/try/app-service/), onde você pode criar imediatamente um aplicativo de início de curta duração no serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e685c-114">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="e685c-115">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="e685c-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="e685c-116"><a name="Step1"></a>Etapa 1: Criar um repositório local</span><span class="sxs-lookup"><span data-stu-id="e685c-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="e685c-117">Execute Olá tarefas toocreate um novo repositório Git a seguir.</span><span class="sxs-lookup"><span data-stu-id="e685c-117">Perform hello following tasks toocreate a new Git repository.</span></span>

1. <span data-ttu-id="e685c-118">Inicie uma ferramenta da linha de comando, como **GitBash** (Windows) ou **Bash** (Unix Shell).</span><span class="sxs-lookup"><span data-stu-id="e685c-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="e685c-119">Em sistemas de OS X, você pode acessar Olá de linha de comando por meio de saudação **Terminal** aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e685c-119">On OS X systems you can access hello command-line through hello **Terminal** application.</span></span>
2. <span data-ttu-id="e685c-120">Navegue toohello diretório onde Olá toodeploy de conteúdo seja localizado.</span><span class="sxs-lookup"><span data-stu-id="e685c-120">Navigate toohello directory where hello content toodeploy would be located.</span></span>
3. <span data-ttu-id="e685c-121">Use Olá comando tooinitialize um novo repositório Git a seguir:</span><span class="sxs-lookup"><span data-stu-id="e685c-121">Use hello following command tooinitialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="e685c-122"><a name="Step2"></a>Etapa 2: Confirmar seu conteúdo</span><span class="sxs-lookup"><span data-stu-id="e685c-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="e685c-123">O Serviço de Aplicativo dá suporte a aplicativos criados em uma variedade de linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="e685c-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="e685c-124">Se o repositório já inclui conteúdo ignorar esse ponto e move toopoint 2 abaixo.</span><span class="sxs-lookup"><span data-stu-id="e685c-124">If your repository already includes content skip this point and move toopoint 2 below.</span></span> <span data-ttu-id="e685c-125">Se seu repositório ainda não inclui conteúdo, simplesmente popule-o com um arquivo .html estático da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e685c-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="e685c-126">Usando um editor de texto, crie um novo arquivo denominado **index** na raiz de saudação do repositório do Git Olá</span><span class="sxs-lookup"><span data-stu-id="e685c-126">Using a text editor, create a new file named **index.html** at hello root of hello Git repository</span></span>
   * <span data-ttu-id="e685c-127">Adicionar Olá depois do texto como conteúdo Olá Olá index de arquivo e salve-o: *Git Olá!*</span><span class="sxs-lookup"><span data-stu-id="e685c-127">Add hello following text as hello contents for hello index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="e685c-128">De saudação de linha de comando, verifique se que você está na raiz de saudação do repositório Git.</span><span class="sxs-lookup"><span data-stu-id="e685c-128">From hello command-line, verify that you are under hello root of your Git repository.</span></span> <span data-ttu-id="e685c-129">Em seguida, use Olá repositório tooyour do comando tooadd arquivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e685c-129">Then use hello following command tooadd files tooyour repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="e685c-130">Em seguida, confirmação Olá alterações toohello repositório usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e685c-130">Next, commit hello changes toohello repository by using hello following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="e685c-131"><a name="Step3"></a>Etapa 3: Habilitar Olá repositório de aplicativo de serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="e685c-131"><a name="Step3"></a>Step 3: Enable hello App Service app repository</span></span>
<span data-ttu-id="e685c-132">Execute Olá seguindo as etapas tooenable um repositório Git para seu aplicativo de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e685c-132">Perform hello following steps tooenable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="e685c-133">Faça logon no toohello [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="e685c-133">Log in toohello [Azure Portal].</span></span>
2. <span data-ttu-id="e685c-134">Na folha do seu aplicativo do Serviço de Aplicativo, clique em **Configurações > Origem da implantação**.</span><span class="sxs-lookup"><span data-stu-id="e685c-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="e685c-135">Clique em **Escolher fonte**, em seguida, clique em **Repositório Git Local** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="e685c-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![Repositório Git local](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="e685c-137">Se esse for o primeiro tempo configurando um repositório no Azure, você precisa ter credenciais de logon toocreate para ele.</span><span class="sxs-lookup"><span data-stu-id="e685c-137">If this is your first time setting up a repository in Azure, you need toocreate login credentials for it.</span></span> <span data-ttu-id="e685c-138">Você usará-los toolog em Olá repositório do Azure e por push as alterações no seu repositório Git local.</span><span class="sxs-lookup"><span data-stu-id="e685c-138">You will use them toolog into hello Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="e685c-139">Na folha do aplicativo, clique em **Configurações > Credenciais da implantação**, em seguida, configure o nome de usuário da implantação e a senha.</span><span class="sxs-lookup"><span data-stu-id="e685c-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="e685c-140">Quando terminar, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="e685c-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="e685c-141"><a name="Step4"></a>Etapa 4: Implantar seu projeto</span><span class="sxs-lookup"><span data-stu-id="e685c-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="e685c-142">Use Olá seguindo as etapas toopublish tooApp seu aplicativo usando o Git Local do serviço.</span><span class="sxs-lookup"><span data-stu-id="e685c-142">Use hello following steps toopublish your app tooApp Service using Local Git.</span></span>

1. <span data-ttu-id="e685c-143">Na folha do seu aplicativo em Olá Portal do Azure, clique em **Configurações > propriedades** para Olá **URL do Git**.</span><span class="sxs-lookup"><span data-stu-id="e685c-143">In your app's blade in hello Azure Portal, click **Settings > Properties** for hello **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="e685c-144">**URL de Git** é Olá referência remota toodeploy toofrom seu repositório local.</span><span class="sxs-lookup"><span data-stu-id="e685c-144">**Git URL** is hello remote reference toodeploy toofrom your local repository.</span></span> <span data-ttu-id="e685c-145">Você usará esta URL no hello etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="e685c-145">You'll use this URL in hello following steps.</span></span>
2. <span data-ttu-id="e685c-146">Usando Olá de linha de comando, verifique se você está na raiz de saudação do seu repositório Git local.</span><span class="sxs-lookup"><span data-stu-id="e685c-146">Using hello command-line, verify that you are in hello root of your local Git repository.</span></span>
3. <span data-ttu-id="e685c-147">Use `git remote` referência remota de saudação tooadd listada na **URL de Git** da etapa 1.</span><span class="sxs-lookup"><span data-stu-id="e685c-147">Use `git remote` tooadd hello remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="e685c-148">O comando terá aparência a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="e685c-148">Your command will look similar toohello following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="e685c-149">Olá **remoto** comando adiciona um repositório remoto de tooa Referência nomeada.</span><span class="sxs-lookup"><span data-stu-id="e685c-149">hello **remote** command adds a named reference tooa remote repository.</span></span> <span data-ttu-id="e685c-150">Neste exemplo, ele cria uma referência chamada ‘azure’ para o repositório do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e685c-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="e685c-151">Enviar por push o serviço de tooApp conteúdo usando Olá novo **azure** remoto você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="e685c-151">Push your content tooApp Service using hello new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for hello password you created earlier when you reset your deployment credentials in hello Azure Portal. Enter hello password (note that Gitbash does not echo asterisks toohello console as you type your password). 
5. <span data-ttu-id="e685c-152">Volte tooyour aplicativo hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e685c-152">Go back tooyour app in hello Azure Portal.</span></span> <span data-ttu-id="e685c-153">Uma entrada de log de seu envio mais recente deve ser exibida em Olá **implantações** folha.</span><span class="sxs-lookup"><span data-stu-id="e685c-153">A log entry of your most recent push should be displayed in hello **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="e685c-154">Clique em Olá **procurar** botão na parte superior de saudação do conteúdo de saudação de tooverify de folha à saudação do aplicativo foi implantado.</span><span class="sxs-lookup"><span data-stu-id="e685c-154">Click hello **Browse** button at hello top of hello app's blade tooverify hello content has been deployed.</span></span> 

## <span data-ttu-id="e685c-155"><a name="Step5"></a>Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="e685c-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="e685c-156">Olá seguem erros ou problemas comumente encontrados ao usar o Git toopublish tooan aplicativo de serviço de aplicativo no Azure:</span><span class="sxs-lookup"><span data-stu-id="e685c-156">hello following are errors or problems commonly encountered when using Git toopublish tooan App Service app in Azure:</span></span>

- - -
<span data-ttu-id="e685c-157">**Sintoma**: não é possível tooaccess '[siteURL]': falha tooconnect muito [scmAddress]</span><span class="sxs-lookup"><span data-stu-id="e685c-157">**Symptom**: Unable tooaccess '[siteURL]': Failed tooconnect too[scmAddress]</span></span>

<span data-ttu-id="e685c-158">**Causa**: este erro pode ocorrer se o aplicativo hello não está em execução.</span><span class="sxs-lookup"><span data-stu-id="e685c-158">**Cause**: This error can occur if hello app is not up and running.</span></span>

<span data-ttu-id="e685c-159">**Resolução**: Iniciar aplicativo Olá Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e685c-159">**Resolution**: Start hello app in hello Azure Portal.</span></span> <span data-ttu-id="e685c-160">Implantação do Git não funcionará a menos que o aplicativo hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="e685c-160">Git deployment will not work unless hello app is running.</span></span> 

- - -
<span data-ttu-id="e685c-161">**Sintoma**: não foi possível resolver o nome de host 'host'</span><span class="sxs-lookup"><span data-stu-id="e685c-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="e685c-162">**Causa**: este erro pode ocorrer se as informações de endereço de saudação inserido durante a criação de saudação 'azure' remoto estava incorreta.</span><span class="sxs-lookup"><span data-stu-id="e685c-162">**Cause**: This error can occur if hello address information entered when creating hello 'azure' remote was incorrect.</span></span>

<span data-ttu-id="e685c-163">**Resolução**: Olá Use `git remote -v` comando toolist todos os remotos, juntamente com a URL de saudação associada.</span><span class="sxs-lookup"><span data-stu-id="e685c-163">**Resolution**: Use hello `git remote -v` command toolist all remotes, along with hello associated URL.</span></span> <span data-ttu-id="e685c-164">Verifique se a URL Olá Olá 'azure' remoto está correto.</span><span class="sxs-lookup"><span data-stu-id="e685c-164">Verify that hello URL for hello 'azure' remote is correct.</span></span> <span data-ttu-id="e685c-165">Se necessário, remova e recrie nesse remoto usando a URL correta do hello.</span><span class="sxs-lookup"><span data-stu-id="e685c-165">If needed, remove and recreate this remote using hello correct URL.</span></span>

- - -
<span data-ttu-id="e685c-166">**Sintoma**: não há referências em comum e nenhuma especificada; nada é feito.</span><span class="sxs-lookup"><span data-stu-id="e685c-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="e685c-167">Talvez você deva especificar uma ramificação como 'mestre'.</span><span class="sxs-lookup"><span data-stu-id="e685c-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="e685c-168">**Causa**: este erro pode ocorrer se você não especificar uma ramificação ao executar uma operação de envio por push do git e ter não Olá push.default valor fixo usado pelo Git.</span><span class="sxs-lookup"><span data-stu-id="e685c-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set hello push.default value used by Git.</span></span>

<span data-ttu-id="e685c-169">**Resolução**: executar a operação de envio de saudação novamente, especificando a ramificação mestre hello.</span><span class="sxs-lookup"><span data-stu-id="e685c-169">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="e685c-170">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e685c-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="e685c-171">**Sintoma**: src refspec [branchname] não corresponde a nada.</span><span class="sxs-lookup"><span data-stu-id="e685c-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="e685c-172">**Causa**: este erro pode ocorrer se você tentar toopush tooa filial que não seja o mestre de saudação 'azure' remoto.</span><span class="sxs-lookup"><span data-stu-id="e685c-172">**Cause**: This error can occur if you attempt toopush tooa branch other than master on hello 'azure' remote.</span></span>

<span data-ttu-id="e685c-173">**Resolução**: executar a operação de envio de saudação novamente, especificando a ramificação mestre hello.</span><span class="sxs-lookup"><span data-stu-id="e685c-173">**Resolution**: Perform hello push operation again, specifying hello master branch.</span></span> <span data-ttu-id="e685c-174">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e685c-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="e685c-175">**Sintoma**: falha de RPC; resultado = 22, código HTTP = 502.</span><span class="sxs-lookup"><span data-stu-id="e685c-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="e685c-176">**Causa**: este erro pode ocorrer se você tentar toopush um repositório git grande via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e685c-176">**Cause**: This error can occur if you attempt toopush a large git repository over HTTPS.</span></span>

<span data-ttu-id="e685c-177">**Resolução**: alteração da configuração do git Olá em postBuffer toomake de saudação do computador local Olá maior</span><span class="sxs-lookup"><span data-stu-id="e685c-177">**Resolution**: Change hello git configuration on hello local machine toomake hello postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="e685c-178">**Sintoma**: erro - o repositório de tooremote confirmada alterações mas seu aplicativo web não está atualizado.</span><span class="sxs-lookup"><span data-stu-id="e685c-178">**Symptom**: Error - Changes committed tooremote repository but your web app not updated.</span></span>

<span data-ttu-id="e685c-179">**Causa**: esse erro poderá ocorrer se você estiver implantando um aplicativo do Node.js que contém um arquivo package.json que especifica os módulos adicionais necessários.</span><span class="sxs-lookup"><span data-stu-id="e685c-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="e685c-180">**Resolução**: as mensagens adicionais contendo 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="e685c-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="e685c-181">deve ser conectado toothis anterior erro e pode fornecer um contexto adicional em caso de falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="e685c-181">should be logged prior toothis error, and can provide additional context on hello failure.</span></span> <span data-ttu-id="e685c-182">a seguir Olá é conhecida causas desse erro e Olá correspondente 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="e685c-182">hello following are known causes of this error and hello corresponding 'npm ERR!'</span></span> <span data-ttu-id="e685c-183">mensagem:</span><span class="sxs-lookup"><span data-stu-id="e685c-183">message:</span></span>

* <span data-ttu-id="e685c-184">**Arquivo malformado package.json**: npm ERR!</span><span class="sxs-lookup"><span data-stu-id="e685c-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="e685c-185">Não foi possível ler as dependências.</span><span class="sxs-lookup"><span data-stu-id="e685c-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="e685c-186">**Um módulo nativo que não tenha uma distribuição binária para o Windows**:</span><span class="sxs-lookup"><span data-stu-id="e685c-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="e685c-187">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="e685c-187">npm ERR!</span></span> <span data-ttu-id="e685c-188">\`cmd "/c" "node-gyp rebuild"\` falhou com 1</span><span class="sxs-lookup"><span data-stu-id="e685c-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="e685c-189">OU</span><span class="sxs-lookup"><span data-stu-id="e685c-189">OR</span></span>
  * <span data-ttu-id="e685c-190">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="e685c-190">npm ERR!</span></span> <span data-ttu-id="e685c-191">[modulename@version] preinstall: \`make || gmake\`</span><span class="sxs-lookup"><span data-stu-id="e685c-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e685c-192">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e685c-192">Additional Resources</span></span>
* [<span data-ttu-id="e685c-193">Documentação do Git</span><span class="sxs-lookup"><span data-stu-id="e685c-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="e685c-194">Documentação do projeto Kudu</span><span class="sxs-lookup"><span data-stu-id="e685c-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="e685c-195">TooAzure implantação contínua do serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="e685c-195">Continous Deployment tooAzure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="e685c-196">Como toouse PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="e685c-196">How toouse PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="e685c-197">Como toouse Olá Interface de linha de comando do Azure</span><span class="sxs-lookup"><span data-stu-id="e685c-197">How toouse hello Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

[do serviço de aplicativo do Azure]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
[Portal do Azure]: https://portal.azure.com
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Interface de linha de comando do Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
