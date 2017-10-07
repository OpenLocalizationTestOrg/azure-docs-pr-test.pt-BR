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
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a><span data-ttu-id="0e4c1-103">Use o Azure Data Factory com o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="0e4c1-103">Use Azure Data Factory with SQL Data Warehouse</span></span>
<span data-ttu-id="0e4c1-104">A fábrica de dados do Azure fornece um método totalmente gerenciado para orquestrar a transferência de saudação de dados e execução de procedimentos armazenados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0e4c1-104">Azure Data Factory provides a fully managed method for orchestrating hello transfer of data and execution of stored procedures on SQL Data Warehouse.</span></span>  <span data-ttu-id="0e4c1-105">Isso permitirá que você toomore facilmente configurar e agendar extrair transformação e carregamento (ETL) procedimentos complexos com o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0e4c1-105">This will allow you toomore easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span></span> <span data-ttu-id="0e4c1-106">Para obter uma visão mais completa de fábrica de dados do Azure, consulte Olá [documentação do Azure Data Factory][Azure Data Factory documentation].</span><span class="sxs-lookup"><span data-stu-id="0e4c1-106">For a more complete overview of Azure Data Factory, see hello [Azure Data Factory documentation][Azure Data Factory documentation].</span></span>

## <a name="data-movement"></a><span data-ttu-id="0e4c1-107">Movimentação de dados</span><span class="sxs-lookup"><span data-stu-id="0e4c1-107">Data Movement</span></span>
<span data-ttu-id="0e4c1-108">O Azure Data Factory permite a movimentação de dados entre fontes locais e diferentes serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e4c1-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span></span>  <span data-ttu-id="0e4c1-109">Integração geral atual com a fábrica de dados do Azure suporta tooand de movimentação de dados de saudação locais a seguir:</span><span class="sxs-lookup"><span data-stu-id="0e4c1-109">Overall, current integration with Azure Data Factory supports data movement tooand from hello following locations:</span></span>

* <span data-ttu-id="0e4c1-110">Armazenamento do blob do Azure</span><span class="sxs-lookup"><span data-stu-id="0e4c1-110">Azure blob storage</span></span>
* <span data-ttu-id="0e4c1-111">Banco de Dados SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0e4c1-111">Azure SQL Database</span></span>
* <span data-ttu-id="0e4c1-112">SQL Server local</span><span class="sxs-lookup"><span data-stu-id="0e4c1-112">On-premises SQL Server</span></span>
* <span data-ttu-id="0e4c1-113">SQL Server na IaaS</span><span class="sxs-lookup"><span data-stu-id="0e4c1-113">SQL Server on IaaS</span></span>

<span data-ttu-id="0e4c1-114">Para obter informações sobre como tooset backup de dados de um atividade de cópia consulte [copiar dados com o Azure Data Factory][Copy data with Azure Data Factory]</span><span class="sxs-lookup"><span data-stu-id="0e4c1-114">For information on how tooset up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span></span>

## <a name="stored-procedures"></a><span data-ttu-id="0e4c1-115">Procedimentos Armazenados</span><span class="sxs-lookup"><span data-stu-id="0e4c1-115">Stored Procedures</span></span>
 <span data-ttu-id="0e4c1-116">Em Olá mesmo maneira pode ser usado tooschedule de transferência de dados, pode Azure Data Factory também ser usadas tooorchestrate Olá execução de procedimentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="0e4c1-116">In hello same way it can be used tooschedule data transfer, Azure Data Factory can also be used tooorchestrate hello execution of stored procedures.</span></span>  <span data-ttu-id="0e4c1-117">Isso permite mais complexa toobe pipelines criado e se estende capacidade tooleverage Olá poder computacional do Azure Data Factory do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0e4c1-117">This allows more complex pipelines toobe created and extends Azure Data Factory's ability tooleverage hello computational power of SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e4c1-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0e4c1-118">Next steps</span></span>
<span data-ttu-id="0e4c1-119">Para obter uma visão geral da integração, consulte [Visão geral de integração do SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="0e4c1-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>
<span data-ttu-id="0e4c1-120">Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="0e4c1-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

