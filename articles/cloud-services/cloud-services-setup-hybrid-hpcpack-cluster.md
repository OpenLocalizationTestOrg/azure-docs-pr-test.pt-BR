---
title: "Configurar um cluster do HPC Pack híbrido no Azure | Microsoft Docs"
description: "Aprenda a usar o Microsoft HPC Pack e o Azure para configurar um cluster de computação de alto desempenho (HPC) híbrido e pequeno"
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
ms.openlocfilehash: f6dc9657e64160be1e68a7356863b53131e9b3c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="4fbcd-103">Configurar um cluster HPC (computação de alto desempenho) híbrido com nós de computação do Azure sob demanda e o Microsoft HPC Pack</span><span class="sxs-lookup"><span data-stu-id="4fbcd-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="4fbcd-104">Use o Microsoft HPC Pack 2012 R2 e o Azure para configurar um cluster HPC (computação de alto desempenho) híbrido e pequeno.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-104">Use Microsoft HPC Pack 2012 R2 and Azure to set up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="4fbcd-105">O cluster mostrado neste artigo é composto por um nó de cabeçalho do HPC Pack local e alguns nós de computação que você implanta sob demanda em um serviço de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-105">The cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span></span> <span data-ttu-id="4fbcd-106">É possível executar trabalhos de computação no cluster híbrido.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-106">You can then run compute jobs on the hybrid cluster.</span></span>

![Cluster híbrido de HPC][Overview] 

<span data-ttu-id="4fbcd-108">Este tutorial mostra uma abordagem, às vezes chamada de cluster "de estouro para a nuvem", para usar os recursos de computação dimensionáveis e sob demanda do Azure para executar aplicativos com uso intensivo de computação.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-108">This tutorial shows one approach, sometimes called cluster "burst to the cloud," to use scalable, on-demand Azure resources to run compute-intensive applications.</span></span>

