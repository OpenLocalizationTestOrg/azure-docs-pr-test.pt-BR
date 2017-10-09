---
title: "aaaAzure integração da Stream Analytics e aprendizado de máquina | Microsoft Docs"
description: "Como toouse uma função definida pelo usuário e o aprendizado de máquina em um trabalho de análise de fluxo"
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: cfced01f-ccaa-4bc6-81e2-c03d1470a7a2
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 07/06/2017
ms.author: jeffstok
ms.openlocfilehash: e1ba7ab51ece80719839793e1320a7666cfc4181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performing-sentiment-analysis-by-using-azure-stream-analytics-and-azure-machine-learning"></a>Como realizar uma análise de sentimento usando o Azure Stream Analytics e o Azure Machine Learning
Este artigo descreve como definir tooquickly um trabalho do Stream Analytics do Azure simples que se integra ao aprendizado de máquina do Azure. Use um modelo de análise de sentimento de aprendizado de máquina do Olá dados de streaming texto Cortana Intelligence Galeria tooanalyze e determinar a pontuação de sensibilidade de saudação em tempo real. Usar Olá Cortana Intelligence Suite permite realizar essa tarefa sem se preocupar com as complexidades de saudação da criação de um modelo de análise de sentimento.

Você pode aplicar a você saber de tooscenarios este artigo como estes:

* Analisar sentimento em tempo real no streaming de dados do Twitter.
* Analisar registros de conversas do cliente com a equipe de suporte.
* Avaliar comentários em fóruns, blogs e vídeos. 
* Muitos outros cenários de pontuação preditiva em tempo real.

Em um cenário do mundo real, você obterá dados saudação diretamente a partir de um fluxo de dados do Twitter. tutorial de saudação toosimplify, escrevemos-lo para que hello trabalho de análise de fluxo contínuo obtém tweets de um arquivo CSV no armazenamento de BLOBs do Azure. Você pode criar seu próprio arquivo CSV, ou você pode usar um arquivo CSV de exemplo, conforme mostrado no Olá a imagem a seguir:

![tweets de exemplo em um arquivo CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-2.png)  

trabalho de análise de fluxo contínuo de saudação que você criar aplica modelo de análise de sentimento hello como uma função definida pelo usuário (UDF) em dados de texto de exemplo hello do repositório de blob hello. saída de Hello (resultado Olá de análise de sentimento Olá) é gravada toohello mesmo repositório de blob em um arquivo CSV diferente. 

