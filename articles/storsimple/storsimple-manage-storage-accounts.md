---
title: aaaManage sua conta de armazenamento StorSimple | Microsoft Docs
description: "Explica como você pode usar o hello StorSimple Manager Configurar página tooadd, editar, excluir ou chaves de segurança Olá Girar para uma conta de armazenamento."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 93207c40-e0eb-489e-8724-59fb94907081
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/29/2016
ms.author: v-sharos
ms.openlocfilehash: 78f408818ee8532dfaac445200048145547c987c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-your-storage-account"></a>Usar toomanage de serviço do StorSimple Manager Olá sua conta de armazenamento
## <a name="overview"></a>Visão geral
Olá **configurar** página apresenta todos os parâmetros de serviços globais de saudação que podem ser criados no hello serviço StorSimple Manager. Esses parâmetros podem ser tooall aplicados Olá dispositivos conectados toohello serviço e incluem:

* Contas de armazenamento 
* Modelos de largura de banda 
* Registros de controle de acesso 

Este tutorial explica como você pode usar o hello **configurar** página tooadd, editar ou excluir contas de armazenamento ou a rotação de chaves de segurança Olá para uma conta de armazenamento.

 ![Configurar página](./media/storsimple-manage-storage-accounts/HCS_ConfigureService.png)  

Contas de armazenamento contêm as credenciais de Olá Olá tooaccess do dispositivo usa sua conta de armazenamento com seu provedor de serviços de nuvem. Para contas de armazenamento do Microsoft Azure, essas são as credenciais como nome da conta hello e chave de acesso primária hello. 

Em Olá **configurar** página, todo o armazenamento de contas que são criadas para Olá cobrança de assinatura são exibidas em um formato de tabela que contém a saudação informações a seguir:

* **Nome** – Olá nome exclusivo atribuído toohello conta quando ele foi criado.
* **SSL habilitado** – se hello SSL está habilitado e comunicação de dispositivo para a nuvem é pelo canal seguro hello.
* **Usado por** – Olá número de volumes usando a conta de armazenamento hello.

tarefas mais comuns de saudação relacionadas toostorage contas que podem ser executadas em Olá **configurar** página são:

* Adicionar uma conta de armazenamento 
* Editar uma conta de armazenamento 
* Excluir uma conta de armazenamento 
* Rotação de chave de contas de armazenamento 

## <a name="types-of-storage-accounts"></a>Tipos de contas de armazenamento
Há três tipos de contas de armazenamento que podem ser usadas com o dispositivo StorSimple.

