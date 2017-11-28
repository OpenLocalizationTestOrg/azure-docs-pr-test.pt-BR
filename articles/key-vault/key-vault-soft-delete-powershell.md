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
# <a name="how-toouse-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="07162-103">Como toouse Cofre de chaves soft-exclusão com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="07162-103">How toouse Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="07162-104">O recurso de exclusão reversível do Azure Key Vault permite a recuperação de cofres e objetos de cofre excluídos.</span><span class="sxs-lookup"><span data-stu-id="07162-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="07162-105">Especificamente, os endereços de exclusão reversível Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="07162-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="07162-106">Suporte à exclusão reversível de cofres de chaves</span><span class="sxs-lookup"><span data-stu-id="07162-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="07162-107">Suporte à exclusão reversível de objetos do cofre de chaves, chaves, segredos e certificados</span><span class="sxs-lookup"><span data-stu-id="07162-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07162-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="07162-108">Prerequisites</span></span>

- <span data-ttu-id="07162-109">O Azure PowerShell 4.0.0 ou posterior - se você não nesse já que a instalação, instale o Azure PowerShell e associá-lo a sua assinatura do Azure, consulte [como tooinstall e configurar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="07162-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="07162-110">Há uma versão desatualizada do nosso formatação de saída do PowerShell do Cofre de chave de arquivo que **pode** ser carregado em seu ambiente, em vez da versão correta do hello.</span><span class="sxs-lookup"><span data-stu-id="07162-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of hello correct version.</span></span> <span data-ttu-id="07162-111">Nós estão prevendo que uma versão atualizada do PowerShell toocontain Olá necessário correção para formatação de saída de hello e atualizará este tópico no momento.</span><span class="sxs-lookup"><span data-stu-id="07162-111">We are anticipating an updated version of PowerShell toocontain hello needed correction for hello output formatting and will update this topic at that time.</span></span> <span data-ttu-id="07162-112">Olá solução atual, se você encontrar esse problema de formatação, é:</span><span class="sxs-lookup"><span data-stu-id="07162-112">hello current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="07162-113">Olá Use consulta a seguir se você perceber que você não estiver vendo hello exclusão reversível habilitada propriedade descrita neste tópico: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span><span class="sxs-lookup"><span data-stu-id="07162-113">Use hello following query if you notice you're not seeing hello soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="07162-114">Para saber mais de referência específicas do Key Vault para o PowerShell, veja [Referência do PowerShell do Azure Key Vault](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="07162-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="07162-115">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="07162-115">Required permissions</span></span>

<span data-ttu-id="07162-116">As operações de Key Vault são gerenciadas separadamente por meio de permissões de RBAC (controle de acesso baseado em função) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="07162-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="07162-117">Operação</span><span class="sxs-lookup"><span data-stu-id="07162-117">Operation</span></span> | <span data-ttu-id="07162-118">Descrição</span><span class="sxs-lookup"><span data-stu-id="07162-118">Description</span></span> | <span data-ttu-id="07162-119">Permissão de usuário</span><span class="sxs-lookup"><span data-stu-id="07162-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="07162-120">Listar</span><span class="sxs-lookup"><span data-stu-id="07162-120">List</span></span>|<span data-ttu-id="07162-121">Lista os cofres de chaves excluídos.</span><span class="sxs-lookup"><span data-stu-id="07162-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="07162-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="07162-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="07162-123">Recuperar</span><span class="sxs-lookup"><span data-stu-id="07162-123">Recover</span></span>|<span data-ttu-id="07162-124">Recupera o cofre de chaves excluído.</span><span class="sxs-lookup"><span data-stu-id="07162-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="07162-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="07162-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="07162-126">Limpar</span><span class="sxs-lookup"><span data-stu-id="07162-126">Purge</span></span>|<span data-ttu-id="07162-127">Remove permanentemente um cofre de chaves excluído e todo o seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="07162-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="07162-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="07162-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="07162-129">Para saber mais sobre permissões e controle de acesso, veja [Proteger seu cofre de chaves](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="07162-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="07162-130">Habilitar a exclusão reversível</span><span class="sxs-lookup"><span data-stu-id="07162-130">Enabling soft-delete</span></span>

<span data-ttu-id="07162-131">toorecover capaz de toobe um cofre de chaves excluído ou objetos armazenados em uma chave de cofre, você deve primeiro habilitar a exclusão reversível para esse Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="07162-131">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="07162-132">Cofre de chaves existente</span><span class="sxs-lookup"><span data-stu-id="07162-132">Existing key vault</span></span>

<span data-ttu-id="07162-133">Para um cofre de chaves existente chamado ContosoVault, habilite a exclusão reversível da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="07162-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="07162-134">Atualmente é necessário Olá de gravação do toouse do Azure Resource Manager recursos manipulação toodirectly *enableSoftDelete* toohello de propriedade de recurso de Cofre de chave.</span><span class="sxs-lookup"><span data-stu-id="07162-134">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="07162-135">Novo cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="07162-135">New key vault</span></span>

<span data-ttu-id="07162-136">Habilitar exclusão reversível para um novo cofre de chave é feito no momento da criação, adicionando o sinalizador de exclusão reversível do hello tooyour criar o comando.</span><span class="sxs-lookup"><span data-stu-id="07162-136">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="07162-137">Verificar a habilitação da exclusão reversível</span><span class="sxs-lookup"><span data-stu-id="07162-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="07162-138">tooverify um cofre de chaves com exclusão reversível habilitada, Olá execução *obter* de comando e procure hello "Flexível excluir ativado?"</span><span class="sxs-lookup"><span data-stu-id="07162-138">tooverify that a key vault has soft-delete enabled, run hello *get* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="07162-139">e sua configuração, true ou false.</span><span class="sxs-lookup"><span data-stu-id="07162-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="07162-140">Excluir um cofre de chaves protegido por exclusão reversível</span><span class="sxs-lookup"><span data-stu-id="07162-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="07162-141">Olá comando toodelete (ou remover) um cofre de chaves permanece Olá mesmo, mas suas alterações de comportamento dependendo se você habilitou o soft-exclusão ou não.</span><span class="sxs-lookup"><span data-stu-id="07162-141">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="07162-142">Se você executar o comando anterior de saudação para um cofre de chaves que não tenha habilitada a exclusão reversível, você excluirá permanentemente este cofre de chaves e todo o seu conteúdo sem opções de recuperação.</span><span class="sxs-lookup"><span data-stu-id="07162-142">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="07162-143">Como a exclusão reversível protege seus cofres de chaves</span><span class="sxs-lookup"><span data-stu-id="07162-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="07162-144">Com a exclusão reversível habilitada:</span><span class="sxs-lookup"><span data-stu-id="07162-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="07162-145">Quando um cofre de chaves é excluído, ele é removido do seu grupo de recursos e colocado em um espaço reservado que só é associado ao local de saudação onde ele foi criado.</span><span class="sxs-lookup"><span data-stu-id="07162-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="07162-146">Objetos em uma chave excluída cofre, como chaves, segredos e certificados, não estão acessíveis e continuar assim enquanto seu Cofre de chaves que contém está em estado de saudação excluído.</span><span class="sxs-lookup"><span data-stu-id="07162-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="07162-147">Olá nome DNS um cofre de chaves em um estado excluído é preservado, portanto, não é possível criar um novo cofre de chave com o mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="07162-147">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="07162-148">Você pode exibir cofres de chave de estado excluído, associados à sua assinatura, usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="07162-148">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

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

<span data-ttu-id="07162-149">Olá *ID de recurso* Olá saída refere-se toohello original ID de recurso do cofre.</span><span class="sxs-lookup"><span data-stu-id="07162-149">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="07162-150">Como este cofre de chaves está em um estado excluído, não há um recurso com essa ID de recurso.</span><span class="sxs-lookup"><span data-stu-id="07162-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="07162-151">Olá *Id* campo pode ser usado tooidentify Olá recurso recuperação ou limpeza.</span><span class="sxs-lookup"><span data-stu-id="07162-151">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="07162-152">Olá *agendado limpar data* campo indica ao Cofre hello será excluído permanentemente (limpas) se nenhuma ação será tomada para este cofre excluído.</span><span class="sxs-lookup"><span data-stu-id="07162-152">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="07162-153">Olá Olá de toocalculate período, a utilização de retenção padrão *agendado limpar data*, é de 90 dias.</span><span class="sxs-lookup"><span data-stu-id="07162-153">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="07162-154">Recuperação de um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="07162-154">Recovering a key vault</span></span>

<span data-ttu-id="07162-155">toorecover um cofre de chaves, que é necessário que o nome de Cofre de chaves do toospecify hello, grupo de recursos e local.</span><span class="sxs-lookup"><span data-stu-id="07162-155">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="07162-156">Observe Olá local e o grupo de recursos de saudação do Cofre de chaves Olá excluído conforme necessário para um processo de recuperação de chave de cofre.</span><span class="sxs-lookup"><span data-stu-id="07162-156">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="07162-157">Quando um cofre de chaves é recuperado, o resultado de saudação é um novo recurso com ID de recurso original do cofre chave Olá</span><span class="sxs-lookup"><span data-stu-id="07162-157">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="07162-158">Se o grupo de recursos de saudação onde o Cofre de chaves Olá existia foi removido, um novo grupo de recursos com o mesmo nome deve criado antes de Cofre de chaves Olá pode ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="07162-158">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="07162-159">Objetos do cofre de chaves e exclusão reversível</span><span class="sxs-lookup"><span data-stu-id="07162-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="07162-160">Para uma chave, "ContosoFirstKey", em um cofre de chaves chamado "ContosoVault" com a exclusão reversível habilitada, essa chave seria excluída da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="07162-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="07162-161">Com o cofre de chaves habilitado para exclusão reversível, uma chave excluída ainda aparece como excluída, exceto, quando você lista ou recupera explicitamente as chaves excluídas.</span><span class="sxs-lookup"><span data-stu-id="07162-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="07162-162">A maioria das operações em uma chave em estado Olá excluído falhará, exceto listagem uma chave excluída, recuperando-la ou limpá-lo.</span><span class="sxs-lookup"><span data-stu-id="07162-162">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="07162-163">Por exemplo, chaves do toorequest toolist excluída em um cofre de chaves, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="07162-163">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="07162-164">Estado de transição</span><span class="sxs-lookup"><span data-stu-id="07162-164">Transition state</span></span> 

<span data-ttu-id="07162-165">Quando você exclui uma chave em um cofre de chaves com exclusão reversível habilitada, pode levar alguns segundos para Olá transição toocomplete.</span><span class="sxs-lookup"><span data-stu-id="07162-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="07162-166">Durante esse estado de transição, pode parecer que chave Olá não está no estado ativo hello ou Olá excluído.</span><span class="sxs-lookup"><span data-stu-id="07162-166">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="07162-167">Esse comando listará todas as chaves excluídas em seu cofre de chaves chamado "ContosoVault".</span><span class="sxs-lookup"><span data-stu-id="07162-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

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

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="07162-168">Usar exclusão reversível com objetos de cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="07162-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="07162-169">Apenas como chave cofres, uma chave excluída, segredo ou certificado permanecerá no estado excluído para backup too90 dias, a menos que recuperá-la ou limpá-lo.</span><span class="sxs-lookup"><span data-stu-id="07162-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="07162-170">simétricas</span><span class="sxs-lookup"><span data-stu-id="07162-170">Keys</span></span>

<span data-ttu-id="07162-171">toorecover uma chave excluída:</span><span class="sxs-lookup"><span data-stu-id="07162-171">toorecover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="07162-172">toopermanently excluir uma chave:</span><span class="sxs-lookup"><span data-stu-id="07162-172">toopermanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="07162-173">A limpeza de uma chave a excluirá permanentemente, ou seja, ela não poderá ser recuperada.</span><span class="sxs-lookup"><span data-stu-id="07162-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="07162-174">Olá **recuperar** e **limpar** ações têm suas próprias permissões associadas em uma política de acesso do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="07162-174">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="07162-175">Para um tooexecute capaz de toobe principal do usuário ou serviço um **recuperar** ou **limpar** ação deve tiverem a permissão respectivos Olá para esse objeto (chave ou segredo) na política de acesso do Cofre de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="07162-175">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="07162-176">Por padrão, Olá **limpar** permissão quando não é adicionada a política de acesso do cofre chave tooa atalho 'todos' hello é usado toogrant todas as permissões do usuário tooa.</span><span class="sxs-lookup"><span data-stu-id="07162-176">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="07162-177">Você deve conceder explicitamente a permissão de **limpeza**.</span><span class="sxs-lookup"><span data-stu-id="07162-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="07162-178">Por exemplo, Olá concessões de comando a seguir user@contoso.com tooperform permissão várias operações nas chaves *ContosoVault* incluindo **limpar**.</span><span class="sxs-lookup"><span data-stu-id="07162-178">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="07162-179">Definir uma política de acesso de cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="07162-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="07162-180">Se você tiver um cofre de chaves para o qual acabou de habilitar a exclusão reversível, talvez você não tenha as permissões de **recuperação** e **limpeza**.</span><span class="sxs-lookup"><span data-stu-id="07162-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="07162-181">Segredos</span><span class="sxs-lookup"><span data-stu-id="07162-181">Secrets</span></span>

<span data-ttu-id="07162-182">Assim como as chaves, os segredos em um cofre de chaves são operados com seus próprios comandos.</span><span class="sxs-lookup"><span data-stu-id="07162-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="07162-183">A seguir, são comandos de saudação para excluir, listar, recuperação e limpeza segredos.</span><span class="sxs-lookup"><span data-stu-id="07162-183">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="07162-184">Excluir um segredo chamado SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="07162-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="07162-185">Listar todos os segredos excluídos em um cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="07162-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="07162-186">Recupere um segredo no estado Olá excluído:</span><span class="sxs-lookup"><span data-stu-id="07162-186">Recover a secret in hello deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="07162-187">Limpar um segredo no estado excluído:</span><span class="sxs-lookup"><span data-stu-id="07162-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="07162-188">A limpeza de um segredo o excluirá permanentemente, ou seja, ele não poderá ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="07162-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="07162-189">Limpeza e cofres de chave</span><span class="sxs-lookup"><span data-stu-id="07162-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="07162-190">Objetos do cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="07162-190">Key vault objects</span></span>

<span data-ttu-id="07162-191">A limpeza de uma chave, segredo ou certificado o excluirá permanentemente, ou seja, não será possível recuperá-lo.</span><span class="sxs-lookup"><span data-stu-id="07162-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="07162-192">Cofre de chaves de saudação que continha Olá excluído objeto porém permanecerão intacto assim como todos os outros objetos no cofre de chaves hello.</span><span class="sxs-lookup"><span data-stu-id="07162-192">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="07162-193">Cofres de chave como contêineres</span><span class="sxs-lookup"><span data-stu-id="07162-193">Key vaults as containers</span></span>
<span data-ttu-id="07162-194">Quando um cofre de chaves é limpo, todo seu conteúdo, incluindo chaves, segredos e certificados, serão excluídos permanentemente.</span><span class="sxs-lookup"><span data-stu-id="07162-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="07162-195">toopurge um cofre de chaves, use Olá `Remove-AzureRmKeyVault` comando com a opção de saudação `-InRemovedState` e especificando o local de saudação do Cofre de chaves Olá excluído com hello `-Location location` argumento.</span><span class="sxs-lookup"><span data-stu-id="07162-195">toopurge a key vault, use hello `Remove-AzureRmKeyVault` command with hello option `-InRemovedState` and by specifying hello location of hello deleted key vault with hello `-Location location` argument.</span></span> <span data-ttu-id="07162-196">Você pode encontrar o local de saudação de um cofre excluído usando o comando Olá `Get-AzureRmKeyVault -InRemovedState`.</span><span class="sxs-lookup"><span data-stu-id="07162-196">You can find hello location of a deleted vault using hello command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="07162-197">A limpeza de um cofre de chaves o excluirá permanentemente, ou seja, não será possível recuperá-lo.</span><span class="sxs-lookup"><span data-stu-id="07162-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="07162-198">Permissões de limpeza necessárias</span><span class="sxs-lookup"><span data-stu-id="07162-198">Purge permissions required</span></span>
- <span data-ttu-id="07162-199">toopurge um cofre de chaves excluído, por exemplo, que cofre hello e todo seu conteúdo será removido permanentemente, Olá usuário precisa de RBAC permissão tooperform um *Microsoft.KeyVault/locations/deletedVaults/purge/action* operação.</span><span class="sxs-lookup"><span data-stu-id="07162-199">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="07162-200">chave de saudação excluída toolist cofre Olá um usuário precisa RBAC permissão tooperform *Microsoft.KeyVault/deletedVaults/read* permissão.</span><span class="sxs-lookup"><span data-stu-id="07162-200">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="07162-201">Por padrão, somente um administrador de assinatura tem essas permissões.</span><span class="sxs-lookup"><span data-stu-id="07162-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="07162-202">Limpeza agendada</span><span class="sxs-lookup"><span data-stu-id="07162-202">Scheduled purge</span></span>

<span data-ttu-id="07162-203">Listar os objetos excluídos de Cofre de chaves mostra quando eles são toobe schedled limpo pelo Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="07162-203">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="07162-204">Olá *agendado limpar data* campo indica quando um objeto de Cofre de chaves será excluído permanentemente, se nenhuma ação será tomada.</span><span class="sxs-lookup"><span data-stu-id="07162-204">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="07162-205">Por padrão, o período de retenção de saudação para um objeto excluído cofre da chave é de 90 dias.</span><span class="sxs-lookup"><span data-stu-id="07162-205">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="07162-206">Um objeto de cofre limpo, disparado pelo campo *Data de Limpeza Agendada*, será excluído permanentemente.</span><span class="sxs-lookup"><span data-stu-id="07162-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="07162-207">Ele não é recuperável.</span><span class="sxs-lookup"><span data-stu-id="07162-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="07162-208">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="07162-208">Other resources</span></span>

- <span data-ttu-id="07162-209">Para obter uma visão geral do recurso de exclusão reversível do Key Vault, veja [Visão geral da exclusão reversível do Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="07162-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="07162-210">Para obter uma visão geral do uso do Azure Key Vault, veja [Introdução ao Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="07162-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

