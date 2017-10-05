---
title: "Exportação contínua de telemetria do Application Insights | Microsoft Docs"
description: "Exportar dados de uso e diagnóstico para armazenamento no Microsoft Azure e baixá-los de lá."
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
ms.openlocfilehash: 6ac3bda5101593b5ca66b4c9035e2fdac9d1e833
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="export-telemetry-from-application-insights"></a><span data-ttu-id="f5908-103">Exportar telemetria do Application Insights</span><span class="sxs-lookup"><span data-stu-id="f5908-103">Export telemetry from Application Insights</span></span>
<span data-ttu-id="f5908-104">Deseja manter a telemetria por mais tempo que o período de retenção padrão?</span><span class="sxs-lookup"><span data-stu-id="f5908-104">Want to keep your telemetry for longer than the standard retention period?</span></span> <span data-ttu-id="f5908-105">Ou processá-la de alguma forma especializada?</span><span class="sxs-lookup"><span data-stu-id="f5908-105">Or process it in some specialized way?</span></span> <span data-ttu-id="f5908-106">Exportação contínua é ideal para isso.</span><span class="sxs-lookup"><span data-stu-id="f5908-106">Continuous Export is ideal for this.</span></span> <span data-ttu-id="f5908-107">Os eventos que você vê no portal do Application Insights podem ser exportados para armazenamento no Microsoft Azure no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="f5908-107">The events you see in the Application Insights portal can be exported to storage in Microsoft Azure in JSON format.</span></span> <span data-ttu-id="f5908-108">Ali, você pode baixar os dados e gravar qualquer código de que você precisa para processá-los.</span><span class="sxs-lookup"><span data-stu-id="f5908-108">From there you can download your data and write whatever code you need to process it.</span></span>  

