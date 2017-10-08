---
title: "cluster de aaaSet o HPC Pack híbridos no Azure | Microsoft Docs"
description: "Saiba como toouse Microsoft HPC Pack e do Azure tooset até um pequeno, alto desempenho computação (HPC) cluster híbrido"
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="bf534-103">Configurar um cluster HPC (computação de alto desempenho) híbrido com nós de computação do Azure sob demanda e o Microsoft HPC Pack</span><span class="sxs-lookup"><span data-stu-id="bf534-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="bf534-104">Use o Microsoft HPC Pack 2012 R2 e do Azure tooset a um pequeno, híbrido computação de alto desempenho cluster (HPC).</span><span class="sxs-lookup"><span data-stu-id="bf534-104">Use Microsoft HPC Pack 2012 R2 and Azure tooset up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="bf534-105">Olá mostrados neste artigo consiste em um nó de cabeçalho do HPC Pack no local e alguns computação nós sob demanda do Azure você implanta o serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="bf534-105">hello cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span></span> <span data-ttu-id="bf534-106">Em seguida, você pode executar trabalhos de computação em cluster híbrido que hello.</span><span class="sxs-lookup"><span data-stu-id="bf534-106">You can then run compute jobs on hello hybrid cluster.</span></span>

![Cluster híbrido de HPC][Overview] 

<span data-ttu-id="bf534-108">Este tutorial mostra uma abordagem, chamados de cluster "intermitência toohello nuvem" aplicativos de computação intensa de toorun toouse escalonáveis e sob demanda de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf534-108">This tutorial shows one approach, sometimes called cluster "burst toohello cloud," toouse scalable, on-demand Azure resources toorun compute-intensive applications.</span></span>

