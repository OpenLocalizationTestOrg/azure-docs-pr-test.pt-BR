---
title: "Estágio de entendimento de negócios do ciclo de vida do Processo de Ciência de Dados da Equipe – Azure | Microsoft Docs"
description: "As metas, as tarefas e as entregas do estágio de entendimento de negócios dos seus projetos de ciência de dados"
services: machine-learning
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/04/2017
ms.author: bradsev;
ms.openlocfilehash: 82784cbfd5f12297c376a395b54a817a2ae915a5
ms.sourcegitcommit: 93902ffcb7c8550dcb65a2a5e711919bd1d09df9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="business-understanding"></a>Noções básicas sobre negócios

Este tópico descreve as metas, as tarefas e as entregas associadas ao estágio de entendimento de negócios do TDSP (Processo de Ciência de Dados da Equipe). Esse processo fornece um ciclo de vida recomendado que você pode usar para estruturar seus projetos de ciência de dados. O ciclo de vida descreve os estágios principais que os projetos normalmente executam, com frequência de modo iterativo:

   1. **Noções básicas sobre negócios**
   2. **Aquisição de dados e entendimento**
   3. **Modelagem**
   4. **Implantação**
   5. **Aceitação do cliente**

Aqui está uma representação visual do ciclo de vida do TDSP: 

![Ciclo de vida do TDSP](./media/lifecycle/tdsp-lifecycle2.png) 


## <a name="goals"></a>Metas
* Especifique as principais variáveis que devem servir como metas modelo e cujas métricas relacionadas são usadas para determinar o sucesso do projeto.
* Identifique as fontes de dados relevantes, às quais a empresa tem acesso ou precisa obtê-lo.

## <a name="how-to-do-it"></a>Como fazer isso
Há duas tarefas principais abordadas neste estágio: 

   * **Definir os objetivos**: trabalhe com o cliente e outros stakeholders para compreender e identificar problemas de negócios. Formule perguntas que definem as metas de negócios e que as técnicas de ciência de dados podem ter como meta.
   * **Identificar as fontes de dados**: encontre os dados relevantes que ajudam a responder as perguntas que definem os objetivos do projeto.

### <a name="define-objectives"></a>Definir os objetivos
1. Um objetivo central desta etapa é identificar as principais variáveis de negócios que a análise precisa prever. Chamamos tais variáveis de *metas modelo* e usamos as métricas associadas a elas para determinar o sucesso do projeto. Dois exemplos dessas metas são a previsão de vendas ou a probabilidade de que um pedido seja fraudulento.

2. Defina as metas do projeto, fazendo perguntas e refinando perguntas “inteligentes” que são relevantes, específicas e inequívocas. A ciência de dados é o processo de usar nomes e números para responder a essas perguntas. Para saber mais sobre como fazer perguntas inteligentes, veja o blog [Como usar a Ciência de Dados](https://blogs.technet.microsoft.com/machinelearning/2016/03/28/how-to-do-data-science/). A ciência de dados e o aprendizado de máquina são normalmente usados para responder a cinco tipos de perguntas:
 
   * Quanto custa ou quantos? (regressão)
   * Qual categoria? (classificação)
   * Qual grupo? (clustering)
   * Isso é estranho? (detecção de anomalias)
   * Qual opção deve ser escolhida? (recomendação)

   Determine quais dessas perguntas você está fazendo e como suas respostas alcançam suas metas de negócios.

3. Defina a equipe do projeto especificando as funções e responsabilidades dos membros. Desenvolva um plano de marcos de alto nível que pode ser usado para iteração, conforme mais informações são descobertas. 

4. Defina as métricas de sucesso. Por exemplo, pode ser útil obter uma previsão de variação de cliente. Você precisa de uma taxa de precisão de “x” por cento no final deste projeto de três meses. Com esses dados, você pode oferecer promoções aos clientes para reduzir a variação. As métricas devem ser **SMART** (INTELIGENTES): 

   * E**S**pecíficas 
   * **M**ensuráveis
   * **A**lcançáveis 
   * **R**elevantes 
   * Com limite de **T**empo 

### <a name="identify-data-sources"></a>Identificar as fontes de dados
Identifique as fontes de dados que contêm exemplos conhecidos de respostas para as perguntas inteligentes. Procure os seguintes dados:

* Dados que são relevantes à pergunta. Você tem medidas da meta e os recursos relacionados a ela?
* Dados que são uma medida precisa de nossa meta modelo e os recursos de interesse.

Por exemplo, você pode descobrir que os sistemas existentes precisam coletar e registrar tipos de dados adicionais para solucionarem o problema e atingirem os objetivos do projeto. Nesse caso, pode ser útil buscar fontes de dados externas ou atualizar os sistemas para coletar novos dados.

## <a name="artifacts"></a>Artefatos
Estas são as entregas deste estágio:

   * [Documento de estatuto](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Charter.md): um modelo padrão é fornecido na definição de estrutura do projeto TDSP. O estatuto é um documento vivo. O modelo é atualizado durante o projeto conforme novas descobertas são feitas e os requisitos de negócios mudam. O segredo é a iteração neste documento, com a adição de mais detalhes, à medida que você avança no processo de descoberta. Mantenha o cliente e outros stakeholders envolvidos no processo de mudança e comunique os motivos das mudanças de forma clara.  
   * [Fontes de Dados](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#raw-data-sources): a seção **Fontes de dados brutos** do relatório **Definições de dados** encontrado na pasta **Relatório de dados** do projeto do TDSP contém as fontes de dados. Esta seção especifica os locais de origem e destino dos dados brutos. Em estágios posteriores, você preencherá outros detalhes como scripts para mover os dados para seu ambiente de análise.  
   * [Dicionários de Dados](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/Data_Dictionaries): este documento fornece descrições dos dados fornecidos pelo cliente. Essas descrições incluem informações sobre o esquema (tipos de dados, informações sobre regras de validação, se houver) e os diagramas de relação de entidade, se disponíveis.

## <a name="next-steps"></a>Próximas etapas

Aqui estão os links para cada etapa do ciclo de vida do TDSP:

   1. [Noções básicas sobre negócios](lifecycle-business-understanding.md)
   2. [Aquisição de dados e entendimento](lifecycle-data.md)
   3. [Modelagem](lifecycle-modeling.md)
   4. [Implantação](lifecycle-deployment.md)
   5. [Aceitação do cliente](lifecycle-acceptance.md)

Fornecemos passo a passo completos que demonstram todas as etapas do processo para cenários específicos. O artigo [Passo a passos de exemplo](walkthroughs.md) fornece uma lista dos cenários com descrições de links e miniaturas. Os passo a passo ilustram como combinar ferramentas e serviços de nuvem e locais em um fluxo de trabalho ou pipeline para criar um aplicativo inteligente. 

Para obter exemplos de como executar etapas nos TDSPs que usam o Azure Microsoft Azure Machine Learning Studio, consulte [Use the TDSP with Azure Machine Learning](http://aka.ms/datascienceprocess) (Usar o TDSP com o Azure Machine Learning).
