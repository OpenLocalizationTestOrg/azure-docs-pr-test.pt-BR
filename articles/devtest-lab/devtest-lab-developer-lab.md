---
title: Usar o Azure DevTest Labs para desenvolvedores | Microsoft Docs
description: "Saiba como usar o Azure DevTest Labs para cenários de desenvolvedor."
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
ms.openlocfilehash: c187819e9392908c8979556f80e8c94739eb14d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-devtest-labs-for-developers"></a><span data-ttu-id="c1b10-103">Usar o Azure DevTest Labs para desenvolvedores</span><span class="sxs-lookup"><span data-stu-id="c1b10-103">Use Azure DevTest Labs for developers</span></span>
<span data-ttu-id="c1b10-104">O Azure DevTest Labs pode ser usado para implementar vários cenários importantes, mas um dos principais cenários envolve o uso DevTest Labs para hospedar computadores de desenvolvimento para desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="c1b10-104">Azure DevTest Labs can be used to implement many key scenarios, but one of the primary scenarios involves using DevTest Labs to host development machines for developers.</span></span> <span data-ttu-id="c1b10-105">Neste cenário, o DevTest Labs oferece estes benefícios:</span><span class="sxs-lookup"><span data-stu-id="c1b10-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="c1b10-106">Os desenvolvedores podem provisionar rapidamente seus computadores de desenvolvimento sob demanda.</span><span class="sxs-lookup"><span data-stu-id="c1b10-106">Developers can quickly provision their development machines on demand.</span></span>
- <span data-ttu-id="c1b10-107">Os desenvolvedores podem personalizar facilmente seus computadores de desenvolvimento sempre que for necessário.</span><span class="sxs-lookup"><span data-stu-id="c1b10-107">Developers can easily customize their development machines whenever needed.</span></span>
- <span data-ttu-id="c1b10-108">Os administradores podem controlar os custos garantindo que:</span><span class="sxs-lookup"><span data-stu-id="c1b10-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="c1b10-109">Os desenvolvedores não podem utilizar mais VMs do que o necessário para o desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="c1b10-109">Developers cannot get more VMs than they need for development.</span></span>
  - <span data-ttu-id="c1b10-110">As VMs ficam fechadas quando não estão em uso.</span><span class="sxs-lookup"><span data-stu-id="c1b10-110">VMs are shut down when not in use.</span></span> 

