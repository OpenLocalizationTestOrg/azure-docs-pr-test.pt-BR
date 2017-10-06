---
title: "aaaGetting de Introdução ao DSC de automação do Azure | Microsoft Docs"
description: "Explicações e exemplos das tarefas mais comuns de saudação no Azure Automation desejado configuração de estado (DSC)"
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
ms.openlocfilehash: 82910c96e928b9264c2e1b52a5c98dc47273dcc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-automation-dsc"></a><span data-ttu-id="b8699-103">Introdução ao DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="b8699-103">Getting started with Azure Automation DSC</span></span>
<span data-ttu-id="b8699-104">Este tópico explica como toodo Olá tarefas mais comuns com o Azure automação desejado configuração de estado (DSC), como criar, importar e compilar configurações, integração muito gerenciar máquinas e exibir relatórios.</span><span class="sxs-lookup"><span data-stu-id="b8699-104">This topic explains how toodo hello most common tasks with Azure Automation Desired State Configuration (DSC), such as creating, importing, and compiling configurations, onboarding machines too manage, and viewing reports.</span></span> <span data-ttu-id="b8699-105">Para obter uma visão geral do que o DSC de Automação do Azure é, consulte [Visão geral do DSC da Automação do Azure](automation-dsc-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b8699-105">For an overview of what Azure Automation DSC is, see [Azure Automation DSC Overview](automation-dsc-overview.md).</span></span> <span data-ttu-id="b8699-106">Para obter a documentação da DSC, consulte [Visão Geral da Configuração de Estado Desejado do Windows PowerShell](https://msdn.microsoft.com/PowerShell/dsc/overview).</span><span class="sxs-lookup"><span data-stu-id="b8699-106">For DSC documentation, see [Windows PowerShell Desired State Configuration Overview](https://msdn.microsoft.com/PowerShell/dsc/overview).</span></span>

<span data-ttu-id="b8699-107">Este tópico fornece um guia passo a passo de toousing DSC de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8699-107">This topic provides a step-by-step guide toousing Azure Automation DSC.</span></span> <span data-ttu-id="b8699-108">Se você quiser um ambiente de exemplo que já está configurado sem Olá etapas descritas neste tópico, você pode usar [Olá seguinte modelo do ARM](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span><span class="sxs-lookup"><span data-stu-id="b8699-108">If you want a sample environment that is already set up without following hello steps described in this topic, you can use [hello following ARM template](https://github.com/azureautomation/automation-packs/tree/master/102-sample-automation-setup).</span></span> <span data-ttu-id="b8699-109">Esse modelo define um ambiente completo do DSC de Automação do Azure, incluindo uma VM do Azure que é gerenciada pelo DSC de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8699-109">This template sets up a completed Azure Automation DSC environment, including an Azure VM that is managed by Azure Automation DSC.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8699-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b8699-110">Prerequisites</span></span>
<span data-ttu-id="b8699-111">toocomplete Olá exemplos neste tópico, a seguinte Olá é necessários:</span><span class="sxs-lookup"><span data-stu-id="b8699-111">toocomplete hello examples in this topic, hello following are required:</span></span>

* <span data-ttu-id="b8699-112">Uma conta de Automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8699-112">An Azure Automation account.</span></span> <span data-ttu-id="b8699-113">Para obter instruções sobre como criar uma conta Executar Como de Automação do Azure, consulte [Conta Executar Como do Azure](automation-sec-configure-azure-runas-account.md).</span><span class="sxs-lookup"><span data-stu-id="b8699-113">For instructions on creating an Azure Automation Run As account, see [Azure Run As Account](automation-sec-configure-azure-runas-account.md).</span></span>
* <span data-ttu-id="b8699-114">Uma VM do Azure Resource Manager (não clássica) executando o Windows Server 2008 R2 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b8699-114">An Azure Resource Manager VM (not Classic) running Windows Server 2008 R2 or later.</span></span> <span data-ttu-id="b8699-115">Para obter instruções sobre como criar uma VM, consulte [criar sua primeira máquina virtual Windows no hello portal do Azure](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="b8699-115">For instructions on creating a VM, see [Create your first Windows virtual machine in hello Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md)</span></span>

## <a name="creating-a-dsc-configuration"></a><span data-ttu-id="b8699-116">Criando uma configuração de DSC</span><span class="sxs-lookup"><span data-stu-id="b8699-116">Creating a DSC configuration</span></span>
<span data-ttu-id="b8699-117">Vamos criar um simples [configuração DSC](https://msdn.microsoft.com/powershell/dsc/configurations) que garante a presença de saudação ou ausência de saudação **Web-Server** recurso (IIS) do Windows, dependendo de como você atribui a nós.</span><span class="sxs-lookup"><span data-stu-id="b8699-117">We will create a simple [DSC configuration](https://msdn.microsoft.com/powershell/dsc/configurations) that ensures either hello presence or absence of hello **Web-Server** Windows Feature (IIS), depending on how you assign nodes.</span></span>

1. <span data-ttu-id="b8699-118">Inicie Olá ISE do Windows PowerShell (ou qualquer editor de texto).</span><span class="sxs-lookup"><span data-stu-id="b8699-118">Start hello Windows PowerShell ISE (or any text editor).</span></span>
2. <span data-ttu-id="b8699-119">Saudação de tipo texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="b8699-119">Type hello following text:</span></span>
   
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
3. <span data-ttu-id="b8699-120">Salve o arquivo hello como `TestConfig.ps1`.</span><span class="sxs-lookup"><span data-stu-id="b8699-120">Save hello file as `TestConfig.ps1`.</span></span>

<span data-ttu-id="b8699-121">Essa configuração chama um recurso em cada bloco de nó, hello [recurso WindowsFeature](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), que garante a presença de saudação ou ausência de saudação **Web-Server** recurso.</span><span class="sxs-lookup"><span data-stu-id="b8699-121">This configuration calls one resource in each node block, hello [WindowsFeature resource](https://msdn.microsoft.com/powershell/dsc/windowsfeatureresource), that ensures either hello presence or absence of hello **Web-Server** feature.</span></span>

## <a name="importing-a-configuration-into-azure-automation"></a><span data-ttu-id="b8699-122">Importando uma configuração na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="b8699-122">Importing a configuration into Azure Automation</span></span>
<span data-ttu-id="b8699-123">Em seguida, podemos vai importar configuração de saudação para Olá conta de automação.</span><span class="sxs-lookup"><span data-stu-id="b8699-123">Next, we'll import hello configuration into hello Automation account.</span></span>

1. <span data-ttu-id="b8699-124">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8699-124">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b8699-125">No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="b8699-125">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="b8699-126">Em Olá **conta de automação** folha, clique em **configurações DSC**.</span><span class="sxs-lookup"><span data-stu-id="b8699-126">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="b8699-127">Em Olá **configurações DSC** folha, clique em **adicionar uma configuração de**.</span><span class="sxs-lookup"><span data-stu-id="b8699-127">On hello **DSC Configurations** blade, click **Add a configuration**.</span></span>
5. <span data-ttu-id="b8699-128">Em Olá **Importar configuração** folha, procurar toohello `TestConfig.ps1` arquivo no seu computador.</span><span class="sxs-lookup"><span data-stu-id="b8699-128">On hello **Import Configuration** blade, browse toohello `TestConfig.ps1` file on your computer.</span></span>
   
    ![Captura de tela de hello * * folha Importar configuração * *](./media/automation-dsc-getting-started/AddConfig.png)
6. <span data-ttu-id="b8699-130">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8699-130">Click **OK**.</span></span>

## <a name="viewing-a-configuration-in-azure-automation"></a><span data-ttu-id="b8699-131">Exibindo uma configuração na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="b8699-131">Viewing a configuration in Azure Automation</span></span>
<span data-ttu-id="b8699-132">Depois de importar uma configuração, você pode exibi-lo no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8699-132">After you have imported a configuration, you can view it in hello Azure portal.</span></span>

1. <span data-ttu-id="b8699-133">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8699-133">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b8699-134">No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="b8699-134">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="b8699-135">Em Olá **conta de automação** folha, clique em **configurações DSC**</span><span class="sxs-lookup"><span data-stu-id="b8699-135">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="b8699-136">Em Olá **configurações DSC** folha, clique em **TestConfig** (esse é nome hello da configuração de saudação você importou no procedimento anterior Olá).</span><span class="sxs-lookup"><span data-stu-id="b8699-136">On hello **DSC Configurations** blade, click **TestConfig** (this is hello name of hello configuration you imported in hello previous procedure).</span></span>
5. <span data-ttu-id="b8699-137">Em Olá **TestConfig configuração** folha, clique em **Exibir código-fonte configuração**.</span><span class="sxs-lookup"><span data-stu-id="b8699-137">On hello **TestConfig Configuration** blade, click **View configuration source**.</span></span>
   
    ![Captura de tela da folha de configuração TestConfig Olá](./media/automation-dsc-getting-started/ViewConfigSource.png)
   
    <span data-ttu-id="b8699-139">Um **fonte de configuração TestConfig** folha é aberta, exibindo o código do PowerShell Olá para configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8699-139">A **TestConfig Configuration source** blade opens, displaying hello PowerShell code for hello configuration.</span></span>

## <a name="compiling-a-configuration-in-azure-automation"></a><span data-ttu-id="b8699-140">Compilando uma configuração na Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="b8699-140">Compiling a configuration in Azure Automation</span></span>
<span data-ttu-id="b8699-141">Antes de aplicar um nó de tooa de estado desejado, uma configuração DSC definindo o estado deve ser compilada em uma ou mais configurações de nó (documento MOF) e colocada no servidor de Pull de DSC de automação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8699-141">Before you can apply a desired state tooa node, a DSC configuration defining that state must be compiled into one or more node configurations (MOF document), and placed on hello Automation DSC Pull Server.</span></span> <span data-ttu-id="b8699-142">Para obter uma descrição mais detalhada da compilação das configurações na DSC de Automação do Azure, consulte [Compilando as configurações na DSC de Automação do Azure](automation-dsc-compile.md).</span><span class="sxs-lookup"><span data-stu-id="b8699-142">For a more detailed description of compiling configurations in Azure Automation DSC, see [Compiling configurations in Azure Automation DSC](automation-dsc-compile.md).</span></span> <span data-ttu-id="b8699-143">Para obter mais informações sobre a compilação das configurações, consulte [Configurações da DSC](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span><span class="sxs-lookup"><span data-stu-id="b8699-143">For more information about compiling configurations, see [DSC Configurations](https://msdn.microsoft.com/PowerShell/DSC/configurations).</span></span>

1. <span data-ttu-id="b8699-144">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8699-144">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b8699-145">No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="b8699-145">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="b8699-146">Em Olá **conta de automação** folha, clique em **configurações DSC**</span><span class="sxs-lookup"><span data-stu-id="b8699-146">On hello **Automation account** blade, click **DSC Configurations**</span></span>
4. <span data-ttu-id="b8699-147">Em Olá **configurações DSC** folha, clique em **TestConfig** (nome de saudação do hello importado anteriormente configuração).</span><span class="sxs-lookup"><span data-stu-id="b8699-147">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="b8699-148">Em Olá **TestConfig configuração** folha, clique em **compilar**e, em seguida, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="b8699-148">On hello **TestConfig Configuration** blade, click **Compile**, and then click **Yes**.</span></span> <span data-ttu-id="b8699-149">Isso inicia um trabalho de compilação.</span><span class="sxs-lookup"><span data-stu-id="b8699-149">This starts a compilation job.</span></span>
   
    ![Captura de tela da folha de configuração TestConfig Olá realce de botão de compilação](./media/automation-dsc-getting-started/CompileConfig.png)

> [!NOTE]
> <span data-ttu-id="b8699-151">Quando você compila uma configuração na automação do Azure, ele implanta automaticamente a qualquer servidor de pull criado nó configuração MOFs toohello.</span><span class="sxs-lookup"><span data-stu-id="b8699-151">When you compile a configuration in Azure Automation, it automatically deploys any created node configuration MOFs toohello pull server.</span></span>
> 
> 

## <a name="viewing-a-compilation-job"></a><span data-ttu-id="b8699-152">Exibindo um trabalho de compilação</span><span class="sxs-lookup"><span data-stu-id="b8699-152">Viewing a compilation job</span></span>
<span data-ttu-id="b8699-153">Depois de iniciar uma compilação, você pode exibi-lo no hello **trabalhos de compilação** lado a lado no hello **configuração** folha.</span><span class="sxs-lookup"><span data-stu-id="b8699-153">After you start a compilation, you can view it in hello **Compilation jobs** tile in hello **Configuration** blade.</span></span> <span data-ttu-id="b8699-154">Olá **trabalhos de compilação** bloco mostra atualmente em execução, concluído e trabalhos com falha.</span><span class="sxs-lookup"><span data-stu-id="b8699-154">hello **Compilation jobs** tile shows currently running, completed, and failed jobs.</span></span> <span data-ttu-id="b8699-155">Quando você abre uma folha de trabalho de compilação, mostra informações sobre o trabalho incluindo erros ou avisos encontrados, parâmetros de entrada usado na configuração de saudação e compilação logs.</span><span class="sxs-lookup"><span data-stu-id="b8699-155">When you open a compilation job blade, it shows information about that job including any errors or warnings encountered, input parameters used in hello configuration, and compilation logs.</span></span>

1. <span data-ttu-id="b8699-156">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8699-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b8699-157">No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="b8699-157">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="b8699-158">Em Olá **conta de automação** folha, clique em **configurações DSC**.</span><span class="sxs-lookup"><span data-stu-id="b8699-158">On hello **Automation account** blade, click **DSC Configurations**.</span></span>
4. <span data-ttu-id="b8699-159">Em Olá **configurações DSC** folha, clique em **TestConfig** (nome de saudação do hello importado anteriormente configuração).</span><span class="sxs-lookup"><span data-stu-id="b8699-159">On hello **DSC Configurations** blade, click **TestConfig** (hello name of hello previously imported configuration).</span></span>
5. <span data-ttu-id="b8699-160">Em Olá **trabalhos de compilação** lado a lado de saudação **TestConfig configuração** folha, clique em qualquer um dos trabalhos de saudação listados.</span><span class="sxs-lookup"><span data-stu-id="b8699-160">On hello **Compilation jobs** tile of hello **TestConfig Configuration** blade, click on any of hello jobs listed.</span></span> <span data-ttu-id="b8699-161">Um **trabalho de compilação** abre folha, rotulado com data Olá Olá trabalho de compilação foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="b8699-161">A **Compilation Job** blade opens, labeled with hello date that hello compilation job was started.</span></span>
   
    ![Captura de tela da folha de trabalho de compilação de saudação](./media/automation-dsc-getting-started/CompilationJob.png)
6. <span data-ttu-id="b8699-163">Clique em qualquer lado a lado no hello **trabalho de compilação** folha toosee mais detalhes sobre o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8699-163">Click on any tile in hello **Compilation Job** blade toosee further details about hello job.</span></span>

## <a name="viewing-node-configurations"></a><span data-ttu-id="b8699-164">Exibindo configurações de nó</span><span class="sxs-lookup"><span data-stu-id="b8699-164">Viewing node configurations</span></span>
<span data-ttu-id="b8699-165">A conclusão com êxito de um trabalho de compilação cria uma ou mais novas configurações de nó.</span><span class="sxs-lookup"><span data-stu-id="b8699-165">Successful completion of a compilation job creates one or more new node configurations.</span></span> <span data-ttu-id="b8699-166">Uma configuração de nó é um documento MOF é implantado toohello servidor de pull e pronto toobe extraída e aplicada por um ou mais nós.</span><span class="sxs-lookup"><span data-stu-id="b8699-166">A node configuration is a MOF document that is deployed toohello pull server and ready toobe pulled and applied by one or more nodes.</span></span> <span data-ttu-id="b8699-167">Você pode exibir as configurações de nó de saudação em sua conta de automação em Olá **configurações do nó DSC** folha.</span><span class="sxs-lookup"><span data-stu-id="b8699-167">You can view hello node configurations in your Automation account in hello **DSC Node Configurations** blade.</span></span> <span data-ttu-id="b8699-168">Uma configuração de nó tem um nome com o formulário de saudação *ConfigurationName*. *NodeName*.</span><span class="sxs-lookup"><span data-stu-id="b8699-168">A node configuration has a name with hello form *ConfigurationName*.*NodeName*.</span></span>

1. <span data-ttu-id="b8699-169">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8699-169">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b8699-170">No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="b8699-170">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="b8699-171">Em Olá **conta de automação** folha, clique em **configurações do nó DSC**.</span><span class="sxs-lookup"><span data-stu-id="b8699-171">On hello **Automation account** blade, click **DSC Node Configurations**.</span></span>
   
    ![Captura de tela da folha de configurações do nó DSC Olá](./media/automation-dsc-getting-started/NodeConfigs.png)

## <a name="onboarding-an-azure-vm-for-management-with-azure-automation-dsc"></a><span data-ttu-id="b8699-173">Integrando uma VM do Azure para o gerenciamento com o DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="b8699-173">Onboarding an Azure VM for management with Azure Automation DSC</span></span>
<span data-ttu-id="b8699-174">Você pode usar o DSC de automação do Azure toomanage Azure VMs (clássico e o Gerenciador de recursos), VMs locais, máquinas Linux, AWS VMs e máquinas físicas locais.</span><span class="sxs-lookup"><span data-stu-id="b8699-174">You can use Azure Automation DSC toomanage Azure VMs (both Classic and Resource Manager), on-premises VMs, Linux machines, AWS VMs, and on-premises physical machines.</span></span> <span data-ttu-id="b8699-175">Neste tópico, abordaremos como tooonboard somente máquinas virtuais do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="b8699-175">In this topic, we cover how tooonboard only Azure Resource Manager VMs.</span></span> <span data-ttu-id="b8699-176">Para obter informações sobre a integração de outros tipos de computadores, consulte [Integrando computadores para o gerenciamento pela DSC de Automação do Azure](automation-dsc-onboarding.md).</span><span class="sxs-lookup"><span data-stu-id="b8699-176">For information about onboarding other types of machines, see [Onboarding machines for management by Azure Automation DSC](automation-dsc-onboarding.md).</span></span>

### <a name="tooonboard-an-azure-resource-manager-vm-for-management-by-azure-automation-dsc"></a><span data-ttu-id="b8699-177">tooonboard uma VM do Azure Resource Manager para o gerenciamento de DSC de automação do Azure</span><span class="sxs-lookup"><span data-stu-id="b8699-177">tooonboard an Azure Resource Manager VM for management by Azure Automation DSC</span></span>
1. <span data-ttu-id="b8699-178">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8699-178">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b8699-179">No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="b8699-179">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="b8699-180">Em Olá **conta de automação** folha, clique em **nós DSC**.</span><span class="sxs-lookup"><span data-stu-id="b8699-180">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="b8699-181">Em Olá **nós DSC** folha, clique em **adicionar a máquina virtual do Azure**.</span><span class="sxs-lookup"><span data-stu-id="b8699-181">In hello **DSC Nodes** blade, click **Add Azure VM**.</span></span>
   
    ![Captura de tela da folha de nós de DSC Olá realce de botão de adicionar a máquina virtual do Azure Olá](./media/automation-dsc-getting-started/OnboardVM.png)
5. <span data-ttu-id="b8699-183">Em Olá **adicionar VMs do Azure** folha, clique em **selecionar máquinas virtuais tooonboard**.</span><span class="sxs-lookup"><span data-stu-id="b8699-183">In hello **Add Azure VMs** blade, click **Select virtual machines tooonboard**.</span></span>
6. <span data-ttu-id="b8699-184">Em Olá **selecione VMs** folha, selecione Olá VM que você deseja tooonboard e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b8699-184">In hello **Select VMs** blade, select hello VM you want tooonboard, and click **OK**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="b8699-185">Ela deve ser uma VM do Azure Resource Manager executando o Windows Server 2008 R2 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b8699-185">This must be an Azure Resource Manager VM running Windows Server 2008 R2 or later.</span></span>
   > 
   > 
7. <span data-ttu-id="b8699-186">Em Olá **adicionar VMs do Azure** folha, clique em **configurar dados de registro**.</span><span class="sxs-lookup"><span data-stu-id="b8699-186">In hello **Add Azure VMs** blade, click **Configure registration data**.</span></span>
8. <span data-ttu-id="b8699-187">Em hello **registro** folha, insira o nome da saudação Olá da configuração de nó que você deseja tooapply toohello VM em Olá **nome de configuração de nó** caixa.</span><span class="sxs-lookup"><span data-stu-id="b8699-187">In hello **Registration** blade, enter hello name of hello node configuration you want tooapply toohello VM in hello **Node Configuration Name** box.</span></span> <span data-ttu-id="b8699-188">Isso deve corresponder exatamente o nome de saudação de uma configuração de nó Olá conta de automação.</span><span class="sxs-lookup"><span data-stu-id="b8699-188">This must exactly match hello name of a node configuration in hello Automation account.</span></span> <span data-ttu-id="b8699-189">Fornecer um nome neste ponto é opcional.</span><span class="sxs-lookup"><span data-stu-id="b8699-189">Providing a name at this point is optional.</span></span> <span data-ttu-id="b8699-190">Você pode alterar a configuração de nó de saudação atribuída após o nó de saudação de integração.</span><span class="sxs-lookup"><span data-stu-id="b8699-190">You can change hello assigned node configuration after onboarding hello node.</span></span>
   <span data-ttu-id="b8699-191">Marque **Reinicializar o Nó se Necessário** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b8699-191">Check **Reboot Node if Needed**, and then click **OK**.</span></span>
   
    ![Captura de tela da folha de registro Olá](./media/automation-dsc-getting-started/RegisterVM.png)
   
    <span data-ttu-id="b8699-193">configuração do nó Olá especificado será aplicado toohello VM em intervalos especificados por Olá **frequência do modo de configuração**, e Olá VM verificará a configuração de nó toohello atualizações em intervalos especificados por Olá  **Frequência de atualização**.</span><span class="sxs-lookup"><span data-stu-id="b8699-193">hello node configuration you specified will be applied toohello VM at intervals specified by hello **Configuration Mode Frequency**, and hello VM will check for updates toohello node configuration at intervals specified by hello **Refresh Frequency**.</span></span> <span data-ttu-id="b8699-194">Para obter mais informações sobre como esses valores são usados, consulte [Configurando Olá Gerenciador de configurações Local](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span><span class="sxs-lookup"><span data-stu-id="b8699-194">For more information about how these values are used, see [Configuring hello Local Configuration Manager](https://msdn.microsoft.com/PowerShell/DSC/metaConfig).</span></span>
9. <span data-ttu-id="b8699-195">Em Olá **adicionar VMs do Azure** folha, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="b8699-195">In hello **Add Azure VMs** blade, click **Create**.</span></span>

<span data-ttu-id="b8699-196">Azure iniciará o processo de saudação de integração hello VM.</span><span class="sxs-lookup"><span data-stu-id="b8699-196">Azure will start hello process of onboarding hello VM.</span></span> <span data-ttu-id="b8699-197">Quando for concluído, Olá VM será exibido no hello **nós DSC** folha em Olá conta de automação.</span><span class="sxs-lookup"><span data-stu-id="b8699-197">When it is complete, hello VM will show up in hello **DSC Nodes** blade in hello Automation account.</span></span>

## <a name="viewing-hello-list-of-dsc-nodes"></a><span data-ttu-id="b8699-198">Exibição de lista de saudação de nós de DSC</span><span class="sxs-lookup"><span data-stu-id="b8699-198">Viewing hello list of DSC nodes</span></span>
<span data-ttu-id="b8699-199">Você pode exibir a lista de saudação de todos os computadores que foram incorporados para gerenciamento na sua conta de automação em Olá **nós DSC** folha.</span><span class="sxs-lookup"><span data-stu-id="b8699-199">You can view hello list of all machines that have been onboarded for management in your Automation account in hello **DSC Nodes** blade.</span></span>

1. <span data-ttu-id="b8699-200">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8699-200">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b8699-201">No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="b8699-201">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="b8699-202">Em Olá **conta de automação** folha, clique em **nós DSC**.</span><span class="sxs-lookup"><span data-stu-id="b8699-202">On hello **Automation account** blade, click **DSC Nodes**.</span></span>

## <a name="viewing-reports-for-dsc-nodes"></a><span data-ttu-id="b8699-203">Exibindo relatórios para nós DSC</span><span class="sxs-lookup"><span data-stu-id="b8699-203">Viewing reports for DSC nodes</span></span>
<span data-ttu-id="b8699-204">Cada vez que DSC de automação do Azure executa uma verificação de consistência em um nó gerenciado, o nó Olá envia um servidor de pull de toohello voltar de relatório de status.</span><span class="sxs-lookup"><span data-stu-id="b8699-204">Each time Azure Automation DSC performs a consistency check on a managed node, hello node sends a status report back toohello pull server.</span></span> <span data-ttu-id="b8699-205">Você pode exibir esses relatórios na folha de saudação para esse nó.</span><span class="sxs-lookup"><span data-stu-id="b8699-205">You can view these reports on hello blade for that node.</span></span>

1. <span data-ttu-id="b8699-206">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8699-206">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b8699-207">No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="b8699-207">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="b8699-208">Em Olá **conta de automação** folha, clique em **nós DSC**.</span><span class="sxs-lookup"><span data-stu-id="b8699-208">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="b8699-209">Em Olá **relatórios** lado a lado, clique em qualquer um dos relatórios de saudação na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8699-209">On hello **Reports** tile, click on any of hello reports in hello list.</span></span>
   
    ![Captura de tela da folha de relatório Olá](./media/automation-dsc-getting-started/NodeReport.png)

<span data-ttu-id="b8699-211">Na folha de saudação para um relatório individual, você pode ver Olá segue as informações de status para manter a consistência correspondente Olá verificar:</span><span class="sxs-lookup"><span data-stu-id="b8699-211">On hello blade for an individual report, you can see hello following status information for hello corresponding consistency check:</span></span>

* <span data-ttu-id="b8699-212">Olá relatar o status — se o nó de saudação é "Compatíveis", a configuração de hello "Não", ou "nó hello não é compatível com" (quando o nó hello está em **applyandmonitor** modo e hello máquina não está em estado de saudação desejado).</span><span class="sxs-lookup"><span data-stu-id="b8699-212">hello report status — whether hello node is "Compliant", hello configuration "Failed", or hello node is "Not Compliant" (when hello node is in **applyandmonitor** mode and hello machine is not in hello desired state).</span></span>
* <span data-ttu-id="b8699-213">hora de início da saudação para verificação de consistência de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8699-213">hello start time for hello consistency check.</span></span>
* <span data-ttu-id="b8699-214">tempo de execução total consistência Olá Olá verificar.</span><span class="sxs-lookup"><span data-stu-id="b8699-214">hello total runtime for hello consistency check.</span></span>
* <span data-ttu-id="b8699-215">verificação de tipo de saudação de consistência.</span><span class="sxs-lookup"><span data-stu-id="b8699-215">hello type of consistency check.</span></span>
* <span data-ttu-id="b8699-216">Erros, incluindo a mensagem de erro e o código de erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8699-216">Any errors, including hello error code and error message.</span></span> 
* <span data-ttu-id="b8699-217">Todos os recursos DSC usados na configuração de Olá e o estado de saudação de cada recurso (se o nó de saudação está no estado de saudação desejado para esse recurso) — você pode clicar em cada recurso tooget informações mais detalhadas sobre esse recurso.</span><span class="sxs-lookup"><span data-stu-id="b8699-217">Any DSC resources used in hello configuration, and hello state of each resource (whether hello node is in hello desired state for that resource) — you can click on each resource tooget more detailed information for that resource.</span></span>
* <span data-ttu-id="b8699-218">nome de saudação, o endereço IP e o modo de configuração do nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="b8699-218">hello name, IP address, and configuration mode of hello node.</span></span>

<span data-ttu-id="b8699-219">Você também pode clicar em **Exibir relatório bruto** toosee Olá dados reais que Olá nó enviam toohello server.</span><span class="sxs-lookup"><span data-stu-id="b8699-219">You can also click **View raw report** toosee hello actual data that hello node sends toohello server.</span></span> <span data-ttu-id="b8699-220">Para obter mais informações sobre como usar esses dados, consulte [Usando um servidor de relatório da DSC](https://msdn.microsoft.com/powershell/dsc/reportserver).</span><span class="sxs-lookup"><span data-stu-id="b8699-220">For more information about using that data, see [Using a DSC report server](https://msdn.microsoft.com/powershell/dsc/reportserver).</span></span>

<span data-ttu-id="b8699-221">Pode levar algum tempo depois de um nó é incorporada antes que o primeiro relatório de saudação está disponível.</span><span class="sxs-lookup"><span data-stu-id="b8699-221">It can take some time after a node is onboarded before hello first report is available.</span></span> <span data-ttu-id="b8699-222">Talvez seja necessário toowait backup too30 minutos para o primeiro relatório de saudação após você integrar um nó.</span><span class="sxs-lookup"><span data-stu-id="b8699-222">You might need toowait up too30 minutes for hello first report after you onboard a node.</span></span>

## <a name="reassigning-a-node-tooa-different-node-configuration"></a><span data-ttu-id="b8699-223">Reatribuindo uma configuração de nó diferente do nó tooa</span><span class="sxs-lookup"><span data-stu-id="b8699-223">Reassigning a node tooa different node configuration</span></span>
<span data-ttu-id="b8699-224">Você pode atribuir uma configuração de nó diferente de toouse um nó de Olá um atribuídas inicialmente.</span><span class="sxs-lookup"><span data-stu-id="b8699-224">You can assign a node toouse a different node configuration than hello one you initially assigned.</span></span>

1. <span data-ttu-id="b8699-225">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8699-225">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b8699-226">No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="b8699-226">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="b8699-227">Em Olá **conta de automação** folha, clique em **nós DSC**.</span><span class="sxs-lookup"><span data-stu-id="b8699-227">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="b8699-228">Em Olá **nós DSC** folha, clique no nome de saudação do nó Olá deseja tooreassign.</span><span class="sxs-lookup"><span data-stu-id="b8699-228">On hello **DSC Nodes** blade, click on hello name of hello node you want tooreassign.</span></span>
5. <span data-ttu-id="b8699-229">Na folha de saudação do nó, clique em **atribuir nó**.</span><span class="sxs-lookup"><span data-stu-id="b8699-229">On hello blade for that node, click **Assign node**.</span></span>
   
    ![Captura de tela da folha de nó Olá realce de botão de nó atribuir Olá](./media/automation-dsc-getting-started/AssignNode.png)
6. <span data-ttu-id="b8699-231">Em Olá **atribuir a configuração do nó** folha, selecione Olá nó configuração toowhich você quiser tooassign Olá nó e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b8699-231">On hello **Assign Node Configuration** blade, select hello node configuration toowhich you want tooassign hello node, and then click **OK**.</span></span>
   
    ![Captura de tela da folha de configuração do nó atribuir Olá](./media/automation-dsc-getting-started/AssignNodeConfig.png)

## <a name="unregistering-a-node"></a><span data-ttu-id="b8699-233">Cancelando o registro de um nó</span><span class="sxs-lookup"><span data-stu-id="b8699-233">Unregistering a node</span></span>
<span data-ttu-id="b8699-234">Se você não quiser mais um toobe nó gerenciado pelo DSC de automação do Azure, você pode cancelar seu registro.</span><span class="sxs-lookup"><span data-stu-id="b8699-234">If you no longer want a node toobe managed by Azure Automation DSC, you can unregister it.</span></span>

1. <span data-ttu-id="b8699-235">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8699-235">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b8699-236">No menu de Hub hello, clique em **todos os recursos** e, em seguida, Olá nome de sua conta de automação.</span><span class="sxs-lookup"><span data-stu-id="b8699-236">On hello Hub menu, click **All resources** and then hello name of your Automation account.</span></span>
3. <span data-ttu-id="b8699-237">Em Olá **conta de automação** folha, clique em **nós DSC**.</span><span class="sxs-lookup"><span data-stu-id="b8699-237">On hello **Automation account** blade, click **DSC Nodes**.</span></span>
4. <span data-ttu-id="b8699-238">Em Olá **nós DSC** folha, clique no nome de saudação do nó Olá deseja toounregister.</span><span class="sxs-lookup"><span data-stu-id="b8699-238">On hello **DSC Nodes** blade, click on hello name of hello node you want toounregister.</span></span>
5. <span data-ttu-id="b8699-239">Na folha de saudação do nó, clique em **Unregister**.</span><span class="sxs-lookup"><span data-stu-id="b8699-239">On hello blade for that node, click **Unregister**.</span></span>
   
    ![Captura de tela da folha de nó Olá realce de botão de cancelamento de registro de saudação](./media/automation-dsc-getting-started/UnregisterNode.png)

## <a name="related-articles"></a><span data-ttu-id="b8699-241">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="b8699-241">Related Articles</span></span>
* [<span data-ttu-id="b8699-242">Visão geral do DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="b8699-242">Azure Automation DSC overview</span></span>](automation-dsc-overview.md)
* [<span data-ttu-id="b8699-243">Máquinas de integração para o gerenciamento pelo DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="b8699-243">Onboarding machines for management by Azure Automation DSC</span></span>](automation-dsc-onboarding.md)
* [<span data-ttu-id="b8699-244">Visão Geral da Configuração de Estado Desejado do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8699-244">Windows PowerShell Desired State Configuration Overview</span></span>](https://msdn.microsoft.com/powershell/dsc/overview)
* [<span data-ttu-id="b8699-245">cmdlets da DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="b8699-245">Azure Automation DSC cmdlets</span></span>](/powershell/module/azurerm.automation/#automation)
* [<span data-ttu-id="b8699-246">preço da DSC de Automação do Azure</span><span class="sxs-lookup"><span data-stu-id="b8699-246">Azure Automation DSC pricing</span></span>](https://azure.microsoft.com/pricing/details/automation/)

