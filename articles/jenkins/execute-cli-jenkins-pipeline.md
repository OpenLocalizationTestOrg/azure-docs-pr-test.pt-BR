---
title: "Olá aaaExecute CLI do Azure com Jenkins | Microsoft Docs"
description: Saiba como toouse CLI do Azure toodeploy um Java web tooAzure de aplicativo no Jenkins Pipeline
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
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a><span data-ttu-id="45c88-103">Implantar tooAzure do serviço de aplicativo com Jenkins e Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="45c88-103">Deploy tooAzure App Service with Jenkins and hello Azure CLI</span></span>
<span data-ttu-id="45c88-104">toodeploy um tooAzure de aplicativo web Java, você pode usar a CLI do Azure em [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span><span class="sxs-lookup"><span data-stu-id="45c88-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](https://jenkins.io/doc/book/pipeline/).</span></span> <span data-ttu-id="45c88-105">Neste tutorial, você cria um pipeline de CI/CD em uma VM do Azure, incluindo como:</span><span class="sxs-lookup"><span data-stu-id="45c88-105">In this tutorial, you create a CI/CD pipeline on an Azure VM including how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="45c88-106">Criar uma VM Jenkins</span><span class="sxs-lookup"><span data-stu-id="45c88-106">Create a Jenkins VM</span></span>
> * <span data-ttu-id="45c88-107">Configurar o Jenkins</span><span class="sxs-lookup"><span data-stu-id="45c88-107">Configure Jenkins</span></span>
> * <span data-ttu-id="45c88-108">Criar um aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="45c88-108">Create a web app in Azure</span></span>
> * <span data-ttu-id="45c88-109">Preparar um repositório GitHub</span><span class="sxs-lookup"><span data-stu-id="45c88-109">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="45c88-110">Criar pipeline do Jenkins</span><span class="sxs-lookup"><span data-stu-id="45c88-110">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="45c88-111">Executar o pipeline de saudação e verifique se o aplicativo da web de saudação</span><span class="sxs-lookup"><span data-stu-id="45c88-111">Run hello pipeline and verify hello web app</span></span>

<span data-ttu-id="45c88-112">Este tutorial requer Olá CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="45c88-112">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="45c88-113">versão de hello toofind, execute `az --version`.</span><span class="sxs-lookup"><span data-stu-id="45c88-113">toofind hello version, run `az --version`.</span></span> <span data-ttu-id="45c88-114">Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="45c88-114">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="45c88-115">Criar e configurar uma instância do Jenkins</span><span class="sxs-lookup"><span data-stu-id="45c88-115">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="45c88-116">Se você ainda não tiver um mestre Jenkins, comece com hello [solução modelo](install-jenkins-solution-template.md), que inclui a saudação necessária [as credenciais do Azure](https://plugins.jenkins.io/azure-credentials) plug-in por padrão.</span><span class="sxs-lookup"><span data-stu-id="45c88-116">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes hello required [Azure Credentials](https://plugins.jenkins.io/azure-credentials) plugin by default.</span></span> 

<span data-ttu-id="45c88-117">plug-in de credencial do Azure Olá permite credenciais do principais de serviço do Microsoft Azure toostore na Jenkins.</span><span class="sxs-lookup"><span data-stu-id="45c88-117">hello Azure Credential plugin allows you toostore Microsoft Azure service principal credentials in Jenkins.</span></span> <span data-ttu-id="45c88-118">Na versão 1.2, adicionamos suporte Olá para que esse Jenkins Pipeline possa obter Olá as credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="45c88-118">In version 1.2, we added hello support so that Jenkins Pipeline can get hello Azure credentials.</span></span> 

<span data-ttu-id="45c88-119">Verifique se você tem a versão 1.2 ou posterior:</span><span class="sxs-lookup"><span data-stu-id="45c88-119">Ensure you have version 1.2 or later:</span></span>
* <span data-ttu-id="45c88-120">No painel do Jenkins hello, clique em **Jenkins Gerenciar -> Gerenciador de plug-in ->** e procure **Azure credencial**.</span><span class="sxs-lookup"><span data-stu-id="45c88-120">Within hello Jenkins dashboard, click **Manage Jenkins -> Plugin Manager ->** and search for **Azure Credential**.</span></span> 
* <span data-ttu-id="45c88-121">Atualize plug-in de saudação se Olá versão é anterior 1.2.</span><span class="sxs-lookup"><span data-stu-id="45c88-121">Update hello plugin if hello version is earlier than 1.2.</span></span>

<span data-ttu-id="45c88-122">Java JDK e Maven também são necessários no mestre de Jenkins hello.</span><span class="sxs-lookup"><span data-stu-id="45c88-122">Java JDK and Maven are also required in hello Jenkins master.</span></span> <span data-ttu-id="45c88-123">tooinstall, faça logon no mestre tooJenkins usando SSH e execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="45c88-123">tooinstall, log in tooJenkins master using SSH and run hello following commands:</span></span>
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="45c88-124">Adicionar a credencial de tooJenkins principal de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="45c88-124">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="45c88-125">Uma credencial do Azure é necessário tooexecute CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="45c88-125">An Azure credential is needed tooexecute Azure CLI.</span></span>

* <span data-ttu-id="45c88-126">No painel do Jenkins hello, clique em **credenciais -> sistema ->**.</span><span class="sxs-lookup"><span data-stu-id="45c88-126">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="45c88-127">Clique em **Credenciais globais (irrestrito)**.</span><span class="sxs-lookup"><span data-stu-id="45c88-127">Click **Global credentials(unrestricted)**.</span></span>
* <span data-ttu-id="45c88-128">Clique em **adicionar credenciais** tooadd um [entidade de serviço do Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) preenchendo Olá ID da assinatura, ID do cliente, o segredo de cliente e ponto de extremidade Token OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="45c88-128">Click **Add Credentials** tooadd a [Microsoft Azure service principal](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="45c88-129">Forneça uma ID para uso na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="45c88-129">Provide an ID for use in subsequent step.</span></span>

![Adicionar Credenciais](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a><span data-ttu-id="45c88-131">Criar um serviço de aplicativo do Azure para implantar o aplicativo de web de Java Olá</span><span class="sxs-lookup"><span data-stu-id="45c88-131">Create an Azure App Service for deploying hello Java web app</span></span>

<span data-ttu-id="45c88-132">Criar um plano de serviço de aplicativo do Azure com hello **livre** preço usando Olá [criar plano de serviço de aplicativo az](/cli/azure/appservice/plan#create) comando CLI.</span><span class="sxs-lookup"><span data-stu-id="45c88-132">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="45c88-133">plano de serviço de aplicativo Hello define Olá recursos físicos usados toohost seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="45c88-133">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="45c88-134">Todos os aplicativos atribuídos plano de serviço de aplicativo tooan compartilham esses recursos, permitindo que você toosave custo ao hospedar vários aplicativos.</span><span class="sxs-lookup"><span data-stu-id="45c88-134">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span> 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

<span data-ttu-id="45c88-135">Quando o plano de saudação estiver pronto, Olá que CLI do Azure mostra semelhante saída toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="45c88-135">When hello plan is ready, hello Azure CLI shows similar output toohello following example:</span></span>

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

### <a name="create-an-azure-web-app"></a><span data-ttu-id="45c88-136">Criar um aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="45c88-136">Create an Azure Web app</span></span>

 <span data-ttu-id="45c88-137">Saudação de uso [az webapp criar](/cli/azure/appservice/web#create) toocreate de comando CLI uma definição de aplicativo da web em Olá `myAppServicePlan` plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="45c88-137">Use hello [az webapp create](/cli/azure/appservice/web#create) CLI command toocreate a web app definition in hello `myAppServicePlan` App Service plan.</span></span> <span data-ttu-id="45c88-138">definição de aplicativo da web Hello fornece um URL tooaccess seu aplicativo com e configura toodeploy de várias opções tooAzure seu código.</span><span class="sxs-lookup"><span data-stu-id="45c88-138">hello web app definition provides a URL tooaccess your application with and configures several options toodeploy your code tooAzure.</span></span> 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

<span data-ttu-id="45c88-139">Olá substituto `<app_name>` espaço reservado com seu próprio nome exclusivo do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="45c88-139">Substitute hello `<app_name>` placeholder with your own unique app name.</span></span> <span data-ttu-id="45c88-140">Esse nome exclusivo faz parte saudação padrão do nome de domínio de aplicativo da web hello, para que o nome do hello deve toobe exclusivo entre todos os aplicativos no Azure.</span><span class="sxs-lookup"><span data-stu-id="45c88-140">This unique name is part of hello default domain name for hello web app, so hello name needs toobe unique across all apps in Azure.</span></span> <span data-ttu-id="45c88-141">Você pode mapear um aplicativo web do domínio personalizado nome entrada toohello antes de você expor tooyour usuários.</span><span class="sxs-lookup"><span data-stu-id="45c88-141">You can map a custom domain name entry toohello web app before you expose it tooyour users.</span></span>

<span data-ttu-id="45c88-142">Quando a definição de aplicativo da web hello estiver pronta, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="45c88-142">When hello web app definition is ready, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-java"></a><span data-ttu-id="45c88-143">Configurar o Java</span><span class="sxs-lookup"><span data-stu-id="45c88-143">Configure Java</span></span> 

<span data-ttu-id="45c88-144">Definir a configuração de tempo de execução do Java Olá precisa de seu aplicativo com hello [atualização da configuração az serviço de aplicativo web](/cli/azure/appservice/web/config#update) comando.</span><span class="sxs-lookup"><span data-stu-id="45c88-144">Set up hello Java runtime configuration that your app needs with hello  [az appservice web config update](/cli/azure/appservice/web/config#update) command.</span></span>

<span data-ttu-id="45c88-145">Olá comando a seguir configura Olá web aplicativo toorun em um recente Java 8 JDK e [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="45c88-145">hello following command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a><span data-ttu-id="45c88-146">Preparar um Repositório GitHub</span><span class="sxs-lookup"><span data-stu-id="45c88-146">Prepare a GitHub Repository</span></span>
<span data-ttu-id="45c88-147">Olá abrir [simples aplicativo de Web de Java para o Azure](https://github.com/azure-devops/javawebappsample) repositório.</span><span class="sxs-lookup"><span data-stu-id="45c88-147">Open hello [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo.</span></span> <span data-ttu-id="45c88-148">toofork Olá repositório tooyour possui a conta do GitHub, clique em Olá **bifurcação** botão no canto direito superior de saudação.</span><span class="sxs-lookup"><span data-stu-id="45c88-148">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>

* <span data-ttu-id="45c88-149">Na interface do usuário da Web do GitHub, abra o arquivo **Jenkinsfile**.</span><span class="sxs-lookup"><span data-stu-id="45c88-149">In GitHub web UI, open **Jenkinsfile** file.</span></span> <span data-ttu-id="45c88-150">Clique em tooedit de ícone de lápis Olá este grupo de recursos do arquivo tooupdate hello e o nome do seu aplicativo web na linha 20 e 21 respectivamente.</span><span class="sxs-lookup"><span data-stu-id="45c88-150">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 20 and 21 respectively.</span></span>

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* <span data-ttu-id="45c88-151">Alterar a linha 23 tooupdate identificação da credencial na sua instância Jenkins</span><span class="sxs-lookup"><span data-stu-id="45c88-151">Change line 23 tooupdate credential ID in your Jenkins instance</span></span>

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a><span data-ttu-id="45c88-152">Criar pipeline do Jenkins</span><span class="sxs-lookup"><span data-stu-id="45c88-152">Create Jenkins pipeline</span></span>
<span data-ttu-id="45c88-153">Abra o Jenkins em um navegador da Web, clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="45c88-153">Open Jenkins in a web browser, click **New Item**.</span></span> 

* <span data-ttu-id="45c88-154">Forneça um nome para o trabalho de saudação e selecione **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="45c88-154">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="45c88-155">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="45c88-155">Click **OK**.</span></span>
* <span data-ttu-id="45c88-156">Clique em Olá **Pipeline** próxima guia.</span><span class="sxs-lookup"><span data-stu-id="45c88-156">Click hello **Pipeline** tab next.</span></span> 
* <span data-ttu-id="45c88-157">Para **Definição**, selecione **Script de pipeline do SCM**.</span><span class="sxs-lookup"><span data-stu-id="45c88-157">For **Definition**, select **Pipeline script from SCM**.</span></span>
* <span data-ttu-id="45c88-158">Para **SCM**, selecione **Git**.</span><span class="sxs-lookup"><span data-stu-id="45c88-158">For **SCM**, select **Git**.</span></span>
* <span data-ttu-id="45c88-159">Digite hello GitHub URL para seu repositório bifurcado: https:\<seu repositório bifurcado\>.git</span><span class="sxs-lookup"><span data-stu-id="45c88-159">Enter hello GitHub URL for your forked repo: https:\<your forked repo\>.git</span></span>
* <span data-ttu-id="45c88-160">Clique em **Salvar**</span><span class="sxs-lookup"><span data-stu-id="45c88-160">Click **Save**</span></span>

## <a name="test-your-pipeline"></a><span data-ttu-id="45c88-161">Testar o pipeline</span><span class="sxs-lookup"><span data-stu-id="45c88-161">Test your pipeline</span></span>
* <span data-ttu-id="45c88-162">Vá pipeline toohello que você criou, clique em **criar agora**</span><span class="sxs-lookup"><span data-stu-id="45c88-162">Go toohello pipeline you created, click **Build Now**</span></span>
* <span data-ttu-id="45c88-163">Uma compilação deve ter êxito em alguns segundos e você pode ir de compilação toohello e clique em **saída do Console** detalhes de saudação toosee</span><span class="sxs-lookup"><span data-stu-id="45c88-163">A build should succeed in a few seconds, and you can go toohello build and click **Console Output** toosee hello details</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="45c88-164">Verifique seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="45c88-164">Verify your web app</span></span>
<span data-ttu-id="45c88-165">arquivo do tooverify Olá WAR seja implantado com êxito tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="45c88-165">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="45c88-166">abra um navegador da Web:</span><span class="sxs-lookup"><span data-stu-id="45c88-166">Open a web browser:</span></span>

* <span data-ttu-id="45c88-167">Vá toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping</span><span class="sxs-lookup"><span data-stu-id="45c88-167">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping</span></span>  
<span data-ttu-id="45c88-168">Você verá:</span><span class="sxs-lookup"><span data-stu-id="45c88-168">You see:</span></span>

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* <span data-ttu-id="45c88-169">Vá toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (substitua &lt;x > e &lt;y > com os números) tooget soma de saudação de x e y</span><span class="sxs-lookup"><span data-stu-id="45c88-169">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>

![Calculadora: adicionar](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a><span data-ttu-id="45c88-171">Implantar tooAzure Web App no Linux</span><span class="sxs-lookup"><span data-stu-id="45c88-171">Deploy tooAzure Web App on Linux</span></span>
<span data-ttu-id="45c88-172">Agora que você sabe como toouse CLI do Azure no seu Jenkins pipeline, você pode modificar Olá script toodeploy tooan aplicativo Web do Azure no Linux.</span><span class="sxs-lookup"><span data-stu-id="45c88-172">Now that you know how toouse Azure CLI in your Jenkins pipeline, you can modify hello script toodeploy tooan Azure Web App on Linux.</span></span>

<span data-ttu-id="45c88-173">Web App no Linux oferece suporte a uma implantação de saudação de toodo de maneira diferente, que é toouse Docker.</span><span class="sxs-lookup"><span data-stu-id="45c88-173">Web App on Linux supports a different way toodo hello deployment, which is toouse Docker.</span></span> <span data-ttu-id="45c88-174">toodeploy, é necessário tooprovide um Dockerfile que os pacotes de aplicativos web com o tempo de execução do serviço em uma imagem do Docker.</span><span class="sxs-lookup"><span data-stu-id="45c88-174">toodeploy, you need tooprovide a Dockerfile that packages your web app with service runtime into a Docker image.</span></span> <span data-ttu-id="45c88-175">Olá plug-in será, em seguida, criar imagem hello, por push do registro de Docker tooa e implantar o aplicativo web do hello imagem tooyour.</span><span class="sxs-lookup"><span data-stu-id="45c88-175">hello plugin will then build hello image, push it tooa Docker registry and deploy hello image tooyour web app.</span></span>

* <span data-ttu-id="45c88-176">Siga as etapas de saudação [aqui](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate um aplicativo Web do Azure em execução no Linux.</span><span class="sxs-lookup"><span data-stu-id="45c88-176">Follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate an Azure Web App running on Linux.</span></span>
* <span data-ttu-id="45c88-177">Instalar o Docker em sua instância Jenkins seguindo as instruções de saudação neste [artigo](https://docs.docker.com/engine/installation/linux/ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="45c88-177">Install Docker on your Jenkins instance by following hello instructions in this [article](https://docs.docker.com/engine/installation/linux/ubuntu/).</span></span>
* <span data-ttu-id="45c88-178">Criar um registro de contêiner Olá portal do Azure usando as etapas de saudação [aqui](/azure/container-registry/container-registry-get-started-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="45c88-178">Create a Container Registry in hello Azure portal by using hello steps [here](/azure/container-registry/container-registry-get-started-azure-cli).</span></span>
* <span data-ttu-id="45c88-179">Em Olá mesmo [simples aplicativo de Web de Java para o Azure](https://github.com/azure-devops/javawebappsample) repositório você bifurcado, editar Olá **Jenkinsfile2** arquivo:</span><span class="sxs-lookup"><span data-stu-id="45c88-179">In hello same [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) repo you forked, edit hello **Jenkinsfile2** file:</span></span>
    * <span data-ttu-id="45c88-180">Linha 18-21, atualize os nomes de toohello de seu grupo de recursos, o aplicativo web e o ACR respectivamente.</span><span class="sxs-lookup"><span data-stu-id="45c88-180">Line 18-21, update toohello names of your resource group, web app, and ACR respectively.</span></span> 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * <span data-ttu-id="45c88-181">Linha 24, atualização \<azsrvprincipal\> tooyour identificação da credencial</span><span class="sxs-lookup"><span data-stu-id="45c88-181">Line 24, update \<azsrvprincipal\> tooyour credential ID</span></span>
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* <span data-ttu-id="45c88-182">Criar um novo pipeline Jenkins como você fez ao implantar o aplicativo da web de tooAzure no Windows, somente esse tempo, use **Jenkinsfile2** em vez disso.</span><span class="sxs-lookup"><span data-stu-id="45c88-182">Create a new Jenkins pipeline as you did when deploying tooAzure web app in Windows, only this time, use **Jenkinsfile2** instead.</span></span>
* <span data-ttu-id="45c88-183">Execute seu novo trabalho.</span><span class="sxs-lookup"><span data-stu-id="45c88-183">Run your new job.</span></span>
* <span data-ttu-id="45c88-184">tooverify, na CLI do Azure, execute:</span><span class="sxs-lookup"><span data-stu-id="45c88-184">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="45c88-185">Você obtém Olá resultados a seguir:</span><span class="sxs-lookup"><span data-stu-id="45c88-185">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="45c88-186">Vá toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="45c88-186">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="45c88-187">Você verá a mensagem de saudação:</span><span class="sxs-lookup"><span data-stu-id="45c88-187">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="45c88-188">Vá toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (substitua &lt;x > e &lt;y > com os números) tooget soma de saudação de x e y</span><span class="sxs-lookup"><span data-stu-id="45c88-188">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="45c88-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="45c88-189">Next steps</span></span>
<span data-ttu-id="45c88-190">Neste tutorial, você configurou um pipeline de Jenkins check-out do código-fonte Olá no repositório do GitHub.</span><span class="sxs-lookup"><span data-stu-id="45c88-190">In this tutorial, you configured a Jenkins pipeline that checks out hello source code in GitHub repo.</span></span> <span data-ttu-id="45c88-191">Executa Maven toobuild um arquivo war e, em seguida, usa a CLI do Azure toodeploy tooAzure do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="45c88-191">Runs Maven toobuild a war file and then uses Azure CLI toodeploy tooAzure App Service.</span></span> <span data-ttu-id="45c88-192">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="45c88-192">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="45c88-193">Criar uma VM Jenkins</span><span class="sxs-lookup"><span data-stu-id="45c88-193">Create a Jenkins VM</span></span>
> * <span data-ttu-id="45c88-194">Configurar o Jenkins</span><span class="sxs-lookup"><span data-stu-id="45c88-194">Configure Jenkins</span></span>
> * <span data-ttu-id="45c88-195">Criar um aplicativo Web no Azure</span><span class="sxs-lookup"><span data-stu-id="45c88-195">Create a web app in Azure</span></span>
> * <span data-ttu-id="45c88-196">Preparar um repositório GitHub</span><span class="sxs-lookup"><span data-stu-id="45c88-196">Prepare a GitHub repository</span></span>
> * <span data-ttu-id="45c88-197">Criar pipeline do Jenkins</span><span class="sxs-lookup"><span data-stu-id="45c88-197">Create Jenkins pipeline</span></span>
> * <span data-ttu-id="45c88-198">Executar o pipeline de saudação e verifique se o aplicativo da web de saudação</span><span class="sxs-lookup"><span data-stu-id="45c88-198">Run hello pipeline and verify hello web app</span></span>
