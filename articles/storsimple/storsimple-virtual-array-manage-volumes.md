---
title: Gerenciar volumes na StorSimple Virtual Array | Microsoft Docs
description: "Descreve o Gerenciador de Dispositivos StorSimple e explica como usá-lo para gerenciar volumes em sua Matriz Virtual StorSimple."
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
ms.openlocfilehash: a507bf1866952cb79fa6334fed80c88cd207cd0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-device-manager-service-to-manage-volumes-on-the-storsimple-virtual-array"></a><span data-ttu-id="ad6d6-103">Usar o Gerenciador de Dispositivos StorSimple para gerenciar volumes na Matriz Virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="ad6d6-103">Use StorSimple Device Manager service to manage volumes on the StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="ad6d6-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ad6d6-104">Overview</span></span>

<span data-ttu-id="ad6d6-105">Este tutorial explica como usar o serviço Gerenciador de Dispositivos StorSimple para criar e gerenciar volumes na Matriz Virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-105">This tutorial explains how to use the StorSimple Device Manager service to create and manage volumes on your StorSimple Virtual Array.</span></span>

<span data-ttu-id="ad6d6-106">O serviço Gerenciador de Dispositivos StorSimple é uma extensão do portal do Azure que permite gerenciar a solução StorSimple em uma única interface da Web.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-106">The StorSimple Device Manager service is an extension in the Azure portal that lets you manage your StorSimple solution from a single web interface.</span></span> <span data-ttu-id="ad6d6-107">Além de gerenciar compartilhamentos e volumes, você pode usar o serviço Gerenciador de Dispositivos StorSimple para exibir e gerenciar dispositivos, exibir alertas, exibir e gerenciar políticas de backup e o catálogo de backup.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-107">In addition to managing shares and volumes, you can use the StorSimple Device Manager service to view and manage devices, view alerts, and view and manage backup policies and the backup catalog.</span></span>

## <a name="volume-types"></a><span data-ttu-id="ad6d6-108">Tipos de volumes</span><span class="sxs-lookup"><span data-stu-id="ad6d6-108">Volume Types</span></span>

<span data-ttu-id="ad6d6-109">Os volumes do StorSimple podem ser:</span><span class="sxs-lookup"><span data-stu-id="ad6d6-109">StorSimple volumes can be:</span></span>

* <span data-ttu-id="ad6d6-110">**Fixados localmente**: os dados nesses volumes permanecerão sempre na matriz e não transbordam para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-110">**Locally pinned**: Data in these volumes stays on the array at all times and does not spill to the cloud.</span></span>
* <span data-ttu-id="ad6d6-111">**Em camadas**: os dados nesses volumes podem transbordar para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-111">**Tiered**: Data in these volumes can spill to the cloud.</span></span> <span data-ttu-id="ad6d6-112">Quando você cria um volume em camadas, aproximadamente 10% do espaço é provisionado na camada de local e 90% do espaço é provisionado na nuvem.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-112">When you create a tiered volume, approximately 10 % of the space is provisioned on the local tier and 90 % of the space is provisioned in the cloud.</span></span> <span data-ttu-id="ad6d6-113">Por exemplo, se você provisionar um volume de 1 TB, 100 GB residiria no espaço local e 900 GB seria usado na nuvem quando os dados fossem distribuídos em camadas.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-113">For example, if you provisioned a 1 TB volume, 100 GB would reside in the local space and 900 GB would be used in the cloud when the data tiers.</span></span> <span data-ttu-id="ad6d6-114">Isso, por sua vez, implica que se você ficar sem todo o espaço local no dispositivo, não poderá provisionar um volume em camadas (porque 10% necessários na camada local não estarão disponíveis).</span><span class="sxs-lookup"><span data-stu-id="ad6d6-114">This in turn implies that if you run out of all the local space on the device, you cannot provision a tiered volume (because the 10 % required on the local tier will not be available).</span></span>

### <a name="provisioned-capacity"></a><span data-ttu-id="ad6d6-115">Capacidade provisionada</span><span class="sxs-lookup"><span data-stu-id="ad6d6-115">Provisioned capacity</span></span>
<span data-ttu-id="ad6d6-116">Consulte a tabela a seguir para saber a capacidade máxima provisionada para cada tipo de volume.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-116">Refer to the following table for maximum provisioned capacity for each volume type.</span></span>

