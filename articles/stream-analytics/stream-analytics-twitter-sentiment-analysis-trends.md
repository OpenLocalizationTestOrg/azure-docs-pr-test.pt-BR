---
title: "análise de sentimento do Twitter aaaReal tempo com o Azure Stream Analytics | Microsoft Docs"
description: "Saiba como toouse do Stream Analytics para análise de sentimento do Twitter em tempo real. Orientações passo a passo de toodata de geração de eventos em um painel ativo."
keywords: "análise de tendência do twitter em tempo real, análise de sentimento, análise de mídia social, exemplo de análise de tendência"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42068691-074b-4c3b-a527-acafa484fda2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: jeffstok
ms.openlocfilehash: 157790caa7ea6f5570dd9c9d3bd9694d437eb4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="real-time-twitter-sentiment-analysis-in-azure-stream-analytics"></a>Análise de sentimento do Twitter em tempo real no Stream Analytics do Azure

Saiba como uma solução de análise de sentimento para análise de mídia social, colocando em tempo real de toobuild Twitter eventos para Hubs de eventos do Azure. Em seguida, você pode escrever um Stream Analytics do Azure consultar tooanalyze Olá dados e um repositório Olá resultados para uso posterior ou use um painel e [Power BI](https://powerbi.com/) tooprovide insights em tempo real.

As ferramentas de análise de mídias sociais ajudam as organizações a compreender os tópicos mais populares. Os tópicos mais populares são entidades e atitudes com um alto volume de postagens em mídia social. Análise de sentimento, que também é chamado *mineração opinião*, usa posturas de toodetermine de ferramentas de análise de mídia social para um produto, ideia e assim por diante. 

Análise de tendência do Twitter em tempo real é um ótimo exemplo de uma ferramenta de análise, porque o modelo de assinatura de hashtag Olá permite que você toolisten toospecific palavras-chave (hashtags) e desenvolver a análise de sentimento de saudação feed.

## <a name="scenario-social-media-sentiment-analysis-in-real-time"></a>Cenário: Análise de sentimento de mídia social em tempo real

Uma empresa que tem um site de mídia está interessa em obter uma vantagem sobre a concorrência apresentando o conteúdo do site que está imediatamente relevantes tooits leitores. empresa de saudação usa análise de mídia social sobre tópicos que são relevantes tooreaders ao fazer a análise de sentimento em tempo real dos dados do Twitter.

tópicos de análise de tendências de tooidentify em tempo real no Twitter, Olá necessidades de empresa análise em tempo real sobre volume de tweet hello e sentimento tópicos chave. Em outras palavras, a necessidade de saudação é um mecanismo de análise de análise de sentimento que se baseia a esta mídia social feed.

## <a name="prerequisites"></a>Pré-requisitos
Neste tutorial, você deve usar um aplicativo cliente que se conecta tooTwitter e procura tweets com determinados hashtags (que pode ser definida). Em ordem toorun Olá aplicativo e analisar Olá tweets usando a análise de fluxo do Azure, você deve ter o seguinte hello:

* Uma assinatura do Azure
* Uma conta do Twitter 
* Um aplicativo do Twitter e hello [token de acesso OAuth](https://dev.twitter.com/oauth/overview/application-owner-access-tokens) para o aplicativo. Podemos fornecer instruções de alto nível sobre como toocreate um aplicativo do Twitter mais tarde.
* aplicativo de TwitterWPFClient Hello, que lê Olá Twitter feed. tooget esse aplicativo, o download Olá [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) do GitHub de arquivo e, em seguida, descompacte o pacote de saudação em uma pasta no seu computador. Se desejar que o código-fonte toosee hello e executar o aplicativo hello em um depurador, você pode obter o código-fonte Olá de [GitHub](https://aka.ms/azure-stream-analytics-telcogenerator). 

## <a name="create-an-event-hub-for-streaming-analytics-input"></a>Criar um hub de eventos para entrada do Streaming Analytics

aplicativo de exemplo Hello gera eventos e envia-os tooan hub de eventos do Azure. Hubs de eventos do Azure são método hello preferido de inclusão de eventos para análise de fluxo. Para obter mais informações, consulte Olá [documentação de Hubs de eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md).


### <a name="create-an-event-hub-namespace-and-event-hub"></a>Criar um namespace de hub de eventos e um hub de eventos
Neste procedimento, você primeiro criar um namespace de hub de eventos e, em seguida, você pode adicionar um namespace de toothat do hub de eventos. Namespaces do hub de eventos são usados toologically grupo relacionadas a instâncias de barramento de eventos. 

1. Faça logon no portal do Azure de toohello e clique em **novo** > **Internet das coisas** > **Hub de eventos**. 

2. Em Olá **criar namespace** folha, insira um nome de namespace como `<yourname>-socialtwitter-eh-ns`. Você pode usar qualquer nome de namespace hello, mas nome hello deve ser válido para uma URL e deve ser exclusivo no Azure. 
    
3. Selecione uma assinatura e crie ou escolha um grupo de recursos e clique em **Criar**. 

    ![Criar um namespace do hub de eventos](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-namespace.png)
 
4. Ao namespace Olá terminou de implantação, encontre hello namespace de hub de eventos na lista de recursos do Azure. 

5. Clique em novo namespace de saudação e na folha de namespace hello, clique em  **+ &nbsp;Hub de eventos**. 

    ![botão de adicionar o Hub de eventos Olá para criar um novo hub de eventos ](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub-button.png)    
 
6. Nome hello novo hub de eventos `socialtwitter-eh`. Você pode usar um nome diferente. Se você fizer isso, anote-lo, porque você precisa de nome hello mais tarde. Você não precisa tooset quaisquer outras opções para o hub de eventos de saudação.

    ![Folha para a criação de um novo hub de eventos](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-eventhub.png)
 
7. Clique em **Criar**.


### <a name="grant-access-toohello-event-hub"></a>Hub de eventos de toohello conceder acesso

Antes de um processo pode enviar o hub de eventos de tooan de dados, o hub de eventos Olá deve ter uma política que permite o acesso apropriado. política de acesso de saudação produz uma cadeia de caracteres de conexão que inclui informações de autorização.

1.  Na folha de namespace do evento hello, clique em **Hubs de eventos** e, em seguida, clique em nome de saudação do seu novo hub de eventos.

2.  Na folha de hub de evento hello, clique em **políticas de acesso compartilhado** e, em seguida, clique em  **+ &nbsp;adicionar**.

    >[!NOTE]
    >Verifique se que você estiver trabalhando com o hub de eventos hello, não Olá namespace de hub de eventos.

3.  Adicione uma política chamada `socialtwitter-access` e para **Declaração**, selecione **Gerenciar**.

    ![Folha para a criação de uma nova política de acesso de hub de eventos](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-shared-access-policy-manage.png)
 
4.  Clique em **Criar**.

5.  Após a implantação de política de saudação, clique na lista de saudação de políticas de acesso compartilhado.

6.  Caixa de saudação localizar **chave primária de cadeia de caracteres de conexão** e clique em cadeia de conexão do hello cópia botão Avançar toohello. 
    
    ![Copiar a chave de cadeia de caracteres de conexão primária de saudação da política de acesso de saudação](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-shared-access-policy-copy-connection-string.png)
 
7.  Cole a cadeia de caracteres de conexão de saudação em um editor de texto. É necessário essa cadeia de caracteres de conexão para a próxima seção de hello, depois de fazer algumas pequenas edições tooit.

    cadeia de caracteres de conexão Olá tem esta aparência:

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=;EntityPath=socialtwitter-eh

    Observe que a cadeia de caracteres de conexão Olá contém vários pares de chave-valor, separados por ponto e vírgula: `Endpoint`, `SharedAccessKeyName`, `SharedAccessKey`, e `EntityPath`.  

    > [!NOTE]
    > Para segurança, partes da cadeia de conexão Olá no exemplo hello foram removidos.

8.  No editor de texto de saudação, remover Olá `EntityPath` par de cadeia de caracteres de conexão de saudação (não se esqueça de tooremove Olá-e-vírgula anterior). Quando terminar, cadeia de caracteres de conexão Olá terá esta aparência:

        Endpoint=sb://YOURNAME-socialtwitter-eh-ns.servicebus.windows.net/;SharedAccessKeyName=socialtwitter-access;SharedAccessKey=Gw2NFZw6r...FxKbXaC2op6a0ZsPkI=


## <a name="configure-and-start-hello-twitter-client-application"></a>Configurar e iniciar o aplicativo de cliente do Twitter hello
aplicativo de cliente Hello obtém eventos tweet diretamente do Twitter. Em ordem toodo isso, é necessário Olá toocall de permissão do Twitter APIs de Streaming. tooconfigure que permissão, você cria um aplicativo no Twitter, que gera as credenciais exclusivas (por exemplo, um token de OAuth). Você pode configurar toouse de aplicativo cliente Olá essas credenciais ao fazer chamadas de API. 

### <a name="create-a-twitter-application"></a>Criar um aplicativo do Twitter
Se você ainda não tiver um aplicativo do Twitter que você possa usar para este tutorial, você pode criar um. Você já deve ter uma conta do Twitter.

> [!NOTE]
> exato do processo no Twitter para criar um aplicativo e obter o token, segredos e chaves de Olá Olá pode ser alterado. Se essas instruções não corresponderem, o que você vê no site do Twitter Olá, consulte a documentação do desenvolvedor do Twitter toohello.

1. Vá toohello [página de gerenciamento de aplicativo do Twitter](https://apps.twitter.com/). 

2. Crie um aplicativo novo. 

    * Para a URL do site hello, especifique uma URL válida. Ele não tem toobe um site ativo. (Você não pode especificar apenas `localhost`.)
    * Deixe o campo de retorno de chamada de saudação em branco. aplicativo de cliente Hello que usar para este tutorial não requer retornos de chamada.

    ![Criando um aplicativo no Twitter](./media/stream-analytics-twitter-sentiment-analysis-trends/create-twitter-application.png)

3. Opcionalmente, altere as permissões do aplicativo hello somente tooread.

4. Quando o aplicativo hello é criado, acesse toohello **chaves e Tokens de acesso** página.

5. Clique em Olá botão toogenerate um token de acesso e o segredo do token de acesso.

Mantenha essas informações úteis, pois você precisará no procedimento a seguir hello.

>[!NOTE]
>chaves de saudação e segredos do aplicativo do Twitter hello fornecem acesso tooyour Twitter conta. Tratar essas informações como confidenciais, Olá mesmo como fazer sua senha do Twitter. Por exemplo, não insira essas informações em um aplicativo que você forneça tooothers. 


### <a name="configure-hello-client-application"></a>Configurar o aplicativo de cliente hello
Criamos um aplicativo cliente que se conecta tooTwitter dados usando [APIs de Streaming do Twitter](https://dev.twitter.com/streaming/overview) toocollect eventos de tweet sobre um conjunto específico de tópicos. usa o aplicativo Hello Olá [Sentiment140](http://help.sentiment140.com/) ferramenta de software livre, que atribui Olá tweet de tooeach do valor de sensibilidade a seguir:

* 0 = negativo
* 2 = neutro
* 4 = positivo

Depois de eventos de tweet Olá atribuiu um valor de sensibilidade, eles são enviados por push toohello hub de eventos que você criou anteriormente.

Antes que o aplicativo hello é executado, ele requer certas informações, como chaves de Twitter hello e cadeia de conexão de hub de evento hello. Você pode fornecer informações de configuração de saudação das seguintes maneiras:

* Executar o aplicativo hello e use do aplicativo hello da interface do usuário tooenter Olá chaves, segredos e cadeia de caracteres de conexão. Se você fizer isso, as informações de configuração de saudação são usadas para a sessão atual, mas não serão salvas.
* Edite o arquivo. config do aplicativo hello e conjunto de valores de saudação nela. Essa abordagem persiste nas informações de configuração hello, mas isso também significa que essas informações potencialmente confidenciais e são armazenadas em texto sem formatação em seu computador.

Olá procedimento a seguir documenta as duas abordagens. 

1. Verifique se você baixou e descompactado Olá [TwitterWPFClient.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TwitterClient/TwitterWPFClient.zip) aplicativo, conforme listado na pré-requisitos hello.

2. tooset Olá valores em tempo de execução (e apenas Olá sessão atual), execute Olá `TwitterWPFClient.exe` aplicativo. Quando o aplicativo hello solicita, digite Olá valores a seguir:

    * Olá chave do consumidor do Twitter (chave de API).
    * Olá segredo de consumidor no Twitter (segredo de API).
    * saudação do Token de acesso do Twitter.
    * Olá Twitter segredo do Token de acesso.
    * Olá conexão informações da cadeia que você salvou anteriormente. Certifique-se de que você use a cadeia de caracteres de conexão de saudação que você removeu Olá `EntityPath` par chave-valor do.
    * Olá Twitter palavras-chave que você deseja que o sentimento toodetermine para.

   ![Aplicativo TwitterWpfClient em execução, mostrando as configurações obscuras](./media/stream-analytics-twitter-sentiment-analysis-trends/wpfclientlines.png)

3. os valores hello tooset persistente, usam um texto editor tooopen Olá TwitterWpfClient.exe.config. Em seguida, em Olá `<appSettings>` elemento, fazer isso:

    * Definir `oauth_consumer_key` toohello chave do consumidor do Twitter (chave de API). 
    * Definir `oauth_consumer_secret` toohello segredo de consumidor no Twitter (segredo de API).
    * Definir `oauth_token` toohello Token de acesso do Twitter.
    * Definir `oauth_token_secret` toohello Twitter segredo do Token de acesso.

    Mais adiante Olá `<appSettings>` elemento, fazer essas alterações:

    * Definir `EventHubName` toohello nome do hub de evento (ou seja, o valor de toohello do caminho de entidade Olá).
    * Definir `EventHubNameConnectionString` toohello cadeia de caracteres de conexão. Certifique-se de que você use a cadeia de caracteres de conexão de saudação que você removeu Olá `EntityPath` par chave-valor do.

    Olá `<appSettings>` seção aparência Olá exemplo a seguir. (Para maior clareza e segurança, nós encapsulamos algumas linhas e removemos alguns caracteres.)

    ![Arquivo de configuração de aplicativo TwitterWpfClient em um editor de texto, mostrando as chaves do Twitter hello e segredos e informações de cadeia de caracteres de conexão de hub do hello evento](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-tiwtter-app-config.png)
 
4. Se você já não iniciar o aplicativo hello, execute TwitterWpfClient.exe agora. 

5. Clique em sentimento social de toocollect Olá de botão Verde Iniciar. Consulte eventos Tweet com hello **criadona**, **tópico**, e **SentimentScore** valores que estão sendo enviados tooyour hub de eventos.

    ![Aplicativo TwitterWpfClient em execução, mostrando as listagem de tweets](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-app-listing.png)

    >[!NOTE]
    >Se você encontrar erros, e você não vir um fluxo de tweets exibido na parte inferior de saudação da janela hello, verifique novamente os segredos e chaves de saudação. Verifique também a cadeia de caracteres de conexão de saudação (certifique-se de que ele não inclui Olá `EntityPath` chave e valor.)


## <a name="create-a-stream-analytics-job"></a>Criar um trabalho de Stream Analytics

Agora que os eventos tweet são streaming em tempo real do Twitter, você pode configurar um tooanalyze de trabalho do Stream Analytics esses eventos em tempo real.

1. No portal do Azure de Olá, clique em **novo** > **Internet das coisas** > **trabalho do Stream Analytics**.

2. Nome do trabalho Olá `socialtwitter-sa-job` e especificar uma assinatura, o grupo de recursos e o local.

    É uma boa ideia tooplace Olá trabalho e hello hub de evento Olá mesma região para melhor desempenho e, portanto, que não é necessário pagar tootransfer dados entre regiões.

    ![Criando um novo trabalho do Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/newjob.png)

3. Clique em **Criar**.

    Olá trabalho é criado e o portal de saudação exibe detalhes do trabalho.


## <a name="specify-hello-job-input"></a>Especificar a entrada de trabalho Olá

1. Em seu trabalho de análise de fluxo, em **trabalho topologia** no meio de saudação da folha de trabalho hello, clique em **entradas**. 

2. Em Olá **entradas** folha, clique em  **+ &nbsp;adicionar** e, em seguida, preencha a folha Olá com estes valores:

    * **Alias de entrada**: Use o nome de saudação `TwitterStream`. Se você usar um nome diferente, anote-o porque você precisará dele depois.
    * **Tipo de Origem**: Selecione **Fluxo de Dados**.
    * **Origem**: Selecione **Hub de Eventos**.
    * **Opção de importação**: Selecione **Usar hub de evento da assinatura atual**. 
    * **Namespace de barramento de serviço**: selecione Olá namespace de hub de eventos que você criou anteriormente (`<yourname>-socialtwitter-eh-ns`).
    * **Hub de eventos**: hub de eventos Olá selecione que você criou anteriormente (`socialtwitter-eh`).
    * **Nome de política do hub de evento**: selecione a política de acesso de saudação que você criou anteriormente (`socialtwitter-access`).

    ![Criar nova entrada para o trabalho de Streaming Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-twitter-new-input.png)

3. Clique em **Criar**.


## <a name="specify-hello-job-query"></a>Especifique a consulta de trabalho Olá

O Stream Analytics dá suporte a um modelo de consulta simples e declarativo que descreve as transformações. toolearn mais sobre a linguagem hello, consulte Olá [referência de linguagem do Azure Stream Analytics consulta](https://msdn.microsoft.com/library/azure/dn834998.aspx).  Este tutorial ajuda você a criar e testar várias consultas sobre dados do Twitter.

número de saudação do toocompare de menções entre tópicos, você pode usar um [janela em cascata](https://msdn.microsoft.com/library/azure/dn835055.aspx) tooget contagem de saudação do menções por tópico cada cinco segundos.

1. Olá fechar **entradas** folha se ainda não o fez.

2. Na folha de trabalho hello, clique em Olá **consulta** caixa. Azure lista entradas hello e saídas que são configuradas para trabalho hello e permite que você crie uma consulta que permite transform o fluxo de entrada hello como saída toohello é enviado.

3. Certifique-se de que Olá TwitterWpfClient aplicativo está em execução. 

3. Em hello **consulta** folha, clique em Olá pontos próximo toohello `TwitterStream` de entrada e, em seguida, selecione **dados de entrada de exemplo**.

    ![Dados de exemplo do menu Opções toouse para Olá análise de fluxo de trabalho da entrada, "Dados de exemplo de entrada" selecionados](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-sample-data-from-input.png)

    Isso abrirá uma folha que permite que você especifique a quantidade tooget de dados de exemplo, definida em termos de quanto tempo o fluxo de entrada hello tooread.

4. Definir **minutos** too3 e, em seguida, clique em **Okey**. 
    
    ![Opções de amostragem de fluxo de entrada hello, com "3 minutos" selecionados.](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-input-create-sample-data.png)

    O Azure amostras de amostra de dados de fluxo de entrada hello de 3 minutos e notifica você quando os dados de exemplo hello estão prontos. (Isso pode levar um tempo.) 

    dados de exemplo Hello são armazenados temporariamente e estão disponíveis enquanto janela de consulta Olá aberto. Se você fechar a janela de consulta Olá, dados de exemplo hello serão descartados e você tiver toocreate um novo conjunto de dados de exemplo. 

5. Alterar consulta Olá Olá código editor toohello seguinte:

    ```
    SELECT System.Timestamp as Time, Topic, COUNT(*)
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY TUMBLINGWINDOW(s, 5), Topic
    ```

    Se não usar `TwitterStream` como Olá alias de entrada hello, substitua o alias para `TwitterStream` na consulta de saudação.  

    Essa consulta usa Olá **TIMESTAMP BY** toospecify de palavra-chave um campo de carimbo de hora no hello carga toobe usado no cálculo temporal hello. Se esse campo não for especificado, a operação de janelas de saudação é executada usando o tempo de saudação que cada evento chegou ao hub de eventos de saudação. Saiba mais na seção hello "tempo de chegada vs hora do aplicativo" [referência de consulta do Stream Analytics](https://msdn.microsoft.com/library/azure/dn834998.aspx).

    Essa consulta também acessa um carimbo de hora de término hello de cada janela usando Olá **timestamp** propriedade.

5. Clique em **Testar**. consulta de saudação é executada em relação aos dados Olá você de amostra.
    
6. Clique em **Salvar**. Isso economiza consulta hello como parte do trabalho de análise de fluxo contínuo de saudação. (Ele não salva os dados de exemplo hello.)


## <a name="experiment-using-different-fields-from-hello-stream"></a>Experimente usar diferentes campos de fluxo de saudação 

Olá tabela a seguir lista os campos de saudação que fazem parte da saudação fluxo de dados JSON. Sinta-se livre tooexperiment no editor de consultas de saudação.

|Propriedade JSON | Definição|
|--- | ---|
|CreatedAt | tempo de saudação que tweet Olá foi criado|
|Tópico | tópico de saudação que corresponde a saudação especificado palavra-chave|
|SentimentScore | pontuação de sensibilidade de saudação do Sentiment140|
|Autor | Identificador do Twitter Olá que enviou tweet Olá|
|Texto | corpo completo de saudação do tweet Olá|


## <a name="create-an-output-sink"></a>Criar um coletor de saída

Agora você definiu um fluxo de eventos, uma entrada tooingest do hub de eventos e uma consulta tooperform uma transformação em fluxo hello. Olá última etapa é toodefine um coletor de saída para o trabalho de saudação.  

Neste tutorial, você pode escrever Olá agregado tweet eventos da saudação trabalho consulta tooAzure armazenamento de Blob.  Você também pode enviar seu resultados tooAzure banco de dados SQL, armazenamento de tabela do Azure, os Hubs de eventos, ou Power BI, dependendo do seu aplicativo precisa.

## <a name="specify-hello-job-output"></a>Especifique a saída do trabalho Olá

1. Em Olá **trabalho topologia** seção, clique em Olá **saída** caixa. 

2. Em Olá **saídas** folha, clique em  **+ &nbsp;adicionar** e, em seguida, preencha a folha Olá com estes valores:

    * **Alias de saída**: Use o nome de saudação `TwitterStream-Output`. 
    * **Coletor**: selecione **Armazenamento de blobs**.
    * **Opções de importação**: Selecione **Usar armazenamento de blobs da assinatura atual**.
    * **Conta de armazenamento**. Selecione **Criar uma nova conta de armazenamento.**
    * **Conta de armazenamento** (segunda caixa). Digite `YOURNAMEsa`, onde `YOURNAME` é o seu nome ou outra cadeia de caracteres exclusiva. nome de saudação pode usar apenas letras minúsculas e números e deve ser exclusivo no Azure. 
    * **Contêiner**. Digite `socialtwitter`.
    nome de conta de armazenamento Hello e o nome do contêiner são tooprovide usado junto um URI para o armazenamento de blob hello, como este: 

    `http://YOURNAMEsa.blob.core.windows.net/socialtwitter/...`
    
    ![Folha "Nova saída" para trabalho do Stream Analytics](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-create-output-blob-storage.png)
    
4. Clique em **Criar**. 

    Azure cria a conta de armazenamento hello e gera uma chave automaticamente. 

5. Olá fechar **saídas** folha. 


## <a name="start-hello-job"></a>Iniciar trabalho Olá

Uma entrada de trabalho, uma consulta e uma saída são especificadas. Você está pronto toostart Olá Stream Analytics.

1. Certifique-se de que Olá TwitterWpfClient aplicativo está em execução. 

2. Na folha de trabalho hello, clique em **iniciar**.

    ![Iniciar o trabalho de análise de fluxo de saudação](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-output.png)

3. Em Olá **Iniciar trabalho** folha, para **hora de início da saída de trabalho**, selecione **agora** e, em seguida, clique em **iniciar**. 

    ![Folha "Iniciar o trabalho" para o trabalho de análise de fluxo de saudação](./media/stream-analytics-twitter-sentiment-analysis-trends/stream-analytics-sa-job-start-job-blade.png)

    Azure notifica quando o trabalho Olá foi iniciado e, na folha de trabalho hello, status de saudação é exibido como **executando**.

    ![Trabalho em execução](./media/stream-analytics-twitter-sentiment-analysis-trends/jobrunning.png)

## <a name="view-output-for-sentiment-analysis"></a>Exibir saída para análise sentimento

Depois que seu trabalho inicia a execução e processamento de fluxo em tempo real de Twitter hello, você pode exibir a saída de saudação para análise de sentimento.

Você pode usar uma ferramenta como [Azure Storage Explorer](https://http://storageexplorer.com/) ou [Azure Explorer](http://www.cerebrata.com/products/azure-explorer/introduction) tooview seu trabalho de saída em tempo real. A partir daqui, você pode usar [Power BI](https://powerbi.com/) tooextend tooinclude seu aplicativo um painel personalizado, como Olá mostrada na Olá captura de tela a seguir:

![Power BI](./media/stream-analytics-twitter-sentiment-analysis-trends/power-bi.png)


## <a name="create-another-query-tooidentify-trending-topics"></a>Criar outra consulta tooidentify tópicos de análise de tendências

Outra consulta, você pode usar o sentimento do Twitter toounderstand baseia-se em uma [janela deslizante](https://msdn.microsoft.com/library/azure/dn835051.aspx). tópicos de análise de tendências tooidentify, pesquisar tópicos que entre um valor de limite para menções em um período de tempo especificado.

Para fins de saudação deste tutorial, você deve verificar tópicos mencionados mais de 20 vezes Olá últimos 5 segundos.

1. Na folha de trabalho hello, clique em **parar** toostop trabalho de saudação. 

2. Em Olá **trabalho topologia** seção, clique em Olá **consulta** caixa. 

3. Alterar a seguir Olá consulta toohello:

    ```    
    SELECT System.Timestamp as Time, Topic, COUNT(*) as Mentions
    FROM TwitterStream TIMESTAMP BY CreatedAt
    GROUP BY SLIDINGWINDOW(s, 5), topic
    HAVING COUNT(*) > 20
    ```

4. Clique em **Salvar**.

5. Certifique-se de que Olá TwitterWpfClient aplicativo está em execução. 

6. Clique em **iniciar** toorestart Olá trabalho nova consulta de saudação.


## <a name="get-support"></a>Obtenha suporte
Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
