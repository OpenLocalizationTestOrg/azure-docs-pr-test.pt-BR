# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a><span data-ttu-id="e7608-101">Perguntas frequentes sobre discos de VM IaaS do Azure e discos premium gerenciados e não gerenciados</span><span class="sxs-lookup"><span data-stu-id="e7608-101">Frequently asked questions about Azure IaaS VM disks and managed and unmanaged premium disks</span></span>

<span data-ttu-id="e7608-102">Este artigo responde a algumas perguntas frequentes sobre o Azure Managed Disks e o Armazenamento Premium do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7608-102">This article answers some frequently asked questions about Azure Managed Disks and Azure Premium Storage.</span></span>

## <a name="managed-disks"></a><span data-ttu-id="e7608-103">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="e7608-103">Managed Disks</span></span>

<span data-ttu-id="e7608-104">**O que é o Azure Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="e7608-104">**What is Azure Managed Disks?**</span></span>

<span data-ttu-id="e7608-105">Managed Disks é um recurso que simplifica o gerenciamento de disco para VMs IaaS do Azure manipulando o gerenciamento de conta de armazenamento para você.</span><span class="sxs-lookup"><span data-stu-id="e7608-105">Managed Disks is a feature that simplifies disk management for Azure IaaS VMs by handling storage account management for you.</span></span> <span data-ttu-id="e7608-106">Para saber mais, veja [Visão geral dos Managed Disks](../articles/virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e7608-106">For more information, see the [Managed Disks overview](../articles/virtual-machines/windows/managed-disks-overview.md).</span></span>

<span data-ttu-id="e7608-107">**Se eu criar um disco gerenciado standard com base em um VHD existente que tem 80 GB, quanto isso custará?**</span><span class="sxs-lookup"><span data-stu-id="e7608-107">**If I create a standard managed disk from an existing VHD that's 80 GB, how much will that cost me?**</span></span>

<span data-ttu-id="e7608-108">Um disco gerenciado standard criado com base em um VHD de 80 GB é tratado como o próximo tamanho de disco standard disponível, um disco S10.</span><span class="sxs-lookup"><span data-stu-id="e7608-108">A standard managed disk created from an 80-GB VHD is treated as the next available standard disk size, which is an S10 disk.</span></span> <span data-ttu-id="e7608-109">Você será cobrado de acordo com o preço do disco S10.</span><span class="sxs-lookup"><span data-stu-id="e7608-109">You're charged according to the S10 disk pricing.</span></span> <span data-ttu-id="e7608-110">Para saber mais, confira a [página de preço](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="e7608-110">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="e7608-111">**Existem custos de transação de discos gerenciados standard?**</span><span class="sxs-lookup"><span data-stu-id="e7608-111">**Are there any transaction costs for standard managed disks?**</span></span>

<span data-ttu-id="e7608-112">Sim.</span><span class="sxs-lookup"><span data-stu-id="e7608-112">Yes.</span></span> <span data-ttu-id="e7608-113">Você é cobrado por cada transação.</span><span class="sxs-lookup"><span data-stu-id="e7608-113">You're charged for each transaction.</span></span> <span data-ttu-id="e7608-114">Para saber mais, confira a [página de preço](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="e7608-114">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="e7608-115">**Para um disco gerenciado standard, eu serei cobrado pelo tamanho real dos dados no disco ou pela capacidade provisionada do disco?**</span><span class="sxs-lookup"><span data-stu-id="e7608-115">**For a standard managed disk, will I be charged for the actual size of the data on the disk or for the provisioned capacity of the disk?**</span></span>

<span data-ttu-id="e7608-116">Você é cobrado com base na capacidade provisionada do disco.</span><span class="sxs-lookup"><span data-stu-id="e7608-116">You're charged based on the provisioned capacity of the disk.</span></span> <span data-ttu-id="e7608-117">Para saber mais, confira a [página de preço](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="e7608-117">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="e7608-118">**O preço dos discos premium gerenciados é diferente do preço dos discos não gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="e7608-118">**How is pricing of premium managed disks different from unmanaged disks?**</span></span>

<span data-ttu-id="e7608-119">O preço dos discos premium gerenciados é o mesmo que os discos premium não gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e7608-119">The pricing of premium managed disks is the same as unmanaged premium disks.</span></span>

<span data-ttu-id="e7608-120">**Posso alterar o tipo de conta de armazenamento (Standard ou Premium) de meus discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="e7608-120">**Can I change the storage account type (Standard or Premium) of my managed disks?**</span></span>

<span data-ttu-id="e7608-121">Sim.</span><span class="sxs-lookup"><span data-stu-id="e7608-121">Yes.</span></span> <span data-ttu-id="e7608-122">Você pode alterar o tipo de conta de armazenamento de seus discos gerenciados usando o portal do Azure, PowerShell ou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7608-122">You can change the storage account type of your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="e7608-123">**É possível copiar ou exportar um disco gerenciado para uma conta de armazenamento privado?**</span><span class="sxs-lookup"><span data-stu-id="e7608-123">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="e7608-124">Sim.</span><span class="sxs-lookup"><span data-stu-id="e7608-124">Yes.</span></span> <span data-ttu-id="e7608-125">Você pode exportar seus discos gerenciados usando o portal do Azure, PowerShell ou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7608-125">You can export your managed disks by using the Azure portal, PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="e7608-126">**Posso usar um arquivo VHD em uma conta de armazenamento do Azure para criar um disco gerenciado com uma assinatura diferente?**</span><span class="sxs-lookup"><span data-stu-id="e7608-126">**Can I use a VHD file in an Azure storage account to create a managed disk with a different subscription?**</span></span>

<span data-ttu-id="e7608-127">Não.</span><span class="sxs-lookup"><span data-stu-id="e7608-127">No.</span></span>

<span data-ttu-id="e7608-128">**Posso usar um arquivo VHD em uma conta de armazenamento do Azure para criar um disco gerenciado em uma região diferente?**</span><span class="sxs-lookup"><span data-stu-id="e7608-128">**Can I use a VHD file in an Azure storage account to create a managed disk in a different region?**</span></span>

<span data-ttu-id="e7608-129">Não.</span><span class="sxs-lookup"><span data-stu-id="e7608-129">No.</span></span>

<span data-ttu-id="e7608-130">**Existem limitações de escala para clientes que usam discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="e7608-130">**Are there any scale limitations for customers that use managed disks?**</span></span>

<span data-ttu-id="e7608-131">O Managed Disks elimina os limites associados a contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e7608-131">Managed Disks eliminates the limits associated with storage accounts.</span></span> <span data-ttu-id="e7608-132">No entanto, o número de discos gerenciados por assinatura é limitado a 2.000 por padrão.</span><span class="sxs-lookup"><span data-stu-id="e7608-132">However, the number of managed disks per subscription is limited to 2,000 by default.</span></span> <span data-ttu-id="e7608-133">Você pode chamar o suporte para aumentar esse número.</span><span class="sxs-lookup"><span data-stu-id="e7608-133">You can call support to increase this number.</span></span>

<span data-ttu-id="e7608-134">**Posso fazer um instantâneo incremental de um disco gerenciado?**</span><span class="sxs-lookup"><span data-stu-id="e7608-134">**Can I take an incremental snapshot of a managed disk?**</span></span>

<span data-ttu-id="e7608-135">Não.</span><span class="sxs-lookup"><span data-stu-id="e7608-135">No.</span></span> <span data-ttu-id="e7608-136">O recurso de instantâneo atual faz uma cópia completa de um disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="e7608-136">The current snapshot capability makes a full copy of a managed disk.</span></span> <span data-ttu-id="e7608-137">No entanto, estamos planejando oferecer suporte a instantâneos incrementais no futuro.</span><span class="sxs-lookup"><span data-stu-id="e7608-137">However, we are planning to support incremental snapshots in the future.</span></span>

<span data-ttu-id="e7608-138">**As VMs em um conjunto de disponibilidade podem consistir de uma combinação de discos gerenciados e não gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="e7608-138">**Can VMs in an availability set consist of a combination of managed and unmanaged disks?**</span></span>

<span data-ttu-id="e7608-139">Não.</span><span class="sxs-lookup"><span data-stu-id="e7608-139">No.</span></span> <span data-ttu-id="e7608-140">As VMs em um conjunto de disponibilidade devem usar todos os discos gerenciados ou não gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e7608-140">The VMs in an availability set must use either all managed disks or all unmanaged disks.</span></span> <span data-ttu-id="e7608-141">Ao criar um conjunto de disponibilidade, você pode escolher qual tipo de discos que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="e7608-141">When you create an availability set, you can choose which type of disks you want to use.</span></span>

<span data-ttu-id="e7608-142">**O Managed Disks é a opção padrão no portal do Azure?**</span><span class="sxs-lookup"><span data-stu-id="e7608-142">**Is Managed Disks the default option in the Azure portal?**</span></span>

<span data-ttu-id="e7608-143">Atualmente não, mas ele se tornará o padrão no futuro.</span><span class="sxs-lookup"><span data-stu-id="e7608-143">Not currently, but it will become the default in the future.</span></span>

<span data-ttu-id="e7608-144">**É possível criar um disco gerenciado vazio?**</span><span class="sxs-lookup"><span data-stu-id="e7608-144">**Can I create an empty managed disk?**</span></span>

<span data-ttu-id="e7608-145">Sim.</span><span class="sxs-lookup"><span data-stu-id="e7608-145">Yes.</span></span> <span data-ttu-id="e7608-146">Você pode criar um disco vazio.</span><span class="sxs-lookup"><span data-stu-id="e7608-146">You can create an empty disk.</span></span> <span data-ttu-id="e7608-147">Um disco gerenciado pode ser criado independentemente de uma VM, por exemplo, sem anexá-lo a uma VM.</span><span class="sxs-lookup"><span data-stu-id="e7608-147">A managed disk can be created independently of a VM, for example, without attaching it to a VM.</span></span>

<span data-ttu-id="e7608-148">**O que é a contagem de domínios de falha com suporte para um conjunto de disponibilidade que usa o Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="e7608-148">**What is the supported fault domain count for an availability set that uses Managed Disks?**</span></span>

<span data-ttu-id="e7608-149">Dependendo da região em que o conjunto de disponibilidade que usa o Managed Disks está localizado, a contagem de domínios de falha com suporte é 2 ou 3.</span><span class="sxs-lookup"><span data-stu-id="e7608-149">Depending on the region where the availability set that uses Managed Disks is located, the supported fault domain count is 2 or 3.</span></span>

<span data-ttu-id="e7608-150">**Como é conta de armazenamento standard para a configuração de diagnóstico?**</span><span class="sxs-lookup"><span data-stu-id="e7608-150">**How is the standard storage account for diagnostics set up?**</span></span>

<span data-ttu-id="e7608-151">Você configura uma conta de armazenamento privado para diagnóstico da VM.</span><span class="sxs-lookup"><span data-stu-id="e7608-151">You set up a private storage account for VM diagnostics.</span></span> <span data-ttu-id="e7608-152">No futuro, planejamos alternar o diagnóstico para o Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="e7608-152">In the future, we plan to switch diagnostics to Managed Disks as well.</span></span>

<span data-ttu-id="e7608-153">**O tipo de suporte ao Controle de Acesso Baseado em Função está disponível para o Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="e7608-153">**What kind of Role-Based Access Control support is available for Managed Disks?**</span></span>

<span data-ttu-id="e7608-154">O Managed Disks oferece suporte a três funções principais padrão:</span><span class="sxs-lookup"><span data-stu-id="e7608-154">Managed Disks supports three key default roles:</span></span>

* <span data-ttu-id="e7608-155">Proprietário: pode gerenciar tudo, incluindo o acesso</span><span class="sxs-lookup"><span data-stu-id="e7608-155">Owner: Can manage everything, including access</span></span>
* <span data-ttu-id="e7608-156">Colaborador: pode gerenciar tudo, exceto o acesso</span><span class="sxs-lookup"><span data-stu-id="e7608-156">Contributor: Can manage everything except access</span></span>
* <span data-ttu-id="e7608-157">Leitor: pode ver tudo, mas não pode fazer alterações</span><span class="sxs-lookup"><span data-stu-id="e7608-157">Reader: Can view everything, but can't make changes</span></span>

<span data-ttu-id="e7608-158">**É possível copiar ou exportar um disco gerenciado para uma conta de armazenamento privado?**</span><span class="sxs-lookup"><span data-stu-id="e7608-158">**Is there a way that I can copy or export a managed disk to a private storage account?**</span></span>

<span data-ttu-id="e7608-159">Você pode obter um URI de assinatura de acesso compartilhado somente leitura para o disco gerenciado e usá-la para copiar o conteúdo para uma conta de armazenamento privado ou armazenamento local.</span><span class="sxs-lookup"><span data-stu-id="e7608-159">You can get a read-only shared access signature URI for the managed disk and use it to copy the contents to a private storage account or on-premises storage.</span></span>

<span data-ttu-id="e7608-160">**Posso criar uma cópia do meu disco gerenciado?**</span><span class="sxs-lookup"><span data-stu-id="e7608-160">**Can I create a copy of my managed disk?**</span></span>

<span data-ttu-id="e7608-161">Os clientes podem tirar um instantâneo de seus discos gerenciados e, em seguida, usar o instantâneo para criar outro disco gerenciado.</span><span class="sxs-lookup"><span data-stu-id="e7608-161">Customers can take a snapshot of their managed disks and then use the snapshot to create another managed disk.</span></span>

<span data-ttu-id="e7608-162">**Ainda há suporte para discos não gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="e7608-162">**Are unmanaged disks still supported?**</span></span>

<span data-ttu-id="e7608-163">Sim.</span><span class="sxs-lookup"><span data-stu-id="e7608-163">Yes.</span></span> <span data-ttu-id="e7608-164">Há suporte para discos gerenciados e não gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e7608-164">We support unmanaged and managed disks.</span></span> <span data-ttu-id="e7608-165">Recomendamos que você use discos gerenciados para novas cargas de trabalho e migre suas cargas de trabalho atuais para discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e7608-165">We recommend that you use managed disks for new workloads and migrate your current workloads to managed disks.</span></span>


<span data-ttu-id="e7608-166">**Se eu criar um disco de 128 GB e aumentar o tamanho para 130 GB, serei cobrado pelo próximo tamanho de disco (512 GB)?**</span><span class="sxs-lookup"><span data-stu-id="e7608-166">**If I create a 128-GB disk and then increase the size to 130 GB, will I be charged for the next disk size (512 GB)?**</span></span>

<span data-ttu-id="e7608-167">Sim.</span><span class="sxs-lookup"><span data-stu-id="e7608-167">Yes.</span></span>

<span data-ttu-id="e7608-168">**Posso criar armazenamento com redundância local, armazenamento com redundância geográfica e discos de armazenamento com redundância de zona gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="e7608-168">**Can I create locally redundant storage, geo-redundant storage, and zone-redundant storage managed disks?**</span></span>

<span data-ttu-id="e7608-169">O Azure Managed Disks atualmente dá suporte apenas a discos gerenciados de armazenamento com redundância local.</span><span class="sxs-lookup"><span data-stu-id="e7608-169">Azure Managed Disks currently supports only locally redundant storage managed disks.</span></span>

<span data-ttu-id="e7608-170">**Posso reduzir ou diminuir o tamanho de meus discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="e7608-170">**Can I shrink or downsize my managed disks?**</span></span>

<span data-ttu-id="e7608-171">Não.</span><span class="sxs-lookup"><span data-stu-id="e7608-171">No.</span></span> <span data-ttu-id="e7608-172">Não há suporte para esse recurso no momento.</span><span class="sxs-lookup"><span data-stu-id="e7608-172">This feature is not supported currently.</span></span> 

<span data-ttu-id="e7608-173">**Posso alterar a propriedade de nome do computador quando um disco do sistema operacional especializado (não criado usando a ferramenta de Preparação do Sistema ou generalizado) é usado para provisionar uma máquina virtual?**</span><span class="sxs-lookup"><span data-stu-id="e7608-173">**Can I change the computer name property when a specialized (not created by using the System Preparation tool or generalized) operating system disk is used to provision a VM?**</span></span>

<span data-ttu-id="e7608-174">Não.</span><span class="sxs-lookup"><span data-stu-id="e7608-174">No.</span></span> <span data-ttu-id="e7608-175">Não é possível atualizar a propriedade de nome do computador.</span><span class="sxs-lookup"><span data-stu-id="e7608-175">You can't update the computer name property.</span></span> <span data-ttu-id="e7608-176">A nova VM a herda do pai, que foi usado para criar o disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="e7608-176">The new VM inherits it from the parent VM, which was used to create the operating system disk.</span></span> 

<span data-ttu-id="e7608-177">**Onde posso encontrar modelos do Azure Resource Manager de exemplo para criar VMs com discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="e7608-177">**Where can I find sample Azure Resource Manager templates to create VMs with managed disks?**</span></span>
* [<span data-ttu-id="e7608-178">Lista de modelos que usam o Managed Disks</span><span class="sxs-lookup"><span data-stu-id="e7608-178">List of templates using Managed Disks</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* <span data-ttu-id="e7608-179">https://github.com/chagarw/MDPP</span><span class="sxs-lookup"><span data-stu-id="e7608-179">https://github.com/chagarw/MDPP</span></span>

## <a name="managed-disks-and-storage-service-encryption"></a><span data-ttu-id="e7608-180">Managed Disks e Criptografia de Serviço de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="e7608-180">Managed Disks and Storage Service Encryption</span></span> 

<span data-ttu-id="e7608-181">**A Criptografia do Serviço de Armazenamento do Azure fica habilitada por padrão quando crio um disco gerenciado?**</span><span class="sxs-lookup"><span data-stu-id="e7608-181">**Is Azure Storage Service Encryption enabled by default when I create a managed disk?**</span></span>

<span data-ttu-id="e7608-182">Sim.</span><span class="sxs-lookup"><span data-stu-id="e7608-182">Yes.</span></span>

<span data-ttu-id="e7608-183">**Quem gerencia as chaves de criptografia?**</span><span class="sxs-lookup"><span data-stu-id="e7608-183">**Who manages the encryption keys?**</span></span>

<span data-ttu-id="e7608-184">A Microsoft gerencia as chaves de criptografia.</span><span class="sxs-lookup"><span data-stu-id="e7608-184">Microsoft manages the encryption keys.</span></span>

<span data-ttu-id="e7608-185">**Posso desabilitar a Criptografia do Serviço de Armazenamento para meus discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="e7608-185">**Can I disable Storage Service Encryption for my managed disks?**</span></span>

<span data-ttu-id="e7608-186">Não.</span><span class="sxs-lookup"><span data-stu-id="e7608-186">No.</span></span>

<span data-ttu-id="e7608-187">**A Criptografia do Serviço de Armazenamento só está disponível em regiões específicas?**</span><span class="sxs-lookup"><span data-stu-id="e7608-187">**Is Storage Service Encryption only available in specific regions?**</span></span>

<span data-ttu-id="e7608-188">Não.</span><span class="sxs-lookup"><span data-stu-id="e7608-188">No.</span></span> <span data-ttu-id="e7608-189">Ele está disponível em todas as regiões em que os discos gerenciados estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e7608-189">It's available in all the regions where Managed Disks is available.</span></span> <span data-ttu-id="e7608-190">O Managed Disks está disponível em todas as regiões públicas e na Alemanha.</span><span class="sxs-lookup"><span data-stu-id="e7608-190">Managed Disks is available in all public regions and Germany.</span></span>

<span data-ttu-id="e7608-191">**Como posso descobrir se o disco gerenciado está criptografado?**</span><span class="sxs-lookup"><span data-stu-id="e7608-191">**How can I find out if my managed disk is encrypted?**</span></span>

<span data-ttu-id="e7608-192">Você pode descobrir a data em que um disco gerenciado foi criado no portal do Azure, na CLI do Azure e no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7608-192">You can find out the time when a managed disk was created from the Azure portal, the Azure CLI, and PowerShell.</span></span> <span data-ttu-id="e7608-193">Se a data é posterior a 9 de junho de 2017, o disco está criptografado.</span><span class="sxs-lookup"><span data-stu-id="e7608-193">If the time is after June 9, 2017, then your disk is encrypted.</span></span> 

<span data-ttu-id="e7608-194">**Como faço para criptografar meus discos existentes que foram criados antes de 10 de junho de 2017?**</span><span class="sxs-lookup"><span data-stu-id="e7608-194">**How can I encrypt my existing disks that were created before June 10, 2017?**</span></span>

<span data-ttu-id="e7608-195">A partir de 10 de junho de 2017, os novos dados gravados em discos gerenciados existentes serão criptografados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e7608-195">As of June 10, 2017, new data written to existing managed disks is automatically encrypted.</span></span> <span data-ttu-id="e7608-196">Nós também estamos planejando criptografar os dados existentes e a criptografia ocorrerá assincronamente em segundo plano.</span><span class="sxs-lookup"><span data-stu-id="e7608-196">We are also planning to encrypt existing data, and the encryption will happen asynchronously in the background.</span></span> <span data-ttu-id="e7608-197">Se você precisar criptografar os dados existentes agora, crie uma cópia do disco.</span><span class="sxs-lookup"><span data-stu-id="e7608-197">If you must encrypt existing data now, create a copy of your disk.</span></span> <span data-ttu-id="e7608-198">Os novos discos serão criptografados.</span><span class="sxs-lookup"><span data-stu-id="e7608-198">New disks will be encrypted.</span></span>

* [<span data-ttu-id="e7608-199">Copiar discos gerenciados usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e7608-199">Copy managed disks by using the Azure CLI</span></span>](../articles/virtual-machines/scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)
* [<span data-ttu-id="e7608-200">Copiar discos gerenciados usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7608-200">Copy managed disks by using PowerShell</span></span>](../articles/virtual-machines/scripts/virtual-machines-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="e7608-201">**Os instantâneos gerenciados e as imagens são criptografados?**</span><span class="sxs-lookup"><span data-stu-id="e7608-201">**Are managed snapshots and images encrypted?**</span></span>

<span data-ttu-id="e7608-202">Sim.</span><span class="sxs-lookup"><span data-stu-id="e7608-202">Yes.</span></span> <span data-ttu-id="e7608-203">Todos os instantâneos e imagens criados após 9 de junho de 2017 são criptografados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e7608-203">All managed snapshots and images created after June 9, 2017, are automatically encrypted.</span></span> 

<span data-ttu-id="e7608-204">**Posso converter máquinas virtuais com discos não gerenciados que estão localizados em contas de armazenamento ou criptografados anteriormente em discos gerenciados?**</span><span class="sxs-lookup"><span data-stu-id="e7608-204">**Can I convert VMs with unmanaged disks that are located on storage accounts that are or were previously encrypted to managed disks?**</span></span>

<span data-ttu-id="e7608-205">Sim</span><span class="sxs-lookup"><span data-stu-id="e7608-205">Yes</span></span>

<span data-ttu-id="e7608-206">**Um VHD exportado de um disco gerenciado ou instantâneo também será criptografado?**</span><span class="sxs-lookup"><span data-stu-id="e7608-206">**Will an exported VHD from a managed disk or a snapshot also be encrypted?**</span></span>

<span data-ttu-id="e7608-207">Não.</span><span class="sxs-lookup"><span data-stu-id="e7608-207">No.</span></span> <span data-ttu-id="e7608-208">Mas se você exportar um VHD para uma conta de armazenamento criptografada de um disco gerenciado ou instantâneo criptografado, ele estará criptografado.</span><span class="sxs-lookup"><span data-stu-id="e7608-208">But if you export a VHD to an encrypted storage account from an encrypted managed disk or snapshot, then it's encrypted.</span></span> 

## <a name="premium-disks-managed-and-unmanaged"></a><span data-ttu-id="e7608-209">Discos Premium: gerenciados e não gerenciados</span><span class="sxs-lookup"><span data-stu-id="e7608-209">Premium disks: Managed and unmanaged</span></span>

<span data-ttu-id="e7608-210">**Se uma VM usa uma série de tamanho que dá suporte ao Armazenamento Premium, como um DSv2, é possível anexar discos de dados standard e premium?**</span><span class="sxs-lookup"><span data-stu-id="e7608-210">**If a VM uses a size series that supports Premium Storage, such as a DSv2, can I attach both premium and standard data disks?**</span></span> 

<span data-ttu-id="e7608-211">Sim.</span><span class="sxs-lookup"><span data-stu-id="e7608-211">Yes.</span></span>

<span data-ttu-id="e7608-212">**É possível anexar discos de dados standard e premium a uma série de tamanho que não oferece suporte a armazenamento Premium, como as séries D, Dv2, G ou F?**</span><span class="sxs-lookup"><span data-stu-id="e7608-212">**Can I attach both premium and standard data disks to a size series that doesn't support Premium Storage, such as D, Dv2, G, or F series?**</span></span>

<span data-ttu-id="e7608-213">Não.</span><span class="sxs-lookup"><span data-stu-id="e7608-213">No.</span></span> <span data-ttu-id="e7608-214">Você só pode anexar discos de dados standard às VMs que não usam uma série de tamanho que dá suporte ao Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="e7608-214">You can attach only standard data disks to VMs that don't use a size series that supports Premium Storage.</span></span>

<span data-ttu-id="e7608-215">**Se criar um disco de dados premium com base em um VHD existente que tinha 80 GB, quanto isso custará?**</span><span class="sxs-lookup"><span data-stu-id="e7608-215">**If I create a premium data disk from an existing VHD that was 80 GB, how much will that cost?**</span></span>

<span data-ttu-id="e7608-216">Um disco de dados premium criado com base em um VHD de 80 GB é tratado como o próximo tamanho de disco premium disponível, um disco P10.</span><span class="sxs-lookup"><span data-stu-id="e7608-216">A premium data disk created from an 80-GB VHD is treated as the next-available premium disk size, which is a P10 disk.</span></span> <span data-ttu-id="e7608-217">Você será cobrado de acordo com o preço do disco P10.</span><span class="sxs-lookup"><span data-stu-id="e7608-217">You're charged according to the P10 disk pricing.</span></span>

<span data-ttu-id="e7608-218">**Existem custos de transação para usar o Armazenamento Premium?**</span><span class="sxs-lookup"><span data-stu-id="e7608-218">**Are there transaction costs to use Premium Storage?**</span></span>

<span data-ttu-id="e7608-219">Há um custo fixo para cada tamanho de disco, que vem provisionado com limites específicos de IOPS e taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="e7608-219">There is a fixed cost for each disk size, which comes provisioned with specific limits on IOPS and throughput.</span></span> <span data-ttu-id="e7608-220">Os outros custos são largura de banda de saída e recurso de instantâneos, caso aplicável.</span><span class="sxs-lookup"><span data-stu-id="e7608-220">The other costs are outbound bandwidth and snapshot capacity, if applicable.</span></span> <span data-ttu-id="e7608-221">Para saber mais, confira a [página de preço](https://azure.microsoft.com/pricing/details/storage).</span><span class="sxs-lookup"><span data-stu-id="e7608-221">For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/storage).</span></span>

<span data-ttu-id="e7608-222">**Quais são os limites de IOPS e taxa de transferência que posso obter do cache de disco?**</span><span class="sxs-lookup"><span data-stu-id="e7608-222">**What are the limits for IOPS and throughput that I can get from the disk cache?**</span></span>

<span data-ttu-id="e7608-223">Os limites combinados para cache e SSD local para um item da série DS são 4.000 IOPS por núcleo e 33 MB por segundo por núcleo.</span><span class="sxs-lookup"><span data-stu-id="e7608-223">The combined limits for cache and local SSD for a DS series are 4,000 IOPS per core and 33 MB per second per core.</span></span> <span data-ttu-id="e7608-224">A série GS oferece 5.000 IOPS por núcleo e 50 MB por segundo por núcleo.</span><span class="sxs-lookup"><span data-stu-id="e7608-224">The GS series offers 5,000 IOPS per core and 50 MB per second per core.</span></span>

<span data-ttu-id="e7608-225">**O SSD local tem suporte para uma VM do Managed Disks?**</span><span class="sxs-lookup"><span data-stu-id="e7608-225">**Is the local SSD supported for a Managed Disks VM?**</span></span>

<span data-ttu-id="e7608-226">O SSD local é um armazenamento temporário fornecido com uma VM do Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="e7608-226">The local SSD is temporary storage that is included with a Managed Disks VM.</span></span> <span data-ttu-id="e7608-227">Não há custo adicional para esse armazenamento temporário.</span><span class="sxs-lookup"><span data-stu-id="e7608-227">There is no extra cost for this temporary storage.</span></span> <span data-ttu-id="e7608-228">Recomendamos que você não use esse SSD local para armazenar os dados do aplicativo porque ele não é mantido no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7608-228">We recommend that you do not use this local SSD to store your application data because it isn't persisted in Azure Blob storage.</span></span>

<span data-ttu-id="e7608-229">**Existem repercussões pelo uso de TRIM em discos premium?**</span><span class="sxs-lookup"><span data-stu-id="e7608-229">**Are there any repercussions for the use of TRIM on premium disks?**</span></span>

<span data-ttu-id="e7608-230">Não há nenhuma desvantagem em usar CORTE nos Discos do Azure Premium ou Standard.</span><span class="sxs-lookup"><span data-stu-id="e7608-230">There is no downside to the use of TRIM on Azure disks on either premium or standard disks.</span></span>

## <a name="new-disk-sizes-managed-and-unmanaged"></a><span data-ttu-id="e7608-231">Novos tamanhos de disco: gerenciados e não gerenciados</span><span class="sxs-lookup"><span data-stu-id="e7608-231">New disk sizes: Managed and unmanaged</span></span>

<span data-ttu-id="e7608-232">**Qual é o maior tamanho de disco com suporte para o sistema operacional e os discos de dados?**</span><span class="sxs-lookup"><span data-stu-id="e7608-232">**What is the largest disk size supported for operating system and data disks?**</span></span>

<span data-ttu-id="e7608-233">O tipo de partição a que o Azure dá suporte para um disco do sistema operacional é o MBR (registro mestre de inicialização).</span><span class="sxs-lookup"><span data-stu-id="e7608-233">The partition type that Azure supports for an operating system disk is the master boot record (MBR).</span></span> <span data-ttu-id="e7608-234">O formato do MBR dá suporte a tamanho de disco de até 2 TB.</span><span class="sxs-lookup"><span data-stu-id="e7608-234">The MBR format supports a disk size up to 2 TB.</span></span> <span data-ttu-id="e7608-235">O maior tamanho a que o Azure dá suporte para um disco do sistema operacional é 2 TB.</span><span class="sxs-lookup"><span data-stu-id="e7608-235">The largest size that Azure supports for an operating system disk is 2 TB.</span></span> <span data-ttu-id="e7608-236">O Azure dá suporte a até 4 TB em discos de dados.</span><span class="sxs-lookup"><span data-stu-id="e7608-236">Azure supports up to 4 TB for data disks.</span></span> 

<span data-ttu-id="e7608-237">**Qual é o maior tamanho de blob de página com suporte?**</span><span class="sxs-lookup"><span data-stu-id="e7608-237">**What is the largest page blob size that's supported?**</span></span>

<span data-ttu-id="e7608-238">O maior tamanho de blob de página a que o Azure dá suporte é 8 TB (8.191 GB).</span><span class="sxs-lookup"><span data-stu-id="e7608-238">The largest page blob size that Azure supports is 8 TB (8,191 GB).</span></span> <span data-ttu-id="e7608-239">Não há suporte para blobs de página maiores que 4 TB (4.095 GB) anexados a uma VM como dados ou discos do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="e7608-239">We don't support page blobs larger than 4 TB (4,095 GB) attached to a VM as data or operating system disks.</span></span>

<span data-ttu-id="e7608-240">**Preciso usar uma nova versão das ferramentas do Azure para criar, anexar, redimensionar e carregar discos maiores que 1 TB?**</span><span class="sxs-lookup"><span data-stu-id="e7608-240">**Do I need to use a new version of Azure tools to create, attach, resize, and upload disks larger than 1 TB?**</span></span>

<span data-ttu-id="e7608-241">Você não precisa atualizar as ferramentas existentes do Azure para criar, anexar ou redimensionar discos maiores que 1 TB.</span><span class="sxs-lookup"><span data-stu-id="e7608-241">You don't need to upgrade your existing Azure tools to create, attach, or resize disks larger than 1 TB.</span></span> <span data-ttu-id="e7608-242">Para carregar o arquivo VHD local diretamente no Azure como um blob de página ou disco não gerenciado, você precisará usar os conjuntos de ferramentas mais recentes:</span><span class="sxs-lookup"><span data-stu-id="e7608-242">To upload your VHD file from on-premises directly to Azure as a page blob or unmanaged disk, you need to use the latest tool sets:</span></span>

|<span data-ttu-id="e7608-243">Ferramentas do Azure</span><span class="sxs-lookup"><span data-stu-id="e7608-243">Azure tools</span></span>      | <span data-ttu-id="e7608-244">Versões com suporte</span><span class="sxs-lookup"><span data-stu-id="e7608-244">Supported versions</span></span>                                |
|-----------------|---------------------------------------------------|
|<span data-ttu-id="e7608-245">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7608-245">Azure PowerShell</span></span> | <span data-ttu-id="e7608-246">Número de versão 4.1.0: versão de junho de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="e7608-246">Version number 4.1.0: June 2017 release or later</span></span>|
|<span data-ttu-id="e7608-247">CLI do Azure v1</span><span class="sxs-lookup"><span data-stu-id="e7608-247">Azure CLI v1</span></span>     | <span data-ttu-id="e7608-248">Número de versão 0.10.13: versão de maio de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="e7608-248">Version number 0.10.13: May 2017 release or later</span></span>|
|<span data-ttu-id="e7608-249">AzCopy</span><span class="sxs-lookup"><span data-stu-id="e7608-249">AzCopy</span></span>           | <span data-ttu-id="e7608-250">Número de versão 6.1.0: versão de junho de 2017 ou posterior</span><span class="sxs-lookup"><span data-stu-id="e7608-250">Version number 6.1.0: June 2017 release or later</span></span>|

<span data-ttu-id="e7608-251">O suporte à CLI do Azure v2 e ao Gerenciador de Armazenamento do Azure estará disponível em breve.</span><span class="sxs-lookup"><span data-stu-id="e7608-251">The support for Azure CLI v2 and Azure Storage Explorer is coming soon.</span></span> 

<span data-ttu-id="e7608-252">**Os tamanhos de disco P4 e P6 têm suporte para discos não gerenciados ou blobs de página?**</span><span class="sxs-lookup"><span data-stu-id="e7608-252">**Are P4 and P6 disk sizes supported for unmanaged disks or page blobs?**</span></span>

<span data-ttu-id="e7608-253">Não.</span><span class="sxs-lookup"><span data-stu-id="e7608-253">No.</span></span> <span data-ttu-id="e7608-254">Os tamanhos de disco P4 (32 GB) e P6 (64 GB) têm suporte somente para discos gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e7608-254">P4 (32 GB) and P6 (64 GB) disk sizes are supported only for managed disks.</span></span> <span data-ttu-id="e7608-255">O suporte a discos não gerenciados e blobs de página será lançado em breve.</span><span class="sxs-lookup"><span data-stu-id="e7608-255">Support for unmanaged disks and page blobs is coming soon.</span></span>

<span data-ttu-id="e7608-256">**Se o meu disco gerenciado premium existente com menos de 64 GB foi criado antes da habilitação da pequeno disco (por volta de 15 de junho de 2017), como ele é cobrado?**</span><span class="sxs-lookup"><span data-stu-id="e7608-256">**If my existing premium managed disk less than 64 GB was created before the small disk was enabled (around June 15, 2017), how is it billed?**</span></span>

<span data-ttu-id="e7608-257">Os discos pequenos premium com menos de 64 GB continuam a ser cobrados de acordo com o tipo de preços P10.</span><span class="sxs-lookup"><span data-stu-id="e7608-257">Existing small premium disks less than 64 GB continue to be billed according to the P10 pricing tier.</span></span> 

<span data-ttu-id="e7608-258">**Como alternar a camada de disco dos discos premium pequenos com menos de 64 GB de P10 para P4 ou P6?**</span><span class="sxs-lookup"><span data-stu-id="e7608-258">**How can I switch the disk tier of small premium disks less than 64 GB from P10 to P4 or P6?**</span></span>

<span data-ttu-id="e7608-259">Você pode tirar um instantâneo dos discos pequenos e criar um disco para alternar automaticamente o tipo de preço para P4 ou P6 com base no tamanho provisionado.</span><span class="sxs-lookup"><span data-stu-id="e7608-259">You can take a snapshot of your small disks and then create a disk to automatically switch the pricing tier to P4 or P6 based on the provisioned size.</span></span> 


## <a name="what-if-my-question-isnt-answered-here"></a><span data-ttu-id="e7608-260">E se dúvida não foi respondida aqui?</span><span class="sxs-lookup"><span data-stu-id="e7608-260">What if my question isn't answered here?</span></span>

<span data-ttu-id="e7608-261">Se sua pergunta não estiver listada aqui, fale conosco e nós ajudaremos a encontrar uma resposta.</span><span class="sxs-lookup"><span data-stu-id="e7608-261">If your question isn't listed here, let us know and we'll help you find an answer.</span></span> <span data-ttu-id="e7608-262">Você pode postar uma pergunta no final deste artigo nos comentários.</span><span class="sxs-lookup"><span data-stu-id="e7608-262">You can post a question at the end of this article in the comments.</span></span> <span data-ttu-id="e7608-263">Para se comunicar com a equipe do Armazenamento do Azure e outros membros da comunidade sobre este artigo, use o [Fórum do Armazenamento do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata) no MSDN.</span><span class="sxs-lookup"><span data-stu-id="e7608-263">To engage with the Azure Storage team and other community members about this article, use the MSDN [Azure Storage forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).</span></span>

<span data-ttu-id="e7608-264">Para solicitar recursos, envie suas solicitações e ideias para o [Fórum de comentários do Armazenamento do Azure](https://feedback.azure.com/forums/217298-storage).</span><span class="sxs-lookup"><span data-stu-id="e7608-264">To request features, submit your requests and ideas to the [Azure Storage feedback forum](https://feedback.azure.com/forums/217298-storage).</span></span>
