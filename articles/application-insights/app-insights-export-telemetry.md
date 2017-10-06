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
# <a name="export-telemetry-from-application-insights"></a>Exportar telemetria do Application Insights
Deseja tookeep sua telemetria por mais de um período de retenção padrão de Olá? Ou processá-la de alguma forma especializada? Exportação contínua é ideal para isso. Olá eventos no portal do Application Insights Olá podem ser exportado toostorage no Microsoft Azure no formato JSON. A partir daí, você pode baixar o seus dados e gravar qualquer código que você precisa tooprocess-lo.  

Usar a exportação contínua pode incorrer em um custo adicional. Verifique o [modelo de preços](http://azure.microsoft.com/pricing/details/application-insights/).

Antes de configurar a exportação contínua, há algumas alternativas que talvez você queira tooconsider:

* botão de exportação de saudação na parte superior de saudação da folha de métricas ou pesquisar permite transferir tabelas e gráficos tooan planilha do Excel.

* O [Analytics](app-insights-analytics.md) fornece uma linguagem de consulta eficiente para telemetria. Ele também pode exportar os resultados.
* Se você estiver procurando muito[explorar seus dados no Power BI](app-insights-export-power-bi.md), você pode fazer isso sem usar a exportação contínua.
* Olá [API REST de acesso a dados](https://dev.applicationinsights.io/) permite que você acesse sua telemetria programaticamente.

Após a exportação contínua copia o toostorage de dados (onde ele pode permanecer para desde que você deseja), ele ainda está disponível no Application Insights para saudação normal [período de retenção](app-insights-data-retention-privacy.md).

## <a name="setup"></a> Criar uma Exportação Contínua
1. No hello recurso do Application Insights para seu aplicativo, abra a exportação contínua e escolha **adicionar**:

    ![Role para baixo e clique em Exportação contínua](./media/app-insights-export-telemetry/01-export.png)

2. Escolha os tipos de dados de telemetria Olá tooexport desejado.

3. Crie ou selecione um [conta de armazenamento do Azure](../storage/common/storage-introduction.md) onde você deseja toostore Olá dados.

    > [!Warning]
    > Por padrão, o local de armazenamento Olá será definido toohello mesma região geográfica que o recurso do Application Insights. Armazenar em uma região diferente poderá incorrer em encargos de transferência.

    ![Clique em Adicionar, Destino de exportação, Conta de armazenamento e, em seguida, crie um novo repositório ou escolha um repositório existente](./media/app-insights-export-telemetry/02-add.png)

4. Crie ou selecione um contêiner no armazenamento de saudação:

    ![Clique em Escolher tipos de evento](./media/app-insights-export-telemetry/create-container.png)

Depois de criar sua exportação, ela começa a ser realizada. Você somente obtém dados que chega depois de criar a exportação de saudação.

Pode haver um atraso de aproximadamente uma hora antes de dados aparecem no armazenamento de saudação.

### <a name="tooedit-continuous-export"></a>exportação contínua tooedit

Se você quiser que tipos de evento toochange hello mais tarde, basta editar Olá exportação:

![Clique em Escolher tipos de evento](./media/app-insights-export-telemetry/05-edit.png)

### <a name="toostop-continuous-export"></a>exportação contínua toostop

exportação de saudação toostop, clique em Desabilitar. Quando você clica em habilitar novamente, exportação Olá reiniciará com novos dados. Você não obterá dados Olá que chegaram no portal de saudação enquanto a exportação foi desabilitada.

exportação de saudação toostop permanentemente, exclua-o. Isso não exclui seus dados do armazenamento.

### <a name="cant-add-or-change-an-export"></a>Não consegue adicionar nem alterar uma exportação?
* tooadd ou alteração de exportação, você precisa ter direitos de acesso de proprietário, colaborador ou colaborador do Application Insights. [Saiba mais sobre as funções][roles].

## <a name="analyze"></a> Quais eventos você recebe?
Olá dados exportados são brutos de telemetria Olá que recebemos do seu aplicativo, exceto que podemos adicionar dados de local que calculamos do endereço IP de cliente hello.

Dados que já foi descartados pelo [amostragem](app-insights-sampling.md) não está incluído nos dados hello exportada.

Outras métricas calculadas não são incluídas. Por exemplo, podemos não exportar a utilização média de CPU, mas podemos exportar telemetria bruto de saudação do qual a média de saudação é computada.

Olá dados também incluem Olá resultados de qualquer [testes da web de disponibilidade](app-insights-monitor-web-app-availability.md) que você configurou.

> [!NOTE]
> **Amostragem.** Se seu aplicativo envia um lote de dados, o recurso de amostragem de saudação pode operar e enviar somente uma fração de telemetria Olá gerado. [Saiba mais sobre amostragem.](app-insights-sampling.md)
>
>

## <a name="get"></a>Inspecionar dados Olá
Você pode inspecionar o armazenamento de saudação diretamente no portal de saudação. Clique em **Procurar**, selecione sua conta de armazenamento e abra **Contêineres**.

tooinspect armazenamento do Azure no Visual Studio, abra **exibição**, **Cloud Explorer**. (Se você não tiver esse comando de menu, você precisa tooinstall Olá SDK do Azure: Olá abrir **novo projeto** caixa de diálogo, expanda Visual c# / nuvem e escolha **obter o Microsoft Azure SDK para .NET**.)

Quando você abrir o armazenamento de blob, verá um contêiner com um conjunto de arquivos de blob. Olá URI de cada arquivo derivado de seu nome de recurso do Application Insights, sua chave de instrumentação, telemetria-tipo/Data/hora. (nome de recurso Olá contém letras minúscula e chave de instrumentação Olá omite traços.)

![Inspecione o armazenamento de blob Olá com uma ferramenta adequada](./media/app-insights-export-telemetry/04-data.png)

saudação de data e hora são UTC e quando telemetria Olá foi depositada no armazenamento Olá - tempo de saudação não foi gerado. Então se você gravar código toodownload Olá dados, ele pode percorrer linearmente dados saudação.

Aqui está o formulário de saudação do caminho de saudação:

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

Where

* `blobCreationTimeUtc`é o tempo quando blob foi criado no hello interno preparo armazenamento
* `blobDeliveryTimeUtc`é o tempo de saudação quando o blob é copiado toohello armazenamento de destino de exportação

## <a name="format"></a> Formato dos dados
* Cada blob é um arquivo de texto que contém várias linhas separadas por “ \n”. Ele contém telemetria Olá processada em um período de tempo de aproximadamente metade um minuto.
* Cada linha representa um ponto de dados de telemetria como uma solicitação ou uma exibição de página.
* Cada linha é um documento JSON não formatado. Se você quiser toosit e como isso, abra-o no Visual Studio e escolha edite, Avançado, arquivo de formato:

![Exibição Olá telemetria com uma ferramenta adequada](./media/app-insights-export-telemetry/06-json.png)

As durações de tempo são em tiques, em que 10.000 tiques = 1 ms. Por exemplo, esses valores mostram um tempo de 1 MS toosend uma solicitação do navegador hello, 3ms tooreceive e 1.8s tooprocess Olá página no navegador de saudação:

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[Referência de tipos de propriedade hello e valores do modelo de dados detalhados.](app-insights-export-data-model.md)

## <a name="processing-hello-data"></a>Processamento de dados Olá
Em pequena escala, você pode escrever alguns toopull código separar seus dados, lê-lo em uma planilha e assim por diante. Por exemplo:

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

Para obter um exemplo de código maior, consulte [usando uma função de trabalho][exportasa].

## <a name="delete"></a>Excluir dados antigos
Observe que você é responsável por gerenciar a capacidade de armazenamento e excluir dados antigos de saudação se necessário.

## <a name="if-you-regenerate-your-storage-key"></a>Se você regenerar sua chave de armazenamento...
Se você alterar o armazenamento de chave tooyour hello, a exportação contínua deixarão de funcionar. Você verá uma notificação em sua conta do Azure.

Abra a folha de exportação contínua de saudação e edite sua exportação. Editar saudação destino de exportação, mas deixe Olá mesmo armazenamento selecionado. Clique em tooconfirm Okey.

![Editar saudação contínua exportar, abrir e fechar o destino de exportação.](./media/app-insights-export-telemetry/07-resetstore.png)

a exportação contínua Olá será reiniciado.

## <a name="export-samples"></a>Exemplos de exportação

* [Exportar tooSQL usando a análise de fluxo][exportasa]
* [Exemplo do Stream Analytics 2](app-insights-export-stream-analytics.md)

Em escalas maiores, considere [HDInsight](https://azure.microsoft.com/services/hdinsight/) -clusters de Hadoop na nuvem hello. HDInsight fornece uma variedade de tecnologias para gerenciar e analisar dados grandes e você pode usar dados tooprocess que foi exportados do Application Insights.

## <a name="q--a"></a>Perguntas e respostas
* *Mas tudo o que eu quero é um download único de um gráfico.*  

    Sim, você pode fazer isso. Na parte superior de saudação da folha de saudação, clique em **exportar dados**.
* *Eu configuro uma exportação, mas não há nenhum dado no meu repositório.*

    Application Insights recebeu qualquer telemetria do seu aplicativo desde que você configurar a exportação de Olá? Você receberá apenas novos dados.
* *Tentativa de tooset a exportação de uma, mas o acesso foi negado*

    Se a conta de saudação é de propriedade de sua organização, você tem toobe um membro dos grupos de proprietários ou colaboradores hello.
* *Posso exportar toomy reta local próprio repositório?*

    Não, infelizmente. Nosso mecanismo de exportação funciona apenas com o armazenamento do Azure no momento.  
* *É qualquer quantidade de toohello de limite de dados colocados em meu repositório?*

    Não. Podemos vai manter enviar dados até que você exclua exportação hello. Vamos parar de se atingiremos limites de saudação externa para armazenamento de blob, mas isso é muito grande. É o tooyou toocontrol quanto armazenamento você usa.  
* *Como muitos blobs deve ver no armazenamento Olá?*

  * Para todos os dados de tipo tooexport selecionada, um novo blob é criado a cada minuto (se os dados estão disponíveis).
  * Além disso, para aplicativos com tráfego intenso, são alocadas unidades de partição adicionais. Nesse caso, cada unidade cria um blob a cada minuto.
* *Eu regeneradas armazenamento de chave toomy hello ou alterado Olá nome do contêiner de saudação, e agora exportação Olá não funciona.*

    Editar a exportação de saudação e abra a folha de destino de exportação de saudação. Deixe Olá mesmo armazenamento selecionado como antes e clique em tooconfirm Okey. A exportação será reiniciada. Se alterar hello dentro Olá alguns dias anteriores, você não perderá os dados.
* *Posso pausar exportação Olá?*

    Sim. Clique em Desabilitar.

## <a name="code-samples"></a>Exemplos de código

* [Exemplo do Stream Analytics](app-insights-export-stream-analytics.md)
* [Exportar tooSQL usando a análise de fluxo][exportasa]
* [Referência de tipos de propriedade hello e valores do modelo de dados detalhados.](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
