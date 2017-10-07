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
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-20"></a>Gerenciar usuários, SSH e verificação ou reparo discos em VMs do Linux usando Olá extensão VMAccess com hello 2.0 do CLI do Azure
disco de saudação em sua VM do Linux está mostrando erros. Redefinir a senha de raiz de Olá de alguma forma para sua VM do Linux ou excluído acidentalmente sua chave privada SSH. Se isso tiver ocorrido em dias de saudação do datacenter Olá, seria necessário toodrive lá e abra Olá KVM tooget no console do servidor de saudação. Pense Olá extensão VMAccess do Azure como comutador KVM que permite que você tooaccess Olá console tooreset acesso tooLinux ou realizar a manutenção de nível de disco.

Este artigo mostra como toouse hello Azure a extensão VMAccess toocheck ou reparar um disco, redefinir o acesso do usuário, gerenciar contas de usuário ou redefinir a configuração de SSH Olá no Linux. Você também pode executar essas etapas com hello [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).


## <a name="ways-toouse-hello-vmaccess-extension"></a>Maneiras toouse Olá extensão VMAccess
Há duas maneiras que você pode usar o hello extensão VMAccess em suas VMs do Linux:

* Use Olá 2.0 do CLI do Azure e os parâmetros de saudação necessário.
* [Use JSON bruto arquivos que o processo de extensão VMAccess Olá](#use-json-files-and-the-vmaccess-extension) e agir em seguida.

Olá use exemplos a seguir [usuário de vm az](/cli/azure/vm/user) comandos. tooperform essas etapas, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).

## <a name="reset-ssh-key"></a>Redefinir chave SSH
Olá, exemplo a seguir redefine uma chave SSH Olá para usuário Olá `azureuser` em Olá VM denominada `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a>Redefinir senha
Olá, exemplo a seguir redefine a senha Olá para usuário Olá `azureuser` em Olá VM denominada `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="restart-ssh"></a>Reiniciar o SSH
exemplo a seguir Hello reinicia daemon do SSH hello e redefine Olá SSH valores de toodefault de configuração em uma VM denominada `myVM`:

```azurecli
az vm user reset-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a>Criar um usuário
Olá, exemplo a seguir cria um usuário chamado `myNewUser` usando uma chave SSH para autenticação no hello VM denominada `myVM`:

```azurecli
az vm user update \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="delete-a-user"></a>Excluir um usuário
Olá, exemplo a seguir exclui um usuário chamado `myNewUser` em Olá VM denominada `myVM`:

```azurecli
az vm user delete \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-hello-vmaccess-extension"></a>Use arquivos JSON e Olá extensão VMAccess
Olá exemplos a seguir usa arquivos brutos do JSON. Use [conjunto de extensão de vm az](/cli/azure/vm/extension#set) toothen chamar seus arquivos JSON. Esses arquivos JSON também podem ser chamados dos modelos do Azure. 

### <a name="reset-user-access"></a>Redefinir o acesso do usuário
Se você tiver perdido acesso tooroot em sua VM do Linux, você pode iniciar um tooreset de script VMAccess chave SSH ou a senha do usuário.

chave pública do tooreset Olá SSH de um usuário, crie um arquivo chamado `reset_ssh_key.json` e adicionar configurações Olá formato a seguir. Substitua seus próprios valores para Olá `username` e `ssh_key` parâmetros:

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNGxxxxxx2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7xxxxxxwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5wxxtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

Execute o script de VMAccess Olá com:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

tooreset uma senha de usuário, crie um arquivo chamado `reset_user_password.json` e adicionar configurações Olá formato a seguir. Substitua seus próprios valores para Olá `username` e `password` parâmetros:

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

Execute o script de VMAccess Olá com:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="restart-ssh"></a>Reiniciar o SSH
toorestart Olá daemon SSH e redefina os valores de toodefault de configuração do SSH hello, crie um arquivo chamado `reset_sshd.json`. Adicione Olá conteúdo a seguir:

```json
{
  "reset_ssh": true
}
```

Execute o script de VMAccess Olá com:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a>Gerenciar usuários

toocreate um usuário que usa uma chave SSH para a autenticação, crie um arquivo chamado `create_new_user.json` e adicionar configurações Olá formato a seguir. Substitua seus próprios valores para Olá `username` e `ssh_key` parâmetros:

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Execute o script de VMAccess Olá com:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

toodelete um usuário, crie um arquivo chamado `delete_user.json` e adicione Olá conteúdo a seguir. Substituir seu próprio valor para Olá `remove_user` parâmetro:

```json
{
  "remove_user":"myNewUser"
}
```

Execute o script de VMAccess Olá com:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-hello-disk"></a>Verificar ou reparar o disco Olá
Usar o VMAccess você pode verificar e reparar um disco que você adicionou toohello VM do Linux.

Reparo Olá disco, toocheck e, em seguida, crie um arquivo chamado `disk_check_repair.json` e adicionar configurações Olá formato a seguir. Substituir seu próprio valor para nome de saudação do `repair_disk`:

```json
{
  "check_disk": "true",
  "repair_disk": "true, mydiskname"
}
```

Execute o script de VMAccess Olá com:

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a>Próximas etapas
Atualizando Linux usar hello Azure a extensão VMAccess é as alterações de toomake um método em uma VM do Linux em execução. Você também pode usar ferramentas como init de nuvem e o Azure Resource Manager modelos toomodify sua VM do Linux na inicialização.

[Recursos e extensões da máquina virtual para Linux](extensions-features.md)

[Criando modelos do Azure Resource Manager com extensões de VM do Linux](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Usando a nuvem init toocustomize uma VM do Linux durante a criação](using-cloud-init.md)

