---
ms.assetid: 
title: "Cofre de chave aaaAzure - como toouse soft-exclusão com o PowerShell"
description: "Usar exemplos de caso de exclusão reversível com trechos de código do PowerShell"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 4968b700a14f764ea1be7de2bf3697664f255f95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a>Como toouse Cofre de chaves soft-exclusão com o PowerShell

O recurso de exclusão reversível do Azure Key Vault permite a recuperação de cofres e objetos de cofre excluídos. Especificamente, os endereços de exclusão reversível Olá os seguintes cenários:

- Suporte à exclusão reversível de cofres de chaves
- Suporte à exclusão reversível de objetos do cofre de chaves, chaves, segredos e certificados

## <a name="prerequisites"></a>Pré-requisitos

- O Azure PowerShell 4.0.0 ou posterior - se você não nesse já que a instalação, instale o Azure PowerShell e associá-lo a sua assinatura do Azure, consulte [como tooinstall e configurar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview). 

>[!NOTE]
> Há uma versão desatualizada do nosso formatação de saída do PowerShell do Cofre de chave de arquivo que **pode** ser carregado em seu ambiente, em vez da versão correta do hello. Nós estão prevendo que uma versão atualizada do PowerShell toocontain Olá necessário correção para formatação de saída de hello e atualizará este tópico no momento. Olá solução atual, se você encontrar esse problema de formatação, é:
> - Olá Use consulta a seguir se você perceber que você não estiver vendo hello exclusão reversível habilitada propriedade descrita neste tópico: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.


Para saber mais de referência específicas do Key Vault para o PowerShell, veja [Referência do PowerShell do Azure Key Vault](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).

## <a name="required-permissions"></a>Permissões necessárias

As operações de Key Vault são gerenciadas separadamente por meio de permissões de RBAC (controle de acesso baseado em função) da seguinte maneira:

| Operação | Descrição | Permissão de usuário |
|:--|:--|:--|
|Listar|Lista os cofres de chaves excluídos.|Microsoft.KeyVault/deletedVaults/read|
|Recuperar|Recupera o cofre de chaves excluído.|Microsoft.KeyVault/vaults/write|
|Limpar|Remove permanentemente um cofre de chaves excluído e todo o seu conteúdo.|Microsoft.KeyVault/locations/deletedVaults/purge/action|

Para saber mais sobre permissões e controle de acesso, veja [Proteger seu cofre de chaves](key-vault-secure-your-key-vault.md).

## <a name="enabling-soft-delete"></a>Habilitar a exclusão reversível

toorecover capaz de toobe um cofre de chaves excluído ou objetos armazenados em uma chave de cofre, você deve primeiro habilitar a exclusão reversível para esse Cofre de chaves.

### <a name="existing-key-vault"></a>Cofre de chaves existente

Para um cofre de chaves existente chamado ContosoVault, habilite a exclusão reversível da seguinte maneira. 

>[!NOTE]
>Atualmente é necessário Olá de gravação do toouse do Azure Resource Manager recursos manipulação toodirectly *enableSoftDelete* toohello de propriedade de recurso de Cofre de chave.

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a>Novo cofre de chaves

Habilitar exclusão reversível para um novo cofre de chave é feito no momento da criação, adicionando o sinalizador de exclusão reversível do hello tooyour criar o comando.

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a>Verificar a habilitação da exclusão reversível

tooverify um cofre de chaves com exclusão reversível habilitada, Olá execução *obter* de comando e procure hello "Flexível excluir ativado?" e sua configuração, true ou false.

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a>Excluir um cofre de chaves protegido por exclusão reversível

Olá comando toodelete (ou remover) um cofre de chaves permanece Olá mesmo, mas suas alterações de comportamento dependendo se você habilitou o soft-exclusão ou não.

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
>Se você executar o comando anterior de saudação para um cofre de chaves que não tenha habilitada a exclusão reversível, você excluirá permanentemente este cofre de chaves e todo o seu conteúdo sem opções de recuperação.

### <a name="how-soft-delete-protects-your-key-vaults"></a>Como a exclusão reversível protege seus cofres de chaves

Com a exclusão reversível habilitada:

