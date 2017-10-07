---
title: "aaaProtect uma implantação de aplicativos do SAP NetWeaver várias camada usando o Azure Site Recovery | Microsoft Docs"
description: "Este artigo descreve como tooprotect do SAP NetWeaver implantações de aplicativo usando o Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: manayar
ms.openlocfilehash: 34651c7b14d23a44005372f4f923c401e0224231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="protect-a-multi-tier-sap-netweaver-application-deployment-using-azure-site-recovery"></a>Proteger uma implantação de aplicativo SAP NetWeaver de várias camada usando o Azure Site Recovery

A maioria das implantações do SAP de grande e médio porte têm alguma forma de solução de recuperação de desastre.  importância Olá das soluções de recuperação de desastres robustas e podem ser testadas aumentou conforme mais negócios principais processos são movidos tooapplications como SAP.  Recuperação de Site do Azure foi testados e integrados com aplicativos do SAP e exceder as capacidades de saudação da maioria das soluções de recuperação de desastre no local, em um menor custo total de propriedade (TCO) que as soluções da concorrência.
Com o Azure Site Recovery, você pode:
* Habilite a proteção de aplicativos SAP NetWeaver e não seja de produção NetWeaver em execução no local, replicando tooAzure de componentes.
* Habilite a proteção de aplicativos SAP NetWeaver e não seja de produção NetWeaver em execução no Azure, replicando componentes tooanother datacenter do Azure.
* Simplificar a migração para a nuvem, usando recuperação de Site toomigrate seu tooAzure de implantação do SAP.
* Simplifique as atualizações, teste e criação de protótipos de projeto SAP criando um clone de produção sob demanda para testar aplicativos SAP.

Este artigo descreve como tooprotect do SAP NetWeaver implantações de aplicativo usando [do Azure Site Recovery](site-recovery-overview.md). Este artigo aborda as práticas recomendadas de saudação para proteger uma implantação do SAP NetWeaver de três camadas no Azure por meio da replicação tooanother datacenter do Azure usando o Azure Site Recovery, Olá suporte para cenários e configurações, e como tooperform failovers, ambos testar failovers (recuperação de desastre) e failovers real.


## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, certifique-se de que compreender o seguinte hello:

1. [Replicando tooAzure uma máquina virtual](azure-to-azure-walkthrough-enable-replication.md)
2. Como muito[criar uma rede de recuperação](site-recovery-azure-to-azure-networking-guidance.md)
3. [Fazer um tooAzure de failover de teste](azure-to-azure-walkthrough-test-failover.md)
4. [Fazer um failover tooAzure](site-recovery-failover.md)
5. Como muito[replicar um controlador de domínio](site-recovery-active-directory.md)
6. Como muito[replicar do SQL Server](site-recovery-sql.md)

