---
title: aaaNAMD com Microsoft HPC Pack em VMs do Linux | Microsoft Docs
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
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a><span data-ttu-id="ff56e-103">Executar o NAMD com o Microsoft HPC Pack em nós de computação do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="ff56e-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>
<span data-ttu-id="ff56e-104">Este artigo mostra uma maneira toorun uma carga de trabalho de computação de alto desempenho (HPC) do Linux em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff56e-104">This article shows you one way toorun a Linux high-performance computing (HPC) workload on Azure virtual machines.</span></span> <span data-ttu-id="ff56e-105">Aqui, você configurar um [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) de cluster no Azure conosco de computação do Linux e executar um [NAMD](http://www.ks.uiuc.edu/Research/namd/) toocalculate de simulação e visualizar a estrutura de saudação de um sistema biomolecular grandes.</span><span class="sxs-lookup"><span data-stu-id="ff56e-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation toocalculate and visualize hello structure of a large biomolecular system.</span></span>  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* <span data-ttu-id="ff56e-106">**NAMD** (para o programa do Dynamics moleculares Nanoscale) é um pacote paralelo dynamics moleculares destinado a simulação de alto desempenho dos sistemas de grande biomolecular que contém o toomillions de átomos.</span><span class="sxs-lookup"><span data-stu-id="ff56e-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up toomillions of atoms.</span></span> <span data-ttu-id="ff56e-107">Vírus, estruturas de célula e grande proteínas são exemplos desses sistemas.</span><span class="sxs-lookup"><span data-stu-id="ff56e-107">Examples of these systems include viruses, cell structures, and large proteins.</span></span> <span data-ttu-id="ff56e-108">NAMD dimensiona toohundreds de núcleos de simulações típicas e toomore de 500.000 núcleos para simulações maior hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-108">NAMD scales toohundreds of cores for typical simulations and toomore than 500,000 cores for hello largest simulations.</span></span>
* <span data-ttu-id="ff56e-109">**Microsoft HPC Pack** fornece recursos toorun HPC em larga escala e aplicativos paralelos em clusters de computadores locais ou máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="ff56e-109">**Microsoft HPC Pack** provides features toorun large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span></span> <span data-ttu-id="ff56e-110">Originalmente desenvolvido como uma solução para cargas de trabalho HPC, o HPC Pack agora permite a execução de aplicativos HPC Linux em VMs do nó de computação do Linux implantadas em um cluster do HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="ff56e-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="ff56e-111">Consulte [Introdução a nós de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md) para ver uma introdução.</span><span class="sxs-lookup"><span data-stu-id="ff56e-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span></span>

