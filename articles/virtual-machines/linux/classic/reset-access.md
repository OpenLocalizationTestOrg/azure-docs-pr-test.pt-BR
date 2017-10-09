---
title: "aaaReset senha de VM do Linux e SSH chave da saudação CLI | Microsoft Docs"
description: "Como toouse Olá extensão VMAccess de saudação do Azure Interface de linha de comando (CLI) tooreset uma senha de VM do Linux ou uma chave SSH, corrija a configuração de SSH hello e verificar a consistência de disco"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a>Como tooreset uma senha de VM do Linux ou chave SSH, corrija a configuração de SSH hello e verificar a consistência de disco usando a extensão VMAccess Olá
Se você não pode se conectar a máquina virtual do tooa Linux no Azure devido a uma senha esquecida, uma chave do Secure Shell (SSH) incorreto ou um problema com a configuração de SSH hello, usar Olá extensão VMAccessForLinux com hello CLI do Azure tooreset Olá senha ou chave SSH, corrigir Olá configuração de SSH e verificar a consistência de disco. 

> [!IMPORTANT] 
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Saiba como muito[executar essas etapas usando o modelo do Gerenciador de recursos de saudação](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).

Com hello CLI do Azure, você usar Olá **conjunto de extensão de vm do azure** comando comandos de tooaccess sua interface de linha de comando (Bash, Terminal, prompt de comando). Execute **azure help vm extension set** para ver o uso detalhado da extensão.

Com hello CLI do Azure, você pode fazer Olá seguintes tarefas:

