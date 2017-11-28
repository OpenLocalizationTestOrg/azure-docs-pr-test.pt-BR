---
title: "Introdução ao dimensionamento automático no Azure | Microsoft Docs"
description: Saiba como dimensionar seu recurso no Azure.
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 68cb624b3ef4a77e7cfc949979e0b1949c2e5535
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="19974-103">Introdução ao dimensionamento automático no Azure</span><span class="sxs-lookup"><span data-stu-id="19974-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="19974-104">Este artigo descreve como configurar o dimensionamento automático para seu recurso no Portal do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="19974-104">This article describes how to set up your Autoscale settings for your resource in the Microsoft Azure portal.</span></span>

<span data-ttu-id="19974-105">O dimensionamento automático do Azure Monitor se aplica somente aos conjuntos de dimensionamento da máquina virtual, aos serviços de nuvem, aos planos do Serviço de Aplicativo do Azure e aos ambientes do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="19974-105">Azure Monitor Autoscale applies only to virtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-the-autoscale-settings-in-your-subscription"></a><span data-ttu-id="19974-106">Descobrir as configurações de dimensionamento automático na sua assinatura</span><span class="sxs-lookup"><span data-stu-id="19974-106">Discover the Autoscale settings in your subscription</span></span>
<span data-ttu-id="19974-107">Você pode descobrir todos os recursos a que o dimensionamento automático se aplica no Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="19974-107">You can discover all the resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="19974-108">Use as etapas a seguir para obter uma explicação passo a passo:</span><span class="sxs-lookup"><span data-stu-id="19974-108">Use the following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="19974-109">Abra o [Portal do Azure.][1]</span><span class="sxs-lookup"><span data-stu-id="19974-109">Open the [Azure portal.][1]</span></span>
2. <span data-ttu-id="19974-110">Clique no ícone do Azure Monitor no painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="19974-110">Click the Azure Monitor icon in the left pane.</span></span>
  <span data-ttu-id="19974-111">![Abra o Azure Monitor][2]</span><span class="sxs-lookup"><span data-stu-id="19974-111">![Open Azure Monitor][2]</span></span>
3. <span data-ttu-id="19974-112">Clique em **Dimensionamento automático** para exibir todos os recursos para os quais o dimensionamento automático é aplicável, juntamente com o status atual.</span><span class="sxs-lookup"><span data-stu-id="19974-112">Click **Autoscale** to view all the resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="19974-113">![Descubra o dimensionamento automático no Azure Monitor][3]</span><span class="sxs-lookup"><span data-stu-id="19974-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="19974-114">Você pode usar o painel de filtro na parte superior para reduzir o escopo da lista e selecionar recursos em um grupo de recursos específico, os tipos de recursos específicos ou um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="19974-114">You can use the filter pane at the top to scope down the list to select resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="19974-115">Para cada recurso, você encontrará a contagem de instâncias atual e o status de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="19974-115">For each resource, you will find the current instance count and the Autoscale status.</span></span> <span data-ttu-id="19974-116">O status de dimensionamento automático pode ser:</span><span class="sxs-lookup"><span data-stu-id="19974-116">The Autoscale status can be:</span></span>

- <span data-ttu-id="19974-117">**Não configurado**: você ainda não habilitou o dimensionamento automático para este recurso.</span><span class="sxs-lookup"><span data-stu-id="19974-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="19974-118">**Habilitado**: você habilitou o dimensionamento automático para este recurso.</span><span class="sxs-lookup"><span data-stu-id="19974-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="19974-119">**Desabilitado**: você desabilitou o dimensionamento automático para este recurso.</span><span class="sxs-lookup"><span data-stu-id="19974-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="19974-120">Crie sua primeira configuração de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="19974-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="19974-121">Agora, vamos percorrer um passo a passo simples para criar sua primeira configuração de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="19974-121">Let's now go through a simple step-by-step walkthrough to create your first Autoscale setting.</span></span>

