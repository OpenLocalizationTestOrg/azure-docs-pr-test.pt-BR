---
title: "API de detecção de anomalias de aprendizado de máquina do aaaAzure | Microsoft Docs"
description: "A API de detecção de anomalias é um exemplo criado com o Microsoft Azure Machine Learning que detecta anomalias nos dados de série temporal com valores numéricos que são espaçados uniformemente no tempo."
services: machine-learning
documentationcenter: 
author: alokkirpal
manager: jhubbard
editor: cgronlun
ms.assetid: 52fafe1f-e93d-47df-a8ac-9a9a53b60824
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/05/2017
ms.author: alok;rotimpe
ms.openlocfilehash: ce153689b8ddb36b67a2ad3607d846ea83ebcf61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-anomaly-detection-api"></a>API de detecção de anomalias do Machine Learning
## <a name="overview"></a>Visão geral
A [API de detecção de anomalias](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2) é um exemplo criado com o Azure Machine Learning que detecta anomalias nos dados de série temporal com valores numéricos que são espaçados uniformemente no tempo.

Esta API pode detectar Olá seguintes tipos de padrões anormais em dados de série temporal:

* **Tendências positivas e negativas**: por exemplo, ao monitorar o uso da memória na computação, uma tendência de aumento pode ser interessante, pois ela pode indicar um vazamento de memória,
* **Alterações no intervalo de saudação dinâmico de valores**: por exemplo, quando o monitoramento de exceções de saudação geradas por um serviço de nuvem, as alterações no intervalo de saudação dinâmico de valores podem indicar instabilidade na integridade de saudação do serviço Olá, e
* **Altos e baixos**: por exemplo, ao monitorar o número de saudação de falhas de logon em um serviço ou o número de check-outs em um site de comércio eletrônico, picos ou queda pode indicar um comportamento anormal.

Esses detectores de aprendizado da máquina rastreiam as alterações nos valores ao longo do tempo e informam as mudanças contínuas em seus valores como pontuações de anomalia. Não precisam de ajuste de limite de ad hoc e suas classificações podem ser usados toocontrol falsos positivos. detecção de anomalias Olá API é útil em vários cenários como o monitoramento do serviço rastreando KPIs ao longo do tempo, o uso de monitoramento por meio de métricas, como o número de pesquisas, número de cliques, monitoramento de desempenho por meio de contadores, como memória, CPU, leituras, etc. ao longo do tempo.

oferta de detecção de anomalias Olá vem com ferramentas úteis tooget que é iniciado.

