---
title: "Alterar feed de recursos HL7 FHIR – Azure Cosmos DB | Microsoft Docs"
description: "Saiba como configurar notificações de alteração em registros de serviços de saúde de pacientes HL7 FHIR usando o Aplicativo Lógico do Azure, o Azure Cosmos DB e o Barramento de Serviço."
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
ms.openlocfilehash: d2b50c0b6864af41fb9cfa051721c432772b228d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="notifying-patients-of-hl7-fhir-health-care-record-changes-using-logic-apps-and-azure-cosmos-db"></a><span data-ttu-id="9730a-104">Notificando pacientes de alterações em registros de serviços de saúde HL7 FHIR usando os Aplicativos Lógicos e o Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9730a-104">Notifying patients of HL7 FHIR health care record changes using Logic Apps and Azure Cosmos DB</span></span>

<span data-ttu-id="9730a-105">Recentemente, o MVP do Azure Howard Edidin foi contatado por uma organização de saúde que queria adicionar uma nova funcionalidade ao seu portal do paciente.</span><span class="sxs-lookup"><span data-stu-id="9730a-105">Azure MVP Howard Edidin was recently contacted by a healthcare organization that wanted to add new functionality to their patient portal.</span></span> <span data-ttu-id="9730a-106">Eles precisavam enviar notificações aos pacientes quando o registro de saúde deles fosse atualizado, e precisavam que os pacientes pudessem assinar essas atualizações.</span><span class="sxs-lookup"><span data-stu-id="9730a-106">They needed to send notifications to patients when their health record was updated, and they needed patients to be able to subscribe to these updates.</span></span> 

<span data-ttu-id="9730a-107">Este artigo apresenta a solução de notificação de feed de alterações criada para esta organização de serviços de saúde usando o Azure Cosmos DB, os Aplicativos Lógicos e o Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="9730a-107">This article walks through the change feed notification solution created for this healthcare organization using Azure Cosmos DB, Logic Apps, and Service Bus.</span></span> 

