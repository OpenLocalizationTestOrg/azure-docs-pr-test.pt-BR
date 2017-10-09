---
title: aaaView e gerenciar trabalhos de StorSimple | Microsoft Docs
description: "Descreve a página de trabalhos de serviço Olá StorSimple Manager e como toouse ela trabalhos de backup agendados, atual e recentes tootrack."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: cdd3e9e8-7ccd-40a3-8c07-0ab1338c0e59
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d6ecdcbc3d8a4757c2328303f268e51c8ce26b65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-jobs-update-2"></a>Usar tooview de serviço do StorSimple Manager hello e gerenciar trabalhos do StorSimple (atualização 2)
[!INCLUDE [storsimple-version-selector-manage-jobs](../../includes/storsimple-version-selector-manage-jobs.md)]

## <a name="overview"></a>Visão geral
Olá **trabalhos** página fornece um único portal central para exibir e gerenciar trabalhos iniciados em dispositivos conectados tooyour o serviço StorSimple Manager. É possível exibir os trabalhos agendados, em execução, concluídos, cancelados e com falha para vários dispositivos. Os resultados são apresentados em um formato tabular. 

![Página Trabalhos](./media/storsimple-manage-jobs-u2/jobs.png)

Você pode localizar rapidamente os trabalhos de saudação que está interessado ao filtrar campos, como:

* **Status** – os trabalhos podem estar em execução, concluídos, cancelados, com falha, em cancelamento ou concluídos com erros.
* **De e para** – trabalhos podem ser o intervalo de filtrado Olá com base na data e hora.
* **Tipo** – tipo de trabalho Olá pode ser backup, backup manual, restauração, clonagem, failover de dispositivo, criar volume afixado localmente, modificar o volume, atualizar, suporte de pacote ou provisionamento do dispositivo virtual.
* **Dispositivos** – os trabalhos são iniciados em um determinado serviço de tooyour dispositivo conectado.
  Olá trabalhos filtrados são então tabulados com base Olá Olá seguintes atributos:
  
  * **Tipo** – backup, backup manual, restauração, clonagem, failover de dispositivo, criação de volume fixado localmente, modificação de volume, atualização, pacote de suporte ou provisionamento do dispositivo virtual.
  * **Status** – em execução, concluídos, cancelados, com falha, em cancelamento ou concluídos com erros.
  * **Entidade** – trabalhos Olá podem ser associados um volume, uma política de backup ou um dispositivo. Por exemplo, um trabalho de clone é associado a um volume, enquanto um trabalho de backup agendado é associado a uma política de backup. Um trabalho de dispositivo é criado como resultado de uma recuperação de desastres (DR) ou uma operação de restauração.
  * **Dispositivo** – hello nome de dispositivo de saudação na qual Olá o trabalho foi iniciado.
  * **Iniciado em** – tempo de saudação quando o trabalho de saudação foi iniciado.
  * **Andamento** – Olá percentual de conclusão de um trabalho em execução. Para um trabalho concluído, sempre deve ser 100%.

lista de saudação de trabalhos é atualizada a cada 30 segundos.

Você pode executar Olá relacionada ao trabalho ações a seguir nesta página:

* Exibir detalhes do trabalho
* Cancelar um trabalho

## <a name="view-job-details"></a>Exibir detalhes do trabalho
Execute Olá etapas tooview Olá detalhes de qualquer trabalho a seguir.

#### <a name="tooview-job-details"></a>detalhes do trabalho tooview
1. Em Olá **trabalhos** página, exibir hello (s) que está interessado executando uma consulta com os filtros apropriados. É possível pesquisar trabalhos concluídos, em execução ou cancelados.
2. Selecione um trabalho.
3. Final Olá Olá página, clique em **detalhes**.
4. Em Olá **detalhes do trabalho de Backup** caixa de diálogo, você pode exibir o status de hello, detalhes, estatísticas de tempo e as estatísticas de dados.
   
    ![Página de detalhes do trabalho](./media/storsimple-manage-jobs-u2/JobDetails.png)

## <a name="cancel-a-job"></a>Cancelar um trabalho
Execute Olá seguindo as etapas toocancel um trabalho em execução.

> [!NOTE]
> Alguns trabalhos, como modificar um tipo de volume do volume toochange hello ou expandir um volume não podem ser cancelados.
> 
> 

### <a name="toocancel-a-job"></a>toocancel um trabalho
1. Em Olá **trabalhos** página, exibir hello em execução (s) que você deseja toocancel executando uma consulta com os filtros apropriados.
2. Selecione o trabalho de saudação.
3. Final Olá Olá página, clique em **Cancelar**.
4. Quando solicitado a confirmar, clique em **Sim**.

Este trabalho agora está cancelado.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[gerenciar suas políticas de backup StorSimple](storsimple-manage-backup-policies.md).
* Saiba como muito[use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).

