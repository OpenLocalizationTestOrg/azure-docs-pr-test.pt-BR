---
title: aaaAttach tooa um disco VM do Linux no Azure | Microsoft Docs
description: "Saiba como tooattach dados de um disco tooa VM Linux usando Olá clássico implantação de modelo e inicializar disco Olá para que esteja pronta para uso"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4901384d-2a6f-4f46-bba0-337a348b7f87
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: c76d8479ac2b522d2b6df658cd28f242473f30ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-a-data-disk-tooa-linux-virtual-machine"></a><span data-ttu-id="dd7cf-103">Como tooAttach tooa um disco de dados Máquina Virtual do Linux</span><span class="sxs-lookup"><span data-stu-id="dd7cf-103">How tooAttach a Data Disk tooa Linux Virtual Machine</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="dd7cf-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="dd7cf-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="dd7cf-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="dd7cf-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="dd7cf-107">Consulte como muito[anexar um disco de dados usando o modelo de implantação do Gerenciador de recursos de saudação](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd7cf-107">See how too[attach a data disk using hello Resource Manager deployment model](../add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="dd7cf-108">Você pode anexar discos vazios e discos que contêm dados tooyour VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-108">You can attach both empty disks and disks that contain data tooyour Azure VMs.</span></span> <span data-ttu-id="dd7cf-109">Ambos os tipos de discos são arquivos .vhd que residem em uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-109">Both types of disks are .vhd files that reside in an Azure storage account.</span></span> <span data-ttu-id="dd7cf-110">Como com a adição de qualquer computador Linux de tooa de disco, depois que você anexar o disco Olá você precisa tooinitialize e formatá-lo para que ele está pronto para uso.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-110">As with adding any disk tooa Linux machine, after you attach hello disk you need tooinitialize and format it so it's ready for use.</span></span> <span data-ttu-id="dd7cf-111">Este artigo detalha anexar discos vazios e discos que já contém dados tooyour VMs, bem como toothen inicializar e formatar um novo disco.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-111">This article details attaching both empty disks and disks already containing data tooyour VMs, as well as how toothen initialize and format a new disk.</span></span>

> [!NOTE]
> <span data-ttu-id="dd7cf-112">É um toouse de prática recomendada, uma ou mais separados discos toostore dados de uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-112">It's a best practice toouse one or more separate disks toostore a virtual machine's data.</span></span> <span data-ttu-id="dd7cf-113">Quando você cria uma máquina virtual Azure, há um disco do sistema operacional e um disco temporário.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-113">When you create an Azure virtual machine, it has an operating system disk and a temporary disk.</span></span> <span data-ttu-id="dd7cf-114">**Não use dados persistentes do toostore Olá disco temporário.**</span><span class="sxs-lookup"><span data-stu-id="dd7cf-114">**Do not use hello temporary disk toostore persistent data.**</span></span> <span data-ttu-id="dd7cf-115">Como Olá nome sugere, ele fornece armazenamento temporário apenas.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-115">As hello name implies, it provides temporary storage only.</span></span> <span data-ttu-id="dd7cf-116">Não oferece redundância nem backup porque eles não residem no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-116">It offers no redundancy or backup because it doesn't reside in Azure storage.</span></span>
> <span data-ttu-id="dd7cf-117">disco temporário Olá é normalmente gerenciado pelo Olá agente Linux do Azure e montado automaticamente muito**/mnt/Retention/ recurso** (ou **/mnt** no Ubuntu imagens).</span><span class="sxs-lookup"><span data-stu-id="dd7cf-117">hello temporary disk is typically managed by hello Azure Linux Agent and automatically mounted too**/mnt/resource** (or **/mnt** on Ubuntu images).</span></span> <span data-ttu-id="dd7cf-118">Em Olá outro lado, um disco de dados pode ser chamado pelo kernel do Linux Olá algo como `/dev/sdc`, e você precisa toopartition, formatar e montar este recurso.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-118">On hello other hand, a data disk might be named by hello Linux kernel something like `/dev/sdc`, and you need toopartition, format, and mount this resource.</span></span> <span data-ttu-id="dd7cf-119">Consulte Olá [guia do usuário do Azure Linux Agent] [ Agent] para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-119">See hello [Azure Linux Agent User Guide][Agent] for details.</span></span>
> 
> 

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-linux.md)]

