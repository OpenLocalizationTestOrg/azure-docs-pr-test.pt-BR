---
title: "Olá aaaDeploy serviço do Gerenciador de dispositivos do StorSimple no Azure | Microsoft Docs"
description: "Explica como toocreate e delete Olá serviço do Gerenciador de dispositivos do StorSimple no hello portal do Azure e descreve como toomanage Olá a chave de registro de serviço."
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
ms.date: 07/13/2017
ms.author: alkohli
ms.openlocfilehash: b84a907d6b735c8fee7bdc51f9c0074857297d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-8000-series-devices"></a>Implantar o serviço do Gerenciador de dispositivos de StorSimple Olá para dispositivos da série StorSimple 8000

## <a name="overview"></a>Visão geral

saudação de serviço do Gerenciador de dispositivos do StorSimple é executado no Microsoft Azure e conecta dispositivos de StorSimple toomultiple. Depois de criar o serviço hello, você pode usá-lo toomanage todos os dispositivos de saudação que são conectado toohello Gerenciador de dispositivos do StorSimple do serviço de um único local central, minimizando a carga administrativa.

Este tutorial descreve etapas Olá necessárias para Olá criação, exclusão, a migração do serviço de saudação e gerenciamento de saudação da chave de registro do serviço de saudação. informações de saudação contidas neste artigo são aplicável somente dispositivos da série tooStorSimple 8000. Para obter mais informações sobre matrizes Virtual StorSimple, vá muito[implantar um serviço de Gerenciador de dispositivos de StorSimple para sua matriz Virtual StorSimple](storsimple-virtual-array-manage-service.md).

## <a name="create-a-service"></a>Criar um serviço
toocreate um serviço de Gerenciador de dispositivos de StorSimple, você precisa toohave:

* Uma assinatura com um Enterprise Agreement
* Uma conta de armazenamento ativa do Microsoft Azure
* Olá informações de cobrança que são usadas para gerenciamento de acesso

São permitidas somente Olá assinaturas com um Enterprise Agreement. Não há suporte para assinaturas do Microsoft Sponsorship que eram permitidas no hello portal clássico do Azure no portal do Azure de saudação. Você verá Olá mensagem a seguir ao usar uma assinatura sem suporte:

![Assinatura inválida](./media/storsimple-8000-manage-service/subscription-not-valid.jpg)

Além disso, é possível toogenerate uma conta de armazenamento padrão ao criar serviço hello.

Um único serviço pode gerenciar vários dispositivos. No entanto, um dispositivo não pode abranger vários serviços. Uma grande empresa pode ter vários toowork de instâncias de serviço com diferentes assinaturas, organizações ou mesmo regiões de implantação. 

> [!NOTE]
> Você precisa de instâncias separadas de dispositivos da série StorSimple 8000 Gerenciador de dispositivos do StorSimple service toomanage e matrizes de Virtual do StorSimple.

Execute Olá etapas toocreate um serviço a seguir.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]


Para cada serviço de Gerenciador de dispositivos de StorSimple, Olá atributos a seguir existe:

* **Nome** – nome hello que foi atribuído o serviço do Gerenciador de dispositivos de StorSimple tooyour quando ele foi criado. **nome do serviço Olá não pode ser alterado depois que o serviço Olá é criado. Isso também é verdadeiro para outras entidades, como os dispositivos, volumes, contêineres de volume e políticas de backup que não podem ser renomeadas no hello portal do Azure.**
* **Status** – Olá status do serviço de saudação, que pode ser **Active**, **criando**, ou **Online**.
* **Local** – Olá localização geográfica na qual Olá StorSimple dispositivo será implantado.
* **Assinatura** – hello cobrança de assinatura que está associada ao seu serviço.

## <a name="move-a-service-tooazure-portal"></a>Mover um portal tooAzure
Série StorSimple 8000 agora pode ser gerenciado no hello portal do Azure. Se você tiver um serviço toomanage Olá StorSimple os dispositivos existentes, é recomendável que você mova seu toohello service portal do Azure. Olá portal clássico do Azure para Olá serviço StorSimple Manager não está disponível após 30 de setembro de 2017.

