---
title: Usar o portal do Azure para configurar o carregamento do arquivo | Microsoft Docs
description: "Como usar o Portal do Azure para configurar o Hub IoT a fim de habilitar transferências de arquivos de dispositivos conectados. Inclui informações sobre como configurar a conta de armazenamento do Azure de destino."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: 149dd84d7d8f4ff9cd30f9fc649ced3cb364cfb7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-iot-hub-file-uploads-using-the-azure-portal"></a><span data-ttu-id="85fd2-104">Configurar uploads de arquivo do Hub IoT usando o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="85fd2-104">Configure IoT Hub file uploads using the Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="85fd2-105">Upload de arquivos</span><span class="sxs-lookup"><span data-stu-id="85fd2-105">File upload</span></span>

<span data-ttu-id="85fd2-106">Para usar a [funcionalidade de upload de arquivo no Hub IoT][lnk-upload], primeiro você deve associar uma conta de Armazenamento do Azure ao hub.</span><span class="sxs-lookup"><span data-stu-id="85fd2-106">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="85fd2-107">Selecione **Upload de arquivo** para exibir uma lista de propriedades de upload de arquivo para o hub IoT que está sendo modificado.</span><span class="sxs-lookup"><span data-stu-id="85fd2-107">Select **File upload** to display a list of file upload properties for the IoT hub that is being modified.</span></span>

![Exibir configurações de upload de arquivo do Hub IoT no portal][13]

<span data-ttu-id="85fd2-109">**Contêiner de armazenamento**: use o Portal do Azure para selecionar um contêiner de blobs em uma conta de Armazenamento do Azure na assinatura atual do Azure para associar ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="85fd2-109">**Storage container**: Use the Azure portal to select a blob container in an Azure Storage account in your current Azure subscription to associate with your IoT Hub.</span></span> <span data-ttu-id="85fd2-110">Se for necessário, você pode criar uma conta de Armazenamento do Azure na folha **Contas de armazenamento** e um contêiner de blob na folha **Contêineres**.</span><span class="sxs-lookup"><span data-stu-id="85fd2-110">If necessary, you can create an Azure Storage account on the **Storage accounts** blade and blob container on the **Containers** blade.</span></span> <span data-ttu-id="85fd2-111">O Hub IoT gera automaticamente os URIs de SAS com permissões de gravação para esse contêiner de blob para dispositivos a serem usados ao carregar arquivos.</span><span class="sxs-lookup"><span data-stu-id="85fd2-111">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

![Exibir contêineres de armazenamento para upload de arquivos no portal][14]

<span data-ttu-id="85fd2-113">**Receber notificações para os arquivos carregados**: habilitar ou desabilitar notificações de upload de arquivo por meio de um botão de opção.</span><span class="sxs-lookup"><span data-stu-id="85fd2-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via the toggle.</span></span>

<span data-ttu-id="85fd2-114">**TTL de SAS**: essa configuração é a vida útil dos URIs de SAS retornados para o dispositivo pelo Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="85fd2-114">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="85fd2-115">Definido para uma hora por padrão, mas pode ser personalizado para outros valores usando o controle deslizante.</span><span class="sxs-lookup"><span data-stu-id="85fd2-115">Set to one hour by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="85fd2-116">**TTL de configurações de notificação de arquivo padrão**: a vida útil de uma notificação de upload de arquivo antes de sua expiração.</span><span class="sxs-lookup"><span data-stu-id="85fd2-116">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="85fd2-117">Definido para um dia por padrão, mas pode ser personalizado para outros valores usando o controle deslizante.</span><span class="sxs-lookup"><span data-stu-id="85fd2-117">Set to one day by default but can be customized to other values using the slider.</span></span>

<span data-ttu-id="85fd2-118">**Contagem de entrega máxima de notificação de arquivo**: o número de vezes que o Hub IoT tenta entregar uma notificação de carregamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="85fd2-118">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="85fd2-119">Definido como 10 por padrão, mas pode ser personalizado para outros valores usando o controle deslizante.</span><span class="sxs-lookup"><span data-stu-id="85fd2-119">Set to 10 by default but can be customized to other values using the slider.</span></span>

![Configurar o upload de arquivos do Hub IoT no portal][15]

## <a name="next-steps"></a><span data-ttu-id="85fd2-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="85fd2-121">Next steps</span></span>

<span data-ttu-id="85fd2-122">Para saber mais sobre os recursos de upload de arquivo do Hub IoT, consulte [Carregar arquivos de um dispositivo][lnk-upload] no guia do desenvolvedor do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="85fd2-122">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in the IoT Hub developer guide.</span></span>

<span data-ttu-id="85fd2-123">Para saber mais sobre o gerenciamento do Hub IoT do Azure, siga estes links:</span><span class="sxs-lookup"><span data-stu-id="85fd2-123">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="85fd2-124">[Gerenciamento em massa de dispositivos IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="85fd2-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="85fd2-125">[Métricas do Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="85fd2-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="85fd2-126">[Monitoramento de operações][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="85fd2-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="85fd2-127">Para explorar melhor as funcionalidades do Hub IoT, consulte:</span><span class="sxs-lookup"><span data-stu-id="85fd2-127">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="85fd2-128">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="85fd2-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="85fd2-129">[Simulando um dispositivo com IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="85fd2-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="85fd2-130">[Proteger sua solução de IoT desde o início][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="85fd2-130">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
