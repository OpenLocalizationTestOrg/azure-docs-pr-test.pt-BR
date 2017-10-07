---
title: "dispositivo virtual do aaaStorSimple atualização 2 | Microsoft Docs"
description: "Saiba como toocreate, implantar e gerenciar um dispositivo virtual StorSimple em uma rede virtual do Microsoft Azure. (Aplica-se tooStorSimple atualização 2)."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: f37752a5-cd0c-479b-bef2-ac2c724bcc37
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.openlocfilehash: 8d2a0520f1ed30ebec929c2bdabb4838691b8ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-virtual-device-in-azure"></a>Implantar e gerenciar um dispositivo virtual StorSimple no Azure
## <a name="overview"></a>Visão geral
dispositivo virtual Olá da série 8000 StorSimple é um recurso adicional que acompanha a sua solução do Microsoft Azure StorSimple. o dispositivo virtual StorSimple Olá é executado em uma máquina virtual em uma rede virtual do Microsoft Azure, e você pode usá-lo tooback backup e clonar dados de seus hosts. Este tutorial descreve como toodeploy e gerenciar um dispositivo virtual no Azure e é aplicável tooall dispositivos virtuais hello, executando a versão do software de atualização 2 e inferior.

#### <a name="virtual-device-model-comparison"></a>Comparação do modelo de dispositivo virtual
Olá StorSimple dispositivo virtual está disponível em dois modelos, um 8010 padrão (anteriormente conhecido como Olá 1100) e um premium 8020 (introduzido na atualização 2). Uma comparação entre dois modelos de saudação é tabulada abaixo.

