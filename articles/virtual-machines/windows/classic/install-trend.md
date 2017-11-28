---
title: Instalar o Trend Micro Deep Security em uma VM | Microsoft Docs
description: "Este artigo descreve como instalar e configurar o Trend Micro security em uma VM criada com o modelo de implantação Clássico no Azure."
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
ms.openlocfilehash: 911b8f12472dcbda3e6bfeb8c97bf1d04a63e1dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="7acf7-103">Como instalar e configurar o Trend Micro Deep Security as a Service em uma VM do Windows</span><span class="sxs-lookup"><span data-stu-id="7acf7-103">How to install and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="7acf7-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7acf7-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="7acf7-105">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="7acf7-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="7acf7-106">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="7acf7-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="7acf7-107">Este artigo mostra como instalar e configurar o Trend Micro Deep Security as a Service em uma VM (máquina virtual) nova ou existente com o Windows Server em execução.</span><span class="sxs-lookup"><span data-stu-id="7acf7-107">This article shows you how to install and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="7acf7-108">O Deep Security as a Service inclui proteção anti-malware, firewall, sistema de prevenção de intrusões e monitoramento de integridade.</span><span class="sxs-lookup"><span data-stu-id="7acf7-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="7acf7-109">O cliente é instalado como uma extensão de segurança via Agente de VM.</span><span class="sxs-lookup"><span data-stu-id="7acf7-109">The client is installed as a security extension via the VM Agent.</span></span> <span data-ttu-id="7acf7-110">Em uma nova máquina virtual, você instala o Deep Security Agent, pois o Agente de VM é criado automaticamente pelo portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7acf7-110">On a new virtual machine, you install the Deep Security Agent, as the VM Agent is created automatically by the Azure portal.</span></span>

<span data-ttu-id="7acf7-111">Uma VM existente criada com o portal clássico, a CLI do Azure ou o PowerShell pode não ter um agente de VM.</span><span class="sxs-lookup"><span data-stu-id="7acf7-111">An existing VM created using the classic portal, the Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="7acf7-112">Em uma máquina virtual existente sem o Agente de VM, você precisa baixar e instalá-lo primeiro.</span><span class="sxs-lookup"><span data-stu-id="7acf7-112">For an existing virtual machine that doesn't have the VM Agent, you need to download and install it first.</span></span> <span data-ttu-id="7acf7-113">Este artigo aborda ambas as situações.</span><span class="sxs-lookup"><span data-stu-id="7acf7-113">This article covers both situations.</span></span>

