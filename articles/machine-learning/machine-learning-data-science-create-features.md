---
title: "engenharia aaaFeature na ciência de dados | Microsoft Docs"
description: "Explica as finalidades de saudação de engenharia de recurso e fornece exemplos de sua função no processo de aprimoramento de dados de saudação do aprendizado de máquina."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3fde69e8-5e7b-49ad-b3fb-ab8ef6503a4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: af40ea9cc9395bc87fe695eeaef26aa71e0ec9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-in-data-science"></a>Engenharia de recursos em ciência de dados
Este tópico explica as finalidades de saudação de engenharia de recurso e fornece exemplos de sua função no processo de aprimoramento de dados de saudação do aprendizado de máquina. exemplos de saudação usaram tooillustrate esse processo foram extraídos do estúdio de aprendizado de máquina do Azure. 

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Isso **menu** links tootopics que descrevem como toocreate recursos para os dados em vários ambientes. Essa tarefa é uma etapa Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

Recurso engenharia tentativas tooincrease Olá poder de previsão de algoritmos de aprendizagem por criar recursos de dados brutos que facilitam o processo de aprendizado de saudação. Olá engenharia e seleção de recursos é uma parte da saudação TDSP descrita Olá [novidades Olá ciclo de vida do processo de ciência de dados de equipe?](data-science-process-overview.md) Engenharia de recurso e seleção são partes Olá **desenvolver recursos** etapa Olá TDSP. 

* **recurso engenharia**: este processo tenta toocreate os recursos relevantes adicionais de saudação bruto os recursos existentes nos dados de saudação e tooincrease Olá poder de previsão de algoritmo de aprendizado hello.
* **seleção de recursos**: esse processo seleciona o subconjunto de chave Olá original de recursos de dados em uma dimensionalidade de saudação tooreduce tentativa de problema de treinamento hello.

Normalmente **recurso engenharia** é aplicada primeiro toogenerate adicionais aos recursos e, em seguida, Olá **seleção de recursos** etapa é executada tooeliminate altamente correlacionado, redundante ou irrelevante recursos.

dados de treinamento Olá usados no aprendizado de máquina geralmente podem ser melhorados por extração dos recursos dos dados brutos de saudação coletados. Um exemplo de um recurso de engenharia no contexto de saudação do aprendizado como imagens de saudação tooclassify caracteres manuscritas é criação de um pouco de densidade mapa construído a partir de dados de distribuição de bits brutos hello. Este mapa pode ajudar a localizar bordas de saudação de caracteres de saudação com mais eficiência do que simplesmente usando distribuição bruto Olá diretamente.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="creating-features-from-your-data---feature-engineering"></a>Criando recursos por meio de seus dados - Engenharia de recursos
dados de treinamento Olá consistem em uma matriz composta de exemplos (registros ou observações armazenadas em linhas), cada qual com um conjunto de recursos (campos armazenados em colunas ou variáveis). recursos de saudação especificados no design experimental Olá estão toocharacterize esperado Olá padrões nos dados de saudação. Embora muitos dos dados brutos de saudação campos podem ser incluídos diretamente em hello tootrain de conjunto usado do recurso selecionado um modelo, ele geralmente é caso Olá que precisam de recursos (engenharia) adicionais toobe construído a partir de recursos Olá Olá dados brutos toogenerate um avançado conjunto de dados de treinamento.

Que tipo de recursos deve ser criado tooenhance Olá dataset ao treinar um modelo? Recursos de engenharia que aprimoram o treinamento Olá fornecem informações que diferencia melhor os padrões de saudação nos dados de saudação. Esperamos Olá novos recursos tooprovide informações adicionais que não é Olá claramente capturada ou facilmente aparente no conjunto de recurso existente ou original. Mas esse processo tem algo de artístico. Decisões sensatas e produtivas frequentemente exigem alguma experiência de domínio.

Ao iniciar com o aprendizado de máquina do Azure, é mais fácil toograsp concretamente usando exemplos fornecido no hello Studio. Dois exemplos são apresentados aqui:

