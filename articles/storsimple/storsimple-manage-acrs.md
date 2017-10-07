---
title: registros de controle de acesso aaaManage em StorSimple | Microsoft Docs
description: Descreve como os registros de controle de acesso de toouse toodetermine (ACRs) quais hosts podem se conectar a tooa volume no dispositivo do StorSimple hello.
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
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a><span data-ttu-id="1a4d2-103">Use os registros de controle de acesso do hello StorSimple Manager serviço toomanage</span><span class="sxs-lookup"><span data-stu-id="1a4d2-103">Use hello StorSimple Manager service toomanage access control records</span></span>
## <a name="overview"></a><span data-ttu-id="1a4d2-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="1a4d2-104">Overview</span></span>
<span data-ttu-id="1a4d2-105">Registros de controle de acesso (ACRs) permitem que você toospecify quais hosts podem se conectar a tooa volume no dispositivo do StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-105">Access control records (ACRs) allow you toospecify which hosts can connect tooa volume on hello StorSimple device.</span></span> <span data-ttu-id="1a4d2-106">ACRs são definidos volume específico tooa e conter Olá iSCSI nomes qualificados (IQNs) de hosts de saudação.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-106">ACRs are set tooa specific volume and contain hello iSCSI Qualified Names (IQNs) of hello hosts.</span></span> <span data-ttu-id="1a4d2-107">Quando um host tenta tooconnect tooa volume, o dispositivo Olá verifica Olá que ACR associado a esse volume do nome IQN do hello e se houver uma correspondência, hello conexão é estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-107">When a host tries tooconnect tooa volume, hello device checks hello ACR associated with that volume for hello IQN name and if there is a match, then hello connection is established.</span></span> <span data-ttu-id="1a4d2-108">registros de controle de acesso de saudação seção Olá **configurar** página exibe todos os registros de controle de acesso de saudação com hello correspondentes IQNs dos hosts de saudação.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-108">hello access control records section on hello **Configure** page displays all hello access control records with hello corresponding IQNs of hello hosts.</span></span>

<span data-ttu-id="1a4d2-109">Este tutorial explica Olá tarefas comuns relacionadas a ACR a seguir:</span><span class="sxs-lookup"><span data-stu-id="1a4d2-109">This tutorial explains hello following common ACR-related tasks:</span></span>

* <span data-ttu-id="1a4d2-110">Adicionar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="1a4d2-110">Add an access control record</span></span> 
* <span data-ttu-id="1a4d2-111">Editar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="1a4d2-111">Edit an access control record</span></span> 
* <span data-ttu-id="1a4d2-112">Excluir um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="1a4d2-112">Delete an access control record</span></span> 

> [!IMPORTANT]
> * <span data-ttu-id="1a4d2-113">Ao atribuir um volume de tooa ACR, lembre-se que Olá volume não é acessado simultaneamente por mais de um host não clusterizado porque isso pode corromper o volume de saudação.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-113">When assigning an ACR tooa volume, take care that hello volume is not concurrently accessed by more than one non-clustered host because this could corrupt hello volume.</span></span> 
> * <span data-ttu-id="1a4d2-114">Ao excluir um ACR do volume, certifique-se de que host Olá correspondente não está acessando o volume Olá porque Olá exclusão pode levar a uma interrupção de leitura / gravação.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-114">When deleting an ACR from a volume, make sure that hello corresponding host is not accessing hello volume because hello deletion could result in a read-write disruption.</span></span>
> 
> 

## <a name="add-an-access-control-record"></a><span data-ttu-id="1a4d2-115">Adicionar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="1a4d2-115">Add an access control record</span></span>
<span data-ttu-id="1a4d2-116">Usar o serviço StorSimple Manager Olá **configurar** página ACRs tooadd.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-116">You use hello StorSimple Manager service **Configure** page tooadd ACRs.</span></span> <span data-ttu-id="1a4d2-117">Normalmente, você associará um ACR a um volume.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-117">Typically, you will associate one ACR with one volume.</span></span>

<span data-ttu-id="1a4d2-118">Execute Olá etapas tooadd um ACR a seguir.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-118">Perform hello following steps tooadd an ACR.</span></span>

#### <a name="tooadd-an-access-control-record"></a><span data-ttu-id="1a4d2-119">tooadd um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="1a4d2-119">tooadd an access control record</span></span>
1. <span data-ttu-id="1a4d2-120">Na página de aterrissagem do serviço hello, selecione o seu serviço, clique duas vezes no nome do serviço hello e clique em Olá **configurar** guia.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-120">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="1a4d2-121">Em Olá tabela listando em **registros de controle de acesso**, forneça um **nome** para seu ACR.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-121">In hello tabular listing under **Access control records**, supply a **Name** for your ACR.</span></span>
3. <span data-ttu-id="1a4d2-122">Forneça o nome IQN de saudação do seu host do Windows em **nome do iniciador iSCSI**.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-122">Provide hello IQN name of your Windows host under **iSCSI Initiator Name**.</span></span> <span data-ttu-id="1a4d2-123">Olá tooget IQN do host do Windows Server, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="1a4d2-123">tooget hello IQN of your Windows Server host, do hello following:</span></span>
   
   * <span data-ttu-id="1a4d2-124">Inicie o iniciador iSCSI da Microsoft hello no seu host do Windows.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-124">Start hello Microsoft iSCSI initiator on your Windows host.</span></span>
   * <span data-ttu-id="1a4d2-125">Em Olá **propriedades do iniciador iSCSI** janela Olá **configuração** , selecione e copie a cadeia de caracteres de saudação do hello **nome do iniciador** campo.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-125">In hello **iSCSI Initiator Properties** window, on hello **Configuration** tab, select and copy hello string from hello **Initiator Name** field.</span></span>
   * <span data-ttu-id="1a4d2-126">Cole essa cadeia de caracteres hello **nome do iniciador iSCSI** campo tabela ACRs Olá Olá portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-126">Paste this string in hello **iSCSI Initiator Name** field on hello ACRs table in hello Azure classic portal.</span></span>