## <a name="initialize-a-new-data-disk-in-linux"></a><span data-ttu-id="dd7cf-120">Inicializar um novo disco de dados no Linux</span><span class="sxs-lookup"><span data-stu-id="dd7cf-120">Initialize a new data disk in Linux</span></span>
1. <span data-ttu-id="dd7cf-121">SSH tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-121">SSH tooyour VM.</span></span> <span data-ttu-id="dd7cf-122">Para obter mais informações, consulte [como toolog na máquina virtual de tooa executando o Linux][Logon].</span><span class="sxs-lookup"><span data-stu-id="dd7cf-122">For more information, see [How toolog on tooa virtual machine running Linux][Logon].</span></span>
2. <span data-ttu-id="dd7cf-123">Em seguida, você precisa identificador de dispositivo toofind Olá para Olá tooinitialize de disco de dados.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-123">Next you need toofind hello device identifier for hello data disk tooinitialize.</span></span> <span data-ttu-id="dd7cf-124">Há dois toodo de maneiras que:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-124">There are two ways toodo that:</span></span>
   
    <span data-ttu-id="dd7cf-125">a) logs de Grep para dispositivos SCSI hello, como Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-125">a) Grep for SCSI devices in hello logs, such as in hello following command:</span></span>
   
    ```bash
    sudo grep SCSI /var/log/messages
    ```
   
    <span data-ttu-id="dd7cf-126">Para distribuições Ubuntu recentes, talvez seja necessário toouse `sudo grep SCSI /var/log/syslog` porque o registro em log muito`/var/log/messages` pode ser desabilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-126">For recent Ubuntu distributions, you may need toouse `sudo grep SCSI /var/log/syslog` because logging too`/var/log/messages` might be disabled by default.</span></span>
   
    <span data-ttu-id="dd7cf-127">Você pode encontrar o identificador Olá Olá última do disco de dados que foi adicionado em mensagens de saudação que são exibidas.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-127">You can find hello identifier of hello last data disk that was added in hello messages that are displayed.</span></span>
   
    ![Obter mensagens de saudação do disco](./media/attach-disk/scsidisklog.png)
   
    <span data-ttu-id="dd7cf-129">OU</span><span class="sxs-lookup"><span data-stu-id="dd7cf-129">OR</span></span>
   
    <span data-ttu-id="dd7cf-130">b) Olá usar `lsscsi` toofind comando out id do dispositivo hello. `lsscsi` pode ser instalado pelo `yum install lsscsi` (no Red Hat com base em distribuições) ou `apt-get install lsscsi` (no Debian distribuições de base).</span><span class="sxs-lookup"><span data-stu-id="dd7cf-130">b) Use hello `lsscsi` command toofind out hello device id. `lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="dd7cf-131">Você pode localizar o disco Olá procurando pelo seu *lun* ou **número de unidade lógica**.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-131">You can find hello disk you are looking for by its *lun* or **logical unit number**.</span></span> <span data-ttu-id="dd7cf-132">Por exemplo, Olá *lun* para discos Olá anexado podem ser vistos facilmente em `azure vm disk list <virtual-machine>` como:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-132">For example, hello *lun* for hello disks you attached can be easily seen from `azure vm disk list <virtual-machine>` as:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="dd7cf-133">saída de Hello é a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-133">hello output is similar toohello following:</span></span>

    ```azurecli
    info:    Executing command vm disk list
    + Fetching disk images
    + Getting virtual machines
    + Getting VM disks
    data:    Lun  Size(GB)  Blob-Name                         OS
    data:    ---  --------  --------------------------------  -----
    data:         30        myVM-2645b8030676c8f8.vhd  Linux
    data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
    info:    vm disk list command OK
    ```
   
    <span data-ttu-id="dd7cf-134">Comparar esses dados com saída Olá `lsscsi` para Olá mesma máquina virtual de amostra:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-134">Compare this data with hello output of `lsscsi` for hello same sample virtual machine:</span></span>
   
    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```
   
    <span data-ttu-id="dd7cf-135">último número Olá Olá tupla em cada linha é hello *lun*.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-135">hello last number in hello tuple in each row is hello *lun*.</span></span> <span data-ttu-id="dd7cf-136">Veja `man lsscsi` para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-136">See `man lsscsi` for more information.</span></span>
