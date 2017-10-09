---
title: aaaClone seu volume StorSimple | Microsoft Docs
description: "Descreve os tipos diferentes de clone hello e quando toouse-los e explica como você pode usar um conjunto de backup de tooclone um volume individual."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b5d615f2-02a7-4222-9867-6c0385ce748c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: e98d28db1abeb515ba78ab5860e7c5eba0dfcbb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooclone-a-volume"></a>Use Olá StorSimple Manager serviço tooclone um volume
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>Visão geral
Olá serviço StorSimple Manager **catálogo de Backup** página exibe todos os conjuntos de backup de saudação que são criados quando os backups manuais ou automatizados são feitos. Você pode usar todos os backups de saudação de toolist essa página para uma política de backup ou um volume, selecione ou excluir backups, ou usar um backup toorestore ou clonar um volume.

![Página Catálogo de backup](./media/storsimple-clone-volume/HCS_BackupCatalog.png)  

Este tutorial descreve como você pode usar um conjunto de backup de tooclone um volume individual. Ele também explica a diferença de saudação entre *transitório* e *permanente* clones. 

## <a name="create-a-clone-of-a-volume"></a>Criar clone de um volume
Você pode criar um clone em Olá mesmo dispositivo, outro dispositivo ou até mesmo uma máquina virtual usando um local ou um instantâneo na nuvem.

#### <a name="tooclone-a-volume"></a>tooclone um volume
1. Na página de serviço do StorSimple Manager hello, clique em Olá **catálogo de Backup** guia e selecione um conjunto de backup.
2. Expanda Olá conjunto de backup tooview Olá associado volumes. Clique em e selecione um volume de conjunto de backup hello.
   
     ![Clonar um volume](./media/storsimple-clone-volume/HCS_Clone.png) 
3. Clique em **Clone** toobegin clonar volume Olá selecionado.
4. No Assistente para clonar Volume de hello, em **especificar nome e local**:
   
   1. Identificar um dispositivo de destino. Esse é o local de saudação onde Olá clone será criado. Você pode escolher Olá mesmo dispositivo ou especifique outro dispositivo. Se você escolher um volume associado com outros provedores de serviços de nuvem (não do Azure), Olá suspensa lista para o dispositivo de destino Olá mostrará apenas os dispositivos físicos. Não é possível clonar um volume associado a outros provedores de serviço de nuvem em um dispositivo virtual.
      
      > [!NOTE]
      > Verifique se capacidade de saudação necessária para o clone Olá é inferior Olá capacidade disponível no dispositivo de destino hello.
      > 
      > 
   2. Especifique um nome de volume exclusivo para o clone. Olá nome deve conter entre 3 e 127 caracteres.
   3. Clique no ícone de seta Olá ![ícone-de-seta](./media/storsimple-clone-volume/HCS_ArrowIcon.png) tooproceed toohello próxima página.
5. Em **Especificar os hosts que podem usar este volume**:
   
   1. Especifique um registro de controle de acesso (ACR) para clonagem de saudação. Você pode adicionar um novo ACR ou escolher na lista existente de saudação.
   2. Clique o ícone de verificação Olá ![check-icon](./media/storsimple-clone-volume/HCS_CheckIcon.png)operação de saudação toocomplete.
6. Um trabalho de clone será iniciado e você será notificado quando clone Olá é criado com êxito. Clique em **Exibir trabalho** toomonitor trabalho de clone de saudação em Olá **trabalhos** página.
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
Clones transitórios e permanentes são criados apenas quando a clonagem de dispositivo diferentes tooa. Você pode clonar um volume específico de um dispositivo diferente do conjunto de backup tooa. Um clone criado dessa maneira é um clone *transitório* . clone transitório Olá terá referências toohello original volume e usará esse volume tooread enquanto grava localmente. 

Depois que você tire um instantâneo de nuvem do clone transitório, o clone resultante Olá será um *permanente* clone. clone permanente Olá é independente e não tem qualquer volume original de toohello de referências foi clonado de.  

## <a name="scenarios-for-transient-and-permanent-clones"></a>Cenários para os clones transitórios e permanentes
Olá seções a seguir descreve situações de exemplo no qual clones transitórios e permanentes podem ser usados.

### <a name="item-level-recovery-with-a-transient-clone"></a>Recuperação ao nível do item com um clone transitório
É necessário toorecover um arquivo de apresentação do PowerPoint do Microsoft de um ano atrás. O administrador de TI identifica o backup específico de saudação do intervalo de tempo e, em seguida, filtros Olá volume. Olá administrador, em seguida, copia o volume de hello, localiza o arquivo hello que você está procurando e fornece tooyou. Nesse cenário, é usado um clone transitório. 

![Vídeo disponível](./media/storsimple-clone-volume/Video_icon.png) **Vídeo disponível**

toowatch um vídeo que demonstra como você pode usar o clone hello e restaurar recursos no StorSimple toorecover excluído arquivos, clique em [aqui](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Teste no ambiente de produção de hello com um clone permanente
É necessário tooverify um bug de teste no ambiente de produção de hello. Você pode criar um clone do volume de saudação no ambiente de produção de hello obtendo um instantâneo de nuvem desse clone. Olá volume clonado agora é independente. Nesse cenário, é usado um clone permanente.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[restaurar de um conjunto de backup de um volume StorSimple](storsimple-restore-from-backup-set.md).
* Saiba como muito[use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).

