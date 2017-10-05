---
title: Mover dados do servidor FTP usando o Azure Data Factory | Microsoft Docs
description: Saiba como mover dados de um servidor FTP usando o Azure Data Factory.
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
ms.openlocfilehash: f8f31f3a2ee02c964737dd32145499f3dcfd0624
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-ftp-server-by-using-azure-data-factory"></a><span data-ttu-id="16d25-103">Mover dados de um servidor FTP usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="16d25-103">Move data from an FTP server by using Azure Data Factory</span></span>
<span data-ttu-id="16d25-104">Este artigo explica como usar a atividade de cópia no Azure Data Factory para mover dados de um servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="16d25-104">This article explains how to use the copy activity in Azure Data Factory to move data from an FTP server.</span></span> <span data-ttu-id="16d25-105">Ele se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral da movimentação de dados com a atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="16d25-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="16d25-106">Você pode copiar dados de um servidor FTP para qualquer repositório de dados de coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="16d25-106">You can copy data from an FTP server to any supported sink data store.</span></span> <span data-ttu-id="16d25-107">Para obter uma lista de repositórios de dados com suporte como coletores da atividade de cópia, confira a tabela [Repositórios de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="16d25-107">For a list of data stores supported as sinks by the copy activity, see the [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="16d25-108">Atualmente, o data factory dá suporte apenas à movimentação de dados de um servidor FTP para outros repositórios de dados, mas não para a movimentação de dados de outros repositórios de dados para um servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="16d25-108">Data Factory currently supports only moving data from an FTP server to other data stores, but not moving data from other data stores to an FTP server.</span></span> <span data-ttu-id="16d25-109">Ele dá suporte a servidores FTP locais e em nuvem.</span><span class="sxs-lookup"><span data-stu-id="16d25-109">It supports both on-premises and cloud FTP servers.</span></span>

> [!NOTE]
> <span data-ttu-id="16d25-110">A atividade de cópia não exclui o arquivo de origem depois que ele é copiado com êxito para o destino.</span><span class="sxs-lookup"><span data-stu-id="16d25-110">The copy activity does not delete the source file after it is successfully copied to the destination.</span></span> <span data-ttu-id="16d25-111">Se precisar excluir o arquivo de origem após uma cópia bem-sucedida, crie uma atividade personalizada para excluir o arquivo e use a atividade no pipeline.</span><span class="sxs-lookup"><span data-stu-id="16d25-111">If you need to delete the source file after a successful copy, create a custom activity to delete the file, and use the activity in the pipeline.</span></span> 

