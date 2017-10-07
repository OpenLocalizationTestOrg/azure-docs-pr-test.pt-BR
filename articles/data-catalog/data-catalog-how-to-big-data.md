---
title: toowork aaaHow com fontes de dados de 'dados grandes' | Microsoft Docs
description: "Padrões de realce tooarticle como para usar o catálogo de dados do Azure com fontes de dados de 'dados grandes', incluindo o armazenamento de BLOBs do Azure, Azure Data Lake e Hadoop HDFS."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 626d1568-0780-4726-bad1-9c5000c6b31a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: e478f71f26744975a7d7e1784b74bf50b424cf65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowork-with-big-data-sources-in-azure-data-catalog"></a><span data-ttu-id="184bc-103">Como fontes de toowork com dados grandes no catálogo de dados do Azure</span><span class="sxs-lookup"><span data-stu-id="184bc-103">How toowork with big data sources in Azure Data Catalog</span></span>
## <a name="introduction"></a><span data-ttu-id="184bc-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="184bc-104">Introduction</span></span>
<span data-ttu-id="184bc-105">**Catálogo de Dados do Microsoft Azure** é um serviço de nuvem totalmente gerenciado que atua como um sistema de registro e sistema de descoberta em fontes de dados da empresa.</span><span class="sxs-lookup"><span data-stu-id="184bc-105">**Microsoft Azure Data Catalog** is a fully managed cloud service that serves as a system of registration and system of discovery for enterprise data sources.</span></span> <span data-ttu-id="184bc-106">É tudo sobre ajudando as pessoas a descobrir, entender e usar fontes de dados e ajudando as organizações tooget mais valor de suas fontes de dados existentes, incluindo dados grandes.</span><span class="sxs-lookup"><span data-stu-id="184bc-106">It is all about helping people discover, understand, and use data sources, and helping organizations tooget more value from their existing data sources, including big data.</span></span>

<span data-ttu-id="184bc-107">**Catálogo de dados do Azure** suporta Olá registro de blobs de armazenamento de Blog do Azure, diretórios, bem como Hadoop HDFS arquivos e diretórios.</span><span class="sxs-lookup"><span data-stu-id="184bc-107">**Azure Data Catalog** supports hello registration of Azure Blog Storage blobs and directories as well as Hadoop HDFS files and directories.</span></span> <span data-ttu-id="184bc-108">a natureza semi-estruturados Olá dessas fontes de dados fornece uma grande flexibilidade.</span><span class="sxs-lookup"><span data-stu-id="184bc-108">hello semi-structured nature of these data sources provides great flexibility.</span></span> <span data-ttu-id="184bc-109">No entanto, tooget Olá máximo de registrando-os com **Data Catalog do Azure**, os usuários devem considerar como fontes de dados de saudação são organizados.</span><span class="sxs-lookup"><span data-stu-id="184bc-109">However, tooget hello most value from registering them with **Azure Data Catalog**, users must consider how hello data sources are organized.</span></span>

## <a name="directories-as-logical-data-sets"></a><span data-ttu-id="184bc-110">Diretórios como conjuntos de dados lógicos</span><span class="sxs-lookup"><span data-stu-id="184bc-110">Directories as logical data sets</span></span>
<span data-ttu-id="184bc-111">Um padrão comum para a organização de grandes fontes de dados é tootreat diretórios como conjuntos de dados lógicos.</span><span class="sxs-lookup"><span data-stu-id="184bc-111">A common pattern for organizing big data sources is tootreat directories as logical data sets.</span></span> <span data-ttu-id="184bc-112">Diretórios de alto nível são toodefine usado um conjunto de dados, enquanto as subpastas definem partições e arquivos Olá contiverem armazenam dados de saudação em si.</span><span class="sxs-lookup"><span data-stu-id="184bc-112">Top-level directories are used toodefine a data set, while subfolders define partitions, and hello files they contain store hello data itself.</span></span>

<span data-ttu-id="184bc-113">Um exemplo desse padrão pode ser:</span><span class="sxs-lookup"><span data-stu-id="184bc-113">An example of this pattern might be:</span></span>

    \vehicle_maintenance_events
        \2013
        \2014
        \2015
            \01
                \2015-01-trailer01.csv
                \2015-01-trailer92.csv
                \2015-01-canister9635.csv
                ...
    \location_tracking_events
        \2013
        ...

<span data-ttu-id="184bc-114">Neste exemplo, vehicle_maintenance_events e location_tracking_events representam conjuntos de dados lógicos.</span><span class="sxs-lookup"><span data-stu-id="184bc-114">In this example, vehicle_maintenance_events and location_tracking_events represent logical data sets.</span></span> <span data-ttu-id="184bc-115">Cada uma dessas pastas contém arquivos de dados organizados por ano e mês em subpastas.</span><span class="sxs-lookup"><span data-stu-id="184bc-115">Each of these folders contains data files that are organized by year and month into subfolders.</span></span> <span data-ttu-id="184bc-116">Cada uma dessas pastas pode conter, potencialmente, centenas ou milhares de arquivos.</span><span class="sxs-lookup"><span data-stu-id="184bc-116">Each of these folders could potentially contain hundreds or thousands of files.</span></span>

