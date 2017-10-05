---
title: Executar a CLI do Azure com o Jenkins | Microsoft Docs
description: Saiba como usar a CLI do Azure para implantar um aplicativo Web do Java no Azure na pipeline do Jenkins
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 5ca8338d4bf343f08fe70081cff755fa76a126a9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-app-service-with-jenkins-and-the-azure-cli"></a><span data-ttu-id="77dcf-103">Implantar o Serviço de Aplicativo do Azure com o Jenkins e a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="77dcf-103">Deploy to Azure App Service with Jenkins and the Azure CLI</span></span>
<span data-ttu-id="77dcf-104">Para implantar um aplicativo Web do Java no Azure, você pode usar a CLI do Azure na [pipeline do Jenkins](https://jenkins.io/doc/book/pipeline/).</span><span class="sxs-lookup"><span data-stu-id="77dcf-104">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="77dcf-105">Neste tutorial, você cria um pipeline de CI/CD em uma VM do Azure, incluindo como:</span><span class="sxs-lookup"><span data-stu-id="77dcf-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="77dcf-106">Criar uma VM Jenkins</span><span class="sxs-lookup"><span data-stu-id="77dcf-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="77dcf-107">Configurar o Jenkins</span><span class="sxs-lookup"><span data-stu-id="77dcf-107">Configure Jenkins</span></span>
> * <span data-ttu-id="77dcf-108">Criar um aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="77dcf-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="77dcf-109">Preparar um repositório GitHub</span><span class="sxs-lookup"><span data-stu-id="77dcf-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="77dcf-110">Criar pipeline do Jenkins</span><span class="sxs-lookup"><span data-stu-id="77dcf-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="77dcf-111">Executar o pipeline e verificar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="77dcf-111">Run the pipeline and verify the web app</span></span>

<span data-ttu-id="77dcf-112">Este tutorial requer a CLI do Azure, versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="77dcf-112">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="77dcf-113">Para saber qual é a versão, execute `az --version`.</span><span class="sxs-lookup"><span data-stu-id="77dcf-113">To find the version, run `az --version`.</span></span> <span data-ttu-id="77dcf-114">Se você precisar atualizar, confira [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="77dcf-114">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="77dcf-115">Criar e configurar uma instância do Jenkins</span><span class="sxs-lookup"><span data-stu-id="77dcf-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="77dcf-116">Se você ainda não tiver um mestre do Jenkins, comece com o [Modelo de solução](install-jenkins-solution-template.md), que inclui o plug-in [Credenciais do Azure](https://plugins.jenkins.io/azure-credentials) necessário por padrão.</span><span class="sxs-lookup"><span data-stu-id="77dcf-116">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes the required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="77dcf-117">O plug-in Credencial do Azure permite que você armazene as credenciais de entidade de serviço do Microsoft Azure no Jenkins.</span><span class="sxs-lookup"><span data-stu-id="77dcf-117">The Azure Credential plugin allows you to store Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="77dcf-118">Na versão 1.2, adicionamos suporte para que esse pipeline do Jenkins possa obter as credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="77dcf-118">In version 1.2, we added the support so that Jenkins Pipeline can get the Azure credentials.</span></span> 

<span data-ttu-id="77dcf-119">Verifique se você tem a versão 1.2 ou posterior:</span><span class="sxs-lookup"><span data-stu-id="77dcf-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="77dcf-120">No painel do Jenkins, clique em **Gerenciar Jenkins -> Gerenciador de plug-ins ->** e pesquise pela **Credencial do Azure**.</span><span class="sxs-lookup"><span data-stu-id="77dcf-120">Within the Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="77dcf-121">Atualize o plug-in se a versão for anterior à 1.2.</span><span class="sxs-lookup"><span data-stu-id="77dcf-121">Update the plugin if the version is earlier than 1.2.</span></span>

<span data-ttu-id="77dcf-122">O Java JDK e o Maven também são necessários no mestre do Jenkins.</span><span class="sxs-lookup"><span data-stu-id="77dcf-122">Java JDK and Maven are also required in the Jenkins master.</span></span> <span data-ttu-id="77dcf-123">Para instalar, faça logon no mestre do Jenkins usando o SSH e execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="77dcf-123">To install, log in to Jenkins master using SSH and run the following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-to-jenkins-credential"></a><span data-ttu-id="77dcf-124">Adicione uma entidade de serviço do Azure na credencial do Jenkins</span><span class="sxs-lookup"><span data-stu-id="77dcf-124">Add Azure service principal to Jenkins credential</span></span>

<span data-ttu-id="77dcf-125">Uma credencial do Azure é necessária para executar a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="77dcf-125">An Azure credential is needed to execute Azure CLI.</span></span>

* <span data-ttu-id="77dcf-126">No painel do Jenkins, clique em **Credenciais -> Sistema ->**.</span><span class="sxs-lookup"><span data-stu-id="77dcf-126">Within the Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="77dcf-127">Clique em **Credenciais globais (irrestrito)**.</span><span class="sxs-lookup"><span data-stu-id="77dcf-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="77dcf-128">Clique em **Adicionar credenciais** para adicionar uma [entidade de serviço do Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json), preenchendo a ID da assinatura, a ID do cliente, o segredo do cliente e o Ponto de Extremidade do Token OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="77dcf-128">Click **Add Credentials** to add a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="77dcf-129">Forneça uma ID para uso na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="77dcf-129">Provide an ID for use in subsequent step.</span></span>

![Adicionar Credenciais](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-the-java-web-app"></a><span data-ttu-id="77dcf-131">Criar um Serviço de Aplicativo do Azure para implantar o aplicativo Web Java</span><span class="sxs-lookup"><span data-stu-id="77dcf-131">Create an Azure App Service for deploying the Java web app</span></span>

<span data-ttu-id="77dcf-132">Crie um plano do Serviço de Aplicativo do Azure com o tipo de preço **GRÁTIS** usando a CLI de comando [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="77dcf-132">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="77dcf-133">O plano do serviço de aplicativo define os recursos físicos usados para hospedar seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="77dcf-133">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="77dcf-134">Todos os aplicativos atribuídos a um plano do serviço de aplicativo compartilham esses recursos, permitindo que você economize hospedando vários aplicativos.</span><span class="sxs-lookup"><span data-stu-id="77dcf-134">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="77dcf-135">Quando o plano estiver pronto, a CLI do Azure mostra uma saída semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="77dcf-135">When the plan is ready, the Azure CLI shows similar output to the following example:</span></span>

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a><span data-ttu-id="77dcf-136">Criar um aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="77dcf-136">Create an Azure Web app</span></span>

 <span data-ttu-id="77dcf-137">Use a CLI de comando [az webapp create](/cli/azure/appservice/web#create) para criar uma definição de aplicativo Web no `myAppServicePlan` Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77dcf-137">Use the [az webapp create](/cli/azure/appservice/web#create) CLI command to create a web app definition in the `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="77dcf-138">A definição de aplicativo Web fornece uma URL para acessar seu aplicativo e define várias opções para implantar seu código no Azure.</span><span class="sxs-lookup"><span data-stu-id="77dcf-138">The web app definition provides a URL to access your application with and configures several options to deploy your code to Azure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="77dcf-139">Substitua o espaço reservado `<app_name>` por seu próprio nome exclusivo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77dcf-139">Substitute the `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="77dcf-140">Esse nome exclusivo é parte do nome de domínio padrão para o aplicativo Web, portanto, o nome precisa ser exclusivo entre todos os aplicativos no Azure.</span><span class="sxs-lookup"><span data-stu-id="77dcf-140">This unique name is part of the default domain name for the web app, so the name needs to be unique across all apps in Azure.</span></span> <span data-ttu-id="77dcf-141">Você poderá mapear uma entrada de nome de domínio personalizada para o aplicativo Web antes de expor para seus usuários.</span><span class="sxs-lookup"><span data-stu-id="77dcf-141">You can map a custom domain name entry to the web app before you expose it to your users.</span></span>

<span data-ttu-id="77dcf-142">Quando a definição do aplicativo Web tiver pronta, a CLI do Azure mostrará informações semelhantes ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="77dcf-142">When the web app definition is ready, the Azure CLI shows information similar to the following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a><span data-ttu-id="77dcf-143">Configurar o Java</span><span class="sxs-lookup"><span data-stu-id="77dcf-143">Configure Java</span></span> 

<span data-ttu-id="77dcf-144">Definir a configuração de tempo de execução Java que seu aplicativo precisa com o comando [az appservice web config update](/cli/azure/appservice/web/config#update).</span><span class="sxs-lookup"><span data-stu-id="77dcf-144">Set up the Java runtime configuration that your app needs with the  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="77dcf-145">O comando a seguir configura o aplicativo Web para ser executado em um JDK 8 Java recente e [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="77dcf-145">The following command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="77dcf-146">Preparar um Repositório GitHub</span><span class="sxs-lookup"><span data-stu-id="77dcf-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="77dcf-147">Abra o repositório [Aplicativo Web Java simples para o Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="77dcf-147">Open the [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="77dcf-148">Para bifurcar o repositório para sua própria conta do GitHub, clique no botão **Bifurcação** no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="77dcf-148">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>

* <span data-ttu-id="77dcf-149">Na interface do usuário da Web do GitHub, abra o arquivo **Jenkinsfile**.</span><span class="sxs-lookup"><span data-stu-id="77dcf-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="77dcf-150">Clique no ícone de lápis para editar esse arquivo para atualizar o grupo de recursos e o nome do seu aplicativo Web nas linhas 20 e 21, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="77dcf-150">Click the pencil icon to edit this file to update the resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="77dcf-151">Altere a linha 23 para atualizar a ID de credencial na sua instância do Jenkins</span><span class="sxs-lookup"><span data-stu-id="77dcf-151">Change line 23 to update credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="77dcf-152">Criar pipeline do Jenkins</span><span class="sxs-lookup"><span data-stu-id="77dcf-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="77dcf-153">Abra o Jenkins em um navegador da Web, clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="77dcf-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="77dcf-154">Dê um nome para o trabalho e selecione **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="77dcf-154">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="77dcf-155">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="77dcf-155">Click **OK**.</span></span>
* <span data-ttu-id="77dcf-156">Clique na próxima guia **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="77dcf-156">Click the **Pipeline** tab next.</span></span> 
* <span data-ttu-id="77dcf-157">Para **Definição**, selecione **Script de pipeline do SCM**.</span><span class="sxs-lookup"><span data-stu-id="77dcf-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="77dcf-158">Para **SCM**, selecione **Git**.</span><span class="sxs-lookup"><span data-stu-id="77dcf-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="77dcf-159">Insira a URL do GitHub em seu repositório bifurcado: https:\<seu repositório bifurcado\>.git</span><span class="sxs-lookup"><span data-stu-id="77dcf-159">Enter the GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="77dcf-160">Clique em **Salvar**</span><span class="sxs-lookup"><span data-stu-id="77dcf-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="77dcf-161">Testar o pipeline</span><span class="sxs-lookup"><span data-stu-id="77dcf-161">Test your pipeline</span></span>
* <span data-ttu-id="77dcf-162">Acesse o pipeline que você criou, clique em **Compilar agora**</span><span class="sxs-lookup"><span data-stu-id="77dcf-162">Go to the pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="77dcf-163">Um build deve ter êxito em poucos segundos e você pode acessar o build e clicar em **Saída do Console** para ver os detalhes</span><span class="sxs-lookup"><span data-stu-id="77dcf-163">A build should succeed in a few seconds, and you can go to the build and click **Console Output** to see the details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="77dcf-164">Verifique seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="77dcf-164">Verify your web app</span></span>
<span data-ttu-id="77dcf-165">Para verificar se o arquivo WAR foi implantado com êxito em seu aplicativo Web,</span><span class="sxs-lookup"><span data-stu-id="77dcf-165">To verify the WAR file is deployed successfully to your web app.</span></span> <span data-ttu-id="77dcf-166">abra um navegador da Web:</span><span class="sxs-lookup"><span data-stu-id="77dcf-166">Open a web browser:</span></span>

* <span data-ttu-id="77dcf-167">Acesse http://&lt;app_name>.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="77dcf-167">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="77dcf-168">Você verá:</span><span class="sxs-lookup"><span data-stu-id="77dcf-168">You see:</span></span>

        Welcome to Java Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="77dcf-169">Acesse http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitua &lt;x > e &lt;y > por qualquer número) para obter a soma de x e y</span><span class="sxs-lookup"><span data-stu-id="77dcf-169">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>

![Calculadora: adicionar](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-to-azure-web-app-on-linux"></a><span data-ttu-id="77dcf-171">Implantar no Aplicativo Web do Azure no Linux</span><span class="sxs-lookup"><span data-stu-id="77dcf-171">Deploy to Azure Web App on Linux</span></span>
<span data-ttu-id="77dcf-172">Agora que você sabe como usar a CLI do Azure em seu pipeline Jenkins, você pode modificar o script para implantar um aplicativo Web do Azure no Linux.</span><span class="sxs-lookup"><span data-stu-id="77dcf-172">Now that you know how to use Azure CLI in your Jenkins pipeline, you can modify the script to deploy to an Azure Web App on Linux.</span></span>

<span data-ttu-id="77dcf-173">O aplicativo Web no Linux dá suporte a uma forma diferente de fazer a implantação, que é usar o Docker.</span><span class="sxs-lookup"><span data-stu-id="77dcf-173">Web App on Linux supports a different way to do the deployment, which is to use Docker.</span></span> <span data-ttu-id="77dcf-174">Para implantar, você precisa fornecer um Dockerfile que empacote seu aplicativo Web com tempo de execução do serviço em uma imagem do Docker.</span><span class="sxs-lookup"><span data-stu-id="77dcf-174">To deploy, you need to provide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="77dcf-175">O plug-in, então, compilará a imagem, a enviará por push a um registro de Docker e a implantará em seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="77dcf-175">The plugin will then build the image, push it to a Docker registry and deploy the image to your web app.</span></span>

* <span data-ttu-id="77dcf-176">Siga as etapas [aqui](/azure/app-service-web/app-service-linux-how-to-create-web-app) para criar um aplicativo Web do Azure em execução no Linux.</span><span class="sxs-lookup"><span data-stu-id="77dcf-176">Follow the steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) to create an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="77dcf-177">Instale o Docker em sua instância do Jenkins seguindo as instruções deste [artigo](https://docs.docker.com/engine/installation/linux/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="77dcf-177">Install Docker on your Jenkins instance by following the instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="77dcf-178">Crie um registro de contêiner no Portal do Azure seguindo as etapas [aqui](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="77dcf-178">Create a Container Registry in the Azure portal by using the steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="77dcf-179">No mesmo repositório bifurcado do [Aplicativo Web Java Simples para o Azure](https://github.com/azure-devops/javawebappsample), edite o arquivo **Jenkinsfile2**:</span><span class="sxs-lookup"><span data-stu-id="77dcf-179">In the same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit the **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="77dcf-180">Nas linhas 18-21, atualize com os nomes do grupo de recursos, do aplicativo Web e do ACR, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="77dcf-180">Line 18-21, update to the names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="77dcf-181">Na linha 24, atualize \<azsrvprincipal\> com sua ID de credencial</span><span class="sxs-lookup"><span data-stu-id="77dcf-181">Line 24, update \<azsrvprincipal\> to your credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="77dcf-182">Crie um novo pipeline do Jenkins como fez ao implantar o aplicativo Web do Azure no Windows. Mas, somente dessa vez, use o **Jenkinsfile2**.</span><span class="sxs-lookup"><span data-stu-id="77dcf-182">Create a new Jenkins pipeline as you did when deploying to Azure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="77dcf-183">Execute seu novo trabalho.</span><span class="sxs-lookup"><span data-stu-id="77dcf-183">Run your new job.</span></span>
* <span data-ttu-id="77dcf-184">Para verificar, na CLI do Azure, execute:</span><span class="sxs-lookup"><span data-stu-id="77dcf-184">To verify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="77dcf-185">Você obterá o seguinte resultado:</span><span class="sxs-lookup"><span data-stu-id="77dcf-185">You get the following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="77dcf-186">Acesse http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="77dcf-186">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="77dcf-187">Você verá a mensagem:</span><span class="sxs-lookup"><span data-stu-id="77dcf-187">You see the message:</span></span> 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="77dcf-188">Acesse http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitua &lt;x > e &lt;y > por qualquer número) para obter a soma de x e y</span><span class="sxs-lookup"><span data-stu-id="77dcf-188">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="77dcf-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="77dcf-189">Next steps</span></span>
<span data-ttu-id="77dcf-190">Neste tutorial, você configurou um pipeline do Jenkins que verifica o código-fonte no repositório do GitHub,</span><span class="sxs-lookup"><span data-stu-id="77dcf-190">In this tutorial, you configured a Jenkins pipeline that checks out the source code in GitHub repo.</span></span> <span data-ttu-id="77dcf-191">executa o Maven para compilar um arquivo war e, então, usa a CLI do Azure para implantar o Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="77dcf-191">Runs Maven to build a war file and then uses Azure CLI to deploy to Azure App Service.</span></span> <span data-ttu-id="77dcf-192">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="77dcf-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="77dcf-193">Criar uma VM Jenkins</span><span class="sxs-lookup"><span data-stu-id="77dcf-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="77dcf-194">Configurar o Jenkins</span><span class="sxs-lookup"><span data-stu-id="77dcf-194">Configure Jenkins</span></span>
> * <span data-ttu-id="77dcf-195">Criar um aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="77dcf-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="77dcf-196">Preparar um repositório GitHub</span><span class="sxs-lookup"><span data-stu-id="77dcf-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="77dcf-197">Criar pipeline do Jenkins</span><span class="sxs-lookup"><span data-stu-id="77dcf-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="77dcf-198">Executar o pipeline e verificar o aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="77dcf-198">Run the pipeline and verify the web app</span></span>
