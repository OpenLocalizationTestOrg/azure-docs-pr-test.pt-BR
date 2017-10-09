---
title: aaaUse DevTest Labs do Azure para desenvolvedores | Microsoft Docs
description: "Saiba como toouse Azure DevTest Labs para cenários de desenvolvedor."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 22e070e5-3d1a-49fe-9d4c-5e07cb0b7fe2
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: tarcher
ms.openlocfilehash: 16a3ef47c9fcbca3050dd50db5b472a9a1e3c62c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a><span data-ttu-id="de79a-103">Usar o Azure DevTest Labs para desenvolvedores</span><span class="sxs-lookup"><span data-stu-id="de79a-103">Use Azure DevTest Labs for developers</span></span>
<span data-ttu-id="de79a-104">Azure DevTest Labs pode ser usado tooimplement muitos cenários de chave, mas um dos principais cenários de saudação envolve o uso de computadores de desenvolvimento do DevTest Labs toohost para desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="de79a-104">Azure DevTest Labs can be used tooimplement many key scenarios, but one of hello primary scenarios involves using DevTest Labs toohost development machines for developers.</span></span> <span data-ttu-id="de79a-105">Neste cenário, o DevTest Labs oferece estes benefícios:</span><span class="sxs-lookup"><span data-stu-id="de79a-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="de79a-106">Os desenvolvedores podem provisionar rapidamente seus computadores de desenvolvimento sob demanda.</span><span class="sxs-lookup"><span data-stu-id="de79a-106">Developers can quickly provision their development machines on demand.</span></span>
- <span data-ttu-id="de79a-107">Os desenvolvedores podem personalizar facilmente seus computadores de desenvolvimento sempre que for necessário.</span><span class="sxs-lookup"><span data-stu-id="de79a-107">Developers can easily customize their development machines whenever needed.</span></span>
- <span data-ttu-id="de79a-108">Os administradores podem controlar os custos garantindo que:</span><span class="sxs-lookup"><span data-stu-id="de79a-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="de79a-109">Os desenvolvedores não podem utilizar mais VMs do que o necessário para o desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="de79a-109">Developers cannot get more VMs than they need for development.</span></span>
  - <span data-ttu-id="de79a-110">As VMs ficam fechadas quando não estão em uso.</span><span class="sxs-lookup"><span data-stu-id="de79a-110">VMs are shut down when not in use.</span></span> 

