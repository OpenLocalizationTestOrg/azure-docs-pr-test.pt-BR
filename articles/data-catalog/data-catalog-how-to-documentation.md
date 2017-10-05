---
title: Como documentar fontes de dados | Microsoft Docs
description: "Artigo de instruções que destaca como documentar ativos de dados no Catálogo de Dados do Azure."
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
ms.openlocfilehash: ffe951f60afb57524568fe1ed3b3668d0088e124
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="document-data-sources"></a><span data-ttu-id="b779a-103">Fontes de dados de documentos</span><span class="sxs-lookup"><span data-stu-id="b779a-103">Document data sources</span></span>
## <a name="introduction"></a><span data-ttu-id="b779a-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="b779a-104">Introduction</span></span>
<span data-ttu-id="b779a-105">**Catálogo de Dados do Microsoft Azure** é um serviço de nuvem totalmente gerenciado que atua como um sistema de registro e sistema de descoberta em fontes de dados da empresa.</span><span class="sxs-lookup"><span data-stu-id="b779a-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="b779a-106">Em outras palavras, o **Catálogo de Dados do Azure** ajuda as pessoas a descobrir, *entender*e usar fontes de dados, ajudando as empresas a obter mais valor de seus dados existentes.</span><span class="sxs-lookup"><span data-stu-id="b779a-106">In other words, **Azure Data Catalog** is all about helping people discover, *understand*, and use data sources, and helping organizations to get more value from their existing data.</span></span>

<span data-ttu-id="b779a-107">Quando uma fonte de dados é registrada no **Catálogo de Dados do Azure**, seus metadados são copiados e indexados pelo serviço, mas a história não para por aí.</span><span class="sxs-lookup"><span data-stu-id="b779a-107">When a data source is registered with **Azure Data Catalog**, its metadata is copied and indexed by the service, but the story doesn’t end there.</span></span> <span data-ttu-id="b779a-108">**Catálogo de Dados do Azure** também permite que os usuários forneçam sua própria documentação completa que pode descrever o uso e cenários comuns para a fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="b779a-108">**Azure Data Catalog** also allows users to provide their own complete documentation that can describe the usage and common scenarios for the data source.</span></span>

<span data-ttu-id="b779a-109">Em [Como anotar fontes de dados](data-catalog-how-to-annotate.md), você aprenderá que especialistas que conhecem a fonte de dados podem fazer anotações nela com marcas e uma descrição.</span><span class="sxs-lookup"><span data-stu-id="b779a-109">In [How to annotate data sources](data-catalog-how-to-annotate.md), you learn that experts who know the data source can annotate it with tags and a description.</span></span> <span data-ttu-id="b779a-110">O portal do **Catálogo de Dados do Azure** inclui um editor de texto avançado para que os usuários possam documentar totalmente contêineres e ativos de dados.</span><span class="sxs-lookup"><span data-stu-id="b779a-110">The **Azure Data Catalog** portal includes a rich text editor so that users can fully document data assets and containers.</span></span> <span data-ttu-id="b779a-111">O editor inclui formatação de parágrafo, como cabeçalhos, formatação de texto, listas com marcadores, listas numeradas e tabelas.</span><span class="sxs-lookup"><span data-stu-id="b779a-111">The editor includes paragraph formatting, such as headings, text formatting, bulleted lists, numbered lists, and tables.</span></span>

<span data-ttu-id="b779a-112">Marcas e descrições são ótimas para anotações simples.</span><span class="sxs-lookup"><span data-stu-id="b779a-112">Tags and descriptions are great for simple annotations.</span></span> <span data-ttu-id="b779a-113">No entanto, para ajudar os consumidores de dados a entender melhor o uso de uma fonte de dados e cenários de negócios para uma fonte de dados, um especialista pode fornecer documentação completa e detalhada.</span><span class="sxs-lookup"><span data-stu-id="b779a-113">However, to help data consumers better understand the use of a data source, and business scenarios for a data source, an expert can provide complete, detailed documentation.</span></span> <span data-ttu-id="b779a-114">É fácil documentar uma fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="b779a-114">It's easy to document a data source.</span></span> <span data-ttu-id="b779a-115">Selecione um ativo de dados ou um contêiner e escolha **Documentação**.</span><span class="sxs-lookup"><span data-stu-id="b779a-115">Select a data asset or container, and choose **Documentation**.</span></span>

![](media/data-catalog-documentation/data-catalog-documentation.png)

