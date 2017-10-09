---
title: "aaaBuild soluções integradas com o SQL Data Warehouse | Microsoft Docs"
description: "Ferramentas e parceiros com soluções que podem ser integradas ao SQL Data Warehouse "
services: sql-data-warehouse
documentationcenter: NA
author: mlee3gsd
manager: jhubbard
editor: 
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: martinle;barbkess
ms.openlocfilehash: c8a4202dd84305bea4e4c2faf0e4791d026e794f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a>Aproveitar outros serviços com o SQL Data Warehouse
Além disso tooits funcionalidade de núcleo, SQL Data Warehouse permite que os usuários tooleverage muitas Olá outros serviços no Azure junto com ele.  Especificamente, podemos atualmente tomaram medidas toodeeply integrar com o seguinte hello:

* Power BI
* Fábrica de dados do Azure
* Azure Machine Learning
* Stream Analytics do Azure

Estamos trabalhando tooconnect com mais serviços em Olá ecossistema do Azure.

## <a name="power-bi"></a>Power BI
Integração do Power BI permite que você tooleverage capacidade de computação de saudação do SQL Data Warehouse com o relatório dinâmico Olá e visualização do Power BI. Atualmente, a integração do Power BI inclui:

* **Conexão direta**: uma conexão mais avançada com a aplicação de lógica no SQL Data Warehouse.  Isso fornece uma análise mais rápida em uma escala maior.
* **Abrir no Power BI**: botão 'Abrir no Power BI' hello passa informações de instância tooPower BI, permitindo uma conexão contínua.

Consulte [integrar com o Power BI](sql-data-warehouse-integrate-power-bi.md) ou hello [documentação do Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) para obter mais informações.

## <a name="azure-data-factory"></a>Fábrica de dados do Azure
A fábrica de dados do Azure oferece aos usuários um toocreate de plataforma gerenciado que complexas para extrair e carregar pipelines.  Integração do SQL Data Warehouse com o Azure Data Factory inclui o seguinte hello:

* **Procedimentos armazenados**: coordenar a execução de saudação de procedimentos armazenados no SQL Data Warehouse.
* **Cópia**: dados de toomove ADF de uso no SQL Data Warehouse.  Essa operação pode usar o mecanismo de movimentação de dados padrão do ADF ou PolyBase em Olá abrange. 

Consulte [integrar com o Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) ou hello [documentação do Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) para obter mais informações.

## <a name="azure-machine-learning"></a>Azure Machine Learning
O aprendizado de máquina do Azure é um serviço de análise totalmente gerenciado que permite aos usuários toocreate modelos complexos utilizando um grande conjunto de ferramentas de previsão.  SQL Data Warehouse tem suporte como uma origem e de destino para esses modelos com hello funcionalidade a seguir:

* **Ler Dados:** encaminhe modelos em escala usando o T-SQL no SQL Data Warehouse.
* **Dados de gravação:** confirmar alterações de qualquer modelo fazer tooSQL Data Warehouse.

Consulte [integrar com o aprendizado de máquina do Azure](sql-data-warehouse-integrate-azure-machine-learning.md) ou hello [documentação de aprendizado de máquina do Azure](https://azure.microsoft.com/services/machine-learning/) para obter mais informações.

## <a name="azure-stream-analytics"></a>Stream Analytics do Azure
O Stream Analytics do Azure é uma infraestrutura complexa, totalmente gerenciada para processamento e consumo de dados de eventos gerados por meio do hub de eventos do Azure.  Integração com o SQL Data Warehouse permite streaming toobe dados efetivamente processados e armazenados junto com dados relacionais, permitindo maior, mais análise avançada.  

* **Saída de trabalho:** enviar saída do Stream Analytics diretamente trabalhos tooSQL Data Warehouse.

Consulte [integrar com o Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) ou hello [documentação do Azure Stream Analytics](https://azure.microsoft.com/documentation/services/stream-analytics/) para obter mais informações.

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
