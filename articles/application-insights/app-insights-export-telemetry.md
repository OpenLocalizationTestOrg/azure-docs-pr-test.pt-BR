---
title: "exportação de aaaContinuous de telemetria do Application Insights | Microsoft Docs"
description: "Exportar toostorage de dados de diagnóstico e de uso no Microsoft Azure e baixá-lo de lá."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: bwren
ms.openlocfilehash: be9ed7e05922c1c8186df9ca4e642862adaa5fd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="c18ec-103">Exportar telemetria do Application Insights</span><span class="sxs-lookup"><span data-stu-id="c18ec-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="c18ec-104">Deseja tookeep sua telemetria por mais de um período de retenção padrão de Olá?</span><span class="sxs-lookup"><span data-stu-id="c18ec-104">Want tookeep your telemetry for longer than hello standard retention period?</span></span> <span data-ttu-id="c18ec-105">Ou processá-la de alguma forma especializada?</span><span class="sxs-lookup"><span data-stu-id="c18ec-105">Or process it in some specialized way?</span></span> <span data-ttu-id="c18ec-106">Exportação contínua é ideal para isso.</span><span class="sxs-lookup"><span data-stu-id="c18ec-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="c18ec-107">Olá eventos no portal do Application Insights Olá podem ser exportado toostorage no Microsoft Azure no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="c18ec-107">hello events you see in hello Application Insights portal can be exported toostorage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="c18ec-108">A partir daí, você pode baixar o seus dados e gravar qualquer código que você precisa tooprocess-lo.</span><span class="sxs-lookup"><span data-stu-id="c18ec-108">From there you can download your data and write whatever code you need tooprocess it.</span></span>  

<span data-ttu-id="c18ec-109">Usar a exportação contínua pode incorrer em um custo adicional.</span><span class="sxs-lookup"><span data-stu-id="c18ec-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="c18ec-110">Verifique o [modelo de preços](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="c18ec-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="c18ec-111">Antes de configurar a exportação contínua, há algumas alternativas que talvez você queira tooconsider:</span><span class="sxs-lookup"><span data-stu-id="c18ec-111">Before you set up continuous export, there are some alternatives you might want tooconsider:</span></span>

* <span data-ttu-id="c18ec-112">botão de exportação de saudação na parte superior de saudação da folha de métricas ou pesquisar permite transferir tabelas e gráficos tooan planilha do Excel.</span><span class="sxs-lookup"><span data-stu-id="c18ec-112">hello Export button at hello top of a metrics or search blade lets you transfer tables and charts tooan Excel spreadsheet.</span></span>

* <span data-ttu-id="c18ec-113">O [Analytics](app-insights-analytics.md) fornece uma linguagem de consulta eficiente para telemetria.</span><span class="sxs-lookup"><span data-stu-id="c18ec-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="c18ec-114">Ele também pode exportar os resultados.</span><span class="sxs-lookup"><span data-stu-id="c18ec-114">It can also export results.</span></span>
* <span data-ttu-id="c18ec-115">Se você estiver procurando muito[explorar seus dados no Power BI](app-insights-export-power-bi.md), você pode fazer isso sem usar a exportação contínua.</span><span class="sxs-lookup"><span data-stu-id="c18ec-115">If you're looking too[explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="c18ec-116">Olá [API REST de acesso a dados](https://dev.applicationinsights.io/) permite que você acesse sua telemetria programaticamente.</span><span class="sxs-lookup"><span data-stu-id="c18ec-116">hello [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="c18ec-117">Após a exportação contínua copia o toostorage de dados (onde ele pode permanecer para desde que você deseja), ele ainda está disponível no Application Insights para saudação normal [período de retenção](app-insights-data-retention-privacy.md).</span><span class="sxs-lookup"><span data-stu-id="c18ec-117">After Continuous Export copies your data toostorage (where it can stay for as long as you like), it's still available in Application Insights for hello usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="c18ec-118"><a name="setup"></a> Criar uma Exportação Contínua</span><span class="sxs-lookup"><span data-stu-id="c18ec-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="c18ec-119">No hello recurso do Application Insights para seu aplicativo, abra a exportação contínua e escolha **adicionar**:</span><span class="sxs-lookup"><span data-stu-id="c18ec-119">In hello Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![Role para baixo e clique em Exportação contínua](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="c18ec-121">Escolha os tipos de dados de telemetria Olá tooexport desejado.</span><span class="sxs-lookup"><span data-stu-id="c18ec-121">Choose hello telemetry data types you want tooexport.</span></span>

