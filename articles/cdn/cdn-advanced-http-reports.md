---
title: "estatísticas de uso de aaaAnalyze com o Azure CDN avançadas relatórios HTTP | Microsoft Docs"
description: "Saiba como toocreate avançado HTTP relatórios no Microsoft Azure CDN. Esses relatórios fornecem informações detalhadas sobre a atividade da CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ef90adc1-580e-4955-8ff1-bde3f3cafc5d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 3184ec00d089613e25c62762f93043cb4ba68394
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-usage-statistics-with-azure-cdn-advanced-http-reports"></a>Analisar estatísticas de uso com os relatórios HTTP avançados da CDN do Azure
## <a name="overview"></a>Visão geral
Este documento explica os relatórios HTTP avançados na CDN do Microsoft Azure. Esses relatórios fornecem informações detalhadas sobre a atividade da CDN.

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="accessing-advanced-http-reports"></a>Acessando relatórios HTTP avançados
1. Na folha de perfil CDN hello, clique em Olá **gerenciar** botão.
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-advanced-http-reports/cdn-manage-btn.png)
   
    portal de gerenciamento de CDN Olá é aberto.
2. Passe o mouse sobre Olá **análise** guia, em seguida, passe o mouse sobre Olá **avançado HTTP relatórios** submenu.  Clique em **Plataforma Grande HTTP**.
   
    ![Portal de gerenciamento da CDN - menu Relatórios Avançados](./media/cdn-advanced-http-reports/cdn-advanced-reports.png)
   
    As opções de relatório são exibidas.

## <a name="geography-reports-map-based"></a>Relatórios de Geografia (baseados em mapa)
Há cinco relatórios que aproveitam tooindicate um mapa de regiões de saudação do qual o conteúdo está sendo solicitado. Esses relatórios são Mapa mundial, Mapa dos Estados Unidos, Mapa do Canadá, Mapa da Europa e Mapa do Pacífico Asiático.

Cada relatório baseada em mapa classifica entidades geográficas (ou seja, países, Estados e províncias) de acordo com o toohello porcentagem de acertos originadas dessa região. Além disso, um mapa é fornecido toohelp você visualizar locais de saudação do qual o conteúdo está sendo solicitado. É possível toodo codificando cada região de acordo com o valor de toohello de demanda apresentou nessa região. As regiões com cores mais claras indicam menor demanda por seu conteúdo, enquanto regiões mais escuras indicam altos níveis de demanda por seu conteúdo.

Informações detalhadas de tráfego e largura de banda para cada região são fornecidas diretamente abaixo mapa hello. Isso permite tooview Olá total de acertos, porcentagem de saudação de acertos, total de saudação de dados transferidos (em gigabytes) e porcentagem Olá dos dados transferidos para cada região. Exiba uma descrição para cada uma das métricas. Finalmente, quando você focaliza uma região (ou seja, país, estado ou província), nome hello e o percentual de saudação de ocorrências que ocorreu na região de saudação serão exibidos como uma dica de ferramenta.

Uma breve descrição abaixo é apresentada abaixo para cada tipo de relatório geográfico baseado em mapa.

| Nome do relatório | Descrição |
| --- | --- |
| Mapa mundial |Este relatório permite à demanda mundial de saudação tooview para o seu conteúdo CDN. Cada país são codificadas por cores em porcentagem de Olá de tooindicate Olá mundo mapa de ocorrências que originou dessa região. |
| Mapa dos Estados Unidos |Este relatório permite tooview demanda de saudação para seu conteúdo CDN no hello dos Estados Unidos. Cada estado é codificado por cores nessa porcentagem de saudação tooindicate mapa de ocorrências que originou dessa região. |
| Mapa do Canadá |Este relatório permite tooview demanda de saudação para o seu conteúdo CDN no Canadá. Cada município é codificado por cores nessa porcentagem de saudação tooindicate mapa de ocorrências que originou dessa região. |
| Mapa da Europa |Este relatório permite tooview demanda de saudação para o seu conteúdo CDN na Europa. Cada país é codificado por cores nessa porcentagem de saudação tooindicate mapa de ocorrências que originou dessa região. |
| Mapa do Pacífico Asiático |Este relatório permite tooview demanda de saudação para o seu conteúdo CDN na Ásia. Cada país é codificado por cores nessa porcentagem de saudação tooindicate mapa de ocorrências que originou dessa região. |

