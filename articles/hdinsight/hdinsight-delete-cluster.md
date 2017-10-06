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
# <a name="delete-an-hdinsight-cluster-using-your-browser-powershell-or-hello-azure-cli"></a><span data-ttu-id="2fc7b-103">Exclua um cluster HDInsight usando seu navegador, o PowerShell ou Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2fc7b-103">Delete an HDInsight cluster using your browser, PowerShell, or hello Azure CLI</span></span>

<span data-ttu-id="2fc7b-104">A cobrança de cluster HDInsight começa quando um cluster é criado e é interrompido quando o cluster Olá é excluído.</span><span class="sxs-lookup"><span data-stu-id="2fc7b-104">HDInsight cluster billing starts once a cluster is created and stops when hello cluster is deleted.</span></span> <span data-ttu-id="2fc7b-105">A cobrança ocorre por minuto, portanto, sempre exclua o cluster quando ele não estiver mais sendo usado.</span><span class="sxs-lookup"><span data-stu-id="2fc7b-105">Billing is pro-rated per minute, so you should always delete your cluster when it is no longer in use.</span></span> <span data-ttu-id="2fc7b-106">Neste documento, você aprenderá como toodelete um cluster usando Olá Olá 1.0 da CLI do Azure, Azure PowerShell e portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fc7b-106">In this document, you learn how toodelete a cluster using hello Azure portal, Azure PowerShell, and hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2fc7b-107">Excluir um cluster HDInsight não exclui as contas de armazenamento do Azure hello ou repositório Data Lake associados com cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2fc7b-107">Deleting an HDInsight cluster does not delete hello Azure Storage accounts or Data Lake Store associated with hello cluster.</span></span> <span data-ttu-id="2fc7b-108">Você pode reutilizar os dados armazenados nos serviços em Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="2fc7b-108">You can reuse data stored in those services in hello future.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="2fc7b-109">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2fc7b-109">Azure portal</span></span>

1. <span data-ttu-id="2fc7b-110">Faça logon no toohello [portal do Azure](https://portal.azure.com) e selecione seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2fc7b-110">Log in toohello [Azure portal](https://portal.azure.com) and select your HDInsight cluster.</span></span> <span data-ttu-id="2fc7b-111">Se o seu cluster HDInsight não está fixado toohello painel, você pode procurá-lo por nome usando o campo de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fc7b-111">If your HDInsight cluster is not pinned toohello dashboard, you can search for it by name using hello search field.</span></span>
   
    ![pesquisa do portal](./media/hdinsight-delete-cluster/navbar.png)

2. <span data-ttu-id="2fc7b-113">Quando abre folha Olá para cluster hello, selecione Olá **excluir** ícone.</span><span class="sxs-lookup"><span data-stu-id="2fc7b-113">Once hello blade opens for hello cluster, select hello **Delete** icon.</span></span> <span data-ttu-id="2fc7b-114">Quando solicitado, selecione **Sim** toodelete cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fc7b-114">When prompted, select **Yes** toodelete hello cluster.</span></span>
   
    ![excluir ícone](./media/hdinsight-delete-cluster/deletecluster.png)

## <a name="azure-powershell"></a><span data-ttu-id="2fc7b-116">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2fc7b-116">Azure PowerShell</span></span>

<span data-ttu-id="2fc7b-117">Em um prompt do PowerShell, use Olá cluster de saudação do toodelete de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="2fc7b-117">From a PowerShell prompt, use hello following command toodelete hello cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName CLUSTERNAME

<span data-ttu-id="2fc7b-118">Substituir **CLUSTERNAME** com nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2fc7b-118">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

## <a name="azure-cli-10"></a><span data-ttu-id="2fc7b-119">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="2fc7b-119">Azure CLI 1.0</span></span>

<span data-ttu-id="2fc7b-120">Em um prompt, use Olá cluster de saudação toodelete a seguir:</span><span class="sxs-lookup"><span data-stu-id="2fc7b-120">From a prompt, use hello following toodelete hello cluster:</span></span>

    azure hdinsight cluster delete CLUSTERNAME

<span data-ttu-id="2fc7b-121">Substituir **CLUSTERNAME** com nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2fc7b-121">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="2fc7b-122">CLI 2.0 do Azure não oferece suporte a clusters de HDInsight excluindo no momento (31 de julho de 2017).</span><span class="sxs-lookup"><span data-stu-id="2fc7b-122">Azure CLI 2.0 does not support deleting HDInsight clusters at this time (July 31, 2017).</span></span>