---
title: "conjuntos de dados de exemplo hello de aaaUse no estúdio de aprendizado de máquina | Microsoft Docs"
description: "Descrições de saudação conjuntos de dados usados em modelos de exemplo incluídos no estúdio de aprendizado de máquina. É possível usar esses conjuntos de dados de exemplo para seus testes."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 03a0b844-e8a7-4896-996f-d3c7a0db7a50
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: c7786478db82d40aaf27c37b3947ded5f042dd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-sample-datasets-in-azure-machine-learning-studio"></a>Usar conjuntos de dados de exemplo hello no estúdio de aprendizado de máquina do Azure
[top]: #machine-learning-sample-datasets

Ao criar um novo espaço de trabalho no Azure Machine Learning, diversos conjuntos de dados de exemplo e testes são incluídos por padrão. Muitos desses conjuntos de dados de exemplo são usados pelos modelos de exemplo hello em Olá [Galeria do Azure Cortana Intelligence](http://gallery.cortanaintelligence.com/). Outros são incluídos como exemplos de vários tipos de dados usados no aprendizado de máquina.

Alguns desses conjuntos de dados estão disponíveis no armazenamento de Blobs do Azure. Para esses conjuntos de dados, Olá a tabela a seguir fornece um link direto. Você pode usar esses conjuntos de dados em suas experiências usando Olá [importar dados] [ import-data] módulo.

Olá outros esses conjuntos de dados de exemplo estão disponíveis no espaço de trabalho em **conjuntos de dados salvos** na esquerda do hello módulo paleta toohello da tela de experimento hello quando você abrir ou criar um novo teste no estúdio de aprendizado de máquina.
Você pode usar qualquer um desses conjuntos de dados em sua própria experiência arrastando-a tela de experimento tooyour.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<table>

<tr>
  <th align=left>Nome do conjunto de dados</th>
  <th align=left>Descrição do conjunto de dados</th>
</tr>

<tr>
  <td valign=top>Conjunto de dados de classificação binária de receita no recenseamento adulto</td>
  <td valign=top>
Um subconjunto do banco de dados de censo Olá 1994, usando o trabalho adultos idade de saudação de 16 com um índice de renda ajustada > 100.<p> </p><b>Uso:</b> classificar as pessoas que usam dados demográficos toopredict se uma pessoa ganha mais de 50 mil por ano.<p> </p><b>Pesquisa relacionada:</b> Kohavi, R., Becker, B., (1996). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr ID=airport-codes-dataset>
  <td valign=top>Conjunto de dados de códigos do aeroporto</td>
  <td valign=top>
Códigos de aeroporto dos EUA.<p> </p>Este conjunto de dados contém uma linha para cada aeroporto dos EUA, fornecendo o número de identificação do aeroporto de saudação e nome junto com hello local cidade e estado.
  </td>
</tr>

<tr>
  <td valign=top>Dados de preço de automóvel (Brutos)</td>
  <td valign=top>
Informações sobre automóveis por marca e modelo, incluindo preço hello, recursos, como o número de saudação de cilindros e MPG, bem como uma pontuação de risco de seguros.<p> </p>pontuação de risco Olá inicialmente associado com preço automática e, em seguida, ajustada para risco real em um processo conhecido tooactuaries como symboling. Um valor de + 3 indica que o auto Olá é arriscado, e um valor de -3 que ele provavelmente é seguro.<p> </p><b>Uso:</b> pontuação de risco Olá prever por recursos, usando a classificação de regressão ou multivariada. <p> </p><b>Pesquisa relacionada:</b> Schlimmer, J.C. (1987). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr ID=bike-rental-uci-dataset>
  <td valign=top>Conjunto de dados UCI de locação de bicicletas</td>
  <td valign=top>
Conjunto de dados UCI Bike Rental que é baseado em dados reais da empresa Capital Bikeshare que mantém uma rede de aluguel de bicicletas em Washington DC.<p> </p>saudação de conjunto de dados tem uma linha para cada hora do dia em 2011 e 2012, para um total de 17,379 linhas. intervalo de saudação de locações de bicicleta por hora é de 1 too977.

  </td>
</tr>

<tr ID=bill-gates-rgb-image>
  <td valign=top>Imagem RGB de Bil Gates</td>
  <td valign=top>
Converter o arquivo de imagem disponível publicamente tooCSV dados.<p> </p>Olá código para converter a imagem de saudação é fornecido no hello <strong>usando clustering K-Means de quantização de cor</strong> página de detalhes do modelo.
  </td>
</tr>

<tr>
  <td valign=top>Dados de doação de sangue</td>
  <td valign=top>
Um subconjunto dos dados do banco de dados de doadores de sangue a Olá do hello sangue Transfusion serviço Central do Hsin Chu cidade, Taiwan.<p> </p>Dados de doadores incluem meses Olá desde a última doação) e frequência, ou número total de saudação do doações, tempo desde a última doação e quantidade de sangue doada.<p> </p><b>Uso:</b> meta Olá é toopredict por meio de classificação se Doadores Olá doada sangue em março de 2007, em que 1 indica um patrocinador durante o período de destino hello e 0 um não Doadores. <p> </p><b>Pesquisa relacionada:</b> Yeh, I.C., (2008). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  <p> </p>Yeh, I-Cheng, Yang, King-Jang, e Ting, Tao-Ming, "Knowledge discovery on RFM model using Bernoulli sequence, "Expert Systems with Applications, 2008, <a href="http://dx.doi.org/10.1016/j.eswa.2008.07.018">http://dx.doi.org/10.1016/j.eswa.2008.07.018</a>
  </td>
