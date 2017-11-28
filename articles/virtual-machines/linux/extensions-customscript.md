---
title: Executar scripts personalizados em VMs do Linux no Azure | Microsoft Docs
description: "Automatizar tarefas de configuração de VM do Linux usando a extensão de script personalizado"
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
ms.openlocfilehash: 1dde64aac72c11ccfccf4fdb676279692befaadd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-custom-script-extension-with-linux-virtual-machines"></a><span data-ttu-id="a8059-103">Uso da extensão de script personalizado do Azure com máquinas virtuais do Linux</span><span class="sxs-lookup"><span data-stu-id="a8059-103">Using the Azure Custom Script Extension with Linux Virtual Machines</span></span>
<span data-ttu-id="a8059-104">A extensão de script personalizado baixa e executa scripts em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8059-104">The Custom Script Extension downloads and executes scripts on Azure virtual machines.</span></span> <span data-ttu-id="a8059-105">Essa extensão é útil para a configuração de implantação de postagem, instalação de software ou qualquer outra configuração/tarefa de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="a8059-105">This extension is useful for post deployment configuration, software installation, or any other configuration / management task.</span></span> <span data-ttu-id="a8059-106">Scripts podem ser baixados do armazenamento do Azure ou de outra localização acessível da Internet ou fornecidos para o tempo de execução da extensão.</span><span class="sxs-lookup"><span data-stu-id="a8059-106">Scripts can be downloaded from Azure storage or other accessible internet location, or provided to the extension run time.</span></span> <span data-ttu-id="a8059-107">A extensão de script personalizado se integra com modelos do Azure Resource Manager e também pode ser executada usando a CLI do Azure, o PowerShell, o portal do Azure ou a API REST da máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8059-107">The Custom Script extension integrates with Azure Resource Manager templates, and can also be run using the Azure CLI, PowerShell, Azure portal, or the Azure Virtual Machine REST API.</span></span>

<span data-ttu-id="a8059-108">Este documento fornece detalhes sobre como usar a extensão de script personalizado na CLI do Azure e um modelo do Azure Resource Manager e também fornece detalhes sobre as etapas de solução de problemas em sistemas Linux.</span><span class="sxs-lookup"><span data-stu-id="a8059-108">This document details how to use the Custom Script Extension from the Azure CLI, and an Azure Resource Manager template, and also details troubleshooting steps on Linux systems.</span></span>

## <a name="extension-configuration"></a><span data-ttu-id="a8059-109">Configuração da extensão</span><span class="sxs-lookup"><span data-stu-id="a8059-109">Extension Configuration</span></span>
<span data-ttu-id="a8059-110">A configuração de extensão de script personalizado especifica itens como localização de script e o comando a ser executado.</span><span class="sxs-lookup"><span data-stu-id="a8059-110">The Custom Script Extension configuration specifies things like script location and the command to be run.</span></span> <span data-ttu-id="a8059-111">Essa configuração pode ser armazenada em arquivos de configuração, especificada na linha de comando ou em um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a8059-111">This configuration can be stored in configuration files, specified on the command line, or in an Azure Resource Manager template.</span></span> <span data-ttu-id="a8059-112">Dados confidenciais podem ser armazenados em uma configuração protegida, que é criptografada e descriptografada somente dentro da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="a8059-112">Sensitive data can be stored in a protected configuration, which is encrypted and only decrypted inside the virtual machine.</span></span> <span data-ttu-id="a8059-113">A configuração protegida é útil quando o comando de execução inclui segredos, como uma senha.</span><span class="sxs-lookup"><span data-stu-id="a8059-113">The protected configuration is useful when the execution command includes secrets such as a password.</span></span>

### <a name="public-configuration"></a><span data-ttu-id="a8059-114">Configuração pública</span><span class="sxs-lookup"><span data-stu-id="a8059-114">Public Configuration</span></span>
<span data-ttu-id="a8059-115">Esquema:</span><span class="sxs-lookup"><span data-stu-id="a8059-115">Schema:</span></span>

<span data-ttu-id="a8059-116">**Observação** – esses nomes de propriedade diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a8059-116">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="a8059-117">Use os nomes conforme mostrado abaixo para evitar problemas de implantação.</span><span class="sxs-lookup"><span data-stu-id="a8059-117">Use the names as seen below to avoid deployment issues.</span></span>

