---
title: "Passo a passo da manutenção preditiva | Microsoft Docs"
description: "Um passo a passo da solução pré-configurada de manutenção preditiva do Azure IoT."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3c48a716-b805-4c99-8177-414cc4bec3de
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: a68a8fdc3976ade0d1036d5ed58c8b2eb6d32a5d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="predictive-maintenance-preconfigured-solution-walkthrough"></a><span data-ttu-id="f7edd-103">Passo a passo da solução pré-configurada de manutenção preditiva</span><span class="sxs-lookup"><span data-stu-id="f7edd-103">Predictive maintenance preconfigured solution walkthrough</span></span>

<span data-ttu-id="f7edd-104">A solução pré-configurada de manutenção preditiva é uma solução de ponta a ponta para um cenário comercial e prevê o ponto no qual há a probabilidade de ocorrer uma falha.</span><span class="sxs-lookup"><span data-stu-id="f7edd-104">The predictive maintenance preconfigured solution is an end-to-end solution for a business scenario that predicts the point at which a failure is likely to occur.</span></span> <span data-ttu-id="f7edd-105">Você pode usar essa solução pré-configurada de forma pró-ativa para atividades como a manutenção de otimização.</span><span class="sxs-lookup"><span data-stu-id="f7edd-105">You can use this preconfigured solution proactively for activities such as optimizing maintenance.</span></span> <span data-ttu-id="f7edd-106">A solução combina os principais serviços do Azure IoT Suite, como o IoT Hub, Stream Analytics e um espaço de trabalho do[Azure Machine Learning][lnk-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="f7edd-106">The solution combines key Azure IoT Suite services, such as IoT Hub, Stream analytics, and an [Azure Machine Learning][lnk-machine-learning] workspace.</span></span> <span data-ttu-id="f7edd-107">Esse espaço de trabalho contém um modelo, com base em um conjunto de dados de exemplo público, para prever a RUL (Vida Útil Restante) de um motor de aeronave.</span><span class="sxs-lookup"><span data-stu-id="f7edd-107">This workspace contains a model, based on a public sample data set, to predict the Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="f7edd-108">A solução implementa totalmente o cenário de negócios IoT como um ponto de partida para você planejar e implementar uma solução que atenda aos seus requisitos de negócios específicos.</span><span class="sxs-lookup"><span data-stu-id="f7edd-108">The solution fully implements the IoT business scenario as a starting point for you to plan and implement a solution that meets your own specific business requirements.</span></span>

## <a name="logical-architecture"></a><span data-ttu-id="f7edd-109">Arquitetura lógica</span><span class="sxs-lookup"><span data-stu-id="f7edd-109">Logical architecture</span></span>

<span data-ttu-id="f7edd-110">O seguinte diagrama descreve os componentes lógicos da solução pré-configurada:</span><span class="sxs-lookup"><span data-stu-id="f7edd-110">The following diagram outlines the logical components of the preconfigured solution:</span></span>

![][img-architecture]

<span data-ttu-id="f7edd-111">Os itens azuis são serviços do Azure provisionados na região em que você implantou a solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="f7edd-111">The blue items are Azure services provisioned in the region where you deployed the preconfigured solution.</span></span> <span data-ttu-id="f7edd-112">Exibe a lista de regiões em que você pode implantar a solução pré-configurado no [página provisionamento][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="f7edd-112">The list of regions where you can deploy the preconfigured solution displays on the [provisioning page][lnk-azureiotsuite].</span></span>

<span data-ttu-id="f7edd-113">O item em verde é um dispositivo simulado que representa um motor de aeronave.</span><span class="sxs-lookup"><span data-stu-id="f7edd-113">The green item is a simulated device that represents an aircraft engine.</span></span> <span data-ttu-id="f7edd-114">Você pode aprender mais sobre esses dispositivos simulados na seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="f7edd-114">You can learn more about these simulated devices in the following section.</span></span>

<span data-ttu-id="f7edd-115">Os itens em cinza representam os componentes que implementam os recursos de *gerenciamento do dispositivo*.</span><span class="sxs-lookup"><span data-stu-id="f7edd-115">The gray items represent components that implement *device management* capabilities.</span></span> <span data-ttu-id="f7edd-116">A versão atual da solução pré-configurada de manutenção preditiva não provisiona esses recursos.</span><span class="sxs-lookup"><span data-stu-id="f7edd-116">The current release of the predictive maintenance preconfigured solution does not provision these resources.</span></span> <span data-ttu-id="f7edd-117">Para saber mais sobre o gerenciamento do dispositivo, consulte a [solução pré-configurada de monitoramento remoto][lnk-remote-monitoring].</span><span class="sxs-lookup"><span data-stu-id="f7edd-117">To learn more about device management, refer to the [remote monitoring pre-configured solution][lnk-remote-monitoring].</span></span>

## <a name="simulated-devices"></a><span data-ttu-id="f7edd-118">Dispositivos simulados</span><span class="sxs-lookup"><span data-stu-id="f7edd-118">Simulated devices</span></span>

<span data-ttu-id="f7edd-119">Na solução pré-configurada, um dispositivo simulado representa um motor de aeronave.</span><span class="sxs-lookup"><span data-stu-id="f7edd-119">In the preconfigured solution, a simulated device represents an aircraft engine.</span></span> <span data-ttu-id="f7edd-120">A solução é provisionada com dois motores que mapeiam uma única aeronave.</span><span class="sxs-lookup"><span data-stu-id="f7edd-120">The solution is provisioned with two engines that map to a single aircraft.</span></span> <span data-ttu-id="f7edd-121">Cada motor emite quatro tipos de telemetria: o Sensor 9, Sensor 11, Sensor 14 e Sensor 15 fornecem os dados necessários para o modelo de Machine Learning calcular a RUL do motor.</span><span class="sxs-lookup"><span data-stu-id="f7edd-121">Each engine emits four types of telemetry: Sensor 9, Sensor 11, Sensor 14, and Sensor 15 provide the data necessary for the Machine Learning model to calculate the RUL for the engine.</span></span> <span data-ttu-id="f7edd-122">Cada dispositivo simulado envia as seguintes mensagens de telemetria ao Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="f7edd-122">Each simulated device sends the following telemetry messages to IoT Hub:</span></span>

<span data-ttu-id="f7edd-123">*Contagem de ciclos*.</span><span class="sxs-lookup"><span data-stu-id="f7edd-123">*Cycle count*.</span></span> <span data-ttu-id="f7edd-124">Um ciclo representa um voo concluído com uma duração entre duas e dez horas.</span><span class="sxs-lookup"><span data-stu-id="f7edd-124">A cycle represents a completed flight with a duration between two and ten hours.</span></span> <span data-ttu-id="f7edd-125">Durante o voo, dados de telemetria são capturados a cada meia hora.</span><span class="sxs-lookup"><span data-stu-id="f7edd-125">During the flight, telemetry data is captured every half hour.</span></span>

<span data-ttu-id="f7edd-126">*Telemetria*.</span><span class="sxs-lookup"><span data-stu-id="f7edd-126">*Telemetry*.</span></span> <span data-ttu-id="f7edd-127">Há quatro sensores que representam os atributos do motor.</span><span class="sxs-lookup"><span data-stu-id="f7edd-127">There are four sensors that represent engine attributes.</span></span> <span data-ttu-id="f7edd-128">Os sensores são rotulados genericamente de Sensor 9, Sensor 11, Sensor 14 e Sensor 15.</span><span class="sxs-lookup"><span data-stu-id="f7edd-128">The sensors are generically labeled Sensor 9, Sensor 11, Sensor 14, and Sensor 15.</span></span> <span data-ttu-id="f7edd-129">Esses quatro sensores representam telemetria suficiente para obter resultados úteis do modelo de regra.</span><span class="sxs-lookup"><span data-stu-id="f7edd-129">These four sensors represent telemetry sufficient to obtain useful results from the RUL model.</span></span> <span data-ttu-id="f7edd-130">O modelo usado na solução pré-configurada é criado de um conjunto de dados público que inclui dados de sensor do mecanismo real.</span><span class="sxs-lookup"><span data-stu-id="f7edd-130">The model used in the preconfigured solution is created from a public data set that includes real engine sensor data.</span></span> <span data-ttu-id="f7edd-131">Para saber mais sobre como o modelo foi criado no conjunto de dados original, confira o [Modelo de manutenção preditiva da Galeria do Cortana Intelligence][lnk-cortana-analytics].</span><span class="sxs-lookup"><span data-stu-id="f7edd-131">For more information on how the model was created from the original data set, see the [Cortana Intelligence Gallery Predictive Maintenance Template][lnk-cortana-analytics].</span></span>

<span data-ttu-id="f7edd-132">Os dispositivos simulados podem lidar com os seguintes comandos enviados do hub IoT na solução:</span><span class="sxs-lookup"><span data-stu-id="f7edd-132">The simulated devices can handle the following commands sent from the IoT hub in the solution:</span></span>

| <span data-ttu-id="f7edd-133">Command</span><span class="sxs-lookup"><span data-stu-id="f7edd-133">Command</span></span> | <span data-ttu-id="f7edd-134">Descrição</span><span class="sxs-lookup"><span data-stu-id="f7edd-134">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f7edd-135">StartTelemetry</span><span class="sxs-lookup"><span data-stu-id="f7edd-135">StartTelemetry</span></span> |<span data-ttu-id="f7edd-136">Controla o estado da simulação.</span><span class="sxs-lookup"><span data-stu-id="f7edd-136">Controls the state of the simulation.</span></span><br/><span data-ttu-id="f7edd-137">Inicia o dispositivo que envia a telemetria</span><span class="sxs-lookup"><span data-stu-id="f7edd-137">Starts the device sending telemetry</span></span> |
| <span data-ttu-id="f7edd-138">StopTelemetry</span><span class="sxs-lookup"><span data-stu-id="f7edd-138">StopTelemetry</span></span> |<span data-ttu-id="f7edd-139">Controla o estado da simulação.</span><span class="sxs-lookup"><span data-stu-id="f7edd-139">Controls the state of the simulation.</span></span><br/><span data-ttu-id="f7edd-140">Para o dispositivo que envia a telemetria</span><span class="sxs-lookup"><span data-stu-id="f7edd-140">Stops the device sending telemetry</span></span> |

<span data-ttu-id="f7edd-141">O Hub IoT fornece reconhecimento de comando do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f7edd-141">IoT Hub provides device command acknowledgment.</span></span>

## <a name="azure-stream-analytics-job"></a><span data-ttu-id="f7edd-142">Trabalho do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="f7edd-142">Azure Stream Analytics job</span></span>

<span data-ttu-id="f7edd-143">**Trabalho: Telemetria** funciona no fluxo de entrada da telemetria do dispositivo usando duas instruções:</span><span class="sxs-lookup"><span data-stu-id="f7edd-143">**Job: Telemetry** operates on the incoming device telemetry stream using two statements:</span></span>

* <span data-ttu-id="f7edd-144">O primeiro seleciona toda a telemetria dos dispositivos e envia os dados para o armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="f7edd-144">The first selects all telemetry from the devices and sends this data to blob storage.</span></span> <span data-ttu-id="f7edd-145">Aqui, ele é visualizado no aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="f7edd-145">From here, it is visualized in the web app.</span></span>
* <span data-ttu-id="f7edd-146">A segunda calcula os valores médios do sensor em uma janela deslizante de dois minutos e envia esses dados por meio do Hub de Eventos para um **processador de eventos**.</span><span class="sxs-lookup"><span data-stu-id="f7edd-146">The second computes average sensor values over a two-minute sliding window and sends this data through the Event hub to an **event processor**.</span></span>

## <a name="event-processor"></a><span data-ttu-id="f7edd-147">Processador de eventos</span><span class="sxs-lookup"><span data-stu-id="f7edd-147">Event processor</span></span>
<span data-ttu-id="f7edd-148">O **host do processador de eventos** é executado em um trabalho de Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7edd-148">The **event processor host** runs in an Azure Web Job.</span></span> <span data-ttu-id="f7edd-149">O **processador de eventos** obtém os valores do sensor médios para um ciclo completo.</span><span class="sxs-lookup"><span data-stu-id="f7edd-149">The **event processor** takes the average sensor values for a completed cycle.</span></span> <span data-ttu-id="f7edd-150">Ele passa esses valores para uma API que expõe o modelo treinado para calcular a RUL para um motor.</span><span class="sxs-lookup"><span data-stu-id="f7edd-150">It then passes those values to an API that exposes trained model to calculate the RUL for an engine.</span></span> <span data-ttu-id="f7edd-151">A API é exposta por um espaço de trabalho do Machine Learning é provisionado como parte da solução.</span><span class="sxs-lookup"><span data-stu-id="f7edd-151">The API is exposed by a Machine Learning workspace that is provisioned as part of the solution.</span></span>

## <a name="machine-learning"></a><span data-ttu-id="f7edd-152">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f7edd-152">Machine Learning</span></span>
<span data-ttu-id="f7edd-153">O componente de Machine Learning usa um modelo derivado dos dados coletados de mecanismos de aeronave real.</span><span class="sxs-lookup"><span data-stu-id="f7edd-153">The Machine Learning component uses a model derived from data collected from real aircraft engines.</span></span> <span data-ttu-id="f7edd-154">Você pode navegar até o Espaço de Trabalho do Machine Learning do bloco na página [azureiotsuite.com][lnk-azureiotsuite] para sua solução provisionada.</span><span class="sxs-lookup"><span data-stu-id="f7edd-154">You can navigate to the Machine Learning workspace from the tile on the [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="f7edd-155">O bloco fica disponível quando a solução fica no estado **Pronto**.</span><span class="sxs-lookup"><span data-stu-id="f7edd-155">The tile is available when the solution is in the **Ready** state.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f7edd-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f7edd-156">Next steps</span></span>
<span data-ttu-id="f7edd-157">Agora você já viu os principais componentes da solução de previsão manutenção pré-configurado, convém personalizá-lo.</span><span class="sxs-lookup"><span data-stu-id="f7edd-157">Now you've seen the key components of the predictive maintenance preconfigured solution, you may want to customize it.</span></span> <span data-ttu-id="f7edd-158">Veja [Orientação sobre como personalizar soluções pré-configuradas][lnk-customize].</span><span class="sxs-lookup"><span data-stu-id="f7edd-158">See [Guidance on customizing preconfigured solutions][lnk-customize].</span></span>

<span data-ttu-id="f7edd-159">Você também pode explorar alguns dos outros recursos das soluções pré-configuradas do IoT Suite:</span><span class="sxs-lookup"><span data-stu-id="f7edd-159">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="f7edd-160">[Perguntas frequentes sobre o IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="f7edd-160">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="f7edd-161">[Segurança IoT desde o início][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="f7edd-161">[IoT security from the ground up][lnk-security-groundup]</span></span>

[img-architecture]: media/iot-suite-predictive-walkthrough/architecture.png

[lnk-remote-monitoring]: iot-suite-remote-monitoring-sample-walkthrough.md
[lnk-cortana-analytics]: http://gallery.cortanaintelligence.com/Collection/Predictive-Maintenance-Template-3
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/