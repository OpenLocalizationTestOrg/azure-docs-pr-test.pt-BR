---
title: Carregar terabytes de dados no SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: c29f1f01b660c4eb780e178a68036327fafa9ba6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="load-1-tb-into-azure-sql-data-warehouse-under-15-minutes-with-data-factory"></a><span data-ttu-id="869be-103">Carregar 1 TB no SQL Data Warehouse do Azure em menos de 15 minutos com o Data Factory</span><span class="sxs-lookup"><span data-stu-id="869be-103">Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Data Factory</span></span>
<span data-ttu-id="869be-104">O [Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) é um banco de dados baseado em nuvem e expansível com capacidade de processar volumes imensos de dados, relacionais e não relacionais.</span><span class="sxs-lookup"><span data-stu-id="869be-104">[Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-overview-what-is.md) is a cloud-based, scale-out database capable of processing massive volumes of data, both relational and non-relational.</span></span>  <span data-ttu-id="869be-105">Criado em arquitetura MPP (processamento paralelo maciço), o SQL Data Warehouse é otimizado para cargas de trabalho do data warehouse corporativas.</span><span class="sxs-lookup"><span data-stu-id="869be-105">Built on massively parallel processing (MPP) architecture, SQL Data Warehouse is optimized for enterprise data warehouse workloads.</span></span>  <span data-ttu-id="869be-106">Ele oferece a elasticidade da nuvem com a flexibilidade de dimensionar o armazenamento e a computação de modo independente.</span><span class="sxs-lookup"><span data-stu-id="869be-106">It offers cloud elasticity with the flexibility to scale storage and compute independently.</span></span>

<span data-ttu-id="869be-107">A introdução ao Azure SQL Data Warehouse agora é mais fácil do que nunca, usando o **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="869be-107">Getting started with Azure SQL Data Warehouse is now easier than ever using **Azure Data Factory**.</span></span>  <span data-ttu-id="869be-108">O Azure Data Factory é um serviço de integração de dados baseado em nuvem totalmente gerenciado, que pode ser usado para popular um SQL Data Warehouse com os dados de seu sistema existente e economizar tempo valioso ao avaliar o SQL Data Warehouse e criar suas soluções de análise.</span><span class="sxs-lookup"><span data-stu-id="869be-108">Azure Data Factory is a fully managed cloud-based data integration service, which can be used to populate a SQL Data Warehouse with the data from your existing system, and saving you valuable time while evaluating SQL Data Warehouse and building your analytics solutions.</span></span> <span data-ttu-id="869be-109">Aqui estão os principais benefícios de carregar dados no Azure SQL Data Warehouse usando o Azure Data Factory:</span><span class="sxs-lookup"><span data-stu-id="869be-109">Here are the key benefits of loading data into Azure SQL Data Warehouse using Azure Data Factory:</span></span>

* <span data-ttu-id="869be-110">**Fácil de configurar**: assistente intuitivo de 5 etapas sem nenhum script necessário.</span><span class="sxs-lookup"><span data-stu-id="869be-110">**Easy to set up**: 5-step intuitive wizard with no scripting required.</span></span>
* <span data-ttu-id="869be-111">**Suporte de armazenamento de dados avançados**: suporte interno para um conjunto avançado de armazenamentos de dados locais e baseados em nuvem.</span><span class="sxs-lookup"><span data-stu-id="869be-111">**Rich data store support**: built-in support for a rich set of on-premises and cloud-based data stores.</span></span>
* <span data-ttu-id="869be-112">**Seguro e compatível**: os dados são transferidos por HTTPS ou ExpressRoute e a presença global do serviço garante que os dados nunca saiam do limite geográfico</span><span class="sxs-lookup"><span data-stu-id="869be-112">**Secure and compliant**: data is transferred over HTTPS or ExpressRoute, and global service presence ensures your data never leaves the geographical boundary</span></span>
* <span data-ttu-id="869be-113">**Desempenho incomparável usando PolyBase** – usar o Polybase é a maneira mais eficiente para mover dados para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="869be-113">**Unparalleled performance by using PolyBase** – Using Polybase is the most efficient way to move data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="869be-114">Usando o recurso de blob de preparo, você pode obter velocidades de alta carga de todos os tipos de armazenamentos de dados além do Armazenamento de Blobs do Azure, ao qual o Polybase dá suporte por padrão.</span><span class="sxs-lookup"><span data-stu-id="869be-114">Using the staging blob feature, you can achieve high load speeds from all types of data stores besides Azure Blob storage, which the Polybase supports by default.</span></span>

