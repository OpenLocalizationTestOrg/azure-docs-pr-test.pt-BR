---
title: "referência de aaaPart do Designer de exibição na análise de logs do OMS | Microsoft Docs"
description: "Designer de exibição na análise de Log permite que você toocreate personalizado modos de exibição no console do OMS Olá que contêm diferentes visualizações de dados no repositório do OMS hello. Este artigo fornece uma referência de configurações de saudação para cada uma das partes de visualização de saudação disponível toouse em exibições personalizadas."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: 5718d620-b96e-4d33-8616-e127ee9379c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 6a19a451cf4cefd2fa5c94e6f61d812c4f820f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-view-designer-visualization-part-reference"></a>Referência da parte de visualização do Designer de modos de exibição do Log Analytics
Olá Designer de exibição de análise de Log permite que você toocreate modos de exibição personalizados no console do OMS Olá que contêm diferentes visualizações de dados de repositório do OMS hello. Este artigo fornece uma referência de configurações de saudação para cada uma das partes de visualização de saudação disponível toouse em exibições personalizadas.

Outros artigos disponíveis para o Designer de modo de exibição:

* [Exibir Designer](log-analytics-view-designer.md) -visão geral da saudação Designer de exibição e procedimentos para criar e editar modos de exibição personalizados.
* [Referência de bloco](log-analytics-view-designer-tiles.md) -referência de configurações de saudação de cada Olá blocos toouse disponível em exibições personalizadas.

