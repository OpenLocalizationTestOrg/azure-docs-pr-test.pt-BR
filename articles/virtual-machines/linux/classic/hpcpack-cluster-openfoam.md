---
title: aaaRun OpenFOAM com HPC Pack em VMs do Linux | Microsoft Docs
description: "Implante um cluster do Microsoft HPC Pack no Azure e execute um trabalho OpenFOAM em vários nós de computação do Linux em uma rede RDMA."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="e7780-103">Executar o OpenFoam com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="e7780-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="e7780-104">Este artigo mostra uma maneira toorun OpenFoam em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7780-104">This article shows you one way toorun OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="e7780-105">Aqui, você implanta um cluster do Microsoft HPC Pack com nós de computação do Linux no Azure e executa um trabalho [OpenFoam](http://openfoam.com/) com Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="e7780-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="e7780-106">Você pode usar VMs do Azure compatíveis com RDMA para nós de computação hello, para que nós de computação Olá se comunicar pela rede de RDMA do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-106">You can use RDMA-capable Azure VMs for hello compute nodes, so that hello compute nodes communicate over hello Azure RDMA network.</span></span> <span data-ttu-id="e7780-107">Outros toorun opções OpenFoam no Azure incluem totalmente configurado comerciais imagens disponíveis na Olá Marketplace, como do UberCloud [OpenFoam 2.3 em CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/)e executando em [do Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span><span class="sxs-lookup"><span data-stu-id="e7780-107">Other options toorun OpenFoam in Azure include fully configured commercial images available in hello Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="e7780-108">OpenFOAM (Operação e Manipulação de Campo Aberto) é um pacote de software com CFD (dinâmica de fluido computacional) aberto, amplamente utilizado na Engenharia e nas Ciências em organizações comerciais e acadêmicas.</span><span class="sxs-lookup"><span data-stu-id="e7780-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="e7780-109">Ele inclui ferramentas para criar malhas, especialmente o snappyHexMesh, um mesher em paralelo para geometrias CAD complexas e de pré e pós-processamento.</span><span class="sxs-lookup"><span data-stu-id="e7780-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="e7780-110">Quase todos os processos executados em paralelo, permitindo que os usuários tootake proveito do hardware do computador à sua disposição.</span><span class="sxs-lookup"><span data-stu-id="e7780-110">Almost all processes run in parallel, enabling users tootake full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="e7780-111">Microsoft HPC Pack fornece recursos toorun HPC em larga escala e aplicativos em paralelo, incluindo aplicativos MPI, em clusters de máquinas virtuais do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="e7780-111">Microsoft HPC Pack provides features toorun large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="e7780-112">O HPC Pack também dá suporte a aplicativos de HPC no Linux em VMs com nós de computação do Linux implantadas em um cluster do HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="e7780-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="e7780-113">Consulte [começar conosco de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md) para uma introdução toousing nós com o HPC Pack de computação do Linux.</span><span class="sxs-lookup"><span data-stu-id="e7780-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction toousing Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="e7780-114">Este artigo ilustra como toorun uma carga de trabalho do Linux MPI com HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="e7780-114">This article illustrates how toorun a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="e7780-115">Ele pressupõe que você tem alguma familiaridade com a administração do sistema Linux e com a execução das cargas de trabalho MPI nos clusters do Linux.</span><span class="sxs-lookup"><span data-stu-id="e7780-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="e7780-116">Se você usar versões de MPI e OpenFOAM diferente da saudação aqueles mostrados neste artigo, você pode ter toomodify algumas etapas de instalação e configuração.</span><span class="sxs-lookup"><span data-stu-id="e7780-116">If you use versions of MPI and OpenFOAM different from hello ones shown in this article, you might have toomodify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e7780-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e7780-117">Prerequisites</span></span>
* <span data-ttu-id="e7780-118">**Cluster HPC Pack com nós de computação do Linux compatíveis com RDMA** – Implante um cluster HPC Pack com nós de computação do Linux do tamanho A8, A9, H16r ou H16rm usando um [modelo do Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) ou um [script do Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="e7780-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="e7780-119">Consulte [começar conosco de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md) para pré-requisitos hello e as etapas para qualquer uma das opções.</span><span class="sxs-lookup"><span data-stu-id="e7780-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="e7780-120">Se você escolher Olá opção de implantação de script do PowerShell, consulte o arquivo de configuração de exemplo hello nos arquivos de exemplo hello final Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="e7780-120">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="e7780-121">Use este cluster de HPC Pack configuração toodeploy um baseado no Azure consiste em um nó de cabeçalho de tamanho A8 Windows Server 2012 R2 e nós de computação de tamanho de 2 A8 SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="e7780-121">Use this configuration toodeploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="e7780-122">Substitua os valores apropriados por sua assinatura e nomes de serviço.</span><span class="sxs-lookup"><span data-stu-id="e7780-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="e7780-123">**Outras coisas que você tooknow**</span><span class="sxs-lookup"><span data-stu-id="e7780-123">**Additional things tooknow**</span></span>
  
  * <span data-ttu-id="e7780-124">Para pré-requisitos de rede RDMA Linux no Azure, consulte [Tamanhos de VM de computação de alto desempenho](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e7780-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="e7780-125">Se você usar Olá opção de implantação de script do Powershell, implante todos os nós de computação Linux hello dentro de conexão de rede RDMA uma nuvem serviço toouse hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-125">If you use hello Powershell script deployment option, deploy all hello Linux compute nodes within one cloud service toouse hello RDMA network connection.</span></span>
  * <span data-ttu-id="e7780-126">Depois de implantar nós do Linux hello, conecte-se SSH tooperform outras tarefas administrativas.</span><span class="sxs-lookup"><span data-stu-id="e7780-126">After deploying hello Linux nodes, connect by SSH tooperform any additional administrative tasks.</span></span> <span data-ttu-id="e7780-127">Localize detalhes de conexão SSH Olá para cada VM do Linux no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e7780-127">Find hello SSH connection details for each Linux VM in hello Azure portal.</span></span>  
* <span data-ttu-id="e7780-128">**Intel MPI** -toorun OpenFOAM em SLES 12 HPC nós de computação no Azure, é necessário em tempo de execução do tooinstall Olá Intel MPI biblioteca 5 da saudação [site Intel.com](https://software.intel.com/en-us/intel-mpi-library/).</span><span class="sxs-lookup"><span data-stu-id="e7780-128">**Intel MPI** - toorun OpenFOAM on SLES 12 HPC compute nodes in Azure, you need tooinstall hello Intel MPI Library 5 runtime from hello [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="e7780-129">(O Intel MPI 5 está pré-instalado em imagens do HPC baseado em CentOS.)  Em uma etapa posterior, se necessário, instale o Intel MPI em seus nós de computação do Linux.</span><span class="sxs-lookup"><span data-stu-id="e7780-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="e7780-130">tooprepare para esta etapa, depois de registrar com a Intel, siga o link de saudação na Olá email toohello relacionados web página de confirmação.</span><span class="sxs-lookup"><span data-stu-id="e7780-130">tooprepare for this step, after you register with Intel, follow hello link in hello confirmation email toohello related web page.</span></span> <span data-ttu-id="e7780-131">Em seguida, Olá cópia baixar link para arquivo hello. tgz versão apropriada de saudação do Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="e7780-131">Then, copy hello download link for hello .tgz file for hello appropriate version of Intel MPI.</span></span> <span data-ttu-id="e7780-132">Este artigo se baseia no Intel MPI versão 5.0.3.048.</span><span class="sxs-lookup"><span data-stu-id="e7780-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="e7780-133">**Pacote de origem OpenFOAM** -baixar o software de pacote de origem OpenFOAM Olá para Linux de saudação [site OpenFOAM Foundation](http://openfoam.org/download/2-3-1-source/).</span><span class="sxs-lookup"><span data-stu-id="e7780-133">**OpenFOAM Source Pack** - Download hello OpenFOAM Source Pack software for Linux from hello [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="e7780-134">Este artigo baseia-se no Source Pack versão 2.3.1, disponível para download como OpenFOAM-2.3.1.tgz.</span><span class="sxs-lookup"><span data-stu-id="e7780-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="e7780-135">Siga instruções Olá posteriormente neste artigo toounpack e compilar OpenFOAM em nós de computação Linux hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-135">Follow hello instructions later in this article toounpack and compile OpenFOAM on hello Linux compute nodes.</span></span>
* <span data-ttu-id="e7780-136">**EnSight** (opcional) - resultados de saudação toosee de simulação OpenFOAM, baixe e instale Olá [EnSight](https://www.ceisoftware.com/download/) programa de visualização e análise.</span><span class="sxs-lookup"><span data-stu-id="e7780-136">**EnSight** (optional) - toosee hello results of your OpenFOAM simulation, download and install hello [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="e7780-137">São informações de licença e o download no site de EnSight hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-137">Licensing and download information are at hello EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="e7780-138">Configurar a relação de confiança mútua entre os nós de computação</span><span class="sxs-lookup"><span data-stu-id="e7780-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="e7780-139">Executar um trabalho de nó cruzado em vários nós do Linux requer Olá nós tootrust entre si (por **rsh** ou **ssh**).</span><span class="sxs-lookup"><span data-stu-id="e7780-139">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="e7780-140">Quando você cria o cluster de HPC Pack Olá com hello script de implantação do Microsoft HPC Pack IaaS, o script hello configura automaticamente confiança mútua permanente da conta de administrador Olá que você especificar.</span><span class="sxs-lookup"><span data-stu-id="e7780-140">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="e7780-141">Para usuários não-administrador que criar no domínio do cluster hello, você tem tooset a relação de confiança mútua temporária entre nós hello quando um trabalho é alocada toothem e destruir relação Olá após a conclusão do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7780-141">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem, and destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="e7780-142">confiança tooestablish para cada usuário, forneça um cluster de toohello de par de chaves RSA HPC Pack usa Olá relação de confiança.</span><span class="sxs-lookup"><span data-stu-id="e7780-142">tooestablish trust for each user, provide an RSA key pair toohello cluster that HPC Pack uses for hello trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="e7780-143">Gerar um par de chaves RSA</span><span class="sxs-lookup"><span data-stu-id="e7780-143">Generate an RSA key pair</span></span>
<span data-ttu-id="e7780-144">É fácil toogenerate um par de chaves RSA, que contém uma chave pública e uma chave privada, executando Olá Linux **ssh-keygen** comando.</span><span class="sxs-lookup"><span data-stu-id="e7780-144">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="e7780-145">Faça logon no tooa computador Linux.</span><span class="sxs-lookup"><span data-stu-id="e7780-145">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="e7780-146">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7780-146">Run hello following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="e7780-147">Pressione **Enter** toouse Olá configurações até que o comando Olá é concluído.</span><span class="sxs-lookup"><span data-stu-id="e7780-147">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="e7780-148">Não insira uma frase secreta aqui. Quando for solicitada uma senha, basta pressionar **Enter**.</span><span class="sxs-lookup"><span data-stu-id="e7780-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Gerar um par de chaves RSA][keygen]
3. <span data-ttu-id="e7780-150">Altere o diretório de ~/.ssh toohello do diretório.</span><span class="sxs-lookup"><span data-stu-id="e7780-150">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="e7780-151">chave privada Olá é armazenado na chave pública id_rsa e hello em id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="e7780-151">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![Chaves públicas e privadas][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="e7780-153">Adicionar um cluster de HPC Pack em toohello Olá par de chaves</span><span class="sxs-lookup"><span data-stu-id="e7780-153">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="e7780-154">Fazer um nó de cabeçalho de tooyour de conexão de área de trabalho remota com sua conta de administrador do HPC Pack (conta de administrador Olá configurada durante a execução do script de implantação de saudação).</span><span class="sxs-lookup"><span data-stu-id="e7780-154">Make a Remote Desktop connection tooyour head node with your HPC Pack administrator account (hello administrator account you set up when you ran hello deployment script).</span></span>
2. <span data-ttu-id="e7780-155">Use toocreate de procedimentos padrão do Windows Server uma conta de usuário de domínio no domínio do Active Directory do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-155">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="e7780-156">Por exemplo, use o hello usuário do Active Directory e a ferramenta de computadores no nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-156">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="e7780-157">exemplos de saudação neste artigo presumem que você criar um usuário de domínio chamado hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="e7780-157">hello examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="e7780-158">Crie um arquivo chamado C:\cred.xml e copiar Olá RSA chave dados nele.</span><span class="sxs-lookup"><span data-stu-id="e7780-158">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="e7780-159">É um arquivo de exemplo cred.xml final Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="e7780-159">A sample cred.xml file is at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="e7780-160">Abra um Prompt de comando e digite Olá Olá tooset credenciais dados da conta de hpclab\hpcuser de saudação do comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="e7780-160">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="e7780-161">Use Olá **extendeddata** toopass parâmetro hello nome de arquivo C:\cred.xml criado para dados de chave hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-161">You use hello **extendeddata** parameter toopass hello name of C:\cred.xml file you created for hello key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="e7780-162">Esse comando é concluído com êxito sem resultados.</span><span class="sxs-lookup"><span data-stu-id="e7780-162">This command completes successfully without output.</span></span> <span data-ttu-id="e7780-163">Depois de definir credenciais Olá Olá para contas de usuário que é necessário toorun trabalhos, armazenar o arquivo de cred.xml Olá em um local seguro ou exclua-o.</span><span class="sxs-lookup"><span data-stu-id="e7780-163">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="e7780-164">Se você gerou Olá par de chaves RSA em um de seus nós do Linux, lembre-se as chaves de saudação toodelete depois de terminar de usá-los.</span><span class="sxs-lookup"><span data-stu-id="e7780-164">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="e7780-165">Se o HPC Pack encontrar um arquivo id_rsa ou id_rsa.pub existente, ele não definirá uma relação de confiança mútua.</span><span class="sxs-lookup"><span data-stu-id="e7780-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7780-166">Não é recomendável executar um trabalho de Linux como um administrador de cluster em um cluster compartilhado, porque um trabalho enviada por um administrador é executado na conta de raiz de saudação em nós do Linux hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="e7780-167">No entanto, um trabalho enviada por um usuário não administrador é executado sob uma conta de usuário local do Linux com hello mesmo nome como usuário do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7780-167">However, a job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="e7780-168">Nesse caso, HPC Pack define a relação de confiança mútua para esse usuário do Linux em nós Olá alocadas toohello trabalho.</span><span class="sxs-lookup"><span data-stu-id="e7780-168">In this case, HPC Pack sets up mutual trust for this Linux user across hello nodes allocated toohello job.</span></span> <span data-ttu-id="e7780-169">Você pode configurar o usuário do Linux Olá manualmente em nós do Linux Olá antes de executar o trabalho de saudação ou HPC Pack cria usuário Olá automaticamente quando o trabalho de saudação é enviado.</span><span class="sxs-lookup"><span data-stu-id="e7780-169">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="e7780-170">Se o HPC Pack cria usuário hello, HPC Pack excluirá Olá trabalho concluído.</span><span class="sxs-lookup"><span data-stu-id="e7780-170">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="e7780-171">ameaças de segurança tooreduce, HPC Pack remove chaves Olá após a conclusão do trabalho.</span><span class="sxs-lookup"><span data-stu-id="e7780-171">tooreduce security threats, HPC Pack removes hello keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="e7780-172">Configurar um compartilhamento de arquivos para nós do Linux</span><span class="sxs-lookup"><span data-stu-id="e7780-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="e7780-173">Agora, configure um compartilhamento SMB padrão em uma pasta no nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-173">Now set up a standard SMB share on a folder on hello head node.</span></span> <span data-ttu-id="e7780-174">tooallow Olá Linux nós tooaccess arquivos de aplicativo com um caminho comum montagem Olá compartilhados pasta em nós do Linux hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-174">tooallow hello Linux nodes tooaccess application files with a common path, mount hello shared folder on hello Linux nodes.</span></span> <span data-ttu-id="e7780-175">Se desejar, você pode usar outra opção de compartilhamento de arquivos, como o compartilhamento de Arquivos do Azure - recomendado para muitos cenários - ou um compartilhamento NFS.</span><span class="sxs-lookup"><span data-stu-id="e7780-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="e7780-176">Consulte informações e etapas detalhadas de compartilhamento de arquivo hello [começar conosco de computação do Linux em um Cluster do HPC Pack no Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e7780-176">See hello file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="e7780-177">Crie uma pasta no nó principal hello e compartilhá-lo tooEveryone Configurando os privilégios de leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="e7780-177">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="e7780-178">Por exemplo, compartilhar C:\OpenFOAM no nó principal do hello como \\ \\SUSE12RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="e7780-178">For example, share C:\OpenFOAM on hello head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="e7780-179">Aqui, *SUSE12RDMA HN* é nome do host de saudação do nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-179">Here, *SUSE12RDMA-HN* is hello host name of hello head node.</span></span>
2. <span data-ttu-id="e7780-180">Abra uma janela do Windows PowerShell e execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7780-180">Open a Windows PowerShell window and run hello following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="e7780-181">Olá primeiro comando cria uma pasta chamada /openfoam em todos os nós no grupo de LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-181">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="e7780-182">comando segundo Olá monta Olá compartilhado pasta //SUSE12RDMA-HN/OpenFOAM em nós do Linux Olá com dir_mode e file_mode too777 de conjunto de bits.</span><span class="sxs-lookup"><span data-stu-id="e7780-182">hello second command mounts hello shared folder //SUSE12RDMA-HN/OpenFOAM on hello Linux nodes with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="e7780-183">Olá *username* e *senha* Olá comando deve ser credenciais de saudação de um usuário no nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-183">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="e7780-184">Olá "\\`" símbolo no segundo comando de saudação é um símbolo de escape para o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7780-184">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="e7780-185">"\\`,"significa hello"," (vírgula) é uma parte do comando hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-185">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="e7780-186">Instalar o MPI e o OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="e7780-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="e7780-187">toorun OpenFOAM como um trabalho MPI na rede RDMA Olá, é necessário toocompile OpenFOAM com bibliotecas de MPI Intel hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-187">toorun OpenFOAM as an MPI job on hello RDMA network, you need toocompile OpenFOAM with hello Intel MPI libraries.</span></span> 

<span data-ttu-id="e7780-188">Primeiro, execute várias **clusrun** comandos tooinstall bibliotecas de MPI Intel (se ainda não estiver instalado) e OpenFOAM em seus nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="e7780-188">First, run several **clusrun** commands tooinstall Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="e7780-189">Compartilhamento de nó principal do uso Olá configurado anteriormente arquivos de instalação de saudação tooshare entre nós do Linux hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-189">Use hello head node share configured previously tooshare hello installation files among hello Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7780-190">Essas etapas de instalação e compilação são exemplos.</span><span class="sxs-lookup"><span data-stu-id="e7780-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="e7780-191">É necessário algum conhecimento dos tooensure de administração do sistema Linux bibliotecas e compiladores dependentes estão instaladas corretamente.</span><span class="sxs-lookup"><span data-stu-id="e7780-191">You need some knowledge of Linux system administration tooensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="e7780-192">Talvez seja necessário toomodify determinadas variáveis de ambiente ou outras configurações para suas versões do Intel MPI e OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="e7780-192">You might need toomodify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="e7780-193">Para obter detalhes, consulte [Guia de instalação do Intel MPI Library para Linux](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) e [Instalação do OpenFOAM Source Pack](http://openfoam.org/download/2-3-1-source/) para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="e7780-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="e7780-194">Instalar o Intel MPI</span><span class="sxs-lookup"><span data-stu-id="e7780-194">Install Intel MPI</span></span>
<span data-ttu-id="e7780-195">Salve pacote de instalação baixado de saudação para Intel MPI (l_mpi_p_5.0.3.048.tgz neste exemplo) em C:\OpenFoam no nó de cabeçalho Olá para que nós do Linux Olá podem acessar esse arquivo de /openfoam.</span><span class="sxs-lookup"><span data-stu-id="e7780-195">Save hello downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="e7780-196">Em seguida, execute **clusrun** biblioteca de MPI Intel tooinstall em todos os nós do Linux hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-196">Then run **clusrun** tooinstall Intel MPI library on all hello Linux nodes.</span></span>

1. <span data-ttu-id="e7780-197">a seguir Olá comandos do pacote de instalação de saudação de cópia e extraia-muito/opt/intel em cada nó.</span><span class="sxs-lookup"><span data-stu-id="e7780-197">hello following commands copy hello installation package and extract it too/opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="e7780-198">tooinstall Intel MPI biblioteca silenciosamente, use um arquivo silent.cfg.</span><span class="sxs-lookup"><span data-stu-id="e7780-198">tooinstall Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="e7780-199">Você pode encontrar um exemplo no hello arquivos de exemplo no final deste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-199">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="e7780-200">Coloque esse arquivo no hello compartilhados /openfoam de pasta.</span><span class="sxs-lookup"><span data-stu-id="e7780-200">Place this file in hello shared folder /openfoam.</span></span> <span data-ttu-id="e7780-201">Para obter detalhes sobre o arquivo de silent.cfg hello, consulte [Intel MPI biblioteca para o guia de instalação do Linux - instalação silenciosa](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span><span class="sxs-lookup"><span data-stu-id="e7780-201">For details about hello silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="e7780-202">Salve o arquivo silent.cfg como um arquivo de texto com as terminações de linha do Linux (LF apenas, não CR LF).</span><span class="sxs-lookup"><span data-stu-id="e7780-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="e7780-203">Essa etapa garante que ele seja executado corretamente em nós do Linux hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-203">This step ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="e7780-204">Instale a Intel MPI Library no modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="e7780-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="e7780-205">Configurar o MPI</span><span class="sxs-lookup"><span data-stu-id="e7780-205">Configure MPI</span></span>
<span data-ttu-id="e7780-206">Para testar, você deve adicionar Olá linhas toohello /etc/security/limits.conf a seguir em cada um de nós do Linux hello:</span><span class="sxs-lookup"><span data-stu-id="e7780-206">For testing, you should add hello following lines toohello /etc/security/limits.conf on each of hello Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="e7780-207">Reinicie nós do Linux Olá depois de atualizar o arquivo de limits.conf hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-207">Restart hello Linux nodes after you update hello limits.conf file.</span></span> <span data-ttu-id="e7780-208">Por exemplo, use o seguinte Olá **clusrun** comando:</span><span class="sxs-lookup"><span data-stu-id="e7780-208">For example, use hello following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="e7780-209">Depois de reiniciar, verifique a que pasta compartilhada hello está montada como /openfoam.</span><span class="sxs-lookup"><span data-stu-id="e7780-209">After restarting, ensure that hello shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="e7780-210">Compilar e instalar o OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="e7780-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="e7780-211">Salve o pacote de instalação baixado de saudação para Olá tooC:\OpenFoam OpenFOAM fonte Pack (OpenFOAM 2.3.1.tgz neste exemplo) no nó de cabeçalho Olá para que nós do Linux Olá podem acessar esse arquivo de /openfoam.</span><span class="sxs-lookup"><span data-stu-id="e7780-211">Save hello downloaded installation package for hello OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) tooC:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="e7780-212">Em seguida, execute **clusrun** comandos Olá de toocompile OpenFOAM em todos os nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="e7780-212">Then run **clusrun** commands toocompile OpenFOAM on all hello Linux nodes.</span></span>

1. <span data-ttu-id="e7780-213">Criar uma pasta /opt/OpenFOAM em cada nó do Linux, pasta de toothis do pacote de origem de saudação cópia e extraia-o lá.</span><span class="sxs-lookup"><span data-stu-id="e7780-213">Create a folder /opt/OpenFOAM on each Linux node, copy hello source package toothis folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="e7780-214">toocompile OpenFOAM com hello Intel MPI biblioteca, primeiro configure algumas variáveis de ambiente para Intel MPI e OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="e7780-214">toocompile OpenFOAM with hello Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="e7780-215">Use um script de bash chamado settings.sh tooset Olá variáveis.</span><span class="sxs-lookup"><span data-stu-id="e7780-215">Use a bash script called settings.sh tooset hello variables.</span></span> <span data-ttu-id="e7780-216">Você pode encontrar um exemplo no hello arquivos de exemplo no final deste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-216">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="e7780-217">O local deste arquivo (salvo com terminações de linha do Linux) em Olá compartilhados /openfoam de pasta.</span><span class="sxs-lookup"><span data-stu-id="e7780-217">Place this file (saved with Linux line endings) in hello shared folder /openfoam.</span></span> <span data-ttu-id="e7780-218">Esse arquivo também contém configurações para Olá MPI OpenFOAM tempos de execução e que você use toorun posteriormente um trabalho OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="e7780-218">This file also contains settings for hello MPI and OpenFOAM runtimes that you use later toorun an OpenFOAM job.</span></span>
3. <span data-ttu-id="e7780-219">Instale pacotes dependentes necessário toocompile OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="e7780-219">Install dependent packages needed toocompile OpenFOAM.</span></span> <span data-ttu-id="e7780-220">Dependendo da distribuição do Linux, talvez seja necessário primeiro tooadd um repositório.</span><span class="sxs-lookup"><span data-stu-id="e7780-220">Depending on your Linux distribution, you might first need tooadd a repository.</span></span> <span data-ttu-id="e7780-221">Executar **clusrun** comandos a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="e7780-221">Run **clusrun** commands similar toohello following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="e7780-222">Se necessário, a saudação do SSH tooeach Linux nó toorun comandos tooconfirm que são executadas corretamente.</span><span class="sxs-lookup"><span data-stu-id="e7780-222">If necessary, SSH tooeach Linux node toorun hello commands tooconfirm that they run properly.</span></span>
4. <span data-ttu-id="e7780-223">Execute Olá comando toocompile OpenFOAM a seguir.</span><span class="sxs-lookup"><span data-stu-id="e7780-223">Run hello following command toocompile OpenFOAM.</span></span> <span data-ttu-id="e7780-224">o processo de compilação Olá leva algum tempo toocomplete e gera uma grande quantidade de saída de toostandard de informações de log, use Olá **/ intercaladas** opção de saída de hello toodisplay intercalada.</span><span class="sxs-lookup"><span data-stu-id="e7780-224">hello compilation process takes some time toocomplete and generates a large amount of log information toostandard output, so use hello **/interleaved** option toodisplay hello output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="e7780-225">Olá "\\`" símbolo no comando Olá é um símbolo de escape para o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e7780-225">hello “\\`” symbol in hello command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="e7780-226">"\\`&" significa Olá "&" é uma parte do comando hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-226">“\\`&” means hello “&” is a part of hello command.</span></span>
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a><span data-ttu-id="e7780-227">Preparar um trabalho de OpenFOAM de toorun</span><span class="sxs-lookup"><span data-stu-id="e7780-227">Prepare toorun an OpenFOAM job</span></span>
<span data-ttu-id="e7780-228">Agora Obtenha pronto toorun um trabalho MPI chamado sloshingTank3D, que é um dos exemplos de OpenFoam hello, em dois nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="e7780-228">Now get ready toorun an MPI job called sloshingTank3D, which is one of hello OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-hello-runtime-environment"></a><span data-ttu-id="e7780-229">Configurar o ambiente de tempo de execução de saudação</span><span class="sxs-lookup"><span data-stu-id="e7780-229">Set up hello runtime environment</span></span>
<span data-ttu-id="e7780-230">tooset ambientes de tempo de execução Olá para MPI e OpenFOAM em nós do Linux hello, executados Olá comando em uma janela do Windows PowerShell a seguir no nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-230">tooset up hello runtime environments for MPI and OpenFOAM on hello Linux nodes, run hello following command in a Windows PowerShell window on hello head node.</span></span> <span data-ttu-id="e7780-231">(Este comando é válido apenas para o Linux SUSE)</span><span class="sxs-lookup"><span data-stu-id="e7780-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="e7780-232">Preparar os dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="e7780-232">Prepare sample data</span></span>
<span data-ttu-id="e7780-233">Compartilhamento de nó principal do uso Olá foi configurado anteriormente tooshare arquivos entre os nós do Linux hello (montados como /openfoam).</span><span class="sxs-lookup"><span data-stu-id="e7780-233">Use hello head node share you configured previously tooshare files among hello Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="e7780-234">Nós de computação tooone SSH do seu Linux.</span><span class="sxs-lookup"><span data-stu-id="e7780-234">SSH tooone of your Linux compute nodes.</span></span>
2. <span data-ttu-id="e7780-235">Execute Olá após o comando tooset o ambiente de tempo de execução de OpenFOAM hello, se você ainda não tiver feito isso.</span><span class="sxs-lookup"><span data-stu-id="e7780-235">Run hello following command tooset up hello OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="e7780-236">Copie a pasta compartilhada do hello sloshingTank3D exemplo toohello e navegue tooit.</span><span class="sxs-lookup"><span data-stu-id="e7780-236">Copy hello sloshingTank3D sample toohello shared folder and navigate tooit.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="e7780-237">Quando você usa os parâmetros padrão Olá deste exemplo, pode levar dezenas de toorun minutos, portanto, talvez você queira toomodify toomake alguns parâmetros que ele executado mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="e7780-237">When you use hello default parameters of this sample, it can take tens of minutes toorun, so you might want toomodify some parameters toomake it run faster.</span></span> <span data-ttu-id="e7780-238">Uma opção simple é toomodify Olá tempo Etapa variáveis deltaT e writeInterval no arquivo de sistema/controlDict hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-238">One simple choice is toomodify hello time step variables deltaT and writeInterval in hello system/controlDict file.</span></span> <span data-ttu-id="e7780-239">Esse arquivo armazena todos os dados de entrada relacionados toohello controle de tempo e leitura e gravação de dados da solução.</span><span class="sxs-lookup"><span data-stu-id="e7780-239">This file stores all input data relating toohello control of time and reading and writing solution data.</span></span> <span data-ttu-id="e7780-240">Por exemplo, você pode alterar o valor de Olá de deltaT de 0,05 too0.5 e valor de saudação do writeInterval de too0.5 0,05.</span><span class="sxs-lookup"><span data-stu-id="e7780-240">For example, you could change hello value of deltaT from 0.05 too0.5 and hello value of writeInterval from 0.05 too0.5.</span></span>
   
   ![Modificar as variáveis da etapa][step_variables]
5. <span data-ttu-id="e7780-242">Especifique os valores desejados para variáveis de saudação no arquivo de sistema/decomposeParDict hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-242">Specify desired values for hello variables in hello system/decomposeParDict file.</span></span> <span data-ttu-id="e7780-243">Este exemplo usa dois nós Linux cada com 8 núcleos, portanto, definir numberOfSubdomains too16 e n hierarchicalCoeffs too(1 1 16), que significa OpenFOAM ser executados em paralelo com 16 processos.</span><span class="sxs-lookup"><span data-stu-id="e7780-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains too16 and n of hierarchicalCoeffs too(1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="e7780-244">Para obter mais informações, consulte [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4)(Guia do usuário OpenFOAM: 3.4 Execução de aplicativos em paralelo).</span><span class="sxs-lookup"><span data-stu-id="e7780-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![Decompor processos][decompose]
6. <span data-ttu-id="e7780-246">Execute Olá comandos a seguir de dados de exemplo hello sloshingTank3D directory tooprepare hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-246">Run hello following commands from hello sloshingTank3D directory tooprepare hello sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="e7780-247">No nó de cabeçalho Olá, você deve ver os arquivos de dados de exemplo hello são copiados para C:\OpenFoam\sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="e7780-247">On hello head node, you should see hello sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="e7780-248">(C:\OpenFoam é a pasta compartilhada Olá no nó de cabeçalho hello.)</span><span class="sxs-lookup"><span data-stu-id="e7780-248">(C:\OpenFoam is hello shared folder on hello head node.)</span></span>
   
   ![Arquivos de dados no nó principal Olá][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="e7780-250">Arquivo de host para mpirun</span><span class="sxs-lookup"><span data-stu-id="e7780-250">Host file for mpirun</span></span>
<span data-ttu-id="e7780-251">Nesta etapa, você criar um arquivo de host (uma lista de nós de computação) que Olá **mpirun** comando usa.</span><span class="sxs-lookup"><span data-stu-id="e7780-251">In this step, you create a host file (a list of compute nodes) which hello **mpirun** command uses.</span></span>

1. <span data-ttu-id="e7780-252">Em um de nós do Linux hello, crie um arquivo chamado arquivo de host em /openfoam, para que esse arquivo pode ser contatado pelo /openfoam/hostfile em todos os nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="e7780-252">On one of hello Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="e7780-253">Grave os nomes dos nós do Linux nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="e7780-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="e7780-254">Neste exemplo, o arquivo hello contém Olá nomes a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7780-254">In this example, hello file contains hello following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="e7780-255">Você também pode criar esse arquivo no C:\OpenFoam\hostfile no nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-255">You can also create this file at C:\OpenFoam\hostfile on hello head node.</span></span> <span data-ttu-id="e7780-256">Se você escolher esta opção, salve-o como um arquivo de texto com as terminações de linha do Linux (LF apenas, não CR LF).</span><span class="sxs-lookup"><span data-stu-id="e7780-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="e7780-257">Isso garante que ele seja executado corretamente em nós do Linux hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-257">This ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="e7780-258">**Wrapper de script bash**</span><span class="sxs-lookup"><span data-stu-id="e7780-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="e7780-259">Se você tiver muitos nós do Linux, e você desejar toorun seu trabalho em apenas alguns deles, não é um toouse recomendável um host fixo de arquivos, porque você não sabe quais nós serão alocados tooyour trabalho.</span><span class="sxs-lookup"><span data-stu-id="e7780-259">If you have many Linux nodes and you want your job toorun on only some of them, it’s not a good idea toouse a fixed host file, because you don’t know which nodes will be allocated tooyour job.</span></span> <span data-ttu-id="e7780-260">Nesse caso, grave um wrapper de script bash para **mpirun** toocreate Olá arquivo host automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e7780-260">In this case, write a bash script wrapper for **mpirun** toocreate hello host file automatically.</span></span> <span data-ttu-id="e7780-261">Você pode encontrar um wrapper de script do exemplo bash chamado hpcimpirun.sh no final deste artigo hello e salve-o como /openfoam/hpcimpirun.sh. Esse script de exemplo hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7780-261">You can find an example bash script wrapper called hpcimpirun.sh at hello end of this article, and save it as /openfoam/hpcimpirun.sh. This example script does hello following:</span></span>
   
   1. <span data-ttu-id="e7780-262">Define as variáveis de ambiente Olá para **mpirun**e alguns adição comando parâmetros toorun Olá MPI trabalho por meio da rede RDMA hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-262">Sets up hello environment variables for **mpirun**, and some addition command parameters toorun hello MPI job through hello RDMA network.</span></span> <span data-ttu-id="e7780-263">Nesse caso, ele define Olá variáveis a seguir:</span><span class="sxs-lookup"><span data-stu-id="e7780-263">In this case, it sets hello following variables:</span></span>
      
      * <span data-ttu-id="e7780-264">I_MPI_FABRICS=shm:dapl</span><span class="sxs-lookup"><span data-stu-id="e7780-264">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="e7780-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span><span class="sxs-lookup"><span data-stu-id="e7780-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="e7780-266">I_MPI_DYNAMIC_CONNECTION=0</span><span class="sxs-lookup"><span data-stu-id="e7780-266">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="e7780-267">Cria um arquivo de host de acordo com toohello variável de ambiente $CCP_NODES_CORES, que é definido por nó principal do HPC hello quando o trabalho de saudação é ativado.</span><span class="sxs-lookup"><span data-stu-id="e7780-267">Creates a host file according toohello environment variable $CCP_NODES_CORES, which is set by hello HPC head node when hello job is activated.</span></span>
      
      <span data-ttu-id="e7780-268">formato de saudação do $CCP_NODES_CORES segue este padrão:</span><span class="sxs-lookup"><span data-stu-id="e7780-268">hello format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="e7780-269">onde</span><span class="sxs-lookup"><span data-stu-id="e7780-269">where</span></span>
      
      * <span data-ttu-id="e7780-270">`<Number of nodes>`-número de saudação de nós alocado toothis trabalho.</span><span class="sxs-lookup"><span data-stu-id="e7780-270">`<Number of nodes>` - hello number of nodes allocated toothis job.</span></span>  
      * <span data-ttu-id="e7780-271">`<Name of node_n_...>`-nome de saudação de cada nó alocada toothis trabalho.</span><span class="sxs-lookup"><span data-stu-id="e7780-271">`<Name of node_n_...>` - hello name of each node allocated toothis job.</span></span>
      * <span data-ttu-id="e7780-272">`<Cores of node_n_...>`-Olá número de núcleos no trabalho do hello nó toothis alocado.</span><span class="sxs-lookup"><span data-stu-id="e7780-272">`<Cores of node_n_...>` - hello number of cores on hello node allocated toothis job.</span></span>
      
      <span data-ttu-id="e7780-273">Por exemplo, se o trabalho de saudação precisa toorun de dois nós, $CCP_NODES_CORES é semelhante a</span><span class="sxs-lookup"><span data-stu-id="e7780-273">For example, if hello job needs two nodes toorun, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="e7780-274">Saudação de chamadas **mpirun** de comando e acrescenta dois parâmetros toohello comando linha.</span><span class="sxs-lookup"><span data-stu-id="e7780-274">Calls hello **mpirun** command and appends two parameters toohello command line.</span></span>
      
      * <span data-ttu-id="e7780-275">`--hostfile <hostfilepath>: <hostfilepath>`-Olá caminho do script de saudação do arquivo de host Olá cria</span><span class="sxs-lookup"><span data-stu-id="e7780-275">`--hostfile <hostfilepath>: <hostfilepath>` - hello path of hello host file hello script creates</span></span>
      * <span data-ttu-id="e7780-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-uma variável de ambiente definida pelo Olá HPC Pack nó principal, que armazena o número de saudação de núcleos total alocada toothis trabalho.</span><span class="sxs-lookup"><span data-stu-id="e7780-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by hello HPC Pack head node, which stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="e7780-277">Nesse caso, ele especifica o número de saudação de processos para **mpirun**.</span><span class="sxs-lookup"><span data-stu-id="e7780-277">In this case, it specifies hello number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="e7780-278">Enviar um trabalho do OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="e7780-278">Submit an OpenFOAM job</span></span>
<span data-ttu-id="e7780-279">Agora, você pode enviar um trabalho no Gerenciador de Cluster de HPC.</span><span class="sxs-lookup"><span data-stu-id="e7780-279">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="e7780-280">É necessário toopass Olá script hpcimpirun.sh nas linhas de comando Olá para algumas das tarefas de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-280">You need toopass hello script hpcimpirun.sh in hello command lines for some of hello job tasks.</span></span>

1. <span data-ttu-id="e7780-281">Conecte-se o nó principal do cluster tooyour e iniciar o Gerenciador de Cluster de HPC.</span><span class="sxs-lookup"><span data-stu-id="e7780-281">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="e7780-282">**No gerenciamento de recursos**, verifique se nós de computação Olá Linux estão em Olá **Online** estado.</span><span class="sxs-lookup"><span data-stu-id="e7780-282">**In Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="e7780-283">Se não estiverem, selecione-os e clique em **Colocar Online**.</span><span class="sxs-lookup"><span data-stu-id="e7780-283">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="e7780-284">Em **Gerenciamento de Trabalhos**, clique em **Novo Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="e7780-284">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="e7780-285">Insira um nome para o trabalho, como *sloshingTank3D*.</span><span class="sxs-lookup"><span data-stu-id="e7780-285">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![Detalhes do trabalho][job_details]
5. <span data-ttu-id="e7780-287">Em **recursos de trabalho**, escolha o tipo de saudação do recurso como "Nó" e defina Olá mínimo too2.</span><span class="sxs-lookup"><span data-stu-id="e7780-287">In **Job resources**, choose hello type of resource as “Node” and set hello Minimum too2.</span></span> <span data-ttu-id="e7780-288">Essa configuração executa o trabalho de saudação em dois nós do Linux, cada um deles tem oito núcleos neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="e7780-288">This configuration runs hello job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![Recursos de trabalho][job_resources]
6. <span data-ttu-id="e7780-290">Clique em **editar tarefas** Olá navegação esquerdo e, em seguida, clique em **adicionar** tooadd um trabalho de toohello de tarefa.</span><span class="sxs-lookup"><span data-stu-id="e7780-290">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span> <span data-ttu-id="e7780-291">Adicionar quatro tarefas toohello trabalho Olá linhas de comando e as configurações a seguir.</span><span class="sxs-lookup"><span data-stu-id="e7780-291">Add four tasks toohello job with hello following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e7780-292">Executando `source /openfoam/settings.sh` configura ambientes de tempo de execução de OpenFOAM e MPI da saudação, para cada uma das seguintes tarefas de saudação chamá-lo antes de saudação OpenFOAM comando.</span><span class="sxs-lookup"><span data-stu-id="e7780-292">Running `source /openfoam/settings.sh` sets up hello OpenFOAM and MPI runtime environments, so each of hello following tasks calls it before hello OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="e7780-293">**Tarefa 1**.</span><span class="sxs-lookup"><span data-stu-id="e7780-293">**Task 1**.</span></span> <span data-ttu-id="e7780-294">Executar **decomposePar** toogenerate arquivos de dados para a execução **interDyMFoam** em paralelo.</span><span class="sxs-lookup"><span data-stu-id="e7780-294">Run **decomposePar** toogenerate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="e7780-295">Atribuir uma tarefa de toohello de nó</span><span class="sxs-lookup"><span data-stu-id="e7780-295">Assign one node toohello task</span></span>
     * <span data-ttu-id="e7780-296">**Linha de comando** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="e7780-296">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="e7780-297">**Diretório de trabalho** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="e7780-297">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="e7780-298">Consulte Olá figura a seguir.</span><span class="sxs-lookup"><span data-stu-id="e7780-298">See hello following figure.</span></span> <span data-ttu-id="e7780-299">Você pode configurar as tarefas restantes Olá da mesma forma.</span><span class="sxs-lookup"><span data-stu-id="e7780-299">You configure hello remaining tasks similarly.</span></span>
     
     ![Detalhes da tarefa 1][task_details1]
   * <span data-ttu-id="e7780-301">**Tarefa 2**.</span><span class="sxs-lookup"><span data-stu-id="e7780-301">**Task 2**.</span></span> <span data-ttu-id="e7780-302">Executar **interDyMFoam** no exemplo de hello toocompute paralela.</span><span class="sxs-lookup"><span data-stu-id="e7780-302">Run **interDyMFoam** in parallel toocompute hello sample.</span></span>
     
     * <span data-ttu-id="e7780-303">Atribuir tarefas de toohello dois nós</span><span class="sxs-lookup"><span data-stu-id="e7780-303">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="e7780-304">**Linha de comando** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="e7780-304">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="e7780-305">**Diretório de trabalho** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="e7780-305">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="e7780-306">**Tarefa 3**.</span><span class="sxs-lookup"><span data-stu-id="e7780-306">**Task 3**.</span></span> <span data-ttu-id="e7780-307">Executar **reconstructPar** toomerge Olá conjuntos dos diretórios de tempo de cada diretório processor_N_ em um único conjunto.</span><span class="sxs-lookup"><span data-stu-id="e7780-307">Run **reconstructPar** toomerge hello sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="e7780-308">Atribuir uma tarefa de toohello de nó</span><span class="sxs-lookup"><span data-stu-id="e7780-308">Assign one node toohello task</span></span>
     * <span data-ttu-id="e7780-309">**Linha de comando** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="e7780-309">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="e7780-310">**Diretório de trabalho** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="e7780-310">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="e7780-311">**Tarefa 4**.</span><span class="sxs-lookup"><span data-stu-id="e7780-311">**Task 4**.</span></span> <span data-ttu-id="e7780-312">Executar **foamToEnsight** em paralelo tooconvert arquivos de resultado Olá OpenFOAM em EnSight formatar em colocar arquivos de EnSight de saudação em um diretório chamado Ensight no diretório caso hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-312">Run **foamToEnsight** in parallel tooconvert hello OpenFOAM result files into EnSight format and place hello EnSight files in a directory named Ensight in hello case directory.</span></span>
     
     * <span data-ttu-id="e7780-313">Atribuir tarefas de toohello dois nós</span><span class="sxs-lookup"><span data-stu-id="e7780-313">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="e7780-314">**Linha de comando** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="e7780-314">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="e7780-315">**Diretório de trabalho** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="e7780-315">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="e7780-316">Adicione tarefas de toothese dependências na tarefa ordem crescente.</span><span class="sxs-lookup"><span data-stu-id="e7780-316">Add dependencies toothese tasks in ascending task order.</span></span>
   
   ![Dependências da tarefa][task_dependencies]
8. <span data-ttu-id="e7780-318">Clique em **enviar** toorun esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="e7780-318">Click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="e7780-319">Por padrão, o HPC Pack envia trabalho hello como sua conta de logon do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="e7780-319">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="e7780-320">Depois de clicar em **enviar**, você verá uma caixa de diálogo solicitando que você tooenter Olá nome e uma senha.</span><span class="sxs-lookup"><span data-stu-id="e7780-320">After you click **Submit**, you might see a dialog box prompting you tooenter hello user name and password.</span></span>
   
   ![Credenciais de trabalho][creds]
   
   <span data-ttu-id="e7780-322">Sob algumas condições, o HPC Pack lembra informações de usuário de saudação antes de entrada e não mostrar esta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e7780-322">Under some conditions, HPC Pack remembers hello user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="e7780-323">toomake HPC Pack mostrá-la novamente, insira Olá comando no prompt de comando a seguir e, em seguida, enviar o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7780-323">toomake HPC Pack show it again, enter hello following command at a Command prompt and then submit hello job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="e7780-324">trabalho de saudação leva de dezenas de minutos tooseveral horas de acordo com os parâmetros de toohello que você definiu para o exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-324">hello job takes from tens of minutes tooseveral hours according toohello parameters you have set for hello sample.</span></span> <span data-ttu-id="e7780-325">Mapa de calor hello, você verá trabalho Olá em execução em nós do Linux hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-325">In hello heat map, you see hello job running on hello Linux nodes.</span></span> 
   
   ![Mapa de calor][heat_map]
   
   <span data-ttu-id="e7780-327">Em cada nó, oito processos são iniciados.</span><span class="sxs-lookup"><span data-stu-id="e7780-327">On each node, eight processes are started.</span></span>
   
   ![Processos do Linux][linux_processes]
10. <span data-ttu-id="e7780-329">Quando termina de trabalho hello, localize resultados do trabalho Olá nas pastas C:\OpenFoam\sloshingTank3D e os arquivos de log de saudação em C:\OpenFoam.</span><span class="sxs-lookup"><span data-stu-id="e7780-329">When hello job finishes, find hello job results in folders under C:\OpenFoam\sloshingTank3D, and hello log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="e7780-330">Exibir resultados no EnSight</span><span class="sxs-lookup"><span data-stu-id="e7780-330">View results in EnSight</span></span>
<span data-ttu-id="e7780-331">Opcionalmente, use [EnSight](https://www.ceisoftware.com/) toovisualize e analisar os resultados de saudação do trabalho de OpenFOAM hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-331">Optionally use [EnSight](https://www.ceisoftware.com/) toovisualize and analyze hello results of hello OpenFOAM job.</span></span> <span data-ttu-id="e7780-332">Para obter mais informações sobre a visualização e a animação no EnSight, consulte o [guia em vídeo](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span><span class="sxs-lookup"><span data-stu-id="e7780-332">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="e7780-333">Depois de instalar EnSight no nó principal do hello, inicie-o.</span><span class="sxs-lookup"><span data-stu-id="e7780-333">After you install EnSight on hello head node, start it.</span></span>
2. <span data-ttu-id="e7780-334">Abra o C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span><span class="sxs-lookup"><span data-stu-id="e7780-334">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="e7780-335">Você verá um tanque no Visualizador de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7780-335">You see a tank in hello viewer.</span></span>
   
   ![Tanque no EnSight][tank]
3. <span data-ttu-id="e7780-337">Criar um **Isosurface** de **internalMesh**e, em seguida, escolha variável Olá **alpha_water**.</span><span class="sxs-lookup"><span data-stu-id="e7780-337">Create an **Isosurface** from **internalMesh**, and then choose hello variable **alpha_water**.</span></span>
   
   ![Criar um isosurface][isosurface]
4. <span data-ttu-id="e7780-339">Definir cor Olá para **Isosurface_part** criado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-339">Set hello color for **Isosurface_part** created in hello previous step.</span></span> <span data-ttu-id="e7780-340">Por exemplo, defina-toowater azul.</span><span class="sxs-lookup"><span data-stu-id="e7780-340">For example, set it toowater blue.</span></span>
   
   ![Editar cor do isosurface][isosurface_color]
5. <span data-ttu-id="e7780-342">Criar um **volume Iso** de **paredes** selecionando **paredes** em Olá **partes** painel e clique em Olá **Isosurfaces**  botão na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7780-342">Create an **Iso-volume** from **walls** by selecting **walls** in hello **Parts** panel and click hello **Isosurfaces** button in hello toolbar.</span></span>
6. <span data-ttu-id="e7780-343">Na caixa de diálogo hello, selecione **tipo** como **Isovolume** e defina Olá Min de **Isovolume intervalo** too0.5.</span><span class="sxs-lookup"><span data-stu-id="e7780-343">In hello dialog box, select **Type** as **Isovolume** and set hello Min of **Isovolume range** too0.5.</span></span> <span data-ttu-id="e7780-344">toocreate Olá isovolume, clique em **criar com partes selecionadas**.</span><span class="sxs-lookup"><span data-stu-id="e7780-344">toocreate hello isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="e7780-345">Definir cor Olá para **Iso_volume_part** criado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="e7780-345">Set hello color for **Iso_volume_part** created in hello previous step.</span></span> <span data-ttu-id="e7780-346">Por exemplo, defina-água toodeep azul.</span><span class="sxs-lookup"><span data-stu-id="e7780-346">For example, set it toodeep water blue.</span></span>
8. <span data-ttu-id="e7780-347">Definir cor Olá para **paredes**.</span><span class="sxs-lookup"><span data-stu-id="e7780-347">Set hello color for **walls**.</span></span> <span data-ttu-id="e7780-348">Por exemplo, defina-tootransparent branco.</span><span class="sxs-lookup"><span data-stu-id="e7780-348">For example, set it tootransparent white.</span></span>
9. <span data-ttu-id="e7780-349">Agora clique **reproduzir** toosee resultados de saudação de simulação de saudação.</span><span class="sxs-lookup"><span data-stu-id="e7780-349">Now click **Play** toosee hello results of hello simulation.</span></span>
   
    ![Resultado do tanque][tank_result]

## <a name="sample-files"></a><span data-ttu-id="e7780-351">Arquivos de exemplo</span><span class="sxs-lookup"><span data-stu-id="e7780-351">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="e7780-352">Exemplo de arquivo de configuração XML para implantação de cluster pelo script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="e7780-352">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a><span data-ttu-id="e7780-353">Exemplo de arquivo cred.xml</span><span class="sxs-lookup"><span data-stu-id="e7780-353">Sample cred.xml file</span></span>
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```
### <a name="sample-silentcfg-file-tooinstall-mpi"></a><span data-ttu-id="e7780-354">Exemplo silent.cfg arquivo tooinstall MPI</span><span class="sxs-lookup"><span data-stu-id="e7780-354">Sample silent.cfg file tooinstall MPI</span></span>
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="e7780-355">Script settings.sh de exemplo</span><span class="sxs-lookup"><span data-stu-id="e7780-355">Sample settings.sh script</span></span>
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="e7780-356">Script hpcimpirun.sh de exemplo</span><span class="sxs-lookup"><span data-stu-id="e7780-356">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png
