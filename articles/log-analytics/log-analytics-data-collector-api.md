---
title: API do coletor de dados HTTP do Log Analytics | Microsoft Docs
description: "Você pode usar a API do coletor de dados HTTP do Log Analytics para adicionar dados JSON de POST ao repositório do Log Analytics de qualquer cliente que possa chamar a API REST. Este artigo descreve como usar a API e tem exemplos de como publicar dados usando diferentes linguagens de programação."
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
ms.openlocfilehash: b0c45ff8c1d4c9d35fbb3c8839b38a20df277055
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="send-data-to-log-analytics-with-the-http-data-collector-api"></a><span data-ttu-id="143cf-104">Enviar dados ao Log Analytics com a API do Coletor de dados HTTP</span><span class="sxs-lookup"><span data-stu-id="143cf-104">Send data to Log Analytics with the HTTP Data Collector API</span></span>
<span data-ttu-id="143cf-105">Este artigo mostra como usar a API do Coletor de Dados HTTP para enviar dados ao Log Analytics de um cliente da API REST.</span><span class="sxs-lookup"><span data-stu-id="143cf-105">This article shows you how to use the HTTP Data Collector API to send data to Log Analytics from a REST API client.</span></span>  <span data-ttu-id="143cf-106">Ele descreve como formatar dados coletados pelo seu script ou aplicativo, incluí-los em uma solicitação e ter essa solicitação autorizada pelo Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="143cf-106">It describes how to format data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="143cf-107">Os exemplos são fornecidos para PowerShell, C# e Python.</span><span class="sxs-lookup"><span data-stu-id="143cf-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="143cf-108">Conceitos</span><span class="sxs-lookup"><span data-stu-id="143cf-108">Concepts</span></span>
<span data-ttu-id="143cf-109">Você pode usar a API do Coletor de Dados HTTP para enviar dados ao Log Analytics de qualquer cliente que possa chamar uma API REST.</span><span class="sxs-lookup"><span data-stu-id="143cf-109">You can use the HTTP Data Collector API to send data to Log Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="143cf-110">Ela pode ser um runbook na Automação do Azure, que coleta dados de gerenciamento do Azure ou de outra nuvem, ou pode ser um sistema de gerenciamento alternativo que usa o Log Analytics para consolidar e analisar dados.</span><span class="sxs-lookup"><span data-stu-id="143cf-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics to consolidate and analyze data.</span></span>

<span data-ttu-id="143cf-111">Todos os dados no repositório do Log Analytics são armazenados como um registro com um tipo de registro específico.</span><span class="sxs-lookup"><span data-stu-id="143cf-111">All data in the Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="143cf-112">Formate seus dados para enviar à API do Coletor de Dados HTTP como vários registros em JSON.</span><span class="sxs-lookup"><span data-stu-id="143cf-112">You format your data to send to the HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="143cf-113">Quando você envia os dados, um registro individual é criado no repositório de cada registro no conteúdo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="143cf-113">When you submit the data, an individual record is created in the repository for each record in the request payload.</span></span>


