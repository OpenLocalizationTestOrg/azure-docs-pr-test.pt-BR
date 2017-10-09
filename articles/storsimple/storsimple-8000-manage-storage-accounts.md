---
title: "aaaManage credenciais de sua conta de armazenamento do StorSimple para dispositivos da série StorSimple 8000 do Microsoft Azure | Microsoft Docs"
description: "Explica como você pode usar o hello tooadd de página Configurar do Gerenciador de dispositivos de StorSimple, editar, excluir ou chaves de segurança Olá Girar para uma conta de armazenamento."
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: 132ee46509b39db4d1b97b0f1077800a253e8da9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-storage-account-credentials"></a>Usar toomanage de serviço do Gerenciador de dispositivos de StorSimple Olá suas credenciais de conta de armazenamento

## <a name="overview"></a>Visão geral

Olá **configuração** seção na folha de serviço do Gerenciador de dispositivos de StorSimple Olá apresenta todos os parâmetros de serviços globais de saudação que podem ser criados no hello serviço do Gerenciador de dispositivos do StorSimple. Esses parâmetros podem ser tooall aplicados Olá dispositivos conectados toohello serviço e incluem:

* Credenciais da conta de armazenamento
* Modelos de largura de banda 
* Registros de controle de acesso 

Este tutorial explica como tooadd, editar ou excluir as credenciais de conta de armazenamento ou rotação de chaves de segurança Olá para uma conta de armazenamento.

 ![Lista de credenciais de conta de armazenamento](./media/storsimple-8000-manage-storage-accounts/createnewstorageacct6.png)  

Contas de armazenamento contêm as credenciais de Olá Olá tooaccess do StorSimple dispositivo usa sua conta de armazenamento com seu provedor de serviços de nuvem. Para contas de armazenamento do Microsoft Azure, essas são as credenciais como nome da conta hello e chave de acesso primária hello. 

Em Olá **credenciais da conta de armazenamento** folha, armazenamento de todas as contas que são criadas para Olá cobrança de assinatura são exibidas em um formato de tabela que contém a saudação informações a seguir:

* **Nome** – Olá nome exclusivo atribuído toohello conta quando ele foi criado.
* **SSL habilitado** – se hello SSL está habilitado e comunicação de dispositivo para a nuvem é pelo canal seguro hello.
* **Usado por** – Olá número de volumes usando a conta de armazenamento hello.

Olá mais comuns tarefas relacionadas toostorage contas que podem ser realizadas são:

* Adicionar uma conta de armazenamento 
* Editar uma conta de armazenamento 
* Excluir uma conta de armazenamento 
* Rotação de chave de contas de armazenamento 

## <a name="types-of-storage-accounts"></a>Tipos de contas de armazenamento

Há três tipos de contas de armazenamento que podem ser usadas com o dispositivo StorSimple.

