---
title: "aaaManage suas políticas de backup StorSimple | Microsoft Docs"
description: "Explica como você pode usar toocreate de serviço do StorSimple Manager hello e gerenciar backups manuais, agendas de backup e retenção de backup."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 4a2db707-bbfc-425c-bfeb-bc5c97781873
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2016
ms.author: v-sharos
ms.openlocfilehash: 7b01f29a8d8a096d9890c8406557021317b9baff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-backup-policies-update-2"></a>Usar políticas de backup toomanage (atualização 2) de serviço de Gerenciador de StorSimple Olá
[!INCLUDE [storsimple-version-selector-manage-backup-policies](../../includes/storsimple-version-selector-manage-backup-policies.md)]

## <a name="overview"></a>Visão geral
Este tutorial explica como toouse Olá serviço StorSimple Manager **políticas de Backup** página toocontrol processos de backup e retenção de backup para os volumes do StorSimple. Ele também descreve como toocomplete um backup manual.

Quando você faz backup de um volume, você pode escolher toocreate um instantâneo local ou um instantâneo na nuvem. Se você estiver fazendo backup de um volume fixado localmente, é recomendável que você especifique um instantâneo de nuvem. Gravar um grande número de instantâneos locais de um volume fixado localmente juntamente com um conjunto de dados que tem muita variação resultará em uma situação em que você pode, rapidamente, ficar sem espaço local. Se você escolher tootake instantâneos locais, é recomendável levar menos tooback instantâneos diários estado mais recente Olá mantê-los por dia e, em seguida, excluí-los.

Quando você usa um instantâneo de nuvem de um volume localmente afixado, você copiar somente Olá alterado dados toohello na nuvem, onde é eliminação de duplicação e compactado. 

## <a name="hello-backup-policies-page"></a>página de políticas de Backup Olá
Olá **políticas de Backup** página permite que você toomanage as políticas de backup e agendamento locais e instantâneos em nuvem. (As políticas de backup são usados tooconfigure agendas de backup e retenção de backup para um conjunto de volumes). Políticas de backup permitem que você tootake um instantâneo de vários volumes simultaneamente. Isso significa que os backups de saudação criados por uma política de backup será cópias consistente. Olá **políticas de Backup** página lista as políticas de backup hello, seus tipos, volumes Olá associado, número de Olá de backups retidos e Olá opção tooenable essas políticas.

Olá **políticas de Backup** página também permite que você toofilter Olá políticas de backup existentes por uma ou mais Olá campos a seguir:

* **Nome da política** – hello nome associado à política de saudação. Olá os tipos diferentes de políticas incluem:
  
  * Políticas agendadas, que são criadas explicitamente pelo usuário hello.
  * Políticas automáticas, que são criadas quando o backup do saudação padrão para essa opção de volume foi habilitado no momento de saudação da criação de volume. Essas políticas são denominadas *VolumeName*default onde *VolumeName* refere-se o nome de toohello de saudação volume StorSimple configurado pelo usuário Olá Olá portal clássico do Azure. políticas automáticas Olá resultam em instantâneos de nuvem diários, começando na hora do dispositivo 22:30.
  * Políticas importadas, que foram criadas no hello StorSimple Snapshot Manager. Elas têm uma marca que descreve o host StorSimple Snapshot Manager Olá Olá políticas foram importadas do.
* **Volumes** – Olá volumes associados à política de saudação. Todos os volumes de saudação associados a uma política de backup são agrupados durante os backups são criados.
* **Último backup bem-sucedido** – Olá data e hora do hello último backup bem-sucedido que foi feito com esta política.
* **Próximo backup** – Olá data e hora do hello próximo backup agendado que será iniciado por essa política.
* **Agendas** – Olá número de agendamentos associados à política de backup hello.

operações de saudação usada com frequência que você pode executar nessa página são:

* Adicionar uma política de backup 
* Adicionar ou modificar um agendamento 
* Excluir uma política de backup 
* Fazer um backup manual 
* Criar uma política de backup personalizada com vários volumes e agendamentos 

## <a name="add-a-backup-policy"></a>Adicionar uma política de backup
Adicione uma agenda de tooautomatically de política de backup de seus backups. Execute Olá etapas Olá tooadd portal clássico do Azure uma política de backup para seu dispositivo StorSimple. Depois de adicionar política hello, você pode definir uma agenda (consulte [adicionar ou modificar uma agenda](#add-or-modify-a-schedule)).

[!INCLUDE [storsimple-add-backup-policy-u2](../../includes/storsimple-add-backup-policy-u2.md)]

![Vídeo disponível](./media/storsimple-manage-backup-policies-u2/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como toocreate local ou na nuvem de política de backup, clique em [aqui](https://azure.microsoft.com/documentation/videos/create-storsimple-backup-policies/).

## <a name="add-or-modify-a-schedule"></a>Adicionar ou modificar um agendamento
Você pode adicionar ou modificar uma agenda que é anexado tooan política de backup existente em seu dispositivo StorSimple. Execute Olá etapas Olá tooadd de portal clássico do Azure ou modificar uma agenda.

[!INCLUDE [storsimple-add-modify-backup-schedule](../../includes/storsimple-add-modify-backup-schedule-u2.md)]

## <a name="delete-a-backup-policy"></a>Excluir uma política de backup
Execute Olá seguindo as etapas em Olá toodelete portal clássico do Azure uma política de backup no dispositivo StorSimple.

[!INCLUDE [storsimple-delete-backup-policy](../../includes/storsimple-delete-backup-policy.md)]

## <a name="take-a-manual-backup"></a>Fazer um backup manual
Execute Olá seguindo as etapas no hello toocreate portal clássico do Azure uma demanda (manual) backup para um único volume.

[!INCLUDE [storsimple-create-manual-backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="create-a-custom-backup-policy-with-multiple-volumes-and-schedules"></a>Criar uma política de backup personalizada com vários volumes e agendamentos
Execute Olá etapas Olá toocreate portal clássico do Azure uma política de backup personalizada que tem vários volumes e agendas.

[!INCLUDE [storsimple-create-custom-backup-policy](../../includes/storsimple-create-custom-backup-policy-u2.md)]

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-manager-service-administration.md).