| <span data-ttu-id="ad6d6-117">**Identificador de limite**</span><span class="sxs-lookup"><span data-stu-id="ad6d6-117">**Limit identifier**</span></span>                                       | <span data-ttu-id="ad6d6-118">**Limite**</span><span class="sxs-lookup"><span data-stu-id="ad6d6-118">**Limit**</span></span>     |
|------------------------------------------------------------|---------------|
| <span data-ttu-id="ad6d6-119">Tamanho mínimo de um volume em camadas</span><span class="sxs-lookup"><span data-stu-id="ad6d6-119">Minimum size of a tiered volume</span></span>                            | <span data-ttu-id="ad6d6-120">500 GB</span><span class="sxs-lookup"><span data-stu-id="ad6d6-120">500 GB</span></span>        |
| <span data-ttu-id="ad6d6-121">Tamanho máximo de um volume em camadas</span><span class="sxs-lookup"><span data-stu-id="ad6d6-121">Maximum size of a tiered volume</span></span>                            | <span data-ttu-id="ad6d6-122">5 TB</span><span class="sxs-lookup"><span data-stu-id="ad6d6-122">5 TB</span></span>          |
| <span data-ttu-id="ad6d6-123">Tamanho mínimo de um volume fixado localmente</span><span class="sxs-lookup"><span data-stu-id="ad6d6-123">Minimum size of a locally pinned volume</span></span>                    | <span data-ttu-id="ad6d6-124">50 GB</span><span class="sxs-lookup"><span data-stu-id="ad6d6-124">50 GB</span></span>         |
| <span data-ttu-id="ad6d6-125">Tamanho máximo de um volume fixado localmente</span><span class="sxs-lookup"><span data-stu-id="ad6d6-125">Maximum size of a locally pinned volume</span></span>                    | <span data-ttu-id="ad6d6-126">500 GB</span><span class="sxs-lookup"><span data-stu-id="ad6d6-126">500 GB</span></span>        |

## <a name="the-volumes-blade"></a><span data-ttu-id="ad6d6-127">A página Volumes</span><span class="sxs-lookup"><span data-stu-id="ad6d6-127">The Volumes blade</span></span>
<span data-ttu-id="ad6d6-128">O menu **Volumes** na sua folha de resumo do serviço StorSimple exibe a lista de volumes de armazenamento em determinada matriz StorSimple e permite gerenciá-los.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-128">The **Volumes** menu on your StorSimple service summary blade displays the list of storage volumes on a given StorSimple array and allows you to manage them.</span></span>