* Olá [aplicativo web](http://anomalydetection-aml.azurewebsites.net/) ajuda você a avaliar e visualizar os resultados de saudação de APIs de detecção de anomalias em seus dados.

> [!NOTE]
> Tente a **solução IT Anomaly Insights** fornecida por [essa API](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2)
> 
> tooget essa solução de tooend final implantado tooyour assinatura do Azure <a href="https://gallery.cortanaintelligence.com/Solution/Anomaly-Detection-Pre-Configured-Solution-1" target="_blank"> **Iniciar aqui >**</a>
> 
>

## <a name="api-deployment"></a>Implantação da API
Saudação de toouse ordem API, você deve implantá-lo tooyour assinatura do Azure, onde ele será hospedado como um serviço web de aprendizado de máquina do Azure.  Você pode fazer isso de saudação [Cortana Intelligence galeria](https://gallery.cortanaintelligence.com/MachineLearningAPI/Anomaly-Detection-2).  Isso irá implantar dois serviços da Web AzureML (e seus recursos relacionados) tooyour assinatura do Azure - uma para detecção de anomalias com detecção de sazonalidade e sem detecção de periodicidade.  Quando Olá implantação for concluída, será possível toomanage suas APIs do hello [serviços web do AzureML](https://services.azureml.net/webservices/) página.  Nessa página, você será ser capaz de toofind seus locais de ponto de extremidade, chaves de API, bem como exemplo de código para chamar a API de saudação.  Instruções mais detalhadas estão disponíveis [aqui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice).

## <a name="scaling-hello-api"></a>Olá escala API
Por padrão, sua implantação terá um plano de cobrança de desenvolvimento/teste gratuito que inclui 1.000 transações/mês e 2 horas de computação/mês.  Você pode atualizar o plano de tooanother de acordo com suas necessidades.  Detalhes sobre Olá preços das diferentes planos estão disponíveis [aqui](https://azure.microsoft.com/en-us/pricing/details/machine-learning/) em "Preços de API da Web de produção".

## <a name="managing-aml-plans"></a>Gerenciando planos do AML 
Você pode gerenciar seu plano de cobrança [aqui](https://services.azureml.net/plans/).  nome do plano de saudação se baseará no nome do grupo de recursos Olá escolhido durante a implantação de API hello, além de uma cadeia de caracteres que é exclusivo tooyour assinatura.  Instruções sobre como tooupgrade seu plano estão disponíveis [aqui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-manage-new-webservice) na seção de "Gerenciar planos de cobrança" hello.

## <a name="api-definition"></a>Definição da API
Olá, serviço web fornece uma API baseada em REST sobre HTTPS que podem ser consumidos maneiras diferentes, incluindo um web ou aplicativo móvel, R, Python, Excel, etc.  Enviar o seu serviço de toothis de dados de série do tempo por meio de uma chamada à API REST e ele é executado em uma combinação de saudação três tipos de anomalias descrito abaixo.

## <a name="calling-hello-api"></a>Chamar a API de saudação
Saudação de toocall ordem API, você precisará tooknow local de ponto de extremidade de saudação e a chave de API.  Ambos, juntamente com o código de exemplo para chamar a API de hello, estão disponíveis no hello [serviços web do AzureML](https://services.azureml.net/webservices/) página.  Navegue API toohello desejado e clique em hello "Consumir" guia toofind-los.  Observe que você pode chamar a API de saudação como uma API Swagger (ou seja, com o parâmetro de URL hello `format=swagger`) ou como uma não - Swagger API (ou seja, sem Olá `format` parâmetro de URL).  o código de exemplo Hello usa o formato de Swagger de saudação.  Veja abaixo um exemplo de solicitação e resposta em um formato não Swagger.  Esses exemplos são o ponto de extremidade do toohello periodicidade.  o ponto de extremidade do Hello periodicidade não é semelhante.

### <a name="sample-request-body"></a>Exemplo de corpo da solicitação
solicitação de saudação contém dois objetos: `Inputs` e `GlobalParameters`.  Solicitação de exemplo hello abaixo, alguns parâmetros são enviados explicitamente enquanto outros não são (para obter uma lista completa de parâmetros para cada ponto de extremidade, role para baixo).  Parâmetros que não são explicitamente enviados na solicitação Olá usará valores padrão de saudação indicados abaixo.

    {
                "Inputs": {
                        "input1": {
                                "ColumnNames": ["Time", "Data"],
                                "Values": [
                                        ["5/30/2010 18:07:00", "1"],
                                        ["5/30/2010 18:08:00", "1.4"],
                                        ["5/30/2010 18:09:00", "1.1"]
                                ]
                        }
                },
        "GlobalParameters": {
            "tspikedetector.sensitivity": "3",
            "zspikedetector.sensitivity": "3",
            "bileveldetector.sensitivity": "3.25",
            "detectors.spikesdips": "Both"
        }
    }

### <a name="sample-response"></a>Exemplo de Resposta
Observe que, no saudação do pedido toosee `ColumnNames` campo, você deve incluir `details=true` como um parâmetro de URL em sua solicitação.  Consulte as tabelas de saudação abaixo significado Olá atrás de cada um desses campos.

    {
        "Results": {
            "output1": {
                "type": "table",
                "value": {
                    "Values": [
                        ["5/30/2010 6:07:00 PM", "1", "1", "0", "0", "-0.687952590518378", "0", "-0.687952590518378", "0", "-0.687952590518378", "0"],
                        ["5/30/2010 6:08:00 PM", "1.4", "1.4", "0", "0", "-1.07030497733224", "0", "-0.884548154298423", "0", "-1.07030497733224", "0"],
                        ["5/30/2010 6:09:00 PM", "1.1", "1.1", "0", "0", "-1.30229513613974", "0", "-1.173800281031", "0", "-1.30229513613974", "0"]
                    ],
                    "ColumnNames": ["Time", "OriginalData", "ProcessedData", "TSpike", "ZSpike", "BiLevelChangeScore", "BiLevelChangeAlert", "PosTrendScore", "PosTrendAlert", "NegTrendScore", "NegTrendAlert"],
                    "ColumnTypes": ["DateTime", "Double", "Double", "Double", "Double", "Double", "Int32", "Double", "Int32", "Double", "Int32"]
                }
            }
        }
    }


## <a name="score-api"></a>API de Pontuação
Olá API de pontuação é usado para executar a detecção de anomalias nos dados de série temporal não sazonais. Olá API executa um número de detectores de anomalias nos dados hello e retorna suas classificações de anomalias. a Figura Olá abaixo mostra um exemplo de anomalias que Olá que API de pontuação pode detectar. A série temporal tem duas alterações distintas no nível e três picos. pontos Olá vermelha mostram o tempo de saudação no qual Olá alteração do nível é detectada, enquanto pontos Olá preto mostram picos Olá detectado.
![API de Pontuação][1]

### <a name="detectors"></a>Detectores
detecção de anomalias Olá API dá suporte a detectores em 3 categorias abrangentes. Detalhes sobre parâmetros de entrada específicos e saídas para cada detector podem ser encontrados em Olá a tabela a seguir.

| Categoria do Detector | Detector | Descrição | Parâmetros de Entrada | Saídas |
| --- | --- | --- | --- | --- |
| Detectores de Pico |Detector TSpike |Detectar picos e dips com base em Olá distante os valores são de Quartis primeiro e terceiro |*tspikedetector.Sensitivity:* usa o valor inteiro no intervalo de saudação padrão de 1 a 10: 3; Valores mais altos irá capturar mais valores extremos tornando menos confidencial |TSpike: valores binários – '1' se um pico/queda for detectado, '0' do contrário |
| Detectores de Pico | Detector ZSpike |Detectar picos e dips com base em quanto datapoints de saudação são de sua média |*zspikedetector.Sensitivity:* usar valor inteiro no intervalo de saudação padrão de 1 a 10: 3; Valores mais altos irá capturar mais valores extremos, tornando-o menos confidencial |ZSpike: valores binários – '1' se um pico/queda for detectado, '0' do contrário | |
| Detector de Tendências Lentas |Detector de Tendências Lentas |Detectar a tendência positiva lenta de acordo com a sensibilidade do conjunto de saudação |*trenddetector.Sensitivity:* limite de pontuação de detector (padrão: 3,25, 3,25 – 5 é tooselect um intervalo razoável de; Olá Olá maior menos sensível) |tscore: número flutuante que representa a pontuação de anomalias na tendência |
| Detectores de Alteração no Nível | Detector de Alteração no Nível Bidirecional |Detectar alteração para cima e para baixo nível, de acordo com a sensibilidade do conjunto de saudação |*bileveldetector.Sensitivity:* limite de pontuação de detector (padrão: 3,25, 3,25 – 5 é tooselect um intervalo razoável de; Olá Olá maior menos sensível) |rpscore: número flutuante que representa a pontuação de anomalias na alteração de aumento e diminuição no nível | |

### <a name="parameters"></a>parâmetros
Informações mais detalhadas sobre esses parâmetros de entrada estão listadas na tabela de saudação abaixo:

| Parâmetros de Entrada | Descrição | Configuração Padrão | Tipo | Intervalo Válido | Intervalo Sugerido |
| --- | --- | --- | --- | --- | --- |
| detectors.historyWindow |Histórico (no número de pontos de dados) usado para o cálculo da pontuação de anomalias |500 |inteiro |10-2.000 |Dependente da série temporal |
| detectors.spikesdips | Se apenas picos toodetect, somente dips ou ambos |Ambos |enumeração |Ambos, Picos, Quedas |Ambos |
| bileveldetector.sensitivity |Sensibilidade para o detector de alteração no nível bidirecional. |3.25 |double |Nenhum |3.25-5 (valores mais baixos significam mais sensibilidade) |
| trenddetector.sensitivity |Sensibilidade para o detector de tendência positiva. |3.25 |double |Nenhum |3.25-5 (valores mais baixos significam mais sensibilidade) |
| tspikedetector.sensitivity |Sensibilidade para o Detector TSpike |3 |inteiro |1-10 |3-5 (valores mais baixos significam mais sensibilidade) |
| zspikedetector.sensitivity |Sensibilidade para o Detector ZSpike |3 |inteiro |1-10 |3-5 (valores mais baixos significam mais sensibilidade) |
| postprocess.tailRows |Número de dados mais recentes Olá pontos toobe mantido nos resultados de saída Olá |0 |inteiro |0 (mantenha todos os pontos de dados), ou especifique o número de pontos tookeep nos resultados |N/D |

### <a name="output"></a>Saída
Olá API executa todos os detectores em seus dados de série temporal e retorna as pontuações de anomalias e indicadores de binário de pico para cada ponto no tempo. Olá tabela a seguir lista saídas de saudação API. 

| outputs | Descrição |
| --- | --- |
| Hora |Carimbos de data/hora dos dados brutos ou dos dados atribuídos (e/ou) agregados se a atribuição dos dados ausentes (e/ou) de agregação for aplicada |
| Dados |Valores dos dados brutos ou dos dados atribuídos (e/ou) agregados se a atribuição dos dados ausentes (e/ou) de agregação for aplicada |
| TSpike |Indicador binário tooindicate se um pico é detectado pelo Detector TSpike |
| ZSpike |Indicador binário tooindicate se um pico é detectado pelo Detector ZSpike |
| rpscore |Um número flutuante que representa a pontuação de anomalias na alteração bidirecional no nível |
| rpalert |valor de 1/0 indicando que há um nível bidirecional alterar anomalias com base na sensibilidade de entrada hello |
| tscore |um número flutuante que representa a pontuação de anomalias na tendência positiva |
| talert |valor de 1/0 indicando que há é uma anomalia de tendência positiva com base na sensibilidade de entrada hello |

## <a name="scorewithseasonality-api"></a>API ScoreWithSeasonality
Olá ScoreWithSeasonality API é usada para executar a detecção de anomalias na série temporal que têm padrões sazonais. Esta API é útil toodetect desvios padrões sazonais.  
Olá figura a seguir mostra um exemplo de anomalias detectado em uma série temporal sazonais. série de tempo de saudação tem um pico (Olá 1º ponto preto), dois dips (ponto de preto 2º hello e uma final Olá) e uma alteração do nível (ponto vermelho). Observe que ambos Olá dip no meio de saudação do MTS hello e alteração do nível de saudação só são discerníveis depois sazonais componentes são removidos da série de saudação.
![API de Sazonalidade][2]

### <a name="detectors"></a>Detectores
detectores de saudação no ponto de extremidade de periodicidade Olá são toohello semelhante no ponto de extremidade de periodicidade não hello, mas com nomes de parâmetro ligeiramente diferente (listados abaixo).

### <a name="parameters"></a>parâmetros

Informações mais detalhadas sobre esses parâmetros de entrada estão listadas na tabela de saudação abaixo:

| Parâmetros de Entrada | Descrição | Configuração Padrão | Tipo | Intervalo Válido | Intervalo Sugerido |
| --- | --- | --- | --- | --- | --- |
| preprocess.aggregationInterval |Intervalo de agregação em segundos para agregar a série temporal de entrada |0 (nenhuma agregação é realizada) |inteiro |0: ignorar a agregação, > 0 do contrário |dia de too1 de 5 minutos, dependente de série temporal |
| preprocess.aggregationFunc |Função usada para agregar dados em Olá especificado AggregationInterval |média |enumeração |média, soma, comprimento |N/D |
| preprocess.replaceMissing |Os valores usados tooimpute falta de dados |lkv (último valor conhecido) |enumeração |zero, lkv, média |N/D |
| detectors.historyWindow |Histórico (no número de pontos de dados) usado para o cálculo da pontuação de anomalias |500 |inteiro |10-2.000 |Dependente da série temporal |
| detectors.spikesdips | Se apenas picos toodetect, somente dips ou ambos |Ambos |enumeração |Ambos, Picos, Quedas |Ambos |
| bileveldetector.sensitivity |Sensibilidade para o detector de alteração no nível bidirecional. |3.25 |double |Nenhum |3.25-5 (valores mais baixos significam mais sensibilidade) |
| postrenddetector.sensitivity |Sensibilidade para o detector de tendência positiva. |3.25 |double |Nenhum |3.25-5 (valores mais baixos significam mais sensibilidade) |
| negtrenddetector.sensitivity |Sensibilidade para o detector de tendência negativa. |3.25 |double |Nenhum |3.25-5 (valores mais baixos significam mais sensibilidade) |
| tspikedetector.sensitivity |Sensibilidade para o Detector TSpike |3 |inteiro |1-10 |3-5 (valores mais baixos significam mais sensibilidade) |
| zspikedetector.sensitivity |Sensibilidade para o Detector ZSpike |3 |inteiro |1-10 |3-5 (valores mais baixos significam mais sensibilidade) |
| seasonality.enable |Se a análise de periodicidade é toobe executada |verdadeiro |Booliano |verdadeiro, falso |Dependente da série temporal |
| seasonality.numSeasonality |Número máximo de ciclos periódicos toobe detectado |1 |inteiro |1, 2 |1-2 |
| seasonality.transform |Caso os componentes sazonais (e) de tendência devam ser removidos antes de aplicar a detecção de anomalias |sem sazonalidade |enumeração |nenhum, sem sazonalidade, sem sazonalidade e tendência |N/D |
| postprocess.tailRows |Número de dados mais recentes Olá pontos toobe mantido nos resultados de saída Olá |0 |inteiro |0 (mantenha todos os pontos de dados), ou especifique o número de pontos tookeep nos resultados |N/D |

### <a name="output"></a>Saída
Olá API executa todos os detectores em seus dados de série temporal e retorna as pontuações de anomalias e indicadores de binário de pico para cada ponto no tempo. Olá tabela a seguir lista saídas de saudação API. 

| outputs | Descrição |
| --- | --- |
| Hora |Carimbos de data/hora dos dados brutos ou dos dados atribuídos (e/ou) agregados se a atribuição dos dados ausentes (e/ou) de agregação for aplicada |
| OriginalData |Valores dos dados brutos ou dos dados atribuídos (e/ou) agregados se a atribuição dos dados ausentes (e/ou) de agregação for aplicada |
| ProcessedData |Um dos seguintes hello: <ul><li>Série temporal ajustada periodicamente caso uma sazonalidade significativa tenha sido detectada e opção sem sazonalidade foi selecionada;</li><li>séries temporais e sem tendência e ajustadas periodicamente caso uma sazonalidade significativa tenha sido detectada e a opção sem sazonalidade e tendência foi selecionada</li><li>Caso contrário, isso é Olá igual a OriginalData</li> |
| TSpike |Indicador binário tooindicate se um pico é detectado pelo Detector TSpike |
| ZSpike |Indicador binário tooindicate se um pico é detectado pelo Detector ZSpike |
| BiLevelChangeScore |Um número flutuante que representa a pontuação de anomalias na alteração de nível |
| BiLevelChangeAlert |1/0 valor que indica há é uma anomalia de alteração do nível com base na sensibilidade de entrada hello |
| PosTrendScore |um número flutuante que representa a pontuação de anomalias na tendência positiva |
| PosTrendAlert |valor de 1/0 indicando que há é uma anomalia de tendência positiva com base na sensibilidade de entrada hello |
| NegTrendScore |Um número flutuante que representa a pontuação de anomalias na tendência negativa |
| NegTrendAlert |valor de 1/0 indicando que há é uma anomalia de tendência negativa com base na sensibilidade de entrada hello |

[1]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-score.png
[2]: ./media/machine-learning-apps-anomaly-detection-api/anomaly-detection-seasonal.png

