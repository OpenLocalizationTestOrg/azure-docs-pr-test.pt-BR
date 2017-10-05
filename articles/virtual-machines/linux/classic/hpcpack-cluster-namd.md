---
title: NAMD com Microsoft HPC Pack em VMs do Linux | Microsoft Docs
description: "Implante um cluster do Microsoft HPC Pack no Azure e executar uma simulação do NAMD com charmrun em vários nós de computação do Linux."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: e31845f3d7aa08357b0e8a1b3b77d97302442ac3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a><span data-ttu-id="6fcf1-103">Executar o NAMD com o Microsoft HPC Pack em nós de computação do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="6fcf1-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>
<span data-ttu-id="6fcf1-104">Este artigo mostra uma maneira de executar uma carga de trabalho de computação de alto desempenho (HPC) do Linux em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-104">This article shows you one way to run a Linux high-performance computing (HPC) workload on Azure virtual machines.</span></span> <span data-ttu-id="6fcf1-105">Aqui, você configura um cluster do [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) no Azure com nós de computação Linux e executa uma simulação do [NAMD](http://www.ks.uiuc.edu/Research/namd/) para calcular e visualizar a estrutura de um sistema biomolecular grande.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation to calculate and visualize the structure of a large biomolecular system.</span></span>  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* <span data-ttu-id="6fcf1-106">O **NAMD** (para o programa Nanoscale Molecular Dynamics) é um pacote de dinâmica molecular paralela criado para a simulação de alto desempenho de sistemas biomoleculares grandes que contêm milhões de átomos.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up to millions of atoms.</span></span> <span data-ttu-id="6fcf1-107">Vírus, estruturas de célula e grande proteínas são exemplos desses sistemas.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-107">Examples of these systems include viruses, cell structures, and large proteins.</span></span> <span data-ttu-id="6fcf1-108">O NAMD é dimensionado para centenas de núcleos de simulações típicas e para mais de 500.000 núcleos para as simulações maiores.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-108">NAMD scales to hundreds of cores for typical simulations and to more than 500,000 cores for the largest simulations.</span></span>
* <span data-ttu-id="6fcf1-109">O **Microsoft HPC Pack** fornece recursos para executar aplicativos de HPC e paralelos em larga escala em clusters de computadores locais ou nas máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-109">**Microsoft HPC Pack** provides features to run large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span></span> <span data-ttu-id="6fcf1-110">Originalmente desenvolvido como uma solução para cargas de trabalho HPC, o HPC Pack agora permite a execução de aplicativos HPC Linux em VMs do nó de computação do Linux implantadas em um cluster do HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="6fcf1-111">Consulte [Introdução a nós de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md) para ver uma introdução.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span></span>

