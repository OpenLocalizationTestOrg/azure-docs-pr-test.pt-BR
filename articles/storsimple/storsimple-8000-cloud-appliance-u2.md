---
title: "aaaStorSimple nuvem Appliance atualização 3 | Microsoft Docs"
description: "Saiba como toocreate, implantar e gerenciar um dispositivo StorSimple de nuvem em uma rede virtual do Microsoft Azure. (Aplica-se tooStorSimple atualização 3 e posterior)."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/10/2017
ms.author: alkohli
ms.openlocfilehash: ba60a629f1f4b8f0d4566eeb45bae8696f50d0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-a-storsimple-cloud-appliance-in-azure-update-3-and-later"></a>Como implantar e gerenciar um Dispositivo de Nuvem StorSimple no Azure (Atualização 3 e posteriores)

## <a name="overview"></a>Visão geral

Olá StorSimple 8000 Series Appliance de nuvem é um recurso adicional que acompanha a sua solução do Microsoft Azure StorSimple. Olá StorSimple Appliance de nuvem é executado em uma máquina virtual em uma rede virtual do Microsoft Azure, e você pode usá-lo tooback backup e clonar dados de seus hosts.

Este artigo descreve Olá processo passo a passo toodeploy e gerenciar um dispositivo StorSimple de nuvem no Azure. Depois de ler este artigo, você irá:

* Entenda como dispositivo de nuvem Olá difere do dispositivo físico hello.
* Ser capaz de toocreate e configurar o dispositivo de nuvem hello.
* Conecte-se o dispositivo de nuvem toohello.
* Saiba como toowork com hello nuvem de dispositivo.

Este tutorial se aplica a saudação tooall StorSimple soluções de nuvem que executa a atualização 3 e posterior.

#### <a name="cloud-appliance-model-comparison"></a>Comparação de modelo do dispositivo de nuvem

Olá StorSimple Appliance de nuvem está disponível em dois modelos, um 8010 padrão (anteriormente conhecido como Olá 1100) e um premium 8020 (introduzido na atualização 2). Olá, a tabela a seguir apresenta uma comparação dos dois modelos de saudação.

