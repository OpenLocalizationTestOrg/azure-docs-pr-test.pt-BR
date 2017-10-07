---
title: aaaManage registros de controle de acesso de matriz Virtual StorSimple | Microsoft Docs
description: "Descreve como os registros de controle de acesso de toomanage toodetermine (ACRs) quais hosts podem se conectar a tooa volume Olá matriz Virtual StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a>Use o Gerenciador de dispositivo StorSimple toomanage registros de controle de acesso de matriz Virtual StorSimple

## <a name="overview"></a>Visão geral

Registros de controle de acesso (ACRs) permitem que você toospecify quais hosts podem se conectar a tooa volume Olá StorSimple Virtual Array (também conhecido como Olá StorSimple no dispositivo virtual local). ACRs são definidos volume específico tooa e conter Olá iSCSI nomes qualificados (IQNs) de hosts de saudação. Quando um host tenta tooconnect tooa volume, dispositivo Olá verifica Olá ACR associado a esse volume do nome IQN do hello, e se houver uma correspondência, conexão Olá é estabelecida. Olá **registros de controle de acesso** folha em Olá **configuração** seção do seu serviço de Gerenciador de dispositivos exibe todos os registros de controle de acesso de saudação com hello correspondentes IQNs dos hosts de saudação.

![Gerenciar registros de controle de acesso](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

Este tutorial explica Olá tarefas comuns relacionadas a ACR a seguir:

* Obter Olá IQN
* Adicionar um registro de controle de acesso
* Editar um registro de controle de acesso
* Excluir um registro de controle de acesso

> [!IMPORTANT]
> 
> * Ao atribuir um volume de tooa ACR, lembre-se que Olá volume não é acessado simultaneamente por mais de um host não clusterizado porque isso pode corromper o volume de saudação.
> * Ao excluir um ACR do volume, certifique-se de que host Olá correspondente não está acessando o volume Olá porque Olá exclusão pode levar a uma interrupção de leitura / gravação.


## <a name="get-hello-iqn"></a>Obter Olá IQN

Execute Olá seguindo as etapas tooget Olá IQN de um host do Windows que está executando o Windows Server 2012.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a>Adicionar um ACR

Você usa **registros de controle de acesso** folha em Olá **configuração** seção do seu serviço de Gerenciador de dispositivos de StorSimple tooadd ACRs. Normalmente, você associa um ACR a um volume.

Para obter informações sobre como associar um ACR um volume, vá muito[adicionar um volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).

> [!IMPORTANT]
> Ao atribuir um volume de tooa ACR, lembre-se que Olá volume não é acessado simultaneamente por mais de um host não clusterizado porque isso pode corromper o volume de saudação.


Execute Olá etapas tooadd um ACR a seguir.

#### <a name="tooadd-an-acr"></a>tooadd um ACR

1. Na página de aterrissagem do serviço hello, selecione o seu serviço, clique duas vezes Olá nome do serviço e, em seguida, dentro de saudação **configuração** seção, clique em **registros de controle de acesso**.
2. Em Olá **registros de controle de acesso** folha, clique em **adicionar**.
3. Em Olá **adicionar ACR** folha, Olá a seguir:
   
    1. Dê um **Nome** para o seu ACR.
    
    2. Em **nome do iniciador iSCSI**, forneça o nome IQN de saudação do seu host do Windows. Olá tooget IQN do host do Windows Server, Olá a seguir:
   
    3. Inicie o iniciador iSCSI da Microsoft hello no seu host do Windows. Na janela de propriedades do iniciador iSCSI hello, em Olá **configuração** , selecione e copie a cadeia de caracteres de saudação do hello **nome do iniciador** campo.
    Cole essa cadeia de caracteres hello **IQN** campo Olá **adicionar ACR** folha.
   
    6. Clique em **adicionar** tooadd Olá ACR.  
   
        ![Adicionar registros de controle de acesso](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. Olá listagem tabular é atualizada tooreflect esta adição.

## <a name="edit-an-acr"></a>Editar um ACR

Use Olá **registros de controle de acesso** folha em Olá **configuração** seção do seu serviço de Gerenciador de dispositivos no hello ACRs tooedit portal do Azure.

> [!NOTE]
> Não modifique um ACR em uso no momento. tooedit que um ACR associado a um volume que está em uso no momento, você deve primeiro colocar Olá volume offline.


Execute Olá etapas tooedit um ACR a seguir.

#### <a name="tooedit-an-acr"></a>tooedit um ACR

1. Na página de aterrissagem do serviço hello, selecione o seu serviço, clique duas vezes Olá nome do serviço e, em seguida, dentro de saudação **configuração** seção, **registros de controle de acesso**.
2. Em Olá **registros de controle de acesso** folha da listagem de saudação tabular dos registros de controle de acesso Olá, clique duas vezes em Olá ACR que quiser toomodify.
3. Em Olá **editar registros de controle de acesso** folha, Olá a seguir:
   
    1. Fornece hello IQN para Olá ACR.
   
    2. Clique em **salvar** na parte superior de saudação do hello folha toosave Olá modificar ACR. Você verá Olá a seguinte mensagem de confirmação:
   
        ![Editar os registros de controle de acesso](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a>Excluir um registro de controle de acesso

Use Olá **configuração** página Olá ACRs toodelete portal do Azure.

> [!NOTE]
> 
> * Não exclua um ACR em uso no momento. toodelete que um ACR associado a um volume que está em uso no momento, você deve primeiro colocar Olá volume offline.
> * Ao excluir um ACR do volume, certifique-se de que host Olá correspondente não está acessando o volume Olá porque Olá exclusão pode levar a uma interrupção de leitura / gravação.


Execute Olá seguindo as etapas toodelete um registro de controle de acesso.

#### <a name="toodelete-an-access-control-record"></a>toodelete um registro de controle de acesso

1. Na página de aterrissagem do serviço hello, selecione o seu serviço, clique duas vezes Olá nome do serviço e, em seguida, dentro de saudação **configuração** seção, **registros de controle de acesso**.

2. Em Olá **registros de controle de acesso** folha da listagem de saudação tabular dos registros de controle de acesso Olá, clique duas vezes em Olá ACR que quiser toodelete.

3. Na folha de registros do controle de acesso de edição hello, clique em **excluir**.
   
    ![Excluir ACRS](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. Quando solicitado a confirmar, clique em **excluir** toocontinue com exclusão hello. listagem tabular Olá é atualizada tooreflect Olá exclusão.
   
   ![Mensagem de aviso](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a>Próximas etapas

* Saiba mais sobre [Adicionar volumes e configurar ACRs](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).

