---
title: "aaaView e gerenciar trabalhos para StorSimple série 8000 | Microsoft Docs"
description: "Descreve a folha de trabalhos de serviço de Gerenciador de dispositivos de StorSimple hello e como toouse ela trabalhos de backup agendados, atual e recentes tootrack."
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: a76acd67e2568478dd43d0fb16c1ae2dfb72a23d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-and-manage-jobs-update-3-and-later"></a>Usar tooview de serviço do Gerenciador de dispositivos de StorSimple hello e gerenciar trabalhos (atualização 3 e posterior)

## <a name="overview"></a>Visão geral
Olá **trabalhos** folha fornece um único portal central para exibir e gerenciar trabalhos iniciados em dispositivos conectados tooyour serviço de Gerenciador de dispositivos do StorSimple. É possível exibir os trabalhos agendados, em execução, concluídos, cancelados e com falha para vários dispositivos. Os resultados são apresentados em um formato tabular.

![Folha de trabalhos](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

Você pode localizar rapidamente os trabalhos de saudação que está interessado ao filtrar campos, como:

* **Status** – Os trabalhos podem estar em andamento, ser bem-sucedidos, cancelados ou concluídos com falha.
* **Intervalo de tempo** – trabalhos podem ser o intervalo de filtrado Olá com base na data e hora. os intervalos de saudação são após 1 hora, nas últimas 24 horas, últimos 7 dias, últimos 30 dias, o último ano ou data personalizada.
* **Tipo** – tipo de trabalho Olá pode ser backup agendado, o backup manual, o backup da restauração, clonar volume failover contêineres de volume, crie volume localmente afixado, modificar o volume, instalar atualizações, coletar logs de suporte e solução de nuvem.
* **Dispositivos** – os trabalhos são iniciados em um determinado serviço de tooyour dispositivo conectado.
  
Olá trabalhos filtrados são então tabulados com base Olá Olá seguintes atributos:
  
* **Nome** – Backup agendado, backup manual, backup de restauração, clonar volume, fazer failover de contêineres de volume, criar volume fixado localmente, modificar volume, instalar atualizações, coletar logs de suporte ou criar dispositivo de nuvem.
* **Status** – em execução, concluídos, cancelados, com falha, em cancelamento ou concluídos com erros.
* **Entidade** – trabalhos Olá podem ser associados um volume, uma política de backup ou um dispositivo. Por exemplo, um trabalho de clone é associado a um volume, enquanto um trabalho de backup agendado é associado a uma política de backup. Um trabalho de dispositivo é criado como resultado de uma recuperação de desastres (DR) ou uma operação de restauração.
* **Dispositivo** – hello nome de dispositivo de saudação na qual Olá o trabalho foi iniciado.
* **Iniciado em** – tempo de saudação quando o trabalho de saudação foi iniciado.
* **Duração** – trabalho de Olá Olá tempo toocomplete necessária.

lista de saudação de trabalhos é atualizada a cada 30 segundos.

Você pode executar Olá relacionada ao trabalho ações a seguir nesta página:

* Exibir detalhes do trabalho
* Cancelar um trabalho

## <a name="view-job-details"></a>Exibir detalhes do trabalho
Execute Olá etapas tooview Olá detalhes de qualquer trabalho a seguir.

#### <a name="tooview-job-details"></a>detalhes do trabalho tooview
1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e, em seguida, clique em **trabalhos**.

2. Em Olá **trabalhos** folha, exibição hello (s) que está interessado executando uma consulta com os filtros apropriados. É possível pesquisar trabalhos concluídos, em execução ou cancelados.

    ![Folha de trabalho](./media/storsimple-8000-manage-jobs-u2/jobs1.png)

2. Selecione e clique em um trabalho.

    ![Folha de trabalho](./media/storsimple-8000-manage-jobs-u2/jobs3.png)

3. Na folha de detalhes do trabalho hello, você pode exibir o status de hello, detalhes, estatísticas de tempo e as estatísticas de dados.
   
    ![Detalhes do trabalho](./media/storsimple-8000-manage-jobs-u2/jobs4.png)

## <a name="cancel-a-job"></a>Cancelar um trabalho
Execute Olá seguindo as etapas toocancel um trabalho em execução.

> [!NOTE]
> Alguns trabalhos, como modificar um tipo de volume do volume toochange hello ou expandir um volume não podem ser cancelados.


### <a name="toocancel-a-job"></a>toocancel um trabalho
1. Em Olá **trabalhos** página, exibir hello em execução (s) que você deseja toocancel executando uma consulta com os filtros apropriados. Selecione o trabalho de saudação.

2. Clique no menu de contexto de saudação do hello trabalho selecionado tooinvoke **Cancelar**.

    ![Detalhes do trabalho](./media/storsimple-8000-manage-jobs-u2/jobs2.png)

3. Quando solicitado a confirmar, clique em **Sim**. Este trabalho agora está cancelado.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[gerenciar suas políticas de backup StorSimple](storsimple-8000-manage-backup-policies-u2.md).
* Saiba como muito[use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

