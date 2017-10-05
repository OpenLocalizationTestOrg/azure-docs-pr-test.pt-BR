---
title: Usar o Stream Analytics do Azure com o SQL Data Warehouse | Microsoft Docs
description: "Dicas para usar o Stream Analytics do Azure com o Azure SQL Data Warehouse para desenvolver as soluções."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 8aeb2247-20c5-4a29-b327-30a8ce09dfdc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 14783f0464764a11d7f03a5db1c2d63728a4cb50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="e5bc8-103">Usar o Stream Analytics do Azure com o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e5bc8-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="e5bc8-104">A Stream Analytics do Azure é um serviço completamente gerenciado que oferece baixa latência, alta disponibilidade e processamento escalonável de eventos complexos ao longo do fluxo de dados na nuvem.</span><span class="sxs-lookup"><span data-stu-id="e5bc8-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in the cloud.</span></span> <span data-ttu-id="e5bc8-105">Você pode aprender as noções básicas lendo [Introdução ao Stream Analytics do Azure][Introduction to Azure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="e5bc8-105">You can learn the basics by reading [Introduction to Azure Stream Analytics][Introduction to Azure Stream Analytics].</span></span> <span data-ttu-id="e5bc8-106">Depois, você pode saber como criar uma solução de ponta a ponta com o Stream Analytics seguindo o tutorial [Introdução ao uso do Stream Analytics do Azure][Get started using Azure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="e5bc8-106">You can then learn how to create an end-to-end solution with Stream Analytics by following the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="e5bc8-107">Neste artigo, você aprenderá como usar o banco de dados do SQL Data Warehouse do Azure como um coletor de saída seus trabalhos do  Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="e5bc8-107">In this article, you will learn how to use your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5bc8-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e5bc8-108">Prerequisites</span></span>
<span data-ttu-id="e5bc8-109">Primeiro, execute as etapas a seguir no tutorial [Introdução ao uso do Stream Analytics do Azure][Get started using Azure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="e5bc8-109">First, run through the following steps in the [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="e5bc8-110">Criar uma entrada de Hub de eventos</span><span class="sxs-lookup"><span data-stu-id="e5bc8-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="e5bc8-111">Configurar e iniciar o aplicativo gerador de evento</span><span class="sxs-lookup"><span data-stu-id="e5bc8-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="e5bc8-112">Provisionar um trabalho de análise de fluxo</span><span class="sxs-lookup"><span data-stu-id="e5bc8-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="e5bc8-113">Especifique a entrada e a consulta do trabalho</span><span class="sxs-lookup"><span data-stu-id="e5bc8-113">Specify job input and query</span></span>

<span data-ttu-id="e5bc8-114">Em seguida, crie um banco de dados do SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="e5bc8-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="e5bc8-115">Especifique a saída do trabalho: banco de dados do SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="e5bc8-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="e5bc8-116">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="e5bc8-116">Step 1</span></span>
<span data-ttu-id="e5bc8-117">No trabalho Stream Analytics, clique em **SAÍDA** na parte superior da página e depois em **ADICIONAR SAÍDA**.</span><span class="sxs-lookup"><span data-stu-id="e5bc8-117">In your Stream Analytics job click **OUTPUT** from the top of the page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="e5bc8-118">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="e5bc8-118">Step 2</span></span>
<span data-ttu-id="e5bc8-119">Selecione o Banco de Dados SQL e clique em Avançar.</span><span class="sxs-lookup"><span data-stu-id="e5bc8-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="e5bc8-120">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="e5bc8-120">Step 3</span></span>
<span data-ttu-id="e5bc8-121">Insira os seguintes valores na próxima página:</span><span class="sxs-lookup"><span data-stu-id="e5bc8-121">Enter the following values on the next page:</span></span>

* <span data-ttu-id="e5bc8-122">*Alias de saída*: insira um nome amigável para essa saída de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e5bc8-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="e5bc8-123">*Assinatura*:</span><span class="sxs-lookup"><span data-stu-id="e5bc8-123">*Subscription*:</span></span>
  * <span data-ttu-id="e5bc8-124">se o seu banco de dados do SQL Data Warehouse estiver na mesma assinatura que o trabalho do Stream Analytics, selecione Usar Banco de Dados SQL da Assinatura Atual.</span><span class="sxs-lookup"><span data-stu-id="e5bc8-124">If your SQL Data Warehouse database is in the same subscription as the Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="e5bc8-125">Se o seu banco de dados estiver em uma assinatura diferente, selecione Usar Banco de Dados SQL de Outra Assinatura.</span><span class="sxs-lookup"><span data-stu-id="e5bc8-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="e5bc8-126">*Banco de dados*: especifique o nome de um banco de dados de destino.</span><span class="sxs-lookup"><span data-stu-id="e5bc8-126">*Database*: Specify the name of a destination database.</span></span>
* <span data-ttu-id="e5bc8-127">*Nome do servidor*: especifique o nome do servidor do banco de dados que você acabou de especificar.</span><span class="sxs-lookup"><span data-stu-id="e5bc8-127">*Server Name*: Specify the server name for the database you just specified.</span></span> <span data-ttu-id="e5bc8-128">Você pode usar o Portal clássico do Azure para encontrá-lo.</span><span class="sxs-lookup"><span data-stu-id="e5bc8-128">You can use the Azure Classic Portal to find this.</span></span>

![][server-name]

* <span data-ttu-id="e5bc8-129">*Nome de usuário*: especifique o nome de usuário de uma conta que tenha permissões de gravação para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e5bc8-129">*User Name*: Specify the user name of an account that has write permissions for the database.</span></span>
* <span data-ttu-id="e5bc8-130">*Senha*: forneça a senha da conta de usuário especificada.</span><span class="sxs-lookup"><span data-stu-id="e5bc8-130">*Password*: Provide the password for the specified user account.</span></span>
* <span data-ttu-id="e5bc8-131">*Tabela*: especifique o nome da tabela de destino no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e5bc8-131">*Table*: Specify the name of the target table in the database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="e5bc8-132">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="e5bc8-132">Step 4</span></span>
<span data-ttu-id="e5bc8-133">Clique no botão de verificação para adicionar essa saída e para verificar se o Stream Analytics pode se conectar com êxito ao banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e5bc8-133">Click the check button to add this job output and to verify that Stream Analytics can successfully connect to the database.</span></span>

![][test-connection]

<span data-ttu-id="e5bc8-134">Quando a conexão com o banco de dados tiver êxito, você verá uma notificação na parte inferior do portal.</span><span class="sxs-lookup"><span data-stu-id="e5bc8-134">When the connection to the database succeeds, you will see a notification at the bottom of the portal.</span></span> <span data-ttu-id="e5bc8-135">Você pode clicar em Testar Conexão na parte inferior para testar a conexão com o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e5bc8-135">You can click Test Connection at the bottom to test the connection to the database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5bc8-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e5bc8-136">Next steps</span></span>
<span data-ttu-id="e5bc8-137">Para obter uma visão geral da integração, consulte [Visão geral de integração do SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="e5bc8-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="e5bc8-138">Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="e5bc8-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction to Azure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
