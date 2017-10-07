---
title: "práticas recomendadas de aaaBest para matriz Virtual StorSimple | Microsoft Docs"
description: "Descreve Olá práticas recomendadas para implantar e gerenciar Olá matriz Virtual StorSimple."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 57ac6eeb-c47c-442d-a5f4-b360d81a76a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/08/2017
ms.author: alkohli
ms.openlocfilehash: f242364365e07f86b78e2f9bb2acfb3aa98e83e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-best-practices"></a>Práticas recomendadas do StorSimple Virtual Array
## <a name="overview"></a>Visão geral
A Matriz Virtual Microsoft Azure StorSimple é uma solução de armazenamento integrado que gerencia as tarefas de armazenamento entre um dispositivo virtual local executando em um hipervisor e o armazenamento em nuvem do Microsoft Azure. Matriz Virtual StorSimple é uma matriz de físicos de série de eficiente e econômica toohello 8000 alternativo. matriz virtual Olá pode ser executados em sua infraestrutura existente do hipervisor, dá suporte a iSCSI hello e protocolos SMB hello e é bem adequado para cenários de filiais/escritórios remotos. Para obter mais informações sobre soluções de StorSimple hello, vá muito[visão geral do Microsoft Azure StorSimple](https://www.microsoft.com/en-us/server-cloud/products/storsimple/overview.aspx).

Este artigo aborda as práticas recomendadas de saudação implementadas durante a configuração inicial do hello, implantação e gerenciamento de saudação matriz Virtual StorSimple. Essas práticas recomendadas fornecem diretrizes validadas para instalação hello e o gerenciamento de sua matriz virtual. Este artigo destina-se em direção à saudação IT administradores que implantar e gerenciar Olá virtuais matrizes em seus datacenters.

É recomendável uma revisão periódica de saudação toohelp de práticas recomendada, verifique se seu dispositivo ainda está em conformidade quando forem feitas alterações toohello instalação ou operação de fluxo. Se você encontrar problemas ao implementar essas práticas recomendadas em sua matriz virtual, [contate o Suporte da Microsoft](storsimple-virtual-array-log-support-ticket.md) para obter assistência.

## <a name="configuration-best-practices"></a>Práticas recomendadas de configuração
Essas práticas recomendadas abordam diretrizes Olá que precisam toobe seguido durante a implantação de matrizes virtual hello e configuração inicial de saudação. Essas práticas recomendadas incluem esses toohello relacionados de provisionamento da máquina virtual de hello, configurações de política de grupo, dimensionamento, configurando Olá de rede, configurar contas de armazenamento e criar compartilhamentos e volumes para Olá array virtual. 

### <a name="provisioning"></a>Provisionamento
Matriz Virtual StorSimple é uma máquina virtual (VM) provisionada no hipervisor hello (Hyper-V ou VMware) do seu servidor de host. Quando o provisionamento de máquina virtual de saudação, certifique-se de que seu host é capaz de toodedicate recursos suficientes. Para obter mais informações, vá muito[requisitos mínimos de recurso](storsimple-virtual-array-deploy2-provision-hyperv.md#step-1-ensure-that-the-host-system-meets-minimum-virtual-array-requirements) tooprovision uma matriz.

Saudação de implementar as práticas recomendadas a seguir ao provisionar matriz virtual hello:

|  | Hyper-V | VMware |
| --- | --- | --- |
| **Tipo de máquina virtual** |**geração 2** a ser usada com o Windows Server 2012 ou posterior e uma imagem *.vhdx* . <br></br> **geração 1** a ser usada com um Windows Server 2008 ou posterior e uma imagem *.vhd* . |Use a máquina virtual versão 8 a 11 ao usar a imagem *.vmdk* . |
| **Tipo de memória** |Configurar como **memória estática**. <br></br> Não use Olá **memória dinâmica** opção. | |
| **Tipo de disco de dados** |Provisione como **expandindo dinamicamente**.<br></br> **tamanho fixo** leva muito tempo. <br></br> Não use Olá **diferenciais** opção. |Saudação de uso **fino provisionar** opção. |
| **Modificação de disco de dados** |A expansão ou a redução não é permitida. Toodo uma tentativa para resulta na perda de saudação de todos os dados de local de saudação no dispositivo. |A expansão ou a redução não é permitida. Toodo uma tentativa para resulta na perda de saudação de todos os dados de local de saudação no dispositivo. |

### <a name="sizing"></a>Dimensionamento
Ao dimensionar sua matriz Virtual StorSimple, considere Olá fatores a seguir:

* Reserva de local de volumes ou de compartilhamentos. Aproximadamente 12% do espaço da saudação está reservado na camada de saudação local para cada compartilhamento ou volume em camadas provisionado. Aproximadamente 10% do espaço de saudação também é reservada para um volume localmente afixado para o sistema de arquivos.
* Sobrecarga de instantâneo. Aproximadamente 15% de espaço no nível local Olá é reservado para instantâneos.
* Necessidade de restaurações. Se fazer a restauração de uma operação de novo, dimensionamento deve levar em conta Olá espaço necessário para a restauração. A restauração é realizada tooa compartilhamento ou volume de saudação mesmo tamanho.
* Parte do buffer deve ser alocada para qualquer crescimento inesperado.

Com base em Olá anterior fatores, Olá requisitos de dimensionamento pode ser representado por Olá equação a seguir:

`Total usable local disk size = (Total provisioned locally pinned volume/share size including space for file system) + (Max (local reservation for a volume/share) for all tiered volumes/share) + (Local reservation for all tiered volumes/shares)`

`Data disk size = Total usable local disk size + Snapshot overhead + buffer for unexpected growth or new share or volume`

Olá exemplos a seguir ilustram como você pode dimensionar uma matriz virtual com base nos seus requisitos.

#### <a name="example-1"></a>Exemplo 1:
Em sua matriz virtual, você deseja toobe capaz

* provisionar um volume ou um compartilhamento em camadas de 2 TB.
* provisionar um volume ou um compartilhamento em camadas de 1 TB.
* provisionar um volume ou um compartilhamento fixado localmente de 300 GB.

Para Olá anterior volumes ou compartilhamentos, vamos calcular os requisitos de espaço de saudação na camada de saudação local.

Primeiro, para cada volume/compartilhamento em camadas, a reserva local seria igual too12% do tamanho de volume/compartilhamento hello. Olá localmente afixado volume/compartilhamento, a reserva de local é 10% da saudação localmente fixados tamanho de volume/compartilhamento (além de toohello provisionado tamanho). Nesse exemplo, você precisa de

* reserva local de 240 GB (para um volume/compartilhamento em camadas de 2 TB)
* reserva local de 120 GB (para um volume/compartilhamento em camadas de 1 TB)
* 330 GB para o volume localmente afixado ou compartilhamento (adicionando 10% do tamanho de 300 GB provisionado toohello reserva local)

Olá espaço total necessário na camada local Olá até agora é: 240 GB + 120 GB + 330 GB = 690 GB.

Em segundo lugar, precisamos de pelo menos o espaço da camada local hello como maior única reserva hello. Esse valor extra é usado caso você precise toorestore de um instantâneo de nuvem. Neste exemplo, a reserva local maior de saudação é 330 GB (incluindo reserva para o sistema de arquivos), portanto você deve adicionar esse toohello GB: 690 690 GB + 330 GB = 1020 GB.
Se realizamos as restaurações subsequentes adicionais, é sempre pode liberar espaço de saudação de operação de restauração anterior hello.

Em terceiro lugar, precisamos de 15% do total local até o momento espaço toostore os instantâneos locais, para que somente 85% dele está disponível. Neste exemplo, isso seria em torno de 1020 GB = 0,85&ast;TB de disco de dados provisionado. Portanto, disco de dados provisionado Olá seria (1020&ast;(1/0.85)) = 1200 GB = 1,20 TB ~ 1,25 TB (arredondamento quartil toonearest)

Incluindo o crescimento inesperado e novas restaurações, você deverá provisionar um disco local de aproximadamente 1,25 a 1,5 TB.

> [!NOTE]
> Também recomendamos que esse disco local Olá escassamente provisionado. Essa recomendação é porque o espaço de restauração Olá só é necessário quando você deseja que os dados toorestore com mais de cinco dias. Recuperação em nível de item permite que você toorestore dados Olá últimos cinco dias sem a necessidade de Olá espaço extra para restauração.


#### <a name="example-2"></a>Exemplo 2:
Em sua matriz virtual, você deseja toobe capaz

* provisionar um volume em camadas de 2 TB
* provisionar um volume fixado localmente de 300 GB

Com base em 12% de reserva do espaço local para volumes/compartilhamentos em camadas e 10% para volumes/compartilhamentos fixados localmente, precisamos de

* uma reserva local de 240 GB (para um volume/compartilhamento em camadas de 2 TB)
* 330 GB para o volume localmente afixado ou compartilhamento (adicionando 10% do espaço de 300 GB provisionado toohello reserva local)

Espaço total necessário na camada de local de saudação é: 240 GB + 330 GB = 570 GB

Olá local espaço mínimo necessário para a restauração é 330 GB.

15% do total do disco é usado toostore instantâneos para 0.85 somente está disponível. Assim, é o tamanho do disco hello (900&ast;(1/0.85)) = TB 1,06 ~ 1,25 TB (arredondamento quartil toonearest)

Incluindo qualquer crescimento inesperado, você poderá provisionar um disco local de 1,25-1,5 TB.

### <a name="group-policy"></a>Política de grupo
Política de grupo é uma infraestrutura que permite que você tooimplement a configurações específicas para usuários e computadores. Configurações de política de grupo estão contidas em objetos de diretiva de grupo (GPOs), que são vinculado toohello contêineres de serviços de domínio Active Directory (AD DS) a seguir: sites, domínios ou unidades organizacionais (OUs). 

Se o virtual array é ingressado no domínio, GPOs podem ser aplicado tooit. Esses GPOs podem instalar aplicativos como um software antivírus que pode afetar a operação de saudação do hello matriz Virtual StorSimple.

Portanto, recomendamos que você:

* Certifique-se de que a matriz virtual esteja em sua própria OU (unidade organizacional) do Active Directory.
* Certifique-se de que nenhum objeto de diretiva de grupo (GPOs) é matriz virtual tooyour aplicado. Você pode bloquear a herança tooensure que Olá virtual array (nó filho) não herdam automaticamente a qualquer GPOs do pai de saudação. Para obter mais informações, vá muito[bloquear herança](https://technet.microsoft.com/library/cc731076.aspx).

### <a name="networking"></a>Rede
configuração de rede Olá para sua matriz virtual é feita através da interface do usuário da web local hello. Uma interface de rede virtual é habilitada por meio de hipervisor Olá em que a matriz virtual Olá é provisionado. Saudação de uso [as configurações de rede](storsimple-virtual-array-deploy3-fs-setup.md) página endereço IP de interface de rede virtual do tooconfigure hello, sub-rede e gateway.  Você também pode configurar o servidor DNS primário e secundário hello, configurações de tempo e configurações de proxy opcionais para seu dispositivo. A maioria da configuração de rede Olá é uma configuração única. Saudação de revisão [StorSimple requisitos de rede](storsimple-ova-system-requirements.md#networking-requirements) array virtual de saudação toodeploying anterior.

Ao implantar sua matriz virtual, recomendamos que você siga estas práticas recomendadas:

* Certifique-se de que essa rede Olá quais Olá array virtual é implantada sempre tem Olá capacidade toodedicate largura de banda de Mbps Internet 5 (ou mais).
  
  * Necessidade de largura de banda de Internet varia dependendo de suas características de carga de trabalho e a taxa de saudação de alteração de dados.
  * alteração de dados de saudação que pode ser tratada é diretamente proporcional tooyour largura de banda de Internet. Como um exemplo, ao fazer um backup, uma largura de banda de 5 Mbps pode acomodar uma alteração de dados de cerca de 18 GB em 8 horas. Com quatro vezes mais largura de banda (20 Mbps), você poderá lidar com uma alteração de dados quatro vezes maior (72 GB).
* Certifique-se de que toohello de conectividade da Internet está sempre disponível. Dispositivos de toohello de conexões da Internet esporádicos ou não confiáveis podem resultar em perda de acesso toodata na nuvem hello e poderá resultar em uma configuração sem suporte.
* Se você planejar toodeploy seu dispositivo, como um servidor iSCSI:
  
  * Recomendamos que você desabilite Olá **obter endereços IP automaticamente** opção (DHCP).
  * Configure endereços IP estáticos. Você deve configurar um servidor DNS principal e um secundário.
  * Se definir várias interfaces de rede no virtual array, apenas Olá primeira interface de rede (por padrão, essa interface é **Ethernet**) pode acessar a nuvem de saudação. tipo de saudação toocontrol de tráfego, você pode criar várias interfaces de rede virtual no virtual array (configurado como um servidor iSCSI) e conectar as sub-redes de toodifferent interfaces.
* toothrottle Olá nuvem largura de banda apenas (usada pela matriz virtual Olá), configurar a limitação no roteador hello ou firewall hello. Se você definir o hipervisor de limitação, limite todos os protocolos de saudação incluindo iSCSI e SMB em vez de apenas Olá nuvem largura de banda.
* Verifique se a sincronização de hora para hipervisores está ativada. Se usando o Hyper-V, selecione sua matriz virtual no Gerenciador do Hyper-V de saudação, vá muito**configurações &gt; Integration Services**e certifique-se de que Olá **sincronização de hora** é verificada.

### <a name="storage-accounts"></a>Contas de armazenamento
O StorSimple Virtual Array pode ser associado a uma única conta de armazenamento. Esta conta de armazenamento pode ser uma conta de armazenamento gerada automaticamente, uma conta no hello mesma assinatura hello, ou uma conta de armazenamento relacionados tooanother assinatura. Para obter mais informações, consulte como muito[gerenciar contas de armazenamento para sua matriz virtual](storsimple-virtual-array-manage-storage-accounts.md).

Saudação de uso para contas de armazenamento associadas com o virtual array as recomendações a seguir.

* Ao vincular várias matrizes virtuais com uma única conta de armazenamento, fatores na capacidade máxima hello (64 TB) para uma matriz virtual e o tamanho máximo do hello (500 TB) para uma conta de armazenamento. Isso limita o número de saudação de matrizes virtuais em tamanho normal que pode ser associado essa conta de armazenamento tooabout 7.
* Ao criar uma nova conta de armazenamento
  
  * É recomendável que você a crie em Olá região mais próxima toohello escritório remoto/filial onde sua matriz Virtual StorSimple é implantado toominimize latências.
  * Tenha em mente que você não pode mover uma conta de armazenamento entre regiões diferentes. Também é possível mover um serviço entre assinaturas.
  * Use uma conta de armazenamento que implementa a redundância entre os datacenters de saudação. O GRS (Armazenamento com Redundância Geográfica), o ZRS (Armazenamento com Redundância Local) e o LRS (Armazenamento Localmente Redundante) têm suporte para serem usados com a matriz virtual. Para obter mais informações sobre tipos diferentes de saudação de contas de armazenamento, vá muito[replicação de armazenamento do Azure](../storage/common/storage-redundancy.md).

### <a name="shares-and-volumes"></a>Compartilhamentos e volumes
Para seu StorSimple Virtual Array, você pode provisionar compartilhamentos quando ele estiver configurado como um servidor de arquivos e volumes como um servidor iSCSI. práticas recomendadas de saudação para criar compartilhamentos e volumes estão relacionadas com o tipo de tamanho e hello toohello configurado.

#### <a name="volumeshare-size"></a>Tamanho de volume/compartilhamento
Em sua matriz virtual, você pode provisionar compartilhamentos quando ele estiver configurado como um servidor de arquivos e volumes quando ele estiver configurado como um servidor iSCSI. Olá práticas recomendadas para criar compartilhamentos e volumes relacionam a tamanho toohello e Olá tipo configurado. 

Lembre-Olá se seguir as práticas recomendadas ao provisionar compartilhamentos ou volumes em seu dispositivo virtual.

* tamanho do Hello arquivo tamanhos relativos toohello provisionado de um compartilhamento em camadas pode afetar o desempenho de camadas de saudação. Trabalhar com arquivos grandes pode resultar em uma divisão lenta em camadas. Ao trabalhar com arquivos grandes, é recomendável que esse arquivo maior Olá é menor do que 3% do tamanho do compartilhamento de saudação.
* Um máximo de 16 volumes/compartilhamento pode ser criado na matriz virtual hello. Limites de tamanho de saudação do hello localmente fixados e hierárquico volumes/compartilhamento, consulte sempre toohello [limites de matriz Virtual StorSimple](storsimple-ova-limits.md).
* Ao criar um volume, o fator de consumo de dados Olá esperado, bem como para futuro crescimento. volume de saudação não pode ser expandida mais tarde.
* Quando o volume de saudação tiver sido criado, é possível reduzir o tamanho de saudação do volume Olá StorSimple.
* Quando gravar tooa hierárquico volume StorSimple, quando os dados de volume Olá atingem um limite determinado (espaço local relativo toohello reservado para o volume de saudação), hello e/s está limitada. Continuar toowrite toothis volume diminui hello e/s significativamente. Embora você possa gravar tooa hierárquico volume além da sua capacidade provisionada (não ativamente paramos usuário Olá gravação além da capacidade de saudação provisionada), você verá uma notificação de alerta em vigor toohello que você tenha com excesso de assinaturas. Quando você vir o alerta Olá, é fundamental que você tome medidas corretivas como excluir dados de volume de saudação (expansão de volume não é suportado atualmente).
* Para casos de uso da recuperação de desastres, como número de saudação de compartilhamentos permitidos/volumes é 16 e hello máximo número de compartilhamentos/volumes que podem ser processadas em paralelo também é 16, Olá o número de compartilhamentos/volumes não tem um efeito sobre o RPO e RTOs.

#### <a name="volumeshare-type"></a>Tipo de volume/compartilhamento
StorSimple oferece suporte a dois tipos de volume/compartilhamento com base no uso de saudação: fixado localmente e em camadas. Volumes localmente afixados/compartilhamentos são muito provisionados enquanto hello volumes/compartilhamento em camadas são escassamente provisionado. Não é possível converter um volume localmente afixado/compartilhamento tootiered ou *vice-versa* depois de criado.

É recomendável que você implemente Olá seguir as práticas recomendadas ao configurar volumes/compartilhamento StorSimple:

* Identifique o tipo de volume de saudação com base em cargas de trabalho de saudação que você pretende toodeploy antes de criar um volume. Use volumes localmente fixos para cargas de trabalho que exigem garantias locais de dados (mesmo durante uma interrupção de nuvem) e que exigem latências de nuvem baixas. Quando você cria um volume em sua matriz virtual, é possível alterar o tipo de volume de saudação do tootiered localmente afixado ou *o contrário*. Por exemplo, crie volumes localmente fixos ao implantar cargas de trabalho do SQL ou cargas de trabalho que hospedam máquinas virtuais (VMs); use volumes em camadas para cargas de trabalho de compartilhamento de arquivo.
* Marque a opção de saudação para dados de arquivamento menos usados com frequência ao lidar com arquivos grandes. Um maior tamanho da parte de eliminação de duplicação de 512 K é usado quando essa opção é habilitada nuvem toohello de transferência de dados de saudação tooexpedite.

#### <a name="volume-format"></a>Formato de volume
Depois de criar volumes do StorSimple em seu servidor do iSCSI, você precisa tooinitialize e montagem Olá formato volumes. Esta operação é executada no dispositivo StorSimple do hello host conectado tooyour. Práticas recomendadas a seguir são recomendadas quando montar e formatar volumes no host de StorSimple hello.

* Execute uma formatação rápida em todos os volumes do StorSimple.
* Ao formatar um volume do StorSimple, use um tamanho de unidade de alocação (AUS) de 64 KB (o padrão é 4 KB). Olá 64 KB Austrália baseia-se em testes realizados internamente para as cargas de trabalho do StorSimple e outras cargas de trabalho.
* Quando usando Olá StorSimple matriz Virtual configurado como um servidor do iSCSI, não use volumes estendidos ou discos dinâmicos como esses volumes ou discos não são suportados pelo StorSimple.

#### <a name="share-access"></a>Acesso ao compartilhamento
Ao criar compartilhamentos em seu servidor de arquivo de matriz virtual, siga estas diretrizes:

* Ao criar um compartilhamento, atribua um grupo de usuários como um administrador de compartilhamento em vez de um único usuário.
* Você pode gerenciar as permissões de NTFS Olá após Olá compartilhamento é criado por meio da edição Olá compartilhamentos através do Windows Explorer.

#### <a name="volume-access"></a>Acesso ao volume
Ao configurar volumes de iSCSI Olá no StorSimple Virtual Array, é importante toocontrol acesso sempre que necessário. toodetermine que hospedam os servidores pode acessar volumes, crie e associe registros de controle de acesso (ACRs) volumes do StorSimple.

Use Olá seguir as práticas recomendadas ao configurar ACRs para volumes do StorSimple:

* Sempre associe pelo menos um ACR a um volume.

* Ao atribuir mais de um volume de tooa ACR, certifique-se de que o volume Olá não é exposto de maneira em que ele pode ser acessado simultaneamente por mais de um host não clusterizado. Se você tiver atribuído um volume de tooa ACRs vários, uma mensagem de aviso exibida para você tooreview sua configuração.

### <a name="data-security-and-encryption"></a>Segurança e criptografia de dados
Sua matriz Virtual StorSimple possui recursos de segurança e criptografia de dados que garantem a confidencialidade de saudação e a integridade de seus dados. Ao usar esses recursos, é recomendável que você siga estas práticas recomendadas: 

* Defina uma criptografia de toogenerate chave AES-256 de criptografia de armazenamento de nuvem antes do envio de dados de saudação da nuvem toohello array virtual. Essa chave não é necessária se os dados estiverem criptografado toobegin com. Olá chave pode ser gerada e mantida em segurança usando um sistema de gerenciamento de chaves como [Cofre de chaves do Azure](../key-vault/key-vault-whatis.md).
* Quando Configurando Olá conta de armazenamento por meio do serviço do StorSimple Manager hello, certifique-se de que você habilite Olá SSL modo toocreate um canal seguro para comunicação de rede entre seu dispositivo StorSimple e hello na nuvem.
* Chaves de regenerar Olá para suas contas de armazenamento (por acessar um serviço de armazenamento do Azure Olá) periodicamente tooaccount para qualquer altera tooaccess com base na lista de saudação alterada de administradores.
* Dados em sua matriz virtual são compactados e eliminação de duplicação antes de serem enviado tooAzure. Não é recomendável usar o serviço de função de eliminação de duplicação de dados de saudação no host do Windows Server.

## <a name="operational-best-practices"></a>Práticas recomendadas operacionais
Olá operacional práticas recomendadas são diretrizes que devem ser seguidas durante operação de matriz virtual hello ou do gerenciamento cotidiano hello. Essas práticas abrangem tarefas específicas de gerenciamento, como fazer backups, a restauração de um conjunto de backup, a execução de um failover, desativando e excluindo Olá matriz, uso do sistema de monitoramento e integridade, e vírus de executando verificações em sua matriz virtual.

### <a name="backups"></a>Backups
Olá sua matriz virtual é feito backup dos dados nuvem toohello de duas maneiras, um padrão automatizado backup diário de saudação todo dispositivo começando às 22:30 ou por meio de um backup manual do sob demanda. Por padrão, o dispositivo Olá automaticamente cria instantâneos de nuvem diários de todos os dados de saudação que residem nele. Para obter mais informações, vá muito[backup sua matriz Virtual StorSimple](storsimple-virtual-array-backup.md).

Hello frequência e associados a saudação padrão backups de retenção não podem ser alteradas, mas você pode configurar o tempo de saudação no qual Olá backups diários são iniciados diariamente. Ao configurar a hora de início de saudação de saudação backups automatizados, recomendamos que:

* Agende os backups fora dos horários de pico. A hora de início de backup não deve coincidir com várias E/S do host.
* Inicie um backup manual do sob demanda ao planejar tooperform um failover de dispositivo ou a janela de manutenção toohello anteriores, dados de saudação tooprotect em sua matriz virtual.

### <a name="restore"></a>Restaurar
Você pode restaurar de um conjunto de duas maneiras de backup: restaurar o compartilhamento ou volume tooanother ou realizar uma recuperação em nível de item (disponível apenas em uma matriz virtual configurada como um servidor de arquivos). Recuperação em nível de item permite que você toodo uma recuperação granular de arquivos e pastas de um backup na nuvem de todos os compartilhamentos de saudação no dispositivo do StorSimple hello. Para obter mais informações, vá muito[restaurar de um backup](storsimple-virtual-array-clone.md).

Ao executar uma restauração, lembre-Olá, seguindo as diretrizes em mente:

* Seu StorSimple Virtual Array não oferece suporte à restauração no local. No entanto pode ser prontamente obtida por um processo de duas etapas: Libere espaço no hello virtual de matriz e, em seguida, restaurar tooanother volume/compartilhamento.
* Ao restaurar de um volume local, manter na restauração de saudação mente será uma operação demorada. Embora o volume de saudação rapidamente pode ficar online, dados saudação continuam toobe serializado no plano de fundo de saudação.
* Olá volume tipo permanece Olá mesmo durante o processo de restauração hello. Um volume em camadas é restaurado em camadas tooanother volume e um volume do volume localmente afixado tooanother fixado localmente.
* Quando tentar toorestore um volume ou um compartilhamento de um conjunto de backup, se o trabalho de restauração Olá falhar, um volume de destino ou compartilhamento ainda pode ser criado no portal de saudação. É importante que você excluir o volume de destino não utilizado ou compartilhar em toominimize portal Olá problemas futuros decorrentes deste elemento.

### <a name="failover-and-disaster-recovery"></a>Failover e recuperação de desastres
Um failover de dispositivo permite que você toomigrate seus dados de um *fonte* dispositivo no hello datacenter tooanother *destino* dispositivo localizado no hello mesma ou em um local geográfico diferente. failover de dispositivo de saudação é para todo dispositivo de saudação. Durante o failover, dados na nuvem para dispositivo de origem Olá Olá alteram toothat de propriedade do dispositivo de destino hello.

Para sua matriz Virtual StorSimple, você pode somente failover matriz virtual tooanother gerenciados por Olá mesmo serviço StorSimple Manager. Um dispositivo da série 8000 do tooan failover ou uma matriz gerenciados por um serviço StorSimple Manager diferentes (que Olá um dispositivo de origem Olá) não é permitida. toolearn mais informações sobre considerações de failover hello, ir muito[pré-requisitos para o failover de dispositivo Olá](storsimple-virtual-array-failover-dr.md).

Ao executar uma falha em para sua matriz virtual, tenha em mente Olá seguinte:

* Para um failover planejado, é uma recomendado prática recomendada tootake tooinitiating anterior offline Olá failover de todos os Olá volumes/compartilhamento. Siga as instruções de específicos do sistema operacional de saudação tootake Olá volumes/compartilhamento offline nos Olá host primeiro e, em seguida, desconecte aqueles em seu dispositivo virtual.
* Uma arquivo server para recuperação de desastres (DR), é recomendável que você ingressar toohello de dispositivo de destino Olá mesmo domínio como origem de saudação para que Olá permissões de compartilhamento são resolvidos automaticamente. Olá somente o dispositivo de destino do failover tooa em Olá mesmo domínio é suportado nesta versão.
* Depois de hello DR é concluída com êxito, o dispositivo de origem Olá é excluído automaticamente. Embora Olá dispositivo não está mais disponível, máquina virtual Olá provisionado no sistema de host Olá ainda está consumindo recursos. É recomendável que você exclua esta máquina virtual da sua tooprevent de sistema host quaisquer encargos do acúmulo.
* Observe que, mesmo se Olá failover for bem-sucedido, **dados saudação são sempre seguros na nuvem Olá**. Considere Olá três cenários nos quais Olá failover não foi concluída com êxito a seguir:
  
  * Ocorreu uma falha nos estágios de saudação inicial de failover hello, como quando as pré-verificações de Olá DR estão sendo executadas. Nessa situação, o dispositivo de destino ainda é utilizável. Você pode repetir Olá failover em hello mesmo dispositivo de destino.
  * Ocorreu uma falha durante o processo de failover real hello. Nesse caso, o dispositivo de destino hello está marcado como inutilizável. Você deve provisionar e configurar outra matriz virtual de destino e usá-la para failover.
  * Olá failover foi concluída após o dispositivo de origem Olá foi excluído, mas o dispositivo de destino Olá tem problemas de e não pode acessar todos os dados. dados saudação ainda seja seguros na nuvem hello e podem ser facilmente recuperados criando outra matriz virtual e, em seguida, usá-lo como um dispositivo de destino para Olá DR.

### <a name="deactivate"></a>Desativar
Quando você desativa uma matriz Virtual StorSimple, servidor de conexão Olá entre Olá dispositivo e o serviço StorSimple Manager correspondente de saudação. A desativação é uma operação **permanente** e não pode ser desfeita. Um dispositivo desativado não pode ser registrado novamente por hello serviço StorSimple Manager. Para obter mais informações, vá muito[desativar e excluir sua matriz Virtual StorSimple](storsimple-virtual-array-deactivate-and-delete-device.md).

Lembre-Olá seguintes práticas recomendadas em mente ao desativar sua matriz virtual:

* Pegue um instantâneo de todos os Olá dados anteriores toodeactivating um dispositivo virtual. Quando você desativar uma matriz virtual, todos os dados de dispositivo local Olá são perdidas. Tirar um instantâneo de nuvem permitirá toorecover dados em um estágio posterior.
* Antes de desativar uma matriz Virtual StorSimple, certifique-se de que toostop ou excluir os clientes e hosts que dependem desse dispositivo.
* Exclua um dispositivo desativado se ele não estiver sendo usado para que ele não acumule cobranças.

### <a name="monitoring"></a>Monitoramento
tooensure sua matriz Virtual StorSimple está em um estado íntegro contínuo, é necessário toomonitor Olá matriz e certifique-se de que você recebe informações do sistema Olá incluindo alertas. toomonitor Olá a integridade geral da matriz de virtual hello, Olá implementar as práticas recomendadas a seguir:

* Configure o uso do disco de saudação de tootrack monitoramento de seu disco de dados de matriz virtual, bem como o disco do sistema operacional hello. Se executando o Hyper-V, você pode usar uma combinação do System Center Virtual Machine Manager (SCVMM) e o System Center Operations Manager (SCOM) toomonitor seus hosts de virtualização.
* Configure notificações por email em seus alertas de toosend array virtual em determinados níveis de uso.                                                                                                                                                                                                

### <a name="index-search-and-virus-scan-applications"></a>Aplicativos de pesquisa de índice e de verificação de vírus
Uma matriz Virtual StorSimple pode camada automaticamente dados de saudação camada local toohello nuvem do Microsoft Azure. Quando um aplicativo como uma pesquisa de índice ou uma verificação de vírus tooscan usados dados de saudação armazenados no StorSimple, você precisa tootake cuidado dados na nuvem Olá não obter acessados e volta extraídos da camada de local de toohello.

É recomendável que você implemente Olá seguir as práticas recomendadas ao configurar a verificação de vírus ou de pesquisa de índice Olá em sua matriz virtual:

* Desabilite todas as operações de verificação completa configuradas automaticamente.
* Para volumes em camadas, configure Olá índice pesquisa ou vírus verificação aplicativo tooperform uma verificação incremental. Isso seria verificar somente Olá novos dados provável que residem na camada de local de saudação. dados Olá toohello hierárquico nuvem não são acessados durante uma operação incremental.
* Certifique-se de Olá filtros de pesquisa correto e as configurações são definidas para que tipos de saudação que se destina somente de arquivos ser verificados. Por exemplo, a imagem de arquivos (JPEG, GIF e TIFF) e projetos de engenharia não devem ser verificados durante a recriação de índice completo ou incremental hello.

Se você estiver usando o processo de indexação do Windows, siga estas diretrizes:

* Não use Olá indexador do Windows para volumes em camadas como recupera grandes quantidades de dados (TB) de nuvem Olá se precisar de índice Olá toobe recriado com frequência. A recriação de índice Olá recuperaria todos os tooindex de tipos de arquivo seu conteúdo.
* Use o Windows hello indexação de processo para volumes localmente afixados como isso seria acessar somente os dados no índice de Olá Olá camadas local toobuild (nuvem Olá dados não serão acessados).

### <a name="byte-range-locking"></a>Bloqueio de intervalo de bytes
Aplicativos podem bloquear um intervalo de bytes especificado nos arquivos de saudação. Se o bloqueio de intervalo de bytes é habilitado em aplicativos de saudação que estiver escrevendo tooyour StorSimple, camadas, em seguida, não funcionam em sua matriz virtual. Para toowork de camadas hello, todas as áreas do hello arquivos acessados devem ser desbloqueadas. Não há suporte para o bloqueio de intervalo de bytes com volumes em camadas em sua matriz virtual.

Recomendado medidas de bloqueio de intervalo de bytes tooalleviate incluem:

* Desligar o bloqueio de intervalo de bytes em sua lógica de aplicativo.
* Use localmente fixados volumes (em vez de em camadas) para dados de Olá associados a este aplicativo. Volumes localmente afixados não camada em nuvem hello.
* Quando usando fixado localmente volumes com bloqueio de intervalo de bytes habilitado, volume Olá pode ficar online antes de saudação restauração for concluída. Nesses casos, você deve aguardar Olá toobe de restauração completa.

## <a name="multiple-arrays"></a>Várias matrizes
Várias matrizes virtuais podem ser necessário tooaccount toobe implantado para um conjunto de trabalho crescente de dados que podem gravar na nuvem hello, portanto, afetar o desempenho de saudação do dispositivo hello. Nesses casos, é melhor dispositivos de tooscale à medida que aumenta de conjunto de trabalho de saudação. Isso requer um ou mais toobe dispositivos adicionados no data center da saudação no local. Ao adicionar dispositivos hello, você pode:

* Saudação de divisão atual conjunto de dados.
* Implante novos dispositivos toonew de cargas de trabalho.
* Se implantar várias matrizes virtuais, é recomendável que a do balanceamento de carga de perspectiva, distribuir matriz Olá em hosts de hipervisor diferentes.
* Várias matrizes virtuais (quando configuradas como um servidor de arquivos ou como um servidor iSCSI) podem ser implantadas em um Namespace de Sistema de Arquivos Distribuído . Para obter etapas detalhadas, consulte muito[Distributed File System Namespace Solution com guia de implantação do armazenamento de nuvem híbrida](https://www.microsoft.com/download/details.aspx?id=45507). Replicação de sistema de arquivos distribuído no momento não é recomendada para uso com matriz virtual Olá. 

## <a name="see-also"></a>Consulte também
Saiba como muito[administrar sua matriz Virtual StorSimple](storsimple-virtual-array-manager-service-administration.md) via Olá serviço StorSimple Manager.

