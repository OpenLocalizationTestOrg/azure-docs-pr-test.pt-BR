---
title: aaaGet iniciar a pesquisa do Azure no Node. js | Microsoft Docs
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
ms.openlocfilehash: e9c7d756c2ea191ee2a285485c90439b96aa73b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-nodejs"></a><span data-ttu-id="f8c8f-103">Introdução ao Azure Search no Node.js</span><span class="sxs-lookup"><span data-stu-id="f8c8f-103">Get started with Azure Search in Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8c8f-104">Portal</span><span class="sxs-lookup"><span data-stu-id="f8c8f-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="f8c8f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f8c8f-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="f8c8f-106">Saiba como o aplicativo que usa a pesquisa do Azure para sua experiência de pesquisa de pesquisa toobuild um Node. js personalizado.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-106">Learn how toobuild a custom Node.js search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="f8c8f-107">Este tutorial usa Olá [API de REST do serviço de pesquisa do Azure](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct Olá objetos e operações usadas neste exercício.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="f8c8f-108">Usamos [Node.js](https://Nodejs.org) e NPM, [Sublime 3 de texto](http://www.sublimetext.com/3)e o Windows PowerShell no Windows 8.1 toodevelop e testar esse código.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-108">We used [Node.js](https://Nodejs.org) and NPM, [Sublime Text 3](http://www.sublimetext.com/3), and Windows PowerShell on Windows 8.1 toodevelop and test this code.</span></span>

<span data-ttu-id="f8c8f-109">toorun neste exemplo, você deve ter um serviço de pesquisa do Azure, que pode inscrever-se em Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f8c8f-109">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f8c8f-110">Consulte [criar um serviço de pesquisa do Azure no portal de saudação](search-create-service-portal.md) para obter instruções passo a passo.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-110">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

## <a name="about-hello-data"></a><span data-ttu-id="f8c8f-111">Sobre dados saudação</span><span class="sxs-lookup"><span data-stu-id="f8c8f-111">About hello data</span></span>
<span data-ttu-id="f8c8f-112">Este aplicativo de exemplo usa dados da saudação [dos Estados Unidos geológica serviços (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtrado no tamanho do conjunto de dados do hello estado de Rhode Island tooreduce hello.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-112">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="f8c8f-113">Vamos usar essa toobuild dados um aplicativo de pesquisa que retorna as construções de pontos de referência, como escolas e hospitais, bem como recursos geológica como fluxos, Lagos e Cúpulas.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-113">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="f8c8f-114">Neste aplicativo, Olá **DataIndexer** programa cria e carrega Olá índice usando um [indexador](https://msdn.microsoft.com/library/azure/dn798918.aspx) construção, recuperando Olá filtrados USGS conjunto de dados de um banco de dados do SQL Azure público.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-114">In this application, hello **DataIndexer** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="f8c8f-115">Conexão e credenciais de fonte de dados online toohello informações é fornecido no código do programa hello.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-115">Credentials and connection information toohello online data source is provided in hello program code.</span></span> <span data-ttu-id="f8c8f-116">Nenhuma configuração adicional é necessária.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-116">No further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="f8c8f-117">Aplicamos um filtro em toostay este conjunto de dados abaixo do limite de documento 10.000 Olá de saudação livre de camada de preços.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-117">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="f8c8f-118">Se você usar a camada padrão hello, esse limite não se aplica.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-118">If you use hello standard tier, this limit does not apply.</span></span> <span data-ttu-id="f8c8f-119">Para obter detalhes sobre a capacidade de cada tipo de preço, consulte [Limites de serviço da Pesquisa](search-limits-quotas-capacity.md).</span><span class="sxs-lookup"><span data-stu-id="f8c8f-119">For details about capacity for each pricing tier, see [Search service limits](search-limits-quotas-capacity.md).</span></span>
> 
> 

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="f8c8f-120">Localizar o nome do serviço hello e chave de api do serviço de pesquisa do Azure</span><span class="sxs-lookup"><span data-stu-id="f8c8f-120">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="f8c8f-121">Depois de criar serviço hello, retorne toohello tooget portal Olá URL ou `api-key`.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-121">After you create hello service, return toohello portal tooget hello URL or `api-key`.</span></span> <span data-ttu-id="f8c8f-122">Conexões tooyour serviço de pesquisa requer que você tenha ambas as URLs de saudação e um `api-key` tooauthenticate chamada de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-122">Connections tooyour Search service require that you have both hello URL and an `api-key` tooauthenticate hello call.</span></span>

1. <span data-ttu-id="f8c8f-123">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f8c8f-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f8c8f-124">Na barra de salto hello, clique em **serviço de pesquisa** toolist todos os serviços de pesquisa do Azure provisionados para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-124">In hello jump bar, click **Search service** toolist all Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="f8c8f-125">Selecione serviço Olá toouse desejado.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-125">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="f8c8f-126">No painel de serviço hello, você deverá ver blocos de informações essenciais, como o ícone de chave Olá para acessar as chaves de administração de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-126">On hello service dashboard, you should see tiles for essential information, such as hello key icon for accessing hello admin keys.</span></span>
5. <span data-ttu-id="f8c8f-127">Copie a URL do serviço hello, uma chave de administração e uma chave de consulta.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-127">Copy hello service URL, an admin key, and a query key.</span></span> <span data-ttu-id="f8c8f-128">Você precisa todos os três posteriormente quando você adicioná-las toohello config.js arquivo.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-128">You need all three later when you add them toohello config.js file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="f8c8f-129">Baixar arquivos de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="f8c8f-129">Download hello sample files</span></span>
<span data-ttu-id="f8c8f-130">Use um dos Olá exemplo de hello toodownload abordagens a seguir.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-130">Use either one of hello following approaches toodownload hello sample.</span></span>

1. <span data-ttu-id="f8c8f-131">Vá muito[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span><span class="sxs-lookup"><span data-stu-id="f8c8f-131">Go too[AzureSearchNodeJSIndexerDemo](https://github.com/AzureSearch/AzureSearchNodejsIndexerDemo).</span></span>
2. <span data-ttu-id="f8c8f-132">Clique em **baixar ZIP**, salve o arquivo. zip de saudação e, em seguida, extraia todos os arquivos de saudação nele.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-132">Click **Download ZIP**, save hello .zip file, and then extract all hello files it contains.</span></span>

<span data-ttu-id="f8c8f-133">Todas as modificações de arquivos posteriores e instruções de execução serão feitas nos arquivos nessa pasta.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-133">All subsequent file modifications and run statements are made against files in this folder.</span></span>

## <a name="update-hello-configjs-with-your-search-service-url-and-api-key"></a><span data-ttu-id="f8c8f-134">Atualize config.js hello.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-134">Update hello config.js.</span></span> <span data-ttu-id="f8c8f-135">com a URL e a chave de api do serviço Pesquisa</span><span class="sxs-lookup"><span data-stu-id="f8c8f-135">with your Search service URL and api-key</span></span>
<span data-ttu-id="f8c8f-136">Usando Olá URL e a chave de api que você copiou anteriormente, especifique a URL de hello, chave de administração e a chave de consulta no arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-136">Using hello URL and api-key that you copied earlier, specify hello URL, admin-key, and query-key in configuration file.</span></span>

<span data-ttu-id="f8c8f-137">As chaves de administrador oferecem controle total sobre as operações do serviço, incluindo a criação ou exclusão de um índice e carregamento de documentos.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-137">Admin keys grant full control over service operations, including creating or deleting an index and loading documents.</span></span> <span data-ttu-id="f8c8f-138">Em contraste, as chaves de consulta são para operações somente leitura, normalmente usadas por aplicativos cliente que se conectam tooAzure pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-138">In contrast, query keys are for read-only operations, typically used by client applications that connect tooAzure Search.</span></span>

<span data-ttu-id="f8c8f-139">Neste exemplo, nós incluímos consulta Olá toohelp chave reforçar a prática recomendada de saudação do uso de chave de consulta Olá em aplicativos cliente.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-139">In this sample, we include hello query key toohelp reinforce hello best practice of using hello query key in client applications.</span></span>

<span data-ttu-id="f8c8f-140">Olá captura de tela mostra a seguir **config.js** aberto em um editor de texto com hello entradas relevantes delimitadas para que você possa ver onde o arquivo hello tooupdate Olá valores que são válidas para o serviço de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-140">hello following screenshot shows **config.js** open in a text editor, with hello relevant entries demarcated so that you can see where tooupdate hello file with hello values that are valid for your search service.</span></span>

![][5]

## <a name="host-a-runtime-environment-for-hello-sample"></a><span data-ttu-id="f8c8f-141">Host de um ambiente de tempo de execução para o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="f8c8f-141">Host a runtime environment for hello sample</span></span>
<span data-ttu-id="f8c8f-142">exemplo Hello requer um servidor HTTP, que pode ser instalado usando globalmente npm.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-142">hello sample requires an HTTP server, which you can install globally using npm.</span></span>

<span data-ttu-id="f8c8f-143">Use uma janela do PowerShell para Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-143">Use a PowerShell window for hello following commands.</span></span>

1. <span data-ttu-id="f8c8f-144">Navegue toohello pasta que contém a saudação **Package. JSON** arquivo.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-144">Navigate toohello folder that contains hello **package.json** file.</span></span>
2. <span data-ttu-id="f8c8f-145">Digite `npm install`.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-145">Type `npm install`.</span></span>
3. <span data-ttu-id="f8c8f-146">Digite `npm install -g http-server`.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-146">Type `npm install -g http-server`.</span></span>

## <a name="build-hello-index-and-run-hello-application"></a><span data-ttu-id="f8c8f-147">Criar índice hello e executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="f8c8f-147">Build hello index and run hello application</span></span>
1. <span data-ttu-id="f8c8f-148">Digite `npm run indexDocuments`.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-148">Type `npm run indexDocuments`.</span></span>
2. <span data-ttu-id="f8c8f-149">Digite `npm run build`.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-149">Type `npm run build`.</span></span>
3. <span data-ttu-id="f8c8f-150">Digite `npm run start_server`.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-150">Type `npm run start_server`.</span></span>
4. <span data-ttu-id="f8c8f-151">Direcione seu navegador para `http://localhost:8080/index.html`</span><span class="sxs-lookup"><span data-stu-id="f8c8f-151">Direct your browser at `http://localhost:8080/index.html`</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="f8c8f-152">Pesquisar dados do USGS</span><span class="sxs-lookup"><span data-stu-id="f8c8f-152">Search on USGS data</span></span>
<span data-ttu-id="f8c8f-153">conjunto de dados USGS Olá inclui registros que são relevante toohello estado de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-153">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="f8c8f-154">Se você clicar em **pesquisa** em uma caixa de pesquisa vazia, você obter entradas de 50 principais hello, que é o padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-154">If you click **Search** on an empty search box, you get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="f8c8f-155">Inserindo um termo de pesquisa fornece o mecanismo de pesquisa Olá algo toogo em.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-155">Entering a search term gives hello search engine something toogo on.</span></span> <span data-ttu-id="f8c8f-156">Tente inserir um nome regional.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-156">Try entering a regional name.</span></span> <span data-ttu-id="f8c8f-157">"Roger Williams" era o administrador primeiro Olá de Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-157">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="f8c8f-158">Vários parques, edifícios e escolas receberam seus nomes em homenagem a ele.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-158">Numerous parks, buildings, and schools are named after him.</span></span>

![][9]

<span data-ttu-id="f8c8f-159">Você também pode tentar qualquer um destes termos:</span><span class="sxs-lookup"><span data-stu-id="f8c8f-159">You could also try any of these terms:</span></span>

* <span data-ttu-id="f8c8f-160">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="f8c8f-160">Pawtucket</span></span>
* <span data-ttu-id="f8c8f-161">Pembroke</span><span class="sxs-lookup"><span data-stu-id="f8c8f-161">Pembroke</span></span>
* <span data-ttu-id="f8c8f-162">goose +cape</span><span class="sxs-lookup"><span data-stu-id="f8c8f-162">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8c8f-163">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f8c8f-163">Next steps</span></span>
<span data-ttu-id="f8c8f-164">Este é o hello primeiro tutorial de pesquisa do Azure com base em Node. js e hello USGS dataset.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-164">This is hello first Azure Search tutorial based on Node.js and hello USGS dataset.</span></span> <span data-ttu-id="f8c8f-165">Ao longo do tempo, estenderemos esse tutorial toodemonstrate recursos adicionais de pesquisa convém toouse em suas soluções personalizadas.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-165">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="f8c8f-166">Se você já tiver alguma experiência com a Pesquisa do Azure, use este exemplo como um trampolim para experimentar sugestões (consultas de preenchimento automático ou de digitação antecipada), filtros e navegação facetada.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-166">If you already have some background in Azure Search, you can use this sample as a springboard for trying suggesters (type-ahead or autocomplete queries), filters, and faceted navigation.</span></span> <span data-ttu-id="f8c8f-167">Você também pode melhorar após a página de resultados da pesquisa de saudação adicionando contagens e envio em lote documentos para que os usuários podem percorrer resultados hello.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-167">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="f8c8f-168">TooAzure nova pesquisa?</span><span class="sxs-lookup"><span data-stu-id="f8c8f-168">New tooAzure Search?</span></span> <span data-ttu-id="f8c8f-169">É recomendável tentar toodevelop outros tutoriais um entendimento de como você pode criar.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-169">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="f8c8f-170">Visite nosso [página de documentação](https://azure.microsoft.com/documentation/services/search/) toofind mais recursos.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-170">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="f8c8f-171">Você também pode exibir links Olá em nosso [vídeo e Tutorial lista](search-video-demo-tutorial-list.md) tooaccess obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="f8c8f-171">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-Nodejs/create-search-portal-1.PNG
[2]: ./media/search-get-started-Nodejs/create-search-portal-2.PNG
[3]: ./media/search-get-started-Nodejs/create-search-portal-3.PNG
[5]: ./media/search-get-started-Nodejs/AzSearch-Nodejs-configjs.png
[9]: ./media/search-get-started-Nodejs/rogerwilliamsschool.png