3. <span data-ttu-id="dd7cf-137">No prompt de hello, digite Olá toocreate de comando a seguir seu dispositivo:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-137">At hello prompt, type hello following command toocreate your device:</span></span>
   
    ```bash
    sudo fdisk /dev/sdc
    ```

4. <span data-ttu-id="dd7cf-138">Quando solicitado, digite  **n**  toocreate uma partição.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-138">When prompted, type **n** toocreate a partition.</span></span>

    ![Criar dispositivo](./media/attach-disk/fdisknewpartition.png)

5. <span data-ttu-id="dd7cf-140">Quando solicitado, digite **p** partição primária do hello toomake Olá partição.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-140">When prompted, type **p** toomake hello partition hello primary partition.</span></span> <span data-ttu-id="dd7cf-141">Tipo **1** toomake Olá primeira partição e, em seguida, digite insira o valor de padrão de saudação do tooaccept para cilindro hello.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-141">Type **1** toomake it hello first partition, and then type enter tooaccept hello default value for hello cylinder.</span></span> <span data-ttu-id="dd7cf-142">Em alguns sistemas, pode mostrar valores padrão Olá Olá primeiro e Olá última setores, em vez de cilindro hello.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-142">On some systems, it can show hello default values of hello first and hello last sectors, instead of hello cylinder.</span></span> <span data-ttu-id="dd7cf-143">Você pode escolher tooaccept esses padrões.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-143">You can choose tooaccept these defaults.</span></span>

    ![Criar partição](./media/attach-disk/fdisknewpartdetails.png)


6. <span data-ttu-id="dd7cf-145">Tipo **p** toosee detalhes Olá disco Olá que estiver sendo particionado.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-145">Type **p** toosee hello details about hello disk that is being partitioned.</span></span>

    ![Listar informações de disco](./media/attach-disk/fdiskpartitiondetails.png)


7. <span data-ttu-id="dd7cf-147">Tipo **w** toowrite configurações Olá disco hello.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-147">Type **w** toowrite hello settings for hello disk.</span></span>

    ![Gravar alterações de disco Olá](./media/attach-disk/fdiskwritedisk.png)

8. <span data-ttu-id="dd7cf-149">Agora você pode criar o sistema de arquivos de saudação na nova partição de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-149">Now you can create hello file system on hello new partition.</span></span> <span data-ttu-id="dd7cf-150">Acrescentar Olá partição número toohello dispositivo ID (no exemplo a seguir de saudação `/dev/sdc1`).</span><span class="sxs-lookup"><span data-stu-id="dd7cf-150">Append hello partition number toohello device ID (in hello following example `/dev/sdc1`).</span></span> <span data-ttu-id="dd7cf-151">Olá exemplo a seguir cria uma partição de ext4 em /dev/sdc1:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-151">hello following example creates an ext4 partition on /dev/sdc1:</span></span>
   
    ```bash
    sudo mkfs -t ext4 /dev/sdc1
    ```
   
    ![Criar sistema de arquivos](./media/attach-disk/mkfsext4.png)
   
   > [!NOTE]
   > <span data-ttu-id="dd7cf-153">Sistemas SuSE Linux Enterprise 11 dão suporte apenas a acesso somente leitura para sistemas de arquivos ext4.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-153">SuSE Linux Enterprise 11 systems only support read-only access for ext4 file systems.</span></span> <span data-ttu-id="dd7cf-154">Para esses sistemas, é recomendável tooformat Olá novo sistema de arquivos como ext3 em vez de ext4.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-154">For these systems, it is recommended tooformat hello new file system as ext3 rather than ext4.</span></span>

