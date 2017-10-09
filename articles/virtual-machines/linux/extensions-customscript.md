---
title: scripts personalizados de aaaRun em VMs do Linux no Azure | Microsoft Docs
description: "Automatizar tarefas de configuração de VM do Linux usando Olá extensão de Script personalizado"
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: cf17ab2b-8d7e-4078-b6df-955c6d5071c2
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: f2c273a5fbd4cd1695aea48fa4bd08e691511e5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a><span data-ttu-id="d1714-103">Usando Olá extensão de Script personalizado do Azure com máquinas virtuais do Linux</span><span class="sxs-lookup"><span data-stu-id="d1714-103">Using hello Azure Custom Script Extension with Linux Virtual Machines</span></span>
<span data-ttu-id="d1714-104">Olá extensão de Script personalizado baixa e executa scripts em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1714-104">hello Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="d1714-105">Essa extensão é útil para a configuração de implantação de postagem, instalação de software ou qualquer outra configuração/tarefa de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="d1714-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="d1714-106">Scripts podem ser baixados do armazenamento do Azure ou outro local acessível da internet ou fornecidos extensão toohello tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="d1714-106">Scripts can be downloaded from Azure storage or other accessible internet location, or provided toohello extension run time.</span></span> <span data-ttu-id="d1714-107">Olá extensão de Script personalizado se integra com os modelos do Gerenciador de recursos do Azure e também pode ser executado usando Olá CLI do Azure, o PowerShell, o portal do Azure ou Olá API de REST de máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1714-107">hello Custom Script extension integrates with Azure Resource Manager templates, and can also be run using hello Azure CLI, PowerShell, Azure portal, or hello Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="d1714-108">Este documento detalha como toouse Olá extensão de Script personalizado de Olá CLI do Azure e um modelo do Gerenciador de recursos do Azure e as etapas em sistemas Linux de solução de problemas de detalhes.</span><span class="sxs-lookup"><span data-stu-id="d1714-108">This document details how toouse hello Custom Script Extension from hello Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.</span></span>

## <a name="extension-configuration"></a><span data-ttu-id="d1714-109">Configuração da extensão</span><span class="sxs-lookup"><span data-stu-id="d1714-109">Extension Configuration</span></span>
<span data-ttu-id="d1714-110">configuração de extensão de Script personalizado Olá Especifica como local de script e Olá toobe de comando executado.</span><span class="sxs-lookup"><span data-stu-id="d1714-110">hello Custom Script Extension configuration specifies things like script location and hello command toobe run.</span></span> <span data-ttu-id="d1714-111">Essa configuração pode ser armazenada em arquivos de configuração especificados na linha de comando hello, ou em um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1714-111">This configuration can be stored in configuration files, specified on hello command line, or in an Azure Resource Manager template.</span></span> <span data-ttu-id="d1714-112">Dados confidenciais podem ser armazenados em uma configuração protegida, que é criptografada e descriptografada apenas dentro de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="d1714-112">Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside hello virtual machine.</span></span> <span data-ttu-id="d1714-113">configuração protegida Olá é útil quando o comando de execução de saudação inclui segredos, como uma senha.</span><span class="sxs-lookup"><span data-stu-id="d1714-113">hello protected configuration is useful when hello execution command includes secrets such as a password.</span></span>

### <a name="public-configuration"></a><span data-ttu-id="d1714-114">Configuração pública</span><span class="sxs-lookup"><span data-stu-id="d1714-114">Public Configuration</span></span>
<span data-ttu-id="d1714-115">Esquema:</span><span class="sxs-lookup"><span data-stu-id="d1714-115">Schema:</span></span>

