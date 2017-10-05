---
title: Executar o OpenFOAM com o HPC Pack nas VMs do Linux | Microsoft Docs
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
ms.openlocfilehash: ef124a8983fa112d499252460bff9ed2fcccc02b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="1bbd5-103">Executar o OpenFoam com o Microsoft HPC Pack em um cluster de RDMA do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="1bbd5-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="1bbd5-104">Este artigo mostra uma maneira de executar OpenFoam em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-104">This article shows you one way to run OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="1bbd5-105">Aqui, você implanta um cluster do Microsoft HPC Pack com nós de computação do Linux no Azure e executa um trabalho [OpenFoam](http://openfoam.com/) com Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="1bbd5-106">Você pode usar VMs do Azure compatíveis com RDMA para os nós de computação, para que eles se comuniquem pela rede RDMA do Azure.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-106">You can use RDMA-capable Azure VMs for the compute nodes, so that the compute nodes communicate over the Azure RDMA network.</span></span> <span data-ttu-id="1bbd5-107">Outras opções para executar o OpenFoam no Azure incluem imagens comerciais totalmente configuradas disponíveis no Marketplace, como [OpenFoam 2.3 no CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/) da UberCloud e executando no [Lote do Azure](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span><span class="sxs-lookup"><span data-stu-id="1bbd5-107">Other options to run OpenFoam in Azure include fully configured commercial images available in the Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="1bbd5-108">OpenFOAM (Operação e Manipulação de Campo Aberto) é um pacote de software com CFD (dinâmica de fluido computacional) aberto, amplamente utilizado na Engenharia e nas Ciências em organizações comerciais e acadêmicas.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="1bbd5-109">Ele inclui ferramentas para criar malhas, especialmente o snappyHexMesh, um mesher em paralelo para geometrias CAD complexas e de pré e pós-processamento.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="1bbd5-110">Quase todos os processos são executados em paralelo, permitindo que os usuários se beneficiam do hardware do computador à sua disposição.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-110">Almost all processes run in parallel, enabling users to take full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="1bbd5-111">O Microsoft HPC Pack fornece recursos para executar aplicativos de HPC e paralelos em larga escala, incluindo aplicativos MPI, em clusters de máquinas virtuais do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-111">Microsoft HPC Pack provides features to run large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="1bbd5-112">O HPC Pack também dá suporte a aplicativos de HPC no Linux em VMs com nós de computação do Linux implantadas em um cluster do HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="1bbd5-113">Consulte a [Introdução aos nós de computação do Linux em um cluster do HPC Pack no Azure](hpcpack-cluster.md) para saber como começar a usar os nós de computação do Linux com o HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction to using Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="1bbd5-114">Este artigo ilustra como executar uma carga de trabalho do Linux MPI com o HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-114">This article illustrates how to run a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="1bbd5-115">Ele pressupõe que você tem alguma familiaridade com a administração do sistema Linux e com a execução das cargas de trabalho MPI nos clusters do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="1bbd5-116">Se você usar versões do MPI e do OpenFOAM diferentes daquelas mostradas neste artigo, você talvez precise modificar algumas etapas de instalação e configuração.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-116">If you use versions of MPI and OpenFOAM different from the ones shown in this article, you might have to modify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1bbd5-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1bbd5-117">Prerequisites</span></span>
* <span data-ttu-id="1bbd5-118">**Cluster HPC Pack com nós de computação do Linux compatíveis com RDMA** – Implante um cluster HPC Pack com nós de computação do Linux do tamanho A8, A9, H16r ou H16rm usando um [modelo do Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) ou um [script do Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="1bbd5-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="1bbd5-119">Consulte [Introdução a nós de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md) para encontrar os pré-requisitos e etapas de cada opção.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span></span> <span data-ttu-id="1bbd5-120">Se você escolher a opção de implantação de script do PowerShell, consulte o arquivo de configuração de exemplo nos arquivos de exemplo no final deste artigo.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-120">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span></span> <span data-ttu-id="1bbd5-121">Use esta configuração para implantar um cluster de HPC Pack com base no Azure consistindo em um nó principal do tamanho do A8 Windows Server 2012 R2 e dois nós de computação do tamanho do A8 SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-121">Use this configuration to deploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="1bbd5-122">Substitua os valores apropriados por sua assinatura e nomes de serviço.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="1bbd5-123">**Informações adicionais importantes**</span><span class="sxs-lookup"><span data-stu-id="1bbd5-123">**Additional things to know**</span></span>
  
  * <span data-ttu-id="1bbd5-124">Para pré-requisitos de rede RDMA Linux no Azure, consulte [Tamanhos de VM de computação de alto desempenho](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1bbd5-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="1bbd5-125">Se você usar a opção de implantação de script do Powershell, implante todos os nós de computação Linux em um serviço de nuvem para usar a conexão de rede RDMA.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-125">If you use the Powershell script deployment option, deploy all the Linux compute nodes within one cloud service to use the RDMA network connection.</span></span>
  * <span data-ttu-id="1bbd5-126">Depois de implantar os nós do Linux, conecte-se via SSH para executar tarefas administrativas adicionais.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-126">After deploying the Linux nodes, connect by SSH to perform any additional administrative tasks.</span></span> <span data-ttu-id="1bbd5-127">Encontre os detalhes da conexão SSH para cada VM do Linux no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-127">Find the SSH connection details for each Linux VM in the Azure portal.</span></span>  
* <span data-ttu-id="1bbd5-128">**Intel MPI** – Para executar o OpenFOAM em nós de computação SLES 12 HPC no Azure, é necessário instalar o tempo de execução do Intel MPI Library 5 no site [Intel.com](https://software.intel.com/en-us/intel-mpi-library/).</span><span class="sxs-lookup"><span data-stu-id="1bbd5-128">**Intel MPI** - To run OpenFOAM on SLES 12 HPC compute nodes in Azure, you need to install the Intel MPI Library 5 runtime from the [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="1bbd5-129">(O Intel MPI 5 está pré-instalado em imagens do HPC baseado em CentOS.)  Em uma etapa posterior, se necessário, instale o Intel MPI em seus nós de computação do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="1bbd5-130">Para se preparar para essa etapa, depois de se registrar na Intel, siga o link no email de confirmação para a página da Web relacionada.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-130">To prepare for this step, after you register with Intel, follow the link in the confirmation email to the related web page.</span></span> <span data-ttu-id="1bbd5-131">Em seguida, copie o link de download do arquivo .tgz para a versão apropriada do Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-131">Then, copy the download link for the .tgz file for the appropriate version of Intel MPI.</span></span> <span data-ttu-id="1bbd5-132">Este artigo se baseia no Intel MPI versão 5.0.3.048.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="1bbd5-133">**OpenFOAM Source Pack** - baixe o software OpenFOAM Source Pack do Linux no [site OpenFOAM Foundation](http://openfoam.org/download/2-3-1-source/).</span><span class="sxs-lookup"><span data-stu-id="1bbd5-133">**OpenFOAM Source Pack** - Download the OpenFOAM Source Pack software for Linux from the [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="1bbd5-134">Este artigo baseia-se no Source Pack versão 2.3.1, disponível para download como OpenFOAM-2.3.1.tgz.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="1bbd5-135">Siga as instruções neste artigo para descompactar e compilar o OpenFOAM nos nós de computação do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-135">Follow the instructions later in this article to unpack and compile OpenFOAM on the Linux compute nodes.</span></span>
* <span data-ttu-id="1bbd5-136">**EnSight** (opcional): para ver os resultados da simulação do OpenFOAM, baixe e instale o programa de análise e visualização [EnSight](https://www.ceisoftware.com/download/) .</span><span class="sxs-lookup"><span data-stu-id="1bbd5-136">**EnSight** (optional) - To see the results of your OpenFOAM simulation, download and install the [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="1bbd5-137">As informações de licenciamento e download estão no site EnSight.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-137">Licensing and download information are at the EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="1bbd5-138">Configurar a relação de confiança mútua entre os nós de computação</span><span class="sxs-lookup"><span data-stu-id="1bbd5-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="1bbd5-139">Executar um trabalho de nós cruzados em vários nós do Linux requer que os nós tenham uma relação de confiança entre si (por **rsh** ou **ssh**).</span><span class="sxs-lookup"><span data-stu-id="1bbd5-139">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="1bbd5-140">Quando você cria o cluster do HPC Pack com o script de implantação de IaaS do Microsoft HPC Pack, o script configura automaticamente uma relação de confiança mútua permanente para a conta de administrador que você especificar.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-140">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span></span> <span data-ttu-id="1bbd5-141">Para usuários que não sejam administradores criados no domínio do cluster, é necessário configurar uma relação de confiança mútua temporária entre os nós quando um trabalho é alocado para eles e destruir a relação depois que o trabalho for concluído.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-141">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them, and destroy the relationship after the job is complete.</span></span> <span data-ttu-id="1bbd5-142">Para estabelecer confiança para cada usuário, forneça um par de chaves RSA para o cluster usado pelo HPC Pack para a relação de confiança.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-142">To establish trust for each user, provide an RSA key pair to the cluster that HPC Pack uses for the trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="1bbd5-143">Gerar um par de chaves RSA</span><span class="sxs-lookup"><span data-stu-id="1bbd5-143">Generate an RSA key pair</span></span>
<span data-ttu-id="1bbd5-144">É fácil gerar um par de chaves RSA, que contém uma chave pública e uma chave privada, executando o comando **ssh-keygen** do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-144">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="1bbd5-145">Faça logon em um computador com Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-145">Log on to a Linux computer.</span></span>
2. <span data-ttu-id="1bbd5-146">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1bbd5-146">Run the following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="1bbd5-147">Pressione **Enter** para usar as configurações padrão até que o comando seja concluído.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-147">Press **Enter** to use the default settings until the command is completed.</span></span> <span data-ttu-id="1bbd5-148">Não insira uma frase secreta aqui. Quando for solicitada uma senha, basta pressionar **Enter**.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Gerar um par de chaves RSA][keygen]
3. <span data-ttu-id="1bbd5-150">Altere o diretório para o diretório ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-150">Change directory to the ~/.ssh directory.</span></span> <span data-ttu-id="1bbd5-151">A chave privada é armazenada em id_rsa e a chave pública em id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-151">The private key is stored in id_rsa and the public key in id_rsa.pub.</span></span>
   
   ![Chaves públicas e privadas][keys]

### <a name="add-the-key-pair-to-the-hpc-pack-cluster"></a><span data-ttu-id="1bbd5-153">Adicionar o par de chaves ao cluster do HPC Pack</span><span class="sxs-lookup"><span data-stu-id="1bbd5-153">Add the key pair to the HPC Pack cluster</span></span>
1. <span data-ttu-id="1bbd5-154">Faça uma conexão da Área de Trabalho Remota com o nó principal com sua conta de administrador do HPC Pack (a conta de administrador criada quando você executou o script de implantação).</span><span class="sxs-lookup"><span data-stu-id="1bbd5-154">Make a Remote Desktop connection to your head node with your HPC Pack administrator account (the administrator account you set up when you ran the deployment script).</span></span>
2. <span data-ttu-id="1bbd5-155">Use os procedimentos padrão do Windows Server para criar uma conta de usuário de domínio no domínio do Active Directory do cluster.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-155">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span></span> <span data-ttu-id="1bbd5-156">Por exemplo, use o Usuário do Active Directory e a ferramenta Computers no nó principal.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-156">For example, use the Active Directory User and Computers tool on the head node.</span></span> <span data-ttu-id="1bbd5-157">Com os exemplos neste artigo, supomos que você criará um usuário de domínio chamado hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-157">The examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="1bbd5-158">Crie um arquivo chamado C:\cred.xml e copie os dados da chave RSA nele.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-158">Create a file named C:\cred.xml and copy the RSA key data into it.</span></span> <span data-ttu-id="1bbd5-159">Um arquivo cred.xml de exemplo está no final deste artigo.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-159">A sample cred.xml file is at the end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy the contents of private key here</PrivateKey>
     <PublicKey>Copy the contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="1bbd5-160">Abra um Prompt de Comando e digite o seguinte comando para definir os dados de credenciais para a conta de hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-160">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span></span> <span data-ttu-id="1bbd5-161">Use o parâmetro **extendeddata** para transmitir o nome do arquivo C:\cred.xml que você criou para os dados da chave.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-161">You use the **extendeddata** parameter to pass the name of C:\cred.xml file you created for the key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="1bbd5-162">Esse comando é concluído com êxito sem resultados.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-162">This command completes successfully without output.</span></span> <span data-ttu-id="1bbd5-163">Depois de definir as credenciais para as contas de usuário, você precisa executar os trabalhos, armazenar o arquivo cred.xml em um local seguro ou excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-163">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="1bbd5-164">Se você gerou o par de chaves RSA em um dos nós do Linux, lembre-se de excluir as chaves após terminar de usá-las.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-164">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span></span> <span data-ttu-id="1bbd5-165">Se o HPC Pack encontrar um arquivo id_rsa ou id_rsa.pub existente, ele não definirá uma relação de confiança mútua.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1bbd5-166">Não recomendamos executar um trabalho do Linux como um administrador de cluster em um cluster compartilhado, já que um trabalho enviado por um administrador é executado na conta raiz nos nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span></span> <span data-ttu-id="1bbd5-167">No entanto, um trabalho enviado por um usuário não administrador é executado sob uma conta de usuário local do Linux com o mesmo nome que o usuário do trabalho.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-167">However, a job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span></span> <span data-ttu-id="1bbd5-168">Nesse caso, HPC Pack define a relação de confiança mútua para este usuário Linux em todos os nós alocados para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-168">In this case, HPC Pack sets up mutual trust for this Linux user across the nodes allocated to the job.</span></span> <span data-ttu-id="1bbd5-169">Você pode configurar o usuário do Linux manualmente nos nós do Linux antes de executar o trabalho, ou o HPC Pack criará o usuário automaticamente quando o trabalho for enviado.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-169">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span></span> <span data-ttu-id="1bbd5-170">Se o HPC Pack criar o usuário, ele o excluirá depois que o trabalho for concluído.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-170">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span></span> <span data-ttu-id="1bbd5-171">Para reduzir ameaças de segurança, o HPC Pack remove as chaves após a conclusão do trabalho.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-171">To reduce security threats, HPC Pack removes the keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="1bbd5-172">Configurar um compartilhamento de arquivos para nós do Linux</span><span class="sxs-lookup"><span data-stu-id="1bbd5-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="1bbd5-173">Agora, configure um compartilhamento SMB padrão em uma pasta no nó principal.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-173">Now set up a standard SMB share on a folder on the head node.</span></span> <span data-ttu-id="1bbd5-174">Para permitir que os nós do Linux acessem os arquivos do aplicativo com um caminho comum, monte a pasta compartilhada nos nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-174">To allow the Linux nodes to access application files with a common path, mount the shared folder on the Linux nodes.</span></span> <span data-ttu-id="1bbd5-175">Se desejar, você pode usar outra opção de compartilhamento de arquivos, como o compartilhamento de Arquivos do Azure - recomendado para muitos cenários - ou um compartilhamento NFS.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="1bbd5-176">Consulte as informações de compartilhamento arquivos e as etapas detalhadas em [Introdução aos nós de computação Linux em um Cluster do HPC Pack no Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="1bbd5-176">See the file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="1bbd5-177">Crie uma pasta no nó principal e compartilhe-a com todos, configurando privilégios de leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-177">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span></span> <span data-ttu-id="1bbd5-178">Por exemplo, compartilhe C:\OpenFOAM no nó principal como \\\\SUSE12RDMA-HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-178">For example, share C:\OpenFOAM on the head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="1bbd5-179">Aqui, *SUSE12RDMA-HN* é o nome de host do nó principal.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-179">Here, *SUSE12RDMA-HN* is the host name of the head node.</span></span>
2. <span data-ttu-id="1bbd5-180">Abra uma janela do Windows PowerShell e execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="1bbd5-180">Open a Windows PowerShell window and run the following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="1bbd5-181">O primeiro comando cria uma pasta chamada /openfoam em todos os nós no grupo LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-181">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="1bbd5-182">O segundo comando monta a pasta compartilhada //SUSE12RDMA-HN/OpenFOAM nos nós do Linux com os bits dir_mode e file_mode definidos como 777.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-182">The second command mounts the shared folder //SUSE12RDMA-HN/OpenFOAM on the Linux nodes with dir_mode and file_mode bits set to 777.</span></span> <span data-ttu-id="1bbd5-183">O *nome de usuário* e a *senha* no comando devem ser as credenciais de um usuário no nó principal.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-183">The *username* and *password* in the command should be the credentials of a user on the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="1bbd5-184">O símbolo "\\`" no segundo comando é um símbolo de escape para o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-184">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="1bbd5-185">"\\`," significa que "," (uma vírgula) é uma parte do comando.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-185">“\\`,” means the “,” (comma character) is a part of the command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="1bbd5-186">Instalar o MPI e o OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="1bbd5-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="1bbd5-187">Para executar o OpenFOAM como um trabalho MPI na rede RDMA, você precisa compilar o OpenFOAM com as bibliotecas do Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-187">To run OpenFOAM as an MPI job on the RDMA network, you need to compile OpenFOAM with the Intel MPI libraries.</span></span> 

<span data-ttu-id="1bbd5-188">Primeiro, execute vários comandos **clusrun** para instalar as bibliotecas do Intel MPI (se ainda não estiverem instaladas) e o OpenFOAM nos seus nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-188">First, run several **clusrun** commands to install Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="1bbd5-189">Use o compartilhamento de nós principais configurado anteriormente para compartilhar os arquivos de instalação entre os nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-189">Use the head node share configured previously to share the installation files among the Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1bbd5-190">Essas etapas de instalação e compilação são exemplos.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="1bbd5-191">Você precisa de algum conhecimento de administração do sistema Linux para garantir a instalação correta dos compiladores dependentes e das bibliotecas.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-191">You need some knowledge of Linux system administration to ensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="1bbd5-192">Talvez você precise modificar determinadas variáveis de ambiente ou outras configurações para as versões do Intel MPI e do OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-192">You might need to modify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="1bbd5-193">Para obter detalhes, consulte [Guia de instalação do Intel MPI Library para Linux](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) e [Instalação do OpenFOAM Source Pack](http://openfoam.org/download/2-3-1-source/) para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="1bbd5-194">Instalar o Intel MPI</span><span class="sxs-lookup"><span data-stu-id="1bbd5-194">Install Intel MPI</span></span>
<span data-ttu-id="1bbd5-195">Salve o pacote de instalação baixado para o Intel MPI (l_mpi_p_5.0.3.048.tgz neste exemplo) em C:\OpenFoam no nó principal para que os nós do Linux possam acessar esse arquivo em /openfoam.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-195">Save the downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="1bbd5-196">Em seguida, execute **clusrun** para instalar a biblioteca do Intel MPI em todos os nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-196">Then run **clusrun** to install Intel MPI library on all the Linux nodes.</span></span>

1. <span data-ttu-id="1bbd5-197">Os comandos a seguir copiam o pacote de instalação e extrai-o para /opt/intel em cada nó.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-197">The following commands copy the installation package and extract it to /opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="1bbd5-198">Para instalar a Intel MPI Library silenciosamente, use um arquivo silent.cfg.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-198">To install Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="1bbd5-199">Você pode encontrar um exemplo nos arquivos de exemplo ao final deste artigo.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-199">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="1bbd5-200">Coloque esse arquivo na pasta compartilhada /openfoam.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-200">Place this file in the shared folder /openfoam.</span></span> <span data-ttu-id="1bbd5-201">Para obter detalhes sobre o arquivo silent.cfg, consulte [Intel MPI Library para o Guia de Instalação do Linux - Instalação Silenciosa](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span><span class="sxs-lookup"><span data-stu-id="1bbd5-201">For details about the silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="1bbd5-202">Salve o arquivo silent.cfg como um arquivo de texto com as terminações de linha do Linux (LF apenas, não CR LF).</span><span class="sxs-lookup"><span data-stu-id="1bbd5-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="1bbd5-203">Esta etapa garante que ele seja executado corretamente nos nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-203">This step ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="1bbd5-204">Instale a Intel MPI Library no modo silencioso.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="1bbd5-205">Configurar o MPI</span><span class="sxs-lookup"><span data-stu-id="1bbd5-205">Configure MPI</span></span>
<span data-ttu-id="1bbd5-206">Para testar, adicione as seguintes linhas a /etc/security/limits.conf em cada um dos nós do Linux:</span><span class="sxs-lookup"><span data-stu-id="1bbd5-206">For testing, you should add the following lines to the /etc/security/limits.conf on each of the Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="1bbd5-207">Depois de atualizar o arquivo limits.conf, reinicie os nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-207">Restart the Linux nodes after you update the limits.conf file.</span></span> <span data-ttu-id="1bbd5-208">Por exemplo, use o comando **clusrun** :</span><span class="sxs-lookup"><span data-stu-id="1bbd5-208">For example, use the following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="1bbd5-209">Depois de reiniciar, verifique se a pasta compartilhada está montada como /openfoam.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-209">After restarting, ensure that the shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="1bbd5-210">Compilar e instalar o OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="1bbd5-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="1bbd5-211">Salve o pacote de instalação baixado para o OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz neste exemplo) em C:\OpenFoam no nó principal para que os nós do Linux possam acessar esse arquivo em /openfoam.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-211">Save the downloaded installation package for the OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) to C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="1bbd5-212">Em seguida, execute comandos **clusrun** para compilar o OpenFOAM em todos os nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-212">Then run **clusrun** commands to compile OpenFOAM on all the Linux nodes.</span></span>

1. <span data-ttu-id="1bbd5-213">Crie uma pasta /opt/OpenFOAM em cada nó do Linux, copie o pacote de origem para essa pasta e extraia-o nesse local.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-213">Create a folder /opt/OpenFOAM on each Linux node, copy the source package to this folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="1bbd5-214">Para compilar o OpenFOAM com a Intel MPI Library, primeiro configure algumas variáveis de ambiente para o Intel MPI e o OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-214">To compile OpenFOAM with the Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="1bbd5-215">Use um script bash chamado settings.sh para definir as variáveis.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-215">Use a bash script called settings.sh to set the variables.</span></span> <span data-ttu-id="1bbd5-216">Você pode encontrar um exemplo nos arquivos de exemplo ao final deste artigo.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-216">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="1bbd5-217">Coloque esse arquivo (salvo com as terminações de linha do Linux) na pasta compartilhada /openfoam.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-217">Place this file (saved with Linux line endings) in the shared folder /openfoam.</span></span> <span data-ttu-id="1bbd5-218">Esse arquivo também contém configurações para os tempos de execução MPI e OpenFOAM que você usará posteriormente para executar um trabalho do OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-218">This file also contains settings for the MPI and OpenFOAM runtimes that you use later to run an OpenFOAM job.</span></span>
3. <span data-ttu-id="1bbd5-219">Instale os pacotes dependentes necessários para compilar o OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-219">Install dependent packages needed to compile OpenFOAM.</span></span> <span data-ttu-id="1bbd5-220">Dependendo de sua distribuição do Linux, você precisará primeiro adicionar um repositório.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-220">Depending on your Linux distribution, you might first need to add a repository.</span></span> <span data-ttu-id="1bbd5-221">Execute comandos **clusrun** semelhantes ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="1bbd5-221">Run **clusrun** commands similar to the following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="1bbd5-222">Se necessário, use SSH em cada nó do Linux para executar os comandos a fim de confirmar se são executados corretamente.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-222">If necessary, SSH to each Linux node to run the commands to confirm that they run properly.</span></span>
4. <span data-ttu-id="1bbd5-223">Execute o comando a seguir para compilar o OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-223">Run the following command to compile OpenFOAM.</span></span> <span data-ttu-id="1bbd5-224">O processo de compilação leva algum tempo para ser concluído e gera uma grande quantidade de informações de log na saída padrão. Portanto, use a opção **/interleaved** para exibir a saída intercalada.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-224">The compilation process takes some time to complete and generates a large amount of log information to standard output, so use the **/interleaved** option to display the output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="1bbd5-225">O símbolo "\\`" no comando é um símbolo de escape para o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-225">The “\\`” symbol in the command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="1bbd5-226">"\\`&" significa que o "&" é uma parte do comando.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-226">“\\`&” means the “&” is a part of the command.</span></span>
   > 
   > 

## <a name="prepare-to-run-an-openfoam-job"></a><span data-ttu-id="1bbd5-227">Preparar para executar um trabalho do OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="1bbd5-227">Prepare to run an OpenFOAM job</span></span>
<span data-ttu-id="1bbd5-228">Agora, prepare-se executar um trabalho MPI chamado sloshingTank3D, que é um dos exemplos de OpenFoam, em dois nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-228">Now get ready to run an MPI job called sloshingTank3D, which is one of the OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-the-runtime-environment"></a><span data-ttu-id="1bbd5-229">Configurar o ambiente do tempo de execução</span><span class="sxs-lookup"><span data-stu-id="1bbd5-229">Set up the runtime environment</span></span>
<span data-ttu-id="1bbd5-230">Para configurar os ambientes do tempo de execução para o MPI e o OpenFOAM em todos os nós do Linux, execute o seguinte comando em uma janela do Windows PowerShell no nó principal.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-230">To set up the runtime environments for MPI and OpenFOAM on the Linux nodes, run the following command in a Windows PowerShell window on the head node.</span></span> <span data-ttu-id="1bbd5-231">(Este comando é válido apenas para o Linux SUSE)</span><span class="sxs-lookup"><span data-stu-id="1bbd5-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="1bbd5-232">Preparar os dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="1bbd5-232">Prepare sample data</span></span>
<span data-ttu-id="1bbd5-233">Use o compartilhamento de nós principais configurado anteriormente para compartilhar os arquivos entre os nós do Linux (montados as /openfoam).</span><span class="sxs-lookup"><span data-stu-id="1bbd5-233">Use the head node share you configured previously to share files among the Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="1bbd5-234">SSH para um dos nós de computação do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-234">SSH to one of your Linux compute nodes.</span></span>
2. <span data-ttu-id="1bbd5-235">Execute o seguinte comando para configurar o ambiente do tempo de execução do OpenFOAM, se você ainda não fez isso.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-235">Run the following command to set up the OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="1bbd5-236">Copie o exemplo sloshingTank3D para a pasta compartilhada e navegue até ele.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-236">Copy the sloshingTank3D sample to the shared folder and navigate to it.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="1bbd5-237">Quando você usa os parâmetros padrão desse exemplo, pode levar vários minutos para ele ser executado, portanto, convém modificar alguns parâmetros para que ele seja executado mais rapidamente.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-237">When you use the default parameters of this sample, it can take tens of minutes to run, so you might want to modify some parameters to make it run faster.</span></span> <span data-ttu-id="1bbd5-238">Uma opção simples é modificar as variáveis da etapa de tempo deltaT e writeInterval no arquivo de sistema/controlDict.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-238">One simple choice is to modify the time step variables deltaT and writeInterval in the system/controlDict file.</span></span> <span data-ttu-id="1bbd5-239">Esse arquivo armazena todos os dados de entrada relacionados ao controle de tempo e leitura e gravação de dados da solução.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-239">This file stores all input data relating to the control of time and reading and writing solution data.</span></span> <span data-ttu-id="1bbd5-240">Por exemplo, você pode alterar o valor de deltaT de 0,05 para 0,5 e o valor de writeInterval de 0,05 para 0,5.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-240">For example, you could change the value of deltaT from 0.05 to 0.5 and the value of writeInterval from 0.05 to 0.5.</span></span>
   
   ![Modificar as variáveis da etapa][step_variables]
5. <span data-ttu-id="1bbd5-242">Especifique os valores desejados para as variáveis no arquivo system/decomposeParDict.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-242">Specify desired values for the variables in the system/decomposeParDict file.</span></span> <span data-ttu-id="1bbd5-243">Este exemplo usa dois nós do Linux, cada um com oito núcleos, portanto, defina numberOfSubdomains para 16 e n de hierarchicalCoeffs para (1 1 16), que significa executar o OpenFOAM em paralelo com 16 processos.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains to 16 and n of hierarchicalCoeffs to (1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="1bbd5-244">Para obter mais informações, consulte [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4)(Guia do usuário OpenFOAM: 3.4 Execução de aplicativos em paralelo).</span><span class="sxs-lookup"><span data-stu-id="1bbd5-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![Decompor processos][decompose]
6. <span data-ttu-id="1bbd5-246">Execute os seguintes comandos no diretório sloshingTank3D para preparar os dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-246">Run the following commands from the sloshingTank3D directory to prepare the sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="1bbd5-247">No nó principal, você deve ver que os arquivos de dados de exemplo são copiados para C:\OpenFoam\sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-247">On the head node, you should see the sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="1bbd5-248">(C:\OpenFoam é a pasta compartilhada no nó principal.)</span><span class="sxs-lookup"><span data-stu-id="1bbd5-248">(C:\OpenFoam is the shared folder on the head node.)</span></span>
   
   ![Arquivos de dados no nó principal][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="1bbd5-250">Arquivo de host para mpirun</span><span class="sxs-lookup"><span data-stu-id="1bbd5-250">Host file for mpirun</span></span>
<span data-ttu-id="1bbd5-251">Nesta etapa, crie um arquivo de host (uma lista de nós de computação) que o comando **mpirun** usa.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-251">In this step, you create a host file (a list of compute nodes) which the **mpirun** command uses.</span></span>

1. <span data-ttu-id="1bbd5-252">Em um dos nós do Linux, crie um arquivo chamado hostfile em /openfoam, para que esse arquivo possa ser obtido em /openfoam/hostfile em todos os nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-252">On one of the Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="1bbd5-253">Grave os nomes dos nós do Linux nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="1bbd5-254">Neste exemplo, o arquivo contém os seguintes nomes:</span><span class="sxs-lookup"><span data-stu-id="1bbd5-254">In this example, the file contains the following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="1bbd5-255">Você também pode criar esse arquivo em C:\OpenFoam\hostfile no nó principal.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-255">You can also create this file at C:\OpenFoam\hostfile on the head node.</span></span> <span data-ttu-id="1bbd5-256">Se você escolher esta opção, salve-o como um arquivo de texto com as terminações de linha do Linux (LF apenas, não CR LF).</span><span class="sxs-lookup"><span data-stu-id="1bbd5-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="1bbd5-257">Isso garante que ele seja executado corretamente nos nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-257">This ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="1bbd5-258">**Wrapper de script bash**</span><span class="sxs-lookup"><span data-stu-id="1bbd5-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="1bbd5-259">Se você tiver vários nós do Linux e desejar que seu trabalho seja executado somente em alguns deles, não será uma boa ideia usar um arquivo de host fixo porque você não sabe quais nós serão alocados para seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-259">If you have many Linux nodes and you want your job to run on only some of them, it’s not a good idea to use a fixed host file, because you don’t know which nodes will be allocated to your job.</span></span> <span data-ttu-id="1bbd5-260">Neste caso, escreva um wrapper de script bash para **mpirun** a fim de criar o arquivo de host automaticamente.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-260">In this case, write a bash script wrapper for **mpirun** to create the host file automatically.</span></span> <span data-ttu-id="1bbd5-261">Você pode encontrar um wrapper de script bash de exemplo chamado hpcimpirun.sh no final deste artigo e salvá-lo como /openfoam/hpcimpirun.sh.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-261">You can find an example bash script wrapper called hpcimpirun.sh at the end of this article, and save it as /openfoam/hpcimpirun.sh.</span></span> <span data-ttu-id="1bbd5-262">Esse script de exemplo faz o seguinte:</span><span class="sxs-lookup"><span data-stu-id="1bbd5-262">This example script does the following:</span></span>
   
   1. <span data-ttu-id="1bbd5-263">Define as variáveis de ambiente para **mpirun**e alguns parâmetros do comando de adição para executar o trabalho MPI por meio da rede RDMA.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-263">Sets up the environment variables for **mpirun**, and some addition command parameters to run the MPI job through the RDMA network.</span></span> <span data-ttu-id="1bbd5-264">Nesse caso, ele define as seguintes variáveis:</span><span class="sxs-lookup"><span data-stu-id="1bbd5-264">In this case, it sets the following variables:</span></span>
      
      * <span data-ttu-id="1bbd5-265">I_MPI_FABRICS=shm:dapl</span><span class="sxs-lookup"><span data-stu-id="1bbd5-265">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="1bbd5-266">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span><span class="sxs-lookup"><span data-stu-id="1bbd5-266">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="1bbd5-267">I_MPI_DYNAMIC_CONNECTION=0</span><span class="sxs-lookup"><span data-stu-id="1bbd5-267">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="1bbd5-268">Cria um arquivo de host de acordo com a variável de ambiente $CCP_NODES_CORES, que é definida pelo nó principal do HPC quando o trabalho é ativado.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-268">Creates a host file according to the environment variable $CCP_NODES_CORES, which is set by the HPC head node when the job is activated.</span></span>
      
      <span data-ttu-id="1bbd5-269">O formato $CCP_NODES_CORES segue este padrão:</span><span class="sxs-lookup"><span data-stu-id="1bbd5-269">The format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="1bbd5-270">onde</span><span class="sxs-lookup"><span data-stu-id="1bbd5-270">where</span></span>
      
      * <span data-ttu-id="1bbd5-271">`<Number of nodes>` : o número de nós alocados para esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-271">`<Number of nodes>` - the number of nodes allocated to this job.</span></span>  
      * <span data-ttu-id="1bbd5-272">`<Name of node_n_...>` : o nome de cada nó alocado para esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-272">`<Name of node_n_...>` - the name of each node allocated to this job.</span></span>
      * <span data-ttu-id="1bbd5-273">`<Cores of node_n_...>`: o número de núcleos no nó alocado para esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-273">`<Cores of node_n_...>` - the number of cores on the node allocated to this job.</span></span>
      
      <span data-ttu-id="1bbd5-274">Por exemplo, se o trabalho precisar de dois núcleos para ser executado, $CCP_NODES_CORES será semelhante a</span><span class="sxs-lookup"><span data-stu-id="1bbd5-274">For example, if the job needs two nodes to run, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="1bbd5-275">Chama o comando **mpirun** e acrescenta dois parâmetros à linha de comando.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-275">Calls the **mpirun** command and appends two parameters to the command line.</span></span>
      
      * <span data-ttu-id="1bbd5-276">`--hostfile <hostfilepath>: <hostfilepath>` - o caminho do arquivo de host que o script cria</span><span class="sxs-lookup"><span data-stu-id="1bbd5-276">`--hostfile <hostfilepath>: <hostfilepath>` - the path of the host file the script creates</span></span>
      * <span data-ttu-id="1bbd5-277">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - uma variável de ambiente definida pelo nó principal do HPC Pack, que armazena o número de núcleos totais alocados para esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-277">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by the HPC Pack head node, which stores the number of total cores allocated to this job.</span></span> <span data-ttu-id="1bbd5-278">Nesse caso, especifica o número de processos para **mpirun**.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-278">In this case, it specifies the number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="1bbd5-279">Enviar um trabalho do OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="1bbd5-279">Submit an OpenFOAM job</span></span>
<span data-ttu-id="1bbd5-280">Agora, você pode enviar um trabalho no Gerenciador de Cluster de HPC.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-280">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="1bbd5-281">Você precisa passar o script hpcimpirun.sh nas linhas de comando para algumas das tarefas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-281">You need to pass the script hpcimpirun.sh in the command lines for some of the job tasks.</span></span>

1. <span data-ttu-id="1bbd5-282">Conecte-se ao nó principal do cluster e inicie o Gerenciador de Cluster do HPC.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-282">Connect to your cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="1bbd5-283">Em **Gerenciamento de Recursos**, verifique se os nós de computação do Linux estão no estado **Online**.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-283">**In Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span></span> <span data-ttu-id="1bbd5-284">Se não estiverem, selecione-os e clique em **Colocar Online**.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-284">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="1bbd5-285">Em **Gerenciamento de Trabalhos**, clique em **Novo Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-285">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="1bbd5-286">Insira um nome para o trabalho, como *sloshingTank3D*.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-286">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![Detalhes do trabalho][job_details]
5. <span data-ttu-id="1bbd5-288">Em **Recursos de trabalho**, selecione o tipo de recurso como “Nó” e defina o Mínimo para 2.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-288">In **Job resources**, choose the type of resource as “Node” and set the Minimum to 2.</span></span> <span data-ttu-id="1bbd5-289">Essa configuração executa o trabalho em dois nós do Linux, cada um deles tem oito núcleos neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-289">This configuration runs the job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![Recursos de trabalho][job_resources]
6. <span data-ttu-id="1bbd5-291">Clique em **Editar Tarefas** na navegação esquerda e clique em **Adicionar** para adicionar uma tarefa ao trabalho.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-291">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span></span> <span data-ttu-id="1bbd5-292">Adicione quatro tarefas ao trabalho com as seguintes linhas de comando e configurações para as tarefas.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-292">Add four tasks to the job with the following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="1bbd5-293">A execução `source /openfoam/settings.sh` configura os ambientes do tempo de execução OpenFOAM e MPI para que cada uma das tarefas a seguir chame antes do comando OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-293">Running `source /openfoam/settings.sh` sets up the OpenFOAM and MPI runtime environments, so each of the following tasks calls it before the OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="1bbd5-294">**Tarefa 1**.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-294">**Task 1**.</span></span> <span data-ttu-id="1bbd5-295">Execute **decomposePar** para gerar arquivos de dados a fim de executar o **interDyMFoam** em paralelo.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-295">Run **decomposePar** to generate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="1bbd5-296">Atribuir um nó à tarefa</span><span class="sxs-lookup"><span data-stu-id="1bbd5-296">Assign one node to the task</span></span>
     * <span data-ttu-id="1bbd5-297">**Linha de comando** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="1bbd5-297">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="1bbd5-298">**Diretório de trabalho** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="1bbd5-298">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="1bbd5-299">Consulte a figura a seguir.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-299">See the following figure.</span></span> <span data-ttu-id="1bbd5-300">Você pode configurar as tarefas restantes da mesma forma.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-300">You configure the remaining tasks similarly.</span></span>
     
     ![Detalhes da tarefa 1][task_details1]
   * <span data-ttu-id="1bbd5-302">**Tarefa 2**.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-302">**Task 2**.</span></span> <span data-ttu-id="1bbd5-303">Execute **interDyMFoam** em paralelo para calcular o exemplo.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-303">Run **interDyMFoam** in parallel to compute the sample.</span></span>
     
     * <span data-ttu-id="1bbd5-304">Atribuir dois nós à tarefa</span><span class="sxs-lookup"><span data-stu-id="1bbd5-304">Assign two nodes to the task</span></span>
     * <span data-ttu-id="1bbd5-305">**Linha de comando** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="1bbd5-305">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="1bbd5-306">**Diretório de trabalho** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="1bbd5-306">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="1bbd5-307">**Tarefa 3**.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-307">**Task 3**.</span></span> <span data-ttu-id="1bbd5-308">Execute **reconstructPar** para mesclar os conjuntos de diretórios de tempo de cada diretório processor_N_ em um único conjunto.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-308">Run **reconstructPar** to merge the sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="1bbd5-309">Atribuir um nó à tarefa</span><span class="sxs-lookup"><span data-stu-id="1bbd5-309">Assign one node to the task</span></span>
     * <span data-ttu-id="1bbd5-310">**Linha de comando** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="1bbd5-310">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="1bbd5-311">**Diretório de trabalho** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="1bbd5-311">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="1bbd5-312">**Tarefa 4**.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-312">**Task 4**.</span></span> <span data-ttu-id="1bbd5-313">Execute **foamToEnsight** em paralelo para converter os arquivos de resultado do OpenFOAM no formato EnSight e colocar os arquivos EnSight em um diretório chamado Ensight no diretório de caso.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-313">Run **foamToEnsight** in parallel to convert the OpenFOAM result files into EnSight format and place the EnSight files in a directory named Ensight in the case directory.</span></span>
     
     * <span data-ttu-id="1bbd5-314">Atribuir dois nós à tarefa</span><span class="sxs-lookup"><span data-stu-id="1bbd5-314">Assign two nodes to the task</span></span>
     * <span data-ttu-id="1bbd5-315">**Linha de comando** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="1bbd5-315">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="1bbd5-316">**Diretório de trabalho** - /openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="1bbd5-316">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="1bbd5-317">Adicione dependências a essas tarefas na  ordem de tarefas crescente.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-317">Add dependencies to these tasks in ascending task order.</span></span>
   
   ![Dependências da tarefa][task_dependencies]
8. <span data-ttu-id="1bbd5-319">Clique em **Enviar** para executar este trabalho.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-319">Click **Submit** to run this job.</span></span>
   
   <span data-ttu-id="1bbd5-320">Por padrão, o HPC Pack envia o trabalho como a sua atual conta de usuário conectado.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-320">By default, HPC Pack submits the job as your current logged-on user account.</span></span> <span data-ttu-id="1bbd5-321">Depois de clicar em **Enviar**, uma caixa de diálogo pode solicitar que você insira o nome de usuário e a senha.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-321">After you click **Submit**, you might see a dialog box prompting you to enter the user name and password.</span></span>
   
   ![Credenciais de trabalho][creds]
   
   <span data-ttu-id="1bbd5-323">Em algumas condições, o HPC Pack memoriza as informações do usuário inseridas anteriormente e não mostra esta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-323">Under some conditions, HPC Pack remembers the user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="1bbd5-324">Para fazer o HPC Pack mostrar novamente, digite o seguinte comando em um prompt de comando e, então, envie o trabalho.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-324">To make HPC Pack show it again, enter the following command at a Command prompt and then submit the job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="1bbd5-325">O trabalho leva de alguns minutos a várias horas de acordo com os parâmetros que você definiu para o exemplo.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-325">The job takes from tens of minutes to several hours according to the parameters you have set for the sample.</span></span> <span data-ttu-id="1bbd5-326">No mapa de calor, você vê o trabalho em execução em dois nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-326">In the heat map, you see the job running on the Linux nodes.</span></span> 
   
   ![Mapa de calor][heat_map]
   
   <span data-ttu-id="1bbd5-328">Em cada nó, oito processos são iniciados.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-328">On each node, eight processes are started.</span></span>
   
   ![Processos do Linux][linux_processes]
10. <span data-ttu-id="1bbd5-330">Quando o trabalho for concluído, localize os resultados do trabalho nas pastas em C:\OpenFoam\sloshingTank3D e os arquivos de log em C:\OpenFoam.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-330">When the job finishes, find the job results in folders under C:\OpenFoam\sloshingTank3D, and the log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="1bbd5-331">Exibir resultados no EnSight</span><span class="sxs-lookup"><span data-stu-id="1bbd5-331">View results in EnSight</span></span>
<span data-ttu-id="1bbd5-332">Opcionalmente, use o [EnSight](https://www.ceisoftware.com/) para visualizar e analisar os resultados do trabalho do OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-332">Optionally use [EnSight](https://www.ceisoftware.com/) to visualize and analyze the results of the OpenFOAM job.</span></span> <span data-ttu-id="1bbd5-333">Para obter mais informações sobre a visualização e a animação no EnSight, consulte o [guia em vídeo](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span><span class="sxs-lookup"><span data-stu-id="1bbd5-333">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="1bbd5-334">Depois de instalar o EnSight no nó principal, inicie-o.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-334">After you install EnSight on the head node, start it.</span></span>
2. <span data-ttu-id="1bbd5-335">Abra o C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-335">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="1bbd5-336">Você verá um tanque no visualizador.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-336">You see a tank in the viewer.</span></span>
   
   ![Tanque no EnSight][tank]
3. <span data-ttu-id="1bbd5-338">Crie um **Isosurface** em **internalMesh**, em seguida, escolha a variável **alpha_water**.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-338">Create an **Isosurface** from **internalMesh**, and then choose the variable **alpha_water**.</span></span>
   
   ![Criar um isosurface][isosurface]
4. <span data-ttu-id="1bbd5-340">Defina a cor do **Isosurface_part** criado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-340">Set the color for **Isosurface_part** created in the previous step.</span></span> <span data-ttu-id="1bbd5-341">Por exemplo, defina-a para água azul.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-341">For example, set it to water blue.</span></span>
   
   ![Editar cor do isosurface][isosurface_color]
5. <span data-ttu-id="1bbd5-343">Crie um **volume Iso** em **paredes** selecionando **paredes** no painel **Partes** e clique no botão **Isosurfaces** na barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-343">Create an **Iso-volume** from **walls** by selecting **walls** in the **Parts** panel and click the **Isosurfaces** button in the toolbar.</span></span>
6. <span data-ttu-id="1bbd5-344">Na caixa de diálogo, selecione **Tipo** como **Isovolume** e defina o Mín. do **Intervalo Isovolume** para 0,5.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-344">In the dialog box, select **Type** as **Isovolume** and set the Min of **Isovolume range** to 0.5.</span></span> <span data-ttu-id="1bbd5-345">Para criar o isovolume, clique em **Criar com partes selecionadas**.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-345">To create the isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="1bbd5-346">Defina a cor de **Iso_volume_part** criado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-346">Set the color for **Iso_volume_part** created in the previous step.</span></span> <span data-ttu-id="1bbd5-347">Por exemplo, defina para água azul profundo.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-347">For example, set it to deep water blue.</span></span>
8. <span data-ttu-id="1bbd5-348">Defina a cor de **paredes**.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-348">Set the color for **walls**.</span></span> <span data-ttu-id="1bbd5-349">Por exemplo, defina para branco transparente.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-349">For example, set it to transparent white.</span></span>
9. <span data-ttu-id="1bbd5-350">Agora, clique em **Reproduzir** para ver os resultados da simulação.</span><span class="sxs-lookup"><span data-stu-id="1bbd5-350">Now click **Play** to see the results of the simulation.</span></span>
   
    ![Resultado do tanque][tank_result]

## <a name="sample-files"></a><span data-ttu-id="1bbd5-352">Arquivos de exemplo</span><span class="sxs-lookup"><span data-stu-id="1bbd5-352">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="1bbd5-353">Exemplo de arquivo de configuração XML para implantação de cluster pelo script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="1bbd5-353">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
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

### <a name="sample-credxml-file"></a><span data-ttu-id="1bbd5-354">Exemplo de arquivo cred.xml</span><span class="sxs-lookup"><span data-stu-id="1bbd5-354">Sample cred.xml file</span></span>
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
### <a name="sample-silentcfg-file-to-install-mpi"></a><span data-ttu-id="1bbd5-355">Arquivo silent.cfg de exemplo para instalar MPI</span><span class="sxs-lookup"><span data-stu-id="1bbd5-355">Sample silent.cfg file to install MPI</span></span>
```
# Patterns used to check silent configuration file
#
# anythingpat - any string
# filepat     - the file location pattern (/file/location/to/license.lic)
# lspat       - the license server address pattern (0123@hostname)
# snpat       - the serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components to install, valid values are: {ALL, DEFAULTS, anythingpat}
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

# Path to the cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes to enable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes to update ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="1bbd5-356">Script settings.sh de exemplo</span><span class="sxs-lookup"><span data-stu-id="1bbd5-356">Sample settings.sh script</span></span>
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


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="1bbd5-357">Script hpcimpirun.sh de exemplo</span><span class="sxs-lookup"><span data-stu-id="1bbd5-357">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# The path of this script
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
    # CCP_NODES_CORES is not found or is empty, just run the mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create the hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into the hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run the mpirun with hostfile arg
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
