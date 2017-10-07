---
title: "uma solução de IoT usando a análise de fluxo de aaaBuild | Microsoft Docs"
description: "Tutorial de Introdução para Olá solução de IoT de análise de fluxo de um cenário de cabina de cobrança"
keywords: "solução de iot, funções da janela"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: e37fc5b56c4ffc4a2d7b820afe0c17631e577ea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-iot-solution-by-using-stream-analytics"></a>Compilar uma solução de IoT usando o Stream Analytics
## <a name="introduction"></a>Introdução
Neste tutorial, você aprenderá como informações em tempo real do toouse Azure Stream Analytics tooget de seus dados. Os desenvolvedores podem facilmente combinar fluxos de dados, como fluxos de clique, logs e eventos gerados pelo dispositivo com registros históricos ou informações de negócios de tooderive de dados de referência. Como um serviço de computação de fluxo em tempo real, totalmente gerenciado que é hospedado no Microsoft Azure, Azure Stream Analytics fornece resiliência interna, baixa latência e escalabilidade tooget preparam em minutos.

Depois de concluir este tutorial, você poderá:

* Familiarize-se com o portal do Azure Stream Analytics hello.
* Configurar e implantar um trabalho de transmissão.
* Descrever os problemas do mundo real e resolvê-los usando a linguagem de consulta do Stream Analytics hello.
* Desenvolver com confiança soluções de transmissão para seus clientes usando o Stream Analytics do Azure.
* Use Olá monitoramento e registro em log experiência tootroubleshoot problemas.

## <a name="prerequisites"></a>Pré-requisitos
Você será necessário Olá toocomplete pré-requisitos a seguir este tutorial:

