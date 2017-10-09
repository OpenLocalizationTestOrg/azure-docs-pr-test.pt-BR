---
title: "aaaClone um volume em série StorSimple 8000 | Microsoft Docs"
description: "Descreve o uso e tipos de clone diferentes hello e explica como você pode usar um conjunto de backup de tooclone um volume individual em um dispositivo da série StorSimple 8000."
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
ms.date: 07/26/2017
ms.author: alkohli
ms.openlocfilehash: 4f7e1f62f17c7b2bd72820a00a5ab87b7e192332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-in-azure-portal-tooclone-a-volume"></a>Usar serviço de Gerenciador de dispositivos de StorSimple Olá em tooclone portal do Azure um volume

## <a name="overview"></a>Visão geral

Este tutorial descreve como você pode usar um tooclone de conjunto de backup de um volume individual por meio de saudação **catálogo de Backup** folha. Ele também explica a diferença de saudação entre *transitório* e *permanente* clones. Guia de saudação neste tutorial se aplica a tooall dispositivo da série StorSimple 8000 do hello executar Update 3 ou posterior.

saudação de serviço do Gerenciador de dispositivos de StorSimple **catálogo de Backup** folha exibe todos os conjuntos de backup de saudação que são criados quando os backups manuais ou automatizados são feitos. Você pode selecionar um volume em um conjunto de backup tooclone.

 ![Lista de conjunto de backup](./media/storsimple-8000-clone-volume-u2/bucatalog.png)

## <a name="considerations-for-cloning-a-volume"></a>Considerações para clonar um volume

Considere Olá informações a seguir ao clonar um volume.

- Um clone se comporta em Olá a maneira como um volume normal. Qualquer operação que é possível em um volume está disponível para o clone hello.

- O monitoramento e o backup padrão são desabilitados automaticamente em um volume clonado. Você precisaria tooconfigure um volume clonado para todos os backups.

- Um volume afixado localmente será clonado como um volume em camadas. Se você precisa hello toobe volume clonado fixado localmente, você pode converter Olá clonar tooa localmente afixado volume após a operação de clonagem Olá for concluída com êxito. Para obter informações sobre como converter um tooa de volume em camadas localmente fixados volume, vá muito[alterar o tipo de volume Olá](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).

- Se você tentar tooconvert que um volume clonado de toolocally hierárquico fixado imediatamente após a clonagem (quando ele ainda é um clone transitório), a conversão de Olá falhar com hello a seguinte mensagem de erro:

    `Unable toomodify hello usage type for volume {0}. This can happen if hello volume being modified is a transient clone and hasn’t been made permanent. Take a cloud snapshot of this volume and then retry hello modify operation.`

    Esse erro é recebido somente se a clonagem de dispositivo diferentes tooa. Você pode converter com êxito Olá volume toolocally fixado se você converter clone permanente da saudação clone transitório tooa. Pegue um instantâneo de saudação clone transitório tooconvert-clone permanente tooa.

## <a name="create-a-clone-of-a-volume"></a>Criar clone de um volume

Você pode criar um clone em Olá mesmo dispositivo, outro dispositivo ou até mesmo um dispositivo de nuvem por meio de um local ou instantâneo na nuvem.

procedimento de saudação abaixo descreve como o catálogo de backup toocreate um clone de saudação.  O clone de tooinitiate um método alternativo é toogo muito**Volumes**, selecione um volume tooinvoke Olá contexto menu de atalho e selecione **Clone**.

Execute Olá seguir etapas toocreate um clone do volume de catálogo de backup hello.

#### <a name="tooclone-a-volume"></a>tooclone um volume

1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go e, em seguida, clique em **catálogo de Backup**.

2. Selecione um conjunto de backup desta maneira:
   
   1. Selecione dispositivo de saudação apropriado.
   2. Na lista suspensa de saudação, escolha política de backup ou volume Olá para backup de saudação que você deseja tooselect.
   3. Especifique o intervalo de tempo de saudação.
   4. Clique em **aplicar** tooexecute esta consulta.

    Hello backups associados à política de backup ou volume Olá selecionado devem aparecer na lista de saudação de conjuntos de backup.
   
    ![Lista de conjunto de backup](./media/storsimple-8000-clone-volume-u2/bucatalog.png)
     
