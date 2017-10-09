---
title: aaaUse .NET com Hadoop MapReduce no HDInsight baseados em Linux - Azure | Microsoft Docs
description: Saiba como aplicativos de .NET toouse para streaming MapReduce no HDInsight baseados em Linux.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a>Migrar soluções .NET para HDInsight baseados em Windows com base em tooLinux HDInsight

Uso de clusters HDInsight baseados em Linux [Mono (https://mono-project.com)](https://mono-project.com) toorun aplicativos de .NET. Mono permite toouse componentes do .NET, como aplicativos de MapReduce com HDInsight baseados em Linux. Neste documento, saiba como soluções de .NET toomigrate criado para toowork de clusters HDInsight baseados em Windows com Mono no HDInsight baseados em Linux.

## <a name="mono-compatibility-with-net"></a>Compatibilidade de Mono com .NET

O Mono versão 4.2.1 está incluído no HDInsight versão 3.5. Para obter mais informações sobre a versão de saudação do Mono incluído no HDInsight, consulte [versões de componente do HDInsight](hdinsight-component-versioning.md). tooinstall uma versão específica do Mono, consulte Olá [instalação ou atualização Mono](hdinsight-hadoop-install-mono.md) documento.

Para obter informações detalhadas sobre a compatibilidade entre Mono e .NET, consulte Olá [compatibilidade Mono (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) documento.

> [!IMPORTANT]
> estrutura SCP.NET Olá é compatível com Mono. Para obter mais informações sobre como usar SCP.NET com Mono, consulte [topologias de toodevelop c# Use o Visual Studio para Apache Storm no HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="automated-portability-analysis"></a>Análise automatizada de portabilidade

Olá [.NET portabilidade analisador](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) pode ser usado toogenerate um relatório de incompatibilidades entre seu aplicativo e Mono. Use Olá seguindo as etapas tooconfigure Olá analisador toocheck seu aplicativo para a portabilidade Mono:

1. Instalar Olá [.NET portabilidade analisador](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer). Durante a instalação, selecione a versão de saudação do toouse do Visual Studio.

2. No Visual Studio 2015, selecione __analisar__ > __configurações do analisador de portabilidade__e certifique-se de que __4.5__ check-in Olá __Mono__  seção.

    ![4.5 verificados na seção Mono para configurações de analisador Olá](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    Selecione __Okey__ toosave configuração de saudação.

3. Selecione __Analisar__ > __Analisar portabilidade do Assembly__. Selecione Olá assembly que contém sua solução e, em seguida, selecione __abrir__ toobegin analysis.

4. Quando a análise for concluída, selecione __Analisar__ > __Exibir relatórios de análise__. Em __resultados da análise de portabilidade__, selecione __abrir relatório__ tooopen um relatório.

    ![Caixa de diálogo de resultados do analisador de portabilidade](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> Analisador de saudação não pode capturar todos os problemas com sua solução. Por exemplo, um caminho de arquivo de `c:\temp\file.txt` é considerado Okey porque Mono é executado no Windows e o caminho de saudação é válido nesse contexto. No entanto, o caminho de saudação não é válido em uma plataforma Linux.

## <a name="manual-portability-analysis"></a>Análise de portabilidade manual

Realizar uma auditoria manual do seu código usando as informações de Olá Olá [portabilidade do aplicativo (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) documento.

## <a name="modify-and-build"></a>Modificar e criar

Você pode continuar toouse Visual Studio toobuild suas soluções .NET para HDInsight. No entanto, você deve garantir que esse projeto Olá é configurado toouse .NET Framework 4.5.

## <a name="deploy-and-test"></a>Implantar e testar

Depois de modificar sua solução usando Olá recomendações de saudação analisador de portabilidade de .NET ou de uma análise manual, você deve testá-lo com HDInsight. Testando a solução Olá em um cluster HDInsight baseados em Linux pode revelar problemas sutis que precisam ser toobe corrigido. Recomendamos que você habilite o registro em log adicional no seu aplicativo ao testá-lo.

Para obter mais informações sobre como acessar os logs, consulte Olá documentos a seguir:

* [Acessar logs do aplicativo YARN no HDInsight baseado em Linux](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a>Próximas etapas

* [Usar C# com MapReduce no HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [Usar funções definidas pelo usuário do C# com Hive e Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [Desenvolver topologias C# para Storm no HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md)