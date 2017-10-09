---
title: ambientes de teste do DevTest Labs aaaUse do Azure para VMs e PaaS | Microsoft Docs
description: "Saiba como o DevTest Labs toouse do Azure para VMs e PaaS testar cenários de ambiente."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: tarcher
ms.openlocfilehash: 9285090da768491e1275942318b094fae89e3273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a><span data-ttu-id="82c83-103">Usar o Azure DevTest Labs para ambientes de teste de VM e PaaS</span><span class="sxs-lookup"><span data-stu-id="82c83-103">Use Azure DevTest Labs for VM and PaaS test environments</span></span>

<span data-ttu-id="82c83-104">Você pode usar o Azure DevTest Labs tooimplement muitos cenários de chave, mas um cenário principal envolve o uso de máquinas do DevTest Labs toohost para testadores.</span><span class="sxs-lookup"><span data-stu-id="82c83-104">You can use Azure DevTest Labs tooimplement many key scenarios, but a primary scenario involves using DevTest Labs toohost machines for testers.</span></span> 

<span data-ttu-id="82c83-105">Neste cenário, o DevTest Labs oferece estes benefícios:</span><span class="sxs-lookup"><span data-stu-id="82c83-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="82c83-106">Testadores podem testar a versão mais recente de saudação do seu aplicativo ao provisionar rapidamente ambientes Windows e Linux usando artefatos e modelos reutilizáveis.</span><span class="sxs-lookup"><span data-stu-id="82c83-106">Testers can test hello latest version of their application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span>
- <span data-ttu-id="82c83-107">Os testadores podem escalar verticalmente seu teste de carga provisionando vários agentes de teste.</span><span class="sxs-lookup"><span data-stu-id="82c83-107">Testers can scale up their load testing by provisioning multiple test agents.</span></span>
- <span data-ttu-id="82c83-108">Os administradores podem controlar os custos garantindo que:</span><span class="sxs-lookup"><span data-stu-id="82c83-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="82c83-109">Os testadores não podem obter mais VMs do que o necessário.</span><span class="sxs-lookup"><span data-stu-id="82c83-109">Testers cannot get more VMs than they need.</span></span>
  - <span data-ttu-id="82c83-110">As VMs ficam fechadas quando não estão em uso.</span><span class="sxs-lookup"><span data-stu-id="82c83-110">VMs are shut down when not in use.</span></span>

