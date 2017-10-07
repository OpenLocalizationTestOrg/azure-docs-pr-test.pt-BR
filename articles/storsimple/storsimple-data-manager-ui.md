---
title: aaaMicrosoft Azure StorSimple Data Manager UI | Microsoft Docs
description: "Descreve como toouse serviço StorSimple Manager de dados da interface do usuário (visualização particular)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: b0ee12b3e495400b54e48eb1a98c68b1af2e5f7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-using-hello-storsimple-data-manager-service-ui-private-preview"></a>Gerenciar usando o serviço de Gerenciador de dados StorSimple Olá da interface do usuário (visualização particular)

Este artigo explica como você pode usar o hello transformação de dados do Gerenciador de dados StorSimple UI tooperform nos dados que residem em dispositivos da série StorSimple 8000 hello. Olá dados transformados podem ser consumidos por outros serviços do Azure, como os serviços de mídia do Azure, HDInsight do Azure, aprendizado de máquina do Azure e pesquisa do Azure. 


## <a name="use-storsimple-data-transformation"></a>Usar a transformação de dados do StorSimple

Olá StorSimple Data Manager é o recurso de saudação dentro do qual a transformação de dados pode ser instanciada. Olá Data Transformation Services permite mover dados de sua tooblobs de dispositivo StorSimple local no armazenamento do Azure. Portanto, no fluxo de trabalho precisar toospecify Olá detalhes sobre os dados de dispositivo e hello StorSimple de interesse que deseja que a conta de armazenamento do toomove toohello.

### <a name="create-a-storsimple-data-manager-service"></a>Criar um serviço Gerenciador de Dados do StorSimple

Execute Olá etapas toocreate um serviço StorSimple Manager de dados a seguir.

1. toocreate um serviço StorSimple Manager de dados, vá muito[https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager)

2. Clique em Olá  **+**  ícone e pesquisa para o Gerenciador de dados do StorSimple. Clique em seu serviço Gerenciador de Dados do StorSimple e então clique em **Criar**.

3. Se sua assinatura está habilitada para a criação desse serviço, você verá Olá folha a seguir.

    ![Criar um recurso Gerenciadores de Dados do StorSimple](./media/storsimple-data-manager-ui/create-new-data-manager-service.png)

4. Insira entradas hello e clique em **criar**. Olá especificado local deve ser Olá que hospeda suas contas de armazenamento e o serviço StorSimple Manager. Atualmente, há suporte somente para as regiões Oeste dos EUA e Europa Ocidental. Portanto, seu serviço StorSimple Manager, o serviço de Gerenciador de dados e a saudação conta de armazenamento associada deve ser em regiões de saudação anterior com suporte. Demora cerca de um serviço de saudação toocreate minutos.

### <a name="create-a-data-transformation-job-definition"></a>Criar uma definição de trabalho de transformação de dados

Em um serviço de Gerenciador de dados de StorSimple, você precisa toocreate uma definição de trabalho de transformação de dados. Uma definição de trabalho Especifica detalhes dos dados de saudação que você está interessado em movimentação em uma conta de armazenamento em formato nativo hello. 

Execute Olá seguindo as etapas toocreate uma nova definição de trabalho de transformação de dados.

1.  Navegue serviço toohello que você criou. Clique em **+ Definição de Trabalho**.

    ![Clique em +Definição de Trabalho](./media/storsimple-data-manager-ui/click-add-job-definition.png)

