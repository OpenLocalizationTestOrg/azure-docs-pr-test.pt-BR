---
title: "aaaMicrosoft StorSimple do Azure e visão geral do programa de provedor de soluções de nuvem | Microsoft Docs"
description: "Uma visão geral sobre Olá StorSimple e o CSP para parceiros do StorSimple."
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
ms.openlocfilehash: b5d999f2fbb9a27e7404ff454957b29dbef56af6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array-for-cloud-solution-provider-program"></a><span data-ttu-id="53119-103">Implantar o StorSimple Virtual Array para o programa Cloud Solution Provider</span><span class="sxs-lookup"><span data-stu-id="53119-103">Deploy StorSimple Virtual Array for Cloud Solution Provider Program</span></span>

## <a name="overview"></a><span data-ttu-id="53119-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="53119-104">Overview</span></span>

<span data-ttu-id="53119-105">Matriz Virtual StorSimple pode ser implantado por parceiros de provedor de solução de nuvem (CSP) Olá para seus clientes.</span><span class="sxs-lookup"><span data-stu-id="53119-105">StorSimple Virtual Array can be deployed by hello Cloud Solution Provider (CSP) partners for their customers.</span></span> <span data-ttu-id="53119-106">Um parceiro CSP pode criar um serviço do Gerenciador de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="53119-106">A CSP partner can create a StorSimple Device Manager service.</span></span> <span data-ttu-id="53119-107">Esse serviço pode ser usado toodeploy e gerenciar matriz Virtual do StorSimple e Olá associados compartilhamentos, volumes e backups.</span><span class="sxs-lookup"><span data-stu-id="53119-107">This service can then be used toodeploy and manage StorSimple Virtual Array and hello associated shares, volumes, and backups.</span></span>

<span data-ttu-id="53119-108">Este artigo descreve como um parceiro CSP pode adicionar um cliente ou um novo cliente de assinatura tooan existente e, em seguida, criar um serviço toodeploy uma matriz Virtual do StorSimple no CSP.</span><span class="sxs-lookup"><span data-stu-id="53119-108">This article describes how a CSP partner can add a customer or a new subscription tooan existing customer and then create a service toodeploy a StorSimple Virtual Array in CSP.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53119-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="53119-109">Prerequisites</span></span>

<span data-ttu-id="53119-110">Antes de começar, verifique se:</span><span class="sxs-lookup"><span data-stu-id="53119-110">Before you begin, ensure that:</span></span>