9. <span data-ttu-id="dd7cf-155">Faça um diretório toomount Olá novo sistema de arquivos, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-155">Make a directory toomount hello new file system, as follows:</span></span>
   
    ```bash
    sudo mkdir /datadrive
    ```

10. <span data-ttu-id="dd7cf-156">Por fim, você pode montar Olá unidade, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-156">Finally you can mount hello drive, as follows:</span></span>
   
    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```
   
    <span data-ttu-id="dd7cf-157">disco de dados Olá agora está pronto toouse como **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-157">hello data disk is now ready toouse as **/datadrive**.</span></span>
   
    ![Criar disco de saudação de diretório e montagem Olá](./media/attach-disk/mkdirandmount.png)

11. <span data-ttu-id="dd7cf-159">Adicione Olá nova unidade muito/etc/fstab:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-159">Add hello new drive too/etc/fstab:</span></span>
   
    <span data-ttu-id="dd7cf-160">unidade de saudação tooensure é remontada automaticamente após uma reinicialização, que ele deve ser adicionado toohello /etc/fstab arquivo.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-160">tooensure hello drive is remounted automatically after a reboot it must be added toohello /etc/fstab file.</span></span> <span data-ttu-id="dd7cf-161">Além disso, é altamente recomendável que Olá UUID (identificador universalmente exclusivo) é usado em /etc/fstab toorefer toohello unidade em vez do nome de dispositivo de saudação apenas (ou seja, /dev/sdc1).</span><span class="sxs-lookup"><span data-stu-id="dd7cf-161">In addition, it is highly recommended that hello UUID (Universally Unique IDentifier) is used in /etc/fstab toorefer toohello drive rather than just hello device name (i.e. /dev/sdc1).</span></span> <span data-ttu-id="dd7cf-162">Usando Olá UUID evita que está sendo montado tooa dado local se Olá SO detecta um erro de disco durante a inicialização e discos de dados restantes, em seguida, que está sendo atribuído as identificações de dispositivo de disco incorreta hello.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-162">Using hello UUID avoids hello incorrect disk being mounted tooa given location if hello OS detects a disk error during boot and any remaining data disks then being assigned those device IDs.</span></span> <span data-ttu-id="dd7cf-163">toofind Olá UUID da unidade nova hello, você pode usar o hello **blkid** utilitário:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-163">toofind hello UUID of hello new drive, you can use hello **blkid** utility:</span></span>
   
    ```bash
    sudo -i blkid
    ```
   
    <span data-ttu-id="dd7cf-164">saída de Hello parece semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-164">hello output looks similar toohello following example:</span></span>
   
    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

    > [!NOTE]
    > <span data-ttu-id="dd7cf-165">Edição incorretamente Olá **/etc/fstab** arquivo pode resultar em um sistema não inicializável.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-165">Improperly editing hello **/etc/fstab** file could result in an unbootable system.</span></span> <span data-ttu-id="dd7cf-166">Se não tiver certeza, consulte a documentação do toohello da distribuição para obter informações sobre como tooproperly editar esse arquivo.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-166">If unsure, refer toohello distribution's documentation for information on how tooproperly edit this file.</span></span> <span data-ttu-id="dd7cf-167">Também é recomendável que um backup de arquivo /etc/fstab de saudação é criado antes de editar.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-167">It is also recommended that a backup of hello /etc/fstab file is created before editing.</span></span>

    <span data-ttu-id="dd7cf-168">Em seguida, abra Olá **/etc/fstab** em um editor de texto:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-168">Next, open hello **/etc/fstab** file in a text editor:</span></span>

    ```bash
    sudo vi /etc/fstab
    ```

    <span data-ttu-id="dd7cf-169">Neste exemplo, usamos Olá UUID valor para Olá novo **/desenvolvimento/sdc1** dispositivo que foi criado em etapas anteriores hello e ponto de montagem Olá **/datadrive**.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-169">In this example, we use hello UUID value for hello new **/dev/sdc1** device that was created in hello previous steps, and hello mountpoint **/datadrive**.</span></span> <span data-ttu-id="dd7cf-170">Adicionar Olá após o final da linha toohello de saudação **/etc/fstab** arquivo:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-170">Add hello following line toohello end of hello **/etc/fstab** file:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,nofail   1   2
    ```

    <span data-ttu-id="dd7cf-171">Ou, em sistemas baseados no SuSE Linux, talvez seja necessário toouse um formato ligeiramente diferente:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-171">Or, on systems based on SuSE Linux you may need toouse a slightly different format:</span></span>

    ```sh
    /dev/disk/by-uuid/33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext3   defaults,nofail   1   2
    ```

    > [!NOTE]
    > <span data-ttu-id="dd7cf-172">Olá `nofail` opção garante que Olá VM iniciado mesmo se Olá de sistema de arquivos está corrompido ou disco Olá não existe no momento da inicialização.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-172">hello `nofail` option ensures that hello VM starts even if hello filesystem is corrupt or hello disk does not exist at boot time.</span></span> <span data-ttu-id="dd7cf-173">Sem essa opção, você pode encontrar o comportamento conforme descrito em [não é possível SSH tooLinux VM devido a erros de tooFSTAB](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span><span class="sxs-lookup"><span data-stu-id="dd7cf-173">Without this option, you may encounter behavior as described in [Cannot SSH tooLinux VM due tooFSTAB errors](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/cannot-ssh-to-linux-vm-after-adding-data-disk-to-etcfstab-and-rebooting/).</span></span>

    <span data-ttu-id="dd7cf-174">Agora você pode testar se o sistema de arquivo hello está montado corretamente desmontar e remontar, em seguida, o sistema de arquivo hello, ou seja, usando o ponto de montagem do exemplo hello `/datadrive` criado no hello etapas anteriores:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-174">You can now test that hello file system is mounted properly by unmounting and then remounting hello file system, i.e. using hello example mount point `/datadrive` created in hello earlier steps:</span></span>

    ```bash
    sudo umount /datadrive
    sudo mount /datadrive
    ```

    <span data-ttu-id="dd7cf-175">Se hello `mount` comando gerará um erro, verifique Olá/etc/fstab arquivo sintaxe correta.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-175">If hello `mount` command produces an error, check hello /etc/fstab file for correct syntax.</span></span> <span data-ttu-id="dd7cf-176">Se as partições ou unidades de dados adicionais forem criadas, insira-as separadamente em/etc/fstab também.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-176">If additional data drives or partitions are created, enter them into /etc/fstab separately as well.</span></span>

    <span data-ttu-id="dd7cf-177">Tornar gravável unidade hello usando este comando:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-177">Make hello drive writable by using this command:</span></span>

    ```bash
    sudo chmod go+w /datadrive
    ```

    > [!NOTE]
    > <span data-ttu-id="dd7cf-178">Subsequentemente, remover um disco de dados sem editar fstab poderia causar Olá VM toofail tooboot.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-178">Subsequently removing a data disk without editing fstab could cause hello VM toofail tooboot.</span></span> <span data-ttu-id="dd7cf-179">Se esta for uma ocorrência comum, a maioria das distribuições fornecem qualquer Olá `nofail` e/ou `nobootwait` fstab opções que permitem que um sistema tooboot mesmo se o disco de saudação falhar toomount no momento da inicialização.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-179">If this is a common occurrence, most distributions provide either hello `nofail` and/or `nobootwait` fstab options that allow a system tooboot even if hello disk fails toomount at boot time.</span></span> <span data-ttu-id="dd7cf-180">Consulte a documentação da distribuição para obter mais informações sobre esses parâmetros.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-180">Consult your distribution's documentation for more information on these parameters.</span></span>

