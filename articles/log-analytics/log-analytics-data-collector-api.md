---
title: "API de coletor de dados de HTTP de análise de aaaLog | Microsoft Docs"
description: "Você pode usar o hello API do coletor de dados do Log Analytics HTTP tooadd POST JSON toohello análise de Log repositório de dados de qualquer cliente que pode chamar a API REST de saudação. Este artigo descreve como toouse Olá API e tem exemplos de como toopublish dados usando linguagens de programação diferentes."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: c2921082831c49da764d946ac9c4fab975a38185
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-data-toolog-analytics-with-hello-http-data-collector-api"></a><span data-ttu-id="14f02-104">Enviar dados tooLog análise com hello API de coletor de dados HTTP</span><span class="sxs-lookup"><span data-stu-id="14f02-104">Send data tooLog Analytics with hello HTTP Data Collector API</span></span>
<span data-ttu-id="14f02-105">Este artigo mostra como toouse Olá API de coletor de dados HTTP toosend dados tooLog análise de um cliente de API REST.</span><span class="sxs-lookup"><span data-stu-id="14f02-105">This article shows you how toouse hello HTTP Data Collector API toosend data tooLog Analytics from a REST API client.</span></span>  <span data-ttu-id="14f02-106">Ele descreve como tooformat dados coletados pelo seu script ou aplicativo, incluí-lo em uma solicitação e ter essa solicitação autorizada pela análise de Log.</span><span class="sxs-lookup"><span data-stu-id="14f02-106">It describes how tooformat data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="14f02-107">Os exemplos são fornecidos para PowerShell, C# e Python.</span><span class="sxs-lookup"><span data-stu-id="14f02-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="14f02-108">Conceitos</span><span class="sxs-lookup"><span data-stu-id="14f02-108">Concepts</span></span>
<span data-ttu-id="14f02-109">Você pode usar o hello API de coletor de dados HTTP toosend dados tooLog análise de qualquer cliente que pode chamar uma API REST.</span><span class="sxs-lookup"><span data-stu-id="14f02-109">You can use hello HTTP Data Collector API toosend data tooLog Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="14f02-110">Isso pode ser um runbook na automação do Azure que o gerenciamento de coleta dados do Azure ou outra nuvem ou podem ser um sistema de gerenciamento alternativo que usa análise de Log tooconsolidate e analisar dados.</span><span class="sxs-lookup"><span data-stu-id="14f02-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics tooconsolidate and analyze data.</span></span>

<span data-ttu-id="14f02-111">Todos os dados no repositório de análise de Log de saudação é armazenado como um registro com um tipo de registro específico.</span><span class="sxs-lookup"><span data-stu-id="14f02-111">All data in hello Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="14f02-112">Você pode formatar seu toohello toosend de dados API de coletor de dados HTTP como vários registros em JSON.</span><span class="sxs-lookup"><span data-stu-id="14f02-112">You format your data toosend toohello HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="14f02-113">Quando você envia dados hello, um registro individual é criado no repositório de saudação para cada registro na carga de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="14f02-113">When you submit hello data, an individual record is created in hello repository for each record in hello request payload.</span></span>


