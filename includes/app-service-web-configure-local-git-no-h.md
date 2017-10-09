<span data-ttu-id="e6ad5-101">Configurar o aplicativo web local Git implantação toohello com hello [origem de implantação de aplicativo Web do az-config-local-git](/cli/azure/webapp/deployment/source#config-local-git) comando.</span><span class="sxs-lookup"><span data-stu-id="e6ad5-101">Configure local Git deployment toohello web app with hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="e6ad5-102">Serviço de aplicativo oferece suporte a várias maneiras toodeploy tooa conteúdo aplicativo web, como FTP, Git local, GitHub, Visual Studio Team Services e Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="e6ad5-102">App Service supports several ways toodeploy content tooa web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="e6ad5-103">Para este início rápido, implante usando o Git local.</span><span class="sxs-lookup"><span data-stu-id="e6ad5-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="e6ad5-104">Isso significa que você implantar usando um toopush de comando Git de um repositório de tooa repositório local no Azure.</span><span class="sxs-lookup"><span data-stu-id="e6ad5-104">That means you deploy by using a Git command toopush from a local repository tooa repository in Azure.</span></span> 

<span data-ttu-id="e6ad5-105">Olá a seguir de comando, substitua  *\<app_name >* com o nome do seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="e6ad5-105">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="e6ad5-106">saída de Hello tem Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="e6ad5-106">hello output has hello following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="e6ad5-107">Olá `<username>` é hello [usuário de implantação](#configure-a-deployment-user) que você criou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="e6ad5-107">hello `<username>` is hello [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="e6ad5-108">Copiar Olá URI mostrada; Você vai usá-lo na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="e6ad5-108">Copy hello URI shown; you'll use it in hello next step.</span></span>
