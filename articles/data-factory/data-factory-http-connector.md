---
title: aaaMove dados de uma fonte de HTTP - Azure | Microsoft Docs
description: Saiba mais sobre como toomove de um local ou uma nuvem HTTP da fonte de dados usando o Azure Data Factory.
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
ms.openlocfilehash: e39b9cbff870aef4be91938cacff39a2fd12d64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-http-source-using-azure-data-factory"></a><span data-ttu-id="c3391-103">Mover dados de uma origem HTTP usando o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c3391-103">Move data from an HTTP source using Azure Data Factory</span></span>
<span data-ttu-id="c3391-104">Este artigo descreve como toouse hello atividade de cópia em dados do Azure Data Factory toomove de um tooa de ponto de extremidade HTTP no local/em nuvem suporte para armazenamento de dados do coletor.</span><span class="sxs-lookup"><span data-stu-id="c3391-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises/cloud HTTP endpoint tooa supported sink data store.</span></span> <span data-ttu-id="c3391-105">Este artigo aproveita Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo que apresenta uma visão geral de movimentação de dados com Copiar atividade e hello lista de repositórios de dados têm suportada como/coletores de fontes.</span><span class="sxs-lookup"><span data-stu-id="c3391-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="c3391-106">Fábrica de dados atualmente suporta apenas os dados movidos de um HTTP tooother repositórios de dados de origem, mas não movendo os dados de outros dados armazena o destino tooan HTTP.</span><span class="sxs-lookup"><span data-stu-id="c3391-106">Data factory currently supports only moving data from an HTTP source tooother data stores, but not moving data from other data stores tooan HTTP destination.</span></span>

## <a name="supported-scenarios-and-authentication-types"></a><span data-ttu-id="c3391-107">Cenários com suporte e tipos de autenticação</span><span class="sxs-lookup"><span data-stu-id="c3391-107">Supported scenarios and authentication types</span></span>
<span data-ttu-id="c3391-108">Você pode usar esses dados de tooretrieve do conector HTTP do **ponto de extremidade HTTP/s de nuvem e local** usando HTTP **obter** ou **POST** método.</span><span class="sxs-lookup"><span data-stu-id="c3391-108">You can use this HTTP connector tooretrieve data from **both cloud and on-premises HTTP/s endpoint** by using HTTP **GET** or **POST** method.</span></span> <span data-ttu-id="c3391-109">Olá, tipos de autenticação a seguir têm suporte: **anônimo**, **básica**, **Digest**, **Windows**, e  **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="c3391-109">hello following authentication types are supported: **Anonymous**, **Basic**, **Digest**, **Windows**, and **ClientCertificate**.</span></span> <span data-ttu-id="c3391-110">Observe a diferença de saudação entre esse conector e Olá [Conector Web de tabela](data-factory-web-table-connector.md) é: Olá este último é a tabela de tooextract usado conteúda da página HTML de web.</span><span class="sxs-lookup"><span data-stu-id="c3391-110">Note hello difference between this connector and hello [Web table connector](data-factory-web-table-connector.md) is: hello latter is used tooextract table content from web HTML page.</span></span>

<span data-ttu-id="c3391-111">Ao copiar dados de um ponto de extremidade HTTP do local, você precisa instalar um Gateway de gerenciamento de dados no ambiente do local de saudação/Azure VM.</span><span class="sxs-lookup"><span data-stu-id="c3391-111">When copying data from an on-premises HTTP endpoint, you need install a Data Management Gateway in hello on-premises environment/Azure VM.</span></span> <span data-ttu-id="c3391-112">Consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Gateway de gerenciamento de dados e instruções passo a passo sobre como configurar o gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="c3391-112">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c3391-113">Introdução</span><span class="sxs-lookup"><span data-stu-id="c3391-113">Getting started</span></span>
<span data-ttu-id="c3391-114">Você pode criar um pipeline com uma atividade de cópia que mova dados de uma origem HTTP usando ferramentas/APIs diferentes.</span><span class="sxs-lookup"><span data-stu-id="c3391-114">You can create a pipeline with a copy activity that moves data from an HTTP source by using different tools/APIs.</span></span>

