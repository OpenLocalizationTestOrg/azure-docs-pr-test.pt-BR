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
# <a name="using-hello-azure-custom-script-extension-with-linux-virtual-machines"></a>Usando Olá extensão de Script personalizado do Azure com máquinas virtuais do Linux
Olá extensão de Script personalizado baixa e executa scripts em máquinas virtuais do Azure. Essa extensão é útil para a configuração de implantação de postagem, instalação de software ou qualquer outra configuração/tarefa de gerenciamento. Scripts podem ser baixados do armazenamento do Azure ou outro local acessível da internet ou fornecidos extensão toohello tempo de execução. Olá extensão de Script personalizado se integra com os modelos do Gerenciador de recursos do Azure e também pode ser executado usando Olá CLI do Azure, o PowerShell, o portal do Azure ou Olá API de REST de máquina Virtual do Azure.

Este documento detalha como toouse Olá extensão de Script personalizado de Olá CLI do Azure e um modelo do Gerenciador de recursos do Azure e as etapas em sistemas Linux de solução de problemas de detalhes.

## <a name="extension-configuration"></a>Configuração da extensão
configuração de extensão de Script personalizado Olá Especifica como local de script e Olá toobe de comando executado. Essa configuração pode ser armazenada em arquivos de configuração especificados na linha de comando hello, ou em um modelo do Gerenciador de recursos do Azure. Dados confidenciais podem ser armazenados em uma configuração protegida, que é criptografada e descriptografada apenas dentro de máquina virtual de saudação. configuração protegida Olá é útil quando o comando de execução de saudação inclui segredos, como uma senha.

### <a name="public-configuration"></a>Configuração pública
Esquema:

**Observação** – esses nomes de propriedade diferenciam maiúsculas de minúsculas. Use nomes de saudação conforme mostrado abaixo tooavoid problemas de implantação.

* **commandToExecute**: (obrigatório, cadeia de caracteres) Olá tooexecute de script do ponto de entrada
* **fileUris**: (opcional, matriz de cadeia de caracteres) Olá URLs para toobe arquivos baixados.
* **carimbo de hora** (inteiro opcional) use este tootrigger somente do campo um executar script hello alterando o valor do campo.

```json
{
  "fileUris": ["<url>"],
  "commandToExecute": "<command-to-execute>"
}
```

### <a name="protected-configuration"></a>Configuração protegida
Esquema:

**Observação** – esses nomes de propriedade diferenciam maiúsculas de minúsculas. Use nomes de saudação conforme mostrado abaixo tooavoid problemas de implantação.

* **commandToExecute**: (opcional, string) Olá tooexecute de script do ponto de entrada. Use este campo se o comando tiver segredos, como senhas.
* **storageAccountName**: (opcional, string) nome hello da conta de armazenamento. Se você especificar credenciais de armazenamento, todos os fileUris deverão ser URLs para Blobs do Azure.
* **storageAccountKey**: (opcional, string) chave de acesso de saudação da conta de armazenamento.

```json
{
  "commandToExecute": "<command-to-execute>",
  "storageAccountName": "<storage-account-name>",
  "storageAccountKey": "<storage-account-key>"
}
```

## <a name="azure-cli"></a>CLI do Azure
Ao usar o hello toorun da CLI do Azure Olá extensão de Script personalizado, crie um arquivo de configuração ou arquivos que contém no mínimo Olá uri de arquivo e comando de execução do script hello.

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

Opcionalmente, as configurações de Olá podem ser especificadas no comando hello como uma cadeia de caracteres do formato JSON. Isso permite Olá toobe de configuração especificado durante a execução e sem um arquivo de configuração separado.

```azurecli
az vm extension set '
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],"commandToExecute": "./test.sh"}'
```

### <a name="azure-cli-examples"></a>Exemplos de CLI do Azure

**Exemplo 1** – Configuração pública com o arquivo de script.

```json
{
  "fileUris": ["https://raw.githubusercontent.com/neilpeterson/test-extension/master/test.sh"],
  "commandToExecute": "./test.sh"
}
```

Comando CLI do Azure:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**Exemplo 2** – Configuração pública sem nenhum arquivo de script.

```json
{
  "commandToExecute": "apt-get -y update && apt-get install -y apache2"
}
```

Comando CLI do Azure:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json
```

**Exemplo 3** - um arquivo de configuração público é o arquivo de script de saudação do toospecify usado URI e um arquivo de configuração protegida é usado toospecify Olá comando toobe executado.

Arquivo de configuração pública:

```json
{
  "fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"]
}
```

Arquivo de configuração protegida:  

```json
{
  "commandToExecute": "./hello.sh <password>"
}
```

Comando CLI do Azure:

```azurecli
az vm extension set --resource-group myResourceGroup --vm-name myVM --name customScript --publisher Microsoft.Azure.Extensions --settings ./script-config.json --protected-settings ./protected-config.json
```

## <a name="resource-manager-template"></a>Modelo do Resource Manager
Olá extensão de Script personalizado do Azure pode ser executado no momento da implantação de máquina Virtual usando um modelo do Gerenciador de recursos. toodo assim, adicione o modelo de implantação de toohello JSON formatado corretamente.

### <a name="resource-manager-examples"></a>Exemplos do Resource Manager
**Exemplo 1** – Configuração pública.

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

**Exemplo 2** – Comando de execução na configuração protegida.

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

Consulte o repositório de música Olá .net Core demonstração para obter um exemplo completo - [demonstração do repositório de música](https://github.com/neilpeterson/nepeters-azure-templates/tree/master/dotnet-core-music-linux-vm-sql-db).

## <a name="troubleshooting"></a>Solucionar problemas
Quando Olá extensão de Script personalizado é executado, o script hello é criado ou baixado em uma toohello semelhante directory exemplo a seguir. saída do comando Olá também serão salvos nesse diretório em `stdout` e `stderr` arquivo.

```bash
/var/lib/waagent/custom-script/download/0/
```

saudação de extensão do Script do Azure gera um log, que pode ser encontrado aqui.

```bash
/var/log/azure/custom-script/handler.log
```

estado de execução de saudação do hello extensão de Script personalizado também pode ser recuperado com hello CLI do Azure.

```azurecli
az vm extension list -g myResourceGroup --vm-name myVM
```

saída de Hello aparência Olá texto a seguir:

```azurecli
info:    Executing command vm extension get
+ Looking up hello VM "scripttst001"
data:    Publisher                   Name                                      Version  State
data:    --------------------------  ----------------------------------------  -------  ---------
data:    Microsoft.Azure.Extensions  CustomScript                              2.0      Succeeded
data:    Microsoft.OSTCExtensions    Microsoft.Insights.VMDiagnosticsSettings  2.3      Succeeded
info:    vm extension get command OK
```

## <a name="next-steps"></a>Próximas etapas
Para obter informações sobre outras extensões de script de VM, consulte [Visão geral da extensão de script do Azure para Linux](extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

