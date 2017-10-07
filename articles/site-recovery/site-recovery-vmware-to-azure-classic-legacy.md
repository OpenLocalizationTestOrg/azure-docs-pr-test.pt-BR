---
title: "aaaReplicate VMs VMware e servidores físicos tooAzure (legados clássico) | Microsoft Docs"
description: "Descreve como tooreplicate local VMs e tooAzure de servidores físicos do Windows/Linux usando o Azure Site Recovery em uma implantação herdada no portal clássico do hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: f980fb52-8ec2-4dd9-85e2-8e52e449f1ba
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: raynew
ms.openlocfilehash: 64c6d906d54426fdd2b884350542a4562bb12528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery-using-hello-classic-portal-legacy"></a>Replicar máquinas virtuais VMware e servidores físicos tooAzure com o Azure Site Recovery usando o portal clássico do hello (legados)
> [!div class="op_single_selector"]
> * [Portal do Azure](site-recovery-vmware-to-azure.md)
> * [Portal clássico](site-recovery-vmware-to-azure-classic.md)
> * [Portal Clássico (herdado)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

Bem-vindo tooAzure recuperação de Site! Este artigo descreve uma implantação herdado para replicar máquinas virtuais VMware a locais ou tooAzure de servidores físicos do Windows/Linux usando o Azure Site Recovery no portal clássico do hello.

## <a name="overview"></a>Visão geral
As organizações precisam de uma estratégia BCDR que determina como aplicativos, cargas de trabalho e dados permanecem em execução e disponível durante o tempo de inatividade planejado e não planejado e recuperar toonormal condições de trabalho assim que possível. Sua estratégia de BCDR devem manter os dados comerciais seguros e passíveis de recuperação e garantir que as cargas de trabalho permaneçam continuamente disponíveis mediante um desastre.

Recuperação de site é um serviço do Azure que contribui com a estratégia BCDR tooyour pela replicação de orquestração de servidores de locais físicos e máquinas virtuais toohello nuvem (Azure) ou datacenter secundário tooa. Quando ocorrem paralisações do local primário, você failover toohello local secundário tookeep aplicativos e cargas de trabalho disponíveis. Você não local primário tooyour voltar ao retornar toonormal operações. Saiba mais em [O que é o Azure Site Recovery?](site-recovery-overview.md)

> [!WARNING]
> Este artigo contém **instruções herdadas**. Não o use para novas implantações. Em vez disso, [, siga estas instruções](site-recovery-vmware-to-azure.md) toodeploy recuperação de Site no hello portal do Azure, ou [use estas instruções](site-recovery-vmware-to-azure-classic.md) tooconfigure Olá avançado de implantação no portal clássico do hello. Se você já implantou o usando o método hello descrito neste artigo, é recomendável que você migre toohello avançado de implantação no portal clássico do hello.
>
>

## <a name="migrate-toohello-enhanced-deployment"></a>Migrar toohello avançado de implantação
Esta seção só é relevante se você já implantou o Site Recovery usando instruções Olá neste artigo.

toomigrate sua implantação existente, você precisará:

1. Implantar novos componentes da Recuperação de Site no site local.
2. Configure credenciais para a descoberta automática de máquinas virtuais do VMware no servidor de configuração nova hello.
3. Descobrir servidores do VMware Olá com o novo servidor de configuração hello.
4. Crie um novo grupo de proteção com o novo servidor de configuração hello.

Antes de começar:

* Recomendamos que você configure uma janela de manutenção para a migração.
* Olá **migrar máquinas** opção está disponível somente se você tiver grupos de proteção existentes que foram criados durante a implantação herdada.
* Depois de concluir as etapas de migração de saudação pode levar 15 minutos ou mais credenciais de saudação toorefresh e toodiscover e atualização de máquinas virtuais para que você possa adicionar grupo de proteção tooa. Você pode atualizar manualmente em vez de aguardar.

Migre da seguinte maneira:

1. Leia sobre [avançado de implantação no portal clássico Olá](site-recovery-vmware-to-azure-classic.md). Saudação de análise avançada [arquitetura](site-recovery-vmware-to-azure-classic.md), e [pré-requisitos](site-recovery-vmware-to-azure-classic.md).
2. Desinstale o serviço de mobilidade de saudação do máquinas que no momento você estiver replicando. Uma nova versão do serviço de saudação será instalada em máquinas de hello quando você adicionar toohello novo grupo de proteção.
3. Baixar um [chave de registro de cofre](site-recovery-vmware-to-azure-classic.md) e [executar o Assistente de instalação unificada de saudação](site-recovery-vmware-to-azure-classic.md) mestre, servidor de processo e servidor de configuração de saudação tooinstall componentes do servidor de destino. Leia mais sobre o [planejamento de capacidade](site-recovery-vmware-to-azure-classic.md).
4. [Configurar credenciais](site-recovery-vmware-to-azure-classic.md) recuperação de Site pode usar tooaccess VMware server tooautomatically descobrir VMs VMware. Saiba mais sobre as [permissões necessárias](site-recovery-vmware-to-azure-classic.md).
5. Adicione [servidores vCenter ou hosts vSphere](site-recovery-vmware-to-azure-classic.md). Pode levar 15 minutos para obter mais informações para servidores tooappear no portal de recuperação de Site hello.
6. Crie um [novo grupo de proteção](site-recovery-vmware-to-azure-classic.md). Pode demorar até minutos too15 toorefresh portal Olá para que as máquinas virtuais de saudação são descobertas e aparecer. Se você não quiser toowait você pode realçar o nome do servidor de gerenciamento de saudação (não clique nele) > **atualizar**.
7. Novo grupo de proteção Olá em **migrar máquinas**.

    ![Adicionar Conta](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration1.png)
8. Em **selecionar máquinas** grupo de proteção Olá selecione desejado toomigrate do e Olá máquinas que você deseja toomigrate.

    ![Adicionar Conta](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration2.png)
9. Em **definir configurações de destino** especificar se deseja toouse Olá as mesmas configurações para todas as máquinas e servidor de processo selecione hello e conta de armazenamento do Azure. Se você não tiver um servidor de processo separado isso será o endereço IP Olá Olá Olá server do servidor de configuração.

    ![Adicionar Conta](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration3.png)

    > [AZURE.NOTE] [Migração de contas de armazenamento](../resource-group-move-resources.md) em recursos grupos dentro Olá a mesma assinatura ou em assinaturas não é há suporte para contas de armazenamento usadas para implantar a recuperação de Site.

1. Em **especificar contas**, selecione conta Olá criada para tooaccess de servidor de processo Olá Olá máquina toopush Olá nova versão do serviço de mobilidade hello.

   ![Adicionar Conta](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration4.png)
2. Recuperação de site irá migrar sua conta de armazenamento do Azure toohello dados replicados que você forneceu. Opcionalmente, você pode reutilizar conta de armazenamento Olá usado na implantação herdado hello.
3. Após o trabalho de saudação máquinas virtuais de conclusão serão automaticamente sincronizados. Após a conclusão da sincronização, você pode excluir máquinas virtuais de Olá Olá herdados do grupo de proteção.
4. Depois de migraram todas as máquinas podem excluir grupo de proteção herdados de saudação.
5. Lembre-se propriedades de failover toospecify Olá para máquinas e Olá as configurações de rede do Azure após a conclusão da sincronização.
6. Se você tem planos de recuperação existentes, você pode migrá-los implantação toohello aprimorada com hello **migrar o plano de recuperação** opção. Você só deverá fazer isso após a migração de todas as máquinas protegidas.

   ![Adicionar Conta](./media/site-recovery-vmware-to-azure-classic-legacy/legacy-migration5.png)

> [!NOTE]
> Depois que você acabou de migração continuar Olá [artigo avançado](site-recovery-vmware-to-azure-classic.md). restante Olá deste artigo herdado deixará de ser relevante e você não precisa toofollow qualquer mais Olá etapas descritas no it * *.
>
>

## <a name="what-do-i-need"></a>Do que eu preciso?
Este diagrama mostra os componentes de implantação de saudação.

![Novo cofre](./media/site-recovery-vmware-to-azure-classic-legacy/architecture.png)

Você precisará de:

| **Componente** | **Implantação** | **Detalhes** |
| --- | --- | --- |
| **Servidor de configuração** |Uma máquina de virtual de A3 padrão do Azure no hello mesma assinatura que a recuperação de Site. |servidor de configuração de saudação coordena a comunicação entre computadores protegidos, o servidor de processo hello e servidores de destino mestre no Azure. Ele configura a replicação e coordena a recuperação no Azure quando o failover ocorre. |
| **Servidor de destino mestre** |Uma máquina virtual do Azure — um servidor Windows com base em uma imagem da Galeria do Windows Server 2012 R2 (tooprotect máquinas do Windows) ou como um servidor Linux com base em uma imagem da Galeria OpenLogic CentOS 6.6 (tooprotect Linux máquinas).<br/><br/> Há três opções de dimensionamento disponíveis: Standard A4, Standard D14 e Standard DS4.<br/><br/> servidor Hello está conectada toohello mesma rede do Azure como o servidor de configuração de saudação.<br/><br/> Configurar no portal de recuperação de Site Olá |Ele recebe e retém os dados replicados dos computadores protegidos usando VHDs anexadas criadas no armazenamento de blobs em sua conta de armazenamento do Azure.<br/><br/> Especificamente, selecione Standard DS4 para configurar a proteção para cargas de trabalho que exigem um alto desempenho consistente e baixa latência usando a Conta de Armazenamento Premium. |
| **Servidor de processo** |Um servidor físico ou virtual local que executa o Windows Server 2012 R2<br/><br/> É recomendável que ele colocado no hello mesmo segmento de LAN máquinas Olá que você deseja tooprotect, mas ele pode ser executado em uma rede diferente como computadores protegidos tem L3 e de rede tooit de visibilidade de rede.<br/><br/> Configurá-lo e registre-o servidor de configuração de toohello no portal de recuperação de Site hello. |Servidor de processo replicação dados toohello local de envio de computadores protegidos. Ele tem um cache com base em disco toocache replicação de dados que recebe. Ele executa várias ações sobre esses dados.<br/><br/> Isso otimiza a dados, cache, a compactação e criptografá-los antes de enviá-la no servidor de destino mestre toohello.<br/><br/> Gerencia a instalação por push do serviço de mobilidade de saudação.<br/><br/> Ele executa a descoberta automática de máquinas virtuais da VMware. |
| **Computadores locais** |Máquinas virtuais da VMware locais ou servidores físicos que executam Windows ou Linux. |Você define as configurações de replicação que se aplicam a um ou mais computadores. Você pode executar failover em um computador individual ou, o mais comum, em vários computadores reunidos em um plano de recuperação. |
| **Serviço de mobilidade** |Instalado em cada máquina virtual ou de um servidor físico em que você deseja tooprotect<br/><br/> Pode ser instalado manualmente ou enviados por push e instalado automaticamente pelo servidor de processo hello quando você habilitar a replicação para uma máquina. |Olá serviço de mobilidade envia o servidor de processo toohello dados durante a replicação inicial (ressincronização). Depois de máquina hello está em um estado protegido (após a conclusão da ressincronização) Olá serviço de mobilidade captura toodisk de gravações de memória e os envia toohello servidor de processo. A consistência com aplicativos para servidores Windows é obtida com o VSS. |
| **Cofre do Azure Site Recovery** |Criar um cofre de recuperação de Site com uma assinatura do Azure e registrar servidores no cofre hello. |Olá coordenadas do cofre e coordena a replicação de dados, failover e recuperação entre o site local e o Azure. |
| **Mecanismo de replicação** |**Sobre Olá Internet**— comunica e replica dados do local protegido tooAzure de servidores usando o canal seguro de SSL/TLS em Olá da internet. Essa é a opção de padrão de saudação.<br/><br/> **VPN/ExpressRoute**– Comunica e replica dados entre servidores locais e o Azure em uma conexão VPN. Você precisará tooset uma VPN site a site ou uma conexão de rota expressa entre sua rede do Azure e o site local.<br/><br/> Você irá selecionar como deseja tooreplicate durante a implantação da recuperação de Site. Você não pode alterar o mecanismo de saudação depois de configurado sem afetar a replicação dos computadores existentes. |Nenhuma opção requer que você tooopen quaisquer portas de rede de entrada nos computadores protegidos. Todas as comunicações de rede é iniciada do hello no site local. |

## <a name="capacity-planning"></a>Planejamento da capacidade
Olá principais áreas que você precisará tooconsider:

* **Ambiente de origem**— Olá infra-estrutura de VMware, as configurações de máquina de origem e requisitos.
* **Servidores de componentes**— Olá servidor de processo, o servidor de configuração e o servidor de destino mestre

### <a name="considerations-for-hello-source-environment"></a>Considerações para o ambiente de origem Olá
* **Tamanho máximo do disco**– tamanho máximo atual de saudação do disco de saudação que pode ser anexado tooa virtual máquina é de 1 TB. Assim, o tamanho máximo de Olá de um disco de origem que pode ser replicado também é limitado too1 TB.
* **Tamanho máximo por origem**– tamanho máximo de saudação um único computador de origem é 31 TB (com 31 discos) e com uma instância de D14 provisionado para o servidor de destino mestre hello.
* **Número de origens por servidor de destino mestre**—vários computadores de origem podem ser protegidos com um único servidor de destino mestre. No entanto, uma máquina de origem única não pode ser protegida em vários servidores de destino mestre, pois como replicam discos, um VHD que reflete o tamanho de saudação do disco de saudação é criado no armazenamento de BLOBs do Azure e anexado como um servidor de destino mestre de toohello de disco de dados.  
* **Taxa de alteração diária máximo por origem**— há três fatores que precisam toobe considerado quando considerar Olá recomendado alteram a taxa por origem. Para considerações de destino com base em Olá dois IOPS são necessários no disco de destino Olá para cada operação na fonte de saudação. Isso ocorre porque uma leitura de dados antigos e uma gravação de dados novo Olá acontecerá no disco de destino hello.
  * **Alterar diariamente taxa suportada pelo servidor de processo Olá**— uma máquina de origem não pode abranger vários servidores de processo. Um servidor de processo único pode dar suporte a até too1 TB de taxa de alteração diária. Portanto, é 1 TB com suporte para uma máquina de origem de taxa de alteração de dados diários máximo de saudação.
  * **A taxa de transferência máxima é suportada por disco de destino Olá**— variação máximo por disco de origem não pode ser mais de 144 GB/dia (com tamanho de gravação de 8 K). Consulte a tabela de saudação na seção de destino mestre Olá para taxa de transferência hello e IOPs de destino Olá para vários tamanhos de gravação. Esse número deve ser dividido por dois, porque cada origem IOP gera 2 IOPS no disco de destino de saudação. Leia sobre [destinos de escalabilidade e desempenho do Azure](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) ao configurar o destino de saudação para contas de armazenamento premium.
  * **Taxa de transferência máxima suportada pela conta de armazenamento Olá**— uma fonte não pode abranger várias contas de armazenamento. Devido a uma conta de armazenamento tem um máximo de 20.000 solicitações por segundo e que cada fonte IOP gera 2 IOPS no servidor de destino mestre Olá, é recomendável que você mantenha o número de saudação de IOPS em Olá fonte too10, 000. Leia sobre [destinos de escalabilidade e desempenho do Azure](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) ao configurar fonte Olá para contas de armazenamento premium.

### <a name="considerations-for-component-servers"></a>Considerações para servidores de componente
A tabela 1 resume os tamanhos de máquina virtual Olá para configuração de saudação e servidores de destino mestre.

| **Componente** | **Instâncias do Azure implantadas** | **Núcleos** | **Memória** | **Máx. de discos** | **Tamanho do disco** |
| --- | --- | --- | --- | --- | --- |
| Servidor de configuração |Padrão A3 |4 |7 GB |8 |1023 GB |
| Servidor de destino mestre |Padrão A4 |8 |14 GB |16 |1023 GB |
| Padrão D14 |16 |112 GB |32 |1023 GB | |
| DS4 padrão |8 |28 GB |16 |1023 GB | |

**Tabela 1**

#### <a name="process-server-considerations"></a>Considerações do servidor de processo
Geralmente dimensionamento do servidor de processo depende de taxa de alteração diária Olá em todas as cargas de trabalho protegidas.

* Você precisa de tarefas de tooperform de computação suficiente como embutido compactação e criptografia.
* servidor de processo Olá usa cache baseado em disco. Verifique se Olá recomendado espaço do cache e taxa de transferência do disco está disponível toofacilitate as alterações de dados de Olá armazenadas no evento de saudação do afunilamento de rede ou interrupção.
* Certifique-se de largura de banda suficiente para que hello servidor de processo pode carregar Olá dados toohello destino mestre server tooprovide proteção contínua dos dados.

A tabela 2 fornece um resumo das diretrizes de servidor de processo hello.

| **Taxa de alteração de dados** | **CPU** | **Memória** | **Tamanho do disco de cache** | **Taxa de transferência do disco de cache** | **Entrada/saída da largura de banda** |
| --- | --- | --- | --- | --- | --- |
| Menos de 300 GB |4 vCPUs (2 soquetes x 2 núcleos a 2,5 GHz) |4 GB |600 GB |too10 7 MB por segundo |30 Mbps/21 Mbps |
| too600 300 GB |8 vCPUs (2 soquetes x 4 núcleos a 2,5 GHz) |6 GB |600 GB |too15 11 MB por segundo |60 Mbps/42 Mbps |
| 600 GB too1 TB |12 vCPUs (2 soquetes x 6 núcleos a 2,5 GHz) |8 GB |600 GB |too20 16 MB por segundo |100 Mbps/70 Mbps |
| Mais de 1 TB |Implantar outro servidor de processo | | | | |

**Tabela 2**

Em que:

* Ingresso é a largura de banda do download (intranet entre o servidor de origem e o processo de saudação).
* Saída é a largura de banda de carregamento (internet entre o servidor de processo hello e servidor de destino mestre). Os números de saída presumem uma compactação média de 30% do servidor de processo.
* Para disco de cache, um disco separado do sistema operacional de 128 GB, no mínimo, é recomendável para todos os servidores de processo.
* Saudação de taxa de transferência do cache em disco para o armazenamento a seguir foi usada para benchmark: 8 unidades SAS de 10K RPM com configuração RAID 10.

#### <a name="configuration-server-considerations"></a>Considerações do servidor de configuração
Cada servidor de configuração pode dar suporte a máquinas de origem too100 com volumes de 3 a 4. Caso a implantação seja maior, recomendamos implantar outro servidor de configuração. Consulte a tabela 1 para propriedades de máquina virtual padrão Olá saudação do servidor de configuração.

#### <a name="master-target-server-and-storage-account-considerations"></a>Considerações de conta de armazenamento e servidor de destino mestre
armazenamento de saudação para cada servidor de destino mestre inclui um disco do sistema operacional, um volume de retenção e os discos de dados. unidade de retenção Olá mantém diário de saudação do disco for alterado durante saudação da janela de retenção Olá definida no portal de recuperação de Site hello.  Consulte 1 tooTable para propriedades de máquina virtual Olá Olá mestre do servidor de destino. A tabela 3 mostra como discos de saudação do A4 são usados.

| **Instância** | **Disco do sistema operacional** | **Retenção** | **Discos de dados** |
| --- | --- | --- | --- |
| **Retenção** |**Discos de dados** | | |
| Padrão A4 |1 disco (1 x 1023 GB) |1 disco (1 x 1023 GB) |15 discos (15 x 1023 GB) |
| Padrão D14 |1 disco (1 x 1023 GB) |1 disco (1 x 1023 GB) |31 discos (15 x 1023 GB) |
| DS4 padrão |1 disco (1 x 1023 GB) |1 disco (1 x 1023 GB) |15 discos (15 x 1023 GB) |

**Tabela 3**

Planejamento de capacidade do servidor de destino mestre Olá depende:

* Das limitações e do desempenho do armazenamento do Azure
  * número máximo de saudação do altamente utilizadas discos para uma VM de camada padrão, é de cerca de 40 (20.000/500 IOPS por disco) em uma única conta de armazenamento. Leia sobre [destino de escalabilidade para contas de armazenamento padrão](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) e para [contas de armazenamento premium](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks).
* Da taxa de alteração diária
* Do armazenamento do volume de retenção.

Observe que:

* Uma fonte não pode incluir várias contas de armazenamento. Isso se aplica a toohello disco de dados que vão toohello contas de armazenamento selecionadas quando você configurar a proteção. discos de retenção de sistema operacional e Olá Olá geralmente vá toohello implantado automaticamente a conta de armazenamento.
* volume de armazenamento de retenção Olá necessário depende de taxa de alteração diária hello e número de saudação de dias de retenção. Olá armazenamento de retenção necessário por servidor de destino mestre = variação total de origem por dia * número de dias de retenção.
* Cada servidor de destino mestre tem apenas um volume de retenção. volume de retenção de saudação é compartilhada entre o servidor de destino mestre Olá discos anexados toohello. Por exemplo:
  * Se uma máquina de origem com 5 discos e cada disco gera 120 IOPS (tamanho de 8K) na fonte hello, isso se traduz too240 IOPS por disco (2 operações no disco de destino Olá por fonte de e/s). IOPS de 240 está dentro do hello Azure por limite de IOPS de disco de 500.
  * Volume de retenção hello, isso se torna a 120 * 5 = 600 IOPS e isso podem se tornar um gargalo. Nesse cenário, uma boa estratégia seria tooadd mais volume de retenção de toohello de discos e abrangem-lo em, como uma configuração de distribuição RAID. Isso melhora o desempenho porque Olá IOPS são distribuídas por vários discos. número de saudação de unidades toobe adicionado toohello volume de retenção será da seguinte maneira:
    * Total de IOPS do ambiente de origem / 500
    * Variação total por dia do ambiente de origem (descompactado) / 287 GB. 287 GB é a taxa de transferência máxima Olá suportada por um disco de destino por dia. Essa métrica irão variar com base no tamanho de gravação da saudação com um fator de 8K, porque nesse caso é 8K três presume-se que o tamanho de gravação. Por exemplo, se o tamanho de gravação da saudação é 4K e taxa de transferência será 287/2. E se o tamanho de gravação da saudação é 16K taxa de transferência será 287 * 2.
* Olá número de contas de armazenamento necessário = total fonte IOPs/10000.

## <a name="before-you-start"></a>Antes de começar
| **Componente** | **Requisitos** | **Detalhes** |
| --- | --- | --- |
| **Conta do Azure** |Você precisará de uma conta do [Microsoft Azure](https://azure.microsoft.com/) . Você pode começar com uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/). | |
| **Armazenamento do Azure** |Você precisará de um toostore replicado dados da conta de armazenamento do Azure<br/><br/> Qualquer conta Olá deve ser um [conta de armazenamento com redundância geográfica padrão](../storage/common/storage-redundancy.md#geo-redundant-storage) ou [conta de armazenamento Premium](../storage/common/storage-premium-storage.md).<br/><br/> Ele no deve Olá mesma região Olá serviço Azure Site Recovery e estar associada a saudação mesma assinatura. Não há suporte para movimentação de saudação de contas de armazenamento criadas usando Olá [novo portal do Azure](../storage/common/storage-create-storage-account.md) entre grupos de recursos.<br/><br/> toolearn mais leitura [Introdução tooMicrosoft armazenamento do Azure](../storage/common/storage-introduction.md) | |
| **Rede virtual do Azure** |Você precisará de uma rede virtual do Azure no qual Olá servidor de configuração e o servidor de destino mestre serão implantados. Ele deve estar no hello mesma assinatura e região do cofre Azure Site Recovery hello. Se você quiser tooreplicate dados em uma saudação de conexão rota expressa ou VPN do Azure virtual rede deve ser rede de local tooyour conectado via uma conexão de rota expressa ou VPN Site a Site. | |
| **Recursos do Azure** |Verifique se que você tem suficiente toodeploy recursos do Azure todos os componentes. Leia mais em [Limites de assinatura do Azure](../azure-subscription-service-limits.md). | |
| **Máquinas Virtuais do Azure** |Máquinas virtuais que você deseja tooprotect devem estar em conformidade com [pré-requisitos do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).<br/><br/> **Contagem de discos** – há suporte para um máximo de 31 discos em um único servidor protegido<br/><br/> **Tamanhos de disco** – a capacidade de disco individual não deve ser superior a 1.023 GB<br/><br/> **Clustering** – não há suporte a servidores clusterizados<br/><br/> **Inicialização** – não há suporte à inicialização UEFI (Unified Extensible Firmware Interface)/EFI (Extensible Firmware Interface)<br/><br/> **Volumes** – não há suporte a volumes criptografados com Bitlocker<br/><br/> **Nomes de servidor**– Os nomes devem conter entre 1 e 63 caracteres (letras, números e hifens). nome da saudação deve começar com uma letra ou número e terminar com uma letra ou número. Depois que um computador estiver protegido, você pode modificar Olá nomes do Azure. | |
| **Servidor de configuração** |Máquina de virtual A3 padrão com base em uma imagem da Galeria do Azure Site Recovery Windows Server 2012 R2 será criada em sua assinatura para o servidor de configuração de saudação. Ele é criado como Olá primeira instância em um novo serviço de nuvem. Se você selecionar Internet pública, como tipo de conectividade de saudação para serviço de nuvem saudação do servidor de configuração Olá será criado com um endereço IP público reservado.<br/><br/> caminho de instalação Olá deve ser somente caracteres em inglês. | |
| **Servidor de destino mestre** |Máquina virtual do Azure, Standard A4, D14 ou DS4.<br/><br/> caminho de instalação Olá deve ser somente caracteres em inglês. Por exemplo deve ser o caminho de saudação **/usr/local/ASR** para um servidor de destino mestre que executa o Linux. | |
| **Servidor de processo** |Você pode implantar o servidor de processo Olá no computador físico ou da máquina virtual que executa o Windows Server 2012 R2 com atualizações mais recentes de saudação. Instale em C:/.<br/><br/> Recomendamos que você colocar o servidor de saudação em Olá Olá máquinas que você deseja tooprotect a mesma rede e sub-rede.<br/><br/> Instale o VMware vSphere CLI 5.5.0 no servidor de processo hello. componente do Hello VMware vSphere CLI é necessária no servidor de processo Olá em máquinas virtuais da ordem toodiscover gerenciados por um servidor do vCenter ou máquinas virtuais em execução em um host de ESXi.<br/><br/> caminho de instalação Olá deve ser somente caracteres em inglês.<br/><br/> Não há suporte para o Sistema de Arquivos ReFS. | |
| **VMware** |Um servidor VMware vCenter que gerencia os hipervisores do VMware vSphere. Ele deve ser executado vCenter versão 5.1 ou 5.5 com atualizações mais recentes de saudação.<br/><br/> Um ou mais hipervisores vSphere que contém máquinas virtuais VMware, você deseja tooprotect. Olá hipervisor deve estar executando o ESX/ESXi versão 5.1 ou 5.5 com atualizações mais recentes de saudação.<br/><br/> As máquinas virtuais da VMware devem ter as ferramentas da VMware instaladas e em execução. | |
| **Computadores Windows** |Servidores físicos protegidos ou máquinas virtuais da VMware que executam o Windows têm uma série de requisitos.<br/><br/> Um sistema operacional de 64 bits com suporte: **Windows Server 2012 R2**, **Windows Server 2012** ou **Windows Server 2008 R2 com, no mínimo, SP1**.<br/><br/> Olá, nome do host, pontos de montagem, nomes de dispositivo, caminho de sistema do Windows (por exemplo: C:\Windows) deve estar em inglês apenas.<br/><br/> sistema operacional de saudação deve ser instalado na unidade C:\.<br/><br/> Somente os discos básicos têm suporte. Não há suporte para discos dinâmicos.<br/><br/> Regras de firewall em computadores protegidos devem permitir que eles servidores de destino tooreach Olá mestre e de configuração no Azure.p ><p>Você precisará de uma conta de administrador do tooprovide (deve ser um administrador local no computador do Windows hello) toopush instalar Olá serviço de mobilidade em servidores Windows. Se Olá fornecido é uma conta de domínio não será necessário toodisable controle de acesso de usuário remoto na máquina local hello. toodo este Olá Adicionar entrada de registro LocalAccountTokenFilterPolicy DWORD com um valor de 1 em HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System. entrada de registro de saudação tooadd de uma CLI abra cmd ou o powershell e digite  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** . [Saiba mais](https://msdn.microsoft.com/library/aa826699.aspx) sobre o controle de acesso.<br/><br/> Após o failover, certifique-se de que a área de trabalho remota está habilitada para máquina local, Olá se você quiser se conectar a máquinas virtuais de tooWindows no Azure com área de trabalho remota. Se você não estiver se conectando através de VPN, as regras de firewall devem permitir conexões de área de trabalho remota em Olá internet. | |
| **Computadores Linux** |Um sistema operacional de 64 bits com suporte: **6.4 Centos, 6.5, 6.6**; **6.4 de Linux do oracle Enterprise, 6.5 executando o kernel compatível do Red Hat hello ou inviolável Enterprise Kernel versão 3 (UEK3)**, **SUSE Linux Enterprise Server 11 SP3**.<br/><br/> Regras de firewall em computadores protegidos devem permitir que eles tooreach configuração de saudação e servidores de destino mestre no Azure.<br/><br/> arquivos de /etc/hosts em computadores protegidos devem conter entradas que mapeiam Olá host local nome tooIP endereços associados a todas as NICs <br/><br/> Se você quiser tooconnect tooan virtuais do Azure do computador Linux em execução depois de failover usando um Secure Shell cliente (ssh), certifique-se de que Olá serviço Secure Shell em Olá protegido máquina está configurada toostart automaticamente na inicialização do sistema, e que as regras de firewall permitem um ssh tooit de conexão.<br/><br/> nome do host Hello, pontos de montagem, nomes de dispositivos e caminhos de sistema do Linux e nomes de arquivo (por exemplo, / etc /; em /usr.) devem estar em inglês apenas.<br/><br/> Proteção pode ser habilitada para computadores locais com hello armazenamento a seguir:-<br>Sistema de arquivos: EXT3, ETX4, ReiserFS, XFS<br>Software de vários caminhos-Mapeador de Dispositivo (vários caminhos)<br>Gerenciador de volumes: LVM2<br>Não há suporte a servidores físicos com o armazenamento de controlador HP CCISS. | |
| **Terceiros** |Alguns componentes de implantação neste cenário dependem de software de terceiros toofunction corretamente. Para obter uma lista completa, confira [Avisos e informações de software de terceiros](#third-party) | |

### <a name="network-connectivity"></a>Conectividade de rede
Você tem duas opções ao configurar a conectividade de rede entre o site local e Olá rede virtual do Azure no qual Olá componentes de infraestrutura (servidor de configuração, os servidores de destino mestre) são implantados. Você precisará toodecide quais toouse de opção de conectividade de rede antes de você pode implantar o servidor de configuração. Você precisará toochoose essa configuração em tempo de saudação da implantação. Ele não pode ser alterado posteriormente.

**Internet:** comunicação e replicação de dados entre servidores locais de saudação (servidor de processo, computadores protegidos) e servidores de componentes de infraestrutura do Azure hello (servidor de configuração, o servidor de destino mestre) ocorra em uma segurança SSL / Conexão TLS do local toohello pontos de extremidade públicos em servidores de destino mestre e configuração hello. (exceção somente Olá é conexão Olá entre Olá processo e servidor de destino mestre Olá na porta TCP 9080 que não criptografada. Apenas informações de controle relacionadas toohello protocolo de replicação para a instalação de replicação é trocado nesta conexão.)

![Diagrama de implementação para Internet](./media/site-recovery-vmware-to-azure-classic-legacy/internet-deployment.png)

**VPN**: replicação de dados entre servidores locais de saudação (servidor de processo, computadores protegidos) e servidores de componentes de infraestrutura do Azure hello (servidor de configuração, o servidor de destino mestre) e comunicação ocorra em uma conexão VPN entre sua rede local e hello Azure no qual Olá são implantados servidores de destino mestre e servidor de configuração de rede virtual. Certifique-se de que sua rede local é toohello conectado a rede virtual do Azure por uma conexão de rota expressa ou uma conexão de VPN site a site.

![Diagrama de implementação para VPN](./media/site-recovery-vmware-to-azure-classic-legacy/vpn-deployment.png)

## <a name="step-1-create-a-vault"></a>Etapa 1: criar um cofre
1. Entrar toohello [Portal de gerenciamento](https://portal.azure.com).
2. Expanda **Serviços de Dados** > **Serviços de Recuperação** e clique em **Cofre do Site Recovery**.
3. Clique em **Criar Novo** > **Criação Rápida**.
4. Em **nome**, insira um cofre de saudação tooidentify nome amigável.
5. Em **região**, selecione Olá região geográfica para Olá cofre. regiões toocheck suporte consulte disponibilidade geográfica em [detalhes de preços do Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
6. Clique em **Criar cofre**.

    ![Novo cofre](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-create-vault.png)

Verifique a saudação tooconfirm de barra de status que Olá cofre foi criado com êxito. Olá cofre será listado como **Active** em Olá principal **dos serviços de recuperação** página.

## <a name="step-2-deploy-a-configuration-server"></a>Etapa 2: implantar um servidor de configuração
### <a name="configure-server-settings"></a>Definir configurações do servidor
1. Em Olá **dos serviços de recuperação** , clique em página de início rápido do hello cofre tooopen hello. Início rápido também pode ser aberto a qualquer momento usando o ícone de saudação.

    ![Ícone de Inicialização Rápida](./media/site-recovery-vmware-to-azure-classic-legacy/quick-start-icon.png)
2. Na lista suspensa de saudação, selecione **entre um site local com VMware/servidores físicos e o Azure**.
3. Em **Preparar Recursos de Destino do Azure**, clique em **Implantar Servidor de Configuração**.

    ![Implantar Servidor de Configuração](./media/site-recovery-vmware-to-azure-classic-legacy/deploy-cs2.png)
4. Em **Novos Detalhes do Servidor de Configuração** , especifique:

   * Um nome para tooit de tooconnect Olá configuração servidor e credenciais.
   * No tipo de conectividade de rede Olá suspenso Selecione **Internet pública** ou **VPN**. Observe que não será possível modificar essa configuração depois que ela for aplicada.
   * Selecione Olá rede do Azure no qual Olá server deve ser localizado. Se você estiver usando VPN, verifique se Olá rede do Azure é conectado tooyour local rede conforme o esperado.
   * Especifique o endereço IP interno de saudação e a sub-rede que será atribuído toohello server. Observe que Olá quatro primeiros endereços IP em qualquer sub-rede são reservados para uso interno do Azure. Use qualquer outro endereço IP disponível.

     ![Implantar Servidor de Configuração](./media/site-recovery-vmware-to-azure-classic-legacy/cs-details.png)
5. Quando você clica em **Okey** uma máquina de virtual A3 padrão com base em uma imagem da Galeria do Azure Site Recovery Windows Server 2012 R2 será criada em sua assinatura para o servidor de configuração de saudação. Ele é criado como Olá primeira instância em um novo serviço de nuvem. Se você selecionou tooconnect sobre o serviço de nuvem em Olá Olá internet é criado com um endereço IP público reservado. Você pode monitorar o andamento no hello **trabalhos** guia.

    ![Monitorar o progresso](./media/site-recovery-vmware-to-azure-classic-legacy/monitor-cs.png)
6. Se você estiver se conectando pela Olá internet, após o servidor de configuração Olá Observação implantado Olá pública IP endereço atribuído tooit em Olá **máquinas virtuais** página Olá portal do Azure. Em seguida, na Olá **pontos de extremidade** porta HTTPS para público do guia Observação Olá mapeado tooprivate porta 443. Você precisará essas informações posteriormente, quando você registra o destino mestre hello e servidores de processo com o servidor de configuração de saudação. servidor de configuração de saudação é implantada com esses pontos de extremidade:

   * HTTPS: Uma porta pública é usada toocoordinate comunicação entre servidores de componentes e Olá de Azure pela internet. Porta privada 443 é usada toocoordinate comunicação entre servidores de componente e o Azure pela VPN.
   * Personalizada: Uma porta pública é usada para comunicação de ferramenta de failback sobre Olá internet. A porta privada 9443 é usada para comunicação da ferramenta de failback pela VPN.
   * PowerShell: porta privada 5986
   * Área de trabalho remota: porta privada 3389

   ![Pontos de extremidade da VM](./media/site-recovery-vmware-to-azure-classic-legacy/vm-endpoints.png)

   > [!WARNING]
   > Não exclua ou altere o número de porta pública ou privada Olá de pontos de extremidade criados durante a implantação de servidor de configuração.
   >
   >

servidor de configuração de saudação é implantado em um serviço de nuvem do Azure criado automaticamente com um endereço IP reservado. Olá, endereço reservado é necessário tooensure que Olá endereço IP do serviço de nuvem do configuration server permanece Olá mesmo entre as reinicializações de saudação as máquinas virtuais (incluindo o servidor de configuração de saudação) no serviço de nuvem hello. Olá endereço IP público reservado precisará toobe não reservado manualmente quando Olá configuração servidor for encerrado ou ele será mantido reservado. Há um limite padrão de 20 endereços IP públicos reservados por assinatura. [Saiba mais](../virtual-network/virtual-networks-reserved-private-ip.md) sobre endereços IP reservado.

### <a name="register-hello-configuration-server-in-hello-vault"></a>Registrar o servidor de configuração de saudação no cofre Olá
1. Em Olá **início rápido** página clique **preparar recursos de destino** > **baixar uma chave de registro**. arquivo de chave de saudação é gerado automaticamente. Ele é válido por cinco dias após ter sido gerado. Copie-o servidor de configuração de toohello.
2. Em **máquinas virtuais** servidor de configuração de saudação selecione na lista de máquinas virtuais de saudação. Olá abrir **painel** guia e clique em **conectar**. **Abra** Olá baixado toolog do arquivo RDP no servidor de configuração de saudação usando a área de trabalho remota. Se você estiver usando VPN, use Olá interno endereço IP (Olá especificado quando você implantou o servidor de configuração de saudação) para uma conexão de área de trabalho remota de saudação no site local. Olá, o Assistente de instalação do Azure Site Recovery Configuration Server é executado automaticamente quando o logon Olá primeira vez.

    ![Registro](./media/site-recovery-vmware-to-azure-classic-legacy/splash.png)
3. Em **instalação de Software de terceiros** clique **aceito** toodownload e instalar o MySQL.

    ![Instalação do MySQL](./media/site-recovery-vmware-to-azure-classic-legacy/sql-eula.png)
4. Em **detalhes do servidor MySQL** criar credenciais toolog na instância do servidor MySQL hello.

    ![Credenciais do MySQL](./media/site-recovery-vmware-to-azure-classic-legacy/sql-password.png)
5. Em **configurações de Internet** especifique como o servidor de configuração de saudação conectarão toohello internet. Observe que:

   * Se você quiser toouse um proxy personalizado você deve configurá-lo antes de instalar o provedor de saudação.
   * Quando você clica em **próximo** um teste será executado toocheck conexão de proxy de saudação.
   * Se você usar um proxy personalizado, ou o proxy padrão exige autenticação, você precisará detalhes de proxy Olá tooenter, incluindo credenciais, porta e endereço de saudação.
   * Olá URLs a seguir deve ser acessível por meio do proxy de saudação:
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Se você tiver com base em endereço IP regras de firewall Certifique-se que regras de saudação são definidas tooallow comunicação Olá configuração toohello IP dos endereços do servidor descrito em [intervalos de IP de Datacenter do Azure](https://msdn.microsoft.com/library/azure/dn175718.aspx) e o protocolo HTTPS (443). Você teria de intervalos de IP de lista toowhite de saudação região do Azure que você planeje toouse e do Oeste dos EUA.

     ![Registro do proxy](./media/site-recovery-vmware-to-azure-classic-legacy/register-proxy.png)
6. Em **configurações de localização de mensagem de erro do provedor** especifique em qual idioma você deseja tooappear de mensagens de erro.

    ![Registro de mensagem de erro](./media/site-recovery-vmware-to-azure-classic-legacy/register-locale.png)
7. Em **registro de recuperação de Site do Azure** procurar e arquivo de chave de saudação selecione copiados toohello server.

    ![Registro do arquivo de chave](./media/site-recovery-vmware-to-azure-classic-legacy/register-vault.png)
8. Na página de conclusão de saudação do Assistente de saudação selecione estas opções:

   * Selecione **Iniciar diálogo de gerenciamento de conta** toospecify que Olá a caixa de diálogo Gerenciar contas deve ser aberto depois de concluir o Assistente de saudação.
   * Selecione **criar um ícone de área de trabalho para Cspsconfigtool** tooadd um atalho da área de trabalho no servidor de configuração de saudação para que você possa abrir Olá **gerenciar contas** caixa de diálogo a qualquer momento sem a necessidade de toorerun Olá Assistente.

     ![Concluir registro](./media/site-recovery-vmware-to-azure-classic-legacy/register-final.png)
9. Clique em **concluir** toocomplete Assistente de saudação. Uma senha é gerada. Copie-o local seguro tooa. Você precisa tooauthenticate e registrar processo hello e servidores de destino mestre com o servidor de configuração de saudação. Ele também tem usado integridade de canal tooensure na comunicação do servidor de configuração. Você pode gerar novamente a senha hello, mas, em seguida, você precisará de destino mestre do registro toore hello e servidores de processo usando a nova senha de saudação.

    ![Senha](./media/site-recovery-vmware-to-azure-classic-legacy/passphrase.png)

Após o registro de servidor de configuração de saudação será listado na Olá **servidores de configuração** página no cofre hello.

### <a name="set-up-and-manage-accounts"></a>Configurar e gerenciar contas
Durante a implantação do Site Recovery solicita as credenciais de saudação ações a seguir:

* Uma conta da VMware para que a Recuperação de Site possa descobrir VMs automaticamente em servidores vCenter ou hosts vSphere.
* Quando você adiciona máquinas para proteção, para que a recuperação de Site pode instalar o serviço de mobilidade Olá neles.

Após ter registrado o servidor de configuração de saudação, você pode abrir Olá **gerenciar contas** tooadd da caixa de diálogo e gerenciar as contas que devem ser usadas para essas ações. Há duas maneiras toodo isso:

* Abra o atalho Olá você optou por toocreated caixa de diálogo de saudação na última página de saudação do programa de instalação do servidor de configuração de saudação (cspsconfigtool).
* Caixa de diálogo Abrir Olá no término da instalação do servidor de configuração.

1. Em **Gerenciar Contas** click **Adicionar Conta**. Você também pode modificar e excluir contas existentes.

    ![Gerenciar Contas](./media/site-recovery-vmware-to-azure-classic-legacy/manage-account.png)
2. Em **detalhes da conta** especificar um toouse de nome de conta no Azure e as credenciais (nome de usuário do domínio).

    ![Gerenciar Contas](./media/site-recovery-vmware-to-azure-classic-legacy/account-details.png)

### <a name="connect-toohello-configuration-server"></a>Conecte-se o servidor de configuração de toohello
Há duas maneiras tooconnect toohello configuração de servidor:

* Por uma conexão VPN site a site ou de ExpressRoute
* Sobre Olá da internet

Observe que:

* Uma conexão de internet usa pontos de extremidade de saudação da máquina virtual de saudação em conjunto com hello endereço IP virtual público do servidor de saudação.
* Uma conexão VPN usa o endereço IP interno de saudação do servidor de saudação com portas privadas de ponto de extremidade de saudação.
* É uma decisão única toodecide se tooconnect (dados de controle e de replicação) de seu toohello de servidores locais vários servidores de componentes (servidor de configuração, o servidor de destino mestre) em execução no Azure em uma conexão VPN ou Olá da internet. Você não pode alterar essa configuração posteriormente. Se fizer isso, você vai precisar tooredeploy Olá cenário e proteja suas máquinas.  

## <a name="step-3-deploy-hello-master-target-server"></a>Etapa 3: Implantar o servidor de destino mestre Olá
1. Clique em **Preparar Recursos de Destino (Azure)** > **Implantar servidor de destino mestre**.
2. Especifica credenciais e detalhes do servidor de destino mestre hello. Olá servidor será implantado em Olá mesma rede do Azure como o servidor de configuração de saudação. Quando você clica em toocomplete uma máquina virtual do Azure será criada com uma galeria de imagens do Windows ou Linux.

    ![Configurações do servidor de destino](./media/site-recovery-vmware-to-azure-classic-legacy/target-details.png)

Observe que Olá quatro primeiros endereços IP em qualquer sub-rede são reservados para uso interno do Azure. Especifique qualquer outro endereço IP disponível.

> [!NOTE]
> Selecione DS4 padrão ao configurar a proteção para cargas de trabalho que exigem alto desempenho de e/s consistente e baixa latência em ordem toohost e/s intensiva cargas de trabalho usando [conta de armazenamento Premium](../storage/common/storage-premium-storage.md).
>
>

1. Uma VM de destino mestre do Windows é criada com estes pontos de extremidade. Observe que os pontos de extremidade públicos são criados somente se a conectar-se via Olá da internet.

   * Personalizada: Porta pública usada por dados de replicação toosend do servidor de processo Olá sobre Olá internet. Porta privada 9443 é usada por Olá processo servidor toosend replicação dados toohello servidor de destino mestre por VPN.
   * Custom1: Porta pública usada por Olá processo servidor toosend metadados sobre Olá internet. Porta privada 9080 é usada pelo servidor de destino mestre Olá processo server toosend metadados toohello por VPN.
   * PowerShell: porta privada 5986
   * Área de trabalho remota: porta privada 3389
2. Uma VM do servidor de destino mestre do Linux é criada com estes pontos de extremidade. Observe que os pontos de extremidade públicos são criados somente se você estiver se conectando através de saudação à internet.

   * Personalizada: Porta pública usada pelos dados de replicação de toosend de servidor de processo sobre Olá internet. Porta privada 9443 é usada por Olá processo servidor toosend replicação dados toohello servidor de destino mestre por VPN.
   * Custom1: Porta pública é usada por Olá processo servidor toosend metadados sobre Olá internet. Porta privada 9080 é usada pelo servidor de destino mestre Olá processo server toosend metadados toohello por VPN
   * SSH: porta privada 22

     > [!WARNING]
     > Não exclua ou altere o número de porta pública ou privada Olá de qualquer um dos pontos de extremidade Olá criados durante a implantação de servidor de destino mestre hello.
     >
     >
3. Em **máquinas virtuais** aguardar Olá toostart de máquina virtual.

   * Se uma anotação de servidor do Windows para baixo de detalhes da área de trabalho remota hello.
   * Se for um servidor Linux e você estiver se conectando pela VPN Observação Olá endereço IP interno da máquina virtual de saudação. Se você estiver se conectando pela Olá internet Observação Olá endereço IP público.
4. Fazer logon na instalação de toocomplete do servidor de saudação e registrá-lo no servidor de configuração de saudação.
5. Se você estiver executando o Windows:

   1. Inicie uma máquina de virtual toohello conexão de área de trabalho remota. Olá primeira vez que fizer logon em um script será executado em uma janela do PowerShell. Não o feche. Quando concluir a ferramenta de configuração do agente de Host de saudação é aberto automaticamente tooregister servidor de saudação.
   2. Em **configuração do agente de Host** especificar o endereço IP interno de saudação do servidor de configuração de saudação e a porta 443. Você pode usar o endereço interno hello e porta privada 443 mesmo se você não estiver conectando através de VPN como máquina virtual de saudação é anexado toohello mesma rede do Azure como o servidor de configuração de saudação. Deixe a opção **Usar HTTPS** habilitada. Insira a senha de saudação de servidor de saudação de configuração que você anotou anteriormente. Clique em **Okey** tooregister servidor de saudação. Você pode ignorar opções de NAT hello. Elas não são usadas.
   3. Se o seu requisito de unidade de retenção estimado é de mais de 1 TB, você pode configurar volume de retenção de saudação (r) usando um disco virtual e [espaços de armazenamento](http://blogs.technet.com/b/askpfeplat/archive/2013/10/21/storage-spaces-how-to-configure-storage-tiers-with-windows-server-2012-r2.aspx)

   ![Servidor de destino mestre Windows](./media/site-recovery-vmware-to-azure-classic-legacy/target-register.png)
6. Se você estiver executando o Linux:

   1. Verifique se você instalou o hello mais recente Integration Services LIS (Linux) instalado antes de instalar o servidor de destino mestre hello. Você pode encontrar a versão mais recente de saudação do LIS com instruções sobre como tooinstall [aqui](https://www.microsoft.com/download/details.aspx?id=46842). Reinicie a máquina de saudação depois Olá LIS instalar.
   2. Em **Preparar Recursos de Destino (Azure)**, clique em **Baixar e Instalar software adicional (somente para o Servidor de Destino Mestre Linux)**. Saudação de cópia baixado tar arquivo toohello VM usando um cliente de sftp. Como alternativa, você pode fazer logon no servidor de destino mestre linux implantado toohello e usar *wget http://go.microsoft.com/fwlink/?LinkID=529757&clcid=0x409* arquivo de Olá Olá toodownload.
   3. Faça logon no servidor de toohello usando um cliente do Secure Shell. Se você estiver conectado toohello rede do Azure por VPN usar endereço IP interno de saudação. Caso contrário, use endereço IP externo de saudação e o ponto de extremidade público Olá SSH.
   4. Extrair arquivos de saudação do instalador do hello gzip executando: **tar – xvzf Microsoft-ASR_UA_8.4.0.0_RHEL6-64***
      ![o servidor de destino mestre Linux](./media/site-recovery-vmware-to-azure-classic-legacy/linux-tar.png)
   5. Verifique se você está no hello diretório toowhich você extraiu o conteúdo de saudação do arquivo tar hello.
   6. Cópia Olá servidor senha tooa local arquivo de configuração usando o comando Olá **echo  *`<passphrase>`*  > passphrase.txt**
   7. Execute o comando hello "**sudo. /Install -t ambas as - a -R hospedar /usr/local/ASR -d MasterTarget -i  *`<Configuration server internal IP address>`*  -p 443 -s y - c https -P passphrase.txt**".

      ![Registrar servidor de destino](./media/site-recovery-vmware-to-azure-classic-legacy/linux-mt-install.png)
7. Aguarde alguns minutos (10 a 15) e na verificação de página Olá nesse servidor de destino mestre hello está listado como registrado no **servidores** > **servidores de configuração** **dedetalhesdoservidor** guia. Se você estiver executando o Linux e não registrou execute host Olá ferramenta de configuração novamente do /usr/local/ASR/Vx/bin/hostconfigcli. Você precisará de permissões de acesso tooset executando chmod como raiz.

    ![Verificar servidor de destino](./media/site-recovery-vmware-to-azure-classic-legacy/target-server-list.png)

> [!NOTE]
> Pode demorar até too15 minutos após a conclusão de toobe de servidor de destino mestre Olá listado no portal de saudação do registro. tooupdate imediatamente, clique em **atualizar** em Olá **servidores de configuração** página.
>
>

## <a name="step-4-deploy-hello-on-premises-process-server"></a>Etapa 4: Implantar servidor de processo Olá local
Antes de começar, é recomendável que você configurar um endereço IP estático no servidor de processo Olá para que é garantido que ele toobe persistente em reinicializações.

1. Clique em início rápido > **instalar servidor de processo no local** > **baixar e instalar o servidor de processo Olá**.

    ![Instalar servidor de processo](./media/site-recovery-vmware-to-azure-classic-legacy/ps-deploy.png)
2. Saudação de cópia baixado servidor de toohello arquivos zip na qual você vai do servidor em processo tooinstall hello. arquivo zip de saudação contém dois arquivos de instalação:

   * Microsoft-ASR_CX_TP_8.4.0.0_Windows*
   * Microsoft-ASR_CX_8.4.0.0_Windows*
3. Descompacte Olá arquivamento e cópia Olá arquivos tooa local de instalação no servidor de saudação.
4. Executar Olá **Microsoft-ASR_CX_TP_8.4.0.0_Windows*** arquivo de instalação e siga as instruções de hello. Isso instala os componentes de terceiros necessários para a implantação de saudação.
5. Em seguida, execute **Microsoft-ASR_CX_8.4.0.0_Windows***.
6. Em Olá **modo de servidor** página Selecione **servidor de processo**.
7. Em Olá **detalhes do ambiente** página Olá a seguir:

    - Se você quiser clique de máquinas virtuais VMware tooprotect **Sim**
    - Se você deseja somente servidores físicos tooprotect e, portanto, não é necessário vCLI VMware instalado no servidor de processo hello. Clique em **Não** e continue.

1. Observe o seguinte Olá ao instalar o VMware vCLI:

   * **Há suporte apenas para o VMware vSphere CLI 5.5.0**. servidor de processo Olá não funciona com outras versões ou atualizações do vSphere CLI.
   * Baixe o vSphere CLI 5.5.0 [aqui.](https://my.vmware.com/web/vmware/details?downloadGroup=VCLI550&productId=352)
   * Se você instalou o vSphere CLI pouco antes de você começou a instalar o servidor de processo hello e a instalação não detecta, aguarde a toofive minutos antes de tentar a instalação novamente. Isso garante que todas as variáveis de ambiente Olá necessário para detecção do vSphere CLI foi inicializadas corretamente.
2. Em **seleção de NIC para o servidor de processo** adaptador de rede Olá selecione esse servidor de processo Olá deve usar.

   ![Selecionar adaptador](./media/site-recovery-vmware-to-azure-classic-legacy/ps-nic.png)
3. Em **Detalhes do Servidor de Configuração**:

   * Para IP hello endereço e porta, se você estiver se conectando através de VPN especificam o endereço IP interno de saudação saudação do servidor de configuração e 443 para a porta de saudação. Caso contrário, especifique o endereço IP público virtual para o hello e mapeado público de ponto de extremidade HTTP.
   * Digite a senha Olá saudação do servidor de configuração.
   * Limpar **assinatura de software do serviço de mobilidade verificar** se desejar toodisable verificação quando você usar o envio automático tooinstall Olá serviço. Verificação de assinatura precisa de conectividade de internet saudação do servidor de processo.
   * Clique em **Avançar**.

   ![Registrar servidor de configuração](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cs.png)
4. Em **Selecionar Unidade de Instalação** , selecione uma unidade de cache. servidor de processo Olá precisa de uma unidade de cache com pelo menos de 600 GB de espaço livre. Em seguida, clique em **Instalar**.

   ![Registrar servidor de configuração](./media/site-recovery-vmware-to-azure-classic-legacy/ps-cache.png)
5. Observe que talvez você precise instalação de saudação do toorestart Olá server toocomplete. Em **servidor de configuração** > **detalhes do servidor** verificar esse servidor de processo Olá aparece e está registrado com êxito no cofre de saudação.

> [!NOTE]
> Pode demorar até too15 minutos após a conclusão de saudação processo servidor tooappear conforme listado no servidor de configuração de saudação do registro. tooupdate imediatamente, atualizar o servidor de configuração de saudação clicando no botão de atualização de Olá Olá final da página de servidor de configuração de saudação
>
>

![Validar servidor de processo](./media/site-recovery-vmware-to-azure-classic-legacy/ps-register.png)

Se você não desabilitar a verificação de assinatura do serviço de mobilidade hello quando você registrou o servidor de processo Olá, você pode fazer isso mais tarde, da seguinte maneira:

1. Fazer logon no servidor de processo hello como administrador e abra o arquivo de saudação C:\pushinstallsvc\pushinstaller.conf para edição. Na seção Olá **[PushInstaller.transport]** adicionar essa linha: **SignatureVerificationChecks = "0"**. Salve e feche o arquivo hello.
2. Reinicie Olá InMage PushInstall service.

## <a name="step-5-update-site-recovery-components"></a>Etapa 5: Atualizar os componentes da Recuperação de Site
Componentes de recuperação de site são atualizadas de tootime de tempo. Quando novas atualizações estiverem disponíveis, você deve instalá-los em Olá ordem a seguir:

1. Servidor de configuração
2. Servidor de processo
3. Servidor de destino mestre
4. Ferramenta de failback (vContinuum)

### <a name="obtain-and-install-hello-updates"></a>Obter e instalar atualizações de saudação
1. Você pode obter atualizações para a configuração de hello, processos e servidores de destino mestre da saudação recuperação de Site **painel**. Para a instalação do Linux extrair arquivos de saudação do instalador do hello gzip e execute o comando de hello "sudo. /install" atualização de saudação tooinstall.
2. [Baixar](http://go.microsoft.com/fwlink/?LinkID=533813) Olá Olá Failback tool(vContinuum) atualização mais recente.
3. Se você estiver executando máquinas virtuais ou servidores físicos que já têm o serviço de mobilidade Olá instalado, você pode obter atualizações para o serviço de saudação da seguinte maneira:

   * **Opção 1**: baixar atualizações:
     * [Windows Server (somente 64 bits)](http://download.microsoft.com/download/8/4/8/8487F25A-E7D9-4810-99E4-6C18DF13A6D3/Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe)
     * [CentOS 6.4,6.5,6.6 (somente 64 bits)](http://download.microsoft.com/download/7/E/D/7ED50614-1FE1-41F8-B4D2-25D73F623E9B/Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz)
     * [Oracle Enterprise Linux 6.4,6.5 (somente 64 bits)](http://download.microsoft.com/download/5/2/6/526AFE4B-7280-4DC6-B10B-BA3FD18B8091/Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz)
     * [SUSE Linux Enterprise Server SP3 (somente 64 bits)](http://download.microsoft.com/download/B/4/2/B4229162-C25C-4DB2-AD40-D0AE90F92305/Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz)
     * Após a atualização de saudação do servidor de processo Olá versão atualizada do serviço de mobilidade da saudação estarão disponível na pasta de C:\pushinstallsvc\repository Olá no servidor de processo hello.
   * **Opção 2**: se você tiver um computador com uma versão mais antiga do hello serviço de mobilidade instalado, você pode atualizar automaticamente serviço de mobilidade Olá na máquina Olá Olá do portal de gerenciamento.

     1. Certifique-se de que esse servidor de processo Olá é atualizada.
     2. Verifique se o computador protegido Olá obedece Olá [pré-requisitos](#install-the-mobility-service-automatically) para enviar automaticamente o serviço de mobilidade hello, para que a atualização de saudação funciona conforme o esperado.
     3. Grupo de proteção de Select hello, realce Olá protegido máquina e clique em **serviço de mobilidade de atualização**. Esse botão só está disponível se houver uma versão mais recente do serviço de mobilidade de saudação.

         ![Selecionar Servidor vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/update-mobility.png)

Selecione contas Especifica serviço de mobilidade Olá administrador conta toobe usado tooupdate Olá no servidor de saudação protegida. Clique em Okey e aguarde Olá disparado toocomplete de trabalho.

## <a name="step-6-add-vcenter-servers-or-vsphere-hosts"></a>Etapa 6: Adicionar servidores vCenter ou hosts vSphere
1. Clique em **servidores** > **servidores de configuração** > servidor de configuração >**Adicionar servidor do vCenter** tooadd um host de servidor ou vSphere do vCenter.

    ![Selecionar Servidor vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter.png)
2. Especifique os detalhes de servidor hello ou o host e o servidor de processo de Olá selecione que será usado toodiscovê-lo.

   * Se o servidor do vCenter Olá não está sendo executado na porta 443 do saudação padrão especifique o número da porta Olá no qual Olá servidor vCenter está em execução.
   * servidor de processo Olá deve estar em Olá mesma rede como Olá vCenter server/host vSphere e deve ter o VMware vSphere CLI 5.5.0 instalado.

     ![Configurações do Servidor vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter4.png)
3. Após a conclusão da descoberta de servidor do vCenter hello será listado em detalhes do servidor de configuração de saudação.

    ![Configurações do Servidor vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/add-vcenter2.png)
4. Se você estiver usando uma conta de administrador não tooadd hello ou servidor host, certifique-se de conta Olá tem Olá privilégios a seguir:

   * Contas do vCenter devem ter os privilégios Datacenter, Repositório de dados, Pasta, Host, Rede, Recurso, exibições de Armazenamento, Máquina virtual e vSphere Distributed Switch habilitados.
   * contas do host vSphere devem ter Olá Datacenter, o repositório de dados, pasta, Host, rede, recursos, Máquina Virtual e privilégios do comutador distribuídas vSphere habilitados

## <a name="step-7-create-a-protection-group"></a>Etapa 7: criar um grupo de proteção
1. Abra **Itens Protegidos** > **Grupo de Proteção** > **Criar grupo de proteção**.

    ![Criar grupo de proteção](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg1.png)
2. Em Olá **especificar configurações do grupo de proteção** página especifique um nome para o grupo de saudação e o servidor de configuração de Olá selecione no qual você deseja que o grupo de saudação toocreate.

    ![Configurações do grupo de proteção](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg2.png)
3. Em Olá **especificar configurações de replicação** página Definir configurações de replicação de saudação que serão usadas para todas as máquinas Olá no grupo de saudação.

    ![Replicação do grupo de proteção](./media/site-recovery-vmware-to-azure-classic-legacy/create-pg3.png)
4. Configurações:

   * **Consistência de múltiplas VMs**: caso você ative esta ele cria pontos de recuperação consistentes com o aplicativo compartilhado entre máquinas Olá Olá grupo de proteção. Essa configuração é mais relevante quando todas as máquinas Olá Olá grupo de proteção estão em execução Olá a mesma carga de trabalho. Todos os computadores serão recuperado toohello mesmo ponto de dados. Disponível somente para servidores do Windows.
   * **O limite de RPO**: alerta será gerado quando a replicação de proteção de dados contínuos Olá RPO excede o valor de limite RPO Olá configurado.
   * **Retenção de ponto de recuperação**: especifica uma janela de retenção hello. Computadores protegidos podem ser recuperados tooany ponto nessa janela.
   * **Frequência do instantâneo consistente com aplicativo**: especifica com que frequência são criados os pontos de recuperação que incluam instantâneos consistentes com aplicativos.

Você pode monitorar o grupo de proteção Olá conforme eles são criados em Olá **itens protegidos** página.

## <a name="step-8-set-up-machines-you-want-tooprotect"></a>Etapa 8: Configurar computadores que você deseja tooprotect
Você precisará Olá tooinstall serviço de mobilidade em máquinas virtuais e servidores físicos que você deseja tooprotect. É possível fazer isso de duas formas:

* Enviar por push e instalar serviço de saudação em cada computador saudação do servidor de processo automaticamente.
* Instale manualmente o serviço de saudação.

### <a name="install-hello-mobility-service-automatically"></a>Instalar serviço de mobilidade Olá automaticamente
Quando você adiciona máquinas tooa proteção grupo Olá serviço de mobilidade é automaticamente enviada por push e instalado em cada computador pelo servidor de processo hello.

**Push instalar automaticamente o serviço de mobilidade Olá em servidores Windows:**

1. Instalar atualizações mais recentes de Olá para o servidor de processo Olá, conforme descrito em [etapa 5: instalar as atualizações mais recentes](#step-5-install-latest-updates)e verifique se esse servidor de processo hello está disponível.
2. Certifique-se de há conectividade de rede entre o computador de origem hello e hello servidor de processo e esse computador de origem hello está acessível saudação do servidor de processo.  
3. Configurar Olá Windows firewall tooallow **compartilhamento de arquivos e impressora** e **Windows Management Instrumentation**. Em configurações do Firewall do Windows, selecione a opção de hello "Permitir que um aplicativo ou recurso pelo Firewall" e selecione aplicativos Olá conforme mostrado na imagem de saudação abaixo. Para máquinas que pertencem a você pode configurar a política de firewall Olá com um GPO de domínio de tooa.

    ![Configurações de firewall](./media/site-recovery-vmware-to-azure-classic-legacy/push-firewall.png)
4. instalação por push do Hello conta usada tooperform Olá deve estar no grupo de administradores de saudação na máquina de saudação que deseja tooprotect. Essas credenciais são usadas apenas para a instalação por push do serviço de mobilidade de saudação e você deverá fornecê-los quando você adiciona um grupo de proteção do computador tooa.
5. Se Olá fornecido a conta não é uma conta de domínio, você precisará toodisable controle de acesso de usuário remoto na máquina local hello. toodo este Olá Adicionar entrada de registro LocalAccountTokenFilterPolicy DWORD com um valor de 1 em HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System. entrada de registro de saudação tooadd de uma CLI abra cmd ou o powershell e digite  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .

**Push instalar automaticamente o serviço de mobilidade Olá em servidores Linux:**

1. Instalar atualizações mais recentes de Olá para o servidor de processo Olá, conforme descrito em [etapa 5: instalar as atualizações mais recentes](#step-5-install-latest-updates)e verifique se esse servidor de processo hello está disponível.
2. Certifique-se de há conectividade de rede entre o computador de origem hello e hello servidor de processo e esse computador de origem hello está acessível saudação do servidor de processo.  
3. Certifique-se de conta Olá é um usuário de raiz no servidor do hello origem Linux.
4. Verifique se o arquivo /etc/hosts Olá na fonte Olá Linux server contém entradas que mapeiam Olá host local nome tooIP endereços associados a todas as NICs.
5. Instalar openssh mais recente hello, servidor do openssh, openssl pacotes na máquina de saudação desejado tooprotect.
6. Verifique se SSH está habilitado e em execução na porta 22.
7. Habilite a autenticação de subsistema e a senha SFTP no arquivo de sshd_config de saudação da seguinte maneira:

   * a) Faça logon como raiz.
   * b) na Olá arquivo/etc/ssh/arquivo sshd_config, localizar Olá linha que começa com **PasswordAuthentication**.
   * c) Descomente a linha hello e altere o valor de saudação de "não" muito "Sim".

       ![Mobilidade do Linux](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push.png)
   * d) linha de saudação localizar que começa com o subsistema e remova os comentários de linha de saudação.

       ![Mobilidade por push do Linux](./media/site-recovery-vmware-to-azure-classic-legacy/linux-push2.png)    
8. Certifique-se de que há suporte para a variante de Linux de máquina de origem hello.

### <a name="install-hello-mobility-service-manually"></a>Instalar serviço de mobilidade Olá manualmente
pacotes de software Olá usado tooinstall Olá mobilidade de serviço estão no servidor de processo Olá em C:\pushinstallsvc\repository. Faça logon no servidor de processo hello e cópia Olá adequadas de instalação pacote toohello computador de origem com base na tabela de saudação abaixo:-

| Sistema operacional de origem | Pacote do Serviço de Mobilidade no servidor de processo |
| --- | --- |
| Windows Server (somente 64 bits) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe` |
| CentOS 6.4, 6.5, 6.6 (somente 64 bits) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_RHEL6-64_GA_28Jul2015_release.tar.gz` |
| SUSE Linux Enterprise Server 11 SP3 (somente 64 bits) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_SLES11-SP3-64_GA_28Jul2015_release.tar.gz` |
| Oracle Enterprise Linux 6.4, 6.5 (somente 64 bits) |`C:\pushinstallsvc\repository\Microsoft-ASR_UA_8.4.0.0_OL6-64_GA_28Jul2015_release.tar.gz` |

**Olá tooinstall serviço de mobilidade manualmente no Windows server**, Olá a seguir:

1. Saudação de cópia **ASR_UA_8.4.0.0_Windows_GA_28Jul2015_release.exe Microsoft** pacote do caminho do diretório de servidor de processo de saudação listadas na tabela de saudação acima toohello da máquina de origem.
2. Instale serviço de mobilidade Olá executando Olá executável no computador de origem de saudação.
3. Siga as instruções de instalador de saudação.
4. Selecione **serviço de mobilidade** como função hello e clique em **próximo**.

    ![Instalar serviço de mobilidade](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install.png)
5. Deixe o diretório de instalação hello como caminho de instalação padrão hello e clique em **instalar**.
6. Em **configuração do agente de Host** especificar endereço IP de saudação e a porta HTTPS saudação do servidor de configuração.

   * Se você estiver se conectando pela Olá internet especificar Olá endereço IP virtual público e o ponto de extremidade HTTPS público como porta hello.
   * Se você estiver se conectando através de VPN especifique o endereço IP interno de saudação e 443 para a porta de saudação. Deixe marcada a opção **Usar HTTPS** .

     ![Instalar serviço de mobilidade](./media/site-recovery-vmware-to-azure-classic-legacy/ms-install2.png)
7. Especifique a senha de servidor de configuração de saudação e clique em **Okey** tooregister Olá serviço de mobilidade com o servidor de configuração de saudação.

**toorun da linha de comando hello:**

1. Copiar senha de saudação do arquivo toohello CX hello "C:\connection.passphrase" no servidor de saudação e execute este comando. Em nosso exemplo CX i 104.40.75.37 e hello porta HTTPS é 62519:

    `C:\Microsoft-ASR_UA_8.2.0.0_Windows_PREVIEW_20Mar2015_Release.exe" -ip 104.40.75.37 -port 62519 -mode UA /LOG="C:\stdout.txt" /DIR="C:\Program Files (x86)\Microsoft Azure Site Recovery" /VERYSILENT  /SUPPRESSMSGBOXES /norestart  -usesysvolumes  /CommunicationMode https /PassphrasePath "C:\connection.passphrase"`

**Instalar serviço de mobilidade Olá manualmente em um servidor Linux**:

1. Copie o arquivo de tar apropriado de saudação com base na tabela de saudação acima, do computador de origem toohello do servidor de processo hello.
2. Abrir um programa de shell e extrair o caminho local de tooa Olá de arquivo tar compactado, executando`tar -xvzf Microsoft-ASR_UA_8.2.0.0*`
3. Criar um arquivo passphrase.txt no toowhich de diretório local Olá você extraiu conteúdo de saudação do arquivo morto de tar Olá inserindo  *`echo <passphrase> >passphrase.txt`*  do shell.
4. Instalar serviço de mobilidade Olá inserindo  *`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`* .
5. Especifique a porta e endereço IP de saudação:

   * Se você estiver se conectando o servidor de configuração toohello Olá internet especificar Olá configuração servidor virtual endereço IP público e ponto de extremidade HTTPS público em `<IP address>` e `<port>`.
   * Se você estiver se conectando através de uma conexão VPN especifique 443 e endereço IP interno de saudação.

**toorun da linha de comando Olá**:

1. Copiar senha de saudação do arquivo toohello CX hello "passphrase.txt" no servidor de saudação e executar esse comando. Em nosso exemplo CX i 104.40.75.37 e hello porta HTTPS é 62519:

tooinstall em um servidor de produção:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

tooinstall no servidor de destino hello:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 62519 -s y -c https -P passphrase.txt

> [!NOTE]
> Quando você adiciona o grupo de proteção de tooa máquinas que já estão executando uma versão apropriada do serviço de mobilidade do hello, em seguida, a instalação por push Olá será ignorada.
>
>

## <a name="step-9-enable-protection"></a>Etapa 9: habilitar proteção
proteção tooenable adicionar máquinas virtuais e o grupo de proteção tooa servidores físicos. Antes de começar, observe que:

* Máquinas virtuais são descobertas a cada 15 minutos e pode demorar até too15 minutos para que eles tooappear no Azure Site Recovery após a descoberta.
* Alterações de ambiente na máquina virtual de saudação (como instalação de ferramentas do VMware) também podem demorar até too15 minutos toobe atualizado na recuperação de Site.
* Você pode verificar a saudação do último descoberto tempo em Olá **último contato em** campo servidor/ESXi host vCenter Olá Olá **servidores de configuração** página.
* Se você tiver um grupo de proteção já criado e adicionar um host de servidor ou ESXi vCenter depois disso, leva quinze minutos para hello Azure Site Recovery portal toorefresh em máquinas virtuais toobe listados no hello **adicionar grupo de proteção de tooa de máquinas**  caixa de diálogo.
* Se você quiser tooproceed imediatamente ao adicionar grupo de tooprotection máquinas sem aguardar a descoberta agendada Olá, realce o servidor de configuração de saudação (não clique nele) e clique em Olá **atualização** botão.
* Quando você adiciona máquinas virtuais ou grupo de proteção tooa máquinas físicas, servidor de processo Olá envia automaticamente e instala o serviço de mobilidade Olá no servidor de origem Olá hello ainda não estiver instalado.
* Para o mecanismo de envio automático de saudação toowork Certifique-se de configurar seus computadores protegidos conforme descrito na etapa anterior hello.

Adicione computadores como se segue:

1. Clique em **Itens Protegidos** > **Grupo de Proteção** > **Computadores** > **Adicionar Computadores**. Como prática recomendada, é recomendável que os grupos de proteção devem ser espelhada suas cargas de trabalho para que você adicionar máquinas que executam um aplicativo específico toohello mesmo grupo.
2. Em **selecionar máquinas virtuais** se você estiver protegendo servidores físicos, em Olá **adicionar máquinas físicas** Assistente para fornecer o endereço IP de saudação e o nome amigável. Em seguida, selecione família de sistemas operacionais de saudação.

    ![Adicionar Servidor vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/physical-protect.png)
3. Em **selecionar máquinas virtuais** se você estiver protegendo as máquinas virtuais VMware, selecione um servidor vCenter que gerencia suas máquinas virtuais (Olá EXSi host ou em que estejam em execução) e, em seguida, selecione as máquinas de saudação.

    ![Adicionar Servidor vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/select-vms.png)    
4. Em **especificar recursos de destino** Selecione servidores de destino mestre hello e toouse de armazenamento para replicação e se Olá configurações devem ser usadas para todas as cargas de trabalho. Selecione [conta de armazenamento Premium](../storage/common/storage-premium-storage.md) ao configurar a proteção para cargas de trabalho que exigem alto desempenho de e/s consistente e baixa latência em ordem toohost e/s intensivas cargas de trabalho. Se você quiser toouse uma conta de armazenamento Premium para os discos de carga de trabalho, você precisa toouse Olá destino mestre da série DS. Mas você não pode usar discos de Armazenamento Premium com Destino mestre que não pertençam às séries DS.

   > [!NOTE]
   > Não há suporte para movimentação de saudação de contas de armazenamento criadas usando Olá [novo portal do Azure](../storage/common/storage-create-storage-account.md) entre grupos de recursos.
   >
   >

    ![Servidor vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/machine-resources.png)
5. Em **especificar contas** selecione conta Olá que deseja toouse para instalar o serviço de mobilidade Olá em computadores protegidos. as credenciais de conta de saudação são necessários para a instalação automática do serviço de mobilidade de saudação. Se não for possível selecionar uma conta, configure uma conforme descrito na Etapa 2. Observe que essa conta não pode ser acessada pelo Azure. Para o Windows a conta de saudação do servidor deve ter privilégios de administrador no servidor de origem de saudação. Para Linux conta Olá deve ser a raiz.

    ![Credenciais do Linux](./media/site-recovery-vmware-to-azure-classic-legacy/mobility-account.png)
6. Clique em toofinish de marca de seleção Olá adicionando máquinas toohello proteção toostart e grupo de replicação inicial para cada máquina. Você pode monitorar o status de saudação **trabalhos** página.

    ![Adicionar Servidor vCenter](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs2.png)
7. Além disso, você pode monitorar o status de proteção clicando em **Itens Protegidos** > nome do grupo de proteção > **Máquinas Virtuais**. Após a conclusão da replicação inicial máquinas Olá estão sincronizando dados mostrarão **protegidos** status.

    ![Trabalhos da máquina virtual](./media/site-recovery-vmware-to-azure-classic-legacy/pg-jobs.png)

### <a name="set-protected-machine-properties"></a>Definir propriedades de computador protegido
1. Quando um computador tem o status **Protegido** , você pode configurar as respectivas propriedades de failover. Em detalhes do grupo de proteção Olá selecione Olá Olá máquina e abra **configurar** guia.
2. Você pode modificar o nome de saudação que será dado toohello máquina no Azure após o failover e hello tamanho de máquina virtual do Azure. Você também pode selecionar máquina de Olá Olá rede Azure toowhich será conectada após o failover.

   > [!NOTE]
   > [Migração de redes](../resource-group-move-resources.md) em recursos grupos dentro Olá a mesma assinatura ou em assinaturas não é há suporte para redes usados para implantar a recuperação de Site.
   >
   >

    ![Definir propriedades da máquina virtual](./media/site-recovery-vmware-to-azure-classic-legacy/vm-props.png)

Observe que:

* nome de saudação do hello máquina do Azure deve atender aos requisitos do Azure.
* Por padrão as máquinas virtuais replicadas no Azure não estão conectado tooan rede do Azure. Se você quiser que as máquinas virtuais replicadas toocommunicate Certifique-se de tooset Olá mesma rede do Azure para eles.
* Se você redimensionar um volume em uma máquina virtual VMware ou um servidor físico, ele entrará em estado crítico. Se você precisar de tamanho de saudação toomodify, Olá a seguir:

  * um) altere a configuração de tamanho de saudação.
  * b) na Olá **máquinas virtuais** , selecione a máquina virtual de saudação e clique em **remover**.
  * c) em **Remover Máquina Virtual** Selecione opção Olá **desabilitar proteção (use para a recuperação de análise e redimensionamento de volume)**. Esta opção desabilita a proteção, mas retém os pontos de recuperação Olá no Azure.

      ![Definir propriedades da máquina virtual](./media/site-recovery-vmware-to-azure-classic-legacy/remove-vm.png)
  * d), reabilite a proteção para a máquina virtual de saudação. Quando você reabilitar a proteção de dados Olá para o volume de saudação redimensionada será tooAzure transferido.

## <a name="step-10-run-a-failover"></a>Etapa 10: executar um failover
No momento, você pode executar somente failovers não planejados para as máquinas virtuais VMware e os servidores físicos protegidos. Observe o seguinte hello:

* Antes de você iniciar um failover, certifique-se de que servidores de destino mestre e configuração Olá estão em execução e íntegro. Caso contrário, o failover falhará.
* As máquinas de origem não são desligadas como parte de um failover não planejado. Executar um failover não planejado interrompe a replicação de dados para servidores de saudação protegida. Você precisa toodelete Olá máquinas saudação do grupo de proteção e adicioná-los novamente em ordem toostart protegendo máquinas novamente após hello failover não planejado.
* Se você desejar toofail sem perder dados, certifique-se de que Olá máquinas de virtuais de site primário estão desativadas antes de você iniciar o failover de saudação.

1. Em Olá **planos de recuperação** página e adicionar um plano de recuperação. Especificar detalhes do plano de saudação e selecione **Azure** como destino de saudação.

    ![Configurar plano de recuperação](./media/site-recovery-vmware-to-azure-classic-legacy/rplan1.png)
2. Em **Selecionar Máquina Virtual** selecione um grupo de proteção e, em seguida, selecione máquinas no plano de recuperação Olá grupo tooadd toohello. [Leia mais](site-recovery-create-recovery-plans.md) sobre planos de recuperação.

    ![Adicionar máquinas virtuais](./media/site-recovery-vmware-to-azure-classic-legacy/rplan2.png)
3. Se necessário você pode personalizar toocreate grupos do plano de saudação e ordem de saudação sequência na qual máquinas na recuperação de saudação plano fizeram failover. Você também pode adicionar prompts para ações manuais e scripts. Olá scripts quando recuperar tooAzure pode ser adicionado usando [Runbooks de automação do Azure](site-recovery-runbook-automation.md).
4. Em Olá **planos de recuperação** página plano Olá selecione e clique em **Failover não planejado**.
5. Em **confirmar Failover** Verifique a direção do failover hello (tooAzure) e selecione Olá toofail de ponto de recuperação em para.
6. Aguarde Olá toocomplete de trabalho de failover e, em seguida, verifique se Olá failover funcionou como esperado e que Olá replicadas inicial de máquinas virtuais com êxito no Azure.

## <a name="step-11-fail-back-failed-over-machines-from-azure"></a>Etapa 11: fazer failback de computadores do Azure
[Saiba mais](site-recovery-failback-azure-to-vmware-classic-legacy.md) sobre como toobring sua falha em máquinas em execução no Azure volta tooyour ambiente de local.

## <a name="manage-your-process-servers"></a>Gerenciar servidores de processo
servidor de processo Olá envia o servidor de destino mestre de toohello de dados de replicação no Azure e descobre o novo servidor do vCenter VMware máquinas virtuais tooa adicionado. Olá circunstâncias a seguir, talvez seja servidor de processo Olá toochange em sua implantação:

* Se o servidor de processo atual Olá cair
* Se o pontos de recuperação objetivo (RPO) aumenta a nível inaceitável tooan para sua organização.

Se for necessário que você pode mover a replicação de alguns ou todos os seu VMware local virtual Olá máquinas e tooa de servidores físicos diferente processo de servidor. Por exemplo:

* **Falha de**— se um servidor de processo falha ou não estiver disponível, você pode mover servidor de processo de tooanother de replicação do computador protegido. Metadados da máquina de origem de saudação e máquina de réplica serão movidos toohello novo servidor de processo e dados é sincronizada novamente. novo servidor de processo Olá conectará automaticamente a descoberta automática do tooperform toohello vCenter server. Você pode monitorar o estado de saudação de servidores de processo no painel do Site Recovery Olá.
* **Tooadjust RPO de balanceamento de carga**— para melhor balanceamento você pode selecionar um servidor de processo diferente no portal de recuperação de Site hello e mova a replicação de um ou mais tooit máquinas para balanceamento de carga manual. Nesse caso, os metadados de origem selecionado hello e máquinas de réplica são movido toohello novo servidor de processo. servidor de processo Olá original permanece conectado toohello vCenter server.

### <a name="monitor-hello-process-server"></a>Servidor de processo de saudação do monitor
Se um servidor de processo está em estado crítico, que um aviso de status será exibido na Olá painel da recuperação de Site. Você pode clicar na guia eventos do hello status tooopen hello e, em seguida, fazer drill down toospecific trabalhos na guia trabalhos de saudação.

### <a name="modify-hello-process-server-used-for-replication"></a>Modificar o servidor de processo Olá usado para replicação
1. Abra **Servidores** > **Servidores de Configuração** > servidor de configuração > **Detalhes do Servidor**.
2. Clique em **servidores de processo** > **alterar servidor de processo** próximo servidor toohello toomodify desejado.

    ![Alterar o Servidor de processo 1](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps1.png)
3. Em **alterar servidor de processo** > **servidor de processo de destino** selecione Olá novo servidor, você deseja toouse e, em seguida, selecione Olá de máquinas virtuais que você deseja tooreplicate toohello novo servidor. Clique em Olá informações ícone próximo toohello nome do servidor para obter detalhes de espaço livre e a memória usada. Olá médio espaço que será necessário tooreplicate cada máquina virtual selecionada toohello novo servidor de processo é exibida toohelp que você fizer as decisões de carga.

    ![Alterar o Servidor de processo 2](./media/site-recovery-vmware-to-azure-classic-legacy/change-ps2.png)
4. Clique em toobegin de marca de seleção Olá replicando toohello novo servidor de processo. Observe que se você remover todas as máquinas virtuais de um servidor de processo que foi crítico deve não exibir um aviso crítico no painel de saudação.

## <a name="third-party-software-notices-and-information"></a>Avisos e informações de software de terceiros
Do Not Translate or Localize

software Hello e firmware em execução no hello produto da Microsoft ou o serviço se baseia em ou incorpora material dos Olá projetos listados abaixo (coletivamente, "código de terceiros").  A Microsoft está Olá autor original não Olá código de terceiros.  Olá original de direitos autorais e licença, sob a qual a Microsoft recebeu esse código de terceiros, estão definidos abaixo.

informações de saudação na seção A é em relação ao código de terceiros, componentes de projetos de saudação listados abaixo. Such licenses and information are provided for informational purposes only.  Esse código de terceiros está sendo tooyou relicensed pela Microsoft em termos de produto da Microsoft hello ou o serviço de licenciamento de software da Microsoft.  

informações de saudação na seção B for referente a componentes de código de terceiros que estão sendo feitas tooyou disponível pela Microsoft em termos de licenciamento original hello.

arquivo completo Olá pode ser encontrado em Olá [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.
