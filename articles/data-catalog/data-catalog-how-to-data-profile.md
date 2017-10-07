---
title: fontes de dados de perfil aaaHow tooData
description: "Tooarticle como realce como perfis de dados no nível de tabela e coluna tooinclude ao registrar fontes de dados no Data Catalog do Azure e como os perfis de dados toouse toounderstand fontes de dados."
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
ms.openlocfilehash: 12c9f38501cdaee903d0dcbbdd0b82395f35a187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-profile-data-sources"></a><span data-ttu-id="b6ab4-103">Fontes de dados de perfil de dados</span><span class="sxs-lookup"><span data-stu-id="b6ab4-103">Data profile data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="b6ab4-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="b6ab4-104">Introduction</span></span>
<span data-ttu-id="b6ab4-105">**Catálogo de Dados do Microsoft Azure** é um serviço de nuvem totalmente gerenciado que atua como um sistema de registro e sistema de descoberta em fontes de dados da empresa.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="b6ab4-106">Em outras palavras, **Data Catalog do Azure** é tudo sobre pessoas ajudando descobrir, entender e usar fontes de dados e ajudar as organizações tooget mais valor de seus dados existentes.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-106">In other words, **Azure Data Catalog** is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data.</span></span> <span data-ttu-id="b6ab4-107">Quando uma fonte de dados é registrada com **Data Catalog do Azure**, seus metadados são copiados e indexados pelo serviço de saudação, mas o texto de saudação não termina existe.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span>

<span data-ttu-id="b6ab4-108">Olá **criação de perfil de dados** recurso de **Data Catalog do Azure** examina Olá dados de fontes de dados com suporte no catálogo e coleta de estatísticas e informações sobre esses dados.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-108">hello **Data Profiling** feature of **Azure Data Catalog** examines hello data from supported data sources in your catalog and collects statistics and information about that data.</span></span> <span data-ttu-id="b6ab4-109">É fácil tooinclude um perfil de seus ativos de dados.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-109">It's easy tooinclude a profile of your data assets.</span></span> <span data-ttu-id="b6ab4-110">Quando você registra um ativo de dados, escolha **incluir dados de perfil** na ferramenta de registro de fonte de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-110">When you register a data asset, choose **Include Data Profile** in hello data source registration tool.</span></span>

## <a name="what-is-data-profiling"></a><span data-ttu-id="b6ab4-111">O que é a criação de perfil de dados</span><span class="sxs-lookup"><span data-stu-id="b6ab4-111">What is Data Profiling</span></span>
<span data-ttu-id="b6ab4-112">Perfil de dados examina Olá dados na fonte de dados hello está sendo registrado e coleta de estatísticas e informações sobre esses dados.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-112">Data profiling examines hello data in hello data source being registered, and collects statistics and information about that data.</span></span> <span data-ttu-id="b6ab4-113">Durante a descoberta de fonte de dados, essas estatísticas podem ajudar a determinar a adequação de saudação do hello dados toosolve um problema de negócios.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-113">During data source discovery, these statistics can help you determine hello suitability of hello data toosolve their business problem.</span></span>

<!-- In [How toodiscover data sources](data-catalog-how-to-discover.md), you learn about **Azure Data Catalog's** extensive search capabilities including searching for data assets that have a profile. See [How tooinclude a data profile when registering a data source](#howto). -->

<span data-ttu-id="b6ab4-114">Olá seguintes fontes de dados oferecem suporte a criação de perfil de dados:</span><span class="sxs-lookup"><span data-stu-id="b6ab4-114">hello following data sources support data profiling:</span></span>

* <span data-ttu-id="b6ab4-115">Tabelas e exibições do SQL Server (incluindo o Banco de Dados SQL do Azure e o Azure SQL Data Warehouse)</span><span class="sxs-lookup"><span data-stu-id="b6ab4-115">SQL Server (including Azure SQL DB and Azure SQL Data Warehouse) tables and views</span></span>
* <span data-ttu-id="b6ab4-116">Tabelas e exibições do oracle</span><span class="sxs-lookup"><span data-stu-id="b6ab4-116">Oracle tables and views</span></span>
* <span data-ttu-id="b6ab4-117">Tabelas e exibições do Teradata</span><span class="sxs-lookup"><span data-stu-id="b6ab4-117">Teradata tables and views</span></span>
* <span data-ttu-id="b6ab4-118">Tabelas do Hive</span><span class="sxs-lookup"><span data-stu-id="b6ab4-118">Hive tables</span></span>

