---
title: "aaaException tratamento e o cenário de log de erro - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Descreve um caso de uso real sobre o log de erros e o tratamento de exceção avançados do Aplicativo Lógico do Azure"
keywords: 
services: logic-apps
author: hedidin
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 63b0b843-f6b0-4d9a-98d0-17500be17385
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/29/2016
ms.author: LADocs; b-hoedid
ms.openlocfilehash: e893a7b652254dca7b8a82398e8afd571f6ccd25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="6410f-103">Cenário: Tratamento de exceção e log de erros de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="6410f-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="6410f-104">Este cenário descreve como você pode estender uma manipulação de exceção lógica aplicativo toobetter suporte.</span><span class="sxs-lookup"><span data-stu-id="6410f-104">This scenario describes how you can extend a logic app toobetter support exception handling.</span></span> <span data-ttu-id="6410f-105">Usamos uma pergunta de saudação tooanswer casos reais de uso: "Aplicativos lógicos do Azure suporta tratamento de erro e exceção?"</span><span class="sxs-lookup"><span data-stu-id="6410f-105">We've used a real-life use case tooanswer hello question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="6410f-106">esquema de aplicativos do Azure lógica atual Olá fornece um modelo padrão para respostas de ação.</span><span class="sxs-lookup"><span data-stu-id="6410f-106">hello current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="6410f-107">Esse modelo inclui a validação interna e as respostas de erro retornadas de um aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="6410f-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="6410f-108">Visão geral do cenário e do caso de uso</span><span class="sxs-lookup"><span data-stu-id="6410f-108">Scenario and use case overview</span></span>

<span data-ttu-id="6410f-109">Aqui está a história hello como caso de uso de saudação para este cenário:</span><span class="sxs-lookup"><span data-stu-id="6410f-109">Here's hello story as hello use case for this scenario:</span></span> 

