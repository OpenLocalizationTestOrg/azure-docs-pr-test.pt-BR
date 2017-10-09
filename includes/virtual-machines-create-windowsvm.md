1. <span data-ttu-id="30b10-101">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="30b10-101">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="30b10-102">Iniciando na parte superior esquerda do hello, clique em **Novo > computação > Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="30b10-102">Starting in hello upper left, click **New > Compute > Windows Server 2016 Datacenter**.</span></span>

    ![Navegue toohello imagens de VM do Azure no portal de saudação](./media/virtual-machines-common-portal-create-fqdn/marketplace-new.png)

3. <span data-ttu-id="30b10-104">Na Olá Datacenter do Windows Server 2016, selecione o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="30b10-104">On hello Windows Server 2016 Datacenter, select hello Classic deployment model.</span></span> <span data-ttu-id="30b10-105">Clique em Criar.</span><span class="sxs-lookup"><span data-stu-id="30b10-105">Click Create.</span></span>

    ![Captura de tela que mostra imagens de VM do Azure Olá disponíveis no portal de saudação](./media/virtual-machines-common-portal-create-fqdn/deployment-classic-model.png)

## <a name="1-basics-blade"></a><span data-ttu-id="30b10-107">1. Folha de Noções básicas</span><span class="sxs-lookup"><span data-stu-id="30b10-107">1. Basics blade</span></span>

<span data-ttu-id="30b10-108">folha de Noções básicas de saudação solicita informações administrativas para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="30b10-108">hello Basics blade requests administrative information for hello virtual machine.</span></span>

1. <span data-ttu-id="30b10-109">Insira um **nome** para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="30b10-109">Enter a **Name** for hello virtual machine.</span></span> <span data-ttu-id="30b10-110">No exemplo hello, _HeroVM_ é Olá nome da máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="30b10-110">In hello example, _HeroVM_ is hello name of hello virtual machine.</span></span> <span data-ttu-id="30b10-111">nome de saudação deve ser de 1 a 15 caracteres e não pode conter caracteres especiais.</span><span class="sxs-lookup"><span data-stu-id="30b10-111">hello name must be 1-15 characters long and it cannot contain special characters.</span></span>

2. <span data-ttu-id="30b10-112">Insira um **nome de usuário** e um forte **senha** que são usada toocreate uma conta local Olá VM.</span><span class="sxs-lookup"><span data-stu-id="30b10-112">Enter a **User name** and a strong **Password** that are used toocreate a local account on hello VM.</span></span> <span data-ttu-id="30b10-113">Olá conta local é usada toosign em tooand gerenciar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="30b10-113">hello local account is used toosign in tooand manage hello VM.</span></span> <span data-ttu-id="30b10-114">No exemplo hello, _azureuser_ é o nome de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="30b10-114">In hello example, _azureuser_ is hello user name.</span></span>

 <span data-ttu-id="30b10-115">Olá senha deve ter 8 123 caracteres e atender aos três das quatro seguintes requisitos de complexidade Olá: caractere minúscula, caractere um maiusculo, um número e um caractere especial.</span><span class="sxs-lookup"><span data-stu-id="30b10-115">hello password must be 8-123 characters long and meet three out of hello four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="30b10-116">Veja mais sobre os [requisitos de nome de usuário e senha](../articles/virtual-machines/windows/faq.md).</span><span class="sxs-lookup"><span data-stu-id="30b10-116">See more about [username and password requirements](../articles/virtual-machines/windows/faq.md).</span></span>

3. <span data-ttu-id="30b10-117">Olá **assinatura** é opcional.</span><span class="sxs-lookup"><span data-stu-id="30b10-117">hello **Subscription** is optional.</span></span> <span data-ttu-id="30b10-118">Uma configuração comum é "Pré-pago".</span><span class="sxs-lookup"><span data-stu-id="30b10-118">One common setting is "Pay-As-You-Go".</span></span>

4. <span data-ttu-id="30b10-119">Selecione uma existente **grupo de recursos** ou nome de saudação do tipo para um novo.</span><span class="sxs-lookup"><span data-stu-id="30b10-119">Select an existing **Resource group** or type hello name for a new one.</span></span> <span data-ttu-id="30b10-120">No exemplo hello, _HeroVMRG_ é nome Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="30b10-120">In hello example, _HeroVMRG_ is hello name of hello resource group.</span></span>

5. <span data-ttu-id="30b10-121">Selecione um datacenter do Azure **local** onde você deseja Olá toorun VM.</span><span class="sxs-lookup"><span data-stu-id="30b10-121">Select an Azure datacenter **Location** where you want hello VM toorun.</span></span> <span data-ttu-id="30b10-122">No exemplo hello, **Leste dos EUA** é Olá local.</span><span class="sxs-lookup"><span data-stu-id="30b10-122">In hello example, **East US** is hello location.</span></span>