* <span data-ttu-id="a8059-118">**commandToExecute**: (obrigatório, cadeia de caracteres) o script de ponto de entrada a ser executado</span><span class="sxs-lookup"><span data-stu-id="a8059-118">**commandToExecute**: (required, string) the entry point script to execute</span></span>
* <span data-ttu-id="a8059-119">**fileUris**: (opcional, matriz de cadeia de caracteres) as URLs de arquivos a serem baixados.</span><span class="sxs-lookup"><span data-stu-id="a8059-119">**fileUris**: (optional, string array) the URLs for files to be downloaded.</span></span>
* <span data-ttu-id="a8059-120">**timestamp** (opcional, inteiro) use este campo somente para disparar uma nova execução do script, alterando o valor desse campo.</span><span class="sxs-lookup"><span data-stu-id="a8059-120">**timestamp** (optional, integer) use this field only to trigger a rerun of the script by changing value of this field.</span></span>

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a><span data-ttu-id="a8059-121">Configuração protegida</span><span class="sxs-lookup"><span data-stu-id="a8059-121">Protected Configuration</span></span>
<span data-ttu-id="a8059-122">Esquema:</span><span class="sxs-lookup"><span data-stu-id="a8059-122">Schema:</span></span>

<span data-ttu-id="a8059-123">**Observação** – esses nomes de propriedade diferenciam maiúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a8059-123">**Note** - these property names are case sensitive.</span></span> <span data-ttu-id="a8059-124">Use os nomes conforme mostrado abaixo para evitar problemas de implantação.</span><span class="sxs-lookup"><span data-stu-id="a8059-124">Use the names as seen below to avoid deployment issues.</span></span>

* <span data-ttu-id="a8059-125">**commandToExecute**: (opcional, cadeia de caracteres) o script de ponto de entrada a ser executado.</span><span class="sxs-lookup"><span data-stu-id="a8059-125">**commandToExecute**: (optional, string) the entry point script to execute.</span></span> <span data-ttu-id="a8059-126">Use este campo se o comando tiver segredos, como senhas.</span><span class="sxs-lookup"><span data-stu-id="a8059-126">Use this field instead if your command contains secrets such as passwords.</span></span>
* <span data-ttu-id="a8059-127">**storageAccountName**: (opcional, cadeia de caracteres) o nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a8059-127">**storageAccountName**: (optional, string) the name of storage account.</span></span> <span data-ttu-id="a8059-128">Se você especificar credenciais de armazenamento, todos os fileUris deverão ser URLs para Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8059-128">If you specify storage credentials, all fileUris must be URLs for Azure Blobs.</span></span>
* <span data-ttu-id="a8059-129">**storageAccountKey**: (opcional, cadeia de caracteres) a tecla de acesso da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a8059-129">**storageAccountKey**: (optional, string) the access key of storage account.</span></span>

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a><span data-ttu-id="a8059-130">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a8059-130">Azure CLI</span></span>
<span data-ttu-id="a8059-131">Ao usar a CLI do Azure para executar a extensão de script personalizado, crie um arquivo de configuração ou arquivos que contêm pelo menos o URI do arquivo e o comando de execução do script.</span><span class="sxs-lookup"><span data-stu-id="a8059-131">When using the Azure CLI to run the Custom Script Extension, create a configuration file or files containing at minimum the file uri, and the script execution command.</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="a8059-132">As configurações também podem ser especificadas no comando como uma cadeia de caracteres formatada em JSON.</span><span class="sxs-lookup"><span data-stu-id="a8059-132">Optionally the settings can be specified in the command as a JSON formatted string.</span></span> <span data-ttu-id="a8059-133">Isso permite especificar a configuração durante a execução e sem um arquivo de configuração separado.</span><span class="sxs-lookup"><span data-stu-id="a8059-133">This allows the configuration to be specified during execution and without a separate configuration file.</span></span>

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a><span data-ttu-id="a8059-134">Exemplos de CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a8059-134">Azure CLI Examples</span></span>

<span data-ttu-id="a8059-135">**Exemplo 1** – Configuração pública com o arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="a8059-135">**Example 1** - Public configuration with script file.</span></span>

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

<span data-ttu-id="a8059-136">Comando CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="a8059-136">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="a8059-137">**Exemplo 2** – Configuração pública sem nenhum arquivo de script.</span><span class="sxs-lookup"><span data-stu-id="a8059-137">**Example 2** - Public configuration with no script file.</span></span>

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

