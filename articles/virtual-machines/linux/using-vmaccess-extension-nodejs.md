---
title: "acesso de aaaReset em VMs do Linux do Azure usando Olá extensão VMAccess | Microsoft Docs"
description: "Redefina o acesso em VMs do Linux do Azure usando Olá extensão VMAccess."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 2636655f3f7d14ba30e1dc62c319e4e278521ead
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a><span data-ttu-id="37a07-103">Gerenciar usuários, SSH e seleção ou discos de reparo em máquinas virtuais do Linux do Azure usando Olá extensão VMAccess com hello 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="37a07-103">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="37a07-104">Este artigo mostra como toouse hello Azure VMAcesss extensão toocheck ou reparar um disco, redefinir o acesso do usuário, gerenciar contas de usuário ou redefinir a configuração de SSHD Olá no Linux.</span><span class="sxs-lookup"><span data-stu-id="37a07-104">This article shows you how toouse hello Azure VMAcesss Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSHD configuration on Linux.</span></span> <span data-ttu-id="37a07-105">artigo Olá requer:</span><span class="sxs-lookup"><span data-stu-id="37a07-105">hello article requires:</span></span>

* <span data-ttu-id="37a07-106">uma conta do Azure ([obtenha uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="37a07-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="37a07-107">Olá [CLI do Azure](../../cli-install-nodejs.md) conectado `azure login`.</span><span class="sxs-lookup"><span data-stu-id="37a07-107">hello [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="37a07-108">Olá CLI do Azure *devem estar no* modo do Azure Resource Manager `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="37a07-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="37a07-109">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="37a07-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="37a07-110">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="37a07-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="37a07-111">[1.0 de CLI do Azure](#quick-commands)– nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="37a07-111">[Azure CLI 1.0](#quick-commands)– our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="37a07-112">[2.0 do CLI do Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="37a07-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="37a07-113">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="37a07-113">Quick commands</span></span>
<span data-ttu-id="37a07-114">Há duas maneiras toouse VMAccess em suas VMs do Linux:</span><span class="sxs-lookup"><span data-stu-id="37a07-114">There are two ways toouse VMAccess on your Linux VMs:</span></span>

* <span data-ttu-id="37a07-115">Usar hello Azure CLI 1.0 e Olá parâmetros necessários.</span><span class="sxs-lookup"><span data-stu-id="37a07-115">Using hello Azure CLI 1.0 and hello required parameters.</span></span>
* <span data-ttu-id="37a07-116">Usando os arquivos JSON brutos que a VMAccess processa e usa.</span><span class="sxs-lookup"><span data-stu-id="37a07-116">Using raw JSON files that VMAccess processes and then act on.</span></span>

<span data-ttu-id="37a07-117">Seção de comando rápido Olá, vamos toouse hello Azure CLI 1.0 `azure vm reset-access` método.</span><span class="sxs-lookup"><span data-stu-id="37a07-117">For hello quick command section, we are going toouse hello Azure CLI 1.0 `azure vm reset-access` method.</span></span> <span data-ttu-id="37a07-118">No Olá a seguir exemplos de comando, substitua os valores de Olá que contêm "exemplo" com valores de saudação do seu próprio ambiente.</span><span class="sxs-lookup"><span data-stu-id="37a07-118">In hello following command examples, replace hello values that contain "example" with hello values from your own environment.</span></span>

## <a name="create-a-resource-group-and-linux-vm"></a><span data-ttu-id="37a07-119">Criar um Grupo de Recursos e uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="37a07-119">Create a Resource Group and Linux VM</span></span>
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a><span data-ttu-id="37a07-120">Criar uma VM Debian</span><span class="sxs-lookup"><span data-stu-id="37a07-120">Create a Debian VM</span></span>
```azurecli
azure vm quick-create \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -g myResourceGroup \
  -l westus \
  -y Linux \
  -n myVM \
  -Q Debian
```

## <a name="reset-root-password"></a><span data-ttu-id="37a07-121">Redefinir a senha raiz</span><span class="sxs-lookup"><span data-stu-id="37a07-121">Reset root password</span></span>
<span data-ttu-id="37a07-122">senha de raiz de saudação tooreset:</span><span class="sxs-lookup"><span data-stu-id="37a07-122">tooreset hello root password:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a><span data-ttu-id="37a07-123">Redefinição de chave SSH</span><span class="sxs-lookup"><span data-stu-id="37a07-123">SSH key reset</span></span>
<span data-ttu-id="37a07-124">chave SSH tooreset Olá de um usuário não raiz:</span><span class="sxs-lookup"><span data-stu-id="37a07-124">tooreset hello SSH key of a non-root user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a><span data-ttu-id="37a07-125">Criar um usuário</span><span class="sxs-lookup"><span data-stu-id="37a07-125">Create a user</span></span>
<span data-ttu-id="37a07-126">toocreate um usuário:</span><span class="sxs-lookup"><span data-stu-id="37a07-126">toocreate a user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a><span data-ttu-id="37a07-127">Remover um usuário</span><span class="sxs-lookup"><span data-stu-id="37a07-127">Remove a user</span></span>
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a><span data-ttu-id="37a07-128">Redefinir SSHD</span><span class="sxs-lookup"><span data-stu-id="37a07-128">Reset SSHD</span></span>
<span data-ttu-id="37a07-129">configuração do tooreset Olá SSHD:</span><span class="sxs-lookup"><span data-stu-id="37a07-129">tooreset hello SSHD configuration:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a><span data-ttu-id="37a07-130">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="37a07-130">Detailed walkthrough</span></span>
### <a name="vmaccess-defined"></a><span data-ttu-id="37a07-131">VMAccess definido:</span><span class="sxs-lookup"><span data-stu-id="37a07-131">VMAccess defined:</span></span>
<span data-ttu-id="37a07-132">disco de saudação em sua VM do Linux está mostrando erros.</span><span class="sxs-lookup"><span data-stu-id="37a07-132">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="37a07-133">Redefinir a senha de raiz de Olá de alguma forma para sua VM do Linux ou excluído acidentalmente sua chave privada SSH.</span><span class="sxs-lookup"><span data-stu-id="37a07-133">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="37a07-134">Se isso tiver ocorrido em dias de saudação do datacenter Olá, seria necessário toodrive lá e abra Olá KVM tooget no console do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="37a07-134">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="37a07-135">Pense Olá extensão VMAccess do Azure como comutador KVM que permite que você tooaccess Olá console tooreset acesso tooLinux ou realizar a manutenção de nível de disco.</span><span class="sxs-lookup"><span data-stu-id="37a07-135">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="37a07-136">Para Olá detalhadas passo a passo, vamos toouse Olá longas de VMAccess, que usa arquivos brutos do JSON.</span><span class="sxs-lookup"><span data-stu-id="37a07-136">For hello detailed walkthrough, we are going toouse hello long form of VMAccess, which uses raw JSON files.</span></span>  <span data-ttu-id="37a07-137">Esses arquivos json da VMAccess também podem ser chamados desde os Modelos do Azure.</span><span class="sxs-lookup"><span data-stu-id="37a07-137">These VMAccess JSON files can also be called from Azure templates.</span></span>

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a><span data-ttu-id="37a07-138">Usando VMAccess toocheck ou reparo do disco de saudação de uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="37a07-138">Using VMAccess toocheck or repair hello disk of a Linux VM</span></span>
<span data-ttu-id="37a07-139">Usar o VMAccess pode fazer um fsck executado em disco Olá em sua VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="37a07-139">Using VMAccess you can do a fsck run on hello disk under your Linux VM.</span></span>  <span data-ttu-id="37a07-140">Você também pode fazer uma verificação e um reparo de disco usando uma VMAccess.</span><span class="sxs-lookup"><span data-stu-id="37a07-140">You can also do a disk check and a disk repair using a VMAccess.</span></span>

<span data-ttu-id="37a07-141">toocheck e reparo Olá disco usam esse script de VMAccess:</span><span class="sxs-lookup"><span data-stu-id="37a07-141">toocheck, and then repair hello disk use this VMAccess script:</span></span>

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

<span data-ttu-id="37a07-142">Execute o script de VMAccess Olá com:</span><span class="sxs-lookup"><span data-stu-id="37a07-142">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a><span data-ttu-id="37a07-143">Usando o VMAccess tooreset usuário acesso tooLinux</span><span class="sxs-lookup"><span data-stu-id="37a07-143">Using VMAccess tooreset user access tooLinux</span></span>
<span data-ttu-id="37a07-144">Se você tiver perdido acesso tooroot em sua VM do Linux, você pode iniciar uma senha de raiz VMAccess script tooreset hello.</span><span class="sxs-lookup"><span data-stu-id="37a07-144">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset hello root password.</span></span>

<span data-ttu-id="37a07-145">senha de raiz de saudação tooreset, use este script VMAccess:</span><span class="sxs-lookup"><span data-stu-id="37a07-145">tooreset hello root password, use this VMAccess script:</span></span>

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

<span data-ttu-id="37a07-146">Execute o script de VMAccess Olá com:</span><span class="sxs-lookup"><span data-stu-id="37a07-146">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

<span data-ttu-id="37a07-147">a chave SSH Olá tooreset de um usuário não raiz, use esse script VMAccess:</span><span class="sxs-lookup"><span data-stu-id="37a07-147">tooreset hello SSH key of a non-root user, use this VMAccess script:</span></span>

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

<span data-ttu-id="37a07-148">Execute o script de VMAccess Olá com:</span><span class="sxs-lookup"><span data-stu-id="37a07-148">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a><span data-ttu-id="37a07-149">Usando contas de usuário toomanage VMAccess no Linux</span><span class="sxs-lookup"><span data-stu-id="37a07-149">Using VMAccess toomanage user accounts on Linux</span></span>
<span data-ttu-id="37a07-150">VMAccess é um script de Python que pode ser usados toomanage usuários em sua VM Linux sem logon e usando a conta raiz de sudo ou hello.</span><span class="sxs-lookup"><span data-stu-id="37a07-150">VMAccess is a Python script that can be used toomanage users on your Linux VM without logging in and using sudo or hello root account.</span></span>

<span data-ttu-id="37a07-151">toocreate um usuário, use esse script VMAccess:</span><span class="sxs-lookup"><span data-stu-id="37a07-151">toocreate a user, use this VMAccess script:</span></span>

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="37a07-152">Execute o script de VMAccess Olá com:</span><span class="sxs-lookup"><span data-stu-id="37a07-152">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

<span data-ttu-id="37a07-153">toodelete um usuário, use esse script VMAccess:</span><span class="sxs-lookup"><span data-stu-id="37a07-153">toodelete a user, use this VMAccess script:</span></span>

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

<span data-ttu-id="37a07-154">Execute o script de VMAccess Olá com:</span><span class="sxs-lookup"><span data-stu-id="37a07-154">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a><span data-ttu-id="37a07-155">Usando VMAccess tooreset Olá SSHD configuração</span><span class="sxs-lookup"><span data-stu-id="37a07-155">Using VMAccess tooreset hello SSHD configuration</span></span>
<span data-ttu-id="37a07-156">Se você fizer a configuração de Linux VMs SSHD toohello alterações e conexão de SSH Olá fechar antes de verificar as alterações de saudação, você pode ser impedido de SSH'ing novamente.</span><span class="sxs-lookup"><span data-stu-id="37a07-156">If you make changes toohello Linux VMs SSHD configuration and close hello SSH connection before verifying hello changes, you may be prevented from SSH'ing back in.</span></span>  <span data-ttu-id="37a07-157">VMAccess pode ser usado tooreset Olá SSHD configuração tooa back configuração válida sem que está sendo conectado via SSH.</span><span class="sxs-lookup"><span data-stu-id="37a07-157">VMAccess can be used tooreset hello SSHD configuration back tooa known good configuration without being logged in over SSH.</span></span>

<span data-ttu-id="37a07-158">configuração de SSHD Olá tooreset usar esse script de VMAccess:</span><span class="sxs-lookup"><span data-stu-id="37a07-158">tooreset hello SSHD configuration use this VMAccess script:</span></span>

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="37a07-159">Execute o script de VMAccess Olá com:</span><span class="sxs-lookup"><span data-stu-id="37a07-159">Execute hello VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a><span data-ttu-id="37a07-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="37a07-160">Next steps</span></span>
<span data-ttu-id="37a07-161">Atualizando Linux usando as extensões de VMAccess do Azure é um alterações toomake de método em uma VM do Linux em execução.</span><span class="sxs-lookup"><span data-stu-id="37a07-161">Updating Linux using Azure VMAccess Extensions is one method toomake changes on a running Linux VM.</span></span>  <span data-ttu-id="37a07-162">Você também pode usar ferramentas como nuvem init e modelos do Azure toomodify sua VM do Linux na inicialização.</span><span class="sxs-lookup"><span data-stu-id="37a07-162">You can also use tools like cloud-init and Azure Templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="37a07-163">Sobre os recursos e extensões de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="37a07-163">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="37a07-164">Criando modelos do Azure Resource Manager com extensões de VM do Linux</span><span class="sxs-lookup"><span data-stu-id="37a07-164">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="37a07-165">Usando a nuvem init toocustomize uma VM do Linux durante a criação</span><span class="sxs-lookup"><span data-stu-id="37a07-165">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

