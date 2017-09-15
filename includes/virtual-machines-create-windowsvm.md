1. <span data-ttu-id="84d87-101">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="84d87-101">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="84d87-102">Começando no canto superior esquerdo, clique em **Nova > Computação > Datacenter do Windows Server 2016**.</span><span class="sxs-lookup"><span data-stu-id="84d87-102">Starting in the upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span></span>

    ![Navegar até as imagens de VM do Azure no portal](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. <span data-ttu-id="84d87-104">No Datacenter do Windows Server 2016, selecione o modelo de implantação Clássico.</span><span class="sxs-lookup"><span data-stu-id="84d87-104">On the Windows Server 2016 Datacenter, select the Classic deployment model.</span></span> <span data-ttu-id="84d87-105">Clique em Criar.</span><span class="sxs-lookup"><span data-stu-id="84d87-105">Click Create.</span></span>

    ![Captura de tela que mostra as imagens da VM do Azure disponíveis no portal](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a><span data-ttu-id="84d87-107">1. Folha de Noções básicas</span><span class="sxs-lookup"><span data-stu-id="84d87-107">1. Basics blade</span></span>

<span data-ttu-id="84d87-108">A folha de Noções básicas solicita informações administrativas da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="84d87-108">The Basics blade requests administrative information for the virtual machine.</span></span>

1. <span data-ttu-id="84d87-109">Insira um **Nome** para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="84d87-109">Enter a **Name** for the virtual machine.</span></span> <span data-ttu-id="84d87-110">Neste exemplo, o nome da máquina virtual é _HeroVM_.</span><span class="sxs-lookup"><span data-stu-id="84d87-110">In the example, _HeroVM_ is the name of the virtual machine.</span></span> <span data-ttu-id="84d87-111">O nome deve ter de 1 a 15 caracteres e não pode conter caracteres especiais.</span><span class="sxs-lookup"><span data-stu-id="84d87-111">The name must be 1-15 characters long and it cannot contain special characters.</span></span>

2. <span data-ttu-id="84d87-112">Insira um **Nome de usuário** e uma **Senha** forte que serão usados para criar uma conta local na VM.</span><span class="sxs-lookup"><span data-stu-id="84d87-112">Enter a **User name** and a strong **Password** that are used to create a local account on the VM.</span></span> <span data-ttu-id="84d87-113">A conta local é usada para conectar e gerenciar a VM.</span><span class="sxs-lookup"><span data-stu-id="84d87-113">The local account is used to sign in to and manage the VM.</span></span> <span data-ttu-id="84d87-114">Neste exemplo, o nome de usuário é _azureuser_.</span><span class="sxs-lookup"><span data-stu-id="84d87-114">In the example, _azureuser_ is the user name.</span></span>

 <span data-ttu-id="84d87-115">A senha deve ter de 8 a 123 caracteres e atender três dos quatro requisitos de complexidade a seguir: um caractere minúsculo, um caractere maiúsculo, um número e um caractere especial.</span><span class="sxs-lookup"><span data-stu-id="84d87-115">The password must be 8-123 characters long and meet three out of the four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="84d87-116">Veja mais sobre os [requisitos de nome de usuário e senha](../articles/virtual-machines/windows/faq.md).</span><span class="sxs-lookup"><span data-stu-id="84d87-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span></span>

3. <span data-ttu-id="84d87-117">A **Assinatura** é opcional.</span><span class="sxs-lookup"><span data-stu-id="84d87-117">The **Subscription** is optional.</span></span> <span data-ttu-id="84d87-118">Uma configuração comum é "Pré-pago".</span><span class="sxs-lookup"><span data-stu-id="84d87-118">One common setting is "Pay-As-You-Go".</span></span>

4. <span data-ttu-id="84d87-119">Selecione um **Grupo de recursos** existente ou digite o nome de um novo.</span><span class="sxs-lookup"><span data-stu-id="84d87-119">Select an existing **Resource group** or type the name for a new one.</span></span> <span data-ttu-id="84d87-120">Neste exemplo, o nome do grupo de recursos é _HeroVMRG_.</span><span class="sxs-lookup"><span data-stu-id="84d87-120">In the example, _HeroVMRG_ is the name of the resource group.</span></span>

5. <span data-ttu-id="84d87-121">Selecione um **Local** de datacenter do Azure no qual você deseja que a VM seja executada.</span><span class="sxs-lookup"><span data-stu-id="84d87-121">Select an Azure datacenter **Location** where you want the VM to run.</span></span> <span data-ttu-id="84d87-122">Neste exemplo, o local é **Leste dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="84d87-122">In the example, **East US** is the location.</span></span>

6. <span data-ttu-id="84d87-123">Ao terminar, clique em **Avançar** para continuar na próxima folha.</span><span class="sxs-lookup"><span data-stu-id="84d87-123">When you are done, click **Next** to continue to the next blade.</span></span>

    ![Captura de tela que mostra as configurações na folha Noções básicas para configurar uma VM do Azure](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a><span data-ttu-id="84d87-125">2. Folha Tamanho</span><span class="sxs-lookup"><span data-stu-id="84d87-125">2. Size blade</span></span>

<span data-ttu-id="84d87-126">A folha Tamanho identifica os detalhes de configuração da VM e lista várias opções que incluem o sistema operacional, o número de processadores, o tipo de armazenamento em disco e os custos mensais estimados de uso.</span><span class="sxs-lookup"><span data-stu-id="84d87-126">The Size blade identifies the configuration details of the VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span></span>  

<span data-ttu-id="84d87-127">Escolha um tamanho de VM e, em seguida, clique em **Selecionar** para continuar.</span><span class="sxs-lookup"><span data-stu-id="84d87-127">Choose a VM size, and then click **Select** to continue.</span></span> <span data-ttu-id="84d87-128">Neste exemplo, o tamanho da VM é _DS1_\__V2 Standard_.</span><span class="sxs-lookup"><span data-stu-id="84d87-128">In this example, _DS1_\__V2 Standard_ is the VM size.</span></span>

  ![Captura de tela da folha Tamanho que mostra a VM do Azure que você pode selecionar](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a><span data-ttu-id="84d87-130">3. Folha de configurações</span><span class="sxs-lookup"><span data-stu-id="84d87-130">3. Settings blade</span></span>

<span data-ttu-id="84d87-131">A folha de Configurações solicita opções de armazenamento e de rede.</span><span class="sxs-lookup"><span data-stu-id="84d87-131">The Settings blade requests storage and network options.</span></span> <span data-ttu-id="84d87-132">Você pode aceitar as configurações padrão.</span><span class="sxs-lookup"><span data-stu-id="84d87-132">You can accept the default settings.</span></span> <span data-ttu-id="84d87-133">O Azure cria entradas apropriadas quando necessário.</span><span class="sxs-lookup"><span data-stu-id="84d87-133">Azure creates appropriate entries where necessary.</span></span>

<span data-ttu-id="84d87-134">Se você selecionou um tamanho de máquina virtual que dá suporte a isso, poderá experimentar o Armazenamento Premium do Azure, selecionando Premium (SSD) em Tipo de disco.</span><span class="sxs-lookup"><span data-stu-id="84d87-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span></span>

<span data-ttu-id="84d87-135">Quando terminar de fazer as alterações, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="84d87-135">When you're done making changes, click **OK**.</span></span>

## <a name="4-summary-blade"></a><span data-ttu-id="84d87-136">4. Folha de Resumo</span><span class="sxs-lookup"><span data-stu-id="84d87-136">4. Summary blade</span></span>

<span data-ttu-id="84d87-137">A folha de Resumo lista as configurações especificadas nas folhas anteriores.</span><span class="sxs-lookup"><span data-stu-id="84d87-137">The Summary blade lists the settings specified in the previous blades.</span></span> <span data-ttu-id="84d87-138">Clique em **OK** quando estiver pronto para criar a imagem.</span><span class="sxs-lookup"><span data-stu-id="84d87-138">Click **OK** when you're ready to make the image.</span></span>

 ![Relatório da folha de Resumo fornecendo as configurações especificadas da máquina virtual](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

<span data-ttu-id="84d87-140">Depois que a máquina virtual é criada, o portal lista a nova máquina virtual em **Todos os recursos** e exibe um bloco da máquina virtual no painel.</span><span class="sxs-lookup"><span data-stu-id="84d87-140">After the virtual machine is created, the portal lists the new virtual machine under **All resources**, and displays a tile of the virtual machine on the dashboard.</span></span> <span data-ttu-id="84d87-141">O serviço de nuvem correspondente e a conta de armazenamento também são criados e listados.</span><span class="sxs-lookup"><span data-stu-id="84d87-141">The corresponding cloud service and storage account also are created and listed.</span></span> <span data-ttu-id="84d87-142">A máquina virtual e o serviço de nuvem são iniciados automaticamente, e seu status é listado como **Em Execução**.</span><span class="sxs-lookup"><span data-stu-id="84d87-142">Both the virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

 ![Configurar Agente de VM e os pontos de extremidade da máquina virtual](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
