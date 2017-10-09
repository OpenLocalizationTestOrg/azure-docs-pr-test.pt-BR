---
title: "aaaClean e preparar dados para o aprendizado de máquina do Azure | Microsoft Docs"
description: "Pré-processar e limpar dados tooprepare para aprendizado de máquina."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: bdf659ec-4881-4324-8b9c-747cbfa0c3cd
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 3e3c3e4b0cfb9187f5820d7165e6ee1ea013ba02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tasks-tooprepare-data-for-enhanced-machine-learning"></a>Dados de tooprepare de tarefas de aprendizado de máquina avançada
O pré-processamento e a limpeza de dados são tarefas importantes e geralmente devem ser realizadas antes que o conjunto de dados possa ser usado com eficiência para o aprendizado de máquina. Dados brutos costumam conter ruídos e não são confiáveis, e pode haver valores ausentes. Usar esses dados para a modelagem pode produzir resultados incorretos. Essas tarefas fazem parte do processo de ciência de dados da equipe (TDSP) do hello e geralmente seguem uma exploração inicial de um toodiscover de conjunto de dados usado e o plano Olá pré-processamento necessário. Para obter instruções sobre o processo TDSP hello mais detalhadas, consulte as etapas de Olá descritas Olá [processo de ciência de dados de equipe](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

Pré-processando e tarefas de limpeza, como tarefa de exploração de dados hello, podem ser executadas em uma ampla variedade de ambientes, como SQL ou Hive ou estúdio de aprendizado de máquina do Azure e com várias ferramentas e linguagens, como Python, dependendo de onde os dados estão ou de R armazenados e como ele é formatado. Como TDSP é iterativa por natureza, essas tarefas podem ocorrer em várias etapas do fluxo de trabalho de saudação do processo de saudação.

Este artigo apresenta vários conceitos e tarefas de processamento de dados que podem ser executados antes ou depois da ingestão de dados no Azure Machine Learning.

Para obter um exemplo de exploração de dados e pré-processamento feito no studio de aprendizado de máquina do Azure, consulte Olá [pré-processamento de dados no estúdio de aprendizado de máquina do Azure](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/) vídeo.

## <a name="why-pre-process-and-clean-data"></a>Por que pré-processar e limpar os dados?
Coleta de dados do mundo real de várias fontes e processos e podem conter irregularidades ou dados corrompidos comprometer a qualidade de saudação do conjunto de dados de saudação. problemas de qualidade de dados típicos de saudação que podem surgir são:

* **Incompleto**: os dados não têm atributos ou contém valores ausentes.
* **Com ruído**: Os dados contêm registros incorretos ou exceções.
* **Inconsistente**: os dados contêm registros conflitantes ou discrepâncias.

Dados de qualidade são um pré-requisito para modelos de previsão de qualidade. tooavoid "lixo no lixo out" e melhorar a qualidade de dados e, portanto, o desempenho de modelo, é fundamental tooconduct um toospot de tela de integridade de dados dados problemas no início e decidir sobre Olá correspondente de processamento de dados e as etapas de limpeza.

## <a name="what-are-some-typical-data-health-screens-that-are-employed"></a>Poderia dar exemplo de filtragens de integridade de dados típicas empregadas?
Podemos verificar a qualidade geral Olá dos dados, marcando:

* Olá inúmeros **registros**.
* Olá inúmeros **atributos** (ou **recursos**).
* atributo Olá **tipos de dados** (nominal, ordinal ou contínuo).
* Olá inúmeros **valores ausentes**.
* **Validez** de dados de saudação.
  * Se dados saudação em TSV ou CSV, verifique que separadores de coluna hello e separadores de linha sempre corretamente separam colunas e linhas.
  * Se dados saudação estão no formato HTML ou XML, verifique se os dados de saudação está bem formados com base em seus respectivos padrões.
  * Análise também pode ser necessária nas informações de tooextract estruturado de ordem de dados estruturados ou não estruturados.
* **Registros de dados inconsistentes**. Verifique o intervalo de saudação de valores são permitidos. Por exemplo, se dados saudação contém GPA aluno, verifique se o hello designado intervalo, Olá GPA dizer 0 ~ 4.

Quando você encontrar problemas com dados, **etapas de processamento** é necessário que geralmente envolve a limpeza de valores ausentes, normalização de dados, diferenciação, tooremove de processamento de texto e/ou substituir caracteres inseridos que podem afetar o alinhamento de dados mistos tipos de dados em comum campos e outros.


            **O Azure Machine Learning consome dados tabulares bem formados**.  Se dados saudação já estão em formato tabular, o pré-processamento de dados pode ser executado diretamente com o aprendizado de máquina do Azure no hello estúdio de aprendizado de máquina.  Se os dados não estão em formato tabular, digamos que ela está em análise de XML, podem ser necessário no formulário do pedido tooconvert Olá dados tootabular.  

## <a name="what-are-some-of-hello-major-tasks-in-data-pre-processing"></a>Quais são algumas das tarefas mais importantes Olá de pré-processamento de dados?
* **Limpeza de dados**: preencher ou valores ausentes, detectar e remover exceções e dados com ruídos.
* **Transformação de dados**: normalizar tooreduce dimensões e dados ruído.
* **Redução de dados**: registros de dados de exemplo ou atributos para fácil manipulação de dados.
* **Diferenciação de dados**: Convert contínua atributos toocategorical atributos para facilidade de uso com determinados métodos de aprendizado de máquina.
* **Limpeza de texto**: remover caracteres inseridos que podem causar desalinhamento de dados, como por exemplo guias incorporadas em um arquivo de dados separado por tabulações, novas linhas incorporadas que podem quebrar registros, etc.

seções de saudação abaixo detalham algumas dessas etapas de processamento de dados.

## <a name="how-toodeal-with-missing-values"></a>Como valores toodeal com ausente?
toodeal com valores ausentes, é melhor toofirst identificar o motivo de saudação para ausente Olá valores problema de saudação do identificador toobetter. Métodos de manipulação de valores ausentes típicos são:

* **Exclusão**: remover os registros com valores ausentes
* **Substituição fictícia**: substituir os valores ausentes por um valor fictício: por exemplo, *desconhecido* para valores categóricos ou 0 para valores numéricos.
* **Média de substituição**: se os dados ausentes Olá forem numéricos, substituir valores ausentes Olá por média de saudação.
* **Frequência de substituição**: se dados ausentes Olá forem categóricos, substituir valores ausentes Olá item mais frequente Olá
* **Substituição de regressão**: Use um método de regressão tooreplace ausente valores com valores retornados.  

## <a name="how-toonormalize-data"></a>Como os dados toonormalize?
Dados normalização novamente dimensiona os valores numéricos tooa o intervalo especificado. Métodos de normalização de dados populares incluem:

* **Normalização Mín-Máx**: linearmente transformar o intervalo de tooa dados hello, digamos, entre 0 e 1, onde hello o valor mínimo é dimensionado too0 e too1 do valor máximo.
* **Normalização da pontuação Z**: Dimensionar dados com base na média e desvio padrão: dividir a diferença de saudação entre dados saudação e média de saudação pelo desvio padrão de saudação.
* **Escala decimal**: Dimensionar dados saudação mover ponto decimal de saudação do valor de atributo hello.  

## <a name="how-toodiscretize-data"></a>Como os dados toodiscretize?
Dados podem ser diferenciados convertendo atributos de toonominal valores contínuos ou intervalos. Algumas formas de fazer isso são:

* **Compartimentalização de largura igual**: divida o intervalo de saudação de todos os valores possíveis de um atributo em grupos de N de saudação mesmo tamanho e atribuir valores de saudação que se enquadram em um binário com número de gaveta hello.
* **Compartimentalização de altura igual**: divida o intervalo de saudação de todos os valores possíveis de um atributo em grupos de N, cada uma contendo Olá o mesmo número de instâncias, em seguida, atribuir Olá valores que se enquadram em um binário com hello guardar o número.  

## <a name="how-tooreduce-data"></a>Como os dados tooreduce?
Há vários métodos tooreduce tamanho de dados mais fácil manipulação de dados. Dependendo do tamanho e hello domínio, Olá métodos a seguir pode ser aplicada:

* **Registre a amostragem**: registros de dados de saudação de exemplo e escolha somente subconjunto representativo Olá dados saudação.
* **Atributo amostragem**: selecione apenas um subconjunto dos atributos mais importantes Olá dos dados de saudação.  
* **Agregação**: dividir dados saudação em grupos e armazenar números Olá para cada grupo. Por exemplo, hello receita diária números de uma cadeia de restaurante sobre Olá 20 anos anteriores podem ser agregados tamanho dos dados de saudação da toomonthly receita tooreduce hello.  

## <a name="how-tooclean-text-data"></a>Como os dados de texto tooclean?
**Campos de texto em dados tabulares** podem incluir caracteres que afetam os alinhamentos das colunas e/ou limites de registros. Por exemplo, guias incorporadas em um arquivo separado por tabulações causa desalinhamento de coluna e caracteres de nova linha incorporados quebram linhas de registros. Texto inadequado codificação tratamento durante a gravação/leitura texto leva tooinformation perda, inadvertida introdução dos caracteres ilegíveis, por exemplo, nulos e pode também afetam análise de texto. Análise cuidadosa e edição podem ser necessário em campos de texto tooclean ordem para alinhamento adequado e/ou dados de tooextract estruturado de dados de texto não estruturados ou semiestruturados.

**Exploração de dados** oferece uma visão antecipada de dados saudação. Um número de problemas de dados pode ser descoberto durante esta etapa e métodos correspondentes podem ser aplicadas tooaddress esses problemas.  É importante tooask perguntas, como o que é a origem de saudação do problema de saudação e como problema Olá pode ter sido introduzido. Isso também ajuda você a decidir sobre etapas de processamento de dados de saudação que toobe necessidade tomada tooresolve-los. tipo de saudação do insights um pretenda tooderive de dados de saudação também pode ser esforço de processamento de dados de saudação tooprioritize usado.

## <a name="references"></a>Referências
> *Data Mining: Concepts and Techniques*, Third Edition, Morgan Kaufmann, 2011, Jiawei Han, Micheline Kamber e Jian Pei
> 
> 