4. <span data-ttu-id="1a4d2-127">Clique em **salvar** toosave Olá recém-criado ACR.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-127">Click **Save** toosave hello newly created ACR.</span></span> <span data-ttu-id="1a4d2-128">Olá tabela listando será atualizado tooreflect de ser essa adição.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-128">hello tabular listing will be updated tooreflect this addition.</span></span>

## <a name="edit-an-access-control-record"></a><span data-ttu-id="1a4d2-129">Editar um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="1a4d2-129">Edit an access control record</span></span>
<span data-ttu-id="1a4d2-130">Use Olá **configurar** página Olá ACRs tooedit de portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-130">You use hello **Configure** page in hello Azure classic portal tooedit ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="1a4d2-131">Você pode modificar somente os ACRs que não estejam em uso no momento.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-131">You can modify only those ACRs that are currently not in use.</span></span> <span data-ttu-id="1a4d2-132">tooedit que um ACR associado a um volume que está em uso no momento, você deve primeiro colocar Olá volume offline.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-132">tooedit an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="1a4d2-133">Execute Olá etapas tooedit um ACR a seguir.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-133">Perform hello following steps tooedit an ACR.</span></span>

#### <a name="tooedit-an-access-control-record"></a><span data-ttu-id="1a4d2-134">tooedit um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="1a4d2-134">tooedit an access control record</span></span>
1. <span data-ttu-id="1a4d2-135">Na página de aterrissagem do serviço hello, selecione o seu serviço, clique duas vezes no nome do serviço hello e clique em Olá **configurar** guia.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-135">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="1a4d2-136">Na listagem tabular de saudação de registros de controle de acesso de saudação, passe o mouse sobre Olá ACR que quiser toomodify.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-136">In hello tabular listing of hello access control records, hover over hello ACR that you wish toomodify.</span></span>
3. <span data-ttu-id="1a4d2-137">Fornece um novo nome e/ou o IQN de saudação ACR.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-137">Supply a new name and/or IQN for hello ACR.</span></span>
4. <span data-ttu-id="1a4d2-138">Clique em **salvar** toosave Olá modificar ACR.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-138">Click **Save** toosave hello modified ACR.</span></span> <span data-ttu-id="1a4d2-139">Olá tabela listando será atualizado tooreflect de ser essa alteração.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-139">hello tabular listing will be updated tooreflect this change.</span></span>

## <a name="delete-an-access-control-record"></a><span data-ttu-id="1a4d2-140">Excluir um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="1a4d2-140">Delete an access control record</span></span>
<span data-ttu-id="1a4d2-141">Use Olá **configurar** página Olá ACRs toodelete de portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-141">You use hello **Configure** page in hello Azure classic portal toodelete ACRs.</span></span> 

> [!NOTE]
> <span data-ttu-id="1a4d2-142">Você pode excluir somente os ACRs que não estejam em uso no momento.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-142">You can delete only those ACRs that are currently not in use.</span></span> <span data-ttu-id="1a4d2-143">toodelete que um ACR associado a um volume que está em uso no momento, você deve primeiro colocar Olá volume offline.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-143">toodelete an ACR associated with a volume that is currently in use, you must first take hello volume offline.</span></span>
> 
> 

<span data-ttu-id="1a4d2-144">Execute Olá seguindo as etapas toodelete um registro de controle de acesso.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-144">Perform hello following steps toodelete an access control record.</span></span>

#### <a name="toodelete-an-access-control-record"></a><span data-ttu-id="1a4d2-145">toodelete um registro de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="1a4d2-145">toodelete an access control record</span></span>
1. <span data-ttu-id="1a4d2-146">Na página de aterrissagem do serviço hello, selecione o seu serviço, clique duas vezes no nome do serviço hello e clique em Olá **configurar** guia.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-146">On hello service landing page, select your service, double-click hello service name, and then click hello **Configure** tab.</span></span>
2. <span data-ttu-id="1a4d2-147">Na listagem tabular de saudação de registros de controle de acesso (ACRs) hello, passe o mouse sobre Olá ACR que quiser toodelete.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-147">In hello tabular listing of hello access control records (ACRs), hover over hello ACR that you wish toodelete.</span></span>
3. <span data-ttu-id="1a4d2-148">Um ícone de exclusão (**x**) aparecerá na coluna de direito extremo Olá para Olá ACR selecionado.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-148">A delete icon (**x**) will appear in hello extreme right column for hello ACR that you select.</span></span> <span data-ttu-id="1a4d2-149">Clique em Olá **x** Olá toodelete de ícone ACR.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-149">Click hello **x** icon toodelete hello ACR.</span></span>
4. <span data-ttu-id="1a4d2-150">Quando solicitado a confirmar, clique em **Sim** toocontinue com exclusão hello.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-150">When prompted for confirmation, click **YES** toocontinue with hello deletion.</span></span> <span data-ttu-id="1a4d2-151">listagem tabular Olá será atualizado tooreflect Olá exclusão.</span><span class="sxs-lookup"><span data-stu-id="1a4d2-151">hello tabular listing will be updated tooreflect hello deletion.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1a4d2-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1a4d2-152">Next steps</span></span>
* <span data-ttu-id="1a4d2-153">Saiba mais sobre [como gerenciar volumes do StorSimple](storsimple-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="1a4d2-153">Learn more about [managing StorSimple volumes](storsimple-manage-volumes.md).</span></span>
* <span data-ttu-id="1a4d2-154">Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="1a4d2-154">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

