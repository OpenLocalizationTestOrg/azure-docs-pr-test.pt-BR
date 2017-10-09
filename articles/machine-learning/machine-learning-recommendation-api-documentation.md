---
title: "aaaMachine documentação da API do aprendizado recomendações | Microsoft Docs"
description: "Documentação da API de recomendações de aprendizado de máquina do Azure para um mecanismo de recomendações disponível no Microsoft Azure Marketplace de saudação."
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
redirect_document_id: True
ms.openlocfilehash: d1cec228bf23870c05c8ab8df2779b0c3c65b06d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations-api-documentation"></a><span data-ttu-id="e9ca8-103">Documentação da API de Recomendações do Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e9ca8-103">Azure Machine Learning Recommendations API Documentation</span></span>
> [!NOTE]
> <span data-ttu-id="e9ca8-104">Deve começar a usar o hello recomendações API cognitivas serviço em vez de nesta versão.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="e9ca8-105">Olá serviço cognitivas recomendações será substituído por esse serviço e todos os novos recursos de saudação serão desenvolvidos existe.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="e9ca8-106">Ele possui novos recursos como suporte ao processamento em lotes, um Gerenciador de API aprimorado, uma superfície de API mais limpa, uma experiência de inscrição/cobrança mais consistente etc.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="e9ca8-107">Saiba mais sobre [toohello migrando novo serviço cognitivas](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="e9ca8-108">Este documento descreve as APIs de Recomendações do Microsoft Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-108">This document depicts Microsoft Azure Machine Learning Recommendations APIs.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="e9ca8-109">1. Visão geral</span><span class="sxs-lookup"><span data-stu-id="e9ca8-109">1. General overview</span></span>
<span data-ttu-id="e9ca8-110">Este documento é uma referência para a API.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-110">This document is an API reference.</span></span> <span data-ttu-id="e9ca8-111">Você deve começar com o documento de "Azure Machine Learning recomendação – início rápido" hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-111">You should start with hello “Azure Machine Learning Recommendation - Quick Start” document.</span></span>

<span data-ttu-id="e9ca8-112">Olá API de recomendações de aprendizado de máquina do Azure pode ser dividido em Olá seguintes grupos lógicos:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-112">hello Azure Machine Learning Recommendations API can be divided into hello following logical groups:</span></span>

* <span data-ttu-id="e9ca8-113"><ins>Limitações</ins> - limitações da API de recomendações.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-113"><ins>Limitations</ins> - Recommendations API limitations.</span></span>
* <span data-ttu-id="e9ca8-114"><ins>Informações gerais</ins> -informações sobre autenticação, controle de versão e URI de serviço.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-114"><ins>General Information</ins> - Information on authentication, service URI and versioning.</span></span>
* <span data-ttu-id="e9ca8-115"><ins>Modelo Basic</ins> -APIs que permitem operações básicas do toodo Olá no modelo (por exemplo, criar, atualizar e excluir um modelo).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-115"><ins>Model Basic</ins> - APIs that enable you toodo hello basic operations on model (e.g. create, update and delete a model).</span></span>
* <span data-ttu-id="e9ca8-116"><ins>Modelo avançado</ins> -APIs que permitem que você tooget avançado análises de dados no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-116"><ins>Model Advanced</ins> - APIs that enable you tooget advanced data insights on hello model.</span></span>
* <span data-ttu-id="e9ca8-117"><ins>Modelo de regras de negócio</ins> -APIs que permitem a você as regras de negócio toomanage nos resultados de recomendação de modelo hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-117"><ins>Model Business Rules</ins> - APIs that enable you toomanage business rules on hello model recommendation results.</span></span>
* <span data-ttu-id="e9ca8-118"><ins>Catálogo</ins> -APIs que permitem operações básicas de toodo em um catálogo de modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-118"><ins>Catalog</ins> - APIs that enable you toodo basic operations on a model catalog.</span></span> <span data-ttu-id="e9ca8-119">Um catálogo contém informações de metadados sobre itens Olá Olá de dados de uso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-119">A catalog contains metadata information on hello items of hello usage data.</span></span>
* <span data-ttu-id="e9ca8-120"><ins>Recurso</ins> -APIs que permitem insights tooget no item no catálogo hello e como toouse esse melhores recomendações toobuild informações.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-120"><ins>Feature</ins> - APIs that enable tooget insights on item into hello catalog and how toouse this information toobuild better recommendations.</span></span>
* <span data-ttu-id="e9ca8-121"><ins>Dados de uso</ins> -APIs que permitem operações básicas de toodo nos dados de uso do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-121"><ins>Usage Data</ins> - APIs that enable you toodo basic operations on hello model usage data.</span></span> <span data-ttu-id="e9ca8-122">Dados de uso no formato básico Olá consistem em linhas que incluem pares de &#60; userId &#62; &#60; itemId &#62;.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-122">Usage data in hello basic form consists of rows that include pairs of &#60;userId&#62;,&#60;itemId&#62;.</span></span>
* <span data-ttu-id="e9ca8-123"><ins>Criar</ins> - criar APIs que permitem que você tootrigger um modelo e façam operações básicas que são relacionadas toothis compilar.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-123"><ins>Build</ins> - APIs that enable you tootrigger a model build and do basic operations that are related toothis build.</span></span> <span data-ttu-id="e9ca8-124">Você pode iniciar uma compilação de modelo uma vez que você tenha dados de uso valiosos.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-124">You can trigger a model build once you have valuable usage data.</span></span>
* <span data-ttu-id="e9ca8-125"><ins>Recomendação</ins> -APIs que permitem a você recomendações tooconsume depois que termina de compilação de saudação de um modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-125"><ins>Recommendation</ins> - APIs that enable you tooconsume recommendations once hello build of a model ends.</span></span>
* <span data-ttu-id="e9ca8-126"><ins>Dados de usuário</ins> -APIs que permitem a você informações toofetch nos dados de uso do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-126"><ins>User Data</ins> - APIs that enable you toofetch information on hello user usage data.</span></span>
* <span data-ttu-id="e9ca8-127"><ins>Notificações</ins> -APIs que permitem que você tooreceive notificações sobre problemas relacionados a operações tooyour API.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-127"><ins>Notifications</ins> - APIs that enable you tooreceive notifications on problems related tooyour API operations.</span></span> <span data-ttu-id="e9ca8-128">(Por exemplo, você estiver relatando dados de uso por meio de aquisição de dados e a maioria dos eventos de saudação processamento estão falhando.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-128">(For example, you are reporting usage data via Data Acquisition and most of hello events processing are failing.</span></span> <span data-ttu-id="e9ca8-129">Uma notificação de erro será gerada.)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-129">An error notification will be raised.)</span></span>

## <a name="2-limitations"></a><span data-ttu-id="e9ca8-130">2. Limitações</span><span class="sxs-lookup"><span data-stu-id="e9ca8-130">2. Limitations</span></span>
* <span data-ttu-id="e9ca8-131">número máximo de saudação de modelos por assinatura é 10.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-131">hello maximum number of models per subscription is 10.</span></span>
* <span data-ttu-id="e9ca8-132">Olá o número máximo de compilações por modelo é 20.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-132">hello maximum number of builds per model is 20.</span></span>
* <span data-ttu-id="e9ca8-133">número máximo de saudação de itens que pode conter um catálogo é 100.000.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-133">hello maximum number of items that a catalog can hold is 100,000.</span></span>
* <span data-ttu-id="e9ca8-134">número máximo de saudação de pontos de uso que são mantidos é ~ 5.000.000.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-134">hello maximum number of usage points that are kept is ~5,000,000.</span></span> <span data-ttu-id="e9ca8-135">Olá mais antigo será excluído se novas serão carregadas ou relatadas.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-135">hello oldest will be deleted if new ones will be uploaded or reported.</span></span>
* <span data-ttu-id="e9ca8-136">tamanho máximo de saudação de dados que podem ser enviados no POST (por exemplo, importar dados de catálogo, importar dados de uso) é de 200MB.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-136">hello maximum size of data that can be sent in POST (e.g. import catalog data, import usage data) is 200MB.</span></span>
* <span data-ttu-id="e9ca8-137">número máximo de saudação de itens que podem ser feitas para a obtenção de recomendações é 150.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-137">hello maximum number of items that can be asked for when getting recommendations is 150.</span></span>

## <a name="3-apis---general-information"></a><span data-ttu-id="e9ca8-138">3. APIs – Informações Gerais</span><span class="sxs-lookup"><span data-stu-id="e9ca8-138">3. APIs - general information</span></span>
### <a name="31-authentication"></a><span data-ttu-id="e9ca8-139">3.1.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-139">3.1.</span></span> <span data-ttu-id="e9ca8-140">Autenticação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-140">Authentication</span></span>
<span data-ttu-id="e9ca8-141">Siga as diretrizes do Microsoft Azure Marketplace Olá sobre a autenticação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-141">Please follow hello Microsoft Azure Marketplace guidelines regarding authentication.</span></span> <span data-ttu-id="e9ca8-142">marketplace Olá dá suporte a um método de autenticação de Basic ou OAuth do hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-142">hello marketplace supports either hello Basic or OAuth authentication method.</span></span>

### <a name="32-service-uri"></a><span data-ttu-id="e9ca8-143">3.2.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-143">3.2.</span></span> <span data-ttu-id="e9ca8-144">URI de serviço</span><span class="sxs-lookup"><span data-stu-id="e9ca8-144">Service URI</span></span>
<span data-ttu-id="e9ca8-145">Olá URI raiz do serviço para Olá APIs de recomendações de aprendizado de máquina do Azure é [aqui.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-145">hello service root URI for hello Azure Machine Learning Recommendations APIs is [here.](https://api.datamarket.azure.com/amla/recommendations/v3/)</span></span>

<span data-ttu-id="e9ca8-146">URI do serviço completo Olá é expressa usando elementos da especificação de OData hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-146">hello full service URI is expressed using elements of hello OData specification.</span></span>  

### <a name="33-api-version"></a><span data-ttu-id="e9ca8-147">3.3.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-147">3.3.</span></span> <span data-ttu-id="e9ca8-148">Versão da API</span><span class="sxs-lookup"><span data-stu-id="e9ca8-148">API version</span></span>
<span data-ttu-id="e9ca8-149">Cada chamada de API terá, no final do hello, um parâmetro de consulta chamado apiVersion too1.0 deve ser definido.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-149">Each API call will have, at hello end, a query parameter called apiVersion that should be set too1.0.</span></span>

### <a name="34-ids-are-case-sensitive"></a><span data-ttu-id="e9ca8-150">3.4.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-150">3.4.</span></span> <span data-ttu-id="e9ca8-151">IDs diferenciam minúsculas e maiúsculas</span><span class="sxs-lookup"><span data-stu-id="e9ca8-151">IDs are case sensitive</span></span>
<span data-ttu-id="e9ca8-152">IDs, retornados por qualquer Olá APIs, diferenciam maiusculas de minúsculas e devem ser usadas como tal quando passados como parâmetros em chamadas API subsequentes.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-152">IDs, returned by any of hello APIs, are case sensitive and should be used as such when passed as parameters in subsequent API calls.</span></span> <span data-ttu-id="e9ca8-153">Por exemplo, IDS d modelo e de catálogo diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-153">For instance, model IDs and catalog IDs are case sensitive.</span></span>

## <a name="4-recommendations-quality-and-cold-items"></a><span data-ttu-id="e9ca8-154">4. Qualidade das recomendações e itens frios</span><span class="sxs-lookup"><span data-stu-id="e9ca8-154">4. Recommendations Quality and Cold Items</span></span>
### <a name="41-recommendation-quality"></a><span data-ttu-id="e9ca8-155">4.1.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-155">4.1.</span></span> <span data-ttu-id="e9ca8-156">Qualidade da recomendação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-156">Recommendation quality</span></span>
<span data-ttu-id="e9ca8-157">Criar um modelo de recomendação é geralmente suficiente recomendações de tooprovide tooallow Olá sistema.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-157">Creating a recommendation model is usually enough tooallow hello system tooprovide recommendations.</span></span> <span data-ttu-id="e9ca8-158">No entanto, qualidade da recomendação varia com base no uso de saudação processado e Olá cobertura do catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-158">Nevertheless, recommendation quality varies based on hello usage processed and hello coverage of hello catalog.</span></span> <span data-ttu-id="e9ca8-159">Por exemplo se você tiver muitos itens frios (sem uso significativo de itens), o sistema de saudação terão dificuldade para fornecer uma recomendação de tal um item ou usando um item tal como recomendado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-159">For example if you have a lot of cold items (items without significant usage), hello system will have difficulties providing a recommendation for such an item or using such an item as a recommended one.</span></span> <span data-ttu-id="e9ca8-160">No item frios problema na ordem tooovercome hello, sistema Olá permite o uso de saudação de metadados de recomendações de Olá Olá itens tooenhance.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-160">In order tooovercome hello cold item problem, hello system allows hello use of metadata of hello items tooenhance hello recommendations.</span></span> <span data-ttu-id="e9ca8-161">Esses metadados são chamados tooas recursos.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-161">This metadata is referred tooas features.</span></span> <span data-ttu-id="e9ca8-162">Os recursos mais comuns são o autor de um livro ou um ator de um filme.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-162">Typical features are a book's author or a movie's actor.</span></span> <span data-ttu-id="e9ca8-163">Recursos são fornecidos por meio do catálogo de saudação na forma de saudação de cadeias de caracteres de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-163">Features are provided via hello catalog in hello form of key/value strings.</span></span> <span data-ttu-id="e9ca8-164">Para o formato completo Olá Olá do arquivo de catálogo, consulte toohello [importar seção catálogo](#81-import-catalog-data).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-164">For hello full format of hello catalog file, please refer toohello [import catalog section](#81-import-catalog-data).</span></span> 

### <a name="42-rank-build"></a><span data-ttu-id="e9ca8-165">4.2.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-165">4.2.</span></span> <span data-ttu-id="e9ca8-166">Compilação de classificação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-166">Rank build</span></span>
<span data-ttu-id="e9ca8-167">Recursos podem aprimorar o modelo de recomendação hello, mas toodo assim requer o uso de saudação do recursos significativos.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-167">Features can enhance hello recommendation model, but toodo so requires hello use of meaningful features.</span></span> <span data-ttu-id="e9ca8-168">Uma nova compilação foi apresentada para essa finalidade: uma compilação de classificação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-168">For this purpose a new build was introduced - a rank build.</span></span> <span data-ttu-id="e9ca8-169">Esta compilação será a classificação da utilidade de saudação de recursos.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-169">This build will rank hello usefulness of features.</span></span> <span data-ttu-id="e9ca8-170">Um recurso significativo é um recurso com uma pontuação de classificação 2 ou maior.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-170">A meaningful feature is a feature with a rank score of 2 and up.</span></span>
<span data-ttu-id="e9ca8-171">Depois de entender quais recursos de saudação são significativos, disparar um build de recomendação com lista hello (ou sublista) dos recursos significativos.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-171">After understanding which of hello features are meaningful, trigger a recommendation build with hello list (or sublist) of meaningful features.</span></span> <span data-ttu-id="e9ca8-172">É possível toouse que esses recursos para o aprimoramento de saudação do passivos itens e itens frios.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-172">It is possible toouse these feature for hello enhancement of both warm items and cold items.</span></span> <span data-ttu-id="e9ca8-173">Em ordem toouse-los para itens passivos, Olá `UseFeatureInModel` parâmetro de compilação deve ser configurado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-173">In order toouse them for warm items, hello `UseFeatureInModel` build parameter should be set up.</span></span> <span data-ttu-id="e9ca8-174">Em ordem toouse de recursos para itens frios, Olá `AllowColdItemPlacement` parâmetro de compilação deve ser habilitado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-174">In order toouse features for cold items, hello `AllowColdItemPlacement` build parameter should be enabled.</span></span>
<span data-ttu-id="e9ca8-175">Observação: Não é possível tooenable `AllowColdItemPlacement` sem habilitar `UseFeatureInModel`.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-175">Note: It is not possible tooenable `AllowColdItemPlacement` without enabling `UseFeatureInModel`.</span></span>

### <a name="43-recommendation-reasoning"></a><span data-ttu-id="e9ca8-176">4.3.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-176">4.3.</span></span> <span data-ttu-id="e9ca8-177">Raciocínio de recomendação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-177">Recommendation reasoning</span></span>
<span data-ttu-id="e9ca8-178">O raciocínio de recomendação é outro aspecto do uso de recursos.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-178">Recommendation reasoning is another aspect of feature usage.</span></span> <span data-ttu-id="e9ca8-179">Na verdade, o mecanismo de recomendações de aprendizado de máquina do Azure de saudação pode usar explicações de recomendação de tooprovide de recursos (também conhecido como</span><span class="sxs-lookup"><span data-stu-id="e9ca8-179">Indeed, hello Azure Machine Learning Recommendations engine can use features tooprovide recommendation explanations (a.k.a.</span></span> <span data-ttu-id="e9ca8-180">raciocínio), à esquerda toomore confiança no hello recomendado item do consumidor de recomendação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-180">reasoning), leading toomore confidence in hello recommended item from hello recommendation consumer.</span></span>
<span data-ttu-id="e9ca8-181">tooenable raciocínio, hello `AllowFeatureCorrelation` e `ReasoningFeatureList` parâmetros devem ser toorequesting antes da instalação uma compilação de recomendação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-181">tooenable reasoning, hello `AllowFeatureCorrelation` and `ReasoningFeatureList` parameters should be setup prior toorequesting a recommendation build.</span></span>

## <a name="5-model-basic"></a><span data-ttu-id="e9ca8-182">5. Modelo Básico</span><span class="sxs-lookup"><span data-stu-id="e9ca8-182">5. Model Basic</span></span>
### <a name="51-create-model"></a><span data-ttu-id="e9ca8-183">5.1.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-183">5.1.</span></span> <span data-ttu-id="e9ca8-184">Criar modelo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-184">Create Model</span></span>
<span data-ttu-id="e9ca8-185">Cria uma solicitação "criar modelo".</span><span class="sxs-lookup"><span data-stu-id="e9ca8-185">Creates a “create model” request.</span></span>

| <span data-ttu-id="e9ca8-186">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-186">HTTP Method</span></span> | <span data-ttu-id="e9ca8-187">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-187">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-188">POST</span><span class="sxs-lookup"><span data-stu-id="e9ca8-188">POST</span></span> |`<rootURI>/CreateModel?modelName=%27<model_name>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-189">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-189">Example:</span></span><br>`<rootURI>/CreateModel?modelName=%27MyFirstModel%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-190">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-190">Parameter Name</span></span> | <span data-ttu-id="e9ca8-191">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-191">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-192">modelName</span><span class="sxs-lookup"><span data-stu-id="e9ca8-192">modelName</span></span> |<span data-ttu-id="e9ca8-193">São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-193">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="e9ca8-194">Comprimento máximo: 20</span><span class="sxs-lookup"><span data-stu-id="e9ca8-194">Max length: 20</span></span> |
| <span data-ttu-id="e9ca8-195">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-195">apiVersion</span></span> |<span data-ttu-id="e9ca8-196">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-196">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-197">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-197">Request Body</span></span> |<span data-ttu-id="e9ca8-198">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-198">NONE</span></span> |

<span data-ttu-id="e9ca8-199">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-199">**Response**:</span></span>

<span data-ttu-id="e9ca8-200">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-200">HTTP Status code: 200</span></span>

* <span data-ttu-id="e9ca8-201">`feed/entry/content/properties/id`-Contém a ID do modelo hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-201">`feed/entry/content/properties/id` - Contains hello model ID.</span></span>
  <span data-ttu-id="e9ca8-202">**Observação**: a ID do modelo diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-202">**Note**: model ID is case sensitive.</span></span>

<span data-ttu-id="e9ca8-203">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-203">OData XML</span></span>

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

### <a name="52-get-model"></a><span data-ttu-id="e9ca8-204">5.2.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-204">5.2.</span></span> <span data-ttu-id="e9ca8-205">Obter modelo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-205">Get Model</span></span>
<span data-ttu-id="e9ca8-206">Criar uma solicitação “obter modelo".</span><span class="sxs-lookup"><span data-stu-id="e9ca8-206">Creates a “get model” request.</span></span>

| <span data-ttu-id="e9ca8-207">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-207">HTTP Method</span></span> | <span data-ttu-id="e9ca8-208">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-208">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-209">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-209">GET</span></span> |`<rootURI>/GetModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="e9ca8-210">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-210">Example:</span></span><br>`<rootURI>/GetModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-211">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-211">Parameter Name</span></span> | <span data-ttu-id="e9ca8-212">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-212">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-213">ID</span><span class="sxs-lookup"><span data-stu-id="e9ca8-213">id</span></span> |<span data-ttu-id="e9ca8-214">Identificador exclusivo do modelo de saudação (com distinção entre maiusculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-214">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="e9ca8-215">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-215">apiVersion</span></span> |<span data-ttu-id="e9ca8-216">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-216">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-217">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-217">Request Body</span></span> |<span data-ttu-id="e9ca8-218">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-218">NONE</span></span> |

<span data-ttu-id="e9ca8-219">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-219">**Response**:</span></span>

<span data-ttu-id="e9ca8-220">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-220">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-221">dados de modelo de saudação podem ser encontrados em Olá elementos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-221">hello model data can be found under hello following elements:</span></span>

* <span data-ttu-id="e9ca8-222">`feed/entry/content/properties/Id` - ID exclusivo do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-222">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="e9ca8-223">`feed/entry/content/properties/Name` - Nome do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-223">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="e9ca8-224">`feed/entry/content/properties/Date` - Data de criação do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-224">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="e9ca8-225">`feed/entry/content/properties/Status` - Status do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-225">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="e9ca8-226">Um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-226">One of hello following:</span></span>
  * <span data-ttu-id="e9ca8-227">Criado - O modelo é criado e não contém Catálogo e Uso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-227">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="e9ca8-228">ReadyForBuild - O modelo é criado e contém Catálogo e Uso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-228">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="e9ca8-229">`feed/entry/content/properties/HasActiveBuild`-Indica se o modelo de saudação foi criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-229">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="e9ca8-230">`feed/entry/content/properties/BuildId` - ID da compilação ativa do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-230">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="e9ca8-231">`feed/entry/content/properties/Mpr` - Classificação porcentual média do modelo (MPR - consulte ModelInsight para obter mais informações).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-231">`feed/entry/content/properties/Mpr` - Model mean percentile ranking (MPR - see ModelInsight for more information).</span></span>
* <span data-ttu-id="e9ca8-232">`feed/entry/content/properties/UserName` - Nome do usuário interno do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-232">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>

<span data-ttu-id="e9ca8-233">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-233">OData XML</span></span>

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

### <a name="53----get-all-models"></a><span data-ttu-id="e9ca8-234">5.3.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-234">5.3.</span></span>    <span data-ttu-id="e9ca8-235">Obter todos os modelos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-235">Get All Models</span></span>
<span data-ttu-id="e9ca8-236">Recupera todos os modelos do usuário atual hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-236">Retrieves all models of hello current user.</span></span>

| <span data-ttu-id="e9ca8-237">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-237">HTTP Method</span></span> | <span data-ttu-id="e9ca8-238">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-238">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-239">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-239">GET</span></span> |`<rootURI>/GetAllModels?apiVersion=%271.0%27`<br><span data-ttu-id="e9ca8-240">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-240">Example:</span></span><br>`<rootURI>/GetAllModels?apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-241">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-241">Parameter Name</span></span> | <span data-ttu-id="e9ca8-242">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-242">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-243">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-243">apiVersion</span></span> |<span data-ttu-id="e9ca8-244">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-244">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-245">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-245">Request Body</span></span> |<span data-ttu-id="e9ca8-246">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-246">NONE</span></span> |

<span data-ttu-id="e9ca8-247">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-247">**Response**:</span></span>

<span data-ttu-id="e9ca8-248">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-248">HTTP Status code: 200</span></span>

* <span data-ttu-id="e9ca8-249">`feed/entry/content/properties/Id` - ID exclusivo do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-249">`feed/entry/content/properties/Id` - Model unique ID.</span></span>
* <span data-ttu-id="e9ca8-250">`feed/entry/content/properties/Name` - Nome do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-250">`feed/entry/content/properties/Name` - Model name.</span></span>
* <span data-ttu-id="e9ca8-251">`feed/entry/content/properties/Date` - Data de criação do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-251">`feed/entry/content/properties/Date` - Model creation date.</span></span>
* <span data-ttu-id="e9ca8-252">`feed/entry/content/properties/Status` - Status do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-252">`feed/entry/content/properties/Status` - Model status.</span></span> <span data-ttu-id="e9ca8-253">Um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-253">One of hello following:</span></span>
  * <span data-ttu-id="e9ca8-254">Criado - O modelo é criado e não contém Catálogo e Uso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-254">Created - Model is created and does not contain Catalog and Usage.</span></span>
  * <span data-ttu-id="e9ca8-255">ReadyForBuild - O modelo é criado e contém Catálogo e Uso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-255">ReadyForBuild - Model is created and contains Catalog and Usage.</span></span>
* <span data-ttu-id="e9ca8-256">`feed/entry/content/properties/HasActiveBuild`-Indica se o modelo de saudação foi criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-256">`feed/entry/content/properties/HasActiveBuild` - Indicates if hello model was built successfully.</span></span>
* <span data-ttu-id="e9ca8-257">`feed/entry/content/properties/BuildId` - ID da compilação ativa do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-257">`feed/entry/content/properties/BuildId` - Model active build ID.</span></span>
* <span data-ttu-id="e9ca8-258">`feed/entry/content/properties/Mpr` - MPR do modelo MPR (consulte o ModelInsight para obter mais informações).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-258">`feed/entry/content/properties/Mpr` - Model MPR (see ModelInsight for more information).</span></span>
* <span data-ttu-id="e9ca8-259">`feed/entry/content/properties/UserName` - Nome do usuário interno do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-259">`feed/entry/content/properties/UserName` - Model internal user name.</span></span>
* <span data-ttu-id="e9ca8-260">`feed/entry/content/properties/UsageFileNames` - Lista de arquivos de uso do modelo separados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-260">`feed/entry/content/properties/UsageFileNames` - List of model usage files separated by comma.</span></span>
* <span data-ttu-id="e9ca8-261">`feed/entry/content/properties/CatalogId` - ID do catálogo do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-261">`feed/entry/content/properties/CatalogId` - Model catalog ID.</span></span>
* <span data-ttu-id="e9ca8-262">`feed/entry/content/properties/Description` - Descrição do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-262">`feed/entry/content/properties/Description` - Model description.</span></span>
* <span data-ttu-id="e9ca8-263">`feed/entry/content/properties/CatalogFileName` - Nome do arquivo do catálogo do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-263">`feed/entry/content/properties/CatalogFileName` - Model catalog file name.</span></span>

<span data-ttu-id="e9ca8-264">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-264">OData XML</span></span>

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

### <a name="54----update-model"></a><span data-ttu-id="e9ca8-265">5.4.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-265">5.4.</span></span>    <span data-ttu-id="e9ca8-266">Atualizar modelo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-266">Update Model</span></span>
<span data-ttu-id="e9ca8-267">Você pode atualizar a descrição do modelo hello ou Olá ID do ativo de compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-267">You can update hello model description or hello active build ID.</span></span><br><span data-ttu-id="e9ca8-268">
<ins>ID de compilação ativa</ins> – cada compilação para cada modelo tem uma ID de compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-268">
<ins>Active build ID</ins> - Every build for every model has a build ID.</span></span> <span data-ttu-id="e9ca8-269">ID de compilação active Olá é Olá primeira compilação bem-sucedida cada novo modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-269">hello active build ID is hello first successful build of every new model.</span></span> <span data-ttu-id="e9ca8-270">Depois que você tiver uma ID de ativo de compilação e fazer compilações adicionais para Olá mesmo modelo, você precisa tooexplicitly defini-lo hello padrão criar ID se desejar.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-270">Once you have an active build ID and you do additional builds for hello same model, you need tooexplicitly set it as hello default build ID if you want to.</span></span> <span data-ttu-id="e9ca8-271">Quando você consome recomendações, se você não especificar a ID de compilação de saudação que você deseja toouse, padrão Olá um será usado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-271">When you consume recommendations, if you do not specify hello build ID that you want toouse, hello default one will be used automatically.</span></span><br>
<span data-ttu-id="e9ca8-272">Esse mecanismo permite que você - depois de um modelo de recomendação em produção - toobuild novos modelos e testá-las antes de promovê-los tooproduction.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-272">This mechanism enables you - once you have a recommendation model in production - toobuild new models and test them before you promote them tooproduction.</span></span>

| <span data-ttu-id="e9ca8-273">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-273">HTTP Method</span></span> | <span data-ttu-id="e9ca8-274">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-274">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-275">PUT</span><span class="sxs-lookup"><span data-stu-id="e9ca8-275">PUT</span></span> |`<rootURI>/UpdateModel?id=%27<modelId>%27&apiVersion=%271.0%27`<br><span data-ttu-id="e9ca8-276">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-276">Example:</span></span><br>`<rootURI>/UpdateModel?id=%279559872f-7a53-4076-a3c7-19d9385c1265%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-277">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-277">Parameter Name</span></span> | <span data-ttu-id="e9ca8-278">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-278">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-279">ID</span><span class="sxs-lookup"><span data-stu-id="e9ca8-279">id</span></span> |<span data-ttu-id="e9ca8-280">Identificador exclusivo do modelo de saudação (com distinção entre maiusculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-280">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="e9ca8-281">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-281">apiVersion</span></span> |<span data-ttu-id="e9ca8-282">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-282">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-283">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-283">Request Body</span></span> |`<ModelUpdateParams xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`<br>`<Description>New Description</Description>`<br>`<ActiveBuildId>-1</ActiveBuildId>`<br>` </ModelUpdateParams>`<br><br><span data-ttu-id="e9ca8-284">Observe que a descrição de marcas Olá XML e ActiveBuildId são opcionais.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-284">Note that hello XML tags Description and ActiveBuildId are optional.</span></span> <span data-ttu-id="e9ca8-285">Se você não quiser tooset descrição ou ActiveBuildId, remova a marca de inteiro de hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-285">If you do not want tooset Description or ActiveBuildId, remove hello entire tag.</span></span> |

<span data-ttu-id="e9ca8-286">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-286">**Response**:</span></span>

<span data-ttu-id="e9ca8-287">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-287">HTTP Status code: 200</span></span>

### <a name="55----delete-model"></a><span data-ttu-id="e9ca8-288">5.5.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-288">5.5.</span></span>    <span data-ttu-id="e9ca8-289">Excluir modelo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-289">Delete Model</span></span>
<span data-ttu-id="e9ca8-290">Exclui um modelo existente por ID.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-290">Deletes an existing model by ID.</span></span>

| <span data-ttu-id="e9ca8-291">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-291">HTTP Method</span></span> | <span data-ttu-id="e9ca8-292">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-292">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-293">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="e9ca8-293">DELETE</span></span> |`<rootURI>/DeleteModel?id=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="e9ca8-294">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-294">Example:</span></span><br>`<rootURI>/DeleteModel?id=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-295">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-295">Parameter Name</span></span> | <span data-ttu-id="e9ca8-296">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-296">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-297">ID</span><span class="sxs-lookup"><span data-stu-id="e9ca8-297">id</span></span> |<span data-ttu-id="e9ca8-298">Identificador exclusivo do modelo de saudação (com distinção entre maiusculas e minúsculas)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-298">Unique identifier of hello model (case sensitive)</span></span> |
| <span data-ttu-id="e9ca8-299">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-299">apiVersion</span></span> |<span data-ttu-id="e9ca8-300">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-300">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-301">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-301">Request Body</span></span> |<span data-ttu-id="e9ca8-302">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-302">NONE</span></span> |

<span data-ttu-id="e9ca8-303">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-303">**Response**:</span></span>

<span data-ttu-id="e9ca8-304">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-304">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-305">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-305">OData XML</span></span>

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

## <a name="6-model-advanced"></a><span data-ttu-id="e9ca8-306">6. Modelo Avançado</span><span class="sxs-lookup"><span data-stu-id="e9ca8-306">6. Model Advanced</span></span>
### <a name="61----model-data-insight"></a><span data-ttu-id="e9ca8-307">6.1.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-307">6.1.</span></span>    <span data-ttu-id="e9ca8-308">Visão de modelo de dados</span><span class="sxs-lookup"><span data-stu-id="e9ca8-308">Model Data Insight</span></span>
<span data-ttu-id="e9ca8-309">Retorna dados estatísticos sobre os dados de uso Olá este modelo foi criado com.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-309">Returns statistical data on hello usage data that this model was built with.</span></span>

<span data-ttu-id="e9ca8-310">Disponível somente para compilação de Recomendação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-310">Available only for Recommendation build.</span></span>

| <span data-ttu-id="e9ca8-311">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-311">HTTP Method</span></span> | <span data-ttu-id="e9ca8-312">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-312">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-313">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-313">GET</span></span> |`<rootURI>/GetDataInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="e9ca8-314">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-314">Example:</span></span><br>`<rootURI>/GetDataInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-315">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-315">Parameter Name</span></span> | <span data-ttu-id="e9ca8-316">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-316">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-317">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-317">modelId</span></span> |<span data-ttu-id="e9ca8-318">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-318">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-319">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-319">apiVersion</span></span> |<span data-ttu-id="e9ca8-320">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-320">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-321">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-321">Request Body</span></span> |<span data-ttu-id="e9ca8-322">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-322">NONE</span></span> |

<span data-ttu-id="e9ca8-323">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-323">**Response**:</span></span>

<span data-ttu-id="e9ca8-324">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-324">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-325">Olá dados são retornados como uma coleção de propriedades.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-325">hello data is returned as a collection of properties.</span></span>

* <span data-ttu-id="e9ca8-326">`feed/entry/id/content/properties/key`-Contém o nome da propriedade hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-326">`feed/entry/id/content/properties/key` - Holds hello property name.</span></span>
* <span data-ttu-id="e9ca8-327">`feed/entry/id/content/properties/value`-Contém o valor da propriedade hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-327">`feed/entry/id/content/properties/value` - Holds hello property value.</span></span>

<span data-ttu-id="e9ca8-328">Olá tabela a seguir mostra o valor de saudação que representa cada chave.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-328">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="e9ca8-329">Chave</span><span class="sxs-lookup"><span data-stu-id="e9ca8-329">Key</span></span> | <span data-ttu-id="e9ca8-330">Descrição</span><span class="sxs-lookup"><span data-stu-id="e9ca8-330">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-331">AvgItemLength</span><span class="sxs-lookup"><span data-stu-id="e9ca8-331">AvgItemLength</span></span> |<span data-ttu-id="e9ca8-332">Média de usuários distintos por item.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-332">Average number of distinct users per item.</span></span> |
| <span data-ttu-id="e9ca8-333">AvgUserLength</span><span class="sxs-lookup"><span data-stu-id="e9ca8-333">AvgUserLength</span></span> |<span data-ttu-id="e9ca8-334">Média de itens distintos por usuários.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-334">Average number of distinct items per user.</span></span> |
| <span data-ttu-id="e9ca8-335">DensificationNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="e9ca8-335">DensificationNumberOfItems</span></span> |<span data-ttu-id="e9ca8-336">Número de itens após a remoção dos itens que não podem ser modelados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-336">Number of items after pruning items that cannot be modelled.</span></span> |
| <span data-ttu-id="e9ca8-337">DensificationNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="e9ca8-337">DensificationNumberOfUsers</span></span> |<span data-ttu-id="e9ca8-338">Número de pontos de uso após a remoção de usuários e itens que não podem ser modelados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-338">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="e9ca8-339">DensificationNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="e9ca8-339">DensificationNumberOfRecords</span></span> |<span data-ttu-id="e9ca8-340">Número de pontos de uso após a remoção de usuários e itens que não podem ser modelados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-340">Number of usage points after pruning users and items that can't be modelled.</span></span> |
| <span data-ttu-id="e9ca8-341">MaxItemLength</span><span class="sxs-lookup"><span data-stu-id="e9ca8-341">MaxItemLength</span></span> |<span data-ttu-id="e9ca8-342">Número de usuários distintos para o item mais popular hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-342">Number of distinct users for hello most popular item.</span></span> |
| <span data-ttu-id="e9ca8-343">MaxUserLength</span><span class="sxs-lookup"><span data-stu-id="e9ca8-343">MaxUserLength</span></span> |<span data-ttu-id="e9ca8-344">Número máximo de itens distintos para um usuário.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-344">Maximal number of distinct items for a user.</span></span> |
| <span data-ttu-id="e9ca8-345">MinItemLength</span><span class="sxs-lookup"><span data-stu-id="e9ca8-345">MinItemLength</span></span> |<span data-ttu-id="e9ca8-346">Número máximo de usuários distintos para um item.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-346">Maximal number of distinct users for an item.</span></span> |
| <span data-ttu-id="e9ca8-347">MinUserLength</span><span class="sxs-lookup"><span data-stu-id="e9ca8-347">MinUserLength</span></span> |<span data-ttu-id="e9ca8-348">Número mínimo de itens distintos para um usuário.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-348">Minimal number of distinct items for a user.</span></span> |
| <span data-ttu-id="e9ca8-349">RawNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="e9ca8-349">RawNumberOfItems</span></span> |<span data-ttu-id="e9ca8-350">Número de itens em arquivos de uso de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-350">Number of items in hello usage files.</span></span> |
| <span data-ttu-id="e9ca8-351">RawNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="e9ca8-351">RawNumberOfUsers</span></span> |<span data-ttu-id="e9ca8-352">Número de pontos de uso antes de qualquer remoção.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-352">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="e9ca8-353">RawNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="e9ca8-353">RawNumberOfRecords</span></span> |<span data-ttu-id="e9ca8-354">Número de pontos de uso antes de qualquer remoção.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-354">Number of usage points before any pruning.</span></span> |
| <span data-ttu-id="e9ca8-355">SamplingNumberOfItems</span><span class="sxs-lookup"><span data-stu-id="e9ca8-355">SamplingNumberOfItems</span></span> |<span data-ttu-id="e9ca8-356">N/D</span><span class="sxs-lookup"><span data-stu-id="e9ca8-356">N/A</span></span> |
| <span data-ttu-id="e9ca8-357">SamplingNumberOfRecords</span><span class="sxs-lookup"><span data-stu-id="e9ca8-357">SamplingNumberOfRecords</span></span> |<span data-ttu-id="e9ca8-358">N/D</span><span class="sxs-lookup"><span data-stu-id="e9ca8-358">N/A</span></span> |
| <span data-ttu-id="e9ca8-359">SamplingNumberOfUsers</span><span class="sxs-lookup"><span data-stu-id="e9ca8-359">SamplingNumberOfUsers</span></span> |<span data-ttu-id="e9ca8-360">N/D</span><span class="sxs-lookup"><span data-stu-id="e9ca8-360">N/A</span></span> |

<span data-ttu-id="e9ca8-361">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-361">OData XML</span></span>

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

### <a name="62----model-insight"></a><span data-ttu-id="e9ca8-362">6.2.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-362">6.2.</span></span>    <span data-ttu-id="e9ca8-363">Percepção de modelo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-363">Model Insight</span></span>
<span data-ttu-id="e9ca8-364">Retorna informações de modelo na compilação active hello ou (se fornecida) em uma versão específica.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-364">Returns model insight on hello active build or (if given) on a specific build.</span></span>

<span data-ttu-id="e9ca8-365">Disponível somente para compilação de Recomendação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-365">Available only for Recommendation build.</span></span>

| <span data-ttu-id="e9ca8-366">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-366">HTTP Method</span></span> | <span data-ttu-id="e9ca8-367">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-367">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-368">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-368">GET</span></span> |<span data-ttu-id="e9ca8-369">Com a ID de compilação ativa:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-369">With active build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-370">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-370">Example:</span></span><br>`<rootURI>/GetModelInsight?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-371">Com a ID de compilação específica:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-371">With specific build ID:</span></span><br>`<rootURI>/GetModelInsight?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-372">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-372">Parameter Name</span></span> | <span data-ttu-id="e9ca8-373">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-373">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-374">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-374">modelId</span></span> |<span data-ttu-id="e9ca8-375">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-375">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-376">buildId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-376">buildId</span></span> |<span data-ttu-id="e9ca8-377">Opcional - número que identifica uma compilação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-377">Optional - number that identifies a successful build.</span></span> |
| <span data-ttu-id="e9ca8-378">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-378">apiVersion</span></span> |<span data-ttu-id="e9ca8-379">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-379">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-380">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-380">Request Body</span></span> |<span data-ttu-id="e9ca8-381">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-381">NONE</span></span> |

<span data-ttu-id="e9ca8-382">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-382">**Response**:</span></span>

<span data-ttu-id="e9ca8-383">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-383">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-384">Olá dados são retornados como uma coleção de propriedades.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-384">hello data is returned as a collection of properties.</span></span>

* `feed/entry/id/content/properties/key`
* `feed/entry/id/content/properties/value`

<span data-ttu-id="e9ca8-385">Olá tabela a seguir mostra o valor de saudação que representa cada chave.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-385">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="e9ca8-386">Chave</span><span class="sxs-lookup"><span data-stu-id="e9ca8-386">Key</span></span> | <span data-ttu-id="e9ca8-387">Descrição</span><span class="sxs-lookup"><span data-stu-id="e9ca8-387">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-388">CatalogCoverage</span><span class="sxs-lookup"><span data-stu-id="e9ca8-388">CatalogCoverage</span></span> |<span data-ttu-id="e9ca8-389">Parte do catálogo de saudação pode ser modelado com padrões de uso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-389">What part of hello catalog can be modelled with usage patterns.</span></span> <span data-ttu-id="e9ca8-390">rest Olá itens Olá precisará de recursos com base no conteúdo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-390">hello rest of hello items will need content-based features.</span></span> |
| <span data-ttu-id="e9ca8-391">Mpr</span><span class="sxs-lookup"><span data-stu-id="e9ca8-391">Mpr</span></span> |<span data-ttu-id="e9ca8-392">Classificação de percentual médio de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-392">Mean percentile ranking of hello model.</span></span> <span data-ttu-id="e9ca8-393">Menor é melhor.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-393">Lower is better.</span></span> |
| <span data-ttu-id="e9ca8-394">NumberOfDimensions</span><span class="sxs-lookup"><span data-stu-id="e9ca8-394">NumberOfDimensions</span></span> |<span data-ttu-id="e9ca8-395">Número de dimensões usado pelo algoritmo de fatoração Olá matriz.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-395">Number of dimensions used by hello matrix factorization algorithm.</span></span> |

<span data-ttu-id="e9ca8-396">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-396">OData XML</span></span>

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

### <a name="63----get-model-sample"></a><span data-ttu-id="e9ca8-397">6.3.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-397">6.3.</span></span>    <span data-ttu-id="e9ca8-398">Obter um exemplo de modelo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-398">Get Model Sample</span></span>
<span data-ttu-id="e9ca8-399">Obtém uma amostra de modelo de recomendação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-399">Gets a sample of hello recommendation model.</span></span>

| <span data-ttu-id="e9ca8-400">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-400">HTTP Method</span></span> | <span data-ttu-id="e9ca8-401">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-401">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-402">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-402">GET</span></span> |`<rootURI>/GetModelSample?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="e9ca8-403">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-403">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-404">Com a ID de compilação específica:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-404">With specific build ID:</span></span><br>`<rootURI>/GetModelSample?modelId=%27<model_id>%27&buildId=%27<build_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="e9ca8-405">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-405">Example:</span></span><br>`<rootURI>/GetModelSample?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-406">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-406">Parameter Name</span></span> | <span data-ttu-id="e9ca8-407">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-407">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-408">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-408">modelId</span></span> |<span data-ttu-id="e9ca8-409">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-409">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-410">apiVersion</span></span> |<span data-ttu-id="e9ca8-411">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-411">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-412">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-412">Request Body</span></span> |<span data-ttu-id="e9ca8-413">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-413">NONE</span></span> |

<span data-ttu-id="e9ca8-414">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-414">**Response**:</span></span>

<span data-ttu-id="e9ca8-415">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-415">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-416">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-416">OData XML</span></span>

<span data-ttu-id="e9ca8-417">A resposta é retornada no formato de texto sem formatação:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-417">Response is returned in raw text format:</span></span>

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
50471eec-9aeb-4900-84d7-21567ab18546, If hello Buddha Dated: A Handbook for Finding Love on a Spiritual Path
    cfe922a1-7ca0-4f8d-ad9d-b7cc87bfe0ef, Divine Secrets of hello Ya-Ya Sisterhood: A Novel Rating: 0.5266
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5252
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5244
    e2cbf7ad-0636-4117-8b30-298da6df7077, Animal Dreams Rating: 0.5227
    6c818fd3-5a09-417d-9ab4-7ffe090f0fef, Confessions of an Ugly Stepsister: A Novel Rating: 0.5222
5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club)
    5e97148f-defb-4d74-af2d-80f4763bf531, hello Deep End of hello Ocean (Oprah's Book Club) Rating: 0.537
    5dcbac37-2946-4f2a-a0b3-bbe710f9409a, Up Island: A Novel Rating: 0.5277
    bc5b69db-733b-4346-adde-3927544258f7, Downtown Rating: 0.5275
    31fe5c63-3e5a-48d0-802b-d3b0f989a634, Have a Nice Day: A Tale of Blood and Sweatsocks Rating: 0.5252
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5238
68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived
    68f97068-ae1a-4163-9e94-396b800b743d, Modoc: hello True Story of hello Greatest Elephant That Ever Lived Rating: 0.5379
    6724862e-e4e7-4022-9614-1468d8b902ff, Little House on hello Prairie Rating: 0.5345
    cdedb837-1620-496d-94c4-6ccfed888320, Little House in hello Big Woods Rating: 0.5325
    382164ba-406b-4187-b726-d7a54b9d790d, hello Tao of Pooh Rating: 0.5309
    6a068d6a-bb74-4ba3-b3f2-a956c4f9d1b5, On hello Banks of Plum Creek Rating: 0.5285
37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships
    37ef8e74-e348-44e5-aabc-1d7f9efcb25b, Men Are from Mars, Women Are from Venus: A Practical Guide for Improving Communication and Getting What You Want in Your Relationships Rating: 0.5397
    f2be16d4-5faf-4d32-ab83-7ba74d29261e, Politically Correct Bedtime Stories: Modern Tales for Our Life and Times Rating: 0.5207
    ef732c5c-334b-4d6b-ab82-7255eb7286d0, Honor Among Thieves Rating: 0.5195
    0b209b8c-7cdd-47fd-b940-05c7ff7c60fc, hello Giving Tree Rating: 0.5194
    883b360f-8b42-407f-b977-2f44ad840877, Scary Stories tooTell in hello Dark: Collected from American Folklore (Scary Stories) Rating: 0.5184
ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball
    d008dae9-c73a-40a1-9a9b-96d5cf546f36, hello Gulag Archipelago 1918-1956: An Experiment in Literary Investigation I-II Rating: 0.5416
    ff51b67e-fa8e-4c5e-8f4d-02a928de735d, Men at Work: hello Craft of Baseball Rating: 0.5403
    49dec30e-0adb-411a-b186-48eaabf6f8bc, Fatherland Rating: 0.5394
    cc7964fd-d30f-478e-a425-93ddbdf094ed, Magic hello Gathering: Arena Vol. 1 Rating: 0.5379
    8a1e9f36-97af-4614-bed9-24e3940a05f3, More Sniglets: Any Word That Doesn't Appear in hello Dictionary but Should Rating: 0.5377
12a6d988-be21-4a09-8143-9d5f4261ba16, A Dream of Eagles
    07b10e28-9e7c-4032-90b7-10acab7f2460, Cryptonomicon Rating: 0.5417
    e4cc5e69-3567-43ab-b00f-f0d8d0506870, Hit List Rating: 0.5416
    1f1a34c4-9781-49f5-a3cc-acec3ae3c71d, hello Family Rating: 0.5371
    56daeffe-7d48-43cd-8ef8-7dffd0c103d3, Kilo Class Rating: 0.5366
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5366
df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish
    56d33036-dfda-46b9-8e2a-76cb03921bb0, hello X-Files: Ground Zero Rating: 0.5417
    0780cde8-6529-4e1d-b6c6-082c1b80e596, Twelve Red Herrings Rating: 0.5416
    df87525b-e435-4bd6-8701-4e60ad344e28, Finding Fish Rating: 0.5408
    400fe331-2c35-490c-adbc-b28b4b73d56c, Shall We Tell hello President? Rating: 0.5383
    f86ad7d0-5c03-42b3-aebf-13d44aec8b30, Shades of Grace Rating: 0.5358
de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology
    de1f62a4-89e6-44d2-aaee-992a4bf093f1, hello Map That Changed hello World: William Smith and hello Birth of Modern Geology Rating: 0.5422
    b303538f-e2c6-4a2c-b425-8d21e684fc3e, My Uncle Oswald Rating: 0.5385
    34b84627-48af-4a4c-96c4-b26fb3863f56, Midnight In hello Garden of Good and Evil Rating: 0.5379
    306cbaa7-b1a8-4142-9d55-e11b5018a7a8, hello Street Lawyer Rating: 0.5376
    e53b4baa-8c09-45c4-95c0-b6a26b98770b, Miss Smillas Feeling for Snow Rating: 0.5367

Level 2
---------------
352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony)
    352aaea1-6b12-454d-a3d5-46379d9e4eb2, hello Sinister Pig (Hillerman Tony) Rating: 0.5425
    74c49398-bc10-4af5-a658-a996a1201254, Children of hello Storm (Peters Elizabeth) Rating: 0.5387
    9ba80080-196e-43fd-8025-391d963f77e7, hello Floating Girl Rating: 0.5372
    e68f81d5-7745-4cc7-b943-fedb8fcc2ced, Killer Smile (Scottoline Lisa) Rating: 0.5353
    b2fe511e-5cb9-4a56-b823-2801e63e6a96, Legal Tender Rating: 0.5332
c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days
    0adf981a-b65b-4c11-b36b-78aca2f948a2, hello Perfect Storm: A True Story of Men Against hello Sea Rating: 0.5433
    c65c3995-abf7-4c7b-bb3c-8eb5aa9be7a5, Lake Wobegon days Rating: 0.543
    a00ae6ad-4a7f-4211-9836-75ce8834eb11, Sniglets (Snig'lit: Any Word That Doesn't Appear in hello Dictionary But Should) Rating: 0.5327
    6f6e192e-0d64-49ca-9b63-f09413ea1ee6, Politically Correct Holiday Stories: For an Enlightened Yuletide Season Rating: 0.5307
    798051a8-147d-4d46-b0dc-e836325029e6, AGE OF INNOCENCE (MOVIE TIE-IN) Rating: 0.5301
73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics)
    cba8163f-6536-436b-8130-47b4a43c827f, Trust No One (hello Official Guide toohello X-Files Vol. 2) Rating: 0.5434
    5708e4cb-2492-49c0-94a8-cc413eec5d89, Small Gods (Discworld Novels (Paperback)) Rating: 0.5406
    73f3e25a-e996-4162-9ed8-ff3d34075650, O Pioneers! (Penguin Twentieth-Century Classics) Rating: 0.5403
    d885b0bd-ae4b-452d-bdf2-faa90197dbc9, hello Color of Magic Rating: 0.539
    b133a9c4-4784-4db3-b100-d0d6dffb94d2, hello Truth Is Out There (hello Official Guide toohello X-Files Vol. 1) Rating: 0.5367
271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings
    271700a5-854a-4d5a-8409-6b57a5ee4de4, Fluke: Or I Know Why hello Winged Whale Sings Rating: 0.5445
    2de1c354-90ff-47c5-a0db-1bad7d88ef94, hello Salaryman's Wife (Children of Violence Series) Rating: 0.5329
    d279416e-19c0-43f8-9ec9-a585947879ca, Zen Attitude Rating: 0.5316
    c8f854d7-3de3-4b23-8217-f4f851670fd4, Revenge of hello Cootie Girls: A Robin Hudson Mystery (Robin Hudson Mysteries (Paperback)) Rating: 0.5305
    8ef4751c-7074-409e-a3ac-d49b222fc864, Where hello Wild Things Are Rating: 0.5289
9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God
    9ad1b620-0a7b-4543-8673-66d4c3bcb2f1, Their Eyes Were Watching God Rating: 0.5446
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5389
    65ecbdd1-131c-40c3-a3d6-d86ca281377a, hello God of Small Things Rating: 0.5387
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5355
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5344
5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback))
    5f17d90a-2604-4fe8-8977-1a280b9098b1, One for hello Money (Stephanie Plum Novels (Paperback)) Rating: 0.5446
    57169b2b-9a8a-486b-9aac-1ed98ce57168, Final Appeal Rating: 0.5332
    efcb1bc4-7278-4a8f-b491-befde02070d6, Moment of Truth Rating: 0.5329
    1efa91a2-993b-4c43-9f5c-3454fc12612d, Burn Factor Rating: 0.5309
    24c59962-458a-4ec8-b95d-d694e861919c, At Home in Mitford (hello Mitford Years) Rating: 0.5303