![Usar o DevTest Labs para treinamento](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="de79a-112">Neste artigo, você aprenderá sobre vários recursos do Azure DevTest Labs que podem ser usados toomeet requisitos de desenvolvedor e Olá etapas detalhadas que você pode seguir tooset um laboratório.</span><span class="sxs-lookup"><span data-stu-id="de79a-112">In this article, you learn about various Azure DevTest Labs features that can be used toomeet developer requirements and hello detailed steps that you can follow tooset up a lab.</span></span>

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a><span data-ttu-id="de79a-113">Implementando ambientes de desenvolvedor com o Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="de79a-113">Implementing developer environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="de79a-114">**Criar um laboratório de saudação**</span><span class="sxs-lookup"><span data-stu-id="de79a-114">**Create hello lab**</span></span> 
   
    <span data-ttu-id="de79a-115">Laboratórios são Olá ponto de partida no Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="de79a-115">Labs are hello starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="de79a-116">Depois de criar um laboratório, você pode executar tarefas como a adição de laboratório de toohello usuários (desenvolvedores), custos de toocontrol de políticas de configuração, definindo imagens da VM que podem criar rapidamente e muito mais.</span><span class="sxs-lookup"><span data-stu-id="de79a-116">Once you create a lab, you can perform tasks such as adding users (developers) toohello lab, setting policies toocontrol costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="de79a-117">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="de79a-117">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="de79a-118">Tarefa</span><span class="sxs-lookup"><span data-stu-id="de79a-118">Task</span></span> | <span data-ttu-id="de79a-119">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="de79a-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="de79a-120">Criar Laboratórios de Desenvolvimento/Teste do Azure</span><span class="sxs-lookup"><span data-stu-id="de79a-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="de79a-121">Saiba como toocreate um laboratório no Azure DevTest Labs em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="de79a-121">Learn how toocreate a lab in Azure DevTest Labs in hello Azure portal.</span></span> |
2. <span data-ttu-id="de79a-122">**Criar VMs em minutos usando imagens prontas do marketplace e imagens personalizadas**</span><span class="sxs-lookup"><span data-stu-id="de79a-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="de79a-123">Você pode escolher imagens prontas de uma ampla variedade de imagens em hello Azure Marketplace e disponibilizá-los no laboratório de saudação.</span><span class="sxs-lookup"><span data-stu-id="de79a-123">You can pick ready-made images from a wide variety of images in hello Azure Marketplace and make them available in hello lab.</span></span> <span data-ttu-id="de79a-124">Se imagens prontas Olá não atenderem às suas necessidades, você pode criar uma imagem personalizada, criando um VM usando uma imagem pronta do Azure Marketplace, instalar todos os softwares de saudação que você precisa, e salvando hello VM como uma imagem personalizada no laboratório de saudação do laboratório.</span><span class="sxs-lookup"><span data-stu-id="de79a-124">If hello ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all hello software that you need, and saving hello VM as a custom image in hello lab.</span></span>

    <span data-ttu-id="de79a-125">Se você estiver usando imagens personalizadas, considere o uso de um toocreate da fábrica de imagem e distribuir as imagens.</span><span class="sxs-lookup"><span data-stu-id="de79a-125">If you will be using custom images, consider using an image factory toocreate and distribute your images.</span></span> <span data-ttu-id="de79a-126">Uma fábrica de imagem é uma solução de configuração como código que normalmente cria e distribui suas imagens configuradas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="de79a-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="de79a-127">Este toomanually de tempo necessário Olá salva configurar o sistema de saudação depois que uma máquina virtual foi criada com hello base do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="de79a-127">This saves hello time required toomanually configure hello system after a VM has been created with hello base OS.</span></span>
  
    <span data-ttu-id="de79a-128">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="de79a-128">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="de79a-129">Tarefa</span><span class="sxs-lookup"><span data-stu-id="de79a-129">Task</span></span> | <span data-ttu-id="de79a-130">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="de79a-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="de79a-131">Configurar imagens do Marketplace</span><span class="sxs-lookup"><span data-stu-id="de79a-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="de79a-132">Saiba como é possível lista branca imagens do Azure Marketplace, tornando disponível para seleção única Olá imagens desejado para os desenvolvedores de saudação.</span><span class="sxs-lookup"><span data-stu-id="de79a-132">Learn how you can whitelist Azure Marketplace images, making available for selection only hello images you want for hello developers.</span></span>|
   | [<span data-ttu-id="de79a-133">Criar uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="de79a-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="de79a-134">Crie uma imagem personalizada, pré-instalando o software de saudação que é necessário para que os desenvolvedores podem criar rapidamente uma máquina virtual usando a imagem personalizada hello.</span><span class="sxs-lookup"><span data-stu-id="de79a-134">Create a custom image by pre-installing hello software you need so that developers can quickly create a VM using hello custom image.</span></span>|
   | [<span data-ttu-id="de79a-135">Saiba mais sobre a fábrica de imagem</span><span class="sxs-lookup"><span data-stu-id="de79a-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="de79a-136">Assista a um vídeo que descreve como tooset up e use uma imagem de fábrica.</span><span class="sxs-lookup"><span data-stu-id="de79a-136">Watch a video that describes how tooset up and use an image factory.</span></span>|

3. <span data-ttu-id="de79a-137">**Criar modelos reutilizáveis para máquinas de desenvolvedor**</span><span class="sxs-lookup"><span data-stu-id="de79a-137">**Create reusable templates for developer machines**</span></span> 
   
    <span data-ttu-id="de79a-138">Uma fórmula no Azure DevTest Labs é que uma lista de valores de propriedade padrão usadas toocreate uma VM.</span><span class="sxs-lookup"><span data-stu-id="de79a-138">A formula in Azure DevTest Labs is a list of default property values used toocreate a VM.</span></span> <span data-ttu-id="de79a-139">Você pode criar uma fórmula no laboratório Olá selecionando uma imagem, um tamanho VM (uma combinação de CPU e RAM) e uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="de79a-139">You can create a formula in hello lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="de79a-140">Cada desenvolvedor pode ver fórmula Olá laboratório hello e use-a como toocreate uma VM.</span><span class="sxs-lookup"><span data-stu-id="de79a-140">Each developer can see hello formula in hello lab and use it toocreate a VM.</span></span> 
   
    <span data-ttu-id="de79a-141">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="de79a-141">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="de79a-142">Tarefa</span><span class="sxs-lookup"><span data-stu-id="de79a-142">Task</span></span> | <span data-ttu-id="de79a-143">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="de79a-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="de79a-144">Gerenciar DevTest Labs fórmulas toocreate VMs</span><span class="sxs-lookup"><span data-stu-id="de79a-144">Manage DevTest Labs formulas toocreate VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="de79a-145">Saiba como você pode criar uma fórmula selecionando uma imagem, um tamanho de VM (uma combinação de CPU e RAM) e uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="de79a-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

4. <span data-ttu-id="de79a-146">**Criar artefatos tooenable flexível VM personalização**</span><span class="sxs-lookup"><span data-stu-id="de79a-146">**Create artifacts tooenable flexible VM customization**</span></span>

   <span data-ttu-id="de79a-147">Artefatos são usado toodeploy e configurar seu aplicativo depois que uma VM é provisionada.</span><span class="sxs-lookup"><span data-stu-id="de79a-147">Artifacts are used toodeploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="de79a-148">Os artefatos podem ser:</span><span class="sxs-lookup"><span data-stu-id="de79a-148">Artifacts can be:</span></span>

   - <span data-ttu-id="de79a-149">Ferramentas que você deseja tooinstall em Olá VM - como agentes, Fiddler e Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de79a-149">Tools that you want tooinstall on hello VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="de79a-150">Ações que você deseja toorun em Olá VM - como clonar um repositório.</span><span class="sxs-lookup"><span data-stu-id="de79a-150">Actions that you want toorun on hello VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="de79a-151">Aplicativos que você deseja tootest.</span><span class="sxs-lookup"><span data-stu-id="de79a-151">Applications that you want tootest.</span></span>

   <span data-ttu-id="de79a-152">Muitos artefatos já estão disponíveis prontos.</span><span class="sxs-lookup"><span data-stu-id="de79a-152">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="de79a-153">Você pode criar seus próprios artefatos personalizados se quiser mais personalização para suas necessidades específicas.</span><span class="sxs-lookup"><span data-stu-id="de79a-153">You can create your own custom artifacts if you want more customization for your specific needs.</span></span>

   <span data-ttu-id="de79a-154">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="de79a-154">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="de79a-155">Tarefa</span><span class="sxs-lookup"><span data-stu-id="de79a-155">Task</span></span> | <span data-ttu-id="de79a-156">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="de79a-156">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="de79a-157">Criar artefatos personalizados para suas VM dos Laboratórios de Desenvolvimento/Teste</span><span class="sxs-lookup"><span data-stu-id="de79a-157">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="de79a-158">Crie seus próprio artefatos personalizados para máquinas virtuais de saudação no laboratório.</span><span class="sxs-lookup"><span data-stu-id="de79a-158">Create your own custom artifacts for hello virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="de79a-159">Adicionar um artefatos do Git repositório toostore personalizados e modelos do Gerenciador de recursos do Azure para usar no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="de79a-159">Add a Git repository toostore custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="de79a-160">Saiba como toostore seus artefatos personalizados em seu próprio repositório Git particular.</span><span class="sxs-lookup"><span data-stu-id="de79a-160">Learn how toostore your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="de79a-161">**Controlar os custos**</span><span class="sxs-lookup"><span data-stu-id="de79a-161">**Control costs**</span></span>
   
    <span data-ttu-id="de79a-162">DevTest Labs do Azure permite que você tooset uma política Olá laboratório toospecify Olá número máximo de máquinas virtuais que podem ser criadas por um desenvolvedor em laboratório hello.</span><span class="sxs-lookup"><span data-stu-id="de79a-162">Azure DevTest Labs allows you tooset a policy in hello lab toospecify hello maximum number of VMs that can be created by a developer in hello lab.</span></span> 
   
    <span data-ttu-id="de79a-163">Se sua equipe de desenvolvedor tem um conjunto a agenda de trabalho e você deseja toostop todas as VMs de saudação em um determinado período do dia hello e, em seguida, automaticamente reiniciá-los Olá após o dia, você pode fazer isso facilmente pelas políticas de desligamento automático e o início automático definindo laboratório hello.</span><span class="sxs-lookup"><span data-stu-id="de79a-163">If your developer team has a set work schedule and you want toostop all hello VMs at a particular time of hello day and then automatically restart them hello following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in hello lab.</span></span> 
   
    <span data-ttu-id="de79a-164">Finalmente, quando o desenvolvimento de aplicativos for concluído, você pode excluir todas as VMs de saudação ao mesmo tempo, executando um único script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de79a-164">Finally, when app development is complete, you can delete all hello VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="de79a-165">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="de79a-165">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="de79a-166">Tarefa</span><span class="sxs-lookup"><span data-stu-id="de79a-166">Task</span></span> | <span data-ttu-id="de79a-167">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="de79a-167">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="de79a-168">Definir políticas de laboratório</span><span class="sxs-lookup"><span data-stu-id="de79a-168">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="de79a-169">Controlar os custos, definindo políticas de laboratório hello.</span><span class="sxs-lookup"><span data-stu-id="de79a-169">Control costs by setting policies in hello lab.</span></span> |
   | [<span data-ttu-id="de79a-170">Excluir o laboratório de saudação todas as máquinas virtuais usando um script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="de79a-170">Delete all hello lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="de79a-171">Exclua todos os laboratórios de saudação em uma única operação quando o desenvolvimento é concluído.</span><span class="sxs-lookup"><span data-stu-id="de79a-171">Delete all hello labs in one operation when development is complete.</span></span>|

1. <span data-ttu-id="de79a-172">**Adicionar uma tooa de rede virtual VM**</span><span class="sxs-lookup"><span data-stu-id="de79a-172">**Add a virtual network tooa VM**</span></span> 
   
    <span data-ttu-id="de79a-173">O DevTest Labs cria uma nova rede virtual (VNET) sempre que um laboratório for criado.</span><span class="sxs-lookup"><span data-stu-id="de79a-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="de79a-174">Se você configurou sua rede virtual – por exemplo, usando o rota expressa ou VPN site a site – você pode adicionar configurações de rede virtual do laboratório de tooyour essa rede virtual para que ele esteja disponível quando criar máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="de79a-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET tooyour lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="de79a-175">Além disso, há um artefato de junção de domínio Active Directory do Azure disponível que serão ingressar em um domínio de tooa VM quando Olá VM está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="de79a-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM tooa domain when hello VM is being created.</span></span> 
   
    <span data-ttu-id="de79a-176">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="de79a-176">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="de79a-177">Tarefa</span><span class="sxs-lookup"><span data-stu-id="de79a-177">Task</span></span> | <span data-ttu-id="de79a-178">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="de79a-178">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="de79a-179">Configurar uma rede virtual no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="de79a-179">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="de79a-180">Saiba como tooconfigure uma rede virtual no Azure DevTest Labs usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="de79a-180">Learn how tooconfigure a virtual network in Azure DevTest Labs using hello Azure portal.</span></span>|

6. <span data-ttu-id="de79a-181">**Laboratório de saudação do compartilhamento com cada desenvolvedor**</span><span class="sxs-lookup"><span data-stu-id="de79a-181">**Share hello lab with each developer**</span></span>
   
    <span data-ttu-id="de79a-182">Os laboratórios podem ser acessados diretamente usando um link que você compartilha com seus desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="de79a-182">Labs can be directly accessed using a link that you share with your developers.</span></span> <span data-ttu-id="de79a-183">Eles não ainda tem toohave uma conta do Azure, desde que elas tenham uma [conta da Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="de79a-183">They don't even have toohave an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="de79a-184">Os desenvolvedores não conseguem ver VMs criadas por outros desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="de79a-184">Developers cannot see VMs created by other developers.</span></span>  
   
    <span data-ttu-id="de79a-185">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="de79a-185">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="de79a-186">Tarefa</span><span class="sxs-lookup"><span data-stu-id="de79a-186">Task</span></span> | <span data-ttu-id="de79a-187">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="de79a-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="de79a-188">Adicionar um laboratório de tooa do desenvolvedor no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="de79a-188">Add a developer tooa lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="de79a-189">Use laboratório de tooyour de desenvolvedores Olá tooadd portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="de79a-189">Use hello Azure portal tooadd developers tooyour lab.</span></span>|
   | [<span data-ttu-id="de79a-190">Adicionar o laboratório de toohello desenvolvedores usando um script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="de79a-190">Add developers toohello lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="de79a-191">Use o PowerShell tooautomate adicionando o laboratório de tooyour de desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="de79a-191">Use PowerShell tooautomate adding developers tooyour lab.</span></span> |
   | [<span data-ttu-id="de79a-192">Obter um laboratório de toohello link</span><span class="sxs-lookup"><span data-stu-id="de79a-192">Get a link toohello lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="de79a-193">Saiba como os desenvolvedores podem acessar diretamente um laboratório por meio de um hiperlink.</span><span class="sxs-lookup"><span data-stu-id="de79a-193">Learn how developers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="de79a-194">**Automatizar a criação de laboratório para mais equipes**</span><span class="sxs-lookup"><span data-stu-id="de79a-194">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="de79a-195">Você pode automatizar a criação de laboratório, incluindo configurações personalizadas, criando um modelo do Gerenciador de recursos e usando laboratórios idênticos toocreate repetidamente.</span><span class="sxs-lookup"><span data-stu-id="de79a-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it toocreate identical labs again and again.</span></span> 
   
    <span data-ttu-id="de79a-196">Saiba mais, basta clicar em links Olá Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="de79a-196">Learn more by clicking on hello links in hello following table:</span></span>
   
   | <span data-ttu-id="de79a-197">Tarefa</span><span class="sxs-lookup"><span data-stu-id="de79a-197">Task</span></span> | <span data-ttu-id="de79a-198">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="de79a-198">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="de79a-199">Criar um laboratório usando um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="de79a-199">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="de79a-200">Crie laboratórios no Azure DevTest Labs usando modelos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="de79a-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

