---
title: "aaaGet iniciado com o dimensionamento automático no Azure | Microsoft Docs"
description: Saiba como tooscale seus recursos no Azure.
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
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="29a13-103">Introdução ao dimensionamento automático no Azure</span><span class="sxs-lookup"><span data-stu-id="29a13-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="29a13-104">Este artigo descreve como tooset suas configurações de dimensionamento automático para o recurso no portal do Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="29a13-104">This article describes how tooset up your Autoscale settings for your resource in hello Microsoft Azure portal.</span></span>

<span data-ttu-id="29a13-105">Dimensionamento automático de Monitor do Azure se aplica apenas conjuntos de escala de máquina toovirtual, serviços de nuvem, planos de serviço de aplicativo do Azure e ambientes de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="29a13-105">Azure Monitor Autoscale applies only toovirtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a><span data-ttu-id="29a13-106">Descobrir as configurações de dimensionamento automático de saudação em sua assinatura</span><span class="sxs-lookup"><span data-stu-id="29a13-106">Discover hello Autoscale settings in your subscription</span></span>
<span data-ttu-id="29a13-107">Você pode descobrir todos os recursos de saudação para o qual o dimensionamento automático é aplicável no Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="29a13-107">You can discover all hello resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="29a13-108">Use Olá seguindo as etapas para obter uma explicação passo a passo:</span><span class="sxs-lookup"><span data-stu-id="29a13-108">Use hello following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="29a13-109">Olá abrir [portal do Azure.][1]</span><span class="sxs-lookup"><span data-stu-id="29a13-109">Open hello [Azure portal.][1]</span></span>
2. <span data-ttu-id="29a13-110">Clique hello Azure ícone no painel esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="29a13-110">Click hello Azure Monitor icon in hello left pane.</span></span>
  <span data-ttu-id="29a13-111">![Abra o Azure Monitor][2]</span><span class="sxs-lookup"><span data-stu-id="29a13-111">![Open Azure Monitor][2]</span></span>
3. <span data-ttu-id="29a13-112">Clique em **AutoEscala** tooview todos os recursos de saudação para o dimensionamento automático é aplicável, juntamente com seu status atual de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="29a13-112">Click **Autoscale** tooview all hello resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="29a13-113">![Descubra o dimensionamento automático no Azure Monitor][3]</span><span class="sxs-lookup"><span data-stu-id="29a13-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="29a13-114">Você pode usar o painel de filtro de saudação em tooscope de saudação principais recursos de tooselect Olá lista em um grupo de recursos específicos, tipos específicos de recursos ou um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="29a13-114">You can use hello filter pane at hello top tooscope down hello list tooselect resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="29a13-115">Para cada recurso, você encontrará a contagem atual de instâncias hello e status da AutoEscala hello.</span><span class="sxs-lookup"><span data-stu-id="29a13-115">For each resource, you will find hello current instance count and hello Autoscale status.</span></span> <span data-ttu-id="29a13-116">Olá AutoEscala status pode ser:</span><span class="sxs-lookup"><span data-stu-id="29a13-116">hello Autoscale status can be:</span></span>

- <span data-ttu-id="29a13-117">**Não configurado**: você ainda não habilitou o dimensionamento automático para este recurso.</span><span class="sxs-lookup"><span data-stu-id="29a13-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="29a13-118">**Habilitado**: você habilitou o dimensionamento automático para este recurso.</span><span class="sxs-lookup"><span data-stu-id="29a13-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="29a13-119">**Desabilitado**: você desabilitou o dimensionamento automático para este recurso.</span><span class="sxs-lookup"><span data-stu-id="29a13-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="29a13-120">Crie sua primeira configuração de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="29a13-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="29a13-121">Agora vamos por meio de uma simples passo toocreate sua primeira configuração de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="29a13-121">Let's now go through a simple step-by-step walkthrough toocreate your first Autoscale setting.</span></span>

