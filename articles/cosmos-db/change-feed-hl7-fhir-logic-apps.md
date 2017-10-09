---
title: aaaChange feed para recursos HL7 FHIR - banco de dados do Azure Cosmos | Microsoft Docs
description: "Saiba como tooset a notificações de alteração para HL7 FHIR assistência médica registros de pacientes usando os aplicativos lógicos do Azure, o banco de dados do Azure Cosmos e barramento de serviço."
keywords: hl7 fhir
services: cosmos-db
author: hedidin
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 0d25c11f-9197-419a-aa19-4614c6ab2d06
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: b-hoedid
ms.openlocfilehash: d2809bf5c6d8c193c49438d20684c56caea646bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a>Notificando pacientes de alterações em registros de serviços de saúde HL7 FHIR usando os Aplicativos Lógicos e o Azure Cosmos DB

Azure MVP Howard Edidin recentemente foi contatado por uma organização de saúde que desejava tooadd novo funcionalidade tootheir paciente portal. Eles necessários toosend toopatients de notificações quando o registro de integridade foi atualizado, e eles necessários pacientes toobe toosubscribe capaz de toothese atualizações. 

Este artigo o orienta por meio da solução de feed de notificação de alteração Olá criada para esta organização de assistência médica usando o banco de dados do Azure Cosmos, aplicativos lógicos e barramento de serviço. 

