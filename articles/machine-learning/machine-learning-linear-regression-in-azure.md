---
title: "Regressão Linear no aprendizado de máquina do aaaUsing | Microsoft Docs"
description: "Uma comparação dos modelos de regressão linear no Excel e no Azure Machine Learning Studio "
metakeywords: 
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 417ae6ab-de4f-4bdd-957a-d96133234656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: kbaroni;garye
ms.openlocfilehash: 8716040ad296053a72fb06c7c9660a186123ac15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-linear-regression-in-azure-machine-learning"></a>Usando regressão linear no Azure Machine Learning
> *Kate Baroni* e *Ben Boatman* são arquitetos de soluções corporativas no Data Insights Center of Excellence da Microsoft. Neste artigo, eles descrevem sua experiência de migrar uma regressão analysis suite tooa baseado em nuvem solução existente usando o aprendizado de máquina do Azure. 
> 
> 

&nbsp; 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="goal"></a>Objetivo
Nosso projeto começou com dois objetivos: 

1. Use a precisão de saudação tooimprove análise preditiva de projeções de receita mensal da organização 
2. Usar tooconfirm de aprendizado de máquina do Azure, otimizar, aumentar a velocidade e a escala de nossos resultados. 

Como muitas empresas, nossa organização passa por uma processo de previsão de receita mensal. Nossa equipe de analistas de negócios de pequeno tarefa era usando o processo de saudação do aprendizado de máquina do Azure toosupport e aumentar a precisão da previsão. equipe de saudação gasto vários meses de coleta de dados de várias fontes e em execução atributos de saudação de dados por meio de análise estatística identificando atributos de chave previsão de vendas tooservices relevantes. Olá próxima etapa foi toobegin protótipos estatística regressão nos dados Olá no Excel. Em algumas semanas, tivemos um modelo de regressão do Excel que foi superando campo atual hello e processos de previsão de finanças. Isso se tornou o resultado da previsão Olá da linha de base. 

Em seguida, tivemos Olá próxima etapa toomoving nossa análise preditiva em toofind de aprendizado de máquina tooAzure out como o aprendizado de máquina podem melhorar desempenho previsível.

## <a name="achieving-predictive-performance-parity"></a>Obtendo a paridade de desempenho preditivo
Nossa primeira prioridade foi tooachieve paridade entre os modelos de regressão de aprendizado de máquina e Excel. Considerando Olá os mesmos dados e Olá mesmo dividido para dados de teste e treinamento, queremos que a paridade de desempenho de previsão tooachieve entre o Excel e aprendizado de máquina. Inicialmente, falhamos. modelo de aprendizado de máquina do Olá Olá Excel superaram do modelo. Falha de saudação venceu tooa falta de compreensão de ferramenta base do hello configuração no aprendizado de máquina. Após uma sincronização com a equipe de produto de aprendizado de máquina hello, obtido um melhor entendimento do hello base configuração necessária para os conjuntos de dados e obtida paridade entre dois modelos de saudação. 

### <a name="create-regression-model-in-excel"></a>Criar um modelo de regressão no Excel
Nosso regressão do Excel usado o modelo de regressão linear padrão Olá encontrado no hello ferramentas de análise do Excel. 

Calculado *% médio absoluto erro* e usado como medida de desempenho Olá para o modelo de saudação. Levou tooarrive 3 meses em um modelo de trabalho usando o Excel. É colocado muito aprendizado Olá em Olá experimento estúdio de aprendizado de máquina que, por fim, foi útil em Noções básicas sobre requisitos.

### <a name="create-comparable-experiment-in-azure-machine-learning"></a>Criar um experimento comparável no Azure Machine Learning
Seguimos toocreate essas etapas nossa experiência no estúdio de aprendizado de máquina: 

1. Conjunto de dados Olá carregado como um arquivo de csv tooMachine estúdio de aprendizado (arquivo muito pequeno)
2. Criado um novo teste e usado Olá [selecionar colunas no conjunto de dados] [ select-columns] tooselect módulo Olá mesmos recursos de dados usados no Excel 
3. Olá usado [dividir dados] [ split] módulo (com *expressão relativa* modo) dados Olá toodivide Olá mesmos conjuntos de dados de treinamento, como era feito no Excel 
4. Experiência com hello [Regressão Linear] [ linear-regression] módulo (somente opções padrão), documentada e, em comparação com o modelo de regressão Olá resultados tooour Excel

### <a name="review-initial-results"></a>Examinar os resultados iniciais
Primeiro, o modelo de saudação do Excel claramente superaram modelo do estúdio de aprendizado de máquina hello: 

