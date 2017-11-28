---
title: "desenvolvimento de ação aaaScript com HDInsight baseados em Linux - Azure | Microsoft Docs"
description: "Saiba como toouse Bash scripts toocustomize clusters de HDInsight baseados em Linux. recurso de ação de script de saudação do HDInsight permite que você toorun scripts durante ou após a criação do cluster. Scripts podem ser usado toochange definições de configuração de cluster ou instalar software adicional."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="7911f-105">Desenvolvimento de ação de script com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="7911f-105">Script action development with HDInsight</span></span>

<span data-ttu-id="7911f-106">Saiba como toocustomize seu cluster HDInsight usando Bash scripts.</span><span class="sxs-lookup"><span data-stu-id="7911f-106">Learn how toocustomize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="7911f-107">Ações de script são uma maneira toocustomize HDInsight durante ou após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="7911f-107">Script actions are a way toocustomize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7911f-108">etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux.</span><span class="sxs-lookup"><span data-stu-id="7911f-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="7911f-109">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="7911f-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7911f-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7911f-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="7911f-111">O que são ações de script</span><span class="sxs-lookup"><span data-stu-id="7911f-111">What are script actions</span></span>

<span data-ttu-id="7911f-112">Ações de script são scripts de Bash Azure é executado em alterações de configuração toomake de nós de cluster hello ou instalam o software.</span><span class="sxs-lookup"><span data-stu-id="7911f-112">Script actions are Bash scripts that Azure runs on hello cluster nodes toomake configuration changes or install software.</span></span> <span data-ttu-id="7911f-113">Uma ação de script é executada como raiz e fornece nós de cluster toohello direitos de acesso completo.</span><span class="sxs-lookup"><span data-stu-id="7911f-113">A script action is executed as root, and provides full access rights toohello cluster nodes.</span></span>

<span data-ttu-id="7911f-114">Ações de script podem ser aplicadas por meio de saudação métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7911f-114">Script actions can be applied through hello following methods:</span></span>

| <span data-ttu-id="7911f-115">Use esse método tooapply um script...</span><span class="sxs-lookup"><span data-stu-id="7911f-115">Use this method tooapply a script...</span></span> | <span data-ttu-id="7911f-116">Durante a criação do cluster...</span><span class="sxs-lookup"><span data-stu-id="7911f-116">During cluster creation...</span></span> | <span data-ttu-id="7911f-117">Em um cluster em execução...</span><span class="sxs-lookup"><span data-stu-id="7911f-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="7911f-118">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7911f-118">Azure portal</span></span> |<span data-ttu-id="7911f-119">✓ </span><span class="sxs-lookup"><span data-stu-id="7911f-119">✓</span></span> |<span data-ttu-id="7911f-120">✓</span><span class="sxs-lookup"><span data-stu-id="7911f-120">✓</span></span> |
| <span data-ttu-id="7911f-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7911f-121">Azure PowerShell</span></span> |<span data-ttu-id="7911f-122">✓</span><span class="sxs-lookup"><span data-stu-id="7911f-122">✓</span></span> |<span data-ttu-id="7911f-123">✓</span><span class="sxs-lookup"><span data-stu-id="7911f-123">✓</span></span> |
| <span data-ttu-id="7911f-124">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7911f-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="7911f-125">✓</span><span class="sxs-lookup"><span data-stu-id="7911f-125">✓</span></span> |
| <span data-ttu-id="7911f-126">SDK do .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="7911f-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="7911f-127">✓</span><span class="sxs-lookup"><span data-stu-id="7911f-127">✓</span></span> |<span data-ttu-id="7911f-128">✓</span><span class="sxs-lookup"><span data-stu-id="7911f-128">✓</span></span> |
| <span data-ttu-id="7911f-129">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7911f-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="7911f-130">✓ </span><span class="sxs-lookup"><span data-stu-id="7911f-130">✓</span></span> |&nbsp; |

