---
title: "cargas de trabalho de aaaWhat você podem proteger com o Azure Site Recovery?"
description: "Recuperação de Site do Azure protege seus aplicativos e cargas de trabalho através da coordenação replicação hello, failover e recuperação de máquinas virtuais em locais e servidores físicos tooAzure ou tooa secundário no site local"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: 4953948f-26c0-4699-8fe7-59d3bfc1d3da
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/08/2017
ms.author: raynew
ms.openlocfilehash: cab2e1ce3c2b7b2c5f899d957219f5c12eb5965c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-workloads-can-you-protect-with-azure-site-recovery"></a>Quais cargas de trabalho posso proteger com o Azure Site Recovery?
Este artigo descreve as cargas de trabalho e aplicativos que você pode replicar com hello serviço Azure Site Recovery.

Postar comentários e perguntas na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="overview"></a>Visão geral
As organizações precisam uma continuidade de negócios e cargas de trabalho tookeep estratégia de recuperação (BCDR) de desastres e os dados seguros e disponíveis durante o tempo de inatividade planejado e e recuperar tooregular condições de trabalho assim que possível.

Recuperação de site é um serviço do Azure que contribui tooyour estratégia BCDR. Com a recuperação de Site, você pode implantar a replicação com reconhecimento de aplicativos toohello nuvem ou site secundário tooa. Se seus aplicativos são Windows ou com base em Linux, em execução em servidores físicos, VMware ou Hyper-V, você pode usar a replicação do Site Recovery tooorchestrate, executar testes de recuperação de desastres e executar failovers e failback.

O Site Recovery se integra aos aplicativos da Microsoft, incluindo o SharePoint, o Exchange, o Dynamics, o SQL Server e o Active Directory. Microsoft também trabalha em conjunto com os principais fornecedores, inclusive Oracle, SAP, IBM e Red Hat. Você pode personalizar soluções de replicação em uma base por aplicativo.

## <a name="why-use-site-recovery-for-application-replication"></a>Por que usar o Site Recovery para a replicação do aplicativo?
Recuperação de site contribuição tooapplication nível proteção e recuperação da seguinte maneira:

* Independente do aplicativo, fornecer replicação para quaisquer cargas de trabalho em execução em um computador com suporte.
* Replicação quase síncrona, com RPOs tão baixos quanto necessidades de saudação toomeet 30 segundos mais importantes de aplicativos de negócios.
* Instantâneos consistentes de aplicativos para os aplicativos simples ou multicamadas.
* Integração com o SQL Server AlwaysOn e parceria com outras tecnologias de replicação em nível de aplicativo, incluindo a replicação do Active Directory, o SQL AlwaysOn, os DAGs (Grupos de Disponibilidade de Banco de Dados do Exchange) e o Oracle Data Guard.
* Planos de recuperação flexível, que permitem a você toorecover um aplicativo inteiro com um único clique de pilha e incluir scripts externos tooinclude e ações manuais no plano de saudação.
* Gerenciamento de rede na recuperação de Site e o Azure toosimplify avançado requisitos de rede do aplicativo, incluindo endereços IP do hello capacidade tooreserve, configurar balanceamento de carga e a integração com o Azure Traffic Manager, para switchovers de rede baixos RTO.
* Uma biblioteca de automação avançada que fornece scripts específicos do aplicativo, prontos para a produção, que pode ser baixada e integrada nos planos de recuperação.

## <a name="workload-summary"></a>Resumo de carga de trabalho
O Site Recovery pode replicar qualquer aplicativo em execução em um computador com suporte. Além disso, uma parceria com toocarry de equipes de produto adicionais teste de aplicativo específico.

