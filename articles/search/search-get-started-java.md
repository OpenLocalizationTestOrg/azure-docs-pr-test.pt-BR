---
title: "Introdução ao Azure Search no Java | Microsoft Docs"
description: "Como criar um aplicativo de pesquisa hospedado na nuvem no Azure usando Java como linguagem de programação."
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
ms.openlocfilehash: f6ca06a0349def97b38a1bf6d0d8f36236077e92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-search-in-java"></a><span data-ttu-id="666c8-103">Introdução à Pesquisa do Azure em Java</span><span class="sxs-lookup"><span data-stu-id="666c8-103">Get started with Azure Search in Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="666c8-104">Portal</span><span class="sxs-lookup"><span data-stu-id="666c8-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="666c8-105">.NET</span><span class="sxs-lookup"><span data-stu-id="666c8-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="666c8-106">Aprenda a criar um aplicativo de pesquisa Java personalizado que usa a Pesquisa do Azure para sua experiência de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="666c8-106">Learn how to build a custom Java search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="666c8-107">O tutorial usa a [API REST do Serviço de Pesquisa do Azure](https://msdn.microsoft.com/library/dn798935.aspx) para construir os objetos e as operações usados neste exercício.</span><span class="sxs-lookup"><span data-stu-id="666c8-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span></span>

<span data-ttu-id="666c8-108">Para executar este exemplo, você deve ter um serviço de Pesquisa do Azure, no qual pode se inscrever no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="666c8-108">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="666c8-109">Consulte [Criar um serviço de Pesquisa do Azure no portal](search-create-service-portal.md) para encontrar instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="666c8-109">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

<span data-ttu-id="666c8-110">Para compilar e testar este exemplo, usamos o seguinte software:</span><span class="sxs-lookup"><span data-stu-id="666c8-110">We used the following software to build and test this sample:</span></span>

