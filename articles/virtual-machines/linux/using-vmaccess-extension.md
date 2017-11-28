---
title: aaaReset acesso tooan VM do Linux do Azure | Microsoft Docs
description: "Como toomanage acesso aos usuários e redefinir em VMs do Linux usando Olá extensão VMAccess e Olá 2.0 do CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/04/2017
ms.author: danlep
ms.openlocfilehash: 2f8db01b9fac20bf547d8b1926e5c0b3c5d18280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a><span data-ttu-id="c1c3c-103">Gerenciar usuários, SSH e verificação ou reparo discos em VMs do Linux usando Olá extensão VMAccess com hello 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c1c3c-103">Manage users, SSH, and check or repair disks on Linux VMs using hello VMAccess Extension with hello Azure CLI 2.0</span></span>
<span data-ttu-id="c1c3c-104">disco de saudação em sua VM do Linux está mostrando erros.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-104">hello disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="c1c3c-105">Redefinir a senha de raiz de Olá de alguma forma para sua VM do Linux ou excluído acidentalmente sua chave privada SSH.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-105">You somehow reset hello root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="c1c3c-106">Se isso tiver ocorrido em dias de saudação do datacenter Olá, seria necessário toodrive lá e abra Olá KVM tooget no console do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-106">If that happened back in hello days of hello datacenter, you would need toodrive there and then open hello KVM tooget at hello server console.</span></span> <span data-ttu-id="c1c3c-107">Pense Olá extensão VMAccess do Azure como comutador KVM que permite que você tooaccess Olá console tooreset acesso tooLinux ou realizar a manutenção de nível de disco.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-107">Think of hello Azure VMAccess extension as that KVM switch that allows you tooaccess hello console tooreset access tooLinux or perform disk level maintenance.</span></span>

<span data-ttu-id="c1c3c-108">Este artigo mostra como toouse hello Azure a extensão VMAccess toocheck ou reparar um disco, redefinir o acesso do usuário, gerenciar contas de usuário ou redefinir a configuração de SSH Olá no Linux.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-108">This article shows you how toouse hello Azure VMAccess Extension toocheck or repair a disk, reset user access, manage user accounts, or reset hello SSH configuration on Linux.</span></span> <span data-ttu-id="c1c3c-109">Você também pode executar essas etapas com hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c1c3c-109">You can also perform these steps with hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="ways-toouse-hello-vmaccess-extension"></a><span data-ttu-id="c1c3c-110">Maneiras toouse Olá extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="c1c3c-110">Ways toouse hello VMAccess Extension</span></span>
<span data-ttu-id="c1c3c-111">Há duas maneiras que você pode usar o hello extensão VMAccess em suas VMs do Linux:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-111">There are two ways that you can use hello VMAccess Extension on your Linux VMs:</span></span>

