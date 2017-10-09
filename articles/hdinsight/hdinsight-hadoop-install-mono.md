---
title: aaaInstall ou atualizar Mono no HDInsight - Azure | Microsoft Docs
description: "Saiba como toouse uma versão específica do Mono com o cluster HDInsight. Mono é usado toorun aplicativos .NET clusters HDInsight baseados em Linux."
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: hdinsightactive
ms.openlocfilehash: 1e8a8aaeff231c93a9e232379448517b326da965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a>Instalar ou atualizar Mono no HDInsight

Saiba como tooinstall uma versão específica de [Mono](https://www.mono-project.com) no HDInsight 3.4 ou superior.

Mono está instalado no HDInsight 3.4 e superior e é usado toorun aplicativos .NET. Para obter informações sobre a versão de saudação do Mono incluída com cada versão do HDInsight, consulte [o controle de versão do HDInsight componente](hdinsight-component-versioning.md). tooinstall uma versão diferente no cluster, use ação de script hello neste documento. 

## <a name="how-it-works"></a>Como ele funciona

Esse script aceita Olá parâmetro a seguir:

* __Número de versão mono__: versão de saudação do tooinstall Mono. versão de Hello deve estar disponível na [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).

Instala o script Hello Olá Mono pacotes a seguir:

* __mono-complete__

* __ca-certificates-mono__

## <a name="hello-script"></a>script Hello

__Local do script__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)

__Requisitos__:

* script Hello deve ser aplicada em Olá __nós de cabeçalho__ e __nós de trabalho__.

## <a name="toouse-hello-script"></a>script de saudação toouse

Para obter informações sobre como toouse esse script com HDInsight, consulte Olá [usando a ação de script de clusters HDInsight baseados em Linux personalizar](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) documento. Você pode usar o script hello por meio de saudação portal do Azure, Azure PowerShell, ou Olá CLI do Azure.

Enquanto a seguir hello documento de ação de script, use Olá URI a seguir:

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> Ao configurar o HDInsight com este script, marcar o script hello como __Persisted__. Essa configuração permite HDInsight tooapply nós de tooworker de script hello adicionados por meio de operações de dimensionamento.


## <a name="next-steps"></a>Próximas etapas

Você aprendeu como tooupgrade ou instale uma versão específica do Mono no HDInsight. Para obter mais informações sobre o uso de aplicativos .NET com Mono no HDInsight, consulte Olá documentos a seguir:

* [Usar o .NET para transmitir MapReduce no HDInsight](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [Usar o .NET com o Hive e o Pig no HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [Desenvolver soluções do C# com o Storm no HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Migrar soluções .NET com base em tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)

Para saber mais sobre como usar as ações de script, confira [Personalizar clusters HDInsight com base em Linux usando a ação de script](hdinsight-hadoop-customize-cluster-linux.md)