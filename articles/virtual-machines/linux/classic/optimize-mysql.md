---
title: aaaOptimize desempenho do MySQL no Linux | Microsoft Docs
description: "Saiba como toooptimize MySQL em execução em uma máquina virtual do Azure (VM) executando o Linux."
services: virtual-machines-linux
documentationcenter: 
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 0c1c7fc5-a528-4d84-b65d-2df225f2233f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: ningk
ms.openlocfilehash: 9e6458723233721e06f30b9de33635d403eefcba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-mysql-performance-on-azure-linux-vms"></a><span data-ttu-id="5170d-103">Otimizar o desempenho do MySQL em VMs Linux do Azure</span><span class="sxs-lookup"><span data-stu-id="5170d-103">Optimize MySQL Performance on Azure Linux VMs</span></span>
<span data-ttu-id="5170d-104">Há muitos fatores que afetam o desempenho do MySQL no Azure, tanto na configuração de software como na seleção de hardware virtual.</span><span class="sxs-lookup"><span data-stu-id="5170d-104">There are many factors that affect MySQL performance on Azure, both in virtual hardware selection and software configuration.</span></span> <span data-ttu-id="5170d-105">Este artigo se concentra na otimização de desempenho por meio de armazenamento, sistema e configurações de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5170d-105">This article focuses on optimizing performance through storage, system, and database configurations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5170d-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Azure Resource Manager](../../../resource-manager-deployment-model.md) e clássico.</span><span class="sxs-lookup"><span data-stu-id="5170d-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager](../../../resource-manager-deployment-model.md) and classic.</span></span> <span data-ttu-id="5170d-107">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="5170d-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="5170d-108">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="5170d-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="5170d-109">Para obter informações sobre as otimizações de VM do Linux com o modelo do Gerenciador de recursos de hello, consulte [otimizar sua VM do Linux no Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5170d-109">For information about Linux VM optimizations with hello Resource Manager model, see [Optimize your Linux VM on Azure](../optimization.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="utilize-raid-on-an-azure-virtual-machine"></a><span data-ttu-id="5170d-110">Utilizar RAID em uma máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="5170d-110">Utilize RAID on an Azure virtual machine</span></span>
<span data-ttu-id="5170d-111">O armazenamento é um fator-chave Olá que afeta o desempenho do banco de dados em ambientes de nuvem.</span><span class="sxs-lookup"><span data-stu-id="5170d-111">Storage is hello key factor that affects database performance in cloud environments.</span></span> <span data-ttu-id="5170d-112">Tooa em comparação com o único disco, RAID pode fornecer acesso mais rápido por meio de simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="5170d-112">Compared tooa single disk, RAID can provide faster access via concurrency.</span></span> <span data-ttu-id="5170d-113">Para obter mais informações, consulte [Níveis de RAID padrão](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span><span class="sxs-lookup"><span data-stu-id="5170d-113">For more information, see [Standard RAID levels](http://en.wikipedia.org/wiki/Standard_RAID_levels).</span></span>   

<span data-ttu-id="5170d-114">A taxa de transferência de E/S de disco e o tempo de resposta de E/S no Azure podem ser melhorados significativamente com o RAID.</span><span class="sxs-lookup"><span data-stu-id="5170d-114">Disk I/O throughput and I/O response time in Azure can be improved through RAID.</span></span> <span data-ttu-id="5170d-115">Nossos testes de laboratório mostram que a taxa de transferência de e/s de disco pode ser duplicada e tempo de resposta de e/s pode ser reduzido pela metade em média quando o número de saudação de discos RAID é duplicado (de toofour duas, quatro tooeight, etc.).</span><span class="sxs-lookup"><span data-stu-id="5170d-115">Our lab tests show that disk I/O throughput can be doubled and I/O response time can be reduced by half on average when hello number of RAID disks is doubled (from two toofour, four tooeight, etc.).</span></span> <span data-ttu-id="5170d-116">Confira o [Apêndice A](#AppendixA) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="5170d-116">See [Appendix A](#AppendixA) for details.</span></span>  

<span data-ttu-id="5170d-117">Além de e/s toodisk, desempenho do MySQL melhora quando você aumenta o nível de RAID de saudação.</span><span class="sxs-lookup"><span data-stu-id="5170d-117">In addition toodisk I/O, MySQL performance improves when you increase hello RAID level.</span></span>  <span data-ttu-id="5170d-118">Confira o [Apêndice B](#AppendixB) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="5170d-118">See [Appendix B](#AppendixB) for details.</span></span>  

<span data-ttu-id="5170d-119">Você também poderá tamanho da parte tooconsider hello.</span><span class="sxs-lookup"><span data-stu-id="5170d-119">You might also want tooconsider hello chunk size.</span></span> <span data-ttu-id="5170d-120">Em geral, quando você tem um grande parte, haverá uma sobrecarga mais baixa, especialmente para grandes gravações.</span><span class="sxs-lookup"><span data-stu-id="5170d-120">In general, when you have a larger chunk size, you get lower overhead, especially for large writes.</span></span> <span data-ttu-id="5170d-121">No entanto, quando o tamanho da parte Olá é muito grande, pode adicionar uma sobrecarga adicional que impede que você aproveite o RAID.</span><span class="sxs-lookup"><span data-stu-id="5170d-121">However, when hello chunk size is too large, it might add additional overhead that prevents you from taking advantage of RAID.</span></span> <span data-ttu-id="5170d-122">tamanho padrão atual de saudação é 512 KB, que é aprovada toobe ideal para ambientes de produção mais gerais.</span><span class="sxs-lookup"><span data-stu-id="5170d-122">hello current default size is 512 KB, which is proven toobe optimal for most general production environments.</span></span> <span data-ttu-id="5170d-123">Confira o [Apêndice C](#AppendixC) para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="5170d-123">See [Appendix C](#AppendixC) for details.</span></span>   

<span data-ttu-id="5170d-124">Há limites para quantos discos você pode adicionar para diferentes tipos de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="5170d-124">There are limits on how many disks you can add for different virtual machine types.</span></span> <span data-ttu-id="5170d-125">Esses limites são detalhados em [Tamanhos de máquinas virtuais e serviço de nuvem para o Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="5170d-125">These limits are detailed in [Virtual machine and cloud service sizes for Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span> <span data-ttu-id="5170d-126">Você precisará de quatro dados anexados discos toofollow Olá RAID exemplos neste artigo, embora você possa escolher tooset RAID com menos discos.</span><span class="sxs-lookup"><span data-stu-id="5170d-126">You will need four attached data disks toofollow hello RAID example in this article, although you can choose tooset up RAID with fewer disks.</span></span>  

<span data-ttu-id="5170d-127">Este artigo pressupõe que você já criou uma máquina virtual Linux e já tenha o MYSQL instalado e configurado.</span><span class="sxs-lookup"><span data-stu-id="5170d-127">This article assumes you have already created a Linux virtual machine and have MYSQL installed and configured.</span></span> <span data-ttu-id="5170d-128">Para obter mais informações sobre como começar, consulte como tooinstall MySQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="5170d-128">For more information on getting started, see How tooinstall MySQL on Azure.</span></span>  

### <a name="set-up-raid-on-azure"></a><span data-ttu-id="5170d-129">Configurar o RAID no Azure</span><span class="sxs-lookup"><span data-stu-id="5170d-129">Set up RAID on Azure</span></span>
<span data-ttu-id="5170d-130">Olá etapas a seguir mostram como toocreate RAID no Azure usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5170d-130">hello following steps show how toocreate RAID on Azure by using hello Azure portal.</span></span> <span data-ttu-id="5170d-131">Você também pode configurar o RAID usando scripts do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5170d-131">You can also set up RAID by using Windows PowerShell scripts.</span></span>
<span data-ttu-id="5170d-132">Neste exemplo, configuraremos o RAID 0 com quatro discos.</span><span class="sxs-lookup"><span data-stu-id="5170d-132">In this example, we will configure RAID 0 with four disks.</span></span>  

#### <a name="add-a-data-disk-tooyour-virtual-machine"></a><span data-ttu-id="5170d-133">Adicionar uma máquina virtual de tooyour de disco de dados</span><span class="sxs-lookup"><span data-stu-id="5170d-133">Add a data disk tooyour virtual machine</span></span>
<span data-ttu-id="5170d-134">No hello portal do Azure, vá toohello painel e selecione Olá toowhich de máquina virtual você deseja tooadd um disco de dados.</span><span class="sxs-lookup"><span data-stu-id="5170d-134">In hello Azure portal, go toohello dashboard and select hello virtual machine toowhich you want tooadd a data disk.</span></span> <span data-ttu-id="5170d-135">Neste exemplo, a máquina virtual de saudação é mysqlnode1.</span><span class="sxs-lookup"><span data-stu-id="5170d-135">In this example, hello virtual machine is mysqlnode1.</span></span>  

<!--![Virtual machines][1]-->

<span data-ttu-id="5170d-136">Clique em **Discos** e depois em **Anexar Novo**.</span><span class="sxs-lookup"><span data-stu-id="5170d-136">Click **Disks** and then click **Attach New**.</span></span>

![Máquinas virtuais - adicionar disco](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-Disks-option.png)

<span data-ttu-id="5170d-138">Crie um novo disco de 500 GB.</span><span class="sxs-lookup"><span data-stu-id="5170d-138">Create a new 500 GB disk.</span></span> <span data-ttu-id="5170d-139">Verifique se **preferência de Cache do Host** está definido muito**nenhum**.</span><span class="sxs-lookup"><span data-stu-id="5170d-139">Make sure that **Host Cache Preference** is set too**None**.</span></span>  <span data-ttu-id="5170d-140">Quando tiver terminado, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="5170d-140">When you're finished, click **OK**.</span></span>

![Anexar disco vazio](media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-attach-empty-disk.png)


<span data-ttu-id="5170d-142">Isso adiciona um disco vazio à sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5170d-142">This adds one empty disk into your virtual machine.</span></span> <span data-ttu-id="5170d-143">Repita essa etapa mais três vezes para que você tenha quatro discos de dados para o RAID.</span><span class="sxs-lookup"><span data-stu-id="5170d-143">Repeat this step three more times so that you have four data disks for RAID.</span></span>  

<span data-ttu-id="5170d-144">Você pode ver Olá adicionado unidades na máquina virtual de saudação examinando o log de mensagens do kernel hello.</span><span class="sxs-lookup"><span data-stu-id="5170d-144">You can see hello added drives in hello virtual machine by looking at hello kernel message log.</span></span> <span data-ttu-id="5170d-145">Por exemplo, toosee isso no Ubuntu, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5170d-145">For example, toosee this on Ubuntu, use hello following command:</span></span>  

    sudo grep SCSI /var/log/dmesg

#### <a name="create-raid-with-hello-additional-disks"></a><span data-ttu-id="5170d-146">Criar RAID com hello discos adicionais</span><span class="sxs-lookup"><span data-stu-id="5170d-146">Create RAID with hello additional disks</span></span>
<span data-ttu-id="5170d-147">Olá etapas a seguir descrevem como muito[configurar software RAID no Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5170d-147">hello following steps describe how too[configure software RAID on Linux](../configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="5170d-148">Se você estiver usando o sistema de arquivos XFS hello, execute Olá etapas a seguir depois que você criou RAID.</span><span class="sxs-lookup"><span data-stu-id="5170d-148">If you are using hello XFS file system, execute hello following steps after you have created RAID.</span></span>
>
>

<span data-ttu-id="5170d-149">tooinstall XFS no Debian, Ubuntu ou Menta Linux, Olá use comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5170d-149">tooinstall XFS on Debian, Ubuntu, or Linux Mint, use hello following command:</span></span>  

    apt-get -y install xfsprogs  

<span data-ttu-id="5170d-150">tooinstall XFS em Fedora, CentOS ou RHEL, Olá use comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5170d-150">tooinstall XFS on Fedora, CentOS, or RHEL, use hello following command:</span></span>  

    yum -y install xfsprogs  xfsdump


#### <a name="set-up-a-new-storage-path"></a><span data-ttu-id="5170d-151">Configurar um novo caminho de armazenamento</span><span class="sxs-lookup"><span data-stu-id="5170d-151">Set up a new storage path</span></span>
<span data-ttu-id="5170d-152">Use Olá comando tooset um novo caminho de armazenamento a seguir:</span><span class="sxs-lookup"><span data-stu-id="5170d-152">Use hello following command tooset up a new storage path:</span></span>  

    root@mysqlnode1:~# mkdir -p /RAID0/mysql

#### <a name="copy-hello-original-data-toohello-new-storage-path"></a><span data-ttu-id="5170d-153">Copiar Olá original dados toohello novo caminho de armazenamento</span><span class="sxs-lookup"><span data-stu-id="5170d-153">Copy hello original data toohello new storage path</span></span>
<span data-ttu-id="5170d-154">Use Olá comando toocopy dados toohello novo caminho de armazenamento a seguir:</span><span class="sxs-lookup"><span data-stu-id="5170d-154">Use hello following command toocopy data toohello new storage path:</span></span>  

    root@mysqlnode1:~# cp -rp /var/lib/mysql/* /RAID0/mysql/

#### <a name="modify-permissions-so-mysql-can-access-read-and-write-hello-data-disk"></a><span data-ttu-id="5170d-155">Modificar permissões para que possa acessar MySQL (leitura e gravação) em disco de dados Olá</span><span class="sxs-lookup"><span data-stu-id="5170d-155">Modify permissions so MySQL can access (read and write) hello data disk</span></span>
<span data-ttu-id="5170d-156">Olá Use as seguintes permissões de toomodify de comando:</span><span class="sxs-lookup"><span data-stu-id="5170d-156">Use hello following command toomodify permissions:</span></span>  

    root@mysqlnode1:~# chown -R mysql.mysql /RAID0/mysql && chmod -R 755 /RAID0/mysql


## <a name="adjust-hello-disk-io-scheduling-algorithm"></a><span data-ttu-id="5170d-157">Olá e/s disco agendando o algoritmo de ajuste</span><span class="sxs-lookup"><span data-stu-id="5170d-157">Adjust hello disk I/O scheduling algorithm</span></span>
<span data-ttu-id="5170d-158">O Linux implementa quatro tipos de algoritmos de agendamento de e/s:</span><span class="sxs-lookup"><span data-stu-id="5170d-158">Linux implements four types of I/O scheduling algorithms:</span></span>  

* <span data-ttu-id="5170d-159">Algoritmo NOOP (nenhuma operação)</span><span class="sxs-lookup"><span data-stu-id="5170d-159">NOOP algorithm (No Operation)</span></span>
* <span data-ttu-id="5170d-160">Algoritmo de prazo (prazo)</span><span class="sxs-lookup"><span data-stu-id="5170d-160">Deadline algorithm (Deadline)</span></span>
* <span data-ttu-id="5170d-161">Algoritmo de fila completamente justa (CFQ)</span><span class="sxs-lookup"><span data-stu-id="5170d-161">Completely fair queuing algorithm (CFQ)</span></span>
* <span data-ttu-id="5170d-162">Algoritmo de período de orçamento (antecipado)</span><span class="sxs-lookup"><span data-stu-id="5170d-162">Budget period algorithm (Anticipatory)</span></span>  

<span data-ttu-id="5170d-163">Você pode selecionar diferentes agendadores de e/s em desempenho de toooptimize cenários diferentes.</span><span class="sxs-lookup"><span data-stu-id="5170d-163">You can select different I/O schedulers under different scenarios toooptimize performance.</span></span> <span data-ttu-id="5170d-164">Em um ambiente de acesso aleatório completamente, não há uma diferença significativa entre hello CFQ e algoritmos de prazo para o desempenho.</span><span class="sxs-lookup"><span data-stu-id="5170d-164">In a completely random access environment, there is not a significant difference between hello CFQ and Deadline algorithms for performance.</span></span> <span data-ttu-id="5170d-165">É recomendável que você defina tooDeadline de ambiente de banco de dados Olá MySQL para estabilidade.</span><span class="sxs-lookup"><span data-stu-id="5170d-165">We recommend that you set hello MySQL database environment tooDeadline for stability.</span></span> <span data-ttu-id="5170d-166">Se houver muita E/S sequencial, o CFQ poderá reduzir o desempenho de E/S do disco.</span><span class="sxs-lookup"><span data-stu-id="5170d-166">If there is a lot of sequential I/O, CFQ might reduce disk I/O performance.</span></span>   

<span data-ttu-id="5170d-167">Para SSD e outros equipamentos, NOOP ou prazo pode alcançar desempenho melhor do que o Agendador de saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="5170d-167">For SSD and other equipment, NOOP or Deadline can achieve better performance than hello default scheduler.</span></span>   

<span data-ttu-id="5170d-168">Toohello anterior kernel 2.5, Olá padrão e/s agendamento algoritmo é prazo.</span><span class="sxs-lookup"><span data-stu-id="5170d-168">Prior toohello kernel 2.5, hello default I/O scheduling algorithm is Deadline.</span></span> <span data-ttu-id="5170d-169">A partir do kernel Olá 2.6.18, CFQ se tornou algoritmo de programação saudação padrão e/s.</span><span class="sxs-lookup"><span data-stu-id="5170d-169">Starting with hello kernel 2.6.18, CFQ became hello default I/O scheduling algorithm.</span></span>  <span data-ttu-id="5170d-170">Você pode especificar essa configuração no momento da inicialização do kernel ou dinamicamente modificar essa configuração quando o sistema hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="5170d-170">You can specify this setting at kernel boot time or dynamically modify this setting when hello system is running.</span></span>  

<span data-ttu-id="5170d-171">saudação de exemplo a seguir demonstra como toocheck e defina Olá algoritmo do padrão Agendador toohello NOOP na família de distribuição Debian hello.</span><span class="sxs-lookup"><span data-stu-id="5170d-171">hello following example demonstrates how toocheck and set hello default scheduler toohello NOOP algorithm in hello Debian distribution family.</span></span>  

### <a name="view-hello-current-io-scheduler"></a><span data-ttu-id="5170d-172">Agendador do modo de exibição Olá atual e/s</span><span class="sxs-lookup"><span data-stu-id="5170d-172">View hello current I/O scheduler</span></span>
<span data-ttu-id="5170d-173">tooview Olá Olá de Agendador executar comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5170d-173">tooview hello scheduler run hello following command:</span></span>  

    root@mysqlnode1:~# cat /sys/block/sda/queue/scheduler

<span data-ttu-id="5170d-174">Você verá a seguinte saída, que indica o Agendador de saudação atual:</span><span class="sxs-lookup"><span data-stu-id="5170d-174">You will see following output, which indicates hello current scheduler:</span></span>  

    noop [deadline] cfq


### <a name="change-hello-current-device-devsda-of-hello-io-scheduling-algorithm"></a><span data-ttu-id="5170d-175">Alterar Olá dispositivo (dev/sda) atual do algoritmo de programação hello e/s</span><span class="sxs-lookup"><span data-stu-id="5170d-175">Change hello current device (/dev/sda) of hello I/O scheduling algorithm</span></span>
<span data-ttu-id="5170d-176">Execute Olá dispositivo atual de saudação de toochange de comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5170d-176">Run hello following commands toochange hello current device:</span></span>  

    azureuser@mysqlnode1:~$ sudo su -
    root@mysqlnode1:~# echo "noop" >/sys/block/sda/queue/scheduler
    root@mysqlnode1:~# sed -i 's/GRUB_CMDLINE_LINUX=""/GRUB_CMDLINE_LINUX_DEFAULT="quiet splash elevator=noop"/g' /etc/default/grub
    root@mysqlnode1:~# update-grub

> [!NOTE]
> <span data-ttu-id="5170d-177">Configurar este somente para /dev/sda não é útil.</span><span class="sxs-lookup"><span data-stu-id="5170d-177">Setting this for /dev/sda alone is not useful.</span></span> <span data-ttu-id="5170d-178">Ele deve ser definido em todos os discos de dados onde reside o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5170d-178">It must be set on all data disks where hello database resides.</span></span>  
>
>

<span data-ttu-id="5170d-179">Você deve ver Olá saída a seguir, indicando que grub.cfg foi recriado com êxito e que o Agendador de saudação padrão tiver sido atualizada tooNOOP:</span><span class="sxs-lookup"><span data-stu-id="5170d-179">You should see hello following output, indicating that grub.cfg has been rebuilt successfully and that hello default scheduler has been updated tooNOOP:</span></span>  

    Generating grub configuration file ...
    Found linux image: /boot/vmlinuz-3.13.0-34-generic
    Found initrd image: /boot/initrd.img-3.13.0-34-generic
    Found linux image: /boot/vmlinuz-3.13.0-32-generic
    Found initrd image: /boot/initrd.img-3.13.0-32-generic
    Found memtest86+ image: /memtest86+.elf
    Found memtest86+ image: /memtest86+.bin
    done

<span data-ttu-id="5170d-180">Para Olá família de distribuição do Red Hat, você só precisa Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5170d-180">For hello Red Hat distribution family, you need only hello following command:</span></span>

    echo 'echo noop >/sys/block/sda/queue/scheduler' >> /etc/rc.local

## <a name="configure-system-file-operations-settings"></a><span data-ttu-id="5170d-181">Definir as configurações de operações de arquivos do sistema</span><span class="sxs-lookup"><span data-stu-id="5170d-181">Configure system file operations settings</span></span>
<span data-ttu-id="5170d-182">Uma prática recomendada é Olá toodisable *atime* recurso de log no sistema de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="5170d-182">One best practice is toodisable hello *atime* logging feature on hello file system.</span></span> <span data-ttu-id="5170d-183">Atime é o último tempo de acesso de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="5170d-183">Atime is hello last file access time.</span></span> <span data-ttu-id="5170d-184">Sempre que um arquivo é acessado, registros de sistema de arquivo Olá Olá carimbo de hora no log de saudação.</span><span class="sxs-lookup"><span data-stu-id="5170d-184">Whenever a file is accessed, hello file system records hello timestamp in hello log.</span></span> <span data-ttu-id="5170d-185">No entanto, essas informações raramente são usadas.</span><span class="sxs-lookup"><span data-stu-id="5170d-185">However, this information is rarely used.</span></span> <span data-ttu-id="5170d-186">Você pode desabilitá-lo se não precisar dele, o que reduzirá o tempo de acesso total do disco.</span><span class="sxs-lookup"><span data-stu-id="5170d-186">You can disable it if you don't need it, which will reduce overall disk access time.</span></span>  

<span data-ttu-id="5170d-187">toodisable atime log, você precisa toomodify Olá arquivo sistema configuração arquivo /etc/ fstab e adicionar Olá **noatime** opção.</span><span class="sxs-lookup"><span data-stu-id="5170d-187">toodisable atime logging, you need toomodify hello file system configuration file /etc/ fstab and add hello **noatime** option.</span></span>  

<span data-ttu-id="5170d-188">Por exemplo, edite o arquivo de /etc/fstab de vim do hello, adicionando noatime hello, conforme mostrado no hello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="5170d-188">For example, edit hello vim /etc/fstab file, adding hello noatime as shown in hello following sample:</span></span>  

    # CLOUD_IMG: This file was created/modified by hello Cloud Image build process
    UUID=3cc98c06-d649-432d-81df-6dcd2a584d41       /        ext4   defaults,discard        0 0
    #Add hello “noatime” option below toodisable atime logging
    UUID="431b1e78-8226-43ec-9460-514a9adf060e"     /RAID0   xfs   defaults,nobootwait, noatime 0 0
    /dev/sdb1       /mnt    auto    defaults,nobootwait,comment=cloudconfig 0       2

<span data-ttu-id="5170d-189">Em seguida, remonte o sistema de arquivos de saudação com hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5170d-189">Then, remount hello file system with hello following command:</span></span>  

    mount -o remount /RAID0

<span data-ttu-id="5170d-190">Saudação de teste modificado resultado.</span><span class="sxs-lookup"><span data-stu-id="5170d-190">Test hello modified result.</span></span> <span data-ttu-id="5170d-191">Quando você modifica o arquivo de teste hello, tempo de acesso de saudação não é atualizado.</span><span class="sxs-lookup"><span data-stu-id="5170d-191">When you modify hello test file, hello access time is not updated.</span></span> <span data-ttu-id="5170d-192">Olá seguintes exemplos mostram quais código Olá aparência antes e depois da modificação.</span><span class="sxs-lookup"><span data-stu-id="5170d-192">hello following examples show what hello code looks like before and after modification.</span></span>

<span data-ttu-id="5170d-193">Antes:</span><span class="sxs-lookup"><span data-stu-id="5170d-193">Before:</span></span>        

![Código antes da modificação de acesso][5]

<span data-ttu-id="5170d-195">Depois:</span><span class="sxs-lookup"><span data-stu-id="5170d-195">After:</span></span>

![Código depois da modificação de acesso][6]

## <a name="increase-hello-maximum-number-of-system-handles-for-high-concurrency"></a><span data-ttu-id="5170d-197">Aumentar o número máximo de saudação de identificadores do sistema de alta simultaneidade</span><span class="sxs-lookup"><span data-stu-id="5170d-197">Increase hello maximum number of system handles for high concurrency</span></span>
<span data-ttu-id="5170d-198">O MySQL é um banco de dados de alta simultaneidade.</span><span class="sxs-lookup"><span data-stu-id="5170d-198">MySQL is a high concurrency database.</span></span> <span data-ttu-id="5170d-199">número de identificadores simultâneas do Hello padrão é 1024 para Linux, que sempre não é suficiente.</span><span class="sxs-lookup"><span data-stu-id="5170d-199">hello default number of concurrent handles is 1024 for Linux, which is not always sufficient.</span></span> <span data-ttu-id="5170d-200">Use Olá seguindo as etapas tooincrease Olá máximo simultâneas identificadores de simultaneidade alta de toosupport do sistema de saudação do MySQL.</span><span class="sxs-lookup"><span data-stu-id="5170d-200">Use hello following steps tooincrease hello maximum concurrent handles of hello system toosupport high concurrency of MySQL.</span></span>

### <a name="modify-hello-limitsconf-file"></a><span data-ttu-id="5170d-201">Modificar o arquivo de limits.conf Olá</span><span class="sxs-lookup"><span data-stu-id="5170d-201">Modify hello limits.conf file</span></span>
<span data-ttu-id="5170d-202">tooincrease Olá máximo permitido identificadores simultâneas, adicione Olá quatro linhas no arquivo de /etc/security/limits.conf Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="5170d-202">tooincrease hello maximum allowed concurrent handles, add hello following four lines in hello /etc/security/limits.conf file.</span></span> <span data-ttu-id="5170d-203">Observe que 65536 é o número máximo de saudação que pode dar suporte a sistema de saudação.</span><span class="sxs-lookup"><span data-stu-id="5170d-203">Note that 65536 is hello maximum number that hello system can support.</span></span>   

    * <span data-ttu-id="5170d-204">soft nofile 65536</span><span class="sxs-lookup"><span data-stu-id="5170d-204">soft nofile 65536</span></span>
    * <span data-ttu-id="5170d-205">hard nofile 65536</span><span class="sxs-lookup"><span data-stu-id="5170d-205">hard nofile 65536</span></span>
    * <span data-ttu-id="5170d-206">soft nproc 65536</span><span class="sxs-lookup"><span data-stu-id="5170d-206">soft nproc 65536</span></span>
    * <span data-ttu-id="5170d-207">hard nproc 65536</span><span class="sxs-lookup"><span data-stu-id="5170d-207">hard nproc 65536</span></span>

### <a name="update-hello-system-for-hello-new-limits"></a><span data-ttu-id="5170d-208">Atualizar sistema Olá para novos limites de saudação</span><span class="sxs-lookup"><span data-stu-id="5170d-208">Update hello system for hello new limits</span></span>
<span data-ttu-id="5170d-209">sistema tooupdate hello, executar Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5170d-209">tooupdate hello system, run hello following commands:</span></span>  

    ulimit -SHn 65536
    ulimit -SHu 65536

### <a name="ensure-that-hello-limits-are-updated-at-boot-time"></a><span data-ttu-id="5170d-210">Certifique-se de que os limites de saudação são atualizados no momento da inicialização</span><span class="sxs-lookup"><span data-stu-id="5170d-210">Ensure that hello limits are updated at boot time</span></span>
<span data-ttu-id="5170d-211">Coloque Olá comandos de inicialização no arquivo de /etc/rc.local Olá a seguir para que ele entrará em vigor no momento da inicialização.</span><span class="sxs-lookup"><span data-stu-id="5170d-211">Put hello following startup commands in hello /etc/rc.local file so it will take effect at boot time.</span></span>  

    echo “ulimit -SHn 65536” >>/etc/rc.local
    echo “ulimit -SHu 65536” >>/etc/rc.local

## <a name="mysql-database-optimization"></a><span data-ttu-id="5170d-212">Otimização de banco de dados do MySQL</span><span class="sxs-lookup"><span data-stu-id="5170d-212">MySQL database optimization</span></span>
<span data-ttu-id="5170d-213">tooconfigure MySQL no Azure, você pode usar Olá a mesma estratégia de ajuste de desempenho você pode usar em uma máquina local.</span><span class="sxs-lookup"><span data-stu-id="5170d-213">tooconfigure MySQL on Azure, you can use hello same performance-tuning strategy you use on an on-premises machine.</span></span>  

<span data-ttu-id="5170d-214">Olá principais regras de otimização de e/s são:</span><span class="sxs-lookup"><span data-stu-id="5170d-214">hello main I/O optimization rules are:</span></span>   

* <span data-ttu-id="5170d-215">Aumente o tamanho do cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="5170d-215">Increase hello cache size.</span></span>
* <span data-ttu-id="5170d-216">Reduza o tempo de resposta de E/S.</span><span class="sxs-lookup"><span data-stu-id="5170d-216">Reduce I/O response time.</span></span>  

<span data-ttu-id="5170d-217">configurações do servidor MySQL toooptimize, você pode atualizar o arquivo my.cnf hello, o que é o arquivo de configuração saudação padrão para computadores cliente e servidor.</span><span class="sxs-lookup"><span data-stu-id="5170d-217">toooptimize MySQL server settings, you can update hello my.cnf file, which is hello default configuration file for both server and client computers.</span></span>  

<span data-ttu-id="5170d-218">Olá seguintes itens de configuração são fatores principais de saudação que afetam o desempenho do MySQL:</span><span class="sxs-lookup"><span data-stu-id="5170d-218">hello following configuration items are hello main factors that affect MySQL performance:</span></span>  

* <span data-ttu-id="5170d-219">**innodb_buffer_pool_size**: pool de buffers Olá contém dados armazenados em buffer e o índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="5170d-219">**innodb_buffer_pool_size**: hello buffer pool contains buffered data and hello index.</span></span> <span data-ttu-id="5170d-220">Isso geralmente é definido too70% da memória física.</span><span class="sxs-lookup"><span data-stu-id="5170d-220">This is usually set too70 percent of physical memory.</span></span>
* <span data-ttu-id="5170d-221">**innodb_log_file_size**: Este é o tamanho do log de refazer hello.</span><span class="sxs-lookup"><span data-stu-id="5170d-221">**innodb_log_file_size**: This is hello redo log size.</span></span> <span data-ttu-id="5170d-222">Use o tooensure de logs de refazer que operações de gravação são rápida, confiável e recuperável após uma falha.</span><span class="sxs-lookup"><span data-stu-id="5170d-222">You use redo logs tooensure that write operations are fast, reliable, and recoverable after a crash.</span></span> <span data-ttu-id="5170d-223">Isso é definido too512 MB, o que lhe dará bastante espaço para log de operações de gravação.</span><span class="sxs-lookup"><span data-stu-id="5170d-223">This is set too512 MB, which will give you plenty of space for logging write operations.</span></span>
* <span data-ttu-id="5170d-224">**max_connections**: às vezes, os aplicativos não fecham as conexões corretamente.</span><span class="sxs-lookup"><span data-stu-id="5170d-224">**max_connections**: Sometimes applications do not close connections properly.</span></span> <span data-ttu-id="5170d-225">Um valor maior dará servidor hello mais tempo toorecycle ociosos conexões.</span><span class="sxs-lookup"><span data-stu-id="5170d-225">A larger value will give hello server more time toorecycle idled connections.</span></span> <span data-ttu-id="5170d-226">Olá o número máximo de conexões é 10.000, mas Olá recomendado máximo é 5.000.</span><span class="sxs-lookup"><span data-stu-id="5170d-226">hello maximum number of connections is 10,000, but hello recommended maximum is 5,000.</span></span>
* <span data-ttu-id="5170d-227">**Innodb_file_per_table**: essa configuração habilita ou desabilita a capacidade de saudação de InnoDB toostore tabelas em arquivos separados.</span><span class="sxs-lookup"><span data-stu-id="5170d-227">**Innodb_file_per_table**: This setting enables or disables hello ability of InnoDB toostore tables in separate files.</span></span> <span data-ttu-id="5170d-228">Ative Olá opção tooensure que várias operações de administração avançados podem ser aplicadas com eficiência.</span><span class="sxs-lookup"><span data-stu-id="5170d-228">Turn on hello option tooensure that several advanced administration operations can be applied efficiently.</span></span> <span data-ttu-id="5170d-229">De um ponto de vista de desempenho, ele pode acelerar a transmissão de espaço de tabela hello e otimizar o desempenho de gerenciamento de resíduos hello.</span><span class="sxs-lookup"><span data-stu-id="5170d-229">From a performance point of view, it can speed up hello table space transmission and optimize hello debris management performance.</span></span> <span data-ttu-id="5170d-230">Olá recomendado configuração desta opção é ON.</span><span class="sxs-lookup"><span data-stu-id="5170d-230">hello recommended setting for this option is ON.</span></span></br></br>
<span data-ttu-id="5170d-231">Do MySQL 5.6, a configuração padrão de saudação for ON, portanto, nenhuma ação é necessária.</span><span class="sxs-lookup"><span data-stu-id="5170d-231">From MySQL 5.6, hello default setting is ON, so no action is required.</span></span> <span data-ttu-id="5170d-232">Para versões anteriores, a configuração padrão de saudação é OFF.</span><span class="sxs-lookup"><span data-stu-id="5170d-232">For earlier versions, hello default setting is OFF.</span></span> <span data-ttu-id="5170d-233">configuração de Olá deve ser alterada antes do carregamento de dados, porque somente tabelas recém-criadas são afetadas.</span><span class="sxs-lookup"><span data-stu-id="5170d-233">hello setting should be changed before data is loaded, because only newly created tables are affected.</span></span>
* <span data-ttu-id="5170d-234">**innodb_flush_log_at_trx_commit**: valor de padrão de saudação é 1, com hello escopo definido too0 ~ 2.</span><span class="sxs-lookup"><span data-stu-id="5170d-234">**innodb_flush_log_at_trx_commit**: hello default value is 1, with hello scope set too0~2.</span></span> <span data-ttu-id="5170d-235">valor padrão de saudação é a opção mais adequada Olá para o banco de dados MySQL.</span><span class="sxs-lookup"><span data-stu-id="5170d-235">hello default value is hello most suitable option for standalone MySQL DB.</span></span> <span data-ttu-id="5170d-236">configuração de saudação do 2 habilita o hello mais integridade de dados e é adequada para mestre no Cluster do MySQL.</span><span class="sxs-lookup"><span data-stu-id="5170d-236">hello setting of 2 enables hello most data integrity and is suitable for Master in MySQL Cluster.</span></span> <span data-ttu-id="5170d-237">configuração de Olá 0 permite que a perda de dados, que pode afetar a confiabilidade (em alguns casos com melhor desempenho) e é adequado para subordinado em MySQL Cluster.</span><span class="sxs-lookup"><span data-stu-id="5170d-237">hello setting of 0 allows data loss, which can affect reliability (in some cases with better performance), and is suitable for Slave in MySQL Cluster.</span></span>
* <span data-ttu-id="5170d-238">**Innodb_log_buffer_size**: o buffer de log Olá permite toorun transações sem ter que tooflush Olá log toodisk antes das transações são confirmadas hello.</span><span class="sxs-lookup"><span data-stu-id="5170d-238">**Innodb_log_buffer_size**: hello log buffer allows transactions toorun without having tooflush hello log toodisk before hello transactions commit.</span></span> <span data-ttu-id="5170d-239">No entanto, se houver objetos binários grandes ou campo de texto, cache hello será consumido rapidamente e e/s de disco frequentes será disparado.</span><span class="sxs-lookup"><span data-stu-id="5170d-239">However, if there is large binary object or text field, hello cache will be consumed quickly and frequent disk I/O will be triggered.</span></span> <span data-ttu-id="5170d-240">É melhor aumentar o tamanho do buffer de saudação se a variável de estado Innodb_log_waits não é 0.</span><span class="sxs-lookup"><span data-stu-id="5170d-240">It is better increase hello buffer size if Innodb_log_waits state variable is not 0.</span></span>
* <span data-ttu-id="5170d-241">**query_cache_size**: Olá melhor opção é toodisable-lo desde o início de saudação.</span><span class="sxs-lookup"><span data-stu-id="5170d-241">**query_cache_size**: hello best option is toodisable it from hello outset.</span></span> <span data-ttu-id="5170d-242">Defina too0 query_cache_size (Isso é configuração do padrão de saudação do MySQL 5.6) e use toospeed outros métodos as consultas.</span><span class="sxs-lookup"><span data-stu-id="5170d-242">Set query_cache_size too0 (this is hello default setting in MySQL 5.6) and use other methods toospeed up queries.</span></span>  

<span data-ttu-id="5170d-243">Consulte [Apêndice D](#AppendixD) para obter uma comparação de desempenho antes e depois da otimização de saudação.</span><span class="sxs-lookup"><span data-stu-id="5170d-243">See [Appendix D](#AppendixD) for a comparison of performance before and after hello optimization.</span></span>

## <a name="turn-on-hello-mysql-slow-query-log-for-analyzing-hello-performance-bottleneck"></a><span data-ttu-id="5170d-244">Ativar o log de consultas lentas Olá MySQL para analisar um afunilamento de desempenho Olá</span><span class="sxs-lookup"><span data-stu-id="5170d-244">Turn on hello MySQL slow query log for analyzing hello performance bottleneck</span></span>
<span data-ttu-id="5170d-245">log de consultas lentas MySQL Olá pode ajudar a identificar consultas lentas Olá para MySQL.</span><span class="sxs-lookup"><span data-stu-id="5170d-245">hello MySQL slow query log can help you identify hello slow queries for MySQL.</span></span> <span data-ttu-id="5170d-246">Depois de habilitar o log de consultas lentas Olá MySQL, você pode usar ferramentas de MySQL como **mysqldumpslow** tooidentify afunilamento de desempenho de saudação.</span><span class="sxs-lookup"><span data-stu-id="5170d-246">After enabling hello MySQL slow query log, you can use MySQL tools like **mysqldumpslow** tooidentify hello performance bottleneck.</span></span>  

<span data-ttu-id="5170d-247">Por padrão, isso não está habilitado.</span><span class="sxs-lookup"><span data-stu-id="5170d-247">By default, this is not enabled.</span></span> <span data-ttu-id="5170d-248">Ativar o log de consultas lentas hello, alguns recursos da CPU pode consumir.</span><span class="sxs-lookup"><span data-stu-id="5170d-248">Turning on hello slow query log might consume some CPU resources.</span></span> <span data-ttu-id="5170d-249">É recomendável que você habilite isso temporariamente para solucionar problemas de afunilamento de desempenho.</span><span class="sxs-lookup"><span data-stu-id="5170d-249">We recommend that you enable this temporarily for troubleshooting performance bottlenecks.</span></span> <span data-ttu-id="5170d-250">tooturn no log de consultas lentas hello:</span><span class="sxs-lookup"><span data-stu-id="5170d-250">tooturn on hello slow query log:</span></span>

1. <span data-ttu-id="5170d-251">Modifique o arquivo de my.cnf de saudação adicionando Olá final de toohello linhas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5170d-251">Modify hello my.cnf file by adding hello following lines toohello end:</span></span>

        long_query_time = 2
        slow_query_log = 1
        slow_query_log_file = /RAID0/mysql/mysql-slow.log

2. <span data-ttu-id="5170d-252">Reinicie o hello MySQL server.</span><span class="sxs-lookup"><span data-stu-id="5170d-252">Restart hello MySQL server.</span></span>

        service  mysql  restart

3. <span data-ttu-id="5170d-253">Verifique se configuração de saudação é entrar em vigor usando Olá **Mostrar** comando.</span><span class="sxs-lookup"><span data-stu-id="5170d-253">Check whether hello setting is taking effect by using hello **show** command.</span></span>

![Slow-query-log ON][7]   

![Slow-query-log results][8]

<span data-ttu-id="5170d-256">Neste exemplo, você pode ver que esse recurso de consultas lentas Olá foi ativado.</span><span class="sxs-lookup"><span data-stu-id="5170d-256">In this example, you can see that hello slow query feature has been turned on.</span></span> <span data-ttu-id="5170d-257">Você pode usar Olá **mysqldumpslow** ferramenta toodetermine afunilamentos de desempenho e otimizar o desempenho, como a adição de índices.</span><span class="sxs-lookup"><span data-stu-id="5170d-257">You can then use hello **mysqldumpslow** tool toodetermine performance bottlenecks and optimize performance, such as adding indexes.</span></span>

## <a name="appendices"></a><span data-ttu-id="5170d-258">Anexos</span><span class="sxs-lookup"><span data-stu-id="5170d-258">Appendices</span></span>
<span data-ttu-id="5170d-259">Olá seguem dados de teste de desempenho de amostra produzidos em um ambiente de laboratório de destino.</span><span class="sxs-lookup"><span data-stu-id="5170d-259">hello following are sample performance test data produced in a targeted lab environment.</span></span> <span data-ttu-id="5170d-260">Eles fornecem gerais sobre a tendência de dados de desempenho de saudação com diferente abordagens de ajuste de desempenho.</span><span class="sxs-lookup"><span data-stu-id="5170d-260">They provide general background on hello performance data trend with different performance tuning approaches.</span></span> <span data-ttu-id="5170d-261">Olá resultados poderão variar em versões diferentes do ambiente ou produto.</span><span class="sxs-lookup"><span data-stu-id="5170d-261">hello results might vary under different environment or product versions.</span></span>

### <span data-ttu-id="5170d-262"><a name="AppendixA"></a>Apêndice A</span><span class="sxs-lookup"><span data-stu-id="5170d-262"><a name="AppendixA"></a>Appendix A</span></span>  
<span data-ttu-id="5170d-263">**Desempenho de disco (IOPS) com diferentes níveis de RAID**</span><span class="sxs-lookup"><span data-stu-id="5170d-263">**Disk performance (IOPS) with different RAID levels**</span></span>

![IOPS de Disco com diferentes níveis de RAID][9]

<span data-ttu-id="5170d-265">**Comandos de teste**</span><span class="sxs-lookup"><span data-stu-id="5170d-265">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=5G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite

> [!NOTE]
> <span data-ttu-id="5170d-266">carga de trabalho Olá desse teste usa 64 threads, tentar tooreach Olá limite de RAID.</span><span class="sxs-lookup"><span data-stu-id="5170d-266">hello workload of this test uses 64 threads, trying tooreach hello upper limit of RAID.</span></span>
>
>

### <span data-ttu-id="5170d-267"><a name="AppendixB"></a>Apêndice B</span><span class="sxs-lookup"><span data-stu-id="5170d-267"><a name="AppendixB"></a>Appendix B</span></span>  
<span data-ttu-id="5170d-268">**Comparação de desempenho (taxa de transferência) do MySQL com diferentes níveis de RAID** </span><span class="sxs-lookup"><span data-stu-id="5170d-268">**MySQL performance (throughput) comparison with different RAID levels** </span></span>  
<span data-ttu-id="5170d-269">(sistema de arquivos XFS)</span><span class="sxs-lookup"><span data-stu-id="5170d-269">(XFS file system)</span></span>

![Comparação de desempenho do MySQL com diferentes níveis de RAID][10]  
![Comparação de desempenho do MySQL com diferentes níveis de RAID][11]

<span data-ttu-id="5170d-272">**Comandos de teste**</span><span class="sxs-lookup"><span data-stu-id="5170d-272">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb

<span data-ttu-id="5170d-273">**Comparação de desempenho (OLTP) do MySQL com diferentes níveis de RAID**</span><span class="sxs-lookup"><span data-stu-id="5170d-273">**MySQL performance (OLTP) comparison with different RAID levels**</span></span>  
<span data-ttu-id="5170d-274">![Comparação de desempenho (OLTP) do MySQL com diferentes níveis de RAID][12]</span><span class="sxs-lookup"><span data-stu-id="5170d-274">![MySQL performance (OLTP) comparison with different RAID levels][12]</span></span>

<span data-ttu-id="5170d-275">**Comandos de teste**</span><span class="sxs-lookup"><span data-stu-id="5170d-275">**Test commands**</span></span>

    time sysbench --test=oltp --db-driver=mysql --mysql-user=root --mysql-password=0ps.123  --mysql-table-engine=innodb --mysql-host=127.0.0.1 --mysql-port=3306 --mysql-socket=/var/run/mysqld/mysqld.sock --mysql-db=test --oltp-table-size=1000000 prepare

### <span data-ttu-id="5170d-276"><a name="AppendixC"></a>Apêndice C</span><span class="sxs-lookup"><span data-stu-id="5170d-276"><a name="AppendixC"></a>Appendix C</span></span>   
<span data-ttu-id="5170d-277">**Comparação de desempenho de disco (IOPS) para diferentes tamanhos de partes**</span><span class="sxs-lookup"><span data-stu-id="5170d-277">**Disk performance (IOPS) comparison for different chunk sizes**</span></span>  
<span data-ttu-id="5170d-278">(sistema de arquivos XFS)</span><span class="sxs-lookup"><span data-stu-id="5170d-278">(XFS file system)</span></span>

![][13]

<span data-ttu-id="5170d-279">**Comandos de teste**</span><span class="sxs-lookup"><span data-stu-id="5170d-279">**Test commands**</span></span>  

    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=30G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite
    fio -filename=/path/test -iodepth=64 -ioengine=libaio -direct=1 -rw=randwrite -bs=4k -size=1G -numjobs=64 -runtime=30 -group_reporting -name=test-randwrite  

<span data-ttu-id="5170d-280">tamanhos de arquivo Hello usados para este teste são 30 GB e 1 GB, respectivamente, com RAID 0 (4 discos) XFS do sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="5170d-280">hello file sizes used for this testing are 30 GB and 1 GB, respectively, with RAID 0 (4 disks) XFS file system.</span></span>

### <span data-ttu-id="5170d-281"><a name="AppendixD"></a>Apêndice D</span><span class="sxs-lookup"><span data-stu-id="5170d-281"><a name="AppendixD"></a>Appendix D</span></span>  
<span data-ttu-id="5170d-282">**Comparação de desempenho do MySQL (taxa de transferência) antes e depois da otimização**</span><span class="sxs-lookup"><span data-stu-id="5170d-282">**MySQL performance (throughput) comparison before and after optimization**</span></span>  
<span data-ttu-id="5170d-283">(sistema de arquivos XFS)</span><span class="sxs-lookup"><span data-stu-id="5170d-283">(XFS File System)</span></span>

![Comparação de desempenho do MySQL (taxa de transferência) antes e depois da otimização][14]

<span data-ttu-id="5170d-285">**Comandos de teste**</span><span class="sxs-lookup"><span data-stu-id="5170d-285">**Test commands**</span></span>

    mysqlslap -p0ps.123 --concurrency=2 --iterations=1 --number-int-cols=10 --number-char-cols=10 -a --auto-generate-sql-guid-primary --number-of-queries=10000 --auto-generate-sql-load-type=write –engine=innodb,misam

<span data-ttu-id="5170d-286">**Olá configuração padrão e a otimização é o seguinte:**</span><span class="sxs-lookup"><span data-stu-id="5170d-286">**hello configuration setting for default and optimization is as follows:**</span></span>

| <span data-ttu-id="5170d-287">parâmetros</span><span class="sxs-lookup"><span data-stu-id="5170d-287">Parameters</span></span> | <span data-ttu-id="5170d-288">Padrão</span><span class="sxs-lookup"><span data-stu-id="5170d-288">Default</span></span> | <span data-ttu-id="5170d-289">Otimização</span><span class="sxs-lookup"><span data-stu-id="5170d-289">Optimization</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5170d-290">**innodb_buffer_pool_size**</span><span class="sxs-lookup"><span data-stu-id="5170d-290">**innodb_buffer_pool_size**</span></span> |<span data-ttu-id="5170d-291">Nenhum</span><span class="sxs-lookup"><span data-stu-id="5170d-291">None</span></span> |<span data-ttu-id="5170d-292">7 GB</span><span class="sxs-lookup"><span data-stu-id="5170d-292">7 GB</span></span> |
| <span data-ttu-id="5170d-293">**innodb_log_file_size**</span><span class="sxs-lookup"><span data-stu-id="5170d-293">**innodb_log_file_size**</span></span> |<span data-ttu-id="5170d-294">5 MB</span><span class="sxs-lookup"><span data-stu-id="5170d-294">5 MB</span></span> |<span data-ttu-id="5170d-295">512 MB</span><span class="sxs-lookup"><span data-stu-id="5170d-295">512 MB</span></span> |
| <span data-ttu-id="5170d-296">**max_connections**</span><span class="sxs-lookup"><span data-stu-id="5170d-296">**max_connections**</span></span> |<span data-ttu-id="5170d-297">100</span><span class="sxs-lookup"><span data-stu-id="5170d-297">100</span></span> |<span data-ttu-id="5170d-298">5.000</span><span class="sxs-lookup"><span data-stu-id="5170d-298">5000</span></span> |
| <span data-ttu-id="5170d-299">**innodb_file_per_table**</span><span class="sxs-lookup"><span data-stu-id="5170d-299">**innodb_file_per_table**</span></span> |<span data-ttu-id="5170d-300">0</span><span class="sxs-lookup"><span data-stu-id="5170d-300">0</span></span> |<span data-ttu-id="5170d-301">1</span><span class="sxs-lookup"><span data-stu-id="5170d-301">1</span></span> |
| <span data-ttu-id="5170d-302">**innodb_flush_log_at_trx_commit**</span><span class="sxs-lookup"><span data-stu-id="5170d-302">**innodb_flush_log_at_trx_commit**</span></span> |<span data-ttu-id="5170d-303">1</span><span class="sxs-lookup"><span data-stu-id="5170d-303">1</span></span> |<span data-ttu-id="5170d-304">2</span><span class="sxs-lookup"><span data-stu-id="5170d-304">2</span></span> |
| <span data-ttu-id="5170d-305">**innodb_log_buffer_size**</span><span class="sxs-lookup"><span data-stu-id="5170d-305">**innodb_log_buffer_size**</span></span> |<span data-ttu-id="5170d-306">8 MB</span><span class="sxs-lookup"><span data-stu-id="5170d-306">8 MB</span></span> |<span data-ttu-id="5170d-307">128 MB</span><span class="sxs-lookup"><span data-stu-id="5170d-307">128 MB</span></span> |
| <span data-ttu-id="5170d-308">**query_cache_size**</span><span class="sxs-lookup"><span data-stu-id="5170d-308">**query_cache_size**</span></span> |<span data-ttu-id="5170d-309">16 MB</span><span class="sxs-lookup"><span data-stu-id="5170d-309">16 MB</span></span> |<span data-ttu-id="5170d-310">0</span><span class="sxs-lookup"><span data-stu-id="5170d-310">0</span></span> |

<span data-ttu-id="5170d-311">Para obter mais [parâmetros de configuração de otimização](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), consulte toohello [instruções oficiais do MySQL](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span><span class="sxs-lookup"><span data-stu-id="5170d-311">For more detailed [optimization configuration parameters](http://dev.mysql.com/doc/refman/5.6/en/innodb-configuration.html), refer toohello [MySQL official instructions](http://dev.mysql.com/doc/refman/5.6/en/innodb-parameters.html#sysvar_innodb_flush_method).</span></span>  

  <span data-ttu-id="5170d-312">**Ambiente de teste**</span><span class="sxs-lookup"><span data-stu-id="5170d-312">**Test environment**</span></span>  

| <span data-ttu-id="5170d-313">Hardware</span><span class="sxs-lookup"><span data-stu-id="5170d-313">Hardware</span></span> | <span data-ttu-id="5170d-314">Detalhes</span><span class="sxs-lookup"><span data-stu-id="5170d-314">Details</span></span> |
| --- | --- |
| <span data-ttu-id="5170d-315">CPU</span><span class="sxs-lookup"><span data-stu-id="5170d-315">CPU</span></span> |<span data-ttu-id="5170d-316">Processador AMD Opteron(tm) 4171 HE/4 cores</span><span class="sxs-lookup"><span data-stu-id="5170d-316">AMD Opteron(tm) Processor 4171 HE/4 cores</span></span> |
| <span data-ttu-id="5170d-317">Memória</span><span class="sxs-lookup"><span data-stu-id="5170d-317">Memory</span></span> |<span data-ttu-id="5170d-318">14 GB</span><span class="sxs-lookup"><span data-stu-id="5170d-318">14 GB</span></span> |
| <span data-ttu-id="5170d-319">Disco</span><span class="sxs-lookup"><span data-stu-id="5170d-319">Disk</span></span> |<span data-ttu-id="5170d-320">10 GB/disco</span><span class="sxs-lookup"><span data-stu-id="5170d-320">10 GB/disk</span></span> |
| <span data-ttu-id="5170d-321">SO</span><span class="sxs-lookup"><span data-stu-id="5170d-321">OS</span></span> |<span data-ttu-id="5170d-322">Ubuntu 14.04.1 LTS</span><span class="sxs-lookup"><span data-stu-id="5170d-322">Ubuntu 14.04.1 LTS</span></span> |

[1]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-01.png
[2]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-02.png
[3]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-03.png
[4]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-04.png
[5]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-05.png
[6]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-06.png
[7]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-07.png
[8]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-08.png
[9]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-09.png
[10]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-10.png
[11]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-11.png
[12]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-12.png
[13]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-13.png
[14]:media/optimize-mysql/virtual-machines-linux-optimize-mysql-perf-14.png

