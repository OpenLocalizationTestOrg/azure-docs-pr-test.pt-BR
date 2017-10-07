---
title: "aaaRestore um volume de backup em uma série StorSimple 8000 | Microsoft Docs"
description: "Explica como toouse Olá toorestore de catálogo de Backup do serviço de Gerenciador de dispositivos de StorSimple um volume StorSimple um conjunto de backup."
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
ms.date: 05/23/2017
ms.author: alkohli
ms.openlocfilehash: 0fe2e4c23a23c75ce4058a8531356c94c973c6f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set"></a>Restaurar um volume do StorSimple de um conjunto de backup

## <a name="overview"></a>Visão geral

Este tutorial descreve a operação de restauração Olá executada em um dispositivo da série StorSimple 8000 usando um conjunto de backup existente. Saudação de uso **catálogo de Backup** folha toorestore um volume de um local ou backup na nuvem. Olá **catálogo de Backup** folha exibe todos os conjuntos de backup de saudação que são criados quando os backups manuais ou automatizados são feitos. a operação de um conjunto de backup restauração Olá coloca o volume de saudação online imediatamente, enquanto dados são baixados no plano de fundo de saudação.

Restauração de toostart um método alternativo é toogo muito**dispositivos > [seu dispositivo] > Volumes**. Em Olá **Volumes** folha, selecione um volume, tooinvoke Olá menu de contexto e, em seguida, selecione **restauração**.

## <a name="before-you-restore"></a>Antes de restaurar

Antes de iniciar uma restauração, revise Olá condições a seguir:

* **Você deve colocar o volume de saudação offline** – coloque o volume de saudação offline em ambos os hosts hello e Olá dispositivo antes de você iniciar a operação de restauração de saudação. Embora a operação de restauração Olá automaticamente coloca o volume de saudação online no dispositivo hello, você deverá colocar manualmente dispositivo Olá on-line no host de saudação. Você pode colocar o volume Olá on-line no host hello como volume hello está online no dispositivo de saudação. (Você não precisa toowait até a conclusão da operação de restauração hello.) Para procedimentos, vá muito[colocar um volume offline](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline).

