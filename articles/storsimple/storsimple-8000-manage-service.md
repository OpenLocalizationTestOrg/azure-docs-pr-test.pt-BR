---
title: "Implantar o serviço do Gerenciador de Dispositivos do StorSimple no Azure | Microsoft Docs"
description: "Explica como criar e excluir o serviço Gerenciador de Dispositivo do StorSimple no Portal do Azure, além de descrever como gerenciar a chave de registro do serviço."
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
ms.date: 10/04/2017
ms.author: alkohli
ms.openlocfilehash: 96dcda25cde2473387842fd01421b6bb619e4ece
ms.sourcegitcommit: 48fce90a4ec357d2fb89183141610789003993d2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2018
---
# <a name="deploy-the-storsimple-device-manager-service-for-storsimple-8000-series-devices"></a>Implantar o serviço do Gerenciador de Dispositivos do StorSimple para dispositivos StorSimple da série 8000

## <a name="overview"></a>Visão geral

O serviço Gerenciador de Dispositivo do StorSimple é executado no Microsoft Azure e se conecta a vários dispositivos StorSimple. Depois de criar o serviço, você pode usá-lo para gerenciar todos os dispositivos que estão conectados ao serviço do Gerenciador de Dispositivos do StorSimple de um local único e central, minimizando assim a carga administrativa.

Este tutorial descreve as etapas necessárias para a criação, exclusão e migração do serviço e o gerenciamento da chave de Registro do serviço. As informações contidas neste artigo aplicam-se apenas a dispositivos StorSimple da série 8000. Para obter mais informações sobre Matrizes Virtual do StorSimple, acesse [Implantar um serviço do Gerenciador de Dispositivos do StorSimple para sua Matriz Virtual do StorSimple](storsimple-virtual-array-manage-service.md).

> [!NOTE]
> Todos os gerenciadores de dispositivo clássicos do StorSimple foram movidos automaticamente para o novo Portal do Azure. Se você tiver dúvidas, consulte [Perguntas Frequentes: migrar para o Portal do Azure](storsimple-8000-move-azure-portal-faq.md). Não há suporte para os cmdlets do PowerShell do Azure Service Management (ASM) após a mudança para o novo Portal do Azure. Atualize os scripts para gerenciar seus dispositivos e, em seguida, vá para o [Use scripts do Azure Resource Manager com base no SDK para gerenciar dispositivos do StorSimple](storsimple-8000-automation-azurerm-scripts.md) para obter mais informações. O novo Portal do Azure dá suporte a dispositivos que executam a Atualização 5.0 ou posterior. Se seu dispositivo não for atualizado, instale a Atualização 5 imediatamente. Para saber mais, vá para [Instalar a Atualização 5](storsimple-8000-install-update-5.md). Se você estiver usando um Dispositivo de Nuvem StorSimple (8010/8020), você não poderá atualizar um dispositivo de nuvem. Use a versão mais recente do software para criar um novo dispositivo de nuvem com Atualização 5.0 e, em seguida, faça failover para o novo dispositivo de nuvem criado. Todos os dispositivos que executam a atualização 4.0 ou anterior terão [funcionalidade de gerenciamento reduzida](storsimple-8000-manage-service.md#supported-operations-on-devices-running-versions-prior-to-update-5.0). 

## <a name="create-a-service"></a>Criar um serviço
Para criar um serviço do Gerenciador de Dispositivos do StorSimple, você precisa ter:

* Uma assinatura com um Enterprise Agreement
* Uma conta de armazenamento ativa do Microsoft Azure
* As informações de cobrança que são usadas para gerenciamento de acesso

Somente as assinaturas com um Contrato Enterprise são permitidas. Não há suporte para assinaturas do Microsoft Sponsorship no Portal do Azure, as que eram permitidas no Portal Clássico do Azure. Você verá a seguinte mensagem ao usar uma assinatura sem suporte:

![Assinatura inválida](./media/storsimple-8000-manage-service/subscription-not-valid.jpg)

Também é possível optar por gerar uma conta de armazenamento padrão ao criar o serviço.

Um único serviço pode gerenciar vários dispositivos. No entanto, um dispositivo não pode abranger vários serviços. Uma grande empresa pode ter várias instâncias do serviço para trabalhar com diferentes assinaturas, organizações ou até mesmo locais de implantação. 

> [!NOTE]
> Você precisa de instâncias separadas do serviço Gerenciador de Dispositivo do StorSimple para gerenciar as Matrizes Virtuais e os dispositivos da série 8000 do StorSimple.

Execute as etapas a seguir para criar um serviço.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-8000-create-new-service.md)]