Olá opção toomigrate toohello portal do Azure está disponível em fases. Se você não vir um portal de tooAzure toomigrate opção, mas você deseja toomove e examinou o impacto de saudação da migração conforme documentado no hello [considerações sobre a transição](#considerations-for-transition), você pode [enviar uma solicitação](https://aka.ms/ss8000-cx-signup).

### <a name="considerations-for-transition"></a>Considerações sobre a transição

Analisar o impacto de saudação de migração toohello novo portal do Azure antes de mover o serviço de saudação.

#### <a name="before-you-transition"></a>Antes da transição

* Seu dispositivo executa a Atualização 3.0 ou posterior. Se seu dispositivo está executando uma versão mais antiga, instale as atualizações mais recentes de saudação. Para obter mais informações, vá muito[instalar atualização 4](storsimple-8000-install-update-4.md). Se usar um Dispositivo de Nuvem StorSimple (8010/8020), crie um novo dispositivo de nuvem com Atualização 4.0. 

* Quando estiver toohello transição novo portal do Azure, você não pode usar Olá toomanage de portal clássico do Azure em seu dispositivo StorSimple.

* transição de saudação é interrupções e não há nenhum tempo de inatividade para dispositivo hello.

* Todos os gerenciadores de dispositivo StorSimple Olá em Olá especificado assinatura são transferidas.

#### <a name="during-hello-transition"></a>Durante a transição de saudação

* Você não pode gerenciar seu dispositivo do portal de saudação.
* As operações, como backups agendados e camadas continuar toooccur.
* Não exclua Olá antigo gerenciadores de dispositivos de StorSimple enquanto transição hello está em andamento.

#### <a name="after-hello-transition"></a>Após a transição de saudação

* Você não poderá mais gerenciar seus dispositivos no portal clássico do hello.

* Não há suporte para os cmdlets do PowerShell do Azure Service Management (ASM) existentes Hello. Atualize Olá scripts toomanage seus dispositivos por meio de saudação do Azure Resource Manager.

* A configuração do serviço e do dispositivo é mantida. Todos os volumes e backups também são toohello transição portal do Azure.

### <a name="begin-transition"></a>Iniciar a transição

Execute Olá seguindo as etapas tootransition toohello seu serviço portal do Azure.

1. Acesse o serviço StorSimple Manager existente tooyour no portal clássico do hello.

2. Você verá uma notificação informando que o serviço do Gerenciador de dispositivos de StorSimple Olá agora está disponível no hello portal do Azure. Observe que, Olá portal do Azure, serviço de saudação é tooas chamado serviço de Gerenciador de dispositivos do StorSimple.

    ![Notificação de migração](./media/storsimple-8000-manage-service/service-transition1.jpg)

    1. Certifique-se de que você leu o impacto total de saudação da migração.
    2. Examine a lista de saudação de gerenciadores de dispositivo StorSimple que serão movidos no portal clássico do hello.

3. Clique em **Migrar**. transição de saudação inicia e leva toocomplete de alguns minutos.

Após a conclusão da transição hello, você pode gerenciar seus dispositivos por meio de saudação de serviço do Gerenciador de dispositivos do StorSimple no hello portal do Azure.

Em Olá portal do Azure, Olá somente dispositivos de StorSimple executando Update 3.0 e superior têm suporte. dispositivos de saudação que estão executando versões mais antigas têm suporte limitado. Olá summrizes tabela quais operações são suportadas em dispositivo Olá executando versios anterior tooUpdate 3.0, depois que você migrou do hello clássico toohello portal do Azure a seguir.

| Operação                                                                                                                       | Suportado      |
|---------------------------------------------------------------------------------------------------------------------------------|----------------|
| Registrar um dispositivo                                                                                                               | Sim            |
| Definir as configurações do dispositivo, tais como configurações gerais, de rede e de segurança                                                                | Sim            |
| Examinar, baixar e instalar atualizações                                                                                             | Sim            |
| Desativar um dispositivo                                                                                                               | Sim            |
| Excluir um dispositivo                                                                                                                   | Sim            |
| Criar, modificar e excluir um contêiner de volume                                                                                   | Não             |
| Criar, modificar e excluir um volume                                                                                             | Não             |
| Criar, modificar e excluir uma política de backup                                                                                      | Não             |
| Fazer um backup manual                                                                                                            | Não             |
| Realizar um backup agendado                                                                                                         | Não aplicável |
| Restaurar de um conjunto de backup                                                                                                        | Não             |
| Clonar tooa dispositivos que executam a atualização 3.0 e posterior <br> dispositivo de origem Hello está sendo executado tooUpdate anterior da versão 3.0.                                | Sim            |
| Clonar tooa dispositivo executando versões anteriores tooUpdate 3.0                                                                          | Não             |
| Failover como dispositivo de origem <br> (de um dispositivo executando versão anterior tooUpdate 3.0 tooa dispositivo executando atualização 3.0 e posterior)                                                               | Sim            |
| Failover como dispositivo de destino <br> (dispositivo tooa executando tooUpdate anterior do software versão 3.0)                                                                                   | Não             |
| Limpar um alerta                                                                                                                  | Sim            |
| Exibir políticas de backup, catálogo de backup, volumes, contêineres de volume, gráficos de monitoramento, trabalhos e alertas criados no portal clássico | Sim            |
| Ativar e desativar controladores de dispositivo                                                                                              | Sim            |


## <a name="delete-a-service"></a>Excluir um serviço

Antes de excluir um serviço, verifique se nenhum dispositivo conectado está usando ele. Se o serviço de saudação está em uso, desative os dispositivos de saudação conectado. Olá desativar operação sever conexão Olá entre dispositivo hello e serviço hello, mas preservar os dados do dispositivo Olá na nuvem hello.

> [!IMPORTANT]
> Depois que um serviço é excluído, operação Olá não pode ser revertida. Qualquer dispositivo que esteja usando o serviço de saudação precisa toobe redefinição toofactory padrões antes que ele pode ser usado com outro serviço. Nesse cenário, os dados de locais de saudação em dispositivo hello, bem como configuração Olá, será perdido.

Execute Olá etapas toodelete um serviço a seguir.

### <a name="toodelete-a-service"></a>toodelete um serviço

1. Pesquisa para o serviço de saudação você deseja toodelete. Clique em **recursos** ícone e, em seguida, entrada hello toosearch termos apropriado. Nos resultados da pesquisa hello, clique em serviço Olá deseja toodelete.

    ![Toodelete do serviço de pesquisa](./media/storsimple-8000-manage-service/deletessdevman1.png)

2. Isso leva folha de serviço do Gerenciador de dispositivos de StorSimple toohello. Clique em **Excluir**.

    ![Excluir serviço](./media/storsimple-8000-manage-service/deletessdevman2.png)

3. Clique em **Sim** na notificação de confirmação de saudação. Ele pode levar alguns minutos para Olá serviço toobe excluído.

    ![Confirmar exclusão](./media/storsimple-8000-manage-service/deletessdevman3.png)

## <a name="get-hello-service-registration-key"></a>Obter chave de registro de serviço Olá

Depois que você criou com êxito um serviço, você precisará tooregister seu dispositivo StorSimple com o serviço de saudação. tooregister seu dispositivo StorSimple primeiro, será necessário Olá o chave de registro de serviço. tooregister dispositivos adicionais com um serviço StorSimple existente, é necessário chave de registro hello e chave criptografia de dados de serviço de saudação (que é gerado no primeiro dispositivo de saudação durante o registro). Para obter mais informações sobre a chave de criptografia de dados de serviço hello, consulte [segurança de StorSimple](storsimple-8000-security.md). Você pode obter a chave de registro Olá acessando **chaves** na sua folha de Gerenciador de dispositivos do StorSimple.

Execute Olá etapas tooget Olá chave de registro a seguir.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

Mantenha a chave de registro do serviço de saudação em um local seguro. Você precisará essa chave, bem como chave de criptografia de dados de serviço hello, tooregister de dispositivos adicionais com este serviço. Depois de obter a chave de registro de serviço hello, você deve configurar seu dispositivo por meio de saudação do Windows PowerShell para StorSimple interface.

Para obter detalhes sobre como toouse essa chave de registro, consulte [etapa 3: configurar e registrar o dispositivo Olá por meio do Windows PowerShell para StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Regenerar chave de registro de serviço Olá
É necessário tooregenerate uma chave de registro de serviço se for necessário tooperform a rotação de chaves ou se a lista de saudação de administradores de serviço foi alterada. Quando você regenerar chave Olá, a nova chave de saudação é usado apenas para registrar dispositivos subsequentes. dispositivos de saudação que já foram registrados não são afetados por esse processo.

Execute Olá etapas tooregenerate uma chave de registro de serviço a seguir.

### <a name="tooregenerate-hello-service-registration-key"></a>chave de registro tooregenerate Olá
1. Em Olá **Gerenciador de dispositivos de StorSimple** folha, ir muito**gerenciamento &gt;**  **chaves**.
    
    ![Folha Chaves](./media/storsimple-8000-manage-service/regenregkey2.png)

2. Em Olá **chaves** folha, clique em **regenerar**.

    ![Clique em regenerar](./media/storsimple-8000-manage-service/regenregkey3.png)
3. Em Olá **regenerar chave de registro** folha, examine Olá necessária uma ação quando hello chaves são geradas novamente. Todos os dispositivos de saudação subsequentes que são registrados com este serviço usarem nova chave de registro hello. Clique em **regenerar** tooconfirm. Você será notificado depois que a regeneração Olá for concluída.

    ![Confirmar a regeneração](./media/storsimple-8000-manage-service/regenregkey4.png)

4. Uma nova chave de registro de serviço será exibida.

5. Copie essa chave e salve-a para registrar todos os novos dispositivos nesse serviço.



## <a name="change-hello-service-data-encryption-key"></a>Alterar a chave de criptografia de dados de serviço Olá
Chaves de criptografia de dados de serviço são dados confidenciais do cliente de tooencrypt usadas, como credenciais de conta de armazenamento, que são enviadas de seu dispositivo do StorSimple Manager serviço toohello StorSimple. Você precisará toochange essas chaves periodicamente se sua organização de TI tiver uma política de rotação de chaves em dispositivos de armazenamento de saudação. Olá processo de alteração de chave pode ser ligeiramente diferente dependendo se há um único ou vários dispositivos gerenciados pelo Olá serviço StorSimple Manager. Para obter mais informações, vá muito[StorSimple segurança e proteção de dados](storsimple-8000-security.md).

Alterar chave de criptografia de dados para serviço Olá é um processo de 3 etapas:

1. Usando scripts do Windows PowerShell para o Gerenciador de recursos do Azure, autorize a chave de criptografia de dados de serviço um dispositivo toochange hello.
2. Usando o Windows PowerShell para StorSimple, inicie a alteração de criptografia de dados chave serviço hello.
3. Se você tiver mais de um dispositivo StorSimple, atualize a chave de criptografia de dados de serviço de saudação em Olá outros dispositivos.

### <a name="step-1-use-windows-powershell-script-tooauthorize-a-device-toochange-hello-service-data-encryption-key"></a>Etapa 1: Usar o Windows PowerShell script tooAuthorize uma chave de criptografia do dispositivo toochange Olá serviço dados
Normalmente, administrador do dispositivo Olá solicita esse administrador de serviço Olá autorizar chaves de criptografia de dados de serviço para toochange um dispositivo. administrador de serviço Hello, então, autorizará chave de Olá Olá dispositivo toochange.

Esta etapa é executada usando hello Azure Resource Manager com base em script. administrador de serviço Olá pode selecionar um dispositivo que é qualificado toobe autorizado. dispositivo Olá é, em seguida, o processo de alteração da chave de criptografia de dados do serviço de saudação toostart autorizados. 

Para obter mais informações sobre como usar o script hello, ir muito[ServiceEncryptionRollover.ps1 autorizar](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Authorize-ServiceEncryptionRollover.ps1)

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Quais dispositivos podem ser autorizados toochange chaves de criptografia de dados de serviço?
Um dispositivo deve atender aos Olá critérios a seguir para que possa ser alterações de criptografia de dados chave serviço tooinitiate autorizados:

* dispositivo de saudação deve ser on-line toobe qualificado para autorização de alteração de chave de criptografia de dados de serviço.
* Você pode autorizar Olá mesmo dispositivo novamente após 30 minutos se a alteração da chave de saudação não foi iniciado.
* Você pode autorizar um dispositivo diferente, desde que a alteração da chave Olá não foi iniciada pelo dispositivo anteriormente autorizado hello. Depois que o novo dispositivo de saudação tiver sido autorizado, dispositivo antigo Olá não pode iniciar a alteração hello.
* Não é possível autorizar um dispositivo, enquanto Olá substituição de chave de criptografia de dados de serviço hello está em andamento.
* Você pode autorizar um dispositivo quando alguns dispositivos Olá registrados com o serviço de saudação tiveram substituído Olá criptografia enquanto outros não. 

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>Etapa 2: Usar o Windows PowerShell para StorSimple tooinitiate Olá serviço criptografia chave alteração de dados
Esta etapa é executada no saudação do Windows PowerShell para StorSimple interface Olá autorizado dispositivo StorSimple.

> [!NOTE]
> Nenhuma operação pode ser executada no hello portal do Azure do seu serviço StorSimple Manager até que a substituição de chave Olá é concluída.
> 
> 

Se você estiver usando a interface do hello dispositivo console serial tooconnect toohello do Windows PowerShell, execute Olá etapas a seguir.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>alteração da chave de criptografia de dados de serviço do tooinitiate Olá
1. Selecione a opção 1 toolog com acesso completo.
2. No prompt de comando hello, digite:
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Depois que o cmdlet Olá for concluída com êxito, você obterá uma nova chave de criptografia de dados de serviço. Copie e salve essa chave para uso na etapa 3 deste processo. Esta chave será usada tooupdate Olá todos os demais dispositivos registrados com o serviço StorSimple Manager hello.
   
   > [!NOTE]
   > Esse processo deve ser iniciado em quatro horas, a contar da autorização de um dispositivo StorSimple.
   > 
   > 
   
   Essa nova chave é enviada toohello toobe enviada por push tooall Olá dispositivos de serviço que são registrados com o serviço de saudação. Um alerta aparecerá no painel de serviço hello. serviço Olá desabilitará todas as operações de Olá Olá registrado dispositivos e administrador do dispositivo hello, em seguida, será necessário chave de criptografia de dados tooupdate Olá serviço em Olá outros dispositivos. No entanto, hello e/SS (hosts que enviam dados na nuvem toohello) não serão interrompidas.
   
   Se você tiver um único dispositivo registrado tooyour serviço, o processo de substituição Olá agora está concluído e você pode ignorar Olá próxima etapa. Se você tiver vários serviços de tooyour registrados de dispositivos, vá toostep 3.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>Etapa 3: Atualize a chave de criptografia de dados de serviço de saudação em outros dispositivos de StorSimple
Essas etapas devem ser executadas na interface do Windows PowerShell de saudação do seu dispositivo StorSimple, se você tiver vários dispositivos registrados tooyour StorSimple Manager service. chave de saudação que você obteve na etapa 2 deve ser usado tooupdate todos Olá restante do dispositivo StorSimple registrado com hello serviço StorSimple Manager.

Execute Olá criptografia de dados de serviço do etapas tooupdate Olá a seguir em seu dispositivo.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>chave de criptografia de dados de serviço do tooupdate Olá
1. Use o Windows PowerShell para StorSimple tooconnect toohello console. Selecione a opção 1 toolog com acesso completo.
2. No prompt de comando hello, digite:
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Forneça Olá serviço dados chave de criptografia que você obteve na [etapa 2: usar o Windows PowerShell para StorSimple tooinitiate Olá serviço alteração criptografia de dados chave](#to-initiate-the-service-data-encryption-key-change).


## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre Olá [o processo de implantação StorSimple](storsimple-8000-deployment-walkthrough-u2.md).
* [Saiba mais sobre como gerenciar sua conta de armazenamento do StorSimple](storsimple-8000-manage-storage-accounts.md).
* Saiba mais sobre como muito[use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).
