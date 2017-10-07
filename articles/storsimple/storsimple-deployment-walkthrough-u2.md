---
title: "aaaDeploy seu dispositivo StorSimple (atualização 2) | Microsoft Docs"
description: "Descreve as etapas de saudação e práticas recomendadas para implantar o serviço e dispositivo Olá StorSimple atualização 2."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7dff0612-617b-4fc8-a3fe-994c24bc7c51
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: alkohli
ms.openlocfilehash: 5906cc3c41f03c426905ef91be37852608ae9393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-on-premises-storsimple-device-update-2"></a>Implantar o dispositivo StorSimple local (Atualização 2)
> [!div class="op_single_selector"]
> * [Atualização 2 e posterior ](storsimple-deployment-walkthrough-u2.md)
> * [Atualização 1](storsimple-deployment-walkthrough-u1.md)
> * [Versão de GA](storsimple-deployment-walkthrough.md)
> 
> 

## <a name="overview"></a>Visão geral
Bem-vindo à implantação de dispositivo Azure StorSimple tooMicrosoft. Esses tutoriais de implantação se aplicam a tooStorSimple 8000 Series atualização 2. Esta série de tutoriais inclui uma lista de verificação de configuração, pré-requisitos de configuração e etapas de configuração detalhadas para seu dispositivo StorSimple.

informações Olá esses tutoriais pressupõem que você tiver revisado precauções de segurança Olá e desempacotados, montados em rack e cabeado seu dispositivo StorSimple. Se você ainda precisar tooperform às tarefas, iniciar revisar Olá [precauções de segurança](storsimple-safety.md). Siga as instruções específicas de dispositivo Olá toounpack, montagem em rack e cabeamento do dispositivo.

* [Desembalar, montar em rack e cabear o 8100](storsimple-8100-hardware-installation.md)
* [Desembalar, montar em rack e cabear o 8600](storsimple-8600-hardware-installation.md)

Você precisará de privilégios toocomplete Olá a instalação e configuração do processo de administrador. É recomendável que você examine a lista de verificação de configuração de saudação antes de começar. processo de implantação e configuração de saudação pode levar algum tempo toocomplete.

