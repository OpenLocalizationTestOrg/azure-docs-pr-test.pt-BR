---
title: "Instruções para o Hub IoT do Azure | Microsoft Docs"
description: "Como desenvolvedor, como usar os vários recursos do Hub IoT?"
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 786121ae249d69376b4be4c74000868cbb208989
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-iot-hub"></a><span data-ttu-id="f0b8d-103">Como usar o Hub IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="f0b8d-103">How to use Azure IoT Hub</span></span>

<span data-ttu-id="f0b8d-104">Você tem várias opções para aprender a desenvolver para o serviço do Hub IoT:</span><span class="sxs-lookup"><span data-stu-id="f0b8d-104">You have various options to learn how to develop for the IoT Hub service:</span></span>

* <span data-ttu-id="f0b8d-105">Leia os artigos conceituais que descrevem os recursos do Hub IoT em detalhes.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-105">Read the conceptual articles that describe the features of IoT Hub in detail.</span></span>
* <span data-ttu-id="f0b8d-106">Siga um dos tutoriais que abordam os vários recursos do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-106">Follow one of the tutorials that cover the various features of IoT Hub.</span></span>

## <a name="developer-guide"></a><span data-ttu-id="f0b8d-107">Guia do desenvolvedor</span><span class="sxs-lookup"><span data-stu-id="f0b8d-107">Developer guide</span></span>

<span data-ttu-id="f0b8d-108">Como desenvolvedor, você pode ler diretrizes conceituais detalhadas sobre o Hub IoT no [Guia do Desenvolvedor][lnk-devguide].</span><span class="sxs-lookup"><span data-stu-id="f0b8d-108">As a developer, you can read detailed conceptual guidance about IoT Hub in the [Developer Guide][lnk-devguide].</span></span> <span data-ttu-id="f0b8d-109">Este guia inclui os seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="f0b8d-109">This guide includes:</span></span>

* <span data-ttu-id="f0b8d-110">Descrições detalhadas de todos os recursos de Hub IoT que ajudam você a aprender a usá-los.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-110">Detailed descriptions of all IoT Hub features that help you to learn how to use them.</span></span>
* <span data-ttu-id="f0b8d-111">Orientação sobre como escolher caso várias opções estejam disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-111">Guidance on how to choose when multiple options are available.</span></span>

## <a name="tutorials"></a><span data-ttu-id="f0b8d-112">Tutoriais</span><span class="sxs-lookup"><span data-stu-id="f0b8d-112">Tutorials</span></span>

<span data-ttu-id="f0b8d-113">Se você prefere aprender sobre recursos específicos do Hub IoT trabalhando em exercícios práticos, há vários tutoriais para escolher.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-113">If you prefer to learn about specific IoT Hub features by working through hands-on exercises, there are several tutorials to choose from.</span></span> <span data-ttu-id="f0b8d-114">Muitos desses tutoriais estão disponíveis em várias linguagens de programação.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-114">Many of these tutorials are available in multiple programming languages.</span></span> <span data-ttu-id="f0b8d-115">Os tutoriais incluem:</span><span class="sxs-lookup"><span data-stu-id="f0b8d-115">These tutorials include:</span></span>

- <span data-ttu-id="f0b8d-116">[Processar mensagens do dispositivo para nuvem do Hub IoT usando rotas][lnk-routes-tutorial].</span><span class="sxs-lookup"><span data-stu-id="f0b8d-116">[Process IoT Hub device-to-cloud messages using routes][lnk-routes-tutorial].</span></span> <span data-ttu-id="f0b8d-117">Este tutorial mostra como usar regras de roteamento do Hub IoT para enviar mensagens de dispositivo à nuvem de maneira fácil, com base em configuração.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-117">This tutorial shows you how to use IoT Hub routing rules to dispatch device-to-cloud messages in an easy, configuration-based way.</span></span>

- <span data-ttu-id="f0b8d-118">[Enviar mensagens da nuvem para o dispositivo com o Hub IoT][lnk-c2d-tutorial].</span><span class="sxs-lookup"><span data-stu-id="f0b8d-118">[Send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial].</span></span> <span data-ttu-id="f0b8d-119">Este tutorial mostra como enviar mensagens de nuvem ao dispositivo por meio do Hub IoT e receber mensagens da nuvem para um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-119">This tutorial shows you how to send cloud-to-device messages through IoT Hub and receive cloud-to-device messages on a device.</span></span>

- <span data-ttu-id="f0b8d-120">[Carregar arquivos de dispositivos para a nuvem com o Hub IoT][lnk-upload-tutorial].</span><span class="sxs-lookup"><span data-stu-id="f0b8d-120">[Upload files from devices to the cloud with IoT Hub][lnk-upload-tutorial].</span></span> <span data-ttu-id="f0b8d-121">Este tutorial mostra como usar os recursos de carregamento de arquivo do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-121">This tutorial shows you how to use the file upload capabilities of IoT Hub.</span></span>

