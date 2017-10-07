---
title: aaaGet iniciar a pesquisa do Azure em Java | Microsoft Docs
description: "Como a pesquisa de toobuild uma nuvem hospedada aplicativo no Azure usando o Java como sua linguagem de programação."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a><span data-ttu-id="f3390-103">Introdução à Pesquisa do Azure em Java</span><span class="sxs-lookup"><span data-stu-id="f3390-103">Get started with Azure Search in Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3390-104">Portal</span><span class="sxs-lookup"><span data-stu-id="f3390-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="f3390-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f3390-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="f3390-106">Saiba como o aplicativo que usa a pesquisa do Azure para sua experiência de pesquisa de pesquisa toobuild um Java personalizados.</span><span class="sxs-lookup"><span data-stu-id="f3390-106">Learn how toobuild a custom Java search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="f3390-107">Este tutorial usa Olá [API de REST do serviço de pesquisa do Azure](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct Olá objetos e operações usadas neste exercício.</span><span class="sxs-lookup"><span data-stu-id="f3390-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="f3390-108">toorun neste exemplo, você deve ter um serviço de pesquisa do Azure, que pode inscrever-se em Olá [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f3390-108">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="f3390-109">Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="f3390-109">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

<span data-ttu-id="f3390-110">Podemos usado Olá toobuild de software a seguir e testar este exemplo:</span><span class="sxs-lookup"><span data-stu-id="f3390-110">We used hello following software toobuild and test this sample:</span></span>

* <span data-ttu-id="f3390-111">[Eclipse IDE para desenvolvedores de Java EE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span><span class="sxs-lookup"><span data-stu-id="f3390-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span></span> <span data-ttu-id="f3390-112">Ter certeza de que toodownload Olá EE versão.</span><span class="sxs-lookup"><span data-stu-id="f3390-112">Be sure toodownload hello EE version.</span></span> <span data-ttu-id="f3390-113">Uma das etapas de verificação de saudação exige um recurso que se encontra apenas nesta edição.</span><span class="sxs-lookup"><span data-stu-id="f3390-113">One of hello verification steps requires a feature that is found only in this edition.</span></span>
* [<span data-ttu-id="f3390-114">JDK 8u40</span><span class="sxs-lookup"><span data-stu-id="f3390-114">JDK 8u40</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="f3390-115">Apache Tomcat 8.0</span><span class="sxs-lookup"><span data-stu-id="f3390-115">Apache Tomcat 8.0</span></span>](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a><span data-ttu-id="f3390-116">Sobre dados saudação</span><span class="sxs-lookup"><span data-stu-id="f3390-116">About hello data</span></span>
<span data-ttu-id="f3390-117">Este aplicativo de exemplo usa dados da saudação [dos Estados Unidos geológica serviços (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtrado no tamanho do conjunto de dados do hello estado de Rhode Island tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="f3390-117">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="f3390-118">Vamos usar essa toobuild dados um aplicativo de pesquisa que retorna as construções de pontos de referência, como escolas e hospitais, bem como recursos geológica como fluxos, Lagos e Cúpulas.</span><span class="sxs-lookup"><span data-stu-id="f3390-118">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="f3390-119">Neste aplicativo, Olá **SearchServlet.java** programa cria e carrega Olá índice usando um [indexador](https://msdn.microsoft.com/library/azure/dn798918.aspx) construção, recuperando Olá filtrados USGS conjunto de dados de um banco de dados do SQL Azure público.</span><span class="sxs-lookup"><span data-stu-id="f3390-119">In this application, hello **SearchServlet.java** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="f3390-120">Credenciais predefinidas e fonte de dados online de toohello de informações de conexão são fornecidas no código do programa hello.</span><span class="sxs-lookup"><span data-stu-id="f3390-120">Predefined credentials and connection  information toohello online data source are provided in hello program code.</span></span> <span data-ttu-id="f3390-121">Em termos de acesso a dados, nenhuma configuração adicional é necessária.</span><span class="sxs-lookup"><span data-stu-id="f3390-121">In terms of data access, no further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="f3390-122">Aplicamos um filtro em toostay este conjunto de dados abaixo do limite de documento 10.000 Olá de saudação livre de camada de preços.</span><span class="sxs-lookup"><span data-stu-id="f3390-122">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="f3390-123">Se você usar a camada padrão Olá, não se aplicam a esse limite, e você pode modificar este código toouse um conjunto de dados maior.</span><span class="sxs-lookup"><span data-stu-id="f3390-123">If you use hello standard tier, this limit does not apply, and you can modify this code toouse a bigger dataset.</span></span> <span data-ttu-id="f3390-124">Para obter detalhes sobre a capacidade de cada camada de preços, consulte [Limites e restrições](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="f3390-124">For details about capacity for each pricing tier, see [Limits and constraints](search-limits-quotas-capacity.md).</span></span>
> 
> 

## <a name="about-hello-program-files"></a><span data-ttu-id="f3390-125">Sobre arquivos de programa Olá</span><span class="sxs-lookup"><span data-stu-id="f3390-125">About hello program files</span></span>
<span data-ttu-id="f3390-126">Olá lista a seguir descreve os arquivos de saudação que são relevantes toothis exemplo.</span><span class="sxs-lookup"><span data-stu-id="f3390-126">hello following list describes hello files that are relevant toothis sample.</span></span>

* <span data-ttu-id="f3390-127">Search.jsp: Fornece a interface do usuário Olá</span><span class="sxs-lookup"><span data-stu-id="f3390-127">Search.jsp: Provides hello user interface</span></span>
* <span data-ttu-id="f3390-128">SearchServlet.java: Fornece métodos (semelhante tooa controlador MVC)</span><span class="sxs-lookup"><span data-stu-id="f3390-128">SearchServlet.java: Provides methods (similar tooa controller in MVC)</span></span>
* <span data-ttu-id="f3390-129">SearchServiceClient.java: lida com solicitações HTTP</span><span class="sxs-lookup"><span data-stu-id="f3390-129">SearchServiceClient.java: Handles HTTP requests</span></span>
* <span data-ttu-id="f3390-130">SearchServiceHelper.java: uma classe auxiliar que fornece métodos estáticos</span><span class="sxs-lookup"><span data-stu-id="f3390-130">SearchServiceHelper.java: A helper class that provides static methods</span></span>
* <span data-ttu-id="f3390-131">Document.Java: Fornece o modelo de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="f3390-131">Document.java: Provides hello data model</span></span>
* <span data-ttu-id="f3390-132">config: define a URL do serviço de pesquisa de saudação e chave de api</span><span class="sxs-lookup"><span data-stu-id="f3390-132">config.properties: Sets hello Search service URL and api-key</span></span>
* <span data-ttu-id="f3390-133">Pom.xml: uma dependência do Maven</span><span class="sxs-lookup"><span data-stu-id="f3390-133">Pom.xml: A Maven dependency</span></span>

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="f3390-134">Localizar o nome do serviço hello e chave de api do serviço de pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="f3390-134">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="f3390-135">Todas as chamadas de API REST na pesquisa do Azure exigem que você forneça a URL do serviço hello e uma chave de api.</span><span class="sxs-lookup"><span data-stu-id="f3390-135">All REST API calls into Azure Search require that you provide hello service URL and an api-key.</span></span> 

1. <span data-ttu-id="f3390-136">Entrar toohello [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f3390-136">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f3390-137">Na barra de salto hello, clique em **serviço de pesquisa** toolist todos os serviços de pesquisa do Azure Olá provisionados para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="f3390-137">In hello jump bar, click **Search service** toolist all of hello Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="f3390-138">Selecione serviço Olá toouse desejado.</span><span class="sxs-lookup"><span data-stu-id="f3390-138">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="f3390-139">No painel de serviço hello, você verá blocos para obter informações essenciais, bem como o ícone de chave Olá para acessar as chaves de administração de saudação.</span><span class="sxs-lookup"><span data-stu-id="f3390-139">On hello service dashboard, you'll see tiles for essential information as well as hello key icon for accessing hello admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="f3390-140">Copiar URL do serviço hello e uma chave de administração.</span><span class="sxs-lookup"><span data-stu-id="f3390-140">Copy hello service URL and an admin key.</span></span> <span data-ttu-id="f3390-141">Você precisará deles mais tarde, quando você adiciona toohello **config** arquivo.</span><span class="sxs-lookup"><span data-stu-id="f3390-141">You will need them later, when you add them toohello **config.properties** file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="f3390-142">Baixar arquivos de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="f3390-142">Download hello sample files</span></span>
1. <span data-ttu-id="f3390-143">Vá muito[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="f3390-143">Go too[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) on GitHub.</span></span>
2. <span data-ttu-id="f3390-144">Clique em **baixar ZIP**, salvar toodisk de arquivo. zip hello e, em seguida, extraia todos os arquivos de saudação nele.</span><span class="sxs-lookup"><span data-stu-id="f3390-144">Click **Download ZIP**, save hello .zip file toodisk, and then extract all hello files it contains.</span></span> <span data-ttu-id="f3390-145">Considere a possibilidade de extrair Olá arquivos em seu toomake de espaço de trabalho do Java-projeto mais fácil de saudação toofind mais tarde.</span><span class="sxs-lookup"><span data-stu-id="f3390-145">Consider extracting hello files into your Java workspace toomake it easier toofind hello project later.</span></span>
3. <span data-ttu-id="f3390-146">arquivos de exemplo Hello são somente leitura.</span><span class="sxs-lookup"><span data-stu-id="f3390-146">hello sample files are read-only.</span></span> <span data-ttu-id="f3390-147">Clique em Propriedades de pasta e atributo somente leitura de saudação limpar.</span><span class="sxs-lookup"><span data-stu-id="f3390-147">Right-click folder properties and clear hello read-only attribute.</span></span>

<span data-ttu-id="f3390-148">Todas as modificações de arquivos subsequentes e instruções de execução serão feitas nos arquivos nessa pasta.</span><span class="sxs-lookup"><span data-stu-id="f3390-148">All subsequent file modifications and run statements will be made against files in this folder.</span></span>  

## <a name="import-project"></a><span data-ttu-id="f3390-149">Projeto de importação</span><span class="sxs-lookup"><span data-stu-id="f3390-149">Import project</span></span>
1. <span data-ttu-id="f3390-150">No Eclipse, escolha **Arquivo** > **Importar** > **Geral** > **Projetos Existentes no Espaço de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="f3390-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span></span>
   
    ![][4]
2. <span data-ttu-id="f3390-151">Em **diretório raiz selecione**, procurar pasta toohello que contém os arquivos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="f3390-151">In **Select root directory**, browse toohello folder containing sample files.</span></span> <span data-ttu-id="f3390-152">Selecione a pasta de saudação que contém a pasta do hello. Project.</span><span class="sxs-lookup"><span data-stu-id="f3390-152">Select hello folder that contains hello .project folder.</span></span> <span data-ttu-id="f3390-153">projeto Olá deve aparecer em Olá **projetos** lista como um item selecionado.</span><span class="sxs-lookup"><span data-stu-id="f3390-153">hello project should appear in hello **Projects** list as a selected item.</span></span>
   
    ![][12]
3. <span data-ttu-id="f3390-154">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="f3390-154">Click **Finish**.</span></span>
4. <span data-ttu-id="f3390-155">Use **Explorador de projeto** tooview e editar arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f3390-155">Use **Project Explorer** tooview and edit hello files.</span></span> <span data-ttu-id="f3390-156">Se ainda não estiver aberto, clique em **janela** > **exibição** > **Explorador de projeto** ou use Olá atalho tooopen-lo.</span><span class="sxs-lookup"><span data-stu-id="f3390-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use hello shortcut tooopen it.</span></span>

## <a name="configure-hello-service-url-and-api-key"></a><span data-ttu-id="f3390-157">Configurar URL do serviço hello e chave de api</span><span class="sxs-lookup"><span data-stu-id="f3390-157">Configure hello service URL and api-key</span></span>
1. <span data-ttu-id="f3390-158">Em **Explorador de projeto**, clique duas vezes em **config** tooedit Olá configurações que contém o nome do servidor de saudação e a chave de api.</span><span class="sxs-lookup"><span data-stu-id="f3390-158">In **Project Explorer**, double-click **config.properties** tooedit hello configuration settings containing hello server name and api-key.</span></span>
2. <span data-ttu-id="f3390-159">Consulte toohello etapas neste artigo, onde você encontrado Olá URL do serviço e a chave de api no hello [Portal do Azure](https://portal.azure.com), valores de saudação tooget agora será informado no **config**.</span><span class="sxs-lookup"><span data-stu-id="f3390-159">Refer toohello steps earlier in this article, where you found hello service URL and api-key in hello [Azure Portal](https://portal.azure.com), tooget hello values you will now enter into **config.properties**.</span></span>
3. <span data-ttu-id="f3390-160">Em **config**, substitua "Chave de Api" hello-chave de api para o serviço.</span><span class="sxs-lookup"><span data-stu-id="f3390-160">In **config.properties**, replace "Api Key" with hello api-key for your service.</span></span> <span data-ttu-id="f3390-161">Em seguida, o nome do serviço (hello primeiro componente Olá URL http://servicename.search.windows.net) substitui o "nome do serviço" no hello mesmo arquivo.</span><span class="sxs-lookup"><span data-stu-id="f3390-161">Next, service name (hello first component of hello URL http://servicename.search.windows.net) replaces "service name" in hello same file.</span></span>
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a><span data-ttu-id="f3390-162">Configurar ambientes de projeto, compilação e tempo de execução de saudação</span><span class="sxs-lookup"><span data-stu-id="f3390-162">Configure hello project, build and runtime environments</span></span>
1. <span data-ttu-id="f3390-163">No Eclipse, no Explorador de projeto, clique com botão direito hello > **propriedades** > **facetas de projeto**.</span><span class="sxs-lookup"><span data-stu-id="f3390-163">In Eclipse, in Project Explorer, right-click hello project > **Properties** > **Project Facets**.</span></span>
2. <span data-ttu-id="f3390-164">Selecione **Módulo da Web dinâmico**, **Java** e **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="f3390-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span></span>
   
    ![][6]
3. <span data-ttu-id="f3390-165">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="f3390-165">Click **Apply**.</span></span>
4. <span data-ttu-id="f3390-166">Selecione **Janela** > **Preferências** > **Servidor** > **Ambientes de tempo de execução** > **Adicionar..**.</span><span class="sxs-lookup"><span data-stu-id="f3390-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span></span>
5. <span data-ttu-id="f3390-167">Expanda o Apache e selecione a versão de saudação do servidor do Apache Tomcat Olá instalado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f3390-167">Expand Apache and select hello version of hello Apache Tomcat server you previously installed.</span></span> <span data-ttu-id="f3390-168">Em nosso sistema, instalamos a versão 8.</span><span class="sxs-lookup"><span data-stu-id="f3390-168">On our system, we installed version 8.</span></span>
   
    ![][7]
6. <span data-ttu-id="f3390-169">Na página seguinte do hello, especifique o diretório de instalação do Tomcat de saudação.</span><span class="sxs-lookup"><span data-stu-id="f3390-169">On hello next page, specify hello Tomcat installation directory.</span></span> <span data-ttu-id="f3390-170">Em um computador Windows, isso provavelmente será C:\Arquivos de Programas\Apache Software Foundation\Tomcat *versão*.</span><span class="sxs-lookup"><span data-stu-id="f3390-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span></span>
7. <span data-ttu-id="f3390-171">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="f3390-171">Click **Finish**.</span></span>
8. <span data-ttu-id="f3390-172">Selecione **Janela** > **Preferências** > **Java** > **JREs Instalados** > **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f3390-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span></span>
9. <span data-ttu-id="f3390-173">Em **Adicionar JRE**, selecione **VM padrão**.</span><span class="sxs-lookup"><span data-stu-id="f3390-173">In **Add JRE**, select **Standard VM**.</span></span>
10. <span data-ttu-id="f3390-174">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="f3390-174">Click **Next**.</span></span>
11. <span data-ttu-id="f3390-175">Na Definição do JRE, na página inicial do JRE, clique em **Diretório**.</span><span class="sxs-lookup"><span data-stu-id="f3390-175">In JRE Definition, in JRE home, click **Directory**.</span></span>
12. <span data-ttu-id="f3390-176">Navegue muito**arquivos de programa** > **Java** e selecione Olá JDK instalado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f3390-176">Navigate too**Program Files** > **Java** and select hello JDK you previously installed.</span></span> <span data-ttu-id="f3390-177">É importante tooselect Olá JDK como Olá JRE.</span><span class="sxs-lookup"><span data-stu-id="f3390-177">It's important tooselect hello JDK as hello JRE.</span></span>
13. <span data-ttu-id="f3390-178">No JREs instalado, escolha Olá **JDK**.</span><span class="sxs-lookup"><span data-stu-id="f3390-178">In Installed JREs, choose hello **JDK**.</span></span> <span data-ttu-id="f3390-179">As configurações devem ter aparência semelhante toohello captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="f3390-179">Your settings should look similar toohello following screenshot.</span></span>
    
    ![][9]
14. <span data-ttu-id="f3390-180">Opcionalmente, selecione **janela** > **navegador da Web** > **Internet Explorer** aplicativo hello de tooopen em uma janela de navegador externo.</span><span class="sxs-lookup"><span data-stu-id="f3390-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** tooopen hello application in an external browser window.</span></span> <span data-ttu-id="f3390-181">Usar um navegador externo oferece uma melhor experiência de aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="f3390-181">Using an external browser gives you a better Web application experience.</span></span>
    
    ![][8]

<span data-ttu-id="f3390-182">Agora você concluiu as tarefas de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="f3390-182">You have now completed hello configuration tasks.</span></span> <span data-ttu-id="f3390-183">Em seguida, compilar e executar o projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="f3390-183">Next, you'll build and run hello project.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="f3390-184">Compilar o projeto de saudação</span><span class="sxs-lookup"><span data-stu-id="f3390-184">Build hello project</span></span>
1. <span data-ttu-id="f3390-185">No Explorador de projeto, clique o nome do projeto hello e escolha **executar como** > **build Maven...**  tooconfigure projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="f3390-185">In Project Explorer, right-click hello project name and choose **Run As** > **Maven build...** tooconfigure hello project.</span></span>
   
    ![][10]
2. <span data-ttu-id="f3390-186">Em Editar configurações, em Metas, digite "instalação limpa" e, em seguida, clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="f3390-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span></span>

<span data-ttu-id="f3390-187">Mensagens de status são a janela do console de toohello de saída.</span><span class="sxs-lookup"><span data-stu-id="f3390-187">Status messages are output toohello console window.</span></span> <span data-ttu-id="f3390-188">Você deve ver o projeto de saudação indicando êxito na compilação compilado sem erros.</span><span class="sxs-lookup"><span data-stu-id="f3390-188">You should see BUILD SUCCESS indicating hello project built without errors.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="f3390-189">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="f3390-189">Run hello app</span></span>
<span data-ttu-id="f3390-190">Nesta última etapa, você executará o aplicativo hello em um ambiente de tempo de execução do servidor local.</span><span class="sxs-lookup"><span data-stu-id="f3390-190">In this last step, you will run hello application in a local server runtime environment.</span></span>

<span data-ttu-id="f3390-191">Se você ainda não especificou um ambiente de tempo de execução do servidor no Eclipse, você precisará toodo isso primeiro.</span><span class="sxs-lookup"><span data-stu-id="f3390-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need toodo that first.</span></span>

1. <span data-ttu-id="f3390-192">No Gerenciador de Projetos, expanda **WebContent**.</span><span class="sxs-lookup"><span data-stu-id="f3390-192">In Project Explorer, expand **WebContent**.</span></span>
2. <span data-ttu-id="f3390-193">Clique com o botão direito do mouse em **Search.jsp** > **Executar como** > **Executar no Servidor**.</span><span class="sxs-lookup"><span data-stu-id="f3390-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span></span> <span data-ttu-id="f3390-194">Selecione o servidor do Apache Tomcat hello e, em seguida, clique em **executar**.</span><span class="sxs-lookup"><span data-stu-id="f3390-194">Select hello Apache Tomcat server, and then click **Run**.</span></span>

> [!TIP]
> <span data-ttu-id="f3390-195">Se você tiver usado um espaço de trabalho não padrão toostore seu projeto, você precisará toomodify **configuração executar** toopoint toohello projeto local tooavoid um erro de inicialização do servidor.</span><span class="sxs-lookup"><span data-stu-id="f3390-195">If you used a non-default workspace toostore your project, you'll need toomodify **Run Configuration** toopoint toohello project location tooavoid a server start-up error.</span></span> <span data-ttu-id="f3390-196">No Gerenciador de Projetos, clique com o botão direito do mouse em **Search.jsp** > **Executar como** > **Configurações de Execução**.</span><span class="sxs-lookup"><span data-stu-id="f3390-196">In Project Explorer, right-click **Search.jsp** > **Run As** > **Run Configurations**.</span></span> <span data-ttu-id="f3390-197">Selecione o servidor do Apache Tomcat Olá.</span><span class="sxs-lookup"><span data-stu-id="f3390-197">Select hello Apache Tomcat server.</span></span> <span data-ttu-id="f3390-198">Clique em **Argumentos**.</span><span class="sxs-lookup"><span data-stu-id="f3390-198">Click **Arguments**.</span></span> <span data-ttu-id="f3390-199">Clique em **espaço de trabalho** ou **sistema de arquivos** tooset pasta de saudação que contém o projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="f3390-199">Click **Workspace** or **File System** tooset hello folder containing hello project.</span></span>
> 
> 

<span data-ttu-id="f3390-200">Quando você executa o aplicativo hello, você verá uma janela do navegador, fornecendo uma caixa de pesquisa para a inserção de termos.</span><span class="sxs-lookup"><span data-stu-id="f3390-200">When you run hello application, you should see a browser window, providing a search box for entering terms.</span></span>

<span data-ttu-id="f3390-201">Aguarde cerca de um minuto antes de clicar em **pesquisa** toogive Olá serviço tempo toocreate e carga Olá índice.</span><span class="sxs-lookup"><span data-stu-id="f3390-201">Wait about one minute before clicking **Search** toogive hello service time toocreate and load hello index.</span></span> <span data-ttu-id="f3390-202">Se você receber um erro HTTP 404, basta toowait mais um pouco antes de tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="f3390-202">If you get an HTTP 404 error, you just need toowait a little bit longer before trying again.</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="f3390-203">Pesquisar dados do USGS</span><span class="sxs-lookup"><span data-stu-id="f3390-203">Search on USGS data</span></span>
<span data-ttu-id="f3390-204">conjunto de dados USGS Olá inclui registros que são relevante toohello estado de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="f3390-204">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="f3390-205">Se você clicar em **pesquisa** em uma caixa de pesquisa vazia, você obterá as entradas de 50 principais hello, que é o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f3390-205">If you click **Search** on an empty search box, you will get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="f3390-206">Inserindo um termo de pesquisa fornecerá o mecanismo de pesquisa Olá algo toogo sobre.</span><span class="sxs-lookup"><span data-stu-id="f3390-206">Entering a search term will give hello search engine something toogo on.</span></span> <span data-ttu-id="f3390-207">Tente inserir um nome regional.</span><span class="sxs-lookup"><span data-stu-id="f3390-207">Try entering a regional name.</span></span> <span data-ttu-id="f3390-208">"Roger Williams" era o administrador primeiro Olá de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="f3390-208">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="f3390-209">Vários parques, edifícios e escolas receberam seus nomes em homenagem a ele.</span><span class="sxs-lookup"><span data-stu-id="f3390-209">Numerous parks, buildings, and schools are named after him.</span></span>

![][11]

<span data-ttu-id="f3390-210">Você também pode tentar qualquer um destes termos:</span><span class="sxs-lookup"><span data-stu-id="f3390-210">You could also try any of these terms:</span></span>

* <span data-ttu-id="f3390-211">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="f3390-211">Pawtucket</span></span>
* <span data-ttu-id="f3390-212">Pembroke</span><span class="sxs-lookup"><span data-stu-id="f3390-212">Pembroke</span></span>
* <span data-ttu-id="f3390-213">goose +cape</span><span class="sxs-lookup"><span data-stu-id="f3390-213">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3390-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f3390-214">Next steps</span></span>
<span data-ttu-id="f3390-215">Este é o hello primeiro tutorial de pesquisa do Azure com base em Java e hello USGS dataset.</span><span class="sxs-lookup"><span data-stu-id="f3390-215">This is hello first Azure Search tutorial based on Java and hello USGS dataset.</span></span> <span data-ttu-id="f3390-216">Ao longo do tempo, estenderemos esse tutorial toodemonstrate recursos adicionais de pesquisa convém toouse em suas soluções personalizadas.</span><span class="sxs-lookup"><span data-stu-id="f3390-216">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="f3390-217">Se você já tiver alguns em segundo plano na pesquisa do Azure, você pode usar este exemplo como um springboard experimentação adicional, aumentando talvez Olá [página Pesquisa](search-pagination-page-layout.md), ou a implementação de [navegação facetada](search-faceted-navigation.md).</span><span class="sxs-lookup"><span data-stu-id="f3390-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting hello [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span></span> <span data-ttu-id="f3390-218">Você também pode melhorar após a página de resultados da pesquisa de saudação adicionando contagens e envio em lote documentos para que os usuários podem percorrer resultados hello.</span><span class="sxs-lookup"><span data-stu-id="f3390-218">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="f3390-219">TooAzure nova pesquisa?</span><span class="sxs-lookup"><span data-stu-id="f3390-219">New tooAzure Search?</span></span> <span data-ttu-id="f3390-220">É recomendável tentar toodevelop outros tutoriais um entendimento de como você pode criar.</span><span class="sxs-lookup"><span data-stu-id="f3390-220">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="f3390-221">Visite nosso [página de documentação](https://azure.microsoft.com/documentation/services/search/) toofind mais recursos.</span><span class="sxs-lookup"><span data-stu-id="f3390-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="f3390-222">Você também pode exibir links Olá em nosso [vídeo e Tutorial lista](search-video-demo-tutorial-list.md) tooaccess obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="f3390-222">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