* <span data-ttu-id="666c8-111">[Eclipse IDE para desenvolvedores de Java EE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span><span class="sxs-lookup"><span data-stu-id="666c8-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span></span> <span data-ttu-id="666c8-112">Certifique-se de baixar a versão EE.</span><span class="sxs-lookup"><span data-stu-id="666c8-112">Be sure to download the EE version.</span></span> <span data-ttu-id="666c8-113">Uma das etapas de verificação requer um recurso que está apenas nesta edição.</span><span class="sxs-lookup"><span data-stu-id="666c8-113">One of the verification steps requires a feature that is found only in this edition.</span></span>
* [<span data-ttu-id="666c8-114">JDK 8u40</span><span class="sxs-lookup"><span data-stu-id="666c8-114">JDK 8u40</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="666c8-115">Apache Tomcat 8.0</span><span class="sxs-lookup"><span data-stu-id="666c8-115">Apache Tomcat 8.0</span></span>](http://tomcat.apache.org/download-80.cgi)

## <a name="about-the-data"></a><span data-ttu-id="666c8-116">Sobre os dados</span><span class="sxs-lookup"><span data-stu-id="666c8-116">About the data</span></span>
<span data-ttu-id="666c8-117">Este exemplo de aplicativo usa dados do [Serviço Geológico dos Estados Unidos (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtrados no estado de Rhode Island, para reduzir o tamanho do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="666c8-117">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span></span> <span data-ttu-id="666c8-118">Vamos usar esses dados para criar um aplicativo de pesquisa que retorna prédios de referência, como hospitais e escolas, bem como características geológicas como rios, lagos e picos.</span><span class="sxs-lookup"><span data-stu-id="666c8-118">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="666c8-119">Neste aplicativo, o programa **SearchServlet.java** cria e carrega o índice usando uma construção [Indexador](https://msdn.microsoft.com/library/azure/dn798918.aspx) , recuperando o conjunto de dados filtrado do USGS por meio de um Banco de dados SQL do Azure público.</span><span class="sxs-lookup"><span data-stu-id="666c8-119">In this application, the **SearchServlet.java** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="666c8-120">Credenciais predefinidas e informações de conexão para a fonte de dados online são fornecidas no código do programa.</span><span class="sxs-lookup"><span data-stu-id="666c8-120">Predefined credentials and connection  information to the online data source are provided in the program code.</span></span> <span data-ttu-id="666c8-121">Em termos de acesso a dados, nenhuma configuração adicional é necessária.</span><span class="sxs-lookup"><span data-stu-id="666c8-121">In terms of data access, no further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="666c8-122">Aplicamos um filtro a esse conjunto de dados para permanecer abaixo do limite de 10.000 documentos da camada de preços gratuita.</span><span class="sxs-lookup"><span data-stu-id="666c8-122">We applied a filter on this dataset to stay under the 10,000 document limit of the free pricing tier.</span></span> <span data-ttu-id="666c8-123">Se você usar a camada padrão, esse limite não se aplica e você pode modificar este código para usar um conjunto de dados maior.</span><span class="sxs-lookup"><span data-stu-id="666c8-123">If you use the standard tier, this limit does not apply, and you can modify this code to use a bigger dataset.</span></span> <span data-ttu-id="666c8-124">Para obter detalhes sobre a capacidade de cada camada de preços, consulte [Limites e restrições](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="666c8-124">For details about capacity for each pricing tier, see [Limits and constraints](search-limits-quotas-capacity.md).</span></span>
> 
> 

## <a name="about-the-program-files"></a><span data-ttu-id="666c8-125">Sobre os arquivos de programa</span><span class="sxs-lookup"><span data-stu-id="666c8-125">About the program files</span></span>
<span data-ttu-id="666c8-126">A lista a seguir descreve os arquivos que são relevantes para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="666c8-126">The following list describes the files that are relevant to this sample.</span></span>

* <span data-ttu-id="666c8-127">Search.jsp: fornece a interface do usuário</span><span class="sxs-lookup"><span data-stu-id="666c8-127">Search.jsp: Provides the user interface</span></span>
* <span data-ttu-id="666c8-128">SearchServlet.java: fornece métodos (semelhantes a um controlador em MVC)</span><span class="sxs-lookup"><span data-stu-id="666c8-128">SearchServlet.java: Provides methods (similar to a controller in MVC)</span></span>
* <span data-ttu-id="666c8-129">SearchServiceClient.java: lida com solicitações HTTP</span><span class="sxs-lookup"><span data-stu-id="666c8-129">SearchServiceClient.java: Handles HTTP requests</span></span>
* <span data-ttu-id="666c8-130">SearchServiceHelper.java: uma classe auxiliar que fornece métodos estáticos</span><span class="sxs-lookup"><span data-stu-id="666c8-130">SearchServiceHelper.java: A helper class that provides static methods</span></span>
* <span data-ttu-id="666c8-131">Document.Java: fornece o modelo de dados</span><span class="sxs-lookup"><span data-stu-id="666c8-131">Document.java: Provides the data model</span></span>
* <span data-ttu-id="666c8-132">config.properties: define a URL do serviço de Pesquisa e a chave de Api</span><span class="sxs-lookup"><span data-stu-id="666c8-132">config.properties: Sets the Search service URL and api-key</span></span>
* <span data-ttu-id="666c8-133">Pom.xml: uma dependência do Maven</span><span class="sxs-lookup"><span data-stu-id="666c8-133">Pom.xml: A Maven dependency</span></span>

<a id="sub-2"></a>

## <a name="find-the-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="666c8-134">Localizar o nome do serviço e a chave de api do serviço de Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="666c8-134">Find the service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="666c8-135">Todas as chamadas da API REST na Pesquisa do Azure exigem que você forneça a URL do serviço e uma chave de api.</span><span class="sxs-lookup"><span data-stu-id="666c8-135">All REST API calls into Azure Search require that you provide the service URL and an api-key.</span></span> 

1. <span data-ttu-id="666c8-136">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="666c8-136">Sign in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="666c8-137">Na barra de atalhos, clique em **Serviço de Pesquisa** para listar todos os serviços da Pesquisa do Azure provisionados para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="666c8-137">In the jump bar, click **Search service** to list all of the Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="666c8-138">Selecione o serviço que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="666c8-138">Select the service you want to use.</span></span>
4. <span data-ttu-id="666c8-139">No painel de serviço, você verá blocos com as informações essenciais e o ícone de chave para acessar as chaves de administrador.</span><span class="sxs-lookup"><span data-stu-id="666c8-139">On the service dashboard, you'll see tiles for essential information as well as the key icon for accessing the admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="666c8-140">Copie a URL do serviço e uma chave de administrador.</span><span class="sxs-lookup"><span data-stu-id="666c8-140">Copy the service URL and an admin key.</span></span> <span data-ttu-id="666c8-141">Você precisará dos três posteriormente, ao adicioná-los ao arquivo **config.properties** .</span><span class="sxs-lookup"><span data-stu-id="666c8-141">You will need them later, when you add them to the **config.properties** file.</span></span>

## <a name="download-the-sample-files"></a><span data-ttu-id="666c8-142">Baixe os arquivos do exemplo.</span><span class="sxs-lookup"><span data-stu-id="666c8-142">Download the sample files</span></span>
1. <span data-ttu-id="666c8-143">Vá para [AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="666c8-143">Go to [AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) on GitHub.</span></span>
2. <span data-ttu-id="666c8-144">Clique em **Baixar ZIP**, salve o arquivo .zip no disco e, em seguida, extraia todos os arquivos que ele contém.</span><span class="sxs-lookup"><span data-stu-id="666c8-144">Click **Download ZIP**, save the .zip file to disk, and then extract all the files it contains.</span></span> <span data-ttu-id="666c8-145">Considere a possibilidade de extrair os arquivos no espaço de trabalho Java para facilitar a localização do projeto posteriormente.</span><span class="sxs-lookup"><span data-stu-id="666c8-145">Consider extracting the files into your Java workspace to make it easier to find the project later.</span></span>
3. <span data-ttu-id="666c8-146">Os arquivos de exemplo são somente leitura.</span><span class="sxs-lookup"><span data-stu-id="666c8-146">The sample files are read-only.</span></span> <span data-ttu-id="666c8-147">Clique com o botão direito em propriedades da pasta e limpe o atributo somente leitura.</span><span class="sxs-lookup"><span data-stu-id="666c8-147">Right-click folder properties and clear the read-only attribute.</span></span>

<span data-ttu-id="666c8-148">Todas as modificações de arquivos subsequentes e instruções de execução serão feitas nos arquivos nessa pasta.</span><span class="sxs-lookup"><span data-stu-id="666c8-148">All subsequent file modifications and run statements will be made against files in this folder.</span></span>  

## <a name="import-project"></a><span data-ttu-id="666c8-149">Projeto de importação</span><span class="sxs-lookup"><span data-stu-id="666c8-149">Import project</span></span>
1. <span data-ttu-id="666c8-150">No Eclipse, escolha **Arquivo** > **Importar** > **Geral** > **Projetos Existentes no Espaço de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="666c8-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span></span>
   
    ![][4]
2. <span data-ttu-id="666c8-151">Em **Selecionar diretório raiz**, navegue até a pasta que contém os arquivos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="666c8-151">In **Select root directory**, browse to the folder containing sample files.</span></span> <span data-ttu-id="666c8-152">Selecione a pasta que contém a pasta .project.</span><span class="sxs-lookup"><span data-stu-id="666c8-152">Select the folder that contains the .project folder.</span></span> <span data-ttu-id="666c8-153">O projeto deve aparecer na lista **Projetos** como um item selecionado.</span><span class="sxs-lookup"><span data-stu-id="666c8-153">The project should appear in the **Projects** list as a selected item.</span></span>
   
    ![][12]
3. <span data-ttu-id="666c8-154">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="666c8-154">Click **Finish**.</span></span>
4. <span data-ttu-id="666c8-155">Use o **Gerenciador de Projetos** para exibir e editar os arquivos.</span><span class="sxs-lookup"><span data-stu-id="666c8-155">Use **Project Explorer** to view and edit the files.</span></span> <span data-ttu-id="666c8-156">Se não ainda estiver aberto, clique em **Janela** > **Exibição** > **Gerenciador de Projetos** ou use o atalho para abri-lo.</span><span class="sxs-lookup"><span data-stu-id="666c8-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use the shortcut to open it.</span></span>

## <a name="configure-the-service-url-and-api-key"></a><span data-ttu-id="666c8-157">Configurar a URL de serviço e a chave de API</span><span class="sxs-lookup"><span data-stu-id="666c8-157">Configure the service URL and api-key</span></span>
1. <span data-ttu-id="666c8-158">Em **Gerenciador de Projetos**, clique duas vezes em **config.properties** para editar as definições de configuração que contêm o nome do servidor e a chave de Api.</span><span class="sxs-lookup"><span data-stu-id="666c8-158">In **Project Explorer**, double-click **config.properties** to edit the configuration settings containing the server name and api-key.</span></span>
2. <span data-ttu-id="666c8-159">Consulte as etapas explicadas anteriormente neste artigo, em que você encontrou a URL de serviço e a chave de API no [Portal do Azure](https://portal.azure.com), para obter os valores que você vai inserir agora em **config.properties**.</span><span class="sxs-lookup"><span data-stu-id="666c8-159">Refer to the steps earlier in this article, where you found the service URL and api-key in the [Azure Portal](https://portal.azure.com), to get the values you will now enter into **config.properties**.</span></span>
3. <span data-ttu-id="666c8-160">Em **config.properties**, substitua "Chave Api" com a chave de Api para o serviço.</span><span class="sxs-lookup"><span data-stu-id="666c8-160">In **config.properties**, replace "Api Key" with the api-key for your service.</span></span> <span data-ttu-id="666c8-161">Em seguida, o nome do serviço (o primeiro componente da URL http://servicename.search.windows.net) substitui o "nome do serviço" no mesmo arquivo.</span><span class="sxs-lookup"><span data-stu-id="666c8-161">Next, service name (the first component of the URL http://servicename.search.windows.net) replaces "service name" in the same file.</span></span>
   
    ![][5]

## <a name="configure-the-project-build-and-runtime-environments"></a><span data-ttu-id="666c8-162">Configurar ambientes de projeto, compilação e tempo de execução</span><span class="sxs-lookup"><span data-stu-id="666c8-162">Configure the project, build and runtime environments</span></span>
1. <span data-ttu-id="666c8-163">No Eclipse, no Gerenciador de Projetos, clique com o botão direito do mouse no projeto > **Propriedades** > **Facetas do Projeto**.</span><span class="sxs-lookup"><span data-stu-id="666c8-163">In Eclipse, in Project Explorer, right-click the project > **Properties** > **Project Facets**.</span></span>
2. <span data-ttu-id="666c8-164">Selecione **Módulo da Web dinâmico**, **Java** e **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="666c8-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span></span>
   
    ![][6]
3. <span data-ttu-id="666c8-165">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="666c8-165">Click **Apply**.</span></span>
4. <span data-ttu-id="666c8-166">Selecione **Janela** > **Preferências** > **Servidor** > **Ambientes de tempo de execução** > **Adicionar..**.</span><span class="sxs-lookup"><span data-stu-id="666c8-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span></span>
5. <span data-ttu-id="666c8-167">Expanda o Apache e selecione a versão do servidor Apache Tomcat instalado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="666c8-167">Expand Apache and select the version of the Apache Tomcat server you previously installed.</span></span> <span data-ttu-id="666c8-168">Em nosso sistema, instalamos a versão 8.</span><span class="sxs-lookup"><span data-stu-id="666c8-168">On our system, we installed version 8.</span></span>
   
    ![][7]
6. <span data-ttu-id="666c8-169">Na próxima página, especifique o diretório de instalação do Tomcat.</span><span class="sxs-lookup"><span data-stu-id="666c8-169">On the next page, specify the Tomcat installation directory.</span></span> <span data-ttu-id="666c8-170">Em um computador Windows, isso provavelmente será C:\Arquivos de Programas\Apache Software Foundation\Tomcat *versão*.</span><span class="sxs-lookup"><span data-stu-id="666c8-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span></span>
7. <span data-ttu-id="666c8-171">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="666c8-171">Click **Finish**.</span></span>
8. <span data-ttu-id="666c8-172">Selecione **Janela** > **Preferências** > **Java** > **JREs Instalados** > **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="666c8-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span></span>
9. <span data-ttu-id="666c8-173">Em **Adicionar JRE**, selecione **VM padrão**.</span><span class="sxs-lookup"><span data-stu-id="666c8-173">In **Add JRE**, select **Standard VM**.</span></span>
10. <span data-ttu-id="666c8-174">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="666c8-174">Click **Next**.</span></span>
11. <span data-ttu-id="666c8-175">Na Definição do JRE, na página inicial do JRE, clique em **Diretório**.</span><span class="sxs-lookup"><span data-stu-id="666c8-175">In JRE Definition, in JRE home, click **Directory**.</span></span>
12. <span data-ttu-id="666c8-176">Navegue até **Arquivos de Programas** > **Java** e selecione o JDK instalado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="666c8-176">Navigate to **Program Files** > **Java** and select the JDK you previously installed.</span></span> <span data-ttu-id="666c8-177">É importante selecionar o JDK como o JRE.</span><span class="sxs-lookup"><span data-stu-id="666c8-177">It's important to select the JDK as the JRE.</span></span>
13. <span data-ttu-id="666c8-178">Em JREs instalados, escolha o **JDK**.</span><span class="sxs-lookup"><span data-stu-id="666c8-178">In Installed JREs, choose the **JDK**.</span></span> <span data-ttu-id="666c8-179">Suas configurações devem ter aparência semelhante à captura de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="666c8-179">Your settings should look similar to the following screenshot.</span></span>
    
    ![][9]
14. <span data-ttu-id="666c8-180">Opcionalmente, selecione **Janela** > **Navegador da Web** > **Internet Explorer** para abrir o aplicativo em uma janela do navegador externo.</span><span class="sxs-lookup"><span data-stu-id="666c8-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** to open the application in an external browser window.</span></span> <span data-ttu-id="666c8-181">Usar um navegador externo oferece uma melhor experiência de aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="666c8-181">Using an external browser gives you a better Web application experience.</span></span>
    
    ![][8]

<span data-ttu-id="666c8-182">Agora, você concluiu as tarefas de configuração.</span><span class="sxs-lookup"><span data-stu-id="666c8-182">You have now completed the configuration tasks.</span></span> <span data-ttu-id="666c8-183">Em seguida, você compilará e executará o projeto.</span><span class="sxs-lookup"><span data-stu-id="666c8-183">Next, you'll build and run the project.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="666c8-184">Compilar o projeto</span><span class="sxs-lookup"><span data-stu-id="666c8-184">Build the project</span></span>
1. <span data-ttu-id="666c8-185">No Gerenciador de Projetos, clique com o botão direito do mouse no nome do projeto e escolha **Executar como** > **Compilação Maven...** para configurar o projeto.</span><span class="sxs-lookup"><span data-stu-id="666c8-185">In Project Explorer, right-click the project name and choose **Run As** > **Maven build...** to configure the project.</span></span>
   
    ![][10]
2. <span data-ttu-id="666c8-186">Em Editar configurações, em Metas, digite "instalação limpa" e, em seguida, clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="666c8-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span></span>

<span data-ttu-id="666c8-187">Mensagens de status são passadas para a janela do console.</span><span class="sxs-lookup"><span data-stu-id="666c8-187">Status messages are output to the console window.</span></span> <span data-ttu-id="666c8-188">Você deve ver a mensagem COMPILAÇÃO BEM-SUCEDIDA, indicando que o foi projeto compilado sem erros.</span><span class="sxs-lookup"><span data-stu-id="666c8-188">You should see BUILD SUCCESS indicating the project built without errors.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="666c8-189">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="666c8-189">Run the app</span></span>
<span data-ttu-id="666c8-190">Nesta última etapa, você executará o aplicativo em um ambiente de tempo de execução do servidor local.</span><span class="sxs-lookup"><span data-stu-id="666c8-190">In this last step, you will run the application in a local server runtime environment.</span></span>

<span data-ttu-id="666c8-191">Se você ainda não especificou um ambiente de tempo de execução do servidor no Eclipse, você precisará fazer isso primeiro.</span><span class="sxs-lookup"><span data-stu-id="666c8-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need to do that first.</span></span>

1. <span data-ttu-id="666c8-192">No Gerenciador de Projetos, expanda **WebContent**.</span><span class="sxs-lookup"><span data-stu-id="666c8-192">In Project Explorer, expand **WebContent**.</span></span>
2. <span data-ttu-id="666c8-193">Clique com o botão direito do mouse em **Search.jsp** > **Executar como** > **Executar no Servidor**.</span><span class="sxs-lookup"><span data-stu-id="666c8-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span></span> <span data-ttu-id="666c8-194">Selecione o servidor Apache Tomcat e, em seguida, clique em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="666c8-194">Select the Apache Tomcat server, and then click **Run**.</span></span>

> [!TIP]
> <span data-ttu-id="666c8-195">Se você tiver usado um espaço de trabalho não padrão para armazenar seu projeto, precisará modificar a **Configuração de Execução** para indicar o local do projeto para evitar um erro de inicialização do servidor.</span><span class="sxs-lookup"><span data-stu-id="666c8-195">If you used a non-default workspace to store your project, you'll need to modify **Run Configuration** to point to the project location to avoid a server start-up error.</span></span> <span data-ttu-id="666c8-196">No Gerenciador de Projetos, clique com o botão direito do mouse em **Search.jsp** > **Executar como** > **Configurações de Execução**.</span><span class="sxs-lookup"><span data-stu-id="666c8-196">In Project Explorer, right-click **Search.jsp** > **Run As** > **Run Configurations**.</span></span> <span data-ttu-id="666c8-197">Selecione o servidor Apache Tomcat.</span><span class="sxs-lookup"><span data-stu-id="666c8-197">Select the Apache Tomcat server.</span></span> <span data-ttu-id="666c8-198">Clique em **Argumentos**.</span><span class="sxs-lookup"><span data-stu-id="666c8-198">Click **Arguments**.</span></span> <span data-ttu-id="666c8-199">Clique em **Espaço de Trabalho** ou **Sistema de Arquivos** para definir a pasta que contém o projeto.</span><span class="sxs-lookup"><span data-stu-id="666c8-199">Click **Workspace** or **File System** to set the folder containing the project.</span></span>
> 
> 

<span data-ttu-id="666c8-200">Quando você executar o aplicativo, verá uma janela do navegador, fornecendo uma caixa de pesquisa para inserir termos.</span><span class="sxs-lookup"><span data-stu-id="666c8-200">When you run the application, you should see a browser window, providing a search box for entering terms.</span></span>

<span data-ttu-id="666c8-201">Aguarde aproximadamente um minuto antes de clicar em **Pesquisa** para dar ao serviço tempo de criar e carregar o índice.</span><span class="sxs-lookup"><span data-stu-id="666c8-201">Wait about one minute before clicking **Search** to give the service time to create and load the index.</span></span> <span data-ttu-id="666c8-202">Se você receber um erro HTTP 404, basta esperar um pouco mais antes de tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="666c8-202">If you get an HTTP 404 error, you just need to wait a little bit longer before trying again.</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="666c8-203">Pesquisar em dados USGS</span><span class="sxs-lookup"><span data-stu-id="666c8-203">Search on USGS data</span></span>
<span data-ttu-id="666c8-204">O conjunto de dados do USGS inclui registros relevantes para o estado de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="666c8-204">The USGS data set includes records that are relevant to the state of Rhode Island.</span></span> <span data-ttu-id="666c8-205">Se você clicar em **Pesquisar** em uma caixa de pesquisa vazia, obterá as 50 entradas principais, que é o valor padrão.</span><span class="sxs-lookup"><span data-stu-id="666c8-205">If you click **Search** on an empty search box, you will get the top 50 entries, which is the default.</span></span>

<span data-ttu-id="666c8-206">A inserção de um termo de pesquisa fornecerá ao mecanismo de pesquisa algo para seguir.</span><span class="sxs-lookup"><span data-stu-id="666c8-206">Entering a search term will give the search engine something to go on.</span></span> <span data-ttu-id="666c8-207">Tente inserir um nome regional.</span><span class="sxs-lookup"><span data-stu-id="666c8-207">Try entering a regional name.</span></span> <span data-ttu-id="666c8-208">"Roger Williams" foi o primeiro governador de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="666c8-208">"Roger Williams" was the first governor of Rhode Island.</span></span> <span data-ttu-id="666c8-209">Vários parques, edifícios e escolas receberam seus nomes em homenagem a ele.</span><span class="sxs-lookup"><span data-stu-id="666c8-209">Numerous parks, buildings, and schools are named after him.</span></span>

![][11]

<span data-ttu-id="666c8-210">Você também pode tentar qualquer um destes termos:</span><span class="sxs-lookup"><span data-stu-id="666c8-210">You could also try any of these terms:</span></span>

* <span data-ttu-id="666c8-211">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="666c8-211">Pawtucket</span></span>
* <span data-ttu-id="666c8-212">Pembroke</span><span class="sxs-lookup"><span data-stu-id="666c8-212">Pembroke</span></span>
* <span data-ttu-id="666c8-213">goose +cape</span><span class="sxs-lookup"><span data-stu-id="666c8-213">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="666c8-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="666c8-214">Next steps</span></span>
<span data-ttu-id="666c8-215">Este é o primeiro tutorial da Pesquisa do Azure com base em Java e no conjunto de dados do USGS.</span><span class="sxs-lookup"><span data-stu-id="666c8-215">This is the first Azure Search tutorial based on Java and the USGS dataset.</span></span> <span data-ttu-id="666c8-216">Ao longo do tempo, ampliaremos este tutorial para demonstrar outros recursos de pesquisa que talvez você queira usar em suas soluções personalizadas.</span><span class="sxs-lookup"><span data-stu-id="666c8-216">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span></span>

<span data-ttu-id="666c8-217">Se você já tiver algum conhecimento sobre o Azure Search, use este exemplo como um trampolim para experimentos adicionais, talvez aumentando a [página de pesquisa](search-pagination-page-layout.md) ou implementando [navegação facetada](search-faceted-navigation.md).</span><span class="sxs-lookup"><span data-stu-id="666c8-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting the [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span></span> <span data-ttu-id="666c8-218">Você também pode melhorar a página de resultados da pesquisa adicionando contagens e documentos em lote para que os usuários possam percorrer os resultados.</span><span class="sxs-lookup"><span data-stu-id="666c8-218">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span></span>

<span data-ttu-id="666c8-219">Ainda não conhece a Pesquisa do Azure?</span><span class="sxs-lookup"><span data-stu-id="666c8-219">New to Azure Search?</span></span> <span data-ttu-id="666c8-220">Recomendamos os outros tutoriais para que você compreenda o que pode criar.</span><span class="sxs-lookup"><span data-stu-id="666c8-220">We recommend trying other tutorials to develop an understanding of what you can create.</span></span> <span data-ttu-id="666c8-221">Visite nossa [página de documentação](https://azure.microsoft.com/documentation/services/search/) para encontrar mais recursos.</span><span class="sxs-lookup"><span data-stu-id="666c8-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span></span> <span data-ttu-id="666c8-222">Você também pode exibir os links em nossa [Lista de vídeos e Tutorial](search-video-demo-tutorial-list.md) para acessar mais informações.</span><span class="sxs-lookup"><span data-stu-id="666c8-222">You can also view the links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) to access more information.</span></span>

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