- <span data-ttu-id="53119-111">Você está inscrito no programa CSP hello.</span><span class="sxs-lookup"><span data-stu-id="53119-111">You are enrolled under hello CSP program.</span></span>
- <span data-ttu-id="53119-112">Você tem credenciais de logon válidas do [Partner Center](http://partnercenter.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="53119-112">You have valid [Partner Center](http://partnercenter.microsoft.com/) login credentials.</span></span> <span data-ttu-id="53119-113">Olá credenciais permitem toosign novos clientes do toohello parceiro tooadd portal, procurar clientes ou navegue tooa conta do cliente do painel de parceiro hello.</span><span class="sxs-lookup"><span data-stu-id="53119-113">hello credentials enable you toosign in toohello Partner portal tooadd new customers, search for customers, or navigate tooa customer account from hello Partner dashboard.</span></span> <span data-ttu-id="53119-114">Olá CSP pode funcionar como um administrador do StorSimple em nome do cliente Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="53119-114">hello CSP can function as a StorSimple administrator on behalf of hello customer in hello Azure portal.</span></span>
                             
## <a name="add-a-customer"></a><span data-ttu-id="53119-115">Adicionar um cliente</span><span class="sxs-lookup"><span data-stu-id="53119-115">Add a customer</span></span>

<span data-ttu-id="53119-116">Se você adicionar um cliente, uma assinatura é criada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="53119-116">If you add a customer, a subscription is automatically created.</span></span> <span data-ttu-id="53119-117">um cliente de tooadd (e criar automaticamente uma assinatura), executar Olá seguindo as etapas no portal de parceiros de saudação.</span><span class="sxs-lookup"><span data-stu-id="53119-117">tooadd a customer (and automatically create a subscription), perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="53119-118">Vá toohello [Partner Center](http://partnercenter.microsoft.com/) e entre com suas credenciais do CSP.</span><span class="sxs-lookup"><span data-stu-id="53119-118">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="53119-119">Clique em **Painel**.</span><span class="sxs-lookup"><span data-stu-id="53119-119">Click **Dashboard**.</span></span>

     ![Painel no Partner Center](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="53119-121">No painel esquerdo do hello, clique em **clientes**.</span><span class="sxs-lookup"><span data-stu-id="53119-121">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="53119-122">No painel direito de saudação, clique em **adicionar clientes**.</span><span class="sxs-lookup"><span data-stu-id="53119-122">In hello right-pane, click **Add customers**.</span></span> <span data-ttu-id="53119-123">Insira detalhes de saudação do cliente hello.</span><span class="sxs-lookup"><span data-stu-id="53119-123">Enter hello details of hello customer.</span></span> <span data-ttu-id="53119-124">Clique em **próximo: assinaturas** toocreate uma assinatura de cliente.</span><span class="sxs-lookup"><span data-stu-id="53119-124">Click **Next: Subscriptions** toocreate a customer subscription.</span></span>

    ![Adicionar cliente](./media/storsimple-partner-csp-deploy/image2.png)

3.  <span data-ttu-id="53119-126">Selecione a oferta **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="53119-126">Select **Microsoft Azure** offer.</span></span> <span data-ttu-id="53119-127">Rolar para o fim da página hello e clique em toohello **revisão**.</span><span class="sxs-lookup"><span data-stu-id="53119-127">Scroll toohello bottom of hello page and click **Review**.</span></span>

    ![Revise as informações da assinatura](./media/storsimple-partner-csp-deploy/image3.png)
                              
4. <span data-ttu-id="53119-129">Revise as informações de saudação e clique em **enviar**.</span><span class="sxs-lookup"><span data-stu-id="53119-129">Review hello information and click **Submit**.</span></span>

    ![Assinatura de envio](./media/storsimple-partner-csp-deploy/image4.png)

5. <span data-ttu-id="53119-131">Salve as informações de confirmação de saudação para referência futura.</span><span class="sxs-lookup"><span data-stu-id="53119-131">Save hello confirmation information for future reference.</span></span>

    ![Salvar confirmação](./media/storsimple-partner-csp-deploy/image5.png)

6. <span data-ttu-id="53119-133">Localizar ou navegar cliente toohello que você acabou de adicionar.</span><span class="sxs-lookup"><span data-stu-id="53119-133">Find or navigate toohello customer you just added.</span></span> <span data-ttu-id="53119-134">Clique em Olá **nome da empresa** toodrill para baixo em detalhes de saudação.</span><span class="sxs-lookup"><span data-stu-id="53119-134">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Pesquisa de cliente Olá](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="53119-136">No painel esquerdo do hello, selecione **gerenciamento de serviço**.</span><span class="sxs-lookup"><span data-stu-id="53119-136">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="53119-137">Em Olá painel direito, em **administrar serviços**, clique em **Portal de gerenciamento do Microsoft Azure** toosign em como um administrador do Azure para seu cliente.</span><span class="sxs-lookup"><span data-stu-id="53119-137">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![Faça logon no portal de tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="53119-139">toocreate um Gerenciador de dispositivos de StorSimple, clique em **+ novo** e pesquise ou navegue muito**série de dispositivo Virtual StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="53119-139">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="53119-140">Para obter mais informações, vá muito[implantar um serviço de Gerenciador de dispositivos de StorSimple](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="53119-140">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Criar serviço Gerenciador de Dispositivos do StorSimple](./media/storsimple-partner-csp-deploy/image8.png)


## <a name="add-a-subscription"></a><span data-ttu-id="53119-142">Adicionar uma assinatura</span><span class="sxs-lookup"><span data-stu-id="53119-142">Add a subscription</span></span>

<span data-ttu-id="53119-143">Em alguns casos, você pode ter um cliente existente e você precisa tooadd uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="53119-143">In some instances, you may have an existing customer, and you need tooadd a subscription.</span></span> <span data-ttu-id="53119-144">tooadd um cliente existente do tooan de assinatura, execute Olá seguindo as etapas no portal de parceiros de saudação.</span><span class="sxs-lookup"><span data-stu-id="53119-144">tooadd a subscription tooan existing customer, perform hello following steps in hello Partner portal.</span></span>

1. <span data-ttu-id="53119-145">Vá toohello [Partner Center](http://partnercenter.microsoft.com/) e entre com suas credenciais do CSP.</span><span class="sxs-lookup"><span data-stu-id="53119-145">Go toohello [Partner Center](http://partnercenter.microsoft.com/) and sign in using your CSP credentials.</span></span> <span data-ttu-id="53119-146">Clique em **Painel**.</span><span class="sxs-lookup"><span data-stu-id="53119-146">Click **Dashboard**.</span></span>

     ![Painel no Partner Center](./media/storsimple-partner-csp-deploy/image1.png)
                              
2. <span data-ttu-id="53119-148">No painel esquerdo do hello, clique em **clientes**.</span><span class="sxs-lookup"><span data-stu-id="53119-148">In hello left-pane, click **Customers**.</span></span> <span data-ttu-id="53119-149">Localizar ou navegar toohello cliente que quiser tooadd uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="53119-149">Find or navigate toohello customer you want tooadd a subscription to.</span></span> <span data-ttu-id="53119-150">Clique em Olá ![ícone de verificação de expansão](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) ícone tooexpand Olá linha hello da empresa para o cliente.</span><span class="sxs-lookup"><span data-stu-id="53119-150">Click hello ![Expand check icon](./media/storsimple-partner-csp-deploy/expand_pane_icon.png) icon tooexpand hello row for hello company name for your customer.</span></span> <span data-ttu-id="53119-151">Nos detalhes de saudação, clique em **adicionar assinaturas**.</span><span class="sxs-lookup"><span data-stu-id="53119-151">In hello details, click **Add subscriptions**.</span></span>

    ![Clientes](./media/storsimple-partner-csp-deploy/image10.png)

3. <span data-ttu-id="53119-153">Verificar **Microsoft Azure** para Olá **principais ofertas** na assinatura hello e clique em **enviar**.</span><span class="sxs-lookup"><span data-stu-id="53119-153">Check **Microsoft Azure** for hello **Top offers** in hello subscription and click **Submit**.</span></span> <span data-ttu-id="53119-154">Isso cria uma nova assinatura.</span><span class="sxs-lookup"><span data-stu-id="53119-154">This creates a new subscription.</span></span>

    ![Adicionar nova assinatura](./media/storsimple-partner-csp-deploy/image11.png)

6. <span data-ttu-id="53119-156">Depois que uma nova assinatura é criada, clique em **< – clientes** em Olá painel esquerdo tooreturn toohello **clientes** página.</span><span class="sxs-lookup"><span data-stu-id="53119-156">After a new subscription is created, click **<-- Customers** in hello left-pane tooreturn toohello **Customers** page.</span></span> <span data-ttu-id="53119-157">Pesquisa de cliente Olá para o qual você acabou de criar uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="53119-157">Search for hello customer for whom you just created a subscription.</span></span> <span data-ttu-id="53119-158">Clique em Olá **nome da empresa** toodrill para baixo em detalhes de saudação.</span><span class="sxs-lookup"><span data-stu-id="53119-158">Click hello **Company name** toodrill down into hello details.</span></span>

    ![Pesquisa de cliente Olá](./media/storsimple-partner-csp-deploy/image6.png)  

7. <span data-ttu-id="53119-160">No painel esquerdo do hello, selecione **gerenciamento de serviço**.</span><span class="sxs-lookup"><span data-stu-id="53119-160">In hello left-pane, select **Service management**.</span></span> <span data-ttu-id="53119-161">Em Olá painel direito, em **administrar serviços**, clique em **Portal de gerenciamento do Microsoft Azure** toosign em como um administrador do Azure para seu cliente.</span><span class="sxs-lookup"><span data-stu-id="53119-161">In hello right-pane, under **Administer services**, click **Microsoft Azure Management Portal** toosign in as an Azure administrator for your customer.</span></span>

    ![Faça logon no portal de tooAzure](./media/storsimple-partner-csp-deploy/image9.png)

8. <span data-ttu-id="53119-163">toocreate um Gerenciador de dispositivos de StorSimple, clique em **+ novo** e pesquise ou navegue muito**série de dispositivo Virtual StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="53119-163">toocreate a StorSimple Device Manager, click **+ New** and search for or navigate too**StorSimple Virtual Device Series**.</span></span> <span data-ttu-id="53119-164">Para obter mais informações, vá muito[implantar um serviço de Gerenciador de dispositivos de StorSimple](storsimple-virtual-array-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="53119-164">For more information, go too[Deploy a StorSimple Device Manager service](storsimple-virtual-array-manage-service.md).</span></span>

    ![Criar serviço Gerenciador de Dispositivos do StorSimple](./media/storsimple-partner-csp-deploy/image8.png)

## <a name="next-steps"></a><span data-ttu-id="53119-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="53119-166">Next steps</span></span>

- <span data-ttu-id="53119-167">Se você tiver mais dúvidas sobre Olá StorSimple no CSP, vá muito[StorSimple no CSP: perguntas frequentes](storsimple-partner-csp-faq.md).</span><span class="sxs-lookup"><span data-stu-id="53119-167">If you have more questions regarding hello StorSimple in CSP, go too[StorSimple in CSP: Frequently asked questions](storsimple-partner-csp-faq.md).</span></span>
- <span data-ttu-id="53119-168">Se você estiver pronto toodeploy seu StorSimple, ir muito[implantar seu StorSimple no CSP](storsimple-partner-csp-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="53119-168">If you are ready toodeploy your StorSimple, go too[Deploy your StorSimple in CSP](storsimple-partner-csp-deploy.md).</span></span>
