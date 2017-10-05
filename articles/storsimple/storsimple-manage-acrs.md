---
title: Gerenciar registros de controle de acesso no StorSimple | Microsoft Docs
description: Descreve como usar os ACRs (registros de controle de acesso) para determinar quais hosts podem se conectar a um volume no dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a87624b5706c1d9b8c2b9926e5580996a89ce984
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-storsimple-manager-service-to-manage-access-control-records"></a><span data-ttu-id="48d3e-103">Usar o serviço StorSimple Manager para gerenciar registros de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="48d3e-103">Use the StorSimple Manager service to manage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="48d3e-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="48d3e-104">Overview</span></span>
<span data-ttu-id="48d3e-105">Os ACRs (registros de controle de acesso) permitem especificar quais hosts podem se conectar a um volume no dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="48d3e-105">Access control records (ACRs) allow you to specify which hosts can connect to a volume on the StorSimple device.</span></span> <span data-ttu-id="48d3e-106">Os ACRs são definidos para um volume específico e contêm os IQNs (Nomes Qualificados iSCSI) dos hosts.</span><span class="sxs-lookup"><span data-stu-id="48d3e-106">ACRs are set to a specific volume and contain the iSCSI Qualified Names (IQNs) of the hosts.</span></span> <span data-ttu-id="48d3e-107">Quando um host tenta se conectar a um volume, o dispositivo verifica o nome do IQN no ACR associado a esse volume e, se houver correspondência, a conexão será estabelecida.</span><span class="sxs-lookup"><span data-stu-id="48d3e-107">When a host tries to connect to a volume, the device checks the ACR associated with that volume for the IQN name and if there is a match, then the connection is established.</span></span> <span data-ttu-id="48d3e-108">A seção de registros do controle de acesso na página **Configurar** exibe todos os registros de controle de acesso com o IQN correspondente dos hosts.</span><span class="sxs-lookup"><span data-stu-id="48d3e-108">The access control records section on the **Configure** page displays all the access control records with the corresponding IQNs of the hosts.</span></span>

<span data-ttu-id="48d3e-109">Este tutorial explica as seguintes tarefas comuns relacionadas ao ACR:</span><span class="sxs-lookup"><span data-stu-id="48d3e-109">This tutorial explains the following common ACR-related tasks:</span></span>

* <span data-ttu-id="48d3e-110">Adicionar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="48d3e-110">Add an access control record</span></span> 
* <span data-ttu-id="48d3e-111">Editar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="48d3e-111">Edit an access control record</span></span> 
* <span data-ttu-id="48d3e-112">Excluir um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="48d3e-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="48d3e-113">Ao atribuir um ACR a um volume, lembre-se que o volume não é acessado simultaneamente por mais de um host não clusterizado porque isso poderia corromper o volume.</span><span class="sxs-lookup"><span data-stu-id="48d3e-113">When assigning an ACR to a volume, take care that the volume is not concurrently accessed by more than one non-clustered host because this could corrupt the volume.</span></span> 
> * <span data-ttu-id="48d3e-114">Ao excluir um ACR de um volume, certifique-se de que o host correspondente não esteja acessando o volume porque a exclusão poderia resultar em uma interrupção de leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="48d3e-114">When deleting an ACR from a volume, make sure that the corresponding host is not accessing the volume because the deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="48d3e-115">Adicionar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="48d3e-115">Add an access control record</span></span>
<span data-ttu-id="48d3e-116">Use a página **Configurar** do serviço StorSimple Manager para adicionar ACRs.</span><span class="sxs-lookup"><span data-stu-id="48d3e-116">You use the StorSimple Manager service **Configure** page to add ACRs.</span></span> <span data-ttu-id="48d3e-117">Normalmente, você associará um ACR a um volume.</span><span class="sxs-lookup"><span data-stu-id="48d3e-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="48d3e-118">Execute as etapas a seguir para adicionar um ACR.</span><span class="sxs-lookup"><span data-stu-id="48d3e-118">Perform the following steps to add an ACR.</span></span>

#### <a name="to-add-an-access-control-record"></a><span data-ttu-id="48d3e-119">Para adicionar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="48d3e-119">To add an access control record</span></span>
1. <span data-ttu-id="48d3e-120">Na página de aterrissagem do serviço, selecione o seu serviço, clique duas vezes no nome do serviço e clique na guia **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="48d3e-120">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="48d3e-121">Na listagem tabular em **Registros de controle de acesso**, forneça um **Nome** para seu ACR.</span><span class="sxs-lookup"><span data-stu-id="48d3e-121">In the tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="48d3e-122">Forneça o nome IQN do host do Windows em **Nome do Iniciador iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="48d3e-122">Provide the IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="48d3e-123">Para obter o IQN do host do Windows Server, siga este procedimento:</span><span class="sxs-lookup"><span data-stu-id="48d3e-123">To get the IQN of your Windows Server host, do the following:</span></span>
   
   * <span data-ttu-id="48d3e-124">Inicie o iniciador Microsoft iSCSI no host do Windows.</span><span class="sxs-lookup"><span data-stu-id="48d3e-124">Start the Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="48d3e-125">Na janela **Propriedades do Iniciador iSCSI**, na guia **Configuração** selecione e copie a cadeia de caracteres do campo **Nome do Iniciador**.</span><span class="sxs-lookup"><span data-stu-id="48d3e-125">In the **iSCSI Initiator Properties** window, on the **Configuration** tab, select and copy the string from the **Initiator Name** field.</span></span>
   * <span data-ttu-id="48d3e-126">Cole essa cadeia de caracteres no campo **Nome do Iniciador iSCSI** na tabela de ACRs no Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="48d3e-126">Paste this string in the **iSCSI Initiator Name** field on the ACRs table in the Azure classic portal.</span></span>
