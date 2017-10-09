---
title: aaaUse um PC Windows com Hadoop no HDInsight - Azure | Microsoft Docs
description: "Trabalhe em um PC com Windows no Hadoop no HDInsight. Gerencie e consulte clusters com as ferramentas do PowerShell, Visual Studio e Linux. Desenvolva soluções de Big Data com .NET."
services: hdinsight
keywords: hadoop no windows,hadoop para windows
author: cjgronlund
manager: jhubbard
ms.author: cgronlun
ms.date: 05/17/2017
ms.topic: article
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 7c93f16e93349c0b8fb1abd55320c2c172b93aa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="work-in-hello-hadoop-ecosystem-on-hdinsight-from-a-windows-pc"></a>Trabalhar no hello ecossistema de Hadoop no HDInsight a partir de um PC Windows

Saiba mais sobre opções de gerenciamento em Olá PC com Windows e desenvolvimento para trabalhar no ecossistema do hello Hadoop no HDInsight. 

O HDInsight tem base em componentes do Apache Hadoop e do Hadoop, tecnologias de código-fonte aberto desenvolvidas no Linux. HDInsight versão 3.4 ou superior usa Olá distribuição Ubuntu Linux como Olá subjacente do sistema operacional para cluster hello. No entanto, você pode trabalhar com o HDInsight de um cliente Windows ou ambiente de desenvolvimento do Windows.

## <a name="use-powershell-for-deployment-and-management-tasks"></a>Usar o PowerShell para as tarefas de implantação e gerenciamento
PowerShell do Azure é um ambiente de script que você pode usar toocontrol e automatizar tarefas de implantação e gerenciamento de HDInsight do Windows.

Exemplos de tarefas que você pode fazer com o PowerShell:

