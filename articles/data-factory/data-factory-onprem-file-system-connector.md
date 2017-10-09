---
title: aaaCopy dados para/de um sistema de arquivos usando o Azure Data Factory | Microsoft Docs
description: Saiba como toocopy tooand de dados de um sistema de arquivos local por meio do Azure Data Factory.
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
ms.openlocfilehash: 201b8bc3ffa639df781443aa0c3f95c975d280be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-an-on-premises-file-system-by-using-azure-data-factory"></a><span data-ttu-id="b9bc1-103">Copiar dados tooand de um sistema de arquivos local usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b9bc1-103">Copy data tooand from an on-premises file system by using Azure Data Factory</span></span>
<span data-ttu-id="b9bc1-104">Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toocopy de/para um sistema de arquivos local.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-104">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data to/from an on-premises file system.</span></span> <span data-ttu-id="b9bc1-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="b9bc1-106">Cenários com suporte</span><span class="sxs-lookup"><span data-stu-id="b9bc1-106">Supported scenarios</span></span>
<span data-ttu-id="b9bc1-107">Você pode copiar dados **de um sistema de arquivos local** toohello repositórios de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-107">You can copy data **from an on-premises file system** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="b9bc1-108">Você pode copiar dados de saudação armazenamentos de dados a seguir **tooan sistema de arquivos local**:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-108">You can copy data from hello following data stores **tooan on-premises file system**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="b9bc1-109">Atividade de cópia não exclui o arquivo de origem Olá depois que ele destino toohello foram copiados com êxito.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="b9bc1-110">Se precisar de arquivo de origem toodelete Olá após uma cópia bem-sucedida, criar um arquivo de saudação toodelete atividade personalizada e usar a atividade Olá no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="b9bc1-111">Habilitando a conectividade</span><span class="sxs-lookup"><span data-stu-id="b9bc1-111">Enabling connectivity</span></span>
<span data-ttu-id="b9bc1-112">Fábrica de dados oferece suporte à conexão tooand de um sistema de arquivos local por meio de **Data Management Gateway**.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-112">Data Factory supports connecting tooand from an on-premises file system via **Data Management Gateway**.</span></span> <span data-ttu-id="b9bc1-113">Você deve instalar Olá Data Management Gateway em seu ambiente local para Olá Data Factory serviço tooconnect tooany com suporte no repositório de dados local incluindo o sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-113">You must install hello Data Management Gateway in your on-premises environment for hello Data Factory service tooconnect tooany supported on-premises data store including file system.</span></span> <span data-ttu-id="b9bc1-114">toolearn sobre o Gateway de gerenciamento de dados e para instruções passo a passo sobre como configurar o gateway hello, consulte [mover dados entre fontes locais e na nuvem de saudação com Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-114">toolearn about Data Management Gateway and for step-by-step instructions on setting up hello gateway, see [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="b9bc1-115">Além de Gateway de gerenciamento de dados, nenhum outro arquivo binário necessário toobe instalado toocommunicate tooand de um sistema de arquivos local.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-115">Apart from Data Management Gateway, no other binary files need toobe installed toocommunicate tooand from an on-premises file system.</span></span> <span data-ttu-id="b9bc1-116">Você deve instalar e usar Olá Gateway de gerenciamento de dados, mesmo se o sistema de arquivos Olá estiver em VM do Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-116">You must install and use hello Data Management Gateway even if hello file system is in Azure IaaS VM.</span></span> <span data-ttu-id="b9bc1-117">Para obter informações detalhadas sobre o gateway hello, consulte [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-117">For detailed information about hello gateway, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>

<span data-ttu-id="b9bc1-118">instalar toouse um compartilhamento de arquivo do Linux, [Samba](https://www.samba.org/) no servidor Linux e instalar o Gateway de gerenciamento de dados em um servidor Windows.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-118">toouse a Linux file share, install [Samba](https://www.samba.org/) on your Linux server, and install Data Management Gateway on a Windows server.</span></span> <span data-ttu-id="b9bc1-119">Não há suporte para a instalação do Gateway de Gerenciamento de Dados em um servidor Linux.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-119">Installing Data Management Gateway on a Linux server is not supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b9bc1-120">Introdução</span><span class="sxs-lookup"><span data-stu-id="b9bc1-120">Getting started</span></span>
<span data-ttu-id="b9bc1-121">Você pode criar um pipeline com uma atividade de cópia que mova dados bidirecionalmente de/para um sistema de arquivos usando ferramentas/APIs diferentes.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-121">You can create a pipeline with a copy activity that moves data to/from a file system by using different tools/APIs.</span></span>

<span data-ttu-id="b9bc1-122">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="b9bc1-123">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="b9bc1-124">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="b9bc1-125">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="b9bc1-126">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="b9bc1-127">Criar uma **data factory**.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-127">Create a **data factory**.</span></span> <span data-ttu-id="b9bc1-128">Um data factory pode conter um ou mais pipelines.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-128">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="b9bc1-129">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-129">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="b9bc1-130">Por exemplo, se você estiver copiando dados de um sistema de arquivos do blob do Azure storage tooan local, você criar duas toolink de serviços vinculados seu sistema de arquivos local e a fábrica de dados de tooyour de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-130">For example, if you are copying data from an Azure blob storage tooan on-premises file system, you create two linked services toolink your on-premises file system and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="b9bc1-131">Para propriedades de serviço vinculado que sistema de arquivos local tooan específicos, consulte [vinculado propriedades do serviço](#linked-service-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-131">For linked service properties that are specific tooan on-premises file system, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="b9bc1-132">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="b9bc1-133">O exemplo hello mencionado na última etapa do hello, você criará um contêiner de blob do conjunto de dados toospecify hello e a pasta que contém os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-133">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="b9bc1-134">E, então, criar outro conjunto de dados toospecify Olá pasta e nome de arquivo (opcional) no sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-134">And, you create another dataset toospecify hello folder and file name (optional) in your file system.</span></span> <span data-ttu-id="b9bc1-135">Para propriedades de conjunto de dados que são específicos de local de tooon sistema de arquivos, consulte [propriedades de conjunto de dados](#dataset-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-135">For dataset properties that are specific tooon-premises file system, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="b9bc1-136">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-136">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="b9bc1-137">Exemplo hello mencionado anteriormente, você usar BlobSource como uma origem e FileSystemSink como um coletor de atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-137">In hello example mentioned earlier, you use BlobSource as a source and FileSystemSink as a sink for hello copy activity.</span></span> <span data-ttu-id="b9bc1-138">Da mesma forma, se você estiver copiando de tooAzure de sistema de arquivos local armazenamento de Blob, use FileSystemSource e BlobSink na atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-138">Similarly, if you are copying from on-premises file system tooAzure Blob Storage, you use FileSystemSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="b9bc1-139">Para o sistema de arquivos de propriedades de atividade de cópia local tooon específico, consulte [copiar as propriedades de atividade](#copy-activity-properties) seção.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-139">For copy activity properties that are specific tooon-premises file system, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="b9bc1-140">Para obter detalhes sobre como toouse um repositório de dados como uma origem ou um coletor, clique em Olá link na seção anterior de saudação para seu armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-140">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="b9bc1-141">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-141">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="b9bc1-142">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-142">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="b9bc1-143">Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de um sistema de arquivos, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-file-system) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-143">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from a file system, see [JSON examples](#json-examples-for-copying-data-to-and-from-file-system) section of this article.</span></span>

<span data-ttu-id="b9bc1-144">Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades toofile específico sistema:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-144">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific toofile system:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="b9bc1-145">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="b9bc1-145">Linked service properties</span></span>
<span data-ttu-id="b9bc1-146">Você pode vincular uma fábrica de dados do Azure local arquivo sistema tooan com hello **o servidor de arquivos local** serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-146">You can link an on-premises file system tooan Azure data factory with hello **On-Premises File Server** linked service.</span></span> <span data-ttu-id="b9bc1-147">Olá a tabela a seguir fornece descrições dos elementos JSON que são específico toohello serviço vinculado de servidor de arquivos local.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-147">hello following table provides descriptions for JSON elements that are specific toohello On-Premises File Server linked service.</span></span>

| <span data-ttu-id="b9bc1-148">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b9bc1-148">Property</span></span> | <span data-ttu-id="b9bc1-149">Descrição</span><span class="sxs-lookup"><span data-stu-id="b9bc1-149">Description</span></span> | <span data-ttu-id="b9bc1-150">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b9bc1-150">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9bc1-151">type</span><span class="sxs-lookup"><span data-stu-id="b9bc1-151">type</span></span> |<span data-ttu-id="b9bc1-152">Verifique se a propriedade de tipo hello está definida muito**OnPremisesFileServer**.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-152">Ensure that hello type property is set too**OnPremisesFileServer**.</span></span> |<span data-ttu-id="b9bc1-153">Sim</span><span class="sxs-lookup"><span data-stu-id="b9bc1-153">Yes</span></span> |
| <span data-ttu-id="b9bc1-154">host</span><span class="sxs-lookup"><span data-stu-id="b9bc1-154">host</span></span> |<span data-ttu-id="b9bc1-155">Especifica o caminho de raiz de saudação da pasta Olá que você deseja toocopy.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-155">Specifies hello root path of hello folder that you want toocopy.</span></span> <span data-ttu-id="b9bc1-156">Use o caractere de escape de saudação ' \ ' para caracteres especiais na cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-156">Use hello escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="b9bc1-157">Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-157">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span> |<span data-ttu-id="b9bc1-158">Sim</span><span class="sxs-lookup"><span data-stu-id="b9bc1-158">Yes</span></span> |
| <span data-ttu-id="b9bc1-159">userid</span><span class="sxs-lookup"><span data-stu-id="b9bc1-159">userid</span></span> |<span data-ttu-id="b9bc1-160">Especifique a ID de saudação do usuário de saudação que tem acesso toohello server.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-160">Specify hello ID of hello user who has access toohello server.</span></span> |<span data-ttu-id="b9bc1-161">Não (se você escolher encryptedcredential)</span><span class="sxs-lookup"><span data-stu-id="b9bc1-161">No (if you choose encryptedCredential)</span></span> |
| <span data-ttu-id="b9bc1-162">Senha</span><span class="sxs-lookup"><span data-stu-id="b9bc1-162">password</span></span> |<span data-ttu-id="b9bc1-163">Especifique a senha de saudação para usuário hello (userid).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-163">Specify hello password for hello user (userid).</span></span> |<span data-ttu-id="b9bc1-164">Não (se você escolher encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="b9bc1-164">No (if you choose encryptedCredential</span></span> |
| <span data-ttu-id="b9bc1-165">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="b9bc1-165">encryptedCredential</span></span> |<span data-ttu-id="b9bc1-166">Especifique credenciais Olá criptografado que você pode obter executando Olá AzureRmDataFactoryEncryptValue novo cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-166">Specify hello encrypted credentials that you can get by running hello New-AzureRmDataFactoryEncryptValue cmdlet.</span></span> |<span data-ttu-id="b9bc1-167">Não (se você escolher toospecify ID de usuário e senha em texto sem formatação)</span><span class="sxs-lookup"><span data-stu-id="b9bc1-167">No (if you choose toospecify userid and password in plain text)</span></span> |
| <span data-ttu-id="b9bc1-168">gatewayName</span><span class="sxs-lookup"><span data-stu-id="b9bc1-168">gatewayName</span></span> |<span data-ttu-id="b9bc1-169">Especifica o nome de saudação do gateway de saudação que Data Factory deve usar o servidor de arquivos tooconnect toohello local.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-169">Specifies hello name of hello gateway that Data Factory should use tooconnect toohello on-premises file server.</span></span> |<span data-ttu-id="b9bc1-170">Sim</span><span class="sxs-lookup"><span data-stu-id="b9bc1-170">Yes</span></span> |


### <a name="sample-linked-service-and-dataset-definitions"></a><span data-ttu-id="b9bc1-171">Definições de conjunto de dados e serviço vinculado de exemplo</span><span class="sxs-lookup"><span data-stu-id="b9bc1-171">Sample linked service and dataset definitions</span></span>
| <span data-ttu-id="b9bc1-172">Cenário</span><span class="sxs-lookup"><span data-stu-id="b9bc1-172">Scenario</span></span> | <span data-ttu-id="b9bc1-173">Host em definição de serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="b9bc1-173">Host in linked service definition</span></span> | <span data-ttu-id="b9bc1-174">folderPath em definição de conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="b9bc1-174">folderPath in dataset definition</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9bc1-175">Pasta local no computador do Gateway de Gerenciamento de Dados </span><span class="sxs-lookup"><span data-stu-id="b9bc1-175">Local folder on Data Management Gateway machine:</span></span> <br/><br/><span data-ttu-id="b9bc1-176">Exemplos: D:\\\* ou D:\pasta\subpasta\\*</span><span class="sxs-lookup"><span data-stu-id="b9bc1-176">Examples: D:\\\* or D:\folder\subfolder\\*</span></span> |<span data-ttu-id="b9bc1-177">D:\\\\ (para o Gateway de Gerenciamento de Dados 2.0 e versões posteriores)</span><span class="sxs-lookup"><span data-stu-id="b9bc1-177">D:\\\\ (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/> <span data-ttu-id="b9bc1-178">localhost (para versões anteriores do Gateway de Gerenciamento de Dados 2.0)</span><span class="sxs-lookup"><span data-stu-id="b9bc1-178">localhost (for earlier versions than Data Management Gateway 2.0)</span></span> |<span data-ttu-id="b9bc1-179">.\\\\ ou pasta\\\\subpasta (para o Gateway de Gerenciamento de Dados 2.0 e versões posteriores)</span><span class="sxs-lookup"><span data-stu-id="b9bc1-179">.\\\\ or folder\\\\subfolder (for Data Management Gateway 2.0 and later versions)</span></span> <br/><br/><span data-ttu-id="b9bc1-180">D:\\\\ ou D:\\\\pasta\\\\subpasta (para a versão de gateway abaixo de 2.0)</span><span class="sxs-lookup"><span data-stu-id="b9bc1-180">D:\\\\ or D:\\\\folder\\\\subfolder (for gateway version below 2.0)</span></span> |
| <span data-ttu-id="b9bc1-181">Pasta compartilhada remota: </span><span class="sxs-lookup"><span data-stu-id="b9bc1-181">Remote shared folder:</span></span> <br/><br/><span data-ttu-id="b9bc1-182">Exemplos: \\\\meuservidor\\compartilhar\\\* ou \\\\meuservidor\\compartilhar\\pasta\\subpasta\\*</span><span class="sxs-lookup"><span data-stu-id="b9bc1-182">Examples: \\\\myserver\\share\\\* or \\\\myserver\\share\\folder\\subfolder\\*</span></span> |<span data-ttu-id="b9bc1-183">\\\\\\\\meuservidor\\\\compartilhar</span><span class="sxs-lookup"><span data-stu-id="b9bc1-183">\\\\\\\\myserver\\\\share</span></span> |<span data-ttu-id="b9bc1-184">.\\\\ ou pasta\\\\subpasta</span><span class="sxs-lookup"><span data-stu-id="b9bc1-184">.\\\\ or folder\\\\subfolder</span></span> |


### <a name="example-using-username-and-password-in-plain-text"></a><span data-ttu-id="b9bc1-185">Exemplo: usando username e password em texto sem formatação</span><span class="sxs-lookup"><span data-stu-id="b9bc1-185">Example: Using username and password in plain text</span></span>

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

### <a name="example-using-encryptedcredential"></a><span data-ttu-id="b9bc1-186">Exemplo: usando encryptedcredential</span><span class="sxs-lookup"><span data-stu-id="b9bc1-186">Example: Using encryptedcredential</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="b9bc1-187">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="b9bc1-187">Dataset properties</span></span>
<span data-ttu-id="b9bc1-188">Para obter uma lista completa das seções e propriedades disponíveis para definir os conjuntos de dados, confira [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-188">For a full list of sections and properties that are available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="b9bc1-189">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="b9bc1-190">seção de typeProperties Olá é diferente para cada tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-190">hello typeProperties section is different for each type of dataset.</span></span> <span data-ttu-id="b9bc1-191">Ele fornece informações como Olá local e o formato dos dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-191">It provides information such as hello location and format of hello data in hello data store.</span></span> <span data-ttu-id="b9bc1-192">Olá typeProperties seção de conjunto de dados de saudação do tipo **FileShare** tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-192">hello typeProperties section for hello dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="b9bc1-193">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b9bc1-193">Property</span></span> | <span data-ttu-id="b9bc1-194">Descrição</span><span class="sxs-lookup"><span data-stu-id="b9bc1-194">Description</span></span> | <span data-ttu-id="b9bc1-195">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b9bc1-195">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9bc1-196">folderPath</span><span class="sxs-lookup"><span data-stu-id="b9bc1-196">folderPath</span></span> |<span data-ttu-id="b9bc1-197">Especifica a pasta de toohello subcaminho hello.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-197">Specifies hello subpath toohello folder.</span></span> <span data-ttu-id="b9bc1-198">Use o caractere de escape de saudação ' \' para caracteres especiais na cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-198">Use hello escape character ‘\’ for special characters in hello string.</span></span> <span data-ttu-id="b9bc1-199">Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-199">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="b9bc1-200">Você pode combinar essa propriedade com **partitionBy** toohave caminhos de pastas com base na fatia datas / horas de início/término.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-200">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="b9bc1-201">Sim</span><span class="sxs-lookup"><span data-stu-id="b9bc1-201">Yes</span></span> |
| <span data-ttu-id="b9bc1-202">fileName</span><span class="sxs-lookup"><span data-stu-id="b9bc1-202">fileName</span></span> |<span data-ttu-id="b9bc1-203">Especifique o nome de saudação do arquivo de saudação em Olá **folderPath** se você quiser Olá tabela toorefer tooa arquivo específico na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-203">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="b9bc1-204">Se você não especificar qualquer valor para essa propriedade, a tabela de saudação aponta tooall arquivos na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-204">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="b9bc1-205">Quando **fileName** não for especificado para um conjunto de dados de saída e **preserveHierarchy** não for especificado no coletor de atividade, nome de saudação do arquivo hello gerado está em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-205">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="b9bc1-206">`Data.<Guid>.txt` (Exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="b9bc1-206">`Data.<Guid>.txt` (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="b9bc1-207">Não</span><span class="sxs-lookup"><span data-stu-id="b9bc1-207">No</span></span> |
| <span data-ttu-id="b9bc1-208">fileFilter</span><span class="sxs-lookup"><span data-stu-id="b9bc1-208">fileFilter</span></span> |<span data-ttu-id="b9bc1-209">Especifique um filtro toobe usado tooselect um subconjunto de arquivos no hello folderPath em vez de todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-209">Specify a filter toobe used tooselect a subset of files in hello folderPath rather than all files.</span></span> <br/><br/><span data-ttu-id="b9bc1-210">Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-210">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="b9bc1-211">Exemplo 1: "fileFilter": "*.log"</span><span class="sxs-lookup"><span data-stu-id="b9bc1-211">Example 1: "fileFilter": "*.log"</span></span><br/><span data-ttu-id="b9bc1-212">Exemplo 2: "fileFilter": 2014-1-?.txt"</span><span class="sxs-lookup"><span data-stu-id="b9bc1-212">Example 2: "fileFilter": 2014-1-?.txt"</span></span><br/><br/><span data-ttu-id="b9bc1-213">Observe que fileFilter é aplicável a um conjunto de dados FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-213">Note that fileFilter is applicable for an input FileShare dataset.</span></span> |<span data-ttu-id="b9bc1-214">Não</span><span class="sxs-lookup"><span data-stu-id="b9bc1-214">No</span></span> |
| <span data-ttu-id="b9bc1-215">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="b9bc1-215">partitionedBy</span></span> |<span data-ttu-id="b9bc1-216">Você pode usar partitionedBy toospecify um dinâmico folderPath/nome do arquivo de dados da série temporal.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-216">You can use partitionedBy toospecify a dynamic folderPath/fileName for time-series data.</span></span> <span data-ttu-id="b9bc1-217">Um exemplo é folderPath parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-217">An example is folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="b9bc1-218">Não</span><span class="sxs-lookup"><span data-stu-id="b9bc1-218">No</span></span> |
| <span data-ttu-id="b9bc1-219">formato</span><span class="sxs-lookup"><span data-stu-id="b9bc1-219">format</span></span> | <span data-ttu-id="b9bc1-220">Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-220">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="b9bc1-221">Saudação de conjunto **tipo** propriedade em formato tooone desses valores.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-221">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="b9bc1-222">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-222">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="b9bc1-223">Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-223">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="b9bc1-224">Não</span><span class="sxs-lookup"><span data-stu-id="b9bc1-224">No</span></span> |
| <span data-ttu-id="b9bc1-225">compactação</span><span class="sxs-lookup"><span data-stu-id="b9bc1-225">compression</span></span> | <span data-ttu-id="b9bc1-226">Especifica tipo de saudação e nível de compactação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-226">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="b9bc1-227">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-227">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="b9bc1-228">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-228">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="b9bc1-229">confira [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-229">see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="b9bc1-230">Não</span><span class="sxs-lookup"><span data-stu-id="b9bc1-230">No</span></span> |

> [!NOTE]
> <span data-ttu-id="b9bc1-231">Você não pode usar fileName e fileFilter simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-231">You cannot use fileName and fileFilter simultaneously.</span></span>

### <a name="using-partitionedby-property"></a><span data-ttu-id="b9bc1-232">Usando a propriedade partitionedBy</span><span class="sxs-lookup"><span data-stu-id="b9bc1-232">Using partitionedBy property</span></span>
<span data-ttu-id="b9bc1-233">Como mencionado na seção anterior hello, você pode especificar um dinâmico folderPath e filename para dados de série temporal com hello **partitionedBy** propriedade [funções da fábrica de dados e variáveis de sistema Olá](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-233">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="b9bc1-234">toounderstand obter mais detalhes sobre conjuntos de dados de série temporal, agendamento e fatias, consulte [criando conjuntos de dados](data-factory-create-datasets.md), [de agendamento e execução](data-factory-scheduling-and-execution.md), e [criar pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-234">toounderstand more details on time-series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="b9bc1-235">Exemplo 1:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-235">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="b9bc1-236">Neste exemplo, {Slice} é substituído pelo valor de saudação da variável de sistema de fábrica de dados Olá SliceStart no formato de saudação (AAAAMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-236">In this example, {Slice} is replaced with hello value of hello Data Factory system variable SliceStart in hello format (YYYYMMDDHH).</span></span> <span data-ttu-id="b9bc1-237">SliceStart refere-se toostart tempo da fração de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-237">SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="b9bc1-238">Olá folderPath é diferente para cada fatia.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-238">hello folderPath is different for each slice.</span></span> <span data-ttu-id="b9bc1-239">Por exemplo: wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-239">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="b9bc1-240">Exemplo 2:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-240">Sample 2:</span></span>

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

<span data-ttu-id="b9bc1-241">Neste exemplo, ano, mês, dia e hora de SliceStart são extraídos em variáveis separadas que usam as propriedades folderPath e fileName hello.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-241">In this example, year, month, day, and time of SliceStart are extracted into separate variables that hello folderPath and fileName properties use.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="b9bc1-242">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="b9bc1-242">Copy activity properties</span></span>
<span data-ttu-id="b9bc1-243">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-243">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b9bc1-244">As propriedades, como nome, descrição, conjuntos de dados de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-244">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="b9bc1-245">Por outro lado, as propriedades disponíveis no hello **typeProperties** seção de atividade Olá variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-245">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span>

<span data-ttu-id="b9bc1-246">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-246">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="b9bc1-247">Se você estiver movendo dados de um sistema de arquivos local, você defina o tipo de fonte de saudação na atividade de cópia de saudação muito**FileSystemSource**.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-247">If you are moving data from an on-premises file system, you set hello source type in hello copy activity too**FileSystemSource**.</span></span> <span data-ttu-id="b9bc1-248">Da mesma forma, se você estiver movendo dados tooan sistema de arquivos local, você definir o tipo de coletor Olá na atividade de cópia de saudação muito**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-248">Similarly, if you are moving data tooan on-premises file system, you set hello sink type in hello copy activity too**FileSystemSink**.</span></span> <span data-ttu-id="b9bc1-249">Esta seção fornece uma lista das propriedades às quais FileSystemSource e FileSystemSink dão suporte.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-249">This section provides a list of properties supported by FileSystemSource and FileSystemSink.</span></span>

<span data-ttu-id="b9bc1-250">**FileSystemSource** dá suporte a saudação propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-250">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="b9bc1-251">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b9bc1-251">Property</span></span> | <span data-ttu-id="b9bc1-252">Descrição</span><span class="sxs-lookup"><span data-stu-id="b9bc1-252">Description</span></span> | <span data-ttu-id="b9bc1-253">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="b9bc1-253">Allowed values</span></span> | <span data-ttu-id="b9bc1-254">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b9bc1-254">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b9bc1-255">recursiva</span><span class="sxs-lookup"><span data-stu-id="b9bc1-255">recursive</span></span> |<span data-ttu-id="b9bc1-256">Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-256">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="b9bc1-257">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="b9bc1-257">True, False (default)</span></span> |<span data-ttu-id="b9bc1-258">Não</span><span class="sxs-lookup"><span data-stu-id="b9bc1-258">No</span></span> |

<span data-ttu-id="b9bc1-259">**FileSystemSink** dá suporte a saudação propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-259">**FileSystemSink** supports hello following properties:</span></span>

| <span data-ttu-id="b9bc1-260">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b9bc1-260">Property</span></span> | <span data-ttu-id="b9bc1-261">Descrição</span><span class="sxs-lookup"><span data-stu-id="b9bc1-261">Description</span></span> | <span data-ttu-id="b9bc1-262">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="b9bc1-262">Allowed values</span></span> | <span data-ttu-id="b9bc1-263">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="b9bc1-263">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b9bc1-264">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="b9bc1-264">copyBehavior</span></span> |<span data-ttu-id="b9bc1-265">Define o comportamento de cópia de saudação quando origem Olá é BlobSource ou sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-265">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="b9bc1-266">**PreserveHierarchy:** preserva a hierarquia de arquivo hello na pasta de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-266">**PreserveHierarchy:** Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="b9bc1-267">Ou seja, caminho relativo do Olá Olá arquivo toohello origem da pasta de origem é Olá igual Olá o caminho relativo da pasta de destino toohello do arquivo de destino hello.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-267">That is, hello relative path of hello source file toohello source folder is hello same as hello relative path of hello target file toohello target folder.</span></span><br/><br/><span data-ttu-id="b9bc1-268">**FlattenHierarchy:** todos os arquivos da pasta de origem Olá são criados no primeiro nível saudação da pasta de destino.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-268">**FlattenHierarchy:** All files from hello source folder are created in hello first level of target folder.</span></span> <span data-ttu-id="b9bc1-269">arquivos de destino de saudação são criados com um nome gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-269">hello target files are created with an autogenerated name.</span></span><br/><br/><span data-ttu-id="b9bc1-270">**MergeFiles:** mescla todos os arquivos Olá pasta tooone do arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-270">**MergeFiles:** Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="b9bc1-271">Se o nome do blob/nome de arquivo hello for especificado, o nome mesclado Olá é nome especificado da saudação.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-271">If hello file name/blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="b9bc1-272">Caso contrário, ele será um nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-272">Otherwise, it is an auto-generated file name.</span></span> |<span data-ttu-id="b9bc1-273">Não</span><span class="sxs-lookup"><span data-stu-id="b9bc1-273">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="b9bc1-274">exemplos de recursive e copyBehavior</span><span class="sxs-lookup"><span data-stu-id="b9bc1-274">recursive and copyBehavior examples</span></span>
<span data-ttu-id="b9bc1-275">Esta seção descreve o comportamento resultante de saudação da operação de cópia de saudação para diferentes combinações de valores de propriedades de saudação recursiva e copyBehavior.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-275">This section describes hello resulting behavior of hello Copy operation for different combinations of values for hello recursive and copyBehavior properties.</span></span>

| <span data-ttu-id="b9bc1-276">valor de recursive</span><span class="sxs-lookup"><span data-stu-id="b9bc1-276">recursive value</span></span> | <span data-ttu-id="b9bc1-277">valor de copyBehavior</span><span class="sxs-lookup"><span data-stu-id="b9bc1-277">copyBehavior value</span></span> | <span data-ttu-id="b9bc1-278">Comportamento resultante</span><span class="sxs-lookup"><span data-stu-id="b9bc1-278">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b9bc1-279">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="b9bc1-279">true</span></span> |<span data-ttu-id="b9bc1-280">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="b9bc1-280">preserveHierarchy</span></span> |<span data-ttu-id="b9bc1-281">Para uma pasta de origem Pasta1 com hello estrutura, a seguir</span><span class="sxs-lookup"><span data-stu-id="b9bc1-281">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="b9bc1-282">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-282">Folder1</span></span><br/><span data-ttu-id="b9bc1-283">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-283">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b9bc1-284">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b9bc1-284">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b9bc1-285">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-285">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b9bc1-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="b9bc1-286">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b9bc1-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="b9bc1-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b9bc1-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="b9bc1-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b9bc1-289">pasta de destino Olá Pasta1 é criada com hello mesma estrutura como fonte de saudação:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-289">hello target folder Folder1 is created with hello same structure as hello source:</span></span><br/><br/><span data-ttu-id="b9bc1-290">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-290">Folder1</span></span><br/><span data-ttu-id="b9bc1-291">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-291">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b9bc1-292">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b9bc1-292">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b9bc1-293">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-293">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b9bc1-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="b9bc1-294">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b9bc1-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="b9bc1-295">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b9bc1-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="b9bc1-296">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span> |
| <span data-ttu-id="b9bc1-297">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="b9bc1-297">true</span></span> |<span data-ttu-id="b9bc1-298">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="b9bc1-298">flattenHierarchy</span></span> |<span data-ttu-id="b9bc1-299">Para uma pasta de origem Pasta1 com hello estrutura, a seguir</span><span class="sxs-lookup"><span data-stu-id="b9bc1-299">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="b9bc1-300">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-300">Folder1</span></span><br/><span data-ttu-id="b9bc1-301">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b9bc1-302">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b9bc1-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b9bc1-303">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b9bc1-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="b9bc1-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b9bc1-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="b9bc1-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b9bc1-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="b9bc1-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b9bc1-307">destino de saudação Pasta1 é criado com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="b9bc1-308">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-308">Folder1</span></span><br/><span data-ttu-id="b9bc1-309">&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-309">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="b9bc1-310">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b9bc1-310">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="b9bc1-311">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo3</span><span class="sxs-lookup"><span data-stu-id="b9bc1-311">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="b9bc1-312">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo4</span><span class="sxs-lookup"><span data-stu-id="b9bc1-312">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="b9bc1-313">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo5</span><span class="sxs-lookup"><span data-stu-id="b9bc1-313">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="b9bc1-314">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="b9bc1-314">true</span></span> |<span data-ttu-id="b9bc1-315">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="b9bc1-315">mergeFiles</span></span> |<span data-ttu-id="b9bc1-316">Para uma pasta de origem Pasta1 com hello estrutura, a seguir</span><span class="sxs-lookup"><span data-stu-id="b9bc1-316">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="b9bc1-317">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-317">Folder1</span></span><br/><span data-ttu-id="b9bc1-318">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-318">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b9bc1-319">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b9bc1-319">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b9bc1-320">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-320">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b9bc1-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="b9bc1-321">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b9bc1-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="b9bc1-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b9bc1-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="b9bc1-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b9bc1-324">destino de saudação Pasta1 é criado com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-324">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="b9bc1-325">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-325">Folder1</span></span><br/><span data-ttu-id="b9bc1-326">&nbsp;&nbsp;&nbsp;&nbsp;Os conteúdos de Arquivo1 + Arquivo2 + Arquivo3 + Arquivo4 + Arquivo5 são mesclados em um arquivo com um nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-326">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with an auto-generated file name.</span></span> |
| <span data-ttu-id="b9bc1-327">false</span><span class="sxs-lookup"><span data-stu-id="b9bc1-327">false</span></span> |<span data-ttu-id="b9bc1-328">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="b9bc1-328">preserveHierarchy</span></span> |<span data-ttu-id="b9bc1-329">Para uma pasta de origem Pasta1 com hello estrutura, a seguir</span><span class="sxs-lookup"><span data-stu-id="b9bc1-329">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="b9bc1-330">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-330">Folder1</span></span><br/><span data-ttu-id="b9bc1-331">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-331">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b9bc1-332">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b9bc1-332">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b9bc1-333">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-333">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b9bc1-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="b9bc1-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b9bc1-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="b9bc1-335">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b9bc1-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="b9bc1-336">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b9bc1-337">pasta de destino Olá Pasta1 é criada com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-337">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="b9bc1-338">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-338">Folder1</span></span><br/><span data-ttu-id="b9bc1-339">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-339">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b9bc1-340">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b9bc1-340">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><span data-ttu-id="b9bc1-341">A Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não é selecionada.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-341">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="b9bc1-342">false</span><span class="sxs-lookup"><span data-stu-id="b9bc1-342">false</span></span> |<span data-ttu-id="b9bc1-343">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="b9bc1-343">flattenHierarchy</span></span> |<span data-ttu-id="b9bc1-344">Para uma pasta de origem Pasta1 com hello estrutura, a seguir</span><span class="sxs-lookup"><span data-stu-id="b9bc1-344">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="b9bc1-345">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-345">Folder1</span></span><br/><span data-ttu-id="b9bc1-346">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b9bc1-347">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b9bc1-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b9bc1-348">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b9bc1-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="b9bc1-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b9bc1-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="b9bc1-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b9bc1-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="b9bc1-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b9bc1-352">pasta de destino Olá Pasta1 é criada com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-352">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="b9bc1-353">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-353">Folder1</span></span><br/><span data-ttu-id="b9bc1-354">&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-354">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="b9bc1-355">&nbsp;&nbsp;&nbsp;&nbsp;nome gerado automaticamente para o Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b9bc1-355">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><span data-ttu-id="b9bc1-356">A Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não é selecionada.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-356">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |
| <span data-ttu-id="b9bc1-357">false</span><span class="sxs-lookup"><span data-stu-id="b9bc1-357">false</span></span> |<span data-ttu-id="b9bc1-358">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="b9bc1-358">mergeFiles</span></span> |<span data-ttu-id="b9bc1-359">Para uma pasta de origem Pasta1 com hello estrutura, a seguir</span><span class="sxs-lookup"><span data-stu-id="b9bc1-359">For a source folder Folder1 with hello following structure,</span></span><br/><br/><span data-ttu-id="b9bc1-360">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-360">Folder1</span></span><br/><span data-ttu-id="b9bc1-361">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-361">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="b9bc1-362">&nbsp;&nbsp;&nbsp;&nbsp;Arquivo2</span><span class="sxs-lookup"><span data-stu-id="b9bc1-362">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="b9bc1-363">&nbsp;&nbsp;&nbsp;&nbsp;Subpasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-363">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="b9bc1-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo3</span><span class="sxs-lookup"><span data-stu-id="b9bc1-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="b9bc1-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo4</span><span class="sxs-lookup"><span data-stu-id="b9bc1-365">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="b9bc1-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arquivo5</span><span class="sxs-lookup"><span data-stu-id="b9bc1-366">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="b9bc1-367">pasta de destino Olá Pasta1 é criada com hello estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-367">hello target folder Folder1 is created with hello following structure:</span></span><br/><br/><span data-ttu-id="b9bc1-368">Pasta1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-368">Folder1</span></span><br/><span data-ttu-id="b9bc1-369">&nbsp;&nbsp;&nbsp;&nbsp;Os conteúdos de Arquivo1 + Arquivo2 são mesclados em um arquivo com um nome de arquivo gerado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-369">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with an auto-generated file name.</span></span><br/><span data-ttu-id="b9bc1-370">&nbsp;&nbsp;&nbsp;&nbsp;Nome gerado automaticamente para o Arquivo1</span><span class="sxs-lookup"><span data-stu-id="b9bc1-370">&nbsp;&nbsp;&nbsp;&nbsp;Auto-generated name for File1</span></span><br/><br/><span data-ttu-id="b9bc1-371">A Subpasta1 com Arquivo3, Arquivo4 e Arquivo5 não é selecionada.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-371">Subfolder1 with File3, File4, and File5 is not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="b9bc1-372">Formatos de arquivo e de compactação com suporte</span><span class="sxs-lookup"><span data-stu-id="b9bc1-372">Supported file and compression formats</span></span>
<span data-ttu-id="b9bc1-373">Consulte o artigo [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-373">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-file-system"></a><span data-ttu-id="b9bc1-374">Exemplos JSON para copiar dados tooand do sistema de arquivos</span><span class="sxs-lookup"><span data-stu-id="b9bc1-374">JSON examples for copying data tooand from file system</span></span>
<span data-ttu-id="b9bc1-375">Olá, exemplos a seguir fornecem as definições de JSON de exemplo que você pode usar toocreate um pipeline usando Olá [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-375">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b9bc1-376">Eles mostram como toocopy tooand de dados de um sistema de arquivos local e o armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-376">They show how toocopy data tooand from an on-premises file system and Azure Blob storage.</span></span> <span data-ttu-id="b9bc1-377">No entanto, você pode copiar dados *diretamente* de qualquer um dos Olá fontes tooany de Coletores Olá listados na [suporte para origens e coletores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-377">However, you can copy data *directly* from any of hello sources tooany of hello sinks listed in [Supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-an-on-premises-file-system-tooazure-blob-storage"></a><span data-ttu-id="b9bc1-378">Exemplo: Copiar dados de um tooAzure de sistema de arquivos local armazenamento de Blob</span><span class="sxs-lookup"><span data-stu-id="b9bc1-378">Example: Copy data from an on-premises file system tooAzure Blob storage</span></span>
<span data-ttu-id="b9bc1-379">Este exemplo mostra como toocopy dados de um tooAzure de sistema de arquivos local armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-379">This sample shows how toocopy data from an on-premises file system tooAzure Blob storage.</span></span> <span data-ttu-id="b9bc1-380">exemplo Hello tem Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-380">hello sample has hello following Data Factory entities:</span></span>

* <span data-ttu-id="b9bc1-381">Um serviço vinculado do tipo [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-381">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="b9bc1-382">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-382">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="b9bc1-383">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-383">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="b9bc1-384">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-384">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="b9bc1-385">Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-385">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="b9bc1-386">saudação de exemplo a seguir copia dados de série temporal de um tooAzure de sistema de arquivos local armazenamento de Blob a cada hora.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-386">hello following sample copies time-series data from an on-premises file system tooAzure Blob storage every hour.</span></span> <span data-ttu-id="b9bc1-387">propriedades JSON Olá usados nesses exemplos são descritas nas seções de saudação após exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-387">hello JSON properties that are used in these samples are described in hello sections after hello samples.</span></span>

<span data-ttu-id="b9bc1-388">Como uma primeira etapa, configurar o Gateway de gerenciamento de dados de acordo com as instruções de saudação do [mover dados entre fontes locais e na nuvem de saudação com Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-388">As a first step, set up Data Management Gateway as per hello instructions in [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md).</span></span>

<span data-ttu-id="b9bc1-389">**Serviço vinculado do Servidor de Arquivos Local:**</span><span class="sxs-lookup"><span data-stu-id="b9bc1-389">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="b9bc1-390">É recomendável usar Olá **encryptedCredential** Olá em vez disso, a propriedade **userid** e **senha** propriedades.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-390">We recommend using hello **encryptedCredential** property instead hello **userid** and **password** properties.</span></span> <span data-ttu-id="b9bc1-391">Confira [File Server linked service](#linked-service-properties) (Serviço vinculado do Servidor de Arquivos) para obter detalhes sobre este serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-391">See [File Server linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="b9bc1-392">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="b9bc1-392">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="b9bc1-393">**Conjunto de dados de entrada do sistema de arquivos local:**</span><span class="sxs-lookup"><span data-stu-id="b9bc1-393">**On-premises file system input dataset:**</span></span>

<span data-ttu-id="b9bc1-394">Dados são coletados de um novo arquivo a cada hora.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-394">Data is picked up from a new file every hour.</span></span> <span data-ttu-id="b9bc1-395">Olá folderPath e fileName propriedades são determinadas com base na hora de início de saudação da fatia hello.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-395">hello folderPath and fileName properties are determined based on hello start time of hello slice.</span></span>  

<span data-ttu-id="b9bc1-396">Configuração `"external": "true"` informa a fábrica de dados Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-396">Setting `"external": "true"` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="b9bc1-397">**Conjunto de dados do Armazenamento de Blobs do Azure:**</span><span class="sxs-lookup"><span data-stu-id="b9bc1-397">**Azure Blob storage output dataset:**</span></span>

<span data-ttu-id="b9bc1-398">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-398">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="b9bc1-399">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-399">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="b9bc1-400">caminho da pasta Olá usa partes de ano, mês, dia e hora Olá Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-400">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

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

<span data-ttu-id="b9bc1-401">**Uma atividade de cópia em um pipeline com origem de Sistema de Arquivos e coletor Blob:**</span><span class="sxs-lookup"><span data-stu-id="b9bc1-401">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="b9bc1-402">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-402">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="b9bc1-403">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**FileSystemSource**, e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-403">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

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

### <a name="example-copy-data-from-azure-sql-database-tooan-on-premises-file-system"></a><span data-ttu-id="b9bc1-404">Exemplo: Copiar dados do sistema de arquivos do banco de dados do Azure SQL tooan local</span><span class="sxs-lookup"><span data-stu-id="b9bc1-404">Example: Copy data from Azure SQL Database tooan on-premises file system</span></span>
<span data-ttu-id="b9bc1-405">Olá mostra de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="b9bc1-405">hello following sample shows:</span></span>

* <span data-ttu-id="b9bc1-406">Um serviço vinculado do tipo [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="b9bc1-406">A linked service of type [AzureSqlDatabase.](data-factory-azure-sql-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="b9bc1-407">Um serviço vinculado do tipo [OnPremisesFileServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-407">A linked service of type [OnPremisesFileServer](#linked-service-properties).</span></span>
* <span data-ttu-id="b9bc1-408">Um conjunto de dados de entrada do tipo [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-408">An input dataset of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="b9bc1-409">Um conjunto de dados de saída do tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-409">An output dataset of type [FileShare](#dataset-properties).</span></span>
* <span data-ttu-id="b9bc1-410">Um pipeline com a atividade de cópia que usa [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) e [FileSystemSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-410">A pipeline with a copy activity that uses [SqlSource](data-factory-azure-sql-connector.md##copy-activity-properties) and [FileSystemSink](#copy-activity-properties).</span></span>

<span data-ttu-id="b9bc1-411">exemplo Hello copia dados de série temporal de um sistema de arquivos local do SQL Azure tabela tooan a cada hora.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-411">hello sample copies time-series data from an Azure SQL table tooan on-premises file system every hour.</span></span> <span data-ttu-id="b9bc1-412">propriedades JSON Olá usados nesses exemplos são descritas nas seções após exemplos hello.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-412">hello JSON properties that are used in these samples are described in sections after hello samples.</span></span>

<span data-ttu-id="b9bc1-413">**Serviço vinculado para o Banco de Dados SQL do Azure:**</span><span class="sxs-lookup"><span data-stu-id="b9bc1-413">**Azure SQL Database linked service:**</span></span>

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

<span data-ttu-id="b9bc1-414">**Serviço vinculado do Servidor de Arquivos Local:**</span><span class="sxs-lookup"><span data-stu-id="b9bc1-414">**On-Premises File Server linked service:**</span></span>

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

<span data-ttu-id="b9bc1-415">É recomendável usar Olá **encryptedCredential** propriedade em vez de usar o hello **userid** e **senha** propriedades.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-415">We recommend using hello **encryptedCredential** property instead of using hello **userid** and **password** properties.</span></span> <span data-ttu-id="b9bc1-416">Confira [File System linked service](#linked-service-properties) (Serviço vinculado do Sistema de Arquivos) para obter detalhes sobre este serviço vinculado.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-416">See [File System linked service](#linked-service-properties) for details about this linked service.</span></span>

<span data-ttu-id="b9bc1-417">**Conjunto de dados de entrada do SQL Azure:**</span><span class="sxs-lookup"><span data-stu-id="b9bc1-417">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="b9bc1-418">exemplo Hello pressupõe que você criou uma tabela "MyTable" no SQL Azure, e ele contém uma coluna chamada "timestampcolumn" para os dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-418">hello sample assumes that you've created a table “MyTable” in Azure SQL, and it contains a column called “timestampcolumn” for time-series data.</span></span>

<span data-ttu-id="b9bc1-419">Configuração ``“external”: ”true”`` informa a fábrica de dados Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-419">Setting ``“external”: ”true”`` informs Data Factory that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="b9bc1-420">**Conjunto de dados de saída do sistema de arquivos local:**</span><span class="sxs-lookup"><span data-stu-id="b9bc1-420">**On-premises file system output dataset:**</span></span>

<span data-ttu-id="b9bc1-421">Dados são copiados tooa novo arquivo a cada hora.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-421">Data is copied tooa new file every hour.</span></span> <span data-ttu-id="b9bc1-422">Olá folderPath e fileName blob Olá são determinados com base na hora de início de saudação da fatia hello.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-422">hello folderPath and fileName for hello blob are determined based on hello start time of hello slice.</span></span>

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

<span data-ttu-id="b9bc1-423">**Uma atividade de cópia em um pipeline com origem SQL e coletor de Sistema de Arquivos:**</span><span class="sxs-lookup"><span data-stu-id="b9bc1-423">**A copy activity in a pipeline with SQL source and File System sink:**</span></span>

<span data-ttu-id="b9bc1-424">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-424">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="b9bc1-425">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**SqlSource**e hello **coletor** tipo está definido muito**FileSystemSink**.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-425">In hello pipeline JSON definition, hello **source** type is set too**SqlSource**, and hello **sink** type is set too**FileSystemSink**.</span></span> <span data-ttu-id="b9bc1-426">consulta SQL Olá especificado para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá após toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-426">hello SQL query that is specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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


<span data-ttu-id="b9bc1-427">Você também pode mapear colunas de origem toocolumns de conjunto de dados do conjunto de coletor de dados na definição de atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="b9bc1-427">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="b9bc1-428">Para obter detalhes, confira [Mapear colunas de conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-428">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b9bc1-429">Desempenho e ajuste</span><span class="sxs-lookup"><span data-stu-id="b9bc1-429">Performance and tuning</span></span>
 <span data-ttu-id="b9bc1-430">toolearn sobre a chave de fatores que afetam o desempenho de saudação de movimentação de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias maneiras, consulte Olá [atividade de cópia guia de desempenho e ajuste](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="b9bc1-430">toolearn about key factors that impact hello performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>
