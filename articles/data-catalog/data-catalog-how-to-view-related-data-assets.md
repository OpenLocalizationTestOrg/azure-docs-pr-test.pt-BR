---
title: "Como exibir ativos de dados relacionados no Catálogo de Dados do Azure | Microsoft Docs"
description: "Este artigo explica como exibir os ativos de dados relacionados de um ativo de dados selecionado no Catálogo de Dados do Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/17/2017
ms.author: maroche
ms.openlocfilehash: d45f2cabe712a7982f99a9d280fed4494fc4d377
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-view-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="71383-103">Como exibir ativos de dados relacionados no Catálogo de Dados do Azure?</span><span class="sxs-lookup"><span data-stu-id="71383-103">How to view related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="71383-104">O Catálogo de Dados do Azure permite que você exiba os ativos de dados relacionados a um ativo de dados selecionado exiba as relações entre eles.</span><span class="sxs-lookup"><span data-stu-id="71383-104">Azure Data Catalog allows you to view data assets related to a selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="71383-105">Fontes de dados com suporte</span><span class="sxs-lookup"><span data-stu-id="71383-105">Supported data sources</span></span> 
<span data-ttu-id="71383-106">Quando você registra os ativos de dados das fontes de dados a seguir, o Catálogo de Dados do Azure registra automaticamente metadados sobre as relações de união entre os ativos de dados selecionados.</span><span class="sxs-lookup"><span data-stu-id="71383-106">When you register data assets from the following data sources, Azure Data Catalog automatically registers metadata about join relationships between the selected data assets.</span></span> 

- <span data-ttu-id="71383-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="71383-107">SQL Server</span></span>
- <span data-ttu-id="71383-108">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="71383-108">Azure SQL Database</span></span>
- <span data-ttu-id="71383-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="71383-109">MySQL</span></span>
- <span data-ttu-id="71383-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="71383-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="71383-111">Exibir ativos de dados relacionados</span><span class="sxs-lookup"><span data-stu-id="71383-111">View related data assets</span></span>
<span data-ttu-id="71383-112">Para exibir os ativos de dados relacionados a um conjunto de dados selecionado, use a guia **Relações** conforme mostrado na imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="71383-112">To view data assets that are related to a selected dataset, use the **Relationships** tab as shown in the following image:</span></span> 

![Catálogo de Dados do Azure – exibir ativos de dados relacionados](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="71383-114">Neste exemplo, existem duas relações para o ativo de dados **ProductSubcategory** selecionado:</span><span class="sxs-lookup"><span data-stu-id="71383-114">In this example, there are two relationships for the selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="71383-115">A coluna ProductSubcategoryID da tabela Produto tem uma relação de chave estrangeira com a coluna ProductSubcategoryID da tabela ProductSubcategory selecionada.</span><span class="sxs-lookup"><span data-stu-id="71383-115">ProductSubcategoryID column of the Product table has a foreign key relationship with ProductSubcategoryID column of the selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="71383-116">A coluna ProductCategoryID da tabela ProductSubCategory tem uma relação de chave estrangeira com a coluna ProductCategoryID da tabela ProductCategory selecionada.</span><span class="sxs-lookup"><span data-stu-id="71383-116">ProductCategoryID column of the ProductSubCategory table has a foreign key relationship with ProductCategoryID column of the selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="71383-117">Observe a direção da seta na exibição de árvore de relações.</span><span class="sxs-lookup"><span data-stu-id="71383-117">Notice the direction of the arrow in the relationships tree view.</span></span>  

<span data-ttu-id="71383-118">Para ver mais detalhes, como o nome totalmente qualificado da coluna, mova o mouse sobre ela e você verá um pop-up semelhante à imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="71383-118">To see more details such as the fully qualified name of the column, move the mouse over and you see a popup similar to the following image:</span></span> 

![Catálogo de Dados do Azure – pop-up de relação](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="71383-120">Para incluir relações entre os ativos que já foram registrados, registre novamente esses ativos.</span><span class="sxs-lookup"><span data-stu-id="71383-120">To include relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71383-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="71383-121">Next steps</span></span>
- [<span data-ttu-id="71383-122">Como gerenciar ativos de dados</span><span class="sxs-lookup"><span data-stu-id="71383-122">How to manage data assets</span></span>](data-catalog-how-to-manage.md)