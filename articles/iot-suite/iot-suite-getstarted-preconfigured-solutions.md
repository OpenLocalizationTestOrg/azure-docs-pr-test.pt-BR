---
title: "Introdução às soluções pré-configuradas | Microsoft Docs"
description: "Siga este tutorial para aprender a implantar uma solução pré-configurada do Azure IoT Suite."
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
ms.openlocfilehash: 466825ab78a5ac9773d8beff69cca90ff9db6c01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-preconfigured-solutions"></a><span data-ttu-id="f399c-103">Introdução a soluções pré-configuradas</span><span class="sxs-lookup"><span data-stu-id="f399c-103">Get started with the preconfigured solutions</span></span>

<span data-ttu-id="f399c-104">As [soluções pré-configuradas][lnk-preconfigured-solutions] do Azure IoT Suite combinam vários serviços de IoT do Azure para fornecer soluções de ponta a ponta que implementam cenários comuns de negócios de IoT.</span><span class="sxs-lookup"><span data-stu-id="f399c-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="f399c-105">A solução pré-configurada de *monitoramento remoto* conecta-se seus dispositivos e os monitora.</span><span class="sxs-lookup"><span data-stu-id="f399c-105">The *remote monitoring* preconfigured solution connects to and monitors your devices.</span></span> <span data-ttu-id="f399c-106">Você pode usar a solução para analisar o fluxo de dados de dispositivos e melhorar os resultados de negócios fazendo com que os processos respondam automaticamente a esse fluxo de dados.</span><span class="sxs-lookup"><span data-stu-id="f399c-106">You can use the solution to analyze the stream of data from your devices and to improve business outcomes by making processes respond automatically to that stream of data.</span></span>

<span data-ttu-id="f399c-107">Este tutorial mostra como provisionar a solução pré-configurada de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="f399c-107">This tutorial shows you how to provision the remote monitoring preconfigured solution.</span></span> <span data-ttu-id="f399c-108">Ele também explica os recursos básicos da solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="f399c-108">It also walks you through the basic features of the preconfigured solution.</span></span> <span data-ttu-id="f399c-109">Você pode acessar muitos desses recursos no *painel* de solução que é implantado como parte da solução pré-configurada:</span><span class="sxs-lookup"><span data-stu-id="f399c-109">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span></span>

![Painel de solução pré-configurada de monitoramento remoto][img-dashboard]

<span data-ttu-id="f399c-111">Para concluir este tutorial, você precisa de uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="f399c-111">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="f399c-112">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f399c-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f399c-113">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="f399c-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

## <a name="scenario-overview"></a><span data-ttu-id="f399c-114">Visão geral do cenário</span><span class="sxs-lookup"><span data-stu-id="f399c-114">Scenario overview</span></span>

<span data-ttu-id="f399c-115">Quando você implanta a solução pré-configurada de monitoramento remoto, ela é preenchida com recursos que permitem que você percorra um cenário comum de monitoramento remoto.</span><span class="sxs-lookup"><span data-stu-id="f399c-115">When you deploy the remote monitoring preconfigured solution, it is prepopulated with resources that enable you to step through a common remote monitoring scenario.</span></span> <span data-ttu-id="f399c-116">Nesse cenário, vários dispositivos conectados à solução estão relatando os valores de temperatura inesperados.</span><span class="sxs-lookup"><span data-stu-id="f399c-116">In this scenario, several devices connected to the solution are reporting unexpected temperature values.</span></span> <span data-ttu-id="f399c-117">As seções a seguir mostram como:</span><span class="sxs-lookup"><span data-stu-id="f399c-117">The following sections show you how to:</span></span>

* <span data-ttu-id="f399c-118">Identificar os dispositivos enviando valores de temperatura inesperados.</span><span class="sxs-lookup"><span data-stu-id="f399c-118">Identify the devices sending unexpected temperature values.</span></span>
* <span data-ttu-id="f399c-119">Configurar esses dispositivos para enviar telemetria mais detalhada.</span><span class="sxs-lookup"><span data-stu-id="f399c-119">Configure these devices to send more detailed telemetry.</span></span>
* <span data-ttu-id="f399c-120">Corrigir o problema atualizando o firmware nesses dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f399c-120">Fix the problem by updating the firmware on these devices.</span></span>
* <span data-ttu-id="f399c-121">Verificar se o problema foi resolvido por sua ação.</span><span class="sxs-lookup"><span data-stu-id="f399c-121">Verify that your action has resolved the issue.</span></span>

<span data-ttu-id="f399c-122">Um recurso-chave desse cenário é que você pode executar todas essas ações remotamente no painel da solução.</span><span class="sxs-lookup"><span data-stu-id="f399c-122">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span></span> <span data-ttu-id="f399c-123">Não é necessário acesso físico aos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f399c-123">You do not need physical access to the devices.</span></span>

## <a name="view-the-solution-dashboard"></a><span data-ttu-id="f399c-124">Exibir o painel de solução</span><span class="sxs-lookup"><span data-stu-id="f399c-124">View the solution dashboard</span></span>

<span data-ttu-id="f399c-125">O painel de solução permite que você gerencie a solução implantada.</span><span class="sxs-lookup"><span data-stu-id="f399c-125">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="f399c-126">Por exemplo, você pode exibir telemetria, adicionar dispositivos e configurar regras.</span><span class="sxs-lookup"><span data-stu-id="f399c-126">For example, you can view telemetry, add devices, and configure rules.</span></span>

1. <span data-ttu-id="f399c-127">Quando o provisionamento for concluído e o bloco da solução pré-configurada indicar **Pronto**, escolha **Iniciar** para abrir o portal de solução de monitoramento remoto em uma nova guia.</span><span class="sxs-lookup"><span data-stu-id="f399c-127">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your remote monitoring solution portal in a new tab.</span></span>

    ![Iniciar a solução pré-configurada][img-launch-solution]

1. <span data-ttu-id="f399c-129">Por padrão, o portal de solução mostra o *painel*.</span><span class="sxs-lookup"><span data-stu-id="f399c-129">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="f399c-130">Você pode navegar para outras áreas do portal de solução usando o menu ao lado esquerdo da página.</span><span class="sxs-lookup"><span data-stu-id="f399c-130">You can navigate to other areas of the solution portal using the menu on the left-hand side of the page.</span></span>

    ![Painel de solução pré-configurada de monitoramento remoto][img-menu]

<span data-ttu-id="f399c-132">O painel exibe as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="f399c-132">The dashboard displays the following information:</span></span>