6. <span data-ttu-id="30b10-123">Quando terminar, clique em **próximo** toocontinue toohello próxima folha.</span><span class="sxs-lookup"><span data-stu-id="30b10-123">When you are done, click **Next** toocontinue toohello next blade.</span></span>

    ![Captura de tela que mostra as configurações de saudação na folha de Noções básicas de saudação para configurar uma VM do Azure](./media/virtual-machines-common-portal-create-fqdn/basics-blade-classic.png)

## <a name="2-size-blade"></a><span data-ttu-id="30b10-125">2. Folha Tamanho</span><span class="sxs-lookup"><span data-stu-id="30b10-125">2. Size blade</span></span>

<span data-ttu-id="30b10-126">folha de tamanho de saudação identifica os detalhes de configuração de saudação de saudação VM e lista as várias opções que incluem o sistema operacional, o número de processadores, o tipo de armazenamento de disco e custos estimados de uso mensal.</span><span class="sxs-lookup"><span data-stu-id="30b10-126">hello Size blade identifies hello configuration details of hello VM, and lists various choices that include OS, number of processors, disk storage type, and estimated monthly usage costs.</span></span>  

<span data-ttu-id="30b10-127">Escolha um tamanho de VM e, em seguida, clique em **selecione** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="30b10-127">Choose a VM size, and then click **Select** toocontinue.</span></span> <span data-ttu-id="30b10-128">Neste exemplo, _DS1_\__V2 padrão_ é o tamanho da VM hello.</span><span class="sxs-lookup"><span data-stu-id="30b10-128">In this example, _DS1_\__V2 Standard_ is hello VM size.</span></span>

  ![Captura de tela da folha de tamanho de saudação que mostra Olá tamanhos de VM do Azure que você pode selecionar](./media/virtual-machines-common-portal-create-fqdn/vm-size-classic.png)


## <a name="3-settings-blade"></a><span data-ttu-id="30b10-130">3. Folha de configurações</span><span class="sxs-lookup"><span data-stu-id="30b10-130">3. Settings blade</span></span>

<span data-ttu-id="30b10-131">folha de configurações de saudação solicitações de opções de armazenamento e rede.</span><span class="sxs-lookup"><span data-stu-id="30b10-131">hello Settings blade requests storage and network options.</span></span> <span data-ttu-id="30b10-132">Você pode aceitar as configurações padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="30b10-132">You can accept hello default settings.</span></span> <span data-ttu-id="30b10-133">O Azure cria entradas apropriadas quando necessário.</span><span class="sxs-lookup"><span data-stu-id="30b10-133">Azure creates appropriate entries where necessary.</span></span>

<span data-ttu-id="30b10-134">Se você selecionou um tamanho de máquina virtual que dá suporte a isso, poderá experimentar o Armazenamento Premium do Azure, selecionando Premium (SSD) em Tipo de disco.</span><span class="sxs-lookup"><span data-stu-id="30b10-134">If you selected a virtual machine size that supports it, you can try Azure Premium Storage by selecting Premium (SSD) in Disk type.</span></span>

<span data-ttu-id="30b10-135">Quando terminar de fazer as alterações, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="30b10-135">When you're done making changes, click **OK**.</span></span>

## <a name="4-summary-blade"></a><span data-ttu-id="30b10-136">4. Folha de Resumo</span><span class="sxs-lookup"><span data-stu-id="30b10-136">4. Summary blade</span></span>

<span data-ttu-id="30b10-137">folha de resumo de saudação lista configurações de Olá especificadas em folhas de saudação anterior.</span><span class="sxs-lookup"><span data-stu-id="30b10-137">hello Summary blade lists hello settings specified in hello previous blades.</span></span> <span data-ttu-id="30b10-138">Clique em **Okey** quando estiver pronto toomake imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="30b10-138">Click **OK** when you're ready toomake hello image.</span></span>

 ![Relatório de resumo de folha fornecendo configurações especificadas da máquina virtual de saudação](./media/virtual-machines-common-portal-create-fqdn/summary-blade-classic.png)

<span data-ttu-id="30b10-140">Após a criação de máquina virtual de hello, portal Olá lista Olá nova máquina virtual em **todos os recursos**e exibe um bloco de máquina virtual de saudação no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="30b10-140">After hello virtual machine is created, hello portal lists hello new virtual machine under **All resources**, and displays a tile of hello virtual machine on hello dashboard.</span></span> <span data-ttu-id="30b10-141">Olá correspondente nuvem serviço e conta de armazenamento também são criadas e listadas.</span><span class="sxs-lookup"><span data-stu-id="30b10-141">hello corresponding cloud service and storage account also are created and listed.</span></span> <span data-ttu-id="30b10-142">Máquina virtual de saudação e o serviço de nuvem são iniciados automaticamente e seu status é listado como **executando**.</span><span class="sxs-lookup"><span data-stu-id="30b10-142">Both hello virtual machine and cloud service are started automatically and their status is listed as **Running**.</span></span>

 ![Configurar o agente de VM e hello pontos de extremidade da máquina virtual de saudação](./media/virtual-machines-common-portal-create-fqdn/portal-with-new-vm.png)
