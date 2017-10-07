---
title: aaaView e gerenciar trabalhos de matriz Virtual StorSimple | Microsoft Docs
description: "Descreve a página de trabalhos de serviço de Gerenciador de dispositivos de StorSimple hello e como toouse-tootrack recente e atual dos trabalhos de saudação matriz Virtual StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 31879821-b599-4609-a7f4-d4b0f658a933
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 11/11/2016
ms.author: alkohli
ms.openlocfilehash: cf3f3e7bcdfff0ff2328b7354db2482286800e93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-tooview-jobs-for-hello-storsimple-virtual-array"></a>Use trabalhos de tooview do serviço de Gerenciador de dispositivos de StorSimple Olá para Olá matriz Virtual StorSimple
## <a name="overview"></a>Visão geral
Olá **trabalhos** folha fornece um único portal central para exibir e gerenciar trabalhos iniciados em matrizes virtuais que estão conectado tooyour serviço do Gerenciador de dispositivos do StorSimple. Você pode exibir os trabalhos em execução, concluídos e com falha para vários dispositivos virtuais. Os resultados são apresentados em um formato tabular.

![Folha de trabalhos](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)

Você pode localizar rapidamente os trabalhos de saudação que está interessado ao filtrar campos, como:

* **Intervalo de tempo** – trabalhos podem ser o intervalo de filtrado Olá com base na data e hora.
* **Dispositivos** – os trabalhos são iniciados em um serviço de tooyour específica do dispositivo conectado. Olá trabalhos filtrados são então tabulados com base em Olá seguintes atributos:
  
  * **Nome** – nome do trabalho Olá pode ser **todos os**, **Backup**, **Clone**, **failover**, **baixar atualizações** , ou **instalar atualizações**.
  * **Status** – Os trabalhos podem ser **Todos**, **Em andamento**, **Concluídos com sucesso**, **Com falha**, ou **Cancelado**.
  * **Entidade** – trabalhos Olá podem ser associados um volume, compartilhamento ou dispositivo.
  * **Dispositivo** – hello nome de dispositivo de saudação na qual Olá o trabalho foi iniciado.
  * **Iniciado em** – tempo de saudação quando o trabalho de saudação foi iniciado.
  * **Duração** – hello duração na qual trabalho Olá foi executada.
* **Status** – você pode pesquisar todos os trabalhos em execução, concluídos ou com falha.
* **Tipo de trabalho** – tipo de trabalho Olá pode ser all, backup, e restauração, failover, baixar atualizações ou instalar atualizações.

lista de saudação de trabalhos é atualizada a cada 30 segundos.

## <a name="view-job-details"></a>Exibir detalhes do trabalho
Execute Olá etapas tooview Olá detalhes de qualquer trabalho a seguir.

#### <a name="tooview-job-details"></a>detalhes do trabalho tooview
1. Em Olá **trabalhos** folha, exibição hello (s) que está interessado executando uma consulta com os filtros apropriados. Você pode pesquisar trabalhos concluídos ou em execução.
2. Selecione um trabalho na lista tabular de saudação de trabalhos.
   
    ![Folha de trabalho](./media/storsimple-virtual-array-manage-jobs/ova-jobs-blade.png)
3. Final Olá Olá página, clique em **detalhes**.
4. Em Olá **detalhes** caixa de diálogo, você pode exibir o status, os detalhes e estatísticas de tempo. Olá, ilustração a seguir mostra um exemplo de hello **detalhes do trabalho de Backup** caixa de diálogo.
   
    ![Detalhes do trabalho](./media/storsimple-virtual-array-manage-jobs/ova-jobs-details.png)

#### <a name="job-failures-when-hello-virtual-machine-is-paused-in-hello-hypervisor"></a>Falhas de trabalho quando a máquina virtual de saudação está em pausa no hipervisor Olá
Quando um trabalho está em andamento na sua matriz Virtual do StorSimple e dispositivo hello (máquina virtual provisionada no hipervisor) está em pausa para mais de 15 minutos, Olá trabalho falhar. Isso é devido ao tempo de matriz Virtual StorSimple tooyour sendo fora de sincronia com o tempo do Microsoft Azure hello. 

Você verá Olá erro a seguir: "o horário do seu dispositivo está fora de sincronia com o tempo do Microsoft Azure Olá por mais de 15 minutos. Certifique-se de que o hipervisor hello e tempos de dispositivo Olá sejam sincronizados com um servidor NTP. Certifique-se de que não haja nenhum problema de conectividade. tootroubleshoot problemas de conectividade, execute testes de diagnóstico da web local de saudação da interface do usuário do seu dispositivo virtual."

Essas falhas aplicam trabalhos toobackup, atualização, failover e restauração. Se sua máquina virtual é provisionada no Hyper-V, máquina Olá eventualmente sincroniza o tempo com o hipervisor. Depois que isso acontece, você pode reiniciar seu trabalho.

## <a name="next-steps"></a>Próximas etapas
[Saiba como toouse Olá tooadminister de interface do usuário da web local sua matriz Virtual StorSimple](storsimple-ova-web-ui-admin.md).

