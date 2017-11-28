


## <a name="attach-an-empty-disk"></a><span data-ttu-id="301f4-101">Anexar um disco vazio</span><span class="sxs-lookup"><span data-stu-id="301f4-101">Attach an empty disk</span></span>
<span data-ttu-id="301f4-102">Anexar um disco vazio é um modo simples de se adicionar um disco de dados, porque o Azure cria o arquivo .vhd para você e o coloca na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="301f4-102">Attaching an empty disk is a simple way to add a data disk, because Azure creates the .vhd file for you and stores it in the storage account.</span></span>

1. <span data-ttu-id="301f4-103">Clique em **Máquinas Virtuais (clássicas)**e selecione a VM apropriada.</span><span class="sxs-lookup"><span data-stu-id="301f4-103">Click **Virtual Machines (classic)**, and then select the appropriate VM.</span></span>

2. <span data-ttu-id="301f4-104">No menu Configurações, clique em **Discos**.</span><span class="sxs-lookup"><span data-stu-id="301f4-104">In the Settings menu, click **Disks**.</span></span>

   ![Anexar um novo disco vazio](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="301f4-106">Na barra de comandos, clique em **Anexar nova**.</span><span class="sxs-lookup"><span data-stu-id="301f4-106">On the command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="301f4-107">A caixa de diálogo **Anexar novo disco** é exibida.</span><span class="sxs-lookup"><span data-stu-id="301f4-107">The **Attach new disk** dialog box appears.</span></span>

    ![Anexar um novo disco](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="301f4-109">Preencha as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="301f4-109">Fill in the following information:</span></span>
    - <span data-ttu-id="301f4-110">Em **Nome do Arquivo**, aceite o nome padrão ou digite outro nome para o arquivo .vhd.</span><span class="sxs-lookup"><span data-stu-id="301f4-110">In **File Name**, accept the default name or type another one for the .vhd file.</span></span> <span data-ttu-id="301f4-111">O disco de dados usa um nome gerado automaticamente, mesmo se você digitar outro nome para o arquivo. vhd.</span><span class="sxs-lookup"><span data-stu-id="301f4-111">The data disk uses an automatically generated name, even if you type another name for the .vhd file.</span></span>
    - <span data-ttu-id="301f4-112">Selecione o **Tipo** do disco de dados.</span><span class="sxs-lookup"><span data-stu-id="301f4-112">Select the **Type** of the data disk.</span></span> <span data-ttu-id="301f4-113">Todas as máquinas virtuais oferecem suporte a discos padrão.</span><span class="sxs-lookup"><span data-stu-id="301f4-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="301f4-114">Muitas máquinas virtuais também oferecem suporte a discos premium.</span><span class="sxs-lookup"><span data-stu-id="301f4-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="301f4-115">Selecione o **Tamanho (GB)** do disco de dados.</span><span class="sxs-lookup"><span data-stu-id="301f4-115">Select the **Size (GB)** of the data disk.</span></span>
    - <span data-ttu-id="301f4-116">Para **Cache de Host**, escolha nenhum ou Somente Leitura.</span><span class="sxs-lookup"><span data-stu-id="301f4-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="301f4-117">Clique em OK para concluir.</span><span class="sxs-lookup"><span data-stu-id="301f4-117">Click OK to finish.</span></span>

4. <span data-ttu-id="301f4-118">Após o disco de dados ser criado e anexado, ele é listado na seção de discos da VM.</span><span class="sxs-lookup"><span data-stu-id="301f4-118">After the data disk is created and attached, it's listed in the disks section of the VM.</span></span>

   ![Disco de dados novo e vazio anexado com êxito](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="301f4-120">Depois de adicionar um disco de dados, você precisará fazer logon na VM e inicializar o disco para que ele possa ser usado.</span><span class="sxs-lookup"><span data-stu-id="301f4-120">After you add a data disk, you need to log on to the VM and initialize the disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="301f4-121">Como: anexar um disco existente</span><span class="sxs-lookup"><span data-stu-id="301f4-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="301f4-122">Anexar um disco existente exige que você tenha um .vhd disponível em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="301f4-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="301f4-123">Use o [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet para fazer o upload do arquivo .vhd para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="301f4-123">Use the [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet to upload the .vhd file to the storage account.</span></span> <span data-ttu-id="301f4-124">Depois de criar e carregar o arquivo .vhd, você poderá anexá-lo a uma VM.</span><span class="sxs-lookup"><span data-stu-id="301f4-124">After you've created and uploaded the .vhd file, you can attach it to a VM.</span></span>

1. <span data-ttu-id="301f4-125">Clique em **Máquinas Virtuais (clássicas)**e, em seguida, selecione a máquina virtual apropriada.</span><span class="sxs-lookup"><span data-stu-id="301f4-125">Click **Virtual Machines (classic)**, and then select the appropriate virtual machine.</span></span>

2. <span data-ttu-id="301f4-126">No menu Configurações, clique em **Discos**.</span><span class="sxs-lookup"><span data-stu-id="301f4-126">In the Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="301f4-127">Na barra de comandos, clique em **Anexar existente**.</span><span class="sxs-lookup"><span data-stu-id="301f4-127">On the command bar, click **Attach existing**.</span></span>

    ![Anexar disco de dados](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="301f4-129">Clique em **Local**.</span><span class="sxs-lookup"><span data-stu-id="301f4-129">Click **Location**.</span></span> <span data-ttu-id="301f4-130">As contas de armazenamento disponíveis são exibidas.</span><span class="sxs-lookup"><span data-stu-id="301f4-130">The available storage accounts display.</span></span> <span data-ttu-id="301f4-131">Em seguida, selecione uma conta de armazenamento apropriada daquelas listadas.</span><span class="sxs-lookup"><span data-stu-id="301f4-131">Next, select an appropriate storage account from those listed.</span></span>

    ![Fornecer conta de armazenamento de disco](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="301f4-133">A **Conta de armazenamento** contém um ou mais contêineres que contêm unidades de disco (vhds).</span><span class="sxs-lookup"><span data-stu-id="301f4-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="301f4-134">Selecione o contêiner apropriado dentre os listados.</span><span class="sxs-lookup"><span data-stu-id="301f4-134">Select the appropriate container from those listed.</span></span>

    ![Fornecer o contêiner de virtual-machines-windows](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="301f4-136">O painel **vhds** lista as unidades de disco mantidas no contêiner.</span><span class="sxs-lookup"><span data-stu-id="301f4-136">The **vhds** panel lists the disk drives held in the container.</span></span> <span data-ttu-id="301f4-137">Clique em um dos discos e, em seguida, clique em Selecionar.</span><span class="sxs-lookup"><span data-stu-id="301f4-137">Click one of the disks, and then click Select.</span></span>

    ![Fornecer a imagem de disco para virtual-machines-windows](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="301f4-139">O painel **Anexar disco existente** é exibido novamente, com o local da conta de armazenamento, o contêiner e o disco rígido selecionado (vhd) a serem adicionados à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="301f4-139">The **Attach existing disk** panel displays again, with the location containing the storage account, container, and selected hard disk (vhd) to add to the virtual machine.</span></span>

  <span data-ttu-id="301f4-140">Defina o **Cache de host** como nenhum ou Somente leitura, então clique em OK.</span><span class="sxs-lookup"><span data-stu-id="301f4-140">Set **Host caching** to none or Read only, then click OK.</span></span>

    ![Disco de dados anexado com êxito](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
