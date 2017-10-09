---
title: credenciais de conta de armazenamento de matriz Virtual StorSimple aaaManage | Microsoft Docs
description: "Explica como usar Olá tooadd de página Configurar do Gerenciador de dispositivos de StorSimple, editar, excluir ou chaves de segurança Olá Girar para credenciais de conta de armazenamento associadas Olá matriz Virtual StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 234bf8bb-d5fe-40be-9d25-721d7482bc3b
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.openlocfilehash: 22a0341eae0b89020065be4dbfaae77999f8be0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-storage-account-credentials-for-storsimple-virtual-array"></a>Use o Gerenciador de dispositivo StorSimple toomanage credenciais de conta de armazenamento para a matriz Virtual StorSimple

## <a name="overview"></a>Visão geral
Olá **configuração** seção da folha de serviço de Gerenciador de dispositivos de StorSimple Olá da sua matriz Virtual StorSimple apresenta os parâmetros de serviços globais de saudação que podem ser criados no hello serviço StorSimple Manager. Esses parâmetros podem ser tooall aplicados Olá dispositivos conectados toohello serviço e incluem:

* Credenciais da conta de armazenamento
* Registros de controle de acesso
  
  ![Painel do serviço Gerenciador de Dispositivos](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccts-dashboard.png)  

Este tutorial explica como você pode adicionar, editar ou excluir credenciais de conta de armazenamento para sua Matriz Virtual StorSimple. informações de saudação neste tutorial se aplica somente a toohello matriz Virtual StorSimple. Para obter informações sobre como contas de armazenamento toomanage em 8000 série, consulte [Use sua conta de armazenamento de toomanage do serviço StorSimple Manager Olá](storsimple-manage-storage-accounts.md).

Conta de armazenamento credenciais contém credenciais Olá Olá dispositivo usa tooaccess sua conta de armazenamento com seu provedor de serviços de nuvem. Para contas de armazenamento do Microsoft Azure, essas são as credenciais como nome da conta hello e chave de acesso primária hello.

Em Olá **credenciais da conta de armazenamento** folha, a conta de armazenamento de todas as credenciais que são criadas para Olá cobrança de assinatura são exibidas em um formato de tabela que contém a saudação informações a seguir:

* **Nome** – Olá nome exclusivo atribuído toohello conta quando ele foi criado.
* **SSL habilitado** – se hello SSL está habilitado e comunicação de dispositivo para a nuvem é pelo canal seguro hello.
  
  ![Seção de configuração](./media/storsimple-virtual-array-manage-storage-accounts/ova-storageaccountcredentials-blade.png)

tarefas mais comuns de saudação relacionadas toostorage credenciais da conta que podem ser executadas em Olá **credenciais da conta de armazenamento** folha são:

* Adicionar uma credencial de conta de armazenamento
* Editar uma credencial de conta de armazenamento
* Excluir uma credencial de conta de armazenamento

## <a name="types-of-storage-account-credentials"></a>Tipos de credenciais da conta de armazenamento
Há três tipos de credenciais de conta de armazenamento que podem ser usados com o dispositivo StorSimple.

