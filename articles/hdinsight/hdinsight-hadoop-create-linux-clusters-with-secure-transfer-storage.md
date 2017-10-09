---
title: "aaaCreate Hadoop de cluster com contas de armazenamento seguro de transferência no Azure HDInsight | Microsoft Docs"
description: "Saiba como clusters de HDInsight toocreate com transferência segura habilitado contas de armazenamento do Azure."
keywords: "guia de introdução do hadoop, hadoop linux, início rápido do hadoop, transferência segura, conta de armazenamento do azure"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a>Criar um cluster Hadoop com contas de armazenamento para transferência segura no Azure HDInsight

Olá [necessária de transferência segura](../storage/common/storage-require-secure-transfer.md) recurso aprimora a segurança de saudação da sua conta de armazenamento do Azure através da aplicação de todas as contas de tooyour solicitações por meio de uma conexão segura. Esse esquema de recurso e hello wasbs só são suportados pela versão de cluster do HDInsight 3.6 ou mais recente. 

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deverá ter o seguinte:

* **Assinatura do Azure**: toocreate uma conta de avaliação de um mês livre, procurar muito[azure.microsoft.com/free](https://azure.microsoft.com/free).
* **Uma conta de Armazenamento do Azure com transferência segura habilitada**. Para obter instruções hello, consulte [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) e [requerem a transferência segura](../storage/common/storage-require-secure-transfer.md).
* **Um contêiner de Blob na conta de armazenamento Olá**. 
## <a name="create-cluster"></a>Criar cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


Nesta seção, você criará um cluster Hadoop no HDInsight usando um [modelo do Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Olá modelo está localizado em [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/). Não é necessário ter experiência com o modelo do Resource Manager para seguir este tutorial. Para outros métodos de criação de cluster e Noções básicas sobre propriedades de saudação usadas neste tutorial, consulte [HDInsight criar clusters](hdinsight-hadoop-provision-linux-clusters.md).

1. Clique em Olá toosign de imagem no tooAzure e modelo do Gerenciador de recursos de saudação abrir no portal do Azure de saudação a seguir. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Execute o cluster de Olá Olá instruções toocreate com hello especificações a seguir: 

    - Especifique o HDInsight versão 3.6.  versão do padrão de saudação é 3.5. É necessário ter a versão 3.6 ou mais recente.
    - Especifique uma conta de armazenamento com transferência segura habilitada.
    - Use o nome curto para a conta de armazenamento hello.
    - Conta de armazenamento hello e o contêiner de blob Olá devem ser criados com antecedência. 

    Para obter instruções hello, consulte [criar cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). 

Se você usar o script ação tooprovide seus próprios arquivos de configuração, você deve usar wasbs no hello configurações a seguir:

- fs.defaultFS (site principal)
- spark.eventLog.dir 
- spark.history.fs.logDirectory

## <a name="add-additional-storage-accounts"></a>Adicionar outras contas de armazenamento

Há várias contas de armazenamento opções tooadd adicionais transferência segura habilitada:

- Modifica modelo de Gerenciador de recursos do Azure Olá na última seção do hello.
- Criar um cluster usando Olá [portal do Azure](https://portal.azure.com) e especifique a conta de armazenamento vinculada.
- Use script ação tooadd adicional transferência segura habilitada armazenamento contas tooan existente cluster do HDInsight.  Para obter mais informações, consulte [adicionar tooHDInsight de contas de armazenamento adicional](hdinsight-hadoop-add-storage.md).

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você aprendeu como toocreate um cluster HDInsight e habilitar seguro transferir toohello contas de armazenamento.

toolearn mais sobre a análise de dados com o HDInsight, consulte Olá artigos a seguir:

* toolearn mais sobre como usar o Hive com HDInsight, incluindo como tooperform Hive as consultas do Visual Studio, consulte [uso de Hive do HDInsight][hdinsight-use-hive].
* toolearn sobre Pig, uma linguagem usada tootransform dados, consulte [usar o Pig com HDInsight][hdinsight-use-pig].
* toolearn sobre MapReduce, programas de toowrite uma maneira que processam dados no Hadoop, consulte [Use MapReduce com HDInsight][hdinsight-use-mapreduce].
* toolearn sobre como usar ferramentas do HDInsight Olá para dados do Visual Studio tooanalyze no HDInsight, consulte [começar a usar ferramentas Hadoop do Visual Studio para HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).

mais informações sobre como HDInsight armazena dados de toolearn ou como dados tooget em HDInsight, consulte Olá artigos a seguir:

* Para saber mais sobre como o HDInsight usa o Armazenamento do Azure, veja [Usar Armazenamento do Azure com o HDInsight](hdinsight-hadoop-use-blob-storage.md).
* Para obter informações sobre como tooupload tooHDInsight de dados, consulte [carregar dados tooHDInsight][hdinsight-upload-data].

toolearn mais sobre como criar ou gerenciar um cluster HDInsight, consulte Olá artigos a seguir:

* toolearn sobre como gerenciar seu cluster HDInsight baseados em Linux, consulte [HDInsight gerenciar clusters usando o Ambari](hdinsight-hadoop-manage-ambari.md).
* toolearn mais sobre opções de saudação, você pode selecionar ao criar um cluster HDInsight, consulte [criando HDInsight no Linux usando opções personalizadas](hdinsight-hadoop-provision-linux-clusters.md).
* Se você estiver familiarizado com Linux e Hadoop, mas desejar tooknow obter as informações específicas sobre o Hadoop Olá HDInsight, consulte [trabalhando com HDInsight no Linux](hdinsight-hadoop-linux-information.md). Este artigo oferece informações como:
  
  * URLs para serviços hospedados no cluster hello, como Ambari e WebHCat
  * local de saudação de arquivos Hadoop e exemplos no sistema de arquivos local Olá
  * uso de saudação do Azure Storage (WASB) em vez de HDFS como armazenamento de dados padrão de saudação

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


