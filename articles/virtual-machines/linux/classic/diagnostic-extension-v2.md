---
title: "aaaMonitoring uma VM do Linux com uma extensão de VM | Microsoft Docs"
description: "Saiba como toouse Olá extensão de diagnóstico do Linux toomonitor Olá dados de desempenho e diagnóstico de uma VM do Linux no Azure."
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a><span data-ttu-id="07268-103">Use Olá extensão de diagnóstico do Linux toomonitor Olá dados de desempenho e diagnóstico de uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="07268-103">Use hello Linux Diagnostic Extension toomonitor hello performance and diagnostic data of a Linux VM</span></span>

<span data-ttu-id="07268-104">Este documento descreve a versão 2.3 Olá extensão de diagnóstico do Linux.</span><span class="sxs-lookup"><span data-stu-id="07268-104">This document describes version 2.3 of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07268-105">Esta versão foi preterida e sua publicação pode ser cancelada a qualquer momento após 30 de junho de 2018.</span><span class="sxs-lookup"><span data-stu-id="07268-105">This version is deprecated, and it may be unpublished any time after June 30, 2018.</span></span> <span data-ttu-id="07268-106">Ela foi substituída pela versão 3.0.</span><span class="sxs-lookup"><span data-stu-id="07268-106">It has been replaced by version 3.0.</span></span> <span data-ttu-id="07268-107">Para obter mais informações, consulte Olá [documentação para a versão 3.0 do hello extensão de diagnóstico do Linux](../diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="07268-107">For more information, see hello [documentation for version 3.0 of hello Linux Diagnostic Extension](../diagnostic-extension.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="07268-108">Introdução</span><span class="sxs-lookup"><span data-stu-id="07268-108">Introduction</span></span>

<span data-ttu-id="07268-109">(**Observação**: Olá extensão de diagnóstico do Linux é originado de abertura em [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) onde informações mais recentes de saudação na extensão de saudação são publicadas pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="07268-109">(**Note**: hello Linux Diagnostic Extension is open-sourced on [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) where hello most current information on hello extension is first published.</span></span> <span data-ttu-id="07268-110">Talvez você queira Olá toocheck [página GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) primeiro.)</span><span class="sxs-lookup"><span data-stu-id="07268-110">You might want toocheck hello [GitHub page](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) first.)</span></span>

<span data-ttu-id="07268-111">Olá extensão de diagnóstico do Linux ajuda uma saudação do usuário monitor VMs do Linux em execução no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="07268-111">hello Linux Diagnostic Extension helps a user monitor hello Linux VMs that are running on Microsoft Azure.</span></span> <span data-ttu-id="07268-112">Ele tem Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="07268-112">It has hello following capabilities:</span></span>

* <span data-ttu-id="07268-113">Coleta e carrega as informações de desempenho do sistema de saudação da tabela de armazenamento do usuário do toohello Olá VM do Linux, incluindo informações de diagnóstico e de syslog.</span><span class="sxs-lookup"><span data-stu-id="07268-113">Collects and uploads hello system performance information from hello Linux VM toohello user's storage table, including diagnostic and syslog information.</span></span>
* <span data-ttu-id="07268-114">Permite que os usuários toocustomize Olá as métricas de dados que serão coletadas e carregadas.</span><span class="sxs-lookup"><span data-stu-id="07268-114">Enables users toocustomize hello data metrics that will be collected and uploaded.</span></span>
* <span data-ttu-id="07268-115">Permite que os usuários tooupload log especificado arquivos tooa armazenamento designadas tabela.</span><span class="sxs-lookup"><span data-stu-id="07268-115">Enables users tooupload specified log files tooa designated storage table.</span></span>

<span data-ttu-id="07268-116">Na versão atual de saudação 2.3, dados de saudação incluem:</span><span class="sxs-lookup"><span data-stu-id="07268-116">In hello current version 2.3, hello data includes:</span></span>