|  | Excel | Estúdio |
| --- |:---:|:---:|
| Desempenho | | |
| <ul style="list-style-type: none;"><li>Quadrado R Ajustado</li></ul> |0,96 |N/D |
| <ul style="list-style-type: none;"><li>Coeficiente de <br />Determinação</li></ul> |N/D |0,78<br />(baixa precisão) |
| Erro Absoluto Médio |US$ 9,5 milhões |US$ 19,4 milhões |
| Erro Absoluto Médio (%) |6,03% |12,2% |

Quando executamos nosso processo e os resultados por desenvolvedores de saudação e os cientistas de dados da equipe de aprendizado de máquina hello, elas rapidamente fornecidas algumas dicas úteis. 

* Quando você usa Olá [Regressão Linear] [ linear-regression] módulo no estúdio de aprendizado de máquina, dois métodos são fornecidos:
  * Gradiente Online Descendente: talvez seja mais adequado para problemas de maior escala
  * Quadrados mínimos: Este é o método hello a maioria das pessoas pensam ao ouvirão regressão linear. Para conjuntos de dados pequenos, Mínimos Quadrados Comuns pode ser uma opção melhor.
* Considere ajustar o desempenho de tooimprove de parâmetro hello peso de Regularização L2. Too0.001 é definido por padrão, mas para nosso conjunto de dados pequeno, configurá-lo too0.005 tooimprove desempenho. 

### <a name="mystery-solved"></a>Mistério resolvido!
Quando aplicamos recomendações Olá, é obtida Olá mesmo desempenho de linha de base no estúdio de aprendizado de máquina, com o Excel: 

|  | Excel | Estúdio (inicial) | Estúdio c/ quadrados mínimos |
| --- |:---:|:---:|:---:|
| Valor rotulado |Dados reais (numéricos) |mesmo |mesmo |
| Aprendiz |Excel -> Dados da Análise -> Regressão |Regressão Linear. |Regressão Linear |
| Opções de aprendiz |N/D |Padrões |quadrados mínimos comuns<br />L2 = 0,005 |
| Conjunto de dados |26 linhas, 3 recursos, 1 rótulo. Todos numéricos. |mesmo |mesmo |
| Divisão: treinamento |Excel treinado em Olá primeiro 18 linhas, testado Olá última 8 linhas. |mesmo |mesmo |
| Divisão: teste |Fórmula de regressão aplicada do Excel toohello última 8 linhas |mesmo |mesmo |
| **Desempenho** | | | |
| Quadrado R Ajustado |0,96 |N/D | |
| Coeficiente de Determinação |N/D |0,78 |0,952049 |
| Erro Absoluto Médio |US$ 9,5 milhões |US$ 19,4 milhões |US$ 9,5 milhões |
| Erro Absoluto Médio (%) |<span style="background-color: 00FF00;"> 6,03%</span> |12,2% |<span style="background-color: 00FF00;"> 6,03%</span> |

Além disso, coeficientes de Excel Olá com bem toohello pesos de recurso no hello treinado do Azure:

|  | Coeficientes do Excel | Pesos de recursos do Azure |
| --- |:---:|:---:|
| Interceptação/desvio |19470209,88 |19328500 |
| Recurso A |0,832653063 |0,834156 |
| Recurso B |11071967,08 |11007300 |
| Recurso C |25383318,09 |25140800 |

## <a name="next-steps"></a>Próximas etapas
Queremos que o serviço de web de aprendizado de máquina tooconsume hello dentro do Excel. Os analistas de negócios contam com Excel e é necessária uma saudação toocall de maneira aprendizado de máquina web serviço com uma linha de dados do Excel e a retornar Olá previsto tooExcel de valor. 

Também queremos toooptimize nosso modelo, usando as opções de saudação e os algoritmos disponíveis no estúdio de aprendizado de máquina.

### <a name="integration-with-excel"></a>Integração com o Excel
Nossa solução foi toooperationalize nosso regressão de aprendizado de máquina de modelo ao criar um serviço web de modelo treinado hello. Em alguns minutos, Olá web serviço foi criado e chamamos-lo diretamente do Excel tooreturn um valor previsto de receita. 

Olá *painel de serviços Web* seção inclui uma pasta de trabalho do Excel para download. pasta de trabalho Olá acompanha pré-formatada Olá API e esquema de informações do serviço web inseridas. Quando você clica em *baixar pasta de trabalho do Excel*, pasta de trabalho Olá abre e salve-o computador local tooyour. 

![][1]

Com abrir da pasta de trabalho hello, copie os parâmetros predefinidos na seção de parâmetro hello azul conforme mostrado abaixo. Depois de saudação parâmetros forem inseridos, Excel chama toohello serviço web de aprendizado de máquina e hello classificado de rótulos previstos serão exibidas na seção de valores previstos Olá verde. pasta de trabalho Olá continuará toocreate previsões para parâmetros com base em seu modelo treinado para todos os itens de linha inserida em parâmetros. Para obter mais informações sobre como toouse esse recurso, consulte [consumir um serviço de Web de aprendizado de máquina do Azure do Excel](machine-learning-consuming-from-excel.md). 

