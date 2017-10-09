---
title: "Olá aaaUse modo de execução de vértice no Data Lake Tools para Visual Studio | Microsoft Docs"
description: "Saiba como toouse Olá trabalhos de análise Data Lake tooexam exibição de execuções de vértice."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a>Olá Use exibição de execuções de vértice no Data Lake Tools para Visual Studio
Saiba como toouse Olá trabalhos de análise Data Lake tooexam exibição de execuções de vértice.

## <a name="prerequisites"></a>Pré-requisitos

É necessário um conhecimento básico de como usar Data Lake Tools para o script do Visual Studio toodevelop U-SQL.  Confira [Tutorial: desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).

## <a name="open-hello-vertex-execution-view"></a>Olá abrir modo de execução de vértice
Abra um trabalho de U-SQL em Ferramentas do Data Lake para Visual Studio. Clique em **exibição de execuções de vértice** no canto do hello inferior esquerdo. Você pode ser perfis tooload solicitada pela primeira vez e pode levar algum tempo dependendo de sua conectividade de rede.

![Modo de Exibição de Execução de Vértice das Ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a>Noções básicas do Modo de Exibição de Execução de Vértice
Olá vértice execução exibição tem três partes:

![Modo de Exibição de Execução de Vértice das Ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

Olá **seletor de vértice** permite esquerdo Olá você seleciona vértices pelos recursos (como top 10 dados de leitura, ou optar por estágio). Um dos filtros usados com mais frequência do hello é Olá toosee **vértices no caminho crítico**. Olá **caminho crítico** Olá a cadeia mais longa dos vértices de um trabalho de U-SQL. Caminho crítico de saudação compreensão é útil para otimizar seus trabalhos verificando quais vértice leva tempo mais longo de saudação.
  
![Modo de Exibição de Execução de Vértice das Ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

painel da parte superior central de saudação mostra Olá **executando o status de todos os vértices de saudação**.
  
![Modo de Exibição de Execução de Vértice das Ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

Painel de central Olá inferior mostra informações sobre cada vértice:
* Nome de processo: nome de saudação da instância de vértice hello. Ele é composto por diferentes partes em StageName|VertexName|VertexRunInstance. Por exemplo, vértice de .v1 [62] Olá SV7_Split representa Olá segunda instância em execução (.v1, índice a partir de 0) do número de vértice 62 no estágio SV7_Split.
* Gravadas/leitura total de dados: dados saudação foram lida/gravada por este vértice.
* Status de estado/saída: Olá status final quando vértice Olá é finalizada.
* Tipo de falha do código de saída: erro de saudação ao vértice Olá falha.
* Motivo da criação: Por que vértice Olá foi criado.
* Latência de fila do recurso latência/processo latência/NP: Olá tempo para Olá vértice toowait para toostay na fila hello, tooprocess dados e recursos.
* GUID de processo/criador: GUID vértice de execução atual hello ou seu criador.
* Versão: instância Olá N-ésimo da saudação executando vértice (o sistema Olá pode agendar novas instâncias de um vértice para muitos motivos, por exemplo, o failover, computação redundância, etc.)
* Hora da Criação da Versão.
* Processar criar Iniciar processo/tempo na fila tempo/processo Iniciar tempo/processo concluir tempo: criação; iniciado o processo de vértice de saudação Quando o processo de vértice de saudação começa tooqueue; Olá quando determinados início do processo de vértice; Quando hello determinados vértice é concluída.

## <a name="next-steps"></a>Próximas etapas
* toolog informações de diagnóstico, consulte [acessar logs de diagnóstico para análise do Azure Data Lake](data-lake-analytics-diagnostic-logs.md)
* toosee uma consulta mais complexa, consulte [site analisar logs usando a análise do Azure Data Lake](data-lake-analytics-analyze-weblogs.md).
* detalhes do trabalho tooview, consulte [navegador de trabalho de uso e a exibição de trabalho de trabalhos da análise Azure Data lake](data-lake-analytics-data-lake-tools-view-jobs.md)
