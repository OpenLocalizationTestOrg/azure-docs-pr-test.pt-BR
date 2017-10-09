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
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="53405-104">Notificando pacientes de alterações em registros de serviços de saúde HL7 FHIR usando os Aplicativos Lógicos e o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="53405-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="53405-105">Azure MVP Howard Edidin recentemente foi contatado por uma organização de saúde que desejava tooadd novo funcionalidade tootheir paciente portal.</span><span class="sxs-lookup"><span data-stu-id="53405-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted tooadd new functionality tootheir patient portal.</span></span> <span data-ttu-id="53405-106">Eles necessários toosend toopatients de notificações quando o registro de integridade foi atualizado, e eles necessários pacientes toobe toosubscribe capaz de toothese atualizações.</span><span class="sxs-lookup"><span data-stu-id="53405-106">They needed toosend notifications toopatients when their health record was updated, and they needed patients toobe able toosubscribe toothese updates.</span></span> 

<span data-ttu-id="53405-107">Este artigo o orienta por meio da solução de feed de notificação de alteração Olá criada para esta organização de assistência médica usando o banco de dados do Azure Cosmos, aplicativos lógicos e barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="53405-107">This article walks through hello change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="53405-108">Requisitos do projeto</span><span class="sxs-lookup"><span data-stu-id="53405-108">Project requirements</span></span>
- <span data-ttu-id="53405-109">Os provedores enviam documentos C-CDA (Consolidated-Clinical Document Arquitecture) HL7 em formato XML.</span><span class="sxs-lookup"><span data-stu-id="53405-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="53405-110">Os documentos C-CDA englobam praticamente qualquer tipo de documento clínico, incluindo documentos clínicos como históricos familiares e registros de vacinação, bem como documentos administrativos, de fluxo de trabalho e financeiros.</span><span class="sxs-lookup"><span data-stu-id="53405-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="53405-111">Documentos de C CDA são convertidos muito[HL7 FHIR recursos](http://hl7.org/fhir/2017Jan/resourcelist.html) no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="53405-111">C-CDA documents are converted too[HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="53405-112">Os documentos de recurso FHIR modificados são enviados por email no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="53405-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="53405-113">Fluxo de trabalho da solução</span><span class="sxs-lookup"><span data-stu-id="53405-113">Solution workflow</span></span> 

<span data-ttu-id="53405-114">Em um nível alto, Olá Olá necessária do projeto seguindo as etapas do fluxo de trabalho:</span><span class="sxs-lookup"><span data-stu-id="53405-114">At a high level, hello project required hello following workflow steps:</span></span> 
1. <span data-ttu-id="53405-115">Converta os recursos do C CDA documentos tooFHIR.</span><span class="sxs-lookup"><span data-stu-id="53405-115">Convert C-CDA documents tooFHIR resources.</span></span>
2. <span data-ttu-id="53405-116">Execute uma sondagem de gatilho recorrente para recursos FHIR modificados.</span><span class="sxs-lookup"><span data-stu-id="53405-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="53405-117">Chame um aplicativo personalizado, FhirNotificationApi, tooconnect tooAzure Cosmos banco de dados e uma consulta para documentos novos ou modificados.</span><span class="sxs-lookup"><span data-stu-id="53405-117">Call a custom app, FhirNotificationApi, tooconnect tooAzure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="53405-118">Salve a fila de barramento de serviço do hello resposta tootoohello.</span><span class="sxs-lookup"><span data-stu-id="53405-118">Save hello response tootoohello Service Bus queue.</span></span>
4. <span data-ttu-id="53405-119">Sondagem para novas mensagens na fila do barramento de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="53405-119">Poll for new messages in hello Service Bus queue.</span></span>
5. <span data-ttu-id="53405-120">Envie toopatients de notificações de email.</span><span class="sxs-lookup"><span data-stu-id="53405-120">Send email notifications toopatients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="53405-121">Arquitetura da solução</span><span class="sxs-lookup"><span data-stu-id="53405-121">Solution architecture</span></span>
<span data-ttu-id="53405-122">Essa solução requer três Olá toomeet de aplicativos lógicos acima requisitos e o fluxo de trabalho de solução completa hello.</span><span class="sxs-lookup"><span data-stu-id="53405-122">This solution requires three Logic Apps toomeet hello above requirements and complete hello solution workflow.</span></span> <span data-ttu-id="53405-123">Olá três lógica aplicativos são:</span><span class="sxs-lookup"><span data-stu-id="53405-123">hello three logic apps are:</span></span>
1. <span data-ttu-id="53405-124">**Aplicativo de mapeamento de FHIR HL7**: recebe um documento de HL7 C-CDA hello, transforma toohello FHIR recursos, em seguida, salva-tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="53405-124">**HL7-FHIR-Mapping app**: Receives hello HL7 C-CDA document, transforms it toohello FHIR Resource, then saves it tooAzure Cosmos DB.</span></span>
2. <span data-ttu-id="53405-125">**Aplicativo EHR**: consulta hello Azure Cosmos DB FHIR repositório e salva a fila de barramento de serviço do hello resposta tooa.</span><span class="sxs-lookup"><span data-stu-id="53405-125">**EHR app**: Queries hello Azure Cosmos DB FHIR repository and saves hello response tooa Service Bus queue.</span></span> <span data-ttu-id="53405-126">Este aplicativo lógico usa um [aplicativo de API](#api-app) tooretrieve documentos de novas e alteradas.</span><span class="sxs-lookup"><span data-stu-id="53405-126">This logic app uses an [API app](#api-app) tooretrieve new and changed documents.</span></span>
3. <span data-ttu-id="53405-127">**Aplicativo de notificação do processo**: envia uma notificação por email com os documentos de recurso FHIR Olá no corpo de saudação.</span><span class="sxs-lookup"><span data-stu-id="53405-127">**Process notification app**: Sends an email notification with hello FHIR resource documents in hello body.</span></span>

![Olá três lógica de aplicativos usados nesta solução saúde FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-hello-solution"></a><span data-ttu-id="53405-129">Serviços do Azure usados na solução de saudação</span><span class="sxs-lookup"><span data-stu-id="53405-129">Azure services used in hello solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="53405-130">API do DocumentDB no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="53405-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="53405-131">Banco de dados do Azure Cosmos é o repositório de saudação para recursos FHIR Olá conforme mostrado na figura a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="53405-131">Azure Cosmos DB is hello repository for hello FHIR resources as shown in hello following figure.</span></span>

![conta de banco de dados do Azure Cosmos Olá usada neste tutorial de assistência médica FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="53405-133">Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="53405-133">Logic Apps</span></span>
<span data-ttu-id="53405-134">Aplicativos lógicos lidar com o processo de fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="53405-134">Logic Apps handle hello workflow process.</span></span> <span data-ttu-id="53405-135">Olá seguintes capturas de tela mostram Olá aplicativos lógicos criados para esta solução.</span><span class="sxs-lookup"><span data-stu-id="53405-135">hello following screenshots show hello Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="53405-136">**Aplicativo de mapeamento de FHIR HL7**: receber Olá HL7 C-CDA documento e transforme-o recurso FHIR tooan usando Olá Enterprise Integration Pack para aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="53405-136">**HL7-FHIR-Mapping app**: Receive hello HL7 C-CDA document and transform it tooan FHIR resource using hello Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="53405-137">Olá Enterprise Integration Pack manipula Olá mapeamento de recursos de tooFHIR C CDA da saudação.</span><span class="sxs-lookup"><span data-stu-id="53405-137">hello Enterprise Integration Pack handles hello mapping from hello C-CDA tooFHIR resources.</span></span>

    ![Olá aplicativo lógico usado registros de saúde do tooreceive FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="53405-139">**Aplicativo EHR**: consultar o repositório do Azure Cosmos DB FHIR hello e salvar Olá resposta tooa barramento de serviço de fila.</span><span class="sxs-lookup"><span data-stu-id="53405-139">**EHR app**: Query hello Azure Cosmos DB FHIR repository and save hello response tooa Service Bus queue.</span></span> <span data-ttu-id="53405-140">código Olá Olá GetNewOrModifiedFHIRDocuments aplicativo está abaixo.</span><span class="sxs-lookup"><span data-stu-id="53405-140">hello code for hello GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![Olá aplicativo lógico usado tooquery Azure Cosmos DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="53405-142">**Aplicativo de notificação do processo**: enviar uma notificação por email com os documentos de recurso FHIR Olá no corpo de saudação.</span><span class="sxs-lookup"><span data-stu-id="53405-142">**Process notification app**: Send an email notification with hello FHIR resource documents in hello body.</span></span>

    ![Olá lógica de aplicativo que envia email pacientes com recurso de FHIR HL7 Olá no corpo de saudação](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="53405-144">Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="53405-144">Service Bus</span></span>
<span data-ttu-id="53405-145">Olá seguinte figura mostra Olá pacientes fila.</span><span class="sxs-lookup"><span data-stu-id="53405-145">hello following figure shows hello patients queue.</span></span> <span data-ttu-id="53405-146">Olá valor da propriedade Tag é usado para o assunto do email Olá.</span><span class="sxs-lookup"><span data-stu-id="53405-146">hello Tag property value is used for hello email subject.</span></span>

![Olá fila do barramento de serviço usados neste tutorial FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="53405-148">Aplicativo de API</span><span class="sxs-lookup"><span data-stu-id="53405-148">API app</span></span>
<span data-ttu-id="53405-149">Conecta-se um aplicativo de API tooAzure Cosmos banco de dados e consultas para documentos FHIR novos ou modificados por tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="53405-149">An API app connects tooAzure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="53405-150">Este aplicativo tem um controlador, **FhirNotificationApi**, com uma operação **GetNewOrModifiedFhirDocuments**, veja [fonte do aplicativo de API](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="53405-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="53405-151">Estamos usando Olá [ `CreateDocumentChangeFeedQuery` ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) classe da saudação API .NET do Azure Cosmos DB documentos.</span><span class="sxs-lookup"><span data-stu-id="53405-151">We are using hello [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from hello Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="53405-152">Para obter mais informações, consulte Olá [alteração feed artigo](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="53405-152">For more information, see hello [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="53405-153">Operação de GetNewOrModifiedFhirDocuments</span><span class="sxs-lookup"><span data-stu-id="53405-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="53405-154">**Entradas**</span><span class="sxs-lookup"><span data-stu-id="53405-154">**Inputs**</span></span>
- <span data-ttu-id="53405-155">DatabaseId</span><span class="sxs-lookup"><span data-stu-id="53405-155">DatabaseId</span></span>
- <span data-ttu-id="53405-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="53405-156">CollectionId</span></span>
- <span data-ttu-id="53405-157">Nome do Tipo de Recurso FHIR HL7</span><span class="sxs-lookup"><span data-stu-id="53405-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="53405-158">Booliano: Começar do início</span><span class="sxs-lookup"><span data-stu-id="53405-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="53405-159">INT: Número de documentos retornados</span><span class="sxs-lookup"><span data-stu-id="53405-159">Int: Number of documents returned</span></span>

<span data-ttu-id="53405-160">**Saídas**</span><span class="sxs-lookup"><span data-stu-id="53405-160">**Outputs**</span></span>
- <span data-ttu-id="53405-161">Sucesso: Código de Status: 200, Resposta: Lista de Documentos (Matriz JSON)</span><span class="sxs-lookup"><span data-stu-id="53405-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="53405-162">Falha: Código de Status: 404, Resposta: "Nenhum Documento encontrado para Tipo de Recurso '*nome do recurso '*"</span><span class="sxs-lookup"><span data-stu-id="53405-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="53405-163">**Origem para o aplicativo hello API**</span><span class="sxs-lookup"><span data-stu-id="53405-163">**Source for hello API app**</span></span>

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

### <a name="testing-hello-fhirnotificationapi"></a><span data-ttu-id="53405-164">Teste FhirNotificationApi</span><span class="sxs-lookup"><span data-stu-id="53405-164">Testing hello FhirNotificationApi</span></span> 

<span data-ttu-id="53405-165">Olá imagem a seguir demonstra como swagger foi usado tootootest Olá [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="53405-165">hello following image demonstrates how swagger was used tootootest hello [FhirNotificationApi](#api-app-source).</span></span>

![o arquivo Swagger Olá usado tootest saudação do aplicativo de API](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="53405-167">Painel do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="53405-167">Azure portal dashboard</span></span>

<span data-ttu-id="53405-168">Olá a imagem a seguir mostra todos os Olá serviços do Azure para essa solução em execução no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="53405-168">hello following image shows all of hello Azure services for this solution running in hello Azure portal.</span></span>

![Olá portal do Azure mostrando todos os serviços de saudação usados neste tutorial FHIR HL7](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="53405-170">Resumo</span><span class="sxs-lookup"><span data-stu-id="53405-170">Summary</span></span>

- <span data-ttu-id="53405-171">Você aprendeu que o banco de dados do Azure Cosmos tem suporte nativo para notificações para novos ou modificados documentos e como é fácil toouse.</span><span class="sxs-lookup"><span data-stu-id="53405-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is toouse.</span></span> 
- <span data-ttu-id="53405-172">Aproveitando os Aplicativos Lógicos, você pode criar fluxos de trabalho sem escrever nenhum código.</span><span class="sxs-lookup"><span data-stu-id="53405-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="53405-173">Usando a distribuição de saudação de toohandle de filas do barramento de serviço do Azure para documentos de FHIR HL7 hello.</span><span class="sxs-lookup"><span data-stu-id="53405-173">Using Azure Service Bus Queues toohandle hello distribution for hello HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53405-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="53405-174">Next steps</span></span>
<span data-ttu-id="53405-175">Para obter mais informações sobre o banco de dados do Azure Cosmos, consulte Olá [home page do banco de dados do Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="53405-175">For more information about Azure Cosmos DB, see hello [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="53405-176">Para saber mais sobre os Aplicativos Lógicos, veja [Aplicativos Lógicos](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="53405-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