## <a name="geography-reports-bar-charts"></a>Relatórios de geografia (gráficos de barras)
Há dois relatórios adicionais que fornecem informações estatísticas de acordo com o toogeography, que são parte superior cidades e países da parte superior. Esses relatórios classificam cidades e países, respectivamente, de acordo com o número toohello de ocorrências foi originado essas regiões. Após gerar esse tipo de relatório, um gráfico de barras indicará top 10 cidades hello ou países que solicitou o conteúdo em uma plataforma específica. Este gráfico de barras permite tooquickly avaliar regiões Olá que geram um número mais alto de saudação de solicitações para o seu conteúdo.

lado esquerdo de saudação do gráfico de saudação (eixo y) indica o número de ocorrências ocorreu na região especificada hello. Diretamente abaixo de gráfico de saudação (eixo x), você encontrará um rótulo para cada uma das regiões de 10 principais hello.

### <a name="using-hello-bar-charts"></a>Usando gráficos de barras Olá
* Se você passar o mouse sobre uma barra, nome hello e número total de saudação de ocorrências que ocorreram na região hello serão exibidos como uma dica de ferramenta.
* Dica de ferramenta Olá Olá relatório superior cidades identifica uma cidade por seu nome, o estado e a abreviação de país.
* Se não foi possível determinar a cidade de saudação ou região (ou seja, estado/província) de uma solicitação de origem, em seguida, ela indicará que são desconhecidas. Se o país Olá for desconhecido, dois pontos de interrogação (isto é,?), será exibida.
* Um relatório pode incluir as métricas para "Europa" ou hello "Região da Ásia-Pacífico /". Esses itens não devem tooprovide informações de estatísticas em todos os endereços IP nessas áreas. Em vez disso, elas se aplicam apenas toorequests que se originam endereços IP que são difundidos em Europa ou na Ásia/Pacífico, em vez de cidade específica tooa ou país.

dados de saudação que era o gráfico de barras Olá toogenerate usados podem ser exibidos abaixo dela. Lá você encontrará o número total de saudação de ocorrências, porcentagem de saudação de ocorrências, a quantidade de saudação de dados transferidos (em gigabytes), e o percentual de saudação de dados transferidos para Olá 250 regiões superiores. Exiba uma descrição para cada uma das métricas.

Uma breve descrição é apresentada para ambos os tipos de relatórios abaixo.

| Nome do relatório | Descrição |
| --- | --- |
| Principais cidades |Este relatório classifica cidades de acordo com o toohello número de ocorrências se originou nessa região. |
| Principais países |Este relatório classifica de acordo com o toohello número de ocorrências que originou dessa região de países. |

## <a name="daily-summary"></a>Resumo diário
Olá relatório de resumo diário permite tooview Olá total de acertos e dados transferidos por uma plataforma específica em uma base diária. Essas informações podem ser usadas tooquickly distinguir os padrões de atividade CDN. Por exemplo, esse relatório pode ajudá-lo a detectar quais dias tiveram tráfego maior ou menor que o esperado.

Após gerar esse tipo de relatório, um gráfico de barras fornecem uma indicação visual como toohello quantidade específica de plataforma a demanda experientes diariamente Olá período de tempo coberto pelo relatório de saudação. Ele fará isso ao exibir uma barra para cada dia no relatório de saudação. Por exemplo, selecionando Olá período chamado "Última semana" irá gerar um gráfico de barras com sete barras. Cada barra indicará o número total de saudação de acertos apresentou naquele dia.

Olá lado esquerdo do gráfico de saudação (eixo y) indica o número de ocorrências ocorreu em Olá especificado Data. Diretamente abaixo de gráfico de saudação (eixo x), você encontrará um rótulo que indica a data de saudação (formato: AAAA-MM-DD) para cada dia incluído no relatório de saudação.

> [!TIP]
> Se você passar o mouse sobre uma barra, Olá o número total de acertos que ocorreram nessa data será exibido como uma dica de ferramenta.
> 
> 

dados de saudação que era o gráfico de barras Olá toogenerate usados podem ser exibidos abaixo dela. Lá você encontrará número total de saudação de ocorrências e a quantidade de saudação de dados transferidos (em gigabytes) para cada dia coberto pelo relatório de saudação.

## <a name="by-hour"></a>Por hora
Olá relatórios por hora permite tooview Olá total de acertos e dados transferidos por uma plataforma específica em uma base por hora. Essas informações podem ser usadas tooquickly distinguir os padrões de atividade CDN. Por exemplo, este relatório pode ajudá-lo a detectar Olá períodos de tempo durante o dia de saudação experiência superior ou inferior a tráfego esperado.

