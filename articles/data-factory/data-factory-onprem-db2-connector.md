---
title: dados de aaaMove do DB2 usando o Azure Data Factory | Microsoft Docs
description: "Saiba como toomove dados do DB2 local banco de dados usando a atividade de cópia de fábrica de dados do Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="21dc0-103">Mover dados do DB2 usando a Atividade de Cópia do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="21dc0-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="21dc0-104">Este artigo descreve como você pode usar a atividade de cópia em dados do Azure Data Factory toocopy de um repositório de dados do tooa de banco de dados do DB2 de local.</span><span class="sxs-lookup"><span data-stu-id="21dc0-104">This article describes how you can use Copy Activity in Azure Data Factory toocopy data from an on-premises DB2 database tooa data store.</span></span> <span data-ttu-id="21dc0-105">Você pode copiar o repositório de tooany de dados que está listado como um coletor com suporte no hello [as atividades de movimentação de dados do Data Factory](data-factory-data-movement-activities.md#supported-data-stores-and-formats) artigo.</span><span class="sxs-lookup"><span data-stu-id="21dc0-105">You can copy data tooany store that is listed as a supported sink in hello [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="21dc0-106">Este tópico se baseia no artigo de fábrica de dados hello, que apresenta uma visão geral de movimentação de dados usando a atividade de cópia e lista de combinações de repositório de dados Olá com suporte.</span><span class="sxs-lookup"><span data-stu-id="21dc0-106">This topic builds on hello Data Factory article, which presents an overview of data movement by using Copy Activity and lists hello supported data store combinations.</span></span> 

<span data-ttu-id="21dc0-107">Fábrica de dados atualmente oferece suporte à movimentação de dados somente de um tooa de banco de dados DB2 [repositório de dados com suporte do coletor](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="21dc0-107">Data Factory currently supports only moving data from a DB2 database tooa [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="21dc0-108">Movimentação de dados de outros dados armazena tooa não há suporte para o banco de dados do DB2.</span><span class="sxs-lookup"><span data-stu-id="21dc0-108">Moving data from other data stores tooa DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21dc0-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="21dc0-109">Prerequisites</span></span>
<span data-ttu-id="21dc0-110">Fábrica de dados oferece suporte a banco de dados DB2 local de conexão tooan usando Olá [gateway de gerenciamento de dados](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="21dc0-110">Data Factory supports connecting tooan on-premises DB2 database by using hello [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="21dc0-111">Para instruções passo a passo tooset os dados de gateway Olá pipeline toomove seus dados, consulte Olá [mover dados de local toocloud](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="21dc0-111">For step-by-step instructions tooset up hello gateway data pipeline toomove your data, see hello [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="21dc0-112">Mesmo se hello DB2 estiver hospedado no Azure IaaS VM, é necessário um gateway.</span><span class="sxs-lookup"><span data-stu-id="21dc0-112">A gateway is required even if hello DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="21dc0-113">Você pode instalar o gateway de Olá Olá mesmo IaaS VM como Olá repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="21dc0-113">You can install hello gateway on hello same IaaS VM as hello data store.</span></span> <span data-ttu-id="21dc0-114">Se o gateway Olá pode se conectar a banco de dados toohello, você pode instalar o gateway de saudação em uma máquina virtual diferente.</span><span class="sxs-lookup"><span data-stu-id="21dc0-114">If hello gateway can connect toohello database, you can install hello gateway on a different VM.</span></span>

<span data-ttu-id="21dc0-115">gateway de gerenciamento de dados Olá fornece um driver DB2 interno, portanto você não precisa toomanually instalar um toocopy de dados do driver do DB2.</span><span class="sxs-lookup"><span data-stu-id="21dc0-115">hello data management gateway provides a built-in DB2 driver, so you don't need toomanually install a driver toocopy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="21dc0-116">Para obter dicas sobre solução de problemas do gateway e conexão, consulte Olá [solucionar problemas do gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) artigo.</span><span class="sxs-lookup"><span data-stu-id="21dc0-116">For tips on troubleshooting connection and gateway issues, see hello [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="21dc0-117">Versões com suporte</span><span class="sxs-lookup"><span data-stu-id="21dc0-117">Supported versions</span></span>
<span data-ttu-id="21dc0-118">conector Olá DB2 da fábrica de dados oferece suporte a saudação plataformas IBM DB2 e versões com o Gerenciador de acesso ao banco de dados arquitetura DRDA (Distributed Relational) SQL versões 9, 10 e 11 a seguir:</span><span class="sxs-lookup"><span data-stu-id="21dc0-118">hello Data Factory DB2 connector supports hello following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="21dc0-119">IBM DB2 para z/OS versão 11.1</span><span class="sxs-lookup"><span data-stu-id="21dc0-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="21dc0-120">IBM DB2 para z/OS versão 10.1</span><span class="sxs-lookup"><span data-stu-id="21dc0-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="21dc0-121">IBM DB2 para i (AS400) versão 7.2</span><span class="sxs-lookup"><span data-stu-id="21dc0-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="21dc0-122">IBM DB2 para i (AS400) versão 7.1</span><span class="sxs-lookup"><span data-stu-id="21dc0-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="21dc0-123">IBM DB2 para LUW (Linux, UNIX e Windows) versão 11</span><span class="sxs-lookup"><span data-stu-id="21dc0-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="21dc0-124">IBM DB2 para LUW versão 10.5</span><span class="sxs-lookup"><span data-stu-id="21dc0-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="21dc0-125">IBM DB2 para LUW versão 10.1</span><span class="sxs-lookup"><span data-stu-id="21dc0-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="21dc0-126">Se você receber a mensagem de erro hello "hello pacote correspondente tooan SQL instrução solicitação de execução não foi encontrada.</span><span class="sxs-lookup"><span data-stu-id="21dc0-126">If you receive hello error message "hello package corresponding tooan SQL statement execution request was not found.</span></span> <span data-ttu-id="21dc0-127">SQLSTATE = 51002 SQLCODE =-805, "motivo Olá é um pacote necessário não foi criado para o usuário normal Olá Olá SO.</span><span class="sxs-lookup"><span data-stu-id="21dc0-127">SQLSTATE=51002 SQLCODE=-805," hello reason is a necessary package is not created for hello normal user on hello OS.</span></span> <span data-ttu-id="21dc0-128">tooresolve esse problema, siga estas instruções para seu tipo de servidor DB2:</span><span class="sxs-lookup"><span data-stu-id="21dc0-128">tooresolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="21dc0-129">DB2 para i (AS400): permitem que um usuário avançado Criar coleção de saudação de usuário normal Olá antes de executar a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="21dc0-129">DB2 for i (AS400): Let a power user create hello collection for hello normal user before running Copy Activity.</span></span> <span data-ttu-id="21dc0-130">coleção de saudação toocreate, use Olá comando:`create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="21dc0-130">toocreate hello collection, use hello command: `create collection <username>`</span></span>
> - <span data-ttu-id="21dc0-131">O DB2 for z/OS ou LUW: Use uma conta de privilégios altos – um usuário avançado ou administrador que tem autoridades de pacote e de associação, BINDADD, CONCEDER permissões de tooPUBLIC de executar – cópia de saudação toorun uma vez.</span><span class="sxs-lookup"><span data-stu-id="21dc0-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE tooPUBLIC permissions--toorun hello copy once.</span></span> <span data-ttu-id="21dc0-132">pacote necessário Olá é criado automaticamente durante a cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="21dc0-132">hello necessary package is automatically created during hello copy.</span></span> <span data-ttu-id="21dc0-133">Posteriormente, você pode alternar usuário normal toohello voltar para a execução de cópia subsequentes.</span><span class="sxs-lookup"><span data-stu-id="21dc0-133">Afterward, you can switch back toohello normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="21dc0-134">Introdução</span><span class="sxs-lookup"><span data-stu-id="21dc0-134">Getting started</span></span>
<span data-ttu-id="21dc0-135">Você pode criar um pipeline com uma cópia de dados de toomove de atividade de um repositório de dados DB2 local usando diversas ferramentas e APIs:</span><span class="sxs-lookup"><span data-stu-id="21dc0-135">You can create a pipeline with a copy activity toomove data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="21dc0-136">toocreate de maneira mais fácil de saudação um pipeline é toouse Olá Assistente para cópia de fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="21dc0-136">hello easiest way toocreate a pipeline is toouse hello Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="21dc0-137">Para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de saudação, consulte Olá [Tutorial: criar um pipeline usando o Assistente para cópia de saudação](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="21dc0-137">For a quick walkthrough on creating a pipeline by using hello Copy Wizard, see hello [Tutorial: Create a pipeline by using hello Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="21dc0-138">Você também pode usar ferramentas toocreate um pipeline, incluindo Olá portal do Azure, Visual Studio, do PowerShell do Azure, um Gerenciador de recursos do Azure modelo, Olá API .NET e Olá API REST.</span><span class="sxs-lookup"><span data-stu-id="21dc0-138">You can also use tools toocreate a pipeline, including hello Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, hello .NET API, and hello REST API.</span></span> <span data-ttu-id="21dc0-139">Para obter instruções passo a passo toocreate um pipeline com uma atividade de cópia, consulte Olá [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="21dc0-139">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="21dc0-140">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="21dc0-140">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="21dc0-141">Crie a fábrica de dados tooyour do repositórios de dados de entrada e saída de toolink serviços vinculados.</span><span class="sxs-lookup"><span data-stu-id="21dc0-141">Create linked services toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="21dc0-142">Criar conjuntos de dados toorepresent entrada e saída de dados para a operação de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="21dc0-142">Create datasets toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="21dc0-143">Criar um pipeline com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="21dc0-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="21dc0-144">Quando você usa Olá Assistente para cópia, definições de JSON para serviços de fábrica de dados vinculado hello, conjuntos de dados e entidades de pipeline são criados automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="21dc0-144">When you use hello Copy Wizard, JSON definitions for hello Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="21dc0-145">Quando você usar ferramentas ou APIs (exceto Olá API .NET), você define entidades da fábrica de dados de saudação usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="21dc0-145">When you use tools or APIs (except hello .NET API), you define hello Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="21dc0-146">Olá [exemplo JSON: copiar dados do DB2 tooAzure armazenamento de Blob](#json-example-copy-data-from-db2-to-azure-blob) mostra definições de JSON Olá para Olá entidades da fábrica de dados que são usados toocopy dados de um repositório de dados DB2 local.</span><span class="sxs-lookup"><span data-stu-id="21dc0-146">hello [JSON example: Copy data from DB2 tooAzure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows hello JSON definitions for hello Data Factory entities that are used toocopy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="21dc0-147">Olá seções a seguir fornece detalhes sobre Olá propriedades JSON que são usadas toodefine Olá fábrica de dados entidades específico tooa DB2 repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="21dc0-147">hello following sections provide details about hello JSON properties that are used toodefine hello Data Factory entities that are specific tooa DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="21dc0-148">Propriedades do serviço vinculado do DB2</span><span class="sxs-lookup"><span data-stu-id="21dc0-148">DB2 linked service properties</span></span>
<span data-ttu-id="21dc0-149">Olá, a tabela a seguir lista propriedades JSON de saudação tooa específico do serviço vinculado do DB2.</span><span class="sxs-lookup"><span data-stu-id="21dc0-149">hello following table lists hello JSON properties that are specific tooa DB2 linked service.</span></span>

| <span data-ttu-id="21dc0-150">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21dc0-150">Property</span></span> | <span data-ttu-id="21dc0-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="21dc0-151">Description</span></span> | <span data-ttu-id="21dc0-152">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="21dc0-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21dc0-153">**tipo**</span><span class="sxs-lookup"><span data-stu-id="21dc0-153">**type**</span></span> |<span data-ttu-id="21dc0-154">Essa propriedade deve ser definida muito**OnPremisesDB2**.</span><span class="sxs-lookup"><span data-stu-id="21dc0-154">This property must be set too**OnPremisesDB2**.</span></span> |<span data-ttu-id="21dc0-155">Sim</span><span class="sxs-lookup"><span data-stu-id="21dc0-155">Yes</span></span> |
| <span data-ttu-id="21dc0-156">**server**</span><span class="sxs-lookup"><span data-stu-id="21dc0-156">**server**</span></span> |<span data-ttu-id="21dc0-157">nome de saudação do servidor de saudação DB2.</span><span class="sxs-lookup"><span data-stu-id="21dc0-157">hello name of hello DB2 server.</span></span> |<span data-ttu-id="21dc0-158">Sim</span><span class="sxs-lookup"><span data-stu-id="21dc0-158">Yes</span></span> |
| <span data-ttu-id="21dc0-159">**database**</span><span class="sxs-lookup"><span data-stu-id="21dc0-159">**database**</span></span> |<span data-ttu-id="21dc0-160">nome de saudação do banco de dados de saudação DB2.</span><span class="sxs-lookup"><span data-stu-id="21dc0-160">hello name of hello DB2 database.</span></span> |<span data-ttu-id="21dc0-161">Sim</span><span class="sxs-lookup"><span data-stu-id="21dc0-161">Yes</span></span> |
| <span data-ttu-id="21dc0-162">**schema**</span><span class="sxs-lookup"><span data-stu-id="21dc0-162">**schema**</span></span> |<span data-ttu-id="21dc0-163">nome de saudação do esquema de saudação no banco de dados do DB2 de saudação.</span><span class="sxs-lookup"><span data-stu-id="21dc0-163">hello name of hello schema in hello DB2 database.</span></span> <span data-ttu-id="21dc0-164">Essa propriedade diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="21dc0-164">This property is case-sensitive.</span></span> |<span data-ttu-id="21dc0-165">Não</span><span class="sxs-lookup"><span data-stu-id="21dc0-165">No</span></span> |
| <span data-ttu-id="21dc0-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="21dc0-166">**authenticationType**</span></span> |<span data-ttu-id="21dc0-167">tipo de saudação de autenticação que é o banco de dados usado tooconnect toohello DB2.</span><span class="sxs-lookup"><span data-stu-id="21dc0-167">hello type of authentication that is used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="21dc0-168">Olá os valores possíveis são: anônima, básica e do Windows.</span><span class="sxs-lookup"><span data-stu-id="21dc0-168">hello possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="21dc0-169">Sim</span><span class="sxs-lookup"><span data-stu-id="21dc0-169">Yes</span></span> |
| <span data-ttu-id="21dc0-170">**username**</span><span class="sxs-lookup"><span data-stu-id="21dc0-170">**username**</span></span> |<span data-ttu-id="21dc0-171">Olá nome hello conta de usuário se você usar a autenticação básica ou do Windows.</span><span class="sxs-lookup"><span data-stu-id="21dc0-171">hello name for hello user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="21dc0-172">Não</span><span class="sxs-lookup"><span data-stu-id="21dc0-172">No</span></span> |
| <span data-ttu-id="21dc0-173">**password**</span><span class="sxs-lookup"><span data-stu-id="21dc0-173">**password**</span></span> |<span data-ttu-id="21dc0-174">Olá senha Olá conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="21dc0-174">hello password for hello user account.</span></span> |<span data-ttu-id="21dc0-175">Não</span><span class="sxs-lookup"><span data-stu-id="21dc0-175">No</span></span> |
| <span data-ttu-id="21dc0-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="21dc0-176">**gatewayName**</span></span> |<span data-ttu-id="21dc0-177">nome de saudação de gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello local DB2.</span><span class="sxs-lookup"><span data-stu-id="21dc0-177">hello name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="21dc0-178">Sim</span><span class="sxs-lookup"><span data-stu-id="21dc0-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="21dc0-179">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="21dc0-179">Dataset properties</span></span>
<span data-ttu-id="21dc0-180">Para obter uma lista de seções de saudação e propriedades que estão disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="21dc0-180">For a list of hello sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="21dc0-181">Seções, como **estrutura**, **disponibilidade**e hello **política** um conjunto de dados JSON, são semelhantes para todos os tipos de conjunto de dados (SQL Azure, armazenamento de BLOBs do Azure, tabela do Azure armazenamento e assim por diante).</span><span class="sxs-lookup"><span data-stu-id="21dc0-181">Sections, such as **structure**, **availability**, and hello **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="21dc0-182">Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="21dc0-182">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="21dc0-183">Olá **typeProperties** seção um conjunto de dados do tipo **RelationalTable**, que inclui o conjunto de dados Olá DB2, tem Olá propriedade a seguir:</span><span class="sxs-lookup"><span data-stu-id="21dc0-183">hello **typeProperties** section for a dataset of type **RelationalTable**, which includes hello DB2 dataset, has hello following property:</span></span>

| <span data-ttu-id="21dc0-184">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21dc0-184">Property</span></span> | <span data-ttu-id="21dc0-185">Descrição</span><span class="sxs-lookup"><span data-stu-id="21dc0-185">Description</span></span> | <span data-ttu-id="21dc0-186">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="21dc0-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="21dc0-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="21dc0-187">**tableName**</span></span> |<span data-ttu-id="21dc0-188">Olá nome da tabela de saudação na instância de banco de dados de saudação DB2 que Olá serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="21dc0-188">hello name of hello table in hello DB2 database instance that hello linked service refers to.</span></span> <span data-ttu-id="21dc0-189">Essa propriedade diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="21dc0-189">This property is case-sensitive.</span></span> |<span data-ttu-id="21dc0-190">Não (se hello **consulta** propriedade de uma atividade de cópia do tipo **RelationalSource** for especificado)</span><span class="sxs-lookup"><span data-stu-id="21dc0-190">No (if hello **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="21dc0-191">Propriedades da Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="21dc0-191">Copy Activity properties</span></span>
<span data-ttu-id="21dc0-192">Para obter uma lista de seções de saudação e propriedades que estão disponíveis para a definição de atividades de cópia, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="21dc0-192">For a list of hello sections and properties that are available for defining copy activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="21dc0-193">As propriedades da Atividade de Cópia, como **name**, **description**, tabela **inputs**, tabela **outputs** e **policy** estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="21dc0-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="21dc0-194">Olá propriedades que estão disponíveis no hello **typeProperties** seção de atividade Olá para cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="21dc0-194">hello properties that are available in hello **typeProperties** section of hello activity for each activity type.</span></span> <span data-ttu-id="21dc0-195">Para a atividade de cópia, propriedades de saudação variam dependendo Olá tipos de fontes de dados e coletores.</span><span class="sxs-lookup"><span data-stu-id="21dc0-195">For Copy Activity, hello properties vary depending on hello types of data sources and sinks.</span></span>

<span data-ttu-id="21dc0-196">Para a atividade de cópia, quando a fonte de saudação é do tipo **RelationalSource** (que inclui DB2), Olá propriedades a seguir está disponível no hello **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="21dc0-196">For Copy Activity, when hello source is of type **RelationalSource** (which includes DB2), hello following properties are available in hello **typeProperties** section:</span></span>

| <span data-ttu-id="21dc0-197">Propriedade</span><span class="sxs-lookup"><span data-stu-id="21dc0-197">Property</span></span> | <span data-ttu-id="21dc0-198">Descrição</span><span class="sxs-lookup"><span data-stu-id="21dc0-198">Description</span></span> | <span data-ttu-id="21dc0-199">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="21dc0-199">Allowed values</span></span> | <span data-ttu-id="21dc0-200">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="21dc0-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="21dc0-201">**query**</span><span class="sxs-lookup"><span data-stu-id="21dc0-201">**query**</span></span> |<span data-ttu-id="21dc0-202">Use Olá consulta personalizada tooread Olá dados.</span><span class="sxs-lookup"><span data-stu-id="21dc0-202">Use hello custom query tooread hello data.</span></span> |<span data-ttu-id="21dc0-203">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="21dc0-203">SQL query string.</span></span> <span data-ttu-id="21dc0-204">Por exemplo: `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="21dc0-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="21dc0-205">Não (se hello **tableName** propriedade de um conjunto de dados for especificada)</span><span class="sxs-lookup"><span data-stu-id="21dc0-205">No (if hello **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="21dc0-206">Os nomes de esquema e tabela diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="21dc0-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="21dc0-207">Na instrução de consulta hello, colocar os nomes de propriedade usando "" (aspas duplas).</span><span class="sxs-lookup"><span data-stu-id="21dc0-207">In hello query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="21dc0-208">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="21dc0-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a><span data-ttu-id="21dc0-209">Exemplo JSON: copiar dados do DB2 tooAzure armazenamento de Blob</span><span class="sxs-lookup"><span data-stu-id="21dc0-209">JSON example: Copy data from DB2 tooAzure Blob storage</span></span>
<span data-ttu-id="21dc0-210">Este exemplo fornece definições de JSON de exemplo que você pode usar toocreate um pipeline usando Olá [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="21dc0-210">This example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="21dc0-211">exemplo Hello mostra como banco de dados toocopy um DB2 dados tooBlob armazenamento.</span><span class="sxs-lookup"><span data-stu-id="21dc0-211">hello example shows you how toocopy data from a DB2 database tooBlob storage.</span></span> <span data-ttu-id="21dc0-212">No entanto, os dados podem ser copiados muito[tipo de coletor de armazenar os dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a atividade de cópia de fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="21dc0-212">However, data can be copied too[any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="21dc0-213">exemplo Hello tem Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="21dc0-213">hello sample has hello following Data Factory entities:</span></span>

- <span data-ttu-id="21dc0-214">Um serviço vinculado do DB2 do tipo [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="21dc0-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="21dc0-215">Um serviço vinculado de armazenamento de Blobs do Azure do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="21dc0-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="21dc0-216">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="21dc0-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="21dc0-217">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="21dc0-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="21dc0-218">Um [pipeline](data-factory-create-pipelines.md) com uma atividade de cópia que usa Olá [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) propriedades</span><span class="sxs-lookup"><span data-stu-id="21dc0-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="21dc0-219">exemplo Hello copia dados de um resultado de consulta em um banco de dados de DB2 tooan BLOBs do Azure por hora.</span><span class="sxs-lookup"><span data-stu-id="21dc0-219">hello sample copies data from a query result in a DB2 database tooan Azure blob hourly.</span></span> <span data-ttu-id="21dc0-220">propriedades JSON Olá que são usadas no exemplo hello são descritas nas seções Olá seguir definições de entidade hello.</span><span class="sxs-lookup"><span data-stu-id="21dc0-220">hello JSON properties that are used in hello sample are described in hello sections that follow hello entity definitions.</span></span>

<span data-ttu-id="21dc0-221">Primeiramente, instale e configure um gateway de dados.</span><span class="sxs-lookup"><span data-stu-id="21dc0-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="21dc0-222">Olá as instruções são [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="21dc0-222">Instructions are in hello [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="21dc0-223">**Serviço vinculado do DB2**</span><span class="sxs-lookup"><span data-stu-id="21dc0-223">**DB2 linked service**</span></span>

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="21dc0-224">**Serviço vinculado do armazenamento de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="21dc0-224">**Azure Blob storage linked service**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="21dc0-225">**Conjunto de dados de entrada do DB2**</span><span class="sxs-lookup"><span data-stu-id="21dc0-225">**DB2 input dataset**</span></span>

<span data-ttu-id="21dc0-226">exemplo Hello pressupõe que você criou uma tabela denominada "MyTable" que tem uma coluna chamada "timestamp" dos dados de série de tempo de saudação do DB2.</span><span class="sxs-lookup"><span data-stu-id="21dc0-226">hello sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for hello time series data.</span></span>

<span data-ttu-id="21dc0-227">Olá **externo** propriedade for definida muito "true".</span><span class="sxs-lookup"><span data-stu-id="21dc0-227">hello **external** property is set too"true."</span></span> <span data-ttu-id="21dc0-228">Essa configuração informa o serviço de fábrica de dados de saudação que este conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="21dc0-228">This setting informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="21dc0-229">Observe que Olá **tipo** propriedade for definida muito**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="21dc0-229">Notice that hello **type** property is set too**RelationalTable**.</span></span>


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="21dc0-230">**Conjunto de dados de saída de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="21dc0-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="21dc0-231">Os dados são gravados tooa novo blob a cada hora por configuração Olá **frequência** propriedade muito "Hora" e hello **intervalo** too1 de propriedade.</span><span class="sxs-lookup"><span data-stu-id="21dc0-231">Data is written tooa new blob every hour by setting hello **frequency** property too"Hour" and hello **interval** property too1.</span></span> <span data-ttu-id="21dc0-232">Olá **folderPath** propriedade para o blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="21dc0-232">hello **folderPath** property for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="21dc0-233">caminho da pasta Olá usa partes de ano, mês, dia e hora Olá Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="21dc0-233">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="21dc0-234">**Pipeline de atividade de cópia de saudação**</span><span class="sxs-lookup"><span data-stu-id="21dc0-234">**Pipeline for hello copy activity**</span></span>

<span data-ttu-id="21dc0-235">pipeline de saudação contém uma atividade de cópia que está configurada toouse especificado conjuntos de dados de entrada e saídos e que é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="21dc0-235">hello pipeline contains a copy activity that is configured toouse specified input and output datasets and which is scheduled toorun every hour.</span></span> <span data-ttu-id="21dc0-236">Na definição JSON para o pipeline de saudação do hello, Olá **fonte** tipo está definido muito**RelationalSource** e hello **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="21dc0-236">In hello JSON definition for hello pipeline, hello **source** type is set too**RelationalSource** and hello **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="21dc0-237">consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá "Orders" tabela.</span><span class="sxs-lookup"><span data-stu-id="21dc0-237">hello SQL query specified for hello **query** property selects hello data from hello "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a><span data-ttu-id="21dc0-238">Mapeamento de tipo para DB2</span><span class="sxs-lookup"><span data-stu-id="21dc0-238">Type mapping for DB2</span></span>
<span data-ttu-id="21dc0-239">Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, atividade de cópia executa conversões de tipo automática de tipo de toosink de tipo de fonte usando Olá abordagem em duas etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="21dc0-239">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type toosink type by using hello following two-step approach:</span></span>

1. <span data-ttu-id="21dc0-240">Converter de um tipo de .NET native fonte tipo tooa</span><span class="sxs-lookup"><span data-stu-id="21dc0-240">Convert from a native source type tooa .NET type</span></span>
2. <span data-ttu-id="21dc0-241">Converter de um tipo de coletor nativo de tooa de tipo .NET</span><span class="sxs-lookup"><span data-stu-id="21dc0-241">Convert from a .NET type tooa native sink type</span></span>

<span data-ttu-id="21dc0-242">mapeamentos de seguir Hello são usados quando copiar atividade converte dados de saudação de um tipo de .NET do DB2 tipo tooa:</span><span class="sxs-lookup"><span data-stu-id="21dc0-242">hello following mappings are used when Copy Activity converts hello data from a DB2 type tooa .NET type:</span></span>

| <span data-ttu-id="21dc0-243">Tipo do banco de dados DB2</span><span class="sxs-lookup"><span data-stu-id="21dc0-243">DB2 database type</span></span> | <span data-ttu-id="21dc0-244">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="21dc0-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="21dc0-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="21dc0-245">SmallInt</span></span> |<span data-ttu-id="21dc0-246">Int16</span><span class="sxs-lookup"><span data-stu-id="21dc0-246">Int16</span></span> |
| <span data-ttu-id="21dc0-247">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="21dc0-247">Integer</span></span> |<span data-ttu-id="21dc0-248">Int32</span><span class="sxs-lookup"><span data-stu-id="21dc0-248">Int32</span></span> |
| <span data-ttu-id="21dc0-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="21dc0-249">BigInt</span></span> |<span data-ttu-id="21dc0-250">Int64</span><span class="sxs-lookup"><span data-stu-id="21dc0-250">Int64</span></span> |
| <span data-ttu-id="21dc0-251">Real</span><span class="sxs-lookup"><span data-stu-id="21dc0-251">Real</span></span> |<span data-ttu-id="21dc0-252">Single</span><span class="sxs-lookup"><span data-stu-id="21dc0-252">Single</span></span> |
| <span data-ttu-id="21dc0-253">Duplo</span><span class="sxs-lookup"><span data-stu-id="21dc0-253">Double</span></span> |<span data-ttu-id="21dc0-254">Duplo</span><span class="sxs-lookup"><span data-stu-id="21dc0-254">Double</span></span> |
| <span data-ttu-id="21dc0-255">Float</span><span class="sxs-lookup"><span data-stu-id="21dc0-255">Float</span></span> |<span data-ttu-id="21dc0-256">Duplo</span><span class="sxs-lookup"><span data-stu-id="21dc0-256">Double</span></span> |
| <span data-ttu-id="21dc0-257">Decimal</span><span class="sxs-lookup"><span data-stu-id="21dc0-257">Decimal</span></span> |<span data-ttu-id="21dc0-258">Decimal</span><span class="sxs-lookup"><span data-stu-id="21dc0-258">Decimal</span></span> |
| <span data-ttu-id="21dc0-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="21dc0-259">DecimalFloat</span></span> |<span data-ttu-id="21dc0-260">Decimal</span><span class="sxs-lookup"><span data-stu-id="21dc0-260">Decimal</span></span> |
| <span data-ttu-id="21dc0-261">Numérico</span><span class="sxs-lookup"><span data-stu-id="21dc0-261">Numeric</span></span> |<span data-ttu-id="21dc0-262">Decimal</span><span class="sxs-lookup"><span data-stu-id="21dc0-262">Decimal</span></span> |
| <span data-ttu-id="21dc0-263">Data</span><span class="sxs-lookup"><span data-stu-id="21dc0-263">Date</span></span> |<span data-ttu-id="21dc0-264">DateTime</span><span class="sxs-lookup"><span data-stu-id="21dc0-264">DateTime</span></span> |
| <span data-ttu-id="21dc0-265">Hora</span><span class="sxs-lookup"><span data-stu-id="21dc0-265">Time</span></span> |<span data-ttu-id="21dc0-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="21dc0-266">TimeSpan</span></span> |
| <span data-ttu-id="21dc0-267">Timestamp</span><span class="sxs-lookup"><span data-stu-id="21dc0-267">Timestamp</span></span> |<span data-ttu-id="21dc0-268">Datetime</span><span class="sxs-lookup"><span data-stu-id="21dc0-268">DateTime</span></span> |
| <span data-ttu-id="21dc0-269">xml</span><span class="sxs-lookup"><span data-stu-id="21dc0-269">Xml</span></span> |<span data-ttu-id="21dc0-270">Byte[]</span><span class="sxs-lookup"><span data-stu-id="21dc0-270">Byte[]</span></span> |
| <span data-ttu-id="21dc0-271">Char</span><span class="sxs-lookup"><span data-stu-id="21dc0-271">Char</span></span> |<span data-ttu-id="21dc0-272">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="21dc0-272">String</span></span> |
| <span data-ttu-id="21dc0-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="21dc0-273">VarChar</span></span> |<span data-ttu-id="21dc0-274">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="21dc0-274">String</span></span> |
| <span data-ttu-id="21dc0-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="21dc0-275">LongVarChar</span></span> |<span data-ttu-id="21dc0-276">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="21dc0-276">String</span></span> |
| <span data-ttu-id="21dc0-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="21dc0-277">DB2DynArray</span></span> |<span data-ttu-id="21dc0-278">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="21dc0-278">String</span></span> |
| <span data-ttu-id="21dc0-279">Binário</span><span class="sxs-lookup"><span data-stu-id="21dc0-279">Binary</span></span> |<span data-ttu-id="21dc0-280">Byte[]</span><span class="sxs-lookup"><span data-stu-id="21dc0-280">Byte[]</span></span> |
| <span data-ttu-id="21dc0-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="21dc0-281">VarBinary</span></span> |<span data-ttu-id="21dc0-282">Byte[]</span><span class="sxs-lookup"><span data-stu-id="21dc0-282">Byte[]</span></span> |
| <span data-ttu-id="21dc0-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="21dc0-283">LongVarBinary</span></span> |<span data-ttu-id="21dc0-284">Byte[]</span><span class="sxs-lookup"><span data-stu-id="21dc0-284">Byte[]</span></span> |
| <span data-ttu-id="21dc0-285">Graphic</span><span class="sxs-lookup"><span data-stu-id="21dc0-285">Graphic</span></span> |<span data-ttu-id="21dc0-286">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="21dc0-286">String</span></span> |
| <span data-ttu-id="21dc0-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="21dc0-287">VarGraphic</span></span> |<span data-ttu-id="21dc0-288">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="21dc0-288">String</span></span> |
| <span data-ttu-id="21dc0-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="21dc0-289">LongVarGraphic</span></span> |<span data-ttu-id="21dc0-290">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="21dc0-290">String</span></span> |
| <span data-ttu-id="21dc0-291">Clob</span><span class="sxs-lookup"><span data-stu-id="21dc0-291">Clob</span></span> |<span data-ttu-id="21dc0-292">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="21dc0-292">String</span></span> |
| <span data-ttu-id="21dc0-293">Blob</span><span class="sxs-lookup"><span data-stu-id="21dc0-293">Blob</span></span> |<span data-ttu-id="21dc0-294">Byte[]</span><span class="sxs-lookup"><span data-stu-id="21dc0-294">Byte[]</span></span> |
| <span data-ttu-id="21dc0-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="21dc0-295">DbClob</span></span> |<span data-ttu-id="21dc0-296">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="21dc0-296">String</span></span> |
| <span data-ttu-id="21dc0-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="21dc0-297">SmallInt</span></span> |<span data-ttu-id="21dc0-298">Int16</span><span class="sxs-lookup"><span data-stu-id="21dc0-298">Int16</span></span> |
| <span data-ttu-id="21dc0-299">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="21dc0-299">Integer</span></span> |<span data-ttu-id="21dc0-300">Int32</span><span class="sxs-lookup"><span data-stu-id="21dc0-300">Int32</span></span> |
| <span data-ttu-id="21dc0-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="21dc0-301">BigInt</span></span> |<span data-ttu-id="21dc0-302">Int64</span><span class="sxs-lookup"><span data-stu-id="21dc0-302">Int64</span></span> |
| <span data-ttu-id="21dc0-303">Real</span><span class="sxs-lookup"><span data-stu-id="21dc0-303">Real</span></span> |<span data-ttu-id="21dc0-304">Single</span><span class="sxs-lookup"><span data-stu-id="21dc0-304">Single</span></span> |
| <span data-ttu-id="21dc0-305">Duplo</span><span class="sxs-lookup"><span data-stu-id="21dc0-305">Double</span></span> |<span data-ttu-id="21dc0-306">Duplo</span><span class="sxs-lookup"><span data-stu-id="21dc0-306">Double</span></span> |
| <span data-ttu-id="21dc0-307">Float</span><span class="sxs-lookup"><span data-stu-id="21dc0-307">Float</span></span> |<span data-ttu-id="21dc0-308">Duplo</span><span class="sxs-lookup"><span data-stu-id="21dc0-308">Double</span></span> |
| <span data-ttu-id="21dc0-309">Decimal</span><span class="sxs-lookup"><span data-stu-id="21dc0-309">Decimal</span></span> |<span data-ttu-id="21dc0-310">Decimal</span><span class="sxs-lookup"><span data-stu-id="21dc0-310">Decimal</span></span> |
| <span data-ttu-id="21dc0-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="21dc0-311">DecimalFloat</span></span> |<span data-ttu-id="21dc0-312">Decimal</span><span class="sxs-lookup"><span data-stu-id="21dc0-312">Decimal</span></span> |
| <span data-ttu-id="21dc0-313">Numérico</span><span class="sxs-lookup"><span data-stu-id="21dc0-313">Numeric</span></span> |<span data-ttu-id="21dc0-314">Decimal</span><span class="sxs-lookup"><span data-stu-id="21dc0-314">Decimal</span></span> |
| <span data-ttu-id="21dc0-315">Data</span><span class="sxs-lookup"><span data-stu-id="21dc0-315">Date</span></span> |<span data-ttu-id="21dc0-316">DateTime</span><span class="sxs-lookup"><span data-stu-id="21dc0-316">DateTime</span></span> |
| <span data-ttu-id="21dc0-317">Hora</span><span class="sxs-lookup"><span data-stu-id="21dc0-317">Time</span></span> |<span data-ttu-id="21dc0-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="21dc0-318">TimeSpan</span></span> |
| <span data-ttu-id="21dc0-319">Timestamp</span><span class="sxs-lookup"><span data-stu-id="21dc0-319">Timestamp</span></span> |<span data-ttu-id="21dc0-320">Datetime</span><span class="sxs-lookup"><span data-stu-id="21dc0-320">DateTime</span></span> |
| <span data-ttu-id="21dc0-321">xml</span><span class="sxs-lookup"><span data-stu-id="21dc0-321">Xml</span></span> |<span data-ttu-id="21dc0-322">Byte[]</span><span class="sxs-lookup"><span data-stu-id="21dc0-322">Byte[]</span></span> |
| <span data-ttu-id="21dc0-323">Char</span><span class="sxs-lookup"><span data-stu-id="21dc0-323">Char</span></span> |<span data-ttu-id="21dc0-324">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="21dc0-324">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="21dc0-325">Mapear colunas de toosink de origem</span><span class="sxs-lookup"><span data-stu-id="21dc0-325">Map source toosink columns</span></span>
<span data-ttu-id="21dc0-326">toolearn como colunas toomap Olá toocolumns de conjunto de dados de origem no conjunto de dados de coletor Olá, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="21dc0-326">toolearn how toomap columns in hello source dataset toocolumns in hello sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="21dc0-327">Leituras repetidas de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="21dc0-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="21dc0-328">Quando você copiar dados de um repositório de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="21dc0-328">When you copy data from a relational data store, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="21dc0-329">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="21dc0-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="21dc0-330">Você também pode configurar a repetição de saudação **política** propriedade para um conjunto de dados de toorerun uma fatia quando ocorre uma falha.</span><span class="sxs-lookup"><span data-stu-id="21dc0-330">You can also configure hello retry **policy** property for a dataset toorerun a slice when a failure occurs.</span></span> <span data-ttu-id="21dc0-331">Certifique-se de que Olá tais dados são lidos não importa como fatia de saudação muitas vezes é independentemente de como você executar novamente a fatia hello e execute novamente.</span><span class="sxs-lookup"><span data-stu-id="21dc0-331">Make sure that hello same data is read no matter how many times hello slice is rerun, and regardless of how you rerun hello slice.</span></span> <span data-ttu-id="21dc0-332">Para saber mais, confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="21dc0-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="21dc0-333">Desempenho e ajuste</span><span class="sxs-lookup"><span data-stu-id="21dc0-333">Performance and tuning</span></span>
<span data-ttu-id="21dc0-334">Saiba mais sobre os principais fatores que afetam o desempenho de saudação do desempenho de toooptimize de atividade de cópia e maneiras de saudação [Copiar atividade guia de desempenho e ajuste](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="21dc0-334">Learn about key factors that affect hello performance of Copy Activity and ways toooptimize performance in hello [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
