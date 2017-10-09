---
ms.assetid: 
title: "Cofre de chave aaaAzure - como toouse flexível excluir CLI"
description: "Usar exemplos de caso de exclusão reversível com trechos de código da CLI"
author: BrucePerlerMS
manager: mbaldwin
ms.service: key-vault
ms.topic: article
ms.workload: identity
ms.date: 08/04/2017
ms.author: bruceper
ms.openlocfilehash: 672f5210ab119c244ca712f0bb80b653b50ea79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-key-vault-soft-delete-with-cli"></a><span data-ttu-id="1be3a-103">Como toouse Cofre de chaves soft-delete com a CLI</span><span class="sxs-lookup"><span data-stu-id="1be3a-103">How toouse Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="1be3a-104">O recurso de exclusão reversível do Azure Key Vault permite a recuperação de cofres e objetos de cofre excluídos.</span><span class="sxs-lookup"><span data-stu-id="1be3a-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="1be3a-105">Especificamente, os endereços de exclusão reversível Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="1be3a-105">Specifically, soft-delete addresses hello following scenarios:</span></span>

- <span data-ttu-id="1be3a-106">Suporte à exclusão reversível de cofres de chaves</span><span class="sxs-lookup"><span data-stu-id="1be3a-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="1be3a-107">Suporte à exclusão reversível de objetos do cofre de chaves, chaves, segredos e certificados</span><span class="sxs-lookup"><span data-stu-id="1be3a-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1be3a-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1be3a-108">Prerequisites</span></span>