### <a name="trimunmap-support-for-linux-in-azure"></a><span data-ttu-id="dd7cf-181">Suporte a TRIM/UNMAP para Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="dd7cf-181">TRIM/UNMAP support for Linux in Azure</span></span>
<span data-ttu-id="dd7cf-182">Suportam a alguns kernels Linux TRIM/DESMAPEAMENTO operações toodiscard blocos não usados no disco hello.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-182">Some Linux kernels support TRIM/UNMAP operations toodiscard unused blocks on hello disk.</span></span> <span data-ttu-id="dd7cf-183">Essas operações são principalmente útil no armazenamento padrão tooinform Azure que páginas excluídas não são mais válidas e podem ser descartadas.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-183">These operations are primarily useful in standard storage tooinform Azure that deleted pages are no longer valid and can be discarded.</span></span> <span data-ttu-id="dd7cf-184">Descartar páginas poderá representar uma economia de dinheiro se você criar arquivos grandes e, em seguida, excluí-los.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-184">Discarding pages can save cost if you create large files and then delete them.</span></span>

<span data-ttu-id="dd7cf-185">Há duas maneiras tooenable TRIM suporte em sua VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-185">There are two ways tooenable TRIM support in your Linux VM.</span></span> <span data-ttu-id="dd7cf-186">Como de costume, consulte a distribuição para Olá abordagem recomendada:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-186">As usual, consult your distribution for hello recommended approach:</span></span>

