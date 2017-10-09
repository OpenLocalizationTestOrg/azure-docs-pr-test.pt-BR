---
title: "aaaAuto dimensionar um serviço de nuvem no portal clássico Olá | Microsoft Docs"
description: "(clássico) Saiba como toouse Olá tooconfigure portal clássico regras de escala automática para uma função de web do serviço de nuvem ou uma função de trabalho no Azure."
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
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a><span data-ttu-id="8502d-103">Como tooconfigure automaticamente a escala para um serviço de nuvem no portal clássico Olá</span><span class="sxs-lookup"><span data-stu-id="8502d-103">How tooconfigure auto scaling for a Cloud Service in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8502d-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8502d-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="8502d-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="8502d-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="8502d-106">Na página de escala de saudação do hello portal clássico do Azure, você pode configurar as configurações de dimensionamento automático para sua função web ou função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8502d-106">On hello Scale page of hello Azure classic portal, you can configure automatic scale settings for your web role or worker role.</span></span> <span data-ttu-id="8502d-107">Como alternativa, você pode configurar a colocação em escala manual em vez da colocação em escala automática com base em regras.</span><span class="sxs-lookup"><span data-stu-id="8502d-107">Alternatively, you can configure manual scaling instead of rules-based automatic scaling.</span></span>

> [!NOTE]
> <span data-ttu-id="8502d-108">Este artigo se concentra nas funções Web e de trabalho do Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="8502d-108">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="8502d-109">Ao criar uma máquina virtual (modelo clássico) diretamente, ela será hospedada em um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="8502d-109">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="8502d-110">Algumas dessas informações se aplica a tipos de toothese de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="8502d-110">Some of this information applies toothese types of virtual machines.</span></span> <span data-ttu-id="8502d-111">Dimensionamento de um conjunto de disponibilidade das máquinas virtuais é apenas sendo-los e desativar com base nas regras de escala Olá configurados.</span><span class="sxs-lookup"><span data-stu-id="8502d-111">Scaling an availability set of virtual machines is just shutting them on and off based on hello scale rules you configure.</span></span> <span data-ttu-id="8502d-112">Para obter mais informações sobre máquinas virtuais e conjuntos de disponibilidade, consulte [gerenciar Olá disponibilidade das máquinas virtuais](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="8502d-112">For more information about Virtual Machines and availability sets, see [Manage hello Availability of Virtual Machines](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="8502d-113">Você deve considerar Olá informações a seguir antes de configurar o dimensionamento para seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="8502d-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="8502d-114">A colocação em escala é afetada pelo uso de núcleo.</span><span class="sxs-lookup"><span data-stu-id="8502d-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="8502d-115">As instâncias de função maiores usam mais núcleos.</span><span class="sxs-lookup"><span data-stu-id="8502d-115">Larger role instances use more cores.</span></span> <span data-ttu-id="8502d-116">Você pode dimensionar um aplicativo somente no limite de saudação de núcleos para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="8502d-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="8502d-117">Por exemplo, digamos que sua assinatura tenha um limite de 20 núcleos.</span><span class="sxs-lookup"><span data-stu-id="8502d-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="8502d-118">Se você executar um aplicativo com dois serviços de nuvem de médio porte (um total de 4 núcleos), você somente poderá expandir outras implantações de serviço de nuvem em sua assinatura por 16 núcleos de saudação restantes.</span><span class="sxs-lookup"><span data-stu-id="8502d-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="8502d-119">Para saber mais sobre os tamanhos, confira [Tamanhos do Serviço de Nuvem](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="8502d-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="8502d-120">Você deve criar uma fila e associá-la a uma função antes de dimensionar um aplicativo com base em um limite de mensagens.</span><span class="sxs-lookup"><span data-stu-id="8502d-120">You must create a queue and associate it with a role before you can scale an application based on a message threshold.</span></span> <span data-ttu-id="8502d-121">Para obter mais informações, consulte [como toouse Olá serviço de armazenamento de fila](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="8502d-121">For more information, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="8502d-122">Você pode dimensionar os recursos que estão vinculado tooyour serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="8502d-122">You can scale resources that are linked tooyour cloud service.</span></span> <span data-ttu-id="8502d-123">Para obter mais informações sobre a vinculação de recursos, consulte [como: vincular a um serviço de nuvem do recurso tooa](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="8502d-123">For more information about linking resources, see [How to: Link a resource tooa cloud service](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).</span></span>

* <span data-ttu-id="8502d-124">tooenable alta disponibilidade do seu aplicativo, você deve garantir que ele seja implantado com duas ou mais instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="8502d-124">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="8502d-125">Para obter mais informações, consulte [Contratos de Nível de Serviço](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="8502d-125">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="schedule-scaling"></a><span data-ttu-id="8502d-126">Agendar o dimensionamento</span><span class="sxs-lookup"><span data-stu-id="8502d-126">Schedule scaling</span></span>
<span data-ttu-id="8502d-127">Por padrão, nenhuma função segue um agendamento específico.</span><span class="sxs-lookup"><span data-stu-id="8502d-127">By default, all roles do not follow a specific schedule.</span></span> <span data-ttu-id="8502d-128">Portanto, quaisquer configurações alteradas aplicam tooall vezes e todos os dias durante o ano de saudação.</span><span class="sxs-lookup"><span data-stu-id="8502d-128">Therefore, any settings changed apply tooall times and all days throughout hello year.</span></span> <span data-ttu-id="8502d-129">Se desejar, você pode configurar a expansão do manual ou automática para um dos modos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="8502d-129">If you want, you can setup manual or automatic scaling for one of hello following modes:</span></span>

* <span data-ttu-id="8502d-130">Dias da semana</span><span class="sxs-lookup"><span data-stu-id="8502d-130">Weekdays</span></span>
* <span data-ttu-id="8502d-131">Finais de semana</span><span class="sxs-lookup"><span data-stu-id="8502d-131">Weekends</span></span>
* <span data-ttu-id="8502d-132">Noites da semana</span><span class="sxs-lookup"><span data-stu-id="8502d-132">Week nights</span></span>
* <span data-ttu-id="8502d-133">Manhãs da semana</span><span class="sxs-lookup"><span data-stu-id="8502d-133">Week mornings</span></span>
* <span data-ttu-id="8502d-134">Datas específicas</span><span class="sxs-lookup"><span data-stu-id="8502d-134">Specific dates</span></span>
* <span data-ttu-id="8502d-135">Intervalos de datas específicos</span><span class="sxs-lookup"><span data-stu-id="8502d-135">Specific date ranges</span></span>

<span data-ttu-id="8502d-136">Olá agenda está definida no hello [portal clássico do Azure](https://manage.windowsazure.com/) em Olá</span><span class="sxs-lookup"><span data-stu-id="8502d-136">hello schedule setting is configured in hello [Azure classic portal](https://manage.windowsazure.com/) on hello</span></span>  
<span data-ttu-id="8502d-137">**Serviços de Nuvem** > **\[Seu serviço de nuvem\]** > **Escala** > **\[Produção ou preparo\]**.</span><span class="sxs-lookup"><span data-stu-id="8502d-137">**Cloud Services** > **\[Your cloud service\]** > **Scale** > **\[Production or Staging\]** page.</span></span>

<span data-ttu-id="8502d-138">Clique em Olá **configurar horas agendadas** botão para cada função você deseja toochange.</span><span class="sxs-lookup"><span data-stu-id="8502d-138">Click hello **set up schedule times** button for each role you want toochange.</span></span>

![Dimensionamento automático do serviço de nuvem baseado em uma agenda][scale_schedules]

## <a name="manual-scale"></a><span data-ttu-id="8502d-140">Dimensionamento manual</span><span class="sxs-lookup"><span data-stu-id="8502d-140">Manual scale</span></span>
<span data-ttu-id="8502d-141">Em Olá **escala** página, você pode manualmente aumentar ou diminuir o número de saudação de instâncias em execução em um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="8502d-141">On hello **Scale** page, you can manually increase or decrease hello number of running instances in a cloud service.</span></span> <span data-ttu-id="8502d-142">Essa configuração é definida para cada agenda que você criou ou tooall tempo se você não tiver criado uma agenda.</span><span class="sxs-lookup"><span data-stu-id="8502d-142">This setting is configured for each schedule you've created or tooall time if you have not created a schedule.</span></span>

1. <span data-ttu-id="8502d-143">Em Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços de nuvem**e, em seguida, clique em nome Olá Olá nuvem tooopen Olá de painel de serviço.</span><span class="sxs-lookup"><span data-stu-id="8502d-143">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="8502d-144">Se você não vir o serviço de nuvem, talvez seja necessário toochange de **produção** muito**preparo** ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="8502d-144">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="8502d-145">Clique em **Escala**.</span><span class="sxs-lookup"><span data-stu-id="8502d-145">Click **Scale**.</span></span>
3. <span data-ttu-id="8502d-146">Selecione a agenda de saudação desejado toochange opções de dimensionamento para.</span><span class="sxs-lookup"><span data-stu-id="8502d-146">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="8502d-147">*Não horários agendados* é o padrão de saudação se você não tiver nenhuma agenda foi definida.</span><span class="sxs-lookup"><span data-stu-id="8502d-147">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="8502d-148">Localize Olá **escala por métrica** seção e selecione **NONE**.</span><span class="sxs-lookup"><span data-stu-id="8502d-148">Find hello **Scale by metric** section and select **NONE**.</span></span> <span data-ttu-id="8502d-149">Essa configuração é o padrão de saudação para todas as funções.</span><span class="sxs-lookup"><span data-stu-id="8502d-149">This setting is hello default for all roles.</span></span>
5. <span data-ttu-id="8502d-150">Cada função no serviço de nuvem Olá tem um controle deslizante para alterar o número de saudação do toouse de instâncias.</span><span class="sxs-lookup"><span data-stu-id="8502d-150">Each role in hello cloud service has a slider for changing hello number of instances toouse.</span></span>
   
    ![Dimensionar manualmente uma função de serviço de nuvem][manual_scale]
   
    <span data-ttu-id="8502d-152">Se você precisar de mais instâncias, talvez seja necessário Olá toochange [tamanho da máquina virtual de serviço de nuvem](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="8502d-152">If you need more instances, you may need toochange hello [cloud service virtual machine size](cloud-services-sizes-specs.md).</span></span>
6. <span data-ttu-id="8502d-153">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8502d-153">Click **Save**.</span></span>  
   <span data-ttu-id="8502d-154">As instâncias de função são adicionadas ou removidas com base nas suas seleções.</span><span class="sxs-lookup"><span data-stu-id="8502d-154">Role instances are added or removed based on your selections.</span></span>

> [!TIP]
> <span data-ttu-id="8502d-155">Sempre que você vir ![][tip_icon] mova seu mouse tooit e você pode obter ajuda sobre o que é uma configuração específica.</span><span class="sxs-lookup"><span data-stu-id="8502d-155">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---cpu"></a><span data-ttu-id="8502d-156">Dimensionamento automático - CPU</span><span class="sxs-lookup"><span data-stu-id="8502d-156">Automatic scale - CPU</span></span>
<span data-ttu-id="8502d-157">Esse modo pode ser dimensionado se a porcentagem média de saudação do uso de CPU fica acima ou abaixo os limites especificados.</span><span class="sxs-lookup"><span data-stu-id="8502d-157">This mode scales if hello average percentage of CPU usage goes above or below specified thresholds.</span></span> <span data-ttu-id="8502d-158">As instâncias de função são criadas ou excluídas quando isso acontece.</span><span class="sxs-lookup"><span data-stu-id="8502d-158">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="8502d-159">Em Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços de nuvem**e, em seguida, clique em nome Olá Olá nuvem tooopen Olá de painel de serviço.</span><span class="sxs-lookup"><span data-stu-id="8502d-159">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="8502d-160">Se você não vir o serviço de nuvem, talvez seja necessário toochange de **produção** muito**preparo** ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="8502d-160">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="8502d-161">Clique em **Escala**.</span><span class="sxs-lookup"><span data-stu-id="8502d-161">Click **Scale**.</span></span>
3. <span data-ttu-id="8502d-162">Selecione a agenda de saudação desejado toochange opções de dimensionamento para.</span><span class="sxs-lookup"><span data-stu-id="8502d-162">Select hello schedule you want toochange scaling options for.</span></span> <span data-ttu-id="8502d-163">*Não horários agendados* é o padrão de saudação se você não tiver nenhuma agenda foi definida.</span><span class="sxs-lookup"><span data-stu-id="8502d-163">*No scheduled times* is hello default if you have no schedules defined.</span></span>
4. <span data-ttu-id="8502d-164">Localize Olá **escala por métrica** seção e selecione **CPU**.</span><span class="sxs-lookup"><span data-stu-id="8502d-164">Find hello **Scale by metric** section and select **CPU**.</span></span>
5. <span data-ttu-id="8502d-165">Agora você pode configurar um intervalo mínimo e máximo de instâncias de função, o uso de CPU de destino de hello (tootrigger a expansão vertical) e quantas instâncias tooscale ativo e inativo por.</span><span class="sxs-lookup"><span data-stu-id="8502d-165">Now you can configure a minimum and maximum range of roles instances, hello target CPU usage (tootrigger a scale up), and how many instances tooscale up and down by.</span></span>

![Dimensionar uma função de serviço de nuvem por carga de cpu][cpu_scale]

> [!TIP]
> <span data-ttu-id="8502d-167">Sempre que você vir ![][tip_icon] mova seu mouse tooit e você pode obter ajuda sobre o que é uma configuração específica.</span><span class="sxs-lookup"><span data-stu-id="8502d-167">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="automatic-scale---queue"></a><span data-ttu-id="8502d-168">Dimensionamento automático - fila</span><span class="sxs-lookup"><span data-stu-id="8502d-168">Automatic scale - Queue</span></span>
<span data-ttu-id="8502d-169">Esse modo dimensiona automaticamente se o número de saudação de mensagens em uma fila fica acima ou abaixo do limite especificado.</span><span class="sxs-lookup"><span data-stu-id="8502d-169">This mode automatically scales if hello number of messages in a queue goes above or below a specified threshold.</span></span> <span data-ttu-id="8502d-170">As instâncias de função são criadas ou excluídas quando isso acontece.</span><span class="sxs-lookup"><span data-stu-id="8502d-170">Role instances are created or deleted when this happens.</span></span>

1. <span data-ttu-id="8502d-171">Em Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços de nuvem**e, em seguida, clique em nome Olá Olá nuvem tooopen Olá de painel de serviço.</span><span class="sxs-lookup"><span data-stu-id="8502d-171">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="8502d-172">Se você não vir o serviço de nuvem, talvez seja necessário toochange de **produção** muito**preparo** ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="8502d-172">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="8502d-173">Clique em **Escala**.</span><span class="sxs-lookup"><span data-stu-id="8502d-173">Click **Scale**.</span></span>
3. <span data-ttu-id="8502d-174">Localize Olá **escala por métrica** seção e selecione **fila**.</span><span class="sxs-lookup"><span data-stu-id="8502d-174">Find hello **Scale by metric** section and select **QUEUE**.</span></span>
4. <span data-ttu-id="8502d-175">Agora você pode configurar um intervalo mínimo e máximo de instâncias de funções, fila hello e número de tooprocess de mensagens de fila para cada instância e quantos tooscale de instâncias para cima e para baixo por.</span><span class="sxs-lookup"><span data-stu-id="8502d-175">Now you can configure a minimum and maximum range of roles instances, hello queue and number of queue messages tooprocess for each instance, and how many instances tooscale up and down by.</span></span>

![Dimensionar uma função de serviço de nuvem por fila de mensagens][queue_scale]

> [!TIP]
> <span data-ttu-id="8502d-177">Sempre que você vir ![][tip_icon] mova seu mouse tooit e você pode obter ajuda sobre o que é uma configuração específica.</span><span class="sxs-lookup"><span data-stu-id="8502d-177">Whenever you see ![][tip_icon] move your mouse tooit and you can get help about what a specific setting does.</span></span>

## <a name="scale-linked-resources"></a><span data-ttu-id="8502d-178">Dimensionar recursos vinculados</span><span class="sxs-lookup"><span data-stu-id="8502d-178">Scale linked resources</span></span>
<span data-ttu-id="8502d-179">Muitas vezes, quando você dimensionar uma função, é vantajoso tooscale Olá banco de dados usando o aplicativo hello é também.</span><span class="sxs-lookup"><span data-stu-id="8502d-179">Often when you scale a role, it's beneficial tooscale hello database that hello application is using also.</span></span> <span data-ttu-id="8502d-180">Se você vincular um serviço de nuvem em toohello Olá banco de dados, você pode acessar Olá escala configurações para esse recurso ao clicar no link apropriado hello.</span><span class="sxs-lookup"><span data-stu-id="8502d-180">If you link hello database toohello cloud service, you can access hello scaling settings for that resource by clicking hello appropriate link.</span></span>

1. <span data-ttu-id="8502d-181">Em Olá [portal clássico do Azure](https://manage.windowsazure.com/), clique em **serviços de nuvem**e, em seguida, clique em nome Olá Olá nuvem tooopen Olá de painel de serviço.</span><span class="sxs-lookup"><span data-stu-id="8502d-181">In hello [Azure classic portal](https://manage.windowsazure.com/), click **Cloud Services**, and then click hello name of hello cloud service tooopen hello dashboard.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="8502d-182">Se você não vir o serviço de nuvem, talvez seja necessário toochange de **produção** muito**preparo** ou vice-versa.</span><span class="sxs-lookup"><span data-stu-id="8502d-182">If you don't see your cloud service, you may need toochange from **Production** too**Staging** or vice versa.</span></span>

2. <span data-ttu-id="8502d-183">Clique em **Escala**.</span><span class="sxs-lookup"><span data-stu-id="8502d-183">Click **Scale**.</span></span>
3. <span data-ttu-id="8502d-184">Localize Olá **recursos vinculados** seção e clique em **gerenciar escala para este banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="8502d-184">Find hello **linked resources** section and click **Manage scale for this database**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8502d-185">Caso você não veja uma seção **recursos vinculados** , é provável que você não tenha recursos vinculados.</span><span class="sxs-lookup"><span data-stu-id="8502d-185">If you don't see a **linked resources** section, you probably do not have any linked resources.</span></span>

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
