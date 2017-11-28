<span data-ttu-id="fc632-101">Configure a implantação local do Git para o aplicativo Web com o comando [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git).</span><span class="sxs-lookup"><span data-stu-id="fc632-101">Configure local Git deployment to the web app with the [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command.</span></span>

<span data-ttu-id="fc632-102">O Serviço de Aplicativo oferece suporte a várias maneiras de implantar conteúdo em um aplicativo Web, como FTP, Git local, GitHub, Visual Studio Team Services e Bitbucket.</span><span class="sxs-lookup"><span data-stu-id="fc632-102">App Service supports several ways to deploy content to a web app, such as FTP, local Git, GitHub, Visual Studio Team Services, and Bitbucket.</span></span> <span data-ttu-id="fc632-103">Para este início rápido, implante usando o Git local.</span><span class="sxs-lookup"><span data-stu-id="fc632-103">For this quickstart, you deploy by using local Git.</span></span> <span data-ttu-id="fc632-104">Isso significa que você implanta usando um comando Git para enviar por push de um repositório local para um repositório no Azure.</span><span class="sxs-lookup"><span data-stu-id="fc632-104">That means you deploy by using a Git command to push from a local repository to a repository in Azure.</span></span> 

<span data-ttu-id="fc632-105">No comando a seguir, substitua *\<nome_do_aplicativo >* pelo nome do seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="fc632-105">In the following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="fc632-106">A saída tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="fc632-106">The output has the following format:</span></span>

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

<span data-ttu-id="fc632-107">O `<username>` é o [usuário de implantação](#configure-a-deployment-user) que você criou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="fc632-107">The `<username>` is the [deployment user](#configure-a-deployment-user) that you created in a previous step.</span></span>

<span data-ttu-id="fc632-108">Copie o URI exibido; você o usará na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="fc632-108">Copy the URI shown; you'll use it in the next step.</span></span>
