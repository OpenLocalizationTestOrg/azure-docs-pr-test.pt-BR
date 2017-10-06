---
title: "cenários de aaaIdentify e planejar o processo de análise - Azure | Microsoft Docs"
description: "Planeje a análise avançada considerando uma série de perguntas importantes."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 421520dd-7728-4d29-889c-ebe6a0a6fb07
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: e445973be0d020a4f9949e5c9d8554fbbd4b515f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooidentify-scenarios-and-plan-for-advanced-analytics-data-processing"></a>Como tooidentify cenários e planejar avançado processamento de dados de análise
Quais recursos deve planejar tooinclude quando configurar um ambiente toodo avançado de processamento em um conjunto de dados de análise? Este artigo sugere uma série de perguntas tooask que ajuda a identificar recursos relevantes e tarefas de saudação do cenário. ordem de saudação de etapas de alto nível para análise preditiva é descrita em [novidades Olá processo de ciência de dados da equipe (TDSP)?](data-science-process-overview.md). Cada uma dessas etapas exigirá recursos específicos para o cenário em particular Olá tarefas tooyour relevantes. Olá tooidentify perguntas mais importantes de seu cenário preocupação dados logística, características, qualidade de saudação de conjuntos de dados Olá e ferramentas de saudação e idiomas que você preferir toodo análise de saudação.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="logistic-questions-data-locations-and-movement"></a>Perguntas sobre logística: locais e movimentação de dados
perguntas logística Olá diz respeito a localização de saudação do hello **fonte de dados**, Olá **destino** no Azure e requisitos para mover os dados hello, inclusive agendamento hello, quantidade e recursos envolvidos. Talvez seja necessário toobe movido várias vezes durante o processo de análise de saudação dados saudação. Um cenário comum é toomove locais de dados em alguma forma de armazenamento no Azure e, em seguida, no estúdio de aprendizado de máquina.

1. **Qual é a sua fonte de dados?** É local ou na nuvem Olá? Por exemplo:
   
   * dados de saudação são publicamente disponíveis em um endereço HTTP.
   * dados de saudação residem em um local de arquivo local/rede.
   * dados de saudação estão em um banco de dados do SQL Server.
   * Olá dados são armazenados em um contêiner de armazenamento do Azure
2. **O que é Olá destino do Azure?** Em que ele precisa toobe para processar ou modelagem? Por exemplo:
   
   * Armazenamento do Blobs do Azure
   * Bancos de dados do SQL Azure
   * SQL Server em VM do Azure
   * Tabelas do HDInsight (Hadoop no Azure) ou do Hive
   * Azure Machine Learning
   * Discos rígidos virtuais montáveis do Azure.
3. **Como você vai dados de saudação toomove?**  Olá procedimentos e os recursos disponíveis tooingest ou carregar dados em uma variedade de armazenamento diferentes e ambientes de processamento são descritos nos Olá tópicos a seguir.
   
   * [Carregar dados em ambientes de armazenamento para análise](machine-learning-data-science-ingest-data.md)
   * 
            [Importar os dados de treinamento para o Azure Machine Learning Studio de diferentes fontes de dados](machine-learning-data-science-import-data.md).
4. **Dados de saudação precisa toobe movidos em um agendamento regular ou modificadas durante a migração?** Considere o uso de fábrica de dados do Azure (AAD) quando dados necessidades toobe continuamente migrada, especialmente se um cenário híbrido que acessa locais e recursos de nuvem está envolvido, ou quando dados saudação são transacionados ou precisa toobe modificado ou tem lógica de negócios adicionado tooit no curso de saudação do que está sendo migrado. Para obter mais informações, consulte [mover dados de um tooSQL de servidor local no SQL Azure com o Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md)
5. **A quantidade de dados de saudação é tooAzure toobe movido?** Conjuntos de dados que são muito grandes podem exceder a capacidade de armazenamento de saudação de determinados ambientes. Para obter um exemplo, consulte a discussão de saudação de limites de tamanho para o estúdio de aprendizado de máquina na próxima seção, Olá. Em tais casos uma amostra de dados Olá pode ser usada durante a análise de saudação. Para obter detalhes sobre como exemplo de toodown um conjunto de dados em vários ambientes do Azure, consulte [dados Olá, equipe de processo de ciência de dados de exemplo](machine-learning-data-science-sample-data.md).

## <a name="data-characteristics-questions-type-format-and-size"></a>Perguntas sobre características de dados: tipo, formato e tamanho
Essas perguntas é tooplanning chave seu armazenamento e ambientes, cada um dos quais são toovarious apropriado de processamento tipos de dados e cada um dos quais têm determinadas restrições.

