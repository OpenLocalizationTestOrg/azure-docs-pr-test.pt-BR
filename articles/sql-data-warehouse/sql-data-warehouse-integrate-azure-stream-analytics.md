---
title: aaaUse Stream Analytics do Azure, SQL Data warehouse | Microsoft Docs
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
ms.openlocfilehash: 1278197a6764864124fd92fc672de00b83ec343f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-with-sql-data-warehouse"></a><span data-ttu-id="95606-103">Usar o Stream Analytics do Azure com o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="95606-103">Use Azure Stream Analytics with SQL Data Warehouse</span></span>
<span data-ttu-id="95606-104">Análise de fluxo do Azure é um serviço totalmente gerenciado fornecendo processamento de eventos complexos de baixa latência, altamente disponível e dimensionável ao longo do fluxo de dados na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="95606-104">Azure Stream Analytics is a fully managed service providing low-latency, highly available, scalable complex event processing over streaming data in hello cloud.</span></span> <span data-ttu-id="95606-105">Você pode aprender os fundamentos de saudação lendo [tooAzure de Introdução do Stream Analytics][Introduction tooAzure Stream Analytics].</span><span class="sxs-lookup"><span data-stu-id="95606-105">You can learn hello basics by reading [Introduction tooAzure Stream Analytics][Introduction tooAzure Stream Analytics].</span></span> <span data-ttu-id="95606-106">Em seguida, saiba como toocreate uma solução de ponta a ponta com análises de fluxo seguindo Olá [começar a usar o Azure Stream Analytics] [ Get started using Azure Stream Analytics] tutorial.</span><span class="sxs-lookup"><span data-stu-id="95606-106">You can then learn how toocreate an end-to-end solution with Stream Analytics by following hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>

<span data-ttu-id="95606-107">Neste artigo, você aprenderá como toouse o Azure SQL Data Warehouse banco de dados como um coletor de saída para os trabalhos de análise de fluxo.</span><span class="sxs-lookup"><span data-stu-id="95606-107">In this article, you will learn how toouse your Azure SQL Data Warehouse database as an output sink for your Steam Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95606-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="95606-108">Prerequisites</span></span>
<span data-ttu-id="95606-109">Primeiro, execute Olá etapas Olá [começar a usar o Azure Stream Analytics] [ Get started using Azure Stream Analytics] tutorial.</span><span class="sxs-lookup"><span data-stu-id="95606-109">First, run through hello following steps in hello [Get started using Azure Stream Analytics][Get started using Azure Stream Analytics] tutorial.</span></span>  

1. <span data-ttu-id="95606-110">Criar uma entrada de Hub de eventos</span><span class="sxs-lookup"><span data-stu-id="95606-110">Create an Event Hub input</span></span>
2. <span data-ttu-id="95606-111">Configurar e iniciar o aplicativo gerador de evento</span><span class="sxs-lookup"><span data-stu-id="95606-111">Configure and start event generator application</span></span>
3. <span data-ttu-id="95606-112">Provisionar um trabalho de análise de fluxo</span><span class="sxs-lookup"><span data-stu-id="95606-112">Provision a Stream Analytics job</span></span>
4. <span data-ttu-id="95606-113">Especifique a entrada e a consulta do trabalho</span><span class="sxs-lookup"><span data-stu-id="95606-113">Specify job input and query</span></span>

<span data-ttu-id="95606-114">Em seguida, crie um banco de dados do SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="95606-114">Then, create an Azure SQL Data Warehouse database</span></span>

## <a name="specify-job-output-azure-sql-data-warehouse-database"></a><span data-ttu-id="95606-115">Especifique a saída do trabalho: banco de dados do SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="95606-115">Specify job output: Azure SQL Data Warehouse database</span></span>
### <a name="step-1"></a><span data-ttu-id="95606-116">Etapa 1</span><span class="sxs-lookup"><span data-stu-id="95606-116">Step 1</span></span>
<span data-ttu-id="95606-117">O trabalho do Stream Analytics em **saída** da parte superior da saudação de página hello e clique **adicionar saída**.</span><span class="sxs-lookup"><span data-stu-id="95606-117">In your Stream Analytics job click **OUTPUT** from hello top of hello page, and then click **ADD OUTPUT**.</span></span>

### <a name="step-2"></a><span data-ttu-id="95606-118">Etapa 2</span><span class="sxs-lookup"><span data-stu-id="95606-118">Step 2</span></span>
<span data-ttu-id="95606-119">Selecione o Banco de Dados SQL e clique em Avançar.</span><span class="sxs-lookup"><span data-stu-id="95606-119">Select SQL Database and click next.</span></span>

![][add-output]

