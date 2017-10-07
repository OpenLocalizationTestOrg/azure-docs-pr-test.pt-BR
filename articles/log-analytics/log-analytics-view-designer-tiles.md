---
title: "referência de aaaTile do Designer de exibição na análise de logs do OMS | Microsoft Docs"
description: "Designer de exibição na análise de Log permite que você toocreate personalizado modos de exibição no console do OMS Olá que contêm diferentes visualizações de dados no repositório do OMS hello. Este artigo fornece uma referência de configurações de saudação para cada um dos blocos de saudação toouse disponíveis em exibições personalizadas."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 41787c8f-6c13-4520-b0d3-5d3d84fcf142
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 4706abb16b8a3719f5dbe8c89cd61739391ab8f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-tile-reference"></a>Referência sobre blocos do Criador de Modos de Exibição do Log Analytics
Olá Designer de exibição de análise de Log permite que você toocreate personalizado modos de exibição no console do OMS Olá que contêm diferentes visualizações de dados no repositório do OMS hello. Este artigo fornece uma referência de configurações de saudação para cada um dos blocos de saudação toouse disponíveis em exibições personalizadas.

Outros artigos disponíveis para o Designer de modo de exibição:

* [Exibir Designer](log-analytics-view-designer.md) -visão geral da saudação Designer de exibição e procedimentos para criar e editar modos de exibição personalizados.
* [Referência de parte da visualização](log-analytics-view-designer-parts.md) -referência de configurações de saudação de cada Olá blocos toouse disponível em exibições personalizadas.