4. <span data-ttu-id="48d3e-127">Clique em **Salvar** para salvar o ACR recentemente criado.</span><span class="sxs-lookup"><span data-stu-id="48d3e-127">Click **Save** to save the newly created ACR.</span></span> <span data-ttu-id="48d3e-128">A listagem de tabela será atualizada para refletir essa adição.</span><span class="sxs-lookup"><span data-stu-id="48d3e-128">The tabular listing will be updated to reflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="48d3e-129">Editar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="48d3e-129">Edit an access control record</span></span>
<span data-ttu-id="48d3e-130">Use a página **Configurar** no Portal clássico do Azure para editar ACRs.</span><span class="sxs-lookup"><span data-stu-id="48d3e-130">You use the **Configure** page in the Azure classic portal to edit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="48d3e-131">Você pode modificar somente os ACRs que não estejam em uso no momento.</span><span class="sxs-lookup"><span data-stu-id="48d3e-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="48d3e-132">Para editar um ACR associado a um volume que esteja em uso no momento, primeiramente, você deverá colocar o volume no estado offline.</span><span class="sxs-lookup"><span data-stu-id="48d3e-132">To edit an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="48d3e-133">Execute as etapas a seguir para editar um ACR.</span><span class="sxs-lookup"><span data-stu-id="48d3e-133">Perform the following steps to edit an ACR.</span></span>

#### <a name="to-edit-an-access-control-record"></a><span data-ttu-id="48d3e-134">Para editar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="48d3e-134">To edit an access control record</span></span>
1. <span data-ttu-id="48d3e-135">Na página de aterrissagem do serviço, selecione o seu serviço, clique duas vezes no nome do serviço e clique na guia **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="48d3e-135">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="48d3e-136">Na listagem de tabela dos registros de controle de acesso, passe o mouse sobre o ACR que deseja modificar.</span><span class="sxs-lookup"><span data-stu-id="48d3e-136">In the tabular listing of the access control records, hover over the ACR that you wish to modify.</span></span>
3. <span data-ttu-id="48d3e-137">Forneça um novo nome e/ou IQN para o ACR.</span><span class="sxs-lookup"><span data-stu-id="48d3e-137">Supply a new name and/or IQN for the ACR.</span></span>
4. <span data-ttu-id="48d3e-138">Clique em **Salvar** para salvar o ACR modificado.</span><span class="sxs-lookup"><span data-stu-id="48d3e-138">Click **Save** to save the modified ACR.</span></span> <span data-ttu-id="48d3e-139">A listagem de tabela será atualizada para refletir essa alteração.</span><span class="sxs-lookup"><span data-stu-id="48d3e-139">The tabular listing will be updated to reflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="48d3e-140">Excluir um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="48d3e-140">Delete an access control record</span></span>
<span data-ttu-id="48d3e-141">Use a página **Configurar** no Portal clássico do Azure para excluir ACRs.</span><span class="sxs-lookup"><span data-stu-id="48d3e-141">You use the **Configure** page in the Azure classic portal to delete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="48d3e-142">Você pode excluir somente os ACRs que não estejam em uso no momento.</span><span class="sxs-lookup"><span data-stu-id="48d3e-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="48d3e-143">Para excluir um ACR associado a um volume que esteja em uso no momento, primeiramente, você deverá colocar o volume no estado offline.</span><span class="sxs-lookup"><span data-stu-id="48d3e-143">To delete an ACR associated with a volume that is currently in use, you must first take the volume offline.</span></span>
> 
> 

<span data-ttu-id="48d3e-144">Execute as etapas a seguir para excluir um registro de controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="48d3e-144">Perform the following steps to delete an access control record.</span></span>

#### <a name="to-delete-an-access-control-record"></a><span data-ttu-id="48d3e-145">Para excluir um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="48d3e-145">To delete an access control record</span></span>
1. <span data-ttu-id="48d3e-146">Na página de aterrissagem do serviço, selecione o seu serviço, clique duas vezes no nome do serviço e clique na guia **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="48d3e-146">On the service landing page, select your service, double-click the service name, and then click the **Configure** tab.</span></span>
2. <span data-ttu-id="48d3e-147">Na listagem de tabela dos ACRs (registros de controle de acesso), passe o mouse sobre o ACR que deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="48d3e-147">In the tabular listing of the access control records (ACRs), hover over the ACR that you wish to delete.</span></span>
3. <span data-ttu-id="48d3e-148">Um ícone de exclusão (**x**) será exibido na coluna mais à direita do ACR selecionado.</span><span class="sxs-lookup"><span data-stu-id="48d3e-148">A delete icon (**x**) will appear in the extreme right column for the ACR that you select.</span></span> <span data-ttu-id="48d3e-149">Clique no ícone **x** para excluir o ACR.</span><span class="sxs-lookup"><span data-stu-id="48d3e-149">Click the **x** icon to delete the ACR.</span></span>
4. <span data-ttu-id="48d3e-150">Quando a confirmação é solicitada, clique em **Sim** para continuar com a exclusão.</span><span class="sxs-lookup"><span data-stu-id="48d3e-150">When prompted for confirmation, click **YES** to continue with the deletion.</span></span> <span data-ttu-id="48d3e-151">A listagem de tabela será atualizada para refletir a exclusão.</span><span class="sxs-lookup"><span data-stu-id="48d3e-151">The tabular listing will be updated to reflect the deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="48d3e-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="48d3e-152">Next steps</span></span>
* <span data-ttu-id="48d3e-153">Saiba mais sobre [como gerenciar volumes do StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="48d3e-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="48d3e-154">Saiba mais sobre o [uso do serviço StorSimple Manager para administrar seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="48d3e-154">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