<span data-ttu-id="ff56e-112">Para outra opções toorun Linux HPC cargas de trabalho no Azure, consulte [recursos técnicos para o lote e computação de alto desempenho](../../../batch/batch-hpc-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ff56e-112">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff56e-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ff56e-113">Prerequisites</span></span>
* <span data-ttu-id="ff56e-114">**Cluster HPC Pack com nós de computação do Linux**: implante um cluster HPC Pack com nós de computação do Linux no Azure usando um [modelo do Azure Resource Manager](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) ou um [script do Azure PowerShell](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="ff56e-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="ff56e-115">Consulte [começar conosco de computação Linux em um cluster de HPC Pack no Azure](hpcpack-cluster.md) para pré-requisitos hello e as etapas para qualquer uma das opções.</span><span class="sxs-lookup"><span data-stu-id="ff56e-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="ff56e-116">Se você escolher Olá opção de implantação de script do PowerShell, consulte o arquivo de configuração de exemplo hello nos arquivos de exemplo hello final Olá deste artigo.</span><span class="sxs-lookup"><span data-stu-id="ff56e-116">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="ff56e-117">Este arquivo configura um cluster de HPC Pack com base no Azure, que consiste em um nó principal do Windows Server 2012 R2 e quatro nós de computação grandes do CentOS 6.6.</span><span class="sxs-lookup"><span data-stu-id="ff56e-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span></span> <span data-ttu-id="ff56e-118">Personalize este arquivo conforme a necessidade para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="ff56e-118">Customize this file as needed for your environment.</span></span>
* <span data-ttu-id="ff56e-119">**Arquivos de software e um tutorial NAMD** -software baixar NAMD para Linux Olá [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registro necessário).</span><span class="sxs-lookup"><span data-stu-id="ff56e-119">**NAMD software and tutorial files** - Download NAMD software for Linux from hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span></span> <span data-ttu-id="ff56e-120">Este artigo se baseia em NAMD versão 2.10 e usa Olá [Linux-x86_64 (64 bits Intel/AMD com Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) arquivamento.</span><span class="sxs-lookup"><span data-stu-id="ff56e-120">This article is based on NAMD version 2.10, and uses hello [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span></span> <span data-ttu-id="ff56e-121">Também baixar Olá [arquivos tutoriais NAMD](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span><span class="sxs-lookup"><span data-stu-id="ff56e-121">Also download hello [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span></span> <span data-ttu-id="ff56e-122">Olá downloads são arquivos. tar, e você precisa de um arquivos de saudação Windows ferramenta tooextract no nó principal do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-122">hello downloads are .tar files, and you need a Windows tool tooextract hello files on hello cluster head node.</span></span> <span data-ttu-id="ff56e-123">arquivos de saudação tooextract, siga as instruções de saudação neste artigo.</span><span class="sxs-lookup"><span data-stu-id="ff56e-123">tooextract hello files, follow hello instructions later in this article.</span></span> 
* <span data-ttu-id="ff56e-124">**VMD** (opcional) - toosee resultados de saudação do seu trabalho NAMD, baixar e instalar o programa de visualização moleculares Olá [VMD](http://www.ks.uiuc.edu/Research/vmd/) em um computador de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="ff56e-124">**VMD** (optional) - toosee hello results of your NAMD job, download and install hello molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span></span> <span data-ttu-id="ff56e-125">versão atual do Hello é 1.9.2.</span><span class="sxs-lookup"><span data-stu-id="ff56e-125">hello current version is 1.9.2.</span></span> <span data-ttu-id="ff56e-126">Consulte Olá VMD baixar tooget site iniciado.</span><span class="sxs-lookup"><span data-stu-id="ff56e-126">See hello VMD download site tooget started.</span></span>  

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="ff56e-127">Configurar a relação de confiança mútua entre os nós de computação</span><span class="sxs-lookup"><span data-stu-id="ff56e-127">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="ff56e-128">Executar um trabalho de nó cruzado em vários nós do Linux requer Olá nós tootrust entre si (por **rsh** ou **ssh**).</span><span class="sxs-lookup"><span data-stu-id="ff56e-128">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="ff56e-129">Quando você cria o cluster de HPC Pack Olá com hello script de implantação do Microsoft HPC Pack IaaS, o script hello configura automaticamente confiança mútua permanente da conta de administrador Olá que você especificar.</span><span class="sxs-lookup"><span data-stu-id="ff56e-129">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="ff56e-130">Para usuários não-administrador que criar no domínio do cluster hello, você tem tooset a relação de confiança mútua temporária entre nós hello quando um trabalho é alocado toothem.</span><span class="sxs-lookup"><span data-stu-id="ff56e-130">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem.</span></span> <span data-ttu-id="ff56e-131">Em seguida, destrua relação Olá após a conclusão do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff56e-131">Then, destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="ff56e-132">toodo isso para cada usuário, fornecer um cluster de toohello do par de chaves RSA quais HPC Pack usa a relação de confiança tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-132">toodo this for each user, provide an RSA key pair toohello cluster which HPC Pack uses tooestablish hello trust relationship.</span></span> <span data-ttu-id="ff56e-133">Siga as instruções.</span><span class="sxs-lookup"><span data-stu-id="ff56e-133">Instructions follow.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="ff56e-134">Gerar um par de chaves RSA</span><span class="sxs-lookup"><span data-stu-id="ff56e-134">Generate an RSA key pair</span></span>
<span data-ttu-id="ff56e-135">É fácil toogenerate um par de chaves RSA, que contém uma chave pública e uma chave privada, executando Olá Linux **ssh-keygen** comando.</span><span class="sxs-lookup"><span data-stu-id="ff56e-135">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="ff56e-136">Faça logon no tooa computador Linux.</span><span class="sxs-lookup"><span data-stu-id="ff56e-136">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="ff56e-137">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff56e-137">Run hello following command:</span></span>
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="ff56e-138">Pressione **Enter** toouse Olá configurações até que o comando Olá é concluído.</span><span class="sxs-lookup"><span data-stu-id="ff56e-138">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="ff56e-139">Não insira uma frase secreta aqui. Quando for solicitada uma senha, basta pressionar **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ff56e-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Gerar um par de chaves RSA][keygen]
3. <span data-ttu-id="ff56e-141">Altere o diretório de ~/.ssh toohello do diretório.</span><span class="sxs-lookup"><span data-stu-id="ff56e-141">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="ff56e-142">chave privada Olá é armazenado na chave pública id_rsa e hello em id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="ff56e-142">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![Chaves públicas e privadas][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="ff56e-144">Adicionar um cluster de HPC Pack em toohello Olá par de chaves</span><span class="sxs-lookup"><span data-stu-id="ff56e-144">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="ff56e-145">[Conecte-se pela área de trabalho remota](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) VM usando o nó principal toohello Olá credenciais de domínio que você forneceu quando você implantou o cluster hello (por exemplo, hpc\clusteradmin).</span><span class="sxs-lookup"><span data-stu-id="ff56e-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, hpc\clusteradmin).</span></span> <span data-ttu-id="ff56e-146">Você gerencia o cluster de saudação do nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-146">You manage hello cluster from hello head node.</span></span>
2. <span data-ttu-id="ff56e-147">Use toocreate de procedimentos padrão do Windows Server uma conta de usuário de domínio no domínio do Active Directory do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-147">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="ff56e-148">Por exemplo, use o hello usuário do Active Directory e a ferramenta de computadores no nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-148">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="ff56e-149">exemplos de saudação neste artigo presumem que você criar um usuário de domínio chamado hpcuser no domínio hpclab de saudação (hpclab\hpcuser).</span><span class="sxs-lookup"><span data-stu-id="ff56e-149">hello examples in this article assume you create a domain user named hpcuser in hello hpclab domain (hpclab\hpcuser).</span></span>
3. <span data-ttu-id="ff56e-150">Adicione o cluster de HPC Pack toohello do usuário de domínio hello como um usuário de cluster.</span><span class="sxs-lookup"><span data-stu-id="ff56e-150">Add hello domain user toohello HPC Pack cluster as a cluster user.</span></span> <span data-ttu-id="ff56e-151">Para obter instruções, consulte [Adicionar ou remover usuários de cluster](https://technet.microsoft.com/library/ff919330.aspx).</span><span class="sxs-lookup"><span data-stu-id="ff56e-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span></span>
4. <span data-ttu-id="ff56e-152">Crie um arquivo chamado C:\cred.xml e copiar Olá RSA chave dados nele.</span><span class="sxs-lookup"><span data-stu-id="ff56e-152">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="ff56e-153">Você pode encontrar um exemplo no hello arquivos de exemplo no final deste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-153">You can find an example in hello sample files at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. <span data-ttu-id="ff56e-154">Abra um Prompt de comando e digite Olá Olá tooset credenciais dados da conta de hpclab\hpcuser de saudação do comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="ff56e-154">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="ff56e-155">Use Olá **extendeddata** toopass parâmetro hello nome do arquivo de C:\cred.xml Olá criado para dados de chave hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-155">You use hello **extendeddata** parameter toopass hello name of hello C:\cred.xml file you created for hello key data.</span></span>
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="ff56e-156">Esse comando é concluído com êxito sem resultados.</span><span class="sxs-lookup"><span data-stu-id="ff56e-156">This command completes successfully without output.</span></span> <span data-ttu-id="ff56e-157">Depois de definir credenciais Olá Olá para contas de usuário que é necessário toorun trabalhos, armazenar o arquivo de cred.xml Olá em um local seguro ou exclua-o.</span><span class="sxs-lookup"><span data-stu-id="ff56e-157">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
6. <span data-ttu-id="ff56e-158">Se você gerou Olá par de chaves RSA em um de seus nós do Linux, lembre-se as chaves de saudação toodelete depois de terminar de usá-los.</span><span class="sxs-lookup"><span data-stu-id="ff56e-158">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="ff56e-159">O HPC Pack não define a relação de confiança mútua se ele encontrar um arquivo id_rsa ou id_rsa.pub existente.</span><span class="sxs-lookup"><span data-stu-id="ff56e-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ff56e-160">Não é recomendável executar um trabalho de Linux como um administrador de cluster em um cluster compartilhado, porque um trabalho enviada por um administrador é executado na conta de raiz de saudação em nós do Linux hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="ff56e-161">Um trabalho enviada por um usuário não administrador é executado sob uma conta de usuário local do Linux com hello mesmo nome como usuário do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff56e-161">A job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="ff56e-162">Nesse caso, HPC Pack define a relação de confiança mútua para esse usuário do Linux em todos os nós de saudação alocados toohello trabalho.</span><span class="sxs-lookup"><span data-stu-id="ff56e-162">In this case, HPC Pack sets up mutual trust for this Linux user across all hello nodes allocated toohello job.</span></span> <span data-ttu-id="ff56e-163">Você pode configurar o usuário do Linux Olá manualmente em nós do Linux Olá antes de executar o trabalho de saudação ou HPC Pack cria usuário Olá automaticamente quando o trabalho de saudação é enviado.</span><span class="sxs-lookup"><span data-stu-id="ff56e-163">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="ff56e-164">Se o HPC Pack cria usuário hello, HPC Pack excluirá Olá trabalho concluído.</span><span class="sxs-lookup"><span data-stu-id="ff56e-164">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="ff56e-165">ameaça à segurança tooreduce, Olá chaves são removidas após a conclusão do trabalho de saudação em nós hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-165">tooreduce security threat, hello keys are removed after hello job completes on hello nodes.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="ff56e-166">Configurar um compartilhamento de arquivos para nós do Linux</span><span class="sxs-lookup"><span data-stu-id="ff56e-166">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="ff56e-167">Agora configurar um compartilhamento de arquivo SMB e montar a pasta compartilhada de saudação em todos os nós tooallow Olá Linux nós tooaccess NAMD arquivos Linux com um caminho comum.</span><span class="sxs-lookup"><span data-stu-id="ff56e-167">Now set up an SMB file share, and mount hello shared folder on all Linux nodes tooallow hello Linux nodes tooaccess NAMD files with a common path.</span></span> <span data-ttu-id="ff56e-168">A seguir é etapas toomount uma pasta compartilhada no nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-168">Following are steps toomount a shared folder on hello head node.</span></span> <span data-ttu-id="ff56e-169">Um compartilhamento é recomendado para distribuições como CentOS 6.6 que atualmente não há suporte para serviços de arquivo do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support hello Azure File service.</span></span> <span data-ttu-id="ff56e-170">Se os nós do Linux oferecem suporte a um compartilhamento de arquivos do Azure, consulte [como toouse armazenamento de arquivo do Azure com Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ff56e-170">If your Linux nodes support an Azure File share, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="ff56e-171">Para opções de compartilhamento de arquivos adicionais com o HPC Pack, e as etapas em [Introdução aos nós de computação do Linux em um cluster do HPC Pack no Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="ff56e-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="ff56e-172">Crie uma pasta no nó principal hello e compartilhá-lo tooEveryone Configurando os privilégios de leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="ff56e-172">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="ff56e-173">Neste exemplo, \\ \\CentOS66HN\Namd é o nome de saudação da pasta de hello, onde CentOS66HN é o nome do host de saudação do nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-173">In this example, \\\\CentOS66HN\Namd is hello name of hello folder, where CentOS66HN is hello host name of hello head node.</span></span>
2. <span data-ttu-id="ff56e-174">Crie uma subpasta chamada namd2 na pasta compartilhada hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-174">Create a subfolder named namd2 in hello shared folder.</span></span> <span data-ttu-id="ff56e-175">No namd2, crie outra subpasta chamada namdsample.</span><span class="sxs-lookup"><span data-stu-id="ff56e-175">In namd2, create another subfolder named namdsample.</span></span>
3. <span data-ttu-id="ff56e-176">Extraia os arquivos NAMD de saudação na pasta hello usando uma versão do Windows do **tar** ou outro utilitário do Windows que opera em arquivos mortos. tar.</span><span class="sxs-lookup"><span data-stu-id="ff56e-176">Extract hello NAMD files in hello folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span></span> 
   
   * <span data-ttu-id="ff56e-177">Extrair o arquivo de tar Olá NAMD muito\\\\CentOS66HN\Namd\namd2.</span><span class="sxs-lookup"><span data-stu-id="ff56e-177">Extract hello NAMD tar archive too\\\\CentOS66HN\Namd\namd2.</span></span>
   * <span data-ttu-id="ff56e-178">Extrair arquivos do tutorial de saudação em \\ \\CentOS66HN\Namd\namd2\namdsample.</span><span class="sxs-lookup"><span data-stu-id="ff56e-178">Extract hello tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span></span>
4. <span data-ttu-id="ff56e-179">Abra uma janela do Windows PowerShell e execute Olá toomount Olá pasta compartilhada em nós do Linux Olá de comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="ff56e-179">Open a Windows PowerShell window and run hello following commands toomount hello shared folder on hello Linux nodes.</span></span>
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="ff56e-180">Olá primeiro comando cria uma pasta chamada /namd2 em todos os nós no grupo de LinuxNodes hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-180">hello first command creates a folder named /namd2 on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="ff56e-181">comando segundo Olá monta Olá compartilhado pasta //CentOS66HN/Namd/namd2 na pasta de saudação com dir_mode e file_mode too777 de conjunto de bits.</span><span class="sxs-lookup"><span data-stu-id="ff56e-181">hello second command mounts hello shared folder //CentOS66HN/Namd/namd2 onto hello folder with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="ff56e-182">Olá *username* e *senha* Olá comando deve ser credenciais de saudação de um usuário no nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-182">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="ff56e-183">Olá "\\`" símbolo no segundo comando de saudação é um símbolo de escape para o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ff56e-183">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="ff56e-184">"\\`,"significa hello"," (vírgula) é uma parte do comando hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-184">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a><span data-ttu-id="ff56e-185">Criar um toorun de script Bash um trabalho NAMD</span><span class="sxs-lookup"><span data-stu-id="ff56e-185">Create a Bash script toorun a NAMD job</span></span>
<span data-ttu-id="ff56e-186">Precisa de seu trabalho NAMD um *nodelist* de arquivos para **charmrun** toodetermine número de saudação de nós toouse ao iniciar processos NAMD.</span><span class="sxs-lookup"><span data-stu-id="ff56e-186">Your NAMD job needs a *nodelist* file for **charmrun** toodetermine hello number of nodes toouse when starting NAMD processes.</span></span> <span data-ttu-id="ff56e-187">Você usar um script de Bash que gera o arquivo de nodelist hello e executa **charmrun** com esse arquivo nodelist.</span><span class="sxs-lookup"><span data-stu-id="ff56e-187">You use a Bash script that generates hello nodelist file and runs **charmrun** with this nodelist file.</span></span> <span data-ttu-id="ff56e-188">Depois, você pode enviar um trabalho do NAMD no Gerenciador de Cluster do HPC que chama esse script.</span><span class="sxs-lookup"><span data-stu-id="ff56e-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span></span>

<span data-ttu-id="ff56e-189">Usando um editor de texto de sua escolha, criar um script de Bash na pasta de /namd2 Olá que contém arquivos de programa NAMD hello e nomeie-a como hpccharmrun.sh. Para uma rápida verificação de conceito, copie o script de hpccharmrun.sh de exemplo hello fornecido no final deste artigo hello e vá muito[enviar um trabalho NAMD](#submit-a-namd-job).</span><span class="sxs-lookup"><span data-stu-id="ff56e-189">Using a text editor of your choice, create a Bash script in hello /namd2 folder containing hello NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy hello example hpccharmrun.sh script provided at hello end of this article and go too[Submit a NAMD job](#submit-a-namd-job).</span></span>

> [!TIP]
> <span data-ttu-id="ff56e-190">Salve o script como um arquivo de texto com as terminações de linha do Linux (somente LF, não CR LF).</span><span class="sxs-lookup"><span data-stu-id="ff56e-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="ff56e-191">Isso garante que ele seja executado corretamente em nós do Linux hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-191">This ensures that it runs properly on hello Linux nodes.</span></span>
> 
> 

<span data-ttu-id="ff56e-192">Veja a seguir os detalhes sobre a função desse script bash.</span><span class="sxs-lookup"><span data-stu-id="ff56e-192">Following are details about what this bash script does.</span></span> 

1. <span data-ttu-id="ff56e-193">Defina algumas variáveis.</span><span class="sxs-lookup"><span data-stu-id="ff56e-193">Define some variables.</span></span>
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. <span data-ttu-id="ff56e-194">Obter informações do nó de variáveis de ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-194">Get node information from hello environment variables.</span></span> <span data-ttu-id="ff56e-195">$NODESCORES armazena uma lista de palavras de divisão de $CCP_NODES_CORES.</span><span class="sxs-lookup"><span data-stu-id="ff56e-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span></span> <span data-ttu-id="ff56e-196">$COUNT é o tamanho de saudação do $NODESCORES.</span><span class="sxs-lookup"><span data-stu-id="ff56e-196">$COUNT is hello size of $NODESCORES.</span></span>
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   <span data-ttu-id="ff56e-197">Olá formato variável do hello $CCP_NODES_CORES é da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ff56e-197">hello format for hello $CCP_NODES_CORES variable is as follows:</span></span>
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   <span data-ttu-id="ff56e-198">Essa variável lista o número total de saudação de nós, nomes de nós e número de núcleos em cada nó que estão alocados toohello trabalho.</span><span class="sxs-lookup"><span data-stu-id="ff56e-198">This variable lists hello total number of nodes, node names, and number of cores on each node that are allocated toohello job.</span></span> <span data-ttu-id="ff56e-199">Por exemplo, se o trabalho de saudação precisar 10 toorun de núcleos, o valor de Olá de $CCP_NODES_CORES é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="ff56e-199">For example, if hello job needs 10 cores toorun, hello value of $CCP_NODES_CORES is similar to:</span></span>
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. <span data-ttu-id="ff56e-200">Se a variável CCP_NODES_CORES $ Olá não for definido, inicie **charmrun** diretamente.</span><span class="sxs-lookup"><span data-stu-id="ff56e-200">If hello $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span></span> <span data-ttu-id="ff56e-201">(Isso só deve ocorrer quando você executa esse script diretamente nos nós do Linux.)</span><span class="sxs-lookup"><span data-stu-id="ff56e-201">(This should only occur when you run this script directly on your Linux nodes.)</span></span>
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. <span data-ttu-id="ff56e-202">Outra opção é criar um arquivo nodelist para **charmrun**.</span><span class="sxs-lookup"><span data-stu-id="ff56e-202">Or create a nodelist file for **charmrun**.</span></span>
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. <span data-ttu-id="ff56e-203">Executar **charmrun** com o arquivo de nodelist hello, obter seu status de retorno e remover Olá nodelist arquivo final hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-203">Run **charmrun** with hello nodelist file, get its return status, and remove hello nodelist file at hello end.</span></span>
   
   <span data-ttu-id="ff56e-204">${CCP_NUMCPUS} é a outra variável de ambiente definido por nó principal do HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-204">${CCP_NUMCPUS} is another environment variable set by hello HPC Pack head node.</span></span> <span data-ttu-id="ff56e-205">Ele armazena o número de saudação de núcleos total alocada toothis trabalho.</span><span class="sxs-lookup"><span data-stu-id="ff56e-205">It stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="ff56e-206">Nós usamos toospecify número de saudação de processos para charmrun.</span><span class="sxs-lookup"><span data-stu-id="ff56e-206">We use it toospecify hello number of processes for charmrun.</span></span>
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. <span data-ttu-id="ff56e-207">Sair com hello **charmrun** status de retorno.</span><span class="sxs-lookup"><span data-stu-id="ff56e-207">Exit with hello **charmrun** return status.</span></span>
   
   ```
   exit ${RTNSTS}
   ```

<span data-ttu-id="ff56e-208">O seguinte é informações Olá no arquivo de nodelist hello, gera o script hello:</span><span class="sxs-lookup"><span data-stu-id="ff56e-208">Following is hello information in hello nodelist file, which hello script generates:</span></span>

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

<span data-ttu-id="ff56e-209">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ff56e-209">For example:</span></span>

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a><span data-ttu-id="ff56e-210">Enviar um trabalho NAMD</span><span class="sxs-lookup"><span data-stu-id="ff56e-210">Submit a NAMD job</span></span>
<span data-ttu-id="ff56e-211">Agora você está pronto toosubmit um trabalho NAMD no Gerenciador de Cluster de HPC.</span><span class="sxs-lookup"><span data-stu-id="ff56e-211">Now you are ready toosubmit a NAMD job in HPC Cluster Manager.</span></span>

1. <span data-ttu-id="ff56e-212">Conecte-se o nó principal do cluster tooyour e iniciar o Gerenciador de Cluster de HPC.</span><span class="sxs-lookup"><span data-stu-id="ff56e-212">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="ff56e-213">Em **gerenciamento de recursos**, verifique se nós de computação Olá Linux estão em Olá **Online** estado.</span><span class="sxs-lookup"><span data-stu-id="ff56e-213">In **Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="ff56e-214">Se não estiverem, selecione-os e clique em **Colocar Online**.</span><span class="sxs-lookup"><span data-stu-id="ff56e-214">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="ff56e-215">Em **Gerenciamento de Trabalhos**, clique em **Novo Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="ff56e-215">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="ff56e-216">Insira um nome para o trabalho como *hpccharmrun*.</span><span class="sxs-lookup"><span data-stu-id="ff56e-216">Enter a name for job such as *hpccharmrun*.</span></span>
   
   ![Novo trabalho do HPC][namd_job]
5. <span data-ttu-id="ff56e-218">Em Olá **detalhes do trabalho** página em **recursos de trabalho**, selecione o tipo de saudação do recurso como **nó** e conjunto hello **mínimo** too3.</span><span class="sxs-lookup"><span data-stu-id="ff56e-218">On hello **Job Details** page, under **Job Resources**, select hello type of resource as **Node** and set hello **Minimum** too3.</span></span> <span data-ttu-id="ff56e-219">, podemos executar o trabalho de saudação em três nós do Linux e cada nó tem quatro núcleos.</span><span class="sxs-lookup"><span data-stu-id="ff56e-219">, we run hello job on three Linux nodes and each node has four cores.</span></span>
   
   ![Recursos de trabalho][job_resources]
6. <span data-ttu-id="ff56e-221">Clique em **editar tarefas** Olá navegação esquerdo e, em seguida, clique em **adicionar** tooadd um trabalho de toohello de tarefa.</span><span class="sxs-lookup"><span data-stu-id="ff56e-221">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span>    
7. <span data-ttu-id="ff56e-222">Em Olá **detalhes da tarefa e redirecionamento de e/s** página saudação do conjunto de valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="ff56e-222">On hello **Task Details and I/O Redirection** page, set hello following values:</span></span>
   
   * <span data-ttu-id="ff56e-223">**Linha de comando** -
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span><span class="sxs-lookup"><span data-stu-id="ff56e-223">**Command line** -
`/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span></span>
     
     > [!TIP]
     > <span data-ttu-id="ff56e-224">Olá, linha de comando anterior é um único comando sem quebras de linha.</span><span class="sxs-lookup"><span data-stu-id="ff56e-224">hello preceding command line is a single command without line breaks.</span></span> <span data-ttu-id="ff56e-225">Ele encapsula tooappear em várias linhas em **linha de comando**.</span><span class="sxs-lookup"><span data-stu-id="ff56e-225">It wraps tooappear on several lines under **Command line**.</span></span>
     > 
     > 
   * <span data-ttu-id="ff56e-226">**Diretório de trabalho** - /namd2</span><span class="sxs-lookup"><span data-stu-id="ff56e-226">**Working directory** - /namd2</span></span>
   * <span data-ttu-id="ff56e-227">**Mínimo** - 3</span><span class="sxs-lookup"><span data-stu-id="ff56e-227">**Minimum** - 3</span></span>
     
     ![Detalhes de tarefa][task_details]
     
     > [!NOTE]
     > <span data-ttu-id="ff56e-229">Definir diretório de trabalho Olá aqui porque **charmrun** tenta toonavigate toohello mesmo diretório de trabalho em cada nó.</span><span class="sxs-lookup"><span data-stu-id="ff56e-229">You set hello working directory here because **charmrun** tries toonavigate toohello same working directory on each node.</span></span> <span data-ttu-id="ff56e-230">Se o diretório de trabalho de saudação não for definido, o HPC Pack inicia o comando de saudação em uma pasta nomeada aleatoriamente criada em um de nós do Linux hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-230">If hello working directory isn't set, HPC Pack starts hello command in a randomly named folder created on one of hello Linux nodes.</span></span> <span data-ttu-id="ff56e-231">Isso faz com que Olá erro a seguir no hello outros nós: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid esse problema, especifique um caminho de pasta que possa ser acessado por todos os nós como diretório de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-231">This causes hello following error on hello other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid this problem, specify a folder path that can be accessed by all nodes as hello working directory.</span></span>
     > 
     > 
8. <span data-ttu-id="ff56e-232">Clique em **Okey** e, em seguida, clique em **enviar** toorun esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="ff56e-232">Click **OK** and then click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="ff56e-233">Por padrão, o HPC Pack envia trabalho hello como sua conta de logon do usuário atual.</span><span class="sxs-lookup"><span data-stu-id="ff56e-233">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="ff56e-234">Uma caixa de diálogo pode solicitar que você tooenter Olá nome e uma senha depois de clicar em **enviar**.</span><span class="sxs-lookup"><span data-stu-id="ff56e-234">A dialog box might prompt you tooenter hello user name and password after you click **Submit**.</span></span>
   
   ![Credenciais de trabalho][creds]
   
   <span data-ttu-id="ff56e-236">Sob algumas condições, o HPC Pack lembra informações de usuário de saudação antes de entrada e não mostrar esta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ff56e-236">Under some conditions, HPC Pack remembers hello user information you input before and doesn't show this dialog box.</span></span> <span data-ttu-id="ff56e-237">toomake HPC Pack mostrá-la novamente, insira Olá comando no Prompt de comando a seguir e, em seguida, enviar o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="ff56e-237">toomake HPC Pack show it again, enter hello following command at a Command Prompt and then submit hello job.</span></span>
   
   ```command
   hpccred delcreds
   ```
9. <span data-ttu-id="ff56e-238">trabalho de saudação toma toofinish de vários minutos.</span><span class="sxs-lookup"><span data-stu-id="ff56e-238">hello job takes several minutes toofinish.</span></span>
10. <span data-ttu-id="ff56e-239">Localizar o log do trabalho de saudação em \\ <headnodeName>\Namd\namd2\namd2_hpccharmrun.log e hello arquivos de saída \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span><span class="sxs-lookup"><span data-stu-id="ff56e-239">Find hello job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and hello output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span></span>
11. <span data-ttu-id="ff56e-240">Opcionalmente, inicie VMD tooview os resultados do trabalho.</span><span class="sxs-lookup"><span data-stu-id="ff56e-240">Optionally, start VMD tooview your job results.</span></span> <span data-ttu-id="ff56e-241">etapas Olá para visualizar os arquivos de saída NAMD hello (nesse caso, uma molécula de proteína ubiquitin em uma esfera de água) estão além do escopo deste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="ff56e-241">hello steps for visualizing hello NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond hello scope of this article.</span></span> <span data-ttu-id="ff56e-242">Veja [Tutorial do NAMD](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="ff56e-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span></span>
    
    ![Resultados de trabalho][vmd_view]

## <a name="sample-files"></a><span data-ttu-id="ff56e-244">Arquivos de exemplo</span><span class="sxs-lookup"><span data-stu-id="ff56e-244">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="ff56e-245">Exemplo de arquivo de configuração XML para implantação de cluster pelo script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff56e-245">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
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

### <a name="sample-credxml-file"></a><span data-ttu-id="ff56e-246">Exemplo de arquivo cred.xml</span><span class="sxs-lookup"><span data-stu-id="ff56e-246">Sample cred.xml file</span></span>
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

### <a name="sample-hpccharmrunsh-script"></a><span data-ttu-id="ff56e-247">Exemplo de script hpccharmrun.sh</span><span class="sxs-lookup"><span data-stu-id="ff56e-247">Sample hpccharmrun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
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
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
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