| Modelo do dispositivo | 8010<sup>1</sup> | 8020 |
| --- | --- | --- |
| **Capacidade máxima** |30 TB |64 TB |
| **VM do Azure** |Standard_A3 (4 núcleos, 7 GB de memória)| Standard_DS3 (4 núcleos, 14 GB de memória)|
| **Disponibilidade de região** |Todas as regiões do Azure |Regiões do Azure que dão suporte ao Armazenamento Premium e às VMs DS3 do Azure<br></br>Use [essa lista](https://azure.microsoft.com/regions/services/) toosee se **máquinas virtuais > série DS** e **armazenamento > armazenamento de disco** estão disponíveis em sua região. |
| **Tipo de armazenamento** |Usa o Armazenamento Standard do Azure para discos locais<br></br> Saiba como muito[criar uma conta de armazenamento padrão](../storage/common/storage-create-storage-account.md) |Usa o Armazenamento Premium do Azure para discos locais<sup>2</sup> <br></br>Saiba como muito[criar uma conta de armazenamento Premium](../storage/common/storage-premium-storage.md) |
| **Diretrizes sobre carga de trabalho** |Recuperação no nível de item de arquivos de backups |Cenários de desenvolvimento e teste de nuvem <br></br>Baixa latência e cargas de trabalho com alto desempenho<br></br>Dispositivo secundário para recuperação de desastre |

<sup>1</sup> *anteriormente conhecido como Olá 1100*.

<sup>2</sup> *ambos Olá 8010 e 8020 usar armazenamento padrão do Azure para Olá nuvem camada. Olá diferença existe apenas na camada de saudação local no dispositivo Olá*.

## <a name="how-hello-cloud-appliance-differs-from-hello-physical-device"></a>Como solução de nuvem Olá difere do dispositivo físico Olá

Olá StorSimple Appliance de nuvem é uma versão somente de software do StorSimple que é executado em um único nó em uma máquina Virtual Microsoft Azure. dispositivo de saudação de nuvem oferece suporte a cenários de recuperação de desastres em que seu dispositivo físico não está disponível. dispositivo de nuvem Olá é apropriado para uso em nível de item de recuperação de backups, recuperação de desastres locais e cenários de desenvolvimento e teste de nuvem.

#### <a name="differences-from-hello-physical-device"></a>Diferenças do dispositivo físico Olá

Olá tabela a seguir mostra algumas das principais diferenças entre hello StorSimple Appliance de nuvem e o dispositivo físico StorSimple hello.

|  | Dispositivo físico | Dispositivo de nuvem |
| --- | --- | --- |
| **Localidade** |Reside no datacenter hello. |É executado no Azure. |
| **Interfaces de rede** |Tem seis interfaces de rede: DATA 0 a DATA 5. |Tem apenas uma interface de rede: DATA 0. |
| **Registro** |Registrado durante a etapa de configuração inicial de saudação. |O registro é uma tarefa separada. |
| **Chave de criptografia de dados do serviço** |Regenerar no dispositivo físico hello e atualizar dispositivo de saudação de nuvem com uma nova chave de saudação. |Não é possível regenerar do dispositivo de saudação de nuvem. |
| **Tipos de volume com suporte** |Dá suporte aos volumes fixados localmente e em camadas. |Oferece suporte apenas a volumes em camadas. |

## <a name="prerequisites-for-hello-cloud-appliance"></a>Pré-requisitos para o dispositivo de saudação de nuvem

Olá seções a seguir explica os pré-requisitos de configuração Olá para o seu dispositivo de nuvem do StorSimple. Antes de implantar uma solução de nuvem, examine as considerações de segurança Olá para usar um dispositivo de nuvem.

[!INCLUDE [StorSimple Cloud Appliance security](../../includes/storsimple-8000-cloud-appliance-security.md)]

#### <a name="azure-requirements"></a>Requisitos do Azure

Antes de provisionar o dispositivo de saudação de nuvem, você precisa Olá toomake preparações no seu ambiente do Azure a seguir:

* Verifique se você tem um dispositivo físico StorSimple série 8000 (modelo 8100 ou 8600) implantado e em execução no seu datacenter. Registrar este dispositivo com hello mesmo serviço de Gerenciador de dispositivos do StorSimple que você pretenda toocreate um StorSimple Appliance de nuvem para.
* Para solução de nuvem hello, [configurar uma rede virtual no Azure](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). Se usar o Armazenamento Premium, você deve criar uma rede virtual em uma região do Azure que dá suporte ao Armazenamento Premium. regiões de armazenamento Premium Olá são regiões que correspondem a linha toohello para armazenamento em disco no hello [lista de serviços do Azure por região](https://azure.microsoft.com/regions/services/).
* É recomendável que você use saudação padrão DNS servidor fornecida pelo Azure em vez de especificar seu próprio nome de servidor DNS. Se o nome do servidor DNS não é válido ou se servidor DNS de saudação não é capaz de tooresolve endereços IP corretamente, a criação de saudação do dispositivo de nuvem Olá falha.
* Ponto a site e site a site são opcionais, mas não obrigatórios. Se desejar, você pode configurar essas opções para cenários mais avançados.
* Você pode criar [máquinas virtuais do Azure](../virtual-machines/virtual-machines-windows-quick-create-portal.md) (servidores de host) na rede virtual Olá pode usar volumes Olá expostos pelo dispositivo de saudação de nuvem. Esses servidores devem atender Olá requisitos a seguir:

  * Ser VMs do Windows ou do Linux com software Iniciador iSCSI instalado.
  * Estar em execução no hello mesma rede virtual que o dispositivo de saudação de nuvem.
  * Ser capaz de tooconnect toohello iSCSI destino do dispositivo de nuvem Olá por meio do endereço IP interno de saudação do dispositivo de saudação de nuvem.
  * Verifique se você configurou o suporte para iSCSI e nuvem tráfego em Olá mesmo rede virtual.

#### <a name="storsimple-requirements"></a>Requisitos do StorSimple

Verifique Olá após o serviço de Gerenciador de dispositivos de StorSimple tooyour atualizações antes de criar um dispositivo de nuvem:

* Adicionar [registros de controle de acesso](storsimple-8000-manage-acrs.md) para VMs de saudação que são servidores de host de saudação contínuo toobe para sua solução de nuvem.
* Use um [conta de armazenamento](storsimple-8000-manage-storage-accounts.md#add-a-storage-account) em Olá mesma região que o dispositivo de saudação de nuvem. Contas de armazenamento em regiões diferentes podem resultar em baixo desempenho. Você pode usar uma padrão ou Premium conta de armazenamento com o dispositivo de saudação de nuvem. Para obter mais informações sobre como toocreate uma [conta de armazenamento Standard](../storage/common/storage-create-storage-account.md) ou um [conta de armazenamento Premium](../storage/common/storage-premium-storage.md)
* Use uma conta de armazenamento diferentes para a criação de dispositivo de nuvem de saudação usada para seus dados. Usando Olá a mesma conta de armazenamento pode resultar em baixo desempenho.

Certifique-se de que você tenha Olá seguintes informações antes de começar:

* Sua conta do portal do Azure com credenciais de acesso.
* Uma cópia da chave de criptografia de dados de serviço de saudação do seu dispositivo físico registrado toohello serviço de Gerenciador de dispositivos do StorSimple.

## <a name="create-and-configure-hello-cloud-appliance"></a>Criar e configurar o dispositivo de saudação de nuvem

Antes de executar esses procedimentos, verifique se você atendeu a saudação [pré-requisitos para o dispositivo de nuvem Olá](#prerequisites-for-the-cloud-appliance).

Execute Olá seguindo as etapas toocreate um dispositivo StorSimple de nuvem.

### <a name="step-1-create-a-cloud-appliance"></a>Etapa 1: criação do dispositivo de nuvem

Execute Olá seguindo as etapas toocreate Olá StorSimple Appliance de nuvem.

[!INCLUDE [Create a cloud appliance](../../includes/storsimple-8000-create-cloud-appliance-u2.md)]

Se a criação de saudação do dispositivo de nuvem Olá falha nesta etapa, você não pode ter toohello de conectividade da Internet. Para obter mais informações, vá muito[solucionar problemas de falhas de conectividade de Internet](#troubleshoot-internet-connectivity-errors) durante a criação de um dispositivo de nuvem.

### <a name="step-2-configure-and-register-hello-cloud-appliance"></a>Etapa 2: Configurar e registrar o dispositivo de saudação de nuvem

Antes de iniciar este procedimento, certifique-se de que você tenha uma cópia da chave de criptografia de dados de serviço de saudação. chave de criptografia de dados de serviço de saudação é criado quando você registrou seu dispositivo físico do StorSimple primeiro com hello serviço do Gerenciador de dispositivos do StorSimple. Foram toosave instruções-lo em um local seguro. Se você não tiver uma cópia da chave de criptografia de dados de serviço hello, você deve contatar o Microsoft Support para obter assistência.

Executar Olá tooconfigure as etapas a seguir e registrar seu dispositivo de nuvem do StorSimple.

[!INCLUDE [Configure and register a cloud appliance](../../includes/storsimple-8000-configure-register-cloud-appliance.md)]

### <a name="step-3-optional-modify-hello-device-configuration-settings"></a>Etapa 3: Definições de configuração de dispositivo de saudação modificar (opcional)

Hello, seção a seguir descreve Olá definições de configuração de dispositivo necessárias para Olá StorSimple Appliance de nuvem se desejar toouse CHAP, Gerenciador de instantâneos do StorSimple ou alterar a senha de administrador do dispositivo hello.

#### <a name="configure-hello-chap-initiator"></a>Configurar o iniciador do CHAP Olá

Este parâmetro contém as credenciais de saudação que sua solução de nuvem (destino) espera dos iniciadores de saudação (servidores) que estão tentando tooaccess volumes de saudação. iniciadores de saudação fornecem um nome de usuário e uma tooidentify de senha CHAP próprios tooyour dispositivo durante essa autenticação. Para obter etapas detalhadas, consulte muito[configurar o CHAP para seu dispositivo](storsimple-8000-configure-chap.md#unidirectional-or-one-way-authentication).

#### <a name="configure-hello-chap-target"></a>Configurar CHAP de destino Olá

Este parâmetro contém as credenciais de saudação que sua solução de nuvem usa quando um iniciador habilitado pelo CHAP solicita a autenticação mútua ou bidirecional. Seu dispositivo de nuvem usa um nome de usuário e tooidentify senha CHAP invertido próprio toohello iniciador durante esse processo de autenticação.

> [!NOTE]
> Observe que as configurações de destino de CHAP são configurações globais. Quando essas configurações são aplicadas, todos os volumes de saudação conectada autenticação de CHAP toohello nuvem dispositivo use.

Para obter etapas detalhadas, consulte muito[configurar o CHAP para seu dispositivo](storsimple-8000-configure-chap.md#bidirectional-or-mutual-authentication).

#### <a name="configure-hello-storsimple-snapshot-manager-password"></a>Configurar a senha do StorSimple Snapshot Manager Olá

Gerenciador de instantâneos StorSimple software reside no host do Windows e permite que os administradores toomanage backups do seu dispositivo StorSimple na forma de saudação de locais e instantâneos em nuvem.

> [!NOTE]
> Para solução de nuvem hello, seu host do Windows é uma máquina virtual do Azure.

Ao configurar um dispositivo em Olá StorSimple Snapshot Manager, você será solicitado tooprovide Olá tooauthenticate de endereço e a senha IP de dispositivo do StorSimple seu dispositivo de armazenamento. Para obter etapas detalhadas, consulte muito[senha configurar Gerenciador de instantâneos do StorSimple](storsimple-8000-change-passwords.md#set-the-storsimple-snapshot-manager-password).

#### <a name="change-hello-device-administrator-password"></a>Senha de administrador de dispositivo de Olá de alteração

Quando você usar tooaccess de interface do Windows PowerShell Olá Olá appliance de nuvem, você estará tooenter necessária uma senha de administrador do dispositivo. Para segurança de saudação dos seus dados, você deve alterar essa senha antes do dispositivo de nuvem Olá pode ser usado. Para obter etapas detalhadas, consulte muito[senha de administrador configurar dispositivo](../storsimple/storsimple-8000-change-passwords.md#change-the-device-administrator-password).

## <a name="connect-remotely-toohello-cloud-appliance"></a>Conectar-se remotamente o dispositivo de nuvem toohello

Dispositivo de nuvem tooyour acesso remoto por meio da interface do Windows PowerShell Olá não está habilitado por padrão. Você deve habilitar o gerenciamento remoto no dispositivo de nuvem Olá primeiro e, em seguida, em Olá cliente usado appliance de nuvem tooaccess hello.

Olá procedimento de duas etapas a seguir descreve como tooconnect remotamente tooyour nuvem appliance.

### <a name="step-1-configure-remote-management"></a>Etapa 1: configurar o gerenciamento remoto

Execute Olá seguindo o gerenciamento remoto do tooconfigure etapas para o seu dispositivo de nuvem do StorSimple.

[!INCLUDE [Configure remote management via HTTP for cloud appliance](../../includes/storsimple-8000-configure-remote-management-http-device.md)]

### <a name="step-2-remotely-access-hello-cloud-appliance"></a>Etapa 2: Acessar remotamente o dispositivo de saudação de nuvem

Depois de habilitar o gerenciamento remoto em um dispositivo de nuvem hello, usar o dispositivo do Windows PowerShell remoting tooconnect toohello de outra máquina virtual dentro de saudação mesma rede virtual. Por exemplo, você pode conectar da VM que você usou e tooconnect iSCSI do host de saudação. Na maioria das implantações, você abrirá um ponto de extremidade público tooaccess sua VM host que você pode usar para acessar o dispositivo de saudação de nuvem.

> [!WARNING]
> **Para maior segurança, é altamente recomendável que você use HTTPS ao se conectar a pontos de extremidade toohello e, em seguida, excluir os pontos de extremidade Olá depois de concluir sua sessão remota do PowerShell.**

Você deve seguir os procedimentos Olá [conectar-se remotamente o dispositivo StorSimple tooyour](storsimple-8000-remote-connect.md) tooset a conexão remota para sua solução de nuvem.

## <a name="connect-directly-toohello-cloud-appliance"></a>Conecte-se diretamente toohello appliance de nuvem

Você também pode conectar diretamente toohello appliance de nuvem. tooconnect diretamente o dispositivo de outro computador fora de nuvem toohello Olá rede virtual ou o ambiente do Microsoft Azure Olá externa, você deve criar pontos de extremidade adicionais.

Execute Olá etapas toocreate um ponto de extremidade público no dispositivo de nuvem Olá a seguir.

[!INCLUDE [Create public endpoints on a cloud appliance](../../includes/storsimple-8000-create-public-endpoints-cloud-appliance.md)]

É recomendável que você se conectar de outra máquina virtual dentro Olá mesmo virtual porque essa prática minimiza o número de saudação de pontos de extremidade públicos na sua rede virtual de rede. Nesse caso, conecte-se a máquina virtual de toohello através de uma sessão de área de trabalho remota e, em seguida, configure essa máquina virtual para uso como faria com qualquer outro cliente do Windows em uma rede local. Número de porta pública Olá tooappend não é necessário porque a porta Olá já é conhecida.

## <a name="work-with-hello-storsimple-cloud-appliance"></a>Trabalhar com hello StorSimple Appliance de nuvem

Agora que você criou e configurou Olá StorSimple Appliance de nuvem, você está pronto toostart trabalhar com ele. Você pode trabalhar com contêineres de volume, volumes e políticas de backup em um dispositivo de nuvem como faria em um dispositivo StorSimple físico. Olá única diferença é que você precisa toomake-se de selecionar o dispositivo de saudação de nuvem na lista de dispositivos. Consulte muito[usar toomanage de serviço de Gerenciador de dispositivos de StorSimple Olá um dispositivo de nuvem](storsimple-8000-manager-service-administration.md) para procedimentos passo a passo de hello tarefas de gerenciamento de vários para dispositivo de saudação de nuvem.

Olá seções a seguir discutem algumas das diferenças de saudação encontrados ao trabalhar com o dispositivo de saudação de nuvem.

### <a name="maintain-a-storsimple-cloud-appliance"></a>Manutenção de um Dispositivo de nuvem StorSimple

Porque ele é um dispositivo somente de software, manutenção de dispositivo de nuvem Olá é mínima quando comparada toomaintenance para dispositivo físico hello.

Você não pode atualizar um dispositivo de nuvem. Use a versão mais recente de saudação do software toocreate um novo dispositivo de nuvem.


### <a name="storage-accounts-for-a-cloud-appliance"></a>Contas de armazenamento para um dispositivo de nuvem

Contas de armazenamento são criadas para uso por Olá serviço do Gerenciador de dispositivos de StorSimple, pelo dispositivo de saudação de nuvem e pelo dispositivo físico hello. Quando você cria suas contas de armazenamento, recomendamos que você use um identificador de região no nome amigável da saudação. Isso ajuda a garantir que região de saudação é consistente em todos os componentes do sistema de saudação do. Para um dispositivo de nuvem, é importante que todos os componentes de saudação estão em hello mesmos problemas de desempenho tooprevent de região.

Para um procedimento passo a passo, consulte muito[adicionar uma conta de armazenamento](storsimple-8000-manage-storage-accounts.md#add-a-storage-account).

### <a name="deactivate-a-storsimple-cloud-appliance"></a>Como desativar um Dispositivo de nuvem StorSimple

Quando você desativa um dispositivo de nuvem, a ação de saudação exclui hello VM e recursos de saudação criados quando ele foi provisionado. Depois que o dispositivo de nuvem hello está desativado, ele não pode ser restaurado estado anterior tooits. Antes de desativar o dispositivo de nuvem hello, certifique-se de que toostop ou exclua os clientes e hosts que dependem dele.

Desativar um dispositivo de nuvem resulta em Olá ações a seguir:

* dispositivo de nuvem Olá é removido.
* disco Olá SO e discos de dados criados para o dispositivo de nuvem Olá são removidos.
* serviço hospedado de saudação e rede virtual criada durante o provisionamento são mantidos. Se você não os estiver usando, deverá excluí-los manualmente.
* Instantâneos de nuvem criados para o dispositivo de nuvem Olá são mantidos.

Para um procedimento passo a passo, consulte muito[desativar e excluir seu dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).

Assim que o dispositivo de saudação de nuvem é mostrado como desativado na folha de serviço do Gerenciador de dispositivos de StorSimple hello, você pode excluir dispositivo de nuvem de saudação da lista de dispositivos em hello **dispositivos** folha.

### <a name="start-stop-and-restart-a-cloud-appliance"></a>Como iniciar, parar e reiniciar um dispositivo de nuvem
Ao contrário do dispositivo físico do StorSimple hello, há sem energia e desligar toopush botão em um dispositivo de nuvem do StorSimple. No entanto, pode haver ocasiões em que você precisa toostop e reiniciar o dispositivo de saudação de nuvem.

saudação de maneira mais fácil para você toostart, parar e reiniciar um dispositivo de nuvem é por meio de saudação folha de serviço de máquinas virtuais. Serviço de máquina Virtual de saudação go. Na lista de saudação de VMs, identificar o dispositivo de nuvem de tooyour correspondente Olá VM (mesmo nome) e clique em nome da VM hello. Quando você examinar sua folha de máquina virtual, status de dispositivo de nuvem Olá é **executando** porque ele é iniciado por padrão, depois que ele é criado. É possível iniciar, parar e reiniciar uma máquina virtual a qualquer momento.

[!INCLUDE [Stop and restart cloud appliance](../../includes/storsimple-8000-stop-restart-cloud-appliance.md)]

### <a name="reset-toofactory-defaults"></a>Redefinir padrões toofactory
Se você decidir que deseja toostart sobre com a sua solução de nuvem, desativar e excluí-lo e, em seguida, crie um novo.

## <a name="fail-over-toohello-cloud-appliance"></a>O failover de dispositivo de toohello de nuvem
Recuperação de desastres (DR) é um de saudação principais cenários de Olá StorSimple Appliance de nuvem foi projetado para. Nesse cenário, Olá dispositivo StorSimple físico ou datacenter inteiro pode não estar disponível. Felizmente, você pode usar as operações toorestore de dispositivo de nuvem em um local alternativo. Durante a recuperação de desastres, contêineres de volume de saudação do dispositivo de origem de saudação alterar a propriedade e são transferidos toohello appliance de nuvem.

Olá pré-requisitos para DR são:

* dispositivo de saudação de nuvem é criado e configurado.
* Todos os volumes de saudação no contêiner de volume Olá estão offline.
* contêiner de volume Olá failover, possui um tipo de instantâneo em nuvem.

> [!NOTE]
> * Ao usar um dispositivo de nuvem como dispositivo secundário Olá para recuperação de desastres, tenha em mente que Olá 8010 tem 30 TB de armazenamento padrão e 8020 tem 64 TB de armazenamento Premium. dispositivo de saudação maior capacidade 8020 nuvem pode ser mais adequado para um cenário de recuperação de desastres.

Para um procedimento passo a passo, consulte muito[failover de dispositivo de nuvem tooa](storsimple-8000-device-failover-cloud-appliance.md).

## <a name="delete-hello-cloud-appliance"></a>Excluir o dispositivo de saudação de nuvem
Se configurado anteriormente e usado um dispositivo de nuvem StorSimple mas agora deseja toostop acúmulo de encargos de computação para seu uso, você deve interromper o dispositivo de saudação de nuvem. Dispositivo de nuvem Olá parando desaloca Olá VM. Esta ação interromperá o acúmulo de encargos na sua assinatura. encargos de armazenamento Olá para Olá SO e discos de dados entretanto continuarão.

toostop Olá a todos os encargos, você deve excluir o dispositivo de saudação de nuvem. toodelete Olá os backups criados pelo dispositivo de saudação de nuvem, você pode desativar ou excluir dispositivo hello. Para saber mais, confira [Desativar e excluir um dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).

[!INCLUDE [Delete a cloud appliance](../../includes/storsimple-8000-delete-cloud-appliance.md)]

## <a name="troubleshoot-internet-connectivity-errors"></a>Solucionar problemas de erros de conectividade com a Internet
Durante a criação de saudação de um dispositivo de nuvem, se não houver nenhum toohello de conectividade da Internet, o hello criação etapa falhar. falhas de conectividade de Internet tootroubleshoot, execute Olá etapas Olá portal do Azure:

1. [Crie uma máquina virtual do Windows Server 2012 no Azure](/articles/virtual-machines/windows/quick-create-portal.md). Esta máquina virtual deve usar Olá a mesma conta de armazenamento, redes e sub-rede conforme usado por seu dispositivo de nuvem. Se houver um host do Windows Server no Azure usando Olá a mesma conta de armazenamento, redes e sub-redes, você também pode usá-lo conectividade com a Internet tootroubleshoot hello.
2. Log remoto na máquina virtual de saudação criado no hello anterior da etapa.
3. Abra uma janela de comando em máquina virtual de saudação (Win + R e digite `cmd`).
4. Execute Olá cmd prompt Olá a seguir.

    `nslookup windows.net`
5. Se `nslookup` falhar, em seguida, falha de conectividade de Internet está impedindo o dispositivo de nuvem Olá ao registrar o serviço de Gerenciador de dispositivos de StorSimple toohello.
6. Fazer alterações de saudação necessária tooyour tooensure de rede virtual que Olá appliance de nuvem é capaz de tooaccess sites do Azure como _windows.net_.

## <a name="next-steps"></a>Próximas etapas
* Saiba como muito[usar toomanage de serviço de Gerenciador de dispositivos de StorSimple Olá um dispositivo de nuvem](storsimple-8000-manager-service-administration.md).
* Entender como muito[restaurar de um conjunto de backup de um volume StorSimple](storsimple-8000-restore-from-backup-set-u2.md).