* [Redefinir senha Olá](#pwresetcli)
* [Redefinir a chave SSH Olá](#sshkeyresetcli)
* [Redefinir a chave SSH de senha e Olá Olá](#resetbothcli)
* [Criar uma nova conta de usuário sudo](#createnewsudocli)
* [Redefinir a configuração de SSH Olá](#sshconfigresetcli)
* [Excluir um usuário](#deletecli)
* [Exibir status Olá Olá extensão VMAccess](#statuscli)
* [Verificar a consistência dos discos adicionados](#checkdisk)
* [Reparar discos adicionados na sua VM do Linux](#repairdisk)

## <a name="prerequisites"></a>Pré-requisitos
Você precisará a seguir Olá toodo:

* Você precisará de muito[instalar Olá CLI do Azure](../../../cli-install-nodejs.md) e [conectar assinatura tooyour](../../../xplat-cli-connect.md) toouse Azure recursos associados à sua conta.
* Conjunto Olá modo correto para modelo de implantação clássico Olá digitando o seguinte Olá no prompt de comando hello:
    ``` 
        azure config mode asm
    ```
* Tem uma nova senha ou um conjunto de chaves SSH, se você quiser tooreset qualquer um. Você não precisa dessas se desejar que a configuração de SSH tooreset hello.

## <a name="pwresetcli"></a>Redefinir senha Olá
1. Crie um arquivo no seu computador local chamado PrivateConf.json com essas linhas. Substitua **myUserName** e **myP@ssW0rd** pelo seu próprio nome de usuário e senha e defina sua própria data de expiração.

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. Execute este comando, substituindo Olá nome da máquina virtual para **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <a name="sshkeyresetcli"></a>Redefinir a chave SSH Olá
1. Crie um arquivo chamado PrivateConf.json com esse conteúdo. Substituir saudação **myUserName** e **mySSHKey** valores com suas próprias informações.

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. Execute este comando, substituindo Olá nome da máquina virtual para **myVM**.
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <a name="resetbothcli"></a>Redefinir senha hello e a chave SSH Olá
1. Crie um arquivo chamado PrivateConf.json com esse conteúdo. Substituir saudação **myUserName**, **mySSHKey** e  **myP@ssW0rd**  valores com suas próprias informações.

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. Execute este comando, substituindo Olá nome da máquina virtual para **myVM**.

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="createnewsudocli"></a>Criar uma nova conta de usuário sudo

Se você esquecer o nome de usuário, você pode usar VMAccess toocreate um novo com a autoridade de sudo hello. Olá nesse caso, o nome de usuário e senha não será modificada.

toocreate um novo usuário sudo com acesso de senha, use script de saudação em [redefinição da senha Olá](#pwresetcli) e especifique o novo nome de usuário hello.

toocreate um novo usuário sudo com acesso de chave SSH, usar o script de saudação em [chave SSH Olá redefinição](#sshkeyresetcli) e especifique o novo nome de usuário hello.

Você também pode usar [Redefinir senha hello e a chave SSH Olá](#resetbothcli) toocreate um novo usuário com senha e o acesso à chave de SSH.

## <a name="sshconfigresetcli"></a>Redefinir a configuração de SSH Olá
Se a configuração de SSH hello está em um estado indesejado, você também poderá perder acesso toohello VM. Você pode usar o hello VMAccess extensão tooreset Olá configuração tooits estado padrão. toodo assim, você apenas precisa tooset hello "reset_ssh" chave muito "True". extensão Olá reiniciar o servidor SSH Olá, abra a porta na sua VM SSH Olá e redefinir Olá SSH configuração toodefault valores. conta de usuário da saudação (nome, a senha ou as chaves de SSH) não será alterada.

> [!NOTE]
> arquivo de configuração do SSH Olá é redefinido está localizado em /etc/ssh/sshd_config.
> 
> 

1. Crie um arquivo chamado PrivateConf.json com esse conteúdo.

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. Execute este comando, substituindo Olá nome da máquina virtual para **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="deletecli"></a>Excluir um usuário
Se você quiser toodelete uma conta de usuário sem efetuar login no toohello VM diretamente, você pode usar esse script.

1. Crie um arquivo chamado PrivateConf.json com esse conteúdo, substituindo Olá tooremove de nome de usuário para **removeUserName**. 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. Execute este comando, substituindo Olá nome da máquina virtual para **myVM**. 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="statuscli"></a>Exibir status Olá Olá extensão VMAccess
status toodisplay Olá Olá extensão VMAccess, execute este comando.

```
        azure vm extension get
```

## <a name='checkdisk'></a>Verificar a consistência dos discos adicionados
toorun fsck em todos os discos em sua máquina virtual do Linux, você precisará a seguir Olá toodo:

1. Crie um arquivo chamado PublicConf.json com esse conteúdo. Verificar disco tem um valor booleano para se toocheck discos anexados a máquina virtual de tooyour ou não. 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. Executar tooexecute esse comando, substituindo Olá nome da máquina virtual para **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <a name='repairdisk'></a>Reparar discos
discos toorepair não montar ou que possuem erros de configuração de montagem, use Olá VMAccess tooreset Olá montagem configuração da extensão na sua máquina virtual do Linux. Substituindo o nome de saudação do disco para **myDisk**.

1. Crie um arquivo chamado PublicConf.json com esse conteúdo. 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. Executar tooexecute esse comando, substituindo Olá nome da máquina virtual para **myVM**.

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a>Próximas etapas
* Se você quiser toouse cmdlets do PowerShell do Azure ou a senha do Gerenciador de recursos do Azure modelos tooreset hello ou a chave SSH, corrija a configuração de SSH Olá e verificar a consistência de disco, consulte Olá [documentação de extensão VMAccess no GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess). 
* Você também pode usar o hello [portal do Azure](https://portal.azure.com) tooreset senha de saudação ou chave SSH de uma VM do Linux implantadas no modelo de implantação clássico hello. No momento, você não pode usar saudação portal toothis para uma VM do Linux é implantado no modelo de implantação do Gerenciador de recursos de saudação.
* Veja [Sobre os recursos e extensões de máquina virtual](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obter mais informações sobre como usar extensões de VM para máquinas virtuais do Azure.

