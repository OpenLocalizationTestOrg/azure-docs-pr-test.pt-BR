---
title: "aaaVirtual computador extensões e recursos para Linux | Microsoft Docs"
description: "Saiba quais extensões estão disponíveis para as máquinas virtuais do Azure, agrupadas pelas funcionalidades fornecidas ou aperfeiçoadas."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a>Recursos e extensões da máquina virtual para Linux

Extensões da máquina virtual do Azure são pequenos aplicativos que fornecem tarefas de configuração e automação pós-implantação nas máquinas virtuais do Azure. Por exemplo, se uma máquina virtual requer a instalação de software, proteção contra vírus ou a configuração do Docker, uma extensão de VM pode ser usado toocomplete essas tarefas. Extensões VM do Azure podem ser executadas usando Olá CLI do Azure, o PowerShell, modelos do Gerenciador de recursos do Azure e Olá portal do Azure. Extensões podem ser agrupadas com uma nova implantação de máquina virtual ou executar qualquer sistema existente.

Este documento fornece uma visão geral de extensões de VM, pré-requisitos para usar extensões de VM do Azure e orientação sobre como toodetect, gerenciar e remover extensões da VM. Este documento fornece informações generalizadas, pois há muitas extensões de VM disponíveis e cada uma delas tem uma configuração possivelmente exclusiva. Detalhes de extensão podem ser encontrados em cada extensão individuais do documento toohello específico.

## <a name="use-cases-and-samples"></a>Casos de uso e exemplos

Há várias extensões de VM do Azure diferentes disponíveis, cada uma com um caso de uso específico. Alguns exemplos incluem:

- Aplica PowerShell Desired configurações tooa máquina virtual em estado usando Olá extensão DSC para Linux. Para saber mais, confira [Extensão de configuração de Estado Desejado do Azure](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).
- Configure o monitoramento de uma máquina virtual com hello extensão VM de agente de monitoramento da Microsoft. Para obter mais informações, consulte [como toomonitor uma VM do Linux](tutorial-monitoring.md).
- Configure o monitoramento da infra-estrutura do Azure com hello Datadog extensão. Para obter mais informações, consulte Olá [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).
- Configure um host Docker em uma máquina virtual do Azure usando a extensão de VM Docker hello. Para saber mais, confira [Extensão de VM do Docker](dockerextension.md).

Além disso extensões específicas de tooprocess, uma extensão de Script personalizado está disponível para máquinas virtuais Windows e Linux. Olá extensão de Script personalizado para Linux permite que qualquer toobe de script Bash executado em uma máquina virtual. Scripts personalizados são úteis para a criação de implantações do Azure que exigem uma configuração que vai além da capacidade das ferramentas nativas do Azure. Para saber mais, confira [Extensão de Script Personalizado de VM do Linux](extensions-customscript.md).


## <a name="prerequisites"></a>Pré-requisitos

Cada extensão da máquina virtual pode ter seu próprio conjunto de pré-requisitos. Por exemplo, Olá extensão da VM Docker tem um pré-requisito de uma distribuição de Linux com suporte. Requisitos das extensões individuais são detalhados na documentação do hello específicas da extensão.

### <a name="azure-vm-agent"></a>Agente de VM do Azure

Agente de VM do Azure Olá gerencia as interações entre uma máquina virtual do Azure e o controlador de malha do Azure hello. Olá VM agent é responsável por muitos aspectos funcionais de implantação e gerenciamento de máquinas virtuais do Azure, incluindo a execução de extensões de VM. Agente de VM do Azure Olá foi pré-instalado no imagens do Azure Marketplace e pode ser instalada manualmente nos sistemas operacionais com suporte.

Para saber mais sobre os sistemas operacionais com suporte e as instruções de instalação, confira [Agente de máquina virtual do Azure](../windows/classic/agents-and-extensions.md).

## <a name="discover-vm-extensions"></a>Descobrir extensões de VM

Muitas extensões de VM diferentes estão disponíveis para uso com as máquinas virtuais do Azure. toosee uma lista completa, execute Olá comando com hello CLI do Azure a seguir, substituindo o local do exemplo hello pelo local de saudação de sua escolha.

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a>Executar extensões de VM

Extensões de máquina virtual do Azure podem ser executadas em máquinas virtuais existentes, que são úteis quando você precisa toomake alterações de configuração ou recuperar de conectividade em uma VM já implantada. As extensões de VM também podem ser agrupadas com implantações de modelo do Azure Resource Manager. Ao usar extensões com modelos do Resource Manager, as máquinas virtuais do Azure podem ser implantadas e configuradas sem intervenção pós-implantação.

Olá métodos a seguir pode ser usado toorun uma extensão em uma máquina virtual existente.

### <a name="azure-cli"></a>CLI do Azure

Extensões de máquina virtual do Azure podem ser executadas em uma máquina virtual existente usando Olá `az vm extension set` comando. Este exemplo executa a extensão do script personalizado Olá contra uma máquina virtual.

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

