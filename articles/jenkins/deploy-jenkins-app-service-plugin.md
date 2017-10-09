---
title: "aaaDeploy tooAzure do serviço de aplicativo com Jenkins Plugin | Microsoft Docs"
description: "Saiba como toouse Jenkins de serviço de aplicativo do Azure plug-in toodeploy um Java web tooAzure de aplicativo em Jenkins"
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
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a><span data-ttu-id="607d4-103">Implantar tooAzure do serviço de aplicativo com Jenkins plug-in</span><span class="sxs-lookup"><span data-stu-id="607d4-103">Deploy tooAzure App Service with Jenkins plugin</span></span> 
<span data-ttu-id="607d4-104">toodeploy um tooAzure de aplicativo web Java, você pode usar a CLI do Azure em [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) ou você pode fazer uso de saudação [Jenkins de serviço de aplicativo do Azure plug-in](https://plugins.jenkins.io/azure-app-service).</span><span class="sxs-lookup"><span data-stu-id="607d4-104">toodeploy a Java web app tooAzure, you can use Azure CLI in [Jenkins Pipeline](/azure/jenkins/execute-cli-jenkins-pipeline) or you can make use of hello [Azure App Service Jenkins plugin](https://plugins.jenkins.io/azure-app-service).</span></span> <span data-ttu-id="607d4-105">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="607d4-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="607d4-106">Configurar Jenkins toodeploy tooAzure do serviço de aplicativo por meio de FTP</span><span class="sxs-lookup"><span data-stu-id="607d4-106">Configure Jenkins toodeploy tooAzure App Service through FTP</span></span> 
> * <span data-ttu-id="607d4-107">Configurar Jenkins toodeploy tooAzure do serviço de aplicativo no Linux por meio do Docker</span><span class="sxs-lookup"><span data-stu-id="607d4-107">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 

## <a name="create-and-configure-jenkins-instance"></a><span data-ttu-id="607d4-108">Criar e configurar uma instância do Jenkins</span><span class="sxs-lookup"><span data-stu-id="607d4-108">Create and Configure Jenkins instance</span></span>
<span data-ttu-id="607d4-109">Se você ainda não tiver um mestre Jenkins, comece com hello [solução modelo](install-jenkins-solution-template.md), que inclui JDK8 e hello plug-ins necessários a seguir:</span><span class="sxs-lookup"><span data-stu-id="607d4-109">If you do not already have a Jenkins master, start with hello [Solution Template](install-jenkins-solution-template.md), which includes JDK8 and hello following required plugins:</span></span>

* <span data-ttu-id="607d4-110">[Plug-in de cliente Git do Jenkins](https://plugins.jenkins.io/git-client) v.2.4.6</span><span class="sxs-lookup"><span data-stu-id="607d4-110">[Jenkins Git client plugin](https://plugins.jenkins.io/git-client) v.2.4.6</span></span> 
* <span data-ttu-id="607d4-111">[Plug-in Docker Commons](https://plugins.jenkins.io/docker-commons) v.1.4.0</span><span class="sxs-lookup"><span data-stu-id="607d4-111">[Docker Commons Plugin](https://plugins.jenkins.io/docker-commons) v.1.4.0</span></span>
* <span data-ttu-id="607d4-112">[Credenciais do Azure](https://plugins.jenkins.io/azure-credentials) v.1.2</span><span class="sxs-lookup"><span data-stu-id="607d4-112">[Azure Credentials](https://plugins.jenkins.io/azure-credentials) v.1.2</span></span>
* <span data-ttu-id="607d4-113">[Serviço de Aplicativo do Azure](https://plugins.jenkins.io/azure-app-server) v.0.1</span><span class="sxs-lookup"><span data-stu-id="607d4-113">[Azure App Service](https://plugins.jenkins.io/azure-app-server) v.0.1</span></span>

<span data-ttu-id="607d4-114">Você pode usar o hello toodeploy aplicativo Web do plug-in do serviço de aplicativo em todos os idiomas (por exemplo, c#, PHP, Java e node.js, etc.) tem suportada pelo serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="607d4-114">You can use hello App Service plugin toodeploy Web App in all languages (for instance, C#, PHP, Java, and node.js etc.) supported by Azure App Service.</span></span> <span data-ttu-id="607d4-115">Neste tutorial, estamos usando Olá amostra de aplicativo Java, [simples aplicativo de Web de Java para o Azure](https://github.com/azure-devops/javawebappsample).</span><span class="sxs-lookup"><span data-stu-id="607d4-115">In this tutorial, we are using hello sample Java app, [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample).</span></span> <span data-ttu-id="607d4-116">toofork Olá repositório tooyour possui a conta do GitHub, clique em Olá **bifurcação** botão no canto direito superior de saudação.</span><span class="sxs-lookup"><span data-stu-id="607d4-116">toofork hello repo tooyour own GitHub account, click hello **Fork** button in hello top right-hand corner.</span></span>  

<span data-ttu-id="607d4-117">JDK de Java e Maven são necessários para compilar o projeto de Java hello.</span><span class="sxs-lookup"><span data-stu-id="607d4-117">Java JDK and Maven are required for building hello Java project.</span></span> <span data-ttu-id="607d4-118">Verifique se que você instalar componentes de saudação em mestre do hello Jenkins ou agente de VM Olá se você usar uma para a integração contínua.</span><span class="sxs-lookup"><span data-stu-id="607d4-118">Make sure you install hello components in hello Jenkins master or hello VM agent if you use one for continuous integration.</span></span> 

<span data-ttu-id="607d4-119">tooinstall, faça logon em toohello Jenkins instância usando o SSH e execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="607d4-119">tooinstall, log in toohello Jenkins instance using SSH and run hello following commands:</span></span>

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

<span data-ttu-id="607d4-120">Para implantar tooApp serviço no Linux, você também precisa tooinstall Docker no mestre de Jenkins de saudação ou agente de VM Olá usado para compilação.</span><span class="sxs-lookup"><span data-stu-id="607d4-120">For deploying tooApp Service on Linux, you also need tooinstall Docker on hello Jenkins master or hello VM agent used for build.</span></span> <span data-ttu-id="607d4-121">Consulte o artigo de toothis tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span><span class="sxs-lookup"><span data-stu-id="607d4-121">Refer toothis article tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.</span></span>

## <a name="add-azure-service-principal-toojenkins-credential"></a><span data-ttu-id="607d4-122">Adicionar a credencial de tooJenkins principal de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="607d4-122">Add Azure service principal tooJenkins credential</span></span>

<span data-ttu-id="607d4-123">Uma entidade de serviço do Azure é necessário toodeploy tooAzure.</span><span class="sxs-lookup"><span data-stu-id="607d4-123">An Azure service principal is needed toodeploy tooAzure.</span></span> 

<ol>
<li><span data-ttu-id="607d4-124">Use [CLI do Azure](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) ou [portal do Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate uma entidade de serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="607d4-124">Use [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) or [Azure portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate an Azure service principal</span></span></li>
<li><span data-ttu-id="607d4-125">No painel do Jenkins hello, clique em **credenciais -> sistema ->**.</span><span class="sxs-lookup"><span data-stu-id="607d4-125">Within hello Jenkins dashboard, click **Credentials -> System ->**.</span></span> <span data-ttu-id="607d4-126">Clique em **Credenciais globais (irrestrito)**.</span><span class="sxs-lookup"><span data-stu-id="607d4-126">Click **Global credentials(unrestricted)**.</span></span></li>
<li><span data-ttu-id="607d4-127">Clique em **adicionar credenciais** tooadd uma entidade de serviço do Microsoft Azure preenchendo Olá ID da assinatura, ID do cliente, o segredo de cliente e ponto de extremidade Token OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="607d4-127">Click **Add Credentials** tooadd a Microsoft Azure service principal by filling out hello Subscription ID, Client ID, Client Secret, and OAuth 2.0 Token Endpoint.</span></span> <span data-ttu-id="607d4-128">Forneça uma ID, **mySp**, para uso na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="607d4-128">Provide an ID, **mySp**, for use in subsequent steps.</span></span></li>
</ol>

## <a name="azure-app-service-plugin"></a><span data-ttu-id="607d4-129">Plug-in do Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="607d4-129">Azure App Service plugin</span></span>

<span data-ttu-id="607d4-130">V 1.0 plug-in de serviço de aplicativo do Azure oferece suporte à implantação contínua tooAzure aplicativo Web por meio de:</span><span class="sxs-lookup"><span data-stu-id="607d4-130">Azure App Service plugin v1.0 supports continuous deployment tooAzure Web App through:</span></span>

* <span data-ttu-id="607d4-131">Git e FTP</span><span class="sxs-lookup"><span data-stu-id="607d4-131">Git and FTP</span></span>
* <span data-ttu-id="607d4-132">Docker para Aplicativo Web no Linux</span><span class="sxs-lookup"><span data-stu-id="607d4-132">Docker for Web App on Linux</span></span>

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a><span data-ttu-id="607d4-133">Configurar toodeploy Jenkins aplicativo Web por meio de FTP usando Olá Jenkins painel</span><span class="sxs-lookup"><span data-stu-id="607d4-133">Configure Jenkins toodeploy Web App through FTP using hello Jenkins dashboard</span></span>

<span data-ttu-id="607d4-134">toodeploy tooAzure seu project Web App, você pode carregar seus artefatos de compilação (por exemplo, o arquivo. war em Java) usando o Git ou FTP.</span><span class="sxs-lookup"><span data-stu-id="607d4-134">toodeploy your project tooAzure Web App, you can upload your build artifacts (for example, .war file in Java) using Git or FTP.</span></span>

<span data-ttu-id="607d4-135">Antes de configurar o trabalho de saudação em Jenkins, é necessário um plano de serviço de aplicativo do Azure e um aplicativo Web para aplicativo de Java Olá em execução.</span><span class="sxs-lookup"><span data-stu-id="607d4-135">Before setting up hello job in Jenkins, you need an Azure App Service plan and a Web App for running hello Java app.</span></span>


1. <span data-ttu-id="607d4-136">Criar um plano de serviço de aplicativo do Azure com hello **livre** preço usando Olá [criar plano de serviço de aplicativo az](/cli/azure/appservice/plan#create) comando CLI.</span><span class="sxs-lookup"><span data-stu-id="607d4-136">Create an Azure App Service plan with hello **FREE** pricing tier using hello  [az appservice plan create](/cli/azure/appservice/plan#create) CLI command.</span></span> <span data-ttu-id="607d4-137">plano de serviço de aplicativo Hello define Olá recursos físicos usados toohost seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="607d4-137">hello appservice plan defines hello physical resources used toohost your apps.</span></span> <span data-ttu-id="607d4-138">Todos os aplicativos atribuídos plano de serviço de aplicativo tooan compartilham esses recursos, permitindo que você toosave custo ao hospedar vários aplicativos.</span><span class="sxs-lookup"><span data-stu-id="607d4-138">All applications assigned tooan appservice plan share these resources, allowing you toosave cost when hosting multiple apps.</span></span>
2. <span data-ttu-id="607d4-139">Crie um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="607d4-139">Create a Web App.</span></span> <span data-ttu-id="607d4-140">Pode hello ou use [portal do Azure](/azure/app-service-web/web-sites-configure) ou use Olá comando CLI Az a seguir:</span><span class="sxs-lookup"><span data-stu-id="607d4-140">You can either use hello [Azure portal](/azure/app-service-web/web-sites-configure) or use hello following Az CLI command:</span></span>
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. <span data-ttu-id="607d4-141">Certifique-se de que definir a configuração de tempo de execução do Java Olá seu aplicativo precisa.</span><span class="sxs-lookup"><span data-stu-id="607d4-141">Make sure you set up hello Java runtime configuration that your app needs.</span></span> <span data-ttu-id="607d4-142">Olá após o comando CLI do Azure configura Olá web aplicativo toorun em um recente Java 8 JDK e [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span><span class="sxs-lookup"><span data-stu-id="607d4-142">hello following Azure CLI command configures hello web app toorun on a recent Java 8 JDK and [Apache Tomcat](http://tomcat.apache.org/) 8.0.</span></span>
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a><span data-ttu-id="607d4-143">Configurar Olá Jenkins trabalho</span><span class="sxs-lookup"><span data-stu-id="607d4-143">Set up hello Jenkins job</span></span>


1. <span data-ttu-id="607d4-144">Criar um novo projeto de **estilo livre** no painel do Jenkins</span><span class="sxs-lookup"><span data-stu-id="607d4-144">Create a new **freestyle** project in Jenkins Dashboard</span></span>
2. <span data-ttu-id="607d4-145">Configurar **código-fonte gerenciamento** toouse seu local bifurcação de [simples aplicativo de Web de Java para o Azure](https://github.com/azure-devops/javawebappsample) fornecendo Olá **URL do repositório**.</span><span class="sxs-lookup"><span data-stu-id="607d4-145">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="607d4-146">Por exemplo: http://github.com/&lt;yourID>/aplicativowebjavadeexemplo.</span><span class="sxs-lookup"><span data-stu-id="607d4-146">For example: http://github.com/&lt;yourID>/javawebappsample.</span></span>
3. <span data-ttu-id="607d4-147">Adicione um projeto de saudação do Build etapa toobuild usando Maven.</span><span class="sxs-lookup"><span data-stu-id="607d4-147">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="607d4-148">Faça isso adicionando um **Executar shell**.</span><span class="sxs-lookup"><span data-stu-id="607d4-148">Do so by adding an **Execute shell**.</span></span> <span data-ttu-id="607d4-149">Neste exemplo, podemos precisará de um arquivo de *.war do etapa adicional toorename Olá no tooROOT.war da pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="607d4-149">For this example, we need an additional step toorename hello *.war file in target folder tooROOT.war.</span></span>   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. <span data-ttu-id="607d4-150">Adicione uma ação pós-build selecionando **Publicar um Aplicativo Web do Azure**.</span><span class="sxs-lookup"><span data-stu-id="607d4-150">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
5. <span data-ttu-id="607d4-151">Fonte, "mySp", entidade de serviço do Azure Olá armazenados na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="607d4-151">Supply, "mySp", hello Azure service principal stored in previous step.</span></span>
6. <span data-ttu-id="607d4-152">Em **configuração do aplicativo** , escolha Olá recurso grupo e o aplicativo web em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="607d4-152">In **App Configuration** section, choose hello resource group and web app in your subscription.</span></span> <span data-ttu-id="607d4-153">plug-in de saudação detecta automaticamente se Olá Web App for Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="607d4-153">hello plugin automatically detects whether hello Web App is Windows or Linux-based.</span></span> <span data-ttu-id="607d4-154">Para um aplicativo Web baseado em Windows, é apresentada a opção hello "Publicar os arquivos".</span><span class="sxs-lookup"><span data-stu-id="607d4-154">For a Windows-based Web App, hello option "Publish Files" is presented.</span></span>
7. <span data-ttu-id="607d4-155">Preenchimento nos arquivos de saudação desejado toodeploy (por exemplo, um pacote war se você estiver usando o Java.) O Diretório de Origem e o Diretório de Destino são opcionais.</span><span class="sxs-lookup"><span data-stu-id="607d4-155">Fill in hello files you want toodeploy (for example, a war package if you're using Java.) Source Directory and Target Directory are optional.</span></span> <span data-ttu-id="607d4-156">Olá parâmetros permitem toospecify pastas de origem e de destino quando o carregamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="607d4-156">hello parameters allow you toospecify source and target folders when uploading files.</span></span> <span data-ttu-id="607d4-157">O aplicativo Web Java no Azure é executado em um servidor Tomcat.</span><span class="sxs-lookup"><span data-stu-id="607d4-157">Java web app on Azure is run in a Tomcat server.</span></span> <span data-ttu-id="607d4-158">Desse modo, você carrega o pacote war para a pasta webapps.</span><span class="sxs-lookup"><span data-stu-id="607d4-158">So you upload you war package to webapps folder.</span></span> <span data-ttu-id="607d4-159">Neste exemplo, defina **diretório de origem** muito "destino" e fornecer "webapps" de **diretório de destino**.</span><span class="sxs-lookup"><span data-stu-id="607d4-159">For this example, set **Source Directory** too"target" and supply "webapps" for **Target Directory**.</span></span>
8. <span data-ttu-id="607d4-160">Se você quiser toodeploy tooa slot que não seja de produção, você também pode definir **Slot** nome.</span><span class="sxs-lookup"><span data-stu-id="607d4-160">If you want toodeploy tooa slot other than production, you can also set **Slot** Name.</span></span>
9. <span data-ttu-id="607d4-161">Salve o projeto hello e compilá-lo.</span><span class="sxs-lookup"><span data-stu-id="607d4-161">Save hello project and build it.</span></span> <span data-ttu-id="607d4-162">Seu aplicativo web é implantado tooAzure quando a compilação for concluída.</span><span class="sxs-lookup"><span data-stu-id="607d4-162">Your web app is deployed tooAzure when build is complete.</span></span>

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a><span data-ttu-id="607d4-163">Implantar o aplicativo Web via FTP usando o pipeline do Jenkins</span><span class="sxs-lookup"><span data-stu-id="607d4-163">Deploy Web App through FTP using Jenkins pipeline</span></span>

<span data-ttu-id="607d4-164">Olá plug-in está preparado para o pipeline.</span><span class="sxs-lookup"><span data-stu-id="607d4-164">hello plugin is pipeline-ready.</span></span> <span data-ttu-id="607d4-165">Você pode consultar o exemplo tooa no repositório do GitHub hello.</span><span class="sxs-lookup"><span data-stu-id="607d4-165">You can refer tooa sample in hello GitHub repo.</span></span>

1. <span data-ttu-id="607d4-166">Na interface do usuário da Web do GitHub, abra o arquivo **Jenkinsfile_ftp_plugin**.</span><span class="sxs-lookup"><span data-stu-id="607d4-166">In GitHub web UI, open **Jenkinsfile_ftp_plugin** file.</span></span> <span data-ttu-id="607d4-167">Clique em tooedit de ícone de lápis Olá este grupo de recursos do arquivo tooupdate hello e o nome do seu aplicativo web na linha 11 e 12 respectivamente.</span><span class="sxs-lookup"><span data-stu-id="607d4-167">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="607d4-168">Alterar a identificação da credencial tooupdate 14 linha em sua instância Jenkins.</span><span class="sxs-lookup"><span data-stu-id="607d4-168">Change line 14 tooupdate credential ID in your Jenkins instance.</span></span>    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a><span data-ttu-id="607d4-169">Crie um pipeline do Jenkins</span><span class="sxs-lookup"><span data-stu-id="607d4-169">Create a Jenkins pipeline</span></span>

1. <span data-ttu-id="607d4-170">Abra o Jenkins em um navegador da Web, clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="607d4-170">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="607d4-171">Forneça um nome para o trabalho de saudação e selecione **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="607d4-171">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="607d4-172">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="607d4-172">Click **OK**.</span></span>
3. <span data-ttu-id="607d4-173">Clique em Olá **Pipeline** próxima guia.</span><span class="sxs-lookup"><span data-stu-id="607d4-173">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="607d4-174">Para **Definição**, selecione **Script de pipeline do SCM**.</span><span class="sxs-lookup"><span data-stu-id="607d4-174">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="607d4-175">Para **SCM**, selecione **Git**.</span><span class="sxs-lookup"><span data-stu-id="607d4-175">For **SCM**, select **Git**.</span></span> <span data-ttu-id="607d4-176">Digite hello GitHub URL para seu repositório bifurcado: https:&lt;seu repositório bifurcado > .git</span><span class="sxs-lookup"><span data-stu-id="607d4-176">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span>
6. <span data-ttu-id="607d4-177">Atualização **caminho de Script** muito "Jenkinsfile_ftp_plugin"</span><span class="sxs-lookup"><span data-stu-id="607d4-177">Update **Script Path** too"Jenkinsfile_ftp_plugin"</span></span>
7. <span data-ttu-id="607d4-178">Clique em **salvar** e trabalho de execução hello.</span><span class="sxs-lookup"><span data-stu-id="607d4-178">Click **Save** and run hello job.</span></span>

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a><span data-ttu-id="607d4-179">Configurar toodeploy Jenkins aplicativo Web no Linux por meio do Docker</span><span class="sxs-lookup"><span data-stu-id="607d4-179">Configure Jenkins toodeploy Web App on Linux through Docker</span></span>

<span data-ttu-id="607d4-180">Além de Git/FTP, o aplicativo Web no Linux dá suporte à implantação usando o Docker.</span><span class="sxs-lookup"><span data-stu-id="607d4-180">Apart from Git/FTP, Web App on Linux supports deployment using Docker.</span></span> <span data-ttu-id="607d4-181">toodeploy usando o Docker, você precisa tooprovide um Dockerfile que os pacotes de aplicativos web com o tempo de execução do serviço em uma imagem do docker.</span><span class="sxs-lookup"><span data-stu-id="607d4-181">toodeploy using Docker, you need tooprovide a Dockerfile that packages your web app with service runtime into a docker image.</span></span> <span data-ttu-id="607d4-182">Em seguida, Olá plug-in compila imagem hello, envia-registro de docker tooa e implanta o aplicativo web do hello imagem tooyour.</span><span class="sxs-lookup"><span data-stu-id="607d4-182">Then hello plugin builds hello image, pushes it tooa docker registry and deploys hello image tooyour web app.</span></span>

<span data-ttu-id="607d4-183">O aplicativo Web no Linux também dá suporte a modos tradicionais, como Git e FTP, mas somente para linguagens internas (.NET Core, Node.js, PHP e Ruby).</span><span class="sxs-lookup"><span data-stu-id="607d4-183">Web App on Linux also supports traditional ways like Git and FTP, but only for built-in languages (.NET Core, Node.js, PHP, and Ruby).</span></span> <span data-ttu-id="607d4-184">Para outros idiomas, você precisa de toopackage o tempo de execução de código e o serviço de aplicativo juntos em uma imagem do docker e usar toodeploy docker.</span><span class="sxs-lookup"><span data-stu-id="607d4-184">For other languages, you need toopackage your application code and service runtime together into a docker image and use docker toodeploy.</span></span>

<span data-ttu-id="607d4-185">Antes de configurar o trabalho de saudação em Jenkins, você precisa de um serviço de aplicativo do Azure em Linux.</span><span class="sxs-lookup"><span data-stu-id="607d4-185">Before setting up hello job in Jenkins, you need an Azure app service on Linux.</span></span> <span data-ttu-id="607d4-186">Um registro de contêiner também é necessário toostore e gerenciar suas imagens de contêiner do Docker particulares.</span><span class="sxs-lookup"><span data-stu-id="607d4-186">A container registry is also needed toostore and manage your private Docker container images.</span></span> <span data-ttu-id="607d4-187">Você pode usar o DockerHub; estamos usando o Registro de Contêiner do Azure para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="607d4-187">You can use DockerHub; we are using Azure Container Registry for this example.</span></span>

* <span data-ttu-id="607d4-188">Você pode seguir as etapas de saudação [aqui](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate um aplicativo Web no Linux</span><span class="sxs-lookup"><span data-stu-id="607d4-188">You can follow hello steps [here](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate a Web App on Linux</span></span> 
* <span data-ttu-id="607d4-189">Registro de contêiner do Azure é um gerenciados [Docker registro] serviço (https://docs.docker.com/registry/) com base no hello 2.0 do código-fonte aberto Docker do registro.</span><span class="sxs-lookup"><span data-stu-id="607d4-189">Azure Container Registry is a managed [Docker registry] (https://docs.docker.com/registry/) service based on hello open-source Docker Registry 2.0.</span></span> <span data-ttu-id="607d4-190">Execute as etapas de saudação [aqui] (/ azure/container-registry/container-registry-get-started-azure-cli) para obter instruções sobre como toodo para.</span><span class="sxs-lookup"><span data-stu-id="607d4-190">Follow hello steps [here] (/azure/container-registry/container-registry-get-started-azure-cli) for more guidance on how toodo so.</span></span> <span data-ttu-id="607d4-191">Você também pode usar o DockerHub.</span><span class="sxs-lookup"><span data-stu-id="607d4-191">You can also use DockerHub.</span></span>

### <a name="toodeploy-using-docker"></a><span data-ttu-id="607d4-192">toodeploy usando o docker:</span><span class="sxs-lookup"><span data-stu-id="607d4-192">toodeploy using docker:</span></span>

1. <span data-ttu-id="607d4-193">Crie um novo projeto de estilo livre no painel do Jenkins.</span><span class="sxs-lookup"><span data-stu-id="607d4-193">Create a new freestyle project in Jenkins Dashboard.</span></span>
2. <span data-ttu-id="607d4-194">Configurar **código-fonte gerenciamento** toouse seu local bifurcação de [simples aplicativo de Web de Java para o Azure](https://github.com/azure-devops/javawebappsample) fornecendo Olá **URL do repositório**.</span><span class="sxs-lookup"><span data-stu-id="607d4-194">Configure **Source Code Management** toouse your local fork of [Simple Java Web App for Azure](https://github.com/azure-devops/javawebappsample) by providing hello **Repository URL**.</span></span> <span data-ttu-id="607d4-195">Por exemplo: http://github.com/&lt;yourid>/aplicativowebjavadeexemplo.</span><span class="sxs-lookup"><span data-stu-id="607d4-195">For example: http://github.com/&lt;yourid>/javawebappsample.</span></span>
<span data-ttu-id="607d4-196">Adicione um projeto de saudação do Build etapa toobuild usando Maven.</span><span class="sxs-lookup"><span data-stu-id="607d4-196">Add a Build step toobuild hello project using Maven.</span></span> <span data-ttu-id="607d4-197">Faça isso adicionando um **executar shell** e adicione Olá a seguinte linha no **comando**:</span><span class="sxs-lookup"><span data-stu-id="607d4-197">Do so by adding an **Execute shell** and add hello following line in **Command**:</span></span>    
```bash
mvn clean package
```

3. <span data-ttu-id="607d4-198">Adicione uma ação pós-build selecionando **Publicar um Aplicativo Web do Azure**.</span><span class="sxs-lookup"><span data-stu-id="607d4-198">Add a post-build action by selecting **Publish an Azure Web App**.</span></span>
4. <span data-ttu-id="607d4-199">Fornecer, **mySp**, entidade de serviço do Azure Olá armazenada na etapa anterior como credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="607d4-199">Supply, **mySp**, hello Azure service principal stored in previous step as Azure Credentials.</span></span>
5. <span data-ttu-id="607d4-200">Em **configuração do aplicativo** , escolha o grupo de recursos de saudação e um aplicativo web do Linux em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="607d4-200">In **App Configuration** section, choose hello resource group and a Linux web app in your subscription.</span></span>
6. <span data-ttu-id="607d4-201">Escolha Publicar por meio do Docker.</span><span class="sxs-lookup"><span data-stu-id="607d4-201">Choose Publish via Docker.</span></span>
7. <span data-ttu-id="607d4-202">Preencha o caminho de **Dockerfile**.</span><span class="sxs-lookup"><span data-stu-id="607d4-202">Fill in **Dockerfile** path.</span></span> <span data-ttu-id="607d4-203">Você pode manter saudação padrão "/ Dockerfile" para **URL de registro de Docker**, forneça no formato de saudação do https://&lt;myRegistry >. azurecr.io se você usar o registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="607d4-203">You can keep hello default "/Dockerfile" For **Docker registry URL**, supply in hello format of https://&lt;myRegistry>.azurecr.io if you use Azure Container Registry.</span></span> <span data-ttu-id="607d4-204">Deixe-a em branco se você usar o DockerHub.</span><span class="sxs-lookup"><span data-stu-id="607d4-204">Leave it blank if you use DockerHub.</span></span>
8. <span data-ttu-id="607d4-205">Para **credenciais de registro**, adicione a credencial Olá de saudação do registro de contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="607d4-205">For **Registry credentials**, add hello credential for hello Azure Container Registry.</span></span> <span data-ttu-id="607d4-206">Você pode obter Olá ID de usuário e senha executando Olá seguintes comandos em CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="607d4-206">You can get hello userid and password by running hello following commands in Azure CLI.</span></span> <span data-ttu-id="607d4-207">comando primeiro Olá permite que a conta de administrador de saudação.</span><span class="sxs-lookup"><span data-stu-id="607d4-207">hello first command enables hello administrator account.</span></span>    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. <span data-ttu-id="607d4-208">Olá, nome de imagem do docker e a marca no **avançado** guia são opcionais.</span><span class="sxs-lookup"><span data-stu-id="607d4-208">hello docker image name and tag in **Advanced** tab are optional.</span></span> <span data-ttu-id="607d4-209">Por padrão, o nome da imagem é obtido da imagem Olá nome configurado na marca de saudação portal (no contêiner do Docker configuração.) do Azure é gerado a partir de $ número do_build.</span><span class="sxs-lookup"><span data-stu-id="607d4-209">By default, image name is obtained from hello image name you configured in Azure portal (in Docker Container setting.) hello tag is generated from $BUILD_NUMBER.</span></span> <span data-ttu-id="607d4-210">Verifique se você especifica o nome da imagem Olá no portal do Azure ou fornece um valor para **Docker imagem** na **avançado** guia. Neste exemplo, forneça "&lt;yourRegistry>.azurecr.io/calculator" para a **Imagem do Docker** e deixe a **Marca da Imagem do Docker** em branco.</span><span class="sxs-lookup"><span data-stu-id="607d4-210">Make sure you specify hello image name in either Azure portal or supply a value for **Docker Image** in **Advanced** tab. For this example, supply "&lt;yourRegistry>.azurecr.io/calculator" for **Docker image** and leave **Docker Image Tag** blank.</span></span>
10. <span data-ttu-id="607d4-211">Observe que a implantação falhará se você usar uma configuração de imagem do Docker interna.</span><span class="sxs-lookup"><span data-stu-id="607d4-211">Note deployment fails if you use built-in Docker image setting.</span></span> <span data-ttu-id="607d4-212">Verifique se que você alterar a imagem personalizada do docker config toouse na configuração do contêiner do Docker no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="607d4-212">Make sure you change docker config toouse custom image in Docker Container setting in Azure portal.</span></span> <span data-ttu-id="607d4-213">Para a imagem interna, use toodeploy de abordagem de carregamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="607d4-213">For built-in image, use file upload approach toodeploy.</span></span>
11. <span data-ttu-id="607d4-214">Método de carregamento toofile semelhante, você pode escolher um slot diferente que não seja de produção.</span><span class="sxs-lookup"><span data-stu-id="607d4-214">Similar toofile upload approach, you can choose a different slot other than production.</span></span>
12. <span data-ttu-id="607d4-215">Salve e compile o projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="607d4-215">Save and build hello project.</span></span> <span data-ttu-id="607d4-216">Você verá sua imagem de contêiner é enviada por push do registro de tooyour e aplicativo web é implantado.</span><span class="sxs-lookup"><span data-stu-id="607d4-216">You see your container image is pushed tooyour registry and web app is deployed.</span></span>

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a><span data-ttu-id="607d4-217">Implantar tooWeb aplicativo no Linux por meio do Docker usando o pipeline Jenkins</span><span class="sxs-lookup"><span data-stu-id="607d4-217">Deploy tooWeb App on Linux through Docker using Jenkins pipeline</span></span>

1. <span data-ttu-id="607d4-218">Na interface do usuário da Web do GitHub, abra o arquivo **Jenkinsfile_container_plugin**.</span><span class="sxs-lookup"><span data-stu-id="607d4-218">In GitHub web UI, open **Jenkinsfile_container_plugin** file.</span></span> <span data-ttu-id="607d4-219">Clique em tooedit de ícone de lápis Olá este grupo de recursos do arquivo tooupdate hello e o nome do seu aplicativo web na linha 11 e 12 respectivamente.</span><span class="sxs-lookup"><span data-stu-id="607d4-219">Click hello pencil icon tooedit this file tooupdate hello resource group and name of your web app on line 11 and 12 respectively.</span></span>    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. <span data-ttu-id="607d4-220">Alterar o servidor de registro de contêiner de tooyour 13 de linha</span><span class="sxs-lookup"><span data-stu-id="607d4-220">Change line 13 tooyour container registry server</span></span>    
```java
def registryServer = '<registryURL>'
```    

3. <span data-ttu-id="607d4-221">Alterar a identificação da credencial tooupdate 16 linha em sua instância Jenkins</span><span class="sxs-lookup"><span data-stu-id="607d4-221">Change line 16 tooupdate credential ID in your Jenkins instance</span></span>    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a><span data-ttu-id="607d4-222">Criar pipeline do Jenkins</span><span class="sxs-lookup"><span data-stu-id="607d4-222">Create Jenkins pipeline</span></span>    

1. <span data-ttu-id="607d4-223">Abra o Jenkins em um navegador da Web, clique em **Novo Item**.</span><span class="sxs-lookup"><span data-stu-id="607d4-223">Open Jenkins in a web browser, click **New Item**.</span></span>
2. <span data-ttu-id="607d4-224">Forneça um nome para o trabalho de saudação e selecione **Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="607d4-224">Provide a name for hello job and select **Pipeline**.</span></span> <span data-ttu-id="607d4-225">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="607d4-225">Click **OK**.</span></span>
3. <span data-ttu-id="607d4-226">Clique em Olá **Pipeline** próxima guia.</span><span class="sxs-lookup"><span data-stu-id="607d4-226">Click hello **Pipeline** tab next.</span></span>
4. <span data-ttu-id="607d4-227">Para **Definição**, selecione **Script de pipeline do SCM**.</span><span class="sxs-lookup"><span data-stu-id="607d4-227">For **Definition**, select **Pipeline script from SCM**.</span></span>
5. <span data-ttu-id="607d4-228">Para **SCM**, selecione **Git**.</span><span class="sxs-lookup"><span data-stu-id="607d4-228">For **SCM**, select **Git**.</span></span>
6. <span data-ttu-id="607d4-229">Digite hello GitHub URL para seu repositório bifurcado: https:&lt;seu repositório bifurcado > .git</span><span class="sxs-lookup"><span data-stu-id="607d4-229">Enter hello GitHub URL for your forked repo: https:&lt;your forked repo>.git</span></span></li>
<span data-ttu-id="607d4-230">Atualização 7, **caminho de Script** muito "Jenkinsfile_container_plugin"</span><span class="sxs-lookup"><span data-stu-id="607d4-230">7, Update **Script Path** too"Jenkinsfile_container_plugin"</span></span>
8. <span data-ttu-id="607d4-231">Clique em **salvar** e trabalho de execução hello.</span><span class="sxs-lookup"><span data-stu-id="607d4-231">Click **Save** and run hello job.</span></span>

## <a name="verify-your-web-app"></a><span data-ttu-id="607d4-232">Verifique seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="607d4-232">Verify your web app</span></span>

1. <span data-ttu-id="607d4-233">arquivo do tooverify Olá WAR seja implantado com êxito tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="607d4-233">tooverify hello WAR file is deployed successfully tooyour web app.</span></span> <span data-ttu-id="607d4-234">Abra um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="607d4-234">Open a web browser.</span></span>
2. <span data-ttu-id="607d4-235">Vá toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping você verá:</span><span class="sxs-lookup"><span data-stu-id="607d4-235">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping You see:</span></span>    
     <span data-ttu-id="607d4-236">Bem-vindo tooJava aplicativo Web!!!</span><span class="sxs-lookup"><span data-stu-id="607d4-236">Welcome tooJava Web App!!!</span></span> <span data-ttu-id="607d4-237">Ele está atualizado!</span><span class="sxs-lookup"><span data-stu-id="607d4-237">This is updated!</span></span>
   <span data-ttu-id="607d4-238">Domingo, 17 de junho de 2017, 16:39:10 UTC</span><span class="sxs-lookup"><span data-stu-id="607d4-238">Sun Jun 17 16:39:10 UTC 2017</span></span>
3. <span data-ttu-id="607d4-239">Vá toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (substitua &lt;x > e &lt;y > com os números) tooget soma de saudação de x e y</span><span class="sxs-lookup"><span data-stu-id="607d4-239">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>        
    ![Calculadora: adicionar](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a><span data-ttu-id="607d4-241">Para o Serviço de Aplicativo no Linux</span><span class="sxs-lookup"><span data-stu-id="607d4-241">For App service on Linux</span></span>

* <span data-ttu-id="607d4-242">tooverify, na CLI do Azure, execute:</span><span class="sxs-lookup"><span data-stu-id="607d4-242">tooverify, in Azure CLI, run:</span></span>

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    <span data-ttu-id="607d4-243">Você obtém Olá resultados a seguir:</span><span class="sxs-lookup"><span data-stu-id="607d4-243">You get hello following result:</span></span>
    
    ```
    [
    "calculator"
    ]
    ```
    
    <span data-ttu-id="607d4-244">Vá toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/ping.</span><span class="sxs-lookup"><span data-stu-id="607d4-244">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/ping.</span></span> <span data-ttu-id="607d4-245">Você verá a mensagem de saudação:</span><span class="sxs-lookup"><span data-stu-id="607d4-245">You see hello message:</span></span> 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    <span data-ttu-id="607d4-246">Vá toohttp: / /&lt;app_name >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (substitua &lt;x > e &lt;y > com os números) tooget soma de saudação de x e y</span><span class="sxs-lookup"><span data-stu-id="607d4-246">Go toohttp://&lt;app_name>.azurewebsites.net/api/calculator/add?x=&lt;x>&y=&lt;y> (substitute &lt;x> and &lt;y> with any numbers) tooget hello sum of x and y</span></span>
    
## <a name="next-steps"></a><span data-ttu-id="607d4-247">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="607d4-247">Next steps</span></span>

<span data-ttu-id="607d4-248">Neste tutorial, você deve usar Olá tooAzure de toodeploy de plug-in de serviço de aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="607d4-248">In this tutorial, you use hello Azure App Service plugin toodeploy tooAzure.</span></span>

<span data-ttu-id="607d4-249">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="607d4-249">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="607d4-250">Configurar Jenkins toodeploy do serviço de aplicativo do Azure por meio de FTP</span><span class="sxs-lookup"><span data-stu-id="607d4-250">Configure Jenkins toodeploy Azure App Service through FTP</span></span> 
> * <span data-ttu-id="607d4-251">Configurar Jenkins toodeploy tooAzure do serviço de aplicativo no Linux por meio do Docker</span><span class="sxs-lookup"><span data-stu-id="607d4-251">Configure Jenkins toodeploy tooAzure App Service on Linux through Docker</span></span> 
