---
title: "Variação de cliente usando o aprendizado de máquina de aaaAnalyzing | Microsoft Docs"
description: "Estudo de caso do desenvolvimento de um modelo integrado para analisar e pontuar a insatisfação do cliente"
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: 1333ffe2-59b8-4f40-9be7-3bf1173fc38d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 070e6a2ebe4f2fe439a42ffe1a3fa9d6d3788d62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-customer-churn-by-using-azure-machine-learning"></a>Analisando a Variação do Cliente usando o Machine Learning do Microsoft Azure
## <a name="overview"></a>Visão geral
Este artigo apresenta uma implementação de referência de um projeto de análise de variação de cliente que é criado usando-se o Azure Machine Learning. Neste artigo, discutiremos modelos genéricos associados para resolver totalmente o problema de saudação de rotatividade de cliente industrial. Podemos também medir a precisão de saudação de modelos que são criados usando o aprendizado de máquina e avaliamos orientações para desenvolvimento futuro.  

### <a name="acknowledgements"></a>Confirmações
Esse experimento foi desenvolvido e testado por Serge Berger, principal cientista de dados na Microsoft, e Roger Barga, ex-gerente de produto para o Microsoft Azure Machine Learning. equipe de documentação do Azure Olá gratamente reconhece sua experiência e Obrigado-los para compartilhar este white paper.

