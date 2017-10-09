---
title: aaaRestore um volume StorSimple de backup | Microsoft Docs
description: "Explica como toouse Olá toorestore de página do Gerenciador do StorSimple serviço Catálogo de Backup a um volume StorSimple um conjunto de backup."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 6f289c39-96c7-4d57-b68a-4bc2e99aef9d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/22/2017
ms.author: alkohli
ms.openlocfilehash: c2e38765e750749f5764b5cbf2167d3cd5edfe5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-storsimple-volume-from-a-backup-set-update-2"></a>Restaurar um volume do StorSimple de um conjunto de backup (Atualização 2)
[!INCLUDE [storsimple-version-selector-restore-from-backup](../../includes/storsimple-version-selector-restore-from-backup.md)]

## <a name="overview"></a>Visão geral
Olá **catálogo de Backup** página exibe todos os conjuntos de backup de saudação que são criados quando os backups manuais ou automatizados são feitos. Use este toolist de página e gerenciar backups, restaurar a partir de um conjunto de backup ou clonar um volume.

 ![Página Catálogo de Backup](./media/storsimple-restore-from-backup-set-u2/restore.png)

Este tutorial explica como Olá toouse **catálogo de Backup** página toorestore seu dispositivo de um conjunto de backup.

Você pode restaurar um volume de um backup local ou na nuvem. Em ambos os casos, a operação de restauração de saudação coloca volume Olá on-line imediatamente, enquanto dados são baixados no plano de fundo de saudação. 

## <a name="before-you-restore"></a>Antes de restaurar
Antes de iniciar uma operação de restauração, você deve estar atento a saudação condições a seguir:

* **Colocar offline o volume de saudação** – coloque o volume de saudação offline em ambos os hosts hello e Olá dispositivo antes de você iniciar a operação de restauração de saudação. Embora a operação de restauração Olá automaticamente coloca o volume de saudação online no dispositivo hello, você deverá colocar manualmente dispositivo Olá on-line no host de saudação. Você pode colocar o volume Olá on-line no host de saudação quando o volume de saudação for on-line no dispositivo de saudação. (Você não precisa toowait até a conclusão da operação de restauração hello.) Para procedimentos, vá muito[colocar um volume offline](storsimple-manage-volumes-u2.md#take-a-volume-offline).
* **O tipo de volume após a restauração** – volumes excluídos são restaurados com base no tipo de saudação no instantâneo de saudação. Os volumes que foram fixados localmente são restaurados como volumes fixados localmente, e os volumes separados em camadas são restaurados como volumes em camadas.
  
    Para os volumes existentes, tipo de uso atual saudação do volume Olá substitui tipo de saudação que é armazenado no instantâneo de saudação. Por exemplo, se você restaurar um volume de um instantâneo que foi feito quando o tipo de volume Olá foi hierárquico e que tipo de volume agora é localmente fixados (devido a operação de conversão tooa), em seguida, o volume de saudação será restaurado como um volume localmente afixado. Da mesma forma, se um volume localmente afixado existente é expandido e subsequentemente restaurado a partir de um instantâneo mais antigo executado quando o volume de saudação era menor, hello volume restaurado retém tamanho expandido atual de saudação.
  
    Não é possível converter um volume de um volume do volume em camadas tooa localmente afixado ou _o contrário_ enquanto o volume de hello está sendo restaurado. Aguarde até que a conclusão da operação de restauração hello e, em seguida, você pode converter o tipo de tooanother de volume Olá. Para obter informações sobre como converter um volume, vá muito[alterar o tipo de volume Olá](storsimple-manage-volumes-u2.md#change-the-volume-type). 
* **Olá tamanho do volume é refletido no volume Olá restaurado** – essa é uma consideração importante, se você estiver restaurando um volume localmente afixado que foi excluído (porque os volumes localmente afixados totalmente provisionados). Certifique-se de que você tem espaço suficiente antes de tentar toorestore um volume localmente afixado que tenha sido excluído anteriormente. 
* **Você não pode expandir um volume enquanto ele está sendo restaurado** – Aguarde até que a operação de restauração Olá for concluída antes de tentar tooexpand volume de saudação. Para obter informações sobre como expandir um volume, vá muito[modificar um volume](storsimple-manage-volumes-u2.md#modify-a-volume).
* **Você pode executar um backup enquanto você estiver restaurando um volume local** – para procedimentos, vá muito[usar políticas de backup do hello Gerenciador StorSimple service toomanage](storsimple-manage-backup-policies.md).
* **Você pode cancelar uma operação de restauração** – se você cancelar trabalho de restauração hello, volume de saudação é revertida toohello estado que estava antes de você iniciou a restauração de saudação. Para procedimentos, vá muito[cancelar um trabalho](storsimple-manage-jobs-u2.md#cancel-a-job).

## <a name="how-does-restore-work"></a>Como restaurar o trabalho
Para dispositivos que estão executando a Atualização 4 ou posterior, uma restauração baseada em mapa de calor é implementada. Como Olá host solicitações tooaccess dados atingirem o dispositivo hello, essas solicitações são rastreadas e um mapa de calor é criado. Alta taxa de resulta em blocos de dados com maior calor enquanto menor taxa de solicitação converte toochunks com calor inferior. Você deve acessar Olá dados pelo menos duas vezes toobe marcado como _hot_. Um arquivo que é modificado também é marcado como _quente_. Quando você iniciar a restauração hello, pró-ativo hidratação de dados ocorre com base no mapa de calor de saudação. Para versões anteriores à atualização 4, dados saudação foi baixados durante a restauração com base no acesso somente. 

O controle baseado em mapa de calor é habilitado somente para volumes com camadas, e não há suporte para volumes fixados localmente. Restauração baseada em mapa de calor também não há suporte ao clonar um volume tooanother dispositivo. Se houver uma restauração no local e um instantâneo local para Olá volume toobe restaurado existe no dispositivo hello, em seguida, nós não realimentar (como os dados já estão disponíveis localmente). Por padrão, quando você restaurar, Olá reidratação trabalhos são iniciados que proativamente realimentar dados com base no mapa de calor de saudação. Na atualização 4, cmdlets do Windows PowerShell podem ser usado tooquery reidratação trabalhos em execução, cancelar um trabalho de reidratação e obter o status de saudação do trabalho de reidratação hello.

* `Get-HcsRehydrationJob`-Este cmdlet obtém o status de saudação do trabalho de reidratação hello. Um único trabalho de reidratação é disparado para um volume.
* `Set-HcsRehydrationJob`-Este cmdlet permite toopause, interromper, continuar Olá reidratação trabalho quando reidratação hello está em andamento. 

Para obter mais informações sobre os cmdlets reidratação, vá muito[referência de cmdlet do Windows PowerShell para StorSimple](https://technet.microsoft.com/library/dn688168.aspx).

Com a reidratação automática, espera-se um desempenho de leitura transitório normalmente mais alto. saudação magniutde real das melhorias depende de vários fatores, como o padrão de acesso, a variação de dados e tipo de dados. toocancel um trabalho reidratação, você pode usar o cmdlet do PowerShell hello. Se você quiser toopermanently desabilitar reidratação trabalhos todas as restaurações de futuras hello, entre em contato com o Microsoft Support.

## <a name="how-toouse-hello-backup-catalog"></a>Como toouse Olá catálogo de backup
Olá **catálogo de Backup** página fornece uma consulta que ajuda você a toonarrow sua seleção de conjunto de backup. Você pode filtrar Olá conjuntos de backup que são recuperados com base em Olá parâmetros a seguir:

* **Dispositivo** – dispositivo Olá no qual Olá o conjunto de backup foi criado.
* **Política de backup** ou **volume** – Olá a política de backup ou volume associado a este conjunto de backup.
* **De** e **para** – Olá intervalo de data e hora quando o conjunto de backup Olá foi criado.

Olá conjuntos de backup filtrados são então tabulados com base em Olá seguintes atributos:

* **Nome** – hello nome de política de backup hello ou volumes associados ao conjunto de backup hello.
* **Tamanho** – Olá tamanho real do conjunto de backup hello.
* **Criado em** – a data de saudação e a hora quando foram criados backups hello. 
* **Tipo** – Conjuntos de Backup podem ser instantâneos locais ou instantâneos de nuvem. Um instantâneo local é um backup de todos os dados de volume armazenados localmente no dispositivo de saudação. Um instantâneo de nuvem se refere a toohello backup dos dados de volume que residem na nuvem hello. Instantâneos locais fornecem acesso mais rápido, enquanto os instantâneos de nuvem são escolhidos para resiliência de dados.
* **Iniciado por** – backups Olá podem ser iniciados automaticamente de acordo com o agendamento de tooa ou manualmente por você. (Você pode usar backups de tooschedule uma política de backup. Como alternativa, você pode usar o hello **fazer backup** tootake opção um backup interativo.)

## <a name="how-toorestore-your-storsimple-volume-from-a-backup"></a>Como toorestore seu volume StorSimple de um backup
Você pode usar o hello **catálogo de Backup** página toorestore seu volume StorSimple de um backup específico. Lembre-se, no entanto, que a restauração de um volume reverte o estado de toohello volume Olá que estava quando foi feito backup hello. Os dados que foi adicionados após a operação de backup hello serão perdidos.

> [!WARNING]
> Restauração de um backup substituirá os volumes existentes de backup Olá Olá. Isso pode causar perda de saudação de todos os dados gravados após Olá backup foi feito.
> 
> 

### <a name="toorestore-your-volume"></a>toorestore seu volume
1. Na página de serviço do StorSimple Manager hello, clique em Olá **catálogo de Backup** guia.
   
    ![Catálogo de backup](./media/storsimple-restore-from-backup-set-u2/restore.png)
2. Selecione um conjunto de backup desta maneira:
   
   1. Selecione dispositivo de saudação apropriado.
   2. Na lista suspensa de saudação, escolha política de backup ou volume Olá para backup de saudação que você deseja tooselect.
   3. Especifique o intervalo de tempo de saudação.
   4. Clique o ícone de verificação Olá ![ícone de verificação](./media/storsimple-restore-from-backup-set-u2/HCS_CheckIcon.png) tooexecute esta consulta.
      
      Hello backups associados à política de backup ou volume Olá selecionado devem aparecer na lista de saudação de conjuntos de backup.
3. Expanda Olá conjunto de backup tooview Olá associado volumes. Esses volumes devem ser colocados offline no host hello e no dispositivo antes de restaurá-los. Acessar volumes Olá Olá **contêineres de Volume** página e, em seguida, execute as etapas de saudação em [colocar um volume offline](storsimple-manage-volumes-u2.md#take-a-volume-offline) tootake-los offline.
   
   > [!IMPORTANT]
   > Certifique-se de que você colocou Olá volumes offline no host Olá primeiro, antes de colocar Olá volumes offline no dispositivo de saudação. Se você não colocar volumes de Olá offline no host hello, isso pode levar potencialmente toodata corrupção.
   > 
   > 
4. Navegue back toohello **catálogo de Backup** guia e selecione um conjunto de backup.
5. Clique em **restaurar** final Olá Olá página.
6. Você recebe uma solicitação para fornecer sua confirmação. Saudação de revisão restaurar as informações e, em seguida, selecione caixa de seleção de confirmação de saudação.
   
    ![Página de confirmação](./media/storsimple-restore-from-backup-set-u2/ConfirmRestore.png)
7. Clique o ícone de verificação Olá ![ícone de verificação](./media/storsimple-restore-from-backup-set-u2/HCS_CheckIcon.png). Um trabalho de restauração começa. Você pode exibir o trabalho de saudação acessando Olá **trabalhos** página. 
8. Após a conclusão da restauração hello, você pode verificar se conteúdo Olá de seus volumes é substituído por volumes de backup hello.

![Vídeo disponível](./media/storsimple-restore-from-backup-set-u2/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como você pode usar o clone hello e restaurar recursos no StorSimple toorecover excluído arquivos, clique em [aqui](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

## <a name="if-hello-restore-fails"></a>Se restaurar Olá falhar
Você receberá um alerta se haverá falha na operação de restauração Olá por qualquer motivo. Se isso ocorrer, tooverify de lista de backup do hello atualização Olá backup ainda é válido. Se Olá backup é válido e você estiver restaurando de nuvem Olá, em seguida, problemas de conectividade podem estar causando Olá problema. 

Olá toocomplete operação de restauração, coloque o volume de saudação offline no host hello e repita a operação de restauração de saudação. Nenhum dado de volume toohello modificações que foram executados durante o processo de restauração hello serão perdidos.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[StorSimple gerenciar volumes](storsimple-manage-volumes-u2.md).
* Saiba como muito[use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).

