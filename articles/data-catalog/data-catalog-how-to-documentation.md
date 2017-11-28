---
title: fontes de dados de toodocument aaaHow | Microsoft Docs
description: "Realce como tooarticle como toodocument ativos de dados no catálogo de dados do Azure."
services: data-catalog
documentationcenter: 
author: spelluru
manager: NA
editor: 
tags: 
ms.assetid: 053b1701-b848-4ada-b726-6f485caa9961
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: 4e46838d91ab4d0c0bc569ac526a0c729134bb10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="0d5c3-103">Fontes de dados de documentos</span><span class="sxs-lookup"><span data-stu-id="0d5c3-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="0d5c3-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="0d5c3-104">Introduction</span></span>
<span data-ttu-id="0d5c3-105">**Catálogo de Dados do Microsoft Azure** é um serviço de nuvem totalmente gerenciado que atua como um sistema de registro e sistema de descoberta em fontes de dados da empresa.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="0d5c3-106">Em outras palavras, **Data Catalog do Azure** é ajudar pessoas descobrir, *entender*e usar fontes de dados e ajudar as organizações tooget mais valor de seus dados existentes.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations tooget more value from their existing data.</span></span>

<span data-ttu-id="0d5c3-107">Quando uma fonte de dados é registrada com **Data Catalog do Azure**, seus metadados são copiados e indexados pelo serviço de saudação, mas o texto de saudação não termina existe.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by hello service, but hello story doesn’t end there.</span></span> <span data-ttu-id="0d5c3-108">**Catálogo de dados do Azure** também permite que os usuários tooprovide sua própria documentação completa que pode descrever o uso de saudação e cenários comuns de fonte de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-108">**Azure Data Catalog** also allows users tooprovide their own complete documentation that can describe hello usage and common scenarios for hello data source.</span></span>

<span data-ttu-id="0d5c3-109">Em [como fontes de dados de tooannotate](data-catalog-how-to-annotate.md), você aprenderá que especialistas que sabem a fonte de dados Olá podem anotar com marcas e uma descrição.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-109">In [How tooannotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know hello data source can annotate it with tags and a description.</span></span> <span data-ttu-id="0d5c3-110">Olá **Data Catalog do Azure** portal inclui um editor de rich text para que os usuários totalmente podem documentar ativos de dados e os contêineres.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-110">hello **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="0d5c3-111">editor de saudação inclui formatação, como títulos, formatação de texto, tabelas, listas numeradas e listas com marcadores de parágrafo.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-111">hello editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="0d5c3-112">Marcas e descrições são ótimas para anotações simples.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="0d5c3-113">No entanto, os consumidores de dados toohelp entender melhor o uso de saudação de uma fonte de dados e cenários de negócios para uma fonte de dados, um especialista podem fornecer a documentação completa e detalhada.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-113">However, toohelp data consumers better understand hello use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="0d5c3-114">É fácil toodocument uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-114">It's easy toodocument a data source.</span></span> <span data-ttu-id="0d5c3-115">Selecione um ativo de dados ou um contêiner e escolha **Documentação**.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="0d5c3-116">Documentar ativos de dados</span><span class="sxs-lookup"><span data-stu-id="0d5c3-116">Documenting data assets</span></span>
<span data-ttu-id="0d5c3-117">Olá benefício de **Data Catalog do Azure** documentação permite que você toouse seus dados de catálogo como um repositório de conteúdo toocreate uma narrativa completa de seus ativos de dados.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-117">hello benefit of **Azure Data Catalog** documentation allows you toouse your Data Catalog as a content repository toocreate a complete narrative of your data assets.</span></span> <span data-ttu-id="0d5c3-118">Você pode explorar o conteúdo detalhado que descreve contêineres e tabelas.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="0d5c3-119">Se você já tiver conteúdo em outro repositório de conteúdo, como o SharePoint ou um compartilhamento de arquivos, você pode adicionar toohello ativo documentação links tooreference este conteúdo existente.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-119">If you already have content in another content repository, such as SharePoint or a file share, you can add toohello asset documentation links tooreference this existing content.</span></span> <span data-ttu-id="0d5c3-120">Esse recurso torna os documentos existentes mais detectáveis.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="0d5c3-121">A documentação não está incluída no índice de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="0d5c3-122">Olá nível de documentação pode variar de descrever as características de saudação e o valor de dados de ativo contêiner tooa descrição detalhada do esquema de tabela dentro de um contêiner.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-122">hello level of documentation can range from describing hello characteristics and value of a data asset container tooa detailed description of table schema within a container.</span></span> <span data-ttu-id="0d5c3-123">nível de saudação da documentação fornecida deve ser orientada por suas necessidades de negócios.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-123">hello level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="0d5c3-124">Porém, em geral, aqui estão alguns prós e contras para a documentação de ativos de dados:</span><span class="sxs-lookup"><span data-stu-id="0d5c3-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="0d5c3-125">Apenas um contêiner de documento: todo o conteúdo de saudação está em um local, mas pode falta necessário detalhes para os usuários toomake uma decisão informada.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-125">Document just a container: All hello content is in one place, but might lack necessary details for users toomake an informed decision.</span></span>
* <span data-ttu-id="0d5c3-126">Apenas as tabelas de saudação de documentos: conteúdo é objeto toothat específico, mas os usuários têm vários locais para documentos.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-126">Document just hello tables: Content is specific toothat object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="0d5c3-127">Tabelas e os contêineres de documento: uma abordagem mais abrangente, mas podem apresentar mais de manutenção de documentos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of hello documents.</span></span>

## <a name="summary"></a><span data-ttu-id="0d5c3-128">Resumo</span><span class="sxs-lookup"><span data-stu-id="0d5c3-128">Summary</span></span>
<span data-ttu-id="0d5c3-129">A documentação de fontes de dados com o **Catálogo de Dados do Azure** pode criar uma narrativa sobre seus ativos de dados com todos os detalhes necessários.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="0d5c3-130">Usando os links, você pode vincular toocontent armazenado em um repositório de conteúdo existente, que reúne os documentos existentes e ativos de dados.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-130">By using links, you can link toocontent stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="0d5c3-131">Depois que os usuários descobrirem ativos de dados apropriados, eles poderão ter um conjunto completo de documentação.</span><span class="sxs-lookup"><span data-stu-id="0d5c3-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>