3. Expanda Olá conjunto de backup tooview Olá associado volumes. Esses volumes devem ser colocados offline no host hello e no dispositivo antes de restaurá-los. Acessar volumes Olá Olá **Volumes** folha do seu dispositivo e, em seguida, siga Olá etapas [colocar um volume offline](storsimple-8000-manage-volumes-u2.md#take-a-volume-offline) tootake-los offline.
   
   > [!IMPORTANT]
   > Certifique-se de que você colocou Olá volumes offline no host Olá primeiro, antes de colocar Olá volumes offline no dispositivo de saudação. Se você não colocar volumes de Olá offline no host hello, isso pode levar potencialmente toodata corrupção.
   
4. Navegue back toohello **catálogo de Backup** e selecione um volume em um conjunto de backup. Com o botão direito e, em seguida, no menu de contexto hello, selecione **Clone**.

   ![Lista de conjunto de backup](./media/storsimple-8000-clone-volume-u2/clonevol3b.png) 

3. Em Olá **Clone** folha, Olá seguintes etapas:
   
    1. Identificar um dispositivo de destino. Esse é o local de saudação onde Olá clone será criado. Você pode escolher Olá mesmo dispositivo ou especifique outro dispositivo.

      > [!NOTE]
      > Verifique se capacidade de saudação necessária para o clone Olá é inferior Olá capacidade disponível no dispositivo de destino hello.
       
    2. Especifique um nome de volume exclusivo para o clone. Olá nome deve conter entre 3 e 127 caracteres.
      
        > [!NOTE]
        > Olá **Clone Volume como** campo será **em camadas** mesmo que a clonagem de um volume localmente afixado. Você não pode alterar esta opção. No entanto, se precisar hello toobe volume clonado também fixado localmente, você pode converter Olá clonar tooa localmente afixado volume após a criação de clone de saudação com êxito. Para obter informações sobre como converter um tooa de volume em camadas localmente fixados volume, vá muito[alterar o tipo de volume Olá](storsimple-8000-manage-volumes-u2.md#change-the-volume-type).
          
    3. Em **conectado hosts**, especifique um registro de controle de acesso (ACR) para clonagem de saudação. Você pode adicionar um novo ACR ou escolher na lista existente de saudação. Olá ACR determinará quais hosts podem acessar esse clone.
      
        ![Lista de conjunto de backup](./media/storsimple-8000-clone-volume-u2/clonevol3a.png) 

    4. Clique em **Clone** toocomplete operação de saudação.

4. Um trabalho de clone é iniciado e você será notificado quando clone Olá é criado com êxito. Clique em notificação de trabalho de saudação ou vá muito**trabalhos** trabalho de clone folha toomonitor hello.

    ![Lista de conjunto de backup](./media/storsimple-8000-clone-volume-u2/clonevol5.png)

7. Após a conclusão do trabalho de clone hello, vá tooyour dispositivo e, em seguida, clique em **Volumes**. Na lista de saudação de volumes, você verá o clone Olá que acabou de ser criado no hello mesmo contêiner de volume que tem o volume de origem hello.

    ![Lista de conjunto de backup](./media/storsimple-8000-clone-volume-u2/clonevol6.png)

Um clone criado dessa maneira é um clone transitório. Para obter mais informações sobre os tipos de clone, consulte [Clones transitórios versus permanentes](#transient-vs-permanent-clones).


## <a name="transient-vs-permanent-clones"></a>Clones transitórios versus permanentes
Clones transitórios são criados apenas quando você clona tooanother dispositivo. Você pode clonar um volume específico de um dispositivo diferente da tooa de conjunto de backup gerenciado pelo Olá Gerenciador de dispositivos do StorSimple. clone transitório Olá tem referências toohello dados no volume original hello e usa esse tooread de dados e a gravação localmente no dispositivo de destino de saudação.

Depois que você tire um instantâneo de nuvem do clone transitório, o clone resultante Olá é um *permanente* clone. Durante esse processo, uma cópia dos dados de saudação é criada na nuvem Olá Olá toocopy tempo que esses dados são determinados pelo tamanho da saudação de dados de saudação e Olá latências do Azure (Esta é uma cópia do Azure para o Azure). Esse processo pode levar dias tooweeks. clone transitório Olá se torna um clone permanente e não tem quaisquer referências toohello volume dados originais que foi clonado de.

## <a name="scenarios-for-transient-and-permanent-clones"></a>Cenários para os clones transitórios e permanentes
Olá seções a seguir descreve situações de exemplo no qual clones transitórios e permanentes podem ser usados.

### <a name="item-level-recovery-with-a-transient-clone"></a>Recuperação ao nível do item com um clone transitório
É necessário toorecover um arquivo de apresentação do PowerPoint do Microsoft de um ano atrás. O administrador de TI identifica o backup específico de saudação do tempo e, em seguida, filtros Olá volume. Olá administrador, em seguida, copia o volume de hello, localiza o arquivo hello que você está procurando e fornece tooyou. Nesse cenário, é usado um clone transitório.

### <a name="testing-in-hello-production-environment-with-a-permanent-clone"></a>Teste no ambiente de produção de hello com um clone permanente
É necessário tooverify um bug de teste no ambiente de produção de hello. Criar um clone do volume de saudação no ambiente de produção de hello e, em seguida, pegue um instantâneo de toocreate este clonar um volume clonado independente. Nesse cenário, é usado um clone permanente.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[restaurar de um conjunto de backup de um volume StorSimple](storsimple-8000-restore-from-backup-set-u2.md).
* Saiba como muito[use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