## <a name="documenting-data-assets"></a><span data-ttu-id="b779a-116">Documentar ativos de dados</span><span class="sxs-lookup"><span data-stu-id="b779a-116">Documenting data assets</span></span>
<span data-ttu-id="b779a-117">O benefício da documentação do **Catálogo de Dados do Azure** permite que você use seu Catálogo de Dados como um repositório de conteúdo para criar uma narrativa completa de seus ativos de dados.</span><span class="sxs-lookup"><span data-stu-id="b779a-117">The benefit of **Azure Data Catalog** documentation allows you to use your Data Catalog as a content repository to create a complete narrative of your data assets.</span></span> <span data-ttu-id="b779a-118">Você pode explorar o conteúdo detalhado que descreve contêineres e tabelas.</span><span class="sxs-lookup"><span data-stu-id="b779a-118">You can explore detailed content that describes containers and tables.</span></span> <span data-ttu-id="b779a-119">Se já tem conteúdo em outro repositório de conteúdo, como o SharePoint ou um compartilhamento de arquivos, você pode adicionar ao ativo links de documentação para fazer referência a esse conteúdo existente.</span><span class="sxs-lookup"><span data-stu-id="b779a-119">If you already have content in another content repository, such as SharePoint or a file share, you can add to the asset documentation links to reference this existing content.</span></span> <span data-ttu-id="b779a-120">Esse recurso torna os documentos existentes mais detectáveis.</span><span class="sxs-lookup"><span data-stu-id="b779a-120">This feature makes your existing documents more discoverable.</span></span>

> [!NOTE]
> <span data-ttu-id="b779a-121">A documentação não está incluída no índice de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b779a-121">Documentation is not included in search index.</span></span>
>
>

![](media/data-catalog-documentation/data-catalog-documentation2.png)

<span data-ttu-id="b779a-122">O nível de documentação pode variar desde a descrição das características e do valor de um contêiner de ativos de dados até uma descrição detalhada do esquema de tabela em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="b779a-122">The level of documentation can range from describing the characteristics and value of a data asset container to a detailed description of table schema within a container.</span></span> <span data-ttu-id="b779a-123">O nível da documentação fornecido deve ser orientado por suas necessidades comerciais.</span><span class="sxs-lookup"><span data-stu-id="b779a-123">The level of documentation provided should be driven by your business needs.</span></span> <span data-ttu-id="b779a-124">Porém, em geral, aqui estão alguns prós e contras para a documentação de ativos de dados:</span><span class="sxs-lookup"><span data-stu-id="b779a-124">But in general, here are a few pros and cons of documenting data assets:</span></span>

* <span data-ttu-id="b779a-125">Documentar apenas um contêiner: todo o conteúdo está em um local, mas talvez não tenha os detalhes necessários para que os usuários a tomem uma decisão embasada.</span><span class="sxs-lookup"><span data-stu-id="b779a-125">Document just a container: All the content is in one place, but might lack necessary details for users to make an informed decision.</span></span>
* <span data-ttu-id="b779a-126">Documentar apenas as tabelas: o conteúdo é específico para o objeto, mas os usuários têm vários lugares para documentos.</span><span class="sxs-lookup"><span data-stu-id="b779a-126">Document just the tables: Content is specific to that object, but your users have multiple places for documents.</span></span>
* <span data-ttu-id="b779a-127">Documentar tabelas e contêineres: essa é uma abordagem mais abrangente, mas pode exigir mais manutenção dos documentos.</span><span class="sxs-lookup"><span data-stu-id="b779a-127">Document containers and tables: Most comprehensive approach, but might introduce more maintenance of the documents.</span></span>

## <a name="summary"></a><span data-ttu-id="b779a-128">Resumo</span><span class="sxs-lookup"><span data-stu-id="b779a-128">Summary</span></span>
<span data-ttu-id="b779a-129">A documentação de fontes de dados com o **Catálogo de Dados do Azure** pode criar uma narrativa sobre seus ativos de dados com todos os detalhes necessários.</span><span class="sxs-lookup"><span data-stu-id="b779a-129">Documenting data sources with **Azure Data Catalog** can create a narrative about your data assets in as much detail as you need.</span></span>  <span data-ttu-id="b779a-130">Usando links, você pode vincular ao conteúdo armazenado em um repositório de conteúdo existente, que reúne os documentos e os ativos de dados existentes.</span><span class="sxs-lookup"><span data-stu-id="b779a-130">By using links, you can link to content stored in an existing content repository, which brings your existing docs and data assets together.</span></span> <span data-ttu-id="b779a-131">Depois que os usuários descobrirem ativos de dados apropriados, eles poderão ter um conjunto completo de documentação.</span><span class="sxs-lookup"><span data-stu-id="b779a-131">Once your users discover appropriate data assets, they can have a complete set of documentation.</span></span>
