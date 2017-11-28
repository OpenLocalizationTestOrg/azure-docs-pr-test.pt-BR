---
title: dados de aaaMove do HDFS local | Microsoft Docs
description: Saiba mais sobre como toomove dados de local HDFS usando o Azure Data Factory.
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
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a><span data-ttu-id="fa415-103">Mover dados do HDFS local usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="fa415-103">Move data from on-premises HDFS using Azure Data Factory</span></span>
<span data-ttu-id="fa415-104">Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove do HDFS local.</span><span class="sxs-lookup"><span data-stu-id="fa415-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises HDFS.</span></span> <span data-ttu-id="fa415-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa415-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="fa415-106">Você pode copiar dados de repositório de dados de coletor do HDFS tooany com suporte.</span><span class="sxs-lookup"><span data-stu-id="fa415-106">You can copy data from HDFS tooany supported sink data store.</span></span> <span data-ttu-id="fa415-107">Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="fa415-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="fa415-108">Fábrica de dados atualmente oferece suporte à movimentação de dados somente de um armazenamento de dados local HDFS tooother, mas não para mover dados de outros dados tooan repositórios locais HDFS.</span><span class="sxs-lookup"><span data-stu-id="fa415-108">Data factory currently supports only moving data from an on-premises HDFS tooother data stores, but not for moving data from other data stores tooan on-premises HDFS.</span></span>

> [!NOTE]
> <span data-ttu-id="fa415-109">Atividade de cópia não exclui o arquivo de origem Olá depois que ele destino toohello foram copiados com êxito.</span><span class="sxs-lookup"><span data-stu-id="fa415-109">Copy Activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="fa415-110">Se precisar de arquivo de origem toodelete Olá após uma cópia bem-sucedida, criar um arquivo de saudação toodelete atividade personalizada e usar a atividade Olá no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa415-110">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file and use hello activity in hello pipeline.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="fa415-111">Habilitando a conectividade</span><span class="sxs-lookup"><span data-stu-id="fa415-111">Enabling connectivity</span></span>
<span data-ttu-id="fa415-112">Serviço de fábrica de dados oferece suporte à conexão HDFS local tooon usando Olá Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="fa415-112">Data Factory service supports connecting tooon-premises HDFS using hello Data Management Gateway.</span></span> <span data-ttu-id="fa415-113">Consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Gateway de gerenciamento de dados e instruções passo a passo sobre como configurar o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa415-113">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="fa415-114">Use Olá gateway tooconnect tooHDFS mesmo se ele está hospedado em uma VM de IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa415-114">Use hello gateway tooconnect tooHDFS even if it is hosted in an Azure IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="fa415-115">Verifique Olá-se de que o Gateway de gerenciamento de dados pode acessar de forma muito**todos os** Olá [server do nó de nome]: [nome de porta de nó] e [servidores de nós de dados]: [porta de nó de dados] do cluster de Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="fa415-115">Make sure hello Data Management Gateway can access too**ALL** hello [name node server]:[name node port] and [data node servers]:[data node port] of hello Hadoop cluster.</span></span> <span data-ttu-id="fa415-116">A [porta do nó de nome] padrão é 50070, e a [porta do nó de dados] padrão é 50075.</span><span class="sxs-lookup"><span data-stu-id="fa415-116">Default [name node port] is 50070, and default [data node port] is 50075.</span></span>

<span data-ttu-id="fa415-117">Embora você possa instalar o gateway em Olá mesmo local máquina ou hello VM do Azure como Olá HDFS, recomendamos que você instale o gateway de saudação em um computador separado/Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="fa415-117">While you can install gateway on hello same on-premises machine or hello Azure VM as hello HDFS, we recommend that you install hello gateway on a separate machine/Azure IaaS VM.</span></span> <span data-ttu-id="fa415-118">Ter o gateway em um computador separado reduz a contenção de recursos e aprimora o desempenho.</span><span class="sxs-lookup"><span data-stu-id="fa415-118">Having gateway on a separate machine reduces resource contention and improves performance.</span></span> <span data-ttu-id="fa415-119">Quando você instalar o gateway de saudação em um computador separado, máquina Olá deve ser capaz de tooaccess máquina Olá Olá HDFS.</span><span class="sxs-lookup"><span data-stu-id="fa415-119">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello HDFS.</span></span>

## <a name="getting-started"></a><span data-ttu-id="fa415-120">Introdução</span><span class="sxs-lookup"><span data-stu-id="fa415-120">Getting started</span></span>
<span data-ttu-id="fa415-121">Você pode criar um pipeline com uma atividade de cópia que mova dados de uma origem HDFS usando diferentes ferramentas/APIs.</span><span class="sxs-lookup"><span data-stu-id="fa415-121">You can create a pipeline with a copy activity that moves data from a HDFS source by using different tools/APIs.</span></span>

