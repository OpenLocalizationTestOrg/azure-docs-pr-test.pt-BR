---
title: "Dimensionar automaticamente um serviço de nuvem no portal | Microsoft Docs"
description: "Saiba como usar o portal para configurar regras de dimensionamento automático para uma função web ou função de trabalho do serviço de nuvem no Azure."
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
ms.openlocfilehash: e9683d4c5779450fd67fa42ab13095c7f201b4cd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-auto-scaling-for-a-cloud-service-in-the-portal"></a><span data-ttu-id="a3fdc-103">Como configurar o dimensionamento automático para um Serviço de Nuvem no portal</span><span class="sxs-lookup"><span data-stu-id="a3fdc-103">How to configure auto scaling for a Cloud Service in the portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a3fdc-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a3fdc-104">Azure portal</span></span>](cloud-services-how-to-scale-portal.md)
> * [<span data-ttu-id="a3fdc-105">Portal clássico do Azure</span><span class="sxs-lookup"><span data-stu-id="a3fdc-105">Azure classic portal</span></span>](cloud-services-how-to-scale.md)

<span data-ttu-id="a3fdc-106">As condições podem ser definidas para uma função de trabalho de serviço de nuvem que dispara uma operação para reduzir ou escalar horizontalmente.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-106">Conditions can be set for a cloud service worker role that trigger a scale in or out operation.</span></span> <span data-ttu-id="a3fdc-107">As condições para a função podem ser baseadas na CPU, no disco ou na carga de rede da função.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-107">The conditions for the role can be based on the CPU, disk, or network load of the role.</span></span> <span data-ttu-id="a3fdc-108">Você também pode definir uma condição com base em uma fila de mensagens ou a métrica de algum outro recurso do Azure associado à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-108">You can also set a condition based on a message queue or the metric of some other Azure resource associated with your subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="a3fdc-109">Este artigo se concentra nas funções Web e de trabalho do Serviço de Nuvem.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-109">This article focuses on Cloud Service web and worker roles.</span></span> <span data-ttu-id="a3fdc-110">Ao criar uma máquina virtual (modelo clássico) diretamente, ela será hospedada em um serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-110">When you create a virtual machine (classic) directly, it is hosted in a cloud service.</span></span> <span data-ttu-id="a3fdc-111">Você pode dimensionar uma máquina virtual padrão ao associá-la a um [conjunto de disponibilidade](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) e ligá-los ou desligá-los manualmente.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-111">You can scale a standard virtual machine by associating it with an [availability set](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) and manually turn them on or off.</span></span>

## <a name="considerations"></a><span data-ttu-id="a3fdc-112">Considerações</span><span class="sxs-lookup"><span data-stu-id="a3fdc-112">Considerations</span></span>
<span data-ttu-id="a3fdc-113">Você deve considerar as seguintes informações antes de configurar a colocação em escala do seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="a3fdc-113">You should consider the following information before you configure scaling for your application:</span></span>

* <span data-ttu-id="a3fdc-114">A colocação em escala é afetada pelo uso de núcleo.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-114">Scaling is affected by core usage.</span></span>

    <span data-ttu-id="a3fdc-115">As instâncias de função maiores usam mais núcleos.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-115">Larger role instances use more cores.</span></span> <span data-ttu-id="a3fdc-116">Você só pode dimensionar um aplicativo dentro do limite de núcleos para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-116">You can scale an application only within the limit of cores for your subscription.</span></span> <span data-ttu-id="a3fdc-117">Por exemplo, digamos que sua assinatura tenha um limite de 20 núcleos.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-117">For example, say your subscription has a limit of 20 cores.</span></span> <span data-ttu-id="a3fdc-118">Ao executar um aplicativo com dois serviços de nuvem de tamanho médio (um total de quatro núcleos), você poderá escalar verticalmente outras implantações de serviço de nuvem na sua assinatura pelos 16 núcleos restantes.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-118">If you run an application with two medium-sized cloud services (a total of 4 cores), you can only scale up other cloud service deployments in your subscription by the remaining 16 cores.</span></span> <span data-ttu-id="a3fdc-119">Para saber mais sobre tamanhos, confira [Tamanhos do Serviço de Nuvem](cloud-services-sizes-specs.md).</span><span class="sxs-lookup"><span data-stu-id="a3fdc-119">For more information about sizes, see [Cloud Service Sizes](cloud-services-sizes-specs.md).</span></span>

