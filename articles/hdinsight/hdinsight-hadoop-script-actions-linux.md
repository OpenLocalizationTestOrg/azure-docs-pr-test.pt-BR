---
title: "Desenvolvimento de ação de script com o HDInsight baseado em Linux – Azure | Microsoft Docs"
description: "Saiba como usar scripts Bash para personalizar os clusters HDInsight baseados em Linux. O recurso de ação de script do HDInsight permite executar scripts durante ou após a criação do cluster. Scripts podem ser usados para alterar as configurações do cluster ou instalar software adicional."
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
ms.openlocfilehash: 7f1a0bd8c7e60770d376f10eaea136a55c632c5e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="e71b3-105">Desenvolvimento de ação de script com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="e71b3-105">Script action development with HDInsight</span></span>

<span data-ttu-id="e71b3-106">Saiba como personalizar o cluster HDInsight usando scripts Bash.</span><span class="sxs-lookup"><span data-stu-id="e71b3-106">Learn how to customize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="e71b3-107">Ações de script são uma maneira de personalizar o HDInsight durante ou após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="e71b3-107">Script actions are a way to customize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e71b3-108">As etapas deste documento exigem um cluster HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="e71b3-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="e71b3-109">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="e71b3-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e71b3-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="e71b3-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="e71b3-111">O que são ações de script</span><span class="sxs-lookup"><span data-stu-id="e71b3-111">What are script actions</span></span>

<span data-ttu-id="e71b3-112">As ações de script são scripts Bash que o Azure executa em nós de cluster para fazer alterações de configuração ou para instalar software.</span><span class="sxs-lookup"><span data-stu-id="e71b3-112">Script actions are Bash scripts that Azure runs on the cluster nodes to make configuration changes or install software.</span></span> <span data-ttu-id="e71b3-113">A Ação de Script é executada como raiz e concede direitos de acesso completo a nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="e71b3-113">A script action is executed as root, and provides full access rights to the cluster nodes.</span></span>

<span data-ttu-id="e71b3-114">As ações de script podem ser aplicadas por meio dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="e71b3-114">Script actions can be applied through the following methods:</span></span>

| <span data-ttu-id="e71b3-115">Use este método para aplicar um script...</span><span class="sxs-lookup"><span data-stu-id="e71b3-115">Use this method to apply a script...</span></span> | <span data-ttu-id="e71b3-116">Durante a criação do cluster...</span><span class="sxs-lookup"><span data-stu-id="e71b3-116">During cluster creation...</span></span> | <span data-ttu-id="e71b3-117">Em um cluster em execução...</span><span class="sxs-lookup"><span data-stu-id="e71b3-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="e71b3-118">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e71b3-118">Azure portal</span></span> |<span data-ttu-id="e71b3-119">✓ </span><span class="sxs-lookup"><span data-stu-id="e71b3-119">✓</span></span> |<span data-ttu-id="e71b3-120">✓</span><span class="sxs-lookup"><span data-stu-id="e71b3-120">✓</span></span> |
| <span data-ttu-id="e71b3-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e71b3-121">Azure PowerShell</span></span> |<span data-ttu-id="e71b3-122">✓</span><span class="sxs-lookup"><span data-stu-id="e71b3-122">✓</span></span> |<span data-ttu-id="e71b3-123">✓</span><span class="sxs-lookup"><span data-stu-id="e71b3-123">✓</span></span> |
| <span data-ttu-id="e71b3-124">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e71b3-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="e71b3-125">✓</span><span class="sxs-lookup"><span data-stu-id="e71b3-125">✓</span></span> |
| <span data-ttu-id="e71b3-126">SDK do .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="e71b3-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="e71b3-127">✓</span><span class="sxs-lookup"><span data-stu-id="e71b3-127">✓</span></span> |<span data-ttu-id="e71b3-128">✓</span><span class="sxs-lookup"><span data-stu-id="e71b3-128">✓</span></span> |
| <span data-ttu-id="e71b3-129">Modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e71b3-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="e71b3-130">✓</span><span class="sxs-lookup"><span data-stu-id="e71b3-130">✓</span></span> |&nbsp; |

