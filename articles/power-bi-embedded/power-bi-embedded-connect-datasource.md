---
title: Microsoft Power BI Embedded - Conectando-se a uma fonte de dados
description: Power BI Embedded, conectar-se a fontes de dados
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 9f614bbc63eae788aa52132c8f0e42ad8963559a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-to-a-data-source"></a><span data-ttu-id="f29dd-103">Conectar-se a uma fonte de dados</span><span class="sxs-lookup"><span data-stu-id="f29dd-103">Connect to a data source</span></span>
<span data-ttu-id="f29dd-104">Com o **Power BI Embedded**, você pode inserir relatórios em seu próprio aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f29dd-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="f29dd-105">Quando você insere um relatório do Power BI em seu aplicativo, o relatório conecta-se aos dados subjacentes por meio da **importação** de uma cópia dos dados ou **conectando-se diretamente** à fonte de dados usando o **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="f29dd-105">When you embed a Power BI report into your app, the report connects to the underlying data by **importing** a copy of the data or by **connecting directly** to the data source using **DirectQuery**.</span></span>

<span data-ttu-id="f29dd-106">Estas são as diferenças entre o uso de **Importar** e **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="f29dd-106">Here are the differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="f29dd-107">Importar</span><span class="sxs-lookup"><span data-stu-id="f29dd-107">Import</span></span> | <span data-ttu-id="f29dd-108">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="f29dd-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="f29dd-109">Tabelas, colunas, *e dados* são importados ou copiados para o conjunto de dados do relatório.</span><span class="sxs-lookup"><span data-stu-id="f29dd-109">Tables, columns, *and data* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="f29dd-110">Para ver as alterações ocorridas nos dados subjacentes, você deve atualizar ou importar novamente um conjunto de dados completo e atual.</span><span class="sxs-lookup"><span data-stu-id="f29dd-110">To see changes that occurred to the underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="f29dd-111">Somente *tabelas e colunas* são importados ou copiados para o conjunto de dados do relatório.</span><span class="sxs-lookup"><span data-stu-id="f29dd-111">Only *tables and columns* are imported or copied into the report's dataset.</span></span> <span data-ttu-id="f29dd-112">Você sempre pode exibir os dados mais atuais.</span><span class="sxs-lookup"><span data-stu-id="f29dd-112">You always view the most current data.</span></span> |

<span data-ttu-id="f29dd-113">Com o Power BI Embedded, você pode usar DirectQuery com fontes de dados de nuvem, mas não em fontes de dados locais no momento.</span><span class="sxs-lookup"><span data-stu-id="f29dd-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="f29dd-114">Não há suporte para o Gateway de Dados Local com o Power BI Embedded no momento.</span><span class="sxs-lookup"><span data-stu-id="f29dd-114">The On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="f29dd-115">Isso significa que não é possível usar o DirectQuery com fontes de dados locais.</span><span class="sxs-lookup"><span data-stu-id="f29dd-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="f29dd-116">Fontes de dados com suporte</span><span class="sxs-lookup"><span data-stu-id="f29dd-116">Supported data sources</span></span>

<span data-ttu-id="f29dd-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="f29dd-117">**DirectQuery**</span></span>
* <span data-ttu-id="f29dd-118">Banco de Dados SQL Azure</span><span class="sxs-lookup"><span data-stu-id="f29dd-118">Azure SQL database</span></span>
* <span data-ttu-id="f29dd-119">SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="f29dd-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="f29dd-120">**Importaçãoação**</span><span class="sxs-lookup"><span data-stu-id="f29dd-120">**Import**</span></span>

<span data-ttu-id="f29dd-121">É possível importar usando todas as fontes de dados disponíveis dentro do Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="f29dd-121">You can import using all of the available data sources within Power BI Desktop.</span></span> <span data-ttu-id="f29dd-122">**Não** é possível atualizar esses dados dentro do Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="f29dd-122">You will **not** be able to refresh that data within Power BI Embedded.</span></span> <span data-ttu-id="f29dd-123">É necessário carregar as alterações feitas no arquivo PBIX no Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="f29dd-123">You will have to upload changes to your PBIX file to Power BI Embedded.</span></span> <span data-ttu-id="f29dd-124">Isso ocorre quando não há gateways disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f29dd-124">This is due to no available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="f29dd-125">Benefícios do uso do DirectQuery</span><span class="sxs-lookup"><span data-stu-id="f29dd-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="f29dd-126">Há duas vantagens principais ao usar **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="f29dd-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="f29dd-127">**DirectQuery** permite compilar visualizações em conjuntos de dados muito grandes nos quais, caso contrário, seria inviável importar primeiro todos os dados.</span><span class="sxs-lookup"><span data-stu-id="f29dd-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible to first import all of the data.</span></span>
* <span data-ttu-id="f29dd-128">Alterações de dados subjacentes podem exigir uma atualização de dados e, para alguns relatórios, a necessidade de exibir dados atuais pode exigir grandes transferências de dados, tornando a importação de dados novamente inviável.</span><span class="sxs-lookup"><span data-stu-id="f29dd-128">Underlying data changes can require a refresh of data, and for some reports, the need to display current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="f29dd-129">Por outro lado, relatórios do **DirectQuery** sempre usam dados atuais.</span><span class="sxs-lookup"><span data-stu-id="f29dd-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="f29dd-130">Limitações do DirectQuery</span><span class="sxs-lookup"><span data-stu-id="f29dd-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="f29dd-131">Há algumas limitações no uso do **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="f29dd-131">There are a few limitations to using **DirectQuery**:</span></span>