<span data-ttu-id="bf534-109">Este tutorial não pressupõe nenhuma experiência anterior com clusters de cálculo ou com o HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="bf534-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span></span> <span data-ttu-id="bf534-110">É pretendido toohelp somente que você implantar um cluster de computação híbrido rapidamente para fins de demonstração.</span><span class="sxs-lookup"><span data-stu-id="bf534-110">It is intended only toohelp you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="bf534-111">Para considerações e etapas toodeploy cluster híbridos HPC Pack em maior escala em um ambiente de produção ou toouse HPC Pack 2016, consulte Olá [detalhadas orientação](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="bf534-111">For considerations and steps toodeploy a hybrid HPC Pack cluster at greater scale in a production environment, or toouse HPC Pack 2016, see hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="bf534-112">Para ver outros cenários com o HPC Pack, incluindo a implantação de cluster automatizada nas máquinas virtuais do Azure, confira [Opções de cluster HPC com o Microsoft HPC Pack no Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bf534-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bf534-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bf534-113">Prerequisites</span></span>
* <span data-ttu-id="bf534-114">**Assinatura do Azure** – Se não tiver uma, você poderá criar uma [conta gratuita](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="bf534-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="bf534-115">**Um computador local executando o Windows Server 2012 R2 ou o Windows Server 2012** -usar este computador como nó de cabeçalho de saudação do cluster HPC hello.</span><span class="sxs-lookup"><span data-stu-id="bf534-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as hello head node of hello HPC cluster.</span></span> <span data-ttu-id="bf534-116">Se você ainda não estiver executando o Windows Server, poderá baixar e instalar uma [versão de avaliação](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span><span class="sxs-lookup"><span data-stu-id="bf534-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="bf534-117">computador Olá deve ser tooan ingressado no domínio de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bf534-117">hello computer must be joined tooan Active Directory domain.</span></span> <span data-ttu-id="bf534-118">Para fins de teste, você pode configurar o computador do nó principal hello como um controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="bf534-118">For test purposes, you can configure hello head node computer as a domain controller.</span></span> <span data-ttu-id="bf534-119">tooadd Olá a função de servidor Serviços de domínio do Active Directory e promover o computador do nó principal hello como um controlador de domínio, consulte documentação Olá para o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="bf534-119">tooadd hello Active Directory Domain Services server role and promote hello head node computer as a domain controller, see hello documentation for Windows Server.</span></span>
  * <span data-ttu-id="bf534-120">toosupport HPC Pack, o sistema operacional de saudação deve ser instalado em um desses idiomas: inglês, japonês ou chinês (simplificado).</span><span class="sxs-lookup"><span data-stu-id="bf534-120">toosupport HPC Pack, hello operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="bf534-121">Verifique se as atualizações importantes e críticas foram instaladas.</span><span class="sxs-lookup"><span data-stu-id="bf534-121">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="bf534-122">**HPC Pack 2012 R2** - [baixar](http://go.microsoft.com/fwlink/p/?linkid=328024) pacote de instalação de Olá para a versão mais recente da saudação livre de custos e cópia Olá arquivos toohello principal computador do nó.</span><span class="sxs-lookup"><span data-stu-id="bf534-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) hello installation package for hello latest version free of charge and copy hello files toohello head node computer.</span></span> <span data-ttu-id="bf534-123">Escolha os arquivos de instalação Olá mesmo idioma em que a instalação do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="bf534-123">Choose installation files in hello same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="bf534-124">Se você quiser toouse HPC Pack 2016, em vez de HPC Pack 2012 R2, a configuração adicional é necessária.</span><span class="sxs-lookup"><span data-stu-id="bf534-124">If you want toouse HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="bf534-125">Consulte Olá [detalhadas orientação](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="bf534-125">See hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="bf534-126">**Conta de domínio** -essa conta deve ser configurada com permissões de administrador local no nó principal de saudação tooinstall HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="bf534-126">**Domain account** - This account must be configured with local Administrator permissions on hello head node tooinstall HPC Pack.</span></span>
* <span data-ttu-id="bf534-127">**Conectividade TCP na porta 443** de saudação tooAzure de nó principal.</span><span class="sxs-lookup"><span data-stu-id="bf534-127">**TCP connectivity on port 443** from hello head node tooAzure.</span></span>

## <a name="install-hpc-pack-on-hello-head-node"></a><span data-ttu-id="bf534-128">Instala o HPC Pack no nó de cabeçalho Olá</span><span class="sxs-lookup"><span data-stu-id="bf534-128">Install HPC Pack on hello head node</span></span>
<span data-ttu-id="bf534-129">Primeiro, instale o Microsoft HPC Pack em seu computador local executando o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="bf534-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span></span> <span data-ttu-id="bf534-130">Este computador se torna o nó principal de saudação do cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf534-130">This computer becomes hello head node of hello cluster.</span></span>

1. <span data-ttu-id="bf534-131">Faça logon no nó principal toohello usando uma conta de domínio que tenha permissões de administrador local.</span><span class="sxs-lookup"><span data-stu-id="bf534-131">Log on toohello head node by using a domain account that has local Administrator permissions.</span></span>

2. <span data-ttu-id="bf534-132">Inicie o hello Assistente de instalação do HPC Pack executando Setup.exe Olá HPC Pack em arquivos de instalação.</span><span class="sxs-lookup"><span data-stu-id="bf534-132">Start hello HPC Pack Installation Wizard by running Setup.exe from hello HPC Pack installation files.</span></span>

3. <span data-ttu-id="bf534-133">Em Olá **instalação do HPC Pack 2012 R2** tela, clique em **nova instalação ou adicione a nova instalação existente de tooan de recursos**.</span><span class="sxs-lookup"><span data-stu-id="bf534-133">On hello **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features tooan existing installation**.</span></span>

    ![Instalação do HPC Pack 2012][install_hpc1]

4. <span data-ttu-id="bf534-135">Em Olá **página Contrato de usuário do Software Microsoft**, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="bf534-135">On hello **Microsoft Software User Agreement page**, click **Next**.</span></span>

5. <span data-ttu-id="bf534-136">Em Olá **Selecionar tipo de instalação** , clique em **criar um novo cluster HPC criando um nó de cabeçalho**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="bf534-136">On hello **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>

6. <span data-ttu-id="bf534-137">Assistente de saudação executa vários testes de pré-instalação.</span><span class="sxs-lookup"><span data-stu-id="bf534-137">hello wizard runs several pre-installation tests.</span></span> <span data-ttu-id="bf534-138">Clique em **próximo** em Olá **regras de instalação** página se todos os testes passarem.</span><span class="sxs-lookup"><span data-stu-id="bf534-138">Click **Next** on hello **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="bf534-139">Caso contrário, examine Olá informações fornecidas e faça as alterações necessárias em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="bf534-139">Otherwise, review hello information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="bf534-140">Em seguida, execute novamente os testes de saudação ou se necessário iniciar Olá Assistente de instalação novamente.</span><span class="sxs-lookup"><span data-stu-id="bf534-140">Then run hello tests again or if necessary start hello Installation Wizard again.</span></span>
7. <span data-ttu-id="bf534-141">Em Olá **configuração de banco de dados do HPC** página, certifique-se de **nó de cabeçalho** está selecionada para todos os bancos de dados do HPC e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="bf534-141">On hello **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span> 

    ![Configuração do BD][install_hpc4]

8. <span data-ttu-id="bf534-143">Aceite as seleções de padrão nas páginas de saudação restantes do Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf534-143">Accept default selections on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="bf534-144">Em Olá **instalar componentes necessários** , clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="bf534-144">On hello **Install Required Components** page, click **Install**.</span></span>
   
    ![Instalar][install_hpc6]

9. <span data-ttu-id="bf534-146">Após a conclusão da instalação Olá, desmarque **iniciar Gerenciador de Cluster de HPC** e, em seguida, clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="bf534-146">After hello installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="bf534-147">(Você iniciará o Gerenciador de Cluster de HPC em uma etapa posterior.)</span><span class="sxs-lookup"><span data-stu-id="bf534-147">(You start HPC Cluster Manager in a later step.)</span></span>
   
    ![Concluir][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a><span data-ttu-id="bf534-149">Preparar Olá assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="bf534-149">Prepare hello Azure subscription</span></span>
<span data-ttu-id="bf534-150">Executar Olá etapas Olá [portal do Azure](https://portal.azure.com) com sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf534-150">Perform hello following steps in hello [Azure portal](https://portal.azure.com) with your Azure subscription.</span></span> <span data-ttu-id="bf534-151">Depois de concluir essas etapas, você pode implantar nós do Azure do nó principal do hello local.</span><span class="sxs-lookup"><span data-stu-id="bf534-151">After completing these steps, you can deploy Azure nodes from hello on-premises head node.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="bf534-152">Além disso, tome nota de sua ID de assinatura do Azure, que será necessária posteriormente.</span><span class="sxs-lookup"><span data-stu-id="bf534-152">Also make a note of your Azure subscription ID, which you need later.</span></span> <span data-ttu-id="bf534-153">Localizar a ID de saudação em **assinaturas** no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf534-153">Find hello ID in **Subscriptions** in hello portal.</span></span>
  > 

### <a name="upload-hello-default-management-certificate"></a><span data-ttu-id="bf534-154">Carregar certificado de gerenciamento saudação padrão</span><span class="sxs-lookup"><span data-stu-id="bf534-154">Upload hello default management certificate</span></span>
<span data-ttu-id="bf534-155">HPC Pack instala um certificado autoassinado no nó principal do hello, chamado de certificado de gerenciamento padrão Microsoft HPC Azure hello, que pode ser carregado como um certificado de gerenciamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf534-155">HPC Pack installs a self-signed certificate on hello head node, called hello Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="bf534-156">Esse certificado é fornecido para teste e conexão de saudação implantações de prova de conceito toosecure entre Olá nó principal e o Azure.</span><span class="sxs-lookup"><span data-stu-id="bf534-156">This certificate is provided for testing and proof-of-concept deployments toosecure hello connection between hello head node and Azure.</span></span>

1. <span data-ttu-id="bf534-157">No computador do nó principal hello, entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bf534-157">From hello head node computer, sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="bf534-158">Clique em **Assinaturas** > *nome_da_assinatura*.</span><span class="sxs-lookup"><span data-stu-id="bf534-158">Click **Subscriptions** > *your_subscription_name*.</span></span>

3. <span data-ttu-id="bf534-159">Clique em **Certificados de gerenciamento** > **Carregar**.4.</span><span class="sxs-lookup"><span data-stu-id="bf534-159">Click **Management certificates** > **Upload**.4.</span></span> <span data-ttu-id="bf534-160">Procure no nó principal Olá Olá arquivo C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span><span class="sxs-lookup"><span data-stu-id="bf534-160">Browse on hello head node for hello file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="bf534-161">Em seguida, clique em **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="bf534-161">Then, click **Upload**.</span></span>

   
<span data-ttu-id="bf534-162">Olá **padrão do HPC Azure Management** certificado será exibido na lista de saudação de certificados de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="bf534-162">hello **Default HPC Azure Management** certificate appears in hello list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="bf534-163">Criar um serviço de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="bf534-163">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="bf534-164">Para melhor desempenho, criar serviço de nuvem hello e conta de armazenamento da saudação (em uma etapa posterior) no hello mesma região geográfica.</span><span class="sxs-lookup"><span data-stu-id="bf534-164">For best performance, create hello cloud service and hello storage account (in a later step) in hello same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="bf534-165">No portal de saudação, clique em **(clássico) de serviços de nuvem** > **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bf534-165">In hello portal, click **Cloud services (classic)** > **+Add**.</span></span>

2.  <span data-ttu-id="bf534-166">Digite um nome DNS para o serviço de saudação, escolha um grupo de recursos e um local e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="bf534-166">Type a DNS name for hello service, choose a resource group and a location, and then click **Create**.</span></span>


### <a name="create-an-azure-storage-account"></a><span data-ttu-id="bf534-167">Criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="bf534-167">Create an Azure storage account</span></span>
1. <span data-ttu-id="bf534-168">No portal de saudação, clique em **contas de armazenamento (clássico)** > **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bf534-168">In hello portal, click **Storage accounts (classic)** > **+Add**.</span></span>

2. <span data-ttu-id="bf534-169">Digite um nome para a conta de saudação e selecione Olá **clássico** modelo de implantação.</span><span class="sxs-lookup"><span data-stu-id="bf534-169">Type a name for hello account, and select hello **Classic** deployment model.</span></span>

3. <span data-ttu-id="bf534-170">Escolha um grupo de recursos e um local e deixe as outras configurações com os valores padrão.</span><span class="sxs-lookup"><span data-stu-id="bf534-170">Choose a resource group and a location, and leave other settings at default values.</span></span> <span data-ttu-id="bf534-171">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="bf534-171">Then click **Create**.</span></span>

## <a name="configure-hello-head-node"></a><span data-ttu-id="bf534-172">Configurar o nó principal Olá</span><span class="sxs-lookup"><span data-stu-id="bf534-172">Configure hello head node</span></span>
<span data-ttu-id="bf534-173">toouse toodeploy do Gerenciador de Cluster de HPC nós do Azure e toosubmit trabalhos, primeiro executar algumas etapas de configuração de cluster necessário.</span><span class="sxs-lookup"><span data-stu-id="bf534-173">toouse HPC Cluster Manager toodeploy Azure nodes and toosubmit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="bf534-174">No nó de cabeçalho hello, inicie o Gerenciador de Cluster de HPC.</span><span class="sxs-lookup"><span data-stu-id="bf534-174">On hello head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="bf534-175">Se hello **selecionar nó principal** caixa de diálogo for exibida, clique em **computador Local**.</span><span class="sxs-lookup"><span data-stu-id="bf534-175">If hello **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="bf534-176">Olá **lista de tarefas de implantação** é exibida.</span><span class="sxs-lookup"><span data-stu-id="bf534-176">hello **Deployment To-do List** appears.</span></span>

2. <span data-ttu-id="bf534-177">Em **Tarefas de implantação necessárias**, clique em **Configurar sua rede**.</span><span class="sxs-lookup"><span data-stu-id="bf534-177">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![Configurar Rede][config_hpc2]

3. <span data-ttu-id="bf534-179">No Assistente de configuração de rede do hello, selecione **todos os nós somente em uma rede corporativa** (topologia 5).</span><span class="sxs-lookup"><span data-stu-id="bf534-179">In hello Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span> <span data-ttu-id="bf534-180">Essa configuração de rede é hello mais simples para fins de demonstração.</span><span class="sxs-lookup"><span data-stu-id="bf534-180">This network configuration is hello simplest for demonstration purposes.</span></span>
   
    ![Topologia 5][config_hpc3]
   
4. <span data-ttu-id="bf534-182">Clique em **próximo** tooaccept valores padrão Olá restantes páginas do Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf534-182">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="bf534-183">Em seguida, na Olá **revisão** , clique em **configurar** toocomplete configuração de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf534-183">Then, on hello **Review** tab, click **Configure** toocomplete hello network configuration.</span></span>

5. <span data-ttu-id="bf534-184">Em Olá **lista de tarefas de implantação**, clique em **fornecer credenciais de instalação**.</span><span class="sxs-lookup"><span data-stu-id="bf534-184">In hello **Deployment To-do List**, click **Provide installation credentials**.</span></span>

6. <span data-ttu-id="bf534-185">Em Olá **credenciais de instalação** caixa de diálogo, digite as credenciais da conta de domínio Olá que você usou tooinstall HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="bf534-185">In hello **Installation Credentials** dialog box, type hello credentials of hello domain account that you used tooinstall HPC Pack.</span></span> <span data-ttu-id="bf534-186">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf534-186">Then click **OK**.</span></span> 
   
    ![Credenciais de instalação][config_hpc6]
   
7. <span data-ttu-id="bf534-188">Em Olá **lista de tarefas de implantação**, clique em **configurar Olá nomeação de novos nós**.</span><span class="sxs-lookup"><span data-stu-id="bf534-188">In hello **Deployment To-do List**, click **Configure hello naming of new nodes**.</span></span>

8. <span data-ttu-id="bf534-189">Em Olá **série de nomeação de nó especifique** caixa de diálogo caixa, aceite o padrão de saudação nomenclatura série e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="bf534-189">In hello **Specify Node Naming Series** dialog box, accept hello default naming series and click **OK**.</span></span> <span data-ttu-id="bf534-190">Conclua esta etapa, embora hello nós do Azure que você adicionar neste tutorial são nomeadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="bf534-190">Complete this step even though hello Azure nodes you add in this tutorial are named automatically.</span></span>
   
    ![Nomeação de nós][config_hpc8]
   
9. <span data-ttu-id="bf534-192">Em Olá **lista de tarefas de implantação**, clique em **criar um modelo de nó**.</span><span class="sxs-lookup"><span data-stu-id="bf534-192">In hello **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="bf534-193">Mais tarde no tutorial hello, use cluster de toohello Olá nós modelo tooadd nós do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf534-193">Later in hello tutorial, you use hello node template tooadd Azure nodes toohello cluster.</span></span>

10. <span data-ttu-id="bf534-194">No Assistente Criar modelo de nó de hello, faça Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf534-194">In hello Create Node Template Wizard, do hello following:</span></span>
    
    <span data-ttu-id="bf534-195">a.</span><span class="sxs-lookup"><span data-stu-id="bf534-195">a.</span></span> <span data-ttu-id="bf534-196">Em Olá **Escolher tipo de modelo de nó** , clique em **modelo de nó do Windows Azure**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="bf534-196">On hello **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span></span>
    
    ![Modelo do nó][config_hpc10]
    
    <span data-ttu-id="bf534-198">b.</span><span class="sxs-lookup"><span data-stu-id="bf534-198">b.</span></span> <span data-ttu-id="bf534-199">Clique em **próximo** nome do modelo tooaccept saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="bf534-199">Click **Next** tooaccept hello default template name.</span></span>
    
    <span data-ttu-id="bf534-200">c.</span><span class="sxs-lookup"><span data-stu-id="bf534-200">c.</span></span> <span data-ttu-id="bf534-201">Em Olá **fornecem informações de assinatura** , insira sua ID de assinatura do Azure (disponível em suas informações de conta do Azure).</span><span class="sxs-lookup"><span data-stu-id="bf534-201">On hello **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="bf534-202">Em seguida, em **Certificado de gerenciamento**, procure por **Gerenciamento do Azure Padrão no Microsoft HPC.**</span><span class="sxs-lookup"><span data-stu-id="bf534-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span></span> <span data-ttu-id="bf534-203">Em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="bf534-203">Then click **Next**.</span></span>
    
    ![Modelo do nó][config_hpc12]
    
    <span data-ttu-id="bf534-205">d.</span><span class="sxs-lookup"><span data-stu-id="bf534-205">d.</span></span> <span data-ttu-id="bf534-206">Em Olá **fornecer informações sobre o serviço** página, serviço de nuvem selecione hello e conta de armazenamento Olá que você criou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="bf534-206">On hello **Provide Service Information** page, select hello cloud service and hello storage account that you created in a previous step.</span></span> <span data-ttu-id="bf534-207">Em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="bf534-207">Then click **Next**.</span></span>
    
    ![Modelo do nó][config_hpc13]
    
    <span data-ttu-id="bf534-209">e.</span><span class="sxs-lookup"><span data-stu-id="bf534-209">e.</span></span> <span data-ttu-id="bf534-210">Clique em **próximo** tooaccept valores padrão Olá restantes páginas do Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf534-210">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="bf534-211">Em seguida, na Olá **revisão** , clique em **criar** toocreate modelo de nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf534-211">Then, on hello **Review** tab, click **Create** toocreate hello node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="bf534-212">Por padrão, modelo de nó do Azure Olá inclui configurações para toostart (provisionar) e stop Olá nós manualmente, usando o Gerenciador de Cluster de HPC.</span><span class="sxs-lookup"><span data-stu-id="bf534-212">By default, hello Azure node template includes settings for you toostart (provision) and stop hello nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="bf534-213">Opcionalmente, você pode configurar um agendamento toostart e parar Olá nós do Azure automaticamente.</span><span class="sxs-lookup"><span data-stu-id="bf534-213">You can optionally configure a schedule toostart and stop hello Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a><span data-ttu-id="bf534-214">Adicionar nós do Azure toohello cluster</span><span class="sxs-lookup"><span data-stu-id="bf534-214">Add Azure nodes toohello cluster</span></span>
<span data-ttu-id="bf534-215">Agora use o cluster de toohello Olá nós modelo tooadd nós do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf534-215">Now use hello node template tooadd Azure nodes toohello cluster.</span></span> <span data-ttu-id="bf534-216">Adicionar o cluster do hello nós toohello armazena suas informações de configuração para que você possa iniciar (provisionar)-los a qualquer momento no serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="bf534-216">Adding hello nodes toohello cluster stores their configuration information so that you can start (provision) them at any time in hello cloud service.</span></span> <span data-ttu-id="bf534-217">Sua assinatura obtém cobrada somente para nós do Azure depois Olá instâncias são executadas no serviço de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="bf534-217">Your subscription only gets charged for Azure nodes after hello instances are running in hello cloud service.</span></span>

<span data-ttu-id="bf534-218">Siga estas etapas tooadd dois pequeno nós.</span><span class="sxs-lookup"><span data-stu-id="bf534-218">Follow these steps tooadd two Small nodes.</span></span>

1. <span data-ttu-id="bf534-219">No Gerenciador de Cluster HPC, clique em **Gerenciamento de Nós** (chamado de **Gerenciamento de Recursos** em versões atuais do HPC Pack) > **Adicionar Nó**.</span><span class="sxs-lookup"><span data-stu-id="bf534-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span></span>
   
    ![Adicionar Nó][add_node1]

2. <span data-ttu-id="bf534-221">Em Olá Assistente para adicionar nó, em Olá **Selecionar método de implantação** , clique em **nós do Windows Azure adicionar**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="bf534-221">In hello Add Node Wizard, on hello **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Adicionar nó do Azure][add_node1_1]

3. <span data-ttu-id="bf534-223">Em Olá **especificar novos nós** página, o modelo de nó do Azure selecione Olá criado anteriormente (chamado por padrão **modelo AzureNode**).</span><span class="sxs-lookup"><span data-stu-id="bf534-223">On hello **Specify New Nodes** page, select hello Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="bf534-224">Em seguida, especifique **2** nós de tamanho **Pequeno** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="bf534-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![Especificar nós][add_node2]
   
4. <span data-ttu-id="bf534-226">Em Olá **Concluindo Olá Assistente para adicionar nó** , clique em **concluir**.</span><span class="sxs-lookup"><span data-stu-id="bf534-226">On hello **Completing hello Add Node Wizard** page, click **Finish**.</span></span>
    
     <span data-ttu-id="bf534-227">Dois nós do Azure, chamados **AzureCN-0001** e **AzureCN-0002**, agora são exibidos no Gerenciador de Cluster de HPC.</span><span class="sxs-lookup"><span data-stu-id="bf534-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="bf534-228">Ambos são Olá **não implantado** estado.</span><span class="sxs-lookup"><span data-stu-id="bf534-228">Both are in hello **Not-Deployed** state.</span></span>
   
    ![Nós adicionados][add_node3]

## <a name="start-hello-azure-nodes"></a><span data-ttu-id="bf534-230">Iniciar Olá nós do Azure</span><span class="sxs-lookup"><span data-stu-id="bf534-230">Start hello Azure nodes</span></span>
<span data-ttu-id="bf534-231">Quando desejar que recursos de cluster toouse Olá no Azure, use o Gerenciador de Cluster de HPC toostart (provisionar) Olá nós do Azure e colocarão-los online.</span><span class="sxs-lookup"><span data-stu-id="bf534-231">When you want toouse hello cluster resources in Azure, use HPC Cluster Manager toostart (provision) hello Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="bf534-232">No Gerenciador de Cluster de HPC, clique em **nó gerenciamento** (chamado **gerenciamento de recursos** nas versões atuais do HPC Pack), e selecione Olá nós do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf534-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select hello Azure nodes.</span></span>

2. <span data-ttu-id="bf534-233">Clique em **Iniciar** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="bf534-233">Click **Start**, and then click **OK**.</span></span>
   
   ![Iniciar nós][add_node4]
   
    <span data-ttu-id="bf534-235">nós Olá transição toohello **provisionamento** estado.</span><span class="sxs-lookup"><span data-stu-id="bf534-235">hello nodes transition toohello **Provisioning** state.</span></span> <span data-ttu-id="bf534-236">Saudação de exibição saudação do log tootrack progresso do provisionamento de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="bf534-236">View hello provisioning log tootrack hello provisioning progress.</span></span>
   
    ![Provisionar nós][add_node6]

3. <span data-ttu-id="bf534-238">Depois de alguns minutos, hello nós do Azure concluir o provisionamento e estão em Olá **Offline** estado.</span><span class="sxs-lookup"><span data-stu-id="bf534-238">After a few minutes, hello Azure nodes finish provisioning and are in hello **Offline** state.</span></span> <span data-ttu-id="bf534-239">Nesse estado, instâncias de função hello estão em execução, mas ainda não podem aceitar trabalhos de cluster.</span><span class="sxs-lookup"><span data-stu-id="bf534-239">In this state, hello role instances are running but cannot yet accept cluster jobs.</span></span>

4. <span data-ttu-id="bf534-240">tooconfirm que Olá instâncias de função está em execução, no hello portal do Azure, clique em **serviços de nuvem (clássicos)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="bf534-240">tooconfirm that hello role instances are running, in hello Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span></span>
   
   <span data-ttu-id="bf534-241">Você deverá ver dois **HpcWorkerRole** instâncias (nós) em execução no serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf534-241">You should see two **HpcWorkerRole** instances (nodes) running in hello service.</span></span> <span data-ttu-id="bf534-242">HPC Pack automaticamente implanta dois **HpcProxy** instâncias a comunicação entre o nó principal hello e Azure toohandle (tamanho médio).</span><span class="sxs-lookup"><span data-stu-id="bf534-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) toohandle communication between hello head node and Azure.</span></span>

   ![Executando instâncias][view_instances1]

5. <span data-ttu-id="bf534-244">toobring Olá nós do Azure online toorun cluster trabalhos, selecione Olá nós, com o botão direito e clique **colocar Online**.</span><span class="sxs-lookup"><span data-stu-id="bf534-244">toobring hello Azure nodes online toorun cluster jobs, select hello nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![Nós off-line][add_node7]
   
    <span data-ttu-id="bf534-246">Gerenciador de Cluster de HPC indica que nós Olá nessa Olá **Online** estado.</span><span class="sxs-lookup"><span data-stu-id="bf534-246">HPC Cluster Manager indicates that hello nodes are in hello **Online** state.</span></span>

## <a name="run-a-command-across-hello-cluster"></a><span data-ttu-id="bf534-247">Executar um comando de cluster Olá</span><span class="sxs-lookup"><span data-stu-id="bf534-247">Run a command across hello cluster</span></span>
<span data-ttu-id="bf534-248">instalação de saudação toocheck, use Olá HPC Pack **clusrun** comando toorun um comando ou o aplicativo em um ou mais nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="bf534-248">toocheck hello installation, use hello HPC Pack **clusrun** command toorun a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="bf534-249">Como um exemplo simples, use **clusrun** tooget configuração de IP de saudação do hello nós do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf534-249">As a simple example, use **clusrun** tooget hello IP configuration of hello Azure nodes.</span></span>

1. <span data-ttu-id="bf534-250">No nó de cabeçalho hello, abra um prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="bf534-250">On hello head node, open a command prompt as an administrator.</span></span>

2. <span data-ttu-id="bf534-251">Digite hello comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf534-251">Type hello following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`

3. <span data-ttu-id="bf534-252">Se solicitado, insira sua senha de administrador de cluster.</span><span class="sxs-lookup"><span data-stu-id="bf534-252">If prompted, enter your cluster administrator password.</span></span> <span data-ttu-id="bf534-253">Você deve ver a saída do comando a seguir toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="bf534-253">You should see command output similar toohello following.</span></span>
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="bf534-255">Executar um trabalho de teste</span><span class="sxs-lookup"><span data-stu-id="bf534-255">Run a test job</span></span>
<span data-ttu-id="bf534-256">Agora, envie um trabalho de teste é executado em um cluster híbrido que hello.</span><span class="sxs-lookup"><span data-stu-id="bf534-256">Now submit a test job that runs on hello hybrid cluster.</span></span> <span data-ttu-id="bf534-257">Este exemplo é um trabalho simples de limpeza paramétrica (um tipo de computação intrinsecamente paralela).</span><span class="sxs-lookup"><span data-stu-id="bf534-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="bf534-258">Este exemplo executa subtarefas que adicionar um tooitself inteiro usando Olá **set /a** comando.</span><span class="sxs-lookup"><span data-stu-id="bf534-258">This example runs subtasks that add an integer tooitself by using hello **set /a** command.</span></span> <span data-ttu-id="bf534-259">Todos os nós de saudação em cluster Olá contribuem toofinishing Olá subtarefas para inteiros de 1 too100.</span><span class="sxs-lookup"><span data-stu-id="bf534-259">All hello nodes in hello cluster contribute toofinishing hello subtasks for integers from 1 too100.</span></span>

1. <span data-ttu-id="bf534-260">No Gerenciador de Cluster HPC, clique em **Gerenciamento de Trabalho** > **Novo Trabalho de Limpeza Paramétrica**.</span><span class="sxs-lookup"><span data-stu-id="bf534-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span></span>
   
    ![Novo trabalho][test_job1]

2. <span data-ttu-id="bf534-262">Em Olá **novo trabalho de varredura paramétrica** na caixa **linha de comando**, tipo `set /a *+*` (substituindo a linha de comando do saudação padrão que é exibido).</span><span class="sxs-lookup"><span data-stu-id="bf534-262">In hello **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting hello default command line that appears).</span></span> <span data-ttu-id="bf534-263">Deixe valores padrão para Olá restantes configurações e, em seguida, clique em **enviar** toosubmit trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="bf534-263">Leave default values for hello remaining settings, and then click **Submit** toosubmit hello job.</span></span>
   
    ![Limpeza paramétrica][param_sweep1]

3. <span data-ttu-id="bf534-265">Quando o trabalho de saudação é concluído, clique duas vezes em Olá **minha tarefa varredura** trabalho.</span><span class="sxs-lookup"><span data-stu-id="bf534-265">When hello job is finished, double-click hello **My Sweep Task** job.</span></span>

4. <span data-ttu-id="bf534-266">Clique em **exibir tarefas**e, em seguida, clique em uma saída de hello calculado tooview subtarefa dessa subtarefa.</span><span class="sxs-lookup"><span data-stu-id="bf534-266">Click **View Tasks**, and then click a subtask tooview hello calculated output of that subtask.</span></span>
   
    ![Resultados da tarefa][view_job361]

5. <span data-ttu-id="bf534-268">toosee qual nó executada cálculo Olá que subtarefa, clique em **alocada nós**.</span><span class="sxs-lookup"><span data-stu-id="bf534-268">toosee which node performed hello calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="bf534-269">(Seu cluster pode mostrar um nome de nó diferente).</span><span class="sxs-lookup"><span data-stu-id="bf534-269">(Your cluster might show a different node name.)</span></span>
   
    ![Resultados da tarefa][view_job362]

## <a name="stop-hello-azure-nodes"></a><span data-ttu-id="bf534-271">Parar Olá nós do Azure</span><span class="sxs-lookup"><span data-stu-id="bf534-271">Stop hello Azure nodes</span></span>
<span data-ttu-id="bf534-272">Depois que você experimente cluster Olá, pare Olá nós do Azure tooavoid desnecessárias cobra tooyour conta.</span><span class="sxs-lookup"><span data-stu-id="bf534-272">After you try out hello cluster, stop hello Azure nodes tooavoid unnecessary charges tooyour account.</span></span> <span data-ttu-id="bf534-273">Esta etapa interrompe o serviço de nuvem hello e remove Olá instâncias de função do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf534-273">This step stops hello cloud service and removes hello Azure role instances.</span></span>

1. <span data-ttu-id="bf534-274">No Gerenciador de Cluster HPC, em **Gerenciamento de Nós** (chamado de **Gerenciamento de Recursos** em versões anteriores do HPC Pack), selecione ambos os nós do Azure.</span><span class="sxs-lookup"><span data-stu-id="bf534-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="bf534-275">Em seguida, clique em **Parar**.</span><span class="sxs-lookup"><span data-stu-id="bf534-275">Then, click **Stop**.</span></span>
   
    ![Parar os nós][stop_node1]

2. <span data-ttu-id="bf534-277">Em Olá **nós do Windows Azure parar** caixa de diálogo, clique em **parar**.</span><span class="sxs-lookup"><span data-stu-id="bf534-277">In hello **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span> 
   
3. <span data-ttu-id="bf534-278">nós Olá transição toohello **parando** estado.</span><span class="sxs-lookup"><span data-stu-id="bf534-278">hello nodes transition toohello **Stopping** state.</span></span> <span data-ttu-id="bf534-279">Depois de alguns minutos, o Gerenciador de Cluster de HPC mostra que nós Olá **não implantado**.</span><span class="sxs-lookup"><span data-stu-id="bf534-279">After a few minutes, HPC Cluster Manager shows that hello nodes are **Not-Deployed**.</span></span>
   
    ![Nós não implantados][stop_node4]

4. <span data-ttu-id="bf534-281">Olá de tooconfirm instâncias de função hello são não mais em execução no Azure, no portal, Azure, clique em **(clássico) de serviços de nuvem** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="bf534-281">tooconfirm that hello role instances are no longer running in Azure, in hello Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span></span> <span data-ttu-id="bf534-282">Não há instâncias são implantadas no ambiente de produção de hello.</span><span class="sxs-lookup"><span data-stu-id="bf534-282">No instances are deployed in hello production environment.</span></span> 
   
    <span data-ttu-id="bf534-283">Isso conclui o tutorial hello.</span><span class="sxs-lookup"><span data-stu-id="bf534-283">This completes hello tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf534-284">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bf534-284">Next steps</span></span>
* <span data-ttu-id="bf534-285">Explorar a documentação de saudação do [HPC Pack](https://technet.microsoft.com/library/cc514029).</span><span class="sxs-lookup"><span data-stu-id="bf534-285">Explore hello documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="bf534-286">Consulte tooset a uma implantação de cluster de HPC Pack em maior escala, híbrida [disparar tooAzure instâncias de função de trabalho com o Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="bf534-286">tooset up a hybrid HPC Pack cluster deployment at greater scale, see [Burst tooAzure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="bf534-287">Para outra maneiras toocreate um cluster de HPC Pack no Azure, incluindo modelos do Azure Resource Manager, consulte [opções de cluster HPC com Microsoft HPC Pack no Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bf534-287">For other ways toocreate an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