- <span data-ttu-id="c3391-115">toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**.</span><span class="sxs-lookup"><span data-stu-id="c3391-115">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="c3391-116">Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.</span><span class="sxs-lookup"><span data-stu-id="c3391-116">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

- <span data-ttu-id="c3391-117">Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**.</span><span class="sxs-lookup"><span data-stu-id="c3391-117">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c3391-118">Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="c3391-118">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> <span data-ttu-id="c3391-119">Para exemplos de JSON toocopy dados de origem HTTP tooAzure armazenamento de Blob, consulte [exemplos JSON](#json-examples) seção neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c3391-119">For JSON samples toocopy data from HTTP source tooAzure Blob Storage, see [JSON examples](#json-examples) section of this articles.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c3391-120">Propriedades do serviço vinculado</span><span class="sxs-lookup"><span data-stu-id="c3391-120">Linked service properties</span></span>
<span data-ttu-id="c3391-121">Olá, a tabela a seguir fornece uma descrição para JSON elementos específicos tooHTTP vinculado serviço.</span><span class="sxs-lookup"><span data-stu-id="c3391-121">hello following table provides description for JSON elements specific tooHTTP linked service.</span></span>

| <span data-ttu-id="c3391-122">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c3391-122">Property</span></span> | <span data-ttu-id="c3391-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="c3391-123">Description</span></span> | <span data-ttu-id="c3391-124">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="c3391-124">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3391-125">type</span><span class="sxs-lookup"><span data-stu-id="c3391-125">type</span></span> | <span data-ttu-id="c3391-126">propriedade de tipo Hello deve ser definida como: `Http`.</span><span class="sxs-lookup"><span data-stu-id="c3391-126">hello type property must be set to: `Http`.</span></span> | <span data-ttu-id="c3391-127">Sim</span><span class="sxs-lookup"><span data-stu-id="c3391-127">Yes</span></span> |
| <span data-ttu-id="c3391-128">url</span><span class="sxs-lookup"><span data-stu-id="c3391-128">url</span></span> | <span data-ttu-id="c3391-129">Base de URL toohello servidor Web</span><span class="sxs-lookup"><span data-stu-id="c3391-129">Base URL toohello Web Server</span></span> | <span data-ttu-id="c3391-130">Sim</span><span class="sxs-lookup"><span data-stu-id="c3391-130">Yes</span></span> |
| <span data-ttu-id="c3391-131">authenticationType</span><span class="sxs-lookup"><span data-stu-id="c3391-131">authenticationType</span></span> | <span data-ttu-id="c3391-132">Especifica o tipo de autenticação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c3391-132">Specifies hello authentication type.</span></span> <span data-ttu-id="c3391-133">Os valores permitidos são: **Anônimo**, **Básico**, **Digest**, **Windows** e **ClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="c3391-133">Allowed values are: **Anonymous**, **Basic**, **Digest**, **Windows**, **ClientCertificate**.</span></span> <br><br> <span data-ttu-id="c3391-134">Consulte toosections abaixo da tabela em mais propriedades e exemplos JSON para esses tipos de autenticação, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="c3391-134">Refer toosections below this table on more properties and JSON samples for those authentication types respectively.</span></span> | <span data-ttu-id="c3391-135">Sim</span><span class="sxs-lookup"><span data-stu-id="c3391-135">Yes</span></span> |
| <span data-ttu-id="c3391-136">enableServerCertificateValidation</span><span class="sxs-lookup"><span data-stu-id="c3391-136">enableServerCertificateValidation</span></span> | <span data-ttu-id="c3391-137">Especifique se tooenable servidor SSL a validação de certificado se origem for o servidor da Web HTTPS</span><span class="sxs-lookup"><span data-stu-id="c3391-137">Specify whether tooenable server SSL certificate validation if source is HTTPS Web Server</span></span> | <span data-ttu-id="c3391-138">Não, o padrão é true</span><span class="sxs-lookup"><span data-stu-id="c3391-138">No, default is true</span></span> |
| <span data-ttu-id="c3391-139">gatewayName</span><span class="sxs-lookup"><span data-stu-id="c3391-139">gatewayName</span></span> | <span data-ttu-id="c3391-140">Nome da saudação Data Management Gateway tooconnect tooan origem HTTP no local.</span><span class="sxs-lookup"><span data-stu-id="c3391-140">Name of hello Data Management Gateway tooconnect tooan on-premises HTTP source.</span></span> | <span data-ttu-id="c3391-141">Sim se estiver copiando dados de uma origem HTTP local.</span><span class="sxs-lookup"><span data-stu-id="c3391-141">Yes if copying data from an on-premises HTTP source.</span></span> |
| <span data-ttu-id="c3391-142">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="c3391-142">encryptedCredential</span></span> | <span data-ttu-id="c3391-143">Credencial criptografada tooaccess Olá ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="c3391-143">Encrypted credential tooaccess hello HTTP endpoint.</span></span> <span data-ttu-id="c3391-144">Gerado automaticamente quando você configura as informações de autenticação de saudação no diálogo de pop-up de ClickOnce de assistente ou saudação de cópia.</span><span class="sxs-lookup"><span data-stu-id="c3391-144">Auto-generated when you configure hello authentication information in copy wizard or hello ClickOnce popup dialog.</span></span> | <span data-ttu-id="c3391-145">Não.</span><span class="sxs-lookup"><span data-stu-id="c3391-145">No.</span></span> <span data-ttu-id="c3391-146">Aplique somente quando estiver copiando dados de um servidor HTTP local.</span><span class="sxs-lookup"><span data-stu-id="c3391-146">Apply only when copying data from an on-premises HTTP server.</span></span> |

<span data-ttu-id="c3391-147">Consulte [mover dados entre fontes locais e na nuvem de saudação com Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para obter detalhes sobre como configurar credenciais locais HTTP conector fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="c3391-147">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for details about setting credentials for on-premises HTTP connector data source.</span></span>

### <a name="using-basic-digest-or-windows-authentication"></a><span data-ttu-id="c3391-148">Usando a autenticação Básica, Digest ou Windows</span><span class="sxs-lookup"><span data-stu-id="c3391-148">Using Basic, Digest, or Windows authentication</span></span>

<span data-ttu-id="c3391-149">Definir `authenticationType` como `Basic`, `Digest`, ou `Windows`e especifique Olá seguintes propriedades além Olá conector HTTP genérico aqueles introduzido acima:</span><span class="sxs-lookup"><span data-stu-id="c3391-149">Set `authenticationType` as `Basic`, `Digest`, or `Windows`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="c3391-150">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c3391-150">Property</span></span> | <span data-ttu-id="c3391-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="c3391-151">Description</span></span> | <span data-ttu-id="c3391-152">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="c3391-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3391-153">Nome de Usuário</span><span class="sxs-lookup"><span data-stu-id="c3391-153">username</span></span> | <span data-ttu-id="c3391-154">Nome de usuário tooaccess Olá ponto de extremidade HTTP.</span><span class="sxs-lookup"><span data-stu-id="c3391-154">Username tooaccess hello HTTP endpoint.</span></span> | <span data-ttu-id="c3391-155">Sim</span><span class="sxs-lookup"><span data-stu-id="c3391-155">Yes</span></span> |
| <span data-ttu-id="c3391-156">Senha</span><span class="sxs-lookup"><span data-stu-id="c3391-156">password</span></span> | <span data-ttu-id="c3391-157">Senha do usuário da saudação (nome de usuário).</span><span class="sxs-lookup"><span data-stu-id="c3391-157">Password for hello user (username).</span></span> | <span data-ttu-id="c3391-158">Sim</span><span class="sxs-lookup"><span data-stu-id="c3391-158">Yes</span></span> |

#### <a name="example-using-basic-digest-or-windows-authentication"></a><span data-ttu-id="c3391-159">Exemplo: usando a autenticação Básica, Digest ou Windows</span><span class="sxs-lookup"><span data-stu-id="c3391-159">Example: using Basic, Digest, or Windows authentication</span></span>

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

### <a name="using-clientcertificate-authentication"></a><span data-ttu-id="c3391-160">Usando a autenticação ClientCertificate</span><span class="sxs-lookup"><span data-stu-id="c3391-160">Using ClientCertificate authentication</span></span>

<span data-ttu-id="c3391-161">Definir toouse a autenticação básica, `authenticationType` como `ClientCertificate`e especifique Olá seguintes propriedades além Olá conector HTTP genérico aqueles introduzido acima:</span><span class="sxs-lookup"><span data-stu-id="c3391-161">toouse basic authentication, set `authenticationType` as `ClientCertificate`, and specify hello following properties besides hello HTTP connector generic ones introduced above:</span></span>

| <span data-ttu-id="c3391-162">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c3391-162">Property</span></span> | <span data-ttu-id="c3391-163">Descrição</span><span class="sxs-lookup"><span data-stu-id="c3391-163">Description</span></span> | <span data-ttu-id="c3391-164">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="c3391-164">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c3391-165">embeddedCertData</span><span class="sxs-lookup"><span data-stu-id="c3391-165">embeddedCertData</span></span> | <span data-ttu-id="c3391-166">conteúdo codificado com Base64 Olá de dados binários do arquivo de troca de informações pessoais (PFX) hello.</span><span class="sxs-lookup"><span data-stu-id="c3391-166">hello Base64-encoded contents of binary data of hello Personal Information Exchange (PFX) file.</span></span> | <span data-ttu-id="c3391-167">Especifique a saudação `embeddedCertData` ou `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="c3391-167">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="c3391-168">certThumbprint</span><span class="sxs-lookup"><span data-stu-id="c3391-168">certThumbprint</span></span> | <span data-ttu-id="c3391-169">Olá a impressão digital do certificado Olá foi instalado no repositório de certificados do computador do gateway.</span><span class="sxs-lookup"><span data-stu-id="c3391-169">hello thumbprint of hello certificate that was installed on your gateway machine’s cert store.</span></span> <span data-ttu-id="c3391-170">Aplique somente ao copiar dados de uma origem HTTP local.</span><span class="sxs-lookup"><span data-stu-id="c3391-170">Apply only when copying data from an on-premises HTTP source.</span></span> | <span data-ttu-id="c3391-171">Especifique a saudação `embeddedCertData` ou `certThumbprint`.</span><span class="sxs-lookup"><span data-stu-id="c3391-171">Specify either hello `embeddedCertData` or `certThumbprint`.</span></span> |
| <span data-ttu-id="c3391-172">Senha</span><span class="sxs-lookup"><span data-stu-id="c3391-172">password</span></span> | <span data-ttu-id="c3391-173">Senha associada com o certificado de saudação.</span><span class="sxs-lookup"><span data-stu-id="c3391-173">Password associated with hello certificate.</span></span> | <span data-ttu-id="c3391-174">Não</span><span class="sxs-lookup"><span data-stu-id="c3391-174">No</span></span> |

<span data-ttu-id="c3391-175">Se você usar `certThumbprint` para certificado de autenticação e hello está instalado no repositório pessoal de saudação do computador local hello, você precisa que o serviço de gateway do toogrant Olá permissão de leitura toohello:</span><span class="sxs-lookup"><span data-stu-id="c3391-175">If you use `certThumbprint` for authentication and hello certificate is installed in hello personal store of hello local computer, you need toogrant hello read permission toohello gateway service:</span></span>

1. <span data-ttu-id="c3391-176">Iniciar o MMC (Console de Gerenciamento Microsoft).</span><span class="sxs-lookup"><span data-stu-id="c3391-176">Launch Microsoft Management Console (MMC).</span></span> <span data-ttu-id="c3391-177">Adicionar Olá **certificados** snap-in que Olá destinos **computador Local**.</span><span class="sxs-lookup"><span data-stu-id="c3391-177">Add hello **Certificates** snap-in that targets hello **Local Computer**.</span></span>
2. <span data-ttu-id="c3391-178">Expanda **Certificados**, **Pessoal** e clique em **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="c3391-178">Expand **Certificates**, **Personal**, and click **Certificates**.</span></span>
3. <span data-ttu-id="c3391-179">Certificado de saudação do armazenamento pessoal hello e selecione **todas as tarefas**->**gerenciar chaves particulares...**</span><span class="sxs-lookup"><span data-stu-id="c3391-179">Right-click hello certificate from hello personal store, and select **All Tasks**->**Manage Private Keys...**</span></span>
3. <span data-ttu-id="c3391-180">Em Olá **segurança** guia, adicione a conta de usuário Olá sob a qual o serviço de Host do Gateway de gerenciamento de dados está em execução com certificado de toohello Olá acesso de leitura.</span><span class="sxs-lookup"><span data-stu-id="c3391-180">On hello **Security** tab, add hello user account under which Data Management Gateway Host Service is running with hello read access toohello certificate.</span></span>  

#### <a name="example-using-client-certificate"></a><span data-ttu-id="c3391-181">Exemplo: usando o certificado do cliente</span><span class="sxs-lookup"><span data-stu-id="c3391-181">Example: using client certificate</span></span>
<span data-ttu-id="c3391-182">Isso vinculado links serviço seu servidor de web data factory tooan locais HTTP.</span><span class="sxs-lookup"><span data-stu-id="c3391-182">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="c3391-183">Ele usa um certificado de cliente é instalado na máquina de saudação com Gateway de gerenciamento de dados instalado.</span><span class="sxs-lookup"><span data-stu-id="c3391-183">It uses a client certificate that is installed on hello machine with Data Management Gateway installed.</span></span>

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

#### <a name="example-using-client-certificate-in-a-file"></a><span data-ttu-id="c3391-184">Exemplo: usando o certificado do cliente em um arquivo</span><span class="sxs-lookup"><span data-stu-id="c3391-184">Example: using client certificate in a file</span></span>
<span data-ttu-id="c3391-185">Isso vinculado links serviço seu servidor de web data factory tooan locais HTTP.</span><span class="sxs-lookup"><span data-stu-id="c3391-185">This linked service links your data factory tooan on-premises HTTP web server.</span></span> <span data-ttu-id="c3391-186">Ele usa um arquivo de certificado de cliente no computador de saudação com Gateway de gerenciamento de dados instalado.</span><span class="sxs-lookup"><span data-stu-id="c3391-186">It uses a client certificate file on hello machine with Data Management Gateway installed.</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="c3391-187">Propriedades do conjunto de dados</span><span class="sxs-lookup"><span data-stu-id="c3391-187">Dataset properties</span></span>
<span data-ttu-id="c3391-188">Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="c3391-188">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c3391-189">As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).</span><span class="sxs-lookup"><span data-stu-id="c3391-189">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="c3391-190">Olá **typeProperties** é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="c3391-190">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="c3391-191">Olá typeProperties seção de conjunto de dados do tipo **Http** tem Olá seguintes propriedades</span><span class="sxs-lookup"><span data-stu-id="c3391-191">hello typeProperties section for dataset of type **Http** has hello following properties</span></span>

| <span data-ttu-id="c3391-192">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c3391-192">Property</span></span> | <span data-ttu-id="c3391-193">Descrição</span><span class="sxs-lookup"><span data-stu-id="c3391-193">Description</span></span> | <span data-ttu-id="c3391-194">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="c3391-194">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c3391-195">type</span><span class="sxs-lookup"><span data-stu-id="c3391-195">type</span></span> | <span data-ttu-id="c3391-196">Tipo de saudação do conjunto de dados de saudação especificado.</span><span class="sxs-lookup"><span data-stu-id="c3391-196">Specified hello type of hello dataset.</span></span> <span data-ttu-id="c3391-197">deve ser definido muito`Http`.</span><span class="sxs-lookup"><span data-stu-id="c3391-197">must be set too`Http`.</span></span> | <span data-ttu-id="c3391-198">Sim</span><span class="sxs-lookup"><span data-stu-id="c3391-198">Yes</span></span> |
| <span data-ttu-id="c3391-199">relativeUrl</span><span class="sxs-lookup"><span data-stu-id="c3391-199">relativeUrl</span></span> | <span data-ttu-id="c3391-200">Um relativa URL toohello de recursos que contém dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="c3391-200">A relative URL toohello resource that contains hello data.</span></span> <span data-ttu-id="c3391-201">Quando não for especificado, somente URL Olá especificado na definição de serviço vinculada de saudação é usado.</span><span class="sxs-lookup"><span data-stu-id="c3391-201">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> <br><br> <span data-ttu-id="c3391-202">URL do tooconstruct dinâmico, você pode usar [funções da fábrica de dados e variáveis de sistema](data-factory-functions-variables.md), por exemplo, "relativeUrl": "$$Text.Format (' Meu/relatório? mês = {0:yyyy}-{0:MM} & fmt = csv', SliceStart)".</span><span class="sxs-lookup"><span data-stu-id="c3391-202">tooconstruct dynamic URL, you can use [Data Factory functions and system variables](data-factory-functions-variables.md), e.g. "relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)".</span></span> | <span data-ttu-id="c3391-203">Não</span><span class="sxs-lookup"><span data-stu-id="c3391-203">No</span></span> |
| <span data-ttu-id="c3391-204">requestMethod</span><span class="sxs-lookup"><span data-stu-id="c3391-204">requestMethod</span></span> | <span data-ttu-id="c3391-205">Método Http.</span><span class="sxs-lookup"><span data-stu-id="c3391-205">Http method.</span></span> <span data-ttu-id="c3391-206">Os valores permitidos são **GET** ou **POST**.</span><span class="sxs-lookup"><span data-stu-id="c3391-206">Allowed values are **GET** or **POST**.</span></span> | <span data-ttu-id="c3391-207">Não.</span><span class="sxs-lookup"><span data-stu-id="c3391-207">No.</span></span> <span data-ttu-id="c3391-208">O padrão é `GET`.</span><span class="sxs-lookup"><span data-stu-id="c3391-208">Default is `GET`.</span></span> |
| <span data-ttu-id="c3391-209">additionalHeaders</span><span class="sxs-lookup"><span data-stu-id="c3391-209">additionalHeaders</span></span> | <span data-ttu-id="c3391-210">Cabeçalhos de solicitação HTTP adicionais.</span><span class="sxs-lookup"><span data-stu-id="c3391-210">Additional HTTP request headers.</span></span> | <span data-ttu-id="c3391-211">Não</span><span class="sxs-lookup"><span data-stu-id="c3391-211">No</span></span> |
| <span data-ttu-id="c3391-212">requestBody</span><span class="sxs-lookup"><span data-stu-id="c3391-212">requestBody</span></span> | <span data-ttu-id="c3391-213">O corpo da solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="c3391-213">Body for HTTP request.</span></span> | <span data-ttu-id="c3391-214">Não</span><span class="sxs-lookup"><span data-stu-id="c3391-214">No</span></span> |
| <span data-ttu-id="c3391-215">formato</span><span class="sxs-lookup"><span data-stu-id="c3391-215">format</span></span> | <span data-ttu-id="c3391-216">Se você quiser toosimply **recuperar dados de saudação do ponto de extremidade HTTP como-é** sem analisá-lo, ignore essa configuração de formato.</span><span class="sxs-lookup"><span data-stu-id="c3391-216">If you want toosimply **retrieve hello data from HTTP endpoint as-is** without parsing it, skip this format settings.</span></span> <br><br> <span data-ttu-id="c3391-217">Se você quiser resposta HTTP de saudação tooparse conteúdo durante a cópia, Olá tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="c3391-217">If you want tooparse hello HTTP response content during copy, hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="c3391-218">Para saber mais, veja as seções [Formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [Formato Json](data-factory-supported-file-and-compression-formats.md#json-format), [Formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [Formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [Formato Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format).</span><span class="sxs-lookup"><span data-stu-id="c3391-218">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> |<span data-ttu-id="c3391-219">Não</span><span class="sxs-lookup"><span data-stu-id="c3391-219">No</span></span> |
| <span data-ttu-id="c3391-220">compactação</span><span class="sxs-lookup"><span data-stu-id="c3391-220">compression</span></span> | <span data-ttu-id="c3391-221">Especifica tipo de saudação e nível de compactação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="c3391-221">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="c3391-222">Os tipos com suporte são: **GZip**, **Deflate**, **BZip2** e **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="c3391-222">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="c3391-223">Os níveis com suporte são **Ideal** e **O mais rápido**.</span><span class="sxs-lookup"><span data-stu-id="c3391-223">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="c3391-224">Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory).</span><span class="sxs-lookup"><span data-stu-id="c3391-224">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="c3391-225">Não</span><span class="sxs-lookup"><span data-stu-id="c3391-225">No</span></span> |

### <a name="example-using-hello-get-default-method"></a><span data-ttu-id="c3391-226">Exemplo: usando o método do hello GET (padrão)</span><span class="sxs-lookup"><span data-stu-id="c3391-226">Example: using hello GET (default) method</span></span>

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

### <a name="example-using-hello-post-method"></a><span data-ttu-id="c3391-227">Exemplo: usando o método POST de saudação</span><span class="sxs-lookup"><span data-stu-id="c3391-227">Example: using hello POST method</span></span>

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

## <a name="copy-activity-properties"></a><span data-ttu-id="c3391-228">Propriedades da atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="c3391-228">Copy activity properties</span></span>
<span data-ttu-id="c3391-229">Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="c3391-229">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c3391-230">As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.</span><span class="sxs-lookup"><span data-stu-id="c3391-230">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="c3391-231">As propriedades disponíveis no hello **typeProperties** seção de atividade Olá Olá outro lado variam de acordo com cada tipo de atividade.</span><span class="sxs-lookup"><span data-stu-id="c3391-231">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="c3391-232">Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.</span><span class="sxs-lookup"><span data-stu-id="c3391-232">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="c3391-233">Atualmente, quando a fonte de saudação na atividade de cópia é do tipo **HttpSource**, Olá propriedades a seguir têm suporte.</span><span class="sxs-lookup"><span data-stu-id="c3391-233">Currently, when hello source in copy activity is of type **HttpSource**, hello following properties are supported.</span></span>

| <span data-ttu-id="c3391-234">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c3391-234">Property</span></span> | <span data-ttu-id="c3391-235">Descrição</span><span class="sxs-lookup"><span data-stu-id="c3391-235">Description</span></span> | <span data-ttu-id="c3391-236">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="c3391-236">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="c3391-237">httpRequestTimeout</span><span class="sxs-lookup"><span data-stu-id="c3391-237">httpRequestTimeout</span></span> | <span data-ttu-id="c3391-238">Olá tempo limite (TimeSpan) para tooget de solicitação HTTP Olá uma resposta.</span><span class="sxs-lookup"><span data-stu-id="c3391-238">hello timeout (TimeSpan) for hello HTTP request tooget a response.</span></span> <span data-ttu-id="c3391-239">É Olá timeout tooget uma resposta não Olá timeout tooread dados de resposta.</span><span class="sxs-lookup"><span data-stu-id="c3391-239">It is hello timeout tooget a response, not hello timeout tooread response data.</span></span> | <span data-ttu-id="c3391-240">Não.</span><span class="sxs-lookup"><span data-stu-id="c3391-240">No.</span></span> <span data-ttu-id="c3391-241">Valor padrão: 00:01:40</span><span class="sxs-lookup"><span data-stu-id="c3391-241">Default value: 00:01:40</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="c3391-242">Formatos de arquivo e de compactação com suporte</span><span class="sxs-lookup"><span data-stu-id="c3391-242">Supported file and compression formats</span></span>
<span data-ttu-id="c3391-243">Consulte o artigo [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="c3391-243">See [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="c3391-244">Exemplos de JSON</span><span class="sxs-lookup"><span data-stu-id="c3391-244">JSON examples</span></span>
<span data-ttu-id="c3391-245">saudação de exemplo a seguir fornece as definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c3391-245">hello following example provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c3391-246">Eles mostram como tooAzure armazenamento de Blob da fonte de dados de toocopy de HTTP.</span><span class="sxs-lookup"><span data-stu-id="c3391-246">They show how toocopy data from HTTP source tooAzure Blob Storage.</span></span> <span data-ttu-id="c3391-247">No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3391-247">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-http-source-tooazure-blob-storage"></a><span data-ttu-id="c3391-248">Exemplo: Copiar dados de origem HTTP tooAzure armazenamento de Blob</span><span class="sxs-lookup"><span data-stu-id="c3391-248">Example: Copy data from HTTP source tooAzure Blob Storage</span></span>
<span data-ttu-id="c3391-249">Olá solução da fábrica de dados para este exemplo contém Olá entidades da fábrica de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="c3391-249">hello Data Factory solution for this sample contains hello following Data Factory entities:</span></span>

1. <span data-ttu-id="c3391-250">Um serviço vinculado do tipo [HTTP](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c3391-250">A linked service of type [HTTP](#linked-service-properties).</span></span>
2. <span data-ttu-id="c3391-251">Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c3391-251">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c3391-252">Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [Http](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c3391-252">An input [dataset](data-factory-create-datasets.md) of type [Http](#dataset-properties).</span></span>
4. <span data-ttu-id="c3391-253">Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c3391-253">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c3391-254">Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [HttpSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c3391-254">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [HttpSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c3391-255">exemplo Hello copia dados de uma origem HTTP tooan BLOBs do Azure a cada hora.</span><span class="sxs-lookup"><span data-stu-id="c3391-255">hello sample copies data from an HTTP source tooan Azure blob every hour.</span></span> <span data-ttu-id="c3391-256">propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="c3391-256">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="http-linked-service"></a><span data-ttu-id="c3391-257">Serviço vinculado HTTP</span><span class="sxs-lookup"><span data-stu-id="c3391-257">HTTP linked service</span></span>
<span data-ttu-id="c3391-258">Este exemplo usa Olá HTTP vinculado de serviço com a autenticação anônima.</span><span class="sxs-lookup"><span data-stu-id="c3391-258">This example uses hello HTTP linked service with anonymous authentication.</span></span> <span data-ttu-id="c3391-259">Confira a seção [Serviço vinculado HTTP](#linked-service-properties) para ver os diferentes tipos de autenticação que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="c3391-259">See [HTTP linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="c3391-260">Serviço vinculado de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c3391-260">Azure Storage linked service</span></span>

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

### <a name="http-input-dataset"></a><span data-ttu-id="c3391-261">Conjunto de dados de entrada HTTP</span><span class="sxs-lookup"><span data-stu-id="c3391-261">HTTP input dataset</span></span>
<span data-ttu-id="c3391-262">Configuração **externo** muito**true** informa o serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.</span><span class="sxs-lookup"><span data-stu-id="c3391-262">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="c3391-263">Conjunto de dados de saída de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="c3391-263">Azure Blob output dataset</span></span>

<span data-ttu-id="c3391-264">Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1).</span><span class="sxs-lookup"><span data-stu-id="c3391-264">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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

### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="c3391-265">Pipeline com Atividade de cópia</span><span class="sxs-lookup"><span data-stu-id="c3391-265">Pipeline with Copy activity</span></span>

<span data-ttu-id="c3391-266">Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora.</span><span class="sxs-lookup"><span data-stu-id="c3391-266">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="c3391-267">Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**HttpSource** e **coletor** tipo está definido muito**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c3391-267">In hello pipeline JSON definition, hello **source** type is set too**HttpSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="c3391-268">Consulte [HttpSource](#copy-activity-properties) para lista de saudação de propriedades com suporte pelo Olá HttpSource.</span><span class="sxs-lookup"><span data-stu-id="c3391-268">See [HttpSource](#copy-activity-properties) for hello list of properties supported by hello HttpSource.</span></span>

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
        "description": "Copy from an HTTP source tooan Azure blob",
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
> <span data-ttu-id="c3391-269">colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c3391-269">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c3391-270">Desempenho e Ajuste</span><span class="sxs-lookup"><span data-stu-id="c3391-270">Performance and Tuning</span></span>
<span data-ttu-id="c3391-271">Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.</span><span class="sxs-lookup"><span data-stu-id="c3391-271">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