1. <span data-ttu-id="29a13-122">Olá abrir **AutoEscala** folha no Monitor do Azure e selecione um recurso que você deseja tooscale.</span><span class="sxs-lookup"><span data-stu-id="29a13-122">Open hello **Autoscale** blade in Azure Monitor and select a resource that you want tooscale.</span></span> <span data-ttu-id="29a13-123">(hello etapas a seguir usam um plano de serviço de aplicativo associado a um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="29a13-123">(hello following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="29a13-124">Você pode [criar seu primeiro aplicativo Web ASP.NET no Azure em 5 minutos.][4])</span><span class="sxs-lookup"><span data-stu-id="29a13-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
2. <span data-ttu-id="29a13-125">Observe que a contagem atual de instâncias de saudação é 1.</span><span class="sxs-lookup"><span data-stu-id="29a13-125">Note that hello current instance count is 1.</span></span> <span data-ttu-id="29a13-126">Clique em **Habilitar dimensionamento automático**.</span><span class="sxs-lookup"><span data-stu-id="29a13-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="29a13-127">![Configuração de dimensionamento para um novo aplicativo Web][5]</span><span class="sxs-lookup"><span data-stu-id="29a13-127">![Scale setting for new web app][5]</span></span>
3. <span data-ttu-id="29a13-128">Forneça um nome para a configuração da escala hello e, em seguida, clique em **adicionar uma regra**.</span><span class="sxs-lookup"><span data-stu-id="29a13-128">Provide a name for hello scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="29a13-129">Observe as opções de regra de escala de saudação que são abertos como um painel de contexto Olá direita.</span><span class="sxs-lookup"><span data-stu-id="29a13-129">Notice hello scale rule options that open as a context pane on hello right side.</span></span> <span data-ttu-id="29a13-130">Por padrão, isso define Olá opção tooscale sua instância de contagem em 1 se Olá percentual de CPU do recurso Olá exceder 70 por cento.</span><span class="sxs-lookup"><span data-stu-id="29a13-130">By default, this sets hello option tooscale your instance count by 1 if hello CPU percentage of hello resource exceeds 70 percent.</span></span> <span data-ttu-id="29a13-131">Deixe-o com seus valores padrão e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="29a13-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="29a13-132">![Criar configuração dimensionamento para um aplicativo Web][6]</span><span class="sxs-lookup"><span data-stu-id="29a13-132">![Create scale setting for a web app][6]</span></span>
4. <span data-ttu-id="29a13-133">Agora, você criou sua primeira regra de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="29a13-133">You've now created your first scale rule.</span></span> <span data-ttu-id="29a13-134">Observe que Olá UX recomenda práticas recomendadas e declara que "é recomendável toohave pelo menos uma escala na regra."</span><span class="sxs-lookup"><span data-stu-id="29a13-134">Note that hello UX recommends best practices and states that "It is recommended toohave at least one scale in rule."</span></span> <span data-ttu-id="29a13-135">toodo para:</span><span class="sxs-lookup"><span data-stu-id="29a13-135">toodo so:</span></span>
  
    <span data-ttu-id="29a13-136">a.</span><span class="sxs-lookup"><span data-stu-id="29a13-136">a.</span></span> <span data-ttu-id="29a13-137">Clique em **Adicionar uma Regra**.</span><span class="sxs-lookup"><span data-stu-id="29a13-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="29a13-138">b.</span><span class="sxs-lookup"><span data-stu-id="29a13-138">b.</span></span> <span data-ttu-id="29a13-139">Definir **operador** muito**menor**.</span><span class="sxs-lookup"><span data-stu-id="29a13-139">Set **Operator** too**Less than**.</span></span>

    <span data-ttu-id="29a13-140">c.</span><span class="sxs-lookup"><span data-stu-id="29a13-140">c.</span></span> <span data-ttu-id="29a13-141">Definir **limite** muito**20**.</span><span class="sxs-lookup"><span data-stu-id="29a13-141">Set **Threshold** too**20**.</span></span>

    <span data-ttu-id="29a13-142">d.</span><span class="sxs-lookup"><span data-stu-id="29a13-142">d.</span></span> <span data-ttu-id="29a13-143">Definir **operação** muito**diminuir a contagem por**.</span><span class="sxs-lookup"><span data-stu-id="29a13-143">Set **Operation** too**Decrease count by**.</span></span>

   <span data-ttu-id="29a13-144">Agora, você deve ter uma configuração de dimensionamento que expande/reduz com base no uso da CPU.</span><span class="sxs-lookup"><span data-stu-id="29a13-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="29a13-145">![Dimensionamento com base na CPU][8]</span><span class="sxs-lookup"><span data-stu-id="29a13-145">![Scale based on CPU][8]</span></span>
5. <span data-ttu-id="29a13-146">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="29a13-146">Click **Save**.</span></span>

<span data-ttu-id="29a13-147">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="29a13-147">Congratulations!</span></span> <span data-ttu-id="29a13-148">Agora você já criou com êxito sua primeira tooautoscale de configuração de escala seu aplicativo web com base no uso da CPU.</span><span class="sxs-lookup"><span data-stu-id="29a13-148">You've now successfully created your first scale setting tooautoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="29a13-149">Olá, mesmas etapas são aplicável tooget iniciado com uma escala de máquina virtual função de serviço de nuvem ou conjunto.</span><span class="sxs-lookup"><span data-stu-id="29a13-149">hello same steps are applicable tooget started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="29a13-150">Outras considerações</span><span class="sxs-lookup"><span data-stu-id="29a13-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="29a13-151">Dimensionamento com base em um planejamento</span><span class="sxs-lookup"><span data-stu-id="29a13-151">Scale based on a schedule</span></span>
<span data-ttu-id="29a13-152">Além disso tooscale com base na CPU, você pode definir sua escala diferente para dias específicos da semana hello.</span><span class="sxs-lookup"><span data-stu-id="29a13-152">In addition tooscale based on CPU, you can set your scale differently for specific days of hello week.</span></span>

1. <span data-ttu-id="29a13-153">Clique em **Adicionar uma condição de dimensionamento**.</span><span class="sxs-lookup"><span data-stu-id="29a13-153">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="29a13-154">Configurando regras de modo e hello de escala de saudação é Olá mesmo como condição de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="29a13-154">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="29a13-155">Selecione **Repita dias específicos** para agendamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="29a13-155">Select **Repeat specific days** for hello schedule.</span></span>
4. <span data-ttu-id="29a13-156">Selecione os dias hello e a hora de início/término hello para quando a condição de escala Olá deve ser aplicada.</span><span class="sxs-lookup"><span data-stu-id="29a13-156">Select hello days and hello start/end time for when hello scale condition should be applied.</span></span>

![Condição de dimensionamento com base no agendamento][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="29a13-158">Dimensionar de forma diferente em datas específicas</span><span class="sxs-lookup"><span data-stu-id="29a13-158">Scale differently on specific dates</span></span>
<span data-ttu-id="29a13-159">Além disso tooscale com base na CPU, você pode definir sua escala diferente para datas específicas.</span><span class="sxs-lookup"><span data-stu-id="29a13-159">In addition tooscale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="29a13-160">Clique em **Adicionar uma condição de dimensionamento**.</span><span class="sxs-lookup"><span data-stu-id="29a13-160">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="29a13-161">Configurando regras de modo e hello de escala de saudação é Olá mesmo como condição de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="29a13-161">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="29a13-162">Selecione **especificar datas de início/término** para agendamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="29a13-162">Select **Specify start/end dates** for hello schedule.</span></span>
4. <span data-ttu-id="29a13-163">Selecione as datas de início/término hello e a hora de início/término hello para quando a condição de escala Olá deve ser aplicada.</span><span class="sxs-lookup"><span data-stu-id="29a13-163">Select hello start/end dates and hello start/end time for when hello scale condition should be applied.</span></span>

![Condição de dimensionamento com base em datas][10]

### <a name="view-hello-scale-history-of-your-resource"></a><span data-ttu-id="29a13-165">Exibir o histórico de escala de saudação do recurso</span><span class="sxs-lookup"><span data-stu-id="29a13-165">View hello scale history of your resource</span></span>
<span data-ttu-id="29a13-166">Sempre que o recurso é dimensionado para cima ou para baixo, um evento é registrado no log de atividades de saudação.</span><span class="sxs-lookup"><span data-stu-id="29a13-166">Whenever your resource is scaled up or down, an event is logged in hello activity log.</span></span> <span data-ttu-id="29a13-167">Você pode exibir histórico de escala de saudação do recurso para Olá últimas 24 horas, alternando toohello **histórico de execução** guia.</span><span class="sxs-lookup"><span data-stu-id="29a13-167">You can view hello scale history of your resource for hello past 24 hours by switching toohello **Run history** tab.</span></span>

![Histórico da execução][11]

<span data-ttu-id="29a13-169">Se você desejar tooview Olá escala completa histórico (para cima too90 dias), selecione **clique aqui toosee mais detalhes**.</span><span class="sxs-lookup"><span data-stu-id="29a13-169">If you want tooview hello complete scale history (for up too90 days), select **Click here toosee more details**.</span></span> <span data-ttu-id="29a13-170">log de atividades de saudação é aberta, com o dimensionamento automático previamente selecionado para o recurso e categoria.</span><span class="sxs-lookup"><span data-stu-id="29a13-170">hello activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-hello-scale-definition-of-your-resource"></a><span data-ttu-id="29a13-171">Exibir definição de escala de saudação do recurso</span><span class="sxs-lookup"><span data-stu-id="29a13-171">View hello scale definition of your resource</span></span>
<span data-ttu-id="29a13-172">Dimensionamento automático é um recurso do Gerenciador de Recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="29a13-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="29a13-173">Você pode exibir a definição de escala de saudação em JSON, alternando toohello **JSON** guia.</span><span class="sxs-lookup"><span data-stu-id="29a13-173">You can view hello scale definition in JSON by switching toohello **JSON** tab.</span></span>

![Definição de escala][12]

<span data-ttu-id="29a13-175">Você pode fazer alterações no JSON diretamente, se necessário.</span><span class="sxs-lookup"><span data-stu-id="29a13-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="29a13-176">Essas alterações serão refletidas depois que você as salvar.</span><span class="sxs-lookup"><span data-stu-id="29a13-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="29a13-177">Desabilitar a escala automática e dimensionar suas instâncias manualmente</span><span class="sxs-lookup"><span data-stu-id="29a13-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="29a13-178">Pode haver momentos quando desejar toodisable sua configuração atual de escala e Dimensionar manualmente o recurso.</span><span class="sxs-lookup"><span data-stu-id="29a13-178">There might be times when you want toodisable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="29a13-179">Clique em Olá **desabilitar dimensionamento automático** botão na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="29a13-179">Click hello **Disable autoscale** button at hello top.</span></span>
<span data-ttu-id="29a13-180">![Desabilitar dimensionamento automático][13]</span><span class="sxs-lookup"><span data-stu-id="29a13-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="29a13-181">Esta opção desabilita a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="29a13-181">This option disables your configuration.</span></span> <span data-ttu-id="29a13-182">No entanto, você pode voltar tooit depois de habilitar o dimensionamento automático novamente.</span><span class="sxs-lookup"><span data-stu-id="29a13-182">However, you can get back tooit after you enable Autoscale again.</span></span> 

<span data-ttu-id="29a13-183">Agora você pode definir número de saudação de instâncias que você deseja tooscale toomanually.</span><span class="sxs-lookup"><span data-stu-id="29a13-183">You can now set hello number of instances that you want tooscale toomanually.</span></span>

![Definir dimensionamento manual][14]

<span data-ttu-id="29a13-185">Você sempre pode retornar tooAutoscale clicando **habilitar a AutoEscala** e **salvar**.</span><span class="sxs-lookup"><span data-stu-id="29a13-185">You can always return tooAutoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="29a13-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="29a13-186">Next steps</span></span>
- [<span data-ttu-id="29a13-187">Criar um alerta de Log da atividade toomonitor todas as operações de mecanismo de dimensionamento automático em sua assinatura</span><span class="sxs-lookup"><span data-stu-id="29a13-187">Create an Activity Log Alert toomonitor all Autoscale engine operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [<span data-ttu-id="29a13-188">Criar um alerta de Log da atividade toomonitor todas as falhas operações de escala-em/expansão de dimensionamento automático em sua assinatura</span><span class="sxs-lookup"><span data-stu-id="29a13-188">Create an Activity Log Alert toomonitor all failed Autoscale scale-in/scale-out operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

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

