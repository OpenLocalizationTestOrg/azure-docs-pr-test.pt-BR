---
title: "Aprofunde-se nos aaaDeep prever a integridade de veículo e orientar hábitos - Azure | Microsoft Docs"
description: "Usar recursos de saudação do insights de previsão e em tempo real de inteligência Cortana toogain na integridade do veículo e orientar hábitos."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a>Guia estratégico de solução de análise de telemetria veículo: mergulho profundo na solução Olá
Isso **menu** toohello seções neste guia estratégico de links: 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

Esta seção faz uma busca detalhada em cada um dos estágios Olá descritos nos Olá arquitetura da solução com instruções e ponteiros para personalização. 

## <a name="data-sources"></a>Fontes de dados
solução de saudação usa duas fontes de dados diferentes:

* **sinais de veículo simulados, conjunto de dados de diagnóstico** e 
* **catálogo do veículo**

Um simulador de telemática do veículo é incluído como parte desta solução. Ele emite informações de diagnóstico e sinaliza o estado toohello correspondente de veículo hello e toohello direcionando padrão em um determinado ponto no tempo. Clique em [veículo Telemáticas da simulador](http://go.microsoft.com/fwlink/?LinkId=717075) Olá toodownload **veículo Telemáticas da simulador solução do Visual Studio** personalizações com base nos seus requisitos. Catálogo de veículo Olá contém um conjunto de dados de referência com um mapeamento de toomodel VIN.

![Simulador de telemática do veículo](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

*Figura 1 – Simulador de Telemática do Veículo*

Este é um conjunto de dados formatados em JSON que contém Olá esquema a seguir.

| Coluna | Descrição | Valores |
| --- | --- | --- |
| VIN |Número de Identificação do Veículo gerado aleatoriamente |É obtido em uma lista principal de 10.000 números de identificação do veículo gerados aleatoriamente. |
| Temperatura externa |Olá fora temperatura onde o veículo hello está aumentando |Número gerado aleatoriamente de 0 a 100 |
| Temperatura do motor |temperatura de mecanismo de saudação do veículo Olá |Número gerado aleatoriamente de 0 a 500 |
| Velocidade |velocidade do mecanismo Olá no qual Olá veículo está aumentando |Número gerado aleatoriamente de 0 a 100 |
| Combustível |nível de combustível de saudação do veículo Olá |Número gerado aleatoriamente de 0 a 100 (indica a porcentagem do nível de combustível) |
| Óleo do Motor |nível de petróleo mecanismo saudação do veículo Olá |Número gerado aleatoriamente de 0 a 100 (indica a porcentagem do nível de óleo do motor) |
| Pressão do pneu |pressão de pneu de saudação do veículo Olá |Número gerado aleatoriamente de 0 a 50 (indica a porcentagem do nível de pressão do pneu) |
| Hodômetro |leitura do odômetro saudação do veículo Olá |Número gerado aleatoriamente de 0 a 200.000 |
| Accelerator_pedal_position |posição de pedais Olá acelerador de veículo Olá |Número gerado aleatoriamente de 0 a 100 (indica a porcentagem do nível do acelerador) |
| Parking_brake_status |Indica se o veículo hello está estacionado ou não |Verdadeiro ou Falso |
| Headlamp_status |Indica onde lâmpada frontal de saudação está ativa ou não |Verdadeiro ou Falso |
| Brake_pedal_status |Indica se o pedal de freio Olá é pressionado ou não |Verdadeiro ou Falso |
| Transmission_gear_position |posição de engrenagem Olá transmissão de veículo Olá |Estados: primeira, segunda, terceira, quarta, quinta, sexta, sétima, oitava |
| Ignition_status |Indica se o veículo hello está em execução ou parado |Verdadeiro ou Falso |
| Windshield_wiper_status |Indica se a wiper de para-brisa hello está ativada ou não |Verdadeiro ou Falso |
| ABS |Indica se o ABS está engatado ou não |Verdadeiro ou Falso |
| Timestamp |Olá carimbo de hora do ponto de dados de saudação é criado |Data |
| City |local de saudação do veículo Olá |Há quatro cidades nesta solução: Bellevue, Redmond, Sammamish, Seattle |

conjunto de dados de referência do Hello veículo modelo contém o mapeamento do modelo toohello VIN. 

| VIN | Modelo |
| --- | --- |
| FHL3O1SA4IEHB4WU1 |Automóvel Sedan |
| 8J0U8XCPRGW4Z3NQE |Híbrido |
| WORG68Z2PLTNZDBI7 |Automóvel de três volumes |
| JTHMYHQTEPP4WBMRN |Automóvel Sedan |
| W9FTHG27LZN1YWO0Y |Híbrido |
| MHTP9N792PHK08WJM |Automóvel de três volumes |
| EI4QXI2AXVQQING4I |Automóvel Sedan |
| 5KKR2VB4WHQH97PF8 |Híbrido |
| W9NSZ423XZHAONYXB |Automóvel de três volumes |
| 26WJSGHX4MA5ROHNL |Conversível |
| GHLUB6ONKMOSI7E77 |Van |
| 9C2RHVRVLMEJDBXLP |Carro compacto |
| BRNHVMZOUJ6EOCP32 |SUV pequeno |
| VCYVW0WUZNBTM594J |Carro esportivo |
| HNVCE6YFZSA5M82NY |SUV médio |
| 4R30FOR7NUOBL05GJ |Van |
| WYNIIY42VKV6OQS1J |SUV grande |
| 8Y5QKG27QET1RBK7I |SUV grande |
| DF6OX2WSRA6511BVG |Cupê |
| Z2EOZWZBXAEW3E60T |Automóvel Sedan |
| M4TV6IEALD5QDS3IR |Híbrido |
| VHRA1Y2TGTA84F00H |Automóvel de três volumes |
| R0JAUHT1L1R3BIKI0 |Automóvel Sedan |
| 9230C202Z60XX84AU |Híbrido |
| T8DNDN5UDCWL7M72H |Automóvel de três volumes |
| 4WPYRUZII5YV7YA42 |Automóvel Sedan |
| D1ZVY26UV2BFGHZNO |Híbrido |
| XUF99EW9OIQOMV7Q7 |Automóvel de três volumes |
| 8OMCL3LGI7XNCC21U |Conversível |
| ……. | |

### <a name="references"></a>Referências
[Solução Vehicle Telematics Simulator do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=717075) 

[Hub de Eventos do Azure](https://azure.microsoft.com/services/event-hubs/)

[Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a>Ingestão
Combinações de fábrica de dados, análise de fluxo e Hubs de eventos do Azure são sinais de veículo tooingest utilizou hello, eventos de diagnóstico Olá e em tempo real e análise em lote. Todos esses componentes são criados e configurados como parte da implantação de solução de saudação. 

### <a name="real-time-analysis"></a>Análise em tempo real
Olá eventos gerados pelo Olá veículo Telemáticas da simulador são publicados usando o Hub de eventos toohello Olá SDK do Hub de eventos. trabalho de análise de fluxo de saudação consome esses eventos de saudação Hub de eventos e processos Olá dados a integridade de veículo de saudação tooanalyze em tempo real. 

![Painel do Hub de Eventos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

*Figura 4 – Painel do Hub de Eventos*

![Dados de processamento do trabalho do Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

*Figura 5 – Dados de processamento do trabalho do Stream Analytics*

trabalho de análise de fluxo de saudação;

* consome dados de saudação Hub de eventos 
* executa uma junção com hello referência toomap Olá veículo VIN toohello correspondente modelo de dados 
* persisti-los no armazenamento de blobs do Azure para análise avançada em lote. 

Olá consulta de análise de fluxo a seguir é usado toopersist Olá dados no armazenamento de BLOBs do Azure. 

![Consulta do trabalho do Stream Analytics para a ingestão de dados](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

*Figura 6 – Consulta do trabalho do Stream Analytics para a ingestão de dados*

### <a name="batch-analysis"></a>Análise do lote
Também podemos gerar um volume adicional de sinais simulados do veículo e um conjunto de dados de diagnóstico para fazer uma análise de lote mais avançada. Isso é necessário tooensure um volume de dados representativo para processamento em lotes. Para essa finalidade, estamos usando um pipeline denominado "PrepareSampleDataPipeline" em toogenerate de fluxo de trabalho do Azure Data Factory Olá registros um ano de veículo simulada sinais e o conjunto de dados de diagnóstico. Clique em [atividade personalizada de fábrica de dados](http://go.microsoft.com/fwlink/?LinkId=717077) Olá toodownload atividade de DotNet fábrica de dados personalizada solução do Visual Studio para personalizações de acordo com suas necessidades. 

![Preparar os dados de exemplo para o fluxo de trabalho do processamento em lote](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

*Figura 7 – Preparar os dados de exemplo para o fluxo de trabalho do processamento em lote*

Olá pipeline consiste em um .net ADF personalizado atividade, mostrados aqui:

![PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

*Figura 8 – PrepareSampleDataPipeline*

Depois que o pipeline Olá for executado com êxito e "RawCarEventsTable" conjunto de dados está marcado como "Pronto", um ano vale a pena de veículo simulada sinais e diagnóstico dados são produzidos. Veja a seguir Olá pastas e arquivos criados na sua conta de armazenamento no contêiner do "connectedcar" hello:

![Saída de PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

*Figura 9 – Saída de PrepareSampleDataPipeline*

### <a name="references"></a>Referências
[SDK do Hub de Eventos do Azure para ingestão de fluxo](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

[Recursos de movimentação de dados do Azure Data Factory](../data-factory/data-factory-data-movement-activities.md)
[Atividade DotNet do Azure Data Factory](../data-factory/data-factory-use-custom-activities.md)

[Solução do Visual Studio de atividade DotNet do Azure Data Factory para preparação de dados de exemplo](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a>Conjunto de dados de saudação de partição
Olá bruto veículo semi-estruturados sinais e o conjunto de dados de diagnóstico são particionadas na etapa de preparação de dados Olá em um formato de ano/mês. Esse particionamento promove a consulta mais eficiente e escalonável armazenamento de longo prazo, permitindo sobre falhas de um blob conta toohello próximo como conta primeiro Olá preenchido. 

>[!NOTE] 
>Esta etapa na solução de saudação é processamento toobatch somente aplicável.

Entrada e saída de gerenciamento de dados:

* Olá **dados de saída** (rotulado *PartitionedCarEventsTable*) é toobe mantida por um longo período de tempo como o formulário básico / "rawest" hello de dados "Data Lake" do cliente hello. 
* Olá **dados de entrada** toothis pipeline normalmente seria descartada como dados de saída de saudação tem toohello fidelidade completa de entrada - apenas é armazenado (particionado) melhor para uso posterior.

![Fluxo de trabalho de eventos de partição de carros](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

*Figura 10 – Fluxo de trabalho de eventos de partição de carros*

dados brutos de saudação são particionados usando uma atividade de HDInsight Hive em "PartitionCarEventsPipeline". dados de exemplo Hello gerados na etapa 1 para um ano são particionados por mês/ano. as partições de Hello são usadas toogenerate veículo sinais e dados de diagnóstico para cada mês (total de 12 partições) de um ano. 

![Atividade de PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

*Figura 11 – PartitionCarEventsPipeline*

***Script do Hive de PartitionConnectedCarEvents***

Hello seguinte script de Hive, chamado "partitioncarevents.hql", é usado para particionamento e está localizado na pasta de "\demo\src\connectedcar\scripts" hello do zip Olá baixado. 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

Depois que o pipeline de saudação for executada com êxito, você verá Olá partições geradas em sua conta de armazenamento no contêiner do "connectedcar" hello a seguir.

![Saída particionada](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

*Figura 12 – Saída Particionada*

dados de saudação agora é otimizado, é mais gerenciáveis e pronto para processamento adicional de informações de lote rich toogain. 

## <a name="data-analysis"></a>Análise de Dados
Nesta seção, consulte como toocombine Stream Analytics do Azure, aprendizado de máquina do Azure, Azure Data Factory e do Azure HDInsight para rich avançado hábitos de análise de integridade de veículo e referências. Há três subseções aqui:

1. **Aprendizado de máquina**: Esta subseção contém informações sobre a experiência de detecção de anomalias de saudação que foram usados em veículos de toopredict essa solução exigir a manutenção e veículos exigir recuperações devido a problemas de toosafety de manutenção.
2. **Análise em tempo real**: Esta subseção contém informações sobre análise de em tempo real hello usando Olá a linguagem de consulta do Stream Analytics e operacionalização de aprendizado de máquina Olá experiências em tempo real usando um aplicativo personalizado.
3. **Análise de lote**: Esta subseção contém informações relativas a saudação transformar e processamento de dados de lote hello usando HDInsight do Azure e aprendizado de máquina do Azure operacionalizada pela fábrica de dados do Azure.

### <a name="machine-learning"></a>Machine Learning
Nossa meta é veículos de saudação toopredict que exigem manutenção ou a recuperação baseada em determinadas estatísticas de integridade. Fazemos Olá suposições a seguir

* Se uma saudação três condições a seguir forem verdadeira, veículos Olá exigem **manutenção manutenção**:
  
  * A pressão do pneu está baixa
  * O nível de óleo do motor está baixo
  * A temperatura do motor está alta
* Se uma saudação seguintes condições forem verdadeira, veículos Olá podem ter um **problema de segurança** e exigem **recuperação**:
  
  * A temperatura do motor é alta, mas a temperatura externa é baixa
  * A temperatura do motor é baixa, mas a temperatura externa é alta

Com base nos requisitos de saudação anterior, nós criamos anomalias de toodetect dois modelos separados, um para detecção de manutenção de veículo e outra para detecção de recuperação do veículo. Em ambos os esses modelos, algoritmo de análise de componente Principal (PCA) interno Olá é usado para detecção de anomalias. 

**Modelo de detecção de manutenção**

Se um dos três indicadores pneu pressão, petróleo mecanismo ou temperatura mecanismo - satisfizer sua condição do respectiva, o modelo de detecção de manutenção de saudação relata uma anomalia. Como resultado, precisamos apenas tooconsider essas três variáveis na criação de modelo de saudação. Em nossa experiência no aprendizado de máquina do Azure, primeiro usamos uma **selecionar colunas no conjunto de dados** tooextract módulo esses três variáveis. Em seguida, usamos Olá anomalias com base em PCA detecção módulo toobuild Olá anomalias modelo de detecção. 

Análise de componente principal (PCA) é uma técnica estabelecida no aprendizado de máquina que pode ser aplicadas toofeature detecção de anomalias, classificação e seleção. O PCA converte um conjunto de casos contendo variáveis possivelmente correlacionadas em um conjunto de valores chamado de componentes principais. a ideia chave Olá de modelagem com base em PCA é tooproject dados em um espaço menor dimensional para anomalias e recursos podem ser identificadas com mais facilidade.

Para cada nova entrada hello muito o modelo de detecção, detector de anomalias Olá primeiro calcula sua projeção de eigenvectors hello e, em seguida, calcula Olá normalizado erro reconstrução. Esse erro normalizado é Olá anomalias. Erro de saudação superior Olá, hello mais anormal Olá instância é. 

Problema de detecção de manutenção hello, cada registro pode ser considerado como um ponto em um espaço de 3-dimensional definido pela pressão pneu, petróleo mecanismo e temperatura de mecanismo coordenadas. toocapture essas anomalias, podemos pode dados de projeto Olá original no espaço de 3-dimensional de saudação para um espaço 2-dimensional usando PCA. Assim, definimos o parâmetro hello número de componentes toouse em PCA toobe 2. Esse parâmetro desempenha um papel importante na aplicação da detecção de anomalias com base no PCA. Depois de projetar os dados usando o PCA, podemos identificar essas anomalias mais facilmente.

**Modelo de detecção de anomalias de recuperação** no modelo de detecção de anomalias de recuperação hello, usamos Olá selecionar colunas no conjunto de dados e de anomalias com base em PCA módulos de detecção de maneira semelhante. Especificamente, podemos primeiro extrair a três variáveis - temperatura de mecanismo, temperatura externa e velocidade - usando Olá **selecionar colunas no conjunto de dados** módulo. Também incluímos velocidade Olá variável desde que a temperatura do mecanismo de saudação normalmente está correlacionada toohello velocidade. Em seguida, usamos a dados de saudação tooproject do módulo de detecção de anomalias com base em PCA de espaço de 3-dimensional Olá para um 2-dimensional. Olá recuperação critérios são atendidos e então veículo Olá requer o Lembre-se quando a temperatura do mecanismo e temperatura fora altamente negativamente são correlacionadas. Usando o algoritmo de detecção de anomalias com base em PCA, podemos capturar anomalias Olá depois de executar o PCA. 

Quando o modelo de treinamento, precisamos de dados normal toouse, que não exigem manutenção ou lembre-se de que o modelo de detecção de anomalias com base em PCA Olá dados de entrada tootrain hello. Olá experimento de pontuação, usamos toodetect de modelo de detecção de anomalias Olá treinado se veículo Olá exige manutenção ou lembre-se ou não. 

### <a name="real-time-analysis"></a>Análise em tempo real
saudação de consulta do Stream Analytics SQL a seguir é usada tooget média de saudação de todas as Olá parâmetros de veículo importantes, como velocidade de veículo, nível de combustível, temperatura de mecanismo, leitura do odômetro, pneu pressão, nível de petróleo mecanismo e outros. médias Hello são usadas toodetect anomalias, emitir alertas e determinar Olá condições de integridade geral dos veículos operados na região específica e correlacioná-lo toodemographics. 

![Consulta do Stream Analytics para o processamento em tempo real](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

*Figura 13 – Consulta do Stream Analytics para o processamento em tempo real*

Todas as médias de saudação são calculadas em um TumblingWindow de 3 segundos. Estamos usando uma TubmlingWindow neste caso, pois exigimos intervalos de tempo que não se sobrepõem e são contínuos. 

toolearn mais informações sobre todos os recursos de "Janelas" hello no Azure Stream Analytics, clique em [janelas (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).

**Previsão em tempo real**

Um aplicativo é incluído como parte do modelo de aprendizado de máquina solução toooperationalize Olá Olá em tempo real. Este aplicativo chamado "RealTimeDashboardApp" é criado e configurado como parte da implantação de solução de saudação. aplicativo Hello executa seguinte hello:

1. Escuta tooan instância de Hub de eventos onde Stream Analytics é publicar Olá eventos em um padrão de continuamente. ![Consulta de análise de fluxo para publicar dados Olá](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figura 14 – a consulta do Stream Analytics para publicar Olá dados tooan instância de Hub de eventos de saída* 
2. Para cada evento que esse aplicativo recebe: 
   
   * Processos Olá dados usando o ponto de extremidade de pontuação de solicitação-resposta de aprendizado máquina (RR). o ponto de extremidade do Hello RRS é automaticamente publicado como parte da implantação de saudação.
   * a saída RRS Olá é o conjunto de dados do Power BI tooa publicado usando APIs de envio por push hello.

Esse padrão também é aplicável tooscenarios no qual você deseja toointegrate um aplicativo de linha de negócios (LoB) com o fluxo de análise em tempo real de hello, para cenários como alertas, notificações e mensagens.

Clique em [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) Olá toodownload solução RealtimeDashboardApp Visual Studio para personalizações. 

**Olá tooexecute aplicativo de painel em tempo real**
1. Extrair e salvar localmente a ![Pasta RealtimeDashboardApp](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figura 16 – Pasta RealtimeDashboardApp*  
2. Execute o aplicativo hello RealtimeDashboardApp.exe
3. Forneça credenciais válidas do Power BI, entre e clique em Aceitar ![Aplicativo de painel em tempo real entrar tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Aplicativo de painel em tempo real concluir entrar tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

*Figura 17 – RealtimeDashboardApp: Entrar tooPower BI*

>[!NOTE] 
>Se desejar que o conjunto de dados tooflush Olá Power BI, execute Olá RealtimeDashboardApp com o parâmetro "flushdata" hello: 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a>Análise do lote
Olá meta é tooshow como Contoso motores utiliza Olá computação do Azure recursos tooharness grandes dados toogain informações valiosas definir padrão, o comportamento de uso e integridade de veículo. Isso possibilita:

* Melhorar a experiência do cliente hello e torná-lo mais barato, fornecendo informações sobre orientando hábitos e comportamentos de um eficiente de combustível
* Saiba proativamente sobre clientes e suas decisões de negócios toogovern padrões de carro e fornecer Olá melhor na classe produtos e serviços

Nesta solução, pretendemos Olá métricas a seguir:

1. **Agressivo orientando comportamento**: identifica a tendência de saudação do hello modelos, locais, condições de referências e tempo de informações de toogain ano Olá nos padrões de um agressivas. A Contoso Motors pode usar essas informações para campanhas de marketing, orientando novos recursos personalizados e seguro baseado em uso.
2. **Comportamento de um eficiente de combustível**: identifica a tendência de saudação do hello modelos, locais, condições de carro e tempo de saudação ano toogain visões e padrões de um eficiente de combustível. Motores Contoso pode usar essas informações para campanhas de marketing orienta a novos recursos e pró-ativo drivers toohello reporting para custam efetivo e ambiente hábitos de carro amigáveis. 
3. **Lembre-se de modelos**: identifica os modelos que exigem recuperações por operacionalização experiência de aprendizado de máquina de detecção de anomalias de saudação

Vamos dar uma olhada nos detalhes de saudação de cada uma dessas métricas

**Padrão de condução agressiva**

Olá particionado veículo sinais e dados de diagnóstico são processados no pipeline de saudação denominado "AggresiveDrivingPatternPipeline" usando modelos de saudação do Hive toodetermine, local, vehicle, gerando condições e outros parâmetros que exibe agressivo um padrão.

![Fluxo de trabalho de padrão de condução agressiva](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figura 18 – Fluxo de trabalho de padrão de condução agressiva*


***Consulta do Hive do padrão de condução agressiva***

Olá script de Hive chamado "aggresivedriving.hql" usado para analisar agressiva um padrão de condição está localizado na pasta "\demo\src\connectedcar\scripts" do zip Olá baixado. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


Ela usa a combinação de saudação da veículo posição de engrenagem de transmissão, freio pedais status e velocidade toodetect precipitado/agressiva orientando comportamento com base no modelo padrão em alta velocidade. 

Depois que o pipeline de saudação for executada com êxito, você verá Olá partições geradas em sua conta de armazenamento no contêiner do "connectedcar" hello a seguir.

![Saída do AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

*Figura 19 – Saída do AggressiveDrivingPatternPipeline*

**Padrão de condução para a eficiência do combustível**

Olá particionado veículo sinais e dados de diagnóstico são processados no pipeline de saudação denominado "FuelEfficientDrivingPatternPipeline". Hive é usado toodetermine Olá modelos, local, veículo, condições uma e outras propriedades que apresentam o padrão de um eficiente combustível.

![Padrão de condução para a eficiência do combustível](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

*Figura 20 – Fluxo de trabalho do padrão de condução para a eficiência do combustível*

***Consulta do Hive do padrão de condução para a eficiência do combustível***

Olá script de Hive chamado "fuelefficientdriving.hql" usado para analisar agressiva um padrão de condição está localizado na pasta "\demo\src\connectedcar\scripts" do zip Olá baixado. 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


Ele usa a combinação de saudação de posição de engrenagem de transmissão do veículo, status pedais freio, velocidade e combustível de toodetect posição pedais de acelerador comportamento um eficiente com base em aceleração, modelo, e acelerar padrões. 

Depois que o pipeline de saudação for executada com êxito, você verá Olá partições geradas em sua conta de armazenamento no contêiner do "connectedcar" hello a seguir.

![Saída do FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

*Figura 21 – Saída do FuelEfficientDrivingPatternPipeline*

**Previsões do Recall**

experiência de aprendizado de máquina de saudação é provisionada e publicada como um serviço web como parte da implantação de solução de saudação. ponto de extremidade de pontuação de lote de saudação é utilizado nesse fluxo de trabalho, registrado como um serviço vinculado de fábrica de dados e operacionalizada usando a atividade de pontuação de lote de fábrica de dados.

![Ponto de extremidade de Machine Learning](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

*Figura 22 – Ponto de extremidade do Machine Learning registrado como um serviço vinculado no data factory*

Olá serviço vinculado registrado é usado nos Olá DetectAnomalyPipeline tooscore Olá dados usando o modelo de detecção de anomalias de saudação. 

![Atividade de pontuação em lote do Machine Learning no data factory](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

*Figura 23 – Atividade de pontuação em lote do Azure Machine Learning no data factory* 

Há algumas etapas executadas nesse pipeline para preparação de dados para que ele pode ser operacionalizado com o serviço web de pontuação de lote de saudação. 

![DetectAnomalyPipeline para prever os veículos que exigem recalls](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

*Figura 24 – DetectAnomalyPipeline para prever os veículos que exigem recalls* 

***Consulta do Hive para detecção de anomalias***

Depois de saudação de pontuação é concluída, uma atividade de HDInsight é tooprocess usados e os dados de agregação Olá categorizadas como anomalias pelo modelo de saudação com uma pontuação de probabilidade de 0,60 ou superior.

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


Depois que o pipeline de saudação for executada com êxito, você verá Olá partições geradas em sua conta de armazenamento no contêiner do "connectedcar" hello a seguir.

![Saída de DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

*Figura 25 – Saída do DetectAnomalyPipeline*

## <a name="publish"></a>Publicar

### <a name="real-time-analysis"></a>Análise em tempo real
Uma das consultas Olá no trabalho do Stream Analytics Olá publica saída de tooan eventos hello instância do Hub de eventos. 

![Trabalho do Stream Analytics publica saída tooan instância de Hub de eventos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

*Figura 26 – trabalho do Stream Analytics publica saída tooan instância de Hub de eventos*

![Instância do Hub de eventos de saída do Stream Analytics consulta toopublish toohello](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

*Figura 27 – toohello de toopublish de consulta do Stream Analytics instância do Hub de eventos de saída*

Este fluxo de eventos é consumido pelos Olá que realtimedashboardapp incluído na solução de saudação. Este aplicativo utiliza o serviço de web de aprendizado de máquina solicitação-resposta Olá para pontuação em tempo real e publica Olá dados resultantes tooa Power BI dataset para consumo. 

### <a name="batch-analysis"></a>Análise do lote
Olá resultados lote hello e processamento em tempo real são tabelas de banco de dados do Azure SQL toohello publicados para consumo. Hello Azure SQL Server, o banco de dados e tabelas de saudação são criadas automaticamente como parte do script de instalação de saudação. 

![Fluxo de trabalho toodata mart de copiar resultados de processamento em lote](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

*Figura 28 – resultados copiar toodata mart fluxo de trabalho de processamento em lotes*

![Trabalho do Stream Analytics publica mart toodata](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

*Figura 29 – trabalho do Stream Analytics publica mart toodata*

![Configuração do data mart no trabalho do Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

*Figura 30 – Configuração do data mart no trabalho do Stream Analytics*

## <a name="consume"></a>Consumir
O PowerBI fornece essa solução a um painel avançado para os dados em tempo real e as visualizações da análise preditiva. 

Clique aqui para obter instruções detalhadas sobre como configurar relatórios do Power BI hello e painel de saudação. painel final Olá tem esta aparência:

![Painel do Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

*Figura 31 – Painel do Power BI*

## <a name="summary"></a>Resumo
Este documento contém um detalhamento de saudação veículo solução de análise de telemetria. Isto apresenta um padrão de arquitetura lambda para a análise em tempo real e em lote com previsões e ações. Esse padrão se aplica a tooa ampla variedade de casos de uso que exigem o afunilamento (em tempo real) e análise de caminho frio (em lotes). 