<span data-ttu-id="869be-115">Este artigo mostra como usar o Assistente de Cópia do Data Factory para carregar 1 TB de dados do Armazenamento de Blobs do Azure no SQL Data Warehouse do Azure em menos de 15 minutos, com uma vazão de dados superior a 1,2 GBps.</span><span class="sxs-lookup"><span data-stu-id="869be-115">This article shows you how to use Data Factory Copy Wizard to load 1-TB data from Azure Blob Storage into Azure SQL Data Warehouse in under 15 minutes, at over 1.2 GBps throughput.</span></span>

<span data-ttu-id="869be-116">Este artigo fornece instruções passo a passo para mover dados no Azure SQL Data Warehouse usando o Assistente de Cópia.</span><span class="sxs-lookup"><span data-stu-id="869be-116">This article provides step-by-step instructions for moving data into Azure SQL Data Warehouse by using the Copy Wizard.</span></span>

> [!NOTE]
>  <span data-ttu-id="869be-117">Para obter informações gerais sobre as funcionalidades do Data Factory para movimentação de dados bidirecionalmente no SQL Data Warehouse do Azure, consulte o artigo [Mover dados bidirecionalmente no SQL Data Warehouse do Azure usando o Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md).</span><span class="sxs-lookup"><span data-stu-id="869be-117">For general information about capabilities of Data Factory in moving data to/from Azure SQL Data Warehouse, see [Move data to and from Azure SQL Data Warehouse using Azure Data Factory](data-factory-azure-sql-data-warehouse-connector.md) article.</span></span>
>
> <span data-ttu-id="869be-118">Você também pode criar pipelines usando o Portal do Azure, Visual Studio, PowerShell, etc. Confira [Tutorial: copiar dados do Blob do Azure para o Banco de Dados SQL do Azure](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter um breve passo a passo com instruções sobre como usar a Atividade de cópia na Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="869be-118">You can also build pipelines using Azure portal, Visual Studio, PowerShell, etc. See [Tutorial: Copy data from Azure Blob to Azure SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for a quick walkthrough with step-by-step instructions for using the Copy Activity in Azure Data Factory.</span></span>  
>
>

## <a name="prerequisites"></a><span data-ttu-id="869be-119">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="869be-119">Prerequisites</span></span>
* <span data-ttu-id="869be-120">Armazenamento de Blobs do Azure: esse teste usa o Armazenamento de Blobs do Azure (GRS) para armazenar o conjunto de dados de teste do TPC-H.</span><span class="sxs-lookup"><span data-stu-id="869be-120">Azure Blob Storage: this experiment uses Azure Blob Storage (GRS) for storing TPC-H testing dataset.</span></span>  <span data-ttu-id="869be-121">Se você não tiver uma conta de armazenamento do Azure, aprenda [como criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="869be-121">If you do not have an Azure storage account, learn [how to create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="869be-122">Dados do [TPC-H](http://www.tpc.org/tpch/): usaremos o TPC-H como o conjunto de dados de teste.</span><span class="sxs-lookup"><span data-stu-id="869be-122">[TPC-H](http://www.tpc.org/tpch/) data: we are going to use TPC-H as the testing dataset.</span></span>  <span data-ttu-id="869be-123">Para fazer isso, você precisa usar `dbgen` do kit de ferramentas do TPC-H, o que ajuda você a gerar o conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="869be-123">To do that, you need to use `dbgen` from TPC-H toolkit, which helps you generate the dataset.</span></span>  <span data-ttu-id="869be-124">Você pode baixar código-fonte para `dbgen` de [Ferramentas TPC](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) e compilá-lo por conta própria ou então baixar o binário compilado de [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span><span class="sxs-lookup"><span data-stu-id="869be-124">You can either download source code for `dbgen` from [TPC Tools](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp) and compile it yourself, or download the compiled binary from [GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TPCHTools).</span></span>  <span data-ttu-id="869be-125">Execute dbgen.exe com os comandos a seguir para gerar um arquivo simples de 1 TB para a tabela `lineitem` dividido em 10 arquivos:</span><span class="sxs-lookup"><span data-stu-id="869be-125">Run dbgen.exe with the following commands to generate 1 TB flat file for `lineitem` table spread across 10 files:</span></span>

  * `Dbgen -s 1000 -S **1** -C 10 -T L -v`
  * `Dbgen -s 1000 -S **2** -C 10 -T L -v`
  * <span data-ttu-id="869be-126">…</span><span class="sxs-lookup"><span data-stu-id="869be-126">…</span></span>
  * `Dbgen -s 1000 -S **10** -C 10 -T L -v`

    <span data-ttu-id="869be-127">Agora, copie os arquivos gerados para o Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="869be-127">Now copy the generated files to Azure Blob.</span></span>  <span data-ttu-id="869be-128">Consulte [Mover dados de e para um sistema de arquivos local usando o Azure Data Factory](data-factory-onprem-file-system-connector.md) para saber como fazer isso usando a Cópia do ADF.</span><span class="sxs-lookup"><span data-stu-id="869be-128">Refer to [Move data to and from an on-premises file system by using Azure Data Factory](data-factory-onprem-file-system-connector.md) for how to do that using ADF Copy.</span></span>    
* <span data-ttu-id="869be-129">Azure SQL Data Warehouse: este experimento carrega dados no Azure SQL Data Warehouse criado com 6.000 DWUs</span><span class="sxs-lookup"><span data-stu-id="869be-129">Azure SQL Data Warehouse: this experiment loads data into Azure SQL Data Warehouse created with 6,000 DWUs</span></span>

    <span data-ttu-id="869be-130">Consulte [Criar um Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) para obter instruções detalhadas sobre como criar um banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="869be-130">Refer to [Create an Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) for detailed instructions on how to create a SQL Data Warehouse database.</span></span>  <span data-ttu-id="869be-131">Para obter o melhor desempenho de carregamento possível no SQL Data Warehouse usando o Polybase, escolhemos o número máximo de DWUs (Unidades de Data Warehouse) permitido na configuração Desempenho, que é de 6.000 DWUs.</span><span class="sxs-lookup"><span data-stu-id="869be-131">To get the best possible load performance into SQL Data Warehouse using Polybase, we choose maximum number of Data Warehouse Units (DWUs) allowed in the Performance setting, which is 6,000 DWUs.</span></span>

  > [!NOTE]
  > <span data-ttu-id="869be-132">Ao carregar do Blob do Azure, o desempenho de carregamento de dados será diretamente proporcional ao número de DWUs que você configurar no SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="869be-132">When loading from Azure Blob, the data loading performance is directly proportional to the number of DWUs you configure on the SQL Data Warehouse:</span></span>
  >
  > <span data-ttu-id="869be-133">Carregar 1 TB em um SQL Data Warehouse com 1.000 DWUs leva 87 minutos (vazão de dados de cerca de 200 MBps) Carregar 1 TB em um SQL Data Warehouse com 2.000 DWUs leva 46 minutos (vazão de dados de cerca de 380 MBps) Carregar 1 TB em um SQL Data Warehouse com 6.000 DWUs leva 14 minutos (vazão de dados de cerca de 1,2 GBps)</span><span class="sxs-lookup"><span data-stu-id="869be-133">Loading 1 TB into 1,000 DWU SQL Data Warehouse takes 87 minutes (~200 MBps throughput) Loading 1 TB into 2,000 DWU SQL Data Warehouse takes 46 minutes (~380 MBps throughput) Loading 1 TB into 6,000 DWU SQL Data Warehouse takes 14 minutes (~1.2 GBps throughput)</span></span>
  >
  >

    <span data-ttu-id="869be-134">Para criar um SQL Data Warehouse com 6.000 DWUs, mova o controle deslizante de desempenho para a direita, até o final:</span><span class="sxs-lookup"><span data-stu-id="869be-134">To create a SQL Data Warehouse with 6,000 DWUs, move the Performance slider all the way to the right:</span></span>

    ![Controle deslizante de Desempenho](media/data-factory-load-sql-data-warehouse/performance-slider.png)

    <span data-ttu-id="869be-136">Um banco de dados existente que não está configurado com 6.000 DWUs poderá ser escalado verticalmente por você usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="869be-136">For an existing database that is not configured with 6,000 DWUs, you can scale it up using Azure portal.</span></span>  <span data-ttu-id="869be-137">Navegue até o banco de dados no Portal do Azure e há um botão **Dimensionar** no painel **Visão Geral** mostrado na imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="869be-137">Navigate to the database in Azure portal, and there is a **Scale** button in the **Overview** panel shown in the following image:</span></span>

    ![Botão Dimensionar](media/data-factory-load-sql-data-warehouse/scale-button.png)    

    <span data-ttu-id="869be-139">Clique no botão **Dimensionar** para abrir o painel seguinte, mova o controle deslizante para o valor máximo e clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="869be-139">Click the **Scale** button to open the following panel, move the slider to the maximum value, and click **Save** button.</span></span>

    ![Caixa de diálogo Dimensionar](media/data-factory-load-sql-data-warehouse/scale-dialog.png)

    <span data-ttu-id="869be-141">Este experimento carrega dados no Azure SQL Data Warehouse usando a classe de recurso `xlargerc`.</span><span class="sxs-lookup"><span data-stu-id="869be-141">This experiment loads data into Azure SQL Data Warehouse using `xlargerc` resource class.</span></span>

    <span data-ttu-id="869be-142">Para obter a melhor taxa de transferência possível, a cópia precisa ser executada usando um usuário do SQL Data Warehouse pertencente à classe de recurso `xlargerc`.</span><span class="sxs-lookup"><span data-stu-id="869be-142">To achieve best possible throughput, copy needs to be performed using a SQL Data Warehouse user belonging to `xlargerc` resource class.</span></span>  <span data-ttu-id="869be-143">Saiba como fazer isso seguindo [Alterar um exemplo de classe de recurso de usuário](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="869be-143">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>  
* <span data-ttu-id="869be-144">Crie um esquema de tabela de destino no banco de dados do Azure SQL Data Warehouse executando a instrução DDL a seguir:</span><span class="sxs-lookup"><span data-stu-id="869be-144">Create destination table schema in Azure SQL Data Warehouse database, by running the following DDL statement:</span></span>

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
<span data-ttu-id="869be-145">Com as etapas de pré-requisito concluídas, agora estamos prontos para configurar a atividade de cópia usando o Assistente de Cópia.</span><span class="sxs-lookup"><span data-stu-id="869be-145">With the prerequisite steps completed, we are now ready to configure the copy activity using the Copy Wizard.</span></span>

## <a name="launch-copy-wizard"></a><span data-ttu-id="869be-146">Iniciar o Assistente de cópia</span><span class="sxs-lookup"><span data-stu-id="869be-146">Launch Copy Wizard</span></span>
1. <span data-ttu-id="869be-147">Faça logon no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="869be-147">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="869be-148">Clique em **+NOVO** no canto superior esquerdo, clique em **Inteligência + análise** e clique em **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="869be-148">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="869be-149">Na folha **Nova data factory** :</span><span class="sxs-lookup"><span data-stu-id="869be-149">In the **New data factory** blade:</span></span>

   1. <span data-ttu-id="869be-150">Insira **LoadIntoSQLDWDataFactory** para o **nome**.</span><span class="sxs-lookup"><span data-stu-id="869be-150">Enter **LoadIntoSQLDWDataFactory** for the **name**.</span></span>
       <span data-ttu-id="869be-151">O nome da data factory do Azure deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="869be-151">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="869be-152">Se você receber o erro: **O nome da data factory “LoadIntoSQLDWDataFactory” não está disponível**, altere o nome da data factory (por exemplo, yournameLoadIntoSQLDWDataFactory) e tente criá-la novamente.</span><span class="sxs-lookup"><span data-stu-id="869be-152">If you receive the error: **Data factory name “LoadIntoSQLDWDataFactory” is not available**, change the name of the data factory (for example, yournameLoadIntoSQLDWDataFactory) and try creating again.</span></span> <span data-ttu-id="869be-153">Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.</span><span class="sxs-lookup"><span data-stu-id="869be-153">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
   2. <span data-ttu-id="869be-154">Selecione sua **assinatura**do Azure.</span><span class="sxs-lookup"><span data-stu-id="869be-154">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="869be-155">Em relação ao Grupo de Recursos, execute uma das seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="869be-155">For Resource Group, do one of the following steps:</span></span>
      1. <span data-ttu-id="869be-156">Selecione **Usar existente** para selecionar um grupo de recursos existente.</span><span class="sxs-lookup"><span data-stu-id="869be-156">Select **Use existing** to select an existing resource group.</span></span>
      2. <span data-ttu-id="869be-157">Selecione **Criar novo** e insira um nome para um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="869be-157">Select **Create new** to enter a name for a resource group.</span></span>
   4. <span data-ttu-id="869be-158">Selecione um **local** para o data factory.</span><span class="sxs-lookup"><span data-stu-id="869be-158">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="869be-159">Marque a caixa de seleção **Fixar no painel** na parte inferior da folha.</span><span class="sxs-lookup"><span data-stu-id="869be-159">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="869be-160">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="869be-160">Click **Create**.</span></span>
4. <span data-ttu-id="869be-161">Depois que a criação for concluída, você verá a folha **Data Factory**, conforme mostrado na seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="869be-161">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>

   ![Página inicial da data factory](media/data-factory-load-sql-data-warehouse/data-factory-home-page-copy-data.png)
5. <span data-ttu-id="869be-163">Na home page do Data Factory, clique no bloco **Copiar dados** para iniciar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="869be-163">On the Data Factory home page, click the **Copy data** tile to launch **Copy Wizard**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="869be-164">Se você vir que o navegador da Web está bloqueado em "Autorizando...", desabilite/desmarque a configuração **Bloquear cookies de terceiros e dados de site** (ou) mantenha-a habilitada, crie uma exceção para **login.microsoftonline.com** e tente iniciar o assistente novamente.</span><span class="sxs-lookup"><span data-stu-id="869be-164">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
   >
   >

## <a name="step-1-configure-data-loading-schedule"></a><span data-ttu-id="869be-165">Etapa 1: configurar o cronograma de carregamento de dados</span><span class="sxs-lookup"><span data-stu-id="869be-165">Step 1: Configure data loading schedule</span></span>
<span data-ttu-id="869be-166">A primeira etapa é configurar o cronograma de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="869be-166">The first step is to configure the data loading schedule.</span></span>  

<span data-ttu-id="869be-167">Na página **Propriedades** :</span><span class="sxs-lookup"><span data-stu-id="869be-167">In the **Properties** page:</span></span>

1. <span data-ttu-id="869be-168">Insira **CopyFromBlobToAzureSqlDataWarehouse** para o **Nome da tarefa**</span><span class="sxs-lookup"><span data-stu-id="869be-168">Enter **CopyFromBlobToAzureSqlDataWarehouse** for **Task name**</span></span>
2. <span data-ttu-id="869be-169">Selecione opção **Executar uma vez agora**.</span><span class="sxs-lookup"><span data-stu-id="869be-169">Select **Run once now** option.</span></span>   
3. <span data-ttu-id="869be-170">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="869be-170">Click **Next**.</span></span>  

    ![Assistente de Cópia – página Propriedades](media/data-factory-load-sql-data-warehouse/copy-wizard-properties-page.png)

## <a name="step-2-configure-source"></a><span data-ttu-id="869be-172">Etapa 2: Configurar a origem</span><span class="sxs-lookup"><span data-stu-id="869be-172">Step 2: Configure source</span></span>
<span data-ttu-id="869be-173">Esta seção mostra as etapas para configurar a origem: Blob do Azure contendo os arquivos de item de linha de 1 TB TPC-H.</span><span class="sxs-lookup"><span data-stu-id="869be-173">This section shows you the steps to configure the source: Azure Blob containing the 1-TB TPC-H line item files.</span></span>

1. <span data-ttu-id="869be-174">Selecione o **Armazenamento de Blobs do Azure** como o armazenamento de dados e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="869be-174">Select the **Azure Blob Storage** as the data store and click **Next**.</span></span>

    ![Assistente de Cópia – selecionar página de origem](media/data-factory-load-sql-data-warehouse/select-source-connection.png)

2. <span data-ttu-id="869be-176">Preencha as informações de conexão para a conta de Armazenamento de Blobs do Azure e, em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="869be-176">Fill in the connection information for the Azure Blob storage account, and click **Next**.</span></span>

    ![Assistente de Cópia – informações de conexão de origem](media/data-factory-load-sql-data-warehouse/source-connection-info.png)

3. <span data-ttu-id="869be-178">Escolha a **pasta** que contém os arquivos de item de linha TPC-H e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="869be-178">Choose the **folder** containing the TPC-H line item files and click **Next**.</span></span>

    ![Assistente de Cópia – selecionar pasta de entrada](media/data-factory-load-sql-data-warehouse/select-input-folder.png)

4. <span data-ttu-id="869be-180">Ao clicar em **Próximo**, as configurações de formato de arquivo são detectadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="869be-180">Upon clicking **Next**, the file format settings are detected automatically.</span></span>  <span data-ttu-id="869be-181">Certifique-se de que delimitador de coluna é ' | 'em vez da vírgula ',' usada como padrão.</span><span class="sxs-lookup"><span data-stu-id="869be-181">Check to make sure that column delimiter is ‘|’ instead of the default comma ‘,’.</span></span>  <span data-ttu-id="869be-182">Clique em **Próximo** depois de ter visualizado os dados.</span><span class="sxs-lookup"><span data-stu-id="869be-182">Click **Next** after you have previewed the data.</span></span>

    ![Assistente de Cópia – configurações de formato de arquivo](media/data-factory-load-sql-data-warehouse/file-format-settings.png)

## <a name="step-3-configure-destination"></a><span data-ttu-id="869be-184">Etapa 3: Configurar o destino</span><span class="sxs-lookup"><span data-stu-id="869be-184">Step 3: Configure destination</span></span>
<span data-ttu-id="869be-185">Esta seção mostra como configurar o destino: tabela `lineitem` no banco de dados do Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="869be-185">This section shows you how to configure the destination: `lineitem` table in the Azure SQL Data Warehouse database.</span></span>

1. <span data-ttu-id="869be-186">Escolha **Azure SQL Data Warehouse** como o repositório de destino e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="869be-186">Choose **Azure SQL Data Warehouse** as the destination store and click **Next**.</span></span>

    ![Assistente de Cópia – selecionar o armazenamento de dados de destino](media/data-factory-load-sql-data-warehouse/select-destination-data-store.png)

2. <span data-ttu-id="869be-188">Preencha as informações de conexão do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="869be-188">Fill in the connection information for Azure SQL Data Warehouse.</span></span>  <span data-ttu-id="869be-189">Certifique-se de especificar o usuário que é membro da função `xlargerc` (consulte a seção **pré-requisitos** para obter instruções detalhadas) e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="869be-189">Make sure you specify the user that is a member of the role `xlargerc` (see the **prerequisites** section for detailed instructions), and click **Next**.</span></span>

    ![Assistente de Cópia – informações de conexão de destino](media/data-factory-load-sql-data-warehouse/destination-connection-info.png)

3. <span data-ttu-id="869be-191">Escolha a tabela de destino e clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="869be-191">Choose the destination table and click **Next**.</span></span>

    ![Assistente de Cópia – página de mapeamento de tabela](media/data-factory-load-sql-data-warehouse/table-mapping-page.png)

4. <span data-ttu-id="869be-193">Na página de mapeamento de esquema, deixe a opção "Aplicar o mapeamento de coluna" desmarcada e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="869be-193">In Schema mapping page, leave "Apply column mapping" option unchecked and click **Next**.</span></span>

## <a name="step-4-performance-settings"></a><span data-ttu-id="869be-194">Etapa 4: Configurações de desempenho</span><span class="sxs-lookup"><span data-stu-id="869be-194">Step 4: Performance settings</span></span>

<span data-ttu-id="869be-195">A opção **Permitir polybase** é marcada por padrão.</span><span class="sxs-lookup"><span data-stu-id="869be-195">**Allow polybase** is checked by default.</span></span>  <span data-ttu-id="869be-196">Clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="869be-196">Click **Next**.</span></span>

![Assistente de Cópia – página de mapeamento de esquema](media/data-factory-load-sql-data-warehouse/performance-settings-page.png)

## <a name="step-5-deploy-and-monitor-load-results"></a><span data-ttu-id="869be-198">Etapa 5: Implantar e monitorar os resultados de carga</span><span class="sxs-lookup"><span data-stu-id="869be-198">Step 5: Deploy and monitor load results</span></span>
1. <span data-ttu-id="869be-199">Clique no botão **Concluir** para implantar.</span><span class="sxs-lookup"><span data-stu-id="869be-199">Click **Finish** button to deploy.</span></span>

    ![Assistente de Cópia – página de resumo](media/data-factory-load-sql-data-warehouse/summary-page.png)

2. <span data-ttu-id="869be-201">Depois que a implantação for concluída, clique em `Click here to monitor copy pipeline` para monitorar o andamento da execução da cópia.</span><span class="sxs-lookup"><span data-stu-id="869be-201">After the deployment is complete, click `Click here to monitor copy pipeline` to monitor the copy run progress.</span></span> <span data-ttu-id="869be-202">Selecione o pipeline de cópia criado na lista **Janelas de Atividade**.</span><span class="sxs-lookup"><span data-stu-id="869be-202">Select the copy pipeline you created in the **Activity Windows** list.</span></span>

    ![Assistente de Cópia – página de resumo](media/data-factory-load-sql-data-warehouse/select-pipeline-monitor-manage-app.png)

    <span data-ttu-id="869be-204">Você pode exibir os detalhes de execução da cópia no **Gerenciador de Janelas de Atividade** no painel direito, incluindo o volume de dados lidos de origem e gravado no destino, a duração e a taxa de transferência média da execução.</span><span class="sxs-lookup"><span data-stu-id="869be-204">You can view the copy run details in the **Activity Window Explorer** in the right panel, including the data volume read from source and written into destination, duration, and the average throughput for the run.</span></span>

    <span data-ttu-id="869be-205">Como você pode ver na captura de tela a seguir, copiar 1 TB do Armazenamento de Blobs do Azure para o SQL Data Warehouse levou 14 minutos, atingindo efetivamente uma taxa de transferência de 1,22 GBps!</span><span class="sxs-lookup"><span data-stu-id="869be-205">As you can see from the following screen shot, copying 1 TB from Azure Blob Storage into SQL Data Warehouse took 14 minutes, effectively achieving 1.22 GBps throughput!</span></span>

    ![Assistente de Cópia – caixa de diálogo de êxito](media/data-factory-load-sql-data-warehouse/succeeded-info.png)

## <a name="best-practices"></a><span data-ttu-id="869be-207">Práticas recomendadas</span><span class="sxs-lookup"><span data-stu-id="869be-207">Best practices</span></span>
<span data-ttu-id="869be-208">Aqui estão algumas práticas recomendadas para a execução de seu banco de dados do Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="869be-208">Here are a few best practices for running your Azure SQL Data Warehouse database:</span></span>

* <span data-ttu-id="869be-209">Use uma classe de recurso maior durante o carregamento em um ÍNDICE COLUMNSTORE CLUSTERIZADO.</span><span class="sxs-lookup"><span data-stu-id="869be-209">Use a larger resource class when loading into a CLUSTERED COLUMNSTORE INDEX.</span></span>
* <span data-ttu-id="869be-210">Para junções mais eficientes, considere usar a distribuição de hash por uma coluna selecionada em vez da distribuição round robin padrão.</span><span class="sxs-lookup"><span data-stu-id="869be-210">For more efficient joins, consider using hash distribution by a select column instead of default round robin distribution.</span></span>
* <span data-ttu-id="869be-211">Para velocidades de carga, considere usar o heap para dados transitórios.</span><span class="sxs-lookup"><span data-stu-id="869be-211">For faster load speeds, consider using heap for transient data.</span></span>
* <span data-ttu-id="869be-212">Crie estatísticas depois de terminar de carregar o Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="869be-212">Create statistics after you finish loading Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="869be-213">Veja [Práticas Recomendadas para o SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="869be-213">See [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md) for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="869be-214">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="869be-214">Next steps</span></span>
* <span data-ttu-id="869be-215">[Assistente de Cópia do Data Factory](data-factory-copy-wizard.md) – este artigo fornece detalhes sobre o Assistente de Cópia.</span><span class="sxs-lookup"><span data-stu-id="869be-215">[Data Factory Copy Wizard](data-factory-copy-wizard.md) - This article provides details about the Copy Wizard.</span></span>
* <span data-ttu-id="869be-216">[Guia de ajuste e desempenho da Atividade de Cópia](data-factory-copy-activity-performance.md) – este artigo contém as medições de desempenho de referência e o guia de ajuste.</span><span class="sxs-lookup"><span data-stu-id="869be-216">[Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) - This article contains the reference performance measurements and tuning guide.</span></span>