1. <span data-ttu-id="19974-122">Abra a folha **Dimensionamento Automático** no Azure Monitor e selecione um recurso que deseja dimensionar.</span><span class="sxs-lookup"><span data-stu-id="19974-122">Open the **Autoscale** blade in Azure Monitor and select a resource that you want to scale.</span></span> <span data-ttu-id="19974-123">(As etapas a seguir usam um plano do serviço de aplicativo associado a um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="19974-123">(The following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="19974-124">Você pode [criar seu primeiro aplicativo Web ASP.NET no Azure em 5 minutos.][4])</span><span class="sxs-lookup"><span data-stu-id="19974-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
2. <span data-ttu-id="19974-125">Observe que a contagem da instância atual é 1.</span><span class="sxs-lookup"><span data-stu-id="19974-125">Note that the current instance count is 1.</span></span> <span data-ttu-id="19974-126">Clique em **Habilitar dimensionamento automático**.</span><span class="sxs-lookup"><span data-stu-id="19974-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="19974-127">![Configuração de dimensionamento para um novo aplicativo Web][5]</span><span class="sxs-lookup"><span data-stu-id="19974-127">![Scale setting for new web app][5]</span></span>
3. <span data-ttu-id="19974-128">Forneça um nome para a configuração de dimensionamento e clique em **Adicionar uma regra**.</span><span class="sxs-lookup"><span data-stu-id="19974-128">Provide a name for the scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="19974-129">Observe as opções de regra de dimensionamento que são abertas como um painel de contexto no lado direito.</span><span class="sxs-lookup"><span data-stu-id="19974-129">Notice the scale rule options that open as a context pane on the right side.</span></span> <span data-ttu-id="19974-130">Por padrão, ele define a opção de dimensionar sua contagem de instâncias em 1 se o percentual de CPU do recurso ultrapassar 70%.</span><span class="sxs-lookup"><span data-stu-id="19974-130">By default, this sets the option to scale your instance count by 1 if the CPU percentage of the resource exceeds 70 percent.</span></span> <span data-ttu-id="19974-131">Deixe-o com seus valores padrão e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="19974-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="19974-132">![Criar configuração dimensionamento para um aplicativo Web][6]</span><span class="sxs-lookup"><span data-stu-id="19974-132">![Create scale setting for a web app][6]</span></span>
4. <span data-ttu-id="19974-133">Agora, você criou sua primeira regra de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="19974-133">You've now created your first scale rule.</span></span> <span data-ttu-id="19974-134">Observe que o UX indica as práticas recomendadas e afirma que "É recomendável ter pelo menos uma escala na regra".</span><span class="sxs-lookup"><span data-stu-id="19974-134">Note that the UX recommends best practices and states that "It is recommended to have at least one scale in rule."</span></span> <span data-ttu-id="19974-135">Para fazer isso:</span><span class="sxs-lookup"><span data-stu-id="19974-135">To do so:</span></span>
  
    <span data-ttu-id="19974-136">a.</span><span class="sxs-lookup"><span data-stu-id="19974-136">a.</span></span> <span data-ttu-id="19974-137">Clique em **Adicionar uma Regra**.</span><span class="sxs-lookup"><span data-stu-id="19974-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="19974-138">b.</span><span class="sxs-lookup"><span data-stu-id="19974-138">b.</span></span> <span data-ttu-id="19974-139">Defina **Operador** como **Menor que**.</span><span class="sxs-lookup"><span data-stu-id="19974-139">Set **Operator** to **Less than**.</span></span>

    <span data-ttu-id="19974-140">c.</span><span class="sxs-lookup"><span data-stu-id="19974-140">c.</span></span> <span data-ttu-id="19974-141">Defina o **Limite** como **20**.</span><span class="sxs-lookup"><span data-stu-id="19974-141">Set **Threshold** to **20**.</span></span>

    <span data-ttu-id="19974-142">d.</span><span class="sxs-lookup"><span data-stu-id="19974-142">d.</span></span> <span data-ttu-id="19974-143">Defina **Operação** como **Diminuir contagem por**.</span><span class="sxs-lookup"><span data-stu-id="19974-143">Set **Operation** to **Decrease count by**.</span></span>

   <span data-ttu-id="19974-144">Agora, você deve ter uma configuração de dimensionamento que expande/reduz com base no uso da CPU.</span><span class="sxs-lookup"><span data-stu-id="19974-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="19974-145">![Dimensionamento com base na CPU][8]</span><span class="sxs-lookup"><span data-stu-id="19974-145">![Scale based on CPU][8]</span></span>
5. <span data-ttu-id="19974-146">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="19974-146">Click **Save**.</span></span>

<span data-ttu-id="19974-147">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="19974-147">Congratulations!</span></span> <span data-ttu-id="19974-148">Você criou com êxito sua primeira configuração de dimensionamento para fazer o dimensionamento automático de seu aplicativo Web com base no uso da CPU.</span><span class="sxs-lookup"><span data-stu-id="19974-148">You've now successfully created your first scale setting to autoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="19974-149">As mesmas etapas são aplicáveis para começar a usar uma função de serviço de nuvem ou conjunto de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="19974-149">The same steps are applicable to get started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="19974-150">Outras considerações</span><span class="sxs-lookup"><span data-stu-id="19974-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="19974-151">Dimensionamento com base em um planejamento</span><span class="sxs-lookup"><span data-stu-id="19974-151">Scale based on a schedule</span></span>
<span data-ttu-id="19974-152">Além de dimensionar com base na CPU, você também pode definir seu dimensionamento de forma diferente em dias específicos da semana.</span><span class="sxs-lookup"><span data-stu-id="19974-152">In addition to scale based on CPU, you can set your scale differently for specific days of the week.</span></span>

1. <span data-ttu-id="19974-153">Clique em **Adicionar uma condição de dimensionamento**.</span><span class="sxs-lookup"><span data-stu-id="19974-153">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="19974-154">A configuração do modo e das regras de dimensionamento é a mesma que a da condição padrão.</span><span class="sxs-lookup"><span data-stu-id="19974-154">Setting the scale mode and the rules is the same as the default condition.</span></span>
3. <span data-ttu-id="19974-155">Selecione **Repetir dias específicos** para o agendamento.</span><span class="sxs-lookup"><span data-stu-id="19974-155">Select **Repeat specific days** for the schedule.</span></span>
4. <span data-ttu-id="19974-156">Selecione os dias e a hora de início/término em que a condição de dimensionamento deve ser aplicada.</span><span class="sxs-lookup"><span data-stu-id="19974-156">Select the days and the start/end time for when the scale condition should be applied.</span></span>

![Condição de dimensionamento com base no agendamento][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="19974-158">Dimensionar de forma diferente em datas específicas</span><span class="sxs-lookup"><span data-stu-id="19974-158">Scale differently on specific dates</span></span>
<span data-ttu-id="19974-159">Além de dimensionar com base na CPU, você também pode definir seu dimensionamento de forma diferente em datas específicas.</span><span class="sxs-lookup"><span data-stu-id="19974-159">In addition to scale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="19974-160">Clique em **Adicionar uma condição de dimensionamento**.</span><span class="sxs-lookup"><span data-stu-id="19974-160">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="19974-161">A configuração do modo e das regras de dimensionamento é a mesma que a da condição padrão.</span><span class="sxs-lookup"><span data-stu-id="19974-161">Setting the scale mode and the rules is the same as the default condition.</span></span>
3. <span data-ttu-id="19974-162">Selecione **Especificar datas de início/término** para o agendamento.</span><span class="sxs-lookup"><span data-stu-id="19974-162">Select **Specify start/end dates** for the schedule.</span></span>
4. <span data-ttu-id="19974-163">Selecione as datas e a hora de início/término em que a condição de dimensionamento deve ser aplicada.</span><span class="sxs-lookup"><span data-stu-id="19974-163">Select the start/end dates and the start/end time for when the scale condition should be applied.</span></span>

![Condição de dimensionamento com base em datas][10]

### <a name="view-the-scale-history-of-your-resource"></a><span data-ttu-id="19974-165">Exibir o histórico de dimensionamento de seu recurso</span><span class="sxs-lookup"><span data-stu-id="19974-165">View the scale history of your resource</span></span>
<span data-ttu-id="19974-166">Sempre que o recurso é expandido/reduzido, um evento é registrado no log de atividades.</span><span class="sxs-lookup"><span data-stu-id="19974-166">Whenever your resource is scaled up or down, an event is logged in the activity log.</span></span> <span data-ttu-id="19974-167">Você pode exibir o histórico de dimensionamento do seu recurso nas últimas 24 horas acessando a guia **Histórico de execução**.</span><span class="sxs-lookup"><span data-stu-id="19974-167">You can view the scale history of your resource for the past 24 hours by switching to the **Run history** tab.</span></span>

![Histórico da execução][11]

<span data-ttu-id="19974-169">Se quiser exibir o histórico completo de dimensionamento (de até 90 dias), selecione **Clique aqui para ver mais detalhes**.</span><span class="sxs-lookup"><span data-stu-id="19974-169">If you want to view the complete scale history (for up to 90 days), select **Click here to see more details**.</span></span> <span data-ttu-id="19974-170">O log de atividade é aberto, com Dimensionamento Automático pré-selecionado para seu recurso e categoria.</span><span class="sxs-lookup"><span data-stu-id="19974-170">The activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-the-scale-definition-of-your-resource"></a><span data-ttu-id="19974-171">Exibir a definição de escala do seu recurso</span><span class="sxs-lookup"><span data-stu-id="19974-171">View the scale definition of your resource</span></span>
<span data-ttu-id="19974-172">Dimensionamento automático é um recurso do Gerenciador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="19974-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="19974-173">Você pode exibir a definição de escala no JSON acessando a guia **JSON**.</span><span class="sxs-lookup"><span data-stu-id="19974-173">You can view the scale definition in JSON by switching to the **JSON** tab.</span></span>

![Definição de escala][12]

<span data-ttu-id="19974-175">Você pode fazer alterações no JSON diretamente, se necessário.</span><span class="sxs-lookup"><span data-stu-id="19974-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="19974-176">Essas alterações serão refletidas depois que você as salvar.</span><span class="sxs-lookup"><span data-stu-id="19974-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="19974-177">Desabilitar a escala automática e dimensionar suas instâncias manualmente</span><span class="sxs-lookup"><span data-stu-id="19974-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="19974-178">Pode haver momentos em que você queira desabilitar sua configuração de dimensionamento atual e dimensionar manualmente seu recurso.</span><span class="sxs-lookup"><span data-stu-id="19974-178">There might be times when you want to disable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="19974-179">Clique no botão **Desabilitar dimensionamento automático** na parte superior.</span><span class="sxs-lookup"><span data-stu-id="19974-179">Click the **Disable autoscale** button at the top.</span></span>
<span data-ttu-id="19974-180">![Desabilitar dimensionamento automático][13]</span><span class="sxs-lookup"><span data-stu-id="19974-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="19974-181">Esta opção desabilita a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="19974-181">This option disables your configuration.</span></span> <span data-ttu-id="19974-182">No entanto, você pode voltar a ela depois que habilitar o Dimensionamento Automático novamente.</span><span class="sxs-lookup"><span data-stu-id="19974-182">However, you can get back to it after you enable Autoscale again.</span></span> 

<span data-ttu-id="19974-183">Agora, você pode definir o número de instâncias para o qual deseja dimensionar manualmente.</span><span class="sxs-lookup"><span data-stu-id="19974-183">You can now set the number of instances that you want to scale to manually.</span></span>

![Definir dimensionamento manual][14]

<span data-ttu-id="19974-185">Você sempre pode retornar para o dimensionamento automático clicando em **Habilitar dimensionamento automático** e **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="19974-185">You can always return to Autoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19974-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="19974-186">Next steps</span></span>
- [<span data-ttu-id="19974-187">Crie um Alerta de Log de Atividades para monitorar todas as operações de mecanismo de dimensionamento automático em sua assinatura</span><span class="sxs-lookup"><span data-stu-id="19974-187">Create an Activity Log Alert to monitor all Autoscale engine operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [<span data-ttu-id="19974-188">Crie um Alerta de Log de Atividades para monitorar todas as operações de escalar horizontalmente/reduzir horizontalmente com falha na sua assinatura</span><span class="sxs-lookup"><span data-stu-id="19974-188">Create an Activity Log Alert to monitor all failed Autoscale scale-in/scale-out operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