* **Contas de armazenamento gerada automaticamente** – como Olá nome sugere, esse tipo de conta de armazenamento é gerado automaticamente quando o serviço de saudação é criado pela primeira vez. toolearn mais sobre como a conta de armazenamento é criada, consulte [etapa 1: criar um novo serviço](storsimple-deployment-walkthrough-u1.md#step-1-create-a-new-service) na [implantar seu dispositivo do StorSimple local](storsimple-deployment-walkthrough.md). 
* **Contas de armazenamento na assinatura do serviço Olá** – essas são contas de armazenamento do Azure Olá que estão associadas a saudação mesma assinatura que o serviço de saudação. toolearn mais sobre como essas contas de armazenamento são criadas, consulte [sobre contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md). 
* **Contas de armazenamento fora da assinatura do serviço Olá** – essas são contas de armazenamento do Azure Olá que não estão associadas com o serviço e provavelmente Olá existente antes do serviço foi criado.

## <a name="add-a-storage-account"></a>Adicionar uma conta de armazenamento
Você pode adicionar uma conta de armazenamento, fornecendo uma única as credenciais de acesso e do nome amigáveis que estão vinculadas toohello conta de armazenamento (com o provedor de serviços de nuvem especificado Olá). Você também tem a opção de saudação da habilitação Olá seguro sockets layer (SSL) modo toocreate um canal seguro para comunicação de rede entre sua nuvem de dispositivo e hello.

Você pode criar várias contas para um provedor de serviços de nuvem específico. Lembre-se, no entanto, depois que uma conta de armazenamento é criada, você não pode alterar o provedor de serviços de nuvem hello.

Enquanto a conta de armazenamento hello está sendo salvo, o serviço de saudação tenta toocommunicate com seu provedor de serviços de nuvem. Olá credenciais e material de acesso de saudação que você forneceu serão autenticados neste momento. Uma conta de armazenamento é criada somente se Olá autenticação for bem-sucedida. Se a autenticação de saudação falhar, uma mensagem de erro apropriado será exibida.

Contas de armazenamento do Gerenciador de Recursos criadas no portal do Azure também são compatíveis com o StorSimple. Olá contas de armazenamento não aparecerá na lista suspensa de saudação para seleção durante a tentativa de toocreate um contêiner de volume, o Gerenciador de recursos somente Olá armazenamento contas criadas no portal clássico do Azure do hello serão exibidas. Contas de armazenamento do Gerenciador de recursos serão necessário toobe adicionado usando Olá procedimento tooadd uma conta de armazenamento descrita abaixo.

> [!NOTE]
> procedimento de saudação para adicionar uma conta de armazenamento varia com base na versão do software StorSimple Olá que você está usando. Ser o procedimento correto do se Olá de toofollow para a sua versão do StorSimple.
> 
> 

[!INCLUDE [add-a-storage-account-update1](../../includes/storsimple-configure-new-storage-account-u1.md)]

[!INCLUDE [add-a-storage-account](../../includes/storsimple-configure-new-storage-account.md)]

## <a name="edit-a-storage-account"></a>Editar uma conta de armazenamento
Você pode editar uma conta de armazenamento usada por um contêiner de volume. Se você editar uma conta de armazenamento que está atualmente em uso, hello somente campo toomodify disponível é Olá chave de acesso para a conta de armazenamento hello. Você pode fornecer a nova chave de acesso de armazenamento hello e salvar as configurações de saudação atualizada.

#### <a name="tooedit-a-storage-account"></a>tooedit uma conta de armazenamento
1. Na página de aterrissagem do serviço hello, selecione o seu serviço, clique duas vezes no nome do serviço hello e, em seguida, clique em **configurar**.
2. Clique em **Adicionar/Editar Contas de Armazenamento**.
3. Em Olá **adicionar/editar contas de armazenamento** caixa de diálogo:
   
   1. Na lista suspensa de saudação do **contas de armazenamento**, escolha uma conta existente que você gostaria que toomodify. Isso também pode incluir contas de armazenamento de saudação que foram geradas automaticamente quando o serviço de saudação foi criado.
   2. Se necessário, você pode modificar Olá **habilitar o modo SSL** seleção.
   3. Você pode escolher toorotate suas chaves de acesso da conta de armazenamento. Consulte [rotação de contas de armazenamento de chaves](#key-rotation-of-storage-accounts) para obter mais informações sobre como tooperform rotação de chaves.
   4. Clique o ícone de verificação Olá ![ícone de verificação](./media/storsimple-manage-storage-accounts/HCS_CheckIcon.png) toosave configurações de saudação. Olá configurações serão atualizadas no hello **configurar** página. Clique em **salvar** toosave Olá recém-atualizado configurações.
      
      ![Editar uma conta de armazenamento](./media/storsimple-manage-storage-accounts/HCs_AddEditStorageAccount.png)

## <a name="delete-a-storage-account"></a>Excluir uma conta de armazenamento
> [!IMPORTANT]
> Você pode excluir uma conta de armazenamento somente se ela não for usada por um contêiner de volume. Se uma conta de armazenamento está sendo usada por um contêiner de volume, primeiro excluir o contêiner de volume hello e, em seguida, excluir conta de armazenamento Olá associado.
> 
> 

#### <a name="toodelete-a-storage-account"></a>toodelete uma conta de armazenamento
1. Na página de aterrissagem do serviço do StorSimple Manager hello, selecione o seu serviço, clique duas vezes no nome do serviço hello e, em seguida, clique em **configurar**.
2. Na lista tabular de saudação de contas de armazenamento, passe o mouse sobre a conta de saudação que você deseja toodelete.
3. Um ícone de exclusão (**x**) aparecerá na coluna extremo direito de Olá para essa conta de armazenamento. Clique em Olá **x** credenciais de saudação do ícone toodelete.
4. Quando solicitado a confirmar, clique em **Sim** toocontinue com exclusão hello. listagem tabular Olá será atualizado tooreflect Olá alterações.

## <a name="key-rotation-of-storage-accounts"></a>Rotação de chave de contas de armazenamento
Por motivos de segurança, a rotação de chaves é normalmente um requisito em datacenters. 

> [!NOTE]
> Olá procedimento de rotação de informações e saudação de rotação de chaves a seguir se aplicam a tooMicrosoft apenas contas de armazenamento do Azure. Se você estiver usando outro provedor de serviços de nuvem, poderá gerenciar chaves de conta de armazenamento por meio do painel de controle do provedor.
> 
> 

Cada assinatura do Microsoft Azure pode ter uma ou mais contas de armazenamento associadas. contas de toothese Olá acesso é controlado pela assinatura hello e chaves de acesso para cada conta de armazenamento. 

Quando você cria uma conta de armazenamento, o Microsoft Azure gera duas chaves de acesso de armazenamento de 512 bits são usadas para autenticação quando a conta de armazenamento Olá é acessada. Ter duas chaves de acesso de armazenamento permite que você tooregenerate Olá chaves sem interrupção tooyour storage Service, serviço ou toothat o serviço de acesso. Olá, chave que está atualmente em uso é hello *primário* chave e hello chave de backup é chamado tooas Olá *secundário* chave. Uma dessas duas chaves deve ser fornecida quando o dispositivo Microsoft Azure StorSimple acessa o provedor de serviços de armazenamento de nuvem.

## <a name="what-is-key-rotation"></a>O que é a rotação de chaves?
Normalmente, a aplicativos usam a apenas uma das Olá chaves tooaccess seus dados. Após um determinado período de tempo, você pode fazer com que seus aplicativos passar a segunda chave do toousing hello. Após a troca de sua chave secundária do toohello de aplicativos, você pode desativar a primeira chave de saudação e, em seguida, gerar uma nova chave. Usar duas chaves de saudação dessa maneira permite que seus aplicativos acessem toohello dados sem incorrer em qualquer tempo de inatividade.

chaves de conta de armazenamento Olá sempre são armazenadas no serviço de saudação em um formato criptografado. No entanto, elas podem ser redefinidas por meio de saudação serviço StorSimple Manager. serviço de saudação pode obter a chave primária hello e chave secundária para todas Olá contas de armazenamento em Olá gerada da mesma assinatura, incluindo contas criadas no serviço de armazenamento de hello, bem como contas de armazenamento padrão Olá Olá serviço StorSimple Manager quando serviço foi criado. Olá serviço StorSimple Manager sempre obtém essas chaves de saudação portal clássico do Azure e, em seguida, armazená-los de forma criptografada.

## <a name="rotation-workflow"></a>Fluxo de trabalho de rotação
Um administrador do Microsoft Azure pode gerar novamente ou alterar a chave primária ou secundária de saudação acessando diretamente a conta de armazenamento da saudação (via Olá serviço de armazenamento do Microsoft Azure). Olá serviço StorSimple Manager não vê essa alteração automaticamente.

tooinform o serviço do StorSimple Manager Olá de alteração de saudação, o serviço StorSimple Manager Olá tooaccess, será necessário acessar a conta de armazenamento hello e, em seguida, sincronizar a chave primária ou secundária hello (dependendo de qual delas foi alterada). serviço Hello, em seguida, obtém a chave mais recente hello, criptografa Olá chaves e envia Olá criptografado toohello chave dispositivo.

#### <a name="toosynchronize-keys-for-storage-accounts-in-hello-same-subscription-as-hello-service-azure-only"></a>chaves de toosynchronize para contas de armazenamento no hello mesma assinatura que o serviço de saudação (somente no Azure)
1. Em Olá **serviços** , clique em Olá **configurar** guia.
2. Clique em **Adicionar/Editar Contas de Armazenamento**.
3. Na caixa de diálogo Olá Olá a seguir:
   
   1. Selecione a conta de armazenamento de saudação com chave Olá que você deseja toosynchronize. chaves de conta de armazenamento Olá são criptografadas quando elas são exibidas.
   2. Olá serviço StorSimple Manager, é necessário chave Olá tooupdate anteriormente foi alterado no hello serviço de armazenamento do Microsoft Azure. Se a chave de acesso primária Olá foi alterada (regenerada), clique em **sincronizar chave primária**. Se a chave secundária Olá foi alterada, clique em **sincronizar chave secundária**.
      
      ![sincronizar chaves](./media/storsimple-manage-storage-accounts/HCS_KeyRotationStorageAccountSameSubscriptionAsService.png)

#### <a name="toosynchronize-keys-for-storage-accounts-outside-of-hello-service-subscription"></a>chaves de toosynchronize para contas de armazenamento fora da assinatura do serviço Olá
1. Em Olá **serviços** , clique em Olá **configurar** guia.
2. Clique em **Adicionar/Editar Contas de Armazenamento**.
3. Na caixa de diálogo Olá Olá a seguir:
   
   1. Selecione a conta de armazenamento de saudação com chave de acesso de saudação que você deseja tooupdate.
   2. Você precisará de chave de acesso de armazenamento tooupdate Olá no hello serviço StorSimple Manager. Nesse caso, você pode ver a chave de acesso de armazenamento hello. Insira a nova chave de saudação no hello **chave de acesso da conta de armazenamento**caixa y. 
   3. Salve suas alterações. Sua chave de acesso da conta de armazenamento deve estar atualizada.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre a [segurança do StorSimple](storsimple-security.md).
* Saiba mais sobre [usando Olá tooadminister de serviço do Gerenciador do StorSimple em seu dispositivo StorSimple](storsimple-manager-service-administration.md).