> [!NOTE]
> Olá StorSimple informações sobre a implantação publicada no site do Microsoft Azure Olá aplica tooStorSimple 8000 series somente para dispositivos. Para obter informações completas sobre os dispositivos da série Olá 7000, vá para: [http://onlinehelp.storsimple.com/](http://onlinehelp.storsimple.com). Para obter informações de implantação de 7000 série, consulte Olá [StorSimple sistema guia de início rápido](http://onlinehelp.storsimple.com/111_Appliance/).
> 
> 

## <a name="deployment-steps"></a>Etapas de implantação.
Executar essas etapas necessárias tooconfigure seu dispositivo StorSimple e conectá-lo tooyour o serviço StorSimple Manager. Além disso, toohello necessárias etapas, há etapas opcionais e talvez seja necessário durante a implantação de saudação de procedimentos. instruções de implantação passo a passo de saudação indicam quando você deve executar cada uma dessas etapas opcionais.

| Etapa | Descrição |
| --- | --- |
| **PRÉ-REQUISITOS** |Será necessário toobe concluída em preparação para implantação de saudação futuros. |
| [Lista de verificação da configuração da implantação](#deployment-configuration-checklist) |Use esta lista de verificação toogather e registrar informações anterior tooand durante a implantação de saudação. |
| [Pré-requisitos de implantação](#deployment-prerequisites) |Esses validar Olá ambiente está preparado para implantação. |
|  | |
| **IMPLANTAÇÃO PASSO A PASSO** |Essas etapas é necessária toodeploy seu dispositivo StorSimple na produção. |
| [Etapa 1: Criar um novo serviço](#step-1-create-a-new-service) |Configure o armazenamento e o gerenciamento de nuvem para o dispositivo StorSimple. *Ignore esta etapa se você tem um serviço existente para outros dispositivos StorSimple*. |
| [Etapa 2: Obter a chave de registro de serviço Olá](#step-2-get-the-service-registration-key) |Use esta chave tooregister & conectar seu dispositivo StorSimple com o serviço de gerenciamento de saudação. |
| [Etapa 3: Configurar e registrar dispositivo Olá por meio do Windows PowerShell para StorSimple](#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple) |Conectar a rede de tooyour dispositivo hello e registrá-lo com a instalação de saudação toocomplete do Azure usando o serviço de gerenciamento de saudação. |
| [Etapa 4: Concluir a instalação mínima do dispositivo](#step-4-complete-minimum-device-setup)</br>[Opcional: atualizar o dispositivo StorSimple](#scan-for-and-apply-updates) |Usar configuração de dispositivo de Olá Olá gerenciamento serviço toocomplete e habilitá-lo tooprovide armazenamento. |
| [Etapa 5: Criar um contêiner de volume](#step-5-create-a-volume-container) |Crie um contêiner de volumes tooprovision. Um contêiner de volume tem a conta de armazenamento, largura de banda e configurações de criptografia para todos os volumes de saudação contidos nele. |
| [Etapa 6: Criar um volume](#step-6-create-a-volume) |Provisionar o volume de armazenamento no dispositivo do StorSimple Olá para seus servidores. |
| [Etapa 7: Montar, inicializar e formatar um volume](#step-7-mount-initialize-and-format-a-volume)</br>[Opcional: configurar o MPIO](storsimple-configure-mpio-windows-server.md) |Conecte-se o armazenamento de iSCSI toohello servidores fornecido pelo dispositivo de saudação. Opcionalmente, configure o MPIO tooensure que seus servidores podem tolerar a falha de link, rede e da interface. |
| [Etapa 8: Fazer um backup](#step-8-take-a-backup) |Configurar a política de backup tooprotect seus dados |
|  | |
| **OUTROS PROCEDIMENTOS** |Talvez seja necessário procedimentos de toothese toorefer como implantar sua solução. |
| [Configurar uma nova conta de armazenamento para o serviço de saudação](#configure-a-new-storage-account-for-the-service) | |
| [Use o console serial do dispositivo PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console) | |
| [Obter Olá IQN de um host do Windows Server](#get-the-iqn-of-a-windows-server-host) | |
| [Criar um backup manual](#create-a-manual-backup) | |

## <a name="deployment-configuration-checklist"></a>Lista de verificação da configuração da implantação
Antes de implantar seu dispositivo, você precisará de software toocollect informações tooconfigure Olá em seu dispositivo StorSimple. Preparar algumas dessas informações antecipadamente ajudará a simplificar o processo de saudação do dispositivo do StorSimple Olá em seu ambiente de implantação. Baixe e use toonote esta lista de verificação para baixo de detalhes de configuração de saudação durante a implantação do seu dispositivo.

* [Baixar lista de verificação da configuração de implantação do StorSimple](http://www.microsoft.com/download/details.aspx?id=49159)

## <a name="deployment-prerequisites"></a>Pré-requisitos de implantação
Olá seções a seguir explica os pré-requisitos de configuração de saudação para seu serviço StorSimple Manager e o dispositivo StorSimple.

### <a name="for-hello-storsimple-manager-service"></a>Para Olá serviço StorSimple Manager
Antes de começar, verifique se:

* Você tem sua conta da Microsoft com credenciais de acesso.
* Você tem sua conta de armazenamento do Microsoft Azure com credenciais de acesso.
* Sua assinatura do Microsoft Azure está habilitada para Olá serviço StorSimple Manager. Sua assinatura deve ser adquirida por meio de saudação [Enterprise Agreement](https://azure.microsoft.com/pricing/enterprise-agreement/).
* Você tem o software de emulação de tooterminal acesso como PuTTY.

### <a name="for-hello-device-in-hello-datacenter"></a>Dispositivo Olá Olá datacenter
Antes de configurar o dispositivo hello, certifique-se de que o dispositivo está totalmente desempacotado, montado em um rack e totalmente cabeado para energia, rede e acesso serial conforme descrito em:

* [Desembalar, montar em rack e cabear o dispositivo 8100](storsimple-8100-hardware-installation.md)
* [Desembalar, montar em rack e cabear o dispositivo 8600](storsimple-8600-hardware-installation.md)

### <a name="for-hello-network-in-hello-datacenter"></a>Para a rede Olá Olá Datacenter
Antes de começar, verifique se:

* Olá portas no firewall datacenter são tooallow aberto para o tráfego iSCSI e nuvem conforme descrito em [requisitos de rede para seu dispositivo StorSimple](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device).

## <a name="step-by-step-deployment"></a>IMPLANTAÇÃO PASSO A PASSO
Use Olá seguindo as instruções passo a passo toodeploy seu dispositivo StorSimple no datacenter hello.

## <a name="step-1-create-a-new-service"></a>Etapa 1: Criar um novo serviço
Um serviço StorSimple Manager pode gerenciar vários dispositivos StorSimple. Execute Olá etapas toocreate uma nova instância do serviço do StorSimple Manager Olá a seguir.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

> [!IMPORTANT]
> Se você não tiver habilitado a criação automática de saudação de uma conta de armazenamento com seu serviço, você precisará toocreate pelo menos uma conta de armazenamento depois que você criou com êxito um serviço. Esta conta de armazenamento será usada quando você criar um contêiner de volume. 
> 
> * Se você não criou uma conta de armazenamento automaticamente, vá muito[configurar uma nova conta de armazenamento para o serviço de saudação](#configure-a-new-storage-account-for-the-service) para obter instruções detalhadas. 
> * Se você tiver habilitado a criação automática de uma conta de armazenamento hello, vá muito[etapa 2: chave de registro de serviço Get hello](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Etapa 2: Obter a chave de registro de serviço Olá
Depois de saudação serviço StorSimple Manager está em execução, você precisará chave de registro tooget Olá. Essa chave é usada tooregister e conectar seu dispositivo StorSimple com o serviço de saudação.

Execute Olá seguindo as etapas no Portal de gerenciamento de saudação.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

## <a name="step-3-configure-and-register-hello-device-through-windows-powershell-for-storsimple"></a>Etapa 3: Configurar e registrar dispositivo Olá por meio do Windows PowerShell para StorSimple
Use o Windows PowerShell para StorSimple toocomplete Olá a configuração inicial do seu dispositivo StorSimple conforme explicado em Olá procedimento a seguir. Você precisará toocomplete de software de emulação de terminal toouse nesta etapa. Para obter mais informações, consulte [console serial do dispositivo Use PuTTY tooconnect toohello](#use-putty-to-connect-to-the-device-serial-console).

[!INCLUDE [storsimple-configure-and-register-device-u1](../../includes/storsimple-configure-and-register-device-u1.md)]

## <a name="step-4-complete-minimum-device-setup"></a>Etapa 4: Concluir a instalação mínima do dispositivo
Para a configuração mínima do dispositivo de saudação do seu dispositivo StorSimple, é necessário: 

* Configure o servidor DNS secundário de saudação.
* Habilitar o iSCSI em pelo menos uma interface de rede.
* Atribua endereços IP fixos tooboth controladores de saudação.

Execute Olá seguindo as etapas da instalação do hello Portal de gerenciamento toocomplete Olá mínima do dispositivo.

[!INCLUDE [storsimple-complete-minimum-device-setup](../../includes/storsimple-complete-minimum-device-setup-u1.md)]

## <a name="step-5-create-a-volume-container"></a>Etapa 5: Criar um contêiner de volume
Um contêiner de volume tem a conta de armazenamento, largura de banda e configurações de criptografia para todos os volumes de saudação contidos nele. Você precisará toocreate um contêiner de volume antes de começar a provisionar volumes no seu dispositivo StorSimple. 

Execute Olá seguindo as etapas no Portal de gerenciamento de saudação toocreate um contêiner de volume.

[!INCLUDE [storsimple-create-volume-container](../../includes/storsimple-create-volume-container.md)]

## <a name="step-6-create-a-volume"></a>Etapa 6: Criar um volume
Depois de criar um contêiner de volume, você pode provisionar um volume de armazenamento no dispositivo do StorSimple Olá para seus servidores. Execute Olá seguindo as etapas no Portal de gerenciamento de saudação toocreate um volume.

> [!IMPORTANT]
> O StorSimple Manager pode criar apenas volumes pequenos e totalmente provisionados. No entanto, não é possível criar volumes parcialmente provisionados. 
> 
> 

[!INCLUDE [storsimple-create-volume](../../includes/storsimple-create-volume-u2.md)]

## <a name="step-7-mount-initialize-and-format-a-volume"></a>Etapa 7: Montar, inicializar e formatar um volume
Olá, as etapas a seguir é executada no host do Windows Server. 

> [!IMPORTANT]
> * Para alta disponibilidade da sua solução StorSimple hello, recomendamos que você configure o MPIO em seu iSCSI de tooconfiguring anteriores de servidores (opcional) do host. Configuração do MPIO nos servidores host garantirá que os servidores de saudação podem tolerar um link, rede ou falhas de interface.
> * Para iSCSI e MPIO configuração instruções de instalação e no host do Windows Server, vá muito[configurar MPIO para seu dispositivo StorSimple](storsimple-configure-mpio-windows-server.md). Eles também serão incluem hello etapas toomount, inicializar e formatar volumes do StorSimple.
> * Para iSCSI e MPIO instalação e configuração de instruções em um host Linux, vá muito[configurar MPIO para o host do StorSimple Linux](storsimple-configure-mpio-on-linux.md)
> 
> 

Se você decidir não tooconfigure MPIO, executar Olá toomount as etapas a seguir, inicializar e formatar seus volumes do StorSimple em um host do Windows Server.

[!INCLUDE [storsimple-mount-initialize-format-volume](../../includes/storsimple-mount-initialize-format-volume.md)]

## <a name="step-8-take-a-backup"></a>Etapa 8: Fazer um backup
Backups oferecem proteção pontual de volumes e melhoram a capacidade de recuperação, minimizando os tempos de restauração. Você pode executar dois tipos de backup em seu dispositivo StorSimple: instantâneos locais e instantâneos em nuvem. Cada um desses tipos de backup pode ser **Agendado** ou **Manual**. 

Execute Olá seguindo as etapas no Portal de gerenciamento de saudação toocreate um backup agendado.

[!INCLUDE [storsimple-take-backup](../../includes/storsimple-take-backup.md)]

Você pode fazer um backup manual a qualquer momento. Para procedimentos, vá muito[criar um backup manual](#create-a-manual-backup). 

## <a name="configure-a-new-storage-account-for-hello-service"></a>Configurar uma nova conta de armazenamento para o serviço de saudação
Isso é uma etapa opcional que você precisa tooperform somente se você não tiver habilitado a criação automática de saudação de uma conta de armazenamento com seu serviço. Uma conta de armazenamento do Microsoft Azure é necessário toocreate um contêiner de volume StorSimple.

Se você precisar de uma conta de armazenamento do Azure em uma região diferente de toocreate, consulte [sobre contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md) para obter instruções passo a passo.

Executar Olá etapas Olá Portal de gerenciamento em Olá **o serviço StorSimple Manager** página.

[!INCLUDE [storsimple-configure-new-storage-account-u1](../../includes/storsimple-configure-new-storage-account-u1.md)]

## <a name="use-putty-tooconnect-toohello-device-serial-console"></a>Use o console serial do dispositivo PuTTY tooconnect toohello
tooconnect tooWindows PowerShell para StorSimple, você precisa toouse software de emulação de terminal como PuTTY. Você pode usar PuTTY ao acessar o dispositivo Olá diretamente através do console serial hello ou abrindo uma sessão telnet de um computador remoto.

[!INCLUDE [Use PuTTY tooconnect toohello device serial console](../../includes/storsimple-use-putty.md)]

## <a name="scan-for-and-apply-updates"></a>Verificar e aplicar atualizações
Atualizar seu dispositivo pode demorar várias horas. Executar Olá tooscan etapas para a seguir e aplique as atualizações em seu dispositivo.
<!--can take 1-4 hours--> 

<!--If you have a gateway configured on a network interface other than Data 0, you will need toodisable Data 2 and Data 3 network interfaces before installing hello update. Go too**Devices > Configure** and disable Data 2 and Data 3 interfaces. You should re-enable these interfaces after hello device is updated.-->

#### <a name="tooupdate-your-device"></a>tooupdate seu dispositivo
1. No dispositivo Olá **início rápido** , clique em **dispositivos**. Selecione o dispositivo físico hello, clique em **manutenção** e, em seguida, clique em **verificar atualizações**.  
2. É criado um tooscan de trabalho atualizações disponíveis. Se houver atualizações disponíveis, Olá **verificar atualizações** muda muito**instalar atualizações de**. Clique em **Instalar Atualizações**. 
3. Será criado um trabalho de atualização. Monitorar o status de saudação de sua atualização navegando muito**trabalhos**.
   
   > [!NOTE]
   > Quando o trabalho de atualização de saudação é iniciado, ele imediatamente exibe status Olá como 50 por cento. Olá status se altera too100% somente depois Olá atualização trabalho seja concluído. Não há nenhum status em tempo real para o processo de atualização de saudação.
   > 
   > 
4. Depois de dispositivo Olá foi atualizado com êxito, habilite as interfaces de rede Data 2 e Data 3 se eles foram desabilitados.

<!-- In step 2, you may be requested toodisable Data 2 and Data 3 prior tooinstalling hello updates. You must disable these network interfaces or hello updates may fail.-->

## <a name="get-hello-iqn-of-a-windows-server-host"></a>Obter Olá IQN de um host do Windows Server
Executar Olá seguindo as etapas tooget Olá iSCSI IQN (nome qualificado) de um host do Windows que está executando o Windows Server® 2012.

[!INCLUDE [Create a manual backup](../../includes/storsimple-get-iqn.md)]

## <a name="create-a-manual-backup"></a>Criar um backup manual
Execute Olá seguindo as etapas no Portal de gerenciamento Olá backup manual de toocreate uma sob demanda para um único volume em seu dispositivo StorSimple.

[!INCLUDE [Create a manual backup](../../includes/storsimple-create-manual-backup.md)]

## <a name="next-steps"></a>Próximas etapas
* Configurar um [dispositivo virtual](storsimple-virtual-device-u2.md).
* Saudação de uso [o serviço StorSimple Manager](storsimple-manager-service-administration.md) toomanage seu dispositivo StorSimple.