| **Carga de trabalho** | **Site secundário do replicar máquinas virtuais do Hyper-V tooa** | **Replicar máquinas virtuais do Hyper-V tooAzure** | **Site secundário do replicar máquinas virtuais do VMware tooa** | **Replicar máquinas virtuais do VMware tooAzure** |
| --- | --- | --- | --- | --- |
| Active Directory, DNS |S |S |S |S |
| Aplicativos Web (IIS, SQL) |S |S |S |S |
| System Center Operations Manager |S |S |S |S |
| Sharepoint |S |S |S |S |
| SAP<br/><br/>Replicar SAP site tooAzure para não clusterizado |Y (testado pela Microsoft) |Y (testado pela Microsoft) |Y (testado pela Microsoft) |Y (testado pela Microsoft) |
| Exchange (não DAG) |S |S |S |S |
| Área de Trabalho Remota/VDI |S |S |S |N/D |
| Linux (sistema operacional e aplicativos) |Y (testado pela Microsoft) |Y (testado pela Microsoft) |Y (testado pela Microsoft) |Y (testado pela Microsoft) |
| Dynamics AX |S |S |S |S |
| Dynamics CRM |S |Em breve |S |Em breve |
| Oracle |Y (testado pela Microsoft) |Y (testado pela Microsoft) |Y (testado pela Microsoft) |Y (testado pela Microsoft) |
| Servidor de arquivos do Windows |S |S |S |S |
| Citrix XenApp e XenDesktop |N/D |S |N/D |S |

## <a name="replicate-active-directory-and-dns"></a>Replicar o Active Directory e o DNS
Uma infraestrutura do Active Directory e DNS são aplicativos de empresa toomost essenciais. Durante a recuperação de desastres, você precisa tooprotect e recuperar esses componentes de infraestrutura, antes de recuperar seus aplicativos e cargas de trabalho.

Você pode usar a recuperação de Site toocreate um plano de recuperação de desastres automatizada completa para Active Directory e DNS. Por exemplo, se você quiser toofail através do SharePoint e do SAP de um site secundário tooa primário, você pode configurar um plano de recuperação que faz o failover do Active Directory pela primeira vez, e, em seguida, uma recuperação específica de aplicativo adicional planejar toofail sobre Olá outros aplicativos que dependem do Active Diretório.

[Saiba mais](site-recovery-active-directory.md) sobre como proteger o Active Directory e o DNS.

## <a name="protect-sql-server"></a>Proteger o SQL Server
O SQL Server fornece uma base de serviços de dados para muitos aplicativos de negócios em um datacenter local.  Recuperação de site pode ser usada junto com as tecnologias HA/DR do SQL Server, aplicativos de várias camadas enterprise tooprotect que usam o SQL Server. A Recuperação de Site fornece:

* Uma solução de recuperação de desastre simples e econômica para o SQL Server. Replica várias versões e edições de servidores do SQL Server autônomos e clusters, tooAzure ou tooa site secundário.  
* Integração com grupos de disponibilidade de AlwaysOn do SQL, toomanage failover e failback com planos de recuperação do Azure Site Recovery.
* Planos de recuperação de ponta a ponta para Olá todas as camadas em um aplicativo, incluindo bancos de dados do SQL Server hello.
* Escala do SQL Server para as cargas de pico com o Site Recovery "disparando-as" em máquinas virtuais IaaS maiores no Azure.
* Teste fácil de recuperação de desastres do SQL Server. Você pode executar failovers de teste tooanalyze dados e executar verificações de conformidade, sem afetar seu ambiente de produção.

[Saiba mais](site-recovery-sql.md) sobre como proteger o SQL Server.

## <a name="protect-sharepoint"></a>Proteger o SharePoint
O Azure Site Recovery ajuda a proteger as implantações do SharePoint, da seguinte forma:

* Elimina a necessidade de saudação e custos de infraestrutura associadas para um farm de modo de espera para recuperação de desastres. Use a recuperação de Site tooreplicate um site de chamadas secundário tooAzure ou tooa toda a farm (camadas da Web, aplicativo e banco de dados).
* Simplifica a implantação e o gerenciamento de aplicativos. Site primário do toohello atualizações implantadas são replicadas automaticamente e, portanto, estão disponível depois do failover e recuperação de um farm em um site secundário. Também reduz a complexidade hello e os custos associados ao manter um farm espera atualizados.
* Simplifica o desenvolvimento de aplicativos do SharePoint e teste criando um ambiente de réplica sob demanda com cópia de produção para o teste e a depuração.
* Simplifica a nuvem de toohello transição usando tooAzure de implantações do Site Recovery toomigrate do SharePoint.

[Saiba mais](site-recovery-sharepoint.md) sobre como proteger o SharePoint.

## <a name="protect-dynamics-ax"></a>Proteger o Dynamics AX
O Azure Site Recovery ajuda a proteger sua solução ERP do Dynamics AX:

* Orquestração de replicação do seu ambiente do Dynamics AX inteira (camadas Web e AOS, camadas de banco de dados, do SharePoint) tooAzure, ou tooa no site secundário.
* Simplificar a migração de nuvem do Dynamics AX implantações toohello (Azure).
* Simplificando o desenvolvimento de aplicativos Dynamics AX e teste criando uma cópia de produção sob demanda para o teste e a depuração.

[Saiba mais](site-recovery-dynamicsax.md) sobre como proteger o Dynamic AX.

## <a name="protect-rds"></a>Proteger o RDS
Serviços de área de trabalho remota (RDS) permite que a infraestrutura de área de trabalho virtual (VDI), áreas de trabalho baseadas em sessão e aplicativos, permitindo que os usuários toowork em qualquer lugar. Com o Azure Site Recovery, você pode:

* Replica o site secundário do tooa gerenciados ou não em pool áreas de trabalho virtuais e aplicativos e sessões tooa local remoto secundário ou no Azure.
* Aqui está o que você pode replicar:

| **RDS** | **Site secundário do replicar máquinas virtuais do Hyper-V tooa** | **Replicar máquinas virtuais do Hyper-V tooAzure** | **Site secundário do replicar máquinas virtuais do VMware tooa** | **Replicar máquinas virtuais do VMware tooAzure** | **Site secundário do tooa replicar servidores físicos** | **Replicar tooAzure servidores físicos** |
| --- | --- | --- | --- | --- | --- | --- |
| **Área de trabalho virtual em pool (não gerenciada)** |Sim |Não |Sim |Não |Sim |Não |
| **Área de trabalho virtual em pool (gerenciada e sem UPD)** |Sim |Não |Sim |Não |Sim |Não |
| **Aplicativos remotos e sessões da área de trabalho (sem UDP)** |Sim |Sim |Sim |Sim |Sim |Sim |

