---
title: "Implantar o serviço do StorSimple Device Manager | Microsoft Docs"
description: "Explica como criar e excluir o serviço Gerenciador de Dispositivo do StorSimple no Portal do Azure, além de descrever como gerenciar a chave de registro do serviço."
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
ms.openlocfilehash: 1881a0625b107ae1a90e5b772f5296a4d728973d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-the-storsimple-device-manager-service-for-storsimple-virtual-array"></a><span data-ttu-id="73c38-103">Implantar o serviço Gerenciador de Dispositivo do StorSimple para a Matriz Virtual do StorSimple</span><span class="sxs-lookup"><span data-stu-id="73c38-103">Deploy the StorSimple Device Manager service for StorSimple Virtual Array</span></span>
## <a name="overview"></a><span data-ttu-id="73c38-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="73c38-104">Overview</span></span>

<span data-ttu-id="73c38-105">O serviço Gerenciador de Dispositivo do StorSimple é executado no Microsoft Azure e se conecta a vários dispositivos StorSimple.</span><span class="sxs-lookup"><span data-stu-id="73c38-105">The StorSimple Device Manager service runs in Microsoft Azure and connects to multiple StorSimple devices.</span></span> <span data-ttu-id="73c38-106">Depois de criar o serviço, você pode usá-lo para gerenciar os dispositivos no portal do Microsoft Azure em execução em um navegador.</span><span class="sxs-lookup"><span data-stu-id="73c38-106">After you create the service, you can use it to manage the devices from the Microsoft Azure portal running in a browser.</span></span> <span data-ttu-id="73c38-107">Isso permite monitorar todos os dispositivos que estão conectados ao serviço Gerenciador de Dispositivo do StorSimple de um local único e central, minimizando a sobrecarga administrativa.</span><span class="sxs-lookup"><span data-stu-id="73c38-107">This allows you to monitor all the devices that are connected to the StorSimple Device Manager service from a single, central location, thereby minimizing administrative burden.</span></span>

<span data-ttu-id="73c38-108">As tarefas comuns relacionadas a um serviço Gerenciador de Dispositivo do StorSimple são:</span><span class="sxs-lookup"><span data-stu-id="73c38-108">The common tasks related to a StorSimple Device Manager service are:</span></span>

* <span data-ttu-id="73c38-109">Criar um serviço</span><span class="sxs-lookup"><span data-stu-id="73c38-109">Create a service</span></span>
* <span data-ttu-id="73c38-110">Excluir um serviço</span><span class="sxs-lookup"><span data-stu-id="73c38-110">Delete a service</span></span>
* <span data-ttu-id="73c38-111">Obtenha a chave de registro do serviço</span><span class="sxs-lookup"><span data-stu-id="73c38-111">Get the service registration key</span></span>
* <span data-ttu-id="73c38-112">Regenerar a chave de registro do serviço</span><span class="sxs-lookup"><span data-stu-id="73c38-112">Regenerate the service registration key</span></span>

<span data-ttu-id="73c38-113">Este tutorial descreve como executar cada uma dessas tarefas.</span><span class="sxs-lookup"><span data-stu-id="73c38-113">This tutorial describes how to perform each of the preceding tasks.</span></span> <span data-ttu-id="73c38-114">As informações contidas neste artigo aplicam-se apenas a Matrizes Virtuais do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="73c38-114">The information contained in this article is applicable only to StorSimple Virtual Arrays.</span></span> <span data-ttu-id="73c38-115">Para obter mais informações sobre a série 8000 do StorSimple, acesse [implantar um serviço StorSimple Manager](storsimple-manage-service.md).</span><span class="sxs-lookup"><span data-stu-id="73c38-115">For more information on StorSimple 8000 series, go to [deploy a StorSimple Manager service](storsimple-manage-service.md).</span></span>

## <a name="create-a-service"></a><span data-ttu-id="73c38-116">Criar um serviço</span><span class="sxs-lookup"><span data-stu-id="73c38-116">Create a service</span></span>

<span data-ttu-id="73c38-117">Para criar um serviço, você precisa ter:</span><span class="sxs-lookup"><span data-stu-id="73c38-117">To create a service, you need to have:</span></span>

* <span data-ttu-id="73c38-118">Uma assinatura com um Enterprise Agreement</span><span class="sxs-lookup"><span data-stu-id="73c38-118">A subscription with an Enterprise Agreement</span></span>
* <span data-ttu-id="73c38-119">Uma conta de armazenamento ativa do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="73c38-119">An active Microsoft Azure storage account</span></span>
* <span data-ttu-id="73c38-120">As informações de cobrança que são usadas para gerenciamento de acesso</span><span class="sxs-lookup"><span data-stu-id="73c38-120">The billing information that is used for access management</span></span>

