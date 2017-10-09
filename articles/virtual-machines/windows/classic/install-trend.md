---
title: "aaaInstall Trend Micro Deep Security em uma máquina virtual | Microsoft Docs"
description: "Este artigo descreve como tooinstall e configurar a segurança de Trend Micro em uma máquina virtual criada com o modelo de implantação clássico Olá no Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="8db4c-103">Como tooinstall e configurar o Trend Micro Deep Security como um serviço em uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="8db4c-103">How tooinstall and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8db4c-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8db4c-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8db4c-105">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="8db4c-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="8db4c-106">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="8db4c-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="8db4c-107">Este artigo mostra como tooinstall e configurar o Trend Micro Deep Security como um serviço em um novo ou existente máquina virtual (VM executando o Windows Server).</span><span class="sxs-lookup"><span data-stu-id="8db4c-107">This article shows you how tooinstall and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="8db4c-108">O Deep Security as a Service inclui proteção anti-malware, firewall, sistema de prevenção de intrusões e monitoramento de integridade.</span><span class="sxs-lookup"><span data-stu-id="8db4c-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="8db4c-109">Olá cliente é instalado como uma extensão de segurança por meio de saudação agente de VM.</span><span class="sxs-lookup"><span data-stu-id="8db4c-109">hello client is installed as a security extension via hello VM Agent.</span></span> <span data-ttu-id="8db4c-110">Em uma nova máquina virtual, instale Olá Deep Security Agent, como Olá que agente VM é criada automaticamente pelo Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="8db4c-110">On a new virtual machine, you install hello Deep Security Agent, as hello VM Agent is created automatically by hello Azure portal.</span></span>

<span data-ttu-id="8db4c-111">Uma VM existente criada usando o portal clássico do hello, Olá CLI do Azure ou o PowerShell não pode ter um agente VM.</span><span class="sxs-lookup"><span data-stu-id="8db4c-111">An existing VM created using hello classic portal, hello Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="8db4c-112">Para uma máquina virtual existente que não tenha Olá agente de VM, você precisa toodownload e instalá-lo primeiro.</span><span class="sxs-lookup"><span data-stu-id="8db4c-112">For an existing virtual machine that doesn't have hello VM Agent, you need toodownload and install it first.</span></span> <span data-ttu-id="8db4c-113">Este artigo aborda ambas as situações.</span><span class="sxs-lookup"><span data-stu-id="8db4c-113">This article covers both situations.</span></span>

