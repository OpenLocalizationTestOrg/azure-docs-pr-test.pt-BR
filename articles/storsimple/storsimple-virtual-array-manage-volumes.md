---
title: volumes aaaManage na matriz Virtual StorSimple | Microsoft Docs
description: "Descreve Olá Gerenciador de dispositivos do StorSimple e explica como toouse-toomanage volumes no StorSimple Virtual Array."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a><span data-ttu-id="433ff-103">Toomanage volumes serviço Gerenciador de dispositivos de StorSimple uso Olá matriz Virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="433ff-103">Use StorSimple Device Manager service toomanage volumes on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="433ff-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="433ff-104">Overview</span></span>

<span data-ttu-id="433ff-105">Este tutorial explica como toouse Olá toocreate de serviço do Gerenciador de dispositivos do StorSimple e gerenciar volumes no StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="433ff-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="433ff-106">saudação de serviço do Gerenciador de dispositivos do StorSimple é uma extensão em Olá portal do Azure que permite que você gerencie sua solução StorSimple de uma única interface da web.</span><span class="sxs-lookup"><span data-stu-id="433ff-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="433ff-107">Em adição toomanaging compartilhamentos e volumes, você pode usar tooview de serviço do Gerenciador de dispositivos de StorSimple hello e gerenciar dispositivos, exibir alertas, exibir e gerenciar políticas de backup e o catálogo de backup hello.</span><span class="sxs-lookup"><span data-stu-id="433ff-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, and view and manage backup policies and hello backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="433ff-108">Tipos de volumes</span><span class="sxs-lookup"><span data-stu-id="433ff-108">Volume Types</span></span>

<span data-ttu-id="433ff-109">Os volumes do StorSimple podem ser:</span><span class="sxs-lookup"><span data-stu-id="433ff-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="433ff-110">**Localmente afixado**: dados nesses volumes permanece na matriz de saudação sempre e não despejar toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="433ff-110">**Locally pinned**: Data in these volumes stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="433ff-111">**Em camadas**: dados nesses volumes podem despejar toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="433ff-111">**Tiered**: Data in these volumes can spill toohello cloud.</span></span> <span data-ttu-id="433ff-112">Quando você cria um volume em camadas, aproximadamente 10% do espaço de saudação é provisionado na camada local hello e 90% do espaço de saudação é provisionado na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="433ff-112">When you create a tiered volume, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="433ff-113">Por exemplo, se você provisionar um volume de 1 TB, 100 GB reside no espaço local hello e 900 GB é usado na nuvem hello quando Olá camadas de dados.</span><span class="sxs-lookup"><span data-stu-id="433ff-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="433ff-114">Por sua vez, isso significa que se você ficar sem todo o espaço local Olá no dispositivo hello, você não pode provisionar um volume em camadas (porque Olá 10% necessário no local de saudação camada não estará disponível).</span><span class="sxs-lookup"><span data-stu-id="433ff-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered volume (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="433ff-115">Capacidade provisionada</span><span class="sxs-lookup"><span data-stu-id="433ff-115">Provisioned capacity</span></span>
<span data-ttu-id="433ff-116">Consulte toohello para máxima capacidade provisionada para cada tipo de volume a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="433ff-116">Refer toohello following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="433ff-117">**Identificador de limite**</span><span class="sxs-lookup"><span data-stu-id="433ff-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="433ff-118">**Limite**</span><span class="sxs-lookup"><span data-stu-id="433ff-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="433ff-119">Tamanho mínimo de um volume em camadas</span><span class="sxs-lookup"><span data-stu-id="433ff-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="433ff-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="433ff-120">500 GB</span></span>        |
| <span data-ttu-id="433ff-121">Tamanho máximo de um volume em camadas</span><span class="sxs-lookup"><span data-stu-id="433ff-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="433ff-122">5 TB</span><span class="sxs-lookup"><span data-stu-id="433ff-122">5 TB</span></span>          |
| <span data-ttu-id="433ff-123">Tamanho mínimo de um volume fixado localmente</span><span class="sxs-lookup"><span data-stu-id="433ff-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="433ff-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="433ff-124">50 GB</span></span>         |
| <span data-ttu-id="433ff-125">Tamanho máximo de um volume fixado localmente</span><span class="sxs-lookup"><span data-stu-id="433ff-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="433ff-126">500 GB</span><span class="sxs-lookup"><span data-stu-id="433ff-126">500 GB</span></span>        |

