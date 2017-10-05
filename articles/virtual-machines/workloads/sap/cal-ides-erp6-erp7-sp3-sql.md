---
title: Implantar SAP IDES EHP7 SP3 para SAP ERP 6.0 no Azure | Microsoft Docs
description: Implantar SAP IDES EHP7 SP3 para SAP ERP 6.0 no Azure
services: virtual-machines-windows
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 626c1523-1026-478f-bd8a-22c83b869231
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/16/2016
ms.author: hermannd
ms.openlocfilehash: 91eed294077ff72d0760018b10c98f32db88f3be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a><span data-ttu-id="51dc0-103">Implantar SAP IDES EHP7 SP3 para SAP ERP 6.0 no Azure</span><span class="sxs-lookup"><span data-stu-id="51dc0-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span></span>
<span data-ttu-id="51dc0-104">Este artigo descreve como implantar o sistema SAP IDES em execução com o SQL Server e o sistema operacional Windows no Azure via SAP Cloud Appliance Library (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="51dc0-104">This article describes how to deploy an SAP IDES system running with SQL Server and the Windows operating system on Azure via the SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="51dc0-105">As capturas de tela mostram o processo passo a passo.</span><span class="sxs-lookup"><span data-stu-id="51dc0-105">The screenshots show the step-by-step process.</span></span> <span data-ttu-id="51dc0-106">Para implantar uma solução diferente, siga as mesmas etapas.</span><span class="sxs-lookup"><span data-stu-id="51dc0-106">To deploy a different solution, follow the same steps.</span></span>

<span data-ttu-id="51dc0-107">Para iniciar com a SAP CAL, consulte o site [SAP Cloud Appliance Library](https://cal.sap.com/).</span><span class="sxs-lookup"><span data-stu-id="51dc0-107">To start with the SAP CAL, go to the [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="51dc0-108">A SAP também tem um blog sobre a nova [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="51dc0-108">SAP also has a blog about the new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

> [!NOTE]
<span data-ttu-id="51dc0-109">A partir de 29 de maio de 2017, você pode usar o modelo de implantação do Azure Resource Manager além do modelo de implantação clássico menos preferencial para implantar a SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="51dc0-109">As of May 29, 2017, you can use the Azure Resource Manager deployment model in addition to the less-preferred classic deployment model to deploy the SAP CAL.</span></span> <span data-ttu-id="51dc0-110">É recomendável que você use o novo modelo de implantação do Resource Manager e ignore o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="51dc0-110">We recommend that you use the new Resource Manager deployment model and disregard the classic deployment model.</span></span>

<span data-ttu-id="51dc0-111">Se você já criou uma conta da SAP CAL que usa o modelo clássico, *é necessário criar outra conta da SAP CAL*.</span><span class="sxs-lookup"><span data-stu-id="51dc0-111">If you already created an SAP CAL account that uses the classic model, *you need to create another SAP CAL account*.</span></span> <span data-ttu-id="51dc0-112">Essa conta precisa implantar exclusivamente no Azure usando o modelo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="51dc0-112">This account needs to exclusively deploy into Azure by using the Resource Manager model.</span></span>

<span data-ttu-id="51dc0-113">Depois de entrar na SAP CAL, a primeira página geralmente leva você para a página **Soluções**.</span><span class="sxs-lookup"><span data-stu-id="51dc0-113">After you sign in to the SAP CAL, the first page usually leads you to the **Solutions** page.</span></span> <span data-ttu-id="51dc0-114">As soluções oferecidas no SAP CAL continuamente estão aumentando, portanto, talvez seja necessário rolar um pouco para encontrar a solução que você deseja.</span><span class="sxs-lookup"><span data-stu-id="51dc0-114">The solutions offered on the SAP CAL are steadily increasing, so you might need to scroll quite a bit to find the solution you want.</span></span> <span data-ttu-id="51dc0-115">A solução SAP IDES com base em Windows destacada está disponível exclusivamente no Azure e demonstra o processo de implantação:</span><span class="sxs-lookup"><span data-stu-id="51dc0-115">The highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates the deployment process:</span></span>

![Soluções de SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-the-sap-cal"></a><span data-ttu-id="51dc0-117">Criar uma conta na SAP CAL</span><span class="sxs-lookup"><span data-stu-id="51dc0-117">Create an account in the SAP CAL</span></span>
1. <span data-ttu-id="51dc0-118">Para entrar na SAP CAL pela primeira vez, use o seu SAP S-User ou outro usuário registrado com a SAP.</span><span class="sxs-lookup"><span data-stu-id="51dc0-118">To sign in to the SAP CAL for the first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="51dc0-119">Em seguida, defina uma conta da SAP CAL que é usada pela SAP CAL para implantar dispositivos no Azure.</span><span class="sxs-lookup"><span data-stu-id="51dc0-119">Then define an SAP CAL account that is used by the SAP CAL to deploy appliances on Azure.</span></span> <span data-ttu-id="51dc0-120">Na definição de conta, você precisa:</span><span class="sxs-lookup"><span data-stu-id="51dc0-120">In the account definition, you need to:</span></span>

    <span data-ttu-id="51dc0-121">a.</span><span class="sxs-lookup"><span data-stu-id="51dc0-121">a.</span></span> <span data-ttu-id="51dc0-122">Selecionar o modelo de implantação no Azure (Resource Manager ou clássico).</span><span class="sxs-lookup"><span data-stu-id="51dc0-122">Select the deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="51dc0-123">b.</span><span class="sxs-lookup"><span data-stu-id="51dc0-123">b.</span></span> <span data-ttu-id="51dc0-124">Inserir sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="51dc0-124">Enter your Azure subscription.</span></span> <span data-ttu-id="51dc0-125">Uma conta da SAP CAL pode ser atribuída a apenas uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="51dc0-125">An SAP CAL account can be assigned to one subscription only.</span></span> <span data-ttu-id="51dc0-126">Se você precisar de mais de uma assinatura, precisará criar uma outra conta da SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="51dc0-126">If you need more than one subscription, you need to create another SAP CAL account.</span></span>
    
    <span data-ttu-id="51dc0-127">c.</span><span class="sxs-lookup"><span data-stu-id="51dc0-127">c.</span></span> <span data-ttu-id="51dc0-128">Conceder a permissão da SAP CAL para implantar em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="51dc0-128">Give the SAP CAL permission to deploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="51dc0-129">As próximas etapas mostram como criar uma conta da SAP CAL para implantações do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="51dc0-129">The next steps show how to create an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="51dc0-130">Se você já tiver uma conta da SAP CAL que está vinculada ao modelo de implantação clássico, é *necessário* seguir estas etapas para criar uma nova conta da SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="51dc0-130">If you already have an SAP CAL account that is linked to the classic deployment model, you *need* to follow these steps to create a new SAP CAL account.</span></span> <span data-ttu-id="51dc0-131">A nova conta da SAP CAL precisa ser implantada no modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="51dc0-131">The new SAP CAL account needs to deploy in the Resource Manager model.</span></span>

2. <span data-ttu-id="51dc0-132">Para criar uma nova conta da SAP CAL, a página **Contas** mostra duas opções para o Azure:</span><span class="sxs-lookup"><span data-stu-id="51dc0-132">To create a new SAP CAL account, the **Accounts** page shows two choices for Azure:</span></span> 

    <span data-ttu-id="51dc0-133">a.</span><span class="sxs-lookup"><span data-stu-id="51dc0-133">a.</span></span> <span data-ttu-id="51dc0-134">**Microsoft Azure (clássico)** é o modelo de implantação clássico e não é mais preferencial.</span><span class="sxs-lookup"><span data-stu-id="51dc0-134">**Microsoft Azure (classic)** is the classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="51dc0-135">b.</span><span class="sxs-lookup"><span data-stu-id="51dc0-135">b.</span></span> <span data-ttu-id="51dc0-136">**Microsoft Azure** é o novo modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="51dc0-136">**Microsoft Azure** is the new Resource Manager deployment model.</span></span>

    ![Contas da SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    <span data-ttu-id="51dc0-138">Para implantar no modelo do Resource Manager, selecione **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="51dc0-138">To deploy in the Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Contas da SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. <span data-ttu-id="51dc0-140">Insira a **ID da assinatura** do Azure que pode ser encontrada no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="51dc0-140">Enter the Azure **Subscription ID** that can be found on the Azure portal.</span></span> 

    ![ID da assinatura da SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. <span data-ttu-id="51dc0-142">Para autorizar a SAP CAL para implantar na assinatura do Azure que você definiu, clique em **Autorizar**.</span><span class="sxs-lookup"><span data-stu-id="51dc0-142">To authorize the SAP CAL to deploy into the Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="51dc0-143">A seguinte página será exibida na guia do navegador:</span><span class="sxs-lookup"><span data-stu-id="51dc0-143">The following page appears in the browser tab:</span></span>

    ![Entrar nos serviços de nuvem do Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. <span data-ttu-id="51dc0-145">Se mais de um usuário estiver listado, escolha a conta da Microsoft que está vinculada para ser o coadministrador da assinatura do Azure que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="51dc0-145">If more than one user is listed, choose the Microsoft account that is linked to be the coadministrator of the Azure subscription you selected.</span></span> <span data-ttu-id="51dc0-146">A seguinte página será exibida na guia do navegador:</span><span class="sxs-lookup"><span data-stu-id="51dc0-146">The following page appears in the browser tab:</span></span>

    ![Confirmação dos serviços de nuvem do Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. <span data-ttu-id="51dc0-148">Clique em **Aceitar**.</span><span class="sxs-lookup"><span data-stu-id="51dc0-148">Click **Accept**.</span></span> <span data-ttu-id="51dc0-149">Se a autorização for bem-sucedido, a definição de conta da SAP CAL será exibida novamente.</span><span class="sxs-lookup"><span data-stu-id="51dc0-149">If the authorization is successful, the SAP CAL account definition displays again.</span></span> <span data-ttu-id="51dc0-150">Após um curto período de tempo, uma mensagem confirmará que o processo de autorização foi bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="51dc0-150">After a short time, a message confirms that the authorization process was successful.</span></span>

7. <span data-ttu-id="51dc0-151">Para atribuir a conta da CAL SAP recém-criada ao seu usuário, insira sua **ID de usuário** na caixa de texto à direita e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="51dc0-151">To assign the newly created SAP CAL account to your user, enter your **User ID** in the text box on the right and click **Add**.</span></span> 

    ![Conta a ser associada ao usuário](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. <span data-ttu-id="51dc0-153">Para associar sua conta com o usuário que você usa para entrar na SAP CAL, clique em **Análise**.</span><span class="sxs-lookup"><span data-stu-id="51dc0-153">To associate your account with the user that you use to sign in to the SAP CAL, click **Review**.</span></span> 

9. <span data-ttu-id="51dc0-154">Para criar a associação entre o usuário e a conta da CAL SAP recém-criada, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="51dc0-154">To create the association between your user and the newly created SAP CAL account, click **Create**.</span></span>

    ![Usuário para a associação de conta](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

<span data-ttu-id="51dc0-156">Você criou com êxito uma conta da SAP CAL que é capaz de:</span><span class="sxs-lookup"><span data-stu-id="51dc0-156">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="51dc0-157">Usar o Modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="51dc0-157">Use the Resource Manager deployment model.</span></span>
- <span data-ttu-id="51dc0-158">Implantar os sistemas SAP na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="51dc0-158">Deploy SAP systems into your Azure subscription.</span></span>

> [!NOTE]
<span data-ttu-id="51dc0-159">Antes de implantar a solução SAP IDES com base no Windows e no SQL Server, você precisará inscrever-se para uma assinatura da SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="51dc0-159">Before you can deploy the SAP IDES solution based on Windows and SQL Server, you might need to sign up for an SAP CAL subscription.</span></span> <span data-ttu-id="51dc0-160">Caso contrário, a solução pode mostrar como **Bloqueado** na página da visão geral.</span><span class="sxs-lookup"><span data-stu-id="51dc0-160">Otherwise, the solution might show up as **Locked** on the overview page.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="51dc0-161">Implantar uma solução</span><span class="sxs-lookup"><span data-stu-id="51dc0-161">Deploy a solution</span></span>
1. <span data-ttu-id="51dc0-162">Depois de configurar uma conta da SAP CAL, selecione a solução **A solução SAP IDES no Windows e no SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="51dc0-162">After you set up an SAP CAL account, select **The SAP IDES solution on Windows and SQL Server** solution.</span></span> <span data-ttu-id="51dc0-163">Clique em **Criar instância** e confirme as condições de uso e termos.</span><span class="sxs-lookup"><span data-stu-id="51dc0-163">Click **Create Instance**, and confirm the usage and terms conditions.</span></span> 

2. <span data-ttu-id="51dc0-164">Na página **Modo básico: criar instância**, você precisa:</span><span class="sxs-lookup"><span data-stu-id="51dc0-164">On the **Basic Mode: Create Instance** page, you need to:</span></span>

    <span data-ttu-id="51dc0-165">a.</span><span class="sxs-lookup"><span data-stu-id="51dc0-165">a.</span></span> <span data-ttu-id="51dc0-166">Inserir um **Nome** para a instância.</span><span class="sxs-lookup"><span data-stu-id="51dc0-166">Enter an instance **Name**.</span></span>

    <span data-ttu-id="51dc0-167">b.</span><span class="sxs-lookup"><span data-stu-id="51dc0-167">b.</span></span> <span data-ttu-id="51dc0-168">Selecionar uma **Região** do Azure.</span><span class="sxs-lookup"><span data-stu-id="51dc0-168">Select an Azure **Region**.</span></span> <span data-ttu-id="51dc0-169">Talvez seja necessário uma assinatura da SAP CAL para obter várias regiões do Azure oferecidas.</span><span class="sxs-lookup"><span data-stu-id="51dc0-169">You might need an SAP CAL subscription to get multiple Azure regions offered.</span></span>

    <span data-ttu-id="51dc0-170">c.</span><span class="sxs-lookup"><span data-stu-id="51dc0-170">c.</span></span>  <span data-ttu-id="51dc0-171">Inserir a **Senha** mestre para a solução, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="51dc0-171">Enter the master **Password** for the solution, as shown:</span></span>

    ![Modo básico da SAP CAL: criar instância](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. <span data-ttu-id="51dc0-173">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="51dc0-173">Click **Create**.</span></span> <span data-ttu-id="51dc0-174">Após algum tempo, dependendo do tamanho e da complexidade da solução (uma estimativa é fornecida pela SAP CAL), o status é mostrado como ativo e pronto para uso:</span><span class="sxs-lookup"><span data-stu-id="51dc0-174">After some time, depending on the size and complexity of the solution (the SAP CAL provides an estimate), the status is shown as active and ready for use:</span></span> 

    ![Instâncias da SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. <span data-ttu-id="51dc0-176">Para localizar o grupo de recursos e todos os seus objetos que foram criados pela SAP CAL, acesse o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="51dc0-176">To find the resource group and all its objects that were created by the SAP CAL, go to the Azure portal.</span></span> <span data-ttu-id="51dc0-177">As máquinas virtuais podem ser encontradas começando com o mesmo nome de instância fornecido na SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="51dc0-177">The virtual machine can be found starting with the same instance name that was given in the SAP CAL.</span></span>

    ![Objetos do grupo de recursos](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. <span data-ttu-id="51dc0-179">No portal da SAP CAL, vá para as instâncias implantadas e clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="51dc0-179">On the SAP CAL portal, go to the deployed instances and click **Connect**.</span></span> <span data-ttu-id="51dc0-180">A seguinte janela pop-up será exibida:</span><span class="sxs-lookup"><span data-stu-id="51dc0-180">The following pop-up window appears:</span></span> 

    ![Conecte-se à instância](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. <span data-ttu-id="51dc0-182">Antes de você poder usar uma das opções para se conectar aos sistemas implantados, clique em **Guia de introdução**.</span><span class="sxs-lookup"><span data-stu-id="51dc0-182">Before you can use one of the options to connect to the deployed systems, click **Getting Started Guide**.</span></span> <span data-ttu-id="51dc0-183">A documentação nomeia os usuários para cada um dos métodos de conectividade.</span><span class="sxs-lookup"><span data-stu-id="51dc0-183">The documentation names the users for each of the connectivity methods.</span></span> <span data-ttu-id="51dc0-184">As senhas para esses usuários são definidas como a senha mestra que você definiu no início do processo de implantação.</span><span class="sxs-lookup"><span data-stu-id="51dc0-184">The passwords for those users are set to the master password you defined at the beginning of the deployment process.</span></span> <span data-ttu-id="51dc0-185">Na documentação, outros usuários mais funcionais são listados com suas senhas, o que você pode usar para entrar no sistema implantado.</span><span class="sxs-lookup"><span data-stu-id="51dc0-185">In the documentation, other more functional users are listed with their passwords, which you can use to sign in to the deployed system.</span></span>

    ![Documentação de boas-vindas da SAP](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="51dc0-187">Em algumas horas, um sistema de SAP IDES íntegro é implantado no Azure.</span><span class="sxs-lookup"><span data-stu-id="51dc0-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span></span>

<span data-ttu-id="51dc0-188">Se você comprou uma assinatura da CAL SAP, a SAP dará total suporte a implantações por meio da CAL SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="51dc0-188">If you bought an SAP CAL subscription, SAP fully supports deployments through the SAP CAL on Azure.</span></span> <span data-ttu-id="51dc0-189">A fila de suporte é BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="51dc0-189">The support queue is BC-VCM-CAL.</span></span>

