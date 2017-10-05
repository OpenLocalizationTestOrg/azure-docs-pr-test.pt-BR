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
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a><span data-ttu-id="57f66-103">Use o Azure Data Factory com o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="57f66-103">Use Azure Data Factory with SQL Data Warehouse</span></span>
<span data-ttu-id="57f66-104">O Azure Data Factory fornece um método totalmente gerenciado para orquestrar a transferência de dados e a execução de procedimentos armazenados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="57f66-104">Azure Data Factory provides a fully managed method for orchestrating the transfer of data and execution of stored procedures on SQL Data Warehouse.</span></span>  <span data-ttu-id="57f66-105">Isso permitirá que você configure e programe mais facilmente procedimentos complexos de Extração, Transformação e Carga (ELT) com o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="57f66-105">This will allow you to more easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span></span> <span data-ttu-id="57f66-106">Para obter uma visão mais completa do Azure Data Factory, consulte a [documentação do Azure Data Factory][Azure Data Factory documentation].</span><span class="sxs-lookup"><span data-stu-id="57f66-106">For a more complete overview of Azure Data Factory, see the [Azure Data Factory documentation][Azure Data Factory documentation].</span></span>

## <a name="data-movement"></a><span data-ttu-id="57f66-107">Movimentação de dados</span><span class="sxs-lookup"><span data-stu-id="57f66-107">Data Movement</span></span>
<span data-ttu-id="57f66-108">O Azure Data Factory permite a movimentação de dados entre fontes locais e diferentes serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="57f66-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span></span>  <span data-ttu-id="57f66-109">De forma geral, a integração atual com o Azure Data Factory oferece suporte à movimentação de dados de e para os seguintes locais:</span><span class="sxs-lookup"><span data-stu-id="57f66-109">Overall, current integration with Azure Data Factory supports data movement to and from the following locations:</span></span>

* <span data-ttu-id="57f66-110">Armazenamento do blob do Azure</span><span class="sxs-lookup"><span data-stu-id="57f66-110">Azure blob storage</span></span>
* <span data-ttu-id="57f66-111">Banco de Dados SQL Azure</span><span class="sxs-lookup"><span data-stu-id="57f66-111">Azure SQL Database</span></span>
* <span data-ttu-id="57f66-112">SQL Server local</span><span class="sxs-lookup"><span data-stu-id="57f66-112">On-premises SQL Server</span></span>
* <span data-ttu-id="57f66-113">SQL Server na IaaS</span><span class="sxs-lookup"><span data-stu-id="57f66-113">SQL Server on IaaS</span></span>

<span data-ttu-id="57f66-114">Para obter informações sobre como configurar uma atividade de cópia de dados, veja [Copiar dados com o Azure Data Factory][Copy data with Azure Data Factory]</span><span class="sxs-lookup"><span data-stu-id="57f66-114">For information on how to set up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span></span>

## <a name="stored-procedures"></a><span data-ttu-id="57f66-115">Procedimentos Armazenados</span><span class="sxs-lookup"><span data-stu-id="57f66-115">Stored Procedures</span></span>
 <span data-ttu-id="57f66-116">Da mesma forma que ele pode ser usado para agendar a transferência de dados, o Azure Data Factory também pode ser usado para coordenar a execução de procedimentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="57f66-116">In the same way it can be used to schedule data transfer, Azure Data Factory can also be used to orchestrate the execution of stored procedures.</span></span>  <span data-ttu-id="57f66-117">Isso permite que pipelines mais complexos sejam criados e estende a capacidade do Azure Data Factory de aproveitar o poder computacional do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="57f66-117">This allows more complex pipelines to be created and extends Azure Data Factory's ability to leverage the computational power of SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57f66-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="57f66-118">Next steps</span></span>
<span data-ttu-id="57f66-119">Para obter uma visão geral da integração, consulte [Visão geral de integração do SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="57f66-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>
<span data-ttu-id="57f66-120">Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="57f66-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

