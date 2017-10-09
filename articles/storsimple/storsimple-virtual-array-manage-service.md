---
title: "aaaDeploy serviço do Gerenciador de dispositivos de StorSimple | Microsoft Docs"
description: "Explica como toocreate e delete Olá serviço do Gerenciador de dispositivos do StorSimple no hello portal do Azure e descreve como toomanage Olá a chave de registro de serviço."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="c53f6-103">Implante o serviço de Gerenciador de dispositivos de StorSimple Olá para matriz Virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="c53f6-103">Deploy hello StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="c53f6-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c53f6-104">Overview</span></span>

<span data-ttu-id="c53f6-105">saudação de serviço do Gerenciador de dispositivos do StorSimple é executado no Microsoft Azure e conecta dispositivos de StorSimple toomultiple.</span><span class="sxs-lookup"><span data-stu-id="c53f6-105">hello StorSimple Device Manager service runs in Microsoft Azure and connects toomultiple StorSimple devices.</span></span> <span data-ttu-id="c53f6-106">Depois de criar o serviço hello, você pode usar dispositivos toomanage Olá Olá Microsoft Azure portal em execução em um navegador.</span><span class="sxs-lookup"><span data-stu-id="c53f6-106">After you create hello service, you can use it toomanage hello devices from hello Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="c53f6-107">Isso permite que você toomonitor todos os dispositivos de saudação que são conectado toohello Gerenciador de dispositivos do StorSimple do serviço de um único local central, minimizando a carga administrativa.</span><span class="sxs-lookup"><span data-stu-id="c53f6-107">This allows you toomonitor all hello devices that are connected toohello StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="c53f6-108">Olá comuns tarefas relacionadas tooa serviço do Gerenciador de dispositivos do StorSimple são:</span><span class="sxs-lookup"><span data-stu-id="c53f6-108">hello common tasks related tooa StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="c53f6-109">Criar um serviço</span><span class="sxs-lookup"><span data-stu-id="c53f6-109">Create a service</span></span>
* <span data-ttu-id="c53f6-110">Excluir um serviço</span><span class="sxs-lookup"><span data-stu-id="c53f6-110">Delete a service</span></span>
* <span data-ttu-id="c53f6-111">Obter chave de registro de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="c53f6-111">Get hello service registration key</span></span>
* <span data-ttu-id="c53f6-112">Regenerar chave de registro de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="c53f6-112">Regenerate hello service registration key</span></span>

