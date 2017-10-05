---
title: "Introdução ao DSC de Automação do Azure | Microsoft Docs"
description: "Explicações e exemplos das tarefas mais comuns no DSC (Configuração de Estado Desejado) de Automação do Azure"
services: automation
documentationcenter: na
author: eslesar
manager: carmonm
editor: tysonn
ms.assetid: a3816593-70a3-403b-9a43-d5555fd2cee2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: na
ms.date: 11/21/2016
ms.author: magoedte;eslesar
ms.openlocfilehash: 8a10d961ad7c107c68b57c64ee6c88544ff8832b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="27ea0-103">Introdução ao DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="27ea0-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="27ea0-104">Este tópico explica como realizar as tarefas mais comuns com o DSC (Configuração de Estado Desejado) de Automação do Azure, como criar, importar e compilar configurações, máquinas de integração para gerenciar e exibir relatórios.</span><span class="sxs-lookup"><span data-stu-id="27ea0-104">This topic explains how to do the most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines to manage, and viewing reports.</span></span> <span data-ttu-id="27ea0-105">Para obter uma visão geral do que o DSC de Automação do Azure é, consulte [Visão geral do DSC da Automação do Azure](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="27ea0-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="27ea0-106">Para obter a documentação da DSC, consulte [Visão Geral da Configuração de Estado Desejado do Windows PowerShell](https://msdn.microsoft.com/PowerShell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="27ea0-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="27ea0-107">Este tópico fornece um guia passo a passo para usar o DSC de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="27ea0-107">This topic provides a step-by-step guide to using Azure Automation DSC.</span></span> <span data-ttu-id="27ea0-108">Se você quiser um ambiente de exemplo que já esteja configurado sem seguir as etapas descritas neste tópico, poderá usar [o seguinte modelo de ARM](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span><span class="sxs-lookup"><span data-stu-id="27ea0-108">If you want a sample environment that is already set up without following the steps described in this topic, you can use [the following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="27ea0-109">Esse modelo define um ambiente completo do DSC de Automação do Azure, incluindo uma VM do Azure que é gerenciada pelo DSC de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="27ea0-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="27ea0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="27ea0-110">Prerequisites</span></span>
<span data-ttu-id="27ea0-111">Para concluir os exemplos neste tópico, são necessários:</span><span class="sxs-lookup"><span data-stu-id="27ea0-111">To complete the examples in this topic, the following are required:</span></span>

* <span data-ttu-id="27ea0-112">Uma conta de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="27ea0-112">An Azure Automation account.</span></span> <span data-ttu-id="27ea0-113">Para obter instruções sobre como criar uma conta Executar Como de Automação do Azure, consulte [Conta Executar Como do Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="27ea0-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="27ea0-114">Uma VM do Azure Resource Manager (não clássica) executando o Windows Server 2008 R2 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="27ea0-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="27ea0-115">Para obter instruções sobre a criação de uma VM, consulte [Criar sua primeira máquina virtual do Windows no portal do Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="27ea0-115">For instructions on creating a VM, see [Create your first Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="27ea0-116">Criando uma configuração de DSC</span><span class="sxs-lookup"><span data-stu-id="27ea0-116">Creating a DSC configuration</span></span>
<span data-ttu-id="27ea0-117">Criaremos uma [configuração de DSC](https://msdn.microsoft.com/powershell/dsc/configurations) simples que garante a presença ou a ausência do WindowsFeature do **Servidor Web** (IIS), dependendo de como os nós são atribuídos.</span><span class="sxs-lookup"><span data-stu-id="27ea0-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either the presence or absence of the **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="27ea0-118">Inicie o ISE do Windows PowerShell (ou qualquer editor de texto).</span><span class="sxs-lookup"><span data-stu-id="27ea0-118">Start the Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="27ea0-119">Digite o seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="27ea0-119">Type the following text:</span></span>
   
    ```powershell
    configuration TestConfig
    {
        Node WebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Present'
                Name                 = 'Web-Server'
                IncludeAllSubFeature = $true
   
            }
        }
   
        Node NotWebServer
        {
            WindowsFeature IIS
            {
                Ensure               = 'Absent'
                Name                 = 'Web-Server'
   
            }
        }
        }
    ```
3. <span data-ttu-id="27ea0-120">Salve o arquivo como `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="27ea0-120">Save the file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="27ea0-121">Esta configuração chama um recurso em cada bloco de nó, o [recurso WindowsFeature](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), que garante a presença ou a ausência da funcionalidade **Servidor Web** .</span><span class="sxs-lookup"><span data-stu-id="27ea0-121">This configuration calls one resource in each node block, the [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either the presence or absence of the **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="27ea0-122">Importando uma configuração na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="27ea0-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="27ea0-123">Em seguida, importaremos a configuração para a conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-123">Next, we'll import the configuration into the Automation account.</span></span>

1. <span data-ttu-id="27ea0-124">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27ea0-124">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="27ea0-125">No menu Hub, clique em **Todos os recursos** , em seguida, no nome da sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-125">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="27ea0-126">Na folha **Conta de Automação**, clique em **Configurações da DSC**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-126">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="27ea0-127">Na folha **Configurações da DSC**, clique em **Adicionar uma configuração**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-127">On the **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="27ea0-128">Na folha **Importar Configuração**, navegue até o arquivo `TestConfig.ps1` em seu computador.</span><span class="sxs-lookup"><span data-stu-id="27ea0-128">On the **Import Configuration** blade, browse to the `TestConfig.ps1` file on your computer.</span></span>
   
    ![Captura de tela da folha **Importar Configuração**](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="27ea0-130">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="27ea0-131">Exibindo uma configuração na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="27ea0-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="27ea0-132">Depois de importar uma configuração, você pode vê-la no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="27ea0-132">After you have imported a configuration, you can view it in the Azure portal.</span></span>

1. <span data-ttu-id="27ea0-133">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27ea0-133">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="27ea0-134">No menu Hub, clique em **Todos os recursos** , em seguida, no nome da sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-134">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="27ea0-135">Na folha **Conta de Automação**, clique em **Configurações da DSC**</span><span class="sxs-lookup"><span data-stu-id="27ea0-135">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="27ea0-136">Na folha **Configurações da DSC**, clique em **TestConfig** (este é o nome da configuração importada no procedimento anterior).</span><span class="sxs-lookup"><span data-stu-id="27ea0-136">On the **DSC Configurations** blade, click **TestConfig** (this is the name of the configuration you imported in the previous procedure).</span></span>
5. <span data-ttu-id="27ea0-137">Na folha **Configuração do TestConfig**, clique em **Exibir fonte da configuração**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-137">On the **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Captura de tela da folha TestConfig configuration (Configuração do TestConfig)](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="27ea0-139">A folha **Fonte da Configuração do TestConfig** é aberta, exibindo o código do PowerShell para a configuração.</span><span class="sxs-lookup"><span data-stu-id="27ea0-139">A **TestConfig Configuration source** blade opens, displaying the PowerShell code for the configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="27ea0-140">Compilando uma configuração na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="27ea0-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="27ea0-141">Antes de aplicar um estado desejado a um nó, uma configuração DSC definindo esse estado deve ser compilada em uma ou mais configurações de nó (documento MOF) e colocada no servidor de pull do DSC de Automação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-141">Before you can apply a desired state to a node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on the Automation DSC Pull Server.</span></span> <span data-ttu-id="27ea0-142">Para obter uma descrição mais detalhada da compilação das configurações na DSC de Automação do Azure, consulte [Compilando as configurações na DSC de Automação do Azure](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="27ea0-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="27ea0-143">Para obter mais informações sobre a compilação das configurações, consulte [Configurações da DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span><span class="sxs-lookup"><span data-stu-id="27ea0-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="27ea0-144">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27ea0-144">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="27ea0-145">No menu Hub, clique em **Todos os recursos** , em seguida, no nome da sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-145">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="27ea0-146">Na folha **Conta de Automação**, clique em **Configurações da DSC**</span><span class="sxs-lookup"><span data-stu-id="27ea0-146">On the **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="27ea0-147">Na folha **Configurações da DSC**, clique em **TestConfig** (o nome da configuração importada anteriormente).</span><span class="sxs-lookup"><span data-stu-id="27ea0-147">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="27ea0-148">Na folha **Configuração do TestConfig**, clique em **Compilar** e **Sim**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-148">On the **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="27ea0-149">Isso inicia um trabalho de compilação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-149">This starts a compilation job.</span></span>
   
    ![Captura de tela da folha TestConfig configuration (Configuração do TestConfig) realçando o botão de compilação](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="27ea0-151">Quando você compila uma configuração na Automação do Azure, ela implanta automaticamente quaisquer MOFs de configuração de nó no servidor de pull.</span><span class="sxs-lookup"><span data-stu-id="27ea0-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs to the pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="27ea0-152">Exibindo um trabalho de compilação</span><span class="sxs-lookup"><span data-stu-id="27ea0-152">Viewing a compilation job</span></span>
<span data-ttu-id="27ea0-153">Depois de iniciar uma compilação, você pode vê-la no bloco **Trabalhos de compilação** na folha **Configuração**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-153">After you start a compilation, you can view it in the **Compilation jobs** tile in the **Configuration** blade.</span></span> <span data-ttu-id="27ea0-154">O bloco **Trabalhos de compilação** mostra os trabalhos atualmente em execução, concluídos e com falha.</span><span class="sxs-lookup"><span data-stu-id="27ea0-154">The **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="27ea0-155">Quando você abre uma folha de trabalho de compilação, ela mostra informações sobre esse trabalho, incluindo quaisquer erros ou avisos encontrados, parâmetros de entrada usados na configuração e logs de compilação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in the configuration, and compilation logs.</span></span>

1. <span data-ttu-id="27ea0-156">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27ea0-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="27ea0-157">No menu Hub, clique em **Todos os recursos** , em seguida, no nome da sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-157">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="27ea0-158">Na folha **Conta de Automação**, clique em **Configurações da DSC**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-158">On the **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="27ea0-159">Na folha **Configurações da DSC**, clique em **TestConfig** (o nome da configuração importada anteriormente).</span><span class="sxs-lookup"><span data-stu-id="27ea0-159">On the **DSC Configurations** blade, click **TestConfig** (the name of the previously imported configuration).</span></span>
5. <span data-ttu-id="27ea0-160">No bloco **Trabalhos de compilação** da folha **Configuração do TestConfig**, clique em qualquer um dos trabalhos listados.</span><span class="sxs-lookup"><span data-stu-id="27ea0-160">On the **Compilation jobs** tile of the **TestConfig Configuration** blade, click on any of the jobs listed.</span></span> <span data-ttu-id="27ea0-161">Uma folha **Trabalho de Compilação** é aberta, rotulada com a data em que o trabalho de compilação foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="27ea0-161">A **Compilation Job** blade opens, labeled with the date that the compilation job was started.</span></span>
   
    ![Captura de tela da folha Trabalho de Compilação](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="27ea0-163">Clique em qualquer bloco na folha **Trabalho de Compilação** para ver mais detalhes sobre o trabalho.</span><span class="sxs-lookup"><span data-stu-id="27ea0-163">Click on any tile in the **Compilation Job** blade to see further details about the job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="27ea0-164">Exibindo configurações de nó</span><span class="sxs-lookup"><span data-stu-id="27ea0-164">Viewing node configurations</span></span>
<span data-ttu-id="27ea0-165">A conclusão com êxito de um trabalho de compilação cria uma ou mais novas configurações de nó.</span><span class="sxs-lookup"><span data-stu-id="27ea0-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="27ea0-166">Uma configuração de nó é um documento MOF que é implantado no servidor de pull e está pronto para ser submetido ao pull e aplicado por um ou mais nós.</span><span class="sxs-lookup"><span data-stu-id="27ea0-166">A node configuration is a MOF document that is deployed to the pull server and ready to be pulled and applied by one or more nodes.</span></span> <span data-ttu-id="27ea0-167">Você pode exibir as configurações do nó em sua conta de Automação na folha **Configurações do Nó DSC** .</span><span class="sxs-lookup"><span data-stu-id="27ea0-167">You can view the node configurations in your Automation account in the **DSC Node Configurations** blade.</span></span> <span data-ttu-id="27ea0-168">Uma configuração de nó tem um nome com o formato *NomeConfiguração*.*NomeNó*.</span><span class="sxs-lookup"><span data-stu-id="27ea0-168">A node configuration has a name with the form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="27ea0-169">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27ea0-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="27ea0-170">No menu Hub, clique em **Todos os recursos** , em seguida, no nome da sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-170">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="27ea0-171">Na folha **Conta de Automação**, clique em **Configurações do Nó DSC**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-171">On the **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Captura de tela da folha DSC Node Configurations (Configurações de Nó DSC)](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="27ea0-173">Integrando uma VM do Azure para o gerenciamento com o DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="27ea0-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="27ea0-174">Você pode usar o DSC de Automação do Azure para gerenciar VMs do Azure (Clássicas e Resource Manager), VMs locais, computadores Linux, VMs AWS e computadores físicos locais.</span><span class="sxs-lookup"><span data-stu-id="27ea0-174">You can use Azure Automation DSC to manage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="27ea0-175">Neste tópico, abordamos como integrar somente VMs do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="27ea0-175">In this topic, we cover how to onboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="27ea0-176">Para obter informações sobre a integração de outros tipos de computadores, consulte [Integrando computadores para o gerenciamento pela DSC de Automação do Azure](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="27ea0-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="to-onboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="27ea0-177">Para integrar uma VM do Azure Resource Manager para o gerenciamento pelo DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="27ea0-177">To onboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="27ea0-178">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27ea0-178">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="27ea0-179">No menu Hub, clique em **Todos os recursos** , em seguida, no nome da sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-179">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="27ea0-180">Na folha **Conta de Automação**, clique em **Nós DSC**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-180">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="27ea0-181">Na folha **Nós DSC**, clique em **Adicionar VM do Azure**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-181">In the **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Captura de tela da folha Nós DSC realçando o botão Adicionar VM do Azure](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="27ea0-183">Na folha **Adicionar VMs do Azure**, clique em **Selecionar máquinas virtuais para integração**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-183">In the **Add Azure VMs** blade, click **Select virtual machines to onboard**.</span></span>
6. <span data-ttu-id="27ea0-184">Na folha **Selecionar VMs**, selecione a VM que você deseja integrar e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-184">In the **Select VMs** blade, select the VM you want to onboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="27ea0-185">Ela deve ser uma VM do Azure Resource Manager executando o Windows Server 2008 R2 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="27ea0-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="27ea0-186">Na folha **Adicionar VMs do Azure**, clique em **Configurar dados de registro**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-186">In the **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="27ea0-187">Na folha **Registro**, insira o nome da configuração do nó que você deseja aplicar à VM na caixa **Nome de Configuração do Nó**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-187">In the **Registration** blade, enter the name of the node configuration you want to apply to the VM in the **Node Configuration Name** box.</span></span> <span data-ttu-id="27ea0-188">Isso deve corresponder exatamente ao nome de uma configuração de nó na conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-188">This must exactly match the name of a node configuration in the Automation account.</span></span> <span data-ttu-id="27ea0-189">Fornecer um nome neste ponto é opcional.</span><span class="sxs-lookup"><span data-stu-id="27ea0-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="27ea0-190">Você pode alterar a configuração de nó atribuída após integrar o nó.</span><span class="sxs-lookup"><span data-stu-id="27ea0-190">You can change the assigned node configuration after onboarding the node.</span></span>
   <span data-ttu-id="27ea0-191">Marque **Reinicializar o Nó se Necessário** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Captura de tela da folha Registro](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="27ea0-193">A configuração do nó especificada será aplicada à VM em intervalos especificados pela **Frequência do Modo de Configuração** e a VM verificará se há atualizações para a configuração do nó em intervalos especificados pela **Frequência de Atualização**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-193">The node configuration you specified will be applied to the VM at intervals specified by the **Configuration Mode Frequency**, and the VM will check for updates to the node configuration at intervals specified by the **Refresh Frequency**.</span></span> <span data-ttu-id="27ea0-194">Para obter mais informações sobre como esses valores são usados, consulte [Configurando o Gerenciador de Configuração Local](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="27ea0-194">For more information about how these values are used, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="27ea0-195">Na folha **Adicionar VMs do Azure**, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-195">In the **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="27ea0-196">O Azure iniciará o processo de integração da VM.</span><span class="sxs-lookup"><span data-stu-id="27ea0-196">Azure will start the process of onboarding the VM.</span></span> <span data-ttu-id="27ea0-197">Quando for concluída, a VM será exibida na folha **Nós DSC** na conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-197">When it is complete, the VM will show up in the **DSC Nodes** blade in the Automation account.</span></span>

## <a name="viewing-the-list-of-dsc-nodes"></a><span data-ttu-id="27ea0-198">Exibindo a lista de nós DSC</span><span class="sxs-lookup"><span data-stu-id="27ea0-198">Viewing the list of DSC nodes</span></span>
<span data-ttu-id="27ea0-199">Você pode exibir a lista de todos os computadores que foram integrados para gerenciamento em sua conta de Automação na folha **Nós DSC** .</span><span class="sxs-lookup"><span data-stu-id="27ea0-199">You can view the list of all machines that have been onboarded for management in your Automation account in the **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="27ea0-200">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27ea0-200">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="27ea0-201">No menu Hub, clique em **Todos os recursos** , em seguida, no nome da sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-201">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="27ea0-202">Na folha **Conta de Automação**, clique em **Nós DSC**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-202">On the **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="27ea0-203">Exibindo relatórios para nós DSC</span><span class="sxs-lookup"><span data-stu-id="27ea0-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="27ea0-204">Cada vez que o DSC de Automação do Azure executa uma verificação de consistência em um nó gerenciado, o nó envia um relatório de status para o servidor de pull.</span><span class="sxs-lookup"><span data-stu-id="27ea0-204">Each time Azure Automation DSC performs a consistency check on a managed node, the node sends a status report back to the pull server.</span></span> <span data-ttu-id="27ea0-205">Você pode exibir esses relatórios na folha do nó.</span><span class="sxs-lookup"><span data-stu-id="27ea0-205">You can view these reports on the blade for that node.</span></span>

1. <span data-ttu-id="27ea0-206">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27ea0-206">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="27ea0-207">No menu Hub, clique em **Todos os recursos** , em seguida, no nome da sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-207">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="27ea0-208">Na folha **Conta de Automação**, clique em **Nós DSC**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-208">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="27ea0-209">No bloco **Relatórios** , clique em qualquer um dos relatórios na lista.</span><span class="sxs-lookup"><span data-stu-id="27ea0-209">On the **Reports** tile, click on any of the reports in the list.</span></span>
   
    ![Captura de tela da folha Relatório](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="27ea0-211">Na folha de um relatório individual, você pode ver as seguintes informações de status para a verificação de consistência correspondente:</span><span class="sxs-lookup"><span data-stu-id="27ea0-211">On the blade for an individual report, you can see the following status information for the corresponding consistency check:</span></span>

* <span data-ttu-id="27ea0-212">Status do relatório — se o nó é "Compatível", a configuração está "Com Falha" ou o nó "Não é Compatível" (quando o nó está no modo **applyandmonitor** e o computador não está no estado desejado).</span><span class="sxs-lookup"><span data-stu-id="27ea0-212">The report status — whether the node is "Compliant", the configuration "Failed", or the node is "Not Compliant" (when the node is in **applyandmonitor** mode and the machine is not in the desired state).</span></span>
* <span data-ttu-id="27ea0-213">A hora de início para a verificação de consistência.</span><span class="sxs-lookup"><span data-stu-id="27ea0-213">The start time for the consistency check.</span></span>
* <span data-ttu-id="27ea0-214">O tempo de execução total para a verificação de consistência.</span><span class="sxs-lookup"><span data-stu-id="27ea0-214">The total runtime for the consistency check.</span></span>
* <span data-ttu-id="27ea0-215">O tipo de verificação de consistência.</span><span class="sxs-lookup"><span data-stu-id="27ea0-215">The type of consistency check.</span></span>
* <span data-ttu-id="27ea0-216">Quaisquer erros, incluindo o código de erro e a mensagem de erro.</span><span class="sxs-lookup"><span data-stu-id="27ea0-216">Any errors, including the error code and error message.</span></span> 
* <span data-ttu-id="27ea0-217">Todos os recursos DSC usados na configuração e o estado de cada recurso (se o nó está no estado desejado para esse recurso) — você pode clicar em cada recurso para obter informações mais detalhadas para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="27ea0-217">Any DSC resources used in the configuration, and the state of each resource (whether the node is in the desired state for that resource) — you can click on each resource to get more detailed information for that resource.</span></span>
* <span data-ttu-id="27ea0-218">O nome, o endereço IP e o modo de configuração do nó.</span><span class="sxs-lookup"><span data-stu-id="27ea0-218">The name, IP address, and configuration mode of the node.</span></span>

<span data-ttu-id="27ea0-219">Você também pode clicar em **Exibir relatório bruto** para ver os dados reais que o nó envia para o servidor.</span><span class="sxs-lookup"><span data-stu-id="27ea0-219">You can also click **View raw report** to see the actual data that the node sends to the server.</span></span> <span data-ttu-id="27ea0-220">Para obter mais informações sobre como usar esses dados, consulte [Usando um servidor de relatório da DSC](https://msdn.microsoft.com/powershell/dsc/reportserver).</span><span class="sxs-lookup"><span data-stu-id="27ea0-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="27ea0-221">Pode levar algum tempo depois de um nó ser integrado até que o primeiro relatório esteja disponível.</span><span class="sxs-lookup"><span data-stu-id="27ea0-221">It can take some time after a node is onboarded before the first report is available.</span></span> <span data-ttu-id="27ea0-222">Talvez seja necessário aguardar até 30 minutos para o primeiro relatório após você integrar um nó.</span><span class="sxs-lookup"><span data-stu-id="27ea0-222">You might need to wait up to 30 minutes for the first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-to-a-different-node-configuration"></a><span data-ttu-id="27ea0-223">Reatribuindo um nó a uma configuração de nó diferente</span><span class="sxs-lookup"><span data-stu-id="27ea0-223">Reassigning a node to a different node configuration</span></span>
<span data-ttu-id="27ea0-224">Você pode atribuir um nó para usar uma configuração de nó diferente daquela que inicialmente atribuída.</span><span class="sxs-lookup"><span data-stu-id="27ea0-224">You can assign a node to use a different node configuration than the one you initially assigned.</span></span>

1. <span data-ttu-id="27ea0-225">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27ea0-225">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="27ea0-226">No menu Hub, clique em **Todos os recursos** , em seguida, no nome da sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-226">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="27ea0-227">Na folha **Conta de Automação**, clique em **Nós DSC**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-227">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="27ea0-228">Na folha **Nós DSC** , clique no nome do nó que você deseja reatribuir.</span><span class="sxs-lookup"><span data-stu-id="27ea0-228">On the **DSC Nodes** blade, click on the name of the node you want to reassign.</span></span>
5. <span data-ttu-id="27ea0-229">Na folha do nó, clique em **Atribuir nó**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-229">On the blade for that node, click **Assign node**.</span></span>
   
    ![Captura de tela da folha Nó realçando o botão Assign Node (Atribuir Nó)](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="27ea0-231">Na folha **Atribuir Configuração de Nó**, selecione a configuração de nó à qual você deseja atribuir o nó, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-231">On the **Assign Node Configuration** blade, select the node configuration to which you want to assign the node, and then click **OK**.</span></span>
   
    ![Captura de tela da folha Atribuir Configuração de Nó](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="27ea0-233">Cancelando o registro de um nó</span><span class="sxs-lookup"><span data-stu-id="27ea0-233">Unregistering a node</span></span>
<span data-ttu-id="27ea0-234">Se você não desejar mais que um nó seja gerenciado pelo DSC de Automação do Azure, você poderá cancelar o registro dele.</span><span class="sxs-lookup"><span data-stu-id="27ea0-234">If you no longer want a node to be managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="27ea0-235">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27ea0-235">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="27ea0-236">No menu Hub, clique em **Todos os recursos** , em seguida, no nome da sua conta de Automação.</span><span class="sxs-lookup"><span data-stu-id="27ea0-236">On the Hub menu, click **All resources** and then the name of your Automation account.</span></span>
3. <span data-ttu-id="27ea0-237">Na folha **Conta de Automação**, clique em **Nós DSC**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-237">On the **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="27ea0-238">Na folha **Nós DSC** , clique no nome do nó cujo registro você deseja cancelar.</span><span class="sxs-lookup"><span data-stu-id="27ea0-238">On the **DSC Nodes** blade, click on the name of the node you want to unregister.</span></span>
5. <span data-ttu-id="27ea0-239">Na folha desse nó, clique em **Cancelar Registro**.</span><span class="sxs-lookup"><span data-stu-id="27ea0-239">On the blade for that node, click **Unregister**.</span></span>
   
    ![Captura de tela da folha Nó realçando o botão Cancelar Registro](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="27ea0-241">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="27ea0-241">Related Articles</span></span>
* [<span data-ttu-id="27ea0-242">Visão geral do DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="27ea0-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="27ea0-243">Máquinas de integração para o gerenciamento pelo DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="27ea0-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="27ea0-244">Visão Geral da Configuração de Estado Desejado do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="27ea0-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="27ea0-245">cmdlets da DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="27ea0-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="27ea0-246">preço da DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="27ea0-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

