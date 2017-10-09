---
title: aaaClone um backup de matriz Virtual StorSimple | Microsoft Docs
description: Saiba como tooclone um backup e recuperar um arquivo de sua matriz Virtual StorSimple.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: af6e979c-55e3-477c-b53e-a76a697f80c9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: 21bfcae48ee07762179cf00ce842b6094abe18ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="clone-from-a-backup-of-your-storsimple-virtual-array"></a>Clonar de um backup da Matriz Virtual StorSimple

## <a name="overview"></a>Visão geral

Este artigo descreve passo a passo como tooclone um conjunto de backup compartilhamentos ou volumes no Microsoft Azure StorSimple Virtual Array. backup clonado Olá é toorecover usado um arquivo excluído ou perdido. Olá também inclui etapas detalhadas tooperform que uma recuperação em nível de item no StorSimple Virtual Array é configurada como um servidor de arquivos.

## <a name="clone-shares-from-a-backup-set"></a>Clonar compartilhamentos de um conjunto de backup

**Antes de tentar tooclone compartilhamentos, certifique-se de que você tem espaço suficiente no hello dispositivo toocomplete esta operação.** tooclone de um backup, em Olá [portal do Azure](https://portal.azure.com/), executar Olá etapas a seguir.

#### <a name="tooclone-a-share"></a>tooclone um compartilhamento

1. Procurar muito**dispositivos** folha. Selecione e clique em seu dispositivo e em **Compartilhamentos**. Selecione Olá compartilhamento que você deseja tooclone, o menu de contexto do botão direito do mouse Olá compartilhamento tooinvoke hello. Selecione **Clonar**.
   
   ![Clonar um backup](./media/storsimple-virtual-array-clone/cloneshare1.png)
2. Em Olá **Clone** folha, clique em **Backup > selecione** e, em seguida, Olá a seguir: 
   
   a.    Filtre um backup no dispositivo com base no intervalo de tempo de saudação. Você pode escolher entre **Últimos 7 dias**, **Últimos 30 dias** e **Ano passado**.
   
   b.    Na lista de Olá dos backups filtrados exibida, selecione um backup tooclone do.
   
   c.    Clique em **OK**.
   
   ![Clonar um backup](./media/storsimple-virtual-array-clone/cloneshare3.png)
3. Em Olá **Clone** folha, clique em **configurações de destino** e, em seguida, Olá a seguir:
   
   a.    Forneça um nome do compartilhamento. nome do compartilhamento Olá deve conter 3 a 127 caracteres.
   
   b.    Opcionalmente, forneça uma descrição para o compartilhamento clonado hello.
   
   c.    Você não pode alterar o tipo de saudação do compartilhamento Olá que você está restaurando. Um compartilhamento em camadas é clonado como em camadas, e um compartilhamento fixado localmente é clonado como um compartilhamento fixado localmente.
   
   d.    capacidade de saudação é definida como igual toohello tamanho do compartilhamento de saudação de que são a clonagem.
   
   e.    Atribua administradores Olá para este compartilhamento. Será capaz de toomodify propriedades de compartilhamento Olá por meio do Explorador de arquivos após a conclusão da clonagem de saudação.
   
   f.    Clique em **OK**.
   
   ![Clonar um backup](./media/storsimple-virtual-array-clone/cloneshare6.png)

4. Clique em **Clone** toostart um trabalho de clone. Após a conclusão do trabalho hello, Olá clone operação inicia e você será notificado. progresso de saudação toomonitor de clone, vá toohello **trabalhos** folha e clique em Olá tooview trabalho detalhes do trabalho.
5. Depois que o clone Olá é criado com êxito, navegue toohello back **compartilhamentos** folha no seu dispositivo.
6. Agora você pode exibir o novo compartilhamento de clonado Olá na lista de saudação de compartilhamentos em seu dispositivo. Um compartilhamento em camadas é clonado como em camadas, e um compartilhamento fixado localmente é clonado como um compartilhamento fixado localmente.
   
   ![Clonar um backup](./media/storsimple-virtual-array-clone/cloneshare10.png)

## <a name="clone-volumes-from-a-backup-set"></a>Clonar volumes de um conjunto de backup

tooclone de um backup, em Olá portal do Azure, você tem toohello do tooperform etapas semelhantes ao clonar um compartilhamento. operação de clonagem Olá clones Olá tooa backup novo volume em Olá mesmo dispositivo virtual. não é possível clonar tooa outro dispositivo.

#### <a name="tooclone-a-volume"></a>tooclone um volume

1. Procurar muito**dispositivos** folha. Selecione e clique em seu dispositivo e em **Volumes**. Selecionar o volume Olá que você deseja tooclone, o menu de contexto do botão direito do mouse Olá volume tooinvoke hello. Selecione **Clonar**.
   
   ![Clonar um volume](./media/storsimple-virtual-array-clone/clonevolume1.png)
2. Em Olá **Clone** folha, clique em **Backup** e, em seguida, Olá a seguir: 
   
   a.    Filtre um backup no dispositivo com base no intervalo de tempo de saudação. Você pode escolher entre **Últimos 7 dias**, **Últimos 30 dias** e **Ano passado**. 
   
   b.    Na lista de Olá dos backups filtrados exibida, selecione um backup tooclone do.
   
   c.    Clique em **OK**.
   
   ![Clonar um backup](./media/storsimple-virtual-array-clone/clonevolume3.png)
3. Em Olá **Clone** folha, clique em **configurações de volume de destino** e, em seguida, Olá a seguir:
   
   a. nome do dispositivo Olá é preenchida automaticamente.
   
   b. Forneça um nome de volume para Olá **clonar volume**. nome do volume Olá deve conter 3 caracteres too127.
   
   c. o tipo de volume Olá é definido automaticamente o volume original toohello. Um volume em camadas é clonado como em camadas, e um volume fixado localmente é clonado como um volume fixado localmente.
   
   d. Para Olá **conectado hosts**, clique em **selecione**.
   
   ![Clonar um backup](./media/storsimple-virtual-array-clone/clonevolume4.png)
4. Em Olá **conectado hosts** folha, selecione um ACR existente ou adicionar um novo ACR. tooadd um novo ACR, será necessário tooprovide um nome ACR e o IQN de host hello. Clique em **Selecionar**.
   
   ![Clonar um backup](./media/storsimple-virtual-array-clone/clonevolume5.png)
5. Clique em **Clone** toolaunch um trabalho de clone.
   
   ![Clonar um backup](./media/storsimple-virtual-array-clone/clonevolume6.png)  
6. Depois que o trabalho de clone Olá é criado, a clonagem será iniciado. Depois de criar o clone hello, ele será exibido na folha de Volumes de saudação em seu dispositivo. Um volume em camadas é clonado como em camadas, e um volume fixado localmente é clonado como um volume fixado localmente.
   
   ![Clonar um backup](./media/storsimple-virtual-array-clone/clonevolume8.png)
7. Depois que o volume de saudação aparece online na lista de saudação de volumes, volume de saudação está disponível para uso. No host de iniciador iSCSI hello, atualize a lista de saudação de destinos na janela de propriedades do iniciador iSCSI. Um novo destino que contém o nome do volume clonado Olá deve aparecer como 'inactive' na coluna de status de saudação.
8. Selecione o destino de saudação e clique em **conectar**. Após o iniciador Olá destino toohello conectado, o status de Olá deve mudar muito**conectado**.
9. Em Olá **gerenciamento de disco** janela, hello volumes montados exibido conforme mostrado na ilustração a seguir de saudação. Com o botão direito volume Olá descoberto (clique em nome do disco Olá) e, em seguida, clique em **Online**.

> [!IMPORTANT]
> Quando tentar tooclone um volume ou um compartilhamento de um conjunto de backup, se ocorrer falha no trabalho de clone hello, um volume de destino ou compartilhamento ainda pode ser criado no portal de saudação. É importante que você excluir o volume de destino ou compartilhar em toominimize portal Olá problemas futuros decorrentes deste elemento.
> 
> 

## <a name="item-level-recovery-ilr"></a>ILR (recuperação em nível de item)

Esta versão apresenta a recuperação em nível de item (ILR) hello em uma matriz Virtual StorSimple configurado como um servidor de arquivos. Olá recurso permite que você toodo recuperação granular de arquivos e pastas de um backup na nuvem de todos os compartilhamentos de saudação no dispositivo do StorSimple hello. Você pode recuperar arquivos excluídos de backups recentes usando um modelo de autoatendimento.

Cada compartilhamento tem um *.backups* pasta que contém os backups mais recentes de saudação. Poderá navegar backup desejado toohello, copiar os arquivos relevantes e pastas de backup de hello e restaurá-los. Este recurso elimina tooadministrators chamadas para restauração de backups de arquivos.

1. Ao executar Olá ILR, você pode exibir backups Olá por meio do Gerenciador de arquivos. Clique em compartilhamento de saudação específico que você deseja toolook backup hello para. Você verá um *.backups* pasta criada no compartilhamento de saudação que armazena todos os backups de saudação. Expanda Olá *.backups* backups de saudação do tooview de pasta. pasta Olá mostra a exibição detalhada de saudação de toda a hierarquia backup hello. Este modo de exibição é criado sob demanda e normalmente leva apenas alguns segundos toocreate.
   
   backups de cinco últimas Olá são exibidos dessa forma e podem ser usado tooperform um nível de item de recuperação. Olá cinco backups recentes incluem Olá agendada padrão e Olá backups manuais.
   
   * **Backups agendados** nomeados como &lt;Device name&gt;DailySchedule-YYYYMMDD-HHMMSS-UTC.
   * **Backups manuais** nomeados como Ad-hoc-YYYYMMDD-HHMMSS-UTC.
     
     ![](./media/storsimple-virtual-array-clone/image14.png)

2. Identificar o backup de saudação que contém a versão mais recente de saudação do arquivo hello excluído. Embora o nome da pasta Olá contém um carimbo de hora UTC em cada saudação anterior casos, o tempo de saudação no qual Olá pasta foi criada é tempo de dispositivo real de hello quando hello backup foi iniciado. Use Olá pasta timestamp toolocate e identificar Olá backups.

3. Localize a pasta de hello ou arquivo hello que você deseja toorestore no backup Olá que você identificou na etapa anterior hello. Observe que você só pode exibir arquivos de saudação ou pastas que você tem permissões para. Se você não pode acessar determinados arquivos ou pastas, contate o administrador do compartilhamento. administrador Olá pode usar permissões de compartilhamento do Explorador de arquivos tooedit Olá e fornecer acesso toohello arquivo ou pasta específica. É uma prática recomendada que Olá administrador compartilhamento é um grupo de usuário em vez de um único usuário.

4. Copiar arquivo Olá Olá pasta toohello apropriado compartilhamento ou em seu servidor de arquivos do StorSimple.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre como muito[administrar sua matriz Virtual StorSimple usando a interface da web local Olá](storsimple-ova-web-ui-admin.md).

