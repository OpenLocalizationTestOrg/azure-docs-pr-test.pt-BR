---
title: aaaMove dados de um servidor FTP por meio do Azure Data Factory | Microsoft Docs
description: Saiba mais sobre como toomove dados de um servidor FTP usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: eea3bab0-a6e4-4045-ad44-9ce06229c718
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: jingwang
ms.openlocfilehash: c707e29532b2a8a870603948cb6150ab857bd6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="cb04f-103">Mover dados de um servidor FTP usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="cb04f-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="cb04f-104">Este artigo explica como toouse hello atividade de cópia de dados do Azure Data Factory toomove de um servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="cb04f-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from an FTP server.</span></span> <span data-ttu-id="cb04f-105">Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb04f-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="cb04f-106">Você pode copiar dados de um repositório de dados de coletor do FTP servidor tooany com suporte.</span><span class="sxs-lookup"><span data-stu-id="cb04f-106">You can copy data from an FTP server tooany supported sink data store.</span></span> <span data-ttu-id="cb04f-107">Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela.</span><span class="sxs-lookup"><span data-stu-id="cb04f-107">For a list of data stores supported as sinks by hello copy activity, see hello [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="cb04f-108">Fábrica de dados atualmente suporta apenas armazena de movimentação de dados de uma data de tooother do servidor FTP, mas não movendo os dados de outros dados armazena server tooan FTP.</span><span class="sxs-lookup"><span data-stu-id="cb04f-108">Data Factory currently supports only moving data from an FTP server tooother data stores, but not moving data from other data stores tooan FTP server.</span></span> <span data-ttu-id="cb04f-109">Ele dá suporte a servidores FTP locais e em nuvem.</span><span class="sxs-lookup"><span data-stu-id="cb04f-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="cb04f-110">atividade de cópia de saudação não exclui o arquivo de origem Olá depois que ele destino toohello foram copiados com êxito.</span><span class="sxs-lookup"><span data-stu-id="cb04f-110">hello copy activity does not delete hello source file after it is successfully copied toohello destination.</span></span> <span data-ttu-id="cb04f-111">Se você precisar de arquivo de origem toodelete Olá após uma cópia com êxito, criar um arquivo de saudação toodelete atividade personalizada e use atividade Olá no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb04f-111">If you need toodelete hello source file after a successful copy, create a custom activity toodelete hello file, and use hello activity in hello pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="cb04f-112">Habilitar a conectividade</span><span class="sxs-lookup"><span data-stu-id="cb04f-112">Enable connectivity</span></span>
<span data-ttu-id="cb04f-113">Se você estiver movendo dados de um **local** armazenamento de dados de nuvem para tooa de servidor FTP (por exemplo, tooAzure armazenamento de Blob), instalar e usar o Gateway de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="cb04f-113">If you are moving data from an **on-premises** FTP server tooa cloud data store (for example, tooAzure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="cb04f-114">Olá Gateway de gerenciamento de dados é um agente de cliente que está instalado em seu computador local e permite que o recurso de local de tooan de tooconnect de serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="cb04f-114">hello Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services tooconnect tooan on-premises resource.</span></span> <span data-ttu-id="cb04f-115">Para ver os detalhes, consulte [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="cb04f-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="cb04f-116">Para obter instruções passo a passo de configuração de gateway hello e usá-lo, consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="cb04f-116">For step-by-step instructions on setting up hello gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="cb04f-117">Usar o servidor FTP de tooan tooconnect do gateway Olá, mesmo se o servidor de saudação estiver em uma infraestrutura do Azure como uma máquina virtual (VM) de serviço (IaaS).</span><span class="sxs-lookup"><span data-stu-id="cb04f-117">You use hello gateway tooconnect tooan FTP server, even if hello server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="cb04f-118">É possível tooinstall Olá gateway Olá mesmo no local máquina ou VM IaaS como Olá servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="cb04f-118">It is possible tooinstall hello gateway on hello same on-premises machine or IaaS VM as hello FTP server.</span></span> <span data-ttu-id="cb04f-119">No entanto, recomendamos que você instale o gateway de saudação em um computador separado ou a contenção de recursos do IaaS VM tooavoid e para melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="cb04f-119">However, we recommend that you install hello gateway on a separate machine or IaaS VM tooavoid resource contention, and for better performance.</span></span> <span data-ttu-id="cb04f-120">Quando você instalar o gateway de saudação em um computador separado, máquina Olá deve ser tooaccess capaz de servidor FTP de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb04f-120">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="cb04f-121">Introdução</span><span class="sxs-lookup"><span data-stu-id="cb04f-121">Get started</span></span>
<span data-ttu-id="cb04f-122">Você pode criar um pipeline com uma atividade de cópia que move dados de uma origem FTP usando diferentes ferramentas ou APIs.</span><span class="sxs-lookup"><span data-stu-id="cb04f-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="cb04f-123">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de fábrica de dados**.</span><span class="sxs-lookup"><span data-stu-id="cb04f-123">hello easiest way toocreate a pipeline is toouse hello **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="cb04f-124">Veja o [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para obter um passo a passo rápido.</span><span class="sxs-lookup"><span data-stu-id="cb04f-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="cb04f-125">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **PowerShell**, **modelo do Azure Resource Manager**, **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="cb04f-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="cb04f-126">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="cb04f-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="cb04f-127">Se você usar ferramentas de saudação ou APIs, execute Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb04f-127">Whether you use hello tools or APIs, perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="cb04f-128">Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.</span><span class="sxs-lookup"><span data-stu-id="cb04f-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="cb04f-129">Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.</span><span class="sxs-lookup"><span data-stu-id="cb04f-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="cb04f-130">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="cb04f-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="cb04f-131">Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="cb04f-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="cb04f-132">Quando você usar ferramentas ou APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb04f-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="cb04f-133">Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados FTP, consulte Olá [exemplo JSON: copiar dados de blob de tooAzure do servidor FTP](#json-example-copy-data-from-ftp-server-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="cb04f-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an FTP data store, see hello [JSON example: Copy data from FTP server tooAzure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="cb04f-134">Para obter detalhes sobre toouse de formatos de arquivo e compactação com suporte, consulte [compactação formatos de arquivo e no Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="cb04f-134">For details about supported file and compression formats toouse, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="cb04f-135">Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooFTP.</span><span class="sxs-lookup"><span data-stu-id="cb04f-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooFTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="cb04f-136">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="cb04f-136">Linked service properties</span></span>
<span data-ttu-id="cb04f-137">Olá, a tabela a seguir descreve o serviço FTP vinculada do JSON elementos tooan específico.</span><span class="sxs-lookup"><span data-stu-id="cb04f-137">hello following table describes JSON elements specific tooan FTP linked service.</span></span>

| <span data-ttu-id="cb04f-138">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cb04f-138">Property</span></span> | <span data-ttu-id="cb04f-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="cb04f-139">Description</span></span> | <span data-ttu-id="cb04f-140">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="cb04f-140">Required</span></span> | <span data-ttu-id="cb04f-141">Padrão</span><span class="sxs-lookup"><span data-stu-id="cb04f-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cb04f-142">type</span><span class="sxs-lookup"><span data-stu-id="cb04f-142">type</span></span> |<span data-ttu-id="cb04f-143">Defina este tooFtpServer.</span><span class="sxs-lookup"><span data-stu-id="cb04f-143">Set this tooFtpServer.</span></span> |<span data-ttu-id="cb04f-144">Sim</span><span class="sxs-lookup"><span data-stu-id="cb04f-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="cb04f-145">host</span><span class="sxs-lookup"><span data-stu-id="cb04f-145">host</span></span> |<span data-ttu-id="cb04f-146">Especifique o nome de saudação ou endereço IP do servidor FTP hello.</span><span class="sxs-lookup"><span data-stu-id="cb04f-146">Specify hello name or IP address of hello FTP server.</span></span> |<span data-ttu-id="cb04f-147">Sim</span><span class="sxs-lookup"><span data-stu-id="cb04f-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="cb04f-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="cb04f-148">authenticationType</span></span> |<span data-ttu-id="cb04f-149">Especifique o tipo de autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb04f-149">Specify hello authentication type.</span></span> |<span data-ttu-id="cb04f-150">Sim</span><span class="sxs-lookup"><span data-stu-id="cb04f-150">Yes</span></span> |<span data-ttu-id="cb04f-151">Básica, Anônima</span><span class="sxs-lookup"><span data-stu-id="cb04f-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="cb04f-152">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="cb04f-152">username</span></span> |<span data-ttu-id="cb04f-153">Especifica usuário Olá que tem o servidor FTP toohello acesso.</span><span class="sxs-lookup"><span data-stu-id="cb04f-153">Specify hello user who has access toohello FTP server.</span></span> |<span data-ttu-id="cb04f-154">Não</span><span class="sxs-lookup"><span data-stu-id="cb04f-154">No</span></span> |&nbsp; |
| <span data-ttu-id="cb04f-155">Senha</span><span class="sxs-lookup"><span data-stu-id="cb04f-155">password</span></span> |<span data-ttu-id="cb04f-156">Especifique a senha de saudação para usuário hello (nome de usuário).</span><span class="sxs-lookup"><span data-stu-id="cb04f-156">Specify hello password for hello user (username).</span></span> |<span data-ttu-id="cb04f-157">Não</span><span class="sxs-lookup"><span data-stu-id="cb04f-157">No</span></span> |&nbsp; |
| <span data-ttu-id="cb04f-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="cb04f-158">encryptedCredential</span></span> |<span data-ttu-id="cb04f-159">Especifica servidor de saudação FTP Olá criptografado credencial tooaccess.</span><span class="sxs-lookup"><span data-stu-id="cb04f-159">Specify hello encrypted credential tooaccess hello FTP server.</span></span> |<span data-ttu-id="cb04f-160">Não</span><span class="sxs-lookup"><span data-stu-id="cb04f-160">No</span></span> |&nbsp; |
| <span data-ttu-id="cb04f-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="cb04f-161">gatewayName</span></span> |<span data-ttu-id="cb04f-162">Especifique o nome de saudação do gateway Olá no servidor do Gateway de gerenciamento de dados tooconnect tooan local FTP.</span><span class="sxs-lookup"><span data-stu-id="cb04f-162">Specify hello name of hello gateway in Data Management Gateway tooconnect tooan on-premises FTP server.</span></span> |<span data-ttu-id="cb04f-163">Não</span><span class="sxs-lookup"><span data-stu-id="cb04f-163">No</span></span> |&nbsp; |
| <span data-ttu-id="cb04f-164">porta</span><span class="sxs-lookup"><span data-stu-id="cb04f-164">port</span></span> |<span data-ttu-id="cb04f-165">Especifique a porta de saudação na qual Olá FTP server está escutando.</span><span class="sxs-lookup"><span data-stu-id="cb04f-165">Specify hello port on which hello FTP server is listening.</span></span> |<span data-ttu-id="cb04f-166">Não</span><span class="sxs-lookup"><span data-stu-id="cb04f-166">No</span></span> |<span data-ttu-id="cb04f-167">21</span><span class="sxs-lookup"><span data-stu-id="cb04f-167">21</span></span> |
| <span data-ttu-id="cb04f-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="cb04f-168">enableSsl</span></span> |<span data-ttu-id="cb04f-169">Especifique se toouse FTP por um canal SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="cb04f-169">Specify whether toouse FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="cb04f-170">Não</span><span class="sxs-lookup"><span data-stu-id="cb04f-170">No</span></span> |<span data-ttu-id="cb04f-171">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="cb04f-171">true</span></span> |
| <span data-ttu-id="cb04f-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="cb04f-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="cb04f-173">Especifique se o servidor de tooenable SSL a validação de certificado quando você estiver usando o FTP por canal SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="cb04f-173">Specify whether tooenable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="cb04f-174">Não</span><span class="sxs-lookup"><span data-stu-id="cb04f-174">No</span></span> |<span data-ttu-id="cb04f-175">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="cb04f-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="cb04f-176">Usar autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="cb04f-176">Use Anonymous authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {        
            "authenticationType": "Anonymous",
              "host": "myftpserver.com"
        }
    }
}
```

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="cb04f-177">Usar nome de usuário e senha em texto sem formatação para autenticação básica</span><span class="sxs-lookup"><span data-stu-id="cb04f-177">Use username and password in plain text for basic authentication</span></span>

```JSON
{
    "name": "FTPLinkedService",
      "properties": {
    "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
      }
}
```

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="cb04f-178">Usar a porta, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="cb04f-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="cb04f-179">Usar encryptedCredential para autenticação e gateway</span><span class="sxs-lookup"><span data-stu-id="cb04f-179">Use encryptedCredential for authentication and gateway</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "mygateway"
        }
      }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="cb04f-180">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="cb04f-180">Dataset properties</span></span>
<span data-ttu-id="cb04f-181">Para obter uma lista completa das seções e propriedades disponíveis para definir os conjuntos de dados, confira [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="cb04f-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="cb04f-182">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="cb04f-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="cb04f-183">Olá **typeProperties** seção é diferente para cada tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="cb04f-183">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="cb04f-184">Ele fornece informações de tipo de conjunto de dados toohello específico.</span><span class="sxs-lookup"><span data-stu-id="cb04f-184">It provides information that is specific toohello dataset type.</span></span> <span data-ttu-id="cb04f-185">Olá **typeProperties** seção um conjunto de dados do tipo **FileShare** tem Olá propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb04f-185">hello **typeProperties** section for a dataset of type **FileShare** has hello following properties:</span></span>

| <span data-ttu-id="cb04f-186">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cb04f-186">Property</span></span> | <span data-ttu-id="cb04f-187">Descrição</span><span class="sxs-lookup"><span data-stu-id="cb04f-187">Description</span></span> | <span data-ttu-id="cb04f-188">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="cb04f-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cb04f-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="cb04f-189">folderPath</span></span> |<span data-ttu-id="cb04f-190">Pasta de toohello subcaminho.</span><span class="sxs-lookup"><span data-stu-id="cb04f-190">Subpath toohello folder.</span></span> <span data-ttu-id="cb04f-191">Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb04f-191">Use escape character ‘ \ ’ for special characters in hello string.</span></span> <span data-ttu-id="cb04f-192">Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="cb04f-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="cb04f-193">Você pode combinar essa propriedade com **partitionBy** toohave caminhos de pastas com base na fatia início e término do data.</span><span class="sxs-lookup"><span data-stu-id="cb04f-193">You can combine this property with **partitionBy** toohave folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="cb04f-194">Sim</span><span class="sxs-lookup"><span data-stu-id="cb04f-194">Yes</span></span> |
| <span data-ttu-id="cb04f-195">fileName</span><span class="sxs-lookup"><span data-stu-id="cb04f-195">fileName</span></span> |<span data-ttu-id="cb04f-196">Especifique o nome de saudação do arquivo de saudação em Olá **folderPath** se você quiser Olá tabela toorefer tooa arquivo específico na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="cb04f-196">Specify hello name of hello file in hello **folderPath** if you want hello table toorefer tooa specific file in hello folder.</span></span> <span data-ttu-id="cb04f-197">Se você não especificar qualquer valor para essa propriedade, a tabela de saudação aponta tooall arquivos na pasta hello.</span><span class="sxs-lookup"><span data-stu-id="cb04f-197">If you do not specify any value for this property, hello table points tooall files in hello folder.</span></span><br/><br/><span data-ttu-id="cb04f-198">Quando **fileName** não for especificado para um conjunto de dados de saída, nome de saudação do arquivo hello gerado está em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb04f-198">When **fileName** is not specified for an output dataset, hello name of hello generated file is in hello following format:</span></span> <br/><br/><span data-ttu-id="cb04f-199">Data.<Guid>.txt (exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="cb04f-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="cb04f-200">Não</span><span class="sxs-lookup"><span data-stu-id="cb04f-200">No</span></span> |
| <span data-ttu-id="cb04f-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="cb04f-201">fileFilter</span></span> |<span data-ttu-id="cb04f-202">Especifique um tooselect toobe usado do filtro um subconjunto de arquivos no hello **folderPath**, em vez de todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="cb04f-202">Specify a filter toobe used tooselect a subset of files in hello **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="cb04f-203">Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).</span><span class="sxs-lookup"><span data-stu-id="cb04f-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="cb04f-204">Exemplo 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="cb04f-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="cb04f-205">Exemplo 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="cb04f-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="cb04f-206">**fileFilter** é aplicável a um conjunto de dados FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="cb04f-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="cb04f-207">Essa propriedade não tem suporte no HDFS (Sistema de Arquivos Distribuído Hadoop).</span><span class="sxs-lookup"><span data-stu-id="cb04f-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="cb04f-208">Não</span><span class="sxs-lookup"><span data-stu-id="cb04f-208">No</span></span> |
| <span data-ttu-id="cb04f-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="cb04f-209">partitionedBy</span></span> |<span data-ttu-id="cb04f-210">Usado toospecify um dinâmico **folderPath** e **fileName** para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="cb04f-210">Used toospecify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="cb04f-211">Por exemplo, você pode especificar um **folderPath** que é parametrizada para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="cb04f-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="cb04f-212">Não</span><span class="sxs-lookup"><span data-stu-id="cb04f-212">No</span></span> |
| <span data-ttu-id="cb04f-213">formato</span><span class="sxs-lookup"><span data-stu-id="cb04f-213">format</span></span> | <span data-ttu-id="cb04f-214">Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="cb04f-214">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="cb04f-215">Saudação de conjunto **tipo** propriedade em formato tooone desses valores.</span><span class="sxs-lookup"><span data-stu-id="cb04f-215">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="cb04f-216">Para obter mais informações, consulte Olá [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Parquet formato ](data-factory-supported-file-and-compression-formats.md#parquet-format) seções.</span><span class="sxs-lookup"><span data-stu-id="cb04f-216">For more information, see hello [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="cb04f-217">Se você quiser toocopy arquivos como eles estão entre repositórios baseada em arquivo (cópia binário), ignore a seção de formato de saudação em ambas as definições de conjunto de dados de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="cb04f-217">If you want toocopy files as they are between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="cb04f-218">Não</span><span class="sxs-lookup"><span data-stu-id="cb04f-218">No</span></span> |
| <span data-ttu-id="cb04f-219">compactação</span><span class="sxs-lookup"><span data-stu-id="cb04f-219">compression</span></span> | <span data-ttu-id="cb04f-220">Especifica tipo de saudação e nível de compactação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb04f-220">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="cb04f-221">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**; e os níveis com suporte são: **Ideal** e **Mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="cb04f-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="cb04f-222">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="cb04f-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="cb04f-223">Não</span><span class="sxs-lookup"><span data-stu-id="cb04f-223">No</span></span> |
| <span data-ttu-id="cb04f-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="cb04f-224">useBinaryTransfer</span></span> |<span data-ttu-id="cb04f-225">Especifique se binário de saudação toouse modo de transferência.</span><span class="sxs-lookup"><span data-stu-id="cb04f-225">Specify whether toouse hello binary transfer mode.</span></span> <span data-ttu-id="cb04f-226">os valores Hello são true para o modo binário (esse é o valor de padrão de saudação) e false para ASCII.</span><span class="sxs-lookup"><span data-stu-id="cb04f-226">hello values are true for binary mode (this is hello default value), and false for ASCII.</span></span> <span data-ttu-id="cb04f-227">Esta propriedade só pode ser usada quando hello tipo de serviço vinculado associado é do tipo: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="cb04f-227">This property can only be used when hello associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="cb04f-228">Não</span><span class="sxs-lookup"><span data-stu-id="cb04f-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="cb04f-229">**fileName** e **fileFilter** não podem ser usados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="cb04f-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-hello-partionedby-property"></a><span data-ttu-id="cb04f-230">Usar a propriedade partionedBy Olá</span><span class="sxs-lookup"><span data-stu-id="cb04f-230">Use hello partionedBy property</span></span>
<span data-ttu-id="cb04f-231">Como mencionado na seção anterior hello, você pode especificar um dinâmico **folderPath** e **fileName** para dados de série temporal com hello **partitionedBy** propriedade.</span><span class="sxs-lookup"><span data-stu-id="cb04f-231">As mentioned in hello previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with hello **partitionedBy** property.</span></span>

<span data-ttu-id="cb04f-232">toolearn sobre conjuntos de dados de série de tempo, planejamento e fatias, consulte [criando conjuntos de dados](data-factory-create-datasets.md), [de agendamento e execução](data-factory-scheduling-and-execution.md), e [criar pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="cb04f-232">toolearn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="cb04f-233">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="cb04f-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="cb04f-234">Neste exemplo, {Slice} é substituído pelo valor de saudação de variável SliceStart de fábrica de dados do sistema, Olá formato (AAAAMMDDHH) especificado.</span><span class="sxs-lookup"><span data-stu-id="cb04f-234">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart, in hello format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="cb04f-235">Olá SliceStart refere-se toostart tempo da fração de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb04f-235">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="cb04f-236">caminho da pasta Olá é diferente para cada fatia.</span><span class="sxs-lookup"><span data-stu-id="cb04f-236">hello folder path is different for each slice.</span></span> <span data-ttu-id="cb04f-237">(Por exemplo, wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.)</span><span class="sxs-lookup"><span data-stu-id="cb04f-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="cb04f-238">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="cb04f-238">Sample 2</span></span>

```json
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
<span data-ttu-id="cb04f-239">Neste exemplo, ano hello, mês, dia e hora de SliceStart são extraídos em variáveis separadas que são usadas por Olá **folderPath** e **fileName** propriedades.</span><span class="sxs-lookup"><span data-stu-id="cb04f-239">In this example, hello year, month, day, and time of SliceStart are extracted into separate variables that are used by hello **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="cb04f-240">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="cb04f-240">Copy activity properties</span></span>
<span data-ttu-id="cb04f-241">Para obter uma lista completa das seções e propriedades disponíveis para definir as atividades, consulte [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="cb04f-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="cb04f-242">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="cb04f-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="cb04f-243">As propriedades disponíveis no hello **typeProperties** seção hello atividade em Olá outro lado, variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="cb04f-243">Properties available in hello **typeProperties** section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="cb04f-244">Para a atividade de cópia hello, propriedades de tipo hello variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="cb04f-244">For hello copy activity, hello type properties vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="cb04f-245">Atividade de cópia, quando a fonte de saudação é do tipo **FileSystemSource**, Olá propriedade a seguir está disponível em **typeProperties** seção:</span><span class="sxs-lookup"><span data-stu-id="cb04f-245">In copy activity, when hello source is of type **FileSystemSource**, hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="cb04f-246">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cb04f-246">Property</span></span> | <span data-ttu-id="cb04f-247">Descrição</span><span class="sxs-lookup"><span data-stu-id="cb04f-247">Description</span></span> | <span data-ttu-id="cb04f-248">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="cb04f-248">Allowed values</span></span> | <span data-ttu-id="cb04f-249">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="cb04f-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cb04f-250">recursiva</span><span class="sxs-lookup"><span data-stu-id="cb04f-250">recursive</span></span> |<span data-ttu-id="cb04f-251">Indica se os dados saudação é lida recursivamente de subpastas de saudação ou somente de pasta especificado hello.</span><span class="sxs-lookup"><span data-stu-id="cb04f-251">Indicates whether hello data is read recursively from hello subfolders, or only from hello specified folder.</span></span> |<span data-ttu-id="cb04f-252">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="cb04f-252">True, False (default)</span></span> |<span data-ttu-id="cb04f-253">Não</span><span class="sxs-lookup"><span data-stu-id="cb04f-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-tooazure-blob"></a><span data-ttu-id="cb04f-254">Exemplo JSON: copiar dados do servidor FTP tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="cb04f-254">JSON example: Copy data from FTP server tooAzure Blob</span></span>
<span data-ttu-id="cb04f-255">Este exemplo mostra como toocopy dados de um servidor FTP tooAzure armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="cb04f-255">This sample shows how toocopy data from an FTP server tooAzure Blob storage.</span></span> <span data-ttu-id="cb04f-256">No entanto, os dados podem ser copiados diretamente tooany de saudação coletores Olá indicado em [suporte para armazenamentos de dados e formatos](data-factory-data-movement-activities.md#supported-data-stores-and-formats), usando a atividade de cópia de saudação na fábrica de dados.</span><span class="sxs-lookup"><span data-stu-id="cb04f-256">However, data can be copied directly tooany of hello sinks stated in hello [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using hello copy activity in Data Factory.</span></span>  

<span data-ttu-id="cb04f-257">Olá, exemplos a seguir fornecem as definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="cb04f-257">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="cb04f-258">Um serviço vinculado do tipo [FtpServer](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="cb04f-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="cb04f-259">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="cb04f-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="cb04f-260">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [FileShare](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="cb04f-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="cb04f-261">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="cb04f-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="cb04f-262">Um [pipeline](data-factory-create-pipelines.md) com a atividade de cópia que usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="cb04f-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="cb04f-263">exemplo Hello copia dados de um servidor FTP tooan BLOBs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="cb04f-263">hello sample copies data from an FTP server tooan Azure blob every hour.</span></span> <span data-ttu-id="cb04f-264">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb04f-264">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="cb04f-265">Serviço vinculado de FTP</span><span class="sxs-lookup"><span data-stu-id="cb04f-265">FTP linked service</span></span>

<span data-ttu-id="cb04f-266">Este exemplo usa autenticação básica, com o nome de usuário de saudação e a senha em texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="cb04f-266">This example uses basic authentication, with hello user name and password in plain text.</span></span> <span data-ttu-id="cb04f-267">Você também pode usar uma saudação maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb04f-267">You can also use one of hello following ways:</span></span>

* <span data-ttu-id="cb04f-268">Autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="cb04f-268">Anonymous authentication</span></span>
* <span data-ttu-id="cb04f-269">Autenticação básica com credenciais criptografadas</span><span class="sxs-lookup"><span data-stu-id="cb04f-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="cb04f-270">FTPS (FTP sobre SSL/TLS)</span><span class="sxs-lookup"><span data-stu-id="cb04f-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="cb04f-271">Consulte Olá [serviço vinculado do FTP](#linked-service-properties) seção para diferentes tipos de autenticação que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="cb04f-271">See hello [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "FTPLinkedService",
    "properties": {
    "type": "FtpServer",
    "typeProperties": {
        "host": "myftpserver.com",           
        "authenticationType": "Basic",
        "username": "Admin",
        "password": "123456"
    }
  }
}
```
### <a name="azure-storage-linked-service"></a><span data-ttu-id="cb04f-272">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="cb04f-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="cb04f-273">Conjunto de dados de entrada de FTP</span><span class="sxs-lookup"><span data-stu-id="cb04f-273">FTP input dataset</span></span>

<span data-ttu-id="cb04f-274">Este conjunto de dados se refere a pasta toohello FTP `mysharedfolder` e o arquivo `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="cb04f-274">This dataset refers toohello FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="cb04f-275">pipeline de saudação copia o destino de toohello arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="cb04f-275">hello pipeline copies hello file toohello destination.</span></span>

<span data-ttu-id="cb04f-276">Configuração **externo** muito**true** informa ao serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="cb04f-276">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory, and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "FTPFileInput",
  "properties": {
    "type": "FileShare",
    "linkedServiceName": "FTPLinkedService",
    "typeProperties": {
      "folderPath": "mysharedfolder",
      "fileName": "test.csv",
      "useBinaryTransfer": true
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="cb04f-277">Conjunto de dados de saída de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="cb04f-277">Azure Blob output dataset</span></span>

<span data-ttu-id="cb04f-278">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="cb04f-278">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="cb04f-279">caminho da pasta Olá blob Olá é avaliado dinamicamente, com base na hora de início de saudação da fatia Olá que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="cb04f-279">hello folder path for hello blob is dynamically evaluated, based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="cb04f-280">caminho da pasta Olá usa partes de ano, mês, dia e horário Olá Olá da hora de início.</span><span class="sxs-lookup"><span data-stu-id="cb04f-280">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/ftp/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="cb04f-281">Uma atividade de cópia em um pipeline com origem no sistema de arquivos e coletor de blobs</span><span class="sxs-lookup"><span data-stu-id="cb04f-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="cb04f-282">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="cb04f-282">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="cb04f-283">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**FileSystemSource**e hello **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="cb04f-283">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and hello **sink** type is set too**BlobSink**.</span></span>

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00Z",
        "end": "2016-08-24T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="cb04f-284">colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="cb04f-284">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb04f-285">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cb04f-285">Next steps</span></span>
<span data-ttu-id="cb04f-286">Consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb04f-286">See hello following articles:</span></span>

* <span data-ttu-id="cb04f-287">toolearn sobre a chave de fatores que afetam o desempenho de movimentação de dados (Copiar atividade) na fábrica de dados e toooptimize de várias maneiras, consulte Olá [Copiar atividade guia de desempenho e ajuste](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="cb04f-287">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="cb04f-288">Para obter instruções passo a passo para criar um pipeline com uma atividade de cópia, consulte Olá [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="cb04f-288">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
