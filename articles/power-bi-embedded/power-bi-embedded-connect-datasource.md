---
title: aaaMicrosoft Power BI inserido - conectar fonte de dados tooa
description: Power BI inserido, conecte-se a fontes de toodata
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
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a><span data-ttu-id="66e73-103">Conecte-se a fonte de dados tooa</span><span class="sxs-lookup"><span data-stu-id="66e73-103">Connect tooa data source</span></span>
<span data-ttu-id="66e73-104">Com o **Power BI Embedded**, você pode inserir relatórios em seu próprio aplicativo.</span><span class="sxs-lookup"><span data-stu-id="66e73-104">With **Power BI Embedded**, you can embed reports into your own app.</span></span> <span data-ttu-id="66e73-105">Quando você insere um relatório do Power BI em seu aplicativo, o relatório de saudação se conecta toohello base de dados por **importando** uma cópia dos dados de saudação ou por **conectando diretamente** toohello fonte de dados usando  **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="66e73-105">When you embed a Power BI report into your app, hello report connects toohello underlying data by **importing** a copy of hello data or by **connecting directly** toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="66e73-106">Aqui estão Olá diferenças entre usar **importação** e **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="66e73-106">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="66e73-107">Importar</span><span class="sxs-lookup"><span data-stu-id="66e73-107">Import</span></span> | <span data-ttu-id="66e73-108">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="66e73-108">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="66e73-109">Tabelas, colunas, *e dados* são importados ou copiados para o conjunto de dados do relatório hello.</span><span class="sxs-lookup"><span data-stu-id="66e73-109">Tables, columns, *and data* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="66e73-110">toosee altera os dados subjacentes toohello ocorreu, você deve atualizar ou importar novamente um dataset completo e atual.</span><span class="sxs-lookup"><span data-stu-id="66e73-110">toosee changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="66e73-111">Somente *tabelas e colunas* são importados ou copiados para o conjunto de dados do relatório hello.</span><span class="sxs-lookup"><span data-stu-id="66e73-111">Only *tables and columns* are imported or copied into hello report's dataset.</span></span> <span data-ttu-id="66e73-112">Você sempre pode exibir dados mais atuais da saudação.</span><span class="sxs-lookup"><span data-stu-id="66e73-112">You always view hello most current data.</span></span> |

<span data-ttu-id="66e73-113">Com o Power BI Embedded, você pode usar DirectQuery com fontes de dados de nuvem, mas não em fontes de dados locais no momento.</span><span class="sxs-lookup"><span data-stu-id="66e73-113">With Power BI Embedded, you can use DirectQuery with cloud data sources but not on-premises data sources at this time.</span></span>

> [!NOTE]
> <span data-ttu-id="66e73-114">Olá Gateway de dados no local não é suportado com o Power BI inserido no momento.</span><span class="sxs-lookup"><span data-stu-id="66e73-114">hello On-Premises Data Gateway is not supported with Power BI Embedded at this time.</span></span> <span data-ttu-id="66e73-115">Isso significa que não é possível usar o DirectQuery com fontes de dados locais.</span><span class="sxs-lookup"><span data-stu-id="66e73-115">This means you cannot use DirectQuery with on-premises data sources.</span></span>

## <a name="supported-data-sources"></a><span data-ttu-id="66e73-116">Fontes de dados com suporte</span><span class="sxs-lookup"><span data-stu-id="66e73-116">Supported data sources</span></span>

<span data-ttu-id="66e73-117">**DirectQuery**</span><span class="sxs-lookup"><span data-stu-id="66e73-117">**DirectQuery**</span></span>
* <span data-ttu-id="66e73-118">Banco de Dados SQL Azure</span><span class="sxs-lookup"><span data-stu-id="66e73-118">Azure SQL database</span></span>
* <span data-ttu-id="66e73-119">SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="66e73-119">Azure SQL Data Warehouse</span></span>

<span data-ttu-id="66e73-120">**Importaçãoação**</span><span class="sxs-lookup"><span data-stu-id="66e73-120">**Import**</span></span>

<span data-ttu-id="66e73-121">Você pode importar usando todas as fontes de dados disponíveis Olá no Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="66e73-121">You can import using all of hello available data sources within Power BI Desktop.</span></span> <span data-ttu-id="66e73-122">Você vai **não** ser capaz de toorefresh esses dados no Power BI inserido.</span><span class="sxs-lookup"><span data-stu-id="66e73-122">You will **not** be able toorefresh that data within Power BI Embedded.</span></span> <span data-ttu-id="66e73-123">Você terá as alterações de tooupload tooyour PBIX arquivo tooPower BI inserido.</span><span class="sxs-lookup"><span data-stu-id="66e73-123">You will have tooupload changes tooyour PBIX file tooPower BI Embedded.</span></span> <span data-ttu-id="66e73-124">Isso é devido gateway disponível toono.</span><span class="sxs-lookup"><span data-stu-id="66e73-124">This is due toono available gateway.</span></span> 

## <a name="benefits-of-using-directquery"></a><span data-ttu-id="66e73-125">Benefícios do uso do DirectQuery</span><span class="sxs-lookup"><span data-stu-id="66e73-125">Benefits of using DirectQuery</span></span>
<span data-ttu-id="66e73-126">Há duas vantagens principais ao usar **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="66e73-126">There are two primary benefits when using **DirectQuery**:</span></span>

