---
title: dados de aaaMove de um tooSQL do SQL Server no local do Azure com o Azure Data Factory | Microsoft Docs
description: "Configure um pipeline do ADF que compõe duas atividades de migração de dados que juntos mover dados em uma base diária entre bancos de dados locais e na nuvem de saudação."
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
ms.openlocfilehash: 7f7e78c7a84a259539221d3235b76bb5a3cf9866
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-sql-server-toosql-azure-with-azure-data-factory"></a><span data-ttu-id="4ab46-103">Mover dados de um tooSQL de servidor local no SQL Azure com o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="4ab46-103">Move data from an on-premises SQL server tooSQL Azure with Azure Data Factory</span></span>
<span data-ttu-id="4ab46-104">Este tópico mostra como toomove dados de um tooa de banco de dados do SQL Server local banco de dados do SQL Azure por meio do armazenamento de Blob do Azure usando Olá fábrica de dados do Azure (AAD).</span><span class="sxs-lookup"><span data-stu-id="4ab46-104">This topic shows how toomove data from an on-premises SQL Server Database tooa SQL Azure Database via Azure Blob Storage using hello Azure Data Factory (ADF).</span></span>

<span data-ttu-id="4ab46-105">Para uma tabela que resume as várias opções para mover dados tooan banco de dados do SQL Azure, consulte [mover dados tooan banco de dados do SQL Azure para o aprendizado de máquina do Azure](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="4ab46-105">For a table that summarizes various options for moving data tooan Azure SQL Database, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

## <span data-ttu-id="4ab46-106"><a name="intro"></a>Introdução: O que é ADF e quando ele deve ser usado toomigrate dados?</span><span class="sxs-lookup"><span data-stu-id="4ab46-106"><a name="intro"></a>Introduction: What is ADF and when should it be used toomigrate data?</span></span>
<span data-ttu-id="4ab46-107">A fábrica de dados do Azure é um serviço de integração de dados totalmente gerenciado baseado em nuvem que orquestra e automatiza a movimentação de saudação e transformação de dados.</span><span class="sxs-lookup"><span data-stu-id="4ab46-107">Azure Data Factory is a fully managed cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="4ab46-108">conceito-chave no modelo do ADF Olá Olá é pipeline.</span><span class="sxs-lookup"><span data-stu-id="4ab46-108">hello key concept in hello ADF model is pipeline.</span></span> <span data-ttu-id="4ab46-109">Um pipeline é um agrupamento lógico de atividades, cada uma delas define Olá ações tooperform nos dados Olá contidos em conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="4ab46-109">A pipeline is a logical grouping of Activities, each of which defines hello actions tooperform on hello data contained in Datasets.</span></span> <span data-ttu-id="4ab46-110">Serviços vinculados são informações de saudação do toodefine usado necessárias para recursos de dados do Data Factory tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="4ab46-110">Linked services are used toodefine hello information needed for Data Factory tooconnect toohello data resources.</span></span>

<span data-ttu-id="4ab46-111">Com o ADF, serviços de processamento de dados existentes podem ser compostos em pipelines de dados que são altamente disponíveis e gerenciados em nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="4ab46-111">With ADF, existing data processing services can be composed into data pipelines that are highly available and managed in hello cloud.</span></span> <span data-ttu-id="4ab46-112">Desses pipelines de dados podem ser agendado tooingest, preparar, transformar, analisar e publicar dados e ADF gerencia e organiza dados complexos hello e dependências de processamento.</span><span class="sxs-lookup"><span data-stu-id="4ab46-112">These data pipelines can be scheduled tooingest, prepare, transform, analyze, and publish data, and ADF manages and orchestrates hello complex data and processing dependencies.</span></span> <span data-ttu-id="4ab46-113">As soluções podem ser nuvem Olá rapidamente construído e implantado no, conectar-se um número crescente de locais e fontes de dados na nuvem.</span><span class="sxs-lookup"><span data-stu-id="4ab46-113">Solutions can be quickly built and deployed in hello cloud, connecting a growing number of on-premises and cloud data sources.</span></span>

<span data-ttu-id="4ab46-114">Considere usar o ADF:</span><span class="sxs-lookup"><span data-stu-id="4ab46-114">Consider using ADF:</span></span>

* <span data-ttu-id="4ab46-115">Quando dados necessidades toobe continuamente migrado em um cenário híbrido que acessa os dois locais e recursos de nuvem</span><span class="sxs-lookup"><span data-stu-id="4ab46-115">when data needs toobe continually migrated in a hybrid scenario that accesses both on-premises and cloud resources</span></span>
* <span data-ttu-id="4ab46-116">Quando dados saudação são transacionados ou necessidades toobe modificado ou tem lógica de negócios adicionado tooit quando está sendo migrado.</span><span class="sxs-lookup"><span data-stu-id="4ab46-116">when hello data is transacted or needs toobe modified or have business logic added tooit when being migrated.</span></span>

<span data-ttu-id="4ab46-117">ADF permite Olá planejamento e monitoramento de trabalhos usando scripts JSON simples que gerencia Olá movimento de dados em uma base periódica.</span><span class="sxs-lookup"><span data-stu-id="4ab46-117">ADF allows for hello scheduling and monitoring of jobs using simple JSON scripts that manage hello movement of data on a periodic basis.</span></span> <span data-ttu-id="4ab46-118">O ADF também possui outros recursos, como suporte para operações complexas.</span><span class="sxs-lookup"><span data-stu-id="4ab46-118">ADF also has other capabilities such as support for complex operations.</span></span> <span data-ttu-id="4ab46-119">Para obter mais informações sobre o AAD, consulte a documentação de saudação em [fábrica de dados do Azure (AAD)](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="4ab46-119">For more information on ADF, see hello documentation at [Azure Data Factory (ADF)](https://azure.microsoft.com/services/data-factory/).</span></span>

## <span data-ttu-id="4ab46-120"><a name="scenario"></a>Olá cenário</span><span class="sxs-lookup"><span data-stu-id="4ab46-120"><a name="scenario"></a>hello Scenario</span></span>
<span data-ttu-id="4ab46-121">Criamos um pipeline do ADF que compõe duas atividades de migração de dados.</span><span class="sxs-lookup"><span data-stu-id="4ab46-121">We set up an ADF pipeline that composes two data migration activities.</span></span> <span data-ttu-id="4ab46-122">Juntos eles mover dados em uma base diária entre um banco de dados do SQL local e um banco de dados do SQL Azure na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="4ab46-122">Together they move data on a daily basis between an on-premises SQL database and an Azure SQL Database in hello cloud.</span></span> <span data-ttu-id="4ab46-123">Olá duas atividades são:</span><span class="sxs-lookup"><span data-stu-id="4ab46-123">hello two activities are:</span></span>

* <span data-ttu-id="4ab46-124">copiar dados de um tooan de banco de dados do SQL Server local conta de armazenamento de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="4ab46-124">copy data from an on-premises SQL Server database tooan Azure Blob Storage account</span></span>
* <span data-ttu-id="4ab46-125">copiar dados de tooan de conta de armazenamento de BLOBs do Azure hello Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="4ab46-125">copy data from hello Azure Blob Storage account tooan Azure SQL Database.</span></span>

> [!NOTE]
> <span data-ttu-id="4ab46-126">Olá etapas mostradas aqui foram adaptado hello mais detalhadas tutorial fornecida pela equipe do ADF Olá: [mover dados entre fontes locais e na nuvem com o Gateway de gerenciamento de dados](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) faz referência a seções relevantes toohello desse tópico são fornecidas quando apropriado.</span><span class="sxs-lookup"><span data-stu-id="4ab46-126">hello steps shown here have been adapted from hello more detailed tutorial provided by hello ADF team: [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md) References toohello relevant sections of that topic are provided when appropriate.</span></span>
>
>

## <span data-ttu-id="4ab46-127"><a name="prereqs"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4ab46-127"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="4ab46-128">Este tutorial presume que você tenha:</span><span class="sxs-lookup"><span data-stu-id="4ab46-128">This tutorial assumes you have:</span></span>

* <span data-ttu-id="4ab46-129">Uma **assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="4ab46-129">An **Azure subscription**.</span></span> <span data-ttu-id="4ab46-130">Se você não tiver uma assinatura, você pode se inscrever em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4ab46-130">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4ab46-131">Uma **conta de armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="4ab46-131">An **Azure storage account**.</span></span> <span data-ttu-id="4ab46-132">Você pode usar uma conta de armazenamento do Azure para armazenar dados de saudação neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="4ab46-132">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="4ab46-133">Se você não tiver uma conta de armazenamento do Azure, consulte Olá [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artigo.</span><span class="sxs-lookup"><span data-stu-id="4ab46-133">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="4ab46-134">Depois que você criou a conta de armazenamento hello, você precisa de conta de saudação tooobtain chave usada tooaccess armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ab46-134">After you have created hello storage account, you need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="4ab46-135">Confira [Gerenciar as chaves de acesso de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="4ab46-135">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="4ab46-136">Acesso tooan **banco de dados do SQL Azure**.</span><span class="sxs-lookup"><span data-stu-id="4ab46-136">Access tooan **Azure SQL Database**.</span></span> <span data-ttu-id="4ab46-137">Se você deve configurar um banco de dados do SQL Azure, Olá tpoic [guia de Introdução ao banco de dados SQL do Microsoft Azure ](../sql-database/sql-database-get-started.md) fornece informações sobre como tooprovision uma nova instância de um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab46-137">If you must set up an Azure SQL Database, hello tpoic [Getting Started with Microsoft Azure SQL Database ](../sql-database/sql-database-get-started.md) provides information on how tooprovision a new instance of an Azure SQL Database.</span></span>
* <span data-ttu-id="4ab46-138">**Azure PowerShell** instalado e configurado localmente.</span><span class="sxs-lookup"><span data-stu-id="4ab46-138">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="4ab46-139">Para obter instruções, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4ab46-139">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!NOTE]
> <span data-ttu-id="4ab46-140">Este procedimento usa Olá [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4ab46-140">This procedure uses hello [Azure portal](https://portal.azure.com/).</span></span>
>
>

## <span data-ttu-id="4ab46-141"><a name="upload-data"></a>Carregamento Olá dados tooyour do SQL Server local</span><span class="sxs-lookup"><span data-stu-id="4ab46-141"><a name="upload-data"></a> Upload hello data tooyour on-premises SQL Server</span></span>
<span data-ttu-id="4ab46-142">Usamos Olá [NYC táxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate processo de migração de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ab46-142">We use hello [NYC Taxi dataset](http://chriswhong.com/open-data/foil_nyc_taxi/) toodemonstrate hello migration process.</span></span> <span data-ttu-id="4ab46-143">Olá NYC táxi dataset estiver disponível, conforme observado na postagem do que, no armazenamento de BLOBs do Azure [NYC táxi dados](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="4ab46-143">hello NYC Taxi dataset is available, as noted in that post, on Azure blob storage [NYC Taxi Data](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="4ab46-144">dados de saudação tem dois arquivos, o arquivo de trip_data.csv de saudação que contém detalhes de processamento, e o arquivo de trip_far.csv de hello, que contém detalhes de passagens Olá pago para cada viagem.</span><span class="sxs-lookup"><span data-stu-id="4ab46-144">hello data has two files, hello trip_data.csv file, which contains trip details, and hello  trip_far.csv file, which contains details of hello fare paid for each trip.</span></span> <span data-ttu-id="4ab46-145">Um exemplo e uma descrição desses arquivos são fornecidos na [Descrição do Conjunto de Dados de Viagens de Táxi de NYC](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span><span class="sxs-lookup"><span data-stu-id="4ab46-145">A sample and description of these files are provided in [NYC Taxi Trips Dataset Description](machine-learning-data-science-process-sql-walkthrough.md#dataset).</span></span>

<span data-ttu-id="4ab46-146">Você pode adaptar procedimento Olá fornecido aqui tooa conjunto de seus próprios dados ou execute as etapas de saudação conforme descrito usando Olá NYC táxi dataset.</span><span class="sxs-lookup"><span data-stu-id="4ab46-146">You can either adapt hello procedure provided here tooa set of your own data or follow hello steps as described by using hello NYC Taxi dataset.</span></span> <span data-ttu-id="4ab46-147">Olá tooupload NYC táxi de conjunto de dados em seu banco de dados do SQL Server local, execute o procedimento de saudação descrito no [dados de importação em massa no banco de dados do SQL Server](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span><span class="sxs-lookup"><span data-stu-id="4ab46-147">tooupload hello NYC Taxi dataset into your on-premises SQL Server database, follow hello procedure outlined in [Bulk Import Data into SQL Server Database](machine-learning-data-science-process-sql-walkthrough.md#dbload).</span></span> <span data-ttu-id="4ab46-148">Essas instruções são para um SQL Server em uma máquina Virtual do Azure, mas o procedimento Olá para carregar toohello local SQL Server é Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="4ab46-148">These instructions are for a SQL Server on an Azure Virtual Machine, but hello procedure for uploading toohello on-premises SQL Server is hello same.</span></span>

## <span data-ttu-id="4ab46-149"><a name="create-adf"></a> Criar uma Data Factory do Azure</span><span class="sxs-lookup"><span data-stu-id="4ab46-149"><a name="create-adf"></a> Create an Azure Data Factory</span></span>
<span data-ttu-id="4ab46-150">Olá instruções para criar uma nova fábrica de dados do Azure e um grupo de recursos no hello [portal do Azure](https://portal.azure.com/) são fornecidos [criar uma fábrica de dados do Azure](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span><span class="sxs-lookup"><span data-stu-id="4ab46-150">hello instructions for creating a new Azure Data Factory and a resource group in hello [Azure portal](https://portal.azure.com/) are provided [Create an Azure Data Factory](../data-factory/data-factory-build-your-first-pipeline-using-editor.md#create-data-factory).</span></span> <span data-ttu-id="4ab46-151">Nome hello nova ADF instância *adfdsp* e o grupo de recursos de saudação do nome criado *adfdsprg*.</span><span class="sxs-lookup"><span data-stu-id="4ab46-151">Name hello new ADF instance *adfdsp* and name hello resource group created *adfdsprg*.</span></span>

## <a name="install-and-configure-up-hello-data-management-gateway"></a><span data-ttu-id="4ab46-152">Instalar e configurar o hello Gateway de gerenciamento de dados</span><span class="sxs-lookup"><span data-stu-id="4ab46-152">Install and configure up hello Data Management Gateway</span></span>
<span data-ttu-id="4ab46-153">tooenable seus pipelines em um toowork da fábrica de dados do Azure com um SQL Server no local, você precisa tooadd-lo como uma fábrica de dados do serviço vinculado toohello.</span><span class="sxs-lookup"><span data-stu-id="4ab46-153">tooenable your pipelines in an Azure data factory toowork with an on-premises SQL Server, you need tooadd it as a Linked Service toohello data factory.</span></span> <span data-ttu-id="4ab46-154">toocreate um serviço vinculado para um SQL Server local, você deve:</span><span class="sxs-lookup"><span data-stu-id="4ab46-154">toocreate a Linked Service for an on-premises SQL Server, you must:</span></span>

* <span data-ttu-id="4ab46-155">Baixe e instale o Gateway de gerenciamento de dados do Microsoft no computador do local de saudação.</span><span class="sxs-lookup"><span data-stu-id="4ab46-155">download and install Microsoft Data Management Gateway onto hello on-premises computer.</span></span>
* <span data-ttu-id="4ab46-156">Configure o serviço de saudação vinculado Olá local gateway de dados fonte toouse hello.</span><span class="sxs-lookup"><span data-stu-id="4ab46-156">configure hello linked service for hello on-premises data source toouse hello gateway.</span></span>

<span data-ttu-id="4ab46-157">Olá Data Management Gateway serializa e desserializa os dados de origem e do coletor de saudação no computador Olá onde ele está hospedado.</span><span class="sxs-lookup"><span data-stu-id="4ab46-157">hello Data Management Gateway serializes and deserializes hello source and sink data on hello computer where it is hosted.</span></span>

<span data-ttu-id="4ab46-158">Para obter instruções e detalhes de instalação sobre o Gateway de Gerenciamento de Dados, confira [Mover dados entre fontes locais e a nuvem com o Gateway de Gerenciamento de Dados](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="4ab46-158">For set-up instructions and details on Data Management Gateway, see [Move data between on-premises sources and cloud with Data Management Gateway](../data-factory/data-factory-move-data-between-onprem-and-cloud.md)</span></span>

## <span data-ttu-id="4ab46-159"><a name="adflinkedservices"></a>Criar serviços vinculados tooconnect toohello recursos de dados</span><span class="sxs-lookup"><span data-stu-id="4ab46-159"><a name="adflinkedservices"></a>Create linked services tooconnect toohello data resources</span></span>
<span data-ttu-id="4ab46-160">Um serviço vinculado define informações de saudação necessárias para o recurso de dados do Azure Data Factory tooconnect tooa.</span><span class="sxs-lookup"><span data-stu-id="4ab46-160">A linked service defines hello information needed for Azure Data Factory tooconnect tooa data resource.</span></span> <span data-ttu-id="4ab46-161">procedimento passo a passo de saudação para criar serviços vinculados é fornecido em [criar serviços vinculados](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span><span class="sxs-lookup"><span data-stu-id="4ab46-161">hello step-by-step procedure for creating linked services is provided in [Create linked services](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-linked-services).</span></span>

<span data-ttu-id="4ab46-162">Temos três recursos neste cenário para o qual os serviços vinculados são necessários.</span><span class="sxs-lookup"><span data-stu-id="4ab46-162">We have three resources in this scenario for which linked services are needed.</span></span>

1. [<span data-ttu-id="4ab46-163">Serviço vinculado para SQL Server local</span><span class="sxs-lookup"><span data-stu-id="4ab46-163">Linked service for on-premises SQL Server</span></span>](#adf-linked-service-onprem-sql)
2. [<span data-ttu-id="4ab46-164">Serviço vinculado do armazenamento de blob do Azure:</span><span class="sxs-lookup"><span data-stu-id="4ab46-164">Linked service for Azure Blob Storage</span></span>](#adf-linked-service-blob-store)
3. [<span data-ttu-id="4ab46-165">Serviço vinculado para o banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="4ab46-165">Linked service for Azure SQL database</span></span>](#adf-linked-service-azure-sql)

### <span data-ttu-id="4ab46-166"><a name="adf-linked-service-onprem-sql"></a>Serviço vinculado para o banco de dados do SQL Server local</span><span class="sxs-lookup"><span data-stu-id="4ab46-166"><a name="adf-linked-service-onprem-sql"></a>Linked service for on-premises SQL Server database</span></span>
<span data-ttu-id="4ab46-167">toocreate Olá vinculado serviço para Olá local do SQL Server:</span><span class="sxs-lookup"><span data-stu-id="4ab46-167">toocreate hello linked service for hello on-premises SQL Server:</span></span>

* <span data-ttu-id="4ab46-168">Clique em Olá **repositório de dados** na página de aterrissagem Olá AAD no Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="4ab46-168">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="4ab46-169">Selecione **SQL** e digite Olá *username* e *senha* as credenciais para saudação do SQL Server local.</span><span class="sxs-lookup"><span data-stu-id="4ab46-169">select **SQL** and enter hello *username* and *password* credentials for hello on-premises SQL Server.</span></span> <span data-ttu-id="4ab46-170">Você precisa tooenter Olá servername como um **nome de instância de barra invertida nome totalmente qualificado do servidor (nome_do_servidor \ nome_da_instância)**.</span><span class="sxs-lookup"><span data-stu-id="4ab46-170">You need tooenter hello servername as a **fully qualified servername backslash instance name (servername\instancename)**.</span></span> <span data-ttu-id="4ab46-171">Serviço vinculado de saudação do nome *adfonpremsql*.</span><span class="sxs-lookup"><span data-stu-id="4ab46-171">Name hello linked service *adfonpremsql*.</span></span>

### <span data-ttu-id="4ab46-172"><a name="adf-linked-service-blob-store"></a>Serviço vinculado para Blob</span><span class="sxs-lookup"><span data-stu-id="4ab46-172"><a name="adf-linked-service-blob-store"></a>Linked service for Blob</span></span>
<span data-ttu-id="4ab46-173">toocreate Olá serviço vinculado para conta de armazenamento de BLOBs do Azure hello:</span><span class="sxs-lookup"><span data-stu-id="4ab46-173">toocreate hello linked service for hello Azure Blob Storage account:</span></span>

* <span data-ttu-id="4ab46-174">Clique em Olá **repositório de dados** na página de aterrissagem Olá AAD no Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="4ab46-174">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="4ab46-175">selecione **Conta de Armazenamento do Azure**</span><span class="sxs-lookup"><span data-stu-id="4ab46-175">select **Azure Storage Account**</span></span>
* <span data-ttu-id="4ab46-176">Digite o nome de chave e o contêiner de conta de armazenamento de BLOBs do Azure do hello.</span><span class="sxs-lookup"><span data-stu-id="4ab46-176">enter hello Azure Blob Storage account key and container name.</span></span> <span data-ttu-id="4ab46-177">Saudação de nome de serviço vinculado *adfds*.</span><span class="sxs-lookup"><span data-stu-id="4ab46-177">Name hello Linked Service *adfds*.</span></span>

### <span data-ttu-id="4ab46-178"><a name="adf-linked-service-azure-sql"></a>Serviço vinculado para o banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="4ab46-178"><a name="adf-linked-service-azure-sql"></a>Linked service for Azure SQL database</span></span>
<span data-ttu-id="4ab46-179">toocreate Olá serviço vinculado para hello Azure SQL Database:</span><span class="sxs-lookup"><span data-stu-id="4ab46-179">toocreate hello linked service for hello Azure SQL Database:</span></span>

* <span data-ttu-id="4ab46-180">Clique em Olá **repositório de dados** na página de aterrissagem Olá AAD no Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="4ab46-180">click hello **Data Store** in hello ADF landing page on Azure Classic Portal</span></span>
* <span data-ttu-id="4ab46-181">Selecione **SQL Azure** e digite Olá *username* e *senha* credenciais para hello Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="4ab46-181">select **Azure SQL** and enter hello *username* and *password* credentials for hello Azure SQL Database.</span></span> <span data-ttu-id="4ab46-182">Olá *username* devem ser especificados como  *user@servername* .</span><span class="sxs-lookup"><span data-stu-id="4ab46-182">hello *username* must be specified as *user@servername*.</span></span>   

## <span data-ttu-id="4ab46-183"><a name="adf-tables"></a>Definir e criar tabelas toospecify como tooaccess Olá conjuntos de dados</span><span class="sxs-lookup"><span data-stu-id="4ab46-183"><a name="adf-tables"></a>Define and create tables toospecify how tooaccess hello datasets</span></span>
<span data-ttu-id="4ab46-184">Crie tabelas que especificam a estrutura hello, local e disponibilidade de conjuntos de dados de saudação com hello baseado no script os procedimentos a seguir.</span><span class="sxs-lookup"><span data-stu-id="4ab46-184">Create tables that specify hello structure, location, and availability of hello datasets with hello following script-based procedures.</span></span> <span data-ttu-id="4ab46-185">Arquivos JSON são usados toodefine Olá tabelas.</span><span class="sxs-lookup"><span data-stu-id="4ab46-185">JSON files are used toodefine hello tables.</span></span> <span data-ttu-id="4ab46-186">Para obter mais informações sobre a estrutura Olá desses arquivos, consulte [conjuntos de dados](../data-factory/data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="4ab46-186">For more information on hello structure of these files, see [Datasets](../data-factory/data-factory-create-datasets.md).</span></span>

> [!NOTE]
> <span data-ttu-id="4ab46-187">Olá deve ser executada `Add-AzureAccount` cmdlet antes de executar Olá [AzureDataFactoryTable novo](https://msdn.microsoft.com/library/azure/dn835096.aspx) tooconfirm cmdlet que Olá assinatura do Azure à direita é selecionado para execução do comando hello.</span><span class="sxs-lookup"><span data-stu-id="4ab46-187">You should execute hello `Add-AzureAccount` cmdlet before executing hello [New-AzureDataFactoryTable](https://msdn.microsoft.com/library/azure/dn835096.aspx) cmdlet tooconfirm that hello right Azure subscription is selected for hello command execution.</span></span> <span data-ttu-id="4ab46-188">Para obter a documentação desse cmdlet, consulte [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="4ab46-188">For documentation of this cmdlet, see [Add-AzureAccount](/powershell/module/azure/add-azureaccount?view=azuresmps-3.7.0).</span></span>
>
>

<span data-ttu-id="4ab46-189">definições de saudação JSON com base nas tabelas de saudação usam Olá nomes a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ab46-189">hello JSON-based definitions in hello tables use hello following names:</span></span>

* <span data-ttu-id="4ab46-190">Olá **nome de tabela** Olá local SQL server está *nyctaxi_data*</span><span class="sxs-lookup"><span data-stu-id="4ab46-190">hello **table name** in hello on-premises SQL server is *nyctaxi_data*</span></span>
* <span data-ttu-id="4ab46-191">Olá **nome do contêiner** Olá armazenamento de BLOBs do Azure conta é *containername*</span><span class="sxs-lookup"><span data-stu-id="4ab46-191">hello **container name** in hello Azure Blob Storage account is *containername*</span></span>  

<span data-ttu-id="4ab46-192">Três definições de tabela são necessárias para este pipeline do ADF:</span><span class="sxs-lookup"><span data-stu-id="4ab46-192">Three table definitions are needed for this ADF pipeline:</span></span>

1. [<span data-ttu-id="4ab46-193">Tabela do SQL local</span><span class="sxs-lookup"><span data-stu-id="4ab46-193">SQL on-premises Table</span></span>](#adf-table-onprem-sql)
2. [<span data-ttu-id="4ab46-194">Tabela de blob </span><span class="sxs-lookup"><span data-stu-id="4ab46-194">Blob Table </span></span>](#adf-table-blob-store)
3. [<span data-ttu-id="4ab46-195">Tabela do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="4ab46-195">SQL Azure Table</span></span>](#adf-table-azure-sql)

> [!NOTE]
> <span data-ttu-id="4ab46-196">Esses procedimentos usam o Azure PowerShell toodefine e criar hello atividades ADF.</span><span class="sxs-lookup"><span data-stu-id="4ab46-196">These procedures use Azure PowerShell toodefine and create hello ADF activities.</span></span> <span data-ttu-id="4ab46-197">Mas essas tarefas também podem ser realizadas usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab46-197">But these tasks can also be accomplished using hello Azure portal.</span></span> <span data-ttu-id="4ab46-198">Para obter detalhes, consulte [Criar conjuntos de dados](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span><span class="sxs-lookup"><span data-stu-id="4ab46-198">For details, see [Create datasets](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-datasets).</span></span>
>
>

### <span data-ttu-id="4ab46-199"><a name="adf-table-onprem-sql"></a>Tabela do SQL local</span><span class="sxs-lookup"><span data-stu-id="4ab46-199"><a name="adf-table-onprem-sql"></a>SQL on-premises Table</span></span>
<span data-ttu-id="4ab46-200">definição da tabela Olá para Olá local do SQL Server é especificado em Olá arquivo JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ab46-200">hello table definition for hello on-premises SQL Server is specified in hello following JSON file:</span></span>

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

<span data-ttu-id="4ab46-201">nomes de coluna de saudação não foram incluídos aqui.</span><span class="sxs-lookup"><span data-stu-id="4ab46-201">hello column names were not included here.</span></span> <span data-ttu-id="4ab46-202">Você pode selecionar em nomes de coluna Olá sub incluindo-os aqui (detalhes Verifique Olá [documentação ADF](../data-factory/data-factory-data-movement-activities.md) tópico.</span><span class="sxs-lookup"><span data-stu-id="4ab46-202">You can sub-select on hello column names by including them here (for details check hello [ADF documentation](../data-factory/data-factory-data-movement-activities.md) topic.</span></span>

<span data-ttu-id="4ab46-203">Copiar a definição de JSON de saudação da tabela de saudação em um arquivo chamado *onpremtabledef.json* de arquivo e salve-o tooa conhecido local (assumido aqui toobe *C:\temp\onpremtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="4ab46-203">Copy hello JSON definition of hello table into a file called *onpremtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\onpremtabledef.json*).</span></span> <span data-ttu-id="4ab46-204">Crie tabela de saudação no ADF com hello Azure PowerShell cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ab46-204">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp –File C:\temp\onpremtabledef.json


### <span data-ttu-id="4ab46-205"><a name="adf-table-blob-store"></a>Tabela de blob</span><span class="sxs-lookup"><span data-stu-id="4ab46-205"><a name="adf-table-blob-store"></a>Blob Table</span></span>
<span data-ttu-id="4ab46-206">A definição da tabela Olá para Olá saída local de blob está no seguinte hello (isso mapeia dados Olá incluído do blob de tooAzure local):</span><span class="sxs-lookup"><span data-stu-id="4ab46-206">Definition for hello table for hello output blob location is in hello following (this maps hello ingested data from on-premises tooAzure blob):</span></span>

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

<span data-ttu-id="4ab46-207">Copiar a definição de JSON de saudação da tabela de saudação em um arquivo chamado *bloboutputtabledef.json* de arquivo e salve-o tooa conhecido local (assumido aqui toobe *C:\temp\bloboutputtabledef.json*).</span><span class="sxs-lookup"><span data-stu-id="4ab46-207">Copy hello JSON definition of hello table into a file called *bloboutputtabledef.json* file and save it tooa known location (here assumed toobe *C:\temp\bloboutputtabledef.json*).</span></span> <span data-ttu-id="4ab46-208">Crie tabela de saudação no ADF com hello Azure PowerShell cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ab46-208">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\bloboutputtabledef.json  

### <span data-ttu-id="4ab46-209"><a name="adf-table-azure-sq"></a>Tabela do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="4ab46-209"><a name="adf-table-azure-sq"></a>SQL Azure Table</span></span>
<span data-ttu-id="4ab46-210">A definição da tabela de saudação de saudação que do SQL Azure de saída está no seguinte hello (esse esquema mapeia dados Olá provenientes de blob Olá):</span><span class="sxs-lookup"><span data-stu-id="4ab46-210">Definition for hello table for hello SQL Azure output is in hello following (this schema maps hello data coming from hello blob):</span></span>

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

<span data-ttu-id="4ab46-211">Copiar a definição de JSON de saudação da tabela de saudação em um arquivo chamado *AzureSqlTable.json* de arquivo e salve-o tooa conhecido local (assumido aqui toobe *C:\temp\AzureSqlTable.json*).</span><span class="sxs-lookup"><span data-stu-id="4ab46-211">Copy hello JSON definition of hello table into a file called *AzureSqlTable.json* file and save it tooa known location (here assumed toobe *C:\temp\AzureSqlTable.json*).</span></span> <span data-ttu-id="4ab46-212">Crie tabela de saudação no ADF com hello Azure PowerShell cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ab46-212">Create hello table in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryTable -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\AzureSqlTable.json  


## <span data-ttu-id="4ab46-213"><a name="adf-pipeline"></a>Definir e criar o pipeline de saudação</span><span class="sxs-lookup"><span data-stu-id="4ab46-213"><a name="adf-pipeline"></a>Define and create hello pipeline</span></span>
<span data-ttu-id="4ab46-214">Especifique atividades Olá que pertencem a toohello pipeline e criar o pipeline de saudação com hello baseado no script os procedimentos a seguir.</span><span class="sxs-lookup"><span data-stu-id="4ab46-214">Specify hello activities that belong toohello pipeline and create hello pipeline with hello following script-based procedures.</span></span> <span data-ttu-id="4ab46-215">Um arquivo JSON é usado toodefine Olá pipeline propriedades.</span><span class="sxs-lookup"><span data-stu-id="4ab46-215">A JSON file is used toodefine hello pipeline properties.</span></span>

* <span data-ttu-id="4ab46-216">script Hello supõe que Olá **nome do pipeline** é *AMLDSProcessPipeline*.</span><span class="sxs-lookup"><span data-stu-id="4ab46-216">hello script assumes that hello **pipeline name** is *AMLDSProcessPipeline*.</span></span>
* <span data-ttu-id="4ab46-217">Observe também que definimos periodicidade Olá de saudação pipeline toobe executado em diariamente base e use Olá tempo de execução padrão para o trabalho de saudação (12: 00 UTC).</span><span class="sxs-lookup"><span data-stu-id="4ab46-217">Also note that we set hello periodicity of hello pipeline toobe executed on daily basis and use hello default execution time for hello job (12 am UTC).</span></span>

> [!NOTE]
> <span data-ttu-id="4ab46-218">Hello procedimentos a seguir usam o Azure PowerShell toodefine e criar hello ADF pipeline.</span><span class="sxs-lookup"><span data-stu-id="4ab46-218">hello following procedures use Azure PowerShell toodefine and create hello ADF pipeline.</span></span> <span data-ttu-id="4ab46-219">Mas essa tarefa também pode ser realizada pelo Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4ab46-219">But this task can also be accomplished using the Azure portal.</span></span> <span data-ttu-id="4ab46-220">Para obter detalhes, consulte [Criar pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span><span class="sxs-lookup"><span data-stu-id="4ab46-220">For details, see [Create pipeline](../data-factory/data-factory-move-data-between-onprem-and-cloud.md#create-pipeline).</span></span>
>
>

<span data-ttu-id="4ab46-221">Usando definições de tabela Olá fornecidas anteriormente, definição pipeline Olá Olá que ADF é especificada da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4ab46-221">Using hello table definitions provided previously, hello pipeline definition for hello ADF is specified as follows:</span></span>

        {
            "name": "AMLDSProcessPipeline",
            "properties":
            {
                "description" : "This pipeline has one Copy activity that copies data from an on-premises SQL tooAzure blob",
                 "activities":
                [
                    {
                        "name": "CopyFromSQLtoBlob",
                        "description": "Copy data from on-premises SQL server tooblob",     
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
                        "description": "Push data tooSql Azure",        
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

<span data-ttu-id="4ab46-222">Copie esta definição de JSON de pipeline de saudação em um arquivo chamado *pipelinedef.json* de arquivo e salve-o tooa conhecido local (assumido aqui toobe *C:\temp\pipelinedef.json*).</span><span class="sxs-lookup"><span data-stu-id="4ab46-222">Copy this JSON definition of hello pipeline into a file called *pipelinedef.json* file and save it tooa known location (here assumed toobe *C:\temp\pipelinedef.json*).</span></span> <span data-ttu-id="4ab46-223">Crie o pipeline de Olá no ADF com hello Azure PowerShell cmdlet a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ab46-223">Create hello pipeline in ADF with hello following Azure PowerShell cmdlet:</span></span>

    New-AzureDataFactoryPipeline  -ResourceGroupName adfdsprg -DataFactoryName adfdsp -File C:\temp\pipelinedef.json

<span data-ttu-id="4ab46-224">Confirme que você pode ver pipeline Olá em Olá AAD no Portal clássico do Azure de saudação aparecem como a seguir (quando você clicar em um diagrama de saudação)</span><span class="sxs-lookup"><span data-stu-id="4ab46-224">Confirm that you can see hello pipeline on hello ADF in hello Azure Classic Portal show up as following (when you click hello diagram)</span></span>

![Pipeline do ADF](media/machine-learning-data-science-move-sql-azure-adf/DJP1kji.png)

## <span data-ttu-id="4ab46-226"><a name="adf-pipeline-start"></a>Iniciar Olá Pipeline</span><span class="sxs-lookup"><span data-stu-id="4ab46-226"><a name="adf-pipeline-start"></a>Start hello Pipeline</span></span>
<span data-ttu-id="4ab46-227">pipeline de saudação pode agora ser executada usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ab46-227">hello pipeline can now be run using hello following command:</span></span>

    Set-AzureDataFactoryPipelineActivePeriod -ResourceGroupName ADFdsprg -DataFactoryName ADFdsp -StartDateTime startdateZ –EndDateTime enddateZ –Name AMLDSProcessPipeline

<span data-ttu-id="4ab46-228">Olá *startdate* e *enddate* toobe substituído com datas reais de saudação entre os quais você deseja Olá pipeline toorun precisam de valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="4ab46-228">hello *startdate* and *enddate* parameter values need toobe replaced with hello actual dates between which you want hello pipeline toorun.</span></span>

<span data-ttu-id="4ab46-229">Depois que o pipeline de saudação é executada, deve ser capaz de toosee Olá dados aparecem no contêiner de saudação selecionado para blob hello, um arquivo por dia.</span><span class="sxs-lookup"><span data-stu-id="4ab46-229">Once hello pipeline executes, you should be able toosee hello data show up in hello container selected for hello blob, one file per day.</span></span>

<span data-ttu-id="4ab46-230">Observe que não utilizaram funcionalidade Olá fornecida pelos dados do ADF toopipe incrementalmente.</span><span class="sxs-lookup"><span data-stu-id="4ab46-230">Note that we have not leveraged hello functionality provided by ADF toopipe data incrementally.</span></span> <span data-ttu-id="4ab46-231">Para obter mais informações sobre como toodo este e outros recursos fornecidos pelo AAD, consulte Olá [documentação ADF](https://azure.microsoft.com/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="4ab46-231">For more information on how toodo this and other capabilities provided by ADF, see hello [ADF documentation](https://azure.microsoft.com/services/data-factory/).</span></span>
