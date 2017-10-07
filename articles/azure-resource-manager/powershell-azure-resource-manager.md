---
title: "aaaManage Azure soluções com o PowerShell | Microsoft Docs"
description: Use o PowerShell do Azure e o Gerenciador de recursos toomanage seus recursos.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a>Gerenciar recursos com o Azure PowerShell e o Resource Manager
> [!div class="op_single_selector"]
> * [Portal](resource-group-portal.md)
> * [CLI do Azure](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [API REST](resource-manager-rest-api.md)
>
>

Neste artigo, você aprenderá como toomanage suas soluções com o PowerShell do Azure e o Azure Resource Manager. Se você não estiver familiarizado com o Resource Manager, veja [Visão geral do Resource Manager](resource-group-overview.md). Este tópico se concentra nas tarefas de gerenciamento. Você irá:

1. Criar um grupo de recursos
2. Adicionar um grupo de recursos do recurso toohello
3. Adicionar um recurso de toohello de marca
4. Recursos de consulta baseados em nomes ou em valores de marca
5. Aplicar e remover um bloqueio no recurso Olá
6. Excluir um grupo de recursos

Este artigo não mostra como toodeploy uma assinatura de tooyour de modelo do Gerenciador de recursos. Para obter essas informações, veja [Implantar recursos com modelos do Resource Manager e o Azure PowerShell](resource-group-template-deploy.md).

## <a name="get-started-with-azure-powershell"></a>Introdução ao Azure PowerShell

Se você não tiver instalado o Azure PowerShell, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

Se você instalou o Azure PowerShell no hello anterior, mas não tiver atualizado-recentemente, considere a possibilidade de instalar a versão mais recente do hello. Você pode atualizar a versão de hello por meio de saudação mesmo método usado tooinstall-lo. Por exemplo, se você usou Olá Web Platform Installer, iniciá-lo novamente e procure uma atualização.

toocheck sua versão do hello módulo de recursos do Azure, use Olá cmdlet a seguir:

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

Este tópico foi atualizado para a versão 3.3.0. Se você tiver uma versão anterior, sua experiência pode não corresponder etapas Olá mostradas neste tópico. Para obter a documentação sobre os cmdlets de saudação nesta versão, consulte [AzureRM.Resources módulo](/powershell/module/azurerm.resources).

## <a name="log-in-tooyour-azure-account"></a>Faça logon no tooyour conta do Azure
Antes de iniciar sua solução, você deve fazer logon na conta de tooyour.

toolog em tooyour conta do Azure, use Olá **AzureRmAccount Login** cmdlet.

```powershell
Login-AzureRmAccount
```

Olá cmdlet solicita as credenciais de logon de saudação para sua conta do Azure. Após o logon, ele baixa as configurações de conta para que eles fiquem disponível tooAzure PowerShell.

Olá cmdlet retorna informações sobre sua conta e hello toouse de assinatura para tarefas de saudação.

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

Se você tiver mais de uma assinatura, você pode alternar a assinatura de tooa diferente. Primeiro, vamos ver todas as assinaturas de saudação para sua conta.

```powershell
Get-AzureRmSubscription
```

Retorna habilitados e desabilitados de assinaturas.

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

tooswitch tooa de assinatura diferente, forneça o nome de assinatura de saudação com hello **AzureRmContext conjunto** cmdlet.

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a>Criar um grupo de recursos
Antes de implantar qualquer assinatura de recursos de tooyour, você deve criar um grupo de recursos que contém recursos de saudação.

toocreate um grupo de recursos, use Olá **AzureRmResourceGroup novo** cmdlet. usa o comando Olá Olá **nome** toospecify parâmetro um nome para o grupo de recursos de saudação e hello **local** parâmetro toospecify seu local.

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

saída de Hello for Olá formato a seguir:

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

Se você precisar de grupo de recursos do tooretrieve hello mais tarde, use Olá cmdlet a seguir:

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

tooget todos os grupos de recursos em sua assinatura de hello, não especifique um nome:

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a>Adicionar grupo de recursos tooa de recursos
tooadd um grupo de recursos de toohello de recurso, você pode usar o hello **New-AzureRmResource** cmdlet ou um cmdlet que toohello específico de tipo de recurso que você está criando (como **novo AzureRmStorageAccount**). Talvez seja mais fácil toouse um cmdlet que é o tipo de recurso específico tooa porque ele inclui parâmetros para propriedades de saudação que são necessários para o novo recurso de saudação. toouse **New-AzureRmResource**, você deve saber todas as tooset de propriedades de saudação sem ser solicitado para eles.

No entanto, a adição de um recurso por meio de cmdlets pode causar confusão futuras porque o novo recurso de saudação não existe em um modelo do Gerenciador de recursos. A Microsoft recomenda definir a infraestrutura de saudação para sua solução do Azure em um modelo do Gerenciador de recursos. Modelos permitem que você tooreliably e repetidamente implantam sua solução. Para este tópico, você cria uma conta de armazenamento com um cmdlet do PowerShell, mas posteriormente você gerar um modelo de seu grupo de recursos.

Olá cmdlet a seguir cria uma conta de armazenamento. Em vez de usar o nome de saudação mostrado no exemplo hello, forneça um nome exclusivo para a conta de armazenamento hello. Olá nome deve ter entre 3 e 24 caracteres de comprimento e usar somente números e letras minúsculas. Se você usar Olá nome mostrado no exemplo hello, você receberá um erro porque esse nome já está em uso.

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

Se você precisar desse recurso de tooretrieve posteriormente, use Olá cmdlet a seguir:

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a>Adicione uma marca

As marcas permitem que você tooorganize seus recursos de acordo com as propriedades de toodifferent. Por exemplo, você pode ter vários recursos em diferentes grupos de recursos que pertencem a toohello mesmo departamento. Você pode aplicar um toomark departamento marca e o valor toothose recursos-los como pertencentes toohello mesma categoria. Ou, você pode marcar se um recurso é usado em um ambiente de produção ou de teste. Neste tópico, você aplicar marcas tooonly um recurso, mas em seu ambiente provavelmente faz sentido tooapply marcas tooall seus recursos.

Olá cmdlet a seguir aplica-se a conta de armazenamento do duas marcas tooyour:

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

Marcas são atualizadas como um único objeto. tooadd um recurso de tooa de marca que já inclua marcas, recuperar marcas existentes hello. Adicionar Olá nova marca toohello objeto que contém marcas existentes hello e reaplique todos os recursos de toohello marcas hello.

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a>Pesquisa de recursos

Saudação de uso **Find-AzureRmResource** cmdlet tooretrieve recursos para condições de pesquisa diferente.

* tooget um recurso por nome, fornecer Olá **ResourceNameContains** parâmetro:

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* tooget todos os recursos de saudação em um grupo de recursos, fornecer Olá **ResourceGroupNameContains** parâmetro:

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* tooget todos os recursos de saudação com um nome de marca e o valor fornecem Olá **TagName** e **TagValue** parâmetros:

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* recursos de saudação tooall com um tipo de recurso específico, forneça Olá **ResourceType** parâmetro:

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a>Um recurso de bloqueio

Quando você precisar toomake-se de que um recurso crítico é acidentalmente excluído ou modificado, aplica um recurso de bloqueio de toohello. Você pode especificar um **CanNotDelete** ou **ReadOnly**.

bloqueios de gerenciamento toocreate ou delete, você deve ter acesso muito`Microsoft.Authorization/*` ou `Microsoft.Authorization/locks/*` ações. De funções internas do hello, somente o proprietário e o administrador de acesso do usuário são concedidas as ações.

tooapply um bloqueio, use Olá cmdlet a seguir:

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Olá recurso bloqueado no hello anterior exemplo não pode ser excluído até que Olá bloqueio seja removido. tooremove um bloqueio, use:

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

Para saber mais sobre bloqueios de configuração, confira [Bloquear recursos com o Azure Resource Manager](resource-group-lock-resources.md).

## <a name="remove-resources-or-resource-group"></a>Remover recursos ou grupo de recursos
Você pode remover um recurso ou grupo de recursos. Quando você remove um grupo de recursos, você também remover todos os recursos de saudação dentro desse grupo de recursos.

* toodelete um recurso do grupo de recursos hello, use Olá **Remove-AzureRmResource** cmdlet. Esse cmdlet exclui o recurso hello, mas não exclui o grupo de recursos de saudação.

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* toodelete um grupo de recursos e todos os seus recursos, use Olá **AzureRmResourceGroup remover** cmdlet.

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

Para ambos os cmdlets, você será solicitado tooconfirm que desejar que recursos de saudação tooremove ou grupo de recursos. Se o operação de saudação exclui com êxito recurso hello ou grupo de recursos, ele retorna **True**.

## <a name="run-resource-manager-scripts-with-azure-automation"></a>Executar scripts do Resource Manager com a automação do Azure

Este tópico mostra como operações básicas de tooperform em seus recursos com o Azure PowerShell. Para cenários mais avançados de gerenciamento, você normalmente deseja toocreate um script e reutilizar esse script conforme o necessário ou em uma agenda. [Automação do Azure](../automation/automation-intro.md) fornece uma maneira para você scripts tooautomate usado com frequência que gerencia as soluções do Azure.

Olá tópicos a seguir mostram como toouse automação do Azure, o Gerenciador de recursos e o PowerShell tooeffectively executam tarefas de gerenciamento:

- Para obter informações sobre como criar um runbook, consulte [meu primeiro runbook PowerShell](../automation/automation-first-runbook-textual-powershell.md).
- Para obter informações sobre como trabalhar com galerias de scripts, consulte [galerias de Runbook e módulo de automação do Azure](../automation/automation-runbook-gallery.md).
- Para runbooks que iniciar e parar máquinas virtuais, consulte [cenário de automação do Azure: toocreate marcas formatada em JSON usando uma agenda para a VM do Azure inicialização e desligamento](../automation/automation-scenario-start-stop-vm-wjson-tags.md).
- Para runbooks que iniciar e parar máquinas virtuais fora do horário comercial, consulte [VMs iniciar/parar durante a solução de fora do horário comercial em automação](../automation/automation-solution-vm-management.md).

## <a name="next-steps"></a>Próximas etapas
* toolearn sobre como criar modelos do Gerenciador de recursos, consulte [criação de modelos de Gerenciador de recursos do Azure](resource-group-authoring-templates.md).
* toolearn sobre a implantação de modelos, consulte [implantar um aplicativo com o modelo do Gerenciador de recursos do Azure](resource-group-template-deploy.md).
* Você pode mover recursos tooa novo grupo de recursos existente. Para obter exemplos, consulte [tooNew recursos Mover grupo de recursos ou assinatura](resource-group-move-resources.md).
* Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).