## <a name="hello-volumes-blade"></a><span data-ttu-id="433ff-127">folha de Volumes Olá</span><span class="sxs-lookup"><span data-stu-id="433ff-127">hello Volumes blade</span></span>
<span data-ttu-id="433ff-128">Olá **Volumes** menu na sua folha de resumo de serviço do StorSimple exibe a lista de saudação de volumes de armazenamento em uma determinada matriz de StorSimple e permite que você toomanage-los.</span><span class="sxs-lookup"><span data-stu-id="433ff-128">hello **Volumes** menu on your StorSimple service summary blade displays hello list of storage volumes on a given StorSimple array and allows you toomanage them.</span></span>

![Folha Volumes](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="433ff-130">Um volume consiste em uma série de atributos:</span><span class="sxs-lookup"><span data-stu-id="433ff-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="433ff-131">**Nome do volume** – um nome descritivo que deve ser exclusivo e ajuda a identificar o volume de saudação.</span><span class="sxs-lookup"><span data-stu-id="433ff-131">**Volume Name** – A descriptive name that must be unique and helps identify hello volume.</span></span>
* <span data-ttu-id="433ff-132">**Status** – Pode ser online ou offline.</span><span class="sxs-lookup"><span data-stu-id="433ff-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="433ff-133">Se o volume estiver offline, não é visível tooinitiators (servidores) que têm permissão de acesso toouse Olá volume.</span><span class="sxs-lookup"><span data-stu-id="433ff-133">If a volume is offline, it is not visible tooinitiators (servers) that are allowed access toouse hello volume.</span></span>
* <span data-ttu-id="433ff-134">**Tipo** – indica se o volume de saudação é **em camadas** (Olá padrão) ou **localmente afixado**.</span><span class="sxs-lookup"><span data-stu-id="433ff-134">**Type** – Indicates whether hello volume is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="433ff-135">**Capacidade** – Especifica Olá quantidade de dados usados como toohello em comparação com a quantidade total de dados que podem ser armazenados pelo iniciador da saudação (servidor).</span><span class="sxs-lookup"><span data-stu-id="433ff-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored by hello initiator (server).</span></span>
* <span data-ttu-id="433ff-136">**Backup** – no caso de Olá matriz Virtual StorSimple, todos os volumes são habilitados automaticamente para o backup.</span><span class="sxs-lookup"><span data-stu-id="433ff-136">**Backup** – In case of hello StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="433ff-137">**Conectado hosts** – Especifica os iniciadores de saudação (servidores) que têm permissão de acesso toothis volume.</span><span class="sxs-lookup"><span data-stu-id="433ff-137">**Connected hosts** – Specifies hello initiators (servers) that are allowed access toothis volume.</span></span>

![Detalhes dos volumes](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="433ff-139">Use as instruções de saudação este Olá tooperform tutorial tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="433ff-139">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="433ff-140">Adicionar um volume</span><span class="sxs-lookup"><span data-stu-id="433ff-140">Add a volume</span></span>
* <span data-ttu-id="433ff-141">Modificar um volume</span><span class="sxs-lookup"><span data-stu-id="433ff-141">Modify a volume</span></span>
* <span data-ttu-id="433ff-142">Colocar um volume offline</span><span class="sxs-lookup"><span data-stu-id="433ff-142">Take a volume offline</span></span>
* <span data-ttu-id="433ff-143">Excluir um volume</span><span class="sxs-lookup"><span data-stu-id="433ff-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="433ff-144">Adicionar um volume</span><span class="sxs-lookup"><span data-stu-id="433ff-144">Add a volume</span></span>

1. <span data-ttu-id="433ff-145">Na folha resumida do serviço do StorSimple de saudação, clique em **+ Adicionar volume** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="433ff-145">From hello StorSimple service summary blade, click **+ Add volume** from hello command bar.</span></span> <span data-ttu-id="433ff-146">Isso abre a saudação **Adicionar volume** folha.</span><span class="sxs-lookup"><span data-stu-id="433ff-146">This opens up hello **Add volume** blade.</span></span>
   
    ![Adicionar volume](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="433ff-148">Em Olá **Adicionar volume** folha, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="433ff-148">In hello **Add volume** blade, do hello following:</span></span>
   
   * <span data-ttu-id="433ff-149">Em Olá **nome do Volume** campo, digite um nome exclusivo para seu volume.</span><span class="sxs-lookup"><span data-stu-id="433ff-149">In hello **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="433ff-150">nome da saudação deve ser uma cadeia de caracteres com 3 caracteres too127.</span><span class="sxs-lookup"><span data-stu-id="433ff-150">hello name must be a string that contains 3 too127 characters.</span></span>
   * <span data-ttu-id="433ff-151">Em Olá **tipo** suspensa lista, especifique se toocreate um **em camadas** ou **localmente afixado** volume.</span><span class="sxs-lookup"><span data-stu-id="433ff-151">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="433ff-152">Para as cargas de trabalho que exigem garantias locais, latências baixas e um melhor desempenho, selecione **Volume fixado localmente**.</span><span class="sxs-lookup"><span data-stu-id="433ff-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="433ff-153">Para todos os outros dados, selecione volume **Em camadas**.</span><span class="sxs-lookup"><span data-stu-id="433ff-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="433ff-154">Em Olá **capacidade** , especifique o tamanho de saudação do volume de saudação.</span><span class="sxs-lookup"><span data-stu-id="433ff-154">In hello **Capacity** field, specify hello size of hello volume.</span></span> <span data-ttu-id="433ff-155">Um volume em camadas deve ter entre 500 GB e 5 TB e um volume fixado localmente deve ter entre 50 GB e 500 GB.</span><span class="sxs-lookup"><span data-stu-id="433ff-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="433ff-156">Clique em **conectado hosts**, selecione um acesso controle ACR (registro) correspondente toohello iniciador iSCSI que você deseja tooconnect toothis volume e, em seguida, clique em **selecione**.</span><span class="sxs-lookup"><span data-stu-id="433ff-156">Click **Connected hosts**, select an access control record (ACR) corresponding toohello iSCSI initiator that you want tooconnect toothis volume, and then click **Select**.</span></span>
3. <span data-ttu-id="433ff-157">tooadd um novo host conectado, clique em **adicionar novo**, insira um nome de host de saudação e o iSCSI IQN (nome qualificado) e depois clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="433ff-157">tooadd a new connected host, click **Add new**, enter a name for hello host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![Adicionar volume](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="433ff-159">Quando você tiver terminado de configurar o volume, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="433ff-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="433ff-160">Um volume será criado com hello especificado as configurações e você verá uma notificação de êxito na criação de Olá Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="433ff-160">A volume will be created with hello specified settings and you will see a notification on hello successful creation of hello same.</span></span> <span data-ttu-id="433ff-161">Por padrão, backup será habilitado para o volume de saudação.</span><span class="sxs-lookup"><span data-stu-id="433ff-161">By default backup will be enabled for hello volume.</span></span>
5. <span data-ttu-id="433ff-162">tooconfirm que Olá volume foi criado com êxito, vá toohello **Volumes** folha.</span><span class="sxs-lookup"><span data-stu-id="433ff-162">tooconfirm that hello volume was successfully created, go toohello **Volumes** blade.</span></span> <span data-ttu-id="433ff-163">Você deve ver o volume de saudação listado.</span><span class="sxs-lookup"><span data-stu-id="433ff-163">You should see hello volume listed.</span></span>
   
    ![Criação do volume bem-sucedida](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="433ff-165">Modificar um volume</span><span class="sxs-lookup"><span data-stu-id="433ff-165">Modify a volume</span></span>

<span data-ttu-id="433ff-166">Modifique um volume quando você precisa toochange Olá hosts que acessam o volume de saudação.</span><span class="sxs-lookup"><span data-stu-id="433ff-166">Modify a volume when you need toochange hello hosts that access hello volume.</span></span> <span data-ttu-id="433ff-167">Olá outros atributos de um volume não podem ser modificados após a criação de volume hello.</span><span class="sxs-lookup"><span data-stu-id="433ff-167">hello other attributes of a volume cannot be modified once hello volume has been created.</span></span>

#### <a name="toomodify-a-volume"></a><span data-ttu-id="433ff-168">toomodify um volume</span><span class="sxs-lookup"><span data-stu-id="433ff-168">toomodify a volume</span></span>

1. <span data-ttu-id="433ff-169">De saudação **Volumes** configuração na folha do resumida de serviço do StorSimple hello, selecione Olá array virtual no qual Olá volume desejar toomodify reside.</span><span class="sxs-lookup"><span data-stu-id="433ff-169">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toomodify resides.</span></span>
2. <span data-ttu-id="433ff-170">**Selecione** Olá volume e clique em **conectado hosts** tooview Olá host conectado no momento e modificá-lo tooa outro servidor.</span><span class="sxs-lookup"><span data-stu-id="433ff-170">**Select** hello volume and click **Connected hosts** tooview hello currently connected host and modify it tooa different server.</span></span>
   
    ![Editar volume](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="433ff-172">Salvar as alterações clicando Olá **salvar** barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="433ff-172">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="433ff-173">As configurações especificadas serão aplicadas e você verá uma notificação.</span><span class="sxs-lookup"><span data-stu-id="433ff-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="433ff-174">Colocar um volume offline</span><span class="sxs-lookup"><span data-stu-id="433ff-174">Take a volume offline</span></span>

<span data-ttu-id="433ff-175">Talvez seja necessário tootake um volume offline quando você estiver planejando toomodify-lo ou exclua-lo.</span><span class="sxs-lookup"><span data-stu-id="433ff-175">You may need tootake a volume offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="433ff-176">Quando um volume está offline, não está disponível para acesso de leitura / gravação.</span><span class="sxs-lookup"><span data-stu-id="433ff-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="433ff-177">Você precisará tootake Olá volume offline no host hello, bem como no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="433ff-177">You will need tootake hello volume offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-volume-offline"></a><span data-ttu-id="433ff-178">tootake um volume offline</span><span class="sxs-lookup"><span data-stu-id="433ff-178">tootake a volume offline</span></span>

1. <span data-ttu-id="433ff-179">Certifique-se de que o volume de saudação em questão não está em uso antes de colocá-lo offline.</span><span class="sxs-lookup"><span data-stu-id="433ff-179">Make sure that hello volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="433ff-180">Olá primeiro coloque volume offline no host de saudação.</span><span class="sxs-lookup"><span data-stu-id="433ff-180">Take hello volume offline on hello host first.</span></span> <span data-ttu-id="433ff-181">Isso eliminará qualquer risco potencial de corrupção de dados no volume de saudação.</span><span class="sxs-lookup"><span data-stu-id="433ff-181">This eliminates any potential risk of data corruption on hello volume.</span></span> <span data-ttu-id="433ff-182">Para etapas específicas, consulte as instruções de toohello para seu sistema operacional do host.</span><span class="sxs-lookup"><span data-stu-id="433ff-182">For specific steps, refer toohello instructions for your host operating system.</span></span>
3. <span data-ttu-id="433ff-183">Depois de volume Olá Olá host estiver offline, coloque o volume de saudação na matriz de saudação offline executando Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="433ff-183">After hello volume on hello host is offline, take hello volume on hello array  offline by performing hello following steps:</span></span>
   
   * <span data-ttu-id="433ff-184">De saudação **Volumes** configuração na folha do resumida de serviço do StorSimple hello, selecione Olá array virtual no qual Olá volume desejar tootake offline reside.</span><span class="sxs-lookup"><span data-stu-id="433ff-184">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you tootake offline resides.</span></span>
   * <span data-ttu-id="433ff-185">**Selecione** Olá volume e clique em **...**  (como alternativa, clique na linha) e no menu de contexto hello, selecione **colocar offline**.</span><span class="sxs-lookup"><span data-stu-id="433ff-185">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![Volume offline](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="433ff-187">Revise as informações de Olá Olá **colocar offline** folha e confirmar a aceitação da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="433ff-187">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="433ff-188">Clique em **colocar offline** tootake volume de saudação offline.</span><span class="sxs-lookup"><span data-stu-id="433ff-188">Click **Take offline** tootake hello volume offline.</span></span> <span data-ttu-id="433ff-189">Você verá uma notificação de operação de saudação em andamento.</span><span class="sxs-lookup"><span data-stu-id="433ff-189">You will see a notification of hello operation in progress.</span></span>
   * <span data-ttu-id="433ff-190">tooconfirm volume Olá com êxito foi colocado offline, vá toohello **Volumes** folha.</span><span class="sxs-lookup"><span data-stu-id="433ff-190">tooconfirm that hello volume was successfully taken offline, go toohello **Volumes** blade.</span></span> <span data-ttu-id="433ff-191">Você deve ver o status de saudação do volume de saudação como offline.</span><span class="sxs-lookup"><span data-stu-id="433ff-191">You should see hello status of hello volume as offline.</span></span>
     
       ![Confirmação de volume offline](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="433ff-193">Excluir um volume</span><span class="sxs-lookup"><span data-stu-id="433ff-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="433ff-194">Você pode excluir um volume apenas se ele estiver offline.</span><span class="sxs-lookup"><span data-stu-id="433ff-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="433ff-195">Concluir Olá etapas toodelete um volume a seguir.</span><span class="sxs-lookup"><span data-stu-id="433ff-195">Complete hello following steps toodelete a volume.</span></span>

#### <a name="toodelete-a-volume"></a><span data-ttu-id="433ff-196">toodelete um volume</span><span class="sxs-lookup"><span data-stu-id="433ff-196">toodelete a volume</span></span>

1. <span data-ttu-id="433ff-197">De saudação **Volumes** configuração na folha do resumida de serviço do StorSimple hello, selecione Olá array virtual no qual Olá volume desejar toodelete reside.</span><span class="sxs-lookup"><span data-stu-id="433ff-197">From hello **Volumes** setting on hello StorSimple service summary blade, select hello virtual array on which hello volume you wish you toodelete resides.</span></span>
2. <span data-ttu-id="433ff-198">**Selecione** Olá volume e clique em **...**  (como alternativa, clique na linha) e no menu de contexto hello, selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="433ff-198">**Select** hello volume and click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![Excluir volume](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="433ff-200">Verificar o status de saudação do volume Olá deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="433ff-200">Check hello status of hello volume you want toodelete.</span></span> <span data-ttu-id="433ff-201">Se o volume Olá toodelete desejado não estiver offline, etapas-lo offline Olá primeiro, o seguinte [colocar um volume offline](#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="433ff-201">If hello volume you want toodelete is not offline, take it offline first, following hello steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="433ff-202">Quando for solicitada a confirmação no hello **excluir** folha, aceite a confirmação de saudação e clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="433ff-202">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="433ff-203">volume de saudação será excluída e Olá **Volumes** folha mostrará a lista de saudação atualizada de volumes em matriz virtual hello.</span><span class="sxs-lookup"><span data-stu-id="433ff-203">hello volume will now be deleted and hello **Volumes** blade will show hello updated list of volumes within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="433ff-204">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="433ff-204">Next steps</span></span>

<span data-ttu-id="433ff-205">Saiba como muito[clonar um volume StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="433ff-205">Learn how too[clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