* <span data-ttu-id="dd7cf-187">Saudação de uso `discard` montar opção `/etc/fstab`, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-187">Use hello `discard` mount option in `/etc/fstab`, for example:</span></span>

    ```sh
    UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults,discard   1   2
    ```

* <span data-ttu-id="dd7cf-188">Em alguns Olá casos `discard` opção pode ter implicações de desempenho.</span><span class="sxs-lookup"><span data-stu-id="dd7cf-188">In some cases hello `discard` option may have performance implications.</span></span> <span data-ttu-id="dd7cf-189">Como alternativa, você pode executar Olá `fstrim` comando manualmente da linha de comando hello, ou adicionar tooyour crontab toorun regularmente:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-189">Alternatively, you can run hello `fstrim` command manually from hello command line, or add it tooyour crontab toorun regularly:</span></span>
  
    <span data-ttu-id="dd7cf-190">**Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="dd7cf-190">**Ubuntu**</span></span>
  
    ```bash
    sudo apt-get install util-linux
    sudo fstrim /datadrive
    ```
  
    <span data-ttu-id="dd7cf-191">**RHEL/CentOS**</span><span class="sxs-lookup"><span data-stu-id="dd7cf-191">**RHEL/CentOS**</span></span>
  
    ```bash
    sudo yum install util-linux
    sudo fstrim /datadrive
    ```

## <a name="troubleshooting"></a><span data-ttu-id="dd7cf-192">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="dd7cf-192">Troubleshooting</span></span>
[!INCLUDE [virtual-machines-linux-lunzero](../../../../includes/virtual-machines-linux-lunzero.md)]

## <a name="next-steps"></a><span data-ttu-id="dd7cf-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dd7cf-193">Next Steps</span></span>
<span data-ttu-id="dd7cf-194">Você pode ler mais sobre como usar a VM do Linux em Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd7cf-194">You can read more about using your Linux VM in hello following articles:</span></span>

* <span data-ttu-id="dd7cf-195">[Como toolog na máquina virtual de tooa executando o Linux][Logon]</span><span class="sxs-lookup"><span data-stu-id="dd7cf-195">[How toolog on tooa virtual machine running Linux][Logon]</span></span>
* [<span data-ttu-id="dd7cf-196">Como toodetach um disco de uma máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="dd7cf-196">How toodetach a disk from a Linux virtual machine</span></span>](detach-disk.md)
* [<span data-ttu-id="dd7cf-197">Usando Olá CLI do Azure com o modelo de implantação clássico Olá</span><span class="sxs-lookup"><span data-stu-id="dd7cf-197">Using hello Azure CLI with hello Classic deployment model</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="dd7cf-198">Configurar o RAID em uma VM Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="dd7cf-198">Configure RAID on a Linux VM in Azure</span></span>](../configure-raid.md)
* [<span data-ttu-id="dd7cf-199">Configurar o LVM em uma VM Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="dd7cf-199">Configure LVM on a Linux VM in Azure</span></span>](../configure-lvm.md)

<!--Link references-->
[Agent]:../agent-user-guide.md
[Logon]:../mac-create-ssh-keys.md