* **Credenciais da conta de armazenamento gerada automaticamente** – como Olá nome sugere, esse tipo de credencial da conta de armazenamento é gerado automaticamente quando o serviço de saudação é criado pela primeira vez. toolearn mais sobre como esta credencial de conta de armazenamento é criada, consulte [criar um novo serviço](storsimple-virtual-array-manage-service.md#create-a-service).
* **credenciais de conta de armazenamento na assinatura do serviço Olá** – essas são contas de armazenamento do Azure Olá credenciais que estão associadas com Olá a mesma assinatura que o serviço de saudação. toolearn mais sobre como essas credenciais de conta de armazenamento são criados, consulte [sobre contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).
* **credenciais de conta de armazenamento fora da assinatura do serviço Olá** – são as credenciais de conta de armazenamento do Azure Olá que não estão associadas com o serviço e provavelmente Olá existente antes do serviço foi criado.

## <a name="add-a-storage-account-credential"></a>Adicionar uma credencial de conta de armazenamento
Você pode adicionar uma configuração de serviço do armazenamento conta credencial tooyour Gerenciador de dispositivos de StorSimple, fornecendo uma única as credenciais de acesso e do nome amigáveis que estão vinculadas toohello conta de armazenamento. Você também tem a opção de saudação da habilitação Olá seguro sockets layer (SSL) modo toocreate um canal seguro para comunicação de rede entre sua nuvem de dispositivo e hello.

Você pode criar várias contas para um provedor de serviços de nuvem específico. Enquanto a credencial da conta de armazenamento hello está sendo salvo, o serviço de saudação tenta toocommunicate com seu provedor de serviços de nuvem. Olá credenciais e material de acesso de saudação fornecidas são autenticadas no momento. Uma credencial de conta de armazenamento é criada somente se Olá autenticação for bem-sucedida. Se a autenticação de saudação falhar, uma mensagem de erro apropriada é exibida.

Saudação de usar credenciais de conta de armazenamento do Azure de tooadd procedimentos a seguir:

* tooadd uma credencial da conta de armazenamento tem Olá a mesma assinatura do Azure como serviço de Gerenciador de dispositivos Olá
* tooadd uma credencial de conta de armazenamento do Azure que está fora da assinatura do serviço de Gerenciador de dispositivos Olá

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>tooadd uma credencial da conta de armazenamento tem Olá a mesma assinatura do Azure como serviço de Gerenciador de dispositivos Olá

1. Navegue tooyour serviço do Gerenciador de dispositivos, selecione e clique duas vezes nele. Isso abre o hello **visão geral** folha.
2. Selecione **credenciais da conta de armazenamento** em Olá **configuração** seção.
3. Clique em **Adicionar**.
4. Em Olá **adicionar uma conta de armazenamento** folha, Olá a seguir:
   
    1. Para **Assinatura**, selecione **Atual**.
    2. Forneça o nome de saudação da sua conta de armazenamento do Azure.
    3. Selecione **habilitar** toocreate um canal seguro para comunicação de rede entre sua nuvem de dispositivo e hello StorSimple. Selecione **Desabilitar** somente se você estiver operando em uma nuvem privada.
    4. Clique em **Adicionar**. Você será notificado depois da conta de armazenamento Olá é criada com êxito.<br></br>
   
        ![Adicionar uma credencial de conta de armazenamento existente](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

#### <a name="tooadd-an-azure-storage-account-credential-that-is-outside-of-hello-device-manager-service-subscription"></a>tooadd uma credencial de conta de armazenamento do Azure que está fora da assinatura do serviço de Gerenciador de dispositivos Olá

1. Navegue tooyour serviço do Gerenciador de dispositivos, selecione e clique duas vezes nele. Isso abre o hello **visão geral** folha.
2. Selecione **credenciais da conta de armazenamento** em Olá **configuração** seção. Lista quaisquer credenciais de conta de armazenamento existente associadas a saudação de serviço do Gerenciador de dispositivos do StorSimple.
3. Clique em **Adicionar**.
4. Em Olá **adicionar uma conta de armazenamento** folha, Olá a seguir:
   
    1. Para **Assinatura**, selecione **Outras**.
   
    2. Forneça o nome de saudação de suas credenciais de conta de armazenamento do Azure.
   
    3. Em Olá **chave de acesso da conta de armazenamento** caixa de texto, fonte Olá chave de acesso primária para suas credenciais de conta de armazenamento do Azure. tooget esta tecla, vá toohello serviço de armazenamento do Azure, selecione suas credenciais de conta de armazenamento e clique em **gerenciar chaves de conta**. Agora você pode copiar a chave de acesso primária hello.
   
    4. tooenable SSL, clique em Olá **habilitar** botão toocreate um canal seguro para comunicação de rede entre sua nuvem de serviço e hello do Gerenciador de dispositivos do StorSimple. Clique em Olá **desabilitar** botão somente se você estiver operando em uma nuvem privada.
   
    5. Clique em **Adicionar**. Você será notificado depois de credencial da conta de armazenamento Olá é criado com êxito.

5. credencial da conta de armazenamento Olá recém-criado é exibido na folha de serviço de Gerenciador de dispositivos do StorSimple configurar Olá em **credenciais da conta de armazenamento**.
   
    ![Adicionar uma credencial de conta de armazenamento fora Olá assinatura de serviço do Gerenciador de dispositivos](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-outside-storageacct.png)

## <a name="edit-a-storage-account-credential"></a>Editar uma credencial de conta de armazenamento
Você pode editar uma credencial de conta de armazenamento usada pelo seu dispositivo. Se você editar uma credencial de conta de armazenamento que está atualmente em uso, Olá campos disponíveis toomodify são chave de acesso hello e modo SSL de saudação do credencial da conta de armazenamento hello. Você pode fornecer a nova chave de acesso de armazenamento hello ou modificar Olá **habilitar modo SSL** seleção e salvar as configurações de saudação atualizada.

#### <a name="tooedit-a-storage-account-credential"></a>tooedit uma credencial da conta de armazenamento
1. Navegue tooyour serviço do Gerenciador de dispositivos, selecione e clique duas vezes nele. Isso abre o hello **visão geral** folha.
2. Selecione **credenciais da conta de armazenamento** em Olá **configuração** seção. Lista quaisquer credenciais de conta de armazenamento existente associadas a saudação de serviço do Gerenciador de dispositivos do StorSimple.
3. Na lista tabular de saudação de credenciais de conta de armazenamento, selecione e clique duas vezes em que você deseja toomodify de conta de saudação.
4. Em credenciais da conta de armazenamento Olá **propriedades** folha, Olá a seguir:
   
   1. Se necessário, você pode modificar Olá **habilitar SSL** seleção de modo.
   2. Você pode escolher tooregenerate suas chaves de acesso de credencial de conta de armazenamento. Para obter mais informações, consulte [regenerar chaves de conta de armazenamento Olá](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys). Forneça a chave de credencial de conta de armazenamento novo de saudação. Para uma conta de armazenamento do Azure, isso é chave de acesso primária hello.
   3. Clique em **salvar** na parte superior de saudação do hello **propriedades** configurações de saudação toosave folha. Olá configurações são atualizadas em Olá **credenciais da conta de armazenamento** folha.
      
      ![Editar uma credencial de conta de armazenamento](./media/storsimple-virtual-array-manage-storage-accounts/ova-edit-storageacct.png)

## <a name="delete-a-storage-account-credential"></a>Excluir uma credencial de conta de armazenamento
> [!IMPORTANT]
> Você só poderá excluir uma credencial de conta de armazenamento se ela não estiver em uso. Se uma credencial de conta de armazenamento estiver em uso, você será notificado.
> 
> 

#### <a name="toodelete-a-storage-account-credential"></a>toodelete uma credencial da conta de armazenamento
1. Navegue tooyour serviço do Gerenciador de dispositivos, selecione e clique duas vezes nele. Isso abre o hello **visão geral** folha.
2. Selecione **credenciais da conta de armazenamento** em Olá **configuração** seção. Lista quaisquer credenciais de conta de armazenamento existente associadas a saudação de serviço do Gerenciador de dispositivos do StorSimple.
3. Na lista tabular de saudação de credenciais de conta de armazenamento, selecione e clique duas vezes em que você deseja toodelete de conta de saudação.
4. Em credenciais da conta de armazenamento Olá **propriedades** folha, Olá a seguir:
   
   1. Clique em **excluir** toodelete credenciais de saudação.
   2. Quando solicitado a confirmar, clique em **Sim** toocontinue com exclusão hello. listagem tabular Olá é atualizada tooreflect Olá alterações.
      
      ![Excluir uma credencial de conta de armazenamento](./media/storsimple-virtual-array-manage-storage-accounts/ova-del-storageacct.png)

## <a name="synchronizing-storage-account-credential-keys"></a>Sincronização de chaves de credenciais de conta de armazenamento
Por motivos de segurança, a rotação de chaves é normalmente um requisito em datacenters. Um administrador do Microsoft Azure pode gerar novamente ou alterar a chave primária ou secundária de saudação acessando diretamente a credencial da conta de armazenamento hello (via Olá serviço de armazenamento do Microsoft Azure). saudação de serviço do Gerenciador de dispositivos do StorSimple não vê essa alteração automaticamente.

serviço de Gerenciador de dispositivos de StorSimple tooinform Olá de alteração hello, você precisa de serviço de Gerenciador de dispositivos do StorSimple do tooaccess Olá, acessar o armazenamento Olá credencial da conta e, em seguida, sincronizar a chave primária ou secundária hello (dependendo de qual delas foi alterada). serviço Hello, em seguida, obtém a chave mais recente hello, criptografa Olá chaves e envia Olá criptografado toohello chave dispositivo.

#### <a name="toosynchronize-keys-for-storage-account-credentials-in-hello-same-subscription-as-hello-service-azure-only"></a>toosynchronize chaves para as credenciais de conta de armazenamento em Olá a mesma assinatura que o serviço de saudação (somente no Azure)
1. Na folha de aterrissagem do serviço hello, selecione o seu serviço, clique duas vezes Olá nome do serviço e, em seguida, em Olá **configuração** seção, clique em **credenciais da conta de armazenamento**.
2. Em Olá **credenciais da conta de armazenamento** folha, na lista de saudação de credenciais de conta de armazenamento, selecione credencial da conta de armazenamento Olá cujas chaves que você deseja toosynchronize.
3. Em Olá **propriedades** folha para Olá selecionada credencial da conta de armazenamento, Olá a seguir:
   
    1. Clique em **Mais** e então clique em **Sincronizar chave de acesso**.
   
    2. Quando solicitado a confirmar, clique em **sincronizar chave** toocomplete sincronização de saudação.
    
4. Olá serviço do Gerenciador de dispositivos de StorSimple, é necessário chave Olá tooupdate anteriormente foi alterado no hello serviço de armazenamento do Microsoft Azure. Em Olá **chave de conta de armazenamento sincronizar** folha, se a chave de acesso primária Olá foi alterada (regenerada), clique em primária e, em seguida, clique em **sincronizar chave**. Se a chave secundária Olá foi alterada, clique em **secundário**e, em seguida, clique em **sincronizar chave**.
   
    ![Sincronizar chave de acesso](./media/storsimple-virtual-array-manage-storage-accounts/ova-sync-acess-key.png)

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[administrar sua matriz Virtual StorSimple](storsimple-ova-web-ui-admin.md).