![][2]

### <a name="optimization-and-further-experiments"></a>Otimização e experimentos adicionais
Agora que tivemos que uma linha de base com nosso modelo do Excel, mudamos toooptimize ahead nosso modelo Regressão Linear de aprendizado de máquina. Usamos o módulo Olá [seleção de recursos baseada em filtro] [ filter-based-feature-selection] tooimprove em nossa seleção de elementos de dados inicial e nos ajudou a obter uma melhoria de desempenho de 4.6% significa erro absoluto. Para projetos futuros usaremos esse recurso que foi possível salvar nos semanas na iteração por meio de atributos toofind Olá certo conjunto de dados de toouse de recursos de modelagem. 

Em seguida, estamos planejando tooinclude de algoritmos adicionais como [Bayesiana] [ bayesian-linear-regression] ou [árvores de decisão impulsionada] [ boosted-decision-tree-regression] em nossa experiência toocompare desempenho. 

Se você quiser tooexperiment com regressão, tootry um bom conjunto de dados é dataset de exemplo de regressão de eficiência de energia hello, que tem muitos atributos numéricos. saudação de conjunto de dados é fornecido como parte dos conjuntos de dados de exemplo de hello no estúdio de aprendizado de máquina. Você pode usar uma variedade de aprendizado módulos toopredict carga aquecimento ou resfriamento de carga. gráfico de saudação abaixo é que uma comparação de desempenho de regressão diferente aprende contra Olá eficiência de energia dataset prevendo Olá carga resfriamento variável de destino: 

| Modelo | Erro Absoluto Médio | Erro Quadrado Médio de Raiz | Erro Absoluto Relativo | Erro Quadrado Relativo | Coeficiente de Determinação |
| --- | --- | --- | --- | --- | --- |
| Árvore de Decisão Aumentada |0,930113 |1,4239 |0,106647 |0,021662 |0,978338 |
| Regressão Linear (Gradiente Descendente) |2,035693 |2,98006 |0,233414 |0,094881 |0,905119 |
| Regressão de Rede Neural |1,548195 |2,114617 |0,177517 |0,047774 |0,952226 |
| Regressão Linear (Quadrados Mínimos Comuns) |1,428273 |1,984461 |0,163767 |0,042074 |0,957926 |

## <a name="key-takeaways"></a>Principais observações
Aprendemos muito executando os experimentos de regressão do Excel e do Azure Machine Learning em paralelo. Criar modelo de linha de base de saudação no Excel e compará-lo usando o aprendizado de máquina de toomodels [Regressão Linear] [ linear-regression] ajudou nos saber o aprendizado de máquina do Azure e descobrimos que os dados de tooimprove de oportunidades desempenho de seleção e o modelo. 

Também descobrimos que ele é aconselhável toouse [seleção de recursos baseada em filtro] [ filter-based-feature-selection] tooaccelerate projetos de previsão futuros. Aplicando tooyour dados da seleção de recurso, você pode criar um modelo aprimorado no aprendizado de máquina com melhor desempenho geral. 

Olá tootransfer de capacidade de saudação previsão analítica de previsão de aprendizado de máquina tooExcel sistemático permite que um aumento significativo no hello capacidade toosuccessfully fornecer resultados público amplo business tooa. 

## <a name="resources"></a>Recursos
Estes são alguns recursos que ajudam a trabalhar com a regressão: 

* Regressão no Excel. Se você nunca experimentou a regressão no Excel, este tutorial facilita tudo: [http://www.excel-easy.com/examples/regression.html](http://www.excel-easy.com/examples/regression.html)
* Regressão versus previsão. Tyler Chessman escreveu um artigo de blog explicando como toodo previsão de série temporal no Excel, que contém a descrição de um bom para iniciantes de regressão linear. [http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts](http://sqlmag.com/sql-server-analysis-services/understanding-time-series-forecasting-concepts) 
* Regressão linear de quadrados mínimos simples: falhas, problemas e armadilhas. Para obter uma introdução e uma discussão sobre regressão: [http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/ ](http://www.clockbackward.com/2009/06/18/ordinary-least-squares-linear-regression-flaws-problems-and-pitfalls/)

[1]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-1.png
[2]: ./media/machine-learning-linear-regression-in-azure/machine-learning-linear-regression-in-azure-2.png


<!-- Module References -->
[bayesian-linear-regression]: https://msdn.microsoft.com/library/azure/ee12de50-2b34-4145-aec0-23e0485da308/
[boosted-decision-tree-regression]: https://msdn.microsoft.com/library/azure/0207d252-6c41-4c77-84c3-73bdf1ac5960/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/

