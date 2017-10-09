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
# <a name="how-tooview-related-data-assets-in-azure-data-catalog"></a>Como tooview relacionados ativos de dados no catálogo de dados do Azure?
Catálogo de dados do Azure permite que você tooview dados ativos relacionados tooa selecionado dados ativos e exibir relações entre elas. 

## <a name="supported-data-sources"></a>Fontes de dados com suporte 
Ao registrar os ativos de dados de saudação fontes de dados a seguir, o Data Catalog do Azure registra automaticamente metadados sobre as relações de junção entre os ativos de dados de saudação selecionado. 

- SQL Server
- Banco de Dados SQL do Azure
- MySQL
- Oracle

## <a name="view-related-data-assets"></a>Exibir ativos de dados relacionados
tooview ativos de dados que são o conjunto de dados relacionados tooa selecionado, use Olá **relações** guia conforme Olá a imagem a seguir: 

![Catálogo de Dados do Azure – exibir ativos de dados relacionados](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

Neste exemplo, existem duas relações para Olá selecionado **ProductSubcategory** ativo de dados: 

- Coluna ProductSubcategoryID da tabela de produto Olá tem uma relação de chave estrangeira com a coluna ProductSubcategoryID da tabela ProductSubcategory de saudação selecionada. 
- Coluna ProductCategoryID da tabela ProductSubCategory de saudação tem uma relação de chave estrangeira com a coluna ProductCategoryID da tabela de ProductCategory Olá selecionado.

> [!NOTE]
> Observe a direção de saudação de seta Olá Olá relações na exibição em árvore.  

toosee mais detalhes como o nome totalmente qualificado de saudação da coluna hello, mova mouse Olá sobre e você verá um toohello semelhante pop-up imagem a seguir: 

![Catálogo de Dados do Azure – pop-up de relação](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

tooinclude relações entre os ativos que já tem sido registrados, registre novamente esses ativos.

## <a name="next-steps"></a>Próximas etapas
- [Como os ativos de dados toomanage](data-catalog-how-to-manage.md)
