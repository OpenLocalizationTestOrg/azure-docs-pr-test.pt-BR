---
title: Como usar o Power BI Embedded com REST | Microsoft Docs
description: 'Saiba como usar o Power BI Embedded com o REST  '
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 8bcef780-cca0-4f30-9a9b-9daa1a7ae865
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 02/06/2017
ms.author: asaxton
ms.openlocfilehash: 31624b9d15772a4f08cf013ac713b3aa636acfca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-power-bi-embedded-with-rest"></a><span data-ttu-id="0e690-103">Como usar o Power BI Embedded com REST</span><span class="sxs-lookup"><span data-stu-id="0e690-103">How to use Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="0e690-104">Power BI Embedded: o que é e para que serve</span><span class="sxs-lookup"><span data-stu-id="0e690-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="0e690-105">Uma visão geral do Power BI Embedded é descrita no [site oficial do Power BI Embedded](https://azure.microsoft.com/services/power-bi-embedded/), mas vamos dar uma rápida olhada antes de adentrarmos nos detalhes sobre como usá-lo com o REST.</span><span class="sxs-lookup"><span data-stu-id="0e690-105">An overview of Power BI Embedded is described in the official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into the details about using it with REST.</span></span>

<span data-ttu-id="0e690-106">Ele é realmente bem simples.</span><span class="sxs-lookup"><span data-stu-id="0e690-106">It's quite simple, really.</span></span> <span data-ttu-id="0e690-107">Talvez você queira usar as visualizações de dados dinâmicos do [Power BI](https://powerbi.microsoft.com) em seu próprio aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0e690-107">you may want to use the dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="0e690-108">A maioria dos aplicativos personalizados precisa distribuir os dados para seus próprios clientes, não necessariamente usuários em sua própria organização.</span><span class="sxs-lookup"><span data-stu-id="0e690-108">Most custom applications need to deliver the data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="0e690-109">Por exemplo, se você estiver distribuindo algum serviço para a empresa A e a empresa B, os usuários na empresa A deverão ver apenas os dados de sua própria empresa. Isto é, a multilocação é necessária para a distribuição.</span><span class="sxs-lookup"><span data-stu-id="0e690-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, the multi-tenancy is needed for the delivery.</span></span>

<span data-ttu-id="0e690-110">O aplicativo personalizado também pode oferecer seus próprios métodos de autenticação, como autenticação de formulário, autenticação básica etc.</span><span class="sxs-lookup"><span data-stu-id="0e690-110">The custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="0e690-111">Assim, a solução de inserção deve colaborar com esses métodos existentes de autenticação de modo seguro.</span><span class="sxs-lookup"><span data-stu-id="0e690-111">Then, the embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="0e690-112">Também é necessário para os usuários poder usar esses aplicativos ISV sem a compra extra ou o licenciamento de uma assinatura do Power BI.</span><span class="sxs-lookup"><span data-stu-id="0e690-112">It's also necessary for users to be able to use those ISV applications without the extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="0e690-113">O **Power BI Embedded** foi desenvolvido exatamente para esses tipos de cenários.</span><span class="sxs-lookup"><span data-stu-id="0e690-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="0e690-114">Agora que fizemos essa rápida introdução, vamos entrar nos detalhes</span><span class="sxs-lookup"><span data-stu-id="0e690-114">So, now that we have that quick introduction out of the way, let's get into some details</span></span>

<span data-ttu-id="0e690-115">É possível usar o SDK para .NET \(C#) ou Node.js para criar seu aplicativo facilmente com o Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="0e690-115">You can use the .NET \(C#) or Node.js SDK, to easily build your application with Power BI Embedded.</span></span> <span data-ttu-id="0e690-116">Mas, neste artigo, explicaremos sobre o fluxo do HTTP \(incluindo AuthN) do Power BI sem SDKs.</span><span class="sxs-lookup"><span data-stu-id="0e690-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="0e690-117">Entendendo esse fluxo, você pode criar seu aplicativo **com qualquer linguagem de programação**, além de poder entender profundamente a essência do Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="0e690-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply the essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="0e690-118">Criar a coleção de espaços de trabalho do Power BI e obter tecla de acesso \(provisionamento)</span><span class="sxs-lookup"><span data-stu-id="0e690-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="0e690-119">O Power BI Embedded é um dos serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e690-119">Power BI Embedded is one of the Azure services.</span></span> <span data-ttu-id="0e690-120">Apenas o ISV que usa o Portal do Azure é cobrado pelo uso \(sessão de usuário por hora). O usuário que exibe o relatório não é cobrado, e nem mesmo uma assinatura do Azure é exigida.</span><span class="sxs-lookup"><span data-stu-id="0e690-120">Only the ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and the user who views the report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="0e690-121">Antes de iniciar o desenvolvimento do nosso aplicativo, devemos criar a **coleção de espaços de trabalho do Power BI** usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e690-121">Before starting our application development, we must create the **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="0e690-122">Cada espaço de trabalho do Power BI Embedded é o espaço de trabalho de cada cliente (locatário), e podemos adicionar muitos espaços de trabalho em cada coleção de espaços de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0e690-122">Each workspace of Power BI Embedded is the workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="0e690-123">A mesma tecla de acesso é usada em cada coleção de espaços de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0e690-123">The same access key is used in each workspace collection.</span></span> <span data-ttu-id="0e690-124">Em vigor, a coleção de espaços de trabalho é o limite de segurança do Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="0e690-124">In-effect, the workspace collection is the security boundary for Power BI Embedded.</span></span>

![](media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="0e690-125">Quando concluirmos a criação da coleção de espaços de trabalho, copie a tecla de acesso do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0e690-125">When we finish creating the workspace collection, copy the access key from Azure Portal.</span></span>

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="0e690-126">Também podemos provisionar a coleção de espaços de trabalho e obter a tecla de acesso por meio da API REST.</span><span class="sxs-lookup"><span data-stu-id="0e690-126">We can also provision the workspace collection and get access key via REST API.</span></span> <span data-ttu-id="0e690-127">Para saber mais, confira [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx)(APIs do provedor de recursos do Power BI).</span><span class="sxs-lookup"><span data-stu-id="0e690-127">To learn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="0e690-128">Criar o arquivo .pbix com o Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="0e690-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="0e690-129">Em seguida, devemos criar a conexão de dados e os relatórios a serem inseridos.</span><span class="sxs-lookup"><span data-stu-id="0e690-129">Next, we must create the data connection and reports to be embedded.</span></span>
<span data-ttu-id="0e690-130">Para essa tarefa, não há programação nem código.</span><span class="sxs-lookup"><span data-stu-id="0e690-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="0e690-131">Vamos usar apenas o Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="0e690-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="0e690-132">Neste artigo, não entraremos em detalhes sobre como usar o Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="0e690-132">In this article, we won't go through the details about how to use Power BI Desktop.</span></span> <span data-ttu-id="0e690-133">Se precisar de ajuda aqui, confira [Introdução ao Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="0e690-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="0e690-134">Em nosso exemplo, usaremos apenas o [Exemplo de Análise de Varejo](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span><span class="sxs-lookup"><span data-stu-id="0e690-134">For our example, we'll just use the [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="0e690-135">Criar um espaço de trabalho do Power BI</span><span class="sxs-lookup"><span data-stu-id="0e690-135">Create a Power BI workspace</span></span>

<span data-ttu-id="0e690-136">Agora que o provisionamento foi feito, vamos começar a criar o espaço de trabalho de um cliente na coleção de espaços de trabalho por meio das APIs REST.</span><span class="sxs-lookup"><span data-stu-id="0e690-136">Now that the provisioning is all done, let’s get started creating a customer’s workspace in the workspace collection via REST APIs.</span></span> <span data-ttu-id="0e690-137">A seguinte Solicitação HTTP POST (REST) está criando o novo espaço de trabalho em nossa coleção de espaços de trabalho existente.</span><span class="sxs-lookup"><span data-stu-id="0e690-137">The following HTTP POST Request (REST) is creating the new workspace in our existing workspace collection.</span></span> <span data-ttu-id="0e690-138">Essa é a [API POST do Espaço de Trabalho](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="0e690-138">This is the [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="0e690-139">Em nosso exemplo, o nome da coleção de espaços de trabalho é **mypbiapp**.</span><span class="sxs-lookup"><span data-stu-id="0e690-139">In our example, the workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="0e690-140">Definimos apenas a tecla de acesso, que copiamos anteriormente, como **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="0e690-140">We just set the access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="0e690-141">A autenticação é muito simples!</span><span class="sxs-lookup"><span data-stu-id="0e690-141">It’s very simple authentication!</span></span>

<span data-ttu-id="0e690-142">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="0e690-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="0e690-143">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="0e690-143">**HTTP Response**</span></span>

```
HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces
RequestId: 4220d385-2fb3-406b-8901-4ebe11a5f6da

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/$metadata#workspaces/$entity",
  "workspaceId": "32960a09-6366-4208-a8bb-9e0678cdbb9d",
  "workspaceCollectionName": "mypbiapp"
}
```

<span data-ttu-id="0e690-144">A **workspaceId** retornada é usada para as chamadas à API subsequentes a seguir.</span><span class="sxs-lookup"><span data-stu-id="0e690-144">The returned **workspaceId** is used for the following subsequent API calls.</span></span> <span data-ttu-id="0e690-145">Nosso aplicativo deve manter esse valor.</span><span class="sxs-lookup"><span data-stu-id="0e690-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-the-workspace"></a><span data-ttu-id="0e690-146">Importar o arquivo .pbix no espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="0e690-146">Import .pbix file into the workspace</span></span>

<span data-ttu-id="0e690-147">Cada relatório num espaço de trabalho corresponde a um único arquivo do Power BI Desktop com um conjunto de dados \(incluindo configurações de fonte de dados).</span><span class="sxs-lookup"><span data-stu-id="0e690-147">Each report in a workspace corresponds to a single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="0e690-148">Podemos importar nosso arquivo .pbix no espaço de trabalho, conforme mostrado no código abaixo.</span><span class="sxs-lookup"><span data-stu-id="0e690-148">We can import our .pbix file to the workspace as shown in the code below.</span></span> <span data-ttu-id="0e690-149">Como você pode ver, podemos carregar o binário do arquivo .pbix usando diversas partes de MIME em http.</span><span class="sxs-lookup"><span data-stu-id="0e690-149">As you can see, we can upload the binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="0e690-150">O fragmento de uri **32960a09-6366-4208-a8bb-9e0678cdbb9d** é a workspaceId e o parâmetro de consulta **datasetDisplayName** é o nome do conjunto de dados a ser criado.</span><span class="sxs-lookup"><span data-stu-id="0e690-150">The uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is the workspaceId, and query parameter **datasetDisplayName** is the dataset name to create.</span></span> <span data-ttu-id="0e690-151">O conjunto de dados criado contém todos os artefatos relacionados aos dados no arquivo .pbix, como dados importados, o ponteiro para a fonte de dados etc.</span><span class="sxs-lookup"><span data-stu-id="0e690-151">The created dataset holds all data related artifacts in .pbix file such as imported data, the pointer to the data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{the content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="0e690-152">A execução dessa tarefa de importação pode demorar um pouco.</span><span class="sxs-lookup"><span data-stu-id="0e690-152">This import task might run for a while.</span></span> <span data-ttu-id="0e690-153">Quando concluída, nosso aplicativo poderá solicitar o status da tarefa usando a id de importação.</span><span class="sxs-lookup"><span data-stu-id="0e690-153">When complete, our application can ask the task status using import id.</span></span> <span data-ttu-id="0e690-154">Em nosso exemplo, a id de importação é **4eec64dd-533b-47c3-a72c-6508ad854659**.</span><span class="sxs-lookup"><span data-stu-id="0e690-154">In our example, the import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="0e690-155">Veja a seguir a solicitação de status usando essa id de importação:</span><span class="sxs-lookup"><span data-stu-id="0e690-155">The following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="0e690-156">Se a tarefa não for concluída, a resposta HTTP poderá ser parecida com esta:</span><span class="sxs-lookup"><span data-stu-id="0e690-156">If the task isn't complete, the HTTP response could be like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: 614a13a5-4de7-43e8-83c9-9cd225535136

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Publishing",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "name": "mydataset01"
}
```

<span data-ttu-id="0e690-157">Se a tarefa for concluída, a resposta HTTP poderá se parecer mais com isto:</span><span class="sxs-lookup"><span data-stu-id="0e690-157">If the task is complete, the HTTP response could be more like this:</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
RequestId: eb2c5a85-4d7d-4cc2-b0aa-0bafee4b1606

{
  "id": "4eec64dd-533b-47c3-a72c-6508ad854659",
  "importState": "Succeeded",
  "createdDateTime": "2016-07-19T07:36:06.227",
  "updatedDateTime": "2016-07-19T07:36:06.227",
  "reports": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://app.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c"
    }
  ],
  "datasets": [
    {
      "id": "458e0451-7215-4029-80b3-9627bf3417b0",
      "name": "mydataset01",
      "tables": [
      ],
      "webUrl": "https://app.powerbi.com/datasets/458e0451-7215-4029-80b3-9627bf3417b0"
    }
  ],
  "name": "mydataset01"
}
```

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="0e690-158">Conectividade da fonte de dados \(e multilocação de dados)</span><span class="sxs-lookup"><span data-stu-id="0e690-158">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="0e690-159">Embora quase todos os artefatos no arquivo .pbix sejam importados para nosso espaço de trabalho, as credenciais das fontes de dados não são.</span><span class="sxs-lookup"><span data-stu-id="0e690-159">While almost all of the artifacts in .pbix file are imported into our workspace, the  credentials for data sources are not.</span></span> <span data-ttu-id="0e690-160">Como resultado, ao usar o **modo DirectQuery**, o relatório inserido não poderá ser exibido corretamente.</span><span class="sxs-lookup"><span data-stu-id="0e690-160">As a result, when using **DirectQuery mode**, the embedded report cannot be shown correctly.</span></span> <span data-ttu-id="0e690-161">Mas, ao usar o **Modo de importação**, poderemos exibir o relatório usando os dados importados existentes.</span><span class="sxs-lookup"><span data-stu-id="0e690-161">But, when using **Import mode**, we can view the report using the existing imported data.</span></span> <span data-ttu-id="0e690-162">Nesse caso, devemos definir a credencial usando as etapas a seguir por meio das chamadas à REST.</span><span class="sxs-lookup"><span data-stu-id="0e690-162">In such a case, we must set the credential using the following steps via REST calls.</span></span>

<span data-ttu-id="0e690-163">Em primeiro lugar, devemos obter a fonte de dados do gateway.</span><span class="sxs-lookup"><span data-stu-id="0e690-163">First, we must get the gateway datasource.</span></span> <span data-ttu-id="0e690-164">Sabemos que a **id** do conjunto de dados é a id retornada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0e690-164">We know the dataset **id** is the previously returned id.</span></span>

<span data-ttu-id="0e690-165">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="0e690-165">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="0e690-166">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="0e690-166">**HTTP Response**</span></span>

```
GET HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: 574b0b18-a6fa-46a6-826c-e65840cf6e15

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#gatewayDatasources",
  "value": [
    {
      "id": "5f7ee2e7-4851-44a1-8b75-3eb01309d0ea",
      "gatewayId": "ca17e77f-1b51-429b-b059-6b3e3e9685d1",
      "datasourceType": "Sql",
      "connectionDetails": "{\"server\":\"testserver.database.windows.net\",\"database\":\"testdb01\"}"
    }
  ]
}
```

<span data-ttu-id="0e690-167">Usando a id de gateway retornada e a id da fonte de dados \(veja a **gatewayId** anterior e a **id** no resultado retornado), podemos mudar a credencial dessa fonte de dados como se segue:</span><span class="sxs-lookup"><span data-stu-id="0e690-167">Using the returned gateway id and datasource id \(see the previous **gatewayId** and **id** in the returned result), we can change the credential of this datasource as follows:</span></span>

<span data-ttu-id="0e690-168">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="0e690-168">**HTTP Request**</span></span>

```
PATCH https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/gateways/ca17e77f-1b51-429b-b059-6b3e3e9685d1/datasources/5f7ee2e7-4851-44a1-8b75-3eb01309d0ea
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "credentialType": "Basic",
  "basicCredentials": {
    "username": "demouser",
    "password": "P@ssw0rd"
  }
}
```

<span data-ttu-id="0e690-169">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="0e690-169">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="0e690-170">Em produção, também podemos definir a cadeia de conexão diferente para cada espaço de trabalho usando a API REST.</span><span class="sxs-lookup"><span data-stu-id="0e690-170">In production, we can also set the different connection string for each workspace using REST API.</span></span> <span data-ttu-id="0e690-171">\(ou seja, podemos separar o banco de dados para cada cliente.)</span><span class="sxs-lookup"><span data-stu-id="0e690-171">\(i.e, we can separate the database for each customers.)</span></span>

<span data-ttu-id="0e690-172">Veja a seguir a mudança da cadeia de conexão da fonte de dados por meio de REST.</span><span class="sxs-lookup"><span data-stu-id="0e690-172">The following is changing the connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="0e690-173">Ou, podemos usar a Segurança em Nível de Linha no Power BI Embedded e separar os dados para cada usuário em um relatório.</span><span class="sxs-lookup"><span data-stu-id="0e690-173">Or, we can use Row Level Security in Power BI Embedded and we can separate the data for each users in one report.</span></span> <span data-ttu-id="0e690-174">Consequentemente, podemos provisionar cada relatório de cliente com o mesmo .pbix \(interface de usuário etc.) e diferentes fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="0e690-174">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="0e690-175">Se você estiver usando o **Modo de importação** em vez do **Modo DirectQuery**, não há como atualizar os modelos por meio da API.</span><span class="sxs-lookup"><span data-stu-id="0e690-175">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way to refresh models via API.</span></span> <span data-ttu-id="0e690-176">As fontes de dados locais por meio do gateway do Power BI ainda não têm suporte no Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="0e690-176">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="0e690-177">No entanto, você vai querer realmente ficar de olho no [blog do Power BI](https://powerbi.microsoft.com/blog/) para saber das novidades e o que virá nas versões futuras.</span><span class="sxs-lookup"><span data-stu-id="0e690-177">However, you'll really want to keep an eye on the [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="0e690-178">Autenticação e hospedagem (inserção) de relatórios em nossa página da Web</span><span class="sxs-lookup"><span data-stu-id="0e690-178">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="0e690-179">Na API REST anterior, podemos usar a tecla de acesso **AppKey** em si como o cabeçalho da autorização.</span><span class="sxs-lookup"><span data-stu-id="0e690-179">In the previous REST API, we can use the access key **AppKey** itself as the authorization header.</span></span> <span data-ttu-id="0e690-180">Como essas chamadas podem ser tratadas no servidor back-end, ela é segura.</span><span class="sxs-lookup"><span data-stu-id="0e690-180">Because these calls can be handled on the backend server side, it's safe.</span></span>

<span data-ttu-id="0e690-181">Porém, quando inserimos o relatório em nossa página da Web, esse tipo de informação de segurança pode ser tratado usando JavaScript \(front-end).</span><span class="sxs-lookup"><span data-stu-id="0e690-181">But, when we embed the report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="0e690-182">Sendo assim, o valor do cabeçalho da autorização deve ser protegido.</span><span class="sxs-lookup"><span data-stu-id="0e690-182">Then the authorization header value must be secured.</span></span> <span data-ttu-id="0e690-183">Se nossa tecla de acesso for descoberta por um usuário ou código mal-intencionado, eles poderão chamar qualquer operação usando essa chave.</span><span class="sxs-lookup"><span data-stu-id="0e690-183">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="0e690-184">Quando inserimos o relatório em nossa página da Web, devemos usar o token calculado no lugar da tecla de acesso **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="0e690-184">When we embed the report in our web page, we must use the computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="0e690-185">Nosso aplicativo deve criar o Token Web JSON \(JWT) OAuth, que consiste em declarações e na assinatura digital calculada.</span><span class="sxs-lookup"><span data-stu-id="0e690-185">Our application must create the OAuth Json Web Token \(JWT) which consists of the claims and the computed digital signature.</span></span> <span data-ttu-id="0e690-186">Conforme ilustrado abaixo, este JWT OAuth são tokens de cadeia de caracteres codificados delimitados por ponto.</span><span class="sxs-lookup"><span data-stu-id="0e690-186">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="0e690-187">Primeiramente, devemos preparar o valor de entrada, que é assinado posteriormente.</span><span class="sxs-lookup"><span data-stu-id="0e690-187">First, we must prepare the input value, which is signed later.</span></span> <span data-ttu-id="0e690-188">Esse valor é a cadeia de caracteres (rfc4648) codificada da url em base64 do seguinte json, limitada pelo caractere de ponto \(.).</span><span class="sxs-lookup"><span data-stu-id="0e690-188">This value is the base64 url encoded (rfc4648) string of the following json, and these are delimited by the dot \(.) character.</span></span> <span data-ttu-id="0e690-189">Mais adiante, explicaremos como obter a identificação de relatório.</span><span class="sxs-lookup"><span data-stu-id="0e690-189">Later, we'll explain how to get the report id.</span></span>

> [!NOTE]
> <span data-ttu-id="0e690-190">Se quisermos usar RLS (Segurança em Nível de Linha) com o Power BI Embedded, também deveremos especificar **nome de usuário** e **funções** nas declarações.</span><span class="sxs-lookup"><span data-stu-id="0e690-190">If we want to use Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in the claims.</span></span>

```
{
  "typ":"JWT",
  "alg":"HS256"
}
```

```
{
  "wid":"{workspace id}",
  "rid":"{report id}",
  "wcn":"{workspace collection name}",
  "iss":"PowerBISDK",
  "ver":"0.2.0",
  "aud":"https://analysis.windows.net/powerbi/api",
  "nbf":{start time of token expiration},
  "exp":{end time of token expiration}
}
```

<span data-ttu-id="0e690-191">Em seguida, devemos criar a cadeia de caracteres codificada em base64 de HMAC \(a assinatura) com o algoritmo SHA256.</span><span class="sxs-lookup"><span data-stu-id="0e690-191">Next, we must create the base64 encoded string of HMAC \(the signature) with SHA256 algorithm.</span></span> <span data-ttu-id="0e690-192">Esse valor de entrada assinado é a cadeia de caracteres anterior.</span><span class="sxs-lookup"><span data-stu-id="0e690-192">This signed input value is the previous string.</span></span>

<span data-ttu-id="0e690-193">Por fim, devemos combinar o valor de entrada e a cadeia de caracteres de assinatura usando o caractere de ponto \(.).</span><span class="sxs-lookup"><span data-stu-id="0e690-193">Last, we must combine the input value and signature string using period \(.) character.</span></span> <span data-ttu-id="0e690-194">A cadeia de caracteres completa é o token de aplicativo para a inserção de relatório.</span><span class="sxs-lookup"><span data-stu-id="0e690-194">The completed string is the app token for the report embedding.</span></span> <span data-ttu-id="0e690-195">Mesmo se o token de aplicativo for descoberto por um usuário mal-intencionado, ele não poderá obter a tecla de acesso original.</span><span class="sxs-lookup"><span data-stu-id="0e690-195">Even if the app token is discovered by a malicious user, they cannot get the original access key.</span></span> <span data-ttu-id="0e690-196">Esse token de aplicativo vai expirar rapidamente.</span><span class="sxs-lookup"><span data-stu-id="0e690-196">This app token will expire quickly.</span></span>

<span data-ttu-id="0e690-197">Veja um exemplo de PHP para essas etapas:</span><span class="sxs-lookup"><span data-stu-id="0e690-197">Here's a PHP example for these steps:</span></span>

```
<?php
// 1. power bi access key
$accesskey = "MpaUgrTv5e...";

// 2. construct input value
$token1 = "{" .
  "\"typ\":\"JWT\"," .
  "\"alg\":\"HS256\"" .
  "}";
$token2 = "{" .
  "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
  "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
  "\"wcn\":\"mypbiapp\"," . // workspace collection name
  "\"iss\":\"PowerBISDK\"," .
  "\"ver\":\"0.2.0\"," .
  "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
  "\"nbf\":" . date("U") . "," .
  "\"exp\":" . date("U" , strtotime("+1 hour")) .
  "}";
$inputval = rfc4648_base64_encode($token1) .
  "." .
  rfc4648_base64_encode($token2);

// 3. get encoded signature
$hash = hash_hmac("sha256",
    $inputval,
    $accesskey,
    true);
$sig = rfc4648_base64_encode($hash);

// 4. show result (which is the apptoken)
$apptoken = $inputval . "." . $sig;
echo($apptoken);

// helper functions
function rfc4648_base64_encode($arg) {
  $res = $arg;
  $res = base64_encode($res);
  $res = str_replace("/", "_", $res);
  $res = str_replace("+", "-", $res);
  $res = rtrim($res, "=");
  return $res;
}
?>
```

## <a name="finally-embed-the-report-into-the-web-page"></a><span data-ttu-id="0e690-198">Por fim, inserir o relatório na página da Web</span><span class="sxs-lookup"><span data-stu-id="0e690-198">Finally, embed the report into the web page</span></span>

<span data-ttu-id="0e690-199">Para inserir nosso relatório, devemos obter a url inserida e a **id** do relatório usando a API REST a seguir.</span><span class="sxs-lookup"><span data-stu-id="0e690-199">For embedding our report, we must get the embed url and report **id** using the following REST API.</span></span>

<span data-ttu-id="0e690-200">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="0e690-200">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="0e690-201">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="0e690-201">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal; odata.streaming=true
RequestId: d4099022-405b-49d3-b3b7-3c60cf675958

{
  "@odata.context": "http://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/$metadata#reports",
  "value": [
    {
      "id": "2027efc6-a308-4632-a775-b9a9186f087c",
      "name": "mydataset01",
      "webUrl": "https://app.powerbi.com/reports/2027efc6-a308-4632-a775-b9a9186f087c",
      "embedUrl": "https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c",
      "isFromPbix": false
    }
  ]
}
```

<span data-ttu-id="0e690-202">Podemos inserir o relatório em nosso aplicativo Web usando o token de aplicativo anterior.</span><span class="sxs-lookup"><span data-stu-id="0e690-202">We can embed the report in our web app using the previous app token.</span></span>
<span data-ttu-id="0e690-203">Se observarmos o próximo código de exemplo, a primeira parte é a mesma do exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="0e690-203">If we look at the next sample code, the former part is the same as the previous example.</span></span> <span data-ttu-id="0e690-204">Na última parte, este exemplo mostra a **embedUrl** \(veja o resultado anterior) no iframe, que está postando o token de aplicativo no iframe.</span><span class="sxs-lookup"><span data-stu-id="0e690-204">In the latter part, this sample shows the **embedUrl** \(see the previous result) in the iframe, and is posting the app token into the iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="0e690-205">Você precisará alterar o valor da id de relatório para um dos seus valores.</span><span class="sxs-lookup"><span data-stu-id="0e690-205">You'll need to change the report id value to one of your own.</span></span> <span data-ttu-id="0e690-206">Além disso, devido a um bug em nosso sistema de gerenciamento de conteúdo, a marcação de iframe no exemplo de código é lida literalmente.</span><span class="sxs-lookup"><span data-stu-id="0e690-206">Also, due to a bug in our content management system, the iframe tag in the code sample is read literally.</span></span> <span data-ttu-id="0e690-207">Remova o texto limitado da marcação caso copie e cole esse código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="0e690-207">Remove the capped text from the tag if you copy and paste this sample code.</span></span>

```
    <?php
    // 1. power bi access key
    $accesskey = "MpaUgrTv5e...";

    // 2. construct input value
    $token1 = "{" .
      "\"typ\":\"JWT\"," .
      "\"alg\":\"HS256\"" .
      "}";
    $token2 = "{" .
      "\"wid\":\"32960a09-6366-4208-a8bb-9e0678cdbb9d\"," . // workspace id
      "\"rid\":\"2027efc6-a308-4632-a775-b9a9186f087c\"," . // report id
      "\"wcn\":\"mypbiapp\"," . // workspace collection name
      "\"iss\":\"PowerBISDK\"," .
      "\"ver\":\"0.2.0\"," .
      "\"aud\":\"https://analysis.windows.net/powerbi/api\"," .
      "\"nbf\":" . date("U") . "," .
      "\"exp\":" . date("U" , strtotime("+1 hour")) .
      "}";
    $inputval = rfc4648_base64_encode($token1) .
      "." .
      rfc4648_base64_encode($token2);

    // 3. get encoded signature value
    $hash = hash_hmac("sha256",
        $inputval,
        $accesskey,
        true);
    $sig = rfc4648_base64_encode($hash);

    // 4. get apptoken
    $apptoken = $inputval . "." . $sig;

    // helper functions
    function rfc4648_base64_encode($arg) {
      $res = $arg;
      $res = base64_encode($res);
      $res = str_replace("/", "_", $res);
      $res = str_replace("+", "-", $res);
      $res = rtrim($res, "=");
      return $res;
    }
    ?>
    <!DOCTYPE html>
    <html>
    <head>
      <meta charset="utf-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <title>Test page</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
    </head>
    <body>
      <button id="btnView">View Report !</button>
      <div id="divView">
        <**REMOVE THIS CAPPED TEXT IF COPIED** iframe id="ifrTile" width="100%" height="400"></iframe>
      </div>
      <script>
        (function () {
          document.getElementById('btnView').onclick = function() {
            var iframe = document.getElementById('ifrTile');
            iframe.src = 'https://embedded.powerbi.com/appTokenReportEmbed?reportId=2027efc6-a308-4632-a775-b9a9186f087c';
            iframe.onload = function() {
              var msgJson = {
                action: "loadReport",
                accessToken: "<?=$apptoken?>",
                height: 500,
                width: 722
              };
              var msgTxt = JSON.stringify(msgJson);
              iframe.contentWindow.postMessage(msgTxt, "*");
            };
          };
        }());
      </script>
    </body>
```

<span data-ttu-id="0e690-208">Aqui está nosso resultado:</span><span class="sxs-lookup"><span data-stu-id="0e690-208">And here's our result:</span></span>

![](media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="0e690-209">Neste momento, o Power BI Embedded mostra o relatório somente no iframe.</span><span class="sxs-lookup"><span data-stu-id="0e690-209">At this time, Power BI Embedded only shows the report in the iframe.</span></span> <span data-ttu-id="0e690-210">Mas, fique atento ao [Blog do Power BI](https://powerbi.microsoft.com/blog/).</span><span class="sxs-lookup"><span data-stu-id="0e690-210">But, keep an eye on the [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="0e690-211">Melhorias futuras poderão usar novas APIs do lado do cliente que nos permitirão enviar informações ao iframe, bem como removê-las.</span><span class="sxs-lookup"><span data-stu-id="0e690-211">Future improvements could use new client side APIs that will let us send information into the iframe as well as get information out.</span></span> <span data-ttu-id="0e690-212">Algo bem interessante!</span><span class="sxs-lookup"><span data-stu-id="0e690-212">Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="0e690-213">Confira também</span><span class="sxs-lookup"><span data-stu-id="0e690-213">See also</span></span>
* [<span data-ttu-id="0e690-214">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="0e690-214">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="0e690-215">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="0e690-215">More questions?</span></span> [<span data-ttu-id="0e690-216">Experimentar a comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="0e690-216">Try the Power BI Community</span></span>](http://community.powerbi.com/)

