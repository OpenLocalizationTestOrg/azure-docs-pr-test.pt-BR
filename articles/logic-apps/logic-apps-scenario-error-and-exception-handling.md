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
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a>Cenário: Tratamento de exceção e log de erros de aplicativos lógicos

Este cenário descreve como você pode estender uma manipulação de exceção lógica aplicativo toobetter suporte. Usamos uma pergunta de saudação tooanswer casos reais de uso: "Aplicativos lógicos do Azure suporta tratamento de erro e exceção?"

> [!NOTE]
> esquema de aplicativos do Azure lógica atual Olá fornece um modelo padrão para respostas de ação. Esse modelo inclui a validação interna e as respostas de erro retornadas de um aplicativo de API.

## <a name="scenario-and-use-case-overview"></a>Visão geral do cenário e do caso de uso

Aqui está a história hello como caso de uso de saudação para este cenário: 

Uma organização de saúde conhecida nos envolvido toodevelop uma solução do Azure que cria um portal de pacientes por meio do Microsoft Dynamics CRM Online. Eles necessários toosend registros de compromisso entre o portal de pacientes Dynamics CRM Online hello e a equipe de vendas. Perguntaram Olá toouse [FHIR HL7](http://www.hl7.org/implement/standards/fhir/) padrão para todos os registros de todos os pacientes.

projeto Olá tinha dois requisitos principais:  

* Um método toolog os registros enviados da saudação portal do Dynamics CRM Online
* Uma maneira tooview quaisquer erros que ocorreram dentro de fluxo de trabalho Olá

> [!TIP]
> Para obter um vídeo de alto nível sobre esse projeto, consulte [grupo de usuário de integração](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "grupo de usuário de integração").

## <a name="how-we-solved-hello-problem"></a>Como solucionamos o problema de saudação

Escolhemos [o banco de dados do Azure Cosmos](https://azure.microsoft.com/services/documentdb/ "o banco de dados do Azure Cosmos") como um repositório de registros de log e de erro de saudação (banco de dados do Cosmos refere-se toorecords como documentos). Como os aplicativos lógicos do Azure tem um modelo padrão para todas as respostas, nós não teria toocreate um esquema personalizado. Poderíamos criar um aplicativo de API muito**inserir** e **consulta** para registros de erro e de log. É também possível definir um esquema para cada um no aplicativo de API de saudação.  

Outro requisito foi toopurge registros após uma determinada data. Cosmos banco de dados tem uma propriedade chamada [tempo tooLive](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "tempo tooLive") (TTL), que permitiu tooset um **tempo tooLive** valor para cada registro ou coleção. Esse recurso eliminado Olá necessidade toomanually excluir registros no banco de dados do Cosmos.

> [!IMPORTANT]
> toocomplete neste tutorial, você precisa toocreate um banco de dados do banco de dados do Cosmos e duas coleções (erros e registro em log).

## <a name="create-hello-logic-app"></a>Criar aplicativo de lógica de saudação

Olá primeira etapa é toocreate Olá lógica aplicativo e o aplicativo hello aberta no Designer de lógica do aplicativo. Neste exemplo, estamos usando aplicativos lógicos pai-filho. Vamos supor que nós já tiver criado o pai de saudação e vai toocreate um aplicativo de lógica de filho.

Vamos começar como vamos toolog registro de saudação saindo do Dynamics CRM Online, na parte superior da saudação. É necessário usar um **solicitação** gatilho porque o aplicativo hello-lógica pai dispara esse filho.

### <a name="logic-app-trigger"></a>Gatilho de aplicativo lógico

Estamos usando um **solicitação** disparar conforme mostrado no exemplo a seguir de saudação:

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


## <a name="steps"></a>Etapas

Deve registramos fonte hello (solicitação) de registro do paciente saudação do portal de saudação do Dynamics CRM Online.

1. É necessário obter um novo registro de compromisso do Dynamics CRM Online.

   gatilho Olá provenientes de CRM fornece Olá **CRM PatentId**, **tipo de registro**, **novo ou atualizado registro** (nova ou atualizar o valor booliano), e  **SalesforceId**. Olá **SalesforceId** pode ser nulo, porque ele é usado somente para uma atualização.
   Obtemos o registro do CRM hello usando Olá CRM **PatientID** e hello **tipo de registro**.

2. Em seguida, precisamos tooadd nosso aplicativo de API do DocumentDB **InsertLogEntry** operação, como mostrado aqui no Designer de lógica do aplicativo.

   **Inserir entrada de log**

   ![Inserir Entrada de Log](media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   **Inserir entrada de erro**

   ![Inserir Entrada de Log](media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   **Verificar falha na criação de registro**

   ![Condição](media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a>Código-fonte do aplicativo lógico

> [!NOTE]
> Olá exemplos a seguir é apenas exemplos. Como este tutorial baseia-se em uma implementação em produção, Olá o valor de um **nó de origem** não pode exibir as propriedades que estão relacionada tooscheduling um compromisso. > 

### <a name="logging"></a>Registro em log

Olá após o código da lógica de aplicativo de exemplo mostra como toohandle registro em log.

#### <a name="log-entry"></a>Entrada de log

Aqui está o código-fonte aplicativo hello lógica para inserir uma entrada de log.

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

#### <a name="log-request"></a>Solicitação de log

Aqui está a mensagem de solicitação de log Olá postada toohello aplicativo de API.

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


#### <a name="log-response"></a>Resposta de log

Aqui está a mensagem de resposta de log de saudação do aplicativo de API de saudação.

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

Agora vamos dar uma olhada em etapas de tratamento de erros de saudação.

### <a name="error-handling"></a>Tratamento de erros

Olá lógica aplicativo exemplo de código mostra como você pode implementar o tratamento de erros.

#### <a name="create-error-record"></a>Criar registro de erro

Aqui está o código-fonte aplicativo hello lógica para a criação de um registro de erro.

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

#### <a name="insert-error-into-cosmos-db--request"></a>Inserir erro na solicitação do Cosmos DB

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

#### <a name="insert-error-into-cosmos-db--response"></a>Inserir erro na resposta do Cosmos DB

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

#### <a name="salesforce-error-response"></a>Resposta de erro do Salesforce

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

### <a name="return-hello-response-back-tooparent-logic-app"></a>Olá retorno resposta tooparent back lógica aplicativo

Depois de obter resposta hello, você pode passar a resposta Olá toohello back aplicativo-pai lógica.

#### <a name="return-success-response-tooparent-logic-app"></a>Retornar o aplicativo de lógica de tooparent de resposta de êxito

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

#### <a name="return-error-response-tooparent-logic-app"></a>Aplicativo de lógica de tooparent de resposta de erro de retorno

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


## <a name="cosmos-db-repository-and-portal"></a>Repositório e portal do Cosmos DB

Nossa solução adicionou funcionalidades ao [Cosmos DB](https://azure.microsoft.com/services/documentdb).

### <a name="error-management-portal"></a>Portal de gerenciamento de erros

erros de saudação tooview, você pode criar um registros de erro do MVC web aplicativo toodisplay Olá do banco de dados do Cosmos. Olá **lista**, **detalhes**, **editar**, e **excluir** operações serão incluídas na versão atual do hello.

> [!NOTE]
> A operação de editar: Cosmos DB substitui todo o documento hello. Olá registros mostrados em Olá **lista** e **detalhes** modos de exibição são apenas exemplos. Eles não são registros reais de consultas de pacientes.

Aqui estão exemplos de nosso aplicativo MVC criado anteriormente com hello detalhes abordagem.

#### <a name="error-management-list"></a>Lista de gerenciamento de erros
![Lista de Erros](media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a>Modo de exibição de detalhes do gerenciamento de erros
![Detalhes do Erro](media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a>Portal de gerenciamento de logs

logs de saudação tooview, também criamos um aplicativo da web MVC. Aqui estão exemplos de nosso aplicativo MVC criado anteriormente com hello detalhes abordagem.

#### <a name="sample-log-detail-view"></a>Modo de exibição de detalhes de log de exemplo
![Modo de Exibição de Detalhes de Log](media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a>Detalhes do aplicativo de API

#### <a name="logic-apps-exception-management-api"></a>API de gerenciamento de exceções de Aplicativos Lógicos

Nosso aplicativo de API de gerenciamento de exceções do Aplicativo Lógico do Azure de software livre fornece a funcionalidade conforme descrito a seguir - existem dois controladores:

* **ErrorController** insere um registro de erro (documento) em uma coleção do DocumentDB.
* **LogController** insere um registro de log (documento) em uma coleção do DocumentDB.

> [!TIP]
> Usam ambos os controladores `async Task<dynamic>` Olá de operações, permitindo operações tooresolve em tempo de execução, portanto, podemos criar documentos de esquema no corpo de saudação da operação de saudação. 
> 

Todos os documentos do DocumentDB devem ter uma ID exclusiva. Estamos usando `PatientId` e adicionar um carimbo de hora é convertida valor de carimbo de hora tooa Unix (double). Podemos truncar Olá tooremove Olá fracionária do valor.

Você pode exibir o código-fonte saudação do nosso controlador erro API [do GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).

Chamamos Olá API de um aplicativo lógico usando Olá sintaxe a seguir:

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

Olá expressão em Olá anterior verificações de exemplo de código para hello *Create_NewPatientRecord* status de **falha**.

## <a name="summary"></a>Resumo

* Você pode implementar facilmente o tratamento de logs e de erros em um aplicativo lógico.
* Você pode usar documentos como repositório de saudação para registros de log e de erros (documentos).
* Você pode usar o MVC toocreate um log toodisplay portal e registros de erro.

### <a name="source-code"></a>Código-fonte

código-fonte Olá Olá aplicativo de API de gerenciamento de exceção de aplicativos de lógica está disponível neste [repositório GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "lógica de API de gerenciamento de exceção de aplicativo").

## <a name="next-steps"></a>Próximas etapas

* [Exibir mais exemplos e cenários de aplicativos lógicos](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Saiba mais sobre como monitorar aplicativos lógicos](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [Criar modelos de implantação automatizados para aplicativos lógicos](../logic-apps/logic-apps-create-deploy-template.md)
