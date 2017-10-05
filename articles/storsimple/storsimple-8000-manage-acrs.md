---
title: Gerenciar registros de controle de acesso no StorSimple | Microsoft Docs
description: Descreve como usar os ACRs (registros de controle de acesso) para determinar quais hosts podem se conectar a um volume no dispositivo StorSimple.
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
ms.openlocfilehash: 9173e34f889ce1c082b20bb382cb6ca9a03dd797
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="75f7a-103">Usar o serviço StorSimple Manager para gerenciar registros de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="75f7a-103">Use the StorSimple Manager service to manage access control records</span></span>

## <a name="overview"></a><span data-ttu-id="75f7a-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="75f7a-104">Overview</span></span>
<span data-ttu-id="75f7a-105">Os ACRs (registros de controle de acesso) permitem especificar quais hosts podem se conectar a um volume no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="75f7a-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="75f7a-106">Os ACRs são definidos para um volume específico e contêm os IQNs (Nomes Qualificados iSCSI) dos hosts.</span><span class="sxs-lookup"><span data-stu-id="75f7a-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="75f7a-107">Quando um host tenta se conectar a um volume, o dispositivo verifica o nome do IQN no ACR associado a esse volume e, se houver correspondência, a conexão será estabelecida.</span><span class="sxs-lookup"><span data-stu-id="75f7a-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="75f7a-108">Os registros de controle de acesso da seção **Configuração** da folha do serviço do Gerenciador de Dispositivos do StorSimple exibe todos os registros de controle de acesso com os IQNs correspondentes dos hosts.</span><span class="sxs-lookup"><span data-stu-id="75f7a-108">The access control records in the **Configuration** section of your StorSimple Device Manager service blade display all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="75f7a-109">Este tutorial explica as seguintes tarefas comuns relacionadas ao ACR:</span><span class="sxs-lookup"><span data-stu-id="75f7a-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="75f7a-110">Adicionar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="75f7a-110">Add an access control record</span></span>
* <span data-ttu-id="75f7a-111">Editar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="75f7a-111">Edit an access control record</span></span>
* <span data-ttu-id="75f7a-112">Excluir um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="75f7a-112">Delete an access control record</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="75f7a-113">Ao atribuir um ACR a um volume, lembre-se que o volume não é acessado simultaneamente por mais de um host não clusterizado porque isso poderia corromper o volume.</span><span class="sxs-lookup"><span data-stu-id="75f7a-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span>
> * <span data-ttu-id="75f7a-114">Ao excluir um ACR de um volume, certifique-se de que o host correspondente não esteja acessando o volume porque a exclusão poderia resultar em uma interrupção de leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="75f7a-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>

## <a name="get-the-iqn"></a><span data-ttu-id="75f7a-115">Obter o IQN</span><span class="sxs-lookup"><span data-stu-id="75f7a-115">Get the IQN</span></span>

<span data-ttu-id="75f7a-116">Execute as seguintes etapas para obter o IQN de um host do Windows que está executando o Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="75f7a-116">Perform the following steps to get the IQN of a Windows host that is running Windows Server 2012.</span></span>

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a><span data-ttu-id="75f7a-117">Adicionar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="75f7a-117">Add an access control record</span></span>
<span data-ttu-id="75f7a-118">Use a seção **Configuração** na folha do serviço do Gerenciador de Dispositivos do StorSimple para adicionar ACRs.</span><span class="sxs-lookup"><span data-stu-id="75f7a-118">You use the **Configuration** section in the StorSimple Device Manager service blade to add ACRs.</span></span> <span data-ttu-id="75f7a-119">Normalmente, você associará um ACR a um volume.</span><span class="sxs-lookup"><span data-stu-id="75f7a-119">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="75f7a-120">Execute as etapas a seguir para adicionar um ACR.</span><span class="sxs-lookup"><span data-stu-id="75f7a-120">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-acr"></a><span data-ttu-id="75f7a-121">Para adicionar um ACR</span><span class="sxs-lookup"><span data-stu-id="75f7a-121">To add an ACR</span></span>

