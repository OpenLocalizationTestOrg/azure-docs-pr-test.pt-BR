---
title: "Visão geral do Microsoft Azure StorSimple e do programa Cloud Solutions Provider | Microsoft Docs"
description: "Uma visão geral sobre o StorSimple e o CSP para parceiros do StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/08/2017
ms.author: alkohli
ms.openlocfilehash: c8cb51093142146fc7d43b51a62d949f6cc38988
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="d0022-103">Implantar o StorSimple Virtual Array para o programa Cloud Solution Provider</span><span class="sxs-lookup"><span data-stu-id="d0022-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="d0022-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d0022-104">Overview</span></span>

<span data-ttu-id="d0022-105">Matriz de StorSimple Virtual pode ser implantado pelos parceiros de provedor de solução de nuvem (CSP) para seus clientes.</span><span class="sxs-lookup"><span data-stu-id="d0022-105">StorSimple Virtual Array can be deployed by the Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="d0022-106">Um parceiro CSP pode criar um serviço do Gerenciador de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="d0022-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="d0022-107">Esse serviço, em seguida, pode ser usado para implantar e gerenciar a matriz Virtual do StorSimple e os compartilhamentos associados, volumes e backups.</span><span class="sxs-lookup"><span data-stu-id="d0022-107">This service can then be used to deploy and manage StorSimple Virtual Array and the associated shares, volumes, and backups.</span></span>

<span data-ttu-id="d0022-108">Este artigo descreve como um parceiro CSP pode adicionar um cliente ou uma nova assinatura para um cliente existente e, em seguida, crie um serviço para implantar uma matriz Virtual StorSimple no CSP.</span><span class="sxs-lookup"><span data-stu-id="d0022-108">This article describes how a CSP partner can add a customer or a new subscription to an existing customer and then create a service to deploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d0022-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d0022-109">Prerequisites</span></span>