## <a name="project-requirements"></a><span data-ttu-id="9730a-108">Requisitos do projeto</span><span class="sxs-lookup"><span data-stu-id="9730a-108">Project requirements</span></span>
- <span data-ttu-id="9730a-109">Os provedores enviam documentos C-CDA (Consolidated-Clinical Document Arquitecture) HL7 em formato XML.</span><span class="sxs-lookup"><span data-stu-id="9730a-109">Providers send HL7 Consolidated-Clinical Document Architecture (C-CDA) documents in XML format.</span></span> <span data-ttu-id="9730a-110">Os documentos C-CDA englobam praticamente qualquer tipo de documento clínico, incluindo documentos clínicos como históricos familiares e registros de vacinação, bem como documentos administrativos, de fluxo de trabalho e financeiros.</span><span class="sxs-lookup"><span data-stu-id="9730a-110">C-CDA documents encompass just about every type of clinical document, including clinical documents such as family histories and immunization records, as well as administrative, workflow, and financial documents.</span></span> 
- <span data-ttu-id="9730a-111">Os documentos C-CDA são convertidos em [Recursos HL7 FHIR](http://hl7.org/fhir/2017Jan/resourcelist.html) no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="9730a-111">C-CDA documents are converted to [HL7 FHIR Resources](http://hl7.org/fhir/2017Jan/resourcelist.html) in JSON format.</span></span>
- <span data-ttu-id="9730a-112">Os documentos de recurso FHIR modificados são enviados por email no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="9730a-112">Modified FHIR resource documents are sent by email in JSON format.</span></span>

## <a name="solution-workflow"></a><span data-ttu-id="9730a-113">Fluxo de trabalho da solução</span><span class="sxs-lookup"><span data-stu-id="9730a-113">Solution workflow</span></span> 

<span data-ttu-id="9730a-114">Em um alto nível, o projeto exigiu as seguintes etapas de fluxo de trabalho:</span><span class="sxs-lookup"><span data-stu-id="9730a-114">At a high level, the project required the following workflow steps:</span></span> 
1. <span data-ttu-id="9730a-115">Converta os documentos C-CDA em recursos FHIR.</span><span class="sxs-lookup"><span data-stu-id="9730a-115">Convert C-CDA documents to FHIR resources.</span></span>
2. <span data-ttu-id="9730a-116">Execute uma sondagem de gatilho recorrente para recursos FHIR modificados.</span><span class="sxs-lookup"><span data-stu-id="9730a-116">Perform recurring trigger polling for modified FHIR resources.</span></span> 
2. <span data-ttu-id="9730a-117">Chame um aplicativo personalizado, FhirNotificationApi, para se conectar ao Azure Cosmos DB e consultar documentos novos ou modificados.</span><span class="sxs-lookup"><span data-stu-id="9730a-117">Call a custom app, FhirNotificationApi, to connect to Azure Cosmos DB and query for new or modified documents.</span></span>
3. <span data-ttu-id="9730a-118">Salve a resposta na fila do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="9730a-118">Save the response to to the Service Bus queue.</span></span>
4. <span data-ttu-id="9730a-119">Sondagem de novas mensagens na fila do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="9730a-119">Poll for new messages in the Service Bus queue.</span></span>
5. <span data-ttu-id="9730a-120">Envie notificações por email para pacientes.</span><span class="sxs-lookup"><span data-stu-id="9730a-120">Send email notifications to patients.</span></span>

## <a name="solution-architecture"></a><span data-ttu-id="9730a-121">Arquitetura da solução</span><span class="sxs-lookup"><span data-stu-id="9730a-121">Solution architecture</span></span>
<span data-ttu-id="9730a-122">Essa solução requer três Aplicativos Lógicos atender aos requisitos acima e concluir o fluxo de trabalho da solução.</span><span class="sxs-lookup"><span data-stu-id="9730a-122">This solution requires three Logic Apps to meet the above requirements and complete the solution workflow.</span></span> <span data-ttu-id="9730a-123">Os três aplicativos lógicos são:</span><span class="sxs-lookup"><span data-stu-id="9730a-123">The three logic apps are:</span></span>
1. <span data-ttu-id="9730a-124">**Aplicativo Mapeamento de HL7 FHIR**: recebe o documento HL7 C-CDA, transforma-o no Recurso FHIR e, depois, salva-o no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9730a-124">**HL7-FHIR-Mapping app**: Receives the HL7 C-CDA document, transforms it to the FHIR Resource, then saves it to Azure Cosmos DB.</span></span>
2. <span data-ttu-id="9730a-125">**Aplicativo EHR**: consulta o repositório de FHIR do Azure Cosmos DB e salva a resposta em uma fila do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="9730a-125">**EHR app**: Queries the Azure Cosmos DB FHIR repository and saves the response to a Service Bus queue.</span></span> <span data-ttu-id="9730a-126">Esse aplicativo lógico usa um [aplicativo de API](#api-app) para recuperar documentos novos e alterados.</span><span class="sxs-lookup"><span data-stu-id="9730a-126">This logic app uses an [API app](#api-app) to retrieve new and changed documents.</span></span>
3. <span data-ttu-id="9730a-127">**Aplicativo de notificação do processo**: envia uma notificação por email com os documentos de recursos FHIR no corpo.</span><span class="sxs-lookup"><span data-stu-id="9730a-127">**Process notification app**: Sends an email notification with the FHIR resource documents in the body.</span></span>

![Os três Aplicativos Lógicos usados nesta solução saúde HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/health-care-solution-hl7-fhir.png)



### <a name="azure-services-used-in-the-solution"></a><span data-ttu-id="9730a-129">Serviços do Azure usados na solução</span><span class="sxs-lookup"><span data-stu-id="9730a-129">Azure services used in the solution</span></span>

#### <a name="azure-cosmos-db-documentdb-api"></a><span data-ttu-id="9730a-130">API do DocumentDB no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9730a-130">Azure Cosmos DB DocumentDB API</span></span>
<span data-ttu-id="9730a-131">O Azure Cosmos DB é o repositório dos recursos FHIR, conforme mostrado na figura a seguir.</span><span class="sxs-lookup"><span data-stu-id="9730a-131">Azure Cosmos DB is the repository for the FHIR resources as shown in the following figure.</span></span>

![A conta do Azure Cosmos DB usada neste tutorial de serviços de saúde HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/account.png)

#### <a name="logic-apps"></a><span data-ttu-id="9730a-133">Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="9730a-133">Logic Apps</span></span>
<span data-ttu-id="9730a-134">Os Aplicativos Lógicos lidam com o processo de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9730a-134">Logic Apps handle the workflow process.</span></span> <span data-ttu-id="9730a-135">As capturas de tela a seguir mostram os Aplicativos Lógicos criados para esta solução.</span><span class="sxs-lookup"><span data-stu-id="9730a-135">The following screenshots show the Logic apps created for this solution.</span></span> 


1. <span data-ttu-id="9730a-136">**Aplicativo de mapeamento de FHIR HL7**: recebem o documento HL7 C-CDA e transformá-la a um recurso FHIR usando o Enterprise Integration Pack para Aplicativos Lógicos.</span><span class="sxs-lookup"><span data-stu-id="9730a-136">**HL7-FHIR-Mapping app**: Receive the HL7 C-CDA document and transform it to an FHIR resource using the Enterprise Integration Pack for Logic Apps.</span></span> <span data-ttu-id="9730a-137">O Enterprise Integration Pack manipula o mapeamento de C-CDA para recursos FHIR.</span><span class="sxs-lookup"><span data-stu-id="9730a-137">The Enterprise Integration Pack handles the mapping from the C-CDA to FHIR resources.</span></span>

    ![O aplicativo lógico usado para receber registros médicos HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-json-transform.png)


2. <span data-ttu-id="9730a-139">**Aplicativo EHR**: consulte o repositório de FHIR do Azure Cosmos DB e salve a resposta em uma fila do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="9730a-139">**EHR app**: Query the Azure Cosmos DB FHIR repository and save the response to a Service Bus queue.</span></span> <span data-ttu-id="9730a-140">O código do aplicativo GetNewOrModifiedFHIRDocuments está abaixo.</span><span class="sxs-lookup"><span data-stu-id="9730a-140">The code for the GetNewOrModifiedFHIRDocuments app is below.</span></span>

    ![O Aplicativo Lógico usado para consultar o Azure Cosmos DB](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-api-app.png)

3. <span data-ttu-id="9730a-142">**Aplicativo de notificação do processo**: enviar uma notificação por email com os documentos de recursos FHIR no corpo.</span><span class="sxs-lookup"><span data-stu-id="9730a-142">**Process notification app**: Send an email notification with the FHIR resource documents in the body.</span></span>

    ![O aplicativo lógico que envia email pacientes com o recurso HL7 FHIR no corpo](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-logic-apps-send-email.png)

#### <a name="service-bus"></a><span data-ttu-id="9730a-144">Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="9730a-144">Service Bus</span></span>
<span data-ttu-id="9730a-145">A figura a seguir mostra os pacientes fila.</span><span class="sxs-lookup"><span data-stu-id="9730a-145">The following figure shows the patients queue.</span></span> <span data-ttu-id="9730a-146">O valor da propriedade Tag é usado para o assunto do email.</span><span class="sxs-lookup"><span data-stu-id="9730a-146">The Tag property value is used for the email subject.</span></span>

![A fila do Barramento de Serviço usada neste tutorial do HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-service-bus-queue.png)

<a id="api-app"></a>

#### <a name="api-app"></a><span data-ttu-id="9730a-148">Aplicativo de API</span><span class="sxs-lookup"><span data-stu-id="9730a-148">API app</span></span>
<span data-ttu-id="9730a-149">Um aplicativo de API se conecta ao Azure Cosmos DB e consulta documentos FHIR novos ou modificados por tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="9730a-149">An API app connects to Azure Cosmos DB and queries for new or modified FHIR documents By resource type.</span></span> <span data-ttu-id="9730a-150">Este aplicativo tem um controlador, **FhirNotificationApi**, com uma operação **GetNewOrModifiedFhirDocuments**, veja [fonte do aplicativo de API](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="9730a-150">This app has one controller, **FhirNotificationApi** with a one operation **GetNewOrModifiedFhirDocuments**, see [source for API app](#api-app-source).</span></span>

<span data-ttu-id="9730a-151">Estamos usando a classe [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) da API do .NET do DocumentDB no Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9730a-151">We are using the [`CreateDocumentChangeFeedQuery`](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery.aspx) class from the Azure Cosmos DB DocumentDB .NET API.</span></span> <span data-ttu-id="9730a-152">Para obter mais informações, consulte o [artigo sobre o feed de alterações](change-feed.md).</span><span class="sxs-lookup"><span data-stu-id="9730a-152">For more information, see the [change feed article](change-feed.md).</span></span> 

##### <a name="getnewormodifiedfhirdocuments-operation"></a><span data-ttu-id="9730a-153">Operação de GetNewOrModifiedFhirDocuments</span><span class="sxs-lookup"><span data-stu-id="9730a-153">GetNewOrModifiedFhirDocuments operation</span></span>

<span data-ttu-id="9730a-154">**Entradas**</span><span class="sxs-lookup"><span data-stu-id="9730a-154">**Inputs**</span></span>
- <span data-ttu-id="9730a-155">DatabaseId</span><span class="sxs-lookup"><span data-stu-id="9730a-155">DatabaseId</span></span>
- <span data-ttu-id="9730a-156">CollectionId</span><span class="sxs-lookup"><span data-stu-id="9730a-156">CollectionId</span></span>
- <span data-ttu-id="9730a-157">Nome do Tipo de Recurso FHIR HL7</span><span class="sxs-lookup"><span data-stu-id="9730a-157">HL7 FHIR Resource Type name</span></span>
- <span data-ttu-id="9730a-158">Booliano: Começar do início</span><span class="sxs-lookup"><span data-stu-id="9730a-158">Boolean: Start from Beginning</span></span>
- <span data-ttu-id="9730a-159">INT: Número de documentos retornados</span><span class="sxs-lookup"><span data-stu-id="9730a-159">Int: Number of documents returned</span></span>

<span data-ttu-id="9730a-160">**Saídas**</span><span class="sxs-lookup"><span data-stu-id="9730a-160">**Outputs**</span></span>
- <span data-ttu-id="9730a-161">Sucesso: Código de Status: 200, Resposta: Lista de Documentos (Matriz JSON)</span><span class="sxs-lookup"><span data-stu-id="9730a-161">Success: Status Code: 200, Response: List of Documents (JSON Array)</span></span>
- <span data-ttu-id="9730a-162">Falha: Código de Status: 404, Resposta: "Nenhum Documento encontrado para Tipo de Recurso '*nome do recurso '*"</span><span class="sxs-lookup"><span data-stu-id="9730a-162">Failure: Status Code: 404, Response: "No Documents found for '*resource name'* Resource Type"</span></span>

<a id="api-app-source"></a>

<span data-ttu-id="9730a-163">**Fonte do aplicativo de API**</span><span class="sxs-lookup"><span data-stu-id="9730a-163">**Source for the API app**</span></span>

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
            ///     Gets the new or modified FHIR documents from Last Run Date 
            ///     or create date of the collection
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

### <a name="testing-the-fhirnotificationapi"></a><span data-ttu-id="9730a-164">Testar o FhirNotificationApi</span><span class="sxs-lookup"><span data-stu-id="9730a-164">Testing the FhirNotificationApi</span></span> 

<span data-ttu-id="9730a-165">A imagem a seguir demonstra como o swagger foi usado para testar a [FhirNotificationApi](#api-app-source).</span><span class="sxs-lookup"><span data-stu-id="9730a-165">The following image demonstrates how swagger was used to to test the [FhirNotificationApi](#api-app-source).</span></span>

![O arquivo de Swagger usado para testar o aplicativo de API](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-testing-app.png)


### <a name="azure-portal-dashboard"></a><span data-ttu-id="9730a-167">Painel do portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9730a-167">Azure portal dashboard</span></span>

<span data-ttu-id="9730a-168">A imagem a seguir mostra todos os serviços do Azure para essa solução em execução no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9730a-168">The following image shows all of the Azure services for this solution running in the Azure portal.</span></span>

![O portal do Azure mostrando todos os serviços usados neste tutorial HL7 FHIR](./media/change-feed-hl7-fhir-logic-apps/hl7-fhir-portal.png)


## <a name="summary"></a><span data-ttu-id="9730a-170">Resumo</span><span class="sxs-lookup"><span data-stu-id="9730a-170">Summary</span></span>

- <span data-ttu-id="9730a-171">Você aprendeu que o Azure Cosmos DB tem suporte nativo para notificações em documentos novos ou modificados e como é fácil usá-lo.</span><span class="sxs-lookup"><span data-stu-id="9730a-171">You have learned that Azure Cosmos DB has native suppport for notifications for new or modifed documents and how easy it is to use.</span></span> 
- <span data-ttu-id="9730a-172">Aproveitando os Aplicativos Lógicos, você pode criar fluxos de trabalho sem escrever nenhum código.</span><span class="sxs-lookup"><span data-stu-id="9730a-172">By leveraging Logic Apps, you can create workflows without writing any code.</span></span>
- <span data-ttu-id="9730a-173">Uso de filas do Barramento de Serviço do Azure para lidar com a distribuição para os documentos FHIR HL7.</span><span class="sxs-lookup"><span data-stu-id="9730a-173">Using Azure Service Bus Queues to handle the distribution for the HL7 FHIR documents.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9730a-174">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9730a-174">Next steps</span></span>
<span data-ttu-id="9730a-175">Para obter mais informações sobre o Azure Cosmos DB, visite a [home page do Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="9730a-175">For more information about Azure Cosmos DB, see the [Azure Cosmos DB home page](https://azure.microsoft.com/services/cosmos-db/).</span></span> <span data-ttu-id="9730a-176">Para saber mais sobre os Aplicativos Lógicos, veja [Aplicativos Lógicos](https://azure.microsoft.com/services/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="9730a-176">For more informaiton about Logic Apps, see [Logic Apps](https://azure.microsoft.com/services/logic-apps/).</span></span>


