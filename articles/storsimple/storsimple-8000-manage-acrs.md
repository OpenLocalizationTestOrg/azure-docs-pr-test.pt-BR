---
title: registros de controle de acesso aaaManage em StorSimple | Microsoft Docs
description: Descreve como os registros de controle de acesso de toouse toodetermine (ACRs) quais hosts podem se conectar a tooa volume no dispositivo do StorSimple hello.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="2c10a-103">Use os registros de controle de acesso do hello StorSimple Manager serviço toomanage</span><span class="sxs-lookup"><span data-stu-id="2c10a-103">Use hello StorSimple Manager service toomanage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="2c10a-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2c10a-104">Overview</span></span>
<span data-ttu-id="2c10a-105">Registros de controle de acesso (ACRs) permitem que você toospecify quais hosts podem se conectar a tooa volume no dispositivo do StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="2c10a-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="2c10a-106">ACRs são definidos volume específico tooa e conter Olá iSCSI nomes qualificados (IQNs) de hosts de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c10a-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="2c10a-107">Quando um host tenta tooconnect tooa volume, o dispositivo Olá verifica Olá que ACR associado a esse volume do nome IQN do hello e se houver uma correspondência, hello conexão é estabelecida.</span><span class="sxs-lookup"><span data-stu-id="2c10a-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="2c10a-108">Olá registros de controle de acesso no hello **configuração** seção da sua folha de serviço do Gerenciador de dispositivos do StorSimple exibir todos os registros de controle de acesso de saudação com hello correspondentes IQNs dos hosts de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c10a-108">hello access control records in hello **Configuration** section of your StorSimple Device Manager service blade display all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="2c10a-109">Este tutorial explica Olá tarefas comuns relacionadas a ACR a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c10a-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="2c10a-110">Adicionar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="2c10a-110">Add an access control record</span></span>
* <span data-ttu-id="2c10a-111">Editar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="2c10a-111">Edit an access control record</span></span>
* <span data-ttu-id="2c10a-112">Excluir um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="2c10a-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="2c10a-113">Ao atribuir um volume de tooa ACR, lembre-se que Olá volume não é acessado simultaneamente por mais de um host não clusterizado porque isso pode corromper o volume de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c10a-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span>
> * <span data-ttu-id="2c10a-114">Ao excluir um ACR do volume, certifique-se de que host Olá correspondente não está acessando o volume Olá porque Olá exclusão pode levar a uma interrupção de leitura / gravação.</span><span class="sxs-lookup"><span data-stu-id="2c10a-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>

## <a name="get-hello-iqn"></a><span data-ttu-id="2c10a-115">Obter Olá IQN</span><span class="sxs-lookup"><span data-stu-id="2c10a-115">Get hello IQN</span></span>

<span data-ttu-id="2c10a-116">Execute Olá seguindo as etapas tooget Olá IQN de um host do Windows que está executando o Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="2c10a-116">Perform hello following steps tooget hello IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="2c10a-117">Adicionar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="2c10a-117">Add an access control record</span></span>
<span data-ttu-id="2c10a-118">Use Olá **configuração** seção Olá Gerenciador de dispositivos do StorSimple serviço folha tooadd ACRs.</span><span class="sxs-lookup"><span data-stu-id="2c10a-118">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooadd ACRs.</span></span> <span data-ttu-id="2c10a-119">Normalmente, você associará um ACR a um volume.</span><span class="sxs-lookup"><span data-stu-id="2c10a-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="2c10a-120">Execute Olá etapas tooadd um ACR a seguir.</span><span class="sxs-lookup"><span data-stu-id="2c10a-120">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-acr"></a><span data-ttu-id="2c10a-121">tooadd um ACR</span><span class="sxs-lookup"><span data-stu-id="2c10a-121">tooadd an ACR</span></span>

