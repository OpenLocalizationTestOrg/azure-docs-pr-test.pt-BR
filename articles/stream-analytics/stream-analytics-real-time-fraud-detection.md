# <a name="get-started-using-azure-stream-analytics-real-time-fraud-detection"></a>Introdução ao uso de Stream Analytics do Azure: detecção de fraudes em tempo real

Este tutorial fornece uma ilustração de ponta a ponta de como toouse Stream Analytics do Azure. Você aprenderá como: 

* Colocar o fluxo de eventos em uma instância de Hubs de eventos do Azure. Neste tutorial, você usará um aplicativo que fornecemos que simula um fluxo de registros de metadados de telefone celular.

* Grave dados do tipo SQL Stream Analytics consultas tootransform, agregar informações ou procurando padrões. Você verá como toouse tooexamine uma consulta Olá fluxo de entrada e procure chamadas que podem ser fraudulentas.

* Envie Olá resultados tooan coletor de saída (armazenamento) que você pode analisar informações adicionais. Nesse caso, você enviará o armazenamento de BLOBs do hello chamada suspeitas dados tooAzure.

Neste tutorial, usamos o exemplo hello de detecção de fraudes em tempo real com base nos dados de chamada telefônica. Mas técnica Olá que ilustraremos também é adequada para outros tipos de detecção de fraudes, como um cartão de crédito fraude ou roubo de identidade. 

## <a name="scenario-telecommunications-and-sim-fraud-detection-in-real-time"></a>Cenário: detecção de fraudes de telecomunicações e SIM em tempo real

Uma empresa de telecomunicações tem um grande volume de dados para as chamadas de entrada. empresa de saudação deseja toodetect fraudulenta chamadas em tempo real para que eles possam notificar clientes ou desligar o serviço para um número específico. Um tipo de fraude SIM envolve várias chamadas de saudação mesma identidade ao redor Olá a mesma hora mas em locais geograficamente diferentes. toodetect esse tipo de fraude, Olá registros tooexamine phone entrada necessidades da empresa e procurar padrões específicos – nesse caso, para chamadas feitas ao redor Olá simultaneamente em diferentes países. Os registros de telefone que entram nesta categoria são gravados toostorage para análise posterior.

## <a name="prerequisites"></a>Pré-requisitos

Neste tutorial, você vai simular dados de chamada telefônica usando um aplicativo cliente que gera os metadados de exemplo de chamada telefônica. Alguns dos registros de Olá Olá aplicativo produz a aparência de chamadas fraudulentas. 

Antes de começar, verifique se que você tem o seguinte hello:

* Uma conta do Azure.
* aplicativo de gerador de evento de chamada Hello. Você pode obter isso baixando Olá [TelcoGenerator.zip arquivo](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip) da saudação Microsoft Download Center. Descompacte este pacote em uma pasta no seu computador. Se desejar que o código-fonte toosee hello e aplicativo hello execução em um depurador, você pode obter o código-fonte aplicativo hello de [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

    >[!NOTE]
    >Windows podem bloquear o arquivo. zip de saudação baixado. Se você não pode descompactá-lo, arquivo hello e selecione **propriedades**. Se você vir Olá mensagem "Este arquivo veio de outro computador e pode ser bloqueado toohelp proteger este computador", selecione Olá **desbloquear** opção e, em seguida, clique em **aplicar**.

Se quiser tooexamine Olá resultados do trabalho de análise de fluxo contínuo do hello, você também precisa de uma ferramenta para exibir o conteúdo de saudação de um contêiner de armazenamento de BLOBs do Azure. Se você usar o Visual Studio, você pode usar [ferramentas do Azure para Visual Studio](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) ou [Visual Studio Cloud Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer). Como alternativa, você pode instalar ferramentas autônomas como [Azure Storage Explorer](http://storageexplorer.com/) ou [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction). 

## <a name="create-an-azure-event-hubs-tooingest-events"></a>Criar um evento do Azure tooingest dos hubs de eventos

tooanalyze um fluxo de dados, você *ingestão* -lo no Azure. Uma maneira comum de dados de tooingest é toouse [Hubs de eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md), que permite ingestão milhões de eventos por segundo e, em seguida, processar e armazenar informações de evento hello. Para este tutorial, você criar um hub de eventos e, em seguida, tiver Olá evento de chamada gerador aplicativo enviar chamada dados toothat hub de eventos. Para obter mais informações sobre hubs de eventos, consulte Olá [documentação do Azure Service Bus](https://docs.microsoft.com/en-us/azure/service-bus/).

>[!NOTE]
>Para obter uma versão mais detalhada deste procedimento, consulte [criar um namespace de Hubs de eventos e um hub de eventos usando o portal do Azure de Olá](../event-hubs/event-hubs-create.md). 

### <a name="create-a-namespace-and-event-hub"></a>Criar um hub de evento e de namespace
Neste procedimento, você primeiro criar um namespace de hub de eventos e, em seguida, você pode adicionar um namepsace de toothat do hub de eventos. Namespaces do hub de eventos são usados toologically grupo relacionadas a instâncias de barramento de eventos. 

1. Faça logon no portal do Azure de saudação e clique em **novo** > **Internet das coisas** > **Hub de eventos**. 

2. Em Olá **criar namespace** folha, insira um nome de namespace como `<yourname>-eh-ns-demo`. Você pode usar qualquer nome de namespace hello, mas nome hello deve ser válido para uma URL e deve ser exclusivo no Azure. 
    
3. Selecione uma assinatura e crie ou escolha um grupo de recursos e clique em **Criar**. 

    ![Criar um namespace do hub de eventos](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-namespace-new-portal.png)
 
4. Ao namespace Olá terminou de implantação, encontre hello namespace de hub de eventos na lista de recursos do Azure. 

5. Clique em novo namespace de saudação e na folha de namespace hello, clique em  **+ &nbsp;Hub de eventos**. 

    ![botão de adicionar o Hub de eventos Olá para criar um novo hub de eventos ](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-button-new-portal.png)    
 
6. Nome hello novo hub de eventos `sa-eh-frauddetection-demo`. Você pode usar um nome diferente. Se você fizer isso, anote-lo, porque você precisa de nome hello mais tarde. Você não precisa tooset quaisquer outras opções para o hub de eventos Olá agora.

    ![Folha para a criação de um novo hub de eventos](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-new-portal.png)
    
 
7. Clique em **Criar**.
### <a name="grant-access-toohello-event-hub-and-get-a-connection-string"></a>Conceda o hub de eventos de toohello de acesso e obter uma cadeia de caracteres de conexão

Antes de um processo pode enviar o hub de eventos de tooan de dados, o hub de eventos Olá deve ter uma política que permite o acesso apropriado. política de acesso de saudação produz uma cadeia de caracteres de conexão que inclui informações de autorização.

1.  Na folha de namespace do evento hello, clique em **Hubs de eventos** e, em seguida, clique em nome de saudação do seu novo hub de eventos.

2.  Na folha de hub de evento hello, clique em **políticas de acesso compartilhado** e, em seguida, clique em  **+ &nbsp;adicionar**.

    >[!NOTE]
    >Verifique se que você estiver trabalhando com o hub de eventos hello, não Olá namespace de hub de eventos.

3.  Adicione uma política chamada `sa-policy-manage-demo` e para **Declaração**, selecione **Gerenciar**.

    ![Folha para a criação de uma nova política de acesso de hub de eventos](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-shared-access-policy-manage-new-portal.png)
 
4.  Clique em **Criar**.

5.  Após a implantação de política de saudação, clique na lista de saudação de políticas de acesso compartilhado.

6.  Caixa de saudação localizar **chave primária de cadeia de caracteres de conexão** e clique em cadeia de conexão do hello cópia botão Avançar toohello. 
    
    ![Copiar a chave de cadeia de caracteres de conexão primária de saudação da política de acesso de saudação](./media/stream-analytics-real-time-fraud-detection/stream-analytics-shared-access-policy-copy-connection-string-new-portal.png)
 
7.  Cole a cadeia de caracteres de conexão de saudação em um editor de texto. É necessário essa cadeia de caracteres de conexão para a próxima seção de hello, depois de fazer algumas pequenas edições tooit.

    cadeia de caracteres de conexão Olá tem esta aparência:

        Endpoint=sb://YOURNAME-eh-ns-demo.servicebus.windows.net/;SharedAccessKeyName=sa-policy-manage-demo;SharedAccessKey=Gw2NFZwU1Di+rxA2T+6hJYAtFExKRXaC2oSQa0ZsPkI=;EntityPath=sa-eh-frauddetection-demo

    Observe que a cadeia de caracteres de conexão Olá contém vários pares de chave-valor, separados por ponto e vírgula: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, e `EntityPath`.  

## <a name="configure-and-start-hello-event-generator-application"></a>Configurar e iniciar o aplicativo de gerador de evento hello

Antes de iniciar o aplicativo de TelcoGenerator hello, você configurá-lo para que você acabou de criar hub de eventos chamada registros toohello será enviada.

### <a name="configure-hello-telcogeneratorapp"></a>Configurar Olá TelcoGeneratorapp

1.  No editor de saudação onde você copiou a cadeia de caracteres de conexão hello, anote Olá `EntityPath` valor e, em seguida, remover Olá `EntityPath` par (não se esqueça de tooremove Olá-e-vírgula anterior). 

2.  Na pasta de Olá onde você descompactou Olá TelcoGenerator.zip arquivo, abra o arquivo de telcodatagen.exe.config Olá em um editor. (Há mais de um arquivo. config, portanto certifique-se de que você abrir um direito de saudação).

3.  Em Olá `<appSettings>` elemento, fazer isso:

    * Definir valor Olá Olá `EventHubName` toohello chave nome do hub de evento (ou seja, o valor de toohello do caminho de entidade Olá).
    * Definir valor Olá Olá `Microsoft.ServiceBus.ConnectionString` chave de cadeia de caracteres de conexão toohello. 

    Olá `<appSettings>` seção será semelhante a saudação de exemplo a seguir. (Para maior clareza, é encapsulado linhas hello e removido alguns caracteres do token de autorização hello.)

    ![Arquivo de configuração de aplicativo TelcoGenerator mostrando a sequência de nome e a conexão de hub de evento do hello](./media/stream-analytics-real-time-fraud-detection/stream-analytics-telcogenerator-config-file-app-settings.png)
 
4.  Salve o arquivo hello. 

### <a name="start-hello-app"></a>Iniciar aplicativo hello
1.  Abra uma janela de comando e altere a pasta toohello onde Olá TelcoGenerator aplicativo é descompactado.
2.  Digite hello comando a seguir:

        telcodatagen.exe 1000 .2 2

    Olá parâmetros são: 

    * Número de CDRs por hora. 
    * Probabilidade de fraude de cartão SIM: Frequência, como uma porcentagem de todas as chamadas, que o aplicativo hello deve simular uma chamada fraudulenta. o valor de saudação.2 significa que cerca de 20% dos registros de chamada hello parecerá fraudulentas.
    * Duração em horas. número de saudação de horas que Olá aplicativo deve ser executado. Você também pode parar aplicativo hello qualquer momento pressionando Ctrl + C na linha de comando hello.

    Após alguns segundos, o aplicativo hello inicia exibindo registros de chamada telefônica na tela hello que ele envia toohello hub de eventos.

Alguns dos campos de chave de saudação que você usará neste aplicativo de detecção de fraudes em tempo real são seguinte hello:

|**Registro**|**Definição**|
|----------|--------------|
|`CallrecTime`|Olá carimbo de hora de início de chamada hello. |
|`SwitchNum`|opção de telefone de saudação usada tooconnect chamada de saudação. Neste exemplo, comutadores de saudação são cadeias de caracteres que representam o país de saudação de origem (Estados Unidos, China, Reino Unido, Alemanha ou Austrália). |
|`CallingNum`|número de telefone de saudação do chamador hello. |
|`CallingIMSI`|Olá International Mobile IMSI (Subscriber Identity). Este é o identificador exclusivo de saudação do chamador hello. |
|`CalledNum`|número de telefone de saudação do destinatário da chamada de saudação. |
|`CalledIMSI`|Identidade do Assinante Móvel Internacional (IMSI). Este é o identificador exclusivo de saudação do destinatário da chamada de saudação. |


## <a name="create-a-stream-analytics-job-toomanage-streaming-data"></a>Criar um toomanage de trabalho do Stream Analytics fluxo de dados

Agora que você tem um fluxo de eventos de chamada, você pode configurar um trabalho do Stream Analytics. trabalho de saudação lê dados de hub de eventos de saudação configurado. 

### <a name="create-hello-job"></a>Criar trabalho de saudação 

1. No portal do Azure de Olá, clique em **novo** > **Internet das coisas** > **trabalho do Stream Analytics**.

2. Nome do trabalho Olá `sa_frauddetection_job_demo`, especifique uma assinatura, o grupo de recursos e o local.

    É uma boa ideia tooplace Olá trabalho e hello hub de evento Olá mesma região para melhor desempenho e, portanto, que não é necessário pagar tootransfer dados entre regiões.

    ![Criar um novo trabalho do Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-job-new-portal.png)

3. Clique em **Criar**.

    Olá trabalho é criado e o portal de saudação exibe detalhes do trabalho. Nada ainda estiver em execução, no entanto, você tem o trabalho de saudação tooconfigure antes que ele possa ser iniciado.

### <a name="configure-job-input"></a>Configurar entrada de trabalho

1. No painel de saudação ou hello **todos os recursos** folha, encontre e selecione Olá `sa_frauddetection_job_demo` trabalho do Stream Analytics. 
2. Em Olá **trabalho topologia** seção Olá folha de trabalho do Stream Analytics, clique em Olá **entrada** caixa.

    ![Caixa de entrada em topologia na folha do hello análise de fluxo de trabalho](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-input-box-new-portal.png)
 
3. Clique em  **+ &nbsp;adicionar** e, em seguida, preencha a folha Olá com estes valores:

    * **Alias de entrada**: Use o nome de saudação `CallStream`. Se você usar um nome diferente, anote-o porque você precisará dele depois.
    * **Tipo de Origem**: Selecione **Fluxo de Dados**. (**Dados de referência** refere-se a dados de pesquisa toostatic, que você não usar neste tutorial.)
    * **Origem**: Selecione **hub de eventos**.
    * **Opção de importação**: Selecione **Usar hub de evento da assinatura atual**. 
    * **Namespace de barramento de serviço**: selecione Olá namespace de hub de eventos que você criou anteriormente (`<yourname>-eh-ns-demo`).
    * **Hub de eventos**: hub de eventos Olá selecione que você criou anteriormente (`sa-eh-frauddetection-demo`).
    * **Nome de política do hub de evento**: selecione a política de acesso de saudação que você criou anteriormente (`sa-policy-manage-demo`).

    ![Criar nova entrada para o trabalho de Streaming Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-input-new-portal.png)

4. Clique em **Criar**.

## <a name="create-queries-tootransform-real-time-data"></a>Criar consultas de dados em tempo real tootransform

Neste ponto, você tem um trabalho do Stream Analytics configurar tooread um fluxo de dados de entrada. Olá próxima etapa é toocreate uma transformação que analisa dados de saudação em tempo real. Você pode fazer isso criando uma consulta. O Stream Analytics dá suporte a um modelo de consulta simples e declarativo para descrever as transformações para processamento em tempo real. consultas de saudação usam uma linguagem semelhante a SQL que tem algumas análises de toostream específico de extensões. 

Uma consulta muito simple simplesmente pode ler todos os dados de entrada hello. No entanto, geralmente você criar consultas que procuram dados específicos ou relações nos dados de saudação. Esta seção do tutorial hello, você criará e testar várias consultas toolearn algumas maneiras em que você pode transformar um fluxo de entrada para análise. 

consultas Olá criadas aqui apenas exibirá a tela de toohello hello dados transformados. Em uma seção posterior, você vai configurar um coletor de saída e uma consulta que grava Olá dados transformados toothat coletor.

toolearn mais sobre a linguagem hello, consulte Olá [referência de linguagem do Azure Stream Analytics consulta](https://msdn.microsoft.com/library/dn834998.aspx).

### <a name="get-sample-data-for-testing-queries"></a>Obter dados de exemplo para teste de consultas

Olá TelcoGenerator aplicativo está enviando o hub de eventos de toohello de registros de chamada e o trabalho do Stream Analytics é configurado tooread de hub de eventos de saudação. Você pode usar uma consulta tootest Olá trabalho toomake-se de que está lendo corretamente. muito testar uma consulta em Olá console do Azure, você precisa de dados de exemplo. Para este passo a passo, você vai extrair dados de exemplo de fluxo de saudação que vêm no hub de eventos de saudação.

1. Certifique-se de que TelcoGenerator o aplicativo hello está em execução e gera os registros de chamada.
2. No portal de hello, retorne toohello folha de trabalho de análise de fluxo contínuo. (Se você fechou folha hello, procure `sa_frauddetection_job_demo` em Olá **todos os recursos** folha.)
3. Clique em Olá **consulta** caixa. Azure lista entradas hello e saídas que são configuradas para trabalho hello e permite que você crie uma consulta que permite transform o fluxo de entrada hello como saída toohello é enviado.
4. Em hello **consulta** folha, clique em Olá pontos próximo toohello `CallStream` de entrada e, em seguida, selecione **dados de entrada de exemplo**.

    ![Dados de exemplo do menu Opções toouse para Olá análise de fluxo de trabalho da entrada, "Dados de exemplo de entrada" selecionados](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sample-data-from-input.png)

    Isso abrirá uma folha que permite que você especifique a quantidade tooget de dados de exemplo, definida em termos de quanto tempo o fluxo de entrada hello tooread.

5. Definir **minutos** too3 e, em seguida, clique em **Okey**. 
    
    ![Opções de amostragem de fluxo de entrada hello, com "3 minutos" selecionados.](./media/stream-analytics-real-time-fraud-detection/stream-analytics-input-create-sample-data.png)

    O Azure amostras de amostra de dados de fluxo de entrada hello de 3 minutos e notifica você quando os dados de exemplo hello estão prontos. (Isso pode levar um tempo.) 

dados de exemplo Hello são armazenados temporariamente e estão disponíveis enquanto janela de consulta Olá aberto. Se você fechar a janela de consulta hello, dados de exemplo hello serão descartados e você terá toocreate um novo conjunto de dados de exemplo. 

Como alternativa, você pode obter um arquivo. JSON que contém dados de exemplo de [do GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json)e, em seguida, carregar esse toouse de arquivo. JSON como dados de exemplo para Olá `CallStream` entrada. 

### <a name="test-using-a-pass-through-query"></a>Teste usando uma consulta de passagem

Se você quiser tooarchive todos os eventos, você pode usar tooread uma consulta de passagem todos os campos de Olá na carga de saudação do evento hello.

1. Na janela de consulta hello, insira esta consulta:

        SELECT 
            *
        FROM 
            CallStream

    >[!NOTE]
    >Assim como acontece com SQL, as palavras-chave não diferenciam maiúsculas de minúsculas e espaço em branco não é significativo.

    Nesta consulta, `CallStream` é Olá alias que você especificou ao criar entrada hello. Se você tiver usado um alias diferente, use esse nome.

2. Clique em **Testar**.

    trabalho de análise de fluxo de saudação executa a consulta de saudação em dados de exemplo hello e exibe a saída de hello na parte inferior da saudação da janela de saudação. Isso indica que o hub de eventos hello e trabalho de análise de fluxo contínuo de saudação estão configurados corretamente. (Conforme observado, mais tarde você criará um coletor de saída que Olá consulta possa gravar dados.)

    ![Saída de trabalho do Stream Analytics, mostrando 73 registros gerados](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output.png)

    número exato de saudação de registros que você vê dependerá quantos registros foram capturados em sua amostra de 3 minutos.
 
### <a name="reduce-hello-number-of-fields-using-a-column-projection"></a>Reduzir o número Olá campos usando uma projeção de coluna

Em muitos casos, a análise não precisa de todas as colunas de saudação do fluxo de entrada hello. Você pode usar um tooproject consulta um conjunto menor de retornado de campos que na consulta de passagem de saudação.

1. Alterar consulta Olá Olá código editor toohello seguinte:

        SELECT CallRecTime, SwitchNum, CallingIMSI, CallingNum, CalledNum 
        FROM 
            CallStream

2. Clique em **Testar** novamente. 

    ![Saída de trabalho do Stream Analytics para projeção, mostrando 25 registros gerados](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-projection.png)
 
### <a name="count-incoming-calls-by-region-tumbling-window-with-aggregation"></a>Contagem de chamadas de entrada por região: janela em cascata com agregação

Suponha que você deseja toocount Olá número de chamadas por região. No fluxo de dados, quando você quiser tooperform funções de agregação como contagem, é necessário toosegment Olá fluxo em unidades temporal (uma vez que o próprio fluxo de dados Olá é efetivamente uma infinidade). Você faz isso usando a [função de janela](stream-analytics-window-functions.md) do Streaming Analytics. Em seguida, você pode trabalhar com dados hello dentro dessa janela como uma unidade.

Para essa transformação, você deseja uma sequência de janelas temporais que não se sobrepõem — cada janela terá um conjunto discreto de dados que você pode agrupar e agregar. Esse tipo de janela é chamado tooas um *janela em cascata* . Na janela em cascata de saudação, você pode obter uma contagem de chamadas de entrada hello agrupados por `SwitchNum`, que representa o país Olá que originou a chamada de saudação. 

1. Alterar consulta Olá Olá código editor toohello seguinte:

        SELECT 
            System.Timestamp as WindowEnd, SwitchNum, COUNT(*) as CallCount 
        FROM
            CallStream TIMESTAMP BY CallRecTime 
        GROUP BY TUMBLINGWINDOW(s, 5), SwitchNum

    Essa consulta usa Olá `Timestamp By` palavra-chave em Olá `FROM` cláusula toospecify qual campo de carimbo de hora no hello janela em cascata do fluxo toouse toodefine Olá de entrada. Nesse caso, janela Olá divide dados saudação em segmentos por Olá `CallRecTime` campo em cada registro. (Se nenhum campo for especificado, Olá windowing operação usa tempo de saudação que cada evento chega no hub de eventos de saudação. Consulte "Hora de chegada versus hora do aplicativo" na [Referência de linguagem de consulta de Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx). 

    projeção de saudação inclui `System.Timestamp`, que retorna um carimbo de hora de término hello de cada janela. 

    toospecify que você deseja toouse uma janela em cascata, que você usar o hello [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx) função hello `GROUP BY `cláusula. Função hello, especifique uma unidade de tempo (em qualquer lugar de um dia de tooa microssegundos) e um tamanho de janela (quantas unidades). Neste exemplo, janela em cascata de saudação consiste em intervalos de 5 segundos, para que você obterá uma contagem por país para o valor de cada 5 segundos de chamadas.

2. Clique em **Testar** novamente. Nos resultados de hello, observe que os Olá carimbos de hora em **WindowEnd** estão em incrementos de 5 segundos.

    ![Saída de trabalho do Stream Analytics para agregação, mostrando 13 registros gerados](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-aggregation.png)
 
### <a name="detect-sim-fraud-using-a-self-join"></a>Detectar fraudes SIM usando uma autojunção

Neste exemplo, pode consideramos uso fraudulento toobe chamadas que se originam Olá mesmo usuário, mas em diferentes locais dentro de 5 segundos uma da outra. Por exemplo, hello mesmo usuário não é possível legitimamente fazer uma chamada do hello dos EUA e Austrália no hello simultaneamente. 

toocheck para esses casos, você pode usar uma autojunção da saudação streaming dados toojoin Olá fluxo tooitself com base em Olá `CallRecTime` valor. Você pode, em seguida, procure chamada registra onde hello `CallingIMSI` valor (número de origem Olá) é Olá mesmo, mas Olá `SwitchNum` valor (país de origem) não é Olá mesmo.

Quando você usa uma associação com o fluxo de dados, junção Olá deve fornecer alguns limites no hello quanto a correspondência de linhas podem ser separados no tempo. (Como observado anteriormente, Olá fluxo de dados é efetivamente uma infinidade.) limites de tempo de saudação para relação Olá são especificados dentro Olá `ON` cláusula de junção hello, usando Olá `DATEDIFF` função. Nesse caso, a junção de Olá é baseada em um intervalo de 5 segundos de dados de chamada.

1. Alterar consulta Olá Olá código editor toohello seguinte: 

        SELECT  System.Timestamp as Time, 
            CS1.CallingIMSI, 
            CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, 
            CS1.SwitchNum as Switch1, 
            CS2.SwitchNum as Switch2 
        FROM CallStream CS1 TIMESTAMP BY CallRecTime 
            JOIN CallStream CS2 TIMESTAMP BY CallRecTime 
            ON CS1.CallingIMSI = CS2.CallingIMSI 
            AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5 
        WHERE CS1.SwitchNum != CS2.SwitchNum

    Essa consulta é como qualquer associação SQL, exceto Olá `DATEDIFF` função na junção hello. Esta é uma versão de `DATEDIFF` tooStreaming específico análise, e ele deve aparecer no hello `ON...BETWEEN` cláusula. parâmetros de saudação são aliases de saudação de duas fontes Olá para junção Olá e uma unidade de tempo (segundos neste exemplo). (Isso é diferente do hello SQL padrão `DATEDIFF` função.) 

    Olá `WHERE` cláusula inclui condição Olá sinalizadores chamada fraudulentas Olá: opções de origem Olá não são Olá mesmo. 

2. Clique em **Testar** novamente. 

    ![Saída de trabalho do Stream Analytics para autojunção, mostrando 6 registros gerados](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-self-join.png)

3. Clique em **Salvar**. Isso salva a consulta de associação a mesmo de saudação como parte do trabalho de análise de fluxo contínuo de saudação. (Ele não salva os dados de exemplo hello.)

    ![Salvar o trabalho do Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-query-editor-save-button-new-portal.png)

## <a name="create-an-output-sink-toostore-transformed-data"></a>Criar um coletor de saída toostore transformado dados

Você definiu um fluxo de eventos, uma entrada tooingest do hub de eventos e uma consulta tooperform uma transformação em fluxo hello. Olá última etapa é toodefine um coletor de saída para o trabalho de saudação — ou seja, uma saudação de toowrite local transformado fluxo para. 

Você pode usar muitos recursos como coletores de saída — um banco de dados do SQL Server, o armazenamento de tabela, armazenamento do Data Lake, Power BI e até mesmo outro hub de eventos. Para este tutorial, você escreverá Olá fluxo tooAzure armazenamento de Blob, que é uma opção típica para coletar informações de evento para análise posterior, já que inclua dados não estruturados.

Se você tiver uma conta de armazenamento de Blobs existente, poderá usá-la. Para este tutorial, vamos mostrar como toocreate um nova conta de armazenamento para este tutorial.

### <a name="create-an-azure-blob-storage-account"></a>Criar uma conta de Armazenamento de Blobs do Azure

1. Olá portal do Azure, retorne toohello folha de trabalho de análise de fluxo contínuo. (Se você fechou folha hello, procure `sa_frauddetection_job_demo` em Olá **todos os recursos** folha.)
2. Em Olá **trabalho topologia** seção, clique em Olá **saída** caixa. 
3. Em Olá **saídas** folha, clique em  **+ &nbsp;adicionar** e, em seguida, preencha a folha Olá com estes valores:

    * **Alias de saída**: Use o nome de saudação `CallStream-FraudulentCalls`. 
    * **Coletor**: selecione **Armazenamento de blobs**.
    * **Opções de importação**: Selecione **Usar armazenamento de blobs da assinatura atual**.
    * **Conta de armazenamento**. Selecione **Criar nova conta de armazenamento.**
    * **Conta de armazenamento** (segunda caixa). Digite `YOURNAMEsademo`, onde `YOURNAME` é o seu nome ou outra cadeia de caracteres exclusiva. nome de saudação pode usar apenas letras minúsculas e números e deve ser exclusivo no Azure. 
    * **Contêiner**. Digite `sa-fraudulentcalls-demo`.
    nome de conta de armazenamento Hello e o nome do contêiner são tooprovide usado junto um URI para o armazenamento de blob hello, como este: 

    `http://yournamesademo.blob.core.windows.net/sa-fraudulentcalls-demo/...`
    
    ![Folha "Nova saída" para trabalho do Stream Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-output-blob-storage-new-console.png)
    
4. Clique em **Criar**. 

    Azure cria a conta de armazenamento hello e gera uma chave automaticamente. 

5. Olá fechar **saídas** folha. 

## <a name="start-hello-streaming-analytics-job"></a>Iniciar Olá análise de fluxo de trabalho

trabalho de saudação agora está configurado. Você especificou uma entrada (hub de eventos de saudação), uma transformação (Olá toolook de consulta para chamadas fraudulentas) e uma saída (armazenamento de blob). Agora você pode iniciar o trabalho de saudação. 

1. Certifique-se de saudação TelcoGenerator aplicativo está em execução.

2. Na folha de trabalho hello, clique em **iniciar**.

    ![Iniciar o trabalho de análise de fluxo de saudação](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-output.png)

3. Em Olá **Iniciar trabalho** folha para a hora de início saída trabalho, selecione **agora**. 

4. Clique em **Iniciar**. 

    ![Folha "Iniciar o trabalho" para o trabalho de análise de fluxo de saudação](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-job-blade.png)

    Azure notifica quando o trabalho Olá foi iniciado e, na folha de trabalho hello, status de saudação é exibido como **executando**.

    ![Status do trabalho de Stream Analytics, mostrando "Em execução"](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-running-status.png)
    

## <a name="examine-hello-transformed-data"></a>Examine os dados transformado de saudação

Agora você tem um trabalho de Streaming Analytics completo. trabalho de saudação é examinando um fluxo de metadados de chamada telefônica, procurando fraudulentas chamadas telefônicas em tempo real e gravar as informações sobre essas chamadas fraudulentas toostorage. 

toocomplete neste tutorial, talvez você queira toolook dados Olá sejam capturados pelo trabalho de análise de fluxo contínuo de saudação. dados Hello está sendo gravados tooAzure armazenamento de Blog em partes (arquivos). Você pode usar qualquer ferramenta que leia o armazenamento de Blobs do Azure. Conforme observado na seção pré-requisitos do hello, você pode usar extensões do Azure no Visual Studio, ou você pode usar uma ferramenta como [Azure Storage Explorer](http://storageexplorer.com/) ou [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction). 

Ao examinar o conteúdo de saudação de um arquivo no armazenamento de blob, você ver algo como Olá a seguir:

![Armazenamento de Blobs do Azure com saída de Streaming Analytics](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-blob-storage-view.png)
 

## <a name="clean-up-resources"></a>Limpar recursos

Temos artigos adicionais que continue com o cenário de detecção de fraudes hello e que usam recursos Olá criado por você neste tutorial. Se você quiser toocontinue, consulte sugestões de saudação em **próximas etapas** mais tarde.

No entanto, se tiver terminado e você não precisa de recursos de saudação que você criou, você pode excluí-los para que não imponha o Azure cobra desnecessário. Nesse caso, sugerimos que você Olá a seguir:

1. Interrompa o trabalho de análise de fluxo contínuo de saudação. Em Olá **trabalhos** folha, clique em **parar** na parte superior da saudação.
2. Pare o aplicativo de telecomunicações gerador de saudação. Na janela de comando Olá onde você iniciou o aplicativo hello, pressione Ctrl + C.
3. Se você criou uma nova conta de armazenamento de blobs apenas para este tutorial, exclua essa conta. 
4. Exclua Olá análise de fluxo de trabalho.
5. Exclua hub de eventos de saudação.
6. Exclua o namespace de hub de eventos de saudação.

## <a name="get-support"></a>Obtenha suporte

Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas

Você pode continuar este tutorial com hello artigos a seguir:

* [Stream Analytics e Power BI: um dashboard de análise em tempo real para fluxo de dados](stream-analytics-power-bi-dashboard.md). Este artigo mostra como toosend Olá saída de telecomunicações de saudação do Stream Analytics trabalho tooPower BI para visualização em tempo real e análise.
* [Como os dados de toostore do Azure Stream Analytics em um Cache Redis do Azure usando funções do Azure](stream-analytics-functions-redis.md). Este artigo mostra como toouse funções do Azure toowrite fraudulenta chama tooan Azure Redis cache por meio de uma fila do barramento de serviço.

Para obter mais informações sobre Stream Analytics em geral, leia estes artigos:

* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