- Quando um cofre de chaves é excluído, ele é removido do seu grupo de recursos e colocado em um espaço reservado que só é associado ao local de saudação onde ele foi criado. 
- Objetos em uma chave excluída cofre, como chaves, segredos e certificados, não estão acessíveis e continuar assim enquanto seu Cofre de chaves que contém está em estado de saudação excluído. 
- Olá nome DNS um cofre de chaves em um estado excluído é preservado, portanto, não é possível criar um novo cofre de chave com o mesmo nome.  

Você pode exibir cofres de chave de estado excluído, associados à sua assinatura, usando o comando a seguir de saudação:

```powershell
PS C:\> Get-AzureRmKeyVault -InRemovedStateVault 

Name           : ContosoVault
Location             : westus
Id                   : /subscriptions/xxx/providers/Microsoft.KeyVault/locations/westus/deletedVaults/ContosoVault
Resource ID          : /subscriptions/xxx/resourceGroups/ContosoVault/providers/Microsoft.KeyVault/vaults/ContosoVault
Deletion Date        : 5/9/2017 12:14:14 AM
Scheduled Purge Date : 8/7/2017 12:14:14 AM
Tags                 :
```

Olá *ID de recurso* Olá saída refere-se toohello original ID de recurso do cofre. Como este cofre de chaves está em um estado excluído, não há um recurso com essa ID de recurso. Olá *Id* campo pode ser usado tooidentify Olá recurso recuperação ou limpeza. Olá *agendado limpar data* campo indica ao Cofre hello será excluído permanentemente (limpas) se nenhuma ação será tomada para este cofre excluído. Olá Olá de toocalculate período, a utilização de retenção padrão *agendado limpar data*, é de 90 dias.

## <a name="recovering-a-key-vault"></a>Recuperação de um cofre de chaves

toorecover um cofre de chaves, que é necessário que o nome de Cofre de chaves do toospecify hello, grupo de recursos e local. Observe Olá local e o grupo de recursos de saudação do Cofre de chaves Olá excluído conforme necessário para um processo de recuperação de chave de cofre.

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

Quando um cofre de chaves é recuperado, o resultado de saudação é um novo recurso com ID de recurso original do cofre chave Olá Se o grupo de recursos de saudação onde o Cofre de chaves Olá existia foi removido, um novo grupo de recursos com o mesmo nome deve criado antes de Cofre de chaves Olá pode ser recuperado.

## <a name="key-vault-objects-and-soft-delete"></a>Objetos do cofre de chaves e exclusão reversível

Para uma chave, "ContosoFirstKey", em um cofre de chaves chamado "ContosoVault" com a exclusão reversível habilitada, essa chave seria excluída da seguinte maneira.

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

Com o cofre de chaves habilitado para exclusão reversível, uma chave excluída ainda aparece como excluída, exceto, quando você lista ou recupera explicitamente as chaves excluídas. A maioria das operações em uma chave em estado Olá excluído falhará, exceto listagem uma chave excluída, recuperando-la ou limpá-lo. 

Por exemplo, chaves do toorequest toolist excluída em um cofre de chaves, use Olá comando a seguir:

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a>Estado de transição 

Quando você exclui uma chave em um cofre de chaves com exclusão reversível habilitada, pode levar alguns segundos para Olá transição toocomplete. Durante esse estado de transição, pode parecer que chave Olá não está no estado ativo hello ou Olá excluído. Esse comando listará todas as chaves excluídas em seu cofre de chaves chamado "ContosoVault".

```powershell
  Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
  Vault Name           : ContosoVault
  Name                 : ContosoFirstKey
  Id                   : https://ContosoVault.vault.azure.net:443/keys/ContosoFirstKey
  Deleted Date         : 2/14/2017 8:20:52 PM
  Scheduled Purge Date : 5/15/2017 8:20:52 PM
  Enabled              : True
  Expires              :
  Not Before           :
  Created              : 2/14/2017 8:16:07 PM
  Updated              : 2/14/2017 8:16:07 PM
  Tags                 :
```

### <a name="using-soft-delete-with-key-vault-objects"></a>Usar exclusão reversível com objetos de cofre de chaves

Apenas como chave cofres, uma chave excluída, segredo ou certificado permanecerá no estado excluído para backup too90 dias, a menos que recuperá-la ou limpá-lo. 

#### <a name="keys"></a>simétricas

toorecover uma chave excluída:

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