>[!NOTE]
> Se o seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), consultas em todos os modos de exibição devem ser gravada em Olá [nova linguagem de consulta](https://go.microsoft.com/fwlink/?linkid=856078).  Todas as exibições que foram criadas antes de atualizar o espaço de trabalho de saudação será automtically convertido.

Olá, tabela a seguir lista tipos diferentes de saudação de blocos disponíveis no hello Designer de exibição.  Olá seções a seguir descrevem cada tipo de bloco em detalhes e suas propriedades.

| Bloco | Descrição |
|:--- |:--- |
| [Número](#number-tile) |Número único mostrando a contagem de registros de uma consulta. |
| [Dois números](#two-numbers-tile) |Dois números únicos mostrando contagens de registros de duas consultas diferentes. |
| [Rosca](#donut-tile) |Gráfico de rosca com base em uma consulta com um valor resumido na Central de saudação. |
| [Gráfico de linhas e balão](#line-chart-amp-callout-tile) |Gráfico de linhas com base em uma consulta e um balão com um valor de resumo. |
| [Gráfico de linhas](#line-chart-tile) |Gráfico de linhas com base em uma consulta. |
| [Duas linhas do tempo](#two-timelines-tile) |Gráfico de colunas com duas séries, cada uma com base em uma consulta separada. |

## <a name="number-tile"></a>Bloco Número
Olá **número** lado a lado exibe um único número mostrando a contagem de saudação de registros de uma consulta de log e um rótulo.

![Bloco Número](media/log-analytics-view-designer/tile-number.png)

| Configuração | Descrição |
|:--- |:--- |
| Nome |Toodisplay de texto na parte superior de saudação do hello lado a lado. |
| Descrição |Texto toodisplay em nome do bloco hello. |
| **Bloco** | |
| Legenda |Toodisplay de texto em valor hello. |
| Consultar |Toorun de consulta.  Contagem de saudação do número de saudação de registros retornados pela consulta hello será exibida. |
| **Avançado** |**> Verificação do fluxo de dados** |
| habilitado |Selecione se a verificação do fluxo de dados deve ser habilitada para o bloco de saudação.  Isso fornece uma mensagem alternativa se os dados não estão disponíveis para o bloco de saudação.  Isso está geralmente usado tooprovide uma mensagem período Olá temporária quando exibir hello está instalado e os dados vêm disponíveis. |
| Consultar |Consulta toorun toocheck se os dados estão disponíveis para exibição de saudação.  Se a consulta de saudação não retorna nenhum resultado, será exibida uma mensagem em vez do valor de saudação da consulta principal hello. |
| Mensagem |Mensagem toodisplay se a consulta de verificação do fluxo de dados de saudação não retorna nenhum dado.  Se você não fornecer nenhuma mensagem, a mensagem *Executando Avaliação* será exibida. |


## <a name="two-numbers-tile"></a>Bloco Dois Números
Olá **número dois** lado a lado exibe dois números mostrando a contagem de saudação registros das duas consultas de log diferente e um rótulo para cada um.

![Bloco Dois Números](media/log-analytics-view-designer/tile-two-numbers.png)

| Configuração | Descrição |
|:--- |:--- |
| Nome |Toodisplay de texto na parte superior de saudação do hello lado a lado. |
| Descrição |Texto toodisplay em nome do bloco hello. |
| **Primeiro Bloco** | |
| Legenda |Toodisplay de texto em valor hello. |
| Consultar |Toorun de consulta.  Contagem de saudação do número de saudação de registros retornados pela consulta hello será exibida. |
| **Segundo Bloco** | |
| Legenda |Toodisplay de texto em valor hello. |
| Consultar |Toorun de consulta.  Contagem de saudação do número de saudação de registros retornados pela consulta hello será exibida. |
| **Avançado** |**> Verificação do fluxo de dados** |
| habilitado |Selecione se a verificação do fluxo de dados deve ser habilitada para o bloco de saudação.  Isso fornece uma mensagem alternativa se os dados não estão disponíveis para o bloco de saudação.  Isso está geralmente usado tooprovide uma mensagem período Olá temporária quando exibir hello está instalado e os dados vêm disponíveis. |
| Consultar |Consulta toorun toocheck se os dados estão disponíveis para exibição de saudação.  Se a consulta de saudação não retorna nenhum resultado, será exibida uma mensagem em vez do valor de saudação da consulta principal hello. |
| Mensagem |Mensagem toodisplay se a consulta de verificação do fluxo de dados de saudação não retorna nenhum dado.  Se você não fornecer nenhuma mensagem, a mensagem *Executando Avaliação* será exibida. |


## <a name="donut-tile"></a>Bloco Rosca
Olá **rosca** lado a lado exibe um único número resumido de uma coluna de valor em uma consulta de log.  rosca Olá exibe graficamente os resultados de registros de três principais hello.

![Bloco Rosca](media/log-analytics-view-designer/tile-donut.png)

| Configuração | Descrição |
|:--- |:--- |
| Nome |Toodisplay de texto na parte superior de saudação do hello lado a lado. |
| Descrição |Texto toodisplay em nome do bloco hello. |
| **Rosca** | |
| Consultar |Consulta toorun para rosca hello.  propriedade primeiro Olá deve ser um valor e hello segunda propriedade text um valor numérico.  Isso é normalmente uma consulta que usa Olá **medidas** resultados toosummarize de palavra-chave. |
| **Rosca** |**> Centro** |
| Texto |Toodisplay de texto em valor hello dentro Olá rosca. |
| Operação |Olá tooperform operação em Olá propriedade toosummarize tooa único valor.<br><br>-Soma: Adicione valores de saudação de todos os registros com o valor da propriedade hello.<br>-Percentual: A porcentagem de valores hello somado de registros com hello propriedade valor comparado toohello somado valores de todos os registros. |
| Valores de resultado usados na operação do centro |Opcionalmente, clique em Olá tooadd de sinal de mais um ou mais valores.  resultados de saudação de consulta hello serão toorecords limitado com valores de propriedade Olá que você especificar.  Se nenhum valor for adicionado, que todos os registros são incluídos na consulta de saudação. |
| **Rosca** |**> Opções adicionais** |
| Cores |Olá toodisplay de cor para cada uma das três propriedades principais de saudação.  Se você quiser cores alternativas toospecify para valores de propriedade específicos, use avançadas de mapeamento de cores. |
| Mapeamento de Cores Avançado |Exibe uma cor para valores de propriedade específicos.  Se valor Olá especificado está em Olá três principais, cor alternativa Olá é exibido em vez de cores padrão hello.  Se Olá propriedade não está no hello três principais, cor da saudação não é exibida. |
| **Avançado** |**> Verificação do fluxo de dados** |
| habilitado |Selecione se a verificação do fluxo de dados deve ser habilitada para o bloco de saudação.  Isso fornece uma mensagem alternativa se os dados não estão disponíveis para o bloco de saudação.  Isso está geralmente usado tooprovide uma mensagem período Olá temporária quando exibir hello está instalado e os dados vêm disponíveis. |
| Consultar |Consulta toorun toocheck se os dados estão disponíveis para exibição de saudação.  Se a consulta de saudação não retorna nenhum resultado, será exibida uma mensagem em vez do valor de saudação da consulta principal hello. |
| Mensagem |Mensagem toodisplay se a consulta de verificação do fluxo de dados de saudação não retorna nenhum dado.  Se você não fornecer nenhuma mensagem, a mensagem *Executando Avaliação* será exibida. |


## <a name="line-chart-tile"></a>Bloco Gráfico de linhas
Olá **gráfico de linhas** lado a lado exibe um gráfico de linha com várias séries de uma consulta de log ao longo do tempo.  

![Bloco Gráfico de Linhas e Balão](media/log-analytics-view-designer/tile-line-chart.png)

| Configuração | Descrição |
|:--- |:--- |
| Nome |Toodisplay de texto na parte superior de saudação do hello lado a lado. |
| Descrição |Texto toodisplay em nome do bloco hello. |
| **Gráfico de Linhas** | |
| Consultar |Toorun de consulta para o gráfico de linha de saudação.  propriedade primeiro Olá deve ser um valor e hello segunda propriedade text um valor numérico.  Isso é normalmente uma consulta que usa Olá **medidas** resultados toosummarize de palavra-chave.  Se a consulta Olá usa Olá **intervalo** palavra-chave e Olá eixo x do gráfico de saudação usará esse intervalo de tempo.  Se a consulta Olá não incluir Olá **intervalo** intervalos de palavra-chave e por hora são usados para Olá eixo x. |
| **Gráfico de Linhas** |**> Eixo Y** |
| Usar Escala Logarítmica |Selecione toouse uma escala logarítmica de saudação eixo y. |
| Unidades |Especifique unidades Olá Olá valores retornados pela consulta hello.  Essas informações são rótulos toodisplay usadas no gráfico de saudação que indica os tipos de valor hello e, opcionalmente, para converter valores hello.  Olá **tipo de unidade** Especifica a categoria de saudação da unidade de saudação e define Olá **tipo de unidade atual** valores que estão disponíveis.  Se você selecionar um valor em **converter** valores numéricos Olá são convertidos de saudação **unidade atual** digite toohello **converter** tipo. |
| Rótulo Personalizado |Texto toodisplay Olá eixo Y próxima toohello rótulo para o tipo de unidade de saudação.  Se nenhum nome for especificado, somente o tipo de unidade de saudação é exibido. |
| **Avançado** |**> Verificação do fluxo de dados** |
| habilitado |Selecione se a verificação do fluxo de dados deve ser habilitada para o bloco de saudação.  Isso fornece uma mensagem alternativa se os dados não estão disponíveis para o bloco de saudação.  Isso está geralmente usado tooprovide uma mensagem período Olá temporária quando exibir hello está instalado e os dados vêm disponíveis. |
| Consultar |Consulta toorun toocheck se os dados estão disponíveis para exibição de saudação.  Se a consulta de saudação não retorna nenhum resultado, será exibida uma mensagem em vez do valor de saudação da consulta principal hello. |
| Mensagem |Mensagem toodisplay se a consulta de verificação do fluxo de dados de saudação não retorna nenhum dado.  Se você não fornecer nenhuma mensagem, a mensagem *Executando Avaliação* será exibida. |


## <a name="line-chart--callout-tile"></a>Bloco Gráfico de linhas e balão
Olá **texto explicativo & gráfico de linha** lado a lado exibe um gráfico de linha com várias séries de uma consulta de log com o tempo e um texto explicativo com um valor resumido.  

![Bloco Gráfico de Linhas e Balão](media/log-analytics-view-designer/tile-line-chart-callout.png)

| Configuração | Descrição |
|:--- |:--- |
| Nome |Toodisplay de texto na parte superior de saudação do hello lado a lado. |
| Descrição |Texto toodisplay em nome do bloco hello. |
| **Gráfico de Linhas** | |
| Consultar |Toorun de consulta para o gráfico de linha de saudação.  propriedade primeiro Olá deve ser um valor e hello segunda propriedade text um valor numérico.  Isso é normalmente uma consulta que usa Olá **medidas** resultados toosummarize de palavra-chave.  Se a consulta Olá usa Olá **intervalo** palavra-chave e Olá eixo x do gráfico de saudação usará esse intervalo de tempo.  Se a consulta Olá não incluir Olá **intervalo** intervalos de palavra-chave e por hora são usados para Olá eixo x. |
| **Gráfico de Linhas** |**> Balão** |
| Balão |Toodisplay de texto do título acima do valor de texto explicativo hello. |
| Nome da Série |Valor da propriedade de saudação série toouse para o valor de texto explicativo hello.  Se nenhuma série for fornecido, todos os registros da consulta hello são usados. |
| Operação |Olá tooperform operação Olá valor toosummarize tooa único valor da propriedade de texto explicativo de saudação.<br>-Média: Média do valor de saudação de todos os registros.<br><br>-Contagem: Contagem de todos os registros retornados pela consulta hello.<br>-Último exemplo: O valor do último intervalo de saudação incluído no gráfico de saudação.<br>-Max: O valor de máximo de intervalos de saudação incluídos no gráfico de saudação.<br>-Mín: O valor de mínimo de intervalos de saudação incluídos no gráfico de saudação.<br>-Soma: A soma do valor de saudação de todos os registros. |
| **Gráfico de Linhas** |**> Eixo Y** |
| Usar Escala Logarítmica |Selecione toouse uma escala logarítmica de saudação eixo y. |
| Unidades |Especifique unidades Olá Olá valores retornados pela consulta hello.  Essas informações são rótulos toodisplay usadas no gráfico de saudação que indica os tipos de valor hello e, opcionalmente, para converter valores hello.  Olá **tipo de unidade** Especifica a categoria de saudação da unidade de saudação e define Olá **tipo de unidade atual** valores que estão disponíveis.  Se você selecionar um valor em **converter** valores numéricos Olá são convertidos de saudação **unidade atual** digite toohello **converter** tipo. |
| Rótulo Personalizado |Texto toodisplay Olá eixo Y próxima toohello rótulo para o tipo de unidade de saudação.  Se nenhum nome for especificado, somente o tipo de unidade de saudação é exibido. |
| **Avançado** |**> Verificação do fluxo de dados** |
| habilitado |Selecione se a verificação do fluxo de dados deve ser habilitada para o bloco de saudação.  Isso fornece uma mensagem alternativa se os dados não estão disponíveis para o bloco de saudação.  Isso está geralmente usado tooprovide uma mensagem período Olá temporária quando exibir hello está instalado e os dados vêm disponíveis. |
| Consultar |Consulta toorun toocheck se os dados estão disponíveis para exibição de saudação.  Se a consulta de saudação não retorna nenhum resultado, será exibida uma mensagem em vez do valor de saudação da consulta principal hello. |
| Mensagem |Mensagem toodisplay se a consulta de verificação do fluxo de dados de saudação não retorna nenhum dado.  Se você não fornecer nenhuma mensagem, a mensagem *Executando Avaliação* será exibida. |


## <a name="two-timelines-tile"></a>Bloco Duas linhas do tempo
Olá **dois cronogramas** lado a lado exibe os resultados de saudação de duas consultas de log ao longo do tempo, como gráficos de colunas.  Um balão é exibido para cada série.  

![Bloco Duas linhas do tempo](media/log-analytics-view-designer/tile-two-timelines.png)

| Configuração | Descrição |
|:--- |:--- |
| Nome |Toodisplay de texto na parte superior de saudação do hello lado a lado. |
| Descrição |Texto toodisplay em nome do bloco hello. |
| Primeiro Gráfico | |
| Legenda |Toodisplay de texto em texto explicativo de saudação primeira série de saudação. |
| Cor |Cor toouse para colunas de saudação na primeira série do hello. |
| Consulta de Gráfico |Consulta toorun primeira série de saudação.  Contagem de saudação do número de saudação de registros em cada intervalo de tempo será representada por colunas de saudação do gráfico. |
| Operação |Olá tooperform operação Olá valor toosummarize tooa único valor da propriedade de texto explicativo de saudação.<br><br>-Média: Média do valor de saudação de todos os registros.<br>-Contagem: Contagem de todos os registros retornados pela consulta hello.<br>-Último exemplo: O valor do último intervalo de saudação incluído no gráfico de saudação.<br>-Max: O valor de máximo de intervalos de saudação incluídos no gráfico de saudação. |
| **Segundo Gráfico** | |
| Legenda |Toodisplay de texto em texto explicativo de saudação para a segunda série de saudação. |
| Cor |Cor toouse para colunas de saudação na segunda série de saudação. |
| Consulta de Gráfico |Toorun de consulta para a segunda série de saudação.  Contagem de saudação do número de saudação de registros em cada intervalo de tempo será representada por colunas de saudação do gráfico. |
| Operação |Olá tooperform operação Olá valor toosummarize tooa único valor da propriedade de texto explicativo de saudação.<br><br>-Média: Média do valor de saudação de todos os registros.<br>-Contagem: Contagem de todos os registros retornados pela consulta hello.<br>-Último exemplo: O valor do último intervalo de saudação incluído no gráfico de saudação.<br>-Max: O valor de máximo de intervalos de saudação incluídos no gráfico de saudação. |
| **Avançado** |**> Verificação do fluxo de dados** |
| habilitado |Selecione se a verificação do fluxo de dados deve ser habilitada para o bloco de saudação.  Isso fornece uma mensagem alternativa se os dados não estão disponíveis para o bloco de saudação.  Isso está geralmente usado tooprovide uma mensagem período Olá temporária quando exibir hello está instalado e os dados vêm disponíveis. |
| Consultar |Consulta toorun toocheck se os dados estão disponíveis para exibição de saudação.  Se a consulta de saudação não retorna nenhum resultado, será exibida uma mensagem em vez do valor de saudação da consulta principal hello. |
| Mensagem |Mensagem toodisplay se a consulta de verificação do fluxo de dados de saudação não retorna nenhum dado.  Se você não fornecer nenhuma mensagem, a mensagem *Executando Avaliação* será exibida. |


## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) toosupport consultas Olá lado a lado.
* Adicionar [visualização partes](log-analytics-view-designer-parts.md) tooyour modo de exibição personalizado.