<span data-ttu-id="4fbcd-109">Este tutorial não pressupõe nenhuma experiência anterior com clusters de cálculo ou com o HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span></span> <span data-ttu-id="4fbcd-110">Ele destina-se somente para ajudá-lo a implantar um cluster híbrido de cálculo de forma rápida para fins de demonstração.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-110">It is intended only to help you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="4fbcd-111">Para obter as considerações e as etapas para implantar um cluster híbrido do HPC Pack em uma escala maior em um ambiente de produção, ou para usar o HCP Pack 2016, confira as [diretrizes detalhadas](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="4fbcd-111">For considerations and steps to deploy a hybrid HPC Pack cluster at greater scale in a production environment, or to use HPC Pack 2016, see the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="4fbcd-112">Para ver outros cenários com o HPC Pack, incluindo a implantação de cluster automatizada nas máquinas virtuais do Azure, confira [Opções de cluster HPC com o Microsoft HPC Pack no Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4fbcd-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fbcd-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4fbcd-113">Prerequisites</span></span>
* <span data-ttu-id="4fbcd-114">**Assinatura do Azure** – Se não tiver uma, você poderá criar uma [conta gratuita](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="4fbcd-115">**Um computador local executando o Windows Server 2012 R2 ou o Windows Server 2012** – use computador como o nó de cabeçalho do cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as the head node of the HPC cluster.</span></span> <span data-ttu-id="4fbcd-116">Se você ainda não estiver executando o Windows Server, poderá baixar e instalar uma [versão de avaliação](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span><span class="sxs-lookup"><span data-stu-id="4fbcd-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="4fbcd-117">O computador deve estar ingressado a um domínio do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-117">The computer must be joined to an Active Directory domain.</span></span> <span data-ttu-id="4fbcd-118">Para fins de teste, você pode configurar o computador do nó de cabeçalho como um controlador de domínio.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-118">For test purposes, you can configure the head node computer as a domain controller.</span></span> <span data-ttu-id="4fbcd-119">Para adicionar a função de servidor dos Active Directory Domain Services e promover o computador do nó de cabeçalho como um controlador de domínio, consulte a documentação do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-119">To add the Active Directory Domain Services server role and promote the head node computer as a domain controller, see the documentation for Windows Server.</span></span>
  * <span data-ttu-id="4fbcd-120">Para oferecer suporte ao HPC Pack, o sistema operacional deve ser instalado em um desses idiomas: inglês, japonês ou chinês (simplificado).</span><span class="sxs-lookup"><span data-stu-id="4fbcd-120">To support HPC Pack, the operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="4fbcd-121">Verifique se as atualizações importantes e críticas foram instaladas.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-121">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="4fbcd-122">**HPC Pack 2012 R2** - [Baixe](http://go.microsoft.com/fwlink/p/?linkid=328024) o pacote de instalação correspondente à versão gratuita mais recente e copie os arquivos para o computador do nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) the installation package for the latest version free of charge and copy the files to the head node computer.</span></span> <span data-ttu-id="4fbcd-123">Escolha os arquivos de instalação no mesmo idioma da sua instalação do Windows Server.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-123">Choose installation files in the same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="4fbcd-124">Se você quiser usar o HPC Pack 2016 em vez do HPC Pack 2012 R2, será necessária uma configuração adicional.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-124">If you want to use HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="4fbcd-125">Confira as [orientações detalhadas](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="4fbcd-125">See the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="4fbcd-126">**Conta de domínio** - Esta conta deve ser configurada com as permissões de Administrador local no nó de cabeçalho para instalar o HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-126">**Domain account** - This account must be configured with local Administrator permissions on the head node to install HPC Pack.</span></span>
* <span data-ttu-id="4fbcd-127">**Conectividade TCP na porta 443** do nó de cabeçalho para o Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-127">**TCP connectivity on port 443** from the head node to Azure.</span></span>

## <a name="install-hpc-pack-on-the-head-node"></a><span data-ttu-id="4fbcd-128">Instalar o HPC Pack no nó de cabeça</span><span class="sxs-lookup"><span data-stu-id="4fbcd-128">Install HPC Pack on the head node</span></span>
<span data-ttu-id="4fbcd-129">Primeiro, instale o Microsoft HPC Pack em seu computador local executando o Windows Server.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span></span> <span data-ttu-id="4fbcd-130">Esse computador se tornará o nó de cabeçalho do cluster.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-130">This computer becomes the head node of the cluster.</span></span>

1. <span data-ttu-id="4fbcd-131">Faça login no nó de cabeça usando uma conta de domínio que tenha permissões de Administrador local.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-131">Log on to the head node by using a domain account that has local Administrator permissions.</span></span>

2. <span data-ttu-id="4fbcd-132">Inicie o Assistente de Instalação do HPC Pack executando Setup.exe nos arquivos de instalação do HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-132">Start the HPC Pack Installation Wizard by running Setup.exe from the HPC Pack installation files.</span></span>

3. <span data-ttu-id="4fbcd-133">Na tela **Instalação do HPC Pack 2012 R2**, clique em **Nova instalação ou adicionar novos recursos a uma instalação existente**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-133">On the **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features to an existing installation**.</span></span>

    ![Instalação do HPC Pack 2012][install_hpc1]

4. <span data-ttu-id="4fbcd-135">Na **página do Contrato de Usuário do Software da Microsoft**, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-135">On the **Microsoft Software User Agreement page**, click **Next**.</span></span>

5. <span data-ttu-id="4fbcd-136">Na página **Selecionar Tipo de Instalação**, clique em **Criar um novo cluster de HPC, criando um nó de cabeça** e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-136">On the **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>

6. <span data-ttu-id="4fbcd-137">O assistente executa vários testes de pré-instalação.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-137">The wizard runs several pre-installation tests.</span></span> <span data-ttu-id="4fbcd-138">Clique em **Avançar** on the **Regras de instalação** se todos os testes forem aprovados.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-138">Click **Next** on the **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="4fbcd-139">Caso contrário, examine as informações fornecidas e faça as alterações necessárias em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-139">Otherwise, review the information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="4fbcd-140">Execute os testes novamente ou se necessário inicie o Assistente de Instalação novamente.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-140">Then run the tests again or if necessary start the Installation Wizard again.</span></span>
7. <span data-ttu-id="4fbcd-141">Na página **Configuração do BD de HPC**, certifique-se de que **Nó de cabeça** esteja selecionado para todos os bancos de dados de HPC e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-141">On the **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span> 

    ![Configuração do BD][install_hpc4]

8. <span data-ttu-id="4fbcd-143">Aceite as seleções padrão nas páginas restantes do assistente.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-143">Accept default selections on the remaining pages of the wizard.</span></span> <span data-ttu-id="4fbcd-144">Na página **Instalar Componentes necessários**, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-144">On the **Install Required Components** page, click **Install**.</span></span>
   
    ![Instalar][install_hpc6]

9. <span data-ttu-id="4fbcd-146">Após a conclusão da instalação, desmarque **Iniciar o Gerenciador de Cluster de HPC** e, em seguida, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-146">After the installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="4fbcd-147">(Você iniciará o Gerenciador de Cluster de HPC em uma etapa posterior.)</span><span class="sxs-lookup"><span data-stu-id="4fbcd-147">(You start HPC Cluster Manager in a later step.)</span></span>
   
    ![Concluir][install_hpc7]

## <a name="prepare-the-azure-subscription"></a><span data-ttu-id="4fbcd-149">Preparar a assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="4fbcd-149">Prepare the Azure subscription</span></span>
<span data-ttu-id="4fbcd-150">Realize as etapas a seguir no [portal do Azure](https://portal.azure.com) com sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-150">Perform the following steps in the [Azure portal](https://portal.azure.com) with your Azure subscription.</span></span> <span data-ttu-id="4fbcd-151">Após concluir essas etapas, você pode implantar os nós do Azure no nó de cabeçalho local.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-151">After completing these steps, you can deploy Azure nodes from the on-premises head node.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="4fbcd-152">Além disso, tome nota de sua ID de assinatura do Azure, que será necessária posteriormente.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-152">Also make a note of your Azure subscription ID, which you need later.</span></span> <span data-ttu-id="4fbcd-153">Encontre a ID em **Assinaturas** no portal.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-153">Find the ID in **Subscriptions** in the portal.</span></span>
  > 

### <a name="upload-the-default-management-certificate"></a><span data-ttu-id="4fbcd-154">Carregue o certificado de gerenciamento padrão</span><span class="sxs-lookup"><span data-stu-id="4fbcd-154">Upload the default management certificate</span></span>
<span data-ttu-id="4fbcd-155">O HPC Pack instala um certificado autoassinado no nó de cabeça, chamado de Certificado de gerenciamento padrão de HPC no Azure da Microsoft, que pode ser carregado como um certificado de gerenciamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-155">HPC Pack installs a self-signed certificate on the head node, called the Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="4fbcd-156">Esse certificado é fornecido para implantações de teste e de prova de conceito para proteger a conexão entre o nó de cabeçalho e o Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-156">This certificate is provided for testing and proof-of-concept deployments to secure the connection between the head node and Azure.</span></span>

1. <span data-ttu-id="4fbcd-157">No computador do nó de cabeçalho, entre no [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4fbcd-157">From the head node computer, sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="4fbcd-158">Clique em **Assinaturas** > *nome_da_assinatura*.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-158">Click **Subscriptions** > *your_subscription_name*.</span></span>

3. <span data-ttu-id="4fbcd-159">Clique em **Certificados de gerenciamento** > **Carregar**.4.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-159">Click **Management certificates** > **Upload**.4.</span></span> <span data-ttu-id="4fbcd-160">Procure no nó de cabeçalho pelo arquivo C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-160">Browse on the head node for the file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="4fbcd-161">Em seguida, clique em **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-161">Then, click **Upload**.</span></span>

   
<span data-ttu-id="4fbcd-162">O certificado de **Gerenciamento padrão de HPC no Azure** aparece na lista de certificados de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-162">The **Default HPC Azure Management** certificate appears in the list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="4fbcd-163">Criar um serviço de nuvem do Azure</span><span class="sxs-lookup"><span data-stu-id="4fbcd-163">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="4fbcd-164">Para melhor desempenho, crie o serviço de nuvem e a conta de armazenamento (em uma etapa posterior) na mesma região geográfica.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-164">For best performance, create the cloud service and the storage account (in a later step) in the same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="4fbcd-165">No portal, clique em **Serviços de nuvem (clássico)** > **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-165">In the portal, click **Cloud services (classic)** > **+Add**.</span></span>

2.  <span data-ttu-id="4fbcd-166">Digite um nome DNS para o serviço, escolha um grupo de recursos e um local e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-166">Type a DNS name for the service, choose a resource group and a location, and then click **Create**.</span></span>


### <a name="create-an-azure-storage-account"></a><span data-ttu-id="4fbcd-167">Criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="4fbcd-167">Create an Azure storage account</span></span>
1. <span data-ttu-id="4fbcd-168">No portal, clique em **Contas de armazenamento (clássico)** > **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-168">In the portal, click **Storage accounts (classic)** > **+Add**.</span></span>

2. <span data-ttu-id="4fbcd-169">Digite um nome para a conta e, em seguida, selecione o modelo de implantação **Clássico**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-169">Type a name for the account, and select the **Classic** deployment model.</span></span>

3. <span data-ttu-id="4fbcd-170">Escolha um grupo de recursos e um local e deixe as outras configurações com os valores padrão.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-170">Choose a resource group and a location, and leave other settings at default values.</span></span> <span data-ttu-id="4fbcd-171">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-171">Then click **Create**.</span></span>

## <a name="configure-the-head-node"></a><span data-ttu-id="4fbcd-172">Configurar o nó de cabeça</span><span class="sxs-lookup"><span data-stu-id="4fbcd-172">Configure the head node</span></span>
<span data-ttu-id="4fbcd-173">Para usar o Gerenciador de Cluster de HPC para implantar nós do Azure e para enviar trabalhos, primeiro realize algumas etapas de configuração necessárias do cluster.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-173">To use HPC Cluster Manager to deploy Azure nodes and to submit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="4fbcd-174">No nó de cabeça, inicie o Gerenciador de Cluster de HPC.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-174">On the head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="4fbcd-175">Se a caixa de diálogo **Selecionar Nó de Cabeça** for exibida, clique em **Computador Local**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-175">If the **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="4fbcd-176">A **Lista de tarefas de implantação** é exibida.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-176">The **Deployment To-do List** appears.</span></span>

2. <span data-ttu-id="4fbcd-177">Em **Tarefas de implantação necessárias**, clique em **Configurar sua rede**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-177">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![Configurar Rede][config_hpc2]

3. <span data-ttu-id="4fbcd-179">No Assistente de Configuração de Rede, selecione **Todos os nós somente em uma rede corporativa** (Topologia 5).</span><span class="sxs-lookup"><span data-stu-id="4fbcd-179">In the Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span> <span data-ttu-id="4fbcd-180">Essa configuração de rede é a mais simples para fins de demonstração.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-180">This network configuration is the simplest for demonstration purposes.</span></span>
   
    ![Topologia 5][config_hpc3]
   
4. <span data-ttu-id="4fbcd-182">Clique em **Avançar** para aceitar os valores padrão nas páginas restantes do assistente.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-182">Click **Next** to accept default values on the remaining pages of the wizard.</span></span> <span data-ttu-id="4fbcd-183">Em seguida, na guia **Examinar**, clique em **Configurar** para concluir a configuração de rede.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-183">Then, on the **Review** tab, click **Configure** to complete the network configuration.</span></span>

5. <span data-ttu-id="4fbcd-184">Na **Lista de tarefas de implantação**, clique em **Fornecer credenciais de instalação**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-184">In the **Deployment To-do List**, click **Provide installation credentials**.</span></span>

6. <span data-ttu-id="4fbcd-185">Na caixa de diálogo **Credenciais de instalação** , digite as credenciais da conta de domínio usada para instalar o HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-185">In the **Installation Credentials** dialog box, type the credentials of the domain account that you used to install HPC Pack.</span></span> <span data-ttu-id="4fbcd-186">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-186">Then click **OK**.</span></span> 
   
    ![Credenciais de instalação][config_hpc6]
   
7. <span data-ttu-id="4fbcd-188">Na **Lista de tarefas de implantação**, clique em **Configurar a nomeação dos novos nós**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-188">In the **Deployment To-do List**, click **Configure the naming of new nodes**.</span></span>

8. <span data-ttu-id="4fbcd-189">Na caixa de diálogo **Especificar Série de Nomeação de Nós**, aceite a série de nomeação padrão e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-189">In the **Specify Node Naming Series** dialog box, accept the default naming series and click **OK**.</span></span> <span data-ttu-id="4fbcd-190">Conclua esta etapa mesmo que os nós do Azure que você adicionar neste tutorial sejam nomeados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-190">Complete this step even though the Azure nodes you add in this tutorial are named automatically.</span></span>
   
    ![Nomeação de nós][config_hpc8]
   
9. <span data-ttu-id="4fbcd-192">Na **Lista de tarefas de implantação**, clique em **Criar um modelo de nó**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-192">In the **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="4fbcd-193">Posteriormente no tutorial, você usará o modelo do nó para adicionar nós do Azure ao cluster.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-193">Later in the tutorial, you use the node template to add Azure nodes to the cluster.</span></span>

10. <span data-ttu-id="4fbcd-194">Em Criar Assistente do modelo de nó, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4fbcd-194">In the Create Node Template Wizard, do the following:</span></span>
    
    <span data-ttu-id="4fbcd-195">a.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-195">a.</span></span> <span data-ttu-id="4fbcd-196">Na página **Escolher Tipo de Modelo de Nó**, clique em **Modelo de nó do Microsoft Azure** e, em seguida, clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-196">On the **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span></span>
    
    ![Modelo do nó][config_hpc10]
    
    <span data-ttu-id="4fbcd-198">b.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-198">b.</span></span> <span data-ttu-id="4fbcd-199">Clique em **Avançar** para aceitar o nome do modelo padrão.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-199">Click **Next** to accept the default template name.</span></span>
    
    <span data-ttu-id="4fbcd-200">c.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-200">c.</span></span> <span data-ttu-id="4fbcd-201">Na página **Fornecer Informações sobre Assinatura**, insira sua ID de Assinatura do Azure (disponível em suas informações de conta do Azure).</span><span class="sxs-lookup"><span data-stu-id="4fbcd-201">On the **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="4fbcd-202">Em seguida, em **Certificado de gerenciamento**, procure por **Gerenciamento do Azure Padrão no Microsoft HPC.**</span><span class="sxs-lookup"><span data-stu-id="4fbcd-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span></span> <span data-ttu-id="4fbcd-203">Em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-203">Then click **Next**.</span></span>
    
    ![Modelo do nó][config_hpc12]
    
    <span data-ttu-id="4fbcd-205">d.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-205">d.</span></span> <span data-ttu-id="4fbcd-206">Na página **Fornecer informações sobre serviço** , selecione o serviço de nuvem e a conta de armazenamento criados na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-206">On the **Provide Service Information** page, select the cloud service and the storage account that you created in a previous step.</span></span> <span data-ttu-id="4fbcd-207">Em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-207">Then click **Next**.</span></span>
    
    ![Modelo do nó][config_hpc13]
    
    <span data-ttu-id="4fbcd-209">e.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-209">e.</span></span> <span data-ttu-id="4fbcd-210">Clique em **Avançar** para aceitar os valores padrão nas páginas restantes do assistente.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-210">Click **Next** to accept default values on the remaining pages of the wizard.</span></span> <span data-ttu-id="4fbcd-211">Em seguida, na guia **Examinar**, clique em **Criar** para criar o modelo de nó.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-211">Then, on the **Review** tab, click **Create** to create the node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4fbcd-212">Por padrão, o modelo de nó do Azure inclui configurações para iniciar (provisionar) e interromper os nós manualmente, usando o Gerenciador de Cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-212">By default, the Azure node template includes settings for you to start (provision) and stop the nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="4fbcd-213">Como opção, você também pode configurar uma agenda para iniciar e interromper os nós do Azure automaticamente.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-213">You can optionally configure a schedule to start and stop the Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-to-the-cluster"></a><span data-ttu-id="4fbcd-214">Adicionar nós do Azure ao cluster</span><span class="sxs-lookup"><span data-stu-id="4fbcd-214">Add Azure nodes to the cluster</span></span>
<span data-ttu-id="4fbcd-215">Agora, use o modelo do nó para adicionar nós do Azure ao cluster.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-215">Now use the node template to add Azure nodes to the cluster.</span></span> <span data-ttu-id="4fbcd-216">Adicionar os nós ao cluster armazena suas informações de configuração para que você possa iniciá-los (provisioná-los) a qualquer momento no serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-216">Adding the nodes to the cluster stores their configuration information so that you can start (provision) them at any time in the cloud service.</span></span> <span data-ttu-id="4fbcd-217">Sua assinatura é cobrada pelos nós do Azure somente depois que as instâncias estiverem sendo executadas no serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-217">Your subscription only gets charged for Azure nodes after the instances are running in the cloud service.</span></span>

<span data-ttu-id="4fbcd-218">Siga estas etapas para adicionar dois nós pequenos.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-218">Follow these steps to add two Small nodes.</span></span>

1. <span data-ttu-id="4fbcd-219">No Gerenciador de Cluster HPC, clique em **Gerenciamento de Nós** (chamado de **Gerenciamento de Recursos** em versões atuais do HPC Pack) > **Adicionar Nó**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span></span>
   
    ![Adicionar Nó][add_node1]

2. <span data-ttu-id="4fbcd-221">No Assistente para Adicionar Nós, na página **Selecionar Método de Implantação**, clique em **Adicionar nós do Windows Azure** e em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-221">In the Add Node Wizard, on the **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Adicionar nó do Azure][add_node1_1]

3. <span data-ttu-id="4fbcd-223">Na página **Especificar Novos Nós**, selecione o modelo do nó do Azure criado anteriormente (chamado por padrão de **Modelo de Nós do Azure Padrão**).</span><span class="sxs-lookup"><span data-stu-id="4fbcd-223">On the **Specify New Nodes** page, select the Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="4fbcd-224">Em seguida, especifique **2** nós de tamanho **Pequeno** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![Especificar nós][add_node2]
   
4. <span data-ttu-id="4fbcd-226">Na página de **Conclusão do Assistente de Adição de Nós**, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-226">On the **Completing the Add Node Wizard** page, click **Finish**.</span></span>
    
     <span data-ttu-id="4fbcd-227">Dois nós do Azure, chamados **AzureCN-0001** e **AzureCN-0002**, agora são exibidos no Gerenciador de Cluster de HPC.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="4fbcd-228">Ambos estão no estado **Não Implantado** .</span><span class="sxs-lookup"><span data-stu-id="4fbcd-228">Both are in the **Not-Deployed** state.</span></span>
   
    ![Nós adicionados][add_node3]

## <a name="start-the-azure-nodes"></a><span data-ttu-id="4fbcd-230">Iniciar os nós do Azure</span><span class="sxs-lookup"><span data-stu-id="4fbcd-230">Start the Azure nodes</span></span>
<span data-ttu-id="4fbcd-231">Quando desejar usar os recursos de cluster no Azure, use o Gerenciador de Cluster de HPC para iniciar (provisionar) os nós no Azure e colocá-los on-line.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-231">When you want to use the cluster resources in Azure, use HPC Cluster Manager to start (provision) the Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="4fbcd-232">No Gerenciador de Cluster HPC, clique em **Gerenciamento de Nós** (chamado de **Gerenciamento de Recursos** em versões atuais do HPC Pack) e selecione os nós do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select the Azure nodes.</span></span>

2. <span data-ttu-id="4fbcd-233">Clique em **Iniciar** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-233">Click **Start**, and then click **OK**.</span></span>
   
   ![Iniciar nós][add_node4]
   
    <span data-ttu-id="4fbcd-235">Os nós farão a transição para o **Provisionamento** .</span><span class="sxs-lookup"><span data-stu-id="4fbcd-235">The nodes transition to the **Provisioning** state.</span></span> <span data-ttu-id="4fbcd-236">Exiba o log de provisionamento para controlar o progresso do provisionamento.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-236">View the provisioning log to track the provisioning progress.</span></span>
   
    ![Provisionar nós][add_node6]

3. <span data-ttu-id="4fbcd-238">Depois de alguns minutos, os nós do Azure concluirão o provisionamento e estarão no estado **Off-line** .</span><span class="sxs-lookup"><span data-stu-id="4fbcd-238">After a few minutes, the Azure nodes finish provisioning and are in the **Offline** state.</span></span> <span data-ttu-id="4fbcd-239">Nesse estado, as instâncias de função estão em execução, mas ainda não podem aceitar trabalhos de cluster.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-239">In this state, the role instances are running but cannot yet accept cluster jobs.</span></span>

4. <span data-ttu-id="4fbcd-240">Para confirmar se as instâncias de função estão sendo executadas, no portal do Azure, clique em **Serviços de Nuvem (clássico)** > *nome_do_serviço_de_nuvem*.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-240">To confirm that the role instances are running, in the Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span></span>
   
   <span data-ttu-id="4fbcd-241">Você deverá ver duas instâncias (nós) de **HpcWorkerRole** em execução no serviço.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-241">You should see two **HpcWorkerRole** instances (nodes) running in the service.</span></span> <span data-ttu-id="4fbcd-242">O HPC Pack implanta automaticamente duas instâncias **HpcProxy** (de tamanho Médio) para manipular as comunicações entre o nó de cabeça e o Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) to handle communication between the head node and Azure.</span></span>

   ![Executando instâncias][view_instances1]

5. <span data-ttu-id="4fbcd-244">Para colocar os nós do Azure on-line para executar trabalhos de cluster, selecione os nós, clique com o botão direito e clique em **Colocar on-line**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-244">To bring the Azure nodes online to run cluster jobs, select the nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![Nós off-line][add_node7]
   
    <span data-ttu-id="4fbcd-246">O Gerenciador de Cluster de HPC indica que os nós estão no estado **On-line** .</span><span class="sxs-lookup"><span data-stu-id="4fbcd-246">HPC Cluster Manager indicates that the nodes are in the **Online** state.</span></span>

## <a name="run-a-command-across-the-cluster"></a><span data-ttu-id="4fbcd-247">Executar um comando no cluster</span><span class="sxs-lookup"><span data-stu-id="4fbcd-247">Run a command across the cluster</span></span>
<span data-ttu-id="4fbcd-248">Para verificar a instalação, use o comando **clusrun** do HPC Pack para executar um comando ou aplicativo em um ou mais nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-248">To check the installation, use the HPC Pack **clusrun** command to run a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="4fbcd-249">Como um exemplo simples, use **clusrun** para obter a configuração de IP dos nós do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-249">As a simple example, use **clusrun** to get the IP configuration of the Azure nodes.</span></span>

1. <span data-ttu-id="4fbcd-250">No nó de cabeçalho, abra um prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-250">On the head node, open a command prompt as an administrator.</span></span>

2. <span data-ttu-id="4fbcd-251">Digite o seguinte comando: </span><span class="sxs-lookup"><span data-stu-id="4fbcd-251">Type the following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`

3. <span data-ttu-id="4fbcd-252">Se solicitado, insira sua senha de administrador de cluster.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-252">If prompted, enter your cluster administrator password.</span></span> <span data-ttu-id="4fbcd-253">Você deverá ver uma saída de comando semelhante à seguinte.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-253">You should see command output similar to the following.</span></span>
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="4fbcd-255">Executar um trabalho de teste</span><span class="sxs-lookup"><span data-stu-id="4fbcd-255">Run a test job</span></span>
<span data-ttu-id="4fbcd-256">Você pode enviar um trabalho de teste que é executado no cluster híbrido.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-256">Now submit a test job that runs on the hybrid cluster.</span></span> <span data-ttu-id="4fbcd-257">Este exemplo é um trabalho simples de limpeza paramétrica (um tipo de computação intrinsecamente paralela).</span><span class="sxs-lookup"><span data-stu-id="4fbcd-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="4fbcd-258">Este exemplo executa as subtarefas que adicionam um número inteiro a si mesmo usando o comando **set /a** .</span><span class="sxs-lookup"><span data-stu-id="4fbcd-258">This example runs subtasks that add an integer to itself by using the **set /a** command.</span></span> <span data-ttu-id="4fbcd-259">Todos os nós no cluster contribuem para concluir as subtarefas para números inteiros de 1 a 100.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-259">All the nodes in the cluster contribute to finishing the subtasks for integers from 1 to 100.</span></span>

1. <span data-ttu-id="4fbcd-260">No Gerenciador de Cluster HPC, clique em **Gerenciamento de Trabalho** > **Novo Trabalho de Limpeza Paramétrica**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span></span>
   
    ![Novo trabalho][test_job1]

2. <span data-ttu-id="4fbcd-262">Na caixa de diálogo **Novo Trabalho de Limpeza Paramétrica** em **Linha de Comando**, digite `set /a *+*` (substituindo a linha de comando padrão que é exibida).</span><span class="sxs-lookup"><span data-stu-id="4fbcd-262">In the **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting the default command line that appears).</span></span> <span data-ttu-id="4fbcd-263">Deixe os valores padrão para o restante das configurações e clique em **Enviar** para enviar o trabalho.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-263">Leave default values for the remaining settings, and then click **Submit** to submit the job.</span></span>
   
    ![Limpeza paramétrica][param_sweep1]

3. <span data-ttu-id="4fbcd-265">Quando o trabalho estiver concluído, clique duas vezes no trabalho **Minhas tarefas de limpeza** .</span><span class="sxs-lookup"><span data-stu-id="4fbcd-265">When the job is finished, double-click the **My Sweep Task** job.</span></span>

4. <span data-ttu-id="4fbcd-266">Clique em **Exibir tarefas**e em uma subtarefa para exibir a saída calculada dessa subtarefa.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-266">Click **View Tasks**, and then click a subtask to view the calculated output of that subtask.</span></span>
   
    ![Resultados da tarefa][view_job361]

5. <span data-ttu-id="4fbcd-268">Para visualizar qual nó executou o cálculo para dessa subtarefa, clique em **Nós alocados**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-268">To see which node performed the calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="4fbcd-269">(Seu cluster pode mostrar um nome de nó diferente).</span><span class="sxs-lookup"><span data-stu-id="4fbcd-269">(Your cluster might show a different node name.)</span></span>
   
    ![Resultados da tarefa][view_job362]

## <a name="stop-the-azure-nodes"></a><span data-ttu-id="4fbcd-271">Parar os nós do Azure</span><span class="sxs-lookup"><span data-stu-id="4fbcd-271">Stop the Azure nodes</span></span>
<span data-ttu-id="4fbcd-272">Depois de testar o cluster, interrompa os nós do Azure para evitar cobranças desnecessárias em sua conta.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-272">After you try out the cluster, stop the Azure nodes to avoid unnecessary charges to your account.</span></span> <span data-ttu-id="4fbcd-273">Essa etapa interromperá o serviço de nuvem e removerá as instâncias de função do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-273">This step stops the cloud service and removes the Azure role instances.</span></span>

1. <span data-ttu-id="4fbcd-274">No Gerenciador de Cluster HPC, em **Gerenciamento de Nós** (chamado de **Gerenciamento de Recursos** em versões anteriores do HPC Pack), selecione ambos os nós do Azure.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="4fbcd-275">Em seguida, clique em **Parar**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-275">Then, click **Stop**.</span></span>
   
    ![Parar os nós][stop_node1]

2. <span data-ttu-id="4fbcd-277">Na caixa de diálogo **Parar nós do Windows Azure**, clique em **Parar**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-277">In the **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span> 
   
3. <span data-ttu-id="4fbcd-278">Os nós farão a transição para a **Parada** .</span><span class="sxs-lookup"><span data-stu-id="4fbcd-278">The nodes transition to the **Stopping** state.</span></span> <span data-ttu-id="4fbcd-279">Depois de alguns minutos, o Gerenciador de Cluster de HPC mostra o estado dos nós como **Não implantados**.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-279">After a few minutes, HPC Cluster Manager shows that the nodes are **Not-Deployed**.</span></span>
   
    ![Nós não implantados][stop_node4]

4. <span data-ttu-id="4fbcd-281">Para confirmar que as instâncias de função não estão mais sendo executadas no Azure, no portal do Azure, clique em **Serviços de nuvem (clássico)** > *nome_do_serviço_de_nuvem*.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-281">To confirm that the role instances are no longer running in Azure, in the Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span></span> <span data-ttu-id="4fbcd-282">Nenhuma instância é implantada no ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-282">No instances are deployed in the production environment.</span></span> 
   
    <span data-ttu-id="4fbcd-283">Assim, concluímos o tutorial.</span><span class="sxs-lookup"><span data-stu-id="4fbcd-283">This completes the tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fbcd-284">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4fbcd-284">Next steps</span></span>
* <span data-ttu-id="4fbcd-285">Explore a documentação do [HPC Pack](https://technet.microsoft.com/library/cc514029).</span><span class="sxs-lookup"><span data-stu-id="4fbcd-285">Explore the documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="4fbcd-286">Para configurar uma implantação de cluster de HPC Pack hibrida em uma escala maior, consulte [Intermitência para Instâncias de Função de Trabalho do Azure com Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="4fbcd-286">To set up a hybrid HPC Pack cluster deployment at greater scale, see [Burst to Azure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="4fbcd-287">Para outras maneiras de criar um cluster de HPC Pack no Azure, inclusive usando modelos do Azure Resource Manager, veja [Opções de cluster HPC com Microsoft HPC Pack no Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4fbcd-287">For other ways to create an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


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
