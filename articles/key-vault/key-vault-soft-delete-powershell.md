---
ms.assetid: 
title: "Azure Key Vault – Como usar a exclusão reversível com PowerShell"
description: "Usar exemplos de caso de exclusão reversível com trechos de código do PowerShell"
services: key-vault
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/21/2017
ms.author: bruceper
ms.openlocfilehash: 8cf0674f7eb139e50da4a3c22a8d8376a86b0dcc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="8b197-103">Como usar a exclusão reversível do Key Vault com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b197-103">How to use Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="8b197-104">O recurso de exclusão reversível do Azure Key Vault permite a recuperação de cofres e objetos de cofre excluídos.</span><span class="sxs-lookup"><span data-stu-id="8b197-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="8b197-105">Especificamente, a exclusão reversível atende aos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="8b197-105">Specifically, soft-delete addresses the following scenarios:</span></span>

- <span data-ttu-id="8b197-106">Suporte à exclusão reversível de cofres de chaves</span><span class="sxs-lookup"><span data-stu-id="8b197-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="8b197-107">Suporte à exclusão reversível de objetos do cofre de chaves, chaves, segredos e certificados</span><span class="sxs-lookup"><span data-stu-id="8b197-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b197-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8b197-108">Prerequisites</span></span>

- <span data-ttu-id="8b197-109">Azure PowerShell 4.0.0 ou posterior – se você ainda não tiver configurado isso, instale o Azure PowerShell e associe-o à sua assinatura do Azure, veja [Como instalar e configurar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8b197-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="8b197-110">Há uma versão desatualizada de nosso arquivo de formatação de saída do PowerShell do Key Vault que **pode** ser carregada em seu ambiente, em vez da versão correta.</span><span class="sxs-lookup"><span data-stu-id="8b197-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of the correct version.</span></span> <span data-ttu-id="8b197-111">Estamos antecipando uma versão atualizada do PowerShell para conter a correção necessária para a formatação de saída e atualizaremos este tópico nessa ocasião.</span><span class="sxs-lookup"><span data-stu-id="8b197-111">We are anticipating an updated version of PowerShell to contain the needed correction for the output formatting and will update this topic at that time.</span></span> <span data-ttu-id="8b197-112">A solução alternativa atual, caso você tenha esse problema de formatação, é:</span><span class="sxs-lookup"><span data-stu-id="8b197-112">The current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="8b197-113">Use a consulta a seguir se você perceber que não está vendo a propriedade habilitada para exclusão reversível descrita neste tópico: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span><span class="sxs-lookup"><span data-stu-id="8b197-113">Use the following query if you notice you're not seeing the soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="8b197-114">Para saber mais de referência específicas do Key Vault para o PowerShell, veja [Referência do PowerShell do Azure Key Vault](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="8b197-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="8b197-115">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="8b197-115">Required permissions</span></span>

<span data-ttu-id="8b197-116">As operações de Key Vault são gerenciadas separadamente por meio de permissões de RBAC (controle de acesso baseado em função) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8b197-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="8b197-117">Operação</span><span class="sxs-lookup"><span data-stu-id="8b197-117">Operation</span></span> | <span data-ttu-id="8b197-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="8b197-118">Description</span></span> | <span data-ttu-id="8b197-119">Permissão de usuário</span><span class="sxs-lookup"><span data-stu-id="8b197-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="8b197-120">Listar</span><span class="sxs-lookup"><span data-stu-id="8b197-120">List</span></span>|<span data-ttu-id="8b197-121">Lista os cofres de chaves excluídos.</span><span class="sxs-lookup"><span data-stu-id="8b197-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="8b197-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="8b197-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="8b197-123">Recuperar</span><span class="sxs-lookup"><span data-stu-id="8b197-123">Recover</span></span>|<span data-ttu-id="8b197-124">Recupera o cofre de chaves excluído.</span><span class="sxs-lookup"><span data-stu-id="8b197-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="8b197-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="8b197-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="8b197-126">Limpar</span><span class="sxs-lookup"><span data-stu-id="8b197-126">Purge</span></span>|<span data-ttu-id="8b197-127">Remove permanentemente um cofre de chaves excluído e todo o seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="8b197-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="8b197-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="8b197-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="8b197-129">Para saber mais sobre permissões e controle de acesso, veja [Proteger seu cofre de chaves](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="8b197-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="8b197-130">Habilitar a exclusão reversível</span><span class="sxs-lookup"><span data-stu-id="8b197-130">Enabling soft-delete</span></span>

<span data-ttu-id="8b197-131">Para poder recuperar um cofre de chaves excluído, ou objetos armazenados em um cofre de chaves, primeiro você deve habilitar a exclusão reversível para esse cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="8b197-131">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="8b197-132">Cofre de chaves existente</span><span class="sxs-lookup"><span data-stu-id="8b197-132">Existing key vault</span></span>

<span data-ttu-id="8b197-133">Para um cofre de chaves existente chamado ContosoVault, habilite a exclusão reversível da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="8b197-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="8b197-134">Atualmente, você precisa usar a manipulação de recursos do Azure Resource Manager para gravar a propriedade *enableSoftDelete* diretamente no recurso Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8b197-134">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="8b197-135">Novo cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="8b197-135">New key vault</span></span>

<span data-ttu-id="8b197-136">A habilitação da exclusão reversível para um novo cofre de chaves é feita no momento da criação adicionando o sinalizador de habilitação de exclusão reversível ao comando create.</span><span class="sxs-lookup"><span data-stu-id="8b197-136">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="8b197-137">Verificar a habilitação da exclusão reversível</span><span class="sxs-lookup"><span data-stu-id="8b197-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="8b197-138">Para verificar se um cofre de chaves tem exclusão reversível habilitada, execute o comando *get* e procure o atributo 'Exclusão Reversível Habilitada?'</span><span class="sxs-lookup"><span data-stu-id="8b197-138">To verify that a key vault has soft-delete enabled, run the *get* command and look for the 'Soft Delete Enabled?'</span></span> <span data-ttu-id="8b197-139">e sua configuração, true ou false.</span><span class="sxs-lookup"><span data-stu-id="8b197-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="8b197-140">Excluir um cofre de chaves protegido por exclusão reversível</span><span class="sxs-lookup"><span data-stu-id="8b197-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="8b197-141">O comando para excluir (ou remover) um cofre de chaves permanece o mesmo, mas seu comportamento muda dependendo da habilitação ou não da exclusão reversível.</span><span class="sxs-lookup"><span data-stu-id="8b197-141">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="8b197-142">Se você executar o comando anterior para um cofre de chaves que não tenha a exclusão reversível habilitada, você excluirá permanentemente esse cofre de chaves e todo seu conteúdo sem opções de recuperação.</span><span class="sxs-lookup"><span data-stu-id="8b197-142">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="8b197-143">Como a exclusão reversível protege seus cofres de chaves</span><span class="sxs-lookup"><span data-stu-id="8b197-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="8b197-144">Com a exclusão reversível habilitada:</span><span class="sxs-lookup"><span data-stu-id="8b197-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="8b197-145">Quando um cofre de chaves é excluído, ele é removido de seu grupo de recursos e colocado em um namespace reservado, associado apenas ao local onde foi criado.</span><span class="sxs-lookup"><span data-stu-id="8b197-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span></span> 
- <span data-ttu-id="8b197-146">Os objetos em um cofre de chaves excluído, como chaves, segredos e certificados, não estão acessíveis e permanecem assim enquanto o cofre de chaves que os contêm estiver no estado excluído.</span><span class="sxs-lookup"><span data-stu-id="8b197-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span></span> 
- <span data-ttu-id="8b197-147">O nome DNS de um cofre de chaves em um estado excluído ainda é reservado, portanto, não é possível criar um novo cofre de chaves com o mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="8b197-147">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="8b197-148">Você pode exibir cofres de chave no estado excluído, associados à sua assinatura, usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8b197-148">You may view deleted state key vaults, associated with your subscription, using the following command:</span></span>

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

<span data-ttu-id="8b197-149">A *ID do Recurso* na saída faz referência à ID do recurso original desse cofre.</span><span class="sxs-lookup"><span data-stu-id="8b197-149">The *Resource ID* in the output refers to the original resource ID of this vault.</span></span> <span data-ttu-id="8b197-150">Como este cofre de chaves está em um estado excluído, não há um recurso com essa ID de recurso.</span><span class="sxs-lookup"><span data-stu-id="8b197-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="8b197-151">O campo *Id* pode ser usado para identificar o recurso durante a recuperação ou limpeza.</span><span class="sxs-lookup"><span data-stu-id="8b197-151">The *Id* field can be used to identify the resource when recovering, or purging.</span></span> <span data-ttu-id="8b197-152">O campo *Data de Limpeza Agendada* indica quando o cofre será excluído permanentemente (limpo) se nenhuma ação for realizada para esse cofre excluído.</span><span class="sxs-lookup"><span data-stu-id="8b197-152">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="8b197-153">O período de retenção padrão, usado para calcular a *Data de Limpeza Agendada*, é de 90 dias.</span><span class="sxs-lookup"><span data-stu-id="8b197-153">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="8b197-154">Recuperação de um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="8b197-154">Recovering a key vault</span></span>

<span data-ttu-id="8b197-155">Para recuperar um cofre de chaves, você precisa especificar o nome do cofre de chaves, o grupo de recursos e o local.</span><span class="sxs-lookup"><span data-stu-id="8b197-155">To recover a key vault, you need to specify the key vault name, resource group, and location.</span></span> <span data-ttu-id="8b197-156">Anote o local e o grupo de recursos do cofre de chaves excluído, pois você precisará deles para um processo de recuperação de cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="8b197-156">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="8b197-157">Após a recuperação de um cofre de chaves, o resultado é um novo recurso com a ID de recurso original do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="8b197-157">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span></span> <span data-ttu-id="8b197-158">Se o grupo de recursos no qual o cofre de chaves residia tiver sido removido, um novo grupo de recursos com o mesmo nome deverá ser criado antes da recuperação do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="8b197-158">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="8b197-159">Objetos do cofre de chaves e exclusão reversível</span><span class="sxs-lookup"><span data-stu-id="8b197-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="8b197-160">Para uma chave, "ContosoFirstKey", em um cofre de chaves chamado "ContosoVault" com a exclusão reversível habilitada, essa chave seria excluída da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="8b197-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="8b197-161">Com o cofre de chaves habilitado para exclusão reversível, uma chave excluída ainda aparece como excluída, exceto, quando você lista ou recupera explicitamente as chaves excluídas.</span><span class="sxs-lookup"><span data-stu-id="8b197-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="8b197-162">A maioria das operações em uma chave no estado excluído falhará, exceto para listagem, recuperação ou limpeza de uma chave excluída.</span><span class="sxs-lookup"><span data-stu-id="8b197-162">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="8b197-163">Por exemplo, para solicitar a listagem de chaves excluídas em um cofre de chaves, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8b197-163">For example, to request to list deleted keys in a key vault, use the following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="8b197-164">Estado de transição</span><span class="sxs-lookup"><span data-stu-id="8b197-164">Transition state</span></span> 

<span data-ttu-id="8b197-165">Quando você exclui uma chave em um cofre de chaves com exclusão reversível habilitada, talvez demore alguns segundos para a transição ser concluída.</span><span class="sxs-lookup"><span data-stu-id="8b197-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span></span> <span data-ttu-id="8b197-166">Durante esse estado de transição, pode parecer que a chave não esteja no estado ativo ou no estado excluído.</span><span class="sxs-lookup"><span data-stu-id="8b197-166">During this transition state, it may appear that the key is not in the active state or the deleted state.</span></span> <span data-ttu-id="8b197-167">Esse comando listará todas as chaves excluídas em seu cofre de chaves chamado "ContosoVault".</span><span class="sxs-lookup"><span data-stu-id="8b197-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

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

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="8b197-168">Usar exclusão reversível com objetos de cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="8b197-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="8b197-169">Assim como os cofres de chave, uma chave, segredo ou certificado excluído permanecerá no estado excluído por até 90 dias, a menos que você o recupere ou limpe.</span><span class="sxs-lookup"><span data-stu-id="8b197-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="8b197-170">simétricas</span><span class="sxs-lookup"><span data-stu-id="8b197-170">Keys</span></span>

<span data-ttu-id="8b197-171">Para recuperar uma chave excluída:</span><span class="sxs-lookup"><span data-stu-id="8b197-171">To recover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="8b197-172">Para excluir permanentemente uma chave:</span><span class="sxs-lookup"><span data-stu-id="8b197-172">To permanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="8b197-173">A limpeza de uma chave a excluirá permanentemente, ou seja, ela não poderá ser recuperada.</span><span class="sxs-lookup"><span data-stu-id="8b197-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="8b197-174">As ações de **recuperação** e **limpeza** têm suas próprias permissões associadas em uma política de acesso de cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="8b197-174">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="8b197-175">Para que um usuário ou entidade de serviço possa executar uma ação de **recuperação** ou **limpeza**, ele precisa ter a permissão respectiva para esse objeto (chave ou segredo) na política de acesso de cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="8b197-175">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span></span> <span data-ttu-id="8b197-176">Por padrão, a permissão de **limpeza** não é adicionada à política de acesso de um cofre de chaves quando o atalho "todos" for usado para conceder todas as permissões a um usuário.</span><span class="sxs-lookup"><span data-stu-id="8b197-176">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span></span> <span data-ttu-id="8b197-177">Você deve conceder explicitamente a permissão de **limpeza**.</span><span class="sxs-lookup"><span data-stu-id="8b197-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="8b197-178">Por exemplo, o comando a seguir concede a permissão user@contoso.com para executar várias operações em chaves no *ContosoVault*, incluindo **limpar**.</span><span class="sxs-lookup"><span data-stu-id="8b197-178">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="8b197-179">Definir uma política de acesso de cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="8b197-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="8b197-180">Se você tiver um cofre de chaves para o qual acabou de habilitar a exclusão reversível, talvez você não tenha as permissões de **recuperação** e **limpeza**.</span><span class="sxs-lookup"><span data-stu-id="8b197-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="8b197-181">Segredos</span><span class="sxs-lookup"><span data-stu-id="8b197-181">Secrets</span></span>

<span data-ttu-id="8b197-182">Assim como as chaves, os segredos em um cofre de chaves são operados com seus próprios comandos.</span><span class="sxs-lookup"><span data-stu-id="8b197-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="8b197-183">Veja a seguir os comandos para excluir, listar, recuperar e limpar os segredos.</span><span class="sxs-lookup"><span data-stu-id="8b197-183">Following, are the commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="8b197-184">Excluir um segredo chamado SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="8b197-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="8b197-185">Listar todos os segredos excluídos em um cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="8b197-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="8b197-186">Recuperar um segredo no estado excluído:</span><span class="sxs-lookup"><span data-stu-id="8b197-186">Recover a secret in the deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="8b197-187">Limpar um segredo no estado excluído:</span><span class="sxs-lookup"><span data-stu-id="8b197-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="8b197-188">A limpeza de um segredo o excluirá permanentemente, ou seja, ele não poderá ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="8b197-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="8b197-189">Limpeza e cofres de chave</span><span class="sxs-lookup"><span data-stu-id="8b197-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="8b197-190">Objetos do cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="8b197-190">Key vault objects</span></span>

<span data-ttu-id="8b197-191">A limpeza de uma chave, segredo ou certificado o excluirá permanentemente, ou seja, não será possível recuperá-lo.</span><span class="sxs-lookup"><span data-stu-id="8b197-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="8b197-192">O cofre de chaves que continha o objeto excluído permanecerá intacto, assim como todos os outros objetos no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="8b197-192">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="8b197-193">Cofres de chave como contêineres</span><span class="sxs-lookup"><span data-stu-id="8b197-193">Key vaults as containers</span></span>
<span data-ttu-id="8b197-194">Quando um cofre de chaves é limpo, todo seu conteúdo, incluindo chaves, segredos e certificados, serão excluídos permanentemente.</span><span class="sxs-lookup"><span data-stu-id="8b197-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="8b197-195">Para limpar um cofre de chaves, use o comando `Remove-AzureRmKeyVault` com a opção `-InRemovedState` e especifique o local do cofre da chave excluído com o argumento `-Location location`.</span><span class="sxs-lookup"><span data-stu-id="8b197-195">To purge a key vault, use the `Remove-AzureRmKeyVault` command with the option `-InRemovedState` and by specifying the location of the deleted key vault with the `-Location location` argument.</span></span> <span data-ttu-id="8b197-196">Você pode encontrar o local de um cofre excluído usando o comando `Get-AzureRmKeyVault -InRemovedState`.</span><span class="sxs-lookup"><span data-stu-id="8b197-196">You can find the location of a deleted vault using the command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="8b197-197">A limpeza de um cofre de chaves o excluirá permanentemente, ou seja, não será possível recuperá-lo.</span><span class="sxs-lookup"><span data-stu-id="8b197-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="8b197-198">Permissões de limpeza necessárias</span><span class="sxs-lookup"><span data-stu-id="8b197-198">Purge permissions required</span></span>
- <span data-ttu-id="8b197-199">Para limpar um cofre de chaves excluído, de modo que o cofre e todo seu conteúdo seja removido permanentemente, o usuário precisa de permissão RBAC para executar uma operação *Microsoft.KeyVault/locations/deletedVaults/purge/action*.</span><span class="sxs-lookup"><span data-stu-id="8b197-199">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="8b197-200">Para listar a chave excluída, o cofre de um usuário precisa de permissão RBAC para executar a permissão *Microsoft.KeyVault/deletedVaults/read*.</span><span class="sxs-lookup"><span data-stu-id="8b197-200">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="8b197-201">Por padrão, somente um administrador de assinatura tem essas permissões.</span><span class="sxs-lookup"><span data-stu-id="8b197-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="8b197-202">Limpeza agendada</span><span class="sxs-lookup"><span data-stu-id="8b197-202">Scheduled purge</span></span>

<span data-ttu-id="8b197-203">A listagem de seus objetos de cofre de chaves excluídos mostra o agendamento da limpeza pelo Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8b197-203">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span></span> <span data-ttu-id="8b197-204">O campo *Data de Limpeza Agendada* indica quando o objeto do cofre de chaves será excluído permanentemente se nenhuma ação for realizada.</span><span class="sxs-lookup"><span data-stu-id="8b197-204">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="8b197-205">Por padrão, o período de retenção para um objeto do cofre de chaves excluído é de 90 dias.</span><span class="sxs-lookup"><span data-stu-id="8b197-205">By default, the retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="8b197-206">Um objeto de cofre limpo, disparado pelo campo *Data de Limpeza Agendada*, será excluído permanentemente.</span><span class="sxs-lookup"><span data-stu-id="8b197-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="8b197-207">Ele não é recuperável.</span><span class="sxs-lookup"><span data-stu-id="8b197-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="8b197-208">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="8b197-208">Other resources</span></span>

- <span data-ttu-id="8b197-209">Para obter uma visão geral do recurso de exclusão reversível do Key Vault, veja [Visão geral da exclusão reversível do Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="8b197-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="8b197-210">Para obter uma visão geral do uso do Azure Key Vault, veja [Introdução ao Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8b197-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