<span data-ttu-id="73c38-121">Também é possível optar por gerar uma conta de armazenamento ao criar o serviço.</span><span class="sxs-lookup"><span data-stu-id="73c38-121">You can also choose to generate a storage account when you create the service.</span></span>

<span data-ttu-id="73c38-122">Um único serviço pode gerenciar vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="73c38-122">A single service can manage multiple devices.</span></span> <span data-ttu-id="73c38-123">No entanto, um dispositivo não pode abranger vários serviços.</span><span class="sxs-lookup"><span data-stu-id="73c38-123">However, a device cannot span multiple services.</span></span> <span data-ttu-id="73c38-124">Uma grande empresa pode ter várias instâncias do serviço para trabalhar com diferentes assinaturas, organizações ou até mesmo locais de implantação.</span><span class="sxs-lookup"><span data-stu-id="73c38-124">A large enterprise can have multiple service instances to work with different subscriptions, organizations, or even deployment locations.</span></span>

> [!NOTE]
> <span data-ttu-id="73c38-125">Você precisa de instâncias separadas do serviço Gerenciador de Dispositivo do StorSimple para gerenciar as Matrizes Virtuais e os dispositivos da série 8000 do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="73c38-125">You need separate instances of StorSimple Device Manager service to manage StorSimple 8000 series devices and StorSimple Virtual Arrays.</span></span>


<span data-ttu-id="73c38-126">Execute as etapas a seguir para criar um serviço.</span><span class="sxs-lookup"><span data-stu-id="73c38-126">Perform the following steps to create a service.</span></span>

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a><span data-ttu-id="73c38-127">Excluir um serviço</span><span class="sxs-lookup"><span data-stu-id="73c38-127">Delete a service</span></span>

<span data-ttu-id="73c38-128">Antes de excluir um serviço, verifique se nenhum dispositivo conectado está usando ele.</span><span class="sxs-lookup"><span data-stu-id="73c38-128">Before you delete a service, make sure that no connected devices are using it.</span></span> <span data-ttu-id="73c38-129">Se o serviço estiver em uso, desative os dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="73c38-129">If the service is in use, deactivate the connected devices.</span></span> <span data-ttu-id="73c38-130">A operação de desativação desfaz a conexão entre o dispositivo e o serviço, mas preserva os dados do dispositivo na nuvem.</span><span class="sxs-lookup"><span data-stu-id="73c38-130">The deactivate operation will sever the connection between the device and the service, but preserve the device data in the cloud.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73c38-131">Depois que um serviço é excluído, a operação não pode ser revertida.</span><span class="sxs-lookup"><span data-stu-id="73c38-131">After a service is deleted, the operation cannot be reversed.</span></span> <span data-ttu-id="73c38-132">Qualquer dispositivo que estava usando o serviço precisará ser redefinida para as configurações de fábrica para que possa ser usado com outro serviço.</span><span class="sxs-lookup"><span data-stu-id="73c38-132">Any device that was using the service will need to be factory reset before it can be used with another service.</span></span> <span data-ttu-id="73c38-133">Nesse cenário, os dados locais no dispositivo, bem como a configuração, serão perdidos.</span><span class="sxs-lookup"><span data-stu-id="73c38-133">In this scenario, the local data on the device, as well as the configuration, will be lost.</span></span>
 

<span data-ttu-id="73c38-134">Execute as etapas a seguir para excluir um serviço.</span><span class="sxs-lookup"><span data-stu-id="73c38-134">Perform the following steps to delete a service.</span></span>

#### <a name="to-delete-a-service"></a><span data-ttu-id="73c38-135">Para excluir um serviço</span><span class="sxs-lookup"><span data-stu-id="73c38-135">To delete a service</span></span>

