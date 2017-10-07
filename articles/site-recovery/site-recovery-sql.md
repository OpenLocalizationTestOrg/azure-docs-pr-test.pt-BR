---
title: aplicativos de aaaReplicate com o SQL Server e o Azure Site Recovery | Microsoft Docs
description: Este artigo descreve como tooreplicate SQL Server usando o Azure Site Recovery para recursos de desastres do SQL Server.
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: pratshar
ms.openlocfilehash: 99755f2cd2f7e924071f1e230ac4a0bda88f0a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-sql-server-using-sql-server-disaster-recovery-and-azure-site-recovery"></a>Proteger o SQL Server usando a recuperação de desastre do SQL Server e o Azure Site Recovery

Este artigo descreve como tooprotect saudação do SQL Server back-end de um aplicativo usando uma combinação de continuidade de negócios do SQL Server e tecnologias de (BCDR) de recuperação de desastres, e [do Azure Site Recovery](site-recovery-overview.md).

Antes de começar, verifique se você entendeu as funcionalidades de recuperação de desastre do SQL Server, incluindo o clustering de failover, grupos de disponibilidade do AlwaysOn, espelhamento de banco de dados e envio de log.


## <a name="sql-server-deployments"></a>Implantações do SQL Server

Muitas cargas de trabalho usam o SQL Server como uma base, e ele pode ser integrado com aplicativos, como o SharePoint, Dynamics e SAP, tooimplement os serviços de dados.  O SQL Server pode ser implantado de várias maneiras:

* **SQL Server autônomo**: o SQL Server e todos os bancos de dados são hospedados em um único computador (físico ou virtual). Quando virtualizado, o cluster de host é usado para alta disponibilidade local. A alta disponibilidade no nível de convidado não é implementada.
* **Instâncias de cluster de Failover (FCI do Always On) do SQL Server**: dois ou mais nós executando o SQL Server com instâncias de discos compartilhados são configurados em um cluster de Failover do Windows. Se um nó estiver inativo, cluster Olá failover do SQL Server tooanother instância. Essa configuração é normalmente usada tooimplement alta disponibilidade em um site primário. Esta implantação não protege contra falha ou interrupção na camada de armazenamento compartilhado hello. Um disco compartilhado pode ser implementado usando ISCSI, Fiber Channel ou vhdx compartilhado.
* **Grupos de Disponibilidade AlwaysOn do SQL**: dois ou mais nós podem ser configurados em um cluster sem compartilhamento, com bancos de dados SQL Server configurados em um grupo de disponibilidade, com replicação síncrona e failover automático.

 Este artigo aproveita Olá nativo tecnologias de recuperação de desastres do SQL para a recuperação de site remoto do tooa de bancos de dados a seguir:

* SQL grupos de disponibilidade AlwaysOn, tooprovide para recuperação de desastres do SQL Server 2012 ou 2014 Enterprise editions.
* Espelhamento de banco de dados SQL no modo de alta segurança para SQL Server Standard Edition (qualquer versão), ou para o SQL Server 2008 R2.

## <a name="site-recovery-support"></a>Suporte do Site Recovery

### <a name="supported-scenarios"></a>Cenários com suporte
Recuperação de site pode proteger o SQL Server, como resumido na tabela de saudação.

**Cenário** | **site secundário tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Sim | Sim
**VMware** | Sim | Sim
**Servidor físico** | Sim | Sim

### <a name="supported-sql-server-versions"></a>Versões do SQL Server com suporte
Essas versões do SQL Server têm suporte para cenários de saudação com suporte:

* SQL Server 2016 Enterprise e Standard
* SQL Server 2014 Enterprise e Standard
* SQL Server 2012 Enterprise e Standard
* SQL Server 2008 R2 Enterprise e Standard

### <a name="supported-sql-server-integration"></a>Integração do SQL Server com suporte

Recuperação de site pode ser integrada às tecnologias de BCDR do SQL Server native resumidas na tabela hello, tooprovide uma solução de recuperação de desastres.