> [!NOTE]
> dados de saudação usados para esse teste não estão disponíveis publicamente. Para obter um exemplo de como modelo para análise de variação de toobuild o aprendizado de máquina, consulte: [varejo variação modelo](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1) na [Cortana Intelligence Galeria](http://gallery.cortanaintelligence.com/)
> 
> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-problem-of-customer-churn"></a>problema de saudação de rotatividade de cliente
As empresas no mercado de consumidor hello e em todos os setores de empresa têm toodeal com variação. Algumas vezes a variação é excessiva e influencia decisões de política. solução tradicional Olá é toopredict churners propensity alta e atender a suas necessidades através de um serviço do assistente, campanhas de marketing ou aplicando dispensations especiais. Essas abordagens podem variar de tooindustry do setor e até mesmo de um tooanother de cluster do consumidor específico dentro de um mercado (por exemplo, telecomunicações).

fator comum Olá é que as empresas precisam toominimize esses esforços de retenção especiais para clientes. Portanto, uma metodologia natural seria tooscore todos os clientes com probabilidade de saudação de variação e superior Olá N aqueles de endereço. clientes principais Olá pode ser Olá os mais lucrativos; Por exemplo, em cenários mais sofisticados, uma função de lucro é utilizada durante a seleção de saudação de candidatos para dispensation especial. No entanto, essas considerações são apenas uma parte da estratégia de holística Olá para lidar com variação. As empresas também têm tootake em risco de conta (e tolerância a riscos associados), Olá nível e o custo de intervenção hello e segmentação plausível do cliente.  

## <a name="industry-outlook-and-approaches"></a>Abordagens e perspectiva industriais
O gerenciamento sofisticado da variação é um sinal de uma indústria madura. exemplo clássico Hello é setor de telecomunicações Olá onde assinantes são conhecidos toofrequently switch de tooanother de um provedor. Essa variação voluntária é uma preocupação primária. Além disso, provedores acumulados conhecimento significativo sobre *variação drivers*, que são fatores de saudação que tooswitch de clientes de unidade.

Por exemplo, escolha fone ou dispositivo é um driver bem conhecido de rotatividade de negócios de telefone celular hello. Como resultado, uma política popular custa toosubsidize Olá de um telefone para novos assinantes e carregando um preço total tooexisting clientes para uma atualização. Historicamente, essa política levou toocustomers um desconto de novo, que por sua vez, tem solicitado provedores toorefine suas estratégias de salto de um provedor tooanother tooget.

A alta volatilidade nas ofertas de aparelhos é um fator que invalida muito rapidamente modelos de variação baseados em modelos de aparelhos atuais. Além disso, os telefones celulares não são apenas dispositivos de telecomunicações; Eles também são instruções de forma (considere Olá iPhone) e essas previsões sociais estão fora do escopo Olá telecomunicações regular de conjuntos de dados.

resultado de saudação para modelagem é que não é possível criar uma política de som eliminando motivos conhecidos de variação. Na verdade, uma estratégia de modelagem contínua, incluindo modelos clássicos que quantificam variáveis categóricas (como árvores de decisão), é **obrigatória**.

Usando grandes conjuntos de dados em seus clientes, as organizações executando a análise de big data (em especial, detecção de variação com base nos dados de grandes) como um problema de toohello abordagem efetiva. Você pode encontrar mais informações sobre o problema do hello grandes dados abordagem toohello de rotatividade de saudação recomendações na seção ETL.  

## <a name="methodology-toomodel-customer-churn"></a>Variação de cliente toomodel metodologia
Uma comuns para solução de problemas processo toosolve insatisfação do cliente é abordada em números de 1 a 3:  

1. Um modelo de risco permite tooconsider como ações afetam a probabilidade e risco.
2. Um modelo de intervenção permite tooconsider como nível de saudação de intervenção do pode afetar a probabilidade de saudação da quantidade de variação e saudação de valor de tempo de vida do cliente (CLV).
3. Essa análise se presta análise qualitativa tooa que é escalado tooa pró-ativo campanha de marketing direcionado a oferta ideal de saudação do cliente segmentos toodeliver.  

![][1]

Essa abordagem avançada que visa é melhor variação de tootreat de maneira hello, mas ele vem com complexidade: temos toodevelop um dependências arquétipo e rastreamento de vários modelos entre modelos de saudação. interação de saudação entre modelos pode ser encapsulada conforme mostrado no diagrama a seguir de saudação:  

![][2]

*Figura 4: Arquétipo multimodelo unificado*  

Interação entre os modelos de saudação é chave se estamos toodeliver retenção de toocustomer uma abordagem abrangente. Cada modelo necessariamente degrada ao longo do tempo; Portanto, a arquitetura de saudação é um loop implícita (semelhante arquétipo toohello definido por padrão de mineração de dados Olá CRISP-DM, [***3***]).  

Olá ciclo geral de risco de decisão de marketing segmentação/Decomposição ainda é uma estrutura generalizada, que é aplicável toomany problemas de negócios. Análise de variação é simplesmente um representante forte desse grupo de problemas porque ele exibe todas as características de saudação de um problema de negócios complexa que não permite uma solução de previsão simplificada. Olá social aspectos da saudação abordagem moderna toochurn não são realçados particularmente abordagem hello, mas aspectos social Olá são encapsulados em arquétipo de modelagem hello, como seriam em qualquer modelo.  

Uma adição interessante nesse caso é a análise de big data. As empresas de telecomunicações e de varejo de hoje coletam dados detalhados sobre seus clientes, e é facilmente pode prever que Olá necessário para vários modelo conectividade se tornará uma tendência comum, considerando surgem tendências, como Olá Internet das coisas e dispositivos onipresentes, que permitem soluções inteligentes de business tooemploy em várias camadas.  

 

## <a name="implementing-hello-modeling-archetype-in-machine-learning-studio"></a>Implementando Olá modelagem arquétipo no estúdio de aprendizado de máquina
Devido a problema de saudação descrito, o que é tooimplement de maneira melhor Olá uma modelagem integrada e a abordagem de pontuação? Nesta seção, demonstraremos como conseguimos isso usando o Estúdio do Azure Machine Learning.  

abordagem de vários modelos de saudação é obrigatória ao criar um arquétipo global de variação. Olá mesmo pontuação (previsão) parte da abordagem Olá deve ser vários modelo.  

Olá diagrama a seguir mostra o protótipo de saudação que criamos, que utiliza algoritmos pontuação quatro na variação de toopredict do estúdio de aprendizado de máquina. Olá motivo usando uma abordagem de vários modelo é não apenas toocreate uma precisão de tooincrease ensemble classificação, mas também tooprotect contra sobreajuste e seleção de recurso prescritivas tooimprove.  

![][3]

*Figura 5: Protótipo de uma abordagem de modelagem de variação*  

Olá seções a seguir fornecem mais detalhes sobre o protótipo Olá pontuação modelo que são implementados usando o estúdio de aprendizado de máquina.  

### <a name="data-selection-and-preparation"></a>Seleção e preparação de dados
dados de Olá usados modelos de saudação toobuild e clientes de pontuação foi obtido de uma solução CRM vertical, com a privacidade do cliente Olá dados ofuscadas tooprotect. dados Hello contém informações sobre 8.000 assinaturas Olá dos EUA, e ele combina três fontes: provisionamento de dados (metadados de assinatura), dados de atividade (uso do sistema de saudação) e dados de suporte ao cliente. dados de saudação não incluem qualquer empresa informações relacionadas sobre os clientes Olá; Por exemplo, ele não inclui classificações de crédito ou de metadados de fidelidade.  

Para simplificar, os processos de ETL e limpeza dos dados estão fora do escopo porque presumimos que a preparação dos dados já foi realizada em outra instância.   

Seleção de recursos de modelagem baseia-se na pontuação preliminar significância do conjunto de saudação de previsões, incluídos no processo de saudação que usa o módulo de floresta aleatório hello. Para a implementação de saudação no estúdio de aprendizado de máquina, calculamos Olá média, média e intervalos para recursos representativos. Por exemplo, adicionamos agregações para dados qualitativa hello, como os valores mínimo e máximo para a atividade de usuário.    

Também podemos capturados informações temporais para Olá últimos seis meses. Analisamos dados por um ano e estabelecemos que mesmo se houvesse tendências estatisticamente significativas, efeito Olá na rotatividade é bastante reduzido depois de seis meses.  

o aspecto mais importante Olá é esse processo todo hello, incluindo ETL, seleção de recursos, e modelagem foi implementada no estúdio de aprendizado de máquina, usando fontes de dados no Microsoft Azure.   

Olá diagramas a seguir ilustram dados Olá que foram usados.  

![][4]

*Figura 6: Extrato de fonte de dados (ofuscado)*  

![][5]

*Figura 7: Recursos extraídos da fonte de dados*
 

> Observe que esses dados são particulares e, portanto, os dados e o modelo de saudação não podem ser compartilhados.
> No entanto, para um modelo semelhante usando dados publicamente disponíveis, consulte esse experimento na Olá [Cortana Intelligence galeria](http://gallery.cortanaintelligence.com/): [rotatividade de cliente de telecomunicações](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383).
> 
> toolearn mais sobre como você pode implementar um modelo de análise de variação usando Cortana Intelligence Suite, também é recomendável [este vídeo](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html) pelo gerente de programas sênior dias da s Hyong Tok. 
> 
> 

### <a name="algorithms-used-in-hello-prototype"></a>Algoritmos usados no protótipo Olá
Usamos Olá quatro algoritmos de aprendizagem de máquina a seguir toobuild protótipo de saudação (nenhuma personalização):  

1. Regressão logística (LR)
2. Árvore de decisão aumentada (BT)
3. Perceptron médio (AP)
4. Máquina de vetor de suporte (SVM)  

Olá diagrama a seguir ilustra uma parte da superfície de design do experimento hello, que indica a sequência de saudação em qual Olá modelos foram criados:  

![][6]  


            *Figura 8: Criando modelos no Machine Learning Studio*  

### <a name="scoring-methods"></a>Métodos de pontuação
Modelos Olá quatro nós de pontuação usando um conjunto de dados de treinamento rotulado.  

Olá pontuação modelos do tooa comparáveis do conjunto de dados criados usando a edição de área de trabalho de saudação do SAS Enterprise mineração 12 também foi enviada. Medimos a precisão de saudação do modelo SAS hello e todos os quatro modelos de estúdio de aprendizado de máquina.  

## <a name="results"></a>Resultados
Nesta seção, apresentamos nossas descobertas de precisão de saudação de modelos hello, com base em Olá pontuação de conjunto de dados.  

### <a name="accuracy-and-precision-of-scoring"></a>Precisão e exatidão da pontuação
Em geral, a implementação de saudação no aprendizado de máquina do Azure é atrás SAS em precisão por aproximadamente 10 a 15% (área na curva ou AUC).  

No entanto, a medida mais importante Olá na variação de é taxa de misclassification Olá: ou seja, de churners de N maiores hello como previsto por classificador hello, qual delas foi realmente **não** variação e ainda recebeu tratamento especial? Olá diagrama a seguir compara a taxa de misclassification para todos os modelos de saudação:  

![][7]

*Figura 9: Área do protótipo de Passau sob a curva*

### <a name="using-auc-toocompare-results"></a>Usando resultados de toocompare AUC
Área na curva (AUC) é uma métrica que representa uma medida global de *Separabilidade* entre as distribuições de saudação de pontuações para populações positivas e negativas. É um gráfico de característica de operador do receptor (ROC) tradicional toohello semelhantes, mas uma diferença importante é a que métrica AUC Olá não exige que você toochoose um valor de limite. Em vez disso, resume os resultados de saudação sobre **todos os** opções possíveis. Por outro lado, gráfico ROC tradicional Olá mostra taxa positivo Olá no eixo vertical hello e Olá falsos positivos no eixo horizontal hello e Olá classificação limite varia.   

AUC geralmente é usado como uma medida de vale a pena para algoritmos diferentes (ou sistemas diferentes) porque ela permite modelos toobe comparado por meio de seus valores AUC. Essa é uma abordagem popular em setores como meteorologia e biociência. Assim, a AUC representa uma ferramenta popular para avaliar o desempenho de um classificador.  

### <a name="comparing-misclassification-rates"></a>Comparando as taxas de classificação incorreta
Comparamos taxas de misclassification Olá Olá de conjunto de dados em questão usando dados CRM saudação de aproximadamente 8.000 assinaturas.  

* taxa de misclassification SAS Olá foi 10 a 15%.
* taxa de misclassification Olá estúdio de aprendizado de máquina foi 15 a 20% para churners do hello superior 200-300.  

No setor de telecomunicações Olá, é importante tooaddress somente aqueles clientes que têm Olá toochurn de risco mais alto, oferecendo-los um serviço de assistente ou outros tratamento especial. Nesse ponto, implementação do estúdio de aprendizado de máquina hello gera resultados no modelo SAS hello.  

Por Olá mesmo token, a precisão é mais importante do que a precisão porque principalmente estamos interessados em Classificar corretamente churners potenciais.  

Olá diagrama a seguir da Wikipedia descreve a relação de saudação em um gráfico animado, fáceis de entender:  

![][8]

*Figura 10: Troca entre exatidão e precisão*

### <a name="accuracy-and-precision-results-for-boosted-decision-tree-model"></a>Resultados de precisão e exatidão para modelo de árvore de decisão aprimorado
Olá gráfico exibe Olá bruto a seguir resulta de pontuação usando o protótipo de aprendizado de máquina Olá para o modelo de árvore de decisão ampliada de saudação, que acontece toobe hello mais preciso entre quatro modelos de saudação:  

![][9]

*Figura 11: Características do modelo de árvore de decisão aprimorado*

## <a name="performance-comparison"></a>Comparação de desempenho
Comparamos velocidade Olá em que dados foi classificados usando modelos de estúdio de aprendizado de máquina hello e um modelo de comparável criados usando a edição de área de trabalho de saudação do SAS Enterprise mineração 12.1.  

Olá a tabela a seguir resume o desempenho de saudação de algoritmos de saudação:  

*Tabela 1. Desempenho geral (precisão) de algoritmos de saudação*

| LR | BT | AP | SVM |
| --- | --- | --- | --- |
| Modelo médio |Olá melhor modelo |Subdesempenhando |Modelo médio |

modelos de saudação hospedados no estúdio de aprendizado de máquina superaram SAS por 15 a 25% para velocidade de execução, mas a precisão foi amplamente em par.  

## <a name="discussion-and-recommendations"></a>Discussão e recomendações
No setor de telecomunicações hello, várias práticas prontas tooanalyze variação, incluindo:  

* As métricas se derivam de quatro categorias essenciais:
  * **Entidade (por exemplo, uma assinatura)**. Fornecer informações básicas sobre assinatura hello e/ou cliente que é o assunto de saudação da variação.
  * **Atividade**. Obter todas as informações de uso possíveis que é a entidade toohello relacionados, por exemplo, número de saudação de logons.
  * **Atendimento ao cliente**. Coletar informações do cliente suporte logs tooindicate se a assinatura de Olá tinha interações com clientes ou problemas de suporte.
  * **Dados empresariais e de concorrência**. Obter informações possíveis sobre cliente hello (por exemplo, pode ser tootrack indisponível ou disco rígido).
* Use seleção de recursos de toodrive de importância. Isso implica que modelo de árvore de decisão ampliada de saudação é sempre uma abordagem promessa.  

Olá uso destas quatro categorias cria Olá ilusão que um simples *determinística* abordagem, com base em índices formados razoável fatores por categoria, deve ser suficiente para clientes tooidentify correm risco de variação. Infelizmente, apesar de esse conceito parecer plausível, ele não é verdadeiro. motivo Olá é que a variação é um efeito temporal e fatores Olá contribuindo toochurn geralmente estão em estados transitórios. O que leva um cliente tooconsider deixando hoje pode ser diferente amanhã e certamente será diferente seis meses a partir de agora. Assim, um modelo *probabilístico* é necessário.  

Essa observação importante muitas vezes é ignorada nos negócios, que geralmente prefere um tooanalytics abordagem orientada a inteligência de negócios, principalmente como é fácil vender e admite automação simples.  

No entanto, a promessa de saudação de análises de autoatendimento usando o estúdio de aprendizado de máquina é quatro categorias de saudação de informação, executar o downgrade por divisão ou departamento, tornam-se uma fonte valiosa para aprendizado de máquina sobre variação.  

Outro recurso interessante as novidades no aprendizado de máquina do Azure é Olá capacidade tooadd um repositório de toohello módulo personalizado de módulos predefinidos que já estão disponíveis. Esse recurso, essencialmente, cria uma oportunidade tooselect bibliotecas e criar modelos para mercados verticais. É um diferenciador importante de aprendizado de máquina do Azure no mercado hello.  

Esperamos que toocontinue este tópico na análise de dados do hello toobig futuras, especialmente relacionados.
  

## <a name="conclusion"></a>Conclusão
Este documento descreve um problema abordagem sensato tootackling Olá comum de rotatividade de cliente usando uma estrutura genérica. Consideramos um protótipo para modelos de pontuação e o implementamos usando o Azure Machine Learning. Por fim, é avaliada precisão hello e o desempenho da solução de protótipo Olá com algoritmos de toocomparable relação na SAS.  

**Para obter mais informações:**  

Este documento foi útil para você? Por favor, nos dê seu feedback. Conte-nos em uma escala de 1 too5 (ruim) (excelente), como você classificaria este documento e por que você forneceu-esta classificação? Por exemplo:  

* Sua classificação é alta devido toohaving bons exemplos, excelentes capturas de tela, redação clara ou outro motivo?
* Sua classificação é baixa devido toopoor exemplos, capturas de tela difusa ou gravação clara?  

Esses comentários nos ajudarão a melhorar a qualidade de saudação do white papers que lançamos.   

[Enviar comentários](mailto:sqlfback@microsoft.com).
 

## <a name="references"></a>Referências
[1] análise preditiva: além de previsões hello, w. McKnight, gerenciamento de informações, julho/agosto de 2011, p.18-20.  

[2] Artigo na Wikipédia: [Precisão e exatidão](http://en.wikipedia.org/wiki/Accuracy_and_precision)

[3] [CRISP-DM 1.0: Step-by-Step Data Mining Guide](http://www.the-modeling-agency.com/crisp-dm.pdf)   

[4] [Marketing de Big Data: envolva seus clientes com mais eficiência e agregue valor](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn)

[5] [Modelo de variação de telecomunicações](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5) na [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/) 
 

## <a name="appendix"></a>Apêndice
![][10]

*Figura 12: Instantâneo de uma apresentação de protótipo de variação*

[1]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-1.png
[2]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-2.png
[3]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-3.png
[4]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-4.png
[5]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-5.png
[6]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-6.png
[7]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-7.png
[8]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-8.png
[9]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-9.png
[10]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-10.png
