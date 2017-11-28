---
title: compartilhamentos de matriz Virtual StorSimple aaaManage | Microsoft Docs
description: "Descreve Olá Gerenciador de dispositivos do StorSimple e explica como toouse-toomanage compartilhamentos no StorSimple Virtual Array."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a><span data-ttu-id="07af7-103">Usar compartilhamentos de toomanage de serviço de Gerenciador de dispositivos de StorSimple Olá em Olá matriz Virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="07af7-103">Use hello StorSimple Device Manager service toomanage shares on hello StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="07af7-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="07af7-104">Overview</span></span>

<span data-ttu-id="07af7-105">Este tutorial explica como toouse Olá toocreate de serviço do Gerenciador de dispositivos do StorSimple e gerenciar os compartilhamentos no StorSimple Virtual Array.</span><span class="sxs-lookup"><span data-stu-id="07af7-105">This tutorial explains how toouse hello StorSimple Device Manager service toocreate and manage shares on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="07af7-106">saudação de serviço do Gerenciador de dispositivos do StorSimple é uma extensão em Olá portal do Azure que permite que você gerencie sua solução StorSimple de uma única interface da web.</span><span class="sxs-lookup"><span data-stu-id="07af7-106">hello StorSimple Device Manager service is an extension in hello Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="07af7-107">Em adição toomanaging compartilhamentos e volumes, você pode usar tooview de serviço do Gerenciador de dispositivos de StorSimple hello e gerenciar dispositivos, exibir alertas, gerenciar políticas de backup e gerenciar o catálogo de backup hello.</span><span class="sxs-lookup"><span data-stu-id="07af7-107">In addition toomanaging shares and volumes, you can use hello StorSimple Device Manager service tooview and manage devices, view alerts, manage backup policies, and manage hello backup catalog.</span></span>

## <a name="share-types"></a><span data-ttu-id="07af7-108">Tipos de compartilhamento</span><span class="sxs-lookup"><span data-stu-id="07af7-108">Share Types</span></span>

<span data-ttu-id="07af7-109">Os compartilhamentos do StorSimple podem ser:</span><span class="sxs-lookup"><span data-stu-id="07af7-109">StorSimple shares can be:</span></span>

