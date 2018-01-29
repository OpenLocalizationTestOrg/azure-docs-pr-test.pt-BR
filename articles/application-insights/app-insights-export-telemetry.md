---
title: "Exportação contínua de telemetria do Application Insights | Microsoft Docs"
description: "Exportar dados de uso e diagnóstico para armazenamento no Microsoft Azure e baixá-los de lá."
services: application-insights
documentationcenter: 
author: mrbullwinkle
manager: carmonm
ms.assetid: 5b859200-b484-4c98-9d9f-929713f1030c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: mbullwin
ms.openlocfilehash: 7d1f648bc2c2a42cfbd668f180bce8f56ebd065b
ms.sourcegitcommit: e462e5cca2424ce36423f9eff3a0cf250ac146ad
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/01/2017
---
# <a name="export-telemetry-from-application-insights"></a>Exportar telemetria do Application Insights
Deseja manter a telemetria por mais tempo que o período de retenção padrão? Ou processá-la de alguma forma especializada? Exportação contínua é ideal para isso. Os eventos que você vê no portal do Application Insights podem ser exportados para armazenamento no Microsoft Azure no formato JSON. Ali, você pode baixar os dados e gravar qualquer código de que você precisa para processá-los.  

Usar a exportação contínua pode incorrer em um custo adicional. Verifique o [modelo de preços](http://azure.microsoft.com/pricing/details/application-insights/).

Antes de configurar a exportação contínua, há algumas alternativas que você talvez queira considerar:

* O botão Exportar na parte superior de uma métrica ou da folha de pesquisa permite transferir tabelas e gráficos para uma planilha do Excel.

* O [Analytics](app-insights-analytics.md) fornece uma linguagem de consulta eficiente para telemetria. Ele também pode exportar os resultados.
* Se desejar [explorar seus dados no Power BI](app-insights-export-power-bi.md), é possível fazer isso sem usar a Exportação Contínua.
* A [API REST de acesso a dados](https://dev.applicationinsights.io/) permite que você acesse a telemetria programaticamente.

Depois que a exportação contínua copia os dados para o armazenamento (onde eles podem permanecer pelo tempo desejado), eles ainda ficam disponíveis no Application Insights pelo [período de retenção](app-insights-data-retention-privacy.md) normal.

## <a name="setup"></a> Criar uma Exportação Contínua
1. No recurso Application Insights do seu aplicativo, abra Exportação Contínua e selecione **Adicionar**:

    ![Role para baixo e clique em Exportação contínua](./media/app-insights-export-telemetry/01-export.png)

2. Escolha a telemetria de tipos de dados que você deseja exportar.

3. Crie ou selecione uma [Conta de armazenamento do Azure](../storage/common/storage-introduction.md) onde você deseja armazenar os dados.

    > [!Warning]
    > Por padrão, o local de armazenamento será definido como a mesma região geográfica que seu recurso Application Insights. Armazenar em uma região diferente poderá incorrer em encargos de transferência.

    ![Clique em Adicionar, Destino de exportação, Conta de armazenamento e, em seguida, crie um novo repositório ou escolha um repositório existente](./media/app-insights-export-telemetry/02-add.png)

4. Crie ou selecione um contêiner no armazenamento:

    ![Clique em Escolher tipos de evento](./media/app-insights-export-telemetry/create-container.png)

Depois de criar sua exportação, ela começa a ser realizada. Você só obtém os dados que chegam após a criação da exportação.

Pode haver um atraso de aproximadamente uma hora antes de os dados aparecem no armazenamento.

### <a name="to-edit-continuous-export"></a>Para editar a exportação contínua

Se você quiser alterar os tipos de evento mais tarde, basta editar a exportação:

![Clique em Escolher tipos de evento](./media/app-insights-export-telemetry/05-edit.png)

### <a name="to-stop-continuous-export"></a>Para interromper a exportação contínua

Para interromper a exportação, clique em Desabilitar. Quando você clicar em Habilitar novamente, a exportação será reiniciada com novos dados. Você não obterá os dados recebidos no portal enquanto a exportação estava desabilitada.

Para interromper a exportação permanentemente, basta excluí-la. Isso não exclui seus dados do armazenamento.

### <a name="cant-add-or-change-an-export"></a>Não consegue adicionar nem alterar uma exportação?
* Para adicionar ou alterar exportações, você precisa de direitos de acesso de Proprietário, Colaborador ou Colaborador do Application Insights. [Saiba mais sobre as funções][roles].

## <a name="analyze"></a> Quais eventos você recebe?
Os dados exportados são a telemetria bruta que recebemos de seu aplicativo, exceto que adicionamos dados de localização que calculamos por meio do endereço IP do cliente.

Dados que foram descartados por [amostragem](app-insights-sampling.md) não são incluídos nos dados exportados.

Outras métricas calculadas não são incluídas. Por exemplo, nós não exportamos a utilização média de CPU, mas exportamos a telemetria bruta por meio da qual a média é computada.

Os dados também incluem os resultados de todos os [testes da Web de disponibilidade](app-insights-monitor-web-app-availability.md) que você configurou.

> [!NOTE]
> **Amostragem.** Se seu aplicativo enviar muitos dados, a funcionalidade de amostragem poderá operar e enviar apenas uma parte da telemetria gerada. [Saiba mais sobre amostragem.](app-insights-sampling.md)
>
>

## <a name="get"></a> Inspecionar os dados
Você pode inspecionar o armazenamento diretamente no portal. Clique em **Procurar**, selecione sua conta de armazenamento e abra **Contêineres**.

Para inspecionar o armazenamento do Azure no Visual Studio, abra **Exibir** e **Cloud Explorer**. (Se você não tiver esse comando de menu, precisará instalar o SDK do Azure: abra o diálogo **Novo Projeto**, expanda Visual C#/Nuvem e escolha **Obter o SDK do Microsoft Azure para .NET**.)

Quando você abrir o armazenamento de blob, verá um contêiner com um conjunto de arquivos de blob. O URI de cada arquivo deriva o nome do recurso Application Insights, da chave de instrumentação e do tipo/data/hora de telemetria. (O nome do recurso está todo em letras minúsculas e a chave de instrumentação omite traços.)

![Inspecione o repositório de blob com uma ferramenta adequada](./media/app-insights-export-telemetry/04-data.png)

A data e hora são em formato UTC, e referentes a quando a telemetria foi depositada no repositório - não à hora em que essa telemetria foi gerada. Então, se você escrever código para baixar os dados, ele pode percorrer os dados linearmente.

Veja o formato do caminho:

    $"{applicationName}_{instrumentationKey}/{type}/{blobDeliveryTimeUtc:yyyy-MM-dd}/{ blobDeliveryTimeUtc:HH}/{blobId}_{blobCreationTimeUtc:yyyyMMdd_HHmmss}.blob"

Where

* `blobCreationTimeUtc` é a hora em que o blob foi criado no armazenamento de preparo interno
* `blobDeliveryTimeUtc` é a hora em que o blob foi copiado para o armazenamento de destino de exportação

## <a name="format"></a> Formato dos dados
* Cada blob é um arquivo de texto que contém várias linhas separadas por “ \n”. Ele contém a telemetria processada durante um período de tempo de aproximadamente metade um minuto.
* Cada linha representa um ponto de dados de telemetria como uma solicitação ou uma exibição de página.
* Cada linha é um documento JSON não formatado. Se você quiser ficar olhando para ele, abra-o no Visual Studio e escolha Editar, Avançado, Arquivo de Formato:

![Veja a telemetria com uma ferramenta adequada](./media/app-insights-export-telemetry/06-json.png)

As durações de tempo são em tiques, em que 10.000 tiques = 1 ms. Por exemplo, esses valores mostram um tempo de 1 ms para enviar uma solicitação do navegador, 3 ms recebê-la e 1,8 s para processar a página no navegador:

    "sendRequest": {"value": 10000.0},
    "receiveRequest": {"value": 30000.0},
    "clientProcess": {"value": 17970000.0}

[Referência de modelo de dados detalhados para os tipos de propriedades e valores.](app-insights-export-data-model.md)

## <a name="processing-the-data"></a>Processamento dos dados
Em pequena escala, você pode escrever um código para extrair e separar seus dados, lê-los em uma planilha e assim por diante. Por exemplo:

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
Observe que você é responsável por gerenciar a capacidade de armazenamento e excluir dados antigos, se necessário.

## <a name="if-you-regenerate-your-storage-key"></a>Se você regenerar sua chave de armazenamento...
Se você alterar a chave para seu armazenamento, a exportação contínua deixará de funcionar. Você verá uma notificação em sua conta do Azure.

Abrir a folha Exportação Contínua e edite sua exportação. Edite o destino de exportação, mas mantenha o mesmo armazenamento selecionado. Clique em OK para confirmar.

![Edite a exportação contínua, abra e feche o destino de exportação.](./media/app-insights-export-telemetry/07-resetstore.png)

A exportação contínua será reiniciada.

## <a name="export-samples"></a>Exemplos de exportação

* [Exportar para o SQL usando o Stream Analytics][exportasa]
* [Exemplo do Stream Analytics 2](app-insights-export-stream-analytics.md)

Em escalas maiores, considere usar o [HDInsight](https://azure.microsoft.com/services/hdinsight/) - clusters de Hadoop na nuvem. O HDInsight fornece várias tecnologias para gerenciar e analisar Big Data, e você pode usá-lo para processar dados que foram exportados do Application Insights.

## <a name="q--a"></a>Perguntas e respostas
* *Mas tudo o que eu quero é um download único de um gráfico.*  

    Sim, você pode fazer isso. Na parte superior da folha, clique **Exportar dados**.
* *Eu configuro uma exportação, mas não há nenhum dado no meu repositório.*

    O Application Insights recebeu qualquer telemetria do seu aplicativo desde que você configurou a exportação? Você receberá apenas novos dados.
* *Eu tentei configurar uma exportação, mas o acesso foi negado*

    Se a conta pertence à sua organização, você precisa ser membro do grupo de proprietários ou do grupo de colaboradores.
* *Eu posso exportar diretamente para meu próprio repositório local?*

    Não, infelizmente. Nosso mecanismo de exportação funciona apenas com o armazenamento do Azure no momento.  
* *Há qualquer limite para a quantidade de dados que você coloca em meu repositório?*

    Não. Continuaremos a enviar dados por push até que você exclua a exportação. Interromperemos o envio se atingirmos os limites externos para o armazenamento de blob, mas são limites enormes. Cabe a você controlar a quantidade de armazenamento que usa.  
* *Quantos blobs devo ver no armazenamento?*

  * Para cada tipo de dados selecionado para exportação, um novo blob é criado a cada minuto (se os dados estiverem disponíveis).
  * Além disso, para aplicativos com tráfego intenso, são alocadas unidades de partição adicionais. Nesse caso, cada unidade cria um blob a cada minuto.
* *Eu regenerei a chave para o meu armazenamento ou alterei o nome do contêiner, e agora a exportação não funciona.*

    Edite a exportação e abra a folha Destino de exportação. Deixe o mesmo armazenamento de antes selecionado e clique em OK para confirmar. A exportação será reiniciada. Se a alteração foi realizada nos últimos dias, você não perderá dados.
* *Posso pausar a exportação?*

    Sim. Clique em Desabilitar.

## <a name="code-samples"></a>Exemplos de código

* [Exemplo do Stream Analytics](app-insights-export-stream-analytics.md)
* [Exportar para o SQL usando o Stream Analytics][exportasa]
* [Referência de modelo de dados detalhados para os tipos de propriedades e valores.](app-insights-export-data-model.md)

<!--Link references-->

[exportasa]: app-insights-code-sample-export-sql-stream-analytics.md
[roles]: app-insights-resources-roles-access-control.md
