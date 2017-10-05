---
title: Como criar um perfil de dados para fontes de dados
description: "Artigo de instruções destacando como incluir os perfis de dados nos níveis da tabela e da coluna ao registrar as fontes de dados no Catálogo de Dados do Azure e como usar os perfis de dados para entender as fontes de dados."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 94a8274b-5c9c-4962-a4b1-2fed38a3d919
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 8f4174f0ed74706b8275c8b1f0a62753f2834fa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="a3d88-103">Fontes de dados de perfil de dados</span><span class="sxs-lookup"><span data-stu-id="a3d88-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="a3d88-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="a3d88-104">Introduction</span></span>
<span data-ttu-id="a3d88-105">**Catálogo de Dados do Microsoft Azure** é um serviço de nuvem totalmente gerenciado que atua como um sistema de registro e sistema de descoberta em fontes de dados da empresa.</span><span class="sxs-lookup"><span data-stu-id="a3d88-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="a3d88-106">Em outras palavras, o **Catálogo de Dados do Azure** ajuda as pessoas a descobrir, entender e usar fontes de dados, ajudando as empresas a obter mais valor de seus dados existentes.</span><span class="sxs-lookup"><span data-stu-id="a3d88-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations to get more value from their existing data.</span></span> <span data-ttu-id="a3d88-107">Quando uma fonte de dados é registrada no **Catálogo de Dados do Azure**, seus metadados são copiados e indexados pelo serviço, mas a história não para por aí.</span><span class="sxs-lookup"><span data-stu-id="a3d88-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span>

<span data-ttu-id="a3d88-108">O recurso **Criação do Perfil de Dados** do **Catálogo de Dados do Azure** examina os dados nas fontes de dados com suporte no catálogo e coleta estatísticas e informações sobre esses dados.</span><span class="sxs-lookup"><span data-stu-id="a3d88-108">The **Data Profiling** feature of **Azure Data Catalog** examines the data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="a3d88-109">É fácil incluir um perfil de seus ativos de dados.</span><span class="sxs-lookup"><span data-stu-id="a3d88-109">It's easy to include a profile of your data assets.</span></span> <span data-ttu-id="a3d88-110">Ao registrar um ativo de dados, escolha **Incluir Perfil de Dados** na ferramenta de registro de fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="a3d88-110">When you register a data asset, choose **Include Data Profile** in the data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="a3d88-111">O que é a criação de perfil de dados</span><span class="sxs-lookup"><span data-stu-id="a3d88-111">What is Data Profiling</span></span>
<span data-ttu-id="a3d88-112">A criação de perfil de dados examina os dados na fonte de dados que está sendo registrada e coleta estatísticas e informações sobre esses dados.</span><span class="sxs-lookup"><span data-stu-id="a3d88-112">Data profiling examines the data in the data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="a3d88-113">Durante a descoberta de fonte de dados, as estatísticas podem ajudar você a determinar a adequação dos dados para resolver seu problema de negócios.</span><span class="sxs-lookup"><span data-stu-id="a3d88-113">During data source discovery, these statistics can help you determine the suitability of the data to solve their business problem.</span></span>

