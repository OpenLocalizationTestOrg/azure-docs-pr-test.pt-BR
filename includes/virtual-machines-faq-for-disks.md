# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="1a884-101">Perguntas frequentes sobre discos de VM IaaS do Azure e discos premium gerenciados e não gerenciados</span><span class="sxs-lookup"><span data-stu-id="1a884-101">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="1a884-102">Este artigo responde a algumas perguntas frequentes sobre o Azure Managed Disks e o Armazenamento Premium do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a884-102">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="1a884-103">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="1a884-103">Managed Disks</span></span>

<span data-ttu-id="1a884-104">**O que é o Azure Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="1a884-104">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="1a884-105">Managed Disks é um recurso que simplifica o gerenciamento de disco para VMs IaaS do Azure manipulando o gerenciamento de conta de armazenamento para você.</span><span class="sxs-lookup"><span data-stu-id="1a884-105">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="1a884-106">Para obter mais informações, consulte Olá [visão geral de discos gerenciados](../articles/virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1a884-106">For more information, see hello [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="1a884-107">**Se eu criar um disco gerenciado standard com base em um VHD existente que tem 80 GB, quanto isso custará?**</span><span class="sxs-lookup"><span data-stu-id="1a884-107">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="1a884-108">Um disco gerenciado padrão criado a partir de um VHD de 80 GB é tratado como Olá próximo padrão tamanho de disco disponível, que é um disco S10.</span><span class="sxs-lookup"><span data-stu-id="1a884-108">A standard managed disk created from an 80-GB VHD is treated as hello next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="1a884-109">Você será cobrado de acordo toohello S10 disco preços.</span><span class="sxs-lookup"><span data-stu-id="1a884-109">You're charged according toohello S10 disk pricing.</span></span> <span data-ttu-id="1a884-110">Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="1a884-110">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="1a884-111">**Existem custos de transação de discos gerenciados standard?**</span><span class="sxs-lookup"><span data-stu-id="1a884-111">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="1a884-112">Sim.</span><span class="sxs-lookup"><span data-stu-id="1a884-112">Yes.</span></span> <span data-ttu-id="1a884-113">Você é cobrado por cada transação.</span><span class="sxs-lookup"><span data-stu-id="1a884-113">You're charged for each transaction.</span></span> <span data-ttu-id="1a884-114">Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="1a884-114">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="1a884-115">**Para um disco gerenciado standard, serei ser cobrado para tamanho real de Olá Olá dados hello ou para capacidade de saudação provisionada de disco Olá?**</span><span class="sxs-lookup"><span data-stu-id="1a884-115">**For a standard managed disk, will I be charged for hello actual size of hello data on hello disk or for hello provisioned capacity of hello disk?**</span></span>

<span data-ttu-id="1a884-116">Você será cobrado com base na capacidade de saudação provisionada de disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="1a884-116">You're charged based on hello provisioned capacity of hello disk.</span></span> <span data-ttu-id="1a884-117">Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="1a884-117">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="1a884-118">**O preço dos discos premium gerenciados é diferente do preço dos discos não gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="1a884-118">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="1a884-119">saudação de preços de discos premium gerenciado é Olá igual a discos premium não gerenciado.</span><span class="sxs-lookup"><span data-stu-id="1a884-119">hello pricing of premium managed disks is hello same as unmanaged premium disks.</span></span>

<span data-ttu-id="1a884-120">**Alterar Olá armazenamento tipo de conta (Standard ou Premium) de meus discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="1a884-120">**Can I change hello storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="1a884-121">Sim.</span><span class="sxs-lookup"><span data-stu-id="1a884-121">Yes.</span></span> <span data-ttu-id="1a884-122">Você pode alterar o tipo de conta de armazenamento Olá discos gerenciados usando Olá portal do Azure, PowerShell ou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a884-122">You can change hello storage account type of your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="1a884-123">**Há uma maneira que eu possa copiar ou exportar uma conta de armazenamento particular de tooa de disco gerenciado?**</span><span class="sxs-lookup"><span data-stu-id="1a884-123">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="1a884-124">Sim.</span><span class="sxs-lookup"><span data-stu-id="1a884-124">Yes.</span></span> <span data-ttu-id="1a884-125">Você pode exportar os discos gerenciados usando Olá portal do Azure, PowerShell ou Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a884-125">You can export your managed disks by using hello Azure portal, PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="1a884-126">**Pode usar um arquivo VHD em uma conta de armazenamento do Azure toocreate um disco gerenciado com uma assinatura diferente?**</span><span class="sxs-lookup"><span data-stu-id="1a884-126">**Can I use a VHD file in an Azure storage account toocreate a managed disk with a different subscription?**</span></span>

<span data-ttu-id="1a884-127">Não.</span><span class="sxs-lookup"><span data-stu-id="1a884-127">No.</span></span>

<span data-ttu-id="1a884-128">**Pode usar um arquivo VHD em uma conta de armazenamento do Azure toocreate um disco gerenciado em uma região diferente?**</span><span class="sxs-lookup"><span data-stu-id="1a884-128">**Can I use a VHD file in an Azure storage account toocreate a managed disk in a different region?**</span></span>

<span data-ttu-id="1a884-129">Não.</span><span class="sxs-lookup"><span data-stu-id="1a884-129">No.</span></span>

<span data-ttu-id="1a884-130">**Existem limitações de escala para clientes que usam discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="1a884-130">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="1a884-131">Discos gerenciados elimina os limites de saudação associados às contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1a884-131">Managed Disks eliminates hello limits associated with storage accounts.</span></span> <span data-ttu-id="1a884-132">No entanto, o número de saudação de discos gerenciados por assinatura é limitado too2, 000 por padrão.</span><span class="sxs-lookup"><span data-stu-id="1a884-132">However, hello number of managed disks per subscription is limited too2,000 by default.</span></span> <span data-ttu-id="1a884-133">Você pode chamar o suporte tooincrease esse número.</span><span class="sxs-lookup"><span data-stu-id="1a884-133">You can call support tooincrease this number.</span></span>

<span data-ttu-id="1a884-134">**Posso fazer um instantâneo incremental de um disco gerenciado?**</span><span class="sxs-lookup"><span data-stu-id="1a884-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="1a884-135">Não.</span><span class="sxs-lookup"><span data-stu-id="1a884-135">No.</span></span> <span data-ttu-id="1a884-136">recurso de instantâneo atual Olá cria uma cópia completa de um disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="1a884-136">hello current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="1a884-137">No entanto, nós estamos planejando toosupport de instantâneos incrementais em Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="1a884-137">However, we are planning toosupport incremental snapshots in hello future.</span></span>

<span data-ttu-id="1a884-138">**As VMs em um conjunto de disponibilidade podem consistir de uma combinação de discos gerenciados e não gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="1a884-138">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="1a884-139">Não.</span><span class="sxs-lookup"><span data-stu-id="1a884-139">No.</span></span> <span data-ttu-id="1a884-140">Olá VMs em um conjunto de disponibilidade deve usar discos todas gerenciados ou todos os discos não gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1a884-140">hello VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="1a884-141">Quando você cria um conjunto de disponibilidade, você pode escolher qual tipo de disco desejado toouse.</span><span class="sxs-lookup"><span data-stu-id="1a884-141">When you create an availability set, you can choose which type of disks you want toouse.</span></span>

<span data-ttu-id="1a884-142">**É a opção de padrão de saudação de discos gerenciados no hello portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="1a884-142">**Is Managed Disks hello default option in hello Azure portal?**</span></span>

<span data-ttu-id="1a884-143">Não no momento, mas ela ficará padrão Olá Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="1a884-143">Not currently, but it will become hello default in hello future.</span></span>

<span data-ttu-id="1a884-144">**É possível criar um disco gerenciado vazio?**</span><span class="sxs-lookup"><span data-stu-id="1a884-144">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="1a884-145">Sim.</span><span class="sxs-lookup"><span data-stu-id="1a884-145">Yes.</span></span> <span data-ttu-id="1a884-146">Você pode criar um disco vazio.</span><span class="sxs-lookup"><span data-stu-id="1a884-146">You can create an empty disk.</span></span> <span data-ttu-id="1a884-147">Um disco gerenciado pode ser criado independentemente de uma VM, por exemplo, sem anexá-lo tooa VM.</span><span class="sxs-lookup"><span data-stu-id="1a884-147">A managed disk can be created independently of a VM, for example, without attaching it tooa VM.</span></span>

<span data-ttu-id="1a884-148">**O que é a contagem de domínios de falha de saudação com suporte para um conjunto de disponibilidade que usa discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="1a884-148">**What is hello supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="1a884-149">Dependendo da região de saudação onde o conjunto de disponibilidade de saudação que usa discos gerenciado está localizado, a contagem de domínios de falha de saudação com suporte é 2 ou 3.</span><span class="sxs-lookup"><span data-stu-id="1a884-149">Depending on hello region where hello availability set that uses Managed Disks is located, hello supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="1a884-150">**Como é a conta de armazenamento padrão de saudação para configurar um diagnóstico?**</span><span class="sxs-lookup"><span data-stu-id="1a884-150">**How is hello standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="1a884-151">Você configura uma conta de armazenamento privado para diagnóstico da VM.</span><span class="sxs-lookup"><span data-stu-id="1a884-151">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="1a884-152">Em Olá futuro, planejamos diagnóstico tooswitch tooManaged discos também.</span><span class="sxs-lookup"><span data-stu-id="1a884-152">In hello future, we plan tooswitch diagnostics tooManaged Disks as well.</span></span>

<span data-ttu-id="1a884-153">**O tipo de suporte ao Controle de Acesso Baseado em Função está disponível para o Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="1a884-153">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="1a884-154">O Managed Disks oferece suporte a três funções principais padrão:</span><span class="sxs-lookup"><span data-stu-id="1a884-154">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="1a884-155">Proprietário: pode gerenciar tudo, incluindo o acesso</span><span class="sxs-lookup"><span data-stu-id="1a884-155">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="1a884-156">Colaborador: pode gerenciar tudo, exceto o acesso</span><span class="sxs-lookup"><span data-stu-id="1a884-156">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="1a884-157">Leitor: pode ver tudo, mas não pode fazer alterações</span><span class="sxs-lookup"><span data-stu-id="1a884-157">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="1a884-158">**Há uma maneira que eu possa copiar ou exportar uma conta de armazenamento particular de tooa de disco gerenciado?**</span><span class="sxs-lookup"><span data-stu-id="1a884-158">**Is there a way that I can copy or export a managed disk tooa private storage account?**</span></span>

<span data-ttu-id="1a884-159">Você pode obter uma assinatura de acesso compartilhado somente leitura URI para Olá gerenciado em disco e usá-lo toocopy Olá conteúdo tooa privada local ou conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1a884-159">You can get a read-only shared access signature URI for hello managed disk and use it toocopy hello contents tooa private storage account or on-premises storage.</span></span>

<span data-ttu-id="1a884-160">**Posso criar uma cópia do meu disco gerenciado?**</span><span class="sxs-lookup"><span data-stu-id="1a884-160">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="1a884-161">Os clientes podem tirar um instantâneo dos seus discos gerenciados e usar Olá instantâneo toocreate outro disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="1a884-161">Customers can take a snapshot of their managed disks and then use hello snapshot toocreate another managed disk.</span></span>

<span data-ttu-id="1a884-162">**Ainda há suporte para discos não gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="1a884-162">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="1a884-163">Sim.</span><span class="sxs-lookup"><span data-stu-id="1a884-163">Yes.</span></span> <span data-ttu-id="1a884-164">Há suporte para discos gerenciados e não gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1a884-164">We support unmanaged and managed disks.</span></span> <span data-ttu-id="1a884-165">É recomendável que você use discos gerenciados para novas cargas de trabalho e migra seus discos de toomanaged cargas de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="1a884-165">We recommend that you use managed disks for new workloads and migrate your current workloads toomanaged disks.</span></span>


<span data-ttu-id="1a884-166">**Se eu criar um disco de 128 GB e, em seguida, aumentar Olá tamanho too130 GB, serei ser cobrado para tamanho de disco seguinte hello (512 GB)?**</span><span class="sxs-lookup"><span data-stu-id="1a884-166">**If I create a 128-GB disk and then increase hello size too130 GB, will I be charged for hello next disk size (512 GB)?**</span></span>

<span data-ttu-id="1a884-167">Sim.</span><span class="sxs-lookup"><span data-stu-id="1a884-167">Yes.</span></span>

<span data-ttu-id="1a884-168">**Posso criar armazenamento com redundância local, armazenamento com redundância geográfica e discos de armazenamento com redundância de zona gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="1a884-168">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="1a884-169">O Azure Managed Disks atualmente dá suporte apenas a discos gerenciados de armazenamento com redundância local.</span><span class="sxs-lookup"><span data-stu-id="1a884-169">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="1a884-170">**Posso reduzir ou diminuir o tamanho de meus discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="1a884-170">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="1a884-171">Não.</span><span class="sxs-lookup"><span data-stu-id="1a884-171">No.</span></span> <span data-ttu-id="1a884-172">Não há suporte para esse recurso no momento.</span><span class="sxs-lookup"><span data-stu-id="1a884-172">This feature is not supported currently.</span></span> 

<span data-ttu-id="1a884-173">**Alterar propriedade de nome de computador hello quando um especializada (não criada usando a ferramenta de preparação do sistema hello ou generalizado) operacional do disco do sistema é usado tooprovision uma máquina virtual?**</span><span class="sxs-lookup"><span data-stu-id="1a884-173">**Can I change hello computer name property when a specialized (not created by using hello System Preparation tool or generalized) operating system disk is used tooprovision a VM?**</span></span>

<span data-ttu-id="1a884-174">Não.</span><span class="sxs-lookup"><span data-stu-id="1a884-174">No.</span></span> <span data-ttu-id="1a884-175">Você não pode atualizar a propriedade de nome de computador hello.</span><span class="sxs-lookup"><span data-stu-id="1a884-175">You can't update hello computer name property.</span></span> <span data-ttu-id="1a884-176">Olá nova VM herda-lo do hello pai VM, que era o disco do sistema operacional Olá toocreate usado.</span><span class="sxs-lookup"><span data-stu-id="1a884-176">hello new VM inherits it from hello parent VM, which was used toocreate hello operating system disk.</span></span> 

<span data-ttu-id="1a884-177">**Onde encontrar o exemplo do Azure Resource Manager modelos toocreate VMs com discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="1a884-177">**Where can I find sample Azure Resource Manager templates toocreate VMs with managed disks?**</span></span>
* [<span data-ttu-id="1a884-178">Lista de modelos que usam o Managed Disks</span><span class="sxs-lookup"><span data-stu-id="1a884-178">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="1a884-179">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="1a884-179">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="1a884-180">Managed Disks e Criptografia de Serviço de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="1a884-180">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="1a884-181">**A Criptografia do Serviço de Armazenamento do Azure fica habilitada por padrão quando crio um disco gerenciado?**</span><span class="sxs-lookup"><span data-stu-id="1a884-181">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="1a884-182">Sim.</span><span class="sxs-lookup"><span data-stu-id="1a884-182">Yes.</span></span>

<span data-ttu-id="1a884-183">**Quem gerencia as chaves de criptografia Olá?**</span><span class="sxs-lookup"><span data-stu-id="1a884-183">**Who manages hello encryption keys?**</span></span>

<span data-ttu-id="1a884-184">A Microsoft gerencia chaves de criptografia de saudação.</span><span class="sxs-lookup"><span data-stu-id="1a884-184">Microsoft manages hello encryption keys.</span></span>

<span data-ttu-id="1a884-185">**Posso desabilitar a Criptografia do Serviço de Armazenamento para meus discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="1a884-185">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="1a884-186">Não.</span><span class="sxs-lookup"><span data-stu-id="1a884-186">No.</span></span>

<span data-ttu-id="1a884-187">**A Criptografia do Serviço de Armazenamento só está disponível em regiões específicas?**</span><span class="sxs-lookup"><span data-stu-id="1a884-187">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="1a884-188">Não.</span><span class="sxs-lookup"><span data-stu-id="1a884-188">No.</span></span> <span data-ttu-id="1a884-189">Ele está disponível em todas as regiões de saudação em discos gerenciado está disponível.</span><span class="sxs-lookup"><span data-stu-id="1a884-189">It's available in all hello regions where Managed Disks is available.</span></span> <span data-ttu-id="1a884-190">O Managed Disks está disponível em todas as regiões públicas e na Alemanha.</span><span class="sxs-lookup"><span data-stu-id="1a884-190">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="1a884-191">**Como posso descobrir se o disco gerenciado está criptografado?**</span><span class="sxs-lookup"><span data-stu-id="1a884-191">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="1a884-192">Você pode descobrir a hora de saudação quando um disco gerenciado foi criado de saudação portal do Azure, Olá CLI do Azure e do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1a884-192">You can find out hello time when a managed disk was created from hello Azure portal, hello Azure CLI, and PowerShell.</span></span> <span data-ttu-id="1a884-193">Se houver tempo Olá após 9 de junho de 2017, o disco está criptografado.</span><span class="sxs-lookup"><span data-stu-id="1a884-193">If hello time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="1a884-194">**Como faço para criptografar meus discos existentes que foram criados antes de 10 de junho de 2017?**</span><span class="sxs-lookup"><span data-stu-id="1a884-194">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="1a884-195">A partir de 10 de junho de 2017, novos dados gravados discos tooexisting gerenciado são criptografados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1a884-195">As of June 10, 2017, new data written tooexisting managed disks is automatically encrypted.</span></span> <span data-ttu-id="1a884-196">Nós também estamos planejando tooencrypt os dados existentes e criptografia Olá acontecerá assincronamente no plano de fundo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1a884-196">We are also planning tooencrypt existing data, and hello encryption will happen asynchronously in hello background.</span></span> <span data-ttu-id="1a884-197">Se você precisar criptografar os dados existentes agora, crie uma cópia do disco.</span><span class="sxs-lookup"><span data-stu-id="1a884-197">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="1a884-198">Os novos discos serão criptografados.</span><span class="sxs-lookup"><span data-stu-id="1a884-198">New disks will be encrypted.</span></span>

* [<span data-ttu-id="1a884-199">Copiar discos gerenciados usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="1a884-199">Copy managed disks by using hello Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="1a884-200">Copiar discos gerenciados usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a884-200">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="1a884-201">**Os instantâneos gerenciados e as imagens são criptografados?**</span><span class="sxs-lookup"><span data-stu-id="1a884-201">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="1a884-202">Sim.</span><span class="sxs-lookup"><span data-stu-id="1a884-202">Yes.</span></span> <span data-ttu-id="1a884-203">Todos os instantâneos e imagens criados após 9 de junho de 2017 são criptografados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1a884-203">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="1a884-204">**Pode converter máquinas virtuais com discos não gerenciados que estão localizados em contas de armazenamento ou foram discos toomanaged previamente criptografado?**</span><span class="sxs-lookup"><span data-stu-id="1a884-204">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted toomanaged disks?**</span></span>

<span data-ttu-id="1a884-205">Sim</span><span class="sxs-lookup"><span data-stu-id="1a884-205">Yes</span></span>

<span data-ttu-id="1a884-206">**Um VHD exportado de um disco gerenciado ou instantâneo também será criptografado?**</span><span class="sxs-lookup"><span data-stu-id="1a884-206">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="1a884-207">Não.</span><span class="sxs-lookup"><span data-stu-id="1a884-207">No.</span></span> <span data-ttu-id="1a884-208">Mas se você exportar um VHD tooan criptografado conta de armazenamento de um disco gerenciado criptografado ou instantâneo e, em seguida, ele é criptografado.</span><span class="sxs-lookup"><span data-stu-id="1a884-208">But if you export a VHD tooan encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="1a884-209">Discos Premium: gerenciados e não gerenciados</span><span class="sxs-lookup"><span data-stu-id="1a884-209">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="1a884-210">**Se uma VM usa uma série de tamanho que dá suporte ao Armazenamento Premium, como um DSv2, é possível anexar discos de dados standard e premium?**</span><span class="sxs-lookup"><span data-stu-id="1a884-210">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="1a884-211">Sim.</span><span class="sxs-lookup"><span data-stu-id="1a884-211">Yes.</span></span>

<span data-ttu-id="1a884-212">**É possível anexar premium e standard discos tooa tamanho séries de dados não dá suporte a armazenamento Premium, como a série D, Dv2, G ou F?**</span><span class="sxs-lookup"><span data-stu-id="1a884-212">**Can I attach both premium and standard data disks tooa size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="1a884-213">Não.</span><span class="sxs-lookup"><span data-stu-id="1a884-213">No.</span></span> <span data-ttu-id="1a884-214">Você pode anexar apenas tooVMs de discos padrão para dados que não usam uma série de tamanho que dá suporte ao armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="1a884-214">You can attach only standard data disks tooVMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="1a884-215">**Se criar um disco de dados premium com base em um VHD existente que tinha 80 GB, quanto isso custará?**</span><span class="sxs-lookup"><span data-stu-id="1a884-215">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="1a884-216">Um disco de dados premium criado a partir de um VHD de 80 GB é tratado como o tamanho de disco disponíveis para o próximo premium Olá, é um disco P10.</span><span class="sxs-lookup"><span data-stu-id="1a884-216">A premium data disk created from an 80-GB VHD is treated as hello next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="1a884-217">Você será cobrado de acordo toohello P10 disco preços.</span><span class="sxs-lookup"><span data-stu-id="1a884-217">You're charged according toohello P10 disk pricing.</span></span>

<span data-ttu-id="1a884-218">**Há transações custos toouse armazenamento Premium?**</span><span class="sxs-lookup"><span data-stu-id="1a884-218">**Are there transaction costs toouse Premium Storage?**</span></span>

<span data-ttu-id="1a884-219">Há um custo fixo para cada tamanho de disco, que vem provisionado com limites específicos de IOPS e taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="1a884-219">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="1a884-220">Olá outros custos são largura de banda de saída e a capacidade de instantâneo, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="1a884-220">hello other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="1a884-221">Para obter mais informações, consulte Olá [página de preços](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="1a884-221">For more information, see hello [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="1a884-222">**Quais são os limites de saudação de IOPS e taxa de transferência que posso obter do cache de disco Olá?**</span><span class="sxs-lookup"><span data-stu-id="1a884-222">**What are hello limits for IOPS and throughput that I can get from hello disk cache?**</span></span>

<span data-ttu-id="1a884-223">Olá combinado de limites para cache e SSD local para uma série DS são 4.000 IOPS por núcleo e 33 MB por segundo por núcleo.</span><span class="sxs-lookup"><span data-stu-id="1a884-223">hello combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="1a884-224">Olá série GS oferece a 5.000 IOPS por núcleo e 50 MB por segundo por núcleo.</span><span class="sxs-lookup"><span data-stu-id="1a884-224">hello GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="1a884-225">**É hello que SSD local tem suporte para uma VM de discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="1a884-225">**Is hello local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="1a884-226">Olá SSD local é o armazenamento temporário que acompanha uma VM de discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1a884-226">hello local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="1a884-227">Não há custo adicional para esse armazenamento temporário.</span><span class="sxs-lookup"><span data-stu-id="1a884-227">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="1a884-228">É recomendável que você não use esse toostore SSD local os dados do aplicativo porque ele não é mantido no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a884-228">We recommend that you do not use this local SSD toostore your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="1a884-229">**São existe qualquer repercussões para Olá usar de TRIM em discos premium?**</span><span class="sxs-lookup"><span data-stu-id="1a884-229">**Are there any repercussions for hello use of TRIM on premium disks?**</span></span>

<span data-ttu-id="1a884-230">Não há nenhum uso de toohello desvantagem de TRIM em discos do Azure em uma premium ou discos padrão.</span><span class="sxs-lookup"><span data-stu-id="1a884-230">There is no downside toohello use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="1a884-231">Novos tamanhos de disco: gerenciados e não gerenciados</span><span class="sxs-lookup"><span data-stu-id="1a884-231">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="1a884-232">**Qual é Olá maior tamanho de disco com suporte para o sistema operacional e discos de dados?**</span><span class="sxs-lookup"><span data-stu-id="1a884-232">**What is hello largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="1a884-233">tipo de partição de Hello Azure oferece suporte para um disco do sistema operacional é Olá mestre de inicialização MBR (registro).</span><span class="sxs-lookup"><span data-stu-id="1a884-233">hello partition type that Azure supports for an operating system disk is hello master boot record (MBR).</span></span> <span data-ttu-id="1a884-234">formato MBR Olá dá suporte a um tamanho de disco até too2 TB.</span><span class="sxs-lookup"><span data-stu-id="1a884-234">hello MBR format supports a disk size up too2 TB.</span></span> <span data-ttu-id="1a884-235">Olá maior tamanho que o Azure oferece suporte para um disco do sistema operacional é de 2 TB.</span><span class="sxs-lookup"><span data-stu-id="1a884-235">hello largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="1a884-236">O Azure suporta até too4 TB para discos de dados.</span><span class="sxs-lookup"><span data-stu-id="1a884-236">Azure supports up too4 TB for data disks.</span></span> 

<span data-ttu-id="1a884-237">**O que é Olá maior blob tamanho de página com suporte?**</span><span class="sxs-lookup"><span data-stu-id="1a884-237">**What is hello largest page blob size that's supported?**</span></span>

<span data-ttu-id="1a884-238">Olá página blob maior que o Azure suporta é 8 TB (8.191 GB).</span><span class="sxs-lookup"><span data-stu-id="1a884-238">hello largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="1a884-239">Não há suporte para blobs de página maiores que 4 TB (4.095 GB) anexado tooa VM como dados ou discos do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="1a884-239">We don't support page blobs larger than 4 TB (4,095 GB) attached tooa VM as data or operating system disks.</span></span>

<span data-ttu-id="1a884-240">**É necessário toouse uma nova versão de ferramentas do Azure toocreate, anexar, redimensionar e carregar discos maiores que 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="1a884-240">**Do I need toouse a new version of Azure tools toocreate, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="1a884-241">Você não precisa tooupgrade seu toocreate de ferramentas do Azure existente, anexar ou redimensionar discos maiores que 1 TB.</span><span class="sxs-lookup"><span data-stu-id="1a884-241">You don't need tooupgrade your existing Azure tools toocreate, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="1a884-242">tooupload seu VHD arquivo local diretamente tooAzure como um blob de página ou disco não gerenciado, é necessário conjuntos de ferramentas toouse hello mais recentes:</span><span class="sxs-lookup"><span data-stu-id="1a884-242">tooupload your VHD file from on-premises directly tooAzure as a page blob or unmanaged disk, you need toouse hello latest tool sets:</span></span>

|<span data-ttu-id="1a884-243">Ferramentas do Azure</span><span class="sxs-lookup"><span data-stu-id="1a884-243">Azure tools</span></span>      | <span data-ttu-id="1a884-244">Versões com suporte</span><span class="sxs-lookup"><span data-stu-id="1a884-244">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="1a884-245">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a884-245">Azure PowerShell</span></span> | <span data-ttu-id="1a884-246">Número de versão 4.1.0: versão de junho de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="1a884-246">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="1a884-247">CLI do Azure v1</span><span class="sxs-lookup"><span data-stu-id="1a884-247">Azure CLI v1</span></span>     | <span data-ttu-id="1a884-248">Número de versão 0.10.13: versão de maio de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="1a884-248">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="1a884-249">AzCopy</span><span class="sxs-lookup"><span data-stu-id="1a884-249">AzCopy</span></span>           | <span data-ttu-id="1a884-250">Número de versão 6.1.0: versão de junho de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="1a884-250">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="1a884-251">suporte a saudação v2 CLI do Azure e o Azure Storage Explorer estará disponível em breve.</span><span class="sxs-lookup"><span data-stu-id="1a884-251">hello support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="1a884-252">**Os tamanhos de disco P4 e P6 têm suporte para discos não gerenciados ou blobs de página?**</span><span class="sxs-lookup"><span data-stu-id="1a884-252">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="1a884-253">Não.</span><span class="sxs-lookup"><span data-stu-id="1a884-253">No.</span></span> <span data-ttu-id="1a884-254">Os tamanhos de disco P4 (32 GB) e P6 (64 GB) têm suporte somente para discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1a884-254">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="1a884-255">O suporte a discos não gerenciados e blobs de página será lançado em breve.</span><span class="sxs-lookup"><span data-stu-id="1a884-255">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="1a884-256">**Se o meu premium existente gerenciado disco menor do que 64 GB foi criado antes da habilitação do disco pequeno hello (em torno de 15 de junho de 2017), como ele é cobrado?**</span><span class="sxs-lookup"><span data-stu-id="1a884-256">**If my existing premium managed disk less than 64 GB was created before hello small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="1a884-257">Discos premium pequeno existentes com menos de 64 GB continuar preço de acordo toohello P10 toobe cobrado.</span><span class="sxs-lookup"><span data-stu-id="1a884-257">Existing small premium disks less than 64 GB continue toobe billed according toohello P10 pricing tier.</span></span> 

<span data-ttu-id="1a884-258">**Como alternar da camada de disco Olá de discos premium pequeno menor do que 64 GB de tooP4 P10 ou P6?**</span><span class="sxs-lookup"><span data-stu-id="1a884-258">**How can I switch hello disk tier of small premium disks less than 64 GB from P10 tooP4 or P6?**</span></span>

<span data-ttu-id="1a884-259">Você pode tirar um instantâneo dos discos pequenos e, em seguida, crie uma saudação de comutador do disco tooautomatically tooP4 da camada de preços ou P6 com base no tamanho de saudação provisionado.</span><span class="sxs-lookup"><span data-stu-id="1a884-259">You can take a snapshot of your small disks and then create a disk tooautomatically switch hello pricing tier tooP4 or P6 based on hello provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="1a884-260">E se dúvida não foi respondida aqui?</span><span class="sxs-lookup"><span data-stu-id="1a884-260">What if my question isn't answered here?</span></span>

<span data-ttu-id="1a884-261">Se sua pergunta não estiver listada aqui, fale conosco e nós ajudaremos a encontrar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="1a884-261">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="1a884-262">Você pode postar uma pergunta no final deste artigo Olá nos comentários de saudação.</span><span class="sxs-lookup"><span data-stu-id="1a884-262">You can post a question at hello end of this article in hello comments.</span></span> <span data-ttu-id="1a884-263">tooengage com a equipe de armazenamento do Azure hello e outros membros da comunidade sobre neste artigo, use Olá MSDN [Fórum de armazenamento do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span><span class="sxs-lookup"><span data-stu-id="1a884-263">tooengage with hello Azure Storage team and other community members about this article, use hello MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="1a884-264">recursos toorequest, enviar sua solicitações e ideias toohello [Fórum de comentários do armazenamento do Azure](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="1a884-264">toorequest features, submit your requests and ideas toohello [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
