---
title: aaaLoad terabytes de dados no SQL Data Warehouse | Microsoft Docs
description: Demonstra como 1 TB de dados podem ser carregado no Azure SQL Data Warehouse em 15 minutos com o Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: a6c133c0-ced2-463c-86f0-a07b00c9e37f
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: e63f60461b082b0e3979004cb631dbf4a6710de3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="fb0f6-103">Carregar 1 TB no SQL Data Warehouse do Azure em menos de 15 minutos com o Data Factory</span><span class="sxs-lookup"><span data-stu-id="fb0f6-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="fb0f6-104">O [Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) é um banco de dados baseado em nuvem e expansível com capacidade de processar volumes imensos de dados, relacionais e não relacionais.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="fb0f6-105">Criado em arquitetura MPP (processamento paralelo maciço), o SQL Data Warehouse é otimizado para cargas de trabalho do data warehouse corporativas.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="fb0f6-106">Ele oferece elasticidade com armazenamento de tooscale flexibilidade Olá de nuvem e computação independentemente.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-106">It offers cloud elasticity with hello flexibility tooscale storage and compute independently.</span></span>

<span data-ttu-id="fb0f6-107">A introdução ao Azure SQL Data Warehouse agora é mais fácil do que nunca, usando o **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="fb0f6-108">A fábrica de dados do Azure é um serviço de integração de dados totalmente gerenciado baseado em nuvem, que pode ser usado toopopulate um SQL Data Warehouse com dados de saudação do seu sistema existente e salvando tempo valioso durante a avaliação SQL Data Warehouse e criação de sua análise soluções.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used toopopulate a SQL Data Warehouse with hello data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="fb0f6-109">Aqui estão os principais benefícios de saudação do carregamento de dados no Azure SQL Data Warehouse usando o Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="fb0f6-109">Here are hello key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="fb0f6-110">**Fácil tooset backup**: etapa 5 intuitivas de assistente sem scripts necessários.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-110">**Easy tooset up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="fb0f6-111">**Suporte de armazenamento de dados avançados**: suporte interno para um conjunto avançado de armazenamentos de dados locais e baseados em nuvem.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="fb0f6-112">**Seguras e compatíveis**: dados são transferidos por HTTPS, ou rota expressa e a presença do serviço global garante que os dados nunca saem limites geográficos Olá</span><span class="sxs-lookup"><span data-stu-id="fb0f6-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves hello geographical boundary</span></span>
* <span data-ttu-id="fb0f6-113">**Desempenho incomparável usando PolyBase** – usando o Polybase é toomove dados de maneira mais eficientes de saudação no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-113">**Unparalleled performance by using PolyBase** – Using Polybase is hello most efficient way toomove data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="fb0f6-114">Usando Olá recurso de blob de preparo, você pode obter velocidades de alta carga de todos os tipos de armazenamentos de dados além do armazenamento de BLOBs do Azure, que Olá suporta Polybase por padrão.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-114">Using hello staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which hello Polybase supports by default.</span></span>