<span data-ttu-id="fa415-122">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="fa415-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="fa415-123">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="fa415-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="fa415-124">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="fa415-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="fa415-125">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="fa415-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="fa415-126">Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa415-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="fa415-127">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="fa415-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="fa415-128">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="fa415-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="fa415-129">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="fa415-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="fa415-130">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="fa415-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="fa415-131">Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa415-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="fa415-132">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados do HDFS, consulte [exemplo JSON: copiar dados de local HDFS tooAzure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="fa415-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a HDFS data store, see [JSON example: Copy data from on-premises HDFS tooAzure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section of this article.</span></span>

<span data-ttu-id="fa415-133">Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específicas tooHDFS:</span><span class="sxs-lookup"><span data-stu-id="fa415-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooHDFS:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="fa415-134">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="fa415-134">Linked service properties</span></span>
<span data-ttu-id="fa415-135">Um serviço vinculado vincula uma fábrica de dados de tooa de repositório de dados.</span><span class="sxs-lookup"><span data-stu-id="fa415-135">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="fa415-136">Criar um serviço vinculado do tipo **Hdfs** toolink uma fábrica de dados local HDFS tooyour.</span><span class="sxs-lookup"><span data-stu-id="fa415-136">You create a linked service of type **Hdfs** toolink an on-premises HDFS tooyour data factory.</span></span> <span data-ttu-id="fa415-137">Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooHDFS vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="fa415-137">hello following table provides description for JSON elements specific tooHDFS linked service.</span></span>

| <span data-ttu-id="fa415-138">Propriedade</span><span class="sxs-lookup"><span data-stu-id="fa415-138">Property</span></span> | <span data-ttu-id="fa415-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="fa415-139">Description</span></span> | <span data-ttu-id="fa415-140">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fa415-140">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fa415-141">type</span><span class="sxs-lookup"><span data-stu-id="fa415-141">type</span></span> |<span data-ttu-id="fa415-142">propriedade de tipo Hello deve ser definida como: **Hdfs**</span><span class="sxs-lookup"><span data-stu-id="fa415-142">hello type property must be set to: **Hdfs**</span></span> |<span data-ttu-id="fa415-143">Sim</span><span class="sxs-lookup"><span data-stu-id="fa415-143">Yes</span></span> |
| <span data-ttu-id="fa415-144">Url</span><span class="sxs-lookup"><span data-stu-id="fa415-144">Url</span></span> |<span data-ttu-id="fa415-145">URL toohello HDFS</span><span class="sxs-lookup"><span data-stu-id="fa415-145">URL toohello HDFS</span></span> |<span data-ttu-id="fa415-146">Sim</span><span class="sxs-lookup"><span data-stu-id="fa415-146">Yes</span></span> |
| <span data-ttu-id="fa415-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="fa415-147">authenticationType</span></span> |<span data-ttu-id="fa415-148">Anônimo ou Windows.</span><span class="sxs-lookup"><span data-stu-id="fa415-148">Anonymous, or Windows.</span></span> <br><br> <span data-ttu-id="fa415-149">toouse **a autenticação Kerberos** para conector HDFS, consulte muito[nesta seção](#use-kerberos-authentication-for-hdfs-connector) tooset seu ambiente local adequadamente.</span><span class="sxs-lookup"><span data-stu-id="fa415-149">toouse **Kerberos authentication** for HDFS connector, refer too[this section](#use-kerberos-authentication-for-hdfs-connector) tooset up your on-premises environment accordingly.</span></span> |<span data-ttu-id="fa415-150">Sim</span><span class="sxs-lookup"><span data-stu-id="fa415-150">Yes</span></span> |
| <span data-ttu-id="fa415-151">userName</span><span class="sxs-lookup"><span data-stu-id="fa415-151">userName</span></span> |<span data-ttu-id="fa415-152">Nome de usuário para a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="fa415-152">Username for Windows authentication.</span></span> |<span data-ttu-id="fa415-153">Sim (para a Autenticação do Windows)</span><span class="sxs-lookup"><span data-stu-id="fa415-153">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="fa415-154">Senha</span><span class="sxs-lookup"><span data-stu-id="fa415-154">password</span></span> |<span data-ttu-id="fa415-155">Senha para a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="fa415-155">Password for Windows authentication.</span></span> |<span data-ttu-id="fa415-156">Sim (para a Autenticação do Windows)</span><span class="sxs-lookup"><span data-stu-id="fa415-156">Yes (for Windows Authentication)</span></span> |
| <span data-ttu-id="fa415-157">gatewayName</span><span class="sxs-lookup"><span data-stu-id="fa415-157">gatewayName</span></span> |<span data-ttu-id="fa415-158">Nome do gateway Olá Olá serviço da fábrica de dados deve usar tooconnect toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="fa415-158">Name of hello gateway that hello Data Factory service should use tooconnect toohello HDFS.</span></span> |<span data-ttu-id="fa415-159">Sim</span><span class="sxs-lookup"><span data-stu-id="fa415-159">Yes</span></span> |
| <span data-ttu-id="fa415-160">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="fa415-160">encryptedCredential</span></span> |<span data-ttu-id="fa415-161">[Novo AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) saída de credencial de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa415-161">[New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) output of hello access credential.</span></span> |<span data-ttu-id="fa415-162">Não</span><span class="sxs-lookup"><span data-stu-id="fa415-162">No</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="fa415-163">Usando a autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="fa415-163">Using Anonymous authentication</span></span>

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

### <a name="using-windows-authentication"></a><span data-ttu-id="fa415-164">Usando a autenticação do Windows</span><span class="sxs-lookup"><span data-stu-id="fa415-164">Using Windows authentication</span></span>

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
## <a name="dataset-properties"></a><span data-ttu-id="fa415-165">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="fa415-165">Dataset properties</span></span>
<span data-ttu-id="fa415-166">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="fa415-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="fa415-167">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="fa415-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="fa415-168">Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa415-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="fa415-169">Olá typeProperties seção de conjunto de dados do tipo **FileShare** (que inclui o conjunto de dados HDFS) tem Olá seguintes propriedades</span><span class="sxs-lookup"><span data-stu-id="fa415-169">hello typeProperties section for dataset of type **FileShare** (which includes HDFS dataset) has hello following properties</span></span>

| <span data-ttu-id="fa415-170">Propriedade</span><span class="sxs-lookup"><span data-stu-id="fa415-170">Property</span></span> | <span data-ttu-id="fa415-171">Descrição</span><span class="sxs-lookup"><span data-stu-id="fa415-171">Description</span></span> | <span data-ttu-id="fa415-172">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fa415-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="fa415-173">folderPath</span><span class="sxs-lookup"><span data-stu-id="fa415-173">folderPath</span></span> |<span data-ttu-id="fa415-174">Pasta de toohello de caminho.</span><span class="sxs-lookup"><span data-stu-id="fa415-174">Path toohello folder.</span></span> <span data-ttu-id="fa415-175">Exemplo: `myfolder`</span><span class="sxs-lookup"><span data-stu-id="fa415-175">Example: `myfolder`</span></span><br/><br/><span data-ttu-id="fa415-176">Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa415-176">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="fa415-177">Por exemplo: para pasta\subpasta, especifique a pasta\\\\subpasta e para d:\pastadeexemplo, especifique d:\\\\pastadeexemplo.</span><span class="sxs-lookup"><span data-stu-id="fa415-177">For example: for folder\subfolder, specify folder\\\\subfolder and for d:\samplefolder, specify d:\\\\samplefolder.</span></span><br/><br/><span data-ttu-id="fa415-178">Você pode combinar essa propriedade com **partitionBy** toohave caminhos de pastas com base na fatia datas / horas de início/término.</span><span class="sxs-lookup"><span data-stu-id="fa415-178">You can combine this property with **partitionBy** toohave folder paths based on slice start/end date-times.</span></span> |<span data-ttu-id="fa415-179">Sim</span><span class="sxs-lookup"><span data-stu-id="fa415-179">Yes</span></span> |
| <span data-ttu-id="fa415-180">fileName</span><span class="sxs-lookup"><span data-stu-id="fa415-180">fileName</span></span> |<span data-ttu-id="fa415-181">Especifique o nome de saudação do arquivo de saudação em Olá **folderPath** se você quiser Olá tabela toorefer tooa arquivo específico na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="fa415-181">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="fa415-182">Se você não especificar qualquer valor para essa propriedade, a tabela de saudação aponta tooall arquivos na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="fa415-182">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="fa415-183">Quando o nome de arquivo não for especificado para um conjunto de dados de saída, o nome de saudação do arquivo hello gerado aparecerá em Olá esse formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa415-183">When fileName is not specified for an output dataset, hello name of hello generated file would be in hello following this format:</span></span> <br/><br/><span data-ttu-id="fa415-184">Data<Guid>.txt (por exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="fa415-184">Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="fa415-185">Não</span><span class="sxs-lookup"><span data-stu-id="fa415-185">No</span></span> |
| <span data-ttu-id="fa415-186">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="fa415-186">partitionedBy</span></span> |<span data-ttu-id="fa415-187">partitionedBy pode ser usado toospecify um folderPath dinâmico, nome de arquivo para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="fa415-187">partitionedBy can be used toospecify a dynamic folderPath, filename for time series data.</span></span> <span data-ttu-id="fa415-188">Exemplo: folderPath parametrizado para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="fa415-188">Example: folderPath parameterized for every hour of data.</span></span> |<span data-ttu-id="fa415-189">Não</span><span class="sxs-lookup"><span data-stu-id="fa415-189">No</span></span> |
| <span data-ttu-id="fa415-190">formato</span><span class="sxs-lookup"><span data-stu-id="fa415-190">format</span></span> | <span data-ttu-id="fa415-191">Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="fa415-191">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="fa415-192">Saudação de conjunto **tipo** propriedade em formato tooone desses valores.</span><span class="sxs-lookup"><span data-stu-id="fa415-192">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="fa415-193">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="fa415-193">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="fa415-194">Se você quiser muito**copiar arquivos como-é** entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="fa415-194">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="fa415-195">Não</span><span class="sxs-lookup"><span data-stu-id="fa415-195">No</span></span> |
| <span data-ttu-id="fa415-196">compactação</span><span class="sxs-lookup"><span data-stu-id="fa415-196">compression</span></span> | <span data-ttu-id="fa415-197">Especifica tipo de saudação e nível de compactação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa415-197">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="fa415-198">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="fa415-198">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="fa415-199">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="fa415-199">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="fa415-200">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="fa415-200">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="fa415-201">Não</span><span class="sxs-lookup"><span data-stu-id="fa415-201">No</span></span> |

> [!NOTE]
> <span data-ttu-id="fa415-202">filename e fileFilter não podem ser usados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="fa415-202">filename and fileFilter cannot be used simultaneously.</span></span>

### <a name="using-partionedby-property"></a><span data-ttu-id="fa415-203">Usando a propriedade partionedBy</span><span class="sxs-lookup"><span data-stu-id="fa415-203">Using partionedBy property</span></span>
<span data-ttu-id="fa415-204">Como mencionado na seção anterior hello, você pode especificar um dinâmico folderPath e filename para dados de série temporal com hello **partitionedBy** propriedade [funções da fábrica de dados e variáveis de sistema Olá](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="fa415-204">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="fa415-205">toolearn mais informações sobre conjuntos de dados de série de tempo, planejamento e fatias, consulte [criando conjuntos de dados](data-factory-create-datasets.md), [de agendamento e execução](data-factory-scheduling-and-execution.md), e [criar Pipelines](data-factory-create-pipelines.md) artigos.</span><span class="sxs-lookup"><span data-stu-id="fa415-205">toolearn more about time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md), [Scheduling & Execution](data-factory-scheduling-and-execution.md), and [Creating Pipelines](data-factory-create-pipelines.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="fa415-206">Exemplo 1:</span><span class="sxs-lookup"><span data-stu-id="fa415-206">Sample 1:</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="fa415-207">Neste exemplo {Slice} é substituído pelo valor de saudação da variável de sistema SliceStart fábrica de dados no formato de saudação (AAAAMMDDHH) especificado.</span><span class="sxs-lookup"><span data-stu-id="fa415-207">In this example {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="fa415-208">Olá SliceStart refere-se toostart tempo da fração de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa415-208">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="fa415-209">Olá folderPath é diferente para cada fatia.</span><span class="sxs-lookup"><span data-stu-id="fa415-209">hello folderPath is different for each slice.</span></span> <span data-ttu-id="fa415-210">Por exemplo: wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.</span><span class="sxs-lookup"><span data-stu-id="fa415-210">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.</span></span>

#### <a name="sample-2"></a><span data-ttu-id="fa415-211">Exemplo 2:</span><span class="sxs-lookup"><span data-stu-id="fa415-211">Sample 2:</span></span>

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
<span data-ttu-id="fa415-212">Neste exemplo, ano, mês, dia e hora do SliceStart são extraídos em variáveis separadas que são usadas pelas propriedades folderPath e fileName.</span><span class="sxs-lookup"><span data-stu-id="fa415-212">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="fa415-213">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="fa415-213">Copy activity properties</span></span>
<span data-ttu-id="fa415-214">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="fa415-214">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="fa415-215">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="fa415-215">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="fa415-216">Por outro lado, as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="fa415-216">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="fa415-217">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="fa415-217">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="fa415-218">Para a atividade de cópia, quando a fonte é do tipo **FileSystemSource** Olá propriedades a seguir está disponível na seção de typeProperties:</span><span class="sxs-lookup"><span data-stu-id="fa415-218">For Copy Activity, when source is of type **FileSystemSource** hello following properties are available in typeProperties section:</span></span>

<span data-ttu-id="fa415-219">**FileSystemSource** dá suporte a saudação propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa415-219">**FileSystemSource** supports hello following properties:</span></span>

| <span data-ttu-id="fa415-220">Propriedade</span><span class="sxs-lookup"><span data-stu-id="fa415-220">Property</span></span> | <span data-ttu-id="fa415-221">Descrição</span><span class="sxs-lookup"><span data-stu-id="fa415-221">Description</span></span> | <span data-ttu-id="fa415-222">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="fa415-222">Allowed values</span></span> | <span data-ttu-id="fa415-223">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fa415-223">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="fa415-224">recursiva</span><span class="sxs-lookup"><span data-stu-id="fa415-224">recursive</span></span> |<span data-ttu-id="fa415-225">Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello.</span><span class="sxs-lookup"><span data-stu-id="fa415-225">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="fa415-226">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="fa415-226">True, False (default)</span></span> |<span data-ttu-id="fa415-227">Não</span><span class="sxs-lookup"><span data-stu-id="fa415-227">No</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="fa415-228">Formatos de arquivo e de compactação com suporte</span><span class="sxs-lookup"><span data-stu-id="fa415-228">Supported file and compression formats</span></span>
<span data-ttu-id="fa415-229">Consulte o artigo [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="fa415-229">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a><span data-ttu-id="fa415-230">Exemplo JSON: copiar dados de local HDFS tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="fa415-230">JSON example: Copy data from on-premises HDFS tooAzure Blob</span></span>
<span data-ttu-id="fa415-231">Este exemplo mostra como toocopy dados de um tooAzure HDFS local armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="fa415-231">This sample shows how toocopy data from an on-premises HDFS tooAzure Blob Storage.</span></span> <span data-ttu-id="fa415-232">No entanto, os dados podem ser copiados **diretamente** tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="fa415-232">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="fa415-233">exemplo Hello fornece definições de JSON para Olá entidades da fábrica de dados a seguir.</span><span class="sxs-lookup"><span data-stu-id="fa415-233">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="fa415-234">Você pode usar essas definições toocreate um pipeline toocopy os dados de HDFS tooAzure armazenamento de Blob usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fa415-234">You can use these definitions toocreate a pipeline toocopy data from HDFS tooAzure Blob Storage by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>

1. <span data-ttu-id="fa415-235">Um serviço vinculado do tipo [OnPremisesHdfs](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fa415-235">A linked service of type [OnPremisesHdfs](#linked-service-properties).</span></span>
2. <span data-ttu-id="fa415-236">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="fa415-236">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="fa415-237">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [FileShare](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fa415-237">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties).</span></span>
4. <span data-ttu-id="fa415-238">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="fa415-238">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="fa415-239">Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="fa415-239">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="fa415-240">exemplo Hello copia dados de um tooan HDFS local BLOBs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="fa415-240">hello sample copies data from an on-premises HDFS tooan Azure blob every hour.</span></span> <span data-ttu-id="fa415-241">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa415-241">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="fa415-242">Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa415-242">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="fa415-243">Olá instruções Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="fa415-243">hello instructions in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="fa415-244">**Serviço vinculado do HDFS:** Este exemplo usa Olá autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="fa415-244">**HDFS linked service:** This example uses hello Windows authentication.</span></span> <span data-ttu-id="fa415-245">Confira a seção [Serviço vinculado ao HDFS](#linked-service-properties) para diferentes tipos de autenticação que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="fa415-245">See [HDFS linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="fa415-246">**Serviço vinculado de armazenamento do Azure:**</span><span class="sxs-lookup"><span data-stu-id="fa415-246">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="fa415-247">**Conjunto de dados de entrada do HDFS:** este conjunto de dados refere-se a pasta HDFS toohello DataTransfer/UnitTest /.</span><span class="sxs-lookup"><span data-stu-id="fa415-247">**HDFS input dataset:** This dataset refers toohello HDFS folder DataTransfer/UnitTest/.</span></span> <span data-ttu-id="fa415-248">pipeline de saudação copia todos os arquivos de saudação nesse destino toohello de pasta.</span><span class="sxs-lookup"><span data-stu-id="fa415-248">hello pipeline copies all hello files in this folder toohello destination.</span></span>

<span data-ttu-id="fa415-249">Definindo "externo": "verdadeiro" informa serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="fa415-249">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="fa415-250">**Conjunto de dados de saída de Blob do Azure:**</span><span class="sxs-lookup"><span data-stu-id="fa415-250">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="fa415-251">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="fa415-251">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="fa415-252">caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="fa415-252">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="fa415-253">caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.</span><span class="sxs-lookup"><span data-stu-id="fa415-253">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="fa415-254">**Uma atividade de cópia em um pipeline com origem de Sistema de Arquivos e coletor Blob:**</span><span class="sxs-lookup"><span data-stu-id="fa415-254">**A copy activity in a pipeline with File System source and Blob sink:**</span></span>

<span data-ttu-id="fa415-255">pipeline de saudação contém uma atividade de cópia que esteja configurado toouse esses conjuntos de dados de entrada e saídos e toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="fa415-255">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="fa415-256">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**FileSystemSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="fa415-256">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="fa415-257">consulta SQL Olá especificada para Olá **consulta** propriedade seleciona dados Olá Olá após toocopy de hora.</span><span class="sxs-lookup"><span data-stu-id="fa415-257">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

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

## <a name="use-kerberos-authentication-for-hdfs-connector"></a><span data-ttu-id="fa415-258">Usar a autenticação Kerberos para o conector HDFS</span><span class="sxs-lookup"><span data-stu-id="fa415-258">Use Kerberos authentication for HDFS connector</span></span>
<span data-ttu-id="fa415-259">Há dois tooset de opções ambiente local de saudação assim como toouse a autenticação Kerberos no conector do HDFS.</span><span class="sxs-lookup"><span data-stu-id="fa415-259">There are two options tooset up hello on-premises environment so as toouse Kerberos Authentication in HDFS connector.</span></span> <span data-ttu-id="fa415-260">Você pode escolher Olá um melhor se adapta à sua ocorrência.</span><span class="sxs-lookup"><span data-stu-id="fa415-260">You can choose hello one better fits your case.</span></span>
* <span data-ttu-id="fa415-261">Opção 1: [Fazer com que o computador do gateway ingresse no realm Kerberos](#kerberos-join-realm)</span><span class="sxs-lookup"><span data-stu-id="fa415-261">Option 1: [Join gateway machine in Kerberos realm](#kerberos-join-realm)</span></span>
* <span data-ttu-id="fa415-262">Opção 2: [habilitar a confiança mútua entre o domínio do Windows e o realm Kerberos](#kerberos-mutual-trust)</span><span class="sxs-lookup"><span data-stu-id="fa415-262">Option 2: [Enable mutual trust between Windows domain and Kerberos realm](#kerberos-mutual-trust)</span></span>

### <span data-ttu-id="fa415-263"><a name="kerberos-join-realm"></a>Opção 1: Fazer com que o computador do gateway ingresse no realm Kerberos</span><span class="sxs-lookup"><span data-stu-id="fa415-263"><a name="kerberos-join-realm"></a>Option 1: Join gateway machine in Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="fa415-264">Requisito:</span><span class="sxs-lookup"><span data-stu-id="fa415-264">Requirement:</span></span>

* <span data-ttu-id="fa415-265">máquina de gateway Olá precisa de realm de Kerberos Olá toojoin e não pode ingressar em qualquer domínio do Windows.</span><span class="sxs-lookup"><span data-stu-id="fa415-265">hello gateway machine needs toojoin hello Kerberos realm and can’t join any Windows domain.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="fa415-266">Como tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="fa415-266">How tooconfigure:</span></span>

<span data-ttu-id="fa415-267">**No computador do gateway:**</span><span class="sxs-lookup"><span data-stu-id="fa415-267">**On gateway machine:**</span></span>

1.  <span data-ttu-id="fa415-268">Executar Olá **Ksetup** tooconfigure utilitário Olá servidor KDC do Kerberos e o realm.</span><span class="sxs-lookup"><span data-stu-id="fa415-268">Run hello **Ksetup** utility tooconfigure hello Kerberos KDC server and realm.</span></span>

    <span data-ttu-id="fa415-269">máquina Olá deve ser configurada como um membro de um grupo de trabalho como um realm Kerberos é diferente de um domínio do Windows.</span><span class="sxs-lookup"><span data-stu-id="fa415-269">hello machine must be configured as a member of a workgroup since a Kerberos realm is different from a Windows domain.</span></span> <span data-ttu-id="fa415-270">Isso pode ser feito definindo o realm de Kerberos hello e adicionar um servidor KDC da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="fa415-270">This can be achieved by setting hello Kerberos realm and adding a KDC server as follows.</span></span> <span data-ttu-id="fa415-271">Substitua *REALM.COM* pelo seu respectivo realm, conforme a necessidade.</span><span class="sxs-lookup"><span data-stu-id="fa415-271">Replace *REALM.COM* with your own respective realm as needed.</span></span>

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    <span data-ttu-id="fa415-272">**Reiniciar** máquina Olá após executar esses comandos de 2.</span><span class="sxs-lookup"><span data-stu-id="fa415-272">**Restart** hello machine after executing these 2 commands.</span></span>

2.  <span data-ttu-id="fa415-273">Verificar a configuração de saudação com **Ksetup** comando.</span><span class="sxs-lookup"><span data-stu-id="fa415-273">Verify hello configuration with **Ksetup** command.</span></span> <span data-ttu-id="fa415-274">saída de Hello deve ser como:</span><span class="sxs-lookup"><span data-stu-id="fa415-274">hello output should be like:</span></span>

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

<span data-ttu-id="fa415-275">**No Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="fa415-275">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="fa415-276">Configurar usando o conector Olá HDFS **autenticação do Windows** junto com o Kerberos principal nome e senha tooconnect toohello HDFS fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="fa415-276">Configure hello HDFS connector using **Windows authentication** together with your Kerberos principal name and password tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="fa415-277">Verifique a seção de [propriedades do Serviço Vinculado HDFS](#linked-service-properties) nos detalhes da configuração.</span><span class="sxs-lookup"><span data-stu-id="fa415-277">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

### <span data-ttu-id="fa415-278"><a name="kerberos-mutual-trust"></a>Opção 2: habilitar a confiança mútua entre o domínio do Windows e o realm Kerberos</span><span class="sxs-lookup"><span data-stu-id="fa415-278"><a name="kerberos-mutual-trust"></a>Option 2: Enable mutual trust between Windows domain and Kerberos realm</span></span>

#### <a name="requirement"></a><span data-ttu-id="fa415-279">Requisito:</span><span class="sxs-lookup"><span data-stu-id="fa415-279">Requirement:</span></span>
*   <span data-ttu-id="fa415-280">máquina de gateway Olá deve ingressar em um domínio do Windows.</span><span class="sxs-lookup"><span data-stu-id="fa415-280">hello gateway machine must join a Windows domain.</span></span>
*   <span data-ttu-id="fa415-281">Você precisar de configurações de permissão tooupdate Olá controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="fa415-281">You need permission tooupdate hello domain controller's settings.</span></span>

#### <a name="how-tooconfigure"></a><span data-ttu-id="fa415-282">Como tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="fa415-282">How tooconfigure:</span></span>

> [!NOTE]
> <span data-ttu-id="fa415-283">Substitua REALM.COM e AD.COM em Olá tutorial com sua respectivo realm e controlador de domínio a seguir conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="fa415-283">Replace REALM.COM and AD.COM in hello following tutorial with your own respective realm and domain controller as needed.</span></span>

<span data-ttu-id="fa415-284">**No servidor KDC:**</span><span class="sxs-lookup"><span data-stu-id="fa415-284">**On KDC server:**</span></span>

1.  <span data-ttu-id="fa415-285">Edita a configuração do KDC Olá no **krb5** toolet arquivo KDC confiança referência toohello seguindo o modelo de configuração de domínio do Windows.</span><span class="sxs-lookup"><span data-stu-id="fa415-285">Edit hello KDC configuration in **krb5.conf** file toolet KDC trust Windows Domain referring toohello following configuration template.</span></span> <span data-ttu-id="fa415-286">Por padrão, a configuração de saudação está localizada em **/etc/krb5.conf**.</span><span class="sxs-lookup"><span data-stu-id="fa415-286">By default, hello configuration is located at **/etc/krb5.conf**.</span></span>

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

  <span data-ttu-id="fa415-287">**Reiniciar** Olá serviço KDC após a configuração.</span><span class="sxs-lookup"><span data-stu-id="fa415-287">**Restart** hello KDC service after configuration.</span></span>

2.  <span data-ttu-id="fa415-288">Preparar uma entidade nomeada  **krbtgt/REALM.COM@AD.COM**  no servidor do KDC com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa415-288">Prepare a principal named **krbtgt/REALM.COM@AD.COM** in KDC server with hello following command:</span></span>

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  <span data-ttu-id="fa415-289">No arquivo de configuração de serviço HDFS **hadoop.security.auth_to_local**, adicione `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span><span class="sxs-lookup"><span data-stu-id="fa415-289">In **hadoop.security.auth_to_local** HDFS service configuration file, add `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.</span></span>

<span data-ttu-id="fa415-290">**No controlador de domínio:**</span><span class="sxs-lookup"><span data-stu-id="fa415-290">**On domain controller:**</span></span>

1.  <span data-ttu-id="fa415-291">Execute seguinte Olá **Ksetup** tooadd uma entrada de realm de comandos:</span><span class="sxs-lookup"><span data-stu-id="fa415-291">Run hello following **Ksetup** commands tooadd a realm entry:</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  <span data-ttu-id="fa415-292">Estabelece relação de confiança de Realm de tooKerberos de domínio do Windows.</span><span class="sxs-lookup"><span data-stu-id="fa415-292">Establish trust from Windows Domain tooKerberos Realm.</span></span> <span data-ttu-id="fa415-293">[senha] é a senha de saudação para entidade Olá  **krbtgt/REALM.COM@AD.COM** .</span><span class="sxs-lookup"><span data-stu-id="fa415-293">[password] is hello password for hello principal **krbtgt/REALM.COM@AD.COM**.</span></span>

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  <span data-ttu-id="fa415-294">Selecione o algoritmo de criptografia usado no Kerberos.</span><span class="sxs-lookup"><span data-stu-id="fa415-294">Select encryption algorithm used in Kerberos.</span></span>

    1. <span data-ttu-id="fa415-295">Vá tooServer Manager > Gerenciamento de diretiva de grupo > domínio > objetos de diretiva de grupo > padrão ou política de domínio do Active e editar.</span><span class="sxs-lookup"><span data-stu-id="fa415-295">Go tooServer Manager > Group Policy Management > Domain > Group Policy Objects > Default or Active Domain Policy, and Edit.</span></span>

    2. <span data-ttu-id="fa415-296">Em Olá **Editor de gerenciamento de política de grupo** janela pop-up, vá tooComputer Configuração > Políticas > configurações do Windows > configurações de segurança > políticas locais > Opções de segurança e configurar **rede segurança: configurar tipos de criptografia permitidos para o Kerberos**.</span><span class="sxs-lookup"><span data-stu-id="fa415-296">In hello **Group Policy Management Editor** popup window, go tooComputer Configuration > Policies > Windows Settings > Security Settings > Local Policies > Security Options, and configure **Network security: Configure Encryption types allowed for Kerberos**.</span></span>

    3. <span data-ttu-id="fa415-297">Algoritmo de criptografia Olá selecione deseja toouse quando se conectar tooKDC.</span><span class="sxs-lookup"><span data-stu-id="fa415-297">Select hello encryption algorithm you want toouse when connect tooKDC.</span></span> <span data-ttu-id="fa415-298">Normalmente, basta selecionar todas as opções de saudação.</span><span class="sxs-lookup"><span data-stu-id="fa415-298">Commonly, you can simply select all hello options.</span></span>

        ![Configuração dos tipos de criptografia para Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. <span data-ttu-id="fa415-300">Use **Ksetup** toobe comando toospecify Olá criptografia algoritmo usado em Olá TERRITÓRIO específico.</span><span class="sxs-lookup"><span data-stu-id="fa415-300">Use **Ksetup** command toospecify hello encryption algorithm toobe used on hello specific REALM.</span></span>

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  <span data-ttu-id="fa415-301">Crie mapeamento de saudação entre a conta de domínio hello e Kerberos principal, em ordem toouse Kerberos principal no domínio do Windows.</span><span class="sxs-lookup"><span data-stu-id="fa415-301">Create hello mapping between hello domain account and Kerberos principal, in order toouse Kerberos principal in Windows Domain.</span></span>

    1. <span data-ttu-id="fa415-302">Iniciar ferramentas administrativas hello > **computadores e usuários do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fa415-302">Start hello Administrative tools > **Active Directory Users and Computers**.</span></span>

    2. <span data-ttu-id="fa415-303">Configure recursos avançados clicando em **Exibir** > **Recursos Avançados**.</span><span class="sxs-lookup"><span data-stu-id="fa415-303">Configure advanced features by clicking **View** > **Advanced Features**.</span></span>

    3. <span data-ttu-id="fa415-304">Localizar Olá conta toowhich toocreate mapeamentos de desejado e clique tooview **mapeamentos de nome** > clique **nomes Kerberos** guia.</span><span class="sxs-lookup"><span data-stu-id="fa415-304">Locate hello account toowhich you want toocreate mappings, and right-click tooview **Name Mappings** > click **Kerberos Names** tab.</span></span>

    4. <span data-ttu-id="fa415-305">Adicione uma entidade de território hello.</span><span class="sxs-lookup"><span data-stu-id="fa415-305">Add a principal from hello realm.</span></span>

        ![Mapear identidade de segurança](media/data-factory-hdfs-connector/map-security-identity.png)

<span data-ttu-id="fa415-307">**No computador do gateway:**</span><span class="sxs-lookup"><span data-stu-id="fa415-307">**On gateway machine:**</span></span>

* <span data-ttu-id="fa415-308">Execute seguinte Olá **Ksetup** comandos tooadd uma entrada de território.</span><span class="sxs-lookup"><span data-stu-id="fa415-308">Run hello following **Ksetup** commands tooadd a realm entry.</span></span>

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

<span data-ttu-id="fa415-309">**No Azure Data Factory:**</span><span class="sxs-lookup"><span data-stu-id="fa415-309">**In Azure Data Factory:**</span></span>

* <span data-ttu-id="fa415-310">Configurar usando o conector Olá HDFS **autenticação do Windows** junto com sua conta de domínio ou uma fonte de dados Principal Kerberos tooconnect toohello HDFS.</span><span class="sxs-lookup"><span data-stu-id="fa415-310">Configure hello HDFS connector using **Windows authentication** together with either your Domain Account or Kerberos Principal tooconnect toohello HDFS data source.</span></span> <span data-ttu-id="fa415-311">Verifique a seção de [propriedades do Serviço Vinculado HDFS](#linked-service-properties) nos detalhes da configuração.</span><span class="sxs-lookup"><span data-stu-id="fa415-311">Check [HDFS Linked Service properties](#linked-service-properties) section on configuration details.</span></span>

> [!NOTE]
> <span data-ttu-id="fa415-312">colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="fa415-312">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="performance-and-tuning"></a><span data-ttu-id="fa415-313">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="fa415-313">Performance and Tuning</span></span>
<span data-ttu-id="fa415-314">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="fa415-314">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
