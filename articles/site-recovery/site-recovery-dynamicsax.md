---
title: "aaaReplicate uma implantação do Dynamics AX de várias camada usando o Azure Site Recovery | Microsoft Docs"
description: Este artigo descreve como tooreplicate e proteger usando o Azure Site Recovery do Dynamics AX
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a>Replicar um aplicativo do Dynamics AX de várias camadas usando o Azure Site Recovery

## <a name="overview"></a>Visão geral


O Microsoft Dynamics AX é uma solução ERP mais popular Olá entre o processo de toostandardized empresas em locais, gerenciar recursos e simplificar a conformidade. Considerando que o aplicativo hello é organização tooan críticos de negócios é muito importante toobe-se de que se qualquer desastre, aplicativo deve estar em execução no tempo mínimo.

Hoje, o Microsoft Dynamics AX não fornece nenhuma funcionalidade integrada de recuperação de desastre. O Microsoft Dynamics AX consiste em vários componentes de servidor como banco de dados do servidor de objeto de aplicativo, Active Directory (AD), SQL Server, SharePoint Server, recuperação de desastres de saudação do Reporting Server etc toomanage de cada um desses componentes manualmente é não apenas cara, mas também propensas a erros.

Este artigo explica em detalhes sobre como você pode criar uma solução de recuperação de desastre para seu aplicativo Dynamics AX usando o [Azure Site Recovery](site-recovery-overview.md). Ele também aborda failovers planejados/não planejados/de teste usando o plano de recuperação com um único clique, configurações com suporte e pré-requisitos.
A solução de recuperação de desastre baseada no Azure Site Recovery é totalmente testada, certificada e recomendada pelo Microsoft Dynamics AX.



## <a name="prerequisites"></a>Pré-requisitos

Implementação de recuperação de desastres para o aplicativo Dynamics AX usando o Azure Site Recovery requer Olá concluídos os pré-requisitos a seguir.

•   Uma implantação local do Dynamics AX foi configurada

•   Um cofre dos Serviços do Azure Site Recovery foi criado em uma assinatura do Microsoft Azure

• Se seu site de recuperação do Azure é executar Olá avaliação de prontidão de máquina Virtual do Azure ferramenta tooensure VMs que são compatíveis com VMs do Azure e serviços de recuperação de Site do Azure


## <a name="site-recovery-support"></a>Suporte do Site Recovery

Para finalidade de saudação de criação deste artigo, as máquinas virtuais VMware com 2012R3 do Dynamics AX no Windows Server 2012 R2 Enterprise foram usadas. Como a replicação de recuperação de site é independente do aplicativo, fornecidas recomendações Olá aqui são toohold esperado nos cenários a seguir também.

### <a name="source-and-target"></a>Origem e destino

**Cenário** | **site secundário tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Sim | Sim
**VMware** | Sim | Sim
**Servidor físico** | Sim | Sim

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a>Habilitar a DR do aplicativo Dynamics AX usando o Azure Site Recovery
### <a name="protect-your-dynamics-ax-application"></a>Proteger o aplicativo Dynamics AX
Cada componente do hello Dynamics AX necessidades toobe protegido tooenable Olá aplicativo completo replicação e a recuperação. Esta seção aborda:

**1. Proteção do Active Directory**

**2. Proteção da Camada SQL**

**3. Proteção de Aplicativo e as Camadas da Web**

**4. Configuração de rede**

**5. Plano de Recuperação**

### <a name="1-setup-ad-and-dns-replication"></a>1. Instalação do AD e replicação de DNS

Active Directory é necessário no local de recuperação de desastres Olá para toofunction de aplicativo do Dynamics AX. Há duas opções recomendadas com base em complexidade Olá Olá do local do ambiente de cliente.

**Opção 1**

Se Olá cliente tiver um pequeno número de aplicativos e um único controlador de domínio para seu todo site local e será estar falhando em todo o site Olá juntos, em seguida, é recomendável usar a replicação de ASR tooreplicate Olá DC máquina toosecondary site ( aplicável para o Site tooSite e tooAzure do Site).

**Opção 2**

Se cliente Olá tem um grande número de aplicativos e está em execução para uma floresta do Active Directory e será failover alguns aplicativos cada vez, é recomendável configurar um controlador de domínio no site Olá DR (site secundário ou no Azure).

Consulte também[guia complementar de tornar um controlador de domínio disponível no site de recuperação de desastres](site-recovery-active-directory.md). Para o restante deste documento, presumiremos que um DC está disponível no site de DR.

### <a name="2-setup-sql-server-replication"></a>2. Configurar a Replicação do SQL Server
Consulte o guia de toocompanion para orientações técnicas detalhadas sobre Olá recomendado a opção para proteger [SQL camadas](site-recovery-sql.md).

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a>3. Habilitar a proteção do cliente Dynamics AX e VMs AOS
Execute a configuração do Azure Site Recovery relevante com base em Olá VMs implantadas em [Hyper-V](site-recovery-hyper-v-site-to-azure.md) ou na [VMware](site-recovery-vmware-to-azure.md).

> [!TIP]
> Tooconfigure de frequência consistente de falha recomendado é de 15 minutos.
>

Olá abaixo instantâneo mostra o status de proteção de saudação de VMs de componente do Dynamics no cenário de proteção 'TooAzure de site VMware'.
![Itens protegidos ](./media/site-recovery-dynamics-ax/protecteditems.png)

### <a name="4-configure-networking"></a>4. Configurar Rede
Definir as Configurações de Rede e de Computação de VM

