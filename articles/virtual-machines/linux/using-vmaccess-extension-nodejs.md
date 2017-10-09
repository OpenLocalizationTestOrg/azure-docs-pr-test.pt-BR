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
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-hello-vmaccess-extension-with-hello-azure-cli-10"></a>Gerenciar usuários, SSH e seleção ou discos de reparo em máquinas virtuais do Linux do Azure usando Olá extensão VMAccess com hello 1.0 da CLI do Azure
Este artigo mostra como toouse hello Azure VMAcesss extensão toocheck ou reparar um disco, redefinir o acesso do usuário, gerenciar contas de usuário ou redefinir a configuração de SSHD Olá no Linux. artigo Olá requer:

* uma conta do Azure ([obtenha uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)).
* Olá [CLI do Azure](../../cli-install-nodejs.md) conectado `azure login`.
* Olá CLI do Azure *devem estar no* modo do Azure Resource Manager `azure config mode arm`.


## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](#quick-commands)– nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação


## <a name="quick-commands"></a>Comandos rápidos
Há duas maneiras toouse VMAccess em suas VMs do Linux:

* Usar hello Azure CLI 1.0 e Olá parâmetros necessários.
* Usando os arquivos JSON brutos que a VMAccess processa e usa.

Seção de comando rápido Olá, vamos toouse hello Azure CLI 1.0 `azure vm reset-access` método. No Olá a seguir exemplos de comando, substitua os valores de Olá que contêm "exemplo" com valores de saudação do seu próprio ambiente.

## <a name="create-a-resource-group-and-linux-vm"></a>Criar um Grupo de Recursos e uma VM do Linux
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a>Criar uma VM Debian
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

## <a name="reset-root-password"></a>Redefinir a senha raiz
senha de raiz de saudação tooreset:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a>Redefinição de chave SSH
chave SSH tooreset Olá de um usuário não raiz:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a>Criar um usuário
toocreate um usuário:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a>Remover um usuário
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a>Redefinir SSHD
configuração do tooreset Olá SSHD:

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a>Passo a passo detalhado
### <a name="vmaccess-defined"></a>VMAccess definido:
disco de saudação em sua VM do Linux está mostrando erros. Redefinir a senha de raiz de Olá de alguma forma para sua VM do Linux ou excluído acidentalmente sua chave privada SSH. Se isso tiver ocorrido em dias de saudação do datacenter Olá, seria necessário toodrive lá e abra Olá KVM tooget no console do servidor de saudação. Pense Olá extensão VMAccess do Azure como comutador KVM que permite que você tooaccess Olá console tooreset acesso tooLinux ou realizar a manutenção de nível de disco.

Para Olá detalhadas passo a passo, vamos toouse Olá longas de VMAccess, que usa arquivos brutos do JSON.  Esses arquivos json da VMAccess também podem ser chamados desde os Modelos do Azure.

### <a name="using-vmaccess-toocheck-or-repair-hello-disk-of-a-linux-vm"></a>Usando VMAccess toocheck ou reparo do disco de saudação de uma VM do Linux
Usar o VMAccess pode fazer um fsck executado em disco Olá em sua VM do Linux.  Você também pode fazer uma verificação e um reparo de disco usando uma VMAccess.

toocheck e reparo Olá disco usam esse script de VMAccess:

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

Execute o script de VMAccess Olá com:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-tooreset-user-access-toolinux"></a>Usando o VMAccess tooreset usuário acesso tooLinux
Se você tiver perdido acesso tooroot em sua VM do Linux, você pode iniciar uma senha de raiz VMAccess script tooreset hello.

senha de raiz de saudação tooreset, use este script VMAccess:

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

Execute o script de VMAccess Olá com:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

a chave SSH Olá tooreset de um usuário não raiz, use esse script VMAccess:

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

Execute o script de VMAccess Olá com:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-toomanage-user-accounts-on-linux"></a>Usando contas de usuário toomanage VMAccess no Linux
VMAccess é um script de Python que pode ser usados toomanage usuários em sua VM Linux sem logon e usando a conta raiz de sudo ou hello.

toocreate um usuário, use esse script VMAccess:

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

Execute o script de VMAccess Olá com:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

toodelete um usuário, use esse script VMAccess:

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

Execute o script de VMAccess Olá com:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-tooreset-hello-sshd-configuration"></a>Usando VMAccess tooreset Olá SSHD configuração
Se você fizer a configuração de Linux VMs SSHD toohello alterações e conexão de SSH Olá fechar antes de verificar as alterações de saudação, você pode ser impedido de SSH'ing novamente.  VMAccess pode ser usado tooreset Olá SSHD configuração tooa back configuração válida sem que está sendo conectado via SSH.

configuração de SSHD Olá tooreset usar esse script de VMAccess:

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

Execute o script de VMAccess Olá com:

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a>Próximas etapas
Atualizando Linux usando as extensões de VMAccess do Azure é um alterações toomake de método em uma VM do Linux em execução.  Você também pode usar ferramentas como nuvem init e modelos do Azure toomodify sua VM do Linux na inicialização.

[Sobre os recursos e extensões de máquina virtual](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Criando modelos do Azure Resource Manager com extensões de VM do Linux](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Usando a nuvem init toocustomize uma VM do Linux durante a criação](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

