


<span data-ttu-id="19be8-101">Os conjuntos de disponibilidade ajudam a manter as máquinas virtuais disponíveis em caso de tempo de inatividade (por exemplo, durante a manutenção).</span><span class="sxs-lookup"><span data-stu-id="19be8-101">An availability set helps keep your virtual machines available during downtime, such as during maintenance.</span></span> <span data-ttu-id="19be8-102">Colocação de dois ou mais máquinas virtuais configuradas de forma semelhante em um conjunto de disponibilidade cria Olá redundância necessário toomaintain disponibilidade de aplicativos de saudação ou serviços que sua máquina virtual é executada.</span><span class="sxs-lookup"><span data-stu-id="19be8-102">Placing two or more similarly configured virtual machines in an availability set creates hello redundancy needed toomaintain availability of hello applications or services that your virtual machine runs.</span></span> <span data-ttu-id="19be8-103">Para obter detalhes sobre como isso funciona, consulte [gerenciar Olá disponibilidade das máquinas virtuais][Manage hello availability of virtual machines].</span><span class="sxs-lookup"><span data-stu-id="19be8-103">For details about how this works, see [Manage hello availability of virtual machines][Manage hello availability of virtual machines].</span></span>

<span data-ttu-id="19be8-104">É um toouse de prática recomendada conjuntos de disponibilidade e balanceamento de carga de pontos de extremidade toohelp Certifique-se de que o aplicativo estará sempre disponível e funcionando com eficiência.</span><span class="sxs-lookup"><span data-stu-id="19be8-104">It's a best practice toouse both availability sets and load-balancing endpoints toohelp ensure that your application is always available and running efficiently.</span></span> <span data-ttu-id="19be8-105">Para obter detalhes sobre os pontos de extremidade com balanceamento de carga, consulte [Balanceamento de carga para os serviços de infraestrutura do Azure][Load balancing for Azure infrastructure services].</span><span class="sxs-lookup"><span data-stu-id="19be8-105">For details about load-balanced endpoints, see [Load balancing for Azure infrastructure services][Load balancing for Azure infrastructure services].</span></span>

<span data-ttu-id="19be8-106">Você pode adicionar máquinas virtuais clássicas a um conjunto de disponibilidade usando uma das duas opções:</span><span class="sxs-lookup"><span data-stu-id="19be8-106">You can add classic virtual machines into an availability set by using one of two options:</span></span>

* <span data-ttu-id="19be8-107">[Opção 1: Criar uma máquina virtual e um conjunto de disponibilidade em Olá mesmo tempo][Option 1: Create a virtual machine and an availability set at hello same time].</span><span class="sxs-lookup"><span data-stu-id="19be8-107">[Option 1: Create a virtual machine and an availability set at hello same time][Option 1: Create a virtual machine and an availability set at hello same time].</span></span> <span data-ttu-id="19be8-108">Em seguida, adicione o novo toohello de máquinas virtuais definido quando você criar essas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="19be8-108">Then, add new virtual machines toohello set when you create those virtual machines.</span></span>
* <span data-ttu-id="19be8-109">[Opção 2: Adicionar um conjunto de disponibilidade de tooan de máquina virtual existente][Option 2: Add an existing virtual machine tooan availability set].</span><span class="sxs-lookup"><span data-stu-id="19be8-109">[Option 2: Add an existing virtual machine tooan availability set][Option 2: Add an existing virtual machine tooan availability set].</span></span>

> [!NOTE]
> <span data-ttu-id="19be8-110">No modelo clássico Olá Olá máquinas virtuais que você deseja tooput no mesmo conjunto de disponibilidade deve pertencer toohello mesmo serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="19be8-110">In hello classic model, virtual machines that you want tooput in hello same availability set must belong toohello same cloud service.</span></span>
> 
> 

## <span data-ttu-id="19be8-111"><a id="createset"></a>Opção 1: criar uma máquina virtual e um conjunto de disponibilidade em Olá mesmo tempo</span><span class="sxs-lookup"><span data-stu-id="19be8-111"><a id="createset"> </a>Option 1: Create a virtual machine and an availability set at hello same time</span></span>
<span data-ttu-id="19be8-112">Você pode usar o portal do Azure hello ou do Azure PowerShell comandos toodo isso.</span><span class="sxs-lookup"><span data-stu-id="19be8-112">You can use either hello Azure portal or Azure PowerShell commands toodo this.</span></span>

