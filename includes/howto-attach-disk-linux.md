
<span data-ttu-id="a326d-101">Para saber mais sobre discos, consulte [Sobre discos e VHDs para máquinas virtuais](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a326d-101">For more information about disks, see [About Disks and VHDs for Virtual Machines](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a><span data-ttu-id="a326d-102">Anexar um disco vazio</span><span class="sxs-lookup"><span data-stu-id="a326d-102">Attach an empty disk</span></span>
1. <span data-ttu-id="a326d-103">Abra o Azure CLI 1.0 e [conectar tooyour assinatura do Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="a326d-103">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="a326d-104">Verifique se você está no modo de Gerenciamento de Serviços do Azure (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="a326d-104">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="a326d-105">Digite `azure vm disk attach-new` toocreate e anexar um novo disco, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="a326d-105">Enter `azure vm disk attach-new` toocreate and attach a new disk as shown in hello following example.</span></span> <span data-ttu-id="a326d-106">Substituir *myVM* com o nome da saudação de sua máquina Virtual do Linux e especifique o tamanho de saudação do disco de saudação em GB, que é *100GB* neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="a326d-106">Replace *myVM* with hello name of your Linux Virtual Machine and specify hello size of hello disk in GB, which is *100GB* in this example:</span></span>

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. <span data-ttu-id="a326d-107">Depois que o disco de dados Olá é criado e anexado, ele é listado na saída de saudação do `azure vm disk list <virtual-machine-name>` conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="a326d-107">After hello data disk is created and attached, it's listed in hello output of `azure vm disk list <virtual-machine-name>` as shown in hello following example:</span></span>
   
    ```azurecli
    azure vm disk list TestVM
    ```

    <span data-ttu-id="a326d-108">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a326d-108">hello output is similar toohello following example:</span></span>

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a><span data-ttu-id="a326d-109">Anexar um disco existente</span><span class="sxs-lookup"><span data-stu-id="a326d-109">Attach an existing disk</span></span>
<span data-ttu-id="a326d-110">Anexar um disco existente exige que você tenha um .vhd disponível em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a326d-110">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span>

1. <span data-ttu-id="a326d-111">Abra o Azure CLI 1.0 e [conectar tooyour assinatura do Azure](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="a326d-111">Open Azure CLI 1.0 and [connect tooyour Azure subscription](../articles/xplat-cli-connect.md).</span></span> <span data-ttu-id="a326d-112">Verifique se você está no modo de Gerenciamento de Serviços do Azure (`azure config mode asm`).</span><span class="sxs-lookup"><span data-stu-id="a326d-112">Make sure you are in Azure Service Management mode (`azure config mode asm`).</span></span>
2. <span data-ttu-id="a326d-113">Verifique se o hello VHD que você deseja tooattach já está carregado tooyour assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="a326d-113">Check if hello VHD you want tooattach is already uploaded tooyour Azure subscription:</span></span>
   
    ```azurecli
    azure vm disk list
    ```

    <span data-ttu-id="a326d-114">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a326d-114">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. <span data-ttu-id="a326d-115">Se você não encontrar o disco de saudação que você deseja toouse, você pode carregar uma assinatura de tooyour local do VHD usando `azure vm disk create` ou `azure vm disk upload`.</span><span class="sxs-lookup"><span data-stu-id="a326d-115">If you don't find hello disk that you want toouse, you may upload a local VHD tooyour subscription by using `azure vm disk create` or `azure vm disk upload`.</span></span> <span data-ttu-id="a326d-116">Um exemplo de `disk create` seria como Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a326d-116">An example of `disk create` would be as in hello following example:</span></span>
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    <span data-ttu-id="a326d-117">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a326d-117">hello output is similar toohello following example:</span></span>

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   <span data-ttu-id="a326d-118">Você também pode usar `azure vm disk upload` tooupload uma conta de armazenamento específica de tooa do VHD.</span><span class="sxs-lookup"><span data-stu-id="a326d-118">You may also use `azure vm disk upload` tooupload a VHD tooa specific storage account.</span></span> <span data-ttu-id="a326d-119">Leia mais sobre Olá comandos toomanage os discos de dados de máquina virtual do Azure [aqui](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="a326d-119">Read more about hello commands toomanage your Azure virtual machine data disks [over here](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

4. <span data-ttu-id="a326d-120">Agora você anexar Olá desejado VHD tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="a326d-120">Now you attach hello desired VHD tooyour virtual machine:</span></span>
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   <span data-ttu-id="a326d-121">Certifique-se de que tooreplace *myVM* com o nome da saudação de sua máquina virtual, e *myVHD* com seu VHD desejado.</span><span class="sxs-lookup"><span data-stu-id="a326d-121">Make sure tooreplace *myVM* with hello name of your virtual machine, and *myVHD* with your desired VHD.</span></span>

5. <span data-ttu-id="a326d-122">Você pode verificar disco Olá é máquina virtual anexado toohello `azure vm disk list <virtual-machine-name>`:</span><span class="sxs-lookup"><span data-stu-id="a326d-122">You can verify hello disk is attached toohello virtual machine with `azure vm disk list <virtual-machine-name>`:</span></span>
   
    ```azurecli
    azure vm disk list myVM
    ```

    <span data-ttu-id="a326d-123">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="a326d-123">hello output is similar toohello following example:</span></span>

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> <span data-ttu-id="a326d-124">Depois de adicionar um disco de dados, você precisa toolog na máquina virtual de toohello e inicializar disco Olá para máquina virtual de saudação pode usar o disco Olá para armazenamento (consulte Olá seguindo as etapas para obter mais informações sobre como toodo inicializar disco Olá).</span><span class="sxs-lookup"><span data-stu-id="a326d-124">After you add a data disk, you'll need toolog on toohello virtual machine and initialize hello disk so hello virtual machine can use hello disk for storage (see hello following steps for more information on how toodo initialize hello disk).</span></span>
> 
> 

