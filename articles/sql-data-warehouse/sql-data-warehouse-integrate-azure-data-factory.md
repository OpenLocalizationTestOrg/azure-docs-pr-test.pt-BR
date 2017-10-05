---
title: Usar o Azure Data Factory com o SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: 7cd113f4a92635bc68253c2beb165ad1f0c96569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a>Use o Azure Data Factory com o SQL Data Warehouse
O Azure Data Factory fornece um método totalmente gerenciado para orquestrar a transferência de dados e a execução de procedimentos armazenados no SQL Data Warehouse.  Isso permitirá que você configure e programe mais facilmente procedimentos complexos de Extração, Transformação e Carga (ELT) com o SQL Data Warehouse. Para obter uma visão mais completa do Azure Data Factory, consulte a [documentação do Azure Data Factory][Azure Data Factory documentation].

## <a name="data-movement"></a>Movimentação de dados
O Azure Data Factory permite a movimentação de dados entre fontes locais e diferentes serviços do Azure.  De forma geral, a integração atual com o Azure Data Factory oferece suporte à movimentação de dados de e para os seguintes locais:

* Armazenamento do blob do Azure
* Banco de Dados SQL Azure
* SQL Server local
* SQL Server na IaaS

Para obter informações sobre como configurar uma atividade de cópia de dados, veja [Copiar dados com o Azure Data Factory][Copy data with Azure Data Factory]

## <a name="stored-procedures"></a>Procedimentos Armazenados
 Da mesma forma que ele pode ser usado para agendar a transferência de dados, o Azure Data Factory também pode ser usado para coordenar a execução de procedimentos armazenados.  Isso permite que pipelines mais complexos sejam criados e estende a capacidade do Azure Data Factory de aproveitar o poder computacional do SQL Data Warehouse.

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

