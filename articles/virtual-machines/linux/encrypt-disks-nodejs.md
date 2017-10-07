---
title: aaaEncrypt discos em uma VM do Linux com hello 1.0 da CLI do Azure | Microsoft Docs
description: "Como tooencrypt discos em uma VM do Linux usando hello Azure CLI 1.0 e o modelo de implantação do Gerenciador de recursos de saudação"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/06/2017
ms.author: iainfou
ms.openlocfilehash: 68a0394d366c3c6941e2c6db0d4263123f951946
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-disks-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="68dc5-103">Criptografar discos em uma VM do Linux usando Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="68dc5-103">Encrypt disks on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="68dc5-104">Para conformidade e segurança aprimorados da máquina virtual (VM), os discos virtuais no Azure podem ser criptografados em repouso.</span><span class="sxs-lookup"><span data-stu-id="68dc5-104">For enhanced virtual machine (VM) security and compliance, virtual disks in Azure can be encrypted at rest.</span></span> <span data-ttu-id="68dc5-105">Discos são criptografados usando chaves criptográficas que são protegidas em um Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="68dc5-105">Disks are encrypted using cryptographic keys that are secured in an Azure Key Vault.</span></span> <span data-ttu-id="68dc5-106">Você controla essas chaves criptográficas e pode auditar seu uso.</span><span class="sxs-lookup"><span data-stu-id="68dc5-106">You control these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="68dc5-107">Este artigo fornece detalhes sobre como tooencrypt de discos virtuais em uma VM do Linux usando hello Azure CLI 1.0 e o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="68dc5-107">This article details how tooencrypt virtual disks on a Linux VM using hello Azure CLI 1.0 and hello Resource Manager deployment model.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="68dc5-108">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="68dc5-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="68dc5-109">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="68dc5-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="68dc5-110">[1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="68dc5-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="68dc5-111">[2.0 do CLI do Azure](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="68dc5-111">[Azure CLI 2.0](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-commands"></a><span data-ttu-id="68dc5-112">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="68dc5-112">Quick commands</span></span>
<span data-ttu-id="68dc5-113">Se você precisar tooquickly realizar tarefa hello, Olá Olá de detalhes da seção base a seguir comandos tooencrypt de discos virtuais na sua VM.</span><span class="sxs-lookup"><span data-stu-id="68dc5-113">If you need tooquickly accomplish hello task, hello following section details hello base commands tooencrypt virtual disks on your VM.</span></span> <span data-ttu-id="68dc5-114">Obter mais informações e o contexto para cada etapa pode ser encontrada restante de saudação do documento hello, [Iniciar aqui](#overview-of-disk-encryption).</span><span class="sxs-lookup"><span data-stu-id="68dc5-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](#overview-of-disk-encryption).</span></span>

<span data-ttu-id="68dc5-115">Você precisa Olá [1.0 mais recente de CLI do Azure](../../xplat-cli-install.md) instalado e registrado usando o modo do Gerenciador de recursos de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68dc5-115">You need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="68dc5-116">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="68dc5-116">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="68dc5-117">Os nomes de parâmetro de exemplo incluem `myResourceGroup`, `myKeyVault` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="68dc5-117">Example parameter names include `myResourceGroup`, `myKeyVault`, and `myVM`.</span></span>

<span data-ttu-id="68dc5-118">Primeiro, habilitar o provedor do Azure Key Vault hello dentro de sua assinatura do Azure e criar um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="68dc5-118">First, enable hello Azure Key Vault provider within your Azure subscription and create a resource group.</span></span> <span data-ttu-id="68dc5-119">Olá, exemplo a seguir cria um nome de grupo de recursos `myResourceGroup` em Olá `WestUS` local:</span><span class="sxs-lookup"><span data-stu-id="68dc5-119">hello following example creates a resource group name `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="68dc5-120">Crie um Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="68dc5-120">Create an Azure Key Vault.</span></span> <span data-ttu-id="68dc5-121">Olá, exemplo a seguir cria um cofre de chaves denominado `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="68dc5-121">hello following example creates a Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="68dc5-122">Crie uma chave de criptografia em seu Cofre de chaves e habilite-a para criptografia de disco.</span><span class="sxs-lookup"><span data-stu-id="68dc5-122">Create a cryptographic key in your Key Vault and enable it for disk encryption.</span></span> <span data-ttu-id="68dc5-123">Olá, exemplo a seguir cria uma chave chamada `myKey`:</span><span class="sxs-lookup"><span data-stu-id="68dc5-123">hello following example creates a key named `myKey`:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```

<span data-ttu-id="68dc5-124">Crie um ponto de extremidade usando o Active Directory do Azure para manipular a autenticação hello e troca de chaves de criptografia do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="68dc5-124">Create an endpoint using Azure Active Directory for handling hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="68dc5-125">Olá `--home-page` e `--identifier-uris` não é necessário toobe real endereço roteável.</span><span class="sxs-lookup"><span data-stu-id="68dc5-125">hello `--home-page` and `--identifier-uris` do not need toobe actual routable address.</span></span> <span data-ttu-id="68dc5-126">Para mais alto nível de segurança hello, segredos de cliente devem ser usados em vez de senhas.</span><span class="sxs-lookup"><span data-stu-id="68dc5-126">For hello highest level of security, client secrets should be used instead of passwords.</span></span> <span data-ttu-id="68dc5-127">Olá CLI do Azure atualmente não é possível gerar segredos de cliente.</span><span class="sxs-lookup"><span data-stu-id="68dc5-127">hello Azure CLI cannot currently generate client secrets.</span></span> <span data-ttu-id="68dc5-128">Segredos de cliente só podem ser gerados no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="68dc5-128">Client secrets can only be generated in hello Azure portal.</span></span> <span data-ttu-id="68dc5-129">Olá, exemplo a seguir cria um ponto de extremidade do Azure Active Directory denominado `myAADApp` e usa uma senha de `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="68dc5-129">hello following example creates an Azure Active Directory endpoint named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="68dc5-130">Especifique sua própria senha da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68dc5-130">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="68dc5-131">Saudação de Observação `applicationId` mostrado na saída de saudação da saudação precede o comando.</span><span class="sxs-lookup"><span data-stu-id="68dc5-131">Note hello `applicationId` shown in hello output from hello preceding command.</span></span> <span data-ttu-id="68dc5-132">Essa ID de aplicativo é usado em Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="68dc5-132">This application ID is used in hello following steps:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```

<span data-ttu-id="68dc5-133">Adicione um tooan de disco de dados existente de VM.</span><span class="sxs-lookup"><span data-stu-id="68dc5-133">Add a data disk tooan existing VM.</span></span> <span data-ttu-id="68dc5-134">Olá, exemplo a seguir adiciona um disco de dados tooa VM denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="68dc5-134">hello following example adds a data disk tooa VM named `myVM`:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="68dc5-135">Examine os detalhes de saudação para sua chave de Cofre de chaves e hello que você criou.</span><span class="sxs-lookup"><span data-stu-id="68dc5-135">Review hello details for your Key Vault and hello key you created.</span></span> <span data-ttu-id="68dc5-136">Você precisa Olá chave, ID de Cofre de chave e URI URL na etapa final hello.</span><span class="sxs-lookup"><span data-stu-id="68dc5-136">You need hello Key Vault ID, URI, and key URL in hello final step.</span></span> <span data-ttu-id="68dc5-137">Olá exemplo a seguir examina Olá detalhes para um cofre de chaves denominado `myKeyVault` e a chave denominada `myKey`:</span><span class="sxs-lookup"><span data-stu-id="68dc5-137">hello following example reviews hello details for a Key Vault named `myKeyVault` and key named `myKey`:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="68dc5-138">Criptografe seus discos da seguinte maneira, digitando seus próprios nomes de parâmetro completamente:</span><span class="sxs-lookup"><span data-stu-id="68dc5-138">Encrypt your disks as follows, entering your own parameter names throughout:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="68dc5-139">Olá CLI do Azure não fornece detalhados erros durante o processo de criptografia hello.</span><span class="sxs-lookup"><span data-stu-id="68dc5-139">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="68dc5-140">Para obter informações adicionais de solução de problemas, examine `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span><span class="sxs-lookup"><span data-stu-id="68dc5-140">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log`.</span></span> <span data-ttu-id="68dc5-141">Como Olá precede o comando tem muitas variáveis e talvez não obtenha muito indicação como toowhy Olá processo falhar, um exemplo completo de comandos seria o seguinte:</span><span class="sxs-lookup"><span data-stu-id="68dc5-141">As hello preceding command has many variables and you may not get much indication as toowhy hello process fails, a complete command example would be as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="68dc5-142">Por fim, examine o status da criptografia Olá novamente tooconfirm que os discos virtuais agora foram criptografados.</span><span class="sxs-lookup"><span data-stu-id="68dc5-142">Finally, review hello encryption status again tooconfirm that your virtual disks have now been encrypted.</span></span> <span data-ttu-id="68dc5-143">Olá, exemplo a seguir verifica o status de saudação de uma VM denominada `myVM` em Olá `myResourceGroup` grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="68dc5-143">hello following example checks hello status of a VM named `myVM` in hello `myResourceGroup` resource group:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```

## <a name="overview-of-disk-encryption"></a><span data-ttu-id="68dc5-144">Visão geral da criptografia de disco</span><span class="sxs-lookup"><span data-stu-id="68dc5-144">Overview of disk encryption</span></span>
<span data-ttu-id="68dc5-145">Discos virtuais em VMs do Linux são criptografados em repouso usando [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span><span class="sxs-lookup"><span data-stu-id="68dc5-145">Virtual disks on Linux VMs are encrypted at rest using [dm-crypt](https://wikipedia.org/wiki/Dm-crypt).</span></span> <span data-ttu-id="68dc5-146">Não há nenhuma taxa para criptografar discos virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="68dc5-146">There is no charge for encrypting virtual disks in Azure.</span></span> <span data-ttu-id="68dc5-147">As chaves de criptografia são armazenadas no cofre de chaves do Azure usando a proteção de software, ou você pode importar ou gerar as chaves em módulos de segurança de Hardware (HSM) certificada tooFIPS padrões do 140-2 nível 2.</span><span class="sxs-lookup"><span data-stu-id="68dc5-147">Cryptographic keys are stored in Azure Key Vault using software-protection, or you can import or generate your keys in Hardware Security Modules (HSMs) certified tooFIPS 140-2 level 2 standards.</span></span> <span data-ttu-id="68dc5-148">Você mantém o controle dessas chaves criptográficas e pode auditar seu uso.</span><span class="sxs-lookup"><span data-stu-id="68dc5-148">You retain control of these cryptographic keys and can audit their use.</span></span> <span data-ttu-id="68dc5-149">Essas chaves de criptografia são usada tooencrypt e descriptografar os discos virtuais anexados tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="68dc5-149">These cryptographic keys are used tooencrypt and decrypt virtual disks attached tooyour VM.</span></span> <span data-ttu-id="68dc5-150">Um ponto de extremidade do Azure Active Directory fornece um mecanismo seguro para emitir essas chaves criptográficas, enquanto as VMs são ligadas e desligadas.</span><span class="sxs-lookup"><span data-stu-id="68dc5-150">An Azure Active Directory endpoint provides a secure mechanism for issuing these cryptographic keys as VMs are powered on and off.</span></span>

<span data-ttu-id="68dc5-151">processo de saudação de criptografia de uma VM é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="68dc5-151">hello process for encrypting a VM is as follows:</span></span>

1. <span data-ttu-id="68dc5-152">Crie uma chave de criptografia em um Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="68dc5-152">Create a cryptographic key in an Azure Key Vault.</span></span>
2. <span data-ttu-id="68dc5-153">Configure Olá criptográfico chave toobe pode ser usado para criptografia de discos.</span><span class="sxs-lookup"><span data-stu-id="68dc5-153">Configure hello cryptographic key toobe usable for encrypting disks.</span></span>
3. <span data-ttu-id="68dc5-154">chave de criptografia de saudação tooread de saudação Cofre de chaves do Azure, crie um ponto de extremidade usando o Azure Active Directory com as permissões adequadas hello.</span><span class="sxs-lookup"><span data-stu-id="68dc5-154">tooread hello cryptographic key from hello Azure Key Vault, create an endpoint using Azure Active Directory with hello appropriate permissions.</span></span>
4. <span data-ttu-id="68dc5-155">Emita Olá comando tooencrypt seus discos virtuais, especificando o ponto de extremidade do hello Active Directory do Azure e adequado toobe chave criptográfica usada.</span><span class="sxs-lookup"><span data-stu-id="68dc5-155">Issue hello command tooencrypt your virtual disks, specifying hello Azure Active Directory endpoint and appropriate cryptographic key toobe used.</span></span>
5. <span data-ttu-id="68dc5-156">o ponto de extremidade do Hello Active Directory do Azure solicita chave de criptografia necessária saudação do Cofre de chaves do Azure.</span><span class="sxs-lookup"><span data-stu-id="68dc5-156">hello Azure Active Directory endpoint requests hello required cryptographic key from Azure Key Vault.</span></span>
6. <span data-ttu-id="68dc5-157">discos virtuais Olá são criptografados usando a chave criptográfica Olá fornecido.</span><span class="sxs-lookup"><span data-stu-id="68dc5-157">hello virtual disks are encrypted using hello provided cryptographic key.</span></span>

## <a name="supporting-services-and-encryption-process"></a><span data-ttu-id="68dc5-158">Suporte a serviços e processo de criptografia</span><span class="sxs-lookup"><span data-stu-id="68dc5-158">Supporting services and encryption process</span></span>
<span data-ttu-id="68dc5-159">Criptografia de disco se baseia em Olá componentes adicionais a seguir:</span><span class="sxs-lookup"><span data-stu-id="68dc5-159">Disk encryption relies on hello following additional components:</span></span>

* <span data-ttu-id="68dc5-160">**Cofre de chaves do Azure** -usado toosafeguard as chaves de criptografia e segredos usados no processo de criptografia/descriptografia de disco hello.</span><span class="sxs-lookup"><span data-stu-id="68dc5-160">**Azure Key Vault** - used toosafeguard cryptographic keys and secrets used for hello disk encryption/decryption process.</span></span>
  * <span data-ttu-id="68dc5-161">Se houver um, você pode usar um Cofre de Chaves do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="68dc5-161">If one exists, you can use an existing Azure Key Vault.</span></span> <span data-ttu-id="68dc5-162">Você não tem toodedicate discos tooencrypting um cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="68dc5-162">You do not have toodedicate a Key Vault tooencrypting disks.</span></span>
  * <span data-ttu-id="68dc5-163">limites administrativos tooseparate e visibilidade de chave, você pode criar um cofre de chaves dedicado.</span><span class="sxs-lookup"><span data-stu-id="68dc5-163">tooseparate administrative boundaries and key visibility, you can create a dedicated Key Vault.</span></span>
* <span data-ttu-id="68dc5-164">**Active Directory do Azure** - identificadores Olá troca segura de chaves de criptografia necessárias e autenticação para ações de solicitada.</span><span class="sxs-lookup"><span data-stu-id="68dc5-164">**Azure Active Directory** - handles hello secure exchanging of required cryptographic keys and authentication for requested actions.</span></span>
  * <span data-ttu-id="68dc5-165">Normalmente, você pode usar uma instância existente do Azure Active Directory para hospedar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="68dc5-165">You can typically use an existing Azure Active Directory instance for housing your application.</span></span>
  * <span data-ttu-id="68dc5-166">aplicativo Hello é mais de um ponto de extremidade para Olá Cofre de chaves e toorequest de serviços de máquina Virtual e obter emitido chaves de criptografia apropriadas hello.</span><span class="sxs-lookup"><span data-stu-id="68dc5-166">hello application is more of an endpoint for hello Key Vault and Virtual Machine services toorequest and get issued hello appropriate cryptographic keys.</span></span> <span data-ttu-id="68dc5-167">Você não está desenvolvendo um aplicativo real que se integra ao Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="68dc5-167">You are not developing an actual application that integrates with Azure Active Directory.</span></span>

## <a name="requirements-and-limitations"></a><span data-ttu-id="68dc5-168">Requisitos e limitações</span><span class="sxs-lookup"><span data-stu-id="68dc5-168">Requirements and limitations</span></span>
<span data-ttu-id="68dc5-169">Requisitos e cenários com suporte para criptografia de disco:</span><span class="sxs-lookup"><span data-stu-id="68dc5-169">Supported scenarios and requirements for disk encryption:</span></span>

* <span data-ttu-id="68dc5-170">saudação do servidor Linux SKUs - Red Hat Enterprise Linux, CentOS, SUSE e SUSE Linux Enterprise Server (SLES) e Ubuntu a seguir.</span><span class="sxs-lookup"><span data-stu-id="68dc5-170">hello following Linux server SKUs - Ubuntu, CentOS, SUSE and SUSE Linux Enterprise Server (SLES), and Red Hat Enterprise Linux.</span></span>
* <span data-ttu-id="68dc5-171">Todos os recursos (como o Cofre de chaves, a conta de armazenamento e VM) devem estar no hello mesma região do Azure e assinatura.</span><span class="sxs-lookup"><span data-stu-id="68dc5-171">All resources (such as Key Vault, Storage account, and VM) must be in hello same Azure region and subscription.</span></span>
* <span data-ttu-id="68dc5-172">VMs Standard das séries A, D, DS, G e GS.</span><span class="sxs-lookup"><span data-stu-id="68dc5-172">Standard A, D, DS, G, and GS series VMs.</span></span>

<span data-ttu-id="68dc5-173">Criptografia de disco não é suportada em Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="68dc5-173">Disk encryption is not currently supported in hello following scenarios:</span></span>

* <span data-ttu-id="68dc5-174">VMs de camada básica.</span><span class="sxs-lookup"><span data-stu-id="68dc5-174">Basic tier VMs.</span></span>
* <span data-ttu-id="68dc5-175">Máquinas virtuais criadas usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="68dc5-175">VMs created using hello Classic deployment model.</span></span>
* <span data-ttu-id="68dc5-176">Desabilitação da criptografia de disco do OS em VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="68dc5-176">Disabling OS disk encryption on Linux VMs.</span></span>
* <span data-ttu-id="68dc5-177">Atualizando chaves de criptografia de saudação em uma VM Linux já criptografados.</span><span class="sxs-lookup"><span data-stu-id="68dc5-177">Updating hello cryptographic keys on an already encrypted Linux VM.</span></span>

## <a name="create-hello-azure-key-vault-and-keys"></a><span data-ttu-id="68dc5-178">Criar hello Azure Key Vault e chaves</span><span class="sxs-lookup"><span data-stu-id="68dc5-178">Create hello Azure Key Vault and keys</span></span>
<span data-ttu-id="68dc5-179">toocomplete Olá restante deste guia, você precisa Olá [mais recente do Azure CLI 1.0](../../xplat-cli-install.md) instalado e registrado usando o modo do Gerenciador de recursos de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68dc5-179">toocomplete hello remainder of this guide, you need hello [latest Azure CLI 1.0](../../xplat-cli-install.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="68dc5-180">Ao longo de exemplos de comando hello, substitua todos os parâmetros de exemplo com seus próprios nomes, o local e valores de chave.</span><span class="sxs-lookup"><span data-stu-id="68dc5-180">Throughout hello command examples, replace all example parameters with your own names, location, and key values.</span></span> <span data-ttu-id="68dc5-181">Olá, exemplos a seguir usam uma convenção de `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span><span class="sxs-lookup"><span data-stu-id="68dc5-181">hello following examples use a convention of `myResourceGroup`, `myKeyVault`, `myAADApp`, etc.</span></span>

<span data-ttu-id="68dc5-182">primeira etapa de saudação é toocreate toostore um cofre de chaves do Azure as chaves criptográficas.</span><span class="sxs-lookup"><span data-stu-id="68dc5-182">hello first step is toocreate an Azure Key Vault toostore your cryptographic keys.</span></span> <span data-ttu-id="68dc5-183">Cofre de chaves do Azure pode armazenar segredos, chaves ou senhas que permitem que você toosecurely implementação-las em seus aplicativos e serviços.</span><span class="sxs-lookup"><span data-stu-id="68dc5-183">Azure Key Vault can store keys, secrets, or passwords that allow you toosecurely implement them in your applications and services.</span></span> <span data-ttu-id="68dc5-184">Para criptografia de disco virtual, use o Cofre de chaves toostore uma chave criptográfica que é usada tooencrypt ou descriptografar os discos virtuais.</span><span class="sxs-lookup"><span data-stu-id="68dc5-184">For virtual disk encryption, you use Key Vault toostore a cryptographic key that is used tooencrypt or decrypt your virtual disks.</span></span>

<span data-ttu-id="68dc5-185">Habilitar hello Azure Key Vault provedor na sua assinatura do Azure, em seguida, criar um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="68dc5-185">Enable hello Azure Key Vault provider in your Azure subscription, then create a resource group.</span></span> <span data-ttu-id="68dc5-186">Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `WestUS` local:</span><span class="sxs-lookup"><span data-stu-id="68dc5-186">hello following example creates a resource group named `myResourceGroup` in hello `WestUS` location:</span></span>

```azurecli
azure provider register Microsoft.KeyVault
azure group create myResourceGroup --location WestUS
```

<span data-ttu-id="68dc5-187">Hello Azure Key Vault contendo Olá chaves criptográficas e computação associada recursos, como armazenamento e hello própria máquina virtual devem residir no hello mesma região.</span><span class="sxs-lookup"><span data-stu-id="68dc5-187">hello Azure Key Vault containing hello cryptographic keys and associated compute resources such as storage and hello VM itself must reside in hello same region.</span></span> <span data-ttu-id="68dc5-188">Olá, exemplo a seguir cria um cofre de chaves do Azure denominado `myKeyVault`:</span><span class="sxs-lookup"><span data-stu-id="68dc5-188">hello following example creates an Azure Key Vault named `myKeyVault`:</span></span>

```azurecli
azure keyvault create --vault-name myKeyVault --resource-group myResourceGroup \
  --location WestUS
```

<span data-ttu-id="68dc5-189">É possível armazenar chaves de criptografia usando a proteção do Modelo de segurança de Hardware (HSM) ou software.</span><span class="sxs-lookup"><span data-stu-id="68dc5-189">You can store cryptographic keys using software or Hardware Security Model (HSM) protection.</span></span> <span data-ttu-id="68dc5-190">Usar um HSM requer um Cofre de Chaves premium.</span><span class="sxs-lookup"><span data-stu-id="68dc5-190">Using an HSM requires a premium Key Vault.</span></span> <span data-ttu-id="68dc5-191">Há um custo adicional toocreating um premium Cofre de chaves em vez de Cofre de chave padrão que armazena as chaves protegidas por software.</span><span class="sxs-lookup"><span data-stu-id="68dc5-191">There is an additional cost toocreating a premium Key Vault rather than standard Key Vault that stores software-protected keys.</span></span> <span data-ttu-id="68dc5-192">toocreate adicionar um cofre de chaves, premium em Olá anterior etapa `--sku Premium` toohello comando.</span><span class="sxs-lookup"><span data-stu-id="68dc5-192">toocreate a premium Key Vault, in hello preceding step add `--sku Premium` toohello command.</span></span> <span data-ttu-id="68dc5-193">Olá exemplo a seguir usa chaves protegidas por software pois criamos um cofre de chaves padrão.</span><span class="sxs-lookup"><span data-stu-id="68dc5-193">hello following example uses software-protected keys since we created a standard Key Vault.</span></span>

<span data-ttu-id="68dc5-194">Para ambos os modelos de proteção, Olá plataforma Windows Azure precisa toobe concedida chaves de criptografia de saudação do acesso toorequest quando Olá VM inicializa os discos virtuais toodecrypt hello.</span><span class="sxs-lookup"><span data-stu-id="68dc5-194">For both protection models, hello Azure platform needs toobe granted access toorequest hello cryptographic keys when hello VM boots toodecrypt hello virtual disks.</span></span> <span data-ttu-id="68dc5-195">Crie uma chave de criptografia dentro de seu Cofre de Chaves e habilite-a para uso com criptografia de disco virtual.</span><span class="sxs-lookup"><span data-stu-id="68dc5-195">Create an encryption key within your Key Vault, then enable it for use with virtual disk encryption.</span></span> <span data-ttu-id="68dc5-196">Olá, exemplo a seguir cria uma chave chamada `myKey` e, em seguida, permite que ele para criptografia de disco:</span><span class="sxs-lookup"><span data-stu-id="68dc5-196">hello following example creates a key named `myKey` and then enables it for disk encryption:</span></span>

```azurecli
azure keyvault key create --vault-name myKeyVault --key-name myKey \
  --destination software
azure keyvault set-policy --vault-name myKeyVault --resource-group myResourceGroup \
  --enabled-for-disk-encryption true
```


## <a name="create-hello-azure-active-directory-application"></a><span data-ttu-id="68dc5-197">Criar o aplicativo do Active Directory do Azure hello</span><span class="sxs-lookup"><span data-stu-id="68dc5-197">Create hello Azure Active Directory application</span></span>
<span data-ttu-id="68dc5-198">Quando discos virtuais são criptografados ou descriptografados, você deve usar um ponto de extremidade toohandle Olá de autenticação e troca de chaves de criptografia do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="68dc5-198">When virtual disks are encrypted or decrypted, you use an endpoint toohandle hello authentication and exchanging of cryptographic keys from Key Vault.</span></span> <span data-ttu-id="68dc5-199">Esse ponto de extremidade, um aplicativo do Active Directory do Azure, permite Olá plataforma Windows Azure toorequest chaves de criptografia apropriado Olá em nome hello VM.</span><span class="sxs-lookup"><span data-stu-id="68dc5-199">This endpoint, an Azure Active Directory application, allows hello Azure platform toorequest hello appropriate cryptographic keys on behalf of hello VM.</span></span> <span data-ttu-id="68dc5-200">Uma instância do Azure Active Directory padrão está disponível em sua assinatura, embora muitas organizações tenham diretórios do Azure Active Directory dedicados.</span><span class="sxs-lookup"><span data-stu-id="68dc5-200">A default Azure Active Directory instance is available in your subscription, though many organizations have dedicated Azure Active Directory directories.</span></span>

<span data-ttu-id="68dc5-201">Como você não estiver criando um aplicativo completo do Active Directory do Azure, Olá `--home-page` e `--identifier-uris` parâmetros no exemplo a seguir de saudação não precisarem toobe real endereço roteável.</span><span class="sxs-lookup"><span data-stu-id="68dc5-201">As you are not creating a full Azure Active Directory application, hello `--home-page` and `--identifier-uris` parameters in hello following example do not need toobe actual routable address.</span></span> <span data-ttu-id="68dc5-202">Olá exemplo a seguir também especifica um segredo baseada em senha, em vez de gerar chaves de dentro de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="68dc5-202">hello following example also specifies a password-based secret rather than generating keys from within hello Azure portal.</span></span> <span data-ttu-id="68dc5-203">Neste momento, a geração de chaves não pode ser feita de saudação CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="68dc5-203">As this time, generating keys cannot be done from hello Azure CLI.</span></span>

<span data-ttu-id="68dc5-204">Crie seu próprio aplicativo do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="68dc5-204">Create your Azure Active Directory application.</span></span> <span data-ttu-id="68dc5-205">Olá, exemplo a seguir cria um aplicativo chamado `myAADApp` e usa uma senha de `myPassword`.</span><span class="sxs-lookup"><span data-stu-id="68dc5-205">hello following example creates an application named `myAADApp` and uses a password of `myPassword`.</span></span> <span data-ttu-id="68dc5-206">Especifique sua própria senha da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68dc5-206">Specify your own password as follows:</span></span>

```azurecli
azure ad app create --name myAADApp \
  --home-page http://testencrypt.contoso.com \
  --identifier-uris http://testencrypt.contoso.com \
  --password myPassword
```

<span data-ttu-id="68dc5-207">Anote Olá `applicationId` que é retornado na saída de saudação do hello precede o comando.</span><span class="sxs-lookup"><span data-stu-id="68dc5-207">Make a note of hello `applicationId` that is returned in hello output from hello preceding command.</span></span> <span data-ttu-id="68dc5-208">Essa ID de aplicativo é usado em alguns Olá restantes etapas.</span><span class="sxs-lookup"><span data-stu-id="68dc5-208">This application ID is used in some of hello remaining steps.</span></span> <span data-ttu-id="68dc5-209">Em seguida, crie um nome de entidade de serviço (SPN) para que o aplicativo hello é acessível em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="68dc5-209">Next, create a service principal name (SPN) so that hello application is accessible within your environment.</span></span> <span data-ttu-id="68dc5-210">toosuccessfully criptografar ou descriptografar discos virtuais, as permissões na chave de criptografia Olá armazenadas no cofre de chaves devem ser conjunto toopermit hello Azure Active Directory aplicativo tooread Olá chaves.</span><span class="sxs-lookup"><span data-stu-id="68dc5-210">toosuccessfully encrypt or decrypt virtual disks, permissions on hello cryptographic key stored in Key Vault must be set toopermit hello Azure Active Directory application tooread hello keys.</span></span>

<span data-ttu-id="68dc5-211">Crie Olá SPN e defina as permissões apropriadas Olá da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68dc5-211">Create hello SPN and set hello appropriate permissions as follows:</span></span>

```azurecli
azure ad sp create --applicationId myApplicationID
azure keyvault set-policy --vault-name myKeyVault --spn myApplicationID \
  --perms-to-keys [\"all\"] --perms-to-secrets [\"all\"]
```


## <a name="add-a-virtual-disk-and-review-encryption-status"></a><span data-ttu-id="68dc5-212">Adicione um disco virtual e examine o status da criptografia</span><span class="sxs-lookup"><span data-stu-id="68dc5-212">Add a virtual disk and review encryption status</span></span>
<span data-ttu-id="68dc5-213">tooactually criptografar alguns discos virtuais, permite adicionar uma tooan de disco existente de VM.</span><span class="sxs-lookup"><span data-stu-id="68dc5-213">tooactually encrypt some virtual disks, lets add a disk tooan existing VM.</span></span> <span data-ttu-id="68dc5-214">Adicione um tooan de disco de dados de 5Gb existente VM da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68dc5-214">Add a 5Gb data disk tooan existing VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="68dc5-215">discos virtuais Olá atualmente não são criptografados.</span><span class="sxs-lookup"><span data-stu-id="68dc5-215">hello virtual disks are not currently encrypted.</span></span> <span data-ttu-id="68dc5-216">Revise o status de criptografia atual Olá da VM da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68dc5-216">Review hello current encryption status of your VM as follows:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="encrypt-virtual-disks"></a><span data-ttu-id="68dc5-217">Criptografar discos virtuais</span><span class="sxs-lookup"><span data-stu-id="68dc5-217">Encrypt virtual disks</span></span>
<span data-ttu-id="68dc5-218">toonow criptografar discos virtuais hello, você reúne todos os componentes anteriores do hello:</span><span class="sxs-lookup"><span data-stu-id="68dc5-218">toonow encrypt hello virtual disks, you bring together all hello previous components:</span></span>

1. <span data-ttu-id="68dc5-219">Especifique a senha e o aplicativo do Active Directory do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="68dc5-219">Specify hello Azure Active Directory application and password.</span></span>
2. <span data-ttu-id="68dc5-220">Especifica Olá Cofre de chaves toostore Olá metadados para os discos criptografados.</span><span class="sxs-lookup"><span data-stu-id="68dc5-220">Specify hello Key Vault toostore hello metadata for your encrypted disks.</span></span>
3. <span data-ttu-id="68dc5-221">Especifique Olá toouse de chaves de criptografia para criptografia hello e descriptografia.</span><span class="sxs-lookup"><span data-stu-id="68dc5-221">Specify hello cryptographic keys toouse for hello actual encryption and decryption.</span></span>
4. <span data-ttu-id="68dc5-222">Especifique se você deseja tooencrypt disco de saudação SO, discos de dados de saudação ou todos.</span><span class="sxs-lookup"><span data-stu-id="68dc5-222">Specify whether you want tooencrypt hello OS disk, hello data disks, or all.</span></span>

<span data-ttu-id="68dc5-223">Permite analisar os detalhes de saudação de sua chave de Cofre de chaves do Azure e hello criado, o que for necessário Olá ID cofre da chave, URI e, em seguida, chave de URL na etapa final hello:</span><span class="sxs-lookup"><span data-stu-id="68dc5-223">Lets review hello details for your Azure Key Vault and hello key you created, as you need hello Key Vault ID, URI, and then key URL in hello final step:</span></span>

```azurecli
azure keyvault show myKeyVault
azure keyvault key show myKeyVault myKey
```

<span data-ttu-id="68dc5-224">Criptografar seus discos virtuais usando a saída de saudação do hello `azure keyvault show` e `azure keyvault key show` comandos da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68dc5-224">Encrypt your virtual disks using hello output from hello `azure keyvault show` and `azure keyvault key show` commands as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
```

<span data-ttu-id="68dc5-225">Olá comando anterior tiver muitas variáveis, hello é um exemplo completo de comandos de saudação para referência:</span><span class="sxs-lookup"><span data-stu-id="68dc5-225">As hello preceding command has many variables, hello following example is hello complete command for reference:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id 147bc426-595d-4bad-b267-58a7cbd8e0b6 \
  --aad-client-secret P@ssw0rd! \
  --disk-encryption-key-vault-url https://myKeyVault.vault.azure.net/ \
  --disk-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --key-encryption-key-url https://myKeyVault.vault.azure.net/keys/myKey/6f5fe9383f4e42d0a41553ebc6a82dd1 \
  --key-encryption-key-vault-id /subscriptions/guid/resourceGroups/myResoureGroup/providers/Microsoft.KeyVault/vaults/myKeyVault \
  --volume-type Data
```

<span data-ttu-id="68dc5-226">Olá CLI do Azure não fornece detalhados erros durante o processo de criptografia hello.</span><span class="sxs-lookup"><span data-stu-id="68dc5-226">hello Azure CLI doesn't provide verbose errors during hello encryption process.</span></span> <span data-ttu-id="68dc5-227">Para obter informações adicionais de solução de problemas, examine `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` no hello VM que está criptografando.</span><span class="sxs-lookup"><span data-stu-id="68dc5-227">For additional troubleshooting information, review `/var/log/azure/Microsoft.OSTCExtensions.AzureDiskEncryptionForLinux/0.x.x.x/extension.log` on hello VM you are encrypting.</span></span>

<span data-ttu-id="68dc5-228">Finalmente, permite examinar o status da criptografia Olá novamente tooconfirm que os discos virtuais agora foram criptografados:</span><span class="sxs-lookup"><span data-stu-id="68dc5-228">Finally, lets review hello encryption status again tooconfirm that your virtual disks have now been encrypted:</span></span>

```azurecli
azure vm show-disk-encryption-status --resource-group myResourceGroup --name myVM
```


## <a name="add-additional-data-disks"></a><span data-ttu-id="68dc5-229">Adicionar discos de dados adicionais</span><span class="sxs-lookup"><span data-stu-id="68dc5-229">Add additional data disks</span></span>
<span data-ttu-id="68dc5-230">Depois que você criptografou os discos de dados, você pode posteriormente adicionar discos virtuais adicionais tooyour VM e também criptografá-los.</span><span class="sxs-lookup"><span data-stu-id="68dc5-230">Once you have encrypted your data disks, you can later add additional virtual disks tooyour VM and also encrypt them.</span></span> <span data-ttu-id="68dc5-231">Quando você executa Olá `azure vm enable-disk-encryption` comando, a versão da sequência usando Olá Olá incremento `--sequence-version` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="68dc5-231">When you run hello `azure vm enable-disk-encryption` command, increment hello sequence version using hello `--sequence-version` parameter.</span></span> <span data-ttu-id="68dc5-232">Esse parâmetro de versão de sequência permite tooperform operações repetidas com hello mesma VM.</span><span class="sxs-lookup"><span data-stu-id="68dc5-232">This sequence version parameter allows you tooperform repeated operations on hello same VM.</span></span>

<span data-ttu-id="68dc5-233">Por exemplo, permite adicionar uma segunda tooyour de disco virtual VM da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68dc5-233">For example, lets add a second virtual disk tooyour VM as follows:</span></span>

```azurecli
azure vm disk attach-new --resource-group myResourceGroup --vm-name myVM \
  --size-in-gb 5
```

<span data-ttu-id="68dc5-234">Executar novamente o hello comando tooencrypt Olá discos virtuais, neste momento adicionando Olá `--sequence-version` parâmetro e valor Olá incremento do nosso primeiro execute da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="68dc5-234">Rerun hello command tooencrypt hello virtual disks, this time adding hello `--sequence-version` parameter, and incrementing hello value from our first run as follows:</span></span>

```azurecli
azure vm enable-disk-encryption --resource-group myResourceGroup --name myVM \
  --aad-client-id myApplicationID --aad-client-secret myApplicationPassword \
  --disk-encryption-key-vault-url myKeyVaultVaultURI \
  --disk-encryption-key-vault-id myKeyVaultID \
  --key-encryption-key-url myKeyKID \
  --key-encryption-key-vault-id myKeyVaultID \
  --volume-type Data
  --sequence-version 2
```


## <a name="next-steps"></a><span data-ttu-id="68dc5-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="68dc5-235">Next steps</span></span>
* <span data-ttu-id="68dc5-236">Para obter mais informações sobre como gerenciar o Cofre de Chaves do Azure, incluindo a exclusão de chaves criptográficas e cofres, consulte [Gerenciar Cofres de Chaves usando a CLI](../../key-vault/key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="68dc5-236">For more information about managing Azure Key Vault, including deleting cryptographic keys and vaults, see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md).</span></span>
* <span data-ttu-id="68dc5-237">Para obter mais informações sobre criptografia de disco, como preparar um tooAzure da tooupload VM personalizado criptografado, consulte [criptografia de disco do Azure](../../security/azure-security-disk-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="68dc5-237">For more information about disk encryption, such as preparing an encrypted custom VM tooupload tooAzure, see [Azure Disk Encryption](../../security/azure-security-disk-encryption.md).</span></span>