<span data-ttu-id="f5908-109">Usar a exportação contínua pode incorrer em um custo adicional.</span><span class="sxs-lookup"><span data-stu-id="f5908-109">Using Continuous Export may incur an additional charge.</span></span> <span data-ttu-id="f5908-110">Verifique o [modelo de preços](http://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="f5908-110">Check your [pricing model](http://azure.microsoft.com/pricing/details/application-insights/).</span></span>

<span data-ttu-id="f5908-111">Antes de configurar a exportação contínua, há algumas alternativas que você talvez queira considerar:</span><span class="sxs-lookup"><span data-stu-id="f5908-111">Before you set up continuous export, there are some alternatives you might want to consider:</span></span>

* <span data-ttu-id="f5908-112">O botão Exportar na parte superior de uma métrica ou da folha de pesquisa permite transferir tabelas e gráficos para uma planilha do Excel.</span><span class="sxs-lookup"><span data-stu-id="f5908-112">The Export button at the top of a metrics or search blade lets you transfer tables and charts to an Excel spreadsheet.</span></span>

* <span data-ttu-id="f5908-113">O [Analytics](app-insights-analytics.md) fornece uma linguagem de consulta eficiente para telemetria.</span><span class="sxs-lookup"><span data-stu-id="f5908-113">[Analytics](app-insights-analytics.md) provides a powerful query language for telemetry.</span></span> <span data-ttu-id="f5908-114">Ele também pode exportar os resultados.</span><span class="sxs-lookup"><span data-stu-id="f5908-114">It can also export results.</span></span>
* <span data-ttu-id="f5908-115">Se desejar [explorar seus dados no Power BI](app-insights-export-power-bi.md), é possível fazer isso sem usar a Exportação Contínua.</span><span class="sxs-lookup"><span data-stu-id="f5908-115">If you're looking to [explore your data in Power BI](app-insights-export-power-bi.md), you can do that without using Continuous Export.</span></span>
* <span data-ttu-id="f5908-116">A [API REST de acesso a dados](https://dev.applicationinsights.io/) permite que você acesse a telemetria programaticamente.</span><span class="sxs-lookup"><span data-stu-id="f5908-116">The [Data access REST API](https://dev.applicationinsights.io/) lets you access your telemetry programmatically.</span></span>

<span data-ttu-id="f5908-117">Depois que a exportação contínua copia os dados para o armazenamento (onde eles podem permanecer pelo tempo desejado), eles ainda ficam disponíveis no Application Insights pelo [período de retenção](app-insights-data-retention-privacy.md) normal.</span><span class="sxs-lookup"><span data-stu-id="f5908-117">After Continuous Export copies your data to storage (where it can stay for as long as you like), it's still available in Application Insights for the usual [retention period](app-insights-data-retention-privacy.md).</span></span>

## <span data-ttu-id="f5908-118"><a name="setup"></a> Criar uma Exportação Contínua</span><span class="sxs-lookup"><span data-stu-id="f5908-118"><a name="setup"></a> Create a Continuous Export</span></span>
1. <span data-ttu-id="f5908-119">No recurso Application Insights do seu aplicativo, abra Exportação Contínua e selecione **Adicionar**:</span><span class="sxs-lookup"><span data-stu-id="f5908-119">In the Application Insights resource for your app, open Continuous Export and choose **Add**:</span></span>

    ![Role para baixo e clique em Exportação contínua](./media/app-insights-export-telemetry/01-export.png)

2. <span data-ttu-id="f5908-121">Escolha a telemetria de tipos de dados que você deseja exportar.</span><span class="sxs-lookup"><span data-stu-id="f5908-121">Choose the telemetry data types you want to export.</span></span>

3. <span data-ttu-id="f5908-122">Crie ou selecione uma [Conta de armazenamento do Azure](../storage/common/storage-introduction.md) onde você deseja armazenar os dados.</span><span class="sxs-lookup"><span data-stu-id="f5908-122">Create or select an [Azure storage account](../storage/common/storage-introduction.md) where you want to store the data.</span></span>

    > [!Warning]
    > <span data-ttu-id="f5908-123">Por padrão, o local de armazenamento será definido como a mesma região geográfica que seu recurso Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f5908-123">By default, the storage location will be set to the same geographical region as your Application Insights resource.</span></span> <span data-ttu-id="f5908-124">Armazenar em uma região diferente poderá incorrer em encargos de transferência.</span><span class="sxs-lookup"><span data-stu-id="f5908-124">If you store in a different region, you may incur transfer charges.</span></span>

    ![Clique em Adicionar, Destino de exportação, Conta de armazenamento e, em seguida, crie um novo repositório ou escolha um repositório existente](./media/app-insights-export-telemetry/02-add.png)

4. <span data-ttu-id="f5908-126">Crie ou selecione um contêiner no armazenamento:</span><span class="sxs-lookup"><span data-stu-id="f5908-126">Create or select a container in the storage:</span></span>

    ![Clique em Escolher tipos de evento](./media/app-insights-export-telemetry/create-container.png)

<span data-ttu-id="f5908-128">Depois de criar sua exportação, ela começa a ser realizada.</span><span class="sxs-lookup"><span data-stu-id="f5908-128">Once you've created your export, it starts going.</span></span> <span data-ttu-id="f5908-129">Você só obtém os dados que chegam após a criação da exportação.</span><span class="sxs-lookup"><span data-stu-id="f5908-129">You only get data that arrives after you create the export.</span></span>

<span data-ttu-id="f5908-130">Pode haver um atraso de aproximadamente uma hora antes de os dados aparecem no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f5908-130">There can be a delay of about an hour before data appears in the storage.</span></span>

### <a name="to-edit-continuous-export"></a><span data-ttu-id="f5908-131">Para editar a exportação contínua</span><span class="sxs-lookup"><span data-stu-id="f5908-131">To edit continuous export</span></span>

<span data-ttu-id="f5908-132">Se você quiser alterar os tipos de evento mais tarde, basta editar a exportação:</span><span class="sxs-lookup"><span data-stu-id="f5908-132">If you want to change the event types later, just edit the export:</span></span>

![Clique em Escolher tipos de evento](./media/app-insights-export-telemetry/05-edit.png)

### <a name="to-stop-continuous-export"></a><span data-ttu-id="f5908-134">Para interromper a exportação contínua</span><span class="sxs-lookup"><span data-stu-id="f5908-134">To stop continuous export</span></span>

<span data-ttu-id="f5908-135">Para interromper a exportação, clique em Desabilitar.</span><span class="sxs-lookup"><span data-stu-id="f5908-135">To stop the export, click Disable.</span></span> <span data-ttu-id="f5908-136">Quando você clicar em Habilitar novamente, a exportação será reiniciada com novos dados.</span><span class="sxs-lookup"><span data-stu-id="f5908-136">When you click Enable again, the export will restart with new data.</span></span> <span data-ttu-id="f5908-137">Você não obterá os dados recebidos no portal enquanto a exportação estava desabilitada.</span><span class="sxs-lookup"><span data-stu-id="f5908-137">You won't get the data that arrived in the portal while export was disabled.</span></span>

<span data-ttu-id="f5908-138">Para interromper a exportação permanentemente, basta excluí-la.</span><span class="sxs-lookup"><span data-stu-id="f5908-138">To stop the export permanently, delete it.</span></span> <span data-ttu-id="f5908-139">Isso não exclui seus dados do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f5908-139">Doing so doesn't delete your data from storage.</span></span>

### <a name="cant-add-or-change-an-export"></a><span data-ttu-id="f5908-140">Não consegue adicionar nem alterar uma exportação?</span><span class="sxs-lookup"><span data-stu-id="f5908-140">Can't add or change an export?</span></span>
* <span data-ttu-id="f5908-141">Para adicionar ou alterar exportações, você precisa de direitos de acesso de Proprietário, Colaborador ou Colaborador do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f5908-141">To add or change exports, you need Owner, Contributor or Application Insights Contributor access rights.</span></span> <span data-ttu-id="f5908-142">[Saiba mais sobre as funções][roles].</span><span class="sxs-lookup"><span data-stu-id="f5908-142">[Learn about roles][roles].</span></span>

## <span data-ttu-id="f5908-143"><a name="analyze"></a> Quais eventos você recebe?</span><span class="sxs-lookup"><span data-stu-id="f5908-143"><a name="analyze"></a> What events do you get?</span></span>
<span data-ttu-id="f5908-144">Os dados exportados são a telemetria bruta que recebemos de seu aplicativo, exceto que adicionamos dados de localização que calculamos por meio do endereço IP do cliente.</span><span class="sxs-lookup"><span data-stu-id="f5908-144">The exported data is the raw telemetry we receive from your application, except that we add location data which we calculate from the client IP address.</span></span>

<span data-ttu-id="f5908-145">Dados que foram descartados por [amostragem](app-insights-sampling.md) não são incluídos nos dados exportados.</span><span class="sxs-lookup"><span data-stu-id="f5908-145">Data that has been discarded by [sampling](app-insights-sampling.md) is not included in the exported data.</span></span>

<span data-ttu-id="f5908-146">Outras métricas calculadas não são incluídas.</span><span class="sxs-lookup"><span data-stu-id="f5908-146">Other calculated metrics are not included.</span></span> <span data-ttu-id="f5908-147">Por exemplo, nós não exportamos a utilização média de CPU, mas exportamos a telemetria bruta por meio da qual a média é computada.</span><span class="sxs-lookup"><span data-stu-id="f5908-147">For example, we don't export average CPU utilisation, but we do export the raw telemetry from which the average is computed.</span></span>

<span data-ttu-id="f5908-148">Os dados também incluem os resultados de todos os [testes da Web de disponibilidade](app-insights-monitor-web-app-availability.md) que você configurou.</span><span class="sxs-lookup"><span data-stu-id="f5908-148">The data also includes the results of any [availability web tests](app-insights-monitor-web-app-availability.md) that you have set up.</span></span>

> [!NOTE]
> <span data-ttu-id="f5908-149">**Amostragem.**</span><span class="sxs-lookup"><span data-stu-id="f5908-149">**Sampling.**</span></span> <span data-ttu-id="f5908-150">Se seu aplicativo enviar muitos dados, a funcionalidade de amostragem poderá operar e enviar apenas uma parte da telemetria gerada.</span><span class="sxs-lookup"><span data-stu-id="f5908-150">If your application sends a lot of data, the sampling feature may operate and send only a fraction of the generated telemetry.</span></span> [<span data-ttu-id="f5908-151">Saiba mais sobre amostragem.</span><span class="sxs-lookup"><span data-stu-id="f5908-151">Learn more about sampling.</span></span>](app-insights-sampling.md)
>
>

## <span data-ttu-id="f5908-152"><a name="get"></a> Inspecionar os dados</span><span class="sxs-lookup"><span data-stu-id="f5908-152"><a name="get"></a> Inspect the data</span></span>
<span data-ttu-id="f5908-153">Você pode inspecionar o armazenamento diretamente no portal.</span><span class="sxs-lookup"><span data-stu-id="f5908-153">You can inspect the storage directly in the portal.</span></span> <span data-ttu-id="f5908-154">Clique em **Procurar**, selecione sua conta de armazenamento e abra **Contêineres**.</span><span class="sxs-lookup"><span data-stu-id="f5908-154">Click **Browse**, select your storage account, and then open **Containers**.</span></span>

<span data-ttu-id="f5908-155">Para inspecionar o armazenamento do Azure no Visual Studio, abra **Exibir** e **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f5908-155">To inspect Azure storage in Visual Studio, open **View**, **Cloud Explorer**.</span></span> <span data-ttu-id="f5908-156">(Se você não tiver esse comando de menu, precisará instalar o SDK do Azure: abra o diálogo **Novo Projeto**, expanda Visual C#/Nuvem e escolha **Obter o SDK do Microsoft Azure para .NET**.)</span><span class="sxs-lookup"><span data-stu-id="f5908-156">(If you don't have that menu command, you need to install the Azure SDK: Open the **New Project** dialog, expand Visual C#/Cloud and choose **Get Microsoft Azure SDK for .NET**.)</span></span>

<span data-ttu-id="f5908-157">Quando você abrir o armazenamento de blob, verá um contêiner com um conjunto de arquivos de blob.</span><span class="sxs-lookup"><span data-stu-id="f5908-157">When you open your blob store, you'll see a container with a set of blob files.</span></span> <span data-ttu-id="f5908-158">O URI de cada arquivo deriva o nome do recurso Application Insights, da chave de instrumentação e do tipo/data/hora de telemetria.</span><span class="sxs-lookup"><span data-stu-id="f5908-158">The URI of each file derived from your Application Insights resource name, its instrumentation key, telemetry-type/date/time.</span></span> <span data-ttu-id="f5908-159">(O nome do recurso está todo em letras minúsculas e a chave de instrumentação omite traços.)</span><span class="sxs-lookup"><span data-stu-id="f5908-159">(The resource name is all lowercase, and the instrumentation key omits dashes.)</span></span>

![Inspecione o repositório de blob com uma ferramenta adequada](./media/app-insights-export-telemetry/04-data.png)

<span data-ttu-id="f5908-161">A data e hora são em formato UTC, e referentes a quando a telemetria foi depositada no repositório - não à hora em que essa telemetria foi gerada.</span><span class="sxs-lookup"><span data-stu-id="f5908-161">The date and time are UTC and are when the telemetry was deposited in the store - not the time it was generated.</span></span> <span data-ttu-id="f5908-162">Então, se você escrever código para baixar os dados, ele pode percorrer os dados linearmente.</span><span class="sxs-lookup"><span data-stu-id="f5908-162">So if you write code to download the data, it can move linearly through the data.</span></span>

<span data-ttu-id="f5908-163">Veja o formato do caminho:</span><span class="sxs-lookup"><span data-stu-id="f5908-163">Here's the form of the path:</span></span>

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

<span data-ttu-id="f5908-164">Where</span><span class="sxs-lookup"><span data-stu-id="f5908-164">Where</span></span>

* <span data-ttu-id="f5908-165">`blobCreationTimeUtc` é a hora em que o blob foi criado no armazenamento de preparo interno</span><span class="sxs-lookup"><span data-stu-id="f5908-165">`blobCreationTimeUtc` is time when blob was created in the internal staging storage</span></span>
* <span data-ttu-id="f5908-166">`blobDeliveryTimeUtc` é a hora em que o blob foi copiado para o armazenamento de destino de exportação</span><span class="sxs-lookup"><span data-stu-id="f5908-166">`blobDeliveryTimeUtc` is the time when blob is copied to the export destination storage</span></span>

## <span data-ttu-id="f5908-167"><a name="format"></a> Formato dos dados</span><span class="sxs-lookup"><span data-stu-id="f5908-167"><a name="format"></a> Data format</span></span>
* <span data-ttu-id="f5908-168">Cada blob é um arquivo de texto que contém várias linhas separadas por “ \n”.</span><span class="sxs-lookup"><span data-stu-id="f5908-168">Each blob is a text file that contains multiple '\n'-separated rows.</span></span> <span data-ttu-id="f5908-169">Ele contém a telemetria processada durante um período de tempo de aproximadamente metade um minuto.</span><span class="sxs-lookup"><span data-stu-id="f5908-169">It contains the telemetry processed over a time period of roughly half a minute.</span></span>
* <span data-ttu-id="f5908-170">Cada linha representa um ponto de dados de telemetria como uma solicitação ou uma exibição de página.</span><span class="sxs-lookup"><span data-stu-id="f5908-170">Each row represents a telemetry data point such as a request or page view.</span></span>
* <span data-ttu-id="f5908-171">Cada linha é um documento JSON não formatado.</span><span class="sxs-lookup"><span data-stu-id="f5908-171">Each row is an unformatted JSON document.</span></span> <span data-ttu-id="f5908-172">Se você quiser ficar olhando para ele, abra-o no Visual Studio e escolha Editar, Avançado, Arquivo de Formato:</span><span class="sxs-lookup"><span data-stu-id="f5908-172">If you want to sit and stare at it, open it in Visual Studio and choose Edit, Advanced, Format File:</span></span>

![Veja a telemetria com uma ferramenta adequada](./media/app-insights-export-telemetry/06-json.png)

<span data-ttu-id="f5908-174">As durações de tempo são em tiques, em que 10.000 tiques = 1 ms.</span><span class="sxs-lookup"><span data-stu-id="f5908-174">Time durations are in ticks, where 10 000 ticks = 1ms.</span></span> <span data-ttu-id="f5908-175">Por exemplo, esses valores mostram um tempo de 1 ms para enviar uma solicitação do navegador, 3 ms recebê-la e 1,8 s para processar a página no navegador:</span><span class="sxs-lookup"><span data-stu-id="f5908-175">For example, these values show a time of 1ms to send a request from the browser, 3ms to receive it, and 1.8s to process the page in the browser:</span></span>

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[<span data-ttu-id="f5908-176">Referência de modelo de dados detalhados para os tipos de propriedades e valores.</span><span class="sxs-lookup"><span data-stu-id="f5908-176">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

## <a name="processing-the-data"></a><span data-ttu-id="f5908-177">Processamento dos dados</span><span class="sxs-lookup"><span data-stu-id="f5908-177">Processing the data</span></span>
<span data-ttu-id="f5908-178">Em pequena escala, você pode escrever um código para extrair e separar seus dados, lê-los em uma planilha e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="f5908-178">On a small scale, you can write some code to pull apart your data, read it into a spreadsheet, and so on.</span></span> <span data-ttu-id="f5908-179">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f5908-179">For example:</span></span>

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

<span data-ttu-id="f5908-180">Para obter um exemplo de código maior, consulte [usando uma função de trabalho][exportasa].</span><span class="sxs-lookup"><span data-stu-id="f5908-180">For a larger code sample, see [using a worker role][exportasa].</span></span>

## <span data-ttu-id="f5908-181"><a name="delete"></a>Excluir dados antigos</span><span class="sxs-lookup"><span data-stu-id="f5908-181"><a name="delete"></a>Delete your old data</span></span>
<span data-ttu-id="f5908-182">Observe que você é responsável por gerenciar a capacidade de armazenamento e excluir dados antigos, se necessário.</span><span class="sxs-lookup"><span data-stu-id="f5908-182">Please note that you are responsible for managing your storage capacity and deleting the old data if necessary.</span></span>

## <a name="if-you-regenerate-your-storage-key"></a><span data-ttu-id="f5908-183">Se você regenerar sua chave de armazenamento...</span><span class="sxs-lookup"><span data-stu-id="f5908-183">If you regenerate your storage key...</span></span>
<span data-ttu-id="f5908-184">Se você alterar a chave para seu armazenamento, a exportação contínua deixará de funcionar.</span><span class="sxs-lookup"><span data-stu-id="f5908-184">If you change the key to your storage, continuous export will stop working.</span></span> <span data-ttu-id="f5908-185">Você verá uma notificação em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5908-185">You'll see a notification in your Azure account.</span></span>

<span data-ttu-id="f5908-186">Abrir a folha Exportação Contínua e edite sua exportação.</span><span class="sxs-lookup"><span data-stu-id="f5908-186">Open the Continuous Export blade and edit your export.</span></span> <span data-ttu-id="f5908-187">Edite o destino de exportação, mas mantenha o mesmo armazenamento selecionado.</span><span class="sxs-lookup"><span data-stu-id="f5908-187">Edit the Export Destination, but just leave the same storage selected.</span></span> <span data-ttu-id="f5908-188">Clique em OK para confirmar.</span><span class="sxs-lookup"><span data-stu-id="f5908-188">Click OK to confirm.</span></span>

![Edite a exportação contínua, abra e feche o destino de exportação.](./media/app-insights-export-telemetry/07-resetstore.png)

<span data-ttu-id="f5908-190">A exportação contínua será reiniciada.</span><span class="sxs-lookup"><span data-stu-id="f5908-190">The continuous export will restart.</span></span>

## <a name="export-samples"></a><span data-ttu-id="f5908-191">Exemplos de exportação</span><span class="sxs-lookup"><span data-stu-id="f5908-191">Export samples</span></span>

* <span data-ttu-id="f5908-192">[Exportar para o SQL usando o Stream Analytics][exportasa]</span><span class="sxs-lookup"><span data-stu-id="f5908-192">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="f5908-193">Exemplo do Stream Analytics 2</span><span class="sxs-lookup"><span data-stu-id="f5908-193">Stream Analytics sample 2</span></span>](app-insights-export-stream-analytics.md)

<span data-ttu-id="f5908-194">Em escalas maiores, considere usar o [HDInsight](https://azure.microsoft.com/services/hdinsight/) - clusters de Hadoop na nuvem.</span><span class="sxs-lookup"><span data-stu-id="f5908-194">On larger scales, consider [HDInsight](https://azure.microsoft.com/services/hdinsight/) - Hadoop clusters in the cloud.</span></span> <span data-ttu-id="f5908-195">O HDInsight fornece várias tecnologias para gerenciar e analisar Big Data, e você pode usá-lo para processar dados que foram exportados do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="f5908-195">HDInsight provides a variety of technologies for managing and analyzing big data, and you could use it to process data that has been exported from Application Insights.</span></span>

## <a name="q--a"></a><span data-ttu-id="f5908-196">Perguntas e respostas</span><span class="sxs-lookup"><span data-stu-id="f5908-196">Q & A</span></span>
* <span data-ttu-id="f5908-197">*Mas tudo o que eu quero é um download único de um gráfico.*</span><span class="sxs-lookup"><span data-stu-id="f5908-197">*But all I want is a one-time download of a chart.*</span></span>  

    <span data-ttu-id="f5908-198">Sim, você pode fazer isso.</span><span class="sxs-lookup"><span data-stu-id="f5908-198">Yes, you can do that.</span></span> <span data-ttu-id="f5908-199">Na parte superior da folha, clique **Exportar dados**.</span><span class="sxs-lookup"><span data-stu-id="f5908-199">At the top of the blade, click **Export Data**.</span></span>
* <span data-ttu-id="f5908-200">*Eu configuro uma exportação, mas não há nenhum dado no meu repositório.*</span><span class="sxs-lookup"><span data-stu-id="f5908-200">*I set up an export, but there's no data in my store.*</span></span>

    <span data-ttu-id="f5908-201">O Application Insights recebeu qualquer telemetria do seu aplicativo desde que você configurou a exportação?</span><span class="sxs-lookup"><span data-stu-id="f5908-201">Did Application Insights receive any telemetry from your app since you set up the export?</span></span> <span data-ttu-id="f5908-202">Você receberá apenas novos dados.</span><span class="sxs-lookup"><span data-stu-id="f5908-202">You'll only receive new data.</span></span>
* <span data-ttu-id="f5908-203">*Eu tentei configurar uma exportação, mas o acesso foi negado*</span><span class="sxs-lookup"><span data-stu-id="f5908-203">*I tried to set up an export, but was denied access*</span></span>

    <span data-ttu-id="f5908-204">Se a conta pertence à sua organização, você precisa ser membro do grupo de proprietários ou do grupo de colaboradores.</span><span class="sxs-lookup"><span data-stu-id="f5908-204">If the account is owned by your organization, you have to be a member of the owners or contributors groups.</span></span>
* <span data-ttu-id="f5908-205">*Eu posso exportar diretamente para meu próprio repositório local?*</span><span class="sxs-lookup"><span data-stu-id="f5908-205">*Can I export straight to my own on-premises store?*</span></span>

    <span data-ttu-id="f5908-206">Não, infelizmente.</span><span class="sxs-lookup"><span data-stu-id="f5908-206">No, sorry.</span></span> <span data-ttu-id="f5908-207">Nosso mecanismo de exportação funciona apenas com o armazenamento do Azure no momento.</span><span class="sxs-lookup"><span data-stu-id="f5908-207">Our export engine currently only works with Azure storage at this time.</span></span>  
* <span data-ttu-id="f5908-208">*Há qualquer limite para a quantidade de dados que você coloca em meu repositório?*</span><span class="sxs-lookup"><span data-stu-id="f5908-208">*Is there any limit to the amount of data you put in my store?*</span></span>

    <span data-ttu-id="f5908-209">Não.</span><span class="sxs-lookup"><span data-stu-id="f5908-209">No.</span></span> <span data-ttu-id="f5908-210">Continuaremos a enviar dados por push até que você exclua a exportação.</span><span class="sxs-lookup"><span data-stu-id="f5908-210">We'll keep pushing data in until you delete the export.</span></span> <span data-ttu-id="f5908-211">Interromperemos o envio se atingirmos os limites externos para o armazenamento de blob, mas são limites enormes.</span><span class="sxs-lookup"><span data-stu-id="f5908-211">We'll stop if we hit the outer limits for blob storage, but that's pretty huge.</span></span> <span data-ttu-id="f5908-212">Cabe a você controlar a quantidade de armazenamento que usa.</span><span class="sxs-lookup"><span data-stu-id="f5908-212">It's up to you to control how much storage you use.</span></span>  
* <span data-ttu-id="f5908-213">*Quantos blobs devo ver no armazenamento?*</span><span class="sxs-lookup"><span data-stu-id="f5908-213">*How many blobs should I see in the storage?*</span></span>

  * <span data-ttu-id="f5908-214">Para cada tipo de dados selecionado para exportação, um novo blob é criado a cada minuto (se os dados estiverem disponíveis).</span><span class="sxs-lookup"><span data-stu-id="f5908-214">For every data type you selected to export, a new blob is created every minute (if data is available).</span></span>
  * <span data-ttu-id="f5908-215">Além disso, para aplicativos com tráfego intenso, são alocadas unidades de partição adicionais.</span><span class="sxs-lookup"><span data-stu-id="f5908-215">In addition, for applications with high traffic, additional partition units are allocated.</span></span> <span data-ttu-id="f5908-216">Nesse caso, cada unidade cria um blob a cada minuto.</span><span class="sxs-lookup"><span data-stu-id="f5908-216">In this case each unit creates a blob every minute.</span></span>
* <span data-ttu-id="f5908-217">*Eu regenerei a chave para o meu armazenamento ou alterei o nome do contêiner, e agora a exportação não funciona.*</span><span class="sxs-lookup"><span data-stu-id="f5908-217">*I regenerated the key to my storage or changed the name of the container, and now the export doesn't work.*</span></span>

    <span data-ttu-id="f5908-218">Edite a exportação e abra a folha Destino de exportação.</span><span class="sxs-lookup"><span data-stu-id="f5908-218">Edit the export and open the export destination blade.</span></span> <span data-ttu-id="f5908-219">Deixe o mesmo armazenamento de antes selecionado e clique em OK para confirmar.</span><span class="sxs-lookup"><span data-stu-id="f5908-219">Leave the same storage selected as before, and click OK to confirm.</span></span> <span data-ttu-id="f5908-220">A exportação será reiniciada.</span><span class="sxs-lookup"><span data-stu-id="f5908-220">Export will restart.</span></span> <span data-ttu-id="f5908-221">Se a alteração foi realizada nos últimos dias, você não perderá dados.</span><span class="sxs-lookup"><span data-stu-id="f5908-221">If the change was within the past few days, you won't lose data.</span></span>
* <span data-ttu-id="f5908-222">*Posso pausar a exportação?*</span><span class="sxs-lookup"><span data-stu-id="f5908-222">*Can I pause the export?*</span></span>

    <span data-ttu-id="f5908-223">Sim.</span><span class="sxs-lookup"><span data-stu-id="f5908-223">Yes.</span></span> <span data-ttu-id="f5908-224">Clique em Desabilitar.</span><span class="sxs-lookup"><span data-stu-id="f5908-224">Click Disable.</span></span>

## <a name="code-samples"></a><span data-ttu-id="f5908-225">Exemplos de código</span><span class="sxs-lookup"><span data-stu-id="f5908-225">Code samples</span></span>

* [<span data-ttu-id="f5908-226">Exemplo do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f5908-226">Stream Analytics sample</span></span>](app-insights-export-stream-analytics.md)
* <span data-ttu-id="f5908-227">[Exportar para o SQL usando o Stream Analytics][exportasa]</span><span class="sxs-lookup"><span data-stu-id="f5908-227">[Export to SQL using Stream Analytics][exportasa]</span></span>
* [<span data-ttu-id="f5908-228">Referência de modelo de dados detalhados para os tipos de propriedades e valores.</span><span class="sxs-lookup"><span data-stu-id="f5908-228">Detailed data model reference for the property types and values.</span></span>](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