* Um exemplo de regressão [previsão do número de saudação de locações de bicicleta](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4) em um experimento supervisionado em que os valores de destino de saudação são conhecidos
* Um exemplo de classificação de mineração de texto usando [Hash de recursos](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/)

## <a name="example-1-adding-temporal-features-for-regression-model"></a>Exemplo 1: adicionando recursos temporais para o modelo de regressão
Vamos usar Olá experimento "previsão de demanda de bicicletas" no estúdio de aprendizado de máquina do Azure toodemonstrate como tooengineer recursos para uma tarefa de regressão. Olá objetivo esse teste é toopredict demanda de saudação de bicicletas hello, ou seja, número de saudação de locações de bicicleta dentro de uma mês/dia/hora específica. Olá dataset "bicicleta aluguel conjunto de dados UCI" é usado como dados brutos de entrada hello. Este conjunto de dados baseia-se em dados reais de saudação da empresa de Capital Bikeshare que mantém uma rede de aluguel de bicicleta em Washington DC no hello dos Estados Unidos. saudação de conjunto de dados representa o número de saudação de locações de bicicleta dentro de uma hora específica do dia em anos de saudação 2011 e o ano de 2012 e contém 17379 linhas e colunas de 17. conjunto de recursos brutos de saudação contém condições de tempo (velocidade de temperatura/umidade/vento) e o tipo de saudação do dia de saudação (feriado/dia da semana). Olá campo toopredict é "cnt", uma contagem que representa locações de bicicleta hello dentro de uma hora específica e qual intervalos varia de 1 too977.

Com o objetivo de saudação de construção efetivos recursos nos dados de treinamento de saudação, quatro modelos de regressão são criados usando Olá mesmo algoritmo, mas com quatro conjuntos de dados de treinamento diferentes. Olá quatro conjuntos de dados representam Olá mesmo dados brutos de entrada, mas com um número crescente de recursos definido. Os recursos são agrupados em quatro categorias:

1. A = clima + dia da semana e feriados + fins de semana, recursos de dia previsto Olá
2. B = número de bicicletas que foram alugado em cada saudação anteriores 12 horas
3. C = número de bicicletas que foram alugado em cada Olá 12 dias anteriores, a saudação mesmo hora
4. D = número de bicicletas que foram alugado em cada Olá 12 semanas anteriores, a saudação mesmo hora e hello mesmo dia

Além do conjunto de recurso A, que já existe em dados não processados originais hello, hello outros três conjuntos de recursos são criados por meio do processo de engenharia de recurso de saudação. Conjunto de recursos B capturas demanda muito recente para bicicletas hello. Conjunto de recursos C capturas demanda Olá de bicicletas em um horário específico. O conjunto de recursos D capturas de demanda de bicicletas em determinada hora e dia específico da semana hello. Olá quatro treinamento conjuntos de dados de cada inclui A de conjunto de recurso, A + B, A + B + C e A + B + C + D, respectivamente.

Olá experiência de aprendizado de máquina do Azure, esses quatro conjuntos de dados de treinamento são formados por meio de quatro ramificações de saudação pré-processada dataset de entrada. Exceto hello esquerda a maioria das filiais, cada uma dessas seções contém um [Executar Script R](https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/) módulo, no qual um conjunto de recursos derivados (definida de recurso B, C e D) são respectivamente construído e acrescentados toohello importado de conjunto de dados. Olá figura a seguir demonstra o script hello R usadas conjunto de recursos toocreate B em Olá segunda ramificação esquerdo.

![criar recursos](./media/machine-learning-data-science-create-features/addFeature-Rscripts.png)

Olá comparação dos resultados de desempenho de saudação do hello quatro modelos são resumidos na Olá a tabela a seguir. obter os melhores resultados Olá são mostrados pelos recursos A + B + C. Observe que Olá diminui de taxa de erro quando o conjunto de recursos adicionais são incluídos nos dados de treinamento hello. Ele verifica nosso suposição que conjunto de recursos de saudação B, C fornecem informações adicionais de relevantes para a tarefa de regressão hello. Mas adicionando recurso de saudação D não parece tooprovide qualquer redução adicional na taxa de erros de saudação.