**Recurso** | **Detalhes** | **SQL Server** |
--- | --- | ---
**Grupo de disponibilidade Sempre Ativo** | Várias instâncias autônomas do SQL Server cada uma executando em um cluster de failover com vários nós.<br/><br/>Os bancos de dados podem ser agrupados em grupos de failover, que podem ser copiados (espelhados) em instâncias do SQL Server, de modo que não exista a necessidade de armazenamento compartilhado.<br/><br/>Fornece a recuperação de desastres entre um site primário e um ou mais sites secundários. Dois nós podem ser configurados em um cluster sem compartilhamento, com bancos de dados do SQL Server configurados em um grupo de disponibilidade, com replicação síncrona e failover automático. | SQL Server 2014 & 2012 Enterprise Edition
**Clustering de failover (FCI AlwaysOn)** | O SQL Server aproveita o Clustering de Failover do Windows para proporcionar a alta disponibilidade de cargas de trabalho local do SQL Server.<br/><br/>Os nós que executam instâncias do SQL Server com discos compartilhados são configurados em um cluster de failover. Se uma instância está inoperante cluster Olá failover toodifferent um.<br/><br/>cluster de saudação não protege contra falhas ou interrupções no armazenamento compartilhado. disco compartilhado Olá pode ser implementado com o iSCSI, Fibre channel ou compartilhados VHDXs. | Edições do SQL Server Enterprise<br/><br/>SQL Server Standard edition (apenas para nós tootwo limitado)
**Espelhamento de banco de dados (modo de alta segurança)** | Protege uma único banco de dados tooa única secundário cópia. Disponível nos modos de replicação de alta segurança (síncrona) e de alto desempenho (assíncrono). Não requer um cluster de failover. | SQL Server 2008 R2<br/><br/>Todas as edições do SQL Server Enterprise
**SQL Server autônomo** | saudação do SQL Server e banco de dados são hospedados em um único servidor (físico ou virtual). Clustering do host é usado para alta disponibilidade, se o servidor de saudação é virtual. Sem alta disponibilidade no nível do convidado. | Edição Enterprise ou Standard

## <a name="deployment-recommendations"></a>Recomendações de implantação

Esta tabela resume nossas recomendações para a integração de tecnologias de BCDR do SQL Server com a Recuperação de Site.

| **Versão** | **Edição** | **Implantação** | **Local de tooon local** | **TooAzure local** |
| --- | --- | --- | --- | --- |
| SQL Server 2014 ou 2012 |Enterprise |Instância do cluster de failover |Grupos de disponibilidade AlwaysOn |Grupos de disponibilidade AlwaysOn |
|| Enterprise |Grupos de disponibilidade AlwaysOn para alta disponibilidade |Grupos de disponibilidade AlwaysOn |Grupos de disponibilidade AlwaysOn | |
|| Standard |FCI (instância do cluster de failover) |Replicação de Recuperação de Site com espelhamento local |Replicação de Recuperação de Site com espelhamento local | |
|| Enterprise ou Standard |Autônomo |Replicação de recuperação de site |Replicação de recuperação de site | |
| SQL Server 2008 R2 ou 2008 |Enterprise ou Standard |FCI (instância do cluster de failover) |Replicação de Recuperação de Site com espelhamento local |Replicação de Recuperação de Site com espelhamento local |
|| Enterprise ou Standard |Autônomo |Replicação de recuperação de site |Replicação de recuperação de site | |
| SQL Server (qualquer versão) |Enterprise ou Standard |Instância do cluster de failover – aplicativo DTC |Replicação de recuperação de site |Sem suporte |

## <a name="deployment-prerequisites"></a>Pré-requisitos de implantação