<span data-ttu-id="e71b3-131">Para saber mais sobre o uso desses métodos para aplicar ações de script, confira [Personalizar clusters HDInsight usando ações de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e71b3-131">For more information on using these methods to apply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="e71b3-132"><a name="bestPracticeScripting"></a>Práticas recomendadas para o desenvolvimento de scripts</span><span class="sxs-lookup"><span data-stu-id="e71b3-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="e71b3-133">Ao desenvolver um script personalizado para um cluster HDInsight, há várias práticas recomendadas para se considerar:</span><span class="sxs-lookup"><span data-stu-id="e71b3-133">When you develop a custom script for an HDInsight cluster, there are several best practices to keep in mind:</span></span>

* [<span data-ttu-id="e71b3-134">Direcionar para a versão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="e71b3-134">Target the Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="e71b3-135">Direcionar para a versão do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="e71b3-135">Target the OS Version</span></span>](#bps10)
* [<span data-ttu-id="e71b3-136">Fornecer links estáveis para recursos de script</span><span class="sxs-lookup"><span data-stu-id="e71b3-136">Provide stable links to script resources</span></span>](#bPS2)
* [<span data-ttu-id="e71b3-137">Usar os recursos pré-compilados</span><span class="sxs-lookup"><span data-stu-id="e71b3-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="e71b3-138">Certifique-se de que o script de personalização do cluster seja idempotente</span><span class="sxs-lookup"><span data-stu-id="e71b3-138">Ensure that the cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="e71b3-139">Garantir alta disponibilidade da arquitetura de cluster</span><span class="sxs-lookup"><span data-stu-id="e71b3-139">Ensure high availability of the cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="e71b3-140">Configurar os componentes personalizados para usar armazenamento de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="e71b3-140">Configure the custom components to use Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="e71b3-141">Gravar informações para STDOUT e STDERR</span><span class="sxs-lookup"><span data-stu-id="e71b3-141">Write information to STDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="e71b3-142">Salvar arquivos como ASCII com terminações de linha LF</span><span class="sxs-lookup"><span data-stu-id="e71b3-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="e71b3-143">Usar a lógica de repetição para recuperar-se de erros transitórios</span><span class="sxs-lookup"><span data-stu-id="e71b3-143">Use retry logic to recover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="e71b3-144">Ações de script devem ser concluídas em 60 minutos ou o processo falha.</span><span class="sxs-lookup"><span data-stu-id="e71b3-144">Script actions must complete within 60 minutes or the process fails.</span></span> <span data-ttu-id="e71b3-145">Durante o provisionamento de nó, o script é executado simultaneamente com outros processos de instalação e configuração.</span><span class="sxs-lookup"><span data-stu-id="e71b3-145">During node provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="e71b3-146">A competição por recursos, como tempo de CPU ou largura de banda rede, pode fazer com que o script leve mais tempo para ser concluído comparado ao seu tempo de conclusão no ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="e71b3-146">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>

### <span data-ttu-id="e71b3-147"><a name="bPS1"></a>Direcionar para a versão do Hadoop</span><span class="sxs-lookup"><span data-stu-id="e71b3-147"><a name="bPS1"></a>Target the Hadoop version</span></span>

<span data-ttu-id="e71b3-148">Diferentes versões do HDInsight têm diferentes versões de componentes e serviços do Hadoop instaladas.</span><span class="sxs-lookup"><span data-stu-id="e71b3-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="e71b3-149">Se seu script espera uma versão específica de um serviço ou componente, você deve usar somente o script com a versão do HDInsight que inclui os componentes necessários.</span><span class="sxs-lookup"><span data-stu-id="e71b3-149">If your script expects a specific version of a service or component, you should only use the script with the version of HDInsight that includes the required components.</span></span> <span data-ttu-id="e71b3-150">Você pode encontrar informações sobre versões dos componentes incluídos com o HDInsight usando o documento [Controle de versão de componente do HDInsight](hdinsight-component-versioning.md) .</span><span class="sxs-lookup"><span data-stu-id="e71b3-150">You can find information on component versions included with HDInsight using the [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="e71b3-151"><a name="bps10"></a>Direcionar para a versão do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="e71b3-151"><a name="bps10"></a> Target the OS version</span></span>

<span data-ttu-id="e71b3-152">O HDInsight baseado em Linux baseia-se na distribuição do Ubuntu do Linux.</span><span class="sxs-lookup"><span data-stu-id="e71b3-152">Linux-based HDInsight is based on the Ubuntu Linux distribution.</span></span> <span data-ttu-id="e71b3-153">Versões diferentes do HDInsight contam com versões diferentes do Ubuntu, o que pode afetar o comportamento do seu script.</span><span class="sxs-lookup"><span data-stu-id="e71b3-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="e71b3-154">Por exemplo, HDInsight 3.4 e versões mais recentes são baseados em versões do Ubuntu que usam o Upstart.</span><span class="sxs-lookup"><span data-stu-id="e71b3-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="e71b3-155">A versão 3.5 baseia-se no Ubuntu 16.04, que usa Systemd.</span><span class="sxs-lookup"><span data-stu-id="e71b3-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="e71b3-156">O Systemd e Upstart contam com comandos diferentes, portanto seu script deve ser escrito para funcionar com ambos.</span><span class="sxs-lookup"><span data-stu-id="e71b3-156">Systemd and Upstart rely on different commands, so your script should be written to work with both.</span></span>

<span data-ttu-id="e71b3-157">Outra diferença importante entre o HDInsight 3.4 e o 3.5 é que o `JAVA_HOME` agora aponta para o Java 8.</span><span class="sxs-lookup"><span data-stu-id="e71b3-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points to Java 8.</span></span>

<span data-ttu-id="e71b3-158">Você pode verificar a versão do sistema operacional usando `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="e71b3-158">You can check the OS version by using `lsb_release`.</span></span> <span data-ttu-id="e71b3-159">O código a seguir demonstra como determinar se o script está sendo executado no Ubuntu 14 ou 16:</span><span class="sxs-lookup"><span data-stu-id="e71b3-159">The following code demonstrates how to determine if the script is running on Ubuntu 14 or 16:</span></span>

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

<span data-ttu-id="e71b3-160">Você pode encontrar o script completo que contém esses trechos de código em https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span><span class="sxs-lookup"><span data-stu-id="e71b3-160">You can find the full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="e71b3-161">Para a versão do Ubuntu, que é usada pelo HDInsight, consulte o documento [Versão do componente HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="e71b3-161">For the version of Ubuntu that is used by HDInsight, see the [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="e71b3-162">Para entender as diferenças entre Systemd e Upstart, consulte [Systemd para usuários do Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="e71b3-162">To understand the differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="e71b3-163"><a name="bPS2"></a>Fornecer links estáveis para recursos de script</span><span class="sxs-lookup"><span data-stu-id="e71b3-163"><a name="bPS2"></a>Provide stable links to script resources</span></span>

<span data-ttu-id="e71b3-164">O script e recursos associados devem permanecer disponíveis durante o tempo de vida do cluster.</span><span class="sxs-lookup"><span data-stu-id="e71b3-164">The script and associated resources must remain available throughout the lifetime of the cluster.</span></span> <span data-ttu-id="e71b3-165">Esses recursos serão necessários se novos nós forem adicionados ao cluster durante as operações de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="e71b3-165">These resources are required if new nodes are added to the cluster during scaling operations.</span></span>

<span data-ttu-id="e71b3-166">A melhor prática é baixar e arquivar tudo em uma conta de Armazenamento do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e71b3-166">The best practice is to download and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e71b3-167">A conta de armazenamento usada deve ser a conta de armazenamento padrão para o cluster ou então em um contêiner público somente leitura em qualquer outra conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e71b3-167">The storage account used must be the default storage account for the cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="e71b3-168">Por exemplo, os exemplos fornecidos pela Microsoft são armazenados na conta de armazenamento [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/).</span><span class="sxs-lookup"><span data-stu-id="e71b3-168">For example, the samples provided by Microsoft are stored in the [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="e71b3-169">É um contêiner público somente leitura mantido pela equipe do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e71b3-169">This is a public, read-only container maintained by the HDInsight team.</span></span>

### <span data-ttu-id="e71b3-170"><a name="bPS4"></a>Usar os recursos pré-compilados</span><span class="sxs-lookup"><span data-stu-id="e71b3-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="e71b3-171">Para reduzir o tempo necessário de execução do script, evite operações que compilem recursos do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="e71b3-171">To reduce the time it takes to run the script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="e71b3-172">Por exemplo, pré-compile recursos e armazene-os em um blob da conta de Armazenamento do Azure no mesmo data center que o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e71b3-172">For example, pre-compile resources and store them in an Azure Storage account blob in the same data center as HDInsight.</span></span>

### <span data-ttu-id="e71b3-173"><a name="bPS3"></a>Certifique-se de que o script de personalização do cluster seja idempotente</span><span class="sxs-lookup"><span data-stu-id="e71b3-173"><a name="bPS3"></a>Ensure that the cluster customization script is idempotent</span></span>

<span data-ttu-id="e71b3-174">Os scripts devem ser idempotentes.</span><span class="sxs-lookup"><span data-stu-id="e71b3-174">Scripts must be idempotent.</span></span> <span data-ttu-id="e71b3-175">Se o script for executado várias vezes, ele deverá retornar o cluster ao mesmo estado a cada vez.</span><span class="sxs-lookup"><span data-stu-id="e71b3-175">If the script runs multiple times, it should return the cluster to the same state every time.</span></span>

<span data-ttu-id="e71b3-176">Por exemplo, um script que modifica os arquivos de configuração não deve adicionar entradas duplicadas se executado várias vezes.</span><span class="sxs-lookup"><span data-stu-id="e71b3-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="e71b3-177"><a name="bPS5"></a>Garantir alta disponibilidade da arquitetura de cluster</span><span class="sxs-lookup"><span data-stu-id="e71b3-177"><a name="bPS5"></a>Ensure high availability of the cluster architecture</span></span>

<span data-ttu-id="e71b3-178">Os clusters HDInsight baseados em Linux fornecem dois nós de cabeçalho que estão ativos dentro do cluster; as ações de script são executadas em ambos esses nós.</span><span class="sxs-lookup"><span data-stu-id="e71b3-178">Linux-based HDInsight clusters provide two head nodes that are active within the cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="e71b3-179">Se os componentes de que instalação esperam apenas um nó principal, não instale os componentes em ambos os nós de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="e71b3-179">If the components you install expect only one head node, do not install the components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e71b3-180">Os serviços fornecidos como parte do HDInsight são projetados para failover entre os dois nós de cabeçalho, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="e71b3-180">Services provided as part of HDInsight are designed to fail over between the two head nodes as needed.</span></span> <span data-ttu-id="e71b3-181">Essa funcionalidade não se estende a componentes personalizados instalados por meio de ações de script.</span><span class="sxs-lookup"><span data-stu-id="e71b3-181">This functionality is not extended to custom components installed through script actions.</span></span> <span data-ttu-id="e71b3-182">Se você precisar de alta disponibilidade para componentes personalizados, você deverá implementar seu próprio mecanismo de failover.</span><span class="sxs-lookup"><span data-stu-id="e71b3-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="e71b3-183"><a name="bPS6"></a>Configurar os componentes personalizados para usar armazenamento de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="e71b3-183"><a name="bPS6"></a>Configure the custom components to use Azure Blob storage</span></span>

<span data-ttu-id="e71b3-184">Os componentes que você instala no cluster podem ter uma configuração padrão que usa o armazenamento HDFS (Sistema de Arquivos Distribuído do Hadoop).</span><span class="sxs-lookup"><span data-stu-id="e71b3-184">Components that you install on the cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="e71b3-185">O HDInsight usa o Armazenamento de Blobs do Azure ou o Azure Data Lake Store como o repositório padrão.</span><span class="sxs-lookup"><span data-stu-id="e71b3-185">HDInsight uses either Azure Storage or Data Lake Store as the default storage.</span></span> <span data-ttu-id="e71b3-186">Ambos fornecem um sistema de arquivos compatível com HDFS que faz os dados persistirem mesmo que o cluster seja excluído.</span><span class="sxs-lookup"><span data-stu-id="e71b3-186">Both provide an HDFS compatible file system that persists data even if the cluster is deleted.</span></span> <span data-ttu-id="e71b3-187">Talvez você precise configurar os componentes instalados para usar o WASB ou ADL em vez de HDFS.</span><span class="sxs-lookup"><span data-stu-id="e71b3-187">You may need to configure components you install to use WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="e71b3-188">Para a maioria das operações, você não precisa especificar o sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="e71b3-188">For most operations, you do not need to specify the file system.</span></span> <span data-ttu-id="e71b3-189">Por exemplo, o arquivo giraph-examples.jar é copiado do sistema de arquivos local para o armazenamento de cluster no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="e71b3-189">For example, the following copies the giraph-examples.jar file from the local file system to cluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="e71b3-190">Neste exemplo, o comando `hdfs` usa o armazenamento de cluster padrão de modo transparente.</span><span class="sxs-lookup"><span data-stu-id="e71b3-190">In this example, the `hdfs` command transparently uses the default cluster storage.</span></span> <span data-ttu-id="e71b3-191">Para algumas operações, talvez seja necessário especificar o URI.</span><span class="sxs-lookup"><span data-stu-id="e71b3-191">For some operations, you may need to specify the URI.</span></span> <span data-ttu-id="e71b3-192">Por exemplo, `adl:///example/jars` para Data Lake Store ou `wasb:///example/jars` para o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e71b3-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="e71b3-193"><a name="bPS7"></a>Gravar informações para STDOUT e STDERR</span><span class="sxs-lookup"><span data-stu-id="e71b3-193"><a name="bPS7"></a>Write information to STDOUT and STDERR</span></span>

<span data-ttu-id="e71b3-194">HDInsight registra em log a saída do script que é gravada para STDOUT e STDERR.</span><span class="sxs-lookup"><span data-stu-id="e71b3-194">HDInsight logs script output that is written to STDOUT and STDERR.</span></span> <span data-ttu-id="e71b3-195">Você pode exibir essas informações usando a interface do usuário da Web do Ambari.</span><span class="sxs-lookup"><span data-stu-id="e71b3-195">You can view this information using the Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="e71b3-196">O Ambari só estará disponível se o cluster for criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="e71b3-196">Ambari is only available if the cluster is successfully created.</span></span> <span data-ttu-id="e71b3-197">Se você usar uma ação de script durante a criação do cluster e a criação falhar, confira a seção de solução de problemas [Personalizar clusters HDInsight usando a ação de script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) para conhecer outras maneiras de acessar informações registradas em log.</span><span class="sxs-lookup"><span data-stu-id="e71b3-197">If you use a script action during cluster creation, and creation fails, see the troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="e71b3-198">A maioria dos pacotes de instalação e utilitários já grava informações para STDOUT e STDERR; no entanto, talvez você queira adicionar registro em log adicional.</span><span class="sxs-lookup"><span data-stu-id="e71b3-198">Most utilities and installation packages already write information to STDOUT and STDERR, however you may want to add additional logging.</span></span> <span data-ttu-id="e71b3-199">Para enviar texto para STDOUT, use `echo`.</span><span class="sxs-lookup"><span data-stu-id="e71b3-199">To send text to STDOUT, use `echo`.</span></span> <span data-ttu-id="e71b3-200">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e71b3-200">For example:</span></span>

```bash
echo "Getting ready to install Foo"
```

<span data-ttu-id="e71b3-201">Por padrão, `echo` envia a cadeia de caracteres para STDOUT.</span><span class="sxs-lookup"><span data-stu-id="e71b3-201">By default, `echo` sends the string to STDOUT.</span></span> <span data-ttu-id="e71b3-202">Para direcioná-lo para STDERR, adicione `>&2` antes de `echo`.</span><span class="sxs-lookup"><span data-stu-id="e71b3-202">To direct it to STDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="e71b3-203">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="e71b3-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="e71b3-204">Isso redireciona as informações gravadas em STDOUT para STDERR (2) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="e71b3-204">This redirects information written to STDOUT to STDERR (2) instead.</span></span> <span data-ttu-id="e71b3-205">Para obter mais informações sobre redirecionamento de E/S, consulte [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="e71b3-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="e71b3-206">Para saber mais sobre exibição de informações registradas em log por ações de script, confira [Personalizar clusters HDInsight usando ação de script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="e71b3-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="e71b3-207"><a name="bps8"></a> Salvar arquivos como ASCII com terminações de linha LF</span><span class="sxs-lookup"><span data-stu-id="e71b3-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="e71b3-208">Scripts de Bash devem ser armazenados com formato ASCII, com linhas terminadas em LF.</span><span class="sxs-lookup"><span data-stu-id="e71b3-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="e71b3-209">Os arquivos que são armazenados como UTF-8 ou usam CRLF como o terminação de linha podem falhar com o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="e71b3-209">Files that are stored as UTF-8, or use CRLF as the line ending may fail with the following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="e71b3-210"><a name="bps9"></a> Usar a lógica de repetição para recuperar-se de erros transitórios</span><span class="sxs-lookup"><span data-stu-id="e71b3-210"><a name="bps9"></a> Use retry logic to recover from transient errors</span></span>

<span data-ttu-id="e71b3-211">Ao baixar arquivos de instalação de pacotes usando apt-get ou outras ações que transmitem dados pela Internet, a ação pode falhar devido a erros de rede temporários.</span><span class="sxs-lookup"><span data-stu-id="e71b3-211">When downloading files, installing packages using apt-get, or other actions that transmit data over the internet, the action may fail due to transient networking errors.</span></span> <span data-ttu-id="e71b3-212">Por exemplo, o recurso remoto com o qual você está se comunicando pode estar em processo de failover para um nó de backup.</span><span class="sxs-lookup"><span data-stu-id="e71b3-212">For example, the remote resource you are communicating with may be in the process of failing over to a backup node.</span></span>

<span data-ttu-id="e71b3-213">Para tornar o script resistente a erros transitórios, você pode implementar lógica de repetição.</span><span class="sxs-lookup"><span data-stu-id="e71b3-213">To make your script resilient to transient errors, you can implement retry logic.</span></span> <span data-ttu-id="e71b3-214">A função a seguir demonstra como implementar a lógica de repetição.</span><span class="sxs-lookup"><span data-stu-id="e71b3-214">The following function demonstrates how to implement retry logic.</span></span> <span data-ttu-id="e71b3-215">Ela tenta realizar a operação novamente três vezes antes de falhar.</span><span class="sxs-lookup"><span data-stu-id="e71b3-215">It retries the operation three times before failing.</span></span>

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

<span data-ttu-id="e71b3-216">Os exemplos a seguir demonstram como usar essa função.</span><span class="sxs-lookup"><span data-stu-id="e71b3-216">The following examples demonstrate how to use this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="e71b3-217"><a name="helpermethods"></a>Métodos auxiliares para scripts personalizados</span><span class="sxs-lookup"><span data-stu-id="e71b3-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="e71b3-218">Os métodos auxiliares da Ação de Script são utilitários que podem ser usados durante a gravação de scripts personalizados.</span><span class="sxs-lookup"><span data-stu-id="e71b3-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="e71b3-219">Esses métodos estão contidos no script [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh).</span><span class="sxs-lookup"><span data-stu-id="e71b3-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="e71b3-220">Use o seguinte para baixá-los e usá-los como parte do script:</span><span class="sxs-lookup"><span data-stu-id="e71b3-220">Use the following to download and use them as part of your script:</span></span>

```bash
# Import the helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="e71b3-221">Os auxiliares a seguir, disponíveis para uso em seu script:</span><span class="sxs-lookup"><span data-stu-id="e71b3-221">The following helpers available for use in your script:</span></span>

| <span data-ttu-id="e71b3-222">Uso do auxiliar</span><span class="sxs-lookup"><span data-stu-id="e71b3-222">Helper usage</span></span> | <span data-ttu-id="e71b3-223">Descrição</span><span class="sxs-lookup"><span data-stu-id="e71b3-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="e71b3-224">Baixa um arquivo da URI de origem para o caminho de arquivo especificado.</span><span class="sxs-lookup"><span data-stu-id="e71b3-224">Downloads a file from the source URI to the specified file path.</span></span> <span data-ttu-id="e71b3-225">Por padrão, ele não substitui um arquivo existente.</span><span class="sxs-lookup"><span data-stu-id="e71b3-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="e71b3-226">Extrai um arquivo tar (usando `-xf`) para o diretório de destino.</span><span class="sxs-lookup"><span data-stu-id="e71b3-226">Extracts a tar file (using `-xf`) to the destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="e71b3-227">Se executado em um nó de cabeçalho do cluster, retorna 1. Caso contrário, 0.</span><span class="sxs-lookup"><span data-stu-id="e71b3-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="e71b3-228">Se o nó atual é um nó de dados (de trabalho), retorna 1; caso contrário, 0.</span><span class="sxs-lookup"><span data-stu-id="e71b3-228">If the current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="e71b3-229">Se o nó atual é o primeiro nó de dados (de trabalho, chamado workernode0), retorna 1; caso contrário, retorna 0.</span><span class="sxs-lookup"><span data-stu-id="e71b3-229">If the current node is the first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="e71b3-230">Retorna o nome de domínio totalmente qualificado dos nós de cabeçalho no cluster.</span><span class="sxs-lookup"><span data-stu-id="e71b3-230">Return the fully qualified domain name of the headnodes in the cluster.</span></span> <span data-ttu-id="e71b3-231">Os nomes são delimitados por vírgula.</span><span class="sxs-lookup"><span data-stu-id="e71b3-231">Names are comma delimited.</span></span> <span data-ttu-id="e71b3-232">Uma cadeia de caracteres vazia retorna em caso de erro.</span><span class="sxs-lookup"><span data-stu-id="e71b3-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="e71b3-233">Obtém o nome de domínio totalmente qualificado do nó de cabeçalho primário.</span><span class="sxs-lookup"><span data-stu-id="e71b3-233">Gets the fully qualified domain name of the primary headnode.</span></span> <span data-ttu-id="e71b3-234">Uma cadeia de caracteres vazia retorna em caso de erro.</span><span class="sxs-lookup"><span data-stu-id="e71b3-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="e71b3-235">Obtém o nome de domínio totalmente qualificado do nó de cabeçalho secundário.</span><span class="sxs-lookup"><span data-stu-id="e71b3-235">Gets the fully qualified domain name of the secondary headnode.</span></span> <span data-ttu-id="e71b3-236">Uma cadeia de caracteres vazia retorna em caso de erro.</span><span class="sxs-lookup"><span data-stu-id="e71b3-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="e71b3-237">Obtém o sufixo numérico do nó de cabeçalho primário.</span><span class="sxs-lookup"><span data-stu-id="e71b3-237">Gets the numeric suffix of the primary headnode.</span></span> <span data-ttu-id="e71b3-238">Uma cadeia de caracteres vazia retorna em caso de erro.</span><span class="sxs-lookup"><span data-stu-id="e71b3-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="e71b3-239">Obtém o sufixo numérico do nó de cabeçalho secundário.</span><span class="sxs-lookup"><span data-stu-id="e71b3-239">Gets the numeric suffix of the secondary headnode.</span></span> <span data-ttu-id="e71b3-240">Uma cadeia de caracteres vazia retorna em caso de erro.</span><span class="sxs-lookup"><span data-stu-id="e71b3-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="e71b3-241"><a name="commonusage"></a>Padrões comuns de uso</span><span class="sxs-lookup"><span data-stu-id="e71b3-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="e71b3-242">Esta seção fornece orientações sobre como implementar alguns dos padrões comuns de uso que você pode encontrar ao escrever seu próprio script personalizado.</span><span class="sxs-lookup"><span data-stu-id="e71b3-242">This section provides guidance on implementing some of the common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-to-a-script"></a><span data-ttu-id="e71b3-243">Passando parâmetros para um script</span><span class="sxs-lookup"><span data-stu-id="e71b3-243">Passing parameters to a script</span></span>

<span data-ttu-id="e71b3-244">Em alguns casos, seu script pode exigir parâmetros.</span><span class="sxs-lookup"><span data-stu-id="e71b3-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="e71b3-245">Por exemplo, a senha do administrador para o cluster talvez seja necessária ao usar a API REST do Ambari.</span><span class="sxs-lookup"><span data-stu-id="e71b3-245">For example, you may need the admin password for the cluster when using the Ambari REST API.</span></span>

<span data-ttu-id="e71b3-246">Os parâmetros passados para o script são conhecidos como *parâmetros posicionais* e são atribuídos a `$1` para o primeiro parâmetro, `$2` para o segundo e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="e71b3-246">Parameters passed to the script are known as *positional parameters*, and are assigned to `$1` for the first parameter, `$2` for the second, and so-on.</span></span> <span data-ttu-id="e71b3-247">`$0` contém o nome do próprio script.</span><span class="sxs-lookup"><span data-stu-id="e71b3-247">`$0` contains the name of the script itself.</span></span>

<span data-ttu-id="e71b3-248">Valores passados para o script como parâmetros devem ser inseridos entre aspas simples (').</span><span class="sxs-lookup"><span data-stu-id="e71b3-248">Values passed to the script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="e71b3-249">Isso garante que o valor passado seja tratado como um literal.</span><span class="sxs-lookup"><span data-stu-id="e71b3-249">Doing so ensures that the passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="e71b3-250">Configurando variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="e71b3-250">Setting environment variables</span></span>

<span data-ttu-id="e71b3-251">Definir uma variável de ambiente é uma ação realizada pela seguinte instrução:</span><span class="sxs-lookup"><span data-stu-id="e71b3-251">Setting an environment variable is performed by the following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="e71b3-252">Em que VARIABLENAME é o nome da variável.</span><span class="sxs-lookup"><span data-stu-id="e71b3-252">Where VARIABLENAME is the name of the variable.</span></span> <span data-ttu-id="e71b3-253">Para acessar a variável, use `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="e71b3-253">To access the variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="e71b3-254">Por exemplo, para atribuir um valor fornecido por um parâmetro posicional como uma variável de ambiente denominada PASSWORD, use a seguinte instrução:</span><span class="sxs-lookup"><span data-stu-id="e71b3-254">For example, to assign a value provided by a positional parameter as an environment variable named PASSWORD, you would use the following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="e71b3-255">O acesso subsequente às informações poderia, então, usar `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="e71b3-255">Subsequent access to the information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="e71b3-256">Variáveis de ambiente definidas no script existem somente dentro do escopo do script.</span><span class="sxs-lookup"><span data-stu-id="e71b3-256">Environment variables set within the script only exist within the scope of the script.</span></span> <span data-ttu-id="e71b3-257">Em alguns casos, talvez seja necessário adicionar variáveis de ambiente de todo o sistema que persistirão após a conclusão do script.</span><span class="sxs-lookup"><span data-stu-id="e71b3-257">In some cases, you may need to add system-wide environment variables that will persist after the script has finished.</span></span> <span data-ttu-id="e71b3-258">Para adicionar variáveis de ambiente de todo o sistema, adicione a variável a `/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="e71b3-258">To add system-wide environment variables, add the variable to `/etc/environment`.</span></span> <span data-ttu-id="e71b3-259">Por exemplo, a instrução a seguir retornará `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="e71b3-259">For example, the following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-to-locations-where-the-custom-scripts-are-stored"></a><span data-ttu-id="e71b3-260">Acesso a locais onde estão armazenados os scripts personalizados</span><span class="sxs-lookup"><span data-stu-id="e71b3-260">Access to locations where the custom scripts are stored</span></span>

<span data-ttu-id="e71b3-261">Scripts usados para personalizar um cluster devem ser armazenados em um dos seguintes locais:</span><span class="sxs-lookup"><span data-stu-id="e71b3-261">Scripts used to customize a cluster needs to be stored in one of the following locations:</span></span>

* <span data-ttu-id="e71b3-262">Uma __conta de armazenamento do Azure__ associada ao cluster.</span><span class="sxs-lookup"><span data-stu-id="e71b3-262">An __Azure Storage account__ that is associated with the cluster.</span></span>

* <span data-ttu-id="e71b3-263">Um __conta de armazenamento adicional__ associada ao cluster.</span><span class="sxs-lookup"><span data-stu-id="e71b3-263">An __additional storage account__ associated with the cluster.</span></span>

* <span data-ttu-id="e71b3-264">Um URI __que pode ser lido publicamente__.</span><span class="sxs-lookup"><span data-stu-id="e71b3-264">A __publicly readable URI__.</span></span> <span data-ttu-id="e71b3-265">Por exemplo, uma URL para dados armazenados no OneDrive, Dropbox ou outro serviço de hospedagem de arquivos.</span><span class="sxs-lookup"><span data-stu-id="e71b3-265">For example, a URL to data stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="e71b3-266">Uma __conta do Azure Data Lake Store__ que está associada com o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e71b3-266">An __Azure Data Lake Store account__ that is associated with the HDInsight cluster.</span></span> <span data-ttu-id="e71b3-267">Para obter mais informações sobre o uso do Azure Data Lake Store com o HDInsight, veja [Criar um cluster HDInsight com o Repositório Data Lake](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e71b3-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="e71b3-268">A entidade de serviço que HDInsight usa para acessar o Data Lake Store deve ter acesso de leitura para o script.</span><span class="sxs-lookup"><span data-stu-id="e71b3-268">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

<span data-ttu-id="e71b3-269">Recursos usados pelo script também devem estar publicamente disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e71b3-269">Resources used by the script must also be publicly available.</span></span>

<span data-ttu-id="e71b3-270">Armazenar os arquivos em uma conta de Armazenamento do Azure ou Azure Data Lake Store fornece acesso rápido, pois ambos estão dentro da rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="e71b3-270">Storing the files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within the Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="e71b3-271">O formato de URI usado para referenciar o script difere dependendo do serviço que está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="e71b3-271">The URI format used to reference the script differs depending on the service being used.</span></span> <span data-ttu-id="e71b3-272">Para contas de armazenamento associadas ao cluster HDInsight, use `wasb://` ou `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="e71b3-272">For storage accounts associated with the HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="e71b3-273">Para URIs lidas publicamente, use `http://` ou `https://`.</span><span class="sxs-lookup"><span data-stu-id="e71b3-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="e71b3-274">Para Data Lake Store, use `adl://`.</span><span class="sxs-lookup"><span data-stu-id="e71b3-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-the-operating-system-version"></a><span data-ttu-id="e71b3-275">Verificando a versão do sistema operacional</span><span class="sxs-lookup"><span data-stu-id="e71b3-275">Checking the operating system version</span></span>

<span data-ttu-id="e71b3-276">Versões diferentes do HDInsight contam com versões específicas do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e71b3-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="e71b3-277">Pode haver diferenças entre as versões de sistema operacional, que você deve verificar em seu script.</span><span class="sxs-lookup"><span data-stu-id="e71b3-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="e71b3-278">Por exemplo, talvez seja necessário instalar um binário que esteja vinculado à versão do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e71b3-278">For example, you may need to install a binary that is tied to the version of Ubuntu.</span></span>

<span data-ttu-id="e71b3-279">Para verificar a versão do sistema operacional, use `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="e71b3-279">To check the OS version, use `lsb_release`.</span></span> <span data-ttu-id="e71b3-280">Por exemplo, o script de exemplo a seguir demonstra como fazer referência a um arquivo tar específico dependendo da versão do SO:</span><span class="sxs-lookup"><span data-stu-id="e71b3-280">For example, the following script demonstrates how to reference a specific tar file depending on the OS version:</span></span>

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

## <span data-ttu-id="e71b3-281"><a name="deployScript"></a>Lista de verificação para implantação de uma ação de script</span><span class="sxs-lookup"><span data-stu-id="e71b3-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="e71b3-282">Aqui estão as etapas que utilizamos ao se preparar para implantar esses scripts:</span><span class="sxs-lookup"><span data-stu-id="e71b3-282">Here are the steps we took when preparing to deploy these scripts:</span></span>

* <span data-ttu-id="e71b3-283">Coloque os arquivos que contêm os scripts personalizados em um local que seja acessível pelos nós de cluster durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="e71b3-283">Put the files that contain the custom scripts in a place that is accessible by the cluster nodes during deployment.</span></span> <span data-ttu-id="e71b3-284">Por exemplo, o armazenamento padrão para o cluster.</span><span class="sxs-lookup"><span data-stu-id="e71b3-284">For example, the default storage for the cluster.</span></span> <span data-ttu-id="e71b3-285">Arquivos também podem ser armazenados nos serviços de hospedagem legíveis publicamente.</span><span class="sxs-lookup"><span data-stu-id="e71b3-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="e71b3-286">Verifique se o script é idempotente.</span><span class="sxs-lookup"><span data-stu-id="e71b3-286">Verify that the script is impotent.</span></span> <span data-ttu-id="e71b3-287">Isso permite que o script seja executado várias vezes no mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="e71b3-287">Doing so allows the script to be executed multiple times on the same node.</span></span>
* <span data-ttu-id="e71b3-288">Use um diretório de arquivos temporário, /tmp, para manter os arquivos baixados usados pelos scripts e em seguida limpá-los, depois de os scripts terem sido executados.</span><span class="sxs-lookup"><span data-stu-id="e71b3-288">Use a temporary file directory /tmp to keep the downloaded files used by the scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="e71b3-289">Se as configurações de nível de SO ou arquivos de configuração de serviço do Hadoop forem alterados, será conveniente reiniciar os serviços do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e71b3-289">If OS-level settings or Hadoop service configuration files are changed, you may want to restart HDInsight services.</span></span>

## <span data-ttu-id="e71b3-290"><a name="runScriptAction"></a>Como executar uma Ação de Script</span><span class="sxs-lookup"><span data-stu-id="e71b3-290"><a name="runScriptAction"></a>How to run a script action</span></span>

<span data-ttu-id="e71b3-291">Você pode usar ações de script para personalizar os clusters HDInsight usando os seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="e71b3-291">You can use script actions to customize HDInsight clusters using the following methods:</span></span>

* <span data-ttu-id="e71b3-292">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e71b3-292">Azure portal</span></span>
* <span data-ttu-id="e71b3-293">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="e71b3-293">Azure PowerShell</span></span>
* <span data-ttu-id="e71b3-294">Modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="e71b3-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="e71b3-295">O SDK .NET do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e71b3-295">The HDInsight .NET SDK.</span></span>

<span data-ttu-id="e71b3-296">Para obter mais informações sobre como usar cada método, consulte [Como usar a ação de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e71b3-296">For more information on using each method, see [How to use script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="e71b3-297"><a name="sampleScripts"></a>Exemplos de script personalizado</span><span class="sxs-lookup"><span data-stu-id="e71b3-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="e71b3-298">A Microsoft fornece scripts de exemplo para instalar componentes em um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e71b3-298">Microsoft provides sample scripts to install components on an HDInsight cluster.</span></span> <span data-ttu-id="e71b3-299">Consulte os links a seguir para obter mais ações de script de exemplo.</span><span class="sxs-lookup"><span data-stu-id="e71b3-299">See the following links for more example script actions.</span></span>

* [<span data-ttu-id="e71b3-300">Instalar e usar o Hue em clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="e71b3-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="e71b3-301">Instalar e usar o Solr em clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="e71b3-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="e71b3-302">Instalar e usar o Giraph em clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="e71b3-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="e71b3-303">Instalar ou atualizar o Mono em clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="e71b3-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="e71b3-304">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="e71b3-304">Troubleshooting</span></span>

<span data-ttu-id="e71b3-305">Estes são erros que você pode encontrar ao usar scripts desenvolvidos por você:</span><span class="sxs-lookup"><span data-stu-id="e71b3-305">The following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="e71b3-306">**Erro**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="e71b3-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="e71b3-307">Às vezes, seguido por `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="e71b3-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="e71b3-308">*Causa*: este erro é gerado quando as linhas em um script terminam com CRLF.</span><span class="sxs-lookup"><span data-stu-id="e71b3-308">*Cause*: This error is caused when the lines in a script end with CRLF.</span></span> <span data-ttu-id="e71b3-309">Os sistemas UNIX esperam apenas LF como terminação da linha.</span><span class="sxs-lookup"><span data-stu-id="e71b3-309">Unix systems expect only LF as the line ending.</span></span>

<span data-ttu-id="e71b3-310">Esse problema ocorre geralmente quando o script é criado em um ambiente Windows, já que CRLF é uma terminação de linha comum para muitos editores de texto no Windows.</span><span class="sxs-lookup"><span data-stu-id="e71b3-310">This problem most often occurs when the script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="e71b3-311">*Solução*: se for uma opção em seu editor de texto, selecione o formato Unix ou LF para terminação de linha.</span><span class="sxs-lookup"><span data-stu-id="e71b3-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for the line ending.</span></span> <span data-ttu-id="e71b3-312">Você também pode usar os seguintes comandos em um sistema Unix para alterar o CRLF para um LF:</span><span class="sxs-lookup"><span data-stu-id="e71b3-312">You may also use the following commands on a Unix system to change the CRLF to an LF:</span></span>

> [!NOTE]
> <span data-ttu-id="e71b3-313">Os comandos a seguir são a grosso modo equivalentes, no sentido que ambos devem alterar as terminações de linha CRLF para LF.</span><span class="sxs-lookup"><span data-stu-id="e71b3-313">The following commands are roughly equivalent in that they should change the CRLF line endings to LF.</span></span> <span data-ttu-id="e71b3-314">Selecione um deles com base nos utilitários disponíveis no sistema.</span><span class="sxs-lookup"><span data-stu-id="e71b3-314">Select one based on the utilities available on your system.</span></span>

| <span data-ttu-id="e71b3-315">Command</span><span class="sxs-lookup"><span data-stu-id="e71b3-315">Command</span></span> | <span data-ttu-id="e71b3-316">Observações</span><span class="sxs-lookup"><span data-stu-id="e71b3-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="e71b3-317">O backup do arquivo original é feito com uma extensão .BAK</span><span class="sxs-lookup"><span data-stu-id="e71b3-317">The original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="e71b3-318">OUTFILE contém uma versão apenas com terminações LF</span><span class="sxs-lookup"><span data-stu-id="e71b3-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="e71b3-319">Modifica o arquivo diretamente</span><span class="sxs-lookup"><span data-stu-id="e71b3-319">Modifies the file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="e71b3-320">OUTFILE contém uma versão apenas com terminações LF.</span><span class="sxs-lookup"><span data-stu-id="e71b3-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="e71b3-321">**Erro**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="e71b3-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="e71b3-322">*Causa*: este erro ocorre quando o script foi salvo como UTF-8 com uma BOM (Marca de Ordem de Byte).</span><span class="sxs-lookup"><span data-stu-id="e71b3-322">*Cause*: This error occurs when the script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="e71b3-323">*Solução*: salve o arquivo como ASCII ou UTF-8, sem nenhuma BOM.</span><span class="sxs-lookup"><span data-stu-id="e71b3-323">*Resolution*: Save the file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="e71b3-324">Você também pode usar o seguinte comando em um sistema Linux ou Unix para criar um arquivo sem a BOM:</span><span class="sxs-lookup"><span data-stu-id="e71b3-324">You may also use the following command on a Linux or Unix system to create a file without the BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="e71b3-325">Substitua `INFILE` com o arquivo que contém a BOM.</span><span class="sxs-lookup"><span data-stu-id="e71b3-325">Replace `INFILE` with the file containing the BOM.</span></span> <span data-ttu-id="e71b3-326">`OUTFILE` deve ser um novo nome de arquivo contendo o script sem a BOM.</span><span class="sxs-lookup"><span data-stu-id="e71b3-326">`OUTFILE` should be a new file name, which contains the script without the BOM.</span></span>

## <span data-ttu-id="e71b3-327"><a name="seeAlso"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e71b3-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="e71b3-328">Saiba como [Personalizar os clusters HDInsight usando a ação de script](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="e71b3-328">Learn how to [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="e71b3-329">Use a [referência do SDK do .NET do HDInsight](https://msdn.microsoft.com/library/mt271028.aspx) para saber mais sobre a criação de aplicativos .NET que gerenciam o HDInsight</span><span class="sxs-lookup"><span data-stu-id="e71b3-329">Use the [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) to learn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="e71b3-330">Use a [API REST do HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) para aprender a usar o REST para executar ações de gerenciamento em clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e71b3-330">Use the [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) to learn how to use REST to perform management actions on HDInsight clusters.</span></span>
