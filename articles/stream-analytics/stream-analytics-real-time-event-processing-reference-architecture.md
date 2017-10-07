---
title: "processamento com o processamento de eventos de análise de fluxo de eventos de tempo aaaReal | Microsoft Docs"
description: "Saiba como um conjunto de serviços do Azure pode interoperar para habilitar a análise e o processamento de eventos em tempo real."
keywords: "processamento em tempo real, processamento de eventos, arquitetura de referência"
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: jeffstok
ms.openlocfilehash: a43c503d709609ba61e9932822d30bc2208906ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a>Arquitetura de referência: processamento de eventos em tempo real com o Stream Analytics do Microsoft Azure
arquitetura de referência de saudação para processamento com o Azure Stream Analytics de eventos em tempo real é pretendida tooprovide um projeto de genérico para a implantação de uma plataforma em tempo real como uma solução de processamento de fluxo de serviço (PaaS) com o Microsoft Azure.

## <a name="summary"></a>Resumo
Tradicionalmente, as soluções de análise baseadas em recursos, como ETL (extrair, transformar, carregar) e o data warehouse, onde os dados são armazenados tooanalysis anterior. Requisitos de alteração, incluindo mais dados tardios rapidamente, sendo transferida para esse limite de toohello modelo existente. dados de tooanalyze capacidade Hello dentro de movimentação toostorage anterior de fluxos são uma solução e, embora não seja um novo recurso, abordagem de saudação não foi amplamente adotada em todos os mercados verticais. 

O Microsoft Azure oferece um catálogo abrangente de tecnologias de análise que são capazes de dar suporte a uma matriz de diferentes requisitos e cenários de solução. Selecionar quais toodeploy os serviços do Azure para uma solução de ponta a ponta pode ser um desafio dado a gama de ofertas hello. Este documento é projetado toodescribe Olá recursos e interoperação de Olá vários serviços do Azure que oferecem suporte a uma solução de fluxo de eventos. Ele também explica alguns dos cenários de saudação em que os clientes podem aproveitar esse tipo de abordagem.

## <a name="contents"></a>Conteúdo
* Resumo executivo
* Análise de tempo de tooReal de Introdução
* Proposta de valor de dados em tempo real no Azure
* Cenários comuns de análise em tempo real
* Arquitetura e componentes
  * Fontes de dados
  * Camada de integração de dados
  * Camada de análise em tempo real
  * Camada de armazenamento de dados
  * Camada de apresentação/consumo
* Conclusão

**Autor:** Charles Feddersen, arquiteto de soluções, Data Insights Center of Excellence, Microsoft Corporation

**Publicação:** janeiro de 2015

**Revisão:** 1.0

**Download:** [Processamento de eventos em tempo real com o Stream Analytics do Microsoft Azure](http://download.microsoft.com/download/6/2/3/623924DE-B083-4561-9624-C1AB62B5F82B/real-time-event-processing-with-microsoft-azure-stream-analytics.pdf)

## <a name="get-help"></a>Obter ajuda
Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooAzure Stream Analytics](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