<span data-ttu-id="fb0f6-115">Este artigo mostra como toouse dados do Assistente para cópia de fábrica de dados tooload 1 TB de armazenamento de BLOBs do Azure no Azure SQL Data Warehouse em menos de 15 minutos, com taxa de transferência mais 1,2 GBps.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-115">This article shows you how toouse Data Factory Copy Wizard tooload 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="fb0f6-116">Este artigo fornece instruções passo a passo para a movimentação de dados no Azure SQL Data Warehouse usando o Assistente para cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using hello Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="fb0f6-117">Para obter informações gerais sobre os recursos da fábrica de dados na movimentação de dados para/do Azure SQL Data Warehouse, consulte [mover tooand de dados de uso do Azure Data Factory do Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data tooand from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="fb0f6-118">Você também pode criar pipelines usando o Portal do Azure, Visual Studio, PowerShell, etc. Consulte [Tutorial: copiar dados de Blob do Azure tooAzure banco de dados SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para uma rápida explicação passo a passo com instruções passo a passo para usar o hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob tooAzure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using hello Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="fb0f6-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fb0f6-119">Prerequisites</span></span>
* <span data-ttu-id="fb0f6-120">Armazenamento de Blobs do Azure: esse teste usa o Armazenamento de Blobs do Azure (GRS) para armazenar o conjunto de dados de teste do TPC-H.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="fb0f6-121">Se você não tiver uma conta de armazenamento do Azure, saiba [como uma conta de armazenamento do toocreate](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="fb0f6-121">If you do not have an Azure storage account, learn [how toocreate a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="fb0f6-122">[TPC-H](http://www.tpc.org/tpch/) dados: vamos toouse TPC-H como Olá teste de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going toouse TPC-H as hello testing dataset.</span></span>  <span data-ttu-id="fb0f6-123">toodo, é necessária toouse `dbgen` do Kit de ferramentas TPC-H, que ajuda a gerar o conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-123">toodo that, you need toouse `dbgen` from TPC-H toolkit, which helps you generate hello dataset.</span></span>  <span data-ttu-id="fb0f6-124">Você pode baixar código-fonte para `dbgen` de [ferramentas TPC](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) e compilá-lo por conta própria ou download Olá compilado binário de [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="fb0f6-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download hello compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="fb0f6-125">Execução dbgen.exe com os seguintes Olá comandos de arquivo simples de 1 TB de toogenerate para `lineitem` visualização de tabela em 10 arquivos:</span><span class="sxs-lookup"><span data-stu-id="fb0f6-125">Run dbgen.exe with hello following commands toogenerate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="fb0f6-126">…</span><span class="sxs-lookup"><span data-stu-id="fb0f6-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="fb0f6-127">Saudação de cópia geradas agora arquivos tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-127">Now copy hello generated files tooAzure Blob.</span></span>  <span data-ttu-id="fb0f6-128">Consulte também[mover tooand de dados de um sistema de arquivos local usando o Azure Data Factory](data-factory-onprem-file-system-connector.md) como toodo que usando a cópia do ADF.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-128">Refer too[Move data tooand from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how toodo that using ADF Copy.</span></span>    
* <span data-ttu-id="fb0f6-129">Azure SQL Data Warehouse: este experimento carrega dados no Azure SQL Data Warehouse criado com 6.000 DWUs</span><span class="sxs-lookup"><span data-stu-id="fb0f6-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="fb0f6-130">Consulte também[criar um Data Warehouse do Azure SQL](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) para obter instruções detalhadas sobre como toocreate um SQL Data Warehouse banco de dados.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-130">Refer too[Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how toocreate a SQL Data Warehouse database.</span></span>  <span data-ttu-id="fb0f6-131">tooget Olá melhor possíveis de carga desempenho no SQL Data Warehouse usando Polybase, escolhemos o número máximo de unidades de depósito de dados (DWUs) permitido na configuração de desempenho de saudação, que é de 6.000 DWUs.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-131">tooget hello best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in hello Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="fb0f6-132">Durante o carregamento de BLOBs do Azure, o desempenho do carregamento de dados de saudação são número de toohello diretamente proporcional de DWUs que você configurar no hello SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="fb0f6-132">When loading from Azure Blob, hello data loading performance is directly proportional toohello number of DWUs you configure on hello SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="fb0f6-133">Carregar 1 TB em um SQL Data Warehouse com 1.000 DWUs leva 87 minutos (vazão de dados de cerca de 200 MBps) Carregar 1 TB em um SQL Data Warehouse com 2.000 DWUs leva 46 minutos (vazão de dados de cerca de 380 MBps) Carregar 1 TB em um SQL Data Warehouse com 6.000 DWUs leva 14 minutos (vazão de dados de cerca de 1,2 GBps)</span><span class="sxs-lookup"><span data-stu-id="fb0f6-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="fb0f6-134">toocreate um SQL Data Warehouse com 6.000 DWUs, mova Olá desempenho seletor de todos os toohello de maneira Olá à direita:</span><span class="sxs-lookup"><span data-stu-id="fb0f6-134">toocreate a SQL Data Warehouse with 6,000 DWUs, move hello Performance slider all hello way toohello right:</span></span>

    ![Controle deslizante de Desempenho](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="fb0f6-136">Um banco de dados existente que não está configurado com 6.000 DWUs poderá ser escalado verticalmente por você usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="fb0f6-137">Navegue toohello banco de dados no portal do Azure e não há um **escala** botão Olá **visão geral** painel mostrada a saudação a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb0f6-137">Navigate toohello database in Azure portal, and there is a **Scale** button in hello **Overview** panel shown in hello following image:</span></span>

    ![Botão Dimensionar](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="fb0f6-139">Clique em Olá **escala** seguinte de saudação do botão tooopen do painel, mover o valor máximo do toohello Olá controle deslizante e clique em **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-139">Click hello **Scale** button tooopen hello following panel, move hello slider toohello maximum value, and click **Save** button.</span></span>

    ![Caixa de diálogo Dimensionar](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="fb0f6-141">Este experimento carrega dados no Azure SQL Data Warehouse usando a classe de recurso `xlargerc`.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="fb0f6-142">necessidades de cópia de tooachieve melhor transferência possíveis, toobe executada por meio de um usuário do SQL Data Warehouse pertencentes muito`xlargerc` classe de recurso.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-142">tooachieve best possible throughput, copy needs toobe performed using a SQL Data Warehouse user belonging too`xlargerc` resource class.</span></span>  <span data-ttu-id="fb0f6-143">Saiba como toodo que seguindo [alterar um exemplo de classe de recurso de usuário](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="fb0f6-143">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="fb0f6-144">Crie o esquema da tabela de destino no banco de dados do Azure SQL Data Warehouse, executando Olá instrução DDL a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb0f6-144">Create destination table schema in Azure SQL Data Warehouse database, by running hello following DDL statement:</span></span>

    ```SQL  
    CREATE TABLE [dbo].[lineitem]
    (
        [L_ORDERKEY] [bigint] NOT NULL,
        [L_PARTKEY] [bigint] NOT NULL,
        [L_SUPPKEY] [bigint] NOT NULL,
        [L_LINENUMBER] [int] NOT NULL,
        [L_QUANTITY] [decimal](15, 2) NULL,
        [L_EXTENDEDPRICE] [decimal](15, 2) NULL,
        [L_DISCOUNT] [decimal](15, 2) NULL,
        [L_TAX] [decimal](15, 2) NULL,
        [L_RETURNFLAG] [char](1) NULL,
        [L_LINESTATUS] [char](1) NULL,
        [L_SHIPDATE] [date] NULL,
        [L_COMMITDATE] [date] NULL,
        [L_RECEIPTDATE] [date] NULL,
        [L_SHIPINSTRUCT] [char](25) NULL,
        [L_SHIPMODE] [char](10) NULL,
        [L_COMMENT] [varchar](44) NULL
    )
    WITH
    (
        DISTRIBUTION = ROUND_ROBIN,
        CLUSTERED COLUMNSTORE INDEX
    )
    ```
<span data-ttu-id="fb0f6-145">Com etapas de pré-requisito Olá concluídas, estamos agora pronto tooconfigure atividade de cópia de saudação usando o Assistente para cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-145">With hello prerequisite steps completed, we are now ready tooconfigure hello copy activity using hello Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="fb0f6-146">Iniciar o Assistente de cópia</span><span class="sxs-lookup"><span data-stu-id="fb0f6-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="fb0f6-147">Faça logon no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fb0f6-147">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fb0f6-148">Clique em **+ novo** no canto superior esquerdo de saudação, clique em **Intelligence + análise**e clique em **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-148">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="fb0f6-149">Em Olá **nova fábrica de dados** folha:</span><span class="sxs-lookup"><span data-stu-id="fb0f6-149">In hello **New data factory** blade:</span></span>

   1. <span data-ttu-id="fb0f6-150">Digite **LoadIntoSQLDWDataFactory** para Olá **nome**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-150">Enter **LoadIntoSQLDWDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="fb0f6-151">nome de Olá Olá do Azure da fábrica de dados deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-151">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="fb0f6-152">Se você receber o erro Olá: **"LoadIntoSQLDWDataFactory" nome da fábrica de dados não está disponível**, altere o nome de Olá Olá da fábrica de dados (por exemplo, yournameLoadIntoSQLDWDataFactory) e tente criar novamente.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-152">If you receive hello error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change hello name of hello data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="fb0f6-153">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="fb0f6-154">Selecione sua **assinatura**do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="fb0f6-155">Para o grupo de recursos, siga um destes Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb0f6-155">For Resource Group, do one of hello following steps:</span></span>
      1. <span data-ttu-id="fb0f6-156">Selecione **usar existente** tooselect um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-156">Select **Use existing** tooselect an existing resource group.</span></span>
      2. <span data-ttu-id="fb0f6-157">Selecione **criar novo** tooenter um nome para um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-157">Select **Create new** tooenter a name for a resource group.</span></span>
   4. <span data-ttu-id="fb0f6-158">Selecione um **local** Olá fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-158">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="fb0f6-159">Selecione **toodashboard Pin** caixa de seleção na parte inferior da saudação da folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-159">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="fb0f6-160">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-160">Click **Create**.</span></span>
4. <span data-ttu-id="fb0f6-161">Após a conclusão da criação de saudação, você ver Olá **Data Factory** folha conforme Olá a imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb0f6-161">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>

   ![Página inicial da data factory](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="fb0f6-163">Na home page do hello fábrica de dados, clique em Olá **copiar dados** bloco toolaunch **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-163">On hello Data Factory home page, click hello **Copy data** tile toolaunch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fb0f6-164">Se você vir esse navegador da web hello está preso em "Autorizar...", desabilitar/desmarque **bloquear cookies de terceiros e dados do site** configuração (ou) manter habilitado e criar uma exceção para **login.microsoftonline.com**e tente iniciar o Assistente de saudação novamente.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-164">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="fb0f6-165">Etapa 1: configurar o cronograma de carregamento de dados</span><span class="sxs-lookup"><span data-stu-id="fb0f6-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="fb0f6-166">Olá primeira etapa é a agenda de carregamento de dados de saudação de tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-166">hello first step is tooconfigure hello data loading schedule.</span></span>  

<span data-ttu-id="fb0f6-167">Em Olá **propriedades** página:</span><span class="sxs-lookup"><span data-stu-id="fb0f6-167">In hello **Properties** page:</span></span>

1. <span data-ttu-id="fb0f6-168">Insira **CopyFromBlobToAzureSqlDataWarehouse** para o **Nome da tarefa**</span><span class="sxs-lookup"><span data-stu-id="fb0f6-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="fb0f6-169">Selecione opção **Executar uma vez agora**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="fb0f6-170">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-170">Click **Next**.</span></span>  

    ![Assistente de Cópia – página Propriedades](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="fb0f6-172">Etapa 2: Configurar a origem</span><span class="sxs-lookup"><span data-stu-id="fb0f6-172">Step 2: Configure source</span></span>
<span data-ttu-id="fb0f6-173">Este mostra seção Olá origem de saudação tooconfigure etapas: Blob do Azure que contém Olá 1 TB TPC-arquivos de item de linha de H.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-173">This section shows you hello steps tooconfigure hello source: Azure Blob containing hello 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="fb0f6-174">Selecione Olá **armazenamento de BLOBs do Azure** como dados saudação armazenar e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-174">Select hello **Azure Blob Storage** as hello data store and click **Next**.</span></span>

    ![Assistente de Cópia – selecionar página de origem](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="fb0f6-176">Preencher informações de conexão de saudação para Olá conta de armazenamento de BLOBs do Azure e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-176">Fill in hello connection information for hello Azure Blob storage account, and click **Next**.</span></span>

    ![Assistente de Cópia – informações de conexão de origem](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="fb0f6-178">Escolha Olá **pasta** que contém a linha hello TPC-H arquivos de item e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-178">Choose hello **folder** containing hello TPC-H line item files and click **Next**.</span></span>

    ![Assistente de Cópia – selecionar pasta de entrada](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="fb0f6-180">Após clicar em **próximo**, configurações de formato de arquivo hello são detectadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-180">Upon clicking **Next**, hello file format settings are detected automatically.</span></span>  <span data-ttu-id="fb0f6-181">Verificar toomake-se de que delimitador de coluna é ' | 'em vez da saudação padrão por vírgulas','.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-181">Check toomake sure that column delimiter is ‘|’ instead of hello default comma ‘,’.</span></span>  <span data-ttu-id="fb0f6-182">Clique em **próximo** depois de ter visualizado dados saudação.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-182">Click **Next** after you have previewed hello data.</span></span>

    ![Assistente de Cópia – configurações de formato de arquivo](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="fb0f6-184">Etapa 3: Configurar o destino</span><span class="sxs-lookup"><span data-stu-id="fb0f6-184">Step 3: Configure destination</span></span>
<span data-ttu-id="fb0f6-185">Esta seção mostra como tooconfigure Olá destino: `lineitem` tabela no banco de dados do hello Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-185">This section shows you how tooconfigure hello destination: `lineitem` table in hello Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="fb0f6-186">Escolha **Azure SQL Data Warehouse** como destino Olá armazenar e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-186">Choose **Azure SQL Data Warehouse** as hello destination store and click **Next**.</span></span>

    ![Assistente de Cópia – selecionar o armazenamento de dados de destino](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="fb0f6-188">Forneça informações de conexão Olá para o Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-188">Fill in hello connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="fb0f6-189">Certifique-se de especificar usuário Olá que é um membro da função de saudação `xlargerc` (consulte Olá **pré-requisitos** seção para obter instruções detalhadas) e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-189">Make sure you specify hello user that is a member of hello role `xlargerc` (see hello **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Assistente de Cópia – informações de conexão de destino](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="fb0f6-191">Escolher tabela de destino hello e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-191">Choose hello destination table and click **Next**.</span></span>

    ![Assistente de Cópia – página de mapeamento de tabela](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="fb0f6-193">Na página de mapeamento de esquema, deixe a opção "Aplicar o mapeamento de coluna" desmarcada e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="fb0f6-194">Etapa 4: Configurações de desempenho</span><span class="sxs-lookup"><span data-stu-id="fb0f6-194">Step 4: Performance settings</span></span>

<span data-ttu-id="fb0f6-195">A opção **Permitir polybase** é marcada por padrão.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="fb0f6-196">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-196">Click **Next**.</span></span>

![Assistente de Cópia – página de mapeamento de esquema](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="fb0f6-198">Etapa 5: Implantar e monitorar os resultados de carga</span><span class="sxs-lookup"><span data-stu-id="fb0f6-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="fb0f6-199">Clique em **concluir** toodeploy do botão.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-199">Click **Finish** button toodeploy.</span></span>

    ![Assistente de Cópia – página de resumo](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="fb0f6-201">Após a conclusão da implantação de saudação, clique em `Click here toomonitor copy pipeline` toomonitor cópia de saudação andamento da execução.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-201">After hello deployment is complete, click `Click here toomonitor copy pipeline` toomonitor hello copy run progress.</span></span> <span data-ttu-id="fb0f6-202">Pipeline de cópia Olá selecione criado no hello **atividade Windows** lista.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-202">Select hello copy pipeline you created in hello **Activity Windows** list.</span></span>

    ![Assistente de Cópia – página de resumo](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="fb0f6-204">Você pode exibir a cópia Olá detalhes da execução em Olá **Pesquisador de objetos de janela de atividade** o painel direito hello, incluindo Olá volume de dados lidos na origem e gravado no destino, a duração e a taxa de transferência média para Olá executar hello.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-204">You can view hello copy run details in hello **Activity Window Explorer** in hello right panel, including hello data volume read from source and written into destination, duration, and hello average throughput for hello run.</span></span>

    <span data-ttu-id="fb0f6-205">Como você pode ver da saudação captura de tela a seguir, copiando 1 TB de armazenamento de BLOBs do Azure no SQL Data Warehouse levou 14 minutos, efetivamente para alcançar a taxa de transferência GBps 1,22!</span><span class="sxs-lookup"><span data-stu-id="fb0f6-205">As you can see from hello following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Assistente de Cópia – caixa de diálogo de êxito](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="fb0f6-207">Práticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="fb0f6-207">Best practices</span></span>
<span data-ttu-id="fb0f6-208">Aqui estão algumas práticas recomendadas para a execução de seu banco de dados do Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="fb0f6-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="fb0f6-209">Use uma classe de recurso maior durante o carregamento em um ÍNDICE COLUMNSTORE CLUSTERIZADO.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="fb0f6-210">Para junções mais eficientes, considere usar a distribuição de hash por uma coluna selecionada em vez da distribuição round robin padrão.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="fb0f6-211">Para velocidades de carga, considere usar o heap para dados transitórios.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="fb0f6-212">Crie estatísticas depois de terminar de carregar o Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="fb0f6-213">Veja [Práticas Recomendadas para o SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb0f6-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fb0f6-214">Next steps</span></span>
* <span data-ttu-id="fb0f6-215">[Assistente para cópia de fábrica de dados](data-factory-copy-wizard.md) -este artigo fornece detalhes sobre o Assistente para cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about hello Copy Wizard.</span></span>
* <span data-ttu-id="fb0f6-216">[Copiar atividade guia de desempenho e ajuste](data-factory-copy-activity-performance.md) -este artigo contém medidas de desempenho de referência hello e guia de ajuste.</span><span class="sxs-lookup"><span data-stu-id="fb0f6-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains hello reference performance measurements and tuning guide.</span></span>
