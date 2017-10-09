---
title: "dados aaaCapture dos Hubs de eventos no repositório Azure Data Lake | Microsoft Docs"
description: "Dados do repositório do uso do Azure Data Lake toocapture dos Hubs de eventos"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/28/2017
ms.author: nitinme
ms.openlocfilehash: 09b17bd0b47043bd2c83dba72c01a8064f206a0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-data-lake-store-toocapture-data-from-event-hubs"></a>Dados do repositório do uso do Azure Data Lake toocapture dos Hubs de eventos

Saiba como toouse dados do repositório Azure Data Lake toocapture recebeu por Hubs de eventos do Azure.

## <a name="prerequisites"></a>Pré-requisitos

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Uma conta do repositório Azure Data Lake**. Para obter instruções sobre como um, ver toocreate [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md).

*  **Um namespace dos Hubs de Eventos**. Para obter instruções, confira [Criar um namespace dos Hubs de Eventos](../event-hubs/event-hubs-create.md#create-an-event-hubs-namespace). Certifique-se de conta do repositório Data Lake hello e Olá Hubs de eventos namespace estão no hello mesma assinatura do Azure.


## <a name="assign-permissions-tooevent-hubs"></a>Atribuir permissões tooEvent Hubs

Nesta seção, você criar uma pasta dentro de conta Olá onde você deseja toocapture Olá dados dos Hubs de eventos. Você também atribuir permissões Hubs tooEvent para que ele possa gravar dados em uma conta do repositório Data Lake. 

1. Abrir conta de repositório Data Lake Olá onde você deseja que os dados toocapture dos Hubs de eventos e, em seguida, clique em **Data Explorer**.

    ![Data explorer do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-open-data-explorer.png "Data explorer do Data Lake Store")

2.  Clique em **nova pasta** e, em seguida, digite um nome para a pasta onde você deseja toocapture Olá dados.

    ![Criar uma nova pasta no Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-new-folder.png "Criar uma nova pasta no Data Lake Store")

3. Atribua permissões na raiz de saudação do hello repositório Data Lake. 

    a. Clique em **Data Explorer**, selecione a raiz de saudação do hello conta do repositório Data Lake e, em seguida, clique em **acesso**.

    ![Atribuir permissões para a raiz do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-root.png "Atribuir permissões para a raiz do Data Lake Store")

    b. Em **Acesso**, clique em **Adicionar**, clique em **Selecionar Usuário ou Grupo** e procure por `Microsoft.EventHubs`. 

    ![Atribuir permissões para a raiz do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Atribuir permissões para a raiz do Data Lake Store")
    
    Clique em **Selecionar**.

    c. Em **Atribuir Permissões**, clique em **Selecionar Permissões**. Definir **permissões** muito**Execute**. Definir **adicionar a** muito**essa pasta e todos os filhos**. Definir **adicionar como** muito**uma entrada de permissão de acesso e uma entrada de permissão padrão**.

    ![Atribuir permissões para a raiz do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp1.png "Atribuir permissões para a raiz do Data Lake Store")

    Clique em **OK**.

4. Atribua permissões para pasta Olá na conta do repositório Data Lake onde você deseja toocapture dados.

    a. Clique em **Data Explorer**, selecione a pasta Olá na conta do repositório Data Lake do hello e, em seguida, clique em **acesso**.

    ![Atribuir permissões para a pasta do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-permissions-to-folder.png "Atribuir permissões para a pasta do Data Lake Store")

    b. Em **Acesso**, clique em **Adicionar**, clique em **Selecionar Usuário ou Grupo** e procure por `Microsoft.EventHubs`. 

    ![Atribuir permissões para a pasta do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp.png "Atribuir permissões para a pasta do Data Lake Store")
    
    Clique em **Selecionar**.

    c. Em **Atribuir Permissões**, clique em **Selecionar Permissões**. Definir **permissões** muito**leitura, gravação,** e **Execute**. Definir **adicionar a** muito**essa pasta e todos os filhos**. Finalmente, defina **adicionar como** muito**uma entrada de permissão de acesso e uma entrada de permissão padrão**.

    ![Atribuir permissões para a pasta do Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-assign-eventhub-sp-folder.png "Atribuir permissões para a pasta do Data Lake Store")
    
    Clique em **OK**. 

## <a name="configure-event-hubs-toocapture-data-toodata-lake-store"></a>Configurar o repositório Hubs de eventos toocapture data tooData Lake

Nesta seção, você criará um Hub de Eventos dentro de um namespace de Hubs de Eventos. Você também pode configurar Olá Hub de eventos toocapture dados tooan conta do repositório Azure Data Lake. Esta seção pressupõe que você já criou um namespace dos Hubs de Eventos.

2. De saudação **visão geral** painel do namespace de Hubs de eventos de saudação, clique em **+ Hub de eventos**.

    ![Criar Hub de Eventos](./media/data-lake-store-archive-eventhub-capture/data-lake-store-create-event-hub.png "Criar Hub de Eventos")

3. Forneça a seguinte Olá valores tooconfigure Hubs de eventos toocapture dados tooData Lake repositório.

    ![Criar Hub de Eventos](./media/data-lake-store-archive-eventhub-capture/data-lake-store-configure-eventhub.png "Criar Hub de Eventos")

    a. Forneça um nome para Olá Hub de eventos.
    
    b. Neste tutorial, defina **contagem de partições** e **retenção de mensagem** toohello os valores padrão.
    
    c. Definir **capturar** muito**em**. Saudação de conjunto **janela de tempo** (frequência toocapture) e **janela de tamanho** (toocapture de tamanho de dados). 
    
    d. Para **provedor capturar**, selecione **repositório Azure Data Lake** e selecione Olá Olá repositório Data Lake criado anteriormente. Para **Data Lake caminho**, digite nome de saudação da pasta de saudação criada na conta do repositório Data Lake do hello. Você só precisa de pasta de toohello tooprovide Olá caminho relativo.

    e. Deixe Olá **formatos de nome de arquivo de captura do exemplo** toohello valor de padrão. Essa opção controla a estrutura de pasta de saudação que é criada na pasta de captura hello.

    f. Clique em **Criar**.

## <a name="test-hello-setup"></a>Configuração de saudação do teste

Agora você pode testar a solução Olá enviando dados toohello Hub de eventos do Azure. Siga as instruções de saudação em [enviar eventos de Hubs de eventos tooAzure](../event-hubs/event-hubs-dotnet-framework-getstarted-send.md). Quando você começa a enviar dados hello, você vê os dados de saudação refletidos no repositório Data Lake usando a estrutura de pastas de saudação especificado. Por exemplo, verá uma estrutura de pasta, conforme mostrado no hello seguinte captura de tela, em seu repositório Data Lake.

![Exemplo de dados do Hub de Eventos no Data Lake Store](./media/data-lake-store-archive-eventhub-capture/data-lake-store-eventhub-data-sample.png "Exemplo de dados do Hub de Eventos no Data Lake Store")

> [!NOTE]
> Mesmo se você não tem mensagens recebidas para Hubs de eventos, Hubs de eventos grava arquivos vazios com apenas a cabeçalhos de saudação em Olá conta do repositório Data Lake. Olá arquivos são gravados no hello mesmo intervalo de tempo que você forneceu durante a criação de Hubs de eventos de saudação.
> 
>

## <a name="analyze-data-in-data-lake-store"></a>Analisar dados no Repositório Data Lake

Quando dados saudação estiverem no repositório Data Lake, você pode executar trabalhos analíticos tooprocess e situação dados de saudação. Consulte [USQL Avro exemplo](https://github.com/Azure/usql/tree/master/Examples/AvroExamples) sobre como toodo esse usando análise Azure Data Lake.
  

## <a name="see-also"></a>Consulte também
* [Proteger dados no Repositório Data Lake](data-lake-store-secure-data.md)
* [Copiar dados do repositório Azure armazenamento de Blobs tooData Lake](data-lake-store-copy-data-azure-storage-blob.md)