* <span data-ttu-id="07268-117">Todos os logs Rsyslog do Linux, incluindo logs de sistema, de segurança e de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="07268-117">All Linux Rsyslog logs, including system, security, and application logs.</span></span>
* <span data-ttu-id="07268-118">Todos os dados do sistema que são especificados em [site de soluções de plataforma cruzada do System Center Olá](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="07268-118">All system data that's specified on [hello System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
* <span data-ttu-id="07268-119">Arquivos de log especificados pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="07268-119">User-specified log files.</span></span>

<span data-ttu-id="07268-120">Essa extensão funciona com hello clássico e modelos de implantação do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="07268-120">This extension works with both hello classic and Resource Manager deployment models.</span></span>

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a><span data-ttu-id="07268-121">Versão atual da extensão hello e substituição de versões antigas</span><span class="sxs-lookup"><span data-stu-id="07268-121">Current version of hello extension and deprecation of old versions</span></span>

<span data-ttu-id="07268-122">Olá a versão mais recente da extensão de saudação é **2.3**, e **todas as versões antigas (2.0, 2.1 e 2.2) serão preteridas e não publicadas pela extremidade deste ano (2017)**.</span><span class="sxs-lookup"><span data-stu-id="07268-122">hello latest version of hello extension is **2.3**, and **any old versions (2.0, 2.1, and 2.2) will be deprecated and unpublished by end of this year (2017)**.</span></span> <span data-ttu-id="07268-123">Se você instalou Olá extensão de diagnóstico do Linux com a atualização automática de versão secundária desabilitada, é altamente recomendável que você desinstale extensão hello e reinstalá-lo com a atualização de versão secundária automático habilitada.</span><span class="sxs-lookup"><span data-stu-id="07268-123">If you installed hello Linux Diagnostic extension with automatic minor version upgrade disabled, it's strongly recommended that you uninstall hello extension and reinstall it with automatic minor version upgrade enabled.</span></span> <span data-ttu-id="07268-124">Em VMs (ASM) clássicas, você pode obter isso especificando '2.*' como versão de hello, se você estiver instalando uma extensão de saudação por meio do Azure XPLAT CLI ou o Powershell.</span><span class="sxs-lookup"><span data-stu-id="07268-124">On classic (ASM) VMs, you can achieve this by specifying '2.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span> <span data-ttu-id="07268-125">Em VMs do ARM, você pode obter isso, incluindo ' "autoUpgradeMinorVersion": true' no modelo de implantação de VM hello.</span><span class="sxs-lookup"><span data-stu-id="07268-125">On ARM VMs, you can achieve this by including '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span> <span data-ttu-id="07268-126">Além disso, qualquer nova instalação da extensão de saudação deve ter versão secundária do hello automaticamente a opção de atualização.</span><span class="sxs-lookup"><span data-stu-id="07268-126">Also, any new installation of hello extension should have hello auto minor version upgrade option turned on.</span></span>

## <a name="enable-hello-extension"></a><span data-ttu-id="07268-127">Habilitar a extensão de saudação</span><span class="sxs-lookup"><span data-stu-id="07268-127">Enable hello extension</span></span>

<span data-ttu-id="07268-128">Você pode habilitar esta extensão usando Olá [portal do Azure](https://portal.azure.com/#), Azure PowerShell ou scripts de CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="07268-128">You can enable this extension by using hello [Azure portal](https://portal.azure.com/#), Azure PowerShell, or Azure CLI scripts.</span></span>

<span data-ttu-id="07268-129">tooview e configurar o sistema hello e dados de desempenho diretamente da saudação portal do Azure, siga [essas etapas em hello Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span><span class="sxs-lookup"><span data-stu-id="07268-129">tooview and configure hello system and performance data directly from hello Azure portal, follow [these steps on hello Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span></span>

<span data-ttu-id="07268-130">Este artigo se concentra em como tooenable e configurar a extensão de saudação usando comandos de CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="07268-130">This article focuses on how tooenable and configure hello extension by using Azure CLI commands.</span></span> <span data-ttu-id="07268-131">Isso permite tooread e exibir dados de saudação diretamente da tabela de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="07268-131">This allows you tooread and view hello data directly from hello storage table.</span></span>

<span data-ttu-id="07268-132">Observe que os métodos de configuração de saudação que são descritos aqui não funcionarão para Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="07268-132">Note that hello configuration methods that are described here won't work for hello Azure portal.</span></span> <span data-ttu-id="07268-133">tooview e configurar dados de desempenho do sistema e de saudação diretamente da saudação portal do Azure, Olá extensão deve ser habilitada por meio do portal hello.</span><span class="sxs-lookup"><span data-stu-id="07268-133">tooview and configure hello system and performance data directly from hello Azure portal, hello extension must be enabled through hello portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07268-134">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="07268-134">Prerequisites</span></span>

* <span data-ttu-id="07268-135">**Agente Linux do Azure versão 2.0.6 ou posterior**.</span><span class="sxs-lookup"><span data-stu-id="07268-135">**Azure Linux Agent version 2.0.6 or later**.</span></span>

  <span data-ttu-id="07268-136">Observe que a maioria das imagens de galeria da VM Linux do Azure inclui a versão 2.0.6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="07268-136">Note that most Azure VM Linux gallery images include version 2.0.6 or later.</span></span> <span data-ttu-id="07268-137">Você pode executar **WAAgent-versão** tooconfirm qual versão está instalada em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="07268-137">You can run **WAAgent -version** tooconfirm which version is installed on hello VM.</span></span> <span data-ttu-id="07268-138">Se Olá VM estiver executando uma versão anterior ao 2.0.6, você pode seguir [estas instruções no GitHub](https://github.com/Azure/WALinuxAgent "instruções") tooupdate-lo.</span><span class="sxs-lookup"><span data-stu-id="07268-138">If hello VM is running a version that's earlier than 2.0.6, you can follow [these instructions on GitHub](https://github.com/Azure/WALinuxAgent "instructions") tooupdate it.</span></span>
* <span data-ttu-id="07268-139">**CLI do Azure**.</span><span class="sxs-lookup"><span data-stu-id="07268-139">**Azure CLI**.</span></span> <span data-ttu-id="07268-140">Execute [neste guia para instalar a CLI](../../../cli-install-nodejs.md) tooset o ambiente de CLI do Azure Olá em seu computador.</span><span class="sxs-lookup"><span data-stu-id="07268-140">Follow [this guidance for installing CLI](../../../cli-install-nodejs.md) tooset up hello Azure CLI environment on your machine.</span></span> <span data-ttu-id="07268-141">Depois de instalar a CLI do Azure, você pode usar o hello **azure** comando de sua interface de linha de comando (Bash Terminal comandos ou prompt de comando) tooaccess Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="07268-141">After Azure CLI is installed, you can use hello **azure** command from your command-line interface (Bash, Terminal, or command prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="07268-142">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="07268-142">For example:</span></span>

  * <span data-ttu-id="07268-143">Execute **azure vm extension set --help** para obter informações de ajuda detalhadas.</span><span class="sxs-lookup"><span data-stu-id="07268-143">Run **azure vm extension set --help** for detailed help information.</span></span>
  * <span data-ttu-id="07268-144">Executar **logon do azure** toosign em tooAzure.</span><span class="sxs-lookup"><span data-stu-id="07268-144">Run **azure login** toosign in tooAzure.</span></span>
  * <span data-ttu-id="07268-145">Executar **vm do azure lista** toolist todos Olá máquinas virtuais que você tem no Azure.</span><span class="sxs-lookup"><span data-stu-id="07268-145">Run **azure vm list** toolist all hello virtual machines that you have on Azure.</span></span>
* <span data-ttu-id="07268-146">Um armazenamento conta toostore Olá de dados.</span><span class="sxs-lookup"><span data-stu-id="07268-146">A storage account toostore hello data.</span></span> <span data-ttu-id="07268-147">Você precisará de um nome de conta de armazenamento que foi criado anteriormente e um armazenamento de tooyour acesso tooupload chave Olá dados.</span><span class="sxs-lookup"><span data-stu-id="07268-147">You will need a storage account name that was created previously and an access key tooupload hello data tooyour storage.</span></span>

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a><span data-ttu-id="07268-148">Use Olá CLI do Azure comando tooenable Olá extensão de diagnóstico do Linux</span><span class="sxs-lookup"><span data-stu-id="07268-148">Use hello Azure CLI command tooenable hello Linux Diagnostic Extension</span></span>

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a><span data-ttu-id="07268-149">Cenário 1.</span><span class="sxs-lookup"><span data-stu-id="07268-149">Scenario 1.</span></span> <span data-ttu-id="07268-150">Habilitar a extensão de saudação com conjunto de dados padrão de saudação</span><span class="sxs-lookup"><span data-stu-id="07268-150">Enable hello extension with hello default data set</span></span>

<span data-ttu-id="07268-151">Na versão 2.3 ou posterior, os dados de padrão de saudação que serão coletados incluem:</span><span class="sxs-lookup"><span data-stu-id="07268-151">In version 2.3 or later, hello default data that will be collected includes:</span></span>

* <span data-ttu-id="07268-152">Todas as informações de Rsyslog (incluindo os logs de sistema, segurança e aplicativo).</span><span class="sxs-lookup"><span data-stu-id="07268-152">All Rsyslog information (including system, security, and application logs).</span></span>  
* <span data-ttu-id="07268-153">Um conjunto principal de dados base do sistema.</span><span class="sxs-lookup"><span data-stu-id="07268-153">A core set of basis system data.</span></span> <span data-ttu-id="07268-154">Observe que Olá conjunto de dados completo é descrito na Olá [site soluções de plataforma cruzada do System Center](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="07268-154">Note that hello full data set is described on hello [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
  <span data-ttu-id="07268-155">Se você quiser tooenable dados extras, continue com as etapas de saudação em cenários de 2 e 3.</span><span class="sxs-lookup"><span data-stu-id="07268-155">If you want tooenable extra data, continue with hello steps in Scenarios 2 and 3.</span></span>

<span data-ttu-id="07268-156">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="07268-156">Step 1.</span></span> <span data-ttu-id="07268-157">Crie um arquivo chamado Privateconfig com hello seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="07268-157">Create a file named PrivateConfig.json with hello following content:</span></span>

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

<span data-ttu-id="07268-158">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="07268-158">Step 2.</span></span> <span data-ttu-id="07268-159">Execute **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="07268-159">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span></span>

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a><span data-ttu-id="07268-160">Cenário 2:</span><span class="sxs-lookup"><span data-stu-id="07268-160">Scenario 2.</span></span> <span data-ttu-id="07268-161">Personalizar as métricas de saudação do monitor de desempenho</span><span class="sxs-lookup"><span data-stu-id="07268-161">Customize hello performance monitor metrics</span></span>

<span data-ttu-id="07268-162">Esta seção descreve como toocustomize Olá desempenho e a tabela de dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="07268-162">This section describes how toocustomize hello performance and diagnostic data table.</span></span>

<span data-ttu-id="07268-163">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="07268-163">Step 1.</span></span> <span data-ttu-id="07268-164">Crie um arquivo chamado Privateconfig com conteúdo Olá descrito no cenário 1.</span><span class="sxs-lookup"><span data-stu-id="07268-164">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="07268-165">Além disso, crie um arquivo chamado PublicConfig.json.</span><span class="sxs-lookup"><span data-stu-id="07268-165">Also create a file named PublicConfig.json.</span></span> <span data-ttu-id="07268-166">Especifica dados Olá específicos a serem toocollect.</span><span class="sxs-lookup"><span data-stu-id="07268-166">Specify hello particular data you want toocollect.</span></span>

<span data-ttu-id="07268-167">Para todos os provedores e variáveis, consulte Olá [site soluções de plataforma cruzada do System Center](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="07268-167">For all supported providers and variables, reference hello [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span> <span data-ttu-id="07268-168">Você pode ter várias consultas e armazená-los em várias tabelas, acrescentando mais script toohello de consultas.</span><span class="sxs-lookup"><span data-stu-id="07268-168">You can have multiple queries and store them in multiple tables by appending more queries toohello script.</span></span>

<span data-ttu-id="07268-169">Por padrão, a saudação Rsyslog dados sempre é coletada.</span><span class="sxs-lookup"><span data-stu-id="07268-169">By default, hello Rsyslog data is always collected.</span></span>

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


<span data-ttu-id="07268-170">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="07268-170">Step 2.</span></span> <span data-ttu-id="07268-171">Execute **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="07268-171">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

### <a name="scenario-3-upload-your-own-log-files"></a><span data-ttu-id="07268-172">Cenário 3:</span><span class="sxs-lookup"><span data-stu-id="07268-172">Scenario 3.</span></span> <span data-ttu-id="07268-173">Carregar os próprios arquivos de log</span><span class="sxs-lookup"><span data-stu-id="07268-173">Upload your own log files</span></span>

<span data-ttu-id="07268-174">Esta seção descreve como os arquivos de log específico toocollect e carregamento tooyour conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="07268-174">This section describes how toocollect and upload specific log files tooyour storage account.</span></span> <span data-ttu-id="07268-175">Você precisará toospecify ambos os Olá caminho tooyour log arquivo e hello nome da tabela de saudação onde você deseja toostore seu log.</span><span class="sxs-lookup"><span data-stu-id="07268-175">You need toospecify both hello path tooyour log file and hello name of hello table where you want toostore your log.</span></span> <span data-ttu-id="07268-176">Você pode criar vários arquivos de log com a adição de vários arquivos/tabela entradas toohello de script.</span><span class="sxs-lookup"><span data-stu-id="07268-176">You can create multiple log files by adding multiple file/table entries toohello script.</span></span>

<span data-ttu-id="07268-177">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="07268-177">Step 1.</span></span> <span data-ttu-id="07268-178">Crie um arquivo chamado Privateconfig com conteúdo Olá descrito no cenário 1.</span><span class="sxs-lookup"><span data-stu-id="07268-178">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="07268-179">Em seguida, crie outro arquivo denominado PublicConfig.json com hello a seguir conteúdo:</span><span class="sxs-lookup"><span data-stu-id="07268-179">Then create another file named PublicConfig.json with hello following content:</span></span>

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

<span data-ttu-id="07268-180">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="07268-180">Step 2.</span></span> <span data-ttu-id="07268-181">Execute `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="07268-181">Run `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span></span>

<span data-ttu-id="07268-182">Observe que, com essa configuração no hello extensão versões anteriores too2.3, todos os logs gravados muito`/var/log/mysql.err` podem estar duplicados muito`/var/log/syslog` (ou `/var/log/messages` dependendo da distribuição de Linux Olá) também.</span><span class="sxs-lookup"><span data-stu-id="07268-182">Note that with this setting on hello extension versions prior too2.3, all logs written too`/var/log/mysql.err` might be duplicated too`/var/log/syslog` (or `/var/log/messages` depending on hello Linux distro) as well.</span></span> <span data-ttu-id="07268-183">Se você quiser tooavoid duplicidade log, você pode excluir o registro em log de `local6` recurso logs em sua configuração de rsyslog.</span><span class="sxs-lookup"><span data-stu-id="07268-183">If you'd like tooavoid this duplicate logging, you can exclude logging of `local6` facility logs in your rsyslog configuration.</span></span> <span data-ttu-id="07268-184">Ele depende da distribuição de Linux Olá, mas em um sistema Ubuntu 14.04, Olá arquivo toomodify é `/etc/rsyslog.d/50-default.conf` e você pode substituir a linha hello `*.*;auth,authpriv.none -/var/log/syslog` muito`*.*;auth,authpriv,local6.none -/var/log/syslog`.</span><span class="sxs-lookup"><span data-stu-id="07268-184">It depends on hello Linux distro, but on an Ubuntu 14.04 system, hello file toomodify is `/etc/rsyslog.d/50-default.conf` and you can replace hello line `*.*;auth,authpriv.none -/var/log/syslog` too`*.*;auth,authpriv,local6.none -/var/log/syslog`.</span></span> <span data-ttu-id="07268-185">Esse problema é corrigido na versão de hotfix mais recente saudação do 2.3 (2.3.9007), portanto, se você tiver a extensão de saudação versão 2.3, esse problema não deve ocorrer.</span><span class="sxs-lookup"><span data-stu-id="07268-185">This issue is fixed in hello latest hotfix release of 2.3 (2.3.9007), so if you have hello extension version 2.3, this issue should not happen.</span></span> <span data-ttu-id="07268-186">Se ainda existir mesmo depois de reiniciar a VM,. entre em contato conosco e ajude-na solução de problemas que a versão mais recente de hotfix Olá não é instalado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="07268-186">If it still does even after restarting your VM, please contact us and help us troubleshoot why hello latest hotfix version is not installed automatically.</span></span>

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a><span data-ttu-id="07268-187">Cenário 4:</span><span class="sxs-lookup"><span data-stu-id="07268-187">Scenario 4.</span></span> <span data-ttu-id="07268-188">Parar extensão Olá colete os logs</span><span class="sxs-lookup"><span data-stu-id="07268-188">Stop hello extension from collecting any logs</span></span>

<span data-ttu-id="07268-189">Esta seção descreve como extensão de saudação toostop de coleta de logs.</span><span class="sxs-lookup"><span data-stu-id="07268-189">This section describes how toostop hello extension from collecting logs.</span></span> <span data-ttu-id="07268-190">Observe que o processo do agente de monitoramento de Olá será ainda em execução até mesmo com essa reconfiguração.</span><span class="sxs-lookup"><span data-stu-id="07268-190">Note that hello monitoring agent process will be still up and running even with this reconfiguration.</span></span> <span data-ttu-id="07268-191">Se você desejar Olá toostop completamente o processo de agente de monitoramento, você pode fazer isso desabilitando extensão Olá.</span><span class="sxs-lookup"><span data-stu-id="07268-191">If you'd like toostop hello monitoring agent process completely, you can do so by disabling hello extension.</span></span> <span data-ttu-id="07268-192">Olá comando toodisable Olá extensão é `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span><span class="sxs-lookup"><span data-stu-id="07268-192">hello command toodisable hello extension is `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span></span>

<span data-ttu-id="07268-193">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="07268-193">Step 1.</span></span> <span data-ttu-id="07268-194">Crie um arquivo chamado Privateconfig com conteúdo Olá descrito no cenário 1.</span><span class="sxs-lookup"><span data-stu-id="07268-194">Create a file named PrivateConfig.json with hello content that was described in Scenario 1.</span></span> <span data-ttu-id="07268-195">Crie outro arquivo chamado PublicConfig.json com hello seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="07268-195">Create another file named PublicConfig.json with hello following content:</span></span>

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


<span data-ttu-id="07268-196">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="07268-196">Step 2.</span></span> <span data-ttu-id="07268-197">Execute **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="07268-197">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

## <a name="review-your-data"></a><span data-ttu-id="07268-198">Examinar os dados</span><span class="sxs-lookup"><span data-stu-id="07268-198">Review your data</span></span>

<span data-ttu-id="07268-199">Olá dados de desempenho e diagnósticos são armazenados em uma tabela de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="07268-199">hello performance and diagnostic data are stored in an Azure Storage table.</span></span> <span data-ttu-id="07268-200">Revisão [como toouse armazenamento de tabela do Azure do Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn como tooaccess Olá no armazenamento de saudação de tabela por meio de scripts de CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="07268-200">Review [How toouse Azure Table Storage from Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn how tooaccess hello data in hello storage table by using Azure CLI scripts.</span></span>

<span data-ttu-id="07268-201">Além disso, você pode usar a interface do usuário ferramentas tooaccess Olá dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="07268-201">In addition, you can use following UI tools tooaccess hello data:</span></span>

1. <span data-ttu-id="07268-202">Gerenciador de Servidores do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="07268-202">Visual Studio Server Explorer.</span></span> <span data-ttu-id="07268-203">Vá tooyour conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="07268-203">Go tooyour storage account.</span></span> <span data-ttu-id="07268-204">Olá VM executado por aproximadamente cinco minutos, você verá tabelas padrão de saudação quatro: "LinuxCpu", "LinuxDisk", "LinuxMemory" e "Linuxsyslog".</span><span class="sxs-lookup"><span data-stu-id="07268-204">After hello VM runs for about five minutes, you'll see hello four default tables: “LinuxCpu”, ”LinuxDisk”, ”LinuxMemory”, and ”Linuxsyslog”.</span></span> <span data-ttu-id="07268-205">Clique duas vezes em dados de saudação do hello tabela nomes tooview.</span><span class="sxs-lookup"><span data-stu-id="07268-205">Double-click hello table names tooview hello data.</span></span>
1. <span data-ttu-id="07268-206">[Gerenciador de Armazenamento do Azure](https://azurestorageexplorer.codeplex.com/ "Gerenciador de Armazenamento do Azure")(Soluções de Plataforma Cruzada do System Center).</span><span class="sxs-lookup"><span data-stu-id="07268-206">[Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

![imagem](./media/diagnostic-extension/no1.png)

<span data-ttu-id="07268-208">Se você tiver habilitado o fileCfg ou perfCfg (conforme descrito em cenários de 2 e 3), você pode usar dados de não-padrão tooview Visual Studio Server Explorer e o Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="07268-208">If you've enabled fileCfg or perfCfg (as described in Scenarios 2 and 3), you can use Visual Studio Server Explorer and Azure Storage Explorer tooview non-default data.</span></span>

## <a name="known-issues"></a><span data-ttu-id="07268-209">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="07268-209">Known issues</span></span>

* <span data-ttu-id="07268-210">Olá Rsyslog informações e o arquivo de log especificado pelo cliente só pode ser acessado por meio de scripts.</span><span class="sxs-lookup"><span data-stu-id="07268-210">hello Rsyslog information and customer-specified log file can only be accessed via scripting.</span></span>
