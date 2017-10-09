---
title: "aaaFeature engenharia e seleção no aprendizado de máquina do Azure | Microsoft Docs"
description: "Explica as finalidades de saudação de engenharia de recurso e seleção de recursos e fornece exemplos de sua função no processo de aprimoramento de dados de saudação do aprendizado de máquina."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 9ceb524d-842e-4f77-9eae-a18e599442d6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: zhangya;bradsev
ROBOTS: NOINDEX
redirect_url: machine-learning-data-science-create-features
redirect_document_id: True
ms.openlocfilehash: e3e59329bf46f334396f5975b4e656137362d7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="feature-engineering-and-selection-in-azure-machine-learning"></a>Engenharia e seleção de recursos no Azure Machine Learning
Este tópico explica a fins de saudação de engenharia de recurso e seleção de recursos no processo de aprimoramento de dados de saudação do aprendizado de máquina. Ele ilustra o que esses processos envolvem usando exemplos fornecidos pelo Azure Machine Learning Studio.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

dados de treinamento Olá usados no aprendizado de máquina geralmente podem ser aprimorados por seleção hello ou extração de recursos dos dados brutos de saudação coletados. Um exemplo de um recurso de engenharia no contexto de saudação do aprendizado como imagens de saudação tooclassify caracteres manuscritas é um mapa de densidade de bits construída de dados de distribuição de bits brutos hello. Este mapa pode ajudar a localizar bordas de saudação de caracteres de saudação de distribuição bruto Olá forma mais eficiente.

Recursos de engenharia e selecionados aumentam a eficiência de saudação do processo de treinamento hello, que tenta tooextract informações de chave Olá contidas nos dados de saudação. Eles também melhoram power Olá esses modelos tooclassify Olá de dados de entrada com precisão e toopredict resultados de seu interesse mais robustez. Engenharia de recurso e seleção também podem combinar o aprendizado de saudação toomake computacionalmente mais manejável. Isso é feito, aprimorando e, em seguida, reduzindo o número de saudação de recursos necessários toocalibrate ou treinar um modelo. Matematicamente falando, o modelo de Olá Olá recursos tootrain selecionado são um conjunto mínimo de variáveis independentes que explicam Olá padrões nos dados hello e, em seguida, prever os resultados com êxito.

engenharia Hello e seleção de recursos é uma parte de um processo maior, que normalmente consiste em quatro etapas:

* Coleta de dados
* Aperfeiçoamento de dados
* Construção de modelo
* Pós-processamento

Engenharia e seleção compõem a etapa de aprimoramento de dados de saudação de aprendizado de máquina. Três aspectos desse processo podem ser diferenciados para nossos propósitos:

* **Pré-processamento de dados**: este processo tooensure tentativas que os dados coletados de Olá é limpo e consistente. Ele inclui tarefas como a integração de vários conjuntos de dados, manipulação de dados que estão faltando, manipulação de dados inconsistentes e conversão de tipos de dados.
* **Recurso engenharia**: este processo tenta toocreate os recursos relevantes adicionais de saudação bruto os recursos existentes no hello dados e tooincrease capacidade de previsão toohello algoritmo de aprendizado.
* **Seleção de recursos**: este processo seleciona o subconjunto de chave de saudação de dados recursos tooreduce Olá dimensionalidade original do problema de treinamento hello.

Este tópico aborda apenas Olá recurso engenharia e recurso aspectos de seleção Olá aprimoramento do processo de dados. Para obter mais informações sobre a etapa de pré-processamento de dados hello, consulte [pré-processamento de dados no estúdio de aprendizado de máquina do Azure](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/).

## <a name="creating-features-from-your-data--feature-engineering"></a>Criando recursos de seus dados - Engenharia de recursos
dados de treinamento Olá consistem em uma matriz composta de exemplos (registros ou observações armazenadas em linhas), cada qual com um conjunto de recursos (campos armazenados em colunas ou variáveis). recursos de saudação especificados no design experimental Olá estão toocharacterize esperado Olá padrões nos dados de saudação. Embora muitos dos dados brutos de saudação campos podem ser incluídos diretamente em hello tootrain de conjunto usado do recurso selecionado um modelo, recursos adicionais de engenharia necessitam geralmente toobe construído a partir de recursos Olá Olá dados brutos toogenerate um conjunto de dados de treinamento avançado.