<span data-ttu-id="c53f6-113">Este tutorial descreve como tooperform de Olá tarefas anteriores.</span><span class="sxs-lookup"><span data-stu-id="c53f6-113">This tutorial describes how tooperform each of hello preceding tasks.</span></span> <span data-ttu-id="c53f6-114">informações de saudação contidas neste artigo são aplicável somente tooStorSimple Virtual matrizes.</span><span class="sxs-lookup"><span data-stu-id="c53f6-114">hello information contained in this article is applicable only tooStorSimple Virtual Arrays.</span></span> <span data-ttu-id="c53f6-115">Para obter mais informações sobre o StorSimple série 8000, vá muito[implantar um serviço StorSimple Manager](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="c53f6-115">For more information on StorSimple 8000 series, go too[deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="c53f6-116">Criar um serviço</span><span class="sxs-lookup"><span data-stu-id="c53f6-116">Create a service</span></span>

<span data-ttu-id="c53f6-117">toocreate um serviço, é necessário toohave:</span><span class="sxs-lookup"><span data-stu-id="c53f6-117">toocreate a service, you need toohave:</span></span>

* <span data-ttu-id="c53f6-118">Uma assinatura com um Enterprise Agreement</span><span class="sxs-lookup"><span data-stu-id="c53f6-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="c53f6-119">Uma conta de armazenamento ativa do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c53f6-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="c53f6-120">Olá informações de cobrança que são usadas para gerenciamento de acesso</span><span class="sxs-lookup"><span data-stu-id="c53f6-120">hello billing information that is used for access management</span></span>

<span data-ttu-id="c53f6-121">Além disso, é possível toogenerate uma conta de armazenamento ao criar serviço hello.</span><span class="sxs-lookup"><span data-stu-id="c53f6-121">You can also choose toogenerate a storage account when you create hello service.</span></span>

<span data-ttu-id="c53f6-122">Um único serviço pode gerenciar vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="c53f6-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="c53f6-123">No entanto, um dispositivo não pode abranger vários serviços.</span><span class="sxs-lookup"><span data-stu-id="c53f6-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="c53f6-124">Uma grande empresa pode ter vários toowork de instâncias de serviço com diferentes assinaturas, organizações ou mesmo regiões de implantação.</span><span class="sxs-lookup"><span data-stu-id="c53f6-124">A large enterprise can have multiple service instances toowork with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="c53f6-125">Você precisa de instâncias separadas de dispositivos da série StorSimple 8000 Gerenciador de dispositivos do StorSimple service toomanage e matrizes de Virtual do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c53f6-125">You need separate instances of StorSimple Device Manager service toomanage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="c53f6-126">Execute Olá etapas toocreate um serviço a seguir.</span><span class="sxs-lookup"><span data-stu-id="c53f6-126">Perform hello following steps toocreate a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="c53f6-127">Excluir um serviço</span><span class="sxs-lookup"><span data-stu-id="c53f6-127">Delete a service</span></span>

<span data-ttu-id="c53f6-128">Antes de excluir um serviço, verifique se nenhum dispositivo conectado está usando ele.</span><span class="sxs-lookup"><span data-stu-id="c53f6-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="c53f6-129">Se o serviço de saudação está em uso, desative os dispositivos de saudação conectado.</span><span class="sxs-lookup"><span data-stu-id="c53f6-129">If hello service is in use, deactivate hello connected devices.</span></span> <span data-ttu-id="c53f6-130">Olá desativar operação sever conexão Olá entre dispositivo hello e serviço hello, mas preservar os dados do dispositivo Olá na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="c53f6-130">hello deactivate operation will sever hello connection between hello device and hello service, but preserve hello device data in hello cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c53f6-131">Depois que um serviço é excluído, operação Olá não pode ser revertida.</span><span class="sxs-lookup"><span data-stu-id="c53f6-131">After a service is deleted, hello operation cannot be reversed.</span></span> <span data-ttu-id="c53f6-132">Qualquer dispositivo que esteja usando o serviço de saudação precisará toobe antes que ele pode ser usado com outro serviço de redefinição de fábrica.</span><span class="sxs-lookup"><span data-stu-id="c53f6-132">Any device that was using hello service will need toobe factory reset before it can be used with another service.</span></span> <span data-ttu-id="c53f6-133">Nesse cenário, os dados de locais de saudação em dispositivo hello, bem como configuração Olá, serão perdidas.</span><span class="sxs-lookup"><span data-stu-id="c53f6-133">In this scenario, hello local data on hello device, as well as hello configuration, will be lost.</span></span>
 

<span data-ttu-id="c53f6-134">Execute Olá etapas toodelete um serviço a seguir.</span><span class="sxs-lookup"><span data-stu-id="c53f6-134">Perform hello following steps toodelete a service.</span></span>

#### <a name="toodelete-a-service"></a><span data-ttu-id="c53f6-135">toodelete um serviço</span><span class="sxs-lookup"><span data-stu-id="c53f6-135">toodelete a service</span></span>

1. <span data-ttu-id="c53f6-136">Vá muito**todos os recursos**.</span><span class="sxs-lookup"><span data-stu-id="c53f6-136">Go too**All resources**.</span></span> <span data-ttu-id="c53f6-137">Pesquise por seu serviço Gerenciador de Dispositivo do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c53f6-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="c53f6-138">Selecione o serviço de saudação que você deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="c53f6-138">Select hello service that you wish toodelete.</span></span>
   
    ![Selecione o serviço toodelete](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="c53f6-140">Vá tooyour tooensure de painel de controle de serviço não há nenhum dispositivo conectado toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="c53f6-140">Go tooyour service dashboard tooensure there are no devices connected toohello service.</span></span> <span data-ttu-id="c53f6-141">Se não houver nenhum dispositivo registrado com esse serviço, você também verá um efeito de toohello de mensagem de faixa.</span><span class="sxs-lookup"><span data-stu-id="c53f6-141">If there are no devices registered with this service, you will also see a banner message toohello effect.</span></span> <span data-ttu-id="c53f6-142">Clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="c53f6-142">Click **Delete**.</span></span>
   
    ![Excluir serviço](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="c53f6-144">Quando solicitado a confirmar, clique em **Sim** na notificação de confirmação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c53f6-144">When prompted for confirmation, click **Yes** in hello confirmation notification.</span></span> 
   
    ![Confirmar exclusão do serviço](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="c53f6-146">Ele pode levar alguns minutos para Olá serviço toobe excluído.</span><span class="sxs-lookup"><span data-stu-id="c53f6-146">It may take a few minutes for hello service toobe deleted.</span></span> <span data-ttu-id="c53f6-147">Depois de saudação serviço é excluído com êxito, você será notificado.</span><span class="sxs-lookup"><span data-stu-id="c53f6-147">After hello service is successfully deleted, you will be notified.</span></span>
   
    ![Exclusão bem-sucedida do serviço](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="c53f6-149">lista de saudação de serviços será atualizada.</span><span class="sxs-lookup"><span data-stu-id="c53f6-149">hello list of services will be refreshed.</span></span>

 ![Lista de serviços atualizada](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a><span data-ttu-id="c53f6-151">Obter chave de registro de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="c53f6-151">Get hello service registration key</span></span>
<span data-ttu-id="c53f6-152">Depois que você criou com êxito um serviço, você precisará tooregister seu dispositivo StorSimple com o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="c53f6-152">After you have successfully created a service, you will need tooregister your StorSimple device with hello service.</span></span> <span data-ttu-id="c53f6-153">tooregister seu dispositivo StorSimple primeiro, será necessário Olá o chave de registro de serviço.</span><span class="sxs-lookup"><span data-stu-id="c53f6-153">tooregister your first StorSimple device, you will need hello service registration key.</span></span> <span data-ttu-id="c53f6-154">tooregister dispositivos adicionais com um serviço StorSimple existente, você precisará chave de registro hello e chave criptografia de dados de serviço de saudação (que é gerado no primeiro dispositivo de saudação durante o registro).</span><span class="sxs-lookup"><span data-stu-id="c53f6-154">tooregister additional devices with an existing StorSimple service, you will need both hello registration key and hello service data encryption key (which is generated on hello first device during registration).</span></span> <span data-ttu-id="c53f6-155">Para obter mais informações sobre a chave de criptografia de dados de serviço hello, consulte [segurança de StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="c53f6-155">For more information about hello service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="c53f6-156">Você pode obter a chave de registro Olá acessando Olá **chaves** folha do seu serviço.</span><span class="sxs-lookup"><span data-stu-id="c53f6-156">You can get hello registration key by accessing hello **Keys** blade for your service.</span></span>

<span data-ttu-id="c53f6-157">Execute Olá etapas tooget Olá chave de registro a seguir.</span><span class="sxs-lookup"><span data-stu-id="c53f6-157">Perform hello following steps tooget hello service registration key.</span></span>

#### <a name="tooget-hello-service-registration-key"></a><span data-ttu-id="c53f6-158">chave de registro tooget Olá</span><span class="sxs-lookup"><span data-stu-id="c53f6-158">tooget hello service registration key</span></span>
1. <span data-ttu-id="c53f6-159">Em Olá **Gerenciador de dispositivos de StorSimple** folha, ir muito**gerenciamento &gt;**  **chaves**.</span><span class="sxs-lookup"><span data-stu-id="c53f6-159">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![Folha Chaves](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="c53f6-161">Em Olá **chaves** folha, uma chave de registro de serviço aparece.</span><span class="sxs-lookup"><span data-stu-id="c53f6-161">In hello **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="c53f6-162">Copiar a chave de registro de saudação usando o ícone para copiar hello.</span><span class="sxs-lookup"><span data-stu-id="c53f6-162">Copy hello registration key using hello copy icon.</span></span> 

<span data-ttu-id="c53f6-163">Mantenha a chave de registro do serviço de saudação em um local seguro.</span><span class="sxs-lookup"><span data-stu-id="c53f6-163">Keep hello service registration key in a safe location.</span></span> <span data-ttu-id="c53f6-164">Você precisará essa chave, bem como chave de criptografia de dados de serviço hello, tooregister de dispositivos adicionais com este serviço.</span><span class="sxs-lookup"><span data-stu-id="c53f6-164">You will need this key, as well as hello service data encryption key, tooregister additional devices with this service.</span></span> <span data-ttu-id="c53f6-165">Depois de obter a chave de registro de serviço hello, você precisará tooconfigure seu dispositivo por meio de saudação do Windows PowerShell para StorSimple interface.</span><span class="sxs-lookup"><span data-stu-id="c53f6-165">After obtaining hello service registration key, you will need tooconfigure your device through hello Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-hello-service-registration-key"></a><span data-ttu-id="c53f6-166">Regenerar chave de registro de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="c53f6-166">Regenerate hello service registration key</span></span>
<span data-ttu-id="c53f6-167">Se for necessário tooperform a rotação de chaves ou se a lista de saudação de administradores de serviço foi alterada, você precisará tooregenerate uma chave de registro de serviço.</span><span class="sxs-lookup"><span data-stu-id="c53f6-167">You will need tooregenerate a service registration key if you are required tooperform key rotation or if hello list of service administrators has changed.</span></span> <span data-ttu-id="c53f6-168">Quando você regenerar chave Olá, a nova chave de saudação é usado apenas para registrar dispositivos subsequentes.</span><span class="sxs-lookup"><span data-stu-id="c53f6-168">When you regenerate hello key, hello new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="c53f6-169">dispositivos de saudação que já foram registrados não são afetados por esse processo.</span><span class="sxs-lookup"><span data-stu-id="c53f6-169">hello devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="c53f6-170">Execute Olá etapas tooregenerate uma chave de registro de serviço a seguir.</span><span class="sxs-lookup"><span data-stu-id="c53f6-170">Perform hello following steps tooregenerate a service registration key.</span></span>

#### <a name="tooregenerate-hello-service-registration-key"></a><span data-ttu-id="c53f6-171">chave de registro tooregenerate Olá</span><span class="sxs-lookup"><span data-stu-id="c53f6-171">tooregenerate hello service registration key</span></span>
1. <span data-ttu-id="c53f6-172">Em Olá **Gerenciador de dispositivos de StorSimple** folha, ir muito**gerenciamento &gt;**  **chaves**.</span><span class="sxs-lookup"><span data-stu-id="c53f6-172">In hello **StorSimple Device Manager** blade, go too**Management &gt;** **Keys**.</span></span>
   
   ![Folha Chaves](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="c53f6-174">Em Olá **chaves** folha, clique em **regenerar**.</span><span class="sxs-lookup"><span data-stu-id="c53f6-174">In hello **Keys** blade, click **Regenerate**.</span></span>
   
   ![Clique em regenerar](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="c53f6-176">Em Olá **regenerar chave de registro** folha, examine Olá necessária uma ação quando hello chaves são geradas novamente.</span><span class="sxs-lookup"><span data-stu-id="c53f6-176">In hello **Regenerate service registration key** blade, review hello action required when hello keys are regenerated.</span></span> <span data-ttu-id="c53f6-177">Todos os dispositivos de saudação subsequentes que são registrados com este serviço usará a nova chave de registro hello.</span><span class="sxs-lookup"><span data-stu-id="c53f6-177">All hello subsequent devices that are registered with this service will use hello new registration key.</span></span> <span data-ttu-id="c53f6-178">Clique em **regenerar** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="c53f6-178">Click **Regenerate** tooconfirm.</span></span> <span data-ttu-id="c53f6-179">Você será notificado depois Olá registro for concluído.</span><span class="sxs-lookup"><span data-stu-id="c53f6-179">You will be notified after hello registration is complete.</span></span>
   
   ![Confirmar regeneração da chave](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="c53f6-181">Uma nova chave de registro de serviço será exibida.</span><span class="sxs-lookup"><span data-stu-id="c53f6-181">A new service registration key will appear.</span></span>
   
    ![Confirmar regeneração da chave](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="c53f6-183">Copie essa chave e salve-a para registrar todos os novos dispositivos nesse serviço.</span><span class="sxs-lookup"><span data-stu-id="c53f6-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c53f6-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c53f6-184">Next steps</span></span>
* <span data-ttu-id="c53f6-185">Saiba como muito[começar](storsimple-virtual-array-deploy1-portal-prep.md) com uma matriz Virtual StorSimple.</span><span class="sxs-lookup"><span data-stu-id="c53f6-185">Learn how too[get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="c53f6-186">Saiba como muito[administrar seu dispositivo StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="c53f6-186">Learn how too[administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