1. <span data-ttu-id="73c38-136">Acesse **Todos os recursos**.</span><span class="sxs-lookup"><span data-stu-id="73c38-136">Go to **All resources**.</span></span> <span data-ttu-id="73c38-137">Pesquise por seu serviço Gerenciador de Dispositivo do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="73c38-137">Search for your StorSimple Device Manager service.</span></span> <span data-ttu-id="73c38-138">Selecione o serviço que você deseja excluir.</span><span class="sxs-lookup"><span data-stu-id="73c38-138">Select the service that you wish to delete.</span></span>
   
    ![Selecione o serviço para exclusão](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. <span data-ttu-id="73c38-140">Acesse o painel do serviço para garantir que nenhum dispositivo esteja conectado a ele.</span><span class="sxs-lookup"><span data-stu-id="73c38-140">Go to your service dashboard to ensure there are no devices connected to the service.</span></span> <span data-ttu-id="73c38-141">Se não houver algum dispositivo registrado nesse serviço, você também verá uma mensagem de cabeçalho sobre isso.</span><span class="sxs-lookup"><span data-stu-id="73c38-141">If there are no devices registered with this service, you will also see a banner message to the effect.</span></span> <span data-ttu-id="73c38-142">Clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="73c38-142">Click **Delete**.</span></span>
   
    ![Excluir serviço](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. <span data-ttu-id="73c38-144">Quando receber a solicitação de confirmação, clique em **Sim** na notificação de confirmação.</span><span class="sxs-lookup"><span data-stu-id="73c38-144">When prompted for confirmation, click **Yes** in the confirmation notification.</span></span> 
   
    ![Confirmar exclusão do serviço](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. <span data-ttu-id="73c38-146">Pode levar alguns minutos para que o serviço seja excluído.</span><span class="sxs-lookup"><span data-stu-id="73c38-146">It may take a few minutes for the service to be deleted.</span></span> <span data-ttu-id="73c38-147">Após a exclusão bem-sucedida do serviço, você receberá uma notificação.</span><span class="sxs-lookup"><span data-stu-id="73c38-147">After the service is successfully deleted, you will be notified.</span></span>
   
    ![Exclusão bem-sucedida do serviço](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

<span data-ttu-id="73c38-149">A lista de serviços será atualizada.</span><span class="sxs-lookup"><span data-stu-id="73c38-149">The list of services will be refreshed.</span></span>

 ![Lista de serviços atualizada](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-the-service-registration-key"></a><span data-ttu-id="73c38-151">Obtenha a chave de registro do serviço</span><span class="sxs-lookup"><span data-stu-id="73c38-151">Get the service registration key</span></span>
<span data-ttu-id="73c38-152">Depois de ter criado um serviço com êxito, você precisará registrar o dispositivo StorSimple no serviço.</span><span class="sxs-lookup"><span data-stu-id="73c38-152">After you have successfully created a service, you will need to register your StorSimple device with the service.</span></span> <span data-ttu-id="73c38-153">Para registrar seu primeiro dispositivo StorSimple, será necessária a chave de registro do serviço.</span><span class="sxs-lookup"><span data-stu-id="73c38-153">To register your first StorSimple device, you will need the service registration key.</span></span> <span data-ttu-id="73c38-154">Para registrar dispositivos adicionais em um serviço StorSimple existente, serão necessárias a chave de registro e a chave de criptografia dos dados de serviço (que é gerada durante o registro do primeiro dispositivo).</span><span class="sxs-lookup"><span data-stu-id="73c38-154">To register additional devices with an existing StorSimple service, you will need both the registration key and the service data encryption key (which is generated on the first device during registration).</span></span> <span data-ttu-id="73c38-155">Para obter mais informações sobre a chave de criptografia dos dados de serviço, consulte [Segurança do StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="73c38-155">For more information about the service data encryption key, see [StorSimple security](storsimple-security.md).</span></span> <span data-ttu-id="73c38-156">Você pode obter a chave de registro acessando a folha **Chaves** de seu serviço.</span><span class="sxs-lookup"><span data-stu-id="73c38-156">You can get the registration key by accessing the **Keys** blade for your service.</span></span>

<span data-ttu-id="73c38-157">Execute as etapas a seguir para obter a chave de registro do serviço.</span><span class="sxs-lookup"><span data-stu-id="73c38-157">Perform the following steps to get the service registration key.</span></span>

#### <a name="to-get-the-service-registration-key"></a><span data-ttu-id="73c38-158">Para obter a chave de registro do serviço</span><span class="sxs-lookup"><span data-stu-id="73c38-158">To get the service registration key</span></span>
1. <span data-ttu-id="73c38-159">No **Gerenciador de Dispositivo do StorSimple**, acesse **Gerenciamento&gt;** **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="73c38-159">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![Folha Chaves](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="73c38-161">Na folha **Chaves**, uma chave de registro de serviço será exibida.</span><span class="sxs-lookup"><span data-stu-id="73c38-161">In the **Keys** blade, a service registration key appears.</span></span> <span data-ttu-id="73c38-162">Copie a chave de registro usando o ícone de cópia.</span><span class="sxs-lookup"><span data-stu-id="73c38-162">Copy the registration key using the copy icon.</span></span> 

<span data-ttu-id="73c38-163">Mantenha a chave de registro do serviço em local seguro.</span><span class="sxs-lookup"><span data-stu-id="73c38-163">Keep the service registration key in a safe location.</span></span> <span data-ttu-id="73c38-164">Você precisará dessa chave, bem como da chave de criptografia dos dados de serviço, para registrar dispositivos adicionais nesse serviço.</span><span class="sxs-lookup"><span data-stu-id="73c38-164">You will need this key, as well as the service data encryption key, to register additional devices with this service.</span></span> <span data-ttu-id="73c38-165">Depois de obter a chave de registro do serviço, você precisará configurar o dispositivo usando o Windows PowerShell para interface do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="73c38-165">After obtaining the service registration key, you will need to configure your device through the Windows PowerShell for StorSimple interface.</span></span>

## <a name="regenerate-the-service-registration-key"></a><span data-ttu-id="73c38-166">Regenerar a chave de registro do serviço</span><span class="sxs-lookup"><span data-stu-id="73c38-166">Regenerate the service registration key</span></span>
<span data-ttu-id="73c38-167">Você precisará regenerar uma chave de registro de serviço se tiver que executar a rotação de chave ou se a lista de administradores de serviço tiver mudado.</span><span class="sxs-lookup"><span data-stu-id="73c38-167">You will need to regenerate a service registration key if you are required to perform key rotation or if the list of service administrators has changed.</span></span> <span data-ttu-id="73c38-168">Quando você regenera a chave, a nova chave é usada somente para registrar dispositivos subsequentes.</span><span class="sxs-lookup"><span data-stu-id="73c38-168">When you regenerate the key, the new key is used only for registering subsequent devices.</span></span> <span data-ttu-id="73c38-169">Os dispositivos que já foram registrados não serão afetados por esse processo.</span><span class="sxs-lookup"><span data-stu-id="73c38-169">The devices that were already registered are unaffected by this process.</span></span>

<span data-ttu-id="73c38-170">Execute as etapas a seguir para regenerar uma chave de registro de serviço.</span><span class="sxs-lookup"><span data-stu-id="73c38-170">Perform the following steps to regenerate a service registration key.</span></span>

#### <a name="to-regenerate-the-service-registration-key"></a><span data-ttu-id="73c38-171">Para regenerar a chave de registro de serviço</span><span class="sxs-lookup"><span data-stu-id="73c38-171">To regenerate the service registration key</span></span>
1. <span data-ttu-id="73c38-172">No **Gerenciador de Dispositivo do StorSimple**, acesse **Gerenciamento&gt;** **Chaves**.</span><span class="sxs-lookup"><span data-stu-id="73c38-172">In the **StorSimple Device Manager** blade, go to **Management &gt;** **Keys**.</span></span>
   
   ![Folha Chaves](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. <span data-ttu-id="73c38-174">Na folha **Chaves**, clique em **Regenerar**.</span><span class="sxs-lookup"><span data-stu-id="73c38-174">In the **Keys** blade, click **Regenerate**.</span></span>
   
   ![Clique em regenerar](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. <span data-ttu-id="73c38-176">Na folha **Regenerar chave de registro do serviço**, revise a ação necessária quando as chaves forem geradas novamente.</span><span class="sxs-lookup"><span data-stu-id="73c38-176">In the **Regenerate service registration key** blade, review the action required when the keys are regenerated.</span></span> <span data-ttu-id="73c38-177">Todos os dispositivos subsequentes registrados com esse serviço usarão a nova chave de registro.</span><span class="sxs-lookup"><span data-stu-id="73c38-177">All the subsequent devices that are registered with this service will use the new registration key.</span></span> <span data-ttu-id="73c38-178">Clique em **Regenerar** para confirmar.</span><span class="sxs-lookup"><span data-stu-id="73c38-178">Click **Regenerate** to confirm.</span></span> <span data-ttu-id="73c38-179">Você receberá uma notificação após a conclusão do registro.</span><span class="sxs-lookup"><span data-stu-id="73c38-179">You will be notified after the registration is complete.</span></span>
   
   ![Confirmar regeneração da chave](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. <span data-ttu-id="73c38-181">Uma nova chave de registro de serviço será exibida.</span><span class="sxs-lookup"><span data-stu-id="73c38-181">A new service registration key will appear.</span></span>
   
    ![Confirmar regeneração da chave](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   <span data-ttu-id="73c38-183">Copie essa chave e salve-a para registrar todos os novos dispositivos nesse serviço.</span><span class="sxs-lookup"><span data-stu-id="73c38-183">Copy this key and save it for registering any new devices with this service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73c38-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="73c38-184">Next steps</span></span>
* <span data-ttu-id="73c38-185">Saiba como obter uma [Introdução](storsimple-virtual-array-deploy1-portal-prep.md) com uma Matriz Virtual do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="73c38-185">Learn how to [get started](storsimple-virtual-array-deploy1-portal-prep.md) with a StorSimple Virtual Array.</span></span>
* <span data-ttu-id="73c38-186">Saiba como [administrar o seu dispositivo StorSimple](storsimple-ova-web-ui-admin.md).</span><span class="sxs-lookup"><span data-stu-id="73c38-186">Learn how to [administer your StorSimple device](storsimple-ova-web-ui-admin.md).</span></span>