Que tipo de recursos deve ser criado o conjunto de dados de saudação tooenhance ao treinar um modelo? Recursos de engenharia que aprimoram o treinamento Olá fornecem informações que diferencia melhor os padrões de saudação nos dados de saudação. Você espera Olá novos recursos tooprovide informações adicionais que não é claramente capturada ou facilmente aparente no hello original ou conjunto de recursos existente, mas esse processo é algo uma arte. Decisões sensatas e produtivas frequentemente exigem alguma experiência de domínio.

Ao iniciar com o aprendizado de máquina do Azure, é mais fácil toograsp esse processo concretamente usando exemplos fornecido no estúdio de aprendizado de máquina. Dois exemplos são apresentados aqui:

* Um exemplo de regressão ([previsão do número de saudação de locações de bicicleta](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4)) em um experimento supervisionado em que os valores de destino de saudação são conhecidos
* Um exemplo de classificação de mineração de texto usando [Hash de Recursos][feature-hashing]

### <a name="example-1-adding-temporal-features-for-a-regression-model"></a>Exemplo 1: adição de recursos temporais para um modelo de regressão
toodemonstrate como tooengineer recursos para uma tarefa de regressão, vamos usar Olá experimento "previsão de demanda de bicicletas" no estúdio de aprendizado de máquina do Azure. Olá objetivo esse teste é toopredict demanda de saudação de bicicletas hello, ou seja, número de saudação de locações de bicicleta dentro de um determinado mês, dia ou hora. conjunto de dados Olá **conjunto de dados UCI de aluguel de bicicleta** é usado como dados brutos de entrada hello.

Esse conjunto de dados baseia-se em dados reais de saudação da empresa de Capital Bikeshare que mantém uma rede de aluguel de bicicleta em Washington DC no hello dos Estados Unidos. conjunto de dados de saudação representa o número de saudação de locações de bicicleta dentro de uma hora específica do dia, de 2011 too2012, e contém 17379 linhas e colunas de 17. conjunto de recursos brutos de saudação contém condições de tempo (temperatura, umidade, velocidade do vento) e o tipo de saudação do dia de saudação (feriado ou dia da semana). Olá campo toopredict é **cnt**, uma contagem que representa locações de bicicleta hello dentro de uma hora específica e que varia de 1 too977.

tooconstruct recursos eficiente nos dados de treinamento hello, quatro modelos de regressão são criados usando o hello mesmo algoritmo, mas com dados de treinamento diferentes quatro define. Olá quatro conjuntos de dados representam Olá mesmo dados brutos de entrada, mas com um número crescente de recursos definido. Os recursos são agrupados em quatro categorias:

1. A = clima + dia da semana e feriados + fins de semana, recursos de dia previsto Olá
2. B = número de bicicletas que foram alugado em cada saudação anteriores 12 horas
3. C = número de bicicletas que foram alugado em cada Olá 12 dias anteriores, a saudação mesmo hora
4. D = número de bicicletas que foram alugado em cada Olá 12 semanas anteriores, a saudação mesmo hora e hello mesmo dia

Além do conjunto de recurso A, que já existe em dados não processados originais hello, hello outros três conjuntos de recursos são criados por meio do processo de engenharia de recurso de saudação. B capturas Olá recente demanda de Bicicletas de saudação do conjunto de recursos. Conjunto de recursos C capturas demanda Olá de bicicletas em um horário específico. O conjunto de recursos D capturas de demanda de bicicletas em determinada hora e dia específico da semana hello. Cada um dos conjuntos de dados de treinamento Olá quatro inclui conjuntos de recursos A, A + B, A + B + C e A + B + C + D, respectivamente.

Olá experiência de aprendizado de máquina do Azure, esses quatro conjuntos de dados de treinamento são formados por meio de quatro ramificações Olá pré-processada entrada no conjunto de dados. Com exceção de ramificação mais à esquerda do hello, cada uma dessas seções contém um [Executar Script R] [ execute-r-script] módulo no qual um conjunto de derivados de recursos (conjuntos de recursos B, C e D) respectivamente é construído e anexado toohello importado o conjunto de dados. Olá figura a seguir demonstra o script hello R usadas conjunto de recursos toocreate B em Olá segunda ramificação esquerdo.

![Criar um conjunto de recursos](./media/machine-learning-feature-selection-and-engineering/addFeature-Rscripts.png)

