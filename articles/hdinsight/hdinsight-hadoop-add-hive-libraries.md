---
title: "bibliotecas de Hive aaaAdd durante HDInsight cluster criação - Azure | Microsoft Docs"
description: "Saiba como bibliotecas de Hive tooadd (arquivos jar), tooan HDInsight cluster durante a criação do cluster."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a>Adicionar bibliotecas Hive personalizadas ao criar seu cluster HDInsight

Se você tiver bibliotecas que você usa com frequência com Hive no HDInsight, este documento contém informações sobre como usar bibliotecas de Olá de toopre carga uma ação de Script durante a criação do cluster. Bibliotecas adicionadas usando etapas Olá neste documento estão disponíveis globalmente no Hive - não há nenhuma necessidade toouse [Adicionar JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload-los.

## <a name="how-it-works"></a>Como ele funciona

Ao criar um cluster, você pode opcionalmente especificar uma ação de Script que executa um script em nós de cluster Olá enquanto estão sendo criados. script Hello neste documento aceita um único parâmetro, que é um local de WASB que contém a saudação bibliotecas (armazenadas como arquivos jar) toobe pré-carregado.

Durante a criação do cluster, o script hello enumera arquivos hello, copia toohello `/usr/lib/customhivelibs/` diretório em nós de cabeçalho e de trabalho, em seguida, adiciona toohello `hive.aux.jars.path` propriedade Olá `core-site.xml` arquivo. Em clusters baseados em Linux, ela também atualiza Olá `hive-env.sh` arquivo com hello local dos arquivos de saudação.

> [!NOTE]
> Usar ações de script hello neste artigo disponibiliza bibliotecas Olá no hello os seguintes cenários:
>
> * **HDInsight baseados em Linux** - quando usando Olá um cliente de Hive, **WebHCat**, e **HiveServer2**.
> * **HDInsight baseados em Windows** - ao usar o cliente de Hive hello e **WebHCat**.

## <a name="hello-script"></a>script Hello

**Local do script**

Para os **clusters baseados no Linux**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)

Para os **clusters baseados no Windows**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

**Requisitos**

* scripts de saudação devem ser aplicada tooboth Olá **nós de cabeçalho** e **nós de trabalho**.

* Olá jars desejar tooinstall devem ser armazenados no armazenamento de BLOBs do Azure em um **único contêiner**.

* conta de armazenamento Olá que contém a biblioteca de saudação arquivos jar **deve** ser vinculada toohello HDInsight cluster durante a criação. Ele deve ser conta de armazenamento saudação padrão ou uma conta adicionada por meio de __configuração opcional__.

* contêiner de toohello Olá WASB caminho deve ser especificado como uma ação de Script de toohello do parâmetro. Por exemplo, se hello jars são armazenados em um contêiner chamado **bibliotecas** em uma conta de armazenamento denominada **mystorage**, parâmetro hello seria  **wasb://libs@mystorage.blob.core.windows.net/** .

  > [!NOTE]
  > Este documento assume que você já crie uma conta de armazenamento, contêiner de blob e carregado Olá arquivos tooit.
  >
  > Se você não tiver criado uma conta de armazenamento, você pode fazer isso por meio de saudação [portal do Azure](https://portal.azure.com). Você pode usar um utilitário como [Azure Storage Explorer](http://storageexplorer.com/) toocreate um contêiner na conta de saudação e carregar arquivos tooit.

## <a name="create-a-cluster-using-hello-script"></a>Criar um cluster usando o script hello

> [!NOTE]
> Olá etapas a seguir cria um cluster HDInsight baseados em Linux. toocreate um cluster baseado no Windows, selecione **Windows** como Olá cluster sistema operacional durante a criação de cluster hello e usar script de saudação do Windows (PowerShell) em vez de scripts de bash Olá.
>
> Você também pode usar o Azure PowerShell ou Olá HDInsight .NET SDK toocreate um cluster usando esse script. Para obter mais informações sobre como usar esses métodos, consulte [Personalizar clusters HDInsight com Ações de Script](hdinsight-hadoop-customize-cluster-linux.md).

1. Iniciar o provisionamento de um cluster usando as etapas de saudação em [HDInsight provisionar clusters no Linux](hdinsight-hadoop-provision-linux-clusters.md), mas não conclua o provisionamento.

2. Em Olá **configuração opcional** folha, selecione **ações de Script**e fornecer Olá informações a seguir:

   * **NOME**: insira um nome amigável para a ação de script hello.

   * **URI do SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh

   * **CABEÇALHO**: marque esta opção.

   * **TRABALHO**: marque esta opção.

   * **ZOOKEEPER**: deixe essa opção em branco.

   * **PARÂMETROS**: insira Olá WASB endereço toohello contêiner e conta de armazenamento que contém os jars hello. Por exemplo, **wasb://libs@mystorage.blob.core.windows.net/**.

3. Na parte inferior de saudação do hello **ações de Script**, use Olá **selecione** configuração de saudação do botão toosave.

4. Em Olá **configuração opcional** folha, selecione **contas de armazenamento vinculadas** e selecione hello **adicionar uma chave de armazenamento** link. Selecionar conta de armazenamento Olá que contém os jars hello e use Olá **selecione** configurações de toosave de botões e hello retorno **configuração opcional** folha.

5. Saudação de uso **selecione** botão na parte inferior de saudação do hello **configuração opcional** informações de configuração opcional de saudação de toosave de folha.

6. Continuar o provisionamento de cluster Olá conforme descrito em [HDInsight provisionar clusters no Linux](hdinsight-hadoop-provision-linux-clusters.md).

Depois de termina a criação do cluster, você está jars do hello capaz de toouse adicionadas por este script de Hive sem ter que toouse Olá `ADD JAR` instrução.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre como trabalhar com o Hive, confira [Usar o Hive com o HDInsight](hdinsight-use-hive.md)