* **Contas de armazenamento gerada automaticamente** – como Olá nome sugere, esse tipo de conta de armazenamento é gerado automaticamente quando o serviço de saudação é criado pela primeira vez. toolearn mais sobre como a conta de armazenamento é criada, consulte [etapa 1: criar um novo serviço](storsimple-8000-deployment-walkthrough-u2.md#step-1-create-a-new-service) na [implantar seu dispositivo do StorSimple local](storsimple-8000-deployment-walkthrough-u2.md). 
* **Contas de armazenamento na assinatura do serviço Olá** – essas são contas de armazenamento do Azure Olá que estão associadas a saudação mesma assinatura que o serviço de saudação. toolearn mais sobre como essas contas de armazenamento são criadas, consulte [sobre contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md). 
* **Contas de armazenamento fora da assinatura do serviço Olá** – essas são contas de armazenamento do Azure Olá que não estão associadas com o serviço e provavelmente Olá existente antes do serviço foi criado.

## <a name="add-a-storage-account"></a>Adicionar uma conta de armazenamento

Você pode adicionar uma conta de armazenamento, fornecendo uma única as credenciais de acesso e do nome amigáveis que estão vinculadas toohello conta de armazenamento (com o provedor de serviços de nuvem especificado Olá). Você também tem a opção de saudação da habilitação Olá seguro sockets layer (SSL) modo toocreate um canal seguro para comunicação de rede entre sua nuvem de dispositivo e hello.

Você pode criar várias contas para um provedor de serviços de nuvem específico. Lembre-se, no entanto, depois que uma conta de armazenamento é criada, você não pode alterar o provedor de serviços de nuvem hello.

Enquanto a conta de armazenamento hello está sendo salvo, o serviço de saudação tenta toocommunicate com seu provedor de serviços de nuvem. Olá credenciais e material de acesso de saudação que você forneceu serão autenticados neste momento. Uma conta de armazenamento é criada somente se Olá autenticação for bem-sucedida. Se a autenticação de saudação falhar, uma mensagem de erro apropriado será exibida.

Saudação de usar credenciais de conta de armazenamento do Azure de tooadd procedimentos a seguir:

* tooadd uma credencial da conta de armazenamento tem Olá a mesma assinatura do Azure como serviço de Gerenciador de dispositivos Olá
* tooadd uma credencial de conta de armazenamento do Azure que está fora da assinatura do serviço de Gerenciador de dispositivos Olá

[!INCLUDE [add-a-storage-account-update2](../../includes/storsimple-8000-configure-new-storage-account-u2.md)]

#### <a name="tooadd-an-azure-storage-account-credential-outside-of-hello-storsimple-device-manager-service-subscription"></a>tooadd uma credencial de conta de armazenamento do Azure fora de assinatura do serviço de Gerenciador de dispositivos de StorSimple Olá

1. Navegue tooyour serviço do Gerenciador de dispositivos de StorSimple, selecione e clique duas vezes nele. Isso abre o hello **visão geral** folha.
2. Selecione **credenciais da conta de armazenamento** em Olá **configuração** seção. Lista quaisquer credenciais de conta de armazenamento existente associadas a saudação de serviço do Gerenciador de dispositivos do StorSimple.
3. Clique em **Adicionar**.
4. Em Olá **adicionar uma credencial de conta de armazenamento** folha, Olá a seguir:
   
    1. Para **Assinatura**, selecione **Outras**.
   
    2. Forneça o nome de saudação de suas credenciais de conta de armazenamento do Azure.
   
    3. Em Olá **chave de acesso da conta de armazenamento** caixa de texto, fonte Olá chave de acesso primária para suas credenciais de conta de armazenamento do Azure. tooget esta tecla, vá toohello serviço de armazenamento do Azure, selecione suas credenciais de conta de armazenamento e clique em **gerenciar chaves de conta**. Agora você pode copiar a chave de acesso primária hello.
   
    4. tooenable SSL, clique em Olá **habilitar** botão toocreate um canal seguro para comunicação de rede entre sua nuvem de serviço e hello do Gerenciador de dispositivos do StorSimple. Clique em Olá **desabilitar** botão somente se você estiver operando em uma nuvem privada.
   
    5. Clique em **Adicionar**. Você será notificado depois de credencial da conta de armazenamento Olá é criado com êxito.

5. credencial da conta de armazenamento Olá recém-criado é exibido na folha de serviço de Gerenciador de dispositivos do StorSimple configurar Olá em **credenciais da conta de armazenamento**.
   


## <a name="edit-a-storage-account"></a>Editar uma conta de armazenamento

Você pode editar uma conta de armazenamento usada por um contêiner de volume. Se você editar uma conta de armazenamento que está atualmente em uso, hello somente campo toomodify disponível é Olá chave de acesso para a conta de armazenamento hello. Você pode fornecer a nova chave de acesso de armazenamento hello e salvar as configurações de saudação atualizada.

#### <a name="tooedit-a-storage-account"></a>tooedit uma conta de armazenamento

1. Acesse o serviço de Gerenciador de dispositivos de StorSimple tooyour. Em Olá **configuração** seção, clique em **credenciais da conta de armazenamento**.

    ![Credenciais da conta de armazenamento](./media/storsimple-8000-manage-storage-accounts/editstorageacct1.png)

2. Em Olá **credenciais da conta de armazenamento** folha, na lista de saudação de credenciais de conta de armazenamento, selecionadas e clique Olá um desejar tooedit. 

3. Você pode modificar Olá **habilitar SSL** seleção. Você também pode clicar em **mais...**  e, em seguida, selecione **toorotate chave de acesso de sincronização** suas chaves de acesso da conta de armazenamento. Vá muito[rotação de contas de armazenamento de chaves](#key-rotation-of-storage-accounts) para obter mais informações sobre como tooperform rotação de chaves. Depois que você modificou as configurações de saudação, clique em **salvar**. 

    ![Salvar as credenciais editadas da conta de armazenamento](./media/storsimple-8000-manage-storage-accounts/editstorageacct3.png)

4. Quando solicitado a confirmar, clique em **Sim**. 

    ![Confirmar modificações](./media/storsimple-8000-manage-storage-accounts/editstorageacct4.png)

configurações de saudação serão atualizadas e salvo para sua conta de armazenamento. 

## <a name="delete-a-storage-account"></a>Excluir uma conta de armazenamento

> [!IMPORTANT]
> Você pode excluir uma conta de armazenamento somente se ela não for usada por um contêiner de volume. Se uma conta de armazenamento está sendo usada por um contêiner de volume, primeiro excluir o contêiner de volume hello e, em seguida, excluir conta de armazenamento Olá associado.

#### <a name="toodelete-a-storage-account"></a>toodelete uma conta de armazenamento

1. Acesse o serviço de Gerenciador de dispositivos de StorSimple tooyour. Em Olá **configuração** seção, clique em **credenciais da conta de armazenamento**.

2. Na lista tabular de saudação de contas de armazenamento, passe o mouse sobre a conta de saudação que você deseja toodelete. Menu de contexto de saudação tooinvoke de atalho e clique em **excluir**.

    ![Excluir as credenciais da conta de armazenamento](./media/storsimple-8000-manage-storage-accounts/deletestorageacct1.png)

3. Quando solicitado a confirmar, clique em **Sim** toocontinue com exclusão hello. listagem tabular Olá será atualizado tooreflect Olá alterações.

    ![Confirmar exclusão](./media/storsimple-8000-manage-storage-accounts/deletestorageacct2.png)

## <a name="key-rotation-of-storage-accounts"></a>Rotação de chave de contas de armazenamento

Por motivos de segurança, a rotação de chaves é normalmente um requisito em datacenters. Cada assinatura do Microsoft Azure pode ter uma ou mais contas de armazenamento associadas. contas de toothese Olá acesso é controlado pela assinatura hello e chaves de acesso para cada conta de armazenamento. 

Quando você cria uma conta de armazenamento, o Microsoft Azure gera duas chaves de acesso de armazenamento de 512 bits são usadas para autenticação quando a conta de armazenamento Olá é acessada. Ter duas chaves de acesso de armazenamento permite que você tooregenerate Olá chaves sem interrupção tooyour storage Service, serviço ou toothat o serviço de acesso. Olá, chave que está atualmente em uso é hello *primário* chave e hello chave de backup é chamado tooas Olá *secundário* chave. Uma dessas duas chaves deve ser fornecida quando o dispositivo Microsoft Azure StorSimple acessa o provedor de serviços de armazenamento de nuvem.

## <a name="what-is-key-rotation"></a>O que é a rotação de chaves?

Normalmente, a aplicativos usam a apenas uma das Olá chaves tooaccess seus dados. Após um determinado período de tempo, você pode fazer com que seus aplicativos passar a segunda chave do toousing hello. Após a troca de sua chave secundária do toohello de aplicativos, você pode desativar a primeira chave de saudação e, em seguida, gerar uma nova chave. Usar duas chaves de saudação dessa maneira permite que seus aplicativos acessem toohello dados sem incorrer em qualquer tempo de inatividade.

chaves de conta de armazenamento Olá sempre são armazenadas no serviço de saudação em um formato criptografado. No entanto, elas podem ser redefinidas por meio de saudação de serviço do Gerenciador de dispositivos do StorSimple. serviço de saudação pode obter a chave primária hello e chave secundária para todas Olá contas de armazenamento em Olá gerada da mesma assinatura, incluindo contas criadas no serviço de armazenamento de hello, bem como contas de armazenamento padrão Olá Olá Gerenciador de dispositivos de StorSimple quando serviço foi criado. saudação de serviço do Gerenciador de dispositivos de StorSimple será sempre obtém essas chaves do hello portal clássico do Azure e, em seguida, armazená-los de forma criptografada.

## <a name="rotation-workflow"></a>Fluxo de trabalho de rotação

Um administrador do Microsoft Azure pode gerar novamente ou alterar a chave primária ou secundária de saudação acessando diretamente a conta de armazenamento da saudação (via Olá serviço de armazenamento do Microsoft Azure). saudação de serviço do Gerenciador de dispositivos do StorSimple não vê essa alteração automaticamente.

serviço de Gerenciador de dispositivos de StorSimple tooinform Olá de alteração Olá, serviço de Gerenciador de dispositivos do StorSimple do tooaccess Olá, será necessário acessar a conta de armazenamento hello e, em seguida, sincronizar a chave primária ou secundária hello (dependendo de qual delas foi alterada). serviço Hello, em seguida, obtém a chave mais recente hello, criptografa Olá chaves e envia Olá criptografado toohello chave dispositivo.

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service"></a>chaves de toosynchronize para contas de armazenamento no hello mesma assinatura que o serviço de saudação 
1. Acesse o serviço de Gerenciador de dispositivos de StorSimple tooyour. Em Olá **configuração** seção, clique em **credenciais da conta de armazenamento**.
2. Na listagem tabular de saudação de contas de armazenamento, clique em Olá um que você deseja toomodify. 

    ![sincronizar chaves](./media/storsimple-8000-manage-storage-accounts/syncaccesskey1.png)

3. Clique em **... Mais** e, em seguida, selecione **toorotate chave de acesso de sincronização**.   

    ![sincronizar chaves](./media/storsimple-8000-manage-storage-accounts/syncaccesskey2.png)

4. Olá serviço do Gerenciador de dispositivos de StorSimple, é necessário chave Olá tooupdate anteriormente foi alterado no hello serviço de armazenamento do Microsoft Azure. Se a chave de acesso primária Olá foi alterada (regenerada), selecione **primário** chave. Se a chave secundária Olá foi alterado, selecione **secundário** chave. Clique em **Sincronizar chave**.
      
      ![sincronizar chaves](./media/storsimple-8000-manage-storage-accounts/syncaccesskey3.png)

Você será notificado depois chave Olá com êxito é sycnhronized.

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a>chaves de toosynchronize para contas de armazenamento fora da assinatura do serviço Olá
1. Em Olá **serviços** , clique em Olá **configurar** guia.
2. Clique em **Adicionar/Editar Contas de Armazenamento**.
3. Na caixa de diálogo Olá Olá a seguir:
   
   1. Selecione a conta de armazenamento de saudação com chave de acesso de saudação que você deseja tooupdate.
   2. Você precisará de chave de acesso de armazenamento tooupdate Olá no hello serviço do Gerenciador de dispositivos do StorSimple. Nesse caso, você pode ver a chave de acesso de armazenamento hello. Insira a nova chave de saudação no hello **chave de acesso da conta de armazenamento** caixa. 
   3. Salve suas alterações. Sua chave de acesso da conta de armazenamento deve estar atualizada.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre a [segurança do StorSimple](storsimple-8000-security.md).
* Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador de dispositivos do StorSimple em seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).