| Modelo do dispositivo | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **Capacidade máxima** |30 TB |64 TB |
| **VM do Azure** |Standard_A3 (4 núcleos, 7 GB de memória) |Standard_DS3 (4 núcleos, 14 GB de memória) |
| **Compatibilidade de versão** |Versões com pré-Atualização 2 ou posterior |Versões com Atualização 2 ou posterior |
| **Disponibilidade de região** |Todas as regiões do Azure |Todas as regiões do Azure que dão suporte ao Armazenamento Premium e às VMs DS3 do Azure<br></br> Use [essa lista](https://azure.microsoft.com/en-us/regions/services) toosee se *máquinas virtuais > série DS* e *armazenamento > armazenamento de disco* estão disponíveis em sua região. |
| **Tipo de armazenamento** |Usa o Armazenamento Standard do Azure para discos locais<br></br> Saiba como muito[criar uma conta de armazenamento padrão](../storage/common/storage-create-storage-account.md) |Usa o Armazenamento Premium do Azure para discos locais<sup>2</sup> <br></br>Saiba como muito[criar uma conta de armazenamento Premium](../storage/common/storage-premium-storage.md) |
| **Diretrizes sobre carga de trabalho** |Recuperação no nível de item de arquivos de backups |Cenários de desenvolvimento e teste na nuvem, baixa latência, cargas de trabalho de desempenho mais altas  <br></br>Dispositivo secundário para recuperação de desastre |

<sup>1</sup> *anteriormente conhecido como Olá 1100*.

<sup>2</sup> *ambos Olá 8010 e 8020 usar armazenamento padrão do Azure para Olá nuvem camada. Olá diferença existe apenas na camada de saudação local no dispositivo Olá*.

Este artigo descreve o processo passo a passo de saudação de implantação de um dispositivo virtual StorSimple no Azure. Depois de ler este artigo, você irá:

* Entenda como o dispositivo virtual Olá difere do dispositivo físico hello.
* Ser capaz de toocreate e configurar o dispositivo virtual hello.
* Conecte o dispositivo virtual toohello.
* Saiba como toowork com o dispositivo virtual hello.

Este tutorial aplica tooall Olá dispositivos virtuais StorSimple executar o Update 2 e superior.

## <a name="how-hello-virtual-device-differs-from-hello-physical-device"></a>Como o dispositivo virtual Olá difere do dispositivo físico Olá
o dispositivo virtual StorSimple Olá é uma versão somente de software do StorSimple que é executado em um único nó em uma máquina Virtual Microsoft Azure. Olá dispositivo virtual oferece suporte a cenários recuperação de desastres em que o seu dispositivo físico não está disponível e é adequado para uso em nível de item de recuperação de backups, recuperação de desastres, local e desenvolvimento em nuvem e cenários de teste.

#### <a name="differences-from-hello-physical-device"></a>Diferenças do dispositivo físico Olá
Olá tabela a seguir mostra algumas das principais diferenças entre o dispositivo virtual StorSimple hello e o dispositivo físico StorSimple hello.

|  | Dispositivo físico | Dispositivo virtual |
| --- | --- | --- |
| **Localidade** |Reside no datacenter hello. |É executado no Azure. |
| **Interfaces de rede** |Tem seis interfaces de rede: DATA 0 a DATA 5. |Tem apenas uma interface de rede: DATA 0. |
| **Registro** |Registrado durante a etapa de configuração de saudação. |O registro é uma tarefa separada. |
| **Chave de criptografia de dados do serviço** |Regenerar no dispositivo físico hello e, em seguida, atualizar o dispositivo virtual Olá com uma nova chave de saudação. |Não é possível gerar novamente do dispositivo virtual hello. |

## <a name="prerequisites-for-hello-virtual-device"></a>Pré-requisitos para o dispositivo virtual Olá
Olá seções a seguir explicam os pré-requisitos de configuração de saudação para seu dispositivo virtual StorSimple. Toodeploying anterior um dispositivo virtual, examine Olá [considerações de segurança para usar um dispositivo virtual](storsimple-security.md#storsimple-virtual-device-security).

#### <a name="azure-requirements"></a>Requisitos do Azure
Antes de provisionar dispositivo virtual Olá, é necessário toomake Olá preparações no seu ambiente do Azure a seguir:

* Dispositivo virtual do hello, [configurar uma rede virtual no Azure](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Se usar o Armazenamento Premium, você deve criar uma rede virtual em uma região do Azure que dá suporte ao Armazenamento Premium. regiões de armazenamento Premium Olá são regiões que correspondem a linha toohello para *o armazenamento em disco* na lista de saudação do [serviços do Azure por região](https://azure.microsoft.com/en-us/regions/services).
* É aconselhável toouse saudação padrão DNS servidor fornecida pelo Azure em vez de especificar seu próprio nome de servidor DNS. Se o nome do servidor DNS não é válido ou se servidor DNS de saudação não é capaz de tooresolve endereços IP corretamente, haverá falha na criação de saudação do dispositivo virtual hello.
* Ponto a site e site a site são opcionais, mas não obrigatórios. Se desejar, você pode configurar essas opções para cenários mais avançados.
* Você pode criar [máquinas virtuais do Azure](../virtual-machines/virtual-machines-linux-about.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (servidores de host) na rede virtual Olá pode usar volumes Olá expostos pelo dispositivo virtual hello. Esses servidores devem atender Olá requisitos a seguir:                             

  * Ser VMs do Windows ou do Linux com software Iniciador iSCSI instalado.
  * Estar em execução no hello mesma rede virtual que o dispositivo virtual hello.
  * Ser capaz de tooconnect toohello destino de iSCSI do dispositivo virtual Olá pelo endereço IP interno de saudação do dispositivo virtual hello.
* Verifique se você configurou o suporte para iSCSI e nuvem tráfego em Olá mesmo rede virtual.

#### <a name="storsimple-requirements"></a>Requisitos do StorSimple
Verifique Olá atualizações tooyour Azure StorSimple serviço a seguir antes de criar um dispositivo virtual:

* Adicionar [registros de controle de acesso](storsimple-manage-acrs.md) para Olá VMs que serão toobe servidores de host para seu dispositivo virtual.
* Use um [conta de armazenamento](storsimple-manage-storage-accounts.md#add-a-storage-account) em Olá mesma região que o dispositivo virtual hello. Contas de armazenamento em regiões diferentes podem resultar em baixo desempenho. Você pode usar uma padrão ou Premium conta de armazenamento com o dispositivo virtual hello. Para obter mais informações sobre como toocreate uma [conta de armazenamento Standard](../storage/common/storage-create-storage-account.md) ou um [conta de armazenamento Premium](../storage/common/storage-premium-storage.md)
* Use uma conta de armazenamento diferentes para a criação de dispositivo virtual do hello usada para seus dados. Usando Olá a mesma conta de armazenamento pode resultar em baixo desempenho.

Certifique-se de que você tenha Olá seguintes informações antes de começar:

* Sua conta do portal clássico do Azure com credenciais de acesso.
* Uma cópia da chave de criptografia de dados de serviço de saudação do seu dispositivo físico.

## <a name="create-and-configure-hello-virtual-device"></a>Criar e configurar o dispositivo virtual Olá
Antes de executar esses procedimentos, verifique se você atendeu a saudação [pré-requisitos para o dispositivo virtual Olá](#prerequisites-for-the-virtual-device).

Após ter criado uma rede virtual, configurado um serviço StorSimple Manager e registrado seu dispositivo StorSimple físico no serviço de saudação, você pode usar Olá toocreate as etapas a seguir e configurar um dispositivo virtual StorSimple.

### <a name="step-1-create-a-virtual-device"></a>Etapa 1: criar um dispositivo virtual
Execute Olá dispositivo virtual do StorSimple etapas toocreate Olá a seguir.

[!INCLUDE [Create a virtual device](../../includes/storsimple-create-virtual-device-u2.md)]

Se a criação de saudação do dispositivo virtual Olá falha nesta etapa, você não pode ter toohello de conectividade da Internet. Para obter mais informações, vá muito[solucionar problemas de falhas de conectividade de Internet](#troubleshoot-internet-connectivity-errors) durante a criação de um dispositivo virtual.

### <a name="step-2-configure-and-register-hello-virtual-device"></a>Etapa 2: Configurar e registrar dispositivo virtual Olá
Antes de iniciar este procedimento, certifique-se de que você tenha uma cópia da chave de criptografia de dados de serviço de saudação. Olá chave de criptografia de dados de serviço foi criado quando você configurou seu primeiro dispositivo StorSimple e foram instruções toosave-lo em um local seguro. Se você não tiver uma cópia da chave de criptografia de dados de serviço hello, você deve contatar o Microsoft Support para obter assistência.

Executar Olá tooconfigure as etapas a seguir e registrar seu dispositivo virtual StorSimple.

[!INCLUDE [Configure and register a virtual device](../../includes/storsimple-configure-register-virtual-device.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>Etapa 3: Definições de configuração de dispositivo de saudação modificar (opcional)
Olá, seção a seguir descreve Olá configurações do dispositivo necessárias para o dispositivo virtual StorSimple Olá toouse CHAP, Gerenciador de instantâneos do StorSimple ou alterar a senha de administrador do dispositivo hello.

#### <a name="configure-hello-chap-initiator"></a>Configurar o iniciador do CHAP Olá
Este parâmetro contém as credenciais de saudação que seu dispositivo virtual (destino) espera dos iniciadores de saudação (servidores) que estão tentando tooaccess volumes de saudação. Olá iniciadores fornecerão um nome de usuário e uma tooidentify de senha CHAP próprios tooyour dispositivo durante essa autenticação. Para obter etapas detalhadas, consulte muito[configurar o CHAP para seu dispositivo](storsimple-configure-chap.md#unidirectional-or-one-way-authentication).

#### <a name="configure-hello-chap-target"></a>Configurar CHAP de destino Olá
Este parâmetro contém as credenciais de saudação que seu dispositivo virtual usa quando um iniciador habilitado pelo CHAP solicita a autenticação mútua ou bidirecional. Seu dispositivo virtual usará um nome de usuário e tooidentify senha CHAP invertido próprio toohello iniciador durante esse processo de autenticação. Observe que as configurações de destino de CHAP são configurações globais. Quando elas são aplicadas, todos os Olá volumes conectados toohello dispositivo virtual armazenamento usará a autenticação CHAP. Para obter etapas detalhadas, consulte muito[configurar o CHAP para seu dispositivo](storsimple-configure-chap.md#bidirectional-or-mutual-authentication).

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>Configurar a senha do StorSimple Snapshot Manager Olá
Gerenciador de instantâneos StorSimple software reside no host do Windows e permite que os administradores toomanage backups do seu dispositivo StorSimple na forma de saudação de locais e instantâneos em nuvem.

> [!NOTE]
> Dispositivo virtual do hello, seu host do Windows é uma máquina virtual do Azure.
>
>

Ao configurar um dispositivo em Olá StorSimple Snapshot Manager, você será solicitado tooprovide Olá tooauthenticate de endereço e a senha IP de dispositivo do StorSimple seu dispositivo de armazenamento. Para obter etapas detalhadas, consulte muito[senha configurar Gerenciador de instantâneos do StorSimple](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password).

#### <a name="change-hello-device-administrator-password"></a>Senha de administrador de dispositivo de Olá de alteração
Quando você usar tooaccess de interface do Windows PowerShell Olá Olá dispositivo virtual, será necessário tooenter uma senha de administrador do dispositivo. Para segurança de saudação dos seus dados, você está toochange necessária essa senha antes de dispositivo virtual Olá pode ser usado. Para obter etapas detalhadas, consulte muito[senha de administrador configurar dispositivo](storsimple-change-passwords.md#change-the-device-administrator-password).

## <a name="connect-remotely-toohello-virtual-device"></a>Conectar-se remotamente dispositivo virtual toohello
Dispositivo virtual do tooyour de acesso remoto por meio da interface do Windows PowerShell Olá não está habilitado por padrão. Você precisa tooenable o gerenciamento remoto no dispositivo virtual Olá primeiro e habilitá-lo no cliente de saudação que será usado tooaccess seu dispositivo virtual.

Olá tooconnect de processo de duas etapas remotamente é detalhado abaixo.

### <a name="step-1-configure-remote-management"></a>Etapa 1: configurar o gerenciamento remoto
Execute Olá gerenciamento remoto do etapas tooconfigure para seu dispositivo virtual StorSimple a seguir.

[!INCLUDE [Configure remote management via HTTP for virtual device](../../includes/storsimple-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-virtual-device"></a>Etapa 2: Acessar remotamente o dispositivo virtual Olá
Depois de habilitar o gerenciamento remoto na página de configuração de dispositivo de StorSimple Olá, você pode usar o Windows PowerShell remoting tooconnect toohello dispositivo virtual de outra máquina virtual dentro de saudação mesma rede virtual. Por exemplo, você pode conectar da VM que você usou e tooconnect iSCSI do host de saudação. Na maioria das implantações, você já terá aberto um ponto de extremidade público tooaccess sua VM host que você pode usar para acessar o dispositivo virtual hello.

> [!WARNING]
> **Para maior segurança, é altamente recomendável que você use HTTPS ao se conectar a pontos de extremidade toohello e, em seguida, excluir os pontos de extremidade Olá depois de concluir sua sessão remota do PowerShell.**
>
>

Você deve seguir os procedimentos Olá [conectar-se remotamente o dispositivo StorSimple tooyour](storsimple-remote-connect.md) tooset a conexão remota para seu dispositivo virtual.

## <a name="connect-directly-toohello-virtual-device"></a>Conecte-se diretamente dispositivo virtual toohello
Você também pode conectar diretamente dispositivo virtual toohello. Se você quiser tooconnect diretamente toohello dispositivo virtual em outro computador fora de rede virtual hello ou ambiente de Microsoft Azure Olá externa, você precisa toocreate pontos de extremidade adicionais conforme descrito em Olá procedimento a seguir.

Execute Olá seguindo as etapas toocreate um ponto de extremidade público no dispositivo virtual hello.

[!INCLUDE [Create public endpoints on a virtual device](../../includes/storsimple-create-public-endpoints-virtual-device.md)]

É recomendável que você se conectar de outra máquina virtual dentro Olá mesmo virtual porque essa prática minimiza o número de saudação de pontos de extremidade públicos na sua rede virtual de rede. Quando você usar esse método, você simplesmente se conectar toohello virtual machine através de uma sessão de área de trabalho remota e, em seguida, configure essa máquina virtual para uso como faria com qualquer outro cliente do Windows em uma rede local. Número de porta pública Olá tooappend não é necessário porque a porta Olá já será conhecida.

## <a name="work-with-hello-storsimple-virtual-device"></a>Trabalhar com o dispositivo virtual StorSimple Olá
Agora que você criou e configurou o dispositivo virtual StorSimple hello, você está pronto toostart trabalhar com ele. Você pode trabalhar com contêineres de volume, volumes e políticas de backup em um dispositivo virtual como faria em um dispositivo StorSimple físico; Olá única diferença é que você precisa toomake-se de selecionar o dispositivo virtual Olá na lista de dispositivos. Consulte também[usar Olá StorSimple Manager serviço toomanage um dispositivo virtual](storsimple-manager-service-administration.md) para procedimentos passo a passo de saudação tarefas de gerenciamento de vários para dispositivo virtual hello.

Olá seções a seguir discutem algumas das diferenças de saudação que você encontrará ao trabalhar com o dispositivo virtual hello.

### <a name="maintain-a-storsimple-virtual-device"></a>Manter um dispositivo virtual StorSimple
Como é um dispositivo somente de software, manutenção de dispositivo virtual Olá é mínima quando comparada toomaintenance para dispositivo físico hello. Você tem Olá as opções a seguir:

* **Atualizações de software** – você pode exibir a data de saudação software Olá última atualização, juntamente com quaisquer mensagens de status de atualização. Você pode usar o hello **verificar atualizações** botão na parte inferior de saudação do hello página tooperform uma verificação manual, se você quiser toocheck para novas atualizações. Se houver atualizações disponíveis, clique em **instalar atualizações** tooinstall. Como há apenas uma única interface no dispositivo virtual hello, isso significa que haverá uma pequena interrupção no serviço quando as atualizações são aplicadas. dispositivo virtual Olá será desligar e reiniciar (se necessário) tooapply quaisquer atualizações que foram lançadas. Para um procedimento passo a passo, consulte muito[atualizar seu dispositivo](storsimple-update-device.md#install-regular-updates-via-the-azure-classic-portal).
* **Pacote de suporte** – você pode criar e carregar um pacote de suporte toohelp Microsoft Support solucionar problemas com seu dispositivo virtual. Para um procedimento passo a passo, consulte muito[criar e gerenciar um pacote de suporte](storsimple-create-manage-support-package.md).

### <a name="storage-accounts-for-a-virtual-device"></a>Contas de armazenamento para um dispositivo virtual
Contas de armazenamento são criadas para uso pelo serviço do StorSimple Manager hello, dispositivo virtual hello e dispositivo físico hello. Quando você cria suas contas de armazenamento, recomendamos que você use uma região de identificador na Olá nome amigável toohelp Certifique-se de que região de saudação é consistente em todos os componentes do sistema de saudação do. Para um dispositivo virtual, é importante que todos Olá componentes estar em hello mesmos problemas de desempenho tooprevent de região.

Para um procedimento passo a passo, consulte muito[adicionar uma conta de armazenamento](storsimple-manage-storage-accounts.md#add-a-storage-account).

### <a name="deactivate-a-storsimple-virtual-device"></a>Desativar um dispositivo virtual StorSimple
Desativar um dispositivo virtual exclui hello VM e recursos de saudação criados quando ele foi provisionado. Depois que o dispositivo virtual hello está desativado, ele não pode ser restaurado estado anterior tooits. Antes de desativar o dispositivo virtual hello, certifique-se de que toostop ou exclua os clientes e hosts que dependem dele.

Desativar um dispositivo virtual resulta em Olá ações a seguir:

* dispositivo virtual Olá é removido.
* disco Olá SO e discos de dados criados para o dispositivo virtual Olá são removidos.
* serviço hospedado de saudação e rede virtual criada durante o provisionamento são mantidos. Se você não os estiver usando, deverá excluí-los manualmente.
* Instantâneos de nuvem criados para o dispositivo virtual Olá são mantidos.

Para um procedimento passo a passo, consulte muito[desativar e excluir seu dispositivo StorSimple](storsimple-deactivate-and-delete-device.md).

Assim que o dispositivo virtual Olá é mostrado como desativado na página do serviço StorSimple Manager hello, você pode excluir o dispositivo virtual Olá da lista de dispositivos em Olá **dispositivos** página.

### <a name="start-stop-and-restart-a-virtual-device"></a>Iniciar, parar e reiniciar um dispositivo virtual
Ao contrário do dispositivo físico do StorSimple hello, há sem energia e desligar toopush botão em um dispositivo virtual StorSimple. No entanto, pode haver ocasiões em que você precisa toostop e reiniciar o dispositivo virtual hello. Por exemplo, algumas atualizações podem exigir que Olá que VM ser reiniciado toofinish processo de atualização de saudação. saudação de maneira mais fácil para você toostart, parar e reiniciar um dispositivo virtual é toouse Olá Console de gerenciamento de máquinas virtuais.

Quando você examinar Olá Console de gerenciamento, status do dispositivo virtual Olá é **executando** porque ele é iniciado por padrão, depois que ele é criado. É possível iniciar, parar e reiniciar uma máquina virtual a qualquer momento.

[!INCLUDE [Stop and restart virtual device](../../includes/storsimple-stop-restart-virtual-device.md)]

### <a name="reset-toofactory-defaults"></a>Redefinir padrões toofactory
Se você decidir que você apenas desejar toostart com seu dispositivo virtual, basta desativar e excluí-lo e, em seguida, crie um novo. Assim como quando o dispositivo é reiniciado, o novo dispositivo virtual não terá atualizações instaladas; Portanto, certifique-se de que toocheck atualizações antes de usá-lo.

## <a name="fail-over-toohello-virtual-device"></a>O failover de dispositivo virtual toohello
Recuperação de desastres (DR) é um dos principais cenários de saudação que Olá StorSimple dispositivo virtual foi desenvolvido para. Nesse cenário, Olá dispositivo StorSimple físico ou datacenter inteiro pode não estar disponível. Felizmente, você pode usar as operações toorestore de dispositivo virtual em um local alternativo. Durante a recuperação de desastres, contêineres de volume de saudação do dispositivo de origem de saudação alterar a propriedade e são transferidos toohello de dispositivo virtual. Olá pré-requisitos para DR são que dispositivo virtual Olá foi criado e configurado, todos os volumes de saudação no contêiner de volume Olá foi colocados offline e o contêiner de volume Olá possui um tipo de instantâneo em nuvem.

> [!NOTE]
> * Ao usar um dispositivo virtual como dispositivo secundário Olá para recuperação de desastres, tenha em mente que Olá 8010 tem 30 TB de armazenamento padrão e 8020 tem 64 TB de armazenamento Premium. Olá maior capacidade 8020 dispositivo virtual pode ser mais adequado para um cenário de recuperação de desastres.
> * Não é possível o failover ou clone de um dispositivo executando atualizar 2 dispositivo tooa executando o software de pré-atualização 1. No entanto, você pode fazer failover um dispositivo que executa a atualização 2 tooa dispositivo executando Update 1 (1.1 ou 1.2)
>
>

Para um procedimento passo a passo, consulte muito[dispositivo virtual do failover tooa](storsimple-device-failover-disaster-recovery.md#fail-over-to-a-storsimple-virtual-device).

## <a name="shut-down-or-delete-hello-virtual-device"></a>Desligar ou excluir o dispositivo virtual Olá
Se configurado anteriormente e usado um StorSimple virtual dispositivo mas agora deseja toostop acúmulo de encargos de computação para seu uso, você pode desligar o dispositivo virtual hello. Desligar o dispositivo virtual Olá não exclui o sistema operacional ou discos de dados no armazenamento. Interrompe o encargos de acúmulo de sua assinatura, mas continuarão encargos de armazenamento para Olá SO e discos de dados.

Se você excluir ou desligar o dispositivo virtual hello, ele será exibido como **Offline** na página de dispositivos de saudação do hello serviço StorSimple Manager. Você pode escolher toodeactivate ou excluir dispositivo Olá se também desejar toodelete backups Olá criados pelo dispositivo virtual hello. Para saber mais, confira [Desativar e excluir um dispositivo StorSimple](storsimple-deactivate-and-delete-device.md).

[!INCLUDE [Shut down a virtual device](../../includes/storsimple-shutdown-virtual-device.md)]

[!INCLUDE [Delete a virtual device](../../includes/storsimple-delete-virtual-device.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>Solucionar problemas de erros de conectividade com a Internet
Durante a criação de saudação de um dispositivo virtual, se não houver nenhum toohello de conectividade da Internet, etapa de criação de saudação falhará. tootroubleshoot se falha Olá devido a conectividade com a Internet, executar Olá etapas Olá portal clássico do Azure:

1. Crie uma máquina virtual do Windows Server 2012 no Azure. Esta máquina virtual deve usar Olá a mesma conta de armazenamento, redes e sub-redes usada por seu dispositivo virtual. Se você já tiver um host do Windows Server no Azure usando Olá a mesma conta de armazenamento, redes e sub-redes, você também pode usá-lo conectividade com a Internet tootroubleshoot hello.
2. Log remoto na máquina virtual de saudação criado no hello anterior da etapa.
3. Abra uma janela de comando em máquina virtual de saudação (Win + R e digite `cmd`).
4. Execute Olá cmd prompt Olá a seguir.

    `nslookup windows.net`
5. Se `nslookup` falhar, em seguida, falha de conectividade de Internet está impedindo o dispositivo virtual Olá ao registrar o serviço StorSimple Manager toohello.
6. Faça alterações de Olá necessário tooyour tooensure de rede virtual que Olá dispositivo virtual é capaz de tooaccess sites do Azure, como "windows.net".

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[usar Olá StorSimple Manager serviço toomanage um dispositivo virtual](storsimple-manager-service-administration.md).
* Entender como muito[restaurar de um conjunto de backup de um volume StorSimple](storsimple-restore-from-backup-set.md).
