---
title: Processamento de eventos em tempo real com o processamento de eventos do Stream Analytics | Microsoft Docs
description: "Saiba como um conjunto de serviços do Azure pode interoperar para habilitar a análise e o processamento de eventos em tempo real."
keywords: "processamento em tempo real, processamento de eventos, arquitetura de referência"
services: stream-analytics,event-hubs,storage,sql-database
documentationcenter: 
author: samacha
manager: jhubbard
editor: 
ms.assetid: 11af48bc-313c-4527-8c80-91088dc9f3c6
ms.service: stream-analytics
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: samacha
ms.openlocfilehash: a5206f74e61c3cfd210ff80654e31f466ce08977
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2017
---
# <a name="reference-architecture-real-time-event-processing-with-microsoft-azure-stream-analytics"></a>Arquitetura de referência: processamento de eventos em tempo real com o Stream Analytics do Microsoft Azure
A arquitetura de referência para processamento de eventos em tempo real com o Stream Analytics do Azure se destina a fornecer um plano gráfico genérico para implantar uma solução de processamento de fluxo de PaaS (plataforma como um serviço) em tempo real com o Microsoft Azure.

## <a name="summary"></a>Resumo
Tradicionalmente, as soluções de análise se baseavam em recursos como ETL (extração, transformação, carregamento) e data warehouse, em que os dados são armazenados antes da análise. Mudanças nos requisitos, incluindo dados que chegam mais rapidamente, estão levando esse modelo existente ao limite. A capacidade de analisar os dados em fluxos em movimento antes do armazenamento de movimentação é uma solução e, embora não seja um novo recurso, a abordagem não foi amplamente adotada em todos os segmentos verticais da indústria. 

O Microsoft Azure oferece um catálogo abrangente de tecnologias de análise que são capazes de dar suporte a uma matriz de diferentes requisitos e cenários de solução. A seleção dos serviços do Azure a serem implantados para uma solução de ponta a ponta pode ser um desafio, devido à diversidade de ofertas. Este documento foi projetado descrever os recursos e a interoperação dos vários serviços do Azure que dão suporte a uma solução de fluxo de eventos. Ele também explica alguns dos cenários em que os clientes podem se beneficiar desse tipo de abordagem.

## <a name="contents"></a>Conteúdo
* Resumo executivo
* Introdução à análise em tempo real
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
* [Introdução ao Stream Analytics do Azure](stream-analytics-introduction.md)
* [Introdução ao uso do Stream Analytics do Azure](stream-analytics-real-time-fraud-detection.md)
* [Dimensionar trabalhos do Stream Analytics do Azure](stream-analytics-scale-jobs.md)
* [Referência de Linguagem de Consulta do Stream Analytics do Azure](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Referência da API REST do Gerenciamento do Azure Stream Analytics](https://msdn.microsoft.com/library/azure/dn835031.aspx)

