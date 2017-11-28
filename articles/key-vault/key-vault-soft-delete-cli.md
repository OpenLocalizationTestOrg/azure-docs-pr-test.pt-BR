---
ms.assetid: 
title: "Azure Key Vault – Como usar a exclusão reversível com a CLI"
description: "Usar exemplos de caso de exclusão reversível com trechos de código da CLI"
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 3ee2c5dfb99d734cde25894174466b8e49823c67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-key-vault-soft-delete-with-cli"></a><span data-ttu-id="b6a6b-103">Como usar a exclusão reversível do Key Vault com a CLI</span><span class="sxs-lookup"><span data-stu-id="b6a6b-103">How to use Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="b6a6b-104">O recurso de exclusão reversível do Azure Key Vault permite a recuperação de cofres e objetos de cofre excluídos.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="b6a6b-105">Especificamente, a exclusão reversível atende aos seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="b6a6b-105">Specifically, soft-delete addresses the following scenarios:</span></span>

- <span data-ttu-id="b6a6b-106">Suporte à exclusão reversível de cofres de chaves</span><span class="sxs-lookup"><span data-stu-id="b6a6b-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="b6a6b-107">Suporte à exclusão reversível de objetos do cofre de chaves, chaves, segredos e certificados</span><span class="sxs-lookup"><span data-stu-id="b6a6b-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6a6b-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b6a6b-108">Prerequisites</span></span>