* <span data-ttu-id="f399c-133">Um mapa que exibe o local de cada dispositivo conectado à solução.</span><span class="sxs-lookup"><span data-stu-id="f399c-133">A map that displays the location of each device connected to the solution.</span></span> <span data-ttu-id="f399c-134">Quando você executa a solução, há 25 dispositivos simulados.</span><span class="sxs-lookup"><span data-stu-id="f399c-134">When you first run the solution, there are 25 simulated devices.</span></span> <span data-ttu-id="f399c-135">Os dispositivos simulados são implementados como trabalhos Web do Azure e a solução usa a API do Bing Mapas para plotar informações no mapa.</span><span class="sxs-lookup"><span data-stu-id="f399c-135">The simulated devices are implemented as Azure WebJobs, and the solution uses the Bing Maps API to plot information on the map.</span></span> <span data-ttu-id="f399c-136">Confira as [Perguntas frequentes][lnk-faq] para aprender a fazer o mapa dinâmico.</span><span class="sxs-lookup"><span data-stu-id="f399c-136">See the [FAQ][lnk-faq] to learn how to make the map dynamic.</span></span>
* <span data-ttu-id="f399c-137">Um painel **Histórico de Telemetria** que plota telemetria de umidade e temperatura de um dispositivo selecionado em tempo quase real e exibe dados de agregação, como umidade média, mínima e máxima.</span><span class="sxs-lookup"><span data-stu-id="f399c-137">A **Telemetry History** panel that plots humidity and temperature telemetry from a selected device in near real time and displays aggregate data such as maximum, minimum, and average humidity.</span></span>
* <span data-ttu-id="f399c-138">Um painel **Histórico de Alarme** que mostra eventos recentes de alarme quando um valor de telemetria excedeu um limite.</span><span class="sxs-lookup"><span data-stu-id="f399c-138">An **Alarm History** panel that shows recent alarm events when a telemetry value has exceeded a threshold.</span></span> <span data-ttu-id="f399c-139">Você pode definir seus próprios alarmes além dos exemplos criados pela solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="f399c-139">You can define your own alarms in addition to the examples created by the preconfigured solution.</span></span>
* <span data-ttu-id="f399c-140">Um painel **Trabalhos** que exibe informações sobre os trabalhos agendados.</span><span class="sxs-lookup"><span data-stu-id="f399c-140">A **Jobs** panel that displays information about scheduled jobs.</span></span> <span data-ttu-id="f399c-141">Você pode agendar seus próprios trabalhos na página **Trabalhos de gerenciamento**.</span><span class="sxs-lookup"><span data-stu-id="f399c-141">You can schedule your own jobs on **Management jobs** page.</span></span>

## <a name="view-alarms"></a><span data-ttu-id="f399c-142">Exibir alarmes</span><span class="sxs-lookup"><span data-stu-id="f399c-142">View alarms</span></span>

<span data-ttu-id="f399c-143">O painel do histórico de alarme mostra que cinco dispositivos estão relatando valores de telemetria maiores que o esperado.</span><span class="sxs-lookup"><span data-stu-id="f399c-143">The alarm history panel shows you that five devices are reporting higher than expected telemetry values.</span></span>

![Histórico de Alarme TODO no painel de solução][img-alarms]