* Uma implantação local do SQL Server executando uma versão com suporte do SQL Server. Normalmente, também é necessário ter um Active Directory para o SQL Server.
* requisitos de saudação do hello cenário que você deseja toodeploy. Saiba mais sobre os requisitos de suporte para [replicação tooAzure](site-recovery-support-matrix-to-azure.md) e [local](site-recovery-support-matrix.md), e [os pré-requisitos de implantação](site-recovery-prereq.md).
* tooset a recuperação no Azure, Olá execução [avaliação de prontidão de máquina Virtual do Azure](http://www.microsoft.com/download/details.aspx?id=40898) ferramenta nas máquinas virtuais do SQL Server, toomake-se de que eles são compatíveis com o Azure e recuperação de Site.

## <a name="set-up-active-directory"></a>Configurar o Active Directory

Instalar o Active Directory, no site de recuperação secundário hello, para SQL Server toorun corretamente.

* **Empresa de pequena porte**— com um pequeno número de aplicativos e o controlador de domínio único para Olá no site local, se você quiser toofail em todo o site Olá, é recomendável usar o controlador de domínio do Site Recovery replicação tooreplicate Olá datacenter secundário toohello ou tooAzure.
* **Empresa de médio toolarge**— se você tiver um grande número de aplicativos, uma floresta do Active Directory, e você deseja toofail a tecla aplicativo ou carga de trabalho, é recomendável que você configurar no datacenter secundário hello, ou em um controlador de domínio adicional Azure. Se você estiver usando o AlwaysOn disponibilidade grupos toorecover tooa site remoto, é recomendável que configurar outro controlador de domínio adicionais no site secundário hello ou no Azure, toouse Olá recuperado instância do SQL Server.

instruções Olá neste artigo presumem que um controlador de domínio está disponível no local secundário hello. [Ler mais](site-recovery-active-directory.md) sobre como proteger o Active Directory com o Site Recovery.


## <a name="integrate-with-sql-server-always-on-for-replication-tooazure"></a>Integrar com o SQL Server Always On para tooAzure de replicação

Aqui está o que você precisa toodo:

1. Importar scripts para sua conta da Automação do Azure. Contém scripts de saudação toofailover grupo de disponibilidade do SQL em um [máquina virtual do Gerenciador de recursos](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAG.ps1) e um [máquina de virtual clássico](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/asr-automation-recovery/scripts/ASR-SQL-FailoverAGClassic.ps1).

    [![Implantar tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)


1. Adicione FailoverAG de SQL de ASR como uma ação antes do primeiro grupo Olá Olá do plano de recuperação.

1. Siga instruções Olá disponíveis no hello script toocreate um nome de saudação do tooprovide variável de automação Olá de grupos de disponibilidade.

### <a name="steps-toodo-a-test-failover"></a>Etapas toodo um failover de teste

O SQL AlwaysOn não dá suporte nativo ao failover de teste. Portanto, é recomendável seguir hello:

1. Configurar [Backup do Azure](../backup/backup-azure-vms.md) na máquina virtual Olá que hospeda a réplica do grupo de disponibilidade Olá no Azure.

1. Antes de disparar um failover de teste do plano de recuperação Olá, recupere máquina virtual de saudação do backup de Olá feito na etapa anterior Olá.

    ![Restaurar do Backup do Azure ](./media/site-recovery-sql/restore-from-backup.png)

1. [Forçar um quorum](https://docs.microsoft.com/sql/sql-server/failover-clusters/windows/force-a-wsfc-cluster-to-start-without-a-quorum#PowerShellProcedure) na máquina virtual de saudação restaurada do backup.

1. Atualização de IP de saudação ouvinte tooan IP disponível na rede de failover de teste de saudação.

    ![Atualizar o Ouvinte de IP](./media/site-recovery-sql/update-listener-ip.png)

1. Coloque o ouvinte online.

    ![Colocar o Ouvinte Online](./media/site-recovery-sql/bring-listener-online.png)

1. Crie um balanceador de carga com um IP criado no front-end IP pool tooeach disponibilidade ouvinte de grupo correspondente e máquina virtual do SQL Olá adicionado ao pool de back-end de saudação.

     ![Criar balanceador de carga – pool IP de front-end ](./media/site-recovery-sql/create-load-balancer1.png)

    ![Criar balanceador de carga – pool de back-end ](./media/site-recovery-sql/create-load-balancer2.png)

1. Faça um failover de teste de saudação do plano de recuperação.

### <a name="steps-toodo-a-failover"></a>Etapas toodo um failover

Depois de adicionar script hello no plano de recuperação de saudação e plano de recuperação de saudação validado seguindo um failover de teste, você pode fazer failover saudação do plano de recuperação.


## <a name="integrate-with-sql-server-always-on-for-replication-tooa-secondary-on-premises-site"></a>Integrar com o SQL Server Always On para replicação tooa secundário no site local

Se a saudação do SQL Server estiver usando grupos de disponibilidade para alta disponibilidade (ou uma FCI), é recomendável usar grupos de disponibilidade no site de recuperação de saudação. Observe que isso se aplica a tooapps que não usam transações distribuídas.

1. [Configure bancos de dados](https://msdn.microsoft.com/library/hh213078.aspx) em grupos de disponibilidade.
1. Crie uma rede virtual no site secundário hello.
1. Configure uma conexão de VPN site a site entre a rede virtual hello e site primário hello.
1. Criar uma máquina virtual no site de recuperação hello e instalar o SQL Server.
1. Estender Olá existente sempre em disponibilidade grupos toohello nova VM do SQL Server. Configure essa instância do SQL Server como uma cópia de réplica assíncrona.
1. Criar um ouvinte de grupo de disponibilidade ou atualizar Olá ouvinte tooinclude Olá réplica assíncrona máquina virtual existente.
1. Verifique se o que farm aplicativo hello é configurado com o ouvinte Olá. Se ele estiver configurado usando o nome do servidor de banco de dados de saudação, atualizá-lo ouvinte de saudação toouse, para que você não precise tooreconfigure-lo após o failover de saudação.

Para aplicativos que usam transações distribuídas, recomendamos a implantação do Site Recovery com a [replicação site a site do VMware/servidor físico](site-recovery-vmware-to-vmware.md).

### <a name="recovery-plan-considerations"></a>Considerações sobre o Plano de Recuperação
1. Adicione biblioteca do VMM neste exemplo script toohello, em sites primários e secundários do hello.

        Param(
        [string]$SQLAvailabilityGroupPath
        )
        import-module sqlps
        Switch-SqlAvailabilityGroup -Path $SQLAvailabilityGroupPath -AllowDataLoss -force

1. Quando você cria um plano de recuperação para o aplicativo hello, adicione uma pré ação tooGroup-1 com script etapa, que invoca Olá script toofail sobre grupos de disponibilidade.

## <a name="protect-a-standalone-sql-server"></a>Proteger um SQL Server autônomo

Nesse cenário, recomendamos que você use o computador do SQL Server do Site Recovery replicação tooprotect hello. as etapas exatas Olá dependerão se o SQL Server é uma VM ou um servidor físico e se você quiser tooreplicate tooAzure ou um secundário site local. Saiba mais sobre [cenários do Site Recovery](site-recovery-overview.md).

## <a name="protect-a-sql-server-cluster-standard-editionwindows-server-2008-r2"></a>Proteger um cluster do SQL Server (edição standard/Windows Server 2008 R2)

Para um cluster executando o SQL Server Standard edition ou SQL Server 2008 R2, é recomendável que você use tooprotect de replicação de recuperação de Site do SQL Server.

### <a name="on-premises-tooon-premises"></a>Tooon local no local

* Se o aplicativo hello usa transações distribuídas, é recomendável implantar [recuperação de Site com a replicação SAN](site-recovery-vmm-san.md) para um ambiente Hyper-V, ou [tooVMware do servidor VMware/físicos](site-recovery-vmware-to-vmware.md) para um ambiente VMware.
* Para aplicativos de DTC não, use Olá acima de cluster de saudação do abordagem toorecover como um servidor autônomo, utilizando uma local de alta segurança espelho de banco de dados.

### <a name="on-premises-tooazure"></a>TooAzure local

Recuperação de site não fornece convidado suporte a cluster ao replicar tooAzure. O SQL Server também não fornece uma solução de recuperação de desastres de baixo custo para a edição Standard. Nesse cenário, é recomendável proteger a saudação local do SQL Server cluster tooa autônoma do SQL Server e recuperá-lo no Azure.

1. Configure uma instância do SQL Server autônomo adicionais no site de local de saudação.
1. Configurar Olá instância tooserve como um espelho de saudação bancos de dados você deseja tooprotect. Configure o espelhamento no modo de alta segurança.
1. Configurar a recuperação de Site no site de local de hello, para ([Hyper-V](site-recovery-hyper-v-site-to-azure.md) ou [VMware VMs/servidores físicos)](site-recovery-vmware-to-azure-classic.md).
1. Use a recuperação de Site replicação tooreplicate Olá novo SQL Server instância tooAzure. Como é uma cópia de espelho de alta segurança, ele será sincronizado com o cluster primário hello, mas será replicada tooAzure usando a replicação de recuperação de Site.


![Cluster padrão](./media/site-recovery-sql/standalone-cluster-local.png)

### <a name="failback-considerations"></a>Considerações sobre failback

Para clusters de SQL Server Standard, failback após um failover não planejado exige um backup do SQL server e restauração, a partir de Olá espelho instância toohello cluster original, com restabelecimento do espelho de saudação.

## <a name="next-steps"></a>Próximas etapas
[Saiba mais](site-recovery-components.md) sobre a arquitetura do Site Recovery.
