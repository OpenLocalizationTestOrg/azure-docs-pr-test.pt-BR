---
title: aaaJoin tooan uma VM do Linux RedHat Azure Active Directory DS | Microsoft Docs
description: "Como toojoin uma tooan de RedHat Enterprise Linux 7 VM existente do Azure serviço de domínio Active Directory."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: f3ba3c764e253191753f1cc5fc8c3b85c53818af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a>Unir um tooan RedHat Linux VM Azure serviço de domínio Active Directory

Este artigo mostra como toojoin uma tooan de máquina virtual do Red Hat Enterprise Linux (RHEL) 7 serviços de domínio do Active Directory (AADDS) do Azure gerenciados domínio.  requisitos de saudação são:

- [uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/)

- [arquivos de chave SSH pública e privada](mac-create-ssh-keys.md)

- [Um controlador de domínio do Azure Active Directory Domain Services](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a>Comandos rápidos

_Substitua quaisquer exemplos por suas próprias configurações._

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a>Modo de implantação de tooclassic do comutador hello cli do azure

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a>Pesquise uma versão do RHEL e uma imagem

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a>Criar uma VM Red Hat do Linux

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-toohello-vm"></a>SSH toohello VM

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a>Atualizar os pacotes YUM

```bash
sudo yum update
```

### <a name="install-packages-needed"></a>Instalar os pacotes necessários

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

Agora que pacotes Olá necessários estão instalados na máquina de virtual do Linux hello, Olá próxima tarefa é domínio gerenciado do toohello toojoin Olá máquina virtual.

### <a name="discover-hello-aad-domain-services-managed-domain"></a>Descobrir o domínio gerenciado do serviços de domínio do AAD Olá

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a>Inicializar o Kerberos

Certifique-se de que você especifique um usuário que pertence a toohello ' AAD controlador de domínio do grupo 'Administradores. Apenas esses usuários podem ingressar em domínio gerenciado toohello dos computadores.

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a>Ingressar Olá máquina toohello domínio

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a>Verifique se machine Olá é toohello ingressado no domínio

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a>Próximas etapas

* [RHUI (Infraestrutura de Atualização do Red Hat) para as VMs Red Hat Enterprise do Linux sob demanda no Azure](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Configurar o Cofre de Chaves para máquinas virtuais no Azure Resource Manager](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Implantar e gerenciar máquinas virtuais usando modelos do Gerenciador de recursos do Azure e hello CLI do Azure](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