- <span data-ttu-id="b6a6b-109">CLI do Azure 2.0 – Se essa configuração não existir para o seu ambiente, veja [Gerenciar Key Vault usando a CLI 2.0](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="b6a6b-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="b6a6b-110">Para saber mais de referência específicas do Key Vault para CLI, veja [Referência de Key Vault da CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="b6a6b-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="b6a6b-111">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="b6a6b-111">Required permissions</span></span>

<span data-ttu-id="b6a6b-112">As operações de Key Vault são gerenciadas separadamente por meio de permissões de RBAC (controle de acesso baseado em função) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="b6a6b-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="b6a6b-113">Operação</span><span class="sxs-lookup"><span data-stu-id="b6a6b-113">Operation</span></span> | <span data-ttu-id="b6a6b-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="b6a6b-114">Description</span></span> | <span data-ttu-id="b6a6b-115">Permissão de usuário</span><span class="sxs-lookup"><span data-stu-id="b6a6b-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="b6a6b-116">Listar</span><span class="sxs-lookup"><span data-stu-id="b6a6b-116">List</span></span>|<span data-ttu-id="b6a6b-117">Lista os cofres de chaves excluídos.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="b6a6b-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="b6a6b-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="b6a6b-119">Recuperar</span><span class="sxs-lookup"><span data-stu-id="b6a6b-119">Recover</span></span>|<span data-ttu-id="b6a6b-120">Recupera o cofre de chaves excluído.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="b6a6b-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="b6a6b-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="b6a6b-122">Limpar</span><span class="sxs-lookup"><span data-stu-id="b6a6b-122">Purge</span></span>|<span data-ttu-id="b6a6b-123">Remove permanentemente um cofre de chaves excluído e todo o seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="b6a6b-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="b6a6b-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="b6a6b-125">Para saber mais sobre permissões e controle de acesso, veja [Proteger seu cofre de chaves](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="b6a6b-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="b6a6b-126">Habilitar a exclusão reversível</span><span class="sxs-lookup"><span data-stu-id="b6a6b-126">Enabling soft-delete</span></span>

<span data-ttu-id="b6a6b-127">Para poder recuperar um cofre de chaves excluído, ou objetos armazenados em um cofre de chaves, primeiro você deve habilitar a exclusão reversível para esse cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-127">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="b6a6b-128">Cofre de chaves existente</span><span class="sxs-lookup"><span data-stu-id="b6a6b-128">Existing key vault</span></span>

<span data-ttu-id="b6a6b-129">Para um cofre de chaves existente chamado ContosoVault, habilite a exclusão reversível da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="b6a6b-130">Atualmente, você precisa usar a manipulação de recursos do Azure Resource Manager para gravar a propriedade *enableSoftDelete* diretamente no recurso Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-130">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="b6a6b-131">Novo cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="b6a6b-131">New key vault</span></span>

<span data-ttu-id="b6a6b-132">A habilitação da exclusão reversível para um novo cofre de chaves é feita no momento da criação adicionando o sinalizador de habilitação de exclusão reversível ao comando create.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-132">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="b6a6b-133">Verificar a habilitação da exclusão reversível</span><span class="sxs-lookup"><span data-stu-id="b6a6b-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="b6a6b-134">Para verificar se um cofre de chaves tem exclusão reversível habilitada, execute o comando *show* e procure o atributo 'Exclusão Reversível Habilitada?'</span><span class="sxs-lookup"><span data-stu-id="b6a6b-134">To verify that a key vault has soft-delete enabled, run the *show* command and look for the 'Soft Delete Enabled?'</span></span> <span data-ttu-id="b6a6b-135">e sua configuração, true ou false.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="b6a6b-136">Excluir um cofre de chaves protegido por exclusão reversível</span><span class="sxs-lookup"><span data-stu-id="b6a6b-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="b6a6b-137">O comando para excluir (ou remover) um cofre de chaves permanece o mesmo, mas seu comportamento muda dependendo da habilitação ou não da exclusão reversível.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-137">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="b6a6b-138">Se você executar o comando anterior para um cofre de chaves que não tenha a exclusão reversível habilitada, você excluirá permanentemente esse cofre de chaves e todo seu conteúdo sem opções de recuperação.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-138">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="b6a6b-139">Como a exclusão reversível protege seus cofres de chaves</span><span class="sxs-lookup"><span data-stu-id="b6a6b-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="b6a6b-140">Com a exclusão reversível habilitada:</span><span class="sxs-lookup"><span data-stu-id="b6a6b-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="b6a6b-141">Quando um cofre de chaves é excluído, ele é removido de seu grupo de recursos e colocado em um namespace reservado, associado apenas ao local onde foi criado.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span></span> 
- <span data-ttu-id="b6a6b-142">Os objetos em um cofre de chaves excluído, como chaves, segredos e certificados, não estão acessíveis e permanecem assim enquanto o cofre de chaves que os contêm estiver no estado excluído.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span></span> 
- <span data-ttu-id="b6a6b-143">O nome DNS de um cofre de chaves em um estado excluído ainda é reservado, portanto, não é possível criar um novo cofre de chaves com o mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-143">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="b6a6b-144">Você pode exibir cofres de chave no estado excluído, associados à sua assinatura, usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="b6a6b-144">You may view deleted state key vaults, associated with your subscription, using the following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="b6a6b-145">A *ID do Recurso* na saída faz referência à ID do recurso original desse cofre.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-145">The *Resource ID* in the output refers to the original resource ID of this vault.</span></span> <span data-ttu-id="b6a6b-146">Como este cofre de chaves está em um estado excluído, não há um recurso com essa ID de recurso.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="b6a6b-147">O campo *Id* pode ser usado para identificar o recurso durante a recuperação ou limpeza.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-147">The *Id* field can be used to identify the resource when recovering, or purging.</span></span> <span data-ttu-id="b6a6b-148">O campo *Data de Limpeza Agendada* indica quando o cofre será excluído permanentemente (limpo) se nenhuma ação for realizada para esse cofre excluído.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-148">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="b6a6b-149">O período de retenção padrão, usado para calcular a *Data de Limpeza Agendada*, é de 90 dias.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-149">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="b6a6b-150">Recuperação de um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="b6a6b-150">Recovering a key vault</span></span>

<span data-ttu-id="b6a6b-151">Para recuperar um cofre de chaves, você precisa especificar o nome do cofre de chaves, o grupo de recursos e o local.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-151">To recover a key vault, you need to specify the key vault name, resource group, and location.</span></span> <span data-ttu-id="b6a6b-152">Anote o local e o grupo de recursos do cofre de chaves excluído, pois você precisará deles para um processo de recuperação de cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-152">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="b6a6b-153">Após a recuperação de um cofre de chaves, o resultado é um novo recurso com a ID de recurso original do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-153">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span></span> <span data-ttu-id="b6a6b-154">Se o grupo de recursos no qual o cofre de chaves residia tiver sido removido, um novo grupo de recursos com o mesmo nome deverá ser criado antes da recuperação do cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-154">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="b6a6b-155">Objetos do cofre de chaves e exclusão reversível</span><span class="sxs-lookup"><span data-stu-id="b6a6b-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="b6a6b-156">Para uma chave, "ContosoFirstKey", em um cofre de chaves chamado "ContosoVault" com a exclusão reversível habilitada, essa chave seria excluída da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="b6a6b-157">Com o cofre de chaves habilitado para exclusão reversível, uma chave excluída ainda aparece como excluída, exceto, quando você lista ou recupera explicitamente as chaves excluídas.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="b6a6b-158">A maioria das operações em uma chave no estado excluído falhará, exceto para listagem, recuperação ou limpeza de uma chave excluída.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-158">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="b6a6b-159">Por exemplo, para solicitar a listagem de chaves excluídas em um cofre de chaves, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="b6a6b-159">For example, to request to list deleted keys in a key vault, use the following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="b6a6b-160">Estado de transição</span><span class="sxs-lookup"><span data-stu-id="b6a6b-160">Transition state</span></span> 

<span data-ttu-id="b6a6b-161">Quando você exclui uma chave em um cofre de chaves com exclusão reversível habilitada, talvez demore alguns segundos para a transição ser concluída.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span></span> <span data-ttu-id="b6a6b-162">Durante esse estado de transição, pode parecer que a chave não esteja no estado ativo ou no estado excluído.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-162">During this transition state, it may appear that the key is not in the active state or the deleted state.</span></span> <span data-ttu-id="b6a6b-163">Esse comando listará todas as chaves excluídas em seu cofre de chaves chamado "ContosoVault".</span><span class="sxs-lookup"><span data-stu-id="b6a6b-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="b6a6b-164">Usar exclusão reversível com objetos de cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="b6a6b-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="b6a6b-165">Assim como os cofres de chave, uma chave, segredo ou certificado excluído permanecerá no estado excluído por até 90 dias, a menos que você o recupere ou limpe.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="b6a6b-166">simétricas</span><span class="sxs-lookup"><span data-stu-id="b6a6b-166">Keys</span></span>

<span data-ttu-id="b6a6b-167">Para recuperar uma chave excluída:</span><span class="sxs-lookup"><span data-stu-id="b6a6b-167">To recover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="b6a6b-168">Para excluir permanentemente uma chave:</span><span class="sxs-lookup"><span data-stu-id="b6a6b-168">To permanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="b6a6b-169">A limpeza de uma chave a excluirá permanentemente, ou seja, ela não poderá ser recuperada.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="b6a6b-170">As ações de **recuperação** e **limpeza** têm suas próprias permissões associadas em uma política de acesso de cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-170">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="b6a6b-171">Para que um usuário ou entidade de serviço possa executar uma ação de **recuperação** ou **limpeza**, ele precisa ter a permissão respectiva para esse objeto (chave ou segredo) na política de acesso de cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-171">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span></span> <span data-ttu-id="b6a6b-172">Por padrão, a permissão de **limpeza** não é adicionada à política de acesso de um cofre de chaves quando o atalho "todos" for usado para conceder todas as permissões a um usuário.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-172">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span></span> <span data-ttu-id="b6a6b-173">Você deve conceder explicitamente a permissão de **limpeza**.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="b6a6b-174">Por exemplo, o comando a seguir concede a permissão user@contoso.com para executar várias operações em chaves no *ContosoVault*, incluindo **limpar**.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-174">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="b6a6b-175">Definir uma política de acesso de cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="b6a6b-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="b6a6b-176">Se você tiver um cofre de chaves para o qual acabou de habilitar a exclusão reversível, talvez você não tenha as permissões de **recuperação** e **limpeza**.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="b6a6b-177">Segredos</span><span class="sxs-lookup"><span data-stu-id="b6a6b-177">Secrets</span></span>

<span data-ttu-id="b6a6b-178">Assim como as chaves, os segredos em um cofre de chaves são operados com seus próprios comandos.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="b6a6b-179">Veja a seguir os comandos para excluir, listar, recuperar e limpar os segredos.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-179">Following, are the commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="b6a6b-180">Excluir um segredo chamado SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="b6a6b-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="b6a6b-181">Listar todos os segredos excluídos em um cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="b6a6b-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="b6a6b-182">Recuperar um segredo no estado excluído:</span><span class="sxs-lookup"><span data-stu-id="b6a6b-182">Recover a secret in the deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="b6a6b-183">Limpar um segredo no estado excluído:</span><span class="sxs-lookup"><span data-stu-id="b6a6b-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="b6a6b-184">A limpeza de um segredo o excluirá permanentemente, ou seja, ele não poderá ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="b6a6b-185">Limpeza e cofres de chave</span><span class="sxs-lookup"><span data-stu-id="b6a6b-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="b6a6b-186">Objetos do cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="b6a6b-186">Key vault objects</span></span>

<span data-ttu-id="b6a6b-187">A limpeza de uma chave, segredo ou certificado o excluirá permanentemente, ou seja, não será possível recuperá-lo.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="b6a6b-188">O cofre de chaves que continha o objeto excluído permanecerá intacto, assim como todos os outros objetos no cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-188">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="b6a6b-189">Cofres de chave como contêineres</span><span class="sxs-lookup"><span data-stu-id="b6a6b-189">Key vaults as containers</span></span>
<span data-ttu-id="b6a6b-190">Quando um cofre de chaves é limpo, todo seu conteúdo, incluindo chaves, segredos e certificados, serão excluídos permanentemente.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="b6a6b-191">Para limpar um cofre de chaves, use o comando `az keyvault purge`.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-191">To purge a key vault, use the `az keyvault purge` command.</span></span> <span data-ttu-id="b6a6b-192">Você pode encontrar o local dos cofres de chave excluído de sua assinatura usando o comando `az keyvault list-deleted`.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-192">You can find the location your subscription's deleted key vaults using the command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="b6a6b-193">A limpeza de um cofre de chaves o excluirá permanentemente, ou seja, não será possível recuperá-lo.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="b6a6b-194">Permissões de limpeza necessárias</span><span class="sxs-lookup"><span data-stu-id="b6a6b-194">Purge permissions required</span></span>
- <span data-ttu-id="b6a6b-195">Para limpar um cofre de chaves excluído, de modo que o cofre e todo seu conteúdo seja removido permanentemente, o usuário precisa de permissão RBAC para executar uma operação *Microsoft.KeyVault/locations/deletedVaults/purge/action*.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-195">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="b6a6b-196">Para listar a chave excluída, o cofre de um usuário precisa de permissão RBAC para executar a permissão *Microsoft.KeyVault/deletedVaults/read*.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-196">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="b6a6b-197">Por padrão, somente um administrador de assinatura tem essas permissões.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="b6a6b-198">Limpeza agendada</span><span class="sxs-lookup"><span data-stu-id="b6a6b-198">Scheduled purge</span></span>

<span data-ttu-id="b6a6b-199">A listagem de seus objetos de cofre de chaves excluídos mostra o agendamento da limpeza pelo Key Vault.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-199">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span></span> <span data-ttu-id="b6a6b-200">O campo *Data de Limpeza Agendada* indica quando o objeto do cofre de chaves será excluído permanentemente se nenhuma ação for realizada.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-200">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="b6a6b-201">Por padrão, o período de retenção para um objeto do cofre de chaves excluído é de 90 dias.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-201">By default, the retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="b6a6b-202">Um objeto de cofre limpo, disparado pelo campo *Data de Limpeza Agendada*, será excluído permanentemente.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="b6a6b-203">Ele não é recuperável.</span><span class="sxs-lookup"><span data-stu-id="b6a6b-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="b6a6b-204">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="b6a6b-204">Other resources</span></span>

- <span data-ttu-id="b6a6b-205">Para obter uma visão geral do recurso de exclusão reversível do Key Vault, veja [Visão geral da exclusão reversível do Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="b6a6b-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="b6a6b-206">Para obter uma visão geral do uso do Azure Key Vault, veja [Introdução ao Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b6a6b-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