* <span data-ttu-id="c1c3c-112">Use Olá 2.0 do CLI do Azure e os parâmetros de saudação necessário.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-112">Use hello Azure CLI 2.0 and hello required parameters.</span></span>
* <span data-ttu-id="c1c3c-113">[Use JSON bruto arquivos que o processo de extensão VMAccess Olá](#use-json-files-and-the-vmaccess-extension) e agir em seguida.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-113">[Use raw JSON files that hello VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span></span>

<span data-ttu-id="c1c3c-114">Olá use exemplos a seguir [usuário de vm az](/cli/azure/vm/user) comandos.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-114">hello following examples use [az vm user](/cli/azure/vm/user) commands.</span></span> <span data-ttu-id="c1c3c-115">tooperform essas etapas, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c1c3c-115">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="reset-ssh-key"></a><span data-ttu-id="c1c3c-116">Redefinir chave SSH</span><span class="sxs-lookup"><span data-stu-id="c1c3c-116">Reset SSH key</span></span>
<span data-ttu-id="c1c3c-117">Olá, exemplo a seguir redefine uma chave SSH Olá para usuário Olá `azureuser` em Olá VM denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-117">hello following example resets hello SSH key for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a><span data-ttu-id="c1c3c-118">Redefinir senha</span><span class="sxs-lookup"><span data-stu-id="c1c3c-118">Reset password</span></span>
<span data-ttu-id="c1c3c-119">Olá, exemplo a seguir redefine a senha Olá para usuário Olá `azureuser` em Olá VM denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-119">hello following example resets hello password for hello user `azureuser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a><span data-ttu-id="c1c3c-120">Reiniciar o SSH</span><span class="sxs-lookup"><span data-stu-id="c1c3c-120">Restart SSH</span></span>
<span data-ttu-id="c1c3c-121">exemplo a seguir Hello reinicia daemon do SSH hello e redefine Olá SSH valores de toodefault de configuração em uma VM denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-121">hello following example restarts hello SSH daemon and resets hello SSH configuration toodefault values on a VM named `myVM`:</span></span>

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a><span data-ttu-id="c1c3c-122">Criar um usuário</span><span class="sxs-lookup"><span data-stu-id="c1c3c-122">Create a user</span></span>
<span data-ttu-id="c1c3c-123">Olá, exemplo a seguir cria um usuário chamado `myNewUser` usando uma chave SSH para autenticação no hello VM denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-123">hello following example creates a user named `myNewUser` using an SSH key for authentication on hello VM named `myVM`:</span></span>

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a><span data-ttu-id="c1c3c-124">Excluir um usuário</span><span class="sxs-lookup"><span data-stu-id="c1c3c-124">Delete a user</span></span>
<span data-ttu-id="c1c3c-125">Olá, exemplo a seguir exclui um usuário chamado `myNewUser` em Olá VM denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-125">hello following example deletes a user named `myNewUser` on hello VM named `myVM`:</span></span>

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a><span data-ttu-id="c1c3c-126">Use arquivos JSON e Olá extensão VMAccess</span><span class="sxs-lookup"><span data-stu-id="c1c3c-126">Use JSON files and hello VMAccess Extension</span></span>
<span data-ttu-id="c1c3c-127">Olá exemplos a seguir usa arquivos brutos do JSON.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-127">hello following examples use raw JSON files.</span></span> <span data-ttu-id="c1c3c-128">Use [conjunto de extensão de vm az](/cli/azure/vm/extension#set) toothen chamar seus arquivos JSON.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-128">Use [az vm extension set](/cli/azure/vm/extension#set) toothen call your JSON files.</span></span> <span data-ttu-id="c1c3c-129">Esses arquivos JSON também podem ser chamados dos modelos do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-129">These JSON files can also be called from Azure templates.</span></span> 

### <a name="reset-user-access"></a><span data-ttu-id="c1c3c-130">Redefinir o acesso do usuário</span><span class="sxs-lookup"><span data-stu-id="c1c3c-130">Reset user access</span></span>
<span data-ttu-id="c1c3c-131">Se você tiver perdido acesso tooroot em sua VM do Linux, você pode iniciar um tooreset de script VMAccess chave SSH ou a senha do usuário.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-131">If you have lost access tooroot on your Linux VM, you can launch a VMAccess script tooreset a user's SSH key or password.</span></span>

<span data-ttu-id="c1c3c-132">chave pública do tooreset Olá SSH de um usuário, crie um arquivo chamado `reset_ssh_key.json` e adicionar configurações Olá formato a seguir.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-132">tooreset hello SSH public key of a user, create a file named `reset_ssh_key.json` and add settings in hello following format.</span></span> <span data-ttu-id="c1c3c-133">Substitua seus próprios valores para Olá `username` e `ssh_key` parâmetros:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-133">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

<span data-ttu-id="c1c3c-134">Execute o script de VMAccess Olá com:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-134">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

<span data-ttu-id="c1c3c-135">tooreset uma senha de usuário, crie um arquivo chamado `reset_user_password.json` e adicionar configurações Olá formato a seguir.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-135">tooreset a user password, create a file named `reset_user_password.json` and add settings in hello following format.</span></span> <span data-ttu-id="c1c3c-136">Substitua seus próprios valores para Olá `username` e `password` parâmetros:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-136">Substitute your own values for hello `username` and `password` parameters:</span></span>

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

<span data-ttu-id="c1c3c-137">Execute o script de VMAccess Olá com:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-137">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a><span data-ttu-id="c1c3c-138">Reiniciar o SSH</span><span class="sxs-lookup"><span data-stu-id="c1c3c-138">Restart SSH</span></span>
<span data-ttu-id="c1c3c-139">toorestart Olá daemon SSH e redefina os valores de toodefault de configuração do SSH hello, crie um arquivo chamado `reset_sshd.json`.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-139">toorestart hello SSH daemon and reset hello SSH configuration toodefault values, create a file named `reset_sshd.json`.</span></span> <span data-ttu-id="c1c3c-140">Adicione Olá conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-140">Add hello following content:</span></span>

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="c1c3c-141">Execute o script de VMAccess Olá com:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-141">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a><span data-ttu-id="c1c3c-142">Gerenciar usuários</span><span class="sxs-lookup"><span data-stu-id="c1c3c-142">Manage users</span></span>

<span data-ttu-id="c1c3c-143">toocreate um usuário que usa uma chave SSH para a autenticação, crie um arquivo chamado `create_new_user.json` e adicionar configurações Olá formato a seguir.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-143">toocreate a user that uses an SSH key for authentication, create a file named `create_new_user.json` and add settings in hello following format.</span></span> <span data-ttu-id="c1c3c-144">Substitua seus próprios valores para Olá `username` e `ssh_key` parâmetros:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-144">Substitute your own values for hello `username` and `ssh_key` parameters:</span></span>

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="c1c3c-145">Execute o script de VMAccess Olá com:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-145">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

<span data-ttu-id="c1c3c-146">toodelete um usuário, crie um arquivo chamado `delete_user.json` e adicione Olá conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-146">toodelete a user, create a file named `delete_user.json` and add hello following content.</span></span> <span data-ttu-id="c1c3c-147">Substituir seu próprio valor para Olá `remove_user` parâmetro:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-147">Substitute your own value for hello `remove_user` parameter:</span></span>

```json
{
  "remove_user":"myNewUser"
}
```

<span data-ttu-id="c1c3c-148">Execute o script de VMAccess Olá com:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-148">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a><span data-ttu-id="c1c3c-149">Verificar ou reparar o disco Olá</span><span class="sxs-lookup"><span data-stu-id="c1c3c-149">Check or repair hello disk</span></span>
<span data-ttu-id="c1c3c-150">Usar o VMAccess você pode verificar e reparar um disco que você adicionou toohello VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-150">Using VMAccess you can also check and repair a disk that you added toohello Linux VM.</span></span>

<span data-ttu-id="c1c3c-151">Reparo Olá disco, toocheck e, em seguida, crie um arquivo chamado `disk_check_repair.json` e adicionar configurações Olá formato a seguir.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-151">toocheck and then repair hello disk, create a file named `disk_check_repair.json` and add settings in hello following format.</span></span> <span data-ttu-id="c1c3c-152">Substituir seu próprio valor para nome de saudação do `repair_disk`:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-152">Substitute your own value for hello name of `repair_disk`:</span></span>

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

<span data-ttu-id="c1c3c-153">Execute o script de VMAccess Olá com:</span><span class="sxs-lookup"><span data-stu-id="c1c3c-153">Execute hello VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a><span data-ttu-id="c1c3c-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c1c3c-154">Next steps</span></span>
<span data-ttu-id="c1c3c-155">Atualizando Linux usar hello Azure a extensão VMAccess é as alterações de toomake um método em uma VM do Linux em execução.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-155">Updating Linux using hello Azure VMAccess Extension is one method toomake changes on a running Linux VM.</span></span> <span data-ttu-id="c1c3c-156">Você também pode usar ferramentas como init de nuvem e o Azure Resource Manager modelos toomodify sua VM do Linux na inicialização.</span><span class="sxs-lookup"><span data-stu-id="c1c3c-156">You can also use tools like cloud-init and Azure Resource Manager templates toomodify your Linux VM on boot.</span></span>

[<span data-ttu-id="c1c3c-157">Recursos e extensões da máquina virtual para Linux</span><span class="sxs-lookup"><span data-stu-id="c1c3c-157">Virtual machine extensions and features for Linux</span></span>](extensions-features.md)

[<span data-ttu-id="c1c3c-158">Criando modelos do Azure Resource Manager com extensões de VM do Linux</span><span class="sxs-lookup"><span data-stu-id="c1c3c-158">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="c1c3c-159">Usando a nuvem init toocustomize uma VM do Linux durante a criação</span><span class="sxs-lookup"><span data-stu-id="c1c3c-159">Using cloud-init toocustomize a Linux VM during creation</span></span>](using-cloud-init.md)