Os atributos a seguir existem para cada serviço do Gerenciador de Dispositivos do StorSimple:

* **Nome** – O nome que foi atribuído ao serviço do Gerenciador de Dispositivos do StorSimple quando ele foi criado. **O nome do serviço não pode ser alterado depois que o serviço é criado. O mesmo ocorre para outras entidades como dispositivos, volumes, contêineres de volume e políticas de backup, os quais não podem ser renomeados no Portal do Azure.**
* **Status**: o status do serviço, que pode ser **Ativo**, **Criando** ou **Online**.
* **Local** : a localização geográfica em que o dispositivo StorSimple será implantado.
* **Assinatura** : a assinatura de cobrança associada ao seu serviço.

## <a name="delete-a-service"></a>Excluir um serviço

Antes de excluir um serviço, verifique se nenhum dispositivo conectado está usando ele. Se o serviço estiver em uso, desative os dispositivos conectados. A operação de desativação desfaz a conexão entre o dispositivo e o serviço, mas preserva os dados do dispositivo na nuvem.

> [!IMPORTANT]
> Depois que um serviço é excluído, a operação não pode ser revertida. Qualquer dispositivo que usava o serviço precisará ser redefinido para as configurações de fábrica para poder ser usado com outro serviço. Nesse cenário, os dados locais no dispositivo, bem como a configuração, serão perdidos.

Execute as etapas a seguir para excluir um serviço.

### <a name="to-delete-a-service"></a>Para excluir um serviço

1. Pesquise o serviço que você deseja excluir. Clique no ícone **Recursos** e insira os termos apropriados para pesquisar. Nos resultados da pesquisa, clique no serviço que você deseja excluir.

    ![Pesquise o serviço a ser excluído](./media/storsimple-8000-manage-service/deletessdevman1.png)

2. Isso levará você para a folha do serviço do Gerenciador de Dispositivos do StorSimple. Clique em **Excluir**.

    ![Excluir serviço](./media/storsimple-8000-manage-service/deletessdevman2.png)

3. Clique em **Sim** na notificação de confirmação. Pode levar alguns minutos para que o serviço seja excluído.

    ![Confirmar exclusão](./media/storsimple-8000-manage-service/deletessdevman3.png)

## <a name="get-the-service-registration-key"></a>Obtenha a chave de registro do serviço

Depois de ter criado um serviço com êxito, você precisará registrar o dispositivo StorSimple no serviço. Para registrar seu primeiro dispositivo StorSimple, será necessária a chave de registro do serviço. Para registrar dispositivos adicionais em um serviço StorSimple existente, você precisará da chave de registro e da chave de criptografia de dados de serviço (que é gerada durante o registro do primeiro dispositivo). Para obter mais informações sobre a chave de criptografia dos dados de serviço, consulte [Segurança do StorSimple](storsimple-8000-security.md). Você pode obter a chave de registro acessando **Chaves** na folha do Gerenciador de Dispositivos do StorSimple.

Execute as etapas a seguir para obter a chave de registro do serviço.

[!INCLUDE [storsimple-8000-get-service-registration-key](../../includes/storsimple-8000-get-service-registration-key.md)]