<span data-ttu-id="8db4c-114">Se você tiver uma assinatura atual da Trend Micro para uma solução local, você pode usá-lo toohelp proteger suas máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="8db4c-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it toohelp protect your Azure virtual machines.</span></span> <span data-ttu-id="8db4c-115">Se ainda não for cliente, você poderá se inscrever em uma assinatura de avaliação.</span><span class="sxs-lookup"><span data-stu-id="8db4c-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="8db4c-116">Para obter mais informações sobre esta solução, consulte Olá Trend Micro postagem de blog [Microsoft Azure VM Agent extensão para Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span><span class="sxs-lookup"><span data-stu-id="8db4c-116">For more information about this solution, see hello Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="8db4c-117">Instalar Olá Deep Security Agent em uma nova VM</span><span class="sxs-lookup"><span data-stu-id="8db4c-117">Install hello Deep Security Agent on a new VM</span></span>

<span data-ttu-id="8db4c-118">Olá [portal do Azure](http://portal.azure.com) permite que você instale a extensão de segurança Trend Micro hello quando você usar uma imagem de saudação **Marketplace** toocreate Olá VM.</span><span class="sxs-lookup"><span data-stu-id="8db4c-118">hello [Azure portal](http://portal.azure.com) lets you install hello Trend Micro security extension when you use an image from hello **Marketplace** toocreate hello virtual machine.</span></span> <span data-ttu-id="8db4c-119">Se você estiver criando uma única máquina virtual, usando o portal de saudação é uma proteção de tooadd de maneira fácil de Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="8db4c-119">If you're creating a single virtual machine, using hello portal is an easy way tooadd protection from Trend Micro.</span></span>

<span data-ttu-id="8db4c-120">Usando uma entrada de saudação **Marketplace** abre um assistente que ajuda você a configurar a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="8db4c-120">Using an entry from hello **Marketplace** opens a wizard that helps you set up hello virtual machine.</span></span> <span data-ttu-id="8db4c-121">Use Olá **configurações** folha, o terceiro painel saudação do assistente hello, Olá tooinstall extensão de segurança Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="8db4c-121">You use hello **Settings** blade, hello third panel of hello wizard, tooinstall hello Trend Micro security extension.</span></span>  <span data-ttu-id="8db4c-122">Para obter instruções gerais, consulte [criar uma máquina virtual executando o Windows hello portal do Azure](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="8db4c-122">For general instructions, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>

<span data-ttu-id="8db4c-123">Quando você obtém toohello **configurações** folha do Assistente de Olá Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="8db4c-123">When you get toohello **Settings** blade of hello wizard, do hello following steps:</span></span>

1. <span data-ttu-id="8db4c-124">Clique em **extensões**, em seguida, clique em **Adicionar extensão** no próximo painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="8db4c-124">Click **Extensions**, then click **Add extension** in hello next pane.</span></span>

   ![Começar a adicionar a extensão de saudação][1]

2. <span data-ttu-id="8db4c-126">Selecione **Deep Security Agent** em Olá **novo recurso** painel.</span><span class="sxs-lookup"><span data-stu-id="8db4c-126">Select **Deep Security Agent** in hello **New resource** pane.</span></span> <span data-ttu-id="8db4c-127">No painel de Deep Security Agent hello, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="8db4c-127">In hello Deep Security Agent pane, click **Create**.</span></span>

   ![Identificar o Deep Security Agent][2]

3. <span data-ttu-id="8db4c-129">Digite hello **identificador do locatário** e **senha de ativação do locatário** para extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="8db4c-129">Enter hello **Tenant Identifier** and **Tenant Activation Password** for hello extension.</span></span> <span data-ttu-id="8db4c-130">Opcionalmente, você pode inserir um **Identificador de Política de Segurança**.</span><span class="sxs-lookup"><span data-stu-id="8db4c-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="8db4c-131">Em seguida, clique em **Okey** tooadd cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="8db4c-131">Then, click **OK** tooadd hello client.</span></span>

   ![Fornecer detalhes da extensão][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="8db4c-133">Instalar Olá Deep Security Agent em uma VM existente</span><span class="sxs-lookup"><span data-stu-id="8db4c-133">Install hello Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="8db4c-134">Agente de saudação tooinstall em uma VM existente, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="8db4c-134">tooinstall hello agent on an existing VM, you need hello following items:</span></span>

* <span data-ttu-id="8db4c-135">módulo do PowerShell do Azure Hello, versão 0.8.2 ou mais recente, instalado no computador local.</span><span class="sxs-lookup"><span data-stu-id="8db4c-135">hello Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="8db4c-136">Você pode verificar a versão de saudação do PowerShell do Azure que você instalou usando Olá **azure Get-Module | versão de formato de tabela** comando.</span><span class="sxs-lookup"><span data-stu-id="8db4c-136">You can check hello version of Azure PowerShell that you have installed by using hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="8db4c-137">Para obter instruções e uma versão mais recente do link toohello, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8db4c-137">For instructions and a link toohello latest version, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="8db4c-138">Faça logon tooyour assinatura do Azure usando `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="8db4c-138">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="8db4c-139">saudação do agente de VM instalado na máquina de virtual de destino hello.</span><span class="sxs-lookup"><span data-stu-id="8db4c-139">hello VM Agent installed on hello target virtual machine.</span></span>

<span data-ttu-id="8db4c-140">Primeiro, verifique se esse Olá que VM Agent já está instalado.</span><span class="sxs-lookup"><span data-stu-id="8db4c-140">First, verify that hello VM Agent is already installed.</span></span> <span data-ttu-id="8db4c-141">Preencha o nome de serviço de nuvem hello e nome da máquina virtual e execute Olá comandos em um prompt de comando do PowerShell do Azure de nível de administrador a seguir.</span><span class="sxs-lookup"><span data-stu-id="8db4c-141">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="8db4c-142">Substitua tudo entre aspas hello, incluindo hello < e > caracteres.</span><span class="sxs-lookup"><span data-stu-id="8db4c-142">Replace everything within hello quotes, including hello < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="8db4c-143">Se você não souber o nome da máquina virtual e serviço de nuvem hello, execute **Get-AzureVM** toodisplay informações para todos os Olá máquinas virtuais em sua assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="8db4c-143">If you don't know hello cloud service and virtual machine name, run **Get-AzureVM** toodisplay that information for all hello virtual machines in your current subscription.</span></span>

<span data-ttu-id="8db4c-144">Se hello **write-host** comando retorna **True**, Olá VM Agent está instalado.</span><span class="sxs-lookup"><span data-stu-id="8db4c-144">If hello **write-host** command returns **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="8db4c-145">Se ele retorna **False**, consulte as instruções de saudação e um toohello link baixar Olá postagem no blog do Azure [agente de VM e extensões – parte 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span><span class="sxs-lookup"><span data-stu-id="8db4c-145">If it returns **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="8db4c-146">Se Olá agente VM é instalado, execute estes comandos.</span><span class="sxs-lookup"><span data-stu-id="8db4c-146">If hello VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="8db4c-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8db4c-147">Next steps</span></span>
<span data-ttu-id="8db4c-148">Leva alguns minutos para Olá toostart de agente em execução quando ele está instalado.</span><span class="sxs-lookup"><span data-stu-id="8db4c-148">It takes a few minutes for hello agent toostart running when it is installed.</span></span> <span data-ttu-id="8db4c-149">Depois disso, você precisa tooactivate segurança profunda na máquina virtual de saudação para que ele possa ser gerenciado por um Gerenciador de segurança profunda.</span><span class="sxs-lookup"><span data-stu-id="8db4c-149">After that, you need tooactivate Deep Security on hello virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="8db4c-150">Consulte Olá artigos para obter instruções adicionais a seguir:</span><span class="sxs-lookup"><span data-stu-id="8db4c-150">See hello following articles for additional instructions:</span></span>

* <span data-ttu-id="8db4c-151">Artigo de tendência sobre essa solução, [Segurança na nuvem Instant-On do Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="8db4c-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="8db4c-152">Um [script do Windows PowerShell de exemplo](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure Olá VM</span><span class="sxs-lookup"><span data-stu-id="8db4c-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello virtual machine</span></span>
* <span data-ttu-id="8db4c-153">[Instruções](http://go.microsoft.com/fwlink/?LinkId=404099) para exemplo hello</span><span class="sxs-lookup"><span data-stu-id="8db4c-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for hello sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8db4c-154">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="8db4c-154">Additional resources</span></span>
<span data-ttu-id="8db4c-155">[Como toolog na máquina virtual de tooa executando o Windows Server]</span><span class="sxs-lookup"><span data-stu-id="8db4c-155">[How toolog on tooa virtual machine running Windows Server]</span></span>

<span data-ttu-id="8db4c-156">[Recursos e extensões de VM do Azure]</span><span class="sxs-lookup"><span data-stu-id="8db4c-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[Como toolog na máquina virtual de tooa executando o Windows Server]:connect-logon.md
[Recursos e extensões de VM do Azure]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
