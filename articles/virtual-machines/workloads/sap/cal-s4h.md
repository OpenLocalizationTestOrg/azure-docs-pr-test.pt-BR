---
title: Implantar o SAP S/4HANA ou o BW/4HANA em uma VM do Azure | Microsoft Docs
description: Implantar o SAP S/4HANA ou o BW/4HANA em uma VM do Azure
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 4788fa14a6c49d39b5a3096a69b6738f4a5d8cca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="844b0-103">Implantar o SAP S/4HANA ou o BW/4HANA no Azure</span><span class="sxs-lookup"><span data-stu-id="844b0-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="844b0-104">Este artigo descreve como implantar o S/4HANA no Azure usando o SAP CAL (SAP Cloud Appliance Library) 3.0.</span><span class="sxs-lookup"><span data-stu-id="844b0-104">This article describes how to deploy S/4HANA on Azure by using the SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="844b0-105">Para implantar outras soluções baseadas em SAP HANA, como BW/4HANA, siga as mesmas etapas.</span><span class="sxs-lookup"><span data-stu-id="844b0-105">To deploy other SAP HANA-based solutions, such as BW/4HANA, follow the same steps.</span></span>

> [!NOTE]
<span data-ttu-id="844b0-106">Para obter mais informações sobre a SAP CAL, consulte o site [SAP Cloud Appliance Library](https://cal.sap.com/).</span><span class="sxs-lookup"><span data-stu-id="844b0-106">For more information about the SAP CAL, go to the [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="844b0-107">A SAP também tem um blog sobre a [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="844b0-107">SAP also has a blog about the [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="844b0-108">A partir de 29 de maio de 2017, você pode usar o modelo de implantação do Azure Resource Manager além do modelo de implantação clássico menos preferencial para implantar a SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="844b0-108">As of May 29, 2017, you can use the Azure Resource Manager deployment model in addition to the less-preferred classic deployment model to deploy the SAP CAL.</span></span> <span data-ttu-id="844b0-109">É recomendável que você use o novo modelo de implantação do Resource Manager e ignore o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="844b0-109">We recommend that you use the new Resource Manager deployment model and disregard the classic deployment model.</span></span>

## <a name="step-by-step-process-to-deploy-the-solution"></a><span data-ttu-id="844b0-110">Processo passo a passo para implantar a solução</span><span class="sxs-lookup"><span data-stu-id="844b0-110">Step-by-step process to deploy the solution</span></span>

<span data-ttu-id="844b0-111">A sequência de capturas de tela a seguir mostra como implantar a S/4HANA no Azure usando a SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="844b0-111">The following sequence of screenshots shows you how to deploy S/4HANA on Azure by using the SAP CAL.</span></span> <span data-ttu-id="844b0-112">O processo funciona da mesma maneira para outras soluções, como o BW/4HANA.</span><span class="sxs-lookup"><span data-stu-id="844b0-112">The process works the same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="844b0-113">A página **Soluções** mostra algumas soluções baseadas no SAP CAL HANA disponíveis no Azure.</span><span class="sxs-lookup"><span data-stu-id="844b0-113">The **Solutions** page shows some of the SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="844b0-114">**SAP S/4HANA 1610 FPS01, dispositivo completamente ativado** está na linha do meio:</span><span class="sxs-lookup"><span data-stu-id="844b0-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in the middle row:</span></span>

![Soluções de SAP CAL](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-the-sap-cal"></a><span data-ttu-id="844b0-116">Criar uma conta na SAP CAL</span><span class="sxs-lookup"><span data-stu-id="844b0-116">Create an account in the SAP CAL</span></span>
1. <span data-ttu-id="844b0-117">Para entrar na SAP CAL pela primeira vez, use o seu SAP S-User ou outro usuário registrado com a SAP.</span><span class="sxs-lookup"><span data-stu-id="844b0-117">To sign in to the SAP CAL for the first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="844b0-118">Em seguida, defina uma conta da SAP CAL que é usada pela SAP CAL para implantar dispositivos no Azure.</span><span class="sxs-lookup"><span data-stu-id="844b0-118">Then define an SAP CAL account that is used by the SAP CAL to deploy appliances on Azure.</span></span> <span data-ttu-id="844b0-119">Na definição de conta, você precisa:</span><span class="sxs-lookup"><span data-stu-id="844b0-119">In the account definition, you need to:</span></span>

    <span data-ttu-id="844b0-120">a.</span><span class="sxs-lookup"><span data-stu-id="844b0-120">a.</span></span> <span data-ttu-id="844b0-121">Selecionar o modelo de implantação no Azure (Resource Manager ou clássico).</span><span class="sxs-lookup"><span data-stu-id="844b0-121">Select the deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="844b0-122">b.</span><span class="sxs-lookup"><span data-stu-id="844b0-122">b.</span></span> <span data-ttu-id="844b0-123">Inserir sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="844b0-123">Enter your Azure subscription.</span></span> <span data-ttu-id="844b0-124">Uma conta da SAP CAL pode ser atribuída a apenas uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="844b0-124">An SAP CAL account can be assigned to one subscription only.</span></span> <span data-ttu-id="844b0-125">Se você precisar de mais de uma assinatura, precisará criar uma outra conta da SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="844b0-125">If you need more than one subscription, you need to create another SAP CAL account.</span></span>

    <span data-ttu-id="844b0-126">c.</span><span class="sxs-lookup"><span data-stu-id="844b0-126">c.</span></span> <span data-ttu-id="844b0-127">Conceder a permissão da SAP CAL para implantar em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="844b0-127">Give the SAP CAL permission to deploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="844b0-128">As próximas etapas mostram como criar uma conta da SAP CAL para implantações do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="844b0-128">The next steps show how to create an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="844b0-129">Se você já tiver uma conta da SAP CAL que está vinculada ao modelo de implantação clássico, é *necessário* seguir estas etapas para criar uma nova conta da SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="844b0-129">If you already have an SAP CAL account that is linked to the classic deployment model, you *need* to follow these steps to create a new SAP CAL account.</span></span> <span data-ttu-id="844b0-130">A nova conta da SAP CAL precisa ser implantada no modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="844b0-130">The new SAP CAL account needs to deploy in the Resource Manager model.</span></span>

2. <span data-ttu-id="844b0-131">Crie uma nova conta do SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="844b0-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="844b0-132">A página **Contas** mostra três opções para o Azure:</span><span class="sxs-lookup"><span data-stu-id="844b0-132">The **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="844b0-133">a.</span><span class="sxs-lookup"><span data-stu-id="844b0-133">a.</span></span> <span data-ttu-id="844b0-134">**Microsoft Azure (clássico)** é o modelo de implantação clássico e não é mais preferencial.</span><span class="sxs-lookup"><span data-stu-id="844b0-134">**Microsoft Azure (classic)** is the classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="844b0-135">b.</span><span class="sxs-lookup"><span data-stu-id="844b0-135">b.</span></span> <span data-ttu-id="844b0-136">**Microsoft Azure** é o novo modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="844b0-136">**Microsoft Azure** is the new Resource Manager deployment model.</span></span>

    <span data-ttu-id="844b0-137">c.</span><span class="sxs-lookup"><span data-stu-id="844b0-137">c.</span></span> <span data-ttu-id="844b0-138">**Windows Azure operado pela 21Vianet** é uma opção na China que usa o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="844b0-138">**Windows Azure operated by 21Vianet** is an option in China that uses the classic deployment model.</span></span>

    <span data-ttu-id="844b0-139">Para implantar no modelo do Resource Manager, selecione **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="844b0-139">To deploy in the Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Detalhes da conta da SAP CAL](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="844b0-141">Insira a **ID da assinatura** do Azure que pode ser encontrada no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="844b0-141">Enter the Azure **Subscription ID** that can be found on the Azure portal.</span></span>

   ![Contas da SAP CAL](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="844b0-143">Para autorizar a SAP CAL para implantar na assinatura do Azure que você definiu, clique em **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="844b0-143">To authorize the SAP CAL to deploy into the Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="844b0-144">A seguinte página será exibida na guia do navegador:</span><span class="sxs-lookup"><span data-stu-id="844b0-144">The following page appears in the browser tab:</span></span>

   ![Entrar nos serviços de nuvem do Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="844b0-146">Se mais de um usuário estiver listado, escolha a conta da Microsoft que está vinculada para ser o coadministrador da assinatura do Azure que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="844b0-146">If more than one user is listed, choose the Microsoft account that is linked to be the coadministrator of the Azure subscription you selected.</span></span> <span data-ttu-id="844b0-147">A seguinte página será exibida na guia do navegador:</span><span class="sxs-lookup"><span data-stu-id="844b0-147">The following page appears in the browser tab:</span></span>

   ![Confirmação dos serviços de nuvem do Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="844b0-149">Clique em **Aceitar**.</span><span class="sxs-lookup"><span data-stu-id="844b0-149">Click **Accept**.</span></span> <span data-ttu-id="844b0-150">Se a autorização for bem-sucedido, a definição de conta da SAP CAL será exibida novamente.</span><span class="sxs-lookup"><span data-stu-id="844b0-150">If the authorization is successful, the SAP CAL account definition displays again.</span></span> <span data-ttu-id="844b0-151">Após um curto período de tempo, uma mensagem confirmará que o processo de autorização foi bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="844b0-151">After a short time, a message confirms that the authorization process was successful.</span></span>

7. <span data-ttu-id="844b0-152">Para atribuir a conta da CAL SAP recém-criada ao seu usuário, insira sua **ID de usuário** na caixa de texto à direita e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="844b0-152">To assign the newly created SAP CAL account to your user, enter your **User ID** in the text box on the right and click **Add**.</span></span>

   ![Conta a ser associada ao usuário](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="844b0-154">Para associar sua conta com o usuário que você usa para entrar na SAP CAL, clique em **Análise**.</span><span class="sxs-lookup"><span data-stu-id="844b0-154">To associate your account with the user that you use to sign in to the SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="844b0-155">Para criar a associação entre o usuário e a conta da CAL SAP recém-criada, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="844b0-155">To create the association between your user and the newly created SAP CAL account, click **Create**.</span></span>

   ![Usuário para a associação de conta da SAP CAL](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="844b0-157">Você criou com êxito uma conta da SAP CAL que é capaz de:</span><span class="sxs-lookup"><span data-stu-id="844b0-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="844b0-158">Usar o Modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="844b0-158">Use the Resource Manager deployment model.</span></span>
- <span data-ttu-id="844b0-159">Implantar os sistemas SAP na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="844b0-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="844b0-160">Agora você pode começar a implantar a 4HANA/S em sua assinatura do usuário no Azure.</span><span class="sxs-lookup"><span data-stu-id="844b0-160">Now you can start to deploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="844b0-161">Antes de continuar, determine se você tem cotas de núcleo do Azure para as VMs Série H do Azure.</span><span class="sxs-lookup"><span data-stu-id="844b0-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="844b0-162">No momento, a SAP CAL usa VMs Série H do Azure para implantar algumas das soluções com base em SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="844b0-162">At the moment, the SAP CAL uses H-Series VMs of Azure to deploy some of the SAP HANA-based solutions.</span></span> <span data-ttu-id="844b0-163">Sua assinatura do Azure talvez não tenha cotas de núcleo da Série H para a Série H.</span><span class="sxs-lookup"><span data-stu-id="844b0-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="844b0-164">Nesse caso, talvez seja necessário entrar em contato com o suporte do Azure para obter uma cota de pelo menos 16 núcleos da Série H.</span><span class="sxs-lookup"><span data-stu-id="844b0-164">If so, you might need to contact Azure support to get a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="844b0-165">Quando você implanta uma solução no Azure com a SAP CAL, talvez você descubra que pode escolher apenas uma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="844b0-165">When you deploy a solution on Azure in the SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="844b0-166">Para implantar em regiões do Azure diferentes daquele sugeridas pela SAP CAL, você precisa comprar uma assinatura da CAL da SAP.</span><span class="sxs-lookup"><span data-stu-id="844b0-166">To deploy into Azure regions other than the one suggested by the SAP CAL, you need to purchase a CAL subscription from SAP.</span></span> <span data-ttu-id="844b0-167">Você também precisará abrir uma mensagem com a SAP para ter sua conta da CAL habilitada para entregar em regiões do Azure diferentes daquelas inicialmente sugeridas.</span><span class="sxs-lookup"><span data-stu-id="844b0-167">You also might need to open a message with SAP to have your CAL account enabled to deliver into Azure regions other than the ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="844b0-168">Implantar uma solução</span><span class="sxs-lookup"><span data-stu-id="844b0-168">Deploy a solution</span></span>

<span data-ttu-id="844b0-169">Permite implantar uma solução a partir da página **Soluções** da SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="844b0-169">Let's deploy a solution from the **Solutions** page of the SAP CAL.</span></span> <span data-ttu-id="844b0-170">A SAP CAL tem duas sequências para implantação:</span><span class="sxs-lookup"><span data-stu-id="844b0-170">The SAP CAL has two sequences to deploy:</span></span>

- <span data-ttu-id="844b0-171">Uma sequência básica que usa uma página para definir o sistema a ser implantado</span><span class="sxs-lookup"><span data-stu-id="844b0-171">A basic sequence that uses one page to define the system to be deployed</span></span>
- <span data-ttu-id="844b0-172">Uma sequência avançada que fornece certas opções sobre tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="844b0-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="844b0-173">Demonstramos o caminho básico para implantação aqui.</span><span class="sxs-lookup"><span data-stu-id="844b0-173">We demonstrate the basic path to deployment here.</span></span>

1. <span data-ttu-id="844b0-174">Na página **Detalhes da conta**, você precisa:</span><span class="sxs-lookup"><span data-stu-id="844b0-174">On the **Account Details** page, you need to:</span></span>

    <span data-ttu-id="844b0-175">a.</span><span class="sxs-lookup"><span data-stu-id="844b0-175">a.</span></span> <span data-ttu-id="844b0-176">Selecionar uma conta da SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="844b0-176">Select an SAP CAL account.</span></span> <span data-ttu-id="844b0-177">(Use uma conta que está associada à implantação com o modelo de implantação do Resource Manager.)</span><span class="sxs-lookup"><span data-stu-id="844b0-177">(Use an account that is associated to deploy with the Resource Manager deployment model.)</span></span>

    <span data-ttu-id="844b0-178">b.</span><span class="sxs-lookup"><span data-stu-id="844b0-178">b.</span></span> <span data-ttu-id="844b0-179">Inserir um **Nome** para a instância.</span><span class="sxs-lookup"><span data-stu-id="844b0-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="844b0-180">c.</span><span class="sxs-lookup"><span data-stu-id="844b0-180">c.</span></span> <span data-ttu-id="844b0-181">Selecionar uma **Região** do Azure.</span><span class="sxs-lookup"><span data-stu-id="844b0-181">Select an Azure **Region**.</span></span> <span data-ttu-id="844b0-182">A SAP CAL sugere uma região.</span><span class="sxs-lookup"><span data-stu-id="844b0-182">The SAP CAL suggests a region.</span></span> <span data-ttu-id="844b0-183">Se precisar de outra região do Azure e não tiver uma assinatura da SAP CAL, você precisa solicitar uma assinatura da CAL com a SAP.</span><span class="sxs-lookup"><span data-stu-id="844b0-183">If you need another Azure region and you don't have an SAP CAL subscription, you need to order a CAL subscription with SAP.</span></span>

    <span data-ttu-id="844b0-184">d.</span><span class="sxs-lookup"><span data-stu-id="844b0-184">d.</span></span> <span data-ttu-id="844b0-185">Inserir uma **Senha** mestre de oito ou nove caracteres para a solução.</span><span class="sxs-lookup"><span data-stu-id="844b0-185">Enter a master **Password** for the solution of eight or nine characters.</span></span> <span data-ttu-id="844b0-186">A senha é usada para os administradores dos diferentes componentes.</span><span class="sxs-lookup"><span data-stu-id="844b0-186">The password is used for the administrators of the different components.</span></span>

   ![Modo básico da SAP CAL: criar instância](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="844b0-188">Clique em **Criar** e na caixa de mensagem que for exibida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="844b0-188">Click **Create**, and in the message box that appears, click **OK**.</span></span>

   ![Tamanhos de VM com suporte na SAP CAL](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="844b0-190">Na caixa de diálogo **Chave privada**, clique em **Armazenar** para armazenar a chave privada na SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="844b0-190">In the **Private Key** dialog box, click **Store** to store the private key in the SAP CAL.</span></span> <span data-ttu-id="844b0-191">Para usar a proteção de senha para a chave privada, clique em **Baixar**.</span><span class="sxs-lookup"><span data-stu-id="844b0-191">To use password protection for the private key, click **Download**.</span></span> 

   ![Chave privada da SAP CAL](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="844b0-193">Leia a Mensagem de **aviso** da SAP CAL e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="844b0-193">Read the SAP CAL **Warning** message, and click **OK**.</span></span>

   ![Aviso da SAP CAL](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="844b0-195">Agora a implantação ocorre.</span><span class="sxs-lookup"><span data-stu-id="844b0-195">Now the deployment takes place.</span></span> <span data-ttu-id="844b0-196">Após algum tempo, dependendo do tamanho e da complexidade da solução (uma estimativa é fornecida pela SAP CAL), o status é mostrado como ativo e pronto para uso.</span><span class="sxs-lookup"><span data-stu-id="844b0-196">After some time, depending on the size and complexity of the solution (the SAP CAL provides an estimate), the status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="844b0-197">Para localizar as máquinas virtuais coletadas com os outros recursos associados em um grupo de recursos, vá para o portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="844b0-197">To find the virtual machines collected with the other associated resources in one resource group, go to the Azure portal:</span></span> 

   ![Objetos da SAP CAL implantados no novo portal](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="844b0-199">No portal da SAP CAL, o status é exibido como **Ativo**.</span><span class="sxs-lookup"><span data-stu-id="844b0-199">On the SAP CAL portal, the status appears as **Active**.</span></span> <span data-ttu-id="844b0-200">Para conectar-se à solução, clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="844b0-200">To connect to the solution, click **Connect**.</span></span> <span data-ttu-id="844b0-201">Opções diferentes para se conectar a diferentes componentes são implantadas dentro dessa solução.</span><span class="sxs-lookup"><span data-stu-id="844b0-201">Different options to connect to the different components are deployed within this solution.</span></span>

   ![Instâncias da SAP CAL](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="844b0-203">Antes de você poder usar uma das opções para se conectar aos sistemas implantados, clique em **Guia de introdução**.</span><span class="sxs-lookup"><span data-stu-id="844b0-203">Before you can use one of the options to connect to the deployed systems, click **Getting Started Guide**.</span></span> 

   ![Conecte-se à instância](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="844b0-205">A documentação nomeia os usuários para cada um dos métodos de conectividade.</span><span class="sxs-lookup"><span data-stu-id="844b0-205">The documentation names the users for each of the connectivity methods.</span></span> <span data-ttu-id="844b0-206">As senhas para esses usuários são definidas como a senha mestra que você definiu no início do processo de implantação.</span><span class="sxs-lookup"><span data-stu-id="844b0-206">The passwords for those users are set to the master password you defined at the beginning of the deployment process.</span></span> <span data-ttu-id="844b0-207">Na documentação, outros usuários mais funcionais são listados com suas senhas, o que você pode usar para entrar no sistema implantado.</span><span class="sxs-lookup"><span data-stu-id="844b0-207">In the documentation, other more functional users are listed with their passwords, which you can use to sign in to the deployed system.</span></span> 

    <span data-ttu-id="844b0-208">Por exemplo, se você usar a GUI da SAP que foi pré-instalada no computador com área de trabalho remota do Windows, o sistema S/4 pode estar assim:</span><span class="sxs-lookup"><span data-stu-id="844b0-208">For example, if you use the SAP GUI that's preinstalled on the Windows Remote Desktop machine, the S/4 system might look like this:</span></span>

   ![SM50 na GUI da SAP pré-instalada](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="844b0-210">Ou, se você usar o DBACockpit, a instância poderia ser assim:</span><span class="sxs-lookup"><span data-stu-id="844b0-210">Or if you use the DBACockpit, the instance might look like this:</span></span>

   ![SM50 na GUI da SAP DBACockpit](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="844b0-212">Em algumas horas, um dispositivo de SAP S/4 íntegro é implantado no Azure.</span><span class="sxs-lookup"><span data-stu-id="844b0-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="844b0-213">Se você comprou uma assinatura da CAL SAP, a SAP dará total suporte a implantações por meio da CAL SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="844b0-213">If you bought an SAP CAL subscription, SAP fully supports deployments through the SAP CAL on Azure.</span></span> <span data-ttu-id="844b0-214">A fila de suporte é BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="844b0-214">The support queue is BC-VCM-CAL.</span></span>







