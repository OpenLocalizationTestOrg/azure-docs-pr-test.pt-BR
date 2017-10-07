---
title: aaaManage registros de controle de acesso de matriz Virtual StorSimple | Microsoft Docs
description: "Descreve como os registros de controle de acesso de toomanage toodetermine (ACRs) quais hosts podem se conectar a tooa volume Olá matriz Virtual StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a><span data-ttu-id="1f8a3-103">Use o Gerenciador de dispositivo StorSimple toomanage registros de controle de acesso de matriz Virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="1f8a3-103">Use StorSimple Device Manager toomanage access control records for StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="1f8a3-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="1f8a3-104">Overview</span></span>

<span data-ttu-id="1f8a3-105">Registros de controle de acesso (ACRs) permitem que você toospecify quais hosts podem se conectar a tooa volume Olá StorSimple Virtual Array (também conhecido como Olá StorSimple no dispositivo virtual local).</span><span class="sxs-lookup"><span data-stu-id="1f8a3-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple Virtual Array (also known as hello StorSimple on-premises virtual device).</span></span> <span data-ttu-id="1f8a3-106">ACRs são definidos volume específico tooa e conter Olá iSCSI nomes qualificados (IQNs) de hosts de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="1f8a3-107">Quando um host tenta tooconnect tooa volume, dispositivo Olá verifica Olá ACR associado a esse volume do nome IQN do hello, e se houver uma correspondência, conexão Olá é estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name, and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="1f8a3-108">Olá **registros de controle de acesso** folha em Olá **configuração** seção do seu serviço de Gerenciador de dispositivos exibe todos os registros de controle de acesso de saudação com hello correspondentes IQNs dos hosts de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-108">hello **Access control records** blade within hello **Configuration** section of your Device Manager service displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

