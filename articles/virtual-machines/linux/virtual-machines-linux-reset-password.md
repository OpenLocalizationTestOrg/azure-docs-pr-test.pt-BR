---
title: aaaHow tooreset Linux senha local nas VMs do Azure | Microsoft Docs
description: "Introduzir Olá etapas tooreset Olá Linux senha local na VM do Azure"
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: delhan
ms.openlocfilehash: 3827e32186c5f034d9bb6fc502dc26708b52a00a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a>Como tooreset local Linux senha em VMs do Azure

Este artigo apresenta vários métodos tooreset Linux Máquina Virtual (VM) as senhas locais. Se a conta de usuário de saudação expirou ou você quiser apenas toocreate uma nova conta, você pode usar Olá métodos toocreate uma nova conta de administrador local a seguir e obter novamente acesso toohello VM.

## <a name="symptoms"></a>Sintomas

Você não pode fazer logon no toohello VM e você receberá uma mensagem que indica que você usou Olá senha está incorreta. Além disso, você não pode usar VMAgent tooreset sua senha Olá Portal do Azure. 

## <a name="manual-password-reset-procedure"></a>Procedimento de Redefinição de Senha Manual

1.  Excluir Olá VM e manter discos Olá anexado.

2.  Anexar Olá unidade do sistema operacional como um tooanother de disco de dados temporal VM Olá mesmo local.

3.  Execute Olá a seguir do comando SSH Olá temporal VM toobecome superusuário.


    ~~~~
    sudo su
    ~~~~

4.  Executar **fdisk -l** ou examinar saudação do sistema logs toofind disco anexado recentemente. Localize Olá toomount de nome de unidade. Em seguida, em Olá VM temporal, examinar Olá relevante arquivo de log.

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    a seguir Olá é exemplo de saída do comando de grep hello:

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  Crie um ponto de montagem chamado **tempmount**.

    ~~~~
    mkdir /tempmount
    ~~~~

6.  Monte o disco de saudação sistema operacional no ponto de montagem de saudação. Normalmente, você precisa toomount sdc1 ou sdc2. Isso dependerá Olá hospedando partição no diretório /etc. do disco de máquina quebrada hello.

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  Execute um backup antes de fazer as alterações:

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  Redefina senha do usuário Olá que você precisa:

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  Mover Olá modificado arquivos toohello local correto Olá dividido disco da máquina.

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    cd / umount /tempmount
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
