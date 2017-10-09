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
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="6afda-104">Instalar ou atualizar Mono no HDInsight</span><span class="sxs-lookup"><span data-stu-id="6afda-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="6afda-105">Saiba como tooinstall uma versão específica de [Mono](https://www.mono-project.com) no HDInsight 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="6afda-105">Learn how tooinstall a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="6afda-106">Mono está instalado no HDInsight 3.4 e superior e é usado toorun aplicativos .NET.</span><span class="sxs-lookup"><span data-stu-id="6afda-106">Mono is installed on HDInsight 3.4 and higher, and is used toorun .NET applications.</span></span> <span data-ttu-id="6afda-107">Para obter informações sobre a versão de saudação do Mono incluída com cada versão do HDInsight, consulte [o controle de versão do HDInsight componente](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="6afda-107">For information on hello version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="6afda-108">tooinstall uma versão diferente no cluster, use ação de script hello neste documento.</span><span class="sxs-lookup"><span data-stu-id="6afda-108">tooinstall a different version on your cluster, use hello script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="6afda-109">Como ele funciona</span><span class="sxs-lookup"><span data-stu-id="6afda-109">How it works</span></span>

<span data-ttu-id="6afda-110">Esse script aceita Olá parâmetro a seguir:</span><span class="sxs-lookup"><span data-stu-id="6afda-110">This script accepts hello following parameter:</span></span>

* <span data-ttu-id="6afda-111">__Número de versão mono__: versão de saudação do tooinstall Mono.</span><span class="sxs-lookup"><span data-stu-id="6afda-111">__Mono version number__: hello version of Mono tooinstall.</span></span> <span data-ttu-id="6afda-112">versão de Hello deve estar disponível na [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span><span class="sxs-lookup"><span data-stu-id="6afda-112">hello version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="6afda-113">Instala o script Hello Olá Mono pacotes a seguir:</span><span class="sxs-lookup"><span data-stu-id="6afda-113">hello script installs hello following Mono packages:</span></span>

* <span data-ttu-id="6afda-114">__mono-complete__</span><span class="sxs-lookup"><span data-stu-id="6afda-114">__mono-complete__</span></span>

* <span data-ttu-id="6afda-115">__ca-certificates-mono__</span><span class="sxs-lookup"><span data-stu-id="6afda-115">__ca-certificates-mono__</span></span>

## <a name="hello-script"></a><span data-ttu-id="6afda-116">script Hello</span><span class="sxs-lookup"><span data-stu-id="6afda-116">hello script</span></span>

<span data-ttu-id="6afda-117">__Local do script__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="6afda-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="6afda-118">__Requisitos__:</span><span class="sxs-lookup"><span data-stu-id="6afda-118">__Requirements__:</span></span>

* <span data-ttu-id="6afda-119">script Hello deve ser aplicada em Olá __nós de cabeçalho__ e __nós de trabalho__.</span><span class="sxs-lookup"><span data-stu-id="6afda-119">hello script must be applied on hello __head nodes__ and __worker nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="6afda-120">script de saudação toouse</span><span class="sxs-lookup"><span data-stu-id="6afda-120">toouse hello script</span></span>

<span data-ttu-id="6afda-121">Para obter informações sobre como toouse esse script com HDInsight, consulte Olá [usando a ação de script de clusters HDInsight baseados em Linux personalizar](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) documento.</span><span class="sxs-lookup"><span data-stu-id="6afda-121">For information on how toouse this script with HDInsight, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="6afda-122">Você pode usar o script hello por meio de saudação portal do Azure, Azure PowerShell, ou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="6afda-122">You can use hello script through hello Azure portal, Azure PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="6afda-123">Enquanto a seguir hello documento de ação de script, use Olá URI a seguir:</span><span class="sxs-lookup"><span data-stu-id="6afda-123">While following hello script action document, use hello following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> <span data-ttu-id="6afda-124">Ao configurar o HDInsight com este script, marcar o script hello como __Persisted__.</span><span class="sxs-lookup"><span data-stu-id="6afda-124">When configuring HDInsight with this script, mark hello script as __Persisted__.</span></span> <span data-ttu-id="6afda-125">Essa configuração permite HDInsight tooapply nós de tooworker de script hello adicionados por meio de operações de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="6afda-125">This setting allows HDInsight tooapply hello script tooworker nodes added through scaling operations.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6afda-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6afda-126">Next steps</span></span>

<span data-ttu-id="6afda-127">Você aprendeu como tooupgrade ou instale uma versão específica do Mono no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="6afda-127">You have learned how tooupgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="6afda-128">Para obter mais informações sobre o uso de aplicativos .NET com Mono no HDInsight, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="6afda-128">For more information on using .NET applications with Mono on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="6afda-129">Usar o .NET para transmitir MapReduce no HDInsight</span><span class="sxs-lookup"><span data-stu-id="6afda-129">Use .NET for streaming MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [<span data-ttu-id="6afda-130">Usar o .NET com o Hive e o Pig no HDInsight</span><span class="sxs-lookup"><span data-stu-id="6afda-130">Use .NET with Hive and Pig on HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [<span data-ttu-id="6afda-131">Desenvolver soluções do C# com o Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="6afda-131">Develop C# solutions with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="6afda-132">Migrar soluções .NET com base em tooLinux HDInsight</span><span class="sxs-lookup"><span data-stu-id="6afda-132">Migrate .NET solutions tooLinux-based HDInsight</span></span>](hdinsight-hadoop-migrate-dotnet-to-linux.md)

<span data-ttu-id="6afda-133">Para saber mais sobre como usar as ações de script, confira [Personalizar clusters HDInsight com base em Linux usando a ação de script](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="6afda-133">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>