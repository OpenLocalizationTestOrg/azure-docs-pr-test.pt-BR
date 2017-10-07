---
title: "as políticas de backup aaaManage StorSimple 8000 series | Microsoft Docs"
description: "Explica como você pode usar toocreate de serviço do Gerenciador de dispositivos de StorSimple hello e gerenciar backups manuais, agendas de backup e retenção de backup em um dispositivo da série StorSimple 8000."
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
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 7c56365abb6ba69d02008829ca6ae703d4632705
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-toomanage-backup-policies"></a>Usar serviço de Gerenciador de dispositivos de StorSimple Olá nas políticas de backup toomanage portal do Azure


## <a name="overview"></a>Visão geral

Este tutorial explica como toouse Olá serviço do Gerenciador de dispositivos de StorSimple **política de Backup** processos de backup de toocontrol de folha e retenção de backup para os volumes do StorSimple. Ele também descreve como toocomplete um backup manual.

Quando você faz backup de um volume, você pode escolher toocreate um instantâneo local ou um instantâneo na nuvem. Se você estiver fazendo backup de um volume fixado localmente, é recomendável que você especifique um instantâneo de nuvem. Gravar um grande número de instantâneos locais de um volume fixado localmente juntamente com um conjunto de dados que tem muita variação resultará em uma situação em que você pode, rapidamente, ficar sem espaço local. Se você escolher tootake instantâneos locais, é recomendável levar menos tooback instantâneos diários estado mais recente Olá mantê-los por dia e, em seguida, excluí-los.

Quando você usa um instantâneo de nuvem de um volume localmente afixado, você copiar somente Olá alterado dados toohello na nuvem, onde é eliminação de duplicação e compactado.

## <a name="hello-backup-policy-blade"></a>folha de política de Backup Olá

Olá **política de Backup** folha para seu dispositivo StorSimple permite que você toomanage as políticas de backup e agendamento locais e instantâneos em nuvem. Políticas de backup são usados tooconfigure agendas de backup e retenção de backup para um conjunto de volumes. Políticas de backup permitem que você tootake um instantâneo de vários volumes simultaneamente. Isso significa que os backups de saudação criados por uma política de backup será cópias consistente.

listagem tabular de políticas de backup Olá também permite que você toofilter Olá políticas de backup existentes por uma ou mais Olá campos a seguir:

* **Nome da política** – hello nome associado à política de saudação. Olá os tipos diferentes de políticas incluem:

  * Políticas agendadas, que são criadas explicitamente pelo usuário hello.
  * Políticas importadas, que foram criadas no hello StorSimple Snapshot Manager. Elas têm uma marca que descreve o host StorSimple Snapshot Manager Olá Olá políticas foram importadas do.

  > [!NOTE]
  > Políticas de backup automático ou padrão não estão mais habilitadas no momento de saudação da criação de volume.

* **Último backup bem-sucedido** – Olá data e hora do hello último backup bem-sucedido que foi feito com esta política.

* **Próximo backup** – Olá data e hora do hello próximo backup agendado que será iniciado por essa política.

* **Volumes** – Olá volumes associados à política de saudação. Todos os volumes de saudação associados a uma política de backup são agrupados durante os backups são criados.

* **Agendas** – Olá número de agendamentos associados à política de backup hello.

operações de Olá usado com frequência que você pode executar para políticas de backup são:

* Adicionar uma política de backup
* Adicionar ou modificar um agendamento
* Adicionar ou remover um volume
* Excluir uma política de backup
* Fazer um backup manual

## <a name="add-a-backup-policy"></a>Adicionar uma política de backup

Adicione uma agenda de tooautomatically de política de backup de seus backups. Quando você cria um volume pela primeira vez, nenhuma política de backup padrão é associada a ele. Você precisa tooadd e atribuir um política de backup tooprotect volume de dados.

Execute Olá etapas Olá tooadd portal do Azure uma política de backup para seu dispositivo StorSimple. Depois de adicionar política hello, você pode definir uma agenda (consulte [adicionar ou modificar uma agenda](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-8000-add-backup-policy-u2](../../includes/storsimple-8000-add-backup-policy-u2.md)]

## <a name="add-or-modify-a-schedule"></a>Adicionar ou modificar um agendamento

Você pode adicionar ou modificar uma agenda que é anexado tooan política de backup existente em seu dispositivo StorSimple. Execute Olá etapas Olá tooadd portal do Azure ou modificar uma agenda.

[!INCLUDE [storsimple-8000-add-modify-backup-schedule](../../includes/storsimple-8000-add-modify-backup-schedule-u2.md)]


## <a name="add-or-remove-a-volume"></a>Adicionar ou remover um volume

Você pode adicionar ou remover um volume atribuído tooa política de backup no dispositivo StorSimple. Executar Olá etapas Olá tooadd portal do Azure ou remover um volume.

[!INCLUDE [storsimple-8000-add-volume-backup-policy-u2](../../includes/storsimple-8000-add-remove-volume-backup-policy-u2.md)]


## <a name="delete-a-backup-policy"></a>Excluir uma política de backup

Execute Olá seguindo as etapas em Olá toodelete portal do Azure uma política de backup no dispositivo StorSimple.

[!INCLUDE [storsimple-8000-delete-backup-policy](../../includes/storsimple-8000-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>Fazer um backup manual

Execute Olá seguindo as etapas no hello toocreate portal do Azure uma demanda (manual) backup para um único volume.

[!INCLUDE [storsimple-8000-create-manual-backup](../../includes/storsimple-8000-create-manual-backup.md)]

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador de dispositivos do StorSimple em seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