<span data-ttu-id="b6ab4-119">A inclusão de perfis de dados ao registrar ativos de dados ajuda os usuários a responder a perguntas sobre fontes de dados, incluindo:</span><span class="sxs-lookup"><span data-stu-id="b6ab4-119">Including data profiles when registering data assets helps users answer questions about data sources, including:</span></span>

* <span data-ttu-id="b6ab4-120">Pode ser usado toosolve meu problema de negócios?</span><span class="sxs-lookup"><span data-stu-id="b6ab4-120">Can it be used toosolve my business problem?</span></span>
* <span data-ttu-id="b6ab4-121">Dados de saudação está em conformidade tooparticular padrões ou padrões?</span><span class="sxs-lookup"><span data-stu-id="b6ab4-121">Does hello data conform tooparticular standards or patterns?</span></span>
* <span data-ttu-id="b6ab4-122">Quais são alguns dos anomalias Olá Olá da fonte de dados?</span><span class="sxs-lookup"><span data-stu-id="b6ab4-122">What are some of hello anomalies of hello data source?</span></span>
* <span data-ttu-id="b6ab4-123">Quais são os possíveis desafios de integração desses dados a meu aplicativo?</span><span class="sxs-lookup"><span data-stu-id="b6ab4-123">What are possible challenges of integrating this data into my application?</span></span>

> [!NOTE]
> <span data-ttu-id="b6ab4-124">Você também pode adicionar documentação tooan ativo toodescribe como os dados podem ser integrados em um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-124">You can also add documentation tooan asset toodescribe how data could be integrated into an application.</span></span> <span data-ttu-id="b6ab4-125">Consulte [como fontes de dados de toodocument](data-catalog-how-to-documentation.md).</span><span class="sxs-lookup"><span data-stu-id="b6ab4-125">See [How toodocument data sources](data-catalog-how-to-documentation.md).</span></span>
>
>

<a name="howto"/>

## <a name="how-tooinclude-a-data-profile-when-registering-a-data-source"></a><span data-ttu-id="b6ab4-126">Como tooinclude um dado de perfil ao registrar uma fonte de dados</span><span class="sxs-lookup"><span data-stu-id="b6ab4-126">How tooinclude a data profile when registering a data source</span></span>
<span data-ttu-id="b6ab4-127">É fácil tooinclude um perfil de sua fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-127">It's easy tooinclude a profile of your data source.</span></span> <span data-ttu-id="b6ab4-128">Quando você registra uma fonte de dados no hello **toobe objetos registrado** painel do registro da fonte de dados Olá ferramenta, escolher **incluir dados de perfil**.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-128">When you register a data source, in hello **Objects toobe registered** panel of hello data source registration tool, choose **Include Data Profile**.</span></span>

![](media/data-catalog-data-profile/data-catalog-register-profile.png)