![Folha Volumes](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

<span data-ttu-id="ad6d6-130">Um volume consiste em uma série de atributos:</span><span class="sxs-lookup"><span data-stu-id="ad6d6-130">A volume consists of a series of attributes:</span></span>

* <span data-ttu-id="ad6d6-131">**Nome** – Um nome descritivo que deve ser exclusivo e que ajuda a identificar o volume.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-131">**Volume Name** – A descriptive name that must be unique and helps identify the volume.</span></span>
* <span data-ttu-id="ad6d6-132">**Status** – Pode ser online ou offline.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-132">**Status** – Can be online or offline.</span></span> <span data-ttu-id="ad6d6-133">Se um volume estiver offline, não é visível para os iniciadores (servidores) que têm permissão de acesso para usar o volume.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-133">If a volume is offline, it is not visible to initiators (servers) that are allowed access to use the volume.</span></span>
* <span data-ttu-id="ad6d6-134">**Tipo** – Indica se o volume é **Em camadas** (o padrão) ou **Afixados localmente**.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-134">**Type** – Indicates whether the volume is **Tiered** (the default) or **Locally pinned**.</span></span>
* <span data-ttu-id="ad6d6-135">**Capacidade** – especifica a quantidade de dados usados em comparação com a quantidade total de dados que podem ser armazenados pelo inicializador (servidor).</span><span class="sxs-lookup"><span data-stu-id="ad6d6-135">**Capacity** – specifies the amount of data used as compared to the total amount of data that can be stored by the initiator (server).</span></span>
* <span data-ttu-id="ad6d6-136">**Backup** – no caso da Matriz Virtual StorSimple, todos os volumes são habilitados para backup automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-136">**Backup** – In case of the StorSimple Virtual Array, all volumes are automatically enabled for backup.</span></span>
* <span data-ttu-id="ad6d6-137">**Hosts conectados** – especifica os iniciadores (servidores) que podem acessar o volume.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-137">**Connected hosts** – Specifies the initiators (servers) that are allowed access to this volume.</span></span>

![Detalhes dos volumes](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

<span data-ttu-id="ad6d6-139">Use as instruções neste tutorial para executar as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="ad6d6-139">Use the instructions in this tutorial to perform the following tasks:</span></span>

* <span data-ttu-id="ad6d6-140">Adicionar um volume</span><span class="sxs-lookup"><span data-stu-id="ad6d6-140">Add a volume</span></span>
* <span data-ttu-id="ad6d6-141">Modificar um volume</span><span class="sxs-lookup"><span data-stu-id="ad6d6-141">Modify a volume</span></span>
* <span data-ttu-id="ad6d6-142">Colocar um volume offline</span><span class="sxs-lookup"><span data-stu-id="ad6d6-142">Take a volume offline</span></span>
* <span data-ttu-id="ad6d6-143">Excluir um volume</span><span class="sxs-lookup"><span data-stu-id="ad6d6-143">Delete a volume</span></span>

## <a name="add-a-volume"></a><span data-ttu-id="ad6d6-144">Adicionar um volume</span><span class="sxs-lookup"><span data-stu-id="ad6d6-144">Add a volume</span></span>

1. <span data-ttu-id="ad6d6-145">Na folha Resumo do serviço StorSimple, clique em **+ Adicionar volume** na barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-145">From the StorSimple service summary blade, click **+ Add volume** from the command bar.</span></span> <span data-ttu-id="ad6d6-146">Isso abre a folha **Adicionar volume**.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-146">This opens up the **Add volume** blade.</span></span>
   
    ![Adicionar volume](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. <span data-ttu-id="ad6d6-148">Na folha **Adicionar volume**, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ad6d6-148">In the **Add volume** blade, do the following:</span></span>
   
   * <span data-ttu-id="ad6d6-149">No campo **Nome do volume**, insira um nome exclusivo para o seu volume.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-149">In the **Volume name** field, enter a unique name for your volume.</span></span> <span data-ttu-id="ad6d6-150">O nome deve ser uma cadeia de caracteres contendo entre 3 e 127 caracteres.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-150">The name must be a string that contains 3 to 127 characters.</span></span>
   * <span data-ttu-id="ad6d6-151">Na lista suspensa **Tipo**, especifique se deseja criar um volume **Em camadas** ou **Fixado localmente**.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-151">In the **Type** dropdown list, specify whether to create a **Tiered** or **Locally pinned** volume.</span></span> <span data-ttu-id="ad6d6-152">Para as cargas de trabalho que exigem garantias locais, latências baixas e um melhor desempenho, selecione **Volume fixado localmente**.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-152">For workloads that require local guarantees, low latencies, and higher performance, select **Locally pinned volume**.</span></span> <span data-ttu-id="ad6d6-153">Para todos os outros dados, selecione volume **Em camadas**.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-153">For all other data, select **Tiered** volume.</span></span>
   * <span data-ttu-id="ad6d6-154">No campo **Capacidade**, especifique o tamanho do volume.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-154">In the **Capacity** field, specify the size of the volume.</span></span> <span data-ttu-id="ad6d6-155">Um volume em camadas deve ter entre 500 GB e 5 TB e um volume fixado localmente deve ter entre 50 GB e 500 GB.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-155">A tiered volume must be between 500 GB and 5 TB and a locally pinned volume must be between 50 GB and 500 GB.</span></span>
   * * <span data-ttu-id="ad6d6-156">Clique em **Hosts conectados**, selecione um ACR (registro de controle de acesso) correspondente ao iniciador iSCSI ao qual você deseja conectar esse volume e clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-156">Click **Connected hosts**, select an access control record (ACR) corresponding to the iSCSI initiator that you want to connect to this volume, and then click **Select**.</span></span>
3. <span data-ttu-id="ad6d6-157">Para adicionar um novo host conectado, clique em **Adicionar novo**, insira um nome para o host e seu IQN (nome qualificado) iSCSI e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-157">To add a new connected host, click **Add new**, enter a name for the host and its iSCSI Qualified Name (IQN), and then click **Add**.</span></span>
   
    ![Adicionar volume](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. <span data-ttu-id="ad6d6-159">Quando você tiver terminado de configurar o volume, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-159">When you've finished configuring your volume, click **Create**.</span></span> <span data-ttu-id="ad6d6-160">Um volume será criado com as configurações especificadas e você verá uma notificação quando ele for criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-160">A volume will be created with the specified settings and you will see a notification on the successful creation of the same.</span></span> <span data-ttu-id="ad6d6-161">Por padrão, o backup estará habilitado para o volume.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-161">By default backup will be enabled for the volume.</span></span>
5. <span data-ttu-id="ad6d6-162">Para confirmar se o volume foi criado com êxito, vá para a folha **Volumes** .</span><span class="sxs-lookup"><span data-stu-id="ad6d6-162">To confirm that the volume was successfully created, go to the **Volumes** blade.</span></span> <span data-ttu-id="ad6d6-163">Você deve ver o volume listado.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-163">You should see the volume listed.</span></span>
   
    ![Criação do volume bem-sucedida](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a><span data-ttu-id="ad6d6-165">Modificar um volume</span><span class="sxs-lookup"><span data-stu-id="ad6d6-165">Modify a volume</span></span>

<span data-ttu-id="ad6d6-166">Modifica um volume quando você precisa alterar os hosts que acessam o volume.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-166">Modify a volume when you need to change the hosts that access the volume.</span></span> <span data-ttu-id="ad6d6-167">Os outros atributos de um volume não poderão ser modificados depois que o volume for criado.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-167">The other attributes of a volume cannot be modified once the volume has been created.</span></span>

#### <a name="to-modify-a-volume"></a><span data-ttu-id="ad6d6-168">Para modificar um volume</span><span class="sxs-lookup"><span data-stu-id="ad6d6-168">To modify a volume</span></span>

1. <span data-ttu-id="ad6d6-169">Na configuração **Volumes** na folha de resumo do serviço StorSimple, selecione a matriz virtual no qual reside o volume que você deseja modificar.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-169">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to modify resides.</span></span>
2. <span data-ttu-id="ad6d6-170">**Selecione** o volume e clique em **Hosts conectados** para exibir o host conectado atualmente e modificá-lo para um servidor diferente.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-170">**Select** the volume and click **Connected hosts** to view the currently connected host and modify it to a different server.</span></span>
   
    ![Editar volume](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. <span data-ttu-id="ad6d6-172">Salve suas alterações clicando na barra de comandos **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-172">Save your changes by clicking the **Save** command bar.</span></span> <span data-ttu-id="ad6d6-173">As configurações especificadas serão aplicadas e você verá uma notificação.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-173">Your specified settings will be applied and you will see a notification.</span></span>

## <a name="take-a-volume-offline"></a><span data-ttu-id="ad6d6-174">Colocar um volume offline</span><span class="sxs-lookup"><span data-stu-id="ad6d6-174">Take a volume offline</span></span>

<span data-ttu-id="ad6d6-175">Talvez seja necessário colocar um volume offline quando você estiver planejando modificá-lo ou excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-175">You may need to take a volume offline when you are planning to modify it or delete it.</span></span> <span data-ttu-id="ad6d6-176">Quando um volume está offline, não está disponível para acesso de leitura / gravação.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-176">When a volume is offline, it is not available for read-write access.</span></span> <span data-ttu-id="ad6d6-177">Você precisará colocar o volume offline no host e no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-177">You will need to take the volume offline on the host as well as on the device.</span></span>

#### <a name="to-take-a-volume-offline"></a><span data-ttu-id="ad6d6-178">Para colocar um volume offline</span><span class="sxs-lookup"><span data-stu-id="ad6d6-178">To take a volume offline</span></span>

1. <span data-ttu-id="ad6d6-179">Certifique-se de que o volume em questão não está em uso antes de colocá-lo offline.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-179">Make sure that the volume in question is not in use before taking it offline.</span></span>
2. <span data-ttu-id="ad6d6-180">Coloque o volume offline no host primeiro.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-180">Take the volume offline on the host first.</span></span> <span data-ttu-id="ad6d6-181">Isso elimina qualquer risco de corrupção de dados no volume.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-181">This eliminates any potential risk of data corruption on the volume.</span></span> <span data-ttu-id="ad6d6-182">Para etapas específicas, consulte as instruções do sistema operacional do host.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-182">For specific steps, refer to the instructions for your host operating system.</span></span>
3. <span data-ttu-id="ad6d6-183">Depois que o volume no host ficar offline, coloque o volume no dispositivo offline executando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="ad6d6-183">After the volume on the host is offline, take the volume on the array  offline by performing the following steps:</span></span>
   
   * <span data-ttu-id="ad6d6-184">Na configuração **Volumes** na folha de resumo do serviço StorSimple, selecione a matriz virtual no qual reside o volume que você deseja colocar offline.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-184">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to take offline resides.</span></span>
   * <span data-ttu-id="ad6d6-185">**Selecione** o volume e clique em **...** (como alternativa, clique com o botão direito do mouse nesta linha) e, no menu de contexto, selecione **Colocar offline**.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-185">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Take offline**.</span></span>
     
        ![Volume offline](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * <span data-ttu-id="ad6d6-187">Examine as informações na folha **Colocar offline** e confirme a aceitação da operação.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-187">Review the information in the **Take offline** blade and confirm your acceptance of the operation.</span></span> <span data-ttu-id="ad6d6-188">Clique em **Colocar offline** para desativar o volume.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-188">Click **Take offline** to take the volume offline.</span></span> <span data-ttu-id="ad6d6-189">Você verá uma notificação da operação em andamento.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-189">You will see a notification of the operation in progress.</span></span>
   * <span data-ttu-id="ad6d6-190">Para confirmar se o volume foi colocado offline com êxito, vá para a folha **Volumes** .</span><span class="sxs-lookup"><span data-stu-id="ad6d6-190">To confirm that the volume was successfully taken offline, go to the **Volumes** blade.</span></span> <span data-ttu-id="ad6d6-191">Você deve ver o status do volume como offline.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-191">You should see the status of the volume as offline.</span></span>
     
       ![Confirmação de volume offline](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a><span data-ttu-id="ad6d6-193">Excluir um volume</span><span class="sxs-lookup"><span data-stu-id="ad6d6-193">Delete a volume</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad6d6-194">Você pode excluir um volume apenas se ele estiver offline.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-194">You can delete a volume only if it is offline.</span></span>
> 
> 

<span data-ttu-id="ad6d6-195">Conclua as seguintes etapas para excluir um volume.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-195">Complete the following steps to delete a volume.</span></span>

#### <a name="to-delete-a-volume"></a><span data-ttu-id="ad6d6-196">Para excluir um volume</span><span class="sxs-lookup"><span data-stu-id="ad6d6-196">To delete a volume</span></span>

1. <span data-ttu-id="ad6d6-197">Na configuração **Volumes** na folha de resumo do serviço StorSimple, selecione a matriz virtual na qual reside o volume que você deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-197">From the **Volumes** setting on the StorSimple service summary blade, select the virtual array on which the volume you wish you to delete resides.</span></span>
2. <span data-ttu-id="ad6d6-198">**Selecione** o volume e clique em **...** (como alternativa, clique com o botão direito do mouse nesta linha) e, no menu de contexto, selecione **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-198">**Select** the volume and click **...** (alternately right-click in this row) and from the context menu, select **Delete**.</span></span>
   
    ![Excluir volume](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. <span data-ttu-id="ad6d6-200">Verifique o status do volume que deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-200">Check the status of the volume you want to delete.</span></span> <span data-ttu-id="ad6d6-201">Se o volume que você deseja excluir não estiver offline, coloque-o offline em primeiro lugar, seguindo as etapas em [Colocar um volume offline](#take-a-volume-offline).</span><span class="sxs-lookup"><span data-stu-id="ad6d6-201">If the volume you want to delete is not offline, take it offline first, following the steps in [Take a volume offline](#take-a-volume-offline).</span></span>
4. <span data-ttu-id="ad6d6-202">Quando a confirmação for solicitada na folha **Excluir**, aceite a confirmação e clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-202">When prompted for confirmation in the **Delete** blade, accept the confirmation and click **Delete**.</span></span> <span data-ttu-id="ad6d6-203">O volume será excluído e a folha **Volumes** mostrará a lista atualizada de volumes na matriz virtual.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-203">The volume will now be deleted and the **Volumes** blade will show the updated list of volumes within the virtual array.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad6d6-204">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ad6d6-204">Next steps</span></span>

<span data-ttu-id="ad6d6-205">Saiba como [Clonar um volume StorSimple](storsimple-virtual-array-clone.md).</span><span class="sxs-lookup"><span data-stu-id="ad6d6-205">Learn how to [clone a StorSimple volume](storsimple-virtual-array-clone.md).</span></span>

