---
title: "aaaAuto dimensionar um serviço de nuvem no portal de saudação | Microsoft Docs"
description: "Saiba como toouse Olá tooconfigure portal regras de escala automática para uma função de web do serviço de nuvem ou uma função de trabalho no Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a><span data-ttu-id="bba25-103">Como tooconfigure automaticamente a escala para um serviço de nuvem no portal de saudação</span><span class="sxs-lookup"><span data-stu-id="bba25-103">How tooconfigure auto scaling for a Cloud Service in hello portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bba25-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bba25-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="bba25-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="bba25-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="bba25-106">As condições podem ser definidas para uma função de trabalho de serviço de nuvem que dispara uma operação para reduzir ou escalar horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="bba25-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="bba25-107">condições de saudação para função hello podem se basear Olá CPU, disco ou da função de saudação de carga de rede.</span><span class="sxs-lookup"><span data-stu-id="bba25-107">hello conditions for hello role can be based on hello CPU, disk, or network load of hello role.</span></span> <span data-ttu-id="bba25-108">Você também pode definir uma condição com base na métrica de fila ou hello mensagem de alguns outros recursos do Azure associado à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="bba25-108">You can also set a condition based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="bba25-109">Este artigo se concentra nas funções Web e de trabalho do Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="bba25-109">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="bba25-110">Ao criar uma máquina virtual (modelo clássico) diretamente, ela será hospedada em um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="bba25-110">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="bba25-111">Você pode dimensionar uma máquina virtual padrão ao associá-la a um [conjunto de disponibilidade](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) e ligá-los ou desligá-los manualmente.</span><span class="sxs-lookup"><span data-stu-id="bba25-111">You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.</span></span>