1. **Quais são os tipos de dados Olá?** Por exemplo:
   
   * Numérico
   * Categóricos
   * Cadeias de caracteres
   * Binário
2. **Como seus dados estão formatados?** Por exemplo:
   
   * Arquivos simples separados por vírgulas (CSV) ou separados por tabulações (TSV)
   * Compactados ou descompactados
   * Blobs do Azure
   * Tabelas do Hive do Hadoop
   * Tabelas do SQL Server
3. **Qual o tamanho dos seus dados?**
   
   * Pequeno: menos de 2 GB
   * Médio: mais de 2 GB e menos de 10 GB
   * Grande: maior que 10 GB

Considere ambiente do estúdio de aprendizado de máquina do Azure hello, por exemplo:

* Para obter uma lista de formatos de dados hello e tipos suportados pelo estúdio de aprendizado de máquina do Azure, consulte [formatos de dados e tipos de dados suportados](machine-learning-data-science-import-data.md#data-formats-and-data-types-supported) seção.
* Para obter informações sobre limitações de dados para o estúdio de aprendizado de máquina do Azure, consulte Olá **como grande Olá conjunto de dados é possível para meu módulos?** seção [importando e exportando dados para o aprendizado de máquina](machine-learning-faq.md#machine-learning-studio-questions)

Para obter informações sobre limitações de saudação de outros serviços do Azure usados no processo de análise de hello, consulte [assinatura do Azure e limites de serviço, cotas e restrições](../azure-subscription-service-limits.md).

## <a name="data-quality-questions-exploration-and-pre-processing"></a>Perguntas sobre qualidade de dados: exploração e pré-processamento
1. **O que você sabe sobre seus dados?** Explore dados quando você precisar toogain um compreender suas características básicas. Quais padrões ou tendências eles exibem, quais exceções que possuem ou quantos valores estão ausentes. Esta etapa é importante para determinar a extensão de saudação do pré-processamento necessário, para formular hipóteses que podem sugerir recursos mais apropriados hello ou tipo de análise e para formular planos para coleta de dados adicionais. O cálculo de estatísticas descritivas e a plotagem de visualizações são técnicas úteis para a inspeção de dados. Para obter detalhes sobre como tooexplore um conjunto de dados em vários ambientes do Azure, consulte [explorar dados em Olá processo de ciência de dados de equipe](machine-learning-data-science-explore-data.md).
2. **Dados de saudação requer pré-processamento ou limpeza?**
   O pré-processamento e a limpeza de dados são tarefas importantes e geralmente devem ser realizadas antes que o conjunto de dados possa ser usado com eficiência para o aprendizado de máquina. Dados brutos costumam conter ruídos e não são confiáveis, e pode haver valores ausentes. Usar esses dados para a modelagem pode produzir resultados incorretos. Para obter uma descrição, consulte [tarefas tooprepare dados para o aprendizado de máquina avançada](machine-learning-data-science-prepare-data.md).

## <a name="tools-and-languages-questions"></a>Perguntas sobre ferramentas e linguagens
Há muitas opções, dependendo de quais linguagens e ambientes ou ferramentas de desenvolvimento você precisa ou com as quais se sente mais confortável.

1. **Quais idiomas fazer você preferir toouse para análise?**  
   
   * R
   * Python
   * SQL
2. **Quais ferramentas você deve usar para a análise de dados?**
   
   * [Microsoft Azure Powershell](/powershell/azure/overview) -uma linguagem de script usada tooadminister seus recursos do Azure em uma linguagem de script.
   * 
            [Azure Machine Learning Studio](machine-learning-what-is-ml-studio.md)
   * [Revolution Analytics](http://www.revolutionanalytics.com/revolution-r-open)
   * [RStudio](http://www.rstudio.com)
   * [Python Tools para Visual Studio](http://microsoft.github.io/PTVS/)
   * [Anaconda](https://www.continuum.io/why-anaconda)
   * [Notebooks Jupyter](http://jupyter.org/)
   * [Microsoft Power BI](http://powerbi.microsoft.com)

## <a name="identify-your-advanced-analytics-scenario"></a>Identificar seu cenário de análise avançada
Depois de responder perguntas Olá na seção anterior hello, são toodetermine pronto qual cenário de melhor se encaixa em seu caso. cenários de exemplo Hello são descritos em [cenários para análises avançadas no aprendizado de máquina do Azure](machine-learning-data-science-plan-sample-scenarios.md).