<span data-ttu-id="6410f-110">Uma organização de saúde conhecida nos envolvido toodevelop uma solução do Azure que cria um portal de pacientes por meio do Microsoft Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="6410f-110">A well-known healthcare organization engaged us toodevelop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="6410f-111">Eles necessários toosend registros de compromisso entre o portal de pacientes Dynamics CRM Online hello e a equipe de vendas.</span><span class="sxs-lookup"><span data-stu-id="6410f-111">They needed toosend appointment records between hello Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="6410f-112">Perguntaram Olá toouse [FHIR HL7](http://www.hl7.org/implement/standards/fhir/) padrão para todos os registros de todos os pacientes.</span><span class="sxs-lookup"><span data-stu-id="6410f-112">We were asked toouse hello [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="6410f-113">projeto Olá tinha dois requisitos principais:</span><span class="sxs-lookup"><span data-stu-id="6410f-113">hello project had two major requirements:</span></span>  

* <span data-ttu-id="6410f-114">Um método toolog os registros enviados da saudação portal do Dynamics CRM Online</span><span class="sxs-lookup"><span data-stu-id="6410f-114">A method toolog records sent from hello Dynamics CRM Online portal</span></span>
* <span data-ttu-id="6410f-115">Uma maneira tooview quaisquer erros que ocorreram dentro de fluxo de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="6410f-115">A way tooview any errors that occurred within hello workflow</span></span>

> [!TIP]
> <span data-ttu-id="6410f-116">Para obter um vídeo de alto nível sobre esse projeto, consulte [grupo de usuário de integração](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "grupo de usuário de integração").</span><span class="sxs-lookup"><span data-stu-id="6410f-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-hello-problem"></a><span data-ttu-id="6410f-117">Como solucionamos o problema de saudação</span><span class="sxs-lookup"><span data-stu-id="6410f-117">How we solved hello problem</span></span>

<span data-ttu-id="6410f-118">Escolhemos [o banco de dados do Azure Cosmos](https://azure.microsoft.com/services/documentdb/ "o banco de dados do Azure Cosmos") como um repositório de registros de log e de erro de saudação (banco de dados do Cosmos refere-se toorecords como documentos).</span><span class="sxs-lookup"><span data-stu-id="6410f-118">We chose [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/ "Azure Cosmos DB") As a repository for hello log and error records (Cosmos DB refers toorecords as documents).</span></span> <span data-ttu-id="6410f-119">Como os aplicativos lógicos do Azure tem um modelo padrão para todas as respostas, nós não teria toocreate um esquema personalizado.</span><span class="sxs-lookup"><span data-stu-id="6410f-119">Because Azure Logic Apps has a standard template for all responses, we would not have toocreate a custom schema.</span></span> <span data-ttu-id="6410f-120">Poderíamos criar um aplicativo de API muito**inserir** e **consulta** para registros de erro e de log.</span><span class="sxs-lookup"><span data-stu-id="6410f-120">We could create an API app too**Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="6410f-121">É também possível definir um esquema para cada um no aplicativo de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="6410f-121">We could also define a schema for each within hello API app.</span></span>  

<span data-ttu-id="6410f-122">Outro requisito foi toopurge registros após uma determinada data.</span><span class="sxs-lookup"><span data-stu-id="6410f-122">Another requirement was toopurge records after a certain date.</span></span> <span data-ttu-id="6410f-123">Cosmos banco de dados tem uma propriedade chamada [tempo tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "tempo tooLive") (TTL), que permitiu tooset um **tempo tooLive** valor para cada registro ou coleção.</span><span class="sxs-lookup"><span data-stu-id="6410f-123">Cosmos DB has a property called [Time tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time tooLive") (TTL), which allowed us tooset a **Time tooLive** value for each record or collection.</span></span> <span data-ttu-id="6410f-124">Esse recurso eliminado Olá necessidade toomanually excluir registros no banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6410f-124">This capability eliminated hello need toomanually delete records in Cosmos DB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6410f-125">toocomplete neste tutorial, você precisa toocreate um banco de dados do banco de dados do Cosmos e duas coleções (erros e registro em log).</span><span class="sxs-lookup"><span data-stu-id="6410f-125">toocomplete this tutorial, you need toocreate a Cosmos DB database and two collections (Logging and Errors).</span></span>

## <a name="create-hello-logic-app"></a><span data-ttu-id="6410f-126">Criar aplicativo de lógica de saudação</span><span class="sxs-lookup"><span data-stu-id="6410f-126">Create hello logic app</span></span>

<span data-ttu-id="6410f-127">Olá primeira etapa é toocreate Olá lógica aplicativo e o aplicativo hello aberta no Designer de lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6410f-127">hello first step is toocreate hello logic app and open hello app in Logic App Designer.</span></span> <span data-ttu-id="6410f-128">Neste exemplo, estamos usando aplicativos lógicos pai-filho.</span><span class="sxs-lookup"><span data-stu-id="6410f-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="6410f-129">Vamos supor que nós já tiver criado o pai de saudação e vai toocreate um aplicativo de lógica de filho.</span><span class="sxs-lookup"><span data-stu-id="6410f-129">Let's assume that we have already created hello parent and are going toocreate one child logic app.</span></span>

<span data-ttu-id="6410f-130">Vamos começar como vamos toolog registro de saudação saindo do Dynamics CRM Online, na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="6410f-130">Because we are going toolog hello record coming out of Dynamics CRM Online, let's start at hello top.</span></span> <span data-ttu-id="6410f-131">É necessário usar um **solicitação** gatilho porque o aplicativo hello-lógica pai dispara esse filho.</span><span class="sxs-lookup"><span data-stu-id="6410f-131">We must use a **Request** trigger because hello parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="6410f-132">Gatilho de aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="6410f-132">Logic app trigger</span></span>

<span data-ttu-id="6410f-133">Estamos usando um **solicitação** disparar conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="6410f-133">We are using a **Request** trigger as shown in hello following example:</span></span>

```` json
"triggers": {
        "request": {
          "type": "request",
          "kind": "http",
          "inputs": {
            "schema": {
              "properties": {
                "CRMid": {
                  "type": "string"
                },
                "recordType": {
                  "type": "string"
                },
                "salesforceID": {
                  "type": "string"
                },
                "update": {
                  "type": "boolean"
                }
              },
              "required": [
                "CRMid",
                "recordType",
                "salesforceID",
                "update"
              ],
              "type": "object"
            }
          }
        }
      },

````


## <a name="steps"></a><span data-ttu-id="6410f-134">Etapas</span><span class="sxs-lookup"><span data-stu-id="6410f-134">Steps</span></span>

<span data-ttu-id="6410f-135">Deve registramos fonte hello (solicitação) de registro do paciente saudação do portal de saudação do Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="6410f-135">We must log hello source (request) of hello patient record from hello Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="6410f-136">É necessário obter um novo registro de compromisso do Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="6410f-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="6410f-137">gatilho Olá provenientes de CRM fornece Olá **CRM PatentId**, **tipo de registro**, **novo ou atualizado registro** (nova ou atualizar o valor booliano), e  **SalesforceId**.</span><span class="sxs-lookup"><span data-stu-id="6410f-137">hello trigger coming from CRM provides us with hello **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="6410f-138">Olá **SalesforceId** pode ser nulo, porque ele é usado somente para uma atualização.</span><span class="sxs-lookup"><span data-stu-id="6410f-138">hello **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="6410f-139">Obtemos o registro do CRM hello usando Olá CRM **PatientID** e hello **tipo de registro**.</span><span class="sxs-lookup"><span data-stu-id="6410f-139">We get hello CRM record by using hello CRM **PatientID** and hello **Record Type**.</span></span>

2. <span data-ttu-id="6410f-140">Em seguida, precisamos tooadd nosso aplicativo de API do DocumentDB **InsertLogEntry** operação, como mostrado aqui no Designer de lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6410f-140">Next, we need tooadd our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="6410f-141">**Inserir entrada de log**</span><span class="sxs-lookup"><span data-stu-id="6410f-141">**Insert log entry**</span></span>

   ![Inserir Entrada de Log](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="6410f-143">**Inserir entrada de erro**</span><span class="sxs-lookup"><span data-stu-id="6410f-143">**Insert error entry**</span></span>

   ![Inserir Entrada de Log](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="6410f-145">**Verificar falha na criação de registro**</span><span class="sxs-lookup"><span data-stu-id="6410f-145">**Check for create record failure**</span></span>

   ![Condição](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="6410f-147">Código-fonte do aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="6410f-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="6410f-148">Olá exemplos a seguir é apenas exemplos.</span><span class="sxs-lookup"><span data-stu-id="6410f-148">hello following examples are samples only.</span></span> <span data-ttu-id="6410f-149">Como este tutorial baseia-se em uma implementação em produção, Olá o valor de um **nó de origem** não pode exibir as propriedades que estão relacionada tooscheduling um compromisso. ></span><span class="sxs-lookup"><span data-stu-id="6410f-149">Because this tutorial is based on an implementation now in production, hello value of a **Source Node** might not display properties that are related tooscheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="6410f-150">Registro em log</span><span class="sxs-lookup"><span data-stu-id="6410f-150">Logging</span></span>

<span data-ttu-id="6410f-151">Olá após o código da lógica de aplicativo de exemplo mostra como toohandle registro em log.</span><span class="sxs-lookup"><span data-stu-id="6410f-151">hello following logic app code sample shows how toohandle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="6410f-152">Entrada de log</span><span class="sxs-lookup"><span data-stu-id="6410f-152">Log entry</span></span>

<span data-ttu-id="6410f-153">Aqui está o código-fonte aplicativo hello lógica para inserir uma entrada de log.</span><span class="sxs-lookup"><span data-stu-id="6410f-153">Here is hello logic app source code for inserting a log entry.</span></span>

``` json
"InsertLogEntry": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "date": "@{outputs('Gets_NewPatientRecord')['headers']['Date']}",
            "operation": "New Patient",
            "patientId": "@{triggerBody()['CRMid']}",
            "providerId": "@{triggerBody()['providerID']}",
            "source": "@{outputs('Gets_NewPatientRecord')['headers']}"
        },
        "method": "post",
        "uri": "https://.../api/Log"
        },
        "runAfter":    {
            "Gets_NewPatientecord": ["Succeeded"]
        }
}
```

#### <a name="log-request"></a><span data-ttu-id="6410f-154">Solicitação de log</span><span class="sxs-lookup"><span data-stu-id="6410f-154">Log request</span></span>

<span data-ttu-id="6410f-155">Aqui está a mensagem de solicitação de log Olá postada toohello aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="6410f-155">Here is hello log request message posted toohello API app.</span></span>

``` json
    {
    "uri": "https://.../api/Log",
    "method": "post",
    "body": {
        "date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "operation": "New Patient",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "providerId": "",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}"
        }
    }

```


#### <a name="log-response"></a><span data-ttu-id="6410f-156">Resposta de log</span><span class="sxs-lookup"><span data-stu-id="6410f-156">Log response</span></span>

<span data-ttu-id="6410f-157">Aqui está a mensagem de resposta de log de saudação do aplicativo de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="6410f-157">Here is hello log response message from hello API app.</span></span>

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:32:17 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "964",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "ttl": 2592000,
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0_1465597937",
        "_rid": "XngRAOT6IQEHAAAAAAAAAA==",
        "_self": "dbs/XngRAA==/colls/XngRAOT6IQE=/docs/XngRAOT6IQEHAAAAAAAAAA==/",
        "_ts": 1465597936,
        "_etag": "/"0400fc2f-0000-0000-0000-575b3ff00000/"",
        "patientID": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:56Z",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}",
        "operation": "New Patient",
        "salesforceId": "",
        "expired": false
    }
}

```

<span data-ttu-id="6410f-158">Agora vamos dar uma olhada em etapas de tratamento de erros de saudação.</span><span class="sxs-lookup"><span data-stu-id="6410f-158">Now let's look at hello error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="6410f-159">Tratamento de erros</span><span class="sxs-lookup"><span data-stu-id="6410f-159">Error handling</span></span>

<span data-ttu-id="6410f-160">Olá lógica aplicativo exemplo de código mostra como você pode implementar o tratamento de erros.</span><span class="sxs-lookup"><span data-stu-id="6410f-160">hello following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="6410f-161">Criar registro de erro</span><span class="sxs-lookup"><span data-stu-id="6410f-161">Create error record</span></span>

<span data-ttu-id="6410f-162">Aqui está o código-fonte aplicativo hello lógica para a criação de um registro de erro.</span><span class="sxs-lookup"><span data-stu-id="6410f-162">Here is hello logic app source code for creating an error record.</span></span>

``` json
"actions": {
    "CreateErrorRecord": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "action": "New_Patient",
            "isError": true,
            "crmId": "@{triggerBody()['CRMid']}",
            "patientID": "@{triggerBody()['CRMid']}",
            "message": "@{body('Create_NewPatientRecord')['message']}",
            "providerId": "@{triggerBody()['providerId']}",
            "severity": 4,
            "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
            "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
            "salesforceId": "",
            "update": false
        },
        "method": "post",
        "uri": "https://.../api/CrMtoSfError"
        },
        "runAfter":
        {
            "Create_NewPatientRecord": ["Failed" ]
        }
    }
}             
```

#### <a name="insert-error-into-cosmos-db--request"></a><span data-ttu-id="6410f-163">Inserir erro na solicitação do Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6410f-163">Insert error into Cosmos DB--request</span></span>

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-cosmos-db--response"></a><span data-ttu-id="6410f-164">Inserir erro na resposta do Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6410f-164">Insert error into Cosmos DB--response</span></span>

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:57 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "1561",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0-1465597917",
        "_rid": "sQx2APhVzAA8AAAAAAAAAA==",
        "_self": "dbs/sQx2AA==/colls/sQx2APhVzAA=/docs/sQx2APhVzAA8AAAAAAAAAA==/",
        "_ts": 1465597912,
        "_etag": "/"0c00eaac-0000-0000-0000-575b3fdc0000/"",
        "prescriberId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:57.3651027Z",
        "action": "New_Patient",
        "salesforceId": "",
        "update": false,
        "body": "CRM failed toocomplete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/":/"DO - Degree level is DO/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MterID_mp__c/":/"/",/"Medicis_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"XXXXXXX/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "code": 400,
        "errors": null,
        "isError": true,
        "severity": 4,
        "notes": null,
        "resolved": 0
        }
}
```

#### <a name="salesforce-error-response"></a><span data-ttu-id="6410f-165">Resposta de erro do Salesforce</span><span class="sxs-lookup"><span data-stu-id="6410f-165">Salesforce error response</span></span>

``` json
{
    "statusCode": 400,
    "headers": {
        "Pragma": "no-cache",
        "x-ms-request-id": "3e8e4884-288e-4633-972c-8271b2cc912c",
        "X-Content-Type-Options": "nosniff",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "Set-Cookie": "ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1",
        "Server": "Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "205",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "status": 400,
        "message": "Salesforce failed toocomplete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-hello-response-back-tooparent-logic-app"></a><span data-ttu-id="6410f-166">Olá retorno resposta tooparent back lógica aplicativo</span><span class="sxs-lookup"><span data-stu-id="6410f-166">Return hello response back tooparent logic app</span></span>

<span data-ttu-id="6410f-167">Depois de obter resposta hello, você pode passar a resposta Olá toohello back aplicativo-pai lógica.</span><span class="sxs-lookup"><span data-stu-id="6410f-167">After you get hello response, you can pass hello response back toohello parent logic app.</span></span>

#### <a name="return-success-response-tooparent-logic-app"></a><span data-ttu-id="6410f-168">Retornar o aplicativo de lógica de tooparent de resposta de êxito</span><span class="sxs-lookup"><span data-stu-id="6410f-168">Return success response tooparent logic app</span></span>

``` json
"SuccessResponse": {
    "runAfter":
        {
            "UpdateNew_CRMPatientResponse": ["Succeeded"]
        },
    "inputs": {
        "body": {
            "status": "Success"
    },
    "headers": {
    "    Content-type": "application/json",
        "x-ms-date": "@utcnow()"
    },
    "statusCode": 200
    },
    "type": "Response"
}
```

#### <a name="return-error-response-tooparent-logic-app"></a><span data-ttu-id="6410f-169">Aplicativo de lógica de tooparent de resposta de erro de retorno</span><span class="sxs-lookup"><span data-stu-id="6410f-169">Return error response tooparent logic app</span></span>

``` json
"ErrorResponse": {
    "runAfter":
        {
            "Create_NewPatientRecord": ["Failed"]
        },
    "inputs": {
        "body": {
            "status": "BadRequest"
        },
        "headers": {
            "Content-type": "application/json",
            "x-ms-date": "@utcnow()"
        },
        "statusCode": 400
    },
    "type": "Response"
}

```


## <a name="cosmos-db-repository-and-portal"></a><span data-ttu-id="6410f-170">Repositório e portal do Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6410f-170">Cosmos DB repository and portal</span></span>

<span data-ttu-id="6410f-171">Nossa solução adicionou funcionalidades ao [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span><span class="sxs-lookup"><span data-stu-id="6410f-171">Our solution added capabilities with [Cosmos DB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="6410f-172">Portal de gerenciamento de erros</span><span class="sxs-lookup"><span data-stu-id="6410f-172">Error management portal</span></span>

<span data-ttu-id="6410f-173">erros de saudação tooview, você pode criar um registros de erro do MVC web aplicativo toodisplay Olá do banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6410f-173">tooview hello errors, you can create an MVC web app toodisplay hello error records from Cosmos DB.</span></span> <span data-ttu-id="6410f-174">Olá **lista**, **detalhes**, **editar**, e **excluir** operações serão incluídas na versão atual do hello.</span><span class="sxs-lookup"><span data-stu-id="6410f-174">hello **List**, **Details**, **Edit**, and **Delete** operations are included in hello current version.</span></span>

> [!NOTE]
> <span data-ttu-id="6410f-175">A operação de editar: Cosmos DB substitui todo o documento hello.</span><span class="sxs-lookup"><span data-stu-id="6410f-175">Edit operation: Cosmos DB replaces hello entire document.</span></span> <span data-ttu-id="6410f-176">Olá registros mostrados em Olá **lista** e **detalhes** modos de exibição são apenas exemplos.</span><span class="sxs-lookup"><span data-stu-id="6410f-176">hello records shown in hello **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="6410f-177">Eles não são registros reais de consultas de pacientes.</span><span class="sxs-lookup"><span data-stu-id="6410f-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="6410f-178">Aqui estão exemplos de nosso aplicativo MVC criado anteriormente com hello detalhes abordagem.</span><span class="sxs-lookup"><span data-stu-id="6410f-178">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="6410f-179">Lista de gerenciamento de erros</span><span class="sxs-lookup"><span data-stu-id="6410f-179">Error management list</span></span>
![Lista de Erros](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="6410f-181">Modo de exibição de detalhes do gerenciamento de erros</span><span class="sxs-lookup"><span data-stu-id="6410f-181">Error management detail view</span></span>
![Detalhes do Erro](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="6410f-183">Portal de gerenciamento de logs</span><span class="sxs-lookup"><span data-stu-id="6410f-183">Log management portal</span></span>

<span data-ttu-id="6410f-184">logs de saudação tooview, também criamos um aplicativo da web MVC.</span><span class="sxs-lookup"><span data-stu-id="6410f-184">tooview hello logs, we also created an MVC web app.</span></span> <span data-ttu-id="6410f-185">Aqui estão exemplos de nosso aplicativo MVC criado anteriormente com hello detalhes abordagem.</span><span class="sxs-lookup"><span data-stu-id="6410f-185">Here are examples of our MVC app details created with hello previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="6410f-186">Modo de exibição de detalhes de log de exemplo</span><span class="sxs-lookup"><span data-stu-id="6410f-186">Sample log detail view</span></span>
![Modo de Exibição de Detalhes de Log](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="6410f-188">Detalhes do aplicativo de API</span><span class="sxs-lookup"><span data-stu-id="6410f-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="6410f-189">API de gerenciamento de exceções de Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="6410f-189">Logic Apps exception management API</span></span>

<span data-ttu-id="6410f-190">Nosso aplicativo de API de gerenciamento de exceções do Aplicativo Lógico do Azure de software livre fornece a funcionalidade conforme descrito a seguir - existem dois controladores:</span><span class="sxs-lookup"><span data-stu-id="6410f-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="6410f-191">**ErrorController** insere um registro de erro (documento) em uma coleção do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="6410f-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="6410f-192">**LogController** insere um registro de log (documento) em uma coleção do DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="6410f-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="6410f-193">Usam ambos os controladores `async Task<dynamic>` Olá de operações, permitindo operações tooresolve em tempo de execução, portanto, podemos criar documentos de esquema no corpo de saudação da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6410f-193">Both controllers use `async Task<dynamic>` operations, allowing operations tooresolve at runtime, so we can create hello DocumentDB schema in hello body of hello operation.</span></span> 
> 

<span data-ttu-id="6410f-194">Todos os documentos do DocumentDB devem ter uma ID exclusiva.</span><span class="sxs-lookup"><span data-stu-id="6410f-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="6410f-195">Estamos usando `PatientId` e adicionar um carimbo de hora é convertida valor de carimbo de hora tooa Unix (double).</span><span class="sxs-lookup"><span data-stu-id="6410f-195">We are using `PatientId` and adding a timestamp that is converted tooa Unix timestamp value (double).</span></span> <span data-ttu-id="6410f-196">Podemos truncar Olá tooremove Olá fracionária do valor.</span><span class="sxs-lookup"><span data-stu-id="6410f-196">We truncate hello value tooremove hello fractional value.</span></span>

<span data-ttu-id="6410f-197">Você pode exibir o código-fonte saudação do nosso controlador erro API [do GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span><span class="sxs-lookup"><span data-stu-id="6410f-197">You can view hello source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="6410f-198">Chamamos Olá API de um aplicativo lógico usando Olá sintaxe a seguir:</span><span class="sxs-lookup"><span data-stu-id="6410f-198">We call hello API from a logic app by using hello following syntax:</span></span>

``` json
 "actions": {
        "CreateErrorRecord": {
          "metadata": {
            "apiDefinitionUrl": "https://.../swagger/docs/v1",
            "swaggerSource": "website"
          },
          "type": "Http",
          "inputs": {
            "body": {
              "action": "New_Patient",
              "isError": true,
              "crmId": "@{triggerBody()['CRMid']}",
              "prescriberId": "@{triggerBody()['CRMid']}",
              "message": "@{body('Create_NewPatientRecord')['message']}",
              "salesforceId": "@{triggerBody()['salesforceID']}",
              "severity": 4,
              "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
              "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
              "update": false
            },
            "method": "post",
            "uri": "https://.../api/CrMtoSfError"
          },
          "runAfter": {
              "Create_NewPatientRecord": ["Failed"]
            }
        }
 }
```

<span data-ttu-id="6410f-199">Olá expressão em Olá anterior verificações de exemplo de código para hello *Create_NewPatientRecord* status de **falha**.</span><span class="sxs-lookup"><span data-stu-id="6410f-199">hello expression in hello preceding code sample checks for hello *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="6410f-200">Resumo</span><span class="sxs-lookup"><span data-stu-id="6410f-200">Summary</span></span>

* <span data-ttu-id="6410f-201">Você pode implementar facilmente o tratamento de logs e de erros em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="6410f-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="6410f-202">Você pode usar documentos como repositório de saudação para registros de log e de erros (documentos).</span><span class="sxs-lookup"><span data-stu-id="6410f-202">You can use DocumentDB as hello repository for log and error records (documents).</span></span>
* <span data-ttu-id="6410f-203">Você pode usar o MVC toocreate um log toodisplay portal e registros de erro.</span><span class="sxs-lookup"><span data-stu-id="6410f-203">You can use MVC toocreate a portal toodisplay log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="6410f-204">Código-fonte</span><span class="sxs-lookup"><span data-stu-id="6410f-204">Source code</span></span>

<span data-ttu-id="6410f-205">código-fonte Olá Olá aplicativo de API de gerenciamento de exceção de aplicativos de lógica está disponível neste [repositório GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "lógica de API de gerenciamento de exceção de aplicativo").</span><span class="sxs-lookup"><span data-stu-id="6410f-205">hello source code for hello Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="6410f-206">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6410f-206">Next steps</span></span>

* [<span data-ttu-id="6410f-207">Exibir mais exemplos e cenários de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="6410f-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="6410f-208">Saiba mais sobre como monitorar aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="6410f-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="6410f-209">Criar modelos de implantação automatizados para aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="6410f-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
