---
title: "Dimensionar automaticamente um serviço de nuvem no portal clássico | Microsoft Docs"
description: "(clássico) Saiba como usar o portal clássico para configurar regras de dimensionamento automático para uma função web ou função de trabalho do serviço de nuvem no Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 90d55bbac6e113d6add848ace67cf0749e26342b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-classic-portal"></a><span data-ttu-id="4ca0f-103">Como configurar a colocação em escala automática em um Serviço de Nuvem no portal clássico</span><span class="sxs-lookup"><span data-stu-id="4ca0f-103">How to configure auto scaling for a Cloud Service in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ca0f-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4ca0f-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="4ca0f-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="4ca0f-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="4ca0f-106">Na página Escala do Portal Clássico do Azure, você pode definir as configurações de dimensionamento automático para a função web ou para a função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-106">On the Scale page of the Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="4ca0f-107">Como alternativa, você pode configurar a colocação em escala manual em vez da colocação em escala automática com base em regras.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="4ca0f-108">Este artigo se concentra nas funções Web e de trabalho do Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="4ca0f-109">Ao criar uma máquina virtual (modelo clássico) diretamente, ela será hospedada em um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="4ca0f-110">Algumas dessas informações se aplica a esses tipos de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-110">Some of this information applies to these types of virtual machines.</span></span> <span data-ttu-id="4ca0f-111">A colocação em escala de um conjunto de disponibilidade das máquinas virtuais é simplesmente ligá-las e desligá-las com base nas regras de dimensionamento configuradas.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-111">Scaling an availability set of virtual machines is just shutting them on and off based on the scale rules you configure.</span></span> <span data-ttu-id="4ca0f-112">Para saber mais sobre as máquinas virtuais e conjuntos de disponibilidade, confira [Gerenciar a disponibilidade de máquinas virtuais](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4ca0f-112">For more information about Virtual Machines and availability sets, see [Manage the Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="4ca0f-113">Você deve considerar as seguintes informações antes de configurar a colocação em escala do seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="4ca0f-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="4ca0f-114">A colocação em escala é afetada pelo uso de núcleo.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="4ca0f-115">As instâncias de função maiores usam mais núcleos.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-115">Larger role instances use more cores.</span></span> <span data-ttu-id="4ca0f-116">Você só pode dimensionar um aplicativo dentro do limite de núcleos para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="4ca0f-117">Por exemplo, digamos que sua assinatura tenha um limite de 20 núcleos.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="4ca0f-118">Ao executar um aplicativo com dois serviços de nuvem de tamanho médio (um total de quatro núcleos), você poderá escalar verticalmente outras implantações de serviço de nuvem na sua assinatura pelos 16 núcleos restantes.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="4ca0f-119">Para saber mais sobre os tamanhos, confira [Tamanhos do Serviço de Nuvem](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="4ca0f-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="4ca0f-120">Você deve criar uma fila e associá-la a uma função antes de dimensionar um aplicativo com base em um limite de mensagens.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="4ca0f-121">Para obter mais informações, consulte [Como usar o serviço de armazenamento de fila](../storage/queues/storage-dotnet-how-to-use-queues.md)(a página pode estar em inglês).</span><span class="sxs-lookup"><span data-stu-id="4ca0f-121">For more information, see [How to use the Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="4ca0f-122">Você pode dimensionar recursos vinculados ao seu serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-122">You can scale resources that are linked to your cloud service.</span></span> <span data-ttu-id="4ca0f-123">Para obter mais informações sobre a vinculação de recursos, consulte [Como vincular um recurso a um serviço de nuvem](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="4ca0f-123">For more information about linking resources, see [How to: Link a resource to a cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="4ca0f-124">Para habilitar a alta disponibilidade do seu aplicativo, você deverá garantir que ele esteja implantado com duas ou mais instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-124">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="4ca0f-125">Para obter mais informações, consulte [Contratos de Nível de Serviço](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="4ca0f-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="4ca0f-126">Agendar o dimensionamento</span><span class="sxs-lookup"><span data-stu-id="4ca0f-126">Schedule scaling</span></span>
<span data-ttu-id="4ca0f-127">Por padrão, nenhuma função segue um agendamento específico.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="4ca0f-128">Portanto, qualquer configuração alterada será aplicada a todos os horários e a todos os dias durante o ano.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-128">Therefore, any settings changed apply to all times and all days throughout the year.</span></span> <span data-ttu-id="4ca0f-129">Se desejar, você poderá configurar a colocação em escala manual ou automática para um dos modos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4ca0f-129">If you want, you can setup manual or automatic scaling for one of the following modes:</span></span>

* <span data-ttu-id="4ca0f-130">Dias da semana</span><span class="sxs-lookup"><span data-stu-id="4ca0f-130">Weekdays</span></span>
* <span data-ttu-id="4ca0f-131">Finais de semana</span><span class="sxs-lookup"><span data-stu-id="4ca0f-131">Weekends</span></span>
* <span data-ttu-id="4ca0f-132">Noites da semana</span><span class="sxs-lookup"><span data-stu-id="4ca0f-132">Week nights</span></span>
* <span data-ttu-id="4ca0f-133">Manhãs da semana</span><span class="sxs-lookup"><span data-stu-id="4ca0f-133">Week mornings</span></span>
* <span data-ttu-id="4ca0f-134">Datas específicas</span><span class="sxs-lookup"><span data-stu-id="4ca0f-134">Specific dates</span></span>
* <span data-ttu-id="4ca0f-135">Intervalos de datas específicos</span><span class="sxs-lookup"><span data-stu-id="4ca0f-135">Specific date ranges</span></span>

<span data-ttu-id="4ca0f-136">A definição da agenda está configurada no [Portal Clássico do Azure](https://manage.windowsazure.com/), na página</span><span class="sxs-lookup"><span data-stu-id="4ca0f-136">The schedule setting is configured in the [Azure classic portal](https://manage.windowsazure.com/) on the</span></span>  
<span data-ttu-id="4ca0f-137">**Serviços de Nuvem** > **\[Seu serviço de nuvem\]** > **Escala** > **\[Produção ou preparo\]**.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="4ca0f-138">Clique no botão **configurar horas agendadas** para cada função que você deseja alterar.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-138">Click the **set up schedule times** button for each role you want to change.</span></span>

![Dimensionamento automático do serviço de nuvem baseado em uma agenda][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="4ca0f-140">Dimensionamento manual</span><span class="sxs-lookup"><span data-stu-id="4ca0f-140">Manual scale</span></span>
<span data-ttu-id="4ca0f-141">Na página **Escala** , você pode aumentar ou diminuir manualmente o número de instâncias em execução em um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-141">On the **Scale** page, you can manually increase or decrease the number of running instances in a cloud service.</span></span> <span data-ttu-id="4ca0f-142">Essa configuração será definida para cada agenda criada ou para todos os horários, se você não tiver criado uma agenda.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-142">This setting is configured for each schedule you've created or to all time if you have not created a schedule.</span></span>

1. <span data-ttu-id="4ca0f-143">No [portal clássico do Azure](https://manage.windowsazure.com/), clique em **Serviços de Nuvem**e no nome do Serviço de Nuvem para abrir o painel.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-143">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="4ca0f-144">Se você não vir seu serviço de nuvem, talvez seja necessário alterar de **Produção** para **Preparo** ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-144">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="4ca0f-145">Clique em **Escala**.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-145">Click **Scale**.</span></span>
3. <span data-ttu-id="4ca0f-146">Escolha a agenda para a qual você deseja alterar as opções de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-146">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="4ca0f-147">O padrão será *Nenhum horário agendado*, se você não tiver agendas definidas.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-147">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="4ca0f-148">Encontre a seção **Dimensionar por métrica** e escolha **NENHUMA**.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-148">Find the **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="4ca0f-149">Essa é a configuração padrão para todas as funções.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-149">This setting is the default for all roles.</span></span>
5. <span data-ttu-id="4ca0f-150">Cada função no Serviço de Nuvem tem um controle deslizante para alterar o número de instâncias a serem usadas.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-150">Each role in the cloud service has a slider for changing the number of instances to use.</span></span>
   
    ![Dimensionar manualmente uma função de serviço de nuvem][manual_scale]
   
    <span data-ttu-id="4ca0f-152">Se você precisar de mais instâncias, talvez seja necessário alterar o [tamanho da máquina virtual do serviço de nuvem](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="4ca0f-152">If you need more instances, you may need to change the [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="4ca0f-153">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-153">Click **Save**.</span></span>  
   <span data-ttu-id="4ca0f-154">As instâncias de função são adicionadas ou removidas com base nas suas seleções.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="4ca0f-155">Sempre que você vir ![][tip_icon], mova o mouse até ele e obtenha ajuda sobre a função de uma configuração específica.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-155">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="4ca0f-156">Dimensionamento automático - CPU</span><span class="sxs-lookup"><span data-stu-id="4ca0f-156">Automatic scale - CPU</span></span>
<span data-ttu-id="4ca0f-157">Esse modo será dimensionado se o percentual médio do uso da CPU ficar acima ou abaixo dos limites especificados.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-157">This mode scales if the average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="4ca0f-158">As instâncias de função são criadas ou excluídas quando isso acontece.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="4ca0f-159">No [portal clássico do Azure](https://manage.windowsazure.com/), clique em **Serviços de Nuvem**e no nome do Serviço de Nuvem para abrir o painel.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-159">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="4ca0f-160">Se você não vir seu serviço de nuvem, talvez seja necessário alterar de **Produção** para **Preparo** ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-160">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="4ca0f-161">Clique em **Escala**.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-161">Click **Scale**.</span></span>
3. <span data-ttu-id="4ca0f-162">Escolha a agenda para a qual você deseja alterar as opções de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-162">Select the schedule you want to change scaling options for.</span></span> <span data-ttu-id="4ca0f-163">O padrão será *Nenhum horário agendado*, se você não tiver agendas definidas.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-163">*No scheduled times* is the default if you have no schedules defined.</span></span>
4. <span data-ttu-id="4ca0f-164">Encontre a seção **Dimensionar por métrica** e selecione **CPU**.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-164">Find the **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="4ca0f-165">Agora você pode configurar um intervalo mínimo e máximo de instâncias de função, o uso da CPU de destino (para disparar um escalonamento vertical) e quantas instâncias para escalonar vertical ou horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-165">Now you can configure a minimum and maximum range of roles instances, the target CPU usage (to trigger a scale up), and how many instances to scale up and down by.</span></span>

![Dimensionar uma função de serviço de nuvem por carga de cpu][cpu_scale]

> [!TIP]
> <span data-ttu-id="4ca0f-167">Sempre que você vir ![][tip_icon], mova o mouse até ele e obtenha ajuda sobre a função de uma configuração específica.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-167">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="4ca0f-168">Dimensionamento automático - fila</span><span class="sxs-lookup"><span data-stu-id="4ca0f-168">Automatic scale - Queue</span></span>
<span data-ttu-id="4ca0f-169">Esse modo será dimensionado automaticamente se o número de mensagens em uma fila estiver acima ou abaixo do limite especificado.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-169">This mode automatically scales if the number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="4ca0f-170">As instâncias de função são criadas ou excluídas quando isso acontece.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="4ca0f-171">No [portal clássico do Azure](https://manage.windowsazure.com/), clique em **Serviços de Nuvem**e no nome do Serviço de Nuvem para abrir o painel.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-171">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="4ca0f-172">Se você não vir seu serviço de nuvem, talvez seja necessário alterar de **Produção** para **Preparo** ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-172">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="4ca0f-173">Clique em **Escala**.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-173">Click **Scale**.</span></span>
3. <span data-ttu-id="4ca0f-174">Encontre a seção **Dimensionar por métrica** e selecione **FILA**.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-174">Find the **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="4ca0f-175">Agora você pode configurar um intervalo mínimo e máximo de instâncias de função, a fila e o número de mensagens de filas a serem processadas para cada instância e quantas instâncias devem ser escaladas vertical ou horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-175">Now you can configure a minimum and maximum range of roles instances, the queue and number of queue messages to process for each instance, and how many instances to scale up and down by.</span></span>

![Dimensionar uma função de serviço de nuvem por fila de mensagens][queue_scale]

> [!TIP]
> <span data-ttu-id="4ca0f-177">Sempre que você vir ![][tip_icon], mova o mouse até ele e obtenha ajuda sobre a função de uma configuração específica.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-177">Whenever you see ![][tip_icon] move your mouse to it and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="4ca0f-178">Dimensionar recursos vinculados</span><span class="sxs-lookup"><span data-stu-id="4ca0f-178">Scale linked resources</span></span>
<span data-ttu-id="4ca0f-179">Sempre que você dimensionar uma função, também é benéfico dimensionar o banco de dados que o aplicativo está usando.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-179">Often when you scale a role, it's beneficial to scale the database that the application is using also.</span></span> <span data-ttu-id="4ca0f-180">Se vincular o banco de dados ao serviço de nuvem, você poderá acessar as configurações de colocação em escala para esse recurso clicando no link apropriado.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-180">If you link the database to the cloud service, you can access the scaling settings for that resource by clicking the appropriate link.</span></span>

1. <span data-ttu-id="4ca0f-181">No [portal clássico do Azure](https://manage.windowsazure.com/), clique em **Serviços de Nuvem**e no nome do Serviço de Nuvem para abrir o painel.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-181">In the [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click the name of the cloud service to open the dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="4ca0f-182">Se você não vir seu serviço de nuvem, talvez seja necessário alterar de **Produção** para **Preparo** ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-182">If you don't see your cloud service, you may need to change from **Production** to **Staging** or vice versa.</span></span>

2. <span data-ttu-id="4ca0f-183">Clique em **Escala**.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-183">Click **Scale**.</span></span>
3. <span data-ttu-id="4ca0f-184">Encontre a seção **recursos vinculados** e clique em **Gerenciar dimensionamento para este banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-184">Find the **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4ca0f-185">Caso você não veja uma seção **recursos vinculados** , é provável que você não tenha recursos vinculados.</span><span class="sxs-lookup"><span data-stu-id="4ca0f-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
