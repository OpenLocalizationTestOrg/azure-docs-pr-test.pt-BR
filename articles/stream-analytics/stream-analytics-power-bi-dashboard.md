---
title: Painel de BI aaaPower no Azure Stream Analytics | Microsoft Docs
description: Use um em tempo real streaming Power BI painel toogather de business intelligence e analisar dados de alto volume de um trabalho do Stream Analytics.
keywords: "painel de análise, painel em tempo real"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: fe8db732-4397-4e58-9313-fec9537aa2ad
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: jeffstok
ms.openlocfilehash: cb9127576230e9d327b437b674f31cc23869bfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-and-power-bi-a-real-time-analytics-dashboard-for-streaming-data"></a>Stream Analytics e Power BI: um painel de análise em tempo real para dados de streaming
Análise de fluxo do Azure permite que você tootake aproveitar uma saudação principais ferramentas de business intelligence, [Microsoft Power BI](https://powerbi.com/). Neste artigo, você saberá como criar ferramentas de business intelligence usando o Power BI como uma saída de seus trabalhos do Stream Analytics do Azure. Você também aprenderá como toocreate e use um dashboard em tempo real.

Este artigo dá continuidade de saudação do Stream Analytics [detecção de fraudes em tempo real](stream-analytics-real-time-fraud-detection.md) tutorial. Ele se baseia no fluxo de trabalho de saudação criado neste tutorial e adiciona um Power BI para que você pode visualizar fraudulentas chamadas telefônicas que são detectadas por um trabalho de análise de fluxo de saída. 

Você pode assistir a [um vídeo](https://www.youtube.com/watch?v=SGUpT-a99MA) que ilustra esse cenário.


## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, verifique se que você tem o seguinte hello:

* Uma conta do Azure.
* Uma conta para o Power BI. Você pode usar uma conta corporativa ou de estudante.
* Uma versão completa do hello [detecção de fraudes em tempo real](stream-analytics-real-time-fraud-detection.md) tutorial. tutorial de saudação inclui um aplicativo que gera metadados fictícios de chamada telefônica. Tutorial Olá, crie um hub de eventos e enviar Olá streaming hub de eventos de toohello de dados de chamada telefônica. Você escrever uma consulta que detecta chamadas fraudulentas (chamadas de saudação mesmo número no Olá a mesma hora em diferentes locais). 


## <a name="add-power-bi-output"></a>Adicionar saída do Power BI
Tutorial de detecção de fraudes em tempo real de hello, saída de saudação é enviada tooAzure armazenamento de Blob. Nesta seção, você deve adicionar uma saída que envia informações tooPower BI.

1. Olá portal do Azure, abra o trabalho de análise de fluxo contínuo de saudação que você criou anteriormente. Se você usou o nome sugerido hello, Olá trabalho é chamado de `sa_frauddetection_job_demo`.

2. Selecione Olá **saídas** caixa no meio de saudação do painel de trabalho hello e, em seguida, selecione **+ adicionar**.

3. Para **Alias de Saída**, digite `CallStream-PowerBI`. Você pode usar um nome diferente. Se você fizer isso, anote-lo, porque você precisa de nome hello mais tarde. 

4. Em **Coletor**, selecione **Power BI**.

   ![Criar uma saída para o Power BI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut.png)

5. Clique em **Autorizar**.

    É aberta uma janela em que você pode fornecer suas credenciais do Azure para uma conta corporativa ou de estudante. 

    ![Insira as credenciais para acesso tooPower BI](./media/stream-analytics-power-bi-dashboard/authorize-area.png)

6. Insira suas credenciais. Lembre-se, em seguida, quando você inserir suas credenciais, você está também concedendo permissão toohello análise de fluxo de trabalho tooaccess sua área de Power BI.

7. Quando você retornar toohello **nova saída** folha, digite Olá informações a seguir:

    * **Espaço de trabalho de grupo**: selecione um espaço de trabalho em seu locatário do Power BI em que você deseja toocreate Olá dataset.
    * **Nome do Conjunto de Dados**: insira `sa-dataset`. Você pode usar um nome diferente. Se você fizer isso, anote-o para mais tarde.
    * **Nome da Tabela**: insira `fraudulent-calls`. Atualmente, a saída do Power BI de trabalhos do Stream Analytics só podem ter uma tabela em um conjunto de dados.

    ![Espaço de trabalho de PBI](./media/stream-analytics-power-bi-dashboard/create-pbi-ouptut-with-dataset-table.png)

    > [!WARNING]
    > Se o Power BI tem um conjunto de dados e tabela Olá mesmos nomes de saudação aquelas que você especificar no trabalho do Stream Analytics hello, Olá existentes é substituído.
    > Recomendamos que você não crie explicitamente esse conjunto de dados e a tabela em sua conta do Power BI. Eles são criados automaticamente quando você iniciar o trabalho do Stream Analytics e Olá inicia bombeamento de saída para o Power BI. Se sua consulta de trabalho não retornar nenhum resultado, tabela e conjunto de dados de saudação não são criados.
    >

8. Clique em **Criar**.

saudação de conjunto de dados é criado com hello configurações a seguir:

* **defaultRetentionPolicy: BasicFIFO**: os dados são FIFO, no máximo com 200 mil linhas.
* **defaultMode: pushStreaming**: Olá conjunto de dados oferece suporte a streaming blocos e visuais tradicionais baseado no relatório (também conhecido como push).

Atualmente, não é possível criar conjuntos de dados com outros sinalizadores.

Para obter mais informações sobre conjuntos de dados do Power BI, consulte Olá [API REST do Power BI](https://msdn.microsoft.com/library/mt203562.aspx) referência.


## <a name="write-hello-query"></a>Gravar consulta Olá

1. Olá fechar **saídas** folha e retorno toohello folha de trabalho.

2. Clique em Olá **consulta** caixa. 

3. Digite hello consulta a seguir. Essa consulta é semelhante toohello autojunção consulta que você criou no tutorial de detecção de fraudes hello. Olá diferença é que essa consulta envia resultados toohello nova saída criada (`CallStream-PowerBI`). 

    >[!NOTE]
    >Se você não nome de entrada hello `CallStream` no tutorial de detecção de fraudes hello, substitua o seu nome para `CallStream` em Olá **FROM** e **INGRESSAR** cláusulas na consulta de saudação.

        /* Our criteria for fraud:
        Calls made from hello same caller tootwo phone switches in different locations (for example, Australia and Europe) within five seconds */

        SELECT System.Timestamp AS WindowEnd, COUNT(*) AS FraudulentCalls
        INTO "CallStream-PowerBI"
        FROM "CallStream" CS1 TIMESTAMP BY CallRecTime
        JOIN "CallStream" CS2 TIMESTAMP BY CallRecTime

        /* Where hello caller is hello same, as indicated by IMSI (International Mobile Subscriber Identity) */
        ON CS1.CallingIMSI = CS2.CallingIMSI

        /* ...and date between CS1 and CS2 is between one and five seconds */
        AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5

        /* Where hello switch location is different */
        WHERE CS1.SwitchNum != CS2.SwitchNum
        GROUP BY TumblingWindow(Duration(second, 1))

4. Clique em **Salvar**.


## <a name="test-hello-query"></a>Consulta de saudação do teste
Esta etapa é opcional, mas recomendada. 

1. Se Olá TelcoStreaming app não estiver em execução, inicie-o seguindo estas etapas:

    * Abra uma janela de comando.
    * Vá toohello pasta onde Olá telcogenerator.exe e arquivos telcodatagen.exe.config modificado.
    * Execute Olá comando a seguir:

            telcodatagen.exe 1000 .2 2

2. Em hello **consulta** folha, clique em Olá pontos próximo toohello `CallStream` de entrada e, em seguida, selecione **dados de entrada de exemplo**.

3. Especifique que você deseja dados equivalentes a três minutos e clique em **OK**. Aguarde até que você é notificado de que dados saudação foram amostrados.

4. Clique em **Teste** e verifique se você está obtendo resultados.


## <a name="run-hello-job"></a>Executar trabalho Olá

1. Certifique-se de que o aplicativo TelcoStreaming hello está em execução.

2. Olá fechar **consulta** folha.

3. Na folha de trabalho hello, clique em **iniciar**.

    ![Iniciar o trabalho de análise de fluxo de saudação](./media/stream-analytics-power-bi-dashboard/stream-analytics-sa-job-start-output.png)

O trabalho de análise de fluxo inicia procurando fraudulentas chamadas no fluxo de entrada hello. trabalho de saudação também cria Olá conjunto de dados e tabela no Power BI e começa a enviar dados sobre Olá fraudulentas chamadas toothem.


## <a name="create-hello-dashboard-in-power-bi"></a>Criar um painel Olá no Power BI

1. Vá muito[Powerbi.com](https://powerbi.com) e entre com sua conta corporativa ou escolar. Se a consulta de trabalho do Stream Analytics hello gera resultados, verá que o conjunto de dados já foi criado:

    ![Conjunto de dados de streaming no Power BI](./media/stream-analytics-power-bi-dashboard/streaming-dataset.png)

2. No espaço de trabalho, clique em **+&nbsp;Criar**.

    ![botão de criar Olá no espaço de trabalho do Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard.png)

3. Crie um novo painel e nomeie-o `Fraudulent Calls`.

    ![Crie um painel e dê a ele um nome no espaço de trabalho do Power BI](./media/stream-analytics-power-bi-dashboard/pbi-create-dashboard-name.png)

4. Na parte superior de saudação da janela de saudação, clique em **Adicionar bloco**, selecione **fluxo de dados personalizado**e, em seguida, clique em **próximo**.

    ![Conjunto de dados de streaming personalizado](./media/stream-analytics-power-bi-dashboard/custom-streaming-data.png)

5. Em **SEUS CONJUNTOS DE DADOS**, selecione o conjunto de dados e, em seguida, clique em **Avançar**.

    ![Seu conjunto de dados de streaming](./media/stream-analytics-power-bi-dashboard/your-streaming-dataset.png)

6. Em **tipo de visualização**, selecione **cartão**e, em seguida, em Olá **campos** lista, selecione **fraudulentcalls**.

    ![Detalhes da visualização para o novo bloco](./media/stream-analytics-power-bi-dashboard/add-fraud.png)

7. Clique em **Avançar**.

8. Preencha os detalhes do bloco, tais como um título e subtítulo.

    ![Título e subtítulo para o novo bloco](./media/stream-analytics-power-bi-dashboard/pbi-new-tile-details.png)

9. Clique em **Aplicar**.

    Agora você tem um contador de fraudes!

    ![Contador de fraudes](./media/stream-analytics-power-bi-dashboard/fraud-counter.png)

8. Olá siga etapas novamente tooadd um bloco (começando com a etapa 4). Neste momento, Olá a seguir:

    * Quando você obtém muito**tipo de visualização**, selecione **gráfico de linhas**. 
    * Adicionar um eixo e selecione **windowend**. 
    * Adicione um valor e selecione **fraudulentcalls**.
    * Para **toodisplay da janela de tempo**, selecione Olá últimos 10 minutos.

    ![Criar um bloco para o gráfico de linhas](./media/stream-analytics-power-bi-dashboard/pbi-create-tile-line-chart.png)

9. Clique em **Avançar**, adicione um título e subtítulo e clique em **Aplicar**.

    painel do Power BI Olá agora oferece dois modos de exibição de dados sobre chamadas fraudulentas conforme detectado no hello fluxo de dados.

    ![O painel do Power BI foi concluído mostrando dois blocos para chamadas fraudulentas](./media/stream-analytics-power-bi-dashboard/pbi-dashboard-fraudulent-calls-finished.png)


## <a name="learn-more-about-power-bi"></a>Saiba mais sobre o Power BI

Este tutorial demonstra como toocreate apenas alguns tipos de visualizações de um conjunto de dados. O Power BI pode ajudá-lo a criar outras ferramentas de cliente business intelligence para sua organização. Para obter mais ideias, consulte Olá recursos a seguir:

* Outro exemplo de um painel do Power BI, assista a saudação [guia de Introdução ao Power BI](https://youtu.be/L-Z_6P56aas?t=1m58s) vídeo.
* Para obter mais informações sobre como configurar a análise de fluxo de trabalho saída tooPower BI e usando grupos do Power BI, examine a saudação [Power BI](stream-analytics-define-outputs.md#power-bi) seção Olá [do Stream Analytics gera](stream-analytics-define-outputs.md) artigo. 
* Para obter informações sobre como usar o Power BI em geral, consulte [Painéis no Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-dashboards/).


## <a name="learn-about-limitations-and-best-practices"></a>Saiba mais sobre limitações e práticas recomendadas
Atualmente, o Power BI pode ser chamado aproximadamente uma vez por segundo. A transmissão de elementos visuais oferece suporte a pacotes de 15 KB. Além disso, falham de streaming visuais (mas push continua toowork). Devido a essas limitações, Power BI Preste mais naturalmente toocases onde Stream Analytics do Azure reduz uma quantidade significativa de dados de carga. É recomendável usar uma janela em cascata ou Hopping janela tooensure dados por push está no máximo um envio por segundo, e se sua consulta cair dentro dos requisitos de taxa de transferência de saudação.

Você pode usar o hello seguinte equação toocompute Olá valor toogive a janela em segundos:

![Equação1](./media/stream-analytics-power-bi-dashboard/equation1.png)  

Por exemplo:

* Você tem 1.000 dispositivos que enviam dados em intervalos de um segundo.
* Você está usando Olá Power BI SKU Pro que suporta 1.000.000 linhas por hora.
* Você deseja toopublish quantidade de saudação da média de dados por dispositivo tooPower BI.

Como resultado, a equação de saudação se torna:

![Equação2](./media/stream-analytics-power-bi-dashboard/equation2.png)  

Dada essa configuração, você pode alterar a seguir original de toohello consulta hello:

    SELECT
        MAX(hmdt) AS hmdt,
        MAX(temp) AS temp,
        System.TimeStamp AS time,
        dspl
    INTO "CallStream-PowerBI"
    FROM
        Input TIMESTAMP BY time
    GROUP BY
        TUMBLINGWINDOW(ss,4),
        dspl


### <a name="renew-authorization"></a>Renovar autorização
Se Olá senha alterada desde que o trabalho foi criado ou última autenticado, será necessário tooreauthenticate sua conta do Power BI. Se o Azure multi-Factor Authentication está configurado no seu locatário do Azure Active Directory (AD do Azure), você também precisará autorização do Power BI de toorenew a cada duas semanas. Se você não renovar, você pode ver os sintomas como falta de saída de trabalho ou um `Authenticate user error` nos logs de operação de saudação.

Da mesma forma, se um trabalho é iniciado depois Olá token tiver expirado, ocorrerá um erro e Olá trabalho falhar. tooresolve esse problema, parar trabalho Olá que está em execução e ir tooyour Power BI de saída. tooavoid perda de dados, selecione Olá **renovar autorização** link e, em seguida, reinicie o trabalho de saudação **hora da última interrupção**.

Após a autorização Olá foi atualizada com o Power BI, um alerta verde é exibida em Olá autorização área tooreflect que problema Olá foi resolvido.

## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de linguagem de consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn835031.aspx)