<span data-ttu-id="a8059-138">Comando CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="a8059-138">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

<span data-ttu-id="a8059-139">**Exemplo 3** – Um arquivo de configuração pública é usado para especificar o URI do arquivo de script, e um arquivo de configuração protegida é usado para especificar o comando a ser executado.</span><span class="sxs-lookup"><span data-stu-id="a8059-139">**Example 3** - A public configuration file is used to specify the script file URI, and a protected configuration file is used to specify the command to be executed.</span></span>

<span data-ttu-id="a8059-140">Arquivo de configuração pública:</span><span class="sxs-lookup"><span data-stu-id="a8059-140">Public configuration file:</span></span>

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

<span data-ttu-id="a8059-141">Arquivo de configuração protegida:</span><span class="sxs-lookup"><span data-stu-id="a8059-141">Protected configuration file:</span></span>  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

<span data-ttu-id="a8059-142">Comando CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="a8059-142">Azure CLI command:</span></span>

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a><span data-ttu-id="a8059-143">Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8059-143">Resource Manager Template</span></span>
<span data-ttu-id="a8059-144">A extensão de script personalizado do Azure pode ser executada no momento da implantação de máquina virtual usando um modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a8059-144">The Azure Custom Script Extension can be run at Virtual Machine deployment time using a Resource Manager template.</span></span> <span data-ttu-id="a8059-145">Para fazer isso, adicione JSON formatado corretamente ao modelo de implantação.</span><span class="sxs-lookup"><span data-stu-id="a8059-145">To do so, add properly formatted JSON to the deployment template.</span></span>

### <a name="resource-manager-examples"></a><span data-ttu-id="a8059-146">Exemplos do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a8059-146">Resource Manager Examples</span></span>
<span data-ttu-id="a8059-147">**Exemplo 1** – Configuração pública.</span><span class="sxs-lookup"><span data-stu-id="a8059-147">**Example 1** - public configuration.</span></span>

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

<span data-ttu-id="a8059-148">**Exemplo 2** – Comando de execução na configuração protegida.</span><span class="sxs-lookup"><span data-stu-id="a8059-148">**Example 2** - execution command in protected configuration.</span></span>

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

<span data-ttu-id="a8059-149">Consulte a Demonstração da Loja de Música do .Net Core para ver um exemplo completo – [Demonstração da Loja de Música](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span><span class="sxs-lookup"><span data-stu-id="a8059-149">See the .Net Core Music Store Demo for a complete example - [Music Store Demo](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="a8059-150">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="a8059-150">Troubleshooting</span></span>
<span data-ttu-id="a8059-151">Quando a extensão de script personalizado é executada, o script é criado ou baixado em um diretório semelhante ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="a8059-151">When the Custom Script Extension runs, the script is created or downloaded into a directory similar to the following example.</span></span> <span data-ttu-id="a8059-152">A saída do comando também é salva nesse diretório no arquivo `stdout` e `stderr`.</span><span class="sxs-lookup"><span data-stu-id="a8059-152">The command output is also saved into this directory in `stdout` and `stderr` file.</span></span>

```bash
/var/lib/waagent/custom-script/download/0/
```

<span data-ttu-id="a8059-153">A extensão de script do Azure produz um log, que pode ser encontrado aqui.</span><span class="sxs-lookup"><span data-stu-id="a8059-153">The Azure Script Extension produces a log, which can be found here.</span></span>

```bash
/var/log/azure/custom-script/handler.log
```

<span data-ttu-id="a8059-154">O estado de execução da extensão de script personalizado também pode ser recuperado com a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a8059-154">The execution state of the Custom Script Extension can also be retrieved with the Azure CLI.</span></span>

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

<span data-ttu-id="a8059-155">A saída se parece com o seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="a8059-155">The output looks like the following text:</span></span>

```azurecli
info:    Executing command vm extension get
+ Looking up the VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a><span data-ttu-id="a8059-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a8059-156">Next Steps</span></span>
<span data-ttu-id="a8059-157">Para obter informações sobre outras extensões de script de VM, consulte [Visão geral da extensão de script do Azure para Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a8059-157">For information on other VM Script Extensions, see [Azure Script Extension overview for Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

