---
title: aaaIoT fluxos de dados em tempo real e o Azure Stream Analytics | Microsoft Docs
description: Marcas e dados de sensor de fluxos IoT com o processamento de dados em tempo real e Stream Analytics
keywords: "solução iot, introdução ao ioT"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 3e829055-75ed-469f-91f5-f0dc95046bdb
ms.service: stream-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 422e6b719d0289880aa7f17fdc585e2b768c63d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-stream-analytics-tooprocess-data-from-iot-devices"></a>Introdução a dados do Azure Stream Analytics tooprocess de dispositivos IoT
Neste tutorial, você aprenderá como dados de toogather de lógica de processamento de fluxo de toocreate de dispositivos de Internet das coisas (IoT). Usaremos uma toodemonstrate caso de uso de Internet das coisas (IoT) reais, como toobuild sua solução rápida e econômica.

## <a name="prerequisites"></a>Pré-requisitos
* [Assinatura do Azure](https://azure.microsoft.com/pricing/free-trial/)
* Exemplos de arquivos de consulta e de dados que podem ser baixados de [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)

## <a name="scenario"></a>Cenário
Contoso, que é uma empresa no espaço de automação industrial hello, automatizou totalmente seu processo de fabricação. máquinas de saudação nesta fábrica tem sensores que são capazes de emitir fluxos de dados em tempo real. Nesse cenário, um gerente de Chão de produção quer toohave de informações em tempo real de toolook de dados de sensor Olá para padrões e executar ações. Usaremos Olá linguagem de consulta de análise de fluxo (SAQL) sobre padrões interessantes do hello sensor dados toofind do fluxo de entrada hello de dados.

Aqui, os dados estão sendo gerados de um dispositivo de tag de sensor da Texas Instruments.

![Tag de sensor Texas Instruments](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-01.jpg)

carga de saudação de dados de saudação está no formato JSON e Olá seguinte aparência:

    {
        "time": "2016-01-26T20:47:53.0000000",  
        "dspl": "sensorE",  
        "temp": 123,  
        "hmdt": 34  
    }  

Em um cenário real, você poderia ter centenas desses sensores gerando eventos como um fluxo. Idealmente, um dispositivo de gateway executaria código toopush esses eventos muito[Hubs de eventos do Azure](https://azure.microsoft.com/services/event-hubs/) ou [Hubs de IoT do Azure](https://azure.microsoft.com/services/iot-hub/). O trabalho do Stream Analytics ingestão esses eventos dos Hubs de eventos e executar consultas de análise em tempo real em fluxos de saudação. Em seguida, você pode enviar Olá resultados tooone de saudação [suporte saídas](stream-analytics-define-outputs.md).

Para facilitar o uso, este guia de Introdução fornece um arquivo de dados de exemplo, capturado de dispositivos de tag de sensor reais. Você pode executar consultas em dados de exemplo hello e ver os resultados. Tutoriais subsequentes, você aprenderá como tooconnect seu trabalho tooinputs e saídas e implantá-las toohello serviço do Azure.

## <a name="create-a-stream-analytics-job"></a>Criar um trabalho de Stream Analytics
1. Em Olá [portal do Azure](http://portal.azure.com), hello mais sinal e, em seguida, digite **do STREAM ANALYTICS** em Olá texto janela toohello à direita. Em seguida, selecione **trabalho do Stream Analytics** na lista de resultados de saudação.
   
    ![Criar um novo trabalho do Stream Analytics](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-02.png)
2. Insira um nome exclusivo do trabalho e verificar a assinatura de saudação é Olá um correto para seu trabalho. Em seguida, crie um novo grupo de recursos ou selecione um já existente em sua assinatura.
3. Selecione um local para seu trabalho. Para velocidade de processamento e a redução do custo na transferência de dados selecionando Olá recomenda-se o mesmo local que o grupo de recursos de saudação e conta de armazenamento pretendida.
   
    ![Detalhes de Como criar um novo trabalho do Stream Analytics](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03.png)
   
   > [!NOTE]
   > Você deve criar essa conta de armazenamento apenas uma vez por região. Esse armazenamento será compartilhado entre todos os trabalhos do Stream Analytics que forem criados nessa região.
   > 
   > 
4. Verifique seu trabalho no painel de Olá caixa tooplace e, em seguida, clique em **criar**.
   
    ![criação do trabalho em andamento](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03a.png)
5. Você deve ver uma implantação' iniciada...' exibido em Olá superior direito da janela do navegador. Assim, ele será alterado tooa concluída janela conforme mostrado abaixo.
   
    ![criação do trabalho em andamento](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03b.png)

### <a name="create-an-azure-stream-analytics-query"></a>Criar uma instância do Azure Stream Analytics
Depois que o trabalho estiver criou tooopen do tempo e construir uma consulta. Você pode acessar facilmente seu trabalho clicando em bloco Olá para ele.

![Bloco de trabalho](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-04.png)

Em Olá **trabalho topologia** painel clique Olá **consulta** caixa toogo toohello Editor de consultas. Olá **consulta** editor permite que você consulta tooenter um T-SQL que executa a transformação Olá por dados de eventos de entrada de saudação.

![Caixa de consulta](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-05.png)

### <a name="query-archive-your-raw-data"></a>Consulta: arquivar seus dados brutos
a forma mais simples Olá de consulta é uma consulta passagem que arquiva todos os tooits de dados de entrada designados de saída. Baixe o arquivo de dados de exemplo de saudação do [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) tooa local no computador. 

1. Cole a consulta de saudação do arquivo de PassThrough.txt hello. 
   
    ![Testar fluxo de entrada](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06.png)
2. Clique em entrada de Avançar tooyour Olá três pontos e selecione **carregar dados de exemplo do arquivo** caixa.
   
    ![Testar fluxo de entrada](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06a.png)
3. Um painel aberto no hello direita como um resultado, nele dados selecione saudação HelloWorldASA InputStream.json de seu local de download de arquivo em clique em **Okey** na parte inferior de saudação do painel de saudação.
   
    ![Testar fluxo de entrada](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06b.png)
4. Em seguida, clique em Olá **teste** engrenagem Olá superior esquerda da janela hello e processar a sua consulta de teste no conjunto de dados de exemplo hello. Será aberta uma janela de resultados abaixo de sua consulta como Olá processamento é concluído.
   
    ![Resultados do teste](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-07.png)

### <a name="query-filter-hello-data-based-on-a-condition"></a>De consulta: Dados de saudação do filtro com base em uma condição
Vamos tentar toofilter resultados de saudação com base em uma condição. Gostaríamos de receber resultados tooshow para somente os eventos que vêm de "sensorA". consulta de saudação está no arquivo de Filtering.txt de saudação.

![Filtrar um fluxo de dados](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-08.png)

Observe que essa consulta diferencia maiusculas de minúsculas Olá compara um valor de cadeia de caracteres. Clique em Olá **teste** engrenagem novamente a consulta de saudação tooexecute. consulta de Olá deve retornar 389 linhas fora 1860 eventos.

![Segundo resultado do teste do teste de consulta](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-09.png)

### <a name="query-alert-tootrigger-a-business-workflow"></a>Consulta: Tootrigger de alerta um fluxo de trabalho de negócios
Vamos tornar nossa consulta mais detalhada. Para cada tipo de sensor, podemos deseja toomonitor a temperatura média por janela de 30 segundos e exibir resultados apenas se a temperatura média hello está acima de 100 graus. Podemos gravará seguinte Olá de consulta e, em seguida, clique em **teste** toosee resultados de saudação. consulta de saudação está no arquivo de ThresholdAlerting.txt de saudação.

![Consulta de filtro de 30 segundos](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-10.png)

Agora você verá resultados que contenham somente 245 nomes de sensores e linhas em que a média de saudação temperatura for maior que 100. Essa consulta agrupa o fluxo de saudação de eventos por **dspl**, que é o nome do sensor de saudação, mais um **janela em cascata** de 30 segundos. Consultas temporais deverá indicar que desejamos tooprogress de tempo. Usando Olá **TIMESTAMP BY** cláusula, especificamos Olá **OUTPUTTIME** tempos de coluna tooassociate todos os cálculos temporal. Para obter informações detalhadas, leia os artigos do MSDN Olá sobre [gerenciamento de tempo](https://msdn.microsoft.com/library/azure/mt582045.aspx) e [funções de janelamento](https://msdn.microsoft.com/library/azure/dn835019.aspx).

### <a name="query-detect-absence-of-events"></a>Consulta: detectar ausência de eventos
Como pode escrevemos toofind uma consulta uma falta de eventos de entrada? Vamos ver Olá última vez que um sensor de dados enviados e, em seguida, não enviou eventos para Olá próximo minuto. consulta de saudação está no arquivo de AbsenseOfEvent.txt de saudação.

![Detectar ausência de eventos](./media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-11.png)

Aqui usamos uma **LEFT OUTER** ingressar toohello mesmo fluxo (autojunção). Para uma junção **INTERNA**, um resultado retorna somente quando uma correspondência é encontrada.  Para uma **LEFT OUTER** junção, se um evento de saudação lado esquerdo da junção Olá for incomparável, uma linha que tem nulo para todos os Olá colunas do lado direito de saudação será retornada. Essa técnica é muito útil toofind uma ausência de eventos. Consulte a documentação do MSDN para saber mais sobre [JUNÇÃO](https://msdn.microsoft.com/library/azure/dn835026.aspx).

## <a name="conclusion"></a>Conclusão
Olá finalidade deste tutorial é toodemonstrate como consultas de linguagem de consulta do Stream Analytics diferentes toowrite e ver os resultados no navegador de saudação. No entanto, isso está apenas começando. Você pode fazer muito mais com Stream Analytics. Stream Analytics dá suporte a uma variedade de entradas e saídas e pode até mesmo usar funções no aprendizado de máquina do Azure toomake-uma ferramenta robusta para analisar os fluxos de dados. Você pode iniciar tooexplore mais sobre análise de fluxo, usando nosso [mapa de aprendizado](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/). Para obter mais informações sobre como consultas toowrite, leia o artigo Olá sobre [padrões comuns de consulta](stream-analytics-stream-analytics-query-patterns.md).