### <a name="step-3"></a><span data-ttu-id="95606-120">Etapa 3</span><span class="sxs-lookup"><span data-stu-id="95606-120">Step 3</span></span>
<span data-ttu-id="95606-121">Digite hello valores a seguir na página seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="95606-121">Enter hello following values on hello next page:</span></span>

* <span data-ttu-id="95606-122">*Alias de saída*: insira um nome amigável para essa saída de trabalho.</span><span class="sxs-lookup"><span data-stu-id="95606-122">*Output Alias*: Enter a friendly name for this job output.</span></span>
* <span data-ttu-id="95606-123">*Assinatura*:</span><span class="sxs-lookup"><span data-stu-id="95606-123">*Subscription*:</span></span>
  * <span data-ttu-id="95606-124">Se seu banco de dados do SQL Data Warehouse estiver em Olá mesma assinatura que o trabalho de análise de fluxo de saudação, selecione Usar banco de dados SQL da assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="95606-124">If your SQL Data Warehouse database is in hello same subscription as hello Stream Analytics job, select Use SQL Database from Current Subscription.</span></span>
  * <span data-ttu-id="95606-125">Se o seu banco de dados estiver em uma assinatura diferente, selecione Usar Banco de Dados SQL de Outra Assinatura.</span><span class="sxs-lookup"><span data-stu-id="95606-125">If your database is in a different subscription, select Use SQL Database from Another Subscription.</span></span>
* <span data-ttu-id="95606-126">*Banco de dados*: especifique o nome de saudação de um banco de dados de destino.</span><span class="sxs-lookup"><span data-stu-id="95606-126">*Database*: Specify hello name of a destination database.</span></span>
* <span data-ttu-id="95606-127">*Nome do servidor*: especificar nome do servidor de saudação do banco de dados de saudação especificado.</span><span class="sxs-lookup"><span data-stu-id="95606-127">*Server Name*: Specify hello server name for hello database you just specified.</span></span> <span data-ttu-id="95606-128">Você pode usar Olá Portal clássico do Azure toofind isso.</span><span class="sxs-lookup"><span data-stu-id="95606-128">You can use hello Azure Classic Portal toofind this.</span></span>

![][server-name]

* <span data-ttu-id="95606-129">*Nome de usuário*: especificar Olá nome de usuário de uma conta que tenha permissões de gravação para o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="95606-129">*User Name*: Specify hello user name of an account that has write permissions for hello database.</span></span>
* <span data-ttu-id="95606-130">*Senha*: fornecer senha Olá Olá especificar conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="95606-130">*Password*: Provide hello password for hello specified user account.</span></span>
* <span data-ttu-id="95606-131">*Tabela*: especifique o nome de Olá Olá tabela de destino no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="95606-131">*Table*: Specify hello name of hello target table in hello database.</span></span>

![][add-database]

### <a name="step-4"></a><span data-ttu-id="95606-132">Etapa 4</span><span class="sxs-lookup"><span data-stu-id="95606-132">Step 4</span></span>
<span data-ttu-id="95606-133">Esta saída de trabalho e tooverify que Stream Analytics pode se conectar com êxito toohello banco de dados, clique em Olá tooadd de botão de seleção.</span><span class="sxs-lookup"><span data-stu-id="95606-133">Click hello check button tooadd this job output and tooverify that Stream Analytics can successfully connect toohello database.</span></span>

![][test-connection]

<span data-ttu-id="95606-134">Quando o banco de dados do hello conexão toohello for bem-sucedida, você verá uma notificação na parte inferior de saudação do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="95606-134">When hello connection toohello database succeeds, you will see a notification at hello bottom of hello portal.</span></span> <span data-ttu-id="95606-135">Você pode clicar em Conexão de teste no hello inferior tootest Olá conexão toohello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="95606-135">You can click Test Connection at hello bottom tootest hello connection toohello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95606-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="95606-136">Next steps</span></span>
<span data-ttu-id="95606-137">Para obter uma visão geral da integração, consulte [Visão geral de integração do SQL Data Warehouse][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="95606-137">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>

<span data-ttu-id="95606-138">Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="95606-138">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

[add-output]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-output.png
[server-name]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/dw-server-name.png
[add-database]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/add-database.png
[test-connection]: ./media/sql-data-warehouse-integrate-azure-stream-analytics/test-connection.png

<!--Article references-->

[Introduction tooAzure Stream Analytics]: ../stream-analytics/stream-analytics-introduction.md
[Get started using Azure Stream Analytics]: ../stream-analytics/stream-analytics-real-time-fraud-detection.md
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Stream Analytics documentation]: http://azure.microsoft.com/documentation/services/stream-analytics/
