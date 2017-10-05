---
title: Mover dados a partir do HDFS local | Microsoft Docs
description: Saiba mais sobre como mover dados do HDFS local usando o Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9a8f3156a62a1a7aa49377349e8a85454efeda50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="74644-103">Mover dados do HDFS local usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="74644-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
<span data-ttu-id="74644-104">Esse artigo explica como usar a Atividade de Cópia no Azure Data Factory para mover dados de um HDFS local.</span><span class="sxs-lookup"><span data-stu-id="74644-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises HDFS.</span></span> <span data-ttu-id="74644-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="74644-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="74644-106">Você pode copiar dados de um HDFS para qualquer armazenamento de dados de coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="74644-106">You can copy data from HDFS to any supported sink data store.</span></span> <span data-ttu-id="74644-107">Para obter uma lista de repositórios de dados com suporte como coletores da atividade de cópia, confira a tabela [Repositórios de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="74644-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="74644-108">Atualmente, a data factory dá suporte apenas para a movimentação de dados de um HDFS local para outros armazenamentos de dados, mas não para a movimentação de dados de outros armazenamentos de dados para um HDFS local.</span><span class="sxs-lookup"><span data-stu-id="74644-108">Data factory currently supports only moving data from an on-premises HDFS to other data stores, but not for moving data from other data stores to an on-premises HDFS.</span></span>

> [!NOTE]
> <span data-ttu-id="74644-109">A Atividade de Cópia não exclui o arquivo de origem depois que ele é copiado com êxito para o destino.</span><span class="sxs-lookup"><span data-stu-id="74644-109">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="74644-110">Se precisar excluir o arquivo de origem após uma cópia bem-sucedida, crie uma atividade personalizada para excluir o arquivo e use a atividade no pipeline.</span><span class="sxs-lookup"><span data-stu-id="74644-110">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="74644-111">Habilitando a conectividade</span><span class="sxs-lookup"><span data-stu-id="74644-111">Enabling connectivity</span></span>
<span data-ttu-id="74644-112">O serviço Data Factory dá suporte à conexão com HDFS local usando o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="74644-112">Data Factory service supports connecting to on-premises HDFS using the Data Management Gateway.</span></span> <span data-ttu-id="74644-113">Consulte o artigo [movendo dados entre pontos locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) para saber mais sobre o Gateway de gerenciamento de dados e obter instruções passo a passo de como configurar o gateway.</span><span class="sxs-lookup"><span data-stu-id="74644-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="74644-114">Use o gateway para se conectar ao HDFS, mesmo se ele estiver hospedado em uma VM IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="74644-114">Use the gateway to connect to HDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="74644-115">Verifique se o Gateway de gerenciamento de dados pode acessar **TODOS** os [servidor de nó de nome]: [porta do nó de nome] e [servidores de nó de dados]:[porta do nó de dados] do cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="74644-115">Make sure the Data Management Gateway can access to **ALL** the [name node server]:[name node port] and [data node servers]:[data node port] of the Hadoop cluster.</span></span> <span data-ttu-id="74644-116">A [porta do nó de nome] padrão é 50070, e a [porta do nó de dados] padrão é 50075.</span><span class="sxs-lookup"><span data-stu-id="74644-116">Default [name node port] is 50070, and default [data node port] is 50075.</span></span>

