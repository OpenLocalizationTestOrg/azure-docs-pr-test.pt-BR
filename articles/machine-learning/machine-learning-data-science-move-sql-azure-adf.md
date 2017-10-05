---
title: Mover dados de um SQL Server local para o SQL Azure com o Azure Data Factory | Microsoft Docs
description: "Configure um pipeline do ADF que compõe duas atividades de migração de dados que movem os dados juntos diariamente entre bancos de dados locais e na nuvem."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 36837c83-2015-48be-b850-c4346aa5ae8a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 39fe26d3388be8b558f05063a8965889c013a41e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-from-an-on-premises-sql-server-to-sql-azure-with-azure-data-factory"></a><span data-ttu-id="8ffce-103">Mover dados de um SQL Server local para o SQL Azure com o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8ffce-103">Move data from an on-premises SQL server to SQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="8ffce-104">Este tópico mostra como mover dados de um banco de dados do SQL Server local para um banco de dados do SQL Azure por meio do Armazenamento de Blobs do Azure usando o ADF (Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="8ffce-104">This topic shows how to move data from an on-premises SQL Server Database to a SQL Azure Database via Azure Blob Storage using the Azure Data Factory (ADF).</span></span>

<span data-ttu-id="8ffce-105">Para conferir uma tabela que resume diversas opções de movimentação de dados para um Banco de Dados SQL do Azure, consulte [Mover dados para um Banco de Dados SQL do Azure para o Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="8ffce-105">For a table that summarizes various options for moving data to an Azure SQL Database, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <span data-ttu-id="8ffce-106"><a name="intro"></a>Introdução: O que é o ADF e quando ele deve ser usado para migrar dados?</span><span class="sxs-lookup"><span data-stu-id="8ffce-106"><a name="intro"></a>Introduction: What is ADF and when should it be used to migrate data?</span></span>
<span data-ttu-id="8ffce-107">O Azure Data Factory é um serviço de integração de dados baseado em nuvem que automatiza a movimentação e a transformação dos dados.</span><span class="sxs-lookup"><span data-stu-id="8ffce-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="8ffce-108">O conceito fundamental no modelo do ADF é o pipeline.</span><span class="sxs-lookup"><span data-stu-id="8ffce-108">The key concept in the ADF model is pipeline.</span></span> <span data-ttu-id="8ffce-109">Um pipeline é um agrupamento lógico de Atividades, e cada uma delas define as ações a serem executadas nos dados contidos em Conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="8ffce-109">A pipeline is a logical grouping of Activities, each of which defines the actions to perform on the data contained in Datasets.</span></span> <span data-ttu-id="8ffce-110">Serviços vinculados definem as informações necessárias para o Data Factory conectar-se a recursos de dados.</span><span class="sxs-lookup"><span data-stu-id="8ffce-110">Linked services are used to define the information needed for Data Factory to connect to the data resources.</span></span>

<span data-ttu-id="8ffce-111">Com o ADF, serviços de processamento de dados existentes podem ser compostos em pipelines de dados que são altamente disponíveis e gerenciados na nuvem.</span><span class="sxs-lookup"><span data-stu-id="8ffce-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in the cloud.</span></span> <span data-ttu-id="8ffce-112">Esses pipelines de dados podem ser agendados para ingerir, preparar, transformar, analisar e publicar os dados, e o ADF gerencia e orquestra os dados complexos e dependências de processamento.</span><span class="sxs-lookup"><span data-stu-id="8ffce-112">These data pipelines can be scheduled to ingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates the complex data and processing dependencies.</span></span> <span data-ttu-id="8ffce-113">As soluções podem ser criadas e implantadas rapidamente na nuvem, conectando um número crescente de fontes de dados em nuvem e locais.</span><span class="sxs-lookup"><span data-stu-id="8ffce-113">Solutions can be quickly built and deployed in the cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="8ffce-114">Considere usar o ADF:</span><span class="sxs-lookup"><span data-stu-id="8ffce-114">Consider using ADF:</span></span>

* <span data-ttu-id="8ffce-115">quando dados precisarem ser migrados continuamente em um cenário híbrido que acessa recursos locais e de nuvem</span><span class="sxs-lookup"><span data-stu-id="8ffce-115">when data needs to be continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="8ffce-116">quando os dados forem transacionados ou precisarem ser modificados ou ter lógica de negócios adicionada a eles quando estiverem sendo migrados.</span><span class="sxs-lookup"><span data-stu-id="8ffce-116">when the data is transacted or needs to be modified or have business logic added to it when being migrated.</span></span>

<span data-ttu-id="8ffce-117">O ADF permite o planejamento e monitoramento de trabalhos usando scripts simples de JSON que gerenciam a movimentação de dados em intervalos periódicos.</span><span class="sxs-lookup"><span data-stu-id="8ffce-117">ADF allows for the scheduling and monitoring of jobs using simple JSON scripts that manage the movement of data on a periodic basis.</span></span> <span data-ttu-id="8ffce-118">O ADF também possui outros recursos, como suporte para operações complexas.</span><span class="sxs-lookup"><span data-stu-id="8ffce-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="8ffce-119">Para obter mais informações sobre o ADF, consulte a documentação em [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="8ffce-119">For more information on ADF, see the documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <span data-ttu-id="8ffce-120"><a name="scenario"></a>O cenário</span><span class="sxs-lookup"><span data-stu-id="8ffce-120"><a name="scenario"></a>The Scenario</span></span>
<span data-ttu-id="8ffce-121">Criamos um pipeline do ADF que compõe duas atividades de migração de dados.</span><span class="sxs-lookup"><span data-stu-id="8ffce-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="8ffce-122">Juntas, elas movem dados diariamente entre um banco de dados do SQL local e um banco de dados SQL do Azure na nuvem.</span><span class="sxs-lookup"><span data-stu-id="8ffce-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in the cloud.</span></span> <span data-ttu-id="8ffce-123">As duas atividades são:</span><span class="sxs-lookup"><span data-stu-id="8ffce-123">The two activities are:</span></span>

* <span data-ttu-id="8ffce-124">copiar os dados de um banco de dados de SQL Server local para uma conta de Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="8ffce-124">copy data from an on-premises SQL Server database to an Azure Blob Storage account</span></span>
* <span data-ttu-id="8ffce-125">copiar dados da conta de armazenamento de blob do Azure para um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8ffce-125">copy data from the Azure Blob Storage account to an Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="8ffce-126">As etapas mostradas aqui foram adaptadas do tutorial mais detalhado [Mover dados entre fontes locais e a nuvem com o Gateway de Gerenciamento de Dados](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) fornecido pela equipe do ADF e referências para as seções relevantes desse tópico são fornecidas quando apropriado.</span><span class="sxs-lookup"><span data-stu-id="8ffce-126">The steps shown here have been adapted from the more detailed tutorial provided by the ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References to the relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <span data-ttu-id="8ffce-127"><a name="prereqs"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8ffce-127"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="8ffce-128">Este tutorial presume que você tenha:</span><span class="sxs-lookup"><span data-stu-id="8ffce-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="8ffce-129">Uma **assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="8ffce-129">An **Azure subscription**.</span></span> <span data-ttu-id="8ffce-130">Se você não tiver uma assinatura, você pode se inscrever em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ffce-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8ffce-131">Uma **conta de armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="8ffce-131">An **Azure storage account**.</span></span> <span data-ttu-id="8ffce-132">Você usará uma conta de armazenamento do Azure para armazenar os dados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="8ffce-132">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="8ffce-133">Se você não tiver uma conta de armazenamento do Azure, consulte o artigo [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) .</span><span class="sxs-lookup"><span data-stu-id="8ffce-133">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="8ffce-134">Depois de criar a conta de armazenamento, você precisa obter a chave de conta usada para acessar o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8ffce-134">After you have created the storage account, you need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="8ffce-135">Consulte [Manage your storage access keys (Gerenciar as chaves de acesso de armazenamento)](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="8ffce-135">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="8ffce-136">Acesso a um **Banco de dados do SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="8ffce-136">Access to an **Azure SQL Database**.</span></span> <span data-ttu-id="8ffce-137">Se você precisa configurar um Banco de Dados SQL do Azure, o [Guia de Introdução ao Banco de Dados SQL do Microsoft Azure ](../sql-database/sql-database-get-started.md) fornece informações sobre como provisionar uma nova instância de um Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ffce-137">If you must set up an Azure SQL Database, the tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how to provision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="8ffce-138">**Azure PowerShell** instalado e configurado localmente.</span><span class="sxs-lookup"><span data-stu-id="8ffce-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="8ffce-139">Para saber mais, confira [Como instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8ffce-139">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="8ffce-140">Este procedimento usa o [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8ffce-140">This procedure uses the [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <span data-ttu-id="8ffce-141"><a name="upload-data"></a> Carregar os dados para o SQL Server local</span><span class="sxs-lookup"><span data-stu-id="8ffce-141"><a name="upload-data"></a> Upload the data to your on-premises SQL Server</span></span>
<span data-ttu-id="8ffce-142">Usamos o [conjunto de dados de Táxi de NYC](http://chriswhong.com/open-data/foil_nyc_taxi/) para demonstrar o processo de migração.</span><span class="sxs-lookup"><span data-stu-id="8ffce-142">We use the [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) to demonstrate the migration process.</span></span> <span data-ttu-id="8ffce-143">O conjunto de dados de Táxi de NYC está disponível, como observado nessa postagem, nos [Dados de Táxi de NYC](http://www.andresmh.com/nyctaxitrips/)do armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ffce-143">The NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="8ffce-144">Os dados têm dois arquivos, o arquivo trip_data.csv que contém detalhes da viagem e o arquivo trip_far.csv que contém detalhes das tarifas pagas para cada viagem.</span><span class="sxs-lookup"><span data-stu-id="8ffce-144">The data has two files, the trip_data.csv file, which contains trip details, and the  trip_far.csv file, which contains details of the fare paid for each trip.</span></span> <span data-ttu-id="8ffce-145">Um exemplo e uma descrição desses arquivos são fornecidos na [Descrição do Conjunto de Dados de Viagens de Táxi de NYC](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span><span class="sxs-lookup"><span data-stu-id="8ffce-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="8ffce-146">Você pode adaptar o procedimento fornecido aqui para um conjunto de seus próprios dados ou seguir as etapas conforme descrito usando o conjunto de dados de Táxi de NYC.</span><span class="sxs-lookup"><span data-stu-id="8ffce-146">You can either adapt the procedure provided here to a set of your own data or follow the steps as described by using the NYC Taxi dataset.</span></span> <span data-ttu-id="8ffce-147">Para carregar o conjunto de dados de Táxi de NYC em seu banco de dados do SQL Server local, siga o procedimento descrito em [Importação de dados em massa para o Banco de Dados do SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span><span class="sxs-lookup"><span data-stu-id="8ffce-147">To upload the NYC Taxi dataset into your on-premises SQL Server database, follow the procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="8ffce-148">Essas instruções são para um SQL Server em uma máquina virtual do Azure, mas o procedimento para carregar o SQL Server local é o mesmo.</span><span class="sxs-lookup"><span data-stu-id="8ffce-148">These instructions are for a SQL Server on an Azure Virtual Machine, but the procedure for uploading to the on-premises SQL Server is the same.</span></span>

## <span data-ttu-id="8ffce-149"><a name="create-adf"></a> Criar uma Data Factory do Azure</span><span class="sxs-lookup"><span data-stu-id="8ffce-149"><a name="create-adf"></a> Create an Azure Data Factory</span></span>
<span data-ttu-id="8ffce-150">As instruções para criar um novo Azure Data Factory e um grupo de recursos no [Portal do Azure](https://portal.azure.com/) são fornecidas em [Create an Azure Data Factory (Criar um Azure Data Factory)](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span><span class="sxs-lookup"><span data-stu-id="8ffce-150">The instructions for creating a new Azure Data Factory and a resource group in the [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="8ffce-151">Nomeie a nova instância ADF como *adfdsp* e nomeie o grupo de recursos criado como *adfdsprg*.</span><span class="sxs-lookup"><span data-stu-id="8ffce-151">Name the new ADF instance *adfdsp* and name the resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-the-data-management-gateway"></a><span data-ttu-id="8ffce-152">Instalar e configurar o Gateway de gerenciamento de dados</span><span class="sxs-lookup"><span data-stu-id="8ffce-152">Install and configure up the Data Management Gateway</span></span>
<span data-ttu-id="8ffce-153">Para habilitar os pipelines em um Azure Data Factory para trabalhar com um SQL Server local, você precisa adicioná-los como um Serviço vinculado à fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="8ffce-153">To enable your pipelines in an Azure data factory to work with an on-premises SQL Server, you need to add it as a Linked Service to the data factory.</span></span> <span data-ttu-id="8ffce-154">Para criar um Serviço Vinculado para o SQL Server local, você precisa:</span><span class="sxs-lookup"><span data-stu-id="8ffce-154">To create a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="8ffce-155">baixar e instalar o Gateway de Gerenciamento de Dados Microsoft no computador local.</span><span class="sxs-lookup"><span data-stu-id="8ffce-155">download and install Microsoft Data Management Gateway onto the on-premises computer.</span></span>
* <span data-ttu-id="8ffce-156">configurar o serviço vinculado para a fonte de dados local para usar o gateway.</span><span class="sxs-lookup"><span data-stu-id="8ffce-156">configure the linked service for the on-premises data source to use the gateway.</span></span>

<span data-ttu-id="8ffce-157">O Gateway de Gerenciamento de Dados serializa e desserializa dados de origem e do coletor no computador em que está hospedado.</span><span class="sxs-lookup"><span data-stu-id="8ffce-157">The Data Management Gateway serializes and deserializes the source and sink data on the computer where it is hosted.</span></span>

<span data-ttu-id="8ffce-158">Para obter instruções e detalhes de instalação sobre o Gateway de Gerenciamento de Dados, confira [Mover dados entre fontes locais e a nuvem com o Gateway de Gerenciamento de Dados](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="8ffce-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <span data-ttu-id="8ffce-159"><a name="adflinkedservices"></a>Criar serviços vinculados para conectar-se aos recursos de dados</span><span class="sxs-lookup"><span data-stu-id="8ffce-159"><a name="adflinkedservices"></a>Create linked services to connect to the data resources</span></span>
<span data-ttu-id="8ffce-160">Um serviço vinculado define as informações necessárias para o Azure Data Factory conectar-se a um recurso de dados.</span><span class="sxs-lookup"><span data-stu-id="8ffce-160">A linked service defines the information needed for Azure Data Factory to connect to a data resource.</span></span> <span data-ttu-id="8ffce-161">O procedimento passo a passo para criar serviços vinculados é fornecido em [Create linked services (Criar serviços vinculados)](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span><span class="sxs-lookup"><span data-stu-id="8ffce-161">The step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="8ffce-162">Temos três recursos neste cenário para o qual os serviços vinculados são necessários.</span><span class="sxs-lookup"><span data-stu-id="8ffce-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="8ffce-163">Serviço vinculado para SQL Server local</span><span class="sxs-lookup"><span data-stu-id="8ffce-163">Linked service for on-premises SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="8ffce-164">Serviço vinculado do armazenamento de blob do Azure:</span><span class="sxs-lookup"><span data-stu-id="8ffce-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="8ffce-165">Serviço vinculado para o banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="8ffce-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <span data-ttu-id="8ffce-166"><a name="adf-linked-service-onprem-sql"></a>Serviço vinculado para o banco de dados do SQL Server local</span><span class="sxs-lookup"><span data-stu-id="8ffce-166"><a name="adf-linked-service-onprem-sql"></a>Linked service for on-premises SQL Server database</span></span>
<span data-ttu-id="8ffce-167">Para criar um serviço vinculado para o SQL Server local:</span><span class="sxs-lookup"><span data-stu-id="8ffce-167">To create the linked service for the on-premises SQL Server:</span></span>

* <span data-ttu-id="8ffce-168">clique na página de aterrissagem do ADF **Armazenamento de Dados** no Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="8ffce-168">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="8ffce-169">selecione **SQL** e insira as credenciais de *nome de usuário* e *senha* do SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="8ffce-169">select **SQL** and enter the *username* and *password* credentials for the on-premises SQL Server.</span></span> <span data-ttu-id="8ffce-170">É necessário digitar o nome do servidor como um **nome totalmente qualificado do servidor barra invertida nome da instância (servername\instancename)**.</span><span class="sxs-lookup"><span data-stu-id="8ffce-170">You need to enter the servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="8ffce-171">Nomeie o serviço vinculado *adfonpremsql*.</span><span class="sxs-lookup"><span data-stu-id="8ffce-171">Name the linked service *adfonpremsql*.</span></span>

### <span data-ttu-id="8ffce-172"><a name="adf-linked-service-blob-store"></a>Serviço vinculado para Blob</span><span class="sxs-lookup"><span data-stu-id="8ffce-172"><a name="adf-linked-service-blob-store"></a>Linked service for Blob</span></span>
<span data-ttu-id="8ffce-173">Para criar o serviço vinculado para a conta do Armazenamento de Blobs do Azure:</span><span class="sxs-lookup"><span data-stu-id="8ffce-173">To create the linked service for the Azure Blob Storage account:</span></span>

* <span data-ttu-id="8ffce-174">clique na página de aterrissagem do ADF **Armazenamento de Dados** no Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="8ffce-174">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="8ffce-175">selecione **Conta de Armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="8ffce-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="8ffce-176">insira a chave da conta do Armazenamento de Blobs do Azure e o nome do contêiner.</span><span class="sxs-lookup"><span data-stu-id="8ffce-176">enter the Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="8ffce-177">Nomeie o Serviço vinculado como *adfds*.</span><span class="sxs-lookup"><span data-stu-id="8ffce-177">Name the Linked Service *adfds*.</span></span>

### <span data-ttu-id="8ffce-178"><a name="adf-linked-service-azure-sql"></a>Serviço vinculado para o banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="8ffce-178"><a name="adf-linked-service-azure-sql"></a>Linked service for Azure SQL database</span></span>
<span data-ttu-id="8ffce-179">Para criar o serviço vinculado para o banco de dados SQL do Azure:</span><span class="sxs-lookup"><span data-stu-id="8ffce-179">To create the linked service for the Azure SQL Database:</span></span>

* <span data-ttu-id="8ffce-180">clique na página de aterrissagem do ADF **Armazenamento de Dados** no Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="8ffce-180">click the **Data Store** in the ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="8ffce-181">selecione **Azure SQL** e insira as credenciais de *nome de usuário* e *senha* do Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ffce-181">select **Azure SQL** and enter the *username* and *password* credentials for the Azure SQL Database.</span></span> <span data-ttu-id="8ffce-182">O *nome de usuário* deve ser especificado como *user@servername*.</span><span class="sxs-lookup"><span data-stu-id="8ffce-182">The *username* must be specified as *user@servername*.</span></span>   

## <span data-ttu-id="8ffce-183"><a name="adf-tables"></a>Definir e criar tabelas para especificar como acessar os conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="8ffce-183"><a name="adf-tables"></a>Define and create tables to specify how to access the datasets</span></span>
<span data-ttu-id="8ffce-184">Crie tabelas que especificam a estrutura, a localização e a disponibilidade dos conjuntos de dados com os procedimentos a seguir baseados em script.</span><span class="sxs-lookup"><span data-stu-id="8ffce-184">Create tables that specify the structure, location, and availability of the datasets with the following script-based procedures.</span></span> <span data-ttu-id="8ffce-185">Os arquivos JSON são usados para definir as tabelas.</span><span class="sxs-lookup"><span data-stu-id="8ffce-185">JSON files are used to define the tables.</span></span> <span data-ttu-id="8ffce-186">Para obter mais informações sobre a estrutura desses arquivos, consulte [Conjuntos de dados](../data-factory/data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="8ffce-186">For more information on the structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8ffce-187">Você deve executar o cmdlet `Add-AzureAccount` antes de executar o cmdlet [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) para confirmar que a assinatura correta do Azure esteja selecionada para a execução do comando.</span><span class="sxs-lookup"><span data-stu-id="8ffce-187">You should execute the `Add-AzureAccount` cmdlet before executing the [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet to confirm that the right Azure subscription is selected for the command execution.</span></span> <span data-ttu-id="8ffce-188">Para obter a documentação desse cmdlet, consulte [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="8ffce-188">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="8ffce-189">As definições baseadas em JSON nas tabelas usam os seguintes nomes:</span><span class="sxs-lookup"><span data-stu-id="8ffce-189">The JSON-based definitions in the tables use the following names:</span></span>

* <span data-ttu-id="8ffce-190">o **nome da tabela** no SQL Server local é *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="8ffce-190">the **table name** in the on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="8ffce-191">o **nome do contêiner** na conta de armazenamento de Blob do Azure é *containername\\\\\\\\\\*</span><span class="sxs-lookup"><span data-stu-id="8ffce-191">the **container name** in the Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="8ffce-192">Três definições de tabela são necessárias para este pipeline do ADF:</span><span class="sxs-lookup"><span data-stu-id="8ffce-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="8ffce-193">Tabela do SQL local</span><span class="sxs-lookup"><span data-stu-id="8ffce-193">SQL on-premises Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="8ffce-194">Tabela de blob </span><span class="sxs-lookup"><span data-stu-id="8ffce-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="8ffce-195">Tabela do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="8ffce-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="8ffce-196">Estes procedimentos usam o Azure PowerShell para definir e criar as atividades do ADF.</span><span class="sxs-lookup"><span data-stu-id="8ffce-196">These procedures use Azure PowerShell to define and create the ADF activities.</span></span> <span data-ttu-id="8ffce-197">Mas essas tarefas também podem ser realizadas pelo Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ffce-197">But these tasks can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="8ffce-198">Para obter detalhes, consulte [Criar conjuntos de dados](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span><span class="sxs-lookup"><span data-stu-id="8ffce-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <span data-ttu-id="8ffce-199"><a name="adf-table-onprem-sql"></a>Tabela do SQL local</span><span class="sxs-lookup"><span data-stu-id="8ffce-199"><a name="adf-table-onprem-sql"></a>SQL on-premises Table</span></span>
<span data-ttu-id="8ffce-200">A definição da tabela do SQL Server local é especificada no seguinte arquivo JSON:</span><span class="sxs-lookup"><span data-stu-id="8ffce-200">The table definition for the on-premises SQL Server is specified in the following JSON file:</span></span>

        {
            "name": "OnPremSQLTable",
            "properties":
            {
                "location":
                {
                "type": "OnPremisesSqlServerTableLocation",
                "tableName": "nyctaxi_data",
                "linkedServiceName": "adfonpremsql"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1,   
                "waitOnExternal":
                {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
                }

                }
            }
        }

<span data-ttu-id="8ffce-201">Os nomes de coluna não foram incluídos aqui.</span><span class="sxs-lookup"><span data-stu-id="8ffce-201">The column names were not included here.</span></span> <span data-ttu-id="8ffce-202">Você pode fazer uma subseleção nos nomes das colunas incluindo-os aqui (para obter detalhes, verifique o tópico [documentação ADF](../data-factory/data-factory-data-movement-activities.md) ).</span><span class="sxs-lookup"><span data-stu-id="8ffce-202">You can sub-select on the column names by including them here (for details check the [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="8ffce-203">Copie a definição de JSON da tabela em um arquivo chamado *onpremtabledef.json* e salve-o em um local conhecido (neste caso deve ser *C:\temp\onpremtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="8ffce-203">Copy the JSON definition of the table into a file called *onpremtabledef.json* file and save it to a known location (here assumed to be *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="8ffce-204">Crie a tabela no ADF com o seguinte cmdlet do Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8ffce-204">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <span data-ttu-id="8ffce-205"><a name="adf-table-blob-store"></a>Tabela de blob</span><span class="sxs-lookup"><span data-stu-id="8ffce-205"><a name="adf-table-blob-store"></a>Blob Table</span></span>
<span data-ttu-id="8ffce-206">A definição da tabela para o local do blob de saída está a seguir (isso mapeia os dados ingeridos localmente para o blob do Azure):</span><span class="sxs-lookup"><span data-stu-id="8ffce-206">Definition for the table for the output blob location is in the following (this maps the ingested data from on-premises to Azure blob):</span></span>

        {
            "name": "OutputBlobTable",
            "properties":
            {
                "location":
                {
                "type": "AzureBlobLocation",
                "folderPath": "containername",
                "format":
                {
                "type": "TextFormat",
                "columnDelimiter": "\t"
                },
                "linkedServiceName": "adfds"
                },
                "availability":
                {
                "frequency": "Day",
                "interval": 1
                }
            }
        }

<span data-ttu-id="8ffce-207">Copie a definição de JSON da tabela para um arquivo chamado *bloboutputtabledef.json* e salve-o em um local conhecido (neste caso deve ser *C:\temp\bloboutputtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="8ffce-207">Copy the JSON definition of the table into a file called *bloboutputtabledef.json* file and save it to a known location (here assumed to be *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="8ffce-208">Crie a tabela no ADF com o seguinte cmdlet do Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8ffce-208">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <span data-ttu-id="8ffce-209"><a name="adf-table-azure-sq"></a>Tabela do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="8ffce-209"><a name="adf-table-azure-sq"></a>SQL Azure Table</span></span>
<span data-ttu-id="8ffce-210">A definição da tabela para a saída do SQL Azure está a seguir (esse esquema mapeia os dados provenientes do blob):</span><span class="sxs-lookup"><span data-stu-id="8ffce-210">Definition for the table for the SQL Azure output is in the following (this schema maps the data coming from the blob):</span></span>

    {
        "name": "OutputSQLAzureTable",
        "properties":
        {
            "structure":
            [
                { "name": "column1", type": "String"},
                { "name": "column2", type": "String"}                
            ],
            "location":
            {
                "type": "AzureSqlTableLocation",
                "tableName": "your_db_name",
                "linkedServiceName": "adfdssqlazure_linked_servicename"
            },
            "availability":
            {
                "frequency": "Day",
                "interval": 1            
            }
        }
    }

<span data-ttu-id="8ffce-211">Copie a definição de JSON da tabela em um arquivo chamado *AzureSqlTable.json* e salve-o em um local conhecido (neste caso deve ser *C:\temp\AzureSqlTable.json*).</span><span class="sxs-lookup"><span data-stu-id="8ffce-211">Copy the JSON definition of the table into a file called *AzureSqlTable.json* file and save it to a known location (here assumed to be *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="8ffce-212">Crie a tabela no ADF com o seguinte cmdlet do Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8ffce-212">Create the table in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <span data-ttu-id="8ffce-213"><a name="adf-pipeline"></a>Definir e criar o pipeline</span><span class="sxs-lookup"><span data-stu-id="8ffce-213"><a name="adf-pipeline"></a>Define and create the pipeline</span></span>
<span data-ttu-id="8ffce-214">Especifique as atividades que pertencem ao pipeline e crie o pipeline com os procedimentos a seguir baseados em script.</span><span class="sxs-lookup"><span data-stu-id="8ffce-214">Specify the activities that belong to the pipeline and create the pipeline with the following script-based procedures.</span></span> <span data-ttu-id="8ffce-215">Um arquivo JSON é usado para definir as propriedades de pipeline.</span><span class="sxs-lookup"><span data-stu-id="8ffce-215">A JSON file is used to define the pipeline properties.</span></span>

* <span data-ttu-id="8ffce-216">O script assume que o **nome do pipeline** é *AMLDSProcessPipeline*.</span><span class="sxs-lookup"><span data-stu-id="8ffce-216">The script assumes that the **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="8ffce-217">Observe também que definimos a periodicidade do pipeline para ser executado diariamente e usar o tempo de execução padrão para o trabalho (12:00 UTC).</span><span class="sxs-lookup"><span data-stu-id="8ffce-217">Also note that we set the periodicity of the pipeline to be executed on daily basis and use the default execution time for the job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="8ffce-218">Os procedimentos a seguir usam o Azure PowerShell para definir e criar o pipeline do ADF.</span><span class="sxs-lookup"><span data-stu-id="8ffce-218">The following procedures use Azure PowerShell to define and create the ADF pipeline.</span></span> <span data-ttu-id="8ffce-219">Mas essa tarefa também pode ser realizada pelo Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8ffce-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="8ffce-220">Para obter detalhes, consulte [Criar pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span><span class="sxs-lookup"><span data-stu-id="8ffce-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="8ffce-221">Usando as definições de tabela fornecidas anteriormente, a definição de pipeline para o ADF é especificada da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8ffce-221">Using the table definitions provided previously, the pipeline definition for the ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL to Azure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server to blob",     
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OnPremSQLTable"} ],
                        "outputs": [ {"name": "OutputBlobTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "SqlSource",
                                "sqlReaderQuery": "select * from nyctaxi_data"
                            },
                            "sink":
                            {
                                "type": "BlobSink"
                            }   
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 0,
                            "timeout": "01:00:00"
                        }       

                     },

                    {
                        "name": "CopyFromBlobtoSQLAzure",
                        "description": "Push data to Sql Azure",        
                        "type": "CopyActivity",
                        "inputs": [ {"name": "OutputBlobTable"} ],
                        "outputs": [ {"name": "OutputSQLAzureTable"} ],
                        "transformation":
                        {
                            "source":
                            {                               
                                "type": "BlobSource"
                            },
                            "sink":
                            {
                                "type": "SqlSink",
                                "WriteBatchTimeout": "00:5:00",                
                            }            
                        },
                        "Policy":
                        {
                            "concurrency": 3,
                            "executionPriorityOrder": "NewestFirst",
                            "style": "StartOfInterval",
                            "retry": 2,
                            "timeout": "02:00:00"
                        }
                     }
                ]
            }
        }

<span data-ttu-id="8ffce-222">Copie a definição de JSON da tabela em um arquivo chamado *pipelinedef.json* e salve-o em um local conhecido (neste caso deve ser *C:\temp\pipelinedef.json*).</span><span class="sxs-lookup"><span data-stu-id="8ffce-222">Copy this JSON definition of the pipeline into a file called *pipelinedef.json* file and save it to a known location (here assumed to be *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="8ffce-223">Crie o pipeline no ADF com o seguinte cmdlet do Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="8ffce-223">Create the pipeline in ADF with the following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="8ffce-224">Confirme que você pode ver o pipeline no ADF no Portal Clássico do Azure da seguinte forma (quando você clicar no diagrama)</span><span class="sxs-lookup"><span data-stu-id="8ffce-224">Confirm that you can see the pipeline on the ADF in the Azure Classic Portal show up as following (when you click the diagram)</span></span>

![Pipeline do ADF](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <span data-ttu-id="8ffce-226"><a name="adf-pipeline-start"></a>Iniciar o Pipeline</span><span class="sxs-lookup"><span data-stu-id="8ffce-226"><a name="adf-pipeline-start"></a>Start the Pipeline</span></span>
<span data-ttu-id="8ffce-227">O pipeline agora pode ser executado usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8ffce-227">The pipeline can now be run using the following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="8ffce-228">Os valores de parâmetro *startdate* e *enddate* precisam ser substituídos pelas datas reais entre os quais você deseja executar o pipeline.</span><span class="sxs-lookup"><span data-stu-id="8ffce-228">The *startdate* and *enddate* parameter values need to be replaced with the actual dates between which you want the pipeline to run.</span></span>

<span data-ttu-id="8ffce-229">Depois que o pipeline é executado, você poderá ver os dados aparecerem no contêiner selecionado para o blob, um arquivo por dia.</span><span class="sxs-lookup"><span data-stu-id="8ffce-229">Once the pipeline executes, you should be able to see the data show up in the container selected for the blob, one file per day.</span></span>

<span data-ttu-id="8ffce-230">Observe que não utilizamos a funcionalidade fornecida pelo ADF para dados de pipe incrementalmente.</span><span class="sxs-lookup"><span data-stu-id="8ffce-230">Note that we have not leveraged the functionality provided by ADF to pipe data incrementally.</span></span> <span data-ttu-id="8ffce-231">Para obter mais informações sobre como fazer isso e outros recursos fornecidos pelo ADF, consulte a [documentação do ADF](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="8ffce-231">For more information on how to do this and other capabilities provided by ADF, see the [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