<span data-ttu-id="d0022-110">Antes de começar, verifique se:</span><span class="sxs-lookup"><span data-stu-id="d0022-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="d0022-111">Você está inscrito no programa CSP.</span><span class="sxs-lookup"><span data-stu-id="d0022-111">You are enrolled under the CSP program.</span></span>
- <span data-ttu-id="d0022-112">Você tem credenciais de logon válidas do [Partner Center](http://partnercenter.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="d0022-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="d0022-113">As credenciais permitem que você entrar no portal de parceiros para adicionar novos clientes, procurar clientes ou navegar para uma conta de cliente no painel do parceiro.</span><span class="sxs-lookup"><span data-stu-id="d0022-113">The credentials enable you to sign in to the Partner portal to add new customers, search for customers, or navigate to a customer account from the Partner dashboard.</span></span> <span data-ttu-id="d0022-114">O CSP pode funcionar como um administrador do StorSimple em nome do cliente no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d0022-114">The CSP can function as a StorSimple administrator on behalf of the customer in the Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="d0022-115">Adicionar um cliente</span><span class="sxs-lookup"><span data-stu-id="d0022-115">Add a customer</span></span>

<span data-ttu-id="d0022-116">Se você adicionar um cliente, uma assinatura é criada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="d0022-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="d0022-117">Para adicionar um cliente (e criar automaticamente uma assinatura), execute as seguintes etapas no portal de parceiros.</span><span class="sxs-lookup"><span data-stu-id="d0022-117">To add a customer (and automatically create a subscription), perform the following steps in the Partner portal.</span></span>

1. <span data-ttu-id="d0022-118">Vá para o [Partner Center](http://partnercenter.microsoft.com/) e entre usando suas credenciais do CSP.</span><span class="sxs-lookup"><span data-stu-id="d0022-118">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="d0022-119">Clique em **Painel**.</span><span class="sxs-lookup"><span data-stu-id="d0022-119">Click **Dashboard**.</span></span>

     ![Painel no Partner Center](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="d0022-121">No painel esquerdo, clique em **Clientes**.</span><span class="sxs-lookup"><span data-stu-id="d0022-121">In the left-pane, click **Customers**.</span></span> <span data-ttu-id="d0022-122">No painel direito, clique em **adicionar clientes**.</span><span class="sxs-lookup"><span data-stu-id="d0022-122">In the right-pane, click **Add customers**.</span></span> <span data-ttu-id="d0022-123">Insira os detalhes do cliente.</span><span class="sxs-lookup"><span data-stu-id="d0022-123">Enter the details of the customer.</span></span> <span data-ttu-id="d0022-124">Clique em **próximo: assinaturas** para criar uma assinatura de cliente.</span><span class="sxs-lookup"><span data-stu-id="d0022-124">Click **Next: Subscriptions** to create a customer subscription.</span></span>

    ![Adicionar cliente](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="d0022-126">Selecione a oferta **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="d0022-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="d0022-127">Role até a parte inferior da página e clique em **revisão**.</span><span class="sxs-lookup"><span data-stu-id="d0022-127">Scroll to the bottom of the page and click **Review**.</span></span>

    ![Revise as informações da assinatura](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="d0022-129">Examine as informações e clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="d0022-129">Review the information and click **Submit**.</span></span>

    ![Assinatura de envio](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="d0022-131">Salve as informações de confirmação para referência futura.</span><span class="sxs-lookup"><span data-stu-id="d0022-131">Save the confirmation information for future reference.</span></span>

    ![Salvar confirmação](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="d0022-133">Localizar ou navegue até o cliente você acabou de adicionar.</span><span class="sxs-lookup"><span data-stu-id="d0022-133">Find or navigate to the customer you just added.</span></span> <span data-ttu-id="d0022-134">Clique no **Nome da empresa** para fazer drill down nos detalhes.</span><span class="sxs-lookup"><span data-stu-id="d0022-134">Click the **Company name** to drill down into the details.</span></span>

    ![Procurar o cliente](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="d0022-136">No painel esquerdo, selecione **Gerenciamento de serviços**.</span><span class="sxs-lookup"><span data-stu-id="d0022-136">In the left-pane, select **Service management**.</span></span> <span data-ttu-id="d0022-137">No painel direito, em **Administrar serviços**, clique em **Portal de Gerenciamento do Microsoft Azure** para entrar como um administrador do Azure para seu cliente.</span><span class="sxs-lookup"><span data-stu-id="d0022-137">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span></span>

    ![Fazer logon no portal do Azure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="d0022-139">Para criar um Gerenciador de Dispositivos do StorSimple, clique em **+ Novo** e procure ou navegue até **Série de Dispositivos Virtuais do StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="d0022-139">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="d0022-140">Para saber mais, vá para [Implantar um serviço do Gerenciador de Dispositivos do StorSimple](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="d0022-140">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Criar serviço Gerenciador de Dispositivos do StorSimple](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="d0022-142">Adicionar uma assinatura</span><span class="sxs-lookup"><span data-stu-id="d0022-142">Add a subscription</span></span>

<span data-ttu-id="d0022-143">Em alguns casos, você pode ter um cliente existente e você precisa adicionar uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="d0022-143">In some instances, you may have an existing customer, and you need to add a subscription.</span></span> <span data-ttu-id="d0022-144">Para adicionar uma assinatura a um cliente existente, execute as seguintes etapas no portal de parceiros.</span><span class="sxs-lookup"><span data-stu-id="d0022-144">To add a subscription to an existing customer, perform the following steps in the Partner portal.</span></span>

1. <span data-ttu-id="d0022-145">Vá para o [Partner Center](http://partnercenter.microsoft.com/) e entre usando suas credenciais do CSP.</span><span class="sxs-lookup"><span data-stu-id="d0022-145">Go to the [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="d0022-146">Clique em **Painel**.</span><span class="sxs-lookup"><span data-stu-id="d0022-146">Click **Dashboard**.</span></span>

     ![Painel no Partner Center](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="d0022-148">No painel esquerdo, clique em **Clientes**.</span><span class="sxs-lookup"><span data-stu-id="d0022-148">In the left-pane, click **Customers**.</span></span> <span data-ttu-id="d0022-149">Localizar ou navegue para o cliente para o qual você deseja adicionar uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="d0022-149">Find or navigate to the customer you want to add a subscription to.</span></span> <span data-ttu-id="d0022-150">Clique o ![ícone de verificação de expansão](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) ícone para expandir a linha para o nome da empresa para o cliente.</span><span class="sxs-lookup"><span data-stu-id="d0022-150">Click the ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon to expand the row for the company name for your customer.</span></span> <span data-ttu-id="d0022-151">Em detalhes, clique em **adicionar assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="d0022-151">In the details, click **Add subscriptions**.</span></span>

    ![Clientes](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="d0022-153">Verificar **Microsoft Azure** para o **principais ofertas** na assinatura e clique em **enviar**.</span><span class="sxs-lookup"><span data-stu-id="d0022-153">Check **Microsoft Azure** for the **Top offers** in the subscription and click **Submit**.</span></span> <span data-ttu-id="d0022-154">Isso cria uma nova assinatura.</span><span class="sxs-lookup"><span data-stu-id="d0022-154">This creates a new subscription.</span></span>

    ![Adicionar nova assinatura](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="d0022-156">Depois de uma nova assinatura for criada, clique em  **<-- Clientes** no painel esquerdo para voltar para a página de **Clientes**.</span><span class="sxs-lookup"><span data-stu-id="d0022-156">After a new subscription is created, click **<-- Customers** in the left-pane to return to the **Customers** page.</span></span> <span data-ttu-id="d0022-157">Pesquisa do cliente para o qual você acabou de criar uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="d0022-157">Search for the customer for whom you just created a subscription.</span></span> <span data-ttu-id="d0022-158">Clique no **Nome da empresa** para fazer drill down nos detalhes.</span><span class="sxs-lookup"><span data-stu-id="d0022-158">Click the **Company name** to drill down into the details.</span></span>

    ![Procurar o cliente](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="d0022-160">No painel esquerdo, selecione **Gerenciamento de serviços**.</span><span class="sxs-lookup"><span data-stu-id="d0022-160">In the left-pane, select **Service management**.</span></span> <span data-ttu-id="d0022-161">No painel direito, em **Administrar serviços**, clique em **Portal de Gerenciamento do Microsoft Azure** para entrar como um administrador do Azure para seu cliente.</span><span class="sxs-lookup"><span data-stu-id="d0022-161">In the right-pane, under **Administer services**, click **Microsoft Azure Management Portal** to sign in as an Azure administrator for your customer.</span></span>

    ![Fazer logon no portal do Azure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="d0022-163">Para criar um Gerenciador de Dispositivos do StorSimple, clique em **+ Novo** e procure ou navegue até **Série de Dispositivos Virtuais do StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="d0022-163">To create a StorSimple Device Manager, click **+ New** and search for or navigate to **StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="d0022-164">Para saber mais, vá para [Implantar um serviço do Gerenciador de Dispositivos do StorSimple](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="d0022-164">For more information, go to [Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Criar serviço Gerenciador de Dispositivos do StorSimple](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="d0022-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d0022-166">Next steps</span></span>

- <span data-ttu-id="d0022-167">Se tiver mais dúvidas relacionadas ao StorSimple no CSP, visite [StorSimple for CSP: Frequently asked questions](storsimple-partner-csp-faq.md) (StorSimple no CSP: perguntas frequentes).</span><span class="sxs-lookup"><span data-stu-id="d0022-167">If you have more questions regarding the StorSimple in CSP, go to [StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="d0022-168">Se você estiver pronto para implantar seu StorSimple, acesse [Implantar o StorSimple para CSP](storsimple-partner-csp-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d0022-168">If you are ready to deploy your StorSimple, go to [Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