<span data-ttu-id="74644-117">Embora você possa instalar o gateway no mesmo computador local ou a VM do Azure como o HDFS, recomendamos que você instale o gateway em um computador separado ou em uma VM IaaS do Azure separada.</span><span class="sxs-lookup"><span data-stu-id="74644-117">While you can install gateway on the same on-premises machine or the Azure VM as the HDFS, we recommend that you install the gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="74644-118">Ter o gateway em um computador separado reduz a contenção de recursos e aprimora o desempenho.</span><span class="sxs-lookup"><span data-stu-id="74644-118">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="74644-119">Quando você instalar o gateway em um computador separado, o computador deverá ser capaz de acessar o computador com o HDFS.</span><span class="sxs-lookup"><span data-stu-id="74644-119">When you install the gateway on a separate machine, the machine should be able to access the machine with the HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="74644-120">Introdução</span><span class="sxs-lookup"><span data-stu-id="74644-120">Getting started</span></span>
<span data-ttu-id="74644-121">Você pode criar um pipeline com uma atividade de cópia que mova dados de uma origem HDFS usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="74644-121">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="74644-122">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="74644-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="74644-123">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="74644-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="74644-124">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="74644-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="74644-125">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="74644-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="74644-126">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="74644-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="74644-127">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="74644-127">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="74644-128">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="74644-128">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="74644-129">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="74644-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="74644-130">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="74644-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="74644-131">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="74644-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="74644-132">Para obter um exemplo com definições de JSON para entidades do Data Factory que são usadas para copiar dados de um armazenamento de dados HDFS local, confira a seção [Exemplo de JSON: Copiar dados do HDFS local para o Blob do Azure](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="74644-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS to Azure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="74644-133">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas ao HDFS:</span><span class="sxs-lookup"><span data-stu-id="74644-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to HDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="74644-134">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="74644-134">Linked service properties</span></span>
<span data-ttu-id="74644-135">Um serviço vinculado vincula um armazenamento de dados a um data factory.</span><span class="sxs-lookup"><span data-stu-id="74644-135">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="74644-136">Crie um serviço vinculado do tipo **Hdfs** para vincular um HDFS local ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="74644-136">You create a linked service of type **Hdfs** to link an on-premises HDFS to your data factory.</span></span> <span data-ttu-id="74644-137">A tabela a seguir fornece a descrição para elementos JSON específicos para o serviço vinculado do HDFS.</span><span class="sxs-lookup"><span data-stu-id="74644-137">The following table provides description for JSON elements specific to HDFS linked service.</span></span>

| <span data-ttu-id="74644-138">Propriedade</span><span class="sxs-lookup"><span data-stu-id="74644-138">Property</span></span> | <span data-ttu-id="74644-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="74644-139">Description</span></span> | <span data-ttu-id="74644-140">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="74644-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="74644-141">type</span><span class="sxs-lookup"><span data-stu-id="74644-141">type</span></span> |<span data-ttu-id="74644-142">A propriedade type deve ser definida como: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="74644-142">The type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="74644-143">Sim</span><span class="sxs-lookup"><span data-stu-id="74644-143">Yes</span></span> |
| <span data-ttu-id="74644-144">Url</span><span class="sxs-lookup"><span data-stu-id="74644-144">Url</span></span> |<span data-ttu-id="74644-145">URL para o HDFS</span><span class="sxs-lookup"><span data-stu-id="74644-145">URL to the HDFS</span></span> |<span data-ttu-id="74644-146">Sim</span><span class="sxs-lookup"><span data-stu-id="74644-146">Yes</span></span> |
| <span data-ttu-id="74644-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="74644-147">authenticationType</span></span> |<span data-ttu-id="74644-148">Anônimo ou Windows.</span><span class="sxs-lookup"><span data-stu-id="74644-148">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="74644-149">Para usar **autenticação Kerberos** com o conector HDFS, veja [esta seção](#use-kerberos-authentication-for-hdfs-connector) para configurar seu ambiente local adequadamente.</span><span class="sxs-lookup"><span data-stu-id="74644-149">To use **Kerberos authentication** for HDFS connector, refer to [this section](#use-kerberos-authentication-for-hdfs-connector) to set up your on-premises environment accordingly.</span></span> |<span data-ttu-id="74644-150">Sim</span><span class="sxs-lookup"><span data-stu-id="74644-150">Yes</span></span> |
| <span data-ttu-id="74644-151">userName</span><span class="sxs-lookup"><span data-stu-id="74644-151">userName</span></span> |<span data-ttu-id="74644-152">Nome de usuário para a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="74644-152">Username for Windows authentication.</span></span> |<span data-ttu-id="74644-153">Sim (para a Autenticação do Windows)</span><span class="sxs-lookup"><span data-stu-id="74644-153">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="74644-154">Senha</span><span class="sxs-lookup"><span data-stu-id="74644-154">password</span></span> |<span data-ttu-id="74644-155">Senha para a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="74644-155">Password for Windows authentication.</span></span> |<span data-ttu-id="74644-156">Sim (para a Autenticação do Windows)</span><span class="sxs-lookup"><span data-stu-id="74644-156">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="74644-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="74644-157">gatewayName</span></span> |<span data-ttu-id="74644-158">O nome do gateway que o serviço Data Factory deve usar para se conectar ao HDFS.</span><span class="sxs-lookup"><span data-stu-id="74644-158">Name of the gateway that the Data Factory service should use to connect to the HDFS.</span></span> |<span data-ttu-id="74644-159">Sim</span><span class="sxs-lookup"><span data-stu-id="74644-159">Yes</span></span> |
| <span data-ttu-id="74644-160">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="74644-160">encryptedCredential</span></span> |<span data-ttu-id="74644-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) da credencial de acesso.</span><span class="sxs-lookup"><span data-stu-id="74644-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of the access credential.</span></span> |<span data-ttu-id="74644-162">Não</span><span class="sxs-lookup"><span data-stu-id="74644-162">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="74644-163">Usando a autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="74644-163">Using Anonymous authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a><span data-ttu-id="74644-164">Usando a autenticação do Windows</span><span class="sxs-lookup"><span data-stu-id="74644-164">Using Windows authentication</span></span>

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a><span data-ttu-id="74644-165">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="74644-165">Dataset properties</span></span>
<span data-ttu-id="74644-166">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, confira o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="74644-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="74644-167">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="74644-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="74644-168">A seção **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="74644-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="74644-169">A seção typeProperties para o conjunto de dados do tipo **FileShare** (que inclui o conjunto de dados do HDFS) tem as propriedades a seguir</span><span class="sxs-lookup"><span data-stu-id="74644-169">The typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has the following properties</span></span>

| <span data-ttu-id="74644-170">Propriedade</span><span class="sxs-lookup"><span data-stu-id="74644-170">Property</span></span> | <span data-ttu-id="74644-171">Descrição</span><span class="sxs-lookup"><span data-stu-id="74644-171">Description</span></span> | <span data-ttu-id="74644-172">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="74644-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="74644-173">folderPath</span><span class="sxs-lookup"><span data-stu-id="74644-173">folderPath</span></span> |<span data-ttu-id="74644-174">Caminho para a pasta.</span><span class="sxs-lookup"><span data-stu-id="74644-174">Path to the folder.</span></span> <span data-ttu-id="74644-175">Exemplo: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="74644-175">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="74644-176">Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="74644-176">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="74644-177">Por exemplo: para pasta\subpasta, especifique a pasta\\\\subpasta e para d:\pastadeexemplo, especifique d:\\\\pastadeexemplo.</span><span class="sxs-lookup"><span data-stu-id="74644-177">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="74644-178">Você pode combinar essa propriedade com **partitionBy** para ter caminhos de pastas com base na fatia de data/hora de início/término.</span><span class="sxs-lookup"><span data-stu-id="74644-178">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="74644-179">Sim</span><span class="sxs-lookup"><span data-stu-id="74644-179">Yes</span></span> |
| <span data-ttu-id="74644-180">fileName</span><span class="sxs-lookup"><span data-stu-id="74644-180">fileName</span></span> |<span data-ttu-id="74644-181">Especifique o nome do arquivo no **folderPath** se quiser que a tabela se refira a um arquivo específico na pasta.</span><span class="sxs-lookup"><span data-stu-id="74644-181">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="74644-182">Se você não especificar algum valor para essa propriedade, a tabela apontará para todos os arquivos na pasta.</span><span class="sxs-lookup"><span data-stu-id="74644-182">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="74644-183">Quando o fileName não for especificado para um conjunto de dados de saída, o nome do arquivo gerado será no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="74644-183">When fileName is not specified for an output dataset, the name of the generated file would be in the following this format:</span></span> <br/><br/><span data-ttu-id="74644-184">Data<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="74644-184">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="74644-185">Não</span><span class="sxs-lookup"><span data-stu-id="74644-185">No</span></span> |
| <span data-ttu-id="74644-186">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="74644-186">partitionedBy</span></span> |<span data-ttu-id="74644-187">partitionedBy pode usado para especificar um filename, folderPath dinâmico para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="74644-187">partitionedBy can be used to specify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="74644-188">Exemplo: folderPath parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="74644-188">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="74644-189">Não</span><span class="sxs-lookup"><span data-stu-id="74644-189">No</span></span> |
| <span data-ttu-id="74644-190">formato</span><span class="sxs-lookup"><span data-stu-id="74644-190">format</span></span> | <span data-ttu-id="74644-191">Há suporte para os seguintes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="74644-191">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="74644-192">Defina a propriedade **type** sob formato como um desses valores.</span><span class="sxs-lookup"><span data-stu-id="74644-192">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="74644-193">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="74644-193">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="74644-194">Se você quiser **copiar arquivos no estado em que se encontram** entre repositórios baseados em arquivo (cópia binária), ignore a seção de formato nas duas definições de conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="74644-194">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="74644-195">Não</span><span class="sxs-lookup"><span data-stu-id="74644-195">No</span></span> |
| <span data-ttu-id="74644-196">compactação</span><span class="sxs-lookup"><span data-stu-id="74644-196">compression</span></span> | <span data-ttu-id="74644-197">Especifique o tipo e o nível de compactação para os dados.</span><span class="sxs-lookup"><span data-stu-id="74644-197">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="74644-198">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="74644-198">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="74644-199">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="74644-199">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="74644-200">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="74644-200">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="74644-201">Não</span><span class="sxs-lookup"><span data-stu-id="74644-201">No</span></span> |

> [!NOTE]
> <span data-ttu-id="74644-202">filename e fileFilter não podem ser usados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="74644-202">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="74644-203">Usando a propriedade partionedBy</span><span class="sxs-lookup"><span data-stu-id="74644-203">Using partionedBy property</span></span>
<span data-ttu-id="74644-204">Conforme mencionado na seção anterior, você pode especificar um nome de arquivo e um folderPath dinâmico para dados de série temporal com a propriedade **partitionedBy**, [funções do Data Factory e as variáveis do sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="74644-204">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="74644-205">Confira os artigos [Criando conjuntos de dados](data-factory-create-datasets.md), [Agendamento e execução](data-factory-scheduling-and-execution.md) e [Criando pipelines](data-factory-create-pipelines.md) para saber mais sobre conjuntos de dados de série temporal, agendamentos e fatias.</span><span class="sxs-lookup"><span data-stu-id="74644-205">To learn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="74644-206">Exemplo 1:</span><span class="sxs-lookup"><span data-stu-id="74644-206">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="74644-207">Nesse exemplo, {Slice} é substituído pelo valor da variável de sistema SliceStart do Data Factory no formato (AAAAMMDDHH) especificado.</span><span class="sxs-lookup"><span data-stu-id="74644-207">In this example {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="74644-208">O SliceStart refere-se à hora de início da fatia.</span><span class="sxs-lookup"><span data-stu-id="74644-208">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="74644-209">O folderPath é diferente para cada fatia.</span><span class="sxs-lookup"><span data-stu-id="74644-209">The folderPath is different for each slice.</span></span> <span data-ttu-id="74644-210">Por exemplo: wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="74644-210">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="74644-211">Exemplo 2:</span><span class="sxs-lookup"><span data-stu-id="74644-211">Sample 2:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="74644-212">Neste exemplo, ano, mês, dia e hora do SliceStart são extraídos em variáveis separadas que são usadas pelas propriedades folderPath e fileName.</span><span class="sxs-lookup"><span data-stu-id="74644-212">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="74644-213">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="74644-213">Copy activity properties</span></span>
<span data-ttu-id="74644-214">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="74644-214">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="74644-215">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="74644-215">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="74644-216">Por outro lado, as propriedades disponíveis na seção typeProperties da atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="74644-216">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="74644-217">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="74644-217">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="74644-218">Para a Atividade de Cópia quando a fonte for do tipo **FileSystemSource** , as propriedades a seguir estarão disponíveis na seção typeProperties:</span><span class="sxs-lookup"><span data-stu-id="74644-218">For Copy Activity, when source is of type **FileSystemSource** the following properties are available in typeProperties section:</span></span>

<span data-ttu-id="74644-219">**FileSystemSource** suporta as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="74644-219">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="74644-220">Propriedade</span><span class="sxs-lookup"><span data-stu-id="74644-220">Property</span></span> | <span data-ttu-id="74644-221">Descrição</span><span class="sxs-lookup"><span data-stu-id="74644-221">Description</span></span> | <span data-ttu-id="74644-222">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="74644-222">Allowed values</span></span> | <span data-ttu-id="74644-223">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="74644-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="74644-224">recursiva</span><span class="sxs-lookup"><span data-stu-id="74644-224">recursive</span></span> |<span data-ttu-id="74644-225">Indica se os dados são lidos recursivamente a partir das subpastas ou somente da pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="74644-225">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="74644-226">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="74644-226">True, False (default)</span></span> |<span data-ttu-id="74644-227">Não</span><span class="sxs-lookup"><span data-stu-id="74644-227">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="74644-228">Formatos de arquivo e de compactação com suporte</span><span class="sxs-lookup"><span data-stu-id="74644-228">Supported file and compression formats</span></span>
<span data-ttu-id="74644-229">Consulte o artigo [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="74644-229">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-to-azure-blob"></a><span data-ttu-id="74644-230">Exemplo de JSON: copiar dados de um HDFS local para um Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="74644-230">JSON example: Copy data from on-premises HDFS to Azure Blob</span></span>
<span data-ttu-id="74644-231">Este exemplo mostra como copiar dados de um HDFS local para o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="74644-231">This sample shows how to copy data from an on-premises HDFS to Azure Blob Storage.</span></span> <span data-ttu-id="74644-232">No entanto, os dados podem ser copiados **diretamente** para qualquer uma das fontes declaradas [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a atividade de cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="74644-232">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="74644-233">O exemplo fornece definições de JSON para as entidades de Data Factory a seguir.</span><span class="sxs-lookup"><span data-stu-id="74644-233">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="74644-234">Você pode usar essas definições para criar um pipeline para copiar dados do HDFS para um Armazenamento de Blobs do Azure usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou ainda o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="74644-234">You can use these definitions to create a pipeline to copy data from HDFS to Azure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="74644-235">Um serviço vinculado do tipo [OnPremisesHdfs](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="74644-235">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="74644-236">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="74644-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="74644-237">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="74644-237">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="74644-238">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="74644-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="74644-239">Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="74644-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="74644-240">O exemplo copia dados de um HDFS local para o blob do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="74644-240">The sample copies data from an on-premises HDFS to an Azure blob every hour.</span></span> <span data-ttu-id="74644-241">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="74644-241">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="74644-242">Como uma primeira etapa, configure o gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="74644-242">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="74644-243">As instruções estão no artigo [Mover dados entre fontes locais e a nuvem](data-factory-move-data-between-onprem-and-cloud.md) .</span><span class="sxs-lookup"><span data-stu-id="74644-243">The instructions in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="74644-244">**Serviço vinculado ao HDFS:** Esse exemplo usa a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="74644-244">**HDFS linked service:** This example uses the Windows authentication.</span></span> <span data-ttu-id="74644-245">Confira a seção [Serviço vinculado ao HDFS](#linked-service-properties) para diferentes tipos de autenticação que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="74644-245">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="74644-246">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="74644-246">**Azure Storage linked service:**</span></span>

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="74644-247">**Conjunto de dados de entrada do HDFS:** Esse conjunto de dados refere-se à pasta DataTransfer/UnitTest/ do HDFS.</span><span class="sxs-lookup"><span data-stu-id="74644-247">**HDFS input dataset:** This dataset refers to the HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="74644-248">O pipeline copia todos os arquivos dessa pasta para o destino.</span><span class="sxs-lookup"><span data-stu-id="74644-248">The pipeline copies all the files in this folder to the destination.</span></span>

<span data-ttu-id="74644-249">Configurar “external”: “true” informa ao serviço Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="74644-249">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

<span data-ttu-id="74644-250">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="74644-250">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="74644-251">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="74644-251">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="74644-252">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="74644-252">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="74644-253">O caminho da pasta usa as partes ano, mês, dia e horas da hora de início.</span><span class="sxs-lookup"><span data-stu-id="74644-253">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="74644-254">**Uma atividade de cópia em um pipeline com origem de Sistema de Arquivos e coletor Blob:**</span><span class="sxs-lookup"><span data-stu-id="74644-254">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="74644-255">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="74644-255">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="74644-256">Na definição JSON do pipeline, o tipo **source** está definido como **FileSystemSource** e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="74644-256">In the pipeline JSON definition, the **source** type is set to **FileSystemSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="74644-257">A consulta SQL especificada para a propriedade **query** seleciona os dados na última hora para copiar.</span><span class="sxs-lookup"><span data-stu-id="74644-257">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="74644-258">Usar a autenticação Kerberos para o conector HDFS</span><span class="sxs-lookup"><span data-stu-id="74644-258">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="74644-259">Há duas opções para configurar o ambiente local para usar a autenticação Kerberos no conector HDFS.</span><span class="sxs-lookup"><span data-stu-id="74644-259">There are two options to set up the on-premises environment so as to use Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="74644-260">Você pode escolher a que melhor se adapta ao seu caso.</span><span class="sxs-lookup"><span data-stu-id="74644-260">You can choose the one better fits your case.</span></span>
* <span data-ttu-id="74644-261">Opção 1: [Fazer com que o computador do gateway ingresse no realm Kerberos](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="74644-261">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="74644-262">Opção 2: [habilitar a confiança mútua entre o domínio do Windows e o realm Kerberos](#kerberos-mutual-trust)</span><span class="sxs-lookup"><span data-stu-id="74644-262">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <span data-ttu-id="74644-263"><a name="kerberos-join-realm"></a>Opção 1: Fazer com que o computador do gateway ingresse no realm Kerberos</span><span class="sxs-lookup"><span data-stu-id="74644-263"><a name="kerberos-join-realm"></a>Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="74644-264">Requisito:</span><span class="sxs-lookup"><span data-stu-id="74644-264">Requirement:</span></span>

* <span data-ttu-id="74644-265">O computador do gateway precisa unir-se ao realm Kerberos e não pode ingressar em nenhum domínio do Windows.</span><span class="sxs-lookup"><span data-stu-id="74644-265">The gateway machine needs to join the Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-to-configure"></a><span data-ttu-id="74644-266">Como configurar:</span><span class="sxs-lookup"><span data-stu-id="74644-266">How to configure:</span></span>

<span data-ttu-id="74644-267">**No computador do gateway:**</span><span class="sxs-lookup"><span data-stu-id="74644-267">**On gateway machine:**</span></span>

1.  <span data-ttu-id="74644-268">Execute o utilitário **Ksetup** para configurar o servidor e o realm KDC Kerberos.</span><span class="sxs-lookup"><span data-stu-id="74644-268">Run the **Ksetup** utility to configure the Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="74644-269">O computador deve ser configurado como um membro de um grupo de trabalho, uma vez que um realm Kerberos é diferente de um domínio do Windows.</span><span class="sxs-lookup"><span data-stu-id="74644-269">The machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="74644-270">Para isso, defina o realm Kerberos e adicione um servidor KDC como se segue.</span><span class="sxs-lookup"><span data-stu-id="74644-270">This can be achieved by setting the Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="74644-271">Substitua *REALM.COM* pelo seu respectivo realm, conforme a necessidade.</span><span class="sxs-lookup"><span data-stu-id="74644-271">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="74644-272">**Reinicie** o computador depois de executar esses 2 comandos.</span><span class="sxs-lookup"><span data-stu-id="74644-272">**Restart** the machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="74644-273">Verifique a configuração com o comando **Ksetup**.</span><span class="sxs-lookup"><span data-stu-id="74644-273">Verify the configuration with **Ksetup** command.</span></span> <span data-ttu-id="74644-274">A saída deverá ser como a seguinte:</span><span class="sxs-lookup"><span data-stu-id="74644-274">The output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="74644-275">**No Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="74644-275">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="74644-276">Configure o conector HDFS usando a **autenticação do Windows** com o nome da entidade de segurança e a senha Kerberos para se conectar à fonte de dados HDFS.</span><span class="sxs-lookup"><span data-stu-id="74644-276">Configure the HDFS connector using **Windows authentication** together with your Kerberos principal name and password to connect to the HDFS data source.</span></span> <span data-ttu-id="74644-277">Verifique a seção de [propriedades do Serviço Vinculado HDFS](#linked-service-properties) nos detalhes da configuração.</span><span class="sxs-lookup"><span data-stu-id="74644-277">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <span data-ttu-id="74644-278"><a name="kerberos-mutual-trust"></a>Opção 2: habilitar a confiança mútua entre o domínio do Windows e o realm Kerberos</span><span class="sxs-lookup"><span data-stu-id="74644-278"><a name="kerberos-mutual-trust"></a>Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="74644-279">Requisito:</span><span class="sxs-lookup"><span data-stu-id="74644-279">Requirement:</span></span>
*   <span data-ttu-id="74644-280">O computador do gateway deve ingressar em um domínio do Windows.</span><span class="sxs-lookup"><span data-stu-id="74644-280">The gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="74644-281">Você precisa de permissão para atualizar as configurações do controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="74644-281">You need permission to update the domain controller's settings.</span></span>

#### <a name="how-to-configure"></a><span data-ttu-id="74644-282">Como configurar:</span><span class="sxs-lookup"><span data-stu-id="74644-282">How to configure:</span></span>

> [!NOTE]
> <span data-ttu-id="74644-283">Substitua REALM.COM e AD.COM no tutorial a seguir pelo seu próprio realm e controlador de domínio conforme a necessidade.</span><span class="sxs-lookup"><span data-stu-id="74644-283">Replace REALM.COM and AD.COM in the following tutorial with your own respective realm and domain controller as needed.</span></span>

<span data-ttu-id="74644-284">**No servidor KDC:**</span><span class="sxs-lookup"><span data-stu-id="74644-284">**On KDC server:**</span></span>

1.  <span data-ttu-id="74644-285">Edite a configuração do KDC no arquivo **krb5.conf** para permitir que o Domínio do Windows de confiança do KDC se refira ao modelo de configuração a seguir.</span><span class="sxs-lookup"><span data-stu-id="74644-285">Edit the KDC configuration in **krb5.conf** file to let KDC trust Windows Domain referring to the following configuration template.</span></span> <span data-ttu-id="74644-286">Por padrão, a configuração está localizada em **/etc/krb5.conf**.</span><span class="sxs-lookup"><span data-stu-id="74644-286">By default, the configuration is located at **/etc/krb5.conf**.</span></span>

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  <span data-ttu-id="74644-287">**Reinicie** o serviço KDC após a configuração.</span><span class="sxs-lookup"><span data-stu-id="74644-287">**Restart** the KDC service after configuration.</span></span>

2.  <span data-ttu-id="74644-288">Prepare uma entidade de segurança chamada **krbtgt/REALM.COM@AD.COM** no servidor KDC com o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="74644-288">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with the following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="74644-289">No arquivo de configuração de serviço HDFS **hadoop.security.auth_to_local**, adicione `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span><span class="sxs-lookup"><span data-stu-id="74644-289">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="74644-290">**No controlador de domínio:**</span><span class="sxs-lookup"><span data-stu-id="74644-290">**On domain controller:**</span></span>

1.  <span data-ttu-id="74644-291">Execute os comandos **Ksetup** a seguir para adicionar uma entrada de realm:</span><span class="sxs-lookup"><span data-stu-id="74644-291">Run the following **Ksetup** commands to add a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="74644-292">Estabeleça uma relação de confiança do Domínio do Windows ao Realm Kerberos.</span><span class="sxs-lookup"><span data-stu-id="74644-292">Establish trust from Windows Domain to Kerberos Realm.</span></span> <span data-ttu-id="74644-293">[password] é a senha da entidade de segurança **krbtgt/REALM.COM@AD.COM**.</span><span class="sxs-lookup"><span data-stu-id="74644-293">[password] is the password for the principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="74644-294">Selecione o algoritmo de criptografia usado no Kerberos.</span><span class="sxs-lookup"><span data-stu-id="74644-294">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="74644-295">Vá para Gerenciador de Servidores > Gerenciamento de Política de Grupo > Domínio > Objetos de Política de Grupo > Política de Domínio Padrão ou Ativa e Editar.</span><span class="sxs-lookup"><span data-stu-id="74644-295">Go to Server Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="74644-296">Na janela pop-up **Editor de Gerenciamento de Política de Grupo**, vá para Configuração do Computador > Políticas > Configurações do Windows > Configurações de Segurança > Políticas Locais > Opções de Segurança e configure **Segurança da rede: Configurar tipos de criptografia permitidos para Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="74644-296">In the **Group Policy Management Editor** popup window, go to Computer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="74644-297">Selecione o algoritmo de criptografia que você deseja usar ao se conectar ao KDC.</span><span class="sxs-lookup"><span data-stu-id="74644-297">Select the encryption algorithm you want to use when connect to KDC.</span></span> <span data-ttu-id="74644-298">Normalmente, você pode simplesmente selecionar todas as opções.</span><span class="sxs-lookup"><span data-stu-id="74644-298">Commonly, you can simply select all the options.</span></span>

        ![Configuração dos tipos de criptografia para Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="74644-300">Use o comando **Ksetup** para especificar o algoritmo de criptografia a ser usado no REALM específico.</span><span class="sxs-lookup"><span data-stu-id="74644-300">Use **Ksetup** command to specify the encryption algorithm to be used on the specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="74644-301">Crie o mapeamento entre a conta de domínio e a entidade de segurança Kerberos para usar a entidade de segurança Kerberos no Domínio do Windows.</span><span class="sxs-lookup"><span data-stu-id="74644-301">Create the mapping between the domain account and Kerberos principal, in order to use Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="74644-302">Inicie as Ferramentas administrativas > **Usuários e Computadores do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="74644-302">Start the Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="74644-303">Configure recursos avançados clicando em **Exibir** > **Recursos Avançados**.</span><span class="sxs-lookup"><span data-stu-id="74644-303">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="74644-304">Localize a conta para a qual deseja criar mapeamentos e clique com o botão direito do mouse para exibir **Mapeamentos de Nome** > clique na guia **Nomes Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="74644-304">Locate the account to which you want to create mappings, and right-click to view **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="74644-305">Adicione uma entidade de segurança do realm.</span><span class="sxs-lookup"><span data-stu-id="74644-305">Add a principal from the realm.</span></span>

        ![Mapear identidade de segurança](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="74644-307">**No computador do gateway:**</span><span class="sxs-lookup"><span data-stu-id="74644-307">**On gateway machine:**</span></span>

* <span data-ttu-id="74644-308">Execute os comandos **Ksetup** a seguir para adicionar uma entrada de realm.</span><span class="sxs-lookup"><span data-stu-id="74644-308">Run the following **Ksetup** commands to add a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="74644-309">**No Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="74644-309">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="74644-310">Configure o conector HDFS usando a **autenticação do Windows** com a Conta de Domínio ou a Entidade de Segurança Kerberos para se conectar à fonte de dados HDFS.</span><span class="sxs-lookup"><span data-stu-id="74644-310">Configure the HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal to connect to the HDFS data source.</span></span> <span data-ttu-id="74644-311">Verifique a seção de [propriedades do Serviço Vinculado HDFS](#linked-service-properties) nos detalhes da configuração.</span><span class="sxs-lookup"><span data-stu-id="74644-311">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> <span data-ttu-id="74644-312">Para mapear colunas de conjunto de dados de origem para colunas do conjunto de dados de coletor, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapeamento de colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="74644-312">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="performance-and-tuning"></a><span data-ttu-id="74644-313">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="74644-313">Performance and Tuning</span></span>
<span data-ttu-id="74644-314">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="74644-314">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