* **O tipo de volume após a restauração** – volumes excluídos são restaurados com base no tipo de saudação no instantâneo Olá; ou seja, volumes que foram localmente fixados serão restaurados como volumes localmente afixados e volumes que foram organizadas em camadas são restaurados como volumes em camadas.

    Para os volumes existentes, tipo de uso atual saudação do volume Olá substitui tipo de saudação que é armazenado no instantâneo de saudação. Por exemplo, se você restaurar um volume de um instantâneo que foi feito quando o tipo de volume Olá foi hierárquico e que tipo de volume agora é localmente fixados (devido a operação de conversão de tooa que foi executada), volume de saudação será restaurado como um volume localmente afixado. Da mesma forma, se um volume localmente afixado existente foi expandido e subsequentemente restaurado a partir de um instantâneo mais antigo executado quando o volume de saudação era menor, hello volume restaurado manterão tamanho expandido atual de saudação.

    Não é possível converter um volume de um volume do volume em camadas tooa fixado localmente ou de um volume localmente afixado tooa hierárquico volume enquanto o volume de hello está sendo restaurado. Aguarde até que a conclusão da operação de restauração hello e, em seguida, você pode converter o tipo de tooanother de volume Olá. Para obter informações sobre como converter um volume, vá muito[alterar o tipo de volume Olá](storsimple-8000-manage-volumes-u2.md#change-the-volume-type). 

* **Olá tamanho do volume é refletido no volume Olá restaurado** – essa é uma consideração importante, se você estiver restaurando um volume localmente afixado que foi excluído (porque os volumes localmente afixados totalmente provisionados). Certifique-se de que você tem espaço suficiente antes de tentar toorestore um volume localmente afixado que tenha sido excluído anteriormente.

* **Você não pode expandir um volume enquanto ele está sendo restaurado** – Aguarde até que a operação de restauração Olá for concluída antes de tentar tooexpand volume de saudação. Para obter informações sobre como expandir um volume, vá muito[modificar um volume](storsimple-8000-manage-volumes-u2.md#modify-a-volume).

* **Você pode executar um backup enquanto você restaurar um volume local** – para procedimentos, vá muito[usar políticas de backup do hello Gerenciador de dispositivos do StorSimple service toomanage](storsimple-8000-manage-backup-policies-u2.md).

* **Você pode cancelar uma operação de restauração** – se você cancelar trabalho de restauração hello, volume de saudação será revertida toohello estado que estava antes de você iniciou a operação de restauração de saudação. Para procedimentos, vá muito[cancelar um trabalho](storsimple-8000-manage-jobs-u2.md#cancel-a-job).

## <a name="how-does-restore-work"></a>Como restaurar o trabalho

Para dispositivos que estão executando a Atualização 4 ou posterior, uma restauração baseada em mapa de calor é implementada. Como Olá host solicitações tooaccess dados atingirem o dispositivo hello, essas solicitações são rastreadas e um mapa de calor é criado. Alta taxa de resulta em blocos de dados com maior calor enquanto menor taxa de solicitação converte toochunks com calor inferior. Você deve acessar Olá dados pelo menos duas vezes toobe marcado como _hot_. Um arquivo que é modificado também é marcado como _quente_. Quando você iniciar a restauração hello, pró-ativo hidratação de dados ocorre com base no mapa de calor de saudação. Para versões anteriores à atualização 4, dados saudação são baixados durante a restauração com base no acesso somente.

Olá condições a seguir se aplicam a restaurações de tooheatmap:

* O acompanhamento de mapa de calor é habilitado somente para volumes em camadas e não há suporte para volumes fixados localmente.

* Não há suporte para restauração baseada em mapa de calor ao clonar um volume tooanother dispositivo. 

* Se houver uma restauração no local e um instantâneo local para Olá volume toobe restaurado existe no dispositivo hello, em seguida, nós não realimentar (como os dados já estão disponíveis localmente). 

* Por padrão, quando você restaurar, Olá reidratação trabalhos são iniciados que proativamente realimentar dados com base no mapa de calor de saudação. 

Na atualização 4, cmdlets do Windows PowerShell podem ser usado tooquery reidratação trabalhos em execução, cancelar um trabalho de reidratação e obter o status de saudação do trabalho de reidratação hello.

* `Get-HcsRehydrationJob`-Este cmdlet obtém o status de saudação do trabalho de reidratação hello. Um único trabalho de reidratação é disparado para um volume.

* `Set-HcsRehydrationJob`-Este cmdlet permite toopause, interromper, continuar Olá reidratação trabalho quando reidratação hello está em andamento.

Para obter mais informações sobre os cmdlets reidratação, vá muito[referência de cmdlet do Windows PowerShell para StorSimple](https://technet.microsoft.com/library/dn688168.aspx).

Com a reidratação automática, espera-se um desempenho de leitura transitório normalmente mais alto. saudação magniutde real das melhorias depende de vários fatores, como o padrão de acesso, a variação de dados e tipo de dados. 

toocancel um trabalho reidratação, você pode usar o cmdlet do PowerShell hello. Se você quiser trabalhos de reidratação desabilitar toopermanently para todos os Olá restaurações futuras, [entre em contato com o Microsoft Support](storsimple-8000-contact-microsoft-support.md).

## <a name="how-toouse-hello-backup-catalog"></a>Como toouse Olá catálogo de backup

Olá **catálogo de Backup** folha fornece uma consulta que ajuda você a toonarrow sua seleção de conjunto de backup. Você pode filtrar Olá conjuntos de backup que são recuperados com base em Olá parâmetros a seguir:

* **Intervalo de tempo** – Olá intervalo de data e hora quando o conjunto de backup Olá foi criado.
* **Dispositivo** – dispositivo Olá no qual Olá o conjunto de backup foi criado.
* **Política de backup** ou **Volume** – Olá a política de backup ou volume associado a este conjunto de backup.

Olá conjuntos de backup filtrados são então tabulados com base em Olá seguintes atributos:

* **Nome** – hello nome de política de backup hello ou volumes associados ao conjunto de backup hello.
* **Tipo** – Conjuntos de Backup podem ser instantâneos locais ou instantâneos de nuvem. Um instantâneo local é um backup de todos os dados de volume armazenados localmente no dispositivo hello, enquanto um instantâneo de nuvem se refere a toohello backup dos dados de volume que residem na nuvem de saudação. Instantâneos locais fornecem acesso mais rápido, enquanto os instantâneos de nuvem são escolhidos para resiliência de dados.
* **Tamanho** – Olá tamanho real do conjunto de backup hello.
* **Criado em** – a data de saudação e a hora quando foram criados backups hello. 
* **Volumes** -Olá número de volumes associados ao conjunto de backup hello.
* **Iniciada** – backups Olá podem ser iniciados automaticamente de acordo com o agendamento de tooa ou manualmente por um usuário. (Você pode usar backups de tooschedule uma política de backup. Como alternativa, você pode usar o hello **fazer backup** tootake opção um backup interativo ou sob demanda.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Como toorestore seu volume StorSimple de um backup

Você pode usar o hello **catálogo de Backup** toorestore folha seu volume StorSimple de um backup específico. Lembre-se, no entanto, que a restauração de um volume será revertido Olá volume toohello estado quando foi feito backup de saudação. Os dados que foi adicionados após a operação de backup hello serão perdidos.

> [!WARNING]
> Restauração de um backup substituirá os volumes existentes de backup Olá Olá. Isso pode causar perda de saudação de todos os dados gravados após Olá backup foi feito.


### <a name="toorestore-your-volume"></a>toorestore seu volume
1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e, em seguida, clique em **catálogo de Backup**.

2. Selecione um conjunto de backup desta maneira:
   
   1. Especifique o intervalo de tempo de saudação.
   2. Selecione dispositivo de saudação apropriado.
   3. Na lista suspensa de saudação, escolha política de backup ou volume Olá para backup de saudação que você deseja tooselect.
   4. Clique em **aplicar** tooexecute esta consulta.

    Hello backups associados à política de backup ou volume Olá selecionado devem aparecer na lista de saudação de conjuntos de backup.
   
    ![Lista de conjunto de backup](./media/storsimple-8000-restore-from-backup-set-u2/bucatalog.png)     
     
3. Expanda Olá conjunto de backup tooview Olá associado volumes. Esses volumes devem ser colocados offline no host hello e no dispositivo antes de restaurá-los. Acessar volumes Olá Olá **Volumes** folha do seu dispositivo e, em seguida, siga Olá etapas [colocar um volume offline](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake-los offline.
   
   > [!IMPORTANT]
   > Certifique-se de que você colocou Olá volumes offline no host Olá primeiro, antes de colocar Olá volumes offline no dispositivo de saudação. Se você não colocar volumes de Olá offline no host hello, isso pode levar potencialmente toodata corrupção.
   
4. Navegue back toohello **catálogo de Backup** guia e selecione um conjunto de backup. Com o botão direito e, em seguida, no menu de contexto hello, selecione **restauração**.

    ![Lista de conjunto de backup](./media/storsimple-8000-restore-from-backup-set-u2/restorebu1.png)

5. Será solicitada a sua confirmação. Saudação de revisão restaurar as informações e, em seguida, selecione caixa de seleção de confirmação de saudação.
   
    ![Página de confirmação](./media/storsimple-8000-restore-from-backup-set-u2/restorebu2.png)

7.  Clique em **Restaurar**. Isso inicia um trabalho de restauração que você pode exibir acessando Olá **trabalhos** página.

    ![Página de confirmação](./media/storsimple-8000-restore-from-backup-set-u2/restorebu5.png)

8. Após a conclusão da restauração Olá, verifique se conteúdo Olá de seus volumes é substituído por volumes de backup de saudação.


## <a name="if-hello-restore-fails"></a>Se restaurar Olá falhar

Você receberá um alerta se haverá falha na operação de restauração Olá por qualquer motivo. Se isso ocorrer, tooverify de lista de backup do hello atualização Olá backup ainda é válido. Se Olá backup é válido e você estiver restaurando de nuvem Olá, em seguida, problemas de conectividade podem estar causando Olá problema.

Olá toocomplete operação de restauração, coloque o volume de saudação offline no host hello e repita a operação de restauração de saudação. Observe que quaisquer dados de volume toohello modificações que foram executados durante a saudação processo de restauração serão perdida.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[StorSimple gerenciar volumes](storsimple-8000-manage-volumes-u2.md).
* Saiba como muito[use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