Após gerar esse tipo de relatório, um gráfico de barras fornecem uma indicação visual como valor toohello apresentou por hora sobre Olá período de tempo coberto pelo relatório Olá a demanda específico da plataforma. Ele fará isso ao exibir uma barra para cada hora coberta pelo relatório de saudação. Por exemplo, a seleção de um período de 24 horas irá gerar um gráfico de barras com vinte e quatro barras. Cada barra indicará o número total de saudação de acertos durante essa hora.

lado esquerdo de saudação do gráfico de saudação (eixo y) indica o número de ocorrências ocorreu na hora especificada hello. Diretamente abaixo de gráfico de saudação (eixo x), você encontrará um rótulo que indica a data/hora da saudação (formato: AAAA-MM-DD HH: mm) para cada hora incluída no relatório de saudação. Tempo é relatado usando o formato de 24 horas e é especificado usando o fuso horário UTC/GMT hello.

> [!TIP]
> Se você passar o mouse sobre uma barra, Olá o número total de acertos de que ocorreu durante essa hora será exibido como uma dica de ferramenta.
> 
> 

dados de saudação que era o gráfico de barras Olá toogenerate usados podem ser exibidos abaixo dela. Lá você encontrará número total de saudação de ocorrências e a quantidade de saudação de dados transferidos (em gigabytes) para cada hora coberta pelo relatório de saudação.

## <a name="by-file"></a>Por arquivo
Olá pelo arquivo de relatório permite que você tooview Olá quantidade de tráfego de demanda e hello criada em uma plataforma específica para hello mais solicitado ativos. Após gerar esse tipo de relatório, um gráfico de barras será gerado em ativos de mais solicitados 10 principais Olá sobre Olá período de tempo especificado.

> [!NOTE]
> Para fins de saudação deste relatório, borda CNAME URLs são convertidos tootheir equivalente CDN URLs. Isso permite que uma contagem precisa para o número total de saudação de acertos associados a um ativo independentemente Olá CDN ou borda CNAME URL usada toorequest-lo.
> 
> 

lado esquerdo de saudação do gráfico de saudação (eixo y) indica o número de saudação de solicitações para cada ativo sobre Olá período de tempo especificado. Diretamente abaixo de gráfico de saudação (eixo x), você encontrará um rótulo que indica o nome do arquivo hello para cada um dos principais ativos solicitados 10 hello.

dados de saudação que era o gráfico de barras Olá toogenerate usados podem ser exibidos abaixo dela. Lá você encontrará Olá seguintes informações para cada um dos principais ativos solicitados 250 Olá: caminho relativo, número total de saudação de ocorrências, porcentagem de saudação de acertos, quantidade Olá dos dados transferidos (em gigabytes) e a porcentagem de saudação de dados transferidos.

## <a name="by-file-detail"></a>Por detalhes do arquivo
Olá relatório por detalhes do arquivo permite que você tooview quantidade de saudação do tráfego de demanda e hello incorrida em uma plataforma específica para um ativo específico. Olá início deste relatório é Olá arquivo detalhes como opção. Essa opção fornece uma lista dos ativos mais solicitados na plataforma selecionada hello. Ordem toogenerate um relatório por detalhes do arquivo, você precisará tooselect Olá desejado do ativo Olá detalhes de arquivo para a opção. Depois disso, um gráfico de barras serão indicam a quantidade de saudação de demanda diária que ela gerada pela Olá período de tempo especificado.

lado esquerdo de saudação do gráfico de saudação (eixo y) indica Olá total de solicitações que passou por um ativo em um dia específico. Diretamente abaixo de gráfico de saudação (eixo x), você encontrará um rótulo que indica a data de saudação (formato: AAAA-MM-DD) para que demanda CDN para Olá ativo foi relatado.

dados de saudação que era o gráfico de barras Olá toogenerate usados podem ser exibidos abaixo dela. Lá você encontrará número total de saudação de ocorrências e a quantidade de saudação de dados transferidos (em gigabytes) para cada dia coberto pelo relatório de saudação.

## <a name="by-file-type"></a>Por tipo de arquivo
Olá relatórios por tipo de arquivo permite que você tooview Olá quantidade de tráfego por demanda e hello incorrida pelo tipo de arquivo. Após gerar esse tipo de relatório, um gráfico de rosca indicará porcentagem Olá de acertos gerados por tipos de arquivo 10 principais hello.

> [!TIP]
> Se você passar o mouse sobre uma fatia no gráfico de rosca hello, Olá Internet tipo de mídia de que tipo de arquivo será exibido como uma dica de ferramenta.
> 
> 

