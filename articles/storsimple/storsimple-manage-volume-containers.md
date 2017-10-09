---
title: "aaaManage seus contêineres de volume StorSimple | Microsoft Docs"
description: "Explica como você pode usar o hello StorSimple Manager página tooadd contêineres de volume de serviço, modificar ou excluir um contêiner de volume."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a>Use contêineres de volume Olá Gerenciador StorSimple service toomanage StorSimple
## <a name="overview"></a>Visão geral
Este tutorial explica como toouse Olá toocreate do serviço StorSimple Manager e gerenciar contêineres de volume StorSimple.

Um contêiner de volume em um dispositivo Microsoft Azure StorSimple contém um ou mais volumes que compartilham as configurações da conta de armazenamento, da criptografia e do consumo de largura de banda. Um dispositivo pode ter vários contêineres de volume para todos os seus volumes. 

Um contêiner de volume possui Olá seguintes atributos:

* **Volumes** – Olá em camadas ou localmente afixado volumes do StorSimple contidos no contêiner de volume hello. Um contêiner de volume pode conter volumes do StorSimple too256.
* **Criptografia** – uma chave de criptografia que pode ser definida para cada contêiner de volume. Essa chave é usada para criptografar dados Olá que são enviados de sua nuvem de toohello do dispositivo StorSimple. Uma chave de grau militar AES de 256 bits é usada com a chave de usuário inserido hello. toosecure seus dados, é recomendável que você sempre habilite a criptografia de armazenamento em nuvem.
* **Conta de armazenamento** – Olá conta de armazenamento que é o provedor de serviço de armazenamento de nuvem tooyour vinculado. Todos os volumes de saudação que reside em um contêiner de volume compartilham essa conta de armazenamento. Você pode escolher uma conta de armazenamento de uma lista existente ou criar uma nova conta ao criar o contêiner de volume hello e, em seguida, especifique as credenciais de acesso de saudação para essa conta.
* **Largura de banda em nuvem** – Olá largura de banda consumida pelo dispositivo hello quando dados de saudação do dispositivo hello está sendo enviados toohello nuvem. Você pode impor um controle de largura de banda, especificando um valor entre 1 e 1000 Mbps ao definir esse contêiner. Se você quiser Olá dispositivo tooconsume largura de banda disponível, defina tooUnlimited neste campo. Você também pode criar e aplicar uma largura de banda modelo tooallocate largura de banda com base em agendamento.

![Página de contêineres de volume](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

Este procedimentos a seguir explicam como toouse Olá StorSimple **contêineres de Volume** Olá toocomplete de página operações comuns a seguir:

* Adicionar um contêiner de volume 
* Modificar um contêiner de volume 
* Excluir um contêiner de volume 

## <a name="add-a-volume-container"></a>Adicionar um contêiner de volume
Execute Olá seguindo as etapas tooadd um contêiner de volume.

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a>Modificar um contêiner de volume
Execute Olá seguindo as etapas toomodify um contêiner de volume.

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>Excluir um contêiner de volume
Um contêiner de volume possui volumes dentro dele. Ele pode ser excluído somente se todos os volumes de saudação contidos nele são excluídos primeiro. Execute Olá seguindo as etapas toodelete um contêiner de volume.

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [como gerenciar volumes do StorSimple](storsimple-manage-volumes.md). 
* Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-manager-service-administration.md).