Olá script produz saída semelhante toohello texto a seguir:

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a>Portal do Azure

Extensões de VM podem ser aplicadas tooan de máquina virtual existente por meio de saudação portal do Azure. toodo portanto, selecione a máquina virtual de saudação, escolha **extensões**e clique em **adicionar**. Selecione a extensão de saudação quer Olá lista de extensões disponíveis e siga as instruções de saudação do Assistente de saudação.

Olá imagem a seguir mostra instalação Olá Olá extensão de Script personalizado de Linux do hello portal do Azure.

![Instalar a extensão de script personalizado](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a>Modelos do Gerenciador de Recursos do Azure

Extensões de VM podem ser adicionado tooan Azure Resource Manager modelo e executado com a implantação de saudação do modelo de saudação. Ao implantar uma extensão com um modelo, você pode criar implantações do Azure totalmente configuradas. Por exemplo, hello que JSON a seguir é obtido a partir de um modelo do Gerenciador de recursos. Olá modelo implanta um conjunto de VMs com balanceamento de carga e um banco de dados do SQL Azure e, em seguida, instala um aplicativo .NET Core em cada VM. Olá extensão de VM cuida Olá da instalação do software.

Para obter mais informações, consulte Olá completo [modelo do Gerenciador de recursos](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
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
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

Para obter mais informações, confira [Criação de modelos do Azure Resource Manager](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).

## <a name="secure-vm-extension-data"></a>Proteger dados de extensão da VM

Quando você estiver executando uma extensão de VM, talvez seja necessário tooinclude informações confidenciais, como as credenciais, nomes de conta de armazenamento e chaves de acesso da conta de armazenamento. Muitas extensões VM incluem uma configuração protegida que criptografa os dados e a descriptografa apenas dentro de saudação máquina de virtual de destino. Cada extensão tem um esquema específico de configuração protegida, e cada um é detalhado na documentação específica à extensão.

saudação de exemplo a seguir mostra uma instância do hello extensão de Script personalizado para Linux. Observe que tooexecute de comando Olá inclui um conjunto de credenciais. Neste exemplo, a saudação comando tooexecute não será criptografado.


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
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
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

Olá móvel **comando tooexecute** propriedade toohello **protegido** configuração protege a cadeia de caracteres de execução de saudação.

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
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
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a>Solucionar problemas de extensões de VM

Cada extensão VM pode ter a extensão de toohello específica de etapas de solução de problemas. Por exemplo, quando você estiver usando a extensão de Script personalizado hello, detalhes de execução de script podem ser encontrados localmente na Olá máquina virtual no qual a extensão de saudação foi executado. As etapas de solução de problemas específicas à extensão são detalhadas na documentação associada.

Olá etapas de solução de problemas a seguir se aplicam a tooall extensões de máquina virtual.

### <a name="view-extension-status"></a>Exibir o status da extensão

Depois que uma extensão de máquina virtual tiver sido executada em uma máquina virtual, use Olá seguindo o status da extensão de tooreturn comando CLI do Azure. Substitua os nomes de parâmetro de exemplo por seus próprios valores.

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

saída de Hello aparência Olá texto a seguir:

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

Status da extensão de execução também podem ser encontradas no hello portal do Azure. status de saudação tooview de uma extensão, a máquina virtual de select Olá, escolha **extensões**, e selecione Olá extensão desejado.

### <a name="rerun-a-vm-extension"></a>Executar novamente uma extensão de VM

Pode haver casos em que uma extensão de máquina virtual deve toobe novamente. Você pode executar novamente uma extensão, removendo-a e, em seguida, executar novamente a extensão de saudação com um método de execução de sua escolha. tooremove uma extensão, executar Olá após o comando com hello CLI do Azure. Substitua os nomes de parâmetro de exemplo por seus próprios valores.

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

Você pode remover uma extensão usando Olá etapas Olá portal do Azure:

1. Selecione uma máquina virtual.
2. Escolha **Extensões**.
3. Selecione a extensão de saudação desejada.
4. Escolha **Desinstalar**.

## <a name="common-vm-extension-reference"></a>Referência à extensão VM comum
| Nome da extensão | Descrição | Mais informações |
| --- | --- | --- |
| Extensão de Script Personalizado para Linux |Executar scripts em uma máquina virtual do Azure |[Extensão de Script Personalizado para Linux](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| Extensão do Docker |Instale Olá Docker daemon toosupport remotos comandos. |[Extensão de VM do Docker](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| Extensão de acesso à VM |Recuperar o acesso tooan máquina virtual do Azure |[Extensão de acesso à VM](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| Extensão de Diagnóstico do Azure |Gerenciar Diagnóstico do Azure |[Extensão de Diagnóstico do Azure](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| Extensão de Acesso à VM do Azure |Gerenciar usuários e credenciais |[Extensão de Acesso à VM para Linux](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