* <span data-ttu-id="66e73-127">**DirectQuery** Olá de permite que você cria visualizações de conjuntos de dados muito grandes, onde caso contrário, seria impraticável toofirst importar todos os dados.</span><span class="sxs-lookup"><span data-stu-id="66e73-127">**DirectQuery** lets you build visualizations over very large datasets, where it otherwise would be unfeasible toofirst import all of hello data.</span></span>
* <span data-ttu-id="66e73-128">Alterações de dados subjacentes podem exigir uma atualização de dados e para alguns relatórios, hello precisam de dados atuais toodisplay pode exigir transferências de dados grandes, tornando os dados de reimportação impraticável.</span><span class="sxs-lookup"><span data-stu-id="66e73-128">Underlying data changes can require a refresh of data, and for some reports, hello need toodisplay current data can require large data transfers, making re-importing data unfeasible.</span></span> <span data-ttu-id="66e73-129">Por outro lado, relatórios do **DirectQuery** sempre usam dados atuais.</span><span class="sxs-lookup"><span data-stu-id="66e73-129">By contrast, **DirectQuery** reports always use current data.</span></span>

## <a name="limitations-of-directquery"></a><span data-ttu-id="66e73-130">Limitações do DirectQuery</span><span class="sxs-lookup"><span data-stu-id="66e73-130">Limitations of DirectQuery</span></span>
   <span data-ttu-id="66e73-131">Há alguns toousing de limitações **DirectQuery**:</span><span class="sxs-lookup"><span data-stu-id="66e73-131">There are a few limitations toousing **DirectQuery**:</span></span>

* <span data-ttu-id="66e73-132">Todas as tabelas devem vir de um banco de dados individual.</span><span class="sxs-lookup"><span data-stu-id="66e73-132">All tables must come from a single database.</span></span>
* <span data-ttu-id="66e73-133">Se a consulta de saudação for excessivamente complexa, ocorrerá um erro.</span><span class="sxs-lookup"><span data-stu-id="66e73-133">If hello query is overly complex, an error will occur.</span></span> <span data-ttu-id="66e73-134">Erro de saudação tooremedy deve refatorar consulta Olá é menos complexo.</span><span class="sxs-lookup"><span data-stu-id="66e73-134">tooremedy hello error you must refactor hello query so it is less complex.</span></span> <span data-ttu-id="66e73-135">Se Olá consulta deve ser complexa, você terá dados de saudação tooimport em vez de usar **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="66e73-135">If hello query must be complex, you will need tooimport hello data instead of using **DirectQuery**.</span></span>
* <span data-ttu-id="66e73-136">A filtragem de relação é limitada tooa única direção, em vez de ambas as direções.</span><span class="sxs-lookup"><span data-stu-id="66e73-136">Relationship filtering is limited tooa single direction, rather than both directions.</span></span>
* <span data-ttu-id="66e73-137">Não é possível alterar o tipo de dados de saudação de uma coluna.</span><span class="sxs-lookup"><span data-stu-id="66e73-137">You cannot change hello data type of a column.</span></span>
* <span data-ttu-id="66e73-138">Por padrão, as limitações são colocadas em expressões DAX permitidas em medidas.</span><span class="sxs-lookup"><span data-stu-id="66e73-138">By default, limitations are placed on DAX expressions allowed in measures.</span></span> <span data-ttu-id="66e73-139">Consulte [DirectQuery e medidas](#measures).</span><span class="sxs-lookup"><span data-stu-id="66e73-139">See [DirectQuery and measures](#measures).</span></span>

<a name="measures"/>

## <a name="directquery-and-measures"></a><span data-ttu-id="66e73-140">DirectQuery e medidas</span><span class="sxs-lookup"><span data-stu-id="66e73-140">DirectQuery and measures</span></span>
<span data-ttu-id="66e73-141">consultas de tooensure enviadas toohello fonte de dados têm um desempenho aceitável, são impostas limitações às medidas.</span><span class="sxs-lookup"><span data-stu-id="66e73-141">tooensure queries sent toohello underlying data source have acceptable performance, limitations are imposed on measures.</span></span> <span data-ttu-id="66e73-142">Ao usar **Power BI Desktop**avançado os usuários podem escolher essa limitação de toobypass escolhendo **arquivo > Opções e configurações > Opções**.</span><span class="sxs-lookup"><span data-stu-id="66e73-142">When using **Power BI Desktop**, advanced users can choose toobypass this limitation by choosing **File > Options and settings > Options**.</span></span> <span data-ttu-id="66e73-143">Em Olá **opções** caixa de diálogo, escolha **DirectQuery**e selecione a opção de saudação **permitir medidas irrestritas no modo DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="66e73-143">In hello **Options** dialog, choose **DirectQuery**, and select hello option **Allow unrestricted measures in DirectQuery mode**.</span></span> <span data-ttu-id="66e73-144">Quando essa opção estiver selecionada, qualquer expressão DAX válida para uma determinada medida poderá ser usada.</span><span class="sxs-lookup"><span data-stu-id="66e73-144">When that option is selected, any DAX expression that is valid for a measure can be used.</span></span> <span data-ttu-id="66e73-145">Os usuários devem estar cientes; No entanto, que algumas expressões que funcionam muito bem quando os dados de saudação são importados pode resultar em consultas muito lentas toohello backend de origem no **DirectQuery** modo.</span><span class="sxs-lookup"><span data-stu-id="66e73-145">Users must be aware; however, that some expressions that perform very well when hello data is imported may result in very slow queries toohello backend source when in **DirectQuery** mode.</span></span> 

## <a name="see-also"></a><span data-ttu-id="66e73-146">Consulte também</span><span class="sxs-lookup"><span data-stu-id="66e73-146">See Also</span></span>
* [<span data-ttu-id="66e73-147">Introdução ao Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="66e73-147">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)
* [<span data-ttu-id="66e73-148">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="66e73-148">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

<span data-ttu-id="66e73-149">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="66e73-149">More questions?</span></span> [<span data-ttu-id="66e73-150">Tente Olá comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="66e73-150">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

