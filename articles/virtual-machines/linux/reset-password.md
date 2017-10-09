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
ms.openlocfilehash: b28a679a36bf93c6881633eefa03aef3cd33e804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a><span data-ttu-id="8227b-103">Como tooreset local Linux senha em VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="8227b-103">How tooreset local Linux password on Azure VMs</span></span>

<span data-ttu-id="8227b-104">Este artigo apresenta vários métodos tooreset Linux Máquina Virtual (VM) as senhas locais.</span><span class="sxs-lookup"><span data-stu-id="8227b-104">This article introduces several methods tooreset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="8227b-105">Se a conta de usuário de saudação expirou ou você quiser apenas toocreate uma nova conta, você pode usar Olá métodos toocreate uma nova conta de administrador local a seguir e obter novamente acesso toohello VM.</span><span class="sxs-lookup"><span data-stu-id="8227b-105">If hello user account is expired or you just want toocreate a new account, you can use hello following methods toocreate a new local admin account and re-gain access toohello VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="8227b-106">Sintomas</span><span class="sxs-lookup"><span data-stu-id="8227b-106">Symptoms</span></span>

<span data-ttu-id="8227b-107">Você não pode fazer logon no toohello VM e você receberá uma mensagem que indica que você usou Olá senha está incorreta.</span><span class="sxs-lookup"><span data-stu-id="8227b-107">You can't log in toohello VM, and you receive a message that indicates that hello password that you used is incorrect.</span></span> <span data-ttu-id="8227b-108">Além disso, você não pode usar VMAgent tooreset sua senha Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8227b-108">Additionally, you can't use VMAgent tooreset your password on hello Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="8227b-109">Procedimento de Redefinição de Senha Manual</span><span class="sxs-lookup"><span data-stu-id="8227b-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="8227b-110">Excluir Olá VM e manter discos Olá anexado.</span><span class="sxs-lookup"><span data-stu-id="8227b-110">Delete hello VM and keep hello attached disks.</span></span>

2.  <span data-ttu-id="8227b-111">Anexar Olá unidade do sistema operacional como um tooanother de disco de dados temporal VM Olá mesmo local.</span><span class="sxs-lookup"><span data-stu-id="8227b-111">Attach hello OS Drive as a data disk tooanother temporal VM in hello same location.</span></span>

3.  <span data-ttu-id="8227b-112">Execute Olá a seguir do comando SSH Olá temporal VM toobecome superusuário.</span><span class="sxs-lookup"><span data-stu-id="8227b-112">Run hello following SSH command on hello temporal VM toobecome a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="8227b-113">Executar **fdisk -l** ou examinar saudação do sistema logs toofind disco anexado recentemente.</span><span class="sxs-lookup"><span data-stu-id="8227b-113">Run **fdisk -l** or look at system logs toofind hello newly attached disk.</span></span> <span data-ttu-id="8227b-114">Localize Olá toomount de nome de unidade.</span><span class="sxs-lookup"><span data-stu-id="8227b-114">Locate hello drive name toomount.</span></span> <span data-ttu-id="8227b-115">Em seguida, em Olá VM temporal, examinar Olá relevante arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="8227b-115">Then on hello temporal VM, look in hello relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="8227b-116">a seguir Olá é exemplo de saída do comando de grep hello:</span><span class="sxs-lookup"><span data-stu-id="8227b-116">hello following is example output of hello grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="8227b-117">Crie um ponto de montagem chamado **tempmount**.</span><span class="sxs-lookup"><span data-stu-id="8227b-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="8227b-118">Monte o disco de saudação sistema operacional no ponto de montagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="8227b-118">Mount hello OS disk on hello mount point.</span></span> <span data-ttu-id="8227b-119">Normalmente, você precisa toomount sdc1 ou sdc2.</span><span class="sxs-lookup"><span data-stu-id="8227b-119">You usually need toomount sdc1 or sdc2.</span></span> <span data-ttu-id="8227b-120">Isso dependerá Olá hospedando partição no diretório /etc. do disco de máquina quebrada hello.</span><span class="sxs-lookup"><span data-stu-id="8227b-120">This will depend on hello hosting partition in /etc directory from hello broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="8227b-121">Execute um backup antes de fazer as alterações:</span><span class="sxs-lookup"><span data-stu-id="8227b-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="8227b-122">Redefina senha do usuário Olá que você precisa:</span><span class="sxs-lookup"><span data-stu-id="8227b-122">Reset hello user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="8227b-123">Mover Olá modificado arquivos toohello local correto Olá dividido disco da máquina.</span><span class="sxs-lookup"><span data-stu-id="8227b-123">Move hello modified files toohello correct location on hello broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    <span data-ttu-id="8227b-124">cd / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="8227b-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)