* <span data-ttu-id="07af7-110">**Localmente afixado**: dados nesses compartilhamentos permanece na matriz de saudação sempre e não despejar toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="07af7-110">**Locally pinned**: Data in these shares stays on hello array at all times and does not spill toohello cloud.</span></span>
* <span data-ttu-id="07af7-111">**Em camadas**: dados nesses compartilhamentos podem despejar toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="07af7-111">**Tiered**: Data in these shares can spill toohello cloud.</span></span> <span data-ttu-id="07af7-112">Quando você cria um compartilhamento em camadas, aproximadamente 10% do espaço de saudação é provisionado na camada local hello e 90% do espaço de saudação é provisionado na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="07af7-112">When you create a tiered share, approximately 10 % of hello space is provisioned on hello local tier and 90 % of hello space is provisioned in hello cloud.</span></span> <span data-ttu-id="07af7-113">Por exemplo, se você provisionou um compartilhamento de 1 TB, 100 GB reside no espaço local hello e 900 GB é usado na nuvem hello quando Olá camadas de dados.</span><span class="sxs-lookup"><span data-stu-id="07af7-113">For example, if you provisioned a 1 TB share, 100 GB would reside in hello local space and 900 GB would be used in hello cloud when hello data tiers.</span></span> <span data-ttu-id="07af7-114">Por sua vez, isso significa que se você ficar sem todo o espaço local Olá no dispositivo hello, você não pode provisionar um compartilhamento em camadas (porque Olá 10% necessário no local de saudação camada não estará disponível).</span><span class="sxs-lookup"><span data-stu-id="07af7-114">This in turn implies that if you run out of all hello local space on hello device, you cannot provision a tiered share (because hello 10 % required on hello local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="07af7-115">Capacidade provisionada</span><span class="sxs-lookup"><span data-stu-id="07af7-115">Provisioned capacity</span></span>

<span data-ttu-id="07af7-116">Consulte toohello para máxima capacidade provisionada para cada tipo de compartilhamento a tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="07af7-116">Refer toohello following table for maximum provisioned capacity for each share type.</span></span>

| <span data-ttu-id="07af7-117">**Identificador de limite**</span><span class="sxs-lookup"><span data-stu-id="07af7-117">**Limit identifier**</span></span> | <span data-ttu-id="07af7-118">**Limite**</span><span class="sxs-lookup"><span data-stu-id="07af7-118">**Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="07af7-119">Tamanho mínimo de um compartilhamento em camadas</span><span class="sxs-lookup"><span data-stu-id="07af7-119">Minimum size of a tiered share</span></span> |<span data-ttu-id="07af7-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="07af7-120">500 GB</span></span> |
| <span data-ttu-id="07af7-121">Tamanho máximo de um compartilhamento em camadas</span><span class="sxs-lookup"><span data-stu-id="07af7-121">Maximum size of a tiered share</span></span> |<span data-ttu-id="07af7-122">20 TB</span><span class="sxs-lookup"><span data-stu-id="07af7-122">20 TB</span></span> |
| <span data-ttu-id="07af7-123">Tamanho mínimo de um compartilhamento fixado localmente</span><span class="sxs-lookup"><span data-stu-id="07af7-123">Minimum size of a locally pinned share</span></span> |<span data-ttu-id="07af7-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="07af7-124">50 GB</span></span> |
| <span data-ttu-id="07af7-125">Tamanho máximo de um compartilhamento fixado localmente</span><span class="sxs-lookup"><span data-stu-id="07af7-125">Maximum size of a locally pinned share</span></span> |<span data-ttu-id="07af7-126">2 TB</span><span class="sxs-lookup"><span data-stu-id="07af7-126">2 TB</span></span> |

## <a name="hello-shares-blade"></a><span data-ttu-id="07af7-127">folha de compartilhamentos Olá</span><span class="sxs-lookup"><span data-stu-id="07af7-127">hello Shares blade</span></span>

<span data-ttu-id="07af7-128">Olá **compartilhamentos** menu na sua folha de resumo de serviço do StorSimple exibe a lista de saudação de compartilhamentos de armazenamento em uma determinada matriz de StorSimple e permite que você toomanage-los.</span><span class="sxs-lookup"><span data-stu-id="07af7-128">hello **Shares** menu on your StorSimple service summary blade displays hello list of storage shares on a given StorSimple array and allows you toomanage them.</span></span>

![Folha Compartilhamentos](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

<span data-ttu-id="07af7-130">Um compartilhamento consiste em uma série de atributos:</span><span class="sxs-lookup"><span data-stu-id="07af7-130">A share consists of a series of attributes:</span></span>

* <span data-ttu-id="07af7-131">**Nome do compartilhamento** – um nome descritivo que deve ser exclusivo e ajuda a identificar o compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="07af7-131">**Share Name** – A descriptive name that must be unique and helps identify hello share.</span></span>
* <span data-ttu-id="07af7-132">**Status** – Pode ser online ou offline.</span><span class="sxs-lookup"><span data-stu-id="07af7-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="07af7-133">Se um compartilhamento estiver offline, os usuários de compartilhamento de saudação não será capaz de tooaccess-lo.</span><span class="sxs-lookup"><span data-stu-id="07af7-133">If a share is offline, users of hello share will not be able tooaccess it.</span></span>
* <span data-ttu-id="07af7-134">**Tipo** – indica se o compartilhamento de saudação é **em camadas** (Olá padrão) ou **localmente afixado**.</span><span class="sxs-lookup"><span data-stu-id="07af7-134">**Type** – Indicates whether hello share is **Tiered** (hello default) or **Locally pinned**.</span></span>
* <span data-ttu-id="07af7-135">**Capacidade** – Especifica Olá quantidade de dados usados como toohello em comparação com a quantidade total de dados que podem ser armazenados no compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="07af7-135">**Capacity** – specifies hello amount of data used as compared toohello total amount of data that can be stored on hello share.</span></span>
* <span data-ttu-id="07af7-136">**Descrição** – uma configuração opcional que ajudam a descrever compartilhamento hello.</span><span class="sxs-lookup"><span data-stu-id="07af7-136">**Description** – An optional setting that helps describe hello share.</span></span>
* <span data-ttu-id="07af7-137">**Permissões** -compartilhamento toohello de permissões de NTFS de saudação que pode ser gerenciado pelo Windows Explorer.</span><span class="sxs-lookup"><span data-stu-id="07af7-137">**Permissions** - hello NTFS permissions toohello share that can be managed through Windows Explorer.</span></span>
* <span data-ttu-id="07af7-138">**Backup** – no caso de Olá matriz Virtual StorSimple, todos os compartilhamentos são habilitados automaticamente para o backup.</span><span class="sxs-lookup"><span data-stu-id="07af7-138">**Backup** – In case of hello StorSimple Virtual Array, all shares are automatically enabled for backup.</span></span>

![Detalhes de compartilhamentos](./media/storsimple-virtual-array-manage-shares/share-details.png)

<span data-ttu-id="07af7-140">Use as instruções de saudação este Olá tooperform tutorial tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="07af7-140">Use hello instructions in this tutorial tooperform hello following tasks:</span></span>

* <span data-ttu-id="07af7-141">Adicionar um compartilhamento</span><span class="sxs-lookup"><span data-stu-id="07af7-141">Add a share</span></span>
* <span data-ttu-id="07af7-142">Modificar um compartilhamento</span><span class="sxs-lookup"><span data-stu-id="07af7-142">Modify a share</span></span>
* <span data-ttu-id="07af7-143">Colocar um compartilhamento offline</span><span class="sxs-lookup"><span data-stu-id="07af7-143">Take a share offline</span></span>
* <span data-ttu-id="07af7-144">Excluir um compartilhamento</span><span class="sxs-lookup"><span data-stu-id="07af7-144">Delete a share</span></span>

## <a name="add-a-share"></a><span data-ttu-id="07af7-145">Adicionar um compartilhamento</span><span class="sxs-lookup"><span data-stu-id="07af7-145">Add a share</span></span>

1. <span data-ttu-id="07af7-146">Na folha resumida do serviço do StorSimple de saudação, clique em **+ Adicionar compartilhamento** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="07af7-146">From hello StorSimple service summary blade, click **+ Add share** from hello command bar.</span></span> <span data-ttu-id="07af7-147">Isso abre a saudação **Adicionar compartilhamento** folha.</span><span class="sxs-lookup"><span data-stu-id="07af7-147">This opens up hello **Add share** blade.</span></span>

    ![Adicionar compartilhamento](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. <span data-ttu-id="07af7-149">Em Olá **Adicionar compartilhamento** folha, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="07af7-149">In hello **Add share** blade, do hello following:</span></span>
   
    1. <span data-ttu-id="07af7-150">Em Olá **nome de compartilhamento** campo, digite um nome exclusivo para o compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="07af7-150">In hello **Share name** field, enter a unique name for your share.</span></span> <span data-ttu-id="07af7-151">nome da saudação deve ser uma cadeia de caracteres com 3 caracteres too127.</span><span class="sxs-lookup"><span data-stu-id="07af7-151">hello name must be a string that contains 3 too127 characters.</span></span>

    2. <span data-ttu-id="07af7-152">Um recurso opcional **descrição** para compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="07af7-152">An optional **Description** for hello share.</span></span> <span data-ttu-id="07af7-153">Descrição de saudação ajudará a identificar os proprietários do compartilhamento hello.</span><span class="sxs-lookup"><span data-stu-id="07af7-153">hello description will help identify hello share owners.</span></span>

    3. <span data-ttu-id="07af7-154">Em Olá **tipo** suspensa lista, especifique se toocreate um **em camadas** ou **localmente afixado** compartilhar.</span><span class="sxs-lookup"><span data-stu-id="07af7-154">In hello **Type** dropdown list, specify whether toocreate a **Tiered** or **Locally pinned** share.</span></span> <span data-ttu-id="07af7-155">Para cargas de trabalho que exigem garantias locais, latências menores e um melhor desempenho, selecione um compartilhamento **Fixado localmente** .</span><span class="sxs-lookup"><span data-stu-id="07af7-155">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned share**.</span></span> <span data-ttu-id="07af7-156">Para todos os outros dados, selecione compartilhamento **Em camadas** .</span><span class="sxs-lookup"><span data-stu-id="07af7-156">For all other data, select **Tiered** share.</span></span>

    4. <span data-ttu-id="07af7-157">Em Olá **capacidade** , especifique o tamanho de saudação do compartilhamento de saudação do.</span><span class="sxs-lookup"><span data-stu-id="07af7-157">In hello **Capacity** field, specify hello size of hello share.</span></span> <span data-ttu-id="07af7-158">Um compartilhamento em camadas deve ter entre 500 GB e 20 TB e um compartilhamento fixo local deve ter entre 50 GB e 2 GB.</span><span class="sxs-lookup"><span data-stu-id="07af7-158">A tiered share must be between 500 GB and 20 TB and a locally pinned share must be between 50 GB and 2 TB.</span></span>

    5. <span data-ttu-id="07af7-159">Em Olá **definir padrão permissões completas** campo, atribua Olá permissões toohello do usuário ou grupo Olá que acessa esse compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="07af7-159">In hello **Set default full permissions to** field, assign hello permissions toohello user, or hello group that is accessing this share.</span></span> <span data-ttu-id="07af7-160">Especificar nome de saudação do Olá Olá de usuário ou grupo no  _john@contoso.com_  formato.</span><span class="sxs-lookup"><span data-stu-id="07af7-160">Specify hello name of hello user or hello user group in _john@contoso.com_ format.</span></span> <span data-ttu-id="07af7-161">É recomendável que você use um tooaccess de privilégios de administrador do usuário grupo (em vez de um único usuário) tooallow esses compartilhamentos.</span><span class="sxs-lookup"><span data-stu-id="07af7-161">We recommend that you use a user group (instead of a single user) tooallow admin privileges tooaccess these shares.</span></span> <span data-ttu-id="07af7-162">Depois que você atribuiu permissões de saudação aqui, você pode usar Explorador de arquivos toomodify essas permissões.</span><span class="sxs-lookup"><span data-stu-id="07af7-162">After you have assigned hello permissions here, you can then use File Explorer toomodify these permissions.</span></span>
3. <span data-ttu-id="07af7-163">Quando você tiver terminado de configurar o compartilhamento, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="07af7-163">When you've finished configuring your share, click **Create**.</span></span> <span data-ttu-id="07af7-164">Será criado um compartilhamento com hello especificado as configurações e você verá uma notificação.</span><span class="sxs-lookup"><span data-stu-id="07af7-164">A share will be created with hello specified settings and you will see a notification.</span></span> <span data-ttu-id="07af7-165">Por padrão, o backup será habilitado para compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="07af7-165">By default, backup will be enabled for hello share.</span></span>
4. <span data-ttu-id="07af7-166">tooconfirm que Olá compartilhamento foi criado com êxito, vá toohello **compartilhamentos** folha.</span><span class="sxs-lookup"><span data-stu-id="07af7-166">tooconfirm that hello share was successfully created, go toohello **Shares** blade.</span></span> <span data-ttu-id="07af7-167">Você deve ver Olá compartilhar listados.</span><span class="sxs-lookup"><span data-stu-id="07af7-167">You should see hello share listed.</span></span>
   
    ![Criação do compartilhamento bem-sucedida](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a><span data-ttu-id="07af7-169">Modificar um compartilhamento</span><span class="sxs-lookup"><span data-stu-id="07af7-169">Modify a share</span></span>

<span data-ttu-id="07af7-170">Modificar um compartilhamento quando precisar de descrição de saudação do toochange do compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="07af7-170">Modify a share when you need toochange hello description of hello share.</span></span> <span data-ttu-id="07af7-171">Outras propriedades de compartilhamento não podem ser modificadas após a criação do compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="07af7-171">No other share properties can be modified once hello share is created.</span></span>

#### <a name="toomodify-a-share"></a><span data-ttu-id="07af7-172">toomodify um compartilhamento</span><span class="sxs-lookup"><span data-stu-id="07af7-172">toomodify a share</span></span>

1. <span data-ttu-id="07af7-173">De saudação **compartilhamentos** configuração na folha do resumida de serviço do StorSimple hello, selecione Olá array virtual no qual Olá compartilhamento desejar toomodify reside.</span><span class="sxs-lookup"><span data-stu-id="07af7-173">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you toomodify resides.</span></span>
2. <span data-ttu-id="07af7-174">**Selecione** Olá descrição do compartilhamento tooview Olá atual e modificá-lo.</span><span class="sxs-lookup"><span data-stu-id="07af7-174">**Select** hello share tooview hello current description and modify it.</span></span>
3. <span data-ttu-id="07af7-175">Salvar as alterações clicando Olá **salvar** barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="07af7-175">Save your changes by clicking hello **Save** command bar.</span></span> <span data-ttu-id="07af7-176">As configurações especificadas serão aplicadas e você verá uma notificação.</span><span class="sxs-lookup"><span data-stu-id="07af7-176">Your specified settings will be applied and you will see a notification.</span></span>
   
    ![ <span data-ttu-id="07af7-177">Editar compartilhamento</span><span class="sxs-lookup"><span data-stu-id="07af7-177">Edit share</span></span>](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a><span data-ttu-id="07af7-178">Colocar um compartilhamento offline</span><span class="sxs-lookup"><span data-stu-id="07af7-178">Take a share offline</span></span>

<span data-ttu-id="07af7-179">Talvez seja necessário tootake um compartilhamento offline quando você estiver planejando toomodify-lo ou exclua-lo.</span><span class="sxs-lookup"><span data-stu-id="07af7-179">You may need tootake a share offline when you are planning toomodify it or delete it.</span></span> <span data-ttu-id="07af7-180">Quando um compartilhamento está offline, não fica disponível para acesso de leitura e gravação.</span><span class="sxs-lookup"><span data-stu-id="07af7-180">When a share is offline, it is not available for read-write access.</span></span> <span data-ttu-id="07af7-181">Você precisará tootake Olá compartilhamento offline no host hello, bem como no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="07af7-181">You will need tootake hello share offline on hello host as well as on hello device.</span></span>

#### <a name="tootake-a-share-offline"></a><span data-ttu-id="07af7-182">tootake um compartilhamento offline</span><span class="sxs-lookup"><span data-stu-id="07af7-182">tootake a share offline</span></span>

1. <span data-ttu-id="07af7-183">Certifique-se de que compartilham Olá em questão não está em uso antes de colocá-lo offline.</span><span class="sxs-lookup"><span data-stu-id="07af7-183">Make sure that hello share in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="07af7-184">Assumir Olá compartilhamento matriz de saudação offline executando Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="07af7-184">Take hello share on hello array offline by performing hello following steps:</span></span>
   
    1. <span data-ttu-id="07af7-185">De saudação **compartilhamentos** configuração na folha do resumida de serviço do StorSimple hello, selecione Olá array virtual no qual Olá reside compartilhamento desejar tootake off-line.</span><span class="sxs-lookup"><span data-stu-id="07af7-185">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish you tootake offline resides.</span></span>

    2. <span data-ttu-id="07af7-186">**Selecione** compartilhamento hello e clique em **...**  (como alternativa, clique na linha) e no menu de contexto hello, selecione **colocar offline**.</span><span class="sxs-lookup"><span data-stu-id="07af7-186">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Take offline**.</span></span>
     
        ![Compartilhamento offline](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. <span data-ttu-id="07af7-188">Revise as informações de Olá Olá **colocar offline** folha e confirmar a aceitação da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="07af7-188">Review hello information in hello **Take offline** blade and confirm your acceptance of hello operation.</span></span> <span data-ttu-id="07af7-189">Clique em **colocar offline** tootake compartilhamento de saudação offline.</span><span class="sxs-lookup"><span data-stu-id="07af7-189">Click **Take offline** tootake hello share offline.</span></span> <span data-ttu-id="07af7-190">Você verá uma notificação de operação de saudação em andamento.</span><span class="sxs-lookup"><span data-stu-id="07af7-190">You will see a notification of hello operation in progress.</span></span>

    4. <span data-ttu-id="07af7-191">tooconfirm que Olá compartilhamento foi realizado com êxito toohello off-line, vá **compartilhamentos** folha.</span><span class="sxs-lookup"><span data-stu-id="07af7-191">tooconfirm that hello share was successfully taken offline, go toohello **Shares** blade.</span></span> <span data-ttu-id="07af7-192">Você deve ver o status de saudação do compartilhamento de saudação como off-line.</span><span class="sxs-lookup"><span data-stu-id="07af7-192">You should see hello status of hello share as offline.</span></span>

## <a name="delete-a-share"></a><span data-ttu-id="07af7-193">Excluir um compartilhamento</span><span class="sxs-lookup"><span data-stu-id="07af7-193">Delete a share</span></span>

> [!IMPORTANT]
> <span data-ttu-id="07af7-194">Você somente pode excluir um compartilhamento se ele está offline.</span><span class="sxs-lookup"><span data-stu-id="07af7-194">You can delete a share only if it is offline.</span></span>


<span data-ttu-id="07af7-195">Olá concluir etapas toodelete um compartilhamento a seguir.</span><span class="sxs-lookup"><span data-stu-id="07af7-195">Complete hello following steps toodelete a share.</span></span>

#### <a name="toodelete-a-share"></a><span data-ttu-id="07af7-196">toodelete um compartilhamento</span><span class="sxs-lookup"><span data-stu-id="07af7-196">toodelete a share</span></span>

1. <span data-ttu-id="07af7-197">De saudação **compartilhamentos** configuração na folha do resumida de serviço do StorSimple hello, selecione Olá array virtual no qual compartilhamento Olá desejar toodelete reside.</span><span class="sxs-lookup"><span data-stu-id="07af7-197">From hello **Shares** setting on hello StorSimple service summary blade, select hello virtual array on which hello share you wish toodelete resides.</span></span>
2. <span data-ttu-id="07af7-198">**Selecione** compartilhamento hello e clique em **...**  (como alternativa, clique na linha) e no menu de contexto hello, selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="07af7-198">**Select** hello share and Click **...** (alternately right-click in this row) and from hello context menu, select **Delete**.</span></span>
   
    ![Excluir compartilhamento](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. <span data-ttu-id="07af7-200">Verificar o status de saudação do compartilhamento Olá deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="07af7-200">Check hello status of hello share you want toodelete.</span></span> <span data-ttu-id="07af7-201">Se você deseja toodelete de compartilhamento de saudação não estiver offline, primeiro coloque-o offline.</span><span class="sxs-lookup"><span data-stu-id="07af7-201">If hello share you want toodelete is not offline, take it offline first.</span></span> <span data-ttu-id="07af7-202">Siga as etapas de saudação em [colocar um compartilhamento offline](#take-a-share-offline).</span><span class="sxs-lookup"><span data-stu-id="07af7-202">Follow hello steps in [Take a share offline](#take-a-share-offline).</span></span>
4. <span data-ttu-id="07af7-203">Quando for solicitada a confirmação no hello **excluir** folha, aceite a confirmação de saudação e clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="07af7-203">When prompted for confirmation in hello **Delete** blade, accept hello confirmation and click **Delete**.</span></span> <span data-ttu-id="07af7-204">compartilhamento de saudação será excluída e Olá **compartilhamentos** folha mostra a lista de saudação atualizada de compartilhamentos em matriz virtual hello.</span><span class="sxs-lookup"><span data-stu-id="07af7-204">hello share will now be deleted and hello **Shares** blade shows hello updated list of shares within hello virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07af7-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="07af7-205">Next steps</span></span>
<span data-ttu-id="07af7-206">Saiba como muito[clonar um compartilhamento de StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="07af7-206">Learn how too[clone a StorSimple share](storsimple-virtual-array-clone.md).</span></span>