- <span data-ttu-id="f0b8d-122">[Introdução a dispositivos gêmeos][lnk-twin-tutorial].</span><span class="sxs-lookup"><span data-stu-id="f0b8d-122">[Get started with device twins][lnk-twin-tutorial].</span></span> <span data-ttu-id="f0b8d-123">Este tutorial apresenta gêmeos de dispositivos, propriedades relatadas, propriedades desejadas e marcas.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-123">This tutorial introduces you to device twins, reported properties, desired properties, and tags.</span></span> <span data-ttu-id="f0b8d-124">Você usa gêmeos de dispositivo para sincronizar valores com os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-124">You use device twins to synchronize values with your devices.</span></span>

- <span data-ttu-id="f0b8d-125">[Usar métodos diretos][lnk-methods-tutorial].</span><span class="sxs-lookup"><span data-stu-id="f0b8d-125">[Use direct methods][lnk-methods-tutorial].</span></span> <span data-ttu-id="f0b8d-126">Este tutorial mostra como usar métodos diretos.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-126">This tutorial shows you how to use direct methods.</span></span> <span data-ttu-id="f0b8d-127">Você adiciona um manipulador a um método direto no dispositivo simulado e invoca o método direto do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-127">You add a handler for a direct method in your simulated device and invoke the direct method from IoT Hub.</span></span>

- <span data-ttu-id="f0b8d-128">[Introdução ao gerenciamento de dispositivos][lnk-dm-tutorial].</span><span class="sxs-lookup"><span data-stu-id="f0b8d-128">[Get started with device management][lnk-dm-tutorial].</span></span> <span data-ttu-id="f0b8d-129">Este tutorial mostra como usar recursos-chave de gerenciamento de dispositivos, como gêmeos e métodos diretos.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-129">This tutorial shows you how to use key device management features such as twins and direct methods.</span></span> <span data-ttu-id="f0b8d-130">Você pode usar esses recursos para reinicializar remotamente seu dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-130">You use these features to remotely reboot your simulated device.</span></span>

- <span data-ttu-id="f0b8d-131">[Usar as propriedades desejadas para configurar os dispositivos][lnk-properties-tutorial].</span><span class="sxs-lookup"><span data-stu-id="f0b8d-131">[Use desired properties to configure devices][lnk-properties-tutorial].</span></span> <span data-ttu-id="f0b8d-132">Este tutorial mostra como usar as propriedades desejadas e relatadas do dispositivo gêmeo para configurar o dispositivo remotamente.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-132">This tutorial shows you how to use the device twin's desired and reported properties, to remotely configure your device.</span></span>

- <span data-ttu-id="f0b8d-133">[Usar trabalhos de dispositivo para iniciar uma atualização de firmware do dispositivo][lnk-jobs-tutorial].</span><span class="sxs-lookup"><span data-stu-id="f0b8d-133">[Use device jobs to initiate a device firmware update][lnk-jobs-tutorial].</span></span> <span data-ttu-id="f0b8d-134">Este tutorial mostra como usar recursos-chave de gerenciamento de dispositivos, como gêmeos e métodos diretos.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-134">This tutorial shows you how to use key device management features such as twins and direct methods.</span></span> <span data-ttu-id="f0b8d-135">Você aprenderá a usar esses recursos para atualizar o firmware do dispositivo remotamente.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-135">You learn how to use these features to remotely update your device's firmware.</span></span>

- <span data-ttu-id="f0b8d-136">[Agendar e transmitir trabalhos][lnk-schedule-tutorial].</span><span class="sxs-lookup"><span data-stu-id="f0b8d-136">[Schedule and broadcast jobs][lnk-schedule-tutorial].</span></span> <span data-ttu-id="f0b8d-137">Este tutorial mostra como usar propriedades desejadas e métodos diretos para interagir com vários dispositivos em um horário agendado.</span><span class="sxs-lookup"><span data-stu-id="f0b8d-137">This tutorial shows you how to use desired properties and direct methods to interact with multiple devices at a scheduled time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0b8d-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f0b8d-138">Next steps</span></span>

<span data-ttu-id="f0b8d-139">Para saber mais sobre o serviço do Hub IoT, confira o [Guia do Desenvolvedor][lnk-devguide].</span><span class="sxs-lookup"><span data-stu-id="f0b8d-139">To learn more about the IoT Hub service, see the [Developer Guide][lnk-devguide].</span></span>

[lnk-devguide]: ./iot-hub-devguide.md
[lnk-routes-tutorial]: ./iot-hub-csharp-csharp-process-d2c.md
[lnk-c2d-tutorial]: ./iot-hub-csharp-csharp-c2d.md
[lnk-upload-tutorial]: ./iot-hub-csharp-csharp-file-upload.md
[lnk-twin-tutorial]: ./iot-hub-node-node-twin-getstarted.md
[lnk-methods-tutorial]: ./iot-hub-node-node-direct-methods.md
[lnk-dm-tutorial]: ./iot-hub-node-node-device-management-get-started.md
[lnk-properties-tutorial]: ./iot-hub-node-node-twin-how-to-configure.md
[lnk-jobs-tutorial]: ./iot-hub-node-node-firmware-update.md
[lnk-schedule-tutorial]: ./iot-hub-node-node-schedule-jobs.md