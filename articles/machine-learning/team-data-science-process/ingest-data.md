---
title: "Carregar dados em ambientes de armazenamento do Azure para análise | Microsoft Docs"
description: Mover dados de e para o Armazenamento de Blobs do Azure
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: cgronlun
editor: cgronlun
ms.assetid: b8fbef77-3e80-4911-8e84-23dbf42c9bee
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/09/2017
ms.author: bradsev
ms.openlocfilehash: 7d7da4f6dfed03d470c5b5706aaf412c07096120
ms.sourcegitcommit: bc8d39fa83b3c4a66457fba007d215bccd8be985
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2017
---
# <a name="load-data-into-storage-environments-for-analytics"></a>Carregar dados em ambientes de armazenamento para análise
O Processo de Ciência de Dados de Equipe exige que os dados sejam incluídos ou carregados em uma variedade de ambientes de armazenamento diferentes para serem processados ou analisados da maneira mais apropriada em cada estágio do processo. Os destinos de dados geralmente usados para processamento incluem Armazenamento de Blobs do Azure, bancos de dados do SQL Azure, SQL Server na VM do Azure, HDInsight (Hadoop) e Azure Machine Learning. 

[!INCLUDE [cap-ingest-data-selector](../../../includes/cap-ingest-data-selector.md)]

Esse **menu** liga os tópicos que descrevem como ingerir dados em ambientes de destino nos quais os dados podem ser armazenados e processados.

Necessidades comerciais e técnicos, bem como o local inicial, formato e tamanho de seus dados que determinarão os ambientes de destino no qual os dados precisam ser incluídos para atingir as metas de sua análise. Não é incomum para um cenário exigir dados a serem movidos entre vários ambientes para atingir a variedade de tarefas necessárias para construir um modelo de previsão. Essa sequência de tarefas pode incluir, por exemplo, a exploração de dados, pré-processamento, limpar, redução da resolução e treinamento de modelo.