<span data-ttu-id="d1714-116">**Observação** – esses nomes de propriedade diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d1714-116">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="d1714-117">Use nomes de saudação conforme mostrado abaixo tooavoid problemas de implantação.</span><span class="sxs-lookup"><span data-stu-id="d1714-117">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="d1714-118">**commandToExecute**: (obrigatório, cadeia de caracteres) Olá tooexecute de script do ponto de entrada</span><span class="sxs-lookup"><span data-stu-id="d1714-118">**commandToExecute**: (required, string) hello entry point script tooexecute</span></span>
* <span data-ttu-id="d1714-119">**fileUris**: (opcional, matriz de cadeia de caracteres) Olá URLs para toobe arquivos baixados.</span><span class="sxs-lookup"><span data-stu-id="d1714-119">**fileUris**: (optional, string array) hello URLs for files toobe downloaded.</span></span>
* <span data-ttu-id="d1714-120">**carimbo de hora** (inteiro opcional) use este tootrigger somente do campo um executar script hello alterando o valor do campo.</span><span class="sxs-lookup"><span data-stu-id="d1714-120">**timestamp** (optional, integer) use this field only tootrigger a rerun of hello script by changing value of this field.</span></span>

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a><span data-ttu-id="d1714-121">Configuração protegida</span><span class="sxs-lookup"><span data-stu-id="d1714-121">Protected Configuration</span></span>
<span data-ttu-id="d1714-122">Esquema:</span><span class="sxs-lookup"><span data-stu-id="d1714-122">Schema:</span></span>

<span data-ttu-id="d1714-123">**Observação** – esses nomes de propriedade diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="d1714-123">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="d1714-124">Use nomes de saudação conforme mostrado abaixo tooavoid problemas de implantação.</span><span class="sxs-lookup"><span data-stu-id="d1714-124">Use hello names as seen below tooavoid deployment issues.</span></span>

* <span data-ttu-id="d1714-125">**commandToExecute**: (opcional, string) Olá tooexecute de script do ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="d1714-125">**commandToExecute**: (optional, string) hello entry point script tooexecute.</span></span> <span data-ttu-id="d1714-126">Use este campo se o comando tiver segredos, como senhas.</span><span class="sxs-lookup"><span data-stu-id="d1714-126">Use this field instead if your command contains secrets such as passwords.</span></span>
* <span data-ttu-id="d1714-127">**storageAccountName**: (opcional, string) nome hello da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d1714-127">**storageAccountName**: (optional, string) hello name of storage account.</span></span> <span data-ttu-id="d1714-128">Se você especificar credenciais de armazenamento, todos os fileUris deverão ser URLs para Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1714-128">If you specify storage credentials, all fileUris must be URLs for Azure Blobs.</span></span>
* <span data-ttu-id="d1714-129">**storageAccountKey**: (opcional, string) chave de acesso de saudação da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d1714-129">**storageAccountKey**: (optional, string) hello access key of storage account.</span></span>

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a><span data-ttu-id="d1714-130">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d1714-130">Azure CLI</span></span>
<span data-ttu-id="d1714-131">Ao usar o hello toorun da CLI do Azure Olá extensão de Script personalizado, crie um arquivo de configuração ou arquivos que contém no mínimo Olá uri de arquivo e comando de execução do script hello.</span><span class="sxs-lookup"><span data-stu-id="d1714-131">When using hello Azure CLI toorun hello Custom Script Extension, create a configuration file or files containing at minimum hello file uri, and hello script execution command.</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="d1714-132">Opcionalmente, as configurações de Olá podem ser especificadas no comando hello como uma cadeia de caracteres do formato JSON.</span><span class="sxs-lookup"><span data-stu-id="d1714-132">Optionally hello settings can be specified in hello command as a JSON formatted string.</span></span> <span data-ttu-id="d1714-133">Isso permite Olá toobe de configuração especificado durante a execução e sem um arquivo de configuração separado.</span><span class="sxs-lookup"><span data-stu-id="d1714-133">This allows hello configuration toobe specified during execution and without a separate configuration file.</span></span>

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a><span data-ttu-id="d1714-134">Exemplos de CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d1714-134">Azure CLI Examples</span></span>

<span data-ttu-id="d1714-135">**Exemplo 1** – Configuração pública com o arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="d1714-135">**Example 1** - Public configuration with script file.</span></span>

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

<span data-ttu-id="d1714-136">Comando CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="d1714-136">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="d1714-137">**Exemplo 2** – Configuração pública sem nenhum arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="d1714-137">**Example 2** - Public configuration with no script file.</span></span>

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

<span data-ttu-id="d1714-138">Comando CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="d1714-138">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="d1714-139">**Exemplo 3** - um arquivo de configuração público é o arquivo de script de saudação do toospecify usado URI e um arquivo de configuração protegida é usado toospecify Olá comando toobe executado.</span><span class="sxs-lookup"><span data-stu-id="d1714-139">**Example 3** - A public configuration file is used toospecify hello script file URI, and a protected configuration file is used toospecify hello command toobe executed.</span></span>

