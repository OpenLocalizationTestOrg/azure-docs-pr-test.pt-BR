---
title: "Implantação do Git local para o Serviço de Aplicativo do Azure"
description: "Saiba como habilitar a implantação do Git local no Serviço de Aplicativo do Azure."
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
ms.openlocfilehash: f1c4911670d3aa32e74b3dfebd83cf3dc3830805
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="local-git-deployment-to-azure-app-service"></a><span data-ttu-id="ab322-103">Implantação do Git local para o Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="ab322-103">Local Git Deployment to Azure App Service</span></span>
<span data-ttu-id="ab322-104">Este tutorial mostra como implantar seu aplicativo para o [Serviço de Aplicativo do Azure] de um repositório do Git no computador local.</span><span class="sxs-lookup"><span data-stu-id="ab322-104">This tutorial shows you how to deploy your app to [Azure App Service] from a Git repository on your local computer.</span></span> <span data-ttu-id="ab322-105">O Serviço de Aplicativo dá suporte a essa abordagem com a opção de implantação do **Git Local** no [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="ab322-105">App Service supports this approach with the **Local Git** deployment option in the [Azure Portal].</span></span>  
<span data-ttu-id="ab322-106">Muitos dos comandos Git descritos neste artigo são executados automaticamente ao criar um aplicativo do Serviço de Aplicativo usando a [Interface da Linha de Comandos do Azure] como descrito [aqui](app-service-web-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ab322-106">Many of the Git commands described in this article are performed automatically when creating an App Service app using the [Azure Command-Line Interface] as described [here](app-service-web-get-started.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ab322-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ab322-107">Prerequisites</span></span>
<span data-ttu-id="ab322-108">Para concluir este tutorial, você precisará:</span><span class="sxs-lookup"><span data-stu-id="ab322-108">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="ab322-109">Git.</span><span class="sxs-lookup"><span data-stu-id="ab322-109">Git.</span></span> <span data-ttu-id="ab322-110">Você pode baixar o binário de instalação [aqui](http://www.git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="ab322-110">You can download the installation binary [here](http://www.git-scm.com/downloads).</span></span>  
* <span data-ttu-id="ab322-111">Conhecimento básico do Git.</span><span class="sxs-lookup"><span data-stu-id="ab322-111">Basic knowledge of Git.</span></span>
* <span data-ttu-id="ab322-112">Uma conta do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ab322-112">A Microsoft Azure account.</span></span> <span data-ttu-id="ab322-113">Se não tiver uma conta, você poderá [inscrever-se para uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial) ou [ativar seus benefícios de assinante do Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span><span class="sxs-lookup"><span data-stu-id="ab322-113">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details).</span></span>

> [!NOTE]
> <span data-ttu-id="ab322-114">Se você deseja começar com o Serviço de Aplicativo do Azure antes de se inscrever em uma conta do Azure, acesse [Experimentar o Serviço de Aplicativo](https://azure.microsoft.com/try/app-service/), em que você pode criar imediatamente um aplicativo inicial de curta duração no Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ab322-114">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter app in App Service.</span></span> <span data-ttu-id="ab322-115">Nenhum cartão de crédito é exigido, sem compromissos.</span><span class="sxs-lookup"><span data-stu-id="ab322-115">No credit cards required; no commitments.</span></span>  
> 
> 

## <span data-ttu-id="ab322-116"><a name="Step1"></a>Etapa 1: Criar um repositório local</span><span class="sxs-lookup"><span data-stu-id="ab322-116"><a name="Step1"></a>Step 1: Create a local repository</span></span>
<span data-ttu-id="ab322-117">Execute as seguintes tarefas para criar um novo repositório do Git.</span><span class="sxs-lookup"><span data-stu-id="ab322-117">Perform the following tasks to create a new Git repository.</span></span>

1. <span data-ttu-id="ab322-118">Inicie uma ferramenta da linha de comando, como **GitBash** (Windows) ou **Bash** (Unix Shell).</span><span class="sxs-lookup"><span data-stu-id="ab322-118">Start a command-line tool, such as **GitBash** (Windows) or **Bash** (Unix Shell).</span></span> <span data-ttu-id="ab322-119">Nos sistemas OS X, você pode acessar a linha de comando por meio do aplicativo **Terminal** .</span><span class="sxs-lookup"><span data-stu-id="ab322-119">On OS X systems you can access the command-line through the **Terminal** application.</span></span>
2. <span data-ttu-id="ab322-120">Navegue até o diretório em que o conteúdo para implantar estaria localizado.</span><span class="sxs-lookup"><span data-stu-id="ab322-120">Navigate to the directory where the content to deploy would be located.</span></span>
3. <span data-ttu-id="ab322-121">Use o seguinte comando para inicializar um novo repositório do Git:</span><span class="sxs-lookup"><span data-stu-id="ab322-121">Use the following command to initialize a new Git repository:</span></span>

```bash  
git init
```

## <span data-ttu-id="ab322-122"><a name="Step2"></a>Etapa 2: Confirmar seu conteúdo</span><span class="sxs-lookup"><span data-stu-id="ab322-122"><a name="Step2"></a>Step 2: Commit your content</span></span>
<span data-ttu-id="ab322-123">O Serviço de Aplicativo dá suporte a aplicativos criados em uma variedade de linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="ab322-123">App Service supports applications created in a variety of programming languages.</span></span> 

1. <span data-ttu-id="ab322-124">Se seu repositório já inclui conteúdo, ignore esse ponto e passe para o ponto 2 abaixo.</span><span class="sxs-lookup"><span data-stu-id="ab322-124">If your repository already includes content skip this point and move to point 2 below.</span></span> <span data-ttu-id="ab322-125">Se seu repositório ainda não inclui conteúdo, simplesmente popule-o com um arquivo .html estático da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ab322-125">If your repository does not already include content simply populate with a static .html file as follows:</span></span> 
   
   * <span data-ttu-id="ab322-126">Usando um editor de texto, crie um novo arquivo chamado **index.html** na raiz do repositório do Git</span><span class="sxs-lookup"><span data-stu-id="ab322-126">Using a text editor, create a new file named **index.html** at the root of the Git repository</span></span>
   * <span data-ttu-id="ab322-127">Adicione o seguinte como o conteúdo do arquivo index.html e salve-o: *Hello Git!*</span><span class="sxs-lookup"><span data-stu-id="ab322-127">Add the following text as the contents for the index.html file and save it: *Hello Git!*</span></span>
2. <span data-ttu-id="ab322-128">Na linha de comando, verifique se você está na raiz do seu repositório do Git.</span><span class="sxs-lookup"><span data-stu-id="ab322-128">From the command-line, verify that you are under the root of your Git repository.</span></span> <span data-ttu-id="ab322-129">Em seguida, use os comandos a seguir para adicionar arquivos ao repositório:</span><span class="sxs-lookup"><span data-stu-id="ab322-129">Then use the following command to add files to your repository:</span></span>

```bash  
git add -A
```
3. <span data-ttu-id="ab322-130">Em seguida, confirme as alterações no repositório usando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab322-130">Next, commit the changes to the repository by using the following command:</span></span>

```bash  
git commit -m "Hello Azure App Service"
```  

## <span data-ttu-id="ab322-131"><a name="Step3"></a>Etapa 3: Habilitar o repositório de aplicativos do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="ab322-131"><a name="Step3"></a>Step 3: Enable the App Service app repository</span></span>
<span data-ttu-id="ab322-132">Execute as seguintes etapas para habilitar um repositório do Git para seu aplicativo do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ab322-132">Perform the following steps to enable a Git repository for your App Service app.</span></span>

1. <span data-ttu-id="ab322-133">Faça logon no [Portal do Azure].</span><span class="sxs-lookup"><span data-stu-id="ab322-133">Log in to the [Azure Portal].</span></span>
2. <span data-ttu-id="ab322-134">Na folha do seu aplicativo do Serviço de Aplicativo, clique em **Configurações > Origem da implantação**.</span><span class="sxs-lookup"><span data-stu-id="ab322-134">In your App Service app's blade, click **Settings > Deployment source**.</span></span> <span data-ttu-id="ab322-135">Clique em **Escolher fonte**, em seguida, clique em **Repositório Git Local** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab322-135">Click **Choose source**, then click **Local Git Repository**, and then click **OK**.</span></span>  
   
    ![Repositório Git local](./media/app-service-deploy-local-git/local_git_selection.png)
3. <span data-ttu-id="ab322-137">Se for a primeira vez que você configura um repositório no Azure, você precisa criar as credenciais de logon para ele.</span><span class="sxs-lookup"><span data-stu-id="ab322-137">If this is your first time setting up a repository in Azure, you need to create login credentials for it.</span></span> <span data-ttu-id="ab322-138">Você as usará para fazer logon no repositório do Azure e enviar por push as alterações do seu repositório Git Local.</span><span class="sxs-lookup"><span data-stu-id="ab322-138">You will use them to log into the Azure repository and push changes from your local Git repository.</span></span> <span data-ttu-id="ab322-139">Na folha do aplicativo, clique em **Configurações > Credenciais da implantação**, em seguida, configure o nome de usuário da implantação e a senha.</span><span class="sxs-lookup"><span data-stu-id="ab322-139">From your app's blade, click **Settings > Deployment credentials**, then configure your deployment username and password.</span></span> <span data-ttu-id="ab322-140">Quando terminar, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ab322-140">When you're done, click **Save**.</span></span>
   
    ![](./media/app-service-deploy-local-git/deployment_credentials.png)

## <span data-ttu-id="ab322-141"><a name="Step4"></a>Etapa 4: Implantar seu projeto</span><span class="sxs-lookup"><span data-stu-id="ab322-141"><a name="Step4"></a>Step 4: Deploy your project</span></span>
<span data-ttu-id="ab322-142">Use as etapas a seguir para publicar seu aplicativo no Serviço de Aplicativo usando o Git Local.</span><span class="sxs-lookup"><span data-stu-id="ab322-142">Use the following steps to publish your app to App Service using Local Git.</span></span>

1. <span data-ttu-id="ab322-143">Na folha do aplicativo no Portal do Azure, clique em **Configurações > Propriedades** para a **URL do Git**.</span><span class="sxs-lookup"><span data-stu-id="ab322-143">In your app's blade in the Azure Portal, click **Settings > Properties** for the **Git URL**.</span></span>
   
    ![](./media/app-service-deploy-local-git/git_url.png)
   
    <span data-ttu-id="ab322-144">**URL do Git** é a referência remota para implantação a partir de seu repositório local.</span><span class="sxs-lookup"><span data-stu-id="ab322-144">**Git URL** is the remote reference to deploy to from your local repository.</span></span> <span data-ttu-id="ab322-145">Você usará essa URL nas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="ab322-145">You'll use this URL in the following steps.</span></span>
2. <span data-ttu-id="ab322-146">Usando a linha de comando, verifique se você está na raiz do seu repositório do Git local.</span><span class="sxs-lookup"><span data-stu-id="ab322-146">Using the command-line, verify that you are in the root of your local Git repository.</span></span>
3. <span data-ttu-id="ab322-147">Use `git remote` para adicionar a referência remota listada na **URL do Git** na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="ab322-147">Use `git remote` to add the remote reference listed in **Git URL** from step 1.</span></span> <span data-ttu-id="ab322-148">O comando será semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="ab322-148">Your command will look similar to the following:</span></span>
   
        git remote add azure https://<username>@localgitdeployment.scm.azurewebsites.net:443/localgitdeployment.git         
   > [!NOTE]
   > <span data-ttu-id="ab322-149">O comando **remoto** adiciona uma referência com nome a um repositório remoto.</span><span class="sxs-lookup"><span data-stu-id="ab322-149">The **remote** command adds a named reference to a remote repository.</span></span> <span data-ttu-id="ab322-150">Neste exemplo, ele cria uma referência chamada ‘azure’ para o repositório do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="ab322-150">In this example, it creates a reference named 'azure' for your web app's repository.</span></span>
   > 
   > 
4. <span data-ttu-id="ab322-151">Envie por push seu conteúdo para o Serviço de Aplicativo usando o novo remoto **azure** que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="ab322-151">Push your content to App Service using the new **azure** remote you just created.</span></span>

```bash  
git push azure master
```
    You will be prompted for the password you created earlier when you reset your deployment credentials in the Azure Portal. Enter the password (note that Gitbash does not echo asterisks to the console as you type your password). 
5. <span data-ttu-id="ab322-152">Volte para seu aplicativo no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab322-152">Go back to your app in the Azure Portal.</span></span> <span data-ttu-id="ab322-153">Uma entrada de log do seu envio por push mais recente deve ser exibida na folha **Implantações** .</span><span class="sxs-lookup"><span data-stu-id="ab322-153">A log entry of your most recent push should be displayed in the **Deployments** blade.</span></span> 
   
    ![](./media/app-service-deploy-local-git/deployment_history.png)
6. <span data-ttu-id="ab322-154">Clique no botão **Procurar** na parte superior da folha do aplicativo para verificar se o conteúdo foi implantado.</span><span class="sxs-lookup"><span data-stu-id="ab322-154">Click the **Browse** button at the top of the app's blade to verify the content has been deployed.</span></span> 

## <span data-ttu-id="ab322-155"><a name="Step5"></a>Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="ab322-155"><a name="Step5"></a>Troubleshooting</span></span>
<span data-ttu-id="ab322-156">Estes são erros ou problemas comumente encontrados ao usar o Git para publicar em um aplicativo do Serviço de Aplicativo no Azure:</span><span class="sxs-lookup"><span data-stu-id="ab322-156">The following are errors or problems commonly encountered when using Git to publish to an App Service app in Azure:</span></span>

- - -
<span data-ttu-id="ab322-157">**Sintoma**: não foi possível acessar ‘[siteURL]': falha ao conectar ao [scmAddress]</span><span class="sxs-lookup"><span data-stu-id="ab322-157">**Symptom**: Unable to access '[siteURL]': Failed to connect to [scmAddress]</span></span>

<span data-ttu-id="ab322-158">**Causa**: esse erro poderá ocorrer se o aplicativo não estiver em funcionamento.</span><span class="sxs-lookup"><span data-stu-id="ab322-158">**Cause**: This error can occur if the app is not up and running.</span></span>

<span data-ttu-id="ab322-159">**Resolução**: inicie o aplicativo no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab322-159">**Resolution**: Start the app in the Azure Portal.</span></span> <span data-ttu-id="ab322-160">A implantação do Git não funcionará a menos que o aplicativo esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="ab322-160">Git deployment will not work unless the app is running.</span></span> 

- - -
<span data-ttu-id="ab322-161">**Sintoma**: não foi possível resolver o nome de host 'host'</span><span class="sxs-lookup"><span data-stu-id="ab322-161">**Symptom**: Couldn't resolve host 'hostname'</span></span>

<span data-ttu-id="ab322-162">**Causa**: este erro pode ocorrer se as informações de endereço inseridas ao criar o azure remoto estiverem incorretas.</span><span class="sxs-lookup"><span data-stu-id="ab322-162">**Cause**: This error can occur if the address information entered when creating the 'azure' remote was incorrect.</span></span>

<span data-ttu-id="ab322-163">**Resolução**: Use o comando `git remote -v` para listar todos os remotos, juntamente com a URL associada.</span><span class="sxs-lookup"><span data-stu-id="ab322-163">**Resolution**: Use the `git remote -v` command to list all remotes, along with the associated URL.</span></span> <span data-ttu-id="ab322-164">Verifique se a URL do remote do 'azure' está correta.</span><span class="sxs-lookup"><span data-stu-id="ab322-164">Verify that the URL for the 'azure' remote is correct.</span></span> <span data-ttu-id="ab322-165">Se necessário, remova e recrie esse remoto usando a URL correta.</span><span class="sxs-lookup"><span data-stu-id="ab322-165">If needed, remove and recreate this remote using the correct URL.</span></span>

- - -
<span data-ttu-id="ab322-166">**Sintoma**: não há referências em comum e nenhuma especificada; nada é feito.</span><span class="sxs-lookup"><span data-stu-id="ab322-166">**Symptom**: No refs in common and none specified; doing nothing.</span></span> <span data-ttu-id="ab322-167">Talvez você deva especificar uma ramificação como 'mestre'.</span><span class="sxs-lookup"><span data-stu-id="ab322-167">Perhaps you should specify a branch such as 'master'.</span></span>

<span data-ttu-id="ab322-168">**Causa**: este erro pode ocorrer se você não especificar uma ramificação ao executar uma operação de envio de git e não tiver definido o valor de push.default usado pelo Git.</span><span class="sxs-lookup"><span data-stu-id="ab322-168">**Cause**: This error can occur if you do not specify a branch when performing a git push operation, and have not set the push.default value used by Git.</span></span>

<span data-ttu-id="ab322-169">**Solução**: execute a operação de envio novamente, especificando a ramificação mestre.</span><span class="sxs-lookup"><span data-stu-id="ab322-169">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="ab322-170">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ab322-170">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="ab322-171">**Sintoma**: src refspec [branchname] não corresponde a nada.</span><span class="sxs-lookup"><span data-stu-id="ab322-171">**Symptom**: src refspec [branchname] does not match any.</span></span>

<span data-ttu-id="ab322-172">**Causa**: este erro pode ocorrer se você tentar enviar para uma ramificação que não seja a mestre no remote 'azure'.</span><span class="sxs-lookup"><span data-stu-id="ab322-172">**Cause**: This error can occur if you attempt to push to a branch other than master on the 'azure' remote.</span></span>

<span data-ttu-id="ab322-173">**Solução**: execute a operação de envio novamente, especificando a ramificação mestre.</span><span class="sxs-lookup"><span data-stu-id="ab322-173">**Resolution**: Perform the push operation again, specifying the master branch.</span></span> <span data-ttu-id="ab322-174">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ab322-174">For example:</span></span>

```bash  
git push azure master
```
- - -
<span data-ttu-id="ab322-175">**Sintoma**: falha de RPC; resultado = 22, código HTTP = 502.</span><span class="sxs-lookup"><span data-stu-id="ab322-175">**Symptom**: RPC failed; result=22, HTTP code = 502.</span></span>

<span data-ttu-id="ab322-176">**Causa**: esse erro poderá ocorrer se você tentar enviar por push um repositório Git de grande porte por HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ab322-176">**Cause**: This error can occur if you attempt to push a large git repository over HTTPS.</span></span>

<span data-ttu-id="ab322-177">**Resolução**: altere a configuração do Git no computador local para aumentar o postBuffer</span><span class="sxs-lookup"><span data-stu-id="ab322-177">**Resolution**: Change the git configuration on the local machine to make the postBuffer bigger</span></span>

```bash  
git config --global http.postBuffer 524288000
```
- - -
<span data-ttu-id="ab322-178">**Sintoma**: erro - alterações confirmadas no repositório remoto, mas o aplicativo Web não foi atualizado.</span><span class="sxs-lookup"><span data-stu-id="ab322-178">**Symptom**: Error - Changes committed to remote repository but your web app not updated.</span></span>

<span data-ttu-id="ab322-179">**Causa**: esse erro poderá ocorrer se você estiver implantando um aplicativo do Node.js que contém um arquivo package.json que especifica os módulos adicionais necessários.</span><span class="sxs-lookup"><span data-stu-id="ab322-179">**Cause**: This error can occur if you are deploying a Node.js app containing a package.json file that specifies additional required modules.</span></span>

<span data-ttu-id="ab322-180">**Resolução**: as mensagens adicionais contendo 'npm ERR!'</span><span class="sxs-lookup"><span data-stu-id="ab322-180">**Resolution**: Additional messages containing 'npm ERR!'</span></span> <span data-ttu-id="ab322-181">devem ser registradas antes desse erro e podem fornecer um contexto extra sobre a falha.</span><span class="sxs-lookup"><span data-stu-id="ab322-181">should be logged prior to this error, and can provide additional context on the failure.</span></span> <span data-ttu-id="ab322-182">A seguir estão as causas conhecidas desse erro e a mensagem 'npm ERR!' correspondente:</span><span class="sxs-lookup"><span data-stu-id="ab322-182">The following are known causes of this error and the corresponding 'npm ERR!'</span></span> <span data-ttu-id="ab322-183">mensagem:</span><span class="sxs-lookup"><span data-stu-id="ab322-183">message:</span></span>

* <span data-ttu-id="ab322-184">**Arquivo malformado package.json**: npm ERR!</span><span class="sxs-lookup"><span data-stu-id="ab322-184">**Malformed package.json file**: npm ERR!</span></span> <span data-ttu-id="ab322-185">Não foi possível ler as dependências.</span><span class="sxs-lookup"><span data-stu-id="ab322-185">Couldn't read dependencies.</span></span>
* <span data-ttu-id="ab322-186">**Um módulo nativo que não tenha uma distribuição binária para o Windows**:</span><span class="sxs-lookup"><span data-stu-id="ab322-186">**Native module that does not have a binary distribution for Windows**:</span></span>
  
  * <span data-ttu-id="ab322-187">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="ab322-187">npm ERR!</span></span> <span data-ttu-id="ab322-188">\`cmd "/c" "node-gyp rebuild"\` falhou com 1</span><span class="sxs-lookup"><span data-stu-id="ab322-188">\`cmd "/c" "node-gyp rebuild"\` failed with 1</span></span>
    
      <span data-ttu-id="ab322-189">OU</span><span class="sxs-lookup"><span data-stu-id="ab322-189">OR</span></span>
  * <span data-ttu-id="ab322-190">npm ERR!</span><span class="sxs-lookup"><span data-stu-id="ab322-190">npm ERR!</span></span> <span data-ttu-id="ab322-191">[modulename@version] preinstall: \`make || gmake\`</span><span class="sxs-lookup"><span data-stu-id="ab322-191">[modulename@version] preinstall: \`make || gmake\`</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ab322-192">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ab322-192">Additional Resources</span></span>
* [<span data-ttu-id="ab322-193">Documentação do Git</span><span class="sxs-lookup"><span data-stu-id="ab322-193">Git documentation</span></span>](http://git-scm.com/documentation)
* [<span data-ttu-id="ab322-194">Documentação do projeto Kudu</span><span class="sxs-lookup"><span data-stu-id="ab322-194">Project Kudu documentation</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="ab322-195">Implantação contínua no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="ab322-195">Continous Deployment to Azure App Service</span></span>](app-service-continuous-deployment.md)
* [<span data-ttu-id="ab322-196">Como usar o PowerShell para o Azure</span><span class="sxs-lookup"><span data-stu-id="ab322-196">How to use PowerShell for Azure</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="ab322-197">Como usar as ferramentas da interface de linha de comando do Azure</span><span class="sxs-lookup"><span data-stu-id="ab322-197">How to use the Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="ab322-198">[Serviço de Aplicativo do Azure]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/</span><span class="sxs-lookup"><span data-stu-id="ab322-198">[Azure App Service]: https://azure.microsoft.com/documentation/articles/app-service-changes-existing-services/</span></span>
[Azure Developer Center]: http://www.windowsazure.com/en-us/develop/overview/
<span data-ttu-id="ab322-199">[Portal do Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="ab322-199">[Azure Portal]: https://portal.azure.com</span></span>
[Git website]: http://git-scm.com
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
<span data-ttu-id="ab322-200">[Interface da Linha de Comandos do Azure]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/</span><span class="sxs-lookup"><span data-stu-id="ab322-200">[Azure Command-Line Interface]: https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-azure-resource-manager/</span></span>

[Using Git with CodePlex]: http://codeplex.codeplex.com/wikipage?title=Using%20Git%20with%20CodePlex&referringTitle=Source%20control%20clients&ProjectName=codeplex
[Quick Start - Mercurial]: http://mercurial.selenic.com/wiki/QuickStart
