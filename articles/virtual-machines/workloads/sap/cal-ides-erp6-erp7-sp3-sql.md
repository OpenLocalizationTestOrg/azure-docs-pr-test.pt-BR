---
title: aaaDeploy IDES EHP7 SP3 do SAP para o SAP ERP 6.0 no Azure | Microsoft Docs
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
ms.openlocfilehash: 26d88c7b48a91d35602464c4f89ca7a30502c4b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a><span data-ttu-id="fe8a0-103">Implantar SAP IDES EHP7 SP3 para SAP ERP 6.0 no Azure</span><span class="sxs-lookup"><span data-stu-id="fe8a0-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span></span>
<span data-ttu-id="fe8a0-104">Este artigo descreve como toodeploy um SAP sistema IDES em execução no SQL Server e do sistema de operacional do Windows hello no Azure por meio de saudação biblioteca de dispositivo de nuvem do SAP (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-104">This article describes how toodeploy an SAP IDES system running with SQL Server and hello Windows operating system on Azure via hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="fe8a0-105">Olá capturas de tela mostram processo passo a passo de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-105">hello screenshots show hello step-by-step process.</span></span> <span data-ttu-id="fe8a0-106">toodeploy uma solução diferente, siga Olá as mesmas etapas.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-106">toodeploy a different solution, follow hello same steps.</span></span>

<span data-ttu-id="fe8a0-107">toostart com hello CAL do SAP, vá toohello [biblioteca de dispositivo de nuvem do SAP](https://cal.sap.com/) site.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-107">toostart with hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="fe8a0-108">SAP também tem um blog sobre Olá novo [SAP nuvem Appliance biblioteca 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="fe8a0-108">SAP also has a blog about hello new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

> [!NOTE]
<span data-ttu-id="fe8a0-109">Além disso como de 29 de maio de 2017, você pode usar o modelo de implantação do Azure Resource Manager Olá implantação clássica menos preferencial toohello modelo toodeploy Olá CAL do SAP.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-109">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="fe8a0-110">É recomendável que você use o novo modelo de implantação de Gerenciador de recursos hello e ignorar o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-110">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

<span data-ttu-id="fe8a0-111">Se você já criou uma conta de CAL do SAP que usa o modelo clássico de hello, *precisar toocreate outra conta SAP CAL*.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-111">If you already created an SAP CAL account that uses hello classic model, *you need toocreate another SAP CAL account*.</span></span> <span data-ttu-id="fe8a0-112">Essa conta precisa tooexclusively implantar no Azure usando o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-112">This account needs tooexclusively deploy into Azure by using hello Resource Manager model.</span></span>

<span data-ttu-id="fe8a0-113">Depois que você entra no toohello CAL do SAP, primeira página do hello geralmente leva você toohello **soluções** página.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-113">After you sign in toohello SAP CAL, hello first page usually leads you toohello **Solutions** page.</span></span> <span data-ttu-id="fe8a0-114">soluções Olá oferecidas no hello CAL SAP estão aumentando continuamente, para que você talvez precise tooscroll solução Olá um pouco toofind que você deseja.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-114">hello solutions offered on hello SAP CAL are steadily increasing, so you might need tooscroll quite a bit toofind hello solution you want.</span></span> <span data-ttu-id="fe8a0-115">Olá realçado baseados em Windows SAP IDES solução disponível exclusivamente no Azure demonstra o processo de implantação de saudação:</span><span class="sxs-lookup"><span data-stu-id="fe8a0-115">hello highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates hello deployment process:</span></span>

![Soluções de SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="fe8a0-117">Criar uma conta no hello CAL do SAP</span><span class="sxs-lookup"><span data-stu-id="fe8a0-117">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="fe8a0-118">toosign em toohello CAL do SAP para hello primeira vez, use seu usuário SAP S ou outro usuário registrado com o SAP.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-118">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="fe8a0-119">Em seguida, defina uma conta de CAL do SAP que é usada por dispositivos de toodeploy Olá CAL do SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-119">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="fe8a0-120">Na definição de conta hello, você precisa:</span><span class="sxs-lookup"><span data-stu-id="fe8a0-120">In hello account definition, you need to:</span></span>

    <span data-ttu-id="fe8a0-121">a.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-121">a.</span></span> <span data-ttu-id="fe8a0-122">Selecione o modelo de implantação de saudação no Azure (Gerenciador de recursos ou clássico).</span><span class="sxs-lookup"><span data-stu-id="fe8a0-122">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="fe8a0-123">b.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-123">b.</span></span> <span data-ttu-id="fe8a0-124">Inserir sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-124">Enter your Azure subscription.</span></span> <span data-ttu-id="fe8a0-125">Tooone assinatura só pode ser atribuída a uma conta de CAL do SAP.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-125">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="fe8a0-126">Se você precisar de mais de uma assinatura, você precisa toocreate outra conta de CAL do SAP.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-126">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>
    
    <span data-ttu-id="fe8a0-127">c.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-127">c.</span></span> <span data-ttu-id="fe8a0-128">Dê Olá SAP CAL permissão toodeploy em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-128">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="fe8a0-129">as próximas etapas Olá mostram como a conta toocreate um CAL do SAP para implantações do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-129">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="fe8a0-130">Se você já tiver uma conta de CAL do SAP que é o modelo de implantação clássico toohello vinculado, você *necessário* toofollow toocreate essas etapas uma nova conta de CAL do SAP.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-130">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="fe8a0-131">nova conta de CAL SAP Olá precisa toodeploy no modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-131">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="fe8a0-132">toocreate um CAL SAP nova conta, hello **contas** página mostra duas opções para o Azure:</span><span class="sxs-lookup"><span data-stu-id="fe8a0-132">toocreate a new SAP CAL account, hello **Accounts** page shows two choices for Azure:</span></span> 

    <span data-ttu-id="fe8a0-133">a.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-133">a.</span></span> <span data-ttu-id="fe8a0-134">**Microsoft Azure (clássica)** é o modelo de implantação clássico hello e não está mais preferencial.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="fe8a0-135">b.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-135">b.</span></span> <span data-ttu-id="fe8a0-136">**Microsoft Azure** é Olá novo modelo de implantação de Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    ![Contas da SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    <span data-ttu-id="fe8a0-138">Selecione toodeploy no modelo do Gerenciador de recursos de hello, **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-138">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Contas da SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. <span data-ttu-id="fe8a0-140">Digite hello Azure **ID da assinatura** que podem ser encontrados no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-140">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span> 

    ![ID da assinatura da SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. <span data-ttu-id="fe8a0-142">tooauthorize Olá CAL SAP toodeploy em Olá assinatura do Azure que você definiu, clique em **autorizar**.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-142">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="fe8a0-143">saudação de página a seguir aparece na guia do navegador hello:</span><span class="sxs-lookup"><span data-stu-id="fe8a0-143">hello following page appears in hello browser tab:</span></span>

    ![Entrar nos serviços de nuvem do Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. <span data-ttu-id="fe8a0-145">Se mais de um usuário estiver listado, escolha a conta da Microsoft hello que é vinculado toobe Olá coadministrator de saudação assinatura do Azure que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-145">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="fe8a0-146">saudação de página a seguir aparece na guia do navegador hello:</span><span class="sxs-lookup"><span data-stu-id="fe8a0-146">hello following page appears in hello browser tab:</span></span>

    ![Confirmação dos serviços de nuvem do Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. <span data-ttu-id="fe8a0-148">Clique em **Aceitar**.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-148">Click **Accept**.</span></span> <span data-ttu-id="fe8a0-149">Se a autorização Olá for bem-sucedida, Olá SAP CAL definição da conta será exibida novamente.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-149">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="fe8a0-150">Após um curto período de tempo, uma mensagem confirmará que o processo de autorização de saudação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-150">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="fe8a0-151">Olá tooassign recém-criado CAL SAP tooyour de conta do usuário, insira seu **ID de usuário** no hello caixa de texto de saudação à direita e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-151">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span> 

    ![Associação de toouser de conta](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. <span data-ttu-id="fe8a0-153">clique de sua conta com usuário Olá que você use toosign em toohello CAL do SAP, tooassociate **revisão**.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-153">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 

9. <span data-ttu-id="fe8a0-154">associação de saudação toocreate entre o usuário e conta de CAL SAP Olá recém-criado, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-154">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

    ![Associação de tooaccount do usuário](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

<span data-ttu-id="fe8a0-156">Você criou com êxito uma conta da SAP CAL que é capaz de:</span><span class="sxs-lookup"><span data-stu-id="fe8a0-156">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="fe8a0-157">Use o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-157">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="fe8a0-158">Implantar os sistemas SAP na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-158">Deploy SAP systems into your Azure subscription.</span></span>

> [!NOTE]
<span data-ttu-id="fe8a0-159">Antes de implantar solução SAP IDES Olá com base no Windows e do SQL Server, talvez seja necessário toosign para uma assinatura de CAL do SAP.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-159">Before you can deploy hello SAP IDES solution based on Windows and SQL Server, you might need toosign up for an SAP CAL subscription.</span></span> <span data-ttu-id="fe8a0-160">Caso contrário, solução de saudação pode mostrar como **bloqueado** na página de visão geral de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-160">Otherwise, hello solution might show up as **Locked** on hello overview page.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="fe8a0-161">Implantar uma solução</span><span class="sxs-lookup"><span data-stu-id="fe8a0-161">Deploy a solution</span></span>
1. <span data-ttu-id="fe8a0-162">Depois de configurar uma conta de CAL do SAP, selecione **Olá solução SAP IDES no Windows e no SQL Server** solução.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-162">After you set up an SAP CAL account, select **hello SAP IDES solution on Windows and SQL Server** solution.</span></span> <span data-ttu-id="fe8a0-163">Clique em **criar instância**e confirme as condições de uso e os termos de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-163">Click **Create Instance**, and confirm hello usage and terms conditions.</span></span> 

2. <span data-ttu-id="fe8a0-164">Em Olá **modo básico: criar instância** página, você precisa:</span><span class="sxs-lookup"><span data-stu-id="fe8a0-164">On hello **Basic Mode: Create Instance** page, you need to:</span></span>

    <span data-ttu-id="fe8a0-165">a.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-165">a.</span></span> <span data-ttu-id="fe8a0-166">Inserir um **Nome** para a instância.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-166">Enter an instance **Name**.</span></span>

    <span data-ttu-id="fe8a0-167">b.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-167">b.</span></span> <span data-ttu-id="fe8a0-168">Selecionar uma **Região** do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-168">Select an Azure **Region**.</span></span> <span data-ttu-id="fe8a0-169">Talvez seja necessário um tooget de assinatura de CAL SAP oferecidas várias regiões do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-169">You might need an SAP CAL subscription tooget multiple Azure regions offered.</span></span>

    <span data-ttu-id="fe8a0-170">c.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-170">c.</span></span>  <span data-ttu-id="fe8a0-171">Insira o mestre de saudação **senha** para solução hello, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="fe8a0-171">Enter hello master **Password** for hello solution, as shown:</span></span>

    ![Modo básico da SAP CAL: criar instância](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. <span data-ttu-id="fe8a0-173">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-173">Click **Create**.</span></span> <span data-ttu-id="fe8a0-174">Depois de algum tempo, dependendo do tamanho de saudação e a complexidade da solução hello (Olá SAP CAL fornece uma estimativa), Olá status será mostrado como ativa e pronta para uso:</span><span class="sxs-lookup"><span data-stu-id="fe8a0-174">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use:</span></span> 

    ![Instâncias da SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. <span data-ttu-id="fe8a0-176">grupo de recursos de saudação toofind e todos os seus objetos que foram criados pelo Olá CAL do SAP, visite toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-176">toofind hello resource group and all its objects that were created by hello SAP CAL, go toohello Azure portal.</span></span> <span data-ttu-id="fe8a0-177">máquina virtual de saudação podem ser encontrada começando com hello mesmo nome que foi fornecida no hello SAP CAL da instância.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-177">hello virtual machine can be found starting with hello same instance name that was given in hello SAP CAL.</span></span>

    ![Objetos do grupo de recursos](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. <span data-ttu-id="fe8a0-179">No portal do SAP CAL hello, vá instâncias toohello implantado e clique em **conectar**.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-179">On hello SAP CAL portal, go toohello deployed instances and click **Connect**.</span></span> <span data-ttu-id="fe8a0-180">Olá janela pop-up a seguir será exibida:</span><span class="sxs-lookup"><span data-stu-id="fe8a0-180">hello following pop-up window appears:</span></span> 

    ![Conecte-se a instância de toohello](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. <span data-ttu-id="fe8a0-182">Antes de usar um dos sistemas de toohello implantado em tooconnect Olá opções, clique em **guia de Introdução**.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-182">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> <span data-ttu-id="fe8a0-183">nomes de documentação Olá Olá usuários para cada um dos métodos de conectividade de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-183">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="fe8a0-184">as senhas de saudação para os usuários são definidas toohello senha mestra que você definiu no início do processo de implantação de saudação hello.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-184">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="fe8a0-185">Na documentação do hello, outros usuários mais funcionais são listados com suas senhas, o que você pode usar toosign no toohello implantado sistema.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-185">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span>

    ![Documentação de boas-vindas da SAP](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="fe8a0-187">Em algumas horas, um sistema de SAP IDES íntegro é implantado no Azure.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span></span>

<span data-ttu-id="fe8a0-188">Se você comprou uma assinatura de CAL do SAP, SAP totalmente dá suporte a implantações por meio de saudação CAL do SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-188">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="fe8a0-189">fila de suporte de saudação é BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="fe8a0-189">hello support queue is BC-VCM-CAL.</span></span>