## <a name="project-requirements"></a>Requisitos do projeto
- Os provedores enviam documentos C-CDA (Consolidated-Clinical Document Arquitecture) HL7 em formato XML. Os documentos C-CDA englobam praticamente qualquer tipo de documento clínico, incluindo documentos clínicos como históricos familiares e registros de vacinação, bem como documentos administrativos, de fluxo de trabalho e financeiros. 
- Documentos de C CDA são convertidos muito[HL7 FHIR recursos](http://hl7.org/fhir/2017Jan/resourcelist.html) no formato JSON.
- Os documentos de recurso FHIR modificados são enviados por email no formato JSON.

## <a name="solution-workflow"></a>Fluxo de trabalho da solução 

Em um nível alto, Olá Olá necessária do projeto seguindo as etapas do fluxo de trabalho: 
1. Converta os recursos do C CDA documentos tooFHIR.
2. Execute uma sondagem de gatilho recorrente para recursos FHIR modificados. 
2. Chame um aplicativo personalizado, FhirNotificationApi, tooconnect tooAzure Cosmos banco de dados e uma consulta para documentos novos ou modificados.
3. Salve a fila de barramento de serviço do hello resposta tootoohello.
4. Sondagem para novas mensagens na fila do barramento de serviço hello.
5. Envie toopatients de notificações de email.

## <a name="solution-architecture"></a>Arquitetura da solução
Essa solução requer três Olá toomeet de aplicativos lógicos acima requisitos e o fluxo de trabalho de solução completa hello. Olá três lógica aplicativos são:
1. **Aplicativo de mapeamento de FHIR HL7**: recebe um documento de HL7 C-CDA hello, transforma toohello FHIR recursos, em seguida, salva-tooAzure Cosmos DB.
2. **Aplicativo EHR**: consulta hello Azure Cosmos DB FHIR repositório e salva a fila de barramento de serviço do hello resposta tooa. Este aplicativo lógico usa um [aplicativo de API](#api-app) tooretrieve documentos de novas e alteradas.
3. **Aplicativo de notificação do processo**: envia uma notificação por email com os documentos de recurso FHIR Olá no corpo de saudação.

![Olá três lógica de aplicativos usados nesta solução saúde FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a>Serviços do Azure usados na solução de saudação

#### <a name="azure-cosmos-db-documentdb-api"></a>API do DocumentDB no Azure Cosmos DB
Banco de dados do Azure Cosmos é o repositório de saudação para recursos FHIR Olá conforme mostrado na figura a seguir de saudação.

![conta de banco de dados do Azure Cosmos Olá usada neste tutorial de assistência médica FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a>Aplicativos Lógicos
Aplicativos lógicos lidar com o processo de fluxo de trabalho de saudação. Olá seguintes capturas de tela mostram Olá aplicativos lógicos criados para esta solução. 


1. **Aplicativo de mapeamento de FHIR HL7**: receber Olá HL7 C-CDA documento e transforme-o recurso FHIR tooan usando Olá Enterprise Integration Pack para aplicativos lógicos. Olá Enterprise Integration Pack manipula Olá mapeamento de recursos de tooFHIR C CDA da saudação.

    ![Olá aplicativo lógico usado registros de saúde do tooreceive FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. **Aplicativo EHR**: consultar o repositório do Azure Cosmos DB FHIR hello e salvar Olá resposta tooa barramento de serviço de fila. código Olá Olá GetNewOrModifiedFHIRDocuments aplicativo está abaixo.

    ![Olá aplicativo lógico usado tooquery Azure Cosmos DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. **Aplicativo de notificação do processo**: enviar uma notificação por email com os documentos de recurso FHIR Olá no corpo de saudação.

    ![Olá lógica de aplicativo que envia email pacientes com recurso de FHIR HL7 Olá no corpo de saudação](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a>Barramento de Serviço
Olá seguinte figura mostra Olá pacientes fila. Olá valor da propriedade Tag é usado para o assunto do email Olá.

![Olá fila do barramento de serviço usados neste tutorial FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a>Aplicativo de API
Conecta-se um aplicativo de API tooAzure Cosmos banco de dados e consultas para documentos FHIR novos ou modificados por tipo de recurso. Este aplicativo tem um controlador, **FhirNotificationApi**, com uma operação **GetNewOrModifiedFhirDocuments**, veja [fonte do aplicativo de API](#api-app-source).

Estamos usando Olá [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) classe da saudação API .NET do Azure Cosmos DB documentos. Para obter mais informações, consulte Olá [alteração feed artigo](change-feed.md). 

##### <a name="getnewormodifiedfhirdocuments-operation"></a>Operação de GetNewOrModifiedFhirDocuments

**Entradas**
- DatabaseId
- CollectionId
- Nome do Tipo de Recurso FHIR HL7
- Booliano: Começar do início
- INT: Número de documentos retornados

**Saídas**
- Sucesso: Código de Status: 200, Resposta: Lista de Documentos (Matriz JSON)
- Falha: Código de Status: 404, Resposta: "Nenhum Documento encontrado para Tipo de Recurso '*nome do recurso '*"

<a id="api-app-source"></a>

**Origem para o aplicativo hello API**

```C#

    using System.Collections.Generic;
    using System.Linq;
    using System.Net;
    using System.Net.Http;
    using System.Threading.Tasks;
    using System.Web.Http;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Swashbuckle.Swagger.Annotations;
    using TRex.Metadata;
    
    namespace FhirNotificationApi.Controllers
    {
        /// <summary>
        ///     FHIR Resource Type Controller
        /// </summary>
        /// <seealso cref="System.Web.Http.ApiController" />
        public class FhirResourceTypeController : ApiController
        {
            /// <summary>
            ///     Gets hello new or modified FHIR documents from Last Run Date 
            ///     or create date of hello collection
            /// </summary>
            /// <param name="databaseId"></param>
            /// <param name="collectionId"></param>
            /// <param name="resourceType"></param>
            /// <param name="startfromBeginning"></param>
            /// <param name="maximumItemCount">-1 returns all (default)</param>
            /// <returns></returns>
            [Metadata("Get New or Modified FHIR Documents",
                "Query for new or modifed FHIR Documents By Resource Type " +
                "from Last Run Date or Begining of Collection creation"
            )]
            [SwaggerResponse(HttpStatusCode.OK, type: typeof(Task<dynamic>))]
            [SwaggerResponse(HttpStatusCode.NotFound, "No New or Modifed Documents found")]
            [SwaggerOperation("GetNewOrModifiedFHIRDocuments")]
            public async Task<dynamic> GetNewOrModifiedFhirDocuments(
                [Metadata("Database Id", "Database Id")] string databaseId,
                [Metadata("Collection Id", "Collection Id")] string collectionId,
                [Metadata("Resource Type", "FHIR resource type name")] string resourceType,
                [Metadata("Start from Beginning ", "Change Feed Option")] bool startfromBeginning,
                [Metadata("Maximum Item Count", "Number of documents returned. '-1 returns all' (default)")] int maximumItemCount = -1
            )
            {
                var collectionLink = UriFactory.CreateDocumentCollectionUri(databaseId, collectionId);
    
                var context = new DocumentDbContext();  
    
                var docs = new List<dynamic>();
    
                var partitionKeyRanges = new List<PartitionKeyRange>();
                FeedResponse<PartitionKeyRange> pkRangesResponse;
    
                do
                {
                    pkRangesResponse = await context.Client.ReadPartitionKeyRangeFeedAsync(collectionLink);
                    partitionKeyRanges.AddRange(pkRangesResponse);
                } while (pkRangesResponse.ResponseContinuation != null);
    
                foreach (var pkRange in partitionKeyRanges)
                {
                    var changeFeedOptions = new ChangeFeedOptions
                    {
                        StartFromBeginning = startfromBeginning,
                        RequestContinuation = null,
                        MaxItemCount = maximumItemCount,
                        PartitionKeyRangeId = pkRange.Id
                    };
    
                    using (var query = context.Client.CreateDocumentChangeFeedQuery(collectionLink, changeFeedOptions))
                    {
                        do
                        {
                            if (query != null)
                            {
                                var results = await query.ExecuteNextAsync<dynamic>().ConfigureAwait(false);
                                if (results.Count > 0)
                                    docs.AddRange(results.Where(doc => doc.resourceType == resourceType));
                            }
                            else
                            {
                                throw new HttpResponseException(new HttpResponseMessage(HttpStatusCode.NotFound));
                            }
                        } while (query.HasMoreResults);
                    }
                }
                if (docs.Count > 0)
                    return docs;
                var msg = new StringContent("No documents found for " + resourceType + " Resource");
                var response = new HttpResponseMessage
                {
                    StatusCode = HttpStatusCode.NotFound,
                    Content = msg
                };
                return response;
            }
        }
    }
    
```

### <a name="testing-hello-fhirnotificationapi"></a>Teste FhirNotificationApi 

Olá imagem a seguir demonstra como swagger foi usado tootootest Olá [FhirNotificationApi](#api-app-source).

![o arquivo Swagger Olá usado tootest saudação do aplicativo de API](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a>Painel do portal do Azure

Olá a imagem a seguir mostra todos os Olá serviços do Azure para essa solução em execução no hello portal do Azure.

![Olá portal do Azure mostrando todos os serviços de saudação usados neste tutorial FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a>Resumo

- Você aprendeu que o banco de dados do Azure Cosmos tem suporte nativo para notificações para novos ou modificados documentos e como é fácil toouse. 
- Aproveitando os Aplicativos Lógicos, você pode criar fluxos de trabalho sem escrever nenhum código.
- Usando a distribuição de saudação de toohandle de filas do barramento de serviço do Azure para documentos de FHIR HL7 hello.

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre o banco de dados do Azure Cosmos, consulte Olá [home page do banco de dados do Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/). Para saber mais sobre os Aplicativos Lógicos, veja [Aplicativos Lógicos](https://azure.microsoft.com/services/logic-apps/).