</tr>

<tr ID=book-reviews-from-amazon>
  <td valign=top>Resenhas de livros da Amazon</td>
  <td valign=top>
Revisões de livros Amazon, obtido site amazon.com de saudação por pesquisadores da Universidade de janeiro (<a href="http://www.cs.jhu.edu/~mdredze/datasets/sentiment/">sentimento</a>). Consulte o artigo de pesquisa hello, "biografias, Bollywood, caixas de explosão e liquidificadores: domínio adaptação a classificação de sentimento" John Blitzer, Mark Dredze e Fernando Pereira; Associação de linguística computacional (ACL) 2007.<p> </p>conjunto de dados original Olá tem revisões 975K com classificações 1, 2, 3, 4 ou 5. Olá revisões foram gravadas em inglês e são do hello 1997-2007 do período de tempo. Este conjunto de dados tiver sido convertidos too10K revisões.
  </td>
</tr>

<tr>
  <td valign=top>Dados de câncer de mama</td>
  <td valign=top>
Um dos três relacionados câncer de conjuntos de dados fornecidos pelo Olá Institute oncológicas que aparece com frequência na literatura de aprendizado de máquina. Ele combina informações de diagnóstico com recursos de análise de laboratório de aproximadamente 300 amostras de tecido.<p> </p><b>Uso:</b> classificar o tipo de saudação do câncer, com base em atributos de 9, alguns dos quais são lineares e alguns são categóricas. <p> </p><b>Pesquisa relacionada:</b> Wohlberg, W.H., Street, W.N., & Mangasarian, O.L. (1995). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr ID=breast-cancer-features>
  <td valign=top>Recursos de câncer de mama <td valign=top>
saudação de conjunto de dados contém informações de 102K suspeitas regiões (candidatos) de imagens de raio x, cada descrito pelos 117 recursos. recursos de saudação são de propriedade e seu significado não seja revelado por criadores de conjunto de dados da saudação (Siemens saúde). 
  </td>
</tr>

<tr ID=breast-cancer-info>
  <td valign=top>Informações de Câncer de Mama</td>
  <td valign=top>
saudação de conjunto de dados contém informações adicionais para cada região suspeita da imagem de raio x. Cada exemplo fornece informações (por exemplo, rótulo, pacientes ID, as coordenadas da imagem inteira do patch toohello relativo) sobre o número de linha correspondente Olá no conjunto de dados de recursos de câncer de mama hello. Cada paciente tem um número de exemplos. Para pacientes que têm um câncer, alguns exemplos são positivos e outros negativos. Para pacientes que não têm câncer, todos os exemplos são negativos. Olá dataset tem exemplos 102K. saudação de conjunto de dados é mais adequado, 0,6% de pontos de saudação são positivo, negativo rest hello. saudação de conjunto de dados foi disponibilizado por saúde Siemens.
  </td>
