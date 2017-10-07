---
title: "aaaAdd tooa um usuário VM do Linux no Azure | Microsoft Docs"
description: "Adicione um usuário tooa VM do Linux no Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8aa633b-8b75-45d7-b61d-11ac112cedd5
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/18/2016
ms.author: v-livech
ms.openlocfilehash: eed050154adf0cbed2c168e7aa675bd3ded85fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-user-tooan-azure-vm"></a>Adicionar um usuário tooan VM do Azure
Uma das primeiras tarefas hello em qualquer nova VM do Linux é toocreate um novo usuário.  Neste artigo, percorremos criando uma conta de usuário do sudo, definir senha de hello, adicionando chaves públicas SSH e finalmente usar `visudo` sudo tooallow sem uma senha.

Pré-requisitos são: [uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/), [as chaves públicas e privadas SSH](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), um grupo de recursos do Azure e Olá CLI do Azure instalado e alternado tooAzure Gerenciador de recursos usando o modo `azure config mode arm`.

## <a name="quick-commands"></a>Comandos rápidos
```bash
# Add a new user on RedHat family distros
sudo useradd -G wheel exampleUser

# Add a new user on Debian family distros
sudo useradd -G sudo exampleUser

# Set a password
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully

# Copy hello SSH Public Key toohello new user
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver

# Change sudoers tooallow no password
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL

# Verify everything
# Verify hello SSH keys & User account
bill@slackware$ ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```

## <a name="detailed-walkthrough"></a>Passo a passo detalhado
### <a name="introduction"></a>Introdução
Uma das tarefas de primeira e mais comum de saudação com um novo servidor é tooadd uma conta de usuário.  Logons de raiz devem ser desabilitados e conta de raiz de saudação em si não deve ser usada com o servidor Linux, somente o sudo.  Fornecendo um escalonamento do usuário raiz privilégios usando o sudo-Olá tooadminister de forma adequada e usar o Linux.

Usando o comando Olá `useradd` estamos adicionando contas de usuário toohello VM do Linux.  Executar `useradd` modifica `/etc/passwd`, `/etc/shadow`, `/etc/group` e `/etc/gshadow`.  Estamos adicionando um sinalizador de linha de comando toohello `useradd` comando tooalso adicionar Olá novo usuário toohello sudo adequada grupo no Linux.  Mesmo que você `useradd` cria uma entrada em `/etc/passwd` ele não oferece a nova conta de usuário Olá uma senha.  Estamos criando uma senha inicial para o novo usuário de saudação usando Olá simples `passwd` comando.  Olá última etapa é toomodify Olá sudo regras que comandos tooexecute de usuário com privilégios de sudo tooallow sem ter que tooenter uma senha para cada comando.  Fazer logon usando a chave privada hello, assumindo que essa conta de usuário está protegido contra atores ruins e vai tooallow sudo acesso sem uma senha.  

### <a name="adding-a-single-sudo-user-tooan-azure-vm"></a>Adicionar um usuário de único sudo tooan VM do Azure
Faça logon no toohello VM do Azure usando as chaves de SSH.  Se você não tiver configurado o acesso de chave pública SSH, leia este artigo primeiro [Using Public Key Authentication with Azure](http://link.to/article)(Usando Autenticação de Chave Pública com o Azure).  

Olá `useradd` comando for concluído Olá tarefas a seguir:

* Criar uma nova conta de usuário
* criar um novo grupo de usuários com hello mesmo nome
* Adicionar uma entrada em branco muito`/etc/passwd`
* Adicionar uma entrada em branco muito`/etc/gpasswd`

Olá `-G` sinalizador de linha de comando adiciona Olá novo usuário conta toohello adequado Linux grupo dando a nova conta de usuário Olá privilégios de escalonamento de raiz.

#### <a name="add-hello-user"></a>Adicionar usuário Olá
```bash
# On RedHat family distros
sudo useradd -G wheel exampleUser

# On Debian family distros
sudo useradd -G sudo exampleUser
```

#### <a name="set-a-password"></a>Definir uma senha
Olá `useradd` comando cria o usuário hello e adiciona uma entrada tooboth `/etc/passwd` e `/etc/gpasswd` , mas não definem senha hello.  Olá senha é toohello entrada adicionada usando Olá `passwd` comando.

```bash
sudo passwd exampleUser
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```

Agora temos um usuário com privilégios de sudo no servidor de saudação.

### <a name="add-your-ssh-public-key-toohello-new-user-account"></a>Adicione sua chave pública SSH toohello nova conta de usuário
Em seu computador, use Olá `ssh-copy-id` comando com a nova senha hello.

```bash
ssh-copy-id -i ~/.ssh/id_rsa exampleuser@exampleserver
```

### <a name="using-visudo-tooallow-sudo-usage-without-a-password"></a>Usando visudo tooallow sudo uso sem uma senha
Usando `visudo` tooedit Olá `/etc/sudoers` arquivo adiciona alguns camadas de proteção contra incorretamente modificar esse arquivo importante.  Após a execução `visudo`, Olá `/etc/sudoers` arquivo está bloqueado tooensure nenhum outro usuário pode fazer alterações enquanto ela está sendo editada ativamente.  Olá `/etc/sudoers` arquivo também é verificado quanto a erros por `visudo` quando você tentar toosave ou sair e não é possível salvar um arquivo sudoers quebrada.

Já temos os usuários no grupo de padrão correto Olá para sudo acesso.  Agora, vamos tooenable esses grupos toouse sudo com e sem senha.

```bash
# Execute visudo as root tooedit hello /etc/sudoers file
visudo

# On RedHat family distros uncomment this line:
## Same thing without a password
# %wheel        ALL=(ALL)       NOPASSWD: ALL

# toothis
## Same thing without a password
%wheel        ALL=(ALL)       NOPASSWD: ALL

# On Debian family distros change this line:
# Allow members of group sudo tooexecute any command
%sudo   ALL=(ALL:ALL) ALL

# toothis
%sudo   ALL=(ALL) NOPASSWD:ALL
```

### <a name="verify-hello-user-ssh-keys-and-sudo"></a>Verifique se o usuário hello, ssh chaves e sudo
```bash
# Verify hello SSH keys & User account
ssh -i ~/.ssh/id_rsa exampleuser@exampleserver

# Verify sudo access
sudo top
```
