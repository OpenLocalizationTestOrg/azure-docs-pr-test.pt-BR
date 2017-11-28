---
title: aaaHow toouse Power BI inserido com REST | Microsoft Docs
description: 'Saiba como toouse Power BI inserido com REST '
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
ms.openlocfilehash: 98057724e60ba868f9c93de8c50383569eb8852d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-power-bi-embedded-with-rest"></a><span data-ttu-id="34ae3-103">Como toouse Power BI inserido com REST</span><span class="sxs-lookup"><span data-stu-id="34ae3-103">How toouse Power BI Embedded with REST</span></span>

## <a name="power-bi-embedded-what-it-is-and-what-its-for"></a><span data-ttu-id="34ae3-104">Power BI Embedded: o que é e para que serve</span><span class="sxs-lookup"><span data-stu-id="34ae3-104">Power BI Embedded: What it is and what it's for</span></span>

<span data-ttu-id="34ae3-105">Uma visão geral do Power BI inserido é descrita em oficial Olá [site Power BI inserido](https://azure.microsoft.com/services/power-bi-embedded/), mas vamos dar uma olhada rápida antes de entrarmos em detalhes de saudação sobre usá-lo com REST.</span><span class="sxs-lookup"><span data-stu-id="34ae3-105">An overview of Power BI Embedded is described in hello official [Power BI Embedded site](https://azure.microsoft.com/services/power-bi-embedded/), but let's take a quick look before we get into hello details about using it with REST.</span></span>

<span data-ttu-id="34ae3-106">Ele é realmente bem simples.</span><span class="sxs-lookup"><span data-stu-id="34ae3-106">It's quite simple, really.</span></span> <span data-ttu-id="34ae3-107">Talvez você queira toouse visualizações de dados dinâmicos de saudação do [Power BI](https://powerbi.microsoft.com) em seu próprio aplicativo.</span><span class="sxs-lookup"><span data-stu-id="34ae3-107">you may want toouse hello dynamic data visualizations of [Power BI](https://powerbi.microsoft.com) in your own application.</span></span>

<span data-ttu-id="34ae3-108">A maioria dos aplicativos personalizada precisa toodeliver dados de saudação para seus próprios clientes, não necessariamente usuários em sua própria organização.</span><span class="sxs-lookup"><span data-stu-id="34ae3-108">Most custom applications need toodeliver hello data for their own customers, not necessarily users in their own organization.</span></span> <span data-ttu-id="34ae3-109">Por exemplo, se você estiver entregando algum serviço para a empresa e a empresa B, os usuários na empresa A deverão ver apenas dados de sua empresa A. Ou seja, multilocação Olá é necessária para a entrega de saudação.</span><span class="sxs-lookup"><span data-stu-id="34ae3-109">For example, if you're delivering some service for both company A and company B, users in company A should only see data for their own company A. That is, hello multi-tenancy is needed for hello delivery.</span></span>

<span data-ttu-id="34ae3-110">aplicativo personalizado Hello também pode oferecer seus próprios métodos de autenticação, como autenticação de formulários, autenticação básica, etc...</span><span class="sxs-lookup"><span data-stu-id="34ae3-110">hello custom application might also be offering its own authentication methods such as forms auth, basic auth, etc..</span></span> <span data-ttu-id="34ae3-111">Em seguida, Olá incorporação de solução deve colaborar com segurança com esse método de autenticação existente.</span><span class="sxs-lookup"><span data-stu-id="34ae3-111">Then, hello embedding solution must collaborate with this existing authentication methods safely.</span></span> <span data-ttu-id="34ae3-112">Também é necessário para os usuários toobe capaz de toouse os aplicativos ISV sem Olá extra compra ou licenciamento de uma assinatura do Power BI.</span><span class="sxs-lookup"><span data-stu-id="34ae3-112">It's also necessary for users toobe able toouse those ISV applications without hello extra purchase or licensing of a Power BI subscription.</span></span>

 <span data-ttu-id="34ae3-113">O **Power BI Embedded** foi desenvolvido exatamente para esses tipos de cenários.</span><span class="sxs-lookup"><span data-stu-id="34ae3-113">**Power BI Embedded** is designed for precisely these kinds of scenarios.</span></span> <span data-ttu-id="34ae3-114">Portanto, agora que temos Introdução rápida fora do modo de Olá, vamos falar alguns detalhes</span><span class="sxs-lookup"><span data-stu-id="34ae3-114">So, now that we have that quick introduction out of hello way, let's get into some details</span></span>

<span data-ttu-id="34ae3-115">Você pode usar o .NET Olá \(c#) ou Node. js SDK, tooeasily criar seu aplicativo com o Power BI inserido.</span><span class="sxs-lookup"><span data-stu-id="34ae3-115">You can use hello .NET \(C#) or Node.js SDK, tooeasily build your application with Power BI Embedded.</span></span> <span data-ttu-id="34ae3-116">Mas, neste artigo, explicaremos sobre o fluxo do HTTP \(incluindo AuthN) do Power BI sem SDKs.</span><span class="sxs-lookup"><span data-stu-id="34ae3-116">But, in this article, we'll explain about HTTP flow \(incl. AuthN) of Power BI without SDKs.</span></span> <span data-ttu-id="34ae3-117">Noções básicas sobre este fluxo, você pode criar seu aplicativo **com qualquer linguagem de programação**, e você pode entender profundamente essência de saudação do Power BI inserido.</span><span class="sxs-lookup"><span data-stu-id="34ae3-117">Understanding this flow, you can build your application **with any programming language**, and you can understand deeply hello essence of Power BI Embedded.</span></span>

## <a name="create-power-bi-workspace-collection-and-get-access-key-provisioning"></a><span data-ttu-id="34ae3-118">Criar a coleção de espaços de trabalho do Power BI e obter tecla de acesso \(provisionamento)</span><span class="sxs-lookup"><span data-stu-id="34ae3-118">Create Power BI workspace collection, and get access key \(Provisioning)</span></span>

<span data-ttu-id="34ae3-119">Power BI inserido é uma saudação em serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="34ae3-119">Power BI Embedded is one of hello Azure services.</span></span> <span data-ttu-id="34ae3-120">Olá somente ISV que usa o Portal do Azure é cobrado por taxas de uso \(por sessão de usuário por hora), e o usuário Olá que o relatório de saudação de modos de exibição não é carregada ou até mesmo exigir uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="34ae3-120">Only hello ISV who uses Azure Portal is charged for usage fees \(per hourly user session), and hello user who views hello report isn't charged or even require an Azure subscription.</span></span>
<span data-ttu-id="34ae3-121">Antes de iniciar o nosso desenvolvimento de aplicativo, é necessário criar hello **coleta de espaço de trabalho do Power BI** usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="34ae3-121">Before starting our application development, we must create hello **Power BI workspace collection** by using Azure Portal.</span></span>

<span data-ttu-id="34ae3-122">Cada espaço de trabalho do Power BI inserido é o espaço de trabalho de saudação para cada cliente (Locatário) e adicionamos vários espaços de trabalho em cada coleção de espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="34ae3-122">Each workspace of Power BI Embedded is hello workspace for each customer (tenant), and we can add many workspaces in each workspace collection.</span></span> <span data-ttu-id="34ae3-123">Olá a mesma chave de acesso é usado em cada coleção de espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="34ae3-123">hello same access key is used in each workspace collection.</span></span> <span data-ttu-id="34ae3-124">Em vigor, coleta de espaço de trabalho de saudação é o limite de segurança de saudação do Power BI inserido.</span><span class="sxs-lookup"><span data-stu-id="34ae3-124">In-effect, hello workspace collection is hello security boundary for Power BI Embedded.</span></span>

![](media/power-bi-embedded-iframe/create-workspace.png)

<span data-ttu-id="34ae3-125">Quando concluir a criação de coleção de espaço de trabalho hello, copie a chave de acesso de saudação do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="34ae3-125">When we finish creating hello workspace collection, copy hello access key from Azure Portal.</span></span>

![](media/power-bi-embedded-iframe/copy-access-key.png)

> [!NOTE]
> <span data-ttu-id="34ae3-126">Também podemos provisionar a coleção de espaço de trabalho hello e obter a chave de acesso por meio da API REST.</span><span class="sxs-lookup"><span data-stu-id="34ae3-126">We can also provision hello workspace collection and get access key via REST API.</span></span> <span data-ttu-id="34ae3-127">mais, consulte toolearn [APIs de provedor de recursos do Power BI](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="34ae3-127">toolearn more, see [Power BI Resource Provider APIs](https://msdn.microsoft.com/library/azure/mt712306.aspx).</span></span>

## <a name="create-pbix-file-with-power-bi-desktop"></a><span data-ttu-id="34ae3-128">Criar o arquivo .pbix com o Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="34ae3-128">Create .pbix file with Power BI Desktop</span></span>

<span data-ttu-id="34ae3-129">Em seguida, devemos criar conexão de dados hello e toobe relatórios inseridos.</span><span class="sxs-lookup"><span data-stu-id="34ae3-129">Next, we must create hello data connection and reports toobe embedded.</span></span>
<span data-ttu-id="34ae3-130">Para essa tarefa, não há programação nem código.</span><span class="sxs-lookup"><span data-stu-id="34ae3-130">For this task, there’s no programming or code.</span></span> <span data-ttu-id="34ae3-131">Vamos usar apenas o Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="34ae3-131">We just use Power BI Desktop.</span></span>
<span data-ttu-id="34ae3-132">Neste artigo, não entraremos detalhes Olá sobre como toouse Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="34ae3-132">In this article, we won't go through hello details about how toouse Power BI Desktop.</span></span> <span data-ttu-id="34ae3-133">Se precisar de ajuda aqui, confira [Introdução ao Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="34ae3-133">If you need some help here, see [Getting started with Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/).</span></span> <span data-ttu-id="34ae3-134">Para nosso exemplo, usaremos Olá [exemplo de análise de varejo](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span><span class="sxs-lookup"><span data-stu-id="34ae3-134">For our example, we'll just use hello [Retail Analysis Sample](https://powerbi.microsoft.com/documentation/powerbi-sample-datasets/).</span></span>

![](media/power-bi-embedded-iframe/power-bi-desktop-1.png)

## <a name="create-a-power-bi-workspace"></a><span data-ttu-id="34ae3-135">Criar um espaço de trabalho do Power BI</span><span class="sxs-lookup"><span data-stu-id="34ae3-135">Create a Power BI workspace</span></span>

<span data-ttu-id="34ae3-136">Agora que o provisionamento de saudação é feito, vamos começar a criar espaço de trabalho do cliente na coleção de espaço de trabalho Olá por meio de APIs REST.</span><span class="sxs-lookup"><span data-stu-id="34ae3-136">Now that hello provisioning is all done, let’s get started creating a customer’s workspace in hello workspace collection via REST APIs.</span></span> <span data-ttu-id="34ae3-137">Olá seguir HTTP POST de solicitação (REST) é criar novo espaço de trabalho de saudação no nosso conjunto de espaço de trabalho existente.</span><span class="sxs-lookup"><span data-stu-id="34ae3-137">hello following HTTP POST Request (REST) is creating hello new workspace in our existing workspace collection.</span></span> <span data-ttu-id="34ae3-138">Isso é hello [API do espaço de trabalho de POST](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="34ae3-138">This is hello [POST Workspace API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span> <span data-ttu-id="34ae3-139">Em nosso exemplo, o nome da coleção de espaço de trabalho Olá é **mypbiapp**.</span><span class="sxs-lookup"><span data-stu-id="34ae3-139">In our example, hello workspace collection name is **mypbiapp**.</span></span> <span data-ttu-id="34ae3-140">Que acabamos de definir chave de acesso hello, que são copiados anteriormente, como **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="34ae3-140">We just set hello access key, which we previously copied, as **AppKey**.</span></span> <span data-ttu-id="34ae3-141">A autenticação é muito simples!</span><span class="sxs-lookup"><span data-stu-id="34ae3-141">It’s very simple authentication!</span></span>

<span data-ttu-id="34ae3-142">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="34ae3-142">**HTTP Request**</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="34ae3-143">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="34ae3-143">**HTTP Response**</span></span>

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

<span data-ttu-id="34ae3-144">Olá retornado **workspaceId** é usado para Olá chamadas API subsequentes a seguir.</span><span class="sxs-lookup"><span data-stu-id="34ae3-144">hello returned **workspaceId** is used for hello following subsequent API calls.</span></span> <span data-ttu-id="34ae3-145">Nosso aplicativo deve manter esse valor.</span><span class="sxs-lookup"><span data-stu-id="34ae3-145">Our application must retain this value.</span></span>

## <a name="import-pbix-file-into-hello-workspace"></a><span data-ttu-id="34ae3-146">Importar o arquivo. pbix no espaço de trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="34ae3-146">Import .pbix file into hello workspace</span></span>

<span data-ttu-id="34ae3-147">Cada relatório em um espaço de trabalho corresponde tooa único arquivo de área de trabalho do Power BI com um conjunto de dados \(incluindo as configurações de fonte de dados).</span><span class="sxs-lookup"><span data-stu-id="34ae3-147">Each report in a workspace corresponds tooa single Power BI Desktop file with a dataset \(including datasource settings).</span></span> <span data-ttu-id="34ae3-148">Podemos importar nosso espaço de toohello do arquivo. pbix conforme mostrado no código de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="34ae3-148">We can import our .pbix file toohello workspace as shown in hello code below.</span></span> <span data-ttu-id="34ae3-149">Como você pode ver, podemos carregar binário de saudação do arquivo. pbix usando MIME de partes múltiplas em http.</span><span class="sxs-lookup"><span data-stu-id="34ae3-149">As you can see, we can upload hello binary of .pbix file using MIME multipart in http.</span></span>

<span data-ttu-id="34ae3-150">o fragmento de uri de saudação **32960a09-6366-4208-a8bb-9e0678cdbb9d** é workspaceId Olá e parâmetro de consulta **datasetDisplayName** é Olá toocreate de nome de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="34ae3-150">hello uri fragment **32960a09-6366-4208-a8bb-9e0678cdbb9d** is hello workspaceId, and query parameter **datasetDisplayName** is hello dataset name toocreate.</span></span> <span data-ttu-id="34ae3-151">Olá criado conjunto de dados contém todos os dados relacionados artefatos no arquivo. pbix como dados importados, Olá fonte de dados do ponteiro toohello, etc...</span><span class="sxs-lookup"><span data-stu-id="34ae3-151">hello created dataset holds all data related artifacts in .pbix file such as imported data, hello pointer toohello data source, etc..</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports?datasetDisplayName=mydataset01
Authorization: AppKey MpaUgrTv5e...
Content-Type: multipart/form-data; boundary="A300testx"

--A300testx
Content-Disposition: form-data

{hello content (binary) of .pbix file}
--A300testx--
```

<span data-ttu-id="34ae3-152">A execução dessa tarefa de importação pode demorar um pouco.</span><span class="sxs-lookup"><span data-stu-id="34ae3-152">This import task might run for a while.</span></span> <span data-ttu-id="34ae3-153">Ao concluir, nosso aplicativo pode solicitar o status da tarefa hello usando uma id de importação. Em nosso exemplo, a id de importação de saudação é **4eec64dd-533b-47c3-a72c-6508ad854659**.</span><span class="sxs-lookup"><span data-stu-id="34ae3-153">When complete, our application can ask hello task status using import id. In our example, hello import id is **4eec64dd-533b-47c3-a72c-6508ad854659**.</span></span>

```
HTTP/1.1 202 Accepted
Content-Type: application/json; charset=utf-8
Location: https://wabi-us-east2-redirect.analysis.windows.net/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659?tenantId=myorg
RequestId: 658bd6b4-b68d-4ec3-8818-2a94266dc220

{"id":"4eec64dd-533b-47c3-a72c-6508ad854659"}
```

<span data-ttu-id="34ae3-154">a seguir Hello está solicitando status com essa id de importação:</span><span class="sxs-lookup"><span data-stu-id="34ae3-154">hello following is asking status using this import id:</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/imports/4eec64dd-533b-47c3-a72c-6508ad854659
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="34ae3-155">Se a tarefa de saudação não for concluída, Olá resposta HTTP poderia ser assim:</span><span class="sxs-lookup"><span data-stu-id="34ae3-155">If hello task isn't complete, hello HTTP response could be like this:</span></span>

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

<span data-ttu-id="34ae3-156">Se Olá tarefa estiver concluída, Olá resposta HTTP pode ser mais parecida com isto:</span><span class="sxs-lookup"><span data-stu-id="34ae3-156">If hello task is complete, hello HTTP response could be more like this:</span></span>

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

## <a name="data-source-connectivity-and-multi-tenancy-of-data"></a><span data-ttu-id="34ae3-157">Conectividade da fonte de dados \(e multilocação de dados)</span><span class="sxs-lookup"><span data-stu-id="34ae3-157">Data source connectivity \(and multi-tenancy of data)</span></span>

<span data-ttu-id="34ae3-158">Enquanto quase todos os artefatos de saudação no arquivo. pbix são importados para nosso espaço de trabalho, Olá para fontes de dados não são credenciais.</span><span class="sxs-lookup"><span data-stu-id="34ae3-158">While almost all of hello artifacts in .pbix file are imported into our workspace, hello  credentials for data sources are not.</span></span> <span data-ttu-id="34ae3-159">Como resultado, ao usar **o modo DirectQuery**, hello incorporados não podem ser exibidos corretamente.</span><span class="sxs-lookup"><span data-stu-id="34ae3-159">As a result, when using **DirectQuery mode**, hello embedded report cannot be shown correctly.</span></span> <span data-ttu-id="34ae3-160">Mas, ao usar **modo de importação**, é possível exibir o relatório de hello usando dados importados existentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="34ae3-160">But, when using **Import mode**, we can view hello report using hello existing imported data.</span></span> <span data-ttu-id="34ae3-161">Nesse caso, é necessário definir as credenciais de Olá usando as etapas a seguir por meio de chamadas REST de saudação.</span><span class="sxs-lookup"><span data-stu-id="34ae3-161">In such a case, we must set hello credential using hello following steps via REST calls.</span></span>

<span data-ttu-id="34ae3-162">Primeiro, devemos obter Olá gateway datasource.</span><span class="sxs-lookup"><span data-stu-id="34ae3-162">First, we must get hello gateway datasource.</span></span> <span data-ttu-id="34ae3-163">Sabemos que o conjunto de dados de saudação **id** é Olá anteriormente retornado id.</span><span class="sxs-lookup"><span data-stu-id="34ae3-163">We know hello dataset **id** is hello previously returned id.</span></span>

<span data-ttu-id="34ae3-164">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="34ae3-164">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.GetBoundGatewayDatasources
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="34ae3-165">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="34ae3-165">**HTTP Response**</span></span>

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

<span data-ttu-id="34ae3-166">Usando hello retornadas id de gateway e id de fonte de dados \(consulte Olá anterior **gatewayId** e **id** Olá retornou resultados), é possível alterar a credencial de saudação desta fonte de dados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="34ae3-166">Using hello returned gateway id and datasource id \(see hello previous **gatewayId** and **id** in hello returned result), we can change hello credential of this datasource as follows:</span></span>

<span data-ttu-id="34ae3-167">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="34ae3-167">**HTTP Request**</span></span>

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

<span data-ttu-id="34ae3-168">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="34ae3-168">**HTTP Response**</span></span>

```
HTTP/1.1 200 OK
Content-Type: application/octet-stream
RequestId: 0e533c13-266a-4a9d-8718-fdad90391099
```

<span data-ttu-id="34ae3-169">Em produção, também podemos definir cadeia de caracteres de conexão diferentes de saudação para cada espaço de trabalho usando a API REST.</span><span class="sxs-lookup"><span data-stu-id="34ae3-169">In production, we can also set hello different connection string for each workspace using REST API.</span></span> <span data-ttu-id="34ae3-170">\(ou seja, poderá Separamos banco de dados de saudação para cada cliente.)</span><span class="sxs-lookup"><span data-stu-id="34ae3-170">\(i.e, we can separate hello database for each customers.)</span></span>

<span data-ttu-id="34ae3-171">seguir Hello está mudando a cadeia de caracteres de conexão de saudação da fonte de dados por meio do REST.</span><span class="sxs-lookup"><span data-stu-id="34ae3-171">hello following is changing hello connection string of datasource via REST.</span></span>

```
POST https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/datasets/458e0451-7215-4029-80b3-9627bf3417b0/Default.SetAllConnections
Authorization: AppKey MpaUgrTv5e...
Content-Type: application/json; charset=utf-8

{
  "connectionString": "data source=testserver02.database.windows.net;initial catalog=testdb02;persist security info=True;encrypt=True;trustservercertificate=False"
}
```

<span data-ttu-id="34ae3-172">Ou, podemos usar segurança em nível de linha no Power BI inserido e é possível separar dados de Olá para cada usuário em um relatório.</span><span class="sxs-lookup"><span data-stu-id="34ae3-172">Or, we can use Row Level Security in Power BI Embedded and we can separate hello data for each users in one report.</span></span> <span data-ttu-id="34ae3-173">Consequentemente, podemos provisionar cada relatório de cliente com o mesmo .pbix \(interface de usuário etc.) e diferentes fontes de dados.</span><span class="sxs-lookup"><span data-stu-id="34ae3-173">As a result, we can provision each customer report with same .pbix \(UI, etc.) and different data sources.</span></span>

> [!NOTE]
> <span data-ttu-id="34ae3-174">Se você estiver usando **modo de importação** em vez de **o modo DirectQuery**, não há nenhum modelo de toorefresh de maneira por meio da API.</span><span class="sxs-lookup"><span data-stu-id="34ae3-174">If you’re using **Import mode** instead of **DirectQuery mode**, there’s no way toorefresh models via API.</span></span> <span data-ttu-id="34ae3-175">As fontes de dados locais por meio do gateway do Power BI ainda não têm suporte no Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="34ae3-175">And, on-premises datasources through Power BI gateway isn't yet supported in Power BI Embedded.</span></span> <span data-ttu-id="34ae3-176">No entanto, você vai realmente deseja tookeep atento Olá [blog do Power BI](https://powerbi.microsoft.com/blog/) para os quais são as novidades e quais são as novidades em futuras versões.</span><span class="sxs-lookup"><span data-stu-id="34ae3-176">However, you'll really want tookeep an eye on hello [Power BI blog](https://powerbi.microsoft.com/blog/) for what's new and what's coming in future releases.</span></span>

## <a name="authentication-and-hosting-embedding-reports-in-our-web-page"></a><span data-ttu-id="34ae3-177">Autenticação e hospedagem (inserção) de relatórios em nossa página da Web</span><span class="sxs-lookup"><span data-stu-id="34ae3-177">Authentication and hosting (embedding) reports in our web page</span></span>

<span data-ttu-id="34ae3-178">Em Olá anterior API de REST, podemos usar chave de acesso Olá **AppKey** a próprio como cabeçalho de autorização de saudação.</span><span class="sxs-lookup"><span data-stu-id="34ae3-178">In hello previous REST API, we can use hello access key **AppKey** itself as hello authorization header.</span></span> <span data-ttu-id="34ae3-179">Como essas chamadas podem ser tratadas no lado do servidor de back-end Olá, é seguro.</span><span class="sxs-lookup"><span data-stu-id="34ae3-179">Because these calls can be handled on hello backend server side, it's safe.</span></span>

<span data-ttu-id="34ae3-180">Mas, quando é inserir o relatório de saudação em nossa página da web, esse tipo de informação de segurança deve ser manipulado usando JavaScript \(front-end).</span><span class="sxs-lookup"><span data-stu-id="34ae3-180">But, when we embed hello report in our web page, this kind of security information would be handled using JavaScript \(frontend).</span></span> <span data-ttu-id="34ae3-181">Em seguida, o valor de cabeçalho de autorização Olá deve ser protegido.</span><span class="sxs-lookup"><span data-stu-id="34ae3-181">Then hello authorization header value must be secured.</span></span> <span data-ttu-id="34ae3-182">Se nossa tecla de acesso for descoberta por um usuário ou código mal-intencionado, eles poderão chamar qualquer operação usando essa chave.</span><span class="sxs-lookup"><span data-stu-id="34ae3-182">If our access key is discovered by a malicious user or malicious code, they can call any operations using this key.</span></span>

<span data-ttu-id="34ae3-183">Quando podemos inserir o relatório de saudação em nossa página da web, devem usar token computada Olá em vez de chave de acesso **AppKey**.</span><span class="sxs-lookup"><span data-stu-id="34ae3-183">When we embed hello report in our web page, we must use hello computed token instead of access key **AppKey**.</span></span> <span data-ttu-id="34ae3-184">Nosso aplicativo crie Olá OAuth Json Web Token \(JWT) que consiste em declarações hello e assinatura digital computada de saudação.</span><span class="sxs-lookup"><span data-stu-id="34ae3-184">Our application must create hello OAuth Json Web Token \(JWT) which consists of hello claims and hello computed digital signature.</span></span> <span data-ttu-id="34ae3-185">Conforme ilustrado abaixo, este JWT OAuth são tokens de cadeia de caracteres codificados delimitados por ponto.</span><span class="sxs-lookup"><span data-stu-id="34ae3-185">As illustrated below, this OAuth JWT is dot-delimited encoded string tokens.</span></span>

![](media/power-bi-embedded-iframe/oauth-jwt.png)

<span data-ttu-id="34ae3-186">Primeiro, é necessário preparar o valor de entrada hello, que é assinado posteriormente.</span><span class="sxs-lookup"><span data-stu-id="34ae3-186">First, we must prepare hello input value, which is signed later.</span></span> <span data-ttu-id="34ae3-187">Esse valor é cadeia de caracteres do hello base64 codificados de url (rfc4648) de saudação json a seguir, e esses são delimitadas por ponto Olá \(.) caracteres.</span><span class="sxs-lookup"><span data-stu-id="34ae3-187">This value is hello base64 url encoded (rfc4648) string of hello following json, and these are delimited by hello dot \(.) character.</span></span> <span data-ttu-id="34ae3-188">Posteriormente, explicaremos como tooget Olá id do relatório.</span><span class="sxs-lookup"><span data-stu-id="34ae3-188">Later, we'll explain how tooget hello report id.</span></span>

> [!NOTE]
> <span data-ttu-id="34ae3-189">Se quisermos toouse linha nível RLS (segurança) com o Power BI inserido, podemos também deve especificar **username** e **funções** em declarações de saudação.</span><span class="sxs-lookup"><span data-stu-id="34ae3-189">If we want toouse Row Level Security (RLS) with Power BI Embedded, we must also specify **username** and **roles** in hello claims.</span></span>

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

<span data-ttu-id="34ae3-190">Em seguida, é necessário criar a cadeia de caracteres codificada em base64 de Olá de HMAC \(assinatura Olá) com o algoritmo SHA256.</span><span class="sxs-lookup"><span data-stu-id="34ae3-190">Next, we must create hello base64 encoded string of HMAC \(hello signature) with SHA256 algorithm.</span></span> <span data-ttu-id="34ae3-191">Esse valor com sinal de entrada é cadeia de caracteres de saudação anterior.</span><span class="sxs-lookup"><span data-stu-id="34ae3-191">This signed input value is hello previous string.</span></span>

<span data-ttu-id="34ae3-192">Por último, podemos deve combinar o valor de entrada hello e cadeia de caracteres de assinatura usando o período \(.) caracteres.</span><span class="sxs-lookup"><span data-stu-id="34ae3-192">Last, we must combine hello input value and signature string using period \(.) character.</span></span> <span data-ttu-id="34ae3-193">cadeia de caracteres de saudação concluída é token de aplicativo Olá Olá incorporação de relatório.</span><span class="sxs-lookup"><span data-stu-id="34ae3-193">hello completed string is hello app token for hello report embedding.</span></span> <span data-ttu-id="34ae3-194">Mesmo se o token de aplicativo hello for descoberto por um usuário mal-intencionado, eles não é possível obter a chave de acesso original hello.</span><span class="sxs-lookup"><span data-stu-id="34ae3-194">Even if hello app token is discovered by a malicious user, they cannot get hello original access key.</span></span> <span data-ttu-id="34ae3-195">Esse token de aplicativo vai expirar rapidamente.</span><span class="sxs-lookup"><span data-stu-id="34ae3-195">This app token will expire quickly.</span></span>

<span data-ttu-id="34ae3-196">Veja um exemplo de PHP para essas etapas:</span><span class="sxs-lookup"><span data-stu-id="34ae3-196">Here's a PHP example for these steps:</span></span>

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

// 4. show result (which is hello apptoken)
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

## <a name="finally-embed-hello-report-into-hello-web-page"></a><span data-ttu-id="34ae3-197">Por fim, inserir o relatório de saudação na página da web de saudação</span><span class="sxs-lookup"><span data-stu-id="34ae3-197">Finally, embed hello report into hello web page</span></span>

<span data-ttu-id="34ae3-198">Para inserir nosso relatório, devemos obter Olá inserir a url e o relatório **id** usando Olá API REST a seguir.</span><span class="sxs-lookup"><span data-stu-id="34ae3-198">For embedding our report, we must get hello embed url and report **id** using hello following REST API.</span></span>

<span data-ttu-id="34ae3-199">**Solicitação HTTP**</span><span class="sxs-lookup"><span data-stu-id="34ae3-199">**HTTP Request**</span></span>

```
GET https://api.powerbi.com/v1.0/collections/mypbiapp/workspaces/32960a09-6366-4208-a8bb-9e0678cdbb9d/reports
Authorization: AppKey MpaUgrTv5e...
```

<span data-ttu-id="34ae3-200">**Resposta HTTP**</span><span class="sxs-lookup"><span data-stu-id="34ae3-200">**HTTP Response**</span></span>

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

<span data-ttu-id="34ae3-201">Podemos pode inserir o relatório de saudação em nosso aplicativo web usando o token de aplicativo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="34ae3-201">We can embed hello report in our web app using hello previous app token.</span></span>
<span data-ttu-id="34ae3-202">Se observarmos próximo código de exemplo hello, parte anterior Olá é Olá igual ao exemplo anterior hello.</span><span class="sxs-lookup"><span data-stu-id="34ae3-202">If we look at hello next sample code, hello former part is hello same as hello previous example.</span></span> <span data-ttu-id="34ae3-203">Na última parte de hello, este exemplo mostra Olá **embedUrl** \(consulte resultado anterior Olá) Olá iframe e está enviando o token de aplicativo hello em Olá iframe.</span><span class="sxs-lookup"><span data-stu-id="34ae3-203">In hello latter part, this sample shows hello **embedUrl** \(see hello previous result) in hello iframe, and is posting hello app token into hello iframe.</span></span>

> [!NOTE]
> <span data-ttu-id="34ae3-204">Você precisará toochange Olá relatório id valor tooone de sua preferência.</span><span class="sxs-lookup"><span data-stu-id="34ae3-204">You'll need toochange hello report id value tooone of your own.</span></span> <span data-ttu-id="34ae3-205">Além disso, devido a erro de tooa em nosso sistema de gerenciamento de conteúdo, marca iframe de saudação no exemplo de código Olá é leitura literalmente.</span><span class="sxs-lookup"><span data-stu-id="34ae3-205">Also, due tooa bug in our content management system, hello iframe tag in hello code sample is read literally.</span></span> <span data-ttu-id="34ae3-206">Remova o texto de saudação limitado de marca de saudação se você copiar e colar esse código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="34ae3-206">Remove hello capped text from hello tag if you copy and paste this sample code.</span></span>

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

<span data-ttu-id="34ae3-207">Aqui está nosso resultado:</span><span class="sxs-lookup"><span data-stu-id="34ae3-207">And here's our result:</span></span>

![](media/power-bi-embedded-iframe/view-report.png)

<span data-ttu-id="34ae3-208">Neste momento, Power BI inserido mostra apenas relatório Olá em Olá iframe.</span><span class="sxs-lookup"><span data-stu-id="34ae3-208">At this time, Power BI Embedded only shows hello report in hello iframe.</span></span> <span data-ttu-id="34ae3-209">Mas, fique atento Olá [Blog do Power BI](https://powerbi.microsoft.com/blog/).</span><span class="sxs-lookup"><span data-stu-id="34ae3-209">But, keep an eye on hello [Power BI Blog](https://powerbi.microsoft.com/blog/).</span></span> <span data-ttu-id="34ae3-210">Melhorias futuras podem usar o novo cliente APIs que será vamos enviar informações em iframe Olá além de transmitir informações. Algo bem interessante!</span><span class="sxs-lookup"><span data-stu-id="34ae3-210">Future improvements could use new client side APIs that will let us send information into hello iframe as well as get information out. Exciting stuff!</span></span>

## <a name="see-also"></a><span data-ttu-id="34ae3-211">Confira também</span><span class="sxs-lookup"><span data-stu-id="34ae3-211">See also</span></span>
* [<span data-ttu-id="34ae3-212">Autenticando e autorizando com o Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="34ae3-212">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)

<span data-ttu-id="34ae3-213">Mais perguntas?</span><span class="sxs-lookup"><span data-stu-id="34ae3-213">More questions?</span></span> [<span data-ttu-id="34ae3-214">Tente Olá comunidade do Power BI</span><span class="sxs-lookup"><span data-stu-id="34ae3-214">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

