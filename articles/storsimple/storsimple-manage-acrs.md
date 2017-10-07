---
title: registros de controle de acesso aaaManage em StorSimple | Microsoft Docs
description: Descreve como os registros de controle de acesso de toouse toodetermine (ACRs) quais hosts podem se conectar a tooa volume no dispositivo do StorSimple hello.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Use os registros de controle de acesso do hello StorSimple Manager serviço toomanage
## <a name="overview"></a>Visão geral
Registros de controle de acesso (ACRs) permitem que você toospecify quais hosts podem se conectar a tooa volume no dispositivo do StorSimple hello. ACRs são definidos volume específico tooa e conter Olá iSCSI nomes qualificados (IQNs) de hosts de saudação. Quando um host tenta tooconnect tooa volume, o dispositivo Olá verifica Olá que ACR associado a esse volume do nome IQN do hello e se houver uma correspondência, hello conexão é estabelecida. registros de controle de acesso de saudação seção Olá **configurar** página exibe todos os registros de controle de acesso de saudação com hello correspondentes IQNs dos hosts de saudação.

Este tutorial explica Olá tarefas comuns relacionadas a ACR a seguir:

* Adicionar um registro de controle de acesso 
* Editar um registro de controle de acesso 
* Excluir um registro de controle de acesso 

> [!IMPORTANT]
> * Ao atribuir um volume de tooa ACR, lembre-se que Olá volume não é acessado simultaneamente por mais de um host não clusterizado porque isso pode corromper o volume de saudação. 
> * Ao excluir um ACR do volume, certifique-se de que host Olá correspondente não está acessando o volume Olá porque Olá exclusão pode levar a uma interrupção de leitura / gravação.
> 
> 

## <a name="add-an-access-control-record"></a>Adicionar um registro de controle de acesso
Usar o serviço StorSimple Manager Olá **configurar** página ACRs tooadd. Normalmente, você associará um ACR a um volume.

Execute Olá etapas tooadd um ACR a seguir.

#### <a name="tooadd-an-access-control-record"></a>tooadd um registro de controle de acesso
1. Na página de aterrissagem do serviço hello, selecione o seu serviço, clique duas vezes no nome do serviço hello e clique em Olá **configurar** guia.
2. Em Olá tabela listando em **registros de controle de acesso**, forneça um **nome** para seu ACR.
3. Forneça o nome IQN de saudação do seu host do Windows em **nome do iniciador iSCSI**. Olá tooget IQN do host do Windows Server, Olá a seguir:
   
   * Inicie o iniciador iSCSI da Microsoft hello no seu host do Windows.
   * Em Olá **propriedades do iniciador iSCSI** janela Olá **configuração** , selecione e copie a cadeia de caracteres de saudação do hello **nome do iniciador** campo.
   * Cole essa cadeia de caracteres hello **nome do iniciador iSCSI** campo tabela ACRs Olá Olá portal clássico do Azure.
4. Clique em **salvar** toosave Olá recém-criado ACR. Olá tabela listando será atualizado tooreflect de ser essa adição.

## <a name="edit-an-access-control-record"></a>Editar um registro de controle de acesso
Use Olá **configurar** página Olá ACRs tooedit de portal clássico do Azure. 

> [!NOTE]
> Você pode modificar somente os ACRs que não estejam em uso no momento. tooedit que um ACR associado a um volume que está em uso no momento, você deve primeiro colocar Olá volume offline.
> 
> 

Execute Olá etapas tooedit um ACR a seguir.

#### <a name="tooedit-an-access-control-record"></a>tooedit um registro de controle de acesso
1. Na página de aterrissagem do serviço hello, selecione o seu serviço, clique duas vezes no nome do serviço hello e clique em Olá **configurar** guia.
2. Na listagem tabular de saudação de registros de controle de acesso de saudação, passe o mouse sobre Olá ACR que quiser toomodify.
3. Fornece um novo nome e/ou o IQN de saudação ACR.
4. Clique em **salvar** toosave Olá modificar ACR. Olá tabela listando será atualizado tooreflect de ser essa alteração.

## <a name="delete-an-access-control-record"></a>Excluir um registro de controle de acesso
Use Olá **configurar** página Olá ACRs toodelete de portal clássico do Azure. 

> [!NOTE]
> Você pode excluir somente os ACRs que não estejam em uso no momento. toodelete que um ACR associado a um volume que está em uso no momento, você deve primeiro colocar Olá volume offline.
> 
> 

Execute Olá seguindo as etapas toodelete um registro de controle de acesso.

#### <a name="toodelete-an-access-control-record"></a>toodelete um registro de controle de acesso
1. Na página de aterrissagem do serviço hello, selecione o seu serviço, clique duas vezes no nome do serviço hello e clique em Olá **configurar** guia.
2. Na listagem tabular de saudação de registros de controle de acesso (ACRs) hello, passe o mouse sobre Olá ACR que quiser toodelete.
3. Um ícone de exclusão (**x**) aparecerá na coluna de direito extremo Olá para Olá ACR selecionado. Clique em Olá **x** Olá toodelete de ícone ACR.
4. Quando solicitado a confirmar, clique em **Sim** toocontinue com exclusão hello. listagem tabular Olá será atualizado tooreflect Olá exclusão.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre [como gerenciar volumes do StorSimple](storsimple-manage-volumes.md).
* Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-manager-service-administration.md).

