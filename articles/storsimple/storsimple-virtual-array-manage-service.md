---
title: "aaaDeploy serviço do Gerenciador de dispositivos de StorSimple | Microsoft Docs"
description: "Explica como toocreate e delete Olá serviço do Gerenciador de dispositivos do StorSimple no hello portal do Azure e descreve como toomanage Olá a chave de registro de serviço."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a>Implante o serviço de Gerenciador de dispositivos de StorSimple Olá para matriz Virtual StorSimple
## <a name="overview"></a>Visão geral

saudação de serviço do Gerenciador de dispositivos do StorSimple é executado no Microsoft Azure e conecta dispositivos de StorSimple toomultiple. Depois de criar o serviço hello, você pode usar dispositivos toomanage Olá Olá Microsoft Azure portal em execução em um navegador. Isso permite que você toomonitor todos os dispositivos de saudação que são conectado toohello Gerenciador de dispositivos do StorSimple do serviço de um único local central, minimizando a carga administrativa.

Olá comuns tarefas relacionadas tooa serviço do Gerenciador de dispositivos do StorSimple são:

* Criar um serviço
* Excluir um serviço
* Obter chave de registro de serviço Olá
* Regenerar chave de registro de serviço Olá

Este tutorial descreve como tooperform de Olá tarefas anteriores. informações de saudação contidas neste artigo são aplicável somente tooStorSimple Virtual matrizes. Para obter mais informações sobre o StorSimple série 8000, vá muito[implantar um serviço StorSimple Manager](storsimple-manage-service.md).

## <a name="create-a-service"></a>Criar um serviço

toocreate um serviço, é necessário toohave:

* Uma assinatura com um Enterprise Agreement
* Uma conta de armazenamento ativa do Microsoft Azure
* Olá informações de cobrança que são usadas para gerenciamento de acesso

Além disso, é possível toogenerate uma conta de armazenamento ao criar serviço hello.

Um único serviço pode gerenciar vários dispositivos. No entanto, um dispositivo não pode abranger vários serviços. Uma grande empresa pode ter vários toowork de instâncias de serviço com diferentes assinaturas, organizações ou mesmo regiões de implantação.

> [!NOTE]
> Você precisa de instâncias separadas de dispositivos da série StorSimple 8000 Gerenciador de dispositivos do StorSimple service toomanage e matrizes de Virtual do StorSimple.


Execute Olá etapas toocreate um serviço a seguir.

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a>Excluir um serviço

Antes de excluir um serviço, verifique se nenhum dispositivo conectado está usando ele. Se o serviço de saudação está em uso, desative os dispositivos de saudação conectado. Olá desativar operação sever conexão Olá entre dispositivo hello e serviço hello, mas preservar os dados do dispositivo Olá na nuvem hello.

> [!IMPORTANT]
> Depois que um serviço é excluído, operação Olá não pode ser revertida. Qualquer dispositivo que esteja usando o serviço de saudação precisará toobe antes que ele pode ser usado com outro serviço de redefinição de fábrica. Nesse cenário, os dados de locais de saudação em dispositivo hello, bem como configuração Olá, serão perdidas.
 

Execute Olá etapas toodelete um serviço a seguir.

#### <a name="toodelete-a-service"></a>toodelete um serviço

1. Vá muito**todos os recursos**. Pesquise por seu serviço Gerenciador de Dispositivo do StorSimple. Selecione o serviço de saudação que você deseja toodelete.
   
    ![Selecione o serviço toodelete](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. Vá tooyour tooensure de painel de controle de serviço não há nenhum dispositivo conectado toohello serviço. Se não houver nenhum dispositivo registrado com esse serviço, você também verá um efeito de toohello de mensagem de faixa. Clique em **Excluir**.
   
    ![Excluir serviço](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. Quando solicitado a confirmar, clique em **Sim** na notificação de confirmação de saudação. 
   
    ![Confirmar exclusão do serviço](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. Ele pode levar alguns minutos para Olá serviço toobe excluído. Depois de saudação serviço é excluído com êxito, você será notificado.
   
    ![Exclusão bem-sucedida do serviço](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

lista de saudação de serviços será atualizada.

 ![Lista de serviços atualizada](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a>Obter chave de registro de serviço Olá
Depois que você criou com êxito um serviço, você precisará tooregister seu dispositivo StorSimple com o serviço de saudação. tooregister seu dispositivo StorSimple primeiro, será necessário Olá o chave de registro de serviço. tooregister dispositivos adicionais com um serviço StorSimple existente, você precisará chave de registro hello e chave criptografia de dados de serviço de saudação (que é gerado no primeiro dispositivo de saudação durante o registro). Para obter mais informações sobre a chave de criptografia de dados de serviço hello, consulte [segurança de StorSimple](storsimple-security.md). Você pode obter a chave de registro Olá acessando Olá **chaves** folha do seu serviço.

Execute Olá etapas tooget Olá chave de registro a seguir.

#### <a name="tooget-hello-service-registration-key"></a>chave de registro tooget Olá
1. Em Olá **Gerenciador de dispositivos de StorSimple** folha, ir muito**gerenciamento &gt;**  **chaves**.
   
   ![Folha Chaves](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. Em Olá **chaves** folha, uma chave de registro de serviço aparece. Copiar a chave de registro de saudação usando o ícone para copiar hello. 

Mantenha a chave de registro do serviço de saudação em um local seguro. Você precisará essa chave, bem como chave de criptografia de dados de serviço hello, tooregister de dispositivos adicionais com este serviço. Depois de obter a chave de registro de serviço hello, você precisará tooconfigure seu dispositivo por meio de saudação do Windows PowerShell para StorSimple interface.

## <a name="regenerate-hello-service-registration-key"></a>Regenerar chave de registro de serviço Olá
Se for necessário tooperform a rotação de chaves ou se a lista de saudação de administradores de serviço foi alterada, você precisará tooregenerate uma chave de registro de serviço. Quando você regenerar chave Olá, a nova chave de saudação é usado apenas para registrar dispositivos subsequentes. dispositivos de saudação que já foram registrados não são afetados por esse processo.

Execute Olá etapas tooregenerate uma chave de registro de serviço a seguir.

#### <a name="tooregenerate-hello-service-registration-key"></a>chave de registro tooregenerate Olá
1. Em Olá **Gerenciador de dispositivos de StorSimple** folha, ir muito**gerenciamento &gt;**  **chaves**.
   
   ![Folha Chaves](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. Em Olá **chaves** folha, clique em **regenerar**.
   
   ![Clique em regenerar](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. Em Olá **regenerar chave de registro** folha, examine Olá necessária uma ação quando hello chaves são geradas novamente. Todos os dispositivos de saudação subsequentes que são registrados com este serviço usará a nova chave de registro hello. Clique em **regenerar** tooconfirm. Você será notificado depois Olá registro for concluído.
   
   ![Confirmar regeneração da chave](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. Uma nova chave de registro de serviço será exibida.
   
    ![Confirmar regeneração da chave](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   Copie essa chave e salve-a para registrar todos os novos dispositivos nesse serviço.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[começar](storsimple-virtual-array-deploy1-portal-prep.md) com uma matriz Virtual StorSimple.
* Saiba como muito[administrar seu dispositivo StorSimple](storsimple-ova-web-ui-admin.md).

