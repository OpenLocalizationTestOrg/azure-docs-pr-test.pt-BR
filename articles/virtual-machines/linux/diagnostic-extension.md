---
title: "Computação do Azure – Extensão de Diagnóstico Linux | Microsoft Docs"
description: "Como configurar a Extensão de Diagnóstico Linux (LAD) no Azure para coletar métricas e eventos de log de VMs Linux em execução no Azure."
services: virtual-machines-linux
author: jasonzio
manager: anandram
ms.service: virtual-machines-linux
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 05/09/2017
ms.author: jasonzio
ms.openlocfilehash: 525d706bd709ae72f2dca1c21e06db533ccf32b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="use-linux-diagnostic-extension-to-monitor-metrics-and-logs"></a><span data-ttu-id="8731b-103">Use a Extensão de Diagnóstico Linux para monitorar as métricas e os logs</span><span class="sxs-lookup"><span data-stu-id="8731b-103">Use Linux Diagnostic Extension to monitor metrics and logs</span></span>

<span data-ttu-id="8731b-104">Este documento descreve a versão 3.0 e mais recente da Extensão de Diagnóstico do Linux.</span><span class="sxs-lookup"><span data-stu-id="8731b-104">This document describes version 3.0 and newer of the Linux Diagnostic Extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8731b-105">Para saber mais sobre a versão 2.3 e anteriores, veja [este documento](./classic/diagnostic-extension-v2.md).</span><span class="sxs-lookup"><span data-stu-id="8731b-105">For information about version 2.3 and older, see [this document](./classic/diagnostic-extension-v2.md).</span></span>

## <a name="introduction"></a><span data-ttu-id="8731b-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="8731b-106">Introduction</span></span>

<span data-ttu-id="8731b-107">A Extensão de Diagnóstico Linux ajuda um usuário a monitorar a integridade de uma VM Linux em execução no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8731b-107">The Linux Diagnostic Extension helps a user monitor the health of a Linux VM running on Microsoft Azure.</span></span> <span data-ttu-id="8731b-108">Ela oferece os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="8731b-108">It has the following capabilities:</span></span>

* <span data-ttu-id="8731b-109">Coleta métricas de desempenho do sistema da VM e as armazena em uma tabela específica em uma conta de armazenamento designada.</span><span class="sxs-lookup"><span data-stu-id="8731b-109">Collects system performance metrics from the VM and stores them in a specific table in a designated storage account.</span></span>
* <span data-ttu-id="8731b-110">Recupera os eventos de log do syslog e os armazena em uma tabela específica na conta de armazenamento designada.</span><span class="sxs-lookup"><span data-stu-id="8731b-110">Retrieves log events from syslog and stores them in a specific table in the designated storage account.</span></span>
* <span data-ttu-id="8731b-111">Permite que os usuários personalizem as métricas de dados que são coletadas e carregadas.</span><span class="sxs-lookup"><span data-stu-id="8731b-111">Enables users to customize the data metrics that are collected and uploaded.</span></span>
* <span data-ttu-id="8731b-112">Permite que os usuários personalizem as instalações de syslog e os níveis de severidade dos eventos que são coletados e carregados.</span><span class="sxs-lookup"><span data-stu-id="8731b-112">Enables users to customize the syslog facilities and severity levels of events that are collected and uploaded.</span></span>
* <span data-ttu-id="8731b-113">Permite que os usuários carreguem arquivos de log especificados em uma tabela de armazenamento designada.</span><span class="sxs-lookup"><span data-stu-id="8731b-113">Enables users to upload specified log files to a designated storage table.</span></span>
* <span data-ttu-id="8731b-114">Oferece suporte ao envio de métricas e eventos de log para pontos de extremidade arbitrários de EventHub e blobs formatados pelo JSON na conta de armazenamento designada.</span><span class="sxs-lookup"><span data-stu-id="8731b-114">Supports sending metrics and log events to arbitrary EventHub endpoints and JSON-formatted blobs in the designated storage account.</span></span>

<span data-ttu-id="8731b-115">Essa extensão funciona com os dois modelos de implantação do Azure.</span><span class="sxs-lookup"><span data-stu-id="8731b-115">This extension works with both Azure deployment models.</span></span>

## <a name="installing-the-extension-in-your-vm"></a><span data-ttu-id="8731b-116">Instalando a extensão em sua VM</span><span class="sxs-lookup"><span data-stu-id="8731b-116">Installing the extension in your VM</span></span>

