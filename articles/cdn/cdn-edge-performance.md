---
title: "desempenho de nó de borda aaaAnalyze no Azure CDN | Microsoft Docs"
description: "Analisar o desempenho do nó de borda no CDN do Microsoft Azure Análise de desempenho de borda fornece informações granular tráfego e largura de banda do uso de saudação CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 8cc596a7-3e01-4f76-af7b-a05a1421517e
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 35361d1c5e27fc6b8536c29e33c2ed217ee4d17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-edge-node-performance-in-microsoft-azure-cdn"></a>Analisar o desempenho do nó de borda no CDN do Microsoft Azure
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a>Visão geral
Análise de desempenho de borda fornece informações granular tráfego e largura de banda do uso de saudação CDN. Essas informações podem ser usadas toogenerate tendências estatísticas, que permitem que você toogain informações sobre como seus ativos estão sendo armazenados em cache e entregue tooyour clientes. Por sua vez, isso permite que tooform uma estratégia em como toooptimize saudação de seu conteúdo e toodetermine quais problemas de fornecimento deve ser resolvidos toobetter aproveite Olá CDN. Como resultado, não apenas você será capaz de tooimprove desempenho de entrega de dados, mas você também poderá ser capaz de tooreduce os custos CDN.

> [!NOTE]
> Todos os relatórios usam notação UTC/GMT, ao especificar um valor de data/hora.
> 
> 

## <a name="reports-and-log-collection"></a>Coleta de logs e relatórios
Dados de atividade CDN devem ser coletados pelo módulo de análise de desempenho de borda Olá antes que ele pode gerar relatórios sobre ele. O processo de coleta ocorre uma vez por dia e abrange a atividade de saudação que ocorreu durante a saudação dia anterior. Isso significa que estatísticas do relatório representam uma amostra das estatísticas do dia Olá momento Olá ele foi processado e não necessariamente conter o conjunto de dados para Olá completo Olá dia atual. a função primária Hello desses relatórios é tooassess desempenho. Eles não devem ser usados para fins de cobrança ou estatísticas numéricas exatas.

> [!NOTE]
> dados brutos de saudação do qual são gerados relatórios de análise de desempenho de borda estão disponíveis pelo menos de 90 dias.
> 
> 

## <a name="dashboard"></a>Painel
Painel de análise de desempenho de borda de saudação controla o tráfego CDN atual e histórico por meio de um gráfico e estatísticas. Use este painel toodetect recente longo prazo as tendências e no desempenho de saudação do tráfego CDN para sua conta.

Este painel consiste em:

* Um gráfico interativo que permite a visualização de saudação de métricas-chave e tendências.
* Uma linha do tempo que fornece uma noção dos padrões de longo prazo das principais tendências e métricas.
* As principais métricas e informações estatísticas sobre como nossa rede CDN melhora o tráfego do site, conforme medido pelo desempenho, uso e a eficiência geral.

### <a name="accessing-hello-edge-performance-dashboard"></a>Acessando o painel de desempenho de borda Olá
1. Na folha de perfil CDN hello, clique em Olá **gerenciar** botão.
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    portal de gerenciamento de CDN Olá é aberto.
2. Passe o mouse sobre Olá **análise** guia, em seguida, passe o mouse sobre Olá **análise de desempenho de borda** flutuante.  Clique em **Painel**.
   
    Painel de análise do nó de borda de saudação é exibida.

### <a name="chart"></a>Gráfico
painel Olá contém um gráfico que acompanha uma métrica sobre Olá período de tempo selecionado na linha de tempo de saudação que aparece diretamente abaixo dele.  Uma linha de tempo que representa graficamente a toohello últimos dois anos de atividade CDN é exibida diretamente abaixo gráfico hello.