Mantenha a chave de registro do serviço em local seguro. Você precisará dessa chave, bem como da chave de criptografia dos dados de serviço, para registrar dispositivos adicionais nesse serviço. Depois de obter a chave de registro do serviço, você deverá configurar o dispositivo usando a Interface do Windows PowerShell para StorSimple.

Para obter detalhes sobre como usar essa chave de registro, consulte [Etapa 3: Configurar e registrar o dispositivo por meio do Windows PowerShell para StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-the-service-registration-key"></a>Regenerar a chave de registro do serviço
Você precisará regenerar uma chave de registro do serviço se for necessário realizar a rotação de chave ou se a lista de administradores de serviço tiver mudado. Quando você regenera a chave, a nova chave é usada somente para registrar dispositivos subsequentes. Os dispositivos que já foram registrados não serão afetados por esse processo.

Execute as etapas a seguir para regenerar uma chave de registro de serviço.

### <a name="to-regenerate-the-service-registration-key"></a>Para regenerar a chave de registro de serviço
1. No **Gerenciador de Dispositivo do StorSimple**, acesse **Gerenciamento&gt;** **Chaves**.
    
    ![Folha Chaves](./media/storsimple-8000-manage-service/regenregkey2.png)

2. Na folha **Chaves**, clique em **Regenerar**.

    ![Clique em regenerar](./media/storsimple-8000-manage-service/regenregkey3.png)
3. Na folha **Regenerar chave de registro do serviço**, revise a ação necessária quando as chaves forem geradas novamente. Todos os dispositivos subsequentes registrados com esse serviço usarão a nova chave de Registro. Clique em **Regenerar** para confirmar. Você será notificado quando a regeneração for concluída.

    ![Confirmar a regeneração](./media/storsimple-8000-manage-service/regenregkey4.png)

4. Uma nova chave de registro de serviço será exibida.

5. Copie essa chave e salve-a para registrar todos os novos dispositivos nesse serviço.



## <a name="change-the-service-data-encryption-key"></a>Alterar a chave de criptografia de dados do serviço
As chaves de criptografia de dados de serviço são usadas para criptografar dados confidenciais, como credenciais de conta de armazenamento, que são enviadas de seu serviço StorSimple Manager ao dispositivo StorSimple. Você precisará alterar essas chaves periodicamente se sua organização de TI tiver uma política de rotação de chave nos dispositivos de armazenamento. O processo de alteração de chave pode ser ligeiramente diferente dependendo se há um só ou vários dispositivos gerenciados pelo serviço StorSimple Manager. Para obter mais informações, acesse [Segurança e proteção de dados do StorSimple](storsimple-8000-security.md).

A alteração da chave de criptografia de dados de serviço é um processo de três etapas:

1. Usando scripts do Windows PowerShell para o Azure Resource Manager, autorize um dispositivo a alterar a chave de criptografia de dados de serviço.
2. Usar o Windows PowerShell para StorSimple para iniciar a alteração da chave de criptografia de dados de serviço.
3. Se você tiver mais de um dispositivo StorSimple, atualize a chave de criptografia de dados de serviço nos outros dispositivos.

### <a name="step-1-use-windows-powershell-script-to-authorize-a-device-to-change-the-service-data-encryption-key"></a>Etapa 1: use um script do Windows PowerShell para autorizar um dispositivo a alterar a chave de criptografia de dados de serviço
Normalmente, o administrador do dispositivo solicita que o administrador do serviço autorize um dispositivo a alterar as chaves de criptografia de dados de serviço. O administrador do serviço então autoriza o dispositivo a alterar a chave.

Esta etapa é executada usando o script baseado no Azure Resource Manager. O administrador de serviços pode selecionar um dispositivo qualificado para receber a autorização. O dispositivo é então autorizado a iniciar o processo de alteração da chave de criptografia de dados de serviço. 

Para obter mais informações sobre como usar o script, acesse [Authorize-ServiceEncryptionRollover.ps1](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Authorize-ServiceEncryptionRollover.ps1)

#### <a name="which-devices-can-be-authorized-to-change-service-data-encryption-keys"></a>Quais dispositivos podem ser autorizados a alterar as chaves de criptografia de dados de serviço?
Um dispositivo deve atender aos seguintes critérios para que possa ser autorizado a iniciar as alterações da chave de criptografia de dados de serviço:

* O dispositivo deve estar online para ser qualificado para autorização da alteração da chave de criptografia de dados de serviço.
* Você pode autorizar o mesmo dispositivo novamente após 30 minutos, caso a alteração de chave não tenha sido iniciada.
* Você pode autorizar um dispositivo diferente, desde que a alteração de chave não tenha sido iniciada pelo dispositivo autorizado anteriormente. Depois que o novo dispositivo tiver sido autorizado, o dispositivo antigo não poderá iniciar a alteração.
* Não é possível autorizar um dispositivo enquanto a substituição da chave de criptografia de dados de serviço estiver em andamento.
* Você pode autorizar um dispositivo quando alguns dos dispositivos registrados no serviço tiverem substituído a criptografia, enquanto outros não. 

### <a name="step-2-use-windows-powershell-for-storsimple-to-initiate-the-service-data-encryption-key-change"></a>Etapa 2: Usar o Windows PowerShell para StorSimple para iniciar a alteração da chave de criptografia de dados de serviço
Essa etapa é executada na interface do Windows PowerShell para StorSimple no dispositivo StorSimple autorizado.

> [!NOTE]
> Nenhuma operação poderá ser executada no Portal do Azure do serviço do StorSimple Manager até que a substituição de chave esteja concluída.
> 
> 

Se você estiver usando o console serial do dispositivo para se conectar à interface do Windows PowerShell, execute as etapas a seguir.

#### <a name="to-initiate-the-service-data-encryption-key-change"></a>Para iniciar a alteração da chave de criptografia de dados de serviço
1. Selecione a Opção 1 para fazer logon com acesso completo.
2. No prompt de comando, digite:
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Depois que o cmdlet tiver sido concluído com êxito, você receberá uma nova chave de criptografia de dados de serviço. Copie e salve essa chave para uso na etapa 3 deste processo. Essa chave será usada para atualizar todos os dispositivos restantes registrados no serviço StorSimple Manager.
   
   > [!NOTE]
   > Esse processo deve ser iniciado em quatro horas, a contar da autorização de um dispositivo StorSimple.
   > 
   > 
   
   Essa nova chave é então enviada ao serviço para ser enviada por push a todos os dispositivos que são registrados no serviço. Um alerta aparecerá no painel de serviço. O serviço desabilitará todas as operações nos dispositivos registrados e o administrador do dispositivo precisará atualizar a chave de criptografia de dados de serviço nos outros dispositivos. No entanto, as E/Ss (hosts que enviam dados à nuvem) não serão interrompidas.
   
   Se você tiver um único dispositivo registrado no serviço, o processo de substituição agora está concluído e a próxima etapa poderá ser ignorada. Se você tiver vários dispositivos registrados em seu serviço, passe para a etapa 3.

### <a name="step-3-update-the-service-data-encryption-key-on-other-storsimple-devices"></a>Etapa 3: Atualizar a chave de criptografia de dados de serviço em outros dispositivos StorSimple
Essas etapas devem ser executadas na interface do Windows PowerShell de seu dispositivo StorSimple, caso você tenha vários dispositivos registrados no serviço StorSimple Manager. A chave que você obteve na Etapa 2 deve ser usada para atualizar todos os demais dispositivos StorSimple registrados com o serviço do StorSimple Manager.

Execute as etapas a seguir para atualizar a criptografia de dados de serviço no seu dispositivo.

#### <a name="to-update-the-service-data-encryption-key-on-physical-devices"></a>Para atualizar a chave de criptografia de dados de serviço em dispositivos físicos
1. Use o Windows PowerShell para StorSimple para se conectar ao console. Selecione a Opção 1 para fazer logon com acesso completo.
2. No prompt de comando, digite: `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Forneça a chave de criptografia de dados de serviço que você obteve na [Etapa 2: Usar o Windows PowerShell para StorSimple para iniciar a alteração da chave de criptografia de dados de serviço](#to-initiate-the-service-data-encryption-key-change).

#### <a name="to-update-the-service-data-encryption-key-on-all-the-80108020-cloud-appliances"></a>Para atualizar a chave de criptografia de dados de serviço em todos os dispositivos de nuvem 8010/8020
1. Baixe e instale o script do PowerShell [Update-CloudApplianceServiceEncryptionKey.ps1](https://github.com/anoobbacker/storsimpledevicemgmttools/blob/master/Update-CloudApplianceServiceEncryptionKey.ps1). 
2. Abra o PowerShell e, no prompt de comando, digite: `Update-CloudApplianceServiceEncryptionKey.ps1 -SubscriptionId [subscription] -TenantId [tenantid] -ResourceGroupName [resource group] -ManagerName [device manager]`

Esse script garantirá que essa chave de criptografia de dados de serviço seja definida em todos os dispositivos de nuvem 8010/8020 no gerenciador de dispositivos.

## <a name="supported-operations-on-devices-running-versions-prior-to-update-50"></a>Suporte para operações em dispositivos que executam versões anteriores à atualização 5.0
No Portal do Azure, há suporte apenas para dispositivos StorSimple que executam a Atualização 5.0 ou superior. Os dispositivos que executam versões mais antigas têm suporte limitado. Após você ter migrado para o Portal do Azure, cheque a tabela a seguir para conferir quais operações têm suporte para dispositivos que executam versões anteriores à Atualização 5.0.

| Operação                                                                                                                       | Com suporte      |
|---------------------------------------------------------------------------------------------------------------------------------|----------------|
| Registrar um dispositivo                                                                                                               | Sim            |
| Definir as configurações do dispositivo, tais como configurações gerais, de rede e de segurança                                                                | Sim            |
| Examinar, baixar e instalar atualizações                                                                                             | Sim            |
| Desativar um dispositivo                                                                                                               | Sim            |
| Excluir um dispositivo                                                                                                                   | Sim            |
| Criar, modificar e excluir um contêiner de volume                                                                                   | Não              |
| Criar, modificar e excluir um volume                                                                                             | Não              |
| Criar, modificar e excluir uma política de backup                                                                                      | Não              |
| Fazer um backup manual                                                                                                            | Não              |
| Realizar um backup agendado                                                                                                         | Não aplicável |
| Restaurar de um conjunto de backup                                                                                                        | Não              |
| Clonar para um dispositivo que executa a Atualização 3.0 e posterior <br> O dispositivo de origem executa uma versão anterior à Atualização 3.0.                                | Sim            |
| Clonar para um dispositivo que executa uma versão anterior à Atualização 3.0                                                                          | Não              |
| Failover como dispositivo de origem <br> (de um dispositivo que executa uma versão anterior à Atualização 3.0 para um dispositivo que executa a Atualização 3.0 e posterior)                                                               | Sim            |
| Failover como dispositivo de destino <br> (para um dispositivo que executa uma versão de software anterior à Atualização 3.0)                                                                                   | Não              |
| Limpar um alerta                                                                                                                  | Sim            |
| Exibir políticas de backup, catálogo de backup, volumes, contêineres de volume, gráficos de monitoramento, trabalhos e alertas criados no portal clássico | Sim            |
| Ativar e desativar controladores de dispositivo                                                                                              | Sim            |


## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre o [processo de implantação do StorSimple](storsimple-8000-deployment-walkthrough-u2.md).
* [Saiba mais sobre como gerenciar sua conta de armazenamento do StorSimple](storsimple-8000-manage-storage-accounts.md).
* Saiba mais sobre como [usar o serviço StorSimple Device Manager para administrar dispositivos StorSimple](storsimple-8000-manager-service-administration.md).