[Saiba mais](https://gallery.technet.microsoft.com/Remote-Desktop-DR-Solution-bdf6ddcb) sobre como proteger o RDS.

## <a name="protect-exchange"></a>Proteger o Exchange
O Site Recovery ajuda a proteger o Exchange da seguinte maneira:

* Para pequenas implantações do Exchange, como servidores de um único ou autônoma, recuperação de Site pode replicar e fazer failover tooAzure ou tooa site secundário.
* Para as implantações maiores, o Site Recovery integra-se ao Exchange DAGS.
* Exchange DAGs são Olá recomendado de solução de recuperação de desastres do Exchange em uma empresa.  Planos de recuperação de recuperação de site podem incluir DAGs, tooorchestrate DAG failover entre sites.

[Saiba mais](https://gallery.technet.microsoft.com/Exchange-DR-Solution-using-11a7dcb6) sobre como proteger o Exchange.

## <a name="protect-sap"></a>Proteger o SAP
Use recuperação de Site tooprotect sua implantação do SAP, da seguinte maneira:

* Habilite a proteção de aplicativos SAP NetWeaver e não seja de produção NetWeaver em execução no local, replicando tooAzure de componentes.
* Habilite a proteção de aplicativos SAP NetWeaver e não seja de produção NetWeaver em execução no Azure, replicando componentes tooanother datacenter do Azure.
* Simplificar a migração para a nuvem, usando recuperação de Site toomigrate seu tooAzure de implantação do SAP.
* Simplifique as atualizações, teste e criação de protótipos de projeto SAP criando um clone de produção sob demanda para testar aplicativos SAP.

[Saiba mais](site-recovery-sap.md) sobre como proteger o SAP.

## <a name="protect-iis"></a>Proteger o IIS
Use tooprotect de recuperação de Site a implantação do IIS, como segue:

Recuperação de Site do Azure fornece recuperação de desastres por meio da replicação componentes essenciais Olá ambiente tooa cold site remoto ou uma nuvem pública, como o Microsoft Azure. Desde que a máquina virtual Olá Olá web server e banco de dados de saudação estão sendo replicados toohello site de recuperação, não há nenhum requisito toobackup arquivos de configuração ou certificados separadamente. Olá mapeamentos de aplicativo e dependentes de associações de variáveis de ambiente que são alterados após failover podem ser atualizados por meio de scripts integradas planos de recuperação de desastres hello. Máquinas virtuais sejam ativadas no site de recuperação Olá apenas no caso de saudação de um failover. Isso, recuperação de Site do Azure também ajuda a organizar Olá final tooend failover fornecendo que Olá de recursos a seguir:

-   Desligamento de saudação de sequenciamento e inicialização de máquinas virtuais em Olá várias camadas.
-   Adicionar atualização de tooallow scripts das dependências de aplicativo e associações em máquinas virtuais de saudação depois que elas foram iniciadas para cima. scripts Olá também podem ser o site de recuperação usado tooupdate Olá DNS server toopoint toohello.
-   Alocar endereços toovirtual máquinas pre-failover de IP mapeando redes de saudação primário e de recuperação e, portanto, usam scripts que não é necessário toobe atualizado após failover.
-   Capacidade de um failover de um clique para vários aplicativos web em servidores de web hello, eliminando assim o escopo de saudação de confusão no evento de saudação de um desastre.
-   Planos de recuperação capacidade tootest Olá em um ambiente isolado para recuperação de desastres detalhada.

[Saiba mais](https://aka.ms/asr-iis) sobre como proteger o web farm do IIS.

## <a name="protect-citrix-xenapp-and-xendesktop"></a>Proteger o Citrix XenApp e o XenDesktop
Use recuperação de Site tooprotect suas implantações Citrix XenApp e XenDesktop, da seguinte maneira:

* Habilitar a proteção de saudação implantação Citrix XenApp e XenDesktop, replicando implantação diferentes camadas incluindo (, controlador de entrega do Citrix, vitrine eletrônica servidor, XenApp mestre (VDA), servidor de licença do Citrix XenApp do banco de dados servidor DNS do AD, SQL) tooAzure.
* Simplificar a migração de nuvem, usando seu tooAzure implantação Citrix XenApp e XenDesktop toomigrate de recuperação de Site.
* Simplifique o teste do Citrix XenApp/XenDesktop criando uma cópia de produção sob demanda para teste e depuração.
* Esta solução só é aplicável para áreas de trabalho virtuais do sistema operacional Windows Server e não para áreas de trabalho virtuais de cliente como áreas de trabalho virtuais do cliente ainda não são suportadas para o licenciamento no Azure.
[Saiba mais](https://azure.microsoft.com/pricing/licensing-faq/) sobre licenciamento para áreas de trabalho de cliente/servidor no Azure.

[Saiba mais](site-recovery-citrix-xenapp-and-xendesktop.md) sobre como proteger as implantações Citrix XenApp e XenDesktop. Como alternativa, você pode consultar Olá [white paper da Citrix](https://aka.ms/citrix-xenapp-xendesktop-with-asr) detalhando Olá mesmo.

## <a name="next-steps"></a>Próximas etapas
[Verificar pré-requisitos](site-recovery-prereq.md)