dados de saudação que era o gráfico de rosca Olá toogenerate usados podem ser exibidos abaixo dela. Lá você encontrará o tipo de mídia extensão/Internet do nome de arquivo hello, número total de saudação de ocorrências, porcentagem de saudação de acertos de, quantidade de saudação de dados transferidos (em gigabytes) e porcentagem dos dados transferidos para cada Olá Olá principais 250 tipos de arquivo.

## <a name="by-directory"></a>Por diretório
relatório de diretório por Olá permite tooview quantidade de saudação do tráfego de demanda e hello incorrida em uma plataforma específica para o conteúdo de um diretório específico. Após gerar esse tipo de relatório, um gráfico de barras indicará o número total de saudação de acertos gerados pelo conteúdo top 10 diretórios hello.

### <a name="using-hello-bar-chart"></a>Usando o gráfico de barras Olá
* Passe o mouse sobre uma barra de diretório correspondente do toohello tooview Olá caminho relativo.
* O conteúdo armazenado em uma subpasta de um diretório não será contado no cálculo da demanda por diretório. Esse cálculo baseia-se exclusivamente no número de saudação de solicitações geradas para conteúdo armazenado no diretório de saudação real.
* Para fins de saudação deste relatório, borda CNAME URLs são convertidos tootheir equivalente CDN URLs. Isso permite que uma contagem precisa para todas as estatísticas associados a um ativo independentemente Olá CDN ou borda CNAME URL usada toorequest-lo.

Hello, lado esquerdo do gráfico de saudação (eixo y) indica Olá o número total de solicitações de saudação conteúdo armazenado em seus diretórios de 10 principais. Cada barra no gráfico de saudação representa um diretório. Olá Use esquema toomatch uma barra de codificação de cores tooa directory listados na seção de superior 250 completo diretórios de saudação.

dados de saudação que era o gráfico de barras Olá toogenerate usados podem ser exibidos abaixo dela. Lá você encontrará Olá seguintes informações para cada um dos diretórios de superior a 250 Olá: caminho relativo, número total de saudação de ocorrências, porcentagem de saudação de acertos, quantidade Olá dos dados transferidos (em gigabytes) e a porcentagem de saudação de dados transferidos.

## <a name="by-browser"></a>Por navegador
Olá relatório pelo navegador permite que você tooview quais navegadores foram usado toorequest conteúdo. Após gerar esse tipo de relatório, um gráfico de pizza indicará porcentagem Olá de solicitação manipulado por navegadores de 10 principais hello.

### <a name="using-hello-pie-chart"></a>Usar o gráfico de pizza Olá
* Passe o mouse sobre uma fatia Olá gráfico de pizza tooview versão e o nome do navegador.
* Para fins de saudação deste relatório, cada combinação exclusiva de navegador/versão é considerada um navegador diferente.
* Olá fatia chamada "Outra" indica a porcentagem de saudação de solicitação manipulado por todos os navegadores e versões.

dados de saudação que era o gráfico de pizza Olá toogenerate usados podem ser exibidos abaixo dela. Lá você encontrará Olá navegador tipo/número de versão, Olá total de acertos e porcentagem de saudação de ocorrências para cada um dos navegadores de 250 superior Olá.

## <a name="by-referrer"></a>Por referenciador
Olá relatório referenciador por permite tooview Olá principais referenciadores toocontent na plataforma selecionada hello. Uma referência indica hostname de saudação do que uma solicitação foi gerada. Após gerar esse tipo de relatório, um gráfico de barras indicará a quantidade de saudação de demanda (ou seja, acertos) gerado pelo 10 Referenciadores principais de saudação.

lado esquerdo de saudação do gráfico de saudação (eixo y) indica Olá total de solicitações que passou por um ativo para cada referência. Cada barra no gráfico de saudação representa uma referência. Olá Use esquema toomatch uma barra de codificação de cores tooa referenciador listadas na seção de superior 250 referenciador de saudação.

dados de saudação que era o gráfico de barras Olá toogenerate usados podem ser exibidos abaixo dela. Lá você encontrará Olá URL, o número total de saudação de ocorrências e a porcentagem de saudação do acertos gerados a partir de cada um dos principais referenciadores de 250 hello.

## <a name="by-download"></a>Por download
Olá por baixar relatório permite que você tooanalyze padrões de download para o seu conteúdo mais solicitado. parte superior de saudação do relatório Olá contém um gráfico de barras que compara a tentativa de downloads com downloads concluídos para hello top 10 ativos solicitados. Cada barra é codificado por cores toowhether é de acordo com um download concluído (verde) ou um tentativa de download (azul).

