---
title: "Implantar o Serviço de Aplicativo do Azure com o Plug-in Jenkins | Microsoft Docs"
description: "Saiba como usar o plug-in Jenkins do Serviço de Aplicativo do Azure para implantar um aplicativo Web do Java no Azure no Jenkins"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 646daad1785f3de067544b6dd38abfcb6bc67d4a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-to-azure-app-service-with-jenkins-plugin"></a><span data-ttu-id="f2483-103">Implantar para o Serviço de Aplicativo do Azure com o Plug-in Jenkins</span><span class="sxs-lookup"><span data-stu-id="f2483-103">Deploy to Azure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="f2483-104">Para implantar um aplicativo Web do Java no Azure, você pode usar a CLI do Azure no [Pipeline do Jenkins](/azure/jenkins/execute-cli-jenkins-pipeline) ou você pode fazer uso do [Plug-in Jenkins do Serviço de Aplicativo do Azure](https://plugins.jenkins.io/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="f2483-104">To deploy a Java web app to Azure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of the [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="f2483-105">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="f2483-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f2483-106">Configurar Jenkins para implantar para o Serviço de Aplicativo do Azure via FTP</span><span class="sxs-lookup"><span data-stu-id="f2483-106">Configure Jenkins to deploy to Azure App Service through FTP</span></span> 
> * <span data-ttu-id="f2483-107">Configurar o Jenkins para implantar o Serviço de Aplicativo do Azure em Linux por meio do Docker</span><span class="sxs-lookup"><span data-stu-id="f2483-107">Configure Jenkins to deploy to Azure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="f2483-108">Criar e configurar uma instância do Jenkins</span><span class="sxs-lookup"><span data-stu-id="f2483-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="f2483-109">Se você ainda não tiver um mestre do Jenkins, comece com o [Modelo de Solução](install-jenkins-solution-template.md), que inclui o JDK8 e os plug-ins necessários a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2483-109">If you do not already have a Jenkins master, start with the [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and the following required plugins:</span></span>

* <span data-ttu-id="f2483-110">[Plug-in de cliente Git do Jenkins](https://plugins.jenkins.io/git-client) v.2.4.6</span><span class="sxs-lookup"><span data-stu-id="f2483-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="f2483-111">[Plug-in Docker Commons](https://plugins.jenkins.io/docker-commons) v.1.4.0</span><span class="sxs-lookup"><span data-stu-id="f2483-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="f2483-112">[Credenciais do Azure](https://plugins.jenkins.io/azure-credentials) v.1.2</span><span class="sxs-lookup"><span data-stu-id="f2483-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="f2483-113">[Serviço de Aplicativo do Azure](https://plugins.jenkins.io/azure-app-server) v.0.1</span><span class="sxs-lookup"><span data-stu-id="f2483-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="f2483-114">Você pode usar o plug-in do Serviço de Aplicativo para implantar o aplicativo Web em todas as linguagens (por exemplo, C#, PHP, Java e node.js, etc.) com suporte pelo Serviço de Aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2483-114">You can use the App Service plugin to deploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="f2483-115">Neste tutorial, estamos usando o aplicativo Java de exemplo, [Aplicativo Web Java Simples para o Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="f2483-115">In this tutorial, we are using the sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="f2483-116">Para bifurcar o repositório para sua própria conta do GitHub, clique no botão **Bifurcação** no canto superior direito.</span><span class="sxs-lookup"><span data-stu-id="f2483-116">To fork the repo to your own GitHub account, click the **Fork** button in the top right-hand corner.</span></span>  

<span data-ttu-id="f2483-117">O Java JDK e o Maven são necessários para compilar o projeto Java.</span><span class="sxs-lookup"><span data-stu-id="f2483-117">Java JDK and Maven are required for building the Java project.</span></span> <span data-ttu-id="f2483-118">Verifique se você instalou os componentes no mestre do Jenkins ou no agente de VM, caso você use um deles para a integração contínua.</span><span class="sxs-lookup"><span data-stu-id="f2483-118">Make sure you install the components in the Jenkins master or the VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="f2483-119">Para instalar, faça logon na instância do Jenkins usando o SSH e execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="f2483-119">To install, log in to the Jenkins instance using SSH and run the following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="f2483-120">Para implantar o Serviço de Aplicativo no Linux, você também precisa instalar o Docker no mestre do Jenkins ou no agente de VM usado para o build.</span><span class="sxs-lookup"><span data-stu-id="f2483-120">For deploying to App Service on Linux, you also need to install Docker on the Jenkins master or the VM agent used for build.</span></span> <span data-ttu-id="f2483-121">Consulte este artigo para instalar o Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span><span class="sxs-lookup"><span data-stu-id="f2483-121">Refer to this article to install Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-to-jenkins-credential"></a><span data-ttu-id="f2483-122">Adicione uma entidade de serviço do Azure na credencial do Jenkins</span><span class="sxs-lookup"><span data-stu-id="f2483-122">Add Azure service principal to Jenkins credential</span></span>

<span data-ttu-id="f2483-123">Uma entidade de serviço do Azure é necessária para implantar no Azure.</span><span class="sxs-lookup"><span data-stu-id="f2483-123">An Azure service principal is needed to deploy to Azure.</span></span> 

<ol>
<li><span data-ttu-id="f2483-124">Use a [CLI do Azure](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) ou o [Portal do Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal) para criar uma entidade de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="f2483-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) to create an Azure service principal</span></span></li>
<li><span data-ttu-id="f2483-125">No painel do Jenkins, clique em **Credenciais -> Sistema ->**.</span><span class="sxs-lookup"><span data-stu-id="f2483-125">Within the Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="f2483-126">Clique em **Credenciais globais (irrestrito)**.</span><span class="sxs-lookup"><span data-stu-id="f2483-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="f2483-127">Clique em **Adicionar credenciais** para adicionar uma entidade de serviço do Microsoft Azure, preenchendo a ID da assinatura, a ID do cliente, o segredo do cliente e o Ponto de Extremidade do Token OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="f2483-127">Click **Add Credentials** to add a Microsoft Azure service principal by filling out the Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="f2483-128">Forneça uma ID, **mySp**, para uso na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="f2483-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="f2483-129">Plug-in do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="f2483-129">Azure App Service plugin</span></span>

<span data-ttu-id="f2483-130">O plug-in do Serviço de Aplicativo do Azure v1.0 dá suporte à implantação contínua para o aplicativo Web do Azure por meio de:</span><span class="sxs-lookup"><span data-stu-id="f2483-130">Azure App Service plugin v1.0 supports continuous deployment to Azure Web App through:</span></span>

* <span data-ttu-id="f2483-131">Git e FTP</span><span class="sxs-lookup"><span data-stu-id="f2483-131">Git and FTP</span></span>
* <span data-ttu-id="f2483-132">Docker para Aplicativo Web no Linux</span><span class="sxs-lookup"><span data-stu-id="f2483-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-to-deploy-web-app-through-ftp-using-the-jenkins-dashboard"></a><span data-ttu-id="f2483-133">Configurar o Jenkins para implantar o aplicativo Web via FTP usando o painel do Jenkins</span><span class="sxs-lookup"><span data-stu-id="f2483-133">Configure Jenkins to deploy Web App through FTP using the Jenkins dashboard</span></span>

<span data-ttu-id="f2483-134">Para implantar seu projeto de aplicativo Web do Azure, você pode carregar seus artefatos de build (por exemplo, o arquivo .war em Java) usando o Git ou FTP.</span><span class="sxs-lookup"><span data-stu-id="f2483-134">To deploy your project to Azure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="f2483-135">Antes de configurar o trabalho em Jenkins, você precisa de um plano do Serviço de Aplicativo do Azure e de um aplicativo Web para executar o aplicativo Java.</span><span class="sxs-lookup"><span data-stu-id="f2483-135">Before setting up the job in Jenkins, you need an Azure App Service plan and a Web App for running the Java app.</span></span>


1. <span data-ttu-id="f2483-136">Crie um plano do Serviço de Aplicativo do Azure com o tipo de preço **GRÁTIS** usando a CLI de comando [az appservice plan create](/cli/azure/appservice/plan#create).</span><span class="sxs-lookup"><span data-stu-id="f2483-136">Create an Azure App Service plan with the **FREE** pricing tier using the  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="f2483-137">O plano do serviço de aplicativo define os recursos físicos usados para hospedar seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f2483-137">The appservice plan defines the physical resources used to host your apps.</span></span> <span data-ttu-id="f2483-138">Todos os aplicativos atribuídos a um plano do serviço de aplicativo compartilham esses recursos, permitindo que você economize hospedando vários aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f2483-138">All applications assigned to an appservice plan share these resources, allowing you to save cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="f2483-139">Crie um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="f2483-139">Create a Web App.</span></span> <span data-ttu-id="f2483-140">Você pode usar o [Portal do Azure](/azure/app-service-web/web-sites-configure) ou use o seguinte comando da CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="f2483-140">You can either use the [Azure portal](/azure/app-service-web/web-sites-configure) or use the following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="f2483-141">Verifique se que você definiu a configuração de tempo de execução do Java que seu aplicativo precisa.</span><span class="sxs-lookup"><span data-stu-id="f2483-141">Make sure you set up the Java runtime configuration that your app needs.</span></span> <span data-ttu-id="f2483-142">O comando da CLI do Azure a seguir configura o aplicativo Web para ser executado em um JDK 8 Java recente e [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="f2483-142">The following Azure CLI command configures the web app to run on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-the-jenkins-job"></a><span data-ttu-id="f2483-143">Configurar o trabalho do Jenkins</span><span class="sxs-lookup"><span data-stu-id="f2483-143">Set up the Jenkins job</span></span>


1. <span data-ttu-id="f2483-144">Criar um novo projeto de **estilo livre** no painel do Jenkins</span><span class="sxs-lookup"><span data-stu-id="f2483-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="f2483-145">Configure o **Gerenciamento de Código-fonte** para usar o seu fork local de [Aplicativo Web Java simples para o Azure](https://github.com/azure-devops/javawebappsample), fornecendo a **URL do Repositório**.</span><span class="sxs-lookup"><span data-stu-id="f2483-145">Configure **Source Code Management** to use your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing the **Repository URL**.</span></span> <span data-ttu-id="f2483-146">Por exemplo: http://github.com/&lt;yourID>/aplicativowebjavadeexemplo.</span><span class="sxs-lookup"><span data-stu-id="f2483-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="f2483-147">Adicione uma etapa de build para compilar o projeto usando o Maven.</span><span class="sxs-lookup"><span data-stu-id="f2483-147">Add a Build step to build the project using Maven.</span></span> <span data-ttu-id="f2483-148">Faça isso adicionando um **Executar shell**.</span><span class="sxs-lookup"><span data-stu-id="f2483-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="f2483-149">Neste exemplo, precisamos de uma etapa adicional para renomear o arquivo *.war na pasta de destino para ROOT.war.</span><span class="sxs-lookup"><span data-stu-id="f2483-149">For this example, we need an additional step to rename the *.war file in target folder to ROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="f2483-150">Adicione uma ação pós-build selecionando **Publicar um Aplicativo Web do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f2483-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="f2483-151">Forneça "mySp", a entidade de serviço do Azure armazenada na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="f2483-151">Supply, "mySp", the Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="f2483-152">Em **Configuração do Aplicativo**, escolha o aplicativo Web e o grupo de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="f2483-152">In **App Configuration** section, choose the resource group and web app in your subscription.</span></span> <span data-ttu-id="f2483-153">O plug-in detecta automaticamente se o aplicativo Web é do Windows ou do Linux.</span><span class="sxs-lookup"><span data-stu-id="f2483-153">The plugin automatically detects whether the Web App is Windows or Linux-based.</span></span> <span data-ttu-id="f2483-154">Para um aplicativo Web baseado em Windows, a opção "Publicar Arquivos" é apresentada.</span><span class="sxs-lookup"><span data-stu-id="f2483-154">For a Windows-based Web App, the option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="f2483-155">Preencha os arquivos que você deseja implantar (por exemplo, um pacote war se você estiver usando o Java.) O Diretório de Origem e o Diretório de Destino são opcionais.</span><span class="sxs-lookup"><span data-stu-id="f2483-155">Fill in the files you want to deploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="f2483-156">Os parâmetros permitem que você especifique as pastas de origem e de destino ao carregar arquivos.</span><span class="sxs-lookup"><span data-stu-id="f2483-156">The parameters allow you to specify source and target folders when uploading files.</span></span> <span data-ttu-id="f2483-157">O aplicativo Web Java no Azure é executado em um servidor Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f2483-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="f2483-158">Desse modo, você carrega o pacote war para a pasta webapps.</span><span class="sxs-lookup"><span data-stu-id="f2483-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="f2483-159">Neste exemplo, defina **Diretório de Origem** como "destino" e forneça "webapps" como **Diretório de Destino**.</span><span class="sxs-lookup"><span data-stu-id="f2483-159">For this example, set **Source Directory** to "target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="f2483-160">Se você deseja implantar em um slot que não seja de produção, você também pode definir o Nome do **Slot**.</span><span class="sxs-lookup"><span data-stu-id="f2483-160">If you want to deploy to a slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="f2483-161">Salve o projeto e compile-o.</span><span class="sxs-lookup"><span data-stu-id="f2483-161">Save the project and build it.</span></span> <span data-ttu-id="f2483-162">Seu aplicativo Web será implantado no Azure quando o build for concluído.</span><span class="sxs-lookup"><span data-stu-id="f2483-162">Your web app is deployed to Azure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="f2483-163">Implantar o aplicativo Web via FTP usando o pipeline do Jenkins</span><span class="sxs-lookup"><span data-stu-id="f2483-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="f2483-164">O plug-in está preparado para o pipeline.</span><span class="sxs-lookup"><span data-stu-id="f2483-164">The plugin is pipeline-ready.</span></span> <span data-ttu-id="f2483-165">Você pode se referir a uma amostra no repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="f2483-165">You can refer to a sample in the GitHub repo.</span></span>

1. <span data-ttu-id="f2483-166">Na interface do usuário da Web do GitHub, abra o arquivo **Jenkinsfile_ftp_plugin**.</span><span class="sxs-lookup"><span data-stu-id="f2483-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="f2483-167">Clique no ícone de lápis para editar esse arquivo para atualizar o grupo de recursos e o nome do seu aplicativo Web nas linhas 11 e 12, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="f2483-167">Click the pencil icon to edit this file to update the resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="f2483-168">Altere a linha 14 para atualizar a ID de credencial na sua instância do Jenkins.</span><span class="sxs-lookup"><span data-stu-id="f2483-168">Change line 14 to update credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="f2483-169">Crie um pipeline do Jenkins</span><span class="sxs-lookup"><span data-stu-id="f2483-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="f2483-170">Abra o Jenkins em um navegador da Web, clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="f2483-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="f2483-171">Dê um nome para o trabalho e selecione **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="f2483-171">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="f2483-172">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f2483-172">Click **OK**.</span></span>
3. <span data-ttu-id="f2483-173">Clique na próxima guia **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="f2483-173">Click the **Pipeline** tab next.</span></span>
4. <span data-ttu-id="f2483-174">Para **Definição**, selecione **Script de pipeline do SCM**.</span><span class="sxs-lookup"><span data-stu-id="f2483-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="f2483-175">Para **SCM**, selecione **Git**.</span><span class="sxs-lookup"><span data-stu-id="f2483-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="f2483-176">Insira a URL do GitHub em seu repositório bifurcado: https:&lt;seu repositório bifurcado>.git</span><span class="sxs-lookup"><span data-stu-id="f2483-176">Enter the GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="f2483-177">Atualize o **Caminho de Script** para "Jenkinsfile_ftp_plugin"</span><span class="sxs-lookup"><span data-stu-id="f2483-177">Update **Script Path** to "Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="f2483-178">Clique em **Salvar** e execute o trabalho.</span><span class="sxs-lookup"><span data-stu-id="f2483-178">Click **Save** and run the job.</span></span>

## <a name="configure-jenkins-to-deploy-web-app-on-linux-through-docker"></a><span data-ttu-id="f2483-179">Configurar o Jenkins para implantar o Aplicativo Web no Linux por meio do Docker</span><span class="sxs-lookup"><span data-stu-id="f2483-179">Configure Jenkins to deploy Web App on Linux through Docker</span></span>

<span data-ttu-id="f2483-180">Além de Git/FTP, o aplicativo Web no Linux dá suporte à implantação usando o Docker.</span><span class="sxs-lookup"><span data-stu-id="f2483-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="f2483-181">Para implantar usando o Docker, você precisa fornecer um Dockerfile que empacote seu aplicativo Web com tempo de execução do serviço em uma imagem do Docker.</span><span class="sxs-lookup"><span data-stu-id="f2483-181">To deploy using Docker, you need to provide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="f2483-182">O plug-in então compila a imagem, envia-a por push a um registro de Docker e a implanta em seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="f2483-182">Then the plugin builds the image, pushes it to a docker registry and deploys the image to your web app.</span></span>

<span data-ttu-id="f2483-183">O aplicativo Web no Linux também dá suporte a modos tradicionais, como Git e FTP, mas somente para linguagens internas (.NET Core, Node.js, PHP e Ruby).</span><span class="sxs-lookup"><span data-stu-id="f2483-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="f2483-184">Para outras linguagens, você precisa empacotar o código do aplicativo e tempo de execução do serviço juntos em uma imagem do Docker e usar o Docker para implantar.</span><span class="sxs-lookup"><span data-stu-id="f2483-184">For other languages, you need to package your application code and service runtime together into a docker image and use docker to deploy.</span></span>

<span data-ttu-id="f2483-185">Antes de configurar o trabalho no Jenkins, você precisa de um Serviço de Aplicativo do Azure no Linux.</span><span class="sxs-lookup"><span data-stu-id="f2483-185">Before setting up the job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="f2483-186">Um registro de contêiner também é necessário para armazenar e gerenciar suas imagens privadas de contêiner Docker.</span><span class="sxs-lookup"><span data-stu-id="f2483-186">A container registry is also needed to store and manage your private Docker container images.</span></span> <span data-ttu-id="f2483-187">Você pode usar o DockerHub; estamos usando o Registro de Contêiner do Azure para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="f2483-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="f2483-188">Você pode seguir as etapas [aqui](/azure/app-service-web/app-service-linux-how-to-create-web-app) para criar um aplicativo Web no Linux</span><span class="sxs-lookup"><span data-stu-id="f2483-188">You can follow the steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) to create a Web App on Linux</span></span> 
* <span data-ttu-id="f2483-189">O Registro de Contêiner do Azure é um serviço gerenciado de [registro do Docker] (https://docs.docker.com/registry/) com base no software livre Docker Registry 2.0.</span><span class="sxs-lookup"><span data-stu-id="f2483-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on the open-source Docker Registry 2.0.</span></span> <span data-ttu-id="f2483-190">Siga as etapas [aqui] (/azure/container-registry/container-registry-get-started-azure-cli) para mais diretrizes sobre como fazer isso.</span><span class="sxs-lookup"><span data-stu-id="f2483-190">Follow the steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how to do so.</span></span> <span data-ttu-id="f2483-191">Você também pode usar o DockerHub.</span><span class="sxs-lookup"><span data-stu-id="f2483-191">You can also use DockerHub.</span></span>

### <a name="to-deploy-using-docker"></a><span data-ttu-id="f2483-192">Para implantar usando o docker:</span><span class="sxs-lookup"><span data-stu-id="f2483-192">To deploy using docker:</span></span>

1. <span data-ttu-id="f2483-193">Crie um novo projeto de estilo livre no painel do Jenkins.</span><span class="sxs-lookup"><span data-stu-id="f2483-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="f2483-194">Configure o **Gerenciamento de Código-fonte** para usar o seu fork local de [Aplicativo Web Java simples para o Azure](https://github.com/azure-devops/javawebappsample), fornecendo a **URL do Repositório**.</span><span class="sxs-lookup"><span data-stu-id="f2483-194">Configure **Source Code Management** to use your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing the **Repository URL**.</span></span> <span data-ttu-id="f2483-195">Por exemplo: http://github.com/&lt;yourid>/aplicativowebjavadeexemplo.</span><span class="sxs-lookup"><span data-stu-id="f2483-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="f2483-196">Adicione uma etapa de build para compilar o projeto usando o Maven.</span><span class="sxs-lookup"><span data-stu-id="f2483-196">Add a Build step to build the project using Maven.</span></span> <span data-ttu-id="f2483-197">Faça isso adicionando um **Executar shell** e adicione a seguinte linha no **Comando**:</span><span class="sxs-lookup"><span data-stu-id="f2483-197">Do so by adding an **Execute shell** and add the following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="f2483-198">Adicione uma ação pós-build selecionando **Publicar um Aplicativo Web do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f2483-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="f2483-199">Forneça **mySp**, a entidade de serviço do Azure armazenada na etapa anterior como Credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2483-199">Supply, **mySp**, the Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="f2483-200">Em **Configuração do Aplicativo**, escolha o aplicativo Web do Linux e o grupo de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="f2483-200">In **App Configuration** section, choose the resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="f2483-201">Escolha Publicar por meio do Docker.</span><span class="sxs-lookup"><span data-stu-id="f2483-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="f2483-202">Preencha o caminho de **Dockerfile**.</span><span class="sxs-lookup"><span data-stu-id="f2483-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="f2483-203">Você pode manter o "/Dockerfile" padrão para a **URL de Registro do Docker**, forneça-a no formato https://&lt;myRegistry>.azurecr.io se você usar o Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2483-203">You can keep the default "/Dockerfile" For **Docker registry URL**, supply in the format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="f2483-204">Deixe-a em branco se você usar o DockerHub.</span><span class="sxs-lookup"><span data-stu-id="f2483-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="f2483-205">Para **Credenciais de registro**, adicione a credencial para o Registro de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2483-205">For **Registry credentials**, add the credential for the Azure Container Registry.</span></span> <span data-ttu-id="f2483-206">Você pode obter a ID de usuário e senha executando os comandos a seguir na CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2483-206">You can get the userid and password by running the following commands in Azure CLI.</span></span> <span data-ttu-id="f2483-207">O primeiro comando habilita a conta administrador.</span><span class="sxs-lookup"><span data-stu-id="f2483-207">The first command enables the administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="f2483-208">O nome da imagem do docker e a marca na guia **Avançado** são opcionais.</span><span class="sxs-lookup"><span data-stu-id="f2483-208">The docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="f2483-209">Por padrão, o nome da imagem é obtido do nome da imagem que você configurou no Portal do Azure (na configuração do Contêiner do Docker). A marca é gerada de $BUILD_NUMBER.</span><span class="sxs-lookup"><span data-stu-id="f2483-209">By default, image name is obtained from the image name you configured in Azure portal (in Docker Container setting.) The tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="f2483-210">Verifique se você especificou o nome da imagem em um Portal do Azure ou forneça um valor para **Imagem do Docker** na guia **Avançado**. Neste exemplo, forneça "&lt;yourRegistry>.azurecr.io/calculator" para a **Imagem do Docker** e deixe a **Marca da Imagem do Docker** em branco.</span><span class="sxs-lookup"><span data-stu-id="f2483-210">Make sure you specify the image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="f2483-211">Observe que a implantação falhará se você usar uma configuração de imagem do Docker interna.</span><span class="sxs-lookup"><span data-stu-id="f2483-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="f2483-212">Verifique se que você alterou a configuração do Docker para usar a imagem personalizada na configuração Contêiner do Docker no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2483-212">Make sure you change docker config to use custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="f2483-213">Para a imagem interna, use a abordagem de upload de arquivo para implantar.</span><span class="sxs-lookup"><span data-stu-id="f2483-213">For built-in image, use file upload approach to deploy.</span></span>
11. <span data-ttu-id="f2483-214">Semelhante à abordagem de upload de arquivo, você pode escolher um slot diferente que não seja de produção.</span><span class="sxs-lookup"><span data-stu-id="f2483-214">Similar to file upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="f2483-215">Salve e compile o projeto.</span><span class="sxs-lookup"><span data-stu-id="f2483-215">Save and build the project.</span></span> <span data-ttu-id="f2483-216">Você verá que sua imagem de contêiner é enviada por push para o Registro e o aplicativo Web é implantado.</span><span class="sxs-lookup"><span data-stu-id="f2483-216">You see your container image is pushed to your registry and web app is deployed.</span></span>

### <a name="deploy-to-web-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="f2483-217">Implante o aplicativo Web no Linux por meio do Docker usando o pipeline do Jenkins</span><span class="sxs-lookup"><span data-stu-id="f2483-217">Deploy to Web App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="f2483-218">Na interface do usuário da Web do GitHub, abra o arquivo **Jenkinsfile_container_plugin**.</span><span class="sxs-lookup"><span data-stu-id="f2483-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="f2483-219">Clique no ícone de lápis para editar esse arquivo para atualizar o grupo de recursos e o nome do seu aplicativo Web nas linhas 11 e 12, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="f2483-219">Click the pencil icon to edit this file to update the resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="f2483-220">Altere a linha 13 para o servidor de registro de contêiner</span><span class="sxs-lookup"><span data-stu-id="f2483-220">Change line 13 to your container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="f2483-221">Altere a linha 16 para atualizar a ID de credencial na instância do Jenkins</span><span class="sxs-lookup"><span data-stu-id="f2483-221">Change line 16 to update credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="f2483-222">Criar pipeline do Jenkins</span><span class="sxs-lookup"><span data-stu-id="f2483-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="f2483-223">Abra o Jenkins em um navegador da Web, clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="f2483-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="f2483-224">Dê um nome para o trabalho e selecione **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="f2483-224">Provide a name for the job and select **Pipeline**.</span></span> <span data-ttu-id="f2483-225">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f2483-225">Click **OK**.</span></span>
3. <span data-ttu-id="f2483-226">Clique na próxima guia **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="f2483-226">Click the **Pipeline** tab next.</span></span>
4. <span data-ttu-id="f2483-227">Para **Definição**, selecione **Script de pipeline do SCM**.</span><span class="sxs-lookup"><span data-stu-id="f2483-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="f2483-228">Para **SCM**, selecione **Git**.</span><span class="sxs-lookup"><span data-stu-id="f2483-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="f2483-229">Insira a URL do GitHub em seu repositório bifurcado: https:&lt;seu repositório bifurcado>.git</span><span class="sxs-lookup"><span data-stu-id="f2483-229">Enter the GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="f2483-230">7, Atualize o **Caminho de Script** para "Jenkinsfile_container_plugin"</span><span class="sxs-lookup"><span data-stu-id="f2483-230">7, Update **Script Path** to "Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="f2483-231">Clique em **Salvar** e execute o trabalho.</span><span class="sxs-lookup"><span data-stu-id="f2483-231">Click **Save** and run the job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="f2483-232">Verifique seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="f2483-232">Verify your web app</span></span>

1. <span data-ttu-id="f2483-233">Para verificar se o arquivo WAR foi implantado com êxito em seu aplicativo Web,</span><span class="sxs-lookup"><span data-stu-id="f2483-233">To verify the WAR file is deployed successfully to your web app.</span></span> <span data-ttu-id="f2483-234">Abra um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="f2483-234">Open a web browser.</span></span>
2. <span data-ttu-id="f2483-235">Acesse http://&lt;nome_do-aplicativo>.azurewebsites.net/api/calculator/ping Você verá:</span><span class="sxs-lookup"><span data-stu-id="f2483-235">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="f2483-236">Bem-vindo ao aplicativo Web Java!!!</span><span class="sxs-lookup"><span data-stu-id="f2483-236">Welcome to Java Web App!!!</span></span> <span data-ttu-id="f2483-237">Ele está atualizado!</span><span class="sxs-lookup"><span data-stu-id="f2483-237">This is updated!</span></span>
   <span data-ttu-id="f2483-238">Domingo, 17 de junho de 2017, 16:39:10 UTC</span><span class="sxs-lookup"><span data-stu-id="f2483-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="f2483-239">Acesse http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitua &lt;x > e &lt;y > por qualquer número) para obter a soma de x e y</span><span class="sxs-lookup"><span data-stu-id="f2483-239">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>        
    ![Calculadora: adicionar](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="f2483-241">Para o Serviço de Aplicativo no Linux</span><span class="sxs-lookup"><span data-stu-id="f2483-241">For App service on Linux</span></span>

* <span data-ttu-id="f2483-242">Para verificar, na CLI do Azure, execute:</span><span class="sxs-lookup"><span data-stu-id="f2483-242">To verify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="f2483-243">Você obterá o seguinte resultado:</span><span class="sxs-lookup"><span data-stu-id="f2483-243">You get the following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="f2483-244">Acesse http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="f2483-244">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="f2483-245">Você verá a mensagem:</span><span class="sxs-lookup"><span data-stu-id="f2483-245">You see the message:</span></span> 
    
        Welcome to Java Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="f2483-246">Acesse http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitua &lt;x > e &lt;y > por qualquer número) para obter a soma de x e y</span><span class="sxs-lookup"><span data-stu-id="f2483-246">Go to http://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) to get the sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="f2483-247">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f2483-247">Next steps</span></span>

<span data-ttu-id="f2483-248">Neste tutorial, você pode usar o plug-in do Serviço de Aplicativo do Azure para implantar no Azure.</span><span class="sxs-lookup"><span data-stu-id="f2483-248">In this tutorial, you use the Azure App Service plugin to deploy to Azure.</span></span>

<span data-ttu-id="f2483-249">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="f2483-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f2483-250">Configurar Jenkins para implantar o Serviço de Aplicativo do Azure via FTP</span><span class="sxs-lookup"><span data-stu-id="f2483-250">Configure Jenkins to deploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="f2483-251">Configurar o Jenkins para implantar o Serviço de Aplicativo do Azure em Linux por meio do Docker</span><span class="sxs-lookup"><span data-stu-id="f2483-251">Configure Jenkins to deploy to Azure App Service on Linux through Docker</span></span> 