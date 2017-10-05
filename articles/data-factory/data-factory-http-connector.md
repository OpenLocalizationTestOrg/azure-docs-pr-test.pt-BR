---
title: "Mover dados de uma fonte HTTP – Azure | Microsoft Docs"
description: Saiba mais sobre como mover dados de uma origem HTTP local ou na nuvem usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 3cc1bd293868b0bb093f617ac12e16c26780fc89
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="00d93-103">Mover dados de uma origem HTTP usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="00d93-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="00d93-104">Este artigo descreve como usar a Atividade de Cópia no Azure Data Factory para mover dados de um ponto de extremidade HTTP local/na nuvem para um armazenamento de dados do coletor com suporte.</span><span class="sxs-lookup"><span data-stu-id="00d93-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from an on-premises/cloud HTTP endpoint to a supported sink data store.</span></span> <span data-ttu-id="00d93-105">Este artigo se baseia no artigo [Atividades de movimentação de dados](data-factory-data-movement-activities.md), que apresenta uma visão geral de movimentação de dados com a atividade de cópia e a lista de armazenamentos de dados com suporte, como fontes/coletores.</span><span class="sxs-lookup"><span data-stu-id="00d93-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="00d93-106">Atualmente, o data factory dá suporte apenas para a movimentação de dados de uma origem HTTP para outros armazenamentos de dados, mas não para a movimentação de dados de outros armazenamentos de dados para um destino HTTP.</span><span class="sxs-lookup"><span data-stu-id="00d93-106">Data factory currently supports only moving data from an HTTP source to other data stores, but not moving data from other data stores to an HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="00d93-107">Cenários com suporte e tipos de autenticação</span><span class="sxs-lookup"><span data-stu-id="00d93-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="00d93-108">Você pode usar esse conector HTTP para recuperar dados de **ponto de extremidade HTTP/s, seja ele na nuvem ou local**, usando o método HTTP **GET** ou **POST**.</span><span class="sxs-lookup"><span data-stu-id="00d93-108">You can use this HTTP connector to retrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="00d93-109">Os seguintes tipos de autenticação têm suporte: **Anônimo**, **Básico**, **Digest**, **Windows** e **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="00d93-109">The following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="00d93-110">Observe que a diferença entre esse conector e o [Conector da tabela da Web](data-factory-web-table-connector.md) é: o segundo é usado para extrair o conteúdo de tabela da página HTML da Web.</span><span class="sxs-lookup"><span data-stu-id="00d93-110">Note the difference between this connector and the [Web table connector](data-factory-web-table-connector.md) is: the latter is used to extract table content from web HTML page.</span></span>

<span data-ttu-id="00d93-111">Ao copiar dados de um ponto de extremidade HTTP local, você precisa instalar um gateway de gerenciamento de dados no ambiente local/VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="00d93-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in the on-premises environment/Azure VM.</span></span> <span data-ttu-id="00d93-112">Consulte o artigo [movendo dados entre pontos locais e na nuvem](data-factory-move-data-between-onprem-and-cloud.md) para saber mais sobre o Gateway de gerenciamento de dados e obter instruções passo a passo de como configurar o gateway.</span><span class="sxs-lookup"><span data-stu-id="00d93-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="00d93-113">Introdução</span><span class="sxs-lookup"><span data-stu-id="00d93-113">Getting started</span></span>
<span data-ttu-id="00d93-114">Você pode criar um pipeline com uma atividade de cópia que mova dados de uma origem HTTP usando ferramentas/APIs diferentes.</span><span class="sxs-lookup"><span data-stu-id="00d93-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="00d93-115">A maneira mais fácil de criar um pipeline é usar o **Assistente de Cópia**.</span><span class="sxs-lookup"><span data-stu-id="00d93-115">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="00d93-116">Confira [Tutorial: Criar um pipeline usando o Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md) para ver um breve passo a passo sobre como criar um pipeline usando o Assistente de cópia de dados.</span><span class="sxs-lookup"><span data-stu-id="00d93-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