- <span data-ttu-id="1be3a-109">CLI do Azure 2.0 – Se essa configuração não existir para o seu ambiente, veja [Gerenciar Key Vault usando a CLI 2.0](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="1be3a-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="1be3a-110">Para saber mais de referência específicas do Key Vault para CLI, veja [Referência de Key Vault da CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="1be3a-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="1be3a-111">Permissões necessárias</span><span class="sxs-lookup"><span data-stu-id="1be3a-111">Required permissions</span></span>

<span data-ttu-id="1be3a-112">As operações de Key Vault são gerenciadas separadamente por meio de permissões de RBAC (controle de acesso baseado em função) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1be3a-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="1be3a-113">Operação</span><span class="sxs-lookup"><span data-stu-id="1be3a-113">Operation</span></span> | <span data-ttu-id="1be3a-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="1be3a-114">Description</span></span> | <span data-ttu-id="1be3a-115">Permissão de usuário</span><span class="sxs-lookup"><span data-stu-id="1be3a-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="1be3a-116">Listar</span><span class="sxs-lookup"><span data-stu-id="1be3a-116">List</span></span>|<span data-ttu-id="1be3a-117">Lista os cofres de chaves excluídos.</span><span class="sxs-lookup"><span data-stu-id="1be3a-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="1be3a-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="1be3a-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="1be3a-119">Recuperar</span><span class="sxs-lookup"><span data-stu-id="1be3a-119">Recover</span></span>|<span data-ttu-id="1be3a-120">Recupera o cofre de chaves excluído.</span><span class="sxs-lookup"><span data-stu-id="1be3a-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="1be3a-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="1be3a-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="1be3a-122">Limpar</span><span class="sxs-lookup"><span data-stu-id="1be3a-122">Purge</span></span>|<span data-ttu-id="1be3a-123">Remove permanentemente um cofre de chaves excluído e todo o seu conteúdo.</span><span class="sxs-lookup"><span data-stu-id="1be3a-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="1be3a-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="1be3a-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="1be3a-125">Para saber mais sobre permissões e controle de acesso, veja [Proteger seu cofre de chaves](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="1be3a-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="1be3a-126">Habilitar a exclusão reversível</span><span class="sxs-lookup"><span data-stu-id="1be3a-126">Enabling soft-delete</span></span>

<span data-ttu-id="1be3a-127">toorecover capaz de toobe um cofre de chaves excluído ou objetos armazenados em uma chave de cofre, você deve primeiro habilitar a exclusão reversível para esse Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="1be3a-127">toobe able toorecover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="1be3a-128">Cofre de chaves existente</span><span class="sxs-lookup"><span data-stu-id="1be3a-128">Existing key vault</span></span>

<span data-ttu-id="1be3a-129">Para um cofre de chaves existente chamado ContosoVault, habilite a exclusão reversível da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="1be3a-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="1be3a-130">Atualmente é necessário Olá de gravação do toouse do Azure Resource Manager recursos manipulação toodirectly *enableSoftDelete* toohello de propriedade de recurso de Cofre de chave.</span><span class="sxs-lookup"><span data-stu-id="1be3a-130">Currently you need toouse Azure Resource Manager resource manipulation toodirectly write hello *enableSoftDelete* property toohello Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="1be3a-131">Novo cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="1be3a-131">New key vault</span></span>

<span data-ttu-id="1be3a-132">Habilitar exclusão reversível para um novo cofre de chave é feito no momento da criação, adicionando o sinalizador de exclusão reversível do hello tooyour criar o comando.</span><span class="sxs-lookup"><span data-stu-id="1be3a-132">Enabling soft-delete for a new key vault is done at creation time by adding hello soft-delete enable flag tooyour create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="1be3a-133">Verificar a habilitação da exclusão reversível</span><span class="sxs-lookup"><span data-stu-id="1be3a-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="1be3a-134">tooverify um cofre de chaves com exclusão reversível habilitada, Olá execução *Mostrar* de comando e procure hello "Flexível excluir ativado?"</span><span class="sxs-lookup"><span data-stu-id="1be3a-134">tooverify that a key vault has soft-delete enabled, run hello *show* command and look for hello 'Soft Delete Enabled?'</span></span> <span data-ttu-id="1be3a-135">e sua configuração, true ou false.</span><span class="sxs-lookup"><span data-stu-id="1be3a-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="1be3a-136">Excluir um cofre de chaves protegido por exclusão reversível</span><span class="sxs-lookup"><span data-stu-id="1be3a-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="1be3a-137">Olá comando toodelete (ou remover) um cofre de chaves permanece Olá mesmo, mas suas alterações de comportamento dependendo se você habilitou o soft-exclusão ou não.</span><span class="sxs-lookup"><span data-stu-id="1be3a-137">hello command toodelete (or remove) a key vault remains hello same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="1be3a-138">Se você executar o comando anterior de saudação para um cofre de chaves que não tenha habilitada a exclusão reversível, você excluirá permanentemente este cofre de chaves e todo o seu conteúdo sem opções de recuperação.</span><span class="sxs-lookup"><span data-stu-id="1be3a-138">If you run hello previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="1be3a-139">Como a exclusão reversível protege seus cofres de chaves</span><span class="sxs-lookup"><span data-stu-id="1be3a-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="1be3a-140">Com a exclusão reversível habilitada:</span><span class="sxs-lookup"><span data-stu-id="1be3a-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="1be3a-141">Quando um cofre de chaves é excluído, ele é removido do seu grupo de recursos e colocado em um espaço reservado que só é associado ao local de saudação onde ele foi criado.</span><span class="sxs-lookup"><span data-stu-id="1be3a-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with hello location where it was created.</span></span> 
- <span data-ttu-id="1be3a-142">Objetos em uma chave excluída cofre, como chaves, segredos e certificados, não estão acessíveis e continuar assim enquanto seu Cofre de chaves que contém está em estado de saudação excluído.</span><span class="sxs-lookup"><span data-stu-id="1be3a-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in hello deleted state.</span></span> 
- <span data-ttu-id="1be3a-143">Olá nome DNS um cofre de chaves em um estado excluído é preservado, portanto, não é possível criar um novo cofre de chave com o mesmo nome.</span><span class="sxs-lookup"><span data-stu-id="1be3a-143">hello DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="1be3a-144">Você pode exibir cofres de chave de estado excluído, associados à sua assinatura, usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="1be3a-144">You may view deleted state key vaults, associated with your subscription, using hello following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="1be3a-145">Olá *ID de recurso* Olá saída refere-se toohello original ID de recurso do cofre.</span><span class="sxs-lookup"><span data-stu-id="1be3a-145">hello *Resource ID* in hello output refers toohello original resource ID of this vault.</span></span> <span data-ttu-id="1be3a-146">Como este cofre de chaves está em um estado excluído, não há um recurso com essa ID de recurso.</span><span class="sxs-lookup"><span data-stu-id="1be3a-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="1be3a-147">Olá *Id* campo pode ser usado tooidentify Olá recurso recuperação ou limpeza.</span><span class="sxs-lookup"><span data-stu-id="1be3a-147">hello *Id* field can be used tooidentify hello resource when recovering, or purging.</span></span> <span data-ttu-id="1be3a-148">Olá *agendado limpar data* campo indica ao Cofre hello será excluído permanentemente (limpas) se nenhuma ação será tomada para este cofre excluído.</span><span class="sxs-lookup"><span data-stu-id="1be3a-148">hello *Scheduled Purge Date* field indicates when hello vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="1be3a-149">Olá Olá de toocalculate período, a utilização de retenção padrão *agendado limpar data*, é de 90 dias.</span><span class="sxs-lookup"><span data-stu-id="1be3a-149">hello default retention period, used toocalculate hello *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="1be3a-150">Recuperação de um cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="1be3a-150">Recovering a key vault</span></span>

<span data-ttu-id="1be3a-151">toorecover um cofre de chaves, que é necessário que o nome de Cofre de chaves do toospecify hello, grupo de recursos e local.</span><span class="sxs-lookup"><span data-stu-id="1be3a-151">toorecover a key vault, you need toospecify hello key vault name, resource group, and location.</span></span> <span data-ttu-id="1be3a-152">Observe Olá local e o grupo de recursos de saudação do Cofre de chaves Olá excluído conforme necessário para um processo de recuperação de chave de cofre.</span><span class="sxs-lookup"><span data-stu-id="1be3a-152">Note hello location and hello resource group of hello deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --name ContosoVault
```

<span data-ttu-id="1be3a-153">Quando um cofre de chaves é recuperado, o resultado de saudação é um novo recurso com ID de recurso original do cofre chave Olá</span><span class="sxs-lookup"><span data-stu-id="1be3a-153">When a key vault is recovered, hello result is a new resource with hello key vault's original resource ID.</span></span> <span data-ttu-id="1be3a-154">Se o grupo de recursos de saudação onde o Cofre de chaves Olá existia foi removido, um novo grupo de recursos com o mesmo nome deve criado antes de Cofre de chaves Olá pode ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="1be3a-154">If hello resource group where hello key vault existed has been removed, a new resource group with same name must be created before hello key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="1be3a-155">Objetos do cofre de chaves e exclusão reversível</span><span class="sxs-lookup"><span data-stu-id="1be3a-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="1be3a-156">Para uma chave, "ContosoFirstKey", em um cofre de chaves chamado "ContosoVault" com a exclusão reversível habilitada, essa chave seria excluída da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="1be3a-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="1be3a-157">Com o cofre de chaves habilitado para exclusão reversível, uma chave excluída ainda aparece como excluída, exceto, quando você lista ou recupera explicitamente as chaves excluídas.</span><span class="sxs-lookup"><span data-stu-id="1be3a-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="1be3a-158">A maioria das operações em uma chave em estado Olá excluído falhará, exceto listagem uma chave excluída, recuperando-la ou limpá-lo.</span><span class="sxs-lookup"><span data-stu-id="1be3a-158">Most operations on a key in hello deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="1be3a-159">Por exemplo, chaves do toorequest toolist excluída em um cofre de chaves, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1be3a-159">For example, toorequest toolist deleted keys in a key vault, use hello following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="1be3a-160">Estado de transição</span><span class="sxs-lookup"><span data-stu-id="1be3a-160">Transition state</span></span> 

<span data-ttu-id="1be3a-161">Quando você exclui uma chave em um cofre de chaves com exclusão reversível habilitada, pode levar alguns segundos para Olá transição toocomplete.</span><span class="sxs-lookup"><span data-stu-id="1be3a-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for hello transition toocomplete.</span></span> <span data-ttu-id="1be3a-162">Durante esse estado de transição, pode parecer que chave Olá não está no estado ativo hello ou Olá excluído.</span><span class="sxs-lookup"><span data-stu-id="1be3a-162">During this transition state, it may appear that hello key is not in hello active state or hello deleted state.</span></span> <span data-ttu-id="1be3a-163">Esse comando listará todas as chaves excluídas em seu cofre de chaves chamado "ContosoVault".</span><span class="sxs-lookup"><span data-stu-id="1be3a-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="1be3a-164">Usar exclusão reversível com objetos de cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="1be3a-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="1be3a-165">Apenas como chave cofres, uma chave excluída, segredo ou certificado permanecerá no estado excluído para backup too90 dias, a menos que recuperá-la ou limpá-lo.</span><span class="sxs-lookup"><span data-stu-id="1be3a-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up too90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="1be3a-166">simétricas</span><span class="sxs-lookup"><span data-stu-id="1be3a-166">Keys</span></span>

<span data-ttu-id="1be3a-167">toorecover uma chave excluída:</span><span class="sxs-lookup"><span data-stu-id="1be3a-167">toorecover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="1be3a-168">toopermanently excluir uma chave:</span><span class="sxs-lookup"><span data-stu-id="1be3a-168">toopermanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="1be3a-169">A limpeza de uma chave a excluirá permanentemente, ou seja, ela não poderá ser recuperada.</span><span class="sxs-lookup"><span data-stu-id="1be3a-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="1be3a-170">Olá **recuperar** e **limpar** ações têm suas próprias permissões associadas em uma política de acesso do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="1be3a-170">hello **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="1be3a-171">Para um tooexecute capaz de toobe principal do usuário ou serviço um **recuperar** ou **limpar** ação deve tiverem a permissão respectivos Olá para esse objeto (chave ou segredo) na política de acesso do Cofre de chaves de saudação.</span><span class="sxs-lookup"><span data-stu-id="1be3a-171">For a user or service principal toobe able tooexecute a **recover** or **purge** action they must have hello respective permission for that object (key or secret) in hello key vault access policy.</span></span> <span data-ttu-id="1be3a-172">Por padrão, Olá **limpar** permissão quando não é adicionada a política de acesso do cofre chave tooa atalho 'todos' hello é usado toogrant todas as permissões do usuário tooa.</span><span class="sxs-lookup"><span data-stu-id="1be3a-172">By default, hello **purge** permission is not added tooa key vault's access policy when hello 'all' shortcut is used toogrant all permissions tooa user.</span></span> <span data-ttu-id="1be3a-173">Você deve conceder explicitamente a permissão de **limpeza**.</span><span class="sxs-lookup"><span data-stu-id="1be3a-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="1be3a-174">Por exemplo, Olá concessões de comando a seguir user@contoso.com tooperform permissão várias operações nas chaves *ContosoVault* incluindo **limpar**.</span><span class="sxs-lookup"><span data-stu-id="1be3a-174">For example, hello following command grants user@contoso.com permission tooperform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="1be3a-175">Definir uma política de acesso de cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="1be3a-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="1be3a-176">Se você tiver um cofre de chaves para o qual acabou de habilitar a exclusão reversível, talvez você não tenha as permissões de **recuperação** e **limpeza**.</span><span class="sxs-lookup"><span data-stu-id="1be3a-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="1be3a-177">Segredos</span><span class="sxs-lookup"><span data-stu-id="1be3a-177">Secrets</span></span>

<span data-ttu-id="1be3a-178">Assim como as chaves, os segredos em um cofre de chaves são operados com seus próprios comandos.</span><span class="sxs-lookup"><span data-stu-id="1be3a-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="1be3a-179">A seguir, são comandos de saudação para excluir, listar, recuperação e limpeza segredos.</span><span class="sxs-lookup"><span data-stu-id="1be3a-179">Following, are hello commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="1be3a-180">Excluir um segredo chamado SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="1be3a-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="1be3a-181">Listar todos os segredos excluídos em um cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="1be3a-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="1be3a-182">Recupere um segredo no estado Olá excluído:</span><span class="sxs-lookup"><span data-stu-id="1be3a-182">Recover a secret in hello deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="1be3a-183">Limpar um segredo no estado excluído:</span><span class="sxs-lookup"><span data-stu-id="1be3a-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="1be3a-184">A limpeza de um segredo o excluirá permanentemente, ou seja, ele não poderá ser recuperado.</span><span class="sxs-lookup"><span data-stu-id="1be3a-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="1be3a-185">Limpeza e cofres de chave</span><span class="sxs-lookup"><span data-stu-id="1be3a-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="1be3a-186">Objetos do cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="1be3a-186">Key vault objects</span></span>

<span data-ttu-id="1be3a-187">A limpeza de uma chave, segredo ou certificado o excluirá permanentemente, ou seja, não será possível recuperá-lo.</span><span class="sxs-lookup"><span data-stu-id="1be3a-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="1be3a-188">Cofre de chaves de saudação que continha Olá excluído objeto porém permanecerão intacto assim como todos os outros objetos no cofre de chaves hello.</span><span class="sxs-lookup"><span data-stu-id="1be3a-188">hello key vault that contained hello deleted object will however remain intact as will all other objects in hello key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="1be3a-189">Cofres de chave como contêineres</span><span class="sxs-lookup"><span data-stu-id="1be3a-189">Key vaults as containers</span></span>
<span data-ttu-id="1be3a-190">Quando um cofre de chaves é limpo, todo seu conteúdo, incluindo chaves, segredos e certificados, serão excluídos permanentemente.</span><span class="sxs-lookup"><span data-stu-id="1be3a-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="1be3a-191">toopurge um cofre de chaves, use Olá `az keyvault purge` comando.</span><span class="sxs-lookup"><span data-stu-id="1be3a-191">toopurge a key vault, use hello `az keyvault purge` command.</span></span> <span data-ttu-id="1be3a-192">Você pode encontrar local Olá cofres chave excluído da assinatura usando o comando Olá `az keyvault list-deleted`.</span><span class="sxs-lookup"><span data-stu-id="1be3a-192">You can find hello location your subscription's deleted key vaults using hello command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="1be3a-193">A limpeza de um cofre de chaves o excluirá permanentemente, ou seja, não será possível recuperá-lo.</span><span class="sxs-lookup"><span data-stu-id="1be3a-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="1be3a-194">Permissões de limpeza necessárias</span><span class="sxs-lookup"><span data-stu-id="1be3a-194">Purge permissions required</span></span>
- <span data-ttu-id="1be3a-195">toopurge um cofre de chaves excluído, por exemplo, que cofre hello e todo seu conteúdo será removido permanentemente, Olá usuário precisa de RBAC permissão tooperform um *Microsoft.KeyVault/locations/deletedVaults/purge/action* operação.</span><span class="sxs-lookup"><span data-stu-id="1be3a-195">toopurge a deleted key vault, such that hello vault and all its contents are permanently removed, hello user needs RBAC permission tooperform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="1be3a-196">chave de saudação excluída toolist cofre Olá um usuário precisa RBAC permissão tooperform *Microsoft.KeyVault/deletedVaults/read* permissão.</span><span class="sxs-lookup"><span data-stu-id="1be3a-196">toolist hello deleted key, hello vault a user needs RBAC permission tooperform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="1be3a-197">Por padrão, somente um administrador de assinatura tem essas permissões.</span><span class="sxs-lookup"><span data-stu-id="1be3a-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="1be3a-198">Limpeza agendada</span><span class="sxs-lookup"><span data-stu-id="1be3a-198">Scheduled purge</span></span>

<span data-ttu-id="1be3a-199">Listar os objetos excluídos de Cofre de chaves mostra quando eles são toobe schedled limpo pelo Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="1be3a-199">Listing your deleted key vault objects shows when they are schedled toobe purged by Key Vault.</span></span> <span data-ttu-id="1be3a-200">Olá *agendado limpar data* campo indica quando um objeto de Cofre de chaves será excluído permanentemente, se nenhuma ação será tomada.</span><span class="sxs-lookup"><span data-stu-id="1be3a-200">hello *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="1be3a-201">Por padrão, o período de retenção de saudação para um objeto excluído cofre da chave é de 90 dias.</span><span class="sxs-lookup"><span data-stu-id="1be3a-201">By default, hello retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="1be3a-202">Um objeto de cofre limpo, disparado pelo campo *Data de Limpeza Agendada*, será excluído permanentemente.</span><span class="sxs-lookup"><span data-stu-id="1be3a-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="1be3a-203">Ele não é recuperável.</span><span class="sxs-lookup"><span data-stu-id="1be3a-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="1be3a-204">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="1be3a-204">Other resources</span></span>

- <span data-ttu-id="1be3a-205">Para obter uma visão geral do recurso de exclusão reversível do Key Vault, veja [Visão geral da exclusão reversível do Azure Key Vault](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="1be3a-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="1be3a-206">Para obter uma visão geral do uso do Azure Key Vault, veja [Introdução ao Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1be3a-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