Olá figura a seguir demonstra essa configuração. Conforme observado, para um cenário mais realista, você pode substituir o armazenamento de blobs pelo streaming de dados do Twitter de uma entrada de Hubs de Eventos do Azure. Além disso, você pode criar um [Microsoft Power BI](https://powerbi.microsoft.com/) visualização em tempo real de sentimento agregação hello.    

![Visão geral de integração do Machine Learning do Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-figure-1.png)  

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, verifique se que você tem o seguinte hello:

* Uma assinatura ativa do Azure.
* Um arquivo CSV com alguns dados. Você pode baixar o arquivo hello mostrado anteriormente do [GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/sampleinput.csv), ou você pode criar seu próprio arquivo. Neste artigo, vamos supor que você está usando o arquivo de saudação do GitHub.

Em um nível alto, tarefas de saudação do toocomplete demonstradas neste artigo, você Olá a seguir:

1. Criar uma conta de armazenamento do Azure e um contêiner de armazenamento de blob e carregar um contêiner de toohello do arquivo de entrada formato CSV.
3. Adicionar um modelo de análise de sentimento do espaço de trabalho do hello Cortana Intelligence Galeria tooyour aprendizado de máquina do Azure e implantar este modelo como um serviço web no espaço de trabalho de aprendizado de máquina hello.
5. Crie um trabalho do Stream Analytics que chama esse serviço da web como uma função no sentimento de toodetermine ordem para entrada de texto de saudação.
6. Iniciar o trabalho de análise de fluxo de saudação e verifique a saída de hello.

## <a name="create-a-storage-container-and-upload-hello-csv-input-file"></a>Criar um contêiner de armazenamento e carregar o arquivo de entrada hello CSV
Nesta etapa, você pode usar qualquer arquivo CSV, como Olá disponível do GitHub.

1. No portal do Azure de Olá, clique em **novo** &gt; **armazenamento** &gt; **conta de armazenamento**.

   ![criar nova conta de armazenamento](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-create-storage-account.png)

2. Forneça um nome (`samldemo` no exemplo hello). nome de saudação pode usar apenas letras minúsculas e números e deve ser exclusivo no Azure. 

3. Especifique um grupo de recursos existente e um local. Para o local, é recomendável que todos os recursos de saudação criados neste tutorial usam Olá mesmo local.

    ![informe os detalhes da conta de armazenamento](./media/stream-analytics-machine-learning-integration-tutorial/create-sa1.png)

4. No portal do Azure de Olá, selecione a conta de armazenamento de saudação. Na folha de conta de armazenamento hello, clique em **contêineres** e, em seguida, clique em  **+ &nbsp;contêiner** toocreate o armazenamento de blob.

    ![criar contêiner de blobs](./media/stream-analytics-machine-learning-integration-tutorial/create-sa2.png)

5. Forneça um nome para o contêiner de saudação (`azuresamldemoblob` no exemplo hello) e verifique **tipo de acesso** está definido muito**Blob**. Quando terminar, clique em **OK**.

    ![especifique os detalhes do contêiner de blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa3.png)

6. Em Olá **contêineres** folha, selecione Olá novo contêiner, que abre a folha de saudação para o contêiner.

7. Clique em **Carregar**.

    ![Botão “Carregar” para um contêiner](./media/stream-analytics-machine-learning-integration-tutorial/create-sa-upload-button.png)

8. Em Olá **carregar blob** folha, especifique o arquivo CSV de saudação que você deseja toouse para este tutorial. Para **tipo de Blob**, selecione **blob de blocos** e blocos de saudação do conjunto de tamanho too4 MB, que é suficiente para este tutorial.

    ![carregar arquivo de blob](./media/stream-analytics-machine-learning-integration-tutorial/create-sa4.png)

9. Clique em Olá **carregar** botão na parte inferior da saudação da folha de saudação.

## <a name="add-hello-sentiment-analytics-model-from-hello-cortana-intelligence-gallery"></a>Adicionar modelo de análise de sentimento de saudação do hello Cortana Intelligence Galeria

Agora que os dados de exemplo hello estão em um blob, você pode habilitar o modelo de análise de sentimento Olá na Galeria de inteligência do Cortana.

1. Vá toohello [modelo de análise preditiva sentimento](https://gallery.cortanaintelligence.com/Experiment/Predictive-Mini-Twitter-sentiment-analysis-Experiment-1) página Olá Cortana Intelligence Galeria.  

2. Clique em **Abrir no Studio**.  
   
   ![Machine Learning do Stream Analytics, abrir o Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-open-ml-studio.png)  

3. Entrar no espaço de trabalho do toogo toohello. Selecione um local.

4. Clique em **executar** final Olá Olá página. processo de saudação é executado, que leva cerca de um minuto.

   ![executar experimento no Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-run-experiment.png)  

5. Depois que o processo de saudação foi executada com êxito, selecione **implantar o serviço da Web** final Olá Olá página.

   ![implantar experimento no Machine Learning Studio como um serviço Web](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-deploy-web-service.png)  

6. toovalidate que Olá sentimento modelo de análise é toouse pronto, clique em Olá **teste** botão. Forneça entrada de texto, como "Eu amo a Microsoft". 

   ![testar experimento no Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test.png)  

    Se o teste Olá funciona, você verá um toohello semelhante resultado exemplo a seguir:

   ![testar os resultados no Machine Learning Studio](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-test-results.png)  

7. Em Olá **aplicativos** coluna, clique em Olá **Excel 2010 ou pasta de trabalho anterior** toodownload link uma pasta de trabalho do Excel. pasta de trabalho Olá contém a chave de uma API de saudação e Olá URL que você precisa posterior tooset Olá análise de fluxo de trabalho.

    ![Machine Learning do Stream Analytics, visão rápida](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-quick-glance.png)  


## <a name="create-a-stream-analytics-job-that-uses-hello-machine-learning-model"></a>Criar um trabalho do Stream Analytics que usa o modelo de aprendizado de máquina Olá

Agora você pode criar um trabalho do Stream Analytics que lê Olá exemplo tweets de arquivo CSV de saudação no armazenamento de blob. 

### <a name="create-hello-job"></a>Criar trabalho de saudação

1. Vá toohello [portal do Azure](https://portal.azure.com).  

2. Clique em **Novo** > **Internet das Coisas** > **Trabalho do Stream Analytics**. 

   ![Caminho do portal do Azure para obter um novo trabalho de análise de fluxo tooa](./media/stream-analytics-machine-learning-integration-tutorial/azure-portal-new-iot-sa-job.png)
   
3. Nome do trabalho Olá `azure-sa-ml-demo`, especifique uma assinatura, especifique um grupo de recursos existente ou crie um novo e selecione Olá local para o trabalho de saudação.

   ![especifique as configurações para o novo trabalho do Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-1.png)
   

### <a name="configure-hello-job-input"></a>Configurar entrada de trabalho Olá
trabalho de saudação obtém sua entrada de arquivo CSV de saudação que você carregou o armazenamento de tooblob anterior.

1. Depois que o trabalho Olá foi criado, em **trabalho topologia** na folha de trabalho hello, clique em hello **entradas** caixa.  
   
   ![Caixa “Entradas” na folha do trabalho do Stream Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input.png)  

2. Em Olá **entradas** folha, clique em **+ adicionar**.

   ![Botão para adicionar um trabalho de análise de fluxo de entrada toohello 'add'](./media/stream-analytics-machine-learning-integration-tutorial/create-job-add-input-button.png)  

3. Preencha Olá **nova entrada** folha com estes valores:

    * **Alias de entrada**: Use o nome de saudação `datainput`.
    * **Tipo de Origem**: Selecione **Fluxo de Dados**.
    * **Fontes**: selecione **Armazenamento de blobs**.
    * **Opção de importação**: selecione **Usar armazenamento de blobs da assinatura atual**. 
    * **Conta de armazenamento**. Selecione a conta de armazenamento de saudação criado anteriormente.
    * **Contêiner**. Contêiner de saudação selecione criado anteriormente (`azuresamldemoblob`).
    * **Formato de serialização do evento**. Selecione **CSV**.

    ![Configurações para a nova entrada de trabalho](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-create-sa-input-new-portal.png)

4. Clique em **Criar**.

### <a name="configure-hello-job-output"></a>Configurar saída de trabalho Olá
Olá trabalho envia resultados toohello mesmo onde ele obtém a entrada de armazenamento de blob. 

1. Em **trabalho topologia** na folha de trabalho hello, clique em Olá **saídas** caixa.  
  
   ![Criar nova saída para o trabalho do Streaming Analytics](./media/stream-analytics-machine-learning-integration-tutorial/create-output.png)  

2. Em Olá **saídas** folha, clique em **+ adicionar**e, em seguida, adicione uma saída com alias Olá `datamloutput`. 

3. Para **Coletor**, selecione **Armazenamento de blobs**. Em seguida, preencha restante Olá Olá saída configurações usando Olá mesmos valores que você usou para o armazenamento de blob Olá para entrada:

    * **Conta de armazenamento**. Selecione a conta de armazenamento de saudação criado anteriormente.
    * **Contêiner**. Contêiner de saudação selecione criado anteriormente (`azuresamldemoblob`).
    * **Formato de serialização do evento**. Selecione **CSV**.

   ![Configurações para a nova saída de trabalho](./media/stream-analytics-machine-learning-integration-tutorial/create-output2.png) 

4. Clique em **Criar**.   


### <a name="add-hello-machine-learning-function"></a>Adicionar função de aprendizado de máquina hello 
Anteriormente, você publicou um serviço web de tooa de modelo de aprendizado de máquina. Em nosso cenário, quando o trabalho de análise de fluxo de saudação é executado, ele envia tweet cada exemplo do serviço de web de entrada toohello Olá para análise de sentimento. Olá serviço web de aprendizado de máquina retorna um sentimento (`positive`, `neutral`, ou `negative`) e a probabilidade de tweet Olá sendo positivo. 

Nesta seção do tutorial hello, você deve definir uma função no trabalho de análise de fluxo de saudação. função Hello pode ser invocado toosend um serviço de web toohello tweet e voltar a resposta de saudação. 

1. Certifique-se de que ter Olá URL e a API de chave de serviço web que você baixou anteriormente na pasta de trabalho do Excel hello.

2. Folha de visão geral do trabalho de retorno toohello.

3. Em **Configurações**, selecione **Funções** e, em seguida, clique em **+ Adicionar**.

   ![Adicionar um trabalho de análise de fluxo de toohello de função](./media/stream-analytics-machine-learning-integration-tutorial/create-function1.png) 

4. Digite `sentiment` como Olá função alias e preencha o restante de saudação da folha de saudação usando esses valores:

    * **Tipo de função**: selecione **Azure ML**.
    * **Opção de importação**: selecione **Importar de outra assinatura**. Isso fornece uma oportunidade tooenter Olá URL e a chave.
    * **URL**: colar na URL do serviço web hello.
    * **Chave**: colar na chave de API de saudação.
  
    ![Configurações para a adição de um trabalho de análise de fluxo de toohello de função de aprendizado de máquina](./media/stream-analytics-machine-learning-integration-tutorial/add-function.png)  
    
5. Clique em **Criar**.

### <a name="create-a-query-tootransform-hello-data"></a>Criar uma consulta tootransform Olá de dados

Análise de fluxo usa uma entrada de saudação tooexamine consulta declarativa baseado em SQL e processá-la. Nesta seção, você deve criar uma consulta que lê cada tweet de entrada e, em seguida, invoca a análise de sentimento Olá aprendizado de máquina função tooperform. consulta de saudação envia Olá toohello de resultados de saída que você definiu (armazenamento de blob).

1. Folha de visão geral do trabalho de retorno toohello.

2.  Em **trabalho topologia**, clique em Olá **consulta** caixa.

    ![Criar uma consulta para o trabalho de Análise de Streaming](./media/stream-analytics-machine-learning-integration-tutorial/create-query.png)  

3. Digite hello consulta a seguir:

    ```
    WITH sentiment AS (  
    SELECT text, sentiment(text) as result from datainput  
    )  

    Select text, result.[Score]  
    Into datamloutput
    From sentiment  
    ```    

    consulta Olá invoca a função de saudação criado anteriormente (`sentiment`) na análise de sentimento ordem tooperform em cada tweet na entrada hello. 

4. Clique em **salvar** toosave consulta de saudação.


## <a name="start-hello-stream-analytics-job-and-check-hello-output"></a>Iniciar o trabalho de análise de fluxo de saudação e verifique a saída de hello

Agora você pode iniciar o trabalho de análise de fluxo de saudação.

### <a name="start-hello-job"></a>Iniciar trabalho Olá
1. Folha de visão geral do trabalho de retorno toohello.

2. Clique em **iniciar** na parte superior de saudação da folha de saudação.

    ![Criar uma consulta para o trabalho de Análise de Streaming](./media/stream-analytics-machine-learning-integration-tutorial/start-job.png)  

3. Em Olá **Iniciar trabalho**, selecione **personalizado**e, em seguida, selecione um dia toowhen anterior que você carregou o armazenamento de tooblob de arquivos CSV hello. Quando terminar, clique em **Iniciar**.  


### <a name="check-hello-output"></a>Verifique a saída de hello
1. Trabalho Olá permitem executar alguns minutos até que você veja a atividade no hello **monitoramento** caixa. 

2. Se você tiver uma ferramenta que você normalmente usa tooexamine conteúdo de saudação do armazenamento de blob, use esse Olá de tooexamine ferramenta `azuresamldemoblob` contêiner. Como alternativa, Olá etapas Olá portal do Azure:

    1. No portal de hello, localize Olá `samldemo` armazenamento de conta e na conta hello, localize Olá `azuresamldemoblob` contêiner. Você ver dois arquivos no contêiner Olá: Olá arquivo que contém a saudação tweets de exemplo e um arquivo CSV gerado pelo trabalho de análise de fluxo de saudação.
    2. Arquivo hello gerado e, em seguida, selecione **baixar**. 

   ![Baixar a saída do trabalho CSV do armazenamento de blobs](./media/stream-analytics-machine-learning-integration-tutorial/download-output-csv-file.png)  

3. Abra Olá gerado arquivo CSV. Você verá algo parecido com hello exemplo a seguir:  
   
   ![Machine Learning do Stream Analytics, exibição de CSV](./media/stream-analytics-machine-learning-integration-tutorial/stream-analytics-machine-learning-integration-tutorial-csv-view.png)  


### <a name="view-metrics"></a>Métricas de exibição
Você também pode exibir as métricas relacionadas à função de Azure Machine Learning. Olá métricas relacionadas à função a seguir é exibido no hello **monitoramento** caixa na folha de trabalho hello:

* **Função solicitações** indica o número de saudação de solicitações enviadas tooa serviço web de aprendizado de máquina.  
* **Função eventos** indica Olá número de eventos na solicitação de saudação. Por padrão, cada serviço web de aprendizado de máquina do tooa de solicitação contém too1, 000 eventos de backup.  


## <a name="next-steps"></a>Próximas etapas

* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Integrar API REST e Machine Learning](stream-analytics-how-to-configure-azure-machine-learning-endpoints-in-stream-analytics.md)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)



