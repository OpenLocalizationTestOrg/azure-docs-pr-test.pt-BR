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
redirect_document_id: True
ms.openlocfilehash: d8f98e85f723a1104cb169b26d797934140979f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-start-guide-for-hello-machine-learning-recommendations-api-version-1"></a><span data-ttu-id="8e4e7-104">Guia de início rápido para Olá API de recomendações de aprendizado de máquina (versão 1)</span><span class="sxs-lookup"><span data-stu-id="8e4e7-104">Quick start guide for hello Machine Learning Recommendations API (version 1)</span></span>

> [!NOTE]
> <span data-ttu-id="8e4e7-105">Você deve começar a usar o hello [recomendações API cognitivas serviço](https://www.microsoft.com/cognitive-services/recommendations-api) em vez de nesta versão.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-105">You should start using hello [Recommendations API Cognitive Service](https://www.microsoft.com/cognitive-services/recommendations-api) instead of this version.</span></span> <span data-ttu-id="8e4e7-106">Olá serviço cognitivas recomendações será substituído por esse serviço e todos os novos recursos de saudação serão desenvolvidos existe.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-106">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="8e4e7-107">Ele possui novos recursos como suporte ao processamento em lotes, um Gerenciador de API aprimorado, uma superfície de API mais limpa, uma experiência de inscrição/cobrança mais consistente etc.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-107">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
>
> <span data-ttu-id="8e4e7-108">Saiba mais sobre [toohello migrando novo serviço cognitivas](http://aka.ms/recomigrate).</span><span class="sxs-lookup"><span data-stu-id="8e4e7-108">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate).</span></span>
> 
> 

<span data-ttu-id="8e4e7-109">Este documento descreve como tooonboard toouse seu serviço ou aplicativo recomendações de aprendizado de máquina do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-109">This document describes how tooonboard your service or application toouse Microsoft Azure Machine Learning Recommendations.</span></span> <span data-ttu-id="8e4e7-110">Você pode encontrar mais detalhes no hello API recomendações em Olá [Cortana Intelligence galeria](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span><span class="sxs-lookup"><span data-stu-id="8e4e7-110">You can find more details on hello Recommendations API in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/MachineLearningAPIs/Recommendations-2).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="general-overview"></a><span data-ttu-id="8e4e7-111">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8e4e7-111">General overview</span></span>
<span data-ttu-id="8e4e7-112">toouse recomendações de aprendizado de máquina do Azure, você precisará Olá tootake etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-112">toouse Azure Machine Learning Recommendations, you need tootake hello following steps:</span></span>

* <span data-ttu-id="8e4e7-113">Criar um modelo - um modelo é um contêiner de seus dados de uso, dados de catálogo e modelo de recomendação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-113">Create a model - A model is a container of your usage data, catalog data, and hello recommendation model.</span></span>
* <span data-ttu-id="8e4e7-114">Importar dados de catálogo - um catálogo contém informações de metadados sobre itens de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-114">Import catalog data - A catalog contains metadata information on hello items.</span></span> 
* <span data-ttu-id="8e4e7-115">Importar dados de uso: os dados de uso podem ser carregados de uma entre duas maneiras (ou ambas):</span><span class="sxs-lookup"><span data-stu-id="8e4e7-115">Import usage data - Usage data can be uploaded in one of two ways (or both):</span></span>
  * <span data-ttu-id="8e4e7-116">Carregando um arquivo que contém dados de uso de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-116">By uploading a file that contains hello usage data.</span></span>
  * <span data-ttu-id="8e4e7-117">Enviando eventos de aquisição de dados.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-117">By sending data acquisition events.</span></span>
    <span data-ttu-id="8e4e7-118">Geralmente você carregar um arquivo de uso na ordem de toobe capaz de toocreate um modelo de recomendação inicial (inicialização) e usá-lo até que o sistema Olá reúne dados suficientes usando o formato de aquisição de dados hello.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-118">Usually you upload a usage file in order toobe able toocreate an initial recommendation model (bootstrap) and use it until hello system gathers enough data by using hello data acquisition format.</span></span>
* <span data-ttu-id="8e4e7-119">Criar um modelo de recomendação - esta é uma operação assíncrona no qual Olá sistema de recomendação usa todos os dados de uso de saudação e cria um modelo de recomendação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-119">Build a recommendation model - This is an asynchronous operation in which hello recommendation system takes all hello usage data and creates a recommendation model.</span></span> <span data-ttu-id="8e4e7-120">Essa operação pode levar vários minutos ou várias horas, dependendo da saudação o tamanho dos dados de saudação e Olá criar parâmetros de configuração.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-120">This operation can take several minutes or several hours depending on hello size of hello data and hello build configuration parameters.</span></span> <span data-ttu-id="8e4e7-121">Quando disparo compilação hello, você obterá uma ID de compilação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-121">When triggering hello build, you will get a build ID.</span></span> <span data-ttu-id="8e4e7-122">Use-toocheck quando o processo de compilação Olá terminou antes de iniciar tooconsume recomendações.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-122">Use it toocheck when hello build process has ended before starting tooconsume recommendations.</span></span>
* <span data-ttu-id="8e4e7-123">Consumir recomendações - Obtenha recomendações para um item específico ou uma lista de itens.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-123">Consume recommendations - Get recommendations for a specific item or list of items.</span></span>

<span data-ttu-id="8e4e7-124">Todas as etapas de saudação acima são feitas por meio de saudação API de recomendações de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-124">All hello steps above are done through hello Azure Machine Learning Recommendations API.</span></span>  <span data-ttu-id="8e4e7-125">Você pode baixar um aplicativo de exemplo que implementa a cada uma dessas etapas de saudação [Galeria também.](http://1drv.ms/1xeO2F3)</span><span class="sxs-lookup"><span data-stu-id="8e4e7-125">You can download a sample application that implements each of these steps from hello [gallery as well.](http://1drv.ms/1xeO2F3)</span></span>

## <a name="limitations"></a><span data-ttu-id="8e4e7-126">Limitações</span><span class="sxs-lookup"><span data-stu-id="8e4e7-126">Limitations</span></span>
* <span data-ttu-id="8e4e7-127">número máximo de saudação de modelos por assinatura é 10.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-127">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="8e4e7-128">número máximo de saudação de itens que pode conter um catálogo é 100.000.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-128">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="8e4e7-129">número máximo de saudação de pontos de uso que são mantidos é ~ 5.000.000.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-129">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="8e4e7-130">Olá mais antigo será excluído se novas serão carregadas ou relatadas.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-130">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="8e4e7-131">tamanho máximo de saudação de dados que podem ser enviados no POST (por exemplo, importar dados de catálogo, importar dados de uso) é de 200MB.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-131">hello maximum size of data that can be sent in POST (for example, import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="8e4e7-132">Olá número de transações por segundo para uma compilação de modelo de recomendação não está ativo é ~ 2TPS.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-132">hello number of transactions per second for a recommendation model build that is not active is ~2TPS.</span></span> <span data-ttu-id="8e4e7-133">Uma compilação de modelo de recomendação está ativa pode conter backup too20TPS.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-133">A recommendation model build that is active can hold up too20TPS.</span></span>

## <a name="integration"></a><span data-ttu-id="8e4e7-134">Integração</span><span class="sxs-lookup"><span data-stu-id="8e4e7-134">Integration</span></span>
### <a name="authentication"></a><span data-ttu-id="8e4e7-135">Autenticação</span><span class="sxs-lookup"><span data-stu-id="8e4e7-135">Authentication</span></span>
<span data-ttu-id="8e4e7-136">Microsoft Azure Marketplace oferece suporte a um método de autenticação básica ou OAuth hello.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-136">Microsoft Azure Marketplace supports either hello Basic or OAuth authentication method.</span></span> <span data-ttu-id="8e4e7-137">Você pode localizar facilmente Olá chaves de conta navegando toohello chaves no marketplace de saudação em [as configurações de conta](https://datamarket.azure.com/account/keys).</span><span class="sxs-lookup"><span data-stu-id="8e4e7-137">You can easily find hello account keys by navigating toohello keys in hello marketplace under [your account settings](https://datamarket.azure.com/account/keys).</span></span> 

#### <a name="basic-authentication"></a><span data-ttu-id="8e4e7-138">Autenticação básica</span><span class="sxs-lookup"><span data-stu-id="8e4e7-138">Basic Authentication</span></span>
<span data-ttu-id="8e4e7-139">Adicione o cabeçalho de autorização hello:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-139">Add hello Authorization header:</span></span>

    Authorization: Basic <creds>

    Where <creds> = ConvertToBase64("AccountKey:" + yourAccountKey);  

<span data-ttu-id="8e4e7-140">Converter tooBase64 (c#)</span><span class="sxs-lookup"><span data-stu-id="8e4e7-140">Convert tooBase64 (C#)</span></span>

    var bytes = Encoding.UTF8.GetBytes("AccountKey:" + yourAccountKey);
    var creds = Convert.ToBase64String(bytes);

<span data-ttu-id="8e4e7-141">Converter tooBase64 (JavaScript)</span><span class="sxs-lookup"><span data-stu-id="8e4e7-141">Convert tooBase64 (JavaScript)</span></span>

    var creds = window.btoa("AccountKey" + ":" + yourAccountKey);




### <a name="service-uri"></a><span data-ttu-id="8e4e7-142">URI de serviço</span><span class="sxs-lookup"><span data-stu-id="8e4e7-142">Service URI</span></span>
<span data-ttu-id="8e4e7-143">Olá URI raiz do serviço para Olá APIs de recomendações de aprendizado de máquina do Azure é [aqui.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span><span class="sxs-lookup"><span data-stu-id="8e4e7-143">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v2/)</span></span>

<span data-ttu-id="8e4e7-144">URI do serviço completo Olá é expressa usando elementos da especificação de OData hello.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-144">hello full service URI is expressed using elements of hello OData specification.</span></span>

### <a name="api-version"></a><span data-ttu-id="8e4e7-145">Versão da API</span><span class="sxs-lookup"><span data-stu-id="8e4e7-145">API version</span></span>
<span data-ttu-id="8e4e7-146">Cada chamada de API terá, no final do hello, um parâmetro de consulta chamado apiVersion que deve ser definido muito "1.0".</span><span class="sxs-lookup"><span data-stu-id="8e4e7-146">Each API call will have, at hello end, a query parameter called apiVersion that should be set too"1.0".</span></span>

### <a name="ids-are-case-sensitive"></a><span data-ttu-id="8e4e7-147">IDs diferenciam minúsculas e maiúsculas</span><span class="sxs-lookup"><span data-stu-id="8e4e7-147">IDs are case-sensitive</span></span>
<span data-ttu-id="8e4e7-148">IDs, retornados por qualquer Olá APIs, diferenciam maiusculas de minúsculas e devem ser usadas como tal quando passados como parâmetros em chamadas API subsequentes.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-148">IDs, returned by any of hello APIs, are case-sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="8e4e7-149">Por exemplo, IDS de modelo e de catálogo diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-149">For instance, model IDs and catalog IDs are case-sensitive.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="8e4e7-150">Criar um modelo</span><span class="sxs-lookup"><span data-stu-id="8e4e7-150">Create a model</span></span>
<span data-ttu-id="8e4e7-151">Criando uma solicitação para "criar modelo":</span><span class="sxs-lookup"><span data-stu-id="8e4e7-151">Creating a "create model" request:</span></span>

| <span data-ttu-id="8e4e7-152">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="8e4e7-152">HTTP Method</span></span> | <span data-ttu-id="8e4e7-153">URI</span><span class="sxs-lookup"><span data-stu-id="8e4e7-153">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e4e7-154">POST</span><span class="sxs-lookup"><span data-stu-id="8e4e7-154">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="8e4e7-155">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-155">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="8e4e7-156">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="8e4e7-156">Parameter Name</span></span> | <span data-ttu-id="8e4e7-157">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="8e4e7-157">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e4e7-158">modelName</span><span class="sxs-lookup"><span data-stu-id="8e4e7-158">modelName</span></span> |<span data-ttu-id="8e4e7-159">São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).</span><span class="sxs-lookup"><span data-stu-id="8e4e7-159">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="8e4e7-160">Comprimento máximo: 20</span><span class="sxs-lookup"><span data-stu-id="8e4e7-160">Max length: 20</span></span> |
| <span data-ttu-id="8e4e7-161">apiVersion</span><span class="sxs-lookup"><span data-stu-id="8e4e7-161">apiVersion</span></span> |<span data-ttu-id="8e4e7-162">1.0</span><span class="sxs-lookup"><span data-stu-id="8e4e7-162">1.0</span></span> |
|  | |
| <span data-ttu-id="8e4e7-163">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="8e4e7-163">Request Body</span></span> |<span data-ttu-id="8e4e7-164">NENHUM</span><span class="sxs-lookup"><span data-stu-id="8e4e7-164">NONE</span></span> |

<span data-ttu-id="8e4e7-165">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-165">**Response**:</span></span>

<span data-ttu-id="8e4e7-166">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="8e4e7-166">HTTP Status code: 200</span></span>

* <span data-ttu-id="8e4e7-167">`feed/entry/content/properties/id`-Contém a ID do modelo hello.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-167">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="8e4e7-168">Observe que a ID do modelo Olá diferencia maiusculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-168">Note that hello model ID is case-sensitive.</span></span>

<span data-ttu-id="8e4e7-169">XML de OData</span><span class="sxs-lookup"><span data-stu-id="8e4e7-169">OData XML</span></span>

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


### <a name="import-catalog-data"></a><span data-ttu-id="8e4e7-170">Importar dados de catálogo</span><span class="sxs-lookup"><span data-stu-id="8e4e7-170">Import catalog data</span></span>
<span data-ttu-id="8e4e7-171">Se você carregar vários catálogo arquivos toohello mesmo modelo com várias chamadas, inserimos somente Olá novos itens de catálogo.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-171">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="8e4e7-172">Itens existentes permanecerão com seus valores originais hello.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-172">Existing items will remain with hello original values.</span></span>

| <span data-ttu-id="8e4e7-173">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="8e4e7-173">HTTP Method</span></span> | <span data-ttu-id="8e4e7-174">URI</span><span class="sxs-lookup"><span data-stu-id="8e4e7-174">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e4e7-175">POST</span><span class="sxs-lookup"><span data-stu-id="8e4e7-175">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="8e4e7-176">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-176">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="8e4e7-177">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="8e4e7-177">Parameter Name</span></span> | <span data-ttu-id="8e4e7-178">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="8e4e7-178">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e4e7-179">modelId</span><span class="sxs-lookup"><span data-stu-id="8e4e7-179">modelId</span></span> |<span data-ttu-id="8e4e7-180">Identificador exclusivo do modelo de saudação (diferencia maiusculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="8e4e7-180">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="8e4e7-181">nome do arquivo</span><span class="sxs-lookup"><span data-stu-id="8e4e7-181">filename</span></span> |<span data-ttu-id="8e4e7-182">Identificador textual do catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-182">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="8e4e7-183">São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).</span><span class="sxs-lookup"><span data-stu-id="8e4e7-183">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="8e4e7-184">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="8e4e7-184">Max length: 50</span></span> |
| <span data-ttu-id="8e4e7-185">apiVersion</span><span class="sxs-lookup"><span data-stu-id="8e4e7-185">apiVersion</span></span> |<span data-ttu-id="8e4e7-186">1.0</span><span class="sxs-lookup"><span data-stu-id="8e4e7-186">1.0</span></span> |
|  | |
| <span data-ttu-id="8e4e7-187">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="8e4e7-187">Request Body</span></span> |<span data-ttu-id="8e4e7-188">Dados de catálogo.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-188">Catalog data.</span></span> <span data-ttu-id="8e4e7-189">Formato:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-189">Format:</span></span><br>`<Item Id>,<Item Name>,<Item Category>[,<description>]`<br><br><table><tr><th><span data-ttu-id="8e4e7-190">Nome</span><span class="sxs-lookup"><span data-stu-id="8e4e7-190">Name</span></span></th><th><span data-ttu-id="8e4e7-191">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8e4e7-191">Mandatory</span></span></th><th><span data-ttu-id="8e4e7-192">Tipo</span><span class="sxs-lookup"><span data-stu-id="8e4e7-192">Type</span></span></th><th><span data-ttu-id="8e4e7-193">Descrição</span><span class="sxs-lookup"><span data-stu-id="8e4e7-193">Description</span></span></th></tr><tr><td><span data-ttu-id="8e4e7-194">Id do item</span><span class="sxs-lookup"><span data-stu-id="8e4e7-194">Item Id</span></span></td><td><span data-ttu-id="8e4e7-195">Sim</span><span class="sxs-lookup"><span data-stu-id="8e4e7-195">Yes</span></span></td><td><span data-ttu-id="8e4e7-196">Alfanumérico, comprimento máximo 50</span><span class="sxs-lookup"><span data-stu-id="8e4e7-196">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="8e4e7-197">Identificador exclusivo de um item</span><span class="sxs-lookup"><span data-stu-id="8e4e7-197">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="8e4e7-198">Nome do Item</span><span class="sxs-lookup"><span data-stu-id="8e4e7-198">Item Name</span></span></td><td><span data-ttu-id="8e4e7-199">Sim</span><span class="sxs-lookup"><span data-stu-id="8e4e7-199">Yes</span></span></td><td><span data-ttu-id="8e4e7-200">Alfanumérico, comprimento máximo 255</span><span class="sxs-lookup"><span data-stu-id="8e4e7-200">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="8e4e7-201">Nome do item</span><span class="sxs-lookup"><span data-stu-id="8e4e7-201">Item name</span></span></td></tr><tr><td><span data-ttu-id="8e4e7-202">Categoria do Item</span><span class="sxs-lookup"><span data-stu-id="8e4e7-202">Item Category</span></span></td><td><span data-ttu-id="8e4e7-203">Sim</span><span class="sxs-lookup"><span data-stu-id="8e4e7-203">Yes</span></span></td><td><span data-ttu-id="8e4e7-204">Alfanumérico, comprimento máximo 255</span><span class="sxs-lookup"><span data-stu-id="8e4e7-204">Alphanumeric, max length 255</span></span></td><td><span data-ttu-id="8e4e7-205">Categoria toowhich que este item pertence (por exemplo, livros de culinária Drama...)</span><span class="sxs-lookup"><span data-stu-id="8e4e7-205">Category toowhich this item belongs (for example, Cooking Books, Drama…)</span></span></td></tr><tr><td><span data-ttu-id="8e4e7-206">Descrição</span><span class="sxs-lookup"><span data-stu-id="8e4e7-206">Description</span></span></td><td><span data-ttu-id="8e4e7-207">Não</span><span class="sxs-lookup"><span data-stu-id="8e4e7-207">No</span></span></td><td><span data-ttu-id="8e4e7-208">Alfanumérico, comprimento máximo 4000</span><span class="sxs-lookup"><span data-stu-id="8e4e7-208">Alphanumeric, max length 4000</span></span></td><td><span data-ttu-id="8e4e7-209">Descrição deste item</span><span class="sxs-lookup"><span data-stu-id="8e4e7-209">Description of this item</span></span></td></tr></table><br><span data-ttu-id="8e4e7-210">O tamanho máximo do arquivo é de 200 MB.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-210">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="8e4e7-211">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-211">Example:</span></span><br><code>2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book<br>21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book<br>3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book<br>552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book</code> |

<span data-ttu-id="8e4e7-212">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-212">**Response**:</span></span>

<span data-ttu-id="8e4e7-213">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="8e4e7-213">HTTP Status code: 200</span></span>

* <span data-ttu-id="8e4e7-214">`Feed\entry\content\properties\LineCount` – O número de linhas aceitas.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-214">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="8e4e7-215">`Feed\entry\content\properties\ErrorCount`-Número de linhas que não foram inseridas devido a erro tooan.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-215">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="8e4e7-216">XML de OData</span><span class="sxs-lookup"><span data-stu-id="8e4e7-216">OData XML</span></span>

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


### <a name="import-usage-data"></a><span data-ttu-id="8e4e7-217">Importar dados de uso</span><span class="sxs-lookup"><span data-stu-id="8e4e7-217">Import usage data</span></span>
#### <a name="uploading-a-file"></a><span data-ttu-id="8e4e7-218">Carregar um arquivo</span><span class="sxs-lookup"><span data-stu-id="8e4e7-218">Uploading a file</span></span>
<span data-ttu-id="8e4e7-219">Esta seção mostra como os dados de uso tooupload usando um arquivo.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-219">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="8e4e7-220">Você pode chamar essa API várias vezes com dados de uso.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-220">You can call this API several times with usage data.</span></span> <span data-ttu-id="8e4e7-221">Todos os dados de uso serão salvos para todas as chamadas.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-221">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="8e4e7-222">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="8e4e7-222">HTTP Method</span></span> | <span data-ttu-id="8e4e7-223">URI</span><span class="sxs-lookup"><span data-stu-id="8e4e7-223">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e4e7-224">POST</span><span class="sxs-lookup"><span data-stu-id="8e4e7-224">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="8e4e7-225">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-225">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="8e4e7-226">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="8e4e7-226">Parameter Name</span></span> | <span data-ttu-id="8e4e7-227">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="8e4e7-227">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e4e7-228">modelId</span><span class="sxs-lookup"><span data-stu-id="8e4e7-228">modelId</span></span> |<span data-ttu-id="8e4e7-229">Identificador exclusivo do modelo de saudação (diferencia maiusculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="8e4e7-229">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="8e4e7-230">nome do arquivo</span><span class="sxs-lookup"><span data-stu-id="8e4e7-230">filename</span></span> |<span data-ttu-id="8e4e7-231">Identificador textual do catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-231">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="8e4e7-232">São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).</span><span class="sxs-lookup"><span data-stu-id="8e4e7-232">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="8e4e7-233">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="8e4e7-233">Max length: 50</span></span> |
| <span data-ttu-id="8e4e7-234">apiVersion</span><span class="sxs-lookup"><span data-stu-id="8e4e7-234">apiVersion</span></span> |<span data-ttu-id="8e4e7-235">1.0</span><span class="sxs-lookup"><span data-stu-id="8e4e7-235">1.0</span></span> |
|  | |
| <span data-ttu-id="8e4e7-236">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="8e4e7-236">Request Body</span></span> |<span data-ttu-id="8e4e7-237">Dados de uso.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-237">Usage data.</span></span> <span data-ttu-id="8e4e7-238">Formato:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-238">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="8e4e7-239">Nome</span><span class="sxs-lookup"><span data-stu-id="8e4e7-239">Name</span></span></th><th><span data-ttu-id="8e4e7-240">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8e4e7-240">Mandatory</span></span></th><th><span data-ttu-id="8e4e7-241">Tipo</span><span class="sxs-lookup"><span data-stu-id="8e4e7-241">Type</span></span></th><th><span data-ttu-id="8e4e7-242">Descrição</span><span class="sxs-lookup"><span data-stu-id="8e4e7-242">Description</span></span></th></tr><tr><td><span data-ttu-id="8e4e7-243">Id de usuário</span><span class="sxs-lookup"><span data-stu-id="8e4e7-243">User Id</span></span></td><td><span data-ttu-id="8e4e7-244">Sim</span><span class="sxs-lookup"><span data-stu-id="8e4e7-244">Yes</span></span></td><td><span data-ttu-id="8e4e7-245">Alfanumérico</span><span class="sxs-lookup"><span data-stu-id="8e4e7-245">Alphanumeric</span></span></td><td><span data-ttu-id="8e4e7-246">Identificador exclusivo de um usuário</span><span class="sxs-lookup"><span data-stu-id="8e4e7-246">Unique identifier of a user</span></span></td></tr><tr><td><span data-ttu-id="8e4e7-247">Id do item</span><span class="sxs-lookup"><span data-stu-id="8e4e7-247">Item Id</span></span></td><td><span data-ttu-id="8e4e7-248">Sim</span><span class="sxs-lookup"><span data-stu-id="8e4e7-248">Yes</span></span></td><td><span data-ttu-id="8e4e7-249">Alfanumérico, comprimento máximo 50</span><span class="sxs-lookup"><span data-stu-id="8e4e7-249">Alphanumeric, max length 50</span></span></td><td><span data-ttu-id="8e4e7-250">Identificador exclusivo de um item</span><span class="sxs-lookup"><span data-stu-id="8e4e7-250">Unique identifier of an item</span></span></td></tr><tr><td><span data-ttu-id="8e4e7-251">Hora</span><span class="sxs-lookup"><span data-stu-id="8e4e7-251">Time</span></span></td><td><span data-ttu-id="8e4e7-252">Não</span><span class="sxs-lookup"><span data-stu-id="8e4e7-252">No</span></span></td><td><span data-ttu-id="8e4e7-253">Data no formato: AAAA/MM/DDTHH:MM:SS (por exemplo, 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="8e4e7-253">Date in format: YYYY/MM/DDTHH:MM:SS (for example, 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="8e4e7-254">Hora dos dados</span><span class="sxs-lookup"><span data-stu-id="8e4e7-254">Time of data</span></span></td></tr><tr><td><span data-ttu-id="8e4e7-255">Evento</span><span class="sxs-lookup"><span data-stu-id="8e4e7-255">Event</span></span></td><td><span data-ttu-id="8e4e7-256">Não, se fornecido, também deve colocar a data</span><span class="sxs-lookup"><span data-stu-id="8e4e7-256">No, if supplied then must also put date</span></span></td><td><span data-ttu-id="8e4e7-257">Um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-257">One of hello following:</span></span><br><span data-ttu-id="8e4e7-258">• Clique</span><span class="sxs-lookup"><span data-stu-id="8e4e7-258">• Click</span></span><br><span data-ttu-id="8e4e7-259">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="8e4e7-259">• RecommendationClick</span></span><br><span data-ttu-id="8e4e7-260">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="8e4e7-260">•    AddShopCart</span></span><br><span data-ttu-id="8e4e7-261">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="8e4e7-261">• RemoveShopCart</span></span><br><span data-ttu-id="8e4e7-262">• Compra</span><span class="sxs-lookup"><span data-stu-id="8e4e7-262">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="8e4e7-263">O tamanho máximo do arquivo é de 200 MB.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-263">Maximum file size is 200MB.</span></span><br><br><span data-ttu-id="8e4e7-264">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-264">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="8e4e7-265">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-265">**Response**:</span></span>

<span data-ttu-id="8e4e7-266">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="8e4e7-266">HTTP Status code: 200</span></span>

* <span data-ttu-id="8e4e7-267">`Feed\entry\content\properties\LineCount` – O número de linhas aceitas.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-267">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="8e4e7-268">`Feed\entry\content\properties\ErrorCount`-Número de linhas que não foram inseridas devido a erro tooan.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-268">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="8e4e7-269">`Feed\entry\content\properties\FileId` – Identificador do arquivo.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-269">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="8e4e7-270">XML de OData</span><span class="sxs-lookup"><span data-stu-id="8e4e7-270">OData XML</span></span>

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


#### <a name="using-data-acquisition"></a><span data-ttu-id="8e4e7-271">Usando a aquisição de dados</span><span class="sxs-lookup"><span data-stu-id="8e4e7-271">Using data acquisition</span></span>
<span data-ttu-id="8e4e7-272">Esta seção mostra como eventos toosend real tempo recomendações tooAzure de aprendizado de máquina, normalmente a partir de seu site.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-272">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="8e4e7-273">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="8e4e7-273">HTTP Method</span></span> | <span data-ttu-id="8e4e7-274">URI</span><span class="sxs-lookup"><span data-stu-id="8e4e7-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e4e7-275">POST</span><span class="sxs-lookup"><span data-stu-id="8e4e7-275">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="8e4e7-276">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="8e4e7-276">Parameter Name</span></span> | <span data-ttu-id="8e4e7-277">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="8e4e7-277">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e4e7-278">apiVersion</span><span class="sxs-lookup"><span data-stu-id="8e4e7-278">apiVersion</span></span> |<span data-ttu-id="8e4e7-279">1.0</span><span class="sxs-lookup"><span data-stu-id="8e4e7-279">1.0</span></span> |
|  | |
| <span data-ttu-id="8e4e7-280">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="8e4e7-280">Request body</span></span> |<span data-ttu-id="8e4e7-281">Entrada de dados de evento para cada evento que você deseja toosend.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-281">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="8e4e7-282">Você deve enviar para a mesma sessão de usuário ou navegador Olá Olá mesmo ID nesse campo de SessionId hello.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-282">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="8e4e7-283">(Consulte o exemplo de corpo de evento abaixo.)</span><span class="sxs-lookup"><span data-stu-id="8e4e7-283">(See sample of event body below.)</span></span> |

* <span data-ttu-id="8e4e7-284">Exemplo de evento “Click”:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-284">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="8e4e7-285">Exemplo de evento “RecommendationClick”:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-285">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="8e4e7-286">Exemplo de evento “AddShopCart”:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-286">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="8e4e7-287">Exemplo de evento “RemoveShopCart”:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-287">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="8e4e7-288">Exemplo de evento “Purchase”:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-288">Example for event 'Purchase':</span></span>
  
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
* <span data-ttu-id="8e4e7-289">Exemplo de envio de dois eventos “Click” e “AddShopCart”:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-289">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="8e4e7-290">**Response**: código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="8e4e7-290">**Response**: HTTP Status code: 200</span></span>

### <a name="build-a-recommendation-model"></a><span data-ttu-id="8e4e7-291">Criar um modelo de recomendação</span><span class="sxs-lookup"><span data-stu-id="8e4e7-291">Build a recommendation model</span></span>
| <span data-ttu-id="8e4e7-292">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="8e4e7-292">HTTP Method</span></span> | <span data-ttu-id="8e4e7-293">URI</span><span class="sxs-lookup"><span data-stu-id="8e4e7-293">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e4e7-294">POST</span><span class="sxs-lookup"><span data-stu-id="8e4e7-294">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="8e4e7-295">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-295">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |

| <span data-ttu-id="8e4e7-296">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="8e4e7-296">Parameter Name</span></span> | <span data-ttu-id="8e4e7-297">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="8e4e7-297">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e4e7-298">modelId</span><span class="sxs-lookup"><span data-stu-id="8e4e7-298">modelId</span></span> |<span data-ttu-id="8e4e7-299">Identificador exclusivo do modelo de saudação (diferencia maiusculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="8e4e7-299">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="8e4e7-300">userDescription</span><span class="sxs-lookup"><span data-stu-id="8e4e7-300">userDescription</span></span> |<span data-ttu-id="8e4e7-301">Identificador textual do catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-301">Textual identifier of hello catalog.</span></span> <span data-ttu-id="8e4e7-302">Observe que se você usar espaços você deve codificá-los com 20%.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-302">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="8e4e7-303">Consulte o exemplo acima.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-303">See example above.</span></span><br><span data-ttu-id="8e4e7-304">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="8e4e7-304">Max length: 50</span></span> |
| <span data-ttu-id="8e4e7-305">apiVersion</span><span class="sxs-lookup"><span data-stu-id="8e4e7-305">apiVersion</span></span> |<span data-ttu-id="8e4e7-306">1.0</span><span class="sxs-lookup"><span data-stu-id="8e4e7-306">1.0</span></span> |
|  | |
| <span data-ttu-id="8e4e7-307">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="8e4e7-307">Request Body</span></span> |<span data-ttu-id="8e4e7-308">NENHUM</span><span class="sxs-lookup"><span data-stu-id="8e4e7-308">NONE</span></span> |

<span data-ttu-id="8e4e7-309">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-309">**Response**:</span></span>

<span data-ttu-id="8e4e7-310">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="8e4e7-310">HTTP Status code: 200</span></span>

<span data-ttu-id="8e4e7-311">Esta é uma API assíncrona.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-311">This is an asynchronous API.</span></span> <span data-ttu-id="8e4e7-312">Você receberá uma ID de compilação como uma resposta.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-312">You will get a build ID as a response.</span></span> <span data-ttu-id="8e4e7-313">tooknow quando a compilação Olá terminou, você deve chamar hello "Obter compilações Status de um modelo de" API e localize essa compilação ID na resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-313">tooknow when hello build has ended, you should call hello "Get Builds Status of a Model" API and locate this build ID in hello response.</span></span> <span data-ttu-id="8e4e7-314">Observe que uma compilação pode levar de toohours minutos dependendo do tamanho de saudação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-314">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="8e4e7-315">Você não pode consumir recomendações até Olá compilar termina.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-315">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="8e4e7-316">Status de compilação válidos:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-316">Valid build status:</span></span>

* <span data-ttu-id="8e4e7-317">Criado – O modelo foi criado.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-317">Create – Model was created.</span></span>
* <span data-ttu-id="8e4e7-318">Na fila – A compilação do modelo foi disparada e está na fila.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-318">Queued – Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="8e4e7-319">Criando – O modelo está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-319">Building – Model is being built.</span></span>
* <span data-ttu-id="8e4e7-320">Sucesso – A compilação concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-320">Success – Build ended successfully.</span></span>
* <span data-ttu-id="8e4e7-321">Erro – A compilação foi concluída com uma falha.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-321">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="8e4e7-322">Cancelado – A compilação foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-322">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="8e4e7-323">Cancelando – A compilação está sendo cancelada.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-323">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="8e4e7-324">Observe que compilação Olá que ID pode ser encontrada em Olá que caminho a seguir:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="8e4e7-324">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="8e4e7-325">XML de OData</span><span class="sxs-lookup"><span data-stu-id="8e4e7-325">OData XML</span></span>

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

### <a name="get-build-status-of-a-model"></a><span data-ttu-id="8e4e7-326">Obter status da compilação de um modelo</span><span class="sxs-lookup"><span data-stu-id="8e4e7-326">Get build status of a model</span></span>
| <span data-ttu-id="8e4e7-327">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="8e4e7-327">HTTP Method</span></span> | <span data-ttu-id="8e4e7-328">URI</span><span class="sxs-lookup"><span data-stu-id="8e4e7-328">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e4e7-329">GET</span><span class="sxs-lookup"><span data-stu-id="8e4e7-329">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="8e4e7-330">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-330">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="8e4e7-331">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="8e4e7-331">Parameter Name</span></span> | <span data-ttu-id="8e4e7-332">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="8e4e7-332">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e4e7-333">modelId</span><span class="sxs-lookup"><span data-stu-id="8e4e7-333">modelId</span></span> |<span data-ttu-id="8e4e7-334">Identificador exclusivo do modelo de saudação (diferencia maiusculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="8e4e7-334">Unique identifier of hello model  (case-sensitive)</span></span> |
| <span data-ttu-id="8e4e7-335">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="8e4e7-335">onlyLastBuild</span></span> |<span data-ttu-id="8e4e7-336">Indica se tooreturn todos Olá criar histórico do modelo de saudação ou somente status de saudação da compilação mais recente do hello.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-336">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="8e4e7-337">apiVersion</span><span class="sxs-lookup"><span data-stu-id="8e4e7-337">apiVersion</span></span> |<span data-ttu-id="8e4e7-338">1.0</span><span class="sxs-lookup"><span data-stu-id="8e4e7-338">1.0</span></span> |

<span data-ttu-id="8e4e7-339">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-339">**Response**:</span></span>

<span data-ttu-id="8e4e7-340">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="8e4e7-340">HTTP Status code: 200</span></span>

<span data-ttu-id="8e4e7-341">resposta de saudação inclui uma entrada por compilação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-341">hello response includes one entry per build.</span></span> <span data-ttu-id="8e4e7-342">Cada entrada tem Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-342">Each entry has hello following data:</span></span>

* <span data-ttu-id="8e4e7-343">`feed/entry/content/properties/UserName`– Nome do usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-343">`feed/entry/content/properties/UserName` – Name of hello user.</span></span>
* <span data-ttu-id="8e4e7-344">`feed/entry/content/properties/ModelName`– Nome do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-344">`feed/entry/content/properties/ModelName` – Name of hello model.</span></span>
* <span data-ttu-id="8e4e7-345">`feed/entry/content/properties/ModelId` – Identificador exclusivo do modelo.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-345">`feed/entry/content/properties/ModelId` – Model unique identifier.</span></span>
* <span data-ttu-id="8e4e7-346">`feed/entry/content/properties/IsDeployed`– Se o build Olá é implantado (também conhecido como</span><span class="sxs-lookup"><span data-stu-id="8e4e7-346">`feed/entry/content/properties/IsDeployed` – Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="8e4e7-347">compilação ativa).</span><span class="sxs-lookup"><span data-stu-id="8e4e7-347">active build).</span></span>
* <span data-ttu-id="8e4e7-348">`feed/entry/content/properties/BuildId` – Identificador exclusivo da compilação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-348">`feed/entry/content/properties/BuildId` – Build unique identifier.</span></span>
* <span data-ttu-id="8e4e7-349">`feed/entry/content/properties/BuildType`-Tipo de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-349">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="8e4e7-350">`feed/entry/content/properties/Status` – Status da compilação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-350">`feed/entry/content/properties/Status` – Build status.</span></span> <span data-ttu-id="8e4e7-351">Pode ser uma das seguintes Olá: erro, construção, na fila, cancelar, cancelado, sucesso</span><span class="sxs-lookup"><span data-stu-id="8e4e7-351">Can be one of hello following: Error, Building, Queued, Canceling, Canceled, Success</span></span>
* <span data-ttu-id="8e4e7-352">`feed/entry/content/properties/StatusMessage`– Mensagem de status detalhadas (aplica-se somente os estados de toospecific).</span><span class="sxs-lookup"><span data-stu-id="8e4e7-352">`feed/entry/content/properties/StatusMessage` – Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="8e4e7-353">`feed/entry/content/properties/Progress` – Andamento da compilação (%).</span><span class="sxs-lookup"><span data-stu-id="8e4e7-353">`feed/entry/content/properties/Progress` – Build progress (%).</span></span>
* <span data-ttu-id="8e4e7-354">`feed/entry/content/properties/StartTime` – Hora de início da compilação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-354">`feed/entry/content/properties/StartTime` – Build start time.</span></span>
* <span data-ttu-id="8e4e7-355">`feed/entry/content/properties/EndTime` – Hora de término da compilação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-355">`feed/entry/content/properties/EndTime` – Build end time.</span></span>
* <span data-ttu-id="8e4e7-356">`feed/entry/content/properties/ExecutionTime` – Duração da compilação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-356">`feed/entry/content/properties/ExecutionTime` – Build duration.</span></span>
* <span data-ttu-id="8e4e7-357">`feed/entry/content/properties/ProgressStep`– Os detalhes sobre o estágio atual de saudação que é uma compilação em andamento no.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-357">`feed/entry/content/properties/ProgressStep` – Details about hello current stage that a build in progress is in.</span></span>

<span data-ttu-id="8e4e7-358">Status de compilação válidos:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-358">Valid build status:</span></span>

* <span data-ttu-id="8e4e7-359">Criada - a entrada da solicitação de compilação foi criada.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-359">Created – Build request entry was created.</span></span>
* <span data-ttu-id="8e4e7-360">Em fila – a solicitação de build foi disparada e está na fila.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-360">Queued – Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="8e4e7-361">Compilando – a build está em andamento.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-361">Building – Build is in process.</span></span>
* <span data-ttu-id="8e4e7-362">Sucesso – A compilação concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-362">Success – Build ended successfully.</span></span>
* <span data-ttu-id="8e4e7-363">Erro – A compilação foi concluída com uma falha.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-363">Error – Build ended with a failure.</span></span>
* <span data-ttu-id="8e4e7-364">Cancelado – A compilação foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-364">Canceled – Build was canceled.</span></span>
* <span data-ttu-id="8e4e7-365">Cancelando – A compilação está sendo cancelada.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-365">Canceling – Build is being canceled.</span></span>

<span data-ttu-id="8e4e7-366">Valores válidos para o tipo de compilação:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-366">Valid values for build type:</span></span>

* <span data-ttu-id="8e4e7-367">Classificação - compilação de classificação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-367">Rank - Rank build.</span></span> <span data-ttu-id="8e4e7-368">(Detalhes da compilação para classificação, consulte o documento de "Documentação de recomendação de aprendizado de máquina API" toohello).</span><span class="sxs-lookup"><span data-stu-id="8e4e7-368">(For rank build details, please refer toohello "Machine Learning Recommendation API documentation" document.)</span></span>
* <span data-ttu-id="8e4e7-369">Recomendação - compilação de recomendação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-369">Recommendation - Recommendation build.</span></span>
* <span data-ttu-id="8e4e7-370">Fbt - Build de frequentemente comprados juntos.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-370">Fbt - Frequently bought together build.</span></span>

<span data-ttu-id="8e4e7-371">XML de OData</span><span class="sxs-lookup"><span data-stu-id="8e4e7-371">OData XML</span></span>

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


### <a name="get-recommendations"></a><span data-ttu-id="8e4e7-372">Obter recomendações</span><span class="sxs-lookup"><span data-stu-id="8e4e7-372">Get recommendations</span></span>
| <span data-ttu-id="8e4e7-373">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="8e4e7-373">HTTP Method</span></span> | <span data-ttu-id="8e4e7-374">URI</span><span class="sxs-lookup"><span data-stu-id="8e4e7-374">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e4e7-375">GET</span><span class="sxs-lookup"><span data-stu-id="8e4e7-375">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="8e4e7-376">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-376">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="8e4e7-377">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="8e4e7-377">Parameter Name</span></span> | <span data-ttu-id="8e4e7-378">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="8e4e7-378">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e4e7-379">modelId</span><span class="sxs-lookup"><span data-stu-id="8e4e7-379">modelId</span></span> |<span data-ttu-id="8e4e7-380">Identificador exclusivo do modelo de saudação (diferencia maiusculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="8e4e7-380">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="8e4e7-381">itemIds</span><span class="sxs-lookup"><span data-stu-id="8e4e7-381">itemIds</span></span> |<span data-ttu-id="8e4e7-382">Lista separada por vírgulas de saudação itens toorecommend para.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-382">Comma-separated list of hello items toorecommend for.</span></span><br><span data-ttu-id="8e4e7-383">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="8e4e7-383">Max length: 1024</span></span> |
| <span data-ttu-id="8e4e7-384">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="8e4e7-384">numberOfResults</span></span> |<span data-ttu-id="8e4e7-385">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="8e4e7-385">Number of required results</span></span> |
| <span data-ttu-id="8e4e7-386">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="8e4e7-386">includeMetatadata</span></span> |<span data-ttu-id="8e4e7-387">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="8e4e7-387">Future use, always false</span></span> |
| <span data-ttu-id="8e4e7-388">apiVersion</span><span class="sxs-lookup"><span data-stu-id="8e4e7-388">apiVersion</span></span> |<span data-ttu-id="8e4e7-389">1.0</span><span class="sxs-lookup"><span data-stu-id="8e4e7-389">1.0</span></span> |

<span data-ttu-id="8e4e7-390">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="8e4e7-390">**Response:**</span></span>

<span data-ttu-id="8e4e7-391">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="8e4e7-391">HTTP Status code: 200</span></span>

<span data-ttu-id="8e4e7-392">resposta de saudação inclui uma entrada por itens recomendados.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-392">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="8e4e7-393">Cada entrada tem Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-393">Each entry has hello following data:</span></span>

* <span data-ttu-id="8e4e7-394">`Feed\entry\content\properties\Id` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-394">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="8e4e7-395">`Feed\entry\content\properties\Name`-Nome do item de saudação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-395">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="8e4e7-396">`Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-396">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="8e4e7-397">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="8e4e7-397">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (for example, recommendation explanations).</span></span>

<span data-ttu-id="8e4e7-398">XML de OData</span><span class="sxs-lookup"><span data-stu-id="8e4e7-398">OData XML</span></span>

<span data-ttu-id="8e4e7-399">resposta de exemplo Hello abaixo inclui 10 itens recomendados:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-399">hello example response below includes 10 recommended items:</span></span>

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

### <a name="update-model"></a><span data-ttu-id="8e4e7-400">Atualizar modelo</span><span class="sxs-lookup"><span data-stu-id="8e4e7-400">Update model</span></span>
<span data-ttu-id="8e4e7-401">Você pode atualizar a descrição do modelo hello ou Olá ID do ativo de compilação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-401">You can update hello model description or hello active build ID.</span></span>
<span data-ttu-id="8e4e7-402">*ID de compilação ativa* – cada compilação para cada modelo tem uma ID de compilação.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-402">*Active build ID* - Every build for every model has a build ID.</span></span> <span data-ttu-id="8e4e7-403">ID de compilação active Olá é Olá primeira compilação bem-sucedida cada novo modelo.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-403">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="8e4e7-404">Depois que você tiver uma ID de ativo de compilação e fazer compilações adicionais para Olá mesmo modelo, você precisa tooexplicitly defini-lo hello padrão criar ID se desejar.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-404">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="8e4e7-405">Quando você consome recomendações, se você não especificar a ID de compilação de saudação que você deseja toouse, padrão Olá um será usado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-405">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span>

<span data-ttu-id="8e4e7-406">Esse mecanismo permite que você - depois de um modelo de recomendação em produção - toobuild novos modelos e testá-las antes de promovê-los tooproduction.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-406">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="8e4e7-407">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="8e4e7-407">HTTP Method</span></span> | <span data-ttu-id="8e4e7-408">URI</span><span class="sxs-lookup"><span data-stu-id="8e4e7-408">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e4e7-409">PUT</span><span class="sxs-lookup"><span data-stu-id="8e4e7-409">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="8e4e7-410">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-410">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="8e4e7-411">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="8e4e7-411">Parameter Name</span></span> | <span data-ttu-id="8e4e7-412">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="8e4e7-412">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="8e4e7-413">ID</span><span class="sxs-lookup"><span data-stu-id="8e4e7-413">id</span></span> |<span data-ttu-id="8e4e7-414">Identificador exclusivo do modelo de saudação (diferencia maiusculas de minúsculas)</span><span class="sxs-lookup"><span data-stu-id="8e4e7-414">Unique identifier of hello model (case-sensitive)</span></span> |
| <span data-ttu-id="8e4e7-415">apiVersion</span><span class="sxs-lookup"><span data-stu-id="8e4e7-415">apiVersion</span></span> |<span data-ttu-id="8e4e7-416">1.0</span><span class="sxs-lookup"><span data-stu-id="8e4e7-416">1.0</span></span> |
|  | |
| <span data-ttu-id="8e4e7-417">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="8e4e7-417">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`   <Description>New Description</Description>`<br>`          <ActiveBuildId>-1</ActiveBuildId>`<br>`</ModelUpdateParams>`<br><br><span data-ttu-id="8e4e7-418">Observe que a descrição de marcas Olá XML e ActiveBuildId são opcionais.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-418">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="8e4e7-419">Se você não quiser tooset descrição ou ActiveBuildId, remova a marca de inteiro de hello.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-419">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="8e4e7-420">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="8e4e7-420">**Response**:</span></span>

<span data-ttu-id="8e4e7-421">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="8e4e7-421">HTTP Status code: 200</span></span>

<span data-ttu-id="8e4e7-422">XML de OData</span><span class="sxs-lookup"><span data-stu-id="8e4e7-422">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Update an Existing Model</subtitle>
      <id>https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T10:27:17Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/Data.ashx/amla/recommendations/v2/UpdateModel?id='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;apiVersion='1.0'" />
    </feed>

## <a name="legal"></a><span data-ttu-id="8e4e7-423">Legal</span><span class="sxs-lookup"><span data-stu-id="8e4e7-423">Legal</span></span>
<span data-ttu-id="8e4e7-424">Este documento é fornecido "no estado em que se encontra".</span><span class="sxs-lookup"><span data-stu-id="8e4e7-424">This document is provided "as-is".</span></span> <span data-ttu-id="8e4e7-425">As informações e opiniões expressadas neste documento, incluindo URLs e outras referências a sites da Internet, podem ser alteradas sem aviso prévio.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-425">Information and views expressed in this document, including URL and other Internet website references, may change without notice.</span></span> <span data-ttu-id="8e4e7-426">Alguns exemplos aqui representados são fornecidos somente para fins de ilustração e são fictícios.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-426">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="8e4e7-427">Nenhuma associação ou conexão real é intencional ou deve ser inferida.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-427">No real association or connection is intended or should be inferred.</span></span> <span data-ttu-id="8e4e7-428">Este documento não dá nenhum direito legal tooany de propriedade intelectual de nenhum produto da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-428">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="8e4e7-429">Você pode copiar e usar este documento para fins de consulta interna.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-429">You may copy and use this document for your internal, reference purposes.</span></span> <span data-ttu-id="8e4e7-430">© 2014 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-430">© 2014 Microsoft.</span></span> <span data-ttu-id="8e4e7-431">Todos os direitos reservados.</span><span class="sxs-lookup"><span data-stu-id="8e4e7-431">All rights reserved.</span></span> 