<span data-ttu-id="b6ab4-129">Saiba mais sobre toolearn como tooregister fontes de dados, consulte [como fontes de dados de tooregister](data-catalog-how-to-register.md) e [Introdução ao Data Catalog do Azure](data-catalog-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b6ab4-129">toolearn more about how tooregister data sources, see [How tooregister data sources](data-catalog-how-to-register.md) and [Get started with Azure Data Catalog](data-catalog-get-started.md).</span></span>

## <a name="filtering-on-data-assets-that-include-data-profiles"></a><span data-ttu-id="b6ab4-130">Filtragem de ativos de dados que incluem perfis de dados</span><span class="sxs-lookup"><span data-stu-id="b6ab4-130">Filtering on data assets that include data profiles</span></span>
<span data-ttu-id="b6ab4-131">toodiscover os ativos de dados que incluem um perfil de dados, você pode incluir `has:tableDataProfiles` ou `has:columnsDataProfiles` como um dos seus termos de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-131">toodiscover data assets that include a data profile, you can include `has:tableDataProfiles` or `has:columnsDataProfiles` as one of your search terms.</span></span>

> [!NOTE]
> <span data-ttu-id="b6ab4-132">Selecionando **incluir dados de perfil** nos dados Olá ferramenta de registro de origem inclui a tabela e informações de perfil de nível de coluna.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-132">Selecting **Include Data Profile** in hello data source registration tool includes both table and column-level profile information.</span></span> <span data-ttu-id="b6ab4-133">No entanto, hello API de catálogo de dados permite toobe de ativos de dados registrado com apenas um conjunto de informações de perfil incluídas.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-133">However, hello Data Catalog API allows data assets toobe registered with only one set of profile information included.</span></span>
>
>

## <a name="viewing-data-profile-information"></a><span data-ttu-id="b6ab4-134">Exibição de informações de perfil de dados</span><span class="sxs-lookup"><span data-stu-id="b6ab4-134">Viewing data profile information</span></span>
<span data-ttu-id="b6ab4-135">Depois de encontrar uma fonte de dados adequado com um perfil, você pode exibir detalhes do perfil de dados hello.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-135">Once you find a suitable data source with a profile, you can view hello data profile details.</span></span> <span data-ttu-id="b6ab4-136">dados de saudação tooview perfil, selecione um ativo de dados e escolha **perfil de dados** na janela portal do catálogo de dados hello.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-136">tooview hello data profile, select a data asset and choose **Data Profile** in hello Data Catalog portal window.</span></span>

![](media/data-catalog-data-profile/data-catalog-view.png)

<span data-ttu-id="b6ab4-137">Um perfil de dados no **Catálogo de Dados do Azure** mostra informações de perfil de tabela e coluna, incluindo:</span><span class="sxs-lookup"><span data-stu-id="b6ab4-137">A data profile in **Azure Data Catalog** shows table and column profile information including:</span></span>

### <a name="object-data-profile"></a><span data-ttu-id="b6ab4-138">Perfil de dados de objeto</span><span class="sxs-lookup"><span data-stu-id="b6ab4-138">Object data profile</span></span>
* <span data-ttu-id="b6ab4-139">Número de linhas</span><span class="sxs-lookup"><span data-stu-id="b6ab4-139">Number of rows</span></span>
* <span data-ttu-id="b6ab4-140">Tamanho de tabela</span><span class="sxs-lookup"><span data-stu-id="b6ab4-140">Table size</span></span>
* <span data-ttu-id="b6ab4-141">Quando Olá última atualização do objeto</span><span class="sxs-lookup"><span data-stu-id="b6ab4-141">When hello object was last updated</span></span>

### <a name="column-data-profile"></a><span data-ttu-id="b6ab4-142">Perfil de dados de coluna</span><span class="sxs-lookup"><span data-stu-id="b6ab4-142">Column data profile</span></span>
* <span data-ttu-id="b6ab4-143">Tipo de dados de coluna</span><span class="sxs-lookup"><span data-stu-id="b6ab4-143">Column data type</span></span>
* <span data-ttu-id="b6ab4-144">Número de valores distintos</span><span class="sxs-lookup"><span data-stu-id="b6ab4-144">Number of distinct values</span></span>
* <span data-ttu-id="b6ab4-145">Número de linhas com valores NULL</span><span class="sxs-lookup"><span data-stu-id="b6ab4-145">Number of rows with NULL values</span></span>
* <span data-ttu-id="b6ab4-146">Desvio mínimo, máximo, médio e padrão para valores de colunas</span><span class="sxs-lookup"><span data-stu-id="b6ab4-146">Minimum, maximum, average, and standard deviation for column values</span></span>

## <a name="summary"></a><span data-ttu-id="b6ab4-147">Resumo</span><span class="sxs-lookup"><span data-stu-id="b6ab4-147">Summary</span></span>
<span data-ttu-id="b6ab4-148">Dados de criação de perfil fornece estatísticas e informações sobre registrados dados ativos toohelp determinar adequação Olá Olá dados toosolve problemas de negócios.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-148">Data profiling provides statistics and information about registered data assets toohelp you determine hello suitability of hello data toosolve business problems.</span></span> <span data-ttu-id="b6ab4-149">Além de anotar e documentar fontes de dados, os perfis de dados podem dar aos usuários uma compreensão mais profunda dos dados.</span><span class="sxs-lookup"><span data-stu-id="b6ab4-149">Along with annotating, and documenting data sources, data profiles can give users a deeper understanding of your data.</span></span>

## <a name="see-also"></a><span data-ttu-id="b6ab4-150">Consulte também</span><span class="sxs-lookup"><span data-stu-id="b6ab4-150">See Also</span></span>
* [<span data-ttu-id="b6ab4-151">Como tooregister fontes de dados</span><span class="sxs-lookup"><span data-stu-id="b6ab4-151">How tooregister data sources</span></span>](data-catalog-how-to-register.md)
* [<span data-ttu-id="b6ab4-152">Introdução ao Catálogo de Dados do Azure</span><span class="sxs-lookup"><span data-stu-id="b6ab4-152">Get started with Azure Data Catalog</span></span>](data-catalog-get-started.md)
