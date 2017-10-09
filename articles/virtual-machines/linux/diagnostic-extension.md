---
title: "Computação de aaaAzure - extensão de diagnóstico do Linux | Microsoft Docs"
description: "Como tooconfigure Olá métricas de toocollect Azure Linux diagnóstico extensão (LAD) e registrar eventos de VMs do Linux em execução no Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 2b27ec00a876ded359a75170b407e28c40d8445d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-linux-diagnostic-extension-toomonitor-metrics-and-logs"></a><span data-ttu-id="f8495-103">Usar os logs e métricas de toomonitor de extensão de diagnóstico do Linux</span><span class="sxs-lookup"><span data-stu-id="f8495-103">Use Linux Diagnostic Extension toomonitor metrics and logs</span></span>

<span data-ttu-id="f8495-104">Este documento descreve a versão 3.0 e versões mais recente de saudação extensão de diagnóstico do Linux.</span><span class="sxs-lookup"><span data-stu-id="f8495-104">This document describes version 3.0 and newer of hello Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8495-105">Para saber mais sobre a versão 2.3 e anteriores, veja [este documento](./classic/diagnostic-extension-v2.md).</span><span class="sxs-lookup"><span data-stu-id="f8495-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="f8495-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="f8495-106">Introduction</span></span>

<span data-ttu-id="f8495-107">Olá extensão de diagnóstico do Linux ajuda uma usuário monitorar Olá a integridade de uma VM do Linux em execução no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f8495-107">hello Linux Diagnostic Extension helps a user monitor hello health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="f8495-108">Ele tem Olá recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8495-108">It has hello following capabilities:</span></span>

* <span data-ttu-id="f8495-109">Coleta métricas de desempenho do sistema de saudação VM e os armazena em uma tabela específica em uma conta de armazenamento designadas.</span><span class="sxs-lookup"><span data-stu-id="f8495-109">Collects system performance metrics from hello VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="f8495-110">Recupera o log de eventos de syslog e os armazena em uma tabela específica no hello designado a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f8495-110">Retrieves log events from syslog and stores them in a specific table in hello designated storage account.</span></span>
* <span data-ttu-id="f8495-111">Permite que os usuários toocustomize Olá as métricas de dados que são coletadas e carregadas.</span><span class="sxs-lookup"><span data-stu-id="f8495-111">Enables users toocustomize hello data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="f8495-112">Habilita recursos de syslog usuários toocustomize hello e níveis de severidade dos eventos que são coletados e carregados.</span><span class="sxs-lookup"><span data-stu-id="f8495-112">Enables users toocustomize hello syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="f8495-113">Permite que os usuários tooupload log especificado arquivos tooa armazenamento designadas tabela.</span><span class="sxs-lookup"><span data-stu-id="f8495-113">Enables users tooupload specified log files tooa designated storage table.</span></span>
* <span data-ttu-id="f8495-114">Oferece suporte ao envio de log e métricas eventos tooarbitrary EventHub pontos de extremidade e blobs formatada em JSON em Olá designado como conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f8495-114">Supports sending metrics and log events tooarbitrary EventHub endpoints and JSON-formatted blobs in hello designated storage account.</span></span>

<span data-ttu-id="f8495-115">Essa extensão funciona com os dois modelos de implantação do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8495-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-hello-extension-in-your-vm"></a><span data-ttu-id="f8495-116">Instalação da extensão Olá em sua VM</span><span class="sxs-lookup"><span data-stu-id="f8495-116">Installing hello extension in your VM</span></span>

<span data-ttu-id="f8495-117">Você pode habilitar esta extensão usando cmdlets do PowerShell do Azure hello, scripts de CLI do Azure ou modelos de implantação do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8495-117">You can enable this extension by using hello Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="f8495-118">Para saber mais, veja [Recursos de extensões](./extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="f8495-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="f8495-119">Olá portal do Azure não pode ser usado tooenable ou configurar LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="f8495-119">hello Azure portal cannot be used tooenable or configure LAD 3.0.</span></span> <span data-ttu-id="f8495-120">Em vez disso, ele instala e configura a versão 2.3.</span><span class="sxs-lookup"><span data-stu-id="f8495-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="f8495-121">Alertas e gráficos do portais do azure trabalham com dados de ambas as versões da extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-121">Azure portal graphs and alerts work with data from both versions of hello extension.</span></span>