2. nova folha de definição de trabalho Olá abre. Dê um nome à sua definição de trabalho e clique em **Origem**. Em Olá **configurar fonte de dados** folha, especifique os detalhes de saudação do seu dispositivo StorSimple e Olá dados de interesse.

    ![Criar definição de trabalho](./media/storsimple-data-manager-ui//create-new-job-deifnition.png)

3. Como esse é um novo serviço Gerenciador de Dados, não há nenhum repositório de dados configurado. tooadd seu StorSimple Manager como um repositório de dados, clique em **adicionar novo** em Olá suspensa de repositório de dados e, em seguida, clique em **Adicionar repositório de dados**.

4. Escolha **StorSimple série 8000 Manager** como repositório de saudação tipo e insira as propriedades de saudação do seu **StorSimple Manager**. Para Olá **Id de recurso** campo, você precisa tooenter Olá número antes Olá **:** na chave de registro de saudação do seu StorSimple manager.

    ![Criar a fonte de dados](./media/storsimple-data-manager-ui/create-new-data-source.png)

5.  Toque em **OK** quando terminar. Isso salva seu repositório de dados e o StorSimple Manager pode ser reutilizado em outras definições de trabalho sem a inserção desses parâmetros novamente. Levará alguns segundos depois de clicar em **Okey** para Olá tooshow StorSimple Manager para cima na lista suspensa de saudação.

6.  Em Olá **configurar fonte de dados** folha, insira o nome do dispositivo hello e Olá nome do volume que tenha seus dados de interesse.

7.  Em Olá **filtro** subseção, insira o diretório raiz de saudação que contém os dados de interesse (este campo deve começar com um `\`). Você também pode adicionar qualquer filtro de arquivo aqui.

8.  serviço de transformação de dados Olá funciona em dados de saudação toohello do Azure são passados por meio de instantâneos. Ao executar este trabalho, você pode escolher tootake um backup sempre que esse trabalho é executado (toowork nos dados mais recentes) ou toouse Olá último backup existente na nuvem hello (se você estiver trabalhando em alguns dados arquivados).

    ![Novos detalhes da fonte de dados](./media/storsimple-data-manager-ui/new-data-source-details.png)

9. Em seguida, as configurações de destino Olá necessário toobe configurado. Há dois tipos de destinos com suporte – contas do Armazenamento do Azure e dos Serviços de Mídia do Azure. Escolha contas de armazenamento tooput arquivos em blobs na conta. Escolha a conta do media services tooput arquivos em recursos nessa conta. Novamente, é preciso tooadd um repositório. No menu suspenso hello, selecione **adicionar novo** e **configurar**.

    ![Criar coletor de dados](./media/storsimple-data-manager-ui/create-new-data-sink.png)

10. Aqui, você pode selecionar o tipo de saudação do repositório que você deseja tooadd e hello outros parâmetros associados a repositório hello. Em ambos os casos, uma fila de armazenamento é criada quando Olá trabalho é executado. Essa fila é populada com mensagens sobre blobs transformados à medida que elas estejam prontas. nome da saudação dessa fila é Olá igual ao nome de Olá Olá da definição do trabalho. Se você selecionar **os serviços de mídia** como tipo de repositório Olá, em seguida, você também pode inserir credenciais da conta de armazenamento em que a fila de saudação é criada.

    ![Novos detalhes do coletor de dados](./media/storsimple-data-manager-ui/new-data-sink-details.png)

11. Depois de adicionar um repositório de dados de saudação (o que levará alguns segundos), você encontrará o repositório Olá na lista suspensa de saudação em Olá **nome da conta de destino**.  Escolha o destino de saudação que você precisa.

12. Clique em **Okey** toocreate definição de trabalho de saudação. A definição de trabalho está configurada. Você pode usar esta definição de trabalho várias vezes por meio de saudação da interface do usuário.

    ![Adicionar nova definição de trabalho](./media/storsimple-data-manager-ui/add-new-job-definition.png)

### <a name="run-hello-job-definition"></a>Executar definição de trabalho Olá

Sempre que você precisar toomove dados da conta de armazenamento do StorSimple toohello especificado na definição de trabalho hello, será necessário tooinvoke-lo. Há alguma flexibilidade na alterando os parâmetros de saudação toda vez que você chama trabalho hello. etapas de saudação são da seguinte maneira:

1. Selecione o serviço StorSimple Manager de dados e vá muito**monitoramento**. Clique em **Executar Agora**.

    ![Definição de trabalho de gatilho](./media/storsimple-data-manager-ui/run-now.png)

2. Escolha a definição de trabalho Olá que você deseja toorun. Clique em **as configurações de execução** toomodify todas as configurações que você poderá toochange para esta execução do trabalho.

    ![Executar configurações do trabalho](./media/storsimple-data-manager-ui/run-settings.png)

3. Clique em **Okey** e, em seguida, clique em **executar** toolaunch seu trabalho. toomonitor esse trabalho, vá toohello **trabalhos** página no Gerenciador de dados de seu StorSimple.

    ![Status e a lista de trabalhos](./media/storsimple-data-manager-ui/jobs-list-and-status.png)

4. Em adição toomonitoring em Olá **trabalhos** folha, você também pode ouvir na fila de armazenamento de saudação em que uma mensagem é adicionada toda vez que um arquivo é movido da conta de armazenamento do StorSimple toohello.


## <a name="next-steps"></a>Próximas etapas

[Usar trabalhos do SDK do .NET toolaunch StorSimple Data Manager](storsimple-data-manager-dotnet-jobs.md).
