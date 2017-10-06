---
title: aaaHow toodelete um cluster HDInsight - Azure | Microsoft Docs
description: "Informações sobre Olá várias maneiras que você pode excluir um cluster HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 55f7838b-9786-47ff-96db-1b64437bd0bb
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 5b9d9a09eecfdcfaed7a1f5ebab440e13bd358b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a>Exclua um cluster HDInsight usando seu navegador, o PowerShell ou Olá CLI do Azure

A cobrança de cluster HDInsight começa quando um cluster é criado e é interrompido quando o cluster Olá é excluído. A cobrança ocorre por minuto, portanto, sempre exclua o cluster quando ele não estiver mais sendo usado. Neste documento, você aprenderá como toodelete um cluster usando Olá Olá 1.0 da CLI do Azure, Azure PowerShell e portal do Azure.

> [!IMPORTANT]
> Excluir um cluster HDInsight não exclui as contas de armazenamento do Azure hello ou repositório Data Lake associados com cluster hello. Você pode reutilizar os dados armazenados nos serviços em Olá futuras.

## <a name="azure-portal"></a>Portal do Azure

1. Faça logon no toohello [portal do Azure](https://portal.azure.com) e selecione seu cluster HDInsight. Se o seu cluster HDInsight não está fixado toohello painel, você pode procurá-lo por nome usando o campo de pesquisa de saudação.
   
    ![pesquisa do portal](./media/hdinsight-delete-cluster/navbar.png)

2. Quando abre folha Olá para cluster hello, selecione Olá **excluir** ícone. Quando solicitado, selecione **Sim** toodelete cluster de saudação.
   
    ![excluir ícone](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a>Azure PowerShell

Em um prompt do PowerShell, use Olá cluster de saudação do toodelete de comando a seguir:

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

Substituir **CLUSTERNAME** com nome de saudação do cluster HDInsight.

## <a name="azure-cli-10"></a>CLI 1.0 do Azure

Em um prompt, use Olá cluster de saudação toodelete a seguir:

    azure hdinsight cluster delete CLUSTERNAME

Substituir **CLUSTERNAME** com nome de saudação do cluster HDInsight.

> [!NOTE]
> CLI 2.0 do Azure não oferece suporte a clusters de HDInsight excluindo no momento (31 de julho de 2017).