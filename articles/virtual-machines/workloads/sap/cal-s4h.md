---
title: aaaDeploy 4HANA/S de SAP ou BW/4HANA em uma VM do Azure | Microsoft Docs
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
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="309c3-103">Implantar o SAP S/4HANA ou o BW/4HANA no Azure</span><span class="sxs-lookup"><span data-stu-id="309c3-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="309c3-104">Este artigo descreve como toodeploy S/4HANA no Azure usando Olá biblioteca de dispositivo de nuvem do SAP (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="309c3-104">This article describes how toodeploy S/4HANA on Azure by using hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="309c3-105">toodeploy outras soluções baseadas em SAP HANA, como BW/4HANA, siga Olá mesmas etapas.</span><span class="sxs-lookup"><span data-stu-id="309c3-105">toodeploy other SAP HANA-based solutions, such as BW/4HANA, follow hello same steps.</span></span>

> [!NOTE]
<span data-ttu-id="309c3-106">Para obter mais informações sobre Olá CAL do SAP, vá toohello [biblioteca de dispositivo de nuvem do SAP](https://cal.sap.com/) site.</span><span class="sxs-lookup"><span data-stu-id="309c3-106">For more information about hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="309c3-107">SAP também tem um blog sobre Olá [SAP nuvem Appliance biblioteca 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="309c3-107">SAP also has a blog about hello [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="309c3-108">Além disso como de 29 de maio de 2017, você pode usar o modelo de implantação do Azure Resource Manager Olá implantação clássica menos preferencial toohello modelo toodeploy Olá CAL do SAP.</span><span class="sxs-lookup"><span data-stu-id="309c3-108">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="309c3-109">É recomendável que você use o novo modelo de implantação de Gerenciador de recursos hello e ignorar o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="309c3-109">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

## <a name="step-by-step-process-toodeploy-hello-solution"></a><span data-ttu-id="309c3-110">Solução de saudação toodeploy processo passo a passo</span><span class="sxs-lookup"><span data-stu-id="309c3-110">Step-by-step process toodeploy hello solution</span></span>

<span data-ttu-id="309c3-111">Olá sequência de capturas de tela a seguir mostra como toodeploy S/4HANA no Azure usando Olá CAL do SAP.</span><span class="sxs-lookup"><span data-stu-id="309c3-111">hello following sequence of screenshots shows you how toodeploy S/4HANA on Azure by using hello SAP CAL.</span></span> <span data-ttu-id="309c3-112">processo de saudação funciona Olá mesma forma para outras soluções, como BW/4HANA.</span><span class="sxs-lookup"><span data-stu-id="309c3-112">hello process works hello same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="309c3-113">Olá **soluções** página mostra alguns Olá soluções baseadas em SAP HANA de CAL disponíveis no Azure.</span><span class="sxs-lookup"><span data-stu-id="309c3-113">hello **Solutions** page shows some of hello SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="309c3-114">**SAP S/4HANA 1610 FPS01, Fully-Activated dispositivo** está na linha intermediária hello:</span><span class="sxs-lookup"><span data-stu-id="309c3-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in hello middle row:</span></span>

![Soluções de SAP CAL](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="309c3-116">Criar uma conta no hello CAL do SAP</span><span class="sxs-lookup"><span data-stu-id="309c3-116">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="309c3-117">toosign em toohello CAL do SAP para hello primeira vez, use seu usuário SAP S ou outro usuário registrado com o SAP.</span><span class="sxs-lookup"><span data-stu-id="309c3-117">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="309c3-118">Em seguida, defina uma conta de CAL do SAP que é usada por dispositivos de toodeploy Olá CAL do SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="309c3-118">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="309c3-119">Na definição de conta hello, você precisa:</span><span class="sxs-lookup"><span data-stu-id="309c3-119">In hello account definition, you need to:</span></span>

    <span data-ttu-id="309c3-120">a.</span><span class="sxs-lookup"><span data-stu-id="309c3-120">a.</span></span> <span data-ttu-id="309c3-121">Selecione o modelo de implantação de saudação no Azure (Gerenciador de recursos ou clássico).</span><span class="sxs-lookup"><span data-stu-id="309c3-121">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="309c3-122">b.</span><span class="sxs-lookup"><span data-stu-id="309c3-122">b.</span></span> <span data-ttu-id="309c3-123">Inserir sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="309c3-123">Enter your Azure subscription.</span></span> <span data-ttu-id="309c3-124">Tooone assinatura só pode ser atribuída a uma conta de CAL do SAP.</span><span class="sxs-lookup"><span data-stu-id="309c3-124">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="309c3-125">Se você precisar de mais de uma assinatura, você precisa toocreate outra conta de CAL do SAP.</span><span class="sxs-lookup"><span data-stu-id="309c3-125">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>

    <span data-ttu-id="309c3-126">c.</span><span class="sxs-lookup"><span data-stu-id="309c3-126">c.</span></span> <span data-ttu-id="309c3-127">Dê Olá SAP CAL permissão toodeploy em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="309c3-127">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="309c3-128">as próximas etapas Olá mostram como a conta toocreate um CAL do SAP para implantações do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="309c3-128">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="309c3-129">Se você já tiver uma conta de CAL do SAP que é o modelo de implantação clássico toohello vinculado, você *necessário* toofollow toocreate essas etapas uma nova conta de CAL do SAP.</span><span class="sxs-lookup"><span data-stu-id="309c3-129">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="309c3-130">nova conta de CAL SAP Olá precisa toodeploy no modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="309c3-130">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="309c3-131">Crie uma nova conta do SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="309c3-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="309c3-132">Olá **contas** página mostra três opções para o Azure:</span><span class="sxs-lookup"><span data-stu-id="309c3-132">hello **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="309c3-133">a.</span><span class="sxs-lookup"><span data-stu-id="309c3-133">a.</span></span> <span data-ttu-id="309c3-134">**Microsoft Azure (clássica)** é o modelo de implantação clássico hello e não está mais preferencial.</span><span class="sxs-lookup"><span data-stu-id="309c3-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="309c3-135">b.</span><span class="sxs-lookup"><span data-stu-id="309c3-135">b.</span></span> <span data-ttu-id="309c3-136">**Microsoft Azure** é Olá novo modelo de implantação de Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="309c3-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    <span data-ttu-id="309c3-137">c.</span><span class="sxs-lookup"><span data-stu-id="309c3-137">c.</span></span> <span data-ttu-id="309c3-138">**Windows Azure operado pela 21Vianet** é uma opção na China que usa o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="309c3-138">**Windows Azure operated by 21Vianet** is an option in China that uses hello classic deployment model.</span></span>

    <span data-ttu-id="309c3-139">Selecione toodeploy no modelo do Gerenciador de recursos de hello, **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="309c3-139">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Detalhes da conta da SAP CAL](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="309c3-141">Digite hello Azure **ID da assinatura** que podem ser encontrados no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="309c3-141">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span>

   ![Contas da SAP CAL](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="309c3-143">tooauthorize Olá CAL SAP toodeploy em Olá assinatura do Azure que você definiu, clique em **autorizar**.</span><span class="sxs-lookup"><span data-stu-id="309c3-143">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="309c3-144">saudação de página a seguir aparece na guia do navegador hello:</span><span class="sxs-lookup"><span data-stu-id="309c3-144">hello following page appears in hello browser tab:</span></span>

   ![Entrar nos serviços de nuvem do Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="309c3-146">Se mais de um usuário estiver listado, escolha a conta da Microsoft hello que é vinculado toobe Olá coadministrator de saudação assinatura do Azure que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="309c3-146">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="309c3-147">saudação de página a seguir aparece na guia do navegador hello:</span><span class="sxs-lookup"><span data-stu-id="309c3-147">hello following page appears in hello browser tab:</span></span>

   ![Confirmação dos serviços de nuvem do Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="309c3-149">Clique em **Aceitar**.</span><span class="sxs-lookup"><span data-stu-id="309c3-149">Click **Accept**.</span></span> <span data-ttu-id="309c3-150">Se a autorização Olá for bem-sucedida, Olá SAP CAL definição da conta será exibida novamente.</span><span class="sxs-lookup"><span data-stu-id="309c3-150">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="309c3-151">Após um curto período de tempo, uma mensagem confirmará que o processo de autorização de saudação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="309c3-151">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="309c3-152">Olá tooassign recém-criado CAL SAP tooyour de conta do usuário, insira seu **ID de usuário** no hello caixa de texto de saudação à direita e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="309c3-152">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span>

   ![Associação de toouser de conta](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="309c3-154">clique de sua conta com usuário Olá que você use toosign em toohello CAL do SAP, tooassociate **revisão**.</span><span class="sxs-lookup"><span data-stu-id="309c3-154">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="309c3-155">associação de saudação toocreate entre o usuário e conta de CAL SAP Olá recém-criado, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="309c3-155">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

   ![Associação de conta do usuário tooSAP CAL](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="309c3-157">Você criou com êxito uma conta da SAP CAL que é capaz de:</span><span class="sxs-lookup"><span data-stu-id="309c3-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="309c3-158">Use o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="309c3-158">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="309c3-159">Implantar os sistemas SAP na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="309c3-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="309c3-160">Agora você pode iniciar toodeploy 4HANA/S em sua assinatura do usuário no Azure.</span><span class="sxs-lookup"><span data-stu-id="309c3-160">Now you can start toodeploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="309c3-161">Antes de continuar, determine se você tem cotas de núcleo do Azure para as VMs Série H do Azure.</span><span class="sxs-lookup"><span data-stu-id="309c3-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="309c3-162">No momento de Olá Olá CAL do SAP usa toodeploy H-Series VMs do Azure algumas das soluções de saudação do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="309c3-162">At hello moment, hello SAP CAL uses H-Series VMs of Azure toodeploy some of hello SAP HANA-based solutions.</span></span> <span data-ttu-id="309c3-163">Sua assinatura do Azure talvez não tenha cotas de núcleo da Série H para a Série H.</span><span class="sxs-lookup"><span data-stu-id="309c3-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="309c3-164">Nesse caso, talvez seja necessário toocontact suporte do Azure tooget uma cota de pelo menos 16 núcleos de série de H.</span><span class="sxs-lookup"><span data-stu-id="309c3-164">If so, you might need toocontact Azure support tooget a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="309c3-165">Quando você implanta uma solução no Azure no hello CAL do SAP, talvez você descubra que você pode escolher apenas uma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="309c3-165">When you deploy a solution on Azure in hello SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="309c3-166">toodeploy em regiões do Azure diferentes Olá um sugeridas pelo Olá CAL do SAP, é necessário toopurchase uma assinatura de CAL do SAP.</span><span class="sxs-lookup"><span data-stu-id="309c3-166">toodeploy into Azure regions other than hello one suggested by hello SAP CAL, you need toopurchase a CAL subscription from SAP.</span></span> <span data-ttu-id="309c3-167">Também pode ser necessário tooopen uma mensagem com SAP toohave seu toodeliver de conta habilitada CAL em regiões do Azure diferentes Olá aqueles inicialmente sugeridos.</span><span class="sxs-lookup"><span data-stu-id="309c3-167">You also might need tooopen a message with SAP toohave your CAL account enabled toodeliver into Azure regions other than hello ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="309c3-168">Implantar uma solução</span><span class="sxs-lookup"><span data-stu-id="309c3-168">Deploy a solution</span></span>

<span data-ttu-id="309c3-169">Permite implantar uma solução de saudação **soluções** página de saudação CAL do SAP.</span><span class="sxs-lookup"><span data-stu-id="309c3-169">Let's deploy a solution from hello **Solutions** page of hello SAP CAL.</span></span> <span data-ttu-id="309c3-170">Olá CAL SAP tem dois toodeploy de sequências:</span><span class="sxs-lookup"><span data-stu-id="309c3-170">hello SAP CAL has two sequences toodeploy:</span></span>

- <span data-ttu-id="309c3-171">Uma sequência básica que usa um toobe de sistema de saudação a toodefine do página implantado</span><span class="sxs-lookup"><span data-stu-id="309c3-171">A basic sequence that uses one page toodefine hello system toobe deployed</span></span>
- <span data-ttu-id="309c3-172">Uma sequência avançada que fornece certas opções sobre tamanhos de VM</span><span class="sxs-lookup"><span data-stu-id="309c3-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="309c3-173">Demonstraremos Olá toodeployment de caminho básica aqui.</span><span class="sxs-lookup"><span data-stu-id="309c3-173">We demonstrate hello basic path toodeployment here.</span></span>

1. <span data-ttu-id="309c3-174">Em Olá **detalhes da conta** página, você precisa:</span><span class="sxs-lookup"><span data-stu-id="309c3-174">On hello **Account Details** page, you need to:</span></span>

    <span data-ttu-id="309c3-175">a.</span><span class="sxs-lookup"><span data-stu-id="309c3-175">a.</span></span> <span data-ttu-id="309c3-176">Selecionar uma conta da SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="309c3-176">Select an SAP CAL account.</span></span> <span data-ttu-id="309c3-177">(Use uma conta que seja toodeploy associado com o modelo de implantação do Gerenciador de recursos de saudação).</span><span class="sxs-lookup"><span data-stu-id="309c3-177">(Use an account that is associated toodeploy with hello Resource Manager deployment model.)</span></span>

    <span data-ttu-id="309c3-178">b.</span><span class="sxs-lookup"><span data-stu-id="309c3-178">b.</span></span> <span data-ttu-id="309c3-179">Inserir um **Nome** para a instância.</span><span class="sxs-lookup"><span data-stu-id="309c3-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="309c3-180">c.</span><span class="sxs-lookup"><span data-stu-id="309c3-180">c.</span></span> <span data-ttu-id="309c3-181">Selecionar uma **Região** do Azure.</span><span class="sxs-lookup"><span data-stu-id="309c3-181">Select an Azure **Region**.</span></span> <span data-ttu-id="309c3-182">Olá CAL do SAP sugere uma região.</span><span class="sxs-lookup"><span data-stu-id="309c3-182">hello SAP CAL suggests a region.</span></span> <span data-ttu-id="309c3-183">Se você precisar outra região do Azure e você não tiver uma assinatura de CAL do SAP, você precisa de assinatura de tooorder um CAL com o SAP.</span><span class="sxs-lookup"><span data-stu-id="309c3-183">If you need another Azure region and you don't have an SAP CAL subscription, you need tooorder a CAL subscription with SAP.</span></span>

    <span data-ttu-id="309c3-184">d.</span><span class="sxs-lookup"><span data-stu-id="309c3-184">d.</span></span> <span data-ttu-id="309c3-185">Insira um mestre **senha** para solução de saudação de oito ou nove caracteres.</span><span class="sxs-lookup"><span data-stu-id="309c3-185">Enter a master **Password** for hello solution of eight or nine characters.</span></span> <span data-ttu-id="309c3-186">Olá senha é usada para administradores de saudação de diferentes componentes de saudação.</span><span class="sxs-lookup"><span data-stu-id="309c3-186">hello password is used for hello administrators of hello different components.</span></span>

   ![Modo básico da SAP CAL: criar instância](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="309c3-188">Clique em **criar**e na caixa de mensagem de saudação que aparece, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="309c3-188">Click **Create**, and in hello message box that appears, click **OK**.</span></span>

   ![Tamanhos de VM com suporte na SAP CAL](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="309c3-190">Em Olá **chave privada** caixa de diálogo, clique em **repositório** toostore Olá chave particular Olá CAL do SAP.</span><span class="sxs-lookup"><span data-stu-id="309c3-190">In hello **Private Key** dialog box, click **Store** toostore hello private key in hello SAP CAL.</span></span> <span data-ttu-id="309c3-191">Clique em toouse proteção por senha para a chave privada do hello, **baixar**.</span><span class="sxs-lookup"><span data-stu-id="309c3-191">toouse password protection for hello private key, click **Download**.</span></span> 

   ![Chave privada da SAP CAL](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="309c3-193">Saudação de leitura CAL SAP **aviso** da mensagem e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="309c3-193">Read hello SAP CAL **Warning** message, and click **OK**.</span></span>

   ![Aviso da SAP CAL](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="309c3-195">Agora a implantação Olá ocorre.</span><span class="sxs-lookup"><span data-stu-id="309c3-195">Now hello deployment takes place.</span></span> <span data-ttu-id="309c3-196">Depois de algum tempo, dependendo do tamanho de saudação e a complexidade da solução hello (Olá SAP CAL fornece uma estimativa), Olá status será exibido como ativa e pronta para uso.</span><span class="sxs-lookup"><span data-stu-id="309c3-196">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="309c3-197">máquinas de virtuais de saudação toofind coletadas com hello outros recursos associados em um grupo de recursos, consulte toohello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="309c3-197">toofind hello virtual machines collected with hello other associated resources in one resource group, go toohello Azure portal:</span></span> 

   ![Objetos de CAL SAP implantados no novo portal de saudação](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="309c3-199">No portal do SAP CAL hello, status de saudação aparece como **Active**.</span><span class="sxs-lookup"><span data-stu-id="309c3-199">On hello SAP CAL portal, hello status appears as **Active**.</span></span> <span data-ttu-id="309c3-200">solução de toohello tooconnect, clique em **conectar**.</span><span class="sxs-lookup"><span data-stu-id="309c3-200">tooconnect toohello solution, click **Connect**.</span></span> <span data-ttu-id="309c3-201">Opções diferentes tooconnect toohello diferentes componentes são implantados dentro dessa solução.</span><span class="sxs-lookup"><span data-stu-id="309c3-201">Different options tooconnect toohello different components are deployed within this solution.</span></span>

   ![Instâncias da SAP CAL](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="309c3-203">Antes de usar um dos sistemas de toohello implantado em tooconnect Olá opções, clique em **guia de Introdução**.</span><span class="sxs-lookup"><span data-stu-id="309c3-203">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> 

   ![Conecte-se a instância de toohello](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="309c3-205">nomes de documentação Olá Olá usuários para cada um dos métodos de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="309c3-205">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="309c3-206">as senhas de saudação para os usuários são definidas toohello senha mestra que você definiu no início do processo de implantação de saudação hello.</span><span class="sxs-lookup"><span data-stu-id="309c3-206">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="309c3-207">Na documentação do hello, outros usuários mais funcionais são listados com suas senhas, o que você pode usar toosign no toohello implantado sistema.</span><span class="sxs-lookup"><span data-stu-id="309c3-207">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span> 

    <span data-ttu-id="309c3-208">Por exemplo, se você usar o hello SAP GUI que foi pré-instalado no computador de área de trabalho remota do Windows hello, Olá sistema S/4 pode parecer assim:</span><span class="sxs-lookup"><span data-stu-id="309c3-208">For example, if you use hello SAP GUI that's preinstalled on hello Windows Remote Desktop machine, hello S/4 system might look like this:</span></span>

   ![SM50 em Olá pré-instalado SAP GUI](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="309c3-210">Ou, se você usar Olá DBACockpit, instância Olá poderia se parecer com:</span><span class="sxs-lookup"><span data-stu-id="309c3-210">Or if you use hello DBACockpit, hello instance might look like this:</span></span>

   ![SM50 em Olá DBACockpit SAP GUI](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="309c3-212">Em algumas horas, um dispositivo de SAP S/4 íntegro é implantado no Azure.</span><span class="sxs-lookup"><span data-stu-id="309c3-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="309c3-213">Se você comprou uma assinatura de CAL do SAP, SAP totalmente dá suporte a implantações por meio de saudação CAL do SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="309c3-213">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="309c3-214">fila de suporte de saudação é BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="309c3-214">hello support queue is BC-VCM-CAL.</span></span>







