---
title: registros de controle de acesso aaaManage em StorSimple | Microsoft Docs
description: Descreve como os registros de controle de acesso de toouse toodetermine (ACRs) quais hosts podem se conectar a tooa volume no dispositivo do StorSimple hello.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Use os registros de controle de acesso do hello StorSimple Manager serviço toomanage

## <a name="overview"></a>Visão geral
Registros de controle de acesso (ACRs) permitem que você toospecify quais hosts podem se conectar a tooa volume no dispositivo do StorSimple hello. ACRs são definidos volume específico tooa e conter Olá iSCSI nomes qualificados (IQNs) de hosts de saudação. Quando um host tenta tooconnect tooa volume, o dispositivo Olá verifica Olá que ACR associado a esse volume do nome IQN do hello e se houver uma correspondência, hello conexão é estabelecida. Olá registros de controle de acesso no hello **configuração** seção da sua folha de serviço do Gerenciador de dispositivos do StorSimple exibir todos os registros de controle de acesso de saudação com hello correspondentes IQNs dos hosts de saudação.

Este tutorial explica Olá tarefas comuns relacionadas a ACR a seguir:

* Adicionar um registro de controle de acesso
* Editar um registro de controle de acesso
* Excluir um registro de controle de acesso

> [!IMPORTANT]
> * Ao atribuir um volume de tooa ACR, lembre-se que Olá volume não é acessado simultaneamente por mais de um host não clusterizado porque isso pode corromper o volume de saudação.
> * Ao excluir um ACR do volume, certifique-se de que host Olá correspondente não está acessando o volume Olá porque Olá exclusão pode levar a uma interrupção de leitura / gravação.

## <a name="get-hello-iqn"></a>Obter Olá IQN

Execute Olá seguindo as etapas tooget Olá IQN de um host do Windows que está executando o Windows Server 2012.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a>Adicionar um registro de controle de acesso
Use Olá **configuração** seção Olá Gerenciador de dispositivos do StorSimple serviço folha tooadd ACRs. Normalmente, você associará um ACR a um volume.

Execute Olá etapas tooadd um ACR a seguir.

#### <a name="tooadd-an-acr"></a>tooadd um ACR

1. Serviço de Gerenciador de dispositivos de StorSimple tooyour go, clique duas vezes Olá nome do serviço e, em seguida, dentro de saudação **configuração** seção, clique em **registros de controle de acesso**.
2. Em Olá **registros de controle de acesso** folha, clique em **+ adicionar ACR**.

    ![Clique em Adicionar ACR](./media/storsimple-8000-manage-acrs/createacr1.png)

3. Em Olá **adicionar ACR** folha, Olá seguintes etapas:

    1. Informe um nome para o ACR.
    
    2. Forneça o nome IQN de saudação do host do Windows Server em **iSCSI Initiator IQN (nome)**.

    3. Clique em **adicionar** toocreate Olá ACR.

        ![Clique em Adicionar ACR](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  Olá recém-adicionado que exibirá ACR na listagem tabular de saudação de ACRs.

    ![Clique em Adicionar ACR](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a>Editar um registro de controle de acesso
Use Olá **configuração** seção Olá Gerenciador de dispositivos do StorSimple serviço folha tooedit ACRs.

> [!NOTE]
> É recomendável modificar somente os ACRs que não estão em uso no momento. tooedit que um ACR associado a um volume que está em uso no momento, você deve primeiro colocar Olá volume offline.

Execute Olá etapas tooedit um ACR a seguir.

#### <a name="tooedit-an-access-control-record"></a>tooedit um registro de controle de acesso
1.  Serviço de Gerenciador de dispositivos de StorSimple tooyour go, clique duas vezes Olá nome do serviço e, em seguida, dentro de saudação **configuração** seção, clique em **registros de controle de acesso**.

    ![Vá tooaccess registros de controle](./media/storsimple-8000-manage-acrs/createacr1.png)

2. Na listagem tabular de saudação de registros de controle de acesso de saudação, clique em e selecione Olá ACR que quiser toomodify.

    ![Editar os registros de controle de acesso](./media/storsimple-8000-manage-acrs/editacr1.png)

3. Em Olá **editar registro de controle de acesso** folha, fornecer um diferentes IQN correspondente tooanother host.

    ![Editar os registros de controle de acesso](./media/storsimple-8000-manage-acrs/editacr2.png)

4. Clique em **Salvar**. Quando solicitado a confirmar, clique em **Sim**. 

    ![Editar os registros de controle de acesso](./media/storsimple-8000-manage-acrs/editacr3.png)

5. Você será notificado quando Olá ACR é atualizado. listagem tabular Olá também atualiza a alteração de saudação tooreflect.

   
## <a name="delete-an-access-control-record"></a>Excluir um registro de controle de acesso
Use Olá **configuração** seção Olá Gerenciador de dispositivos do StorSimple serviço folha toodelete ACRs.

> [!NOTE]
> Você pode excluir somente os ACRs que não estejam em uso no momento. toodelete que um ACR associado a um volume que está em uso no momento, você deve primeiro colocar Olá volume offline.

Execute Olá seguindo as etapas toodelete um registro de controle de acesso.

#### <a name="toodelete-an-access-control-record"></a>toodelete um registro de controle de acesso
1.  Serviço de Gerenciador de dispositivos de StorSimple tooyour go, clique duas vezes Olá nome do serviço e, em seguida, dentro de saudação **configuração** seção, clique em **registros de controle de acesso**.

    ![Vá tooaccess registros de controle](./media/storsimple-8000-manage-acrs/createacr1.png)

2. Na listagem tabular de saudação de registros de controle de acesso de saudação, clique em e selecione Olá ACR que quiser toodelete.

    ![Vá tooaccess registros de controle](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. Menu de contexto tooinvoke hello e selecione **excluir**.

    ![Vá tooaccess registros de controle](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. Quando solicitada a confirmação, examine as informações de saudação e, em seguida, clique em **excluir**.

    ![Vá tooaccess registros de controle](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. Você será notificado quando a exclusão de saudação é concluída. listagem tabular Olá é atualizada tooreflect Olá exclusão.

    ![Vá tooaccess registros de controle](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [como gerenciar volumes do StorSimple](storsimple-8000-manage-volumes-u2.md).
* Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