## <a name="considerations"></a><span data-ttu-id="bba25-112">Considerações</span><span class="sxs-lookup"><span data-stu-id="bba25-112">Considerations</span></span>
<span data-ttu-id="bba25-113">Você deve considerar Olá informações a seguir antes de configurar o dimensionamento para seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="bba25-113">You should consider hello following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="bba25-114">A colocação em escala é afetada pelo uso de núcleo.</span><span class="sxs-lookup"><span data-stu-id="bba25-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="bba25-115">As instâncias de função maiores usam mais núcleos.</span><span class="sxs-lookup"><span data-stu-id="bba25-115">Larger role instances use more cores.</span></span> <span data-ttu-id="bba25-116">Você pode dimensionar um aplicativo somente no limite de saudação de núcleos para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="bba25-116">You can scale an application only within hello limit of cores for your subscription.</span></span> <span data-ttu-id="bba25-117">Por exemplo, digamos que sua assinatura tenha um limite de 20 núcleos.</span><span class="sxs-lookup"><span data-stu-id="bba25-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="bba25-118">Se você executar um aplicativo com dois serviços de nuvem de médio porte (um total de 4 núcleos), você somente poderá expandir outras implantações de serviço de nuvem em sua assinatura por 16 núcleos de saudação restantes.</span><span class="sxs-lookup"><span data-stu-id="bba25-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by hello remaining 16 cores.</span></span> <span data-ttu-id="bba25-119">Para saber mais sobre os tamanhos, confira [Tamanhos do Serviço de Nuvem](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="bba25-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="bba25-120">Você pode dimensionar com base em um limite de mensagens da fila.</span><span class="sxs-lookup"><span data-stu-id="bba25-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="bba25-121">Para obter mais informações sobre como toouse filas, consulte [como toouse Olá serviço de armazenamento de fila](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="bba25-121">For more information about how toouse queues, see [How toouse hello Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="bba25-122">Você também pode dimensionar outros recursos associados à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="bba25-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="bba25-123">tooenable alta disponibilidade do seu aplicativo, você deve garantir que ele seja implantado com duas ou mais instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="bba25-123">tooenable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="bba25-124">Para obter mais informações, consulte [Contratos de Nível de Serviço](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="bba25-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>


## <a name="where-scale-is-located"></a><span data-ttu-id="bba25-125">Onde a escala está localizada</span><span class="sxs-lookup"><span data-stu-id="bba25-125">Where scale is located</span></span>
<span data-ttu-id="bba25-126">Depois de selecionar o serviço de nuvem, você deve ter folha de serviço de nuvem de saudação visível.</span><span class="sxs-lookup"><span data-stu-id="bba25-126">After you select your cloud service, you should have hello cloud service blade visible.</span></span>

1. <span data-ttu-id="bba25-127">Na folha de serviço de nuvem hello, em Olá **funções e instâncias** lado a lado, o nome de select Olá Olá do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="bba25-127">On hello cloud service blade, on hello **Roles and Instances** tile, select hello name of hello cloud service.</span></span>   
   <span data-ttu-id="bba25-128">**IMPORTANTE**: tornar-se de que tooclick Olá função de serviço, não Olá instância de função que está abaixo da função hello.</span><span class="sxs-lookup"><span data-stu-id="bba25-128">**IMPORTANT**: Make sure tooclick hello cloud service role, not hello role instance that is below hello role.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="bba25-129">Selecione Olá **escala** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="bba25-129">Select hello **scale** tile.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="bba25-130">Escala automática</span><span class="sxs-lookup"><span data-stu-id="bba25-130">Automatic scale</span></span>
<span data-ttu-id="bba25-131">Você pode definir as configurações de escala para uma função com o modo **manual** ou **automático**.</span><span class="sxs-lookup"><span data-stu-id="bba25-131">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="bba25-132">Manual é conforme o esperado, você definir número absoluto de Olá de instâncias.</span><span class="sxs-lookup"><span data-stu-id="bba25-132">Manual is as you would expect, you set hello absolute count of instances.</span></span> <span data-ttu-id="bba25-133">Automático porém permite tooset regras que controlam como e por como muito você deverá fazer o dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="bba25-133">Automatic however allows you tooset rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="bba25-134">Saudação de conjunto **o dimensionamento por** opção muito**regras de agendamento e desempenho**.</span><span class="sxs-lookup"><span data-stu-id="bba25-134">Set hello **Scale by** option too**schedule and performance rules**.</span></span>

![Escala dos serviços de nuvem com perfil e regra](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="bba25-136">Um perfil existente.</span><span class="sxs-lookup"><span data-stu-id="bba25-136">An existing profile.</span></span>
2. <span data-ttu-id="bba25-137">Adicione uma regra para o perfil do hello pai.</span><span class="sxs-lookup"><span data-stu-id="bba25-137">Add a rule for hello parent profile.</span></span>
3. <span data-ttu-id="bba25-138">Adicione outro perfil.</span><span class="sxs-lookup"><span data-stu-id="bba25-138">Add another profile.</span></span>

<span data-ttu-id="bba25-139">Selecione **Adicionar Perfil**.</span><span class="sxs-lookup"><span data-stu-id="bba25-139">Select **Add Profile**.</span></span> <span data-ttu-id="bba25-140">perfil Hello determina qual modo você deseja toouse para escala Olá: **sempre**, **recorrência**, **data fixa**.</span><span class="sxs-lookup"><span data-stu-id="bba25-140">hello profile determines which mode you want toouse for hello scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="bba25-141">Depois que você configurou o perfil de saudação e regras, selecione Olá **salvar** no hello superior.</span><span class="sxs-lookup"><span data-stu-id="bba25-141">After you have configured hello profile and rules, select hello **Save** icon at hello top.</span></span>

#### <a name="profile"></a><span data-ttu-id="bba25-142">Perfil</span><span class="sxs-lookup"><span data-stu-id="bba25-142">Profile</span></span>
<span data-ttu-id="bba25-143">mínimo de conjuntos de perfis de saudação e escala de instâncias máxima para hello e também quando esse intervalo de escala está ativo.</span><span class="sxs-lookup"><span data-stu-id="bba25-143">hello profile sets minimum and maximum instances for hello scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="bba25-144">**Sempre**</span><span class="sxs-lookup"><span data-stu-id="bba25-144">**Always**</span></span>

    <span data-ttu-id="bba25-145">Sempre mantenha esse intervalo de instâncias disponível.</span><span class="sxs-lookup"><span data-stu-id="bba25-145">Always keep this range of instances available.</span></span>  

    ![Serviço de nuvem que sempre dimensiona](./media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="bba25-147">**Recorrência**</span><span class="sxs-lookup"><span data-stu-id="bba25-147">**Recurrence**</span></span>

    <span data-ttu-id="bba25-148">Escolha um conjunto de dias de saudação semana tooscale.</span><span class="sxs-lookup"><span data-stu-id="bba25-148">Choose a set of days of hello week tooscale.</span></span>

    ![Escala de serviço de nuvem com um agendamento de recorrência](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="bba25-150">**Data Fixa**</span><span class="sxs-lookup"><span data-stu-id="bba25-150">**Fixed Date**</span></span>

    <span data-ttu-id="bba25-151">Uma função de saudação do data fixa intervalo tooscale.</span><span class="sxs-lookup"><span data-stu-id="bba25-151">A fixed date range tooscale hello role.</span></span>

    ![Escala de serviço de nuvem com uma data fixa](./media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="bba25-153">Depois de configurar o perfil de saudação, selecione Olá **Okey** botão na parte inferior da saudação da folha de perfil de saudação.</span><span class="sxs-lookup"><span data-stu-id="bba25-153">After you have configured hello profile, select hello **OK** button at hello bottom of hello profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="bba25-154">Regra</span><span class="sxs-lookup"><span data-stu-id="bba25-154">Rule</span></span>
<span data-ttu-id="bba25-155">As regras são adicionadas tooa perfil e representam uma condição que dispara a escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="bba25-155">Rules are added tooa profile and represent a condition that triggers hello scale.</span></span>

<span data-ttu-id="bba25-156">gatilho de regra Olá baseia-se uma métrica de saudação do serviço de nuvem (utilização da CPU, atividade de disco ou atividade de rede) toowhich, você pode adicionar um valor condicional.</span><span class="sxs-lookup"><span data-stu-id="bba25-156">hello rule trigger is based on a metric of hello cloud service (CPU usage, disk activity, or network activity) toowhich you can add a conditional value.</span></span> <span data-ttu-id="bba25-157">Além disso, você pode ter gatilho Olá com base em uma métrica de saudação ou fila de mensagem de alguns outros recursos do Azure associado à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="bba25-157">Additionally you can have hello trigger based on a message queue or hello metric of some other Azure resource associated with your subscription.</span></span>

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="bba25-158">Depois de configurar a regra de saudação, selecione Olá **Okey** botão na parte inferior da saudação da folha de regra de saudação.</span><span class="sxs-lookup"><span data-stu-id="bba25-158">After you have configured hello rule, select hello **OK** button at hello bottom of hello rule blade.</span></span>

## <a name="back-toomanual-scale"></a><span data-ttu-id="bba25-159">Escala de toomanual back</span><span class="sxs-lookup"><span data-stu-id="bba25-159">Back toomanual scale</span></span>
<span data-ttu-id="bba25-160">Navegue toohello [as configurações de escala](#where-scale-is-located) e conjunto hello **o dimensionamento por** opção muito**uma contagem de instâncias que inseri manualmente**.</span><span class="sxs-lookup"><span data-stu-id="bba25-160">Navigate toohello [scale settings](#where-scale-is-located) and set hello **Scale by** option too**an instance count that I enter manually**.</span></span>

![Escala dos serviços de nuvem com perfil e regra](./media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="bba25-162">Essa configuração remove o dimensionamento automatizadas de função hello e, em seguida, você pode definir a contagem de instâncias Olá diretamente.</span><span class="sxs-lookup"><span data-stu-id="bba25-162">This setting removes automated scaling from hello role and then you can set hello instance count directly.</span></span>

1. <span data-ttu-id="bba25-163">opção de escala (manual ou automatizada) do Hello.</span><span class="sxs-lookup"><span data-stu-id="bba25-163">hello scale (manual or automated) option.</span></span>
2. <span data-ttu-id="bba25-164">Uma saudação tooset de controle deslizante de instância de função tooscale para as instâncias.</span><span class="sxs-lookup"><span data-stu-id="bba25-164">A role instance slider tooset hello instances tooscale to.</span></span>
3. <span data-ttu-id="bba25-165">Instâncias de saudação função tooscale para.</span><span class="sxs-lookup"><span data-stu-id="bba25-165">Instances of hello role tooscale to.</span></span>

<span data-ttu-id="bba25-166">Depois de configurar as configurações de dimensionamento hello, selecione Olá **salvar** no hello superior.</span><span class="sxs-lookup"><span data-stu-id="bba25-166">After you have configured hello scale settings, select hello **Save** icon at hello top.</span></span>
