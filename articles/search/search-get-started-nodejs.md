---
title: "Introdução ao Azure Search no Node.js | Microsoft Docs"
description: "Percorra a criação de um aplicativo de pesquisa em um serviço de pesquisa hospedado na nuvem no Azure usando Node.js como linguagem de programação."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 0625dc1b-9db6-40d5-ba9a-4738b75cbe19
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 04/26/2017
ms.author: evboyle
ms.openlocfilehash: 32865ed986f5eea961ef2c3813dcc6531498c90a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="c16cf-103">Introdução ao Azure Search no Node.js</span><span class="sxs-lookup"><span data-stu-id="c16cf-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c16cf-104">Portal</span><span class="sxs-lookup"><span data-stu-id="c16cf-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="c16cf-105">.NET</span><span class="sxs-lookup"><span data-stu-id="c16cf-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="c16cf-106">Aprenda a criar um aplicativo de pesquisa Node.js personalizado que usa o Azure Search para a sua experiência de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="c16cf-106">Learn how to build a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="c16cf-107">O tutorial usa a [API REST do Serviço de Pesquisa do Azure](https://msdn.microsoft.com/library/dn798935.aspx) para construir os objetos e as operações usados neste exercício.</span><span class="sxs-lookup"><span data-stu-id="c16cf-107">This tutorial uses the [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) to construct the objects and operations used in this exercise.</span></span>

<span data-ttu-id="c16cf-108">Usamos o [Node.js](https://Nodejs.org) e o NPM, o [Sublime Text 3](http://www.sublimetext.com/3) e o Windows PowerShell no Windows 8.1 para desenvolver e testar esse código.</span><span class="sxs-lookup"><span data-stu-id="c16cf-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 to develop and test this code.</span></span>

<span data-ttu-id="c16cf-109">Para executar este exemplo, você deve ter um serviço do Azure Search, no qual pode se inscrever no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c16cf-109">To run this sample, you must have an Azure Search service, which you can sign up for in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c16cf-110">Consulte [Criar um serviço de Pesquisa do Azure no portal](search-create-service-portal.md) para encontrar instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="c16cf-110">See [Create an Azure Search service in the portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-the-data"></a><span data-ttu-id="c16cf-111">Sobre os dados</span><span class="sxs-lookup"><span data-stu-id="c16cf-111">About the data</span></span>
<span data-ttu-id="c16cf-112">Este exemplo de aplicativo usa dados do [Serviço Geológico dos Estados Unidos (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtrados no estado de Rhode Island, para reduzir o tamanho do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="c16cf-112">This sample application uses data from the [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on the state of Rhode Island to reduce the dataset size.</span></span> <span data-ttu-id="c16cf-113">Vamos usar esses dados para criar um aplicativo de pesquisa que retorna prédios de referência, por exemplo, hospitais e escolas, e características geológicas, como rios, lagos e picos.</span><span class="sxs-lookup"><span data-stu-id="c16cf-113">We'll use this data to build a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="c16cf-114">Neste aplicativo, o programa **DataIndexer** cria e carrega o índice usando um constructo [Indexador](https://msdn.microsoft.com/library/azure/dn798918.aspx) , recuperando o conjunto de dados filtrado do USGS de um Banco de Dados SQL do Azure público.</span><span class="sxs-lookup"><span data-stu-id="c16cf-114">In this application, the **DataIndexer** program builds and loads the index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving the filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="c16cf-115">As informações de credenciais e de conexão para a fonte de dados online são fornecidas no código do programa.</span><span class="sxs-lookup"><span data-stu-id="c16cf-115">Credentials and connection information to the online data source is provided in the program code.</span></span> <span data-ttu-id="c16cf-116">Nenhuma configuração adicional é necessária.</span><span class="sxs-lookup"><span data-stu-id="c16cf-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="c16cf-117">Aplicamos um filtro a esse conjunto de dados para permanecer abaixo do limite de 10.000 documentos da camada de preços gratuita.</span><span class="sxs-lookup"><span data-stu-id="c16cf-117">We applied a filter on this dataset to stay under the 10,000 document limit of the free pricing tier.</span></span> <span data-ttu-id="c16cf-118">Se você usar a camada padrão, esse limite não se aplicará.</span><span class="sxs-lookup"><span data-stu-id="c16cf-118">If you use the standard tier, this limit does not apply.</span></span> <span data-ttu-id="c16cf-119">Para obter detalhes sobre a capacidade de cada tipo de preço, consulte [Limites de serviço da Pesquisa](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="c16cf-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-the-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="c16cf-120">Localizar o nome do serviço e a chave de api do serviço de Pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="c16cf-120">Find the service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="c16cf-121">Depois de criar o serviço, retorne ao portal para obter a URL ou `api-key`.</span><span class="sxs-lookup"><span data-stu-id="c16cf-121">After you create the service, return to the portal to get the URL or `api-key`.</span></span> <span data-ttu-id="c16cf-122">Conexões com seu serviço de Pesquisa requerem que você tenha tanto uma URL quanto um `api-key` para autenticar a chamada.</span><span class="sxs-lookup"><span data-stu-id="c16cf-122">Connections to your Search service require that you have both the URL and an `api-key` to authenticate the call.</span></span>

1. <span data-ttu-id="c16cf-123">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c16cf-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c16cf-124">Na barra de atalhos, clique em **Serviço de Pesquisa** para listar todos os serviços do Azure Search provisionados para a sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="c16cf-124">In the jump bar, click **Search service** to list all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="c16cf-125">Selecione o serviço que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="c16cf-125">Select the service you want to use.</span></span>
4. <span data-ttu-id="c16cf-126">No painel de serviço, você deverá ver blocos com as informações essenciais, como o ícone de chave para acessar as chaves de administrador.</span><span class="sxs-lookup"><span data-stu-id="c16cf-126">On the service dashboard, you should see tiles for essential information, such as the key icon for accessing the admin keys.</span></span>
5. <span data-ttu-id="c16cf-127">Copie a URL do serviço, uma chave de administrador e uma chave de consulta.</span><span class="sxs-lookup"><span data-stu-id="c16cf-127">Copy the service URL, an admin key, and a query key.</span></span> <span data-ttu-id="c16cf-128">Você precisa de todos os três mais tarde, ao adicioná-los ao arquivo config.js.</span><span class="sxs-lookup"><span data-stu-id="c16cf-128">You need all three later when you add them to the config.js file.</span></span>

## <a name="download-the-sample-files"></a><span data-ttu-id="c16cf-129">Baixe os arquivos do exemplo.</span><span class="sxs-lookup"><span data-stu-id="c16cf-129">Download the sample files</span></span>
<span data-ttu-id="c16cf-130">Use qualquer um dos procedimentos a seguir para baixar o exemplo.</span><span class="sxs-lookup"><span data-stu-id="c16cf-130">Use either one of the following approaches to download the sample.</span></span>

1. <span data-ttu-id="c16cf-131">Acesse [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span><span class="sxs-lookup"><span data-stu-id="c16cf-131">Go to [AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="c16cf-132">Clique em **Baixar ZIP**, salve o arquivo .zip e, em seguida, extraia todos os arquivos que ele contém.</span><span class="sxs-lookup"><span data-stu-id="c16cf-132">Click **Download ZIP**, save the .zip file, and then extract all the files it contains.</span></span>

<span data-ttu-id="c16cf-133">Todas as modificações de arquivos posteriores e instruções de execução serão feitas nos arquivos nessa pasta.</span><span class="sxs-lookup"><span data-stu-id="c16cf-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-the-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="c16cf-134">Atualize o config.js.</span><span class="sxs-lookup"><span data-stu-id="c16cf-134">Update the config.js.</span></span> <span data-ttu-id="c16cf-135">com a URL e a chave de api do serviço Pesquisa</span><span class="sxs-lookup"><span data-stu-id="c16cf-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="c16cf-136">Usando a URL e a chave de api que você copiou anteriormente, especifique a URL, a chave de administrador e a chave de consulta no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="c16cf-136">Using the URL and api-key that you copied earlier, specify the URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="c16cf-137">As chaves de administrador oferecem controle total sobre as operações do serviço, incluindo a criação ou exclusão de um índice e carregamento de documentos.</span><span class="sxs-lookup"><span data-stu-id="c16cf-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="c16cf-138">Em contraste, as chaves de consulta servem para operações somente leitura, normalmente usadas por aplicativos cliente que se conectam à Pesquisa do Azure.</span><span class="sxs-lookup"><span data-stu-id="c16cf-138">In contrast, query keys are for read-only operations, typically used by client applications that connect to Azure Search.</span></span>

<span data-ttu-id="c16cf-139">Neste exemplo, incluímos a chave de consulta para ajudar a reforçar a prática recomendada de usar a chave de consulta em aplicativos cliente.</span><span class="sxs-lookup"><span data-stu-id="c16cf-139">In this sample, we include the query key to help reinforce the best practice of using the query key in client applications.</span></span>

<span data-ttu-id="c16cf-140">A captura de tela a seguir mostra **config.js** aberto em um editor de texto, com as entradas relevantes demarcadas para que você possa ver onde deve atualizá-lo com os valores válidos para o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="c16cf-140">The following screenshot shows **config.js** open in a text editor, with the relevant entries demarcated so that you can see where to update the file with the values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-the-sample"></a><span data-ttu-id="c16cf-141">Hospedar um ambiente de tempo de execução para o exemplo</span><span class="sxs-lookup"><span data-stu-id="c16cf-141">Host a runtime environment for the sample</span></span>
<span data-ttu-id="c16cf-142">O exemplo exige um servidor HTTP, que pode ser instalado globalmente usando npm.</span><span class="sxs-lookup"><span data-stu-id="c16cf-142">The sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="c16cf-143">Use uma janela do PowerShell para os comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="c16cf-143">Use a PowerShell window for the following commands.</span></span>

1. <span data-ttu-id="c16cf-144">Navegue até a pasta que contém o arquivo **package.json** .</span><span class="sxs-lookup"><span data-stu-id="c16cf-144">Navigate to the folder that contains the **package.json** file.</span></span>
2. <span data-ttu-id="c16cf-145">Digite `npm install`.</span><span class="sxs-lookup"><span data-stu-id="c16cf-145">Type `npm install`.</span></span>
3. <span data-ttu-id="c16cf-146">Digite `npm install -g http-server`.</span><span class="sxs-lookup"><span data-stu-id="c16cf-146">Type `npm install -g http-server`.</span></span>

## <a name="build-the-index-and-run-the-application"></a><span data-ttu-id="c16cf-147">Crie o índice e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c16cf-147">Build the index and run the application</span></span>
1. <span data-ttu-id="c16cf-148">Digite `npm run indexDocuments`.</span><span class="sxs-lookup"><span data-stu-id="c16cf-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="c16cf-149">Digite `npm run build`.</span><span class="sxs-lookup"><span data-stu-id="c16cf-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="c16cf-150">Digite `npm run start_server`.</span><span class="sxs-lookup"><span data-stu-id="c16cf-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="c16cf-151">Direcione seu navegador para `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="c16cf-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="c16cf-152">Pesquisar dados do USGS</span><span class="sxs-lookup"><span data-stu-id="c16cf-152">Search on USGS data</span></span>
<span data-ttu-id="c16cf-153">O conjunto de dados do USGS inclui registros relevantes para o estado de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="c16cf-153">The USGS data set includes records that are relevant to the state of Rhode Island.</span></span> <span data-ttu-id="c16cf-154">Se você clicar em **Pesquisar** em uma caixa de pesquisa vazia, obterá as 50 entradas principais, que é o valor padrão.</span><span class="sxs-lookup"><span data-stu-id="c16cf-154">If you click **Search** on an empty search box, you get the top 50 entries, which is the default.</span></span>

<span data-ttu-id="c16cf-155">A inserção de um termo de pesquisa fornece ao mecanismo de pesquisa algo para seguir.</span><span class="sxs-lookup"><span data-stu-id="c16cf-155">Entering a search term gives the search engine something to go on.</span></span> <span data-ttu-id="c16cf-156">Tente inserir um nome regional.</span><span class="sxs-lookup"><span data-stu-id="c16cf-156">Try entering a regional name.</span></span> <span data-ttu-id="c16cf-157">"Roger Williams" foi o primeiro governador de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="c16cf-157">"Roger Williams" was the first governor of Rhode Island.</span></span> <span data-ttu-id="c16cf-158">Vários parques, edifícios e escolas receberam seus nomes em homenagem a ele.</span><span class="sxs-lookup"><span data-stu-id="c16cf-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="c16cf-159">Você também pode tentar qualquer um destes termos:</span><span class="sxs-lookup"><span data-stu-id="c16cf-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="c16cf-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="c16cf-160">Pawtucket</span></span>
* <span data-ttu-id="c16cf-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="c16cf-161">Pembroke</span></span>
* <span data-ttu-id="c16cf-162">goose +cape</span><span class="sxs-lookup"><span data-stu-id="c16cf-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="c16cf-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c16cf-163">Next steps</span></span>
<span data-ttu-id="c16cf-164">Este é o primeiro tutorial do Azure Search com base no Node.js e no conjunto de dados do USGS.</span><span class="sxs-lookup"><span data-stu-id="c16cf-164">This is the first Azure Search tutorial based on Node.js and the USGS dataset.</span></span> <span data-ttu-id="c16cf-165">Ao longo do tempo, ampliaremos este tutorial para demonstrar outros recursos de pesquisa que talvez você queira usar em suas soluções personalizadas.</span><span class="sxs-lookup"><span data-stu-id="c16cf-165">Over time, we'll extend this tutorial to demonstrate additional search features you might want to use in your custom solutions.</span></span>

<span data-ttu-id="c16cf-166">Se você já tiver alguma experiência com a Pesquisa do Azure, use este exemplo como um trampolim para experimentar sugestões (consultas de preenchimento automático ou de digitação antecipada), filtros e navegação facetada.</span><span class="sxs-lookup"><span data-stu-id="c16cf-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="c16cf-167">Você também pode melhorar a página de resultados da pesquisa adicionando contagens e documentos em lote para que os usuários possam percorrer os resultados.</span><span class="sxs-lookup"><span data-stu-id="c16cf-167">You can also improve upon the search results page by adding counts and batching documents so that users can page through the results.</span></span>

<span data-ttu-id="c16cf-168">Ainda não conhece a Pesquisa do Azure?</span><span class="sxs-lookup"><span data-stu-id="c16cf-168">New to Azure Search?</span></span> <span data-ttu-id="c16cf-169">Recomendamos os outros tutoriais para que você compreenda o que pode criar.</span><span class="sxs-lookup"><span data-stu-id="c16cf-169">We recommend trying other tutorials to develop an understanding of what you can create.</span></span> <span data-ttu-id="c16cf-170">Visite nossa [página de documentação](https://azure.microsoft.com/documentation/services/search/) para encontrar mais recursos.</span><span class="sxs-lookup"><span data-stu-id="c16cf-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) to find more resources.</span></span> <span data-ttu-id="c16cf-171">Você também pode exibir os links em nossa [Lista de vídeos e Tutorial](search-video-demo-tutorial-list.md) para acessar mais informações.</span><span class="sxs-lookup"><span data-stu-id="c16cf-171">You can also view the links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) to access more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