<span data-ttu-id="8731b-117">Você pode habilitar essa extensão usando os cmdlets do Azure PowerShell, os scripts da CLI do Azure ou os modelos de implantação do Azure.</span><span class="sxs-lookup"><span data-stu-id="8731b-117">You can enable this extension by using the Azure PowerShell cmdlets, Azure CLI scripts, or Azure deployment templates.</span></span> <span data-ttu-id="8731b-118">Para saber mais, veja [Recursos de extensões](./extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="8731b-118">For more information, see [Extensions Features](./extensions-features.md).</span></span>

<span data-ttu-id="8731b-119">O Portal do Azure não pode ser usado para habilitar ou configurar o LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="8731b-119">The Azure portal cannot be used to enable or configure LAD 3.0.</span></span> <span data-ttu-id="8731b-120">Em vez disso, ele instala e configura a versão 2.3.</span><span class="sxs-lookup"><span data-stu-id="8731b-120">Instead, it installs and configures version 2.3.</span></span> <span data-ttu-id="8731b-121">Os gráficos de portal e os alertas do Azure funcionam com dados de ambas as versões da extensão.</span><span class="sxs-lookup"><span data-stu-id="8731b-121">Azure portal graphs and alerts work with data from both versions of the extension.</span></span>

<span data-ttu-id="8731b-122">Estas instruções de instalação e uma [configuração de amostra para download](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configuram o LAD 3.0 para:</span><span class="sxs-lookup"><span data-stu-id="8731b-122">These installation instructions and a [downloadable sample configuration](https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json) configure LAD 3.0 to:</span></span>

* <span data-ttu-id="8731b-123">capturar e armazenar as mesmas métricas fornecidas pelo LAD 2.3;</span><span class="sxs-lookup"><span data-stu-id="8731b-123">capture and store the same metrics as were provided by LAD 2.3;</span></span>
* <span data-ttu-id="8731b-124">capturar um conjunto útil de métricas do sistema de arquivo, novos para o LAD 3.0;</span><span class="sxs-lookup"><span data-stu-id="8731b-124">capture a useful set of file system metrics, new to LAD 3.0;</span></span>
* <span data-ttu-id="8731b-125">capturar a coleção de syslog padrão habilitada pelo LAD 2.3;</span><span class="sxs-lookup"><span data-stu-id="8731b-125">capture the default syslog collection enabled by LAD 2.3;</span></span>
* <span data-ttu-id="8731b-126">habilitar a experiência do Portal do Azure para gráficos e criação de alertas nas métricas da VM.</span><span class="sxs-lookup"><span data-stu-id="8731b-126">enable the Azure portal experience for charting and alerting on VM metrics.</span></span>

<span data-ttu-id="8731b-127">A configuração para download é apenas um exemplo; modifique-a para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="8731b-127">The downloadable configuration is just an example; modify it to suit your own needs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="8731b-128">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8731b-128">Prerequisites</span></span>

* <span data-ttu-id="8731b-129">**Agente Linux do Azure versão 2.2.0 ou posterior**.</span><span class="sxs-lookup"><span data-stu-id="8731b-129">**Azure Linux Agent version 2.2.0 or later**.</span></span> <span data-ttu-id="8731b-130">A maioria das imagens de galeria da VM Linux do Azure inclui a versão 2.2.7 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="8731b-130">Most Azure VM Linux gallery images include version 2.2.7 or later.</span></span> <span data-ttu-id="8731b-131">Execute `/usr/sbin/waagent -version` para confirmar a versão instalada na VM.</span><span class="sxs-lookup"><span data-stu-id="8731b-131">Run `/usr/sbin/waagent -version` to confirm the version installed on the VM.</span></span> <span data-ttu-id="8731b-132">Se a VM estiver executando uma versão mais antiga do agente convidado, execute [estas instruções](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) para atualizá-la.</span><span class="sxs-lookup"><span data-stu-id="8731b-132">If the VM is running an older version of the guest agent, follow [these instructions](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/update-agent) to update it.</span></span>
* <span data-ttu-id="8731b-133">**CLI do Azure**.</span><span class="sxs-lookup"><span data-stu-id="8731b-133">**Azure CLI**.</span></span> <span data-ttu-id="8731b-134">[Configurar o ambiente do CLI 2.0 do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli) em seu computador.</span><span class="sxs-lookup"><span data-stu-id="8731b-134">[Set up the Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) environment on your machine.</span></span>
* <span data-ttu-id="8731b-135">O comando wget, caso ainda não o tenha: execute `sudo apt-get install wget`.</span><span class="sxs-lookup"><span data-stu-id="8731b-135">The wget command, if you don't already have it: Run `sudo apt-get install wget`.</span></span>
* <span data-ttu-id="8731b-136">Uma assinatura existente do Azure e uma conta de armazenamento existente nela para armazenar os dados.</span><span class="sxs-lookup"><span data-stu-id="8731b-136">An existing Azure subscription and an existing storage account within it to store the data.</span></span>

### <a name="sample-installation"></a><span data-ttu-id="8731b-137">Instalação de exemplo</span><span class="sxs-lookup"><span data-stu-id="8731b-137">Sample installation</span></span>

<span data-ttu-id="8731b-138">Preencha os parâmetros corretos nas três primeiras linhas, em seguida, execute este script como raiz:</span><span class="sxs-lookup"><span data-stu-id="8731b-138">Fill in the correct parameters on the first three lines, then execute this script as root:</span></span>

```bash
# Set your Azure VM diagnostic parameters correctly below
my_resource_group=<your_azure_resource_group_name_containing_your_azure_linux_vm>
my_linux_vm=<your_azure_linux_vm_name>
my_diagnostic_storage_account=<your_azure_storage_account_for_storing_vm_diagnostic_data>

# Should login to Azure first before anything else
az login

# Select the subscription containing the storage account
az account set --subscription <your_azure_subscription_id>

# Download the sample Public settings. (You could also use curl or any web browser)
wget https://raw.githubusercontent.com/Azure/azure-linux-extensions/master/Diagnostic/tests/lad_2_3_compatible_portal_pub_settings.json -O portal_public_settings.json

# Build the VM resource ID. Replace storage account name and resource ID in the public settings.
my_vm_resource_id=$(az vm show -g $my_resource_group -n $my_linux_vm --query "id" -o tsv)
sed -i "s#__DIAGNOSTIC_STORAGE_ACCOUNT__#$my_diagnostic_storage_account#g" portal_public_settings.json
sed -i "s#__VM_RESOURCE_ID__#$my_vm_resource_id#g" portal_public_settings.json

# Build the protected settings (storage account SAS token)
my_diagnostic_storage_account_sastoken=$(az storage account generate-sas --account-name $my_diagnostic_storage_account --expiry 9999-12-31T23:59Z --permissions wlacu --resource-types co --services bt -o tsv)
my_lad_protected_settings="{'storageAccountName': '$my_diagnostic_storage_account', 'storageAccountSasToken': '$my_diagnostic_storage_account_sastoken'}"

# Finallly tell Azure to install and enable the extension
az vm extension set --publisher Microsoft.Azure.Diagnostics --name LinuxDiagnostic --version 3.0 --resource-group $my_resource_group --vm-name $my_linux_vm --protected-settings "${my_lad_protected_settings}" --settings portal_public_settings.json
```

<span data-ttu-id="8731b-139">A URL para a configuração de amostra e seu conteúdo estão sujeitos a alterações.</span><span class="sxs-lookup"><span data-stu-id="8731b-139">The URL for the sample configuration, and its contents, are subject to change.</span></span> <span data-ttu-id="8731b-140">Baixe uma cópia do arquivo JSON de configurações do portal e personalize-o de acordo com as suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="8731b-140">Download a copy of the portal settings JSON file and customize it for your needs.</span></span> <span data-ttu-id="8731b-141">Os modelos ou as automações que você construir deverão usar sua própria cópia em vez de baixar essa URL toda vez.</span><span class="sxs-lookup"><span data-stu-id="8731b-141">Any templates or automation you construct should use your own copy, rather than downloading that URL each time.</span></span>

### <a name="updating-the-extension-settings"></a><span data-ttu-id="8731b-142">Atualização das configurações de extensão</span><span class="sxs-lookup"><span data-stu-id="8731b-142">Updating the extension settings</span></span>

<span data-ttu-id="8731b-143">Depois que você tiver alterado as configurações Públicas ou Protegidas, implante-as na VM executando o mesmo comando.</span><span class="sxs-lookup"><span data-stu-id="8731b-143">After you've changed your Protected or Public settings, deploy them to the VM by running the same command.</span></span> <span data-ttu-id="8731b-144">Se algo for alterado nas configurações, as configurações atualizadas serão enviadas para a extensão.</span><span class="sxs-lookup"><span data-stu-id="8731b-144">If anything changed in the settings, the updated settings are sent to the extension.</span></span> <span data-ttu-id="8731b-145">O LAD recarrega a configuração e é reiniciado.</span><span class="sxs-lookup"><span data-stu-id="8731b-145">LAD reloads the configuration and restarts itself.</span></span>

### <a name="migration-from-previous-versions-of-the-extension"></a><span data-ttu-id="8731b-146">Migração de versões anteriores da extensão</span><span class="sxs-lookup"><span data-stu-id="8731b-146">Migration from previous versions of the extension</span></span>

<span data-ttu-id="8731b-147">A versão mais recente da extensão é a **3.0**.</span><span class="sxs-lookup"><span data-stu-id="8731b-147">The latest version of the extension is **3.0**.</span></span> <span data-ttu-id="8731b-148">**As versões anteriores (2.x) antigas são substituídas e podem ser canceladas em ou após 31 de julho de 2018**.</span><span class="sxs-lookup"><span data-stu-id="8731b-148">**Any old versions (2.x) are deprecated and may be unpublished on or after July 31, 2018**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8731b-149">Essa extensão introduz alterações significativas na configuração da extensão.</span><span class="sxs-lookup"><span data-stu-id="8731b-149">This extension introduces breaking changes to the configuration of the extension.</span></span> <span data-ttu-id="8731b-150">Uma alteração foi feita para melhorar a segurança da extensão; como resultado disso, a compatibilidade com as versões 2.x pode não ser mantida.</span><span class="sxs-lookup"><span data-stu-id="8731b-150">One such change was made to improve the security of the extension; as a result, backwards compatibility with 2.x could not be maintained.</span></span> <span data-ttu-id="8731b-151">Além disso, o Editor de Extensões para esta extensão é diferente do editor para as versões 2.x.</span><span class="sxs-lookup"><span data-stu-id="8731b-151">Also, the Extension Publisher for this extension is different than the publisher for the 2.x versions.</span></span>
>
> <span data-ttu-id="8731b-152">Para migrar da 2.x para essa nova versão da extensão, você deverá desinstalar a extensão antiga (com o nome do editor antigo) e instalar a versão 3 da extensão.</span><span class="sxs-lookup"><span data-stu-id="8731b-152">To migrate from 2.x to this new version of the extension, you must uninstall the old extension (under the old publisher name), then install version 3 of the extension.</span></span>

<span data-ttu-id="8731b-153">Recomendações:</span><span class="sxs-lookup"><span data-stu-id="8731b-153">Recommendations:</span></span>

* <span data-ttu-id="8731b-154">Instale a extensão com a atualização de versão secundária automática habilitada.</span><span class="sxs-lookup"><span data-stu-id="8731b-154">Install the extension with automatic minor version upgrade enabled.</span></span>
  * <span data-ttu-id="8731b-155">Em VMs de modelo de implantação clássicas, especifique '3.*' como a versão, se você estiver instalando a extensão por meio da CLI do Azure XPLAT ou do Powershell.</span><span class="sxs-lookup"><span data-stu-id="8731b-155">On classic deployment model VMs, specify '3.*' as the version if you are installing the extension through Azure XPLAT CLI or Powershell.</span></span>
  * <span data-ttu-id="8731b-156">Nas VMs do Modelo de implantação do Azure Resource Manager, inclua '"autoUpgradeMinorVersion": true' no modelo de implantação da VM.</span><span class="sxs-lookup"><span data-stu-id="8731b-156">On Azure Resource Manager deployment model VMs, include '"autoUpgradeMinorVersion": true' in the VM deployment template.</span></span>
* <span data-ttu-id="8731b-157">Use uma conta de armazenamento nova/diferente para o LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="8731b-157">Use a new/different storage account for LAD 3.0.</span></span> <span data-ttu-id="8731b-158">Há várias pequenas incompatibilidades entre o LAD 2.3 e o LAD 3.0 que dificultam o compartilhamento de uma conta:</span><span class="sxs-lookup"><span data-stu-id="8731b-158">There are several small incompatibilities between LAD 2.3 and LAD 3.0 that make sharing an account troublesome:</span></span>
  * <span data-ttu-id="8731b-159">O LAD 3.0 armazena os eventos de syslog em uma tabela com um nome diferente.</span><span class="sxs-lookup"><span data-stu-id="8731b-159">LAD 3.0 stores syslog events in a table with a different name.</span></span>
  * <span data-ttu-id="8731b-160">As cadeias de caracteres counterSpecifier para as métricas `builtin` são diferentes no LAD 3.0.</span><span class="sxs-lookup"><span data-stu-id="8731b-160">The counterSpecifier strings for `builtin` metrics differ in LAD 3.0.</span></span>

## <a name="protected-settings"></a><span data-ttu-id="8731b-161">Configurações protegidas</span><span class="sxs-lookup"><span data-stu-id="8731b-161">Protected settings</span></span>

<span data-ttu-id="8731b-162">Esse conjunto de informações de configuração contém informações confidenciais que devem ser protegidas da visualização pública, por exemplo, as credenciais de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8731b-162">This set of configuration information contains sensitive information that should be protected from public view, for example, storage credentials.</span></span> <span data-ttu-id="8731b-163">Essas configurações são transmitidas para e armazenadas pela extensão de forma criptografada.</span><span class="sxs-lookup"><span data-stu-id="8731b-163">These settings are transmitted to and stored by the extension in encrypted form.</span></span>

```json
{
    "storageAccountName" : "the storage account to receive data",
    "storageAccountEndPoint": "the hostname suffix for the cloud for this account",
    "storageAccountSasToken": "SAS access token",
    "mdsdHttpProxy": "HTTP proxy settings",
    "sinksConfig": { ... }
}
```

<span data-ttu-id="8731b-164">Nome</span><span class="sxs-lookup"><span data-stu-id="8731b-164">Name</span></span> | <span data-ttu-id="8731b-165">Valor</span><span class="sxs-lookup"><span data-stu-id="8731b-165">Value</span></span>
---- | -----
<span data-ttu-id="8731b-166">storageAccountName</span><span class="sxs-lookup"><span data-stu-id="8731b-166">storageAccountName</span></span> | <span data-ttu-id="8731b-167">O nome da conta de armazenamento na qual os dados são gravados pela extensão.</span><span class="sxs-lookup"><span data-stu-id="8731b-167">The name of the storage account in which data is written by the extension.</span></span>
<span data-ttu-id="8731b-168">storageAccountEndPoint</span><span class="sxs-lookup"><span data-stu-id="8731b-168">storageAccountEndPoint</span></span> | <span data-ttu-id="8731b-169">(opcional) O ponto de extremidade que identifica a nuvem na qual existe a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8731b-169">(optional) The endpoint identifying the cloud in which the storage account exists.</span></span> <span data-ttu-id="8731b-170">Se essa configuração estiver ausente, o LAD utiliza como padrão a nuvem pública do Azure, `https://core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="8731b-170">If this setting is absent, LAD defaults to the Azure public cloud, `https://core.windows.net`.</span></span> <span data-ttu-id="8731b-171">Para usar uma conta de armazenamento no Azure Alemanha, no Azure Governamental ou Azure China, defina este valor corretamente.</span><span class="sxs-lookup"><span data-stu-id="8731b-171">To use a storage account in Azure Germany, Azure Government, or Azure China, set this value accordingly.</span></span>
<span data-ttu-id="8731b-172">storageAccountSasToken</span><span class="sxs-lookup"><span data-stu-id="8731b-172">storageAccountSasToken</span></span> | <span data-ttu-id="8731b-173">Um [Token de SAS de conta](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) para serviços Blob e de tabela (`ss='bt'`), aplicável a contêineres e objetos (`srt='co'`), que concede permissão para adicionar, criar, listar, atualizar e gravar (`sp='acluw'`).</span><span class="sxs-lookup"><span data-stu-id="8731b-173">An [Account SAS token](https://azure.microsoft.com/blog/sas-update-account-sas-now-supports-all-storage-services/) for Blob and Table services (`ss='bt'`), applicable to containers and objects (`srt='co'`), which grants add, create, list, update, and write permissions (`sp='acluw'`).</span></span> <span data-ttu-id="8731b-174">*Não* inclua o ponto de interrogação (?) no início.</span><span class="sxs-lookup"><span data-stu-id="8731b-174">Do *not* include the leading question-mark (?).</span></span>
<span data-ttu-id="8731b-175">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="8731b-175">mdsdHttpProxy</span></span> | <span data-ttu-id="8731b-176">(opcional) As informações de proxy de HTTP necessárias para habilitar a extensão para se conectar ao ponto de extremidade e à conta de armazenamento especificados.</span><span class="sxs-lookup"><span data-stu-id="8731b-176">(optional) HTTP proxy information needed to enable the extension to connect to the specified storage account and endpoint.</span></span>
<span data-ttu-id="8731b-177">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="8731b-177">sinksConfig</span></span> | <span data-ttu-id="8731b-178">(opcional) Detalhes de destinos alternativos para os quais as métricas e os eventos podem ser entregues.</span><span class="sxs-lookup"><span data-stu-id="8731b-178">(optional) Details of alternative destinations to which metrics and events can be delivered.</span></span> <span data-ttu-id="8731b-179">Os detalhes específicos de cada coletor de dados compatível com a extensão são abordados nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="8731b-179">The specific details of each data sink supported by the extension are covered in the sections that follow.</span></span>

<span data-ttu-id="8731b-180">Você pode facilmente construir o token de SAS necessário por meio do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8731b-180">You can easily construct the required SAS token through the Azure portal.</span></span>

1. <span data-ttu-id="8731b-181">Selecione a conta de armazenamento de uso geral na qual você deseja que a extensão grave</span><span class="sxs-lookup"><span data-stu-id="8731b-181">Select the general-purpose storage account to which you want the extension to write</span></span>
1. <span data-ttu-id="8731b-182">Selecione "Assinatura de acesso compartilhado" na parte de configurações do menu à esquerda</span><span class="sxs-lookup"><span data-stu-id="8731b-182">Select "Shared access signature" from the Settings part of the left menu</span></span>
1. <span data-ttu-id="8731b-183">Verifique as seções apropriadas conforme descrito anteriormente</span><span class="sxs-lookup"><span data-stu-id="8731b-183">Make the appropriate sections as previously described</span></span>
1. <span data-ttu-id="8731b-184">Clique no botão "Gerar SAS".</span><span class="sxs-lookup"><span data-stu-id="8731b-184">Click the "Generate SAS" button.</span></span>

![imagem](./media/diagnostic-extension/make_sas.png)

<span data-ttu-id="8731b-186">Copie o SAS gerado no campo storageAccountSasToken; remova o ponto de interrogação ("?") do início.</span><span class="sxs-lookup"><span data-stu-id="8731b-186">Copy the generated SAS into the storageAccountSasToken field; remove the leading question-mark ("?").</span></span>

### <a name="sinksconfig"></a><span data-ttu-id="8731b-187">sinksConfig</span><span class="sxs-lookup"><span data-stu-id="8731b-187">sinksConfig</span></span>

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

<span data-ttu-id="8731b-188">Esta seção opcional define os destinos adicionais para os quais a extensão envia as informações coletadas.</span><span class="sxs-lookup"><span data-stu-id="8731b-188">This optional section defines additional destinations to which the extension sends the information it collects.</span></span> <span data-ttu-id="8731b-189">A matriz "coletor" contém um objeto para cada coletor de dados adicional.</span><span class="sxs-lookup"><span data-stu-id="8731b-189">The "sink" array contains an object for each additional data sink.</span></span> <span data-ttu-id="8731b-190">O atributo "tipo" determina os outros atributos no objeto.</span><span class="sxs-lookup"><span data-stu-id="8731b-190">The "type" attribute determines the other attributes in the object.</span></span>

<span data-ttu-id="8731b-191">Elemento</span><span class="sxs-lookup"><span data-stu-id="8731b-191">Element</span></span> | <span data-ttu-id="8731b-192">Valor</span><span class="sxs-lookup"><span data-stu-id="8731b-192">Value</span></span>
------- | -----
<span data-ttu-id="8731b-193">name</span><span class="sxs-lookup"><span data-stu-id="8731b-193">name</span></span> | <span data-ttu-id="8731b-194">Uma cadeia de caracteres usada para se referir a esse coletor em outro lugar na configuração da extensão.</span><span class="sxs-lookup"><span data-stu-id="8731b-194">A string used to refer to this sink elsewhere in the extension configuration.</span></span>
<span data-ttu-id="8731b-195">type</span><span class="sxs-lookup"><span data-stu-id="8731b-195">type</span></span> | <span data-ttu-id="8731b-196">O tipo de coletor que está sendo definido.</span><span class="sxs-lookup"><span data-stu-id="8731b-196">The type of sink being defined.</span></span> <span data-ttu-id="8731b-197">Determina os outros valores (se houver) em instâncias desse tipo.</span><span class="sxs-lookup"><span data-stu-id="8731b-197">Determines the other values (if any) in instances of this type.</span></span>

<span data-ttu-id="8731b-198">A extensão de Diagnóstico do Linux versão 3.0 oferece suporte a dois tipos de coletor: EventHub e JsonBlob.</span><span class="sxs-lookup"><span data-stu-id="8731b-198">Version 3.0 of the Linux Diagnostic Extension supports two sink types: EventHub, and JsonBlob.</span></span>

#### <a name="the-eventhub-sink"></a><span data-ttu-id="8731b-199">O coletor EventHub</span><span class="sxs-lookup"><span data-stu-id="8731b-199">The EventHub sink</span></span>

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

<span data-ttu-id="8731b-200">A entrada "sasURL" contém a URL completa, incluindo o token de SAS para o Hub de eventos para os quais os dados devem ser publicados.</span><span class="sxs-lookup"><span data-stu-id="8731b-200">The "sasURL" entry contains the full URL, including SAS token, for the Event Hub to which data should be published.</span></span> <span data-ttu-id="8731b-201">O LAD exige uma SAS uma política de nomeação de SAS que permite a declaração de envio.</span><span class="sxs-lookup"><span data-stu-id="8731b-201">LAD requires a SAS naming a policy that enables the Send claim.</span></span> <span data-ttu-id="8731b-202">Um exemplo:</span><span class="sxs-lookup"><span data-stu-id="8731b-202">An example:</span></span>

* <span data-ttu-id="8731b-203">Criar um namespace de Hubs de Eventos chamado `contosohub`</span><span class="sxs-lookup"><span data-stu-id="8731b-203">Create an Event Hubs namespace called `contosohub`</span></span>
* <span data-ttu-id="8731b-204">Criar um Hub de Eventos no namespace chamado `syslogmsgs`</span><span class="sxs-lookup"><span data-stu-id="8731b-204">Create an Event Hub in the namespace called `syslogmsgs`</span></span>
* <span data-ttu-id="8731b-205">Criar uma política de acesso compartilhado no Hub de Eventos chamado `writer` que permite que a declaração de envio</span><span class="sxs-lookup"><span data-stu-id="8731b-205">Create a Shared access policy on the Event Hub named `writer` that enables the Send claim</span></span>

<span data-ttu-id="8731b-206">Se você tiver criado uma SAS válida até meia-noite UTC em 1 de janeiro de 2018, o valor de sasURL poderá ser:</span><span class="sxs-lookup"><span data-stu-id="8731b-206">If you created a SAS good until midnight UTC on January 1, 2018, the sasURL value might be:</span></span>

```url
https://contosohub.servicebus.windows.net/syslogmsgs?sr=contosohub.servicebus.windows.net%2fsyslogmsgs&sig=xxxxxxxxxxxxxxxxxxxxxxxxx&se=1514764800&skn=writer
```

<span data-ttu-id="8731b-207">Para saber mais sobre como gerar tokens de SAS para Hubs de Eventos, veja [esta página da Web](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8731b-207">For more information about generating SAS tokens for Event Hubs, see [this web page](../../event-hubs/event-hubs-authentication-and-security-model-overview.md).</span></span>

#### <a name="the-jsonblob-sink"></a><span data-ttu-id="8731b-208">O coletor JsonBlob</span><span class="sxs-lookup"><span data-stu-id="8731b-208">The JsonBlob sink</span></span>

```json
"sink": [
    {
        "name": "sinkname",
        "type": "JsonBlob"
    },
    ...
]
```

<span data-ttu-id="8731b-209">Os dados direcionados para um coletor JsonBlob são armazenados em blobs no armazenamento do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="8731b-209">Data directed to a JsonBlob sink is stored in blobs in Azure storage.</span></span> <span data-ttu-id="8731b-210">Cada instância de LAD cria um blob a cada hora para cada nome de coletor.</span><span class="sxs-lookup"><span data-stu-id="8731b-210">Each instance of LAD creates a blob every hour for each sink name.</span></span> <span data-ttu-id="8731b-211">Cada blob sempre contém uma matriz de objeto JSON sintaticamente válida.</span><span class="sxs-lookup"><span data-stu-id="8731b-211">Each blob always contains a syntactically valid JSON array of object.</span></span> <span data-ttu-id="8731b-212">Novas entradas são adicionadas atomicamente à matriz.</span><span class="sxs-lookup"><span data-stu-id="8731b-212">New entries are atomically added to the array.</span></span> <span data-ttu-id="8731b-213">Os BLOBs são armazenados em um contêiner com o mesmo nome que o coletor.</span><span class="sxs-lookup"><span data-stu-id="8731b-213">Blobs are stored in a container with the same name as the sink.</span></span> <span data-ttu-id="8731b-214">As regras de armazenamento do Azure para nomes de contêineres de blob aplicam-se aos nomes dos coletores JsonBlob: entre 3 e 63 caracteres ASCII alfanuméricos minúsculos ou traços.</span><span class="sxs-lookup"><span data-stu-id="8731b-214">The Azure storage rules for blob container names apply to the names of JsonBlob sinks: between 3 and 63 lower-case alphanumeric ASCII characters or dashes.</span></span>

## <a name="public-settings"></a><span data-ttu-id="8731b-215">Configurações públicas</span><span class="sxs-lookup"><span data-stu-id="8731b-215">Public settings</span></span>

<span data-ttu-id="8731b-216">Essa estrutura contém vários blocos de configurações que controlam as informações coletadas pela extensão.</span><span class="sxs-lookup"><span data-stu-id="8731b-216">This structure contains various blocks of settings that control the information collected by the extension.</span></span> <span data-ttu-id="8731b-217">Cada configuração é opcional.</span><span class="sxs-lookup"><span data-stu-id="8731b-217">Each setting is optional.</span></span> <span data-ttu-id="8731b-218">Se você especificar `ladCfg`, também deverá especificar `StorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="8731b-218">If you specify `ladCfg`, you must also specify `StorageAccount`.</span></span>

```json
{
    "ladCfg":  { ... },
    "perfCfg": { ... },
    "fileLogs": { ... },
    "StorageAccount": "the storage account to receive data",
    "mdsdHttpProxy" : ""
}
```

<span data-ttu-id="8731b-219">Elemento</span><span class="sxs-lookup"><span data-stu-id="8731b-219">Element</span></span> | <span data-ttu-id="8731b-220">Valor</span><span class="sxs-lookup"><span data-stu-id="8731b-220">Value</span></span>
------- | -----
<span data-ttu-id="8731b-221">StorageAccount</span><span class="sxs-lookup"><span data-stu-id="8731b-221">StorageAccount</span></span> | <span data-ttu-id="8731b-222">O nome da conta de armazenamento na qual os dados são gravados pela extensão.</span><span class="sxs-lookup"><span data-stu-id="8731b-222">The name of the storage account in which data is written by the extension.</span></span> <span data-ttu-id="8731b-223">Deve ser o mesmo nome, conforme especificado nas [Configurações protegidas](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="8731b-223">Must be the same name as is specified in the [Protected settings](#protected-settings).</span></span>
<span data-ttu-id="8731b-224">mdsdHttpProxy</span><span class="sxs-lookup"><span data-stu-id="8731b-224">mdsdHttpProxy</span></span> | <span data-ttu-id="8731b-225">(opcional) O mesmo que nas [Configurações protegidas](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="8731b-225">(optional) Same as in the [Protected settings](#protected-settings).</span></span> <span data-ttu-id="8731b-226">O valor público é substituído pelo valor particular, se tiver sido definido.</span><span class="sxs-lookup"><span data-stu-id="8731b-226">The public value is overridden by the private value, if set.</span></span> <span data-ttu-id="8731b-227">Coloque as configurações de proxy que contêm um segredo, como uma senha, nas [Configurações protegidas](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="8731b-227">Place proxy settings that contain a secret, such as a password, in the [Protected settings](#protected-settings).</span></span>

<span data-ttu-id="8731b-228">Os elementos restantes serão descritos em detalhes nas seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="8731b-228">The remaining elements are described in detail in the following sections.</span></span>

### <a name="ladcfg"></a><span data-ttu-id="8731b-229">ladCfg</span><span class="sxs-lookup"><span data-stu-id="8731b-229">ladCfg</span></span>

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

<span data-ttu-id="8731b-230">Essa estrutura opcional controla a reunião de métricas e logs de entrega para o serviço de Métricas do Azure e outros coletores de dados.</span><span class="sxs-lookup"><span data-stu-id="8731b-230">This optional structure controls the gathering of metrics and logs for delivery to the Azure Metrics service and to other data sinks.</span></span> <span data-ttu-id="8731b-231">Você deve especificar `performanceCounters` ou `syslogEvents`, ou ambos.</span><span class="sxs-lookup"><span data-stu-id="8731b-231">You must specify either `performanceCounters` or `syslogEvents` or both.</span></span> <span data-ttu-id="8731b-232">Você deve especificar a estrutura `metrics`.</span><span class="sxs-lookup"><span data-stu-id="8731b-232">You must specify the `metrics` structure.</span></span>

<span data-ttu-id="8731b-233">Elemento</span><span class="sxs-lookup"><span data-stu-id="8731b-233">Element</span></span> | <span data-ttu-id="8731b-234">Valor</span><span class="sxs-lookup"><span data-stu-id="8731b-234">Value</span></span>
------- | -----
<span data-ttu-id="8731b-235">eventVolume</span><span class="sxs-lookup"><span data-stu-id="8731b-235">eventVolume</span></span> | <span data-ttu-id="8731b-236">(opcional) Controla o número de partições criadas dentro da tabela de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8731b-236">(optional) Controls the number of partitions created within the storage table.</span></span> <span data-ttu-id="8731b-237">Pode ser `"Large"`, `"Medium"` ou `"Small"`.</span><span class="sxs-lookup"><span data-stu-id="8731b-237">Must be one of `"Large"`, `"Medium"`, or `"Small"`.</span></span> <span data-ttu-id="8731b-238">Se esse campo não for especificado, o valor padrão será `"Medium"`.</span><span class="sxs-lookup"><span data-stu-id="8731b-238">If not specified, the default value is `"Medium"`.</span></span>
<span data-ttu-id="8731b-239">sampleRateInSeconds</span><span class="sxs-lookup"><span data-stu-id="8731b-239">sampleRateInSeconds</span></span> | <span data-ttu-id="8731b-240">(opcional) O intervalo padrão entre a coleta de métricas brutas (não agregadas).</span><span class="sxs-lookup"><span data-stu-id="8731b-240">(optional) The default interval between collection of raw (unaggregated) metrics.</span></span> <span data-ttu-id="8731b-241">A menor taxa de amostra com suporte é de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="8731b-241">The smallest supported sample rate is 15 seconds.</span></span> <span data-ttu-id="8731b-242">Se esse campo não for especificado, o valor padrão será `15`.</span><span class="sxs-lookup"><span data-stu-id="8731b-242">If not specified, the default value is `15`.</span></span>

#### <a name="metrics"></a><span data-ttu-id="8731b-243">Métricas</span><span class="sxs-lookup"><span data-stu-id="8731b-243">metrics</span></span>

```json
"metrics": {
    "resourceId": "/subscriptions/...",
    "metricAggregation" : [
        { "scheduledTransferPeriod" : "PT1H" },
        { "scheduledTransferPeriod" : "PT5M" }
    ]
}
```

<span data-ttu-id="8731b-244">Elemento</span><span class="sxs-lookup"><span data-stu-id="8731b-244">Element</span></span> | <span data-ttu-id="8731b-245">Valor</span><span class="sxs-lookup"><span data-stu-id="8731b-245">Value</span></span>
------- | -----
<span data-ttu-id="8731b-246">resourceId</span><span class="sxs-lookup"><span data-stu-id="8731b-246">resourceId</span></span> | <span data-ttu-id="8731b-247">A ID de recurso do Azure Resource Manager da VM ou conjunto de dimensionamento de máquinas virtuais à qual pertence a VM.</span><span class="sxs-lookup"><span data-stu-id="8731b-247">The Azure Resource Manager resource ID of the VM or of the virtual machine scale set to which the VM belongs.</span></span> <span data-ttu-id="8731b-248">Essa configuração também deverá ser especificada se algum coletor JsonBlob for usado na configuração.</span><span class="sxs-lookup"><span data-stu-id="8731b-248">This setting must be also specified if any JsonBlob sink is used in the configuration.</span></span>
<span data-ttu-id="8731b-249">scheduledTransferPeriod</span><span class="sxs-lookup"><span data-stu-id="8731b-249">scheduledTransferPeriod</span></span> | <span data-ttu-id="8731b-250">A frequência na qual as métricas agregadas serão computadas e transferidas para as Métricas do Azure, expressas como um intervalo de tempo de IS 8601.</span><span class="sxs-lookup"><span data-stu-id="8731b-250">The frequency at which aggregate metrics are to be computed and transferred to Azure Metrics, expressed as an IS 8601 time interval.</span></span> <span data-ttu-id="8731b-251">O menor período de transferência é 60 segundos, ou seja, PT1M.</span><span class="sxs-lookup"><span data-stu-id="8731b-251">The smallest transfer period is 60 seconds, that is, PT1M.</span></span> <span data-ttu-id="8731b-252">Você deve especificar pelo menos um scheduledTransferPeriod.</span><span class="sxs-lookup"><span data-stu-id="8731b-252">You must specify at least one scheduledTransferPeriod.</span></span>

<span data-ttu-id="8731b-253">As amostras de métricas especificados na seção performanceCounters são coletados a cada 15 segundos ou na taxa de amostra explicitamente definidas para o contador.</span><span class="sxs-lookup"><span data-stu-id="8731b-253">Samples of the metrics specified in the performanceCounters section are collected every 15 seconds or at the sample rate explicitly defined for the counter.</span></span> <span data-ttu-id="8731b-254">Se várias frequências scheduledTransferPeriod aparecerem (como no exemplo), cada agregação será calculada independentemente.</span><span class="sxs-lookup"><span data-stu-id="8731b-254">If multiple scheduledTransferPeriod frequencies appear (as in the example), each aggregation is computed independently.</span></span>

#### <a name="performancecounters"></a><span data-ttu-id="8731b-255">performanceCounters</span><span class="sxs-lookup"><span data-stu-id="8731b-255">performanceCounters</span></span>

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

<span data-ttu-id="8731b-256">Essa seção opcional controla a coleção de métricas.</span><span class="sxs-lookup"><span data-stu-id="8731b-256">This optional section controls the collection of metrics.</span></span> <span data-ttu-id="8731b-257">As amostras brutas são agregadas para cada [scheduledTransferPeriod](#metrics) para produzir esses valores:</span><span class="sxs-lookup"><span data-stu-id="8731b-257">Raw samples are aggregated for each [scheduledTransferPeriod](#metrics) to produce these values:</span></span>

* <span data-ttu-id="8731b-258">média</span><span class="sxs-lookup"><span data-stu-id="8731b-258">mean</span></span>
* <span data-ttu-id="8731b-259">mínimo</span><span class="sxs-lookup"><span data-stu-id="8731b-259">minimum</span></span>
* <span data-ttu-id="8731b-260">máximo</span><span class="sxs-lookup"><span data-stu-id="8731b-260">maximum</span></span>
* <span data-ttu-id="8731b-261">valor coletado por último</span><span class="sxs-lookup"><span data-stu-id="8731b-261">last-collected value</span></span>
* <span data-ttu-id="8731b-262">contagem de amostras brutas usadas para computar a agregação</span><span class="sxs-lookup"><span data-stu-id="8731b-262">count of raw samples used to compute the aggregate</span></span>

<span data-ttu-id="8731b-263">Elemento</span><span class="sxs-lookup"><span data-stu-id="8731b-263">Element</span></span> | <span data-ttu-id="8731b-264">Valor</span><span class="sxs-lookup"><span data-stu-id="8731b-264">Value</span></span>
------- | -----
<span data-ttu-id="8731b-265">coletores</span><span class="sxs-lookup"><span data-stu-id="8731b-265">sinks</span></span> | <span data-ttu-id="8731b-266">(opcional) Uma lista separada por vírgulas de nomes de coletores para os quais o LAD envia resultados de métricas agregadas.</span><span class="sxs-lookup"><span data-stu-id="8731b-266">(optional) A comma-separated list of names of sinks to which LAD sends aggregated metric results.</span></span> <span data-ttu-id="8731b-267">Todas as métricas agregadas são publicadas em cada coletor listado.</span><span class="sxs-lookup"><span data-stu-id="8731b-267">All aggregated metrics are published to each listed sink.</span></span> <span data-ttu-id="8731b-268">Veja [sinksConfig](#sinksconfig).</span><span class="sxs-lookup"><span data-stu-id="8731b-268">See [sinksConfig](#sinksconfig).</span></span> <span data-ttu-id="8731b-269">Exemplo: `"EHsink1, myjsonsink"`.</span><span class="sxs-lookup"><span data-stu-id="8731b-269">Example: `"EHsink1, myjsonsink"`.</span></span>
<span data-ttu-id="8731b-270">type</span><span class="sxs-lookup"><span data-stu-id="8731b-270">type</span></span> | <span data-ttu-id="8731b-271">Identifica o provedor real da métrica.</span><span class="sxs-lookup"><span data-stu-id="8731b-271">Identifies the actual provider of the metric.</span></span>
<span data-ttu-id="8731b-272">class</span><span class="sxs-lookup"><span data-stu-id="8731b-272">class</span></span> | <span data-ttu-id="8731b-273">Junto com "counter", identifica a métrica específica dentro do namespace do provedor.</span><span class="sxs-lookup"><span data-stu-id="8731b-273">Together with "counter", identifies the specific metric within the provider's namespace.</span></span>
<span data-ttu-id="8731b-274">contador</span><span class="sxs-lookup"><span data-stu-id="8731b-274">counter</span></span> | <span data-ttu-id="8731b-275">Junto com "class", identifica a métrica específica dentro do namespace do provedor.</span><span class="sxs-lookup"><span data-stu-id="8731b-275">Together with "class", identifies the specific metric within the provider's namespace.</span></span>
<span data-ttu-id="8731b-276">counterSpecifier</span><span class="sxs-lookup"><span data-stu-id="8731b-276">counterSpecifier</span></span> | <span data-ttu-id="8731b-277">Identifica a métrica específica dentro do namespace de Métricas do Azure.</span><span class="sxs-lookup"><span data-stu-id="8731b-277">Identifies the specific metric within the Azure Metrics namespace.</span></span>
<span data-ttu-id="8731b-278">condition</span><span class="sxs-lookup"><span data-stu-id="8731b-278">condition</span></span> | <span data-ttu-id="8731b-279">(opcional) Seleciona uma instância específica do objeto ao qual a métrica se aplica ou seleciona a agregação em todas as instâncias desse objeto.</span><span class="sxs-lookup"><span data-stu-id="8731b-279">(optional) Selects a specific instance of the object to which the metric applies or selects the aggregation across all instances of that object.</span></span> <span data-ttu-id="8731b-280">Para saber mais, veja as [`builtin` definições de métricas](#metrics-supported-by-builtin).</span><span class="sxs-lookup"><span data-stu-id="8731b-280">For more information, see the [`builtin` metric definitions](#metrics-supported-by-builtin).</span></span>
<span data-ttu-id="8731b-281">sampleRate</span><span class="sxs-lookup"><span data-stu-id="8731b-281">sampleRate</span></span> | <span data-ttu-id="8731b-282">O intervalo IS 8601 que define a taxa na qual as amostras brutas para esta métrica são coletados.</span><span class="sxs-lookup"><span data-stu-id="8731b-282">IS 8601 interval that sets the rate at which raw samples for this metric are collected.</span></span> <span data-ttu-id="8731b-283">Se não estiver definido, o intervalo de coleta será definido pelo valor de [sampleRateInSeconds](#ladcfg).</span><span class="sxs-lookup"><span data-stu-id="8731b-283">If not set, the collection interval is set by the value of [sampleRateInSeconds](#ladcfg).</span></span> <span data-ttu-id="8731b-284">A menor taxa de amostra com suporte é de 15 segundos (PT15S).</span><span class="sxs-lookup"><span data-stu-id="8731b-284">The shortest supported sample rate is 15 seconds (PT15S).</span></span>
<span data-ttu-id="8731b-285">unit</span><span class="sxs-lookup"><span data-stu-id="8731b-285">unit</span></span> | <span data-ttu-id="8731b-286">Deve ser uma destas cadeias de caracteres: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span><span class="sxs-lookup"><span data-stu-id="8731b-286">Should be one of these strings: "Count", "Bytes", "Seconds", "Percent", "CountPerSecond", "BytesPerSecond", "Millisecond".</span></span> <span data-ttu-id="8731b-287">Define a unidade para a métrica.</span><span class="sxs-lookup"><span data-stu-id="8731b-287">Defines the unit for the metric.</span></span> <span data-ttu-id="8731b-288">Os consumidores dos dados coletados esperam que os valores de dados coletados correspondam a essa unidade.</span><span class="sxs-lookup"><span data-stu-id="8731b-288">Consumers of the collected data expect the collected data values to match this unit.</span></span> <span data-ttu-id="8731b-289">O LAD ignora esse campo.</span><span class="sxs-lookup"><span data-stu-id="8731b-289">LAD ignores this field.</span></span>
<span data-ttu-id="8731b-290">displayName</span><span class="sxs-lookup"><span data-stu-id="8731b-290">displayName</span></span> | <span data-ttu-id="8731b-291">O rótulo (no idioma especificado pela configuração da localidade associada) a ser anexado a esses dados nas Métricas do Azure.</span><span class="sxs-lookup"><span data-stu-id="8731b-291">The label (in the language specified by the associated locale setting) to be attached to this data in Azure Metrics.</span></span> <span data-ttu-id="8731b-292">O LAD ignora esse campo.</span><span class="sxs-lookup"><span data-stu-id="8731b-292">LAD ignores this field.</span></span>

<span data-ttu-id="8731b-293">O counterSpecifier é um identificador arbitrário.</span><span class="sxs-lookup"><span data-stu-id="8731b-293">The counterSpecifier is an arbitrary identifier.</span></span> <span data-ttu-id="8731b-294">Os consumidores de métricas, como o gráfico do Portal do Azure e o recurso de alerta, usam o counterSpecifier como a "chave" que identifica uma métrica ou instância de uma métrica.</span><span class="sxs-lookup"><span data-stu-id="8731b-294">Consumers of metrics, like the Azure portal charting and alerting feature, use counterSpecifier as the "key" that identifies a metric or an instance of a metric.</span></span> <span data-ttu-id="8731b-295">Para as métricas `builtin`, é recomendável usar valores counterSpecifier que começam com `/builtin/`.</span><span class="sxs-lookup"><span data-stu-id="8731b-295">For `builtin` metrics, we recommend you use counterSpecifier values that begin with `/builtin/`.</span></span> <span data-ttu-id="8731b-296">Se você estiver coletando a instância específica de uma métrica, recomendamos anexar o identificador da instância para o valor de counterSpecifier.</span><span class="sxs-lookup"><span data-stu-id="8731b-296">If you are collecting a specific instance of a metric, we recommend you attach the identifier of the instance to the counterSpecifier value.</span></span> <span data-ttu-id="8731b-297">Alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="8731b-297">Some examples:</span></span>

* <span data-ttu-id="8731b-298">`/builtin/Processor/PercentIdleTime` – tempo ocioso médio de todos os núcleos</span><span class="sxs-lookup"><span data-stu-id="8731b-298">`/builtin/Processor/PercentIdleTime` - Idle time averaged across all cores</span></span>
* <span data-ttu-id="8731b-299">`/builtin/Disk/FreeSpace(/mnt)` – espaço livre para o sistema de arquivos /mnt</span><span class="sxs-lookup"><span data-stu-id="8731b-299">`/builtin/Disk/FreeSpace(/mnt)` - Free space for the /mnt filesystem</span></span>
* <span data-ttu-id="8731b-300">`/builtin/Disk/FreeSpace` – espaço livre com a média de todos os sistemas de arquivos montados</span><span class="sxs-lookup"><span data-stu-id="8731b-300">`/builtin/Disk/FreeSpace` - Free space averaged across all mounted filesystems</span></span>

<span data-ttu-id="8731b-301">Nem o LAD nem o Portal do Azure esperam que o valor counterSpecifier corresponda a qualquer padrão.</span><span class="sxs-lookup"><span data-stu-id="8731b-301">Neither LAD nor the Azure portal expects the counterSpecifier value to match any pattern.</span></span> <span data-ttu-id="8731b-302">Seja consistente no modo como você constrói valores counterSpecifier.</span><span class="sxs-lookup"><span data-stu-id="8731b-302">Be consistent in how you construct counterSpecifier values.</span></span>

<span data-ttu-id="8731b-303">Quando você especifica `performanceCounters`, o LAD sempre grava dados em uma tabela no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8731b-303">When you specify `performanceCounters`, LAD always writes data to a table in Azure storage.</span></span> <span data-ttu-id="8731b-304">Você pode ter os mesmos dados gravados em blobs JSON e/ou Hubs de Eventos, mas não é possível desabilitar o armazenamento de dados em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="8731b-304">You can have the same data written to JSON blobs and/or Event Hubs, but you cannot disable storing data to a table.</span></span> <span data-ttu-id="8731b-305">Todas as instâncias da extensão do diagnóstico configurado para usar o mesmo nome de conta de armazenamento e ponto de extremidade adicionam suas métricas e seus logs na mesma tabela.</span><span class="sxs-lookup"><span data-stu-id="8731b-305">All instances of the diagnostic extension configured to use the same storage account name and endpoint add their metrics and logs to the same table.</span></span> <span data-ttu-id="8731b-306">Se muitas VMs estiverem gravando na mesma partição de tabela, o Azure poderá limitar as gravações nessa partição.</span><span class="sxs-lookup"><span data-stu-id="8731b-306">If too many VMs are writing to the same table partition, Azure can throttle writes to that partition.</span></span> <span data-ttu-id="8731b-307">A configuração eventVolume faz as entradas serem distribuídas entre 1 (pequeno), 10 (médio) ou 100 (grande) partições diferentes.</span><span class="sxs-lookup"><span data-stu-id="8731b-307">The eventVolume setting causes entries to be spread across 1 (Small), 10 (Medium), or 100 (Large) different partitions.</span></span> <span data-ttu-id="8731b-308">Normalmente, "médio" é suficiente para garantir que o tráfego não seja limitado.</span><span class="sxs-lookup"><span data-stu-id="8731b-308">Usually, "Medium" is sufficient to ensure traffic is not throttled.</span></span> <span data-ttu-id="8731b-309">O recurso de Métricas do Azure do Portal do Azure usa os dados nesta tabela para gerar gráficos ou disparar alertas.</span><span class="sxs-lookup"><span data-stu-id="8731b-309">The Azure Metrics feature of the Azure portal uses the data in this table to produce graphs or to trigger alerts.</span></span> <span data-ttu-id="8731b-310">O nome da tabela é a concatenação dessas cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="8731b-310">The table name is the concatenation of these strings:</span></span>

* `WADMetrics`
* <span data-ttu-id="8731b-311">O "scheduledTransferPeriod" para os valores agregados armazenados na tabela</span><span class="sxs-lookup"><span data-stu-id="8731b-311">The "scheduledTransferPeriod" for the aggregated values stored in the table</span></span>
* `P10DV2S`
* <span data-ttu-id="8731b-312">Uma data, na forma "AAAAMMDD", que é alterada a cada 10 dias</span><span class="sxs-lookup"><span data-stu-id="8731b-312">A date, in the form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="8731b-313">Os exemplos incluem `WADMetricsPT1HP10DV2S20170410` e `WADMetricsPT1MP10DV2S20170609`.</span><span class="sxs-lookup"><span data-stu-id="8731b-313">Examples include `WADMetricsPT1HP10DV2S20170410` and `WADMetricsPT1MP10DV2S20170609`.</span></span>

#### <a name="syslogevents"></a><span data-ttu-id="8731b-314">syslogEvents</span><span class="sxs-lookup"><span data-stu-id="8731b-314">syslogEvents</span></span>

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

<span data-ttu-id="8731b-315">Essa seção opcional controla a coleção de eventos de log do syslog.</span><span class="sxs-lookup"><span data-stu-id="8731b-315">This optional section controls the collection of log events from syslog.</span></span> <span data-ttu-id="8731b-316">Se a seção for omitida, os eventos de syslog não serão capturados.</span><span class="sxs-lookup"><span data-stu-id="8731b-316">If the section is omitted, syslog events are not captured at all.</span></span>

<span data-ttu-id="8731b-317">A coleção syslogEventConfiguration tem uma entrada para cada instalação de syslog de interesse.</span><span class="sxs-lookup"><span data-stu-id="8731b-317">The syslogEventConfiguration collection has one entry for each syslog facility of interest.</span></span> <span data-ttu-id="8731b-318">Se minSeverity for "NENHUM" para um recurso específico, ou se o recurso não aparecer no elemento, nenhum evento desse recurso será capturado.</span><span class="sxs-lookup"><span data-stu-id="8731b-318">If minSeverity is "NONE" for a particular facility, or if that facility does not appear in the element at all, no events from that facility are captured.</span></span>

<span data-ttu-id="8731b-319">Elemento</span><span class="sxs-lookup"><span data-stu-id="8731b-319">Element</span></span> | <span data-ttu-id="8731b-320">Valor</span><span class="sxs-lookup"><span data-stu-id="8731b-320">Value</span></span>
------- | -----
<span data-ttu-id="8731b-321">coletores</span><span class="sxs-lookup"><span data-stu-id="8731b-321">sinks</span></span> | <span data-ttu-id="8731b-322">Uma lista separada por vírgulas de nomes de coletores nos quais os eventos de log individuais são publicados.</span><span class="sxs-lookup"><span data-stu-id="8731b-322">A comma-separated list of names of sinks to which individual log events are published.</span></span> <span data-ttu-id="8731b-323">Todos os eventos de log correspondentes às restrições em syslogEventConfiguration são publicados em cada coletor listado.</span><span class="sxs-lookup"><span data-stu-id="8731b-323">All log events matching the restrictions in syslogEventConfiguration are published to each listed sink.</span></span> <span data-ttu-id="8731b-324">Exemplo: "EHforsyslog"</span><span class="sxs-lookup"><span data-stu-id="8731b-324">Example: "EHforsyslog"</span></span>
<span data-ttu-id="8731b-325">facilityName</span><span class="sxs-lookup"><span data-stu-id="8731b-325">facilityName</span></span> | <span data-ttu-id="8731b-326">Um nome de recurso de syslog (como "LOG\_USER" ou "LOG\_LOCAL0").</span><span class="sxs-lookup"><span data-stu-id="8731b-326">A syslog facility name (such as "LOG\_USER" or "LOG\_LOCAL0").</span></span> <span data-ttu-id="8731b-327">Veja a seção "facility" da [página de manual do syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) para obter a lista completa.</span><span class="sxs-lookup"><span data-stu-id="8731b-327">See the "facility" section of the [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for the full list.</span></span>
<span data-ttu-id="8731b-328">minSeverity</span><span class="sxs-lookup"><span data-stu-id="8731b-328">minSeverity</span></span> | <span data-ttu-id="8731b-329">Um nível de severidade de syslog (como "LOG\_ERR" ou "LOG\_INFO").</span><span class="sxs-lookup"><span data-stu-id="8731b-329">A syslog severity level (such as "LOG\_ERR" or "LOG\_INFO").</span></span> <span data-ttu-id="8731b-330">Veja a seção "level" da [página de manual do syslog](http://man7.org/linux/man-pages/man3/syslog.3.html) para obter a lista completa.</span><span class="sxs-lookup"><span data-stu-id="8731b-330">See the "level" section of the [syslog man page](http://man7.org/linux/man-pages/man3/syslog.3.html) for the full list.</span></span> <span data-ttu-id="8731b-331">A extensão de captura eventos enviados para o recurso em ou acima do nível especificado.</span><span class="sxs-lookup"><span data-stu-id="8731b-331">The extension captures events sent to the facility at or above the specified level.</span></span>

<span data-ttu-id="8731b-332">Quando você especifica `syslogEvents`, o LAD sempre grava dados em uma tabela no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8731b-332">When you specify `syslogEvents`, LAD always writes data to a table in Azure storage.</span></span> <span data-ttu-id="8731b-333">Você pode ter os mesmos dados gravados em blobs JSON e/ou Hubs de Eventos, mas não é possível desabilitar o armazenamento de dados em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="8731b-333">You can have the same data written to JSON blobs and/or Event Hubs, but you cannot disable storing data to a table.</span></span> <span data-ttu-id="8731b-334">O comportamento de particionamento para essa tabela é o mesmo descrito para `performanceCounters`.</span><span class="sxs-lookup"><span data-stu-id="8731b-334">The partitioning behavior for this table is the same as described for `performanceCounters`.</span></span> <span data-ttu-id="8731b-335">O nome da tabela é a concatenação dessas cadeias de caracteres:</span><span class="sxs-lookup"><span data-stu-id="8731b-335">The table name is the concatenation of these strings:</span></span>

* `LinuxSyslog`
* <span data-ttu-id="8731b-336">Uma data, na forma "AAAAMMDD", que é alterada a cada 10 dias</span><span class="sxs-lookup"><span data-stu-id="8731b-336">A date, in the form "YYYYMMDD", which changes every 10 days</span></span>

<span data-ttu-id="8731b-337">Os exemplos incluem `LinuxSyslog20170410` e `LinuxSyslog20170609`.</span><span class="sxs-lookup"><span data-stu-id="8731b-337">Examples include `LinuxSyslog20170410` and `LinuxSyslog20170609`.</span></span>

### <a name="perfcfg"></a><span data-ttu-id="8731b-338">perfCfg</span><span class="sxs-lookup"><span data-stu-id="8731b-338">perfCfg</span></span>

<span data-ttu-id="8731b-339">Essa seção controla a execução de consultas [OMI](https://github.com/Microsoft/omi) arbitrárias.</span><span class="sxs-lookup"><span data-stu-id="8731b-339">This optional section controls execution of arbitrary [OMI](https://github.com/Microsoft/omi) queries.</span></span>

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

<span data-ttu-id="8731b-340">Elemento</span><span class="sxs-lookup"><span data-stu-id="8731b-340">Element</span></span> | <span data-ttu-id="8731b-341">Valor</span><span class="sxs-lookup"><span data-stu-id="8731b-341">Value</span></span>
------- | -----
<span data-ttu-id="8731b-342">namespace</span><span class="sxs-lookup"><span data-stu-id="8731b-342">namespace</span></span> | <span data-ttu-id="8731b-343">(opcional) O namespace OMI dentro do qual a consulta deve ser executada.</span><span class="sxs-lookup"><span data-stu-id="8731b-343">(optional) The OMI namespace within which the query should be executed.</span></span> <span data-ttu-id="8731b-344">Se não for especificado, o valor padrão será "root/scx", implementado pelos [Provedores de várias plataformas do System Center](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span><span class="sxs-lookup"><span data-stu-id="8731b-344">If unspecified, the default value is "root/scx", implemented by the [System Center Cross-platform Providers](http://scx.codeplex.com/wikipage?title=xplatproviders&referringTitle=Documentation).</span></span>
<span data-ttu-id="8731b-345">query</span><span class="sxs-lookup"><span data-stu-id="8731b-345">query</span></span> | <span data-ttu-id="8731b-346">A consulta OMI a ser executada.</span><span class="sxs-lookup"><span data-stu-id="8731b-346">The OMI query to be executed.</span></span>
<span data-ttu-id="8731b-347">tabela</span><span class="sxs-lookup"><span data-stu-id="8731b-347">table</span></span> | <span data-ttu-id="8731b-348">(opcional) A tabela de armazenamento do Azure, na conta de armazenamento designada (veja [Configurações protegidas](#protected-settings)).</span><span class="sxs-lookup"><span data-stu-id="8731b-348">(optional) The Azure storage table, in the designated storage account (see [Protected settings](#protected-settings)).</span></span>
<span data-ttu-id="8731b-349">frequência</span><span class="sxs-lookup"><span data-stu-id="8731b-349">frequency</span></span> | <span data-ttu-id="8731b-350">(opcional) O número de segundos entre a execução da consulta.</span><span class="sxs-lookup"><span data-stu-id="8731b-350">(optional) The number of seconds between execution of the query.</span></span> <span data-ttu-id="8731b-351">O valor padrão é 300 (5 minutos); o valor mínimo é de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="8731b-351">Default value is 300 (5 minutes); minimum value is 15 seconds.</span></span>
<span data-ttu-id="8731b-352">coletores</span><span class="sxs-lookup"><span data-stu-id="8731b-352">sinks</span></span> | <span data-ttu-id="8731b-353">(opcional) Uma lista separada por vírgulas de nomes de coletores adicionais para os quais os resultados brutos de métricas de amostras devem ser publicados.</span><span class="sxs-lookup"><span data-stu-id="8731b-353">(optional) A comma-separated list of names of additional sinks to which raw sample metric results should be published.</span></span> <span data-ttu-id="8731b-354">Nenhuma agregação desses exemplos brutos é calculada pela extensão ou Métricas do Azure.</span><span class="sxs-lookup"><span data-stu-id="8731b-354">No aggregation of these raw samples is computed by the extension or by Azure Metrics.</span></span>

<span data-ttu-id="8731b-355">As informações de "tabela" ou "coletores" ou de ambos devem ser especificadas.</span><span class="sxs-lookup"><span data-stu-id="8731b-355">Either "table" or "sinks", or both, must be specified.</span></span>

### <a name="filelogs"></a><span data-ttu-id="8731b-356">fileLogs</span><span class="sxs-lookup"><span data-stu-id="8731b-356">fileLogs</span></span>

<span data-ttu-id="8731b-357">Controla a captura de arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="8731b-357">Controls the capture of log files.</span></span> <span data-ttu-id="8731b-358">O LAD captura novas linhas de texto, como elas são gravadas no arquivo e as grava em linhas da tabela e/ou qualquer coletor especificado (JsonBlob ou EventHub).</span><span class="sxs-lookup"><span data-stu-id="8731b-358">LAD captures new text lines as they are written to the file and writes them to table rows and/or any specified sinks (JsonBlob or EventHub).</span></span>

```json
"fileLogs": [
    {
        "file": "/var/log/mydaemonlog",
        "table": "MyDaemonEvents",
        "sinks": ""
    }
]
```

<span data-ttu-id="8731b-359">Elemento</span><span class="sxs-lookup"><span data-stu-id="8731b-359">Element</span></span> | <span data-ttu-id="8731b-360">Valor</span><span class="sxs-lookup"><span data-stu-id="8731b-360">Value</span></span>
------- | -----
<span data-ttu-id="8731b-361">file</span><span class="sxs-lookup"><span data-stu-id="8731b-361">file</span></span> | <span data-ttu-id="8731b-362">O nome de caminho completo do arquivo de log a ser observado e capturado.</span><span class="sxs-lookup"><span data-stu-id="8731b-362">The full pathname of the log file to be watched and captured.</span></span> <span data-ttu-id="8731b-363">O nome do caminho deve nomear um único arquivo; ele não pode nomear um diretório ou conter curingas.</span><span class="sxs-lookup"><span data-stu-id="8731b-363">The pathname must name a single file; it cannot name a directory or contain wildcards.</span></span>
<span data-ttu-id="8731b-364">tabela</span><span class="sxs-lookup"><span data-stu-id="8731b-364">table</span></span> | <span data-ttu-id="8731b-365">(opcional) A tabela de armazenamento do Azure, na conta de armazenamento designada (conforme especificado na configuração protegida), na qual novas linhas depois do "final" do arquivo são gravadas.</span><span class="sxs-lookup"><span data-stu-id="8731b-365">(optional) The Azure storage table, in the designated storage account (as specified in the protected configuration), into which new lines from the "tail" of the file are written.</span></span>
<span data-ttu-id="8731b-366">coletores</span><span class="sxs-lookup"><span data-stu-id="8731b-366">sinks</span></span> | <span data-ttu-id="8731b-367">(opcional) Uma lista separada por vírgulas de nomes de coletores adicionais para os quais as linhas de log são enviadas.</span><span class="sxs-lookup"><span data-stu-id="8731b-367">(optional) A comma-separated list of names of additional sinks to which log lines sent.</span></span>

<span data-ttu-id="8731b-368">As informações de "tabela" ou "coletores" ou de ambos devem ser especificadas.</span><span class="sxs-lookup"><span data-stu-id="8731b-368">Either "table" or "sinks", or both, must be specified.</span></span>

## <a name="metrics-supported-by-the-builtin-provider"></a><span data-ttu-id="8731b-369">Métricas com suporte do provedor interno</span><span class="sxs-lookup"><span data-stu-id="8731b-369">Metrics supported by the builtin provider</span></span>

<span data-ttu-id="8731b-370">O provedor interno de métricas é uma fonte de métricas mais interessante para um amplo conjunto de usuários.</span><span class="sxs-lookup"><span data-stu-id="8731b-370">The builtin metric provider is a source of metrics most interesting to a broad set of users.</span></span> <span data-ttu-id="8731b-371">Essas métricas enquadram-se em cinco classes amplas:</span><span class="sxs-lookup"><span data-stu-id="8731b-371">These metrics fall into five broad classes:</span></span>

* <span data-ttu-id="8731b-372">Processador</span><span class="sxs-lookup"><span data-stu-id="8731b-372">Processor</span></span>
* <span data-ttu-id="8731b-373">Memória</span><span class="sxs-lookup"><span data-stu-id="8731b-373">Memory</span></span>
* <span data-ttu-id="8731b-374">Rede</span><span class="sxs-lookup"><span data-stu-id="8731b-374">Network</span></span>
* <span data-ttu-id="8731b-375">Filesystem</span><span class="sxs-lookup"><span data-stu-id="8731b-375">Filesystem</span></span>
* <span data-ttu-id="8731b-376">Disco</span><span class="sxs-lookup"><span data-stu-id="8731b-376">Disk</span></span>

### <a name="builtin-metrics-for-the-processor-class"></a><span data-ttu-id="8731b-377">métricas internas para a classe Processor</span><span class="sxs-lookup"><span data-stu-id="8731b-377">builtin metrics for the Processor class</span></span>

<span data-ttu-id="8731b-378">A classe de métricas Processor fornece informações sobre o uso do processador na VM.</span><span class="sxs-lookup"><span data-stu-id="8731b-378">The Processor class of metrics provides information about processor usage in the VM.</span></span> <span data-ttu-id="8731b-379">Ao agregar porcentagens, o resultado é a média em todas as CPUs.</span><span class="sxs-lookup"><span data-stu-id="8731b-379">When aggregating percentages, the result is the average across all CPUs.</span></span> <span data-ttu-id="8731b-380">Em uma VM de dois núcleos, se um núcleo estiver 100% ocupado e o outro 100% ocioso, o PercentIdleTime relatado seria 50.</span><span class="sxs-lookup"><span data-stu-id="8731b-380">In a two core VM, if one core was 100% busy and the other was 100% idle, the reported PercentIdleTime would be 50.</span></span> <span data-ttu-id="8731b-381">Se cada núcleo estiver 50% ocupado para o mesmo período, o resultado relatado também seria 50.</span><span class="sxs-lookup"><span data-stu-id="8731b-381">If each core was 50% busy for the same period, the reported result would also be 50.</span></span> <span data-ttu-id="8731b-382">Em uma VM de quatro núcleos, com um núcleo 100% ocupado e o outro ocioso, o PercentIdleTime relatado seria 75.</span><span class="sxs-lookup"><span data-stu-id="8731b-382">In a four core VM, with one core 100% busy and the others idle, the reported PercentIdleTime would be 75.</span></span>

<span data-ttu-id="8731b-383">contador</span><span class="sxs-lookup"><span data-stu-id="8731b-383">counter</span></span> | <span data-ttu-id="8731b-384">Significado</span><span class="sxs-lookup"><span data-stu-id="8731b-384">Meaning</span></span>
------- | -------
<span data-ttu-id="8731b-385">PercentIdleTime</span><span class="sxs-lookup"><span data-stu-id="8731b-385">PercentIdleTime</span></span> | <span data-ttu-id="8731b-386">Porcentagem de tempo durante a janela de agregação que os processadores estavam executando o loop ocioso do kernel</span><span class="sxs-lookup"><span data-stu-id="8731b-386">Percentage of time during the aggregation window that processors were executing the kernel idle loop</span></span>
<span data-ttu-id="8731b-387">PercentProcessorTime</span><span class="sxs-lookup"><span data-stu-id="8731b-387">PercentProcessorTime</span></span> | <span data-ttu-id="8731b-388">Porcentagem de tempo de execução de um thread não ocioso</span><span class="sxs-lookup"><span data-stu-id="8731b-388">Percentage of time executing a non-idle thread</span></span>
<span data-ttu-id="8731b-389">PercentIOWaitTime</span><span class="sxs-lookup"><span data-stu-id="8731b-389">PercentIOWaitTime</span></span> | <span data-ttu-id="8731b-390">Porcentagem de tempo esperando a conclusão das operações de E/S</span><span class="sxs-lookup"><span data-stu-id="8731b-390">Percentage of time waiting for IO operations to complete</span></span>
<span data-ttu-id="8731b-391">PercentInterruptTime</span><span class="sxs-lookup"><span data-stu-id="8731b-391">PercentInterruptTime</span></span> | <span data-ttu-id="8731b-392">Porcentagem de tempo de execução de interrupções de hardware/software e DPCs (chamadas de procedimento deferidas)</span><span class="sxs-lookup"><span data-stu-id="8731b-392">Percentage of time executing hardware/software interrupts and DPCs (deferred procedure calls)</span></span>
<span data-ttu-id="8731b-393">PercentUserTime</span><span class="sxs-lookup"><span data-stu-id="8731b-393">PercentUserTime</span></span> | <span data-ttu-id="8731b-394">De tempo não ocioso durante a janela de agregação, a porcentagem de tempo gasto no usuário mais em prioridade normal</span><span class="sxs-lookup"><span data-stu-id="8731b-394">Of non-idle time during the aggregation window, the percentage of time spent in user more at normal priority</span></span>
<span data-ttu-id="8731b-395">PercentNiceTime</span><span class="sxs-lookup"><span data-stu-id="8731b-395">PercentNiceTime</span></span> | <span data-ttu-id="8731b-396">De tempo não ocioso, a porcentagem gasta em prioridade diminuída (boa)</span><span class="sxs-lookup"><span data-stu-id="8731b-396">Of non-idle time, the percentage spent at lowered (nice) priority</span></span>
<span data-ttu-id="8731b-397">PercentPrivilegedTime</span><span class="sxs-lookup"><span data-stu-id="8731b-397">PercentPrivilegedTime</span></span> | <span data-ttu-id="8731b-398">De tempo não ocioso, a porcentagem gasta em modo privilegiado (kernel)</span><span class="sxs-lookup"><span data-stu-id="8731b-398">Of non-idle time, the percentage spent in privileged (kernel) mode</span></span>

<span data-ttu-id="8731b-399">Os primeiros quatro contadores devem somar 100%.</span><span class="sxs-lookup"><span data-stu-id="8731b-399">The first four counters should sum to 100%.</span></span> <span data-ttu-id="8731b-400">Os três últimos contadores também somam 100%; eles subdividem a soma de PercentProcessorTime, PercentIOWaitTime e PercentInterruptTime.</span><span class="sxs-lookup"><span data-stu-id="8731b-400">The last three counters also sum to 100%; they subdivide the sum of PercentProcessorTime, PercentIOWaitTime, and PercentInterruptTime.</span></span>

<span data-ttu-id="8731b-401">Para obter uma única métrica agregada em todos os processadores, defina `"condition": "IsAggregate=TRUE"`.</span><span class="sxs-lookup"><span data-stu-id="8731b-401">To obtain a single metric aggregated across all processors, set `"condition": "IsAggregate=TRUE"`.</span></span> <span data-ttu-id="8731b-402">Para obter uma métrica para um processador específico, como o segundo processador lógico de uma VM de quatro núcleos, defina `"condition": "Name=\\"1\\""`.</span><span class="sxs-lookup"><span data-stu-id="8731b-402">To obtain a metric for a specific processor, such as the second logical processor of a four core VM, set `"condition": "Name=\\"1\\""`.</span></span> <span data-ttu-id="8731b-403">Os números de processadores lógicos estão no intervalo `[0..n-1]`.</span><span class="sxs-lookup"><span data-stu-id="8731b-403">Logical processor numbers are in the range `[0..n-1]`.</span></span>

### <a name="builtin-metrics-for-the-memory-class"></a><span data-ttu-id="8731b-404">métricas internas para a classe Memory</span><span class="sxs-lookup"><span data-stu-id="8731b-404">builtin metrics for the Memory class</span></span>

<span data-ttu-id="8731b-405">A classe de métricas Memory fornece informações sobre a utilização de memória, paginação e troca.</span><span class="sxs-lookup"><span data-stu-id="8731b-405">The Memory class of metrics provides information about memory utilization, paging, and swapping.</span></span>

<span data-ttu-id="8731b-406">contador</span><span class="sxs-lookup"><span data-stu-id="8731b-406">counter</span></span> | <span data-ttu-id="8731b-407">Significado</span><span class="sxs-lookup"><span data-stu-id="8731b-407">Meaning</span></span>
------- | -------
<span data-ttu-id="8731b-408">AvailableMemory</span><span class="sxs-lookup"><span data-stu-id="8731b-408">AvailableMemory</span></span> | <span data-ttu-id="8731b-409">Memória física disponível em MiB</span><span class="sxs-lookup"><span data-stu-id="8731b-409">Available physical memory in MiB</span></span>
<span data-ttu-id="8731b-410">PercentAvailableMemory</span><span class="sxs-lookup"><span data-stu-id="8731b-410">PercentAvailableMemory</span></span> | <span data-ttu-id="8731b-411">Memória física disponível como uma porcentagem da memória total</span><span class="sxs-lookup"><span data-stu-id="8731b-411">Available physical memory as a percent of total memory</span></span>
<span data-ttu-id="8731b-412">UsedMemory</span><span class="sxs-lookup"><span data-stu-id="8731b-412">UsedMemory</span></span> | <span data-ttu-id="8731b-413">Memória física em uso (MiB)</span><span class="sxs-lookup"><span data-stu-id="8731b-413">In-use physical memory (MiB)</span></span>
<span data-ttu-id="8731b-414">PercentUsedMemory</span><span class="sxs-lookup"><span data-stu-id="8731b-414">PercentUsedMemory</span></span> | <span data-ttu-id="8731b-415">Memória física em uso como uma porcentagem da memória total</span><span class="sxs-lookup"><span data-stu-id="8731b-415">In-use physical memory as a percent of total memory</span></span>
<span data-ttu-id="8731b-416">PagesPerSec</span><span class="sxs-lookup"><span data-stu-id="8731b-416">PagesPerSec</span></span> | <span data-ttu-id="8731b-417">Paginação total (leitura/gravação)</span><span class="sxs-lookup"><span data-stu-id="8731b-417">Total paging (read/write)</span></span>
<span data-ttu-id="8731b-418">PagesReadPerSec</span><span class="sxs-lookup"><span data-stu-id="8731b-418">PagesReadPerSec</span></span> | <span data-ttu-id="8731b-419">Páginas lidas do repositório de backup (arquivo de permuta, arquivo de programa, arquivo mapeado etc.)</span><span class="sxs-lookup"><span data-stu-id="8731b-419">Pages read from backing store (swap file, program file, mapped file, etc.)</span></span>
<span data-ttu-id="8731b-420">PagesWrittenPerSec</span><span class="sxs-lookup"><span data-stu-id="8731b-420">PagesWrittenPerSec</span></span> | <span data-ttu-id="8731b-421">Páginas gravadas no armazenamento de backup (arquivo de permuta, arquivo mapeado etc.)</span><span class="sxs-lookup"><span data-stu-id="8731b-421">Pages written to backing store (swap file, mapped file, etc.)</span></span>
<span data-ttu-id="8731b-422">AvailableSwap</span><span class="sxs-lookup"><span data-stu-id="8731b-422">AvailableSwap</span></span> | <span data-ttu-id="8731b-423">Espaço de permuta não utilizado (MiB)</span><span class="sxs-lookup"><span data-stu-id="8731b-423">Unused swap space (MiB)</span></span>
<span data-ttu-id="8731b-424">PercentAvailableSwap</span><span class="sxs-lookup"><span data-stu-id="8731b-424">PercentAvailableSwap</span></span> | <span data-ttu-id="8731b-425">Espaço de troca não utilizado como uma porcentagem da troca total</span><span class="sxs-lookup"><span data-stu-id="8731b-425">Unused swap space as a percentage of total swap</span></span>
<span data-ttu-id="8731b-426">UsedSwap</span><span class="sxs-lookup"><span data-stu-id="8731b-426">UsedSwap</span></span> | <span data-ttu-id="8731b-427">Espaço de troca em uso (MiB)</span><span class="sxs-lookup"><span data-stu-id="8731b-427">In-use swap space (MiB)</span></span>
<span data-ttu-id="8731b-428">PercentUsedSwap</span><span class="sxs-lookup"><span data-stu-id="8731b-428">PercentUsedSwap</span></span> | <span data-ttu-id="8731b-429">Espaço de troca em uso como uma porcentagem da troca total</span><span class="sxs-lookup"><span data-stu-id="8731b-429">In-use swap space as a percentage of total swap</span></span>

<span data-ttu-id="8731b-430">Essa classe de métricas tem apenas uma única instância.</span><span class="sxs-lookup"><span data-stu-id="8731b-430">This class of metrics has only a single instance.</span></span> <span data-ttu-id="8731b-431">O atributo "condição" não tem configurações úteis e deve ser omitido.</span><span class="sxs-lookup"><span data-stu-id="8731b-431">The "condition" attribute has no useful settings and should be omitted.</span></span>

### <a name="builtin-metrics-for-the-network-class"></a><span data-ttu-id="8731b-432">métricas internas para a classe Network</span><span class="sxs-lookup"><span data-stu-id="8731b-432">builtin metrics for the Network class</span></span>

<span data-ttu-id="8731b-433">A classe de métricas Network fornece informações sobre a atividade de rede em adaptadores de rede individuais desde a inicialização.</span><span class="sxs-lookup"><span data-stu-id="8731b-433">The Network class of metrics provides information about network activity on an individual network interfaces since boot.</span></span> <span data-ttu-id="8731b-434">O LAD não expõe as métricas de largura de banda, que podem ser recuperadas de métricas de host.</span><span class="sxs-lookup"><span data-stu-id="8731b-434">LAD does not expose bandwidth metrics, which can be retrieved from host metrics.</span></span>

<span data-ttu-id="8731b-435">contador</span><span class="sxs-lookup"><span data-stu-id="8731b-435">counter</span></span> | <span data-ttu-id="8731b-436">Significado</span><span class="sxs-lookup"><span data-stu-id="8731b-436">Meaning</span></span>
------- | -------
<span data-ttu-id="8731b-437">BytesTransmitted</span><span class="sxs-lookup"><span data-stu-id="8731b-437">BytesTransmitted</span></span> | <span data-ttu-id="8731b-438">Total de bytes enviados desde a inicialização</span><span class="sxs-lookup"><span data-stu-id="8731b-438">Total bytes sent since boot</span></span>
<span data-ttu-id="8731b-439">BytesReceived</span><span class="sxs-lookup"><span data-stu-id="8731b-439">BytesReceived</span></span> | <span data-ttu-id="8731b-440">Total de bytes recebidos desde a inicialização</span><span class="sxs-lookup"><span data-stu-id="8731b-440">Total bytes received since boot</span></span>
<span data-ttu-id="8731b-441">BytesTotal</span><span class="sxs-lookup"><span data-stu-id="8731b-441">BytesTotal</span></span> | <span data-ttu-id="8731b-442">Total de bytes enviados ou recebidos desde a inicialização</span><span class="sxs-lookup"><span data-stu-id="8731b-442">Total bytes sent or received since boot</span></span>
<span data-ttu-id="8731b-443">PacketsTransmitted</span><span class="sxs-lookup"><span data-stu-id="8731b-443">PacketsTransmitted</span></span> | <span data-ttu-id="8731b-444">Total de pacotes enviados desde a inicialização</span><span class="sxs-lookup"><span data-stu-id="8731b-444">Total packets sent since boot</span></span>
<span data-ttu-id="8731b-445">PacketsReceived</span><span class="sxs-lookup"><span data-stu-id="8731b-445">PacketsReceived</span></span> | <span data-ttu-id="8731b-446">Total de pacotes recebidos desde a inicialização</span><span class="sxs-lookup"><span data-stu-id="8731b-446">Total packets received since boot</span></span>
<span data-ttu-id="8731b-447">TotalRxErrors</span><span class="sxs-lookup"><span data-stu-id="8731b-447">TotalRxErrors</span></span> | <span data-ttu-id="8731b-448">Número de erros de recebimento desde a inicialização</span><span class="sxs-lookup"><span data-stu-id="8731b-448">Number of receive errors since boot</span></span>
<span data-ttu-id="8731b-449">TotalTxErrors</span><span class="sxs-lookup"><span data-stu-id="8731b-449">TotalTxErrors</span></span> | <span data-ttu-id="8731b-450">Número de erros de transmissão desde a inicialização</span><span class="sxs-lookup"><span data-stu-id="8731b-450">Number of transmit errors since boot</span></span>
<span data-ttu-id="8731b-451">TotalCollisions</span><span class="sxs-lookup"><span data-stu-id="8731b-451">TotalCollisions</span></span> | <span data-ttu-id="8731b-452">Número de colisões relatadas pelas portas de rede desde a inicialização</span><span class="sxs-lookup"><span data-stu-id="8731b-452">Number of collisions reported by the network ports since boot</span></span>

 <span data-ttu-id="8731b-453">Embora essa classe seja instanciada, o LAD não oferece suporte à captura de métricas Network agregadas em todos os dispositivos de rede.</span><span class="sxs-lookup"><span data-stu-id="8731b-453">Although this class is instanced, LAD does not support capturing Network metrics aggregated across all network devices.</span></span> <span data-ttu-id="8731b-454">Para obter a métrica para uma interface específica, como eth0, defina `"condition": "InstanceID=\\"eth0\\""`.</span><span class="sxs-lookup"><span data-stu-id="8731b-454">To obtain the metrics for a specific interface, such as eth0, set `"condition": "InstanceID=\\"eth0\\""`.</span></span>

### <a name="builtin-metrics-for-the-filesystem-class"></a><span data-ttu-id="8731b-455">métricas internas para a classe Filesystem</span><span class="sxs-lookup"><span data-stu-id="8731b-455">builtin metrics for the Filesystem class</span></span>

<span data-ttu-id="8731b-456">A classe de métricas Filesystem fornece informações sobre o uso do sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="8731b-456">The Filesystem class of metrics provides information about filesystem usage.</span></span> <span data-ttu-id="8731b-457">Valores absolutos e porcentagem são relatados como seriam exibidos para um usuário comum (não raiz).</span><span class="sxs-lookup"><span data-stu-id="8731b-457">Absolute and percentage values are reported as they'd be displayed to an ordinary user (not root).</span></span>

<span data-ttu-id="8731b-458">contador</span><span class="sxs-lookup"><span data-stu-id="8731b-458">counter</span></span> | <span data-ttu-id="8731b-459">Significado</span><span class="sxs-lookup"><span data-stu-id="8731b-459">Meaning</span></span>
------- | -------
<span data-ttu-id="8731b-460">FreeSpace</span><span class="sxs-lookup"><span data-stu-id="8731b-460">FreeSpace</span></span> | <span data-ttu-id="8731b-461">Espaço em disco disponível em bytes</span><span class="sxs-lookup"><span data-stu-id="8731b-461">Available disk space in bytes</span></span>
<span data-ttu-id="8731b-462">UsedSpace</span><span class="sxs-lookup"><span data-stu-id="8731b-462">UsedSpace</span></span> | <span data-ttu-id="8731b-463">Espaço em disco usado em bytes</span><span class="sxs-lookup"><span data-stu-id="8731b-463">Used disk space in bytes</span></span>
<span data-ttu-id="8731b-464">PercentFreeSpace</span><span class="sxs-lookup"><span data-stu-id="8731b-464">PercentFreeSpace</span></span> | <span data-ttu-id="8731b-465">Porcentagem de espaço livre</span><span class="sxs-lookup"><span data-stu-id="8731b-465">Percentage free space</span></span>
<span data-ttu-id="8731b-466">PercentUsedSpace</span><span class="sxs-lookup"><span data-stu-id="8731b-466">PercentUsedSpace</span></span> | <span data-ttu-id="8731b-467">Porcentagem de espaço usado</span><span class="sxs-lookup"><span data-stu-id="8731b-467">Percentage used space</span></span>
<span data-ttu-id="8731b-468">PercentFreeInodes</span><span class="sxs-lookup"><span data-stu-id="8731b-468">PercentFreeInodes</span></span> | <span data-ttu-id="8731b-469">Porcentagem de inodes não utilizados</span><span class="sxs-lookup"><span data-stu-id="8731b-469">Percentage of unused inodes</span></span>
<span data-ttu-id="8731b-470">PercentUsedInodes</span><span class="sxs-lookup"><span data-stu-id="8731b-470">PercentUsedInodes</span></span> | <span data-ttu-id="8731b-471">Porcentagem de inodes alocados (em uso) somados em todos os sistemas de arquivos</span><span class="sxs-lookup"><span data-stu-id="8731b-471">Percentage of allocated (in use) inodes summed across all filesystems</span></span>
<span data-ttu-id="8731b-472">BytesReadPerSecond</span><span class="sxs-lookup"><span data-stu-id="8731b-472">BytesReadPerSecond</span></span> | <span data-ttu-id="8731b-473">Bytes lidos por segundo</span><span class="sxs-lookup"><span data-stu-id="8731b-473">Bytes read per second</span></span>
<span data-ttu-id="8731b-474">BytesWrittenPerSecond</span><span class="sxs-lookup"><span data-stu-id="8731b-474">BytesWrittenPerSecond</span></span> | <span data-ttu-id="8731b-475">Bytes gravados por segundo</span><span class="sxs-lookup"><span data-stu-id="8731b-475">Bytes written per second</span></span>
<span data-ttu-id="8731b-476">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="8731b-476">BytesPerSecond</span></span> | <span data-ttu-id="8731b-477">Bytes lido ou gravados por segundo</span><span class="sxs-lookup"><span data-stu-id="8731b-477">Bytes read or written per second</span></span>
<span data-ttu-id="8731b-478">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="8731b-478">ReadsPerSecond</span></span> | <span data-ttu-id="8731b-479">Operações de leitura por segundo</span><span class="sxs-lookup"><span data-stu-id="8731b-479">Read operations per second</span></span>
<span data-ttu-id="8731b-480">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="8731b-480">WritesPerSecond</span></span> | <span data-ttu-id="8731b-481">Operações de gravação por segundo</span><span class="sxs-lookup"><span data-stu-id="8731b-481">Write operations per second</span></span>
<span data-ttu-id="8731b-482">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="8731b-482">TransfersPerSecond</span></span> | <span data-ttu-id="8731b-483">Operações de leitura ou gravação por segundo</span><span class="sxs-lookup"><span data-stu-id="8731b-483">Read or write operations per second</span></span>

<span data-ttu-id="8731b-484">Os valores agregados em todos os sistemas de arquivo podem ser obtidos pela configuração `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="8731b-484">Aggregated values across all file systems can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="8731b-485">Os valores para um sistema de arquivos montado específico, como "/mnt", podem ser obtidos pela configuração `"condition": 'Name="/mnt"'`.</span><span class="sxs-lookup"><span data-stu-id="8731b-485">Values for a specific mounted file system, such as "/mnt", can be obtained by setting `"condition": 'Name="/mnt"'`.</span></span>

### <a name="builtin-metrics-for-the-disk-class"></a><span data-ttu-id="8731b-486">métricas internas para a classe Disk</span><span class="sxs-lookup"><span data-stu-id="8731b-486">builtin metrics for the Disk class</span></span>

<span data-ttu-id="8731b-487">A classe de métricas Disk fornece informações sobre o uso do dispositivo de disco.</span><span class="sxs-lookup"><span data-stu-id="8731b-487">The Disk class of metrics provides information about disk device usage.</span></span> <span data-ttu-id="8731b-488">Essas estatísticas aplicam-se a toda a unidade.</span><span class="sxs-lookup"><span data-stu-id="8731b-488">These statistics apply to the entire drive.</span></span> <span data-ttu-id="8731b-489">Se houver vários sistemas de arquivos em um dispositivo, os contadores do dispositivo serão, na verdade, agregados em todos eles.</span><span class="sxs-lookup"><span data-stu-id="8731b-489">If there are multiple file systems on a device, the counters for that device are, effectively, aggregated across all of them.</span></span>

<span data-ttu-id="8731b-490">contador</span><span class="sxs-lookup"><span data-stu-id="8731b-490">counter</span></span> | <span data-ttu-id="8731b-491">Significado</span><span class="sxs-lookup"><span data-stu-id="8731b-491">Meaning</span></span>
------- | -------
<span data-ttu-id="8731b-492">ReadsPerSecond</span><span class="sxs-lookup"><span data-stu-id="8731b-492">ReadsPerSecond</span></span> | <span data-ttu-id="8731b-493">Operações de leitura por segundo</span><span class="sxs-lookup"><span data-stu-id="8731b-493">Read operations per second</span></span>
<span data-ttu-id="8731b-494">WritesPerSecond</span><span class="sxs-lookup"><span data-stu-id="8731b-494">WritesPerSecond</span></span> | <span data-ttu-id="8731b-495">Operações de gravação por segundo</span><span class="sxs-lookup"><span data-stu-id="8731b-495">Write operations per second</span></span>
<span data-ttu-id="8731b-496">TransfersPerSecond</span><span class="sxs-lookup"><span data-stu-id="8731b-496">TransfersPerSecond</span></span> | <span data-ttu-id="8731b-497">Operações totais por segundo</span><span class="sxs-lookup"><span data-stu-id="8731b-497">Total operations per second</span></span>
<span data-ttu-id="8731b-498">AverageReadTime</span><span class="sxs-lookup"><span data-stu-id="8731b-498">AverageReadTime</span></span> | <span data-ttu-id="8731b-499">Média de segundos por operação de leitura</span><span class="sxs-lookup"><span data-stu-id="8731b-499">Average seconds per read operation</span></span>
<span data-ttu-id="8731b-500">AverageWriteTime</span><span class="sxs-lookup"><span data-stu-id="8731b-500">AverageWriteTime</span></span> | <span data-ttu-id="8731b-501">Média de segundos por operação de gravação</span><span class="sxs-lookup"><span data-stu-id="8731b-501">Average seconds per write operation</span></span>
<span data-ttu-id="8731b-502">AverageTransferTime</span><span class="sxs-lookup"><span data-stu-id="8731b-502">AverageTransferTime</span></span> | <span data-ttu-id="8731b-503">Média de segundos por operação</span><span class="sxs-lookup"><span data-stu-id="8731b-503">Average seconds per operation</span></span>
<span data-ttu-id="8731b-504">AverageDiskQueueLength</span><span class="sxs-lookup"><span data-stu-id="8731b-504">AverageDiskQueueLength</span></span> | <span data-ttu-id="8731b-505">Número médio de operações de disco enfileiradas</span><span class="sxs-lookup"><span data-stu-id="8731b-505">Average number of queued disk operations</span></span>
<span data-ttu-id="8731b-506">ReadBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="8731b-506">ReadBytesPerSecond</span></span> | <span data-ttu-id="8731b-507">Número de bytes lidos por segundo</span><span class="sxs-lookup"><span data-stu-id="8731b-507">Number of bytes read per second</span></span>
<span data-ttu-id="8731b-508">WriteBytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="8731b-508">WriteBytesPerSecond</span></span> | <span data-ttu-id="8731b-509">Número de bytes gravados por segundo</span><span class="sxs-lookup"><span data-stu-id="8731b-509">Number of bytes written per second</span></span>
<span data-ttu-id="8731b-510">BytesPerSecond</span><span class="sxs-lookup"><span data-stu-id="8731b-510">BytesPerSecond</span></span> | <span data-ttu-id="8731b-511">Número de bytes lidos ou gravados por segundo</span><span class="sxs-lookup"><span data-stu-id="8731b-511">Number of bytes read or written per second</span></span>

<span data-ttu-id="8731b-512">Os valores agregados em todos os discos podem ser obtidos pela configuração `"condition": "IsAggregate=True"`.</span><span class="sxs-lookup"><span data-stu-id="8731b-512">Aggregated values across all disks can be obtained by setting `"condition": "IsAggregate=True"`.</span></span> <span data-ttu-id="8731b-513">Para saber mais para um dispositivo específico (por exemplo, /dev/sdf1), defina `"condition": "Name=\\"/dev/sdf1\\""`.</span><span class="sxs-lookup"><span data-stu-id="8731b-513">To get information for a specific device (for example, /dev/sdf1), set `"condition": "Name=\\"/dev/sdf1\\""`.</span></span>

## <a name="installing-and-configuring-lad-30-via-cli"></a><span data-ttu-id="8731b-514">Instalação e configuração do LAD 3.0 via CLI</span><span class="sxs-lookup"><span data-stu-id="8731b-514">Installing and configuring LAD 3.0 via CLI</span></span>

<span data-ttu-id="8731b-515">Supondo que as configurações protegidas estejam no arquivo PrivateConfig.json e suas informações de configuração pública estejam em PublicConfig.json, execute este comando:</span><span class="sxs-lookup"><span data-stu-id="8731b-515">Assuming your protected settings are in the file PrivateConfig.json and your public configuration information is in PublicConfig.json, run this command:</span></span>

```azurecli
az vm extension set *resource_group_name* *vm_name* LinuxDiagnostic Microsoft.Azure.Diagnostics '3.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json
```

<span data-ttu-id="8731b-516">O comando supõe que você esteja usando o modo de Gerenciamento de Recursos do Azure (arm) da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8731b-516">The command assumes you are using the Azure Resource Management mode (arm) of the Azure CLI.</span></span> <span data-ttu-id="8731b-517">Para configurar o LAD para as VMs do modelo de implantação clássico (ASM), alterne para o modo "asm" (`azure config mode asm`) e omita o nome do grupo de recursos no comando.</span><span class="sxs-lookup"><span data-stu-id="8731b-517">To configure LAD for classic deployment model (ASM) VMs, switch to "asm" mode (`azure config mode asm`) and omit the resource group name in the command.</span></span> <span data-ttu-id="8731b-518">Para saber mais, confira a [documentação da CLI entre plataformas](https://docs.microsoft.com/azure/xplat-cli-connect).</span><span class="sxs-lookup"><span data-stu-id="8731b-518">For more information, see the [cross-platform CLI documentation](https://docs.microsoft.com/azure/xplat-cli-connect).</span></span>

## <a name="an-example-lad-30-configuration"></a><span data-ttu-id="8731b-519">Uma configuração de exemplo do LAD 3.0</span><span class="sxs-lookup"><span data-stu-id="8731b-519">An example LAD 3.0 configuration</span></span>

<span data-ttu-id="8731b-520">Com base nas definições anteriores, aqui está uma configuração de extensão de amostra do LAD 3.0 com alguma explicação.</span><span class="sxs-lookup"><span data-stu-id="8731b-520">Based on the preceding definitions, here's a sample LAD 3.0 extension configuration with some explanation.</span></span> <span data-ttu-id="8731b-521">Para aplicar este exemplo ao seu caso, você deverá usar seu próprio nome da conta de armazenamento, token de SAS de conta e tokens de SAS de EventHubs.</span><span class="sxs-lookup"><span data-stu-id="8731b-521">To apply this sample to your case, you should use your own storage account name, account SAS token, and EventHubs SAS tokens.</span></span>

### <a name="privateconfigjson"></a><span data-ttu-id="8731b-522">PrivateConfig.json</span><span class="sxs-lookup"><span data-stu-id="8731b-522">PrivateConfig.json</span></span>

<span data-ttu-id="8731b-523">Essas configurações privadas definem os parâmetros de:</span><span class="sxs-lookup"><span data-stu-id="8731b-523">These private settings configure:</span></span>

* <span data-ttu-id="8731b-524">uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="8731b-524">a storage account</span></span>
* <span data-ttu-id="8731b-525">um token de SAS de conta correspondente</span><span class="sxs-lookup"><span data-stu-id="8731b-525">a matching account SAS token</span></span>
* <span data-ttu-id="8731b-526">vários coletores (JsonBlob ou EventHubs com tokens de SAS)</span><span class="sxs-lookup"><span data-stu-id="8731b-526">several sinks (JsonBlob or EventHubs with SAS tokens)</span></span>

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

### <a name="publicconfigjson"></a><span data-ttu-id="8731b-527">PublicConfig.json</span><span class="sxs-lookup"><span data-stu-id="8731b-527">PublicConfig.json</span></span>

<span data-ttu-id="8731b-528">Essas configurações públicas fazem o LAD:</span><span class="sxs-lookup"><span data-stu-id="8731b-528">These public settings cause LAD to:</span></span>

* <span data-ttu-id="8731b-529">Carregar as métricas de porcentagem de tempo de processador e espaço em disco usado para a tabela `WADMetrics*`</span><span class="sxs-lookup"><span data-stu-id="8731b-529">Upload percent-processor-time and used-disk-space metrics to the `WADMetrics*` table</span></span>
* <span data-ttu-id="8731b-530">Carregar as mensagens do recurso do syslog "user" e gravidade "info" para a tabela `LinuxSyslog*`</span><span class="sxs-lookup"><span data-stu-id="8731b-530">Upload messages from syslog facility "user" and severity "info" to the `LinuxSyslog*` table</span></span>
* <span data-ttu-id="8731b-531">Carregar resultados de consulta brutos de OMI (PercentProcessorTime e PercentIdleTime) para a tabela nomeada `LinuxCPU`</span><span class="sxs-lookup"><span data-stu-id="8731b-531">Upload raw OMI query results (PercentProcessorTime and PercentIdleTime) to the named `LinuxCPU` table</span></span>
* <span data-ttu-id="8731b-532">Carregar as linhas acrescentadas no arquivo `/var/log/myladtestlog` para a tabela `MyLadTestLog`</span><span class="sxs-lookup"><span data-stu-id="8731b-532">Upload appended lines in file `/var/log/myladtestlog` to the `MyLadTestLog` table</span></span>

<span data-ttu-id="8731b-533">Em cada caso, os dados também são carregados para:</span><span class="sxs-lookup"><span data-stu-id="8731b-533">In each case, data is also uploaded to:</span></span>

* <span data-ttu-id="8731b-534">O armazenamento de Blobs do Azure (o nome do contêiner é o definido no coletor JsonBlob)</span><span class="sxs-lookup"><span data-stu-id="8731b-534">Azure Blob storage (container name is as defined in the JsonBlob sink)</span></span>
* <span data-ttu-id="8731b-535">Ponto de extremidade de EventHubs (conforme especificado no coletor EventHubs)</span><span class="sxs-lookup"><span data-stu-id="8731b-535">EventHubs endpoint (as specified in the EventHubs sink)</span></span>

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

<span data-ttu-id="8731b-536">O `resourceId` na configuração deve corresponder à da máquina virtual ou conjunto de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="8731b-536">The `resourceId` in the configuration must match that of the VM or the virtual machine scale set.</span></span>

* <span data-ttu-id="8731b-537">Os gráficos e os alertas das métricas da plataforma Azure conhecem o resourceId da VM em que você está trabalhando.</span><span class="sxs-lookup"><span data-stu-id="8731b-537">Azure platform metrics charting and alerting knows the resourceId of the VM you're working on.</span></span> <span data-ttu-id="8731b-538">Ele espera localizar os dados para sua VM usando a chave de pesquisa do resourceId.</span><span class="sxs-lookup"><span data-stu-id="8731b-538">It expects to find the data for your VM using the resourceId the lookup key.</span></span>
* <span data-ttu-id="8731b-539">Se você usar o dimensionamento automático do Azure, o resourceId na configuração do dimensionamento automático deverá corresponder ao resourceId usado pelo LAD.</span><span class="sxs-lookup"><span data-stu-id="8731b-539">If you use Azure autoscale, the resourceId in the autoscale configuration must match the resourceId used by LAD.</span></span>
* <span data-ttu-id="8731b-540">O resourceId está integrado nos nomes de JsonBlobs escritos pelo LAD.</span><span class="sxs-lookup"><span data-stu-id="8731b-540">The resourceId is built into the names of JsonBlobs written by LAD.</span></span>

## <a name="view-your-data"></a><span data-ttu-id="8731b-541">Ver seus dados</span><span class="sxs-lookup"><span data-stu-id="8731b-541">View your data</span></span>

<span data-ttu-id="8731b-542">Use o Portal do Azure para exibir dados de desempenho ou definir alertas:</span><span class="sxs-lookup"><span data-stu-id="8731b-542">Use the Azure portal to view performance data or set alerts:</span></span>

![imagem](./media/diagnostic-extension/graph_metrics.png)

<span data-ttu-id="8731b-544">Os dados de `performanceCounters` são sempre armazenados em uma tabela de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8731b-544">The `performanceCounters` data are always stored in an Azure Storage table.</span></span> <span data-ttu-id="8731b-545">As APIs do Armazenamento do Azure estão disponíveis em várias linguagens e plataformas.</span><span class="sxs-lookup"><span data-stu-id="8731b-545">Azure Storage APIs are available for many languages and platforms.</span></span>

<span data-ttu-id="8731b-546">Os dados enviados para coletores JsonBlob são armazenados nos blobs na conta de armazenamento nomeada nas [Configurações protegidas](#protected-settings).</span><span class="sxs-lookup"><span data-stu-id="8731b-546">Data sent to JsonBlob sinks is stored in blobs in the storage account named in the [Protected settings](#protected-settings).</span></span> <span data-ttu-id="8731b-547">Você pode consumir os dados do blob usando qualquer API de Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="8731b-547">You can consume the blob data using any Azure Blob Storage APIs.</span></span>

<span data-ttu-id="8731b-548">Além disso, você pode usar essas ferramentas de interface do usuário para acessar os dados no Armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="8731b-548">In addition, you can use these UI tools to access the data in Azure Storage:</span></span>

* <span data-ttu-id="8731b-549">Gerenciador de Servidores do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8731b-549">Visual Studio Server Explorer.</span></span>
* <span data-ttu-id="8731b-550">[Gerenciador de Armazenamento do Microsoft Azure](https://azurestorageexplorer.codeplex.com/ "Gerenciador de Armazenamento do Azure").</span><span class="sxs-lookup"><span data-stu-id="8731b-550">[Microsoft Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/ "Azure Storage Explorer").</span></span>

<span data-ttu-id="8731b-551">Esse instantâneo de uma sessão do Gerenciador de Armazenamento do Microsoft Azure mostra as tabelas do Armazenamento do Azure geradas e os contêineres de uma extensão de LAD 3.0 configurada corretamente em uma VM de teste.</span><span class="sxs-lookup"><span data-stu-id="8731b-551">This snapshot of a Microsoft Azure Storage Explorer session shows the generated Azure Storage tables and containers from a correctly configured LAD 3.0 extension on a test VM.</span></span> <span data-ttu-id="8731b-552">A imagem não coincide exatamente com a [configuração de amostra do LAD 3.0](#an-example-lad-30-configuration).</span><span class="sxs-lookup"><span data-stu-id="8731b-552">The image doesn't match exactly with the [sample LAD 3.0 configuration](#an-example-lad-30-configuration).</span></span>

![imagem](./media/diagnostic-extension/stg_explorer.png)

<span data-ttu-id="8731b-554">Consulte a [Documentação de EventHubs](../../event-hubs/event-hubs-what-is-event-hubs.md) correspondente para aprender a consumir mensagens publicadas em um ponto de extremidade de EventHubs.</span><span class="sxs-lookup"><span data-stu-id="8731b-554">See the relevant [EventHubs documentation](../../event-hubs/event-hubs-what-is-event-hubs.md) to learn how to consume messages published to an EventHubs endpoint.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8731b-555">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8731b-555">Next steps</span></span>

* <span data-ttu-id="8731b-556">Criar alertas de métricas no [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) para as métricas que você coletar.</span><span class="sxs-lookup"><span data-stu-id="8731b-556">Create metric alerts in [Azure Monitor](../../monitoring-and-diagnostics/insights-alerts-portal.md) for the metrics you collect.</span></span>
* <span data-ttu-id="8731b-557">Criar [gráficos de monitoramento](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) para suas métricas.</span><span class="sxs-lookup"><span data-stu-id="8731b-557">Create [monitoring charts](../../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md) for your metrics.</span></span>
* <span data-ttu-id="8731b-558">Aprenda a [criar um conjunto de dimensionamento de máquinas virtuais](/azure/virtual-machines/linux/tutorial-create-vmss) usando suas métricas para controlar o dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="8731b-558">Learn how to [create a virtual machine scale set](/azure/virtual-machines/linux/tutorial-create-vmss) using your metrics to control autoscaling.</span></span>