<span data-ttu-id="184bc-117">Nesse padrão, registrar arquivos individuais com o **Catálogo de Dados do Azure** provavelmente não faz sentido.</span><span class="sxs-lookup"><span data-stu-id="184bc-117">In this pattern, registering individual files with **Azure Data Catalog** probably does not make sense.</span></span> <span data-ttu-id="184bc-118">Em vez disso, registre diretórios Olá que representam os conjuntos de dados de saudação ser significativo toohello usuários trabalhando com dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="184bc-118">Instead, register hello directories that represent hello data sets that be meaningful toohello users working with hello data.</span></span>

## <a name="reference-data-files"></a><span data-ttu-id="184bc-119">Arquivos de dados de referência</span><span class="sxs-lookup"><span data-stu-id="184bc-119">Reference data files</span></span>
<span data-ttu-id="184bc-120">Um padrão de complementar é toostore conjuntos de dados de referência como arquivos individuais.</span><span class="sxs-lookup"><span data-stu-id="184bc-120">A complementary pattern is toostore reference data sets as individual files.</span></span> <span data-ttu-id="184bc-121">Esses conjuntos de dados pode ser pensados como lado de 'pequena' hello de big data e são geralmente toodimensions semelhante em um modelo de dados analíticos.</span><span class="sxs-lookup"><span data-stu-id="184bc-121">These data sets may be thought of as hello 'small' side of big data, and are often similar toodimensions in an analytical data model.</span></span> <span data-ttu-id="184bc-122">Arquivos de dados de referência contêm registros de contexto tooprovide usado para bulk Olá Olá dos arquivos de dados armazenados em outro lugar no repositório de dados grande hello.</span><span class="sxs-lookup"><span data-stu-id="184bc-122">Reference data files contain records that are used tooprovide context for hello bulk of hello data files stored elsewhere in hello big data store.</span></span>

<span data-ttu-id="184bc-123">Um exemplo desse padrão pode ser:</span><span class="sxs-lookup"><span data-stu-id="184bc-123">An example of this pattern might be:</span></span>

    \vehicles.csv
    \maintenance_facilities.csv
    \maintenance_types.csv

<span data-ttu-id="184bc-124">Quando um cientista de dados ou analista está trabalhando com dados de saudação contidos nas estruturas de diretório maior hello, dados Olá nesses arquivos de referência podem ser usado tooprovide informações mais detalhadas para entidades que são chamados tooonly por nome ou ID de dados maior Olá conjunto.</span><span class="sxs-lookup"><span data-stu-id="184bc-124">When an analyst or data scientist is working with hello data contained in hello larger directory structures, hello data in these reference files can be used tooprovide more detailed information for entities that are referred tooonly by name or ID in hello larger data set.</span></span>

<span data-ttu-id="184bc-125">Nesse padrão, isso faz sentido tooregister arquivos de dados de referência individual Olá com **Data Catalog do Azure**.</span><span class="sxs-lookup"><span data-stu-id="184bc-125">In this pattern, it makes sense tooregister hello individual reference data files with **Azure Data Catalog**.</span></span> <span data-ttu-id="184bc-126">Cada arquivo representa um conjunto de dados e cada um deles pode ser anotado e descoberto individualmente.</span><span class="sxs-lookup"><span data-stu-id="184bc-126">Each file represents a data set, and each one can be annotated and discovered individually.</span></span>

## <a name="alternate-patterns"></a><span data-ttu-id="184bc-127">Padrões alternativos</span><span class="sxs-lookup"><span data-stu-id="184bc-127">Alternate patterns</span></span>
<span data-ttu-id="184bc-128">padrões descritos em Olá anterior seção Hello são apenas duas maneiras possíveis de que um repositório de dados grandes pode ser organizado, mas cada implementação é diferente.</span><span class="sxs-lookup"><span data-stu-id="184bc-128">hello patterns described in hello preceding section are just two possible ways a big data store may be organized, but each implementation is different.</span></span> <span data-ttu-id="184bc-129">Independentemente de como as fontes de dados são estruturadas, ao registrar fontes de dados grandes com **Data Catalog do Azure**, enfocam registrando Olá arquivos e diretórios representam os conjuntos de dados de saudação do valor tooothers dentro de sua organização.</span><span class="sxs-lookup"><span data-stu-id="184bc-129">Regardless of how your data sources are structured, when registering big data sources with **Azure Data Catalog**, focus on registering hello files and directories that represent hello data sets that are of value tooothers within your organization.</span></span> <span data-ttu-id="184bc-130">Registrar todos os arquivos e diretórios pode sobrecarregar o catálogo hello, tornando mais difícil para os usuários toofind que precisam.</span><span class="sxs-lookup"><span data-stu-id="184bc-130">Registering all files and directories can clutter hello catalog, making it harder for users toofind what they need.</span></span>

## <a name="summary"></a><span data-ttu-id="184bc-131">Resumo</span><span class="sxs-lookup"><span data-stu-id="184bc-131">Summary</span></span>
<span data-ttu-id="184bc-132">Registrar fontes de dados com **Data Catalog do Azure** torna mais fácil toodiscover e entender.</span><span class="sxs-lookup"><span data-stu-id="184bc-132">Registering data sources with **Azure Data Catalog** makes them easier toodiscover and understand.</span></span> <span data-ttu-id="184bc-133">Registrando e anotar Olá dados grandes arquivos e diretórios representam os conjuntos de dados lógicos, você pode ajudar os usuários a localizar e utilizar Olá grandes fontes de dados que precisam.</span><span class="sxs-lookup"><span data-stu-id="184bc-133">By registering and annotating hello big data files and directories that represent logical data sets, you can help users find and use hello big data sources they need.</span></span>