![comparação de resultados](./media/machine-learning-data-science-create-features/result1.png)

## <a name="example2"></a> Exemplo 2: Criando recursos com mineração de texto
Recurso engenharia amplamente é aplicada em tootext relacionado de tarefas de mineração, como a análise de sentimento e classificação do documento. Por exemplo, quando queremos tooclassify documentos em várias categorias, uma suposição típica é hello word/expressões incluídas na categoria de um documento são menos provável toooccur em outra categoria de documento. Em outras palavras, a frequência de saudação da distribuição de palavras/expressões Olá é toocharacterize capaz de categorias de documento diferente. Em aplicativos de mineração de texto, como partes individuais do conteúdo de texto geralmente servem como dados de entrada hello, o recurso de saudação processo de engenharia é necessário toocreate Olá recursos que envolvem a palavra/expressão frequências.

tooachieve essa tarefa, uma técnica chamada **hash de recurso** é aplicado tooefficiently ativar recursos de texto arbitrário em índices. Em vez de associar cada recurso (palavras/expressões) tooa determinado índice de texto, essas funções de método aplicando uma recursos de toohello de função de hash e usando os respectivos valores de hash como índices diretamente.

No Azure Machine Learning, há um módulo [Hash de Recursos](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) que cria esses recursos de palavra/expressão de maneira conveniente. A figura a seguir mostra um exemplo de uso deste módulo. conjunto de dados de entrada Hello contém duas colunas: Olá classificação de catálogo que variam de 1 too5 e Olá real revisar o conteúdo. objetivo de saudação desta [hash de recurso](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) módulo é tooretrieve uma série de novos recursos que mostram a frequência de ocorrência de saudação do hello correspondente palavras / phrase(s) dentro de revisão de catálogo específico de saudação. toouse neste módulo, precisamos Olá toocomplete etapas a seguir:

* Primeiro, selecione a coluna de saudação que contém o texto de entrada hello ("Col2" neste exemplo).
* Em seguida, definir Olá too8 "Hashing bitsize", que significa 2 ^ 8 = 256 recursos serão criados. Olá, word ou fase em todo o texto de saudação será índices de hash too256. parâmetro Hello "Hashing bitsize" varia de 1 too31. Olá palavras phrase(s) são menos provável toobe transformado em Olá mesmo se configurá-la toobe um número maior de índice.
* Em terceiro lugar, defina too2 do parâmetro "N-gramas" hello. Frequência de ocorrência de saudação do unigrams (um recurso para cada palavra única) e bigrams (um recurso para cada par de palavras adjacentes) obtém Olá texto de entrada. intervalos de "N-gramas" Hello parâmetros de too10 0, que indica o número máximo de saudação de palavras sequencial toobe incluído em um recurso.  

![Módulo "Hash de Recursos"](./media/machine-learning-data-science-create-features/feature-Hashing1.png)

Olá figura a seguir mostra o que Olá esses novos recursos a aparência.

![Exemplo de "Hash de Recursos"](./media/machine-learning-data-science-create-features/feature-Hashing2.png)

## <a name="conclusion"></a>Conclusão
Recursos de engenharia e selecionados aumentam a eficiência de saudação do processo de treinamento de saudação que tentativas de informações de chave de saudação do tooextract contidas nos dados de saudação. Eles também melhoram power Olá esses modelos tooclassify Olá de dados de entrada com precisão e toopredict resultados de seu interesse mais robustez. Engenharia de recurso e seleção também podem combinar o aprendizado de saudação toomake computacionalmente mais manejável. Isso é feito, aprimorando e, em seguida, reduzindo o número de saudação de recursos necessários toocalibrate ou treinar um modelo. Matematicamente falando, o modelo de Olá Olá recursos tootrain selecionado são um conjunto mínimo de variáveis independentes que explicam Olá padrões nos dados hello e, em seguida, prever os resultados com êxito.

Observe que nem sempre é necessariamente tooperform seleção de engenharia ou recurso do recurso. Se for necessário ou não depende de dados Olá temos ou coletar, algoritmo Olá que podemos escolher, e Olá objetivo do experimento hello.