![Gerenciar registros de controle de acesso](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

<span data-ttu-id="1f8a3-110">Este tutorial explica Olá tarefas comuns relacionadas a ACR a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f8a3-110">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="1f8a3-111">Obter Olá IQN</span><span class="sxs-lookup"><span data-stu-id="1f8a3-111">Get hello IQN</span></span>
* <span data-ttu-id="1f8a3-112">Adicionar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="1f8a3-112">Add an access control record</span></span>
* <span data-ttu-id="1f8a3-113">Editar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="1f8a3-113">Edit an access control record</span></span>
* <span data-ttu-id="1f8a3-114">Excluir um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="1f8a3-114">Delete an access control record</span></span>

> [!IMPORTANT]
> 
> * <span data-ttu-id="1f8a3-115">Ao atribuir um volume de tooa ACR, lembre-se que Olá volume não é acessado simultaneamente por mais de um host não clusterizado porque isso pode corromper o volume de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-115">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="1f8a3-116">Ao excluir um ACR do volume, certifique-se de que host Olá correspondente não está acessando o volume Olá porque Olá exclusão pode levar a uma interrupção de leitura / gravação.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-116">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


## <a name="get-hello-iqn"></a><span data-ttu-id="1f8a3-117">Obter Olá IQN</span><span class="sxs-lookup"><span data-stu-id="1f8a3-117">Get hello IQN</span></span>

<span data-ttu-id="1f8a3-118">Execute Olá seguindo as etapas tooget Olá IQN de um host do Windows que está executando o Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-118">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a><span data-ttu-id="1f8a3-119">Adicionar um ACR</span><span class="sxs-lookup"><span data-stu-id="1f8a3-119">Add an ACR</span></span>

<span data-ttu-id="1f8a3-120">Você usa **registros de controle de acesso** folha em Olá **configuração** seção do seu serviço de Gerenciador de dispositivos de StorSimple tooadd ACRs.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-120">You use **Access control records** blade within hello **Configuration** section of your StorSimple Device Manager service tooadd ACRs.</span></span> <span data-ttu-id="1f8a3-121">Normalmente, você associa um ACR a um volume.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-121">Typically, you associate one ACR with one volume.</span></span>

<span data-ttu-id="1f8a3-122">Para obter informações sobre como associar um ACR um volume, vá muito[adicionar um volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="1f8a3-122">For information about associating an ACR with a volume, go too[add a volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f8a3-123">Ao atribuir um volume de tooa ACR, lembre-se que Olá volume não é acessado simultaneamente por mais de um host não clusterizado porque isso pode corromper o volume de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-123">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>


<span data-ttu-id="1f8a3-124">Execute Olá etapas tooadd um ACR a seguir.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-124">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="1f8a3-125">tooadd um ACR</span><span class="sxs-lookup"><span data-stu-id="1f8a3-125">tooadd an ACR</span></span>

1. <span data-ttu-id="1f8a3-126">Na página de aterrissagem do serviço hello, selecione o seu serviço, clique duas vezes Olá nome do serviço e, em seguida, dentro de saudação **configuração** seção, clique em **registros de controle de acesso**.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-126">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="1f8a3-127">Em Olá **registros de controle de acesso** folha, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-127">In hello **Access control records** blade, click **Add**.</span></span>
3. <span data-ttu-id="1f8a3-128">Em Olá **adicionar ACR** folha, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f8a3-128">In hello **Add ACR** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="1f8a3-129">Dê um **Nome** para o seu ACR.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-129">Supply a **Name** for your ACR.</span></span>
    
    2. <span data-ttu-id="1f8a3-130">Em **nome do iniciador iSCSI**, forneça o nome IQN de saudação do seu host do Windows.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-130">Under **iSCSI Initiator Name**, provide hello IQN name of your Windows host.</span></span> <span data-ttu-id="1f8a3-131">Olá tooget IQN do host do Windows Server, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f8a3-131">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
    3. <span data-ttu-id="1f8a3-132">Inicie o iniciador iSCSI da Microsoft hello no seu host do Windows.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-132">Start hello Microsoft iSCSI initiator on your Windows host.</span></span> <span data-ttu-id="1f8a3-133">Na janela de propriedades do iniciador iSCSI hello, em Olá **configuração** , selecione e copie a cadeia de caracteres de saudação do hello **nome do iniciador** campo.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-133">In hello iSCSI Initiator Properties window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
    <span data-ttu-id="1f8a3-134">Cole essa cadeia de caracteres hello **IQN** campo Olá **adicionar ACR** folha.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-134">Paste this string in hello **IQN** field in hello **Add ACR** blade.</span></span>
   
    6. <span data-ttu-id="1f8a3-135">Clique em **adicionar** tooadd Olá ACR.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-135">Click **Add** tooadd hello ACR.</span></span>  
   
        ![Adicionar registros de controle de acesso](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. <span data-ttu-id="1f8a3-137">Olá listagem tabular é atualizada tooreflect esta adição.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-137">hello tabular listing is updated tooreflect this addition.</span></span>

## <a name="edit-an-acr"></a><span data-ttu-id="1f8a3-138">Editar um ACR</span><span class="sxs-lookup"><span data-stu-id="1f8a3-138">Edit an ACR</span></span>

<span data-ttu-id="1f8a3-139">Use Olá **registros de controle de acesso** folha em Olá **configuração** seção do seu serviço de Gerenciador de dispositivos no hello ACRs tooedit portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-139">You use hello **Access control records** blade within hello **Configuration** section of your Device Manager service in hello Azure portal tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="1f8a3-140">Não modifique um ACR em uso no momento.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-140">You should not modify an ACR that is currently in use.</span></span> <span data-ttu-id="1f8a3-141">tooedit que um ACR associado a um volume que está em uso no momento, você deve primeiro colocar Olá volume offline.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-141">tooedit an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>


<span data-ttu-id="1f8a3-142">Execute Olá etapas tooedit um ACR a seguir.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-142">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-acr"></a><span data-ttu-id="1f8a3-143">tooedit um ACR</span><span class="sxs-lookup"><span data-stu-id="1f8a3-143">tooedit an ACR</span></span>

1. <span data-ttu-id="1f8a3-144">Na página de aterrissagem do serviço hello, selecione o seu serviço, clique duas vezes Olá nome do serviço e, em seguida, dentro de saudação **configuração** seção, **registros de controle de acesso**.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-144">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>
2. <span data-ttu-id="1f8a3-145">Em Olá **registros de controle de acesso** folha da listagem de saudação tabular dos registros de controle de acesso Olá, clique duas vezes em Olá ACR que quiser toomodify.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-145">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="1f8a3-146">Em Olá **editar registros de controle de acesso** folha, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f8a3-146">In hello **Edit access control records** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="1f8a3-147">Fornece hello IQN para Olá ACR.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-147">Supply hello IQN for hello ACR.</span></span>
   
    2. <span data-ttu-id="1f8a3-148">Clique em **salvar** na parte superior de saudação do hello folha toosave Olá modificar ACR.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-148">Click **Save** at hello top of hello blade toosave hello modified ACR.</span></span> <span data-ttu-id="1f8a3-149">Você verá Olá a seguinte mensagem de confirmação:</span><span class="sxs-lookup"><span data-stu-id="1f8a3-149">You see hello following confirmation message:</span></span>
   
        ![Editar os registros de controle de acesso](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a><span data-ttu-id="1f8a3-151">Excluir um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="1f8a3-151">Delete an access control record</span></span>

<span data-ttu-id="1f8a3-152">Use Olá **configuração** página Olá ACRs toodelete portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-152">You use hello **Configuration** page in hello Azure portal toodelete ACRs.</span></span>

> [!NOTE]
> 
> * <span data-ttu-id="1f8a3-153">Não exclua um ACR em uso no momento.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-153">You should not delete an ACR that is currently in use.</span></span> <span data-ttu-id="1f8a3-154">toodelete que um ACR associado a um volume que está em uso no momento, você deve primeiro colocar Olá volume offline.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-154">toodelete an ACR associated with a volume that is currently in use, you should first take hello volume offline.</span></span>
> * <span data-ttu-id="1f8a3-155">Ao excluir um ACR do volume, certifique-se de que host Olá correspondente não está acessando o volume Olá porque Olá exclusão pode levar a uma interrupção de leitura / gravação.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-155">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>


<span data-ttu-id="1f8a3-156">Execute Olá seguindo as etapas toodelete um registro de controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-156">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="1f8a3-157">toodelete um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="1f8a3-157">toodelete an access control record</span></span>

1. <span data-ttu-id="1f8a3-158">Na página de aterrissagem do serviço hello, selecione o seu serviço, clique duas vezes Olá nome do serviço e, em seguida, dentro de saudação **configuração** seção, **registros de controle de acesso**.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-158">On hello service landing page, select your service, double-click hello service name, and then within hello **Configuration** section, **Access control records**.</span></span>

2. <span data-ttu-id="1f8a3-159">Em Olá **registros de controle de acesso** folha da listagem de saudação tabular dos registros de controle de acesso Olá, clique duas vezes em Olá ACR que quiser toodelete.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-159">In hello **Access control records** blade, from hello tabular listing of hello access control records, double-click hello ACR that you wish toodelete.</span></span>

3. <span data-ttu-id="1f8a3-160">Na folha de registros do controle de acesso de edição hello, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-160">In hello Edit access control records blade, click **Delete**.</span></span>
   
    ![Excluir ACRS](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. <span data-ttu-id="1f8a3-162">Quando solicitado a confirmar, clique em **excluir** toocontinue com exclusão hello.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-162">When prompted for confirmation, click **Delete** toocontinue with hello deletion.</span></span> <span data-ttu-id="1f8a3-163">listagem tabular Olá é atualizada tooreflect Olá exclusão.</span><span class="sxs-lookup"><span data-stu-id="1f8a3-163">hello tabular listing is updated tooreflect hello deletion.</span></span>
   
   ![Mensagem de aviso](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a><span data-ttu-id="1f8a3-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1f8a3-165">Next steps</span></span>

* <span data-ttu-id="1f8a3-166">Saiba mais sobre [Adicionar volumes e configurar ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span><span class="sxs-lookup"><span data-stu-id="1f8a3-166">Learn more about [adding volumes and configuring ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).</span></span>

