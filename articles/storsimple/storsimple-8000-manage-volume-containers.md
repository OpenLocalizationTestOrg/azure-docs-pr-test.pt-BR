---
title: "aaaManage seus contêineres de volume StorSimple no dispositivo da série StorSimple 8000 do hello | Microsoft Docs"
description: "Explica como você pode usar o hello Gerenciador de dispositivos do StorSimple contêineres de volume do serviço página tooadd, modificar ou excluir um contêiner de volume."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a>Use contêineres de volume Olá Gerenciador de dispositivos do StorSimple service toomanage StorSimple

## <a name="overview"></a>Visão geral
Este tutorial explica como toouse Olá toocreate de serviço do Gerenciador de dispositivos do StorSimple e gerenciar contêineres de volume StorSimple.

Um contêiner de volume em um dispositivo Microsoft Azure StorSimple contém um ou mais volumes que compartilham as configurações da conta de armazenamento, da criptografia e do consumo de largura de banda. Um dispositivo pode ter vários contêineres de volume para todos os seus volumes. 

Um contêiner de volume possui Olá seguintes atributos:

* **Volumes** – Olá em camadas ou localmente afixado volumes do StorSimple contidos no contêiner de volume hello. 
* **Criptografia** – uma chave de criptografia que pode ser definida para cada contêiner de volume. Essa chave é usada para criptografar dados Olá que são enviados de sua nuvem de toohello do dispositivo StorSimple. Uma chave de grau militar AES de 256 bits é usada com a chave de usuário inserido hello. toosecure seus dados, é recomendável que você sempre habilite a criptografia de armazenamento em nuvem.
* **Conta de armazenamento** – Olá conta de armazenamento do Azure que é usado toostore Olá dados. Todos os volumes de saudação que reside em um contêiner de volume compartilham essa conta de armazenamento. Você pode escolher uma conta de armazenamento de uma lista existente ou criar uma nova conta ao criar o contêiner de volume hello e, em seguida, especifique as credenciais de acesso de saudação para essa conta.
* **Largura de banda em nuvem** – Olá largura de banda consumida pelo dispositivo hello quando dados de saudação do dispositivo hello está sendo enviados toohello nuvem. Imponha um controle de largura de banda especificando um valor entre 1 e 1.000 Mbps ao criar esse contêiner. Se você quiser Olá dispositivo tooconsume largura de banda disponível, defina este campo muito**Unlimited**. Você também pode criar e aplicar uma largura de banda modelo tooallocate largura de banda com base em agendamento.

Olá procedimentos a seguir explicam como toouse Olá StorSimple **contêineres de Volume** Olá toocomplete de folha operações comuns a seguir:

* Adicionar um contêiner de volume
* Modificar um contêiner de volume
* Excluir um contêiner de volume

## <a name="add-a-volume-container"></a>Adicionar um contêiner de volume
Execute Olá seguindo as etapas tooadd um contêiner de volume.

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a>Modificar um contêiner de volume
Execute Olá seguindo as etapas toomodify um contêiner de volume.

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>Excluir um contêiner de volume
Um contêiner de volume possui volumes dentro dele. Ele pode ser excluído somente se todos os volumes de saudação contidos nele são excluídos primeiro. Execute Olá seguindo as etapas toodelete um contêiner de volume.

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [como gerenciar volumes do StorSimple](storsimple-8000-manage-volumes-u2.md). 
* Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador de dispositivos do StorSimple em seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