<span data-ttu-id="19be8-113">Olá toouse portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="19be8-113">toouse hello Azure portal:</span></span>

1. <span data-ttu-id="19be8-114">Se você ainda não fez isso, entre no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="19be8-114">If you haven't already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="19be8-115">No menu de hub hello, clique em **+ novo**e, em seguida, clique em **Máquina Virtual**.</span><span class="sxs-lookup"><span data-stu-id="19be8-115">On hello hub menu, click **+ New**, and then click **Virtual Machine**.</span></span>
   
    ![Texto Alt da imagem](./media/virtual-machines-common-classic-configure-availability/ChooseVMImage.png)
3. <span data-ttu-id="19be8-117">Selecione a imagem de máquina virtual do Marketplace Olá desejar toouse.</span><span class="sxs-lookup"><span data-stu-id="19be8-117">Select hello Marketplace virtual machine image you wish toouse.</span></span> <span data-ttu-id="19be8-118">Você pode escolher toocreate uma máquina virtual Linux ou Windows.</span><span class="sxs-lookup"><span data-stu-id="19be8-118">You can choose toocreate a Linux or Windows virtual machine.</span></span>
4. <span data-ttu-id="19be8-119">Olá selecionada a máquina virtual, verifique se esse modelo de implantação hello está definido muito**clássico** e, em seguida, clique em **criar**</span><span class="sxs-lookup"><span data-stu-id="19be8-119">For hello selected virtual machine, verify that hello deployment model is set too**Classic** and then click **Create**</span></span>
   
    ![Texto Alt da imagem](./media/virtual-machines-common-classic-configure-availability/ChooseClassicModel.png)
5. <span data-ttu-id="19be8-121">Insira um nome da máquina virtual, nome de usuário e senha (para computadores Windows) ou a chave pública SSH (para computadores Linux).</span><span class="sxs-lookup"><span data-stu-id="19be8-121">Enter a virtual machine name, user name and password (for Windows machines) or SSH public key (for Linux machines).</span></span> 
6. <span data-ttu-id="19be8-122">Escolha o tamanho da VM hello e, em seguida, clique em **selecione** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="19be8-122">Choose hello VM size and then click **Select** toocontinue.</span></span>
7. <span data-ttu-id="19be8-123">Escolha **configuração opcional > conjunto de disponibilidade**e selecione o conjunto de disponibilidade Olá desejar tooadd Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="19be8-123">Choose **Optional Configuration > Availability set**, and select hello availability set you wish tooadd hello virtual machine to.</span></span>
   
    ![Texto Alt da imagem](./media/virtual-machines-common-classic-configure-availability/ChooseAvailabilitySet.png) 
8. <span data-ttu-id="19be8-125">Analise suas definições de configuração.</span><span class="sxs-lookup"><span data-stu-id="19be8-125">Review your configuration settings.</span></span> <span data-ttu-id="19be8-126">Quando tiver concluído, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="19be8-126">When you're done, click **Create**.</span></span>
9. <span data-ttu-id="19be8-127">Enquanto o Azure cria sua máquina virtual, você pode acompanhar o progresso de saudação em **máquinas virtuais** no menu de hub hello.</span><span class="sxs-lookup"><span data-stu-id="19be8-127">While Azure creates your virtual machine, you can track hello progress under **Virtual Machines** in hello hub menu.</span></span>