* <span data-ttu-id="a3fdc-120">Você pode dimensionar com base em um limite de mensagens da fila.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-120">You can scale based on a queue message threshold.</span></span> <span data-ttu-id="a3fdc-121">Para obter mais informações sobre como usar as filas, confira [Como usar o serviço de Armazenamento de Filas](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="a3fdc-121">For more information about how to use queues, see [How to use the Queue Storage Service](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>

* <span data-ttu-id="a3fdc-122">Você também pode dimensionar outros recursos associados à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-122">You can also scale other resources associated with your subscription.</span></span>

* <span data-ttu-id="a3fdc-123">Para habilitar a alta disponibilidade do seu aplicativo, você deverá garantir que ele esteja implantado com duas ou mais instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-123">To enable high availability of your application, you should ensure that it is deployed with two or more role instances.</span></span> <span data-ttu-id="a3fdc-124">Para obter mais informações, consulte [Contratos de Nível de Serviço](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="a3fdc-124">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>


## <a name="where-scale-is-located"></a><span data-ttu-id="a3fdc-125">Onde a escala está localizada</span><span class="sxs-lookup"><span data-stu-id="a3fdc-125">Where scale is located</span></span>
<span data-ttu-id="a3fdc-126">Após selecionar o serviço de nuvem, a folha de serviço de nuvem deverá estar visível.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-126">After you select your cloud service, you should have the cloud service blade visible.</span></span>

1. <span data-ttu-id="a3fdc-127">Na folha de serviço de nuvem, no bloco **Funções e Instâncias** , selecione o nome do serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-127">On the cloud service blade, on the **Roles and Instances** tile, select the name of the cloud service.</span></span>   
   <span data-ttu-id="a3fdc-128">**IMPORTANTE**: certifique-se de clicar na função de serviço de nuvem, não na instância de função que está abaixo da função.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-128">**IMPORTANT**: Make sure to click the cloud service role, not the role instance that is below the role.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. <span data-ttu-id="a3fdc-129">Selecione o bloco **escala** .</span><span class="sxs-lookup"><span data-stu-id="a3fdc-129">Select the **scale** tile.</span></span>

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a><span data-ttu-id="a3fdc-130">Escala automática</span><span class="sxs-lookup"><span data-stu-id="a3fdc-130">Automatic scale</span></span>
<span data-ttu-id="a3fdc-131">Você pode definir as configurações de escala para uma função com o modo **manual** ou **automático**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-131">You can configure scale settings for a role with either two modes **manual** or **automatic**.</span></span> <span data-ttu-id="a3fdc-132">O modo manual é a forma como você esperaria, você define a contagem absoluta de instâncias.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-132">Manual is as you would expect, you set the absolute count of instances.</span></span> <span data-ttu-id="a3fdc-133">No entanto, o modo automático permite que você defina regras que determinem como e quanto você deverá dimensionar.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-133">Automatic however allows you to set rules that govern how and by how much you should scale.</span></span>

<span data-ttu-id="a3fdc-134">Defina a opção **Dimensionar por** para as **regras de planejamento e desempenho**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-134">Set the **Scale by** option to **schedule and performance rules**.</span></span>