1. <span data-ttu-id="2c10a-122">Serviço de Gerenciador de dispositivos de StorSimple tooyour go, clique duas vezes Olá nome do serviço e, em seguida, dentro de saudação **configuração** seção, clique em **registros de controle de acesso**.</span><span class="sxs-lookup"><span data-stu-id="2c10a-122">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="2c10a-123">Em Olá **registros de controle de acesso** folha, clique em **+ adicionar ACR**.</span><span class="sxs-lookup"><span data-stu-id="2c10a-123">In hello **Access control records** blade, click **+ Add ACR**.</span></span>

    ![Clique em Adicionar ACR](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="2c10a-125">Em Olá **adicionar ACR** folha, Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="2c10a-125">In hello **Add ACR** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="2c10a-126">Informe um nome para o ACR.</span><span class="sxs-lookup"><span data-stu-id="2c10a-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="2c10a-127">Forneça o nome IQN de saudação do host do Windows Server em **iSCSI Initiator IQN (nome)**.</span><span class="sxs-lookup"><span data-stu-id="2c10a-127">Provide hello IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="2c10a-128">Clique em **adicionar** toocreate Olá ACR.</span><span class="sxs-lookup"><span data-stu-id="2c10a-128">Click **Add** toocreate hello ACR.</span></span>

        ![Clique em Adicionar ACR](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="2c10a-130">Olá recém-adicionado que exibirá ACR na listagem tabular de saudação de ACRs.</span><span class="sxs-lookup"><span data-stu-id="2c10a-130">hello newly added ACR will display in hello tabular listing of ACRs.</span></span>

    ![Clique em Adicionar ACR](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="2c10a-132">Editar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="2c10a-132">Edit an access control record</span></span>
<span data-ttu-id="2c10a-133">Use Olá **configuração** seção Olá Gerenciador de dispositivos do StorSimple serviço folha tooedit ACRs.</span><span class="sxs-lookup"><span data-stu-id="2c10a-133">You use hello **Configuration** section in hello StorSimple Device Manager service blade tooedit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="2c10a-134">É recomendável modificar somente os ACRs que não estão em uso no momento.</span><span class="sxs-lookup"><span data-stu-id="2c10a-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="2c10a-135">tooedit que um ACR associado a um volume que está em uso no momento, você deve primeiro colocar Olá volume offline.</span><span class="sxs-lookup"><span data-stu-id="2c10a-135">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="2c10a-136">Execute Olá etapas tooedit um ACR a seguir.</span><span class="sxs-lookup"><span data-stu-id="2c10a-136">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="2c10a-137">tooedit um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="2c10a-137">tooedit an access control record</span></span>
1.  <span data-ttu-id="2c10a-138">Serviço de Gerenciador de dispositivos de StorSimple tooyour go, clique duas vezes Olá nome do serviço e, em seguida, dentro de saudação **configuração** seção, clique em **registros de controle de acesso**.</span><span class="sxs-lookup"><span data-stu-id="2c10a-138">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Vá tooaccess registros de controle](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="2c10a-140">Na listagem tabular de saudação de registros de controle de acesso de saudação, clique em e selecione Olá ACR que quiser toomodify.</span><span class="sxs-lookup"><span data-stu-id="2c10a-140">In hello tabular listing of hello access control records, click and select hello ACR that you wish toomodify.</span></span>

    ![Editar os registros de controle de acesso](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="2c10a-142">Em Olá **editar registro de controle de acesso** folha, fornecer um diferentes IQN correspondente tooanother host.</span><span class="sxs-lookup"><span data-stu-id="2c10a-142">In hello **Edit access control record** blade, provide a different IQN corresponding tooanother host.</span></span>

    ![Editar os registros de controle de acesso](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="2c10a-144">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="2c10a-144">Click **Save**.</span></span> <span data-ttu-id="2c10a-145">Quando solicitado a confirmar, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="2c10a-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![Editar os registros de controle de acesso](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="2c10a-147">Você será notificado quando Olá ACR é atualizado.</span><span class="sxs-lookup"><span data-stu-id="2c10a-147">You are notified when hello ACR is updated.</span></span> <span data-ttu-id="2c10a-148">listagem tabular Olá também atualiza a alteração de saudação tooreflect.</span><span class="sxs-lookup"><span data-stu-id="2c10a-148">hello tabular listing also updates tooreflect hello change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="2c10a-149">Excluir um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="2c10a-149">Delete an access control record</span></span>
<span data-ttu-id="2c10a-150">Use Olá **configuração** seção Olá Gerenciador de dispositivos do StorSimple serviço folha toodelete ACRs.</span><span class="sxs-lookup"><span data-stu-id="2c10a-150">You use hello **Configuration** section in hello StorSimple Device Manager service blade toodelete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="2c10a-151">Você pode excluir somente os ACRs que não estejam em uso no momento.</span><span class="sxs-lookup"><span data-stu-id="2c10a-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="2c10a-152">toodelete que um ACR associado a um volume que está em uso no momento, você deve primeiro colocar Olá volume offline.</span><span class="sxs-lookup"><span data-stu-id="2c10a-152">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>

<span data-ttu-id="2c10a-153">Execute Olá seguindo as etapas toodelete um registro de controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="2c10a-153">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="2c10a-154">toodelete um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="2c10a-154">toodelete an access control record</span></span>
1.  <span data-ttu-id="2c10a-155">Serviço de Gerenciador de dispositivos de StorSimple tooyour go, clique duas vezes Olá nome do serviço e, em seguida, dentro de saudação **configuração** seção, clique em **registros de controle de acesso**.</span><span class="sxs-lookup"><span data-stu-id="2c10a-155">Go tooyour StorSimple Device Manager service, double-click hello service name, and then within hello **Configuration** section, click **Access control records**.</span></span>

    ![Vá tooaccess registros de controle](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="2c10a-157">Na listagem tabular de saudação de registros de controle de acesso de saudação, clique em e selecione Olá ACR que quiser toodelete.</span><span class="sxs-lookup"><span data-stu-id="2c10a-157">In hello tabular listing of hello access control records, click and select hello ACR that you wish toodelete.</span></span>

    ![Vá tooaccess registros de controle](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="2c10a-159">Menu de contexto tooinvoke hello e selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="2c10a-159">Right-click tooinvoke hello context menu and select **Delete**.</span></span>

    ![Vá tooaccess registros de controle](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="2c10a-161">Quando solicitada a confirmação, examine as informações de saudação e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="2c10a-161">When prompted for confirmation, review hello information and then click **Delete**.</span></span>

    ![Vá tooaccess registros de controle](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="2c10a-163">Você será notificado quando a exclusão de saudação é concluída.</span><span class="sxs-lookup"><span data-stu-id="2c10a-163">You are notified when hello deletion completes.</span></span> <span data-ttu-id="2c10a-164">listagem tabular Olá é atualizada tooreflect Olá exclusão.</span><span class="sxs-lookup"><span data-stu-id="2c10a-164">hello tabular listing is updated tooreflect hello deletion.</span></span>

    ![Vá tooaccess registros de controle](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="2c10a-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2c10a-166">Next steps</span></span>
* <span data-ttu-id="2c10a-167">Saiba mais sobre [como gerenciar volumes do StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="2c10a-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="2c10a-168">Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="2c10a-168">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