<span data-ttu-id="f8495-122">Estas instruções de instalação e uma [configuração de amostra para download](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configuram o LAD 3.0 para:</span><span class="sxs-lookup"><span data-stu-id="f8495-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="f8495-123">captura e armazenamento Olá mesmas métricas que foram fornecidos pela LAD 2.3;</span><span class="sxs-lookup"><span data-stu-id="f8495-123">capture and store hello same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="f8495-124">capturar um conjunto útil de métricas do sistema de arquivo, novo tooLAD 3.0;</span><span class="sxs-lookup"><span data-stu-id="f8495-124">capture a useful set of file system metrics, new tooLAD 3.0;</span></span>
* <span data-ttu-id="f8495-125">capturar a coleção de syslog padrão Olá habilitada por LAD 2.3;</span><span class="sxs-lookup"><span data-stu-id="f8495-125">capture hello default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="f8495-126">Habilite Olá experiência do portal do Azure para criar gráficos e alertas em métricas VM.</span><span class="sxs-lookup"><span data-stu-id="f8495-126">enable hello Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="f8495-127">configuração para download Olá é apenas um exemplo; Modifique toosuit suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="f8495-127">hello downloadable configuration is just an example; modify it toosuit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f8495-128">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f8495-128">Prerequisites</span></span>

* <span data-ttu-id="f8495-129">**Agente Linux do Azure versão 2.2.0 ou posterior**.</span><span class="sxs-lookup"><span data-stu-id="f8495-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="f8495-130">A maioria das imagens de galeria da VM Linux do Azure inclui a versão 2.2.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f8495-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="f8495-131">Executar `/usr/sbin/waagent -version` versão Olá tooconfirm no hello VM.</span><span class="sxs-lookup"><span data-stu-id="f8495-131">Run `/usr/sbin/waagent -version` tooconfirm hello version installed on hello VM.</span></span> <span data-ttu-id="f8495-132">Se Olá VM estiver executando uma versão mais antiga do agente de convidado hello, siga [estas instruções](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate-lo.</span><span class="sxs-lookup"><span data-stu-id="f8495-132">If hello VM is running an older version of hello guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) tooupdate it.</span></span>
* <span data-ttu-id="f8495-133">**CLI do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f8495-133">**Azure CLI**.</span></span> <span data-ttu-id="f8495-134">[Configurar hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) ambiente em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f8495-134">[Set up hello Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="f8495-135">Olá wget comando, se ainda não tiver: executar `sudo apt-get install wget`.</span><span class="sxs-lookup"><span data-stu-id="f8495-135">hello wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="f8495-136">Uma assinatura do Azure existente e um armazenamento existente conta nele toostore dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-136">An existing Azure subscription and an existing storage account within it toostore hello data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="f8495-137">Instalação de exemplo</span><span class="sxs-lookup"><span data-stu-id="f8495-137">Sample installation</span></span>

<span data-ttu-id="f8495-138">Preencha parâmetros corretos Olá Olá três primeiras linhas, em seguida, executar este script como raiz:</span><span class="sxs-lookup"><span data-stu-id="f8495-138">Fill in hello correct parameters on hello first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login tooAzure first before anything else
az login

# Select hello subscription containing hello storage account
az account set --subscription <your_azure_subscription_id>

# Download hello sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build hello VM resource ID. Replace storage account name and resource ID in hello public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build hello protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure tooinstall and enable hello extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="f8495-139">saudação URL para a configuração de exemplo hello e seu conteúdo, é toochange de assunto.</span><span class="sxs-lookup"><span data-stu-id="f8495-139">hello URL for hello sample configuration, and its contents, are subject toochange.</span></span> <span data-ttu-id="f8495-140">Baixe uma cópia do arquivo JSON de configurações do portal hello e personalizá-la para suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="f8495-140">Download a copy of hello portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="f8495-141">Os modelos ou as automações que você construir deverão usar sua própria cópia em vez de baixar essa URL toda vez.</span><span class="sxs-lookup"><span data-stu-id="f8495-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-hello-extension-settings"></a><span data-ttu-id="f8495-142">Atualizando configurações de extensão Olá</span><span class="sxs-lookup"><span data-stu-id="f8495-142">Updating hello extension settings</span></span>

<span data-ttu-id="f8495-143">Depois que você alterou seu protegidos ou as configurações públicas, implantá-los toohello VM executando Olá mesmo comando.</span><span class="sxs-lookup"><span data-stu-id="f8495-143">After you've changed your Protected or Public settings, deploy them toohello VM by running hello same command.</span></span> <span data-ttu-id="f8495-144">Se nada alterado nas configurações de Olá, configurações de saudação atualizada sejam enviadas toohello extensão.</span><span class="sxs-lookup"><span data-stu-id="f8495-144">If anything changed in hello settings, hello updated settings are sent toohello extension.</span></span> <span data-ttu-id="f8495-145">LAD de recargas de configuração hello e reinicia em si.</span><span class="sxs-lookup"><span data-stu-id="f8495-145">LAD reloads hello configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-hello-extension"></a><span data-ttu-id="f8495-146">Migração de versões anteriores da extensão de saudação</span><span class="sxs-lookup"><span data-stu-id="f8495-146">Migration from previous versions of hello extension</span></span>

<span data-ttu-id="f8495-147">Olá a versão mais recente da extensão de saudação é **3.0**.</span><span class="sxs-lookup"><span data-stu-id="f8495-147">hello latest version of hello extension is **3.0**.</span></span> <span data-ttu-id="f8495-148">**As versões anteriores (2.x) antigas são substituídas e podem ser canceladas em ou após 31 de julho de 2018**.</span><span class="sxs-lookup"><span data-stu-id="f8495-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8495-149">Essa extensão apresenta a configuração de toohello recentes alterações de extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-149">This extension introduces breaking changes toohello configuration of hello extension.</span></span> <span data-ttu-id="f8495-150">Uma alteração foi feita a segurança de saudação tooimprove da extensão de saudação; Como resultado, com versões anteriores a compatibilidade com 2. x pode não ser mantida.</span><span class="sxs-lookup"><span data-stu-id="f8495-150">One such change was made tooimprove hello security of hello extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="f8495-151">Além disso, Olá publicador de extensão para esta extensão é diferente do publicador Olá para as versões 2. x de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-151">Also, hello Extension Publisher for this extension is different than hello publisher for hello 2.x versions.</span></span>
>
> <span data-ttu-id="f8495-152">toomigrate de 2. x toothis nova versão da extensão hello, você deve desinstalar a extensão antigo hello (no antigo nome do publicador Olá), em seguida, instalar a versão 3 da extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-152">toomigrate from 2.x toothis new version of hello extension, you must uninstall hello old extension (under hello old publisher name), then install version 3 of hello extension.</span></span>

<span data-ttu-id="f8495-153">Recomendações:</span><span class="sxs-lookup"><span data-stu-id="f8495-153">Recommendations:</span></span>

* <span data-ttu-id="f8495-154">Instale a extensão de saudação com a atualização de versão secundária automático habilitada.</span><span class="sxs-lookup"><span data-stu-id="f8495-154">Install hello extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="f8495-155">No modelo de implantação clássico VMs, especifica '3.*' como versão de hello, se você estiver instalando uma extensão de saudação por meio do Azure XPLAT CLI ou o Powershell.</span><span class="sxs-lookup"><span data-stu-id="f8495-155">On classic deployment model VMs, specify '3.*' as hello version if you are installing hello extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="f8495-156">Na implantação do Azure Resource Manager modelo VMs, incluem ' "autoUpgradeMinorVersion": true' no modelo de implantação de VM hello.</span><span class="sxs-lookup"><span data-stu-id="f8495-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in hello VM deployment template.</span></span>
* <span data-ttu-id="f8495-157">Use uma conta de armazenamento nova/diferente para o LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="f8495-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="f8495-158">Há várias pequenas incompatibilidades entre o LAD 2.3 e o LAD 3.0 que dificultam o compartilhamento de uma conta:</span><span class="sxs-lookup"><span data-stu-id="f8495-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="f8495-159">O LAD 3.0 armazena os eventos de syslog em uma tabela com um nome diferente.</span><span class="sxs-lookup"><span data-stu-id="f8495-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="f8495-160">counterSpecifier Olá cadeias de caracteres para `builtin` métricas diferem em LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="f8495-160">hello counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="f8495-161">Configurações protegidas</span><span class="sxs-lookup"><span data-stu-id="f8495-161">Protected settings</span></span>

<span data-ttu-id="f8495-162">Esse conjunto de informações de configuração contém informações confidenciais que devem ser protegidas da visualização pública, por exemplo, as credenciais de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f8495-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="f8495-163">Essas configurações são transmitida tooand armazenado pela extensão de saudação em formato criptografado.</span><span class="sxs-lookup"><span data-stu-id="f8495-163">These settings are transmitted tooand stored by hello extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "hello storage account tooreceive data",
    "storageAccountEndPoint": "hello hostname suffix for hello cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="f8495-164">Nome</span><span class="sxs-lookup"><span data-stu-id="f8495-164">Name</span></span> | <span data-ttu-id="f8495-165">Valor</span><span class="sxs-lookup"><span data-stu-id="f8495-165">Value</span></span>
---- | -----
<span data-ttu-id="f8495-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="f8495-166">storageAccountName</span></span> | <span data-ttu-id="f8495-167">nome de Olá Olá da conta de armazenamento na qual os dados são gravados pela extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-167">hello name of hello storage account in which data is written by hello extension.</span></span>
<span data-ttu-id="f8495-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="f8495-168">storageAccountEndPoint</span></span> | <span data-ttu-id="f8495-169">ponto de extremidade de saudação (opcional) identificando nuvem Olá no qual Olá conta de armazenamento existe.</span><span class="sxs-lookup"><span data-stu-id="f8495-169">(optional) hello endpoint identifying hello cloud in which hello storage account exists.</span></span> <span data-ttu-id="f8495-170">Se essa configuração estiver ausente, LAD padrões toohello nuvem pública do Azure, `https://core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="f8495-170">If this setting is absent, LAD defaults toohello Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="f8495-171">toouse uma conta de armazenamento no Azure Alemanha, governo do Azure ou Azure China, defina este valor adequadamente.</span><span class="sxs-lookup"><span data-stu-id="f8495-171">toouse a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="f8495-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="f8495-172">storageAccountSasToken</span></span> | <span data-ttu-id="f8495-173">Um [token SAS de conta](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) para serviços Blob e tabela (`ss='bt'`), objetos e toocontainers aplicáveis (`srt='co'`), que concede adiciona, criar, listar, atualizar e permissões de gravação (`sp='acluw'`).</span><span class="sxs-lookup"><span data-stu-id="f8495-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable toocontainers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="f8495-174">Fazer *não* incluem hello líder do ponto de interrogação (?).</span><span class="sxs-lookup"><span data-stu-id="f8495-174">Do *not* include hello leading question-mark (?).</span></span>
<span data-ttu-id="f8495-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="f8495-175">mdsdHttpProxy</span></span> | <span data-ttu-id="f8495-176">(opcional) As informações necessárias de proxy HTTP tooenable Olá extensão tooconnect toohello especificado a conta de armazenamento e o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="f8495-176">(optional) HTTP proxy information needed tooenable hello extension tooconnect toohello specified storage account and endpoint.</span></span>
<span data-ttu-id="f8495-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="f8495-177">sinksConfig</span></span> | <span data-ttu-id="f8495-178">(opcional) Detalhes de destinos alternativos toowhich métricas e eventos podem ser entregues.</span><span class="sxs-lookup"><span data-stu-id="f8495-178">(optional) Details of alternative destinations toowhich metrics and events can be delivered.</span></span> <span data-ttu-id="f8495-179">detalhes específicos de saudação de cada coletor de dados suportados pela extensão de saudação são abordados nas seções de saudação que seguem.</span><span class="sxs-lookup"><span data-stu-id="f8495-179">hello specific details of each data sink supported by hello extension are covered in hello sections that follow.</span></span>

<span data-ttu-id="f8495-180">Você pode facilmente construir token SAS Olá necessárias por meio de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8495-180">You can easily construct hello required SAS token through hello Azure portal.</span></span>

1. <span data-ttu-id="f8495-181">Selecione Olá armazenamento geral conta toowhich desejar Olá extensão toowrite</span><span class="sxs-lookup"><span data-stu-id="f8495-181">Select hello general-purpose storage account toowhich you want hello extension toowrite</span></span>
1. <span data-ttu-id="f8495-182">Selecione "Assinatura de acesso compartilhado" da parte de configurações de saudação do menu esquerdo Olá</span><span class="sxs-lookup"><span data-stu-id="f8495-182">Select "Shared access signature" from hello Settings part of hello left menu</span></span>
1. <span data-ttu-id="f8495-183">Tornar Olá as seções apropriadas conforme descritas anteriormente</span><span class="sxs-lookup"><span data-stu-id="f8495-183">Make hello appropriate sections as previously described</span></span>
1. <span data-ttu-id="f8495-184">Clique botão de "Gerar SAS" hello.</span><span class="sxs-lookup"><span data-stu-id="f8495-184">Click hello "Generate SAS" button.</span></span>

![imagem](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="f8495-186">Saudação de cópia gerada SAS no campo de storageAccountSasToken Olá; Remover saudação à esquerda-interrogação ("?").</span><span class="sxs-lookup"><span data-stu-id="f8495-186">Copy hello generated SAS into hello storageAccountSasToken field; remove hello leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="f8495-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="f8495-187">sinksConfig</span></span>

```json
"sinksConfig": {
    "sink": [
        {
            "name": "sinkname",
            "type": "sinktype",
            ...
        },
        ...
    ]
},
```

<span data-ttu-id="f8495-188">Esta seção opcional define destinos adicionais, extensão de saudação toowhich envia informações de saudação coleta.</span><span class="sxs-lookup"><span data-stu-id="f8495-188">This optional section defines additional destinations toowhich hello extension sends hello information it collects.</span></span> <span data-ttu-id="f8495-189">matriz de "sink" Hello contém um objeto para cada coletor de dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="f8495-189">hello "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="f8495-190">Olá determina de atributo "type" hello outros atributos no objeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-190">hello "type" attribute determines hello other attributes in hello object.</span></span>

<span data-ttu-id="f8495-191">Elemento</span><span class="sxs-lookup"><span data-stu-id="f8495-191">Element</span></span> | <span data-ttu-id="f8495-192">Valor</span><span class="sxs-lookup"><span data-stu-id="f8495-192">Value</span></span>
------- | -----
<span data-ttu-id="f8495-193">name</span><span class="sxs-lookup"><span data-stu-id="f8495-193">name</span></span> | <span data-ttu-id="f8495-194">Uma cadeia de caracteres usada toorefer toothis coletor em outro lugar na configuração de extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-194">A string used toorefer toothis sink elsewhere in hello extension configuration.</span></span>
<span data-ttu-id="f8495-195">type</span><span class="sxs-lookup"><span data-stu-id="f8495-195">type</span></span> | <span data-ttu-id="f8495-196">tipo de saudação do coletor está sendo definido.</span><span class="sxs-lookup"><span data-stu-id="f8495-196">hello type of sink being defined.</span></span> <span data-ttu-id="f8495-197">Determina o hello outros valores (se houver) em instâncias desse tipo.</span><span class="sxs-lookup"><span data-stu-id="f8495-197">Determines hello other values (if any) in instances of this type.</span></span>

<span data-ttu-id="f8495-198">A versão 3.0 do hello extensão de diagnóstico do Linux oferece suporte a dois tipos de coletor: EventHub e JsonBlob.</span><span class="sxs-lookup"><span data-stu-id="f8495-198">Version 3.0 of hello Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="hello-eventhub-sink"></a><span data-ttu-id="f8495-199">coletor de EventHub Olá</span><span class="sxs-lookup"><span data-stu-id="f8495-199">hello EventHub sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "EventHub",
        "sasURL": "https SAS URL"
    },
    ...
]
```

<span data-ttu-id="f8495-200">entrada de "sasURL" Hello contém Olá URL completa, incluindo o token SAS, Olá dados do Hub de eventos toowhich deve ser publicado.</span><span class="sxs-lookup"><span data-stu-id="f8495-200">hello "sasURL" entry contains hello full URL, including SAS token, for hello Event Hub toowhich data should be published.</span></span> <span data-ttu-id="f8495-201">LAD requer uma SAS uma política que permite que a declaração de envio de saudação de nomenclatura.</span><span class="sxs-lookup"><span data-stu-id="f8495-201">LAD requires a SAS naming a policy that enables hello Send claim.</span></span> <span data-ttu-id="f8495-202">Um exemplo:</span><span class="sxs-lookup"><span data-stu-id="f8495-202">An example:</span></span>

* <span data-ttu-id="f8495-203">Criar um namespace de Hubs de Eventos chamado `contosohub`</span><span class="sxs-lookup"><span data-stu-id="f8495-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="f8495-204">Criar um Hub de eventos no namespace Olá chamado`syslogmsgs`</span><span class="sxs-lookup"><span data-stu-id="f8495-204">Create an Event Hub in hello namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="f8495-205">Criar uma política de acesso compartilhado em Olá Hub de eventos denominado `writer` habilita Olá declaração de envio</span><span class="sxs-lookup"><span data-stu-id="f8495-205">Create a Shared access policy on hello Event Hub named `writer` that enables hello Send claim</span></span>

<span data-ttu-id="f8495-206">Se você tiver criado uma SAS válida até meia-noite UTC em 1 de janeiro de 2018, o valor de sasURL de saudação pode ser:</span><span class="sxs-lookup"><span data-stu-id="f8495-206">If you created a SAS good until midnight UTC on January 1, 2018, hello sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="f8495-207">Para saber mais sobre como gerar tokens de SAS para Hubs de Eventos, veja [esta página da Web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f8495-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="hello-jsonblob-sink"></a><span data-ttu-id="f8495-208">coletor de JsonBlob Olá</span><span class="sxs-lookup"><span data-stu-id="f8495-208">hello JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="f8495-209">Dados direcionados tooa JsonBlob coletor é armazenado em blobs no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8495-209">Data directed tooa JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="f8495-210">Cada instância de LAD cria um blob a cada hora para cada nome de coletor.</span><span class="sxs-lookup"><span data-stu-id="f8495-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="f8495-211">Cada blob sempre contém uma matriz de objeto JSON sintaticamente válida.</span><span class="sxs-lookup"><span data-stu-id="f8495-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="f8495-212">Matriz de toohello atomicamente são adicionadas novas entradas.</span><span class="sxs-lookup"><span data-stu-id="f8495-212">New entries are atomically added toohello array.</span></span> <span data-ttu-id="f8495-213">BLOBs são armazenados em um contêiner com mesmo nome como o coletor de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="f8495-213">Blobs are stored in a container with hello same name as hello sink.</span></span> <span data-ttu-id="f8495-214">Olá regras de armazenamento do Azure para nomes de contêiner de blob se aplicam a nomes de toohello de JsonBlob coletores: entre 3 e 63 caracteres ASCII alfanuméricos minúsculos ou traços.</span><span class="sxs-lookup"><span data-stu-id="f8495-214">hello Azure storage rules for blob container names apply toohello names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="f8495-215">Configurações públicas</span><span class="sxs-lookup"><span data-stu-id="f8495-215">Public settings</span></span>

<span data-ttu-id="f8495-216">Essa estrutura contém vários blocos de configurações que controlam as informações de saudação coletadas pela extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-216">This structure contains various blocks of settings that control hello information collected by hello extension.</span></span> <span data-ttu-id="f8495-217">Cada configuração é opcional.</span><span class="sxs-lookup"><span data-stu-id="f8495-217">Each setting is optional.</span></span> <span data-ttu-id="f8495-218">Se você especificar `ladCfg`, também deverá especificar `StorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="f8495-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "hello storage account tooreceive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="f8495-219">Elemento</span><span class="sxs-lookup"><span data-stu-id="f8495-219">Element</span></span> | <span data-ttu-id="f8495-220">Valor</span><span class="sxs-lookup"><span data-stu-id="f8495-220">Value</span></span>
------- | -----
<span data-ttu-id="f8495-221">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="f8495-221">StorageAccount</span></span> | <span data-ttu-id="f8495-222">nome de Olá Olá da conta de armazenamento na qual os dados são gravados pela extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-222">hello name of hello storage account in which data is written by hello extension.</span></span> <span data-ttu-id="f8495-223">Deve ser Olá mesmo nome que seja especificado na Olá [protegido configurações](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="f8495-223">Must be hello same name as is specified in hello [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="f8495-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="f8495-224">mdsdHttpProxy</span></span> | <span data-ttu-id="f8495-225">(opcional) Mesmo da saudação [protegido configurações](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="f8495-225">(optional) Same as in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="f8495-226">valor de público Olá é substituído pelo valor de private Olá, se definido.</span><span class="sxs-lookup"><span data-stu-id="f8495-226">hello public value is overridden by hello private value, if set.</span></span> <span data-ttu-id="f8495-227">Coloque as configurações de proxy que contêm um segredo, como uma senha, em Olá [protegido configurações](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="f8495-227">Place proxy settings that contain a secret, such as a password, in hello [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="f8495-228">elementos restantes da saudação são descritos detalhadamente nas seções a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-228">hello remaining elements are described in detail in hello following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="f8495-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="f8495-229">ladCfg</span></span>

```json
"ladCfg": {
    "diagnosticMonitorConfiguration": {
        "eventVolume": "Medium",
        "metrics": { ... },
        "performanceCounters": { ... },
        "syslogEvents": { ... }
    },
    "sampleRateInSeconds": 15
}
```

<span data-ttu-id="f8495-230">Essa coleta de saudação controles estrutura opcional de métricas e os logs para entrega toohello dados de serviço e tooother de métricas do Azure coletores.</span><span class="sxs-lookup"><span data-stu-id="f8495-230">This optional structure controls hello gathering of metrics and logs for delivery toohello Azure Metrics service and tooother data sinks.</span></span> <span data-ttu-id="f8495-231">Você deve especificar `performanceCounters` ou `syslogEvents`, ou ambos.</span><span class="sxs-lookup"><span data-stu-id="f8495-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="f8495-232">Você deve especificar Olá `metrics` estrutura.</span><span class="sxs-lookup"><span data-stu-id="f8495-232">You must specify hello `metrics` structure.</span></span>

<span data-ttu-id="f8495-233">Elemento</span><span class="sxs-lookup"><span data-stu-id="f8495-233">Element</span></span> | <span data-ttu-id="f8495-234">Valor</span><span class="sxs-lookup"><span data-stu-id="f8495-234">Value</span></span>
------- | -----
<span data-ttu-id="f8495-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="f8495-235">eventVolume</span></span> | <span data-ttu-id="f8495-236">(opcional) Número de partições criadas na tabela de armazenamento Olá Olá a controles.</span><span class="sxs-lookup"><span data-stu-id="f8495-236">(optional) Controls hello number of partitions created within hello storage table.</span></span> <span data-ttu-id="f8495-237">Pode ser `"Large"`, `"Medium"` ou `"Small"`.</span><span class="sxs-lookup"><span data-stu-id="f8495-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="f8495-238">Se não for especificado, o valor padrão de saudação é `"Medium"`.</span><span class="sxs-lookup"><span data-stu-id="f8495-238">If not specified, hello default value is `"Medium"`.</span></span>
<span data-ttu-id="f8495-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="f8495-239">sampleRateInSeconds</span></span> | <span data-ttu-id="f8495-240">intervalo padrão de saudação (opcional) entre o conjunto de métricas (não agregados) brutos.</span><span class="sxs-lookup"><span data-stu-id="f8495-240">(optional) hello default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="f8495-241">taxa de amostragem Olá menor com suporte é de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="f8495-241">hello smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="f8495-242">Se não for especificado, o valor padrão de saudação é `15`.</span><span class="sxs-lookup"><span data-stu-id="f8495-242">If not specified, hello default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="f8495-243">Métricas</span><span class="sxs-lookup"><span data-stu-id="f8495-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="f8495-244">Elemento</span><span class="sxs-lookup"><span data-stu-id="f8495-244">Element</span></span> | <span data-ttu-id="f8495-245">Valor</span><span class="sxs-lookup"><span data-stu-id="f8495-245">Value</span></span>
------- | -----
<span data-ttu-id="f8495-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="f8495-246">resourceId</span></span> | <span data-ttu-id="f8495-247">ID de recurso do Azure Resource Manager Olá do hello VM ou de escala de máquinas virtuais de saudação definir Olá toowhich que VM pertence.</span><span class="sxs-lookup"><span data-stu-id="f8495-247">hello Azure Resource Manager resource ID of hello VM or of hello virtual machine scale set toowhich hello VM belongs.</span></span> <span data-ttu-id="f8495-248">Essa configuração deve ser especificada também se qualquer coletor JsonBlob é usado na configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-248">This setting must be also specified if any JsonBlob sink is used in hello configuration.</span></span>
<span data-ttu-id="f8495-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="f8495-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="f8495-250">frequência de saudação em que as métricas agregadas são toobe computadas e transferidos tooAzure métricas, expressada como um intervalo de tempo é 8601.</span><span class="sxs-lookup"><span data-stu-id="f8495-250">hello frequency at which aggregate metrics are toobe computed and transferred tooAzure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="f8495-251">o período de transferência menor Olá é 60 segundos, ou seja, PT1M.</span><span class="sxs-lookup"><span data-stu-id="f8495-251">hello smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="f8495-252">Você deve especificar pelo menos um scheduledTransferPeriod.</span><span class="sxs-lookup"><span data-stu-id="f8495-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="f8495-253">Exemplos de saudação métricas especificadas na seção de performanceCounters Olá são coletadas a cada 15 segundos ou na taxa de amostragem Olá definido explicitamente para o contador de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-253">Samples of hello metrics specified in hello performanceCounters section are collected every 15 seconds or at hello sample rate explicitly defined for hello counter.</span></span> <span data-ttu-id="f8495-254">Se vários frequências de scheduledTransferPeriod aparecerem (como exemplo hello), cada agregação é calculada independentemente.</span><span class="sxs-lookup"><span data-stu-id="f8495-254">If multiple scheduledTransferPeriod frequencies appear (as in hello example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="f8495-255">performanceCounters</span><span class="sxs-lookup"><span data-stu-id="f8495-255">performanceCounters</span></span>

```json
"performanceCounters": {
    "sinks": "",
    "performanceCounterConfiguration": [
        {
            "type": "builtin",
            "class": "Processor",
            "counter": "PercentIdleTime",
            "counterSpecifier": "/builtin/Processor/PercentIdleTime",
            "condition": "IsAggregate=TRUE",
            "sampleRate": "PT15S",
            "unit": "Percent",
            "annotation": [
                {
                    "displayName" : "Aggregate CPU %idle time",
                    "locale" : "en-us"
                }
            ]
        }
    ]
}
```

<span data-ttu-id="f8495-256">Nesta seção opcional controla coleção Olá de métricas.</span><span class="sxs-lookup"><span data-stu-id="f8495-256">This optional section controls hello collection of metrics.</span></span> <span data-ttu-id="f8495-257">Exemplos processados são agregados para cada [scheduledTransferPeriod](#metrics) tooproduce estes valores:</span><span class="sxs-lookup"><span data-stu-id="f8495-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) tooproduce these values:</span></span>

* <span data-ttu-id="f8495-258">média</span><span class="sxs-lookup"><span data-stu-id="f8495-258">mean</span></span>
* <span data-ttu-id="f8495-259">mínimo</span><span class="sxs-lookup"><span data-stu-id="f8495-259">minimum</span></span>
* <span data-ttu-id="f8495-260">máximo</span><span class="sxs-lookup"><span data-stu-id="f8495-260">maximum</span></span>
* <span data-ttu-id="f8495-261">valor coletado por último</span><span class="sxs-lookup"><span data-stu-id="f8495-261">last-collected value</span></span>
* <span data-ttu-id="f8495-262">Contagem de amostras brutas usado agregação de saudação toocompute</span><span class="sxs-lookup"><span data-stu-id="f8495-262">count of raw samples used toocompute hello aggregate</span></span>

<span data-ttu-id="f8495-263">Elemento</span><span class="sxs-lookup"><span data-stu-id="f8495-263">Element</span></span> | <span data-ttu-id="f8495-264">Valor</span><span class="sxs-lookup"><span data-stu-id="f8495-264">Value</span></span>
------- | -----
<span data-ttu-id="f8495-265">coletores</span><span class="sxs-lookup"><span data-stu-id="f8495-265">sinks</span></span> | <span data-ttu-id="f8495-266">(opcional) Uma lista separada por vírgulas de nomes de Coletores toowhich que LAD envia resultados agregados de métrica.</span><span class="sxs-lookup"><span data-stu-id="f8495-266">(optional) A comma-separated list of names of sinks toowhich LAD sends aggregated metric results.</span></span> <span data-ttu-id="f8495-267">Todas as métricas agregadas são publicados tooeach listado coletor.</span><span class="sxs-lookup"><span data-stu-id="f8495-267">All aggregated metrics are published tooeach listed sink.</span></span> <span data-ttu-id="f8495-268">Veja [sinksConfig](#sinksconfig).</span><span class="sxs-lookup"><span data-stu-id="f8495-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="f8495-269">Exemplo: `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="f8495-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="f8495-270">type</span><span class="sxs-lookup"><span data-stu-id="f8495-270">type</span></span> | <span data-ttu-id="f8495-271">Identifica o provedor real de saudação da métrica de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-271">Identifies hello actual provider of hello metric.</span></span>
<span data-ttu-id="f8495-272">class</span><span class="sxs-lookup"><span data-stu-id="f8495-272">class</span></span> | <span data-ttu-id="f8495-273">Junto com "counter" identifica a métrica específica Olá no namespace do provedor de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-273">Together with "counter", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="f8495-274">contador</span><span class="sxs-lookup"><span data-stu-id="f8495-274">counter</span></span> | <span data-ttu-id="f8495-275">Junto com "classe", identifica a métrica específica Olá no namespace do provedor de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-275">Together with "class", identifies hello specific metric within hello provider's namespace.</span></span>
<span data-ttu-id="f8495-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="f8495-276">counterSpecifier</span></span> | <span data-ttu-id="f8495-277">Identifica a métrica específica Olá no namespace do Azure métricas hello.</span><span class="sxs-lookup"><span data-stu-id="f8495-277">Identifies hello specific metric within hello Azure Metrics namespace.</span></span>
<span data-ttu-id="f8495-278">condition</span><span class="sxs-lookup"><span data-stu-id="f8495-278">condition</span></span> | <span data-ttu-id="f8495-279">(opcional) Seleciona uma instância específica da métrica de Olá Olá objeto toowhich aplica ou selecionará Olá agregação em todas as instâncias do objeto.</span><span class="sxs-lookup"><span data-stu-id="f8495-279">(optional) Selects a specific instance of hello object toowhich hello metric applies or selects hello aggregation across all instances of that object.</span></span> <span data-ttu-id="f8495-280">Para obter mais informações, consulte Olá [ `builtin` definições de métrica](#metrics-supported-by-builtin).</span><span class="sxs-lookup"><span data-stu-id="f8495-280">For more information, see hello [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="f8495-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="f8495-281">sampleRate</span></span> | <span data-ttu-id="f8495-282">É o intervalo de 8601 que define Olá taxa na qual os exemplos brutos para esta métrica são coletados.</span><span class="sxs-lookup"><span data-stu-id="f8495-282">IS 8601 interval that sets hello rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="f8495-283">Se não estiver definida, o intervalo de coleta de saudação é definido pelo valor de saudação do [sampleRateInSeconds](#ladcfg).</span><span class="sxs-lookup"><span data-stu-id="f8495-283">If not set, hello collection interval is set by hello value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="f8495-284">taxa de amostra com suporte mais curta do Hello é 15 segundos (PT15S).</span><span class="sxs-lookup"><span data-stu-id="f8495-284">hello shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="f8495-285">unit</span><span class="sxs-lookup"><span data-stu-id="f8495-285">unit</span></span> | <span data-ttu-id="f8495-286">Deve ser uma destas cadeias de caracteres: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span><span class="sxs-lookup"><span data-stu-id="f8495-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="f8495-287">Define a unidade de saudação de métrica de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-287">Defines hello unit for hello metric.</span></span> <span data-ttu-id="f8495-288">Os consumidores de dados coletado de saudação esperam Olá coletados toomatch de valores de dados dessa unidade.</span><span class="sxs-lookup"><span data-stu-id="f8495-288">Consumers of hello collected data expect hello collected data values toomatch this unit.</span></span> <span data-ttu-id="f8495-289">O LAD ignora esse campo.</span><span class="sxs-lookup"><span data-stu-id="f8495-289">LAD ignores this field.</span></span>
<span data-ttu-id="f8495-290">displayName</span><span class="sxs-lookup"><span data-stu-id="f8495-290">displayName</span></span> | <span data-ttu-id="f8495-291">Olá rótulo (na linguagem de saudação especificado pela configuração da localidade Olá associado) toobe anexado toothis dados de métricas do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8495-291">hello label (in hello language specified by hello associated locale setting) toobe attached toothis data in Azure Metrics.</span></span> <span data-ttu-id="f8495-292">O LAD ignora esse campo.</span><span class="sxs-lookup"><span data-stu-id="f8495-292">LAD ignores this field.</span></span>

<span data-ttu-id="f8495-293">counterSpecifier Olá é um identificador arbitrário.</span><span class="sxs-lookup"><span data-stu-id="f8495-293">hello counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="f8495-294">Os consumidores de métricas, como Olá gráficos portal do Azure e alerta o recurso, usam counterSpecifier como hello "chave" que identifica uma métrica ou uma instância de uma métrica.</span><span class="sxs-lookup"><span data-stu-id="f8495-294">Consumers of metrics, like hello Azure portal charting and alerting feature, use counterSpecifier as hello "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="f8495-295">Para as métricas `builtin`, é recomendável usar valores counterSpecifier que começam com `/builtin/`.</span><span class="sxs-lookup"><span data-stu-id="f8495-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="f8495-296">Se você estiver coletando uma instância específica de uma métrica, recomendamos que você anexar o identificador de saudação do valor da saudação instância toohello counterSpecifier.</span><span class="sxs-lookup"><span data-stu-id="f8495-296">If you are collecting a specific instance of a metric, we recommend you attach hello identifier of hello instance toohello counterSpecifier value.</span></span> <span data-ttu-id="f8495-297">Alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="f8495-297">Some examples:</span></span>

* <span data-ttu-id="f8495-298">`/builtin/Processor/PercentIdleTime` – tempo ocioso médio de todos os núcleos</span><span class="sxs-lookup"><span data-stu-id="f8495-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="f8495-299">`/builtin/Disk/FreeSpace(/mnt)`-Espaço livre para o sistema de arquivos do hello /mnt</span><span class="sxs-lookup"><span data-stu-id="f8495-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for hello /mnt filesystem</span></span>
* <span data-ttu-id="f8495-300">`/builtin/Disk/FreeSpace` – espaço livre com a média de todos os sistemas de arquivos montados</span><span class="sxs-lookup"><span data-stu-id="f8495-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="f8495-301">Nem LAD nem Olá portal do Azure espera Olá counterSpecifier valor toomatch nenhum padrão.</span><span class="sxs-lookup"><span data-stu-id="f8495-301">Neither LAD nor hello Azure portal expects hello counterSpecifier value toomatch any pattern.</span></span> <span data-ttu-id="f8495-302">Seja consistente no modo como você constrói valores counterSpecifier.</span><span class="sxs-lookup"><span data-stu-id="f8495-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="f8495-303">Quando você especificar `performanceCounters`, LAD sempre cria a tabela de tooa de dados no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8495-303">When you specify `performanceCounters`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="f8495-304">Você pode ter Olá mesmo dados gravados tooJSON blobs e/ou Hubs de eventos, mas não é possível desabilitar tooa tabela de dados de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f8495-304">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="f8495-305">Todas as instâncias de toouse de extensão de diagnóstico configurado Olá Olá conta de armazenamento de mesmo nome e o ponto de extremidade adicionam toohello seus logs e métricas mesma tabela.</span><span class="sxs-lookup"><span data-stu-id="f8495-305">All instances of hello diagnostic extension configured toouse hello same storage account name and endpoint add their metrics and logs toohello same table.</span></span> <span data-ttu-id="f8495-306">Se estiver escrevendo um número excessivo de VMs toohello pode acelerar a mesma partição de tabela, o Azure grava toothat partição.</span><span class="sxs-lookup"><span data-stu-id="f8495-306">If too many VMs are writing toohello same table partition, Azure can throttle writes toothat partition.</span></span> <span data-ttu-id="f8495-307">Olá eventVolume configuração faz com que as entradas toobe espalhadas por 1 (pequeno), (médio) de 10 ou 100 (grande) diferentes partições.</span><span class="sxs-lookup"><span data-stu-id="f8495-307">hello eventVolume setting causes entries toobe spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="f8495-308">Geralmente, "Médio" é suficiente tooensure tráfego não é limitado.</span><span class="sxs-lookup"><span data-stu-id="f8495-308">Usually, "Medium" is sufficient tooensure traffic is not throttled.</span></span> <span data-ttu-id="f8495-309">recurso de métricas do Azure de saudação do hello portal do Azure usa dados de saudação nesta gráficos de tooproduce da tabela ou tootrigger alertas.</span><span class="sxs-lookup"><span data-stu-id="f8495-309">hello Azure Metrics feature of hello Azure portal uses hello data in this table tooproduce graphs or tootrigger alerts.</span></span> <span data-ttu-id="f8495-310">nome da tabela Olá é a concatenação de saudação dessas cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="f8495-310">hello table name is hello concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="f8495-311">Olá "scheduledTransferPeriod" hello agregados valores armazenados na tabela de saudação</span><span class="sxs-lookup"><span data-stu-id="f8495-311">hello "scheduledTransferPeriod" for hello aggregated values stored in hello table</span></span>
* `P10DV2S`
* <span data-ttu-id="f8495-312">Uma data, na forma de hello "AAAAMMDD", que altera a cada 10 dias</span><span class="sxs-lookup"><span data-stu-id="f8495-312">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="f8495-313">Os exemplos incluem `WADMetricsPT1HP10DV2S20170410` e `WADMetricsPT1MP10DV2S20170609`.</span><span class="sxs-lookup"><span data-stu-id="f8495-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="f8495-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="f8495-314">syslogEvents</span></span>

```json
"syslogEvents": {
    "sinks": "",
    "syslogEventConfiguration": {
        "facilityName1": "minSeverity",
        "facilityName2": "minSeverity",
        ...
    }
}
```

<span data-ttu-id="f8495-315">Nesta seção opcional controla a coleção de saudação de eventos de log de syslog.</span><span class="sxs-lookup"><span data-stu-id="f8495-315">This optional section controls hello collection of log events from syslog.</span></span> <span data-ttu-id="f8495-316">Se a seção de saudação for omitida, os eventos de syslog não são capturados em todos os.</span><span class="sxs-lookup"><span data-stu-id="f8495-316">If hello section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="f8495-317">a coleção de syslogEventConfiguration Olá tem uma entrada para cada recurso de syslog de interesse.</span><span class="sxs-lookup"><span data-stu-id="f8495-317">hello syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="f8495-318">Se minSeverity for "Nenhum" para um recurso específico, ou se o recurso não aparecerá no elemento de saudação, nenhum evento de recurso é capturado.</span><span class="sxs-lookup"><span data-stu-id="f8495-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in hello element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="f8495-319">Elemento</span><span class="sxs-lookup"><span data-stu-id="f8495-319">Element</span></span> | <span data-ttu-id="f8495-320">Valor</span><span class="sxs-lookup"><span data-stu-id="f8495-320">Value</span></span>
------- | -----
<span data-ttu-id="f8495-321">coletores</span><span class="sxs-lookup"><span data-stu-id="f8495-321">sinks</span></span> | <span data-ttu-id="f8495-322">Uma lista separada por vírgulas de nomes de Coletores de log individuais do toowhich eventos são publicados.</span><span class="sxs-lookup"><span data-stu-id="f8495-322">A comma-separated list of names of sinks toowhich individual log events are published.</span></span> <span data-ttu-id="f8495-323">Todos os eventos de log correspondentes restrições Olá syslogEventConfiguration são publicados tooeach listado coletor.</span><span class="sxs-lookup"><span data-stu-id="f8495-323">All log events matching hello restrictions in syslogEventConfiguration are published tooeach listed sink.</span></span> <span data-ttu-id="f8495-324">Exemplo: "EHforsyslog"</span><span class="sxs-lookup"><span data-stu-id="f8495-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="f8495-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="f8495-325">facilityName</span></span> | <span data-ttu-id="f8495-326">Um nome de recurso de syslog (como "LOG\_USER" ou "LOG\_LOCAL0").</span><span class="sxs-lookup"><span data-stu-id="f8495-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="f8495-327">Consulte a seção "recurso" Olá Olá [página syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) para a lista completa de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-327">See hello "facility" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span>
<span data-ttu-id="f8495-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="f8495-328">minSeverity</span></span> | <span data-ttu-id="f8495-329">Um nível de severidade de syslog (como "LOG\_ERR" ou "LOG\_INFO").</span><span class="sxs-lookup"><span data-stu-id="f8495-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="f8495-330">Consulte a seção "nível" Olá Olá [página syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) para a lista completa de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-330">See hello "level" section of hello [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for hello full list.</span></span> <span data-ttu-id="f8495-331">extensão de saudação captura eventos enviados toohello recurso em ou acima Olá especificado nível.</span><span class="sxs-lookup"><span data-stu-id="f8495-331">hello extension captures events sent toohello facility at or above hello specified level.</span></span>

<span data-ttu-id="f8495-332">Quando você especificar `syslogEvents`, LAD sempre cria a tabela de tooa de dados no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8495-332">When you specify `syslogEvents`, LAD always writes data tooa table in Azure storage.</span></span> <span data-ttu-id="f8495-333">Você pode ter Olá mesmo dados gravados tooJSON blobs e/ou Hubs de eventos, mas não é possível desabilitar tooa tabela de dados de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f8495-333">You can have hello same data written tooJSON blobs and/or Event Hubs, but you cannot disable storing data tooa table.</span></span> <span data-ttu-id="f8495-334">Olá comportamento para essa tabela de particionamento é Olá igual ao descrito para `performanceCounters`.</span><span class="sxs-lookup"><span data-stu-id="f8495-334">hello partitioning behavior for this table is hello same as described for `performanceCounters`.</span></span> <span data-ttu-id="f8495-335">nome da tabela Olá é a concatenação de saudação dessas cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="f8495-335">hello table name is hello concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="f8495-336">Uma data, na forma de hello "AAAAMMDD", que altera a cada 10 dias</span><span class="sxs-lookup"><span data-stu-id="f8495-336">A date, in hello form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="f8495-337">Os exemplos incluem `LinuxSyslog20170410` e `LinuxSyslog20170609`.</span><span class="sxs-lookup"><span data-stu-id="f8495-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="f8495-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="f8495-338">perfCfg</span></span>

<span data-ttu-id="f8495-339">Essa seção controla a execução de consultas [OMI](https://github.com/Microsoft/omi) arbitrárias.</span><span class="sxs-lookup"><span data-stu-id="f8495-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

```json
"perfCfg": [
    {
        "namespace": "root/scx",
        "query": "SELECT PercentAvailableMemory, PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
        "table": "LinuxOldMemory",
        "frequency": 300,
        "sinks": ""
    }
]
```

<span data-ttu-id="f8495-340">Elemento</span><span class="sxs-lookup"><span data-stu-id="f8495-340">Element</span></span> | <span data-ttu-id="f8495-341">Valor</span><span class="sxs-lookup"><span data-stu-id="f8495-341">Value</span></span>
------- | -----
<span data-ttu-id="f8495-342">namespace</span><span class="sxs-lookup"><span data-stu-id="f8495-342">namespace</span></span> | <span data-ttu-id="f8495-343">namespace OMI hello (opcional) no qual Olá consulta deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="f8495-343">(optional) hello OMI namespace within which hello query should be executed.</span></span> <span data-ttu-id="f8495-344">Se não for especificado, o valor de padrão de saudação é "raiz/scx", implementada por Olá [provedores de plataforma cruzada do System Center](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span><span class="sxs-lookup"><span data-stu-id="f8495-344">If unspecified, hello default value is "root/scx", implemented by hello [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="f8495-345">query</span><span class="sxs-lookup"><span data-stu-id="f8495-345">query</span></span> | <span data-ttu-id="f8495-346">Olá OMI toobe de consulta executada.</span><span class="sxs-lookup"><span data-stu-id="f8495-346">hello OMI query toobe executed.</span></span>
<span data-ttu-id="f8495-347">tabela</span><span class="sxs-lookup"><span data-stu-id="f8495-347">table</span></span> | <span data-ttu-id="f8495-348">tabela de armazenamento do Azure hello (opcional), em Olá designado a conta de armazenamento (consulte [protegido configurações](#protected-settings)).</span><span class="sxs-lookup"><span data-stu-id="f8495-348">(optional) hello Azure storage table, in hello designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="f8495-349">frequência</span><span class="sxs-lookup"><span data-stu-id="f8495-349">frequency</span></span> | <span data-ttu-id="f8495-350">número de saudação (opcional) de segundos entre a execução da consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8495-350">(optional) hello number of seconds between execution of hello query.</span></span> <span data-ttu-id="f8495-351">O valor padrão é 300 (5 minutos); o valor mínimo é de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="f8495-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="f8495-352">coletores</span><span class="sxs-lookup"><span data-stu-id="f8495-352">sinks</span></span> | <span data-ttu-id="f8495-353">(opcional) Uma lista separada por vírgulas de nomes de resultados de métricas adicionais coletores toowhich exemplo bruto deve ser publicada.</span><span class="sxs-lookup"><span data-stu-id="f8495-353">(optional) A comma-separated list of names of additional sinks toowhich raw sample metric results should be published.</span></span> <span data-ttu-id="f8495-354">Nenhuma agregação desses exemplos bruto é calculada pela extensão de saudação ou pelas métricas do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8495-354">No aggregation of these raw samples is computed by hello extension or by Azure Metrics.</span></span>

<span data-ttu-id="f8495-355">As informações de "tabela" ou "coletores" ou de ambos devem ser especificadas.</span><span class="sxs-lookup"><span data-stu-id="f8495-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="f8495-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="f8495-356">fileLogs</span></span>

<span data-ttu-id="f8495-357">Saudação de controles de captura de arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="f8495-357">Controls hello capture of log files.</span></span> <span data-ttu-id="f8495-358">LAD captura novas linhas de texto, como eles são gravados toohello arquivo e grava linhas tootable e/ou qualquer coletores especificados (JsonBlob ou EventHub).</span><span class="sxs-lookup"><span data-stu-id="f8495-358">LAD captures new text lines as they are written toohello file and writes them tootable rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="f8495-359">Elemento</span><span class="sxs-lookup"><span data-stu-id="f8495-359">Element</span></span> | <span data-ttu-id="f8495-360">Valor</span><span class="sxs-lookup"><span data-stu-id="f8495-360">Value</span></span>
------- | -----
<span data-ttu-id="f8495-361">file</span><span class="sxs-lookup"><span data-stu-id="f8495-361">file</span></span> | <span data-ttu-id="f8495-362">nome de caminho completo de toobe de arquivo de log Olá Olá observados e capturados.</span><span class="sxs-lookup"><span data-stu-id="f8495-362">hello full pathname of hello log file toobe watched and captured.</span></span> <span data-ttu-id="f8495-363">Olá pathname deve nomear um único arquivo; ele não é possível nomear um diretório ou conter curingas.</span><span class="sxs-lookup"><span data-stu-id="f8495-363">hello pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="f8495-364">tabela</span><span class="sxs-lookup"><span data-stu-id="f8495-364">table</span></span> | <span data-ttu-id="f8495-365">tabela de armazenamento do Azure hello (opcional), no armazenamento de saudação designado conta (conforme especificado na configuração de saudação protegida), na qual novas linhas de saudação "final" do arquivo hello é gravados.</span><span class="sxs-lookup"><span data-stu-id="f8495-365">(optional) hello Azure storage table, in hello designated storage account (as specified in hello protected configuration), into which new lines from hello "tail" of hello file are written.</span></span>
<span data-ttu-id="f8495-366">coletores</span><span class="sxs-lookup"><span data-stu-id="f8495-366">sinks</span></span> | <span data-ttu-id="f8495-367">(opcional) Uma lista separada por vírgulas de nomes de Coletores adicionais toowhich log linhas enviadas.</span><span class="sxs-lookup"><span data-stu-id="f8495-367">(optional) A comma-separated list of names of additional sinks toowhich log lines sent.</span></span>

<span data-ttu-id="f8495-368">As informações de "tabela" ou "coletores" ou de ambos devem ser especificadas.</span><span class="sxs-lookup"><span data-stu-id="f8495-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-hello-builtin-provider"></a><span data-ttu-id="f8495-369">Métricas suportadas pelo provedor de builtin Olá</span><span class="sxs-lookup"><span data-stu-id="f8495-369">Metrics supported by hello builtin provider</span></span>

<span data-ttu-id="f8495-370">provedor de métrica de builtin Olá é uma origem de métricas mais interessantes tooa amplo conjunto de usuários.</span><span class="sxs-lookup"><span data-stu-id="f8495-370">hello builtin metric provider is a source of metrics most interesting tooa broad set of users.</span></span> <span data-ttu-id="f8495-371">Essas métricas enquadram-se em cinco classes amplas:</span><span class="sxs-lookup"><span data-stu-id="f8495-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="f8495-372">Processador</span><span class="sxs-lookup"><span data-stu-id="f8495-372">Processor</span></span>
* <span data-ttu-id="f8495-373">Memória</span><span class="sxs-lookup"><span data-stu-id="f8495-373">Memory</span></span>
* <span data-ttu-id="f8495-374">Rede</span><span class="sxs-lookup"><span data-stu-id="f8495-374">Network</span></span>
* <span data-ttu-id="f8495-375">Filesystem</span><span class="sxs-lookup"><span data-stu-id="f8495-375">Filesystem</span></span>
* <span data-ttu-id="f8495-376">Disco</span><span class="sxs-lookup"><span data-stu-id="f8495-376">Disk</span></span>

### <a name="builtin-metrics-for-hello-processor-class"></a><span data-ttu-id="f8495-377">métricas de Builtin para Olá classe do processador</span><span class="sxs-lookup"><span data-stu-id="f8495-377">builtin metrics for hello Processor class</span></span>

<span data-ttu-id="f8495-378">Olá classe processador de métricas fornece informações sobre o uso do processador em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="f8495-378">hello Processor class of metrics provides information about processor usage in hello VM.</span></span> <span data-ttu-id="f8495-379">Ao agregar porcentagens, o resultado de saudação é média Olá em todas as CPUs.</span><span class="sxs-lookup"><span data-stu-id="f8495-379">When aggregating percentages, hello result is hello average across all CPUs.</span></span> <span data-ttu-id="f8495-380">Em uma máquina virtual de núcleos dois, se um núcleo 100% ocupado e outros Olá era 100% ocioso, Olá relatado que percentidletime seria 50.</span><span class="sxs-lookup"><span data-stu-id="f8495-380">In a two core VM, if one core was 100% busy and hello other was 100% idle, hello reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="f8495-381">Se cada núcleo foi 50% de disponibilidade para Olá mesmo período, Olá relatou o resultado também seria 50.</span><span class="sxs-lookup"><span data-stu-id="f8495-381">If each core was 50% busy for hello same period, hello reported result would also be 50.</span></span> <span data-ttu-id="f8495-382">Em um núcleo quatro VM, com 100% de um núcleo ocupado e Olá outros ocioso, Olá relatado que percentidletime seria 75.</span><span class="sxs-lookup"><span data-stu-id="f8495-382">In a four core VM, with one core 100% busy and hello others idle, hello reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="f8495-383">contador</span><span class="sxs-lookup"><span data-stu-id="f8495-383">counter</span></span> | <span data-ttu-id="f8495-384">Significado</span><span class="sxs-lookup"><span data-stu-id="f8495-384">Meaning</span></span>
------- | -------
<span data-ttu-id="f8495-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="f8495-385">PercentIdleTime</span></span> | <span data-ttu-id="f8495-386">Porcentagem de tempo durante a janela de agregação de saudação que processadores estavam executando loop ocioso do kernel Olá</span><span class="sxs-lookup"><span data-stu-id="f8495-386">Percentage of time during hello aggregation window that processors were executing hello kernel idle loop</span></span>
<span data-ttu-id="f8495-387">PercentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="f8495-387">PercentProcessorTime</span></span> | <span data-ttu-id="f8495-388">Porcentagem de tempo de execução de um thread não ocioso</span><span class="sxs-lookup"><span data-stu-id="f8495-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="f8495-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="f8495-389">PercentIOWaitTime</span></span> | <span data-ttu-id="f8495-390">Porcentagem de tempo de espera para toocomplete de operações de e/s</span><span class="sxs-lookup"><span data-stu-id="f8495-390">Percentage of time waiting for IO operations toocomplete</span></span>
<span data-ttu-id="f8495-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="f8495-391">PercentInterruptTime</span></span> | <span data-ttu-id="f8495-392">Porcentagem de tempo de execução de interrupções de hardware/software e DPCs (chamadas de procedimento deferidas)</span><span class="sxs-lookup"><span data-stu-id="f8495-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="f8495-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="f8495-393">PercentUserTime</span></span> | <span data-ttu-id="f8495-394">De tempo não-ocioso durante a janela de agregação hello, porcentagem de saudação do tempo gasto no usuário mais em prioridade normal</span><span class="sxs-lookup"><span data-stu-id="f8495-394">Of non-idle time during hello aggregation window, hello percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="f8495-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="f8495-395">PercentNiceTime</span></span> | <span data-ttu-id="f8495-396">Tempo não-ocioso, Olá porcentagem gasta em baixa prioridade (BOM)</span><span class="sxs-lookup"><span data-stu-id="f8495-396">Of non-idle time, hello percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="f8495-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="f8495-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="f8495-398">Tempo não-ocioso, Olá porcentagem gasta em modo privilegiado (kernel)</span><span class="sxs-lookup"><span data-stu-id="f8495-398">Of non-idle time, hello percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="f8495-399">Olá primeiro quatro contadores devem ser somadas too100%.</span><span class="sxs-lookup"><span data-stu-id="f8495-399">hello first four counters should sum too100%.</span></span> <span data-ttu-id="f8495-400">Olá última três contadores também soma too100%; eles subdividir a soma de saudação do PercentProcessorTime, PercentIOWaitTime e PercentInterruptTime.</span><span class="sxs-lookup"><span data-stu-id="f8495-400">hello last three counters also sum too100%; they subdivide hello sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="f8495-401">tooobtain uma única métrica agregada para todos os processadores, defina `"condition": "IsAggregate=TRUE"`.</span><span class="sxs-lookup"><span data-stu-id="f8495-401">tooobtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="f8495-402">tooobtain uma métrica para um processador específico, como o segundo processador lógico saudação de um quatro principais VM, defina `"condition": "Name=\\"1\\""`.</span><span class="sxs-lookup"><span data-stu-id="f8495-402">tooobtain a metric for a specific processor, such as hello second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="f8495-403">Número de processadores lógicos está no intervalo de saudação `[0..n-1]`.</span><span class="sxs-lookup"><span data-stu-id="f8495-403">Logical processor numbers are in hello range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-hello-memory-class"></a><span data-ttu-id="f8495-404">métricas de Builtin para Olá classe de memória</span><span class="sxs-lookup"><span data-stu-id="f8495-404">builtin metrics for hello Memory class</span></span>

<span data-ttu-id="f8495-405">Olá classe memória das métricas fornece informações sobre utilização de memória, paginação e troca.</span><span class="sxs-lookup"><span data-stu-id="f8495-405">hello Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="f8495-406">contador</span><span class="sxs-lookup"><span data-stu-id="f8495-406">counter</span></span> | <span data-ttu-id="f8495-407">Significado</span><span class="sxs-lookup"><span data-stu-id="f8495-407">Meaning</span></span>
------- | -------
<span data-ttu-id="f8495-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="f8495-408">AvailableMemory</span></span> | <span data-ttu-id="f8495-409">Memória física disponível em MiB</span><span class="sxs-lookup"><span data-stu-id="f8495-409">Available physical memory in MiB</span></span>
<span data-ttu-id="f8495-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="f8495-410">PercentAvailableMemory</span></span> | <span data-ttu-id="f8495-411">Memória física disponível como uma porcentagem da memória total</span><span class="sxs-lookup"><span data-stu-id="f8495-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="f8495-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="f8495-412">UsedMemory</span></span> | <span data-ttu-id="f8495-413">Memória física em uso (MiB)</span><span class="sxs-lookup"><span data-stu-id="f8495-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="f8495-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="f8495-414">PercentUsedMemory</span></span> | <span data-ttu-id="f8495-415">Memória física em uso como uma porcentagem da memória total</span><span class="sxs-lookup"><span data-stu-id="f8495-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="f8495-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="f8495-416">PagesPerSec</span></span> | <span data-ttu-id="f8495-417">Paginação total (leitura/gravação)</span><span class="sxs-lookup"><span data-stu-id="f8495-417">Total paging (read/write)</span></span>
<span data-ttu-id="f8495-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="f8495-418">PagesReadPerSec</span></span> | <span data-ttu-id="f8495-419">Páginas lidas do repositório de backup (arquivo de permuta, arquivo de programa, arquivo mapeado etc.)</span><span class="sxs-lookup"><span data-stu-id="f8495-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="f8495-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="f8495-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="f8495-421">Páginas escritas toobacking armazenam (arquivo de permuta, arquivo mapeado, etc.)</span><span class="sxs-lookup"><span data-stu-id="f8495-421">Pages written toobacking store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="f8495-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="f8495-422">AvailableSwap</span></span> | <span data-ttu-id="f8495-423">Espaço de permuta não utilizado (MiB)</span><span class="sxs-lookup"><span data-stu-id="f8495-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="f8495-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="f8495-424">PercentAvailableSwap</span></span> | <span data-ttu-id="f8495-425">Espaço de troca não utilizado como uma porcentagem da troca total</span><span class="sxs-lookup"><span data-stu-id="f8495-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="f8495-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="f8495-426">UsedSwap</span></span> | <span data-ttu-id="f8495-427">Espaço de troca em uso (MiB)</span><span class="sxs-lookup"><span data-stu-id="f8495-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="f8495-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="f8495-428">PercentUsedSwap</span></span> | <span data-ttu-id="f8495-429">Espaço de troca em uso como uma porcentagem da troca total</span><span class="sxs-lookup"><span data-stu-id="f8495-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="f8495-430">Essa classe de métricas tem apenas uma única instância.</span><span class="sxs-lookup"><span data-stu-id="f8495-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="f8495-431">atributo de "condição" Hello não úteis de configurações e deve ser omitido.</span><span class="sxs-lookup"><span data-stu-id="f8495-431">hello "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-hello-network-class"></a><span data-ttu-id="f8495-432">métricas de Builtin para Olá classe da rede</span><span class="sxs-lookup"><span data-stu-id="f8495-432">builtin metrics for hello Network class</span></span>

<span data-ttu-id="f8495-433">Olá classe de métricas de rede fornece informações sobre atividade de rede em um interfaces de rede individuais desde a inicialização.</span><span class="sxs-lookup"><span data-stu-id="f8495-433">hello Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="f8495-434">O LAD não expõe as métricas de largura de banda, que podem ser recuperadas de métricas de host.</span><span class="sxs-lookup"><span data-stu-id="f8495-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="f8495-435">contador</span><span class="sxs-lookup"><span data-stu-id="f8495-435">counter</span></span> | <span data-ttu-id="f8495-436">Significado</span><span class="sxs-lookup"><span data-stu-id="f8495-436">Meaning</span></span>
------- | -------
<span data-ttu-id="f8495-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="f8495-437">BytesTransmitted</span></span> | <span data-ttu-id="f8495-438">Total de bytes enviados desde a inicialização</span><span class="sxs-lookup"><span data-stu-id="f8495-438">Total bytes sent since boot</span></span>
<span data-ttu-id="f8495-439">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="f8495-439">BytesReceived</span></span> | <span data-ttu-id="f8495-440">Total de bytes recebidos desde a inicialização</span><span class="sxs-lookup"><span data-stu-id="f8495-440">Total bytes received since boot</span></span>
<span data-ttu-id="f8495-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="f8495-441">BytesTotal</span></span> | <span data-ttu-id="f8495-442">Total de bytes enviados ou recebidos desde a inicialização</span><span class="sxs-lookup"><span data-stu-id="f8495-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="f8495-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="f8495-443">PacketsTransmitted</span></span> | <span data-ttu-id="f8495-444">Total de pacotes enviados desde a inicialização</span><span class="sxs-lookup"><span data-stu-id="f8495-444">Total packets sent since boot</span></span>
<span data-ttu-id="f8495-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="f8495-445">PacketsReceived</span></span> | <span data-ttu-id="f8495-446">Total de pacotes recebidos desde a inicialização</span><span class="sxs-lookup"><span data-stu-id="f8495-446">Total packets received since boot</span></span>
<span data-ttu-id="f8495-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="f8495-447">TotalRxErrors</span></span> | <span data-ttu-id="f8495-448">Número de erros de recebimento desde a inicialização</span><span class="sxs-lookup"><span data-stu-id="f8495-448">Number of receive errors since boot</span></span>
<span data-ttu-id="f8495-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="f8495-449">TotalTxErrors</span></span> | <span data-ttu-id="f8495-450">Número de erros de transmissão desde a inicialização</span><span class="sxs-lookup"><span data-stu-id="f8495-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="f8495-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="f8495-451">TotalCollisions</span></span> | <span data-ttu-id="f8495-452">Número de relatados pelas portas de rede Olá desde a inicialização</span><span class="sxs-lookup"><span data-stu-id="f8495-452">Number of collisions reported by hello network ports since boot</span></span>

 <span data-ttu-id="f8495-453">Embora essa classe seja instanciada, o LAD não oferece suporte à captura de métricas Network agregadas em todos os dispositivos de rede.</span><span class="sxs-lookup"><span data-stu-id="f8495-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="f8495-454">conjunto de métricas de saudação tooobtain para uma interface específica, como eth0, `"condition": "InstanceID=\\"eth0\\""`.</span><span class="sxs-lookup"><span data-stu-id="f8495-454">tooobtain hello metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-hello-filesystem-class"></a><span data-ttu-id="f8495-455">métricas de Builtin para Olá classe do sistema de arquivos</span><span class="sxs-lookup"><span data-stu-id="f8495-455">builtin metrics for hello Filesystem class</span></span>

<span data-ttu-id="f8495-456">Olá classe de sistema de arquivos de métricas fornece informações sobre o uso do sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="f8495-456">hello Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="f8495-457">Valores absolutos e porcentagem são relatados como seriam exibidos tooan usuário comum (não raiz).</span><span class="sxs-lookup"><span data-stu-id="f8495-457">Absolute and percentage values are reported as they'd be displayed tooan ordinary user (not root).</span></span>

<span data-ttu-id="f8495-458">contador</span><span class="sxs-lookup"><span data-stu-id="f8495-458">counter</span></span> | <span data-ttu-id="f8495-459">Significado</span><span class="sxs-lookup"><span data-stu-id="f8495-459">Meaning</span></span>
------- | -------
<span data-ttu-id="f8495-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="f8495-460">FreeSpace</span></span> | <span data-ttu-id="f8495-461">Espaço em disco disponível em bytes</span><span class="sxs-lookup"><span data-stu-id="f8495-461">Available disk space in bytes</span></span>
<span data-ttu-id="f8495-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="f8495-462">UsedSpace</span></span> | <span data-ttu-id="f8495-463">Espaço em disco usado em bytes</span><span class="sxs-lookup"><span data-stu-id="f8495-463">Used disk space in bytes</span></span>
<span data-ttu-id="f8495-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="f8495-464">PercentFreeSpace</span></span> | <span data-ttu-id="f8495-465">Porcentagem de espaço livre</span><span class="sxs-lookup"><span data-stu-id="f8495-465">Percentage free space</span></span>
<span data-ttu-id="f8495-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="f8495-466">PercentUsedSpace</span></span> | <span data-ttu-id="f8495-467">Porcentagem de espaço usado</span><span class="sxs-lookup"><span data-stu-id="f8495-467">Percentage used space</span></span>
<span data-ttu-id="f8495-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="f8495-468">PercentFreeInodes</span></span> | <span data-ttu-id="f8495-469">Porcentagem de inodes não utilizados</span><span class="sxs-lookup"><span data-stu-id="f8495-469">Percentage of unused inodes</span></span>
<span data-ttu-id="f8495-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="f8495-470">PercentUsedInodes</span></span> | <span data-ttu-id="f8495-471">Porcentagem de inodes alocados (em uso) somados em todos os sistemas de arquivos</span><span class="sxs-lookup"><span data-stu-id="f8495-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="f8495-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="f8495-472">BytesReadPerSecond</span></span> | <span data-ttu-id="f8495-473">Bytes lidos por segundo</span><span class="sxs-lookup"><span data-stu-id="f8495-473">Bytes read per second</span></span>
<span data-ttu-id="f8495-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="f8495-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="f8495-475">Bytes gravados por segundo</span><span class="sxs-lookup"><span data-stu-id="f8495-475">Bytes written per second</span></span>
<span data-ttu-id="f8495-476">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="f8495-476">BytesPerSecond</span></span> | <span data-ttu-id="f8495-477">Bytes lido ou gravados por segundo</span><span class="sxs-lookup"><span data-stu-id="f8495-477">Bytes read or written per second</span></span>
<span data-ttu-id="f8495-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="f8495-478">ReadsPerSecond</span></span> | <span data-ttu-id="f8495-479">Operações de leitura por segundo</span><span class="sxs-lookup"><span data-stu-id="f8495-479">Read operations per second</span></span>
<span data-ttu-id="f8495-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="f8495-480">WritesPerSecond</span></span> | <span data-ttu-id="f8495-481">Operações de gravação por segundo</span><span class="sxs-lookup"><span data-stu-id="f8495-481">Write operations per second</span></span>
<span data-ttu-id="f8495-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="f8495-482">TransfersPerSecond</span></span> | <span data-ttu-id="f8495-483">Operações de leitura ou gravação por segundo</span><span class="sxs-lookup"><span data-stu-id="f8495-483">Read or write operations per second</span></span>

<span data-ttu-id="f8495-484">Os valores agregados em todos os sistemas de arquivo podem ser obtidos pela configuração `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="f8495-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="f8495-485">Os valores para um sistema de arquivos montado específico, como "/mnt", podem ser obtidos pela configuração `"condition": 'Name="/mnt"'`.</span><span class="sxs-lookup"><span data-stu-id="f8495-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-hello-disk-class"></a><span data-ttu-id="f8495-486">métricas de Builtin para Olá classe disco</span><span class="sxs-lookup"><span data-stu-id="f8495-486">builtin metrics for hello Disk class</span></span>

<span data-ttu-id="f8495-487">Olá classe disco das métricas fornece informações sobre o uso do dispositivo de disco.</span><span class="sxs-lookup"><span data-stu-id="f8495-487">hello Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="f8495-488">Essas estatísticas se aplicam a toda a unidade toohello.</span><span class="sxs-lookup"><span data-stu-id="f8495-488">These statistics apply toohello entire drive.</span></span> <span data-ttu-id="f8495-489">Se houver vários sistemas de arquivos em um dispositivo, Olá contadores para o dispositivo são, na verdade, agregados em todos eles.</span><span class="sxs-lookup"><span data-stu-id="f8495-489">If there are multiple file systems on a device, hello counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="f8495-490">contador</span><span class="sxs-lookup"><span data-stu-id="f8495-490">counter</span></span> | <span data-ttu-id="f8495-491">Significado</span><span class="sxs-lookup"><span data-stu-id="f8495-491">Meaning</span></span>
------- | -------
<span data-ttu-id="f8495-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="f8495-492">ReadsPerSecond</span></span> | <span data-ttu-id="f8495-493">Operações de leitura por segundo</span><span class="sxs-lookup"><span data-stu-id="f8495-493">Read operations per second</span></span>
<span data-ttu-id="f8495-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="f8495-494">WritesPerSecond</span></span> | <span data-ttu-id="f8495-495">Operações de gravação por segundo</span><span class="sxs-lookup"><span data-stu-id="f8495-495">Write operations per second</span></span>
<span data-ttu-id="f8495-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="f8495-496">TransfersPerSecond</span></span> | <span data-ttu-id="f8495-497">Operações totais por segundo</span><span class="sxs-lookup"><span data-stu-id="f8495-497">Total operations per second</span></span>
<span data-ttu-id="f8495-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="f8495-498">AverageReadTime</span></span> | <span data-ttu-id="f8495-499">Média de segundos por operação de leitura</span><span class="sxs-lookup"><span data-stu-id="f8495-499">Average seconds per read operation</span></span>
<span data-ttu-id="f8495-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="f8495-500">AverageWriteTime</span></span> | <span data-ttu-id="f8495-501">Média de segundos por operação de gravação</span><span class="sxs-lookup"><span data-stu-id="f8495-501">Average seconds per write operation</span></span>
<span data-ttu-id="f8495-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="f8495-502">AverageTransferTime</span></span> | <span data-ttu-id="f8495-503">Média de segundos por operação</span><span class="sxs-lookup"><span data-stu-id="f8495-503">Average seconds per operation</span></span>
<span data-ttu-id="f8495-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="f8495-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="f8495-505">Número médio de operações de disco enfileiradas</span><span class="sxs-lookup"><span data-stu-id="f8495-505">Average number of queued disk operations</span></span>
<span data-ttu-id="f8495-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="f8495-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="f8495-507">Número de bytes lidos por segundo</span><span class="sxs-lookup"><span data-stu-id="f8495-507">Number of bytes read per second</span></span>
<span data-ttu-id="f8495-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="f8495-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="f8495-509">Número de bytes gravados por segundo</span><span class="sxs-lookup"><span data-stu-id="f8495-509">Number of bytes written per second</span></span>
<span data-ttu-id="f8495-510">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="f8495-510">BytesPerSecond</span></span> | <span data-ttu-id="f8495-511">Número de bytes lidos ou gravados por segundo</span><span class="sxs-lookup"><span data-stu-id="f8495-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="f8495-512">Os valores agregados em todos os discos podem ser obtidos pela configuração `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="f8495-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="f8495-513">tooget informações para um dispositivo específico (por exemplo, / desenvolvimento/sdf1), definir `"condition": "Name=\\"/dev/sdf1\\""`.</span><span class="sxs-lookup"><span data-stu-id="f8495-513">tooget information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="f8495-514">Instalação e configuração do LAD 3.0 via CLI</span><span class="sxs-lookup"><span data-stu-id="f8495-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="f8495-515">Supondo que as configurações protegidas estão no arquivo hello Privateconfig e suas informações de configuração pública estão em PublicConfig.json, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="f8495-515">Assuming your protected settings are in hello file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="f8495-516">comando Olá pressupõe que você esteja usando o modo de gerenciamento de recursos do Azure hello (arm) do hello CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8495-516">hello command assumes you are using hello Azure Resource Management mode (arm) of hello Azure CLI.</span></span> <span data-ttu-id="f8495-517">tooconfigure LAD para implantação clássica do modelo de VMs (ASM), alternar muito "asm" modo (`azure config mode asm`) e omitir o nome do grupo de recursos Olá no comando hello.</span><span class="sxs-lookup"><span data-stu-id="f8495-517">tooconfigure LAD for classic deployment model (ASM) VMs, switch too"asm" mode (`azure config mode asm`) and omit hello resource group name in hello command.</span></span> <span data-ttu-id="f8495-518">Para obter mais informações, consulte Olá [documentação da CLI de plataforma cruzada](https://docs.microsoft.com/azure/xplat-cli-connect).</span><span class="sxs-lookup"><span data-stu-id="f8495-518">For more information, see hello [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="f8495-519">Uma configuração de exemplo do LAD 3.0</span><span class="sxs-lookup"><span data-stu-id="f8495-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="f8495-520">Com base em Olá anterior definições, aqui um exemplo de configuração de extensão de LAD 3.0 com alguma explicação.</span><span class="sxs-lookup"><span data-stu-id="f8495-520">Based on hello preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="f8495-521">tooapply caso de tooyour neste exemplo, você deve usar seu próprio nome de conta de armazenamento, conta token SAS e tokens EventHubs SAS.</span><span class="sxs-lookup"><span data-stu-id="f8495-521">tooapply this sample tooyour case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="f8495-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="f8495-522">PrivateConfig.json</span></span>

<span data-ttu-id="f8495-523">Essas configurações privadas definem os parâmetros de:</span><span class="sxs-lookup"><span data-stu-id="f8495-523">These private settings configure:</span></span>

* <span data-ttu-id="f8495-524">uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f8495-524">a storage account</span></span>
* <span data-ttu-id="f8495-525">um token de SAS de conta correspondente</span><span class="sxs-lookup"><span data-stu-id="f8495-525">a matching account SAS token</span></span>
* <span data-ttu-id="f8495-526">vários coletores (JsonBlob ou EventHubs com tokens de SAS)</span><span class="sxs-lookup"><span data-stu-id="f8495-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

```json
{
  "storageAccountName": "yourdiagstgacct",
  "storageAccountSasToken": "sv=xxxx-xx-xx&ss=bt&srt=co&sp=wlacu&st=yyyy-yy-yyT21%3A22%3A00Z&se=zzzz-zz-zzT21%3A22%3A00Z&sig=fake_signature",
  "sinksConfig": {
    "sink": [
      {
        "name": "SyslogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "FilelogJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuJsonBlob",
        "type": "JsonBlob"
      },
      {
        "name": "MyJsonMetricsBlob",
        "type": "JsonBlob"
      },
      {
        "name": "LinuxCpuEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=fake_signature&se=1808096361&skn=yourehpolicy"
      },
      {
        "name": "MyMetricEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&skn=yourehpolicy"
      },
      {
        "name": "LoggingEventHub",
        "type": "EventHub",
        "sasURL": "https://youreventhubnamespace.servicebus.windows.net/youreventhubpublisher?sr=https%3a%2f%2fyoureventhubnamespace.servicebus.windows.net%2fyoureventhubpublisher%2f&sig=yourehpolicy&se=1808096361&skn=yourehpolicy"
      }
    ]
  }
}
```

### <a name="publicconfigjson"></a><span data-ttu-id="f8495-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="f8495-527">PublicConfig.json</span></span>

<span data-ttu-id="f8495-528">Essas configurações públicas fazem o LAD:</span><span class="sxs-lookup"><span data-stu-id="f8495-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="f8495-529">Carregar métricas % tempo de processador e espaço em disco usado toohello `WADMetrics*` tabela</span><span class="sxs-lookup"><span data-stu-id="f8495-529">Upload percent-processor-time and used-disk-space metrics toohello `WADMetrics*` table</span></span>
* <span data-ttu-id="f8495-530">Carregue as mensagens de syslog recurso "usuário" e gravidade "info" toohello `LinuxSyslog*` tabela</span><span class="sxs-lookup"><span data-stu-id="f8495-530">Upload messages from syslog facility "user" and severity "info" toohello `LinuxSyslog*` table</span></span>
* <span data-ttu-id="f8495-531">Carregar bruto OMI consulta resultados (PercentProcessorTime e PercentIdleTime) toohello chamado `LinuxCPU` tabela</span><span class="sxs-lookup"><span data-stu-id="f8495-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) toohello named `LinuxCPU` table</span></span>
* <span data-ttu-id="f8495-532">Carregar acrescentadas linhas no arquivo `/var/log/myladtestlog` toohello `MyLadTestLog` tabela</span><span class="sxs-lookup"><span data-stu-id="f8495-532">Upload appended lines in file `/var/log/myladtestlog` toohello `MyLadTestLog` table</span></span>

<span data-ttu-id="f8495-533">Em cada caso, os dados também são carregados para:</span><span class="sxs-lookup"><span data-stu-id="f8495-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="f8495-534">Armazenamento de BLOBs do Azure (nome do contêiner é conforme definido no coletor de JsonBlob Olá)</span><span class="sxs-lookup"><span data-stu-id="f8495-534">Azure Blob storage (container name is as defined in hello JsonBlob sink)</span></span>
* <span data-ttu-id="f8495-535">Ponto de extremidade EventHubs (conforme especificado no coletor de EventHubs Olá)</span><span class="sxs-lookup"><span data-stu-id="f8495-535">EventHubs endpoint (as specified in hello EventHubs sink)</span></span>

```json
{
  "StorageAccount": "yourdiagstgacct",
  "sampleRateInSeconds": 15,
  "ladCfg": {
    "diagnosticMonitorConfiguration": {
      "performanceCounters": {
        "sinks": "MyMetricEventHub,MyJsonMetricsBlob",
        "performanceCounterConfiguration": [
          {
            "unit": "Percent",
            "type": "builtin",
            "counter": "PercentProcessorTime",
            "counterSpecifier": "/builtin/Processor/PercentProcessorTime",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Aggregate CPU %utilization"
              }
            ],
            "condition": "IsAggregate=TRUE",
            "class": "Processor"
          },
          {
            "unit": "Bytes",
            "type": "builtin",
            "counter": "UsedSpace",
            "counterSpecifier": "/builtin/FileSystem/UsedSpace",
            "annotation": [
              {
                "locale": "en-us",
                "displayName": "Used disk space on /"
              }
            ],
            "condition": "Name=\"/\"",
            "class": "Filesystem"
          }
        ]
      },
      "metrics": {
        "metricAggregation": [
          {
            "scheduledTransferPeriod": "PT1H"
          },
          {
            "scheduledTransferPeriod": "PT1M"
          }
        ],
        "resourceId": "/subscriptions/your_azure_subscription_id/resourceGroups/your_resource_group_name/providers/Microsoft.Compute/virtualMachines/your_vm_name"
      },
      "eventVolume": "Large",
      "syslogEvents": {
        "sinks": "SyslogJsonBlob,LoggingEventHub",
        "syslogEventConfiguration": {
          "LOG_USER": "LOG_INFO"
        }
      }
    }
  },
  "perfCfg": [
    {
      "query": "SELECT PercentProcessorTime, PercentIdleTime FROM SCX_ProcessorStatisticalInformation WHERE Name='_TOTAL'",
      "table": "LinuxCpu",
      "frequency": 60,
      "sinks": "LinuxCpuJsonBlob,LinuxCpuEventHub"
    }
  ],
  "fileLogs": [
    {
      "file": "/var/log/myladtestlog",
      "table": "MyLadTestLog",
      "sinks": "FilelogJsonBlob,LoggingEventHub"
    }
  ]
}
```

<span data-ttu-id="f8495-536">Olá `resourceId` em Olá configuração deve corresponder ao que de escala de máquina virtual VM ou Olá Olá definido.</span><span class="sxs-lookup"><span data-stu-id="f8495-536">hello `resourceId` in hello configuration must match that of hello VM or hello virtual machine scale set.</span></span>

* <span data-ttu-id="f8495-537">Métricas de plataforma Windows Azure, gráficos e alertas sabe resourceId Olá de saudação VM que você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="f8495-537">Azure platform metrics charting and alerting knows hello resourceId of hello VM you're working on.</span></span> <span data-ttu-id="f8495-538">Ele espera dados de saudação toofind para sua VM usando a chave de pesquisa de Olá Olá resourceId.</span><span class="sxs-lookup"><span data-stu-id="f8495-538">It expects toofind hello data for your VM using hello resourceId hello lookup key.</span></span>
* <span data-ttu-id="f8495-539">Se você usar o dimensionamento automático do Azure, Olá resourceId na configuração de AutoEscala Olá deve corresponder resourceId Olá usado pelo LAD.</span><span class="sxs-lookup"><span data-stu-id="f8495-539">If you use Azure autoscale, hello resourceId in hello autoscale configuration must match hello resourceId used by LAD.</span></span>
* <span data-ttu-id="f8495-540">Olá resourceId é criada em nomes de saudação do JsonBlobs gravados pelo LAD.</span><span class="sxs-lookup"><span data-stu-id="f8495-540">hello resourceId is built into hello names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="f8495-541">Ver seus dados</span><span class="sxs-lookup"><span data-stu-id="f8495-541">View your data</span></span>

<span data-ttu-id="f8495-542">Usar dados de desempenho do hello tooview portal do Azure ou definir alertas:</span><span class="sxs-lookup"><span data-stu-id="f8495-542">Use hello Azure portal tooview performance data or set alerts:</span></span>

![imagem](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="f8495-544">Olá `performanceCounters` dados sempre são armazenados em uma tabela de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8495-544">hello `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="f8495-545">As APIs do Armazenamento do Azure estão disponíveis em várias linguagens e plataformas.</span><span class="sxs-lookup"><span data-stu-id="f8495-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="f8495-546">Enviado tooJsonBlob Coletores de dados são armazenados em blobs na conta de armazenamento Olá nomeado no hello [protegido configurações](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="f8495-546">Data sent tooJsonBlob sinks is stored in blobs in hello storage account named in hello [Protected settings](#protected-settings).</span></span> <span data-ttu-id="f8495-547">Você pode consumir dados de blob hello usando quaisquer APIs de armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8495-547">You can consume hello blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="f8495-548">Além disso, você pode usar esses dados de saudação de tooaccess de ferramentas de interface do usuário no armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="f8495-548">In addition, you can use these UI tools tooaccess hello data in Azure Storage:</span></span>

* <span data-ttu-id="f8495-549">Gerenciador de Servidores do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f8495-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="f8495-550">[Gerenciador de Armazenamento do Microsoft Azure](https://azurestorageexplorer.codeplex.com/ "Gerenciador de Armazenamento do Azure").</span><span class="sxs-lookup"><span data-stu-id="f8495-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="f8495-551">Esse instantâneo de uma sessão do Microsoft Azure Storage Explorer mostra Olá geradas tabelas de armazenamento do Azure e os contêineres de uma extensão de LAD 3.0 corretamente configurada em uma VM de teste.</span><span class="sxs-lookup"><span data-stu-id="f8495-551">This snapshot of a Microsoft Azure Storage Explorer session shows hello generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="f8495-552">imagem de saudação não corresponde exatamente à saudação [LAD 3.0 de exemplo de configuração](#an-example-lad-30-configuration).</span><span class="sxs-lookup"><span data-stu-id="f8495-552">hello image doesn't match exactly with hello [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![imagem](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="f8495-554">Consulte Olá relevante [EventHubs documentação](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn como tooconsume mensagens publicadas tooan EventHubs endpoint.</span><span class="sxs-lookup"><span data-stu-id="f8495-554">See hello relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) toolearn how tooconsume messages published tooan EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8495-555">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f8495-555">Next steps</span></span>

* <span data-ttu-id="f8495-556">Criar alertas de métrica no [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) para métricas de saudação coletar.</span><span class="sxs-lookup"><span data-stu-id="f8495-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for hello metrics you collect.</span></span>
* <span data-ttu-id="f8495-557">Criar [gráficos de monitoramento](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) para suas métricas.</span><span class="sxs-lookup"><span data-stu-id="f8495-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="f8495-558">Saiba como muito[criar um conjunto de escala de máquina virtual](/azure/virtual-machines/linux/tutorial-create-vmss) usando o dimensionamento automático toocontrol de métricas.</span><span class="sxs-lookup"><span data-stu-id="f8495-558">Learn how too[create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics toocontrol autoscaling.</span></span>