> [!NOTE]
> Para fins de saudação deste relatório, borda CNAME URLs são convertidos tootheir equivalente CDN URLs. Isso permite que uma contagem precisa para todas as estatísticas associados a um ativo independentemente Olá CDN ou borda CNAME URL usada toorequest-lo.
> 
> 

lado esquerdo de saudação do gráfico de saudação (eixo y) indica o nome do arquivo de saudação para cada um dos principais ativos solicitados 10 hello. Diretamente abaixo de gráfico de saudação (eixo x), você encontrará rótulos que indicam o número total de saudação de downloads tentativa/concluída.

Diretamente abaixo do gráfico de barras hello, Olá informações a seguir será listado para principais ativos solicitados 250 Olá: caminho relativo (incluindo o nome de arquivo), número de saudação de vezes que foi baixado toocompletion, número de saudação de vezes que foi solicitada e Olá Porcentagem de solicitações que resultou em um download completo.

> [!TIP]
> Nossa CDN não é informada por um cliente HTTP (ou seja, o navegador) quando um ativo é baixado por completo. Como resultado, temos toocalculate se um ativo foi completamente baixado códigos de toostatus acordo e solicitações de intervalo de bytes. Olá primeiro, procuramos quando fazer esse cálculo é se a solicitação de saudação resulta em um código de status Okey 200. Nesse caso, em seguida, vamos examinar tooensure de solicitações de intervalo de bytes que abrangem ativo todo hello. Por fim, podemos comparar quantidade Olá transferidos toohello do tamanho dos dados de ativo solicitada hello. Se Olá dados transferidos é igual tooor maior que o tamanho do arquivo hello e solicitações de intervalo de bytes de saudação são apropriadas para esse ativo, Olá ocorrência será contabilizada como um download completo.
> 
> Devido a natureza de autorização interpretativa toohello deste relatório, você deve manter em Olá mente pontos que podem alterar consistência hello e precisão deste relatório a seguir.
> 
> * Padrões de tráfego não podem ser previstos com precisão quando os agentes-usuários se comportam de maneira diferente. Isso pode produzir resultados de download concluído acima de 100%.
> * Ativos que tiram proveito do download progressivo de HTTP podem não ser representados com precisão no relatório. Isso é devido toousers busca toodifferent posições em um vídeo.
> 
> 

## <a name="by-404-errors"></a>Por erros 404
Olá relatório por erros de 404 permite tooidentify tipo de saudação do conteúdo que gera hello mais número 404 não encontrado dos códigos de status. parte superior de saudação do relatório Olá contém um gráfico de barras para ativos de 10 principais Olá para o qual foi retornado um código de status 404 não encontrado. Este gráfico de barras compara o número total de saudação de solicitações com solicitações que resultaram no código de status 404 não encontrado para esses ativos. Cada barra é codificada por cor. Uma barra amarela é usada tooindicate que Olá solicitação resultou em um código de status 404 não encontrado. Uma barra vermelha é usada tooindicate Olá total de solicitações para o ativo de saudação.

> [!NOTE]
> Para fins de saudação deste relatório, observe o seguinte de saudação:
> 
> * Uma ocorrência representa qualquer solicitação para um ativo, independentemente do código de status.
> * URLs de CNAME de borda são convertidos tootheir equivalente CDN URLs. Isso permite que uma contagem precisa para todas as estatísticas associados a um ativo independentemente Olá CDN ou borda CNAME URL usada toorequest-lo.
> 
> 

lado esquerdo de saudação do gráfico de saudação (eixo y) indica o nome do arquivo de saudação para cada Olá top 10 ativos solicitados que resultaram em um código de status 404 não encontrado. Diretamente abaixo de gráfico de saudação (eixo x), você encontrará rótulos que indicam o número total de saudação de solicitações e o número de saudação de solicitações que resultou em um código de status 404 não encontrado.

Diretamente abaixo do gráfico de barras hello, Olá informações a seguir será listado para principais ativos solicitados 250 Olá: caminho relativo (incluindo o nome de arquivo), número de saudação de solicitações que resultou em um 404 não encontrado código de status, número total de saudação de vezes que Olá ativo: solicitada e Olá porcentagem de solicitações que resultou em um código de status 404 não encontrado.

## <a name="see-also"></a>Consulte também
* [Visão geral da CDN do Azure](cdn-overview.md)
* [Estatísticas em tempo real na CDN do Microsoft Azure](cdn-real-time-stats.md)
* [Substituindo o comportamento HTTP padrão usando o mecanismo de regras de saudação](cdn-rules-engine.md)
* [Analisar o desempenho de borda](cdn-edge-performance.md)