3. <span data-ttu-id="c18ec-122">Crie ou selecione um [conta de armazenamento do Azure](../storage/common/storage-introduction.md) onde você deseja toostore Olá dados.</span><span class="sxs-lookup"><span data-stu-id="c18ec-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want toostore hello data.</span></span>

    > [!Warning]
    > <span data-ttu-id="c18ec-123">Por padrão, o local de armazenamento Olá será definido toohello mesma região geográfica que o recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c18ec-123">By default, hello storage location will be set toohello same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="c18ec-124">Armazenar em uma região diferente poderá incorrer em encargos de transferência.</span><span class="sxs-lookup"><span data-stu-id="c18ec-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![Clique em Adicionar, Destino de exportação, Conta de armazenamento e, em seguida, crie um novo repositório ou escolha um repositório existente](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="c18ec-126">Crie ou selecione um contêiner no armazenamento de saudação:</span><span class="sxs-lookup"><span data-stu-id="c18ec-126">Create or select a container in hello storage:</span></span>

    ![Clique em Escolher tipos de evento](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="c18ec-128">Depois de criar sua exportação, ela começa a ser realizada.</span><span class="sxs-lookup"><span data-stu-id="c18ec-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="c18ec-129">Você somente obtém dados que chega depois de criar a exportação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c18ec-129">You only get data that arrives after you create hello export.</span></span>

<span data-ttu-id="c18ec-130">Pode haver um atraso de aproximadamente uma hora antes de dados aparecem no armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="c18ec-130">There can be a delay of about an hour before data appears in hello storage.</span></span>

### <a name="tooedit-continuous-export"></a><span data-ttu-id="c18ec-131">exportação contínua tooedit</span><span class="sxs-lookup"><span data-stu-id="c18ec-131">tooedit continuous export</span></span>

<span data-ttu-id="c18ec-132">Se você quiser que tipos de evento toochange hello mais tarde, basta editar Olá exportação:</span><span class="sxs-lookup"><span data-stu-id="c18ec-132">If you want toochange hello event types later, just edit hello export:</span></span>

![Clique em Escolher tipos de evento](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a><span data-ttu-id="c18ec-134">exportação contínua toostop</span><span class="sxs-lookup"><span data-stu-id="c18ec-134">toostop continuous export</span></span>

<span data-ttu-id="c18ec-135">exportação de saudação toostop, clique em Desabilitar.</span><span class="sxs-lookup"><span data-stu-id="c18ec-135">toostop hello export, click Disable.</span></span> <span data-ttu-id="c18ec-136">Quando você clica em habilitar novamente, exportação Olá reiniciará com novos dados.</span><span class="sxs-lookup"><span data-stu-id="c18ec-136">When you click Enable again, hello export will restart with new data.</span></span> <span data-ttu-id="c18ec-137">Você não obterá dados Olá que chegaram no portal de saudação enquanto a exportação foi desabilitada.</span><span class="sxs-lookup"><span data-stu-id="c18ec-137">You won't get hello data that arrived in hello portal while export was disabled.</span></span>

<span data-ttu-id="c18ec-138">exportação de saudação toostop permanentemente, exclua-o.</span><span class="sxs-lookup"><span data-stu-id="c18ec-138">toostop hello export permanently, delete it.</span></span> <span data-ttu-id="c18ec-139">Isso não exclui seus dados do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c18ec-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="c18ec-140">Não consegue adicionar nem alterar uma exportação?</span><span class="sxs-lookup"><span data-stu-id="c18ec-140">Can't add or change an export?</span></span>
* <span data-ttu-id="c18ec-141">tooadd ou alteração de exportação, você precisa ter direitos de acesso de proprietário, colaborador ou colaborador do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c18ec-141">tooadd or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="c18ec-142">[Saiba mais sobre as funções][roles].</span><span class="sxs-lookup"><span data-stu-id="c18ec-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="c18ec-143"><a name="analyze"></a> Quais eventos você recebe?</span><span class="sxs-lookup"><span data-stu-id="c18ec-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="c18ec-144">Olá dados exportados são brutos de telemetria Olá que recebemos do seu aplicativo, exceto que podemos adicionar dados de local que calculamos do endereço IP de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="c18ec-144">hello exported data is hello raw telemetry we receive from your application, except that we add location data which we calculate from hello client IP address.</span></span>

<span data-ttu-id="c18ec-145">Dados que já foi descartados pelo [amostragem](app-insights-sampling.md) não está incluído nos dados hello exportada.</span><span class="sxs-lookup"><span data-stu-id="c18ec-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in hello exported data.</span></span>

<span data-ttu-id="c18ec-146">Outras métricas calculadas não são incluídas.</span><span class="sxs-lookup"><span data-stu-id="c18ec-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="c18ec-147">Por exemplo, podemos não exportar a utilização média de CPU, mas podemos exportar telemetria bruto de saudação do qual a média de saudação é computada.</span><span class="sxs-lookup"><span data-stu-id="c18ec-147">For example, we don't export average CPU utilisation, but we do export hello raw telemetry from which hello average is computed.</span></span>

<span data-ttu-id="c18ec-148">Olá dados também incluem Olá resultados de qualquer [testes da web de disponibilidade](app-insights-monitor-web-app-availability.md) que você configurou.</span><span class="sxs-lookup"><span data-stu-id="c18ec-148">hello data also includes hello results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="c18ec-149">**Amostragem.**</span><span class="sxs-lookup"><span data-stu-id="c18ec-149">**Sampling.**</span></span> <span data-ttu-id="c18ec-150">Se seu aplicativo envia um lote de dados, o recurso de amostragem de saudação pode operar e enviar somente uma fração de telemetria Olá gerado.</span><span class="sxs-lookup"><span data-stu-id="c18ec-150">If your application sends a lot of data, hello sampling feature may operate and send only a fraction of hello generated telemetry.</span></span> [<span data-ttu-id="c18ec-151">Saiba mais sobre amostragem.</span><span class="sxs-lookup"><span data-stu-id="c18ec-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="c18ec-152"><a name="get"></a>Inspecionar dados Olá</span><span class="sxs-lookup"><span data-stu-id="c18ec-152"><a name="get"></a> Inspect hello data</span></span>
<span data-ttu-id="c18ec-153">Você pode inspecionar o armazenamento de saudação diretamente no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="c18ec-153">You can inspect hello storage directly in hello portal.</span></span> <span data-ttu-id="c18ec-154">Clique em **Procurar**, selecione sua conta de armazenamento e abra **Contêineres**.</span><span class="sxs-lookup"><span data-stu-id="c18ec-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="c18ec-155">tooinspect armazenamento do Azure no Visual Studio, abra **exibição**, **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="c18ec-155">tooinspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="c18ec-156">(Se você não tiver esse comando de menu, você precisa tooinstall Olá SDK do Azure: Olá abrir **novo projeto** caixa de diálogo, expanda Visual c# / nuvem e escolha **obter o Microsoft Azure SDK para .NET**.)</span><span class="sxs-lookup"><span data-stu-id="c18ec-156">(If you don't have that menu command, you need tooinstall hello Azure SDK: Open hello **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="c18ec-157">Quando você abrir o armazenamento de blob, verá um contêiner com um conjunto de arquivos de blob.</span><span class="sxs-lookup"><span data-stu-id="c18ec-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="c18ec-158">Olá URI de cada arquivo derivado de seu nome de recurso do Application Insights, sua chave de instrumentação, telemetria-tipo/Data/hora.</span><span class="sxs-lookup"><span data-stu-id="c18ec-158">hello URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="c18ec-159">(nome de recurso Olá contém letras minúscula e chave de instrumentação Olá omite traços.)</span><span class="sxs-lookup"><span data-stu-id="c18ec-159">(hello resource name is all lowercase, and hello instrumentation key omits dashes.)</span></span>

![Inspecione o armazenamento de blob Olá com uma ferramenta adequada](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="c18ec-161">saudação de data e hora são UTC e quando telemetria Olá foi depositada no armazenamento Olá - tempo de saudação não foi gerado.</span><span class="sxs-lookup"><span data-stu-id="c18ec-161">hello date and time are UTC and are when hello telemetry was deposited in hello store - not hello time it was generated.</span></span> <span data-ttu-id="c18ec-162">Então se você gravar código toodownload Olá dados, ele pode percorrer linearmente dados saudação.</span><span class="sxs-lookup"><span data-stu-id="c18ec-162">So if you write code toodownload hello data, it can move linearly through hello data.</span></span>

<span data-ttu-id="c18ec-163">Aqui está o formulário de saudação do caminho de saudação:</span><span class="sxs-lookup"><span data-stu-id="c18ec-163">Here's hello form of hello path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="c18ec-164">Where</span><span class="sxs-lookup"><span data-stu-id="c18ec-164">Where</span></span>

* <span data-ttu-id="c18ec-165">`blobCreationTimeUtc`é o tempo quando blob foi criado no hello interno preparo armazenamento</span><span class="sxs-lookup"><span data-stu-id="c18ec-165">`blobCreationTimeUtc` is time when blob was created in hello internal staging storage</span></span>
* <span data-ttu-id="c18ec-166">`blobDeliveryTimeUtc`é o tempo de saudação quando o blob é copiado toohello armazenamento de destino de exportação</span><span class="sxs-lookup"><span data-stu-id="c18ec-166">`blobDeliveryTimeUtc` is hello time when blob is copied toohello export destination storage</span></span>

## <span data-ttu-id="c18ec-167"><a name="format"></a> Formato dos dados</span><span class="sxs-lookup"><span data-stu-id="c18ec-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="c18ec-168">Cada blob é um arquivo de texto que contém várias linhas separadas por “ \n”.</span><span class="sxs-lookup"><span data-stu-id="c18ec-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="c18ec-169">Ele contém telemetria Olá processada em um período de tempo de aproximadamente metade um minuto.</span><span class="sxs-lookup"><span data-stu-id="c18ec-169">It contains hello telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="c18ec-170">Cada linha representa um ponto de dados de telemetria como uma solicitação ou uma exibição de página.</span><span class="sxs-lookup"><span data-stu-id="c18ec-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="c18ec-171">Cada linha é um documento JSON não formatado.</span><span class="sxs-lookup"><span data-stu-id="c18ec-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="c18ec-172">Se você quiser toosit e como isso, abra-o no Visual Studio e escolha edite, Avançado, arquivo de formato:</span><span class="sxs-lookup"><span data-stu-id="c18ec-172">If you want toosit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![Exibição Olá telemetria com uma ferramenta adequada](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="c18ec-174">As durações de tempo são em tiques, em que 10.000 tiques = 1 ms.</span><span class="sxs-lookup"><span data-stu-id="c18ec-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="c18ec-175">Por exemplo, esses valores mostram um tempo de 1 MS toosend uma solicitação do navegador hello, 3ms tooreceive e 1.8s tooprocess Olá página no navegador de saudação:</span><span class="sxs-lookup"><span data-stu-id="c18ec-175">For example, these values show a time of 1ms toosend a request from hello browser, 3ms tooreceive it, and 1.8s tooprocess hello page in hello browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="c18ec-176">Referência de tipos de propriedade hello e valores do modelo de dados detalhados.</span><span class="sxs-lookup"><span data-stu-id="c18ec-176">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a><span data-ttu-id="c18ec-177">Processamento de dados Olá</span><span class="sxs-lookup"><span data-stu-id="c18ec-177">Processing hello data</span></span>
<span data-ttu-id="c18ec-178">Em pequena escala, você pode escrever alguns toopull código separar seus dados, lê-lo em uma planilha e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="c18ec-178">On a small scale, you can write some code toopull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="c18ec-179">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c18ec-179">For example:</span></span>

    private IEnumerable<T> DeserializeMany<T>(string folderName)
    {
      var files = Directory.EnumerateFiles(folderName, "*.blob", SearchOption.AllDirectories);
      foreach (var file in files)
      {
         using (var fileReader = File.OpenText(file))
         {
            string fileContent = fileReader.ReadToEnd();
            IEnumerable<string> entities = fileContent.Split('\n').Where(s => !string.IsNullOrWhiteSpace(s));
            foreach (var entity in entities)
            {
                yield return JsonConvert.DeserializeObject<T>(entity);
            }
         }
      }
    }

<span data-ttu-id="c18ec-180">Para obter um exemplo de código maior, consulte [usando uma função de trabalho][exportasa].</span><span class="sxs-lookup"><span data-stu-id="c18ec-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="c18ec-181"><a name="delete"></a>Excluir dados antigos</span><span class="sxs-lookup"><span data-stu-id="c18ec-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="c18ec-182">Observe que você é responsável por gerenciar a capacidade de armazenamento e excluir dados antigos de saudação se necessário.</span><span class="sxs-lookup"><span data-stu-id="c18ec-182">Please note that you are responsible for managing your storage capacity and deleting hello old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="c18ec-183">Se você regenerar sua chave de armazenamento...</span><span class="sxs-lookup"><span data-stu-id="c18ec-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="c18ec-184">Se você alterar o armazenamento de chave tooyour hello, a exportação contínua deixarão de funcionar.</span><span class="sxs-lookup"><span data-stu-id="c18ec-184">If you change hello key tooyour storage, continuous export will stop working.</span></span> <span data-ttu-id="c18ec-185">Você verá uma notificação em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="c18ec-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="c18ec-186">Abra a folha de exportação contínua de saudação e edite sua exportação.</span><span class="sxs-lookup"><span data-stu-id="c18ec-186">Open hello Continuous Export blade and edit your export.</span></span> <span data-ttu-id="c18ec-187">Editar saudação destino de exportação, mas deixe Olá mesmo armazenamento selecionado.</span><span class="sxs-lookup"><span data-stu-id="c18ec-187">Edit hello Export Destination, but just leave hello same storage selected.</span></span> <span data-ttu-id="c18ec-188">Clique em tooconfirm Okey.</span><span class="sxs-lookup"><span data-stu-id="c18ec-188">Click OK tooconfirm.</span></span>

![Editar saudação contínua exportar, abrir e fechar o destino de exportação.](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="c18ec-190">a exportação contínua Olá será reiniciado.</span><span class="sxs-lookup"><span data-stu-id="c18ec-190">hello continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="c18ec-191">Exemplos de exportação</span><span class="sxs-lookup"><span data-stu-id="c18ec-191">Export samples</span></span>

* <span data-ttu-id="c18ec-192">[Exportar tooSQL usando a análise de fluxo][exportasa]</span><span class="sxs-lookup"><span data-stu-id="c18ec-192">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="c18ec-193">Exemplo do Stream Analytics 2</span><span class="sxs-lookup"><span data-stu-id="c18ec-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="c18ec-194">Em escalas maiores, considere [HDInsight](https://azure.microsoft.com/services/hdinsight/) -clusters de Hadoop na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="c18ec-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in hello cloud.</span></span> <span data-ttu-id="c18ec-195">HDInsight fornece uma variedade de tecnologias para gerenciar e analisar dados grandes e você pode usar dados tooprocess que foi exportados do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="c18ec-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it tooprocess data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="c18ec-196">Perguntas e respostas</span><span class="sxs-lookup"><span data-stu-id="c18ec-196">Q & A</span></span>
* <span data-ttu-id="c18ec-197">*Mas tudo o que eu quero é um download único de um gráfico.*</span><span class="sxs-lookup"><span data-stu-id="c18ec-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="c18ec-198">Sim, você pode fazer isso.</span><span class="sxs-lookup"><span data-stu-id="c18ec-198">Yes, you can do that.</span></span> <span data-ttu-id="c18ec-199">Na parte superior de saudação da folha de saudação, clique em **exportar dados**.</span><span class="sxs-lookup"><span data-stu-id="c18ec-199">At hello top of hello blade, click **Export Data**.</span></span>
* <span data-ttu-id="c18ec-200">*Eu configuro uma exportação, mas não há nenhum dado no meu repositório.*</span><span class="sxs-lookup"><span data-stu-id="c18ec-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="c18ec-201">Application Insights recebeu qualquer telemetria do seu aplicativo desde que você configurar a exportação de Olá?</span><span class="sxs-lookup"><span data-stu-id="c18ec-201">Did Application Insights receive any telemetry from your app since you set up hello export?</span></span> <span data-ttu-id="c18ec-202">Você receberá apenas novos dados.</span><span class="sxs-lookup"><span data-stu-id="c18ec-202">You'll only receive new data.</span></span>
* <span data-ttu-id="c18ec-203">*Tentativa de tooset a exportação de uma, mas o acesso foi negado*</span><span class="sxs-lookup"><span data-stu-id="c18ec-203">*I tried tooset up an export, but was denied access*</span></span>

    <span data-ttu-id="c18ec-204">Se a conta de saudação é de propriedade de sua organização, você tem toobe um membro dos grupos de proprietários ou colaboradores hello.</span><span class="sxs-lookup"><span data-stu-id="c18ec-204">If hello account is owned by your organization, you have toobe a member of hello owners or contributors groups.</span></span>
* <span data-ttu-id="c18ec-205">*Posso exportar toomy reta local próprio repositório?*</span><span class="sxs-lookup"><span data-stu-id="c18ec-205">*Can I export straight toomy own on-premises store?*</span></span>

    <span data-ttu-id="c18ec-206">Não, infelizmente.</span><span class="sxs-lookup"><span data-stu-id="c18ec-206">No, sorry.</span></span> <span data-ttu-id="c18ec-207">Nosso mecanismo de exportação funciona apenas com o armazenamento do Azure no momento.</span><span class="sxs-lookup"><span data-stu-id="c18ec-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="c18ec-208">*É qualquer quantidade de toohello de limite de dados colocados em meu repositório?*</span><span class="sxs-lookup"><span data-stu-id="c18ec-208">*Is there any limit toohello amount of data you put in my store?*</span></span>

    <span data-ttu-id="c18ec-209">Não.</span><span class="sxs-lookup"><span data-stu-id="c18ec-209">No.</span></span> <span data-ttu-id="c18ec-210">Podemos vai manter enviar dados até que você exclua exportação hello.</span><span class="sxs-lookup"><span data-stu-id="c18ec-210">We'll keep pushing data in until you delete hello export.</span></span> <span data-ttu-id="c18ec-211">Vamos parar de se atingiremos limites de saudação externa para armazenamento de blob, mas isso é muito grande.</span><span class="sxs-lookup"><span data-stu-id="c18ec-211">We'll stop if we hit hello outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="c18ec-212">É o tooyou toocontrol quanto armazenamento você usa.</span><span class="sxs-lookup"><span data-stu-id="c18ec-212">It's up tooyou toocontrol how much storage you use.</span></span>  
* <span data-ttu-id="c18ec-213">*Como muitos blobs deve ver no armazenamento Olá?*</span><span class="sxs-lookup"><span data-stu-id="c18ec-213">*How many blobs should I see in hello storage?*</span></span>

  * <span data-ttu-id="c18ec-214">Para todos os dados de tipo tooexport selecionada, um novo blob é criado a cada minuto (se os dados estão disponíveis).</span><span class="sxs-lookup"><span data-stu-id="c18ec-214">For every data type you selected tooexport, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="c18ec-215">Além disso, para aplicativos com tráfego intenso, são alocadas unidades de partição adicionais.</span><span class="sxs-lookup"><span data-stu-id="c18ec-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="c18ec-216">Nesse caso, cada unidade cria um blob a cada minuto.</span><span class="sxs-lookup"><span data-stu-id="c18ec-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="c18ec-217">*Eu regeneradas armazenamento de chave toomy hello ou alterado Olá nome do contêiner de saudação, e agora exportação Olá não funciona.*</span><span class="sxs-lookup"><span data-stu-id="c18ec-217">*I regenerated hello key toomy storage or changed hello name of hello container, and now hello export doesn't work.*</span></span>

    <span data-ttu-id="c18ec-218">Editar a exportação de saudação e abra a folha de destino de exportação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c18ec-218">Edit hello export and open hello export destination blade.</span></span> <span data-ttu-id="c18ec-219">Deixe Olá mesmo armazenamento selecionado como antes e clique em tooconfirm Okey.</span><span class="sxs-lookup"><span data-stu-id="c18ec-219">Leave hello same storage selected as before, and click OK tooconfirm.</span></span> <span data-ttu-id="c18ec-220">A exportação será reiniciada.</span><span class="sxs-lookup"><span data-stu-id="c18ec-220">Export will restart.</span></span> <span data-ttu-id="c18ec-221">Se alterar hello dentro Olá alguns dias anteriores, você não perderá os dados.</span><span class="sxs-lookup"><span data-stu-id="c18ec-221">If hello change was within hello past few days, you won't lose data.</span></span>
* <span data-ttu-id="c18ec-222">*Posso pausar exportação Olá?*</span><span class="sxs-lookup"><span data-stu-id="c18ec-222">*Can I pause hello export?*</span></span>

    <span data-ttu-id="c18ec-223">Sim.</span><span class="sxs-lookup"><span data-stu-id="c18ec-223">Yes.</span></span> <span data-ttu-id="c18ec-224">Clique em Desabilitar.</span><span class="sxs-lookup"><span data-stu-id="c18ec-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="c18ec-225">Exemplos de código</span><span class="sxs-lookup"><span data-stu-id="c18ec-225">Code samples</span></span>

* [<span data-ttu-id="c18ec-226">Exemplo do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c18ec-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="c18ec-227">[Exportar tooSQL usando a análise de fluxo][exportasa]</span><span class="sxs-lookup"><span data-stu-id="c18ec-227">[Export tooSQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="c18ec-228">Referência de tipos de propriedade hello e valores do modelo de dados detalhados.</span><span class="sxs-lookup"><span data-stu-id="c18ec-228">Detailed data model reference for hello property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