toopermanently excluir uma chave:

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
>A limpeza de uma chave a excluirá permanentemente, ou seja, ela não poderá ser recuperada.

Olá **recuperar** e **limpar** ações têm suas próprias permissões associadas em uma política de acesso do Cofre de chaves. Para um tooexecute capaz de toobe principal do usuário ou serviço um **recuperar** ou **limpar** ação deve tiverem a permissão respectivos Olá para esse objeto (chave ou segredo) na política de acesso do Cofre de chaves de saudação. Por padrão, Olá **limpar** permissão quando não é adicionada a política de acesso do cofre chave tooa atalho 'todos' hello é usado toogrant todas as permissões do usuário tooa. Você deve conceder explicitamente a permissão de **limpeza**. Por exemplo, Olá concessões de comando a seguir user@contoso.com tooperform permissão várias operações nas chaves *ContosoVault* incluindo **limpar**.

#### <a name="set-a-key-vault-access-policy"></a>Definir uma política de acesso de cofre de chaves

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> Se você tiver um cofre de chaves para o qual acabou de habilitar a exclusão reversível, talvez você não tenha as permissões de **recuperação** e **limpeza**.

#### <a name="secrets"></a>Segredos

Assim como as chaves, os segredos em um cofre de chaves são operados com seus próprios comandos. A seguir, são comandos de saudação para excluir, listar, recuperação e limpeza segredos.

- Excluir um segredo chamado SQLPassword: 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- Listar todos os segredos excluídos em um cofre de chaves: 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- Recupere um segredo no estado Olá excluído: 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- Limpar um segredo no estado excluído: 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
>A limpeza de um segredo o excluirá permanentemente, ou seja, ele não poderá ser recuperado.

## <a name="purging-and-key-vaults"></a>Limpeza e cofres de chave

### <a name="key-vault-objects"></a>Objetos do cofre de chaves

A limpeza de uma chave, segredo ou certificado o excluirá permanentemente, ou seja, não será possível recuperá-lo. Cofre de chaves de saudação que continha Olá excluído objeto porém permanecerão intacto assim como todos os outros objetos no cofre de chaves hello. 

### <a name="key-vaults-as-containers"></a>Cofres de chave como contêineres
Quando um cofre de chaves é limpo, todo seu conteúdo, incluindo chaves, segredos e certificados, serão excluídos permanentemente. toopurge um cofre de chaves, use Olá `Remove-AzureRmKeyVault` comando com a opção de saudação `-InRemovedState` e especificando o local de saudação do Cofre de chaves Olá excluído com hello `-Location location` argumento. Você pode encontrar o local de saudação de um cofre excluído usando o comando Olá `Get-AzureRmKeyVault -InRemovedState`.

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
>A limpeza de um cofre de chaves o excluirá permanentemente, ou seja, não será possível recuperá-lo.

### <a name="purge-permissions-required"></a>Permissões de limpeza necessárias
- toopurge um cofre de chaves excluído, por exemplo, que cofre hello e todo seu conteúdo será removido permanentemente, Olá usuário precisa de RBAC permissão tooperform um *Microsoft.KeyVault/locations/deletedVaults/purge/action* operação. 
- chave de saudação excluída toolist cofre Olá um usuário precisa RBAC permissão tooperform *Microsoft.KeyVault/deletedVaults/read* permissão. 
- Por padrão, somente um administrador de assinatura tem essas permissões. 

### <a name="scheduled-purge"></a>Limpeza agendada

Listar os objetos excluídos de Cofre de chaves mostra quando eles são toobe schedled limpo pelo Cofre de chaves. Olá *agendado limpar data* campo indica quando um objeto de Cofre de chaves será excluído permanentemente, se nenhuma ação será tomada. Por padrão, o período de retenção de saudação para um objeto excluído cofre da chave é de 90 dias.

>[!NOTE]
>Um objeto de cofre limpo, disparado pelo campo *Data de Limpeza Agendada*, será excluído permanentemente. Ele não é recuperável.

## <a name="other-resources"></a>Outros recursos

- Para obter uma visão geral do recurso de exclusão reversível do Key Vault, veja [Visão geral da exclusão reversível do Azure Key Vault](key-vault-ovw-soft-delete.md).
- Para obter uma visão geral do uso do Azure Key Vault, veja [Introdução ao Azure Key Vault](key-vault-get-started.md).