* <span data-ttu-id="f29dd-132">Todas as tabelas devem vir de um banco de dados individual.</span><span class="sxs-lookup"><span data-stu-id="f29dd-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="f29dd-133">Se a consulta for excessivamente complexa, ocorrerá um erro.</span><span class="sxs-lookup"><span data-stu-id="f29dd-133">If the query is overly complex, an error will occur.</span></span> <span data-ttu-id="f29dd-134">Para corrigir o erro, você deve refatorar a consulta para que se torne menos complexa.</span><span class="sxs-lookup"><span data-stu-id="f29dd-134">To remedy the error you must refactor the query so it is less complex.</span></span> <span data-ttu-id="f29dd-135">Se for necessário que a consulta seja complexa, você precisará importar os dados em vez de usar o **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="f29dd-135">If the query must be complex, you will need to import the data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="f29dd-136">Filtragem de relação é limitada a uma única direção, em vez de ambos os trajetos.</span><span class="sxs-lookup"><span data-stu-id="f29dd-136">Relationship filtering is limited to a single direction, rather than both directions.</span></span>
* <span data-ttu-id="f29dd-137">Você não pode alterar o tipo de dados de uma coluna.</span><span class="sxs-lookup"><span data-stu-id="f29dd-137">You cannot change the data type of a column.</span></span>
* <span data-ttu-id="f29dd-138">Por padrão, as limitações são colocadas em expressões DAX permitidas em medidas.</span><span class="sxs-lookup"><span data-stu-id="f29dd-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="f29dd-139">Consulte [DirectQuery e medidas](#measures).</span><span class="sxs-lookup"><span data-stu-id="f29dd-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="f29dd-140">DirectQuery e medidas</span><span class="sxs-lookup"><span data-stu-id="f29dd-140">DirectQuery and measures</span></span>
<span data-ttu-id="f29dd-141">Para garantir que as consultas enviadas à fonte de dados subjacente tenham um desempenho aceitável, limitações são impostas para as medidas.</span><span class="sxs-lookup"><span data-stu-id="f29dd-141">To ensure queries sent to the underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="f29dd-142">Ao usar o **Power BI Desktop**, usuários avançados podem optar por ignorar essa limitação, escolhendo **Arquivo > Opções e configurações > Opções**.</span><span class="sxs-lookup"><span data-stu-id="f29dd-142">When using **Power BI Desktop**, advanced users can choose to bypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="f29dd-143">Na caixa de diálogo **Opções**, escolha **DirectQuery** e selecione a opção **Permitir medidas irrestritas no modo DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="f29dd-143">In the **Options** dialog, choose **DirectQuery**, and select the option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="f29dd-144">Quando essa opção estiver selecionada, qualquer expressão DAX válida para uma determinada medida poderá ser usada.</span><span class="sxs-lookup"><span data-stu-id="f29dd-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="f29dd-145">No entanto, os usuários devem estar cientes de algumas expressões que funcionam muito bem quando os dados são importados podem resultar em consultas muito lentas para a origem de back-end no modo **DirectQuery** .</span><span class="sxs-lookup"><span data-stu-id="f29dd-145">Users must be aware; however, that some expressions that perform very well when the data is imported may result in very slow queries to the backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="f29dd-146">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f29dd-146">See Also</span></span>
* [<span data-ttu-id="f29dd-147">Introdução ao Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="f29dd-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="f29dd-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="f29dd-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="f29dd-149">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="f29dd-149">More questions?</span></span> [<span data-ttu-id="f29dd-150">Experimentar a comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="f29dd-150">Try the Power BI Community</span></span>](http://community.powerbi.com/)

