---
title: "aaaUse ferramentas de análise de fluxo do Azure para Visual Studio | Microsoft Docs"
description: "Tutorial de Introdução para Olá ferramentas de análise de fluxo do Azure para Visual Studio"
keywords: visual studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a>Usar Ferramentas do Stream Analytics do Azure para Visual Studio
## <a name="introduction"></a>Introdução
Neste tutorial, você aprenderá como toouse ferramentas de análise de fluxo do Azure para Visual Studio toocreate, criar, testar localmente, gerenciar e depurar os trabalhos do Stream Analytics. 

Depois de concluir este tutorial, você poderá:
* Familiarize-se com as Ferramentas do Stream Analytics para Visual Studio.
* Configurar e implantar um trabalho do Stream Analytics.
* Testar seu trabalho local com os dados de exemplo locais.
* Use tootroubleshoot problemas de monitoramento.
* Exporte tooprojects de trabalhos existente.

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você precisa Olá pré-requisitos a seguir:
* Conclua as etapas de saudação que precedem "Criar um trabalho de análise de fluxo" em Olá [criar uma solução de IoT usando o tutorial de análise de fluxo](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics). 
* Use o Visual Studio 2015, Visual Studio 2013 Update 4 ou Visual Studio 2012. As edições Enterprise (Ultimate/Premium), Professional, Community têm suporte. Não há suporte para a Edição Express. O Visual Studio 2017 não tem suporte. 
* Saudação de uso do Azure SDK para .NET versão 2.7.1 ou posterior. Instalá-lo usando Olá [instalador de plataforma da Web](http://www.microsoft.com/web/downloads/platform.aspx).
* Instalar Olá [ferramentas de análise de fluxo para o Visual Studio](http://aka.ms/asatoolsvs).

## <a name="create-a-stream-analytics-project"></a>Criar um projeto do Stream Analytics
1. No Visual Studio, clique em Olá **arquivo** menu e selecione **novo projeto**. 

2. Na lista de modelos Olá Olá esquerda, selecione **do Stream Analytics** e, em seguida, clique em **aplicativo do Azure Stream Analytics**.

3. Insira o projeto Olá **nome**, **local**, e **nome da solução** como é feito para outros projetos.

    ![Janela Novo Projeto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    Um projeto **Pedágio** é gerado no **Gerenciador de Soluções**.

    ![Projeto Pedágio gerado no Gerenciador de Soluções](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a>Escolha a assinatura correta Olá
1. No Visual Studio, clique em Olá **exibição** menu e abra **Server Explorer**.

2. Entre com sua conta do Azure. 

## <a name="define-hello-input-sources"></a>Definir fontes de entrada hello
1.  Em **Solution Explorer**, expanda Olá **entradas** nó e renomear **Input.json** muito**EntryStream.json**. Clique duas vezes em **EntryStream.json**.
2.  Olá **Alias de entrada** agora é **EntryStream**. saudação de entrada alias é usada no script de consulta de saudação. 
3.  Em **Tipo de Origem**, selecione **Fluxo de Dados**.
4.  Em **Origem**, selecione **Hub de Eventos**.
5.  Em **Namespace de barramento de serviço**, selecione Olá **TollData** opção.
6.  Em **Nome do Hub de Eventos**, selecione **entrada**.
7.  Em **nome de política do Hub de evento**, selecione **RootManageSharedAccessKey** (Olá valor padrão).
8.  Em **Formato de Serialização de Evento**, selecione **Json**. 
9.  Em **Codificação**, selecione **UTF8**. As configurações devem ser semelhantes Olá captura de tela a seguir:

    ![Janela Entrada](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. Assistente de saudação toofinish, clique em **salvar**. Agora você pode adicionar outro fluxo de saída do hello toocreate de fonte de entrada. Saudação de atalho **entradas** nó e selecione **Novo Item**.

    ![Novo Item](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. Na janela de saudação, selecione **entrada do Azure Stream Analytics**e alterar Olá **nome** muito**ExitStream.json**. Clique em **Adicionar**.

    ![Janela Adicionar Novo Item](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. Clique duas vezes em **ExitStream.json** no projeto hello e siga Olá mesmas etapas de fluxo de entrada hello. Ser tooenter se **sair** para Olá **nome do Hub de evento** conforme Olá captura de tela a seguir:

    ![Janela ExitStream](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    Agora você definiu dois fluxos de entrada:

    ![Fluxos de recebimento de entrada e saída](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    Em seguida, adicione a entrada de dados de referência para o arquivo de blob de saudação que contém dados de registro de carro.

13. Saudação de atalho **entradas** nó no projeto de saudação e, em seguida, siga Olá mesmas etapas de entradas de fluxo de saudação. Em **Alias de Entrada**, digite **Registro** e em **Tipo de Origem**, selecione **Dados de referência**.

    ![Janela Registro](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. Em **conta de armazenamento**, selecione Olá **tolldata** opção. Em **Contêiner**, selecione **tolldata** e, em **Padrão de Caminho**, digite **registration.json**. Este nome de arquivo diferencia maiúsculas de minúsculas e deve estar em minúsculas.
15. Assistente de saudação toofinish, clique em **salvar**.

Agora, todas as entradas de saudação são definidas.

## <a name="define-hello-output"></a>Definir a saída de hello
1.  Em **Solution Explorer**, expanda Olá **entradas** nó e clique duas vezes em **Output.json**.

2.  Em **Alias de Saída**, digite **saída**. 
3.  Em **Coletor**, selecione **Banco de Dados SQL**.
4.  Em **Banco de Dados**, selecione **TollDataDB**.
5.  Em **Nome de Usuário**, digite **tolladmin**. 
6.  Em **Senha**, digite **123toll!**.
7.  Em **Tabela**, digite **TollDataRefJoin**.
8.  Clique em **Salvar**.

    ![Janela de Saída](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a>Criar uma consulta do Stream Analytics
Este tutorial tentativas tooanswer várias questões comerciais que são dados tootoll relacionados. Ele também cria consultas de análise de fluxo que podem ser usadas em respostas relevantes do Stream Analytics tooprovide.
Antes de iniciar o trabalho do Stream Analytics primeiro, vamos explorar uma sintaxe de consulta simple do cenário e hello.

### <a name="introduction-toohello-stream-analytics-query-language"></a>Introdução toohello linguagem de consulta do Stream Analytics
Digamos que você precisa que o número de saudação toocount dos veículos que insere um pedágio. Como este exemplo é um fluxo contínuo de eventos, é preciso toodefine um período de tempo. Modificar Olá pergunta toobe "quantos veículos inserir um pedágio a cada três minutos?" Este toocount de maneira dados geralmente são chamado tooas Olá em cascata de contagem.

Examine a consulta de análise de fluxo de saudação que responde a essa pergunta:

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

O Stream Analytics usa uma linguagem de consulta como SQL e adiciona algumas extensões toospecify tempo aspectos relacionados à consulta hello.

Para obter mais informações, consulte [gerenciamento de tempo](https://msdn.microsoft.com/library/azure/mt582045.aspx) e [janelas](https://msdn.microsoft.com/library/azure/dn835019.aspx) construções usadas na consulta de saudação do MSDN.

Agora que você escreveu a primeira consulta de análise de fluxo, é hora tootest-lo. Use arquivos de dados de exemplo hello localizados na pasta TollApp no Olá que caminho a seguir:

..\TollApp\TollApp\Data

Esta pasta contém Olá seguintes arquivos:
*   Entry.json
*   Exit.JSON
*   registration.json

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a>Número de saudação de contagem de veículos inserindo um pedágio
No projeto de saudação, clique duas vezes em **Script.asaql** tooopen script Olá Olá **Editor de consultas**. Copie e cole o script hello na seção anterior Olá no editor de hello. Olá Editor de consultas oferece suporte a IntelliSense, a coloração de sintaxe e marcador de saudação de erro.

![Editor de Consultas](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a>Testar as consultas do Stream Analytics localmente

1. toocompile Olá consulta toosee se houver um erro de sintaxe, clique com botão direito hello e selecione **criar**. 

2. toovalidate esta consulta em relação a dados de exemplo, você pode usar dados de exemplo do local. Entrada hello e selecione **Adicionar entrada local**.

    ![Adicionar entrada local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. Na janela pop-up do hello, selecione os dados de exemplo hello do caminho local. Clique em **Salvar**.

    ![Janela Adicionar entrada local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    Um arquivo chamado **local_EntryStream.json** é adicionada automaticamente a pasta de entradas de tooyour.

    ![Pasta do arquivo de inclusão tooinputs](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. Em Olá **Editor de consultas**, clique em **executado localmente**. Ou você pode pressionar a tecla F5 de saudação.

    ![Executar Localmente](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Saída de execução local](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    Pressione qualquer saída de hello tooview chave no hello **resultados de execução Local ASA** janela no Visual Studio. 

    ![Janela Resultado da Execução Local de ASA](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. Clique em **Abrir pasta resultado** arquivos de saída de hello toocheck ambos no formato CSV e JSON.

    ![Saída de Abrir a Pasta de Resultados](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a>Dados de entrada do exemplo hello
Você também pode dados de entrada de exemplo do arquivo local de tooa de fontes de entrada. 
1. Arquivo de configuração de entrada hello e selecione **dados de exemplo**. 

   ![Dados de exemplo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    Você pode fazer amostragem apenas do Hub de Eventos ou do Hub IoT, por enquanto. Não há suporte para outras fontes de entrada.

2. Na janela pop-up do hello, inserir dados de exemplo de saudação do hello caminho local usado toosave. Clique em **Exemplo**.

    ![Janela Dados de Exemplo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    Você pode ver o progresso de saudação em Olá **saída** janela. 

    ![Janela de Saída](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a>Enviar um tooAzure de consulta do Stream Analytics
1. Em Olá **Editor de consultas**, clique em **enviar tooAzure** no editor de script hello.

    ![Enviar tooAzure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. Selecione **Criar um Novo Trabalho do Stream Analytics do Azure**. Digite hello **nome do trabalho**e selecione hello correto **assinatura**. Clique em **Enviar**.

    ![Janela Enviar Trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a>Iniciar um trabalho
Agora que o trabalho é criado, exibição de trabalho Olá é aberta automaticamente. 
1. Olá toostart de trabalho, clique em Olá **seta verde** botão.

    ![Iniciar um trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. Selecione a configuração padrão de saudação e, em seguida, clique em **iniciar**.
 
    ![Janela Iniciar Trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    trabalho de saudação **Status** muda muito**executando**, e **eventos de entrada** e **eventos de saída** aparecer.

    ![Status Em Execução no Resumo do Trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a>Resultados da verificação Olá no Visual Studio
1. No Visual Studio, abra **Server Explorer** e com o botão direito hello **TollDataRefJoin** tabela.
2. Selecione **Mostrar dados da tabela** toosee saída de saudação do seu trabalho.
   
    ![Seleção de Mostrar Dados da Tabela no Gerenciador de Servidores](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a>Exibição Olá trabalho métricas
Algumas estatísticas básicas de trabalho podem ser encontradas em **Métricas do Trabalho**. 

![Janela Métricas de Trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a>Trabalho de saudação de lista no Gerenciador de servidores
No **Gerenciador de Servidores**, clique em **Trabalhos do Stream Analytics** e clique em **Atualizar**. trabalho de saudação aparece sob **trabalhos do Stream Analytics**.

![Trabalhos do Stream Analytics listados no Gerenciador de Servidores](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a>Exibição de trabalho Olá aberto
exibição de trabalho Olá tooopen, expanda o nó do trabalho e clique duas vezes Olá **exibição trabalho** nó.

![Nó Exibição de Trabalho](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a>Exportar um projeto existente de tooa de trabalho
Há duas maneiras que você pode exportar um projeto de tooa de trabalho existente.

Em **Server Explorer**, nó de trabalho de saudação com o botão direito no hello **trabalhos do Stream Analytics** nó e selecione **exportar tooNew projeto de análise de fluxo**.

![Exportar tooNew projeto de análise de fluxo](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

projeto de saudação é gerado no **Gerenciador de soluções**.

![Projeto gerado no Gerenciador de Soluções](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
Você também pode usar o modo de exibição do hello trabalho e clique em **projeto gerar**.

![Gerar Projeto](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a>Problemas e limitações conhecidos
 
- Não há suporte para a saída do Power BI e a saída do Azure Date Lake Store.
- Não há suporte do editor para adicionar ou alterar funções definidas pelo usuário de JavaScript.

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)