#### <a name="using-hello-chart"></a>Usando o gráfico de saudação
* Por padrão, será possível no gráfico a taxa de eficiência de cache Olá para Olá últimos 30 dias.
* Este gráfico é gerado diariamente a partir de dados agrupados.
* Passar o mouse sobre um dia no gráfico de linha de saudação indica um valor de data e saudação da métrica de saudação nessa data.
* Clique nos finais de semana realçar tootoggle uma sobreposição de luz barras verticais cinzas que representam os finais de semana em um gráfico de saudação. Esse tipo de sobreposição é útil para identificar padrões de tráfego nos finais de semana.
* Clique em Exibir um ano atrás tootoggle uma sobreposição da saudação anterior a atividade do ano sobre Olá mesmo período no gráfico de saudação. Esse tipo de comparação fornece informações sobre padrões de uso CDN a longo prazo. canto de superior direito de saudação do gráfico de saudação contém uma legenda que indica o código de cor Olá para cada gráfico de linha.

#### <a name="updating-hello-chart"></a>Atualizando o gráfico de saudação
* Intervalo de tempo: Execute uma das seguintes hello:
  * Selecione a região desejada Olá na linha de tempo de hello. Olá gráfico será atualizado com os dados que corresponde a toohello período de tempo selecionado.
  * Clique duas vezes em Olá gráfico toodisplay todos os dados históricos disponíveis tooa máximo de dois anos.
* Métrica: Clique ícone de gráfico de saudação que aparece próxima métrica de toohello desejado. gráfico de saudação e linha do tempo de saudação serão atualizados com dados de métrica de saudação correspondente.

### <a name="key-metrics-and-statistics"></a>Principais métricas e estatísticas
#### <a name="efficiency-metrics"></a>Métricas de eficiência
Olá finalidade essas métricas é toosee se é possível melhorar a eficiência do cache. Olá principais benefícios derivados da eficiência de cache são:

* Carga reduzida no servidor de origem de saudação que pode levar a:
  * Um melhor desempenho do servidor principal
  * Redução dos custos operacionais.
* Melhor aceleração de entrega de dados desde que mais solicitações serão servidas diretamente do hello CDN.

| Campo | Descrição |
| --- | --- |
| Eficiência de cache |Indica a porcentagem de saudação de dados transferidos que foi servida do cache. Essa métrica medidas quando uma versão em cache do hello solicitado conteúdo foi servido diretamente do hello CDN (servidores de borda) toorequesters (por exemplo, o navegador da web) |
| Taxa de acertos |Indica a porcentagem de saudação de solicitações que foram atendidas no cache. Essa métrica medidas quando uma versão em cache de saudação solicitou o conteúdo foi servido diretamente do hello CDN (servidores de borda) toorequesters (por exemplo, o navegador da web). |
| % de bytes remotos - Nenhuma configuração de cache |Indica a porcentagem de saudação do tráfego que foi fornecida de servidores de origem toohello CDN (servidores de borda) que não será em cache como resultado do recurso de desvio de Cache de saudação (mecanismo de regras de HTTP). |
| % de bytes remotos - Cache expirado |Indica a porcentagem de saudação do tráfego atendida a partir de servidores de origem toohello CDN (servidores de borda) como resultado de revalidação conteúda obsoleta. |

#### <a name="usage-metrics"></a>Métricas de uso
Olá finalidade essas métricas é tooprovide percepção Olá redução de custos medidas a seguir:

* Minimizar os custos operacionais por meio de saudação CDN.
* Reduzir as despesas com CDN por meio de eficiência de cache e compactação.

> [!NOTE]
> Números de volume de tráfego representam o tráfego que foi usado em cálculos de razões e porcentagens e pode mostrar apenas uma parte do tráfego total de saudação para clientes de alto volume.
> 
> 