4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl
    4fd48c46-1a20-4c57-bc7f-a02ef123dc52, As Nature Made Him: hello Boy Who Was Raised As a Girl Rating: 0.5449
    cd5f2c03-20cb-43be-a1fb-3b4233e63222, Pigs in Heaven Rating: 0.5329
    19985fdb-d07a-4a25-ae4a-97b9cb61e5d1, Love in hello Time of Cholera (Penguin Great Books of hello 20th Century) Rating: 0.5267
    15689d09-c711-4844-84d8-130a90237b26, Bel Canto Rating: 0.5245
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5235
98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories
    f874b5a3-5d40-4436-94ff-0fa1c090ddf5, hello Sun Also Rises (A Scribner classic) Rating: 0.5451
    98df28ec-41e7-4fca-b77f-8b0d3109085d, Star Trek Memories Rating: 0.5442
    0ce0014a-9a48-4013-a08a-7f2c11877930, H.M.S. Unseen Rating: 0.5421
    15316ca6-1e38-425f-893d-691944a47000, More Scary Stories tooTell In hello Dark Rating: 0.5409
    329d5682-3dc3-4206-8aa2-eef4b1032258, Letters from hello Earth Rating: 0.54
5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover))
    5b9445d5-c072-419c-8d49-6f669bb1b0a9, Daughter of Fortune: A Novel (Oprah's Book Club (Hardcover)) Rating: 0.5462
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5372
    604eb3bd-6026-4f51-bffd-9fb54f180400, Family Pictures: A Novel Rating: 0.5341
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5334
    da45c4d5-aba1-413b-a9bd-50df98b1e1d2, hello Bean Trees Rating: 0.5319
d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven
    d5358189-d70f-4e35-8add-34b83b4942b3, Pigs in Heaven Rating: 0.5491
    ff91a483-1ce5-4b37-a6fd-5ffcf21f8745, hello Poisonwood Bible: A Novel Rating: 0.5401
    c78743bf-7947-4a0c-8db7-8a3bfe69ba70, hello Stone Diaries Rating: 0.5393
    8d06d01d-31cd-4678-b6b1-140a67987ce9, Songs in Ordinary Time (Oprah's Book Club (Paperback)) Rating: 0.5382
    973f8cbd-0846-4f6b-9d28-4dd0d7dc3a19, Pigs in Heaven Rating: 0.5367

</pre>


## <a name="7-model-business-rules"></a><span data-ttu-id="e9ca8-418">7. Regras de negócio do modelo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-418">7. Model Business Rules</span></span>
<span data-ttu-id="e9ca8-419">Estes são os tipos de saudação de regras de suporte:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-419">These are hello types of rules supported:</span></span>

* <span data-ttu-id="e9ca8-420"><strong>Lista de bloqueios</strong> -lista de bloqueios permite que você tooprovide uma lista de itens que você não quer tooreturn nos resultados de recomendação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-420"><strong>BlockList</strong> - BlockList enables you tooprovide a list of items that you do not want tooreturn in hello recommendation results.</span></span> 
* <span data-ttu-id="e9ca8-421"><strong>FeatureBlockList</strong> -lista de bloqueios do recurso permite que você tooblock itens com base nos valores de saudação de seus recursos.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-421"><strong>FeatureBlockList</strong> - Feature BlockList enables you tooblock items based on hello values of its features.</span></span>

<span data-ttu-id="e9ca8-422">*Não envie mais de 1.000 itens em uma única regra de lista de bloqueios ou sua chamada poderá expirar. Se você precisar de mais de 1.000 itens tooblock, você pode fazer várias chamadas de lista de bloqueios.*</span><span class="sxs-lookup"><span data-stu-id="e9ca8-422">*Do not send more than 1000 items in a single blocklist rule or your call may timeout. If you need tooblock more than 1000 items, you can make several blocklist calls.*</span></span>

* <span data-ttu-id="e9ca8-423"><strong>Upsale</strong> -Upsale permite que você tooenforce itens tooreturn nos resultados de recomendação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-423"><strong>Upsale</strong> - Upsale enables you tooenforce items tooreturn in hello recommendation results.</span></span>
* <span data-ttu-id="e9ca8-424"><strong>Lista branca</strong> -lista branca permite você tooonly sugerir recomendações de uma lista de itens.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-424"><strong>WhiteList</strong> - White List enables you tooonly suggest recommendations from a list of items.</span></span>
* <span data-ttu-id="e9ca8-425"><strong>FeatureWhiteList</strong> -lista de permissões de recurso permite que você tooonly recomendável itens que têm valores de recurso específico.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-425"><strong>FeatureWhiteList</strong> - Feature White List enables you tooonly recommend items that have specific feature values.</span></span>
* <span data-ttu-id="e9ca8-426"><strong>PerSeedBlockList</strong> - por habilita semente de bloco que você tooprovide por uma lista de itens que não pode ser retornado como resultados de recomendação de item.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-426"><strong>PerSeedBlockList</strong> - Per Seed Block List enables you tooprovide per item a list of items that cannot be returned as recommendation results.</span></span>

### <a name="71----get-model-rules"></a><span data-ttu-id="e9ca8-427">7.1.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-427">7.1.</span></span>    <span data-ttu-id="e9ca8-428">Obter regras de modelo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-428">Get Model Rules</span></span>
| <span data-ttu-id="e9ca8-429">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-429">HTTP Method</span></span> | <span data-ttu-id="e9ca8-430">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-430">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-431">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-431">GET</span></span> |`<rootURI>/GetModelRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><span data-ttu-id="e9ca8-432">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-432">Example:</span></span><br>`<rootURI>/GetModelRules?modelId=%271cac7b76-def4-41f1-bc81-29b806adb1de%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-433">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-433">Parameter Name</span></span> | <span data-ttu-id="e9ca8-434">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-434">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-435">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-435">modelId</span></span> |<span data-ttu-id="e9ca8-436">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-436">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-437">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-437">apiVersion</span></span> |<span data-ttu-id="e9ca8-438">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-438">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-439">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-439">Request Body</span></span> |<span data-ttu-id="e9ca8-440">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-440">NONE</span></span> |

<span data-ttu-id="e9ca8-441">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-441">**Response**:</span></span>

<span data-ttu-id="e9ca8-442">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-442">HTTP Status code: 200</span></span>

* <span data-ttu-id="e9ca8-443">`feed/entry/content/properties/Id` - Identificador exclusivo desta regra.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-443">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="e9ca8-444">`feed/entry/content/properties/Type`-Tipo de regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-444">`feed/entry/content/properties/Type` - Type of hello rule.</span></span>
* <span data-ttu-id="e9ca8-445">`feed/entry/content/properties/Parameter` - O parâmetro da regra.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-445">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="e9ca8-446">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-446">OData XML</span></span>

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

### <a name="72----add-rule"></a><span data-ttu-id="e9ca8-447">7.2.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-447">7.2.</span></span>    <span data-ttu-id="e9ca8-448">Adicionar regra</span><span class="sxs-lookup"><span data-stu-id="e9ca8-448">Add Rule</span></span>
| <span data-ttu-id="e9ca8-449">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-449">HTTP Method</span></span> | <span data-ttu-id="e9ca8-450">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-450">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-451">POST</span><span class="sxs-lookup"><span data-stu-id="e9ca8-451">POST</span></span> |`<rootURI>/AddRule?apiVersion=%271.0%27` |
| <span data-ttu-id="e9ca8-452">HEADER</span><span class="sxs-lookup"><span data-stu-id="e9ca8-452">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="e9ca8-453">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-453">Parameter Name</span></span> | <span data-ttu-id="e9ca8-454">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-454">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-455">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-455">apiVersion</span></span> |<span data-ttu-id="e9ca8-456">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-456">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-457">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-457">Request Body</span></span> | |

<span data-ttu-id="e9ca8-458"><ins>Sempre que fornecer Ids de Item para regras de negócios, verifique se toouse Olá externo Id do item de hello (Olá a mesma Id que você usou no arquivo de catálogo Olá)</ins></span><span class="sxs-lookup"><span data-stu-id="e9ca8-458"><ins>Whenever providing Item Ids for business rules, make sure toouse hello External Id of hello item (hello same Id that you used in hello catalog file)</ins></span></span><br><span data-ttu-id="e9ca8-459">
<ins>tooadd uma regra de lista de bloqueios:</ins></span><span class="sxs-lookup"><span data-stu-id="e9ca8-459">
<ins>tooadd a BlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>BlockList</Type><Value>{"ItemsToExclude":["2406E770-769C-4189-89DE-1C9283F93A96","3906E110-769C-4189-89DE-1C9283F98888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="e9ca8-460"><ins>
<ins>tooadd uma regra de FeatureBlockList:</ins></span><span class="sxs-lookup"><span data-stu-id="e9ca8-460"><ins>
<ins>tooadd a FeatureBlockList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureBlockList</Type><Value>{"Name":"Movie_category","Values":["Adult","Drama"]}</Value></ApiFilter>`<br><br><span data-ttu-id="e9ca8-461"><ins>tooadd uma regra de Upsale:</ins></span><span class="sxs-lookup"><span data-stu-id="e9ca8-461"><ins> tooadd an Upsale rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>Upsale</Type><Value>{"ItemsToUpsale":["2406E770-769C-4189-89DE-1C9283F93A96"],"NumberOfItemsToUpsale":5}</Value></ApiFilter>`<br><br><span data-ttu-id="e9ca8-462">
<ins>tooadd uma regra de lista de permissões:</ins></span><span class="sxs-lookup"><span data-stu-id="e9ca8-462">
<ins>tooadd a WhiteList rule:</ins></span></span><br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>WhiteList</Type><Value>{"ItemsToInclude":["2406E770-769C-4189-89DE-1C9283F93A96","1116E770-769C-4189-89DE-1C9283F88888"]}</Value></ApiFilter>`<br><br><span data-ttu-id="e9ca8-463"><ins>
<ins>tooadd uma regra de FeatureWhiteList:</ins></span><span class="sxs-lookup"><span data-stu-id="e9ca8-463"><ins>
<ins>tooadd a FeatureWhiteList rule:</ins></span></span><br>
<br>
`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>FeatureWhiteList</Type><Value>{"Name":"Movie_rating","Values":["PG13"]}</Value></ApiFilter>`<br><br><span data-ttu-id="e9ca8-464"><ins>tooadd uma regra de PerSeedBlockList:</ins></span><span class="sxs-lookup"><span data-stu-id="e9ca8-464"><ins> tooadd a PerSeedBlockList rule:</ins></span></span><br>`<ApiFilter xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"><ModelId>24024f7e-b45c-419e-bfa2-dfd947e0d253</ModelId><Type>PerSeedBlockList</Type><Value>{"SeedItems":["9949"],"ItemsToExclude":["9862","8158","8244"]}</Value></ApiFilter>`|

<span data-ttu-id="e9ca8-465">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-465">**Response**:</span></span>

<span data-ttu-id="e9ca8-466">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-466">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-467">Olá API retorna Olá recém-criado regra com seus detalhes.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-467">hello API returns hello newly created rule with its details.</span></span> <span data-ttu-id="e9ca8-468">propriedade de regras Olá pode ser recuperada da saudação caminhos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-468">hello rules property can be retrieved from hello following paths:</span></span>

* <span data-ttu-id="e9ca8-469">`feed/entry/content/properties/Id` - Identificador exclusivo desta regra.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-469">`feed/entry/content/properties/Id` - Unique identifier of this rule.</span></span>
* <span data-ttu-id="e9ca8-470">`feed/entry/content/properties/Type`-Tipo de regra de saudação: lista de bloqueios ou Upsale.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-470">`feed/entry/content/properties/Type` - Type of hello rule: BlockList or Upsale.</span></span>
* <span data-ttu-id="e9ca8-471">`feed/entry/content/properties/Parameter` - O parâmetro da regra.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-471">`feed/entry/content/properties/Parameter` - Rule parameter.</span></span>

<span data-ttu-id="e9ca8-472">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-472">OData XML</span></span>

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

### <a name="73----delete-rule"></a><span data-ttu-id="e9ca8-473">7.3.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-473">7.3.</span></span>    <span data-ttu-id="e9ca8-474">Excluir regra</span><span class="sxs-lookup"><span data-stu-id="e9ca8-474">Delete Rule</span></span>
| <span data-ttu-id="e9ca8-475">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-475">HTTP Method</span></span> | <span data-ttu-id="e9ca8-476">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-476">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-477">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="e9ca8-477">DELETE</span></span> |`<rootURI>/DeleteRule?modelId=%27<model_id>%27&filterId=%27<filter_Id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-478">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-478">Example:</span></span><br>`DeleteRule?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&filterId=%271000011%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-479">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-479">Parameter Name</span></span> | <span data-ttu-id="e9ca8-480">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-480">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-481">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-481">modelId</span></span> |<span data-ttu-id="e9ca8-482">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-482">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-483">filterId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-483">filterId</span></span> |<span data-ttu-id="e9ca8-484">Identificador exclusivo do filtro de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-484">Unique identifier of hello filter</span></span> |
| <span data-ttu-id="e9ca8-485">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-485">apiVersion</span></span> |<span data-ttu-id="e9ca8-486">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-486">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-487">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-487">Request Body</span></span> |<span data-ttu-id="e9ca8-488">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-488">NONE</span></span> |

<span data-ttu-id="e9ca8-489">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-489">**Response**:</span></span>

<span data-ttu-id="e9ca8-490">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-490">HTTP Status code: 200</span></span>

### <a name="74----delete-all-rules"></a><span data-ttu-id="e9ca8-491">7.4.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-491">7.4.</span></span>    <span data-ttu-id="e9ca8-492">Excluir todas as regras</span><span class="sxs-lookup"><span data-stu-id="e9ca8-492">Delete All Rules</span></span>
| <span data-ttu-id="e9ca8-493">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-493">HTTP Method</span></span> | <span data-ttu-id="e9ca8-494">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-495">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="e9ca8-495">DELETE</span></span> |`<rootURI>/DeleteAllRules?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-496">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-496">Example:</span></span><br>`DeleteAllRules?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-497">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-497">Parameter Name</span></span> | <span data-ttu-id="e9ca8-498">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-499">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-499">modelId</span></span> |<span data-ttu-id="e9ca8-500">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-501">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-501">apiVersion</span></span> |<span data-ttu-id="e9ca8-502">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-502">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-503">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-503">Request Body</span></span> |<span data-ttu-id="e9ca8-504">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-504">NONE</span></span> |

<span data-ttu-id="e9ca8-505">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-505">**Response**:</span></span>

<span data-ttu-id="e9ca8-506">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-506">HTTP Status code: 200</span></span>

## <a name="8-catalog"></a><span data-ttu-id="e9ca8-507">8. Catálogo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-507">8. Catalog</span></span>
### <a name="81----import-catalog-data"></a><span data-ttu-id="e9ca8-508">8.1.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-508">8.1.</span></span>    <span data-ttu-id="e9ca8-509">Importar Dados de Catálogo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-509">Import Catalog Data</span></span>
<span data-ttu-id="e9ca8-510">Se você carregar vários catálogo arquivos toohello mesmo modelo com várias chamadas, inserimos somente Olá novos itens de catálogo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-510">If you upload several catalog files toohello same model with several calls, we will insert only hello new catalog items.</span></span> <span data-ttu-id="e9ca8-511">Itens existentes permanecerão com seus valores originais hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-511">Existing items will remain with hello original values.</span></span> <span data-ttu-id="e9ca8-512">Você não pode atualizar os dados do catálogo usando este método.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-512">You cannot update catalog data by using this method.</span></span>

<span data-ttu-id="e9ca8-513">dados de catálogo de saudação devem seguir Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-513">hello catalog data should follow hello following format:</span></span>

* <span data-ttu-id="e9ca8-514">Sem recursos – `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span><span class="sxs-lookup"><span data-stu-id="e9ca8-514">Without features - `<Item Id>,<Item Name>,<Item Category>[,<Description>]`</span></span>
* <span data-ttu-id="e9ca8-515">Com recursos – `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span><span class="sxs-lookup"><span data-stu-id="e9ca8-515">With features - `<Item Id>,<Item Name>,<Item Category>,[<Description>],<Features list>`</span></span>

<span data-ttu-id="e9ca8-516">Observação: o tamanho máximo do arquivo de saudação é 200MB.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-516">Note: hello maximum file size is 200MB.</span></span>

<span data-ttu-id="e9ca8-517">** Detalhes do formato **</span><span class="sxs-lookup"><span data-stu-id="e9ca8-517">** Format details **</span></span>

| <span data-ttu-id="e9ca8-518">Nome</span><span class="sxs-lookup"><span data-stu-id="e9ca8-518">Name</span></span> | <span data-ttu-id="e9ca8-519">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e9ca8-519">Mandatory</span></span> | <span data-ttu-id="e9ca8-520">Tipo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-520">Type</span></span> | <span data-ttu-id="e9ca8-521">Descrição</span><span class="sxs-lookup"><span data-stu-id="e9ca8-521">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e9ca8-522">Id do item</span><span class="sxs-lookup"><span data-stu-id="e9ca8-522">Item Id</span></span> |<span data-ttu-id="e9ca8-523">Sim</span><span class="sxs-lookup"><span data-stu-id="e9ca8-523">Yes</span></span> |<span data-ttu-id="e9ca8-524">[A-z], [a-z], [0-9], [_] &#40;Sublinhado&#41;, [-] &#40;Traço&#41;</span><span class="sxs-lookup"><span data-stu-id="e9ca8-524">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="e9ca8-525">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="e9ca8-525">Max length: 50</span></span> |<span data-ttu-id="e9ca8-526">Identificador exclusivo de um item</span><span class="sxs-lookup"><span data-stu-id="e9ca8-526">Unique identifier of an item.</span></span> |
| <span data-ttu-id="e9ca8-527">Nome do Item</span><span class="sxs-lookup"><span data-stu-id="e9ca8-527">Item Name</span></span> |<span data-ttu-id="e9ca8-528">Sim</span><span class="sxs-lookup"><span data-stu-id="e9ca8-528">Yes</span></span> |<span data-ttu-id="e9ca8-529">Qualquer caractere alfanumérico</span><span class="sxs-lookup"><span data-stu-id="e9ca8-529">Any alphanumeric characters</span></span><br> <span data-ttu-id="e9ca8-530">Comprimento máximo: 255</span><span class="sxs-lookup"><span data-stu-id="e9ca8-530">Max length: 255</span></span> |<span data-ttu-id="e9ca8-531">Nome do item.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-531">Item name.</span></span> |
| <span data-ttu-id="e9ca8-532">Categoria do Item</span><span class="sxs-lookup"><span data-stu-id="e9ca8-532">Item Category</span></span> |<span data-ttu-id="e9ca8-533">Sim</span><span class="sxs-lookup"><span data-stu-id="e9ca8-533">Yes</span></span> |<span data-ttu-id="e9ca8-534">Qualquer caractere alfanumérico</span><span class="sxs-lookup"><span data-stu-id="e9ca8-534">Any alphanumeric characters</span></span> <br> <span data-ttu-id="e9ca8-535">Comprimento máximo: 255</span><span class="sxs-lookup"><span data-stu-id="e9ca8-535">Max length: 255</span></span> |<span data-ttu-id="e9ca8-536">Categoria toowhich este item pertence (por exemplo, culinária manuais, Drama...); pode ser vazio.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-536">Category toowhich this item belongs (e.g. Cooking Books, Drama…); can be empty.</span></span> |
| <span data-ttu-id="e9ca8-537">Descrição</span><span class="sxs-lookup"><span data-stu-id="e9ca8-537">Description</span></span> |<span data-ttu-id="e9ca8-538">Não, a menos que os recursos estejam presentes (mas pode estar vazia)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-538">No, unless features are present (but can be empty)</span></span> |<span data-ttu-id="e9ca8-539">Qualquer caractere alfanumérico</span><span class="sxs-lookup"><span data-stu-id="e9ca8-539">Any alphanumeric characters</span></span> <br> <span data-ttu-id="e9ca8-540">Comprimento máximo: 4000</span><span class="sxs-lookup"><span data-stu-id="e9ca8-540">Max length: 4000</span></span> |<span data-ttu-id="e9ca8-541">Descrição deste item.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-541">Description of this item.</span></span> |
| <span data-ttu-id="e9ca8-542">Lista de recursos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-542">Features list</span></span> |<span data-ttu-id="e9ca8-543">Não</span><span class="sxs-lookup"><span data-stu-id="e9ca8-543">No</span></span> |<span data-ttu-id="e9ca8-544">Qualquer caractere alfanumérico</span><span class="sxs-lookup"><span data-stu-id="e9ca8-544">Any alphanumeric characters</span></span> <br> <span data-ttu-id="e9ca8-545">Comprimento máximo: 4.000; Número máximo de recursos: 20</span><span class="sxs-lookup"><span data-stu-id="e9ca8-545">Max length: 4000; Max number of features:20</span></span> |<span data-ttu-id="e9ca8-546">Lista separada por vírgulas de nome do recurso = valor de recurso que pode ser usado tooenhance recomendação do modelo; consulte [tópicos avançados](#2-advanced-topics) seção.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-546">Comma-separated list of feature name=feature value that can be used tooenhance model recommendation; see [Advanced topics](#2-advanced-topics) section.</span></span> |

| <span data-ttu-id="e9ca8-547">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-547">HTTP Method</span></span> | <span data-ttu-id="e9ca8-548">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-548">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-549">POST</span><span class="sxs-lookup"><span data-stu-id="e9ca8-549">POST</span></span> |`<rootURI>/ImportCatalogFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-550">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-550">Example:</span></span><br>`<rootURI>/ImportCatalogFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27catalog10_small.txt%27&apiVersion=%271.0%27` |
| <span data-ttu-id="e9ca8-551">HEADER</span><span class="sxs-lookup"><span data-stu-id="e9ca8-551">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="e9ca8-552">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-552">Parameter Name</span></span> | <span data-ttu-id="e9ca8-553">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-553">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-554">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-554">modelId</span></span> |<span data-ttu-id="e9ca8-555">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-555">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-556">nome do arquivo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-556">filename</span></span> |<span data-ttu-id="e9ca8-557">Identificador textual do catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-557">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="e9ca8-558">São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-558">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="e9ca8-559">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="e9ca8-559">Max length: 50</span></span> |
| <span data-ttu-id="e9ca8-560">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-560">apiVersion</span></span> |<span data-ttu-id="e9ca8-561">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-561">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-562">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-562">Request Body</span></span> |<span data-ttu-id="e9ca8-563">Exemplo (com recursos):</span><span class="sxs-lookup"><span data-stu-id="e9ca8-563">Example (with features):</span></span><br/><span data-ttu-id="e9ca8-564">2406e770-769c-4189-89de-1c9283f93a96, Clara Callan, catálogo, descrição de catálogo hello, criar = Richard Wright, publicador = Harper Flamingo Canadá, ano = 2001</span><span class="sxs-lookup"><span data-stu-id="e9ca8-564">2406e770-769c-4189-89de-1c9283f93a96,Clara Callan,Book,hello book  description,author=Richard Wright,publisher=Harper Flamingo Canada,year=2001</span></span><br><span data-ttu-id="e9ca8-565">Olá 21bf8088-b6c0-4509-870c-e1c7ac78304a, sala Forgetting: criar um ficção (Byzantium catálogo), catálogo, = Nick Bantock, publicador = Harpercollins, ano = 1997</span><span class="sxs-lookup"><span data-stu-id="e9ca8-565">21bf8088-b6c0-4509-870c-e1c7ac78304a,hello Forgetting Room: A Fiction (Byzantium Book),Book,,author=Nick Bantock,publisher=Harpercollins,year=1997</span></span><br><span data-ttu-id="e9ca8-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span><span class="sxs-lookup"><span data-stu-id="e9ca8-566">3bb5cb44-d143-4bdd-a55c-443964bf4b23,Spadework,Book,,author=Timothy Findley, publisher=HarperFlamingo Canada, year=2001</span></span><br><span data-ttu-id="e9ca8-567">552a1940-21e4-4399-82bb-594b46d7ed54, moderação de feras, livro, descrição de catálogo hello, criar = Magnus Mills, publicador = publicação de Arcade ano = 1998</span><span class="sxs-lookup"><span data-stu-id="e9ca8-567">552a1940-21e4-4399-82bb-594b46d7ed54,Restraint of Beasts,Book,hello book description,author=Magnus Mills, publisher=Arcade Publishing, year=1998</span></span></pre> |

<span data-ttu-id="e9ca8-568">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-568">**Response**:</span></span>

<span data-ttu-id="e9ca8-569">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-569">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-570">Olá API retorna um relatório de importação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-570">hello API returns a report of hello import.</span></span>

* <span data-ttu-id="e9ca8-571">`feed\entry\content\properties\LineCount` – O número de linhas aceitas.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-571">`feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="e9ca8-572">`feed\entry\content\properties\ErrorCount`-Número de linhas que não foram inseridas devido a erro tooan.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-572">`feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>

<span data-ttu-id="e9ca8-573">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-573">OData XML</span></span>

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

### <a name="82----get-catalog"></a><span data-ttu-id="e9ca8-574">8.2.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-574">8.2.</span></span>    <span data-ttu-id="e9ca8-575">Obter catálogo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-575">Get Catalog</span></span>
<span data-ttu-id="e9ca8-576">Recupera todos os itens de catálogo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-576">Retrieves all catalog items.</span></span>
<span data-ttu-id="e9ca8-577">Olá catálogo será recuperado de uma página por vez.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-577">hello catalog will be retrieved one page at a time.</span></span> <span data-ttu-id="e9ca8-578">Se você quiser tooget itens em um índice específico, você pode usar o parâmetro de odata Olá $skip.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-578">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="e9ca8-579">Por exemplo se você quiser itens tooget começando na posição 100, Adicionar parâmetro hello $skip = solicitação de toohello 100.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-579">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="e9ca8-580">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-580">HTTP Method</span></span> | <span data-ttu-id="e9ca8-581">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-581">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-582">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-582">GET</span></span> |`<rootURI>/GetCatalog?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-583">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-583">Example:</span></span><br>`GetCatalog?modelId=%2724024f7e-b45c-419e-bfa2-dfd947e0d253%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-584">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-584">Parameter Name</span></span> | <span data-ttu-id="e9ca8-585">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-585">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-586">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-586">modelId</span></span> |<span data-ttu-id="e9ca8-587">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-587">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-588">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-588">apiVersion</span></span> |<span data-ttu-id="e9ca8-589">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-589">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-590">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-590">Request Body</span></span> |<span data-ttu-id="e9ca8-591">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-591">NONE</span></span> |

<span data-ttu-id="e9ca8-592">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-592">**Response**:</span></span>

<span data-ttu-id="e9ca8-593">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-593">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-594">resposta de saudação inclui uma entrada por item de catálogo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-594">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="e9ca8-595">Cada entrada tem Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-595">Each entry has hello following data:</span></span>

* <span data-ttu-id="e9ca8-596">`feed/entry/content/properties/ExternalId`-ID externa do item de catálogo, Olá fornecido pelo cliente hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-596">`feed/entry/content/properties/ExternalId` - Catalog item external ID, hello one provided by hello customer.</span></span>
* <span data-ttu-id="e9ca8-597">`feed/entry/content/properties/InternalId`-ID interna do item, Olá que gerou recomendações de aprendizado de máquina do Azure do catálogo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-597">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="e9ca8-598">`feed/entry/content/properties/Name` - Nome do item do catálogo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-598">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="e9ca8-599">`feed/entry/content/properties/Category` - Categoria do item do catálogo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-599">`feed/entry/content/properties/Category` - Catalog item category.</span></span>
* <span data-ttu-id="e9ca8-600">`feed/entry/content/properties/Description` - Descrição do item do catálogo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-600">`feed/entry/content/properties/Description` - Catalog item description.</span></span>
* <span data-ttu-id="e9ca8-601">`feed/entry/content/properties/Metadata` - Metadados do item do catálogo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-601">`feed/entry/content/properties/Metadata` - Catalog item metadata.</span></span>

<span data-ttu-id="e9ca8-602">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-602">OData XML</span></span>

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
                <d:Name m:type="Edm.String">hello Forgetting Room: A Fiction (Byzantium Book)</d:Name>
                <d:Category m:type="Edm.String">Book</d:Category>
                <d:Description m:type="Edm.String"></d:Description>
                <d:Metadata m:type="Edm.String"></d:Metadata>
            </m:properties>
        </content>
    </entry>
    </feed>

### <a name="83----get-catalog-items-by-token"></a><span data-ttu-id="e9ca8-603">8.3.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-603">8.3.</span></span>    <span data-ttu-id="e9ca8-604">Obter itens de catálogo por Token</span><span class="sxs-lookup"><span data-stu-id="e9ca8-604">Get Catalog Items by Token</span></span>
| <span data-ttu-id="e9ca8-605">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-605">HTTP Method</span></span> | <span data-ttu-id="e9ca8-606">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-606">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-607">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-607">GET</span></span> |`<rootURI>/GetCatalogItemsByToken?modelId=%27<modelId>%27&token=%27<token>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-608">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-608">Example:</span></span><br>`GetCatalogItemsByToken?modelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&token=%27Cla%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-609">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-609">Parameter Name</span></span> | <span data-ttu-id="e9ca8-610">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-610">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-611">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-611">modelId</span></span> |<span data-ttu-id="e9ca8-612">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-612">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-613">token</span><span class="sxs-lookup"><span data-stu-id="e9ca8-613">token</span></span> |<span data-ttu-id="e9ca8-614">Token de nome do item de catálogo hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-614">Token of hello catalog item’s name.</span></span> <span data-ttu-id="e9ca8-615">Deve conter pelo menos três caracteres.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-615">Should contain at least 3 characters.</span></span> |
| <span data-ttu-id="e9ca8-616">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-616">apiVersion</span></span> |<span data-ttu-id="e9ca8-617">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-617">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-618">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-618">Request Body</span></span> |<span data-ttu-id="e9ca8-619">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-619">NONE</span></span> |

<span data-ttu-id="e9ca8-620">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-620">**Response**:</span></span>

<span data-ttu-id="e9ca8-621">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-621">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-622">resposta de saudação inclui uma entrada por item de catálogo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-622">hello response includes one entry per catalog item.</span></span> <span data-ttu-id="e9ca8-623">Cada entrada tem Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-623">Each entry has hello following data:</span></span>

* <span data-ttu-id="e9ca8-624">`feed/entry/content/properties/InternalId`-ID interna do item, Olá que gerou recomendações de aprendizado de máquina do Azure do catálogo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-624">`feed/entry/content/properties/InternalId` - Catalog item internal ID, hello one that Azure Machine Learning Recommendations has generated.</span></span>
* <span data-ttu-id="e9ca8-625">`feed/entry/content/properties/Name` - Nome do item do catálogo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-625">`feed/entry/content/properties/Name` - Catalog item name.</span></span>
* <span data-ttu-id="e9ca8-626">`feed/entry/content/properties/Rating` - (para uso futuro)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-626">`feed/entry/content/properties/Rating` -  (for future use)</span></span>
* <span data-ttu-id="e9ca8-627">`feed/entry/content/properties/Reasoning` - (para uso futuro)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-627">`feed/entry/content/properties/Reasoning` -  (for future use)</span></span>
* <span data-ttu-id="e9ca8-628">`feed/entry/content/properties/Metadata` - (para uso futuro)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-628">`feed/entry/content/properties/Metadata` -  (for future use)</span></span>
* <span data-ttu-id="e9ca8-629">`feed/entry/content/properties/FormattedRating` - (para uso futuro)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-629">`feed/entry/content/properties/FormattedRating` - (for future use)</span></span>

<span data-ttu-id="e9ca8-630">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-630">OData XML</span></span>

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

## <a name="9-usage-data"></a><span data-ttu-id="e9ca8-631">9. Dados de uso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-631">9. Usage data</span></span>
### <a name="91----import-usage-data"></a><span data-ttu-id="e9ca8-632">9.1.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-632">9.1.</span></span>    <span data-ttu-id="e9ca8-633">Importar Dados de Uso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-633">Import Usage Data</span></span>
#### <a name="911-uploading-file"></a><span data-ttu-id="e9ca8-634">9.1.1.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-634">9.1.1.</span></span> <span data-ttu-id="e9ca8-635">Carregamento de Arquivo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-635">Uploading File</span></span>
<span data-ttu-id="e9ca8-636">Esta seção mostra como os dados de uso tooupload usando um arquivo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-636">This section shows how tooupload usage data by using a file.</span></span> <span data-ttu-id="e9ca8-637">Você pode chamar essa API várias vezes com dados de uso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-637">You can call this API several times with usage data.</span></span> <span data-ttu-id="e9ca8-638">Todos os dados de uso serão salvos para todas as chamadas.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-638">All usage data will be saved for all calls.</span></span>

| <span data-ttu-id="e9ca8-639">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-639">HTTP Method</span></span> | <span data-ttu-id="e9ca8-640">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-640">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-641">POST</span><span class="sxs-lookup"><span data-stu-id="e9ca8-641">POST</span></span> |`<rootURI>/ImportUsageFile?modelId=%27<modelId>%27&filename=%27<fileName>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-642">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-642">Example:</span></span><br>`<rootURI>/ImportUsageFile?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&filename=%27ImplicitMatrix10_Guid_small.txt%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-643">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-643">Parameter Name</span></span> | <span data-ttu-id="e9ca8-644">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-644">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-645">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-645">modelId</span></span> |<span data-ttu-id="e9ca8-646">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-646">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-647">nome do arquivo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-647">filename</span></span> |<span data-ttu-id="e9ca8-648">Identificador textual do catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-648">Textual identifier of hello catalog.</span></span><br><span data-ttu-id="e9ca8-649">São permitidos apenas letras (A-Z, a-z), números (0-9), hifens (-) e sublinhado (_).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-649">Only letters (A-Z, a-z), numbers (0-9), hyphens (-) and underscore (_) are allowed.</span></span><br><span data-ttu-id="e9ca8-650">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="e9ca8-650">Max length: 50</span></span> |
| <span data-ttu-id="e9ca8-651">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-651">apiVersion</span></span> |<span data-ttu-id="e9ca8-652">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-652">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-653">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-653">Request Body</span></span> |<span data-ttu-id="e9ca8-654">Dados de uso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-654">Usage data.</span></span> <span data-ttu-id="e9ca8-655">Formato:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-655">Format:</span></span><br>`<User Id>,<Item Id>[,<Time>,<Event>]`<br><br><table><tr><th><span data-ttu-id="e9ca8-656">Nome</span><span class="sxs-lookup"><span data-stu-id="e9ca8-656">Name</span></span></th><th><span data-ttu-id="e9ca8-657">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e9ca8-657">Mandatory</span></span></th><th><span data-ttu-id="e9ca8-658">Tipo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-658">Type</span></span></th><th><span data-ttu-id="e9ca8-659">Descrição</span><span class="sxs-lookup"><span data-stu-id="e9ca8-659">Description</span></span></th></tr><tr><td><span data-ttu-id="e9ca8-660">Id de usuário</span><span class="sxs-lookup"><span data-stu-id="e9ca8-660">User Id</span></span></td><td><span data-ttu-id="e9ca8-661">Sim</span><span class="sxs-lookup"><span data-stu-id="e9ca8-661">Yes</span></span></td><td><span data-ttu-id="e9ca8-662">[A-z], [a-z], [0-9], [_] &#40;Sublinhado&#41;, [-] &#40;Traço&#41;</span><span class="sxs-lookup"><span data-stu-id="e9ca8-662">[A-z], [a-z], [0-9], [_] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="e9ca8-663">Comprimento máximo: 255</span><span class="sxs-lookup"><span data-stu-id="e9ca8-663">Max length: 255</span></span> </td><td><span data-ttu-id="e9ca8-664">Identificador exclusivo de um usuário.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-664">Unique identifier of a user.</span></span></td></tr><tr><td><span data-ttu-id="e9ca8-665">Id do item</span><span class="sxs-lookup"><span data-stu-id="e9ca8-665">Item Id</span></span></td><td><span data-ttu-id="e9ca8-666">Sim</span><span class="sxs-lookup"><span data-stu-id="e9ca8-666">Yes</span></span></td><td><span data-ttu-id="e9ca8-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span><span class="sxs-lookup"><span data-stu-id="e9ca8-667">[A-z], [a-z], [0-9], [&#95;] &#40;Underscore&#41;, [-] &#40;Dash&#41;</span></span><br> <span data-ttu-id="e9ca8-668">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="e9ca8-668">Max length: 50</span></span></td><td><span data-ttu-id="e9ca8-669">Identificador exclusivo de um item</span><span class="sxs-lookup"><span data-stu-id="e9ca8-669">Unique identifier of an item.</span></span></td></tr><tr><td><span data-ttu-id="e9ca8-670">Hora</span><span class="sxs-lookup"><span data-stu-id="e9ca8-670">Time</span></span></td><td><span data-ttu-id="e9ca8-671">Não</span><span class="sxs-lookup"><span data-stu-id="e9ca8-671">No</span></span></td><td><span data-ttu-id="e9ca8-672">Data no formato: AAAA/MM/DDTHH:MM:SS (por exemplo, 2013/06/20T10:00:00)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-672">Date in format: YYYY/MM/DDTHH:MM:SS (e.g. 2013/06/20T10:00:00)</span></span></td><td><span data-ttu-id="e9ca8-673">Hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-673">Time of data.</span></span></td></tr><tr><td><span data-ttu-id="e9ca8-674">Evento</span><span class="sxs-lookup"><span data-stu-id="e9ca8-674">Event</span></span></td><td><span data-ttu-id="e9ca8-675">Não; se fornecido, também deve colocar a data</span><span class="sxs-lookup"><span data-stu-id="e9ca8-675">No; if supplied then must also put date</span></span></td><td><span data-ttu-id="e9ca8-676">Um dos seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-676">One of hello following:</span></span><br><span data-ttu-id="e9ca8-677">• Clique</span><span class="sxs-lookup"><span data-stu-id="e9ca8-677">• Click</span></span><br><span data-ttu-id="e9ca8-678">• RecommendationClick</span><span class="sxs-lookup"><span data-stu-id="e9ca8-678">• RecommendationClick</span></span><br><span data-ttu-id="e9ca8-679">•    AddShopCart</span><span class="sxs-lookup"><span data-stu-id="e9ca8-679">•    AddShopCart</span></span><br><span data-ttu-id="e9ca8-680">• RemoveShopCart</span><span class="sxs-lookup"><span data-stu-id="e9ca8-680">• RemoveShopCart</span></span><br><span data-ttu-id="e9ca8-681">• Compra</span><span class="sxs-lookup"><span data-stu-id="e9ca8-681">• Purchase</span></span></td><td></td></tr></table><br><span data-ttu-id="e9ca8-682">Tamanho máximo do arquivo: 200 MB</span><span class="sxs-lookup"><span data-stu-id="e9ca8-682">Maximum file size: 200MB</span></span><br><br><span data-ttu-id="e9ca8-683">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-683">Example:</span></span><br><pre>149452,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>6360,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>50321,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>71285,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>224450,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>236645,1b3d95e2-84e4-414c-bb38-be9cf461c347<br>107951,1b3d95e2-84e4-414c-bb38-be9cf461c347</pre> |

<span data-ttu-id="e9ca8-684">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-684">**Response**:</span></span>

<span data-ttu-id="e9ca8-685">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-685">HTTP Status code: 200</span></span>

* <span data-ttu-id="e9ca8-686">`Feed\entry\content\properties\LineCount` – O número de linhas aceitas.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-686">`Feed\entry\content\properties\LineCount` - Number of lines accepted.</span></span>
* <span data-ttu-id="e9ca8-687">`Feed\entry\content\properties\ErrorCount`-Número de linhas que não foram inseridas devido a erro tooan.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-687">`Feed\entry\content\properties\ErrorCount` - Number of lines that were not inserted due tooan error.</span></span>
* <span data-ttu-id="e9ca8-688">`Feed\entry\content\properties\FileId` – Identificador do arquivo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-688">`Feed\entry\content\properties\FileId` - File identifier.</span></span>

<span data-ttu-id="e9ca8-689">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-689">OData XML</span></span>

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


#### <a name="912-using-data-acquisition"></a><span data-ttu-id="e9ca8-690">9.1.2.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-690">9.1.2.</span></span> <span data-ttu-id="e9ca8-691">Usar a Aquisição de Dados</span><span class="sxs-lookup"><span data-stu-id="e9ca8-691">Using Data Acquisition</span></span>
<span data-ttu-id="e9ca8-692">Esta seção mostra como eventos toosend real tempo recomendações tooAzure de aprendizado de máquina, normalmente a partir de seu site.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-692">This section shows how toosend events in real time tooAzure Machine Learning Recommendations, usually from your website.</span></span>

| <span data-ttu-id="e9ca8-693">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-693">HTTP Method</span></span> | <span data-ttu-id="e9ca8-694">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-694">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-695">POST</span><span class="sxs-lookup"><span data-stu-id="e9ca8-695">POST</span></span> |`<rootURI>/AddUsageEvent?apiVersion=%271.0%27` |
| <span data-ttu-id="e9ca8-696">HEADER</span><span class="sxs-lookup"><span data-stu-id="e9ca8-696">HEADER</span></span> |`"Content-Type", "text/xml"` |

| <span data-ttu-id="e9ca8-697">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-697">Parameter Name</span></span> | <span data-ttu-id="e9ca8-698">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-698">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-699">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-699">apiVersion</span></span> |<span data-ttu-id="e9ca8-700">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-700">1.0</span></span> |
| <span data-ttu-id="e9ca8-701">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-701">Request body</span></span> |<span data-ttu-id="e9ca8-702">Entrada de dados de evento para cada evento que você deseja toosend.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-702">Event data entry for each event you want toosend.</span></span> <span data-ttu-id="e9ca8-703">Você deve enviar para a mesma sessão de usuário ou navegador Olá Olá mesmo ID nesse campo de SessionId hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-703">You should send for hello same user or browser session hello same ID in hello SessionId field.</span></span> <span data-ttu-id="e9ca8-704">(Consulte o exemplo de corpo de evento abaixo.)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-704">(See sample of event body below.)</span></span> |

* <span data-ttu-id="e9ca8-705">Exemplo de evento “Click”:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-705">Example for event 'Click':</span></span>
  
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
* <span data-ttu-id="e9ca8-706">Exemplo de evento “RecommendationClick”:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-706">Example for event 'RecommendationClick':</span></span>
  
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
* <span data-ttu-id="e9ca8-707">Exemplo de evento “AddShopCart”:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-707">Example for event 'AddShopCart':</span></span>
  
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
* <span data-ttu-id="e9ca8-708">Exemplo de evento “RemoveShopCart”:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-708">Example for event 'RemoveShopCart':</span></span>
  
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
* <span data-ttu-id="e9ca8-709">Exemplo de evento “Purchase”:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-709">Example for event 'Purchase':</span></span>
  
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
* <span data-ttu-id="e9ca8-710">Exemplo de envio de dois eventos “Click” e “AddShopCart”:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-710">Example sending 2 events, 'Click' and 'AddShopCart':</span></span>
  
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

<span data-ttu-id="e9ca8-711">**Response**: código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-711">**Response**: HTTP Status code: 200</span></span>

### <a name="92----list-model-usage-files"></a><span data-ttu-id="e9ca8-712">9.2.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-712">9.2.</span></span>    <span data-ttu-id="e9ca8-713">Lista dos arquivos de modelo de uso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-713">List Model Usage Files</span></span>
<span data-ttu-id="e9ca8-714">Recupera os metadados de todos os arquivos de uso do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-714">Retrieves metadata of all model usage files.</span></span>
<span data-ttu-id="e9ca8-715">Olá uso arquivos poderão ser recuperados uma página por vez.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-715">hello usage files will be retrieved one page at a time.</span></span> <span data-ttu-id="e9ca8-716">Cada página contém 100 itens.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-716">Each page containes 100 items.</span></span> <span data-ttu-id="e9ca8-717">Se você quiser tooget itens em um índice específico, você pode usar o parâmetro de odata Olá $skip.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-717">If you want tooget items at a particular index, you can use hello $skip odata parameter.</span></span> <span data-ttu-id="e9ca8-718">Por exemplo se você quiser itens tooget começando na posição 100, Adicionar parâmetro hello $skip = solicitação de toohello 100.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-718">For instance if you want tooget items starting at position 100, add hello parameter $skip=100 toohello request.</span></span>

| <span data-ttu-id="e9ca8-719">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-719">HTTP Method</span></span> | <span data-ttu-id="e9ca8-720">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-720">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-721">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-721">GET</span></span> |`<rootURI>/ListModelUsageFiles?forModelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-722">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-722">Example:</span></span><br>`<rootURI>/ListModelUsageFiles?forModelId=%270dbb55fa-7f11-418d-8537-8ff2d9d1d9c6%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-723">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-723">Parameter Name</span></span> | <span data-ttu-id="e9ca8-724">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-724">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-725">forModelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-725">forModelId</span></span> |<span data-ttu-id="e9ca8-726">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-726">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-727">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-727">apiVersion</span></span> |<span data-ttu-id="e9ca8-728">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-728">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-729">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-729">Request Body</span></span> |<span data-ttu-id="e9ca8-730">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-730">NONE</span></span> |

<span data-ttu-id="e9ca8-731">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-731">**Response**:</span></span>

<span data-ttu-id="e9ca8-732">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-732">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-733">resposta de saudação inclui uma entrada por arquivo de uso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-733">hello response includes one entry per usage file.</span></span> <span data-ttu-id="e9ca8-734">Cada entrada tem Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-734">Each entry has hello following data:</span></span>

* <span data-ttu-id="e9ca8-735">`feed\entry\content\properties\Id` - ID do arquivo de uso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-735">`feed\entry\content\properties\Id` - Usage file ID.</span></span>
* <span data-ttu-id="e9ca8-736">`feed\entry\content\properties\Length` - Comprimento de arquivo de uso em MB.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-736">`feed\entry\content\properties\Length` - Usage file length in MB.</span></span>
* <span data-ttu-id="e9ca8-737">`feed\entry\content\properties\DateModified`-Data em que o arquivo de uso de saudação foi criado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-737">`feed\entry\content\properties\DateModified` - Date when hello usage file was created.</span></span>
* <span data-ttu-id="e9ca8-738">`feed\entry\content\properties\UseInModel`-Se o arquivo de uso de saudação é usado no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-738">`feed\entry\content\properties\UseInModel` - Whether hello usage file is used in hello model.</span></span>

<span data-ttu-id="e9ca8-739">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-739">OData XML</span></span>

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

### <a name="93----get-usage-statistics"></a><span data-ttu-id="e9ca8-740">9.3.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-740">9.3.</span></span>    <span data-ttu-id="e9ca8-741">Obter estatísticas de uso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-741">Get Usage Statistics</span></span>
<span data-ttu-id="e9ca8-742">Obter estatísticas de uso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-742">Gets usage statistics.</span></span>

| <span data-ttu-id="e9ca8-743">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-743">HTTP Method</span></span> | <span data-ttu-id="e9ca8-744">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-744">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-745">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-745">GET</span></span> |`<rootURI>/GetUsageStatistics?modelId=%27<modelId>%27& startDate=%27<date>%27&endDate=%27<date>%27&eventTypes=%27<types>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-746">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-746">Example:</span></span><br>`<rootURI>/GetUsageStatistics?modelId=%271d20c34f-dca1-4eac-8e5d-f299e4e4ad66%27&startDate=%272014%2F10%2F17T00%3A00%3A00%27&endDate=%272014%2F11%2F16T00%3A00%3A00%27&eventTypes=%271%2C2%2C3%2C4%2C5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-747">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-747">Parameter Name</span></span> | <span data-ttu-id="e9ca8-748">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-748">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-749">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-749">modelId</span></span> |<span data-ttu-id="e9ca8-750">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-750">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-751">startDate</span><span class="sxs-lookup"><span data-stu-id="e9ca8-751">startDate</span></span> |<span data-ttu-id="e9ca8-752">Data de início.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-752">Start date.</span></span> <span data-ttu-id="e9ca8-753">Formato: aaaa/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="e9ca8-753">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="e9ca8-754">endDate</span><span class="sxs-lookup"><span data-stu-id="e9ca8-754">endDate</span></span> |<span data-ttu-id="e9ca8-755">Data de término.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-755">End date.</span></span> <span data-ttu-id="e9ca8-756">Formato: aaaa/MM/ddTHH:mm:ss</span><span class="sxs-lookup"><span data-stu-id="e9ca8-756">Format: yyyy/MM/ddTHH:mm:ss</span></span> |
| <span data-ttu-id="e9ca8-757">eventTypes</span><span class="sxs-lookup"><span data-stu-id="e9ca8-757">eventTypes</span></span> |<span data-ttu-id="e9ca8-758">Tipos de cadeia de caracteres separada por vírgulas de evento ou null tooget todos os eventos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-758">Comma-separated string of event types or null tooget all events</span></span> |
| <span data-ttu-id="e9ca8-759">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-759">apiVersion</span></span> |<span data-ttu-id="e9ca8-760">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-760">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-761">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-761">Request Body</span></span> |<span data-ttu-id="e9ca8-762">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-762">NONE</span></span> |

<span data-ttu-id="e9ca8-763">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-763">**Response**:</span></span>

<span data-ttu-id="e9ca8-764">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-764">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-765">Uma coleção de elementos de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-765">A collection of key/value elements.</span></span> <span data-ttu-id="e9ca8-766">Cada uma contém a soma de saudação de eventos para um tipo de evento específico, agrupados por hora.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-766">Each one contains hello sum of events for a specific event type grouped by hour.</span></span>

* <span data-ttu-id="e9ca8-767">`feed\entry[i]\content\properties\Key`-Contém o tempo de saudação (agrupado por hora) e o tipo de evento de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-767">`feed\entry[i]\content\properties\Key` - Contains hello time (grouped by hour) and hello event type.</span></span>
* <span data-ttu-id="e9ca8-768">`feed\entry[i]\content\properties\Value` - Contagem de eventos total.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-768">`feed\entry[i]\content\properties\Value` - Total event count.</span></span>

<span data-ttu-id="e9ca8-769">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-769">OData XML</span></span>

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

### <a name="94----get-usage-file-sample"></a><span data-ttu-id="e9ca8-770">9.4.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-770">9.4.</span></span>    <span data-ttu-id="e9ca8-771">Obter um exemplo de arquivo de uso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-771">Get Usage File Sample</span></span>
<span data-ttu-id="e9ca8-772">Recupera Olá primeiro 2KB de conteúdo do arquivo de uso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-772">Retrieves hello first 2KB of usage file content.</span></span>

| <span data-ttu-id="e9ca8-773">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-773">HTTP Method</span></span> | <span data-ttu-id="e9ca8-774">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-774">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-775">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-775">GET</span></span> |`<rootURI>/GetUsageFileSample?modelId=%27<modelId>%27& fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-776">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-776">Example:</span></span><br>`<rootURI>/GetUsageFileSample?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fileId=%274c067b42-e975-4cb2-8c98-a6ab80ed6d63%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-777">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-777">Parameter Name</span></span> | <span data-ttu-id="e9ca8-778">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-778">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-779">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-779">modelId</span></span> |<span data-ttu-id="e9ca8-780">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-780">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-781">fileId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-781">fileId</span></span> |<span data-ttu-id="e9ca8-782">Identificador exclusivo do arquivo de modelo de uso de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-782">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="e9ca8-783">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-783">apiVersion</span></span> |<span data-ttu-id="e9ca8-784">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-784">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-785">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-785">Request Body</span></span> |<span data-ttu-id="e9ca8-786">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-786">NONE</span></span> |

<span data-ttu-id="e9ca8-787">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-787">**Response**:</span></span>

<span data-ttu-id="e9ca8-788">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-788">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-789">A resposta é retornada no formato de texto sem formatação:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-789">Response is returned in raw text format:</span></span>

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


### <a name="95----get-model-usage-file"></a><span data-ttu-id="e9ca8-790">9.5.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-790">9.5.</span></span>    <span data-ttu-id="e9ca8-791">Obtenha o modelo do arquivo de uso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-791">Get Model Usage File</span></span>
<span data-ttu-id="e9ca8-792">Recupera todo o conteúdo do arquivo de uso Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-792">Retrieves hello full content of hello usage file.</span></span>

| <span data-ttu-id="e9ca8-793">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-793">HTTP Method</span></span> | <span data-ttu-id="e9ca8-794">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-794">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-795">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-795">GET</span></span> |`<rootURI>/GetModelUsageFile?mid=%27<modelId>%27& fid=%27<fileId>%27&download=%27<download_value>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-796">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-796">Example:</span></span><br>`<rootURI>/GetModelUsageFile?mid=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&fid=%273126d816-4e80-4248-8339-1ebbdb9d544d%27&download=%271%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-797">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-797">Parameter Name</span></span> | <span data-ttu-id="e9ca8-798">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-798">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-799">mid</span><span class="sxs-lookup"><span data-stu-id="e9ca8-799">mid</span></span> |<span data-ttu-id="e9ca8-800">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-800">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-801">fid</span><span class="sxs-lookup"><span data-stu-id="e9ca8-801">fid</span></span> |<span data-ttu-id="e9ca8-802">Identificador exclusivo do arquivo de modelo de uso de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-802">Unique identifier of hello model usage file</span></span> |
| <span data-ttu-id="e9ca8-803">baixar</span><span class="sxs-lookup"><span data-stu-id="e9ca8-803">download</span></span> |<span data-ttu-id="e9ca8-804">1</span><span class="sxs-lookup"><span data-stu-id="e9ca8-804">1</span></span> |
| <span data-ttu-id="e9ca8-805">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-805">apiVersion</span></span> |<span data-ttu-id="e9ca8-806">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-806">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-807">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-807">Request Body</span></span> |<span data-ttu-id="e9ca8-808">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-808">NONE</span></span> |

<span data-ttu-id="e9ca8-809">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-809">**Response**:</span></span>

<span data-ttu-id="e9ca8-810">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-810">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-811">A resposta é retornada no formato de texto sem formatação:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-811">Response is returned in raw text format:</span></span>

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

### <a name="96----delete-usage-file"></a><span data-ttu-id="e9ca8-812">9.6.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-812">9.6.</span></span>    <span data-ttu-id="e9ca8-813">Excluir o arquivo de uso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-813">Delete Usage File</span></span>
<span data-ttu-id="e9ca8-814">Exclui o arquivo de uso do modelo especificado hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-814">Deletes hello specified model usage file.</span></span>

| <span data-ttu-id="e9ca8-815">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-815">HTTP Method</span></span> | <span data-ttu-id="e9ca8-816">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-816">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-817">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="e9ca8-817">DELETE</span></span> |`<rootURI>/DeleteUsageFile?modelId=%27<modelId>%27&fileId=%27<fileId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-818">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-818">Example:</span></span><br>`<rootURI>/DeleteUsageFile?modelId=%270f86d698-d0f4-4406-a684-d13d22c47a73%27&fileId=%27f2e0b09d-be5c-46b2-9ac2-c7f622e5e1a5%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-819">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-819">Parameter Name</span></span> | <span data-ttu-id="e9ca8-820">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-820">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-821">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-821">modelId</span></span> |<span data-ttu-id="e9ca8-822">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-822">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-823">fileId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-823">fileId</span></span> |<span data-ttu-id="e9ca8-824">Identificador exclusivo da saudação toobe de arquivo excluído</span><span class="sxs-lookup"><span data-stu-id="e9ca8-824">Unique identifier of hello file toobe deleted</span></span> |
| <span data-ttu-id="e9ca8-825">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-825">apiVersion</span></span> |<span data-ttu-id="e9ca8-826">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-826">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-827">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-827">Request Body</span></span> |<span data-ttu-id="e9ca8-828">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-828">NONE</span></span> |

<span data-ttu-id="e9ca8-829">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-829">**Response**:</span></span>

<span data-ttu-id="e9ca8-830">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-830">HTTP Status code: 200</span></span>

### <a name="97----delete-all-usage-files"></a><span data-ttu-id="e9ca8-831">9.7.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-831">9.7.</span></span>    <span data-ttu-id="e9ca8-832">Excluir todos os arquivos de uso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-832">Delete All Usage Files</span></span>
<span data-ttu-id="e9ca8-833">Exclui todos os arquivos de uso do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-833">Deletes all model usage files.</span></span>

| <span data-ttu-id="e9ca8-834">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-834">HTTP Method</span></span> | <span data-ttu-id="e9ca8-835">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-835">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-836">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="e9ca8-836">DELETE</span></span> |`<rootURI>/DeleteAllUsageFiles?modelId=%27<modelId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-837">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-837">Example:</span></span><br>`<rootURI>/DeleteAllUsageFiles?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-838">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-838">Parameter Name</span></span> | <span data-ttu-id="e9ca8-839">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-839">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-840">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-840">modelId</span></span> |<span data-ttu-id="e9ca8-841">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-841">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-842">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-842">apiVersion</span></span> |<span data-ttu-id="e9ca8-843">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-843">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-844">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-844">Request Body</span></span> |<span data-ttu-id="e9ca8-845">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-845">NONE</span></span> |

<span data-ttu-id="e9ca8-846">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-846">**Response**:</span></span>

<span data-ttu-id="e9ca8-847">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-847">HTTP Status code: 200</span></span>

## <a name="10-features"></a><span data-ttu-id="e9ca8-848">10. Recursos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-848">10. Features</span></span>
<span data-ttu-id="e9ca8-849">Esta seção mostra como tooretrieve recurso informações, como recursos de saudação importado e seus valores, sua classificação, e quando esta classificação foi alocada.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-849">This section shows how tooretrieve feature information, such as hello imported features and their values, their rank, and when this rank was allocated.</span></span> <span data-ttu-id="e9ca8-850">Recursos são importados como parte dos dados de catálogo Olá, e, em seguida, sua classificação associada quando é feita uma compilação de classificação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-850">Features are imported as part of hello catalog data, and then their rank is associated when a rank build is done.</span></span>
<span data-ttu-id="e9ca8-851">Classificação de recurso pode alterar o acordo padrão de toohello de dados de uso e tipo de itens.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-851">Feature rank can change according toohello pattern of usage data and type of items.</span></span> <span data-ttu-id="e9ca8-852">Mas para uso consistentes/itens, classificação de saudação deve ter apenas pequenas flutuações.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-852">But for consistent usage/items, hello rank should have only small fluctuations.</span></span>
<span data-ttu-id="e9ca8-853">classificação de saudação de recursos é um número negativo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-853">hello rank of features is a non-negative number.</span></span> <span data-ttu-id="e9ca8-854">Olá número 0 significa que não foi classificado com o recurso hello (acontece se você invocar essa conclusão de toohello anterior de API da compilação de classificação primeiro Olá).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-854">hello  number 0 means that hello feature was not ranked (happens if you invoke this API prior toohello completion of hello first rank build).</span></span> <span data-ttu-id="e9ca8-855">Data de saudação em que a classificação Olá foi atribuída é chamada de atualização de pontuação hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-855">hello date at which hello rank was attributed is called hello score freshness.</span></span>

### <a name="101-get-features-info-for-last-rank-build"></a><span data-ttu-id="e9ca8-856">10.1.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-856">10.1.</span></span> <span data-ttu-id="e9ca8-857">Obter informações de recursos (para a última compilação de classificação)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-857">Get Features Info (For Last Rank Build)</span></span>
<span data-ttu-id="e9ca8-858">Recupera as informações de recurso hello, incluindo classificação, para a última compilação classificação bem-sucedida hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-858">Retrieves hello feature information, including ranking, for hello last successful rank build.</span></span>

| <span data-ttu-id="e9ca8-859">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-859">HTTP Method</span></span> | <span data-ttu-id="e9ca8-860">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-860">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-861">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-861">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-862">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-862">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-863">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-863">Parameter Name</span></span> | <span data-ttu-id="e9ca8-864">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-864">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-865">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-865">modelId</span></span> |<span data-ttu-id="e9ca8-866">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-866">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-867">samplingSize</span><span class="sxs-lookup"><span data-stu-id="e9ca8-867">samplingSize</span></span> |<span data-ttu-id="e9ca8-868">Número de valores tooinclude para cada recurso de acordo com dados de toohello presentes no catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-868">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span> <br/><span data-ttu-id="e9ca8-869">Os valores possíveis são:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-869">Possible values are:</span></span><br> <span data-ttu-id="e9ca8-870">- 1 - Todas as amostras.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-870">-1 - All samples.</span></span> <br><span data-ttu-id="e9ca8-871">0 - Sem amostragem.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-871">0 - No sampling.</span></span> <br><span data-ttu-id="e9ca8-872">N - Retornar N amostras para cada nome de recurso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-872">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="e9ca8-873">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-873">apiVersion</span></span> |<span data-ttu-id="e9ca8-874">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-874">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-875">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-875">Request Body</span></span> |<span data-ttu-id="e9ca8-876">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-876">NONE</span></span> |

<span data-ttu-id="e9ca8-877">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-877">**Response**:</span></span>

<span data-ttu-id="e9ca8-878">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-878">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-879">resposta de saudação contém uma lista de entradas de informações de recurso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-879">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="e9ca8-880">Cada entrada contém:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-880">Each entry contains:</span></span>

* <span data-ttu-id="e9ca8-881">`feed/entry/content/m:properties/d:Name` - Nome do recurso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-881">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="e9ca8-882">`feed/entry/content/m:properties/d:RankUpdateDate`-Data em que Olá classificação foi alocado toothis recurso, também conhecido como</span><span class="sxs-lookup"><span data-stu-id="e9ca8-882">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="e9ca8-883">recurso de atualização de pontuação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-883">score freshness feature.</span></span> <span data-ttu-id="e9ca8-884">Uma data do histórico (“0001-01-01T00:00:00”) significa que nenhuma compilação de classificação foi executada.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-884">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="e9ca8-885">`feed/entry/content/m:properties/d:Rank` - Classificação de recurso (float).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-885">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="e9ca8-886">Uma classificação de 2.0 e superior é considerada um bom recurso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-886">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="e9ca8-887">`feed/entry/content/m:properties/d:SampleValues`-Lista separada por vírgulas dos valores de tamanho de amostragem toohello solicitado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-887">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="e9ca8-888">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-888">OData XML</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
    <title type="text" />
    <subtitle type="text">Get hello features of a model</subtitle>
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

### <a name="102-get-features-info-for-specific-rank-build"></a><span data-ttu-id="e9ca8-889">10.2.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-889">10.2.</span></span> <span data-ttu-id="e9ca8-890">Obter informações de recursos (para uma compilação de classificação específica)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-890">Get Features Info (For Specific Rank Build)</span></span>
<span data-ttu-id="e9ca8-891">Recupera as informações de recurso hello, incluindo Olá de classificação para uma determinada compilação de classificação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-891">Retrieves hello feature information, including hello ranking for a specific rank build.</span></span>

| <span data-ttu-id="e9ca8-892">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-892">HTTP Method</span></span> | <span data-ttu-id="e9ca8-893">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-893">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-894">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-894">GET</span></span> |`<rootURI>/GetModelFeatures?modelId=%27<modelId>%27&samplingSize=%27<samplingSize>%27&rankBuildId=<rankBuildId>&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-895">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-895">Example:</span></span><br>`<rootURI>/GetModelFeatures?modelId=%271c1110f8-7d9f-4c64-a807-4c9c5329993a%27&samplingSize=10%27&rankBuildId=1000551&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-896">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-896">Parameter Name</span></span> | <span data-ttu-id="e9ca8-897">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-897">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-898">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-898">modelId</span></span> |<span data-ttu-id="e9ca8-899">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-899">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-900">samplingSize</span><span class="sxs-lookup"><span data-stu-id="e9ca8-900">samplingSize</span></span> |<span data-ttu-id="e9ca8-901">Número de valores tooinclude para cada recurso de acordo com dados de toohello presentes no catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-901">Number of values tooinclude for each feature according toohello data present in hello catalog.</span></span><br/> <span data-ttu-id="e9ca8-902">Os valores possíveis são:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-902">Possible values are:</span></span><br> <span data-ttu-id="e9ca8-903">- 1 - Todas as amostras.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-903">-1 - All samples.</span></span> <br><span data-ttu-id="e9ca8-904">0 - Sem amostragem.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-904">0 - No sampling.</span></span> <br><span data-ttu-id="e9ca8-905">N - Retornar N amostras para cada nome de recurso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-905">N - Return N samples for each feature name.</span></span> |
| <span data-ttu-id="e9ca8-906">rankBuildId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-906">rankBuildId</span></span> |<span data-ttu-id="e9ca8-907">Identificador exclusivo da compilação classificação hello ou -1 para a última compilação de classificação Olá</span><span class="sxs-lookup"><span data-stu-id="e9ca8-907">Unique identifier of hello rank build or -1 for hello last rank build</span></span> |
| <span data-ttu-id="e9ca8-908">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-908">apiVersion</span></span> |<span data-ttu-id="e9ca8-909">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-909">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-910">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-910">Request Body</span></span> |<span data-ttu-id="e9ca8-911">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-911">NONE</span></span> |

<span data-ttu-id="e9ca8-912">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-912">**Response**:</span></span>

<span data-ttu-id="e9ca8-913">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-913">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-914">resposta de saudação contém uma lista de entradas de informações de recurso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-914">hello response contains a list of feature info entries.</span></span> <span data-ttu-id="e9ca8-915">Cada entrada contém:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-915">Each entry contains:</span></span>

* <span data-ttu-id="e9ca8-916">`feed/entry/content/m:properties/d:Name` - Nome do recurso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-916">`feed/entry/content/m:properties/d:Name` - Feature name.</span></span>
* <span data-ttu-id="e9ca8-917">`feed/entry/content/m:properties/d:RankUpdateDate`-Data em que Olá classificação foi alocado toothis recurso, também conhecido como</span><span class="sxs-lookup"><span data-stu-id="e9ca8-917">`feed/entry/content/m:properties/d:RankUpdateDate` - Date at which hello rank was allocated toothis feature, a.k.a.</span></span> <span data-ttu-id="e9ca8-918">recurso de atualização de pontuação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-918">score freshness feature.</span></span> <span data-ttu-id="e9ca8-919">Uma data do histórico (“0001-01-01T00:00:00”) significa que nenhuma compilação de classificação foi executada.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-919">A historical date ('0001-01-01T00:00:00') means that no rank build was performed.</span></span>
* <span data-ttu-id="e9ca8-920">`feed/entry/content/m:properties/d:Rank` - Classificação de recurso (float).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-920">`feed/entry/content/m:properties/d:Rank` - Feature rank (float).</span></span> <span data-ttu-id="e9ca8-921">Uma classificação de 2.0 e superior é considerada um bom recurso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-921">A rank of 2.0 and up is considered a good feature.</span></span>
* <span data-ttu-id="e9ca8-922">`feed/entry/content/m:properties/d:SampleValues`-Lista separada por vírgulas dos valores de tamanho de amostragem toohello solicitado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-922">`feed/entry/content/m:properties/d:SampleValues` - Comma-separated list of values up toohello sampling size requested.</span></span>

<span data-ttu-id="e9ca8-923">OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-923">OData</span></span>

    <feed xmlns:base="https://api.datamarket.azure.com/amla/recommendations/v3/GetModelFeatures" xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices" xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata" xmlns="http://www.w3.org/2005/Atom">
        <title type="text" />
        <subtitle type="text">Get hello features of a model</subtitle>
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


## <a name="11-build"></a><span data-ttu-id="e9ca8-924">11. Compilação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-924">11. Build</span></span>
  <span data-ttu-id="e9ca8-925">Esta seção explica Olá diferentes APIs relacionadas toobuilds.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-925">This section explains hello different APIs related toobuilds.</span></span> <span data-ttu-id="e9ca8-926">Existem 3 tipos de compilações: uma compilação de recomendação, uma compilação de classificação e uma compilação FBT (frequentemente comprada junto).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-926">There are 3 types of builds: a recommendation build, a rank build and an FBT (frequently bought together) build.</span></span>

<span data-ttu-id="e9ca8-927">finalidade da compilação do Hello recomendação é toogenerate um modelo de recomendação é usado para previsões.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-927">hello recommendation build's purpose is toogenerate a recommendation model used for predictions.</span></span> <span data-ttu-id="e9ca8-928">As previsões (para esse tipo de compilação) vêm em duas versões:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-928">Predictions (for this type of build) come in two flavors:</span></span>

* <span data-ttu-id="e9ca8-929">I2I - também conhecido como</span><span class="sxs-lookup"><span data-stu-id="e9ca8-929">I2I - a.k.a.</span></span> <span data-ttu-id="e9ca8-930">Item recomendações tooItem - receber um item ou uma lista de itens, essa opção poderá prever uma lista de itens que são provavelmente toobe altamente interessante.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-930">Item tooItem recommendations - given an item or a list of items this option will predict a list of items that are likely toobe of high interest.</span></span>
* <span data-ttu-id="e9ca8-931">U2I - também conhecido como</span><span class="sxs-lookup"><span data-stu-id="e9ca8-931">U2I - a.k.a.</span></span> <span data-ttu-id="e9ca8-932">Recomendações de tooItem usuário - recebe uma id de usuário (e, opcionalmente, uma lista de itens) essa opção poderá prever uma lista de itens que são provavelmente toobe altamente interessante para Olá dado usuário (e suas opções adicionais de itens).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-932">User tooItem recommendations - given a user id (and optionally a list of items) this option will predict a list of items that are likely toobe of high interest for hello given user (and its additional choice of items).</span></span> <span data-ttu-id="e9ca8-933">recomendações de U2I Olá baseiam-se no histórico de saudação de itens que foram de interesse do usuário Olá tempo toohello Olá modelo foi criado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-933">hello U2I recommendations are based on hello history of items that were of interest for hello user up toohello time hello model was built.</span></span>

<span data-ttu-id="e9ca8-934">Uma compilação de classificação é uma compilação técnica que permite que você toolearn sobre a utilidade de saudação de seus recursos.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-934">A rank build is a technical build that allows you toolearn about hello usefulness of your features.</span></span> <span data-ttu-id="e9ca8-935">Geralmente, em ordem tooget Olá melhores resultados para um modelo de recomendação que envolvem recursos, você deve levar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-935">Usually, in order tooget hello best result for a recommendation model involving features, you should take hello following steps:</span></span>

* <span data-ttu-id="e9ca8-936">Disparar um build de classificação (a menos que a pontuação Olá dos recursos de estável) e aguarde até que você obtém a pontuação de recurso de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-936">Trigger a rank build (unless hello score of your features is stable) and wait till you get hello feature score.</span></span>
* <span data-ttu-id="e9ca8-937">Recuperar classificação Olá os recursos por chamada hello [obter informações de recursos](#101-get-features-info-for-last-rank-build) API.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-937">Retrieve hello rank of your features by calling hello [Get Features Info](#101-get-features-info-for-last-rank-build) API.</span></span>
* <span data-ttu-id="e9ca8-938">Configure uma compilação de recomendação com hello parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-938">Configure a recommendation build with hello following parameters:</span></span>
  * <span data-ttu-id="e9ca8-939">`useFeatureInModel`-Definir tooTrue.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-939">`useFeatureInModel` - Set tooTrue.</span></span>
  * <span data-ttu-id="e9ca8-940">`ModelingFeatureList`-Lista de separada por vírgulas de tooa conjunto de recursos com uma pontuação de 2.0 ou mais (de acordo com classificações toohello recuperado na etapa anterior Olá).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-940">`ModelingFeatureList` - Set tooa comma-separated list of features with a score of 2.0 or more (according toohello ranks you retrieved in hello previous step).</span></span>
  * <span data-ttu-id="e9ca8-941">`AllowColdItemPlacement`-Definir tooTrue.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-941">`AllowColdItemPlacement` - Set tooTrue.</span></span>
  * <span data-ttu-id="e9ca8-942">Opcionalmente, você pode definir `EnableFeatureCorrelation` tooTrue e `ReasoningFeatureList` toohello lista de recursos que você deseja toouse para obter explicações (geralmente Olá mesma lista de recursos usada na modelagem ou uma sublista).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-942">Optionally you can set `EnableFeatureCorrelation` tooTrue and `ReasoningFeatureList` toohello list of features you want toouse for explanations (usually hello same list of features used in modelling or a sublist).</span></span>
* <span data-ttu-id="e9ca8-943">Disparar Olá recomendação compilação com parâmetros de saudação configurado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-943">Trigger hello recommendation build with hello configured parameters.</span></span>

<span data-ttu-id="e9ca8-944">Observação: Se você não configurar os parâmetros (por exemplo, invocar a compilação de recomendação de saudação sem parâmetros) ou você não desabilitar explicitamente uso Olá de recursos (por exemplo, `UseFeatureInModel` definir tooFalse), sistema Olá definirá os parâmetros relacionados ao recurso de saudação toohello explicado acima de valores, caso exista uma compilação de classificação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-944">Note: If you do not configure any parameters (e.g. invoke hello recommendation build without parameters) or you do not explicitly disable hello usage of features (e.g. `UseFeatureInModel` set tooFalse), hello system will set up hello feature-related parameters toohello explained values above in case a rank build exists.</span></span>

<span data-ttu-id="e9ca8-945">Não há nenhuma restrição sobre como executar uma compilação de classificação e uma recomendação de compilação simultaneamente para Olá mesmo modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-945">There is no restriction on running a rank build and a recommendation build concurrently for hello same model.</span></span> <span data-ttu-id="e9ca8-946">No entanto, você não pode executar duas versões do mesmo tipo no mesmo modelo em paralelo de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-946">Nevertheless, you cannot run two builds of hello same type on hello same model in parallel.</span></span>

<span data-ttu-id="e9ca8-947">Uma compilação FBT (Frequentemente Comprado Juntos) é outro algoritmo de recomendações chamado por vezes de recomendador "conservador", o que é bom para os catálogos não homogêneos por natureza (homogêneas: livros, filmes, alguns alimentos, moda; não homogêneo: computadores e dispositivos, entre domínios, altamente diversificados).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-947">An FBT (Frequently bought together) build is yet another recommendations algorithm called sometimes "conservative" recommender, which is good for catalogs that are not homogeneous in nature (homogeneous: books, movies, some food, fashion; non-homogeneous: computer and devices, cross-domain, highly diverse).</span></span>

<span data-ttu-id="e9ca8-948">Observação: se os arquivos de uso que você carregou hello contêm campo opcional de hello "tipo de evento", em seguida, para FBT modelagem somente eventos de "Comprar" será usado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-948">Note: if hello usage files that you uploaded contain hello optional field "event type" then for FBT modelling only "Purchase" events will be used.</span></span> <span data-ttu-id="e9ca8-949">Se nenhum tipo de evento for fornecido, todos os eventos serão considerados como compra.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-949">If no event type is provided all events will be considered as purchase.</span></span>

#### <a name="111-build-parameters"></a><span data-ttu-id="e9ca8-950">11.1 Parâmetros de compilação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-950">11.1 Build parameters</span></span>
<span data-ttu-id="e9ca8-951">Cada tipo de compilação pode ser configurado por meio de um conjunto de parâmetros (descritos abaixo).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-951">Each build type can be configured via a set of parameters (depicted below).</span></span> <span data-ttu-id="e9ca8-952">Se você não configurar parâmetros de saudação, o sistema Olá automaticamente atributo valores de parâmetros toohello toohello informações presentes no tempo de saudação disparar um build de acordo com.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-952">If you don't configure hello parameters, hello system will automatically attribute values toohello parameters according toohello information present at hello time you trigger a build.</span></span>

##### <a name="1111-usage-condenser"></a><span data-ttu-id="e9ca8-953">11.1.1.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-953">11.1.1.</span></span> <span data-ttu-id="e9ca8-954">Condensador de uso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-954">Usage condenser</span></span>
<span data-ttu-id="e9ca8-955">Os usuários ou itens com poucos pontos de uso podem conter mais ruído que informações.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-955">Users or items with few usage points might contain more noise than information.</span></span> <span data-ttu-id="e9ca8-956">sistema de saudação tentativas toopredict Olá o número mínimo de pontos de uso por usuário/item toobe usada em um modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-956">hello system attempts toopredict hello minimal number of usage points per user/item toobe used in a model.</span></span> <span data-ttu-id="e9ca8-957">Esse número será dentro do intervalo de saudação definido pelo hello ItemCutoffLowerBound e parâmetros de ItemCutoffUpperBound itens e o intervalo de saudação definido pelo hello UserCutOffLowerBound e UserCutoffUpperBound parâmetros para os usuários.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-957">This number will be within hello range defined by hello ItemCutoffLowerBound and ItemCutoffUpperBound parameters for items, and hello range defined by hello UserCutOffLowerBound and UserCutoffUpperBound parameters for users.</span></span> <span data-ttu-id="e9ca8-958">efeito de condensador Olá itens ou usuários pode ser minimizado definindo pelo menos uma das Olá correspondente toozero de limites.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-958">hello condenser effect on items or users can be minimized by setting at least one of hello corresponding bounds toozero.</span></span>

##### <a name="1112-rank-build-parameters"></a><span data-ttu-id="e9ca8-959">11.1.2.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-959">11.1.2.</span></span> <span data-ttu-id="e9ca8-960">Parâmetros de compilação de classificação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-960">Rank build parameters</span></span>
<span data-ttu-id="e9ca8-961">Olá a tabela abaixo descreve os parâmetros de construção Olá para um build de classificação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-961">hello table below depicts hello build parameters for a rank build.</span></span>

| <span data-ttu-id="e9ca8-962">Chave</span><span class="sxs-lookup"><span data-stu-id="e9ca8-962">Key</span></span> | <span data-ttu-id="e9ca8-963">Descrição</span><span class="sxs-lookup"><span data-stu-id="e9ca8-963">Description</span></span> | <span data-ttu-id="e9ca8-964">Tipo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-964">Type</span></span> | <span data-ttu-id="e9ca8-965">Valor Válido</span><span class="sxs-lookup"><span data-stu-id="e9ca8-965">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e9ca8-966">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="e9ca8-966">NumberOfModelIterations</span></span> |<span data-ttu-id="e9ca8-967">número de saudação de iterações modelo Olá executa é refletido pela Olá tempo e hello precisão do modelo de computação geral.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-967">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="e9ca8-968">número mais alto de Olá Olá, você terá maior precisão do hello, mas Olá computação tempo irá demorar mais.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-968">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="e9ca8-969">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-969">Integer</span></span> |<span data-ttu-id="e9ca8-970">10-50</span><span class="sxs-lookup"><span data-stu-id="e9ca8-970">10-50</span></span> |
| <span data-ttu-id="e9ca8-971">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="e9ca8-971">NumberOfModelDimensions</span></span> |<span data-ttu-id="e9ca8-972">número de saudação de dimensões se relaciona toohello número do modelo de saudação 'recursos' tentará toofind dentro de seus dados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-972">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="e9ca8-973">Aumentar o número de saudação de dimensões permitirá ajustar melhor os resultados de saudação em clusters menores.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-973">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="e9ca8-974">No entanto, muitas dimensões impedirá modelo Olá localização de correlações entre itens.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-974">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="e9ca8-975">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-975">Integer</span></span> |<span data-ttu-id="e9ca8-976">10-40</span><span class="sxs-lookup"><span data-stu-id="e9ca8-976">10-40</span></span> |
| <span data-ttu-id="e9ca8-977">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="e9ca8-977">ItemCutOffLowerBound</span></span> |<span data-ttu-id="e9ca8-978">Define Olá item inferior para condensador hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-978">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="e9ca8-979">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-979">See usage condenser above.</span></span> |<span data-ttu-id="e9ca8-980">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-980">Integer</span></span> |<span data-ttu-id="e9ca8-981">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-981">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="e9ca8-982">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="e9ca8-982">ItemCutOffUpperBound</span></span> |<span data-ttu-id="e9ca8-983">Define Olá item limite superior condensador hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-983">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="e9ca8-984">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-984">See usage condenser above.</span></span> |<span data-ttu-id="e9ca8-985">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-985">Integer</span></span> |<span data-ttu-id="e9ca8-986">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-986">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="e9ca8-987">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="e9ca8-987">UserCutOffLowerBound</span></span> |<span data-ttu-id="e9ca8-988">Define Olá usuário inferior para condensador hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-988">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="e9ca8-989">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-989">See usage condenser above.</span></span> |<span data-ttu-id="e9ca8-990">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-990">Integer</span></span> |<span data-ttu-id="e9ca8-991">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-991">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="e9ca8-992">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="e9ca8-992">UserCutOffUpperBound</span></span> |<span data-ttu-id="e9ca8-993">Define Olá usuário limite superior condensador hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-993">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="e9ca8-994">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-994">See usage condenser above.</span></span> |<span data-ttu-id="e9ca8-995">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-995">Integer</span></span> |<span data-ttu-id="e9ca8-996">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-996">2 or more (0 disable condenser)</span></span> |

##### <a name="1113-recommendation-build-parameters"></a><span data-ttu-id="e9ca8-997">11.1.3.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-997">11.1.3.</span></span> <span data-ttu-id="e9ca8-998">Parâmetros de compilação de recomendação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-998">Recommendation build parameters</span></span>
<span data-ttu-id="e9ca8-999">Olá a tabela abaixo descreve os parâmetros de construção Olá para compilação de recomendação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-999">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="e9ca8-1000">Chave</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1000">Key</span></span> | <span data-ttu-id="e9ca8-1001">Descrição</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1001">Description</span></span> | <span data-ttu-id="e9ca8-1002">Tipo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1002">Type</span></span> | <span data-ttu-id="e9ca8-1003">Valor Válido</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1003">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e9ca8-1004">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1004">NumberOfModelIterations</span></span> |<span data-ttu-id="e9ca8-1005">número de saudação de iterações modelo Olá executa é refletido pela Olá tempo e hello precisão do modelo de computação geral.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1005">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="e9ca8-1006">número mais alto de Olá Olá, você terá maior precisão do hello, mas Olá computação tempo irá demorar mais.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1006">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="e9ca8-1007">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1007">Integer</span></span> |<span data-ttu-id="e9ca8-1008">10-50</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1008">10-50</span></span> |
| <span data-ttu-id="e9ca8-1009">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1009">NumberOfModelDimensions</span></span> |<span data-ttu-id="e9ca8-1010">número de saudação de dimensões se relaciona toohello número do modelo de saudação 'recursos' tentará toofind dentro de seus dados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1010">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="e9ca8-1011">Aumentar o número de saudação de dimensões permitirá ajustar melhor os resultados de saudação em clusters menores.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1011">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="e9ca8-1012">No entanto, muitas dimensões impedirá modelo Olá localização de correlações entre itens.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1012">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="e9ca8-1013">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1013">Integer</span></span> |<span data-ttu-id="e9ca8-1014">10-40</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1014">10-40</span></span> |
| <span data-ttu-id="e9ca8-1015">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1015">ItemCutOffLowerBound</span></span> |<span data-ttu-id="e9ca8-1016">Define Olá item inferior para condensador hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1016">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="e9ca8-1017">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1017">See usage condenser above.</span></span> |<span data-ttu-id="e9ca8-1018">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1018">Integer</span></span> |<span data-ttu-id="e9ca8-1019">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1019">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="e9ca8-1020">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1020">ItemCutOffUpperBound</span></span> |<span data-ttu-id="e9ca8-1021">Define Olá item limite superior condensador hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1021">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="e9ca8-1022">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1022">See usage condenser above.</span></span> |<span data-ttu-id="e9ca8-1023">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1023">Integer</span></span> |<span data-ttu-id="e9ca8-1024">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1024">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="e9ca8-1025">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1025">UserCutOffLowerBound</span></span> |<span data-ttu-id="e9ca8-1026">Define Olá usuário inferior para condensador hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1026">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="e9ca8-1027">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1027">See usage condenser above.</span></span> |<span data-ttu-id="e9ca8-1028">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1028">Integer</span></span> |<span data-ttu-id="e9ca8-1029">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1029">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="e9ca8-1030">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1030">UserCutOffUpperBound</span></span> |<span data-ttu-id="e9ca8-1031">Define Olá usuário limite superior condensador hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1031">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="e9ca8-1032">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1032">See usage condenser above.</span></span> |<span data-ttu-id="e9ca8-1033">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1033">Integer</span></span> |<span data-ttu-id="e9ca8-1034">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1034">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="e9ca8-1035">Descrição</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1035">Description</span></span> |<span data-ttu-id="e9ca8-1036">Descrição da compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1036">Build description.</span></span> |<span data-ttu-id="e9ca8-1037">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1037">String</span></span> |<span data-ttu-id="e9ca8-1038">Qualquer texto, máximo de 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1038">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="e9ca8-1039">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1039">EnableModelingInsights</span></span> |<span data-ttu-id="e9ca8-1040">Permite que você toocompute métricas no modelo de recomendação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1040">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="e9ca8-1041">Booliano</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1041">Boolean</span></span> |<span data-ttu-id="e9ca8-1042">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1042">True/False</span></span> |
| <span data-ttu-id="e9ca8-1043">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1043">UseFeaturesInModel</span></span> |<span data-ttu-id="e9ca8-1044">Indica se os recursos podem ser usados no modelo de recomendação de saudação do pedido tooenhance.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1044">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="e9ca8-1045">Booliano</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1045">Boolean</span></span> |<span data-ttu-id="e9ca8-1046">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1046">True/False</span></span> |
| <span data-ttu-id="e9ca8-1047">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1047">ModelingFeatureList</span></span> |<span data-ttu-id="e9ca8-1048">Lista separada por vírgulas de toobe de nomes de recurso usado na compilação de recomendação hello, na recomendação de saudação do tooenhance de ordem.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1048">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="e9ca8-1049">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1049">String</span></span> |<span data-ttu-id="e9ca8-1050">Nomes de recurso, o too512 caracteres</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1050">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="e9ca8-1051">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1051">AllowColdItemPlacement</span></span> |<span data-ttu-id="e9ca8-1052">Indica se a recomendação de saudação também enviar por push itens frios por meio de similaridade de recurso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1052">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="e9ca8-1053">Booliano</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1053">Boolean</span></span> |<span data-ttu-id="e9ca8-1054">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1054">True/False</span></span> |
| <span data-ttu-id="e9ca8-1055">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1055">EnableFeatureCorrelation</span></span> |<span data-ttu-id="e9ca8-1056">Indica se os recursos podem ser usados no raciocínio.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1056">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="e9ca8-1057">Booliano</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1057">Boolean</span></span> |<span data-ttu-id="e9ca8-1058">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1058">True/False</span></span> |
| <span data-ttu-id="e9ca8-1059">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1059">ReasoningFeatureList</span></span> |<span data-ttu-id="e9ca8-1060">Lista separada por vírgulas de toobe de nomes de recurso usado para raciocínio sentenças (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1060">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="e9ca8-1061">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1061">String</span></span> |<span data-ttu-id="e9ca8-1062">Nomes de recurso, o too512 caracteres</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1062">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="e9ca8-1063">EnableU2I</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1063">EnableU2I</span></span> |<span data-ttu-id="e9ca8-1064">Permitir recomendação Olá personalizado conhecido como</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1064">Allow hello personalized recommendation a.k.a.</span></span> <span data-ttu-id="e9ca8-1065">U2I (recomendações de tooitem do usuário).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1065">U2I (user tooitem recommendations).</span></span> |<span data-ttu-id="e9ca8-1066">Booliano</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1066">Boolean</span></span> |<span data-ttu-id="e9ca8-1067">True/False (verdadeiro por padrão)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1067">True/False (default true)</span></span> |

##### <a name="1114-fbt-build-parameters"></a><span data-ttu-id="e9ca8-1068">11.1.4.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1068">11.1.4.</span></span> <span data-ttu-id="e9ca8-1069">Parâmetros de compilação FBT</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1069">FBT build parameters</span></span>
<span data-ttu-id="e9ca8-1070">Olá a tabela abaixo descreve os parâmetros de construção Olá para compilação de recomendação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1070">hello table below depicts hello build parameters for recommendation build.</span></span>

| <span data-ttu-id="e9ca8-1071">Chave</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1071">Key</span></span> | <span data-ttu-id="e9ca8-1072">Descrição</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1072">Description</span></span> | <span data-ttu-id="e9ca8-1073">Tipo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1073">Type</span></span> | <span data-ttu-id="e9ca8-1074">Valor Válido (Padrão)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1074">Valid Value (Default)</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e9ca8-1075">FbtSupportThreshold</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1075">FbtSupportThreshold</span></span> |<span data-ttu-id="e9ca8-1076">Como o modelo Olá conservadora é.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1076">How conservative hello model is.</span></span> <span data-ttu-id="e9ca8-1077">Número de ocorrências colegas de itens toobe considerados para modelagem.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1077">Number of co-occurrences of items toobe considered for modeling.</span></span> |<span data-ttu-id="e9ca8-1078">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1078">Integer</span></span> |<span data-ttu-id="e9ca8-1079">3-50 (6)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1079">3-50 (6)</span></span> |
| <span data-ttu-id="e9ca8-1080">FbtMaxItemSetSize</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1080">FbtMaxItemSetSize</span></span> |<span data-ttu-id="e9ca8-1081">Limites Olá número de itens em um conjunto frequente.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1081">Bounds hello number of items in a frequent set.</span></span> |<span data-ttu-id="e9ca8-1082">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1082">Integer</span></span> |<span data-ttu-id="e9ca8-1083">2-3 (2)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1083">2-3 (2)</span></span> |
| <span data-ttu-id="e9ca8-1084">FbtMinimalScore</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1084">FbtMinimalScore</span></span> |<span data-ttu-id="e9ca8-1085">Pontuação mínima que um conjunto frequente deve ter em ordem toobe incluído no hello retornados resultados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1085">Minimal score that a frequent set should have in order toobe included in hello returned results.</span></span> <span data-ttu-id="e9ca8-1086">Olá superior hello melhor.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1086">hello higher hello better.</span></span> |<span data-ttu-id="e9ca8-1087">Duplo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1087">Double</span></span> |<span data-ttu-id="e9ca8-1088">0 e acima (0)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1088">0 and above (0)</span></span> |
| <span data-ttu-id="e9ca8-1089">FbtSimilarityFunction</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1089">FbtSimilarityFunction</span></span> |<span data-ttu-id="e9ca8-1090">Define Olá toobe de função de similaridade usado pela compilação hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1090">Defines hello similarity function toobe used by hello build.</span></span> <span data-ttu-id="e9ca8-1091">Comparação de precisão favorece serendipity, ocorrência colegas favorece previsibilidade e Jaccard é um bom meio-termo entre Olá dois.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1091">Lift favors serendipity, Co-occurrence favors predictability, and Jaccard is a nice compromise between hello two.</span></span> |<span data-ttu-id="e9ca8-1092">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1092">String</span></span> |<span data-ttu-id="e9ca8-1093">cooccurrence, lift, jaccard (lift)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1093">cooccurrence, lift, jaccard (lift)</span></span> |

### <a name="112-trigger-a-recommendation-build"></a><span data-ttu-id="e9ca8-1094">11.2.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1094">11.2.</span></span> <span data-ttu-id="e9ca8-1095">Disparar uma Compilação de Recomendação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1095">Trigger a Recommendation Build</span></span>
  <span data-ttu-id="e9ca8-1096">Por padrão, essa API vai disparar uma compilação de modelo de recomendação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1096">By default this API will trigger a recommendation model build.</span></span> <span data-ttu-id="e9ca8-1097">tootrigger uma classificação de compilação (em ordem tooscore de recursos), variante de API de compilação Olá com parâmetro de tipo de compilação deve ser usado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1097">tootrigger a rank build (in order tooscore  features), hello build API variant with build type parameter should be used.</span></span>

| <span data-ttu-id="e9ca8-1098">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1098">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1099">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1099">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1100">POST</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1100">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1101">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1101">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&apiVersion=%271.0%27` |
| <span data-ttu-id="e9ca8-1102">HEADER</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1102">HEADER</span></span> |<span data-ttu-id="e9ca8-1103">`"Content-Type", "text/xml"` (Se estiver enviando o Corpo da solicitação)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1103">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="e9ca8-1104">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1104">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1105">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1105">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1106">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1106">modelId</span></span> |<span data-ttu-id="e9ca8-1107">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1107">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-1108">userDescription</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1108">userDescription</span></span> |<span data-ttu-id="e9ca8-1109">Identificador textual do catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1109">Textual identifier of hello catalog.</span></span> <span data-ttu-id="e9ca8-1110">Observe que se você usar espaços você deve codificá-los com 20%.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1110">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="e9ca8-1111">Consulte o exemplo acima.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1111">See example above.</span></span><br><span data-ttu-id="e9ca8-1112">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1112">Max length: 50</span></span> |
| <span data-ttu-id="e9ca8-1113">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1113">apiVersion</span></span> |<span data-ttu-id="e9ca8-1114">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1114">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-1115">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1115">Request Body</span></span> |<span data-ttu-id="e9ca8-1116">Se deixado em branco compilação Olá será executada com parâmetros de compilação saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1116">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="e9ca8-1117">Se você quiser parâmetros de compilação tooset hello, envie parâmetros de saudação como XML no corpo de saudação como Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1117">If you want tooset hello build parameters, send hello parameters as XML into hello body as in hello following sample.</span></span> <span data-ttu-id="e9ca8-1118">(Consulte a seção de hello "parâmetros de compilação" para obter uma explicação dos parâmetros de saudação).`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1118">(See hello "Build parameters" section for an explanation of hello parameters.)`<NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance><EnableModelingInsights>true</EnableModelingInsights><UseFeaturesInModel>false</UseFeaturesInModel><ModelingFeatureList>feature_name_1,feature_name_2,...</ModelingFeatureList><AllowColdItemPlacement>false</AllowColdItemPlacement><EnableFeatureCorrelation>false</EnableFeatureCorrelation><ReasoningFeatureList>feature_name_a,feature_name_b,...</ReasoningFeatureList></BuildParametersList>`</span></span> |

<span data-ttu-id="e9ca8-1119">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1119">**Response**:</span></span>

<span data-ttu-id="e9ca8-1120">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1120">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-1121">Esta é uma API assíncrona.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1121">This is an asynchronous API.</span></span> <span data-ttu-id="e9ca8-1122">Você receberá uma ID de compilação como uma resposta.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1122">You will get a build ID as a response.</span></span> <span data-ttu-id="e9ca8-1123">tooknow quando a compilação Olá terminou, você deve chamar hello "Obter compilações Status de um modelo de" API e localize essa compilação ID na resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1123">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="e9ca8-1124">Observe que uma compilação pode levar de toohours minutos dependendo do tamanho de saudação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1124">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="e9ca8-1125">Você não pode consumir recomendações até Olá compilar termina.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1125">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="e9ca8-1126">Status de compilação válidos:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1126">Valid build status:</span></span>

* <span data-ttu-id="e9ca8-1127">Criar - A solicitação de compilação foi criada.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1127">Create - Build request was created.</span></span>
* <span data-ttu-id="e9ca8-1128">Em fila - A solicitação de compilação foi enviada e será enfileirada.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1128">Queued - Build request was sent and it is queued.</span></span>
* <span data-ttu-id="e9ca8-1129">Compilando - A compilação está em andamento.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1129">Building - Build is in progress.</span></span>
* <span data-ttu-id="e9ca8-1130">Sucesso - A compilação concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1130">Success - Build ended successfully.</span></span>
* <span data-ttu-id="e9ca8-1131">Erro - A compilação foi concluída com uma falha.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1131">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="e9ca8-1132">Cancelado - A compilação foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1132">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="e9ca8-1133">Cancelando - foi enviada uma solicitação de cancelamento para compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1133">Cancelling - A cancel request for hello build was sent.</span></span>

<span data-ttu-id="e9ca8-1134">Observe que compilação Olá que ID pode ser encontrada em Olá que caminho a seguir:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1134">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="e9ca8-1135">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1135">OData XML</span></span>

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

### <a name="113-trigger-build-recommendation-rank-or-fbt"></a><span data-ttu-id="e9ca8-1136">11.3.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1136">11.3.</span></span> <span data-ttu-id="e9ca8-1137">Disparar Compilação (Recomendação, Classificação ou FBT)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1137">Trigger Build (Recommendation, Rank or FBT)</span></span>
| <span data-ttu-id="e9ca8-1138">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1138">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1139">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1139">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1140">POST</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1140">POST</span></span> |`<rootURI>/BuildModel?modelId=%27<modelId>%27&userDescription=%27<description>%27&buildType=%27<buildType>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1141">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1141">Example:</span></span><br>`<rootURI>/BuildModel?modelId=%27a658c626-2baa-43a7-ac98-f6ee26120a12%27&userDescription=%27First%20build%27&buildType=%27Ranking%27&apiVersion=%271.0%27` |
| <span data-ttu-id="e9ca8-1142">HEADER</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1142">HEADER</span></span> |<span data-ttu-id="e9ca8-1143">`"Content-Type", "text/xml"` (Se estiver enviando o Corpo da solicitação)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1143">`"Content-Type", "text/xml"` (If sending Request Body)</span></span> |

| <span data-ttu-id="e9ca8-1144">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1144">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1145">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1145">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1146">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1146">modelId</span></span> |<span data-ttu-id="e9ca8-1147">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1147">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-1148">userDescription</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1148">userDescription</span></span> |<span data-ttu-id="e9ca8-1149">Identificador textual do catálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1149">Textual identifier of hello catalog.</span></span> <span data-ttu-id="e9ca8-1150">Observe que se você usar espaços você deve codificá-los com 20%.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1150">Note that if you use spaces you must encode it with %20 instead.</span></span> <span data-ttu-id="e9ca8-1151">Consulte o exemplo acima.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1151">See example above.</span></span><br><span data-ttu-id="e9ca8-1152">Comprimento máximo: 50</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1152">Max length: 50</span></span> |
| <span data-ttu-id="e9ca8-1153">buildType</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1153">buildType</span></span> |<span data-ttu-id="e9ca8-1154">Tipo de saudação compilação tooinvoke:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1154">Type of hello build tooinvoke:</span></span> <br/> <span data-ttu-id="e9ca8-1155">-.'Recomendação' compilação de recomendação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1155">- 'Recommendation' for recommendation build</span></span> <br> <span data-ttu-id="e9ca8-1156">- 'Classificação' para compilação de classificação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1156">- 'Ranking' for rank build</span></span> <br/> <span data-ttu-id="e9ca8-1157">- “Fbt” para compilação FBT</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1157">- 'Fbt' for FBT build</span></span> |
| <span data-ttu-id="e9ca8-1158">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1158">apiVersion</span></span> |<span data-ttu-id="e9ca8-1159">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1159">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-1160">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1160">Request Body</span></span> |<span data-ttu-id="e9ca8-1161">Se deixado em branco compilação Olá será executada com parâmetros de compilação saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1161">If left empty then hello build will be executed with hello default build parameters.</span></span><br><br><span data-ttu-id="e9ca8-1162">Se você quiser tooset parâmetros de compilação, enviá-los como XML no corpo de saudação como em Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1162">If you want tooset build parameters, send them as XML into hello body like in hello following sample.</span></span> <span data-ttu-id="e9ca8-1163">(Consulte a seção de hello "parâmetros de compilação" para uma explicação e uma lista completa de parâmetros de saudação).`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1163">(See hello "Build parameters" section for an explanation and full list of hello parameters.)`<BuildParametersList><NumberOfModelIterations>40</NumberOfModelIterations><NumberOfModelDimensions>20</NumberOfModelDimensions><MinItemAppearance>5</MinItemAppearance><MinUserAppearance>5</MinUserAppearance></BuildParametersList>`</span></span> |

<span data-ttu-id="e9ca8-1164">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1164">**Response**:</span></span>

<span data-ttu-id="e9ca8-1165">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1165">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-1166">Esta é uma API assíncrona.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1166">This is an asynchronous API.</span></span> <span data-ttu-id="e9ca8-1167">Você receberá uma ID de compilação como uma resposta.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1167">You will get a build ID as a response.</span></span> <span data-ttu-id="e9ca8-1168">tooknow quando a compilação Olá terminou, você deve chamar hello "Obter compilações Status de um modelo de" API e localize essa compilação ID na resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1168">tooknow when hello build has ended, you should call hello “Get Builds Status of a Model” API and locate this build ID in hello response.</span></span> <span data-ttu-id="e9ca8-1169">Observe que uma compilação pode levar de toohours minutos dependendo do tamanho de saudação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1169">Note that a build can take from minutes toohours depending on hello size of hello data.</span></span>

<span data-ttu-id="e9ca8-1170">Você não pode consumir recomendações até Olá compilar termina.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1170">You cannot consume recommendations till hello build ends.</span></span>

<span data-ttu-id="e9ca8-1171">Status de compilação válidos:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1171">Valid build status:</span></span>

* <span data-ttu-id="e9ca8-1172">Criado - O modelo foi criado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1172">Create - Model was created.</span></span>
* <span data-ttu-id="e9ca8-1173">Na fila - A compilação do modelo foi disparada e está na fila.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1173">Queued - Model build was triggered and it is queued.</span></span>
* <span data-ttu-id="e9ca8-1174">Criando - O modelo está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1174">Building - Model is being built.</span></span>
* <span data-ttu-id="e9ca8-1175">Sucesso - A compilação concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1175">Success - Build ended successfully.</span></span>
* <span data-ttu-id="e9ca8-1176">Erro - A compilação foi concluída com uma falha.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1176">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="e9ca8-1177">Cancelado - A compilação foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1177">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="e9ca8-1178">Cancelando - A compilação está sendo cancelada.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1178">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="e9ca8-1179">Observe que compilação Olá que ID pode ser encontrada em Olá que caminho a seguir:`Feed\entry\content\properties\Id`</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1179">Note that hello build ID can be found under hello following path: `Feed\entry\content\properties\Id`</span></span>

<span data-ttu-id="e9ca8-1180">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1180">OData XML</span></span>

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




### <a name="114-get-builds-status-of-a-model"></a><span data-ttu-id="e9ca8-1181">11.4.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1181">11.4.</span></span> <span data-ttu-id="e9ca8-1182">Obter status da compilação de um modelo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1182">Get Builds Status of a Model</span></span>
<span data-ttu-id="e9ca8-1183">Recupera compilações e seus status para um modelo específico.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1183">Retrieves builds and their status for a specified model.</span></span>

| <span data-ttu-id="e9ca8-1184">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1184">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1185">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1185">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1186">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1186">GET</span></span> |`<rootURI>/GetModelBuildsStatus?modelId=%27<modelId>%27&onlyLastBuild=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1187">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1187">Example:</span></span><br>`<rootURI>/GetModelBuildsStatus?modelId=%279559872f-7a53-4076-a3c7-19d9385c1265%27&onlyLastBuild=true&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-1188">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1188">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1189">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1189">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1190">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1190">modelId</span></span> |<span data-ttu-id="e9ca8-1191">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1191">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-1192">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1192">onlyLastBuild</span></span> |<span data-ttu-id="e9ca8-1193">Indica se tooreturn todos Olá criar histórico do modelo de saudação ou somente status de saudação da compilação mais recente do hello</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1193">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build</span></span> |
| <span data-ttu-id="e9ca8-1194">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1194">apiVersion</span></span> |<span data-ttu-id="e9ca8-1195">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1195">1.0</span></span> |

<span data-ttu-id="e9ca8-1196">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1196">**Response**:</span></span>

<span data-ttu-id="e9ca8-1197">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1197">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-1198">resposta de saudação inclui uma entrada por compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1198">hello response includes one entry per build.</span></span> <span data-ttu-id="e9ca8-1199">Cada entrada tem Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1199">Each entry has hello following data:</span></span>

* <span data-ttu-id="e9ca8-1200">`feed/entry/content/properties/UserName`-Nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1200">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="e9ca8-1201">`feed/entry/content/properties/ModelName`-Nome do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1201">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="e9ca8-1202">`feed/entry/content/properties/ModelId` - Identificador exclusivo do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1202">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="e9ca8-1203">`feed/entry/content/properties/IsDeployed`-Se a compilação Olá é implantada (também conhecido como</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1203">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed (a.k.a.</span></span> <span data-ttu-id="e9ca8-1204">compilação ativa).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1204">active build).</span></span>
* <span data-ttu-id="e9ca8-1205">`feed/entry/content/properties/BuildId` - Identificador exclusivo da compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1205">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="e9ca8-1206">`feed/entry/content/properties/BuildType`-Tipo de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1206">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="e9ca8-1207">`feed/entry/content/properties/Status` - Status da compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1207">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="e9ca8-1208">Pode ser uma das seguintes Olá: erro, construção, na fila, cancelando, cancelado, êxito.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1208">Can be one of hello following: Error, Building, Queued, Cancelling, Cancelled, Success.</span></span>
* <span data-ttu-id="e9ca8-1209">`feed/entry/content/properties/StatusMessage`-Mensagem de status detalhadas (aplica-se somente os estados de toospecific).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1209">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="e9ca8-1210">`feed/entry/content/properties/Progress` - Andamento da compilação (%).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1210">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="e9ca8-1211">`feed/entry/content/properties/StartTime` - Hora de início da compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1211">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="e9ca8-1212">`feed/entry/content/properties/EndTime` - Hora de término da compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1212">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="e9ca8-1213">`feed/entry/content/properties/ExecutionTime` - Duração da compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1213">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="e9ca8-1214">`feed/entry/content/properties/ProgressStep`-Os detalhes sobre o estágio atual de saudação de uma compilação em andamento.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1214">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="e9ca8-1215">Status de compilação válidos:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1215">Valid build status:</span></span>

* <span data-ttu-id="e9ca8-1216">Criada - a entrada da solicitação de compilação foi criada.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1216">Created - Build request entry was created.</span></span>
* <span data-ttu-id="e9ca8-1217">Em fila - a solicitação de build foi disparada e está na fila.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1217">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="e9ca8-1218">Compilando - a build está em andamento.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1218">Building - Build is in process.</span></span>
* <span data-ttu-id="e9ca8-1219">Sucesso - A compilação concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1219">Success - Build ended successfully.</span></span>
* <span data-ttu-id="e9ca8-1220">Erro - A compilação foi concluída com uma falha.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1220">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="e9ca8-1221">Cancelado - A compilação foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1221">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="e9ca8-1222">Cancelando - A compilação está sendo cancelada.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1222">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="e9ca8-1223">Valores válidos para o tipo de compilação:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1223">Valid values for build type:</span></span>

* <span data-ttu-id="e9ca8-1224">Classificação - compilação de classificação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1224">Rank - Rank build.</span></span>
* <span data-ttu-id="e9ca8-1225">Recomendação - compilação de recomendação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1225">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="e9ca8-1226">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1226">OData XML</span></span>

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


### <a name="115-get-builds-status"></a><span data-ttu-id="e9ca8-1227">11.5.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1227">11.5.</span></span> <span data-ttu-id="e9ca8-1228">Obter Status da Compilação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1228">Get Builds Status</span></span>
<span data-ttu-id="e9ca8-1229">Recupera os status da compilação de todos os modelos de um usuário</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1229">Retrieves build statuses of all models of a user.</span></span>

| <span data-ttu-id="e9ca8-1230">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1230">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1231">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1231">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1232">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1232">GET</span></span> |`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1233">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1233">Example:</span></span><br>`<rootURI>/GetUserBuildsStatus?onlyLastBuilds=true&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-1234">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1234">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1235">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1235">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1236">onlyLastBuild</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1236">onlyLastBuild</span></span> |<span data-ttu-id="e9ca8-1237">Indica se tooreturn todos Olá criar histórico do modelo de saudação ou somente status de saudação da compilação mais recente do hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1237">Indicates whether tooreturn all hello build history of hello model or only hello status of hello most recent build.</span></span> |
| <span data-ttu-id="e9ca8-1238">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1238">apiVersion</span></span> |<span data-ttu-id="e9ca8-1239">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1239">1.0</span></span> |

<span data-ttu-id="e9ca8-1240">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1240">**Response**:</span></span>

<span data-ttu-id="e9ca8-1241">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1241">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-1242">resposta de saudação inclui uma entrada por compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1242">hello response includes one entry per build.</span></span> <span data-ttu-id="e9ca8-1243">Cada entrada tem Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1243">Each entry has hello following data:</span></span>

* <span data-ttu-id="e9ca8-1244">`feed/entry/content/properties/UserName`-Nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1244">`feed/entry/content/properties/UserName` - Name of hello user.</span></span>
* <span data-ttu-id="e9ca8-1245">`feed/entry/content/properties/ModelName`-Nome do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1245">`feed/entry/content/properties/ModelName` - Name of hello model.</span></span>
* <span data-ttu-id="e9ca8-1246">`feed/entry/content/properties/ModelId` - Identificador exclusivo do modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1246">`feed/entry/content/properties/ModelId` - Model unique identifier.</span></span>
* <span data-ttu-id="e9ca8-1247">`feed/entry/content/properties/IsDeployed`-Se a compilação de saudação é implantada.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1247">`feed/entry/content/properties/IsDeployed` - Whether hello build is deployed.</span></span>
* <span data-ttu-id="e9ca8-1248">`feed/entry/content/properties/BuildId` - Identificador exclusivo da compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1248">`feed/entry/content/properties/BuildId` - Build unique identifier.</span></span>
* <span data-ttu-id="e9ca8-1249">`feed/entry/content/properties/BuildType`-Tipo de compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1249">`feed/entry/content/properties/BuildType` - Type of hello build.</span></span>
* <span data-ttu-id="e9ca8-1250">`feed/entry/content/properties/Status` - Status da compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1250">`feed/entry/content/properties/Status` - Build status.</span></span> <span data-ttu-id="e9ca8-1251">Pode ser uma das seguintes Olá: erro, construção, na fila, cancelado, cancelando, êxito.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1251">Can be one of hello following: Error, Building, Queued, Cancelled, Cancelling, Success.</span></span>
* <span data-ttu-id="e9ca8-1252">`feed/entry/content/properties/StatusMessage`-Mensagem de status detalhadas (aplica-se somente os estados de toospecific).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1252">`feed/entry/content/properties/StatusMessage` - Detailed status message (applies only toospecific states).</span></span>
* <span data-ttu-id="e9ca8-1253">`feed/entry/content/properties/Progress` - Andamento da compilação (%).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1253">`feed/entry/content/properties/Progress` - Build progress (%).</span></span>
* <span data-ttu-id="e9ca8-1254">`feed/entry/content/properties/StartTime` - Hora de início da compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1254">`feed/entry/content/properties/StartTime` - Build start time.</span></span>
* <span data-ttu-id="e9ca8-1255">`feed/entry/content/properties/EndTime` - Hora de término da compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1255">`feed/entry/content/properties/EndTime` - Build end time.</span></span>
* <span data-ttu-id="e9ca8-1256">`feed/entry/content/properties/ExecutionTime` - Duração da compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1256">`feed/entry/content/properties/ExecutionTime` - Build duration.</span></span>
* <span data-ttu-id="e9ca8-1257">`feed/entry/content/properties/ProgressStep`-Os detalhes sobre o estágio atual de saudação de uma compilação em andamento.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1257">`feed/entry/content/properties/ProgressStep` - Details about hello current stage of a build in progress.</span></span>

<span data-ttu-id="e9ca8-1258">Status de compilação válidos:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1258">Valid build status:</span></span>

* <span data-ttu-id="e9ca8-1259">Criada - a entrada da solicitação de compilação foi criada.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1259">Created - Build request entry was created.</span></span>
* <span data-ttu-id="e9ca8-1260">Em fila - a solicitação de build foi disparada e está na fila.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1260">Queued - Build request was triggered and it is queued.</span></span>
* <span data-ttu-id="e9ca8-1261">Compilando - a build está em andamento.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1261">Building - Build is in process.</span></span>
* <span data-ttu-id="e9ca8-1262">Sucesso - A compilação concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1262">Success - Build ended successfully.</span></span>
* <span data-ttu-id="e9ca8-1263">Erro - A compilação foi concluída com uma falha.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1263">Error - Build ended with a failure.</span></span>
* <span data-ttu-id="e9ca8-1264">Cancelado - A compilação foi cancelada.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1264">Cancelled - Build was cancelled.</span></span>
* <span data-ttu-id="e9ca8-1265">Cancelando - A compilação está sendo cancelada.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1265">Cancelling - Build is being cancelled.</span></span>

<span data-ttu-id="e9ca8-1266">Valores válidos para o tipo de compilação:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1266">Valid values for build type:</span></span>

* <span data-ttu-id="e9ca8-1267">Classificação - compilação de classificação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1267">Rank - Rank build.</span></span>
* <span data-ttu-id="e9ca8-1268">Recomendação - compilação de recomendação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1268">Recommendation - Recommendation build.</span></span>

<span data-ttu-id="e9ca8-1269">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1269">OData XML</span></span>

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


### <a name="116-delete-build"></a><span data-ttu-id="e9ca8-1270">11.6.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1270">11.6.</span></span> <span data-ttu-id="e9ca8-1271">Excluir compilação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1271">Delete Build</span></span>
<span data-ttu-id="e9ca8-1272">Exclui uma compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1272">Deletes a build.</span></span>

<span data-ttu-id="e9ca8-1273">OBSERVAÇÃO: </span><span class="sxs-lookup"><span data-stu-id="e9ca8-1273">NOTE:</span></span> <br><span data-ttu-id="e9ca8-1274">Não é possível excluir uma compilação ativa.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1274">You cannot delete an active build.</span></span> <span data-ttu-id="e9ca8-1275">Olá modelo deve ser atualizada tooa compilação diferente de ativo antes de excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1275">hello model should be updated tooa different active build before you delete it.</span></span><br><span data-ttu-id="e9ca8-1276">Não é possível excluir um build em andamento.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1276">You cannot delete an in-progress build.</span></span> <span data-ttu-id="e9ca8-1277">Você deve cancelar a compilação Olá primeiro chamar <strong>cancelar a compilação</strong>.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1277">You should cancel hello build first by calling <strong>Cancel Build</strong>.</span></span>

| <span data-ttu-id="e9ca8-1278">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1278">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1279">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1279">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1280">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1280">DELETE</span></span> |`<rootURI>/DeleteBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1281">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1281">Example:</span></span><br>`<rootURI>/DeleteBuild?buildId=%271500068%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-1282">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1282">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1283">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1283">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1284">buildId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1284">buildId</span></span> |<span data-ttu-id="e9ca8-1285">Identificador exclusivo da compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1285">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="e9ca8-1286">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1286">apiVersion</span></span> |<span data-ttu-id="e9ca8-1287">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1287">1.0</span></span> |

<span data-ttu-id="e9ca8-1288">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1288">**Response:**</span></span>

<span data-ttu-id="e9ca8-1289">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1289">HTTP Status code: 200</span></span>

### <a name="117-cancel-build"></a><span data-ttu-id="e9ca8-1290">11.7.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1290">11.7.</span></span> <span data-ttu-id="e9ca8-1291">Cancelar compilação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1291">Cancel Build</span></span>
<span data-ttu-id="e9ca8-1292">Cancela uma compilação que está no status de compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1292">Cancels a build that is in building status.</span></span>

| <span data-ttu-id="e9ca8-1293">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1293">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1294">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1294">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1295">PUT</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1295">PUT</span></span> |`<rootURI>/CancelBuild?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1296">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1296">Example:</span></span><br>`<rootURI>/CancelBuild?buildId=%271500076%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-1297">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1297">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1298">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1298">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1299">buildId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1299">buildId</span></span> |<span data-ttu-id="e9ca8-1300">Identificador exclusivo da compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1300">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="e9ca8-1301">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1301">apiVersion</span></span> |<span data-ttu-id="e9ca8-1302">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1302">1.0</span></span> |

<span data-ttu-id="e9ca8-1303">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1303">**Response:**</span></span>

<span data-ttu-id="e9ca8-1304">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1304">HTTP Status code: 200</span></span>

### <a name="118-get-build-parameters"></a><span data-ttu-id="e9ca8-1305">11.8.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1305">11.8.</span></span> <span data-ttu-id="e9ca8-1306">Obter parâmetros de compilação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1306">Get Build Parameters</span></span>
<span data-ttu-id="e9ca8-1307">Recupera parâmetros de compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1307">Retrieves build parameters.</span></span>

| <span data-ttu-id="e9ca8-1308">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1308">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1309">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1309">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1310">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1310">GET</span></span> |`<rootURI>/GetBuildParameters?buildId=%27<buildId>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1311">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1311">Example:</span></span><br>`<rootURI>/GetBuildParameters?buildId=%271000653%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-1312">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1312">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1313">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1313">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1314">buildId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1314">buildId</span></span> |<span data-ttu-id="e9ca8-1315">Identificador exclusivo da compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1315">Unique identifier of hello build.</span></span> |
| <span data-ttu-id="e9ca8-1316">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1316">apiVersion</span></span> |<span data-ttu-id="e9ca8-1317">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1317">1.0</span></span> |

<span data-ttu-id="e9ca8-1318">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1318">**Response:**</span></span>

<span data-ttu-id="e9ca8-1319">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1319">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-1320">Essa API retorna uma coleção de elementos de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1320">This API returns a collection of key/value elements.</span></span> <span data-ttu-id="e9ca8-1321">Cada elemento representa um parâmetro e seu valor:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1321">Each element represents a parameter and its value:</span></span>

* <span data-ttu-id="e9ca8-1322">`feed/entry/content/properties/Key` - nome do parâmetro de build.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1322">`feed/entry/content/properties/Key` - Build parameter name.</span></span>
* <span data-ttu-id="e9ca8-1323">`feed/entry/content/properties/Value` - valor do parâmetro de build.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1323">`feed/entry/content/properties/Value` - Build parameter value.</span></span>

<span data-ttu-id="e9ca8-1324">Olá tabela a seguir mostra o valor de saudação que representa cada chave.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1324">hello table below depicts hello value that each key represents.</span></span>

| <span data-ttu-id="e9ca8-1325">Chave</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1325">Key</span></span> | <span data-ttu-id="e9ca8-1326">Descrição</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1326">Description</span></span> | <span data-ttu-id="e9ca8-1327">Tipo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1327">Type</span></span> | <span data-ttu-id="e9ca8-1328">Valor Válido</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1328">Valid Value</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="e9ca8-1329">NumberOfModelIterations</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1329">NumberOfModelIterations</span></span> |<span data-ttu-id="e9ca8-1330">número de saudação de iterações modelo Olá executa é refletido pela Olá tempo e hello precisão do modelo de computação geral.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1330">hello number of iterations hello model performs is reflected by hello overall compute time and hello model accuracy.</span></span> <span data-ttu-id="e9ca8-1331">número mais alto de Olá Olá, você terá maior precisão do hello, mas Olá computação tempo irá demorar mais.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1331">hello higher hello number, hello better accuracy you will get, but hello compute time will take longer.</span></span> |<span data-ttu-id="e9ca8-1332">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1332">Integer</span></span> |<span data-ttu-id="e9ca8-1333">10-50</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1333">10-50</span></span> |
| <span data-ttu-id="e9ca8-1334">NumberOfModelDimensions</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1334">NumberOfModelDimensions</span></span> |<span data-ttu-id="e9ca8-1335">número de saudação de dimensões se relaciona toohello número do modelo de saudação 'recursos' tentará toofind dentro de seus dados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1335">hello number of dimensions relates toohello number of 'features' hello model will try toofind within your data.</span></span> <span data-ttu-id="e9ca8-1336">Aumentar o número de saudação de dimensões permitirá ajustar melhor os resultados de saudação em clusters menores.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1336">Increasing hello number of dimensions will allow better fine-tuning of hello results into smaller clusters.</span></span> <span data-ttu-id="e9ca8-1337">No entanto, muitas dimensões impedirá modelo Olá localização de correlações entre itens.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1337">However, too many dimensions will prevent hello model from finding correlations between items.</span></span> |<span data-ttu-id="e9ca8-1338">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1338">Integer</span></span> |<span data-ttu-id="e9ca8-1339">10-40</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1339">10-40</span></span> |
| <span data-ttu-id="e9ca8-1340">ItemCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1340">ItemCutOffLowerBound</span></span> |<span data-ttu-id="e9ca8-1341">Define Olá item inferior para condensador hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1341">Defines hello item lower bound for hello condenser.</span></span> <span data-ttu-id="e9ca8-1342">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1342">See usage condenser above.</span></span> |<span data-ttu-id="e9ca8-1343">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1343">Integer</span></span> |<span data-ttu-id="e9ca8-1344">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1344">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="e9ca8-1345">ItemCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1345">ItemCutOffUpperBound</span></span> |<span data-ttu-id="e9ca8-1346">Define Olá item limite superior condensador hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1346">Defines hello item upper bound for hello condenser.</span></span> <span data-ttu-id="e9ca8-1347">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1347">See usage condenser above.</span></span> |<span data-ttu-id="e9ca8-1348">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1348">Integer</span></span> |<span data-ttu-id="e9ca8-1349">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1349">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="e9ca8-1350">UserCutOffLowerBound</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1350">UserCutOffLowerBound</span></span> |<span data-ttu-id="e9ca8-1351">Define Olá usuário inferior para condensador hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1351">Defines hello user lower bound for hello condenser.</span></span> <span data-ttu-id="e9ca8-1352">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1352">See usage condenser above.</span></span> |<span data-ttu-id="e9ca8-1353">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1353">Integer</span></span> |<span data-ttu-id="e9ca8-1354">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1354">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="e9ca8-1355">UserCutOffUpperBound</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1355">UserCutOffUpperBound</span></span> |<span data-ttu-id="e9ca8-1356">Define Olá usuário limite superior condensador hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1356">Defines hello user upper bound for hello condenser.</span></span> <span data-ttu-id="e9ca8-1357">Consulte o condensador de uso acima.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1357">See usage condenser above.</span></span> |<span data-ttu-id="e9ca8-1358">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1358">Integer</span></span> |<span data-ttu-id="e9ca8-1359">2 ou mais (0 desabilita o condensador)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1359">2 or more (0 disable condenser)</span></span> |
| <span data-ttu-id="e9ca8-1360">Descrição</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1360">Description</span></span> |<span data-ttu-id="e9ca8-1361">Descrição da compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1361">Build description.</span></span> |<span data-ttu-id="e9ca8-1362">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1362">String</span></span> |<span data-ttu-id="e9ca8-1363">Qualquer texto, máximo de 512 caracteres</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1363">Any text, maximum 512 chars</span></span> |
| <span data-ttu-id="e9ca8-1364">EnableModelingInsights</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1364">EnableModelingInsights</span></span> |<span data-ttu-id="e9ca8-1365">Permite que você toocompute métricas no modelo de recomendação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1365">Allows you toocompute metrics on hello recommendation model.</span></span> |<span data-ttu-id="e9ca8-1366">Booliano</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1366">Boolean</span></span> |<span data-ttu-id="e9ca8-1367">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1367">True/False</span></span> |
| <span data-ttu-id="e9ca8-1368">UseFeaturesInModel</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1368">UseFeaturesInModel</span></span> |<span data-ttu-id="e9ca8-1369">Indica se os recursos podem ser usados no modelo de recomendação de saudação do pedido tooenhance.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1369">Indicates if features can be used in order tooenhance hello recommendation model.</span></span> |<span data-ttu-id="e9ca8-1370">Booliano</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1370">Boolean</span></span> |<span data-ttu-id="e9ca8-1371">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1371">True/False</span></span> |
| <span data-ttu-id="e9ca8-1372">ModelingFeatureList</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1372">ModelingFeatureList</span></span> |<span data-ttu-id="e9ca8-1373">Lista separada por vírgulas de toobe de nomes de recurso usado na compilação de recomendação hello, na recomendação de saudação do tooenhance de ordem.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1373">Comma-separated list of feature names toobe used in hello recommendation build, in order tooenhance hello recommendation.</span></span> |<span data-ttu-id="e9ca8-1374">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1374">String</span></span> |<span data-ttu-id="e9ca8-1375">Nomes de recurso, o too512 caracteres</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1375">Feature names, up too512 chars</span></span> |
| <span data-ttu-id="e9ca8-1376">AllowColdItemPlacement</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1376">AllowColdItemPlacement</span></span> |<span data-ttu-id="e9ca8-1377">Indica se a recomendação de saudação também enviar por push itens frios por meio de similaridade de recurso.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1377">Indicates if hello recommendation should also push cold items via feature similarity.</span></span> |<span data-ttu-id="e9ca8-1378">Booliano</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1378">Boolean</span></span> |<span data-ttu-id="e9ca8-1379">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1379">True/False</span></span> |
| <span data-ttu-id="e9ca8-1380">EnableFeatureCorrelation</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1380">EnableFeatureCorrelation</span></span> |<span data-ttu-id="e9ca8-1381">Indica se os recursos podem ser usados no raciocínio.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1381">Indicates if features can be used in reasoning.</span></span> |<span data-ttu-id="e9ca8-1382">Booliano</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1382">Boolean</span></span> |<span data-ttu-id="e9ca8-1383">Verdadeiro/Falso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1383">True/False</span></span> |
| <span data-ttu-id="e9ca8-1384">ReasoningFeatureList</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1384">ReasoningFeatureList</span></span> |<span data-ttu-id="e9ca8-1385">Lista separada por vírgulas de toobe de nomes de recurso usado para raciocínio sentenças (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1385">Comma-separated list of feature names toobe used for reasoning sentences (e.g. recommendation explanations).</span></span> |<span data-ttu-id="e9ca8-1386">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1386">String</span></span> |<span data-ttu-id="e9ca8-1387">Nomes de recurso, o too512 caracteres</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1387">Feature names, up too512 chars</span></span> |

<span data-ttu-id="e9ca8-1388">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1388">OData XML</span></span>

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

## <a name="12-recommendation"></a><span data-ttu-id="e9ca8-1389">12. Recomendações</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1389">12. Recommendation</span></span>
### <a name="121-get-item-recommendations-for-active-build"></a><span data-ttu-id="e9ca8-1390">12.1.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1390">12.1.</span></span> <span data-ttu-id="e9ca8-1391">Obter Recomendações de Item (para compilação ativa)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1391">Get Item Recommendations (for active build)</span></span>
<span data-ttu-id="e9ca8-1392">Obter recomendações de compilação de saudação ativo do tipo "Recomendação" ou "Fbt" com base em uma lista de itens de sementes (entrada).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1392">Get recommendations of hello active build of type "Recommendation" or "Fbt" based on a list of seeds (input) items.</span></span>

| <span data-ttu-id="e9ca8-1393">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1393">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1394">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1394">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1395">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1395">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1396">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1396">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-1397">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1397">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1398">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1398">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1399">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1399">modelId</span></span> |<span data-ttu-id="e9ca8-1400">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1400">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-1401">itemIds</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1401">itemIds</span></span> |<span data-ttu-id="e9ca8-1402">Lista separada por vírgulas de saudação itens toorecommend para.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1402">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="e9ca8-1403">Se compilação active Olá é do tipo FBT, em seguida, você pode enviar somente um item.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1403">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="e9ca8-1404">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1404">Max length: 1024</span></span> |
| <span data-ttu-id="e9ca8-1405">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1405">numberOfResults</span></span> |<span data-ttu-id="e9ca8-1406">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="e9ca8-1406">Number of required results</span></span> <br> <span data-ttu-id="e9ca8-1407">Máx.: 150</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1407">Max: 150</span></span> |
| <span data-ttu-id="e9ca8-1408">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1408">includeMetatadata</span></span> |<span data-ttu-id="e9ca8-1409">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1409">Future use, always false</span></span> |
| <span data-ttu-id="e9ca8-1410">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1410">apiVersion</span></span> |<span data-ttu-id="e9ca8-1411">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1411">1.0</span></span> |

<span data-ttu-id="e9ca8-1412">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1412">**Response:**</span></span>

<span data-ttu-id="e9ca8-1413">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1413">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-1414">resposta de saudação inclui uma entrada por itens recomendados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1414">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="e9ca8-1415">Cada entrada tem Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1415">Each entry has hello following data:</span></span>

* <span data-ttu-id="e9ca8-1416">`Feed\entry\content\properties\Id` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1416">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="e9ca8-1417">`Feed\entry\content\properties\Name`-Nome do item de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1417">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="e9ca8-1418">`Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1418">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="e9ca8-1419">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1419">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="e9ca8-1420">resposta de exemplo Hello abaixo inclui 10 itens recomendados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1420">hello example response below includes 10 recommended items.</span></span>

<span data-ttu-id="e9ca8-1421">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1421">OData XML</span></span>

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

### <a name="122-get-item-recommendations-of-a-specific-build"></a><span data-ttu-id="e9ca8-1422">12.2.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1422">12.2.</span></span> <span data-ttu-id="e9ca8-1423">Obter Recomendações de Item (de uma compilação específica)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1423">Get Item Recommendations (of a specific build)</span></span>
<span data-ttu-id="e9ca8-1424">Obtenha recomendações de uma compilação específica do tipo “Recomendação” ou “Fbt”.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1424">Get recommendations of a specific build of type "Recommendation" or "Fbt".</span></span>

| <span data-ttu-id="e9ca8-1425">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1425">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1426">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1426">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1427">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1427">GET</span></span> |`<rootURI>/ItemRecommend?modelId=%27<modelId>%27&itemIds=%27<itemId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1428">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1428">Example:</span></span><br>`<rootURI>/ItemRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-1429">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1429">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1430">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1430">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1431">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1431">modelId</span></span> |<span data-ttu-id="e9ca8-1432">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1432">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-1433">itemIds</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1433">itemIds</span></span> |<span data-ttu-id="e9ca8-1434">Lista separada por vírgulas de saudação itens toorecommend para.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1434">Comma-separated list of hello items toorecommend for.</span></span> <br><span data-ttu-id="e9ca8-1435">Se compilação active Olá é do tipo FBT, em seguida, você pode enviar somente um item.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1435">If hello active build is of type FBT then you can send only one item.</span></span> <br><span data-ttu-id="e9ca8-1436">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1436">Max length: 1024</span></span> |
| <span data-ttu-id="e9ca8-1437">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1437">numberOfResults</span></span> |<span data-ttu-id="e9ca8-1438">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="e9ca8-1438">Number of required results</span></span> <br> <span data-ttu-id="e9ca8-1439">Máx.: 150</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1439">Max: 150</span></span> |
| <span data-ttu-id="e9ca8-1440">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1440">includeMetatadata</span></span> |<span data-ttu-id="e9ca8-1441">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1441">Future use, always false</span></span> |
| <span data-ttu-id="e9ca8-1442">buildId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1442">buildId</span></span> |<span data-ttu-id="e9ca8-1443">Olá toouse id para esta solicitação de recomendação de compilação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1443">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="e9ca8-1444">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1444">apiVersion</span></span> |<span data-ttu-id="e9ca8-1445">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1445">1.0</span></span> |

<span data-ttu-id="e9ca8-1446">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1446">**Response:**</span></span>

<span data-ttu-id="e9ca8-1447">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1447">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-1448">resposta de saudação inclui uma entrada por itens recomendados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1448">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="e9ca8-1449">Cada entrada tem Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1449">Each entry has hello following data:</span></span>

* <span data-ttu-id="e9ca8-1450">`Feed\entry\content\properties\Id` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1450">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="e9ca8-1451">`Feed\entry\content\properties\Name`-Nome do item de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1451">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="e9ca8-1452">`Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1452">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="e9ca8-1453">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1453">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="e9ca8-1454">Veja um exemplo de resposta no 12.1</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1454">See a response example in 12.1</span></span>

### <a name="123-get-fbt-recommendations-for-active-build"></a><span data-ttu-id="e9ca8-1455">12.3.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1455">12.3.</span></span> <span data-ttu-id="e9ca8-1456">Obter Recomendações de FBT (para compilação ativa)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1456">Get FBT Recommendations (for active build)</span></span>
<span data-ttu-id="e9ca8-1457">Obter recomendações de compilação de ativo de saudação do tipo "Fbt" com base em um item de semente (entrada).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1457">Get recommendations of hello active build of type "Fbt" based on a seed (input) item.</span></span>

| <span data-ttu-id="e9ca8-1458">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1458">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1459">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1459">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1460">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1460">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1461">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1461">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=<double>&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-1462">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1462">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1463">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1463">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1464">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1464">modelId</span></span> |<span data-ttu-id="e9ca8-1465">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1465">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-1466">itemId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1466">itemId</span></span> |<span data-ttu-id="e9ca8-1467">Item toorecommend para.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1467">Item toorecommend for.</span></span> <br><span data-ttu-id="e9ca8-1468">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1468">Max length: 1024</span></span> |
| <span data-ttu-id="e9ca8-1469">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1469">numberOfResults</span></span> |<span data-ttu-id="e9ca8-1470">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="e9ca8-1470">Number of required results</span></span> <br><span data-ttu-id="e9ca8-1471">Máx.: 150</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1471">Max: 150</span></span> |
| <span data-ttu-id="e9ca8-1472">minimalScore</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1472">minimalScore</span></span> |<span data-ttu-id="e9ca8-1473">Pontuação mínima que um conjunto frequente deve ter em ordem toobe incluído no hello retornados resultados</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1473">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="e9ca8-1474">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1474">includeMetatadata</span></span> |<span data-ttu-id="e9ca8-1475">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1475">Future use, always false</span></span> |
| <span data-ttu-id="e9ca8-1476">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1476">apiVersion</span></span> |<span data-ttu-id="e9ca8-1477">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1477">1.0</span></span> |

<span data-ttu-id="e9ca8-1478">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1478">**Response:**</span></span>

<span data-ttu-id="e9ca8-1479">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1479">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-1480">resposta de saudação inclui uma entrada por conjunto de itens Recomendados (um conjunto de itens que são geralmente comprados junto com o item de semente/entrada hello).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1480">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="e9ca8-1481">Cada entrada tem Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1481">Each entry has hello following data:</span></span>

* <span data-ttu-id="e9ca8-1482">`Feed\entry\content\properties\Id1` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1482">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="e9ca8-1483">`Feed\entry\content\properties\Name1`-Nome do item de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1483">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="e9ca8-1484">`Feed\entry\content\properties\Id2` - ID do segundo item recomendado (opcional).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1484">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="e9ca8-1485">`Feed\entry\content\properties\Name2`-Nome do item 2 da saudação (opcional).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1485">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="e9ca8-1486">`Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1486">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="e9ca8-1487">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1487">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="e9ca8-1488">resposta de exemplo Hello abaixo inclui 3 conjuntos de itens recomendados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1488">hello example response below includes 3 recommended item sets.</span></span>

<span data-ttu-id="e9ca8-1489">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1489">OData XML</span></span>

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

### <a name="124-get-fbt-recommendations-of-a-specific-build"></a><span data-ttu-id="e9ca8-1490">12.4.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1490">12.4.</span></span> <span data-ttu-id="e9ca8-1491">Obter Recomendações FBT (de uma compilação específica)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1491">Get FBT Recommendations (of a specific build)</span></span>
<span data-ttu-id="e9ca8-1492">Obtenha recomendações de uma compilação específica do tipo "Fbt".</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1492">Get recommendations of a specific build of type "Fbt".</span></span>

| <span data-ttu-id="e9ca8-1493">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1493">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1494">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1494">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1495">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1495">GET</span></span> |`<rootURI>/ItemFbtRecommend?modelId=%27<modelId>%27&itemId=%27<itemId>%27&numberOfResults=<int>&minimalScore=<double>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1496">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1496">Example:</span></span><br>`<rootURI>/ItemFbtRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&itemId=%271003%27&numberOfResults=10&minimalScore=0.1&includeMetadata=false&buildId=1234&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-1497">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1497">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1498">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1498">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1499">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1499">modelId</span></span> |<span data-ttu-id="e9ca8-1500">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1500">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-1501">itemId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1501">itemId</span></span> |<span data-ttu-id="e9ca8-1502">Item toorecommend para.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1502">Item toorecommend for.</span></span> <br><span data-ttu-id="e9ca8-1503">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1503">Max length: 1024</span></span> |
| <span data-ttu-id="e9ca8-1504">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1504">numberOfResults</span></span> |<span data-ttu-id="e9ca8-1505">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="e9ca8-1505">Number of required results</span></span> <br><span data-ttu-id="e9ca8-1506">Máx.: 150</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1506">Max: 150</span></span> |
| <span data-ttu-id="e9ca8-1507">minimalScore</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1507">minimalScore</span></span> |<span data-ttu-id="e9ca8-1508">Pontuação mínima que um conjunto frequente deve ter em ordem toobe incluído no hello retornados resultados</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1508">Minimal score that a frequent set should have in order toobe included in hello returned results</span></span> |
| <span data-ttu-id="e9ca8-1509">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1509">includeMetatadata</span></span> |<span data-ttu-id="e9ca8-1510">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1510">Future use, always false</span></span> |
| <span data-ttu-id="e9ca8-1511">buildId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1511">buildId</span></span> |<span data-ttu-id="e9ca8-1512">Olá toouse id para esta solicitação de recomendação de compilação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1512">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="e9ca8-1513">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1513">apiVersion</span></span> |<span data-ttu-id="e9ca8-1514">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1514">1.0</span></span> |

<span data-ttu-id="e9ca8-1515">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1515">**Response:**</span></span>

<span data-ttu-id="e9ca8-1516">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1516">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-1517">resposta de saudação inclui uma entrada por conjunto de itens Recomendados (um conjunto de itens que são geralmente comprados junto com o item de semente/entrada hello).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1517">hello response includes one entry per recommended item set (a set of items which are usually bought together with hello seed/input item).</span></span> <span data-ttu-id="e9ca8-1518">Cada entrada tem Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1518">Each entry has hello following data:</span></span>

* <span data-ttu-id="e9ca8-1519">`Feed\entry\content\properties\Id1` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1519">`Feed\entry\content\properties\Id1` - Recommended item ID.</span></span>
* <span data-ttu-id="e9ca8-1520">`Feed\entry\content\properties\Name1`-Nome do item de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1520">`Feed\entry\content\properties\Name1` - Name of hello item.</span></span>
* <span data-ttu-id="e9ca8-1521">`Feed\entry\content\properties\Id2` - ID do segundo item recomendado (opcional).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1521">`Feed\entry\content\properties\Id2` - 2nd recommended item ID (optional).</span></span>
* <span data-ttu-id="e9ca8-1522">`Feed\entry\content\properties\Name2`-Nome do item 2 da saudação (opcional).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1522">`Feed\entry\content\properties\Name2` - Name of hello 2nd item (optional).</span></span>
* <span data-ttu-id="e9ca8-1523">`Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1523">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="e9ca8-1524">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1524">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="e9ca8-1525">Veja um exemplo de resposta no 12.3</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1525">See a response example in 12.3</span></span>

### <a name="125-get-user-recommendations-for-active-build"></a><span data-ttu-id="e9ca8-1526">12.5.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1526">12.5.</span></span> <span data-ttu-id="e9ca8-1527">Obter Recomendações do Usuário (para compilação ativa)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1527">Get User Recommendations (for active build)</span></span>
<span data-ttu-id="e9ca8-1528">Obtenha recomendações de usuário de uma compilação do tipo "Recomendação" marcada como compilação ativa.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1528">Get user recommendations of a build of type "Recommendation" marked as active build.</span></span>

<span data-ttu-id="e9ca8-1529">Olá API retornará uma lista de item previsto de acordo com o toohello histórico de uso do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1529">hello API will return a list of predicted item according toohello usage history of hello user.</span></span>

<span data-ttu-id="e9ca8-1530">Observações:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1530">Notes:</span></span> 

1. <span data-ttu-id="e9ca8-1531">Não há nenhuma recomendação de usuário para a compilação FBT.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1531">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="e9ca8-1532">Se criar hello ativo é FBT esse método será retornará um erro.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1532">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="e9ca8-1533">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1533">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1534">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1534">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1535">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1535">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1536">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1536">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-1537">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1537">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1538">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1538">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1539">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1539">modelId</span></span> |<span data-ttu-id="e9ca8-1540">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1540">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-1541">userId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1541">userId</span></span> |<span data-ttu-id="e9ca8-1542">Identificador exclusivo do usuário Olá</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1542">Unique identifier of hello user</span></span> |
| <span data-ttu-id="e9ca8-1543">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1543">numberOfResults</span></span> |<span data-ttu-id="e9ca8-1544">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="e9ca8-1544">Number of required results</span></span> |
| <span data-ttu-id="e9ca8-1545">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1545">includeMetatadata</span></span> |<span data-ttu-id="e9ca8-1546">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1546">Future use, always false</span></span> |
| <span data-ttu-id="e9ca8-1547">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1547">apiVersion</span></span> |<span data-ttu-id="e9ca8-1548">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1548">1.0</span></span> |

<span data-ttu-id="e9ca8-1549">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1549">**Response:**</span></span>

<span data-ttu-id="e9ca8-1550">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1550">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-1551">resposta de saudação inclui uma entrada por itens recomendados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1551">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="e9ca8-1552">Cada entrada tem Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1552">Each entry has hello following data:</span></span>

* <span data-ttu-id="e9ca8-1553">`Feed\entry\content\properties\Id` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1553">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="e9ca8-1554">`Feed\entry\content\properties\Name`-Nome do item de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1554">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="e9ca8-1555">`Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1555">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="e9ca8-1556">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1556">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="e9ca8-1557">Veja um exemplo de resposta no 12.1</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1557">See a response example in 12.1</span></span>

### <a name="126-get-user-recommendations-with-item-list-for-active-build"></a><span data-ttu-id="e9ca8-1558">12.6.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1558">12.6.</span></span> <span data-ttu-id="e9ca8-1559">Obter recomendações de usuário com a lista de itens (para compilação ativa)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1559">Get User Recommendations with item list (for active build)</span></span>
<span data-ttu-id="e9ca8-1560">Obtenha recomendações de usuário de uma compilação do tipo "Recomendação" marcada como compilação ativa com uma lista de itens adicionais</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1560">Get user recommendations of a build of type "Recommendation" marked as active build with an additional list of items</span></span>

<span data-ttu-id="e9ca8-1561">Olá API retornará uma lista de item previsto de acordo com o toohello histórico de uso do usuário de saudação e itens fornecidos adicionais de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1561">hello API will return a list of predicted item according toohello usage history of hello user and hello additional provided items.</span></span>

<span data-ttu-id="e9ca8-1562">Observações:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1562">Notes:</span></span> 

1. <span data-ttu-id="e9ca8-1563">Não há nenhuma recomendação de usuário para a compilação FBT.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1563">There is no user recommendation for FBT build.</span></span>
2. <span data-ttu-id="e9ca8-1564">Se criar hello ativo é FBT esse método será retornará um erro.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1564">If hello active build is FBT this method will returns an error.</span></span>

| <span data-ttu-id="e9ca8-1565">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1565">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1566">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1566">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1567">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1567">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1568">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1568">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%2C1000%27&numberOfResults=10&includeMetadata=false&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-1569">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1569">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1570">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1570">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1571">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1571">modelId</span></span> |<span data-ttu-id="e9ca8-1572">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1572">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-1573">userId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1573">userId</span></span> |<span data-ttu-id="e9ca8-1574">Identificador exclusivo do usuário Olá</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1574">Unique identifier of hello user</span></span> |
| <span data-ttu-id="e9ca8-1575">itemsIds</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1575">itemsIds</span></span> |<span data-ttu-id="e9ca8-1576">Lista separada por vírgulas de saudação itens toorecommend para.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1576">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="e9ca8-1577">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1577">Max length: 1024</span></span> |
| <span data-ttu-id="e9ca8-1578">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1578">numberOfResults</span></span> |<span data-ttu-id="e9ca8-1579">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="e9ca8-1579">Number of required results</span></span> |
| <span data-ttu-id="e9ca8-1580">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1580">includeMetatadata</span></span> |<span data-ttu-id="e9ca8-1581">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1581">Future use, always false</span></span> |
| <span data-ttu-id="e9ca8-1582">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1582">apiVersion</span></span> |<span data-ttu-id="e9ca8-1583">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1583">1.0</span></span> |

<span data-ttu-id="e9ca8-1584">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1584">**Response:**</span></span>

<span data-ttu-id="e9ca8-1585">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1585">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-1586">resposta de saudação inclui uma entrada por itens recomendados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1586">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="e9ca8-1587">Cada entrada tem Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1587">Each entry has hello following data:</span></span>

* <span data-ttu-id="e9ca8-1588">`Feed\entry\content\properties\Id` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1588">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="e9ca8-1589">`Feed\entry\content\properties\Name`-Nome do item de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1589">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="e9ca8-1590">`Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1590">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="e9ca8-1591">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1591">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="e9ca8-1592">Veja um exemplo de resposta no 12.1</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1592">See a response example in 12.1</span></span>

### <a name="127-get-user-recommendations--of-a-specific-build"></a><span data-ttu-id="e9ca8-1593">12.7.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1593">12.7.</span></span> <span data-ttu-id="e9ca8-1594">Obter Recomendações de Usuário (de uma compilação específica)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1594">Get User Recommendations  (of a specific build)</span></span>
<span data-ttu-id="e9ca8-1595">Obtenha recomendações de usuário de uma compilação específica do tipo "Recomendação".</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1595">Get user recommendations of a specific build of type "Recommendation".</span></span>

<span data-ttu-id="e9ca8-1596">Olá API retornará uma lista de item previsto, de acordo com o histórico de utilização de toohello de usuário de hello (utilizado na compilação específico Olá).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1596">hello API will return a list of predicted item according toohello usage history of hello user (used in hello specific build).</span></span>

<span data-ttu-id="e9ca8-1597">Observação: Não há nenhuma recomendação de usuário para a compilação FBT.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1597">Note: There is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="e9ca8-1598">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1598">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1599">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1599">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1600">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1600">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1601">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1601">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-1602">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1602">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1603">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1603">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1604">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1604">modelId</span></span> |<span data-ttu-id="e9ca8-1605">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1605">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-1606">userId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1606">userId</span></span> |<span data-ttu-id="e9ca8-1607">Identificador exclusivo do usuário Olá</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1607">Unique identifier of hello user</span></span> |
| <span data-ttu-id="e9ca8-1608">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1608">numberOfResults</span></span> |<span data-ttu-id="e9ca8-1609">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="e9ca8-1609">Number of required results</span></span> |
| <span data-ttu-id="e9ca8-1610">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1610">includeMetatadata</span></span> |<span data-ttu-id="e9ca8-1611">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1611">Future use, always false</span></span> |
| <span data-ttu-id="e9ca8-1612">buildId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1612">buildId</span></span> |<span data-ttu-id="e9ca8-1613">Olá toouse id para esta solicitação de recomendação de compilação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1613">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="e9ca8-1614">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1614">apiVersion</span></span> |<span data-ttu-id="e9ca8-1615">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1615">1.0</span></span> |

<span data-ttu-id="e9ca8-1616">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1616">**Response:**</span></span>

<span data-ttu-id="e9ca8-1617">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1617">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-1618">resposta de saudação inclui uma entrada por itens recomendados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1618">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="e9ca8-1619">Cada entrada tem Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1619">Each entry has hello following data:</span></span>

* <span data-ttu-id="e9ca8-1620">`Feed\entry\content\properties\Id` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1620">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="e9ca8-1621">`Feed\entry\content\properties\Name`-Nome do item de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1621">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="e9ca8-1622">`Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1622">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="e9ca8-1623">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1623">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="e9ca8-1624">Veja um exemplo de resposta no 12.1</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1624">See a response example in 12.1</span></span>

### <a name="128-get-user-recommendations-with-item-list-of-a-specific-build"></a><span data-ttu-id="e9ca8-1625">12.8.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1625">12.8.</span></span> <span data-ttu-id="e9ca8-1626">Obtenha Recomendações de Usuário com a lista de itens (de uma compilação específica)</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1626">Get User Recommendations with item list (of a specific build)</span></span>
<span data-ttu-id="e9ca8-1627">Obter recomendações de usuário de uma versão específica do tipo "Recomendação" e a lista de saudação de itens adicionais.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1627">Get user recommendations of a specific build of type "Recommendation" and hello list of additional items.</span></span>

<span data-ttu-id="e9ca8-1628">Retorna uma lista de item previsto, de acordo com toohello histórico de uso do usuário hello e uma lista de itens adicional Olá Olá API.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1628">hello API will return a list of predicted item according toohello usage history of hello user and hello additional list of items.</span></span>

<span data-ttu-id="e9ca8-1629">Observação: Não há nenhuma recomendação de usuário para a compilação FBT.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1629">Note: Tthere is no user recommendation for FBT build.</span></span>

| <span data-ttu-id="e9ca8-1630">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1630">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1631">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1631">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1632">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1632">GET</span></span> |`<rootURI>/UserRecommend?modelId=%27<modelId>%27&userId=%27<userId>%27&itemsIds=%27<itemsIds>%27&numberOfResults=<int>&includeMetadata=<bool>&buildId=<int>&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1633">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1633">Example:</span></span><br>`<rootURI>/UserRecommend?modelId=%272779c063-48fb-46c1-bae3-74acddc8c1d1%27&userId=%27u1101%27&itemsIds=%271003%27&numberOfResults=10&includeMetadata=false&buildId=50012&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-1634">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1634">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1635">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1635">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1636">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1636">modelId</span></span> |<span data-ttu-id="e9ca8-1637">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1637">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-1638">userId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1638">userId</span></span> |<span data-ttu-id="e9ca8-1639">Identificador exclusivo do usuário Olá</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1639">Unique identifier of hello user</span></span> |
| <span data-ttu-id="e9ca8-1640">itemIds</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1640">itemIds</span></span> |<span data-ttu-id="e9ca8-1641">Lista separada por vírgulas de saudação itens toorecommend para.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1641">Comma-separated list of hello items toorecommend for.</span></span> <span data-ttu-id="e9ca8-1642">Comprimento máximo: 1024</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1642">Max length: 1024</span></span> |
| <span data-ttu-id="e9ca8-1643">numberOfResults</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1643">numberOfResults</span></span> |<span data-ttu-id="e9ca8-1644">Número de resultados necessários </span><span class="sxs-lookup"><span data-stu-id="e9ca8-1644">Number of required results</span></span> |
| <span data-ttu-id="e9ca8-1645">includeMetatadata</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1645">includeMetatadata</span></span> |<span data-ttu-id="e9ca8-1646">Uso futuro, sempre falso</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1646">Future use, always false</span></span> |
| <span data-ttu-id="e9ca8-1647">buildId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1647">buildId</span></span> |<span data-ttu-id="e9ca8-1648">Olá toouse id para esta solicitação de recomendação de compilação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1648">hello build id toouse for this recommendation request</span></span> |
| <span data-ttu-id="e9ca8-1649">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1649">apiVersion</span></span> |<span data-ttu-id="e9ca8-1650">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1650">1.0</span></span> |

<span data-ttu-id="e9ca8-1651">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1651">**Response:**</span></span>

<span data-ttu-id="e9ca8-1652">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1652">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-1653">resposta de saudação inclui uma entrada por itens recomendados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1653">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="e9ca8-1654">Cada entrada tem Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1654">Each entry has hello following data:</span></span>

* <span data-ttu-id="e9ca8-1655">`Feed\entry\content\properties\Id` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1655">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="e9ca8-1656">`Feed\entry\content\properties\Name`-Nome do item de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1656">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="e9ca8-1657">`Feed\entry\content\properties\Rating`-Classificação de recomendação de saudação; número mais alto significa maior confiança.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1657">`Feed\entry\content\properties\Rating` - Rating of hello recommendation; higher number means higher confidence.</span></span>
* <span data-ttu-id="e9ca8-1658">`Feed\entry\content\properties\Reasoning` - Raciocínio da recomendação (por exemplo, explicações de recomendação).</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1658">`Feed\entry\content\properties\Reasoning` - Recommendation reasoning (e.g. recommendation explanations).</span></span>

<span data-ttu-id="e9ca8-1659">Veja um exemplo de resposta no 12.1</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1659">See a response example in 12.1</span></span>

## <a name="13-user-usage-history"></a><span data-ttu-id="e9ca8-1660">13. Histórico de uso do usuário</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1660">13. User Usage History</span></span>
<span data-ttu-id="e9ca8-1661">Após a criação de um modelo de recomendação foi sistema Olá permitirá tooretrieve Olá histórico do usuário (usuário específico de itens tooa associado) usado para compilação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1661">Once a recommendation model was built hello system will allow tooretrieve hello user history (items associated tooa specific user) used for hello build.</span></span>
<span data-ttu-id="e9ca8-1662">Essa API permite histórico do usuário Olá tooretrieve</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1662">This API allow tooretrieve hello user history</span></span>

<span data-ttu-id="e9ca8-1663">Observação: histórico de saudação do usuário está atualmente disponível apenas para compilações de recomendação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1663">Note: hello user history is currently available only for recommendation builds.</span></span>

### <a name="131-retrieve-user-history"></a><span data-ttu-id="e9ca8-1664">13.1 Recuperar o histórico do usuário</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1664">13.1 Retrieve user history</span></span>
<span data-ttu-id="e9ca8-1665">Recuperar Olá lista de item usado na Olá active compilar ou no hello especificado compilar para Olá id de usuário fornecida.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1665">Retrieve hello list of item used in hello active build or in hello specified build for hello given user id.</span></span>

| <span data-ttu-id="e9ca8-1666">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1666">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1667">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1667">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1668">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1668">GET</span></span> |<span data-ttu-id="e9ca8-1669">Obter o histórico de saudação do usuário para compilação active hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1669">Get hello user history for hello active build.</span></span><br/>`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&apiVersion=%271.0%27`<br/><br/><span data-ttu-id="e9ca8-1670">Obter o histórico de saudação do usuário para Olá fornecido compilação`<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1670">Get hello user history for hello given build `<rootURI>/GetUserHistory?modelId=%27<model_id>%27&userId=%27<userId>%27&buildId=<int>&apiVersion=%271.0%27`</span></span><br/><br/><span data-ttu-id="e9ca8-1671">Exemplo:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1671">Example:`<rootURI>/GetUserHistory?modelId=%2727967136e8-f868-4258-9331-10d567f87fae%27&&userId=%27u_1013%27&apiVersion=%271.0%277`</span></span> |

| <span data-ttu-id="e9ca8-1672">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1672">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1673">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1673">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1674">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1674">modelId</span></span> |<span data-ttu-id="e9ca8-1675">Olá identificador exclusivo do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1675">hello unique identifier of hello model.</span></span> |
| <span data-ttu-id="e9ca8-1676">userId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1676">userId</span></span> |<span data-ttu-id="e9ca8-1677">Identificador exclusivo de saudação do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1677">hello unique identifier of hello user.</span></span> |
| <span data-ttu-id="e9ca8-1678">buildId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1678">buildId</span></span> |<span data-ttu-id="e9ca8-1679">parâmetro opcional, permitir tooindicate de qual compilação histórico de saudação do usuário deve ser busca</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1679">optional parameter, allow tooindicate from which build hello user history should be fetch</span></span> |
| <span data-ttu-id="e9ca8-1680">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1680">apiVersion</span></span> |<span data-ttu-id="e9ca8-1681">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1681">1.0</span></span> |

<span data-ttu-id="e9ca8-1682">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1682">**Response:**</span></span>

<span data-ttu-id="e9ca8-1683">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1683">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-1684">resposta de saudação inclui uma entrada por itens recomendados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1684">hello response includes one entry per recommended item.</span></span> <span data-ttu-id="e9ca8-1685">Cada entrada tem Olá seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1685">Each entry has hello following data:</span></span>

* <span data-ttu-id="e9ca8-1686">`Feed\entry\content\properties\Id` - ID do item recomendado.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1686">`Feed\entry\content\properties\Id` - Recommended item ID.</span></span>
* <span data-ttu-id="e9ca8-1687">`Feed\entry\content\properties\Name`-Nome do item de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1687">`Feed\entry\content\properties\Name` - Name of hello item.</span></span>
* <span data-ttu-id="e9ca8-1688">`Feed\entry\content\properties\Rating` - N/A.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1688">`Feed\entry\content\properties\Rating` - N/A.</span></span>
* <span data-ttu-id="e9ca8-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1689">`Feed\entry\content\properties\Reasoning` - N/A.</span></span>

<span data-ttu-id="e9ca8-1690">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1690">OData XML</span></span>

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

## <a name="14-notifications"></a><span data-ttu-id="e9ca8-1691">14. Notificações</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1691">14. Notifications</span></span>
<span data-ttu-id="e9ca8-1692">Recomendações de aprendizado de máquina do Azure cria notificações quando ocorrem erros persistentes no sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1692">Azure Machine Learning Recommendations creates notifications when persistent errors happen in hello system.</span></span> <span data-ttu-id="e9ca8-1693">Há três tipos de notificações:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1693">There are 3 types of notifications:</span></span>

1. <span data-ttu-id="e9ca8-1694">Falha na compilação – Essa notificação é disparada para cada falha de compilação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1694">Build failure - This notification is triggered for every build failure.</span></span>
2. <span data-ttu-id="e9ca8-1695">Falha - esta notificação de processamento de aquisição de dados é disparada quando temos mais de 100 erros em Olá últimos 5 minutos no processamento de saudação de eventos de uso por modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1695">Data acquisition processing failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of usage events per model.</span></span>
3. <span data-ttu-id="e9ca8-1696">Falha de consumo de recomendação - essa notificação é disparada quando temos mais de 100 erros em Olá últimos 5 minutos no processamento de saudação de solicitações de recomendação por modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1696">Recommendation consumption failure - This notification is triggered when we have more than 100 errors in hello last 5 minutes in hello processing of recommendation requests per model.</span></span>

### <a name="141-get-notifications"></a><span data-ttu-id="e9ca8-1697">14.1.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1697">14.1.</span></span> <span data-ttu-id="e9ca8-1698">Obter notificações</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1698">Get Notifications</span></span>
<span data-ttu-id="e9ca8-1699">Recupera todas as notificações de Olá para todos os modelos ou para um único modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1699">Retrieves all hello notifications for all models or for a single model.</span></span>

| <span data-ttu-id="e9ca8-1700">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1700">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1701">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1701">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1702">GET</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1702">GET</span></span> |`<rootURI>/GetNotifications?modelId=%27<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1703">Obter todas as notificações para todos os modelos:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1703">Getting all notifications for all models:</span></span><br>`<rootURI>/GetNotifications?apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1704">Exemplo para obter notificações para um modelo específico:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1704">Example for getting notifications for a specific model:</span></span><br>`<rootURI>/GetNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%277` |

| <span data-ttu-id="e9ca8-1705">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1705">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1706">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1706">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1707">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1707">modelId</span></span> |<span data-ttu-id="e9ca8-1708">Parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1708">Optional parameter.</span></span> <span data-ttu-id="e9ca8-1709">Quando omitido, você receberá todas as notificações para todos os modelos.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1709">When omitted, you will get all notifications for all models.</span></span> <br><span data-ttu-id="e9ca8-1710">Valor válido: o identificador exclusivo do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1710">Valid value: unique identifier of hello model.</span></span> |
| <span data-ttu-id="e9ca8-1711">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1711">apiVersion</span></span> |<span data-ttu-id="e9ca8-1712">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1712">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-1713">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1713">Request Body</span></span> |<span data-ttu-id="e9ca8-1714">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1714">NONE</span></span> |

<span data-ttu-id="e9ca8-1715">**Resposta:**</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1715">**Response:**</span></span>

<span data-ttu-id="e9ca8-1716">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1716">HTTP Status code: 200</span></span>

<span data-ttu-id="e9ca8-1717">XML de OData</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1717">OData XML</span></span>

    hello response includes one entry per notification. Each entry has hello following data:
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

### <a name="142-delete-model-notifications"></a><span data-ttu-id="e9ca8-1718">14.2.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1718">14.2.</span></span> <span data-ttu-id="e9ca8-1719">Excluir as notificações de modelo</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1719">Delete Model Notifications</span></span>
<span data-ttu-id="e9ca8-1720">Exclui todas notificações de leitura de um modelo.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1720">Deletes all read notifications for a model.</span></span>

| <span data-ttu-id="e9ca8-1721">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1721">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1722">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1722">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1723">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1723">DELETE</span></span> |`<rootURI>/DeleteModelNotifications?modelId=%<model_id>%27&apiVersion=%271.0%27`<br><br><span data-ttu-id="e9ca8-1724">Exemplo:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1724">Example:</span></span><br>`<rootURI>/DeleteModelNotifications?modelId=%27967136e8-f868-4258-9331-10d567f87fae%27&apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-1725">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1725">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1726">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1726">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1727">modelId</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1727">modelId</span></span> |<span data-ttu-id="e9ca8-1728">Identificador exclusivo do modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1728">Unique identifier of hello model</span></span> |
| <span data-ttu-id="e9ca8-1729">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1729">apiVersion</span></span> |<span data-ttu-id="e9ca8-1730">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1730">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-1731">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1731">Request Body</span></span> |<span data-ttu-id="e9ca8-1732">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1732">NONE</span></span> |

<span data-ttu-id="e9ca8-1733">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1733">**Response**:</span></span>

<span data-ttu-id="e9ca8-1734">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1734">HTTP Status code: 200</span></span>

### <a name="143-delete-user-notifications"></a><span data-ttu-id="e9ca8-1735">14.3.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1735">14.3.</span></span> <span data-ttu-id="e9ca8-1736">Excluir as notificações do usuário</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1736">Delete User Notifications</span></span>
<span data-ttu-id="e9ca8-1737">Exclui todas as notificações de todos os modelos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1737">Deletes all notifications for all models.</span></span>

| <span data-ttu-id="e9ca8-1738">Método HTTP</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1738">HTTP Method</span></span> | <span data-ttu-id="e9ca8-1739">URI</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1739">URI</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1740">EXCLUIR</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1740">DELETE</span></span> |`<rootURI>/DeleteUserNotifications?apiVersion=%271.0%27` |

| <span data-ttu-id="e9ca8-1741">Nome do Parâmetro</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1741">Parameter Name</span></span> | <span data-ttu-id="e9ca8-1742">Valores Válidos</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1742">Valid Values</span></span> |
|:--- |:--- |
| <span data-ttu-id="e9ca8-1743">apiVersion</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1743">apiVersion</span></span> |<span data-ttu-id="e9ca8-1744">1.0</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1744">1.0</span></span> |
|  | |
| <span data-ttu-id="e9ca8-1745">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1745">Request Body</span></span> |<span data-ttu-id="e9ca8-1746">NENHUM</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1746">NONE</span></span> |

<span data-ttu-id="e9ca8-1747">**Resposta**:</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1747">**Response**:</span></span>

<span data-ttu-id="e9ca8-1748">Código de status HTTP: 200</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1748">HTTP Status code: 200</span></span>

## <a name="15-legal"></a><span data-ttu-id="e9ca8-1749">15. Legal</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1749">15. Legal</span></span>
<span data-ttu-id="e9ca8-1750">Este documento é fornecido "no estado em que se encontra".</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1750">This document is provided “as-is”.</span></span> <span data-ttu-id="e9ca8-1751">Informações e opiniões expressadas neste documento, incluindo URLs e outras referências a sites da Internet, podem ser alteradas sem aviso prévio.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1751">Information and views expressed in this document, including URL and other Internet Web site references, may change without notice.</span></span><br><br>
<span data-ttu-id="e9ca8-1752">Alguns exemplos aqui representados são fornecidos somente para fins de ilustração e são fictícios.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1752">Some examples depicted herein are provided for illustration only and are fictitious.</span></span> <span data-ttu-id="e9ca8-1753">Nenhuma associação ou conexão real é intencional ou deve ser inferida.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1753">No real association or connection is intended or should be inferred.</span></span><br><br>
<span data-ttu-id="e9ca8-1754">Este documento não dá nenhum direito legal tooany de propriedade intelectual de nenhum produto da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1754">This document does not provide you with any legal rights tooany intellectual property in any Microsoft product.</span></span> <span data-ttu-id="e9ca8-1755">Você pode copiar e usar este documento para fins de consulta interna.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1755">You may copy and use this document for your internal, reference purposes.</span></span><br><br>
<span data-ttu-id="e9ca8-1756">© 2015 Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1756">© 2015 Microsoft.</span></span> <span data-ttu-id="e9ca8-1757">Todos os direitos reservados.</span><span class="sxs-lookup"><span data-stu-id="e9ca8-1757">All rights reserved.</span></span>