![Escala dos serviços de nuvem com perfil e regra](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. <span data-ttu-id="a3fdc-136">Um perfil existente.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-136">An existing profile.</span></span>
2. <span data-ttu-id="a3fdc-137">Adicione uma regra para o perfil pai.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-137">Add a rule for the parent profile.</span></span>
3. <span data-ttu-id="a3fdc-138">Adicione outro perfil.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-138">Add another profile.</span></span>

<span data-ttu-id="a3fdc-139">Selecione **Adicionar Perfil**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-139">Select **Add Profile**.</span></span> <span data-ttu-id="a3fdc-140">O perfil determina qual modo você deseja usar para a escala: **sempre**, **recorrência** ou **data fixa**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-140">The profile determines which mode you want to use for the scale: **always**, **recurrence**, **fixed date**.</span></span>

<span data-ttu-id="a3fdc-141">Depois de configurar o perfil e as regras, selecione o ícone **Salvar** na parte superior.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-141">After you have configured the profile and rules, select the **Save** icon at the top.</span></span>

#### <a name="profile"></a><span data-ttu-id="a3fdc-142">Perfil</span><span class="sxs-lookup"><span data-stu-id="a3fdc-142">Profile</span></span>
<span data-ttu-id="a3fdc-143">O perfil define as instâncias mínimas e máximas da escala, e também quando esse intervalo de escala estará ativo.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-143">The profile sets minimum and maximum instances for the scale, and also when this scale range is active.</span></span>

* <span data-ttu-id="a3fdc-144">**Sempre**</span><span class="sxs-lookup"><span data-stu-id="a3fdc-144">**Always**</span></span>

    <span data-ttu-id="a3fdc-145">Sempre mantenha esse intervalo de instâncias disponível.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-145">Always keep this range of instances available.</span></span>  

    ![Serviço de nuvem que sempre dimensiona](./media/cloud-services-how-to-scale-portal/select-always.png)
* <span data-ttu-id="a3fdc-147">**Recorrência**</span><span class="sxs-lookup"><span data-stu-id="a3fdc-147">**Recurrence**</span></span>

    <span data-ttu-id="a3fdc-148">Escolha um conjunto de dias da semana para dimensionar.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-148">Choose a set of days of the week to scale.</span></span>

    ![Escala de serviço de nuvem com um agendamento de recorrência](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* <span data-ttu-id="a3fdc-150">**Data Fixa**</span><span class="sxs-lookup"><span data-stu-id="a3fdc-150">**Fixed Date**</span></span>

    <span data-ttu-id="a3fdc-151">Um intervalo de datas fixo para dimensionar a função.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-151">A fixed date range to scale the role.</span></span>

    ![Escala de serviço de nuvem com uma data fixa](./media/cloud-services-how-to-scale-portal/select-fixed.png)

<span data-ttu-id="a3fdc-153">Depois de configurar o perfil, selecione o botão **OK** na parte inferior da folha de perfil.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-153">After you have configured the profile, select the **OK** button at the bottom of the profile blade.</span></span>

#### <a name="rule"></a><span data-ttu-id="a3fdc-154">Regra</span><span class="sxs-lookup"><span data-stu-id="a3fdc-154">Rule</span></span>
<span data-ttu-id="a3fdc-155">As regras são adicionadas a um perfil e representam uma condição que dispara a escala.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-155">Rules are added to a profile and represent a condition that triggers the scale.</span></span>

<span data-ttu-id="a3fdc-156">O gatilho de regra se baseia em uma métrica do serviço de nuvem (utilização da CPU, atividade de disco ou atividade de rede) para a qual você pode adicionar um valor condicional.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-156">The rule trigger is based on a metric of the cloud service (CPU usage, disk activity, or network activity) to which you can add a conditional value.</span></span> <span data-ttu-id="a3fdc-157">Além disso, o gatilho pode se basear em uma fila de mensagens ou na métrica de algum outro recurso do Azure associada à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-157">Additionally you can have the trigger based on a message queue or the metric of some other Azure resource associated with your subscription.</span></span>

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

<span data-ttu-id="a3fdc-158">Depois de configurar a regra, selecione o botão **OK** na parte inferior da folha de regra.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-158">After you have configured the rule, select the **OK** button at the bottom of the rule blade.</span></span>

## <a name="back-to-manual-scale"></a><span data-ttu-id="a3fdc-159">Volte à escala manual</span><span class="sxs-lookup"><span data-stu-id="a3fdc-159">Back to manual scale</span></span>
<span data-ttu-id="a3fdc-160">Navegue até as [configurações de escala](#where-scale-is-located) e defina a opção **Dimensionar por** para **uma contagem de instâncias que inseri manualmente**.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-160">Navigate to the [scale settings](#where-scale-is-located) and set the **Scale by** option to **an instance count that I enter manually**.</span></span>

![Escala dos serviços de nuvem com perfil e regra](./media/cloud-services-how-to-scale-portal/manual-basics.png)

<span data-ttu-id="a3fdc-162">Essa configuração remove o dimensionamento automático da função. Em seguida, você pode definir a contagem de instâncias diretamente.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-162">This setting removes automated scaling from the role and then you can set the instance count directly.</span></span>

1. <span data-ttu-id="a3fdc-163">A opção escala (manual ou automática).</span><span class="sxs-lookup"><span data-stu-id="a3fdc-163">The scale (manual or automated) option.</span></span>
2. <span data-ttu-id="a3fdc-164">Um controle deslizante da instância de função para definir as instâncias para dimensionar.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-164">A role instance slider to set the instances to scale to.</span></span>
3. <span data-ttu-id="a3fdc-165">Instâncias da função para dimensionar.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-165">Instances of the role to scale to.</span></span>

<span data-ttu-id="a3fdc-166">Depois de definir as configurações de escala, selecione o ícone **Salvar** na parte superior.</span><span class="sxs-lookup"><span data-stu-id="a3fdc-166">After you have configured the scale settings, select the **Save** icon at the top.</span></span>