Olá AX e do cliente AOS VMs definir configurações de rede no Azure Site Recovery para que redes VM Olá toohello anexado à direita DR rede após o failover. Certifique-se de rede de DR Olá para essas camadas é roteável toohello SQL camadas.

Você pode selecionar Olá VM em Olá replicadas configurações de rede itens tooconfigure Olá conforme mostrado no instantâneo de saudação abaixo.

* Para servidores do AOS selecione conjunto de disponibilidade correto de saudação.

* Se você estiver usando um endereço IP estático, especifique Olá IP que você deseja Olá tootake de máquina virtual em Olá **IP de destino** campo ![as configurações de rede](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)



### <a name="5-creating-a-recovery-plan"></a>5. Criar um plano de recuperação

Você pode criar um plano de recuperação no processo de failover do Azure Site Recovery tooautomate hello. Adicione camada de aplicativo e a camada da web em Olá plano de recuperação. Ordene-as em diferentes grupos de forma que Olá front-end desligamento antes da camada de aplicativo.

1)  Selecione o cofre do Azure Site Recovery Olá em sua assinatura e clique no bloco 'Planos de recuperação'.

2)  Clique em '+ Plano de recuperação' e especifique um nome.

3)  Selecione hello 'Fonte' e 'Target'. destino de saudação pode ser o site do Azure ou secundário. Caso escolha do Azure, você deve especificar o modelo de implantação de saudação

![Criar Plano de Recuperação](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  Selecione Olá AOS e um plano de recuperação do cliente VMs toohello e clique em ✓.
![Criar Plano de Recuperação](./media/site-recovery-dynamics-ax/selectvms.png)


![Plano de Recuperação](./media/site-recovery-dynamics-ax/recoveryplan.png)

Você pode personalizar o plano de recuperação de saudação para o aplicativo Dynamics AX adicionando várias etapas, conforme detalhado abaixo. Olá acima instantâneo mostra Olá plano de recuperação completo depois de adicionar todas as etapas de saudação.

*Etapas:*

*1. Etapas de failover do SQL Server*

Consulte também['Solução de recuperação de desastres do SQL Server'](site-recovery-sql.md) guia complementar para obter detalhes sobre o servidor de tooSQL específica de etapas de recuperação.

*2. Failover de grupo 1: Failover Olá AOS VMs*

Certifique-se de que o ponto de recuperação de saudação selecionado é mais próximo possível toohello banco de dados PIT mas não em frente.

*3. Script: Balanceador de carga adicionar (somente E-A)* adicionar um script (por meio da automação do Azure) depois do grupo AOS VM surge tooadd um tooit de Balanceador de carga. Você pode usar um script toodo essa tarefa. Consulte o artigo [como tooadd balanceador de carga de aplicativo multicamadas DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)

*4. Failover de grupo 2: Failover de cliente do AX Olá VMs.*
Failover Olá web da camada de máquinas virtuais como parte do plano de recuperação de saudação.


### <a name="doing-a-test-failover"></a>Executar um failover de teste

Consulte too'AD DR Solution ' e 'Solução de recuperação de desastres do SQL Server' os guias complementares para tooAD específicas de considerações e o SQL server respectivamente durante o Failover de teste.

1.  Vá tooAzure portal e selecione seu Cofre de recuperação de Site.
2.  Clique no plano de recuperação de saudação criado do Dynamics AX.
3.  Clique em 'Failover de Teste'.
4.  Selecione o processo de failover de teste Olá Olá rede virtual toostart.
5.  Após ambiente secundário hello, você pode executar a validação.
6.  Depois que as validações de saudação estiverem concluídas, você pode selecionar 'Validações Concluir' e ambiente de failover de teste hello serão limpos.

Execute [neste guia](site-recovery-test-failover-to-azure.md) toodo um failover de teste.

### <a name="doing-a-failover"></a>Executar um failover

1.  Vá tooAzure portal e selecione seu Cofre de recuperação de Site.
2.  Clique no plano de recuperação de saudação criado do Dynamics AX.
3.  Clique em 'Failover' e selecione 'Failover'.
4.  Selecione a rede de destino hello e clique em processo de failover do ✓ toostart hello.

Siga [este guia](site-recovery-failover.md) quando estiver realizando um failover.

### <a name="perform-a-failback"></a>Executar um Failback

Consulte too'SQL solução de recuperação de desastres do servidor ' guia complementar para o servidor de tooSQL específicas de considerações durante o Failback.

1.  Vá tooAzure portal e selecione seu Cofre de recuperação de Site.
2.  Clique no plano de recuperação de saudação criado do Dynamics AX.
3.  Clique em 'Failover' e selecione o failover.
4.  Clique em 'Alterar Direção'.
5.  Selecionar opções apropriadas Olá - sincronização de dados e opções de criação de VM
6.  Clique em ✓ toostart Olá '' Failback' processo.


Siga [estas diretrizes](site-recovery-failback-azure-to-vmware.md) quando estiver realizando um failback.

##<a name="summary"></a>Resumo
Com o Azure Site Recovery, você pode criar um plano totalmente automatizado de recuperação de desastre para seu aplicativo do Dynamics AX. Você pode iniciar failover hello dentro de segundos de qualquer lugar no hello evento de interrupção e obter o aplicativo hello em funcionamento em minutos.

## <a name="next-steps"></a>Próximas etapas
Leitura [que cargas de trabalho posso proteger?](site-recovery-workload.md) toolearn mais sobre como proteger as cargas de trabalho com o Azure Site Recovery.