![Visão geral do Coletor de Dados HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="14f02-115">Criar uma solicitação</span><span class="sxs-lookup"><span data-stu-id="14f02-115">Create a request</span></span>
<span data-ttu-id="14f02-116">API de coletor de dados do toouse Olá HTTP, você criar uma solicitação POST que inclui Olá dados toosend na notação JSON (JavaScript Object).</span><span class="sxs-lookup"><span data-stu-id="14f02-116">toouse hello HTTP Data Collector API, you create a POST request that includes hello data toosend in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="14f02-117">Olá três tabelas lista Olá atributos que são necessários para cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="14f02-117">hello next three tables list hello attributes that are required for each request.</span></span> <span data-ttu-id="14f02-118">Descrevemos cada atributo em mais detalhes posteriormente neste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="14f02-118">We describe each attribute in more detail later in hello article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="14f02-119">URI da solicitação</span><span class="sxs-lookup"><span data-stu-id="14f02-119">Request URI</span></span>
| <span data-ttu-id="14f02-120">Atributo</span><span class="sxs-lookup"><span data-stu-id="14f02-120">Attribute</span></span> | <span data-ttu-id="14f02-121">Propriedade</span><span class="sxs-lookup"><span data-stu-id="14f02-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="14f02-122">Método</span><span class="sxs-lookup"><span data-stu-id="14f02-122">Method</span></span> |<span data-ttu-id="14f02-123">POST</span><span class="sxs-lookup"><span data-stu-id="14f02-123">POST</span></span> |
| <span data-ttu-id="14f02-124">URI</span><span class="sxs-lookup"><span data-stu-id="14f02-124">URI</span></span> |<span data-ttu-id="14f02-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="14f02-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="14f02-126">Tipo de conteúdo</span><span class="sxs-lookup"><span data-stu-id="14f02-126">Content type</span></span> |<span data-ttu-id="14f02-127">aplicativo/json</span><span class="sxs-lookup"><span data-stu-id="14f02-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="14f02-128">Solicitar parâmetros de URI (Uniform Resource Identifier)</span><span class="sxs-lookup"><span data-stu-id="14f02-128">Request URI parameters</span></span>
| <span data-ttu-id="14f02-129">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="14f02-129">Parameter</span></span> | <span data-ttu-id="14f02-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="14f02-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="14f02-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="14f02-131">CustomerID</span></span> |<span data-ttu-id="14f02-132">Olá identificador exclusivo para o espaço de trabalho do hello Microsoft Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="14f02-132">hello unique identifier for hello Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="14f02-133">Recurso</span><span class="sxs-lookup"><span data-stu-id="14f02-133">Resource</span></span> |<span data-ttu-id="14f02-134">nome do recurso Olá API: api/logs.</span><span class="sxs-lookup"><span data-stu-id="14f02-134">hello API resource name: /api/logs.</span></span> |
| <span data-ttu-id="14f02-135">Versão da API</span><span class="sxs-lookup"><span data-stu-id="14f02-135">API Version</span></span> |<span data-ttu-id="14f02-136">versão de saudação do hello API toouse com esta solicitação.</span><span class="sxs-lookup"><span data-stu-id="14f02-136">hello version of hello API toouse with this request.</span></span> <span data-ttu-id="14f02-137">Atualmente, ela é 2016-04-01.</span><span class="sxs-lookup"><span data-stu-id="14f02-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="14f02-138">Cabeçalhos da solicitação</span><span class="sxs-lookup"><span data-stu-id="14f02-138">Request headers</span></span>
| <span data-ttu-id="14f02-139">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="14f02-139">Header</span></span> | <span data-ttu-id="14f02-140">Descrição</span><span class="sxs-lookup"><span data-stu-id="14f02-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="14f02-141">Autorização</span><span class="sxs-lookup"><span data-stu-id="14f02-141">Authorization</span></span> |<span data-ttu-id="14f02-142">assinatura de autorização de saudação.</span><span class="sxs-lookup"><span data-stu-id="14f02-142">hello authorization signature.</span></span> <span data-ttu-id="14f02-143">Artigo hello, você pode ler sobre como cabeçalho toocreate um HMAC-SHA256.</span><span class="sxs-lookup"><span data-stu-id="14f02-143">Later in hello article, you can read about how toocreate an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="14f02-144">Log-Type</span><span class="sxs-lookup"><span data-stu-id="14f02-144">Log-Type</span></span> |<span data-ttu-id="14f02-145">Especifica o tipo de registro de saudação de dados de saudação que está sendo enviados.</span><span class="sxs-lookup"><span data-stu-id="14f02-145">Specify hello record type of hello data that is being submitted.</span></span> <span data-ttu-id="14f02-146">Atualmente, o tipo de log Olá dá suporte a somente caracteres alfa.</span><span class="sxs-lookup"><span data-stu-id="14f02-146">Currently, hello log type supports only alpha characters.</span></span> <span data-ttu-id="14f02-147">Ele não dá suporte a caracteres alfanuméricos ou caracteres especiais.</span><span class="sxs-lookup"><span data-stu-id="14f02-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="14f02-148">x-ms-date</span><span class="sxs-lookup"><span data-stu-id="14f02-148">x-ms-date</span></span> |<span data-ttu-id="14f02-149">Data de saudação solicitação Olá foi processada, no formato RFC 1123.</span><span class="sxs-lookup"><span data-stu-id="14f02-149">hello date that hello request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="14f02-150">time-generated-field</span><span class="sxs-lookup"><span data-stu-id="14f02-150">time-generated-field</span></span> |<span data-ttu-id="14f02-151">nome de saudação de um campo nos dados de saudação que contém o carimbo de hora Olá Olá do item de dados.</span><span class="sxs-lookup"><span data-stu-id="14f02-151">hello name of a field in hello data that contains hello timestamp of hello data item.</span></span> <span data-ttu-id="14f02-152">Se você especificar um campo, seu conteúdo será usado para **TimeGenerated**.</span><span class="sxs-lookup"><span data-stu-id="14f02-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="14f02-153">Se esse campo não for especificado, Olá padrão para **TimeGenerated** é tempo de saudação que hello mensagem está incluída.</span><span class="sxs-lookup"><span data-stu-id="14f02-153">If this field isn’t specified, hello default for **TimeGenerated** is hello time that hello message is ingested.</span></span> <span data-ttu-id="14f02-154">conteúdo de saudação do campo de mensagem de saudação deve seguir o formato de saudação ISO 8601 aaaa-MM-ddTHH.</span><span class="sxs-lookup"><span data-stu-id="14f02-154">hello contents of hello message field should follow hello ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="14f02-155">Autorização</span><span class="sxs-lookup"><span data-stu-id="14f02-155">Authorization</span></span>
<span data-ttu-id="14f02-156">Qualquer API de coletor de dados de HTTP de análise de Log de toohello de solicitação deve incluir um cabeçalho de autorização.</span><span class="sxs-lookup"><span data-stu-id="14f02-156">Any request toohello Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="14f02-157">tooauthenticate uma solicitação, você deve assinar a solicitação de saudação com hello primário ou a chave secundária Olá para espaço de trabalho de saudação que está fazendo a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="14f02-157">tooauthenticate a request, you must sign hello request with either hello primary or hello secondary key for hello workspace that is making hello request.</span></span> <span data-ttu-id="14f02-158">Em seguida, passe essa assinatura como parte da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="14f02-158">Then, pass that signature as part of hello request.</span></span>   

<span data-ttu-id="14f02-159">Aqui é o formato de saudação do cabeçalho de autorização de saudação:</span><span class="sxs-lookup"><span data-stu-id="14f02-159">Here's hello format for hello authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="14f02-160">*WorkspaceID* é o identificador exclusivo de saudação do espaço de trabalho do hello Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="14f02-160">*WorkspaceID* is hello unique identifier for hello Operations Management Suite workspace.</span></span> <span data-ttu-id="14f02-161">*Assinatura* é um [baseadas em Hash HMAC Message Authentication Code ()](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) que é construído a partir de solicitação hello e, em seguida, computado usando Olá [algoritmo SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span><span class="sxs-lookup"><span data-stu-id="14f02-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from hello request and then computed by using hello [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="14f02-162">Em seguida, você o codifica usando a codificação Base64.</span><span class="sxs-lookup"><span data-stu-id="14f02-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="14f02-163">Use este Olá tooencode de formato **SharedKey** cadeia de caracteres de assinatura:</span><span class="sxs-lookup"><span data-stu-id="14f02-163">Use this format tooencode hello **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="14f02-164">Aqui está um exemplo de uma cadeia de caracteres de assinatura:</span><span class="sxs-lookup"><span data-stu-id="14f02-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="14f02-165">Quando há uma cadeia de caracteres de assinatura hello, codificá-lo usando Olá algoritmo HMAC-SHA256 na Olá cadeia de caracteres codificados em UTF-8 e, em seguida, codificar o resultado de saudação como Base64.</span><span class="sxs-lookup"><span data-stu-id="14f02-165">When you have hello signature string, encode it by using hello HMAC-SHA256 algorithm on hello UTF-8-encoded string, and then encode hello result as Base64.</span></span> <span data-ttu-id="14f02-166">Use este formato:</span><span class="sxs-lookup"><span data-stu-id="14f02-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="14f02-167">exemplos de saudação nas seções próximos Olá têm toohelp de código de exemplo, crie um cabeçalho de autorização.</span><span class="sxs-lookup"><span data-stu-id="14f02-167">hello samples in hello next sections have sample code toohelp you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="14f02-168">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="14f02-168">Request body</span></span>
<span data-ttu-id="14f02-169">corpo de saudação de mensagem de saudação deve estar em JSON.</span><span class="sxs-lookup"><span data-stu-id="14f02-169">hello body of hello message must be in JSON.</span></span> <span data-ttu-id="14f02-170">Ele deve incluir um ou mais registros com pares de nome e valor da propriedade Olá neste formato:</span><span class="sxs-lookup"><span data-stu-id="14f02-170">It must include one or more records with hello property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="14f02-171">Você pode processar em lotes vários registros em uma única solicitação usando Olá formato a seguir.</span><span class="sxs-lookup"><span data-stu-id="14f02-171">You can batch multiple records together in a single request by using hello following format.</span></span> <span data-ttu-id="14f02-172">Todos os registros de saudação devem ser Olá mesmo tipo de registro.</span><span class="sxs-lookup"><span data-stu-id="14f02-172">All hello records must be hello same record type.</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a><span data-ttu-id="14f02-173">Propriedades e o tipo de registro</span><span class="sxs-lookup"><span data-stu-id="14f02-173">Record type and properties</span></span>
<span data-ttu-id="14f02-174">Você definir um tipo de registro personalizadas ao enviar dados por meio de saudação API de coletor de dados de HTTP de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="14f02-174">You define a custom record type when you submit data through hello Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="14f02-175">No momento, você não pode gravar dados tooexisting tipos de registros que foram criados por outros tipos de dados e soluções.</span><span class="sxs-lookup"><span data-stu-id="14f02-175">Currently, you can't write data tooexisting record types that were created by other data types and solutions.</span></span> <span data-ttu-id="14f02-176">Análise de log lê os dados de entrada hello e, em seguida, cria propriedades que correspondem a tipos de dados de saudação de valores de saudação que você inserir.</span><span class="sxs-lookup"><span data-stu-id="14f02-176">Log Analytics reads hello incoming data and then creates properties that match hello data types of hello values that you enter.</span></span>

<span data-ttu-id="14f02-177">Cada toohello solicitação API de análise de Log deve incluir um **tipo de Log** cabeçalho com nome Olá Olá ao tipo de registro.</span><span class="sxs-lookup"><span data-stu-id="14f02-177">Each request toohello Log Analytics API must include a **Log-Type** header with hello name for hello record type.</span></span> <span data-ttu-id="14f02-178">sufixo de saudação **_CL** é acrescentada automaticamente toohello nome toodistinguish do log de outros tipos como um log personalizado.</span><span class="sxs-lookup"><span data-stu-id="14f02-178">hello suffix **_CL** is automatically appended toohello name you enter toodistinguish it from other log types as a custom log.</span></span> <span data-ttu-id="14f02-179">Por exemplo, se você inserir o nome da saudação **MyNewRecordType**, análise de Log cria um registro com tipo hello **MyNewRecordType_CL**.</span><span class="sxs-lookup"><span data-stu-id="14f02-179">For example, if you enter hello name **MyNewRecordType**, Log Analytics creates a record with hello type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="14f02-180">Isso ajuda a garantir que não haja nenhum conflito entre os nomes de tipo criados pelo usuário e aqueles fornecidos nas soluções atuais ou futuras da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="14f02-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="14f02-181">tooidentify de tipo de dados de uma propriedade, a análise de Log adiciona um nome de propriedade toohello sufixo.</span><span class="sxs-lookup"><span data-stu-id="14f02-181">tooidentify a property's data type, Log Analytics adds a suffix toohello property name.</span></span> <span data-ttu-id="14f02-182">Se uma propriedade contiver um valor nulo, a propriedade de saudação não está incluída no registro.</span><span class="sxs-lookup"><span data-stu-id="14f02-182">If a property contains a null value, hello property is not included in that record.</span></span> <span data-ttu-id="14f02-183">Esta tabela lista o tipo de dados de propriedade hello e sufixo correspondente:</span><span class="sxs-lookup"><span data-stu-id="14f02-183">This table lists hello property data type and corresponding suffix:</span></span>

| <span data-ttu-id="14f02-184">Tipo de dados de propriedade</span><span class="sxs-lookup"><span data-stu-id="14f02-184">Property data type</span></span> | <span data-ttu-id="14f02-185">Suffix</span><span class="sxs-lookup"><span data-stu-id="14f02-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="14f02-186">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="14f02-186">String</span></span> |<span data-ttu-id="14f02-187">_s</span><span class="sxs-lookup"><span data-stu-id="14f02-187">_s</span></span> |
| <span data-ttu-id="14f02-188">Booliano</span><span class="sxs-lookup"><span data-stu-id="14f02-188">Boolean</span></span> |<span data-ttu-id="14f02-189">_b</span><span class="sxs-lookup"><span data-stu-id="14f02-189">_b</span></span> |
| <span data-ttu-id="14f02-190">Duplo</span><span class="sxs-lookup"><span data-stu-id="14f02-190">Double</span></span> |<span data-ttu-id="14f02-191">_d</span><span class="sxs-lookup"><span data-stu-id="14f02-191">_d</span></span> |
| <span data-ttu-id="14f02-192">Data/hora</span><span class="sxs-lookup"><span data-stu-id="14f02-192">Date/time</span></span> |<span data-ttu-id="14f02-193">_t</span><span class="sxs-lookup"><span data-stu-id="14f02-193">_t</span></span> |
| <span data-ttu-id="14f02-194">GUID</span><span class="sxs-lookup"><span data-stu-id="14f02-194">GUID</span></span> |<span data-ttu-id="14f02-195">_g</span><span class="sxs-lookup"><span data-stu-id="14f02-195">_g</span></span> |

<span data-ttu-id="14f02-196">tipo de dados de saudação que usa análise de Log para cada propriedade depende se o tipo de registro de saudação para novo registro de saudação já existe.</span><span class="sxs-lookup"><span data-stu-id="14f02-196">hello data type that Log Analytics uses for each property depends on whether hello record type for hello new record already exists.</span></span>

* <span data-ttu-id="14f02-197">Se o tipo de registro de saudação não existir, a análise de Log cria um novo.</span><span class="sxs-lookup"><span data-stu-id="14f02-197">If hello record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="14f02-198">Análise de log usa Olá JSON inferência toodetermine Olá tipo de dados para cada propriedade para o novo registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="14f02-198">Log Analytics uses hello JSON type inference toodetermine hello data type for each property for hello new record.</span></span>
* <span data-ttu-id="14f02-199">Se o tipo de registro Olá existir, análise de Log tentativas toocreate um novo registro com base nas propriedades existentes.</span><span class="sxs-lookup"><span data-stu-id="14f02-199">If hello record type does exist, Log Analytics attempts toocreate a new record based on existing properties.</span></span> <span data-ttu-id="14f02-200">Se hello tipo de dados para uma propriedade no novo registro de saudação não corresponder e não pode ser convertido toohello existente do tipo ou se hello registro inclui uma propriedade que não existe, a análise de Log cria uma nova propriedade que tem o sufixo relevantes hello.</span><span class="sxs-lookup"><span data-stu-id="14f02-200">If hello data type for a property in hello new record doesn’t match and can’t be converted toohello existing type, or if hello record includes a property that doesn’t exist, Log Analytics creates a new property that has hello relevant suffix.</span></span>

<span data-ttu-id="14f02-201">Por exemplo, esta entrada de envio criaria um registro com três propriedades, **number_d**, **boolean_b** e **string_s**:</span><span class="sxs-lookup"><span data-stu-id="14f02-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![Registro de exemplo 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="14f02-203">Se você, em seguida, enviar essa próxima entrada, com todos os valores formatados como cadeias de caracteres, propriedades de saudação não seriam alterado.</span><span class="sxs-lookup"><span data-stu-id="14f02-203">If you then submitted this next entry, with all values formatted as strings, hello properties would not change.</span></span> <span data-ttu-id="14f02-204">Esses valores podem ser convertidos tooexisting tipos de dados:</span><span class="sxs-lookup"><span data-stu-id="14f02-204">These values can be converted tooexisting data types:</span></span>

![Registro de exemplo 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="14f02-206">Mas, se você fez, em seguida, o próximo envio, análise de Log cria Olá novas propriedades **boolean_d** e **string_d**.</span><span class="sxs-lookup"><span data-stu-id="14f02-206">But, if you then made this next submission, Log Analytics would create hello new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="14f02-207">Esses valores não podem ser convertidos:</span><span class="sxs-lookup"><span data-stu-id="14f02-207">These values can't be converted:</span></span>

![Registro de exemplo 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="14f02-209">Se você, então, enviadas Olá seguinte entrada, antes de tipo de registro de saudação foi criado, a análise de Log criaria um registro com três propriedades, **núm_s**, **boolean_s**, e **string_s**.</span><span class="sxs-lookup"><span data-stu-id="14f02-209">If you then submitted hello following entry, before hello record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="14f02-210">Nesta entrada, cada um dos valores de saudação inicial é formatada como uma cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="14f02-210">In this entry, each of hello initial values is formatted as a string:</span></span>

![Registro de exemplo 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="14f02-212">Limites de dados</span><span class="sxs-lookup"><span data-stu-id="14f02-212">Data limits</span></span>
<span data-ttu-id="14f02-213">Há algumas restrições em torno dos dados Olá postadas toohello coleta de dados de análise de Log de API.</span><span class="sxs-lookup"><span data-stu-id="14f02-213">There are some constraints around hello data posted toohello Log Analytics Data collection API.</span></span>

* <span data-ttu-id="14f02-214">Máximo de 30 MB por post tooLog API do coletor de dados de análise.</span><span class="sxs-lookup"><span data-stu-id="14f02-214">Maximum of 30 MB per post tooLog Analytics Data Collector API.</span></span> <span data-ttu-id="14f02-215">Este é um limite de tamanho para um único post.</span><span class="sxs-lookup"><span data-stu-id="14f02-215">This is a size limit for a single post.</span></span> <span data-ttu-id="14f02-216">Se dados de saudação de uma postagem único que excede 30 MB, você deve dividi-Olá dados toosmaller dimensionado blocos e enviá-los simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="14f02-216">If hello data from a single post that exceeds 30 MB, you should split hello data up toosmaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="14f02-217">Limite máximo de 32 KB para valores de campo.</span><span class="sxs-lookup"><span data-stu-id="14f02-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="14f02-218">Se o valor do campo Olá é maior do que 32 KB, dados saudação serão truncados.</span><span class="sxs-lookup"><span data-stu-id="14f02-218">If hello field value is greater than 32 KB, hello data will be truncated.</span></span>
* <span data-ttu-id="14f02-219">O número máximo recomendado de campos para um determinado tipo é 50.</span><span class="sxs-lookup"><span data-stu-id="14f02-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="14f02-220">Este é um limite prático de uma perspectiva de experiência de pesquisa e usabilidade.</span><span class="sxs-lookup"><span data-stu-id="14f02-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="14f02-221">Códigos de retorno</span><span class="sxs-lookup"><span data-stu-id="14f02-221">Return codes</span></span>
<span data-ttu-id="14f02-222">Olá o código de status HTTP 200 significa que essa solicitação Olá foi recebida para processamento.</span><span class="sxs-lookup"><span data-stu-id="14f02-222">hello HTTP status code 200 means that hello request has been received for processing.</span></span> <span data-ttu-id="14f02-223">Isso indica que essa operação Olá foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="14f02-223">This indicates that hello operation completed successfully.</span></span>

<span data-ttu-id="14f02-224">Esta tabela lista o conjunto completo de saudação de códigos de status que serviço Olá pode retornar:</span><span class="sxs-lookup"><span data-stu-id="14f02-224">This table lists hello complete set of status codes that hello service might return:</span></span>

| <span data-ttu-id="14f02-225">Código</span><span class="sxs-lookup"><span data-stu-id="14f02-225">Code</span></span> | <span data-ttu-id="14f02-226">Status</span><span class="sxs-lookup"><span data-stu-id="14f02-226">Status</span></span> | <span data-ttu-id="14f02-227">Código do erro</span><span class="sxs-lookup"><span data-stu-id="14f02-227">Error code</span></span> | <span data-ttu-id="14f02-228">Descrição</span><span class="sxs-lookup"><span data-stu-id="14f02-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="14f02-229">200</span><span class="sxs-lookup"><span data-stu-id="14f02-229">200</span></span> |<span data-ttu-id="14f02-230">OK</span><span class="sxs-lookup"><span data-stu-id="14f02-230">OK</span></span> | |<span data-ttu-id="14f02-231">solicitação de saudação aceita com êxito.</span><span class="sxs-lookup"><span data-stu-id="14f02-231">hello request was successfully accepted.</span></span> |
| <span data-ttu-id="14f02-232">400</span><span class="sxs-lookup"><span data-stu-id="14f02-232">400</span></span> |<span data-ttu-id="14f02-233">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="14f02-233">Bad request</span></span> |<span data-ttu-id="14f02-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="14f02-234">InactiveCustomer</span></span> |<span data-ttu-id="14f02-235">espaço de trabalho de saudação foi fechado.</span><span class="sxs-lookup"><span data-stu-id="14f02-235">hello workspace has been closed.</span></span> |
| <span data-ttu-id="14f02-236">400</span><span class="sxs-lookup"><span data-stu-id="14f02-236">400</span></span> |<span data-ttu-id="14f02-237">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="14f02-237">Bad request</span></span> |<span data-ttu-id="14f02-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="14f02-238">InvalidApiVersion</span></span> |<span data-ttu-id="14f02-239">versão de API de saudação especificado não foi reconhecido pelo serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="14f02-239">hello API version that you specified was not recognized by hello service.</span></span> |
| <span data-ttu-id="14f02-240">400</span><span class="sxs-lookup"><span data-stu-id="14f02-240">400</span></span> |<span data-ttu-id="14f02-241">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="14f02-241">Bad request</span></span> |<span data-ttu-id="14f02-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="14f02-242">InvalidCustomerId</span></span> |<span data-ttu-id="14f02-243">ID do espaço de trabalho Olá especificado é inválido.</span><span class="sxs-lookup"><span data-stu-id="14f02-243">hello workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="14f02-244">400</span><span class="sxs-lookup"><span data-stu-id="14f02-244">400</span></span> |<span data-ttu-id="14f02-245">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="14f02-245">Bad request</span></span> |<span data-ttu-id="14f02-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="14f02-246">InvalidDataFormat</span></span> |<span data-ttu-id="14f02-247">JSON inválido foi enviado.</span><span class="sxs-lookup"><span data-stu-id="14f02-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="14f02-248">corpo da resposta Olá pode conter mais informações sobre como tooresolve Olá erro.</span><span class="sxs-lookup"><span data-stu-id="14f02-248">hello response body might contain more information about how tooresolve hello error.</span></span> |
| <span data-ttu-id="14f02-249">400</span><span class="sxs-lookup"><span data-stu-id="14f02-249">400</span></span> |<span data-ttu-id="14f02-250">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="14f02-250">Bad request</span></span> |<span data-ttu-id="14f02-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="14f02-251">InvalidLogType</span></span> |<span data-ttu-id="14f02-252">tipo de log Olá especificado independentes caracteres especiais ou valores numéricos.</span><span class="sxs-lookup"><span data-stu-id="14f02-252">hello log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="14f02-253">400</span><span class="sxs-lookup"><span data-stu-id="14f02-253">400</span></span> |<span data-ttu-id="14f02-254">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="14f02-254">Bad request</span></span> |<span data-ttu-id="14f02-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="14f02-255">MissingApiVersion</span></span> |<span data-ttu-id="14f02-256">versão da API Olá não foi especificado.</span><span class="sxs-lookup"><span data-stu-id="14f02-256">hello API version wasn’t specified.</span></span> |
| <span data-ttu-id="14f02-257">400</span><span class="sxs-lookup"><span data-stu-id="14f02-257">400</span></span> |<span data-ttu-id="14f02-258">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="14f02-258">Bad request</span></span> |<span data-ttu-id="14f02-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="14f02-259">MissingContentType</span></span> |<span data-ttu-id="14f02-260">tipo de conteúdo de saudação não foi especificado.</span><span class="sxs-lookup"><span data-stu-id="14f02-260">hello content type wasn’t specified.</span></span> |
| <span data-ttu-id="14f02-261">400</span><span class="sxs-lookup"><span data-stu-id="14f02-261">400</span></span> |<span data-ttu-id="14f02-262">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="14f02-262">Bad request</span></span> |<span data-ttu-id="14f02-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="14f02-263">MissingLogType</span></span> |<span data-ttu-id="14f02-264">Olá necessário o tipo de valor de log não foi especificado.</span><span class="sxs-lookup"><span data-stu-id="14f02-264">hello required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="14f02-265">400</span><span class="sxs-lookup"><span data-stu-id="14f02-265">400</span></span> |<span data-ttu-id="14f02-266">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="14f02-266">Bad request</span></span> |<span data-ttu-id="14f02-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="14f02-267">UnsupportedContentType</span></span> |<span data-ttu-id="14f02-268">tipo de conteúdo de saudação não foi definido muito**aplicativo/json**.</span><span class="sxs-lookup"><span data-stu-id="14f02-268">hello content type was not set too**application/json**.</span></span> |
| <span data-ttu-id="14f02-269">403</span><span class="sxs-lookup"><span data-stu-id="14f02-269">403</span></span> |<span data-ttu-id="14f02-270">Proibido</span><span class="sxs-lookup"><span data-stu-id="14f02-270">Forbidden</span></span> |<span data-ttu-id="14f02-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="14f02-271">InvalidAuthorization</span></span> |<span data-ttu-id="14f02-272">solicitação de saudação tooauthenticate falha do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="14f02-272">hello service failed tooauthenticate hello request.</span></span> <span data-ttu-id="14f02-273">Verifique se essa chave de ID e a conexão de espaço de trabalho Olá são válidos.</span><span class="sxs-lookup"><span data-stu-id="14f02-273">Verify that hello workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="14f02-274">404</span><span class="sxs-lookup"><span data-stu-id="14f02-274">404</span></span> |<span data-ttu-id="14f02-275">Não encontrado</span><span class="sxs-lookup"><span data-stu-id="14f02-275">Not Found</span></span> | | <span data-ttu-id="14f02-276">Ou Olá URL fornecida está incorreta ou solicitação de saudação é muito grande.</span><span class="sxs-lookup"><span data-stu-id="14f02-276">Either hello URL provided is incorrect, or hello request is too large.</span></span> |
| <span data-ttu-id="14f02-277">429</span><span class="sxs-lookup"><span data-stu-id="14f02-277">429</span></span> |<span data-ttu-id="14f02-278">Número Excessivo de Solicitações</span><span class="sxs-lookup"><span data-stu-id="14f02-278">Too Many Requests</span></span> | | <span data-ttu-id="14f02-279">serviço de saudação está apresentando um alto volume de dados de sua conta.</span><span class="sxs-lookup"><span data-stu-id="14f02-279">hello service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="14f02-280">Tente novamente a solicitação hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="14f02-280">Please retry hello request later.</span></span> |
| <span data-ttu-id="14f02-281">500</span><span class="sxs-lookup"><span data-stu-id="14f02-281">500</span></span> |<span data-ttu-id="14f02-282">Erro interno do servidor</span><span class="sxs-lookup"><span data-stu-id="14f02-282">Internal Server Error</span></span> |<span data-ttu-id="14f02-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="14f02-283">UnspecifiedError</span></span> |<span data-ttu-id="14f02-284">serviço de saudação encontrou um erro interno.</span><span class="sxs-lookup"><span data-stu-id="14f02-284">hello service encountered an internal error.</span></span> <span data-ttu-id="14f02-285">Tente novamente a solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="14f02-285">Please retry hello request.</span></span> |
| <span data-ttu-id="14f02-286">503</span><span class="sxs-lookup"><span data-stu-id="14f02-286">503</span></span> |<span data-ttu-id="14f02-287">Serviço indisponível</span><span class="sxs-lookup"><span data-stu-id="14f02-287">Service Unavailable</span></span> |<span data-ttu-id="14f02-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="14f02-288">ServiceUnavailable</span></span> |<span data-ttu-id="14f02-289">Atualmente, o serviço de saudação é solicitações tooreceive não está disponível.</span><span class="sxs-lookup"><span data-stu-id="14f02-289">hello service currently is unavailable tooreceive requests.</span></span> <span data-ttu-id="14f02-290">Tente novamente a sua solicitação.</span><span class="sxs-lookup"><span data-stu-id="14f02-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="14f02-291">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="14f02-291">Query data</span></span>
<span data-ttu-id="14f02-292">tooquery dados enviados pelo Olá API análise de Log HTTP dados coletor, procurar registros com **tipo** que é igual toohello **LogType** valor que você especificou, concatenado com **_CL**.</span><span class="sxs-lookup"><span data-stu-id="14f02-292">tooquery data submitted by hello Log Analytics HTTP Data Collector API, search for records with **Type** that is equal toohello **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="14f02-293">Por exemplo, se você usou **MyCustomLog**, você poderia retornar todos os registros com **Type=MyCustomLog_CL**.</span><span class="sxs-lookup"><span data-stu-id="14f02-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="14f02-294">Se seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), então Olá acima consulta alteraria toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="14f02-294">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="14f02-295">Solicitações de exemplo</span><span class="sxs-lookup"><span data-stu-id="14f02-295">Sample requests</span></span>
<span data-ttu-id="14f02-296">Nas seções de Avançar hello, você encontrará exemplos de como toosubmit dados toohello API de coletor de dados de HTTP de análise de Log usando as linguagens de programação diferentes.</span><span class="sxs-lookup"><span data-stu-id="14f02-296">In hello next sections, you'll find samples of how toosubmit data toohello Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="14f02-297">Para cada exemplo, siga estas etapas tooset variáveis de saudação do cabeçalho de autorização de saudação:</span><span class="sxs-lookup"><span data-stu-id="14f02-297">For each sample, do these steps tooset hello variables for hello authorization header:</span></span>

1. <span data-ttu-id="14f02-298">No portal do Operations Management Suite hello, selecione Olá **configurações** lado a lado e, em seguida, selecione Olá **fontes conectadas** guia.</span><span class="sxs-lookup"><span data-stu-id="14f02-298">In hello Operations Management Suite portal, select hello **Settings** tile, and then select hello **Connected Sources** tab.</span></span>
2. <span data-ttu-id="14f02-299">toohello à direita do **ID do espaço de trabalho**, selecione o ícone para copiar Olá e, em seguida, cole a ID de hello como valor de saudação do hello **Customer ID** variável.</span><span class="sxs-lookup"><span data-stu-id="14f02-299">toohello right of **Workspace ID**, select hello copy icon, and then paste hello ID as hello value of hello **Customer ID** variable.</span></span>
3. <span data-ttu-id="14f02-300">toohello à direita do **chave primária**, selecione o ícone para copiar Olá e, em seguida, cole a ID de hello como valor de saudação do hello **chave compartilhada** variável.</span><span class="sxs-lookup"><span data-stu-id="14f02-300">toohello right of **Primary Key**, select hello copy icon, and then paste hello ID as hello value of hello **Shared Key** variable.</span></span>

<span data-ttu-id="14f02-301">Como alternativa, você pode alterar variáveis Olá Olá tipo de log e dados JSON.</span><span class="sxs-lookup"><span data-stu-id="14f02-301">Alternatively, you can change hello variables for hello log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="14f02-302">Exemplo do PowerShell</span><span class="sxs-lookup"><span data-stu-id="14f02-302">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify hello name of hello record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with hello created time for hello records
$TimeStampField = "DateValue"


# Create two records with hello same set of properties toocreate
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create hello function toocreate hello authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create hello function toocreate and post hello request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit hello data toohello API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="14f02-303">Exemplo de C#</span><span class="sxs-lookup"><span data-stu-id="14f02-303">C# sample</span></span>
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId tooyour Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either hello primary or hello secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of hello event type that is being submitted tooLog Analytics
        static string LogName = "DemoExample";

        // You can use an optional field toospecify hello timestamp from hello data. If hello time field is not specified, Log Analytics assumes hello time is hello message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for hello API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build hello API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request toohello POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            {
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";

                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);

                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);

                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a><span data-ttu-id="14f02-304">Exemplo de Python</span><span class="sxs-lookup"><span data-stu-id="14f02-304">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update hello customer ID tooyour Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For hello shared key, use either hello primary or hello secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# hello log type is hello name of hello event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build hello API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request toohello POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a><span data-ttu-id="14f02-305">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="14f02-305">Next steps</span></span>
- <span data-ttu-id="14f02-306">Saudação de uso [API de pesquisa de Log](log-analytics-log-search-api.md) tooretrieve dados do repositório de análise de Log de saudação.</span><span class="sxs-lookup"><span data-stu-id="14f02-306">Use hello [Log Search API](log-analytics-log-search-api.md) tooretrieve data from hello Log Analytics repository.</span></span>
