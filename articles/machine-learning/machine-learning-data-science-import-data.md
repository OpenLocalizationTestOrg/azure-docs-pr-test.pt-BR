---
title: "dados de aaaImport no estúdio de aprendizado de máquina | Microsoft Docs"
description: "Como tooimport seus dados no estúdio de aprendizado de máquina do Azure de várias fontes de dados. Saiba quais tipos e formatos de dados têm suporte."
keywords: importar dados, formato de dados, tipos de dados, fontes de dados, dados de treinamento
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c194ee3b-838c-4efe-bb2a-c1d052326216
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: garye;bradsev
ms.openlocfilehash: 830dcdde9d43809900c520a41d6d94a65731ca3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="import-your-training-data-into-azure-machine-learning-studio-from-various-data-sources"></a>Importar os dados de treinamento para o Azure Machine Learning Studio de diferentes fontes de dados
toouse seus próprios dados no estúdio de aprendizado de máquina toodevelop e treinar uma solução de análise de previsão, você pode: 

* carregar dados de um **arquivo local** depois do tempo de sua unidade de disco rígido toocreate um módulo de conjunto de dados no espaço de trabalho
* acessar dados de uma das várias **fontes de dados online** enquanto o teste está em execução usando Olá [importar dados] [ import-data] módulo 
* usar dados de outro **teste** do Azure Machine Learning salvo como um conjunto de dados
* usar dados de um **banco de dados do SQL Server** local

Cada uma dessas opções é descrita em um dos tópicos de saudação no menu de saudação abaixo. Esses tópicos mostram como dados de tooimport desses dados de várias fontes toouse no estúdio de aprendizado de máquina. 

[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

> [!NOTE]
> Há diversos conjuntos de dados de exemplo disponíveis no Machine Learning Studio que você pode usar para treinamento de dados. Para obter informações sobre estas configurações, consulte [usar conjuntos de dados de exemplo hello no estúdio de aprendizado de máquina do Azure](machine-learning-use-sample-datasets.md)).
> 
> 

Este tópico introdutório também discute como tooget dados prontos para usam no estúdio de aprendizado de máquina e descreve quais tipos de dados e formatos de dados têm suporte. 

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

## <a name="get-data-ready-for-use-in-azure-machine-learning-studio"></a>Preparar dados para uso no Azure Machine Learning Studio.
O estúdio de aprendizado de máquina é projetado toowork com dados retangulares ou de tabela, como dados de texto delimitados ou estruturado dados de um banco de dados, embora em algumas circunstâncias não retangulares dados podem ser usados.

É melhor se os dados estiverem relativamente limpos. Ou seja, você desejará tootake respeito problemas como cadeias de caracteres sem aspas antes de carregar dados saudação em sua experiência.

No entanto, há módulos disponíveis no Machine Learning Studio que permitem fazer alguma manipulação de dados dentro do teste. Dependendo de algoritmos de aprendizado de máquina Olá você está usando, talvez seja necessário toodecide como você vai lidar com problemas estruturais de dados, como valores ausentes e dados esparsos e há módulos que podem ajudar com isso. Examinar Olá **transformação de dados** seção da paleta de módulo Olá para módulos que executam essas funções.

A qualquer momento em sua experiência, você pode exibir ou baixar dados Olá produzido por um módulo clicando Olá porta de saída. Dependendo do módulo hello, pode haver download diferentes opções disponíveis ou pode ser capaz de toovisualize dados de saudação em seu navegador da web no estúdio de aprendizado de máquina.

## <a name="data-formats-and-data-types-supported"></a>Formatos e tipos de dados compatíveis
Você pode importar uma variedade de tipos de dados para sua experiência, dependendo de qual mecanismo de você usar dados tooimport e onde ele está vindo:

* Texto sem formatação (.txt)
* Valores separados por vírgulas (CSV) com cabeçalho (.csv) ou sem (.nh.csv)
* Valores separados por tabulação (TSV) com cabeçalho (.tsv) ou sem (.nh.tsv)
* Arquivo do Excel
* Tabela do Azure
* Tabela do Hive
* Tabela de Banco de Dados SQL
* Valores de OData
* Dados de SVMLight (.svmlight) (consulte Olá [SVMLight definição](http://svmlight.joachims.org/) informações de formato)
* Atributo de dados de formato de arquivo de relação (ARFF) (.arff) (consulte Olá [definição ARFF](http://weka.wikispaces.com/ARFF) informações de formato)
* Arquivo zip (.zip)
* Arquivo de espaço de trabalho ou objeto R (.RData)

Se você importar dados em um formato como ARFF que contém metadados, o estúdio de aprendizado de máquina usa esse cabeçalho de saudação toodefine metadados e o tipo de dados de cada coluna.

Se você importar dados, como o formato TSV ou CSV que não inclua esses metadados, estúdio de aprendizado de máquina infere Olá o tipo de dados para cada coluna por amostragem de dados de saudação. Se dados saudação também não tem títulos de coluna, o estúdio de aprendizado de máquina fornece nomes padrão.

Você pode especificar explicitamente ou alterar Olá cabeçalhos e tipos de dados para colunas usando Olá [editar metadados][edit-metadata].

a seguir Olá **tipos de dados** reconhecidos pelo estúdio de aprendizado de máquina:

* Cadeia de caracteres
* Número inteiro
* Duplo
* Booliano
* DateTime
* TimeSpan

O estúdio de aprendizado de máquina usa um tipo de dados interno chamado ***tabela de dados*** toopass dados entre os módulos. Você pode converter explicitamente os dados em formato de tabela de dados usando Olá [converter tooDataset] [ convert-to-dataset] módulo.

Qualquer módulo que aceita formatos diferentes de tabela de dados serão convertidos Olá dados tooData tabela silenciosamente antes de passá-lo toohello próximo módulo.

Se necessário, você pode converter o formato Data Table de volta para o formato CSV, TSV, ARFF ou SVMLight usando outros módulos de conversão.
Examinar Olá **conversões de formato de dados** seção da paleta de módulo Olá para módulos que executam essas funções.

<!-- Module References -->
[convert-to-dataset]: https://msdn.microsoft.com/library/azure/72bf58e0-fc87-4bb1-9704-f1805003b975/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
