---
title: "soluções pré-configuradas de aaaGet iniciado com | Microsoft Docs"
description: "Siga este tutorial toolearn como toodeploy um Azure IoT Suite pré-configurado solução."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 6ab38d1a-b564-469e-8a87-e597aa51d0f7
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: a7f46023d26b08de2e8ed48c34c5066a43e3fa38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-preconfigured-solutions"></a><span data-ttu-id="4bb2a-103">Introdução ao soluções Olá pré-configurado</span><span class="sxs-lookup"><span data-stu-id="4bb2a-103">Get started with hello preconfigured solutions</span></span>

<span data-ttu-id="4bb2a-104">Azure IoT Suite [soluções pré-configuradas] [ lnk-preconfigured-solutions] combinar várias IoT do Azure services toodeliver ponta a ponta soluções que implementam cenários comuns de negócios de IoT.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="4bb2a-105">Olá *monitoramento remoto* solução pré-configurada conecta tooand monitora seus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-105">hello *remote monitoring* preconfigured solution connects tooand monitors your devices.</span></span> <span data-ttu-id="4bb2a-106">Você pode usar o fluxo de saudação do hello solução tooanalyze de dados de seus dispositivos e os resultados dos negócios tooimprove fazendo processos responder automaticamente toothat o fluxo de dados.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-106">You can use hello solution tooanalyze hello stream of data from your devices and tooimprove business outcomes by making processes respond automatically toothat stream of data.</span></span>

<span data-ttu-id="4bb2a-107">Este tutorial mostra como o monitoramento remoto tooprovision Olá pré-configurado solução.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-107">This tutorial shows you how tooprovision hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="4bb2a-108">Ele também orienta você por meio de recursos básicos de saudação da solução Olá pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="4bb2a-109">Você pode acessar muitos desses recursos de solução de saudação *painel* que implanta como parte da solução Olá pré-configurados:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![Painel de solução pré-configurada de monitoramento remoto][img-dashboard]

<span data-ttu-id="4bb2a-111">toocomplete neste tutorial, você precisa de uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="4bb2a-112">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4bb2a-113">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="4bb2a-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="4bb2a-114">Visão geral do cenário</span><span class="sxs-lookup"><span data-stu-id="4bb2a-114">Scenario overview</span></span>

<span data-ttu-id="4bb2a-115">Quando você implanta Olá solução pré-configurada de monitoramento remoto, ele será preenchido com recursos que permitem que você toostep por meio de um cenário comum de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-115">When you deploy hello remote monitoring preconfigured solution, it is prepopulated with resources that enable you toostep through a common remote monitoring scenario.</span></span> <span data-ttu-id="4bb2a-116">Nesse cenário, solução de toohello conectado vários dispositivos estão relatando os valores de temperatura inesperado.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-116">In this scenario, several devices connected toohello solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="4bb2a-117">Olá seções a seguir mostram como para:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-117">hello following sections show you how to:</span></span>

* <span data-ttu-id="4bb2a-118">Identificar os dispositivos de saudação enviar valores de temperatura inesperado.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-118">Identify hello devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="4bb2a-119">Configurar esses dispositivos toosend mais detalhadas da telemetria.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-119">Configure these devices toosend more detailed telemetry.</span></span>
* <span data-ttu-id="4bb2a-120">Corrigi o problema de saudação pela atualização do firmware Olá nesses dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-120">Fix hello problem by updating hello firmware on these devices.</span></span>
* <span data-ttu-id="4bb2a-121">Verifique se que a ação resolveu o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-121">Verify that your action has resolved hello issue.</span></span>

<span data-ttu-id="4bb2a-122">Um recurso principal deste cenário é que você pode executar todas essas ações remotamente no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-122">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="4bb2a-123">Dispositivos de toohello acesso físico não é necessário.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-123">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="4bb2a-124">Painel de solução de saudação de View</span><span class="sxs-lookup"><span data-stu-id="4bb2a-124">View hello solution dashboard</span></span>

<span data-ttu-id="4bb2a-125">Painel de solução de saudação permite toomanage solução de saudação implantada.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-125">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="4bb2a-126">Por exemplo, você pode exibir telemetria, adicionar dispositivos e configurar regras.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="4bb2a-127">Quando Olá provisionamento for concluído e lado a lado para sua solução pré-configurada Olá indica **pronto**, escolha **iniciar** tooopen seu portal de solução de monitoramento remoto em uma nova guia.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-127">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your remote monitoring solution portal in a new tab.</span></span>

    ![Iniciar a solução de saudação pré-configurado][img-launch-solution]

1. <span data-ttu-id="4bb2a-129">Por padrão, o portal de solução Olá mostra Olá *painel*.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-129">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="4bb2a-130">Você pode navegar tooother áreas do portal de solução hello usando o menu de saudação no lado esquerdo de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-130">You can navigate tooother areas of hello solution portal using hello menu on hello left-hand side of hello page.</span></span>

    ![Painel de solução pré-configurada de monitoramento remoto][img-menu]

<span data-ttu-id="4bb2a-132">Painel de saudação exibe Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-132">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="4bb2a-133">Um mapa que exibe o local de saudação de cada dispositivo conectado toohello solução.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-133">A map that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="4bb2a-134">Quando você executa solução hello, há 25 dispositivos simulados.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-134">When you first run hello solution, there are 25 simulated devices.</span></span> <span data-ttu-id="4bb2a-135">Hello simulados dispositivos são implementados como WebJobs do Azure, e solução de saudação usa as informações de tooplot de API do Bing Maps de Olá no mapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-135">hello simulated devices are implemented as Azure WebJobs, and hello solution uses hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="4bb2a-136">Consulte Olá [perguntas frequentes sobre] [ lnk-faq] toolearn como toomake Olá mapa dinâmico.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-136">See hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="4bb2a-137">Um painel **Histórico de Telemetria** que plota telemetria de umidade e temperatura de um dispositivo selecionado em tempo quase real e exibe dados de agregação, como umidade média, mínima e máxima.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="4bb2a-138">Um painel **Histórico de Alarme** que mostra eventos recentes de alarme quando um valor de telemetria excedeu um limite.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="4bb2a-139">Você pode definir seus próprios alarmes nos exemplos de toohello adição criados pela solução Olá pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-139">You can define your own alarms in addition toohello examples created by hello preconfigured solution.</span></span>
* <span data-ttu-id="4bb2a-140">Um painel **Trabalhos** que exibe informações sobre os trabalhos agendados.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="4bb2a-141">Você pode agendar seus próprios trabalhos na página **Trabalhos de gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="4bb2a-142">Exibir alarmes</span><span class="sxs-lookup"><span data-stu-id="4bb2a-142">View alarms</span></span>