Olá tabela a seguir resume a comparação Olá de resultados de desempenho de saudação de quatro modelos de saudação. obter os melhores resultados Olá são mostrados pelos recursos A + B + C. Observe que a taxa de erro Olá diminui quando os conjuntos de recursos adicionais são incluídos nos dados de treinamento hello. Isso verifica nossa suposição que Olá B e C fornecem informações relevantes para a tarefa de regressão de saudação de conjuntos de recursos. Adicionar o conjunto de recursos de saudação D não parece tooprovide qualquer redução adicional na taxa de erros de saudação.

![Comparação dos resultados de desempenho](./media/machine-learning-feature-selection-and-engineering/result1.png)

### <a name="example2"></a> Exemplo 2: criando recursos com mineração de texto
Recurso engenharia amplamente é aplicada em tootext relacionado de tarefas de mineração, como a análise de sentimento e classificação do documento. Por exemplo, quando desejar tooclassify documentos em várias categorias, uma suposição típica é que palavras hello ou expressões incluídas na categoria de um documento são menos provável toooccur em outra categoria de documento. Em outras palavras, a frequência de saudação da distribuição de palavra ou frase Olá é toocharacterize capaz de categorias de documento diferente. Em aplicativos de mineração de texto, o recurso de saudação processo de engenharia é necessário toocreate Olá recursos que envolvem a palavra ou frase frequências porque partes individuais do conteúdo de texto geralmente funcionam como Olá dados de entrada.

tooachieve essa tarefa, uma técnica chamada *hash de recurso* é aplicado tooefficiently ativar recursos de texto arbitrário em índices. Em vez de associar cada recurso (palavras ou frases) tooa determinado índice de texto, essas funções de método aplicando uma recursos de toohello de função de hash e usando os valores de hash como índices diretamente.

No Azure Machine Learning, há um módulo de [Hash de Recursos][feature-hashing] que cria esses recursos de palavra ou expressão. Olá figura a seguir mostra um exemplo de como usar este módulo. conjunto de dados de entrada de saudação contém duas colunas: classificação de catálogo Olá que variam de 1 too5 Olá real revisão e conteúdo. objetivo de saudação desta [hash de recurso] [ feature-hashing] tooretrieve novos recursos que mostram a frequência de ocorrência de saudação de palavras correspondente hello ou frases dentro de revisão de catálogo específico de saudação do módulo é. toouse neste módulo, você precisa Olá toocomplete etapas a seguir:

1. Coluna Olá Select que contém o texto de entrada hello (**Col2** neste exemplo).
2. Definir *bitsize de hash* too8, o que significa que 2 ^ 8 = 256 recursos são criados. Olá palavra ou frase em texto de saudação é, em seguida, too256 índices de hash. Olá parâmetro *bitsize de hash* varia de 1 too31. Se o parâmetro hello está definido tooa maior número, Olá de palavras ou frases são menos prováveis toobe transformado em Olá mesmo índice.
3. Defina o parâmetro hello *N-grams* too2. Isso recupera a frequência de ocorrência de saudação do unigrams (um recurso para cada palavra única) e bigrams (um recurso para cada par de palavras adjacentes) Olá texto de entrada. Olá parâmetro *N-grams* varia de 0 too10, que indica o número máximo de saudação do toobe palavras sequenciais incluído em um recurso.  

![Módulo Hash de Recursos](./media/machine-learning-feature-selection-and-engineering/feature-Hashing1.png)

Olá figura a seguir mostra esses novos recursos como a aparência.

![Exemplo de Hash de Recursos](./media/machine-learning-feature-selection-and-engineering/feature-Hashing2.png)

## <a name="filtering-features-from-your-data--feature-selection"></a>Filtrando recursos de seus dados--Seleção de recursos
*Seleção de recursos* é um processo que é geralmente aplicada toohello construção de conjuntos de dados de treinamento para tarefas de modelagem de previsão, como tarefas de classificação ou regressão. meta de saudação é tooselect um subconjunto de recursos Olá Olá original no conjunto de dados que reduz suas dimensões usando um conjunto mínimo de recursos toorepresent Olá máximo de variação nos dados de saudação. Esse subconjunto de recursos contém Olá apenas recursos toobe incluído tootrain Olá modelo. A seleção de recursos atende a duas finalidades principais:

* A seleção de recursos frequentemente aumenta a precisão de classificação, eliminando recursos irrelevantes, redundantes ou altamente correlacionados.
* Recurso seleção diminui Olá número de recursos, que torna mais eficiente o processo de treinamento de modelo de saudação. Isso é particularmente importante para alunos que são caro tootrain como máquinas de vetor de suporte.

Embora a seleção de recursos buscas tooreduce vários Olá recursos no modelo de Olá Olá conjunto de dados usado tootrain, não é geralmente chamado de termo de saudação tooby *redução de dimensionalidade.* Métodos de seleção de recurso extrair um subconjunto de recursos originais em dados saudação sem alterá-los.  Métodos de redução de dimensionalidade empregam recursos de engenharia que podem transformar recursos original hello e, portanto, modificá-las. Exemplos de métodos de redução de dimensionalidade incluem a análise de componente principal, a análise de correlação canônica e a decomposição de valor singular.

Uma categoria amplamente aplicada de métodos de seleção de recursos em um contexto supervisionado é a seleção de recursos baseada em filtros. Avaliando a correlação de saudação entre cada atributo de destino do recurso e hello, esses métodos se aplicam a tooassign uma medida estatística um recurso de tooeach de pontuação. Olá recursos são então classificados pela pontuação hello, que você pode usar o limite de saudação tooset para manter ou eliminar um recurso específico. Correlação de Pearson, informações mútuas e teste qui-quadrada Olá são exemplos de medidas estatísticas de saudação usadas nesses métodos.

O Azure Machine Learning Studio fornece módulos para seleção de recursos. Conforme mostrado na figura a seguir de saudação, esses módulos abrangem [seleção de recursos baseada em filtro] [ filter-based-feature-selection] e [análise Discriminante Linear Fisher] [ fisher-linear-discriminant-analysis].

![Exemplo de seleção de recursos](./media/machine-learning-feature-selection-and-engineering/feature-Selection.png)

Por exemplo, usar Olá [seleção de recursos baseada em filtro] [ filter-based-feature-selection] módulo com exemplo de mineração de texto hello descrito anteriormente. Digamos que você queira toobuild um modelo de regressão depois que um conjunto de 256 recursos é criado por meio de saudação [hash de recurso] [ feature-hashing] módulo e essa variável de resposta de saudação é **Col1**e representa um catálogo de examinar a classificação que variam de 1 too5. Definir **recurso método de pontuação** muito**correlação de Pearson**, **coluna de destino** muito**Col1**, e **desejado de número de recursos** muito**50**. módulo Olá [seleção de recursos baseada em filtro] [ filter-based-feature-selection] , em seguida, gera um conjunto de dados que contém 50 recursos junto com o atributo de destino Olá **Col1**. a seguir Olá figura mostra o fluxo de saudação desse teste e Olá parâmetros de entrada.

![Exemplo de seleção de recursos](./media/machine-learning-feature-selection-and-engineering/feature-Selection1.png)

Olá seguinte figura mostra Olá conjuntos de dados resultante. Cada recurso é classificado com base Olá correlação de Pearson entre ele mesmo e Olá atributo de destino **Col1**. recursos de saudação com pontos mais altos são mantidos.

![Conjuntos de dados da seleção de recursos baseada em filtro](./media/machine-learning-feature-selection-and-engineering/feature-Selection2.png)

Olá mostra a figura a seguir Olá pontuações correspondentes dos recursos de saudação selecionado.

![Pontuações de recursos selecionados](./media/machine-learning-feature-selection-and-engineering/feature-Selection3.png)

Aplicando isso [seleção de recursos baseada em filtro] [ filter-based-feature-selection] módulo, 50 de 256 recursos são selecionados porque eles têm Olá a maioria dos recursos correlacionadas com variável de destino Olá **Col1** com base no método de pontuação de saudação **correlação de Pearson**.

## <a name="conclusion"></a>Conclusão
Seleção de recursos e de engenharia de recurso são duas etapas executadas comumente tooprepare dados de treinamento de saudação ao criar um modelo de aprendizado de máquina. Normalmente, engenharia de recurso é aplicada primeiro recursos adicionais do toogenerate e etapa de seleção de recurso Olá é executada tooeliminate irrelevante, redundância ou recursos altamente correlacionados.

Nem sempre é necessariamente tooperform seleção de engenharia ou recurso do recurso. Se for necessário depende dos dados Olá tiver ou coletar, algoritmo Olá que você escolher, e Olá objetivo do experimento Olá.

<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/
