---
title: "aaaHow tooview relacionados ativos de dados no catálogo de dados do Azure | Microsoft Docs"
description: "Este artigo explica como tooview relacionados ativos de dados de um ativo de dados selecionada no catálogo de dados do Azure."
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
ms.openlocfilehash: b69686737070ac563a0318f48e693215c605f90b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="73c5d-103">Como tooview relacionados ativos de dados no catálogo de dados do Azure?</span><span class="sxs-lookup"><span data-stu-id="73c5d-103">How tooview related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="73c5d-104">Catálogo de dados do Azure permite que você tooview dados ativos relacionados tooa selecionado dados ativos e exibir relações entre elas.</span><span class="sxs-lookup"><span data-stu-id="73c5d-104">Azure Data Catalog allows you tooview data assets related tooa selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="73c5d-105">Fontes de dados com suporte</span><span class="sxs-lookup"><span data-stu-id="73c5d-105">Supported data sources</span></span> 
<span data-ttu-id="73c5d-106">Ao registrar os ativos de dados de saudação fontes de dados a seguir, o Data Catalog do Azure registra automaticamente metadados sobre as relações de junção entre os ativos de dados de saudação selecionado.</span><span class="sxs-lookup"><span data-stu-id="73c5d-106">When you register data assets from hello following data sources, Azure Data Catalog automatically registers metadata about join relationships between hello selected data assets.</span></span> 

- <span data-ttu-id="73c5d-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="73c5d-107">SQL Server</span></span>
- <span data-ttu-id="73c5d-108">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="73c5d-108">Azure SQL Database</span></span>
- <span data-ttu-id="73c5d-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="73c5d-109">MySQL</span></span>
- <span data-ttu-id="73c5d-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="73c5d-110">Oracle</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="73c5d-111">Exibir ativos de dados relacionados</span><span class="sxs-lookup"><span data-stu-id="73c5d-111">View related data assets</span></span>
<span data-ttu-id="73c5d-112">tooview ativos de dados que são o conjunto de dados relacionados tooa selecionado, use Olá **relações** guia conforme Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="73c5d-112">tooview data assets that are related tooa selected dataset, use hello **Relationships** tab as shown in hello following image:</span></span> 

![Catálogo de Dados do Azure – exibir ativos de dados relacionados](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="73c5d-114">Neste exemplo, existem duas relações para Olá selecionado **ProductSubcategory** ativo de dados:</span><span class="sxs-lookup"><span data-stu-id="73c5d-114">In this example, there are two relationships for hello selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="73c5d-115">Coluna ProductSubcategoryID da tabela de produto Olá tem uma relação de chave estrangeira com a coluna ProductSubcategoryID da tabela ProductSubcategory de saudação selecionada.</span><span class="sxs-lookup"><span data-stu-id="73c5d-115">ProductSubcategoryID column of hello Product table has a foreign key relationship with ProductSubcategoryID column of hello selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="73c5d-116">Coluna ProductCategoryID da tabela ProductSubCategory de saudação tem uma relação de chave estrangeira com a coluna ProductCategoryID da tabela de ProductCategory Olá selecionado.</span><span class="sxs-lookup"><span data-stu-id="73c5d-116">ProductCategoryID column of hello ProductSubCategory table has a foreign key relationship with ProductCategoryID column of hello selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="73c5d-117">Observe a direção de saudação de seta Olá Olá relações na exibição em árvore.</span><span class="sxs-lookup"><span data-stu-id="73c5d-117">Notice hello direction of hello arrow in hello relationships tree view.</span></span>  

<span data-ttu-id="73c5d-118">toosee mais detalhes como o nome totalmente qualificado de saudação da coluna hello, mova mouse Olá sobre e você verá um toohello semelhante pop-up imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="73c5d-118">toosee more details such as hello fully qualified name of hello column, move hello mouse over and you see a popup similar toohello following image:</span></span> 

![Catálogo de Dados do Azure – pop-up de relação](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="73c5d-120">tooinclude relações entre os ativos que já tem sido registrados, registre novamente esses ativos.</span><span class="sxs-lookup"><span data-stu-id="73c5d-120">tooinclude relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73c5d-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="73c5d-121">Next steps</span></span>
- [<span data-ttu-id="73c5d-122">Como os ativos de dados toomanage</span><span class="sxs-lookup"><span data-stu-id="73c5d-122">How toomanage data assets</span></span>](data-catalog-how-to-manage.md)