![Usar o DevTest Labs para treinamento](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="c1b10-112">Neste artigo, você aprenderá sobre os diversos recursos do Azure DevTest Labs que podem ser usados para atender aos requisitos de desenvolvedor e as etapas detalhadas a seguir para configurar um laboratório.</span><span class="sxs-lookup"><span data-stu-id="c1b10-112">In this article, you learn about various Azure DevTest Labs features that can be used to meet developer requirements and the detailed steps that you can follow to set up a lab.</span></span>

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a><span data-ttu-id="c1b10-113">Implementando ambientes de desenvolvedor com o Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="c1b10-113">Implementing developer environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="c1b10-114">**Criar o laboratório**</span><span class="sxs-lookup"><span data-stu-id="c1b10-114">**Create the lab**</span></span> 
   
    <span data-ttu-id="c1b10-115">Os laboratórios são o ponto de partida no Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="c1b10-115">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="c1b10-116">Depois de criar um laboratório, você pode executar tarefas como adicionar usuários (desenvolvedores) ao laboratório, definir políticas para controlar custos, definir imagens da VM que podem criar rapidamente e muito mais.</span><span class="sxs-lookup"><span data-stu-id="c1b10-116">Once you create a lab, you can perform tasks such as adding users (developers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="c1b10-117">Saiba mais clicando nos links na tabela abaixo:</span><span class="sxs-lookup"><span data-stu-id="c1b10-117">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="c1b10-118">Tarefa</span><span class="sxs-lookup"><span data-stu-id="c1b10-118">Task</span></span> | <span data-ttu-id="c1b10-119">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="c1b10-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="c1b10-120">Criar Laboratórios de Desenvolvimento/Teste do Azure</span><span class="sxs-lookup"><span data-stu-id="c1b10-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="c1b10-121">Saiba como criar um laboratório no Azure DevTest Labs no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1b10-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="c1b10-122">**Criar VMs em minutos usando imagens prontas do marketplace e imagens personalizadas**</span><span class="sxs-lookup"><span data-stu-id="c1b10-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="c1b10-123">Você pode escolher imagens prontas de uma ampla variedade de imagens no Azure Marketplace e torná-las disponíveis no laboratório.</span><span class="sxs-lookup"><span data-stu-id="c1b10-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span></span> <span data-ttu-id="c1b10-124">Se as imagens prontas não atenderem às suas necessidades, você poderá criar uma imagem personalizada criando um laboratório de VM com uma imagem pronta do Azure Marketplace, instalando todos os softwares necessários e salvando a VM como uma imagem personalizada no laboratório.</span><span class="sxs-lookup"><span data-stu-id="c1b10-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span></span>

    <span data-ttu-id="c1b10-125">Se você estiver usando imagens personalizadas, use uma fábrica de imagem para criar e distribuir suas imagens.</span><span class="sxs-lookup"><span data-stu-id="c1b10-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span></span> <span data-ttu-id="c1b10-126">Uma fábrica de imagem é uma solução de configuração como código que normalmente cria e distribui suas imagens configuradas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c1b10-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="c1b10-127">Isso economiza o tempo necessário para configurar manualmente o sistema depois que uma máquina virtual foi criada com o sistema operacional base.</span><span class="sxs-lookup"><span data-stu-id="c1b10-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span></span>
  
    <span data-ttu-id="c1b10-128">Saiba mais clicando nos links na tabela abaixo:</span><span class="sxs-lookup"><span data-stu-id="c1b10-128">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="c1b10-129">Tarefa</span><span class="sxs-lookup"><span data-stu-id="c1b10-129">Task</span></span> | <span data-ttu-id="c1b10-130">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="c1b10-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="c1b10-131">Configurar imagens do Marketplace</span><span class="sxs-lookup"><span data-stu-id="c1b10-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="c1b10-132">Saiba como você pode colocar imagens do Azure Marketplace na lista branca, disponibilizando para seleção apenas as imagens você deseja para os desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="c1b10-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the developers.</span></span>|
   | [<span data-ttu-id="c1b10-133">Criar uma imagem personalizada</span><span class="sxs-lookup"><span data-stu-id="c1b10-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="c1b10-134">Crie uma imagem personalizada instalando previamente o software de que você precisa para que os desenvolvedores possam criar rapidamente uma máquina virtual usando a imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="c1b10-134">Create a custom image by pre-installing the software you need so that developers can quickly create a VM using the custom image.</span></span>|
   | [<span data-ttu-id="c1b10-135">Saiba mais sobre a fábrica de imagem</span><span class="sxs-lookup"><span data-stu-id="c1b10-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="c1b10-136">Assista a um vídeo que descreve como configurar e usar uma fábrica de imagem.</span><span class="sxs-lookup"><span data-stu-id="c1b10-136">Watch a video that describes how to set up and use an image factory.</span></span>|

3. <span data-ttu-id="c1b10-137">**Criar modelos reutilizáveis para máquinas de desenvolvedor**</span><span class="sxs-lookup"><span data-stu-id="c1b10-137">**Create reusable templates for developer machines**</span></span> 
   
    <span data-ttu-id="c1b10-138">Uma fórmula no Azure DevTest Labs é uma lista de valores de propriedade padrão usados para criar uma VM.</span><span class="sxs-lookup"><span data-stu-id="c1b10-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="c1b10-139">Você pode criar uma fórmula no laboratório selecionando uma imagem, um tamanho de VM (uma combinação de CPU e RAM) e uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c1b10-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="c1b10-140">Cada desenvolvedor pode ver a fórmula no laboratório e usá-la para criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c1b10-140">Each developer can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="c1b10-141">Saiba mais clicando nos links na tabela abaixo:</span><span class="sxs-lookup"><span data-stu-id="c1b10-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="c1b10-142">Tarefa</span><span class="sxs-lookup"><span data-stu-id="c1b10-142">Task</span></span> | <span data-ttu-id="c1b10-143">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="c1b10-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="c1b10-144">Gerenciar fórmulas de Laboratórios de Desenvolvimento/Teste para criar VMs</span><span class="sxs-lookup"><span data-stu-id="c1b10-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="c1b10-145">Saiba como você pode criar uma fórmula selecionando uma imagem, um tamanho de VM (uma combinação de CPU e RAM) e uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c1b10-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

4. <span data-ttu-id="c1b10-146">**Criar artefatos para permitir a personalização de VM flexível**</span><span class="sxs-lookup"><span data-stu-id="c1b10-146">**Create artifacts to enable flexible VM customization**</span></span>

   <span data-ttu-id="c1b10-147">Artefatos são usados para implantar e configurar seu aplicativo após o provisionamento de uma VM.</span><span class="sxs-lookup"><span data-stu-id="c1b10-147">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="c1b10-148">Os artefatos podem ser:</span><span class="sxs-lookup"><span data-stu-id="c1b10-148">Artifacts can be:</span></span>

   - <span data-ttu-id="c1b10-149">Ferramentas que você deseja instalar na VM, por exemplo, agentes, Fiddler e Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c1b10-149">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="c1b10-150">Ações que você deseja executar na VM - como clonar um repositório.</span><span class="sxs-lookup"><span data-stu-id="c1b10-150">Actions that you want to run on the VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="c1b10-151">Aplicativos que você deseja testar.</span><span class="sxs-lookup"><span data-stu-id="c1b10-151">Applications that you want to test.</span></span>

   <span data-ttu-id="c1b10-152">Muitos artefatos já estão disponíveis prontos.</span><span class="sxs-lookup"><span data-stu-id="c1b10-152">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="c1b10-153">Você pode criar seus próprios artefatos personalizados se quiser mais personalização para suas necessidades específicas.</span><span class="sxs-lookup"><span data-stu-id="c1b10-153">You can create your own custom artifacts if you want more customization for your specific needs.</span></span>

   <span data-ttu-id="c1b10-154">Saiba mais clicando nos links na tabela abaixo:</span><span class="sxs-lookup"><span data-stu-id="c1b10-154">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="c1b10-155">Tarefa</span><span class="sxs-lookup"><span data-stu-id="c1b10-155">Task</span></span> | <span data-ttu-id="c1b10-156">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="c1b10-156">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="c1b10-157">Criar artefatos personalizados para suas VM dos Laboratórios de Desenvolvimento/Teste</span><span class="sxs-lookup"><span data-stu-id="c1b10-157">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="c1b10-158">Crie seus próprio artefatos personalizados para as máquinas virtuais em seu laboratório.</span><span class="sxs-lookup"><span data-stu-id="c1b10-158">Create your own custom artifacts for the virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="c1b10-159">Adicionar um repositório Git para armazenar os artefatos personalizados e modelos do Azure Resource Manager para uso no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="c1b10-159">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="c1b10-160">Saiba como armazenar os artefatos personalizados em seu próprio repositório de Git privado.</span><span class="sxs-lookup"><span data-stu-id="c1b10-160">Learn how to store your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="c1b10-161">**Controlar os custos**</span><span class="sxs-lookup"><span data-stu-id="c1b10-161">**Control costs**</span></span>
   
    <span data-ttu-id="c1b10-162">O Azure DevTest Labs permite que você defina uma política no laboratório para especificar o número máximo de máquinas virtuais que podem ser criadas por um desenvolvedor no laboratório.</span><span class="sxs-lookup"><span data-stu-id="c1b10-162">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a developer in the lab.</span></span> 
   
    <span data-ttu-id="c1b10-163">Se sua equipe de desenvolvedores tiver definido uma agenda de trabalho e se você quiser interromper todas as VMs em determinado momento do dia para reiniciá-las no dia seguinte, poderá fazer isso facilmente definindo políticas de desligamento automático e início automático no laboratório.</span><span class="sxs-lookup"><span data-stu-id="c1b10-163">If your developer team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="c1b10-164">Finalmente, quando o desenvolvimento de aplicativo estiver concluído, você poderá excluir todas as VMs ao mesmo tempo executando um único script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c1b10-164">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="c1b10-165">Saiba mais clicando nos links na tabela abaixo:</span><span class="sxs-lookup"><span data-stu-id="c1b10-165">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="c1b10-166">Tarefa</span><span class="sxs-lookup"><span data-stu-id="c1b10-166">Task</span></span> | <span data-ttu-id="c1b10-167">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="c1b10-167">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="c1b10-168">Definir políticas de laboratório</span><span class="sxs-lookup"><span data-stu-id="c1b10-168">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="c1b10-169">Controle os custos definindo políticas no laboratório.</span><span class="sxs-lookup"><span data-stu-id="c1b10-169">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="c1b10-170">Excluir todas as VMs do laboratório usando um script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1b10-170">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-can-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="c1b10-171">Exclua todos os laboratórios em uma única operação quando o desenvolvimento for concluído.</span><span class="sxs-lookup"><span data-stu-id="c1b10-171">Delete all the labs in one operation when development is complete.</span></span>|

1. <span data-ttu-id="c1b10-172">**Adicionar uma rede virtual a uma máquina virtual**</span><span class="sxs-lookup"><span data-stu-id="c1b10-172">**Add a virtual network to a VM**</span></span> 
   
    <span data-ttu-id="c1b10-173">O DevTest Labs cria uma nova rede virtual (VNET) sempre que um laboratório for criado.</span><span class="sxs-lookup"><span data-stu-id="c1b10-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="c1b10-174">Se você tiver configurado sua própria rede virtual, por exemplo, usando o ExpressRoute ou VPN site a site, pode adicionar essa rede virtual para as configurações de rede virtual do laboratório para que ele esteja disponível ao criar VMs.</span><span class="sxs-lookup"><span data-stu-id="c1b10-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="c1b10-175">Além disso, há um artefato de associação de domínio do Azure Active Directory disponível que unirá uma máquina virtual a um domínio quando a VM estiver sendo criada.</span><span class="sxs-lookup"><span data-stu-id="c1b10-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM to a domain when the VM is being created.</span></span> 
   
    <span data-ttu-id="c1b10-176">Saiba mais clicando nos links na tabela abaixo:</span><span class="sxs-lookup"><span data-stu-id="c1b10-176">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="c1b10-177">Tarefa</span><span class="sxs-lookup"><span data-stu-id="c1b10-177">Task</span></span> | <span data-ttu-id="c1b10-178">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="c1b10-178">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="c1b10-179">Configurar uma rede virtual no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="c1b10-179">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="c1b10-180">Saiba como configurar uma rede virtual no Azure DevTest Labs usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1b10-180">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span></span>|

6. <span data-ttu-id="c1b10-181">**Compartilhar o laboratório com todos os desenvolvedores**</span><span class="sxs-lookup"><span data-stu-id="c1b10-181">**Share the lab with each developer**</span></span>
   
    <span data-ttu-id="c1b10-182">Os laboratórios podem ser acessados diretamente usando um link que você compartilha com seus desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="c1b10-182">Labs can be directly accessed using a link that you share with your developers.</span></span> <span data-ttu-id="c1b10-183">Eles não precisam ter uma conta do Azure, desde que eles tenham um [conta da Microsoft](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="c1b10-183">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="c1b10-184">Os desenvolvedores não conseguem ver VMs criadas por outros desenvolvedores.</span><span class="sxs-lookup"><span data-stu-id="c1b10-184">Developers cannot see VMs created by other developers.</span></span>  
   
    <span data-ttu-id="c1b10-185">Saiba mais clicando nos links na tabela abaixo:</span><span class="sxs-lookup"><span data-stu-id="c1b10-185">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="c1b10-186">Tarefa</span><span class="sxs-lookup"><span data-stu-id="c1b10-186">Task</span></span> | <span data-ttu-id="c1b10-187">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="c1b10-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="c1b10-188">Adicionar um desenvolvedor a um laboratório no Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="c1b10-188">Add a developer to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="c1b10-189">Use o Portal do Azure para adicionar os desenvolvedores ao laboratório.</span><span class="sxs-lookup"><span data-stu-id="c1b10-189">Use the Azure portal to add developers to your lab.</span></span>|
   | [<span data-ttu-id="c1b10-190">Adicionar desenvolvedores ao laboratório usando um script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="c1b10-190">Add developers to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="c1b10-191">Use o PowerShell para automatizar a adição de desenvolvedores ao seu laboratório.</span><span class="sxs-lookup"><span data-stu-id="c1b10-191">Use PowerShell to automate adding developers to your lab.</span></span> |
   | [<span data-ttu-id="c1b10-192">Obter um link para o laboratório</span><span class="sxs-lookup"><span data-stu-id="c1b10-192">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="c1b10-193">Saiba como os desenvolvedores podem acessar diretamente um laboratório por meio de um hiperlink.</span><span class="sxs-lookup"><span data-stu-id="c1b10-193">Learn how developers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="c1b10-194">**Automatizar a criação de laboratório para mais equipes**</span><span class="sxs-lookup"><span data-stu-id="c1b10-194">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="c1b10-195">Você pode automatizar a criação de laboratórios, incluindo configurações personalizadas, com a criação de um modelo do Resource Manager e usá-lo para criar laboratórios idênticos várias vezes.</span><span class="sxs-lookup"><span data-stu-id="c1b10-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="c1b10-196">Saiba mais clicando nos links na tabela abaixo:</span><span class="sxs-lookup"><span data-stu-id="c1b10-196">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="c1b10-197">Tarefa</span><span class="sxs-lookup"><span data-stu-id="c1b10-197">Task</span></span> | <span data-ttu-id="c1b10-198">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="c1b10-198">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="c1b10-199">Criar um laboratório usando um modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c1b10-199">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-an-azure-resource-manager-template) |<span data-ttu-id="c1b10-200">Crie laboratórios no Azure DevTest Labs usando modelos do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c1b10-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

