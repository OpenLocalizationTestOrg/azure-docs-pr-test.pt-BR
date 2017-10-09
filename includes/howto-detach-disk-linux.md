<span data-ttu-id="4cdac-101">Quando você não precisa mais um disco de dados é anexado tooa VM (máquina virtual), você pode facilmente desanexá-lo.</span><span class="sxs-lookup"><span data-stu-id="4cdac-101">When you no longer need a data disk that's attached tooa virtual machine (VM), you can easily detach it.</span></span> <span data-ttu-id="4cdac-102">Ao desanexar um disco de saudação VM, disco Olá não é removido do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4cdac-102">When you detach a disk from hello VM, hello disk is not removed it from storage.</span></span> <span data-ttu-id="4cdac-103">Se você quiser toouse Olá dados existentes ao disco Olá novamente, você poderá reanexar-toohello mesma VM, ou outro.</span><span class="sxs-lookup"><span data-stu-id="4cdac-103">If you want toouse hello existing data on hello disk again, you can reattach it toohello same VM, or another one.</span></span>  

> [!NOTE]
> <span data-ttu-id="4cdac-104">Uma VM no Azure usa diferentes tipos de discos, um disco de sistema operacional, um disco temporário local e discos de dados opcionais.</span><span class="sxs-lookup"><span data-stu-id="4cdac-104">A VM in Azure uses different types of disks - an operating system disk, a local temporary disk, and optional data disks.</span></span> <span data-ttu-id="4cdac-105">Para obter detalhes, confira [Sobre discos e VHDs para máquinas virtuais](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4cdac-105">For details, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4cdac-106">Você não pode desanexar um disco do sistema operacional, a menos que você também excluir Olá VM.</span><span class="sxs-lookup"><span data-stu-id="4cdac-106">You cannot detach an operating system disk unless you also delete hello VM.</span></span>

## <a name="find-hello-disk"></a><span data-ttu-id="4cdac-107">Localizar o disco Olá</span><span class="sxs-lookup"><span data-stu-id="4cdac-107">Find hello disk</span></span>
<span data-ttu-id="4cdac-108">Antes de poder desanexar um disco de uma VM é necessário toofind out Olá número LUN, que é um identificador para Olá disco toobe desanexado.</span><span class="sxs-lookup"><span data-stu-id="4cdac-108">Before you can detach a disk from a VM you need toofind out hello LUN number, which is an identifier for hello disk toobe detached.</span></span> <span data-ttu-id="4cdac-109">toodo que, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="4cdac-109">toodo that, follow these steps:</span></span>

1. <span data-ttu-id="4cdac-110">Abra a CLI do Azure e [conectar tooyour assinatura do Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="4cdac-110">Open Azure CLI and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="4cdac-111">Verifique se você está no modo de Gerenciamento de Serviços do Azure (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="4cdac-111">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="4cdac-112">Descubra quais discos estão anexado tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="4cdac-112">Find out which disks are attached tooyour VM.</span></span> <span data-ttu-id="4cdac-113">Olá, exemplo a seguir lista discos para Olá VM denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="4cdac-113">hello following example lists disks for hello VM named `myVM`:</span></span>

    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="4cdac-114">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4cdac-114">hello output is similar toohello following example:</span></span>

    ```azurecli
    * Fetching disk images
    * Getting virtual machines
    * Getting VM disks
      data:    Lun  Size(GB)  Blob-Name                         OS
      data:    ---  --------  --------------------------------  -----
      data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
      data:    0    30        myDataDisk.vhd
      info:    vm disk list command OK
    ```

3. <span data-ttu-id="4cdac-115">Observe Olá LUN ou hello **número de unidade lógica** para disco Olá que você deseja toodetach.</span><span class="sxs-lookup"><span data-stu-id="4cdac-115">Note hello LUN or hello **logical unit number** for hello disk that you want toodetach.</span></span>

## <a name="remove-operating-system-references-toohello-disk"></a><span data-ttu-id="4cdac-116">Remover disco do sistema operacional referências toohello</span><span class="sxs-lookup"><span data-stu-id="4cdac-116">Remove operating system references toohello disk</span></span>
<span data-ttu-id="4cdac-117">Antes de desanexar o disco de saudação do convidado do Linux hello, você deve garantir que todas as partições no disco Olá não estão em uso.</span><span class="sxs-lookup"><span data-stu-id="4cdac-117">Before detaching hello disk from hello Linux guest, you should make sure that all partitions on hello disk are not in use.</span></span> <span data-ttu-id="4cdac-118">Certifique-se de sistema operacional Olá não tenta tooremount-las após uma reinicialização.</span><span class="sxs-lookup"><span data-stu-id="4cdac-118">Ensure that hello operating system does not attempt tooremount them after a reboot.</span></span> <span data-ttu-id="4cdac-119">Essas etapas Desfazer configuração Olá provavelmente criou quando [anexando](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) disco hello.</span><span class="sxs-lookup"><span data-stu-id="4cdac-119">These steps undo hello configuration you likely created when [attaching](../articles/virtual-machines/linux/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json) hello disk.</span></span>

1. <span data-ttu-id="4cdac-120">Saudação de uso `lsscsi` identificador de disco do comando toodiscover hello.</span><span class="sxs-lookup"><span data-stu-id="4cdac-120">Use hello `lsscsi` command toodiscover hello disk identifier.</span></span> <span data-ttu-id="4cdac-121">O `lsscsi` pode ser instalado pelo `yum install lsscsi` (distribuições baseadas no Red Hat) ou pelo `apt-get install lsscsi` (distribuições baseadas no Debian).</span><span class="sxs-lookup"><span data-stu-id="4cdac-121">`lsscsi` can be installed by either `yum install lsscsi` (on Red Hat based distributions) or `apt-get install lsscsi` (on Debian based distributions).</span></span> <span data-ttu-id="4cdac-122">Você pode encontrar o identificador de disco Olá que procurando usando o número LUN de saudação.</span><span class="sxs-lookup"><span data-stu-id="4cdac-122">You can find hello disk identifier you are looking for by using hello LUN number.</span></span> <span data-ttu-id="4cdac-123">último número Olá Olá tupla em cada linha é hello LUN.</span><span class="sxs-lookup"><span data-stu-id="4cdac-123">hello last number in hello tuple in each row is hello LUN.</span></span> <span data-ttu-id="4cdac-124">Em Olá seguinte exemplo de `lsscsi`, LUN 0 mapeia muito  */desenvolvimento/sdc*</span><span class="sxs-lookup"><span data-stu-id="4cdac-124">In hello following example from `lsscsi`, LUN 0 maps too*/dev/sdc*</span></span>

    ```bash
    [1:0:0:0]    cd/dvd  Msft     Virtual CD/ROM   1.0   /dev/sr0
    [2:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sda
    [3:0:1:0]    disk    Msft     Virtual Disk     1.0   /dev/sdb
    [5:0:0:0]    disk    Msft     Virtual Disk     1.0   /dev/sdc
    ```

2. <span data-ttu-id="4cdac-125">Use `fdisk -l <disk>` toodiscover partições de saudação associadas Olá disco toobe desanexado.</span><span class="sxs-lookup"><span data-stu-id="4cdac-125">Use `fdisk -l <disk>` toodiscover hello partitions associated with hello disk toobe detached.</span></span> <span data-ttu-id="4cdac-126">Olá, exemplo a seguir mostra a saída de hello para `/dev/sdc`:</span><span class="sxs-lookup"><span data-stu-id="4cdac-126">hello following example shows hello output for `/dev/sdc`:</span></span>

    ```bash
    Disk /dev/sdc: 1098.4 GB, 1098437885952 bytes, 2145386496 sectors
    Units = sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disk label type: dos
    Disk identifier: 0x5a1d2a1a
    
        Device Boot      Start         End      Blocks   Id  System
    /dev/sdc1            2048  2145386495  1072692224   83  Linux
    ```

3. <span data-ttu-id="4cdac-127">Desmonte cada partição listada para disco hello.</span><span class="sxs-lookup"><span data-stu-id="4cdac-127">Unmount each partition listed for hello disk.</span></span> <span data-ttu-id="4cdac-128">Olá exemplo a seguir desmonta `/dev/sdc1`:</span><span class="sxs-lookup"><span data-stu-id="4cdac-128">hello following example unmounts `/dev/sdc1`:</span></span>

    ```bash
    sudo umount /dev/sdc1
    ```

4. <span data-ttu-id="4cdac-129">Saudação de uso `blkid` Olá de toodiscovery comando UUIDs para todas as partições.</span><span class="sxs-lookup"><span data-stu-id="4cdac-129">Use hello `blkid` command toodiscovery hello UUIDs for all partitions.</span></span> <span data-ttu-id="4cdac-130">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4cdac-130">hello output is similar toohello following example:</span></span>

    ```bash
    /dev/sda1: UUID="11111111-1b1b-1c1c-1d1d-1e1e1e1e1e1e" TYPE="ext4"
    /dev/sdb1: UUID="22222222-2b2b-2c2c-2d2d-2e2e2e2e2e2e" TYPE="ext4"
    /dev/sdc1: UUID="33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e" TYPE="ext4"
    ```

5. <span data-ttu-id="4cdac-131">Remover as entradas nos Olá **/etc/fstab** arquivo associado com caminhos de dispositivo de saudação ou UUIDs para todas as partições de saudação disco toobe desanexado.</span><span class="sxs-lookup"><span data-stu-id="4cdac-131">Remove entries in hello **/etc/fstab** file associated with either hello device paths or UUIDs for all partitions for hello disk toobe detached.</span></span>  <span data-ttu-id="4cdac-132">As entradas para este exemplo poderiam ser:</span><span class="sxs-lookup"><span data-stu-id="4cdac-132">Entries for this example might be:</span></span>

    ```sh  
   UUID=33333333-3b3b-3c3c-3d3d-3e3e3e3e3e3e   /datadrive   ext4   defaults   1   2
   ```

    <span data-ttu-id="4cdac-133">ou o</span><span class="sxs-lookup"><span data-stu-id="4cdac-133">or</span></span>
   
   ```sh   
   /dev/sdc1   /datadrive   ext4   defaults   1   2
   ```

## <a name="detach-hello-disk"></a><span data-ttu-id="4cdac-134">Desanexar o disco Olá</span><span class="sxs-lookup"><span data-stu-id="4cdac-134">Detach hello disk</span></span>
<span data-ttu-id="4cdac-135">Depois de localizar o número LUN de saudação do disco de saudação e referências de sistema operacional Olá removido, você está pronto toodetach-lo:</span><span class="sxs-lookup"><span data-stu-id="4cdac-135">After you find hello LUN number of hello disk and removed hello operating system references, you're ready toodetach it:</span></span>

1. <span data-ttu-id="4cdac-136">Desanexar o disco selecionado de saudação da máquina virtual de saudação executando o comando Olá `azure vm disk detach
   <virtual-machine-name> <LUN>`.</span><span class="sxs-lookup"><span data-stu-id="4cdac-136">Detach hello selected disk from hello virtual machine by running hello command `azure vm disk detach
<virtual-machine-name> <LUN>`.</span></span> <span data-ttu-id="4cdac-137">Olá, exemplo a seguir desanexa LUN `0` de saudação VM denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="4cdac-137">hello following example detaches LUN `0` from hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk detach myVM 0
    ```

2. <span data-ttu-id="4cdac-138">Você pode verificar se o disco de saudação foi desanexado executando `azure vm disk list` novamente.</span><span class="sxs-lookup"><span data-stu-id="4cdac-138">You can check if hello disk got detached by running `azure vm disk list` again.</span></span> <span data-ttu-id="4cdac-139">Olá verificações de exemplo a seguir Olá VM denominada `myVM`:</span><span class="sxs-lookup"><span data-stu-id="4cdac-139">hello following example checks hello VM named `myVM`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="4cdac-140">saudação de saída é similar toohello exemplo, que mostra o disco de dados Olá não esteja conectado a seguir:</span><span class="sxs-lookup"><span data-stu-id="4cdac-140">hello output is similar toohello following example, which shows hello data disk is no longer attached:</span></span>

    ```azurecli
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        ubuntuVM-2645b8030676c8f8.vhd  Linux
     info:    vm disk list command OK
    ```

<span data-ttu-id="4cdac-141">disco Olá desanexado permanece no armazenamento, mas não está mais anexado tooa virtual machine.</span><span class="sxs-lookup"><span data-stu-id="4cdac-141">hello detached disk remains in storage but is no longer attached tooa virtual machine.</span></span>