<span data-ttu-id="6fcf1-112">Para obter outras opções para executar cargas de trabalho HPC Linux no Azure, consulte [Recursos técnicos para computação em lote e de alto desempenho](../../../batch/batch-hpc-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="6fcf1-112">For other options to run Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6fcf1-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6fcf1-113">Prerequisites</span></span>
* <span data-ttu-id="6fcf1-114">**Cluster HPC Pack com nós de computação do Linux**: implante um cluster HPC Pack com nós de computação do Linux no Azure usando um [modelo do Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) ou um [script do Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="6fcf1-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="6fcf1-115">Consulte [Introdução a nós de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md) para encontrar os pré-requisitos e etapas de cada opção.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span></span> <span data-ttu-id="6fcf1-116">Se você escolher a opção de implantação de script do PowerShell, consulte o arquivo de configuração de exemplo nos arquivos de exemplo no final deste artigo.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-116">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span></span> <span data-ttu-id="6fcf1-117">Este arquivo configura um cluster de HPC Pack com base no Azure, que consiste em um nó principal do Windows Server 2012 R2 e quatro nós de computação grandes do CentOS 6.6.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span></span> <span data-ttu-id="6fcf1-118">Personalize este arquivo conforme a necessidade para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-118">Customize this file as needed for your environment.</span></span>
* <span data-ttu-id="6fcf1-119">**Arquivos do tutorial e software do NAMD** : baixe o software do NAMD para o Linux no site do [NAMD](http://www.ks.uiuc.edu/Research/namd/) (o registro é obrigatório).</span><span class="sxs-lookup"><span data-stu-id="6fcf1-119">**NAMD software and tutorial files** - Download NAMD software for Linux from the [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span></span> <span data-ttu-id="6fcf1-120">Este artigo se baseia na versão 2.10 do NAMD e usa o arquivamento do [Linux-x86_64 (64 bits Intel/AMD com Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310).</span><span class="sxs-lookup"><span data-stu-id="6fcf1-120">This article is based on NAMD version 2.10, and uses the [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span></span> <span data-ttu-id="6fcf1-121">Baixe também os [Arquivos do tutorial do NAMD](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span><span class="sxs-lookup"><span data-stu-id="6fcf1-121">Also download the [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span></span> <span data-ttu-id="6fcf1-122">Os downloads são arquivos .tar e você precisa de uma ferramenta do Windows para extrair os arquivos no nó principal do cluster.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-122">The downloads are .tar files, and you need a Windows tool to extract the files on the cluster head node.</span></span> <span data-ttu-id="6fcf1-123">Para extrair os arquivos, siga as instruções mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-123">To extract the files, follow the instructions later in this article.</span></span> 
* <span data-ttu-id="6fcf1-124">**VMD** (opcional) – Para ver os resultados do trabalho do NAMD, baixe e instale o programa de visualização molecular [VMD](http://www.ks.uiuc.edu/Research/vmd/) em um computador de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-124">**VMD** (optional) - To see the results of your NAMD job, download and install the molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span></span> <span data-ttu-id="6fcf1-125">A versão atual é 1.9.2.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-125">The current version is 1.9.2.</span></span> <span data-ttu-id="6fcf1-126">Visite o site de download do VMD para começar.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-126">See the VMD download site to get started.</span></span>  

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="6fcf1-127">Configurar a relação de confiança mútua entre os nós de computação</span><span class="sxs-lookup"><span data-stu-id="6fcf1-127">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="6fcf1-128">Executar um trabalho de nós cruzados em vários nós do Linux requer que os nós tenham uma relação de confiança entre si (por **rsh** ou **ssh**).</span><span class="sxs-lookup"><span data-stu-id="6fcf1-128">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="6fcf1-129">Quando você cria o cluster do HPC Pack com o script de implantação de IaaS do Microsoft HPC Pack, o script configura automaticamente uma relação de confiança mútua permanente para a conta de administrador que você especificar.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-129">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span></span> <span data-ttu-id="6fcf1-130">Para usuários que não sejam administradores criados no domínio do cluster, é necessário configurar uma relação de confiança mútua temporária entre os nós quando um trabalho é alocado para eles.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-130">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them.</span></span> <span data-ttu-id="6fcf1-131">Em seguida, destrua a relação depois que o trabalho for concluído.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-131">Then, destroy the relationship after the job is complete.</span></span> <span data-ttu-id="6fcf1-132">Para fazer isso para cada usuário, forneça um par de chaves RSA para o cluster usado pelo HPC Pack para estabelecer a relação de confiança.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-132">To do this for each user, provide an RSA key pair to the cluster which HPC Pack uses to establish the trust relationship.</span></span> <span data-ttu-id="6fcf1-133">Siga as instruções.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-133">Instructions follow.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="6fcf1-134">Gerar um par de chaves RSA</span><span class="sxs-lookup"><span data-stu-id="6fcf1-134">Generate an RSA key pair</span></span>
<span data-ttu-id="6fcf1-135">É fácil gerar um par de chaves RSA, que contém uma chave pública e uma chave privada, executando o comando **ssh-keygen** do Linux.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-135">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="6fcf1-136">Faça logon em um computador com Linux.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-136">Log on to a Linux computer.</span></span>
2. <span data-ttu-id="6fcf1-137">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="6fcf1-137">Run the following command:</span></span>
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="6fcf1-138">Pressione **Enter** para usar as configurações padrão até que o comando seja concluído.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-138">Press **Enter** to use the default settings until the command is completed.</span></span> <span data-ttu-id="6fcf1-139">Não insira uma frase secreta aqui. Quando for solicitada uma senha, basta pressionar **Enter**.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Gerar um par de chaves RSA][keygen]
3. <span data-ttu-id="6fcf1-141">Altere o diretório para o diretório ~/.ssh.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-141">Change directory to the ~/.ssh directory.</span></span> <span data-ttu-id="6fcf1-142">A chave privada é armazenada em id_rsa e a chave pública em id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-142">The private key is stored in id_rsa and the public key in id_rsa.pub.</span></span>
   
   ![Chaves públicas e privadas][keys]

### <a name="add-the-key-pair-to-the-hpc-pack-cluster"></a><span data-ttu-id="6fcf1-144">Adicionar o par de chaves ao cluster do HPC Pack</span><span class="sxs-lookup"><span data-stu-id="6fcf1-144">Add the key pair to the HPC Pack cluster</span></span>
1. <span data-ttu-id="6fcf1-145">[Conecte-se por meio da Área de Trabalho Remota](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) à VM do nó principal usando as credenciais de domínio fornecidas quando você implantou o cluster (por exemplo, hpc\clusteradmin).</span><span class="sxs-lookup"><span data-stu-id="6fcf1-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to the head node VM using the domain credentials you provided when you deployed the cluster (for example, hpc\clusteradmin).</span></span> <span data-ttu-id="6fcf1-146">Você gerencia o cluster do nó principal.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-146">You manage the cluster from the head node.</span></span>
2. <span data-ttu-id="6fcf1-147">Use os procedimentos padrão do Windows Server para criar uma conta de usuário de domínio no domínio do Active Directory do cluster.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-147">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span></span> <span data-ttu-id="6fcf1-148">Por exemplo, use o Usuário do Active Directory e a ferramenta Computers no nó principal.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-148">For example, use the Active Directory User and Computers tool on the head node.</span></span> <span data-ttu-id="6fcf1-149">Com os exemplos neste artigo, supomos que você criará um usuário de domínio chamado hpcuser no domínio hpclab (hpclab\hpcuser).</span><span class="sxs-lookup"><span data-stu-id="6fcf1-149">The examples in this article assume you create a domain user named hpcuser in the hpclab domain (hpclab\hpcuser).</span></span>
3. <span data-ttu-id="6fcf1-150">Adicione o usuário do domínio ao cluster HPC Pack como um usuário do cluster.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-150">Add the domain user to the HPC Pack cluster as a cluster user.</span></span> <span data-ttu-id="6fcf1-151">Para obter instruções, consulte [Adicionar ou remover usuários de cluster](https://technet.microsoft.com/library/ff919330.aspx).</span><span class="sxs-lookup"><span data-stu-id="6fcf1-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span></span>
4. <span data-ttu-id="6fcf1-152">Crie um arquivo chamado C:\cred.xml e copie os dados da chave RSA nele.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-152">Create a file named C:\cred.xml and copy the RSA key data into it.</span></span> <span data-ttu-id="6fcf1-153">Você pode encontrar um exemplo nos arquivos de exemplo ao final deste artigo.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-153">You can find an example in the sample files at the end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy the contents of private key here</PrivateKey>
     <PublicKey>Copy the contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. <span data-ttu-id="6fcf1-154">Abra um Prompt de Comando e digite o seguinte comando para definir os dados de credenciais para a conta de hpclab\hpcuser.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-154">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span></span> <span data-ttu-id="6fcf1-155">Use o parâmetro **extendeddata** para transmitir o nome do arquivo C:\cred.xml que você criou para os dados da chave.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-155">You use the **extendeddata** parameter to pass the name of the C:\cred.xml file you created for the key data.</span></span>
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="6fcf1-156">Esse comando é concluído com êxito sem resultados.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-156">This command completes successfully without output.</span></span> <span data-ttu-id="6fcf1-157">Depois de definir as credenciais para as contas de usuário, você precisa executar os trabalhos, armazenar o arquivo cred.xml em um local seguro ou excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-157">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span></span>
6. <span data-ttu-id="6fcf1-158">Se você gerou o par de chaves RSA em um dos nós do Linux, lembre-se de excluir as chaves após terminar de usá-las.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-158">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span></span> <span data-ttu-id="6fcf1-159">O HPC Pack não define a relação de confiança mútua se ele encontrar um arquivo id_rsa ou id_rsa.pub existente.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6fcf1-160">Não recomendamos executar um trabalho do Linux como um administrador de cluster em um cluster compartilhado, já que um trabalho enviado por um administrador é executado na conta raiz nos nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span></span> <span data-ttu-id="6fcf1-161">Um trabalho enviado por um usuário não administrador é executado sob uma conta de usuário local do Linux com o mesmo nome que o usuário do trabalho.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-161">A job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span></span> <span data-ttu-id="6fcf1-162">Nesse caso, o HPC Pack define a relação de confiança mútua para este usuário Linux em todos os nós alocados para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-162">In this case, HPC Pack sets up mutual trust for this Linux user across all the nodes allocated to the job.</span></span> <span data-ttu-id="6fcf1-163">Você pode configurar o usuário do Linux manualmente nos nós do Linux antes de executar o trabalho, ou o HPC Pack criará o usuário automaticamente quando o trabalho for enviado.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-163">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span></span> <span data-ttu-id="6fcf1-164">Se o HPC Pack criar o usuário, ele o excluirá depois que o trabalho for concluído.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-164">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span></span> <span data-ttu-id="6fcf1-165">Para reduzir a ameaça à segurança, as chaves são removidas após a conclusão do trabalho em nós.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-165">To reduce security threat, the keys are removed after the job completes on the nodes.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="6fcf1-166">Configurar um compartilhamento de arquivos para nós do Linux</span><span class="sxs-lookup"><span data-stu-id="6fcf1-166">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="6fcf1-167">Agora, configure um compartilhamento de arquivo SMB e monte a pasta compartilhada em todos os nós do Linux para permitir que os nós do Linux acessem os arquivos NAMD com um caminho comum.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-167">Now set up an SMB file share, and mount the shared folder on all Linux nodes to allow the Linux nodes to access NAMD files with a common path.</span></span> <span data-ttu-id="6fcf1-168">A seguir, as etapas para montar uma pasta compartilhada no nó principal.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-168">Following are steps to mount a shared folder on the head node.</span></span> <span data-ttu-id="6fcf1-169">Um compartilhamento é recomendado para distribuições, como CentOS 6.6, que atualmente não têm suporte para o serviço de Arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support the Azure File service.</span></span> <span data-ttu-id="6fcf1-170">Se os nós do Linux derem suporte a compartilhamento de Arquivo do Azure, confira [Como usar o armazenamento de Arquivos do Azure com Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6fcf1-170">If your Linux nodes support an Azure File share, see [How to use Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="6fcf1-171">Para opções de compartilhamento de arquivos adicionais com o HPC Pack, e as etapas em [Introdução aos nós de computação do Linux em um cluster do HPC Pack no Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6fcf1-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="6fcf1-172">Crie uma pasta no nó principal e compartilhe-a com todos, configurando privilégios de leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-172">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span></span> <span data-ttu-id="6fcf1-173">Neste exemplo, \\\\CentOS66HN\Namd é o nome da pasta, em que CentOS66HN é o nome de host do nó principal.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-173">In this example, \\\\CentOS66HN\Namd is the name of the folder, where CentOS66HN is the host name of the head node.</span></span>
2. <span data-ttu-id="6fcf1-174">Crie uma subpasta chamada namd2 na pasta compartilhada.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-174">Create a subfolder named namd2 in the shared folder.</span></span> <span data-ttu-id="6fcf1-175">No namd2, crie outra subpasta chamada namdsample.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-175">In namd2, create another subfolder named namdsample.</span></span>
3. <span data-ttu-id="6fcf1-176">Extraia os arquivos do NAMD na pasta usando uma versão do Windows de **tar** ou outro utilitário do Windows que funciona em arquivos .tar.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-176">Extract the NAMD files in the folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span></span> 
   
   * <span data-ttu-id="6fcf1-177">Extraia o arquivo tar do NAMD para \\\\CentOS66HN\Namd\namd2.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-177">Extract the NAMD tar archive to \\\\CentOS66HN\Namd\namd2.</span></span>
   * <span data-ttu-id="6fcf1-178">Extraia os arquivos do tutorial em \\\\CentOS66HN\Namd\namd2\namdsample.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-178">Extract the tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span></span>
4. <span data-ttu-id="6fcf1-179">Abra uma janela do Windows PowerShell e execute os seguintes comandos para montar a pasta compartilhada nos nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-179">Open a Windows PowerShell window and run the following commands to mount the shared folder on the Linux nodes.</span></span>
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="6fcf1-180">O primeiro comando cria uma pasta chamada /namd2 em todos os nós do grupo LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-180">The first command creates a folder named /namd2 on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="6fcf1-181">O segundo comando monta a pasta compartilhada //CentOS66HN/Namd/namd2 para a pasta com os bits de dir_mode e file_mode definidos como 777.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-181">The second command mounts the shared folder //CentOS66HN/Namd/namd2 onto the folder with dir_mode and file_mode bits set to 777.</span></span> <span data-ttu-id="6fcf1-182">O *nome de usuário* e a *senha* no comando devem ser as credenciais de um usuário no nó principal.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-182">The *username* and *password* in the command should be the credentials of a user on the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="6fcf1-183">O símbolo "\\`" no segundo comando é um símbolo de escape para o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-183">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="6fcf1-184">"\\`," significa que "," (uma vírgula) é uma parte do comando.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-184">“\\`,” means the “,” (comma character) is a part of the command.</span></span>
> 
> 

## <a name="create-a-bash-script-to-run-a-namd-job"></a><span data-ttu-id="6fcf1-185">Criar um script Bash para executar um trabalho NAMD</span><span class="sxs-lookup"><span data-stu-id="6fcf1-185">Create a Bash script to run a NAMD job</span></span>
<span data-ttu-id="6fcf1-186">Seu trabalho NAMD requer um arquivo *nodelist* para **charmrun** a fim de determinar o número de nós a ser usado ao iniciar processos do NAMD.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-186">Your NAMD job needs a *nodelist* file for **charmrun** to determine the number of nodes to use when starting NAMD processes.</span></span> <span data-ttu-id="6fcf1-187">Você usa um script Bash que gera o arquivo nodelist e executa **charmrun** com esse arquivo nodelist.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-187">You use a Bash script that generates the nodelist file and runs **charmrun** with this nodelist file.</span></span> <span data-ttu-id="6fcf1-188">Depois, você pode enviar um trabalho do NAMD no Gerenciador de Cluster do HPC que chama esse script.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span></span>

<span data-ttu-id="6fcf1-189">Usando um editor de texto de sua escolha, crie o script Bash na pasta /namd2 que contém os arquivos do programa NAMD e nomeie-o hpccharmrun.sh. Para uma rápida prova de conceito, copie o script hpccharmrun.sh de exemplo no final deste artigo e vá para [Enviar um trabalho do NAMD](#submit-a-namd-job).</span><span class="sxs-lookup"><span data-stu-id="6fcf1-189">Using a text editor of your choice, create a Bash script in the /namd2 folder containing the NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy the example hpccharmrun.sh script provided at the end of this article and go to [Submit a NAMD job](#submit-a-namd-job).</span></span>

> [!TIP]
> <span data-ttu-id="6fcf1-190">Salve o script como um arquivo de texto com as terminações de linha do Linux (somente LF, não CR LF).</span><span class="sxs-lookup"><span data-stu-id="6fcf1-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="6fcf1-191">Isso garante que ele seja executado corretamente nos nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-191">This ensures that it runs properly on the Linux nodes.</span></span>
> 
> 

<span data-ttu-id="6fcf1-192">Veja a seguir os detalhes sobre a função desse script bash.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-192">Following are details about what this bash script does.</span></span> 

1. <span data-ttu-id="6fcf1-193">Defina algumas variáveis.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-193">Define some variables.</span></span>
   
   ```bash
   #!/bin/bash
   
   # The path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. <span data-ttu-id="6fcf1-194">Obtenha informações sobre o nó das variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-194">Get node information from the environment variables.</span></span> <span data-ttu-id="6fcf1-195">$NODESCORES armazena uma lista de palavras de divisão de $CCP_NODES_CORES.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span></span> <span data-ttu-id="6fcf1-196">$COUNT é o tamanho de $NODESCORES.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-196">$COUNT is the size of $NODESCORES.</span></span>
   
   ```
   # Get node information from the environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   <span data-ttu-id="6fcf1-197">O formato para a variável $CCP_NODES_CORES é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6fcf1-197">The format for the $CCP_NODES_CORES variable is as follows:</span></span>
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   <span data-ttu-id="6fcf1-198">Essa variável lista o número total de nós, os nomes dos nós e o número de núcleos em cada nó que estão alocados para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-198">This variable lists the total number of nodes, node names, and number of cores on each node that are allocated to the job.</span></span> <span data-ttu-id="6fcf1-199">Por exemplo, se o trabalho precisar de 10 núcleos para ser executado, o valor de $CCP_NODES_CORES será semelhante a:</span><span class="sxs-lookup"><span data-stu-id="6fcf1-199">For example, if the job needs 10 cores to run, the value of $CCP_NODES_CORES is similar to:</span></span>
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. <span data-ttu-id="6fcf1-200">Se a variável $CCP_NODES_CORES não estiver definida, inicie **charmrun** diretamente.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-200">If the $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span></span> <span data-ttu-id="6fcf1-201">(Isso só deve ocorrer quando você executa esse script diretamente nos nós do Linux.)</span><span class="sxs-lookup"><span data-stu-id="6fcf1-201">(This should only occur when you run this script directly on your Linux nodes.)</span></span>
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. <span data-ttu-id="6fcf1-202">Outra opção é criar um arquivo nodelist para **charmrun**.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-202">Or create a nodelist file for **charmrun**.</span></span>
   
   ```
   else
     # Create the nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write the head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into the nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. <span data-ttu-id="6fcf1-203">Execute **charmrun** com o arquivo nodelist, obtenha seu status de retorno e remova o arquivo nodelist ao final.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-203">Run **charmrun** with the nodelist file, get its return status, and remove the nodelist file at the end.</span></span>
   
   <span data-ttu-id="6fcf1-204">${CCP_NUMCPUS} é outra variável de ambiente definida pelo nó principal do HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-204">${CCP_NUMCPUS} is another environment variable set by the HPC Pack head node.</span></span> <span data-ttu-id="6fcf1-205">Ela armazena o número total de núcleos alocados para esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-205">It stores the number of total cores allocated to this job.</span></span> <span data-ttu-id="6fcf1-206">Usamos essa variável para especificar o número de processos para charmrun.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-206">We use it to specify the number of processes for charmrun.</span></span>
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. <span data-ttu-id="6fcf1-207">Saia com o status de retorno de **charmrun** .</span><span class="sxs-lookup"><span data-stu-id="6fcf1-207">Exit with the **charmrun** return status.</span></span>
   
   ```
   exit ${RTNSTS}
   ```

<span data-ttu-id="6fcf1-208">Veja abaixo as informações no arquivo nodelist, que são geradas pelo script:</span><span class="sxs-lookup"><span data-stu-id="6fcf1-208">Following is the information in the nodelist file, which the script generates:</span></span>

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

<span data-ttu-id="6fcf1-209">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6fcf1-209">For example:</span></span>

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a><span data-ttu-id="6fcf1-210">Enviar um trabalho NAMD</span><span class="sxs-lookup"><span data-stu-id="6fcf1-210">Submit a NAMD job</span></span>
<span data-ttu-id="6fcf1-211">Agora você está pronto para enviar um trabalho do NAMD no Gerenciador de Cluster do HPC.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-211">Now you are ready to submit a NAMD job in HPC Cluster Manager.</span></span>

1. <span data-ttu-id="6fcf1-212">Conecte-se ao nó principal do cluster e inicie o Gerenciador de Cluster do HPC.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-212">Connect to your cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="6fcf1-213">Em **Gerenciamento de Recursos**, verifique se os nós de computação do Linux estão no estado **Online**.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-213">In **Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span></span> <span data-ttu-id="6fcf1-214">Se não estiverem, selecione-os e clique em **Colocar Online**.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-214">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="6fcf1-215">Em **Gerenciamento de Trabalhos**, clique em **Novo Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-215">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="6fcf1-216">Insira um nome para o trabalho como *hpccharmrun*.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-216">Enter a name for job such as *hpccharmrun*.</span></span>
   
   ![Novo trabalho do HPC][namd_job]
5. <span data-ttu-id="6fcf1-218">Na página **Detalhes do Trabalho** em **Recursos de Trabalho**, selecione o tipo de recurso como **Nó** e defina o **Mínimo** para 3.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-218">On the **Job Details** page, under **Job Resources**, select the type of resource as **Node** and set the **Minimum** to 3.</span></span> <span data-ttu-id="6fcf1-219">, executamos o trabalho em três nós do Linux e cada nó tem quatro núcleos.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-219">, we run the job on three Linux nodes and each node has four cores.</span></span>
   
   ![Recursos de trabalho][job_resources]
6. <span data-ttu-id="6fcf1-221">Clique em **Editar Tarefas** na navegação esquerda e clique em **Adicionar** para adicionar uma tarefa ao trabalho.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-221">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span></span>    
7. <span data-ttu-id="6fcf1-222">Na página **Detalhes da Tarefa e Redirecionamento de E/S**, defina os valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="6fcf1-222">On the **Task Details and I/O Redirection** page, set the following values:</span></span>
   
   * <span data-ttu-id="6fcf1-223">**Linha de comando** -
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span><span class="sxs-lookup"><span data-stu-id="6fcf1-223">**Command line** -
`/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span></span>
     
     > [!TIP]
     > <span data-ttu-id="6fcf1-224">A linha de comando anterior é um único comando sem quebras de linha.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-224">The preceding command line is a single command without line breaks.</span></span> <span data-ttu-id="6fcf1-225">Ele é encapsulado para aparecer em várias linhas em **Linha de comando**.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-225">It wraps to appear on several lines under **Command line**.</span></span>
     > 
     > 
   * <span data-ttu-id="6fcf1-226">**Diretório de trabalho** - /namd2</span><span class="sxs-lookup"><span data-stu-id="6fcf1-226">**Working directory** - /namd2</span></span>
   * <span data-ttu-id="6fcf1-227">**Mínimo** - 3</span><span class="sxs-lookup"><span data-stu-id="6fcf1-227">**Minimum** - 3</span></span>
     
     ![Detalhes de tarefa][task_details]
     
     > [!NOTE]
     > <span data-ttu-id="6fcf1-229">Defina o diretório de trabalho aqui, pois **charmrun** tentará navegar até o mesmo diretório de trabalho em cada nó.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-229">You set the working directory here because **charmrun** tries to navigate to the same working directory on each node.</span></span> <span data-ttu-id="6fcf1-230">Se o diretório de trabalho não for definido, o HPC Pack iniciará o comando em uma pasta nomeada aleatoriamente, criada em um dos nós do Linux.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-230">If the working directory isn't set, HPC Pack starts the command in a randomly named folder created on one of the Linux nodes.</span></span> <span data-ttu-id="6fcf1-231">Isso causa o seguinte erro nos outros nós: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` Para evitar esse problema, especifique um caminho de pasta que possa ser acessado por todos os nós como o diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-231">This causes the following error on the other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` To avoid this problem, specify a folder path that can be accessed by all nodes as the working directory.</span></span>
     > 
     > 
8. <span data-ttu-id="6fcf1-232">Clique em **OK** e depois em **Enviar** para executar este trabalho.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-232">Click **OK** and then click **Submit** to run this job.</span></span>
   
   <span data-ttu-id="6fcf1-233">Por padrão, o HPC Pack envia o trabalho como a sua atual conta de usuário conectado.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-233">By default, HPC Pack submits the job as your current logged-on user account.</span></span> <span data-ttu-id="6fcf1-234">Uma caixa de diálogo pode solicitar que você insira o nome de usuário e a senha depois de clicar em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-234">A dialog box might prompt you to enter the user name and password after you click **Submit**.</span></span>
   
   ![Credenciais de trabalho][creds]
   
   <span data-ttu-id="6fcf1-236">Em algumas condições, o HPC Pack memoriza as informações do usuário inseridas anteriormente e não mostra esta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-236">Under some conditions, HPC Pack remembers the user information you input before and doesn't show this dialog box.</span></span> <span data-ttu-id="6fcf1-237">Para fazer o HPC Pack mostrá-la novamente, digite o seguinte comando em um Prompt de Comando e, então, envie o trabalho.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-237">To make HPC Pack show it again, enter the following command at a Command Prompt and then submit the job.</span></span>
   
   ```command
   hpccred delcreds
   ```
9. <span data-ttu-id="6fcf1-238">O trabalho leva vários minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-238">The job takes several minutes to finish.</span></span>
10. <span data-ttu-id="6fcf1-239">Encontre o log do trabalho em \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log e os arquivos de saída em \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-239">Find the job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and the output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span></span>
11. <span data-ttu-id="6fcf1-240">Opcionalmente, inicie o VMD para exibir os resultados do trabalho.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-240">Optionally, start VMD to view your job results.</span></span> <span data-ttu-id="6fcf1-241">As etapas para visualizar os arquivos de saída do NAMD (neste caso, uma molécula da proteína ubiquitina em uma esfera de água) estão além do escopo deste artigo.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-241">The steps for visualizing the NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond the scope of this article.</span></span> <span data-ttu-id="6fcf1-242">Veja [Tutorial do NAMD](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="6fcf1-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span></span>
    
    ![Resultados de trabalho][vmd_view]

## <a name="sample-files"></a><span data-ttu-id="6fcf1-244">Arquivos de exemplo</span><span class="sxs-lookup"><span data-stu-id="6fcf1-244">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="6fcf1-245">Exemplo de arquivo de configuração XML para implantação de cluster pelo script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="6fcf1-245">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>    
```

### <a name="sample-credxml-file"></a><span data-ttu-id="6fcf1-246">Exemplo de arquivo cred.xml</span><span class="sxs-lookup"><span data-stu-id="6fcf1-246">Sample cred.xml file</span></span>
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

### <a name="sample-hpccharmrunsh-script"></a><span data-ttu-id="6fcf1-247">Exemplo de script hpccharmrun.sh</span><span class="sxs-lookup"><span data-stu-id="6fcf1-247">Sample hpccharmrun.sh script</span></span>
```
#!/bin/bash

# The path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run the charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create the nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write the head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into the nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run the charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png