| Campo | Descrição |
| --- | --- |
| Média de bytes enviados |Indica o número médio de saudação de bytes transferidos para cada solicitação servida do solicitante do toohello (servidores de borda) do hello CDN (por exemplo, o navegador da web). |
| Nenhuma taxa de byte de configuração de cache |Indica a porcentagem de saudação do tráfego servido Olá CDN (servidores de borda) toohello solicitante (por exemplo, o navegador da web) que não serão armazenadas cache devido toohello recurso de desvio de Cache. |
| Taxa de bytes compactados |Indica a porcentagem de saudação do tráfego enviado da saudação CDN (servidores de borda) toorequesters (por exemplo, o navegador da web) em um formato compactado. |
| Bytes de saída |Indica a quantidade de saudação de dados, em bytes, que foram entregues do solicitante do toohello (servidores de borda) do hello CDN (por exemplo, o navegador da web). |
| Bytes de entrada |Indica a quantidade de saudação de dados, em bytes enviados do solicitantes (por exemplo, o navegador da web) toohello CDN (servidores de borda). |
| Bytes remotos |Indica a quantidade de saudação de dados, em bytes enviados do atendimento ao cliente e CDN toohello de servidores de origem CDN (servidores de borda). |

#### <a name="performance-metrics"></a>Métricas de desempenho
Olá finalidade essas métricas é tootrack desempenho geral da CDN para o tráfego.

| Campo | Descrição |
| --- | --- |
| Taxa de transferência |Indica a taxa média de saudação no qual conteúdo foi transferido do solicitante de tooa CDN hello. |
| Duration |Indica o tempo médio de saudação, em milissegundos, que levou toodeliver um solicitante de tooa ativo (por exemplo, o navegador da web). |
| Taxa de solicitação compactada |Indica a porcentagem de saudação de ocorrências que foram entregues do solicitante do toohello (servidores de borda) do hello CDN (por exemplo, o navegador da web) em um formato compactado. |
| Taxa de erros 4xx |Indica a porcentagem de saudação de ocorrências de um código de status 4xx gerado. |
| Taxa de erros 5xx |Indica a porcentagem de saudação de ocorrências geradas pelo código de status 5xx. |
| Acertos |Indica o número de saudação de solicitações de conteúdo da CDN. |

#### <a name="secure-traffic-metrics"></a>Métricas de tráfego de segurança
Olá finalidade essas métricas é tootrack desempenho de CDN para tráfego HTTPS.

| Campo | Descrição |
| --- | --- |
| Eficiência de cache seguro |Indica a porcentagem de saudação de dados transferidos para solicitações HTTPS que foram atendidas do cache. Essa métrica mede quando uma versão em cache de saudação solicitado conteúdo foi servido diretamente do hello CDN (servidores de borda) toorequesters (por exemplo, o navegador da web) sobre HTTPS. |
| Taxa de transferência segura |Indica a taxa média de saudação no qual conteúdo foi transferido do hello CDN (servidores de borda) toorequesters (por exemplo, servidores web) via HTTPS. |
| Duração média segura |Indica o tempo médio de saudação, em milissegundos, necessário toodeliver um solicitante de tooa ativo (por exemplo, o navegador da web) sobre HTTPS. |
| Acertos seguros |Indica o número de saudação de solicitações HTTPS para conteúdo da CDN. |
| Bytes de saída seguros |Indica a quantidade de saudação do tráfego HTTPS, em bytes, que foram entregues do solicitante do toohello (servidores de borda) do hello CDN (por exemplo, o navegador da web). |

## <a name="reports"></a>Relatórios
Cada relatório neste módulo contém um gráfico e as estatísticas de uso de largura de banda e o tráfego para diferentes tipos de métricas (por exemplo, códigos de status HTTP, códigos de status do cache, solicitação de URL, etc.). Essas informações podem ser usada toodelve detalhes como o conteúdo está sendo atendido tooyour clientes e o desempenho de entrega do ajuste toofine CDN comportamento tooimprove dados.