1. <span data-ttu-id="75f7a-122">Acesse seu serviço do Gerenciador de Dispositivos do StorSimple, clique duas vezes no nome do serviço e, na seção **Configuração**, clique em **Registros de controle de acesso**.</span><span class="sxs-lookup"><span data-stu-id="75f7a-122">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>
2. <span data-ttu-id="75f7a-123">Na folha **Registros de controle de acesso**, clique em **+ Adicionar ACR**.</span><span class="sxs-lookup"><span data-stu-id="75f7a-123">In the **Access control records** blade, click **+ Add ACR**.</span></span>

    ![Clique em Adicionar ACR](./media/storsimple-8000-manage-acrs/createacr1.png)

3. <span data-ttu-id="75f7a-125">Na folha **Adicionar ACR**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="75f7a-125">In the **Add ACR** blade, do the following steps:</span></span>

    1. <span data-ttu-id="75f7a-126">Informe um nome para o ACR.</span><span class="sxs-lookup"><span data-stu-id="75f7a-126">Supply a name for your ACR.</span></span>
    
    2. <span data-ttu-id="75f7a-127">Forneça o nome IQN do host do Windows Server em **Nome do Iniciador iSCSI (IQN)**.</span><span class="sxs-lookup"><span data-stu-id="75f7a-127">Provide the IQN name of your Windows Server host under **iSCSI Initiator Name (IQN)**.</span></span>

    3. <span data-ttu-id="75f7a-128">Clique em **Adicionar** para criar o ACR.</span><span class="sxs-lookup"><span data-stu-id="75f7a-128">Click **Add** to create the ACR.</span></span>

        ![Clique em Adicionar ACR](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  <span data-ttu-id="75f7a-130">O ACR recém-adicionado será exibido na listagem tabular de ACRs.</span><span class="sxs-lookup"><span data-stu-id="75f7a-130">The newly added ACR will display in the tabular listing of ACRs.</span></span>

    ![Clique em Adicionar ACR](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a><span data-ttu-id="75f7a-132">Editar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="75f7a-132">Edit an access control record</span></span>
<span data-ttu-id="75f7a-133">Use a seção **Configuração** na folha do serviço do Gerenciador de Dispositivos do StorSimple para editar ACRs.</span><span class="sxs-lookup"><span data-stu-id="75f7a-133">You use the **Configuration** section in the StorSimple Device Manager service blade to edit ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="75f7a-134">É recomendável modificar somente os ACRs que não estão em uso no momento.</span><span class="sxs-lookup"><span data-stu-id="75f7a-134">It is recommended that you modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="75f7a-135">Para editar um ACR associado a um volume que esteja em uso no momento, primeiramente, você deverá colocar o volume no estado offline.</span><span class="sxs-lookup"><span data-stu-id="75f7a-135">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="75f7a-136">Execute as etapas a seguir para editar um ACR.</span><span class="sxs-lookup"><span data-stu-id="75f7a-136">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="75f7a-137">Para editar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="75f7a-137">To edit an access control record</span></span>
1.  <span data-ttu-id="75f7a-138">Acesse seu serviço do Gerenciador de Dispositivos do StorSimple, clique duas vezes no nome do serviço e, na seção **Configuração**, clique em **Registros de controle de acesso**.</span><span class="sxs-lookup"><span data-stu-id="75f7a-138">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![Acessar os registro de controle de acesso](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="75f7a-140">Na listagem tabular dos registros de controle de acesso, clique e selecione o ACR que você deseja modificar.</span><span class="sxs-lookup"><span data-stu-id="75f7a-140">In the tabular listing of the access control records, click and select the ACR that you wish to modify.</span></span>

    ![Editar os registros de controle de acesso](./media/storsimple-8000-manage-acrs/editacr1.png)

3. <span data-ttu-id="75f7a-142">Na folha **Editar registro de controle de acesso**, forneça um IQN diferente que corresponde a outro host.</span><span class="sxs-lookup"><span data-stu-id="75f7a-142">In the **Edit access control record** blade, provide a different IQN corresponding to another host.</span></span>

    ![Editar os registros de controle de acesso](./media/storsimple-8000-manage-acrs/editacr2.png)

4. <span data-ttu-id="75f7a-144">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="75f7a-144">Click **Save**.</span></span> <span data-ttu-id="75f7a-145">Quando solicitado a confirmar, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="75f7a-145">When prompted for confirmation, click **Yes**.</span></span> 

    ![Editar os registros de controle de acesso](./media/storsimple-8000-manage-acrs/editacr3.png)

5. <span data-ttu-id="75f7a-147">Você será notificado quando o ACR for atualizado.</span><span class="sxs-lookup"><span data-stu-id="75f7a-147">You are notified when the ACR is updated.</span></span> <span data-ttu-id="75f7a-148">A listagem tabular também é atualizada para refletir as alterações.</span><span class="sxs-lookup"><span data-stu-id="75f7a-148">The tabular listing also updates to reflect the change.</span></span>

   
## <a name="delete-an-access-control-record"></a><span data-ttu-id="75f7a-149">Excluir um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="75f7a-149">Delete an access control record</span></span>
<span data-ttu-id="75f7a-150">Use a seção **Configuração** na folha do serviço do Gerenciador de Dispositivos do StorSimple para excluir ACRs.</span><span class="sxs-lookup"><span data-stu-id="75f7a-150">You use the **Configuration** section in the StorSimple Device Manager service blade to delete ACRs.</span></span>

> [!NOTE]
> <span data-ttu-id="75f7a-151">Você pode excluir somente os ACRs que não estejam em uso no momento.</span><span class="sxs-lookup"><span data-stu-id="75f7a-151">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="75f7a-152">Para excluir um ACR associado a um volume que esteja em uso no momento, primeiramente, você deverá colocar o volume no estado offline.</span><span class="sxs-lookup"><span data-stu-id="75f7a-152">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>

<span data-ttu-id="75f7a-153">Execute as etapas a seguir para excluir um registro de controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="75f7a-153">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="75f7a-154">Para excluir um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="75f7a-154">To delete an access control record</span></span>
1.  <span data-ttu-id="75f7a-155">Acesse seu serviço do Gerenciador de Dispositivos do StorSimple, clique duas vezes no nome do serviço e, na seção **Configuração**, clique em **Registros de controle de acesso**.</span><span class="sxs-lookup"><span data-stu-id="75f7a-155">Go to your StorSimple Device Manager service, double-click the service name, and then within the **Configuration** section, click **Access control records**.</span></span>

    ![Acessar os registro de controle de acesso](./media/storsimple-8000-manage-acrs/createacr1.png)

2. <span data-ttu-id="75f7a-157">Na listagem tabular dos registros de controle de acesso, clique e selecione o ACR que você deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="75f7a-157">In the tabular listing of the access control records, click and select the ACR that you wish to delete.</span></span>

    ![Acessar os registro de controle de acesso](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. <span data-ttu-id="75f7a-159">Clique com o botão direito do mouse para invocar o menu de contexto e selecione **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="75f7a-159">Right-click to invoke the context menu and select **Delete**.</span></span>

    ![Acessar os registro de controle de acesso](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. <span data-ttu-id="75f7a-161">Quando sua confirmação for solicitada, leia as informações e clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="75f7a-161">When prompted for confirmation, review the information and then click **Delete**.</span></span>

    ![Acessar os registro de controle de acesso](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. <span data-ttu-id="75f7a-163">Você será notificado quando a exclusão for concluída.</span><span class="sxs-lookup"><span data-stu-id="75f7a-163">You are notified when the deletion completes.</span></span> <span data-ttu-id="75f7a-164">A listagem de tabela é atualizada para refletir a exclusão.</span><span class="sxs-lookup"><span data-stu-id="75f7a-164">The tabular listing is updated to reflect the deletion.</span></span>

    ![Acessar os registro de controle de acesso](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a><span data-ttu-id="75f7a-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="75f7a-166">Next steps</span></span>
* <span data-ttu-id="75f7a-167">Saiba mais sobre [como gerenciar volumes do StorSimple](storsimple-8000-manage-volumes-u2.md).</span><span class="sxs-lookup"><span data-stu-id="75f7a-167">Learn more about [managing StorSimple volumes](storsimple-8000-manage-volumes-u2.md).</span></span>
* <span data-ttu-id="75f7a-168">Saiba mais sobre o [uso do serviço StorSimple Manager para administrar seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="75f7a-168">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

