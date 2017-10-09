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
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a>Configurar o IoT Hub carregamentos de arquivo usando Olá portal do Azure

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a>Upload de arquivos

Olá toouse [funcionalidade de carregamento de arquivo no IoT Hub][lnk-upload], primeiro você deve associar uma conta de armazenamento do Azure com o hub. Selecione **carregamento do arquivo** toodisplay uma lista de propriedades de carregamento de arquivo para o hub IoT Olá que está sendo modificado.

![As configurações no portal de saudação de carregamento de arquivo de IoT Hub de exibição][13]

**Contêiner de armazenamento**: Use Olá tooselect portal do Azure de um contêiner de blob em uma conta de armazenamento do Azure no seu atual tooassociate de assinatura do Azure com o IoT Hub. Se necessário, você pode criar uma conta de armazenamento do Azure no hello **contas de armazenamento** contêiner de blob e folha em Olá **contêineres** folha. IoT Hub gera automaticamente os URIs de SAS com contêiner de blob de toothis de permissões de gravação para dispositivos toouse ao carregar arquivos.

![Contêineres de armazenamento de modo de exibição para o carregamento do arquivo no portal de saudação][14]

**Receber notificações para arquivos carregados**: habilitar ou desabilitar notificações de carregamento de arquivo por meio da alternância de saudação.

**SAS TTL**: essa configuração é hello tempo de vida da saudação SAS URIs retornados toohello dispositivo pelo IoT Hub. Definir tooone horas por padrão, mas podem ser personalizado tooother valores usando Olá controle deslizante.

**Notificação de tempo de vida padrão de configurações de arquivo**: Olá tempo de vida de uma notificação de carregamento de arquivo antes de expirar. Definir dia tooone por padrão, mas podem ser personalizado tooother valores usando Olá controle deslizante.

**Contagem máxima de entrega de notificação de arquivo**: Olá número de vezes Olá toodeliver tentativas de IoT Hub uma notificação de carregamento de arquivo. Definir too10 por padrão, mas podem ser personalizado tooother valores usando Olá controle deslizante.

![Configurar o carregamento do arquivo de IoT Hub no portal de saudação][15]

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre os recursos de carregamento de arquivo hello IoT Hub, consulte [carregar arquivos de um dispositivo] [ lnk-upload] em Olá guia do desenvolvedor de IoT Hub.

Siga essas toolearn links mais sobre como gerenciar o Azure IoT Hub:

* [Gerenciamento em massa de dispositivos IoT][lnk-bulk]
* [Métricas do Hub IoT][lnk-metrics]
* [Monitoramento de operações][lnk-monitor]

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Guia do desenvolvedor do Hub IoT][lnk-devguide]
* [Simulando um dispositivo com IoT Edge][lnk-iotedge]
* [Proteger a sua solução de IoT da saudação de plano de fundo para cima][lnk-securing]

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