<!-- In [How to discover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How to include a data profile when registering a data source](#howto). -->

<span data-ttu-id="a3d88-114">As seguintes fontes de dados dão suporte à criação de perfil de dados:</span><span class="sxs-lookup"><span data-stu-id="a3d88-114">The following data sources support data profiling:</span></span>

* <span data-ttu-id="a3d88-115">Tabelas e exibições do SQL Server (incluindo o Banco de Dados SQL do Azure e o Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="a3d88-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="a3d88-116">Tabelas e exibições do oracle</span><span class="sxs-lookup"><span data-stu-id="a3d88-116">Oracle tables and views</span></span>
* <span data-ttu-id="a3d88-117">Tabelas e exibições do Teradata</span><span class="sxs-lookup"><span data-stu-id="a3d88-117">Teradata tables and views</span></span>
* <span data-ttu-id="a3d88-118">Tabelas do Hive</span><span class="sxs-lookup"><span data-stu-id="a3d88-118">Hive tables</span></span>

<span data-ttu-id="a3d88-119">A inclusão de perfis de dados ao registrar ativos de dados ajuda os usuários a responder a perguntas sobre fontes de dados, incluindo:</span><span class="sxs-lookup"><span data-stu-id="a3d88-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="a3d88-120">Ele pode ser usado para resolver meu problema de negócios?</span><span class="sxs-lookup"><span data-stu-id="a3d88-120">Can it be used to solve my business problem?</span></span>
* <span data-ttu-id="a3d88-121">Os dados estão em conformidade com padrões específicos?</span><span class="sxs-lookup"><span data-stu-id="a3d88-121">Does the data conform to particular standards or patterns?</span></span>
* <span data-ttu-id="a3d88-122">Quais são algumas das anomalias da fonte de dados?</span><span class="sxs-lookup"><span data-stu-id="a3d88-122">What are some of the anomalies of the data source?</span></span>
* <span data-ttu-id="a3d88-123">Quais são os possíveis desafios de integração desses dados a meu aplicativo?</span><span class="sxs-lookup"><span data-stu-id="a3d88-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="a3d88-124">Você também pode adicionar documentação a um ativo para descrever como os dados podem ser integrados a um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a3d88-124">You can also add documentation to an asset to describe how data could be integrated into an application.</span></span> <span data-ttu-id="a3d88-125">Confira [Como documentar fontes de dados](data-catalog-how-to-documentation.md).</span><span class="sxs-lookup"><span data-stu-id="a3d88-125">See [How to document data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-to-include-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="a3d88-126">Como incluir um perfil de dados ao registrar uma fonte de dados</span><span class="sxs-lookup"><span data-stu-id="a3d88-126">How to include a data profile when registering a data source</span></span>
<span data-ttu-id="a3d88-127">É fácil incluir um perfil de sua fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="a3d88-127">It's easy to include a profile of your data source.</span></span> <span data-ttu-id="a3d88-128">Quando você registra uma fonte de dados, no painel **Objetos a ser registrados** da ferramenta de registro da fonte de dados, escolha **Incluir Perfil dos Dados**.</span><span class="sxs-lookup"><span data-stu-id="a3d88-128">When you register a data source, in the **Objects to be registered** panel of the data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="a3d88-129">Para saber mais sobre como registrar as fontes de dados, consulte [Como registrar as fontes de dados](data-catalog-how-to-register.md) e [Introdução ao Catálogo de Dados do Azure](data-catalog-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a3d88-129">To learn more about how to register data sources, see [How to register data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="a3d88-130">Filtragem de ativos de dados que incluem perfis de dados</span><span class="sxs-lookup"><span data-stu-id="a3d88-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="a3d88-131">Para descobrir ativos de dados que incluem um perfil de dados, você pode incluir `has:tableDataProfiles`ou `has:columnsDataProfiles`como um dos seus termos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="a3d88-131">To discover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="a3d88-132">A seleção de **Incluir Dados de Perfil** na ferramenta de registro de fonte de dados inclui informações de perfil de nível de coluna e da tabela.</span><span class="sxs-lookup"><span data-stu-id="a3d88-132">Selecting **Include Data Profile** in the data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="a3d88-133">No entanto, a API de Catálogo de Dados permite que os ativos de dados sejam registrados com um único conjunto de informações de perfil incluído.</span><span class="sxs-lookup"><span data-stu-id="a3d88-133">However, the Data Catalog API allows data assets to be registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="a3d88-134">Exibição de informações de perfil de dados</span><span class="sxs-lookup"><span data-stu-id="a3d88-134">Viewing data profile information</span></span>
<span data-ttu-id="a3d88-135">Depois de encontrar uma fonte de dados adequada com um perfil, você pode exibir os detalhes do perfil de dados.</span><span class="sxs-lookup"><span data-stu-id="a3d88-135">Once you find a suitable data source with a profile, you can view the data profile details.</span></span> <span data-ttu-id="a3d88-136">Para exibir o perfil de dados, selecione um ativo de dados e escolha **Perfil de Dados** na janela do portal do Catálogo de Dados.</span><span class="sxs-lookup"><span data-stu-id="a3d88-136">To view the data profile, select a data asset and choose **Data Profile** in the Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="a3d88-137">Um perfil de dados no **Catálogo de Dados do Azure** mostra informações de perfil de tabela e coluna, incluindo:</span><span class="sxs-lookup"><span data-stu-id="a3d88-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="a3d88-138">Perfil de dados de objeto</span><span class="sxs-lookup"><span data-stu-id="a3d88-138">Object data profile</span></span>
* <span data-ttu-id="a3d88-139">Número de linhas</span><span class="sxs-lookup"><span data-stu-id="a3d88-139">Number of rows</span></span>
* <span data-ttu-id="a3d88-140">Tamanho de tabela</span><span class="sxs-lookup"><span data-stu-id="a3d88-140">Table size</span></span>
* <span data-ttu-id="a3d88-141">Quando o objeto foi atualizado pela última vez</span><span class="sxs-lookup"><span data-stu-id="a3d88-141">When the object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="a3d88-142">Perfil de dados de coluna</span><span class="sxs-lookup"><span data-stu-id="a3d88-142">Column data profile</span></span>
* <span data-ttu-id="a3d88-143">Tipo de dados de coluna</span><span class="sxs-lookup"><span data-stu-id="a3d88-143">Column data type</span></span>
* <span data-ttu-id="a3d88-144">Número de valores distintos</span><span class="sxs-lookup"><span data-stu-id="a3d88-144">Number of distinct values</span></span>
* <span data-ttu-id="a3d88-145">Número de linhas com valores NULL</span><span class="sxs-lookup"><span data-stu-id="a3d88-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="a3d88-146">Desvio mínimo, máximo, médio e padrão para valores de colunas</span><span class="sxs-lookup"><span data-stu-id="a3d88-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="a3d88-147">Resumo</span><span class="sxs-lookup"><span data-stu-id="a3d88-147">Summary</span></span>
<span data-ttu-id="a3d88-148">A criação de perfil de dados fornece estatísticas e informações sobre ativos de dados registrados para ajudar você a determinar a adequação dos dados para solucionar problemas de negócios.</span><span class="sxs-lookup"><span data-stu-id="a3d88-148">Data profiling provides statistics and information about registered data assets to help you determine the suitability of the data to solve business problems.</span></span> <span data-ttu-id="a3d88-149">Além de anotar e documentar fontes de dados, os perfis de dados podem dar aos usuários uma compreensão mais profunda dos dados.</span><span class="sxs-lookup"><span data-stu-id="a3d88-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="a3d88-150">Consulte também</span><span class="sxs-lookup"><span data-stu-id="a3d88-150">See Also</span></span>
* [<span data-ttu-id="a3d88-151">Como registrar fontes de dados</span><span class="sxs-lookup"><span data-stu-id="a3d88-151">How to register data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="a3d88-152">Introdução ao Catálogo de Dados do Azure</span><span class="sxs-lookup"><span data-stu-id="a3d88-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