<span data-ttu-id="7acf7-114">Se você tiver uma assinatura atual da Trend Micro para uma solução local, poderá usá-la para ajudar a proteger as máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="7acf7-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it to help protect your Azure virtual machines.</span></span> <span data-ttu-id="7acf7-115">Se ainda não for cliente, você poderá se inscrever em uma assinatura de avaliação.</span><span class="sxs-lookup"><span data-stu-id="7acf7-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="7acf7-116">Para saber mais sobre essa solução, confira a postagem no blog da Trend Micro [Extensão do agente de VM do Microsoft Azure para segurança profunda](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span><span class="sxs-lookup"><span data-stu-id="7acf7-116">For more information about this solution, see the Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-the-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="7acf7-117">Instalar o Agente do Deep Security Agent em uma nova VM</span><span class="sxs-lookup"><span data-stu-id="7acf7-117">Install the Deep Security Agent on a new VM</span></span>

<span data-ttu-id="7acf7-118">O [portal do Azure](http://portal.azure.com) permite que você instale a extensão de segurança da Trend Micro ao usar uma imagem do **Marketplace** para criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7acf7-118">The [Azure portal](http://portal.azure.com) lets you install the Trend Micro security extension when you use an image from the **Marketplace** to create the virtual machine.</span></span> <span data-ttu-id="7acf7-119">Se você estiver criando uma única máquina virtual, usar o portal será uma maneira fácil de adicionar proteção da Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="7acf7-119">If you're creating a single virtual machine, using the portal is an easy way to add protection from Trend Micro.</span></span>

<span data-ttu-id="7acf7-120">O uso de uma entrada do **Marketplace** abre um assistente que ajuda você a configurar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7acf7-120">Using an entry from the **Marketplace** opens a wizard that helps you set up the virtual machine.</span></span> <span data-ttu-id="7acf7-121">Você usa a folha **Configurações**, o terceiro painel do assistente, para instalar a extensão de segurança da Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="7acf7-121">You use the **Settings** blade, the third panel of the wizard, to install the Trend Micro security extension.</span></span>  <span data-ttu-id="7acf7-122">Para obter instruções gerais, consulte [Criar uma máquina virtual que executa o Windows no portal do Azure](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="7acf7-122">For general instructions, see [Create a virtual machine running Windows in the Azure portal](tutorial.md).</span></span>

<span data-ttu-id="7acf7-123">Quando chegar à folha **Configurações** do assistente, realize as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="7acf7-123">When you get to the **Settings** blade of the wizard, do the following steps:</span></span>

1. <span data-ttu-id="7acf7-124">Clique em **Extensões** e, em seguida, em **Adicionar extensão** no próximo painel.</span><span class="sxs-lookup"><span data-stu-id="7acf7-124">Click **Extensions**, then click **Add extension** in the next pane.</span></span>

   ![Começar a adicionar a extensão][1]

2. <span data-ttu-id="7acf7-126">Selecione **Deep Security Agent** no painel **Novo recurso**.</span><span class="sxs-lookup"><span data-stu-id="7acf7-126">Select **Deep Security Agent** in the **New resource** pane.</span></span> <span data-ttu-id="7acf7-127">No painel do Deep Security Agent, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="7acf7-127">In the Deep Security Agent pane, click **Create**.</span></span>

   ![Identificar o Deep Security Agent][2]

3. <span data-ttu-id="7acf7-129">Insira o **Identificador de Locatário** e a **Senha de Ativação do Locatário** da extensão.</span><span class="sxs-lookup"><span data-stu-id="7acf7-129">Enter the **Tenant Identifier** and **Tenant Activation Password** for the extension.</span></span> <span data-ttu-id="7acf7-130">Opcionalmente, você pode inserir um **Identificador de Política de Segurança**.</span><span class="sxs-lookup"><span data-stu-id="7acf7-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="7acf7-131">Em seguida, clique em **OK** para adicionar o cliente.</span><span class="sxs-lookup"><span data-stu-id="7acf7-131">Then, click **OK** to add the client.</span></span>

   ![Fornecer detalhes da extensão][3]

## <a name="install-the-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="7acf7-133">Instalar o Agente do Deep Security em uma VM existente</span><span class="sxs-lookup"><span data-stu-id="7acf7-133">Install the Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="7acf7-134">Para instalar o agente em uma VM existente, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="7acf7-134">To install the agent on an existing VM, you need the following items:</span></span>

* <span data-ttu-id="7acf7-135">O módulo do Azure PowerShell versão 0.8.2 ou mais recente instalado no computador local.</span><span class="sxs-lookup"><span data-stu-id="7acf7-135">The Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="7acf7-136">Você pode verificar a versão do Azure PowerShell que tem instalada usando o comando **Get-Module azure | format-table version** .</span><span class="sxs-lookup"><span data-stu-id="7acf7-136">You can check the version of Azure PowerShell that you have installed by using the **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="7acf7-137">Para obter instruções e um link para a versão mais recente, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7acf7-137">For instructions and a link to the latest version, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="7acf7-138">Faça logon em sua assinatura do Azure usando `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="7acf7-138">Log in to your Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="7acf7-139">O agente de VM instalado na máquina virtual de destino.</span><span class="sxs-lookup"><span data-stu-id="7acf7-139">The VM Agent installed on the target virtual machine.</span></span>

<span data-ttu-id="7acf7-140">Primeiramente, verifique se que o agente de VM já está instalado.</span><span class="sxs-lookup"><span data-stu-id="7acf7-140">First, verify that the VM Agent is already installed.</span></span> <span data-ttu-id="7acf7-141">Preencha o nome do serviço de nuvem e o nome da máquina virtual e, em seguida, execute os seguintes comandos em um prompt de comando do Azure PowerShell com nível de administrador.</span><span class="sxs-lookup"><span data-stu-id="7acf7-141">Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="7acf7-142">Substitua tudo entre aspas, incluindo os caracteres < e >.</span><span class="sxs-lookup"><span data-stu-id="7acf7-142">Replace everything within the quotes, including the < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="7acf7-143">Se você não souber o nome da máquina virtual e serviço de nuvem, execute **Get-AzureVM** para exibir essas informações para todas as máquinas virtuais em sua assinatura atual.</span><span class="sxs-lookup"><span data-stu-id="7acf7-143">If you don't know the cloud service and virtual machine name, run **Get-AzureVM** to display that information for all the virtual machines in your current subscription.</span></span>

<span data-ttu-id="7acf7-144">Se o comando **write-host** retornar **True**, o agente da VM estará instalado.</span><span class="sxs-lookup"><span data-stu-id="7acf7-144">If the **write-host** command returns **True**, the VM Agent is installed.</span></span> <span data-ttu-id="7acf7-145">Se ele retornar **False**, confira as instruções e um link para download na postagem do blog do Azure [Agente de VM e extensões - parte 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span><span class="sxs-lookup"><span data-stu-id="7acf7-145">If it returns **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="7acf7-146">Se o Agente de VM estiver instalado, execute estes comandos.</span><span class="sxs-lookup"><span data-stu-id="7acf7-146">If the VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="7acf7-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7acf7-147">Next steps</span></span>
<span data-ttu-id="7acf7-148">Leva alguns minutos para o agente abrir quando ele está instalado.</span><span class="sxs-lookup"><span data-stu-id="7acf7-148">It takes a few minutes for the agent to start running when it is installed.</span></span> <span data-ttu-id="7acf7-149">Depois disso, você precisa ativar o Deep Security na máquina virtual para que ela possa ser gerenciada por um Deep Security Manager.</span><span class="sxs-lookup"><span data-stu-id="7acf7-149">After that, you need to activate Deep Security on the virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="7acf7-150">Consulte os artigos a seguir para obter instruções adicionais:</span><span class="sxs-lookup"><span data-stu-id="7acf7-150">See the following articles for additional instructions:</span></span>

* <span data-ttu-id="7acf7-151">Artigo de tendência sobre essa solução, [Segurança na nuvem Instant-On do Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="7acf7-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="7acf7-152">Um [script do Windows PowerShell de exemplo](http://go.microsoft.com/fwlink/?LinkId=404100) para configurar a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7acf7-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) to configure the virtual machine</span></span>
* <span data-ttu-id="7acf7-153">[Instruções](http://go.microsoft.com/fwlink/?LinkId=404099) para o exemplo</span><span class="sxs-lookup"><span data-stu-id="7acf7-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for the sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7acf7-154">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="7acf7-154">Additional resources</span></span>
<span data-ttu-id="7acf7-155">[Como fazer logon em uma máquina virtual executando o Windows Server]</span><span class="sxs-lookup"><span data-stu-id="7acf7-155">[How to log on to a virtual machine running Windows Server]</span></span>

<span data-ttu-id="7acf7-156">[Recursos e extensões de VM do Azure]</span><span class="sxs-lookup"><span data-stu-id="7acf7-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
<span data-ttu-id="7acf7-157">[Como fazer logon em uma máquina virtual executando o Windows Server]:connect-logon.md</span><span class="sxs-lookup"><span data-stu-id="7acf7-157">[How to log on to a virtual machine running Windows Server]:connect-logon.md</span></span>
<span data-ttu-id="7acf7-158">[Recursos e extensões de VM do Azure]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409</span><span class="sxs-lookup"><span data-stu-id="7acf7-158">[Azure VM Extensions and features]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409</span></span>
