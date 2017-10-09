---
title: "aaaClone volume de série StorSimple 8000 | Microsoft Docs"
description: "Descreve os tipos diferentes de clone hello e quando toouse-los e explica como você pode usar um conjunto de backup de tooclone um volume individual."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 070ac53e-7388-4c48-b8a5-8ed7f9108b2c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: f457625d2e3aa173f7ccf26984e1902a64e33b5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume-update-2"></a>Use Olá StorSimple Manager serviço tooclone um volume (atualização 2)
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>Visão geral
Olá serviço StorSimple Manager **catálogo de Backup** página exibe todos os conjuntos de backup de saudação que são criados quando os backups manuais ou automatizados são feitos. Você pode usar todos os backups de saudação de toolist essa página para uma política de backup ou um volume, selecione ou excluir backups, ou usar um backup toorestore ou clonar um volume.

![Página Catálogo de backup](./media/storsimple-clone-volume-u2/backupCatalog.png)  

Este tutorial descreve como você pode usar um conjunto de backup de tooclone um volume individual. Ele também explica a diferença de saudação entre *transitório* e *permanente* clones.

> [!NOTE]
> Um volume fixo local será clonado como um volume em camadas. Se você precisa hello toobe volume clonado fixado localmente, você pode converter Olá clonar tooa localmente afixado volume após a operação de clonagem Olá for concluída com êxito. Para obter informações sobre como converter um tooa de volume em camadas localmente fixados volume, vá muito[alterar o tipo de volume Olá](storsimple-manage-volumes-u2.md#change-the-volume-type).
> 
> Se você tentar tooconvert que um volume clonado de toolocally hierárquico fixado imediatamente após a clonagem (quando ele ainda é um clone transitório), a conversão Olá falhará com Olá a seguinte mensagem de erro:
> 
> `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.` 
> 
> Esse erro é recebido somente se a clonagem de dispositivo diferentes tooa. Você pode converter com êxito Olá volume toolocally fixado se você converter clone permanente da saudação clone transitório tooa. tooconvert Olá clone transitório tooa permanente clone, pegue um instantâneo dele.
> 
> 

## <a name="create-a-clone-of-a-volume"></a>Criar clone de um volume
Você pode criar um clone em Olá mesmo dispositivo, outro dispositivo ou mesmo uma máquina virtual usando um local ou instantâneo na nuvem.

#### <a name="tooclone-a-volume"></a>tooclone um volume
1. Na página de serviço do StorSimple Manager hello, clique em Olá **catálogo de Backup** guia e selecione um conjunto de backup.
2. Expanda Olá conjunto de backup tooview Olá associado volumes. Clique em e selecione um volume de conjunto de backup hello.
   
     ![Clonar um volume](./media/storsimple-clone-volume-u2/CloneVol.png) 
3. Clique em **Clone** toobegin clonar volume Olá selecionado.
4. No Assistente para clonar Volume de hello, em **especificar nome e local**:
   
   1. Identificar um dispositivo de destino. Esse é o local de saudação onde Olá clone será criado. Você pode escolher Olá mesmo dispositivo ou especifique outro dispositivo. Se você escolher um volume associado com outros provedores de serviços de nuvem (não do Azure), Olá suspensa lista para o dispositivo de destino Olá mostrará apenas os dispositivos físicos. Não é possível clonar um volume associado a outros provedores de serviço de nuvem em um dispositivo virtual.
      
      > [!NOTE]
      > Verifique se capacidade de saudação necessária para o clone Olá é inferior Olá capacidade disponível no dispositivo de destino hello.
      > 
      > 
   2. Especifique um nome de volume exclusivo para o clone. Olá nome deve conter entre 3 e 127 caracteres. 
      
      > [!NOTE]
      > Olá **Clone Volume como** campo será **em camadas** mesmo que a clonagem de um volume localmente afixado. Você não pode alterar esta opção. No entanto, se precisar hello toobe volume clonado também fixado localmente, você pode converter Olá clonar tooa localmente afixado volume após a criação de clone de saudação com êxito. Para obter informações sobre como converter um tooa de volume em camadas localmente fixados volume, vá muito[alterar o tipo de volume Olá](storsimple-manage-volumes-u2.md#change-the-volume-type).
      > 
      > 
      
        ![Assistente de clone 1](./media/storsimple-clone-volume-u2/clone1.png) 
   3. Clique no ícone de seta Olá ![ícone-de-seta](./media/storsimple-clone-volume-u2/HCS_ArrowIcon.png) tooproceed toohello próxima página.
5. Em **Especificar os hosts que podem usar este volume**:
   
   1. Especifique um registro de controle de acesso (ACR) para clonagem de saudação. Você pode adicionar um novo ACR ou escolher na lista existente de saudação.
      
        ![Assistente de clone 2](./media/storsimple-clone-volume-u2/clone2.png) 
   2. Clique o ícone de verificação Olá ![check-icon](./media/storsimple-clone-volume-u2/HCS_CheckIcon.png)operação de saudação toocomplete.
6. Um trabalho de clone será iniciado e você será notificado quando clone Olá é criado com êxito. Clique em **Exibir trabalho** toomonitor trabalho de clone de saudação em Olá **trabalhos** página. Você verá Olá a seguinte mensagem quando o trabalho de clone Olá for concluído:
   
    ![Mensagem de clone](./media/storsimple-clone-volume-u2/CloneMsg.png) 
7. Depois de saudação trabalho de clonagem é concluído:
   
   1. Vá toohello **dispositivos** página e selecione Olá **contêineres de Volume** guia. 
   2. Selecione o contêiner de volume de saudação que está associado ao volume de origem Olá que você clonou. Na lista de saudação de volumes, você deve ver o clone Olá que acabou de ser criado.

> [!NOTE]
> O monitoramento e o backup padrão são desabilitados automaticamente em um volume clonado.
> 
> 

Um clone criado dessa maneira é um clone transitório. Para obter mais informações sobre os tipos de clone, consulte [Clones transitórios versus permanentes](#transient-vs-permanent-clones).

O clone está agora um volume normal e qualquer operação que é possível em um volume estará disponível para o clone hello. Você precisará tooconfigure este volume para todos os backups.

## <a name="transient-vs-permanent-clones"></a>Clones transitórios versus permanentes
Clones transitórios são criados apenas quando a clonagem de tooa outro dispositivo. Você pode clonar um volume específico de um dispositivo diferente da tooa de conjunto de backup gerenciado pelo Olá StorSimple Manager. clone transitório Olá terá referências toohello dados no volume original hello e será usar tooread que dados e gravar localmente no dispositivo de destino hello. 

Depois que você tire um instantâneo de nuvem do clone transitório, o clone resultante Olá será um *permanente* clone. Durante esse processo, uma cópia dos dados de saudação é criada na nuvem Olá Olá toocopy tempo que esses dados são determinados pelo tamanho da saudação de dados de saudação e Olá latências do Azure (Esta é uma cópia do Azure para o Azure). Esse processo pode levar dias tooweeks. clone transitório Olá se torna um clone permanente dessa maneira e não tem quaisquer referências toohello volume dados originais que foi clonado de. 

## <a name="scenarios-for-transient-and-permanent-clones"></a>Cenários para os clones transitórios e permanentes
Olá seções a seguir descreve situações de exemplo no qual clones transitórios e permanentes podem ser usados.

### <a name="item-level-recovery-with-a-transient-clone"></a>Recuperação ao nível do item com um clone transitório
É necessário toorecover um arquivo de apresentação do PowerPoint do Microsoft de um ano atrás. O administrador de TI identifica o backup específico de saudação do intervalo de tempo e, em seguida, filtros Olá volume. Olá administrador, em seguida, copia o volume de hello, localiza o arquivo hello que você está procurando e fornece tooyou. Nesse cenário, é usado um clone transitório. 

![Vídeo disponível](./media/storsimple-clone-volume-u2/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como você pode usar o clone hello e restaurar recursos no StorSimple toorecover excluído arquivos, clique em [aqui](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Teste no ambiente de produção de hello com um clone permanente
É necessário tooverify um bug de teste no ambiente de produção de hello. Criar um clone do volume de saudação no ambiente de produção de hello e, em seguida, pegue um instantâneo de toocreate este clonar um volume clonado independente. Nesse cenário, é usado um clone permanente.  

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[restaurar de um conjunto de backup de um volume StorSimple](storsimple-restore-from-backup-set-u2.md).
* Saiba como muito[use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).

