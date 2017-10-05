---
title: Mover dados do DB2 usando o Azure Data Factory | Microsoft Docs
description: "Saiba mais sobre como mover dados de um banco de dados DB2 local usando a Atividade de Cópia do Azure Data Factory"
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
ms.openlocfilehash: 6a89cc44724dbb5b46a9e89d6da24d9b35ddbbef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="8efab-103">Mover dados do DB2 usando a Atividade de Cópia do Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8efab-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="8efab-104">Este artigo descreve como você pode usar a Atividade de Cópia no Azure Data Factory para copiar dados de um banco de dados DB2 local para um armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="8efab-104">This article describes how you can use Copy Activity in Azure Data Factory to copy data from an on-premises DB2 database to a data store.</span></span> <span data-ttu-id="8efab-105">Você pode copiar dados em qualquer armazenamento listado como um coletor suportado no artigo [Atividades de movimentação de dados no Data Factory](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="8efab-105">You can copy data to any store that is listed as a supported sink in the [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="8efab-106">Este tópico foi criado com base no artigo do Data Factory, que apresenta uma visão geral da movimentação de dados usando a Atividade de Cópia e lista as combinações de armazenamento de dados suportadas.</span><span class="sxs-lookup"><span data-stu-id="8efab-106">This topic builds on the Data Factory article, which presents an overview of data movement by using Copy Activity and lists the supported data store combinations.</span></span> 

<span data-ttu-id="8efab-107">Atualmente, o Data Factory dá suporte apenas à movimentação de dados de um banco de dados DB2 para um [armazenamento de dados do coletor suportado](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="8efab-107">Data Factory currently supports only moving data from a DB2 database to a [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="8efab-108">Não há suporte para a movimentação de dados de outros armazenamentos de dados para um banco de dados DB2.</span><span class="sxs-lookup"><span data-stu-id="8efab-108">Moving data from other data stores to a DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8efab-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8efab-109">Prerequisites</span></span>
<span data-ttu-id="8efab-110">O Data Factory dá suporte à conexão com um banco de dados DB2 local usando o [gateway de gerenciamento de dados](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="8efab-110">Data Factory supports connecting to an on-premises DB2 database by using the [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="8efab-111">Para obter instruções passo a passo de como configurar o pipeline de dados de gateway para mover dados, confira o artigo [Mover dados de fontes locais para a nuvem](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="8efab-111">For step-by-step instructions to set up the gateway data pipeline to move your data, see the [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="8efab-112">O gateway é necessário, mesmo se o DB2 estiver hospedado na VM da Iaas do Azure.</span><span class="sxs-lookup"><span data-stu-id="8efab-112">A gateway is required even if the DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="8efab-113">Você pode instalar o gateway na mesma VM da IaaS que o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="8efab-113">You can install the gateway on the same IaaS VM as the data store.</span></span> <span data-ttu-id="8efab-114">Se o gateway puder se conectar com o banco de dados, você poderá instalar o gateway em uma VM diferente.</span><span class="sxs-lookup"><span data-stu-id="8efab-114">If the gateway can connect to the database, you can install the gateway on a different VM.</span></span>

<span data-ttu-id="8efab-115">O gateway de gerenciamento de dados fornece um driver DB2 interno, de modo que não é necessário instalar manualmente um driver para copiar dados do DB2.</span><span class="sxs-lookup"><span data-stu-id="8efab-115">The data management gateway provides a built-in DB2 driver, so you don't need to manually install a driver to copy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="8efab-116">Para obter dicas sobre como solucionar problemas de conexão e gateway, confira o artigo [Solução de problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).</span><span class="sxs-lookup"><span data-stu-id="8efab-116">For tips on troubleshooting connection and gateway issues, see the [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="8efab-117">Versões com suporte</span><span class="sxs-lookup"><span data-stu-id="8efab-117">Supported versions</span></span>
<span data-ttu-id="8efab-118">O conector DB2 do Data Factory dá suporte às seguintes plataformas e versões do IBM DB2 com as versões 9, 10 e 11 do SQL Access Manager da DRDA (Distributed Relational Database Architecture):</span><span class="sxs-lookup"><span data-stu-id="8efab-118">The Data Factory DB2 connector supports the following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="8efab-119">IBM DB2 para z/OS versão 11.1</span><span class="sxs-lookup"><span data-stu-id="8efab-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="8efab-120">IBM DB2 para z/OS versão 10.1</span><span class="sxs-lookup"><span data-stu-id="8efab-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="8efab-121">IBM DB2 para i (AS400) versão 7.2</span><span class="sxs-lookup"><span data-stu-id="8efab-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="8efab-122">IBM DB2 para i (AS400) versão 7.1</span><span class="sxs-lookup"><span data-stu-id="8efab-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="8efab-123">IBM DB2 para LUW (Linux, UNIX e Windows) versão 11</span><span class="sxs-lookup"><span data-stu-id="8efab-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="8efab-124">IBM DB2 para LUW versão 10.5</span><span class="sxs-lookup"><span data-stu-id="8efab-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="8efab-125">IBM DB2 para LUW versão 10.1</span><span class="sxs-lookup"><span data-stu-id="8efab-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="8efab-126">Se você receber a mensagem de erro "O pacote correspondente a uma solicitação de execução da instrução SQL não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="8efab-126">If you receive the error message "The package corresponding to an SQL statement execution request was not found.</span></span> <span data-ttu-id="8efab-127">SQLSTATE=51002 SQLCODE=-805", é porque um pacote necessário não foi criado para o usuário normal no SO.</span><span class="sxs-lookup"><span data-stu-id="8efab-127">SQLSTATE=51002 SQLCODE=-805," the reason is a necessary package is not created for the normal user on the OS.</span></span> <span data-ttu-id="8efab-128">Para resolver esse problema, siga estas instruções para seu tipo de servidor DB2:</span><span class="sxs-lookup"><span data-stu-id="8efab-128">To resolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="8efab-129">DB2 para i (AS400): permita que o usuário avançado crie a coleção para o usuário normal antes de executar a Atividade de Cópia.</span><span class="sxs-lookup"><span data-stu-id="8efab-129">DB2 for i (AS400): Let a power user create the collection for the normal user before running Copy Activity.</span></span> <span data-ttu-id="8efab-130">Para criar a coleção, use o comando: `create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="8efab-130">To create the collection, use the command: `create collection <username>`</span></span>
> - <span data-ttu-id="8efab-131">DB2 para z/OS ou LUW: use uma conta com privilégios elevados – um usuário avançado ou administrador com autoridades de pacote e permissões BIND, BINDADD, GRANT EXECUTE TO PUBLIC – para executar a cópia de uma vez.</span><span class="sxs-lookup"><span data-stu-id="8efab-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE TO PUBLIC permissions--to run the copy once.</span></span> <span data-ttu-id="8efab-132">O pacote necessário é criado automaticamente durante a cópia.</span><span class="sxs-lookup"><span data-stu-id="8efab-132">The necessary package is automatically created during the copy.</span></span> <span data-ttu-id="8efab-133">Posteriormente, você poderá voltar para o usuário normal para as execuções de cópia subsequentes.</span><span class="sxs-lookup"><span data-stu-id="8efab-133">Afterward, you can switch back to the normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="8efab-134">Introdução</span><span class="sxs-lookup"><span data-stu-id="8efab-134">Getting started</span></span>
<span data-ttu-id="8efab-135">Você pode criar um pipeline com uma atividade de cópia para mover dados de um armazenamento de dados DB2 local usando diferentes ferramentas e APIs:</span><span class="sxs-lookup"><span data-stu-id="8efab-135">You can create a pipeline with a copy activity to move data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="8efab-136">A maneira mais fácil de criar um pipeline é usando o Assistente de Cópia do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8efab-136">The easiest way to create a pipeline is to use the Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="8efab-137">Para obter um rápido passo a passo sobre como criar um pipeline usando o Assistente de Cópia, confira o [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="8efab-137">For a quick walkthrough on creating a pipeline by using the Copy Wizard, see the [Tutorial: Create a pipeline by using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="8efab-138">Você também pode usar ferramentas para criar um pipeline, incluindo o Portal do Azure, o Visual Studio, o Azure PowerShell, um modelo do Azure Resource Manager, a API .NET e a API REST.</span><span class="sxs-lookup"><span data-stu-id="8efab-138">You can also use tools to create a pipeline, including the Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, the .NET API, and the REST API.</span></span> <span data-ttu-id="8efab-139">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="8efab-139">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="8efab-140">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="8efab-140">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="8efab-141">Criar serviços vinculados para vincular armazenamentos de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="8efab-141">Create linked services to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="8efab-142">Criar conjuntos de dados para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="8efab-142">Create datasets to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="8efab-143">Criar um pipeline com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="8efab-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="8efab-144">Ao usar o Assistente de Cópia, as definições de JSON para os serviços vinculados, conjuntos de dados e entidades de pipeline do Data Factory são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="8efab-144">When you use the Copy Wizard, JSON definitions for the Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="8efab-145">Ao usar ferramentas ou APIs (exceto a API .NET), você define as entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="8efab-145">When you use tools or APIs (except the .NET API), you define the Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="8efab-146">O [Exemplo de JSON: copiar dados do DB2 para o armazenamento de Blobs do Azure](#json-example-copy-data-from-db2-to-azure-blob) mostra as definições de JSON para as entidades do Data Factory que são usadas para copiar dados de um armazenamento de dados DB2 local.</span><span class="sxs-lookup"><span data-stu-id="8efab-146">The [JSON example: Copy data from DB2 to Azure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows the JSON definitions for the Data Factory entities that are used to copy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="8efab-147">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas a um armazenamento de dados DB2.</span><span class="sxs-lookup"><span data-stu-id="8efab-147">The following sections provide details about the JSON properties that are used to define the Data Factory entities that are specific to a DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="8efab-148">Propriedades do serviço vinculado do DB2</span><span class="sxs-lookup"><span data-stu-id="8efab-148">DB2 linked service properties</span></span>
<span data-ttu-id="8efab-149">A tabela a seguir lista as propriedades JSON que são específicas a um serviço vinculado do DB2.</span><span class="sxs-lookup"><span data-stu-id="8efab-149">The following table lists the JSON properties that are specific to a DB2 linked service.</span></span>

| <span data-ttu-id="8efab-150">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8efab-150">Property</span></span> | <span data-ttu-id="8efab-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="8efab-151">Description</span></span> | <span data-ttu-id="8efab-152">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8efab-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8efab-153">**tipo**</span><span class="sxs-lookup"><span data-stu-id="8efab-153">**type**</span></span> |<span data-ttu-id="8efab-154">Essa propriedade deve ser definida como **OnPremisesDB2**.</span><span class="sxs-lookup"><span data-stu-id="8efab-154">This property must be set to **OnPremisesDB2**.</span></span> |<span data-ttu-id="8efab-155">Sim</span><span class="sxs-lookup"><span data-stu-id="8efab-155">Yes</span></span> |
| <span data-ttu-id="8efab-156">**server**</span><span class="sxs-lookup"><span data-stu-id="8efab-156">**server**</span></span> |<span data-ttu-id="8efab-157">O nome do servidor DB2.</span><span class="sxs-lookup"><span data-stu-id="8efab-157">The name of the DB2 server.</span></span> |<span data-ttu-id="8efab-158">Sim</span><span class="sxs-lookup"><span data-stu-id="8efab-158">Yes</span></span> |
| <span data-ttu-id="8efab-159">**database**</span><span class="sxs-lookup"><span data-stu-id="8efab-159">**database**</span></span> |<span data-ttu-id="8efab-160">O nome do banco de dados DB2.</span><span class="sxs-lookup"><span data-stu-id="8efab-160">The name of the DB2 database.</span></span> |<span data-ttu-id="8efab-161">Sim</span><span class="sxs-lookup"><span data-stu-id="8efab-161">Yes</span></span> |
| <span data-ttu-id="8efab-162">**schema**</span><span class="sxs-lookup"><span data-stu-id="8efab-162">**schema**</span></span> |<span data-ttu-id="8efab-163">O nome do esquema no banco de dados DB2.</span><span class="sxs-lookup"><span data-stu-id="8efab-163">The name of the schema in the DB2 database.</span></span> <span data-ttu-id="8efab-164">Essa propriedade diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8efab-164">This property is case-sensitive.</span></span> |<span data-ttu-id="8efab-165">Não</span><span class="sxs-lookup"><span data-stu-id="8efab-165">No</span></span> |
| <span data-ttu-id="8efab-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="8efab-166">**authenticationType**</span></span> |<span data-ttu-id="8efab-167">O tipo de autenticação que é usado para se conectar ao banco de dados DB2.</span><span class="sxs-lookup"><span data-stu-id="8efab-167">The type of authentication that is used to connect to the DB2 database.</span></span> <span data-ttu-id="8efab-168">Os valores possíveis são: Anônimo, Básico e Windows.</span><span class="sxs-lookup"><span data-stu-id="8efab-168">The possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="8efab-169">Sim</span><span class="sxs-lookup"><span data-stu-id="8efab-169">Yes</span></span> |
| <span data-ttu-id="8efab-170">**username**</span><span class="sxs-lookup"><span data-stu-id="8efab-170">**username**</span></span> |<span data-ttu-id="8efab-171">O nome da conta de usuário, se você usar a autenticação Básica ou do Windows.</span><span class="sxs-lookup"><span data-stu-id="8efab-171">The name for the user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="8efab-172">Não</span><span class="sxs-lookup"><span data-stu-id="8efab-172">No</span></span> |
| <span data-ttu-id="8efab-173">**password**</span><span class="sxs-lookup"><span data-stu-id="8efab-173">**password**</span></span> |<span data-ttu-id="8efab-174">A senha para a conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="8efab-174">The password for the user account.</span></span> |<span data-ttu-id="8efab-175">Não</span><span class="sxs-lookup"><span data-stu-id="8efab-175">No</span></span> |
| <span data-ttu-id="8efab-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="8efab-176">**gatewayName**</span></span> |<span data-ttu-id="8efab-177">O nome do gateway que o serviço Data Factory deve usar para se conectar ao banco de dados DB2 local.</span><span class="sxs-lookup"><span data-stu-id="8efab-177">The name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="8efab-178">Sim</span><span class="sxs-lookup"><span data-stu-id="8efab-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="8efab-179">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="8efab-179">Dataset properties</span></span>
<span data-ttu-id="8efab-180">Para obter uma lista das seções e propriedades disponíveis para definir os conjuntos de dados, veja o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="8efab-180">For a list of the sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="8efab-181">As seções como **structure**, **availability** e **policy** de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, armazenamento de Blobs do Azure, armazenamento de Tabelas do Azure, entre outros).</span><span class="sxs-lookup"><span data-stu-id="8efab-181">Sections, such as **structure**, **availability**, and the **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="8efab-182">A seção **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="8efab-182">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="8efab-183">A seção **typeProperties** de um conjunto de dados do tipo **RelationalTable**, que inclui o conjunto de dados do DB2, tem a seguinte propriedade:</span><span class="sxs-lookup"><span data-stu-id="8efab-183">The **typeProperties** section for a dataset of type **RelationalTable**, which includes the DB2 dataset, has the following property:</span></span>

| <span data-ttu-id="8efab-184">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8efab-184">Property</span></span> | <span data-ttu-id="8efab-185">Descrição</span><span class="sxs-lookup"><span data-stu-id="8efab-185">Description</span></span> | <span data-ttu-id="8efab-186">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8efab-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8efab-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="8efab-187">**tableName**</span></span> |<span data-ttu-id="8efab-188">O nome da tabela na instância do banco de dados DB2 à qual o serviço vinculado se refere.</span><span class="sxs-lookup"><span data-stu-id="8efab-188">The name of the table in the DB2 database instance that the linked service refers to.</span></span> <span data-ttu-id="8efab-189">Essa propriedade diferencia maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8efab-189">This property is case-sensitive.</span></span> |<span data-ttu-id="8efab-190">Não (se a propriedade **query** de uma atividade de cópia do tipo **RelationalSource** for especificada)</span><span class="sxs-lookup"><span data-stu-id="8efab-190">No (if the **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="8efab-191">Propriedades da Atividade de Cópia</span><span class="sxs-lookup"><span data-stu-id="8efab-191">Copy Activity properties</span></span>
<span data-ttu-id="8efab-192">Para obter uma lista das seções e propriedades disponíveis para definir as atividades de cópia, veja o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="8efab-192">For a list of the sections and properties that are available for defining copy activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8efab-193">As propriedades da Atividade de Cópia, como **name**, **description**, tabela **inputs**, tabela **outputs** e **policy** estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="8efab-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="8efab-194">As propriedades estão disponíveis na seção **typeProperties** da atividade para cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="8efab-194">The properties that are available in the **typeProperties** section of the activity for each activity type.</span></span> <span data-ttu-id="8efab-195">Para a Atividade de Cópia, as propriedades variam conforme os tipos de fonte de dados e coletor.</span><span class="sxs-lookup"><span data-stu-id="8efab-195">For Copy Activity, the properties vary depending on the types of data sources and sinks.</span></span>

<span data-ttu-id="8efab-196">Para a Atividade de Cópia, quando a fonte for do tipo **RelationalSource** (que inclui o DB2), as seguintes propriedades estarão disponíveis na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="8efab-196">For Copy Activity, when the source is of type **RelationalSource** (which includes DB2), the following properties are available in the **typeProperties** section:</span></span>

| <span data-ttu-id="8efab-197">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8efab-197">Property</span></span> | <span data-ttu-id="8efab-198">Descrição</span><span class="sxs-lookup"><span data-stu-id="8efab-198">Description</span></span> | <span data-ttu-id="8efab-199">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="8efab-199">Allowed values</span></span> | <span data-ttu-id="8efab-200">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8efab-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8efab-201">**query**</span><span class="sxs-lookup"><span data-stu-id="8efab-201">**query**</span></span> |<span data-ttu-id="8efab-202">Use a consulta personalizada para ler os dados.</span><span class="sxs-lookup"><span data-stu-id="8efab-202">Use the custom query to read the data.</span></span> |<span data-ttu-id="8efab-203">Cadeia de caracteres de consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="8efab-203">SQL query string.</span></span> <span data-ttu-id="8efab-204">Por exemplo: `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="8efab-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="8efab-205">Não (se a propriedade **tableName** de um conjunto de dados for especificada)</span><span class="sxs-lookup"><span data-stu-id="8efab-205">No (if the **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="8efab-206">Os nomes de esquema e tabela diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="8efab-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="8efab-207">Na instrução de consulta, coloque os nomes de propriedade usando "" (aspas duplas).</span><span class="sxs-lookup"><span data-stu-id="8efab-207">In the query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="8efab-208">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8efab-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-to-azure-blob-storage"></a><span data-ttu-id="8efab-209">Exemplo de JSON: copiar dados do DB2 para o armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="8efab-209">JSON example: Copy data from DB2 to Azure Blob storage</span></span>
<span data-ttu-id="8efab-210">Esse exemplo fornece amostra de definições de JSON que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8efab-210">This example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="8efab-211">O exemplo mostra como copiar dados de um banco de dados do DB2 no armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="8efab-211">The example shows you how to copy data from a DB2 database to Blob storage.</span></span> <span data-ttu-id="8efab-212">No entanto, os dados podem ser copiados em [qualquer tipo de coletor de armazenamento de dados suportado](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a Atividade de Cópia do Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8efab-212">However, data can be copied to [any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="8efab-213">O exemplo tem as seguintes entidades do Data Factory:</span><span class="sxs-lookup"><span data-stu-id="8efab-213">The sample has the following Data Factory entities:</span></span>

- <span data-ttu-id="8efab-214">Um serviço vinculado do DB2 do tipo [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="8efab-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="8efab-215">Um serviço vinculado de armazenamento de Blobs do Azure do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="8efab-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="8efab-216">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="8efab-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="8efab-217">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="8efab-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="8efab-218">Um [pipeline](data-factory-create-pipelines.md) com uma atividade de cópia que usa as propriedades [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="8efab-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses the [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="8efab-219">O exemplo copia dados de um resultado de consulta no banco de dados DB2 para um blob do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="8efab-219">The sample copies data from a query result in a DB2 database to an Azure blob hourly.</span></span> <span data-ttu-id="8efab-220">As propriedades JSON que são usadas no exemplo são descritas nas seções que seguem as definições de entidade.</span><span class="sxs-lookup"><span data-stu-id="8efab-220">The JSON properties that are used in the sample are described in the sections that follow the entity definitions.</span></span>

<span data-ttu-id="8efab-221">Primeiramente, instale e configure um gateway de dados.</span><span class="sxs-lookup"><span data-stu-id="8efab-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="8efab-222">As instruções estão no artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="8efab-222">Instructions are in the [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="8efab-223">**Serviço vinculado do DB2**</span><span class="sxs-lookup"><span data-stu-id="8efab-223">**DB2 linked service**</span></span>

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

<span data-ttu-id="8efab-224">**Serviço vinculado do armazenamento de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="8efab-224">**Azure Blob storage linked service**</span></span>

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

<span data-ttu-id="8efab-225">**Conjunto de dados de entrada do DB2**</span><span class="sxs-lookup"><span data-stu-id="8efab-225">**DB2 input dataset**</span></span>

<span data-ttu-id="8efab-226">O exemplo supõe que você tenha criado uma tabela no DB2 chamada "MyTable" que tenha uma coluna rotulada "timestamp" para os dados seriais de tempo.</span><span class="sxs-lookup"><span data-stu-id="8efab-226">The sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for the time series data.</span></span>

<span data-ttu-id="8efab-227">A propriedade **external** está definida como "true."</span><span class="sxs-lookup"><span data-stu-id="8efab-227">The **external** property is set to "true."</span></span> <span data-ttu-id="8efab-228">Essa configuração informa o serviço Data Factory que o conjunto de dados é externo ao data factory e não é produzido por uma atividade no data factory.</span><span class="sxs-lookup"><span data-stu-id="8efab-228">This setting informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="8efab-229">Observe que a propriedade **type** é definida como **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="8efab-229">Notice that the **type** property is set to **RelationalTable**.</span></span>


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

<span data-ttu-id="8efab-230">**Conjunto de dados de saída de Blob do Azure**</span><span class="sxs-lookup"><span data-stu-id="8efab-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="8efab-231">Os dados são gravados em um novo blob de hora em hora pela definição da propriedade **frequency** como "Hour" e a propriedade **interval** como 1.</span><span class="sxs-lookup"><span data-stu-id="8efab-231">Data is written to a new blob every hour by setting the **frequency** property to "Hour" and the **interval** property to 1.</span></span> <span data-ttu-id="8efab-232">A propriedade **folderPath** do blob é avaliada dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="8efab-232">The **folderPath** property for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="8efab-233">O caminho da pasta usa as partes ano, mês, dia e hora da hora de início.</span><span class="sxs-lookup"><span data-stu-id="8efab-233">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

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

<span data-ttu-id="8efab-234">**Pipeline para a atividade de cópia**</span><span class="sxs-lookup"><span data-stu-id="8efab-234">**Pipeline for the copy activity**</span></span>

<span data-ttu-id="8efab-235">O pipeline contém uma atividade de cópia que está configurada para usar os conjuntos de dados especificados de entrada e saída e que está agendada para ser executada de hora em hora.</span><span class="sxs-lookup"><span data-stu-id="8efab-235">The pipeline contains a copy activity that is configured to use specified input and output datasets and which is scheduled to run every hour.</span></span> <span data-ttu-id="8efab-236">Na definição JSON do pipeline, o tipo **source** está definido como **RelationalSource** e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="8efab-236">In the JSON definition for the pipeline, the **source** type is set to **RelationalSource** and the **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="8efab-237">A consulta SQL especificada para a propriedade **query** seleciona os dados da tabela "Orders".</span><span class="sxs-lookup"><span data-stu-id="8efab-237">The SQL query specified for the **query** property selects the data from the "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for the copy activity",
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

## <a name="type-mapping-for-db2"></a><span data-ttu-id="8efab-238">Mapeamento de tipo para DB2</span><span class="sxs-lookup"><span data-stu-id="8efab-238">Type mapping for DB2</span></span>
<span data-ttu-id="8efab-239">Como mencionado no artigo sobre as [atividades de movimentação de dados](data-factory-data-movement-activities.md), a Atividade de Cópia executa conversões automáticas do tipo de fonte em tipo de coletor usando a seguinte abordagem de duas etapas:</span><span class="sxs-lookup"><span data-stu-id="8efab-239">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type to sink type by using the following two-step approach:</span></span>

1. <span data-ttu-id="8efab-240">Converter de tipo de origem nativo em um tipo .NET</span><span class="sxs-lookup"><span data-stu-id="8efab-240">Convert from a native source type to a .NET type</span></span>
2. <span data-ttu-id="8efab-241">Converter de um tipo .NET em um tipo de coletor nativo</span><span class="sxs-lookup"><span data-stu-id="8efab-241">Convert from a .NET type to a native sink type</span></span>

<span data-ttu-id="8efab-242">Os seguintes mapeamentos são usados quando a Atividade de Cópia converte os dados de um tipo DB2 em um tipo .NET:</span><span class="sxs-lookup"><span data-stu-id="8efab-242">The following mappings are used when Copy Activity converts the data from a DB2 type to a .NET type:</span></span>

| <span data-ttu-id="8efab-243">Tipo do banco de dados DB2</span><span class="sxs-lookup"><span data-stu-id="8efab-243">DB2 database type</span></span> | <span data-ttu-id="8efab-244">Tipo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="8efab-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="8efab-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="8efab-245">SmallInt</span></span> |<span data-ttu-id="8efab-246">Int16</span><span class="sxs-lookup"><span data-stu-id="8efab-246">Int16</span></span> |
| <span data-ttu-id="8efab-247">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="8efab-247">Integer</span></span> |<span data-ttu-id="8efab-248">Int32</span><span class="sxs-lookup"><span data-stu-id="8efab-248">Int32</span></span> |
| <span data-ttu-id="8efab-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="8efab-249">BigInt</span></span> |<span data-ttu-id="8efab-250">Int64</span><span class="sxs-lookup"><span data-stu-id="8efab-250">Int64</span></span> |
| <span data-ttu-id="8efab-251">Real</span><span class="sxs-lookup"><span data-stu-id="8efab-251">Real</span></span> |<span data-ttu-id="8efab-252">Single</span><span class="sxs-lookup"><span data-stu-id="8efab-252">Single</span></span> |
| <span data-ttu-id="8efab-253">Duplo</span><span class="sxs-lookup"><span data-stu-id="8efab-253">Double</span></span> |<span data-ttu-id="8efab-254">Duplo</span><span class="sxs-lookup"><span data-stu-id="8efab-254">Double</span></span> |
| <span data-ttu-id="8efab-255">Float</span><span class="sxs-lookup"><span data-stu-id="8efab-255">Float</span></span> |<span data-ttu-id="8efab-256">Duplo</span><span class="sxs-lookup"><span data-stu-id="8efab-256">Double</span></span> |
| <span data-ttu-id="8efab-257">Decimal</span><span class="sxs-lookup"><span data-stu-id="8efab-257">Decimal</span></span> |<span data-ttu-id="8efab-258">Decimal</span><span class="sxs-lookup"><span data-stu-id="8efab-258">Decimal</span></span> |
| <span data-ttu-id="8efab-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="8efab-259">DecimalFloat</span></span> |<span data-ttu-id="8efab-260">Decimal</span><span class="sxs-lookup"><span data-stu-id="8efab-260">Decimal</span></span> |
| <span data-ttu-id="8efab-261">Numérico</span><span class="sxs-lookup"><span data-stu-id="8efab-261">Numeric</span></span> |<span data-ttu-id="8efab-262">Decimal</span><span class="sxs-lookup"><span data-stu-id="8efab-262">Decimal</span></span> |
| <span data-ttu-id="8efab-263">Data</span><span class="sxs-lookup"><span data-stu-id="8efab-263">Date</span></span> |<span data-ttu-id="8efab-264">DateTime</span><span class="sxs-lookup"><span data-stu-id="8efab-264">DateTime</span></span> |
| <span data-ttu-id="8efab-265">Hora</span><span class="sxs-lookup"><span data-stu-id="8efab-265">Time</span></span> |<span data-ttu-id="8efab-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="8efab-266">TimeSpan</span></span> |
| <span data-ttu-id="8efab-267">Timestamp</span><span class="sxs-lookup"><span data-stu-id="8efab-267">Timestamp</span></span> |<span data-ttu-id="8efab-268">Datetime</span><span class="sxs-lookup"><span data-stu-id="8efab-268">DateTime</span></span> |
| <span data-ttu-id="8efab-269">xml</span><span class="sxs-lookup"><span data-stu-id="8efab-269">Xml</span></span> |<span data-ttu-id="8efab-270">Byte[]</span><span class="sxs-lookup"><span data-stu-id="8efab-270">Byte[]</span></span> |
| <span data-ttu-id="8efab-271">Char</span><span class="sxs-lookup"><span data-stu-id="8efab-271">Char</span></span> |<span data-ttu-id="8efab-272">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8efab-272">String</span></span> |
| <span data-ttu-id="8efab-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="8efab-273">VarChar</span></span> |<span data-ttu-id="8efab-274">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8efab-274">String</span></span> |
| <span data-ttu-id="8efab-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="8efab-275">LongVarChar</span></span> |<span data-ttu-id="8efab-276">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8efab-276">String</span></span> |
| <span data-ttu-id="8efab-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="8efab-277">DB2DynArray</span></span> |<span data-ttu-id="8efab-278">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8efab-278">String</span></span> |
| <span data-ttu-id="8efab-279">Binário</span><span class="sxs-lookup"><span data-stu-id="8efab-279">Binary</span></span> |<span data-ttu-id="8efab-280">Byte[]</span><span class="sxs-lookup"><span data-stu-id="8efab-280">Byte[]</span></span> |
| <span data-ttu-id="8efab-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="8efab-281">VarBinary</span></span> |<span data-ttu-id="8efab-282">Byte[]</span><span class="sxs-lookup"><span data-stu-id="8efab-282">Byte[]</span></span> |
| <span data-ttu-id="8efab-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="8efab-283">LongVarBinary</span></span> |<span data-ttu-id="8efab-284">Byte[]</span><span class="sxs-lookup"><span data-stu-id="8efab-284">Byte[]</span></span> |
| <span data-ttu-id="8efab-285">Graphic</span><span class="sxs-lookup"><span data-stu-id="8efab-285">Graphic</span></span> |<span data-ttu-id="8efab-286">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8efab-286">String</span></span> |
| <span data-ttu-id="8efab-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="8efab-287">VarGraphic</span></span> |<span data-ttu-id="8efab-288">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8efab-288">String</span></span> |
| <span data-ttu-id="8efab-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="8efab-289">LongVarGraphic</span></span> |<span data-ttu-id="8efab-290">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8efab-290">String</span></span> |
| <span data-ttu-id="8efab-291">Clob</span><span class="sxs-lookup"><span data-stu-id="8efab-291">Clob</span></span> |<span data-ttu-id="8efab-292">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8efab-292">String</span></span> |
| <span data-ttu-id="8efab-293">Blob</span><span class="sxs-lookup"><span data-stu-id="8efab-293">Blob</span></span> |<span data-ttu-id="8efab-294">Byte[]</span><span class="sxs-lookup"><span data-stu-id="8efab-294">Byte[]</span></span> |
| <span data-ttu-id="8efab-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="8efab-295">DbClob</span></span> |<span data-ttu-id="8efab-296">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8efab-296">String</span></span> |
| <span data-ttu-id="8efab-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="8efab-297">SmallInt</span></span> |<span data-ttu-id="8efab-298">Int16</span><span class="sxs-lookup"><span data-stu-id="8efab-298">Int16</span></span> |
| <span data-ttu-id="8efab-299">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="8efab-299">Integer</span></span> |<span data-ttu-id="8efab-300">Int32</span><span class="sxs-lookup"><span data-stu-id="8efab-300">Int32</span></span> |
| <span data-ttu-id="8efab-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="8efab-301">BigInt</span></span> |<span data-ttu-id="8efab-302">Int64</span><span class="sxs-lookup"><span data-stu-id="8efab-302">Int64</span></span> |
| <span data-ttu-id="8efab-303">Real</span><span class="sxs-lookup"><span data-stu-id="8efab-303">Real</span></span> |<span data-ttu-id="8efab-304">Single</span><span class="sxs-lookup"><span data-stu-id="8efab-304">Single</span></span> |
| <span data-ttu-id="8efab-305">Duplo</span><span class="sxs-lookup"><span data-stu-id="8efab-305">Double</span></span> |<span data-ttu-id="8efab-306">Duplo</span><span class="sxs-lookup"><span data-stu-id="8efab-306">Double</span></span> |
| <span data-ttu-id="8efab-307">Float</span><span class="sxs-lookup"><span data-stu-id="8efab-307">Float</span></span> |<span data-ttu-id="8efab-308">Duplo</span><span class="sxs-lookup"><span data-stu-id="8efab-308">Double</span></span> |
| <span data-ttu-id="8efab-309">Decimal</span><span class="sxs-lookup"><span data-stu-id="8efab-309">Decimal</span></span> |<span data-ttu-id="8efab-310">Decimal</span><span class="sxs-lookup"><span data-stu-id="8efab-310">Decimal</span></span> |
| <span data-ttu-id="8efab-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="8efab-311">DecimalFloat</span></span> |<span data-ttu-id="8efab-312">Decimal</span><span class="sxs-lookup"><span data-stu-id="8efab-312">Decimal</span></span> |
| <span data-ttu-id="8efab-313">Numérico</span><span class="sxs-lookup"><span data-stu-id="8efab-313">Numeric</span></span> |<span data-ttu-id="8efab-314">Decimal</span><span class="sxs-lookup"><span data-stu-id="8efab-314">Decimal</span></span> |
| <span data-ttu-id="8efab-315">Data</span><span class="sxs-lookup"><span data-stu-id="8efab-315">Date</span></span> |<span data-ttu-id="8efab-316">DateTime</span><span class="sxs-lookup"><span data-stu-id="8efab-316">DateTime</span></span> |
| <span data-ttu-id="8efab-317">Hora</span><span class="sxs-lookup"><span data-stu-id="8efab-317">Time</span></span> |<span data-ttu-id="8efab-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="8efab-318">TimeSpan</span></span> |
| <span data-ttu-id="8efab-319">Timestamp</span><span class="sxs-lookup"><span data-stu-id="8efab-319">Timestamp</span></span> |<span data-ttu-id="8efab-320">Datetime</span><span class="sxs-lookup"><span data-stu-id="8efab-320">DateTime</span></span> |
| <span data-ttu-id="8efab-321">xml</span><span class="sxs-lookup"><span data-stu-id="8efab-321">Xml</span></span> |<span data-ttu-id="8efab-322">Byte[]</span><span class="sxs-lookup"><span data-stu-id="8efab-322">Byte[]</span></span> |
| <span data-ttu-id="8efab-323">Char</span><span class="sxs-lookup"><span data-stu-id="8efab-323">Char</span></span> |<span data-ttu-id="8efab-324">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="8efab-324">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="8efab-325">Mapear origem para colunas de coletor</span><span class="sxs-lookup"><span data-stu-id="8efab-325">Map source to sink columns</span></span>
<span data-ttu-id="8efab-326">Para saber mais sobre como mapear colunas no conjunto de dados de origem para colunas no conjunto de dados de coletor, confira [Mapeando colunas de conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="8efab-326">To learn how to map columns in the source dataset to columns in the sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="8efab-327">Leituras repetidas de fontes relacionais</span><span class="sxs-lookup"><span data-stu-id="8efab-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="8efab-328">Ao copiar dados de um armazenamento de dados relacional, lembre-se da capacidade de repetição para evitar resultados não intencionais.</span><span class="sxs-lookup"><span data-stu-id="8efab-328">When you copy data from a relational data store, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="8efab-329">No Azure Data Factory, você pode repetir a execução de uma fatia manualmente.</span><span class="sxs-lookup"><span data-stu-id="8efab-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="8efab-330">Você também pode configurar a propriedade **policy** de repetição para um conjunto de dados, a fim de executar novamente uma fatia quando ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="8efab-330">You can also configure the retry **policy** property for a dataset to rerun a slice when a failure occurs.</span></span> <span data-ttu-id="8efab-331">Certifique-se de que os mesmos dados sejam lidos, não importa quantas vezes a fatia seja executada e independentemente de como você executa novamente a fatia.</span><span class="sxs-lookup"><span data-stu-id="8efab-331">Make sure that the same data is read no matter how many times the slice is rerun, and regardless of how you rerun the slice.</span></span> <span data-ttu-id="8efab-332">Para saber mais, confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="8efab-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="8efab-333">Desempenho e ajuste</span><span class="sxs-lookup"><span data-stu-id="8efab-333">Performance and tuning</span></span>
<span data-ttu-id="8efab-334">Saiba mais sobre os principais fatores que afetam o desempenho da Atividade de Cópia e maneiras de otimizar o desempenho no [Guia de Desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="8efab-334">Learn about key factors that affect the performance of Copy Activity and ways to optimize performance in the [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>