</tr>

<tr ID=crm-appetency-labels-shared>
  <td valign=top>Rótulos de apetência CRM compartilhados</td>
  <td valign=top>
Os rótulos de desafio de previsão de relação de cliente Olá KDD Cup 2009 (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_appetency.labels">orange_small_train_appetency.labels</a>).
  </td>
</tr>

<tr ID=crm-churn-labels-shared>
  <td valign=top>Rótulos de variação CRM compartilhados</td>
  <td valign=top>
Os rótulos de desafio de previsão de relação de cliente Olá KDD Cup 2009 (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_churn.labels">orange_small_train_churn.labels</a>).
  </td>
</tr>

<tr ID=crm-dataset-shared>
  <td valign=top>Conjunto de dados CRM compartilhado</td>
  <td valign=top>
Esses dados vêm de desafio de previsão de relação de cliente Olá KDD Cup 2009 (<a href="http://www.sigkdd.org/kdd-cup-2009-customer-relationship-prediction - orange_small_train.data.zip">orange_small_train.data.zip</a>).<p> </p>saudação de conjunto de dados contém 50 mil clientes de saudação da empresa de telecomunicações francês laranja. Cada cliente possui 230 recursos anônimos, dos quais 190 são numéricos e 40 categóricos. recursos de saudação são muito esparsos.
  </td>
</tr>

<tr ID=crm-upselling-labels-shared>
  <td valign=top>Rótulos de vendas agregadas CRM compartilhados</td>
  <td valign=top>
Os rótulos de desafio de previsão de relação de cliente Olá KDD Cup 2009 (<a href="http://www.sigkdd.org/site/2009/files/orange_large_train_upselling.labels">orange_large_train_upselling.labels</a>).
  </td>
</tr>

<tr>
  <td valign=top>Dados de regressão de eficiência de energia</td>
  <td valign=top>
Uma coleção de perfis de energia simulados, com base em 12 formatos de construções diferentes. construções de saudação são diferenciadas por 8 recursos, como glazing área, Olá glazing distribuição área e orientação.<p> </p><b>Uso:</b> usar classificação ou regressão toopredict Olá eficiência de energia com base como uma das duas respostas real com valor de classificação. Para classificação de várias classes, é redondo Olá resposta variável toohello inteiro mais próximo. <p> </p><b>Pesquisa relacionada:</b> Xifara, A. & Tsanas, A. (2012). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr ID=flight-delays-data>
  <td valign=top>Dados de atrasos de voo</td>
  <td valign=top>
Flight passageiro em tempo de dados de desempenho obtidos Olá TranStats coleta de dados de saudação dos EUA Departamento de Transportes dos EUA (<a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">On-Time</a>).<p> </p>saudação de conjunto de dados abrange Olá período abril – outubro de 2013. Antes de carregar tooAzure estúdio de aprendizado de máquina, conjunto de dados de saudação foi processado da seguinte maneira:<ul><li>saudação de conjunto de dados foi filtrado toocover somente Olá 70 mais ocupados aeroportos continental Olá dos EUA</li><li>Os voos cancelados foram rotulados como atrasados por mais de 15 minutos</li><li>Voos desviados foram retirados.</li><li>Olá colunas a seguir foram selecionadas: ano, mês, DayofMonth, DayOfWeek, da operadora, OriginAirportID, DestAirportID, CRSDepTime, DepDelay, DepDel15, CRSArrTime, ArrDelay, ArrDel15, cancelado</li></ul>
</td>
</tr>

<tr>
  <td valign=top>Desempenho pontual de voo (Bruto)</td>
  <td valign=top>
Registros de pousos e decolagens nos Estados Unidos desde outubro de 2011.<p> </p><b>Uso:</b> prever atrasos nos voos. <p> </p><b>Pesquisa relacionada:</b> do Departamento de Transportes dos EUA <a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time</a>.
  </td>
</tr>

<tr>
  <td valign=top>Dados de incêndios florestais</td>
  <td valign=top>
Contém dados meteorológicos, como índices de temperatura e umidade e velocidade do vento, de uma área no nordeste de Portugal, combinados com registros de incêndios florestais.<p> </p><b>Uso:</b> é uma tarefa difícil de regressão, onde aim Olá Olá toopredict gravado área da floresta acionado. <p> </p><b>Pesquisa relacionada:</b> Cortez, P., & Morais, A. (2008). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  <p> </p>[Cortez and Morais, 2007] P. Cortez and A. Morais. Uma abordagem de mineração de dados tooPredict acionado de floresta usando meteorológicas por dados. Em J. Neves, M. F. Santos e J. Machado Eds., novas tendências em inteligência Artificial, procedimentos de Olá 13 EPIA 2007 - português conferência em inteligência Artificial, dezembro, Guimarães, Portugal páginas 512-523, 2007. APPIA, ISBN-13 978-989-95618-0-9. Disponível em: <a href="http://www.dsi.uminho.pt/~pcortez/fires.pdf">http://www.dsi.uminho.pt/~pcortez/fires.pdf</a>.
  </td>
</tr>

<tr ID=german-credit-card-uci-dataset>
  <td valign=top>Conjunto de dados do cartão de crédito alemão UCI</td>
  <td valign=top>
Olá conjunto de dados UCI Statlog (cartão de crédito alemão) (<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">Statlog + alemão + crédito + dados</a>), usando o arquivo de german.data hello.<p> </p>conjunto de dados Olá classifica pessoas, descritas por um conjunto de atributos, como riscos de crédito baixa ou alta. Cada exemplo representa uma pessoa. Há 20 recursos, numéricos e categóricos e um rótulo de binário (valor de risco de crédito Olá). Entradas de risco de crédito alto têm o rótulo = 2, entradas de risco de crédito baixo têm o rótulo = 1. Olá custo classifique um exemplo de baixo risco como alta é 1, enquanto o custo de saudação do classifique um exemplo de alto risco como baixa é 5.
  </td>
</tr>

<tr ID=imdb-movie-titles>
  <td valign=top>Títulos de filmes no IMDB</td>
  <td valign=top>
Olá, conjunto de dados contém informações sobre que foram classificados no Twitter tweets filmes: IMDB ID de filme, o nome do filme, gênero e ano de produção. Há 17K filmes no conjunto de dados de saudação. saudação de conjunto de dados foi introduzido no papel de hello "S. Dooms, T. De Pessemier e L. Martens. MovieTweetings: um conjunto de dados de classificação de filmes coletado do Twitter. Oficina de crowdsourcing and computação humana para sistemas recomendados, CrowdRec em RecSys 2013."
  </td>
</tr>

<tr>
  <td valign=top>Dados da íris classe dois</td>
  <td valign=top>
Essa é talvez Olá toobe do banco de dados mais conhecida encontrado na literatura de reconhecimento de padrão de saudação. saudação de conjunto de dados é relativamente pequeno, que contém 50 exemplos cada medidas pétala de três tipos de íris.<p> </p><b>Uso:</b> prever Olá íris tipo de medidas de saudação.  <p> </p><b>Pesquisa relacionada:</b> Fisher, R.A. (1988). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr ID=movie-tweets>
  <td valign=top>Tweets de Filmes</td>
  <td valign=top>
saudação de conjunto de dados é uma versão estendida do conjunto de dados de filme Tweetings hello. saudação de conjunto de dados tem as classificações de 170K de filmes, extraídos de tweets bem estruturados no Twitter. Cada instância representa uma tweet e é uma tupla: ID de usuário, ID de filme IMDB, classificação, carimbo de hora, número de Favoritos para este tweet e número de retweets desse tweet. saudação de conjunto de dados foi disponibilizado por diz-A., Dooms S., B. Loni e D. Tikk para sistemas de recomendação de desafio de 2014.
  </td>
</tr>

<tr>
  <td valign=top>Dados MPG para vários automóveis</td>
  <td valign=top>
Este conjunto de dados é uma versão ligeiramente modificada do conjunto de dados Olá fornecida pela biblioteca de StatLib de saudação do Carnegie Mellon University. saudação de conjunto de dados foi usado no hello 1983 American feira estatística de associação.<p> </p>dados de saudação listarem consumo de combustível para vários automóveis no consumo, juntamente com informações, como o número de cilindros, deslocamento de mecanismo, potência, peso total e aceleração de saudação.<p> </p><b>Uso:</b> prever a economia de combustível com base em 3 atributos discretos de múltiplos valores e 5 atributos contínuos. <p> </p><b>Pesquisa relacionada:</b> StatLib, Carnegie Mellon University, (1993). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr>
  <td valign=top>Conjunto de dados de classificação binária de diabetes da população indiana de Pima</td>
  <td valign=top>
Um subconjunto de dados do banco de dados Instituto Nacional de Diabetes e Digestive e piscina infecciosas hello. saudação de conjunto de dados foi filtrado toofocus em feminino pacientes de herança indiano Pima. dados de saudação incluem dados médicos como glicose e níveis de insulin, bem como fatores de estilo de vida.<p> </p><b>Uso:</b> prever se o assunto Olá tem diabetes (classificação binária). <p> </p><b>Pesquisa relacionada:</b> Sigillito, V. (1990). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml"</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr>
  <td valign=top>Dados de consumidores de restaurantes</td>
  <td valign=top>
Um conjunto de metadados sobre consumidores, incluindo demografia e preferências.<p> </p><b>Uso:</b> usar este conjunto de dados, em combinação com hello outros dois restaurante conjuntos de dados, tootrain e testar um sistema de recomendação. <p> </p><b>Pesquisa relacionada:</b> Bache, K. e Lichman, M. (2013). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science.
  </td>
</tr>

<tr>
  <td valign=top>Dados de recurso de restaurante</td>
  <td valign=top>
Um conjunto de metadados sobre restaurantes e seus recursos, como tipo de comida, estilo de jantar e localização.<p> </p><b>Uso:</b> usar este conjunto de dados, em combinação com hello outros dois restaurante conjuntos de dados, tootrain e testar um sistema de recomendação. <p> </p><b>Pesquisa relacionada:</b> Bache, K. e Lichman, M. (2013). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science.
  </td>
</tr>

<tr>
  <td valign=top>Classificação de restaurantes</td>
  <td valign=top>
Contém classificações fornecidas pelos usuários toorestaurants em uma escala de 0 too2.<p> </p><b>Uso:</b> usar este conjunto de dados, em combinação com hello outros dois restaurante conjuntos de dados, tootrain e testar um sistema de recomendação. <p> </p><b>Pesquisa relacionada:</b> Bache, K. e Lichman, M. (2013). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science.
  </td>
</tr>

<tr>
  <td valign=top>Conjunto de dados multiclasses de recozimento de aço</td>
  <td valign=top>
Este conjunto de dados contém uma série de registros de aço recozimento avaliações com atributos físicos de saudação (largura, espessura, tipos de tipo (bobina, planilha, etc.) do hello resultante aço.<p> </p><b>Uso:</b> prever um dos dois atributos de classe numérica: resistência ou força. Você também pode analisar correlações entre os atributos.<p> </p>Os graus de aço seguem um padrão definido pela SAE e outras organizações. Está procurando uma determinada 'classificação de (variável de classe Olá) e quiser toounderstand Olá valores necessários. <p> </p><b>Pesquisa relacionada:</b> Sterling, D. & Buntine, W. (NA). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  <p> </p>Notas de toosteel um guia útil podem ser encontradas aqui: <a href="http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf">http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf</a>
  </td>
</tr>

<tr>
  <td valign=top>Dados de telescópio</td>
  <td valign=top>
Registros de explosões de partículas gama de alta energia com ruídos de fundo, ambos simulados usando o processo de Monte Carlo.<p> </p>intenção de saudação de simulação de saudação foi tooimprove precisão de saudação com base em zero atmosféricas Cherenkov gama telescopes, usando métodos estatísticos toodifferentiate entre o sinal desejado da saudação (Cherenkov radiação Pancadas de chuva) e ruídos de fundo (hadronic Pancadas de chuva iniciadas por raios cósmicos em Olá superior atmosfera).<p> </p>Olá dados foram toocreate pré-processada um cluster alongado com eixo de tempo de saudação é orientado para o Centro de câmera hello. características de saudação dessa elipse (geralmente chamados de parâmetros Hillas) estão entre parâmetros de imagem de saudação que podem ser usados para distinção.<p> </p><b>Uso:</b> prever se a imagem de um chuveiro representa ruído de fundo ou sinal.<p> </p><b>Observações:</b> a precisão da classificação simples não é significativa para esses dados, já que classificar um evento de fundo como sinal é pior do que classificar um evento de sinal como de fundo. Para comparação de classificadores diferentes gráfico ROC Olá deve ser usado. Olá probabilidade de aceitar um evento de plano de fundo como sinal deve ser abaixo de um Olá limites a seguir: 0,01, 0,02, 0,05, 0,1 ou 0,2.<p> </p>Além disso, observe que o número de saudação de eventos em segundo plano (h, para Pancadas de chuva hadronic) é subestimado, enquanto em medidas reais, Olá h ou ruído classe representa a maioria de saudação de eventos. <p> </p><b>Pesquisa relacionada:</b> Bock, R.K. (1995). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information </td>
</tr>

<tr ID=weather-dataset>
  <td valign=top>Conjunto de dados de clima</td>
  <td valign=top>
Observações de Terra com base no tempo por hora de NOAA (<a href="http://cdo.ncdc.noaa.gov/qclcd_ascii/, merged data from 201304 too201310">mescladas de dados de too201310 201304</a>).<p> </p>os dados de clima Olá abrange observações feitas do aeroporto clima estações, abrangendo Olá período abril – outubro de 2013. Antes de carregar tooAzure estúdio de aprendizado de máquina, conjunto de dados de saudação foi processado da seguinte maneira:<ul><li>IDs de estação de clima foram mapeadas toocorresponding aeroporto IDs</li><li>Estações de clima não associadas aos aeroportos de mais ocupados 70 Olá foram filtradas</li><li>coluna de data Olá foi dividida em colunas separadas de ano, mês e dia</li><li>Olá colunas a seguir foram selecionadas: AirportID, ano, mês, dia, hora, fuso horário, SkyCondition, visibilidade, WeatherType, DryBulbFarenheit, DryBulbCelsius, WetBulbFarenheit, WetBulbCelsius, DewPointFarenheit, DewPointCelsius, RelativeHumidity, WindSpeed, WindDirection, ValueForWindCharacter, StationPressure, PressureTendency, PressureChange, SeaLevelPressure, RecordType, HourlyPrecip, altímetro</li></ul>
  </td>
</tr>

<tr ID=wikipedia-sp-500-dataset>
  <td valign=top>Conjunto de dados da SP 500 da Wikipédia</td>
  <td valign=top>
Os dados foram extraídos do Wikipedia (<a href="http://www.wikipedia.org/">http://www.wikipedia.org/</a>), com base em artigos de cada empresa S&P 500, armazenados como dados XML.<p> </p>Antes de carregar tooAzure estúdio de aprendizado de máquina, conjunto de dados de saudação foi processado da seguinte maneira:<ul><li>Extraia o conteúdo do texto para cada empresa específica</li><li>Remova a formatação wiki</li><li>Remova caracteres não alfanuméricos</li><li>Converter todos os toolowercase de texto</li><li>Categorias de empresas conhecidas foram adicionadas</li></ul><p> </p>Observe que algumas empresas para um artigo não pôde ser encontrado, portanto, número de saudação de registros é menor que 500.
  </td>
</tr>





<tr ID=direct-marketing>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/direct_marketing.csv">direct_marketing.csv</a></td>
  <td valign=top>
saudação de conjunto de dados contém os dados do cliente e indicações sobre sua campanha de mala direta resposta tooa direto. Cada linha representa um cliente. Olá, conjunto de dados contém 9 recursos sobre dados demográficos do usuário e depois do comportamento e 3 colunas de rótulo (visite conversão e o gasto).  Visite é uma coluna binária que indica que um cliente visitado depois hello campanha de marketing, conversão indica que um cliente adquiriu algo e gastar é a quantidade de saudação que foi gasto.  saudação de conjunto de dados foi disponibilizado por Kevin Hillstrom para MineThatData email análise e Data Mining desafio.
  </td>
</tr>

<tr ID=lyrl2004-tokens-test>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_test.csv">lyrl2004_tokens_test.csv</a></td>
  <td valign=top>
Recursos dos exemplos de teste no conjunto de dados de notícias do hello Reuters RCV1 V2. conjunto de dados de saudação tiver artigos de notícias 781K junto com suas IDs (primeira coluna do conjunto de dados de saudação). Cada artigo é marcado, recebe stopwords e é interrompido. saudação de conjunto de dados foi disponibilizado por David. D. Lewis.
  </td>
</tr>

<tr ID=lyrl2004-tokens-train>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_train.csv">lyrl2004_tokens_train.csv</a></td>
  <td valign=top>
Recursos de exemplos de treinamento no conjunto de dados de notícias do hello Reuters RCV1 V2. conjunto de dados de saudação tiver artigos de notícias 23K junto com suas IDs (primeira coluna do conjunto de dados de saudação). Cada artigo é marcado, recebe stopwords e é interrompido. saudação de conjunto de dados foi disponibilizado por David. D. Lewis.
  </td>
</tr>

<tr ID=intrusion-detection>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a><br></td>
  <td valign=top>
Conjunto de dados de saudação KDD Cup 1999 descoberta de conhecimento e concorrência de ferramentas de mineração de dados (<a href="http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html">kddcup99.html</a>).<p> </p>saudação de conjunto de dados foi baixado e armazenado no armazenamento de BLOBs do Azure (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a>) e inclui o treinamento e conjuntos de dados de teste. Olá conjunto de dados de treinamento tem aproximadamente 126 mil linhas e 43 colunas, incluindo rótulos de saudação. Três colunas fazem parte das informações de rótulo hello e 40 colunas, consiste em recursos numéricos e de cadeia de caracteres/categórica, estão disponíveis para treinar o modelo de saudação. dados de teste de saudação tem aproximadamente 22,5 K exemplos com colunas Olá 43 mesmo como dados de treinamento de saudação de teste.

  </td>
</tr>

<tr ID=rcv1-v2-topics-qrels>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/rcv1-v2.topics.qrels.csv">rcv1-v2.topics.qrels.csv</a></td>
  <td valign=top>
Atribuições de tópico para artigos de notícias no conjunto de dados de notícias do hello Reuters RCV1 V2. Tooseveral tópicos pode ser atribuído a um artigo de notícias. formato de saudação de cada linha é "&lt;o nome do tópico&gt; &lt;id do documento&gt; 1". saudação de conjunto de dados contém 2.6M atribuições de tópico. saudação de conjunto de dados foi disponibilizado por David. D. Lewis.
  </td>
</tr>

<tr ID=student-performance>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a></td>
  <td valign=top>
Esses dados vêm de saudação desafio de avaliação de desempenho KDD Cup 2010 aluno (<a href="http://www.kdd.org/kdd-cup-2010-student-performance-evaluation">avaliação de desempenho do aluno</a>). dados usados Hello são o conjunto de treinamento Olá Algebra_2008_2009 (Stamper, J., Niculescu-Mizil, r., Ritter, s, Gordon, G.J. & Koedinger, K.R. (2010). Algebra I 2008-2009. Conjunto de dados de desafio do KDD Cup 2010 Educational Data Mining Challenge. Encontre-o em <a href="http://pslcdatashop.web.cmu.edu/KDDCup/downloads.jsp">downloads.jsp</a> ou <a href="http://www.kdd.org/sites/default/files/kddcup/site/2010/files/algebra_2008_2009.zip">algebra_2008_2009.zip</a>.<p> </p>saudação de conjunto de dados foi baixado e armazenado no armazenamento de BLOBs do Azure (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a>) e contém os arquivos de log de um aluno ensino particular de sistema. recursos de Olá fornecido incluem o ID do problema e uma descrição curta, ID do estudante, timestamp, e quantas tentativas de aluno Olá feito antes de solução de problema Olá Olá diretas. conjunto de dados original Olá tem registros 8.9M; Este conjunto de dados foi toohello convertidos primeiro 100 mil linhas. Olá dataset tem 23 colunas separados por tabulação de vários tipos: numeric, categórica e o carimbo de hora.

  </td>
</tr>




</table>


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