>[!NOTE]
> Se o seu espaço de trabalho tiver sido atualizado toohello [linguagem de consulta de análise de Log novo](log-analytics-log-search-upgrade.md), consultas em todos os modos de exibição devem ser gravada em Olá [nova linguagem de consulta](https://go.microsoft.com/fwlink/?linkid=856078).  Todas as exibições que foram criadas antes de atualizar o espaço de trabalho de saudação será automtically convertido.

Olá, tabela a seguir descreve Olá diferentes tipos de blocos disponíveis no hello Designer de exibição.  Olá seções a seguir descrevem cada tipo de bloco em detalhes e suas propriedades.

| Tipo de exibição | Descrição |
|:--- |:--- |
| [Lista de consultas](#list-of-queries-part) |Exibe uma lista de consultas de pesquisa de log.  usuário Olá pode clicar em cada consulta toodisplay seus resultados. |
| [Número e lista](#number-amp-list-part) |O cabeçalho tem um número único mostrando a contagem de registros de uma consulta de pesquisa de log.  Lista exibe o saudação dez primeiros resultados de uma consulta com um gráfico que indica o valor relativo de saudação de uma coluna numérica ou as alterações ao longo do tempo. |
| [Dois números e lista](#two-numbers-amp-list-part) |O cabeçalho tem dois números mostrando a contagem de registros de consultas de pesquisa de log separadas.  Lista exibe o saudação dez primeiros resultados de uma consulta com um gráfico que indica o valor relativo de saudação de uma coluna numérica ou as alterações ao longo do tempo. |
| [Rosca e lista](#donut-amp-list-part) |O cabeçalho exibe um único número resumido de uma coluna de valor em uma consulta de log.  rosca Olá exibe graficamente os resultados de registros de três principais hello. |
| [Duas linhas do tempo e lista](#two-timelines-amp-list-part) |Cabeçalho exibe Olá resultados de consultas de dois de log ao longo do tempo, como gráficos de coluna com um texto explicativo exibindo um único número resumidos de uma coluna de valor em uma consulta de log.  Lista exibe o saudação dez primeiros resultados de uma consulta com um gráfico que indica o valor relativo de saudação de uma coluna numérica ou as alterações ao longo do tempo. |
| [Informações](#information-part) |O cabeçalho exibe texto estático e um link opcional.  A lista exibe um ou mais itens com texto estático e o título. |
| [Gráfico de linhas, balão e lista](#line-chart-callout-amp-list-part) |O cabeçalho exibe um gráfico de linhas com várias séries de uma consulta de log ao longo do tempo, além de um balão com um valor resumido.  Lista exibe o saudação dez primeiros resultados de uma consulta com um gráfico que indica o valor relativo de saudação de uma coluna numérica ou as alterações ao longo do tempo. |
| [Gráfico de linhas e lista](#line-chart-amp-list-part) |O cabeçalho exibe um gráfico de linhas com várias séries de uma consulta de log ao longo do tempo.  Lista exibe o saudação dez primeiros resultados de uma consulta com um gráfico que indica o valor relativo de saudação de uma coluna numérica ou as alterações ao longo do tempo. |
| [Pilha de parte de gráficos de linha](#stack-of-line-charts-part) |Exibe três gráficos de linhas separados com várias séries de uma consulta de log ao longo do tempo. |

## <a name="list-of-queries-part"></a>Lista da parte de consultas
Exibe uma lista de consultas de pesquisa de log.  usuário Olá pode clicar em cada consulta toodisplay seus resultados.  exibição de saudação incluirá uma única consulta por padrão, e você pode clicar em **+ consulta** consultas adicionais tooadd.

![Lista da exibição de consultas](media/log-analytics-view-designer/view-list-queries.png)

| Configuração | Descrição |
|:--- |:--- |
| **Geral** | |
| Title |Toodisplay de texto na parte superior de saudação do modo de exibição de saudação. |
| Novo Grupo |Selecione toocreate um novo grupo na exibição de saudação iniciar no modo de exibição atual hello. |
| Filtros pré-selecionados |Lista delimitada por vírgulas de tooinclude propriedades no painel de filtro à esquerda do hello quando o usuário Olá seleciona uma consulta. |
| Modo de renderização |Exibição inicial exibida quando a consulta hello está selecionada.  usuário Olá pode selecionar qualquer modos de exibição disponíveis após a abertura de consulta de saudação. |
| **Consultas** | |
| Consulta de pesquisa |Toorun de consulta. |
| Nome amigável |Nome de usuário do hello consulta toodisplay toohello. |

## <a name="number--list-part"></a>Parte de número e lista
O cabeçalho tem um número único mostrando a contagem de registros de uma consulta de pesquisa de log.  Lista exibe o saudação dez primeiros resultados de uma consulta com um gráfico que indica o valor relativo de saudação de uma coluna numérica ou as alterações ao longo do tempo.

![Lista da exibição de consultas](media/log-analytics-view-designer/view-number-list.png)

| Configuração | Descrição |
|:--- |:--- |
| **Geral** | |
| Título do Grupo |Toodisplay de texto na parte superior de saudação do modo de exibição de saudação. |
| Novo Grupo |Selecione toocreate um novo grupo na exibição de saudação iniciar no modo de exibição atual hello. |
| ícone |Arquivo toodisplay próximo toohello resultado no cabeçalho de saudação da imagem. |
| Usar Ícone |Selecione a exibição do ícone Olá toohave. |
| **Título** | |
| Legenda |Toodisplay de texto na parte superior de saudação do cabeçalho de saudação. |
| Consultar |Consulta toorun para cabeçalho hello.  Contagem de saudação do número de saudação de registros retornados pela consulta hello será exibida. |
| **Lista** | |
| Consultar |Toorun de consulta para a lista de saudação.  Olá primeiro duas propriedades para hello dez primeiros registros nos resultados de hello serão exibidos.  propriedade primeiro Olá deve ser um valor e hello segunda propriedade text um valor numérico.  As barras são criadas automaticamente com base no valor relativo de saudação de coluna numérica hello.<br><br>Use o comando de classificação de saudação no hello consultar toosort Olá os registros na lista de saudação.  saudação de usuário pode clicar consulte Olá de todos os toorun de consulta e retornar todos os registros. |
| Ocultar gráfico |Selecione toodisable Olá gráfico toohello direito de coluna numérica hello. |
| Habilitar minigráficos |Selecione o Minigráfico toodisplay em vez de barra horizontal.  Consulte [Configurações Comuns](#sparklines) para obter detalhes. |
| Cor |Cor das barras de saudação ou Minigráficos. |
| Separador de Valor e Nome |Delimitador de caractere, se você quiser que a propriedade de texto de saudação tooparse em vários valores.  Consulte [Configurações Comuns](#name-value-separator) para obter detalhes. |
| Consulta de navegação |Consultar toorun ao usuário Olá seleciona um item na lista de saudação.  Consulte [Configurações Comuns](#navigation-query) para obter detalhes. |
| **Lista** |**> Títulos de coluna** |
| Nome |Toodisplay de texto na parte superior de saudação da primeira coluna Olá da lista de saudação. |
| Valor |Toodisplay de texto na parte superior de saudação da segunda coluna Olá da lista de saudação. |
| **Lista** |**> Limites** |
| Habilitar limites |Selecione limites tooenable.  Consulte [Configurações Comuns](#thresholds) para obter detalhes. |

## <a name="two-numbers--list-part"></a>Parte de dois números e lista
O cabeçalho tem dois números mostrando a contagem de registros de consultas de pesquisa de log separadas.  Lista exibe o saudação dez primeiros resultados de uma consulta com um gráfico que indica o valor relativo de saudação de uma coluna numérica ou as alterações ao longo do tempo.

![Exibição de dois números e lista](media/log-analytics-view-designer/view-two-numbers-list.png)

| Configuração | Descrição |
|:--- |:--- |
| **Geral** | |
| Título do Grupo |Toodisplay de texto na parte superior de saudação do modo de exibição de saudação. |
| Novo Grupo |Selecione toocreate um novo grupo na exibição de saudação iniciar no modo de exibição atual hello. |
| ícone |Arquivo toodisplay próximo toohello resultado no cabeçalho de saudação da imagem. |
| Usar Ícone |Selecione a exibição do ícone Olá toohave. |
| **Título** | |
| Legenda |Toodisplay de texto na parte superior de saudação do cabeçalho de saudação. |
| Consultar |Consulta toorun para cabeçalho hello.  Contagem de saudação do número de saudação de registros retornados pela consulta hello será exibida. |
| **Lista** | |
| Consultar |Toorun de consulta para a lista de saudação.  Olá primeiro duas propriedades para hello dez primeiros registros nos resultados de hello serão exibidos.  propriedade primeiro Olá deve ser um valor e hello segunda propriedade text um valor numérico.  As barras são criadas automaticamente com base no valor relativo de saudação de coluna numérica hello.<br><br>Use o comando de classificação de saudação no hello consultar toosort Olá os registros na lista de saudação.  saudação de usuário pode clicar consulte Olá de todos os toorun de consulta e retornar todos os registros. |
| Ocultar gráfico |Selecione toodisable Olá gráfico toohello direito de coluna numérica hello. |
| Habilitar minigráficos |Selecione o Minigráfico toodisplay em vez de barra horizontal.  Consulte [Configurações Comuns](#sparklines) para obter detalhes. |
| Cor |Cor das barras de saudação ou Minigráficos. |
| Operação |Operação tooperform para Olá Minigráfico.  Consulte [Configurações Comuns](#sparklines) para obter detalhes. |
| Separador de Valor e Nome |Delimitador de caractere, se você quiser que a propriedade de texto de saudação tooparse em vários valores.  Consulte [Configurações Comuns](#name-value-separator) para obter detalhes. |
| Consulta de navegação |Consultar toorun ao usuário Olá seleciona um item na lista de saudação.  Consulte [Configurações Comuns](#navigation-query) para obter detalhes. |
| **Lista** |**> Títulos de coluna** |
| Nome |Toodisplay de texto na parte superior de saudação da primeira coluna Olá da lista de saudação. |
| Valor |Toodisplay de texto na parte superior de saudação da segunda coluna Olá da lista de saudação. |
| **Lista** |**> Limites** |
| Habilitar limites |Selecione limites tooenable.  Consulte [Configurações Comuns](#thresholds) para obter detalhes. |

## <a name="donut--list-part"></a>Parte de rosca e lista
O cabeçalho exibe um único número resumido de uma coluna de valor em uma consulta de log.  rosca Olá exibe graficamente os resultados de registros de três principais hello.

![Exibição de rosca e lista](media/log-analytics-view-designer/view-donut-list.png)

| Configuração | Descrição |
|:--- |:--- |
| **Geral** | |
| Título do Grupo |Toodisplay de texto na parte superior de saudação do hello lado a lado. |
| Novo Grupo |Selecione toocreate um novo grupo na exibição de saudação iniciar no modo de exibição atual hello. |
| ícone |Arquivo toodisplay próximo toohello resultado no cabeçalho de saudação da imagem. |
| Usar Ícone |Selecione a exibição do ícone Olá toohave. |
| **Cabeçalho** | |
| Title |Toodisplay de texto na parte superior de saudação do cabeçalho de saudação. |
| Subtítulo |Texto toodisplay em Olá título na parte superior de saudação do cabeçalho de saudação. |
| **Rosca** | |
| Consultar |Consulta toorun para rosca hello.  propriedade primeiro Olá deve ser um valor e hello segunda propriedade text um valor numérico. |
| **Rosca** |**> Centro** |
| Texto |Toodisplay de texto em valor hello dentro Olá rosca. |
| Operação |Olá tooperform operação em Olá propriedade toosummarize tooa único valor.<br><br>-Soma: Adicione valores de saudação de todos os registros.<br>-Percentual: Porcentagem Olá registros retornados pelos valores de saudação do **resultar valores usados na operação do Centro** toohello total de registros na consulta de saudação. |
| Valores de resultado usados na operação do centro |Opcionalmente, clique em Olá tooadd de sinal de mais um ou mais valores.  resultados de saudação de consulta hello serão toorecords limitado com valores de propriedade Olá que você especificar.  Se nenhum valor for adicionado, todos os registros são incluídos na consulta de saudação. |
| **Opções adicionais** |**> Cores** |
| Cor 1<br>Cor 2<br>Cor 3 |Selecione cor Olá Olá Olá valores exibidos na rosca Olá. |
| **Opções adicionais** |**> Mapeamento de Cores Avançado** |
| Valor do campo |Nome de saudação do tipo de um campo toodisplay-lo como uma cor diferente se ele está incluído no rosca hello. |
| Cor |Selecione a cor de saudação para campo exclusivo hello. |
| **Lista** | |
| Consultar |Toorun de consulta para a lista de saudação.  Contagem de saudação do número de saudação de registros retornados pela consulta hello será exibida. |
| Ocultar gráfico |Selecione toodisable Olá gráfico toohello direito de coluna numérica hello. |
| Habilitar minigráficos |Selecione o Minigráfico toodisplay em vez de barra horizontal.  Consulte [Configurações Comuns](#sparklines) para obter detalhes. |
| Cor |Cor das barras de saudação ou Minigráficos. |
| Operação |Operação tooperform para Olá Minigráfico.  Consulte [Configurações Comuns](#sparklines) para obter detalhes. |
| Separador de Valor e Nome |Delimitador de caractere, se você quiser que a propriedade de texto de saudação tooparse em vários valores.  Consulte [Configurações Comuns](#name-value-separator) para obter detalhes. |
| Consulta de navegação |Consultar toorun ao usuário Olá seleciona um item na lista de saudação.  Consulte [Configurações Comuns](#navigation-query) para obter detalhes. |
| **Lista** |**> Títulos de coluna** |
| Nome |Toodisplay de texto na parte superior de saudação da primeira coluna Olá da lista de saudação. |
| Valor |Toodisplay de texto na parte superior de saudação da segunda coluna Olá da lista de saudação. |
| **Lista** |**> Limites** |
| Habilitar limites |Selecione limites tooenable.  Consulte [Configurações Comuns](#thresholds) para obter detalhes. |

## <a name="two-timelines--list-part"></a>Parte de duas linhas do tempo e lista
Cabeçalho exibe Olá resultados de consultas de dois de log ao longo do tempo, como gráficos de coluna com um texto explicativo exibindo um único número resumidos de uma coluna de valor em uma consulta de log.  Lista exibe o saudação dez primeiros resultados de uma consulta com um gráfico que indica o valor relativo de saudação de uma coluna numérica ou as alterações ao longo do tempo.

![Exibição de duas linhas do tempo e lista](media/log-analytics-view-designer/view-two-timelines-list.png)

| Configuração | Descrição |
|:--- |:--- |
| **Geral** | |
| Título do Grupo |Toodisplay de texto na parte superior de saudação do hello lado a lado. |
| Novo Grupo |Selecione toocreate um novo grupo na exibição de saudação iniciar no modo de exibição atual hello. |
| ícone |Arquivo toodisplay próximo toohello resultado no cabeçalho de saudação da imagem. |
| Usar Ícone |Selecione a exibição do ícone Olá toohave. |
| **Primeiro gráfico<br>Segundo gráfico** | |
| Legenda |Toodisplay de texto em texto explicativo de saudação primeira série de saudação. |
| Cor |Cor toouse para colunas de saudação na série de saudação. |
| Consultar |Consulta toorun primeira série de saudação.  Contagem de saudação do número de saudação de registros em cada intervalo de tempo será representada por colunas de saudação do gráfico. |
| Operação |Olá tooperform operação Olá valor toosummarize tooa único valor da propriedade de texto explicativo de saudação.<br><br>-Soma: A soma do valor de saudação de todos os registros.<br>-Média: Média do valor de saudação de todos os registros.<br>-Último exemplo: O valor do último intervalo de saudação incluído no gráfico de saudação.<br>-O primeiro exemplo: O valor do primeiro intervalo de saudação incluído no gráfico de saudação.<br>-Contagem: Contagem de todos os registros retornados pela consulta hello. |
| **Lista** | |
| Consultar |Toorun de consulta para a lista de saudação.  Contagem de saudação do número de saudação de registros retornados pela consulta hello será exibida. |
| Ocultar gráfico |Selecione toodisable Olá gráfico toohello direito de coluna numérica hello. |
| Habilitar minigráficos |Selecione o Minigráfico toodisplay em vez de barra horizontal.  Consulte [Configurações Comuns](#sparklines) para obter detalhes. |
| Cor |Cor das barras de saudação ou Minigráficos. |
| Operação |Operação tooperform para Olá Minigráfico.  Consulte [Configurações Comuns](#sparklines) para obter detalhes. |
| Consulta de navegação |Consultar toorun ao usuário Olá seleciona um item na lista de saudação.  Consulte [Configurações Comuns](#navigation-query) para obter detalhes. |
| **Lista** |**> Títulos de coluna** |
| Nome |Toodisplay de texto na parte superior de saudação da primeira coluna Olá da lista de saudação. |
| Valor |Toodisplay de texto na parte superior de saudação da segunda coluna Olá da lista de saudação. |
| **Lista** |**> Limites** |
| Habilitar limites |Selecione limites tooenable.  Consulte [Configurações Comuns](#thresholds) para obter detalhes. |

## <a name="information-part"></a>Parte de informações
O cabeçalho exibe texto estático e um link opcional.  A lista exibe um ou mais itens com texto estático e o título.

![Exibição de informações](media/log-analytics-view-designer/view-information.png)

| Configuração | Descrição |
|:--- |:--- |
| **Geral** | |
| Título do Grupo |Toodisplay de texto na parte superior de saudação do hello lado a lado. |
| Novo Grupo |Selecione toocreate um novo grupo na exibição de saudação iniciar no modo de exibição atual hello. |
| Cor |Cor de plano de fundo do cabeçalho de saudação. |
| **Cabeçalho** | |
| Imagem |Toodisplay de arquivo de imagem no cabeçalho de saudação. |
| Rótulo |Toodisplay de texto no cabeçalho de saudação. |
| **Cabeçalho** |**> Link** |
| Rótulo |Texto do link. |
| Url |URL do link. |
| **Itens de Informações** | |
| Title |Toodisplay de texto de título de cada item. |
| Conteúdo |Toodisplay de texto para cada item. |

## <a name="line-chart-callout--list-part"></a>Parte de gráfico de linhas, balão e lista
O cabeçalho exibe um gráfico de linhas com várias séries de uma consulta de log ao longo do tempo, além de um balão com um valor resumido.  Lista exibe o saudação dez primeiros resultados de uma consulta com um gráfico que indica o valor relativo de saudação de uma coluna numérica ou as alterações ao longo do tempo.

![Exibição de gráfico de linhas, balão e lista](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| Configuração | Descrição |
|:--- |:--- |
| **Geral** | |
| Título do Grupo |Toodisplay de texto na parte superior de saudação do hello lado a lado. |
| Novo Grupo |Selecione toocreate um novo grupo na exibição de saudação iniciar no modo de exibição atual hello. |
| ícone |Arquivo toodisplay próximo toohello resultado no cabeçalho de saudação da imagem. |
| Usar Ícone |Selecione a exibição do ícone Olá toohave. |
| **Cabeçalho** | |
| Title |Toodisplay de texto na parte superior de saudação do cabeçalho de saudação. |
| Subtítulo |Texto toodisplay em Olá título na parte superior de saudação do cabeçalho de saudação. |
| **Gráfico de Linhas** | |
| Consultar |Toorun de consulta para o gráfico de linha de saudação.  propriedade primeiro Olá deve ser um valor e hello segunda propriedade text um valor numérico.  Isso é normalmente uma consulta que usa Olá **medidas** resultados toosummarize de palavra-chave.  Se a consulta Olá usa Olá **intervalo** palavra-chave e Olá eixo x do gráfico de saudação usará esse intervalo de tempo.  Se a consulta Olá não incluir Olá **intervalo** intervalos de palavra-chave e por hora são usados para Olá eixo x. |
| **Gráfico de Linhas** |**> Balão** |
| Título do balão |Texto toodisplay acima do valor de texto explicativo hello. |
| Nome da Série |Valor da propriedade de saudação série toouse para o valor de texto explicativo hello.  Se nenhuma série for fornecido, todos os registros da consulta hello são usados. |
| Operação |Olá tooperform operação Olá valor toosummarize tooa único valor da propriedade de texto explicativo de saudação.<br><br>-Média: Média do valor de saudação de todos os registros.<br>-Contagem de contagem de todos os registros retornados pela consulta hello.<br>-Último exemplo: O valor do último intervalo de saudação incluído no gráfico de saudação.<br>-Max: O valor de máximo de intervalos de saudação incluídos no gráfico de saudação.<br>-Mín: O valor de mínimo de intervalos de saudação incluídos no gráfico de saudação.<br>-Soma: A soma do valor de saudação de todos os registros. |
| **Gráfico de Linhas** |**> Eixo Y** |
| Usar Escala Logarítmica |Selecione toouse uma escala logarítmica de saudação eixo y. |
| Unidades |Especifique unidades Olá Olá valores retornados pela consulta hello.  Essas informações são rótulos toodisplay usadas no gráfico de saudação que indica os tipos de valor hello e, opcionalmente, para converter valores hello.  Olá tipo de unidade Especifica Olá categoria da unidade hello e define os valores de tipo de unidade atual de saudação que estão disponíveis.  Se você selecionar um valor em Converter toothen Olá numérico valores são convertidos de saudação unidade atual tipo toohello Convert tootype. |
| Rótulo Personalizado |Texto toodisplay Olá eixo Y próxima toohello rótulo para o tipo de unidade de saudação.  Se nenhum nome for especificado, somente o tipo de unidade de saudação é exibido. |
| **Lista** | |
| Consultar |Toorun de consulta para a lista de saudação.  Contagem de saudação do número de saudação de registros retornados pela consulta hello será exibida. |
| Ocultar gráfico |Selecione toodisable Olá gráfico toohello direito de coluna numérica hello. |
| Habilitar minigráficos |Selecione o Minigráfico toodisplay em vez de barra horizontal.  Consulte [Configurações Comuns](#sparklines) para obter detalhes. |
| Cor |Cor das barras de saudação ou Minigráficos. |
| Operação |Operação tooperform para Olá Minigráfico.  Consulte [Configurações Comuns](#sparklines) para obter detalhes. |
| Separador de Valor e Nome |Delimitador de caractere, se você quiser que a propriedade de texto de saudação tooparse em vários valores.  Consulte [Configurações Comuns](#name-value-separator) para obter detalhes. |
| Consulta de navegação |Consultar toorun ao usuário Olá seleciona um item na lista de saudação.  Consulte [Configurações Comuns](#navigation-query) para obter detalhes. |
| **Lista** |**> Títulos de coluna** |
| Nome |Toodisplay de texto na parte superior de saudação da primeira coluna Olá da lista de saudação. |
| Valor |Toodisplay de texto na parte superior de saudação da segunda coluna Olá da lista de saudação. |
| **Lista** |**> Limites** |
| Habilitar limites |Selecione limites tooenable.  Consulte [Configurações Comuns](#thresholds) para obter detalhes. |

## <a name="line-chart--list-part"></a>Parte de gráfico de linhas e lista
O cabeçalho exibe um gráfico de linhas com várias séries de uma consulta de log ao longo do tempo.  Lista exibe o saudação dez primeiros resultados de uma consulta com um gráfico que indica o valor relativo de saudação de uma coluna numérica ou as alterações ao longo do tempo.

![Exibição de gráfico de linhas e lista](media/log-analytics-view-designer/view-line-chart-callout-list.png)

| Configuração | Descrição |
|:--- |:--- |
| **Geral** | |
| Título do Grupo |Toodisplay de texto na parte superior de saudação do hello lado a lado. |
| Novo Grupo |Selecione toocreate um novo grupo na exibição de saudação iniciar no modo de exibição atual hello. |
| ícone |Arquivo toodisplay próximo toohello resultado no cabeçalho de saudação da imagem. |
| Usar Ícone |Selecione a exibição do ícone Olá toohave. |
| **Cabeçalho** | |
| Title |Toodisplay de texto na parte superior de saudação do cabeçalho de saudação. |
| Subtítulo |Texto toodisplay em Olá título na parte superior de saudação do cabeçalho de saudação. |
| **Gráfico de Linhas** | |
| Consultar |Toorun de consulta para o gráfico de linha de saudação.  propriedade primeiro Olá deve ser um valor e hello segunda propriedade text um valor numérico.  Isso é normalmente uma consulta que usa Olá **medidas** resultados toosummarize de palavra-chave.  Se a consulta Olá usa Olá **intervalo** palavra-chave e Olá eixo x do gráfico de saudação usará esse intervalo de tempo.  Se a consulta Olá não incluir Olá **intervalo** intervalos de palavra-chave e por hora são usados para Olá eixo x. |
| **Gráfico de Linhas** |**> Eixo Y** |
| Usar Escala Logarítmica |Selecione toouse uma escala logarítmica de saudação eixo y. |
| Unidades |Especifique unidades Olá Olá valores retornados pela consulta hello.  Essas informações são rótulos toodisplay usadas no gráfico de saudação que indica os tipos de valor hello e, opcionalmente, para converter valores hello.  Olá tipo de unidade Especifica Olá categoria da unidade hello e define os valores de tipo de unidade atual de saudação que estão disponíveis.  Se você selecionar um valor em Converter toothen Olá numérico valores são convertidos de saudação unidade atual tipo toohello Convert tootype. |
| Rótulo Personalizado |Texto toodisplay Olá eixo Y próxima toohello rótulo para o tipo de unidade de saudação.  Se nenhum nome for especificado, somente o tipo de unidade de saudação é exibido. |
| **Lista** | |
| Consultar |Toorun de consulta para a lista de saudação.  Contagem de saudação do número de saudação de registros retornados pela consulta hello será exibida. |
| Ocultar gráfico |Selecione toodisable Olá gráfico toohello direito de coluna numérica hello. |
| Habilitar minigráficos |Selecione o Minigráfico toodisplay em vez de barra horizontal.  Consulte [Configurações Comuns](#sparklines) para obter detalhes. |
| Cor |Cor das barras de saudação ou Minigráficos. |
| Operação |Operação tooperform para Olá Minigráfico.  Consulte [Configurações Comuns](#sparklines) para obter detalhes. |
| Separador de Valor e Nome |Delimitador de caractere, se você quiser que a propriedade de texto de saudação tooparse em vários valores.  Consulte [Configurações Comuns](#name-value-separator) para obter detalhes. |
| Consulta de navegação |Consultar toorun ao usuário Olá seleciona um item na lista de saudação.  Consulte [Configurações Comuns](#navigation-query) para obter detalhes. |
| **Lista** |**> Títulos de coluna** |
| Nome |Toodisplay de texto na parte superior de saudação da primeira coluna Olá da lista de saudação. |
| Valor |Toodisplay de texto na parte superior de saudação da segunda coluna Olá da lista de saudação. |
| **Lista** |**> Limites** |
| Habilitar limites |Selecione limites tooenable.  Consulte [Configurações Comuns](#thresholds) para obter detalhes. |

## <a name="stack-of-line-charts-part"></a>Pilha de parte de gráficos de linha
Exibe três gráficos de linhas separados com várias séries de uma consulta de log ao longo do tempo.

![Pilha de gráficos de linha](media/log-analytics-view-designer/view-stack-line-charts.png)

| Configuração | Descrição |
|:--- |:--- |
| **Geral** | |
| Título do Grupo |Toodisplay de texto na parte superior de saudação do hello lado a lado. |
| Novo Grupo |Selecione toocreate um novo grupo na exibição de saudação iniciar no modo de exibição atual hello. |
| ícone |Arquivo toodisplay próximo toohello resultado no cabeçalho de saudação da imagem. |
| **Gráfico 1<br>Gráfico 2<br>Gráfico 3** |**> Cabeçalho** |
| Title |Toodisplay de texto na parte superior de saudação do gráfico de saudação. |
| Subtítulo |Texto toodisplay em Olá título na parte superior de saudação do gráfico de saudação. |
| **Gráfico 1<br>Gráfico 2<br>Gráfico 3** |**Gráfico de Linhas** |
| Consultar |Toorun de consulta para o gráfico de linha de saudação.  propriedade primeiro Olá deve ser um valor e hello segunda propriedade text um valor numérico.  Isso é normalmente uma consulta que usa Olá **medidas** resultados toosummarize de palavra-chave.  Se a consulta Olá usa Olá **intervalo** palavra-chave e Olá eixo x do gráfico de saudação usará esse intervalo de tempo.  Se a consulta Olá não incluir Olá **intervalo** intervalos de palavra-chave e por hora são usados para Olá eixo x. |
| **Gráfico** |**> Eixo Y** |
| Usar Escala Logarítmica |Selecione toouse uma escala logarítmica de saudação eixo y. |
| Unidades |Especifique unidades Olá Olá valores retornados pela consulta hello.  Essas informações são rótulos toodisplay usadas no gráfico de saudação que indica os tipos de valor hello e, opcionalmente, para converter valores hello.  Olá tipo de unidade Especifica Olá categoria da unidade hello e define os valores de tipo de unidade atual de saudação que estão disponíveis.  Se você selecionar um valor em Converter toothen Olá numérico valores são convertidos de saudação unidade atual tipo toohello Convert tootype. |
| Rótulo Personalizado |Texto toodisplay Olá eixo Y próxima toohello rótulo para o tipo de unidade de saudação.  Se nenhum nome for especificado, somente o tipo de unidade de saudação é exibido. |

## <a name="common-settings"></a>Configurações comuns
Olá seções a seguir descreve partes do configurações comuns tooseveral visualização.

### <a name="name-value-separator">Separador de valor e nome</a>
Delimitador de caractere, se você quiser tooparse propriedade de texto de saudação de uma consulta de lista em vários valores.  Se você especificar um delimitador, você pode fornecer nomes para cada campo separado por Olá mesmo delimitador na caixa de nome de saudação.

Por exemplo, considere uma propriedade chamada *Localização* que incluía valores como *Redmond-Building 41* e *Bellevue-Building12*.  Você pode especificar – para Olá nome & separador de valor e *City Building* para Olá nome.  Isso analisaria cada valor em duas propriedades chamadas *Cidade* e *Edifício*.

### <a name="navigation-query">Consulta de navegação</a>
Consultar toorun ao usuário Olá seleciona um item na lista de saudação.  Use *{item selecionado}* tooinclude sintaxe Olá item que Olá selecionado pelo usuário.

Por exemplo, se hello consulta tem uma coluna chamada *computador* e consulta de navegação Olá é *{item selecionado}*, uma consulta, como *computador = "MyComputer"* seria executado quando usuário Olá um computador selecionado.  Se a consulta de navegação Olá é *tipo = evento {item selecionado}* , em seguida, consulta de saudação *tipo = evento computador = "MyComputer"* seriam executadas.

### <a name="sparklines">Minigráficos</a>
Um minigráfico é um gráfico de linha pequena que ilustra o valor de saudação de uma entrada de lista ao longo do tempo.  Para partes de visualização com uma lista, você pode selecionar se toodisplay uma barra indicando horizontal Olá valor relativo de uma coluna numérica ou um minigráfico indicando seu valor ao longo do tempo.

Olá, a tabela a seguir descreve as configurações de saudação para Minigráficos.

| Configuração | Descrição |
|:--- |:--- |
| Habilitar minigráficos |Selecione o Minigráfico toodisplay em vez de barra horizontal. |
| Operação |Se os Minigráficos são habilitados, este é Olá operação tooperform em cada propriedade no hello toocalculate Olá valores hello Minigráfico.<br><br>-Última amostra: O último valor para a série Olá durante o intervalo de tempo hello.<br>-Max: O valor de máximo série Olá durante o intervalo de tempo hello.<br>-Mín: Valor mínimo série Olá durante o intervalo de tempo hello.<br>-Soma: Soma de valores de séries Olá durante o intervalo de tempo hello.<br>-Resumo: Usa Olá mesmo comando de medida como consulta Olá no cabeçalho de saudação. |

### <a name="thresholds">Limites</a>
Limites permitem que você toodisplay um item de tooeach próximo ícone colorida em uma lista, dando a você um indicador visual rápido de itens que excedem um valor específico ou ficam dentro de um intervalo específico.  Por exemplo, você pode exibir um ícone verde de itens com um valor aceitável, amarelo, se o valor de saudação está dentro do intervalo que indica um aviso e vermelho se exceder um valor de erro.

Quando você habilitar os limites para uma parte, será necessário especificar um ou mais limites.  Se o valor de saudação de um item for maior que um valor de limite e menor que o próximo valor de limite Olá, essa cor é usada.  Se o item de saudação for maior que o valor de limite, em seguida, mais alto, essa cor é definida.   

Cada conjunto de limite tem um limite com um valor de **Padrão**.  Isso é cor Olá definida se nenhum outro valor seja excedido.  Você pode adicionar ou remover os limites clicando Olá  **+**  ou **x** botão.

Olá, a tabela a seguir descreve as configurações de saudação para tresholds.

| Configuração | Descrição |
|:--- |:--- |
| Habilitar limites |Selecione toodisplay que um toohello de ícone de cor à esquerda de cada valor indicando seus limites de toospecified relativo de integridade. |
| Nome |Valor de limite de saudação do nome tooidentify. |
| Limite |Valor de limite de saudação.  cor de integridade Olá para cada item da lista é definir a cor de toohello do valor de limite mais alto Olá excedido pelo valor do item de saudação.  Há um limite padrão que é a cor de saudação se nenhum valor de limite seja excedido. |
| Cor |Cor do valor de limite de saudação. |

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [pesquisas de log](log-analytics-log-searches.md) toosupport consultas de saudação em partes de visualização.