<span data-ttu-id="4bb2a-143">Painel de histórico de alarme Olá mostra que cinco dispositivos estão se comunicando maior do que os valores esperados de telemetria.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-143">hello alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![Histórico de alarme de tarefas no painel de solução de saudação][img-alarms]

> [!NOTE]
> <span data-ttu-id="4bb2a-145">Esses alarmes são gerados por uma regra que está incluída na solução Olá pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-145">These alarms are generated by a rule that is included in hello preconfigured solution.</span></span> <span data-ttu-id="4bb2a-146">Essa regra gera um alerta quando o valor de temperatura Olá enviado por um dispositivo excede 60.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-146">This rule generates an alert when hello temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="4bb2a-147">Você pode definir suas próprias regras e ações escolhendo [regras](#add-a-rule) e [ações](#add-an-action) no menu esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in hello left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="4bb2a-148">Exibir dispositivos</span><span class="sxs-lookup"><span data-stu-id="4bb2a-148">View devices</span></span>

<span data-ttu-id="4bb2a-149">Olá *dispositivos* lista mostra todos os dispositivos de saudação registrado na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-149">hello *devices* list shows all hello registered devices in hello solution.</span></span> <span data-ttu-id="4bb2a-150">Na lista de dispositivos Olá você pode exibir e editar os metadados do dispositivo, adicionar ou remover dispositivos e chamar métodos em dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-150">From hello device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="4bb2a-151">Você pode filtrar e classificar lista Olá de dispositivos na lista de dispositivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-151">You can filter and sort hello list of devices in hello device list.</span></span> <span data-ttu-id="4bb2a-152">Você também pode personalizar as colunas de Olá mostradas na lista de dispositivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-152">You can also customize hello columns shown in hello device list.</span></span>

1. <span data-ttu-id="4bb2a-153">Escolha **dispositivos** tooshow lista de dispositivos Olá para esta solução.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-153">Choose **Devices** tooshow hello device list for this solution.</span></span>

   ![Lista de dispositivos de saudação de exibição no portal de solução de saudação][img-devicelist]

1. <span data-ttu-id="4bb2a-155">lista de dispositivos Olá inicialmente mostra 25 dispositivos simulados criados pelo processo de provisionamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-155">hello device list initially shows 25 simulated devices created by hello provisioning process.</span></span> <span data-ttu-id="4bb2a-156">Você pode adicionar a solução de toohello de dispositivos adicionais simulada e físico.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-156">You can add additional simulated and physical devices toohello solution.</span></span>

1. <span data-ttu-id="4bb2a-157">detalhes de saudação tooview de um dispositivo, escolha um dispositivo na lista de dispositivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-157">tooview hello details of a device, choose a device in hello device list.</span></span>

   ![Exibir detalhes do dispositivo Olá no portal de solução de saudação][img-devicedetails]

<span data-ttu-id="4bb2a-159">Olá **detalhes do dispositivo** painel contém seis seções:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-159">hello **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="4bb2a-160">Uma coleção de links que permitem a você toocustomize Olá ícone do dispositivo, desativar dispositivo hello, adicionar uma regra, invocar um método ou enviar um comando.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-160">A collection of links that enable you toocustomize hello device icon, disable hello device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="4bb2a-161">Para ter uma comparação de comandos (mensagens do dispositivo para nuvem) e métodos (métodos diretos), consulte [Orientação para comunicações entre o dispositivo e a nuvem][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="4bb2a-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="4bb2a-162">Olá **dispositivo duas - marcas** seção permite que você tooedit valores de marca para dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-162">hello **Device Twin - Tags** section enables you tooedit tag values for hello device.</span></span> <span data-ttu-id="4bb2a-163">Você pode exibir valores de marca na lista de dispositivos de saudação e usar a lista de dispositivos marca valores toofilter hello.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-163">You can display tag values in hello device list and use tag values toofilter hello device list.</span></span>
* <span data-ttu-id="4bb2a-164">Olá **dispositivo duas - propriedades desejado** seção permite que você tooset propriedade valores toobe enviado toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-164">hello **Device Twin - Desired Properties** section enables you tooset property values toobe sent toohello device.</span></span>
* <span data-ttu-id="4bb2a-165">Olá **dispositivo duas - propriedades relatadas** seção mostra os valores de propriedade enviados do dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-165">hello **Device Twin - Reported Properties** section shows property values sent from hello device.</span></span>
* <span data-ttu-id="4bb2a-166">Olá **propriedades do dispositivo** seção mostra informações de registro de identidade hello como dispositivo Olá chaves de identificação e autenticação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-166">hello **Device Properties** section shows information from hello identity registry such as hello device id and authentication keys.</span></span>
* <span data-ttu-id="4bb2a-167">Olá **trabalhos recentes** seção mostra informações sobre todos os trabalhos que têm recentemente esse dispositivo de destino.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-167">hello **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-hello-device-list"></a><span data-ttu-id="4bb2a-168">Lista de dispositivos de saudação do filtro</span><span class="sxs-lookup"><span data-stu-id="4bb2a-168">Filter hello device list</span></span>

<span data-ttu-id="4bb2a-169">Você pode usar um filtro toodisplay apenas os dispositivos que estão enviando valores de temperatura inesperado.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-169">You can use a filter toodisplay only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="4bb2a-170">Olá solução pré-configurada de monitoramento remoto inclui Olá **dispositivos não íntegro** filtrar tooshow dispositivos com um valor de temperatura média maior que 60.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-170">hello remote monitoring preconfigured solution includes hello **Unhealthy devices** filter tooshow devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="4bb2a-171">Você também pode [criar seus próprios filtros](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="4bb2a-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="4bb2a-172">Escolha **abrir salvos filtro** toodisplay uma lista de filtros disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-172">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="4bb2a-173">Em seguida, escolha **dispositivos não íntegro** filtro de saudação tooapply:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-173">Then choose **Unhealthy devices** tooapply hello filter:</span></span>

    ![Exibir a lista de saudação de filtros][img-unhealthy-filter]

1. <span data-ttu-id="4bb2a-175">lista de dispositivos Olá agora mostra somente os dispositivos com um valor de temperatura média maior que 60.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-175">hello device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![Exibir lista de dispositivo filtrado Olá mostrando dispositivos não íntegro][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="4bb2a-177">Atualizar as propriedades desejadas</span><span class="sxs-lookup"><span data-stu-id="4bb2a-177">Update desired properties</span></span>

<span data-ttu-id="4bb2a-178">Você identificou agora um conjunto de dispositivos que precisam de correção.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="4bb2a-179">No entanto, você decidir que a frequência de dados de saudação de 15 segundos não é suficiente para um diagnóstico claro do problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-179">However, you decide that hello data frequency of 15 seconds is not sufficient for a clear diagnosis of hello issue.</span></span> <span data-ttu-id="4bb2a-180">Com mais toobetter de pontos de dados alterando Olá telemetria frequência toofive segundos tooprovide diagnostica o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-180">Changing hello telemetry frequency toofive seconds tooprovide you with more data points toobetter diagnose hello issue.</span></span> <span data-ttu-id="4bb2a-181">Você pode enviar por push dispositivos remotos do alteração tooyour essa configuração do portal de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-181">You can push this configuration change tooyour remote devices from hello solution portal.</span></span> <span data-ttu-id="4bb2a-182">Você pode fazer a alteração de saudação uma vez, avaliar o impacto de Olá e, em seguida, atuar em resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-182">You can make hello change once, evaluate hello impact, and then act on hello results.</span></span>

<span data-ttu-id="4bb2a-183">Siga essas etapas toorun um trabalho que altera a saudação **TelemetryInterval** propriedade para dispositivos Olá afetado desejada.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-183">Follow these steps toorun a job that changes hello **TelemetryInterval** desired property for hello affected devices.</span></span> <span data-ttu-id="4bb2a-184">Quando dispositivos Olá recebem Olá novo **TelemetryInterval** valor da propriedade, eles mudam seu telemetria de toosend configuração cada cinco segundos, em vez da cada 15 segundos:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-184">When hello devices receive hello new **TelemetryInterval** property value, they change their configuration toosend telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="4bb2a-185">Enquanto você estiver mostrando a lista de Olá de dispositivos não íntegro na lista de dispositivos de saudação, escolha **Agendador de trabalhos**, em seguida, **Editar dispositivo duas**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-185">While you are showing hello list of unhealthy devices in hello device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="4bb2a-186">Chamar trabalho Olá **intervalo de alteração de telemetria**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-186">Call hello job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="4bb2a-187">Alterar valor Olá Olá **propriedade desejada** nome **desejado. Config.TelemetryInterval** toofive segundos.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-187">Change hello value of hello **Desired Property** name **desired.Config.TelemetryInterval** toofive seconds.</span></span>

1. <span data-ttu-id="4bb2a-188">Escolha **Agenda**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-188">Choose **Schedule**.</span></span>

    ![Alterar Olá TelemetryInterval propriedade toofive segundos][img-change-interval]

1. <span data-ttu-id="4bb2a-190">Você pode monitorar o andamento de saudação do trabalho Olá Olá **gerenciamento trabalhos** página no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-190">You can monitor hello progress of hello job on hello **Management Jobs** page in hello portal.</span></span>

> [!NOTE]
> <span data-ttu-id="4bb2a-191">Se você quiser toochange um valor de propriedade desejada para um dispositivo individual, use Olá **propriedades desejadas** seção Olá **detalhes do dispositivo** painel em vez de executar um trabalho.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-191">If you want toochange a desired property value for an individual device, use hello **Desired Properties** section in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="4bb2a-192">Esse trabalho define o valor de saudação do hello **TelemetryInterval** desejado de propriedade em duas de dispositivo Olá para todos os dispositivos selecionados pelo filtro de saudação de hello.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-192">This job sets hello value of hello **TelemetryInterval** desired property in hello device twin for all hello devices selected by hello filter.</span></span> <span data-ttu-id="4bb2a-193">dispositivos de saudação recuperar esse valor de duas de dispositivo hello e atualizar seu comportamento.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-193">hello devices retrieve this value from hello device twin and update their behavior.</span></span> <span data-ttu-id="4bb2a-194">Quando um dispositivo recupera e processa uma propriedade desejada de duas um dispositivo, ele define a propriedade de valor relatado correspondente do hello.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-194">When a device retrieves and processes a desired property from a device twin, it sets hello corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="4bb2a-195">Invocar métodos</span><span class="sxs-lookup"><span data-stu-id="4bb2a-195">Invoke methods</span></span>

<span data-ttu-id="4bb2a-196">Enquanto o trabalho Olá é executado, você observe na lista de saudação de dispositivos não íntegro todos esses dispositivos têm firmware antigo (menor que a versão 1.6) versões.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-196">While hello job runs, you notice in hello list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![Saudação de exibição relatados versão do firmware para dispositivos não íntegro Olá][img-old-firmware]

<span data-ttu-id="4bb2a-198">Esta versão do firmware pode ser a causa raiz Olá Olá inesperado temperatura valores porque você sabe que outros dispositivos íntegros foram atualizado recentemente tooversion 2.0.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-198">This firmware version may be hello root cause of hello unexpected temperature values because you know that other healthy devices were recently updated tooversion 2.0.</span></span> <span data-ttu-id="4bb2a-199">É possível usar Olá interno **dispositivos antigos do firmware** filtrar tooidentify quaisquer dispositivos com versões antigas do firmware.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-199">You can use hello built-in **Old firmware devices** filter tooidentify any devices with old firmware versions.</span></span> <span data-ttu-id="4bb2a-200">No portal de saudação, você poderá remotamente atualizar todos os dispositivos de saudação ainda executando versões antigas do firmware:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-200">From hello portal, you can then remotely update all hello devices still running old firmware versions:</span></span>

1. <span data-ttu-id="4bb2a-201">Escolha **abrir salvos filtro** toodisplay uma lista de filtros disponíveis.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-201">Choose **Open saved filter** toodisplay a list of available filters.</span></span> <span data-ttu-id="4bb2a-202">Em seguida, escolha **dispositivos antigos do firmware** filtro de saudação tooapply:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-202">Then choose **Old firmware devices** tooapply hello filter:</span></span>

    ![Exibir a lista de saudação de filtros][img-old-filter]

1. <span data-ttu-id="4bb2a-204">lista de dispositivos Olá agora mostra somente os dispositivos com versões antigas do firmware.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-204">hello device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="4bb2a-205">Essa lista inclui cinco dispositivos de saudação identificados pelo Olá **dispositivos não íntegro** filtro e três dispositivos adicionais:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-205">This list includes hello five devices identified by hello **Unhealthy devices** filter and three additional devices:</span></span>

    ![Exibir lista de dispositivo filtrado Olá mostrando dispositivos antigos][img-filtered-old-list]

1. <span data-ttu-id="4bb2a-207">Escolha **Agendador de Trabalho** e, em seguida, **Chamar o Método**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="4bb2a-208">Definir **nome do trabalho** muito**tooversion de atualização de Firmware 2.0**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-208">Set **Job Name** too**Firmware update tooversion 2.0**.</span></span>

1. <span data-ttu-id="4bb2a-209">Escolha **InitiateFirmwareUpdate** como Olá **método**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-209">Choose **InitiateFirmwareUpdate** as hello **Method**.</span></span>

1. <span data-ttu-id="4bb2a-210">Saudação de conjunto **FwPackageUri** parâmetro muito**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-210">Set hello **FwPackageUri** parameter too**https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="4bb2a-211">Escolha **Agenda**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-211">Choose **Schedule**.</span></span> <span data-ttu-id="4bb2a-212">saudação padrão é Olá trabalho toorun agora.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-212">hello default is for hello job toorun now.</span></span>

    ![Criar trabalho tooupdate Olá firmware dispositivos Olá selecionado][img-method-update]

> [!NOTE]
> <span data-ttu-id="4bb2a-214">Se você quiser tooinvoke um método em um dispositivo individual, escolha **métodos** em Olá **detalhes do dispositivo** painel em vez de executar um trabalho.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-214">If you want tooinvoke a method on an individual device, choose **Methods** in hello **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="4bb2a-215">Esse trabalho invoca Olá **InitiateFirmwareUpdate** método direto em todos os dispositivos de saudação selecionados pelo filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-215">This job invokes hello **InitiateFirmwareUpdate** direct method on all hello devices selected by hello filter.</span></span> <span data-ttu-id="4bb2a-216">Dispositivos respondem imediatamente tooIoT Hub e iniciam o processo de atualização de firmware Olá assincronamente.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-216">Devices respond immediately tooIoT Hub and then initiate hello firmware update process asynchronously.</span></span> <span data-ttu-id="4bb2a-217">dispositivos de saudação fornecem informações de status sobre o processo de atualização de firmware Olá por meio de valores de propriedade relatado, conforme mostrado no hello capturas de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-217">hello devices provide status information about hello firmware update process through reported property values, as shown in hello following screenshots.</span></span> <span data-ttu-id="4bb2a-218">Escolha Olá **atualização** informações de saudação tooupdate ícone em listas de trabalho e dispositivo hello:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-218">Choose hello **Refresh** icon tooupdate hello information in hello device and job lists:</span></span>

<span data-ttu-id="4bb2a-219">![Lista de trabalhos, mostrando a execução de lista de atualização de firmware Olá][img-update-1]
![lista de dispositivos, mostrando o status de atualização de firmware][img-update-2]
![trabalho mostrando Olá firmware atualização lista completa][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="4bb2a-219">![Job list showing hello firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing hello firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="4bb2a-220">Em um ambiente de produção, você pode agendar trabalhos toorun durante uma janela de manutenção designado.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-220">In a production environment, you can schedule jobs toorun during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="4bb2a-221">Análise do cenário</span><span class="sxs-lookup"><span data-stu-id="4bb2a-221">Scenario review</span></span>

<span data-ttu-id="4bb2a-222">Nesse cenário, você identificou um problema potencial com alguns de seus dispositivos remotos usando o histórico de alarme Olá no painel hello e um filtro.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-222">In this scenario, you identified a potential issue with some of your remote devices using hello alarm history on hello dashboard and a filter.</span></span> <span data-ttu-id="4bb2a-223">Você então filtro Olá usado e tooremotely um trabalho configurar Olá dispositivos tooprovide toohelp de informações mais diagnosticar o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-223">You then used hello filter and a job tooremotely configure hello devices tooprovide more information toohelp diagnose hello issue.</span></span> <span data-ttu-id="4bb2a-224">Finalmente, você usou um filtro e manutenção de tooschedule um trabalho em dispositivos Olá afetado.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-224">Finally, you used a filter and a job tooschedule maintenance on hello affected devices.</span></span> <span data-ttu-id="4bb2a-225">Se você retornar toohello painel, você pode verificar que não existem mais qualquer alarmes provenientes de dispositivos em sua solução.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-225">If you return toohello dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="4bb2a-226">Você pode usar um filtro tooverify que Olá firmware está atualizado em todos os dispositivos de saudação em sua solução e que não há mais nenhum íntegros dispositivos:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-226">You can use a filter tooverify that hello firmware is up-to-date on all hello devices in your solution and that there are no more unhealthy devices:</span></span>

![Filtro mostrando que todos os dispositivos têm um firmware atualizado][img-updated]

![Filtro mostrando que todos os dispositivos estão íntegros][img-healthy]

## <a name="other-features"></a><span data-ttu-id="4bb2a-229">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="4bb2a-229">Other features</span></span>

<span data-ttu-id="4bb2a-230">Olá seções a seguir descrevem alguns recursos adicionais de saudação solução pré-configurada de monitoramento remoto que não são descritos como parte do cenário anterior hello.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-230">hello following sections describe some additional features of hello remote monitoring preconfigured solution that are not described as part of hello previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="4bb2a-231">Personalizar colunas</span><span class="sxs-lookup"><span data-stu-id="4bb2a-231">Customize columns</span></span>

<span data-ttu-id="4bb2a-232">Você pode personalizar as informações de saudação mostradas na lista de dispositivos Olá escolhendo **editor coluna**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-232">You can customize hello information shown in hello device list by choosing **Column editor**.</span></span> <span data-ttu-id="4bb2a-233">Você pode adicionar e remover as colunas que exibem os valores de propriedade e marcação relatados.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="4bb2a-234">Também pode reorganizar e renomear as colunas:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-234">You can also reorder and rename columns:</span></span>

   ![Lista de dispositivos coluna editor ion Olá][img-columneditor]

### <a name="customize-hello-device-icon"></a><span data-ttu-id="4bb2a-236">Personalizar o ícone do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="4bb2a-236">Customize hello device icon</span></span>

<span data-ttu-id="4bb2a-237">Você pode personalizar o ícone do dispositivo Olá exibido na lista de dispositivos de saudação do hello **detalhes do dispositivo** painel da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-237">You can customize hello device icon displayed in hello device list from hello **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="4bb2a-238">Escolha Olá Olá de tooopen do ícone de lápis **Editar imagem** painel para um dispositivo:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-238">Choose hello pencil icon tooopen hello **Edit image** panel for a device:</span></span>

   ![Abrir o editor de imagens do dispositivo][img-startimageedit]

1. <span data-ttu-id="4bb2a-240">Carregar uma nova imagem ou usar uma das imagens existentes hello e, em seguida, escolha **salvar**:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-240">Either upload a new image or use one of hello existing images and then choose **Save**:</span></span>

   ![Editar o editor de imagens do dispositivo][img-imageedit]

1. <span data-ttu-id="4bb2a-242">Olá imagem selecionada agora exibe em Olá **ícone** coluna para o dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-242">hello image you selected now displays in hello **Icon** column for hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="4bb2a-243">Olá imagem está armazenada no armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-243">hello image is stored in blob storage.</span></span> <span data-ttu-id="4bb2a-244">Uma marca em duas de dispositivo Olá contém uma imagem de toohello link no armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-244">A tag in hello device twin contains a link toohello image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="4bb2a-245">Adicionar um dispositivo</span><span class="sxs-lookup"><span data-stu-id="4bb2a-245">Add a device</span></span>

<span data-ttu-id="4bb2a-246">Quando você implanta a solução Olá pré-configurados, você provisiona automaticamente 25 dispositivos de exemplo que você pode ver na lista de dispositivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-246">When you deploy hello preconfigured solution, you automatically provision 25 sample devices that you can see in hello device list.</span></span> <span data-ttu-id="4bb2a-247">Esses dispositivos são *dispositivos simulados* em execução em um Trabalho Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="4bb2a-248">Dispositivos simulados tornam mais fácil para você tooexperiment com solução Olá pré-configurado sem Olá necessidade toodeploy real, físico dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-248">Simulated devices make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical devices.</span></span> <span data-ttu-id="4bb2a-249">Se você quiser tooconnect uma solução de toohello dispositivo real, consulte Olá [conectar sua solução pré-configurada de monitoramento remoto de toohello dispositivo] [ lnk-connect-rm] tutorial.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-249">If you do want tooconnect a real device toohello solution, see hello [Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="4bb2a-250">Olá etapas a seguir mostram como tooadd uma solução do dispositivo simulado toohello:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-250">hello following steps show you how tooadd a simulated device toohello solution:</span></span>

1. <span data-ttu-id="4bb2a-251">Navegue back toohello lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-251">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="4bb2a-252">tooadd um dispositivo, escolha **+ adicionar um dispositivo** no canto do hello inferior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-252">tooadd a device, choose **+ Add A Device** in hello bottom left corner.</span></span>

   ![Adicionar uma solução de toohello pré-configurado do dispositivo][img-adddevice]

1. <span data-ttu-id="4bb2a-254">Escolha **adicionar novo** em Olá **dispositivo simulado** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-254">Choose **Add New** on hello **Simulated Device** tile.</span></span>

   ![Definir novos detalhes do dispositivo no painel][img-addnew]

   <span data-ttu-id="4bb2a-256">Em adição toocreating um novo dispositivo simulado, você também pode adicionar um dispositivo físico se você escolher toocreate um **dispositivo personalizado**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-256">In addition toocreating a new simulated device, you can also add a physical device if you choose toocreate a **Custom Device**.</span></span> <span data-ttu-id="4bb2a-257">toolearn mais sobre como se conectar a solução de toohello de dispositivos físicos, consulte [conectar seu toohello de dispositivo IoT Suite solução pré-configurada de monitoramento remoto][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="4bb2a-257">toolearn more about connecting physical devices toohello solution, see [Connect your device toohello IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="4bb2a-258">Selecione **Deixe-me definir minha própria ID** de dispositivo e adicione um nome de ID de dispositivo exclusivo, como **mydevice_01**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="4bb2a-259">Escolha **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-259">Choose **Create**.</span></span>

   ![Salvar um novo dispositivo][img-definedevice]

1. <span data-ttu-id="4bb2a-261">Na etapa 3 do **adicionar um dispositivo simulado**, escolha **feito** lista de dispositivos de toohello tooreturn.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-261">In step 3 of **Add a simulated device**, choose **Done** tooreturn toohello device list.</span></span>

1. <span data-ttu-id="4bb2a-262">Você pode exibir seu dispositivo **executando** na lista de dispositivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-262">You can view your device **Running** in hello device list.</span></span>

    ![Exibir novo dispositivo na lista de dispositivos][img-runningnew]

1. <span data-ttu-id="4bb2a-264">Você também pode exibir hello simulados telemetria do seu dispositivo novo painel hello:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-264">You can also view hello simulated telemetry from your new device on hello dashboard:</span></span>

    ![Exibir telemetria do novo dispositivo][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="4bb2a-266">Desabilitar e excluir um dispositivo</span><span class="sxs-lookup"><span data-stu-id="4bb2a-266">Disable and delete a device</span></span>

<span data-ttu-id="4bb2a-267">Você pode desabilitar um dispositivo e depois que ele for desabilitado, poderá removê-lo:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![Desabilitar e remover um dispositivo][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="4bb2a-269">Adicionar uma regra</span><span class="sxs-lookup"><span data-stu-id="4bb2a-269">Add a rule</span></span>

<span data-ttu-id="4bb2a-270">Existem regras para o novo dispositivo de saudação recém-adicionado.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-270">There are no rules for hello new device you just added.</span></span> <span data-ttu-id="4bb2a-271">Nesta seção, você deve adicionar uma regra que dispara um alarme quando temperatura Olá relatado pelo Olá novo dispositivo excede 47 graus.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-271">In this section, you add a rule that triggers an alarm when hello temperature reported by hello new device exceeds 47 degrees.</span></span> <span data-ttu-id="4bb2a-272">Antes de começar, observe que o histórico de telemetria Olá para novo dispositivo de saudação no painel de saudação mostra a temperatura do dispositivo Olá nunca exceda 45 graus.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-272">Before you start, notice that hello telemetry history for hello new device on hello dashboard shows hello device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="4bb2a-273">Navegue back toohello lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-273">Navigate back toohello device list.</span></span>

1. <span data-ttu-id="4bb2a-274">tooadd uma regra para dispositivo hello, selecione o novo dispositivo no hello **lista de dispositivos**e, em seguida, escolha **Adicionar regra**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-274">tooadd a rule for hello device, select your new device in hello **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="4bb2a-275">Criar uma regra que usa **temperatura** como campo de dados hello e usa **AlarmTemp** como hello quando temperatura Olá excede 47 graus de saída:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-275">Create a rule that uses **Temperature** as hello data field and uses **AlarmTemp** as hello output when hello temperature exceeds 47 degrees:</span></span>

    ![Adicionar uma regra de dispositivo][img-adddevicerule]

1. <span data-ttu-id="4bb2a-277">toosave as alterações, escolha **salvar e exibir regras**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-277">toosave your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="4bb2a-278">Escolha **comandos** no painel de detalhes de dispositivo Olá para o novo dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-278">Choose **Commands** in hello device details pane for hello new device.</span></span>

    ![Adicionar uma regra de dispositivo][img-adddevicerule2]

1. <span data-ttu-id="4bb2a-280">Selecione **ChangeSetPointTemp** da lista de comandos hello e defina **SetPointTemp** too45.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-280">Select **ChangeSetPointTemp** from hello command list and set **SetPointTemp** too45.</span></span> <span data-ttu-id="4bb2a-281">Escolha **Enviar Comando**:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-281">Then choose **Send Command**:</span></span>

    ![Adicionar uma regra de dispositivo][img-adddevicerule3]

1. <span data-ttu-id="4bb2a-283">Navegue painel traseiro toohello.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-283">Navigate back toohello dashboard.</span></span> <span data-ttu-id="4bb2a-284">Após um curto período de tempo, você verá uma nova entrada no hello **histórico de alarme** painel quando a temperatura Olá relatado pelo seu novo dispositivo excede o limite de grau 47 hello:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-284">After a short time, you will see a new entry in hello **Alarm History** pane when hello temperature reported by your new device exceeds hello 47-degree threshold:</span></span>

    ![Adicionar uma regra de dispositivo][img-adddevicerule4]

1. <span data-ttu-id="4bb2a-286">Você pode revisar e editar todas as regras em Olá **regras** página do painel de saudação:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-286">You can review and edit all your rules on hello **Rules** page of hello dashboard:</span></span>

    ![Listar regras de dispositivo][img-rules]

1. <span data-ttu-id="4bb2a-288">Você pode revisar e editar todas as ações de saudação que podem ser executadas na regra de tooa de resposta em Olá **ações** página do painel de saudação:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-288">You can review and edit all hello actions that can be taken in response tooa rule on hello **Actions** page of hello dashboard:</span></span>

    ![Listar ações de dispositivo][img-actions]

> [!NOTE]
> <span data-ttu-id="4bb2a-290">É possível toodefine ações que podem enviar uma mensagem de email ou SMS na resposta tooa regra ou integrar com um sistema de linha de negócios por meio de um [aplicativo lógico][lnk-logic-apps].</span><span class="sxs-lookup"><span data-stu-id="4bb2a-290">It is possible toodefine actions that can send an email message or SMS in response tooa rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="4bb2a-291">Para obter mais informações, consulte Olá [tooyour conexão lógica aplicativo monitoramento remoto do Azure IoT Suite pré-configurado solução][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="4bb2a-291">For more information, see hello [Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="4bb2a-292">Gerenciar filtros</span><span class="sxs-lookup"><span data-stu-id="4bb2a-292">Manage filters</span></span>

<span data-ttu-id="4bb2a-293">Na lista de dispositivos hello, criar, salvar e recarregar filtros toodisplay uma lista personalizada de hub de tooyour conectado de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-293">In hello device list, you can create, save, and reload filters toodisplay a customized list of devices connected tooyour hub.</span></span> <span data-ttu-id="4bb2a-294">toocreate um filtro:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-294">toocreate a filter:</span></span>

1. <span data-ttu-id="4bb2a-295">Escolha o ícone de filtro de edição Olá acima da lista de saudação de dispositivos:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-295">Choose hello edit filter icon above hello list of devices:</span></span>

    ![Editor de filtro Olá aberto][img-editfiltericon]

1. <span data-ttu-id="4bb2a-297">Em Olá **editor de filtro**, adicionar campos hello, operadores e lista de dispositivos valores toofilter hello.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-297">In hello **Filter editor**, add hello fields, operators, and values toofilter hello device list.</span></span> <span data-ttu-id="4bb2a-298">Você pode adicionar vários toorefine de cláusulas seu filtro.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-298">You can add multiple clauses toorefine your filter.</span></span> <span data-ttu-id="4bb2a-299">Escolha **filtro** filtro de saudação tooapply:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-299">Choose **Filter** tooapply hello filter:</span></span>

    ![Crie um filtro][img-filtereditor]

1. <span data-ttu-id="4bb2a-301">Neste exemplo, a lista de saudação é filtrada por fabricante e modelo:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-301">In this example, hello list is filtered by manufacturer and model number:</span></span>

    ![Lista filtrada][img-filterelist]

1. <span data-ttu-id="4bb2a-303">toosave o filtro com um nome personalizado, escolha Olá **Salvar como** ícone:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-303">toosave your filter with a custom name, choose hello **Save as** icon:</span></span>

    ![Salvar um filtro][img-savefilter]

1. <span data-ttu-id="4bb2a-305">tooreapply um filtro que você salvou anteriormente, escolha Olá **abrir salvos filtro** ícone:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-305">tooreapply a filter you saved previously, choose hello **Open saved filter** icon:</span></span>

    ![Abrir um filtro][img-openfilter]

<span data-ttu-id="4bb2a-307">Você pode criar filtros com base na id do dispositivo, estado do dispositivo, propriedades desejadas, propriedades relatadas e marcações.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="4bb2a-308">Adicionar seu próprio dispositivo tooa de marcas personalizadas no hello **marcas** seção Olá **detalhes do dispositivo** painel ou executar um trabalho tooupdate tags em vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-308">You add your own custom tags tooa device in hello **Tags** section of hello **Device Details** panel, or run a job tooupdate tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="4bb2a-309">Em Olá **editor de filtro**, você pode usar o hello **exibição avançada** tooedit Olá texto da consulta diretamente.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-309">In hello **Filter editor**, you can use hello **Advanced view** tooedit hello query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="4bb2a-310">Comandos</span><span class="sxs-lookup"><span data-stu-id="4bb2a-310">Commands</span></span>

<span data-ttu-id="4bb2a-311">De saudação **detalhes do dispositivo** painel, você pode enviar o dispositivo de toohello de comandos.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-311">From hello **Device Details** panel, you can send commands toohello device.</span></span> <span data-ttu-id="4bb2a-312">Quando um dispositivo é iniciado, ele envia informações sobre Olá comandos dá suporte à solução toohello.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-312">When a device first starts, it sends information about hello commands it supports toohello solution.</span></span> <span data-ttu-id="4bb2a-313">Para obter uma discussão das diferenças de saudação entre os métodos e comandos, consulte [opções de nuvem para dispositivo do Azure IoT Hub][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="4bb2a-313">For a discussion of hello differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="4bb2a-314">Escolha **comandos** em Olá **detalhes do dispositivo** painel para o dispositivo selecionado hello:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-314">Choose **Commands** in hello **Device Details** panel for hello selected device:</span></span>

   ![Comandos de dispositivo no painel][img-devicecommands]

1. <span data-ttu-id="4bb2a-316">Selecione **PingDevice** da lista de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-316">Select **PingDevice** from hello command list.</span></span>

1. <span data-ttu-id="4bb2a-317">Escolha **Enviar Comando**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="4bb2a-318">Você pode ver o status de saudação do comando Olá no histórico de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-318">You can see hello status of hello command in hello command history.</span></span>

   ![Status do comando no painel][img-pingcommand]

<span data-ttu-id="4bb2a-320">solução de saudação rastreia o status de saudação de cada comando envia.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-320">hello solution tracks hello status of each command it sends.</span></span> <span data-ttu-id="4bb2a-321">Inicialmente é o resultado de saudação **pendente**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-321">Initially hello result is **Pending**.</span></span> <span data-ttu-id="4bb2a-322">Quando o dispositivo Olá relata que ele executou o comando hello, Olá é conjunto de resultados muito**sucesso**.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-322">When hello device reports that it has executed hello command, hello result is set too**Success**.</span></span>

## <a name="behind-hello-scenes"></a><span data-ttu-id="4bb2a-323">Em segundo plano da saudação</span><span class="sxs-lookup"><span data-stu-id="4bb2a-323">Behind hello scenes</span></span>

<span data-ttu-id="4bb2a-324">Quando você implanta uma solução pré-configurada, o processo de implantação de saudação cria vários recursos no hello assinatura do Azure que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-324">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="4bb2a-325">Você pode exibir esses recursos no hello Azure [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="4bb2a-325">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="4bb2a-326">o processo de implantação Olá cria um **grupo de recursos** com um nome baseado no nome hello escolhido para sua solução pré-configurada:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-326">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Solução pré-configurada em Olá portal do Azure][img-portal]

<span data-ttu-id="4bb2a-328">Você pode exibir configurações de saudação de cada recurso, selecionando-o na lista de saudação de recursos no grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-328">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="4bb2a-329">Você também pode exibir o código-fonte Olá para solução de saudação pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-329">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="4bb2a-330">Olá código-fonte solução pré-configurada de monitoramento remoto está em Olá [azure-iot-monitoramento remoto] [ lnk-rmgithub] repositório GitHub:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-330">hello remote monitoring preconfigured solution source code is in hello [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="4bb2a-331">Olá **DeviceAdministration** pasta contém o código-fonte para o painel Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-331">hello **DeviceAdministration** folder contains hello source code for hello dashboard.</span></span>
* <span data-ttu-id="4bb2a-332">Olá **simulador** pasta contém o código-fonte para o dispositivo simulado Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-332">hello **Simulator** folder contains hello source code for hello simulated device.</span></span>
* <span data-ttu-id="4bb2a-333">Olá **EventProcessor** pasta contém o código-fonte Olá para o processo de back-end de saudação que manipula a telemetria de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-333">hello **EventProcessor** folder contains hello source code for hello back-end process that handles hello incoming telemetry.</span></span>

<span data-ttu-id="4bb2a-334">Quando você terminar, você pode excluir solução Olá pré-configurado de sua assinatura do Azure em Olá [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-334">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="4bb2a-335">Este site permite que você exclua tooeasily que todos os recursos que foram provisionados quando você criou a solução Olá pré-configurado de hello.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-335">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="4bb2a-336">tooensure excluir tudo relacionados à solução toohello pré-configurado, excluí-la em Olá [azureiotsuite.com] [ lnk-azureiotsuite] do site e não exclua o grupo de recursos de saudação no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="4bb2a-336">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site and do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bb2a-337">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4bb2a-337">Next Steps</span></span>

<span data-ttu-id="4bb2a-338">Agora que você implantou uma solução de trabalho pré-configurados, você pode continuar a guia de Introdução com IoT Suite lendo Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4bb2a-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="4bb2a-339">[Passo a passo da solução pré-configurada de monitoramento remoto][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="4bb2a-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="4bb2a-340">[Conecte-se a sua solução pré-configurada de monitoramento remoto de toohello de dispositivo][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="4bb2a-340">[Connect your device toohello remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="4bb2a-341">[Permissões no site de azureiotsuite.com Olá][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="4bb2a-341">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

[img-launch-solution]: media/iot-suite-getstarted-preconfigured-solutions/launch.png
[img-dashboard]: media/iot-suite-getstarted-preconfigured-solutions/dashboard.png
[img-menu]: media/iot-suite-getstarted-preconfigured-solutions/menu.png
[img-devicelist]: media/iot-suite-getstarted-preconfigured-solutions/devicelist.png
[img-alarms]: media/iot-suite-getstarted-preconfigured-solutions/alarms.png
[img-devicedetails]: media/iot-suite-getstarted-preconfigured-solutions/devicedetails.png
[img-devicecommands]: media/iot-suite-getstarted-preconfigured-solutions/devicecommands.png
[img-pingcommand]: media/iot-suite-getstarted-preconfigured-solutions/pingcommand.png
[img-adddevice]: media/iot-suite-getstarted-preconfigured-solutions/adddevice.png
[img-addnew]: media/iot-suite-getstarted-preconfigured-solutions/addnew.png
[img-definedevice]: media/iot-suite-getstarted-preconfigured-solutions/definedevice.png
[img-runningnew]: media/iot-suite-getstarted-preconfigured-solutions/runningnew.png
[img-runningnew-2]: media/iot-suite-getstarted-preconfigured-solutions/runningnew2.png
[img-rules]: media/iot-suite-getstarted-preconfigured-solutions/rules.png
[img-adddevicerule]: media/iot-suite-getstarted-preconfigured-solutions/addrule.png
[img-adddevicerule2]: media/iot-suite-getstarted-preconfigured-solutions/addrule2.png
[img-adddevicerule3]: media/iot-suite-getstarted-preconfigured-solutions/addrule3.png
[img-adddevicerule4]: media/iot-suite-getstarted-preconfigured-solutions/addrule4.png
[img-actions]: media/iot-suite-getstarted-preconfigured-solutions/actions.png
[img-portal]: media/iot-suite-getstarted-preconfigured-solutions/portal.png
[img-disable]: media/iot-suite-getstarted-preconfigured-solutions/solutionportal_08.png
[img-columneditor]: media/iot-suite-getstarted-preconfigured-solutions/columneditor.png
[img-startimageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit1.png
[img-imageedit]: media/iot-suite-getstarted-preconfigured-solutions/imagedit2.png
[img-editfiltericon]: media/iot-suite-getstarted-preconfigured-solutions/editfiltericon.png
[img-filtereditor]: media/iot-suite-getstarted-preconfigured-solutions/filtereditor.png
[img-filterelist]: media/iot-suite-getstarted-preconfigured-solutions/filteredlist.png
[img-savefilter]: media/iot-suite-getstarted-preconfigured-solutions/savefilter.png
[img-openfilter]:  media/iot-suite-getstarted-preconfigured-solutions/openfilter.png
[img-unhealthy-filter]: media/iot-suite-getstarted-preconfigured-solutions/unhealthyfilter.png
[img-filtered-unhealthy-list]: media/iot-suite-getstarted-preconfigured-solutions/unhealthylist.png
[img-change-interval]: media/iot-suite-getstarted-preconfigured-solutions/changeinterval.png
[img-old-firmware]: media/iot-suite-getstarted-preconfigured-solutions/noticeold.png
[img-old-filter]: media/iot-suite-getstarted-preconfigured-solutions/oldfilter.png
[img-filtered-old-list]: media/iot-suite-getstarted-preconfigured-solutions/oldlist.png
[img-method-update]: media/iot-suite-getstarted-preconfigured-solutions/methodupdate.png
[img-update-1]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate1.png
[img-update-2]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate2.png
[img-update-3]: media/iot-suite-getstarted-preconfigured-solutions/jobupdate3.png
[img-updated]: media/iot-suite-getstarted-preconfigured-solutions/updated.png
[img-healthy]: media/iot-suite-getstarted-preconfigured-solutions/healthy.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-logic-apps]: https://azure.microsoft.com/documentation/services/app-service/logic/
[lnk-portal]: http://portal.azure.com/
[lnk-rmgithub]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-logicapptutorial]: iot-suite-logic-apps-tutorial.md
[lnk-rm-walkthrough]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-connect-rm]: iot-suite-connecting-devices.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-faq]: iot-suite-faq.md