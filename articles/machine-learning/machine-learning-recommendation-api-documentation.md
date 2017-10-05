---
title: "Documentação da API de Recomendações do Machine Learning | Microsoft Docs"
description: "Documentação da API de Recomendações de Azure Machine Learning para um mecanismo de recomendações disponível no Microsoft Azure Marketplace."
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: 32c3ab2f-fdd7-48cc-b501-ad55c79b87dc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: LuisCa
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: TRUE
ms.openlocfilehash: 1fba64d78d779344e2895b0d54419186b7584865
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a><span data-ttu-id="c1e6d-103">Documentação da API de Recomendações do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c1e6d-103">Azure Machine Learning Recommendations API Documentation</span></span>
> [!NOTE]
> <span data-ttu-id="c1e6d-104">Você deve começar a usar o Serviço Cognitivo da API de Recomendações em vez desta versão.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="c1e6d-105">O Serviço Cognitivo de Recomendações substituirá esse serviço, e todos os recursos novos serão desenvolvidos lá.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="c1e6d-106">Ele possui novos recursos como suporte ao processamento em lotes, um Gerenciador de API aprimorado, uma superfície de API mais limpa, uma experiência de inscrição/cobrança mais consistente etc.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="c1e6d-107">Saiba mais sobre [Como migrar para o novo Serviço Cognitivo](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="c1e6d-108">Este documento descreve as APIs de Recomendações do Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="c1e6d-109">1. Visão geral</span><span class="sxs-lookup"><span data-stu-id="c1e6d-109">1. General overview</span></span>
<span data-ttu-id="c1e6d-110">Este documento é uma referência para a API.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-110">This document is an API reference.</span></span> <span data-ttu-id="c1e6d-111">Você deve começar pelo documento "Recomendação do Azure Machine Learning - Início Rápido".</span><span class="sxs-lookup"><span data-stu-id="c1e6d-111">You should start with the “Azure Machine Learning Recommendation - Quick Start” document.</span></span>

<span data-ttu-id="c1e6d-112">A API de Recomendações do Azure Machine Learning pode ser dividida nos seguintes grupos lógicos:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-112">The Azure Machine Learning Recommendations API can be divided into the following logical groups:</span></span>

* <span data-ttu-id="c1e6d-113"><ins>Limitações</ins> - limitações da API de recomendações.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-113"><ins>Limitations</ins> - Recommendations API limitations.</span></span>
* <span data-ttu-id="c1e6d-114"><ins>Informações gerais</ins> -informações sobre autenticação, controle de versão e URI de serviço.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span></span>
* <span data-ttu-id="c1e6d-115"><ins>Modelo Básico</ins> - APIs que permitem realizar operações básicas no modelo (por exemplo, criar, atualizar e excluir um modelo).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-115"><ins>Model Basic</ins> - APIs that enable you to do the basic operations on model (e.g. create, update and delete a model).</span></span>
* <span data-ttu-id="c1e6d-116"><ins>Modelo Avançado</ins> - APIs que permitem aprofundar-se nos dados avançados no modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-116"><ins>Model Advanced</ins> - APIs that enable you to get advanced data insights on the model.</span></span>
* <span data-ttu-id="c1e6d-117"><ins>Modelo de Regras de Negócio</ins> - APIs que permitem gerenciar regras comerciais dos resultados de recomendação do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-117"><ins>Model Business Rules</ins> - APIs that enable you to manage business rules on the model recommendation results.</span></span>
* <span data-ttu-id="c1e6d-118"><ins>Catálogo</ins> - APIs que permitem executar operações básicas em um catálogo de modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-118"><ins>Catalog</ins> - APIs that enable you to do basic operations on a model catalog.</span></span> <span data-ttu-id="c1e6d-119">Um catálogo contém informações de metadados sobre os itens dos dados de uso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-119">A catalog contains metadata information on the items of the usage data.</span></span>
* <span data-ttu-id="c1e6d-120"><ins>Recurso</ins> - APIs que permitem obter informações no item presente no catálogo e como usar essas informações para criar recomendações melhores.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-120"><ins>Feature</ins> - APIs that enable to get insights on item into the catalog and how to use this information to build better recommendations.</span></span>
* <span data-ttu-id="c1e6d-121"><ins>Dados de uso</ins> - APIs que permitem executar operações básicas com os dados de uso do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-121"><ins>Usage Data</ins> - APIs that enable you to do basic operations on the model usage data.</span></span> <span data-ttu-id="c1e6d-122">Os dados de uso no formulário básico são formados por linhas que incluem pares de &#60;usuárioId&#62;,&#60;itemId&#62;.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-122">Usage data in the basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span></span>
* <span data-ttu-id="c1e6d-123"><ins>Compilação</ins> - APIs que permitem disparar uma compilação de modelo e realizam operações básicas relacionadas a essa compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-123"><ins>Build</ins> - APIs that enable you to trigger a model build and do basic operations that are related to this build.</span></span> <span data-ttu-id="c1e6d-124">Você pode iniciar uma compilação de modelo uma vez que você tenha dados de uso valiosos.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-124">You can trigger a model build once you have valuable usage data.</span></span>
* <span data-ttu-id="c1e6d-125"><ins>Recomendação</ins> - após a compilação de um modelo terminar, você pode consumir recomendações usando essas APIs.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-125"><ins>Recommendation</ins> - APIs that enable you to consume recommendations once the build of a model ends.</span></span>
* <span data-ttu-id="c1e6d-126"><ins>Dados de usuário</ins> - APIs que permitem que você busque informações sobre os dados de uso do usuário.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-126"><ins>User Data</ins> - APIs that enable you to fetch information on the user usage data.</span></span>
* <span data-ttu-id="c1e6d-127"><ins>Notificações</ins> - APIs que permitem receber notificações sobre problemas relacionados às suas operações de API.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-127"><ins>Notifications</ins> - APIs that enable you to receive notifications on problems related to your API operations.</span></span> <span data-ttu-id="c1e6d-128">(Por exemplo, você está reportando dados de uso por meio da aquisição de dados e a maioria dos eventos de processamento está com falha.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-128">(For example, you are reporting usage data via Data Acquisition and most of the events processing are failing.</span></span> <span data-ttu-id="c1e6d-129">Uma notificação de erro será gerada.)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-129">An error notification will be raised.)</span></span>

## <a name="2-limitations"></a><span data-ttu-id="c1e6d-130">2. Limitações</span><span class="sxs-lookup"><span data-stu-id="c1e6d-130">2. Limitations</span></span>
* <span data-ttu-id="c1e6d-131">O número máximo de modelos por assinatura é 10.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-131">The maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="c1e6d-132">O número máximo de builds por modelo é 20.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-132">The maximum number of builds per model is 20.</span></span>
* <span data-ttu-id="c1e6d-133">O número máximo de itens que um catálogo pode conter é 100.000.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-133">The maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="c1e6d-134">O número máximo de pontos de uso mantidos é cerca de 5.000.000.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-134">The maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="c1e6d-135">Os mais antigos serão excluídos se novos forem carregados ou relatados.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-135">The oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="c1e6d-136">O volume máximo dos dados que podem ser enviado no POST (por exemplo, importar dados de catálogo e importar dados de uso) é de 200 MB.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-136">The maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="c1e6d-137">O número máximo de itens que podem ser solicitados ao obter recomendações é 150.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-137">The maximum number of items that can be asked for when getting recommendations is 150.</span></span>

## <a name="3-apis---general-information"></a><span data-ttu-id="c1e6d-138">3. APIs – Informações Gerais</span><span class="sxs-lookup"><span data-stu-id="c1e6d-138">3. APIs - general information</span></span>
### <a name="31-authentication"></a><span data-ttu-id="c1e6d-139">3.1.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-139">3.1.</span></span> <span data-ttu-id="c1e6d-140">Autenticação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-140">Authentication</span></span>
<span data-ttu-id="c1e6d-141">Siga as diretrizes do Microsoft Azure Marketplace referentes à autenticação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-141">Please follow the Microsoft Azure Marketplace guidelines regarding authentication.</span></span> <span data-ttu-id="c1e6d-142">O Marketplace dá suporte aos métodos de autenticação Básico e OAuth.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-142">The marketplace supports either the Basic or OAuth authentication method.</span></span>

### <a name="32-service-uri"></a><span data-ttu-id="c1e6d-143">3.2.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-143">3.2.</span></span> <span data-ttu-id="c1e6d-144">URI de serviço</span><span class="sxs-lookup"><span data-stu-id="c1e6d-144">Service URI</span></span>
<span data-ttu-id="c1e6d-145">O URI da raiz de serviço para as APIs de Recomendações do Azure Machine Learning está [aqui.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-145">The service root URI for the Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span></span>

<span data-ttu-id="c1e6d-146">O URI do serviço completo é expresso usando elementos da especificação de OData.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-146">The full service URI is expressed using elements of the OData specification.</span></span>  

### <a name="33-api-version"></a><span data-ttu-id="c1e6d-147">3.3.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-147">3.3.</span></span> <span data-ttu-id="c1e6d-148">Versão da API</span><span class="sxs-lookup"><span data-stu-id="c1e6d-148">API version</span></span>
<span data-ttu-id="c1e6d-149">Cada chamada à API terá, por fim, um parâmetro de consulta chamado apiVersion que deve ser definido como 1.0.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-149">Each API call will have, at the end, a query parameter called apiVersion that should be set to 1.0.</span></span>

### <a name="34-ids-are-case-sensitive"></a><span data-ttu-id="c1e6d-150">3.4.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-150">3.4.</span></span> <span data-ttu-id="c1e6d-151">IDs diferenciam minúsculas e maiúsculas</span><span class="sxs-lookup"><span data-stu-id="c1e6d-151">IDs are case sensitive</span></span>
<span data-ttu-id="c1e6d-152">IDs, retornados por qualquer uma das APIS, diferenciam minúsculas de maiúsculas e devem ser usados desta maneira quando passados como parâmetros nas chamadas de API subsequentes.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-152">IDs, returned by any of the APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="c1e6d-153">Por exemplo, IDS d modelo e de catálogo diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-153">For instance, model IDs and catalog IDs are case sensitive.</span></span>

## <a name="4-recommendations-quality-and-cold-items"></a><span data-ttu-id="c1e6d-154">4. Qualidade das recomendações e itens frios</span><span class="sxs-lookup"><span data-stu-id="c1e6d-154">4. Recommendations Quality and Cold Items</span></span>
### <a name="41-recommendation-quality"></a><span data-ttu-id="c1e6d-155">4.1.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-155">4.1.</span></span> <span data-ttu-id="c1e6d-156">Qualidade da recomendação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-156">Recommendation quality</span></span>
<span data-ttu-id="c1e6d-157">Criar um modelo de recomendação geralmente é suficiente para permitir que o sistema forneça recomendações.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-157">Creating a recommendation model is usually enough to allow the system to provide recommendations.</span></span> <span data-ttu-id="c1e6d-158">No entanto, a qualidade da recomendação varia de acordo com o uso processado e a abrangência do catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-158">Nevertheless, recommendation quality varies based on the usage processed and the coverage of the catalog.</span></span> <span data-ttu-id="c1e6d-159">Por exemplo se você tiver muitos itens sem interesse (sem uso significativo), o sistema terá dificuldade para fornecer uma recomendação para um item ou para usar um item como aquele recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-159">For example if you have a lot of cold items (items without significant usage), the system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span></span> <span data-ttu-id="c1e6d-160">Para solucionar o problema de item sem interesse, o sistema permite o uso de metadados dos itens para aprimorar as recomendações.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-160">In order to overcome the cold item problem, the system allows the use of metadata of the items to enhance the recommendations.</span></span> <span data-ttu-id="c1e6d-161">Esses metadados são conhecidos como recursos.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-161">This metadata is referred to as features.</span></span> <span data-ttu-id="c1e6d-162">Os recursos mais comuns são o autor de um livro ou um ator de um filme.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-162">Typical features are a book's author or a movie's actor.</span></span> <span data-ttu-id="c1e6d-163">Recursos são fornecidos pelo catálogo na forma de cadeias de caracteres de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-163">Features are provided via the catalog in the form of key/value strings.</span></span> <span data-ttu-id="c1e6d-164">Para o formato completo do arquivo de catálogo, consulte a [seção de importação de catálogo](#81-import-catalog-data).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-164">For the full format of the catalog file, please refer to the [import catalog section](#81-import-catalog-data).</span></span> 

### <a name="42-rank-build"></a><span data-ttu-id="c1e6d-165">4.2.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-165">4.2.</span></span> <span data-ttu-id="c1e6d-166">Compilação de classificação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-166">Rank build</span></span>
<span data-ttu-id="c1e6d-167">Recursos podem aperfeiçoar o modelo de recomendação, mas isso requer o uso de recursos significativos.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-167">Features can enhance the recommendation model, but to do so requires the use of meaningful features.</span></span> <span data-ttu-id="c1e6d-168">Uma nova compilação foi apresentada para essa finalidade: uma compilação de classificação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-168">For this purpose a new build was introduced - a rank build.</span></span> <span data-ttu-id="c1e6d-169">Esta compilação classifica a utilidade dos recursos.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-169">This build will rank the usefulness of features.</span></span> <span data-ttu-id="c1e6d-170">Um recurso significativo é um recurso com uma pontuação de classificação 2 ou maior.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-170">A meaningful feature is a feature with a rank score of 2 and up.</span></span>
<span data-ttu-id="c1e6d-171">Depois de se entender quais recursos são significativos, dispare uma compilação de recomendação com a lista (ou sublista) de recursos significativos.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-171">After understanding which of the features are meaningful, trigger a recommendation build with the list (or sublist) of meaningful features.</span></span> <span data-ttu-id="c1e6d-172">É possível usar esses recursos para o aprimoramento de itens com e sem interesse.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-172">It is possible to use these feature for the enhancement of both warm items and cold items.</span></span> <span data-ttu-id="c1e6d-173">Para usá-los em itens com interesse, o parâmetro de compilação `UseFeatureInModel` deve ser configurado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-173">In order to use them for warm items, the `UseFeatureInModel` build parameter should be set up.</span></span> <span data-ttu-id="c1e6d-174">Para usá-los em itens sem interesse, o parâmetro de compilação `AllowColdItemPlacement` deve ser habilitado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-174">In order to use features for cold items, the `AllowColdItemPlacement` build parameter should be enabled.</span></span>
<span data-ttu-id="c1e6d-175">Observação: não é possível habilitar `AllowColdItemPlacement` sem habilitar `UseFeatureInModel`.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-175">Note: It is not possible to enable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span></span>

### <a name="43-recommendation-reasoning"></a><span data-ttu-id="c1e6d-176">4.3.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-176">4.3.</span></span> <span data-ttu-id="c1e6d-177">Raciocínio de recomendação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-177">Recommendation reasoning</span></span>
<span data-ttu-id="c1e6d-178">O raciocínio de recomendação é outro aspecto do uso de recursos.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-178">Recommendation reasoning is another aspect of feature usage.</span></span> <span data-ttu-id="c1e6d-179">Na verdade, o mecanismo de Recomendações do Azure Machine Learning pode usar recursos para fornecer explicações de recomendação (também conhecidas como</span><span class="sxs-lookup"><span data-stu-id="c1e6d-179">Indeed, the Azure Machine Learning Recommendations engine can use features to provide recommendation explanations (a.k.a.</span></span> <span data-ttu-id="c1e6d-180">raciocínio), gerando maior confiança do consumidor da recomendação no item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-180">reasoning), leading to more confidence in the recommended item from the recommendation consumer.</span></span>
<span data-ttu-id="c1e6d-181">Para habilitar o raciocínio, os parâmetros `AllowFeatureCorrelation` e `ReasoningFeatureList` devem ser configurado antes de solicitar uma compilação de recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-181">To enable reasoning, the `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior to requesting a recommendation build.</span></span>

## <a name="5-model-basic"></a><span data-ttu-id="c1e6d-182">5. Modelo Básico</span><span class="sxs-lookup"><span data-stu-id="c1e6d-182">5. Model Basic</span></span>
### <a name="51-create-model"></a><span data-ttu-id="c1e6d-183">5.1.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-183">5.1.</span></span> <span data-ttu-id="c1e6d-184">Criar modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-184">Create Model</span></span>
<span data-ttu-id="c1e6d-185">Cria uma solicitação "criar modelo".</span><span class="sxs-lookup"><span data-stu-id="c1e6d-185">Creates a “create model” request.</span></span>

| <span data-ttu-id="c1e6d-186">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-186">HTTP Method</span></span> | <span data-ttu-id="c1e6d-187">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-187">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-188">POST</span><span class="sxs-lookup"><span data-stu-id="c1e6d-188">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-189">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-189">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-190">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-190">Parameter Name</span></span> | <span data-ttu-id="c1e6d-191">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-191">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-192">modelName</span><span class="sxs-lookup"><span data-stu-id="c1e6d-192">modelName</span></span> |<span data-ttu-id="c1e6d-193">São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="c1e6d-194">Comprimento máximo: 20</span><span class="sxs-lookup"><span data-stu-id="c1e6d-194">Max length: 20</span></span> |
| <span data-ttu-id="c1e6d-195">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-195">apiVersion</span></span> |<span data-ttu-id="c1e6d-196">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-196">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-197">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-197">Request Body</span></span> |<span data-ttu-id="c1e6d-198">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-198">NONE</span></span> |

<span data-ttu-id="c1e6d-199">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-199">**Response**:</span></span>

<span data-ttu-id="c1e6d-200">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-200">HTTP Status code: 200</span></span>

* <span data-ttu-id="c1e6d-201">`feed/entry/content/properties/id` – Contém a ID do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-201">`feed/entry/content/properties/id` - Contains the model ID.</span></span>
  <span data-ttu-id="c1e6d-202">**Observação**: a ID do modelo diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-202">**Note**: model ID is case sensitive.</span></span>

<span data-ttu-id="c1e6d-203">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-203">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Create A New Model</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T06:35:21Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">CreateANewModelEntity2</title>
    <updated>2014-10-05T06:35:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/CreateModel?modelName='MyFirstModel'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="52-get-model"></a><span data-ttu-id="c1e6d-204">5.2.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-204">5.2.</span></span> <span data-ttu-id="c1e6d-205">Obter modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-205">Get Model</span></span>
<span data-ttu-id="c1e6d-206">Criar uma solicitação “obter modelo".</span><span class="sxs-lookup"><span data-stu-id="c1e6d-206">Creates a “get model” request.</span></span>

| <span data-ttu-id="c1e6d-207">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-207">HTTP Method</span></span> | <span data-ttu-id="c1e6d-208">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-208">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-209">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-209">GET</span></span> |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="c1e6d-210">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-210">Example:</span></span><br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-211">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-211">Parameter Name</span></span> | <span data-ttu-id="c1e6d-212">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-212">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-213">ID</span><span class="sxs-lookup"><span data-stu-id="c1e6d-213">id</span></span> |<span data-ttu-id="c1e6d-214">O identificador exclusivo do modelo (diferencia maiúsculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-214">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="c1e6d-215">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-215">apiVersion</span></span> |<span data-ttu-id="c1e6d-216">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-216">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-217">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-217">Request Body</span></span> |<span data-ttu-id="c1e6d-218">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-218">NONE</span></span> |

<span data-ttu-id="c1e6d-219">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-219">**Response**:</span></span>

<span data-ttu-id="c1e6d-220">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-220">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-221">Os dados do modelo podem ser encontrados sob os seguintes elementos:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-221">The model data can be found under the following elements:</span></span>

* <span data-ttu-id="c1e6d-222">`feed/entry/content/properties/Id` - ID exclusivo do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-222">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="c1e6d-223">`feed/entry/content/properties/Name` - Nome do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-223">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="c1e6d-224">`feed/entry/content/properties/Date` - Data de criação do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-224">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="c1e6d-225">`feed/entry/content/properties/Status` - Status do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-225">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="c1e6d-226">Um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-226">One of the following:</span></span>
  * <span data-ttu-id="c1e6d-227">Criado - O modelo é criado e não contém Catálogo e Uso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-227">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="c1e6d-228">ReadyForBuild - O modelo é criado e contém Catálogo e Uso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="c1e6d-229">`feed/entry/content/properties/HasActiveBuild` - Indica se o modelo foi criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if the model was built successfully.</span></span>
* <span data-ttu-id="c1e6d-230">`feed/entry/content/properties/BuildId` - ID da compilação ativa do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="c1e6d-231">`feed/entry/content/properties/Mpr` - Classificação porcentual média do modelo (MPR - consulte ModelInsight para obter mais informações).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span></span>
* <span data-ttu-id="c1e6d-232">`feed/entry/content/properties/UserName` - Nome do usuário interno do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-232">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>

<span data-ttu-id="c1e6d-233">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-233">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get A List Of All Models</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T14:35:51Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
        <d:Name m:type="Edm.String">vah-11111</d:Name>
        <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
        <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
        <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
        <d:BuildId m:type="Edm.String">-1</d:BuildId>
        <d:Mpr m:type="Edm.String">0</d:Mpr>
        <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
        <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
        <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
        <d:Description m:type="Edm.String">short description</d:Description>
        <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="53----get-all-models"></a><span data-ttu-id="c1e6d-234">5.3.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-234">5.3.</span></span>    <span data-ttu-id="c1e6d-235">Obter todos os modelos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-235">Get All Models</span></span>
<span data-ttu-id="c1e6d-236">Recupera todos os modelos do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-236">Retrieves all models of the current user.</span></span>

| <span data-ttu-id="c1e6d-237">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-237">HTTP Method</span></span> | <span data-ttu-id="c1e6d-238">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-238">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-239">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-239">GET</span></span> |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br><span data-ttu-id="c1e6d-240">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-240">Example:</span></span><br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-241">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-241">Parameter Name</span></span> | <span data-ttu-id="c1e6d-242">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-242">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-243">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-243">apiVersion</span></span> |<span data-ttu-id="c1e6d-244">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-244">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-245">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-245">Request Body</span></span> |<span data-ttu-id="c1e6d-246">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-246">NONE</span></span> |

<span data-ttu-id="c1e6d-247">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-247">**Response**:</span></span>

<span data-ttu-id="c1e6d-248">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-248">HTTP Status code: 200</span></span>

* <span data-ttu-id="c1e6d-249">`feed/entry/content/properties/Id` - ID exclusivo do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-249">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="c1e6d-250">`feed/entry/content/properties/Name` - Nome do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-250">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="c1e6d-251">`feed/entry/content/properties/Date` - Data de criação do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-251">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="c1e6d-252">`feed/entry/content/properties/Status` - Status do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-252">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="c1e6d-253">Um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-253">One of the following:</span></span>
  * <span data-ttu-id="c1e6d-254">Criado - O modelo é criado e não contém Catálogo e Uso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-254">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="c1e6d-255">ReadyForBuild - O modelo é criado e contém Catálogo e Uso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="c1e6d-256">`feed/entry/content/properties/HasActiveBuild` - Indica se o modelo foi criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if the model was built successfully.</span></span>
* <span data-ttu-id="c1e6d-257">`feed/entry/content/properties/BuildId` - ID da compilação ativa do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="c1e6d-258">`feed/entry/content/properties/Mpr` - MPR do modelo MPR (consulte o ModelInsight para obter mais informações).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span></span>
* <span data-ttu-id="c1e6d-259">`feed/entry/content/properties/UserName` - Nome do usuário interno do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-259">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>
* <span data-ttu-id="c1e6d-260">`feed/entry/content/properties/UsageFileNames` - Lista de arquivos de uso do modelo separados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span></span>
* <span data-ttu-id="c1e6d-261">`feed/entry/content/properties/CatalogId` - ID do catálogo do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span></span>
* <span data-ttu-id="c1e6d-262">`feed/entry/content/properties/Description` - Descrição do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-262">`feed/entry/content/properties/Description` - Model description.</span></span>
* <span data-ttu-id="c1e6d-263">`feed/entry/content/properties/CatalogFileName` - Nome do arquivo do catálogo do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span></span>

<span data-ttu-id="c1e6d-264">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-264">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get A List Of All Models</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-28T14:35:51Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfAllModelsEntity</title>
    <updated>2014-10-28T14:35:51Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetAllModels?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">68b232f2-1037-45f7-8f49-af822695ee63</d:Id>
                    <d:Name m:type="Edm.String">vah-11111</d:Name>
                    <d:Date m:type="Edm.String">10/28/2014 2:16:07 PM</d:Date>
                    <d:Status m:type="Edm.String">ReadyForBuild</d:Status>
                    <d:HasActiveBuild m:type="Edm.String">false</d:HasActiveBuild>
                    <d:BuildId m:type="Edm.String">-1</d:BuildId>
                    <d:Mpr m:type="Edm.String">0</d:Mpr>
                    <d:UsageFileNames m:type="Edm.String">ImplicitMatrix10_Guid_small.txt, ImplicitMatrix11_Guid_small.txt</d:UsageFileNames>
                    <d:CatalogId m:type="Edm.String">626babdb-cab6-43a6-82ef-4fb86345700c</d:CatalogId>
                    <d:UserName m:type="Edm.String">89dc4722-03ba-4f90-8821-b1db388408b5@dm.com</d:UserName>
                    <d:Description m:type="Edm.String">short description</d:Description>
                    <d:CatalogFileName m:type="Edm.String">catalog10_small.txt</d:CatalogFileName>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="54----update-model"></a><span data-ttu-id="c1e6d-265">5.4.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-265">5.4.</span></span>    <span data-ttu-id="c1e6d-266">Atualizar modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-266">Update Model</span></span>
<span data-ttu-id="c1e6d-267">Você pode atualizar a descrição do modelo ou a ID de compilação ativa.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-267">You can update the model description or the active build ID.</span></span><br><span data-ttu-id="c1e6d-268">
<ins>ID de compilação ativa</ins> – cada compilação para cada modelo tem uma ID de compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-268">
<ins>Active build ID</ins> - Every build for every model has a build ID.</span></span> <span data-ttu-id="c1e6d-269">A ID de compilação ativa é a primeira compilação executada com êxito de cada novo modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-269">The active build ID is the first successful build of every new model.</span></span> <span data-ttu-id="c1e6d-270">Depois que tiver uma ID de compilação ativa e criar compilações adicionais para o mesmo modelo, você precisará defini-lo explicitamente como a ID de compilação padrão, se desejar.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-270">Once you have an active build ID and you do additional builds for the same model, you need to explicitly set it as the default build ID if you want to.</span></span> <span data-ttu-id="c1e6d-271">Ao consumir recomendações, se você não especificar a ID de compilação que deseja usar, o padrão será usado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-271">When you consume recommendations, if you do not specify the build ID that you want to use, the default one will be used automatically.</span></span><br>
<span data-ttu-id="c1e6d-272">Esse mecanismo permite, depois de ter um modelo de recomendação em produção, compilar e testar novos modelos antes de promovê-los para produção.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-272">This mechanism enables you - once you have a recommendation model in production - to build new models and test them before you promote them to production.</span></span>

| <span data-ttu-id="c1e6d-273">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-273">HTTP Method</span></span> | <span data-ttu-id="c1e6d-274">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-275">PUT</span><span class="sxs-lookup"><span data-stu-id="c1e6d-275">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><span data-ttu-id="c1e6d-276">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-276">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-277">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-277">Parameter Name</span></span> | <span data-ttu-id="c1e6d-278">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-278">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-279">ID</span><span class="sxs-lookup"><span data-stu-id="c1e6d-279">id</span></span> |<span data-ttu-id="c1e6d-280">O identificador exclusivo do modelo (diferencia maiúsculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-280">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="c1e6d-281">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-281">apiVersion</span></span> |<span data-ttu-id="c1e6d-282">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-282">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-283">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-283">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br><span data-ttu-id="c1e6d-284">Observe que as marcações XML Description e ActiveBuildId são opcionais.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-284">Note that the XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="c1e6d-285">Se você não quiser definir Description ou ActiveBuildId, remova a marca inteira.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-285">If you do not want to set Description or ActiveBuildId, remove the entire tag.</span></span> |

<span data-ttu-id="c1e6d-286">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-286">**Response**:</span></span>

<span data-ttu-id="c1e6d-287">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-287">HTTP Status code: 200</span></span>

### <a name="55----delete-model"></a><span data-ttu-id="c1e6d-288">5.5.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-288">5.5.</span></span>    <span data-ttu-id="c1e6d-289">Excluir modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-289">Delete Model</span></span>
<span data-ttu-id="c1e6d-290">Exclui um modelo existente por ID.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-290">Deletes an existing model by ID.</span></span>

| <span data-ttu-id="c1e6d-291">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-291">HTTP Method</span></span> | <span data-ttu-id="c1e6d-292">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-292">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-293">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="c1e6d-293">DELETE</span></span> |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="c1e6d-294">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-294">Example:</span></span><br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-295">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-295">Parameter Name</span></span> | <span data-ttu-id="c1e6d-296">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-296">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-297">ID</span><span class="sxs-lookup"><span data-stu-id="c1e6d-297">id</span></span> |<span data-ttu-id="c1e6d-298">O identificador exclusivo do modelo (diferencia maiúsculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-298">Unique identifier of the model (case sensitive)</span></span> |
| <span data-ttu-id="c1e6d-299">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-299">apiVersion</span></span> |<span data-ttu-id="c1e6d-300">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-300">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-301">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-301">Request Body</span></span> |<span data-ttu-id="c1e6d-302">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-302">NONE</span></span> |

<span data-ttu-id="c1e6d-303">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-303">**Response**:</span></span>

<span data-ttu-id="c1e6d-304">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-304">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-305">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-305">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Delete Model by Id</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-28T10:39:33Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">DeleteModelByIdEntity</title>
    <updated>2014-10-28T10:39:33Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/DeleteModel?id='1cac7b76-def4-41f1-bc81-29b806adb1de'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:string m:type="Edm.String"></d:string>
      </m:properties>
    </content>
      </entry>
    </feed>

## <a name="6-model-advanced"></a><span data-ttu-id="c1e6d-306">6. Modelo Avançado</span><span class="sxs-lookup"><span data-stu-id="c1e6d-306">6. Model Advanced</span></span>
### <a name="61----model-data-insight"></a><span data-ttu-id="c1e6d-307">6.1.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-307">6.1.</span></span>    <span data-ttu-id="c1e6d-308">Visão de modelo de dados</span><span class="sxs-lookup"><span data-stu-id="c1e6d-308">Model Data Insight</span></span>
<span data-ttu-id="c1e6d-309">Retorna dados estatísticos sobre os dados com os quais este modelo foi criado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-309">Returns statistical data on the usage data that this model was built with.</span></span>

<span data-ttu-id="c1e6d-310">Disponível somente para compilação de Recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-310">Available only for Recommendation build.</span></span>

| <span data-ttu-id="c1e6d-311">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-311">HTTP Method</span></span> | <span data-ttu-id="c1e6d-312">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-312">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-313">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-313">GET</span></span> |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="c1e6d-314">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-314">Example:</span></span><br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-315">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-315">Parameter Name</span></span> | <span data-ttu-id="c1e6d-316">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-316">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-317">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-317">modelId</span></span> |<span data-ttu-id="c1e6d-318">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-318">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-319">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-319">apiVersion</span></span> |<span data-ttu-id="c1e6d-320">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-320">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-321">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-321">Request Body</span></span> |<span data-ttu-id="c1e6d-322">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-322">NONE</span></span> |

<span data-ttu-id="c1e6d-323">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-323">**Response**:</span></span>

<span data-ttu-id="c1e6d-324">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-324">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-325">Os dados são retornados como uma coleção de propriedades.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-325">The data is returned as a collection of properties.</span></span>

* <span data-ttu-id="c1e6d-326">`feed/entry/id/content/properties/key` - Contém o nome da propriedade.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-326">`feed/entry/id/content/properties/key` - Holds the property name.</span></span>
* <span data-ttu-id="c1e6d-327">`feed/entry/id/content/properties/value` - Contém o valor da propriedade.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-327">`feed/entry/id/content/properties/value` - Holds the property value.</span></span>

<span data-ttu-id="c1e6d-328">A tabela a seguir descreve o valor que cada chave representa.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-328">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="c1e6d-329">Chave</span><span class="sxs-lookup"><span data-stu-id="c1e6d-329">Key</span></span> | <span data-ttu-id="c1e6d-330">Descrição</span><span class="sxs-lookup"><span data-stu-id="c1e6d-330">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-331">AvgItemLength</span><span class="sxs-lookup"><span data-stu-id="c1e6d-331">AvgItemLength</span></span> |<span data-ttu-id="c1e6d-332">Média de usuários distintos por item.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-332">Average number of distinct users per item.</span></span> |
| <span data-ttu-id="c1e6d-333">AvgUserLength</span><span class="sxs-lookup"><span data-stu-id="c1e6d-333">AvgUserLength</span></span> |<span data-ttu-id="c1e6d-334">Média de itens distintos por usuários.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-334">Average number of distinct items per user.</span></span> |
| <span data-ttu-id="c1e6d-335">DensificationNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="c1e6d-335">DensificationNumberOfItems</span></span> |<span data-ttu-id="c1e6d-336">Número de itens após a remoção dos itens que não podem ser modelados.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-336">Number of items after pruning items that cannot be modelled.</span></span> |
| <span data-ttu-id="c1e6d-337">DensificationNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="c1e6d-337">DensificationNumberOfUsers</span></span> |<span data-ttu-id="c1e6d-338">Número de pontos de uso após a remoção de usuários e itens que não podem ser modelados.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-338">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="c1e6d-339">DensificationNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="c1e6d-339">DensificationNumberOfRecords</span></span> |<span data-ttu-id="c1e6d-340">Número de pontos de uso após a remoção de usuários e itens que não podem ser modelados.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-340">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="c1e6d-341">MaxItemLength</span><span class="sxs-lookup"><span data-stu-id="c1e6d-341">MaxItemLength</span></span> |<span data-ttu-id="c1e6d-342">Número de usuários distintos para o item mais popular.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-342">Number of distinct users for the most popular item.</span></span> |
| <span data-ttu-id="c1e6d-343">MaxUserLength</span><span class="sxs-lookup"><span data-stu-id="c1e6d-343">MaxUserLength</span></span> |<span data-ttu-id="c1e6d-344">Número máximo de itens distintos para um usuário.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-344">Maximal number of distinct items for a user.</span></span> |
| <span data-ttu-id="c1e6d-345">MinItemLength</span><span class="sxs-lookup"><span data-stu-id="c1e6d-345">MinItemLength</span></span> |<span data-ttu-id="c1e6d-346">Número máximo de usuários distintos para um item.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-346">Maximal number of distinct users for an item.</span></span> |
| <span data-ttu-id="c1e6d-347">MinUserLength</span><span class="sxs-lookup"><span data-stu-id="c1e6d-347">MinUserLength</span></span> |<span data-ttu-id="c1e6d-348">Número mínimo de itens distintos para um usuário.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-348">Minimal number of distinct items for a user.</span></span> |
| <span data-ttu-id="c1e6d-349">RawNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="c1e6d-349">RawNumberOfItems</span></span> |<span data-ttu-id="c1e6d-350">Número de itens nos arquivos de uso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-350">Number of items in the usage files.</span></span> |
| <span data-ttu-id="c1e6d-351">RawNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="c1e6d-351">RawNumberOfUsers</span></span> |<span data-ttu-id="c1e6d-352">Número de pontos de uso antes de qualquer remoção.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-352">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="c1e6d-353">RawNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="c1e6d-353">RawNumberOfRecords</span></span> |<span data-ttu-id="c1e6d-354">Número de pontos de uso antes de qualquer remoção.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-354">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="c1e6d-355">SamplingNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="c1e6d-355">SamplingNumberOfItems</span></span> |<span data-ttu-id="c1e6d-356">N/D</span><span class="sxs-lookup"><span data-stu-id="c1e6d-356">N/A</span></span> |
| <span data-ttu-id="c1e6d-357">SamplingNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="c1e6d-357">SamplingNumberOfRecords</span></span> |<span data-ttu-id="c1e6d-358">N/D</span><span class="sxs-lookup"><span data-stu-id="c1e6d-358">N/A</span></span> |
| <span data-ttu-id="c1e6d-359">SamplingNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="c1e6d-359">SamplingNumberOfUsers</span></span> |<span data-ttu-id="c1e6d-360">N/D</span><span class="sxs-lookup"><span data-stu-id="c1e6d-360">N/A</span></span> |

<span data-ttu-id="c1e6d-361">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-361">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get data insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgItemLength</d:Key>
        <d:Value m:type="Edm.String">18.936</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">AvgUserLength</d:Key>
        <d:Value m:type="Edm.String">51.879</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfItems</d:Key>
        <d:Value m:type="Edm.String">2,000</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Key m:type="Edm.String">DensificationNumberOfRecords</d:Key>
        <d:Value m:type="Edm.String">37,872</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetDataInsightStatisticsEntity</title>
    <updated>2014-10-27T14:21:21Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
    <content type="application/xml">
        <m:properties>
            <d:Key m:type="Edm.String">DensificationNumberOfUsers</d:Key>
            <d:Value m:type="Edm.String">730</d:Value>
      </m:properties>
    </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxItemLength</d:Key>
                <d:Value m:type="Edm.String">4,704</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MaxUserLength</d:Key>
                <d:Value m:type="Edm.String">190</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinItemLength</d:Key>
                <d:Value m:type="Edm.String">8</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">MinUserLength</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">RawNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfItems</d:Key>
                <d:Value m:type="Edm.String">2,000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=13&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfRecords</d:Key>
                <d:Value m:type="Edm.String">72,022</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1</id>
        <title type="text">GetDataInsightStatisticsEntity</title>
        <updated>2014-10-27T14:21:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetDataInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=14&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">SampelingNumberOfUsers</d:Key>
                <d:Value m:type="Edm.String">9,044</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="62----model-insight"></a><span data-ttu-id="c1e6d-362">6.2.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-362">6.2.</span></span>    <span data-ttu-id="c1e6d-363">Percepção de modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-363">Model Insight</span></span>
<span data-ttu-id="c1e6d-364">Retorna informações de modelo na compilação ativa ou (se fornecido) em uma compilação específica.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-364">Returns model insight on the active build or (if given) on a specific build.</span></span>

<span data-ttu-id="c1e6d-365">Disponível somente para compilação de Recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-365">Available only for Recommendation build.</span></span>

| <span data-ttu-id="c1e6d-366">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-366">HTTP Method</span></span> | <span data-ttu-id="c1e6d-367">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-367">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-368">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-368">GET</span></span> |<span data-ttu-id="c1e6d-369">Com a ID de compilação ativa:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-369">With active build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-370">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-370">Example:</span></span><br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-371">Com a ID de compilação específica:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-371">With specific build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-372">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-372">Parameter Name</span></span> | <span data-ttu-id="c1e6d-373">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-373">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-374">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-374">modelId</span></span> |<span data-ttu-id="c1e6d-375">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-375">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-376">buildId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-376">buildId</span></span> |<span data-ttu-id="c1e6d-377">Opcional - número que identifica uma compilação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-377">Optional - number that identifies a successful build.</span></span> |
| <span data-ttu-id="c1e6d-378">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-378">apiVersion</span></span> |<span data-ttu-id="c1e6d-379">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-379">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-380">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-380">Request Body</span></span> |<span data-ttu-id="c1e6d-381">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-381">NONE</span></span> |

<span data-ttu-id="c1e6d-382">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-382">**Response**:</span></span>

<span data-ttu-id="c1e6d-383">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-383">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-384">Os dados são retornados como uma coleção de propriedades.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-384">The data is returned as a collection of properties.</span></span>

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

<span data-ttu-id="c1e6d-385">A tabela a seguir descreve o valor que cada chave representa.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-385">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="c1e6d-386">Chave</span><span class="sxs-lookup"><span data-stu-id="c1e6d-386">Key</span></span> | <span data-ttu-id="c1e6d-387">Descrição</span><span class="sxs-lookup"><span data-stu-id="c1e6d-387">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-388">CatalogCoverage</span><span class="sxs-lookup"><span data-stu-id="c1e6d-388">CatalogCoverage</span></span> |<span data-ttu-id="c1e6d-389">Qual parte do catálogo pode ser modelado com padrões de uso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-389">What part of the catalog can be modelled with usage patterns.</span></span> <span data-ttu-id="c1e6d-390">O restante dos itens precisará de recursos com base no conteúdo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-390">The rest of the items will need content-based features.</span></span> |
| <span data-ttu-id="c1e6d-391">Mpr</span><span class="sxs-lookup"><span data-stu-id="c1e6d-391">Mpr</span></span> |<span data-ttu-id="c1e6d-392">Classificação percentual média do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-392">Mean percentile ranking of the model.</span></span> <span data-ttu-id="c1e6d-393">Menor é melhor.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-393">Lower is better.</span></span> |
| <span data-ttu-id="c1e6d-394">NumberOfDimensions</span><span class="sxs-lookup"><span data-stu-id="c1e6d-394">NumberOfDimensions</span></span> |<span data-ttu-id="c1e6d-395">Número de dimensões usado pelo algoritmo de fatoração de matriz.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-395">Number of dimensions used by the matrix factorization algorithm.</span></span> |

<span data-ttu-id="c1e6d-396">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-396">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get model insight statistics</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">CatalogCoverage</d:Key>
                <d:Value m:type="Edm.String">1.000</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">Mpr</d:Key>
                <d:Value m:type="Edm.String">0.367</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetModelInsightStatisticsEntity</title>
        <updated>2014-10-27T14:27:11Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelInsight?modelId='6254b40d-0514-49cb-a298-b81256d2b3ca'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Key m:type="Edm.String">NumberOfDimensions</d:Key>
                <d:Value m:type="Edm.String">20</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="63----get-model-sample"></a><span data-ttu-id="c1e6d-397">6.3.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-397">6.3.</span></span>    <span data-ttu-id="c1e6d-398">Obter um exemplo de modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-398">Get Model Sample</span></span>
<span data-ttu-id="c1e6d-399">Obter um exemplo de modelo de recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-399">Gets a sample of the recommendation model.</span></span>

| <span data-ttu-id="c1e6d-400">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-400">HTTP Method</span></span> | <span data-ttu-id="c1e6d-401">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-401">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-402">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-402">GET</span></span> |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="c1e6d-403">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-403">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-404">Com a ID de compilação específica:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-404">With specific build ID:</span></span><br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="c1e6d-405">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-405">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-406">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-406">Parameter Name</span></span> | <span data-ttu-id="c1e6d-407">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-407">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-408">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-408">modelId</span></span> |<span data-ttu-id="c1e6d-409">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-409">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-410">apiVersion</span></span> |<span data-ttu-id="c1e6d-411">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-411">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-412">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-412">Request Body</span></span> |<span data-ttu-id="c1e6d-413">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-413">NONE</span></span> |

<span data-ttu-id="c1e6d-414">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-414">**Response**:</span></span>

<span data-ttu-id="c1e6d-415">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-415">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-416">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-416">OData XML</span></span>

<span data-ttu-id="c1e6d-417">A resposta é retornada no formato de texto sem formatação:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-417">Response is returned in raw text format:</span></span>

<pre>
Level 1
---------------
655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel
    655fc955-a5a3-4a26-9723-3090859cb27b, Prey: A Novel Rating: 0.5215
    3f471802-f84f-44a0-99c8-6d2e7418eec1, Black Hawk Down: A Story of Modern War Rating: 0.5151
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5148
    6afc18e4-8c2a-43d1-9021-57543d6b11d8, Imajica Rating: 0.5146
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.514
56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai
    56b61441-0eed-46cc-a8f6-112775b81892, Life and Death in Shanghai Rating: 0.5218
    53156702-cc0c-443d-b718-6fb74b2491d3, Son of \ Rating: 0.5212
    fb8cf7a6-8719-46ee-97d4-92f931d77a3a, Smoke and Mirrors: Short Fictions and Illusions Rating: 0.5188
    8f5fe006-79e4-4679-816b-950989d1db4b, A Place I've Never Been (Contemporary American Fiction) Rating: 0.5156
    d8db4583-cc0f-49ce-bc95-b7fa3491623f, Happiness: A Novel Rating: 0.5156
50471eec-9aeb-4900-84d7-21567ab18546, If the Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of the Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, The Deep End of the Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, The Deep End of the Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, The Perfect Storm: A True Story of Men Against the Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: The True Story of the Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: The True Story of the Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on the Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in the Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, The Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On the Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, The Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories to Tell in the Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: The Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, The Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: The Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic the Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in the Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, The Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, The X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell the President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, The Map That Changed the World: William Smith and the Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, The Map That Changed the World: William Smith and the Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In the Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, The Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, The Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, The Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of the Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, The Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, The Perfect Storm: A True Story of Men Against the Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in the Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (The Official Guide to the X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, The Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, The Truth Is Out There (The Official Guide to the X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why the Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why the Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, The Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of the Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where the Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, The Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, The God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, The Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for the Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for the Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (The Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: The Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: The Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in the Time of Cholera (Penguin Great Books of the 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, The Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories To Tell In The Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from the Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, The Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, The Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, The Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a><span data-ttu-id="c1e6d-418">7. Regras de negócio do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-418">7. Model Business Rules</span></span>
<span data-ttu-id="c1e6d-419">Estes são os tipos de regras com suporte:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-419">These are the types of rules supported:</span></span>

* <span data-ttu-id="c1e6d-420"><strong>BlockList</strong> – a BlockList permite que você forneça uma lista de itens que não deseja que sejam retornados nos resultados de recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-420"><strong>BlockList</strong> - BlockList enables you to provide a list of items that you do not want to return in the recommendation results.</span></span> 
* <span data-ttu-id="c1e6d-421"><strong>FeatureBlockList</strong> – a Feature BlockList permite que você bloqueie itens com base nos valores de seus recursos.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you to block items based on the values of its features.</span></span>

<span data-ttu-id="c1e6d-422">*Não envie mais de 1.000 itens em uma única regra de lista de bloqueios ou sua chamada poderá expirar. Se você precisa bloquear mais de 1.000 itens, você pode fazer várias chamadas de lista de bloqueios.*</span><span class="sxs-lookup"><span data-stu-id="c1e6d-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need to block more than 1000 items, you can make several blocklist calls.*</span></span>

* <span data-ttu-id="c1e6d-423"><strong>Upsale</strong> - Upsale permite reforçar os itens a serem retornados nos resultados de recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-423"><strong>Upsale</strong> - Upsale enables you to enforce items to return in the recommendation results.</span></span>
* <span data-ttu-id="c1e6d-424"><strong>WhiteList</strong> – WhiteList permite a você sugerir recomendações apenas de uma lista de itens.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-424"><strong>WhiteList</strong> - White List enables you to only suggest recommendations from a list of items.</span></span>
* <span data-ttu-id="c1e6d-425"><strong>FeatureWhiteList</strong> – Feature White List permite que você recomende somente os itens com valores de recurso específicos.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-425"><strong>FeatureWhiteList</strong> - Feature White List enables you to only recommend items that have specific feature values.</span></span>
* <span data-ttu-id="c1e6d-426"><strong>PerSeedBlockList</strong> - Per Seed Block List permite fornecer por itens uma lista dos itens que não podem ser retornados como resultados de recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you to provide per item a list of items that cannot be returned as recommendation results.</span></span>

### <a name="71----get-model-rules"></a><span data-ttu-id="c1e6d-427">7.1.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-427">7.1.</span></span>    <span data-ttu-id="c1e6d-428">Obter regras de modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-428">Get Model Rules</span></span>
| <span data-ttu-id="c1e6d-429">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-429">HTTP Method</span></span> | <span data-ttu-id="c1e6d-430">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-430">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-431">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-431">GET</span></span> |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="c1e6d-432">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-432">Example:</span></span><br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-433">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-433">Parameter Name</span></span> | <span data-ttu-id="c1e6d-434">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-434">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-435">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-435">modelId</span></span> |<span data-ttu-id="c1e6d-436">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-436">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-437">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-437">apiVersion</span></span> |<span data-ttu-id="c1e6d-438">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-438">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-439">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-439">Request Body</span></span> |<span data-ttu-id="c1e6d-440">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-440">NONE</span></span> |

<span data-ttu-id="c1e6d-441">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-441">**Response**:</span></span>

<span data-ttu-id="c1e6d-442">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-442">HTTP Status code: 200</span></span>

* <span data-ttu-id="c1e6d-443">`feed/entry/content/properties/Id` - Identificador exclusivo desta regra.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="c1e6d-444">`feed/entry/content/properties/Type` - O tipo da regra.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-444">`feed/entry/content/properties/Type` - Type of the rule.</span></span>
* <span data-ttu-id="c1e6d-445">`feed/entry/content/properties/Parameter` - O parâmetro da regra.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="c1e6d-446">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-446">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get a list of rules for a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T12:58:57Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000043</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1000"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfRulesForAModelEntity</title>
        <updated>2014-11-05T12:58:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelRules?modelId='5e824626-50d3-469d-a824-564d38453103'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000044</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1001"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="72----add-rule"></a><span data-ttu-id="c1e6d-447">7.2.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-447">7.2.</span></span>    <span data-ttu-id="c1e6d-448">Adicionar regra</span><span class="sxs-lookup"><span data-stu-id="c1e6d-448">Add Rule</span></span>
| <span data-ttu-id="c1e6d-449">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-449">HTTP Method</span></span> | <span data-ttu-id="c1e6d-450">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-450">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-451">POST</span><span class="sxs-lookup"><span data-stu-id="c1e6d-451">POST</span></span> |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| <span data-ttu-id="c1e6d-452">HEADER</span><span class="sxs-lookup"><span data-stu-id="c1e6d-452">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="c1e6d-453">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-453">Parameter Name</span></span> | <span data-ttu-id="c1e6d-454">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-454">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-455">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-455">apiVersion</span></span> |<span data-ttu-id="c1e6d-456">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-456">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-457">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-457">Request Body</span></span> | |

<span data-ttu-id="c1e6d-458"><ins>Sempre ao fornecer Ids de Item para regras de negócio, use a Id Externa do item (a mesma Id que você usou no arquivo de catálogo)</ins></span><span class="sxs-lookup"><span data-stu-id="c1e6d-458"><ins>Whenever providing Item Ids for business rules, make sure to use the External Id of the item (the same Id that you used in the catalog file)</ins></span></span><br><span data-ttu-id="c1e6d-459">
<ins>Para adicionar uma regra BlockList:</ins></span><span class="sxs-lookup"><span data-stu-id="c1e6d-459">
<ins>To add a BlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="c1e6d-460"><ins>
<ins>Para adicionar uma regra FeatureBlockList:</ins></span><span class="sxs-lookup"><span data-stu-id="c1e6d-460"><ins>
<ins>To add a FeatureBlockList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><span data-ttu-id="c1e6d-461"><ins> Para adicionar uma regra Upsale:</ins></span><span class="sxs-lookup"><span data-stu-id="c1e6d-461"><ins> To add an Upsale rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br><span data-ttu-id="c1e6d-462">
<ins>Para adicionar uma regra WhiteList:</ins></span><span class="sxs-lookup"><span data-stu-id="c1e6d-462">
<ins>To add a WhiteList rule:</ins></span></span><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="c1e6d-463"><ins>
<ins>Para adicionar uma regra FeatureWhiteList:</ins></span><span class="sxs-lookup"><span data-stu-id="c1e6d-463"><ins>
<ins>To add a FeatureWhiteList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><span data-ttu-id="c1e6d-464"><ins> Para adicionar uma regra PerSeedBlockList:</ins></span><span class="sxs-lookup"><span data-stu-id="c1e6d-464"><ins> To add a PerSeedBlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

<span data-ttu-id="c1e6d-465">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-465">**Response**:</span></span>

<span data-ttu-id="c1e6d-466">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-466">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-467">A API retorna a regra recém-criada com seus detalhes.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-467">The API returns the newly created rule with its details.</span></span> <span data-ttu-id="c1e6d-468">A propriedade de regras pode ser recuperada dos caminhos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-468">The rules property can be retrieved from the following paths:</span></span>

* <span data-ttu-id="c1e6d-469">`feed/entry/content/properties/Id` - Identificador exclusivo desta regra.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="c1e6d-470">`feed/entry/content/properties/Type` - O tipo de regra: BlockList ou Upsale.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-470">`feed/entry/content/properties/Type` - Type of the rule: BlockList or Upsale.</span></span>
* <span data-ttu-id="c1e6d-471">`feed/entry/content/properties/Parameter` - O parâmetro da regra.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="c1e6d-472">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-472">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Add A Rule</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-05T11:13:28Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AddARuleEntity</title>
        <updated>2014-11-05T11:13:28Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/AddRule?apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">1000041</d:Id>
                <d:Type m:type="Edm.String">BlockList</d:Type>
                <d:Parameters m:type="Edm.String">{"ItemsToExclude":["1002"]}</d:Parameters>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="73----delete-rule"></a><span data-ttu-id="c1e6d-473">7.3.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-473">7.3.</span></span>    <span data-ttu-id="c1e6d-474">Excluir regra</span><span class="sxs-lookup"><span data-stu-id="c1e6d-474">Delete Rule</span></span>
| <span data-ttu-id="c1e6d-475">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-475">HTTP Method</span></span> | <span data-ttu-id="c1e6d-476">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-476">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-477">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="c1e6d-477">DELETE</span></span> |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-478">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-478">Example:</span></span><br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-479">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-479">Parameter Name</span></span> | <span data-ttu-id="c1e6d-480">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-480">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-481">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-481">modelId</span></span> |<span data-ttu-id="c1e6d-482">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-482">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-483">filterId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-483">filterId</span></span> |<span data-ttu-id="c1e6d-484">Identificador exclusivo do filtro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-484">Unique identifier of the filter</span></span> |
| <span data-ttu-id="c1e6d-485">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-485">apiVersion</span></span> |<span data-ttu-id="c1e6d-486">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-486">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-487">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-487">Request Body</span></span> |<span data-ttu-id="c1e6d-488">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-488">NONE</span></span> |

<span data-ttu-id="c1e6d-489">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-489">**Response**:</span></span>

<span data-ttu-id="c1e6d-490">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-490">HTTP Status code: 200</span></span>

### <a name="74----delete-all-rules"></a><span data-ttu-id="c1e6d-491">7.4.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-491">7.4.</span></span>    <span data-ttu-id="c1e6d-492">Excluir todas as regras</span><span class="sxs-lookup"><span data-stu-id="c1e6d-492">Delete All Rules</span></span>
| <span data-ttu-id="c1e6d-493">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-493">HTTP Method</span></span> | <span data-ttu-id="c1e6d-494">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-495">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="c1e6d-495">DELETE</span></span> |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-496">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-496">Example:</span></span><br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-497">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-497">Parameter Name</span></span> | <span data-ttu-id="c1e6d-498">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-499">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-499">modelId</span></span> |<span data-ttu-id="c1e6d-500">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-500">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-501">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-501">apiVersion</span></span> |<span data-ttu-id="c1e6d-502">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-502">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-503">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-503">Request Body</span></span> |<span data-ttu-id="c1e6d-504">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-504">NONE</span></span> |

<span data-ttu-id="c1e6d-505">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-505">**Response**:</span></span>

<span data-ttu-id="c1e6d-506">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-506">HTTP Status code: 200</span></span>

## <a name="8-catalog"></a><span data-ttu-id="c1e6d-507">8. Catálogo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-507">8. Catalog</span></span>
### <a name="81----import-catalog-data"></a><span data-ttu-id="c1e6d-508">8.1.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-508">8.1.</span></span>    <span data-ttu-id="c1e6d-509">Importar Dados de Catálogo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-509">Import Catalog Data</span></span>
<span data-ttu-id="c1e6d-510">Se você carregar vários arquivos de catálogo para o mesmo modelo com várias chamadas, inseriremos apenas os novos itens de catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-510">If you upload several catalog files to the same model with several calls, we will insert only the new catalog items.</span></span> <span data-ttu-id="c1e6d-511">Os itens existentes permanecerão com os valores originais.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-511">Existing items will remain with the original values.</span></span> <span data-ttu-id="c1e6d-512">Você não pode atualizar os dados do catálogo usando este método.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-512">You cannot update catalog data by using this method.</span></span>

<span data-ttu-id="c1e6d-513">Os dados do catálogo devem seguir o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-513">The catalog data should follow the following format:</span></span>

* <span data-ttu-id="c1e6d-514">Sem recursos – `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span><span class="sxs-lookup"><span data-stu-id="c1e6d-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span></span>
* <span data-ttu-id="c1e6d-515">Com recursos – `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span><span class="sxs-lookup"><span data-stu-id="c1e6d-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span></span>

<span data-ttu-id="c1e6d-516">Observação: o tamanho máximo do arquivo é de 200 MB.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-516">Note: The maximum file size is 200MB.</span></span>

<span data-ttu-id="c1e6d-517">** Detalhes do formato **</span><span class="sxs-lookup"><span data-stu-id="c1e6d-517">** Format details **</span></span>

| <span data-ttu-id="c1e6d-518">Nome</span><span class="sxs-lookup"><span data-stu-id="c1e6d-518">Name</span></span> | <span data-ttu-id="c1e6d-519">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="c1e6d-519">Mandatory</span></span> | <span data-ttu-id="c1e6d-520">Tipo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-520">Type</span></span> | <span data-ttu-id="c1e6d-521">Descrição</span><span class="sxs-lookup"><span data-stu-id="c1e6d-521">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c1e6d-522">Id do item</span><span class="sxs-lookup"><span data-stu-id="c1e6d-522">Item Id</span></span> |<span data-ttu-id="c1e6d-523">Sim</span><span class="sxs-lookup"><span data-stu-id="c1e6d-523">Yes</span></span> |<span data-ttu-id="c1e6d-524">[A-z], [a-z], [0-9], [_] &#40;Sublinhado&#41;, [-] &#40;Traço&#41;</span><span class="sxs-lookup"><span data-stu-id="c1e6d-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="c1e6d-525">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="c1e6d-525">Max length: 50</span></span> |<span data-ttu-id="c1e6d-526">Identificador exclusivo de um item</span><span class="sxs-lookup"><span data-stu-id="c1e6d-526">Unique identifier of an item.</span></span> |
| <span data-ttu-id="c1e6d-527">Nome do Item</span><span class="sxs-lookup"><span data-stu-id="c1e6d-527">Item Name</span></span> |<span data-ttu-id="c1e6d-528">Sim</span><span class="sxs-lookup"><span data-stu-id="c1e6d-528">Yes</span></span> |<span data-ttu-id="c1e6d-529">Qualquer caractere alfanumérico</span><span class="sxs-lookup"><span data-stu-id="c1e6d-529">Any alphanumeric characters</span></span><br> <span data-ttu-id="c1e6d-530">Comprimento máximo: 255</span><span class="sxs-lookup"><span data-stu-id="c1e6d-530">Max length: 255</span></span> |<span data-ttu-id="c1e6d-531">Nome do item.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-531">Item name.</span></span> |
| <span data-ttu-id="c1e6d-532">Categoria do Item</span><span class="sxs-lookup"><span data-stu-id="c1e6d-532">Item Category</span></span> |<span data-ttu-id="c1e6d-533">Sim</span><span class="sxs-lookup"><span data-stu-id="c1e6d-533">Yes</span></span> |<span data-ttu-id="c1e6d-534">Qualquer caractere alfanumérico</span><span class="sxs-lookup"><span data-stu-id="c1e6d-534">Any alphanumeric characters</span></span> <br> <span data-ttu-id="c1e6d-535">Comprimento máximo: 255</span><span class="sxs-lookup"><span data-stu-id="c1e6d-535">Max length: 255</span></span> |<span data-ttu-id="c1e6d-536">Categoria à qual este item pertence (por exemplo, Livros de Culinária, Drama...); pode estar vazia.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-536">Category to which this item belongs (e.g. Cooking Books, Drama…); can be empty.</span></span> |
| <span data-ttu-id="c1e6d-537">Descrição</span><span class="sxs-lookup"><span data-stu-id="c1e6d-537">Description</span></span> |<span data-ttu-id="c1e6d-538">Não, a menos que os recursos estejam presentes (mas pode estar vazia)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-538">No, unless features are present (but can be empty)</span></span> |<span data-ttu-id="c1e6d-539">Qualquer caractere alfanumérico</span><span class="sxs-lookup"><span data-stu-id="c1e6d-539">Any alphanumeric characters</span></span> <br> <span data-ttu-id="c1e6d-540">Comprimento máximo: 4000</span><span class="sxs-lookup"><span data-stu-id="c1e6d-540">Max length: 4000</span></span> |<span data-ttu-id="c1e6d-541">Descrição deste item.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-541">Description of this item.</span></span> |
| <span data-ttu-id="c1e6d-542">Lista de recursos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-542">Features list</span></span> |<span data-ttu-id="c1e6d-543">Não</span><span class="sxs-lookup"><span data-stu-id="c1e6d-543">No</span></span> |<span data-ttu-id="c1e6d-544">Qualquer caractere alfanumérico</span><span class="sxs-lookup"><span data-stu-id="c1e6d-544">Any alphanumeric characters</span></span> <br> <span data-ttu-id="c1e6d-545">Comprimento máximo: 4.000; Número máximo de recursos: 20</span><span class="sxs-lookup"><span data-stu-id="c1e6d-545">Max length: 4000; Max number of features:20</span></span> |<span data-ttu-id="c1e6d-546">Lista separada por vírgulas de nome do recurso = valor do recurso que pode ser usada para aperfeiçoar a recomendação do modelo; consulte a seção [Tópicos avançados](#2-advanced-topics) .</span><span class="sxs-lookup"><span data-stu-id="c1e6d-546">Comma-separated list of feature name=feature value that can be used to enhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span></span> |

| <span data-ttu-id="c1e6d-547">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-547">HTTP Method</span></span> | <span data-ttu-id="c1e6d-548">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-548">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-549">POST</span><span class="sxs-lookup"><span data-stu-id="c1e6d-549">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-550">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-550">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| <span data-ttu-id="c1e6d-551">HEADER</span><span class="sxs-lookup"><span data-stu-id="c1e6d-551">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="c1e6d-552">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-552">Parameter Name</span></span> | <span data-ttu-id="c1e6d-553">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-553">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-554">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-554">modelId</span></span> |<span data-ttu-id="c1e6d-555">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-555">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-556">nome do arquivo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-556">filename</span></span> |<span data-ttu-id="c1e6d-557">Identificador textual do catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-557">Textual identifier of the catalog.</span></span><br><span data-ttu-id="c1e6d-558">São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="c1e6d-559">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="c1e6d-559">Max length: 50</span></span> |
| <span data-ttu-id="c1e6d-560">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-560">apiVersion</span></span> |<span data-ttu-id="c1e6d-561">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-561">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-562">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-562">Request Body</span></span> |<span data-ttu-id="c1e6d-563">Exemplo (com recursos):</span><span class="sxs-lookup"><span data-stu-id="c1e6d-563">Example (with features):</span></span><br/><span data-ttu-id="c1e6d-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,the book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span><span class="sxs-lookup"><span data-stu-id="c1e6d-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,the book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span></span><br><span data-ttu-id="c1e6d-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span><span class="sxs-lookup"><span data-stu-id="c1e6d-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,The Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span></span><br><span data-ttu-id="c1e6d-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span><span class="sxs-lookup"><span data-stu-id="c1e6d-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span></span><br><span data-ttu-id="c1e6d-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,the book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span><span class="sxs-lookup"><span data-stu-id="c1e6d-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,the book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span></span></pre> |

<span data-ttu-id="c1e6d-568">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-568">**Response**:</span></span>

<span data-ttu-id="c1e6d-569">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-569">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-570">A API retorna um relatório da importação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-570">The API returns a report of the import.</span></span>

* <span data-ttu-id="c1e6d-571">`feed\entry\content\properties\LineCount` – O número de linhas aceitas.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="c1e6d-572">`feed\entry\content\properties\ErrorCount` – O número de linhas que não foram inseridas devido a um erro.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>

<span data-ttu-id="c1e6d-573">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-573">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Import catalog file</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-10-05T06:58:04Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'" />
    <entry>
       <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ImportCatalogFileEntity2</title>
        <updated>2014-10-05T06:58:04Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportCatalogFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='catalog10_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:LineCount m:type="Edm.String">4</d:LineCount>
                <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="82----get-catalog"></a><span data-ttu-id="c1e6d-574">8.2.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-574">8.2.</span></span>    <span data-ttu-id="c1e6d-575">Obter catálogo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-575">Get Catalog</span></span>
<span data-ttu-id="c1e6d-576">Recupera todos os itens de catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-576">Retrieves all catalog items.</span></span>
<span data-ttu-id="c1e6d-577">O catálogo será recuperado uma página por vez.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-577">The catalog will be retrieved one page at a time.</span></span> <span data-ttu-id="c1e6d-578">Se você quiser obter itens em um índice específico, use o parâmetro odata $skip.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-578">If you want to get items at a particular index, you can use the $skip odata parameter.</span></span> <span data-ttu-id="c1e6d-579">Por exemplo, se você quiser obter itens a partir da posição 100, adicione o parâmetro $skip=100 à solicitação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-579">For instance if you want to get items starting at position 100, add the parameter $skip=100 to the request.</span></span>

| <span data-ttu-id="c1e6d-580">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-580">HTTP Method</span></span> | <span data-ttu-id="c1e6d-581">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-581">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-582">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-582">GET</span></span> |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-583">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-583">Example:</span></span><br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-584">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-584">Parameter Name</span></span> | <span data-ttu-id="c1e6d-585">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-585">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-586">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-586">modelId</span></span> |<span data-ttu-id="c1e6d-587">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-587">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-588">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-588">apiVersion</span></span> |<span data-ttu-id="c1e6d-589">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-589">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-590">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-590">Request Body</span></span> |<span data-ttu-id="c1e6d-591">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-591">NONE</span></span> |

<span data-ttu-id="c1e6d-592">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-592">**Response**:</span></span>

<span data-ttu-id="c1e6d-593">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-593">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-594">A resposta inclui uma entrada por item de catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-594">The response includes one entry per catalog item.</span></span> <span data-ttu-id="c1e6d-595">Cada entrada tem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-595">Each entry has the following data:</span></span>

* <span data-ttu-id="c1e6d-596">`feed/entry/content/properties/ExternalId` - ID externa do item do catálogo, fornecida pelo cliente.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, the one provided by the customer.</span></span>
* <span data-ttu-id="c1e6d-597">`feed/entry/content/properties/InternalId` - ID interna do item do catálogo, gerada pelas Recomendações do Machine Learning do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, the one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="c1e6d-598">`feed/entry/content/properties/Name` - Nome do item do catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-598">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="c1e6d-599">`feed/entry/content/properties/Category` - Categoria do item do catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-599">`feed/entry/content/properties/Category` - Catalog item category.</span></span>
* <span data-ttu-id="c1e6d-600">`feed/entry/content/properties/Description` - Descrição do item do catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-600">`feed/entry/content/properties/Description` - Catalog item description.</span></span>
* <span data-ttu-id="c1e6d-601">`feed/entry/content/properties/Metadata` - Metadados do item do catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span></span>

<span data-ttu-id="c1e6d-602">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-602">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get All Catalog Items</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">552A1940-21E4-4399-82BB-594B46D7ED54</d:ExternalId>
                <d:InternalId m:type="Edm.String">060db26a-e6a6-464e-bb52-436d2da82a50</d:InternalId>
                <d:Name m:type="Edm.String">Restraint of Beasts</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:ExternalId>
                <d:InternalId m:type="Edm.String">209d7bfe-2eb9-4455-92a3-7c867a41a74a</d:InternalId>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">3BB5CB44-D143-4BDD-A55C-443964BF4B23</d:ExternalId>
                <d:InternalId m:type="Edm.String">913ff79b-059b-4d4d-8042-6fa4cc1391dd</d:InternalId>
                <d:Name m:type="Edm.String">Spadework</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">AllCatalogItemsEntity</title>
        <updated>2014-10-29T11:13:26Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalog?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:ExternalId m:type="Edm.String">21BF8088-B6C0-4509-870C-E1C7AC78304A</d:ExternalId>
                <d:InternalId m:type="Edm.String">ea65e4fa-768c-40b4-92c3-69d3e8178691</d:InternalId>
                <d:Name m:type="Edm.String">The Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a><span data-ttu-id="c1e6d-603">8.3.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-603">8.3.</span></span>    <span data-ttu-id="c1e6d-604">Obter itens de catálogo por Token</span><span class="sxs-lookup"><span data-stu-id="c1e6d-604">Get Catalog Items by Token</span></span>
| <span data-ttu-id="c1e6d-605">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-605">HTTP Method</span></span> | <span data-ttu-id="c1e6d-606">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-606">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-607">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-607">GET</span></span> |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-608">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-608">Example:</span></span><br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-609">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-609">Parameter Name</span></span> | <span data-ttu-id="c1e6d-610">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-610">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-611">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-611">modelId</span></span> |<span data-ttu-id="c1e6d-612">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-612">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-613">token</span><span class="sxs-lookup"><span data-stu-id="c1e6d-613">token</span></span> |<span data-ttu-id="c1e6d-614">Token do nome do item do catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-614">Token of the catalog item’s name.</span></span> <span data-ttu-id="c1e6d-615">Deve conter pelo menos três caracteres.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-615">Should contain at least 3 characters.</span></span> |
| <span data-ttu-id="c1e6d-616">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-616">apiVersion</span></span> |<span data-ttu-id="c1e6d-617">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-617">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-618">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-618">Request Body</span></span> |<span data-ttu-id="c1e6d-619">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-619">NONE</span></span> |

<span data-ttu-id="c1e6d-620">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-620">**Response**:</span></span>

<span data-ttu-id="c1e6d-621">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-621">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-622">A resposta inclui uma entrada por item de catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-622">The response includes one entry per catalog item.</span></span> <span data-ttu-id="c1e6d-623">Cada entrada tem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-623">Each entry has the following data:</span></span>

* <span data-ttu-id="c1e6d-624">`feed/entry/content/properties/InternalId` - ID interna do item do catálogo, gerada pelas Recomendações do Machine Learning do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, the one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="c1e6d-625">`feed/entry/content/properties/Name` - Nome do item do catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-625">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="c1e6d-626">`feed/entry/content/properties/Rating` - (para uso futuro)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-626">`feed/entry/content/properties/Rating` -  (for future use)</span></span>
* <span data-ttu-id="c1e6d-627">`feed/entry/content/properties/Reasoning` - (para uso futuro)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span></span>
* <span data-ttu-id="c1e6d-628">`feed/entry/content/properties/Metadata` - (para uso futuro)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-628">`feed/entry/content/properties/Metadata` -  (for future use)</span></span>
* <span data-ttu-id="c1e6d-629">`feed/entry/content/properties/FormattedRating` - (para uso futuro)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span></span>

<span data-ttu-id="c1e6d-630">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-630">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get Catalog items that contain a token</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-29T11:48:19Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">CatalogItemsThatContainATokenEntity</title>
            <updated>2014-10-29T11:48:19Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetCatalogItemsByToken?modelId='0dbb55fa-7f11-418d-8537-8ff2d9d1d9c6'&amp;token='Cla'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                  <m:properties>
                    <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                    <d:Name m:type="Edm.String">Clara Callan</d:Name>
                    <d:Rating m:type="Edm.Double">0</d:Rating>
                    <d:Reasoning m:type="Edm.String"></d:Reasoning>
                    <d:Metadata m:type="Edm.String"></d:Metadata>
                    <d:FormattedRating m:type="Edm.Double" m:null="true"></d:FormattedRating>
                  </m:properties>
            </content>
        </entry>
    </feed>

## <a name="9-usage-data"></a><span data-ttu-id="c1e6d-631">9. Dados de uso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-631">9. Usage data</span></span>
### <a name="91----import-usage-data"></a><span data-ttu-id="c1e6d-632">9.1.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-632">9.1.</span></span>    <span data-ttu-id="c1e6d-633">Importar Dados de Uso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-633">Import Usage Data</span></span>
#### <a name="911-uploading-file"></a><span data-ttu-id="c1e6d-634">9.1.1.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-634">9.1.1.</span></span> <span data-ttu-id="c1e6d-635">Carregamento de Arquivo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-635">Uploading File</span></span>
<span data-ttu-id="c1e6d-636">Esta seção mostra como carregar dados de uso usando um arquivo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-636">This section shows how to upload usage data by using a file.</span></span> <span data-ttu-id="c1e6d-637">Você pode chamar essa API várias vezes com dados de uso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-637">You can call this API several times with usage data.</span></span> <span data-ttu-id="c1e6d-638">Todos os dados de uso serão salvos para todas as chamadas.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-638">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="c1e6d-639">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-639">HTTP Method</span></span> | <span data-ttu-id="c1e6d-640">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-640">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-641">POST</span><span class="sxs-lookup"><span data-stu-id="c1e6d-641">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-642">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-642">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-643">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-643">Parameter Name</span></span> | <span data-ttu-id="c1e6d-644">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-644">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-645">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-645">modelId</span></span> |<span data-ttu-id="c1e6d-646">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-646">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-647">nome do arquivo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-647">filename</span></span> |<span data-ttu-id="c1e6d-648">Identificador textual do catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-648">Textual identifier of the catalog.</span></span><br><span data-ttu-id="c1e6d-649">São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="c1e6d-650">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="c1e6d-650">Max length: 50</span></span> |
| <span data-ttu-id="c1e6d-651">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-651">apiVersion</span></span> |<span data-ttu-id="c1e6d-652">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-652">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-653">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-653">Request Body</span></span> |<span data-ttu-id="c1e6d-654">Dados de uso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-654">Usage data.</span></span> <span data-ttu-id="c1e6d-655">Formato:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-655">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="c1e6d-656">Nome</span><span class="sxs-lookup"><span data-stu-id="c1e6d-656">Name</span></span></th><th><span data-ttu-id="c1e6d-657">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="c1e6d-657">Mandatory</span></span></th><th><span data-ttu-id="c1e6d-658">Tipo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-658">Type</span></span></th><th><span data-ttu-id="c1e6d-659">Descrição</span><span class="sxs-lookup"><span data-stu-id="c1e6d-659">Description</span></span></th></tr><tr><td><span data-ttu-id="c1e6d-660">Id de usuário</span><span class="sxs-lookup"><span data-stu-id="c1e6d-660">User Id</span></span></td><td><span data-ttu-id="c1e6d-661">Sim</span><span class="sxs-lookup"><span data-stu-id="c1e6d-661">Yes</span></span></td><td><span data-ttu-id="c1e6d-662">[A-z], [a-z], [0-9], [_] &#40;Sublinhado&#41;, [-] &#40;Traço&#41;</span><span class="sxs-lookup"><span data-stu-id="c1e6d-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="c1e6d-663">Comprimento máximo: 255</span><span class="sxs-lookup"><span data-stu-id="c1e6d-663">Max length: 255</span></span> </td><td><span data-ttu-id="c1e6d-664">Identificador exclusivo de um usuário.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-664">Unique identifier of a user.</span></span></td></tr><tr><td><span data-ttu-id="c1e6d-665">Id do item</span><span class="sxs-lookup"><span data-stu-id="c1e6d-665">Item Id</span></span></td><td><span data-ttu-id="c1e6d-666">Sim</span><span class="sxs-lookup"><span data-stu-id="c1e6d-666">Yes</span></span></td><td><span data-ttu-id="c1e6d-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span><span class="sxs-lookup"><span data-stu-id="c1e6d-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="c1e6d-668">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="c1e6d-668">Max length: 50</span></span></td><td><span data-ttu-id="c1e6d-669">Identificador exclusivo de um item</span><span class="sxs-lookup"><span data-stu-id="c1e6d-669">Unique identifier of an item.</span></span></td></tr><tr><td><span data-ttu-id="c1e6d-670">Hora</span><span class="sxs-lookup"><span data-stu-id="c1e6d-670">Time</span></span></td><td><span data-ttu-id="c1e6d-671">Não</span><span class="sxs-lookup"><span data-stu-id="c1e6d-671">No</span></span></td><td><span data-ttu-id="c1e6d-672">Data no formato: AAAA/MM/DDTHH:MM:SS (por exemplo, 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="c1e6d-673">Hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-673">Time of data.</span></span></td></tr><tr><td><span data-ttu-id="c1e6d-674">Evento</span><span class="sxs-lookup"><span data-stu-id="c1e6d-674">Event</span></span></td><td><span data-ttu-id="c1e6d-675">Não; se fornecido, também deve colocar a data</span><span class="sxs-lookup"><span data-stu-id="c1e6d-675">No; if supplied then must also put date</span></span></td><td><span data-ttu-id="c1e6d-676">Um dos seguintes:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-676">One of the following:</span></span><br><span data-ttu-id="c1e6d-677">• Clique</span><span class="sxs-lookup"><span data-stu-id="c1e6d-677">• Click</span></span><br><span data-ttu-id="c1e6d-678">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="c1e6d-678">• RecommendationClick</span></span><br><span data-ttu-id="c1e6d-679">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="c1e6d-679">•    AddShopCart</span></span><br><span data-ttu-id="c1e6d-680">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="c1e6d-680">• RemoveShopCart</span></span><br><span data-ttu-id="c1e6d-681">• Compra</span><span class="sxs-lookup"><span data-stu-id="c1e6d-681">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="c1e6d-682">Tamanho máximo do arquivo: 200 MB</span><span class="sxs-lookup"><span data-stu-id="c1e6d-682">Maximum file size: 200MB</span></span><br><br><span data-ttu-id="c1e6d-683">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-683">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="c1e6d-684">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-684">**Response**:</span></span>

<span data-ttu-id="c1e6d-685">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-685">HTTP Status code: 200</span></span>

* <span data-ttu-id="c1e6d-686">`Feed\entry\content\properties\LineCount` – O número de linhas aceitas.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="c1e6d-687">`Feed\entry\content\properties\ErrorCount` – O número de linhas que não foram inseridas devido a um erro.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due to an error.</span></span>
* <span data-ttu-id="c1e6d-688">`Feed\entry\content\properties\FileId` – Identificador do arquivo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-688">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="c1e6d-689">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-689">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Add bulk usage data (usage file)</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T07:21:44Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">AddBulkUsageDataUsageFileEntity2</title>
    <updated>2014-10-05T07:21:44Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ImportUsageFile?modelId='a658c626-2baa-43a7-ac98-f6ee26120a12'&amp;filename='ImplicitMatrix10_Guid_small.txt'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:LineCount m:type="Edm.String">33</d:LineCount>
        <d:ErrorCount m:type="Edm.String">0</d:ErrorCount>
        <d:FileId m:type="Edm.String">fead7c1c-db01-46c0-872f-65bcda36025d</d:FileId>
      </m:properties>
    </content>
      </entry>
    </feed>


#### <a name="912-using-data-acquisition"></a><span data-ttu-id="c1e6d-690">9.1.2.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-690">9.1.2.</span></span> <span data-ttu-id="c1e6d-691">Usar a Aquisição de Dados</span><span class="sxs-lookup"><span data-stu-id="c1e6d-691">Using Data Acquisition</span></span>
<span data-ttu-id="c1e6d-692">Esta seção mostra como enviar eventos em tempo real para as Recomendações do Azure Machine Learning, geralmente do seu site.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-692">This section shows how to send events in real time to Azure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="c1e6d-693">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-693">HTTP Method</span></span> | <span data-ttu-id="c1e6d-694">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-694">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-695">POST</span><span class="sxs-lookup"><span data-stu-id="c1e6d-695">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| <span data-ttu-id="c1e6d-696">HEADER</span><span class="sxs-lookup"><span data-stu-id="c1e6d-696">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="c1e6d-697">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-697">Parameter Name</span></span> | <span data-ttu-id="c1e6d-698">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-698">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-699">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-699">apiVersion</span></span> |<span data-ttu-id="c1e6d-700">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-700">1.0</span></span> |
| <span data-ttu-id="c1e6d-701">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-701">Request body</span></span> |<span data-ttu-id="c1e6d-702">Entrada de dados de evento para cada evento que você deseja enviar.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-702">Event data entry for each event you want to send.</span></span> <span data-ttu-id="c1e6d-703">Você deve enviar a mesma ID no campo SessionId para a mesma sessão de usuário ou navegador.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-703">You should send for the same user or browser session the same ID in the SessionId field.</span></span> <span data-ttu-id="c1e6d-704">(Consulte o exemplo de corpo de evento abaixo.)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-704">(See sample of event body below.)</span></span> |

* <span data-ttu-id="c1e6d-705">Exemplo de evento “Click”:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-705">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="c1e6d-706">Exemplo de evento “RecommendationClick”:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-706">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="c1e6d-707">Exemplo de evento “AddShopCart”:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-707">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="c1e6d-708">Exemplo de evento “RemoveShopCart”:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-708">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="c1e6d-709">Exemplo de evento “Purchase”:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-709">Example for event 'Purchase':</span></span>
  
        <Event xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <ModelId>2779c063-48fb-46c1-bae3-74acddc8c1d1</ModelId>
        <SessionId>11112222</SessionId>
        <EventData>
            <EventData>
                <Name>Purchase</Name>
                <PurchaseItems>
                    <PurchaseItem>
                        <ItemId>ABBF8081-C5C0-4F09-9701-E1C7AC78304A</ItemId>
                        <Count>1</Count>
                    </PurchaseItem>
                    <PurchaseItem>
                        <ItemId>21BF8088-B6C0-4509-870C-11C0AC7F304B</ItemId>
                        <Count>3</Count>
                    </PurchaseItem>
                </PurchaseItems>
            </EventData>
        </EventData>
        </Event>
* <span data-ttu-id="c1e6d-710">Exemplo de envio de dois eventos “Click” e “AddShopCart”:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-710">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="c1e6d-711">**Response**: código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-711">**Response**: HTTP Status code: 200</span></span>

### <a name="92----list-model-usage-files"></a><span data-ttu-id="c1e6d-712">9.2.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-712">9.2.</span></span>    <span data-ttu-id="c1e6d-713">Lista dos arquivos de modelo de uso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-713">List Model Usage Files</span></span>
<span data-ttu-id="c1e6d-714">Recupera os metadados de todos os arquivos de uso do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-714">Retrieves metadata of all model usage files.</span></span>
<span data-ttu-id="c1e6d-715">Os arquivos de uso serão recuperados uma página por vez.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-715">The usage files will be retrieved one page at a time.</span></span> <span data-ttu-id="c1e6d-716">Cada página contém 100 itens.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-716">Each page containes 100 items.</span></span> <span data-ttu-id="c1e6d-717">Se você quiser obter itens em um índice específico, use o parâmetro odata $skip.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-717">If you want to get items at a particular index, you can use the $skip odata parameter.</span></span> <span data-ttu-id="c1e6d-718">Por exemplo, se você quiser obter itens a partir da posição 100, adicione o parâmetro $skip=100 à solicitação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-718">For instance if you want to get items starting at position 100, add the parameter $skip=100 to the request.</span></span>

| <span data-ttu-id="c1e6d-719">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-719">HTTP Method</span></span> | <span data-ttu-id="c1e6d-720">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-720">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-721">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-721">GET</span></span> |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-722">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-722">Example:</span></span><br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-723">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-723">Parameter Name</span></span> | <span data-ttu-id="c1e6d-724">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-724">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-725">forModelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-725">forModelId</span></span> |<span data-ttu-id="c1e6d-726">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-726">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-727">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-727">apiVersion</span></span> |<span data-ttu-id="c1e6d-728">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-728">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-729">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-729">Request Body</span></span> |<span data-ttu-id="c1e6d-730">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-730">NONE</span></span> |

<span data-ttu-id="c1e6d-731">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-731">**Response**:</span></span>

<span data-ttu-id="c1e6d-732">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-732">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-733">A resposta inclui uma entrada por arquivo de uso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-733">The response includes one entry per usage file.</span></span> <span data-ttu-id="c1e6d-734">Cada entrada tem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-734">Each entry has the following data:</span></span>

* <span data-ttu-id="c1e6d-735">`feed\entry\content\properties\Id` - ID do arquivo de uso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-735">`feed\entry\content\properties\Id` - Usage file ID.</span></span>
* <span data-ttu-id="c1e6d-736">`feed\entry\content\properties\Length` - Comprimento de arquivo de uso em MB.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span></span>
* <span data-ttu-id="c1e6d-737">`feed\entry\content\properties\DateModified` - Data da criação do arquivo de uso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-737">`feed\entry\content\properties\DateModified` - Date when the usage file was created.</span></span>
* <span data-ttu-id="c1e6d-738">`feed\entry\content\properties\UseInModel` - Se o arquivo de uso foi usado no modelo ou não.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-738">`feed\entry\content\properties\UseInModel` - Whether the usage file is used in the model.</span></span>

<span data-ttu-id="c1e6d-739">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-739">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of model's usage files info</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
            <updated>2014-10-30T09:40:25Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Id m:type="Edm.String">4c067b42-e975-4cb2-8c98-a6ab80ed6d63</d:Id>
                    <d:Length m:type="Edm.Double">0</d:Length>
                    <d:DateModified m:type="Edm.String">10/30/2014 9:19:57 AM</d:DateModified>
                    <d:UseInModel m:type="Edm.String">true</d:UseInModel>
                </m:properties>
            </content>
        </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetAListOfModelsUsageFilesInfoEntity</title>
        <updated>2014-10-30T09:40:25Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ListModelUsageFiles?forModelId='1c1110f8-7d9f-4c64-a807-4c9c5329993a'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">3126d816-4e80-4248-8339-1ebbdb9d544d</d:Id>
                <d:Length m:type="Edm.Double">0.001</d:Length>
                <d:DateModified m:type="Edm.String">10/30/2014 9:21:44 AM</d:DateModified>
                <d:UseInModel m:type="Edm.String">true</d:UseInModel>
              </m:properties>
        </content>
    </entry>
</feed>

### <a name="93----get-usage-statistics"></a><span data-ttu-id="c1e6d-740">9.3.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-740">9.3.</span></span>    <span data-ttu-id="c1e6d-741">Obter estatísticas de uso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-741">Get Usage Statistics</span></span>
<span data-ttu-id="c1e6d-742">Obter estatísticas de uso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-742">Gets usage statistics.</span></span>

| <span data-ttu-id="c1e6d-743">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-743">HTTP Method</span></span> | <span data-ttu-id="c1e6d-744">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-744">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-745">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-745">GET</span></span> |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-746">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-746">Example:</span></span><br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-747">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-747">Parameter Name</span></span> | <span data-ttu-id="c1e6d-748">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-748">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-749">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-749">modelId</span></span> |<span data-ttu-id="c1e6d-750">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-750">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-751">startDate</span><span class="sxs-lookup"><span data-stu-id="c1e6d-751">startDate</span></span> |<span data-ttu-id="c1e6d-752">Data de início.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-752">Start date.</span></span> <span data-ttu-id="c1e6d-753">Formato: aaaa/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="c1e6d-753">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="c1e6d-754">endDate</span><span class="sxs-lookup"><span data-stu-id="c1e6d-754">endDate</span></span> |<span data-ttu-id="c1e6d-755">Data de término.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-755">End date.</span></span> <span data-ttu-id="c1e6d-756">Formato: aaaa/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="c1e6d-756">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="c1e6d-757">eventTypes</span><span class="sxs-lookup"><span data-stu-id="c1e6d-757">eventTypes</span></span> |<span data-ttu-id="c1e6d-758">Cadeia de caracteres separada por vírgulas de tipos de eventos ou nulo para obter todos os eventos.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-758">Comma-separated string of event types or null to get all events</span></span> |
| <span data-ttu-id="c1e6d-759">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-759">apiVersion</span></span> |<span data-ttu-id="c1e6d-760">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-760">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-761">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-761">Request Body</span></span> |<span data-ttu-id="c1e6d-762">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-762">NONE</span></span> |

<span data-ttu-id="c1e6d-763">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-763">**Response**:</span></span>

<span data-ttu-id="c1e6d-764">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-764">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-765">Uma coleção de elementos de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-765">A collection of key/value elements.</span></span> <span data-ttu-id="c1e6d-766">Cada um deles contém a soma dos eventos para um tipo de evento específico agrupados por hora.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-766">Each one contains the sum of events for a specific event type grouped by hour.</span></span>

* <span data-ttu-id="c1e6d-767">`feed\entry[i]\content\properties\Key` - Contém a hora (agrupados por hora) e o tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-767">`feed\entry[i]\content\properties\Key` - Contains the time (grouped by hour) and the event type.</span></span>
* <span data-ttu-id="c1e6d-768">`feed\entry[i]\content\properties\Value` - Contagem de eventos total.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-768">`feed\entry[i]\content\properties\Value` - Total event count.</span></span>

<span data-ttu-id="c1e6d-769">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-769">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get usage statistics</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2014-11-18T11:39:16Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;Click</d:Event>
                <d:Value m:type="Edm.String">5</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/9/2014 8:00:00 AM;RecommendationClick</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
              </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/1/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
        <title type="text">GetUsageStatisticsEntity</title>
        <updated>2014-11-18T11:39:16Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUsageStatistics?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;startDate='2014/10/12T00:00:00'&amp;endDate='2014/11/10T00:00:00'&amp;eventTypes=''&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Event m:type="Edm.String">11/5/2014 8:00:00 AM;RemoveShopCart</d:Event>
                <d:Value m:type="Edm.String">10</d:Value>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="94----get-usage-file-sample"></a><span data-ttu-id="c1e6d-770">9.4.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-770">9.4.</span></span>    <span data-ttu-id="c1e6d-771">Obter um exemplo de arquivo de uso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-771">Get Usage File Sample</span></span>
<span data-ttu-id="c1e6d-772">Recupera os primeiros 2 KB de conteúdo de arquivos de uso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-772">Retrieves the first 2KB of usage file content.</span></span>

| <span data-ttu-id="c1e6d-773">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-773">HTTP Method</span></span> | <span data-ttu-id="c1e6d-774">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-774">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-775">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-775">GET</span></span> |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-776">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-776">Example:</span></span><br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-777">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-777">Parameter Name</span></span> | <span data-ttu-id="c1e6d-778">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-778">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-779">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-779">modelId</span></span> |<span data-ttu-id="c1e6d-780">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-780">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-781">fileId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-781">fileId</span></span> |<span data-ttu-id="c1e6d-782">Identificador exclusivo do arquivo de uso do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-782">Unique identifier of the model usage file</span></span> |
| <span data-ttu-id="c1e6d-783">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-783">apiVersion</span></span> |<span data-ttu-id="c1e6d-784">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-784">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-785">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-785">Request Body</span></span> |<span data-ttu-id="c1e6d-786">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-786">NONE</span></span> |

<span data-ttu-id="c1e6d-787">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-787">**Response**:</span></span>

<span data-ttu-id="c1e6d-788">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-788">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-789">A resposta é retornada no formato de texto sem formatação:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-789">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
</pre>


### <a name="95----get-model-usage-file"></a><span data-ttu-id="c1e6d-790">9.5.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-790">9.5.</span></span>    <span data-ttu-id="c1e6d-791">Obtenha o modelo do arquivo de uso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-791">Get Model Usage File</span></span>
<span data-ttu-id="c1e6d-792">Recupera o conteúdo completo do arquivo de uso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-792">Retrieves the full content of the usage file.</span></span>

| <span data-ttu-id="c1e6d-793">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-793">HTTP Method</span></span> | <span data-ttu-id="c1e6d-794">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-794">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-795">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-795">GET</span></span> |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-796">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-796">Example:</span></span><br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-797">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-797">Parameter Name</span></span> | <span data-ttu-id="c1e6d-798">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-798">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-799">mid</span><span class="sxs-lookup"><span data-stu-id="c1e6d-799">mid</span></span> |<span data-ttu-id="c1e6d-800">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-800">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-801">fid</span><span class="sxs-lookup"><span data-stu-id="c1e6d-801">fid</span></span> |<span data-ttu-id="c1e6d-802">Identificador exclusivo do arquivo de uso do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-802">Unique identifier of the model usage file</span></span> |
| <span data-ttu-id="c1e6d-803">baixar</span><span class="sxs-lookup"><span data-stu-id="c1e6d-803">download</span></span> |<span data-ttu-id="c1e6d-804">1</span><span class="sxs-lookup"><span data-stu-id="c1e6d-804">1</span></span> |
| <span data-ttu-id="c1e6d-805">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-805">apiVersion</span></span> |<span data-ttu-id="c1e6d-806">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-806">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-807">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-807">Request Body</span></span> |<span data-ttu-id="c1e6d-808">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-808">NONE</span></span> |

<span data-ttu-id="c1e6d-809">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-809">**Response**:</span></span>

<span data-ttu-id="c1e6d-810">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-810">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-811">A resposta é retornada no formato de texto sem formatação:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-811">Response is returned in raw text format:</span></span>

<pre>
85526,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
210926,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
116866,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
177458,2406E770-769C-4189-89DE-1C9283F93A96,2014/11/02T13:40:15,True,1
274004,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
123883,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
37712,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
152249,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
250948,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
235588,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
158254,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
271195,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
141157,21BF8088-B6C0-4509-870C-E1C7AC78304A,2014/11/02T13:40:15,True,1
171118,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
225087,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
244881,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
50547,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
213090,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
260655,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
72214,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
36326,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189336,3BB5CB44-D143-4BDD-A55C-443964BF4B23,2014/11/02T13:40:15,True,1
189334,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260655,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
162100,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
54946,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
260965,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
102758,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
112602,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
163925,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
262998,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
144717,552A1940-21E4-4399-82BB-594B46D7ED54,2014/11/02T13:40:15,True,1
</pre>

### <a name="96----delete-usage-file"></a><span data-ttu-id="c1e6d-812">9.6.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-812">9.6.</span></span>    <span data-ttu-id="c1e6d-813">Excluir o arquivo de uso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-813">Delete Usage File</span></span>
<span data-ttu-id="c1e6d-814">Exclui o arquivo de uso do modelo especificado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-814">Deletes the specified model usage file.</span></span>

| <span data-ttu-id="c1e6d-815">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-815">HTTP Method</span></span> | <span data-ttu-id="c1e6d-816">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-816">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-817">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="c1e6d-817">DELETE</span></span> |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-818">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-818">Example:</span></span><br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-819">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-819">Parameter Name</span></span> | <span data-ttu-id="c1e6d-820">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-820">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-821">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-821">modelId</span></span> |<span data-ttu-id="c1e6d-822">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-822">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-823">fileId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-823">fileId</span></span> |<span data-ttu-id="c1e6d-824">Identificador exclusivo do arquivo a ser excluído</span><span class="sxs-lookup"><span data-stu-id="c1e6d-824">Unique identifier of the file to be deleted</span></span> |
| <span data-ttu-id="c1e6d-825">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-825">apiVersion</span></span> |<span data-ttu-id="c1e6d-826">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-826">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-827">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-827">Request Body</span></span> |<span data-ttu-id="c1e6d-828">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-828">NONE</span></span> |

<span data-ttu-id="c1e6d-829">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-829">**Response**:</span></span>

<span data-ttu-id="c1e6d-830">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-830">HTTP Status code: 200</span></span>

### <a name="97----delete-all-usage-files"></a><span data-ttu-id="c1e6d-831">9.7.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-831">9.7.</span></span>    <span data-ttu-id="c1e6d-832">Excluir todos os arquivos de uso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-832">Delete All Usage Files</span></span>
<span data-ttu-id="c1e6d-833">Exclui todos os arquivos de uso do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-833">Deletes all model usage files.</span></span>

| <span data-ttu-id="c1e6d-834">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-834">HTTP Method</span></span> | <span data-ttu-id="c1e6d-835">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-835">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-836">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="c1e6d-836">DELETE</span></span> |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-837">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-837">Example:</span></span><br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-838">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-838">Parameter Name</span></span> | <span data-ttu-id="c1e6d-839">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-839">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-840">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-840">modelId</span></span> |<span data-ttu-id="c1e6d-841">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-841">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-842">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-842">apiVersion</span></span> |<span data-ttu-id="c1e6d-843">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-843">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-844">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-844">Request Body</span></span> |<span data-ttu-id="c1e6d-845">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-845">NONE</span></span> |

<span data-ttu-id="c1e6d-846">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-846">**Response**:</span></span>

<span data-ttu-id="c1e6d-847">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-847">HTTP Status code: 200</span></span>

## <a name="10-features"></a><span data-ttu-id="c1e6d-848">10. Recursos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-848">10. Features</span></span>
<span data-ttu-id="c1e6d-849">Esta seção mostra como recuperar informações de recurso, como os recursos importados e seus valores, sua classificação e quando essa classificação foi alocada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-849">This section shows how to retrieve feature information, such as the imported features and their values, their rank, and when this rank was allocated.</span></span> <span data-ttu-id="c1e6d-850">Os recursos são importados como parte dos dados do catálogo e, em seguida, sua posição é associada quando uma compilação de classificação é criada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-850">Features are imported as part of the catalog data, and then their rank is associated when a rank build is done.</span></span>
<span data-ttu-id="c1e6d-851">A classificação de recursos pode mudar de acordo com o padrão dos dados de uso e tipo de itens.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-851">Feature rank can change according to the pattern of usage data and type of items.</span></span> <span data-ttu-id="c1e6d-852">Mas, para uso/itens consistentes, a classificação deve ter apenas pequenas flutuações.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-852">But for consistent usage/items, the rank should have only small fluctuations.</span></span>
<span data-ttu-id="c1e6d-853">A classificação de recursos é um número não negativo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-853">The rank of features is a non-negative number.</span></span> <span data-ttu-id="c1e6d-854">O número 0 significa que o recurso não foi classificado (acontece se você invocar essa API antes da conclusão da primeira compilação de classificação).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-854">The  number 0 means that the feature was not ranked (happens if you invoke this API prior to the completion of the first rank build).</span></span> <span data-ttu-id="c1e6d-855">A data em que a classificação foi atribuída é chamada de atualização da pontuação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-855">The date at which the rank was attributed is called the score freshness.</span></span>

### <a name="101-get-features-info-for-last-rank-build"></a><span data-ttu-id="c1e6d-856">10.1.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-856">10.1.</span></span> <span data-ttu-id="c1e6d-857">Obter informações de recursos (para a última compilação de classificação)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-857">Get Features Info (For Last Rank Build)</span></span>
<span data-ttu-id="c1e6d-858">Recupera as informações de recurso, incluindo classificação, para a última compilação de classificação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-858">Retrieves the feature information, including ranking, for the last successful rank build.</span></span>

| <span data-ttu-id="c1e6d-859">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-859">HTTP Method</span></span> | <span data-ttu-id="c1e6d-860">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-860">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-861">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-861">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-862">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-862">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-863">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-863">Parameter Name</span></span> | <span data-ttu-id="c1e6d-864">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-864">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-865">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-865">modelId</span></span> |<span data-ttu-id="c1e6d-866">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-866">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-867">samplingSize</span><span class="sxs-lookup"><span data-stu-id="c1e6d-867">samplingSize</span></span> |<span data-ttu-id="c1e6d-868">Número de valores a serem incluídos para cada recurso de acordo com os dados presentes no catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-868">Number of values to include for each feature according to the data present in the catalog.</span></span> <br/><span data-ttu-id="c1e6d-869">Os valores possíveis são:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-869">Possible values are:</span></span><br> <span data-ttu-id="c1e6d-870">- 1 - Todas as amostras.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-870">-1 - All samples.</span></span> <br><span data-ttu-id="c1e6d-871">0 - Sem amostragem.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-871">0 - No sampling.</span></span> <br><span data-ttu-id="c1e6d-872">N - Retornar N amostras para cada nome de recurso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-872">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="c1e6d-873">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-873">apiVersion</span></span> |<span data-ttu-id="c1e6d-874">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-874">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-875">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-875">Request Body</span></span> |<span data-ttu-id="c1e6d-876">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-876">NONE</span></span> |

<span data-ttu-id="c1e6d-877">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-877">**Response**:</span></span>

<span data-ttu-id="c1e6d-878">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-878">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-879">A resposta contém uma lista de entradas de informações de recurso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-879">The response contains a list of feature info entries.</span></span> <span data-ttu-id="c1e6d-880">Cada entrada contém:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-880">Each entry contains:</span></span>

* <span data-ttu-id="c1e6d-881">`feed/entry/content/m:properties/d:Name` - Nome do recurso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="c1e6d-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Data em que a classificação foi alocada para esse recurso, conhecido como</span><span class="sxs-lookup"><span data-stu-id="c1e6d-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which the rank was allocated to this feature, a.k.a.</span></span> <span data-ttu-id="c1e6d-883">recurso de atualização de pontuação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-883">score freshness feature.</span></span> <span data-ttu-id="c1e6d-884">Uma data do histórico (“0001-01-01T00:00:00”) significa que nenhuma compilação de classificação foi executada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="c1e6d-885">`feed/entry/content/m:properties/d:Rank` - Classificação de recurso (float).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="c1e6d-886">Uma classificação de 2.0 e superior é considerada um bom recurso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-886">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="c1e6d-887">`feed/entry/content/m:properties/d:SampleValues` - Lista separada por vírgulas dos valores até o tamanho de amostragem solicitado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up to the sampling size requested.</span></span>

<span data-ttu-id="c1e6d-888">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-888">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get the features of a model</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-01-08T13:15:02Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Author</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Name m:type="Edm.String">Publisher</d:Name>
                <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
                <d:Rank m:type="Edm.String">0</d:Rank>
                <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
            </m:properties>
        </content>
    </entry>
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
        <title type="text">ModelFeaturesEntity</title>
        <updated>2015-01-08T13:15:02Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1"/>
        <contenttype="application/xml">
        <m:properties>
            <d:Name m:type="Edm.String">Year</d:Name>
            <d:RankUpdateDate m:type="Edm.String">0001-01-01T00:00:00</d:RankUpdateDate>
            <d:Rank m:type="Edm.String">0</d:Rank>
            <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
        </m:properties>
        </content>
    </entry>
</feed>

### <a name="102-get-features-info-for-specific-rank-build"></a><span data-ttu-id="c1e6d-889">10.2.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-889">10.2.</span></span> <span data-ttu-id="c1e6d-890">Obter informações de recursos (para uma compilação de classificação específica)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-890">Get Features Info (For Specific Rank Build)</span></span>
<span data-ttu-id="c1e6d-891">Recupera as informações de recurso, incluindo a classificação, para uma compilação de classificação específica.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-891">Retrieves the feature information, including the ranking for a specific rank build.</span></span>

| <span data-ttu-id="c1e6d-892">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-892">HTTP Method</span></span> | <span data-ttu-id="c1e6d-893">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-893">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-894">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-894">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-895">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-895">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-896">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-896">Parameter Name</span></span> | <span data-ttu-id="c1e6d-897">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-897">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-898">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-898">modelId</span></span> |<span data-ttu-id="c1e6d-899">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-899">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-900">samplingSize</span><span class="sxs-lookup"><span data-stu-id="c1e6d-900">samplingSize</span></span> |<span data-ttu-id="c1e6d-901">Número de valores a serem incluídos para cada recurso de acordo com os dados presentes no catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-901">Number of values to include for each feature according to the data present in the catalog.</span></span><br/> <span data-ttu-id="c1e6d-902">Os valores possíveis são:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-902">Possible values are:</span></span><br> <span data-ttu-id="c1e6d-903">- 1 - Todas as amostras.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-903">-1 - All samples.</span></span> <br><span data-ttu-id="c1e6d-904">0 - Sem amostragem.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-904">0 - No sampling.</span></span> <br><span data-ttu-id="c1e6d-905">N - Retornar N amostras para cada nome de recurso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-905">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="c1e6d-906">rankBuildId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-906">rankBuildId</span></span> |<span data-ttu-id="c1e6d-907">Identificador exclusivo da compilação de classificação ou -1 para a última compilação de classificação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-907">Unique identifier of the rank build or -1 for the last rank build</span></span> |
| <span data-ttu-id="c1e6d-908">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-908">apiVersion</span></span> |<span data-ttu-id="c1e6d-909">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-909">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-910">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-910">Request Body</span></span> |<span data-ttu-id="c1e6d-911">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-911">NONE</span></span> |

<span data-ttu-id="c1e6d-912">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-912">**Response**:</span></span>

<span data-ttu-id="c1e6d-913">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-913">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-914">A resposta contém uma lista de entradas de informações de recurso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-914">The response contains a list of feature info entries.</span></span> <span data-ttu-id="c1e6d-915">Cada entrada contém:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-915">Each entry contains:</span></span>

* <span data-ttu-id="c1e6d-916">`feed/entry/content/m:properties/d:Name` - Nome do recurso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="c1e6d-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Data em que a classificação foi alocada para esse recurso, conhecido como</span><span class="sxs-lookup"><span data-stu-id="c1e6d-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which the rank was allocated to this feature, a.k.a.</span></span> <span data-ttu-id="c1e6d-918">recurso de atualização de pontuação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-918">score freshness feature.</span></span> <span data-ttu-id="c1e6d-919">Uma data do histórico (“0001-01-01T00:00:00”) significa que nenhuma compilação de classificação foi executada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="c1e6d-920">`feed/entry/content/m:properties/d:Rank` - Classificação de recurso (float).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="c1e6d-921">Uma classificação de 2.0 e superior é considerada um bom recurso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-921">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="c1e6d-922">`feed/entry/content/m:properties/d:SampleValues` - Lista separada por vírgulas dos valores até o tamanho de amostragem solicitado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up to the sampling size requested.</span></span>

<span data-ttu-id="c1e6d-923">OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-923">OData</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get the features of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:54:22Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Author</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">3.38867426</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. A. Attanasio, A. A. Milne, A. Bates, A. C. Bhaktivedanta Swami Prabhupada et al., A. C. Crispin, A. C. Doyle, A. C. H. Smith, A. E. Parker, A. J. Holt, A. J. Matthews</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Publisher</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.67839336</d:Rank>
                    <d:SampleValues m:type="Edm.String">A. Mondadori, Abacus, Abacus Press, Abacus Uk, Abstract Studio, Acacia Press, Academy Chicago Publishers, Ace Books, ACE Charter, Actar</d:SampleValues>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">ModelFeaturesEntity</title>
            <updated>2015-01-08T13:54:22Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures?modelId='f13ab2e8-b530-4aa1-86f7-2f4a24714765'&amp;samplingSize='10'&amp;rankBuildId=1000653&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Name m:type="Edm.String">Year</d:Name>
                    <d:RankUpdateDate m:type="Edm.String">2015-01-08T13:52:14.673</d:RankUpdateDate>
                    <d:Rank m:type="Edm.String">1.12352145</d:Rank>
                    <d:SampleValues m:type="Edm.String">0, 1920, 1926, 1927, 1929, 1930, 1932, 1942, 1943, 1946</d:SampleValues>
                </m:properties>
            </content>
        </entry>
    </feed>


## <a name="11-build"></a><span data-ttu-id="c1e6d-924">11. Compilação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-924">11. Build</span></span>
  <span data-ttu-id="c1e6d-925">Esta seção explica as diferentes APIs relacionadas a compilações.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-925">This section explains the different APIs related to builds.</span></span> <span data-ttu-id="c1e6d-926">Existem 3 tipos de compilações: uma compilação de recomendação, uma compilação de classificação e uma compilação FBT (frequentemente comprada junto).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span></span>

<span data-ttu-id="c1e6d-927">A compilação de recomendação tem o objetivo de gerar um modelo de recomendação usado para previsões.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-927">The recommendation build's purpose is to generate a recommendation model used for predictions.</span></span> <span data-ttu-id="c1e6d-928">As previsões (para esse tipo de compilação) vêm em duas versões:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-928">Predictions (for this type of build) come in two flavors:</span></span>

* <span data-ttu-id="c1e6d-929">I2I - também conhecido como</span><span class="sxs-lookup"><span data-stu-id="c1e6d-929">I2I - a.k.a.</span></span> <span data-ttu-id="c1e6d-930">Recomendações de Item a Item - ao receber um item ou uma lista de itens, essa opção poderá prever uma lista de itens que provavelmente serão de grande interesse.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-930">Item to Item recommendations - given an item or a list of items this option will predict a list of items that are likely to be of high interest.</span></span>
* <span data-ttu-id="c1e6d-931">U2I - também conhecido como</span><span class="sxs-lookup"><span data-stu-id="c1e6d-931">U2I - a.k.a.</span></span> <span data-ttu-id="c1e6d-932">Recomendações do Usuário ao Item - ao receber uma ID de usuário (e, opcionalmente, uma lista de itens), essa opção poderá prever uma lista de itens que provavelmente serão de grande interesse para o usuário especificado (e suas opções adicionais de itens).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-932">User to Item recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely to be of high interest for the given user (and its additional choice of items).</span></span> <span data-ttu-id="c1e6d-933">As recomendações de U2I são baseadas no histórico de itens que foram de interesse do usuário até o momento em que o modelo foi criado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-933">The U2I recommendations are based on the history of items that were of interest for the user up to the time the model was built.</span></span>

<span data-ttu-id="c1e6d-934">Uma compilação de classificação é uma compilação técnica que permite que você saiba mais sobre a utilidade dos seus recursos.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-934">A rank build is a technical build that allows you to learn about the usefulness of your features.</span></span> <span data-ttu-id="c1e6d-935">Geralmente, para obter o melhor resultado para um modelo de recomendação que envolve recursos, siga as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-935">Usually, in order to get the best result for a recommendation model involving features, you should take the following steps:</span></span>

* <span data-ttu-id="c1e6d-936">Dispare uma compilação de classificação (a menos que a pontuação dos seus recursos seja estável) e aguarde até obter a pontuação do recurso.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-936">Trigger a rank build (unless the score of your features is stable) and wait till you get the feature score.</span></span>
* <span data-ttu-id="c1e6d-937">Obtenha a classificação dos recursos chamando a API [Obter informações de recursos](#101-get-features-info-for-last-rank-build) .</span><span class="sxs-lookup"><span data-stu-id="c1e6d-937">Retrieve the rank of your features by calling the [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span></span>
* <span data-ttu-id="c1e6d-938">Configure uma compilação de recomendação com os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-938">Configure a recommendation build with the following parameters:</span></span>
  * <span data-ttu-id="c1e6d-939">`useFeatureInModel` – definido como True.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-939">`useFeatureInModel` - Set to True.</span></span>
  * <span data-ttu-id="c1e6d-940">`ModelingFeatureList` – definido como uma lista separada por vírgulas de recursos com uma pontuação de 2,0 ou mais (de acordo com as classificações que você recuperou na etapa anterior).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-940">`ModelingFeatureList` - Set to a comma-separated list of features with a score of 2.0 or more (according to the ranks you retrieved in the previous step).</span></span>
  * <span data-ttu-id="c1e6d-941">`AllowColdItemPlacement` – definido como True.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-941">`AllowColdItemPlacement` - Set to True.</span></span>
  * <span data-ttu-id="c1e6d-942">Opcionalmente, você pode definir `EnableFeatureCorrelation` como True e `ReasoningFeatureList` para a lista de recursos que deseja usar para obter explicações (normalmente é a mesma lista de recursos usada na modelagem ou uma sublista).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-942">Optionally you can set `EnableFeatureCorrelation` to True and `ReasoningFeatureList` to the list of features you want to use for explanations (usually the same list of features used in modelling or a sublist).</span></span>
* <span data-ttu-id="c1e6d-943">Dispare a compilação de recomendação com os parâmetros configurados.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-943">Trigger the recommendation build with the configured parameters.</span></span>

<span data-ttu-id="c1e6d-944">Observação: se você não definir nenhum parâmetro (por exemplo, invocar a compilação de recomendação sem parâmetros) ou se você não desabilitar explicitamente o uso de recursos (por exemplo, `UseFeatureInModel` definido como Falso), o sistema vai configurar os parâmetros relacionados a recursos aos valores explicados acima caso exista uma compilação de classificação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-944">Note: If you do not configure any parameters (e.g. invoke the recommendation build without parameters) or you do not explicitly disable the usage of features (e.g. `UseFeatureInModel` set to False), the system will set up the feature-related parameters to the explained values above in case a rank build exists.</span></span>

<span data-ttu-id="c1e6d-945">Não há nenhuma restrição sobre como executar uma compilação de classificação e uma compilação de recomendação simultaneamente para o mesmo modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-945">There is no restriction on running a rank build and a recommendation build concurrently for the same model.</span></span> <span data-ttu-id="c1e6d-946">No entanto, não é possível executar duas compilações do mesmo tipo no mesmo modelo em paralelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-946">Nevertheless, you cannot run two builds of the same type on the same model in parallel.</span></span>

<span data-ttu-id="c1e6d-947">Uma compilação FBT (Frequentemente Comprado Juntos) é outro algoritmo de recomendações chamado por vezes de recomendador "conservador", o que é bom para os catálogos não homogêneos por natureza (homogêneas: livros, filmes, alguns alimentos, moda; não homogêneo: computadores e dispositivos, entre domínios, altamente diversificados).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span></span>

<span data-ttu-id="c1e6d-948">Observação: se os arquivos de uso que você carregou contiverem o campo opcional "tipo de evento", somente os eventos “Compra” serão usados para modelagem FBT.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-948">Note: if the usage files that you uploaded contain the optional field "event type" then for FBT modelling only "Purchase" events will be used.</span></span> <span data-ttu-id="c1e6d-949">Se nenhum tipo de evento for fornecido, todos os eventos serão considerados como compra.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-949">If no event type is provided all events will be considered as purchase.</span></span>

#### <a name="111-build-parameters"></a><span data-ttu-id="c1e6d-950">11.1 Parâmetros de compilação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-950">11.1 Build parameters</span></span>
<span data-ttu-id="c1e6d-951">Cada tipo de compilação pode ser configurado por meio de um conjunto de parâmetros (descritos abaixo).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-951">Each build type can be configured via a set of parameters (depicted below).</span></span> <span data-ttu-id="c1e6d-952">Se você não configurar os parâmetros, o sistema atribuirá automaticamente valores aos parâmetros de acordo com as informações presentes ao disparar uma compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-952">If you don't configure the parameters, the system will automatically attribute values to the parameters according to the information present at the time you trigger a build.</span></span>

##### <a name="1111-usage-condenser"></a><span data-ttu-id="c1e6d-953">11.1.1.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-953">11.1.1.</span></span> <span data-ttu-id="c1e6d-954">Condensador de uso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-954">Usage condenser</span></span>
<span data-ttu-id="c1e6d-955">Os usuários ou itens com poucos pontos de uso podem conter mais ruído que informações.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-955">Users or items with few usage points might contain more noise than information.</span></span> <span data-ttu-id="c1e6d-956">O sistema tenta prever o número mínimo de pontos de uso por usuário/item a ser usado em um modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-956">The system attempts to predict the minimal number of usage points per user/item to be used in a model.</span></span> <span data-ttu-id="c1e6d-957">Esse número estará dentro do intervalo definido pelos parâmetros ItemCutoffLowerBound e ItemCutoffUpperBound para itens, e o intervalo definido pelos parâmetros UserCutOffLowerBound e UserCutoffUpperBound para os usuários.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-957">This number will be within the range defined by the ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and the range defined by the UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span></span> <span data-ttu-id="c1e6d-958">O efeito condensador sobre os itens ou usuários pode ser minimizado ao configurar pelo menos um dos limites correspondentes a zero.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-958">The condenser effect on items or users can be minimized by setting at least one of the corresponding bounds to zero.</span></span>

##### <a name="1112-rank-build-parameters"></a><span data-ttu-id="c1e6d-959">11.1.2.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-959">11.1.2.</span></span> <span data-ttu-id="c1e6d-960">Parâmetros de compilação de classificação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-960">Rank build parameters</span></span>
<span data-ttu-id="c1e6d-961">A tabela a seguir descreve os parâmetros de compilação para uma compilação de classificação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-961">The table below depicts the build parameters for a rank build.</span></span>

| <span data-ttu-id="c1e6d-962">Chave</span><span class="sxs-lookup"><span data-stu-id="c1e6d-962">Key</span></span> | <span data-ttu-id="c1e6d-963">Descrição</span><span class="sxs-lookup"><span data-stu-id="c1e6d-963">Description</span></span> | <span data-ttu-id="c1e6d-964">Tipo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-964">Type</span></span> | <span data-ttu-id="c1e6d-965">Valor Válido</span><span class="sxs-lookup"><span data-stu-id="c1e6d-965">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c1e6d-966">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="c1e6d-966">NumberOfModelIterations</span></span> |<span data-ttu-id="c1e6d-967">O número de iterações que o modelo executa é refletido pelo tempo de computação geral e a precisão do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-967">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="c1e6d-968">Quanto maior o número, maior será a precisão obtida, mas o tempo de computação será mais longo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-968">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="c1e6d-969">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-969">Integer</span></span> |<span data-ttu-id="c1e6d-970">10-50</span><span class="sxs-lookup"><span data-stu-id="c1e6d-970">10-50</span></span> |
| <span data-ttu-id="c1e6d-971">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="c1e6d-971">NumberOfModelDimensions</span></span> |<span data-ttu-id="c1e6d-972">O número de dimensões está relacionado ao número de “recursos” que o modelo tentará localizar em seus dados.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-972">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="c1e6d-973">Aumentar o número de dimensões possibilitará um melhor ajuste dos resultados em clusters menores.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-973">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="c1e6d-974">No entanto, ter muitas dimensões impedirá que o modelo localize correlações entre itens.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-974">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="c1e6d-975">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-975">Integer</span></span> |<span data-ttu-id="c1e6d-976">10-40</span><span class="sxs-lookup"><span data-stu-id="c1e6d-976">10-40</span></span> |
| <span data-ttu-id="c1e6d-977">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="c1e6d-977">ItemCutOffLowerBound</span></span> |<span data-ttu-id="c1e6d-978">Define o limite inferior de item para o condensador.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-978">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="c1e6d-979">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-979">See usage condenser above.</span></span> |<span data-ttu-id="c1e6d-980">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-980">Integer</span></span> |<span data-ttu-id="c1e6d-981">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-981">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="c1e6d-982">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="c1e6d-982">ItemCutOffUpperBound</span></span> |<span data-ttu-id="c1e6d-983">Define o limite superior de item para o condensador.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-983">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="c1e6d-984">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-984">See usage condenser above.</span></span> |<span data-ttu-id="c1e6d-985">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-985">Integer</span></span> |<span data-ttu-id="c1e6d-986">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-986">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="c1e6d-987">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="c1e6d-987">UserCutOffLowerBound</span></span> |<span data-ttu-id="c1e6d-988">Define o limite inferior de usuário para o condensador.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-988">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="c1e6d-989">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-989">See usage condenser above.</span></span> |<span data-ttu-id="c1e6d-990">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-990">Integer</span></span> |<span data-ttu-id="c1e6d-991">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-991">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="c1e6d-992">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="c1e6d-992">UserCutOffUpperBound</span></span> |<span data-ttu-id="c1e6d-993">Define o limite superior de usuário para o condensador.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-993">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="c1e6d-994">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-994">See usage condenser above.</span></span> |<span data-ttu-id="c1e6d-995">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-995">Integer</span></span> |<span data-ttu-id="c1e6d-996">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-996">2 or more (0 disable condenser)</span></span> |

##### <a name="1113-recommendation-build-parameters"></a><span data-ttu-id="c1e6d-997">11.1.3.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-997">11.1.3.</span></span> <span data-ttu-id="c1e6d-998">Parâmetros de compilação de recomendação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-998">Recommendation build parameters</span></span>
<span data-ttu-id="c1e6d-999">A tabela a seguir descreve os parâmetros de compilação para uma compilação de recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-999">The table below depicts the build parameters for recommendation build.</span></span>

| <span data-ttu-id="c1e6d-1000">Chave</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1000">Key</span></span> | <span data-ttu-id="c1e6d-1001">Descrição</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1001">Description</span></span> | <span data-ttu-id="c1e6d-1002">Tipo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1002">Type</span></span> | <span data-ttu-id="c1e6d-1003">Valor Válido</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1003">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c1e6d-1004">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1004">NumberOfModelIterations</span></span> |<span data-ttu-id="c1e6d-1005">O número de iterações que o modelo executa é refletido pelo tempo de computação geral e a precisão do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1005">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="c1e6d-1006">Quanto maior o número, maior será a precisão obtida, mas o tempo de computação será mais longo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1006">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="c1e6d-1007">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1007">Integer</span></span> |<span data-ttu-id="c1e6d-1008">10-50</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1008">10-50</span></span> |
| <span data-ttu-id="c1e6d-1009">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1009">NumberOfModelDimensions</span></span> |<span data-ttu-id="c1e6d-1010">O número de dimensões está relacionado ao número de “recursos” que o modelo tentará localizar em seus dados.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1010">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="c1e6d-1011">Aumentar o número de dimensões possibilitará um melhor ajuste dos resultados em clusters menores.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1011">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="c1e6d-1012">No entanto, ter muitas dimensões impedirá que o modelo localize correlações entre itens.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1012">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="c1e6d-1013">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1013">Integer</span></span> |<span data-ttu-id="c1e6d-1014">10-40</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1014">10-40</span></span> |
| <span data-ttu-id="c1e6d-1015">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1015">ItemCutOffLowerBound</span></span> |<span data-ttu-id="c1e6d-1016">Define o limite inferior de item para o condensador.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1016">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="c1e6d-1017">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1017">See usage condenser above.</span></span> |<span data-ttu-id="c1e6d-1018">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1018">Integer</span></span> |<span data-ttu-id="c1e6d-1019">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1019">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="c1e6d-1020">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1020">ItemCutOffUpperBound</span></span> |<span data-ttu-id="c1e6d-1021">Define o limite superior de item para o condensador.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1021">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="c1e6d-1022">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1022">See usage condenser above.</span></span> |<span data-ttu-id="c1e6d-1023">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1023">Integer</span></span> |<span data-ttu-id="c1e6d-1024">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1024">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="c1e6d-1025">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1025">UserCutOffLowerBound</span></span> |<span data-ttu-id="c1e6d-1026">Define o limite inferior de usuário para o condensador.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1026">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="c1e6d-1027">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1027">See usage condenser above.</span></span> |<span data-ttu-id="c1e6d-1028">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1028">Integer</span></span> |<span data-ttu-id="c1e6d-1029">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1029">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="c1e6d-1030">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1030">UserCutOffUpperBound</span></span> |<span data-ttu-id="c1e6d-1031">Define o limite superior de usuário para o condensador.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1031">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="c1e6d-1032">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1032">See usage condenser above.</span></span> |<span data-ttu-id="c1e6d-1033">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1033">Integer</span></span> |<span data-ttu-id="c1e6d-1034">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1034">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="c1e6d-1035">Descrição</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1035">Description</span></span> |<span data-ttu-id="c1e6d-1036">Descrição da compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1036">Build description.</span></span> |<span data-ttu-id="c1e6d-1037">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1037">String</span></span> |<span data-ttu-id="c1e6d-1038">Qualquer texto, máximo de 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1038">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="c1e6d-1039">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1039">EnableModelingInsights</span></span> |<span data-ttu-id="c1e6d-1040">Permite computar métricas sobre o modelo de recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1040">Allows you to compute metrics on the recommendation model.</span></span> |<span data-ttu-id="c1e6d-1041">Booliano</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1041">Boolean</span></span> |<span data-ttu-id="c1e6d-1042">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1042">True/False</span></span> |
| <span data-ttu-id="c1e6d-1043">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1043">UseFeaturesInModel</span></span> |<span data-ttu-id="c1e6d-1044">Indica se os recursos podem ser usados para aperfeiçoar o modelo de recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1044">Indicates if features can be used in order to enhance the recommendation model.</span></span> |<span data-ttu-id="c1e6d-1045">Booliano</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1045">Boolean</span></span> |<span data-ttu-id="c1e6d-1046">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1046">True/False</span></span> |
| <span data-ttu-id="c1e6d-1047">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1047">ModelingFeatureList</span></span> |<span data-ttu-id="c1e6d-1048">Lista separada por vírgulas de nomes de recursos a serem usados na compilação de recomendação a fim de melhorar as recomendações.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1048">Comma-separated list of feature names to be used in the recommendation build, in order to enhance the recommendation.</span></span> |<span data-ttu-id="c1e6d-1049">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1049">String</span></span> |<span data-ttu-id="c1e6d-1050">Nomes de recursos, até 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1050">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="c1e6d-1051">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1051">AllowColdItemPlacement</span></span> |<span data-ttu-id="c1e6d-1052">Indica se a recomendação também enviar itens sem interesse através da similaridade de recursos.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1052">Indicates if the recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="c1e6d-1053">Booliano</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1053">Boolean</span></span> |<span data-ttu-id="c1e6d-1054">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1054">True/False</span></span> |
| <span data-ttu-id="c1e6d-1055">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1055">EnableFeatureCorrelation</span></span> |<span data-ttu-id="c1e6d-1056">Indica se os recursos podem ser usados no raciocínio.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1056">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="c1e6d-1057">Booliano</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1057">Boolean</span></span> |<span data-ttu-id="c1e6d-1058">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1058">True/False</span></span> |
| <span data-ttu-id="c1e6d-1059">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1059">ReasoningFeatureList</span></span> |<span data-ttu-id="c1e6d-1060">Lista separada por vírgulas de nomes de recursos a serem usado em frases de raciocínio (isto é, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1060">Comma-separated list of feature names to be used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="c1e6d-1061">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1061">String</span></span> |<span data-ttu-id="c1e6d-1062">Nomes de recursos, até 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1062">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="c1e6d-1063">EnableU2I</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1063">EnableU2I</span></span> |<span data-ttu-id="c1e6d-1064">Permitir a recomendação personalizada também conhecido como</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1064">Allow the personalized recommendation a.k.a.</span></span> <span data-ttu-id="c1e6d-1065">U2I (usuário às recomendações de item).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1065">U2I (user to item recommendations).</span></span> |<span data-ttu-id="c1e6d-1066">Booliano</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1066">Boolean</span></span> |<span data-ttu-id="c1e6d-1067">True/False (verdadeiro por padrão)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1067">True/False (default true)</span></span> |

##### <a name="1114-fbt-build-parameters"></a><span data-ttu-id="c1e6d-1068">11.1.4.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1068">11.1.4.</span></span> <span data-ttu-id="c1e6d-1069">Parâmetros de compilação FBT</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1069">FBT build parameters</span></span>
<span data-ttu-id="c1e6d-1070">A tabela a seguir descreve os parâmetros de compilação para uma compilação de recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1070">The table below depicts the build parameters for recommendation build.</span></span>

| <span data-ttu-id="c1e6d-1071">Chave</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1071">Key</span></span> | <span data-ttu-id="c1e6d-1072">Descrição</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1072">Description</span></span> | <span data-ttu-id="c1e6d-1073">Tipo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1073">Type</span></span> | <span data-ttu-id="c1e6d-1074">Valor Válido (Padrão)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1074">Valid Value (Default)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c1e6d-1075">FbtSupportThreshold</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1075">FbtSupportThreshold</span></span> |<span data-ttu-id="c1e6d-1076">O quanto o modelo é conservador.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1076">How conservative the model is.</span></span> <span data-ttu-id="c1e6d-1077">O número de co-ocorrências de itens a ser considerado para modelagem.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1077">Number of co-occurrences of items to be considered for modeling.</span></span> |<span data-ttu-id="c1e6d-1078">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1078">Integer</span></span> |<span data-ttu-id="c1e6d-1079">3-50 (6)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1079">3-50 (6)</span></span> |
| <span data-ttu-id="c1e6d-1080">FbtMaxItemSetSize</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1080">FbtMaxItemSetSize</span></span> |<span data-ttu-id="c1e6d-1081">Limita o número de itens em um conjunto frequente.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1081">Bounds the number of items in a frequent set.</span></span> |<span data-ttu-id="c1e6d-1082">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1082">Integer</span></span> |<span data-ttu-id="c1e6d-1083">2-3 (2)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1083">2-3 (2)</span></span> |
| <span data-ttu-id="c1e6d-1084">FbtMinimalScore</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1084">FbtMinimalScore</span></span> |<span data-ttu-id="c1e6d-1085">Pontuação mínima que um conjunto frequente deve ter para ser incluído nos resultados retornados.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1085">Minimal score that a frequent set should have in order to be included in the returned results.</span></span> <span data-ttu-id="c1e6d-1086">Quanto maior, melhor.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1086">The higher the better.</span></span> |<span data-ttu-id="c1e6d-1087">Duplo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1087">Double</span></span> |<span data-ttu-id="c1e6d-1088">0 e acima (0)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1088">0 and above (0)</span></span> |
| <span data-ttu-id="c1e6d-1089">FbtSimilarityFunction</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1089">FbtSimilarityFunction</span></span> |<span data-ttu-id="c1e6d-1090">Define a função de semelhança a ser usada pela compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1090">Defines the similarity function to be used by the build.</span></span> <span data-ttu-id="c1e6d-1091">A comparação de precisão favorece a serendipidade, a concorrência favorece a previsibilidade e Jaccard é uma boa combinação entre os dois.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between the two.</span></span> |<span data-ttu-id="c1e6d-1092">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1092">String</span></span> |<span data-ttu-id="c1e6d-1093">cooccurrence, lift, jaccard (lift)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1093">cooccurrence, lift, jaccard (lift)</span></span> |

### <a name="112-trigger-a-recommendation-build"></a><span data-ttu-id="c1e6d-1094">11.2.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1094">11.2.</span></span> <span data-ttu-id="c1e6d-1095">Disparar uma Compilação de Recomendação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1095">Trigger a Recommendation Build</span></span>
  <span data-ttu-id="c1e6d-1096">Por padrão, essa API vai disparar uma compilação de modelo de recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1096">By default this API will trigger a recommendation model build.</span></span> <span data-ttu-id="c1e6d-1097">Para disparar uma compilação de classificação (para classificar recursos), a variante da API de compilação com o parâmetro de tipo de compilação deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1097">To trigger a rank build (in order to score  features), the build API variant with build type parameter should be used.</span></span>

| <span data-ttu-id="c1e6d-1098">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1098">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1099">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1099">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1100">POST</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1100">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1101">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1101">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| <span data-ttu-id="c1e6d-1102">HEADER</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1102">HEADER</span></span> |<span data-ttu-id="c1e6d-1103">`"Content-Type", "text/xml"` (Se estiver enviando o Corpo da solicitação)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="c1e6d-1104">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1104">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1105">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1105">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1106">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1106">modelId</span></span> |<span data-ttu-id="c1e6d-1107">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1107">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-1108">userDescription</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1108">userDescription</span></span> |<span data-ttu-id="c1e6d-1109">Identificador textual do catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1109">Textual identifier of the catalog.</span></span> <span data-ttu-id="c1e6d-1110">Observe que se você usar espaços você deve codificá-los com 20%.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1110">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="c1e6d-1111">Consulte o exemplo acima.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1111">See example above.</span></span><br><span data-ttu-id="c1e6d-1112">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1112">Max length: 50</span></span> |
| <span data-ttu-id="c1e6d-1113">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1113">apiVersion</span></span> |<span data-ttu-id="c1e6d-1114">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1114">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-1115">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1115">Request Body</span></span> |<span data-ttu-id="c1e6d-1116">Se for deixado em branco, o build será executado com os parâmetros de build padrão.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1116">If left empty then the build will be executed with the default build parameters.</span></span><br><br><span data-ttu-id="c1e6d-1117">Se você quiser definir os parâmetros de build, envie-os como XML no corpo, como mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1117">If you want to set the build parameters, send the parameters as XML into the body as in the following sample.</span></span> <span data-ttu-id="c1e6d-1118">(Veja a seção "Parâmetros de build" para obter uma explicação dos parâmetros.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1118">(See the "Build parameters" section for an explanation of the parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span></span> |

<span data-ttu-id="c1e6d-1119">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1119">**Response**:</span></span>

<span data-ttu-id="c1e6d-1120">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1120">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-1121">Esta é uma API assíncrona.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1121">This is an asynchronous API.</span></span> <span data-ttu-id="c1e6d-1122">Você receberá uma ID de compilação como uma resposta.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1122">You will get a build ID as a response.</span></span> <span data-ttu-id="c1e6d-1123">Para saber quando a compilação foi concluída, você deve chamar a API "Obter Status de Compilações de um Modelo" e localizar a ID desta compilação na resposta.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1123">To know when the build has ended, you should call the “Get Builds Status of a Model” API and locate this build ID in the response.</span></span> <span data-ttu-id="c1e6d-1124">Observe que uma compilação pode levar de minutos a horas dependendo do tamanho dos dados.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1124">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="c1e6d-1125">Você não pode consumir recomendações até a compilação terminar.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1125">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="c1e6d-1126">Status de compilação válidos:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1126">Valid build status:</span></span>

* <span data-ttu-id="c1e6d-1127">Criar - A solicitação de compilação foi criada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1127">Create - Build request was created.</span></span>
* <span data-ttu-id="c1e6d-1128">Em fila - A solicitação de compilação foi enviada e será enfileirada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1128">Queued - Build request was sent and it is queued.</span></span>
* <span data-ttu-id="c1e6d-1129">Compilando - A compilação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1129">Building - Build is in progress.</span></span>
* <span data-ttu-id="c1e6d-1130">Sucesso - A compilação concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1130">Success - Build ended successfully.</span></span>
* <span data-ttu-id="c1e6d-1131">Erro - A compilação foi concluída com uma falha.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1131">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="c1e6d-1132">Cancelado - A compilação foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1132">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="c1e6d-1133">Cancelando - Uma solicitação de cancelamento para a compilação foi enviada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1133">Cancelling - A cancel request for the build was sent.</span></span>

<span data-ttu-id="c1e6d-1134">Observe que a ID de compilação pode ser encontrada no seguinte caminho: `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1134">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="c1e6d-1135">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1135">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a><span data-ttu-id="c1e6d-1136">11.3.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1136">11.3.</span></span> <span data-ttu-id="c1e6d-1137">Disparar Compilação (Recomendação, Classificação ou FBT)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1137">Trigger Build (Recommendation, Rank or FBT)</span></span>
| <span data-ttu-id="c1e6d-1138">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1138">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1139">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1139">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1140">POST</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1140">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1141">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1141">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| <span data-ttu-id="c1e6d-1142">HEADER</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1142">HEADER</span></span> |<span data-ttu-id="c1e6d-1143">`"Content-Type", "text/xml"` (Se estiver enviando o Corpo da solicitação)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="c1e6d-1144">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1144">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1145">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1145">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1146">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1146">modelId</span></span> |<span data-ttu-id="c1e6d-1147">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1147">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-1148">userDescription</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1148">userDescription</span></span> |<span data-ttu-id="c1e6d-1149">Identificador textual do catálogo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1149">Textual identifier of the catalog.</span></span> <span data-ttu-id="c1e6d-1150">Observe que se você usar espaços você deve codificá-los com 20%.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1150">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="c1e6d-1151">Consulte o exemplo acima.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1151">See example above.</span></span><br><span data-ttu-id="c1e6d-1152">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1152">Max length: 50</span></span> |
| <span data-ttu-id="c1e6d-1153">buildType</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1153">buildType</span></span> |<span data-ttu-id="c1e6d-1154">Tipo de compilação para invocar: </span><span class="sxs-lookup"><span data-stu-id="c1e6d-1154">Type of the build to invoke:</span></span> <br/> <span data-ttu-id="c1e6d-1155">-.'Recomendação' compilação de recomendação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1155">- 'Recommendation' for recommendation build</span></span> <br> <span data-ttu-id="c1e6d-1156">- 'Classificação' para compilação de classificação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1156">- 'Ranking' for rank build</span></span> <br/> <span data-ttu-id="c1e6d-1157">- “Fbt” para compilação FBT</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1157">- 'Fbt' for FBT build</span></span> |
| <span data-ttu-id="c1e6d-1158">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1158">apiVersion</span></span> |<span data-ttu-id="c1e6d-1159">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1159">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-1160">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1160">Request Body</span></span> |<span data-ttu-id="c1e6d-1161">Se for deixado em branco, o build será executado com os parâmetros de build padrão.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1161">If left empty then the build will be executed with the default build parameters.</span></span><br><br><span data-ttu-id="c1e6d-1162">Se você quiser definir os parâmetros de build, envie-os como XML no corpo, como no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1162">If you want to set build parameters, send them as XML into the body like in the following sample.</span></span> <span data-ttu-id="c1e6d-1163">(Veja a seção "Parâmetros de build" para obter uma explicação e a lista completa dos parâmetros.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1163">(See the "Build parameters" section for an explanation and full list of the parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span></span> |

<span data-ttu-id="c1e6d-1164">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1164">**Response**:</span></span>

<span data-ttu-id="c1e6d-1165">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1165">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-1166">Esta é uma API assíncrona.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1166">This is an asynchronous API.</span></span> <span data-ttu-id="c1e6d-1167">Você receberá uma ID de compilação como uma resposta.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1167">You will get a build ID as a response.</span></span> <span data-ttu-id="c1e6d-1168">Para saber quando a compilação foi concluída, você deve chamar a API "Obter Status de Compilações de um Modelo" e localizar a ID desta compilação na resposta.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1168">To know when the build has ended, you should call the “Get Builds Status of a Model” API and locate this build ID in the response.</span></span> <span data-ttu-id="c1e6d-1169">Observe que uma compilação pode levar de minutos a horas dependendo do tamanho dos dados.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1169">Note that a build can take from minutes to hours depending on the size of the data.</span></span>

<span data-ttu-id="c1e6d-1170">Você não pode consumir recomendações até a compilação terminar.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1170">You cannot consume recommendations till the build ends.</span></span>

<span data-ttu-id="c1e6d-1171">Status de compilação válidos:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1171">Valid build status:</span></span>

* <span data-ttu-id="c1e6d-1172">Criado - O modelo foi criado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1172">Create - Model was created.</span></span>
* <span data-ttu-id="c1e6d-1173">Na fila - A compilação do modelo foi disparada e está na fila.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1173">Queued - Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="c1e6d-1174">Criando - O modelo está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1174">Building - Model is being built.</span></span>
* <span data-ttu-id="c1e6d-1175">Sucesso - A compilação concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1175">Success - Build ended successfully.</span></span>
* <span data-ttu-id="c1e6d-1176">Erro - A compilação foi concluída com uma falha.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1176">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="c1e6d-1177">Cancelado - A compilação foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1177">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="c1e6d-1178">Cancelando - A compilação está sendo cancelada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1178">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="c1e6d-1179">Observe que a ID de compilação pode ser encontrada no seguinte caminho: `Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1179">Note that the build ID can be found under the following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="c1e6d-1180">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1180">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Build a Model with RequestBody</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T08:56:34Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">BuildAModelEntity2</title>
    <updated>2014-10-05T08:56:34Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/BuildModel?modelId='9559872f-7a53-4076-a3c7-19d9385c1265'&amp;userDescription='First%20build'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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




### <a name="114-get-builds-status-of-a-model"></a><span data-ttu-id="c1e6d-1181">11.4.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1181">11.4.</span></span> <span data-ttu-id="c1e6d-1182">Obter status da compilação de um modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1182">Get Builds Status of a Model</span></span>
<span data-ttu-id="c1e6d-1183">Recupera compilações e seus status para um modelo específico.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1183">Retrieves builds and their status for a specified model.</span></span>

| <span data-ttu-id="c1e6d-1184">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1184">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1185">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1185">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1186">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1186">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1187">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1187">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-1188">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1188">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1189">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1189">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1190">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1190">modelId</span></span> |<span data-ttu-id="c1e6d-1191">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1191">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-1192">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1192">onlyLastBuild</span></span> |<span data-ttu-id="c1e6d-1193">Indica se é necessário retornar todo o histórico de compilação do modelo ou apenas o status da compilação mais recente</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1193">Indicates whether to return all the build history of the model or only the status of the most recent build</span></span> |
| <span data-ttu-id="c1e6d-1194">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1194">apiVersion</span></span> |<span data-ttu-id="c1e6d-1195">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1195">1.0</span></span> |

<span data-ttu-id="c1e6d-1196">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1196">**Response**:</span></span>

<span data-ttu-id="c1e6d-1197">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1197">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-1198">A resposta inclui uma entrada por compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1198">The response includes one entry per build.</span></span> <span data-ttu-id="c1e6d-1199">Cada entrada tem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1199">Each entry has the following data:</span></span>

* <span data-ttu-id="c1e6d-1200">`feed/entry/content/properties/UserName` Nome do usuário.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1200">`feed/entry/content/properties/UserName` - Name of the user.</span></span>
* <span data-ttu-id="c1e6d-1201">`feed/entry/content/properties/ModelName` - O nome do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1201">`feed/entry/content/properties/ModelName` - Name of the model.</span></span>
* <span data-ttu-id="c1e6d-1202">`feed/entry/content/properties/ModelId` - Identificador exclusivo do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="c1e6d-1203">`feed/entry/content/properties/IsDeployed` - Se a compilação é implantada (conhecido como</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1203">`feed/entry/content/properties/IsDeployed` - Whether the build is deployed (a.k.a.</span></span> <span data-ttu-id="c1e6d-1204">compilação ativa).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1204">active build).</span></span>
* <span data-ttu-id="c1e6d-1205">`feed/entry/content/properties/BuildId` - Identificador exclusivo da compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="c1e6d-1206">`feed/entry/content/properties/BuildType` - Tipo de compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1206">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="c1e6d-1207">`feed/entry/content/properties/Status` - Status da compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1207">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="c1e6d-1208">Este pode ser uma das seguintes opções: Erro, Criando, Na fila, Cancelando, Cancelado e Êxito.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1208">Can be one of the following: Error, Building, Queued, Cancelling, Cancelled, Success.</span></span>
* <span data-ttu-id="c1e6d-1209">`feed/entry/content/properties/StatusMessage` - Mensagem de status detalhada (aplica-se somente a estados específicos).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="c1e6d-1210">`feed/entry/content/properties/Progress` - Andamento da compilação (%).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="c1e6d-1211">`feed/entry/content/properties/StartTime` - Hora de início da compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1211">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="c1e6d-1212">`feed/entry/content/properties/EndTime` - Hora de término da compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1212">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="c1e6d-1213">`feed/entry/content/properties/ExecutionTime` - Duração da compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="c1e6d-1214">`feed/entry/content/properties/ProgressStep` - Detalhes sobre o estágio atual de uma compilação em andamento.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1214">`feed/entry/content/properties/ProgressStep` - Details about the current stage of a build in progress.</span></span>

<span data-ttu-id="c1e6d-1215">Status de compilação válidos:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1215">Valid build status:</span></span>

* <span data-ttu-id="c1e6d-1216">Criada - a entrada da solicitação de compilação foi criada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1216">Created - Build request entry was created.</span></span>
* <span data-ttu-id="c1e6d-1217">Em fila - a solicitação de build foi disparada e está na fila.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1217">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="c1e6d-1218">Compilando - a build está em andamento.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1218">Building - Build is in process.</span></span>
* <span data-ttu-id="c1e6d-1219">Sucesso - A compilação concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1219">Success - Build ended successfully.</span></span>
* <span data-ttu-id="c1e6d-1220">Erro - A compilação foi concluída com uma falha.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1220">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="c1e6d-1221">Cancelado - A compilação foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1221">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="c1e6d-1222">Cancelando - A compilação está sendo cancelada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1222">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="c1e6d-1223">Valores válidos para o tipo de compilação:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1223">Valid values for build type:</span></span>

* <span data-ttu-id="c1e6d-1224">Classificação - compilação de classificação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1224">Rank - Rank build.</span></span>
* <span data-ttu-id="c1e6d-1225">Recomendação - compilação de recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1225">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="c1e6d-1226">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1226">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a model</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T17:51:10Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T17:51:10Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelBuildsStatus?modelId='1d20c34f-dca1-4eac-8e5d-f299e4e4ad66'&amp;onlyLastBuild=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="115-get-builds-status"></a><span data-ttu-id="c1e6d-1227">11.5.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1227">11.5.</span></span> <span data-ttu-id="c1e6d-1228">Obter Status da Compilação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1228">Get Builds Status</span></span>
<span data-ttu-id="c1e6d-1229">Recupera os status da compilação de todos os modelos de um usuário</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1229">Retrieves build statuses of all models of a user.</span></span>

| <span data-ttu-id="c1e6d-1230">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1230">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1231">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1231">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1232">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1232">GET</span></span> |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1233">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1233">Example:</span></span><br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-1234">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1234">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1235">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1235">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1236">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1236">onlyLastBuild</span></span> |<span data-ttu-id="c1e6d-1237">Indica se é necessário retornar todo o histórico de compilação do modelo ou apenas o status da compilação mais recente.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1237">Indicates whether to return all the build history of the model or only the status of the most recent build.</span></span> |
| <span data-ttu-id="c1e6d-1238">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1238">apiVersion</span></span> |<span data-ttu-id="c1e6d-1239">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1239">1.0</span></span> |

<span data-ttu-id="c1e6d-1240">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1240">**Response**:</span></span>

<span data-ttu-id="c1e6d-1241">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1241">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-1242">A resposta inclui uma entrada por compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1242">The response includes one entry per build.</span></span> <span data-ttu-id="c1e6d-1243">Cada entrada tem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1243">Each entry has the following data:</span></span>

* <span data-ttu-id="c1e6d-1244">`feed/entry/content/properties/UserName` Nome do usuário.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1244">`feed/entry/content/properties/UserName` - Name of the user.</span></span>
* <span data-ttu-id="c1e6d-1245">`feed/entry/content/properties/ModelName` - O nome do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1245">`feed/entry/content/properties/ModelName` - Name of the model.</span></span>
* <span data-ttu-id="c1e6d-1246">`feed/entry/content/properties/ModelId` - Identificador exclusivo do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="c1e6d-1247">`feed/entry/content/properties/IsDeployed` - Se a compilação é implantada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1247">`feed/entry/content/properties/IsDeployed` - Whether the build is deployed.</span></span>
* <span data-ttu-id="c1e6d-1248">`feed/entry/content/properties/BuildId` - Identificador exclusivo da compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="c1e6d-1249">`feed/entry/content/properties/BuildType` - Tipo de compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1249">`feed/entry/content/properties/BuildType` - Type of the build.</span></span>
* <span data-ttu-id="c1e6d-1250">`feed/entry/content/properties/Status` - Status da compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1250">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="c1e6d-1251">Este pode ser uma das seguintes opções: Erro, Criando, Na fila, Cancelado, Cancelando e Êxito.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1251">Can be one of the following: Error, Building, Queued, Cancelled, Cancelling, Success.</span></span>
* <span data-ttu-id="c1e6d-1252">`feed/entry/content/properties/StatusMessage` - Mensagem de status detalhada (aplica-se somente a estados específicos).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only to specific states).</span></span>
* <span data-ttu-id="c1e6d-1253">`feed/entry/content/properties/Progress` - Andamento da compilação (%).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="c1e6d-1254">`feed/entry/content/properties/StartTime` - Hora de início da compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1254">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="c1e6d-1255">`feed/entry/content/properties/EndTime` - Hora de término da compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1255">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="c1e6d-1256">`feed/entry/content/properties/ExecutionTime` - Duração da compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="c1e6d-1257">`feed/entry/content/properties/ProgressStep` - Detalhes sobre o estágio atual de uma compilação em andamento.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1257">`feed/entry/content/properties/ProgressStep` - Details about the current stage of a build in progress.</span></span>

<span data-ttu-id="c1e6d-1258">Status de compilação válidos:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1258">Valid build status:</span></span>

* <span data-ttu-id="c1e6d-1259">Criada - a entrada da solicitação de compilação foi criada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1259">Created - Build request entry was created.</span></span>
* <span data-ttu-id="c1e6d-1260">Em fila - a solicitação de build foi disparada e está na fila.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1260">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="c1e6d-1261">Compilando - a build está em andamento.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1261">Building - Build is in process.</span></span>
* <span data-ttu-id="c1e6d-1262">Sucesso - A compilação concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1262">Success - Build ended successfully.</span></span>
* <span data-ttu-id="c1e6d-1263">Erro - A compilação foi concluída com uma falha.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1263">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="c1e6d-1264">Cancelado - A compilação foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1264">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="c1e6d-1265">Cancelando - A compilação está sendo cancelada.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1265">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="c1e6d-1266">Valores válidos para o tipo de compilação:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1266">Valid values for build type:</span></span>

* <span data-ttu-id="c1e6d-1267">Classificação - compilação de classificação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1267">Rank - Rank build.</span></span>
* <span data-ttu-id="c1e6d-1268">Recomendação - compilação de recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1268">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="c1e6d-1269">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1269">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get builds status of a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-05T18:41:21Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildsStatusEntity</title>
            <updated>2014-11-05T18:41:21Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserBuildsStatus?onlyLastBuilds=False&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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


### <a name="116-delete-build"></a><span data-ttu-id="c1e6d-1270">11.6.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1270">11.6.</span></span> <span data-ttu-id="c1e6d-1271">Excluir compilação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1271">Delete Build</span></span>
<span data-ttu-id="c1e6d-1272">Exclui uma compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1272">Deletes a build.</span></span>

<span data-ttu-id="c1e6d-1273">OBSERVAÇÃO: </span><span class="sxs-lookup"><span data-stu-id="c1e6d-1273">NOTE:</span></span> <br><span data-ttu-id="c1e6d-1274">Não é possível excluir uma compilação ativa.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1274">You cannot delete an active build.</span></span> <span data-ttu-id="c1e6d-1275">O modelo deve ser atualizado para um build ativo diferente antes que seja excluído.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1275">The model should be updated to a different active build before you delete it.</span></span><br><span data-ttu-id="c1e6d-1276">Não é possível excluir um build em andamento.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1276">You cannot delete an in-progress build.</span></span> <span data-ttu-id="c1e6d-1277">Você deve cancelar a compilação antes chamando <strong>Cancelar compilação</strong>.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1277">You should cancel the build first by calling <strong>Cancel Build</strong>.</span></span>

| <span data-ttu-id="c1e6d-1278">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1278">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1279">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1279">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1280">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1280">DELETE</span></span> |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1281">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1281">Example:</span></span><br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-1282">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1282">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1283">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1283">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1284">buildId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1284">buildId</span></span> |<span data-ttu-id="c1e6d-1285">Identificador exclusivo da compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1285">Unique identifier of the build.</span></span> |
| <span data-ttu-id="c1e6d-1286">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1286">apiVersion</span></span> |<span data-ttu-id="c1e6d-1287">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1287">1.0</span></span> |

<span data-ttu-id="c1e6d-1288">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1288">**Response:**</span></span>

<span data-ttu-id="c1e6d-1289">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1289">HTTP Status code: 200</span></span>

### <a name="117-cancel-build"></a><span data-ttu-id="c1e6d-1290">11.7.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1290">11.7.</span></span> <span data-ttu-id="c1e6d-1291">Cancelar compilação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1291">Cancel Build</span></span>
<span data-ttu-id="c1e6d-1292">Cancela uma compilação que está no status de compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1292">Cancels a build that is in building status.</span></span>

| <span data-ttu-id="c1e6d-1293">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1293">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1294">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1294">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1295">PUT</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1295">PUT</span></span> |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1296">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1296">Example:</span></span><br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-1297">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1297">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1298">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1298">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1299">buildId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1299">buildId</span></span> |<span data-ttu-id="c1e6d-1300">Identificador exclusivo da compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1300">Unique identifier of the build.</span></span> |
| <span data-ttu-id="c1e6d-1301">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1301">apiVersion</span></span> |<span data-ttu-id="c1e6d-1302">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1302">1.0</span></span> |

<span data-ttu-id="c1e6d-1303">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1303">**Response:**</span></span>

<span data-ttu-id="c1e6d-1304">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1304">HTTP Status code: 200</span></span>

### <a name="118-get-build-parameters"></a><span data-ttu-id="c1e6d-1305">11.8.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1305">11.8.</span></span> <span data-ttu-id="c1e6d-1306">Obter parâmetros de compilação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1306">Get Build Parameters</span></span>
<span data-ttu-id="c1e6d-1307">Recupera parâmetros de compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1307">Retrieves build parameters.</span></span>

| <span data-ttu-id="c1e6d-1308">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1308">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1309">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1309">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1310">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1310">GET</span></span> |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1311">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1311">Example:</span></span><br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-1312">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1312">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1313">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1313">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1314">buildId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1314">buildId</span></span> |<span data-ttu-id="c1e6d-1315">Identificador exclusivo da compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1315">Unique identifier of the build.</span></span> |
| <span data-ttu-id="c1e6d-1316">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1316">apiVersion</span></span> |<span data-ttu-id="c1e6d-1317">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1317">1.0</span></span> |

<span data-ttu-id="c1e6d-1318">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1318">**Response:**</span></span>

<span data-ttu-id="c1e6d-1319">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1319">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-1320">Essa API retorna uma coleção de elementos de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1320">This API returns a collection of key/value elements.</span></span> <span data-ttu-id="c1e6d-1321">Cada elemento representa um parâmetro e seu valor:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1321">Each element represents a parameter and its value:</span></span>

* <span data-ttu-id="c1e6d-1322">`feed/entry/content/properties/Key` - nome do parâmetro de build.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1322">`feed/entry/content/properties/Key` - Build parameter name.</span></span>
* <span data-ttu-id="c1e6d-1323">`feed/entry/content/properties/Value` - valor do parâmetro de build.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1323">`feed/entry/content/properties/Value` - Build parameter value.</span></span>

<span data-ttu-id="c1e6d-1324">A tabela a seguir descreve o valor que cada chave representa.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1324">The table below depicts the value that each key represents.</span></span>

| <span data-ttu-id="c1e6d-1325">Chave</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1325">Key</span></span> | <span data-ttu-id="c1e6d-1326">Descrição</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1326">Description</span></span> | <span data-ttu-id="c1e6d-1327">Tipo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1327">Type</span></span> | <span data-ttu-id="c1e6d-1328">Valor Válido</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1328">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="c1e6d-1329">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1329">NumberOfModelIterations</span></span> |<span data-ttu-id="c1e6d-1330">O número de iterações que o modelo executa é refletido pelo tempo de computação geral e a precisão do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1330">The number of iterations the model performs is reflected by the overall compute time and the model accuracy.</span></span> <span data-ttu-id="c1e6d-1331">Quanto maior o número, maior será a precisão obtida, mas o tempo de computação será mais longo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1331">The higher the number, the better accuracy you will get, but the compute time will take longer.</span></span> |<span data-ttu-id="c1e6d-1332">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1332">Integer</span></span> |<span data-ttu-id="c1e6d-1333">10-50</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1333">10-50</span></span> |
| <span data-ttu-id="c1e6d-1334">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1334">NumberOfModelDimensions</span></span> |<span data-ttu-id="c1e6d-1335">O número de dimensões está relacionado ao número de “recursos” que o modelo tentará localizar em seus dados.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1335">The number of dimensions relates to the number of 'features' the model will try to find within your data.</span></span> <span data-ttu-id="c1e6d-1336">Aumentar o número de dimensões possibilitará um melhor ajuste dos resultados em clusters menores.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1336">Increasing the number of dimensions will allow better fine-tuning of the results into smaller clusters.</span></span> <span data-ttu-id="c1e6d-1337">No entanto, ter muitas dimensões impedirá que o modelo localize correlações entre itens.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1337">However, too many dimensions will prevent the model from finding correlations between items.</span></span> |<span data-ttu-id="c1e6d-1338">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1338">Integer</span></span> |<span data-ttu-id="c1e6d-1339">10-40</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1339">10-40</span></span> |
| <span data-ttu-id="c1e6d-1340">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1340">ItemCutOffLowerBound</span></span> |<span data-ttu-id="c1e6d-1341">Define o limite inferior de item para o condensador.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1341">Defines the item lower bound for the condenser.</span></span> <span data-ttu-id="c1e6d-1342">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1342">See usage condenser above.</span></span> |<span data-ttu-id="c1e6d-1343">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1343">Integer</span></span> |<span data-ttu-id="c1e6d-1344">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1344">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="c1e6d-1345">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1345">ItemCutOffUpperBound</span></span> |<span data-ttu-id="c1e6d-1346">Define o limite superior de item para o condensador.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1346">Defines the item upper bound for the condenser.</span></span> <span data-ttu-id="c1e6d-1347">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1347">See usage condenser above.</span></span> |<span data-ttu-id="c1e6d-1348">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1348">Integer</span></span> |<span data-ttu-id="c1e6d-1349">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1349">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="c1e6d-1350">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1350">UserCutOffLowerBound</span></span> |<span data-ttu-id="c1e6d-1351">Define o limite inferior de usuário para o condensador.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1351">Defines the user lower bound for the condenser.</span></span> <span data-ttu-id="c1e6d-1352">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1352">See usage condenser above.</span></span> |<span data-ttu-id="c1e6d-1353">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1353">Integer</span></span> |<span data-ttu-id="c1e6d-1354">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1354">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="c1e6d-1355">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1355">UserCutOffUpperBound</span></span> |<span data-ttu-id="c1e6d-1356">Define o limite superior de usuário para o condensador.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1356">Defines the user upper bound for the condenser.</span></span> <span data-ttu-id="c1e6d-1357">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1357">See usage condenser above.</span></span> |<span data-ttu-id="c1e6d-1358">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1358">Integer</span></span> |<span data-ttu-id="c1e6d-1359">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1359">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="c1e6d-1360">Descrição</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1360">Description</span></span> |<span data-ttu-id="c1e6d-1361">Descrição da compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1361">Build description.</span></span> |<span data-ttu-id="c1e6d-1362">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1362">String</span></span> |<span data-ttu-id="c1e6d-1363">Qualquer texto, máximo de 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1363">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="c1e6d-1364">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1364">EnableModelingInsights</span></span> |<span data-ttu-id="c1e6d-1365">Permite computar métricas sobre o modelo de recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1365">Allows you to compute metrics on the recommendation model.</span></span> |<span data-ttu-id="c1e6d-1366">Booliano</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1366">Boolean</span></span> |<span data-ttu-id="c1e6d-1367">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1367">True/False</span></span> |
| <span data-ttu-id="c1e6d-1368">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1368">UseFeaturesInModel</span></span> |<span data-ttu-id="c1e6d-1369">Indica se os recursos podem ser usados para aperfeiçoar o modelo de recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1369">Indicates if features can be used in order to enhance the recommendation model.</span></span> |<span data-ttu-id="c1e6d-1370">Booliano</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1370">Boolean</span></span> |<span data-ttu-id="c1e6d-1371">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1371">True/False</span></span> |
| <span data-ttu-id="c1e6d-1372">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1372">ModelingFeatureList</span></span> |<span data-ttu-id="c1e6d-1373">Lista separada por vírgulas de nomes de recursos a serem usados na compilação de recomendação a fim de melhorar as recomendações.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1373">Comma-separated list of feature names to be used in the recommendation build, in order to enhance the recommendation.</span></span> |<span data-ttu-id="c1e6d-1374">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1374">String</span></span> |<span data-ttu-id="c1e6d-1375">Nomes de recursos, até 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1375">Feature names, up to 512 chars</span></span> |
| <span data-ttu-id="c1e6d-1376">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1376">AllowColdItemPlacement</span></span> |<span data-ttu-id="c1e6d-1377">Indica se a recomendação também enviar itens sem interesse através da similaridade de recursos.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1377">Indicates if the recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="c1e6d-1378">Booliano</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1378">Boolean</span></span> |<span data-ttu-id="c1e6d-1379">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1379">True/False</span></span> |
| <span data-ttu-id="c1e6d-1380">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1380">EnableFeatureCorrelation</span></span> |<span data-ttu-id="c1e6d-1381">Indica se os recursos podem ser usados no raciocínio.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1381">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="c1e6d-1382">Booliano</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1382">Boolean</span></span> |<span data-ttu-id="c1e6d-1383">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1383">True/False</span></span> |
| <span data-ttu-id="c1e6d-1384">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1384">ReasoningFeatureList</span></span> |<span data-ttu-id="c1e6d-1385">Lista separada por vírgulas de nomes de recursos a serem usado em frases de raciocínio (isto é, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1385">Comma-separated list of feature names to be used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="c1e6d-1386">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1386">String</span></span> |<span data-ttu-id="c1e6d-1387">Nomes de recursos, até 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1387">Feature names, up to 512 chars</span></span> |

<span data-ttu-id="c1e6d-1388">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1388">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get build parameters</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2015-01-08T13:50:57Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'" />
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UseFeaturesInModel</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">AllowColdItemPlacement</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableFeatureCorrelation</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">EnableModelingInsights</d:Key>
                    <d:Value m:type="Edm.String">False</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelIterations</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
            <titletype="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">NumberOfModelDimensions</d:Key>
                    <d:Value m:type="Edm.String">10</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <linkrel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ItemCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffLowerBound</d:Key>
                    <d:Value m:type="Edm.String">2</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">UserCutOffUpperBound</d:Key>
                    <d:Value m:type="Edm.String">2147483647</d:Value>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=10&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ModelingFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=11&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">ReasoningFeatureList</d:Key>
                    <d:Value m:type="Edm.String"/>
                </m:properties>
            </content>
        </entry>
        <entry>
            <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1</id>
            <title type="text">GetBuildParametersEntity</title>
            <updated>2015-01-08T13:50:57Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetBuildParameters?buildId='1000653'&amp;apiVersion='1.0'&amp;$skip=12&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:Key m:type="Edm.String">Description</d:Key>
                    <d:Value m:type="Edm.String">rankBuild</d:Value>
                </m:properties>
            </content>
        </entry>
    </feed>

## <a name="12-recommendation"></a><span data-ttu-id="c1e6d-1389">12. Recomendações</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1389">12. Recommendation</span></span>
### <a name="121-get-item-recommendations-for-active-build"></a><span data-ttu-id="c1e6d-1390">12.1.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1390">12.1.</span></span> <span data-ttu-id="c1e6d-1391">Obter Recomendações de Item (para compilação ativa)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1391">Get Item Recommendations (for active build)</span></span>
<span data-ttu-id="c1e6d-1392">Obtenha recomendações da compilação ativa do tipo "Recomendação" ou "Fbt" com base em uma lista de itens de propagação (entrada).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1392">Get recommendations of the active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span></span>

| <span data-ttu-id="c1e6d-1393">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1393">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1394">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1394">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1395">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1395">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1396">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1396">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-1397">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1397">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1398">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1398">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1399">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1399">modelId</span></span> |<span data-ttu-id="c1e6d-1400">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1400">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-1401">itemIds</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1401">itemIds</span></span> |<span data-ttu-id="c1e6d-1402">Lista separada por vírgulas dos itens para recomendar.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1402">Comma-separated list of the items to recommend for.</span></span> <br><span data-ttu-id="c1e6d-1403">Se a compilação ativa for do tipo FBT, você poderá enviar somente um item.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1403">If the active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="c1e6d-1404">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1404">Max length: 1024</span></span> |
| <span data-ttu-id="c1e6d-1405">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1405">numberOfResults</span></span> |<span data-ttu-id="c1e6d-1406">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="c1e6d-1406">Number of required results</span></span> <br> <span data-ttu-id="c1e6d-1407">Máx.: 150</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1407">Max: 150</span></span> |
| <span data-ttu-id="c1e6d-1408">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1408">includeMetatadata</span></span> |<span data-ttu-id="c1e6d-1409">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1409">Future use, always false</span></span> |
| <span data-ttu-id="c1e6d-1410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1410">apiVersion</span></span> |<span data-ttu-id="c1e6d-1411">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1411">1.0</span></span> |

<span data-ttu-id="c1e6d-1412">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1412">**Response:**</span></span>

<span data-ttu-id="c1e6d-1413">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1413">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-1414">A resposta inclui uma entrada por item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1414">The response includes one entry per recommended item.</span></span> <span data-ttu-id="c1e6d-1415">Cada entrada tem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1415">Each entry has the following data:</span></span>

* <span data-ttu-id="c1e6d-1416">`Feed\entry\content\properties\Id` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="c1e6d-1417">`Feed\entry\content\properties\Name` - Nome do item.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1417">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="c1e6d-1418">`Feed\entry\content\properties\Rating` - Classificação da recomendação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1418">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="c1e6d-1419">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="c1e6d-1420">A resposta de exemplo a seguir inclui 10 itens recomendados.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1420">The example response below includes 10 recommended items.</span></span>

<span data-ttu-id="c1e6d-1421">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1421">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=3&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=4&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=5&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=6&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=7&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=8&amp;$top=1" />
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
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1</id>
    <title type="text">GetRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=10&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=9&amp;$top=1" />
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

### <a name="122-get-item-recommendations-of-a-specific-build"></a><span data-ttu-id="c1e6d-1422">12.2.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1422">12.2.</span></span> <span data-ttu-id="c1e6d-1423">Obter Recomendações de Item (de uma compilação específica)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1423">Get Item Recommendations (of a specific build)</span></span>
<span data-ttu-id="c1e6d-1424">Obtenha recomendações de uma compilação específica do tipo “Recomendação” ou “Fbt”.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span></span>

| <span data-ttu-id="c1e6d-1425">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1425">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1426">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1426">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1427">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1427">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1428">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1428">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-1429">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1429">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1430">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1430">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1431">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1431">modelId</span></span> |<span data-ttu-id="c1e6d-1432">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1432">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-1433">itemIds</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1433">itemIds</span></span> |<span data-ttu-id="c1e6d-1434">Lista separada por vírgulas dos itens para recomendar.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1434">Comma-separated list of the items to recommend for.</span></span> <br><span data-ttu-id="c1e6d-1435">Se a compilação ativa for do tipo FBT, você poderá enviar somente um item.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1435">If the active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="c1e6d-1436">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1436">Max length: 1024</span></span> |
| <span data-ttu-id="c1e6d-1437">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1437">numberOfResults</span></span> |<span data-ttu-id="c1e6d-1438">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="c1e6d-1438">Number of required results</span></span> <br> <span data-ttu-id="c1e6d-1439">Máx.: 150</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1439">Max: 150</span></span> |
| <span data-ttu-id="c1e6d-1440">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1440">includeMetatadata</span></span> |<span data-ttu-id="c1e6d-1441">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1441">Future use, always false</span></span> |
| <span data-ttu-id="c1e6d-1442">buildId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1442">buildId</span></span> |<span data-ttu-id="c1e6d-1443">a id de compilação a ser usada para esta solicitação de recomendação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1443">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="c1e6d-1444">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1444">apiVersion</span></span> |<span data-ttu-id="c1e6d-1445">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1445">1.0</span></span> |

<span data-ttu-id="c1e6d-1446">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1446">**Response:**</span></span>

<span data-ttu-id="c1e6d-1447">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1447">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-1448">A resposta inclui uma entrada por item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1448">The response includes one entry per recommended item.</span></span> <span data-ttu-id="c1e6d-1449">Cada entrada tem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1449">Each entry has the following data:</span></span>

* <span data-ttu-id="c1e6d-1450">`Feed\entry\content\properties\Id` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="c1e6d-1451">`Feed\entry\content\properties\Name` - Nome do item.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1451">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="c1e6d-1452">`Feed\entry\content\properties\Rating` - Classificação da recomendação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1452">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="c1e6d-1453">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="c1e6d-1454">Veja um exemplo de resposta no 12.1</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1454">See a response example in 12.1</span></span>

### <a name="123-get-fbt-recommendations-for-active-build"></a><span data-ttu-id="c1e6d-1455">12.3.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1455">12.3.</span></span> <span data-ttu-id="c1e6d-1456">Obter Recomendações de FBT (para compilação ativa)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1456">Get FBT Recommendations (for active build)</span></span>
<span data-ttu-id="c1e6d-1457">Obtenha recomendações da compilação ativa do tipo "Fbt" com base em um item de semente (entrada).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1457">Get recommendations of the active build of type "Fbt" based on a seed (input) item.</span></span>

| <span data-ttu-id="c1e6d-1458">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1458">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1459">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1459">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1460">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1460">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1461">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1461">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-1462">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1462">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1463">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1463">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1464">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1464">modelId</span></span> |<span data-ttu-id="c1e6d-1465">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1465">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-1466">itemId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1466">itemId</span></span> |<span data-ttu-id="c1e6d-1467">Item a ser recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1467">Item to recommend for.</span></span> <br><span data-ttu-id="c1e6d-1468">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1468">Max length: 1024</span></span> |
| <span data-ttu-id="c1e6d-1469">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1469">numberOfResults</span></span> |<span data-ttu-id="c1e6d-1470">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="c1e6d-1470">Number of required results</span></span> <br><span data-ttu-id="c1e6d-1471">Máx.: 150</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1471">Max: 150</span></span> |
| <span data-ttu-id="c1e6d-1472">minimalScore</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1472">minimalScore</span></span> |<span data-ttu-id="c1e6d-1473">Pontuação mínima que um conjunto frequente deve ter para ser incluído nos resultados retornados</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1473">Minimal score that a frequent set should have in order to be included in the returned results</span></span> |
| <span data-ttu-id="c1e6d-1474">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1474">includeMetatadata</span></span> |<span data-ttu-id="c1e6d-1475">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1475">Future use, always false</span></span> |
| <span data-ttu-id="c1e6d-1476">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1476">apiVersion</span></span> |<span data-ttu-id="c1e6d-1477">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1477">1.0</span></span> |

<span data-ttu-id="c1e6d-1478">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1478">**Response:**</span></span>

<span data-ttu-id="c1e6d-1479">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1479">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-1480">A resposta inclui uma entrada por conjunto de item recomendado (um conjunto de itens que são geralmente comprados junto com o item de semente/entrada).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1480">The response includes one entry per recommended item set (a set of items which are usually bought together with the seed/input item).</span></span> <span data-ttu-id="c1e6d-1481">Cada entrada tem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1481">Each entry has the following data:</span></span>

* <span data-ttu-id="c1e6d-1482">`Feed\entry\content\properties\Id1` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="c1e6d-1483">`Feed\entry\content\properties\Name1` - Nome do item.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1483">`Feed\entry\content\properties\Name1` - Name of the item.</span></span>
* <span data-ttu-id="c1e6d-1484">`Feed\entry\content\properties\Id2` - ID do segundo item recomendado (opcional).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="c1e6d-1485">`Feed\entry\content\properties\Name2` - nome do segundo item (opcional).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1485">`Feed\entry\content\properties\Name2` - Name of the 2nd item (optional).</span></span>
* <span data-ttu-id="c1e6d-1486">`Feed\entry\content\properties\Rating` - Classificação da recomendação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1486">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="c1e6d-1487">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="c1e6d-1488">A resposta de exemplo a seguir inclui 3 conjuntos de itens recomendados.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1488">The example response below includes 3 recommended item sets.</span></span>

<span data-ttu-id="c1e6d-1489">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1489">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
      <title type="text" />
      <subtitle type="text">Get Recommendation</subtitle>
      <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemId='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'</id>
      <rights type="text" />
      <updated>2014-10-05T12:28:48Z</updated>
      <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'" />
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">159</d:Id1>
        <d:Name1 m:type="Edm.String">159</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.543343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '159'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=1&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">52</d:Id1>
        <d:Name1 m:type="Edm.String">52</d:Name1>
        <d:Id2 m:type="Edm.String"></d:Id2>
        <d:Name2 m:type="Edm.String"></d:Name2>
        <d:Rating m:type="Edm.Double">0.533343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '52'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
      <entry>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1</id>
    <title type="text">GetFbtRecommendationEntity</title>
    <updated>2014-10-05T12:28:48Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/ItemFbtRecommend?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;itemIds='1003'&amp;numberOfResults=3&amp;minimalScore=0.1&amp;includeMetadata=false&amp;apiVersion='1.0'&amp;$skip=2&amp;$top=1" />
    <content type="application/xml">
      <m:properties>
        <d:Id1 m:type="Edm.String">35</d:Id1>
        <d:Name1 m:type="Edm.String">35</d:Name1>
        <d:Id2 m:type="Edm.String">102</d:Id2>
        <d:Name2 m:type="Edm.String">102</d:Name2>
        <d:Rating m:type="Edm.Double">0.523343480387708</d:Rating>
        <d:Reasoning m:type="Edm.String">People who bought '1003' also bought '35' and '102'</d:Reasoning>
      </m:properties>
    </content>
      </entry>
    </feed>

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a><span data-ttu-id="c1e6d-1490">12.4.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1490">12.4.</span></span> <span data-ttu-id="c1e6d-1491">Obter Recomendações FBT (de uma compilação específica)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1491">Get FBT Recommendations (of a specific build)</span></span>
<span data-ttu-id="c1e6d-1492">Obtenha recomendações de uma compilação específica do tipo "Fbt".</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1492">Get recommendations of a specific build of type "Fbt".</span></span>

| <span data-ttu-id="c1e6d-1493">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1493">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1494">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1495">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1495">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1496">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1496">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-1497">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1497">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1498">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1499">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1499">modelId</span></span> |<span data-ttu-id="c1e6d-1500">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1500">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-1501">itemId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1501">itemId</span></span> |<span data-ttu-id="c1e6d-1502">Item a ser recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1502">Item to recommend for.</span></span> <br><span data-ttu-id="c1e6d-1503">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1503">Max length: 1024</span></span> |
| <span data-ttu-id="c1e6d-1504">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1504">numberOfResults</span></span> |<span data-ttu-id="c1e6d-1505">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="c1e6d-1505">Number of required results</span></span> <br><span data-ttu-id="c1e6d-1506">Máx.: 150</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1506">Max: 150</span></span> |
| <span data-ttu-id="c1e6d-1507">minimalScore</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1507">minimalScore</span></span> |<span data-ttu-id="c1e6d-1508">Pontuação mínima que um conjunto frequente deve ter para ser incluído nos resultados retornados</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1508">Minimal score that a frequent set should have in order to be included in the returned results</span></span> |
| <span data-ttu-id="c1e6d-1509">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1509">includeMetatadata</span></span> |<span data-ttu-id="c1e6d-1510">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1510">Future use, always false</span></span> |
| <span data-ttu-id="c1e6d-1511">buildId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1511">buildId</span></span> |<span data-ttu-id="c1e6d-1512">a id de compilação a ser usada para esta solicitação de recomendação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1512">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="c1e6d-1513">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1513">apiVersion</span></span> |<span data-ttu-id="c1e6d-1514">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1514">1.0</span></span> |

<span data-ttu-id="c1e6d-1515">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1515">**Response:**</span></span>

<span data-ttu-id="c1e6d-1516">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1516">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-1517">A resposta inclui uma entrada por conjunto de item recomendado (um conjunto de itens que são geralmente comprados junto com o item de semente/entrada).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1517">The response includes one entry per recommended item set (a set of items which are usually bought together with the seed/input item).</span></span> <span data-ttu-id="c1e6d-1518">Cada entrada tem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1518">Each entry has the following data:</span></span>

* <span data-ttu-id="c1e6d-1519">`Feed\entry\content\properties\Id1` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="c1e6d-1520">`Feed\entry\content\properties\Name1` - Nome do item.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1520">`Feed\entry\content\properties\Name1` - Name of the item.</span></span>
* <span data-ttu-id="c1e6d-1521">`Feed\entry\content\properties\Id2` - ID do segundo item recomendado (opcional).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="c1e6d-1522">`Feed\entry\content\properties\Name2` - nome do segundo item (opcional).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1522">`Feed\entry\content\properties\Name2` - Name of the 2nd item (optional).</span></span>
* <span data-ttu-id="c1e6d-1523">`Feed\entry\content\properties\Rating` - Classificação da recomendação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1523">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="c1e6d-1524">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="c1e6d-1525">Veja um exemplo de resposta no 12.3</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1525">See a response example in 12.3</span></span>

### <a name="125-get-user-recommendations-for-active-build"></a><span data-ttu-id="c1e6d-1526">12.5.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1526">12.5.</span></span> <span data-ttu-id="c1e6d-1527">Obter Recomendações do Usuário (para compilação ativa)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1527">Get User Recommendations (for active build)</span></span>
<span data-ttu-id="c1e6d-1528">Obtenha recomendações de usuário de uma compilação do tipo "Recomendação" marcada como compilação ativa.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span></span>

<span data-ttu-id="c1e6d-1529">A API retornará uma lista de itens prevista de acordo com o histórico de uso do usuário.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1529">The API will return a list of predicted item according to the usage history of the user.</span></span>

<span data-ttu-id="c1e6d-1530">Observações:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1530">Notes:</span></span> 

1. <span data-ttu-id="c1e6d-1531">Não há nenhuma recomendação de usuário para a compilação FBT.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1531">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="c1e6d-1532">Se a compilação ativa for FBT, esse método retornará um erro.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1532">If the active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="c1e6d-1533">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1533">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1534">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1534">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1535">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1535">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1536">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1536">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-1537">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1537">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1538">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1538">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1539">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1539">modelId</span></span> |<span data-ttu-id="c1e6d-1540">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1540">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-1541">coluna</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1541">userId</span></span> |<span data-ttu-id="c1e6d-1542">Identificador exclusivo do usuário</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1542">Unique identifier of the user</span></span> |
| <span data-ttu-id="c1e6d-1543">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1543">numberOfResults</span></span> |<span data-ttu-id="c1e6d-1544">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="c1e6d-1544">Number of required results</span></span> |
| <span data-ttu-id="c1e6d-1545">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1545">includeMetatadata</span></span> |<span data-ttu-id="c1e6d-1546">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1546">Future use, always false</span></span> |
| <span data-ttu-id="c1e6d-1547">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1547">apiVersion</span></span> |<span data-ttu-id="c1e6d-1548">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1548">1.0</span></span> |

<span data-ttu-id="c1e6d-1549">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1549">**Response:**</span></span>

<span data-ttu-id="c1e6d-1550">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1550">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-1551">A resposta inclui uma entrada por item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1551">The response includes one entry per recommended item.</span></span> <span data-ttu-id="c1e6d-1552">Cada entrada tem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1552">Each entry has the following data:</span></span>

* <span data-ttu-id="c1e6d-1553">`Feed\entry\content\properties\Id` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="c1e6d-1554">`Feed\entry\content\properties\Name` - Nome do item.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1554">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="c1e6d-1555">`Feed\entry\content\properties\Rating` - Classificação da recomendação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1555">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="c1e6d-1556">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="c1e6d-1557">Veja um exemplo de resposta no 12.1</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1557">See a response example in 12.1</span></span>

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a><span data-ttu-id="c1e6d-1558">12.6.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1558">12.6.</span></span> <span data-ttu-id="c1e6d-1559">Obter recomendações de usuário com a lista de itens (para compilação ativa)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1559">Get User Recommendations with item list (for active build)</span></span>
<span data-ttu-id="c1e6d-1560">Obtenha recomendações de usuário de uma compilação do tipo "Recomendação" marcada como compilação ativa com uma lista de itens adicionais</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span></span>

<span data-ttu-id="c1e6d-1561">A API retornará uma lista de itens previstos de acordo com o histórico de uso do usuário e os outros itens fornecidos.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1561">The API will return a list of predicted item according to the usage history of the user and the additional provided items.</span></span>

<span data-ttu-id="c1e6d-1562">Observações:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1562">Notes:</span></span> 

1. <span data-ttu-id="c1e6d-1563">Não há nenhuma recomendação de usuário para a compilação FBT.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1563">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="c1e6d-1564">Se a compilação ativa for FBT, esse método retornará um erro.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1564">If the active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="c1e6d-1565">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1565">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1566">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1566">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1567">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1567">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1568">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1568">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-1569">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1569">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1570">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1570">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1571">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1571">modelId</span></span> |<span data-ttu-id="c1e6d-1572">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1572">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-1573">coluna</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1573">userId</span></span> |<span data-ttu-id="c1e6d-1574">Identificador exclusivo do usuário</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1574">Unique identifier of the user</span></span> |
| <span data-ttu-id="c1e6d-1575">itemsIds</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1575">itemsIds</span></span> |<span data-ttu-id="c1e6d-1576">Lista separada por vírgulas dos itens para recomendar.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1576">Comma-separated list of the items to recommend for.</span></span> <span data-ttu-id="c1e6d-1577">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1577">Max length: 1024</span></span> |
| <span data-ttu-id="c1e6d-1578">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1578">numberOfResults</span></span> |<span data-ttu-id="c1e6d-1579">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="c1e6d-1579">Number of required results</span></span> |
| <span data-ttu-id="c1e6d-1580">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1580">includeMetatadata</span></span> |<span data-ttu-id="c1e6d-1581">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1581">Future use, always false</span></span> |
| <span data-ttu-id="c1e6d-1582">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1582">apiVersion</span></span> |<span data-ttu-id="c1e6d-1583">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1583">1.0</span></span> |

<span data-ttu-id="c1e6d-1584">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1584">**Response:**</span></span>

<span data-ttu-id="c1e6d-1585">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1585">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-1586">A resposta inclui uma entrada por item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1586">The response includes one entry per recommended item.</span></span> <span data-ttu-id="c1e6d-1587">Cada entrada tem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1587">Each entry has the following data:</span></span>

* <span data-ttu-id="c1e6d-1588">`Feed\entry\content\properties\Id` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="c1e6d-1589">`Feed\entry\content\properties\Name` - Nome do item.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1589">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="c1e6d-1590">`Feed\entry\content\properties\Rating` - Classificação da recomendação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1590">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="c1e6d-1591">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="c1e6d-1592">Veja um exemplo de resposta no 12.1</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1592">See a response example in 12.1</span></span>

### <a name="127-get-user-recommendations--of-a-specific-build"></a><span data-ttu-id="c1e6d-1593">12.7.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1593">12.7.</span></span> <span data-ttu-id="c1e6d-1594">Obter Recomendações de Usuário (de uma compilação específica)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1594">Get User Recommendations  (of a specific build)</span></span>
<span data-ttu-id="c1e6d-1595">Obtenha recomendações de usuário de uma compilação específica do tipo "Recomendação".</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1595">Get user recommendations of a specific build of type "Recommendation".</span></span>

<span data-ttu-id="c1e6d-1596">A API retornará uma lista de itens previstos de acordo com o histórico de uso do usuário (usado na compilação específica).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1596">The API will return a list of predicted item according to the usage history of the user (used in the specific build).</span></span>

<span data-ttu-id="c1e6d-1597">Observação: Não há nenhuma recomendação de usuário para a compilação FBT.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1597">Note: There is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="c1e6d-1598">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1598">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1599">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1599">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1600">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1600">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1601">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1601">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-1602">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1602">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1603">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1603">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1604">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1604">modelId</span></span> |<span data-ttu-id="c1e6d-1605">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1605">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-1606">coluna</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1606">userId</span></span> |<span data-ttu-id="c1e6d-1607">Identificador exclusivo do usuário</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1607">Unique identifier of the user</span></span> |
| <span data-ttu-id="c1e6d-1608">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1608">numberOfResults</span></span> |<span data-ttu-id="c1e6d-1609">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="c1e6d-1609">Number of required results</span></span> |
| <span data-ttu-id="c1e6d-1610">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1610">includeMetatadata</span></span> |<span data-ttu-id="c1e6d-1611">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1611">Future use, always false</span></span> |
| <span data-ttu-id="c1e6d-1612">buildId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1612">buildId</span></span> |<span data-ttu-id="c1e6d-1613">a id de compilação a ser usada para esta solicitação de recomendação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1613">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="c1e6d-1614">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1614">apiVersion</span></span> |<span data-ttu-id="c1e6d-1615">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1615">1.0</span></span> |

<span data-ttu-id="c1e6d-1616">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1616">**Response:**</span></span>

<span data-ttu-id="c1e6d-1617">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1617">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-1618">A resposta inclui uma entrada por item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1618">The response includes one entry per recommended item.</span></span> <span data-ttu-id="c1e6d-1619">Cada entrada tem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1619">Each entry has the following data:</span></span>

* <span data-ttu-id="c1e6d-1620">`Feed\entry\content\properties\Id` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="c1e6d-1621">`Feed\entry\content\properties\Name` - Nome do item.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1621">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="c1e6d-1622">`Feed\entry\content\properties\Rating` - Classificação da recomendação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1622">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="c1e6d-1623">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="c1e6d-1624">Veja um exemplo de resposta no 12.1</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1624">See a response example in 12.1</span></span>

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a><span data-ttu-id="c1e6d-1625">12.8.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1625">12.8.</span></span> <span data-ttu-id="c1e6d-1626">Obtenha Recomendações de Usuário com a lista de itens (de uma compilação específica)</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1626">Get User Recommendations with item list (of a specific build)</span></span>
<span data-ttu-id="c1e6d-1627">Obtenha recomendações de usuário de uma compilação específica do tipo "Recomendação" e a lista de itens adicionais.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1627">Get user recommendations of a specific build of type "Recommendation" and the list of additional items.</span></span>

<span data-ttu-id="c1e6d-1628">A API retornará uma lista de itens previstos de acordo com o histórico de uso do usuário e os outros itens da lista.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1628">The API will return a list of predicted item according to the usage history of the user and the additional list of items.</span></span>

<span data-ttu-id="c1e6d-1629">Observação: Não há nenhuma recomendação de usuário para a compilação FBT.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1629">Note: Tthere is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="c1e6d-1630">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1630">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1631">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1631">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1632">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1632">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1633">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1633">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-1634">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1634">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1635">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1635">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1636">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1636">modelId</span></span> |<span data-ttu-id="c1e6d-1637">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1637">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-1638">coluna</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1638">userId</span></span> |<span data-ttu-id="c1e6d-1639">Identificador exclusivo do usuário</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1639">Unique identifier of the user</span></span> |
| <span data-ttu-id="c1e6d-1640">itemIds</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1640">itemIds</span></span> |<span data-ttu-id="c1e6d-1641">Lista separada por vírgulas dos itens para recomendar.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1641">Comma-separated list of the items to recommend for.</span></span> <span data-ttu-id="c1e6d-1642">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1642">Max length: 1024</span></span> |
| <span data-ttu-id="c1e6d-1643">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1643">numberOfResults</span></span> |<span data-ttu-id="c1e6d-1644">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="c1e6d-1644">Number of required results</span></span> |
| <span data-ttu-id="c1e6d-1645">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1645">includeMetatadata</span></span> |<span data-ttu-id="c1e6d-1646">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1646">Future use, always false</span></span> |
| <span data-ttu-id="c1e6d-1647">buildId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1647">buildId</span></span> |<span data-ttu-id="c1e6d-1648">a id de compilação a ser usada para esta solicitação de recomendação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1648">the build id to use for this recommendation request</span></span> |
| <span data-ttu-id="c1e6d-1649">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1649">apiVersion</span></span> |<span data-ttu-id="c1e6d-1650">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1650">1.0</span></span> |

<span data-ttu-id="c1e6d-1651">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1651">**Response:**</span></span>

<span data-ttu-id="c1e6d-1652">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1652">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-1653">A resposta inclui uma entrada por item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1653">The response includes one entry per recommended item.</span></span> <span data-ttu-id="c1e6d-1654">Cada entrada tem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1654">Each entry has the following data:</span></span>

* <span data-ttu-id="c1e6d-1655">`Feed\entry\content\properties\Id` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="c1e6d-1656">`Feed\entry\content\properties\Name` - Nome do item.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1656">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="c1e6d-1657">`Feed\entry\content\properties\Rating` - Classificação da recomendação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1657">`Feed\entry\content\properties\Rating` - Rating of the recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="c1e6d-1658">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="c1e6d-1659">Veja um exemplo de resposta no 12.1</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1659">See a response example in 12.1</span></span>

## <a name="13-user-usage-history"></a><span data-ttu-id="c1e6d-1660">13. Histórico de uso do usuário</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1660">13. User Usage History</span></span>
<span data-ttu-id="c1e6d-1661">Após a compilação de um modelo de recomendação, o sistema permitirá recuperar o histórico do usuário (os itens associados a um usuário específico) usado para a compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1661">Once a recommendation model was built the system will allow to retrieve the user history (items associated to a specific user) used for the build.</span></span>
<span data-ttu-id="c1e6d-1662">Essa API permite recuperar o histórico do usuário</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1662">This API allow to retrieve the user history</span></span>

<span data-ttu-id="c1e6d-1663">Observação: o histórico do usuário está disponível atualmente apenas para compilações de recomendação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1663">Note: the user history is currently available only for recommendation builds.</span></span>

### <a name="131-retrieve-user-history"></a><span data-ttu-id="c1e6d-1664">13.1 Recuperar o histórico do usuário</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1664">13.1 Retrieve user history</span></span>
<span data-ttu-id="c1e6d-1665">Recupere a lista de itens usada na compilação ativa ou na compilação especificada para a ID de usuário fornecida.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1665">Retrieve the list of item used in the active build or in the specified build for the given user id.</span></span>

| <span data-ttu-id="c1e6d-1666">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1666">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1667">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1667">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1668">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1668">GET</span></span> |<span data-ttu-id="c1e6d-1669">Obter o histórico do usuário para a compilação ativa.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1669">Get the user history for the active build.</span></span><br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/><span data-ttu-id="c1e6d-1670">Obter o histórico do usuário para a compilação ativa `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1670">Get the user history for the given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span></span><br/><br/><span data-ttu-id="c1e6d-1671">Exemplo:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span></span> |

| <span data-ttu-id="c1e6d-1672">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1672">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1673">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1673">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1674">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1674">modelId</span></span> |<span data-ttu-id="c1e6d-1675">o identificador exclusivo do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1675">the unique identifier of the model.</span></span> |
| <span data-ttu-id="c1e6d-1676">coluna</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1676">userId</span></span> |<span data-ttu-id="c1e6d-1677">o identificador exclusivo do usuário.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1677">the unique identifier of the user.</span></span> |
| <span data-ttu-id="c1e6d-1678">buildId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1678">buildId</span></span> |<span data-ttu-id="c1e6d-1679">parâmetro opcional, permitir indicar a partir de qual versão do histórico do usuário deve fazer a busca</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1679">optional parameter, allow to indicate from which build the user history should be fetch</span></span> |
| <span data-ttu-id="c1e6d-1680">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1680">apiVersion</span></span> |<span data-ttu-id="c1e6d-1681">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1681">1.0</span></span> |

<span data-ttu-id="c1e6d-1682">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1682">**Response:**</span></span>

<span data-ttu-id="c1e6d-1683">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1683">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-1684">A resposta inclui uma entrada por item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1684">The response includes one entry per recommended item.</span></span> <span data-ttu-id="c1e6d-1685">Cada entrada tem os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1685">Each entry has the following data:</span></span>

* <span data-ttu-id="c1e6d-1686">`Feed\entry\content\properties\Id` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="c1e6d-1687">`Feed\entry\content\properties\Name` - Nome do item.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1687">`Feed\entry\content\properties\Name` - Name of the item.</span></span>
* <span data-ttu-id="c1e6d-1688">`Feed\entry\content\properties\Rating` - N/A.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1688">`Feed\entry\content\properties\Rating` - N/A.</span></span>
* <span data-ttu-id="c1e6d-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span></span>

<span data-ttu-id="c1e6d-1690">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1690">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get User History</subtitle>
    <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'</id>
    <rights type="text" />
    <updated>2015-05-26T15:32:47Z</updated>
    <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'" />
    <entry>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
        <title type="text">CatalogItemsThatContainATokenEntity</title>
        <updated>2015-05-26T15:32:47Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetUserHistory?modelId='2779c063-48fb-46c1-bae3-74acddc8c1d1'&amp;userId='u_1013'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
        <content type="application/xml">
            <m:properties>
                <d:Id m:type="Edm.String">2406E770-769C-4189-89DE-1C9283F93A96</d:Id>
                <d:Name m:type="Edm.String">Clara Callan</d:Name>
                <d:Rating m:type="Edm.Double">0</d:Rating>
                <d:Reasoning m:type="Edm.String"/>
                <d:Metadata m:type="Edm.String"/>
                <d:FormattedRating m:type="Edm.Double" m:null="true"/>
            </m:properties>
        </content>
    </entry>
</feed>

## <a name="14-notifications"></a><span data-ttu-id="c1e6d-1691">14. Notificações</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1691">14. Notifications</span></span>
<span data-ttu-id="c1e6d-1692">As Recomendações do Azure Machine Learning criam notificações quando erros persistentes ocorrem no sistema.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in the system.</span></span> <span data-ttu-id="c1e6d-1693">Há três tipos de notificações:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1693">There are 3 types of notifications:</span></span>

1. <span data-ttu-id="c1e6d-1694">Falha na compilação – Essa notificação é disparada para cada falha de compilação.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1694">Build failure - This notification is triggered for every build failure.</span></span>
2. <span data-ttu-id="c1e6d-1695">Falha no processo de aquisição de dados - Essa notificação é disparada quando há mais de 100 erros nos últimos 5 minutos no processamento de eventos de uso por modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in the last 5 minutes in the processing of usage events per model.</span></span>
3. <span data-ttu-id="c1e6d-1696">Falha de consumo de recomendação - Essa notificação é disparada quando há mais de 100 erros nos últimos 5 minutos no processamento de solicitações de recomendação por modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in the last 5 minutes in the processing of recommendation requests per model.</span></span>

### <a name="141-get-notifications"></a><span data-ttu-id="c1e6d-1697">14.1.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1697">14.1.</span></span> <span data-ttu-id="c1e6d-1698">Obter notificações</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1698">Get Notifications</span></span>
<span data-ttu-id="c1e6d-1699">Recupera todas as notificação para todos os modelos ou para um único modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1699">Retrieves all the notifications for all models or for a single model.</span></span>

| <span data-ttu-id="c1e6d-1700">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1700">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1701">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1701">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1702">GET</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1702">GET</span></span> |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1703">Obter todas as notificações para todos os modelos:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1703">Getting all notifications for all models:</span></span><br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1704">Exemplo para obter notificações para um modelo específico:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1704">Example for getting notifications for a specific model:</span></span><br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| <span data-ttu-id="c1e6d-1705">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1705">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1706">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1706">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1707">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1707">modelId</span></span> |<span data-ttu-id="c1e6d-1708">Parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1708">Optional parameter.</span></span> <span data-ttu-id="c1e6d-1709">Quando omitido, você receberá todas as notificações para todos os modelos.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1709">When omitted, you will get all notifications for all models.</span></span> <br><span data-ttu-id="c1e6d-1710">Valor válido: o identificador exclusivo do modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1710">Valid value: unique identifier of the model.</span></span> |
| <span data-ttu-id="c1e6d-1711">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1711">apiVersion</span></span> |<span data-ttu-id="c1e6d-1712">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1712">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-1713">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1713">Request Body</span></span> |<span data-ttu-id="c1e6d-1714">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1714">NONE</span></span> |

<span data-ttu-id="c1e6d-1715">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1715">**Response:**</span></span>

<span data-ttu-id="c1e6d-1716">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1716">HTTP Status code: 200</span></span>

<span data-ttu-id="c1e6d-1717">XML de OData</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1717">OData XML</span></span>

    The response includes one entry per notification. Each entry has the following data:
        * feed\entry\content\properties\UserName - Internal user name identification.
        * feed\entry\content\properties\ModelId - Model ID.
        * feed\entry\content\properties\Message - Notification message.
        * feed\entry\content\properties\DateCreated - Date that this notification was created in UTC format.
        * feed\entry\content\properties\NotificationType - Notification types. Values are BuildFailure, RecommendationFailure, and DataAquisitionFailure.

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get a list of Notifications for a user</subtitle>
        <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'</id>
        <rights type="text" />
        <updated>2014-11-04T13:24:23Z</updated>
        <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'" />
        <entry>
                <id>https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1</id>
            <title type="text">GetAListOfNotificationsForAUserEntity</title>
            <updated>2014-11-04T13:24:23Z</updated>
            <link rel="self" href="https://api.datamarket.azure.com/amla/recommendations/v3/GetNotifications?modelId='967136e8-f868-4258-9331-10d567f87fae'&amp;apiVersion='1.0'&amp;$skip=0&amp;$top=1" />
            <content type="application/xml">
                <m:properties>
                    <d:UserName m:type="Edm.String">515506bc-3693-4dce-a5e2-81cb3e8efb56@dm.com</d:UserName>
                    <d:ModelId m:type="Edm.String">967136e8-f868-4258-9331-10d567f87fae</d:ModelId>
                    <d:Message m:type="Edm.String">Build failed for user</d:Message>
                    <d:DateCreated m:type="Edm.String">2014-11-04T13:23:14.383</d:DateCreated>
                    <d:NotificationType m:type="Edm.String">BuildFailure</d:NotificationType>
                </m:properties>
            </content>
        </entry>
    </feed>

### <a name="142-delete-model-notifications"></a><span data-ttu-id="c1e6d-1718">14.2.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1718">14.2.</span></span> <span data-ttu-id="c1e6d-1719">Excluir as notificações de modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1719">Delete Model Notifications</span></span>
<span data-ttu-id="c1e6d-1720">Exclui todas notificações de leitura de um modelo.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1720">Deletes all read notifications for a model.</span></span>

| <span data-ttu-id="c1e6d-1721">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1721">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1722">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1722">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1723">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1723">DELETE</span></span> |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="c1e6d-1724">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1724">Example:</span></span><br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-1725">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1725">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1726">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1726">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1727">modelId</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1727">modelId</span></span> |<span data-ttu-id="c1e6d-1728">Identificador exclusivo do modelo</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1728">Unique identifier of the model</span></span> |
| <span data-ttu-id="c1e6d-1729">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1729">apiVersion</span></span> |<span data-ttu-id="c1e6d-1730">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1730">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-1731">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1731">Request Body</span></span> |<span data-ttu-id="c1e6d-1732">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1732">NONE</span></span> |

<span data-ttu-id="c1e6d-1733">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1733">**Response**:</span></span>

<span data-ttu-id="c1e6d-1734">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1734">HTTP Status code: 200</span></span>

### <a name="143-delete-user-notifications"></a><span data-ttu-id="c1e6d-1735">14.3.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1735">14.3.</span></span> <span data-ttu-id="c1e6d-1736">Excluir as notificações do usuário</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1736">Delete User Notifications</span></span>
<span data-ttu-id="c1e6d-1737">Exclui todas as notificações de todos os modelos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1737">Deletes all notifications for all models.</span></span>

| <span data-ttu-id="c1e6d-1738">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1738">HTTP Method</span></span> | <span data-ttu-id="c1e6d-1739">URI</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1739">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1740">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1740">DELETE</span></span> |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| <span data-ttu-id="c1e6d-1741">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1741">Parameter Name</span></span> | <span data-ttu-id="c1e6d-1742">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1742">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="c1e6d-1743">apiVersion</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1743">apiVersion</span></span> |<span data-ttu-id="c1e6d-1744">1.0</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1744">1.0</span></span> |
|  | |
| <span data-ttu-id="c1e6d-1745">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1745">Request Body</span></span> |<span data-ttu-id="c1e6d-1746">NENHUM</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1746">NONE</span></span> |

<span data-ttu-id="c1e6d-1747">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1747">**Response**:</span></span>

<span data-ttu-id="c1e6d-1748">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1748">HTTP Status code: 200</span></span>

## <a name="15-legal"></a><span data-ttu-id="c1e6d-1749">15. Legal</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1749">15. Legal</span></span>
<span data-ttu-id="c1e6d-1750">Este documento é fornecido "no estado em que se encontra".</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1750">This document is provided “as-is”.</span></span> <span data-ttu-id="c1e6d-1751">Informações e opiniões expressadas neste documento, incluindo URLs e outras referências a sites da Internet, podem ser alteradas sem aviso prévio.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span><br><br>
<span data-ttu-id="c1e6d-1752">Alguns exemplos aqui representados são fornecidos somente para fins de ilustração e são fictícios.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="c1e6d-1753">Nenhuma associação ou conexão real é intencional ou deve ser inferida.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1753">No real association or connection is intended or should be inferred.</span></span><br><br>
<span data-ttu-id="c1e6d-1754">Este documento não fornece a você nenhum direito legal a qualquer propriedade intelectual de qualquer produto da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1754">This document does not provide you with any legal rights to any intellectual property in any Microsoft product.</span></span> <span data-ttu-id="c1e6d-1755">Você pode copiar e usar este documento para fins de consulta interna.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1755">You may copy and use this document for your internal, reference purposes.</span></span><br><br>
<span data-ttu-id="c1e6d-1756">© 2015 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1756">© 2015 Microsoft.</span></span> <span data-ttu-id="c1e6d-1757">Todos os direitos reservados.</span><span class="sxs-lookup"><span data-stu-id="c1e6d-1757">All rights reserved.</span></span>

