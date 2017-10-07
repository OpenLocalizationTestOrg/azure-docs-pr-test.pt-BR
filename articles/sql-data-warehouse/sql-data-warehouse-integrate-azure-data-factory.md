---
title: "Fábrica de dados do Azure SQL Data warehouse de aaaUse | Microsoft Docs"
description: "Dicas de utilização do  Azure Data Factory (ADF) com o Azure SQL Data Warehouse para o desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 492de762-c7a2-4cdb-943f-3135230e94f1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d40a547830f9681504253d39ae3066800a955c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a>Use o Azure Data Factory com o SQL Data Warehouse
A fábrica de dados do Azure fornece um método totalmente gerenciado para orquestrar a transferência de saudação de dados e execução de procedimentos armazenados no SQL Data Warehouse.  Isso permitirá que você toomore facilmente configurar e agendar extrair transformação e carregamento (ETL) procedimentos complexos com o SQL Data Warehouse. Para obter uma visão mais completa de fábrica de dados do Azure, consulte Olá [documentação do Azure Data Factory][Azure Data Factory documentation].

## <a name="data-movement"></a>Movimentação de dados
O Azure Data Factory permite a movimentação de dados entre fontes locais e diferentes serviços do Azure.  Integração geral atual com a fábrica de dados do Azure suporta tooand de movimentação de dados de saudação locais a seguir:

* Armazenamento do blob do Azure
* Banco de Dados SQL Azure
* SQL Server local
* SQL Server na IaaS

Para obter informações sobre como tooset backup de dados de um atividade de cópia consulte [copiar dados com o Azure Data Factory][Copy data with Azure Data Factory]

## <a name="stored-procedures"></a>Procedimentos Armazenados
 Em Olá mesmo maneira pode ser usado tooschedule de transferência de dados, pode Azure Data Factory também ser usadas tooorchestrate Olá execução de procedimentos armazenados.  Isso permite mais complexa toobe pipelines criado e se estende capacidade tooleverage Olá poder computacional do Azure Data Factory do SQL Data Warehouse.

## <a name="next-steps"></a>Próximas etapas
Para obter uma visão geral da integração, consulte [Visão geral de integração do SQL Data Warehouse][SQL Data Warehouse integration overview].
Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

