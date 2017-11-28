---
title: Copiar dados bidirecionalmente em um sistema de arquivos usando o Azure Data Factory | Microsoft Docs
description: Saiba como copiar dados bidirecionalmente em um sistema de arquivos local usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ce19f1ae-358e-4ffc-8a80-d802505c9c84
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 52305e54f539de6aba2ba9cc856a09e04d608ded
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="copy-data-to-and-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="ba499-103">Copiar dados bidirecionalmente em um sistema de arquivos local usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ba499-103">Copy data to and from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="ba499-104">Esse artigo explica como usar a Atividade de Cópia no Azure Data Factory para copiar dados de/para um sistema de arquivos local.</span><span class="sxs-lookup"><span data-stu-id="ba499-104">This article explains how to use the Copy Activity in Azure Data Factory to copy data to/from an on-premises file system.</span></span> <span data-ttu-id="ba499-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="ba499-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="ba499-106">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="ba499-106">Supported scenarios</span></span>
<span data-ttu-id="ba499-107">Você pode copiar dados **de um sistema de arquivos local** para os seguintes armazenamentos de dados:</span><span class="sxs-lookup"><span data-stu-id="ba499-107">You can copy data **from an on-premises file system** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="ba499-108">Você pode copiar dados dos seguintes armazenamentos de dados **para um sistema de arquivos local**:</span><span class="sxs-lookup"><span data-stu-id="ba499-108">You can copy data from the following data stores **to an on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="ba499-109">A Atividade de Cópia não exclui o arquivo de origem depois que ele é copiado com êxito para o destino.</span><span class="sxs-lookup"><span data-stu-id="ba499-109">Copy Activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="ba499-110">Se precisar excluir o arquivo de origem após uma cópia bem-sucedida, crie uma atividade personalizada para excluir o arquivo e use a atividade no pipeline.</span><span class="sxs-lookup"><span data-stu-id="ba499-110">If you need to delete the source file after a successful copy, create a custom activity to delete the file and use the activity in the pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="ba499-111">Habilitando a conectividade</span><span class="sxs-lookup"><span data-stu-id="ba499-111">Enabling connectivity</span></span>
<span data-ttu-id="ba499-112">O Data Factory dá suporte à conexão de e para um sistema de arquivos local por meio do **Gateway de Gerenciamento de Dados**.</span><span class="sxs-lookup"><span data-stu-id="ba499-112">Data Factory supports connecting to and from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="ba499-113">Você deve instalar o Gateway de Gerenciamento de Dados no seu ambiente local para o serviço Data Factory para se conectar a qualquer armazenamento de dados local com suporte, incluindo o sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="ba499-113">You must install the Data Management Gateway in your on-premises environment for the Data Factory service to connect to any supported on-premises data store including file system.</span></span> <span data-ttu-id="ba499-114">Para saber mais sobre o Gateway de Gerenciamento de Dados e para obter instruções passo a passo sobre como configurar o gateway, confira [Mover dados entre fontes locais e a nuvem com o Gateway de Gerenciamento de Dados](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="ba499-114">To learn about Data Management Gateway and for step-by-step instructions on setting up the gateway, see [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="ba499-115">Com exceção do Gateway de Gerenciamento de Dados, não é necessário instalar nenhum outro binário para se comunicar de e para o sistema de arquivos local.</span><span class="sxs-lookup"><span data-stu-id="ba499-115">Apart from Data Management Gateway, no other binary files need to be installed to communicate to and from an on-premises file system.</span></span> <span data-ttu-id="ba499-116">Você deve instalar e usar o Gateway de gerenciamento de dados, mesmo se o sistema de arquivos estiver em uma VM IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba499-116">You must install and use the Data Management Gateway even if the file system is in Azure IaaS VM.</span></span> <span data-ttu-id="ba499-117">Para obter informações detalhadas sobre o gateway, consulte [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="ba499-117">For detailed information about the gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="ba499-118">Para usar um compartilhamento de arquivos do Linux, instale o [Samba](https://www.samba.org/) no servidor Linux e instale o Gateway de Gerenciamento de Dados em um servidor Windows.</span><span class="sxs-lookup"><span data-stu-id="ba499-118">To use a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="ba499-119">Não há suporte para a instalação do Gateway de Gerenciamento de Dados em um servidor Linux.</span><span class="sxs-lookup"><span data-stu-id="ba499-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ba499-120">Introdução</span><span class="sxs-lookup"><span data-stu-id="ba499-120">Getting started</span></span>
<span data-ttu-id="ba499-121">Você pode criar um pipeline com uma atividade de cópia que mova dados bidirecionalmente de/para um sistema de arquivos usando ferramentas/APIs diferentes.</span><span class="sxs-lookup"><span data-stu-id="ba499-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="ba499-122">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="ba499-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="ba499-123">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="ba499-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="ba499-124">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="ba499-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ba499-125">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="ba499-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="ba499-126">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="ba499-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="ba499-127">Criar uma **data factory**.</span><span class="sxs-lookup"><span data-stu-id="ba499-127">Create a **data factory**.</span></span> <span data-ttu-id="ba499-128">Um data factory pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="ba499-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="ba499-129">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="ba499-129">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="ba499-130">Por exemplo, se você estiver copiando dados de um Armazenamento de Blobs do Azure para um sistema de arquivos local, crie dois serviços vinculados para vincular seu sistema de arquivos local e a Conta de Armazenamento do Azure para seu data factory.</span><span class="sxs-lookup"><span data-stu-id="ba499-130">For example, if you are copying data from an Azure blob storage to an on-premises file system, you create two linked services to link your on-premises file system and Azure storage account to your data factory.</span></span> <span data-ttu-id="ba499-131">Para propriedades do serviço vinculado que são específicas para um sistema de arquivos local, consulte a seção de [propriedades do serviço vinculado](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ba499-131">For linked service properties that are specific to an on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="ba499-132">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="ba499-132">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="ba499-133">No exemplo mencionado na última etapa, você cria um conjunto de dados para especificar o contêiner de blobs e a pasta que contém os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="ba499-133">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="ba499-134">E você cria outro conjunto de dados para especificar o nome do arquivo e da pasta (opcional) no sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="ba499-134">And, you create another dataset to specify the folder and file name (optional) in your file system.</span></span> <span data-ttu-id="ba499-135">Para propriedades de conjunto de dados específicas do sistema de arquivos local, consulte a seção de [propriedades do conjunto de dados](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ba499-135">For dataset properties that are specific to on-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="ba499-136">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="ba499-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="ba499-137">No exemplo mencionado anteriormente, você usa BlobSource como fonte e FileSystemSink como coletor para a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="ba499-137">In the example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for the copy activity.</span></span> <span data-ttu-id="ba499-138">De modo similar, se estiver copiando de um sistema de arquivos local para o Armazenamento de Blobs do Azure, você usará FileSystemSource e BlobSink na atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="ba499-138">Similarly, if you are copying from on-premises file system to Azure Blob Storage, you use FileSystemSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="ba499-139">Para propriedades da atividade de cópia específicas do sistema de arquivos local, consulte a seção de [propriedades da atividade de cópia](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ba499-139">For copy activity properties that are specific to on-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="ba499-140">Para obter detalhes sobre como usar um armazenamento de dados como uma origem ou um coletor, clique no link na seção anterior para o seu armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="ba499-140">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="ba499-141">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="ba499-141">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="ba499-142">Ao usar ferramentas/APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="ba499-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="ba499-143">Para obter exemplos com definições de JSON das entidades do Data Factory usadas para copiar dados de/para um sistema de arquivos, confira a seção [Exemplos de JSON](#json-examples-for-copying-data-to-and-from-file-system) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="ba499-143">For samples with JSON definitions for Data Factory entities that are used to copy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="ba499-144">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas do sistema de arquivos:</span><span class="sxs-lookup"><span data-stu-id="ba499-144">The following sections provide details about JSON properties that are used to define Data Factory entities specific to file system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="ba499-145">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ba499-145">Linked service properties</span></span>
<span data-ttu-id="ba499-146">Você pode vincular um sistema de arquivos local ao Azure Data Factory com o serviço vinculado do **Servidor de Arquivos Local**.</span><span class="sxs-lookup"><span data-stu-id="ba499-146">You can link an on-premises file system to an Azure data factory with the **On-Premises File Server** linked service.</span></span> <span data-ttu-id="ba499-147">A tabela a seguir fornece descrições dos elementos JSON específicos para o serviço vinculado do Servidor de Arquivos Local.</span><span class="sxs-lookup"><span data-stu-id="ba499-147">The following table provides descriptions for JSON elements that are specific to the On-Premises File Server linked service.</span></span>

| <span data-ttu-id="ba499-148">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ba499-148">Property</span></span> | <span data-ttu-id="ba499-149">Descrição</span><span class="sxs-lookup"><span data-stu-id="ba499-149">Description</span></span> | <span data-ttu-id="ba499-150">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ba499-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba499-151">type</span><span class="sxs-lookup"><span data-stu-id="ba499-151">type</span></span> |<span data-ttu-id="ba499-152">Verifique se a propriedade de tipo foi definida como **OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="ba499-152">Ensure that the type property is set to **OnPremisesFileServer**.</span></span> |<span data-ttu-id="ba499-153">Sim</span><span class="sxs-lookup"><span data-stu-id="ba499-153">Yes</span></span> |
| <span data-ttu-id="ba499-154">host</span><span class="sxs-lookup"><span data-stu-id="ba499-154">host</span></span> |<span data-ttu-id="ba499-155">Especifica o caminho raiz da pasta que você deseja copiar.</span><span class="sxs-lookup"><span data-stu-id="ba499-155">Specifies the root path of the folder that you want to copy.</span></span> <span data-ttu-id="ba499-156">Use o caractere de escape ‘ \ ’ para caracteres especiais na cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="ba499-156">Use the escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="ba499-157">Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="ba499-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="ba499-158">Sim</span><span class="sxs-lookup"><span data-stu-id="ba499-158">Yes</span></span> |
| <span data-ttu-id="ba499-159">userid</span><span class="sxs-lookup"><span data-stu-id="ba499-159">userid</span></span> |<span data-ttu-id="ba499-160">Especifique a ID do usuário que tem acesso ao servidor.</span><span class="sxs-lookup"><span data-stu-id="ba499-160">Specify the ID of the user who has access to the server.</span></span> |<span data-ttu-id="ba499-161">Não (se você escolher encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="ba499-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="ba499-162">Senha</span><span class="sxs-lookup"><span data-stu-id="ba499-162">password</span></span> |<span data-ttu-id="ba499-163">Especifique a senha para o usuário (userid).</span><span class="sxs-lookup"><span data-stu-id="ba499-163">Specify the password for the user (userid).</span></span> |<span data-ttu-id="ba499-164">Não (se você escolher encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="ba499-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="ba499-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="ba499-165">encryptedCredential</span></span> |<span data-ttu-id="ba499-166">Especifique as credenciais criptografadas que você pode obter executando o cmdlet New-AzureRmDataFactoryEncryptValue.</span><span class="sxs-lookup"><span data-stu-id="ba499-166">Specify the encrypted credentials that you can get by running the New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="ba499-167">Não (se você optar por especificar userid e password em texto sem formatação)</span><span class="sxs-lookup"><span data-stu-id="ba499-167">No (if you choose to specify userid and password in plain text)</span></span> |
| <span data-ttu-id="ba499-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ba499-168">gatewayName</span></span> |<span data-ttu-id="ba499-169">Especifica o nome do gateway que o Data Factory deve usar para se conectar ao servidor de arquivos local.</span><span class="sxs-lookup"><span data-stu-id="ba499-169">Specifies the name of the gateway that Data Factory should use to connect to the on-premises file server.</span></span> |<span data-ttu-id="ba499-170">Sim</span><span class="sxs-lookup"><span data-stu-id="ba499-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="ba499-171">Definições de conjunto de dados e serviço vinculado de exemplo</span><span class="sxs-lookup"><span data-stu-id="ba499-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="ba499-172">Cenário</span><span class="sxs-lookup"><span data-stu-id="ba499-172">Scenario</span></span> | <span data-ttu-id="ba499-173">Host em definição de serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="ba499-173">Host in linked service definition</span></span> | <span data-ttu-id="ba499-174">folderPath em definição de conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ba499-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba499-175">Pasta local no computador do Gateway de Gerenciamento de Dados </span><span class="sxs-lookup"><span data-stu-id="ba499-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="ba499-176">Exemplos: D:\\\* ou D:\pasta\subpasta\\*</span><span class="sxs-lookup"><span data-stu-id="ba499-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="ba499-177">D:\\\\ (para o Gateway de Gerenciamento de Dados 2.0 e versões posteriores)</span><span class="sxs-lookup"><span data-stu-id="ba499-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="ba499-178">localhost (para versões anteriores do Gateway de Gerenciamento de Dados 2.0)</span><span class="sxs-lookup"><span data-stu-id="ba499-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="ba499-179">.\\\\ ou pasta\\\\subpasta (para o Gateway de Gerenciamento de Dados 2.0 e versões posteriores)</span><span class="sxs-lookup"><span data-stu-id="ba499-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="ba499-180">D:\\\\ ou D:\\\\pasta\\\\subpasta (para a versão de gateway abaixo de 2.0)</span><span class="sxs-lookup"><span data-stu-id="ba499-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="ba499-181">Pasta compartilhada remota: </span><span class="sxs-lookup"><span data-stu-id="ba499-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="ba499-182">Exemplos: \\\\meuservidor\\compartilhar\\\* ou \\\\meuservidor\\compartilhar\\pasta\\subpasta\\*</span><span class="sxs-lookup"><span data-stu-id="ba499-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="ba499-183">\\\\\\\\meuservidor\\\\compartilhar</span><span class="sxs-lookup"><span data-stu-id="ba499-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="ba499-184">.\\\\ ou pasta\\\\subpasta</span><span class="sxs-lookup"><span data-stu-id="ba499-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="ba499-185">Exemplo: usando username e password em texto sem formatação</span><span class="sxs-lookup"><span data-stu-id="ba499-185">Example: Using username and password in plain text</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="ba499-186">Exemplo: usando encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="ba499-186">Example: Using encryptedcredential</span></span>

```JSON
{
  "Name": " OnPremisesFileServerLinkedService ",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "D:\\",
      "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
      "gatewayName": "mygateway"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="ba499-187">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="ba499-187">Dataset properties</span></span>
<span data-ttu-id="ba499-188">Para obter uma lista completa das seções e propriedades disponíveis para definir os conjuntos de dados, confira [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="ba499-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="ba499-189">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ba499-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="ba499-190">A seção typeProperties é diferente para cada tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="ba499-190">The typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="ba499-191">Ela fornece informações, como o local e o formato dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="ba499-191">It provides information such as the location and format of the data in the data store.</span></span> <span data-ttu-id="ba499-192">A seção typeProperties para o conjunto de dados do tipo **FileShare** tem as propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="ba499-192">The typeProperties section for the dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="ba499-193">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ba499-193">Property</span></span> | <span data-ttu-id="ba499-194">Descrição</span><span class="sxs-lookup"><span data-stu-id="ba499-194">Description</span></span> | <span data-ttu-id="ba499-195">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ba499-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba499-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="ba499-196">folderPath</span></span> |<span data-ttu-id="ba499-197">Especifica o subcaminho para a pasta.</span><span class="sxs-lookup"><span data-stu-id="ba499-197">Specifies the subpath to the folder.</span></span> <span data-ttu-id="ba499-198">Use o caractere de escape ‘\’ para caracteres especiais na cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="ba499-198">Use the escape character ‘\’ for special characters in the string.</span></span> <span data-ttu-id="ba499-199">Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="ba499-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="ba499-200">Você pode combinar essa propriedade com **partitionBy** para ter caminhos de pastas com base na fatia de data/hora de início/término.</span><span class="sxs-lookup"><span data-stu-id="ba499-200">You can combine this property with **partitionBy** to have folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="ba499-201">Sim</span><span class="sxs-lookup"><span data-stu-id="ba499-201">Yes</span></span> |
| <span data-ttu-id="ba499-202">fileName</span><span class="sxs-lookup"><span data-stu-id="ba499-202">fileName</span></span> |<span data-ttu-id="ba499-203">Especifique o nome do arquivo no **folderPath** se quiser que a tabela se refira a um arquivo específico na pasta.</span><span class="sxs-lookup"><span data-stu-id="ba499-203">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="ba499-204">Se você não especificar algum valor para essa propriedade, a tabela apontará para todos os arquivos na pasta.</span><span class="sxs-lookup"><span data-stu-id="ba499-204">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="ba499-205">Quando **fileName** não for especificado para um conjunto de dados de saída e **preserveHierarchy** não for especificado em um coletor de atividade, o nome do arquivo gerado está no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="ba499-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="ba499-206">`Data.<Guid>.txt` (Exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="ba499-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="ba499-207">Não</span><span class="sxs-lookup"><span data-stu-id="ba499-207">No</span></span> |
| <span data-ttu-id="ba499-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="ba499-208">fileFilter</span></span> |<span data-ttu-id="ba499-209">Especifique um filtro a ser usado para selecionar um subconjunto de arquivos no folderPath em vez de todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="ba499-209">Specify a filter to be used to select a subset of files in the folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="ba499-210">Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).</span><span class="sxs-lookup"><span data-stu-id="ba499-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="ba499-211">Exemplo 1: "fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="ba499-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="ba499-212">Exemplo 2: "fileFilter": 2014-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="ba499-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="ba499-213">Observe que fileFilter é aplicável a um conjunto de dados FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="ba499-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="ba499-214">Não</span><span class="sxs-lookup"><span data-stu-id="ba499-214">No</span></span> |
| <span data-ttu-id="ba499-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="ba499-215">partitionedBy</span></span> |<span data-ttu-id="ba499-216">Você pode usar partitionedBy para especificar um folderPath/fileName dinâmico para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="ba499-216">You can use partitionedBy to specify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="ba499-217">Um exemplo é folderPath parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="ba499-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="ba499-218">Não</span><span class="sxs-lookup"><span data-stu-id="ba499-218">No</span></span> |
| <span data-ttu-id="ba499-219">formato</span><span class="sxs-lookup"><span data-stu-id="ba499-219">format</span></span> | <span data-ttu-id="ba499-220">Há suporte para os seguintes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="ba499-220">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="ba499-221">Defina a propriedade **type** sob formato como um desses valores.</span><span class="sxs-lookup"><span data-stu-id="ba499-221">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="ba499-222">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="ba499-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="ba499-223">Se você quiser **copiar arquivos no estado em que se encontram** entre repositórios baseados em arquivo (cópia binária), ignore a seção de formato nas duas definições de conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="ba499-223">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="ba499-224">Não</span><span class="sxs-lookup"><span data-stu-id="ba499-224">No</span></span> |
| <span data-ttu-id="ba499-225">compactação</span><span class="sxs-lookup"><span data-stu-id="ba499-225">compression</span></span> | <span data-ttu-id="ba499-226">Especifique o tipo e o nível de compactação para os dados.</span><span class="sxs-lookup"><span data-stu-id="ba499-226">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="ba499-227">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="ba499-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="ba499-228">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="ba499-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="ba499-229">confira [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="ba499-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="ba499-230">Não</span><span class="sxs-lookup"><span data-stu-id="ba499-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="ba499-231">Você não pode usar fileName e fileFilter simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="ba499-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="ba499-232">Usando a propriedade partitionedBy</span><span class="sxs-lookup"><span data-stu-id="ba499-232">Using partitionedBy property</span></span>
<span data-ttu-id="ba499-233">Conforme mencionado na seção anterior, você pode especificar um nome de arquivo e um folderPath dinâmico para dados de série temporal com a propriedade **partitionedBy**, [funções do Data Factory e as variáveis do sistema](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="ba499-233">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="ba499-234">Confira [Criando conjuntos de dados](data-factory-create-datasets.md), [Agendamento e execução](data-factory-scheduling-and-execution.md) e [Criando pipelines](data-factory-create-pipelines.md) para saber mais detalhes sobre conjuntos de dados de série temporal, agendamentos e fatias.</span><span class="sxs-lookup"><span data-stu-id="ba499-234">To understand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="ba499-235">Exemplo 1:</span><span class="sxs-lookup"><span data-stu-id="ba499-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="ba499-236">Neste exemplo, {Slice} é substituído pelo valor da variável de sistema SliceStart do Data Factory no formato (AAAAMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="ba499-236">In this example, {Slice} is replaced with the value of the Data Factory system variable SliceStart in the format (YYYYMMDDHH).</span></span> <span data-ttu-id="ba499-237">SliceStart se refere à hora de início da fatia.</span><span class="sxs-lookup"><span data-stu-id="ba499-237">SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="ba499-238">O folderPath é diferente para cada fatia.</span><span class="sxs-lookup"><span data-stu-id="ba499-238">The folderPath is different for each slice.</span></span> <span data-ttu-id="ba499-239">Por exemplo: wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="ba499-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="ba499-240">Exemplo 2:</span><span class="sxs-lookup"><span data-stu-id="ba499-240">Sample 2:</span></span>

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

<span data-ttu-id="ba499-241">Neste exemplo, ano, mês, dia e hora do SliceStart são extraídos em variáveis separadas, que são usadas pelas propriedades folderPath e fileName.</span><span class="sxs-lookup"><span data-stu-id="ba499-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that the folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="ba499-242">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="ba499-242">Copy activity properties</span></span>
<span data-ttu-id="ba499-243">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="ba499-243">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ba499-244">As propriedades, como nome, descrição, conjuntos de dados de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="ba499-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="ba499-245">Por outro lado, as propriedades disponíveis na seção **typeProperties** da atividade variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="ba499-245">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span>

<span data-ttu-id="ba499-246">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="ba499-246">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="ba499-247">Se você estiver movendo dados de um sistema de arquivos local, defina o tipo de origem na atividade de cópia como **FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="ba499-247">If you are moving data from an on-premises file system, you set the source type in the copy activity to **FileSystemSource**.</span></span> <span data-ttu-id="ba499-248">De modo similar, se você estiver movendo dados para um sistema de arquivos local, defina o tipo de coletor na atividade de cópia como **FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="ba499-248">Similarly, if you are moving data to an on-premises file system, you set the sink type in the copy activity to **FileSystemSink**.</span></span> <span data-ttu-id="ba499-249">Esta seção fornece uma lista das propriedades às quais FileSystemSource e FileSystemSink dão suporte.</span><span class="sxs-lookup"><span data-stu-id="ba499-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="ba499-250">**FileSystemSource** suporta as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="ba499-250">**FileSystemSource** supports the following properties:</span></span>

| <span data-ttu-id="ba499-251">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ba499-251">Property</span></span> | <span data-ttu-id="ba499-252">Descrição</span><span class="sxs-lookup"><span data-stu-id="ba499-252">Description</span></span> | <span data-ttu-id="ba499-253">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ba499-253">Allowed values</span></span> | <span data-ttu-id="ba499-254">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ba499-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ba499-255">recursiva</span><span class="sxs-lookup"><span data-stu-id="ba499-255">recursive</span></span> |<span data-ttu-id="ba499-256">Indica se os dados são lidos recursivamente das subpastas ou somente da pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="ba499-256">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="ba499-257">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="ba499-257">True, False (default)</span></span> |<span data-ttu-id="ba499-258">Não</span><span class="sxs-lookup"><span data-stu-id="ba499-258">No</span></span> |

<span data-ttu-id="ba499-259">**FileSystemSink** dá suporte às seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="ba499-259">**FileSystemSink** supports the following properties:</span></span>

| <span data-ttu-id="ba499-260">Propriedade</span><span class="sxs-lookup"><span data-stu-id="ba499-260">Property</span></span> | <span data-ttu-id="ba499-261">Descrição</span><span class="sxs-lookup"><span data-stu-id="ba499-261">Description</span></span> | <span data-ttu-id="ba499-262">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="ba499-262">Allowed values</span></span> | <span data-ttu-id="ba499-263">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="ba499-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ba499-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="ba499-264">copyBehavior</span></span> |<span data-ttu-id="ba499-265">Define o comportamento de cópia quando a origem é BlobSource ou FileSystem.</span><span class="sxs-lookup"><span data-stu-id="ba499-265">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="ba499-266">**PreserveHierarchy:** preserva a hierarquia de arquivos na pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="ba499-266">**PreserveHierarchy:** Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="ba499-267">Ou seja, o caminho relativo do arquivo de origem para a pasta de origem é o mesmo que o caminho relativo do arquivo de destino para a pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="ba499-267">That is, the relative path of the source file to the source folder is the same as the relative path of the target file to the target folder.</span></span><br/><br/><span data-ttu-id="ba499-268">**FlattenHierarchy:** todos os arquivos da pasta de origem estarão no primeiro nível da pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="ba499-268">**FlattenHierarchy:** All files from the source folder are created in the first level of target folder.</span></span> <span data-ttu-id="ba499-269">Os arquivos de destino são criados com um nome gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ba499-269">The target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="ba499-270">**MergeFiles**: mescla todos os arquivos da pasta de origem em um arquivo.</span><span class="sxs-lookup"><span data-stu-id="ba499-270">**MergeFiles:** Merges all files from the source folder to one file.</span></span> <span data-ttu-id="ba499-271">Se o nome do arquivo/nome do blob for especificado, o nome do arquivo mesclado será o nome especificado.</span><span class="sxs-lookup"><span data-stu-id="ba499-271">If the file name/blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="ba499-272">Caso contrário, ele será um nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ba499-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="ba499-273">Não</span><span class="sxs-lookup"><span data-stu-id="ba499-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="ba499-274">exemplos de recursive e copyBehavior</span><span class="sxs-lookup"><span data-stu-id="ba499-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="ba499-275">Esta seção descreve o comportamento resultante da operação de cópia para diferentes combinações de valores nas propriedades recursive e copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="ba499-275">This section describes the resulting behavior of the Copy operation for different combinations of values for the recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="ba499-276">valor de recursive</span><span class="sxs-lookup"><span data-stu-id="ba499-276">recursive value</span></span> | <span data-ttu-id="ba499-277">valor de copyBehavior</span><span class="sxs-lookup"><span data-stu-id="ba499-277">copyBehavior value</span></span> | <span data-ttu-id="ba499-278">Comportamento resultante</span><span class="sxs-lookup"><span data-stu-id="ba499-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba499-279">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="ba499-279">true</span></span> |<span data-ttu-id="ba499-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="ba499-280">preserveHierarchy</span></span> |<span data-ttu-id="ba499-281">Para uma pasta de origem Pasta1 com a seguinte estrutura,</span><span class="sxs-lookup"><span data-stu-id="ba499-281">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="ba499-282">Pasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-282">Folder1</span></span><br/><span data-ttu-id="ba499-283">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="ba499-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="ba499-284">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="ba499-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="ba499-285">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="ba499-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="ba499-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="ba499-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="ba499-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="ba499-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="ba499-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="ba499-289">a pasta de destino Pasta1 é criada com a mesma estrutura de origem:</span><span class="sxs-lookup"><span data-stu-id="ba499-289">the target folder Folder1 is created with the same structure as the source:</span></span><br/><br/><span data-ttu-id="ba499-290">Pasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-290">Folder1</span></span><br/><span data-ttu-id="ba499-291">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="ba499-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="ba499-292">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="ba499-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="ba499-293">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="ba499-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="ba499-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="ba499-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="ba499-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="ba499-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="ba499-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="ba499-297">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="ba499-297">true</span></span> |<span data-ttu-id="ba499-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="ba499-298">flattenHierarchy</span></span> |<span data-ttu-id="ba499-299">Para uma pasta de origem Pasta1 com a seguinte estrutura,</span><span class="sxs-lookup"><span data-stu-id="ba499-299">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="ba499-300">Pasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-300">Folder1</span></span><br/><span data-ttu-id="ba499-301">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="ba499-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="ba499-302">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="ba499-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="ba499-303">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="ba499-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="ba499-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="ba499-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="ba499-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="ba499-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="ba499-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="ba499-307">a Pasta1 de destino é criada com a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="ba499-307">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="ba499-308">Pasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-308">Folder1</span></span><br/><span data-ttu-id="ba499-309">&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="ba499-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="ba499-310">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo2</span><span class="sxs-lookup"><span data-stu-id="ba499-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="ba499-311">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo3</span><span class="sxs-lookup"><span data-stu-id="ba499-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="ba499-312">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo4</span><span class="sxs-lookup"><span data-stu-id="ba499-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="ba499-313">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo5</span><span class="sxs-lookup"><span data-stu-id="ba499-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="ba499-314">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="ba499-314">true</span></span> |<span data-ttu-id="ba499-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="ba499-315">mergeFiles</span></span> |<span data-ttu-id="ba499-316">Para uma pasta de origem Pasta1 com a seguinte estrutura,</span><span class="sxs-lookup"><span data-stu-id="ba499-316">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="ba499-317">Pasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-317">Folder1</span></span><br/><span data-ttu-id="ba499-318">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="ba499-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="ba499-319">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="ba499-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="ba499-320">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="ba499-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="ba499-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="ba499-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="ba499-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="ba499-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="ba499-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="ba499-324">a Pasta1 de destino é criada com a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="ba499-324">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="ba499-325">Pasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-325">Folder1</span></span><br/><span data-ttu-id="ba499-326">&nbsp;&nbsp;&nbsp;&nbsp;Os conteúdos de Arquivo1 + Arquivo2 + Arquivo3 + Arquivo4 + Arquivo5 são mesclados em um arquivo com um nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ba499-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="ba499-327">false</span><span class="sxs-lookup"><span data-stu-id="ba499-327">false</span></span> |<span data-ttu-id="ba499-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="ba499-328">preserveHierarchy</span></span> |<span data-ttu-id="ba499-329">Para uma pasta de origem Pasta1 com a seguinte estrutura,</span><span class="sxs-lookup"><span data-stu-id="ba499-329">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="ba499-330">Pasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-330">Folder1</span></span><br/><span data-ttu-id="ba499-331">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="ba499-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="ba499-332">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="ba499-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="ba499-333">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="ba499-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="ba499-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="ba499-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="ba499-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="ba499-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="ba499-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="ba499-337">a pasta de destino Pasta1 é criada com a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="ba499-337">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="ba499-338">Pasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-338">Folder1</span></span><br/><span data-ttu-id="ba499-339">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="ba499-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="ba499-340">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="ba499-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="ba499-341">A Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não é selecionada.</span><span class="sxs-lookup"><span data-stu-id="ba499-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="ba499-342">false</span><span class="sxs-lookup"><span data-stu-id="ba499-342">false</span></span> |<span data-ttu-id="ba499-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="ba499-343">flattenHierarchy</span></span> |<span data-ttu-id="ba499-344">Para uma pasta de origem Pasta1 com a seguinte estrutura,</span><span class="sxs-lookup"><span data-stu-id="ba499-344">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="ba499-345">Pasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-345">Folder1</span></span><br/><span data-ttu-id="ba499-346">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="ba499-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="ba499-347">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="ba499-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="ba499-348">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="ba499-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="ba499-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="ba499-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="ba499-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="ba499-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="ba499-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="ba499-352">a pasta de destino Pasta1 é criada com a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="ba499-352">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="ba499-353">Pasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-353">Folder1</span></span><br/><span data-ttu-id="ba499-354">&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="ba499-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="ba499-355">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo2</span><span class="sxs-lookup"><span data-stu-id="ba499-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="ba499-356">A Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não é selecionada.</span><span class="sxs-lookup"><span data-stu-id="ba499-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="ba499-357">false</span><span class="sxs-lookup"><span data-stu-id="ba499-357">false</span></span> |<span data-ttu-id="ba499-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="ba499-358">mergeFiles</span></span> |<span data-ttu-id="ba499-359">Para uma pasta de origem Pasta1 com a seguinte estrutura,</span><span class="sxs-lookup"><span data-stu-id="ba499-359">For a source folder Folder1 with the following structure,</span></span><br/><br/><span data-ttu-id="ba499-360">Pasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-360">Folder1</span></span><br/><span data-ttu-id="ba499-361">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="ba499-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="ba499-362">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="ba499-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="ba499-363">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="ba499-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="ba499-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="ba499-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="ba499-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="ba499-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="ba499-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="ba499-367">a pasta de destino Pasta1 é criada com a seguinte estrutura:</span><span class="sxs-lookup"><span data-stu-id="ba499-367">the target folder Folder1 is created with the following structure:</span></span><br/><br/><span data-ttu-id="ba499-368">Pasta1</span><span class="sxs-lookup"><span data-stu-id="ba499-368">Folder1</span></span><br/><span data-ttu-id="ba499-369">&nbsp;&nbsp;&nbsp;&nbsp;Os conteúdos de Arquivo1 + Arquivo2 são mesclados em um arquivo com um nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ba499-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="ba499-370">&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="ba499-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="ba499-371">A Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não é selecionada.</span><span class="sxs-lookup"><span data-stu-id="ba499-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="ba499-372">Formatos de arquivo e de compactação com suporte</span><span class="sxs-lookup"><span data-stu-id="ba499-372">Supported file and compression formats</span></span>
<span data-ttu-id="ba499-373">Consulte o artigo [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="ba499-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-file-system"></a><span data-ttu-id="ba499-374">Exemplos JSON para cópia de dados do sistema de arquivos</span><span class="sxs-lookup"><span data-stu-id="ba499-374">JSON examples for copying data to and from file system</span></span>
<span data-ttu-id="ba499-375">Os exemplos a seguir fornecem amostras de definições de JSON que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ba499-375">The following examples provide sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ba499-376">Eles mostram como copiar dados entre um sistema de arquivos local e o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba499-376">They show how to copy data to and from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="ba499-377">No entanto, você pode copiar dados *diretamente* de qualquer uma das fontes para qualquer um dos receptores listados em [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) (Fontes e coletores com suporte) usando a Atividade de Cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ba499-377">However, you can copy data *directly* from any of the sources to any of the sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-to-azure-blob-storage"></a><span data-ttu-id="ba499-378">Exemplo: copiar dados de um sistema de arquivos local para um Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="ba499-378">Example: Copy data from an on-premises file system to Azure Blob storage</span></span>
<span data-ttu-id="ba499-379">Este exemplo mostra como copiar dados de um sistema de arquivos local para um Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba499-379">This sample shows how to copy data from an on-premises file system to Azure Blob storage.</span></span> <span data-ttu-id="ba499-380">O exemplo tem as seguintes entidades do Data Factory:</span><span class="sxs-lookup"><span data-stu-id="ba499-380">The sample has the following Data Factory entities:</span></span>

* <span data-ttu-id="ba499-381">Um serviço vinculado do tipo [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ba499-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="ba499-382">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ba499-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="ba499-383">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ba499-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="ba499-384">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ba499-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="ba499-385">Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ba499-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ba499-386">O exemplo a seguir copia dados de uma série temporal do sistema de arquivos local para o Armazenamento de Blobs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ba499-386">The following sample copies time-series data from an on-premises file system to Azure Blob storage every hour.</span></span> <span data-ttu-id="ba499-387">As propriedades JSON que são usadas nestes exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="ba499-387">The JSON properties that are used in these samples are described in the sections after the samples.</span></span>

<span data-ttu-id="ba499-388">Como uma primeira etapa, configure o Gateway de Gerenciamento de Dados conforme as instruções em [Mover dados entre fontes locais e a nuvem com o Gateway de Gerenciamento de Dados](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="ba499-388">As a first step, set up Data Management Gateway as per the instructions in [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="ba499-389">**Serviço vinculado do Servidor de Arquivos Local:**</span><span class="sxs-lookup"><span data-stu-id="ba499-389">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="ba499-390">É recomendável usar a propriedade **encryptedCredential** em vez das propriedades **userid** e **password**.</span><span class="sxs-lookup"><span data-stu-id="ba499-390">We recommend using the **encryptedCredential** property instead the **userid** and **password** properties.</span></span> <span data-ttu-id="ba499-391">Confira [File Server linked service](#linked-service-properties) (Serviço vinculado do Servidor de Arquivos) para obter detalhes sobre este serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ba499-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="ba499-392">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="ba499-392">**Azure Storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

<span data-ttu-id="ba499-393">**Conjunto de dados de entrada do sistema de arquivos local:**</span><span class="sxs-lookup"><span data-stu-id="ba499-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="ba499-394">Dados são coletados de um novo arquivo a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ba499-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="ba499-395">As propriedades folderPath e fileName são determinadas com base na hora de início da fatia.</span><span class="sxs-lookup"><span data-stu-id="ba499-395">The folderPath and fileName properties are determined based on the start time of the slice.</span></span>  

<span data-ttu-id="ba499-396">A configuração `"external": "true"` informa ao Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade nele.</span><span class="sxs-lookup"><span data-stu-id="ba499-396">Setting `"external": "true"` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemInput",
  "properties": {
    "type": " FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

<span data-ttu-id="ba499-397">**Conjunto de dados do Armazenamento de Blobs do Azure:**</span><span class="sxs-lookup"><span data-stu-id="ba499-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="ba499-398">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="ba499-398">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ba499-399">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="ba499-399">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="ba499-400">O caminho da pasta usa as partes ano, mês, dia e hora da hora de início.</span><span class="sxs-lookup"><span data-stu-id="ba499-400">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="ba499-401">**Uma atividade de cópia em um pipeline com origem de Sistema de Arquivos e coletor de Blob:**</span><span class="sxs-lookup"><span data-stu-id="ba499-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="ba499-402">O pipeline contém uma atividade de cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ba499-402">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="ba499-403">Na definição JSON do pipeline, o tipo de **fonte** está definido como **FileSystemSource** e o tipo de **coletor** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="ba499-403">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T19:00:00",
    "description":"Pipeline for copy activity",
    "activities":[  
      {
        "name": "OnpremisesFileSystemtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "OnpremisesFileSystemInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "FileSystemSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```

### <a name="example-copy-data-from-azure-sql-database-to-an-on-premises-file-system"></a><span data-ttu-id="ba499-404">Exemplo: copiar dados do Banco de Dados SQL do Azure para um sistema de arquivos local</span><span class="sxs-lookup"><span data-stu-id="ba499-404">Example: Copy data from Azure SQL Database to an on-premises file system</span></span>
<span data-ttu-id="ba499-405">O exemplo a seguir mostra:</span><span class="sxs-lookup"><span data-stu-id="ba499-405">The following sample shows:</span></span>

* <span data-ttu-id="ba499-406">Um serviço vinculado do tipo [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="ba499-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="ba499-407">Um serviço vinculado do tipo [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ba499-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="ba499-408">Um conjunto de dados de entrada do tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ba499-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="ba499-409">Um conjunto de dados de saída do tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ba499-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="ba499-410">Um pipeline com a atividade de cópia que usa [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) e [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ba499-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="ba499-411">O exemplo copia os dados de série temporal de uma tabela SQL do Azure para um sistema de arquivos local a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ba499-411">The sample copies time-series data from an Azure SQL table to an on-premises file system every hour.</span></span> <span data-ttu-id="ba499-412">As propriedades JSON que são usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="ba499-412">The JSON properties that are used in these samples are described in sections after the samples.</span></span>

<span data-ttu-id="ba499-413">**Serviço vinculado para o Banco de Dados SQL do Azure:**</span><span class="sxs-lookup"><span data-stu-id="ba499-413">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```

<span data-ttu-id="ba499-414">**Serviço vinculado do Servidor de Arquivos Local:**</span><span class="sxs-lookup"><span data-stu-id="ba499-414">**On-Premises File Server linked service:**</span></span>

```JSON
{
  "Name": "OnPremisesFileServerLinkedService",
  "properties": {
    "type": "OnPremisesFileServer",
    "typeProperties": {
      "host": "\\\\Contosogame-Asia.<region>.corp.<company>.com",
      "userid": "Admin",
      "password": "123456",
      "gatewayName": "mygateway"
    }
  }
}
```

<span data-ttu-id="ba499-415">É recomendável usar a propriedade **encryptedCredential** em vez de usar as propriedades **userid** e **password**.</span><span class="sxs-lookup"><span data-stu-id="ba499-415">We recommend using the **encryptedCredential** property instead of using the **userid** and **password** properties.</span></span> <span data-ttu-id="ba499-416">Confira [File System linked service](#linked-service-properties) (Serviço vinculado do Sistema de Arquivos) para obter detalhes sobre este serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="ba499-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="ba499-417">**Conjunto de dados de entrada do SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="ba499-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="ba499-418">O exemplo supõe que você criou uma tabela "MyTable" no SQL Azure e que ela contém uma coluna chamada "timestampcolumn" para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="ba499-418">The sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="ba499-419">A configuração ``“external”: ”true”`` informa ao Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade nele.</span><span class="sxs-lookup"><span data-stu-id="ba499-419">Setting ``“external”: ”true”`` informs Data Factory that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

<span data-ttu-id="ba499-420">**Conjunto de dados de saída do sistema de arquivos local:**</span><span class="sxs-lookup"><span data-stu-id="ba499-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="ba499-421">Dados são copiados para um novo arquivo a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ba499-421">Data is copied to a new file every hour.</span></span> <span data-ttu-id="ba499-422">folderPath e fileName para o blob são determinados com base na hora de início da fatia.</span><span class="sxs-lookup"><span data-stu-id="ba499-422">The folderPath and fileName for the blob are determined based on the start time of the slice.</span></span>

```JSON
{
  "name": "OnpremisesFileSystemOutput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": " OnPremisesFileServerLinkedService ",
    "typeProperties": {
      "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

<span data-ttu-id="ba499-423">**Uma atividade de cópia em um pipeline com origem SQL e coletor de Sistema de Arquivos:**</span><span class="sxs-lookup"><span data-stu-id="ba499-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="ba499-424">O pipeline contém uma atividade de cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="ba499-424">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="ba499-425">Na definição JSON do pipeline, o tipo de **fonte** está definido como **SqlSource** e o tipo de **coletor** está definido como **FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="ba499-425">In the pipeline JSON definition, the **source** type is set to **SqlSource**, and the **sink** type is set to **FileSystemSink**.</span></span> <span data-ttu-id="ba499-426">A consulta SQL que é especificada para a propriedade **SqlReaderQuery** seleciona os dados da última hora a serem copiados.</span><span class="sxs-lookup"><span data-stu-id="ba499-426">The SQL query that is specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-06-01T18:00:00",
    "end":"2015-06-01T20:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoOnPremisesFile",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "OnpremisesFileSystemOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "FileSystemSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 3,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```


<span data-ttu-id="ba499-427">Você também pode mapear colunas do conjunto de dados de origem para colunas do conjunto de dados de coletor na definição da atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="ba499-427">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="ba499-428">Para obter detalhes, confira [Mapear colunas de conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="ba499-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ba499-429">Desempenho e ajuste</span><span class="sxs-lookup"><span data-stu-id="ba499-429">Performance and tuning</span></span>
 <span data-ttu-id="ba499-430">Para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory e diversas maneiras para otimizá-la, confira [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) (Guia de desempenho e ajuste da Atividade de Cópia).</span><span class="sxs-lookup"><span data-stu-id="ba499-430">To learn about key factors that impact the performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
