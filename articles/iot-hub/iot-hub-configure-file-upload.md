---
title: "carregamento do arquivo aaaUse Olá tooconfigure portal do Azure | Microsoft Docs"
description: "Como toouse Olá tooconfigure portal do Azure seu arquivo de tooenable de hub IoT carregamentos de dispositivos conectados. Inclui informações sobre como configurar a conta de armazenamento do Azure de destino hello."
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
ms.openlocfilehash: b90c3fbed47b4eb144d3cb7480068b7cfc776ba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a><span data-ttu-id="3210b-104">Configurar o IoT Hub carregamentos de arquivo usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3210b-104">Configure IoT Hub file uploads using hello Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="3210b-105">Upload de arquivos</span><span class="sxs-lookup"><span data-stu-id="3210b-105">File upload</span></span>

<span data-ttu-id="3210b-106">Olá toouse [funcionalidade de carregamento de arquivo no IoT Hub][lnk-upload], primeiro você deve associar uma conta de armazenamento do Azure com o hub.</span><span class="sxs-lookup"><span data-stu-id="3210b-106">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="3210b-107">Selecione **carregamento do arquivo** toodisplay uma lista de propriedades de carregamento de arquivo para o hub IoT Olá que está sendo modificado.</span><span class="sxs-lookup"><span data-stu-id="3210b-107">Select **File upload** toodisplay a list of file upload properties for hello IoT hub that is being modified.</span></span>

![As configurações no portal de saudação de carregamento de arquivo de IoT Hub de exibição][13]

<span data-ttu-id="3210b-109">**Contêiner de armazenamento**: Use Olá tooselect portal do Azure de um contêiner de blob em uma conta de armazenamento do Azure no seu atual tooassociate de assinatura do Azure com o IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3210b-109">**Storage container**: Use hello Azure portal tooselect a blob container in an Azure Storage account in your current Azure subscription tooassociate with your IoT Hub.</span></span> <span data-ttu-id="3210b-110">Se necessário, você pode criar uma conta de armazenamento do Azure no hello **contas de armazenamento** contêiner de blob e folha em Olá **contêineres** folha.</span><span class="sxs-lookup"><span data-stu-id="3210b-110">If necessary, you can create an Azure Storage account on hello **Storage accounts** blade and blob container on hello **Containers** blade.</span></span> <span data-ttu-id="3210b-111">IoT Hub gera automaticamente os URIs de SAS com contêiner de blob de toothis de permissões de gravação para dispositivos toouse ao carregar arquivos.</span><span class="sxs-lookup"><span data-stu-id="3210b-111">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

![Contêineres de armazenamento de modo de exibição para o carregamento do arquivo no portal de saudação][14]

<span data-ttu-id="3210b-113">**Receber notificações para arquivos carregados**: habilitar ou desabilitar notificações de carregamento de arquivo por meio da alternância de saudação.</span><span class="sxs-lookup"><span data-stu-id="3210b-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via hello toggle.</span></span>

<span data-ttu-id="3210b-114">**SAS TTL**: essa configuração é hello tempo de vida da saudação SAS URIs retornados toohello dispositivo pelo IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3210b-114">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="3210b-115">Definir tooone horas por padrão, mas podem ser personalizado tooother valores usando Olá controle deslizante.</span><span class="sxs-lookup"><span data-stu-id="3210b-115">Set tooone hour by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="3210b-116">**Notificação de tempo de vida padrão de configurações de arquivo**: Olá tempo de vida de uma notificação de carregamento de arquivo antes de expirar.</span><span class="sxs-lookup"><span data-stu-id="3210b-116">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="3210b-117">Definir dia tooone por padrão, mas podem ser personalizado tooother valores usando Olá controle deslizante.</span><span class="sxs-lookup"><span data-stu-id="3210b-117">Set tooone day by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="3210b-118">**Contagem máxima de entrega de notificação de arquivo**: Olá número de vezes Olá toodeliver tentativas de IoT Hub uma notificação de carregamento de arquivo.</span><span class="sxs-lookup"><span data-stu-id="3210b-118">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="3210b-119">Definir too10 por padrão, mas podem ser personalizado tooother valores usando Olá controle deslizante.</span><span class="sxs-lookup"><span data-stu-id="3210b-119">Set too10 by default but can be customized tooother values using hello slider.</span></span>

![Configurar o carregamento do arquivo de IoT Hub no portal de saudação][15]

## <a name="next-steps"></a><span data-ttu-id="3210b-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3210b-121">Next steps</span></span>

<span data-ttu-id="3210b-122">Para obter mais informações sobre os recursos de carregamento de arquivo hello IoT Hub, consulte [carregar arquivos de um dispositivo] [ lnk-upload] em Olá guia do desenvolvedor de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3210b-122">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in hello IoT Hub developer guide.</span></span>

<span data-ttu-id="3210b-123">Siga essas toolearn links mais sobre como gerenciar o Azure IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="3210b-123">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="3210b-124">[Gerenciamento em massa de dispositivos IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="3210b-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="3210b-125">[Métricas do Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="3210b-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="3210b-126">[Monitoramento de operações][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="3210b-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="3210b-127">toofurther explorar recursos de saudação do IoT Hub, consulte:</span><span class="sxs-lookup"><span data-stu-id="3210b-127">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="3210b-128">[Guia do desenvolvedor do Hub IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="3210b-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="3210b-129">[Simulando um dispositivo com IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="3210b-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="3210b-130">[Proteger a sua solução de IoT da saudação de plano de fundo para cima][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="3210b-130">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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