## <a name="enable-connectivity"></a><span data-ttu-id="16d25-112">Habilitar a conectividade</span><span class="sxs-lookup"><span data-stu-id="16d25-112">Enable connectivity</span></span>
<span data-ttu-id="16d25-113">Se você estiver movendo dados de um servidor FTP **local** para um armazenamento de dados em nuvem (por exemplo, para o Armazenamento de Blobs do Azure), instale e use o Gateway de Gerenciamento de Dados.</span><span class="sxs-lookup"><span data-stu-id="16d25-113">If you are moving data from an **on-premises** FTP server to a cloud data store (for example, to Azure Blob storage), install and use Data Management Gateway.</span></span> <span data-ttu-id="16d25-114">O Gateway de Gerenciamento de Dados é um agente cliente instalado em seu computador local que permite aos serviços de nuvem conectarem-se a recursos locais.</span><span class="sxs-lookup"><span data-stu-id="16d25-114">The Data Management Gateway is a client agent that is installed on your on-premises machine, and it allows cloud services to connect to an on-premises resource.</span></span> <span data-ttu-id="16d25-115">Para ver os detalhes, consulte [Gateway de Gerenciamento de Dados](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="16d25-115">For details, see [Data Management Gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="16d25-116">Para ver instruções passo a passo sobre como configurar o gateway e usá-lo, consulte [Mover dados entre pontos locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="16d25-116">For step-by-step instructions on setting up the gateway and using it, see [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md).</span></span> <span data-ttu-id="16d25-117">Use o gateway para conectar-se a um servidor FTP mesmo que o servidor esteja em uma VM (máquina virtual) de IaaS (infraestrutura como serviço) do Azure.</span><span class="sxs-lookup"><span data-stu-id="16d25-117">You use the gateway to connect to an FTP server, even if the server is on an Azure infrastructure as a service (IaaS) virtual machine (VM).</span></span>

<span data-ttu-id="16d25-118">É possível instalar o gateway no mesmo computador local ou na VM IaaS que o servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="16d25-118">It is possible to install the gateway on the same on-premises machine or IaaS VM as the FTP server.</span></span> <span data-ttu-id="16d25-119">No entanto, recomendamos que você instale o gateway em uma máquina separada/VM IaaS para evitar a contenção de recursos e para melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="16d25-119">However, we recommend that you install the gateway on a separate machine or IaaS VM to avoid resource contention, and for better performance.</span></span> <span data-ttu-id="16d25-120">Ao instalar o gateway em um computador separado, o computador deverá ser capaz de acessar o servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="16d25-120">When you install the gateway on a separate machine, the machine should be able to access the FTP server.</span></span>

## <a name="get-started"></a><span data-ttu-id="16d25-121">Introdução</span><span class="sxs-lookup"><span data-stu-id="16d25-121">Get started</span></span>
<span data-ttu-id="16d25-122">Você pode criar um pipeline com uma atividade de cópia que move dados de uma origem FTP usando diferentes ferramentas ou APIs.</span><span class="sxs-lookup"><span data-stu-id="16d25-122">You can create a pipeline with a copy activity that moves data from an FTP source by using different tools or APIs.</span></span>

<span data-ttu-id="16d25-123">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia do Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="16d25-123">The easiest way to create a pipeline is to use the **Data Factory Copy Wizard**.</span></span> <span data-ttu-id="16d25-124">Veja o [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para obter um passo a passo rápido.</span><span class="sxs-lookup"><span data-stu-id="16d25-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough.</span></span>

<span data-ttu-id="16d25-125">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="16d25-125">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="16d25-126">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="16d25-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="16d25-127">Ao usar as ferramentas ou APIs, você executa as seguintes etapas para criar um pipeline que move dados de um armazenamento de dados de origem para um armazenamento de dados de coletor:</span><span class="sxs-lookup"><span data-stu-id="16d25-127">Whether you use the tools or APIs, perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="16d25-128">Criar **serviços vinculados** para vincular repositórios de dados de entrada e saída ao seu data factory.</span><span class="sxs-lookup"><span data-stu-id="16d25-128">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="16d25-129">Criar **conjuntos de dados** para representar dados de entrada e saída para a operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="16d25-129">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="16d25-130">Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.</span><span class="sxs-lookup"><span data-stu-id="16d25-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="16d25-131">Ao usar o assistente, as definições de JSON para essas entidades do Data Factory (serviços vinculados, conjuntos de dados e o pipeline) são automaticamente criadas para você.</span><span class="sxs-lookup"><span data-stu-id="16d25-131">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="16d25-132">Ao usar ferramentas ou APIs (exceto a API .NET), você define essas entidades do Data Factory usando o formato JSON.</span><span class="sxs-lookup"><span data-stu-id="16d25-132">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="16d25-133">Para obter um exemplo com definições de JSON para entidades do Data Factory que são usadas para copiar dados de um armazenamento de dados FTP, confira a seção [Exemplo de JSON: copiar dados do servidor FTP para o blob do Azure](#json-example-copy-data-from-ftp-server-to-azure-blob) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="16d25-133">For a sample with JSON definitions for Data Factory entities that are used to copy data from an FTP data store, see the [JSON example: Copy data from FTP server to Azure blob](#json-example-copy-data-from-ftp-server-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="16d25-134">Para obter detalhes sobre os formatos de arquivo e de compactação com suporte para uso, consulte [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="16d25-134">For details about supported file and compression formats to use, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="16d25-135">As seções que se seguem fornecem detalhes sobre as propriedades JSON que são usadas para definir entidades do Data Factory específicas ao FTP.</span><span class="sxs-lookup"><span data-stu-id="16d25-135">The following sections provide details about JSON properties that are used to define Data Factory entities specific to FTP.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="16d25-136">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="16d25-136">Linked service properties</span></span>
<span data-ttu-id="16d25-137">A tabela a seguir descreve elementos JSON específicos para um serviço FTP vinculado.</span><span class="sxs-lookup"><span data-stu-id="16d25-137">The following table describes JSON elements specific to an FTP linked service.</span></span>

| <span data-ttu-id="16d25-138">Propriedade</span><span class="sxs-lookup"><span data-stu-id="16d25-138">Property</span></span> | <span data-ttu-id="16d25-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="16d25-139">Description</span></span> | <span data-ttu-id="16d25-140">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="16d25-140">Required</span></span> | <span data-ttu-id="16d25-141">Padrão</span><span class="sxs-lookup"><span data-stu-id="16d25-141">Default</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="16d25-142">type</span><span class="sxs-lookup"><span data-stu-id="16d25-142">type</span></span> |<span data-ttu-id="16d25-143">Defina isso para FtpServer.</span><span class="sxs-lookup"><span data-stu-id="16d25-143">Set this to FtpServer.</span></span> |<span data-ttu-id="16d25-144">Sim</span><span class="sxs-lookup"><span data-stu-id="16d25-144">Yes</span></span> |&nbsp; |
| <span data-ttu-id="16d25-145">host</span><span class="sxs-lookup"><span data-stu-id="16d25-145">host</span></span> |<span data-ttu-id="16d25-146">Especifique o nome ou endereço IP do servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="16d25-146">Specify the name or IP address of the FTP server.</span></span> |<span data-ttu-id="16d25-147">Sim</span><span class="sxs-lookup"><span data-stu-id="16d25-147">Yes</span></span> |&nbsp; |
| <span data-ttu-id="16d25-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="16d25-148">authenticationType</span></span> |<span data-ttu-id="16d25-149">Especifique o tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="16d25-149">Specify the authentication type.</span></span> |<span data-ttu-id="16d25-150">Sim</span><span class="sxs-lookup"><span data-stu-id="16d25-150">Yes</span></span> |<span data-ttu-id="16d25-151">Básica, Anônima</span><span class="sxs-lookup"><span data-stu-id="16d25-151">Basic, Anonymous</span></span> |
| <span data-ttu-id="16d25-152">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="16d25-152">username</span></span> |<span data-ttu-id="16d25-153">Especifique o usuário que tem acesso ao servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="16d25-153">Specify the user who has access to the FTP server.</span></span> |<span data-ttu-id="16d25-154">Não</span><span class="sxs-lookup"><span data-stu-id="16d25-154">No</span></span> |&nbsp; |
| <span data-ttu-id="16d25-155">Senha</span><span class="sxs-lookup"><span data-stu-id="16d25-155">password</span></span> |<span data-ttu-id="16d25-156">Especifique a senha para o usuário (nome de usuário).</span><span class="sxs-lookup"><span data-stu-id="16d25-156">Specify the password for the user (username).</span></span> |<span data-ttu-id="16d25-157">Não</span><span class="sxs-lookup"><span data-stu-id="16d25-157">No</span></span> |&nbsp; |
| <span data-ttu-id="16d25-158">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="16d25-158">encryptedCredential</span></span> |<span data-ttu-id="16d25-159">Especifique a credencial criptografada para acessar o servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="16d25-159">Specify the encrypted credential to access the FTP server.</span></span> |<span data-ttu-id="16d25-160">Não</span><span class="sxs-lookup"><span data-stu-id="16d25-160">No</span></span> |&nbsp; |
| <span data-ttu-id="16d25-161">gatewayName</span><span class="sxs-lookup"><span data-stu-id="16d25-161">gatewayName</span></span> |<span data-ttu-id="16d25-162">Especifique o nome do gateway no Gateway de Gerenciamento de Dados para se conectar a um servidor FTP local.</span><span class="sxs-lookup"><span data-stu-id="16d25-162">Specify the name of the gateway in Data Management Gateway to connect to an on-premises FTP server.</span></span> |<span data-ttu-id="16d25-163">Não</span><span class="sxs-lookup"><span data-stu-id="16d25-163">No</span></span> |&nbsp; |
| <span data-ttu-id="16d25-164">porta</span><span class="sxs-lookup"><span data-stu-id="16d25-164">port</span></span> |<span data-ttu-id="16d25-165">Especifique a porta ouvida pelo servidor FTP.</span><span class="sxs-lookup"><span data-stu-id="16d25-165">Specify the port on which the FTP server is listening.</span></span> |<span data-ttu-id="16d25-166">Não</span><span class="sxs-lookup"><span data-stu-id="16d25-166">No</span></span> |<span data-ttu-id="16d25-167">21</span><span class="sxs-lookup"><span data-stu-id="16d25-167">21</span></span> |
| <span data-ttu-id="16d25-168">enableSsl</span><span class="sxs-lookup"><span data-stu-id="16d25-168">enableSsl</span></span> |<span data-ttu-id="16d25-169">Especifique se o canal FTP sobre SSL/TLS deve ser usado.</span><span class="sxs-lookup"><span data-stu-id="16d25-169">Specify whether to use FTP over an SSL/TLS channel.</span></span> |<span data-ttu-id="16d25-170">Não</span><span class="sxs-lookup"><span data-stu-id="16d25-170">No</span></span> |<span data-ttu-id="16d25-171">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="16d25-171">true</span></span> |
| <span data-ttu-id="16d25-172">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="16d25-172">enableServerCertificateValidation</span></span> |<span data-ttu-id="16d25-173">Especifique se deseja habilitar a validação do certificado SSL do servidor ao usar o canal FTP sobre SSL/TLS.</span><span class="sxs-lookup"><span data-stu-id="16d25-173">Specify whether to enable server SSL certificate validation when you are using FTP over SSL/TLS channel.</span></span> |<span data-ttu-id="16d25-174">Não</span><span class="sxs-lookup"><span data-stu-id="16d25-174">No</span></span> |<span data-ttu-id="16d25-175">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="16d25-175">true</span></span> |

### <a name="use-anonymous-authentication"></a><span data-ttu-id="16d25-176">Usar autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="16d25-176">Use Anonymous authentication</span></span>

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

### <a name="use-username-and-password-in-plain-text-for-basic-authentication"></a><span data-ttu-id="16d25-177">Usar nome de usuário e senha em texto sem formatação para autenticação básica</span><span class="sxs-lookup"><span data-stu-id="16d25-177">Use username and password in plain text for basic authentication</span></span>

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

### <a name="use-port-enablessl-enableservercertificatevalidation"></a><span data-ttu-id="16d25-178">Usar a porta, enableSsl, enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="16d25-178">Use port, enableSsl, enableServerCertificateValidation</span></span>

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

### <a name="use-encryptedcredential-for-authentication-and-gateway"></a><span data-ttu-id="16d25-179">Usar encryptedCredential para autenticação e gateway</span><span class="sxs-lookup"><span data-stu-id="16d25-179">Use encryptedCredential for authentication and gateway</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="16d25-180">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="16d25-180">Dataset properties</span></span>
<span data-ttu-id="16d25-181">Para obter uma lista completa das seções e propriedades disponíveis para definir os conjuntos de dados, confira [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="16d25-181">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> <span data-ttu-id="16d25-182">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="16d25-182">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="16d25-183">A seção **typeProperties** é diferente para cada tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="16d25-183">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="16d25-184">Ela fornece informações específicas ao tipo de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="16d25-184">It provides information that is specific to the dataset type.</span></span> <span data-ttu-id="16d25-185">A seção **typeProperties** para o conjunto de dados do tipo **FileShare** tem as propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="16d25-185">The **typeProperties** section for a dataset of type **FileShare** has the following properties:</span></span>

| <span data-ttu-id="16d25-186">Propriedade</span><span class="sxs-lookup"><span data-stu-id="16d25-186">Property</span></span> | <span data-ttu-id="16d25-187">Descrição</span><span class="sxs-lookup"><span data-stu-id="16d25-187">Description</span></span> | <span data-ttu-id="16d25-188">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="16d25-188">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="16d25-189">folderPath</span><span class="sxs-lookup"><span data-stu-id="16d25-189">folderPath</span></span> |<span data-ttu-id="16d25-190">Subcaminho para a pasta.</span><span class="sxs-lookup"><span data-stu-id="16d25-190">Subpath to the folder.</span></span> <span data-ttu-id="16d25-191">Use o caractere de escape ' \ ' para caracteres especiais na cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="16d25-191">Use escape character ‘ \ ’ for special characters in the string.</span></span> <span data-ttu-id="16d25-192">Confira [Definições de conjunto de dados e serviço vinculado de exemplo](#sample-linked-service-and-dataset-definitions) para obter exemplos.</span><span class="sxs-lookup"><span data-stu-id="16d25-192">See [Sample linked service and dataset definitions](#sample-linked-service-and-dataset-definitions) for examples.</span></span><br/><br/><span data-ttu-id="16d25-193">Você pode combinar essa propriedade com **partitionBy** para ter caminhos de pastas com base na fatia de data/hora de início e término.</span><span class="sxs-lookup"><span data-stu-id="16d25-193">You can combine this property with **partitionBy** to have folder paths based on slice start and end date-times.</span></span> |<span data-ttu-id="16d25-194">Sim</span><span class="sxs-lookup"><span data-stu-id="16d25-194">Yes</span></span> |
| <span data-ttu-id="16d25-195">fileName</span><span class="sxs-lookup"><span data-stu-id="16d25-195">fileName</span></span> |<span data-ttu-id="16d25-196">Especifique o nome do arquivo no **folderPath** se quiser que a tabela se refira a um arquivo específico na pasta.</span><span class="sxs-lookup"><span data-stu-id="16d25-196">Specify the name of the file in the **folderPath** if you want the table to refer to a specific file in the folder.</span></span> <span data-ttu-id="16d25-197">Se você não especificar algum valor para essa propriedade, a tabela apontará para todos os arquivos na pasta.</span><span class="sxs-lookup"><span data-stu-id="16d25-197">If you do not specify any value for this property, the table points to all files in the folder.</span></span><br/><br/><span data-ttu-id="16d25-198">Quando o **fileName** não for especificado para um conjunto de dados de saída, o nome do arquivo gerado será no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="16d25-198">When **fileName** is not specified for an output dataset, the name of the generated file is in the following format:</span></span> <br/><br/><span data-ttu-id="16d25-199">Data.<Guid>.txt (exemplo: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span><span class="sxs-lookup"><span data-stu-id="16d25-199">Data.<Guid>.txt (Example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt)</span></span> |<span data-ttu-id="16d25-200">Não</span><span class="sxs-lookup"><span data-stu-id="16d25-200">No</span></span> |
| <span data-ttu-id="16d25-201">fileFilter</span><span class="sxs-lookup"><span data-stu-id="16d25-201">fileFilter</span></span> |<span data-ttu-id="16d25-202">Especifique um filtro a ser usado para selecionar um subconjunto de arquivos no **folderPath** em vez de todos os arquivos.</span><span class="sxs-lookup"><span data-stu-id="16d25-202">Specify a filter to be used to select a subset of files in the **folderPath**, rather than all files.</span></span><br/><br/><span data-ttu-id="16d25-203">Os valores permitidos são: `*` (vários caracteres) e `?` (um único caractere).</span><span class="sxs-lookup"><span data-stu-id="16d25-203">Allowed values are: `*` (multiple characters) and `?` (single character).</span></span><br/><br/><span data-ttu-id="16d25-204">Exemplo 1: `"fileFilter": "*.log"`</span><span class="sxs-lookup"><span data-stu-id="16d25-204">Example 1: `"fileFilter": "*.log"`</span></span><br/><span data-ttu-id="16d25-205">Exemplo 2: `"fileFilter": 2014-1-?.txt"`</span><span class="sxs-lookup"><span data-stu-id="16d25-205">Example 2: `"fileFilter": 2014-1-?.txt"`</span></span><br/><br/> <span data-ttu-id="16d25-206">**fileFilter** é aplicável a um conjunto de dados FileShare de entrada.</span><span class="sxs-lookup"><span data-stu-id="16d25-206">**fileFilter** is applicable for an input FileShare dataset.</span></span> <span data-ttu-id="16d25-207">Essa propriedade não tem suporte no HDFS (Sistema de Arquivos Distribuído Hadoop).</span><span class="sxs-lookup"><span data-stu-id="16d25-207">This property is not supported with Hadoop Distributed File System (HDFS).</span></span> |<span data-ttu-id="16d25-208">Não</span><span class="sxs-lookup"><span data-stu-id="16d25-208">No</span></span> |
| <span data-ttu-id="16d25-209">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="16d25-209">partitionedBy</span></span> |<span data-ttu-id="16d25-210">Usado especificar um **folderPath** dinâmico e o **fileName** para dados de série temporal.</span><span class="sxs-lookup"><span data-stu-id="16d25-210">Used to specify a dynamic **folderPath** and **fileName** for time series data.</span></span> <span data-ttu-id="16d25-211">Por exemplo, você pode especificar um **folderPath** que é parametrizada para cada hora dos dados.</span><span class="sxs-lookup"><span data-stu-id="16d25-211">For example, you can specify a **folderPath** that is parameterized for every hour of data.</span></span> |<span data-ttu-id="16d25-212">Não</span><span class="sxs-lookup"><span data-stu-id="16d25-212">No</span></span> |
| <span data-ttu-id="16d25-213">formato</span><span class="sxs-lookup"><span data-stu-id="16d25-213">format</span></span> | <span data-ttu-id="16d25-214">Há suporte para os seguintes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="16d25-214">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="16d25-215">Defina a propriedade **type** sob formato como um desses valores.</span><span class="sxs-lookup"><span data-stu-id="16d25-215">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="16d25-216">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format) e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="16d25-216">For more information, see the [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="16d25-217">Se você quiser copiar arquivos no estado em que se encontram entre repositórios baseados em arquivo (cópia binária), ignore a seção de formato nas duas definições de conjunto de dados de entrada e de saída.</span><span class="sxs-lookup"><span data-stu-id="16d25-217">If you want to copy files as they are between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="16d25-218">Não</span><span class="sxs-lookup"><span data-stu-id="16d25-218">No</span></span> |
| <span data-ttu-id="16d25-219">compactação</span><span class="sxs-lookup"><span data-stu-id="16d25-219">compression</span></span> | <span data-ttu-id="16d25-220">Especifique o tipo e o nível de compactação para os dados.</span><span class="sxs-lookup"><span data-stu-id="16d25-220">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="16d25-221">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**; e os níveis com suporte são: **Ideal** e **Mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="16d25-221">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**, and supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="16d25-222">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="16d25-222">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="16d25-223">Não</span><span class="sxs-lookup"><span data-stu-id="16d25-223">No</span></span> |
| <span data-ttu-id="16d25-224">useBinaryTransfer</span><span class="sxs-lookup"><span data-stu-id="16d25-224">useBinaryTransfer</span></span> |<span data-ttu-id="16d25-225">Especifique se o modo de transferência binário deve ser usado.</span><span class="sxs-lookup"><span data-stu-id="16d25-225">Specify whether to use the binary transfer mode.</span></span> <span data-ttu-id="16d25-226">Os valores são true para o modo binário (esse é o valor padrão) e false para ASCII.</span><span class="sxs-lookup"><span data-stu-id="16d25-226">The values are true for binary mode (this is the default value), and false for ASCII.</span></span> <span data-ttu-id="16d25-227">Essa propriedade só pode ser usada quando o tipo de serviço vinculado associado for do tipo: FtpServer.</span><span class="sxs-lookup"><span data-stu-id="16d25-227">This property can only be used when the associated linked service type is of type: FtpServer.</span></span> |<span data-ttu-id="16d25-228">Não</span><span class="sxs-lookup"><span data-stu-id="16d25-228">No</span></span> |

> [!NOTE]
> <span data-ttu-id="16d25-229">**fileName** e **fileFilter** não podem ser usados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="16d25-229">**fileName** and **fileFilter** cannot be used simultaneously.</span></span>

### <a name="use-the-partionedby-property"></a><span data-ttu-id="16d25-230">Usar a propriedade partionedBy</span><span class="sxs-lookup"><span data-stu-id="16d25-230">Use the partionedBy property</span></span>
<span data-ttu-id="16d25-231">Conforme mencionado na seção anterior, você pode especificar um **folderPath** e um **fileName** dinâmicos para dados de série temporal com a propriedade **partitionedBy**.</span><span class="sxs-lookup"><span data-stu-id="16d25-231">As mentioned in the previous section, you can specify a dynamic **folderPath** and **fileName** for time series data with the **partitionedBy** property.</span></span>

<span data-ttu-id="16d25-232">Consulte [Criando conjuntos de dados](data-factory-create-datasets.md), [Agendamento e execução](data-factory-scheduling-and-execution.md) e [Criando pipelines](data-factory-create-pipelines.md) para saber mais sobre conjuntos de dados de série temporal, agendamentos e fatias.</span><span class="sxs-lookup"><span data-stu-id="16d25-232">To learn about time series datasets, scheduling, and slices, see [Creating datasets](data-factory-create-datasets.md), [Scheduling and execution](data-factory-scheduling-and-execution.md), and [Creating pipelines](data-factory-create-pipelines.md).</span></span>

#### <a name="sample-1"></a><span data-ttu-id="16d25-233">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="16d25-233">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
<span data-ttu-id="16d25-234">Nesse exemplo, {Slice} é substituído pelo valor da variável de sistema SliceStart do Data Factory no formato (AAAAMMDDHH) especificado.</span><span class="sxs-lookup"><span data-stu-id="16d25-234">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart, in the format specified (YYYYMMDDHH).</span></span> <span data-ttu-id="16d25-235">O SliceStart refere-se à hora de início da fatia.</span><span class="sxs-lookup"><span data-stu-id="16d25-235">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="16d25-236">O caminho da pasta é diferente para cada fatia.</span><span class="sxs-lookup"><span data-stu-id="16d25-236">The folder path is different for each slice.</span></span> <span data-ttu-id="16d25-237">(Por exemplo, wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.)</span><span class="sxs-lookup"><span data-stu-id="16d25-237">(For example, wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104.)</span></span>

#### <a name="sample-2"></a><span data-ttu-id="16d25-238">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="16d25-238">Sample 2</span></span>

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
<span data-ttu-id="16d25-239">Neste exemplo, ano, mês, dia e hora do SliceStart são extraídos em variáveis separadas que são usadas pelas propriedades **folderPath** e **fileName**.</span><span class="sxs-lookup"><span data-stu-id="16d25-239">In this example, the year, month, day, and time of SliceStart are extracted into separate variables that are used by the **folderPath** and **fileName** properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="16d25-240">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="16d25-240">Copy activity properties</span></span>
<span data-ttu-id="16d25-241">Para obter uma lista completa das seções e propriedades disponíveis para definir as atividades, consulte [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="16d25-241">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="16d25-242">As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.</span><span class="sxs-lookup"><span data-stu-id="16d25-242">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="16d25-243">As propriedades disponíveis na seção **typeProperties** da atividade, por outro lado, variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="16d25-243">Properties available in the **typeProperties** section of the activity, on the other hand, vary with each activity type.</span></span> <span data-ttu-id="16d25-244">Para a atividade de cópia, as propriedades de tipo variam conforme os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="16d25-244">For the copy activity, the type properties vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="16d25-245">Na atividade de cópia quando a fonte for do tipo **FileSystemSource**, as propriedades a seguir estarão disponíveis na seção **typeProperties**:</span><span class="sxs-lookup"><span data-stu-id="16d25-245">In copy activity, when the source is of type **FileSystemSource**, the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="16d25-246">Propriedade</span><span class="sxs-lookup"><span data-stu-id="16d25-246">Property</span></span> | <span data-ttu-id="16d25-247">Descrição</span><span class="sxs-lookup"><span data-stu-id="16d25-247">Description</span></span> | <span data-ttu-id="16d25-248">Valores permitidos</span><span class="sxs-lookup"><span data-stu-id="16d25-248">Allowed values</span></span> | <span data-ttu-id="16d25-249">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="16d25-249">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="16d25-250">recursiva</span><span class="sxs-lookup"><span data-stu-id="16d25-250">recursive</span></span> |<span data-ttu-id="16d25-251">Indica se os dados são lidos recursivamente das subpastas ou somente da pasta especificada.</span><span class="sxs-lookup"><span data-stu-id="16d25-251">Indicates whether the data is read recursively from the subfolders, or only from the specified folder.</span></span> |<span data-ttu-id="16d25-252">True, False (padrão)</span><span class="sxs-lookup"><span data-stu-id="16d25-252">True, False (default)</span></span> |<span data-ttu-id="16d25-253">Não</span><span class="sxs-lookup"><span data-stu-id="16d25-253">No</span></span> |

## <a name="json-example-copy-data-from-ftp-server-to-azure-blob"></a><span data-ttu-id="16d25-254">Exemplo de JSON: Copiar dados do servidor FTP para o Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="16d25-254">JSON example: Copy data from FTP server to Azure Blob</span></span>
<span data-ttu-id="16d25-255">Este exemplo mostra como copiar dados de um servidor FTP para um Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="16d25-255">This sample shows how to copy data from an FTP server to Azure Blob storage.</span></span> <span data-ttu-id="16d25-256">No entanto, os dados podem ser copiados diretamente para qualquer um dos coletores declarados em [formatos e repositórios de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a atividade de cópia no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="16d25-256">However, data can be copied directly to any of the sinks stated in the [supported data stores and formats](data-factory-data-movement-activities.md#supported-data-stores-and-formats), by using the copy activity in Data Factory.</span></span>  

<span data-ttu-id="16d25-257">Os exemplos a seguir fornecem amostras de definições de JSON que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="16d25-257">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md):</span></span>

* <span data-ttu-id="16d25-258">Um serviço vinculado do tipo [FtpServer](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="16d25-258">A linked service of type [FtpServer](#linked-service-properties)</span></span>
* <span data-ttu-id="16d25-259">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="16d25-259">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="16d25-260">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [FileShare](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="16d25-260">An input [dataset](data-factory-create-datasets.md) of type [FileShare](#dataset-properties)</span></span>
* <span data-ttu-id="16d25-261">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="16d25-261">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="16d25-262">Um [pipeline](data-factory-create-pipelines.md) com a atividade de cópia que usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="16d25-262">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="16d25-263">O exemplo copia dados de um servidor FTP para um blob do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="16d25-263">The sample copies data from an FTP server to an Azure blob every hour.</span></span> <span data-ttu-id="16d25-264">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="16d25-264">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="ftp-linked-service"></a><span data-ttu-id="16d25-265">Serviço vinculado de FTP</span><span class="sxs-lookup"><span data-stu-id="16d25-265">FTP linked service</span></span>

<span data-ttu-id="16d25-266">Este exemplo usa autenticação Básica com nome de usuário e senha em texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="16d25-266">This example uses basic authentication, with the user name and password in plain text.</span></span> <span data-ttu-id="16d25-267">Você também pode usar uma das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="16d25-267">You can also use one of the following ways:</span></span>

* <span data-ttu-id="16d25-268">Autenticação anônima</span><span class="sxs-lookup"><span data-stu-id="16d25-268">Anonymous authentication</span></span>
* <span data-ttu-id="16d25-269">Autenticação básica com credenciais criptografadas</span><span class="sxs-lookup"><span data-stu-id="16d25-269">Basic authentication with encrypted credentials</span></span>
* <span data-ttu-id="16d25-270">FTPS (FTP sobre SSL/TLS)</span><span class="sxs-lookup"><span data-stu-id="16d25-270">FTP over SSL/TLS (FTPS)</span></span>

<span data-ttu-id="16d25-271">Confira a seção [Serviço FTP vinculado](#linked-service-properties) para ver os diferentes tipos de autenticação que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="16d25-271">See the [FTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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
### <a name="azure-storage-linked-service"></a><span data-ttu-id="16d25-272">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="16d25-272">Azure Storage linked service</span></span>

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
### <a name="ftp-input-dataset"></a><span data-ttu-id="16d25-273">Conjunto de dados de entrada de FTP</span><span class="sxs-lookup"><span data-stu-id="16d25-273">FTP input dataset</span></span>

<span data-ttu-id="16d25-274">Esse conjunto de dados refere-se à pasta FTP `mysharedfolder` e ao arquivo `test.csv`.</span><span class="sxs-lookup"><span data-stu-id="16d25-274">This dataset refers to the FTP folder `mysharedfolder` and file `test.csv`.</span></span> <span data-ttu-id="16d25-275">O pipeline copia o arquivo para o destino.</span><span class="sxs-lookup"><span data-stu-id="16d25-275">The pipeline copies the file to the destination.</span></span>

<span data-ttu-id="16d25-276">Configurar **external**: **true** informa ao serviço Data Factory que o conjunto de dados é externo ao data factory e não é produzido por uma atividade no data factory.</span><span class="sxs-lookup"><span data-stu-id="16d25-276">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory, and is not produced by an activity in the data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="16d25-277">Conjunto de dados de saída de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="16d25-277">Azure Blob output dataset</span></span>

<span data-ttu-id="16d25-278">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="16d25-278">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="16d25-279">O caminho de pasta para o blob é avaliado dinamicamente com base na hora de início da fatia que está sendo processada.</span><span class="sxs-lookup"><span data-stu-id="16d25-279">The folder path for the blob is dynamically evaluated, based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="16d25-280">O caminho da pasta usa as partes ano, mês, dia e hora da hora de início.</span><span class="sxs-lookup"><span data-stu-id="16d25-280">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

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


### <a name="a-copy-activity-in-a-pipeline-with-file-system-source-and-blob-sink"></a><span data-ttu-id="16d25-281">Uma atividade de cópia em um pipeline com origem no sistema de arquivos e coletor de blobs</span><span class="sxs-lookup"><span data-stu-id="16d25-281">A copy activity in a pipeline with file system source and blob sink</span></span>

<span data-ttu-id="16d25-282">O pipeline contém uma atividade de cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="16d25-282">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="16d25-283">Na definição JSON do pipeline, o tipo **source** está definido como **FileSystemSource** e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="16d25-283">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and the **sink** type is set to **BlobSink**.</span></span>

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
> <span data-ttu-id="16d25-284">Para mapear colunas de conjunto de dados de origem para colunas do conjunto de dados de coletor, confira [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md) (Mapeamento de colunas de conjunto de dados no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="16d25-284">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="16d25-285">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="16d25-285">Next steps</span></span>
<span data-ttu-id="16d25-286">Confira os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="16d25-286">See the following articles:</span></span>

* <span data-ttu-id="16d25-287">Para saber mais sobre os principais fatores que afetam o desempenho e a movimentação dos dados (atividade de cópia) no Azure Data Factory, além de várias maneiras de otimizá-la, consulte o [Guia de desempenho e ajuste da atividade de cópia](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="16d25-287">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="16d25-288">Para obter instruções passo a passo para criar um pipeline com uma atividade de cópia, consulte o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="16d25-288">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