<span data-ttu-id="7911f-131">Para obter mais informações sobre como usar essas ações de script tooapply métodos, consulte [clusters de HDInsight personalizar usando ações de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7911f-131">For more information on using these methods tooapply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="7911f-132"><a name="bestPracticeScripting"></a>Práticas recomendadas para o desenvolvimento de scripts</span><span class="sxs-lookup"><span data-stu-id="7911f-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="7911f-133">Quando você desenvolve um script personalizado para um cluster HDInsight, há vários tookeep práticas recomendadas em mente:</span><span class="sxs-lookup"><span data-stu-id="7911f-133">When you develop a custom script for an HDInsight cluster, there are several best practices tookeep in mind:</span></span>

* [<span data-ttu-id="7911f-134">Versão do Hadoop de saudação de destino</span><span class="sxs-lookup"><span data-stu-id="7911f-134">Target hello Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="7911f-135">Olá, versão do sistema operacional de destino</span><span class="sxs-lookup"><span data-stu-id="7911f-135">Target hello OS Version</span></span>](#bps10)
* [<span data-ttu-id="7911f-136">Fornecer estável links tooscript recursos</span><span class="sxs-lookup"><span data-stu-id="7911f-136">Provide stable links tooscript resources</span></span>](#bPS2)
* [<span data-ttu-id="7911f-137">Usar os recursos pré-compilados</span><span class="sxs-lookup"><span data-stu-id="7911f-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="7911f-138">Certifique-se de que o script de personalização de cluster Olá é idempotente</span><span class="sxs-lookup"><span data-stu-id="7911f-138">Ensure that hello cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="7911f-139">Garantir a alta disponibilidade da arquitetura de cluster Olá</span><span class="sxs-lookup"><span data-stu-id="7911f-139">Ensure high availability of hello cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="7911f-140">Configurar o armazenamento de BLOBs do Azure em toouse Olá componentes personalizados</span><span class="sxs-lookup"><span data-stu-id="7911f-140">Configure hello custom components toouse Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="7911f-141">Gravar informações tooSTDOUT e STDERR</span><span class="sxs-lookup"><span data-stu-id="7911f-141">Write information tooSTDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="7911f-142">Salvar arquivos como ASCII com terminações de linha LF</span><span class="sxs-lookup"><span data-stu-id="7911f-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="7911f-143">Usar toorecover de lógica de repetição de erros transitórios</span><span class="sxs-lookup"><span data-stu-id="7911f-143">Use retry logic toorecover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="7911f-144">Ações de script devem ser concluído dentro de 60 minutos ou Olá processo falhar.</span><span class="sxs-lookup"><span data-stu-id="7911f-144">Script actions must complete within 60 minutes or hello process fails.</span></span> <span data-ttu-id="7911f-145">Durante o provisionamento de nó, o script hello é executado simultaneamente com outros processos de instalação e configuração.</span><span class="sxs-lookup"><span data-stu-id="7911f-145">During node provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="7911f-146">Competição por recursos, como largura de banda rede ou tempo de CPU pode provocar Olá script tootake mais toofinish do que no ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="7911f-146">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>

### <span data-ttu-id="7911f-147"><a name="bPS1"></a>Versão do Hadoop de saudação de destino</span><span class="sxs-lookup"><span data-stu-id="7911f-147"><a name="bPS1"></a>Target hello Hadoop version</span></span>

<span data-ttu-id="7911f-148">Diferentes versões do HDInsight têm diferentes versões de componentes e serviços do Hadoop instaladas.</span><span class="sxs-lookup"><span data-stu-id="7911f-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="7911f-149">Se seu script espera uma versão específica de um serviço ou componente, você deve usar somente script hello com versão de saudação do HDInsight que inclui componentes de saudação necessária.</span><span class="sxs-lookup"><span data-stu-id="7911f-149">If your script expects a specific version of a service or component, you should only use hello script with hello version of HDInsight that includes hello required components.</span></span> <span data-ttu-id="7911f-150">Você pode encontrar informações sobre versões de componentes incluídos no HDInsight usando Olá [o controle de versão do HDInsight componente](hdinsight-component-versioning.md) documento.</span><span class="sxs-lookup"><span data-stu-id="7911f-150">You can find information on component versions included with HDInsight using hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="7911f-151"><a name="bps10"></a>Versão de hello sistema operacional de destino</span><span class="sxs-lookup"><span data-stu-id="7911f-151"><a name="bps10"></a> Target hello OS version</span></span>

<span data-ttu-id="7911f-152">HDInsight baseados em Linux baseia-se em Olá distribuição Ubuntu Linux.</span><span class="sxs-lookup"><span data-stu-id="7911f-152">Linux-based HDInsight is based on hello Ubuntu Linux distribution.</span></span> <span data-ttu-id="7911f-153">Versões diferentes do HDInsight contam com versões diferentes do Ubuntu, o que pode afetar o comportamento do seu script.</span><span class="sxs-lookup"><span data-stu-id="7911f-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="7911f-154">Por exemplo, HDInsight 3.4 e versões mais recentes são baseados em versões do Ubuntu que usam o Upstart.</span><span class="sxs-lookup"><span data-stu-id="7911f-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="7911f-155">A versão 3.5 baseia-se no Ubuntu 16.04, que usa Systemd.</span><span class="sxs-lookup"><span data-stu-id="7911f-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="7911f-156">Systemd e Upstart dependem comandos diferentes, para que o script deve ser gravado toowork com ambos.</span><span class="sxs-lookup"><span data-stu-id="7911f-156">Systemd and Upstart rely on different commands, so your script should be written toowork with both.</span></span>

<span data-ttu-id="7911f-157">Outra diferença importante entre HDInsight 3.4 e 3.5 é que `JAVA_HOME` agora aponta tooJava 8.</span><span class="sxs-lookup"><span data-stu-id="7911f-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points tooJava 8.</span></span>

<span data-ttu-id="7911f-158">Você pode verificar a versão de hello SO usando `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="7911f-158">You can check hello OS version by using `lsb_release`.</span></span> <span data-ttu-id="7911f-159">Olá código a seguir demonstra como toodetermine se hello script está em execução no Ubuntu 14 ou 16:</span><span class="sxs-lookup"><span data-stu-id="7911f-159">hello following code demonstrates how toodetermine if hello script is running on Ubuntu 14 or 16:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

<span data-ttu-id="7911f-160">Você pode encontrar o script hello completo contém estes trechos de código em https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span><span class="sxs-lookup"><span data-stu-id="7911f-160">You can find hello full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="7911f-161">Para a versão de saudação do Ubuntu que é usado pelo HDInsight, consulte Olá [HDInsight a versão do componente](hdinsight-component-versioning.md) documento.</span><span class="sxs-lookup"><span data-stu-id="7911f-161">For hello version of Ubuntu that is used by HDInsight, see hello [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="7911f-162">diferenças de saudação toounderstand entre Systemd e Upstart, consulte [Systemd para usuários Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="7911f-162">toounderstand hello differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="7911f-163"><a name="bPS2"></a>Fornecer estável links tooscript recursos</span><span class="sxs-lookup"><span data-stu-id="7911f-163"><a name="bPS2"></a>Provide stable links tooscript resources</span></span>

<span data-ttu-id="7911f-164">Olá script e os recursos associados devem permanecer disponíveis durante o tempo de vida de saudação do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7911f-164">hello script and associated resources must remain available throughout hello lifetime of hello cluster.</span></span> <span data-ttu-id="7911f-165">Esses recursos são necessários se novos nós forem adicionados toohello cluster durante as operações de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="7911f-165">These resources are required if new nodes are added toohello cluster during scaling operations.</span></span>

<span data-ttu-id="7911f-166">prática recomendada Olá é toodownload e arquivar tudo em uma conta de armazenamento do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="7911f-166">hello best practice is toodownload and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7911f-167">conta de armazenamento Olá usada deve ser uma conta de armazenamento de padrão Olá para cluster de saudação ou um contêiner público, somente leitura em qualquer outra conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7911f-167">hello storage account used must be hello default storage account for hello cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="7911f-168">Por exemplo, os exemplos de saudação fornecidos pela Microsoft são armazenados em Olá [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7911f-168">For example, hello samples provided by Microsoft are stored in hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="7911f-169">Isso é um contêiner de público, somente leitura mantido pela equipe de HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7911f-169">This is a public, read-only container maintained by hello HDInsight team.</span></span>

### <span data-ttu-id="7911f-170"><a name="bPS4"></a>Usar os recursos pré-compilados</span><span class="sxs-lookup"><span data-stu-id="7911f-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="7911f-171">Olá tooreduce tempo que demora toorun Olá script, evite operações que são compilados recursos do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="7911f-171">tooreduce hello time it takes toorun hello script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="7911f-172">Por exemplo, pré-compilar recursos e armazená-las em um blob da conta de armazenamento do Azure no hello mesmo data center que HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7911f-172">For example, pre-compile resources and store them in an Azure Storage account blob in hello same data center as HDInsight.</span></span>

### <span data-ttu-id="7911f-173"><a name="bPS3"></a>Certifique-se de que o script de personalização de cluster Olá é idempotente</span><span class="sxs-lookup"><span data-stu-id="7911f-173"><a name="bPS3"></a>Ensure that hello cluster customization script is idempotent</span></span>

<span data-ttu-id="7911f-174">Os scripts devem ser idempotentes.</span><span class="sxs-lookup"><span data-stu-id="7911f-174">Scripts must be idempotent.</span></span> <span data-ttu-id="7911f-175">Se o script hello será executado várias vezes, ele deverá retornar Olá toohello cluster mesmo estado de cada vez.</span><span class="sxs-lookup"><span data-stu-id="7911f-175">If hello script runs multiple times, it should return hello cluster toohello same state every time.</span></span>

<span data-ttu-id="7911f-176">Por exemplo, um script que modifica os arquivos de configuração não deve adicionar entradas duplicadas se executado várias vezes.</span><span class="sxs-lookup"><span data-stu-id="7911f-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="7911f-177"><a name="bPS5"></a>Garantir a alta disponibilidade da arquitetura de cluster Olá</span><span class="sxs-lookup"><span data-stu-id="7911f-177"><a name="bPS5"></a>Ensure high availability of hello cluster architecture</span></span>

<span data-ttu-id="7911f-178">Clusters de HDInsight baseados em Linux fornecem dois nós de cabeçalho que estão ativo no cluster hello e executar ações de script em ambos os nós.</span><span class="sxs-lookup"><span data-stu-id="7911f-178">Linux-based HDInsight clusters provide two head nodes that are active within hello cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="7911f-179">Se a instalação de componentes de saudação esperam apenas um nó principal, não instale os componentes de saudação em ambos os nós principal.</span><span class="sxs-lookup"><span data-stu-id="7911f-179">If hello components you install expect only one head node, do not install hello components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7911f-180">Os serviços fornecidos como parte do HDInsight são toofail projetado através entre dois nós de cabeça Olá conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="7911f-180">Services provided as part of HDInsight are designed toofail over between hello two head nodes as needed.</span></span> <span data-ttu-id="7911f-181">Essa funcionalidade não é estendida toocustom componentes instalados por meio de ações de script.</span><span class="sxs-lookup"><span data-stu-id="7911f-181">This functionality is not extended toocustom components installed through script actions.</span></span> <span data-ttu-id="7911f-182">Se você precisar de alta disponibilidade para componentes personalizados, você deverá implementar seu próprio mecanismo de failover.</span><span class="sxs-lookup"><span data-stu-id="7911f-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="7911f-183"><a name="bPS6"></a>Configurar o armazenamento de BLOBs do Azure em toouse Olá componentes personalizados</span><span class="sxs-lookup"><span data-stu-id="7911f-183"><a name="bPS6"></a>Configure hello custom components toouse Azure Blob storage</span></span>

<span data-ttu-id="7911f-184">Componentes que você instalar no cluster Olá podem ter uma configuração padrão que usa o armazenamento do sistema de arquivos distribuído da Hadoop (HDFS).</span><span class="sxs-lookup"><span data-stu-id="7911f-184">Components that you install on hello cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="7911f-185">HDInsight usa o armazenamento do Azure ou repositório Data Lake como armazenamento de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="7911f-185">HDInsight uses either Azure Storage or Data Lake Store as hello default storage.</span></span> <span data-ttu-id="7911f-186">Oferecem um sistema de arquivos compatíveis do HDFS que persiste dados mesmo que o cluster Olá é excluído.</span><span class="sxs-lookup"><span data-stu-id="7911f-186">Both provide an HDFS compatible file system that persists data even if hello cluster is deleted.</span></span> <span data-ttu-id="7911f-187">Talvez seja necessário tooconfigure componentes instalar toouse WASB ou publicitário em vez de HDFS.</span><span class="sxs-lookup"><span data-stu-id="7911f-187">You may need tooconfigure components you install toouse WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="7911f-188">Para a maioria das operações, não é necessário toospecify sistema de arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="7911f-188">For most operations, you do not need toospecify hello file system.</span></span> <span data-ttu-id="7911f-189">Por exemplo, seguinte Olá copia o arquivo de giraph examples.jar de saudação do armazenamento de toocluster do sistema de arquivos local hello:</span><span class="sxs-lookup"><span data-stu-id="7911f-189">For example, hello following copies hello giraph-examples.jar file from hello local file system toocluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="7911f-190">Neste exemplo, Olá `hdfs` comando transparentemente usa armazenamento de cluster saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="7911f-190">In this example, hello `hdfs` command transparently uses hello default cluster storage.</span></span> <span data-ttu-id="7911f-191">Para algumas operações, talvez seja necessário toospecify Olá URI.</span><span class="sxs-lookup"><span data-stu-id="7911f-191">For some operations, you may need toospecify hello URI.</span></span> <span data-ttu-id="7911f-192">Por exemplo, `adl:///example/jars` para Data Lake Store ou `wasb:///example/jars` para o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="7911f-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="7911f-193"><a name="bPS7"></a>Gravar informações tooSTDOUT e STDERR</span><span class="sxs-lookup"><span data-stu-id="7911f-193"><a name="bPS7"></a>Write information tooSTDOUT and STDERR</span></span>

<span data-ttu-id="7911f-194">HDInsight registra a saída do script é escrito tooSTDOUT e STDERR.</span><span class="sxs-lookup"><span data-stu-id="7911f-194">HDInsight logs script output that is written tooSTDOUT and STDERR.</span></span> <span data-ttu-id="7911f-195">Você pode exibir essas informações usando a interface da web hello Ambari.</span><span class="sxs-lookup"><span data-stu-id="7911f-195">You can view this information using hello Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="7911f-196">Ambari só estará disponível se o cluster de saudação é criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="7911f-196">Ambari is only available if hello cluster is successfully created.</span></span> <span data-ttu-id="7911f-197">Se você usar uma ação de script durante a criação do cluster e falha de criação, consulte seção de solução de problemas de saudação [HDInsight personalizar clusters usando a ação de script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) para outras maneiras de acessar as informações registradas.</span><span class="sxs-lookup"><span data-stu-id="7911f-197">If you use a script action during cluster creation, and creation fails, see hello troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="7911f-198">A maioria dos pacotes de instalação e utilitários já gravam informações tooSTDOUT e STDERR, no entanto, convém tooadd adicionais de log.</span><span class="sxs-lookup"><span data-stu-id="7911f-198">Most utilities and installation packages already write information tooSTDOUT and STDERR, however you may want tooadd additional logging.</span></span> <span data-ttu-id="7911f-199">toosend texto tooSTDOUT, use `echo`.</span><span class="sxs-lookup"><span data-stu-id="7911f-199">toosend text tooSTDOUT, use `echo`.</span></span> <span data-ttu-id="7911f-200">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7911f-200">For example:</span></span>

```bash
echo "Getting ready tooinstall Foo"
```

<span data-ttu-id="7911f-201">Por padrão, `echo` envia Olá tooSTDOUT de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="7911f-201">By default, `echo` sends hello string tooSTDOUT.</span></span> <span data-ttu-id="7911f-202">toodirect-tooSTDERR, adicionar `>&2` antes de `echo`.</span><span class="sxs-lookup"><span data-stu-id="7911f-202">toodirect it tooSTDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="7911f-203">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7911f-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="7911f-204">Isso redirecionará informações gravadas tooSTDOUT tooSTDERR (2) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="7911f-204">This redirects information written tooSTDOUT tooSTDERR (2) instead.</span></span> <span data-ttu-id="7911f-205">Para obter mais informações sobre redirecionamento de E/S, consulte [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="7911f-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="7911f-206">Para saber mais sobre exibição de informações registradas em log por ações de script, confira [Personalizar clusters HDInsight usando ação de script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="7911f-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="7911f-207"><a name="bps8"></a> Salvar arquivos como ASCII com terminações de linha LF</span><span class="sxs-lookup"><span data-stu-id="7911f-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="7911f-208">Scripts de Bash devem ser armazenados com formato ASCII, com linhas terminadas em LF.</span><span class="sxs-lookup"><span data-stu-id="7911f-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="7911f-209">Arquivos que são armazenados como UTF-8, ou usam CRLF como final de linha hello podem falhar com hello erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="7911f-209">Files that are stored as UTF-8, or use CRLF as hello line ending may fail with hello following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="7911f-210"><a name="bps9"></a>Usar toorecover de lógica de repetição de erros transitórios</span><span class="sxs-lookup"><span data-stu-id="7911f-210"><a name="bps9"></a> Use retry logic toorecover from transient errors</span></span>

<span data-ttu-id="7911f-211">Ao fazer o download de arquivos, instalando os pacotes usando apt get ou outras ações que transmitem dados sobre Olá da internet, ação Olá pode falhar devido a erros de rede tootransient.</span><span class="sxs-lookup"><span data-stu-id="7911f-211">When downloading files, installing packages using apt-get, or other actions that transmit data over hello internet, hello action may fail due tootransient networking errors.</span></span> <span data-ttu-id="7911f-212">Por exemplo, o recurso remoto hello, com que você está se comunicando pode ser no processo de saudação da falha ao nó de backup tooa.</span><span class="sxs-lookup"><span data-stu-id="7911f-212">For example, hello remote resource you are communicating with may be in hello process of failing over tooa backup node.</span></span>

<span data-ttu-id="7911f-213">toomake os erros do script tootransient resiliente, você pode implementar a lógica de repetição.</span><span class="sxs-lookup"><span data-stu-id="7911f-213">toomake your script resilient tootransient errors, you can implement retry logic.</span></span> <span data-ttu-id="7911f-214">saudação de função a seguir demonstra como tooimplement lógica de repetição.</span><span class="sxs-lookup"><span data-stu-id="7911f-214">hello following function demonstrates how tooimplement retry logic.</span></span> <span data-ttu-id="7911f-215">Tentar novamente a operação Olá três vezes antes de falhar.</span><span class="sxs-lookup"><span data-stu-id="7911f-215">It retries hello operation three times before failing.</span></span>

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

<span data-ttu-id="7911f-216">Olá exemplos a seguir demonstram como toouse essa função.</span><span class="sxs-lookup"><span data-stu-id="7911f-216">hello following examples demonstrate how toouse this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="7911f-217"><a name="helpermethods"></a>Métodos auxiliares para scripts personalizados</span><span class="sxs-lookup"><span data-stu-id="7911f-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="7911f-218">Os métodos auxiliares da Ação de Script são utilitários que podem ser usados durante a gravação de scripts personalizados.</span><span class="sxs-lookup"><span data-stu-id="7911f-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="7911f-219">Esses métodos estão contidos no script [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="7911f-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="7911f-220">Use Olá toodownload a seguir e usá-los como parte do script:</span><span class="sxs-lookup"><span data-stu-id="7911f-220">Use hello following toodownload and use them as part of your script:</span></span>

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="7911f-221">Olá auxiliares disponíveis para uso em seu script a seguir:</span><span class="sxs-lookup"><span data-stu-id="7911f-221">hello following helpers available for use in your script:</span></span>

| <span data-ttu-id="7911f-222">Uso do auxiliar</span><span class="sxs-lookup"><span data-stu-id="7911f-222">Helper usage</span></span> | <span data-ttu-id="7911f-223">Descrição</span><span class="sxs-lookup"><span data-stu-id="7911f-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="7911f-224">Baixa um arquivo do caminho de arquivo especificado toohello do URI de origem hello.</span><span class="sxs-lookup"><span data-stu-id="7911f-224">Downloads a file from hello source URI toohello specified file path.</span></span> <span data-ttu-id="7911f-225">Por padrão, ele não substitui um arquivo existente.</span><span class="sxs-lookup"><span data-stu-id="7911f-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="7911f-226">Extrai um arquivo tar (usando `-xf`) toohello diretório de destino.</span><span class="sxs-lookup"><span data-stu-id="7911f-226">Extracts a tar file (using `-xf`) toohello destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="7911f-227">Se executado em um nó de cabeçalho do cluster, retorna 1. Caso contrário, 0.</span><span class="sxs-lookup"><span data-stu-id="7911f-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="7911f-228">Se o nó atual Olá for um nó de dados (trabalho), retornar um 1; Caso contrário, 0.</span><span class="sxs-lookup"><span data-stu-id="7911f-228">If hello current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="7911f-229">Se Olá atual é dados primeiro saudação (trabalho) nó (chamado workernode0) retornará 1; Caso contrário, 0.</span><span class="sxs-lookup"><span data-stu-id="7911f-229">If hello current node is hello first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="7911f-230">Retorne o nome de domínio totalmente qualificado de saudação do hello headnodes no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="7911f-230">Return hello fully qualified domain name of hello headnodes in hello cluster.</span></span> <span data-ttu-id="7911f-231">Os nomes são delimitados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="7911f-231">Names are comma delimited.</span></span> <span data-ttu-id="7911f-232">Uma cadeia de caracteres vazia retorna em caso de erro.</span><span class="sxs-lookup"><span data-stu-id="7911f-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="7911f-233">Obtém o nome de domínio totalmente qualificado de saudação do nó primário principal de saudação.</span><span class="sxs-lookup"><span data-stu-id="7911f-233">Gets hello fully qualified domain name of hello primary headnode.</span></span> <span data-ttu-id="7911f-234">Uma cadeia de caracteres vazia retorna em caso de erro.</span><span class="sxs-lookup"><span data-stu-id="7911f-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="7911f-235">Obtém o nome de domínio totalmente qualificado de saudação do nó secundário principal de saudação.</span><span class="sxs-lookup"><span data-stu-id="7911f-235">Gets hello fully qualified domain name of hello secondary headnode.</span></span> <span data-ttu-id="7911f-236">Uma cadeia de caracteres vazia retorna em caso de erro.</span><span class="sxs-lookup"><span data-stu-id="7911f-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="7911f-237">Obtém o sufixo numérico de saudação do nó primário principal de saudação.</span><span class="sxs-lookup"><span data-stu-id="7911f-237">Gets hello numeric suffix of hello primary headnode.</span></span> <span data-ttu-id="7911f-238">Uma cadeia de caracteres vazia retorna em caso de erro.</span><span class="sxs-lookup"><span data-stu-id="7911f-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="7911f-239">Obtém o sufixo numérico de saudação do nó secundário principal de saudação.</span><span class="sxs-lookup"><span data-stu-id="7911f-239">Gets hello numeric suffix of hello secondary headnode.</span></span> <span data-ttu-id="7911f-240">Uma cadeia de caracteres vazia retorna em caso de erro.</span><span class="sxs-lookup"><span data-stu-id="7911f-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="7911f-241"><a name="commonusage"></a>Padrões comuns de uso</span><span class="sxs-lookup"><span data-stu-id="7911f-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="7911f-242">Esta seção fornece orientação sobre como implementar alguns Olá padrões comuns de uso que você pode encontrar ao gravar seu próprio script personalizado.</span><span class="sxs-lookup"><span data-stu-id="7911f-242">This section provides guidance on implementing some of hello common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-tooa-script"></a><span data-ttu-id="7911f-243">Passando parâmetros de script tooa</span><span class="sxs-lookup"><span data-stu-id="7911f-243">Passing parameters tooa script</span></span>

<span data-ttu-id="7911f-244">Em alguns casos, seu script pode exigir parâmetros.</span><span class="sxs-lookup"><span data-stu-id="7911f-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="7911f-245">Por exemplo, talvez seja necessário senha do administrador Olá para cluster Olá ao usar Olá API REST do Ambari.</span><span class="sxs-lookup"><span data-stu-id="7911f-245">For example, you may need hello admin password for hello cluster when using hello Ambari REST API.</span></span>

<span data-ttu-id="7911f-246">Parâmetros passados toohello script são conhecidos como *parâmetros posicionais*e são atribuídos muito`$1` para o primeiro parâmetro de hello, `$2` para Olá segundo e portanto no.</span><span class="sxs-lookup"><span data-stu-id="7911f-246">Parameters passed toohello script are known as *positional parameters*, and are assigned too`$1` for hello first parameter, `$2` for hello second, and so-on.</span></span> <span data-ttu-id="7911f-247">`$0`contém o nome de saudação do próprio script hello.</span><span class="sxs-lookup"><span data-stu-id="7911f-247">`$0` contains hello name of hello script itself.</span></span>

<span data-ttu-id="7911f-248">Os valores passados toohello script como parâmetros devem ser fechados por aspas simples (').</span><span class="sxs-lookup"><span data-stu-id="7911f-248">Values passed toohello script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="7911f-249">Isso garante que Olá passado valor é tratado como um literal.</span><span class="sxs-lookup"><span data-stu-id="7911f-249">Doing so ensures that hello passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="7911f-250">Configurando variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="7911f-250">Setting environment variables</span></span>

<span data-ttu-id="7911f-251">Definir uma variável de ambiente é executada por Olá instrução a seguir:</span><span class="sxs-lookup"><span data-stu-id="7911f-251">Setting an environment variable is performed by hello following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="7911f-252">Onde o VARIABLENAME é o nome de saudação da variável de saudação.</span><span class="sxs-lookup"><span data-stu-id="7911f-252">Where VARIABLENAME is hello name of hello variable.</span></span> <span data-ttu-id="7911f-253">uso da variável, Olá tooaccess `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="7911f-253">tooaccess hello variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="7911f-254">Por exemplo, tooassign um valor fornecido por um parâmetro posicional como uma variável de ambiente denominada senha, você usaria Olá instrução a seguir:</span><span class="sxs-lookup"><span data-stu-id="7911f-254">For example, tooassign a value provided by a positional parameter as an environment variable named PASSWORD, you would use hello following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="7911f-255">Informações de toohello acesso subsequente podem usar `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="7911f-255">Subsequent access toohello information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="7911f-256">Variáveis de ambiente definida no script hello existem somente no escopo de saudação do script hello.</span><span class="sxs-lookup"><span data-stu-id="7911f-256">Environment variables set within hello script only exist within hello scope of hello script.</span></span> <span data-ttu-id="7911f-257">Em alguns casos, talvez seja necessário variáveis de ambiente de todo o sistema de tooadd que serão mantido depois que o script hello terminou.</span><span class="sxs-lookup"><span data-stu-id="7911f-257">In some cases, you may need tooadd system-wide environment variables that will persist after hello script has finished.</span></span> <span data-ttu-id="7911f-258">variáveis de ambiente de todo o sistema tooadd, adicione a variável de saudação muito`/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="7911f-258">tooadd system-wide environment variables, add hello variable too`/etc/environment`.</span></span> <span data-ttu-id="7911f-259">Por exemplo, a saudação instrução a seguir adiciona `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="7911f-259">For example, hello following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a><span data-ttu-id="7911f-260">Acesso toolocations onde são armazenados os scripts personalizados Olá</span><span class="sxs-lookup"><span data-stu-id="7911f-260">Access toolocations where hello custom scripts are stored</span></span>

<span data-ttu-id="7911f-261">Scripts usados toocustomize um cluster precisa toobe armazenado em uma saudação locais a seguir:</span><span class="sxs-lookup"><span data-stu-id="7911f-261">Scripts used toocustomize a cluster needs toobe stored in one of hello following locations:</span></span>

* <span data-ttu-id="7911f-262">Um __conta de armazenamento do Azure__ que está associado ao cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7911f-262">An __Azure Storage account__ that is associated with hello cluster.</span></span>

* <span data-ttu-id="7911f-263">Um __conta de armazenamento adicional__ associada Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="7911f-263">An __additional storage account__ associated with hello cluster.</span></span>

* <span data-ttu-id="7911f-264">Um URI __que pode ser lido publicamente__.</span><span class="sxs-lookup"><span data-stu-id="7911f-264">A __publicly readable URI__.</span></span> <span data-ttu-id="7911f-265">Por exemplo, uma URL toodata armazenado no OneDrive, Dropbox ou outro arquivo de serviço de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="7911f-265">For example, a URL toodata stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="7911f-266">Um __conta do repositório Azure Data Lake__ que está associado ao cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="7911f-266">An __Azure Data Lake Store account__ that is associated with hello HDInsight cluster.</span></span> <span data-ttu-id="7911f-267">Para obter mais informações sobre o uso do Azure Data Lake Store com o HDInsight, veja [Criar um cluster HDInsight com o Repositório Data Lake](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7911f-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="7911f-268">Olá serviço principal HDInsight usa tooaccess repositório Data Lake deve ter acesso de leitura toohello script.</span><span class="sxs-lookup"><span data-stu-id="7911f-268">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

<span data-ttu-id="7911f-269">Recursos usados pelo script hello também devem estar publicamente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="7911f-269">Resources used by hello script must also be publicly available.</span></span>

<span data-ttu-id="7911f-270">Armazenar arquivos de saudação em uma conta de armazenamento do Azure ou um repositório Azure Data Lake fornece acesso rápido, como ambos em Olá rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="7911f-270">Storing hello files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within hello Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="7911f-271">Olá URI formato usado tooreference Olá script difere dependendo de serviço hello está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="7911f-271">hello URI format used tooreference hello script differs depending on hello service being used.</span></span> <span data-ttu-id="7911f-272">Para contas de armazenamento associadas com o cluster do HDInsight hello, use `wasb://` ou `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="7911f-272">For storage accounts associated with hello HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="7911f-273">Para URIs lidas publicamente, use `http://` ou `https://`.</span><span class="sxs-lookup"><span data-stu-id="7911f-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="7911f-274">Para Data Lake Store, use `adl://`.</span><span class="sxs-lookup"><span data-stu-id="7911f-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-hello-operating-system-version"></a><span data-ttu-id="7911f-275">Verificando a versão do sistema operacional Olá</span><span class="sxs-lookup"><span data-stu-id="7911f-275">Checking hello operating system version</span></span>

<span data-ttu-id="7911f-276">Versões diferentes do HDInsight contam com versões específicas do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="7911f-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="7911f-277">Pode haver diferenças entre as versões de sistema operacional, que você deve verificar em seu script.</span><span class="sxs-lookup"><span data-stu-id="7911f-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="7911f-278">Por exemplo, talvez seja necessário tooinstall um binário de versão associado toohello do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="7911f-278">For example, you may need tooinstall a binary that is tied toohello version of Ubuntu.</span></span>

<span data-ttu-id="7911f-279">toocheck Olá SO a versão `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="7911f-279">toocheck hello OS version, use `lsb_release`.</span></span> <span data-ttu-id="7911f-280">Por exemplo, a saudação script a seguir demonstra como tooreference um tar específico de arquivo dependendo Olá versão do sistema operacional:</span><span class="sxs-lookup"><span data-stu-id="7911f-280">For example, hello following script demonstrates how tooreference a specific tar file depending on hello OS version:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <span data-ttu-id="7911f-281"><a name="deployScript"></a>Lista de verificação para implantação de uma ação de script</span><span class="sxs-lookup"><span data-stu-id="7911f-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="7911f-282">Aqui estão as etapas Olá que demos ao preparar toodeploy esses scripts:</span><span class="sxs-lookup"><span data-stu-id="7911f-282">Here are hello steps we took when preparing toodeploy these scripts:</span></span>

* <span data-ttu-id="7911f-283">Coloca os arquivos de saudação que contêm scripts personalizados de saudação em um local que seja acessível por nós de cluster Olá durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="7911f-283">Put hello files that contain hello custom scripts in a place that is accessible by hello cluster nodes during deployment.</span></span> <span data-ttu-id="7911f-284">Por exemplo, Olá armazenamento padrão para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="7911f-284">For example, hello default storage for hello cluster.</span></span> <span data-ttu-id="7911f-285">Arquivos também podem ser armazenados nos serviços de hospedagem legíveis publicamente.</span><span class="sxs-lookup"><span data-stu-id="7911f-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="7911f-286">Verifique se o script hello é impotent.</span><span class="sxs-lookup"><span data-stu-id="7911f-286">Verify that hello script is impotent.</span></span> <span data-ttu-id="7911f-287">Isso permite Olá script toobe executada várias vezes em Olá mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="7911f-287">Doing so allows hello script toobe executed multiple times on hello same node.</span></span>
* <span data-ttu-id="7911f-288">Use uma saudação do arquivo temporário diretório /tmp tookeep baixado os arquivos usados pelos scripts de saudação e depois limpá-los depois de scripts foram executadas.</span><span class="sxs-lookup"><span data-stu-id="7911f-288">Use a temporary file directory /tmp tookeep hello downloaded files used by hello scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="7911f-289">Se as configurações de nível de sistema operacional ou arquivos de configuração do serviço de Hadoop forem alterados, convém toorestart HDInsight serviços.</span><span class="sxs-lookup"><span data-stu-id="7911f-289">If OS-level settings or Hadoop service configuration files are changed, you may want toorestart HDInsight services.</span></span>

## <span data-ttu-id="7911f-290"><a name="runScriptAction"></a>Como toorun uma ação de script</span><span class="sxs-lookup"><span data-stu-id="7911f-290"><a name="runScriptAction"></a>How toorun a script action</span></span>

<span data-ttu-id="7911f-291">Você pode usar clusters de HDInsight do script ações toocustomize usando Olá métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="7911f-291">You can use script actions toocustomize HDInsight clusters using hello following methods:</span></span>

* <span data-ttu-id="7911f-292">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7911f-292">Azure portal</span></span>
* <span data-ttu-id="7911f-293">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="7911f-293">Azure PowerShell</span></span>
* <span data-ttu-id="7911f-294">Modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="7911f-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="7911f-295">Olá HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="7911f-295">hello HDInsight .NET SDK.</span></span>

<span data-ttu-id="7911f-296">Para obter mais informações sobre como usar cada método, consulte [como toouse scripts de ação](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7911f-296">For more information on using each method, see [How toouse script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="7911f-297"><a name="sampleScripts"></a>Exemplos de script personalizado</span><span class="sxs-lookup"><span data-stu-id="7911f-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="7911f-298">Microsoft fornece scripts de exemplo tooinstall componentes em um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7911f-298">Microsoft provides sample scripts tooinstall components on an HDInsight cluster.</span></span> <span data-ttu-id="7911f-299">Consulte Olá links para mais ações de script de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="7911f-299">See hello following links for more example script actions.</span></span>

* [<span data-ttu-id="7911f-300">Instalar e usar o Hue em clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="7911f-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="7911f-301">Instalar e usar o Solr em clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="7911f-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="7911f-302">Instalar e usar o Giraph em clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="7911f-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="7911f-303">Instalar ou atualizar o Mono em clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="7911f-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="7911f-304">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="7911f-304">Troubleshooting</span></span>

<span data-ttu-id="7911f-305">Olá seguem erros que você pode encontrar ao usar scripts que você desenvolveu:</span><span class="sxs-lookup"><span data-stu-id="7911f-305">hello following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="7911f-306">**Erro**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="7911f-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="7911f-307">Às vezes, seguido por `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="7911f-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="7911f-308">*Causa*: este erro é causado quando terminam de linhas de saudação em um script com CRLF.</span><span class="sxs-lookup"><span data-stu-id="7911f-308">*Cause*: This error is caused when hello lines in a script end with CRLF.</span></span> <span data-ttu-id="7911f-309">Sistemas UNIX esperam LF apenas como final de linha de saudação.</span><span class="sxs-lookup"><span data-stu-id="7911f-309">Unix systems expect only LF as hello line ending.</span></span>

<span data-ttu-id="7911f-310">Esse problema geralmente ocorre quando o script hello é criado em um ambiente do Windows, como CRLF é uma linha comum final para muitos editores de texto no Windows.</span><span class="sxs-lookup"><span data-stu-id="7911f-310">This problem most often occurs when hello script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="7911f-311">*Resolução*: se ela é uma opção em seu editor de texto, selecione o formato Unix ou LF para terminação de linha de saudação.</span><span class="sxs-lookup"><span data-stu-id="7911f-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for hello line ending.</span></span> <span data-ttu-id="7911f-312">Você também pode usar os comandos a seguir em uma instalação do Unix sistema toochange Olá CRLF tooan LF de saudação:</span><span class="sxs-lookup"><span data-stu-id="7911f-312">You may also use hello following commands on a Unix system toochange hello CRLF tooan LF:</span></span>

> [!NOTE]
> <span data-ttu-id="7911f-313">Olá comandos a seguir são equivalentes em que eles devem alterar tooLF de terminações de linha hello CRLF.</span><span class="sxs-lookup"><span data-stu-id="7911f-313">hello following commands are roughly equivalent in that they should change hello CRLF line endings tooLF.</span></span> <span data-ttu-id="7911f-314">Selecione uma opção com base em utilitários de saudação disponíveis no sistema.</span><span class="sxs-lookup"><span data-stu-id="7911f-314">Select one based on hello utilities available on your system.</span></span>

| <span data-ttu-id="7911f-315">Command</span><span class="sxs-lookup"><span data-stu-id="7911f-315">Command</span></span> | <span data-ttu-id="7911f-316">Observações</span><span class="sxs-lookup"><span data-stu-id="7911f-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="7911f-317">arquivo original Olá é feito com um. Extensão BAK</span><span class="sxs-lookup"><span data-stu-id="7911f-317">hello original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="7911f-318">OUTFILE contém uma versão apenas com terminações LF</span><span class="sxs-lookup"><span data-stu-id="7911f-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="7911f-319">Modifica o arquivo hello diretamente</span><span class="sxs-lookup"><span data-stu-id="7911f-319">Modifies hello file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="7911f-320">OUTFILE contém uma versão apenas com terminações LF.</span><span class="sxs-lookup"><span data-stu-id="7911f-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="7911f-321">**Erro**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="7911f-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="7911f-322">*Causa*: este erro ocorre quando hello script foi salvo como UTF-8 com marca de ordem de um Byte (BOM).</span><span class="sxs-lookup"><span data-stu-id="7911f-322">*Cause*: This error occurs when hello script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="7911f-323">*Resolução*: Olá de salvar arquivo como ASCII ou UTF-8 sem um BOM.</span><span class="sxs-lookup"><span data-stu-id="7911f-323">*Resolution*: Save hello file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="7911f-324">Você também pode usar o hello comando a seguir em um toocreate de sistema Linux ou Unix um arquivo sem Olá BOM:</span><span class="sxs-lookup"><span data-stu-id="7911f-324">You may also use hello following command on a Linux or Unix system toocreate a file without hello BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="7911f-325">Substituir `INFILE` com arquivo hello contendo Olá BOM.</span><span class="sxs-lookup"><span data-stu-id="7911f-325">Replace `INFILE` with hello file containing hello BOM.</span></span> <span data-ttu-id="7911f-326">`OUTFILE`deve ser um novo nome de arquivo que contém o script hello sem Olá BOM.</span><span class="sxs-lookup"><span data-stu-id="7911f-326">`OUTFILE` should be a new file name, which contains hello script without hello BOM.</span></span>

## <span data-ttu-id="7911f-327"><a name="seeAlso"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7911f-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="7911f-328">Saiba como muito[clusters de HDInsight personalizar usando a ação de script](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="7911f-328">Learn how too[Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="7911f-329">Saudação de uso [referência do HDInsight .NET SDK](https://msdn.microsoft.com/library/mt271028.aspx) toolearn mais sobre a criação de aplicativos .NET que gerenciar o HDInsight</span><span class="sxs-lookup"><span data-stu-id="7911f-329">Use hello [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) toolearn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="7911f-330">Saudação de uso [API REST do HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn como clusters de ações de gerenciamento de tooperform toouse REST no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7911f-330">Use hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn how toouse REST tooperform management actions on HDInsight clusters.</span></span>
