---
title: "dados de aaaStream do Stream Analytics em repositório Data Lake | Microsoft Docs"
description: "Usar dados de toostream do Stream Analytics do Azure no repositório Azure Data Lake"
services: data-lake-store,stream-analytics
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: edb58e0b-311f-44b0-a499-04d7e6c07a90
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 68c727d4807db0abe6efa90145d68c78902eb789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-data-from-azure-storage-blob-into-data-lake-store-using-azure-stream-analytics"></a>Dados de transmissão do Blob de Armazenamento do Azure para o Repositório Data Lake usando o Stream Analytics do Azure
Neste artigo, você aprenderá como toouse do Azure Data Lake armazenar como uma saída para um trabalho do Stream Analytics do Azure. Este artigo demonstra um cenário simples que lê dados de um blob de armazenamento do Azure (entrada) e gravações Olá dados tooData Lake repositório (saída).

> [!NOTE]
> Neste momento, criação e configuração do repositório Data Lake saída para análise de fluxo tem suporte apenas em Olá [Portal clássico do Azure](https://manage.windowsazure.com). Portanto, algumas partes deste tutorial usará Olá Portal clássico do Azure.
>
>

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Conta de Armazenamento do Azure**. Você usará um contêiner de blob de dados de tooinput essa conta para um trabalho do Stream Analytics. Para este tutorial, suponha que você tem uma conta de armazenamento chamada **storageforasa** e um contêiner na conta Olá chamado **storageforasacontainer**. Depois de criar o contêiner de hello, carregue um tooit de arquivo de dados de exemplo. 
  
* **Conta do Repositório Azure Data Lake**. Siga as instruções de saudação em [Introdução ao repositório Azure Data Lake usando hello Azure Portal](data-lake-store-get-started-portal.md). Vamos supor que você tenha uma conta do Data Lake Store chamada **asadatalakestore**. 

## <a name="create-a-stream-analytics-job"></a>Criar um trabalho do Stream Analytics
Você começa ao criar um trabalho do Stream Analytics, que inclui uma fonte de entrada e um destino de saída. Para este tutorial, origem Olá é um contêiner de BLOBs do Azure e o destino de saudação é repositório Data Lake.

1. Logon toohello [Portal do Azure](https://portal.azure.com).

2. No painel esquerdo do hello, clique em **trabalhos do Stream Analytics**e, em seguida, clique em **adicionar**.

    ![Criar um trabalho do Stream Analytics](./media/data-lake-store-stream-analytics/create.job.png "Criar um trabalho do Stream Analytics")

    > [!NOTE]
    > Certifique-se de criar trabalho Olá mesma região que a conta de armazenamento hello, ou você incorrerá em custos adicionais de mover dados entre regiões.
    >

## <a name="create-a-blob-input-for-hello-job"></a>Criar uma entrada de Blob para o trabalho de saudação

1. Página abrir Olá para o trabalho de análise de fluxo hello, no painel esquerdo do hello clique Olá **entradas** guia e, em seguida, clique em **adicionar**.

    ![Adicionar um trabalho de entrada tooyour](./media/data-lake-store-stream-analytics/create.input.1.png "adicionar um trabalho de entrada tooyour")

2. Em Olá **nova entrada** folha, fornecer Olá valores a seguir.

    ![Adicionar um trabalho de entrada tooyour](./media/data-lake-store-stream-analytics/create.input.2.png "adicionar um trabalho de entrada tooyour")

    * Para **alias de entrada**, insira um nome exclusivo para a entrada de trabalho hello.
    * Para **Tipo de fonte**, selecione **luxo de dados**.
    * Para **Fonte**, selecione **Armazenamento de Blobs**.
    * Para **Assinatura**, selecione **Usar armazenamento de blobs da assinatura atual**.
    * Para **conta de armazenamento**, selecione a conta de armazenamento de saudação que você criou como parte dos pré-requisitos de saudação. 
    * Para **contêiner**, selecione contêiner Olá que você criou na saudação selecionado conta de armazenamento.
    * Para **Formato de Serialização de Evento**, clique em **CSV**.
    * Para **Delimitador**, selecione **guia**.
    * Para **Codificação**, selecione **UTF-8**.

    Clique em **Criar**. portal de saudação agora adiciona entrada hello e testa Olá tooit de conexão.


## <a name="create-a-data-lake-store-output-for-hello-job"></a>Criar uma saída de repositório Data Lake para trabalho Olá

1. Abra a página Olá para o trabalho de análise de fluxo de saudação, clique em Olá **saídas** guia e, em seguida, clique em **adicionar**.

    ![Adicionar um trabalho de saída tooyour](./media/data-lake-store-stream-analytics/create.output.1.png "adicionar um trabalho de tooyour de saída")

2. Em Olá **nova saída** folha, fornecer Olá valores a seguir.

    ![Adicionar um trabalho de saída tooyour](./media/data-lake-store-stream-analytics/create.output.2.png "adicionar um trabalho de tooyour de saída")

    * Para **alias de saída**, insira uma um nome exclusivo para a saída do trabalho hello. Este é um nome amigável usado em consultas toodirect Olá consulta saída toothis repositório Data Lake.
    * Para **Coletor**, selecione **Data Lake Store**.
    * Você será solicitado tooauthorize acessar a conta do repositório de Lake tooData. Clique em **Autorizar**.

3. Em Olá **nova saída** folha, continuar Olá tooprovide valores a seguir.

    ![Adicionar um trabalho de saída tooyour](./media/data-lake-store-stream-analytics/create.output.3.png "adicionar um trabalho de tooyour de saída")

    * Para **nome da conta**, selecione conta de repositório Data Lake Olá já criada onde você deseja Olá toobe de saída de trabalho enviado para.
    * Para **padrão de prefixo de caminho**, insira um toowrite de caminho usado do arquivo especificado de seus arquivos no hello conta do repositório Data Lake.
    * Para **formato de data**, se você usou um token de data no caminho de prefixo Olá, você pode selecionar o formato de data de saudação na qual os arquivos são organizados.
    * Para **formato de hora**, se você usou um token de tempo no caminho de prefixo hello, especificar o formato de tempo de saudação na qual os arquivos são organizados.
    * Para **Formato de Serialização de Evento**, clique em **CSV**.
    * Para **Delimitador**, selecione **guia**.
    * Para **Codificação**, selecione **UTF-8**.
    
    Clique em **Criar**. portal de saudação agora adiciona a saída de hello e testa Olá tooit de conexão.
    
## <a name="run-hello-stream-analytics-job"></a>Executar trabalho do Stream Analytics Olá

1. toorun um trabalho do Stream Analytics, você deve executar uma consulta de saudação **consulta** guia. Para este tutorial, você pode executar a consulta de exemplo hello, substituindo reservados Olá Olá trabalho aliases de entrada e saídas, conforme mostrado na captura de tela de saudação abaixo.

    ![Executar consulta](./media/data-lake-store-stream-analytics/run.query.png "Executar consulta")

2. Clique em **salvar** de topo de saudação da tela hello e, em seguida, de saudação **visão geral** , clique em **iniciar**. Na caixa de diálogo hello, selecione **tempo personalizado**e, em seguida, defina Olá data e hora atuais.

    ![Definir o tempo de trabalho](./media/data-lake-store-stream-analytics/run.query.2.png "Definir o tempo de trabalho")

    Clique em **iniciar** toostart trabalho de saudação. Pode levar tooa alguns minutos toostart Olá de trabalho.

3. dados tootrigger saudação trabalho toopick saudação do blob hello, copie um contêiner de blob do exemplo dados arquivo toohello. Você pode obter um arquivo de dados de exemplo da saudação [repositório Git do Azure Data Lake](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/Drivers.txt). Para este tutorial, vamos copiar arquivo hello **vehicle1_09142014.csv**. Você pode usar vários clientes, como [Azure Storage Explorer](http://storageexplorer.com/), contêiner de blob de tooa tooupload dados.

4. De saudação **visão geral** guia em **monitoramento**, consulte como dados saudação foi processados.

    ![Monitorar o trabalho](./media/data-lake-store-stream-analytics/run.query.3.png "Monitorar o trabalho")

5. Por fim, você pode verificar que os dados de saída do trabalho de saudação estão disponíveis na conta do repositório Data Lake Olá. 

    ![Verificar a saída](./media/data-lake-store-stream-analytics/run.query.4.png "Verificar a saída")

    No painel do Explorador de dados de hello, observe que Olá saída caminho da pasta tooa escrito como especificado no hello configurações de saída do repositório Data Lake (`streamanalytics/job/output/{date}/{time}`).  

## <a name="see-also"></a>Consulte também
* [Criar um cluster de HDInsight toouse repositório Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