<span data-ttu-id="d1714-140">Arquivo de configuração pública:</span><span class="sxs-lookup"><span data-stu-id="d1714-140">Public configuration file:</span></span>

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

<span data-ttu-id="d1714-141">Arquivo de configuração protegida:</span><span class="sxs-lookup"><span data-stu-id="d1714-141">Protected configuration file:</span></span>  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

<span data-ttu-id="d1714-142">Comando CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="d1714-142">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a><span data-ttu-id="d1714-143">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d1714-143">Resource Manager Template</span></span>
<span data-ttu-id="d1714-144">Olá extensão de Script personalizado do Azure pode ser executado no momento da implantação de máquina Virtual usando um modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="d1714-144">hello Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template.</span></span> <span data-ttu-id="d1714-145">toodo assim, adicione o modelo de implantação de toohello JSON formatado corretamente.</span><span class="sxs-lookup"><span data-stu-id="d1714-145">toodo so, add properly formatted JSON toohello deployment template.</span></span>

### <a name="resource-manager-examples"></a><span data-ttu-id="d1714-146">Exemplos do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d1714-146">Resource Manager Examples</span></span>
<span data-ttu-id="d1714-147">**Exemplo 1** – Configuração pública.</span><span class="sxs-lookup"><span data-stu-id="d1714-147">**Example 1** - public configuration.</span></span>

```json
{
    "name": "scriptextensiondemo",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "2015-06-15",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', parameters('scriptextensiondemoName'))]"
    ],
    "tags": {
        "displayName": "scriptextensiondemo"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Extensions",
        "type": "CustomScript",
        "typeHandlerVersion": "2.0",
        "autoUpgradeMinorVersion": true,
      "settings": {
        "fileUris": [
          "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
        ],
        "commandToExecute": "sh hello.sh"
      }
    }
}
```

<span data-ttu-id="d1714-148">**Exemplo 2** – Comando de execução na configuração protegida.</span><span class="sxs-lookup"><span data-stu-id="d1714-148">**Example 2** - execution command in protected configuration.</span></span>

```json
{
  "name": "config-app",
  "type": "extensions",
  "location": "[resourceGroup().location]",
  "apiVersion": "2015-06-15",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"
      ]              
    },
    "protectedSettings": {
      "commandToExecute": "sh hello.sh <password>"
    }
  }
}
```

<span data-ttu-id="d1714-149">Consulte o repositório de música Olá .net Core demonstração para obter um exemplo completo - [demonstração do repositório de música](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span><span class="sxs-lookup"><span data-stu-id="d1714-149">See hello .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d1714-150">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="d1714-150">Troubleshooting</span></span>
<span data-ttu-id="d1714-151">Quando Olá extensão de Script personalizado é executado, o script hello é criado ou baixado em uma toohello semelhante directory exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="d1714-151">When hello Custom Script Extension runs, hello script is created or downloaded into a directory similar toohello following example.</span></span> <span data-ttu-id="d1714-152">saída do comando Olá também serão salvos nesse diretório em `stdout` e `stderr` arquivo.</span><span class="sxs-lookup"><span data-stu-id="d1714-152">hello command output is also saved into this directory in `stdout` and `stderr` file.</span></span>

```bash
/var/lib/waagent/custom-script/download/0/
```

<span data-ttu-id="d1714-153">saudação de extensão do Script do Azure gera um log, que pode ser encontrado aqui.</span><span class="sxs-lookup"><span data-stu-id="d1714-153">hello Azure Script Extension produces a log, which can be found here.</span></span>

```bash
/var/log/azure/custom-script/handler.log
```

<span data-ttu-id="d1714-154">estado de execução de saudação do hello extensão de Script personalizado também pode ser recuperado com hello CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="d1714-154">hello execution state of hello Custom Script Extension can also be retrieved with hello Azure CLI.</span></span>

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

<span data-ttu-id="d1714-155">saída de Hello aparência Olá texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="d1714-155">hello output looks like hello following text:</span></span>

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a><span data-ttu-id="d1714-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d1714-156">Next Steps</span></span>
<span data-ttu-id="d1714-157">Para obter informações sobre outras extensões de script de VM, consulte [Visão geral da extensão de script do Azure para Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d1714-157">For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

