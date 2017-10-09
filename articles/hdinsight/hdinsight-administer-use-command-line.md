---
title: clusters de Hadoop aaaManage usando a CLI do Azure - HDInsight do Azure | Microsoft Docs
description: "Saiba como clusters de toouse Olá Interface de linha de comando do Azure toomanage Hadoop no HDInsight do Azure. Olá CLI do Azure funciona no Windows, Mac e Linux."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: 4f26c79f-8540-44bd-a470-84722a9e4eca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 03b0cff9331c1c581095b80cc6d1177d843ffa83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-using-hello-azure-cli"></a>Gerenciar clusters Hadoop em HDInsight usando Olá CLI do Azure
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Saiba como Olá toouse [Interface de linha de comando do Azure](../cli-install-nodejs.md) toomanage Hadoop clusters de HDInsight do Azure. Olá CLI do Azure é implementada no Node. js. Ela pode ser usada em qualquer plataforma que dê suporte ao Node.js, incluindo Windows, Mac e Linux.

Este artigo aborda apenas com hello CLI do Azure HDInsight. Para obter um guia geral sobre como toouse CLI do Azure, consulte [instalar e configurar a CLI do Azure][azure-command-line-tools].

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este artigo, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **CLI do Azure** -consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) para obter informações de instalação e configuração.
* **Conecte-se tooAzure**usando Olá seguinte comando:
  
        azure login
  
    Para obter mais informações sobre autenticação usando uma conta corporativa ou escolar, consulte [conectar tooan assinatura do Azure do hello CLI do Azure](../xplat-cli-connect.md).
* **Modo do comutador toohello Azure Resource Manager**usando Olá seguinte comando:
  
        azure config mode arm

tooget ajuda, use Olá **-h** alternar.  Por exemplo:

    azure hdinsight cluster create -h

## <a name="create-clusters-with-hello-cli"></a>Criar clusters com hello CLI
Consulte [criar clusters HDInsight usando Olá CLI do Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md).

## <a name="list-and-show-cluster-details"></a>Listar e mostrar detalhes do cluster
Use Olá toolist comandos a seguir e mostrar os detalhes do cluster:

    azure hdinsight cluster list
    azure hdinsight cluster show <Cluster Name>

![Modo de exibição de linha de comando de lista de clusters][image-cli-clusterlisting]

## <a name="delete-clusters"></a>Excluir clusters
Use Olá comando toodelete um cluster a seguir:

    azure hdinsight cluster delete <Cluster Name>

Você também pode excluir um cluster, excluindo o grupo de recursos de saudação que contém o cluster de saudação. Observe que isso excluirá todos os recursos de saudação no grupo de hello, incluindo a conta de armazenamento padrão de saudação.

    azure group delete <Resource Group Name>

## <a name="scale-clusters"></a>Dimensionar clusters
Olá toochange tamanho do cluster Hadoop:

    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>


## <a name="enabledisable-http-access-for-a-cluster"></a>Habilitar/desabilitar o acesso HTTP para um cluster
    azure hdinsight cluster enable-http-access [options] <Cluster Name> <userName> <password>
    azure hdinsight cluster disable-http-access [options] <Cluster Name>

## <a name="enabledisable-rdp-access-for-a-cluster"></a>Habilitar/desabilitar o acesso RDP para um cluster
      azure hdinsight cluster enable-rdp-access [options] <Cluster Name> <rdpUserName> <rdpPassword> <rdpExpiryDate>
      azure hdinsight cluster disable-rdp-access [options] <Cluster Name>


## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como tooperform HDInsight cluster tarefas administrativas. toolearn mais, consulte Olá artigos a seguir:

* [Administrar HDInsight usando Olá Portal do Azure][hdinsight-admin-portal]
* [Administrar clusters HDInsight usando o Azure PowerShell][hdinsight-admin-powershell]
* [Introdução ao Azure HDInsight][hdinsight-get-started]
* [Como toouse Olá CLI do Azure][azure-command-line-tools]

[azure-command-line-tools]: ../cli-install-nodejs.md
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[image-cli-account-download-import]: ./media/hdinsight-administer-use-command-line/HDI.CLIAccountDownloadImport.png
[image-cli-clustercreation]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreation.png
[image-cli-clustercreation-config]: ./media/hdinsight-administer-use-command-line/HDI.CLIClusterCreationConfig.png
[image-cli-clusterlisting]: ./media/hdinsight-administer-use-command-line/command-line-list-of-clusters.png "Listar e mostrar clusters"
