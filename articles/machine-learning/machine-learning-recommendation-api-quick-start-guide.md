---
title: "Início Rápido: API de Recomendações do Azure Machine Learning (versão 1)| Microsoft Docs"
description: "Recomendações do Azure Machine Learning - guia de início rápido"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 5bce1a4a-1ad6-473f-812b-84f800fdc09a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 0a9d0b6aa1ef734a857ecc16777ba6250909b38d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="quick-start-guide-for-the-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="63309-104">Guia de início rápido para a API de Recomendações do Machine Learning (versão 1)</span><span class="sxs-lookup"><span data-stu-id="63309-104">Quick start guide for the Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="63309-105">Você deve começar usando o [Serviço Cognitivo da API de Recomendações](https://www.microsoft.com/cognitive-services/recommendations-api) em vez desta versão.</span><span class="sxs-lookup"><span data-stu-id="63309-105">You should start using the [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="63309-106">O Serviço Cognitivo de Recomendações substituirá esse serviço, e todos os recursos novos serão desenvolvidos lá.</span><span class="sxs-lookup"><span data-stu-id="63309-106">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="63309-107">Ele possui novos recursos como suporte ao processamento em lotes, um Gerenciador de API aprimorado, uma superfície de API mais limpa, uma experiência de inscrição/cobrança mais consistente etc.</span><span class="sxs-lookup"><span data-stu-id="63309-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="63309-108">Saiba mais sobre [Como migrar para o novo Serviço Cognitivo](http://aka.ms/recomigrate).</span><span class="sxs-lookup"><span data-stu-id="63309-108">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="63309-109">Este documento descreve como integrar o seu serviço ou aplicativo para usar as Recomendações do Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="63309-109">This document describes how to onboard your service or application to use Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="63309-110">Encontre mais detalhes sobre a API de Recomendações na [Galeria do Cortana Intelligence](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="63309-110">You can find more details on the Recommendations API in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="63309-111">Visão geral</span><span class="sxs-lookup"><span data-stu-id="63309-111">General overview</span></span>
<span data-ttu-id="63309-112">Para usar as Recomendações de Azure Machine Learning, você precisa executar as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="63309-112">To use Azure Machine Learning Recommendations, you need to take the following steps:</span></span>

* <span data-ttu-id="63309-113">Criar um modelo – um modelo é um contêiner de seus dados de uso, dados do catálogo e o modelo de recomendação.</span><span class="sxs-lookup"><span data-stu-id="63309-113">Create a model - A model is a container of your usage data, catalog data, and the recommendation model.</span></span>
* <span data-ttu-id="63309-114">Importar dados do catálogo - Um catálogo contém informações de metadados sobre os itens.</span><span class="sxs-lookup"><span data-stu-id="63309-114">Import catalog data - A catalog contains metadata information on the items.</span></span> 
* <span data-ttu-id="63309-115">Importar dados de uso: os dados de uso podem ser carregados de uma entre duas maneiras (ou ambas):</span><span class="sxs-lookup"><span data-stu-id="63309-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="63309-116">Carregando um arquivo que contém os dados de uso.</span><span class="sxs-lookup"><span data-stu-id="63309-116">By uploading a file that contains the usage data.</span></span>
  * <span data-ttu-id="63309-117">Enviando eventos de aquisição de dados.</span><span class="sxs-lookup"><span data-stu-id="63309-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="63309-118">Normalmente, você carrega um arquivo de uso para poder criar um modelo de recomendação inicial (inicialização) e usá-lo até que o sistema reúna dados suficientes usando o formato de aquisição de dados.</span><span class="sxs-lookup"><span data-stu-id="63309-118">Usually you upload a usage file in order to be able to create an initial recommendation model (bootstrap) and use it until the system gathers enough data by using the data acquisition format.</span></span>
* <span data-ttu-id="63309-119">Criar um modelo de recomendação – Esta é uma operação assíncrona, em que o sistema de recomendação emprega todos os dados de uso e cria um modelo de recomendação.</span><span class="sxs-lookup"><span data-stu-id="63309-119">Build a recommendation model - This is an asynchronous operation in which the recommendation system takes all the usage data and creates a recommendation model.</span></span> <span data-ttu-id="63309-120">Essa operação pode levar vários minutos ou várias horas, dependendo do tamanho dos dados e dos parâmetros de configuração da compilação.</span><span class="sxs-lookup"><span data-stu-id="63309-120">This operation can take several minutes or several hours depending on the size of the data and the build configuration parameters.</span></span> <span data-ttu-id="63309-121">Ao disparar a compilação, você receberá uma ID de compilação.</span><span class="sxs-lookup"><span data-stu-id="63309-121">When triggering the build, you will get a build ID.</span></span> <span data-ttu-id="63309-122">Use-o para verificar quando o processo de compilação foi concluído antes de começar a consumir recomendações.</span><span class="sxs-lookup"><span data-stu-id="63309-122">Use it to check when the build process has ended before starting to consume recommendations.</span></span>
* <span data-ttu-id="63309-123">Consumir recomendações - Obtenha recomendações para um item específico ou uma lista de itens.</span><span class="sxs-lookup"><span data-stu-id="63309-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="63309-124">Todas as etapas acima são feitas por meio da API de Recomendações do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="63309-124">All the steps above are done through the Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="63309-125">Você pode baixar um aplicativo de exemplo que implementa cada uma dessas etapas da [galeria também.](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="63309-125">You can download a sample application that implements each of these steps from the [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="63309-126">Limitações</span><span class="sxs-lookup"><span data-stu-id="63309-126">Limitations</span></span>
* <span data-ttu-id="63309-127">O número máximo de modelos por assinatura é 10.</span><span class="sxs-lookup"><span data-stu-id="63309-127">The maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="63309-128">O número máximo de itens que um catálogo pode conter é 100.000.</span><span class="sxs-lookup"><span data-stu-id="63309-128">The maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="63309-129">O número máximo de pontos de uso mantidos é cerca de 5.000.000.</span><span class="sxs-lookup"><span data-stu-id="63309-129">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="63309-130">Os mais antigos serão excluídos se novos forem carregados ou relatados.</span><span class="sxs-lookup"><span data-stu-id="63309-130">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="63309-131">O volume máximo dos dados que podem ser enviado no POST (por exemplo, importar dados de catálogo e importar dados de uso) é de 200 MB.</span><span class="sxs-lookup"><span data-stu-id="63309-131">The maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="63309-132">O número de transações por segundo para uma compilação de modelo de recomendação que não está ativa é cerca de 2 TPS.</span><span class="sxs-lookup"><span data-stu-id="63309-132">The number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="63309-133">Uma compilação de modelo de recomendação ativo pode conter até 20 TPS.</span><span class="sxs-lookup"><span data-stu-id="63309-133">A recommendation model build that is active can hold up to 20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="63309-134">Integração</span><span class="sxs-lookup"><span data-stu-id="63309-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="63309-135">Autenticação</span><span class="sxs-lookup"><span data-stu-id="63309-135">Authentication</span></span>
<span data-ttu-id="63309-136">O Microsoft Azure Marketplace dá suporte ao método de autenticação Básico ou OAuth.</span><span class="sxs-lookup"><span data-stu-id="63309-136">Microsoft Azure Marketplace supports either the Basic or OAuth authentication method.</span></span> <span data-ttu-id="63309-137">Você pode localizar facilmente as chaves de conta, navegando até as chaves no marketplace [nas configurações da conta](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="63309-137">You can easily find the account keys by navigating to the keys in the marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="63309-138">Autenticação básica</span><span class="sxs-lookup"><span data-stu-id="63309-138">Basic Authentication</span></span>
<span data-ttu-id="63309-139">Adicione o cabeçalho de autorização:</span><span class="sxs-lookup"><span data-stu-id="63309-139">Add the Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="63309-140">Converta em Base64 (c#)</span><span class="sxs-lookup"><span data-stu-id="63309-140">Convert to Base64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="63309-141">Converta em Base64 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="63309-141">Convert to Base64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="63309-142">URI de serviço</span><span class="sxs-lookup"><span data-stu-id="63309-142">Service URI</span></span>
<span data-ttu-id="63309-143">O URI da raiz de serviço para as APIs de Recomendações do Azure Machine Learning está [aqui.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="63309-143">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="63309-144">O URI do serviço completo é expresso usando elementos da especificação de OData.</span><span class="sxs-lookup"><span data-stu-id="63309-144">The full service URI is expressed using elements of the OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="63309-145">Versão da API</span><span class="sxs-lookup"><span data-stu-id="63309-145">API version</span></span>
<span data-ttu-id="63309-146">Cada chamada à API terá, por fim, um parâmetro de consulta chamado apiVersion que deve ser definido como “1.0”.</span><span class="sxs-lookup"><span data-stu-id="63309-146">Each API call will have, at the end, a query parameter called apiVersion that should be set to "1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="63309-147">IDs diferenciam minúsculas e maiúsculas</span><span class="sxs-lookup"><span data-stu-id="63309-147">IDs are case-sensitive</span></span>
<span data-ttu-id="63309-148">IDs, retornados por qualquer uma das APIS, diferenciam minúsculas de maiúsculas e devem ser usados desta maneira quando passados como parâmetros nas chamadas de API subsequentes.</span><span class="sxs-lookup"><span data-stu-id="63309-148">IDs, returned by any of the APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="63309-149">Por exemplo, IDS de modelo e de catálogo diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="63309-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="63309-150">Criar um modelo</span><span class="sxs-lookup"><span data-stu-id="63309-150">Create a model</span></span>
<span data-ttu-id="63309-151">Criando uma solicitação para "criar modelo":</span><span class="sxs-lookup"><span data-stu-id="63309-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="63309-152">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="63309-152">HTTP Method</span></span> | <span data-ttu-id="63309-153">URI</span><span class="sxs-lookup"><span data-stu-id="63309-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="63309-154">POST</span><span class="sxs-lookup"><span data-stu-id="63309-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="63309-155">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="63309-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="63309-156">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="63309-156">Parameter Name</span></span> | <span data-ttu-id="63309-157">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="63309-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="63309-158">modelName</span><span class="sxs-lookup"><span data-stu-id="63309-158">modelName</span></span> |<span data-ttu-id="63309-159">São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).</span><span class="sxs-lookup"><span data-stu-id="63309-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="63309-160">Comprimento máximo: 20</span><span class="sxs-lookup"><span data-stu-id="63309-160">Max length: 20</span></span> |
| <span data-ttu-id="63309-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="63309-161">apiVersion</span></span> |<span data-ttu-id="63309-162">1.0</span><span class="sxs-lookup"><span data-stu-id="63309-162">1.0</span></span> |
|  | |
| <span data-ttu-id="63309-163">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="63309-163">Request Body</span></span> |<span data-ttu-id="63309-164">NENHUM</span><span class="sxs-lookup"><span data-stu-id="63309-164">NONE</span></span> |

<span data-ttu-id="63309-165">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="63309-165">**Response**:</span></span>

<span data-ttu-id="63309-166">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="63309-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="63309-167">`feed/entry/content/properties/id` – Contém a ID do modelo.</span><span class="sxs-lookup"><span data-stu-id="63309-167">`feed/entry/content/properties/id` - Contains the model ID.</span></span>
  <span data-ttu-id="63309-168">Lembre-se que a ID do modelo diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="63309-168">Note that the model ID is case-sensitive.</span></span>

<span data-ttu-id="63309-169">XML de OData</span><span class="sxs-lookup"><span data-stu-id="63309-169">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">a658c626-2baa-43a7-ac98-f6ee26120a12</d:Id>
        <d:Name m:type="Edm.String">MyFirstModel</d:Name>
        <d:Date m:type="Edm.String">10/5/2014 6:35:19 AM</d:Date>
        <d:Status m:type="Edm.String">Created</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:UserName>
        <d:Description m:type="Edm.String"></d:Description>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-catalog-data"></a><span data-ttu-id="63309-170">Importar dados de catálogo</span><span class="sxs-lookup"><span data-stu-id="63309-170">Import catalog data</span></span>
<span data-ttu-id="63309-171">Se você carregar vários arquivos de catálogo para o mesmo modelo com várias chamadas, inseriremos apenas os novos itens de catálogo.</span><span class="sxs-lookup"><span data-stu-id="63309-171">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span></span> <span data-ttu-id="63309-172">Os itens existentes permanecerão com os valores originais.</span><span class="sxs-lookup"><span data-stu-id="63309-172">Existing items will remain with the original values.</span></span>

| <span data-ttu-id="63309-173">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="63309-173">HTTP Method</span></span> | <span data-ttu-id="63309-174">URI</span><span class="sxs-lookup"><span data-stu-id="63309-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="63309-175">POST</span><span class="sxs-lookup"><span data-stu-id="63309-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="63309-176">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="63309-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="63309-177">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="63309-177">Parameter Name</span></span> | <span data-ttu-id="63309-178">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="63309-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="63309-179">modelId</span><span class="sxs-lookup"><span data-stu-id="63309-179">modelId</span></span> |<span data-ttu-id="63309-180">O identificador exclusivo do modelo (diferencia maiúsculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="63309-180">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="63309-181">nome do arquivo</span><span class="sxs-lookup"><span data-stu-id="63309-181">filename</span></span> |<span data-ttu-id="63309-182">Identificador textual do catálogo.</span><span class="sxs-lookup"><span data-stu-id="63309-182">Textual identifier of the catalog.</span></span><br><span data-ttu-id="63309-183">São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).</span><span class="sxs-lookup"><span data-stu-id="63309-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="63309-184">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="63309-184">Max length: 50</span></span> |
| <span data-ttu-id="63309-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="63309-185">apiVersion</span></span> |<span data-ttu-id="63309-186">1.0</span><span class="sxs-lookup"><span data-stu-id="63309-186">1.0</span></span> |
|  | |
| <span data-ttu-id="63309-187">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="63309-187">Request Body</span></span> |<span data-ttu-id="63309-188">Dados de catálogo.</span><span class="sxs-lookup"><span data-stu-id="63309-188">Catalog data.</span></span> <span data-ttu-id="63309-189">Formato:</span><span class="sxs-lookup"><span data-stu-id="63309-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="63309-190">Nome</span><span class="sxs-lookup"><span data-stu-id="63309-190">Name</span></span></th><th><span data-ttu-id="63309-191">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="63309-191">Mandatory</span></span></th><th><span data-ttu-id="63309-192">Tipo</span><span class="sxs-lookup"><span data-stu-id="63309-192">Type</span></span></th><th><span data-ttu-id="63309-193">Descrição</span><span class="sxs-lookup"><span data-stu-id="63309-193">Description</span></span></th></tr><tr><td><span data-ttu-id="63309-194">Id do item</span><span class="sxs-lookup"><span data-stu-id="63309-194">Item Id</span></span></td><td><span data-ttu-id="63309-195">Sim</span><span class="sxs-lookup"><span data-stu-id="63309-195">Yes</span></span></td><td><span data-ttu-id="63309-196">Alfanumérico, comprimento máximo 50</span><span class="sxs-lookup"><span data-stu-id="63309-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="63309-197">Identificador exclusivo de um item</span><span class="sxs-lookup"><span data-stu-id="63309-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="63309-198">Nome do Item</span><span class="sxs-lookup"><span data-stu-id="63309-198">Item Name</span></span></td><td><span data-ttu-id="63309-199">Sim</span><span class="sxs-lookup"><span data-stu-id="63309-199">Yes</span></span></td><td><span data-ttu-id="63309-200">Alfanumérico, comprimento máximo 255</span><span class="sxs-lookup"><span data-stu-id="63309-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="63309-201">Nome do item</span><span class="sxs-lookup"><span data-stu-id="63309-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="63309-202">Categoria do Item</span><span class="sxs-lookup"><span data-stu-id="63309-202">Item Category</span></span></td><td><span data-ttu-id="63309-203">Sim</span><span class="sxs-lookup"><span data-stu-id="63309-203">Yes</span></span></td><td><span data-ttu-id="63309-204">Alfanumérico, comprimento máximo 255</span><span class="sxs-lookup"><span data-stu-id="63309-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="63309-205">Categoria à qual este item pertence (por exemplo, Livros de Culinária, Drama...)</span><span class="sxs-lookup"><span data-stu-id="63309-205">Category to which this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="63309-206">Descrição</span><span class="sxs-lookup"><span data-stu-id="63309-206">Description</span></span></td><td><span data-ttu-id="63309-207">Não</span><span class="sxs-lookup"><span data-stu-id="63309-207">No</span></span></td><td><span data-ttu-id="63309-208">Alfanumérico, comprimento máximo 4000</span><span class="sxs-lookup"><span data-stu-id="63309-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="63309-209">Descrição deste item</span><span class="sxs-lookup"><span data-stu-id="63309-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="63309-210">O tamanho máximo do arquivo é de 200 MB.</span><span class="sxs-lookup"><span data-stu-id="63309-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="63309-211">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="63309-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="63309-212">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="63309-212">**Response**:</span></span>

<span data-ttu-id="63309-213">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="63309-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="63309-214">`Feed\entry\content\properties\LineCount` – O número de linhas aceitas.</span><span class="sxs-lookup"><span data-stu-id="63309-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="63309-215">`Feed\entry\content\properties\ErrorCount` – O número de linhas que não foram inseridas devido a um erro.</span><span class="sxs-lookup"><span data-stu-id="63309-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>

<span data-ttu-id="63309-216">XML de OData</span><span class="sxs-lookup"><span data-stu-id="63309-216">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
          <subtitle type="text">Import catalog file</subtitle>
          <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:58:04Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">ImportCatalogFileEntity2</title>
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">4</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
      </m:properties>
    </content>
      </entry>
    </feed>


### <a name="import-usage-data"></a><span data-ttu-id="63309-217">Importar dados de uso</span><span class="sxs-lookup"><span data-stu-id="63309-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="63309-218">Carregar um arquivo</span><span class="sxs-lookup"><span data-stu-id="63309-218">Uploading a file</span></span>
<span data-ttu-id="63309-219">Esta seção mostra como carregar dados de uso usando um arquivo.</span><span class="sxs-lookup"><span data-stu-id="63309-219">This section shows how to upload usage data by using a file.</span></span> <span data-ttu-id="63309-220">Você pode chamar essa API várias vezes com dados de uso.</span><span class="sxs-lookup"><span data-stu-id="63309-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="63309-221">Todos os dados de uso serão salvos para todas as chamadas.</span><span class="sxs-lookup"><span data-stu-id="63309-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="63309-222">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="63309-222">HTTP Method</span></span> | <span data-ttu-id="63309-223">URI</span><span class="sxs-lookup"><span data-stu-id="63309-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="63309-224">POST</span><span class="sxs-lookup"><span data-stu-id="63309-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="63309-225">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="63309-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="63309-226">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="63309-226">Parameter Name</span></span> | <span data-ttu-id="63309-227">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="63309-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="63309-228">modelId</span><span class="sxs-lookup"><span data-stu-id="63309-228">modelId</span></span> |<span data-ttu-id="63309-229">O identificador exclusivo do modelo (diferencia maiúsculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="63309-229">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="63309-230">nome do arquivo</span><span class="sxs-lookup"><span data-stu-id="63309-230">filename</span></span> |<span data-ttu-id="63309-231">Identificador textual do catálogo.</span><span class="sxs-lookup"><span data-stu-id="63309-231">Textual identifier of the catalog.</span></span><br><span data-ttu-id="63309-232">São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).</span><span class="sxs-lookup"><span data-stu-id="63309-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="63309-233">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="63309-233">Max length: 50</span></span> |
| <span data-ttu-id="63309-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="63309-234">apiVersion</span></span> |<span data-ttu-id="63309-235">1.0</span><span class="sxs-lookup"><span data-stu-id="63309-235">1.0</span></span> |
|  | |
| <span data-ttu-id="63309-236">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="63309-236">Request Body</span></span> |<span data-ttu-id="63309-237">Dados de uso.</span><span class="sxs-lookup"><span data-stu-id="63309-237">Usage data.</span></span> <span data-ttu-id="63309-238">Formato:</span><span class="sxs-lookup"><span data-stu-id="63309-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="63309-239">Nome</span><span class="sxs-lookup"><span data-stu-id="63309-239">Name</span></span></th><th><span data-ttu-id="63309-240">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="63309-240">Mandatory</span></span></th><th><span data-ttu-id="63309-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="63309-241">Type</span></span></th><th><span data-ttu-id="63309-242">Descrição</span><span class="sxs-lookup"><span data-stu-id="63309-242">Description</span></span></th></tr><tr><td><span data-ttu-id="63309-243">Id de usuário</span><span class="sxs-lookup"><span data-stu-id="63309-243">User Id</span></span></td><td><span data-ttu-id="63309-244">Sim</span><span class="sxs-lookup"><span data-stu-id="63309-244">Yes</span></span></td><td><span data-ttu-id="63309-245">Alfanumérico</span><span class="sxs-lookup"><span data-stu-id="63309-245">Alphanumeric</span></span></td><td><span data-ttu-id="63309-246">Identificador exclusivo de um usuário</span><span class="sxs-lookup"><span data-stu-id="63309-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="63309-247">Id do item</span><span class="sxs-lookup"><span data-stu-id="63309-247">Item Id</span></span></td><td><span data-ttu-id="63309-248">Sim</span><span class="sxs-lookup"><span data-stu-id="63309-248">Yes</span></span></td><td><span data-ttu-id="63309-249">Alfanumérico, comprimento máximo 50</span><span class="sxs-lookup"><span data-stu-id="63309-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="63309-250">Identificador exclusivo de um item</span><span class="sxs-lookup"><span data-stu-id="63309-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="63309-251">Hora</span><span class="sxs-lookup"><span data-stu-id="63309-251">Time</span></span></td><td><span data-ttu-id="63309-252">Não</span><span class="sxs-lookup"><span data-stu-id="63309-252">No</span></span></td><td><span data-ttu-id="63309-253">Data no formato: AAAA/MM/DDTHH:MM:SS (por exemplo, 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="63309-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="63309-254">Hora dos dados</span><span class="sxs-lookup"><span data-stu-id="63309-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="63309-255">Evento</span><span class="sxs-lookup"><span data-stu-id="63309-255">Event</span></span></td><td><span data-ttu-id="63309-256">Não, se fornecido, também deve colocar a data</span><span class="sxs-lookup"><span data-stu-id="63309-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="63309-257">Um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="63309-257">One of the following:</span></span><br><span data-ttu-id="63309-258">• Clique</span><span class="sxs-lookup"><span data-stu-id="63309-258">• Click</span></span><br><span data-ttu-id="63309-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="63309-259">• RecommendationClick</span></span><br><span data-ttu-id="63309-260">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="63309-260">•    AddShopCart</span></span><br><span data-ttu-id="63309-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="63309-261">• RemoveShopCart</span></span><br><span data-ttu-id="63309-262">• Compra</span><span class="sxs-lookup"><span data-stu-id="63309-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="63309-263">O tamanho máximo do arquivo é de 200 MB.</span><span class="sxs-lookup"><span data-stu-id="63309-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="63309-264">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="63309-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="63309-265">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="63309-265">**Response**:</span></span>

<span data-ttu-id="63309-266">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="63309-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="63309-267">`Feed\entry\content\properties\LineCount` – O número de linhas aceitas.</span><span class="sxs-lookup"><span data-stu-id="63309-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="63309-268">`Feed\entry\content\properties\ErrorCount` – O número de linhas que não foram inseridas devido a um erro.</span><span class="sxs-lookup"><span data-stu-id="63309-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>
* <span data-ttu-id="63309-269">`Feed\entry\content\properties\FileId` – Identificador do arquivo.</span><span class="sxs-lookup"><span data-stu-id="63309-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="63309-270">XML de OData</span><span class="sxs-lookup"><span data-stu-id="63309-270">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="using-data-acquisition"></a><span data-ttu-id="63309-271">Usando a aquisição de dados</span><span class="sxs-lookup"><span data-stu-id="63309-271">Using data acquisition</span></span>
<span data-ttu-id="63309-272">Esta seção mostra como enviar eventos em tempo real para as Recomendações do Azure Machine Learning, geralmente do seu site.</span><span class="sxs-lookup"><span data-stu-id="63309-272">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="63309-273">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="63309-273">HTTP Method</span></span> | <span data-ttu-id="63309-274">URI</span><span class="sxs-lookup"><span data-stu-id="63309-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="63309-275">POST</span><span class="sxs-lookup"><span data-stu-id="63309-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="63309-276">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="63309-276">Parameter Name</span></span> | <span data-ttu-id="63309-277">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="63309-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="63309-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="63309-278">apiVersion</span></span> |<span data-ttu-id="63309-279">1.0</span><span class="sxs-lookup"><span data-stu-id="63309-279">1.0</span></span> |
|  | |
| <span data-ttu-id="63309-280">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="63309-280">Request body</span></span> |<span data-ttu-id="63309-281">Entrada de dados de evento para cada evento que você deseja enviar.</span><span class="sxs-lookup"><span data-stu-id="63309-281">Event data entry for each event you want to send.</span></span> <span data-ttu-id="63309-282">Você deve enviar a mesma ID no campo SessionId para a mesma sessão de usuário ou navegador.</span><span class="sxs-lookup"><span data-stu-id="63309-282">You should send for the same user or browser session the same ID in the SessionId field.</span></span> <span data-ttu-id="63309-283">(Consulte o exemplo de corpo de evento abaixo.)</span><span class="sxs-lookup"><span data-stu-id="63309-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="63309-284">Exemplo de evento “Click”:</span><span class="sxs-lookup"><span data-stu-id="63309-284">Example for event 'Click':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
        <Name>Click</Name>
        <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="63309-285">Exemplo de evento “RecommendationClick”:</span><span class="sxs-lookup"><span data-stu-id="63309-285">Example for event 'RecommendationClick':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RecommendationClick</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="63309-286">Exemplo de evento “AddShopCart”:</span><span class="sxs-lookup"><span data-stu-id="63309-286">Example for event 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="63309-287">Exemplo de evento “RemoveShopCart”:</span><span class="sxs-lookup"><span data-stu-id="63309-287">Example for event 'RemoveShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>RemoveShopCart</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
        </EventData>
          </EventData>
        </Event>
* <span data-ttu-id="63309-288">Exemplo de evento “Purchase”:</span><span class="sxs-lookup"><span data-stu-id="63309-288">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
        <EventData>
            <Name>Purchase</Name> 
            <PurchaseItems>
            <PurchaseItems>
                <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
                <Count>3</Count>
            </PurchaseItems>
        </PurchaseItems>
        </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="63309-289">Exemplo de envio de dois eventos “Click” e “AddShopCart”:</span><span class="sxs-lookup"><span data-stu-id="63309-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
          <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
          <SessionId>11112222</SessionId>
          <EventData>
        <EventData>
          <Name>Click</Name>
          <ItemId>21BF8088-B6C0-4509-870C-E1C7AC78304A</ItemId>
          <ItemName>itemName</ItemName>
          <ItemDescription>item description</ItemDescription>
          <ItemCategory>category</ItemCategory>
        </EventData>
        <EventData>
          <Name>AddShopCart</Name>
          <ItemId>552A1940-21E4-4399-82BB-594B46D7ED54</ItemId>
        </EventData>
          </EventData>
        </Event>

<span data-ttu-id="63309-290">**Response**: código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="63309-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="63309-291">Criar um modelo de recomendação</span><span class="sxs-lookup"><span data-stu-id="63309-291">Build a recommendation model</span></span>
| <span data-ttu-id="63309-292">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="63309-292">HTTP Method</span></span> | <span data-ttu-id="63309-293">URI</span><span class="sxs-lookup"><span data-stu-id="63309-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="63309-294">POST</span><span class="sxs-lookup"><span data-stu-id="63309-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="63309-295">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="63309-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="63309-296">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="63309-296">Parameter Name</span></span> | <span data-ttu-id="63309-297">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="63309-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="63309-298">modelId</span><span class="sxs-lookup"><span data-stu-id="63309-298">modelId</span></span> |<span data-ttu-id="63309-299">O identificador exclusivo do modelo (diferencia maiúsculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="63309-299">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="63309-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="63309-300">userDescription</span></span> |<span data-ttu-id="63309-301">Identificador textual do catálogo.</span><span class="sxs-lookup"><span data-stu-id="63309-301">Textual identifier of the catalog.</span></span> <span data-ttu-id="63309-302">Observe que se você usar espaços você deve codificá-los com 20%.</span><span class="sxs-lookup"><span data-stu-id="63309-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="63309-303">Consulte o exemplo acima.</span><span class="sxs-lookup"><span data-stu-id="63309-303">See example above.</span></span><br><span data-ttu-id="63309-304">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="63309-304">Max length: 50</span></span> |
| <span data-ttu-id="63309-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="63309-305">apiVersion</span></span> |<span data-ttu-id="63309-306">1.0</span><span class="sxs-lookup"><span data-stu-id="63309-306">1.0</span></span> |
|  | |
| <span data-ttu-id="63309-307">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="63309-307">Request Body</span></span> |<span data-ttu-id="63309-308">NENHUM</span><span class="sxs-lookup"><span data-stu-id="63309-308">NONE</span></span> |

<span data-ttu-id="63309-309">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="63309-309">**Response**:</span></span>

<span data-ttu-id="63309-310">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="63309-310">HTTP Status code: 200</span></span>

<span data-ttu-id="63309-311">Esta é uma API assíncrona.</span><span class="sxs-lookup"><span data-stu-id="63309-311">This is an asynchronous API.</span></span> <span data-ttu-id="63309-312">Você receberá uma ID de compilação como uma resposta.</span><span class="sxs-lookup"><span data-stu-id="63309-312">You will get a build ID as a response.</span></span> <span data-ttu-id="63309-313">Para saber quando a compilação foi concluída, você deve chamar a API "Obter Status de Compilações de um Modelo" e localizar a ID desta compilação na resposta.</span><span class="sxs-lookup"><span data-stu-id="63309-313">To know when the build has ended, you should call the "Get Builds Status of a Model" API and locate this build ID in the response.</span></span> <span data-ttu-id="63309-314">Observe que uma compilação pode levar de minutos a horas dependendo do tamanho dos dados.</span><span class="sxs-lookup"><span data-stu-id="63309-314">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="63309-315">Você não pode consumir recomendações até a compilação terminar.</span><span class="sxs-lookup"><span data-stu-id="63309-315">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="63309-316">Status de compilação válidos:</span><span class="sxs-lookup"><span data-stu-id="63309-316">Valid build status:</span></span>

* <span data-ttu-id="63309-317">Criado – O modelo foi criado.</span><span class="sxs-lookup"><span data-stu-id="63309-317">Create – Model was created.</span></span>
* <span data-ttu-id="63309-318">Na fila – A compilação do modelo foi disparada e está na fila.</span><span class="sxs-lookup"><span data-stu-id="63309-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="63309-319">Criando – O modelo está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="63309-319">Building – Model is being built.</span></span>
* <span data-ttu-id="63309-320">Sucesso – A compilação concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="63309-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="63309-321">Erro – A compilação foi concluída com uma falha.</span><span class="sxs-lookup"><span data-stu-id="63309-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="63309-322">Cancelado – A compilação foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="63309-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="63309-323">Cancelando – A compilação está sendo cancelada.</span><span class="sxs-lookup"><span data-stu-id="63309-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="63309-324">Observe que a ID de compilação pode ser encontrada no seguinte caminho: `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="63309-324">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="63309-325">XML de OData</span><span class="sxs-lookup"><span data-stu-id="63309-325">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">1000272</d:Id>
        <d:UserName m:type="Edm.String"></d:UserName>
        <d:ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:ModelId>
        <d:ModelName m:type="Edm.String">docTest</d:ModelName>
        <d:Type m:type="Edm.String">Recommendation</d:Type>
        <d:CreationTime m:type="Edm.String">2014-10-05T08:56:31.893</d:CreationTime>
        <d:Progress_BuildId m:type="Edm.String">1000272</d:Progress_BuildId>
        <d:Progress_ModelId m:type="Edm.String">9559872f-7a53-4076-a3c7-19d9385c1265</d:Progress_ModelId>
        <d:Progress_UserName m:type="Edm.String">5-4058-ab36-1fe254f05102@dm.com</d:Progress_UserName>
        <d:Progress_IsExecutionStarted m:type="Edm.String">false</d:Progress_IsExecutionStarted>
        <d:Progress_IsExecutionEnded m:type="Edm.String">false</d:Progress_IsExecutionEnded>
        <d:Progress_Percent m:type="Edm.String">0</d:Progress_Percent>
        <d:Progress_StartTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_StartTime>
        <d:Progress_EndTime m:type="Edm.String">0001-01-01T00:00:00</d:Progress_EndTime>
        <d:Progress_UpdateDateUTC m:type="Edm.String"></d:Progress_UpdateDateUTC>
        <d:Status m:type="Edm.String">Queued</d:Status>
        <d:Key1 m:type="Edm.String">UseFeaturesInModel</d:Key1>
        <d:Value1 m:type="Edm.String">False</d:Value1>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="63309-326">Obter status da compilação de um modelo</span><span class="sxs-lookup"><span data-stu-id="63309-326">Get build status of a model</span></span>
| <span data-ttu-id="63309-327">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="63309-327">HTTP Method</span></span> | <span data-ttu-id="63309-328">URI</span><span class="sxs-lookup"><span data-stu-id="63309-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="63309-329">GET</span><span class="sxs-lookup"><span data-stu-id="63309-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="63309-330">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="63309-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="63309-331">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="63309-331">Parameter Name</span></span> | <span data-ttu-id="63309-332">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="63309-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="63309-333">modelId</span><span class="sxs-lookup"><span data-stu-id="63309-333">modelId</span></span> |<span data-ttu-id="63309-334">O identificador exclusivo do modelo (diferencia maiúsculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="63309-334">Unique identifier of the model  (case-sensitive)</span></span> |
| <span data-ttu-id="63309-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="63309-335">onlyLastBuild</span></span> |<span data-ttu-id="63309-336">Indica se é necessário retornar todo o histórico de compilação do modelo ou apenas o status da compilação mais recente.</span><span class="sxs-lookup"><span data-stu-id="63309-336">Indicates whether to return all the build history of the model or only the status of the most recent build.</span></span> |
| <span data-ttu-id="63309-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="63309-337">apiVersion</span></span> |<span data-ttu-id="63309-338">1.0</span><span class="sxs-lookup"><span data-stu-id="63309-338">1.0</span></span> |

<span data-ttu-id="63309-339">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="63309-339">**Response**:</span></span>

<span data-ttu-id="63309-340">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="63309-340">HTTP Status code: 200</span></span>

<span data-ttu-id="63309-341">A resposta inclui uma entrada por compilação.</span><span class="sxs-lookup"><span data-stu-id="63309-341">The response includes one entry per build.</span></span> <span data-ttu-id="63309-342">Cada entrada tem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="63309-342">Each entry has the following data:</span></span>

* <span data-ttu-id="63309-343">`feed/entry/content/properties/UserName` – O nome do usuário.</span><span class="sxs-lookup"><span data-stu-id="63309-343">`feed/entry/content/properties/UserName` – Name of the user.</span></span>
* <span data-ttu-id="63309-344">`feed/entry/content/properties/ModelName` – O nome do modelo.</span><span class="sxs-lookup"><span data-stu-id="63309-344">`feed/entry/content/properties/ModelName` – Name of the model.</span></span>
* <span data-ttu-id="63309-345">`feed/entry/content/properties/ModelId` – Identificador exclusivo do modelo.</span><span class="sxs-lookup"><span data-stu-id="63309-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="63309-346">`feed/entry/content/properties/IsDeployed` - Se a compilação é implantada (conhecido como</span><span class="sxs-lookup"><span data-stu-id="63309-346">`feed/entry/content/properties/IsDeployed` – Whether the build is deployed (a.k.a.</span></span> <span data-ttu-id="63309-347">compilação ativa).</span><span class="sxs-lookup"><span data-stu-id="63309-347">active build).</span></span>
* <span data-ttu-id="63309-348">`feed/entry/content/properties/BuildId` – Identificador exclusivo da compilação.</span><span class="sxs-lookup"><span data-stu-id="63309-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="63309-349">`feed/entry/content/properties/BuildType` - Tipo de compilação.</span><span class="sxs-lookup"><span data-stu-id="63309-349">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="63309-350">`feed/entry/content/properties/Status` – Status da compilação.</span><span class="sxs-lookup"><span data-stu-id="63309-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="63309-351">Este pode ser uma das seguintes opções: Erro, Criando, Na fila, Cancelando, Cancelado e Êxito</span><span class="sxs-lookup"><span data-stu-id="63309-351">Can be one of the following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="63309-352">`feed/entry/content/properties/StatusMessage` – Mensagem de status detalhada (aplica-se somente a estados específicos).</span><span class="sxs-lookup"><span data-stu-id="63309-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="63309-353">`feed/entry/content/properties/Progress` – Andamento da compilação (%).</span><span class="sxs-lookup"><span data-stu-id="63309-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="63309-354">`feed/entry/content/properties/StartTime` – Hora de início da compilação.</span><span class="sxs-lookup"><span data-stu-id="63309-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="63309-355">`feed/entry/content/properties/EndTime` – Hora de término da compilação.</span><span class="sxs-lookup"><span data-stu-id="63309-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="63309-356">`feed/entry/content/properties/ExecutionTime` – Duração da compilação.</span><span class="sxs-lookup"><span data-stu-id="63309-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="63309-357">`feed/entry/content/properties/ProgressStep` – Detalhes sobre o estágio atual de uma compilação em andamento.</span><span class="sxs-lookup"><span data-stu-id="63309-357">`feed/entry/content/properties/ProgressStep` – Details about the current stage that a build in progress is in.</span></span>

<span data-ttu-id="63309-358">Status de compilação válidos:</span><span class="sxs-lookup"><span data-stu-id="63309-358">Valid build status:</span></span>

* <span data-ttu-id="63309-359">Criada - a entrada da solicitação de compilação foi criada.</span><span class="sxs-lookup"><span data-stu-id="63309-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="63309-360">Em fila – a solicitação de build foi disparada e está na fila.</span><span class="sxs-lookup"><span data-stu-id="63309-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="63309-361">Compilando – a build está em andamento.</span><span class="sxs-lookup"><span data-stu-id="63309-361">Building – Build is in process.</span></span>
* <span data-ttu-id="63309-362">Sucesso – A compilação concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="63309-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="63309-363">Erro – A compilação foi concluída com uma falha.</span><span class="sxs-lookup"><span data-stu-id="63309-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="63309-364">Cancelado – A compilação foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="63309-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="63309-365">Cancelando – A compilação está sendo cancelada.</span><span class="sxs-lookup"><span data-stu-id="63309-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="63309-366">Valores válidos para o tipo de compilação:</span><span class="sxs-lookup"><span data-stu-id="63309-366">Valid values for build type:</span></span>

* <span data-ttu-id="63309-367">Classificação - compilação de classificação.</span><span class="sxs-lookup"><span data-stu-id="63309-367">Rank - Rank build.</span></span> <span data-ttu-id="63309-368">(Para obter detalhes do build de classificação, consulte o documento “Documentação da API de Recomendação do Machine Learning”).</span><span class="sxs-lookup"><span data-stu-id="63309-368">(For rank build details, please refer to the "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="63309-369">Recomendação - compilação de recomendação.</span><span class="sxs-lookup"><span data-stu-id="63309-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="63309-370">Fbt - Build de frequentemente comprados juntos.</span><span class="sxs-lookup"><span data-stu-id="63309-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="63309-371">XML de OData</span><span class="sxs-lookup"><span data-stu-id="63309-371">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get builds status of a model</subtitle>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetBuildsStatusEntity</title>
    <updated>2014-11-05T17:51:10Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:UserName m:type="Edm.String">b-434e-b2c9-84935664ff20@dm.com</d:UserName>
        <d:ModelName m:type="Edm.String">ModelName</d:ModelName>
        <d:ModelId m:type="Edm.String">1d20c34f-dca1-4eac-8e5d-f299e4e4ad66</d:ModelId>
        <d:IsDeployed m:type="Edm.String">true</d:IsDeployed>
        <d:BuildId m:type="Edm.String">1000272</d:BuildId>
        <d:BuildType m:type="Edm.String">Recommendation</d:BuildType>
        <d:Status m:type="Edm.String">Success</d:Status>
        <d:StatusMessage m:type="Edm.String"></d:StatusMessage>
        <d:Progress m:type="Edm.String">0</d:Progress>
        <d:StartTime m:type="Edm.String">2014-11-02T13:43:51</d:StartTime>
        <d:EndTime m:type="Edm.String">2014-11-02T13:45:10</d:EndTime>
        <d:ExecutionTime m:type="Edm.String">00:01:19</d:ExecutionTime>
        <d:IsExecutionStarted m:type="Edm.String">false</d:IsExecutionStarted>
        <d:ProgressStep m:type="Edm.String"></d:ProgressStep>
      </m:properties>
     </content>
    </entry>
    </feed>


### <a name="get-recommendations"></a><span data-ttu-id="63309-372">Obter recomendações</span><span class="sxs-lookup"><span data-stu-id="63309-372">Get recommendations</span></span>
| <span data-ttu-id="63309-373">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="63309-373">HTTP Method</span></span> | <span data-ttu-id="63309-374">URI</span><span class="sxs-lookup"><span data-stu-id="63309-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="63309-375">GET</span><span class="sxs-lookup"><span data-stu-id="63309-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="63309-376">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="63309-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="63309-377">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="63309-377">Parameter Name</span></span> | <span data-ttu-id="63309-378">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="63309-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="63309-379">modelId</span><span class="sxs-lookup"><span data-stu-id="63309-379">modelId</span></span> |<span data-ttu-id="63309-380">O identificador exclusivo do modelo (diferencia maiúsculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="63309-380">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="63309-381">itemIds</span><span class="sxs-lookup"><span data-stu-id="63309-381">itemIds</span></span> |<span data-ttu-id="63309-382">Lista separada por vírgulas dos itens para recomendar.</span><span class="sxs-lookup"><span data-stu-id="63309-382">Comma-separated list of the items to recommend for.</span></span><br><span data-ttu-id="63309-383">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="63309-383">Max length: 1024</span></span> |
| <span data-ttu-id="63309-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="63309-384">numberOfResults</span></span> |<span data-ttu-id="63309-385">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="63309-385">Number of required results</span></span> |
| <span data-ttu-id="63309-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="63309-386">includeMetatadata</span></span> |<span data-ttu-id="63309-387">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="63309-387">Future use, always false</span></span> |
| <span data-ttu-id="63309-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="63309-388">apiVersion</span></span> |<span data-ttu-id="63309-389">1.0</span><span class="sxs-lookup"><span data-stu-id="63309-389">1.0</span></span> |

<span data-ttu-id="63309-390">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="63309-390">**Response:**</span></span>

<span data-ttu-id="63309-391">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="63309-391">HTTP Status code: 200</span></span>

<span data-ttu-id="63309-392">A resposta inclui uma entrada por item recomendado.</span><span class="sxs-lookup"><span data-stu-id="63309-392">The response includes one entry per recommended item.</span></span> <span data-ttu-id="63309-393">Cada entrada tem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="63309-393">Each entry has the following data:</span></span>

* <span data-ttu-id="63309-394">`Feed\entry\content\properties\Id` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="63309-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="63309-395">`Feed\entry\content\properties\Name` - Nome do item.</span><span class="sxs-lookup"><span data-stu-id="63309-395">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="63309-396">`Feed\entry\content\properties\Rating` - Classificação da recomendação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="63309-396">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="63309-397">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="63309-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="63309-398">XML de OData</span><span class="sxs-lookup"><span data-stu-id="63309-398">OData XML</span></span>

<span data-ttu-id="63309-399">A resposta de exemplo a seguir inclui 10 itens recomendados:</span><span class="sxs-lookup"><span data-stu-id="63309-399">The example response below includes 10 recommended items:</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">159</d:Id>
        <d:Name m:type="Edm.String">159</d:Name>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">52</d:Id>
        <d:Name m:type="Edm.String">52</d:Name>
        <d:Rating m:type="Edm.Double">0.539588900748721</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">35</d:Id>
        <d:Name m:type="Edm.String">35</d:Name>
        <d:Rating m:type="Edm.Double">0.53842946443853</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '35'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">124</d:Id>
        <d:Name m:type="Edm.String">124</d:Name>
        <d:Rating m:type="Edm.Double">0.536712832792886</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '124'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">120</d:Id>
        <d:Name m:type="Edm.String">120</d:Name>
        <d:Rating m:type="Edm.Double">0.533673023762878</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '120'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">96</d:Id>
        <d:Name m:type="Edm.String">96</d:Name>
        <d:Rating m:type="Edm.Double">0.532544826370521</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '96'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">69</d:Id>
        <d:Name m:type="Edm.String">69</d:Name>
        <d:Rating m:type="Edm.Double">0.531678607847759</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '69'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">172</d:Id>
        <d:Name m:type="Edm.String">172</d:Name>
        <d:Rating m:type="Edm.Double">0.530957821375951</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '172'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">155</d:Id>
        <d:Name m:type="Edm.String">155</d:Name>
        <d:Rating m:type="Edm.Double">0.529093541481333</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '155'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">32</d:Id>
        <d:Name m:type="Edm.String">32</d:Name>
        <d:Rating m:type="Edm.Double">0.528917978168322</d:Rating>
        <d:Reasoning m:type="Edm.String">People who like '1003' also like '32'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="update-model"></a><span data-ttu-id="63309-400">Atualizar modelo</span><span class="sxs-lookup"><span data-stu-id="63309-400">Update model</span></span>
<span data-ttu-id="63309-401">Você pode atualizar a descrição do modelo ou a ID de compilação ativa.</span><span class="sxs-lookup"><span data-stu-id="63309-401">You can update the model description or the active build ID.</span></span>
<span data-ttu-id="63309-402">*ID de compilação ativa* – cada compilação para cada modelo tem uma ID de compilação.</span><span class="sxs-lookup"><span data-stu-id="63309-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="63309-403">A ID de compilação ativa é a primeira compilação executada com êxito de cada novo modelo.</span><span class="sxs-lookup"><span data-stu-id="63309-403">The active build ID is the first successful build of every new model.</span></span> <span data-ttu-id="63309-404">Depois que tiver uma ID de compilação ativa e criar compilações adicionais para o mesmo modelo, você precisará defini-lo explicitamente como a ID de compilação padrão, se desejar.</span><span class="sxs-lookup"><span data-stu-id="63309-404">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span></span> <span data-ttu-id="63309-405">Ao consumir recomendações, se você não especificar a ID de compilação que deseja usar, o padrão será usado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="63309-405">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span></span>

<span data-ttu-id="63309-406">Esse mecanismo permite, depois de ter um modelo de recomendação em produção, compilar e testar novos modelos antes de promovê-los para produção.</span><span class="sxs-lookup"><span data-stu-id="63309-406">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span></span>

| <span data-ttu-id="63309-407">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="63309-407">HTTP Method</span></span> | <span data-ttu-id="63309-408">URI</span><span class="sxs-lookup"><span data-stu-id="63309-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="63309-409">PUT</span><span class="sxs-lookup"><span data-stu-id="63309-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="63309-410">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="63309-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="63309-411">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="63309-411">Parameter Name</span></span> | <span data-ttu-id="63309-412">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="63309-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="63309-413">ID</span><span class="sxs-lookup"><span data-stu-id="63309-413">id</span></span> |<span data-ttu-id="63309-414">O identificador exclusivo do modelo (diferencia maiúsculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="63309-414">Unique identifier of the model (case-sensitive)</span></span> |
| <span data-ttu-id="63309-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="63309-415">apiVersion</span></span> |<span data-ttu-id="63309-416">1.0</span><span class="sxs-lookup"><span data-stu-id="63309-416">1.0</span></span> |
|  | |
| <span data-ttu-id="63309-417">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="63309-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="63309-418">Observe que as marcações XML Description e ActiveBuildId são opcionais.</span><span class="sxs-lookup"><span data-stu-id="63309-418">Note that the XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="63309-419">Se você não quiser definir Description ou ActiveBuildId, remova a marca inteira.</span><span class="sxs-lookup"><span data-stu-id="63309-419">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span></span> |

<span data-ttu-id="63309-420">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="63309-420">**Response**:</span></span>

<span data-ttu-id="63309-421">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="63309-421">HTTP Status code: 200</span></span>

<span data-ttu-id="63309-422">XML de OData</span><span class="sxs-lookup"><span data-stu-id="63309-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="63309-423">Legal</span><span class="sxs-lookup"><span data-stu-id="63309-423">Legal</span></span>
<span data-ttu-id="63309-424">Este documento é fornecido "no estado em que se encontra".</span><span class="sxs-lookup"><span data-stu-id="63309-424">This document is provided "as-is".</span></span> <span data-ttu-id="63309-425">As informações e opiniões expressadas neste documento, incluindo URLs e outras referências a sites da Internet, podem ser alteradas sem aviso prévio.</span><span class="sxs-lookup"><span data-stu-id="63309-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="63309-426">Alguns exemplos aqui representados são fornecidos somente para fins de ilustração e são fictícios.</span><span class="sxs-lookup"><span data-stu-id="63309-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="63309-427">Nenhuma associação ou conexão real é intencional ou deve ser inferida.</span><span class="sxs-lookup"><span data-stu-id="63309-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="63309-428">Este documento não fornece a você nenhum direito legal a qualquer propriedade intelectual de qualquer produto da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="63309-428">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="63309-429">Você pode copiar e usar este documento para fins de consulta interna.</span><span class="sxs-lookup"><span data-stu-id="63309-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="63309-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="63309-430">© 2014 Microsoft.</span></span> <span data-ttu-id="63309-431">Todos os direitos reservados.</span><span class="sxs-lookup"><span data-stu-id="63309-431">All rights reserved.</span></span> 