![Visão geral do Coletor de Dados HTTP](media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="143cf-115">Criar uma solicitação</span><span class="sxs-lookup"><span data-stu-id="143cf-115">Create a request</span></span>
<span data-ttu-id="143cf-116">Para usar a API do Coletor de Dados HTTP, crie uma solicitação POST que inclua os dados a serem enviados em JSON (JavaScript Object Notation).</span><span class="sxs-lookup"><span data-stu-id="143cf-116">To use the HTTP Data Collector API, you create a POST request that includes the data to send in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="143cf-117">As próximas três tabelas listam os atributos que são necessários para cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="143cf-117">The next three tables list the attributes that are required for each request.</span></span> <span data-ttu-id="143cf-118">Descrevemos cada atributo em mais detalhes posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="143cf-118">We describe each attribute in more detail later in the article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="143cf-119">URI da solicitação</span><span class="sxs-lookup"><span data-stu-id="143cf-119">Request URI</span></span>
| <span data-ttu-id="143cf-120">Atributo</span><span class="sxs-lookup"><span data-stu-id="143cf-120">Attribute</span></span> | <span data-ttu-id="143cf-121">Propriedade</span><span class="sxs-lookup"><span data-stu-id="143cf-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="143cf-122">Método</span><span class="sxs-lookup"><span data-stu-id="143cf-122">Method</span></span> |<span data-ttu-id="143cf-123">POST</span><span class="sxs-lookup"><span data-stu-id="143cf-123">POST</span></span> |
| <span data-ttu-id="143cf-124">URI</span><span class="sxs-lookup"><span data-stu-id="143cf-124">URI</span></span> |<span data-ttu-id="143cf-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="143cf-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="143cf-126">Tipo de conteúdo</span><span class="sxs-lookup"><span data-stu-id="143cf-126">Content type</span></span> |<span data-ttu-id="143cf-127">aplicativo/json</span><span class="sxs-lookup"><span data-stu-id="143cf-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="143cf-128">Solicitar parâmetros de URI (Uniform Resource Identifier)</span><span class="sxs-lookup"><span data-stu-id="143cf-128">Request URI parameters</span></span>
| <span data-ttu-id="143cf-129">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="143cf-129">Parameter</span></span> | <span data-ttu-id="143cf-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="143cf-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="143cf-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="143cf-131">CustomerID</span></span> |<span data-ttu-id="143cf-132">O identificador exclusivo para o espaço de trabalho do Microsoft Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="143cf-132">The unique identifier for the Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="143cf-133">Recurso</span><span class="sxs-lookup"><span data-stu-id="143cf-133">Resource</span></span> |<span data-ttu-id="143cf-134">O nome do recurso de API: /api/logs.</span><span class="sxs-lookup"><span data-stu-id="143cf-134">The API resource name: /api/logs.</span></span> |
| <span data-ttu-id="143cf-135">Versão da API</span><span class="sxs-lookup"><span data-stu-id="143cf-135">API Version</span></span> |<span data-ttu-id="143cf-136">A versão da API a ser usada com esta solicitação.</span><span class="sxs-lookup"><span data-stu-id="143cf-136">The version of the API to use with this request.</span></span> <span data-ttu-id="143cf-137">Atualmente, ela é 2016-04-01.</span><span class="sxs-lookup"><span data-stu-id="143cf-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="143cf-138">Cabeçalhos da solicitação</span><span class="sxs-lookup"><span data-stu-id="143cf-138">Request headers</span></span>
| <span data-ttu-id="143cf-139">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="143cf-139">Header</span></span> | <span data-ttu-id="143cf-140">Descrição</span><span class="sxs-lookup"><span data-stu-id="143cf-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="143cf-141">Autorização</span><span class="sxs-lookup"><span data-stu-id="143cf-141">Authorization</span></span> |<span data-ttu-id="143cf-142">A assinatura de autorização.</span><span class="sxs-lookup"><span data-stu-id="143cf-142">The authorization signature.</span></span> <span data-ttu-id="143cf-143">Posteriormente neste artigo, você pode ler sobre como criar um cabeçalho HMAC-SHA256.</span><span class="sxs-lookup"><span data-stu-id="143cf-143">Later in the article, you can read about how to create an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="143cf-144">Log-Type</span><span class="sxs-lookup"><span data-stu-id="143cf-144">Log-Type</span></span> |<span data-ttu-id="143cf-145">Especifique o tipo de registro dos dados que estão sendo enviados.</span><span class="sxs-lookup"><span data-stu-id="143cf-145">Specify the record type of the data that is being submitted.</span></span> <span data-ttu-id="143cf-146">Atualmente, o tipo de log dá suporte apenas a caracteres alfa.</span><span class="sxs-lookup"><span data-stu-id="143cf-146">Currently, the log type supports only alpha characters.</span></span> <span data-ttu-id="143cf-147">Ele não dá suporte a caracteres alfanuméricos ou caracteres especiais.</span><span class="sxs-lookup"><span data-stu-id="143cf-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="143cf-148">x-ms-date</span><span class="sxs-lookup"><span data-stu-id="143cf-148">x-ms-date</span></span> |<span data-ttu-id="143cf-149">A data em que a solicitação foi processada, no formato RFC 1123.</span><span class="sxs-lookup"><span data-stu-id="143cf-149">The date that the request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="143cf-150">time-generated-field</span><span class="sxs-lookup"><span data-stu-id="143cf-150">time-generated-field</span></span> |<span data-ttu-id="143cf-151">O nome de um campo nos dados que contém o carimbo de data/hora do item de dados.</span><span class="sxs-lookup"><span data-stu-id="143cf-151">The name of a field in the data that contains the timestamp of the data item.</span></span> <span data-ttu-id="143cf-152">Se você especificar um campo, seu conteúdo será usado para **TimeGenerated**.</span><span class="sxs-lookup"><span data-stu-id="143cf-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="143cf-153">Se esse campo não for especificado, o padrão para **TimeGenerated** será a hora em que a mensagem é incluída.</span><span class="sxs-lookup"><span data-stu-id="143cf-153">If this field isn’t specified, the default for **TimeGenerated** is the time that the message is ingested.</span></span> <span data-ttu-id="143cf-154">O conteúdo do campo de mensagem deve seguir o formato ISO 8601 AAAA-MM-DDThh:mm:ssZ.</span><span class="sxs-lookup"><span data-stu-id="143cf-154">The contents of the message field should follow the ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="143cf-155">Autorização</span><span class="sxs-lookup"><span data-stu-id="143cf-155">Authorization</span></span>
<span data-ttu-id="143cf-156">Todas as solicitações para a API do coletor de dados HTTP do Log Analytics devem incluir um cabeçalho de autorização.</span><span class="sxs-lookup"><span data-stu-id="143cf-156">Any request to the Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="143cf-157">Para autenticar uma solicitação, você deve assinar a solicitação com a chave primária ou secundária para o espaço de trabalho que está fazendo a solicitação.</span><span class="sxs-lookup"><span data-stu-id="143cf-157">To authenticate a request, you must sign the request with either the primary or the secondary key for the workspace that is making the request.</span></span> <span data-ttu-id="143cf-158">Em seguida, passe essa assinatura como parte da solicitação.</span><span class="sxs-lookup"><span data-stu-id="143cf-158">Then, pass that signature as part of the request.</span></span>   

<span data-ttu-id="143cf-159">Aqui está o formato do cabeçalho de autorização:</span><span class="sxs-lookup"><span data-stu-id="143cf-159">Here's the format for the authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="143cf-160">*WorkspaceID* é o identificador exclusivo para o espaço de trabalho do Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="143cf-160">*WorkspaceID* is the unique identifier for the Operations Management Suite workspace.</span></span> <span data-ttu-id="143cf-161">*Signature* é um [HMAC (Código de Autenticação de Mensagem Baseado em Hash)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) que é construído a partir da solicitação e, em seguida, calculado usando o [algoritmo SHA256](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span><span class="sxs-lookup"><span data-stu-id="143cf-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from the request and then computed by using the [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="143cf-162">Em seguida, você o codifica usando a codificação Base64.</span><span class="sxs-lookup"><span data-stu-id="143cf-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="143cf-163">Use este formato para codificar a cadeia de caracteres de assinatura **SharedKey**:</span><span class="sxs-lookup"><span data-stu-id="143cf-163">Use this format to encode the **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="143cf-164">Aqui está um exemplo de uma cadeia de caracteres de assinatura:</span><span class="sxs-lookup"><span data-stu-id="143cf-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="143cf-165">Quando você tiver a cadeia de caracteres de assinatura, codifique-a usando o algoritmo HMAC-SHA256 na sequência de caracteres codificada em UTF-8 e codifique o resultado em Base64.</span><span class="sxs-lookup"><span data-stu-id="143cf-165">When you have the signature string, encode it by using the HMAC-SHA256 algorithm on the UTF-8-encoded string, and then encode the result as Base64.</span></span> <span data-ttu-id="143cf-166">Use este formato:</span><span class="sxs-lookup"><span data-stu-id="143cf-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="143cf-167">Os exemplos nas seções a seguir têm o código de exemplo para ajudá-lo a criar um cabeçalho de autorização.</span><span class="sxs-lookup"><span data-stu-id="143cf-167">The samples in the next sections have sample code to help you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="143cf-168">Corpo da solicitação</span><span class="sxs-lookup"><span data-stu-id="143cf-168">Request body</span></span>
<span data-ttu-id="143cf-169">O corpo da mensagem deve ser em JSON.</span><span class="sxs-lookup"><span data-stu-id="143cf-169">The body of the message must be in JSON.</span></span> <span data-ttu-id="143cf-170">Ele deve incluir um ou mais registros com os pares de nome e valor de propriedade neste formato:</span><span class="sxs-lookup"><span data-stu-id="143cf-170">It must include one or more records with the property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="143cf-171">Você pode criar lotes de vários registros em uma única solicitação usando o formato a seguir.</span><span class="sxs-lookup"><span data-stu-id="143cf-171">You can batch multiple records together in a single request by using the following format.</span></span> <span data-ttu-id="143cf-172">Todos os registros devem ser do mesmo tipo de registro.</span><span class="sxs-lookup"><span data-stu-id="143cf-172">All the records must be the same record type.</span></span>

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

## <a name="record-type-and-properties"></a><span data-ttu-id="143cf-173">Propriedades e o tipo de registro</span><span class="sxs-lookup"><span data-stu-id="143cf-173">Record type and properties</span></span>
<span data-ttu-id="143cf-174">Você define um tipo de registro personalizado ao enviar dados por meio da API do coletor de dados HTTP do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="143cf-174">You define a custom record type when you submit data through the Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="143cf-175">No momento, você não pode gravar dados em tipos de registro existentes que foram criados por outras soluções e tipos de dados.</span><span class="sxs-lookup"><span data-stu-id="143cf-175">Currently, you can't write data to existing record types that were created by other data types and solutions.</span></span> <span data-ttu-id="143cf-176">O Log Analytics lê os dados de entrada e, em seguida, cria propriedades que correspondem aos tipos de dados dos valores que você inseriu.</span><span class="sxs-lookup"><span data-stu-id="143cf-176">Log Analytics reads the incoming data and then creates properties that match the data types of the values that you enter.</span></span>

<span data-ttu-id="143cf-177">Cada solicitação para a API do Log Analytics deve incluir um cabeçalho **Log-Type** com o nome do tipo de registro.</span><span class="sxs-lookup"><span data-stu-id="143cf-177">Each request to the Log Analytics API must include a **Log-Type** header with the name for the record type.</span></span> <span data-ttu-id="143cf-178">O sufixo **_CL** é acrescentado automaticamente ao nome inserido para distingui-lo de outros tipos de log como um log personalizado.</span><span class="sxs-lookup"><span data-stu-id="143cf-178">The suffix **_CL** is automatically appended to the name you enter to distinguish it from other log types as a custom log.</span></span> <span data-ttu-id="143cf-179">Por exemplo, se você inserir o nome **MyNewRecordType**, o Log Analytics criará um registro com o tipo **MyNewRecordType_CL**.</span><span class="sxs-lookup"><span data-stu-id="143cf-179">For example, if you enter the name **MyNewRecordType**, Log Analytics creates a record with the type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="143cf-180">Isso ajuda a garantir que não haja nenhum conflito entre os nomes de tipo criados pelo usuário e aqueles fornecidos nas soluções atuais ou futuras da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="143cf-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="143cf-181">Para identificar o tipo de dados de uma propriedade, o Log Analytics adiciona um sufixo ao nome da propriedade.</span><span class="sxs-lookup"><span data-stu-id="143cf-181">To identify a property's data type, Log Analytics adds a suffix to the property name.</span></span> <span data-ttu-id="143cf-182">Se uma propriedade contiver um valor nulo, ela não será incluída no registro.</span><span class="sxs-lookup"><span data-stu-id="143cf-182">If a property contains a null value, the property is not included in that record.</span></span> <span data-ttu-id="143cf-183">Esta tabela lista o tipo de dados de propriedade e o sufixo correspondente:</span><span class="sxs-lookup"><span data-stu-id="143cf-183">This table lists the property data type and corresponding suffix:</span></span>

| <span data-ttu-id="143cf-184">Tipo de dados de propriedade</span><span class="sxs-lookup"><span data-stu-id="143cf-184">Property data type</span></span> | <span data-ttu-id="143cf-185">Suffix</span><span class="sxs-lookup"><span data-stu-id="143cf-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="143cf-186">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="143cf-186">String</span></span> |<span data-ttu-id="143cf-187">_s</span><span class="sxs-lookup"><span data-stu-id="143cf-187">_s</span></span> |
| <span data-ttu-id="143cf-188">Booliano</span><span class="sxs-lookup"><span data-stu-id="143cf-188">Boolean</span></span> |<span data-ttu-id="143cf-189">_b</span><span class="sxs-lookup"><span data-stu-id="143cf-189">_b</span></span> |
| <span data-ttu-id="143cf-190">Duplo</span><span class="sxs-lookup"><span data-stu-id="143cf-190">Double</span></span> |<span data-ttu-id="143cf-191">_d</span><span class="sxs-lookup"><span data-stu-id="143cf-191">_d</span></span> |
| <span data-ttu-id="143cf-192">Data/hora</span><span class="sxs-lookup"><span data-stu-id="143cf-192">Date/time</span></span> |<span data-ttu-id="143cf-193">_t</span><span class="sxs-lookup"><span data-stu-id="143cf-193">_t</span></span> |
| <span data-ttu-id="143cf-194">GUID</span><span class="sxs-lookup"><span data-stu-id="143cf-194">GUID</span></span> |<span data-ttu-id="143cf-195">_g</span><span class="sxs-lookup"><span data-stu-id="143cf-195">_g</span></span> |

<span data-ttu-id="143cf-196">O tipo de dados que o Log Analytics usa para cada propriedade depende de se o tipo de registro do novo registro já existe.</span><span class="sxs-lookup"><span data-stu-id="143cf-196">The data type that Log Analytics uses for each property depends on whether the record type for the new record already exists.</span></span>

* <span data-ttu-id="143cf-197">Se o tipo de registro não existir, o Log Analytics cria um novo.</span><span class="sxs-lookup"><span data-stu-id="143cf-197">If the record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="143cf-198">O Log Analytics usa a interferência de tipo JSON para determinar o tipo de dados de cada propriedade para o novo registro.</span><span class="sxs-lookup"><span data-stu-id="143cf-198">Log Analytics uses the JSON type inference to determine the data type for each property for the new record.</span></span>
* <span data-ttu-id="143cf-199">Se o tipo de registro existir, o Log Analytics tenta criar um novo registro com base nas propriedades existentes.</span><span class="sxs-lookup"><span data-stu-id="143cf-199">If the record type does exist, Log Analytics attempts to create a new record based on existing properties.</span></span> <span data-ttu-id="143cf-200">Se o tipo de dados de uma propriedade no novo registro não corresponder e não puder ser convertida para o tipo existente, ou se o registro incluir uma propriedade que não existe, o Log Analytics criará uma nova propriedade que tenha o sufixo relevante.</span><span class="sxs-lookup"><span data-stu-id="143cf-200">If the data type for a property in the new record doesn’t match and can’t be converted to the existing type, or if the record includes a property that doesn’t exist, Log Analytics creates a new property that has the relevant suffix.</span></span>

<span data-ttu-id="143cf-201">Por exemplo, esta entrada de envio criaria um registro com três propriedades, **number_d**, **boolean_b** e **string_s**:</span><span class="sxs-lookup"><span data-stu-id="143cf-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![Registro de exemplo 1](media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="143cf-203">Se você enviasse essa próxima entrada, com todos os valores formatados como cadeias de caracteres, as propriedades não seriam alteradas.</span><span class="sxs-lookup"><span data-stu-id="143cf-203">If you then submitted this next entry, with all values formatted as strings, the properties would not change.</span></span> <span data-ttu-id="143cf-204">Esses valores podem ser convertidos para tipos de dados existentes:</span><span class="sxs-lookup"><span data-stu-id="143cf-204">These values can be converted to existing data types:</span></span>

![Registro de exemplo 2](media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="143cf-206">Mas, se você fizesse esse próximo envio, o Log Analytics criaria as novas propriedades **boolean_d** e **string_d**.</span><span class="sxs-lookup"><span data-stu-id="143cf-206">But, if you then made this next submission, Log Analytics would create the new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="143cf-207">Esses valores não podem ser convertidos:</span><span class="sxs-lookup"><span data-stu-id="143cf-207">These values can't be converted:</span></span>

![Registro de exemplo 3](media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="143cf-209">Se você enviasse a entrada a seguir, antes de o tipo de registro ter sido criado, o Log Analytics criaria um registro com três propriedades, **number_s**, **boolean_s** e **string_s**.</span><span class="sxs-lookup"><span data-stu-id="143cf-209">If you then submitted the following entry, before the record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="143cf-210">Nesta entrada, cada um dos valores iniciais é formatado como uma cadeia de caracteres:</span><span class="sxs-lookup"><span data-stu-id="143cf-210">In this entry, each of the initial values is formatted as a string:</span></span>

![Registro de exemplo 4](media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="143cf-212">Limites de dados</span><span class="sxs-lookup"><span data-stu-id="143cf-212">Data limits</span></span>
<span data-ttu-id="143cf-213">Há algumas restrições sobre os dados publicados na API de coleta de dados do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="143cf-213">There are some constraints around the data posted to the Log Analytics Data collection API.</span></span>

* <span data-ttu-id="143cf-214">Máximo de 30 MB por post na API do coletor de dados do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="143cf-214">Maximum of 30 MB per post to Log Analytics Data Collector API.</span></span> <span data-ttu-id="143cf-215">Este é um limite de tamanho para um único post.</span><span class="sxs-lookup"><span data-stu-id="143cf-215">This is a size limit for a single post.</span></span> <span data-ttu-id="143cf-216">Se os dados de uma única postagem excederem 30 MB, será necessário dividi-los em partes menores e enviá-los simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="143cf-216">If the data from a single post that exceeds 30 MB, you should split the data up to smaller sized chunks and send them concurrently.</span></span>
* <span data-ttu-id="143cf-217">Limite máximo de 32 KB para valores de campo.</span><span class="sxs-lookup"><span data-stu-id="143cf-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="143cf-218">Se o valor do campo for maior do que 32 KB, os dados serão truncados.</span><span class="sxs-lookup"><span data-stu-id="143cf-218">If the field value is greater than 32 KB, the data will be truncated.</span></span>
* <span data-ttu-id="143cf-219">O número máximo recomendado de campos para um determinado tipo é 50.</span><span class="sxs-lookup"><span data-stu-id="143cf-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="143cf-220">Este é um limite prático de uma perspectiva de experiência de pesquisa e usabilidade.</span><span class="sxs-lookup"><span data-stu-id="143cf-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="143cf-221">Códigos de retorno</span><span class="sxs-lookup"><span data-stu-id="143cf-221">Return codes</span></span>
<span data-ttu-id="143cf-222">O código de status HTTP 200 significa que a solicitação foi recebida para processamento.</span><span class="sxs-lookup"><span data-stu-id="143cf-222">The HTTP status code 200 means that the request has been received for processing.</span></span> <span data-ttu-id="143cf-223">Isso indica que a operação foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="143cf-223">This indicates that the operation completed successfully.</span></span>

<span data-ttu-id="143cf-224">Esta tabela lista o conjunto completo de códigos de status que o serviço pode retornar:</span><span class="sxs-lookup"><span data-stu-id="143cf-224">This table lists the complete set of status codes that the service might return:</span></span>

| <span data-ttu-id="143cf-225">Código</span><span class="sxs-lookup"><span data-stu-id="143cf-225">Code</span></span> | <span data-ttu-id="143cf-226">Status</span><span class="sxs-lookup"><span data-stu-id="143cf-226">Status</span></span> | <span data-ttu-id="143cf-227">Código do erro</span><span class="sxs-lookup"><span data-stu-id="143cf-227">Error code</span></span> | <span data-ttu-id="143cf-228">Descrição</span><span class="sxs-lookup"><span data-stu-id="143cf-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="143cf-229">200</span><span class="sxs-lookup"><span data-stu-id="143cf-229">200</span></span> |<span data-ttu-id="143cf-230">OK</span><span class="sxs-lookup"><span data-stu-id="143cf-230">OK</span></span> | |<span data-ttu-id="143cf-231">A solicitação foi aceita com êxito.</span><span class="sxs-lookup"><span data-stu-id="143cf-231">The request was successfully accepted.</span></span> |
| <span data-ttu-id="143cf-232">400</span><span class="sxs-lookup"><span data-stu-id="143cf-232">400</span></span> |<span data-ttu-id="143cf-233">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="143cf-233">Bad request</span></span> |<span data-ttu-id="143cf-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="143cf-234">InactiveCustomer</span></span> |<span data-ttu-id="143cf-235">O espaço de trabalho foi fechado.</span><span class="sxs-lookup"><span data-stu-id="143cf-235">The workspace has been closed.</span></span> |
| <span data-ttu-id="143cf-236">400</span><span class="sxs-lookup"><span data-stu-id="143cf-236">400</span></span> |<span data-ttu-id="143cf-237">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="143cf-237">Bad request</span></span> |<span data-ttu-id="143cf-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="143cf-238">InvalidApiVersion</span></span> |<span data-ttu-id="143cf-239">A versão da API que você especificou não foi reconhecida pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="143cf-239">The API version that you specified was not recognized by the service.</span></span> |
| <span data-ttu-id="143cf-240">400</span><span class="sxs-lookup"><span data-stu-id="143cf-240">400</span></span> |<span data-ttu-id="143cf-241">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="143cf-241">Bad request</span></span> |<span data-ttu-id="143cf-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="143cf-242">InvalidCustomerId</span></span> |<span data-ttu-id="143cf-243">A ID do espaço de trabalho especificada é inválida.</span><span class="sxs-lookup"><span data-stu-id="143cf-243">The workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="143cf-244">400</span><span class="sxs-lookup"><span data-stu-id="143cf-244">400</span></span> |<span data-ttu-id="143cf-245">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="143cf-245">Bad request</span></span> |<span data-ttu-id="143cf-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="143cf-246">InvalidDataFormat</span></span> |<span data-ttu-id="143cf-247">JSON inválido foi enviado.</span><span class="sxs-lookup"><span data-stu-id="143cf-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="143cf-248">O corpo da resposta pode conter mais informações sobre como resolver o erro.</span><span class="sxs-lookup"><span data-stu-id="143cf-248">The response body might contain more information about how to resolve the error.</span></span> |
| <span data-ttu-id="143cf-249">400</span><span class="sxs-lookup"><span data-stu-id="143cf-249">400</span></span> |<span data-ttu-id="143cf-250">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="143cf-250">Bad request</span></span> |<span data-ttu-id="143cf-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="143cf-251">InvalidLogType</span></span> |<span data-ttu-id="143cf-252">O tipo de log especificado continha caracteres especiais ou numéricos.</span><span class="sxs-lookup"><span data-stu-id="143cf-252">The log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="143cf-253">400</span><span class="sxs-lookup"><span data-stu-id="143cf-253">400</span></span> |<span data-ttu-id="143cf-254">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="143cf-254">Bad request</span></span> |<span data-ttu-id="143cf-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="143cf-255">MissingApiVersion</span></span> |<span data-ttu-id="143cf-256">A versão da API não foi especificada.</span><span class="sxs-lookup"><span data-stu-id="143cf-256">The API version wasn’t specified.</span></span> |
| <span data-ttu-id="143cf-257">400</span><span class="sxs-lookup"><span data-stu-id="143cf-257">400</span></span> |<span data-ttu-id="143cf-258">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="143cf-258">Bad request</span></span> |<span data-ttu-id="143cf-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="143cf-259">MissingContentType</span></span> |<span data-ttu-id="143cf-260">O tipo de conteúdo não foi especificado.</span><span class="sxs-lookup"><span data-stu-id="143cf-260">The content type wasn’t specified.</span></span> |
| <span data-ttu-id="143cf-261">400</span><span class="sxs-lookup"><span data-stu-id="143cf-261">400</span></span> |<span data-ttu-id="143cf-262">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="143cf-262">Bad request</span></span> |<span data-ttu-id="143cf-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="143cf-263">MissingLogType</span></span> |<span data-ttu-id="143cf-264">O tipo de log de valor necessário não foi especificado.</span><span class="sxs-lookup"><span data-stu-id="143cf-264">The required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="143cf-265">400</span><span class="sxs-lookup"><span data-stu-id="143cf-265">400</span></span> |<span data-ttu-id="143cf-266">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="143cf-266">Bad request</span></span> |<span data-ttu-id="143cf-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="143cf-267">UnsupportedContentType</span></span> |<span data-ttu-id="143cf-268">O tipo de conteúdo não foi definido como **application/json**.</span><span class="sxs-lookup"><span data-stu-id="143cf-268">The content type was not set to **application/json**.</span></span> |
| <span data-ttu-id="143cf-269">403</span><span class="sxs-lookup"><span data-stu-id="143cf-269">403</span></span> |<span data-ttu-id="143cf-270">Proibido</span><span class="sxs-lookup"><span data-stu-id="143cf-270">Forbidden</span></span> |<span data-ttu-id="143cf-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="143cf-271">InvalidAuthorization</span></span> |<span data-ttu-id="143cf-272">O serviço falhou ao autenticar a solicitação.</span><span class="sxs-lookup"><span data-stu-id="143cf-272">The service failed to authenticate the request.</span></span> <span data-ttu-id="143cf-273">Verifique se a chave de conexão e a ID do espaço de trabalho são válidos.</span><span class="sxs-lookup"><span data-stu-id="143cf-273">Verify that the workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="143cf-274">404</span><span class="sxs-lookup"><span data-stu-id="143cf-274">404</span></span> |<span data-ttu-id="143cf-275">Não encontrado</span><span class="sxs-lookup"><span data-stu-id="143cf-275">Not Found</span></span> | | <span data-ttu-id="143cf-276">A URL fornecida está incorreta ou a solicitação é muito grande.</span><span class="sxs-lookup"><span data-stu-id="143cf-276">Either the URL provided is incorrect, or the request is too large.</span></span> |
| <span data-ttu-id="143cf-277">429</span><span class="sxs-lookup"><span data-stu-id="143cf-277">429</span></span> |<span data-ttu-id="143cf-278">Número Excessivo de Solicitações</span><span class="sxs-lookup"><span data-stu-id="143cf-278">Too Many Requests</span></span> | | <span data-ttu-id="143cf-279">O serviço está recebendo um alto volume de dados da sua conta.</span><span class="sxs-lookup"><span data-stu-id="143cf-279">The service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="143cf-280">Tente fazer novamente a solicitação.</span><span class="sxs-lookup"><span data-stu-id="143cf-280">Please retry the request later.</span></span> |
| <span data-ttu-id="143cf-281">500</span><span class="sxs-lookup"><span data-stu-id="143cf-281">500</span></span> |<span data-ttu-id="143cf-282">Erro interno do servidor</span><span class="sxs-lookup"><span data-stu-id="143cf-282">Internal Server Error</span></span> |<span data-ttu-id="143cf-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="143cf-283">UnspecifiedError</span></span> |<span data-ttu-id="143cf-284">O serviço encontrou um erro interno.</span><span class="sxs-lookup"><span data-stu-id="143cf-284">The service encountered an internal error.</span></span> <span data-ttu-id="143cf-285">Tente novamente a solicitação.</span><span class="sxs-lookup"><span data-stu-id="143cf-285">Please retry the request.</span></span> |
| <span data-ttu-id="143cf-286">503</span><span class="sxs-lookup"><span data-stu-id="143cf-286">503</span></span> |<span data-ttu-id="143cf-287">Serviço indisponível</span><span class="sxs-lookup"><span data-stu-id="143cf-287">Service Unavailable</span></span> |<span data-ttu-id="143cf-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="143cf-288">ServiceUnavailable</span></span> |<span data-ttu-id="143cf-289">No momento, o serviço está indisponível para receber solicitações.</span><span class="sxs-lookup"><span data-stu-id="143cf-289">The service currently is unavailable to receive requests.</span></span> <span data-ttu-id="143cf-290">Tente novamente a sua solicitação.</span><span class="sxs-lookup"><span data-stu-id="143cf-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="143cf-291">Consultar dados</span><span class="sxs-lookup"><span data-stu-id="143cf-291">Query data</span></span>
<span data-ttu-id="143cf-292">Para consultar os dados enviados pela API do coletor de dados HTTP do Log Analytics, procure registros com **Tipo** que é igual ao valor **LogType** valor que você especificou, acrescido com **_CL**.</span><span class="sxs-lookup"><span data-stu-id="143cf-292">To query data submitted by the Log Analytics HTTP Data Collector API, search for records with **Type** that is equal to the **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="143cf-293">Por exemplo, se você usou **MyCustomLog**, você poderia retornar todos os registros com **Type=MyCustomLog_CL**.</span><span class="sxs-lookup"><span data-stu-id="143cf-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

>[!NOTE]
> <span data-ttu-id="143cf-294">Se o seu espaço de trabalho fosse atualizado para a [nova linguagem de consulta do Log Analytics](log-analytics-log-search-upgrade.md), a consulta acima seria alterada para o demonstrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="143cf-294">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>

> `MyCustomLog_CL`

## <a name="sample-requests"></a><span data-ttu-id="143cf-295">Solicitações de exemplo</span><span class="sxs-lookup"><span data-stu-id="143cf-295">Sample requests</span></span>
<span data-ttu-id="143cf-296">Nas seções a seguir, você encontrará exemplos de como enviar dados para a AAPI do coletor de dados HTTP do Log Analytics usando diferentes linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="143cf-296">In the next sections, you'll find samples of how to submit data to the Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="143cf-297">Para cada exemplo, realize essas etapas para definir as variáveis para o cabeçalho de autorização:</span><span class="sxs-lookup"><span data-stu-id="143cf-297">For each sample, do these steps to set the variables for the authorization header:</span></span>

1. <span data-ttu-id="143cf-298">No portal do Operations Management Suite, selecione o bloco **Configurações** e, em seguida, selecione a guia **Fontes Conectadas**.</span><span class="sxs-lookup"><span data-stu-id="143cf-298">In the Operations Management Suite portal, select the **Settings** tile, and then select the **Connected Sources** tab.</span></span>
2. <span data-ttu-id="143cf-299">À direita da **ID do Espaço de Trabalho**, selecione o ícone de cópia e cole a ID como o valor da variável **Customer ID**.</span><span class="sxs-lookup"><span data-stu-id="143cf-299">To the right of **Workspace ID**, select the copy icon, and then paste the ID as the value of the **Customer ID** variable.</span></span>
3. <span data-ttu-id="143cf-300">À direita da **Chave Primária**, selecione o ícone de cópia e cole a ID como o valor da variável **Shared Key**.</span><span class="sxs-lookup"><span data-stu-id="143cf-300">To the right of **Primary Key**, select the copy icon, and then paste the ID as the value of the **Shared Key** variable.</span></span>

<span data-ttu-id="143cf-301">Como alternativa, você pode alterar as variáveis para o tipo de log e dados JSON.</span><span class="sxs-lookup"><span data-stu-id="143cf-301">Alternatively, you can change the variables for the log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="143cf-302">Exemplo do PowerShell</span><span class="sxs-lookup"><span data-stu-id="143cf-302">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify the name of the record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with the created time for the records
$TimeStampField = "DateValue"


# Create two records with the same set of properties to create
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

# Create the function to create the authorization signature
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


# Create the function to create and post the request
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

# Submit the data to the API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="143cf-303">Exemplo de C#</span><span class="sxs-lookup"><span data-stu-id="143cf-303">C# sample</span></span>
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

        // Update customerId to your Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either the primary or the secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of the event type that is being submitted to Log Analytics
        static string LogName = "DemoExample";

        // You can use an optional field to specify the timestamp from the data. If the time field is not specified, Log Analytics assumes the time is the message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for the API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;

            PostData(signature, datestring, json);
        }

        // Build the API signature
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

        // Send a request to the POST API endpoint
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

### <a name="python-sample"></a><span data-ttu-id="143cf-304">Exemplo de Python</span><span class="sxs-lookup"><span data-stu-id="143cf-304">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update the customer ID to your Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For the shared key, use either the primary or the secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# The log type is the name of the event that is being submitted
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

# Build the API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request to the POST API
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

## <a name="next-steps"></a><span data-ttu-id="143cf-305">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="143cf-305">Next steps</span></span>
- <span data-ttu-id="143cf-306">Usar a [API da pesquisa de log](log-analytics-log-search-api.md) para recuperar dados do repositório do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="143cf-306">Use the [Log Search API](log-analytics-log-search-api.md) to retrieve data from the Log Analytics repository.</span></span>