![Usar o DevTest Labs para treinamento](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="82c83-112">Neste artigo, saiba mais sobre vários requisitos do Azure DevTest Labs recursos usados toomeet testador e Olá etapas detalhadas toofollow tooset um laboratório.</span><span class="sxs-lookup"><span data-stu-id="82c83-112">In this article, you learn about various Azure DevTest Labs features used toomeet tester requirements and hello detailed steps toofollow tooset up a lab.</span></span>

## <a name="implementing-test-environments-with-azure-devtest-labs"></a><span data-ttu-id="82c83-113">Implementando ambientes de teste com o Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="82c83-113">Implementing test environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="82c83-114">**Criar um laboratório de saudação**</span><span class="sxs-lookup"><span data-stu-id="82c83-114">**Create hello lab**</span></span> 
   
    <span data-ttu-id="82c83-115">Laboratórios são Olá ponto de partida no Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="82c83-115">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="82c83-116">Depois de criar um laboratório, você pode executar tarefas como a adição de laboratório de toohello usuários (testadores), custos de toocontrol de políticas de configuração, definindo imagens da VM que podem criar rapidamente e muito mais.</span><span class="sxs-lookup"><span data-stu-id="82c83-116">Once you create a lab, you can perform tasks such as adding users (testers) toohello lab, setting policies toocontrol costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="82c83-117">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="82c83-117">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="82c83-118">Tarefa</span><span class="sxs-lookup"><span data-stu-id="82c83-118">Task</span></span> | <span data-ttu-id="82c83-119">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="82c83-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="82c83-120">Criar Laboratórios de Desenvolvimento/Teste do Azure</span><span class="sxs-lookup"><span data-stu-id="82c83-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="82c83-121">Saiba como toocreate um laboratório no Azure DevTest Labs em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="82c83-121">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="82c83-122">**Criar VMs em minutos usando imagens prontas do marketplace e imagens personalizadas**</span><span class="sxs-lookup"><span data-stu-id="82c83-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="82c83-123">Você pode escolher imagens prontas de uma ampla variedade de imagens em hello Azure Marketplace e disponibilizá-los no laboratório de saudação.</span><span class="sxs-lookup"><span data-stu-id="82c83-123">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available in hello lab.</span></span> <span data-ttu-id="82c83-124">Se imagens prontas Olá não atenderem às suas necessidades, você pode criar uma imagem personalizada, criando um VM usando uma imagem pronta do Azure Marketplace, instalar todos os softwares de saudação que você precisa, e salvando hello VM como uma imagem personalizada no laboratório de saudação do laboratório.</span><span class="sxs-lookup"><span data-stu-id="82c83-124">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need, and saving hello VM as a custom image in hello lab.</span></span>

    <span data-ttu-id="82c83-125">Se você estiver usando imagens personalizadas, considere o uso de um toocreate da fábrica de imagem e distribuir as imagens.</span><span class="sxs-lookup"><span data-stu-id="82c83-125">If you will be using custom images, consider using an image factory toocreate and distribute your images.</span></span> <span data-ttu-id="82c83-126">Uma fábrica de imagem é uma solução de configuração como código que normalmente cria e distribui suas imagens configuradas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="82c83-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="82c83-127">Este toomanually de tempo necessário Olá salva configurar o sistema de saudação depois que uma máquina virtual foi criada com hello base do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="82c83-127">This saves hello time required toomanually configure hello system after a VM has been created with hello base OS.</span></span>
  
    <span data-ttu-id="82c83-128">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="82c83-128">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="82c83-129">Tarefa</span><span class="sxs-lookup"><span data-stu-id="82c83-129">Task</span></span> | <span data-ttu-id="82c83-130">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="82c83-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="82c83-131">Configurar imagens do Marketplace</span><span class="sxs-lookup"><span data-stu-id="82c83-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="82c83-132">Saiba como é possível imagens do Azure Marketplace lista branca, tornando disponíveis para seleção única Olá imagens que você deseja para testadores hello.</span><span class="sxs-lookup"><span data-stu-id="82c83-132">Learn how you can whitelist Azure Marketplace images, making available for selection only hello images you want for hello testers.</span></span>|
   | [<span data-ttu-id="82c83-133">Criar uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="82c83-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="82c83-134">Crie uma imagem personalizada, pré-instalando o software de saudação que é necessário para que os testadores podem criar rapidamente uma máquina virtual usando a imagem personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="82c83-134">Create a custom image by pre-installing hello software you need so that testers can quickly create a VM using hello custom image.</span></span>|
   | [<span data-ttu-id="82c83-135">Saiba mais sobre a fábrica de imagem</span><span class="sxs-lookup"><span data-stu-id="82c83-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="82c83-136">Assista a um vídeo que descreve como tooset up e use uma imagem de fábrica.</span><span class="sxs-lookup"><span data-stu-id="82c83-136">Watch a video that describes how tooset up and use an image factory.</span></span>|

3. <span data-ttu-id="82c83-137">**Criar modelos reutilizáveis para computadores de teste**</span><span class="sxs-lookup"><span data-stu-id="82c83-137">**Create reusable templates for test machines**</span></span> 
   
    <span data-ttu-id="82c83-138">Uma fórmula no Azure DevTest Labs é que uma lista de valores de propriedade padrão usadas toocreate uma VM.</span><span class="sxs-lookup"><span data-stu-id="82c83-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="82c83-139">Você pode criar uma fórmula no laboratório Olá selecionando uma imagem, um tamanho VM (uma combinação de CPU e RAM) e uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="82c83-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="82c83-140">Cada testador pode ver fórmula Olá laboratório hello e use-o toocreate uma VM.</span><span class="sxs-lookup"><span data-stu-id="82c83-140">Each tester can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="82c83-141">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="82c83-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="82c83-142">Tarefa</span><span class="sxs-lookup"><span data-stu-id="82c83-142">Task</span></span> | <span data-ttu-id="82c83-143">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="82c83-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="82c83-144">Gerenciar DevTest Labs fórmulas toocreate VMs</span><span class="sxs-lookup"><span data-stu-id="82c83-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="82c83-145">Saiba como você pode criar uma fórmula selecionando uma imagem, um tamanho de VM (uma combinação de CPU e RAM) e uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="82c83-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

3. <span data-ttu-id="82c83-146">**Criar ambientes de teste com várias VMs**</span><span class="sxs-lookup"><span data-stu-id="82c83-146">**Create multi-VM test environments**</span></span> 
   
    <span data-ttu-id="82c83-147">Você pode usar a infraestrutura do Azure Resource Manager modelos toodefine hello e a configuração de sua solução do Azure e implantar várias vezes teste várias VMs em um estado consistente.</span><span class="sxs-lookup"><span data-stu-id="82c83-147">You can use Azure Resource Manager templates toodefine hello infrastructure and configuration of your Azure solution and repeatedly deploy multiple test VMs in a consistent state.</span></span>

    <span data-ttu-id="82c83-148">Os recursos de PaaS do Azure podem ser provisionados em um ambiente com base em um modelo do Resource Manager e serem exibidos no controle de custos.</span><span class="sxs-lookup"><span data-stu-id="82c83-148">Azure PaaS resources can be provisioned in an environment from a Resource Manager template and appear in cost tracking.</span></span> <span data-ttu-id="82c83-149">No entanto, o desligamento automático VM não é aplicável a tooPaaS recursos.</span><span class="sxs-lookup"><span data-stu-id="82c83-149">However, VM auto shutdown does not apply tooPaaS resources.</span></span>

    <span data-ttu-id="82c83-150">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="82c83-150">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="82c83-151">Tarefa</span><span class="sxs-lookup"><span data-stu-id="82c83-151">Task</span></span> | <span data-ttu-id="82c83-152">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="82c83-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="82c83-153">Crie ambientes de várias VMs e recursos de PaaS com modelos do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="82c83-153">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>](devtest-lab-create-environment-from-arm.md) |<span data-ttu-id="82c83-154">Saiba como você pode implantar várias VMs em um estado consistente no ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="82c83-154">Learn how you can deploy multiple VMs in a consistent state for your test environment.</span></span>|

4. <span data-ttu-id="82c83-155">**Criar artefatos tooenable flexível VM personalização**</span><span class="sxs-lookup"><span data-stu-id="82c83-155">**Create artifacts tooenable flexible VM customization**</span></span>

   <span data-ttu-id="82c83-156">Artefatos são usado toodeploy e configurar seu aplicativo depois que uma VM é provisionada.</span><span class="sxs-lookup"><span data-stu-id="82c83-156">Artifacts are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="82c83-157">Os artefatos podem ser:</span><span class="sxs-lookup"><span data-stu-id="82c83-157">Artifacts can be:</span></span>

   - <span data-ttu-id="82c83-158">Ferramentas que você deseja tooinstall em Olá VM - como agentes, Fiddler e Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="82c83-158">Tools that you want tooinstall on hello VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="82c83-159">Ações que você deseja toorun em Olá VM - como clonar um repositório.</span><span class="sxs-lookup"><span data-stu-id="82c83-159">Actions that you want toorun on hello VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="82c83-160">Aplicativos que você deseja tootest.</span><span class="sxs-lookup"><span data-stu-id="82c83-160">Applications that you want tootest.</span></span>

   <span data-ttu-id="82c83-161">Muitos artefatos já estão disponíveis prontos.</span><span class="sxs-lookup"><span data-stu-id="82c83-161">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="82c83-162">No entanto, se desejar mias personalização para suas necessidades específicas, crie seus próprios artefatos personalizados.</span><span class="sxs-lookup"><span data-stu-id="82c83-162">But if you want more customization for your specific needs, you can create your own custom artifacts.</span></span>

   <span data-ttu-id="82c83-163">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="82c83-163">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="82c83-164">Tarefa</span><span class="sxs-lookup"><span data-stu-id="82c83-164">Task</span></span> | <span data-ttu-id="82c83-165">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="82c83-165">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="82c83-166">Criar artefatos personalizados para suas VM dos Laboratórios de Desenvolvimento/Teste</span><span class="sxs-lookup"><span data-stu-id="82c83-166">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="82c83-167">Crie seus próprio artefatos personalizados para máquinas virtuais de saudação no laboratório.</span><span class="sxs-lookup"><span data-stu-id="82c83-167">Create your own custom artifacts for hello virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="82c83-168">Adicionar um artefatos do Git repositório toostore personalizados e modelos do Gerenciador de recursos do Azure para usar no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="82c83-168">Add a Git repository toostore custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="82c83-169">Saiba como toostore seus artefatos personalizados em seu próprio repositório Git particular.</span><span class="sxs-lookup"><span data-stu-id="82c83-169">Learn how toostore your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="82c83-170">**Controlar os custos**</span><span class="sxs-lookup"><span data-stu-id="82c83-170">**Control costs**</span></span>
   
    <span data-ttu-id="82c83-171">DevTest Labs do Azure permite que você tooset uma política Olá laboratório toospecify Olá número máximo de máquinas virtuais que podem ser criadas por um testador laboratório hello.</span><span class="sxs-lookup"><span data-stu-id="82c83-171">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a tester in hello lab.</span></span> 
   
    <span data-ttu-id="82c83-172">Se sua equipe de teste tem um conjunto a agenda de trabalho e você deseja toostop todas as VMs de saudação em um determinado período do dia hello e, em seguida, automaticamente reiniciá-los Olá após o dia, você pode fazer isso facilmente pelas políticas de desligamento automático e o início automático definindo laboratório hello.</span><span class="sxs-lookup"><span data-stu-id="82c83-172">If your test team has a set work schedule and you want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="82c83-173">Finalmente, quando o desenvolvimento de aplicativos for concluído, você pode excluir todas as VMs de saudação ao mesmo tempo, executando um único script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="82c83-173">Finally, when app development is complete, you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="82c83-174">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="82c83-174">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="82c83-175">Tarefa</span><span class="sxs-lookup"><span data-stu-id="82c83-175">Task</span></span> | <span data-ttu-id="82c83-176">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="82c83-176">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="82c83-177">Definir políticas de laboratório</span><span class="sxs-lookup"><span data-stu-id="82c83-177">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="82c83-178">Controlar os custos, definindo políticas de laboratório hello.</span><span class="sxs-lookup"><span data-stu-id="82c83-178">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="82c83-179">Excluir o laboratório de saudação todas as máquinas virtuais usando um script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="82c83-179">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="82c83-180">Exclua todos os laboratórios de saudação em uma operação quando o teste for concluído.</span><span class="sxs-lookup"><span data-stu-id="82c83-180">Delete all hello labs in one operation when testing is complete.</span></span>|

1. <span data-ttu-id="82c83-181">**Adicionar um laboratório de tooa de rede virtual**</span><span class="sxs-lookup"><span data-stu-id="82c83-181">**Add a virtual network tooa Lab**</span></span> 
   
    <span data-ttu-id="82c83-182">O DevTest Labs cria uma nova rede virtual (VNET) sempre que um laboratório for criado.</span><span class="sxs-lookup"><span data-stu-id="82c83-182">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="82c83-183">Se você configurou sua rede virtual – por exemplo, usando o rota expressa ou VPN site a site – você pode adicionar configurações de rede virtual do laboratório de tooyour essa rede virtual para que ele esteja disponível quando criar máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="82c83-183">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET tooyour lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="82c83-184">Além disso, há um Active Directory do Azure domínio junção artefato disponível que ingressa em um domínio de tooa VM quando Olá VM está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="82c83-184">In addition, there is an Azure Active Directory domain join artifact available that joins a VM tooa domain when hello VM is being created.</span></span> 
   
    <span data-ttu-id="82c83-185">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="82c83-185">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="82c83-186">Tarefa</span><span class="sxs-lookup"><span data-stu-id="82c83-186">Task</span></span> | <span data-ttu-id="82c83-187">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="82c83-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="82c83-188">Configurar uma rede virtual no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="82c83-188">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="82c83-189">Saiba como tooconfigure uma rede virtual no Azure DevTest Labs usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="82c83-189">Learn how tooconfigure a virtual network in Azure DevTest Labs using hello Azure portal.</span></span>|

6. <span data-ttu-id="82c83-190">**Laboratório de saudação do compartilhamento com cada tester**</span><span class="sxs-lookup"><span data-stu-id="82c83-190">**Share hello lab with each tester**</span></span>
   
    <span data-ttu-id="82c83-191">Os laboratórios podem ser acessados diretamente com um link que você compartilha com os testadores.</span><span class="sxs-lookup"><span data-stu-id="82c83-191">Labs can be directly accessed using a link that you share with your testers.</span></span> <span data-ttu-id="82c83-192">Eles não ainda tem toohave uma conta do Azure, desde que elas tenham uma [conta da Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="82c83-192">They don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="82c83-193">Os testadores não podem ver as VMs criadas por outros testadores.</span><span class="sxs-lookup"><span data-stu-id="82c83-193">Testers cannot see VMs created by other testers.</span></span>  
   
    <span data-ttu-id="82c83-194">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="82c83-194">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="82c83-195">Tarefa</span><span class="sxs-lookup"><span data-stu-id="82c83-195">Task</span></span> | <span data-ttu-id="82c83-196">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="82c83-196">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="82c83-197">Adicionar um laboratório de teste tooa no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="82c83-197">Add a tester tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="82c83-198">Use o laboratório de tooyour de testadores Olá tooadd portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="82c83-198">Use hello Azure portal tooadd testers tooyour lab.</span></span>|
   | [<span data-ttu-id="82c83-199">Adicionar o laboratório de toohello testadores usando um script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="82c83-199">Add testers toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="82c83-200">Use o PowerShell tooautomate adicionando o laboratório de tooyour testadores.</span><span class="sxs-lookup"><span data-stu-id="82c83-200">Use PowerShell tooautomate adding testers tooyour lab.</span></span> |
   | [<span data-ttu-id="82c83-201">Obter um laboratório de toohello link</span><span class="sxs-lookup"><span data-stu-id="82c83-201">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="82c83-202">Saiba como os testadores podem acessar diretamente um laboratório por meio de um hiperlink.</span><span class="sxs-lookup"><span data-stu-id="82c83-202">Learn how testers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="82c83-203">**Automatizar a criação de laboratório para mais equipes**</span><span class="sxs-lookup"><span data-stu-id="82c83-203">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="82c83-204">Você pode automatizar a criação de laboratório, incluindo configurações personalizadas, criando um modelo do Gerenciador de recursos e usando laboratórios idênticos toocreate repetidamente.</span><span class="sxs-lookup"><span data-stu-id="82c83-204">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="82c83-205">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="82c83-205">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="82c83-206">Tarefa</span><span class="sxs-lookup"><span data-stu-id="82c83-206">Task</span></span> | <span data-ttu-id="82c83-207">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="82c83-207">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="82c83-208">Criar um laboratório usando um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="82c83-208">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="82c83-209">Crie laboratórios no Azure DevTest Labs usando modelos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="82c83-209">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