> [!NOTE]
> <span data-ttu-id="f399c-145">Esses alarmes são gerados por uma regra que está incluída na solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="f399c-145">These alarms are generated by a rule that is included in the preconfigured solution.</span></span> <span data-ttu-id="f399c-146">Essa regra gera um alerta quando o valor de temperatura enviado por um dispositivo excede 60.</span><span class="sxs-lookup"><span data-stu-id="f399c-146">This rule generates an alert when the temperature value sent by a device exceeds 60.</span></span> <span data-ttu-id="f399c-147">Você pode definir suas próprias regras e ações escolhendo [Regras](#add-a-rule) e [Ações](#add-an-action) no menu esquerdo.</span><span class="sxs-lookup"><span data-stu-id="f399c-147">You can define your own rules and actions by choosing [Rules](#add-a-rule) and [Actions](#add-an-action) in the left-hand menu.</span></span>

## <a name="view-devices"></a><span data-ttu-id="f399c-148">Exibir dispositivos</span><span class="sxs-lookup"><span data-stu-id="f399c-148">View devices</span></span>

<span data-ttu-id="f399c-149">A lista de *dispositivos* mostra todos os dispositivos registrados na solução.</span><span class="sxs-lookup"><span data-stu-id="f399c-149">The *devices* list shows all the registered devices in the solution.</span></span> <span data-ttu-id="f399c-150">Na lista de dispositivos, você pode exibir e editar os metadados do dispositivo, adicionar ou remover os dispositivos e chamar métodos nos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f399c-150">From the device list you can view and edit device metadata, add or remove devices, and invoke methods on devices.</span></span> <span data-ttu-id="f399c-151">Você pode filtrar e classificar a lista de dispositivos na lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f399c-151">You can filter and sort the list of devices in the device list.</span></span> <span data-ttu-id="f399c-152">Você também pode personalizar as colunas mostradas na lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f399c-152">You can also customize the columns shown in the device list.</span></span>

1. <span data-ttu-id="f399c-153">Escolha **Dispositivos** para mostrar a lista de dispositivos para esta solução.</span><span class="sxs-lookup"><span data-stu-id="f399c-153">Choose **Devices** to show the device list for this solution.</span></span>

   ![Exiba a lista de dispositivos no portal de solução][img-devicelist]

1. <span data-ttu-id="f399c-155">A lista de dispositivos mostra inicialmente 25 dispositivos simulados criados pelo processo de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="f399c-155">The device list initially shows 25 simulated devices created by the provisioning process.</span></span> <span data-ttu-id="f399c-156">Você pode adicionar dispositivos simulados e físicos extras à solução.</span><span class="sxs-lookup"><span data-stu-id="f399c-156">You can add additional simulated and physical devices to the solution.</span></span>

1. <span data-ttu-id="f399c-157">Clique em um dispositivo na lista de dispositivos para exibir os respectivos detalhes.</span><span class="sxs-lookup"><span data-stu-id="f399c-157">To view the details of a device, choose a device in the device list.</span></span>

   ![Exiba os detalhes do dispositivo no portal de solução][img-devicedetails]

<span data-ttu-id="f399c-159">O painel **Detalhes do Dispositivo** contém seis seções:</span><span class="sxs-lookup"><span data-stu-id="f399c-159">The **Device Details** panel contains six sections:</span></span>

* <span data-ttu-id="f399c-160">Uma coleção de links que permite personalizar o ícone do dispositivo, desabilitar o dispositivo, adicionar uma regra, chamar um método ou enviar um comando.</span><span class="sxs-lookup"><span data-stu-id="f399c-160">A collection of links that enable you to customize the device icon, disable the device, add a rule, invoke a method, or send a command.</span></span> <span data-ttu-id="f399c-161">Para ter uma comparação de comandos (mensagens do dispositivo para nuvem) e métodos (métodos diretos), consulte [Orientação para comunicações entre o dispositivo e a nuvem][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="f399c-161">For a comparison of commands (device-to-cloud messages) and methods (direct methods), see [Cloud-to-device communications guidance][lnk-c2d-guidance].</span></span>
* <span data-ttu-id="f399c-162">A seção **Dispositivo Gêmeo - Marcações** permite editar os valores da marcação para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f399c-162">The **Device Twin - Tags** section enables you to edit tag values for the device.</span></span> <span data-ttu-id="f399c-163">Você pode exibir os valores da marcação na lista de dispositivos e usar tais valores para filtrar a lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f399c-163">You can display tag values in the device list and use tag values to filter the device list.</span></span>
* <span data-ttu-id="f399c-164">A seção **Dispositivo Gêmeo - Propriedades Desejadas** permite definir os valores da propriedade a ser enviados para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f399c-164">The **Device Twin - Desired Properties** section enables you to set property values to be sent to the device.</span></span>
* <span data-ttu-id="f399c-165">A seção **Dispositivo Gêmeo - Propriedades Relatadas** mostra os valores da propriedade enviados do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f399c-165">The **Device Twin - Reported Properties** section shows property values sent from the device.</span></span>
* <span data-ttu-id="f399c-166">A seção **Propriedades do Dispositivo** mostra as informações do registro de identidade, como a ID do dispositivo e as chaves de autenticação.</span><span class="sxs-lookup"><span data-stu-id="f399c-166">The **Device Properties** section shows information from the identity registry such as the device id and authentication keys.</span></span>
* <span data-ttu-id="f399c-167">A seção **Trabalhos Recentes** mostra as informações sobre qualquer trabalho destinado recentemente a esse dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f399c-167">The **Recent Jobs** section shows information about any jobs that have recently targeted this device.</span></span>

## <a name="filter-the-device-list"></a><span data-ttu-id="f399c-168">Filtrar a lista de dispositivos</span><span class="sxs-lookup"><span data-stu-id="f399c-168">Filter the device list</span></span>

<span data-ttu-id="f399c-169">Você pode usar um filtro para exibir apenas os dispositivos que estão enviando valores de temperatura inesperados.</span><span class="sxs-lookup"><span data-stu-id="f399c-169">You can use a filter to display only those devices that are sending unexpected temperature values.</span></span> <span data-ttu-id="f399c-170">A solução pré-configurada de monitoramento remoto inclui o filtro **Dispositivos sem integridade** para mostrar os dispositivos com um valor de temperatura médio maior que 60.</span><span class="sxs-lookup"><span data-stu-id="f399c-170">The remote monitoring preconfigured solution includes the **Unhealthy devices** filter to show devices with a mean temperature value greater than 60.</span></span> <span data-ttu-id="f399c-171">Você também pode [criar seus próprios filtros](#add-a-filter).</span><span class="sxs-lookup"><span data-stu-id="f399c-171">You can also [create your own filters](#add-a-filter).</span></span>

1. <span data-ttu-id="f399c-172">Escolha **Abrir filtro salvo** para exibir uma lista de filtros disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f399c-172">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="f399c-173">Escolha **Dispositivos sem integridade** para aplicar o filtro:</span><span class="sxs-lookup"><span data-stu-id="f399c-173">Then choose **Unhealthy devices** to apply the filter:</span></span>

    ![Exibir a lista de filtros][img-unhealthy-filter]

1. <span data-ttu-id="f399c-175">A lista de dispositivos agora mostra somente os dispositivos com um valor de temperatura média maior que 60.</span><span class="sxs-lookup"><span data-stu-id="f399c-175">The device list now shows only devices with a mean temperature value greater than 60.</span></span>

    ![Exibir a lista filtrada de dispositivo mostrando dispositivos sem integridade][img-filtered-unhealthy-list]

## <a name="update-desired-properties"></a><span data-ttu-id="f399c-177">Atualizar as propriedades desejadas</span><span class="sxs-lookup"><span data-stu-id="f399c-177">Update desired properties</span></span>

<span data-ttu-id="f399c-178">Você identificou agora um conjunto de dispositivos que precisam de correção.</span><span class="sxs-lookup"><span data-stu-id="f399c-178">You have now identified a set of devices that may need remediation.</span></span> <span data-ttu-id="f399c-179">No entanto, você decide se a frequência de dados de 15 segundos não é suficiente para um diagnóstico claro do problema.</span><span class="sxs-lookup"><span data-stu-id="f399c-179">However, you decide that the data frequency of 15 seconds is not sufficient for a clear diagnosis of the issue.</span></span> <span data-ttu-id="f399c-180">Alterando a frequência de telemetria para 5 segundos para fornecer a você mais pontos de dados para diagnosticar melhor o problema.</span><span class="sxs-lookup"><span data-stu-id="f399c-180">Changing the telemetry frequency to five seconds to provide you with more data points to better diagnose the issue.</span></span> <span data-ttu-id="f399c-181">Você pode enviar essa alteração de configuração para seus dispositivos remotos no portal de solução.</span><span class="sxs-lookup"><span data-stu-id="f399c-181">You can push this configuration change to your remote devices from the solution portal.</span></span> <span data-ttu-id="f399c-182">Você pode fazer a alteração uma vez, avaliar o impacto e, em seguida, agir nos resultados.</span><span class="sxs-lookup"><span data-stu-id="f399c-182">You can make the change once, evaluate the impact, and then act on the results.</span></span>

<span data-ttu-id="f399c-183">Siga estas etapas para executar um trabalho que altera a propriedade desejada **TelemetryInterval** para os dispositivos afetados.</span><span class="sxs-lookup"><span data-stu-id="f399c-183">Follow these steps to run a job that changes the **TelemetryInterval** desired property for the affected devices.</span></span> <span data-ttu-id="f399c-184">Quando os dispositivos recebem o novo valor de propriedade **TelemetryInterval**, eles alteram suas configurações para enviar telemetria a cada 5 segundos, em vez de a cada 15 segundos:</span><span class="sxs-lookup"><span data-stu-id="f399c-184">When the devices receive the new **TelemetryInterval** property value, they change their configuration to send telemetry every five seconds instead of every 15 seconds:</span></span>

1. <span data-ttu-id="f399c-185">Enquanto você está mostrando a lista de dispositivos não íntegros na lista de dispositivos, escolha **Agendador de trabalhos** e, em seguida, **Editar dispositivo Gêmeo**.</span><span class="sxs-lookup"><span data-stu-id="f399c-185">While you are showing the list of unhealthy devices in the device list, choose **Job Scheduler**, then **Edit Device Twin**.</span></span>

1. <span data-ttu-id="f399c-186">Chame o trabalho **Alterar intervalo de telemetria**.</span><span class="sxs-lookup"><span data-stu-id="f399c-186">Call the job **Change telemetry interval**.</span></span>

1. <span data-ttu-id="f399c-187">Altere o valor do nome da **Propriedade desejada** **desired.Config.TelemetryInterval** para cinco segundos.</span><span class="sxs-lookup"><span data-stu-id="f399c-187">Change the value of the **Desired Property** name **desired.Config.TelemetryInterval** to five seconds.</span></span>

1. <span data-ttu-id="f399c-188">Escolha **Agenda**.</span><span class="sxs-lookup"><span data-stu-id="f399c-188">Choose **Schedule**.</span></span>

    ![Altere a propriedade TelemetryInterval para cinco segundos][img-change-interval]

1. <span data-ttu-id="f399c-190">Monitore o progresso do trabalho na página **Trabalhos de Gerenciamento** no portal.</span><span class="sxs-lookup"><span data-stu-id="f399c-190">You can monitor the progress of the job on the **Management Jobs** page in the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="f399c-191">Se você quiser alterar um valor de propriedade desejada para um dispositivo individual, use a seção **Propriedades Desejadas** no painel **Detalhes do Dispositivo** em vez de executar um trabalho.</span><span class="sxs-lookup"><span data-stu-id="f399c-191">If you want to change a desired property value for an individual device, use the **Desired Properties** section in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="f399c-192">Esse trabalho define o valor da propriedade desejada **TelemetryInterval** no dispositivo gêmeo para todos os dispositivos selecionados pelo filtro.</span><span class="sxs-lookup"><span data-stu-id="f399c-192">This job sets the value of the **TelemetryInterval** desired property in the device twin for all the devices selected by the filter.</span></span> <span data-ttu-id="f399c-193">Os dispositivos recuperam esse valor do dispositivo gêmeo e atualizam seu comportamento.</span><span class="sxs-lookup"><span data-stu-id="f399c-193">The devices retrieve this value from the device twin and update their behavior.</span></span> <span data-ttu-id="f399c-194">Quando um dispositivo recupera e processa uma propriedade desejada do dispositivo gêmeo, ele define a propriedade de valor relatado correspondente.</span><span class="sxs-lookup"><span data-stu-id="f399c-194">When a device retrieves and processes a desired property from a device twin, it sets the corresponding reported value property.</span></span>

## <a name="invoke-methods"></a><span data-ttu-id="f399c-195">Invocar métodos</span><span class="sxs-lookup"><span data-stu-id="f399c-195">Invoke methods</span></span>

<span data-ttu-id="f399c-196">Enquanto o trabalho é executado, você observará na lista de dispositivos não íntegros que todos esses dispositivos têm versões de firmware antigas (abaixo da versão 1.6).</span><span class="sxs-lookup"><span data-stu-id="f399c-196">While the job runs, you notice in the list of unhealthy devices that all these devices have old (less than version 1.6) firmware versions.</span></span>

![Exiba a versão do firmware relatada para os dispositivos não íntegros][img-old-firmware]

<span data-ttu-id="f399c-198">Essa versão de firmware pode ser a causa raiz dos valores de temperatura inesperados porque você sabe que outros dispositivos íntegros foram atualizados recentemente para a versão 2.0.</span><span class="sxs-lookup"><span data-stu-id="f399c-198">This firmware version may be the root cause of the unexpected temperature values because you know that other healthy devices were recently updated to version 2.0.</span></span> <span data-ttu-id="f399c-199">Use o filtro interno **Dispositivos antigos do firmware** para identificar todos os dispositivos com versões antigas do firmware.</span><span class="sxs-lookup"><span data-stu-id="f399c-199">You can use the built-in **Old firmware devices** filter to identify any devices with old firmware versions.</span></span> <span data-ttu-id="f399c-200">No portal, você poderá atualizar remotamente todos os dispositivos ainda executando versões antigas de firmware:</span><span class="sxs-lookup"><span data-stu-id="f399c-200">From the portal, you can then remotely update all the devices still running old firmware versions:</span></span>

1. <span data-ttu-id="f399c-201">Escolha **Abrir filtro salvo** para exibir uma lista de filtros disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f399c-201">Choose **Open saved filter** to display a list of available filters.</span></span> <span data-ttu-id="f399c-202">Escolha **Dispositivos com firmware antigo** para aplicar o filtro:</span><span class="sxs-lookup"><span data-stu-id="f399c-202">Then choose **Old firmware devices** to apply the filter:</span></span>

    ![Exibir a lista de filtros][img-old-filter]

1. <span data-ttu-id="f399c-204">A lista de dispositivos agora mostra somente os dispositivos com versões antigas de firmware.</span><span class="sxs-lookup"><span data-stu-id="f399c-204">The device list now shows only devices with old firmware versions.</span></span> <span data-ttu-id="f399c-205">Essa lista inclui 5 dispositivos identificados pelo filtro **Dispositivos não íntegros** e 3 dispositivos adicionais:</span><span class="sxs-lookup"><span data-stu-id="f399c-205">This list includes the five devices identified by the **Unhealthy devices** filter and three additional devices:</span></span>

    ![Exibir a lista filtrada de dispositivo mostrando dispositivos antigos][img-filtered-old-list]

1. <span data-ttu-id="f399c-207">Escolha **Agendador de Trabalho** e, em seguida, **Chamar o Método**.</span><span class="sxs-lookup"><span data-stu-id="f399c-207">Choose **Job Scheduler**, then **Invoke Method**.</span></span>

1. <span data-ttu-id="f399c-208">Defina **Nome do Trabalho** para **Atualização do firmware para a versão 2.0**.</span><span class="sxs-lookup"><span data-stu-id="f399c-208">Set **Job Name** to **Firmware update to version 2.0**.</span></span>

1. <span data-ttu-id="f399c-209">Escolha **InitiateFirmwareUpdate** como o **Método**.</span><span class="sxs-lookup"><span data-stu-id="f399c-209">Choose **InitiateFirmwareUpdate** as the **Method**.</span></span>

1. <span data-ttu-id="f399c-210">Defina o parâmetro **FwPackageUri** para **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span><span class="sxs-lookup"><span data-stu-id="f399c-210">Set the **FwPackageUri** parameter to **https://iotrmassets.blob.core.windows.net/firmwares/FW20.bin**.</span></span>

1. <span data-ttu-id="f399c-211">Escolha **Agenda**.</span><span class="sxs-lookup"><span data-stu-id="f399c-211">Choose **Schedule**.</span></span> <span data-ttu-id="f399c-212">O padrão é para que o trabalho seja executado agora.</span><span class="sxs-lookup"><span data-stu-id="f399c-212">The default is for the job to run now.</span></span>

    ![Crie um trabalho para atualizar o firmware dos dispositivos selecionados][img-method-update]

> [!NOTE]
> <span data-ttu-id="f399c-214">Se você deseja invocar um método em um dispositivo individual, escolha **Métodos** no painel **Detalhes do Dispositivo** em vez de executar um trabalho.</span><span class="sxs-lookup"><span data-stu-id="f399c-214">If you want to invoke a method on an individual device, choose **Methods** in the **Device Details** panel instead of running a job.</span></span>

<span data-ttu-id="f399c-215">Esse trabalho invoca o método direto **InitiateFirmwareUpdate** em todos os dispositivos selecionados pelo filtro.</span><span class="sxs-lookup"><span data-stu-id="f399c-215">This job invokes the **InitiateFirmwareUpdate** direct method on all the devices selected by the filter.</span></span> <span data-ttu-id="f399c-216">Os dispositivos respondem imediatamente ao Hub IoT e, em seguida, iniciam o processo de atualização de firmware assincronamente.</span><span class="sxs-lookup"><span data-stu-id="f399c-216">Devices respond immediately to IoT Hub and then initiate the firmware update process asynchronously.</span></span> <span data-ttu-id="f399c-217">Os dispositivos fornecem informações de status sobre o processo de atualização de firmware através de valores de propriedade relatados, conforme mostrado nas capturas de tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="f399c-217">The devices provide status information about the firmware update process through reported property values, as shown in the following screenshots.</span></span> <span data-ttu-id="f399c-218">Escolha o ícone **Atualizar** para atualizar as informações nas listas de dispositivo e de trabalho:</span><span class="sxs-lookup"><span data-stu-id="f399c-218">Choose the **Refresh** icon to update the information in the device and job lists:</span></span>

<span data-ttu-id="f399c-219">![Lista de trabalho, mostrando a lista de atualização de firmware em execução][img-update-1]
![Lista de dispositivos, mostrando o status de atualização de firmware][img-update-2]
![Lista de trabalho, mostrando a lista de atualização de firmware concluída][img-update-3]</span><span class="sxs-lookup"><span data-stu-id="f399c-219">![Job list showing the firmware update list running][img-update-1]
![Device list showing firmware update status][img-update-2]
![Job list showing the firmware update list complete][img-update-3]</span></span>

> [!NOTE]
> <span data-ttu-id="f399c-220">Em um ambiente de produção, você pode agendar trabalhos para execução durante uma janela de manutenção designada.</span><span class="sxs-lookup"><span data-stu-id="f399c-220">In a production environment, you can schedule jobs to run during a designated maintenance window.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="f399c-221">Análise do cenário</span><span class="sxs-lookup"><span data-stu-id="f399c-221">Scenario review</span></span>

<span data-ttu-id="f399c-222">Nesse cenário, você identificou um problema potencial com alguns de seus dispositivos remotos usando o histórico de alarme no painel e um filtro.</span><span class="sxs-lookup"><span data-stu-id="f399c-222">In this scenario, you identified a potential issue with some of your remote devices using the alarm history on the dashboard and a filter.</span></span> <span data-ttu-id="f399c-223">Você então usou o filtro e um trabalho para configurar remotamente os dispositivos para fornecer mais informações para ajudar a diagnosticar o problema.</span><span class="sxs-lookup"><span data-stu-id="f399c-223">You then used the filter and a job to remotely configure the devices to provide more information to help diagnose the issue.</span></span> <span data-ttu-id="f399c-224">Finalmente, você usou um filtro e um trabalho para agendar a manutenção nos dispositivos afetados.</span><span class="sxs-lookup"><span data-stu-id="f399c-224">Finally, you used a filter and a job to schedule maintenance on the affected devices.</span></span> <span data-ttu-id="f399c-225">Se você retornar para o painel, poderá verificar que não há alarmes provenientes de dispositivos em sua solução.</span><span class="sxs-lookup"><span data-stu-id="f399c-225">If you return to the dashboard, you can check that there are no longer any alarms coming from devices in your solution.</span></span> <span data-ttu-id="f399c-226">Você pode usar um filtro para verificar se o firmware está atualizado em todos os dispositivos da sua solução e que não há mais dispositivos não íntegros:</span><span class="sxs-lookup"><span data-stu-id="f399c-226">You can use a filter to verify that the firmware is up-to-date on all the devices in your solution and that there are no more unhealthy devices:</span></span>

![Filtro mostrando que todos os dispositivos têm um firmware atualizado][img-updated]

![Filtro mostrando que todos os dispositivos estão íntegros][img-healthy]

## <a name="other-features"></a><span data-ttu-id="f399c-229">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="f399c-229">Other features</span></span>

<span data-ttu-id="f399c-230">As seções a seguir descrevem alguns recursos adicionais de solução pré-configurada de monitoramento remoto que não são descritos como parte do cenário anterior.</span><span class="sxs-lookup"><span data-stu-id="f399c-230">The following sections describe some additional features of the remote monitoring preconfigured solution that are not described as part of the previous scenario.</span></span>

### <a name="customize-columns"></a><span data-ttu-id="f399c-231">Personalizar colunas</span><span class="sxs-lookup"><span data-stu-id="f399c-231">Customize columns</span></span>

<span data-ttu-id="f399c-232">É possível personalizar as informações exibidas na lista de dispositivos clicando no **Editor de colunas**.</span><span class="sxs-lookup"><span data-stu-id="f399c-232">You can customize the information shown in the device list by choosing **Column editor**.</span></span> <span data-ttu-id="f399c-233">Você pode adicionar e remover as colunas que exibem os valores de propriedade e marcação relatados.</span><span class="sxs-lookup"><span data-stu-id="f399c-233">You can add and remove columns that display reported property and tag values.</span></span> <span data-ttu-id="f399c-234">Também pode reorganizar e renomear as colunas:</span><span class="sxs-lookup"><span data-stu-id="f399c-234">You can also reorder and rename columns:</span></span>

   ![Editor de colunas na lista de dispositivos][img-columneditor]

### <a name="customize-the-device-icon"></a><span data-ttu-id="f399c-236">Personalizar o ícone do dispositivo</span><span class="sxs-lookup"><span data-stu-id="f399c-236">Customize the device icon</span></span>

<span data-ttu-id="f399c-237">Você pode personalizar o ícone do dispositivo exibido na lista de dispositivos no painel **Detalhes do Dispositivo** como a seguir:</span><span class="sxs-lookup"><span data-stu-id="f399c-237">You can customize the device icon displayed in the device list from the **Device Details** panel as follows:</span></span>

1. <span data-ttu-id="f399c-238">Escolha o ícone de lápis para abrir o painel **Editar imagem** de um dispositivo:</span><span class="sxs-lookup"><span data-stu-id="f399c-238">Choose the pencil icon to open the **Edit image** panel for a device:</span></span>

   ![Abrir o editor de imagens do dispositivo][img-startimageedit]

1. <span data-ttu-id="f399c-240">Carregue uma nova imagem ou use uma das imagens existentes e, em seguida, escolha **Salvar**:</span><span class="sxs-lookup"><span data-stu-id="f399c-240">Either upload a new image or use one of the existing images and then choose **Save**:</span></span>

   ![Editar o editor de imagens do dispositivo][img-imageedit]

1. <span data-ttu-id="f399c-242">A imagem selecionada agora é exibida na coluna **Ícone** do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f399c-242">The image you selected now displays in the **Icon** column for the device.</span></span>

> [!NOTE]
> <span data-ttu-id="f399c-243">A imagem é colocada no armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="f399c-243">The image is stored in blob storage.</span></span> <span data-ttu-id="f399c-244">Uma marcação no dispositivo gêmeo contém um link para a imagem no armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="f399c-244">A tag in the device twin contains a link to the image in blob storage.</span></span>

### <a name="add-a-device"></a><span data-ttu-id="f399c-245">Adicionar um dispositivo</span><span class="sxs-lookup"><span data-stu-id="f399c-245">Add a device</span></span>

<span data-ttu-id="f399c-246">Ao implantar a solução pré-configurada, você provisiona automaticamente os 25 dispositivos de exemplo exibidos na lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f399c-246">When you deploy the preconfigured solution, you automatically provision 25 sample devices that you can see in the device list.</span></span> <span data-ttu-id="f399c-247">Esses dispositivos são *dispositivos simulados* em execução em um Trabalho Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="f399c-247">These devices are *simulated devices* running in an Azure WebJob.</span></span> <span data-ttu-id="f399c-248">Com os dispositivos simulados, você pode experimentar mais facilmente a solução pré-configurada sem a necessidade de implantar dispositivos físicos reais.</span><span class="sxs-lookup"><span data-stu-id="f399c-248">Simulated devices make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical devices.</span></span> <span data-ttu-id="f399c-249">Se você quiser conectar um dispositivo real à solução, confira o tutorial [Conectar o dispositivo à solução pré-configurada de monitoramento remoto][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="f399c-249">If you do want to connect a real device to the solution, see the [Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm] tutorial.</span></span>

<span data-ttu-id="f399c-250">As etapas a seguir mostram como adicionar um dispositivo simulado à solução:</span><span class="sxs-lookup"><span data-stu-id="f399c-250">The following steps show you how to add a simulated device to the solution:</span></span>

1. <span data-ttu-id="f399c-251">Navegue de volta para a lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f399c-251">Navigate back to the device list.</span></span>

1. <span data-ttu-id="f399c-252">Para adicionar um dispositivo, escolha **+ Adicionar um Dispositivo** no canto inferior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="f399c-252">To add a device, choose **+ Add A Device** in the bottom left corner.</span></span>

   ![Adicionar um dispositivo à solução pré-configurada][img-adddevice]

1. <span data-ttu-id="f399c-254">Escolha **Adicionar Novo** no bloco **Dispositivo Simulado**.</span><span class="sxs-lookup"><span data-stu-id="f399c-254">Choose **Add New** on the **Simulated Device** tile.</span></span>

   ![Definir novos detalhes do dispositivo no painel][img-addnew]

   <span data-ttu-id="f399c-256">Além de criar um novo dispositivo simulado, você também poderá adicionar um dispositivo físico se optar por criar um **Dispositivo Personalizado**.</span><span class="sxs-lookup"><span data-stu-id="f399c-256">In addition to creating a new simulated device, you can also add a physical device if you choose to create a **Custom Device**.</span></span> <span data-ttu-id="f399c-257">Para saber mais sobre como conectar dispositivos físicos à solução, confira [Conectar o dispositivo à solução pré-configurada de monitoramento remoto do IoT Suite][lnk-connect-rm].</span><span class="sxs-lookup"><span data-stu-id="f399c-257">To learn more about connecting physical devices to the solution, see [Connect your device to the IoT Suite remote monitoring preconfigured solution][lnk-connect-rm].</span></span>

1. <span data-ttu-id="f399c-258">Selecione **Deixe-me definir minha própria ID** de dispositivo e adicione um nome de ID de dispositivo exclusivo, como **mydevice_01**.</span><span class="sxs-lookup"><span data-stu-id="f399c-258">Select **Let me define my own Device ID**, and enter a unique device ID name such as **mydevice_01**.</span></span>

1. <span data-ttu-id="f399c-259">Escolha **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f399c-259">Choose **Create**.</span></span>

   ![Salvar um novo dispositivo][img-definedevice]

1. <span data-ttu-id="f399c-261">Na etapa 3 de **Adicionar um dispositivo simulado**, escolha **Concluído** para retornar à lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f399c-261">In step 3 of **Add a simulated device**, choose **Done** to return to the device list.</span></span>

1. <span data-ttu-id="f399c-262">Você pode exibir o dispositivo **Executando** na lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f399c-262">You can view your device **Running** in the device list.</span></span>

    ![Exibir novo dispositivo na lista de dispositivos][img-runningnew]

1. <span data-ttu-id="f399c-264">Você também pode exibir a telemetria simulada do novo dispositivo no painel:</span><span class="sxs-lookup"><span data-stu-id="f399c-264">You can also view the simulated telemetry from your new device on the dashboard:</span></span>

    ![Exibir telemetria do novo dispositivo][img-runningnew-2]

### <a name="disable-and-delete-a-device"></a><span data-ttu-id="f399c-266">Desabilitar e excluir um dispositivo</span><span class="sxs-lookup"><span data-stu-id="f399c-266">Disable and delete a device</span></span>

<span data-ttu-id="f399c-267">Você pode desabilitar um dispositivo e depois que ele for desabilitado, poderá removê-lo:</span><span class="sxs-lookup"><span data-stu-id="f399c-267">You can disable a device, and after it is disabled you can remove it:</span></span>

![Desabilitar e remover um dispositivo][img-disable]

### <a name="add-a-rule"></a><span data-ttu-id="f399c-269">Adicionar uma regra</span><span class="sxs-lookup"><span data-stu-id="f399c-269">Add a rule</span></span>

<span data-ttu-id="f399c-270">Não existem regras para o novo dispositivo recém-adicionado.</span><span class="sxs-lookup"><span data-stu-id="f399c-270">There are no rules for the new device you just added.</span></span> <span data-ttu-id="f399c-271">Nesta seção, você adiciona uma regra que dispara um alarme quando a temperatura relatada pelo novo dispositivo excede 47 graus.</span><span class="sxs-lookup"><span data-stu-id="f399c-271">In this section, you add a rule that triggers an alarm when the temperature reported by the new device exceeds 47 degrees.</span></span> <span data-ttu-id="f399c-272">Antes de começar, observe que o histórico de telemetria para o novo dispositivo no painel mostra que a temperatura do dispositivo nunca excede 45 graus.</span><span class="sxs-lookup"><span data-stu-id="f399c-272">Before you start, notice that the telemetry history for the new device on the dashboard shows the device temperature never exceeds 45 degrees.</span></span>

1. <span data-ttu-id="f399c-273">Navegue de volta para a lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f399c-273">Navigate back to the device list.</span></span>

1. <span data-ttu-id="f399c-274">Para adicionar uma regra do dispositivo, selecione o novo dispositivo na **Lista de Dispositivos** e escolha **Adicionar regra**.</span><span class="sxs-lookup"><span data-stu-id="f399c-274">To add a rule for the device, select your new device in the **Devices List**, and then choose **Add rule**.</span></span>

1. <span data-ttu-id="f399c-275">Crie uma regra que usa **Temperature** como o campo de dados e **AlarmTemp** como a saída quando a temperatura excede 47 graus:</span><span class="sxs-lookup"><span data-stu-id="f399c-275">Create a rule that uses **Temperature** as the data field and uses **AlarmTemp** as the output when the temperature exceeds 47 degrees:</span></span>

    ![Adicionar uma regra de dispositivo][img-adddevicerule]

1. <span data-ttu-id="f399c-277">Para salvar suas alterações, escolha **Salvar e Exibir Regras**.</span><span class="sxs-lookup"><span data-stu-id="f399c-277">To save your changes, choose **Save and View Rules**.</span></span>

1. <span data-ttu-id="f399c-278">Clique em **Comandos** no painel de detalhes do novo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f399c-278">Choose **Commands** in the device details pane for the new device.</span></span>

    ![Adicionar uma regra de dispositivo][img-adddevicerule2]

1. <span data-ttu-id="f399c-280">Selecione **ChangeSetPointTemp** na lista de comandos e defina **SetPointTemp** como 45.</span><span class="sxs-lookup"><span data-stu-id="f399c-280">Select **ChangeSetPointTemp** from the command list and set **SetPointTemp** to 45.</span></span> <span data-ttu-id="f399c-281">Escolha **Enviar Comando**:</span><span class="sxs-lookup"><span data-stu-id="f399c-281">Then choose **Send Command**:</span></span>

    ![Adicionar uma regra de dispositivo][img-adddevicerule3]

1. <span data-ttu-id="f399c-283">Navegue até o painel.</span><span class="sxs-lookup"><span data-stu-id="f399c-283">Navigate back to the dashboard.</span></span> <span data-ttu-id="f399c-284">Após um curto período, você verá uma nova entrada no painel **Histórico de Alarme** quando a temperatura relatada pelo seu novo dispositivo exceder o limite de 47 graus:</span><span class="sxs-lookup"><span data-stu-id="f399c-284">After a short time, you will see a new entry in the **Alarm History** pane when the temperature reported by your new device exceeds the 47-degree threshold:</span></span>

    ![Adicionar uma regra de dispositivo][img-adddevicerule4]

1. <span data-ttu-id="f399c-286">Você pode revisar e editar todas as regras na página **Regras** do painel:</span><span class="sxs-lookup"><span data-stu-id="f399c-286">You can review and edit all your rules on the **Rules** page of the dashboard:</span></span>

    ![Listar regras de dispositivo][img-rules]

1. <span data-ttu-id="f399c-288">Você pode revisar e editar todas as ações que podem ser realizadas em resposta a uma regra na página **Ações** do painel:</span><span class="sxs-lookup"><span data-stu-id="f399c-288">You can review and edit all the actions that can be taken in response to a rule on the **Actions** page of the dashboard:</span></span>

    ![Listar ações de dispositivo][img-actions]

> [!NOTE]
> <span data-ttu-id="f399c-290">É possível definir ações que podem enviar uma mensagem de email ou SMS em resposta a uma regra ou se integrar com um sistema de linha de negócios por meio de um [Aplicativo Lógico][lnk-logic-apps].</span><span class="sxs-lookup"><span data-stu-id="f399c-290">It is possible to define actions that can send an email message or SMS in response to a rule or integrate with a line-of-business system through a [Logic App][lnk-logic-apps].</span></span> <span data-ttu-id="f399c-291">Para obter mais informações, confira [Conectar o Aplicativo Lógico à solução pré-configurada de monitoramento remoto do Azure IoT Suite][lnk-logicapptutorial].</span><span class="sxs-lookup"><span data-stu-id="f399c-291">For more information, see the [Connect Logic App to your Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logicapptutorial].</span></span>

### <a name="manage-filters"></a><span data-ttu-id="f399c-292">Gerenciar filtros</span><span class="sxs-lookup"><span data-stu-id="f399c-292">Manage filters</span></span>

<span data-ttu-id="f399c-293">Na lista de dispositivos, você pode criar, salvar e recarregar os filtros para exibir uma lista personalizada de dispositivos conectados ao hub.</span><span class="sxs-lookup"><span data-stu-id="f399c-293">In the device list, you can create, save, and reload filters to display a customized list of devices connected to your hub.</span></span> <span data-ttu-id="f399c-294">Para criar um filtro:</span><span class="sxs-lookup"><span data-stu-id="f399c-294">To create a filter:</span></span>

1. <span data-ttu-id="f399c-295">Escolha o ícone para editar o filtro acima da lista de dispositivos:</span><span class="sxs-lookup"><span data-stu-id="f399c-295">Choose the edit filter icon above the list of devices:</span></span>

    ![Abrir o editor de filtro][img-editfiltericon]

1. <span data-ttu-id="f399c-297">No **Editor de filtro**, adicione os campos, operadores e valores para filtrar a lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f399c-297">In the **Filter editor**, add the fields, operators, and values to filter the device list.</span></span> <span data-ttu-id="f399c-298">Você pode adicionar várias cláusulas para refinar seu filtro.</span><span class="sxs-lookup"><span data-stu-id="f399c-298">You can add multiple clauses to refine your filter.</span></span> <span data-ttu-id="f399c-299">Escolha **Filtrar** para aplicar o filtro:</span><span class="sxs-lookup"><span data-stu-id="f399c-299">Choose **Filter** to apply the filter:</span></span>

    ![Crie um filtro][img-filtereditor]

1. <span data-ttu-id="f399c-301">Neste exemplo, a lista é filtrada pelo fabricante e número do modelo:</span><span class="sxs-lookup"><span data-stu-id="f399c-301">In this example, the list is filtered by manufacturer and model number:</span></span>

    ![Lista filtrada][img-filterelist]

1. <span data-ttu-id="f399c-303">Para salvar seu filtro com um nome personalizado, escolha o ícone **Salvar como**:</span><span class="sxs-lookup"><span data-stu-id="f399c-303">To save your filter with a custom name, choose the **Save as** icon:</span></span>

    ![Salvar um filtro][img-savefilter]

1. <span data-ttu-id="f399c-305">Para reaplicar um filtro salvo anteriormente, escolha o ícone **Abrir filtro salvo**:</span><span class="sxs-lookup"><span data-stu-id="f399c-305">To reapply a filter you saved previously, choose the **Open saved filter** icon:</span></span>

    ![Abrir um filtro][img-openfilter]

<span data-ttu-id="f399c-307">Você pode criar filtros com base na id do dispositivo, estado do dispositivo, propriedades desejadas, propriedades relatadas e marcações.</span><span class="sxs-lookup"><span data-stu-id="f399c-307">You can create filters based on device id, device state, desired properties, reported properties, and tags.</span></span> <span data-ttu-id="f399c-308">Adicione rótulos personalizados para um dispositivo na seção **Rótulos** do painel **Detalhes do Dispositivo** ou execute um trabalho para atualizar os rótulos em vários dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f399c-308">You add your own custom tags to a device in the **Tags** section of the **Device Details** panel, or run a job to update tags on multiple devices.</span></span>

> [!NOTE]
> <span data-ttu-id="f399c-309">No **Editor de filtro**, você pode usar a **Exibição avançada** para editar o texto da consulta diretamente.</span><span class="sxs-lookup"><span data-stu-id="f399c-309">In the **Filter editor**, you can use the **Advanced view** to edit the query text directly.</span></span>

### <a name="commands"></a><span data-ttu-id="f399c-310">Comandos</span><span class="sxs-lookup"><span data-stu-id="f399c-310">Commands</span></span>

<span data-ttu-id="f399c-311">No painel **Detalhes do Dispositivo**, você pode enviar comandos ao dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f399c-311">From the **Device Details** panel, you can send commands to the device.</span></span> <span data-ttu-id="f399c-312">Quando um dispositivo é iniciado, ele envia informações sobre os comandos a que ele dá suporte para a solução.</span><span class="sxs-lookup"><span data-stu-id="f399c-312">When a device first starts, it sends information about the commands it supports to the solution.</span></span> <span data-ttu-id="f399c-313">Para obter uma discussão sobre as diferenças entre os métodos e comandos, confira [Opções de nuvem para dispositivo do Hub IoT do Azure][lnk-c2d-guidance].</span><span class="sxs-lookup"><span data-stu-id="f399c-313">For a discussion of the differences between commands and methods, see [Azure IoT Hub cloud-to-device options][lnk-c2d-guidance].</span></span>

1. <span data-ttu-id="f399c-314">Escolha **Comandos** no painel **Detalhes do Dispositivo**  do dispositivo selecionado:</span><span class="sxs-lookup"><span data-stu-id="f399c-314">Choose **Commands** in the **Device Details** panel for the selected device:</span></span>

   ![Comandos de dispositivo no painel][img-devicecommands]

1. <span data-ttu-id="f399c-316">Selecione **PingDevice** na lista de comandos.</span><span class="sxs-lookup"><span data-stu-id="f399c-316">Select **PingDevice** from the command list.</span></span>

1. <span data-ttu-id="f399c-317">Escolha **Enviar Comando**.</span><span class="sxs-lookup"><span data-stu-id="f399c-317">Choose **Send Command**.</span></span>

1. <span data-ttu-id="f399c-318">Você pode ver o status do comando no histórico de comandos.</span><span class="sxs-lookup"><span data-stu-id="f399c-318">You can see the status of the command in the command history.</span></span>

   ![Status do comando no painel][img-pingcommand]

<span data-ttu-id="f399c-320">A solução rastreia o status de cada comando enviado.</span><span class="sxs-lookup"><span data-stu-id="f399c-320">The solution tracks the status of each command it sends.</span></span> <span data-ttu-id="f399c-321">Inicialmente, o resultado é **Pendente**.</span><span class="sxs-lookup"><span data-stu-id="f399c-321">Initially the result is **Pending**.</span></span> <span data-ttu-id="f399c-322">Quando o dispositivo relata que executou o comando, o resultado é definido como **Sucesso**.</span><span class="sxs-lookup"><span data-stu-id="f399c-322">When the device reports that it has executed the command, the result is set to **Success**.</span></span>

## <a name="behind-the-scenes"></a><span data-ttu-id="f399c-323">Nos bastidores</span><span class="sxs-lookup"><span data-stu-id="f399c-323">Behind the scenes</span></span>

<span data-ttu-id="f399c-324">Ao implantar uma solução pré-configurada, o processo de implantação criará vários recursos na assinatura do Azure que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="f399c-324">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span></span> <span data-ttu-id="f399c-325">Você pode exibir esses recursos no [portal][lnk-portal] do Azure.</span><span class="sxs-lookup"><span data-stu-id="f399c-325">You can view these resources in the Azure [portal][lnk-portal].</span></span> <span data-ttu-id="f399c-326">O processo de implantação cria um **grupo de recursos** com um nome baseado no nome escolhido para sua solução pré-configurada:</span><span class="sxs-lookup"><span data-stu-id="f399c-326">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span></span>

![Solução pré-configurada no portal do Azure][img-portal]

<span data-ttu-id="f399c-328">Você pode exibir as configurações de cada recurso selecionando-o na lista de recursos no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f399c-328">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span></span>

<span data-ttu-id="f399c-329">Você também pode exibir o código-fonte para a solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="f399c-329">You can also view the source code for the preconfigured solution.</span></span> <span data-ttu-id="f399c-330">O código-fonte da solução pré-configurada de monitoramento remoto está no repositório do GitHub [azure-iot-remote-monitoring][lnk-rmgithub]:</span><span class="sxs-lookup"><span data-stu-id="f399c-330">The remote monitoring preconfigured solution source code is in the [azure-iot-remote-monitoring][lnk-rmgithub] GitHub repository:</span></span>

* <span data-ttu-id="f399c-331">A pasta **DeviceAdministration** contém o código-fonte para o painel.</span><span class="sxs-lookup"><span data-stu-id="f399c-331">The **DeviceAdministration** folder contains the source code for the dashboard.</span></span>
* <span data-ttu-id="f399c-332">A pasta **Simulator** contém o código-fonte do dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="f399c-332">The **Simulator** folder contains the source code for the simulated device.</span></span>
* <span data-ttu-id="f399c-333">A pasta **EventProcessor** contém o código-fonte para o processo de back-end que manipula a telemetria de entrada.</span><span class="sxs-lookup"><span data-stu-id="f399c-333">The **EventProcessor** folder contains the source code for the back-end process that handles the incoming telemetry.</span></span>

<span data-ttu-id="f399c-334">Quando você terminar, poderá excluir a solução pré-configurada de sua assinatura do Azure no site [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="f399c-334">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="f399c-335">Esse site permite que você exclua facilmente todos os recursos que foram provisionados quando criou a solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="f399c-335">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="f399c-336">Para garantir que você excluirá tudo relacionado à solução pré-configurada, exclua-a no site [azureiotsuite.com][lnk-azureiotsuite] e não simplesmente exclua o grupo de recursos no portal.</span><span class="sxs-lookup"><span data-stu-id="f399c-336">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site and do not delete the resource group in the portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f399c-337">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f399c-337">Next Steps</span></span>

<span data-ttu-id="f399c-338">Agora que você implantou uma solução de trabalho pré-configurada, poderá continuar a introdução ao Suite IoT lendo os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="f399c-338">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="f399c-339">[Passo a passo da solução pré-configurada de monitoramento remoto][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="f399c-339">[Remote monitoring preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="f399c-340">[Conectar seu dispositivo à solução pré-configurada de monitoramento remoto][lnk-connect-rm]</span><span class="sxs-lookup"><span data-stu-id="f399c-340">[Connect your device to the remote monitoring preconfigured solution][lnk-connect-rm]</span></span>
* <span data-ttu-id="f399c-341">[Permissões no site azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="f399c-341">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

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