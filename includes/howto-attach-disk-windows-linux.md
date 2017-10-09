


## <a name="attach-an-empty-disk"></a><span data-ttu-id="59d15-101">Anexar um disco vazio</span><span class="sxs-lookup"><span data-stu-id="59d15-101">Attach an empty disk</span></span>
<span data-ttu-id="59d15-102">Anexar um disco vazio é tooadd uma maneira simples que dados de um disco, porque o Azure cria o arquivo. vhd de saudação para você e o armazena na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="59d15-102">Attaching an empty disk is a simple way tooadd a data disk, because Azure creates hello .vhd file for you and stores it in hello storage account.</span></span>

1. <span data-ttu-id="59d15-103">Clique em **máquinas virtuais (clássicas)**, e, em seguida, selecione Olá VM apropriado.</span><span class="sxs-lookup"><span data-stu-id="59d15-103">Click **Virtual Machines (classic)**, and then select hello appropriate VM.</span></span>

2. <span data-ttu-id="59d15-104">No menu de configurações de saudação, clique em **discos**.</span><span class="sxs-lookup"><span data-stu-id="59d15-104">In hello Settings menu, click **Disks**.</span></span>

   ![Anexar um novo disco vazio](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. <span data-ttu-id="59d15-106">Na barra de comandos de saudação, clique em **anexar novos**.</span><span class="sxs-lookup"><span data-stu-id="59d15-106">On hello command bar, click **Attach new**.</span></span>  
    <span data-ttu-id="59d15-107">Olá **anexar novo disco** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="59d15-107">hello **Attach new disk** dialog box appears.</span></span>

    ![Anexar um novo disco](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    <span data-ttu-id="59d15-109">Preencha Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="59d15-109">Fill in hello following information:</span></span>
    - <span data-ttu-id="59d15-110">Em **nome de arquivo**, aceite o nome padrão de saudação ou digite um outro para o arquivo. vhd de saudação.</span><span class="sxs-lookup"><span data-stu-id="59d15-110">In **File Name**, accept hello default name or type another one for hello .vhd file.</span></span> <span data-ttu-id="59d15-111">disco de dados Olá usa um nome gerado automaticamente, mesmo se você digitar outro nome para o arquivo. vhd de saudação.</span><span class="sxs-lookup"><span data-stu-id="59d15-111">hello data disk uses an automatically generated name, even if you type another name for hello .vhd file.</span></span>
    - <span data-ttu-id="59d15-112">Selecione Olá **tipo** saudação do disco de dados.</span><span class="sxs-lookup"><span data-stu-id="59d15-112">Select hello **Type** of hello data disk.</span></span> <span data-ttu-id="59d15-113">Todas as máquinas virtuais oferecem suporte a discos padrão.</span><span class="sxs-lookup"><span data-stu-id="59d15-113">All virtual machines support standard disks.</span></span> <span data-ttu-id="59d15-114">Muitas máquinas virtuais também oferecem suporte a discos premium.</span><span class="sxs-lookup"><span data-stu-id="59d15-114">Many virtual machines also support premium disks.</span></span>
    - <span data-ttu-id="59d15-115">Selecione Olá **tamanho (GB)** saudação do disco de dados.</span><span class="sxs-lookup"><span data-stu-id="59d15-115">Select hello **Size (GB)** of hello data disk.</span></span>
    - <span data-ttu-id="59d15-116">Para **Cache de Host**, escolha nenhum ou Somente Leitura.</span><span class="sxs-lookup"><span data-stu-id="59d15-116">For **Host caching**, choose none or Read Only.</span></span>
    - <span data-ttu-id="59d15-117">Clique em toofinish Okey.</span><span class="sxs-lookup"><span data-stu-id="59d15-117">Click OK toofinish.</span></span>

4. <span data-ttu-id="59d15-118">Depois que o disco de dados Olá é criado e anexado, ele é listado na seção de discos de saudação do hello VM.</span><span class="sxs-lookup"><span data-stu-id="59d15-118">After hello data disk is created and attached, it's listed in hello disks section of hello VM.</span></span>

   ![Disco de dados novo e vazio anexado com êxito](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> <span data-ttu-id="59d15-120">Depois de adicionar um disco de dados, você precisa toolog em toohello VM e inicializar disco Olá para que ele possa ser usado.</span><span class="sxs-lookup"><span data-stu-id="59d15-120">After you add a data disk, you need toolog on toohello VM and initialize hello disk so that it can be used.</span></span>

## <a name="how-to-attach-an-existing-disk"></a><span data-ttu-id="59d15-121">Como: anexar um disco existente</span><span class="sxs-lookup"><span data-stu-id="59d15-121">How to: Attach an existing disk</span></span>
<span data-ttu-id="59d15-122">Anexar um disco existente exige que você tenha um .vhd disponível em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="59d15-122">Attaching an existing disk requires that you have a .vhd available in a storage account.</span></span> <span data-ttu-id="59d15-123">Saudação de uso [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) conta de armazenamento toohello de arquivo. vhd de saudação tooupload de cmdlet.</span><span class="sxs-lookup"><span data-stu-id="59d15-123">Use hello [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) cmdlet tooupload hello .vhd file toohello storage account.</span></span> <span data-ttu-id="59d15-124">Depois de criar e carregar o arquivo. vhd de saudação, você pode anexar tooa VM.</span><span class="sxs-lookup"><span data-stu-id="59d15-124">After you've created and uploaded hello .vhd file, you can attach it tooa VM.</span></span>

1. <span data-ttu-id="59d15-125">Clique em **máquinas virtuais (clássicas)**, e, em seguida, selecione Olá máquina virtual apropriado.</span><span class="sxs-lookup"><span data-stu-id="59d15-125">Click **Virtual Machines (classic)**, and then select hello appropriate virtual machine.</span></span>

2. <span data-ttu-id="59d15-126">No menu de configurações de saudação, clique em **discos**.</span><span class="sxs-lookup"><span data-stu-id="59d15-126">In hello Settings menu, click **Disks**.</span></span>

3. <span data-ttu-id="59d15-127">Na barra de comandos de saudação, clique em **anexar existente**.</span><span class="sxs-lookup"><span data-stu-id="59d15-127">On hello command bar, click **Attach existing**.</span></span>

    ![Anexar disco de dados](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. <span data-ttu-id="59d15-129">Clique em **Local**.</span><span class="sxs-lookup"><span data-stu-id="59d15-129">Click **Location**.</span></span> <span data-ttu-id="59d15-130">exibem contas de armazenamento disponível Hello.</span><span class="sxs-lookup"><span data-stu-id="59d15-130">hello available storage accounts display.</span></span> <span data-ttu-id="59d15-131">Em seguida, selecione uma conta de armazenamento apropriada daquelas listadas.</span><span class="sxs-lookup"><span data-stu-id="59d15-131">Next, select an appropriate storage account from those listed.</span></span>

    ![Fornecer conta de armazenamento de disco](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. <span data-ttu-id="59d15-133">A **Conta de armazenamento** contém um ou mais contêineres que contêm unidades de disco (vhds).</span><span class="sxs-lookup"><span data-stu-id="59d15-133">A **Storage account** holds one or more containers that contain disk drives (vhds).</span></span> <span data-ttu-id="59d15-134">Selecione o contêiner apropriado Olá daqueles listados.</span><span class="sxs-lookup"><span data-stu-id="59d15-134">Select hello appropriate container from those listed.</span></span>

    ![Fornecer o contêiner de virtual-machines-windows](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. <span data-ttu-id="59d15-136">Olá **vhds** painel lista de unidades de disco Olá mantidas no contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="59d15-136">hello **vhds** panel lists hello disk drives held in hello container.</span></span> <span data-ttu-id="59d15-137">Clique em um dos discos hello e, em seguida, clique em Selecionar.</span><span class="sxs-lookup"><span data-stu-id="59d15-137">Click one of hello disks, and then click Select.</span></span>

    ![Fornecer a imagem de disco para virtual-machines-windows](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. <span data-ttu-id="59d15-139">Olá **anexar o disco existente** painel exibe novamente, com o local de saudação que contém a conta de armazenamento hello, contêiner e máquina virtual do disco rígido (vhd) selecionado tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="59d15-139">hello **Attach existing disk** panel displays again, with hello location containing hello storage account, container, and selected hard disk (vhd) tooadd toohello virtual machine.</span></span>

  <span data-ttu-id="59d15-140">Definir **cache de Host** toonone ou leitura somente, em seguida, clique em Okey.</span><span class="sxs-lookup"><span data-stu-id="59d15-140">Set **Host caching** toonone or Read only, then click OK.</span></span>

    ![Disco de dados anexado com êxito](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