* versão mais recente de saudação do [PowerShell do Azure](/powershell/azure/overview)
* Visual Studio de 2017, 2015 ou hello livre [Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)
* Uma [assinatura do Azure](https://azure.microsoft.com/pricing/free-trial/)
* Privilégios administrativos no computador de saudação
* Download de [TollApp.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) de saudação Microsoft Download Center
* Opcional: Código gerador de evento Olá TollApp em [GitHub](https://aka.ms/azure-stream-analytics-toll-source)

## <a name="scenario-introduction-hello-toll"></a>Introdução ao cenário: “Olá, pedágio!”
Uma praça de pedágio é um fenômeno comum. Você encontre-los em várias estradas, pontes e túneis em Olá, mundo. Cada praça de pedágio tem várias cabines do pedágio. Em cabines manuais, você pare atendente de tooan toopay Olá pedágio. Em cabines automatizadas, um sensor na parte superior de cada cabine examina um cartão RFID que é afixada toohello para-brisa do seu veículo conforme você passa pedágio hello. É fácil toovisualize passagem de saudação dos veículos por essas estações de pedágio como um fluxo de eventos onde operações interessantes podem ser executadas.

![Imagem de carros em cabines de pedágio](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image1.jpg)

## <a name="incoming-data"></a>Dados de entrada
Este tutorial funciona com dois fluxos de dados. Sensores instalados em entrada hello e saída de estações de pedágio Olá produzir primeiro fluxo de saudação. segundo fluxo de saudação é um conjunto de dados de pesquisa estática que tem dados de registro de veículo.

### <a name="entry-data-stream"></a>Fluxo de dados de entrada
fluxo de dados de entrada Hello contém informações sobre o carro conforme ele entra estações de pedágio.

| TollID | EntryTime | PlacaDeCarro | Estado | Faça | Modelo | VehicleType | VehicleWeight | Pedágio | Marca |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 |2014-09-10 12:01:00.000 |JNB 7001 |NOVA IORQUE |Honda |CRV |1 |0 |7 | |
| 1 |2014-09-10 12:02:00.000 |1001 YXZ |NOVA IORQUE |Toyota |Camry |1 |0 |4 |123456789 |
| 3 |2014-09-10 12:02:00.000 |ABC 1004 |CT |Ford |Taurus |1 |0 |5 |456789123 |
| 2 |2014-09-10 12:03:00.000 |1003 XYZ |CT |Toyota |Corolla |1 |0 |4 | |
| 1 |2014-09-10 12:03:00.000 |1007 BNJ |NOVA IORQUE |Honda |CRV |1 |0 |5 |789123456 |
| 2 |2014-09-10 12:05:00.000 |CDE 1007 |NJ |Toyota |4x4 |1 |0 |6 |321987654 |

Aqui está uma breve descrição das colunas de saudação:

| Coluna | Descrição |
| --- | --- |
| TollID |ID de cabine do pedágio Olá que identifica exclusivamente um pedágio |
| EntryTime |Data de saudação e a hora da entrada de saudação veículo toohello pedágio em UTC |
| PlacaDeCarro |número de placa de saudação do veículo Olá |
| Estado |Um estado nos Estados Unidos |
| Faça |fabricante de saudação do automóvel Olá |
| Modelo |número de modelo de saudação do automóvel Olá |
| VehicleType |1 para veículos de passageiros ou 2 para veículos comerciais |
| WeightType |Peso do veículo em toneladas; 0 para veículos de passageiros |
| Pedágio |valor de pedágio Olá em USD |
| Marca |Olá e-Tag em automóvel Olá que automatiza o pagamento; espaço em branco em que o pagamento Olá foi feito manualmente |

### <a name="exit-data-stream"></a>Fluxo de dados de saída
fluxo de dados de saída de Hello contém informações sobre carros deixa a estação de pedágio hello.

| **TollId** | **ExitTime** | **PlacaDeCarro** |
| --- | --- | --- |
| 1 |2014-09-10T12:03:00.0000000Z |JNB 7001 |
| 1 |2014-09-10T12:03:00.0000000Z |1001 YXZ |
| 3 |2014-09-10T12:04:00.0000000Z |ABC 1004 |
| 2 |2014-09-10T12:07:00.0000000Z |1003 XYZ |
| 1 |2014-09-10T12:08:00.0000000Z |1007 BNJ |
| 2 |2014-09-10T12:07:00.0000000Z |CDE 1007 |

Aqui está uma breve descrição das colunas de saudação:

| Coluna | Descrição |
| --- | --- |
| TollID |ID de cabine do pedágio Olá que identifica exclusivamente um pedágio |
| ExitTime |Data de saudação e a hora de saída do veículo de saudação do pedágio em UTC |
| PlacaDeCarro |número de placa de saudação do veículo Olá |

### <a name="commercial-vehicle-registration-data"></a>Dados de registro de veículo comercial
tutorial de saudação usa um instantâneo estático de um banco de dados de registro de veículo comercial.

| PlacaDeCarro | RegistrationId | Expirado |
| --- | --- | --- |
| SVT 6023 |285429838 |1 |
| XLZ 3463 |362715656 |0 |
| BAC 1005 |876133137 |1 |
| RIV 8632 |992711956 |0 |
| SNY 7188 |592133890 |0 |
| ELH 9896 |678427724 |1 |

Aqui está uma breve descrição das colunas de saudação:

| Coluna | Descrição |
| --- | --- |
| PlacaDeCarro |número de placa de saudação do veículo Olá |
| RegistrationId |ID de registro do veículo Olá |
| Expirado |Olá status de registro de veículo Olá: 0 se o registro de veículo estiver ativo, 1 se o registro está vencido |

## <a name="set-up-hello-environment-for-azure-stream-analytics"></a>Configurar o ambiente de saudação para análise de fluxo do Azure
toocomplete neste tutorial, você precisa de uma assinatura Microsoft Azure. A Microsoft oferece uma avaliação gratuita dos serviços do Microsoft Azure.

Se não tiver uma conta do Azure, [solicite uma versão de avaliação gratuita](http://azure.microsoft.com/pricing/free-trial/).

> [!NOTE]
> toosign para uma avaliação gratuita, você precisa de um dispositivo móvel que pode receber mensagens de texto e um cartão de crédito válido.
> 
> 

Certifique-se de que toofollow Olá as etapas na seção de "Limpar sua conta do Azure" hello final Olá deste artigo para que você possa fazer melhor uso de saudação do seu crédito do Azure.

## <a name="provision-azure-resources-required-for-hello-tutorial"></a>Provisionar recursos do Azure necessários para o tutorial Olá
Este tutorial requer dois tooreceive de hubs de evento *entrada* e *sair* fluxos de dados. Banco de dados SQL do Azure gera resultados de saudação de trabalhos do Stream Analytics hello. O Armazenamento do Azure armazena dados de referência sobre o registro do veículo.

Você pode usar Olá Setup.ps1 script na pasta de TollApp Olá no GitHub toocreate todos os recursos necessários. Interesse Olá de tempo, recomendamos que você executá-lo. Se você quiser toolearn mais informações sobre como tooconfigure desses recursos no hello portal do Azure, consulte o apêndice de "Configurando recursos de tutorial no portal do Azure" toohello.

Baixar e salvar Olá suporte [TollApp](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip) arquivos e pastas.

Abra uma janela do **Microsoft Azure PowerShell***como administrador*. Se ainda não tiver o Azure PowerShell, siga as instruções de saudação em [instalar e configurar o Azure PowerShell](/powershell/azure/overview) tooinstall-lo.

Como o Windows bloqueia automaticamente. ps1,. dll e arquivos de .exe, é necessário tooset política de execução de saudação antes de executar o script hello. Verifique se está executando a janela do PowerShell do Azure Olá *como um administrador*. Execute **Set-ExecutionPolicy unrestricted**. Quando solicitado, digite **Y**.

![Captura de tela de "Set-ExecutionPolicy unrestricted" em execução na janela do Azure PowerShell](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image2.png)

Executar **Get-ExecutionPolicy** toomake-se de que o comando Olá trabalhou.

![Captura de tela de "Get-ExecutionPolicy" em execução na janela do Azure PowerShell](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image3.png)

Acesse o diretório toohello com scripts de saudação e o aplicativo gerador.

![Captura de tela de "cd .\TollApp\TollApp" em execução na janela do PowerShell do Azure Olá](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image4.png)

Tipo **.\\ Setup.ps1** tooset a sua conta do Azure, criar e configurar todos os recursos necessários e iniciar toogenerate eventos. script Hello aleatoriamente seleciona uma região toocreate seus recursos. tooexplicitly especificar uma região, você pode passar Olá **-local** parâmetro como Olá exemplo a seguir:

**.\\Setup.ps1 -location “Central US”**

![Captura de tela da página Olá entrada do Azure](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image5.png)

script Hello abre Olá **entrar** página do Microsoft Azure. Insira suas credenciais de conta.

> [!NOTE]
> Se sua conta tiver acesso toomultiple assinaturas, você será o nome da assinatura que você deseja toouse tutorial Olá Olá tooenter frequentes.
> 
> 

script Hello pode levar vários toorun de minutos. Depois da conclusão, saída de hello deve ter a aparência Olá captura de tela a seguir.

![Captura de tela de saída do script hello na janela do PowerShell do Azure Olá](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image6.PNG)

Você também verá outra janela é semelhante toohello captura de tela a seguir. Este aplicativo está enviando eventos tooAzure Hubs de eventos, que é necessário toorun tutorial de saudação. Assim, não pare o aplicativo hello ou fechar esta janela até que você concluir o tutorial hello.

![Captura de tela de "Enviando dados de hub de evento"](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image7.png)

Você deve ser capaz de toosee seus recursos no portal do Azure agora. Vá muito<https://portal.azure.com>e entre com suas credenciais de conta. Observe que no momento algumas funcionalidades utiliza o portal clássico do hello. Essas etapas serão indicadas claramente.

### <a name="azure-event-hubs"></a>Hubs de eventos do Azure
No portal do Azure de Olá, clique em **mais serviços** na parte inferior de saudação do painel de gerenciamento esquerdo hello. Tipo **hubs de eventos** no hello campo fornecido e clique em **hubs de eventos**. Isso inicia uma nova saudação de toodisplay de janela de navegador **SERVICE BUS** área Olá **portal clássico**. Aqui você pode ver Olá Hub de eventos criados pelo Olá Setup.ps1 script.

![Barramento de Serviço](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image8.png)

Clique em Olá que inicia com *tolldata*. Clique em Olá **HUBS de eventos** guia. Você verá dois Hubs de Eventos chamados *entry* e *exit* criados nesse namespace.

![Guia de Hubs de evento no portal clássico Olá](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image9.png)

### <a name="azure-storage-container"></a>Contêiner de armazenamento do Azure
1. Volte a guia toohello no portal de tooAzure abra seu navegador. Clique em **armazenamento** em Olá lado esquerdo da saudação toosee portal do Azure hello Azure contêiner de armazenamento que é usado no tutorial de saudação.
   
    ![Item de menu de armazenamento](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image11.png)
2. Clique em Olá que começam com *tolldata*. Clique em Olá **CONTÊINERES** contêiner do guia toosee Olá criado.
   
    ![Guia de contêineres no hello portal do Azure](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image10.png)
3. Clique em Olá **tolldata** saudação do contêiner toosee carregado o arquivo JSON que contém dados de registro de veículo.
   
    ![Captura de tela de arquivo de registration.json Olá no contêiner de saudação](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image12.png)

### <a name="azure-sql-database"></a>Banco de Dados SQL do Azure
1. Volte toohello portal do Azure na guia de primeira Olá que foi aberto no navegador de saudação. Clique em **bancos de dados SQL** em Olá lado esquerdo da saudação toosee portal do Azure Olá banco de dados SQL que será usado no tutorial hello e clique em **tolldatadb**.
   
    ![Captura de tela da saudação criado o banco de dados SQL](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15.png)
2. Nome do servidor de saudação cópia sem número de porta de saudação (*servername*. t, por exemplo).
    ![Captura de tela da saudação criado o banco de dados de banco de dados SQL](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15a.png)

## <a name="connect-toohello-database-from-visual-studio"></a>Conecte-se o banco de dados toohello do Visual Studio
Use o Visual Studio tooaccess resultados da consulta no banco de dados de saída de hello.

Conecte-se toohello banco de dados do SQL (destino Olá) do Visual Studio:

1. Abra o Visual Studio e, em seguida, clique em **ferramentas** > **conectar tooDatabase**.
2. Se for solicitado, clique em **Microsoft SQL Server** como uma fonte de dados.
   
    ![Caixa de diálogo Alterar Fonte de Dados](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image16.png)
3. Em Olá **nome do servidor** campo, cole o nome hello que você copiou na seção anterior de saudação do hello portal do Azure (ou seja, *servername*. t).
4. Clique em **Usar Autenticação do SQL Server**.
5. Digite **tolladmin** em Olá **nome de usuário** campo e **123toll!** em Olá **senha** campo.
6. Clique em **selecionar ou digitar um nome de banco de dados**e selecione **TollDataDB** como banco de dados de saudação.
   
    ![Caixa de diálogo Adicionar Conexão](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image17.jpg)
7. Clique em **OK**.
8. Abra o Gerenciador de Servidores.
   
    ![Gerenciador de Servidores](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image18.png)
9. Consulte as quatro tabelas no banco de dados de TollDataDB hello.
   
    ![Tabelas no banco de dados de TollDataDB Olá](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image19.jpg)

## <a name="event-generator-tollapp-sample-project"></a>Gerador de eventos: projeto de exemplo TollApp
saudação de script do PowerShell é iniciado automaticamente toosend eventos usando o programa de aplicativo de exemplo hello TollApp. Você não precisa tooperform as etapas adicionais.

No entanto, se você estiver interessado nos detalhes de implementação, você pode encontrar código-fonte do hello TollApp aplicativo hello no GitHub [exemplos/TollApp](https://aka.ms/azure-stream-analytics-toll-source).

![Captura de tela do código de exemplo exibido no Visual Studio](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image20.png)

## <a name="create-a-stream-analytics-job"></a>Criar um trabalho de Stream Analytics
1. Olá portal do Azure, o clique Olá sinal de adição verde no canto superior esquerdo Olá Olá página toocreate um novo trabalho de análise de fluxo. Selecione **Inteligência + Análise** e clique em **Trabalho do Stream Analytics**.
   
    ![Novo botão](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image21.png)
2. Forneça um nome de trabalho, validar assinatura hello está correto e, em seguida, criar um novo grupo de recursos no hello mesma região Olá armazenamento de hub de evento (o padrão é Centro Sul dos EUA para script hello).
3. Clique em **Pin toodashboard** e **criar** final Olá Olá página.
   
    ![Opção Criar um Trabalho do Stream Analytics](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image22.png)

## <a name="define-input-sources"></a>Definir fontes de entrada
1. Olá trabalho criar e abrir a página de saudação do trabalho. Ou você pode clicar em Olá ao criar trabalho de análise no painel do portal hello.

2. Clique em Olá **ENTRADAS** guia toodefine Olá fonte de dados.
   
    ![Guia de entradas de saudação](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image24.png)
3. Clique em **ADICIONAR UMA ENTRADA**.
   
    ![Olá, adicionar uma opção de entrada](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image25.png)
4. Digite **EntryStream** como **ALIAS DE ENTRADA**.
5. O Tipo de Origem é **Transmissão de Dados**
6. A Fonte é **Hub de eventos**.
7. **Namespace de barramento de serviço** devem ser Olá TollData uma saudação lista suspensa.
8. **Nome do hub de evento** deve ser definido muito**entrada**.
9. **Nome de política do hub de evento*é **RootManageSharedAccessKey** (Olá valor padrão).
10. Selecione **JSON** como **FORMATO DE SERIALIZAÇÃO DO EVENTO** e **UTF8** como **CODIFICAÇÃO**.
   
    As configurações ficarão semelhantes:
   
    ![Configurações do hub de evento](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image28.png)

10. Clique em **criar** na parte inferior de saudação do Assistente de Olá Olá página toofinish.
    
    Agora que você criou o fluxo de entrada hello, você seguirá Olá mesmo fluxo de saída etapas toocreate hello. Ser valores de tooenter-se em Olá captura de tela a seguir.
    
    ![Configurações de fluxo de saída de saudação de](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image31.png)
    
    Você definiu dois fluxos de entrada:
    
    ![Fluxos de entrada definidos no hello portal do Azure](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image32.png)
    
    Em seguida, você irá adicionar a entrada de dados de referência para o arquivo de blob de saudação que contém dados de registro de carro.
11. Clique em **adicionar**e, em seguida, siga Olá mesmo processo para entradas de fluxo hello, mas selecionar **dados de referência** em vez de **fluxo de dados** e hello **Alias de entrada**  é **registro**.

12. conta de armazenamento que começa com **tolldata**. nome do contêiner Olá deve ser **tolldata**e hello **padrão de caminho** devem ser **registration.json**. Este nome de arquivo diferencia maiúsculas de minúsculas e deve estar em **minúsculas**.
    
    ![Configurações de armazenamento de blob](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image34.png)
13. Clique em **criar** toofinish Assistente de saudação.

Agora, todas as entradas são definidas.

## <a name="define-output"></a>Definir saída
1. No painel de visão geral do trabalho do Stream Analytics hello, selecione **SAÍDAS**.
   
    ![Olá, guia saída e a opção "Adicionar uma saída de"](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image37.png)
2. Clique em **Adicionar**.
3. Saudação de conjunto **alias de saída** too'output' e, em seguida, **coletor** muito**banco de dados SQL**.
3. Selecione o nome do servidor de saudação que foi usado no Olá a seção "Conectar tooDatabase do Visual Studio" do artigo hello. nome do banco de dados de saudação é **TollDataDB**.
4. Digite **tolladmin** em Olá **USERNAME** campo, **123toll!** em Olá **senha** campo, e **TollDataRefJoin** em Olá **tabela** campo.
   
    ![Configurações do Banco de Dados SQL](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image38.png)
5. Clique em **Criar**.

## <a name="azure-stream-analytics-query"></a>Consulta do Stream Analytics do Azure
Olá **consulta** guia contém uma consulta SQL transformações Olá os dados de entrada.

![Uma consulta adicionada toohello guia de consulta](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image39.png)

Este tutorial tentativas tooanswer várias questões comerciais que estão relacionadas a dados tootoll e construtores de análise de fluxo de consultas que podem ser usados no Azure Stream Analytics tooprovide uma resposta relevante.

Antes de iniciar o trabalho do Stream Analytics primeiro, vamos explorar alguns cenários e sintaxe de consulta de saudação.

## <a name="introduction-tooazure-stream-analytics-query-language"></a>Introdução tooAzure linguagem de consulta do Stream Analytics
- - -
Digamos que você precisa que o número de saudação toocount dos veículos que insere um pedágio. Como esse é um fluxo contínuo de eventos, você tem toodefine um "período de tempo." Vamos modificar Olá pergunta toobe "quantos veículos inserir um pedágio a cada três minutos?". Isso é normalmente chamados tooas Olá em cascata contagem.

Vamos analisar consulta do Stream Analytics do Azure Olá que responde a essa pergunta:

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count
    FROM EntryStream TIMESTAMP BY EntryTime
    GROUP BY TUMBLINGWINDOW(minute, 3), TollId

Como você pode ver, o Azure Stream Analytics usa uma linguagem de consulta como SQL e adiciona algumas extensões toospecify tempo aspectos relacionados à consulta hello.

Para obter mais detalhes, leia sobre [gerenciamento de tempo](https://msdn.microsoft.com/library/azure/mt582045.aspx) e [janelas](https://msdn.microsoft.com/library/azure/dn835019.aspx) construções usadas na consulta de saudação do MSDN.

## <a name="testing-azure-stream-analytics-queries"></a>Testando consultas do Stream Analytics do Azure
Agora que você tenha escrito a primeira consulta do Stream Analytics do Azure, é hora tootest usando arquivos de dados de exemplo localizado na pasta TollApp no Olá que caminho a seguir:

**..\\TollApp\\TollApp\\Data**

Esta pasta contém Olá seguintes arquivos:

* Entry.json
* Exit.JSON
* registration.json

## <a name="question-1-number-of-vehicles-entering-a-toll-booth"></a>Pergunta 1: número de veículos que entram em uma cabine de pedágio
1. Abra hello portal do Azure e o trabalho do Stream Analytics do Azure vá tooyour criado. Clique em Olá **consulta** guia e cole a consulta da seção anterior hello.

2. toovalidate esta consulta em relação aos dados de exemplo, carregar dados Olá Olá EntryStream entrada clicando … Olá símbolo e selecionando **carregar dados de exemplo do arquivo**.

    ![Captura de tela de arquivo de Entry.json Olá](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image41.png)
3. No painel de saudação que aparece arquivo hello select (Entry.json) no seu computador local e clique em **Okey**. Olá **teste** ícone agora iluminam e ser clicável.
   
    ![Captura de tela de arquivo de Entry.json Olá](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image42.png)
3. Valide que saída Olá consulta Olá é conforme o esperado:
   
    ![Resultados de teste de saudação](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image43.png)

## <a name="question-2-report-total-time-for-each-car-toopass-through-hello-toll-booth"></a>Pergunta 2: Tempo total para cada toopass carro por meio de pedágio Olá de relatório
tempo médio de saudação necessária para toopass um carro por meio de pedágio Olá ajuda a eficiência de saudação tooassess do processo de saudação e experiência de saudação do cliente.

tempo total do toofind Olá, é necessário toojoin Olá EntryTime fluxo com o fluxo de ExitTime hello. Você adicionará fluxos Olá nas colunas TollId e LicencePlate. Olá **INGRESSAR** operador requer toospecify reserva temporal que descreve a diferença entre hello Unido eventos de tempo aceitável de saudação. Você usará **DATEDIFF** função toospecify que eventos devem ser não mais de 15 minutos entre si. Você também aplicará Olá **DATEDIFF** estação de chamada de função tooexit e entrada vezes toocompute Olá tempo real que um carro gasta em hello. Observe a diferença de saudação do uso de saudação do **DATEDIFF** quando ele é usado em uma **selecione** instrução em vez de **INGRESSAR** condição.

    SELECT EntryStream.TollId, EntryStream.EntryTime, ExitStream.ExitTime, EntryStream.LicensePlate, DATEDIFF (minute , EntryStream.EntryTime, ExitStream.ExitTime) AS DurationInMinutes
    FROM EntryStream TIMESTAMP BY EntryTime
    JOIN ExitStream TIMESTAMP BY ExitTime
    ON (EntryStream.TollId= ExitStream.TollId AND EntryStream.LicensePlate = ExitStream.LicensePlate)
    AND DATEDIFF (minute, EntryStream, ExitStream ) BETWEEN 0 AND 15

1. tootest nesta consulta, atualização Olá consulta em Olá **consulta** para trabalho hello. Adicionar arquivo de teste Olá para **ExitStream** como **EntryStream** foi especificado acima.
   
2. Clique em **Testar**.

3. Selecione Olá caixa de seleção tootest Olá consulta e exibição Olá saída:
   
    ![Saída do teste Olá](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image45.png)

## <a name="question-3-report-all-commercial-vehicles-with-expired-registration"></a>Pergunta 3: relatar todos os veículos comerciais com o registro vencido
O Azure Stream Analytics pode usar instantâneos estáticos dos dados toojoin com fluxos de dados temporais. toodemonstrate esse recurso, use Olá pergunta de exemplo a seguir.

Se um veículo comercial é registrado com a empresa de pedágio Olá, ele pode passar pelo pedágio Olá sem ser parado para inspeção. Você usará tooidentify de tabela de pesquisa de registro de veículo comercial todos os veículos comerciais registros expirados.

```
SELECT EntryStream.EntryTime, EntryStream.LicensePlate, EntryStream.TollId, Registration.RegistrationId
FROM EntryStream TIMESTAMP BY EntryTime
JOIN Registration
ON EntryStream.LicensePlate = Registration.LicensePlate
WHERE Registration.Expired = '1'
```

tootest uma consulta usando dados de referência, você precisa toodefine uma fonte de entrada hello dados de referência, que você tenha feito.

tootest nesta consulta, cole Olá consulta em hello **consulta** , clique em **teste**e especificar as fontes de entrada hello dois e o registro de saudação dados de exemplo e clique em **teste**.  
   
![Saída do teste Olá](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image46.png)

## <a name="start-hello-stream-analytics-job"></a>Iniciar o trabalho de análise de fluxo de saudação
Agora é hora toofinish Olá configuração e início Olá trabalho. Salvar a consulta de saudação da pergunta 3, que irá gerar saída correspondências Olá esquema da saudação **TollDataRefJoin** tabela de saída.

Trabalho vá toohello **painel**e clique em **iniciar**.

![Captura de tela do botão Iniciar de saudação no painel de trabalho Olá](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image48.png)

Na caixa de diálogo de saudação que é aberta, alterar Olá **iniciar saída** muito tempo**tempo personalizado**. Alteração Olá hora tooone hora antes Olá hora atual. Essa alteração garante que todos os eventos do hub de eventos de saudação são processados desde o início de eventos de saudação toogenerate no início de saudação do tutorial de saudação. Agora clique Olá **iniciar** trabalho de saudação do botão toostart.

![Seleção de hora personalizada](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image49.png)

Iniciando o trabalho Olá pode levar alguns minutos. Você pode ver o status de saudação na página de nível superior Olá para análises de fluxo.

![Captura de tela de status de saudação do trabalho de saudação](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image50.png)

## <a name="check-results-in-visual-studio"></a>Verificar resultados no Visual Studio
1. Abra o Visual Studio Server Explorer e clique Olá **TollDataRefJoin** tabela.
2. Clique em **Mostrar dados da tabela** toosee saída de saudação do seu trabalho.
   
    ![Seleção de "Mostrar Dados da Tabela" no Gerenciador de Servidores](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image51.jpg)

## <a name="scale-out-azure-stream-analytics-jobs"></a>Escalar horizontalmente trabalhos do Stream Analytics do Azure
O Azure Stream Analytics foi projetado tooelastically dimensionar para que ele possa manipular a muitos dados. consulta do Stream Analytics do Azure Olá pode usar um **PARTITION BY** sistema de saudação do tootell cláusula esta etapa será escalável. **PartitionId** é uma coluna especial Olá sistema adiciona toomatch Olá partição ID de entrada hello (hub de eventos).

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*)AS Count
    FROM EntryStream TIMESTAMP BY EntryTime PARTITION BY PartitionId
    GROUP BY TUMBLINGWINDOW(minute,3), TollId, PartitionId

1. Trabalho atual parar hello, atualização Olá consulta em Olá **consulta** guia e abra Olá **configurações** engrenagem no painel de trabalho hello. Clique em **Escala**.
   
    **UNIDADES de STREAMING** definir Olá o valor de capacidade de computação que Olá trabalho pode receber.
2. Olá suspenso Change de 1 de 6.
   
    ![Captura de tela da seleção de 6 unidades de streaming](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image52.png)
3. Vá toohello **SAÍDAS** guia e altere o nome de saudação da tabela do SQL Olá muito**TollDataTumblingCountPartitioned**.

Se você iniciar o trabalho de saudação agora, Stream Analytics do Azure pode distribuir o trabalho entre mais recursos de computação e obter melhor taxa de transferência. Observe que esse aplicativo TollApp Olá também está enviando eventos particionados por TollId.

## <a name="monitor"></a>Monitoramento
Olá **MONITOR** área contém estatísticas sobre Olá executando o trabalho. Primeira vez que a configuração é necessária toouse Olá conta de armazenamento Olá mesma região (nome de pedágio como Olá restante deste documento).   

![Captura de tela do monitor](media/stream-analytics-build-an-iot-solution-using-stream-analytics/monitoring.png)

Você pode acessar **Logs de atividade** do painel de trabalho Olá **configurações** área também.


## <a name="conclusion"></a>Conclusão
Este tutorial introduziu um serviço do Azure Stream Analytics toohello. Ele demonstrou como tooconfigure entradas e saídas para Olá trabalho do Stream Analytics. Usando o cenário de pedágio dados hello, tutorial Olá explicado tipos comuns de problemas que surgem no espaço de saudação de dados em movimento e como eles podem ser resolvidos com simples consultas SQL no Azure Stream Analytics. tutorial de saudação descrito SQL construções de extensão para trabalhar com dados temporais. Ele mostrou como toojoin fluxos de dados, como o fluxo de dados de saudação do tooenrich com dados de referência estática e tooscale-out de uma consulta tooachieve maior taxa de transferência.

Embora este tutorial forneça uma boa introdução, ele não é, de forma alguma, completo. Você pode encontrar mais padrões de consulta usando a linguagem SAQL Olá em [consultar exemplos de padrões de uso comuns do Stream Analytics](stream-analytics-stream-analytics-query-patterns.md).
Consulte toohello [documentação on-line](https://azure.microsoft.com/documentation/services/stream-analytics/) toolearn mais sobre o Azure Stream Analytics.

## <a name="clean-up-your-azure-account"></a>Limpar sua conta do Azure
1. Pare o trabalho de análise de fluxo de saudação no hello portal do Azure.
   
    Olá Setup.ps1 script cria dois hubs de eventos e um banco de dados SQL. Olá você limpar os recursos no final de saudação do tutorial de saudação de ajuda de instruções a seguir.
2. Em uma janela do PowerShell, digite **.\\ CleanUp.ps1** script hello toostart exclui os recursos usados no tutorial de saudação.
   
   > [!NOTE]
   > Recursos são identificados pelo nome da saudação. Certifique-se de examinar cuidadosamente cada item antes de confirmar a remoção.
   > 
   > 


