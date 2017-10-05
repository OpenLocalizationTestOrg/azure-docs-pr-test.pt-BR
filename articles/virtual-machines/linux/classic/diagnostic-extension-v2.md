---
title: "Monitorando uma VM Linux com uma extensão de VM | Microsoft Docs"
description: "Saiba como usar a Extensão de Diagnóstico do Linux para monitorar os dados de desempenho e diagnóstico de uma VM do Linux no Azure."
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
ms.openlocfilehash: b8c6e2e22d8478b6e92e7b7942f15d37a840fed3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-linux-diagnostic-extension-to-monitor-the-performance-and-diagnostic-data-of-a-linux-vm"></a><span data-ttu-id="9c8bb-103">Usar a Extensão de Diagnóstico do Linux para monitorar os dados de desempenho e diagnóstico da VM do Linux</span><span class="sxs-lookup"><span data-stu-id="9c8bb-103">Use the Linux Diagnostic Extension to monitor the performance and diagnostic data of a Linux VM</span></span>

<span data-ttu-id="9c8bb-104">Este documento descreve a versão 2.3 da Extensão de Diagnóstico do Linux.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-104">This document describes version 2.3 of the Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c8bb-105">Esta versão foi preterida e sua publicação pode ser cancelada a qualquer momento após 30 de junho de 2018.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-105">This version is deprecated, and it may be unpublished any time after June 30, 2018.</span></span> <span data-ttu-id="9c8bb-106">Ela foi substituída pela versão 3.0.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-106">It has been replaced by version 3.0.</span></span> <span data-ttu-id="9c8bb-107">Para obter mais informações, confira a [documentação da versão 3.0 da Extensão de Diagnóstico do Linux](../diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="9c8bb-107">For more information, see the [documentation for version 3.0 of the Linux Diagnostic Extension](../diagnostic-extension.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="9c8bb-108">Introdução</span><span class="sxs-lookup"><span data-stu-id="9c8bb-108">Introduction</span></span>

<span data-ttu-id="9c8bb-109">(**Observação**: a Extensão de Diagnóstico do Linux é de software livre no [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic), onde as informações mais atuais sobre a extensão foram publicadas pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-109">(**Note**: The Linux Diagnostic Extension is open-sourced on [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) where the most current information on the extension is first published.</span></span> <span data-ttu-id="9c8bb-110">Convém dar uma olhada na [página do GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) primeiro.)</span><span class="sxs-lookup"><span data-stu-id="9c8bb-110">You might want to check the [GitHub page](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) first.)</span></span>

<span data-ttu-id="9c8bb-111">A Extensão de Diagnóstico do Linux ajuda um usuário a monitorar as VMs Linux em execução no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-111">The Linux Diagnostic Extension helps a user monitor the Linux VMs that are running on Microsoft Azure.</span></span> <span data-ttu-id="9c8bb-112">Ela oferece os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="9c8bb-112">It has the following capabilities:</span></span>

* <span data-ttu-id="9c8bb-113">Coleta e carregamento de informações de desempenho do sistema, da VM Linux para a tabela de armazenamento do usuário, incluindo informações de diagnóstico e syslog.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-113">Collects and uploads the system performance information from the Linux VM to the user's storage table, including diagnostic and syslog information.</span></span>
* <span data-ttu-id="9c8bb-114">Permite que os usuários personalizem as métricas de dados que serão coletadas e carregadas.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-114">Enables users to customize the data metrics that will be collected and uploaded.</span></span>
* <span data-ttu-id="9c8bb-115">Permite que os usuários carreguem arquivos de log especificados em uma tabela de armazenamento designada.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-115">Enables users to upload specified log files to a designated storage table.</span></span>

<span data-ttu-id="9c8bb-116">Na versão 2.3 atual, os dados incluem:</span><span class="sxs-lookup"><span data-stu-id="9c8bb-116">In the current version 2.3, the data includes:</span></span>

* <span data-ttu-id="9c8bb-117">Todos os logs Rsyslog do Linux, incluindo logs de sistema, de segurança e de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-117">All Linux Rsyslog logs, including system, security, and application logs.</span></span>
* <span data-ttu-id="9c8bb-118">Todos os dados do sistema especificados [no site do System Center Cross Platform Solutions](https://scx.codeplex.com/wikipage?title=xplatproviders)(Soluções de Plataforma Cruzada do System Center).</span><span class="sxs-lookup"><span data-stu-id="9c8bb-118">All system data that's specified on [the System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
* <span data-ttu-id="9c8bb-119">Arquivos de log especificados pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-119">User-specified log files.</span></span>

<span data-ttu-id="9c8bb-120">Essa extensão funciona com os modelos de implantação Clássico e do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-120">This extension works with both the classic and Resource Manager deployment models.</span></span>

### <a name="current-version-of-the-extension-and-deprecation-of-old-versions"></a><span data-ttu-id="9c8bb-121">Versão atual da extensão e substituição de versões antigas</span><span class="sxs-lookup"><span data-stu-id="9c8bb-121">Current version of the extension and deprecation of old versions</span></span>

<span data-ttu-id="9c8bb-122">A versão mais recente da extensão é a **2.3** e **todas as versões antigas (2.0, 2.1 e 2.2) serão preteridas com suas publicações canceladas até o final deste ano (2017)**.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-122">The latest version of the extension is **2.3**, and **any old versions (2.0, 2.1, and 2.2) will be deprecated and unpublished by end of this year (2017)**.</span></span> <span data-ttu-id="9c8bb-123">Se você instalou a Extensão de Diagnóstico do Linux com a atualização automática de versão secundária desabilitada, é altamente recomendado que você desinstale a extensão e reinstale-a com a atualização automática de versão secundária habilitada.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-123">If you installed the Linux Diagnostic extension with automatic minor version upgrade disabled, it's strongly recommended that you uninstall the extension and reinstall it with automatic minor version upgrade enabled.</span></span> <span data-ttu-id="9c8bb-124">Em VMs clássicas (ASM), você pode conseguir isso especificando '2.*' como a versão, se você estiver instalando a extensão por meio da CLI do Azure XPLAT ou do Powershell.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-124">On classic (ASM) VMs, you can achieve this by specifying '2.*' as the version if you are installing the extension through Azure XPLAT CLI or Powershell.</span></span> <span data-ttu-id="9c8bb-125">Em VMs ARM, você pode conseguir isso, incluindo ' "autoUpgradeMinorVersion": true' no modelo de implantação da VM.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-125">On ARM VMs, you can achieve this by including '"autoUpgradeMinorVersion": true' in the VM deployment template.</span></span> <span data-ttu-id="9c8bb-126">Além disso, todas as novas instalações da extensão devem ter a opção de atualização automática de versão secundária ativada.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-126">Also, any new installation of the extension should have the auto minor version upgrade option turned on.</span></span>

## <a name="enable-the-extension"></a><span data-ttu-id="9c8bb-127">Habilitar a extensão</span><span class="sxs-lookup"><span data-stu-id="9c8bb-127">Enable the extension</span></span>

<span data-ttu-id="9c8bb-128">Você pode habilitar essa extensão usando o [Portal do Azure](https://portal.azure.com/#), o Azure PowerShell ou os scripts da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-128">You can enable this extension by using the [Azure portal](https://portal.azure.com/#), Azure PowerShell, or Azure CLI scripts.</span></span>

<span data-ttu-id="9c8bb-129">Para exibir e configurar os dados de desempenho e do sistema diretamente do portal do Azure, siga [estas etapas no blog do Azure](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span><span class="sxs-lookup"><span data-stu-id="9c8bb-129">To view and configure the system and performance data directly from the Azure portal, follow [these steps on the Azure blog](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).</span></span>

<span data-ttu-id="9c8bb-130">Este artigo se concentra em como habilitar e configurar a extensão usando os comandos da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-130">This article focuses on how to enable and configure the extension by using Azure CLI commands.</span></span> <span data-ttu-id="9c8bb-131">Isso permite que você leia e exiba os dados diretamente da tabela de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-131">This allows you to read and view the data directly from the storage table.</span></span>

<span data-ttu-id="9c8bb-132">Observe que os métodos de configuração descritos abaixo não funcionarão para o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-132">Note that the configuration methods that are described here won't work for the Azure portal.</span></span> <span data-ttu-id="9c8bb-133">Para exibir e configurar os dados de desempenho e do sistema diretamente do Portal do Azure, a extensão deve ser habilitada no Portal.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-133">To view and configure the system and performance data directly from the Azure portal, the extension must be enabled through the portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c8bb-134">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9c8bb-134">Prerequisites</span></span>

* <span data-ttu-id="9c8bb-135">**Agente Linux do Azure versão 2.0.6 ou posterior**.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-135">**Azure Linux Agent version 2.0.6 or later**.</span></span>

  <span data-ttu-id="9c8bb-136">Observe que a maioria das imagens de galeria da VM Linux do Azure inclui a versão 2.0.6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-136">Note that most Azure VM Linux gallery images include version 2.0.6 or later.</span></span> <span data-ttu-id="9c8bb-137">É possível executar **WAAgent-version** para confirmar a versão que está instalada na VM.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-137">You can run **WAAgent -version** to confirm which version is installed on the VM.</span></span> <span data-ttu-id="9c8bb-138">Se a VM estiver executando uma versão anterior à 2.0.6, execute [estas instruções no GitHub](https://github.com/Azure/WALinuxAgent "instruções") para atualizá-la.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-138">If the VM is running a version that's earlier than 2.0.6, you can follow [these instructions on GitHub](https://github.com/Azure/WALinuxAgent "instructions") to update it.</span></span>
* <span data-ttu-id="9c8bb-139">**CLI do Azure**.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-139">**Azure CLI**.</span></span> <span data-ttu-id="9c8bb-140">Siga [estas diretrizes de instalação da CLI](../../../cli-install-nodejs.md) para configurar o ambiente da CLI do Azure em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-140">Follow [this guidance for installing CLI](../../../cli-install-nodejs.md) to set up the Azure CLI environment on your machine.</span></span> <span data-ttu-id="9c8bb-141">Depois de instalar a CLI do Azure, você poderá usar o comando **azure** em sua interface de linha de comando (Bash, Terminal ou prompt de comando) para acessar os comandos da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-141">After Azure CLI is installed, you can use the **azure** command from your command-line interface (Bash, Terminal, or command prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="9c8bb-142">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9c8bb-142">For example:</span></span>

  * <span data-ttu-id="9c8bb-143">Execute **azure vm extension set --help** para obter informações de ajuda detalhadas.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-143">Run **azure vm extension set --help** for detailed help information.</span></span>
  * <span data-ttu-id="9c8bb-144">Execute **azure login** para entrar no Azure.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-144">Run **azure login** to sign in to Azure.</span></span>
  * <span data-ttu-id="9c8bb-145">Execute **azure vm list** para listar todas as máquinas virtuais que você tem no Azure.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-145">Run **azure vm list** to list all the virtual machines that you have on Azure.</span></span>
* <span data-ttu-id="9c8bb-146">Uma conta de armazenamento para armazenar os dados.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-146">A storage account to store the data.</span></span> <span data-ttu-id="9c8bb-147">Você precisará de um nome de conta de armazenamento criado anteriormente e de uma chave de acesso para carregar os dados no armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-147">You will need a storage account name that was created previously and an access key to upload the data to your storage.</span></span>

## <a name="use-the-azure-cli-command-to-enable-the-linux-diagnostic-extension"></a><span data-ttu-id="9c8bb-148">Usar o comando da CLI do Azure para habilitar a Extensão de Diagnóstico do Linux</span><span class="sxs-lookup"><span data-stu-id="9c8bb-148">Use the Azure CLI command to enable the Linux Diagnostic Extension</span></span>

### <a name="scenario-1-enable-the-extension-with-the-default-data-set"></a><span data-ttu-id="9c8bb-149">Cenário 1.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-149">Scenario 1.</span></span> <span data-ttu-id="9c8bb-150">Habilitar a extensão com o conjunto de dados padrão</span><span class="sxs-lookup"><span data-stu-id="9c8bb-150">Enable the extension with the default data set</span></span>

<span data-ttu-id="9c8bb-151">Na versão 2.3 ou posterior, os dados padrão que serão coletados incluem:</span><span class="sxs-lookup"><span data-stu-id="9c8bb-151">In version 2.3 or later, the default data that will be collected includes:</span></span>

* <span data-ttu-id="9c8bb-152">Todas as informações de Rsyslog (incluindo os logs de sistema, segurança e aplicativo).</span><span class="sxs-lookup"><span data-stu-id="9c8bb-152">All Rsyslog information (including system, security, and application logs).</span></span>  
* <span data-ttu-id="9c8bb-153">Um conjunto principal de dados base do sistema.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-153">A core set of basis system data.</span></span> <span data-ttu-id="9c8bb-154">Observe que o conjunto de dados completo está descrito no [site do System Center Cross Platform Solutions](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="9c8bb-154">Note that the full data set is described on the [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span>
  <span data-ttu-id="9c8bb-155">Se você quiser habilitar dados extras, continue com as etapas nos Cenários 2 e 3.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-155">If you want to enable extra data, continue with the steps in Scenarios 2 and 3.</span></span>

<span data-ttu-id="9c8bb-156">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-156">Step 1.</span></span> <span data-ttu-id="9c8bb-157">Crie um arquivo chamado PrivateConfig.json com o conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c8bb-157">Create a file named PrivateConfig.json with the following content:</span></span>

    {
        "storageAccountName" : "the storage account to receive data",
        "storageAccountKey" : "the key of the account"
    }

<span data-ttu-id="9c8bb-158">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-158">Step 2.</span></span> <span data-ttu-id="9c8bb-159">Execute **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-159">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.</span></span>

### <a name="scenario-2-customize-the-performance-monitor-metrics"></a><span data-ttu-id="9c8bb-160">Cenário 2:</span><span class="sxs-lookup"><span data-stu-id="9c8bb-160">Scenario 2.</span></span> <span data-ttu-id="9c8bb-161">Personalizar a métrica do monitor de desempenho</span><span class="sxs-lookup"><span data-stu-id="9c8bb-161">Customize the performance monitor metrics</span></span>

<span data-ttu-id="9c8bb-162">Esta seção descreve como personalizar a tabela de dados de desempenho e diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-162">This section describes how to customize the performance and diagnostic data table.</span></span>

<span data-ttu-id="9c8bb-163">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-163">Step 1.</span></span> <span data-ttu-id="9c8bb-164">Crie um arquivo chamado PrivateConfig.json com o conteúdo descrito no Cenário 1.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-164">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="9c8bb-165">Além disso, crie um arquivo chamado PublicConfig.json.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-165">Also create a file named PublicConfig.json.</span></span> <span data-ttu-id="9c8bb-166">Especifique os dados específicos que deseja coletar.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-166">Specify the particular data you want to collect.</span></span>

<span data-ttu-id="9c8bb-167">Para conhecer todos os provedores e variáveis com suporte, consulte o [site do System Center Cross Platform Solutions](https://scx.codeplex.com/wikipage?title=xplatproviders).</span><span class="sxs-lookup"><span data-stu-id="9c8bb-167">For all supported providers and variables, reference the [System Center Cross Platform Solutions site](https://scx.codeplex.com/wikipage?title=xplatproviders).</span></span> <span data-ttu-id="9c8bb-168">Você pode ter várias consultas e armazená-las em várias tabelas, acrescentando mais consultas ao script.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-168">You can have multiple queries and store them in multiple tables by appending more queries to the script.</span></span>

<span data-ttu-id="9c8bb-169">Por padrão, os dados de Rsyslog sempre são coletados.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-169">By default, the Rsyslog data is always collected.</span></span>

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


<span data-ttu-id="9c8bb-170">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-170">Step 2.</span></span> <span data-ttu-id="9c8bb-171">Execute **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-171">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

### <a name="scenario-3-upload-your-own-log-files"></a><span data-ttu-id="9c8bb-172">Cenário 3:</span><span class="sxs-lookup"><span data-stu-id="9c8bb-172">Scenario 3.</span></span> <span data-ttu-id="9c8bb-173">Carregar os próprios arquivos de log</span><span class="sxs-lookup"><span data-stu-id="9c8bb-173">Upload your own log files</span></span>

<span data-ttu-id="9c8bb-174">Esta seção descreve como coletar e carregar arquivos de log específicos em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-174">This section describes how to collect and upload specific log files to your storage account.</span></span> <span data-ttu-id="9c8bb-175">Você precisa especificar o caminho até seu arquivo de log e o nome da tabela onde você deseja armazenar seu log.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-175">You need to specify both the path to your log file and the name of the table where you want to store your log.</span></span> <span data-ttu-id="9c8bb-176">Você pode criar vários arquivos de log adicionando várias entradas de arquivo/tabela ao script.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-176">You can create multiple log files by adding multiple file/table entries to the script.</span></span>

<span data-ttu-id="9c8bb-177">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-177">Step 1.</span></span> <span data-ttu-id="9c8bb-178">Crie um arquivo chamado PrivateConfig.json com o conteúdo descrito no Cenário 1.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-178">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="9c8bb-179">Em seguida, crie outro arquivo denominado PublicConfig.json com o conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c8bb-179">Then create another file named PublicConfig.json with the following content:</span></span>

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

<span data-ttu-id="9c8bb-180">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-180">Step 2.</span></span> <span data-ttu-id="9c8bb-181">Execute `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-181">Run `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.</span></span>

<span data-ttu-id="9c8bb-182">Observe que, com essa configuração nas versões de extensão anteriores a 2.3, todos os logs gravados em `/var/log/mysql.err` também podem ser duplicados para `/var/log/syslog` (ou `/var/log/messages`, dependendo da distribuição Linux).</span><span class="sxs-lookup"><span data-stu-id="9c8bb-182">Note that with this setting on the extension versions prior to 2.3, all logs written to `/var/log/mysql.err` might be duplicated to `/var/log/syslog` (or `/var/log/messages` depending on the Linux distro) as well.</span></span> <span data-ttu-id="9c8bb-183">Se você quiser evitar esse registro duplicado, exclua o registro em log dos logs de recursos do `local6` em sua configuração de rsyslog.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-183">If you'd like to avoid this duplicate logging, you can exclude logging of `local6` facility logs in your rsyslog configuration.</span></span> <span data-ttu-id="9c8bb-184">Isso depende da distribuição do Linux, mas em um sistema Ubuntu 14.04, o arquivo a ser modificado é o `/etc/rsyslog.d/50-default.conf` e você pode substituir a linha `*.*;auth,authpriv.none -/var/log/syslog` por `*.*;auth,authpriv,local6.none -/var/log/syslog`.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-184">It depends on the Linux distro, but on an Ubuntu 14.04 system, the file to modify is `/etc/rsyslog.d/50-default.conf` and you can replace the line `*.*;auth,authpriv.none -/var/log/syslog` to `*.*;auth,authpriv,local6.none -/var/log/syslog`.</span></span> <span data-ttu-id="9c8bb-185">Esse problema foi corrigido na versão mais recente de hotfix 2.3 (2.3.9007); portanto, se você tiver a versão de extensão 2.3, esse problema não deverá ocorrer.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-185">This issue is fixed in the latest hotfix release of 2.3 (2.3.9007), so if you have the extension version 2.3, this issue should not happen.</span></span> <span data-ttu-id="9c8bb-186">Se o problema ainda persistir mesmo após a reinicialização da VM, entre em contato conosco e nos ajude a descobrir por que a versão mais recente de hotfix não é instalada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-186">If it still does even after restarting your VM, please contact us and help us troubleshoot why the latest hotfix version is not installed automatically.</span></span>

### <a name="scenario-4-stop-the-extension-from-collecting-any-logs"></a><span data-ttu-id="9c8bb-187">Cenário 4:</span><span class="sxs-lookup"><span data-stu-id="9c8bb-187">Scenario 4.</span></span> <span data-ttu-id="9c8bb-188">Parar a coleta de todos os logs pela extensão</span><span class="sxs-lookup"><span data-stu-id="9c8bb-188">Stop the extension from collecting any logs</span></span>

<span data-ttu-id="9c8bb-189">Esta seção descreve como parar a coleta de logs pela extensão.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-189">This section describes how to stop the extension from collecting logs.</span></span> <span data-ttu-id="9c8bb-190">Observe que o processo do agente de monitoramento ainda estará em execução mesmo com essa reconfiguração.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-190">Note that the monitoring agent process will be still up and running even with this reconfiguration.</span></span> <span data-ttu-id="9c8bb-191">Se quiser parar o completamente processo do agente de monitoramento, você poderá fazer isso desabilitando a extensão.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-191">If you'd like to stop the monitoring agent process completely, you can do so by disabling the extension.</span></span> <span data-ttu-id="9c8bb-192">O comando para desabilitar a extensão é `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-192">The command to disable the extension is `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.</span></span>

<span data-ttu-id="9c8bb-193">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-193">Step 1.</span></span> <span data-ttu-id="9c8bb-194">Crie um arquivo chamado PrivateConfig.json com o conteúdo descrito no Cenário 1.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-194">Create a file named PrivateConfig.json with the content that was described in Scenario 1.</span></span> <span data-ttu-id="9c8bb-195">Crie outro arquivo denominado PublicConfig.json com o conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9c8bb-195">Create another file named PublicConfig.json with the following content:</span></span>

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


<span data-ttu-id="9c8bb-196">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-196">Step 2.</span></span> <span data-ttu-id="9c8bb-197">Execute **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-197">Run **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.</span></span>

## <a name="review-your-data"></a><span data-ttu-id="9c8bb-198">Examinar os dados</span><span class="sxs-lookup"><span data-stu-id="9c8bb-198">Review your data</span></span>

<span data-ttu-id="9c8bb-199">Os dados de desempenho e diagnóstico são armazenados em uma tabela de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-199">The performance and diagnostic data are stored in an Azure Storage table.</span></span> <span data-ttu-id="9c8bb-200">Revise [Como usar o Armazenamento de Tabelas do Azure no Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) para saber como acessar os dados na tabela de armazenamento por meio de scripts da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-200">Review [How to use Azure Table Storage from Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) to learn how to access the data in the storage table by using Azure CLI scripts.</span></span>

<span data-ttu-id="9c8bb-201">Além disso, você pode usar as ferramentas de interface do usuário a seguir para acessar os dados:</span><span class="sxs-lookup"><span data-stu-id="9c8bb-201">In addition, you can use following UI tools to access the data:</span></span>

1. <span data-ttu-id="9c8bb-202">Gerenciador de Servidores do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-202">Visual Studio Server Explorer.</span></span> <span data-ttu-id="9c8bb-203">Vá até sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-203">Go to your storage account.</span></span> <span data-ttu-id="9c8bb-204">Depois que a VM for executada por aproximadamente cinco minutos, você deverá ver as quatro tabelas padrão: "LinuxCpu", "LinuxDisk", "LinuxMemory" e "Linuxsyslog".</span><span class="sxs-lookup"><span data-stu-id="9c8bb-204">After the VM runs for about five minutes, you'll see the four default tables: “LinuxCpu”, ”LinuxDisk”, ”LinuxMemory”, and ”Linuxsyslog”.</span></span> <span data-ttu-id="9c8bb-205">Clique duas vezes nos nomes de tabela para exibir os dados.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-205">Double-click the table names to view the data.</span></span>
1. <span data-ttu-id="9c8bb-206">[Gerenciador de Armazenamento do Azure](https://azurestorageexplorer.codeplex.com/ "Gerenciador de Armazenamento do Azure")(Soluções de Plataforma Cruzada do System Center).</span><span class="sxs-lookup"><span data-stu-id="9c8bb-206">[Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

![imagem](./media/diagnostic-extension/no1.png)

<span data-ttu-id="9c8bb-208">Se você tiver habilitado fileCfg ou perfCfg (conforme descrito nos Cenários 2 e 3), você poderá usar o Gerenciador de Servidores do Visual Studio e o Gerenciador de Armazenamento do Azure para exibir dados não padrão.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-208">If you've enabled fileCfg or perfCfg (as described in Scenarios 2 and 3), you can use Visual Studio Server Explorer and Azure Storage Explorer to view non-default data.</span></span>

## <a name="known-issues"></a><span data-ttu-id="9c8bb-209">Problemas conhecidos</span><span class="sxs-lookup"><span data-stu-id="9c8bb-209">Known issues</span></span>

* <span data-ttu-id="9c8bb-210">As informações do Rsyslog e o arquivo de log especificado pelo cliente só podem ser acessados por meio de scripts.</span><span class="sxs-lookup"><span data-stu-id="9c8bb-210">The Rsyslog information and customer-specified log file can only be accessed via scripting.</span></span>