### <a name="accessing-hello-edge-performance-reports"></a>Acessar relatórios de desempenho de borda Olá
1. Na folha de perfil CDN hello, clique em Olá **gerenciar** botão.
   
    ![botão gerenciar da folha Perfil CDN](./media/cdn-edge-performance/cdn-manage-btn.png)
   
    portal de gerenciamento de CDN Olá é aberto.
2. Passe o mouse sobre Olá **análise** guia, em seguida, passe o mouse sobre Olá **análise de desempenho de borda** flutuante.  Clique em **Objeto grande de HTTP**.
   
    tela de relatórios de análise do Hello borda nó é exibida.

| Relatório | Descrição |
| --- | --- |
| Resumo diário |Permite que você tooview tendências de tráfego diário em um período de tempo especificado. Cada barra no gráfico representa uma data específica. tamanho de Olá da barra de saudação indica o número total de saudação de ocorrências que ocorreram nessa data. |
| Resumo por hora |Permite que você tooview tendências de tráfego por hora por um período de tempo especificado. Cada barra no gráfico representa uma única hora em uma determinada data. tamanho de Olá da barra de saudação indica o número total de saudação de ocorrências que ocorreram durante essa hora. |
| Protocolos |Exibe a divisão de saudação do tráfego entre Olá HTTP e protocolos HTTPS. Um gráfico de rosca indica a porcentagem de saudação de ocorrências que ocorreram para cada tipo de protocolo. |
| Métodos HTTP |Permite que você tooget uma ideia de quais métodos HTTP estão sendo usado toorequest seus dados. Normalmente, os métodos de solicitação HTTP mais comuns Olá são GET, HEAD e POST. Um gráfico de rosca indica a porcentagem de saudação de ocorrências que ocorreram para cada tipo de método de solicitação HTTP. |
| URLs |Contém um gráfico que exibe o saudação top 10 solicitada URLs. É exibida uma barra para cada URL. altura de saudação da barra de saudação indica o número de ocorrências geradas pelo URL específica em um período de tempo de saudação coberto pelo relatório de saudação. Estatísticas de 100 principais de saudação solicitado que URLs são exibidos diretamente abaixo desse gráfico. |
| CNAMEs |Contém um gráfico que exibe Olá top 10 CNAMEs usados toorequest ativos ao longo do período de tempo de saudação de um relatório. Estatísticas de 100 principais de saudação solicitado que CNAMEs são exibidos diretamente abaixo desse gráfico. |
| Origens |Contém um gráfico que exibe o saudação 10 principais CDN ou cliente servidores de origem do qual os ativos foram solicitados por um período de tempo especificado. Estatísticas de 100 principais de saudação solicitado CDN ou cliente servidores de origem são exibidos diretamente abaixo desse gráfico. Servidores de origem do cliente são identificados por nome de saudação definido no hello opção de nome de diretório. |
| POPs geográficos |Mostra a quantidade do tráfego que está sendo roteado por meio de um determinado ponto-de-presença (POP). abreviação de três letras Olá representa um POP em nossa rede CDN. |
| Clientes |Contém um gráfico que exibe o saudação top 10 clientes solicitado ativos por um período de tempo especificado. Para fins de saudação deste relatório, todas as solicitações que se originam Olá mesmo endereço IP são considerados toobe de saudação mesmo cliente. Para clientes de 100 principais Olá são exibidas diretamente abaixo desse gráfico. Este relatório é útil para determinar os padrões de atividade de download para os principais clientes. |
| Status do Cache |Fornece uma análise detalhada do comportamento de cache, que pode revelar abordagens para melhorar Olá experiência geral do usuário final. Desde que o desempenho mais rápido Olá vierem de acertos do cache, você pode otimizar dados velocidades de entrega minimizar erros de cache e de acertos do cache expirada. |
| Detalhes NONE |Contém um gráfico que exibe o saudação top 10 URLs ativos para o qual a atualização de conteúdo de cache não foi verificada por um período de tempo especificado. Olá URLs de 100 principais para esses tipos de ativos são exibidas diretamente abaixo desse gráfico. |
| Detalhes CONFIG_NOCACHE |Contém um gráfico que exibe o saudação 10 principais URLs de ativos que não foram colocados no cache devido a configuração de CDN toohello do cliente. Esses tipos de recursos foram atendidos diretamente do servidor de origem de saudação. Olá URLs de 100 principais para esses tipos de ativos são exibidas diretamente abaixo desse gráfico. |
| Detalhes UNCACHEABLE |Contém um gráfico que exibe o saudação top 10 URLs ativos que pode não ser armazenado em cache devido a dados de cabeçalho toorequest. Olá URLs de 100 principais para esses tipos de ativos são exibidas diretamente abaixo desse gráfico. |
| Detalhes TCP_HIT |Contém um gráfico que exibe o saudação top 10 URLs de ativos que são atendidos imediatamente do cache. Olá URLs de 100 principais para esses tipos de ativos são exibidas diretamente abaixo desse gráfico. |
| Detalhes TCP_MISS |Contém um gráfico que exibe o saudação top 10 URLs de ativos que têm um status de cache de TCP_MISS. Olá URLs de 100 principais para esses tipos de ativos são exibidas diretamente abaixo desse gráfico. |
| Detalhes TCP_EXPIRED_HIT |Contém um gráfico que exibe o saudação top 10 URLs obsoletos ativos que foram fornecidas diretamente da saudação POP. Olá URLs de 100 principais para esses tipos de ativos são exibidas diretamente abaixo desse gráfico. |
| Detalhes TCP_EXPIRED_MISS |Contém um gráfico que exibe o saudação top 10 URLs obsoletos ativos para o qual uma nova versão tinha toobe recuperado do servidor de origem de saudação. Olá URLs de 100 principais para esses tipos de ativos são exibidas diretamente abaixo desse gráfico. |
| Detalhes TCP_CLIENT_REFRESH_MISS |Contém um gráfico de barras que exibe o saudação top 10 URLs para ativos foram recuperados de um servidor de origem devido a solicitação do tooa sem cache de cliente de saudação. Olá URLs de 100 principais para esses tipos de solicitações são exibidas diretamente abaixo deste gráfico. |
| Tipos de solicitação do cliente |Indica o tipo de saudação de solicitações feitas por clientes HTTP (por exemplo, navegadores). Este relatório inclui um gráfico de rosca que fornece uma noção como toohow solicitações estão sendo tratadas. Informações de largura de banda e o tráfego para cada tipo de solicitação são exibidas abaixo do gráfico de saudação. |
| Agente do usuário |Contém um gráfico de barras exibindo toorequest de agentes de usuário 10 principais Olá seu conteúdo por meio de nosso CDN. Normalmente, um agente de usuário é um navegador da web, media player ou um navegador do celular. Para agentes de usuário 100 principais Olá são exibidas diretamente abaixo deste gráfico. |
| Referenciadores |Contém um gráfico de barras exibindo Olá principais referenciadores 10 toocontent acessado por meio de nosso CDN. Normalmente, uma referência é Olá URL de página da web de saudação ou recurso que vincula tooyour conteúdo. Informações detalhadas são fornecidas abaixo gráfico Olá para Referenciadores de 100 principais hello. |
| Tipos de compressão |Contém um gráfico de rosca que divide os ativos solicitados entre os que foram e os que não foram compactados nos nossos servidores de borda. Porcentagem de saudação de ativos compactados é dividida por tipo de saudação de compactação usado. Informações detalhadas são fornecidas abaixo gráfico Olá para cada tipo de compactação e o status. |
| Tipos de arquivo |Contém um gráfico de barras que exibe Olá top 10 tipos de arquivos que foram solicitados por meio de nosso CDN para sua conta. Para fins de saudação deste relatório, um tipo de arquivo é definido pela extensão de nome de arquivo do ativo hello e tipo de mídia da Internet (por exemplo,. HTML \[texto/html\],. htm \[texto/html\],. aspx \[detexto/html\], etc.). Informações detalhadas são fornecidas abaixo gráfico Olá Olá top 100 para tipos de arquivo. |
| Arquivos exclusivos |Contém um gráfico que plota o número total de saudação de ativos exclusivos que foram solicitados em um determinado dia em um período de tempo especificado. |
| Resumo de autenticação de token |Contém um gráfico de pizza que fornece uma visão geral sobre se ativos solicitados foram protegidos pela autenticação baseada em Token. Ativos protegidos são exibidos no gráfico de saudação de acordo com o toohello resultados de sua tentativa autenticação. |
| Detalhes da autenticação de token negada |Contém um gráfico de barras que permite que você tooview Olá top 10 solicitações que foram negadas devido a autenticação baseada em tooToken. |
| Códigos de resposta HTTP |Fornece uma análise dos códigos de status HTTP da saudação (por exemplo, 200 Okey, 403 Proibido, 404 não encontrado, etc.) que foram entregues tooyour HTTP clientes por nossos servidores de borda. Um gráfico de pizza permite tooquickly avaliar como seus ativos foram atendidos. Dados de estatísticas detalhados são fornecidos para cada código de resposta abaixo gráfico hello. |
| Erros 404 |Contém um gráfico de barras que permite que você tooview Olá top 10 solicitações que resultaram em um código de resposta 404 não encontrado. |
| Erros 403 |Contém um gráfico de barras que permite que você tooview Olá top 10 solicitações que resultaram em um código de resposta 403 Proibido. Um código de resposta 403 Forbidden ocorre quando uma solicitação for negada por um servidor de origem do cliente ou um servidor de borda em nosso POP. |
| Erros 4xx |Contém um gráfico de barras que permite que você tooview Olá top 10 solicitações que resultaram em um código de resposta no intervalo de 400 hello. Os códigos de resposta 403 Not Found e 404 Forbidden não estão incluídos neste relatório. Normalmente, um código de resposta 4xx ocorre quando uma solicitação for negada devido a um erro do cliente. |
| Erros 504 |Contém um gráfico de barras que permite que você tooview Olá top 10 solicitações que resultaram em um código de resposta de tempo limite do Gateway 504. Um código de resposta de tempo limite do Gateway 504 ocorre quando um tempo limite ocorre quando um proxy HTTP está tentando toocommunicate com outro servidor. No caso de saudação do nosso CDN, um código de resposta de tempo limite do Gateway 504 normalmente ocorre quando um servidor de borda é tooestablish não é possível a comunicação com um servidor de origem do cliente. |
| Erros 502 |Contém um gráfico de barras que permite que você tooview Olá top 10 solicitações que resultaram em um código de resposta 502 Gateway incorreto. Um código de resposta 502 Bad Gateway ocorre quando ocorre uma falha de protocolo HTTP entre um servidor e um proxy HTTP. No caso de saudação do nosso CDN, um código de resposta 502 Gateway incorreto normalmente ocorre quando um servidor de origem do cliente retorna um servidor de borda tooan resposta inválida. Uma resposta é inválida, se ela não pode ser analisada ou se está incompleta. |
| Erros 5xx |Contém um gráfico de barras que permite que você tooview Olá top 10 solicitações que resultaram em um código de resposta no intervalo de 500 hello.  Os códigos de resposta 502 Bad Gateway e 504 Gateway Timeout não estão incluídos no relatório. |

## <a name="see-also"></a>Consulte também
* [Visão geral da CDN do Azure](cdn-overview.md)
* [Estatísticas em tempo real na CDN do Microsoft Azure](cdn-real-time-stats.md)
* [Substituindo o comportamento HTTP padrão usando o mecanismo de regras de saudação](cdn-rules-engine.md)
* [Relatórios avançados de HTTP](cdn-advanced-http-reports.md)

