---
title: "Olá aaaDeploy serviço StorSimple Manager | Microsoft Docs"
description: "Explica como toocreate e delete Olá o serviço StorSimple Manager Olá portal clássico do Azure e descreve como toomanage Olá a chave de registro de serviço."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: bc1d5650-275c-42ed-bc77-cdb596f85943
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f49b647d91b03bb89ebd0e5cce196e50e3c00296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-manager-service-in-hello-azure-classic-portal"></a>Implantar o serviço StorSimple Manager Olá no hello portal clássico do Azure

## <a name="overview"></a>Visão geral
Olá serviço StorSimple Manager é executado no Microsoft Azure e conecta dispositivos de StorSimple toomultiple. Depois de criar o serviço hello, você pode usar dispositivos toomanage Olá Olá Microsoft Azure clássico portal em execução em um navegador. Isso permite que você toomonitor todos os dispositivos de saudação que são conectado toohello Gerenciador do StorSimple do serviço de um único local central, minimizando a carga administrativa.

página de aterrissagem do StorSimple Manager Olá lista todos os serviços do StorSimple Manager Olá que você pode usar toomanage os dispositivos de armazenamento do StorSimple. Para cada serviço StorSimple Manager, Olá informações a seguir é apresentado na página do Gerenciador do StorSimple hello:

* **Nome** – nome hello que foi atribuído o serviço StorSimple Manager tooyour quando ele foi criado. **nome do serviço Olá não pode ser alterado depois que o serviço Olá é criado. Isso também é verdadeiro para outras entidades, como os dispositivos, volumes, contêineres de volume e políticas de backup que não podem ser renomeadas no hello portal clássico do Azure.**
* **Status** – Olá status do serviço de saudação, que pode ser **Active**, **criando**, ou **Online**.
* **Local** – Olá localização geográfica na qual Olá StorSimple dispositivo será implantado.
* **Assinatura** – hello cobrança de assinatura que está associada ao seu serviço.

Olá tarefas comuns que podem ser executadas por meio da página do Gerenciador do StorSimple Olá são:

* Criar um serviço
* Excluir um serviço
* Obter chave de registro de serviço Olá
* Regenerar chave de registro de serviço Olá

Este tutorial descreve como tooperform essas tarefas.

## <a name="create-a-service"></a>Criar um serviço
Saudação de uso **criação rápida** opção toocreate um serviço StorSimple Manager, se você quiser toodeploy seu dispositivo StorSimple. toocreate um serviço, é necessário toohave:

* Uma assinatura com um Enterprise Agreement
* Uma conta de armazenamento ativa do Microsoft Azure
* Olá informações de cobrança que são usadas para gerenciamento de acesso

Além disso, é possível toogenerate uma conta de armazenamento padrão ao criar serviço hello.

Um único serviço pode gerenciar vários dispositivos. No entanto, um dispositivo não pode abranger vários serviços. Uma grande empresa pode ter vários toowork de instâncias de serviço com diferentes assinaturas, organizações ou mesmo regiões de implantação. Observe que você precisa separar instâncias de dispositivos da série StorSimple 8000 StorSimple Manager serviço toomanage e matrizes de Virtual do StorSimple.

> [!IMPORTANT] 
> Se você tiver um serviço não utilizado criado (nenhum dispositivo operações foram realizadas nesse recurso) tooAugust anterior 2016, ele não pode ser gerenciado por meio do portal do Azure ou portal clássico do Azure. É recomendável que você crie um novo serviço em Olá portal do Azure.

Execute Olá etapas toocreate um serviço a seguir.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

## <a name="delete-a-service"></a>Excluir um serviço
Antes de excluir um serviço, verifique se nenhum dispositivo conectado está usando ele. Se o serviço de saudação está em uso, desative os dispositivos de saudação conectado. Olá desativar operação sever conexão Olá entre dispositivo hello e serviço hello, mas preservar os dados do dispositivo Olá na nuvem hello.

> [!IMPORTANT] 
> Depois que um serviço é excluído, operação Olá não pode ser revertida. Qualquer dispositivo que esteja usando o serviço de saudação precisará toobe antes que ele pode ser usado com outro serviço de redefinição de fábrica. Nesse cenário, os dados de locais de saudação em dispositivo hello, bem como configuração Olá, serão perdidas.

Execute Olá etapas toodelete um serviço a seguir.

### <a name="toodelete-a-service"></a>toodelete um serviço
1. Em Olá **o serviço StorSimple Manager** página serviço Olá selecione que você deseja toodelete.
2. Clique em **excluir** final Olá Olá página.
3. Clique em **Sim** na notificação de confirmação de saudação. Ele pode levar alguns minutos para Olá serviço toobe excluído.

## <a name="get-hello-service-registration-key"></a>Obter chave de registro de serviço Olá
Depois que você criou com êxito um serviço, você precisará tooregister seu dispositivo StorSimple com o serviço de saudação. tooregister seu dispositivo StorSimple primeiro, será necessário Olá o chave de registro de serviço. tooregister dispositivos adicionais com um serviço StorSimple existente, você precisará chave de registro hello e chave criptografia de dados de serviço de saudação (que é gerado no primeiro dispositivo de saudação durante o registro). Para obter mais informações sobre a chave de criptografia de dados de serviço hello, consulte [segurança de StorSimple](storsimple-security.md). Você pode obter a chave de registro Olá acessando **chave de registro** em Olá **serviços** página.

Execute Olá etapas tooget Olá chave de registro a seguir.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

Mantenha a chave de registro do serviço de saudação em um local seguro. Você precisará essa chave, bem como chave de criptografia de dados de serviço hello, tooregister de dispositivos adicionais com este serviço. Depois de obter a chave de registro de serviço hello, você precisará tooconfigure seu dispositivo por meio de saudação do Windows PowerShell para StorSimple interface.

Para obter detalhes sobre como toouse essa chave de registro, consulte [etapa 3: configurar e registrar o dispositivo Olá por meio do Windows PowerShell para StorSimple](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Regenerar chave de registro de serviço Olá
Se for necessário tooperform a rotação de chaves ou se a lista de saudação de administradores de serviço foi alterada, você precisará tooregenerate uma chave de registro de serviço. Quando você regenerar chave Olá, a nova chave de saudação é usado apenas para registrar dispositivos subsequentes. dispositivos de saudação que já foram registrados não são afetados por esse processo.

Execute Olá etapas tooregenerate uma chave de registro de serviço a seguir.

### <a name="tooregenerate-hello-service-registration-key"></a>chave de registro tooregenerate Olá
1. Em Olá **o serviço StorSimple Manager** , clique em **chave de registro**.
2. Em Olá **chave de registro** caixa de diálogo, clique em **regenerar**.
3. Você verá uma mensagem de confirmação. Clique em **Okey** toocontinue com regeneração hello.
4. Uma nova chave de registro de serviço será exibida.
5. Copie essa chave e salve-a para registrar todos os novos dispositivos nesse serviço.
6. Clique o ícone de verificação Olá ![Ícone de verificação](./media/storsimple-manage-service/HCS_CheckIcon.png) tooclose essa caixa de diálogo.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre Olá [o processo de implantação StorSimple](storsimple-deployment-walkthrough-u2.md).
* [Saiba mais sobre como gerenciar sua conta de armazenamento do StorSimple](storsimple-manage-storage-accounts.md).
* Saiba mais sobre como muito[use Olá tooadminister do serviço StorSimple Manager seu dispositivo StorSimple](storsimple-manager-service-administration.md).