<span data-ttu-id="19be8-128">toouse do Azure PowerShell comandos toocreate uma máquina virtual do Azure e adicioná-lo tooa conjunto de disponibilidade novo ou existente, consulte [toocreate de usar o PowerShell do Azure e pré-configurar máquinas virtuais baseadas em Windows](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="19be8-128">toouse Azure PowerShell commands toocreate an Azure virtual machine and add it tooa new or existing availability set, see [Use Azure PowerShell toocreate and preconfigure Windows-based virtual machines](../articles/virtual-machines/windows/classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="19be8-129"><a id="addmachine"></a>Opção 2: adicionar um conjunto de disponibilidade de tooan de máquina virtual existente</span><span class="sxs-lookup"><span data-stu-id="19be8-129"><a id="addmachine"> </a>Option 2: Add an existing virtual machine tooan availability set</span></span>
<span data-ttu-id="19be8-130">Em Olá portal do Azure, você pode adicionar tooan existente de máquinas virtuais clássicas existente conjunto de disponibilidade ou criar um novo para eles.</span><span class="sxs-lookup"><span data-stu-id="19be8-130">In hello Azure portal, you can add existing classic virtual machines tooan existing availability set or create a new one for them.</span></span> <span data-ttu-id="19be8-131">(Lembre-se de que as máquinas virtuais Olá Olá mesmo conjunto de disponibilidade deve pertencer toohello mesmo serviço de nuvem.) etapas de saudação são quase Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="19be8-131">(Keep in mind that hello virtual machines in hello same availability set must belong toohello same cloud service.) hello steps are almost hello same.</span></span> <span data-ttu-id="19be8-132">Com o Azure PowerShell, você pode adicionar conjunto de disponibilidade existente do hello máquina virtual tooan.</span><span class="sxs-lookup"><span data-stu-id="19be8-132">With Azure PowerShell, you can add hello virtual machine tooan existing availability set.</span></span>

1. <span data-ttu-id="19be8-133">Se você ainda não tiver feito isso, entre no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="19be8-133">If you have not already done so, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="19be8-134">No menu de Hub hello, clique em **máquinas virtuais (clássicas)**.</span><span class="sxs-lookup"><span data-stu-id="19be8-134">On hello Hub menu, click **Virtual Machines (classic)**.</span></span>
   
    ![Texto Alt da imagem](./media/virtual-machines-common-classic-configure-availability/ChooseClassicVM.png)
3. <span data-ttu-id="19be8-136">Na lista de saudação de máquinas virtuais, selecione o nome de Olá da máquina virtual de saudação que você deseja que o conjunto de toohello tooadd.</span><span class="sxs-lookup"><span data-stu-id="19be8-136">From hello list of virtual machines, select hello name of hello virtual machine that you want tooadd toohello set.</span></span>
4. <span data-ttu-id="19be8-137">Escolha **conjunto de disponibilidade** da máquina virtual de saudação **configurações**.</span><span class="sxs-lookup"><span data-stu-id="19be8-137">Choose **Availability set** from hello virtual machine **Settings**.</span></span>
   
    ![Texto Alt da imagem](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetSettings.png)
5. <span data-ttu-id="19be8-139">Selecione conjunto de disponibilidade Olá que desejar tooadd Olá máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="19be8-139">Select hello availability set you wish tooadd hello virtual machine to.</span></span> <span data-ttu-id="19be8-140">máquina virtual de saudação deve pertencer toohello mesmo serviço em nuvem como um conjunto de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="19be8-140">hello virtual machine must belong toohello same cloud service as hello availability set.</span></span>
   
    ![Texto Alt da imagem](./media/virtual-machines-common-classic-configure-availability/AvailabilitySetPicker.png)
6. <span data-ttu-id="19be8-142">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="19be8-142">Click **Save**.</span></span>

<span data-ttu-id="19be8-143">toouse comandos do PowerShell do Azure, abra uma sessão do PowerShell do Azure de nível de administrador e execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="19be8-143">toouse Azure PowerShell commands, open an administrator-level Azure PowerShell session and run hello following command.</span></span> <span data-ttu-id="19be8-144">Espaços reservados de saudação (como &lt;VmCloudServiceName&gt;), substituir tudo entre aspas hello, incluindo hello < e > caracteres, com hello corrigir nomes.</span><span class="sxs-lookup"><span data-stu-id="19be8-144">For hello placeholders (such as &lt;VmCloudServiceName&gt;), replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

> [!NOTE]
> <span data-ttu-id="19be8-145">Olá VM pode ter toofinish toobe reiniciado adicioná-lo toohello conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="19be8-145">hello virtual machine might have toobe restarted toofinish adding it toohello availability set.</span></span>
> 
> 

<!-- LINKS -->
[Option 1: Create a virtual machine and an availability set at hello same time]: #createset
[Option 2: Add an existing virtual machine tooan availability set]: #addmachine

[Load balancing for Azure infrastructure services]: ../articles/virtual-machines/virtual-machines-linux-load-balance.md
[Manage hello availability of virtual machines]:../articles/virtual-machines/linux/manage-availability.md

[Create a virtual machine running Windows]: ../articles/virtual-machines/virtual-machines-windows-hero-tutorial.md
[Virtual Network overview]: ../articles/virtual-network/virtual-networks-overview.md