- <span data-ttu-id="00d93-117">Você também pode usar as seguintes ferramentas para criar um pipeline: **Portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Azure Resource Manager**, **API .NET** e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="00d93-117">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="00d93-118">Confira o [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo sobre a criação de um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="00d93-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> <span data-ttu-id="00d93-119">Para obter amostras JSON copiar dados da origem HTTP para o Armazenamento de Blobs do Azure, consulte a seção [Exemplos de JSON](#json-examples) nestes artigos.</span><span class="sxs-lookup"><span data-stu-id="00d93-119">For JSON samples to copy data from HTTP source to Azure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="00d93-120">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="00d93-120">Linked service properties</span></span>
<span data-ttu-id="00d93-121">A tabela a seguir apresenta a descrição para elementos JSON específicos do serviço HTTP vinculado.</span><span class="sxs-lookup"><span data-stu-id="00d93-121">The following table provides description for JSON elements specific to HTTP linked service.</span></span>

| <span data-ttu-id="00d93-122">Propriedade</span><span class="sxs-lookup"><span data-stu-id="00d93-122">Property</span></span> | <span data-ttu-id="00d93-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="00d93-123">Description</span></span> | <span data-ttu-id="00d93-124">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="00d93-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="00d93-125">type</span><span class="sxs-lookup"><span data-stu-id="00d93-125">type</span></span> | <span data-ttu-id="00d93-126">A propriedade type deve ser definida como: `Http`.</span><span class="sxs-lookup"><span data-stu-id="00d93-126">The type property must be set to: `Http`.</span></span> | <span data-ttu-id="00d93-127">Sim</span><span class="sxs-lookup"><span data-stu-id="00d93-127">Yes</span></span> |
| <span data-ttu-id="00d93-128">url</span><span class="sxs-lookup"><span data-stu-id="00d93-128">url</span></span> | <span data-ttu-id="00d93-129">URL base para o Servidor Web</span><span class="sxs-lookup"><span data-stu-id="00d93-129">Base URL to the Web Server</span></span> | <span data-ttu-id="00d93-130">Sim</span><span class="sxs-lookup"><span data-stu-id="00d93-130">Yes</span></span> |
| <span data-ttu-id="00d93-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="00d93-131">authenticationType</span></span> | <span data-ttu-id="00d93-132">Especifica o tipo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="00d93-132">Specifies the authentication type.</span></span> <span data-ttu-id="00d93-133">Os valores permitidos são: **Anônimo**, **Básico**, **Digest**, **Windows** e **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="00d93-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="00d93-134">Consulte as seções abaixo desta tabela para mais propriedades e amostras JSON para esses tipos de autenticação, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="00d93-134">Refer to sections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="00d93-135">Sim</span><span class="sxs-lookup"><span data-stu-id="00d93-135">Yes</span></span> |
| <span data-ttu-id="00d93-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="00d93-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="00d93-137">Especifique se deseja habilitar a validação do certificado SSL do servidor se a origem for um servidor Web HTTPS</span><span class="sxs-lookup"><span data-stu-id="00d93-137">Specify whether to enable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="00d93-138">Não, o padrão é true</span><span class="sxs-lookup"><span data-stu-id="00d93-138">No, default is true</span></span> |
| <span data-ttu-id="00d93-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="00d93-139">gatewayName</span></span> | <span data-ttu-id="00d93-140">Nome do Gateway de Gerenciamento de Dados para se conectar a uma origem HTTP local.</span><span class="sxs-lookup"><span data-stu-id="00d93-140">Name of the Data Management Gateway to connect to an on-premises HTTP source.</span></span> | <span data-ttu-id="00d93-141">Sim se estiver copiando dados de uma origem HTTP local.</span><span class="sxs-lookup"><span data-stu-id="00d93-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="00d93-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="00d93-142">encryptedCredential</span></span> | <span data-ttu-id="00d93-143">Credencial criptografada para acessar o ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="00d93-143">Encrypted credential to access the HTTP endpoint.</span></span> <span data-ttu-id="00d93-144">Gerado automaticamente quando você configura as informações de autenticação no assistente de cópia ou a caixa de diálogo pop-up do ClickOnce.</span><span class="sxs-lookup"><span data-stu-id="00d93-144">Auto-generated when you configure the authentication information in copy wizard or the ClickOnce popup dialog.</span></span> | <span data-ttu-id="00d93-145">Não.</span><span class="sxs-lookup"><span data-stu-id="00d93-145">No.</span></span> <span data-ttu-id="00d93-146">Aplique somente quando estiver copiando dados de um servidor HTTP local.</span><span class="sxs-lookup"><span data-stu-id="00d93-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="00d93-147">Consulte [Mover dados entre fontes locais e a nuvem com o Gateway de Gerenciamento de Dados](data-factory-move-data-between-onprem-and-cloud.md) para obter detalhes sobre como configurar as credenciais para uma fonte de dados de conector HTTP local.</span><span class="sxs-lookup"><span data-stu-id="00d93-147">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="00d93-148">Usando a autenticação Básica, Digest ou Windows</span><span class="sxs-lookup"><span data-stu-id="00d93-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="00d93-149">Defina `authenticationType` como `Basic`, `Digest` ou `Windows` e especifique as propriedades a seguir, além das genéricas do conector HTTP apresentadas acima:</span><span class="sxs-lookup"><span data-stu-id="00d93-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="00d93-150">Propriedade</span><span class="sxs-lookup"><span data-stu-id="00d93-150">Property</span></span> | <span data-ttu-id="00d93-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="00d93-151">Description</span></span> | <span data-ttu-id="00d93-152">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="00d93-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="00d93-153">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="00d93-153">username</span></span> | <span data-ttu-id="00d93-154">Nome de usuário para acessar o ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="00d93-154">Username to access the HTTP endpoint.</span></span> | <span data-ttu-id="00d93-155">Sim</span><span class="sxs-lookup"><span data-stu-id="00d93-155">Yes</span></span> |
| <span data-ttu-id="00d93-156">Senha</span><span class="sxs-lookup"><span data-stu-id="00d93-156">password</span></span> | <span data-ttu-id="00d93-157">Senha do usuário (nome de usuário).</span><span class="sxs-lookup"><span data-stu-id="00d93-157">Password for the user (username).</span></span> | <span data-ttu-id="00d93-158">Sim</span><span class="sxs-lookup"><span data-stu-id="00d93-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="00d93-159">Exemplo: usando a autenticação Básica, Digest ou Windows</span><span class="sxs-lookup"><span data-stu-id="00d93-159">Example: using Basic, Digest, or Windows authentication</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "basic",
            "url" : "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="00d93-160">Usando a autenticação ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="00d93-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="00d93-161">Para usar a autenticação Básica, defina `authenticationType` como `ClientCertificate` e especifique as propriedades a seguir, além das genéricas do conector HTTP apresentadas acima:</span><span class="sxs-lookup"><span data-stu-id="00d93-161">To use basic authentication, set `authenticationType` as `ClientCertificate`, and specify the following properties besides the HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="00d93-162">Propriedade</span><span class="sxs-lookup"><span data-stu-id="00d93-162">Property</span></span> | <span data-ttu-id="00d93-163">Descrição</span><span class="sxs-lookup"><span data-stu-id="00d93-163">Description</span></span> | <span data-ttu-id="00d93-164">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="00d93-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="00d93-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="00d93-165">embeddedCertData</span></span> | <span data-ttu-id="00d93-166">O conteúdo codificado na Base64 de dados binários do arquivo Personal Information Exchange (PFX).</span><span class="sxs-lookup"><span data-stu-id="00d93-166">The Base64-encoded contents of binary data of the Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="00d93-167">Especifique `embeddedCertData` ou `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="00d93-167">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="00d93-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="00d93-168">certThumbprint</span></span> | <span data-ttu-id="00d93-169">A impressão digital do certificado que foi instalado no repositório de certificados do computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="00d93-169">The thumbprint of the certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="00d93-170">Aplique somente ao copiar dados de uma origem HTTP local.</span><span class="sxs-lookup"><span data-stu-id="00d93-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="00d93-171">Especifique `embeddedCertData` ou `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="00d93-171">Specify either the `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="00d93-172">Senha</span><span class="sxs-lookup"><span data-stu-id="00d93-172">password</span></span> | <span data-ttu-id="00d93-173">Senha associada ao certificado.</span><span class="sxs-lookup"><span data-stu-id="00d93-173">Password associated with the certificate.</span></span> | <span data-ttu-id="00d93-174">Não</span><span class="sxs-lookup"><span data-stu-id="00d93-174">No</span></span> |

<span data-ttu-id="00d93-175">Se você usar `certThumbprint` para autenticação e o certificado estiver instalado no armazenamento pessoal do computador local, você precisará conceder a permissão de leitura para o serviço de gateway:</span><span class="sxs-lookup"><span data-stu-id="00d93-175">If you use `certThumbprint` for authentication and the certificate is installed in the personal store of the local computer, you need to grant the read permission to the gateway service:</span></span>

1. <span data-ttu-id="00d93-176">Iniciar o MMC (Console de Gerenciamento Microsoft).</span><span class="sxs-lookup"><span data-stu-id="00d93-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="00d93-177">Adicionar o snap-in **Certificados**, que tem como destino o **Computador Local**.</span><span class="sxs-lookup"><span data-stu-id="00d93-177">Add the **Certificates** snap-in that targets the **Local Computer**.</span></span>
2. <span data-ttu-id="00d93-178">Expanda **Certificados**, **Pessoal** e clique em **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="00d93-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="00d93-179">Clique com o botão direito do mouse no certificado do repositório pessoal e selecione **Todas as Tarefas**->**Gerenciar Chaves Particulares...**</span><span class="sxs-lookup"><span data-stu-id="00d93-179">Right-click the certificate from the personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="00d93-180">Na guia **Segurança**, adicione a conta de usuário sob a qual o serviço de Host de Gateway de Gerenciamento de Dados está em execução com o acesso de leitura para o certificado.</span><span class="sxs-lookup"><span data-stu-id="00d93-180">On the **Security** tab, add the user account under which Data Management Gateway Host Service is running with the read access to the certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="00d93-181">Exemplo: usando o certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="00d93-181">Example: using client certificate</span></span>
<span data-ttu-id="00d93-182">Esse serviço vinculado vincula seu data factory a um servidor Web HTTP local.</span><span class="sxs-lookup"><span data-stu-id="00d93-182">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="00d93-183">Ele usa um certificado do cliente instalado no computador com o Gateway de Gerenciamento de Dados instalado.</span><span class="sxs-lookup"><span data-stu-id="00d93-183">It uses a client certificate that is installed on the machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"

        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="00d93-184">Exemplo: usando o certificado do cliente em um arquivo</span><span class="sxs-lookup"><span data-stu-id="00d93-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="00d93-185">Esse serviço vinculado vincula seu data factory a um servidor Web HTTP local.</span><span class="sxs-lookup"><span data-stu-id="00d93-185">This linked service links your data factory to an on-premises HTTP web server.</span></span> <span data-ttu-id="00d93-186">Ele usa um certificado do cliente no computador com o Gateway de Gerenciamento de Dados instalado.</span><span class="sxs-lookup"><span data-stu-id="00d93-186">It uses a client certificate file on the machine with Data Management Gateway installed.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="00d93-187">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="00d93-187">Dataset properties</span></span>
<span data-ttu-id="00d93-188">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, confira o artigo [Criando conjuntos de dados](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="00d93-188">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="00d93-189">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="00d93-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="00d93-190">A seção **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local dos dados no armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="00d93-190">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="00d93-191">A seção typeProperties para o conjunto de dados do tipo **Http** tem as propriedades a seguir</span><span class="sxs-lookup"><span data-stu-id="00d93-191">The typeProperties section for dataset of type **Http** has the following properties</span></span>

| <span data-ttu-id="00d93-192">Propriedade</span><span class="sxs-lookup"><span data-stu-id="00d93-192">Property</span></span> | <span data-ttu-id="00d93-193">Descrição</span><span class="sxs-lookup"><span data-stu-id="00d93-193">Description</span></span> | <span data-ttu-id="00d93-194">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="00d93-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="00d93-195">type</span><span class="sxs-lookup"><span data-stu-id="00d93-195">type</span></span> | <span data-ttu-id="00d93-196">O tipo do conjunto de dados foi especificado.</span><span class="sxs-lookup"><span data-stu-id="00d93-196">Specified the type of the dataset.</span></span> <span data-ttu-id="00d93-197">deve ser definido como `Http`.</span><span class="sxs-lookup"><span data-stu-id="00d93-197">must be set to `Http`.</span></span> | <span data-ttu-id="00d93-198">Sim</span><span class="sxs-lookup"><span data-stu-id="00d93-198">Yes</span></span> |
| <span data-ttu-id="00d93-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="00d93-199">relativeUrl</span></span> | <span data-ttu-id="00d93-200">Uma URL relativa para o recurso que contém os dados.</span><span class="sxs-lookup"><span data-stu-id="00d93-200">A relative URL to the resource that contains the data.</span></span> <span data-ttu-id="00d93-201">Quando o caminho não for especificado, apenas a URL especificada na definição do serviço vinculado será usada.</span><span class="sxs-lookup"><span data-stu-id="00d93-201">When path is not specified, only the URL specified in the linked service definition is used.</span></span> <br><br> <span data-ttu-id="00d93-202">Para construir uma URL dinâmica, você pode usar as [funções e variáveis de sistema do Data Factory](data-factory-functions-variables.md), por exemplo, “relativeUrl”: “$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)”.</span><span class="sxs-lookup"><span data-stu-id="00d93-202">To construct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="00d93-203">Não</span><span class="sxs-lookup"><span data-stu-id="00d93-203">No</span></span> |
| <span data-ttu-id="00d93-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="00d93-204">requestMethod</span></span> | <span data-ttu-id="00d93-205">Método Http.</span><span class="sxs-lookup"><span data-stu-id="00d93-205">Http method.</span></span> <span data-ttu-id="00d93-206">Os valores permitidos são **GET** ou **POST**.</span><span class="sxs-lookup"><span data-stu-id="00d93-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="00d93-207">Não.</span><span class="sxs-lookup"><span data-stu-id="00d93-207">No.</span></span> <span data-ttu-id="00d93-208">O padrão é `GET`.</span><span class="sxs-lookup"><span data-stu-id="00d93-208">Default is `GET`.</span></span> |
| <span data-ttu-id="00d93-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="00d93-209">additionalHeaders</span></span> | <span data-ttu-id="00d93-210">Cabeçalhos de solicitação HTTP adicionais.</span><span class="sxs-lookup"><span data-stu-id="00d93-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="00d93-211">Não</span><span class="sxs-lookup"><span data-stu-id="00d93-211">No</span></span> |
| <span data-ttu-id="00d93-212">requestBody</span><span class="sxs-lookup"><span data-stu-id="00d93-212">requestBody</span></span> | <span data-ttu-id="00d93-213">O corpo da solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="00d93-213">Body for HTTP request.</span></span> | <span data-ttu-id="00d93-214">Não</span><span class="sxs-lookup"><span data-stu-id="00d93-214">No</span></span> |
| <span data-ttu-id="00d93-215">formato</span><span class="sxs-lookup"><span data-stu-id="00d93-215">format</span></span> | <span data-ttu-id="00d93-216">Se você quiser simplesmente **recuperar os dados do ponto de extremidade HTTP como estão** sem analisá-los, ignore estas configurações de formato.</span><span class="sxs-lookup"><span data-stu-id="00d93-216">If you want to simply **retrieve the data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="00d93-217">Se você quiser analisar o conteúdo da resposta HTTP durante a cópia, há suporte para os seguintes tipos de formato: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat** e **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="00d93-217">If you want to parse the HTTP response content during copy, the following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="00d93-218">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="00d93-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="00d93-219">Não</span><span class="sxs-lookup"><span data-stu-id="00d93-219">No</span></span> |
| <span data-ttu-id="00d93-220">compactação</span><span class="sxs-lookup"><span data-stu-id="00d93-220">compression</span></span> | <span data-ttu-id="00d93-221">Especifique o tipo e o nível de compactação para os dados.</span><span class="sxs-lookup"><span data-stu-id="00d93-221">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="00d93-222">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="00d93-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="00d93-223">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="00d93-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="00d93-224">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="00d93-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="00d93-225">Não</span><span class="sxs-lookup"><span data-stu-id="00d93-225">No</span></span> |

### <a name="example-using-the-get-default-method"></a><span data-ttu-id="00d93-226">Exemplo: usando o método GET (padrão)</span><span class="sxs-lookup"><span data-stu-id="00d93-226">Example: using the GET (default) method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

### <a name="example-using-the-post-method"></a><span data-ttu-id="00d93-227">Exemplo: usando o método POST</span><span class="sxs-lookup"><span data-stu-id="00d93-227">Example: using the POST method</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
           "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="00d93-228">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="00d93-228">Copy activity properties</span></span>
<span data-ttu-id="00d93-229">Para obter uma lista completa das seções e propriedades disponíveis para definir atividades, confia o artigo [Criando pipelines](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="00d93-229">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="00d93-230">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="00d93-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="00d93-231">As propriedades disponíveis na seção **typeProperties** da atividade, por outro lado, variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="00d93-231">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="00d93-232">Para a atividade de cópia, elas variam de acordo com os tipos de fonte e coletor.</span><span class="sxs-lookup"><span data-stu-id="00d93-232">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="00d93-233">Atualmente, quando a origem na atividade de cópia é do tipo **HttpSource**, há suporte para as propriedades a seguir.</span><span class="sxs-lookup"><span data-stu-id="00d93-233">Currently, when the source in copy activity is of type **HttpSource**, the following properties are supported.</span></span>

| <span data-ttu-id="00d93-234">Propriedade</span><span class="sxs-lookup"><span data-stu-id="00d93-234">Property</span></span> | <span data-ttu-id="00d93-235">Descrição</span><span class="sxs-lookup"><span data-stu-id="00d93-235">Description</span></span> | <span data-ttu-id="00d93-236">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="00d93-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="00d93-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="00d93-237">httpRequestTimeout</span></span> | <span data-ttu-id="00d93-238">O tempo limite (TimeSpan) para a solicitação HTTP obter uma resposta.</span><span class="sxs-lookup"><span data-stu-id="00d93-238">The timeout (TimeSpan) for the HTTP request to get a response.</span></span> <span data-ttu-id="00d93-239">É o tempo limite para obter uma resposta e não o tempo limite para ler dados de resposta.</span><span class="sxs-lookup"><span data-stu-id="00d93-239">It is the timeout to get a response, not the timeout to read response data.</span></span> | <span data-ttu-id="00d93-240">Não.</span><span class="sxs-lookup"><span data-stu-id="00d93-240">No.</span></span> <span data-ttu-id="00d93-241">Valor padrão: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="00d93-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="00d93-242">Formatos de arquivo e de compactação com suporte</span><span class="sxs-lookup"><span data-stu-id="00d93-242">Supported file and compression formats</span></span>
<span data-ttu-id="00d93-243">Consulte o artigo [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="00d93-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="00d93-244">Exemplos de JSON</span><span class="sxs-lookup"><span data-stu-id="00d93-244">JSON examples</span></span>
<span data-ttu-id="00d93-245">O exemplo a seguir fornece as definições de JSON de exemplo que você pode usar para criar um pipeline usando o [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), o [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou o [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="00d93-245">The following example provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="00d93-246">Eles mostram como copiar dados da origem HTTP para o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="00d93-246">They show how to copy data from HTTP source to Azure Blob Storage.</span></span> <span data-ttu-id="00d93-247">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes para qualquer um dos coletores declarados [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a Atividade de Cópia no Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="00d93-247">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-to-azure-blob-storage"></a><span data-ttu-id="00d93-248">Exemplo: copiar dados da origem HTTP para o Armazenamento de Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="00d93-248">Example: Copy data from HTTP source to Azure Blob Storage</span></span>
<span data-ttu-id="00d93-249">A solução de Data Factory para este exemplo contém as seguintes entidades de Data Factory:</span><span class="sxs-lookup"><span data-stu-id="00d93-249">The Data Factory solution for this sample contains the following Data Factory entities:</span></span>

1. <span data-ttu-id="00d93-250">Um serviço vinculado do tipo [HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="00d93-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="00d93-251">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="00d93-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="00d93-252">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [Http](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="00d93-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="00d93-253">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="00d93-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="00d93-254">Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [HttpSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="00d93-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="00d93-255">O exemplo copia dados de uma origem HTTP para um blob do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="00d93-255">The sample copies data from an HTTP source to an Azure blob every hour.</span></span> <span data-ttu-id="00d93-256">As propriedades JSON usadas nesses exemplos são descritas nas seções após os exemplos.</span><span class="sxs-lookup"><span data-stu-id="00d93-256">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="00d93-257">Serviço vinculado HTTP</span><span class="sxs-lookup"><span data-stu-id="00d93-257">HTTP linked service</span></span>
<span data-ttu-id="00d93-258">Esse exemplo usa o serviço vinculado HTTP com autenticação anônima.</span><span class="sxs-lookup"><span data-stu-id="00d93-258">This example uses the HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="00d93-259">Confira a seção [Serviço vinculado HTTP](#linked-service-properties) para ver os diferentes tipos de autenticação que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="00d93-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```JSON
{
    "name": "HttpLinkedService",
    "properties":
    {
        "type": "Http",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="00d93-260">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="00d93-260">Azure Storage linked service</span></span>

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

### <a name="http-input-dataset"></a><span data-ttu-id="00d93-261">Conjunto de dados de entrada HTTP</span><span class="sxs-lookup"><span data-stu-id="00d93-261">HTTP input dataset</span></span>
<span data-ttu-id="00d93-262">Configurar **external** como **true** informa ao serviço Data Factory que o conjunto de dados é externo ao Data Factory e não é produzido por uma atividade no Data Factory.</span><span class="sxs-lookup"><span data-stu-id="00d93-262">Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}

```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="00d93-263">Conjunto de dados de saída de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="00d93-263">Azure Blob output dataset</span></span>

<span data-ttu-id="00d93-264">Os dados são gravados em um novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="00d93-264">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="00d93-265">Pipeline com Atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="00d93-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="00d93-266">O pipeline contém uma Atividade de Cópia que está configurada para usar os conjuntos de dados de entrada e saída e é agendada para ser executada a cada hora.</span><span class="sxs-lookup"><span data-stu-id="00d93-266">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="00d93-267">Na definição JSON do pipeline, o tipo **source** está definido como **HttpSource** e o tipo **sink** está definido como **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="00d93-267">In the pipeline JSON definition, the **source** type is set to **HttpSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="00d93-268">Consulte [HttpSource](#copy-activity-properties) para obter a lista de propriedades às quais HttpSource dá suporte.</span><span class="sxs-lookup"><span data-stu-id="00d93-268">See [HttpSource](#copy-activity-properties) for the list of properties supported by the HttpSource.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "HttpSourceToAzureBlob",
        "description": "Copy from an HTTP source to an Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "HttpSourceDataInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "HttpSource"
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

> [!NOTE]
> <span data-ttu-id="00d93-269">Para mapear colunas de conjunto de dados de origem para colunas do conjunto de dados de coletor, confira [Mapeando colunas de conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="00d93-269">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="00d93-270">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="00d93-270">Performance and Tuning</span></span>
<span data-ttu-id="00d93-271">Veja o [Guia de desempenho e ajuste da Atividade de Cópia](data-factory-copy-activity-performance.md) para saber mais sobre os principais fatores que afetam o desempenho da movimentação de dados (Atividade de Cópia) no Azure Data Factory, além de várias maneiras de otimizar esse processo.</span><span class="sxs-lookup"><span data-stu-id="00d93-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