* [Criar clusters usando o PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [Executar consultas Hive usando o PowerShell](hdinsight-hadoop-use-hive-powershell.md)
* [Gerenciar clusters com o PowerShell](hdinsight-administer-use-powershell.md)

Siga as etapas muito[instalar e configurar o Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) versão mais recente do tooget hello. Se você tiver scripts que precisam toobe modificado toouse Olá novos cmdlets do Azure Resource Manager, consulte [migrar tooAzure ferramentas de desenvolvimento com base no Gerenciador de recursos para clusters de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="utilities-you-can-run-in-a-browser"></a>Utilitários que você pode executar em um navegador
Olá, utilitários a seguir têm uma interface do usuário que é executado em um navegador da web:
* **[Shell de nuvem do Azure (visualização)](https://docs.microsoft.com/azure/cloud-shell/quickstart)**  é um shell interativo, de linha de comando que é executado no navegador e no hello portal do Azure.
* **[Interface de usuário do Ambari Web](hdinsight-hadoop-manage-ambari.md)**  é um gerenciamento e monitoramento do utilitário disponível no hello portal do Azure que pode ser usado toomanage diferentes tipos de trabalhos, como:
    * [Usar Ambari com hello API REST](hdinsight-hadoop-manage-ambari-rest-api.md)
    * [Modo de Exibição do Hive no Ambari](hdinsight-hadoop-use-hive-ambari-view.md)
    * [Modo de Exibição do Tez no Ambari](hdinsight-debug-ambari-tez-view.md)

## <a name="data-lake-hadoop-tools-for-visual-studio"></a>Ferramentas do Data Lake (Hadoop) para Visual Studio
Usar Data Lake Tools para Visual Studio toodeploy e gerenciar topologias Storm. Ferramentas do data Lake também instala Olá SCP.NET SDK, que permite topologias de C# Storm toodevelop com o Visual Studio.

Antes de ir toohello seguindo exemplos [instalar e testar Data Lake Tools para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md). 

Exemplos de tarefas que você pode realizar com o Visual Studio e o Data Lake Tools para Visual Studio:
* [Implantar e gerenciar topologias Storm no Visual Studio](hdinsight-storm-deploy-monitor-topology-linux.md)
* [Desenvolver topologias em C# para Storm usando o Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md). bits de saudação incluem modelos de exemplo para topologias Storm toodatabases, como o banco de dados do Azure Cosmos e banco de dados SQL pode se conectar.

## <a name="visual-studio-and-hello-net-sdk"></a>Visual Studio e hello SDK .NET 

Você pode usar o Visual Studio com clusters de toomanage .NET SDK hello e desenvolver aplicativos de dados grandes. Você pode usar outros IDEs para Olá tarefas a seguir, mas os exemplos são mostrados no Visual Studio.

Exemplos de tarefas que você pode fazer com hello SDK do .NET no Visual Studio:
* [Criar clusters e trabalhar no HDInsight de um aplicativo do .NET Framework](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* [Executar consultas de Hive usando Olá SDK .NET](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [Usar funções definidas pelo usuário do C# com streaming de Hive e Pig no Hadoop](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

> Dica Se você estiver executando soluções .NET com clusters HDInsight baseados no Windows, é um bom momento tooplan uma migração de clusters com base em tooLinux. Para obter mais informações, consulte [solução .NET migrar para HDInsight baseados em Windows com base em tooLinux HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).

## <a name="intellij-idea-and-eclipse-ide-for-spark-clusters"></a>IDEA do IntelliJ e IDE do Eclipse para clusters Spark
Ambos [Intellij IDEIA](https://www.jetbrains.com/idea/download) e hello [IDE do Eclipse](https://www.eclipse.org/downloads/) pode ser usado para:
* Desenvolver e enviar um aplicativo Scala Spark em um cluster HDInsight Spark.
* Acessar os recursos em cluster Spark.
* Desenvolver e executar um aplicativo Scala Spark localmente.

Esses artigos mostram como: 
* IntelliJ IDEIA: [aplicativos criar Spark usando hello Azure Toolkit for Intellij plug-in e Olá Scala SDK.](hdinsight-apache-spark-intellij-tool-plugin.md)
* Eclipse IDE ou Scala IDE para Eclipse: [aplicativos criar Spark e hello Kit de ferramentas do Azure para Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md) 


## <a name="notebooks-on-spark-for-data-scientists"></a>Notebooks no Spark para os cientistas de dados 
Os clusters do Apache Spark no HDInsight incluem notebooks e kernels Zeppelin que podem ser usados com notebooks do Jupyter. 

* [Saiba como kernels toouse no Spark clusters com aplicativos do Jupyter notebooks tootest Spark](hdinsight-apache-spark-zeppelin-notebook.md)
* [Saiba como toouse Zeppelin blocos de anotações Spark clusters trabalhos do Spark toorun](hdinsight-apache-spark-jupyter-notebook-kernels.md) 


## <a name="run-linux-based-tools-and-technologies-on-windows"></a>Executar ferramentas e tecnologias baseadas em Linux no Windows

Se você encontrar uma situação em que você deve usar uma ferramenta ou tecnologia que está disponível apenas no Linux, considere Olá as opções a seguir:

* **Bash (beta) no Windows 10** fornece um subsistema Linux no Windows. Bash permite toodirectly executar utilitários de Linux sem ter que toomaintain uma instalação Linux dedicada. [Instalar e executar o beta do hello Bash no Windows 10](https://msdn.microsoft.com/commandline/wsl/install_guide)
* **Docker para Windows** fornece acesso a ferramentas toomany Linux e podem ser executados diretamente do Windows. Por exemplo, você pode usar o cliente do Docker toorun Olá Beeline para Hive diretamente do Windows. Você pode usar também o Docker toorun um bloco de anotações do Jupyter local e conectar-se remotamente tooSpark no HDInsight. [Introdução ao Docker para Windows](https://docs.docker.com/docker-for-windows/)
* **[MobaXTerm](http://mobaxterm.mobatek.net/)**  permite que o sistema de arquivos do toographically procurar Olá cluster sobre uma conexão SSH.

## <a name="next-steps"></a>Próximas etapas
Se você for novo tooworking em clusters baseados em Linux, consulte Olá siga artigos:
* [Configurar o Hadoop, Kafka, Spark ou outros clusters](hdinsight-hadoop-provision-linux-clusters.md)
* [Dicas para clusters HDInsight no Linux](hdinsight-hadoop-linux-information.md)