## <a name="supported-scenarios"></a>Cenários com suporte
Com o Azure Site Recovery, você pode implementar uma solução de recuperação de desastres para Olá os seguintes cenários:
* Sistemas SAP em execução em um datacenter do Azure replicando tooanother datacenter do Azure (recuperação de desastres do Azure para o Azure), conforme o projetado [aqui](https://aka.ms/asr-a2a-architecture).
* Sistemas SAP em execução nos servidores VMWare (ou físico) replicação site tooa DR em um datacenter do Azure (VMware para o Azure DR), que exige alguns componentes adicionais como projetado local [aqui](https://aka.ms/asr-v2a-architecture).
* Sistemas SAP em execução no Hyper-V Replica site tooa DR em um datacenter do Azure (Hyper-V para Azure DR), que exige alguns componentes adicionais como projetado local [aqui](https://aka.ms/asr-h2a-architecture).

Este documento usa recursos de recuperação de desastres SAP Olá primeiro caso - DR do Azure para o Azure - toodemonstrate do Azure Site Recovery. Como a replicação do Azure Site Recovery é independente do aplicativo, o processo de Olá descrito é toohold esperado para outros cenários bem.

### <a name="required-foundation-services"></a>Serviços básicos necessários
Neste cenário de documentação todos foi implantado com hello serviços foundation implantados a seguir:
* ExpressRoute ou VPN (Rede Virtual Privada) Site a Site
* Pelo menos um Controlador de Domínio do Active Directory e um servidor DNS em execução no Azure

É recomendável que a infraestrutura Olá acima é estabelecida toodeploying anterior do Azure Site Recovery.


## <a name="typical-sap-application-deployment"></a>Implantação típica do aplicativo SAP
Grandes clientes SAP normalmente implantar entre 6 aplicativos SAP too20 individuais.  A maioria desses aplicativos é baseada em SAP NetWeaver ABAP ou Java mecanismos de saudação.  Dando suporte a esses aplicativos NetWeaver, existem vários mecanismos autônomos e aplicativos específicos que não são SAP NetWeaver.  

É crítico tooinventory a variação de tamanhos de todos os aplicativos de SAP hello, em execução em um cenário e toodetermine Olá modo de implantação (camada 2 ou 3 camadas), versões, patches, taxas e requisitos de persistência do disco.

![Padrão de implantação](./media/site-recovery-sap/sap-typical-deployment.png)

camada de persistência do banco de dados SAP Olá deve ser protegida por meio de ferramentas nativas de DBMS hello como AlwaysOn do SQL Server, Oracle Data Guard ou HANA sistema de replicação. camada de cliente Olá também não está protegida pelo Azure Site Recovery, mas é importante tooconsider tópicos que afetam esta camada como o atraso de propagação de DNS, segurança e acesso remoto toohello data center de recuperação de desastres.

O Azure Site Recovery é hello solução Olá camada de aplicativo, incluindo o (A) SCS recomendada. Outros aplicativos, como aplicativos não é do SAP NetWeaver e SAP não fazem parte de saudação SAP ambiente de implantação geral e também devem ser protegidos com o Azure Site Recovery.

## <a name="replicate-virtual-machines"></a>Replicar máquinas virtuais
Execute [neste guia](azure-to-azure-walkthrough-enable-replication.md) toostart replicando todas Olá toohello de máquinas virtuais de aplicativo SAP do Azure data center de recuperação de desastres.

Se você estiver usando um endereço IP estático, você pode especificar Olá IP que você deseja Olá tootake de máquina virtual na seção de placas de interface de rede de saudação nas configurações de rede e computação.

![IP de Destino](./media/site-recovery-sap/sap-static-ip.png)


## <a name="creating-a-recovery-plan"></a>Criar um plano de recuperação
Um plano de recuperação permite sequenciamento Olá failover de várias camadas em um aplicativo de várias camada, assim, manter a consistência do aplicativo. Execute as etapas de saudação descritas [aqui](site-recovery-create-recovery-plans.md) ao criar um plano de recuperação para um aplicativo web de várias camadas.

### <a name="adding-scripts-toohello-recovery-plan"></a>Adicionar plano de recuperação de toohello de scripts
Você pode precisar toodo algumas operações em Olá failover de teste de failover/post máquinas virtuais do Azure para seu aplicativos toofunction corretamente. Você pode automatizar a operação de failover Olá post como atualizar a entrada DNS e alterar associações e conexões, adicionando scripts correspondentes no plano de recuperação hello, conforme descrito em [neste artigo](site-recovery-create-recovery-plans.md#add-scripts).

### <a name="dns-update"></a>Atualização de DNS
Se Olá DNS é configurado para a atualização dinâmica de DNS, máquinas virtuais normalmente atualizar Olá DNS com hello novo IP quando eles são iniciados. Se desejar tooadd um tooupdate etapa explícita DNS com hello novos IPs de máquinas virtuais de hello, em seguida, adicione isso [script tooupdate IP no DNS](https://aka.ms/asr-dns-update) como uma ação de postagem em grupos do plano de recuperação.  

## <a name="example-azure-to-azure-deployment"></a>Exemplo de implantação do Azure para o Azure
É representado no diagrama Olá abaixo o cenário de recuperação de desastres do Azure Site Recovery do Azure para o Azure hello:
* Olá Datacenter primário está localizado em Cingapura (Azure sudeste asiático) e hello data center de recuperação de desastres é RAE de Hong Kong (Ásia Oriental do Azure).  Nesse cenário, a Alta Disponibilidade local é fornecida por duas VMs que executam o SQL Server AlwaysOn no modo síncrono em Cingapura.
* Olá ASCS de compartilhamento de arquivo pode ser usado tooprovide HA para Olá SAP pontos de falha únicos. O ASCS de Compartilhamento de Arquivos não requer um disco de cluster compartilhado, e aplicativos como o SIOS não são necessários.
* Proteção de recuperação de desastres para a camada de DBMS Olá é obtida usando a replicação assíncrona.
* Este cenário mostra "simétrico DR" – um termo usado toodescribe uma solução de recuperação de desastres que é uma réplica exata de produção, portanto Olá solução de recuperação de desastres SQL Server tem alta disponibilidade local. Olá uso DR simétrico não é obrigatório para a camada de banco de dados de saudação e muitos clientes aproveitam flexibilidade de saudação de implantações de nuvem toobuild um nó de disponibilidade alta local rapidamente após um evento de recuperação de desastres.
* diagrama de saudação descreve hello SAP NetWeaver ASCS e camada de aplicativo de servidor replicadas pelo Azure Site Recovery.

![Cenário de replicação](./media/site-recovery-sap/sap-replication-scenario.png)

## <a name="doing-a-test-failover"></a>Executar um failover de teste
Execute [neste guia](azure-to-azure-walkthrough-test-failover.md) toodo um failover de teste.

1.  Visite o portal tooAzure e selecione seu Cofre de serviços de recuperação.
2.  Clique no plano de recuperação de saudação criado para aplicativos do SAP (s).
3.  Clique em 'Failover de Teste'.
4.  Selecione o ponto de recuperação e o processo de failover de teste do rede virtual do Azure toostart hello.
5.  Após ambiente secundário hello, você pode executar a validação.
6.  Depois que as validações de saudação estiverem concluídas, clique em 'Failovers de teste de limpeza' e tooclean Olá ambiente.

## <a name="doing-a-failover"></a>Executar um failover
Siga [este guia](site-recovery-failover.md) quando estiver realizando um failover.

1.  Visite o portal tooAzure e selecione seu Cofre de serviços de recuperação.
2.  Clique no plano de recuperação de saudação criado para aplicativos do SAP.
3.  Clique em 'Failover'.
4.  Selecione o processo de failover de saudação de toostart de ponto de recuperação.

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre como criar uma solução de recuperação de desastre para implantações do SAP NetWeaver usando o Azure Site Recovery [neste white paper](http://aka.ms/asr-sap). white paper de saudação também aborda as recomendações para diferentes arquiteturas do SAP, a lista de aplicativos com suporte e tipos de VM para SAP no Azure e descreve possíveis planos de teste para a solução de recuperação de desastres.

Saiba mais sobre [como replicar outras cargas de trabalho](site-recovery-workload.md) usando o Site Recovery.
